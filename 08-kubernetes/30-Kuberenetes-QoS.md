## Kubernetes QoS Classes

Kubernetes uses Quality of Service (QoS) classes to manage and prioritize Pods based on their resource requirements. These classes help Kubernetes make decisions about which Pods to evict when Node resources are exceeded. There are three QoS classes in Kubernetes: Guaranteed, Burstable, and BestEffort.

### 1. Guaranteed QoS Class

Pods in the Guaranteed QoS class have the highest priority and are the least likely to be evicted. To achieve this class, every Container in the Pod must have both memory and CPU limits and requests, and these limits must be equal to the requests. This ensures that the Pod has strict resource guarantees.

Example
```yaml
apiVersion: v1
kind: Pod
metadata:
 name: qos-demo
 namespace: qos-example
spec:
 containers:
 - name: qos-demo-ctr
   image: nginx
   resources:
     limits:
       memory: "200Mi"
       cpu: "700m"
     requests:
       memory: "200Mi"
       cpu: "700m"
```
To create this Pod:
kubectl apply -f https://k8s.io/examples/pods/qos/qos-pod.yaml --namespace=qos-example

### 2. Burstable QoS Class

Pods in the Burstable QoS class have some resource guarantees but are more flexible. They are evicted only after all BestEffort Pods are evicted. A Pod is classified as Burstable if it does not meet the criteria for Guaranteed but has at least one Container with a memory or CPU request or limit.

Example
```yaml
apiVersion: v1
kind: Pod
metadata:
 name: qos-demo-2
 namespace: qos-example
spec:
 containers:
 - name: qos-demo-2-ctr
   image: nginx
   resources:
     limits:
       memory: "200Mi"
     requests:
       memory: "100Mi"
```
To create this Pod:
kubectl apply -f https://k8s.io/examples/pods/qos/qos-pod-2.yaml --namespace=qos-example

### 3. BestEffort QoS Class

Pods in the BestEffort QoS class have the lowest priority and are the first to be evicted when Node resources are constrained. A Pod is classified as BestEffort if none of its Containers have memory or CPU limits or requests.

Example
```yaml
apiVersion: v1
kind: Pod
metadata:
 name: qos-demo-2
 namespace: qos-example
spec:
 containers:
 - name: qos-demo-2-ctr
   image: nginx
   resources:
     limits:
       memory: "200Mi"
     requests:
       memory: "100Mi"
```       
To create this Pod:
kubectl apply -f https://k8s.io/examples/pods/qos/qos-pod-3.yaml --namespace=qos-example