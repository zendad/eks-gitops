# Kubernetes setup on Amazon AWS using Kops and Ansible
This repository contains tooling for deploying a HA Kubernetes cluster in Amazon AWS using the [Kops](https://github.com/kubernetes/kops) tool. The following tools will be install on the cluster by default.
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

## Prerequisites
The cluster will be deployed from a linux jumpbox/bastion host with the following:
 - ansible

Export the AWS credentials which will be used to authenticate with Amazon AWS:
```
export AWS_ACCESS_KEY_ID="XXX"
export AWS_SECRET_ACCESS_KEY="XXX"
```

 - other prerequisites will be installed with a ansible playbook on the jumpbox/bastion host.
   - kubectl 
   - aws tools
   - aws roles for instances
   - helm 
   - kops
   - S3 bucket to store where `Kops` will store its information
   
   ```
    ansible-playbook install-prerequisites.yaml
   ```
## Configurations
The main configuration of the cluster is in the variables in `group_vars/all/vars.yaml`. Each ansible role might require extra  variables not defined in  `group_vars/all/vars.yaml`. Tagging of aws resources will be created will done through a lambda function, tags are configured in also in `group_vars/all/vars.yaml`

## Installing the Kubernetes cluster
Create the Kubernetes cluster using `Kops`:
```
ansible-playbook create-cluster.yaml
```

## Updating the Kubernetes cluster
All updates to the running Kubernetes cluster can be done directly using `Kops`. 

Create the Kubernetes cluster using `Kops`:
```
ansible-playbook update-cluster.yaml
```


## Deleting the Kubernetes cluster
To delete the cluster export the AWS credentials:
```
export AWS_ACCESS_KEY_ID="XXX"
export AWS_SECRET_ACCESS_KEY="XXX"
```

And run:
```
ansible-playbook delete-cluster.yaml
```
