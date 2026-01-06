## Kubernetes Cluster Architecture Explained

### Question  
Can you explain the architecture of a Kubernetes cluster and the components involved?

### Short explanation of the question  
This tests your conceptual understanding of how Kubernetes is structured — including its control plane, worker nodes, and communication between components that enable cluster orchestration.

### Answer  
A Kubernetes cluster consists of a **Control Plane** (API Server, Scheduler, Controller Manager, etcd) and multiple **Worker Nodes** (Kubelet, Kube Proxy, Container Runtime). The control plane manages the cluster state, while the worker nodes run the actual workloads (pods).

---
![alt text](image.png)
### Detailed explanation of the answer for readers’ understanding

A Kubernetes cluster is made up of:

---

## 🧠 1. **Control Plane** — The Brain of the Cluster

The control plane manages and maintains the desired state of the cluster (e.g., which apps are running, what images they use, which nodes they run on, etc.).

### Key components:

| Component          | Purpose |
|-------------------|---------|
| **kube-apiserver** | Entry point to the cluster. All communication (kubectl, controllers) goes through this REST API. |
| **etcd**           | Distributed key-value store for storing all cluster data (configuration, state, secrets, etc.). |
| **kube-scheduler** | Assigns pods to nodes based on resource availability, taints/tolerations, affinities. |
| **controller-manager** | Runs various controllers (e.g., Node, ReplicaSet, Job) to monitor and maintain the desired state. |

---

## ⚙️ 2. **Worker Nodes** — Where Your Apps Run

Worker nodes are where actual application workloads (pods) are deployed.

### Components on worker nodes:

| Component        | Purpose |
|------------------|---------|
| **kubelet**      | Agent that runs on each node, communicates with the API server, ensures containers are running. |
| **kube-proxy**   | Manages networking rules to route traffic to the correct pod using Services. |
| **Container Runtime** | Responsible for running the containers (e.g., containerd, Docker, CRI-O). |

---

## 🔄 3. **Pods, Deployments, and Services**

- **Pod**: Smallest deployable unit. Wraps one or more containers.
- **Deployment**: Controller that manages ReplicaSets and ensures the desired number of pods are running.
- **Service**: Provides a stable IP and DNS name for a set of pods, and handles load balancing.

---

## 🔐 4. **Add-Ons (optional but critical)**

| Add-on             | Purpose |
|--------------------|---------|
| **CoreDNS**        | Resolves service and pod names to IPs within the cluster. |
| **Ingress Controller** | Manages HTTP and HTTPS access from outside the cluster. |
| **Metrics Server** | Collects metrics for autoscaling. |

---

### 🔗 Communication Flow (Simplified)

1. You run `kubectl apply -f deployment.yaml`
2. `kubectl` talks to the `kube-apiserver`
3. The API server stores config/state in `etcd`
4. The `scheduler` finds the best node to place the pod
5. The `kubelet` on that node pulls the image and starts the container
6. `kube-proxy` and `service` route traffic to the pod

---

Follow this article to have in-depth knowledge - https://devopscube.com/kubernetes-architecture-explained/

### Control plane

1. Kube-api server-The kube-api server is the central hub of the Kubernetes cluster that exposes the Kubernetes API. 
![alt text](image-1.png)

2. etcd- Kubernetes is a distributed system and it needs an efficient distributed database like etcd that supports its distributed nature. It acts as both a backend service discovery and a database. You can call it the brain of the Kubernetes cluster.
etcd stores all configurations, states, and metadata of Kubernetes objects (pods, secrets, daemonsets, deployments, configmaps, statefulsets, etc).
![alt text](image-2.png)

3. kube-scheduler- The kube-scheduler is responsible for scheduling Kubernetes pods on worker nodes.
When you deploy a pod, you specify the pod requirements such as CPU, memory, affinity, taints or tolerations, priority, persistent volumes (PV), etc. The scheduler's primary task is to identify the create request and choose the best node for a pod that satisfies the requirements.
![alt text](image-3.png)

4. Kube Controller Manager- What is a controller? Controllers are programs that run infinite control loops. Meaning it runs continuously and watches the actual and desired state of objects. If there is a difference in the actual and desired state, it ensures that the kubernetes resource/object is in the desired state.
![alt text](image-4.png)

5. Cloud Controller Manager (CCM)- When kubernetes is deployed in cloud environments, the cloud controller manager acts as a bridge between Cloud Platform APIs and the Kubernetes cluster.
![alt text](image-5.png)

### Data Plane

1. Kubelet - Kubelet is an agent component that runs on every node in the cluster. It does not run as a container instead runs as a daemon, managed by systemd. It is responsible for registering worker nodes with the API server and working with the podSpec (Pod specification - YAML or JSON) primarily from the API server. 
![alt text](image-6.png)

2. Kube proxy- Kube-proxy is a daemon that runs on every node as a daemonset. It is a proxy component that implements the Kubernetes Services concept for pods. (single DNS for a set of pods with load balancing). It primarily proxies UDP, TCP, and SCTP and does not understand HTTP.
When you expose pods using a Service (ClusterIP), Kube-proxy creates network rules to send traffic to the backend pods (endpoints) grouped under the Service object. Meaning, all the load balancing, and service discovery are handled by the Kube proxy.
![alt text](image-7.png)

3. Container Runtime- In the same way, container runtime is a software component that is required to run containers.
Container runtime runs on all the nodes in the Kubernetes cluster. It is responsible for pulling images from container registries, running containers, allocating and isolating resources for containers, and managing the entire lifecycle of a container on a host.
![alt text](image-8.png)