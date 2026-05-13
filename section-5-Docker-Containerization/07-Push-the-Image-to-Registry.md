### Summary of the Lecture

This lecture explains how to share Docker images using container registries after building and running containers locally.

Key concepts covered:

* Previously, Dockerfiles were created, Docker images were built, and containers were run locally on an EC2 instance.
* Local Docker images can only be used on the same machine unless they are shared through a centralized platform.
* To share images with developers, QA engineers, or other teams, Docker images are pushed to **container registries**.

Popular container registries mentioned:

* Docker Hub
* Amazon Web Services Elastic Container Registry (ECR)
* Quay.io

Main workflow explained:

1. **Choose a container registry**

   * Example: organizations using AWS may prefer ECR.
   * Public/open organizations may use Docker Hub or Quay.io.

2. **Authenticate with the registry**

   * Use the `docker login` command.
   * Examples:

     * `docker login docker.io`
     * `docker login quay.io`
     * `docker login <ECR_URL>`

3. **Push Docker images**

   * Use the `docker push` command.

Example:

```bash
docker push abhishekf5/product-catalog:v2
```

The lecture explains the structure of an image name:

```text
docker.io / username / repository : tag
```

Meaning:

* `docker.io` → registry
* `username` → account/user
* `repository` → image repository name
* `tag` → image version

Example:

```text
docker.io/abhishekf5/product-catalog:v2
```

Important points:

* If `docker.io` is omitted, Docker assumes Docker Hub by default.
* Pushing an image can automatically create a new repository if it does not already exist.
* Multiple microservice images such as Product Catalog, Ad Service, and Recommendation Service were pushed successfully.

Final takeaway:

* Container registries allow teams to centrally store and share Docker images.
* Understanding the image naming format (registry, username, repository, tag) is essential for working with Docker push commands and different registries.
