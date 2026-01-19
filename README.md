# Siem Home Lab

## Objective
Built a home SIEM lab to evaluate host-based detection capabilities using Wazuh. The environment simulated real-world attacker activity from a Kali Linux system targeting an Ubuntu endpoint. The goal was to assess telemetry visibility, alert fidelity, and detection gaps rather than achieve perfect alerting.

### Skills Learned
- Deployment & Enrollment: You learned how to deploy a complex SIEM (Wazuh) and enroll endpoints using agents. This demonstrates I can manage the "plumbing" of a security stack.
- Rule Tuning & Noise Reduction: One of the most valued skills in a SOC is the ability to "silence the noise." By identifying and suppressing Rule 510, you demonstrated that you can prevent alert fatigue and focus on high-fidelity threats.
- Custom Rule Creation: You learned how to write and modify XML rules to escalate security levels based on frequency and timeframe— essential for catching sophisticated brute-force attacks.
- Tool Proficiency: I gained hands-on experience with Hydra and Nmap, the industry standards for password cracking and network discovery.
- Attack Patterns: I didn't just run a command; you learned what those attacks look like "on the wire" and in the logs. This "Attacker Mindset" helps me become a better defender.
- Mapping to MITRE ATT&CK: I learned to categorize alerts using a professional framework.
- Log Correlation: I practiced "connecting the dots" between a source IP in Kali and a failed login event on Ubuntu. This is the core of incident investigation.
- Virtual Networking: I successfully managed communication between three different VMs (Kali, Ubuntu, and Wazuh OVA), which requires an understanding of IP addressing, subnets, and host-only networking.


### Tools Used
- Wazuh (SIEM/XDR): Centralized log management, correlation, and intrusion detection.
- Wazuh Agent: Installed on the endpoint to monitor system logs (auth.log), file integrity, and running processes.
- Kali Linux: The primary offensive platform used for adversary emulation.
- Hydra: High-speed network logon cracker used to simulate SSH brute-force attacks.
- Nmap (Network Mapper): Used for network discovery and security auditing to trigger "multiple connection" alerts.
- Oracle VirtualBox: Hosted the virtualized lab environment.
- Ubuntu Server 24.04: Acted as the victim/target endpoint.
- Linux CLI / Bash Scripting: Used for automated log generation, rule configuration, and system administration.
  


## Steps


Reference: SIEM 1


<img width="642" height="486" alt="Ubuntu_check" src="https://github.com/user-attachments/assets/1574ad30-3ef6-40b7-aff5-339be70ddb97" />




In this phase of the project, I validated the Ubuntu victim endpoint’s network identity using the ip a command. This confirmed the assigned IP address and network configuration, ensuring reliable connectivity within the isolated lab environment for log forwarding to the Wazuh Manager. Verifying endpoint identity was essential to accurately attribute generated telemetry to the targeted host during the simulated attack and monitoring phases.


Reference: SIEM 2




<img width="341" height="143" alt="ping" src="https://github.com/user-attachments/assets/50e0552d-6493-458b-8c36-44f4259f441d" />




Performed baseline network reconnaissance from the Kali attacker by validating connectivity to the Ubuntu victim via targeted ping. This confirmed the lab was prepared for subsequent simulated attacks, including Hydra brute-forcing and Nmap scanning, monitored through the Wazuh SIEM.





Reference: SIEM 3




<img width="358" height="402" alt="Nmapscan" src="https://github.com/user-attachments/assets/42b6531b-be32-43d5-8657-4de85364c1c9" />




I conducted an aggressive network scan from the Kali Linux attacker host using Nmap to enumerate the Ubuntu victim’s attack surface. By executing the nmap -A -T4 command, I performed OS detection, service versioning, and traceroute analysis to simulate active reconnaissance behavior. This activity was intentionally designed to generate a high volume of connection attempts, allowing me to evaluate whether the Wazuh SIEM could detect and alert on scanning behavior and distinguish it from normal network traffic.



Reference: SIEM 4


<img width="331" height="71" alt="Hydra" src="https://github.com/user-attachments/assets/9c7fa96b-13f8-464f-bb1d-afe46fd1010b" />


Simulated an SSH brute-force attack using Hydra to generate high-frequency authentication attempts, validating Wazuh’s ability to detect and alert on credential-stuffing behavior.



Reference: SIEM 5


<img width="1572" height="720" alt="Screenshot 2026-01-18 190811" src="https://github.com/user-attachments/assets/b665903d-a371-4014-adc0-02a6dadfbad0" />


I designed a SOC-focused home lab using Wazuh SIEM to evaluate detection coverage for credential-based attacks. An Ubuntu 24.04 endpoint was instrumented with a Wazuh agent to collect authentication and system logs in real time. A simulated SSH brute-force attack generated high-volume authentication failures, which Wazuh correlated into a Level 10 (High Severity) alert and mapped to MITRE ATT&CK T1110. The resulting dashboard illustrates how raw telemetry is enriched, correlated, and presented as actionable intelligence for SOC analysis.



Reference: SIEM 6


<img width="1566" height="729" alt="Screenshot 2026-01-18 192321" src="https://github.com/user-attachments/assets/07a03d97-e310-4786-a2eb-6b544508ffb5" />


Wazuh SIEM detecting host-level anomalies (Rule 510) and AppArmor policy enforcements (Rule 52002) via Rootcheck and kernel auditing.

Reference: SIEM 7


<img width="1101" height="666" alt="Screenshot 2026-01-18 192745" src="https://github.com/user-attachments/assets/5075cb64-2798-449d-9e42-9ec32f0da12a" />

Configured Wazuh for host-level anomaly detection and kernel policy enforcement on an Ubuntu endpoint. Analysis of Rootcheck (Rule 510) and AppArmor (Rule 52002) events provided visibility into suspicious behaviors and unauthorized process attempts. Activities were mapped to PCI DSS and GDPR standards, illustrating the conversion of raw telemetry into actionable, compliance-aligned security intelligence.

Reference: SIEM 8





<img width="799" height="673" alt="Screenshot 2026-01-18 201553" src="https://github.com/user-attachments/assets/1d9b062a-890e-4e4f-9985-df663eaf728e" />



Wazuh SIEM performing deep-level auditing of an Ubuntu victim endpoint via host-based anomaly detection and kernel-level policy enforcement. Monitoring Rootcheck (Rule 510) and AppArmor (Rule 52002) events provided visibility into suspicious system behavior and unauthorized process attempts. Activities were mapped to PCI DSS (10.6.1, 10.2.6) and GDPR compliance standards, demonstrating the transformation of raw endpoint telemetry into actionable, audit-ready security intelligence.

### Lessons Learned:

- Telemetry gaps matter: Some attack activity did not trigger alerts due to missing or misconfigured audit logs, highlighting the importance of complete endpoint coverage.

- Rule tuning is critical: Default Wazuh rules generated false positives; tuning improved alert fidelity.

- Detection vs. response: Detecting events is only the first step—mapping alerts to MITRE ATT&CK and compliance standards ensures actionable intelligence.

- Simulated attacks are valuable: Controlled Hydra and Nmap simulations allowed safe testing without risking real systems.

- Continuous improvement: Even a well-configured SIEM requires iterative testing, analysis, and updates to maintain effective coverage.
