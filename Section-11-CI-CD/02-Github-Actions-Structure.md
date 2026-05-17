
<img width="1593" height="690" alt="image" src="https://github.com/user-attachments/assets/8fe8fe7b-7d30-4b27-b4df-5a32f22642ce" />



## Summary

* DevOps engineers usually manage CI/CD only for the microservices owned by their development team, not the entire organization.
* The example focuses on implementing CI/CD for the **product catalog microservice**.

### GitHub Actions

* GitHub Actions is GitHub’s built-in CI orchestrator.
* CI workflows are defined using YAML files inside:

  ```text
  .github/workflows/
  ```
* Example file:

  ```text
  ci.yaml
  ```

### Purpose of Workflow File

The YAML workflow file tells GitHub:

* when to trigger CI,
* what jobs to run,
* and what steps to execute.

### GitHub Actions (Plugins)

GitHub provides reusable actions/plugins, such as:

* checkout action → clones repository
* Docker login/push actions
* language setup actions (Java, Go, etc.)

This reduces the need to manually write shell commands.

### Basic Workflow Structure

A GitHub Actions workflow typically contains:

1. **name**

   * Name of the workflow

2. **trigger**

   * Defines when CI should run:

     * pull request
     * push/commit
     * or both

3. **jobs**

   * Organizes CI tasks into separate sections for:

     * readability,
     * troubleshooting,
     * and parallel execution.

### Example Jobs

* **build job**

  * checkout code
  * install dependencies/language
  * run unit tests

* **static code analysis job**

  * scan code quality/issues

* **docker job**

  * build and push Docker image

### Important Point

* All steps can technically exist in one job,
* but separating them into multiple jobs makes CI pipelines cleaner and easier to manage.
