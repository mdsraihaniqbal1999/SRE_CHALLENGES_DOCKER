# 🐳 DevOps SRE Daily Challenge: Docker Volumes

Welcome to Day 2 of the DevOps SRE Challenge series! Today we're diving into Docker Volumes for persistent data management.

## 📝 Overview

Learn how to implement persistent storage in containerized applications using Docker volumes. This challenge focuses on practical implementation with the Yelb application stack.

## 🎯 Learning Objectives

- Understanding Docker volumes and their importance
- Implementing persistent storage for stateful applications
- Managing data across container lifecycles
- Practicing volume backup and restoration

## 🛠 Prerequisites

- Docker installed on your system
- Basic understanding of container concepts
- Completed Day 1's Docker Networking challenge

## 📚 Key Concepts

### Docker Volumes

Docker volumes provide:
- Data persistence across container restarts
- Secure isolation from host filesystem
- Easy data sharing between containers
- Simplified backup and migration

### Essential Commands

```bash
# List all volumes
docker volume ls

# Create a new volume
docker volume create my-volume

# Inspect volume details
docker volume inspect my-volume

# Remove a volume
docker volume rm my-volume

# Clean up unused volumes
docker volume prune
```

## 💻 Challenge Steps

### 1. PostgreSQL Setup

```bash
# Create PostgreSQL volume
docker volume create pg-data

# Run PostgreSQL with volume
docker run --name yelb-db \
  --network=yelb-network \
  -v pg-data:/var/lib/postgresql/data \
  -p 5432:5432 \
  -d mreferre/yelb-db:0.6
```

### 2. Redis Setup

```bash
# Create Redis volume
docker volume create redis-data

# Run Redis with volume
docker run --name redis-server \
  --network=yelb-network \
  -v redis-data:/data \
  -p 6379:6379 \
  -d redis:4.0.2
```

### 3. Verify Persistence

```bash
# Stop and remove containers
docker stop redis-server yelb-db
docker rm redis-server yelb-db

# Restart containers
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

## ✅ Submission Requirements

### Required Screenshots
1. Running containers (`docker ps` output)
2. Volume inspection results (`docker volume inspect` output)
3. Data persistence verification after container restart

### Documentation
- Detailed steps of volume implementation
- Learnings and insights
- Challenges faced and solutions

## 🌟 Bonus Challenges

1. **Bind Mounts vs Volumes**
   - Compare both approaches
   - Document use cases for each

2. **Docker Compose Integration**
   - Create a docker-compose.yml with volume configurations
   - Implement service definitions with proper volume mounts

3. **Volume Backup & Restore**
   - Implement volume backup using `docker cp`
   - Demonstrate restoration process

## 🤝 Share Your Progress

Share your learning journey on social media using:
- #getfitwithsagar
- #SRELife
- #DevOpsForAll

## ❓Why This Matters

Understanding Docker volumes is crucial for:
- Managing stateful applications in production
- Ensuring data persistence and reliability
- Implementing proper backup strategies
- Scaling containerized applications

## 📞 Support

Questions or stuck? Reach out to Sagar Utekar through the community channels.

---

Happy Learning! 🚀
