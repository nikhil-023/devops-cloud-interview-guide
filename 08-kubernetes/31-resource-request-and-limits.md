### What Are Resource Requests and Limits?

## Requests
A request specifies the minimum resources Kubernetes guarantees for a container. The scheduler uses this value to allocate resources and ensure the container can always operate within its reserved capacity.
Example: A container with a CPU request of 500m will have 0.5 CPU cores reserved for it.

## Limits
A limit sets the maximum resources a container can consume. Kubernetes enforces this cap through throttling (CPU) or termination (memory) to prevent a container from impacting other workloads.
Example: A container with a memory limit of 1Gi will be terminated if it exceeds 1 GiB of memory. 

```yaml
resources:
  requests:
    memory: "256Mi"
    cpu: "250m"
  limits:
    memory: "512Mi"
    cpu: "500m"
```