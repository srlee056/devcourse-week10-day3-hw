# airflow.cfg

1. DAGs 폴더는 어디에 지정되는가?
    
    ```bash
    dags_folder = /var/lib/airflow/dags
    ```
    
2. DAGs 폴더에 새로운 Dag를 만들면 언제 실제로 Airflow 시스템에서 이를 알게되나? 이 스캔 주기를 결정해주는 키의 이름이 무엇인가?
    
    ```bash
    # How often (in seconds) to scan the DAGs directory for new files. Default to 5 minutes.
    dag_dir_list_interval = 300
    ```
    
3. 이 파일에서 Airflow를 API 형태로 외부에서 조작하고 싶다면 어느 섹션을 변경해야하는가?
    
    https://airflow.apache.org/docs/apache-airflow/stable/security/api.html
    
    ```bash
    # Enables the deprecated experimental API. Please note that these APIs do not have access control.
    # The authenticated user has full access.
    #
    # .. warning::
    #
    #   This `Experimental REST API <https://airflow.readthedocs.io/en/latest/rest-api-ref.html>`__ is
    #   deprecated since version 2.0. Please consider using
    #   `the Stable REST API <https://airflow.readthedocs.io/en/latest/stable-rest-api-ref.html>`__.
    #   For more information on migration, see
    #   `RELEASE_NOTES.rst <https://github.com/apache/airflow/blob/main/RELEASE_NOTES.rst>`_
    enable_experimental_api = False
    
    # Comma separated list of auth backends to authenticate users of the API. See
    # https://airflow.apache.org/docs/apache-airflow/stable/security/api.html for possible values.
    # ("airflow.api.auth.backend.default" allows all requests for historic reasons)
    auth_backends = airflow.api.auth.backend.session
    ```
    
4. Variable에서 변수의 값이 encrypted가 되려면 변수의 이름에 어떤 단어들이 들어가야 하는데 이 단어들은 무엇일까? :)
    
    참고 : https://airflow.apache.org/docs/apache-airflow/stable/security/secrets/mask-sensitive-values.html
    
    ```bash
    ‘access_token’
    ‘api_key’
    ‘apikey’
    ’authorization’
    ‘passphrase’
    ‘passwd’
    ‘password’
    ‘private_key’
    ‘secret’
    ‘token’
    ```
    
    ```bash
    # Hide sensitive Variables or Connection extra json keys from UI and task logs when set to True
    #
    # (Connection passwords are always hidden in logs)
    hide_sensitive_var_conn_fields = True
    
    # A comma-separated list of extra sensitive keywords to look for in variables names or connection's
    # extra JSON.
    sensitive_var_conn_names =
    ```
    
5. 이환경설정파일이수정되었다면이를실제로반영하기위해서해야하는 일은?
    
    ```bash
    sudo systemctl restart airflow-webserver
    sudo systemctl restart airflow-scheduler
    ```
    
6. Metadata DB의 내용을 암호화하는데 사용되는 키는 무엇인가?
    
    https://airflow.apache.org/docs/apache-airflow/1.10.13/howto/secure-connections.html
    
    ```bash
    [core]
    # Secret key to save connection passwords in the db
    fernet_key =
    ```
