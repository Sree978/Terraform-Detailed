Take one server and install jenkins we have to give s3 full access
Vim provider.tf
vim resource.tf
resource "aws_s3_bucket" "mybucket" {
  bucket = var.bucket_name
}

resource "aws_s3_bucket_versioning" "bucketversioning" {
  bucket = aws_s3_bucket.mybucket.id

  versioning_configuration {
    status = "Enabled"
  }
}

variable "bucket_name" {
  type    = string
  default = "sree.terraform.tinku.bucket"
}
~

Terraform init
Terraform apply --auto-approve

