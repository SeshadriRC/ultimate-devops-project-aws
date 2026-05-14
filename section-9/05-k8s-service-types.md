# Kubernetes Service Types

Kubernetes services provide a way to expose applications running on a set of Pods as a network service. Kubernetes supports several types of services, each suited to different use cases.

## 1. ClusterIP

### Description
- The default service type.
- Exposes the service on an internal IP in the cluster.
- Makes the service only reachable from within the cluster.

### Use Case
- Suitable for internal services that do not need to be exposed to the outside world.
- Commonly used for communication between microservices within the cluster.

### How It Works
- Kubernetes assigns a stable IP address to the service.
- Pods within the cluster can access the service using this IP address.

## 2. NodePort

### Description
- Exposes the service on each Node's IP at a static port.
- Makes the service accessible from outside the cluster using `<NodeIP>:<NodePort>`.

### Use Case
- Useful for exposing services for external access without a load balancer.
- Suitable for development and testing environments.

### How It Works
- Kubernetes allocates a port from a range (default: 30000-32767) on each Node.
- Traffic to this port is forwarded to the service.

## 3. LoadBalancer

### Description
- Exposes the service externally using a cloud provider's load balancer.
- Automatically creates an external IP address that forwards traffic to the service.

### Use Case
- Ideal for production environments where high availability and scalability are required.
- Suitable for services that need to be accessible from the internet.

### How It Works
- Kubernetes provisions a load balancer from the cloud provider.
- The load balancer distributes incoming traffic across the Pods.

## Conclusion

Choosing the right service type depends on the specific requirements of your application. ClusterIP is best for internal communication, NodePort for simple external access, LoadBalancer for external access.

---

# Summary

## Kubernetes Service Types Summary

In Kubernetes, services are mainly of 3 types:

### 1. ClusterIP (Default)

* Allows communication only **inside the Kubernetes cluster**
* Used for:

  * Service-to-service communication
  * Internal applications
  * Databases or sensitive services
* External users, EC2 instances, or Lambda functions cannot directly access it
* Secure because it is limited to the cluster network

Example:

```bash
frontend-service.default.svc.cluster.local
```

---

### 2. NodePort

* Exposes the service on a port of each Kubernetes node
* External systems inside the VPC/network can access it using:

```bash
<Node-IP>:<NodePort>
```

Example:

```bash
10.0.1.5:33000
```

How it works:

* Kubernetes assigns a unique port (usually 30000–32767)
* kube-proxy updates iptables internally
* Requests reaching the node port are forwarded to the service/pod

Use case:

* Access from:

  * EC2 instances
  * Internal corporate network
  * Applications inside the VPC

---

### 3. LoadBalancer

* Used for public/external internet access
* When service type is changed to `LoadBalancer`:

  * Kubernetes API Server talks to CCM (Cloud Controller Manager)
  * CCM communicates with cloud providers like:

    * Amazon Web Services
    * Microsoft Azure
  * Cloud provider creates an external load balancer automatically

Result:

```bash
External-IP --> LoadBalancer --> Kubernetes Service --> Pods
```

Use case:

* Public websites
* Frontend applications
* APIs accessible from the internet

---

## Key Points

| Service Type | Accessible From      | Main Use                 |
| ------------ | -------------------- | ------------------------ |
| ClusterIP    | Inside cluster only  | Internal communication   |
| NodePort     | VPC/Internal network | Internal external access |
| LoadBalancer | Internet/Public      | Public applications      |

---

## Important Concept

Kubernetes creates its own internal cluster network using CNI (Container Network Interface). By default, services inside this network are not reachable from outside unless exposed using:

* NodePort
* LoadBalancer
