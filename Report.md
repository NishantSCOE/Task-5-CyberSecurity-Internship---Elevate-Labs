# Task 5: Network Traffic Analysis using Wireshark

### **Objective**
The objective of this task was to capture live network packets using Wireshark, analyze the traffic to identify different protocols, and report on the findings.

### **Tools Used**
* **Wireshark:** For packet capture and analysis.
* **Kali Linux (in VirtualBox):** The operating environment for running Wireshark.
* **Python 3:** To create a simple HTTP server for file transfer.
* **Windows 11:** The host operating system.

### **Methodology**
The process involved capturing network traffic, transferring the capture file from the virtual machine to the host machine, and analyzing the results.

#### **1. Packet Capture**
1.  Wireshark was started on a Kali Linux virtual machine.
2.  The active network interface (`eth0`) was selected for packet capturing.
3.  To generate diverse traffic, I browsed several websites and used the `ping` command in the terminal.
4.  After approximately two minutes, the capture was stopped.
5.  The captured data was saved as `Task_5_Traffic_Capture.pcapng`.

#### **2. File Transfer Method (Kali VM to Windows Host)**
To move the `.pcapng` file from the Kali VM to the Windows host for submission, a simple Python web server was used:
1.  The UFW (Uncomplicated Firewall) on Kali was temporarily disabled using `sudo ufw disable` to ensure the connection from the host was not blocked.
2.  The IP address of the Kali VM was identified using the `ip addr` command.
3.  A web server was started in the directory containing the capture file with the command: `python3 -m http.server 8080`.
4.  On the Windows host machine, a web browser was used to navigate to the Kali VM's IP address on port 8080.
5.  The `Task_5_Traffic_Capture.pcapng` file was downloaded directly from the browser.

### **Analysis and Findings**
The captured packets were analyzed by applying display filters in Wireshark to isolate and inspect specific protocols. The following protocols were identified and analyzed:

#### **A. DNS (Domain Name System)**
DNS traffic was clearly visible, responsible for translating human-readable domain names into IP addresses.
* **Observations:** The capture shows the local machine (`192.168.43.85`) sending "Standard query" packets to the local DNS server (`192.168.43.115`).
* **Example:** Queries were made for domains like `play.google.com`, `httpforever.com`, and `cdnjs.cloudflare.com`. The server responded with the corresponding IP addresses.

#### **B. TCP (Transmission Control Protocol)**
TCP is a connection-oriented protocol that ensures reliable data delivery.
* **Observations:** The classic **TCP three-way handshake** was observed. Packets with `[SYN]`, `[SYN, ACK]`, and `[ACK]` flags were captured, showing the establishment of a connection between the local machine and a remote server (`74.125.24.84`, a Google server).
* **Encrypted Traffic:** Many packets were also identified as **TLSv1.2** and **TLSv1.3**, which is the encrypted session (HTTPS) running on top of the TCP connection.

#### **C. HTTP (Hypertext Transfer Protocol)**
HTTP is the protocol used for transmitting web page data.
* **Observations:** Standard `GET` requests from the local machine to web servers were captured. These requests were for web assets like stylesheets (`.css`), JavaScript files (`.js`), and images (`favicon.ico`).
* **Server Responses:** The servers responded with status codes like `HTTP/1.1 200 OK` (indicating a successful request) and `HTTP/1.1 301 Moved Permanently`.

#### **D. ICMP (Internet Control Message Protocol)**
ICMP is used by network devices to send error messages and operational information.
* **Observations:** The capture did not contain the typical `ping` (echo request/reply) packets. Instead, it showed "Destination unreachable (Port unreachable)" messages.
* **Meaning:** This indicates that a device (likely the local router at `192.168.43.115`) sent a message back to our machine (`192.168.43.85`) to inform it that it tried to connect to a service on a port that was closed.

### **Conclusion**
This task provided valuable hands-on experience with Wireshark. I successfully captured and analyzed live network traffic, identifying and understanding the roles of fundamental protocols like DNS, TCP, HTTP, and ICMP. The process also reinforced practical skills in transferring files between a VM and a host machine.