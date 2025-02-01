# Flask-deployment-With-Docker-Trial
A simple deployment of a flask backend with postgres and nginx with SSL on docker

This README provides instructions on how to run containers using Docker Compose, including building images and making necessary changes to some files before deployment.

## Prerequisites
- Install [Docker](https://docs.docker.com/get-docker/)
- Install [Docker Compose](https://docs.docker.com/compose/install/)

## Steps to Run Containers

### 1. Clone the Repository
```sh
git clone https://github.com/Marius-Mulama/Flask-deployment-With-Docker-Trial.git
cd Flask-deployment-With-Docker-Trial
```

### 2. Update Configuration Files
Before running the containers, make necessary changes to the following files:
- **nginx-certbot.env**: Add Your Email address so that you can get ssl certificate 
- **myapp.conf**: replace domain name to your domain name or subdomain name
- If running on Linux, ensure that the file paths in `compose.yml` have `./` before the file names. Example:
  ```yaml
  configs:
    my_config:
      file: ./flask/config-dev.yaml
    nginx_config:
      file: ./nginx.conf
    myapp_config:
      file: ./myapp.conf
  ```



### 3. Build the Docker Images
Run the following command to build the images before running the containers:
```sh
docker compose build
```

### 4. Start the Containers
Once the build is complete, start the containers with:
```sh
docker compose up -d
```
The `-d` flag runs the containers in detached mode.

### 5. Check Running Containers
To verify that all containers are running:
```sh
docker ps
```

### 6. Access PostgreSQL Service and Create a Table
To access the PostgreSQL service and create a table, follow these steps:
```sh
docker exec -it <postgres_container_name> psql -U <postgres_user> -d <database_name>
```
Once inside the PostgreSQL prompt, create a table:
```sql
CREATE TABLE tasks (
    item_id SERIAL PRIMARY KEY,
    priority INT,
    task TEXT
);
```
To exit the PostgreSQL shell, type:
```sql
\q
```

### 7. Stopping Containers
To stop and remove the running containers:
```sh
docker-compose down
```

### 8. Logs and Debugging
- View logs:
```sh
docker-compose logs -f
```
- Restart a specific container:
```sh
docker-compose restart <container_name>
```

### 9. Rebuilding and Restarting
If changes are made to the Dockerfile or application code, rebuild and restart:
```sh
docker-compose up --build -d
```

## Notes
- Ensure any required dependencies are installed before running.
- If using a database, check if migrations need to be applied.
- Use `docker volume ls` and `docker volume rm <volume_name>` if persistent volumes need to be cleaned.

## Troubleshooting
- If encountering permission issues, try running commands with `sudo`.
- If a container fails to start, check logs using `docker-compose logs <container_name>`.
- Ensure ports specified in `docker-compose.yml` are not already in use.

---
This Documentation written at 3AM on a saturday so there can be errors inside but IT WORKED ON MY MACHINE and also an ubuntu EC2 Virtual Machine. Incase of errors chatgpt it first if no solution Im happy to address.

For any additional support, refer to the official [Docker Compose documentation](https://docs.docker.com/compose/).

