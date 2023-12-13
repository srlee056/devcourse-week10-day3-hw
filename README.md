# airflow.cfg

1. DAGs 폴더는 어디에 지정되는가?
    - `dags_folder`
   
    ```bash
    dags_folder = /var/lib/airflow/dags
    ```
    
2. DAGs 폴더에 새로운 Dag를 만들면 언제 실제로 Airflow 시스템에서 이를 알게되나? 이 스캔 주기를 결정해주는 키의 이름이 무엇인가?
    - `dag_dir_list_interval`, 300초=5분 마다 DAG 폴더를 스캔해 새로운 파일을 찾아낸다.
   
    ```bash
    dag_dir_list_interval = 300
    ```
    
3. 이 파일에서 Airflow를 API 형태로 외부에서 조작하고 싶다면 어느 섹션을 변경해야하는가?
    - `[api] - auth_backends` 를 수정하여 API 형태로 조작할 수 있다.

    ```bash
    auth_backends = airflow.api.auth.backend.session
    ```
    - 참고 : <https://airflow.apache.org/docs/apache-airflow/stable/security/api.html>
    
4. Variable에서 변수의 값이 encrypted가 되려면 변수의 이름에 어떤 단어들이 들어가야 하는데 이 단어들은 무엇일까? :)
    - 다음 단어들이 변수 이름에 포함되면 그 값은 encrypted 된다.
      
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

    - 참고 : <https://airflow.apache.org/docs/apache-airflow/stable/security/secrets/mask-sensitive-values.html>
    
5. 이 환경설정파일이 수정되었다면 이를 실제로 반영하기 위해서 해야 하는 일은?
    - airflow 웹서버와 스케쥴러 프로세스를 재실행한다.
      
    ```bash
    sudo systemctl restart airflow-webserver
    sudo systemctl restart airflow-scheduler
    ```
    
6. Metadata DB의 내용을 암호화하는데 사용되는 키는 무엇인가?
    - `fernet_key`를 통해 암호화할 수 있다.
   
    ```bash
    [core]
    # Secret key to save connection passwords in the db
    fernet_key =
    ```

    - 참고 : <https://airflow.apache.org/docs/apache-airflow/1.10.13/howto/secure-connections.html>
