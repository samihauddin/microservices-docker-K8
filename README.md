### What is Microservices?

Microservices is an architectural style that structures an application as a collection of small, loosely coupled services.

These services are designed to be highly maintainable, testable, and scalable. 

### What is Docker?

Docker is a platform for developing, shipping, and running applications inside containers. 

Containers are lightweight, portable, and self-sufficient units that can run applications and their dependencies. 

### Benefits of Docker for a business?

- **Easy Portability:** Applications can run on any machine without compatibility issues.

- **Isolation and Security:** Applications run securely without interfering with each other.

- **Efficient Resource Use:** Maximizes the use of server resources, saving costs.

- **Quick Deployment:** Applications can be deployed rapidly, responding to demand swiftly.

- **Scalability:** Easy to scale up or down based on workload.

- **Version Control:** Keeps track of changes and allows easy rollback if issues occur.

- **Simplified Testing:** Eases testing in various environments without complications.

### How does Docker work?

### Setting up Docker 

Check if Docker is installed:
```
# Check if Docker is instlled 
docker

# Check Docker version
docker --version
```

Build an image:
```
docker build -t <image name>
```

List all Docker images:
```
docker images
```

Run a Docker container:
```
docker run
```
List all running containers:
```
docker ps
```
List all containers:
```
docker ps -a
```
Stop a running container:
```
docker stop <container ID>
```
Remove a container:
```
docker rm <container ID> -f
```
Remove an image:
```
docker rmi <image name> -f
```
Push an Image:
```
docker push <image name>
```
Running a command inside a Docker container:
```
docker exec -it <ID> sh
apt update -y
apt upgrade -y
apt install sudo
apt install nano

cd /usr
cd share
cd nginx
cd html

pwd
ls
cat index.html
sudo nano index.html
```
### Building an Image and Pushing to Docker Hub

1. Create an index.html file locally and save
```
<h1>Samiha Uddin</h1>
<p>Samiha is a driven and dedicated Psychology graduate with a strong desire and determination to advance in the Technology sector.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```
2. Create a default file 
```
server {
    listen 80 default_server;
    listen [::]:80 default_server;
    
    root /usr/share/nginx/html;
    index index.html index.htm;

    server_name _;
    location / {
        try_files $uri $uri/ =404;
    }
}
```
3. In your dockerfile enter the following:
```
FROM ubuntu:18.04  
LABEL maintainer="samihauddin@live.co.uk" 
RUN  apt-get -y update && apt-get -y install nginx
COPY files/default /etc/nginx/sites-available/default
COPY files/index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
```
4. Build your image
```
docker build -t imagename .
```
5. Check if image has been created
```
docker images
docker run -d -p 81:80 samiha-image:v1
docker login
```
6. Create a tag
```
docker tag samiha-image:v1 samihauddin/samiha-image:v1
```
7. Push your image to DockerHub
```
docker push samihauddin/samiha-image:v1
```

**Successful Output**

![alt text](Images/so.png)