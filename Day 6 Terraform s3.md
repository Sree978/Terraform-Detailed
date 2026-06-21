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
  default = "sree.terraform.tinku.bucket.dev20260621"
}


Terraform init
Terraform apply --auto-approve

To store statefile into s3 


vim bacekend.tf
terraform {
  backend "s3" {
    bucket = "sree.terraform.tinku.bucket.dev20260621"
    key    = "prod/terraform.tfstate"
    region = "us-east-1"
  }
}

Terraform init 
terraform apply --auto-approve

server.tf
resource "aws_instance" "myserver" {

  tags = {
    Name = "terraformserver"
  }

  ami           = "ami-0521cb2d60cfbb1a6"
  instance_type = "t2.micro"
}

Terraform init 
terraform apply -auto-approve

will notice whenever we update infrastructure will notice our state files and previous statefile also 
 will get s3 and ec2 storage also 

 ---> to store war /jar files in s3 

 Install jenkins

 In jenkins install plugins

 stage pipleline view and s3 publisher
 Instta manage jekins > system > s3
 

 
 
 



 








