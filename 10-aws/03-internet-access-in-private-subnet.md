### How to enable internet access to application deployed in private subnet
Applications deployed in a private subnet are isolated from direct internet traffic for security reasons. To enable outbound internet access while maintaining privacy from inbound traffic, you typically need to use Network Address Translation (NAT). 

## AWS (EC2  in a Private Subnet)

# Key Components
Private Subnet: Contains resources without public IP addresses. No direct internet access.
Public Subnet: Contains a NAT Gateway or NAT Instance and an Internet Gateway (IGW) for internet connectivity.
Route Table: Configures routes from private subnet through the NAT Gateway.

## Steps to Enable Internet Access

1.Create a NAT Gateway in a public subnet
2.Allocate an Elastic IP.
3.Attach the NAT Gateway to the public subnet.
4.Update Private Subnet Route Table
Route all outbound traffic (0.0.0.0/0) to the NAT Gateway.
Ensures instances in the private subnet can send traffic to the internet.
5.Security Groups and NACLs
Outbound rules: Allow access to required ports (typically HTTP 80, HTTPS 443).
Inbound rules: Usually not needed unless returning traffic must be allowed.
Ensure Network ACLs allow ephemeral ports (1024–65535) for NAT response traffic.
6.Test Connectivity
SSH into the private instance (via a bastion host if necessary).
Verify access: curl http://example.com or package update commands.

