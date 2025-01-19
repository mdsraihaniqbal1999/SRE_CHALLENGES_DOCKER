## 💻 Challenge Steps

### 1. PostgreSQL Setup

```bash
# Create PostgreSQL volume
docker volume create pg-data

<img width="423" alt="image" src="https://github.com/user-attachments/assets/b137b899-0f6c-450c-a549-2c17574e35a0" />


# Run PostgreSQL with volume
docker run --name yelb-db \
  --network=yelb-network \
  -v pg-data:/var/lib/postgresql/data \
  -p 5432:5432 \
  -d mreferre/yelb-db:0.6
```

<img width="485" alt="image" src="https://github.com/user-attachments/assets/e482fb45-7110-45c3-9cab-7d01954f2bc1" />


### 2. Redis Setup

```bash
# Create Redis volume
docker volume create redis-data

<img width="449" alt="image" src="https://github.com/user-attachments/assets/ec62a6e0-7604-41b6-8ce6-c18a6b9199e5" />


# Run Redis with volume
docker run --name redis-server \
  --network=yelb-network \
  -v redis-data:/data \
  -p 6379:6379 \
  -d redis:4.0.2
```
<img width="456" alt="image" src="https://github.com/user-attachments/assets/ca51c1f5-309e-411a-ab2f-61e3b458166f" />

<img width="563" alt="image" src="https://github.com/user-attachments/assets/89c9fa5d-bce7-405b-a10d-9ab93a1f2b11" />

<img width="604" alt="image" src="https://github.com/user-attachments/assets/439f7819-afbd-42f9-b59e-4d4cd11a09e0" />


### 3. Verify Persistence

```bash
# Stop and remove containers
docker stop redis-server yelb-db
docker rm redis-server yelb-db
```

<img width="598" alt="image" src="https://github.com/user-attachments/assets/1811b0a2-a8c3-499e-b28b-8bf520880b3a" />



<img width="505" alt="image" src="https://github.com/user-attachments/assets/26976709-00b2-4c59-8853-16701cd6d123" />



<img width="463" alt="image" src="https://github.com/user-attachments/assets/53cd7952-dd82-4760-a19b-81ca4d51bc58" />



<img width="441" alt="image" src="https://github.com/user-attachments/assets/b39e26f2-c94a-4bf1-8294-ebb55fcfd7be" />








# Restart containers

```bash
docker run --name yelb-db \
  --network=yelb-network \
  -v pg-data:/var/lib/postgresql/data \
  -p 5432:5432 \
  -d mreferre/yelb-db:0.6

docker run --name redis-server \
  --network=yelb-network \
  -v redis-data:/data \
  -p 6379:6379 \
  -d redis:4.0.2
```
<img width="462" alt="image" src="https://github.com/user-attachments/assets/208c1c8b-7aaa-453a-86af-7c7f893eec96" />



<img width="482" alt="image" src="https://github.com/user-attachments/assets/90360cf7-bd86-4c23-adbd-6de29aa8c63c" />


## ✅ Submission Requirements

### Required Screenshots
1. Running containers (`docker ps` output)
2. Volume inspection results (`docker volume inspect` output)
3. Data persistence verification after container restart

### Documentation
- Detailed steps of volume implementation
- Learnings and insights
- Challenges faced and solutions
