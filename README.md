# Windows--11--Security-Baseline-and-Monitoring-Lab
This project develops and evaluates a security baseline for a Windows 11 workstation operating within a controlled cybersecurity laboratory.
. Project Overview
This project develops and evaluates a security baseline for a Windows 11 workstation operating within a controlled cybersecurity laboratory.
The project combines Windows security hardening, threat modelling, network connectivity testing, security monitoring, and controlled security testing. The objective is not simply to apply a collection of security settings, but to understand which risks those controls address, verify that the controls operate as intended, and identify their limitations.
A Windows 11 workstation is used as the primary system under assessment. A Wazuh agent installed on the Windows workstation is intended to forward relevant security telemetry to a Wazuh infrastructure hosted on an Ubuntu 24 virtual machine.
The monitoring environment consists of:
* Windows 11 workstation
* Wazuh agent
* Ubuntu 24 Wazuh manager
* Wazuh indexer
* Wazuh dashboard
* VirtualBox networking
The project is being developed incrementally, with configuration, connectivity, monitoring and troubleshooting documented as part of the engineering process.
 
