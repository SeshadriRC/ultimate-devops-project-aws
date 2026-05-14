# Kubernetes Service Account

## What is a Service Account in Kubernetes?

A Service Account in Kubernetes is an identity that pods can use to interact with the Kubernetes API. It provides a way for applications running in pods to authenticate and authorize themselves to perform actions within the cluster.

## Why is it Important?

Service Accounts are important for several reasons:
- **Security**: They provide a secure way for applications to interact with the Kubernetes API without using user credentials.
- **Granular Access Control**: Service Accounts can be assigned specific roles and permissions, allowing fine-grained control over what actions a pod can perform.
- **Isolation**: Different applications or components can use different Service Accounts, ensuring that they only have access to the resources they need.

## Default Service Account

If a user does not specify a Service Account for a pod, Kubernetes automatically assigns the default Service Account in the namespace. This default Service Account has limited permissions and is intended for general use. However, for more secure and controlled access, it is recommended to create and use custom Service Accounts with appropriate roles and permissions.

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: example-pod
spec:
    serviceAccountName: custom-service-account
    containers:
    - name: example-container
        image: example-image
```

In the above example, the `serviceAccountName` field specifies the Service Account to be used by the pod. If this field is omitted, the default Service Account in the namespace will be used.

---

### Summarized


# Summary

* In demo Kubernetes projects, people often deploy pods without explicitly creating a Service Account.
* In real-world environments, every pod should ideally use a dedicated Service Account.

---

# User Account vs Service Account

## User Account

Used by humans such as:

* DevOps engineers
* Developers
* Administrators

Purpose:

* Access Kubernetes cluster
* Use `kubectl`
* Access Kubernetes UI/dashboard

User accounts use:

* kubeconfig
* authentication credentials

---

## Service Account

Used by:

* Pods
* Applications
* Microservices
* Controllers

Purpose:

* Allow services running inside Kubernetes to interact with the cluster/API.

---

# Important Concept

Every pod in Kubernetes must run with a Service Account.

If you do not specify one manually:

```text id="jlwm6q"
Kubernetes automatically assigns
the default Service Account
from that namespace.
```

You can verify it using:

```bash id="jlwm6q"
kubectl get sa
```

or

```bash id="jlwm6q"
kubectl get sa -n kube-system
```

---

# Default Service Account

Kubernetes creates a `default` Service Account in every namespace.

This default account gives minimal permissions such as:

* allowing pods to run

This is why demo applications work even without explicitly creating Service Accounts.

---

# Why Service Accounts Need Permissions

Sometimes applications need to:

* access Kubernetes API server
* read ConfigMaps
* manage resources
* build controllers/operators
* use webhooks/admission controllers

For such cases, the Service Account requires additional permissions.

---

# How Permissions Are Given

## Step 1: Create Role or ClusterRole

Defines permissions.

Examples:

* read pods
* access ConfigMaps
* manage deployments

---

## Step 2: Bind Role to Service Account

Using:

* `RoleBinding`
* `ClusterRoleBinding`

This connects:

* Service Account → Role

---

# Flow

```text id="jlwm6q"
Pod
 ↓
Service Account
 ↓
Role / ClusterRole
 ↓
Permissions
```

---

# AWS Analogy

This is similar to AWS IAM:

| AWS               | Kubernetes       |
| ----------------- | ---------------- |
| IAM User/Role     | Service Account  |
| IAM Policy        | Role/ClusterRole |
| Policy Attachment | RoleBinding      |

---

# Key Takeaway

* Demo projects often rely on the default Service Account.
* Production workloads should use dedicated Service Accounts.
* Service Accounts allow pods to securely access Kubernetes resources.
* Additional permissions are controlled using Roles and RoleBindings.
