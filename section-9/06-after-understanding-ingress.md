
# Part 1

## Summary of Ingress, Egress, and Ingress Controller in Kubernetes

* **Ingress** means incoming traffic to an application or Kubernetes cluster.
* **Egress** means outgoing traffic from the application or cluster.

---

### Problem with Service Type LoadBalancer

Previously:

* A Kubernetes Service of type `LoadBalancer` was used to expose the frontend application externally.
* The Cloud Controller Manager (CCM) created a cloud load balancer automatically.
* Users could access the application using:

  * Load balancer DNS
  * Direct IP address

Issue:

* Companies usually do **not** want applications accessible directly through IP addresses for security reasons.
* They want access only through official domain names like:

  * `amazon.com`
  * `company.com`

---

### What is Kubernetes Ingress?

Kubernetes provides a resource called **Ingress**.

Ingress is used to:

* Define routing rules for incoming traffic
* Control how external users access services
* Configure:

  * Host-based routing
  * Path-based routing
  * Domain restrictions

Example:

* Allow traffic only for:

  * `amazon.com`
  * `xyz.com/app`

---

### Role of Ingress Controller

Creating an Ingress resource alone does nothing.

An **Ingress Controller**:

* Reads the Ingress YAML configuration
* Understands routing rules
* Creates/configures the load balancer accordingly

This is similar to how:

* CCM handles `Service type LoadBalancer`

---

### Typical Architecture

1. Application runs inside an EKS cluster.
2. Service usually remains:

   * `ClusterIP`
   * or `NodePort`
3. DevOps engineer creates:

   * Deployment
   * Service
   * Ingress
4. Ingress Controller:

   * Reads ingress rules
   * Creates/configures load balancer
5. External users access app only through approved domain names.

---

### Ingress Features

#### Host-Based Routing

Allow access only through a specific domain:

```text id="lk2gxx"
amazon.com
```

#### Path-Based Routing

Allow access only on specific paths:

```text id="i1urq5"
amazon.com/xyz
```

---

### Important Ingress YAML Fields

Typical ingress configuration contains:

* `apiVersion`
* `kind: Ingress`
* `metadata`
* `spec`

Inside `spec`:

* Rules
* Hostnames
* Paths
* Backend service name and port

---

### Key DevOps Understanding

For internal services:

* Only Deployment + Service are needed.

For externally accessible applications:

* Deployment
* Service
* Ingress

Example:

* Frontend service → needs Ingress
* Internal email/microservices → usually do not need Ingress

---

### Interview Point

If asked:

> “When do you create Ingress?”

Answer:

* Create Ingress only when an application/service must be exposed externally with custom routing rules such as domain-based or path-based access.

---

# Part 2

<img width="1671" height="701" alt="image" src="https://github.com/user-attachments/assets/e1cf8f45-049e-4268-bd85-fff57f016eb6" />


## Summary of Ingress Controller in Kubernetes

* An **Ingress resource** only defines routing rules.
* The actual implementation is done by an **Ingress Controller**.

---

### Is Ingress Controller Available by Default?

No.

Kubernetes does **not** provide a default ingress controller because Kubernetes is **not opinionated** about which load balancer you should use.

It gives flexibility to choose:

* NGINX
* Kong
* Traefik
* AWS Application Load Balancer
* F5 load balancer
* NLB, etc.

Different load balancers support different capabilities such as:

* Host-based routing
* Path-based routing
* Blacklisting/whitelisting
* Advanced security features

---

### What Does the Ingress Controller Do?

The ingress controller:

* Watches Kubernetes Ingress resources
* Reads ingress YAML rules
* Creates/configures the load balancer accordingly

Without an ingress controller:

* Creating an Ingress resource does nothing.

---

### How Do You Deploy an Ingress Controller?

You choose the controller based on the load balancer you want to use.

Examples:

* NGINX → NGINX Ingress Controller
* Kong → Kong Ingress Controller
* Traefik → Traefik Ingress Controller
* AWS ALB → ALB Ingress Controller

These controllers are usually provided by the respective vendors or communities.

---

### Project Example in AWS EKS

For the project:

1. Deploy AWS ALB Ingress Controller.
2. Existing microservices remain deployed.
3. Create an Ingress resource for the frontend service.
4. ALB controller reads the ingress rules.
5. Controller creates an AWS Application Load Balancer.
6. Load balancer allows access only through the configured domain name.

---

### Important Concept

```text id="lxg73t"
Ingress Resource + Ingress Controller = Working External Routing
```

Without the controller:

* No load balancer gets created
* No routing rules are applied

---

### Key Interview Point

If asked:

> “Why is an ingress controller required?”

Answer:

* Because the Ingress resource only stores routing rules.
* The ingress controller is the component that reads those rules and configures the actual load balancer.

---
