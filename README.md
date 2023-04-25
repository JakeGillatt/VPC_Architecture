# VPC Architecture
#
# What is VPC architecture?

A virtual private cloud (VPC) is a virtual network dedicated to your AWS account. It is logically isolated from other virtual networks in the AWS Cloud. You can specify an IP address range for the VPC, add subnets, add gateways, and associate security groups.

#
# Why use a VPC?

A VPC allows you to secure your virtual networking environment, including your IP addresses, subnets and network gateways. For instance, you can securely isolate a database in a private-facing subnet that isn't connected to the internet.

#
# What is a subnet?

A subnet, or subnetwork, is a network inside a network. Subnets make networks more efficient. Through subnetting, network traffic can travel a shorter distance without passing through unnecessary routers to reach its destination.

#
# What is a CIDR block?

A CIDR block is a collection of IP addresses that share the same network prefix and number of bits. A large block consists of more IP addresses and a small suffix. The Internet Assigned Numbers Authority (IANA) assigns large CIDR blocks to regional internet registries (RIR).

#
# What is an Internet Gateway?

An Internet gateway is a network "node" that connects two different networks that use different protocols (rules) for communicating. In the most basic terms, an Internet gateway is where data stops on its way to or from other networks. Thanks to gateways, we can communicate and send data back and forth with each other.

#
# What are Route Tables?

A route table contains a set of rules, called routes, that determine where network traffic from your subnet or gateway is directed.

Your VPC has an implicit router, and you use route tables to control where network traffic is directed. Each subnet in your VPC must be associated with a route table, which controls the routing for the subnet (subnet route table). You can explicitly associate a subnet with a particular route table. Otherwise, the subnet is implicitly associated with the main route table. A subnet can only be associated with one route table at a time, but you can associate multiple subnets with the same subnet route table.

#
# VPC Diagram:
![VPC-diagram](https://user-images.githubusercontent.com/129315605/234340160-9eea70cf-1f33-4b8a-844d-ed8c9b8f3d6b.png)
#
# How to deploy the node app in VPC

---APP Instance---

1. Head to the VPC dashboard in AWS and Create a VPC
- On AWS website type VPC in the search bar and then in Services select VPC
- On the new page select Create VPC
- Complete the VCP settings as following:
VPC Only
'your name'-tech221-vcp - name
IPv4 CIDR set to 10.0.0.0/16
Leave the rest as default
3. Create AMI's of your app and database instances
4. In the VPC dashboard select Internet Gateways
- Select Create internet gateway
- Name the gateway and create it
5. In the VPC dashboard, select subnets from the left VPC menu list
- Select 'Create subnet'
- Select your VPC from the dropdown
- Name the subnet ending in public
- Select the region
- Enter a IPv4 CIDR block e.g `10.0.11.0/24`
- Create the subnet - this is your public subnet for the app
6. In the VPC dashboard select Route tables
- Select Create route tables
- Name the route table and select your VPC
- Add `0.0.0.0/0` to create public access
- Create the route table (public)
7. Go to subnets and select your public subnet from the list
- Under the 'route table' section, select 'edit route table association`
- Add your route table to the subnet and save
8. Go to the EC2 dashboard and select 'Launch instance'
- Name the instance and select your app AMI
- Select the key-pair
- Under Network settings select 'Edit'
- Select the VPC and the public subnet
- Enable auto assign public ip
- Select create security group and add the following rules:
SSH, source type: My ip
HTTP, Source type: anywhere
Custom TCP, Source type: anywhere, Port: 3000
- Launch the instance
#
---Database Instance---

1. Create a new subnet from the VPC dashboard
- Select your VPC
- Name it ending in private
- Select the right region if neccissary
- Add private IPv4 CIDR block - e.g `10.0.12.0/24`
- Create the subnet
2. Create a route table
- Name it
- Select your VPC
- Select create
3. Go to the EC2 dashboard and select 'Launch instance'
- Name the instance and select your database AMI
- Select the key-pair
- Under Network settings select 'Edit'
- Select the VPC and the private subnet
- Disable auto assign public ip
- Select create security group and add the following rule:
Custom TCP, source type: anywhere, Port: 27017
- Launch the instance
4. In your git bash terminal SSH into the app instance
5. Edit your .bashrc file and add the new IP for the database
6. Run `source .bashrc` to refresh the file
7. In the app folder run the `node app.js` command to start the app
8. Head over to your browser and enter 'your ip'/posts to see the posts page of the app
