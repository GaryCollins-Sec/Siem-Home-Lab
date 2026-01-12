# ML Detection Engineering Lab

## Objective

Engineered an advanced Machine Learning-driven detection pipeline centered on an Isolation Forest anomaly detection model. By leveraging a Dockerized Shuffle SOAR framework on Ubuntu Server, the system autonomously analyzes high-fidelity telemetry from auditd and Suricata. This architecture demonstrates the power of unsupervised learning to detect "living-off-the-land" attacks and zero-day threats that bypass traditional signature-based SIEM rules.


### Skills Learned

- Log Ingestion & Normalization: Configured Rsyslog to stream logs and used Wazuh to normalize diverse data sources (network vs. host) into a unified format.

- Signature-Based Detection: Wrote and tuned Suricata rules for network intrusion detection and created custom Wazuh XML rules to trigger alerts on specific system events.

- Kernel-Level Auditing: Implemented auditd on Linux to capture low-level system calls (execve, connect, open), providing the deep telemetry necessary for behavioral analysis.

- Anomaly Detection: Implemented an Isolation Forest model, an unsupervised learning algorithm ideal for security because it identifies "outliers" (attacks) without needing labeled training data.

- Feature Engineering: Selected and transformed raw security logs into numerical features such as frequency of system calls and unusual port connections that the ML model could process.

- Behavioral Baselining: Taught the model to recognize "normal" Ubuntu server behavior to reduce false positives from routine administrative tasks.

- API Integration: Connected Shuffle SOAR to the Wazuh API to fetch alerts in real-time.

- Automated Response Workflows: Designed logic in Shuffle to automatically pass suspicious logs to the ML model for scoring and execute defensive actions based on the output.

- Containerization: Deployed and managed the SOAR platform using Docker, demonstrating an understanding of microservices architecture.

- Attack Simulation: Used Kali Linux to execute real-world attack vectors, including brute force, privilege escalation, and lateral movement, to validate detection efficacy.

- Virtual Infrastructure: Managed a multi-node lab environment using different OS flavors (Ubuntu, Kali) and specialized appliances (Wazuh OVA).

### Tools Used

- Wazuh (OVA): Served as the central Security Information and Event Management (SIEM) platform for log aggregation, indexing, and alerting.

- Rsyslog: Acted as the high-speed log transport protocol to stream telemetry from endpoints to the Wazuh manager.

- auditd (Linux Audit Daemon): Captured low-level kernel telemetry, including system calls, file integrity changes, and process execution on the victim host.

- Suricata: Deployed as a Network Intrusion Detection System (NIDS) to monitor traffic for known attack signatures and protocol anomalies.

- Shuffle (Docker-based): A Security Orchestration, Automation, and Response (SOAR) platform used to build workflows that ingest Wazuh alerts and trigger response actions.

- Docker: Used to containerize and manage the Shuffle environment, ensuring a portable and scalable automation backend.

- Isolation Forest Model: A Machine Learning algorithm (Unsupervised Learning) implemented to detect "outliers" in system behavior—identifying stealthy attacks that bypass traditional rules.

- Python (Scikit-Learn): Used for the data preprocessing, feature engineering, and deployment of the ML model.

- Ubuntu: The "Victim VM" where auditd and the Wazuh agent were deployed to provide data for analysis.

- Kali Linux: The "Adversary VM" used to simulate real-world attacks like brute-forcing, lateral movement, and data exfiltration.

- Ubuntu Server (Host): Acted as the high-performance backbone for the security stack, configured as a headless orchestration node to manage the SOAR backend and ML processing.
  


## Steps
drag & drop screenshots here or use imgur and reference them using imgsrc

Every screenshot should have some text explaining what the screenshot is about.

Example below.
