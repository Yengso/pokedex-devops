## 1. Pokedex DevOps Platform – Self-Hosted GitOps on k3s

This project is about learning the workflow of a DevOps engineer and Go developer.
It runs GitOps with Flux, to push changes and applications on to my own k3s cluster at home.
I built this project for my own growth, learning and curiosity as a developer. 

## Features/What I've Built

CI/CD pipeline with GitHub Actions
GitOps with Flux
Kubernetes deployment on k3s
Docker containerization
Automated deployments

## Tech Stack

- Go
- Docker
- Kubernetes (k3s)
- Flux
- GitHub Actions

## Architecture/Pipeline Flow

Push → CI → Build → Deploy → Flux → k3s

## Project Structure

**Clusters:** Flux-system files to connect flux with the k3s cluster.
**Docker:** Dockerfiles for applications.
**K8s:** Holds manifests/yaml files used for applications in the cluster
**Pokedex-cli:** All relevant Golang code and files for the pokedex CLI application.

## What I've learned so far

**Flux CD & GitOps:** Implemented continuous deployment where Git is the 
single source of truth. Flux automatically syncs my Kubernetes cluster 
with my Git repository.

**GitHub Actions Workflows:** Built a multi-stage CI/CD pipeline with 
separate workflows for testing, building, and deployment. Learned to 
chain workflows and prevent infinite loops with bot commits.

**Containerization:** Dockerized my Go application with immutable image 
tagging using Git SHAs for full traceability of deployments.

**Infrastructure as Code:** All infrastructure is version-controlled YAML 
manifests. Changes go through code review and are automatically applied.

**Production Concepts:** Implemented patterns used in real production 
environments - immutable deployments, automated pipelines, and proper 
separation of CI/CD stages.
