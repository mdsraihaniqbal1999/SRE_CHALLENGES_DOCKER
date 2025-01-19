# Docker Networking Challenge: Deploy Yelb Application

Hello Learners,

Welcome back to the DevOps SRE Daily Challenge! 🎉

Today’s challenge focuses on **Docker Networking**, a fundamental concept for deploying and managing multi-container applications. To make this practical, we’ll deploy **Yelb**, a multi-service demo application, while highlighting Docker networking capabilities.

By the end of this challenge, you’ll have a hands-on understanding of connecting containers using Docker's networking features and managing a multi-container application effectively.

---

## **What is Docker Networking?**
Docker networking enables communication between containers, the host, and external systems. It’s crucial for connecting services in a multi-container environment, ensuring seamless communication.

### **Key Features of Docker Networking:**
- **Isolation:** Containers communicate only when allowed, ensuring security.
- **Name Resolution:** Containers on a user-defined bridge network can resolve each other by name.
- **Customizability:** Networks can be configured for specific requirements, such as isolation or external access.

---

## **Key Docker Networking Commands**
- **List Networks:**
  ```bash
  docker network ls
  ```
- **Inspect a Network:**
  ```bash
  docker network inspect yelb-network
  ```
- **Connect a Running Container to a Network:**
  ```bash
  docker network connect yelb-network <container_name>
  ```

---

## **Types of Docker Networks**
- **Bridge (Default):** For standalone containers; supports user-defined configurations.
- **Host:** Shares the host's network stack. Ideal for high-performance scenarios.
- **Overlay:** Connects containers across multiple Docker hosts.

---

## **Steps to Complete the Challenge**

### **1. Create a Docker Network**
Start by creating a user-defined bridge network for container communication.
```bash
docker network create yelb-network
```

### **2. Run Redis Server**
Deploy Redis, which acts as a caching layer to store page views.
```bash
docker run --name redis-server \
  --network=yelb-network \
  -p 6379:6379 \
  -d redis:4.0.2
```

### **3. Run PostgreSQL Database**
Start PostgreSQL to store persistent vote data.
```bash
docker run --name yelb-db \
  --network=yelb-network \
  -p 5432:5432 \
  -d mreferre/yelb-db:0.6
```

### **4. Run Yelb Appserver**
Launch the application server, ensuring it connects to Redis and PostgreSQL.
```bash
docker run --name yelb-appserver \
  --network=yelb-network \
  -d -p 4567:4567 \
  -e RACK_ENV=test \
  mreferre/yelb-appserver:0.7
```

### **5. Run the Yelb UI**
Deploy the front-end, connecting it to the app server, and expose it for user access.
```bash
docker run --name yelb-ui \
  --network=yelb-network \
  -d -p 8080:80 \
  -e UI_ENV=test \
  mreferre/yelb-ui:0.10
```

### **6. Test Application**
Open your browser and visit `http://localhost:8080`. Interact with the Yelb UI to confirm all services are working correctly.

---

## **Troubleshooting Tips**

### **Service Not Accessible:**
- Check if the containers are running:
  ```bash
  docker ps
  ```
- Inspect container logs for errors:
  ```bash
  docker logs <container_name>
  ```

### **Containers Cannot Communicate:**
- Verify the network configuration:
  ```bash
  docker network inspect yelb-network
  ```
- Reconnect a container to the network:
  ```bash
  docker network connect yelb-network <container_name>
  ```

### **Port Conflict:**
- If a port is already in use, map the container to an available port:
  ```bash
  docker run -d -p 8081:80 <image_name>
  ```

### **Environment Variable Errors:**
- Verify that required environment variables (`RACK_ENV` and `UI_ENV`) are set.
- If incorrect, stop the container, remove it, and restart with the correct variables.

---

## **Cleanup Steps**

### **Stop and Remove Containers:**
```bash
docker stop redis-server yelb-db yelb-appserver yelb-ui
docker rm redis-server yelb-db yelb-appserver yelb-ui
```

### **Remove the Docker Network:**
```bash
docker network rm yelb-network
```

### **Remove Unused Docker Images (Optional):**
```bash
docker image prune -a
```

---

## **Submission Guidelines**

### **Proof of Completion:**
- Screenshot of `docker ps` showing all running Yelb containers.
- Screenshot of the Yelb UI in the browser.
- Output from `docker network inspect yelb-network` showing container connectivity.

### **Documentation:**
- Steps to deploy Yelb manually.
- Insights into how Docker networking facilitated communication between containers.
- Key challenges faced and solutions.

### **Bonus Tasks:**
- Use Docker volumes to persist Redis and PostgreSQL data.
- Push the custom Yelb images to a container registry (ECR, GCR, or ACR).

---

## **Share Your Progress**
Post your experience on social media with the hashtags:
- `#getfitwithsagar`
- `#SRELife`
- `#DevOpsForAll`

---

## **Why This Matters**
Understanding Docker networking is crucial for deploying containerized applications efficiently. This challenge bridges the gap between theory and practice by deploying a real-world application and leveraging Docker's networking capabilities.

If you missed any previous challenges, you can catch up by reviewing the problem statements on GitHub.

---

**Best regards,**

*Sagar Utekar*
