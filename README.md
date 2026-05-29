# terraform-azure-aks-platform

Production-grade Kubernetes platform on Azure, fully provisioned with Terraform and automated via GitHub Actions CI/CD.

![HCL](https://img.shields.io/badge/Terraform-HCL-7B42BC?style=flat&logo=terraform)
![Azure](https://img.shields.io/badge/Azure-AKS-0078D4?style=flat&logo=microsoftazure)
![Kubernetes](https://img.shields.io/badge/Kubernetes-K8s-326CE5?style=flat&logo=kubernetes)
![GitHub Actions](https://img.shields.io/badge/CI/CD-GitHub_Actions-2088FF?style=flat&logo=githubactions)

## Overview

This project provisions and manages a full cloud-native infrastructure on Azure for deploying a containerized weather application. Infrastructure is entirely defined as code using Terraform, with automated validation, planning, and deployment through GitHub Actions.

## Architecture

    .github/workflows/     - GitHub Actions: Terraform plan, validate, deploy
    infra/backend/         - Azure Storage: Terraform remote state
    infra/network/         - VNet, subnets, NSGs
    infra/aks/             - AKS clusters (test + production)
    infra/redis/           - Azure Cache for Redis
    infra/weather_app/     - Application deployment manifests
    k8s/                   - Kubernetes manifests

## Infrastructure Components

| Component | Details |
|---|---|
| AKS | Kubernetes clusters for test and production environments |
| Azure Redis Cache | Managed Redis for application caching |
| Azure Container Registry | Private container image registry |
| Virtual Network | Isolated VNet with dedicated subnets |
| Terraform Remote State | Azure Storage backend for state management |
| Monitoring | Prometheus and Grafana for metrics and dashboards |

## CI/CD Pipeline

GitHub Actions workflows enforce quality gates on every pull request:

- Terraform Format Check: enforces consistent HCL formatting
- Terraform Validate: validates configuration syntax
- TFLint Analysis: lints for Azure provider best practices
- Infrastructure Plan Review: generates plan as PR comment

Branch protection rules require all checks to pass before merge.

## Prerequisites

- Azure subscription with Contributor access
- Azure CLI
- Terraform >= 1.1.0
- kubectl
- Node.js 16+

## Getting Started

    git clone https://github.com/D1207-D/terraform-azure-aks-platform.git
    cd terraform-azure-aks-platform/infra
    terraform init
    terraform plan
    terraform apply

Retrieve AKS credentials:

    az aks get-credentials --resource-group <resource-group> --name <cluster-name>
    kubectl apply -f ../k8s/

## Environment Variables

    AZURE_CLIENT_ID=
    AZURE_TENANT_ID=
    AZURE_SUBSCRIPTION_ID=
    REGISTRY_NAME=
    RESOURCE_GROUP=
    AKS_CLUSTER_NAME=
    GRAFANA_ADMIN_PASSWORD=
    OPENWEATHER_KEY=

## Contributors

- [@D1207-D](https://github.com/D1207-D)
- [@rhythmsh05](https://github.com/rhythmsh05)
- [@seerat-sawhney](https://github.com/seerat-sawhney)
- [@yogeshBhatt897](https://github.com/yogeshBhatt897)
