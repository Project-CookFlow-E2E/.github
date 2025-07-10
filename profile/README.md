# CookFlow E2E

Elevating Quality Through Automated E2E Testing & CI/CD

This repository is dedicated to the end-to-end (E2E) testing infrastructure for the CookFlow application. It stands as a robust demonstration of a modern CI/CD pipeline, integrating a Django backend, a React frontend, and Cypress for comprehensive E2E validation. My core work here has been to engineer a cross-repository trigger, ensuring that critical frontend E2E tests are automatically executed with every backend change, thus guaranteeing continuous application integrity and quality across all services.

This base project is forked from https://github.com/Final-Project-CookFlow/, a foundational part of Factoría F5's Rural Camp 2nd Edition of Full Stack Web Development with Salesforce course.

![Screenshot 2025-07-05 074002](https://github.com/user-attachments/assets/ea458773-08c5-4a92-b3c0-27c6b8c1d15b)
![image](https://github.com/user-attachments/assets/ee104338-96f9-41f7-87b5-fc5cce212f64)
![image](https://github.com/user-attachments/assets/20bfaec8-523b-4b16-80cd-358f666a032c)

## 🙋 My Role & Contributions: Ensuring Quality at Every Step
As the QA/Developer for this project, my focus has been on building and maintaining a resilient automated testing framework. This involved:
- Designing and implementing the E2E test suite using Cypress to validate core user flows and API integrations.
- Containerizing the testing environment using Docker to guarantee consistent and reproducible test runs across local development and CI.
- Orchestrating complex CI/CD workflows with GitHub Actions, specifically implementing the cross-repository dispatch mechanism to integrate backend and frontend testing.
- Troubleshooting and resolving critical environmental challenges (e.g., bus.cc errors, module import issues in Docker, VcXsrv setup for UI testing) to ensure a smooth and reliable testing pipeline.
- Establishing robust health checks within Docker Compose to ensure all services are ready before tests begin, minimizing flaky results.

This project showcases practical expertise in building automated quality gates for complex distributed systems.

## 🚀 Overview
The project is structured across two main GitHub repositories, which are brought together for E2E validation:
- CF-Backend: Houses the Django REST API.
- CF-Frontend: Contains the React single-page application (SPA) and the Cypress E2E testing suite.
- Both services are containerized with Docker and orchestrated via Docker Compose, providing a consistent environment for both local development and continuous integration.

<img src="https://github.com/user-attachments/assets/32ca4209-33e3-4256-959c-abfb3d4fabcb" width="300" alt="Description of this image">
<img src="https://github.com/user-attachments/assets/7c283e0c-bd97-4655-a23b-fff980d495ec" width="300" alt="Description of this image">

## ⚙️ Architecture
The Project-CookFlow-E2E system's testable components include:
- db: A PostgreSQL database container, the backend's data store.
- backend: A Django API container.
- frontend: A React UI application container.
- cypress: A dedicated container where all automated end-to-end tests are executed against the live frontend and backend services.

All components communicate seamlessly over a shared Docker network, mirroring a production-like environment for accurate testing.

## 🌟 Key Features for Quality Assurance
- Consistent Test Environments 🐳: All components, including the Cypress test runner, operate within Docker containers. This eliminates "works on my machine" issues and ensures that tests run identically in CI as they do locally.
- Automated Quality Gates (Cross-Repository CI/CD) 🔗:
- A GitHub Actions workflow in CF-Backend automatically builds the backend Docker image upon pushes to dev.
- Crucially, this workflow then dispatches an event to CF-Frontend, triggering a comprehensive E2E test run. This creates a critical feedback loop for backend changes impacting the frontend.
- The CF-Frontend GitHub Actions workflow, triggered by this dispatch (and standard pushes), orchestrates the entire test environment.
- Reliable Test Setup (Service Health Checks) ❤️‍🩹: Docker Compose configurations include robust health checks. This ensures that dependent services (like the database or backend API) are fully operational and ready before E2E tests even attempt to interact with them, significantly reducing test flakiness.
- Comprehensive E2E Test Suite 🧪: Cypress is integrated to perform automated, user-centric tests against the fully integrated application stack, verifying critical end-to-end user flows and API interactions.

## 🚀 Getting Started
These instructions will guide you through setting up the project locally for development and comprehensive E2E testing.

*** Prerequisites ***
```Git
Docker Desktop for Windows (includes Docker Compose)
For Cypress UI on Windows: VcXsrv Windows X Server
```

### Installation and Local Setup
#### Clone the repositories:
It's recommended to clone them into a parent directory for correct Docker Compose build contexts.

# Create a parent directory, e.g., CookFlow-Project
```Bash
mkdir CookFlow-Project
cd CookFlow-Project
```

# Clone the backend repository
```
git clone https://github.com/Project-CookFlow-E2E/CF-Backend.git
```

# Clone the frontend repository
```
git clone https://github.com/Project-CookFlow-E2E/CF-Frontend.git
```

#### Navigate to the CF-Frontend directory:
All Docker Compose operations will be run from here.

```Bash
cd CF-Frontend
```

Install Node.js dependencies for the frontend:
```Bash
npm install
```

### Running the Project Locally with Docker Compose
#### From the CF-Frontend directory, bring up the entire stack:

```Bash
docker compose up --build -d
```
docker compose up: Starts services defined in docker-compose.yml.

- --build: Rebuilds service images if changes are detected.
- -d: Runs containers in detached mode (background).

#### Monitor service health with:

```Bash
docker compose ps
docker compose logs -f
```

#### Accessing Services
Once all services are up and healthy:

- Frontend: Access at http://localhost:5173.
- Backend API: Access at http://localhost:8000 (e.g., http://localhost:8000/admin/).

## Stopping the Project
To stop and remove all containers, networks, and volumes:

```Bash
docker compose down -v
```

## 🧪 Testing
End-to-End tests are written using Cypress and executed within a dedicated Docker container.

### Running Cypress Locally (Headless Mode - Like CI) 🚀
This is how tests run in the automated CI pipeline.

#### From the CF-Frontend directory, after docker compose up -d:

For Windows (Git Bash/MINGW64):
```bash
docker compose run --rm \
  -v /$(pwd -W):/app \
  -w //app \
  -e CYPRESS_BASE_URL=http://frontend:80 \
  -e CYPRESS_API_URL=http://backend:8000/api \
  cypress \
  npm run cypress:run
```

## Local UI Testing (Windows with VcXsrv) 🖥️
For interactive debugging and test development, run Cypress UI on your Windows desktop.

### 1. Configure VcXsrv on Windows

<img src="https://github.com/user-attachments/assets/5ce3b89c-d697-4752-aa73-d936995c40e7" width="300" alt="VcXsrv XLaunch Display Settings">
<img src="https://github.com/user-attachments/assets/f251d386-0439-4478-8aed-cd7e57810ac7" width="300" alt="VcXsrv XLaunch Client Startup">
<img src="https://github.com/user-attachments/assets/bc8b9055-a6f4-4a65-b6c6-e384a3b3b56b" width="300" alt="VcXsrv XLaunch Extra Settings">
<img src="https://github.com/user-attachments/assets/9fe875f4-68c9-4a82-88ff-4f869c78d957" width="300" alt="VcXsrv Tray Icon">

Launch XLaunch: Find and run "XLaunch" from your Start Menu.

- Display Settings:
  - Select Multiple windows.
  - Display number 0. Click Next.

- Client startup: Select Start no client. Click Next.

- Extra settings:

  - Crucially, check "Disable access control". This enables Docker containers to connect.
(Optional) Check Native opengl.

  - Click Next.

- Finish configuration:
  - Click Finish.
(Optional) Save configuration.

Ensure VcXsrv is running (check the 'X' icon in your system tray).

Windows Firewall: If prompted, allow access for VcXsrv on your Private networks.

### 2. Modify CF-Frontend/docker-compose.yml for Cypress UI
Update the cypress service to point to your X server:

```YAML
# In your CF-Frontend/docker-compose.yml

services:
  # ... (other services) ...

  cypress:
    image: cypress/included:13.13.1 # Or your chosen Cypress version
    environment:
      CYPRESS_BASE_URL: http://frontend:80
      CYPRESS_API_URL: http://backend:8000/api
      DISPLAY: host.docker.internal:0.0 # <--- Add this line
    extra_hosts:
      - "host.docker.internal:host-gateway" # <--- Add this line
    volumes:
      - ./cypress:/e2e/cypress
      - ./cypress.config.js:/e2e/cypress.config.js
      - ./package.json:/e2e/package.json
      - ./package-lock.json:/e2e/package-lock.json
      - /e2e/node_modules
    working_dir: /e2e
    depends_on:
      frontend:
        condition: service_healthy
      backend:
        condition: service_healthy
    ports:
      - "8080:8080"
```

### 3. Run Cypress in UI Mode
Start VcXsrv: Verify it's running.

Bring up services: From CF-Frontend directory, ensure db, backend, and frontend are up:

```Bash
docker compose up -d db backend frontend
```

Run Cypress Open:

```Bash
docker compose run --rm --entrypoint "" cypress sh -c "cd /e2e && npm install && npx cypress open --project ./"
```

## 🔄 CI/CD Pipeline: Automated Quality Assurance Workflow
- The project leverages GitHub Actions to implement a robust CI/CD pipeline, with a strong emphasis on cross-repository communication to automate quality gates.

- CF-Backend Workflow: Initiating the Quality Check
- Location: CF-Backend/.github/workflows/backend-ci.yml
- Trigger: push to the dev branch.

Key QA Step: After building and pushing the backend Docker image, it triggers the CF-Frontend E2E workflow using a repository_dispatch event. This proactive trigger ensures that any backend change immediately undergoes E2E validation.

- CF-Frontend Workflow: The E2E Automation Hub
- Location: CF-Frontend/.github/workflows/ci.yml

Trigger:
- push events to main or dev.

repository_dispatch events with types: [backend_update] (from CF-Backend).

Key QA Steps:
- Sets up the full Docker Compose stack (db, backend, frontend, cypress).
- Performs rigorous health checks for db, backend, and frontend services to ensure a stable testing environment.
- Runs database migrations and seeds data, creating a consistent test state.
- Executes Cypress E2E tests within the dedicated cypress container. This includes npm install for self-contained test execution.
- Uploads Cypress screenshots and videos (on failure), providing crucial artifacts for test result analysis and debugging.
- Cleans up all Docker resources, ensuring a fresh state for subsequent runs.

## ✅ Common QA Challenges & Solutions
Through the development of this pipeline, I addressed several key challenges:

- Error [ERR_MODULE_NOT_FOUND]: Cannot find package 'cypress': This was resolved by ensuring npm install is executed inside the cypress Docker container before tests run, guaranteeing correct dependency resolution.

- Failed to connect to the bus / Cypress timeout: This headless browser environment issue was fixed by using Cypress-optimized Docker images (cypress/included) and removing conflicting DISPLAY environment variables, allowing the image to manage its virtual display internally.

- repository_dispatch not triggering: This was resolved by ensuring the CF-Frontend workflow file (ci.yml) with the repository_dispatch listener was correctly placed on the default branch (main) of the CF-Frontend repository.

## 🤝 Contributing
Contributions are welcome! Please follow standard Git Flow practices.

## 📄 License
This project is licensed under the MIT License - see the LICENSE file for details (if applicable).

## 🔗 Connect with Me!
You can find more about my work and connect with me here:

- LinkedIn Profile: linkedin.com/in/hemaps
- GitHub Profile: github.com/void-craft
- Email: hemapriyaweb@gmail.com
