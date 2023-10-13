# Hands-on: Docker Storage

# Start the AWS EC2 instance running Docker

Access AWS, navigate to EC2, and then start the VM created for Docker usage.

# Cleaning the Environment:

Clean your Docker environment:

```
docker system prune -a -f --volumes

```

Create a new directory and switch to it:

```
mkdir docker-volumes
cd docker-volumes

```

Download zip file with hands-on task files. Unzip it:

```
wget https://tcb-bootcamps.s3.amazonaws.com/tcb5001-devopscloud-bootcamp/v2/module5-docker/files/module5-docker.zip

sudo apt install unzip

unzip module5-docker.zip
cd handsontask/volumes
```

Build the Docker image:

```
docker build . -t tcb-img-upload-file:v1.0

```

Check your Docker images:

```
docker images

```

# Running Container without Data Persistence:

```
docker run --rm -d -p 8081:3000 --name ctr-upload-file tcb-img-upload-file:v1.0

```

List files in the container and uploads directory:

```
docker exec <containerid> ls
ls uploads

```

Stop the container:

```
docker stop <containerid>

```

Run the container again:

```
docker run --rm -d -p 8081:3000 --name ctr-upload-file tcb-img-upload-file:v1.0
```

List files in the container and uploads directory:

```
docker exec <containerid> ls
ls uploads

```

# Creating a Volume:

List Docker volumes:

```
docker volume ls

```

Create a Docker volume:

```
docker volume create upload-files

```

List Docker volumes:

```
docker volume ls

```

Inspect where Docker stores all its data:

```
sudo ls -l /var/lib/docker/volumes

```

Stop the container:

```
docker stop <containerid>

```

# Volume Persistence Managed by Docker:

Run the container with a Docker volume:

```
docker run --rm -d -p 8081:3000 --name ctr-upload-file -v upload-files:/app/uploads tcb-img-upload-file:v1.0

```

Inspect the volume in the container:

```
docker inspect <containerid> | grep volume

```

Upload a new file

List files in the container and uploads directory:

```
docker exec <containerid> ls
ls uploads

```

Stop the container:

```
docker stop <containerid>

```

Run the container with the Docker volume again:

```
docker run --rm -d -p 8081:3000 --name ctr-upload-file -v upload-files:/app/uploads tcb-img-upload-file:v1.0

```

# Bind Mount - Folder/Directory Persistence Managed by You:

Stop the container:

```
docker stop <containerid>

```

Create a backup directory and get the current path:

```
mkdir bkp-upload
pwd

```

Run the container with a bind mount:

```
docker run --rm -d -p 8081:3000 --name ctr-upload-file -v /home/ubuntu/docker-volumes/handsontask/volumes/bkp-upload:/app/uploads tcb-img-upload-file:v1.0

```

# Updating an Application File in Real Time without Building Image Process:

Stop the container:

```
docker stop <containerid>

```

Run the container with a bind mount to the `templates` directory: