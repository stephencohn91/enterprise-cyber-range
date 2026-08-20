\# Network Access Policy



\## Purpose

This document defines the intended network access-control policy for the Enterprise Cyber Range.

The simulated environment represents a small electronics sales and repair business with trusted internal systems, public-facing services, guest wireless access, and an untrusted repair-quarantine network used for customer-owned devices.

The goal is to enforce least-privilege communication between network segments while preserving legitimate business functionality.



\------------------------



\## Network Segments



| VLAN | Name | Subnet | Purpose |

| --- | --- | --- |

| 10 | Management | 10.10.10.0/24 | Management and admin systems |

| 20 | Store/POS | 10.10.20.0/24 | Retail and point-of-sale systems |

| 30 | Repair Technician | 10.10.30.0/24 | Trusted technician workstations |

| 40 | Repair Quarantine | 10.10.40.0/24 | untrusted customer-owned devices |

| 50 | Servers | 10.10.50.0/24 | Internal business services |

| 55 | Database Servers | 10.10.55.0/24 | Protected backend database services |

| 60 | Security | 10.10.60.0/24 | Security monitoring and management systems |

| 70 | Guest Wi-Fi | 10.10.70.0/24 | Customer and visitor wireless access |

| 80 | DMZ | 10.10.80.0/24 | Public-facing services |



\------------------------



\## Trusted Model



\### Highly Trusted

* VLAN 10 - Management
* VLAN 60 - Security



\### Trusted

* VLAN 20 - Store/POS
* VLAN 30 - Repair Services
* VLAN 50 - Servers
* VLAN 55 - Database Servers



\### Untrusted

* VLAN 40 - Repair Quarantine
* VLAN 70 - Guest Wi-Fi



\------------------------



\## Access-Control Matrix



| Source | Management | POS | Repair Tech | Quarantine | Servers | Security | Guest | DMZ | Internet |

|---|---|---|---|---|---|---|---|---|---|

| Management | Allow | Allow | Allow | Deny | Allow | Allow | Deny | Allow | Allow |

| POS | Deny | Allow | Deny | Deny | Limited | Deny | Deny | Allow | Allow |

| Repair Technicians | Deny | Deny | Allow | Limited | Limited | Deny | Deny | Allow | Allow |

| Repair Quarantine | Deny | Deny | Deny | Allow | Deny | Deny | Deny | Limited | Allow |

| Servers | Limited | Limited | Limited | Deny | Allow | Limited | Deny | Allow | Allow |

| Security | Allow | Allow | Allow | Allow | Allow | Allow | Allow | Allow | Allow |

| Guest Wi-Fi | Deny | Deny | Deny | Deny | Deny | Deny | Allow | Allow | Allow |

| DMZ | Deny | Deny | Deny | Deny | Deny | Limited | Deny | Allow | Allow |



\------------------------



\## Policy Requirements



\### Management Network



The Management network contains privileged administrative systems.



Management systems may access internal business services and security systems as required.



Untrusted networks must not initiate connections to the Management network.



\------------------------



\### Store/POS Network



The Store/POS network contains retail and point-of-sale systems.



POS systems should only communicate with the business services necessary for store operations.



POS systems should not have direct access to:



\- Management systems

\- Technician systems

\- Customer repair devices

\- Security-monitoring infrastructure

\- Internal database systems unless explicitly required



Where possible, POS systems should access business data through an application service rather than directly connecting to database systems.



\------------------------



\### Repair Technician Network



The Repair Technician network contains trusted technician workstations.



Technician systems may require access to:



\- Repair-ticket systems

\- Inventory systems

\- Approved internal application services

\- Internet resources used for troubleshooting, documentation, drivers, and updates



Technicians should not have unrestricted access to:



\- Management systems

\- POS systems

\- Security-monitoring systems

\- Internal databases



Access to customer-owned devices should be limited to services required for repair and diagnostics.



\------------------------



\### Repair Quarantine Network



The Repair Quarantine network is considered untrusted.



Customer-owned devices may be infected, compromised, misconfigured, or otherwise unsafe.



Devices on this network must not initiate connections to trusted internal business networks.



Allowed communication should be limited to:



\- Local network gateway

\- Internet access

\- Approved repair or diagnostic services when specifically required



This network is expected to generate potentially hostile or suspicious traffic and will be a primary target for security monitoring.



\------------------------



\### Application Server Network



The Application Server network contains internal business application services.



Approved client networks may access application services based on business requirements.



Application servers may communicate with protected backend database services when required.



Ordinary client systems should not directly access database services.



\------------------------



\### Database Server Network



The Database Server network contains protected backend data services.



Direct access from ordinary client networks is prohibited.



Database access should be limited to explicitly authorized application servers and administrative systems.



Separating application and database systems into different network segments allows routing and access-control policies to enforce this boundary.



\------------------------



\### Security Network



The Security network contains security-monitoring, logging, and administrative systems.



Security systems require broad visibility into the environment for monitoring and incident-response purposes.



Access to security systems from ordinary client networks should be restricted.



\------------------------



\### Guest Wi-Fi



Guest Wi-Fi is considered untrusted.



Guest devices may access:



\- Their local gateway

\- Public-facing DMZ services

\- Internet resources



Guest devices must not access trusted internal business networks.



\------------------------



\### DMZ



The DMZ contains public-facing services.



Internet and guest users may access approved public services hosted in the DMZ.



DMZ systems must not have unrestricted access to trusted internal networks.



Any DMZ-to-internal communication must be explicitly justified and restricted to required services.



\------------------------



\## Current Implemented Controls



\### Repair Quarantine Isolation



VLAN 40 is restricted from accessing internal 10.10.0.0/16 business networks.



The quarantine network retains access to its local gateway and is intended to retain Internet access once external routing is completed.



\### Guest Wi-Fi Isolation



VLAN 70 is restricted from accessing trusted internal business networks.



Guest devices retain access to:



\- VLAN 70 gateway

\- Public DMZ services

\- Future Internet connectivity



\### Application and Database Segmentation



Application and database services were originally located within the same server VLAN.



Security validation identified that hosts within the same Layer-2 network could communicate without passing through the router access-control boundary.



The architecture was revised to separate these systems:



\- VLAN 50 - Application Servers

\- VLAN 55 - Database Servers



The database server is now isolated from ordinary POS and technician systems, while authorized application-server communication remains functional.



\------------------------



\## Security Principles



The network design follows these principles:



1\. Default deny between security zones unless communication is required.

2\. Untrusted networks must be isolated from trusted business systems.

3\. Public-facing services should reside in the DMZ.

4\. Database systems should not be directly exposed to ordinary client networks.

5\. Security-monitoring systems should be protected from ordinary user access.

6\. Access should be granted based on business need rather than convenience.

7\. Security controls must be tested before and after implementation.

8\. Any permitted exception should have a documented business justification.



\------------------------



\## Validation Approach



Each security control should be tested using a repeatable process:



1\. Test connectivity before the control is implemented.

2\. Record the insecure baseline.

3\. Implement the security control.

4\. Repeat the same test.

5\. Confirm authorized traffic still works.

6\. Confirm unauthorized traffic is blocked.

7\. Record the result as project evidence.



This process provides measurable before-and-after validation of network-security improvements.



