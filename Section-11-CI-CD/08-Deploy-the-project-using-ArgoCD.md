### Summary: Configuring GitOps Tool Argo CD with Git Repository

* The lecture demonstrates how to configure Argo CD to automatically deploy updated application versions from a Git repository.

### Creating an Argo CD Application

* In the Argo CD UI:

  * Click **Create Application**
  * Provide an application name (for example, `product-catalog-service`)
  * Keep the project as `default`

### Sync Policy

* Two deployment modes are available:

  1. **Manual Sync**

     * Deployment happens only when triggered manually.
  2. **Automatic Sync**

     * Argo CD continuously monitors the Git repository and automatically deploys changes.

* By default:

  * Argo CD checks the repository every **180 seconds**.
  * This polling interval can be customized through ConfigMaps.

### Repository Configuration

* Configure:

  * Git repository URL
  * Repository revision (`HEAD`)
  * Path containing Kubernetes manifests

* In this example:

  * The manifests are inside:

    * `kubernetes/product-catalog`

* Argo CD supports deploying:

  * Plain Kubernetes manifests
  * Helm charts
  * Kustomize configurations

### Cluster and Namespace

* Target cluster:

  * `https://kubernetes.default.svc`
  * This represents the same cluster where Argo CD is installed.

* Namespace selected:

  * `default`

### Deployment Process

* Once the application is created:

  * Argo CD detects the Deployment and Service manifests.
  * It creates a new ReplicaSet using the updated Docker image (`abhishekf5` version).

### Issue Encountered

* The new pod failed to become ready because:

  * The Kubernetes cluster lacked sufficient resources.

* Important observation:

  * The deployment itself was successful.
  * The new ReplicaSet and updated image version were correctly applied by Argo CD.

### DevOps Responsibility

* If deployment fails due to:

  * Application bugs
  * Code issues
  * Runtime problems

  → Those issues should be reported back to developers.

* DevOps responsibility mainly includes:

  * Ensuring CI/CD pipelines work correctly
  * Ensuring deployment automation functions properly
  * Maintaining cluster capacity and infrastructure

### Assignment Suggested

* Make a new code change in the repository.
* Verify the complete CI/CD flow:

  1. CI pipeline triggers
  2. New Docker image is built and pushed
  3. Kubernetes manifests are updated
  4. Argo CD automatically deploys the new version

### Overall Course Outcome

The section implemented end-to-end CI/CD for a microservices application including:

* Static code analysis
* Unit testing
* Docker containerization
* CI using GitHub Actions
* CD using GitOps with Argo CD
* Automated Kubernetes deployments


