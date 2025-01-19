## Prerequisites
```bash
# Verify Docker Compose installation
docker compose version
```

<img width="391" alt="image" src="https://github.com/user-attachments/assets/1a5f200b-d649-4956-9fec-46e2e8c76578" />


## Challenge Steps

### 1. Create docker-compose.yml
Create a file defining these services:
- Redis (Cache Layer)
- PostgreSQL (Data Storage)
- Appserver (Application Logic)
- UI (User Interface)

### 2. Deploy Application
```bash
# Start all services
docker compose up -d
```

<img width="871" alt="image" src="https://github.com/user-attachments/assets/060ced10-9a17-4676-bc10-ddca422e0d19" />


### 3. Verify Deployment
```bash
# Check container status
docker compose ps

# Access application
# Open browser: http://localhost:8080
```

<img width="1039" alt="image" src="https://github.com/user-attachments/assets/8a716d03-fec0-4fbd-bfe6-1edccd58cfeb" />

<img width="1151" alt="image" src="https://github.com/user-attachments/assets/c5eb7ef3-c070-4ab1-bf7a-30510078d9bb" />



### 4. Cleanup
```bash
# Stop and remove everything
docker compose down --volumes
```

<img width="1031" alt="image" src="https://github.com/user-attachments/assets/d4d54c5e-2928-4282-b8f6-c73fb2e428ea" />


## Example docker-compose.yml
```yaml
version: "2.1"
services:
  yelb-ui:
    image: mreferre/yelb-ui:0.10
    depends_on:
      - yelb-appserver
    ports:
      - 8080:80
    environment:
      - UI_ENV=test # dev | test | prod 

  yelb-appserver:
    image: mreferre/yelb-appserver:0.7
    depends_on:
      - redis-server
      - yelb-db
    ports:
      - 4567:4567
    environment:
      - RACK_ENV=test # development | test | production 

  redis-server:
    image: redis:4.0.2
    ports:
      - 6379:6379

  yelb-db:
    image: mreferre/yelb-db:0.6
    ports:
      - 5432:5432
```

## Submission Requirements

### Required Screenshots
1. `docker compose ps` output
2. Yelb UI in browser
3. docker-compose.yml file

### Documentation Needs
- Deployment simplification explanation
- Challenges and solutions encountered
- Implementation insights

## Bonus Challenges

### 1. Service Scaling
```bash
# Scale appserver to 3 instances
docker compose up --scale appserver=3 -d
```

### 2. Health Checks
Add to docker-compose.yml:
```yaml
services:
  appserver:
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:4567/health"]
      interval: 30s
      timeout: 10s
      retries: 3
```
