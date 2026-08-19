# Enterprise Cyber Range

A simulated enterprise cybersecurity environment designed to demonstrate network architecture, security monitoring, controlled attack simulation, incident investigation, defensive hardening, and security validation.

## Project Status

**Current Version:** v0.1 - Initial Planning and Network Architecture

This project is currently under active development.

## Project Overview

The Enterprise Cyber Range models the network and cybersecurity requirements of a small electronics sales and repair business.

The simulated business provides:

- Electronics and computer repair
- Component-level electronics repair
- PC building and upgrades
- Software troubleshooting
- Electronics and computer retail
- Networking equipment and accessories

A key security challenge is the regular introduction of untrusted customer-owned devices into the repair environment.

The project will use Cisco Packet Tracer to design and document the enterprise network architecture and a containerized environment to implement representative business systems and security controls.

## Project Goals

- Design a segmented enterprise network
- Implement representative business services using containers
- Separate untrusted customer devices from business systems
- Establish centralized security monitoring and logging
- Generate normal network activity and establish a baseline
- Conduct controlled attack simulations
- Investigate attacks using collected telemetry
- Implement defensive improvements
- Repeat attacks to validate security controls
- Compare security results before and after hardening

## Planned Network Segments

| VLAN | Network | Subnet | Purpose |
|------|---------|--------|---------|
| 10 | Management/Admin | 10.10.10.0/24 | Management and administrative systems |
| 20 | Store/POS | 10.10.20.0/24 | Retail and point-of-sale systems |
| 30 | Repair Technicians | 10.10.30.0/24 | Trusted technician workstations |
| 40 | Repair Quarantine | 10.10.40.0/24 | Untrusted customer devices |
| 50 | Servers | 10.10.50.0/24 | Internal business services |
| 60 | Security/Management | 10.10.60.0/24 | Security monitoring and network management |
| 70 | Guest Wi-Fi | 10.10.70.0/24 | Customer Internet access |
| 80 | DMZ | 10.10.80.0/24 | Public-facing services |

## Planned Technologies

- Cisco Packet Tracer
- Docker
- Git/GitHub
- Wireshark
- Linux
- Network security monitoring and logging tools

Additional technologies will be selected as the project develops.

## Development Roadmap

1. Business and security requirements
2. Network architecture
3. Packet Tracer implementation
4. Containerized cyber range
5. Business services
6. Security monitoring and logging
7. Normal traffic baseline
8. Controlled attack scenarios
9. Incident investigation
10. Security hardening
11. Attack retesting and validation
12. Documentation and portfolio release

## Disclaimer

All attacks and security testing performed as part of this project will be conducted exclusively within an isolated lab environment using simulated systems and fictional data.