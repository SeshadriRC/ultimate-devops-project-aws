<img width="1893" height="875" alt="image" src="https://github.com/user-attachments/assets/d3f49bea-f326-43e2-8e5d-62ee726a182d" />


## Summary of CI/CD Introduction

* **CI/CD** stands for:

  * **CI (Continuous Integration)** → focuses on building, testing, and validating code.
  * **CD (Continuous Delivery/Deployment)** → focuses on deploying applications.

### Why CI/CD is Needed

Before CI/CD, developers manually:

* tested code,
* built applications,
* created Docker images,
* checked for security issues,
* and deployed applications.

This caused problems because:

* developers may skip steps,
* reviewers cannot fully verify everything manually,
* bad code or vulnerabilities can enter the repository,
* and other developers get impacted when they pull broken code.

### Example Workflow Without CI/CD

1. Developer Ram creates a pull request (PR).
2. Another developer reviews and merges it manually.
3. If Ram’s code has:

   * compilation issues,
   * security vulnerabilities,
   * outdated packages,
   * or broken Docker images,

   the entire team gets affected.

### How CI Solves This

DevOps engineers automate the validation process using CI tools like:

* GitHub Actions
* Jenkins

Typical CI pipeline stages:

1. Checkout code on a fresh VM/environment
2. Run unit tests
   
    - Examines source code without executing it to detect syntax issues, bad practices, vulnerabilities, or code quality problems.
3. Perform static code analysis

    - Examines source code without executing it to detect syntax issues, bad practices ( if functions not used or any outdated packages ), vulnerabilities, or code quality problems.
   
6. Build the application
7. Create Docker image
8. Scan Docker image for vulnerabilities
9. Push Docker image
10. Update Kubernetes manifests with new image version

### Benefits of CI

* Reduces manual effort
* Improves code quality
* Saves developer and reviewer time
* Ensures only validated code gets merged
* Increases confidence in deployments

### What CD Does

After CI completes:

* CD tools automatically deploy the updated application to Kubernetes clusters.

Common CD/GitOps tools:

* Argo CD

This allows:

* testers to perform integration/regression testing,
* developers to verify deployments,
* and teams to continuously release updates.

### Continuous Process

CI/CD pipelines usually run:

* on every pull request,
* every commit,
* or both.

This ensures:

* every change is tested,
* validated,
* and deployed automatically.

### Key Takeaway

CI/CD:

* automates software delivery,
* improves reliability,
* speeds up development cycles,
* reduces operational overhead,
* and enables faster, safer deployments in Kubernetes-based microservices environments.
