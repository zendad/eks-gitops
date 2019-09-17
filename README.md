# EKS GitOps
This repository contains tooling for deploying an AWS EKS cluster using eksctl through GitOp. The following tools will be install on the cluster by default.

### Components
- chartmuseam - internal app hub for kubernetes
- docker registry - internal registry to be used for apps
- elasticsearch - for logs
- fluentd - log shipping
- kibana - interface for ES
- dex/RBAC - cluster and app authentication using external AD
- grafana - graphs for apps and cluster from prometheus
- prometheus - monitoring cluster and apps in cluster
- node-problem-detector -  problem detectors running on the Kubernetes nodes
- setup kubectl-config
- kubernetes dashboard
- autoscaler for nodes

## Installing the cluster and its components
Run this command from your local check-out of your config repository
```
EKSCTL_EXPERIMENTAL=true eksctl \
        gitops apply \
        --quickstart-profile app-dev \
        --git-url git@github.com:zendad/eks-gitops \
        --git-email dereckzenda@mangwana.com \
        --cluster apps-prod
```
