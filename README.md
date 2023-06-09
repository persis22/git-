# Airflow documentation

## For local testing and deployment:

1. Installation steps for the apache airflow using docker.
 Make sure you have Docker and Docker Compose installed on your system. If not, you can refer to the official Docker documentation to install them. (https://docs.docker.com/get-docker/)
   * Create a directory for your Airflow project and navigate to it using the command line. (ex- mkdir airflow-default - >cd  airflow-default)
   * To deploy Airflow on Docker Compose, you should fetch docker-compose.yaml. Use the below command to download the docker-compose.yaml file.
   ```
   curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.3.3/docker-compose.yaml'
   ```
   ![image](https://github.com/persis22/git-/assets/104055832/b5ba6cd0-47de-46c3-92b2-1019b7d348cf)


   * Open the code editor and check whether docker-compose.yaml file is downloaded or not.
   * open the terminal in vs code 
   * Give the following commands
      ``` 
      mkdir -p ./dags ./logs ./plugins
      ```
      ```			
      echo -e "AIRFLOW_UID=$(id -u)" > .env
      ```
      
      -->The above command creates a .env file and sets the AIRFLOW_UID variable to the user ID of the current user, which can be useful for configuring environment variables in an Airflow project.
      ```
      docker-compose up airflow-init
      ```
      ```
      docker-compose up
      ```
    * By this all the services will be up and running.
      
2. Make sure the airflow web server is running in the terminal after running the ‘airflow-init’ command. 

3. Make sure airflow scheduler is also running as it automatically picks up the DAG within the dag folder and schedules it based on start_date.

4. The web server can now be accessed through local host (http://0.0.0.0:8080) with the default username and password being ‘airflow’ for both.

5. Create a connection using aws_access_key and aws_secret_access_id in the airflow by navigating to admin > conections > new in airflow web UI.

    * Connection_id: s3_conn
    * Connection_type : Amazon s3
    * Description : -
    * Host: -
    * Schema : -
    * Login : -
    * Password : -
    * Port : -
    * Extras : {"aws_access_key_id": "your_aws_access_key_id", "aws_secret_access_key": "your_aws_secret_access_key"}


6. Make sure the AWS credentials are correct and has appropriate permissions as this connection allows us to access S3 files locally.

7. Copy the scripts into airflow > dags folder.

8. Now the dags will be present and can be seen in the airflow web UI.

9. Run the DAG manually by triggering it for local testing.


## For production-level deployment:

1. Push the code into the necessary repository. 

2. Set up a continuous integration/continuous deployment (CI/CD) pipeline to automatically deploy the DAG file to the production DAG directory.

3. Make sure the AWS credentials are correct and has appropriate permissions.

4. Validate the DAG file using the airflow dags validate command to ensure there are no configuration issues.

5. Access the Airflow web UI to monitor the execution of the each DAG.

6. Create a connection using aws_access_key and aws_secret_access_id in the airflow by navigating to admin > conections > new in airflow web UI.

    * Connection_id: s3_conn
    * Connection_type : Amazon s3
    * Description : -
    * Host: -
    * Schema : -
    * Login : -
    * Password : -
    * Port : -
    * Extras : {"aws_access_key_id": "your_aws_access_key_id", "aws_secret_access_key": "your_aws_secret_access_key"}

7. Review the DAG run history, logs, and task statuses to ensure everything is running smoothly.

