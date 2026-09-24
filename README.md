# Windows-11-Security-Baseline-and-Monitoring-Lab
This project develops and evaluates a security baseline for a Windows 11 workstation operating within a controlled cybersecurity laboratory.

1. Project Overview
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

2. Project Objectives
The primary objectives are to:

Establish a practical security baseline for a Windows 11 workstation.
Identify realistic threats against the workstation.
Select Windows security controls based on those identified threats.
Reduce the risk of unauthorized access.
Protect the confidentiality and integrity of information stored or processed on the workstation.
Reduce risks associated with weak authentication and inappropriate access permissions.
Configure appropriate Windows security controls to reduce the impact of common threats.
Deploy security monitoring using Wazuh.
Verify that relevant Windows security events can be collected and forwarded.
Test whether implemented security controls operate as intended.
Evaluate the effectiveness and limitations of the security baseline.
Maintain reasonable usability so that security controls remain practical and do not encourage users to bypass them.

3. Security Objectives
The security objectives of the project are to:

Reduce the risk of unauthorized access to the Windows 11 workstation.
Protect the confidentiality and integrity of information stored or processed on the system.
Reduce the risk associated with weak authentication and inappropriate access permissions.
Configure appropriate Windows security controls to mitigate common threats.
Enable relevant security events to be monitored through the Wazuh agent and Wazuh infrastructure.
Verify that selected security controls are correctly configured and operating as intended.
Evaluate the effectiveness and limitations of the baseline through controlled security testing.
Maintain reasonable usability while improving the security posture of the workstation.
 

4. System Being Protected
The primary system being protected is a Windows 11 workstation operating within a controlled cybersecurity laboratory.
The workstation runs a Wazuh agent intended to forward relevant security events to a Wazuh stack hosted on an Ubuntu 24 virtual machine.
The laboratory environment allows security controls and monitoring functionality to be tested without targeting external systems.

 
5. Laboratory Architecture
The initial architecture consists of two principal virtual machines.
Windows 11
The Windows 11 VM acts as the monitored endpoint.

Responsibilities include:
Operating system security controls
User and authentication security
File and system protection
Security event generation
Wazuh agent operation
Forwarding security telemetry to the Wazuh manager

Ubuntu 24
The Ubuntu VM hosts the Wazuh monitoring infrastructure.
Responsibilities include:

Wazuh manager
Wazuh indexer
Wazuh dashboard
Receiving endpoint telemetry
Processing security events
Providing monitoring and analysis capabilities

VirtualBox networking provides connectivity between the two systems.
 

6. Assets
The principal assets requiring protection include:

User accounts and authentication
User accounts and authentication mechanisms are protected against unauthorized access and credential compromise.
Credentials
Credentials represent a high-value asset because compromised credentials may allow unauthorized access to the workstation or other resources.
Files and data
Files and information stored or processed on the Windows workstation must be protected against unauthorized modification, deletion or disclosure.
Windows operating system integrity
The integrity of the operating system is important because modification of system components or security configuration could undermine other security controls.
Security logs and event information
Security logs provide evidence of activity and are therefore important for both detection and investigation.
Wazuh agent and collected telemetry
The Wazuh agent and the data it collects are important monitoring components. If monitoring is disabled or compromised, security visibility may be reduced.
Availability
The availability and reliability of the Windows workstation and monitoring infrastructure are also considered because security controls are less useful if the underlying systems cannot operate reliably.

7. Threat Model

The threat model identifies realistic threats against the Windows workstation so that security controls can be selected based on the threats they are intended to mitigate rather than simply applying a generic collection of security settings.

7.1 Potential Attackers
The model considers several attacker types.
External attacker
An attacker attempting to obtain unauthorized access to the workstation or its resources.
Malicious or compromised user
A user with legitimate access who attempts to abuse privileges or access information beyond their intended authorization.
Malware
Malicious software executing on the workstation and attempting to compromise the operating system, files, credentials or security controls.
Credential attacker
An attacker attempting to obtain, guess, reuse or otherwise compromise user credentials.
Security-control bypass attacker
An attacker attempting to disable, evade or bypass security controls and monitoring mechanisms.
The project does not assume that every attacker has unrestricted access to the system. Attacker capabilities depend on the specific threat being evaluated.
 

8. Threats Considered
The baseline considers threats including:

Unauthorized account access
Password guessing
Credential compromise
Excessive or inappropriate user privileges
Unauthorized modification of files
Unauthorized modification of system configuration
Malicious software execution
Attempts to evade or disable security monitoring
Loss or manipulation of security event information
Unnecessary network exposure
Insecure Windows functionality
Failure of security monitoring infrastructure

 9. Security Assumptions
The project makes the following assumptions:

The Windows 11 system is under the control of the project owner.
Security testing is performed only within the controlled laboratory environment.
The Ubuntu 24 virtual machine and Wazuh infrastructure are trusted components of the laboratory.
The attacker does not initially have unrestricted administrative control of the Windows workstation.
Physical security of the host computer is outside the primary scope of this project.
Testing is performed against systems owned or controlled by the project owner.

10. Security Controls
Security controls will be selected according to the threats identified in the threat model.

Areas considered include:
Authentication configuration
Account security
Password policy
User privileges
Windows Defender and malware protection
Firewall configuration
Unnecessary service and network exposure
File and system permissions
Security logging
Event monitoring
Wazuh endpoint monitoring
Monitoring infrastructure integrity

The purpose of these controls is not simply to make the system more restrictive, but to provide measurable risk reduction while maintaining reasonable usability.
 

11. Wazuh Monitoring Architecture
A major component of the project is the implementation of endpoint monitoring using Wazuh.
The intended telemetry path is:

Windows security event → Wazuh agent → Wazuh manager → Wazuh analysis/indexing → Wazuh dashboard/alert
The ultimate objective is to generate a controlled security event on Windows and demonstrate that the event can be observed through the Wazuh infrastructure.
This will provide evidence that the monitoring component of the security baseline is functioning.

12. Wazuh Agent Investigation
The Windows Wazuh agent is being configured as agent 001.
An existing agent identity, 003, has been retained and its previous client key has been backed up. Neither agent 001 nor agent 003 is being deleted during the investigation.
The Windows agent is configured to communicate with the Ubuntu Wazuh manager using:
Manager address: 192.***.**.***
Protocol: TCP
Agent communication port: 1514
The investigation deliberately avoids making multiple unrelated configuration changes at the same time. This allows individual observations to be associated with specific tests.
 
13. Connectivity Testing
Connectivity between the Windows workstation and Ubuntu manager was tested before continuing with the Wazuh handshake investigation.
The Windows workstation successfully established TCP connectivity to the Wazuh manager on port 1514.

This demonstrated that:
The Windows workstation can reach the Ubuntu VM.
The manager IP address is reachable.
TCP port 1514 is accessible from Windows.
The basic network path is functioning.

On the Ubuntu side, the Wazuh manager was also confirmed to be listening on TCP port 1514.
The wazuh-remoted process was confirmed to be running.
These tests significantly narrow the troubleshooting scope because they make a basic network connectivity failure less likely.
 

14. Wazuh Service Investigation
During the investigation, the Windows Wazuh agent service was initially found to be stopped.
The service was subsequently started/restarted and its state was checked.
The Windows agent log then showed activity indicating that the agent process was starting and attempting to operate.
The Windows log also reported:
invalid IP address 11
This message is being investigated rather than immediately interpreted as evidence that the manager address is incorrect.
The configured manager address was separately verified as:
192.***.**.***
and connectivity to that address on TCP 1514 was successful.
 
15. Ubuntu Manager Investigation
The Ubuntu Wazuh manager was confirmed to be:

Enabled
Active
Listening on TCP 1514
The wazuh-remoted process was also confirmed to be running.
However, the Ubuntu environment produced repeated messages involving:
connection refused / error 111
More importantly, querying agent 001 using the Wazuh agent_control utility produced a cannot connect to queue type error.
This provided a significant new troubleshooting direction.
Rather than continuing to modify Windows networking or authentication configuration, the investigation is now examining the internal Wazuh manager queue/socket infrastructure.

 16. Troubleshooting Methodology
The troubleshooting process follows a layered approach.
The investigation began with the basic system state:

Is the Wazuh manager running?
Is the Windows agent running?
Does Windows have the correct manager address?
Can Windows reach the manager?
Is TCP 1514 accessible?
Is the Wazuh manager actually listening?
Is wazuh-remoted running?
Can Wazuh’s own management tools communicate with its internal queues?
Only after those checks will the agent authentication handshake be evaluated in detail.
This approach prevents multiple configuration changes from obscuring the cause of a failure.


17. Current Findings
At the current stage, the following has been established:

See Picture

This means the project has not yet reached successful end-to-end telemetry, and this is explicitly recorded as an outstanding objective rather than being presented as completed.

18. Outstanding Investigation
The next investigation step is to inspect the Wazuh manager’s internal queue sockets.
The next command identified for the investigation is:

sudo ls -la /var/ossec/queue/sockets/

The purpose of this check is to determine whether the expected Wazuh queue/socket endpoints exist and whether their state provides an explanation for the agent control queue connection failure.
Following that investigation, the project will return to the Windows agent handshake and determine whether agent 001 can successfully authenticate and become active.
 

19. Planned End-to-End Security Test
Once agent 001 successfully connects, the original monitoring objective will be completed.
The planned workflow is:

Controlled Windows security event
↓
Windows event/log generation
↓
Wazuh agent collection
↓
Wazuh manager reception
↓
Wazuh analysis
↓
Alert/telemetry
↓
Wazuh dashboard or event evidence

The resulting evidence will demonstrate whether the monitoring architecture can provide useful security telemetry from the Windows endpoint.


20. Security Testing
After the monitoring pipeline is operational, controlled security tests will be performed against the Windows workstation.
Testing will be designed to answer specific questions such as:

Does the relevant Windows security control activate?
Is the event logged?
Does the Wazuh agent collect the event?
Does the Wazuh manager receive it?
Is the event correctly represented in Wazuh?
Can the resulting telemetry support investigation?
Are there gaps between the security control and monitoring system?
Testing will remain within the controlled laboratory environment.
  
22. Evaluation Criteria
The security baseline will be evaluated using several criteria.
Configuration
Is the control configured correctly?
Operation
Does the control actually function as intended?
Detection
Can relevant activity be detected?
Visibility
Does Wazuh provide useful evidence of the event?
Effectiveness
Does the control meaningfully reduce the relevant risk?
Limitations
What threats remain despite the control?
Usability
Does the control remain practical for normal operation?
 
23. Limitations
The project recognises that a security baseline cannot eliminate all security risk.
Potential limitations include:

Security controls may reduce but not eliminate attack risk.
Monitoring depends on the availability and integrity of the monitoring infrastructure.
An attacker with sufficient privileges may attempt to disable or evade monitoring.
Security logs may not capture every relevant action.
Wazuh telemetry depends on correct agent and manager operation.
Virtualised laboratory conditions do not perfectly represent a production enterprise environment.
Physical security is outside the primary scope.
The current Wazuh telemetry pipeline remains under development.

These limitations will be considered when interpreting the results.
 
23. Findings
The findings section will be updated as testing progresses.
Current findings include:

The Windows workstation and Ubuntu Wazuh manager can communicate over the required network path.
TCP 1514 connectivity has been successfully demonstrated.
The Wazuh manager is listening on the required agent communication port.
wazuh-remoted is running.
The Windows agent is able to start and attempt communication.
The Wazuh manager currently reports an internal queue connection problem during agent_control interaction.
Agent 001 has not yet been demonstrated as fully active.
End-to-end Windows-to-Wazuh telemetry has therefore not yet been demonstrated.

Further findings will be added as the queue investigation and agent handshake investigation continue.

 
24. Reflection
This project is also intended to demonstrate the development of practical security-engineering skills.

The troubleshooting process has demonstrated the importance of:
Breaking complex problems into smaller components.
Testing assumptions rather than relying on them.
Understanding TCP/IP connectivity.
Working with Windows services.
Working with Linux services and processes.
Reading security logs.
Understanding Wazuh architecture.
Distinguishing network failures from application-level failures.
Investigating authentication and communication problems.
Making controlled changes rather than changing multiple variables simultaneously.
Documenting unsuccessful tests as well as successful ones.
An unsuccessful test is still valuable when it provides evidence that narrows the possible causes of a problem.
The Wazuh integration is therefore being treated not simply as a configuration exercise, but as an engineering investigation.
 
25. Project Status
Status: In progress

The Windows security baseline and Wazuh monitoring environment have been established sufficiently to begin structured testing and troubleshooting.
Basic network connectivity has been demonstrated, and the Wazuh manager’s agent communication service has been confirmed to be operational.
The remaining technical work is to resolve the Wazuh manager’s internal queue issue, complete the agent 001 authentication/handshake process, and demonstrate the complete telemetry path from a controlled Windows security event through to Wazuh detection and alerting.

Once completed, the project will contain evidence of both security control implementation and security monitoring effectiveness.

 
26. Final Project Goal
The final goal is to demonstrate a complete security-engineering workflow:
Threat model → security baseline → implementation → monitoring → controlled testing → telemetry → analysis → findings → limitations → reflection

Rather than simply demonstrating that a security tool was installed, the project aims to demonstrate an understanding of why controls were selected, what risks they address, how their effectiveness can be tested, and how monitoring can provide evidence of security-relevant activity.

 

