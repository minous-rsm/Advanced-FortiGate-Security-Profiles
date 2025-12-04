# Cources Center Network ( HQ + 1BR ) 
## Project Overview :Secure Multi-Site Enterprise Network with Fortinet Security Fabric:

## Cources Center Network:
Secure Enterprise Network with Fortinet Security Fabric – HQ + Branch Office Deployment.

## Business Objectives
* Provide secure, highly available network services for HQ and Branch users
+ Centralize authentication on a single Windows Server (Active Directory)
* Deliver full remote worker support via IPsec-VPN
* Securely connect HQ and Branch with IPsec site-to-site VPN
* Implement Zero-Trust segmentation using Fortinet Security Fabric



## Core Components & Architecture:

### High-Availability FortiGate Cluster (HQ)
*  2 × FortiGate firewalls in Active/Passive HA cluster
*  All interfaces and policies synchronized
*  Single virtual IP for all zones used by clients and routers

### FortiGate (Branch)
* Single FortiGate for cost optimization (can be upgraded to HA later)
* Site-to-site IPsec VPN tunnel to HQ HA cluster

### Fortinet Security Fabric
* Root FortiGate = HQ HA cluster
* Windows Server authorized and added into Security Fabric
* Fabric telemetry, FortiClient EMS integration, and automatic quarantine possible

### Windows Server 2016 (HQ – placed in DMZ)
 Roles installed:
* Active Directory Domain Controller
* LDAP server (used for FortiGate user authentication – SSL-VPN & administrative logins).

 Machine is joined to Security Fabric for visibility and automatic IOC sharing

### Remote Access
* FortiGate IPsec-VPN (GlobalProtect-style portal & tunnel mode)
* Authentication against Active Directory via LDAP
* Full-tunnel options configured per group

### Site-to-Site Connectivity
* Permanent IPsec VPN tunnel between HQ HA cluster and Branch FortiGate
* Full reachability for all VLANs in both directions
* Encrypted traffic with DES (the only available method for our version)

### Inter-VLAN Routing
* HQ & BR: Router-on-a-Stick on the HQ FortiGate cluster
* Sub-interfaces for VLAN 10, 20, 30, on the internal port 

### DHCP Strategy
*HQ: DHCP scopes served directly from Relay (ip-helper) from the main router (HQ-R1)
*Branch: DHCP Relay (ip-helper) configured on the main router (BR1-R10) as HQ.


### Security Profiles (Applied on all FortiGates)
* Deep packet inspection (Application Control, IPS, AntiVirus, Web Filter)
* SSL/SSH inspection enabled
* All policies logged to FortiAnalyzer (or FortiGate Cloud)
  
## Key Benefits
* Single Active Directory for authentication everywhere (VPN, Wi-Fi, admins)
* Full high availability at headquarters
* Centralized logging, policy, and visibility via Security Fabric
* Consistent security policy enforcement at both sites
* Easy future scaling (add more branches or upgrade Branch to HA)

## Challenges:
* We don’t have enough resources to expand our project 
* We don’t have FortiGuard licence
* We couldn’t test the security profiles because of licence 
* Don’t have FrtiAnaluzer to put in security fabric for the logs
