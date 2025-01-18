# 🚀 DevOps SRE Daily Challenge: Docker Fundamentals

Welcome, Learners! 🎉  
This week, we're diving deep into **Docker**, the cornerstone of modern containerization. By completing this challenge, you'll establish a solid foundation in Docker and learn how to install it, explore its essential commands, and build your first custom containerized application.

---

## **What is Docker?**
Docker is an open platform designed to help developers and DevOps teams build, ship, and run applications in isolated environments called **containers**. It simplifies software development, deployment, and scalability by packaging applications with all the dependencies needed to run consistently across various environments.

### **Why Do We Need Docker?**
- **Consistency**: Solves the "works on my machine" issue by providing consistent environments.
- **Portability**: Run containers anywhere—laptops, servers, the cloud, or Kubernetes.
- **Efficiency**: Lightweight compared to virtual machines, as containers share the host OS kernel.
- **Scalability**: Easily scale apps to meet demand.

### **Core Docker Concepts**
1. **Docker Images**: Lightweight, standalone software packages containing everything required to run a piece of software.
2. **Docker Containers**: Instances of images that run as isolated processes.
3. **Dockerfile**: A text file with instructions to create a custom Docker image.

_For more details, refer to the [Docker Overview](https://docs.docker.com/get-started/overview/) (Official Docs)._

---

## **Requirements**
### Install Docker
1. Install Docker on your system (refer to [Docker Install Guide](https://docs.docker.com/get-docker/)).
2. Verify installation:
   ```bash
   docker --version
   ```

### Pull and Run a Container
1. Pull the official NGINX image:
   ```bash
   docker pull nginx
   ```
2. Run the container in detached mode with port mapping:
   ```bash
   docker run -d --name my-nginx -p 8080:80 nginx
   ```

### Inspect and Explore
- List running containers:
  ```bash
  docker ps
  ```
- View container logs:
  ```bash
  docker logs my-nginx
  ```
- Inspect container metadata:
  ```bash
  docker inspect my-nginx
  ```

---

## **Challenge: Build a Custom Docker Image**
1. Save the provided `index.html` file in your project directory.
2. Create a `Dockerfile` with the following:
   ```dockerfile
   FROM nginx:latest
   COPY index.html /usr/share/nginx/html/index.html
   EXPOSE 80
   ```
3. Build and tag the image:
   ```bash
   docker build -t my-nginx:custom .
   ```
4. Run the custom container:
   ```bash
   docker run -d --name my-custom-nginx -p 8081:80 my-nginx:custom
   ```

---

## **Access and Test**
- Default NGINX: [http://localhost:8080](http://localhost:8080)
- Custom NGINX: [http://localhost:8081](http://localhost:8081)

---

## **Troubleshooting Challenges**
1. Try running another container on the same port `8080`. Fix the issue and document your solution.
2. Stop a container and observe what happens when you access its endpoint in the browser.
3. Debug using:
   ```bash
   docker logs <container-name>
   ```
4. Introduce an error in the `Dockerfile` and use logs to troubleshoot.

---

## **Cleanup**
1. Stop and remove containers:
   ```bash
   docker stop my-nginx my-custom-nginx
   docker rm my-nginx my-custom-nginx
   ```
2. Remove custom image:
   ```bash
   docker rmi my-nginx:custom
   ```

---

## **Why This Matters**
This hands-on challenge will help you:
- Understand Docker fundamentals.
- Practice key concepts like building images, running containers, and troubleshooting issues.
- Prepare for real-world use cases in modern DevOps workflows.

---

## **Submission Guidelines**
### Proof of Completion
1. Screenshots:
   - Running containers (`docker ps`).
   - Custom webpage served via `my-custom-nginx`.
   - Output from `docker logs my-nginx`.

### Documentation
- Steps to build and run the custom image.
- Challenges you faced and how you resolved them.
- Key takeaways and learnings.

---

## **Bonus Tasks**
- Push your custom Docker image to Docker Hub or a private registry.
- Use Docker's API to list running containers via a script.

---

## **Share Your Progress**
Share your experience on social media using the hashtags:
- `#getfitwithsagar`
- `#SRELife`
- `#DevOpsForAll`

---

Happy Learning! 💻🛥️  
**Best regards,**  
Sagar Utekar
