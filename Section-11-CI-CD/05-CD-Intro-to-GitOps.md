<img width="1895" height="954" alt="image" src="https://github.com/user-attachments/assets/b9c40d39-3081-411c-a857-6da2edab0f1c" />

### Summary: Continuous Delivery (CD) with GitOps

* In the previous lecture, the CI pipeline handled:

  * Unit testing
  * Build stages
  * Static code analysis
  * Docker image creation and push
  * Updating Kubernetes manifests

* After CI completes, the CD process begins:

  * A CD tool reads the updated Kubernetes manifests.
  * It deploys the new application version to the Kubernetes cluster.
  * Developers or QA engineers can then verify the deployed changes.
  * The full CI/CD cycle usually completes within 2–10 minutes.

### GitOps Concept

* GitOps is a popular CD approach where:

  * Kubernetes manifests are stored in a version control system (commonly Git).
  * A CD tool like Argo CD continuously monitors the repository.
  * When manifest changes are detected, it automatically deploys them to the target platform (commonly Kubernetes).

* Although GitOps is not limited to Git or Kubernetes:

  * Git is the most common version control system.
  * Kubernetes is the most common deployment target.

### Benefits of GitOps

1. **Automatic Deployment**

   * The CD tool constantly monitors the repository.
   * Any new image/version updates are automatically deployed.

2. **Reconciliation / Desired State Management**

   * The version control system acts as the “source of truth.”
   * If someone manually changes resources in the cluster, GitOps tools detect the drift and restore the cluster to the state defined in Git.

3. **Continuous Synchronization**

   * Sync operations happen automatically at regular intervals (for example, every few minutes).
   * No manual monitoring or triggering is required.

### Key Point

* Only approved changes pushed through CI and stored in Git are deployed.
* Manual changes directly on the cluster are overwritten to maintain consistency.

### Next Step

* The next lecture focuses on:

  * Installing Argo CD
  * Connecting it to the Git repository
  * Demonstrating automatic Kubernetes deployment updates using GitOps.
