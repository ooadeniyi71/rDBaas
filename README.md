# rDBaas
Redis Database As A Service

# Redis StatefulSet Deployment on OpenShift using Ansible

## Overview
-----------------
This repository provides an automated solution for deploying a **Redis StatefulSet** on an **OpenShift cluster** using **Ansible**.

The deployment ensures:
- High availability using StatefulSets
- Data persistence using Persistent Volume Claims (PVCs)
- Repeatable and automated deployment via Ansible

---

## Architecture
---------------------
- Redis deployed as a StatefulSet
- Each pod has a unique identity (redis-0, redis-1, etc.)
- Each pod is backed by its own Persistent Volume
- Ansible automates provisioning and deployment

<img width="804" height="1008" alt="image" src="https://github.com/user-attachments/assets/1b946cbf-f6aa-4c4d-81b8-1699f0eb7b30" />


                 
------------------------

## Prerequisites
----------------------

- OpenShift Cluster (4.x recommended)
- `oc` CLI configured and authenticated
- Ansible installed (>=2.9)
- Access to a StorageClass for dynamic provisioning
- Proper permissions to create:
  - Projects/Namespaces
  - StatefulSets
  - Persistent Volumes

---

## Repository Structure
---------------------------
<img width="776" height="758" alt="image" src="https://github.com/user-attachments/assets/fa0226e5-b2a3-4393-a6bf-7e0932b99c23" />


----------------------------
1. To depoly REDIS; Run as follow:
ansible-playbook install-redisv2.yml -e project_name=<project-name> -e redis_version=<redis:version> -e redis_name=< redis-name> -e replica_count=<no of replicas>

2. To depoly REDIS upgrade; Run as follow:
ansible-playbook install-redisv2.yml -e project_name=<project-name> -e redis_version=<redis:new-version> -e redis_name=< redis-name>


3. To ddecommision REDIS; Run as follow:
ansible-playbook decomm-redisv2.yml -e project_name=<project-name> -e redis_version=<redis:version> -e redis_name=< redis-name>
