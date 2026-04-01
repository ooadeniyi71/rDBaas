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

                    +----------------------+
                  |   Ansible Control    |
                  |  (Automation Engine) |
                  +----------+-----------+
                             |
                             v
                +--------------------------+
                |   OpenShift Cluster      |
                +--------------------------+
                             |
        -------------------------------------------------
        |                |                |              |
        v                v                v              v

   +----------+     +----------+     +----------+
   | redis-0  |     | redis-1  |     | redis-2  |
   |  Pod     |     |  Pod     |     |  Pod     |
   +----+-----+     +----+-----+     +----+-----+
        |                |                |
        v                v                v
   +----------+     +----------+     +----------+
   |   PVC    |     |   PVC    |     |   PVC    |
   | (Volume) |     | (Volume) |     | (Volume) |
   +----------+     +----------+     +----------+

              <---- Headless Service ---->
              (Stable network identities)

---

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

├── ansible/
│ ├── playbook.yml
│ ├── roles/
│ │ └── redis/
│ │ ├── tasks/
│ │ ├── templates/
│ │ └── vars/
├── manifests/
│ ├── statefulset.yaml
│ ├── service.yaml
│ └── pvc.yaml
└── README.md

----------------------------
1. To depoly REDIS; Run as follow:
ansible-playbook install-redisv2.yml -e project_name=<project-name> -e redis_version=<redis:version> -e redis_name=< redis-name> -e replica_count=<no of replicas>

2. To depoly REDIS upgrade; Run as follow:
ansible-playbook install-redisv2.yml -e project_name=<project-name> -e redis_version=<redis:new-version> -e redis_name=< redis-name>


3. To ddecommision REDIS; Run as follow:
ansible-playbook decomm-redisv2.yml -e project_name=<project-name> -e redis_version=<redis:version> -e redis_name=< redis-name>
