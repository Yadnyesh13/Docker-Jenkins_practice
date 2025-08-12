# Docker-Jenkins_practice
Here’s a clean and well-structured **`README.md`** for your GitHub repository based on the steps you provided:

---

````markdown
# Docker + Jenkins + Nginx on AWS EC2

This guide walks through setting up **Docker**, running **Jenkins** and **Nginx** containers on an **Amazon Linux EC2 instance**, and basic Docker container/image management.

---

## 1. Sign up for Docker Hub
1. Visit [https://hub.docker.com/](https://hub.docker.com/).
2. Create a username in the format: **firstlast**.

---

## 2. Launch AWS EC2 Instance
- **Instance Type:** `t2.micro`
- **AMI:** Amazon Linux
- **Key Pair:** `docker.pem`
- **Security Group Ports:**
  - SSH: `22`
  - HTTP: `80`
  - HTTPS: `443`
  - Jenkins: `8080`

---

## 3. Connect to EC2 via SSH
```bash
ssh -i docker.pem ec2-user@<instance-ip>
````

---

## 4. Install and Configure Docker

```bash
sudo yum update -y
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
docker --version
```

---

## 5. Log in to Docker Hub

```bash
sudo docker login
```

---

## 6. Pull and Run Nginx

```bash
sudo docker images
sudo docker pull nginx
sudo docker images
```

---

## 7. Pull and Run Jenkins (Java 21)

```bash
sudo docker pull jenkins/jenkins:jdk21
sudo docker run -d -p 8080:8080 jenkins/jenkins:jdk21
```

* Open Jenkins in your browser:
  `http://<instance-ip>:8080`

---

## 8. Get Jenkins Initial Admin Password

1. List running containers:

   ```bash
   sudo docker container ls
   ```

   Example container ID: `da6e91230c61`

2. View password:

   ```bash
   sudo docker exec -it da6e91230c61 cat /var/jenkins_home/secrets/initialAdminPassword
   ```

---

## 9. Run Nginx Container

```bash
sudo docker run -d -p 80:80 nginx
```

* Open Nginx in your browser:
  `http://<instance-ip>:80`

---

## 10. Managing Containers & Images

### View images:

```bash
sudo docker images
```

### Remove an image:

```bash
sudo docker rmi <image-id>
```

### Stop and remove containers:

```bash
sudo docker container stop <container-id>
sudo docker container rm <container-id>
```

### Remove unused images:

```bash
sudo docker rmi <image-id>
```

---

## 11. Example Cleanup Commands

```bash
sudo docker rmi 5e9791083610
sudo docker container stop db5e0601917d
sudo docker container rm db5e0601917d
sudo docker container stop da6e91230c61
sudo docker container rm da6e91230c61
sudo docker images
sudo docker container ls
sudo docker rmi 5e9791083610
sudo docker rmi 2cd1d97f893f
```

---

## Notes

* Replace `<instance-ip>` with your EC2 public IP.
* Ensure security group allows the necessary ports.
* Always clean up unused containers/images to save resources.

---

```

---

