Statefile lock : 
If we are using two persons same tf file at a time and modifying both same time , its happen over clash 
statefile will corrupt in these case

So will usee statefile lock here 

install terrform 

Terraform acquires a state lock to protect the state from being written
 by multiple users at the same time. Please resolve the issue above and try
again. For most commands, you can disable locking with the "-lock=false"
lag, but this is not recommended.

Vim provider.tf
provider "aws"  {
region = "us-east-1"
}


vim resource.tf
resource "aws_instance" "myserver" {
ami = "ami-0521cb2d60cfbb1a6"
instance_type = "t2.micr"
tags = {
name = "statefilelock123"
}
}

vim backend.tf
terraform {
backend "s3" {
bucket = "sree.terraform.tinku.bucket.dev20260621"
region = "us-east-1"
key = "prod/terraform.tfstate"
use_lockfile = true

}

}



