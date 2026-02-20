# homelab-k8s-gitops

Production-style Kubernetes homelab running on a single-node cluster using GitOps principles.

This repository represents the **desired state of the cluster**, managed via Argo CD using the Root Application (App of Apps) pattern.

---

## Architecture Overview

Cluster components:

- Kubernetes (single node)
- Argo CD (GitOps controller)
- Cilium (CNI)
- MetalLB (bare-metal LoadBalancer)
- kube-prometheus-stack (monitoring)
- Loki (logging)
- Velero (backup)

All workloads are deployed declaratively via Argo CD.

---

## GitOps Workflow

This repository follows a GitOps workflow:

1. Changes are made via Pull Request
2. GitHub Actions CI validates:
   - YAML syntax
   - Kubernetes schema (kubeconform)
   - Helm chart validation
3. After merge to `main`
4. Argo CD automatically syncs the cluster state

The cluster continuously reconciles against this repository.

---

## Repository Structure

.
├── apps/
│ ├── backup/
│ ├── cilium_infrastructure/
│ ├── loadbalancer/
│ ├── monitoring/
│ └── test-pod/
├── rootApplication.yaml
└── README.md


- `rootApplication.yaml` – Root Argo CD Application
- `apps/` – All child applications managed by Argo CD

---

## Argo CD Setup

Argo CD is deployed inside the cluster and bootstrapped using:

- Root Application pattern
- Declarative Application manifests
- Automated sync enabled

Git is the single source of truth.

---

## Observability

Monitoring stack includes:

- Prometheus
- Grafana
- Alertmanager
- Loki

All deployed and managed via GitOps.

---

## Networking

- Cilium as CNI
- MetalLB for LoadBalancer services
- Ingress resources for external access testing

---

## Backup Strategy

Velero is deployed for:

- Cluster resource backups
- Future disaster recovery simulation

---

## CI Pipeline

This repository includes a GitHub Actions CI pipeline that performs:

- YAML linting
- Kubernetes schema validation (kubeconform)
- Helm lint validation

All changes must pass validation before merge.

This ensures invalid manifests never reach the cluster.

---

## Goals of This Project

- Practice production-grade GitOps workflows
- Improve Kubernetes platform engineering skills
- Simulate real-world infrastructure patterns
- Showcase DevOps/SRE capabilities

---

## Reproducible Platform Vision

This project aims to evolve into a fully reproducible Kubernetes platform.

The objective is to design the system so that anyone can:

1. Provision infrastructure
2. Bootstrap Argo CD
3. Sync this repository
4. Obtain a production-style Kubernetes environment

All with minimal manual intervention.

The cluster should be treated as code — versioned, reproducible, and self-healing.

---

Author: Antonio Zdravac 
DevOps Engineer
LinkedIn: https://www.linkedin.com/in/antonio-%C5%BEdravac-96b030b4/
