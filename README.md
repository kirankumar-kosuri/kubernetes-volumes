# Kubernetes Volumes

This repository provides practical examples and explanations of **Kubernetes Volumes**, which are used to manage data persistence in containerized applications.

---

## What are Kubernetes Volumes?

In Kubernetes, containers are **ephemeral**, meaning data inside a container is lost when it restarts. Volumes solve this problem by providing **persistent storage** that exists beyond the lifecycle of containers. :contentReference[oaicite:0]{index=0}

A volume is mounted into a Pod and can be shared between multiple containers.

---

## Types of Kubernetes Storage

### 1. Ephemeral Volumes
- Exist only for the lifetime of a Pod
- Data is deleted when the Pod is removed

**Example:**
- `emptyDir`
- `configMap`
- `secret`

---

### 2. Persistent Volumes (PV)

A **Persistent Volume (PV)** is a piece of storage in the cluster provisioned by an administrator or dynamically. :contentReference[oaicite:1]{index=1}

- Independent of Pod lifecycle
- Can be reused across Pods
- Backed by storage like AWS EBS, NFS, etc.

---

### 3. Persistent Volume Claim (PVC)

A **Persistent Volume Claim (PVC)** is a request for storage by a user or application. :contentReference[oaicite:2]{index=2}

- Requests storage size (e.g., 5Gi, 10Gi)
- Defines access modes (RWO, RWX, ROX)
- Automatically binds to a suitable PV

---

## How PV and PVC Work Together

1. Admin creates PV (or uses dynamic provisioning)
2. User creates PVC requesting storage
3. Kubernetes binds PVC to matching PV
4. Pod uses PVC to mount storage

This ensures data persists even if Pods restart. :contentReference[oaicite:3]{index=3}

---

## Repository Contents

- YAML files for volume examples
- Pod configurations using volumes
- PV and PVC configurations
- Real-time storage usage examples

---

## Example: Pod with Volume

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: volume-demo
spec:
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - mountPath: /data
      name: my-volume
  volumes:
  - name: my-volume
    emptyDir: {}
