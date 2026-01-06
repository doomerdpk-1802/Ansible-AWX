# AWX on Kind – Minimal Single-File Installation Guide

This document installs **AWX (Ansible Web UI)** on a **local Kind (Kubernetes in Docker)** cluster using the **AWX Operator**.

---

## Architecture

```text
Local Machine
 └── Kind Kubernetes Cluster
      ├── AWX Operator
      ├── AWX Web Pod
      ├── AWX Task Pod
      └── Internal PostgreSQL
```

---

## Prerequisites

Required tools:

- Docker
- kind
- kubectl

Verify:

```bash
docker --version
kind version
 version --client
```

```bash
kind create cluster --config awx_cluster.yml -n awx
k get nodes
k apply -k github.com/ansible/awx-operator/config/default?ref=2.19.1
k get pods -n awx -w
k apply -f awx.yml
k get pods -n awx
```

credentials:

```text
username: admin
password:k get secret awx-admin-password -n awx -o jsonpath="{.data.password}" | base64 -d
http://localhost:30080
```
