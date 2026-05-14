[code-link](https://github.com/SeshadriRC/ultimate-devops-project-aws/blob/main/eks-install/backend/main.tf)

# Code explanation for S3 bucket and DynamoDB terraform file

## **1. AWS Provider Configuration**
```hcl
provider "aws" {
  region = "us-west-2"
}
```
- This block defines the **AWS provider** that Terraform will use.
- The `region` attribute specifies the AWS region where resources will be created (in this case, `us-west-2`).

---

## **2. Creating an S3 Bucket for Terraform State Storage**
```hcl
resource "aws_s3_bucket" "terraform_state" {
  bucket = "demo-terraform-eks-state-bucket"

  lifecycle {
    prevent_destroy = false
  }
}
```
- This block creates an **S3 bucket** named `demo-terraform-eks-state-bucket`.
- The `lifecycle` rule with `prevent_destroy = false` allows Terraform to delete the bucket when required.

---

## **3. Enabling Versioning for the S3 Bucket**
```hcl
resource "aws_s3_bucket_versioning" "terraform_state" {
  bucket = aws_s3_bucket.terraform_state.id
  versioning_configuration {
    status = "Enabled"
  }
}
```
- This block enables **versioning** on the S3 bucket to retain previous versions of the Terraform statefile.
- Helps with rollback and recovery in case of accidental changes.

---

## **4. Enabling Server-Side Encryption for the S3 Bucket**
```hcl
resource "aws_s3_bucket_server_side_encryption_configuration" "terraform_state" {
  bucket = aws_s3_bucket.terraform_state.id

  rule {
    apply_server_side_encryption_by_default {
      sse_algorithm = "AES256"
    }
  }
}
```
- This block **enables encryption** using the `AES256` algorithm to protect statefile data at rest.
- Ensures that Terraform statefiles are stored securely in the S3 bucket.

---

## **5. Creating a DynamoDB Table for State Locking**
```hcl
resource "aws_dynamodb_table" "terraform_locks" {
  name         = "terraform-eks-state-locks"
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "LockID"

  attribute {
    name = "LockID"
    type = "S"
  }
}
```
- This block creates a **DynamoDB table** named `terraform-eks-state-locks`.
- The table is used for **state locking**, preventing concurrent modifications to the statefile.
- `billing_mode = "PAY_PER_REQUEST"` ensures cost-effective pricing based on actual usage.
- The primary key (`hash_key`) is `LockID`, ensuring unique entries for locks.

### Practicals

- Below is the yaml , which abhi used for practical purpose. However doc contains extra parameters in the block

```hcl
provider "aws" {
  region = "ap-south-1"
}

resource "aws_s3_bucket" "terraform_state" {
  bucket = "sesh-terraform-eks-state-s3-bucket"

  lifecycle {
    prevent_destroy = false
  }
}

resource "aws_dynamodb_table" "terraform_locks" {
  name         = "terraform-eks-state-locks"
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "LockID"

  attribute {
    name = "LockID"
    type = "S"
  }
}
```

- S3 bucket

<img width="1386" height="482" alt="image" src="https://github.com/user-attachments/assets/b5a593e2-a44d-4d12-9ee5-6cc1b7559236" />


- DyanomoDB table

<img width="1919" height="469" alt="image" src="https://github.com/user-attachments/assets/a751942d-b798-4248-bd4a-5e29f9f3d2e3" />



