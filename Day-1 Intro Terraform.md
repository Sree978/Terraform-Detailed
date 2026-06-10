Terraform is IAC ( Infrastructure as a code )
Infrastructure ( Servers, database & storage)
will use terraform for all cloud paltforms ( aws, Azure & GCP)
will use Hashicorp language 
We have 3 sections for code 
    1) provider section
        will mention ( cloud platform & region)
    2) Resource Section 
       service which will create ( ec2, ebs ,s3 ,asg, lb)
    3) variable section
         use to store the values 

    Steps

create a foler ( it's optional)
vim provider.tf
provider "aws" {
region = "us-east-1"
}

vim  main.tf
resource "aws_instance" "myinstance" {
  tags = {
    Name = "FLM-Servers"
  }

  ami           = "ami-0341d95f75f311023"
  instance_type = "t3.micro"
  key_name      = "swarm"
  availability_zone = "us-east-1a"

  root_block_device {
    volume_size = 12
  }
}

Indentation not manditary however indentation is manditary 

terraform init           -->   install plugins of our services
terraform fmt            --> to get indentation of all all our tf files
terraform plan            -->   its hits error 

before that we have to permission
 over IAM or user or role   ( IAM -USERS -create user - UN - next - attach plicy select ec2 full access- next & create user) go to crfeated user security credentials  will get access keys ( create access key  ) 
 
 while giving access will get access key or secret key  (copy local macine & use)

 real time will use user 

 aws configure 
 aws access key id  :
 secret key access :
 region 
 o/p format ( no need)

 Terraform plan 
 Terraform apply   / terraform apply --auto-approve (for run w/o permission)
 
 

will get know over statefile what and we made changes after terraform plan

If make changes in main.tf its communicate with statefile  7 compare 
( If its already same it wont create if its require changes it create )

 
 
 
 
 

         
         
          
