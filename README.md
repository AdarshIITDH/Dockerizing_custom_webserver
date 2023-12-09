# Dockerizing_custom_webserver

### Objective:
The objective of this assignment is to familiarize yourself with Docker and containerization by Dockerizing a simple HTML page using Nginx as the web server.

### Requirements:

Install docker in ubuntu machine
```
sudo apt install docker.io -y
```
![image](https://github.com/AdarshIITDH/Dockerizing_custom_webserver/assets/60352729/184a61da-d97b-4c78-badf-499f29d9d748)

1. Basic HTML Page:

   - Create a plain HTML page named `index.html` with some content (e.g., "Hello, Docker!").

```
#------------------index.html---------------------------------
<!DOCTYPE html>
<html>
<head>
    <title>Hello, Docker!</title>
</head>
<body>
    <h1>Hello, Docker!</h1>
    <p>This is a plain HTML page served by Nginx in a Docker container.</p>
</body>
</html>
#-------------------------------------------------------------------
```

2. Nginx Configuration:

   - Create an Nginx configuration file named `nginx.conf` that serves the `index.html` page.

   - Configure Nginx to listen on port 80.
```
#-----------------------------nginx.conf-------------------------
events {}
http {
    server {
        listen 80;
        location / {
            root /usr/share/nginx/html;
            index index.html;
        }
    }
}
#----------------------------------------------------------------
```

3. Dockerfile:

   - Create a `Dockerfile` to define the Docker image.

   - Use an official Nginx base image.

   - Copy the `index.html` and `nginx.conf` files into the appropriate location in the container.

   - Ensure that the Nginx server is started when the container is run.

```
#---------------------------Dockerfile----------------------
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
COPY nginx.conf /etc/nginx/nginx.conf
#-----------------------------------------------------------
```

4. Building the Docker Image:

   - Build the Docker image using the `Dockerfile`.
     
```
docker build -t custom_webserver:v1 -f dockerfile .
```
![image](https://github.com/AdarshIITDH/Dockerizing_custom_webserver/assets/60352729/b35acf2b-7a15-488c-b906-58d7c98ed2ed)

Lets! Test the image
```
docker run -it -d  -p 8080:80 custom_webserver:v1
```

![image](https://github.com/AdarshIITDH/Dockerizing_custom_webserver/assets/60352729/a6c11cb5-d7e3-4990-999a-2578ef1fe0c0)

Its working fine WOW!

5. Push the image on ECR

   - Make the public repository and push them on the ECR

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

apt install unzip
unzip awscliv2.zip
sudo ./aws/install
aws --version


```

```
aws configure

AWS Access Key ID:
AWS secret Acess Key:
Default region name: ap-south-1
Default output format:
```

![image](https://github.com/AdarshIITDH/Dockerizing_custom_webserver/assets/60352729/4dee76ea-f6a1-40a4-acb5-f182ec183fa0)



![image](https://github.com/AdarshIITDH/Dockerizing_custom_webserver/assets/60352729/17a074be-13d1-4782-94b9-1e43cf19b514)


![image](https://github.com/AdarshIITDH/Dockerizing_custom_webserver/assets/60352729/6972a8f3-3f8d-40e2-8a76-e942a2a52c1b)
```
https://gallery.ecr.aws/c3w1m1q2/docker_customwebservice_adarsh
```


