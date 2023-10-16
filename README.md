# Rail Fence Cipher

## Background
During the execution of this activity, I decided to use HTML to minimize the complexity of using containers for displaying results.


## Encrypt
## Specifications

The code will ignore spaces and will convert all input is lower case.

## How to execute the Rail Fence Cipher

Create a Dockerfile file with the following instructions for downloading and adjusting the configurations inside the container to work using port 8181. If you wish to modify this port, you can do so directly here.
```html
# Use the official NGINX image as the base image
FROM nginx

# Replace the default NGINX configuration with a custom configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Create a directory for the HTML file
WORKDIR /usr/share/nginx/html

# Download the decrypt.html file and save it as index.html
RUN apt-get update && apt-get install -y wget && \
    wget https://raw.githubusercontent.com/deimergruesobar/741Crypto/main/encrypt.html -O index.html && \
    apt-get remove --purge -y wget && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Expose port 8181
EXPOSE 8181

# Start NGINX
CMD ["nginx", "-g", "daemon off;"]
```

It is necessary to include the Nginx configuration file in the same folder where the Dockerfile is located so that it can operate using the previously defined port. Define the file nginx.conf with the next config:
```
server {
    listen 8181;
    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        index index.html;
    }

    location /favicon.ico {
        alias /usr/share/nginx/html/favicon.ico;
    }
}
```
From a command console, locate the folder that contains the Dockerfile file and the nginx.conf and execute the builds command; in this case, I am associating the execution so that it can be later uploaded to my repository in DockerHub.

```bash
docker build -t deimergrueso/nginx-encrypt:latest .
```
Sending the new container image to DockerHub
```bash
docker push deimergrueso/nginx-encrypt:latest
```
## Usage
The use of this container is limited only to executing the image previously created or downloaded from DockerHub. To do this, execute from the command line:
```bash
docker run -d -p 8181:8181 --name encrypt deimergrueso/nginx-encrypt:latest
```
![Alt text](https://github.com/deimergruesobar/741Crypto/blob/main/Img/Docker_Encrypt_ps.png)

Go to the web browser using your computer's IP address or using localhost:8181 as the destination address

![Alt text](https://github.com/deimergruesobar/741Crypto/blob/main/Img/UI_Encryption.png)

## Decrypt
## Specifications

The code will ignore spaces and will convert all input is lower case.

## How to execute the Rail Fence Cipher Decryption 

Create a Dockerfile file with the following instructions for downloading and adjusting the configurations inside the container to work using port 8080. If you wish to modify this port, you can do so directly here.
```dockerfile
# Use the official NGINX image as the base image
FROM nginx

# Replace the default NGINX configuration with a custom configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Create a directory for the HTML file
WORKDIR /usr/share/nginx/html

# Download the decrypt.html file and save it as index.html
RUN apt-get update && apt-get install -y wget && \
    wget https://raw.githubusercontent.com/deimergruesobar/741Crypto/main/decrypt.html -O index.html && \
    apt-get remove --purge -y wget && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Expose port 8080
EXPOSE 8080

# Start NGINX
CMD ["nginx", "-g", "daemon off;"]
```

It is necessary to include the Nginx configuration file in the same folder where the Dockerfile is located so that it can operate using the previously defined port. Define the file nginx.conf with the next config:
```
server {
    listen 8080;
    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        index index.html;
    }

    location /favicon.ico {
        alias /usr/share/nginx/html/favicon.ico;
    }
}
```
From a command console, locate the folder that contains the Dockerfile file and the nginx.conf and execute the builds command; in this case, I am associating the execution so that it can be later uploaded to my repository in DockerHub.

```bash
docker build -t deimergrueso/nginx-decrypt:latest .
```
Sending the new container image to DockerHub
```bash
docker push deimergrueso/nginx-decrypt:latest
```
## Usage
The use of this container is limited only to executing the image previously created or downloaded from DockerHub. To do this, execute from the command line:
```bash
docker run -d -p 8080:8080 --name decrypt deimergrueso/nginx-decrypt:latest
```
![Alt text](https://github.com/deimergruesobar/741Crypto/blob/main/Img/Docker_Decrypt_ps.png)


Go to the web browser using your computer's IP address or using localhost:8080 as the destination address

![Alt text](https://github.com/deimergruesobar/741Crypto/blob/main/Img/UI_Decryption.png)


## Testing 


Encrypt using (4,5): “CRYPTOLOGY IS THE PRACTICE AND STUDY OF TECHNIQUES FOR SECURE COMMUNICATION IN THE PRESENCE OF THIRD PARTIES CALLED ADVERSARIES”
![Alt text](https://github.com/deimergruesobar/741Crypto/blob/main/Img/UI_Decryption.png)

Decrypt using (3): “TPSNIONFRMHANOIREEOIBTSEAKLAPSEHISOBPEGTBRQREPTTMHRTHTTAWE AACTFVAECAOLHANSEEKFHALOITUEEAICNLEYOLTOLEPADFKATATSJMSIINSH ROCTITRIEEAKYNHYUEOTTSTATSIIRSARERUYUEDPCLETEROINEIYEHC"

![Alt text](https://github.com/deimergruesobar/741Crypto/blob/main/Img/Docker_Decrypt_ps.png)



