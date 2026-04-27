# CI/CD Pipeline with GitHub Actions & Docker

![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF?style=flat&logo=github-actions&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.10-3776AB?style=flat&logo=python&logoColor=white)
![VPS](https://img.shields.io/badge/Deploy-VPS-orange?style=flat)

A production-style CI/CD pipeline that automatically builds a Dockerized Python application and deploys it to a VPS every time code is pushed to the `main` branch — zero manual intervention required.

---

## How It Works

```
Developer pushes code
        ↓
GitHub Actions triggered
        ↓
Docker image built & tested
        ↓
Image pushed to registry
        ↓
VPS pulls & restarts container
        ↓
App is live ✓
```

Every push to `main` triggers the full pipeline. If any step fails, deployment is blocked automatically.

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| **GitHub Actions** | CI/CD automation |
| **Docker** | Containerization |
| **Python 3.10** | Application runtime |
| **VPS (DigitalOcean/AWS EC2)** | Deployment target |
| **SSH** | Secure remote deployment |

---

## Project Structure

```
ci-cd-pipeline/
├── .github/
│   └── workflows/
│       └── deploy.yml        # CI/CD pipeline definition
├── app.py                    # Python application
├── Dockerfile                # Container build instructions
├── requirements.txt          # Python dependencies
└── README.md
```

---

## Pipeline Stages

### 1. Build
- Checks out code from repository
- Builds Docker image from `Dockerfile`
- Tags image with commit SHA for traceability

### 2. Test
- Runs container to verify application starts correctly
- Checks for dependency issues

### 3. Deploy
- SSHs into VPS using GitHub Secrets
- Pulls latest Docker image
- Restarts container with zero-downtime strategy

---

## Setup & Usage

### Prerequisites
- A VPS running Ubuntu 22.04
- Docker installed on VPS
- GitHub repository secrets configured

### Required GitHub Secrets

Go to **Settings → Secrets and variables → Actions** and add:

| Secret | Description |
|--------|-------------|
| `VPS_HOST` | Your VPS IP address |
| `VPS_USER` | SSH username (e.g. `ubuntu`) |
| `VPS_SSH_KEY` | Private SSH key for VPS access |
| `DOCKER_USERNAME` | Docker Hub username |
| `DOCKER_PASSWORD` | Docker Hub password or access token |

### Run Locally

```bash
# Clone the repository
git clone https://github.com/mdmusab123/ci-cd-piplene.git
cd ci-cd-piplene

# Build Docker image
docker build -t ci-cd-app .

# Run container
docker run -p 5000:5000 ci-cd-app
```

### Trigger Deployment

```bash
# Any push to main triggers the pipeline automatically
git add .
git commit -m "feat: update application"
git push origin main
```

---

## What I Learned

- Structuring GitHub Actions workflows with multiple jobs
- Building and tagging Docker images in CI
- Securely deploying to a remote VPS using SSH keys and GitHub Secrets
- Managing environment-specific configuration without hardcoding credentials
- Debugging failed pipeline runs from GitHub Actions logs

---

## Author

**Musab Ahmed**
- GitHub: [@mdmusab123](https://github.com/mdmusab123)
- Email: mdmusab207@gmail.com
- LinkedIn: [linkedin.com/in/mdmusab123](https://linkedin.com/in/mdmusab123)

---

## License

MIT License — feel free to use this as a template for your own CI/CD pipelines.
