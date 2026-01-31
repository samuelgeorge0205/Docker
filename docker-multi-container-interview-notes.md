
# Docker Multi-Container Application – Interview Notes

## Project Overview
Built a **3-tier multi-container web application** using Docker Desktop to understand **containerisation, Docker Compose, and Docker Swarm**.

### Architecture
Browser → Nginx (Frontend) → Flask API (Backend) → Redis (Database)

Each component runs in its **own container**, communicating over a **Docker-managed network**.

---

## Why Multi-Container?
- Real applications are not single containers
- Separation of concerns
- Independent scaling
- Fault isolation
- Matches microservices architecture

---

## Docker Concepts Demonstrated

### 1. Image vs Container
- **Image**: Immutable blueprint built using Dockerfile
- **Container**: Running instance of an image with a writable layer

```

Dockerfile → Image → Container → Process

````

---

### 2. Dockerfile Best Practices Used
- Lightweight base images (`python:slim`, `nginx:alpine`)
- Layer caching (COPY requirements before app code)
- Explicit CMD for runtime execution
- Minimal instructions for faster builds

---

### 3. Container Runtime
- Docker uses `containerd` and `runc`
- Runtime creates containers using:
  - Linux namespaces (isolation)
  - cgroups (resource limits)
- Containers share host kernel (not VMs)

---

### 4. Docker Networking
- Docker Compose automatically creates a **bridge network**
- Each service gets:
  - Unique container IP
  - DNS entry using **service name**

Example:
```yaml
REDIS_HOST: redis
````

* No hard-coded IPs
* Containers communicate using service names

---

### 5. Service Discovery

* Docker internal DNS resolves:

  * `backend` → backend container
  * `redis` → redis container
* Enables dynamic container replacement without config changes

---

### 6. Volumes & Data Persistence

* Redis uses a **named volume**

```yaml
volumes:
  - redis-data:/data
```

Benefits:

* Data survives container restart
* Stateless containers
* Production-ready pattern

---

### 7. Environment Variables

* Used for configuration injection
* Keeps images generic
* Same image works across environments (dev/prod)

---

### 8. Docker Compose

* Tool for defining and running **multi-container applications**
* Single YAML file defines:

  * Services
  * Networks
  * Volumes
  * Dependencies

Key commands:

```bash
docker compose up
docker compose ps
docker compose logs
docker compose down
```

---

### 9. Container Lifecycle

```
create → start → running → stop → removed
```

Important commands:

```bash
docker ps
docker exec -it <container> sh
docker logs <container>
```

---

## Docker Swarm Concepts (Same App)

### Why Swarm?

* Single host Docker is not enough
* Need orchestration:

  * Scaling
  * Self-healing
  * Desired state

---

### Swarm Setup

```bash
docker swarm init
docker stack deploy -c docker-compose.yml demo
```

---

### Swarm Objects

| Object  | Description              |
| ------- | ------------------------ |
| Node    | Docker host              |
| Service | Desired state definition |
| Task    | Running container        |
| Stack   | Group of services        |

---

### Scaling Services

```bash
docker service scale demo_backend=3
```

* Swarm automatically:

  * Creates replicas
  * Load balances traffic
  * Restarts failed containers

---

### Networking in Swarm

* Uses **overlay network**
* Containers can communicate across nodes
* Built-in load balancing via VIP

---

## Real-World Learnings

* Containers are **processes**, not machines
* Images must be immutable
* Data must live outside containers
* Networking is abstracted but critical
* Compose is for **single-host**
* Swarm adds **orchestration**

---

## Common Issues & Debugging

| Issue              | Cause                    |
| ------------------ | ------------------------ |
| Container exits    | App crash / CMD error    |
| Connection refused | Wrong service name       |
| Data loss          | Missing volumes          |
| DNS failure        | Network misconfiguration |

---

## Interview One-Liners

**What did you build?**

> A multi-container web application using Docker Compose and deployed it on Docker Swarm with service discovery, persistent storage, and scaling.

**How do containers communicate?**

> Through Docker’s internal DNS using service names on a user-defined network.

**Difference between Compose & Swarm?**

> Compose is for local multi-container apps, Swarm provides orchestration features like scaling, self-healing, and overlay networking.

**Why volumes?**

> Containers are ephemeral; volumes persist data independently of container lifecycle.

---

## Next Improvements (Future Work)

* Add healthchecks
* Add resource limits
* Secure secrets
* Convert to Kubernetes
* Add CI/CD pipeline

---

## Summary

This project provided **hands-on understanding of Docker internals**, multi-container architecture, networking, storage, and orchestration — moving beyond basic container usage into production-style workflows.

```
