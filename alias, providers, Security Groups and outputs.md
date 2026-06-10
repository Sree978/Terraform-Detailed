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
