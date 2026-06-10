Try over VScode
open remote window > connect to host > add new ssh host  type enter and enter
open ,ssh/config > open config change details
    Host terraform-server
    HostName 54.91.160.25    --> our server public IP
    User ec2-user
    IdentityFile ~/Downloads/swarm.pem   --> our pem key path   + save
    click on connect to host 
    go to root user before that 
    sudo chmod 777 /root   --> to give permisiion for root user 

  Same path will create 
  provider.tf 
  main.tf 
  var.tf
  



output.tf 
output "myOutput" {
  value = [aws_instance.myinstance[0].public_ip, aws_instance.myinstance[1].private_ip]
}


---> How to create security group and attach to our server 
security.tf
resource "aws_security_group" "mysg" {
  name        = "Terraform-SG"
  description = "This is created by terraform"

  ingress {
    protocol = "tcp"
    from_port =22
    to_port =22
    }
      ingress {
    protocol = "tcp"
    from_port =80
    to_port =80
    }
    egress {
  protocol    = "-1"
  from_port   = 0
  to_port     = 0
  cidr_blocks = ["0.0.0.0/0"]
}


    ---> Alias & Provider  <---

    Two server will be create in two different Regions (Norh or virginia & mumbai)

    Main.tf
    resource "aws_instance" "nvinstance" {

  tags = {
    Name        = "NV-Instance"
    Environment = "Dev"
    Client      = "FLM"
  }

  ami           = "ami-0341d95f75f311023"
  instance_type = "t3.micro"
  key_name      = "swarm"
}

resource "aws_instance" "southinstance" {
 provider = aws.mumbai
  tags = {
    Name        = "Mumbai-Instance"
    Environment = "Dev"
    Client      = "FLM"
  }
     ami           = "ami-0341d95f75f311023"   --> ita change
  instance_type = "t3.micro"
  key_name      = "mini"
}


Providers.tf

provider "aws" {
  region = "us-east-1"
}

provider "aws" {
  region = "ap-south-1"
  alias  = Mumbai
}
