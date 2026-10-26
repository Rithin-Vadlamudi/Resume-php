# Personal Web Resume – Docker Containerization & Deployment

## 1. Application Name

**Personal Web Resume**

This project is a simple PHP-based web resume application that displays personal details. The application is containerized using Docker, published to Docker Hub, and redeployed on an independent Ubuntu Linux virtual machine using the Docker image pulled from Docker Hub.

---

## 2. Project Structure

```text
project/
├── source-code/
│   └── index.php
├── Dockerfile
├── README.md
└── screenshots/
    ├── docker-build.png
    ├── docker-images.png
    ├── docker-ps.png
    ├── browser-v1.png
    ├── dockerhub.png
    └── browser-v2.png
```

---

## 3. Technology Stack

| Component | Technology |
|---|---|
| Programming Language | PHP 8.2 |
| Web Server | Apache |
| Containerization | Docker |
| Container Registry | Docker Hub |
| Virtual Machine | Ubuntu Linux |
| VM Platform | UTM |
| Development Host | macOS |
| Browser | Safari / Firefox |

---

## 4. Dockerfile

The project uses the following Dockerfile:

```dockerfile
FROM php:8.2-apache

COPY source-code/ /var/www/html/

EXPOSE 80

CMD ["apache2-foreground"]
```

### Dockerfile Explanation

### `FROM php:8.2-apache`

Uses the official PHP 8.2 image with Apache web server. This provides the PHP runtime and Apache environment required to run the application.

### `COPY source-code/ /var/www/html/`

Copies the PHP application source code from the project's `source-code` directory into Apache's default web directory inside the container.

### `EXPOSE 80`

Documents that Apache listens on port 80 inside the Docker container.

### `CMD ["apache2-foreground"]`

Starts Apache in the foreground. This allows the Docker container to continue running while serving the PHP application.

---

## 5. Docker Build

### Version 1

The initial Docker image was created using:

```bash
docker build -t webresume:v1 .
```

### Version 2

After modifying the application, a new Docker image was created:

```bash
docker build -t webresume:v2 .
```

The successful image build was verified using:

```bash
docker images
```

---

## 6. Docker Run

### Version 1

The initial application was run locally using:

```bash
docker run -d -p 8080:80 --name webresume-container webresume:v1
```

The application was then accessed through:

```text
http://localhost:8080
```

### Version 2

The final Version 2 image was deployed using:

```bash
docker run -d -p 8080:80 --name webresume-v2 rithinvadlamudi/webresume:v2
```

### Port Mapping

```text
8080:80
```

means:

- `8080` = host/VM port
- `80` = Apache port inside the Docker container

Therefore, requests sent to port `8080` are forwarded to Apache running on port `80` inside the container.

---

## 7. Docker Image Name and Version

### Local Image

```text
webresume:v2
```

### Docker Hub Image

```text
rithinvadlamudi/webresume:v2
```

### Repository

```text
rithinvadlamudi/webresume
```

### Version

```text
v2
```

The `v2` tag identifies the modified version of the application.

---

## 8. Docker Hub Deployment

After creating Version 2, the local image was tagged with the Docker Hub repository name:

```bash
docker tag webresume:v2 rithinvadlamudi/webresume:v2
```

The image was then pushed to Docker Hub:

```bash
docker push rithinvadlamudi/webresume:v2
```

The Docker Hub repository was used as the image registry between the Mac and Ubuntu VM.

---

## 9. Pulling the Image on Ubuntu VM

The Ubuntu VM was running separately from the development Mac.

Docker was installed on the Ubuntu VM and the Docker Hub image was downloaded using:

```bash
docker pull rithinvadlamudi/webresume:v2
```

The downloaded image was verified using:

```bash
docker images
```

Expected image:

```text
rithinvadlamudi/webresume   v2
```

---

## 10. VM Deployment

### Virtual Machine Details

- **Operating System:** Ubuntu Linux
- **Virtualization Platform:** UTM
- **Architecture:** Linux VM running on the Mac
- **VM IP Address:** `192.168.64.3`

The Docker container was created on the Ubuntu VM using:

```bash
docker run -d -p 8080:80 --name webresume-v2 rithinvadlamudi/webresume:v2
```

The running container was verified using:

```bash
docker ps
```

The application was tested from inside the VM using:

```bash
curl http://localhost:8080
```

---

## 11. Application URL

After successful deployment, the application was accessible from the host Mac using:

```text
http://192.168.64.3:8080
```

The application was successfully tested from the Mac using:

```bash
curl http://192.168.64.3:8080
```

The response displayed the Version 2 application content.

---

## 12. Version 2 Changes

The original Version 1 application displayed basic personal information.

For Version 2, the following visible changes were made:

- Added the heading **"My Personal Web Resume"**
- Added the heading **"Dockerized Version 2"**
- Added a Docker deployment confirmation message
- Improved the overall presentation of the application content

The Version 2 application displays:

```text
My Personal Web Resume

My Details

Name: Rithin Vadlamudi
Email: rithinvadlamudi@gmail.com
Phone Number: +91 9390205389

Dockerized Version 2

Application successfully updated and deployed using Docker.
```

---

## 13. Verification

The deployment was verified at multiple stages.

### Check Docker Images

```bash
docker images
```

### Check Running Containers

```bash
docker ps
```

### Test Application Inside VM

```bash
curl http://localhost:8080
```

### Test Application from Mac

```bash
curl http://192.168.64.3:8080
```

### Browser Verification

The application was opened using:

```text
http://192.168.64.3:8080
```

The browser displayed the modified **Dockerized Version 2** application.

---

## 14. Screenshots

The following screenshots are included as part of the submission:

| Screenshot | Purpose |
|---|---|
| `docker-build.png` | Shows successful Docker image build |
| `docker-images.png` | Shows the created Docker image and version |
| `docker-ps.png` | Shows the running Docker container and port mapping |
| `browser-v1.png` | Shows the original Version 1 application |
| `dockerhub.png` | Shows the Version 2 image on Docker Hub |
| `browser-v2.png` | Shows the modified Version 2 application deployed from the Ubuntu VM |

---

## 15. Complete Containerization and Deployment Process

The complete workflow followed in this project is:

### Step 1 – Develop the Application

A simple PHP web resume application was created.

### Step 2 – Create the Dockerfile

A Dockerfile using the official PHP 8.2 Apache image was created.

### Step 3 – Build Version 1

The initial application was converted into a Docker image:

```bash
docker build -t webresume:v1 .
```

### Step 4 – Run Version 1

The application was deployed locally:

```bash
docker run -d -p 8080:80 --name webresume-container webresume:v1
```

The Version 1 application was verified in a browser.

### Step 5 – Modify the Application

The PHP application was modified to create Version 2.

### Step 6 – Build Version 2

The modified application was rebuilt:

```bash
docker build -t webresume:v2 .
```

### Step 7 – Tag Version 2

The image was tagged for Docker Hub:

```bash
docker tag webresume:v2 rithinvadlamudi/webresume:v2
```

### Step 8 – Push to Docker Hub

The image was uploaded:

```bash
docker push rithinvadlamudi/webresume:v2
```

### Step 9 – Pull on Ubuntu VM

The Ubuntu VM downloaded the same image:

```bash
docker pull rithinvadlamudi/webresume:v2
```

### Step 10 – Deploy on Ubuntu VM

The pulled image was run as a container:

```bash
docker run -d -p 8080:80 --name webresume-v2 rithinvadlamudi/webresume:v2
```

### Step 11 – Verify the Container

The running container was checked using:

```bash
docker ps
```

The application was also tested using:

```bash
curl http://localhost:8080
```

### Step 12 – Access from Mac

The application was accessed from the Mac through:

```text
http://192.168.64.3:8080
```

---

## 16. Deployment Flow

```text
PHP Web Resume
       │
       ▼
   Dockerfile
       │
       ▼
Build Docker Image
  webresume:v1
       │
       ▼
Modify Application
       │
       ▼
Build Version 2
  webresume:v2
       │
       ▼
Tag Docker Image
       │
       ▼
Docker Hub
rithinvadlamudi/webresume:v2
       │
       │ docker pull
       ▼
Ubuntu VM
       │
       ▼
Docker Container
webresume-v2
       │
       │ 8080:80
       ▼
http://192.168.64.3:8080
       │
       ▼
Web Browser
```

---

## 17. Key Docker Commands Used

```bash
# Build Version 1
docker build -t webresume:v1 .

# Run Version 1
docker run -d -p 8080:80 --name webresume-container webresume:v1

# Build Version 2
docker build -t webresume:v2 .

# Tag Version 2
docker tag webresume:v2 rithinvadlamudi/webresume:v2

# Push to Docker Hub
docker push rithinvadlamudi/webresume:v2

# Pull on Ubuntu VM
docker pull rithinvadlamudi/webresume:v2

# Run Version 2 on VM
docker run -d -p 8080:80 --name webresume-v2 rithinvadlamudi/webresume:v2

# Verify images
docker images

# Verify running containers
docker ps

# Test application
curl http://localhost:8080
```

---

## 18. Result

The PHP web resume application was successfully:

1. Containerized using Docker.
2. Built as Version 1.
3. Modified and rebuilt as Version 2.
4. Tagged with a Docker Hub repository.
5. Pushed to Docker Hub.
6. Pulled into an independent Ubuntu VM.
7. Deployed as a Docker container.
8. Verified using Docker commands and `curl`.
9. Accessed successfully from the Mac browser through the VM IP address.

---

## 19. Conclusion

This project demonstrates the complete Docker containerization and deployment lifecycle of a PHP web application.

The application was first containerized and tested locally. After creating Version 2, the Docker image was pushed to Docker Hub. The same image was then pulled into an independent Ubuntu VM and deployed without rebuilding the application on the VM.

This demonstrates the portability and consistency of Docker containers across different environments.