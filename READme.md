### 📦 Full Stack DevOps Project
---

This repository contains a multi-service full-stack application composed of three independent services:

* Client – Frontend application
* Node API – Backend service (Node.js)
* Java API – Backend service (Java)

Each service is containerized using Docker and deployed via CI/CD pipelines.

### 🏗️ Project Structure
---

```
app/
├── client/            # Frontend application (Dockerized)
├── nodeapi/           # Node.js backend service (Dockerized)
├── javaapi/           # Java backend service (Dockerized)
├── docker-compose.yaml # Multi-container orchestration
├── .env               # Environment variables
├── .dockerignore
└── .github/
    └── workflows/    # CI/CD pipelines for each service
```

### ⚙️ Architecture Overview
---

The system follows a microservices-based architecture:

* Each service is independently built and deployed
Services are packaged as Docker images.

* Images are pushed to a container registry.

* A central Docker Compose file orchestrates all services


### 🚀 CI/CD Pipelines
---

Each service has its own pipeline defined in .github/workflows.

🔁 Pipeline Workflow

For each of the following services: `client`, `nodeapi`, `javaapi`

   The pipeline performs:

   * Code Checkout
   * Security Scanning
   * Build Application
   * Docker Image Build
   * Push Image to Registry

This ensures:

 * Consistent builds
 * Secure artifacts
 * Isolated deployments per service

🐳 Docker Setup

Each service contains its own:

  * Dockerfile
  * Application-specific dependencies
  * Build Example (Manual)

    * Node API

        `docker build -t nodeapi ./nodeapi`

    * Java API
    
        `docker build -t javaapi ./javaapi`

    * Client

        `docker build -t client ./client`


🧩 Running the Application
---

The entire system can be started locally using Docker Compose.

#### 🛠️ Prerequisites

Before running this application locally, ensure the following tools are installed:

* Docker (for containerization)
* Docker Compose (for multi-container orchestration)
* Git (for cloning the repository)

#### 🔐 Environment Variables

Environment variables are managed using the .env file.

Ensure this file is properly configured with correct values for `MONGO_INITDB_DATABASE`, `MYSQL_ROOT_PASSWORD`, `MYSQL_DATABASE`, before running the application.

For local development, Docker Compose will:

  * Build images from the local Dockerfiles
  * Start all services (client, nodeapi, javaapi). `docker-compose up -d --build`
  * Configure networking between services automatically


#### 🚀 Running on a Server (Production)

In a production environment, the server pulls pre-built images from a container registry.

  * Authentication to Container Registry

    Before running Docker Compose, the server must authenticate with the container registry:

    * `docker login <registry-url>`
    * Provide the required credentials (e.g., username/password, access token, or service principal).
    * Pull Latest Images: `docker-compose pull`
    * Start Services: `docker-compose up -d`