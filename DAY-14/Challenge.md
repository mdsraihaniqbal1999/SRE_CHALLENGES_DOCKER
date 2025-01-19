# Docker Compose Challenge - DevOps SRE Daily Series 🚀

Welcome back to the **DevOps SRE Daily Challenge!** 

## Overview
Building on our journey through Docker fundamentals, Dockerfiles, networking, and volumes, today we explore **Docker Compose** for orchestrating multi-container applications.

## Learning Objectives
Learn to orchestrate the Yelb application using `docker-compose.yml`, enabling simplified deployment and management of microservices.

## What is Docker Compose?
Docker Compose is a powerful tool for defining and running multi-container applications. Using a single YAML file, you can configure all services, networks, and volumes, making deployment streamlined and consistent.

## Key Benefits
1. **Simplicity**
   - Replace complex Docker commands with YAML configuration
   - Single file for all container definitions

2. **Multi-Container Management**
   - Start/stop all services with one command
   - Simplified scaling and updates

3. **Portability**
   - Consistent deployments across environments
   - Easy sharing and version control

## Prerequisites
```bash
# Verify Docker Compose installation
docker compose version
```

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

### 3. Verify Deployment
```bash
# Check container status
docker compose ps

# Access application
# Open browser: http://localhost:8080
```

### 4. Cleanup
```bash
# Stop and remove everything
docker compose down --volumes
```

## Example docker-compose.yml
```yaml
version: '3.8'

services:
  redis:
    image: redis:4.0.2
    volumes:
      - redis-data:/data
    networks:
      - yelb-network

  postgres:
    image: mreferre/yelb-db:0.6
    volumes:
      - pg-data:/var/lib/postgresql/data
    networks:
      - yelb-network

  appserver:
    image: mreferre/yelb-appserver:0.7
    depends_on:
      - redis
      - postgres
    networks:
      - yelb-network

  ui:
    image: mreferre/yelb-ui:0.10
    ports:
      - "8080:80"
    depends_on:
      - appserver
    networks:
      - yelb-network

volumes:
  redis-data:
  pg-data:

networks:
  yelb-network:
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

### 3. GitHub Integration
- Push compose file to GitHub
- Include detailed README
- Add deployment instructions

## Why Docker Compose Matters
- Simplifies complex deployments
- Industry standard for development
- Foundation for container orchestration
- Essential for microservices architecture

## Troubleshooting Tips
1. Check logs: `docker compose logs`
2. Verify networks: `docker network ls`
3. Inspect services: `docker compose ps`
4. Validate compose file: `docker compose config`

## Social Sharing
Share your progress using:
- #getfitwithsagar
- #SRELife
- #DevOpsForAll

## Additional Resources
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Compose File Reference](https://docs.docker.com/compose/compose-file/)
- [Best Practices](https://docs.docker.com/develop/dev-best-practices/)

---

_Missed previous challenges? Catch up on GitHub!_

Best regards,  
**Sagar Utekar**
