# AWS Cloud Labs — Simisola Alabi

Hands-on AWS labs completed as part of structured Cloud Practitioner training.
Each lab documents the scenario, solution, and concepts applied.

---

## Lab 1 — Dynamic File Creation with Bash Scripting
**Environment:** Amazon Linux 2 EC2 (SSH via key pair)

Wrote a Bash script that creates 25 empty files per execution with
auto-incrementing names. Each run detects the highest existing file
number and continues from there — no hardcoded values.

**Skills:** Bash scripting, EC2 SSH access, Linux file system, automation logic

---

## Lab 2 — VPC Design: Subnets and IP Allocation
**Environment:** AWS Management Console

**Scenario:** A startup owner needed help building their first VPC with
~15,000 private IP addresses and a public subnet supporting at least 50 IPs.

**Solution:**
| Component | Value | Reasoning |
|---|---|---|
| VPC CIDR | 192.168.0.0/18 | 16,384 addresses — closest /n above 15,000 |
| Subnet CIDR | 192.168.1.0/26 | 64 addresses — closest /n above 50 |
| Address space | 192.168.x.x | RFC 1918 confirmed private range |

**Skills:** CIDR notation, subnet sizing, RFC 1918 private ranges,
VPC architecture, internet gateway configuration

---

## Lab 3 — Troubleshooting VPC Connectivity
**Environment:** AWS Management Console + EC2 terminal

**Scenario:** A customer's EC2 instance in a new VPC could not reach
the internet. Pings to google.com were failing.

**Root cause:** Missing three layers of connectivity — routing,
subnet-level security, and instance-level security.

**Solution — The Three-Layer Fix:**

**Layer 1 — Routing**
- Created an Internet Gateway (IGW) and attached it to the VPC
- Added a default route `0.0.0.0/0 → IGW` to the route table
- Associated the public subnet with the updated route table

**Layer 2 — Network ACL (stateless)**
- Configured NACL Rule 100 to allow all inbound and outbound traffic

**Layer 3 — Security Group (stateful)**
- Allowed inbound SSH (port 22), HTTP (80), and HTTPS (443)

**Verification:** Launched a t3.micro instance with a public IP enabled.
Successfully ran `ping google.com` from the terminal — confirming
end-to-end internet connectivity.

**Skills:** Internet gateways, route tables, NACLs vs security groups
(stateless vs stateful), EC2 networking, connectivity troubleshooting
