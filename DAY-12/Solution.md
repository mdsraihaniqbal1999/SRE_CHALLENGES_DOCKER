## **Steps to Complete the Challenge**

### **1. Create a Docker Network**
Start by creating a user-defined bridge network for container communication.
```bash
docker network create yelb-network
```
<img width="598" alt="image" src="https://github.com/user-attachments/assets/689f2ab6-323d-4b8d-9b26-eae6bcccb995" />

<img width="512" alt="image" src="https://github.com/user-attachments/assets/86cbb07a-4322-44d8-b5c8-7fc0a0a18d70" />





### **2. Run Redis Server**
Deploy Redis, which acts as a caching layer to store page views.
```bash
docker run --name redis-server \
  --network=yelb-network \
  -p 6379:6379 \
  -d redis:4.0.2
```

<img width="594" alt="image" src="https://github.com/user-attachments/assets/c0eb4783-7dac-41c2-99a8-20b21cba2930" />



### **3. Run PostgreSQL Database**
Start PostgreSQL to store persistent vote data.
```bash
docker run --name yelb-db \
  --network=yelb-network \
  -p 5432:5432 \
  -d mreferre/yelb-db:0.6
```

<img width="597" alt="image" src="https://github.com/user-attachments/assets/c9a9272c-3788-47d1-b4d2-6c92dd2a9fe8" />



### **4. Run Yelb Appserver**
Launch the application server, ensuring it connects to Redis and PostgreSQL.
```bash
docker run --name yelb-appserver \
  --network=yelb-network \
  -d -p 4567:4567 \
  -e RACK_ENV=test \
  mreferre/yelb-appserver:0.7
```

<img width="596" alt="image" src="https://github.com/user-attachments/assets/649ca202-1fcc-4830-aaba-d7dacfbd4aaa" />


### **5. Run the Yelb UI**
Deploy the front-end, connecting it to the app server, and expose it for user access.
```bash
docker run --name yelb-ui \
  --network=yelb-network \
  -d -p 8080:80 \
  -e UI_ENV=test \
  mreferre/yelb-ui:0.10
```

<img width="605" alt="image" src="https://github.com/user-attachments/assets/1516b481-342d-41e0-bab0-3f3dfd031f75" />


### **6. Test Application**
Open your browser and visit `http://localhost:8080`. Interact with the Yelb UI to confirm all services are working correctly.

<img width="1149" alt="image" src="https://github.com/user-attachments/assets/7646d01c-d329-4d8f-a11c-40eb94ff1248" />

<img width="1150" alt="image" src="https://github.com/user-attachments/assets/a25a8769-2b40-4cfb-84eb-507ed4502a5b" />

### **Proof of Completion:**
- Screenshot of `docker ps` showing all running Yelb containers.
<img width="1032" alt="image" src="https://github.com/user-attachments/assets/4a3bdd1d-89d7-4f13-ad3b-0199312f77bc" />

- Screenshot of the Yelb UI in the browser. (attached above)
- Output from `docker network inspect yelb-network` showing container connectivity.
<img width="755" alt="image" src="https://github.com/user-attachments/assets/b1ca6ac1-bf54-4964-89e7-1b75a6d77b34" />




