<img width="1526" height="804" alt="image" src="https://github.com/user-attachments/assets/6c274e3d-c800-441e-ae5b-4c482831d230" />

### Summary of the Lecture

This lecture explains different ways to get started with Kubernetes and why managed Kubernetes services are commonly used in real-world environments.

## Ways to Run Kubernetes

### 1. Local Kubernetes Clusters

Local platforms mentioned:

* Minikube
* K3s
* Kind
* MicroK8s
* K3D

Purpose:

* Mainly used for development and learning.
* Can run locally on a laptop or workstation.

Limitations:

* Not commonly used in production.
* Requires manual management of:

  * Scaling
  * Upgrades
  * Cost optimization
  * Cluster maintenance

---

### 2. Self-Managed Kubernetes on Virtual Machines

* Create multiple VMs or EC2 instances.
* Install Kubernetes manually using tools like kubeadm.

Example:

* Create 3–5 EC2 instances and configure the cluster manually.

Challenges:

* High operational overhead
* Manual cluster management
* Difficult upgrades and maintenance

---

### 3. Managed Kubernetes Services (Preferred in Real Time)

Popular managed services:

* Amazon Web Services EKS (Elastic Kubernetes Service)
* Microsoft AKS (Azure Kubernetes Service)
* Google GKE (Google Kubernetes Engine)
* Managed OpenShift
* Rancher-managed Kubernetes

Benefits:

* Easier Kubernetes upgrades
* Cloud providers manage the control plane
* Some providers also manage the data plane
* Easier scaling of nodes
* Integrated Kubernetes UI and tooling
* Better enterprise support and reliability

---

## Important Kubernetes Concepts Mentioned

* **Control Plane**

  * Runs core Kubernetes components.
  * Manages the cluster.

* **Data Plane**

  * Runs application workloads and pods.

---

## Project Approach in the Course

For this project:

* A managed Kubernetes cluster using Amazon Web Services EKS will be used.
* The EKS cluster will be created using Terraform.

Why Terraform:

* Infrastructure as Code (IaC) is widely used in real-world DevOps environments.
* Infrastructure will not be created manually.
* Best practices such as:

  * Remote backend
  * State locking
  * VPC creation
    will also be covered.

Final takeaway:

* Managed Kubernetes services are the industry standard for production environments.
* Learning Kubernetes together with Terraform and cloud-managed services is highly valuable for real-world DevOps work and interviews.
