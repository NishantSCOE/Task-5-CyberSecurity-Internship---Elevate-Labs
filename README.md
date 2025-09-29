# Elevate Labs Internship - Task 5: Wireshark Traffic Analysis

This repository contains the deliverables for Task 5 of the Elevate Labs Cybersecurity Internship. The task involved capturing and analyzing network traffic using Wireshark.

### **Objective**
The primary goal was to capture live network packets and identify basic protocols and traffic types to gain hands-on packet analysis skills.

### **Files in this Repository**
* `Task_5_Traffic_Capture.pcapng`: The raw packet capture file generated during the task. It can be opened and analyzed using Wireshark.
* `report.md`: A detailed report summarizing the methodology, analysis, and findings from the packet capture.
* `/screenshots`: A directory containing screenshots of the Wireshark analysis and the file transfer process.

### **Process Overview**
1.  Network traffic was captured on a Kali Linux VM using Wireshark.
2.  The raw capture was saved to a `.pcapng` file.
3.  The capture file was transferred to the Windows host machine using a simple Python web server for submission.
4.  The capture was analyzed by filtering for specific protocols.

### **Protocols Identified**
The following four protocols were successfully identified and analyzed in the capture:
* **DNS:** Observed name resolution queries and responses.
* **TCP:** Identified the three-way handshake and TLS-encrypted sessions.
* **HTTP:** Found `GET` requests for web content and server status responses.
* **ICMP:** Captured "Destination unreachable" error messages.

---
*This task was completed as part of the Elevate Labs Cybersecurity Internship program.*
