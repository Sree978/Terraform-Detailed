VPC is large network divided like small network subnet 1-a, Subnet 1-b, subnet 1-c and place each network in different   data centers for getting high availability of application 
we have two types of subnets public and private 
public subnet - will hold LB 
private subnet - will store our actuval application  , we can't access servers over internet , will use NAT to access resources which is in private subnet , 
while creating VPC we haev to IGW ( internet gateway )

CIDR - Classless inter domain range 

Cretae VPC and two subnets & internet gate way and attach to vpc , create route table its default 


VPC 

<img width="1028" height="599" alt="image" src="https://github.com/user-attachments/assets/30bd6b25-396f-43bb-9e0c-e18208045a3a" />




