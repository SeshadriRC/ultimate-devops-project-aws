# Kubernetes: LoadBalancer Service Type vs Ingress

<img width="1917" height="898" alt="image" src="https://github.com/user-attachments/assets/21aea574-59c2-4544-a6d6-763bf73dfe8d" />


In Kubernetes, both LoadBalancer service type and Ingress are used to expose services to external traffic. However, they serve different purposes and have distinct characteristics. This document explains the differences between the two in detail.

## LoadBalancer Service Type

### Overview
- The LoadBalancer service type is a way to expose a service to external traffic by provisioning an external load balancer.
- It is typically used to expose a single service to the internet.

### Characteristics
- **Automatic Provisioning**: When a LoadBalancer service is created, Kubernetes automatically provisions an external load balancer from the cloud provider.
- **Single Service Exposure**: Each LoadBalancer service exposes a single service.
- **Cloud Provider Dependent**: The implementation and features of the LoadBalancer depend on the cloud provider (e.g., AWS, GCP, Azure).
- **Static IP**: It usually provides a static IP address for the service.

### Use Cases
- Suitable for exposing a single service to the internet.
- Ideal for simple use cases where advanced routing is not required.

## Ingress

### Overview
- Ingress is a Kubernetes resource that manages external access to services within a cluster, typically HTTP and HTTPS.
- It provides more advanced routing capabilities compared to the LoadBalancer service type.

### Characteristics
- **Advanced Routing**: Ingress can route traffic to multiple services based on hostnames, paths, and other rules.
- **Single Entry Point**: It provides a single entry point for multiple services.
- **TLS Termination**: Ingress can handle TLS termination, providing secure HTTPS access.
- **Requires Ingress Controller**: An Ingress resource requires an Ingress controller to be deployed in the cluster (e.g., NGINX, Traefik).

### Use Cases
- Suitable for exposing multiple services through a single IP address.
- Ideal for complex routing scenarios, such as path-based or host-based routing.
- Useful for managing SSL/TLS certificates and providing secure access.

## Comparison Table

| Feature                  | LoadBalancer Service Type | Ingress                        |
|--------------------------|---------------------------|-------------------------------|
| Provisioning             | Automatic by cloud provider| Requires Ingress controller   |
| Service Exposure         | Single service            | Multiple services             |
| Routing Capabilities     | Basic                     | Advanced (host/path-based)    |
| TLS Termination          | No                        | Yes                           |
| Cloud Provider Dependency| Yes                       | No                            |
| Use Case                 | Simple, single service    | Complex, multiple services    |

## Conclusion

Both LoadBalancer service type and Ingress are essential tools in Kubernetes for exposing services to external traffic. The choice between them depends on the specific requirements of your application. Use LoadBalancer for simple, single-service exposure and Ingress for more complex scenarios requiring advanced routing and secure access.

---

# Summary

## Summary — LoadBalancer Service Type vs Ingress in Kubernetes

In the previous lecture, the frontend application was exposed using a Kubernetes Service of type `LoadBalancer`.

Flow:

```text
Kubernetes Service (LoadBalancer)
        ↓
API Server
        ↓
Cloud Controller Manager (CCM)
        ↓
AWS creates Load Balancer
        ↓
External users access application
```

This works, but it has several drawbacks.

---

# Drawbacks of LoadBalancer Service Type

## 1. Not Fully Declarative

Only the service type is defined in Kubernetes YAML.

Example:

```yaml id="1z64cb"
type: LoadBalancer
```

But advanced configurations like:

* HTTPS/TLS certificates
* Routing rules
* Health checks
* Security settings
* Load balancing algorithms

must be changed manually in the cloud console (AWS UI).

Problem:

* Changes are not tracked in YAML
* Harder to maintain
* Not fully Infrastructure-as-Code

---

## 2. Costly

If 10 microservices need external access:

* Kubernetes creates 10 separate cloud load balancers

This becomes expensive in:

* Amazon Web Services
* Microsoft Azure
* Google Cloud

---

## 3. Limited Flexibility

Using `LoadBalancer` service type usually ties you to the cloud provider’s default load balancer.

Example in AWS:

* ALB/NLB gets created automatically

But you cannot easily switch to:

* NGINX
* F5
* Traefik
* Envoy

---

## 4. Depends on Cloud Controller Manager (CCM)

`LoadBalancer` service type works only when CCM exists.

Not supported properly in:

* Minikube
* Kind
* K3s local clusters

Without CCM:

* External load balancer is not created

---

# Why Ingress is Better

Ingress is a Kubernetes resource used for advanced HTTP/HTTPS routing.

Advantages:

## 1. Declarative Configuration

Everything is written in YAML:

* TLS
* Routing
* Paths
* Hosts
* Annotations
* Load balancer behavior

Example:

```yaml id="s6vfpk"
kind: Ingress
```

---

## 2. Cost Effective

Instead of:

* 10 Load Balancers for 10 services

Ingress allows:

* 1 Load Balancer
* Multiple routes/target groups

Example:

```text
/app1 → Service1
/app2 → Service2
/api  → Service3
```

---

## 3. More Flexible

Ingress Controllers can use different technologies:

* NGINX
* F5
* Traefik
* Envoy
* HAProxy

You are not locked to cloud-provider load balancers.

---

## 4. Works Without CCM

Ingress can work even in:

* Minikube
* Kind
* Local Kubernetes clusters

No dependency on cloud-managed load balancers.

---

# Main Advantage of LoadBalancer Service Type

It is very simple.

Just:

```yaml id="v7f0uc"
type: LoadBalancer
```

No need for:

* Ingress YAML
* Ingress Controller
* Extra configuration

So it reduces operational complexity, but sacrifices flexibility and scalability.

---

# Interview Important Point

A very common interview question:

> Difference between LoadBalancer Service Type and Ingress

### LoadBalancer

* Easy to configure
* Creates separate load balancer per service
* Less flexible
* Costly
* Cloud dependent

### Ingress

* Declarative
* Advanced routing
* Cost effective
* Flexible
* Better for production environments

---

