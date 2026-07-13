![VPC Diagram](<Images/VPC Diagram.png>)
Type VPC in search Bar, click all VPCs -> Create VPC

Select:
- VPC only
- give it a sensible name tag
- for the IPv4 CIDR manual input: 10.0.0.0/16
- No IPv6 CIDR block
- No VPC encryption
- Create VPC
### Subnets

- Subnets -> Create subnet
- Select the VPC you just made

name the subnets public and private respectively including with these settings
public:
- cohort+name+public-subnet
- Availability zone = 1a
- IPv4 VPC CIDR block = 10.0.0.0/16
- IPv4 subnet CIDR block = 10.0.2.0/24
private:
- cohort+name+private-subnet
- Availability zone = 1b
- IPv4 VPC CIDR block = 10.0.0.0/16
- IPv4 subnet CIDR block = 10.0.3.0/24
Select Create Subnet

### Internet Gateways
- Go to VPCs -> Internet gateways -> Create internet
- name it vpc_name+igw
- Select Create Internet Gateway
Once created you should see a prompt in green to attach to VPC Otherwise you can Select your IG and go to actions to find this button, select your vpc and attach it to the gateway.

### Route Table
- Go to VPCs -> Route tables -> Create route tables
- name it vpc_name+rt
- Select Create Route Table.
Head to your newly created route table and select Subnet associations -> Explicit subnet associations -> Edit subnet associations and add the public subnet

in Routes -> Edit routes add a new route for Destination 0.0.0.0/0 with the target set to Internet Gateway, select your internet gateway from the dropdown just below


### Creating our Instances

Create an instance from the DB AMI first, Select the keys as usual but in network settings click edit and do the following:
- Select your VPC
- Select your private subnet
- Select Disable for Auto-assign public IP 
- Create a security group that allows SSH and custom TCP from CIDR 10.0.2.0/24 at port 27017
- Select Launch Instance

For the App AMI do the same but:
- Select public subnet
- Select Enable for Auto-assign public IP  
- Create a security group that allows SSH and allow HTTP from any IP
- Enter your userdata to provision the instance with the private IP you got from the DB
- Select Launch Instance