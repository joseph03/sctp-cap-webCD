# my-app2 Kubernetes Deployment

This repository contains the Kubernetes manifests and ArgoCD configuration required to deploy my-app2, a web application consisting of a frontend and a backend fraud detection service, into a Kubernetes cluster. Deployment is managed via ArgoCD for GitOps-based continuous delivery.

---

# 🚀 Architecture

## Frontend

Static web app served by frontend-service on port 80

Backed by a deployment using image:
dkjt/frontend-static-7766:v1.0.10

## Backend

Fraud detection microservice (fraud-detection)

Exposed internally on port 4000

Deployed with 2 replicas for high availability

## Ingress

### NGINX Ingress resource routes external HTTP(S) traffic:

/api/detect → backend (fraud-detection)

/ (all other paths) → frontend

### Host:
ce-grp-3a-my-app2.sctp-sandbox.com

## Namespace

All resources are deployed in ns-app

## Monitoring

Backend annotated for Prometheus scraping (/health endpoint)

## 📁 Key Files
File	Purpose
ingress.yaml	Configures external access and path-based routing
service.yaml	Frontend service definition
backend-service.yaml	Backend service definition
deployment.yaml	Frontend deployment specification
backend-deploy.yaml	Backend deployment specification
app2.yaml	ArgoCD Application manifest

---

# 🔄 Deployment Workflow
GitOps with ArgoCD
All manifests are stored in this repo. Changes are auto-synced to the cluster by ArgoCD.

Ingress Routing
NGINX Ingress exposes the app at
ce-grp-3a-my-app2.sctp-sandbox.com
with custom backend timeouts.

Service Discovery
Internal services use Kubernetes label selectors for connection between frontend and backend.

# 🛠️ How to Use
Clone this repository and adjust configs as needed.

Ensure ArgoCD is installed and configured in your cluster.

Apply the app2.yaml manifest to ArgoCD to begin automated deployment.

Access the application via the configured Ingress host.

# 📝 Notes
Backend uses rolling updates for zero downtime.

Resource requests/limits are set for efficient usage.

Health and readiness probes are configured for robust monitoring and traffic management.