# Pokedex DevOps Platform

A self-hosted GitOps platform running on k3s, demonstrating modern DevOps practices and continuous deployment workflows.

## Motivation

This project is about learning the workflow of a DevOps engineer and Go developer. It runs GitOps with Flux to push changes and applications onto my own k3s cluster at home. I built this project for my own growth, learning, and curiosity as a developer.

The goal is to implement production-grade DevOps practices in a home lab environment, gaining hands-on experience with container orchestration, GitOps workflows, and automated CI/CD pipelines.

## Quick Start

### Prerequisites

- Docker installed
- kubectl configured
- k3s cluster running
- Flux CLI installed
- GitHub account with access to this repository

### Installation

1. Clone the repository:
```bash
git clone https://github.com/Yengso/pokedex-devops.git
cd pokedex-devops
```

2. Bootstrap Flux on your k3s cluster:
```bash
flux bootstrap github \
  --owner=<you-github-name> \
  --repository=pokedex-devops \
  --branch=main \
  --path=clusters
```

3. Verify Flux installation:
```bash
flux check
kubectl get pods -n flux-system
```

4. Deploy the Pokedex application:
```bash
kubectl apply -f k8s/
```

## Usage

### Running the Pokedex CLI

```bash
# Build the CLI locally
cd pokedex-cli
go build -o pokedex

# Run the CLI
./pokedex [command]
```

### Making Changes

All changes are deployed automatically via GitOps:

1. Make your changes to the code or manifests
2. Commit and push to the main branch
3. GitHub Actions will build and tag a new Docker image
4. Flux will detect the changes and deploy to your k3s cluster

### Monitoring Deployments

```bash
# Watch Flux reconciliation
flux get kustomizations --watch

# Check application status
kubectl get pods -n default

# View logs
kubectl logs -f deployment/pokedex-app
```

## Features

### What I've Built

- **CI/CD Pipeline**: Automated testing, building, and deployment with GitHub Actions
- **GitOps with Flux**: Continuous deployment where Git is the single source of truth
- **Kubernetes Deployment**: Self-hosted k3s cluster for container orchestration
- **Docker Containerization**: Immutable image tagging using Git SHAs for full traceability
- **Automated Deployments**: Push-based workflow with automatic cluster synchronization

### Tech Stack

- **Go**: Backend application development
- **Docker**: Container runtime and image building
- **Kubernetes (k3s)**: Lightweight Kubernetes distribution for production workloads
- **Flux**: GitOps operator for continuous delivery
- **GitHub Actions**: CI/CD automation and workflow orchestration

### Architecture/Pipeline Flow

```
Code Push → GitHub Actions (CI) → Docker Build → Image Push → Flux Detects Change → k3s Cluster Update
```

1. Developer pushes code to GitHub
2. GitHub Actions triggers automated tests and builds
3. Docker image is built and tagged with Git SHA
4. Image is pushed to container registry
5. Flux detects manifest changes in Git
6. Flux applies changes to k3s cluster
7. Application is deployed/updated automatically

### Project Structure

```
pokedex-devops/
├── clusters/           # Flux-system files to connect Flux with the k3s cluster
├── docker/             # Dockerfiles for applications
├── k8s/                # Kubernetes manifests/YAML files for cluster applications
└── pokedex-cli/        # All relevant Golang code and files for the Pokedex CLI application
```

### What I've Learned

**Flux CD & GitOps**
- Implemented continuous deployment where Git is the single source of truth
- Flux automatically syncs my Kubernetes cluster with my Git repository
- Declarative infrastructure management with automatic reconciliation

**GitHub Actions Workflows**
- Built a multi-stage CI/CD pipeline with separate workflows for testing, building, and deployment
- Learned to chain workflows and prevent infinite loops with bot commits
- Implemented proper workflow triggers and conditional execution

**Containerization**
- Dockerized my Go application with best practices
- Implemented immutable image tagging using Git SHAs for full traceability of deployments
- Optimized Docker images for size and security

**Infrastructure as Code**
- All infrastructure is version-controlled with YAML manifests
- Changes go through code review and are automatically applied
- Configuration drift is automatically corrected by Flux

**Production Concepts**
- Implemented patterns used in real production environments
- Immutable deployments with rollback capabilities
- Automated pipelines with proper CI/CD stage separation
- Observability and monitoring of deployment status

## Contributing

This is currently a solo project for my own experience to grow, so I'm currently not taking contributions.

### Development Workflow

- All commits should have clear, descriptive messages
- Test your changes locally before pushing
- Update documentation for any new features or changes
- Ensure GitHub Actions workflows pass before merging

---

**Note**: This project is designed for learning and experimentation. It runs on a home k3s cluster and may not reflect all production security considerations for public-facing deployments.
