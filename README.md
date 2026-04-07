## Lab 2 — VPC Setup: Subnets and IP Allocation

Built an Amazon VPC for a customer scenario requiring 15,000+ 
private IP addresses and a public subnet with 50+ IPs.

**Solution:**
- VPC CIDR: 192.168.0.0/18 (16,384 addresses — RFC 1918 private range)
- Public Subnet CIDR: 192.168.1.0/26 (64 addresses)
- Attached internet gateway for public subnet connectivity

**Concepts covered:** CIDR notation, subnet sizing, 
public vs private subnets, RFC 1918 private ranges, 
VPC architecture design

**Environment:** AWS Management Console
