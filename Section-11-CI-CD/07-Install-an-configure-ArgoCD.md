### Summary: Installing and Accessing GitOps Tool Argo CD

* The lecture focuses on installing Argo CD on a Kubernetes cluster running on an EC2 instance.

### Installation Process

* The instructor refers to the official documentation of Argo CD for installation methods:

  * Helm chart
  * Plain Kubernetes manifests
  * Kubernetes Operator

* For this demo, installation is done using plain Kubernetes manifests.

### Steps Performed

1. Create a namespace called `argocd`.
2. Apply the Argo CD manifest YAML file.
3. Verify installation using:

   * `kubectl get pods -n argocd`
   * `kubectl get svc -n argocd`

### Argo CD Architecture

* Argo CD is a complex controller with multiple internal components:

  * Git repository synchronization
  * Kubernetes cluster state monitoring
  * Web UI hosting
  * OIDC/authentication handling

* Even though the backend architecture is complex, the end-user experience is designed to be simple.

### Exposing the Argo CD UI

* The `argocd-server` service is edited:

  * Service type changed to `LoadBalancer`

* Alternative option:

  * Use Kubernetes Ingress with AWS ALB Controller

* After waiting a few minutes, the external load balancer becomes available and the UI can be accessed from the browser.

### Logging into Argo CD

* Retrieve the initial admin secret:

  * `kubectl get secrets -n argocd`

* Find the `argocd-initial-admin-secret`

* Decode the Base64 password using:

  * `echo <encoded-password> | base64 --decode`

* Login credentials:

  * Username: `admin`
  * Password: decoded secret value

### Important Concept

* Argo CD does not need to run on the same Kubernetes cluster it manages.
* In enterprise environments:

  * A centralized Argo CD instance can manage multiple clusters.
  * This architecture is commonly called the **Hub-Spoke model**.

