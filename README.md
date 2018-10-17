# ansibleproject

# ansible-aws-vpc-ec2

Ansible playbook to automate cloud networking in an AWS VPC. The following will be configured and built:

1) VPC and Subnets: create the VPC with two subnets across two us-east-1 availability zones: a and b

2) Internet Gateway: configure a gateway to access the internet

3) Security Groups: security groups for limiting communication only within the VPC, and/or to allow SSH or HTTP/S traffic from the public internet

4) Create Launch Configuration, ELB and ASG with Scaling policies and Alarm

5) Install Nginx on the instances in both the zones for HA and access the http page through the ELB DNS name

Folder Structure

|--playbook.yml

|--inventory

|-- vars.yml

|--roles/

|   |---vpc/

|   |   |--tasks/

|   |   |  |----vpc.yml

|   |   |  |----ec2.yml

playbook.yml
Define the list of roles we want to apply to a group of hosts.

inventory
The group of hosts which will run the playbook is defined in the inventory file.

vars.yml
All the variables used in the playbook are listed in this file

vpc.yml
Creates VPC, Subnets, Internet Gateway, Route Table and SG

ec2.yml
Creates SG for EC2 instances, keypair, Launch Configuration, ELB, ASG, Scaling and Alarms

NOTE
1) You will need to replace the AWS credentials variables
2) Optional, you can change the AWS region
3) my_local_cidr_ip, variable is used to configure Security Group (SG) that the playbook will add to the VPC. The SG will allow incming SSH access from this IP only to any EC2 instances attached with this group.

Running the Ansible playbook
ansible-playbook -i inventory/hosts playbook.yml
