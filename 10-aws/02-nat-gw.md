To access the Internet, one public IP address is needed, but we can use a private IP address in our private network. The idea of NAT is to allow multiple devices to access the Internet through a single public address. To achieve this, the translation of a private IP address to a public IP address is required. 
Network Address Translation (NAT) is a process in which one or more local IP address is translated into one or more Global IP address and vice versa in order to provide Internet access to the local hosts. Also, it does the translation of port numbers i.e. masks the port number of the host with another port number, in the packet that will be routed to the destination. It then makes the corresponding entries of IP address and port number in the NAT table. NAT generally operates on a router or firewall. 

## AWS NAT Gateways
Amazon Web Services (AWS) NAT Gateway - stands for Network Address Translation. It is a managed AWS service that is scaled based on your usage. NAT Gateway will help you to access the internet which instances are configured in the private subnet but without proper routing, no one can access that instance from outside.

## Types Of AWS NAT Gateways

1. Public: NAT Gateway that resides in a public subnet. You can access the internet from the instance which is residing in the private subnet but others cant access this instance which is in the private subnet through the internet without proper routing to the subnets.

2. Private: Private NAT Gateways are mostly used for communication between VPCs or between VPCs and Transit Gateway. You can't access Elastic IP with the private NAT Gateway.

The main use case of NAT Gateway is to allow you to have Internet access in private subnets of your Virtual Private Cloud. This way your instances still can't be accessed from the Internet but the instances themselves can access the Internet. So you have Internet access without having a risk of being hacked through publicly accessible instances.

## Benefits Of AWS NAT Gateway
1. Improved security: NAT Gateways enable instances in private subnets to access the Internet while preventing Internet-based access to those instances. This helps to improve security by reducing the attack surface of your VPC.
2. Simplified network architecture: NAT Gateways allow you to simplify your network architecture by eliminating the need for a bastion host or VPN connection to access instances in private subnets.
3. Automatic scaling: NAT Gateways are automatically scaled based on your usage, so you don't have to worry about managing the service yourself.
4. High availability: NAT Gateways are designed for high availability, with multiple redundant gateways in each Availability Zone to ensure that traffic continues to flow even if one gateway goes offline.
5. Cost-effective: NAT Gateways are cost-effective, with pay-as-you-go pricing and no upfront costs. They also offer a lower-cost alternative to using (Vitual Private Network) VPN connection or a bastion host to access private instances.

[set up NAT Gateway guide](https://medium.com/@thelovearinze/how-to-set-up-a-nat-gateway-in-aws-step-by-step-for-beginners-dd0da5e1ea4e)

____________________________________________________________________________
## Internet Gateway

An internet gateway is a crucial component in a Virtual Private Cloud (VPC) that enables communication between your VPC and the internet. It is a horizontally scaled, redundant, and highly available VPC component that supports both IPv4 and IPv6 traffic. The internet gateway does not introduce availability risks or bandwidth constraints on your network traffic.

Functionality and Use Cases

An internet gateway allows resources in your public subnets, such as EC2 instances, to connect to the internet if they have a public IPv4 address or an IPv6 address. Similarly, resources on the internet can initiate a connection to resources in your subnet using the public IPv4 address or IPv6 address. For example, an internet gateway enables you to connect to an EC2 instance in AWS using your local computer.

The internet gateway provides a target in your VPC route tables for internet-routable traffic. For communication using IPv4, the internet gateway also performs network address translation (NAT). This is essential for enabling bidirectional communication between instances in a VPC and the internet.

[Internet gateway guide](https://medium.com/@andregustavols4/aws-internet-gateway-what-is-it-and-how-does-it-work-2d4e07f53c99)