# Cloud-Native GitOps Deployment Pipeline

![Kubernetes](https://img.shields.io/badge/kubernetes-v1.32-blue)
![ArgoCD](https://img.shields.io/badge/gitops-argoCD-orange)
![Helm](https://img.shields.io/badge/helm-v3-0F1689)
![Python](https://img.shields.io/badge/python-3.9-yellow)
![License](https://img.shields.io/badge/license-MIT-green)

## Abstract

This repository implements a declarative Continuous Delivery (CD) pipeline for a Python-based microservice. The project demonstrates the practical application of **GitOps** principles, utilizing Kubernetes for orchestration, Helm for package management, and ArgoCD for automated state synchronization.

The primary objective is to showcase a transition from imperative infrastructure management to a fully declarative **Infrastructure as Code (IaC)** approach, where the Git repository serves as the Single Source of Truth for the cluster state.

## Architecture

The infrastructure is built upon a local Kubernetes cluster (Kind) simulating a production environment. Traffic management is handled via the Gateway API implementation (Traefik), and the application lifecycle is managed by ArgoCD.

### Workflow Diagram

```mermaid
graph LR
    User[Developer] -- Pushes Code --> Git(GitHub Repository)
    Argo[ArgoCD Controller] -- Polls/Webhooks --> Git
    Argo -- Detects Drift --> Sync{Synchronization}
    Sync -- Applies Manifests --> K8s[Kubernetes Cluster]
    K8s -- Manages --> Pod1[Replica 1]
    K8s -- Manages --> Pod2[Replica 2]
    K8s -- Manages --> Pod3[Replica 3]
    
