# Jenkins_starter
  Overview

This repository provisions a persistent Jenkins controller running inside a Kubernetes cluster. It provides a stable CI/CD platform environment with persistent storage for plugins, jobs, and credentials, preconfigured Kubernetes ServiceAccount and RBAC for dynamic agent support, and service exposure via service or ingress. This repository does not contain application code, Terraform, or pipeline logic. Pipelines can be defined and executed from external repositories.

Repository Structure

.
├── Jenkinsfile # Placeholder for future pipelines (optional)
├── README.md
│
├── k8s/ # Kubernetes manifests for Jenkins
│ ├── jenkins-ca-configmap.yaml
│ ├── jenkins-pvc.yaml
│ ├── jenkins-sa.yaml
│ ├── jenkins-deployment.yaml
│ ├── jenkins-rbac.yaml
│ └── jenkins-service.yaml

Features
Persistent Jenkins Home

All Jenkins configuration persists in the PVC: installed plugins, job configurations, credentials, pipeline history, and workspace directories. Storage is mounted at /var/jenkins_home.

Kubernetes Integration

ServiceAccount with required permissions, ClusterRole and ClusterRoleBinding for dynamic agent provisioning, and support for pod-based builds.

Service Exposure

jenkins-service.yaml exposes Jenkins to the cluster (NodePort or ClusterIP). Optional CA ConfigMap can provide custom certificates. Optional ingress can be configured for external access.

Deployment Steps
kubectl apply -f k8s/jenkins-pvc.yaml

Apply service account and RBAC: kubectl apply -f k8s/jenkins-sa.yaml and kubectl apply -f k8s/jenkins-rbac.yaml

Apply persistent volume claim: kubectl apply -f k8s/jenkins-pvc.yaml

Deploy Jenkins: kubectl apply -f k8s/jenkins-deployment.yaml

Expose Jenkins service: kubectl apply -f k8s/jenkins-service.yaml

Optional: apply CA ConfigMap: kubectl apply -f k8s/jenkins-ca-configmap.yaml

Accessing Jenkins

NodePort (default in service manifest): http://<node-ip>:<node-port>
If using ingress: http://<hostname>

Notes

The Jenkins controller is stateful, ensuring all plugins, credentials, and job configurations persist after restarts.  
External repositories can define pipelines that run on this Jenkins instance without needing to provision Jenkins themselves.