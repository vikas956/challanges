# challanges

Challenge1
A three-tier architecture is a software architecture pattern where the application is broken down into three logical tiers: 
1.	Presentation layer, 
2.	Business logic layer 
3.	Data storage layer. 
This architecture is used in a client-server application such as a web application that has the frontend, the backend and the database.
 
GCP Services which we require are :-
1.	VPC
2.	Cloud NAT
3.	Subnets in Different Regions and Firewall Rules
4.	Application Load Balancer and Internal Load balancer)
5.	Managed Instance group
6.	Cloud DNS
7.	Bastion Host
8.	IAP
9.	Service Account
Above services we can create either through GCP console or through Infrastructure as code (IAC)
 Terraforms

 We will use of the following GCP services to design and build a three-tier cloud infrastructure:
1.	Setup the Virtual Private Cloud (VPC): Create subnets in 2 different regions.
To make little bit secure we will change firewall rule of VPC instead of 0.0.0.0/0 we will use source as IAP range and target will be based on the service account and will allow port 22.
2.	We will set up IAP security service to communicate internally via internal IP’s.
3.	Set up Cloud NAT to communicate with internet by attaching require Subnets.  
4.	Managed instance group.
5.	Create L7 HTTPS load balancer. Select Backend, Configure host and Path rule and Front End
6.	We will use some firewalls rule 
a. Allow SSH on port 22.
b. Allow health check of MIG on port 80.
7.	In Frontend configuration we will mention Frontend service name and port 80 for HTTP.
We will get IP address after creating load balancer
8.	Set up CLOUD DNS
Need to Enabling cloud DNS API and will MAP LB IP in DNS service provider.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

Challenge 2:-

•	Instance metadata is data about your instance that you can use to configure or manage the running instance.
•	Using Terraform Data Sources  we can retrieve or fetch the data from the cloud service providers such as AWS and      GCP.
•	Using terraform Apply we can create Instance at AWS .After creation its information is stored in state file which is in JSON format.
•	We can check information from state file by using
•	Terraform state show “aws_instance.ec2_example” 
•	This Output we can also store in any file in json format.
Code:- 
provider "aws" {
    region     = "eu-central-1"
    access_key = "AKIATQ37NXB2JMXVGYPG"
    secret_key = "ockvEN1DzYynDuKIh56BVQv/tMqmzvKnYB8FttSp"
}

resource "aws_instance" "ec2_example" {

    ami           = "ami-0767046d1677be5a0"
    instance_type =  "t2.micro"

    tags = {
      Name = "Terraform EC2"
    }
}

data "aws_instance" "myawsinstance" {
    filter {
        name = "tag:Name"
        values = ["Terraform EC2"]
    }

    depends_on = [
      "aws_instance.ec2_example"
    ]
}

output "fetched_info_from_aws" {
  value = data.aws_instance.myawsinstance.public_ip
}

----------------------------------------------------------------------------------------------------------------------------------------------------------------

 Challenge 3:-

import json

# some JSON:
obj = '{"a":{"b":{"c":"d"}}}'
keys= list("a","b","c")
# parse x:
y = json.loads(obj)
i=1
# the result is a Python dictionary:
for x in keys:
try:
y=y[x]
if i= len(keys):
print(y)
else: i+1 
except:
 return "key not found"

