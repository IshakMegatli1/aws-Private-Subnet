# Creating a Private Subnet

![Image](http://learn.nextwork.org/lively_blue_beautiful_jellyfish/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project!


### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to set up a private subnet, a private route table and a private network ACL.

I created a private subnet : a new subnet and set its CIDR block to avoid an overlap with my public subnet.

I created a private route table. I also made this subnet private by assigning it to a dedicated route table that doesn't route traffic to an internet gateway.

I created a private network ACL: Then, I set up custom network ACLs to control inbound and outbound traffic for this private subnet, denying all traffic by default.


### This project took me 1 hour


---

## Private vs Public Subnets

A public subnet has a route to an Internet Gateway, so resources can be reached from the internet while a private subnet has no direct route to an Internet Gateway so resources can't be directly reached from the internet.

Having private subnets are useful because some resources need to be private (not on the public internet). Example : databases, backends ...

My private and public subnets cannot have the same CIDR address blocks because they risk overlaping. They also can't share the same route table.

![Image](http://learn.nextwork.org/lively_blue_beautiful_jellyfish/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, my private subnet is associated with the VPC’s main route table (default one)

I had to set up a new route table to control routing per subnet instead of letting subnets inherit the VPC’s main route table. (To create a route table for my private subnet)

My private subnet's dedicated route table only has one inbound and one outbound rule that allows local traffic within the VPC CIDR.

![Image](http://learn.nextwork.org/lively_blue_beautiful_jellyfish/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, my private subnet is associated with the VPC’s default network ACL (the one AWS creates automatically)

I set up a dedicated network ACL for my private subnet because I need to apply subnet-level allow/deny rules that are different from the default network ACL. 

My new network ACL has two simple rules : deny all inbound and outbound traffic 

![Image](http://learn.nextwork.org/lively_blue_beautiful_jellyfish/uploads/aws-networks-private_1ed2cb07)

---

---
