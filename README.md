# airflow-2-docker-setup

This project contains a docker-compose file and instructions to setup Airflow 2 on a single Linux (Ubuntu 20.04) machine. The file is completely based on the official installation guide of Airflow with Docker, which can be found [here](https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html). Personally I used to [Portainer](https://www.portainer.io/) `stacks` instead of docker-compose but you should be able to get Airflow 2 up and running with the file and instructions. If not, please have a look at the Airflow documentation for further assistance.

## Instructions

Before you run `docker-compose` you have to make and prepare a few folders from your home directory.

```bash
cd ~ 
mkdir airflow && cd airflow
mkdir dags logs plugins tmp
chmod 777 logs
``` 

The reason that we need to change the `write` mode of the `logs` folder to 'the world' is that it allows Airflow to write the logs to this folder. The `tmp` folder is added so you have a folder to store your data from local projects without messing up the other folders. You also need to modify the `docker-compose.yaml` file with your user name and user id. In case you are not aware of these variables enter the following command.

```bash
echo $USER $UID
```

Please note that the setup is meant for local use only, therefore the username and password for Postgres and Airflow are standard, and the exposed port is only published to the local port.

```yaml
      airflow-webserver:
        <<: *airflow-common
        command: webserver
        ports:
          - 127.0.0.1:8080:8080
``` 

You are now ready to run `docker-compose`. When up and running you can store your local dags in the `dags` folder and they should become visible pretty quickly in the Airflow UI, which you can reach by browsing to `localhost:8080`.