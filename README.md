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
