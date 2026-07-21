VPC is large network divided like small network subnet 1-a, Subnet 1-b, subnet 1-c and place each network in different   data centers for getting high availability of application 
we have two types of subnets public and private 
public subnet - will hold LB 
private subnet - will store our actuval application  , we can't access servers over internet , will use NAT to access resources which is in private subnet , 
while creating VPC we haev to IGW ( internet gateway )

CIDR - Classless inter domain range 

Cretae VPC and two subnets & internet gate way and attach to vpc , create route table its default 


VPC 

![Uploading image.png…]()

provider.tf 

vpc.tf
resource "aws_vpc" "myvpc" {
  tags = {
    Name = "Terraform-VPC"
  }

  cidr_block           = "10.0.0.0/16"
  instance_tenancy     = "default"
  enable_dns_hostnames = true
}

subnet.tf 

resource "aws_subnet" "mysubnet1" {
  vpc_id = aws_vpc.myvpc.id

  tags = {
    Name = "Public-SN-1"
  }

  availability_zone       = "us-east-2a"
  cidr_block              = "10.0.0.0/24"
  map_public_ip_on_launch = true
}

resource "aws_subnet" "mysubnet2" {
  vpc_id = aws_vpc.myvpc.id

  tags = {
    Name = "Public-SN-2"
  }

  availability_zone       = "us-east-2b"
  cidr_block              = "10.0.1.0/24"
  map_public_ip_on_launch = true
}

IGW.tf
resource "aws_internet_gateway" "myigw" {

  tags = {
    Name = "TERRAFORM-IGW"
  }

  vpc_id = aws_vpc.myvpc.id
}

route table.tf

resource "aws_route_table" "myrt" {

  tags = {
    Name = "Terraform-RT"
  }

  vpc_id = aws_vpc.myvpc.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.myigw.id
  }
}









