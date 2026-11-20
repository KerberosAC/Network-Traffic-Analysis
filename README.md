# Network Traffic Analysis

**Windows Network Defense & Packet Analysis Lab**

![Wireshark](https://img.shields.io/badge/Wireshark-087DAF?style=flat-square&logo=wireshark&logoColor=white) ![Nmap](https://img.shields.io/badge/Nmap-327FB5?style=flat-square) ![PowerShell](https://img.shields.io/badge/PowerShell-478BF5?style=flat-square&logo=powershell&logoColor=white) ![Windows](https://img.shields.io/badge/Windows-0078D4?style=flat-square)

## Objective

Investigate network activity in a Windows lab by identifying active connections and services, configuring firewall controls, and inspecting captured HTTP, TLS, DNS, and ICMP traffic. This repository documents the **complete original lab** with all **21 screenshots** in sequence.

## Skills Learned

- Identifying IP configuration, listening ports, and associated processes.
- Auditing and managing Windows services with PowerShell.
- Creating, modifying, and removing Windows Defender Firewall rules.
- Performing basic network reconnaissance with Nmap.
- Filtering and interpreting network packets in Wireshark.
- Distinguishing between unencrypted HTTP and encrypted TLS traffic.
- Understanding how DNS resolution and ICMP connectivity tests appear in network investigations.

## Tools Used

| Tool | Purpose |
| --- | --- |
| [Wireshark](https://www.wireshark.org/) | Packet capture, display filters, and protocol inspection |
| [Nmap](https://nmap.org/) | Host and service reconnaissance |
| [PowerShell](https://learn.microsoft.com/en-us/powershell/) | Network enumeration, service management, firewall configuration |
| [Windows Defender Firewall](https://learn.microsoft.com/en-us/windows/security/operating-system-security/network-security/windows-firewall/) | Inbound and outbound access-control rules |
| [Windows networking utilities](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands) | `ipconfig`, `netstat`, `tasklist`, and `ping` |

## Lab Walkthrough

### 1. Establish a Network Baseline

![Windows IP configuration](screenshots/01-ip-configuration.png)

*Ref 01 — IP configuration.* Used `ipconfig` to identify the Windows host's IPv4 address, subnet mask, and default gateway. This established which local interface and network to investigate.

### 2. Enumerate Connections and Processes

![Listening ports and process IDs](screenshots/02-listening-ports.png)

*Ref 02 — Active connections.* Ran `netstat -ano` to inspect listening ports, connection states, and process IDs (PIDs). This helps identify potential exposure from locally running services.

![Task list with process IDs](screenshots/03-process-inventory.png)

*Ref 03 — Process inventory.* Used `tasklist` to correlate process names with PIDs, providing context for connections discovered during port enumeration.

### 3. Audit and Manage Windows Services

![Windows service inventory](screenshots/04-service-inventory.png)

*Ref 04 — Service inventory.* Reviewed service names and running/stopped states with `Get-Service` to establish a service-management baseline.

![Service list and Spooler stop](screenshots/05-spooler-stop-command.png)

*Ref 05 — Controlled service change.* Located the Print Spooler service and issued `Stop-Service -Name Spooler` as a demonstration of service administration.

![Spooler stopped status](screenshots/06-spooler-stopped.png)

*Ref 06 — Stopped service.* Inspected service status after the stop command, illustrating how an administrator checks the effect of a change.

![PowerShell service checks](screenshots/07-service-verification.png)

*Ref 07 — Service verification.* Repeated service-management and status queries in PowerShell to verify the controlled change rather than relying only on command execution.

![Spooler startup configuration and restart](screenshots/08-spooler-restart.png)

*Ref 08 — Service restoration.* Configured the Spooler startup type and issued a start command, demonstrating a return to the previous operational state.

![Running service status](screenshots/09-spooler-running.png)

*Ref 09 — Restored status.* Verified that the service was running again, completing the stop–check–restore workflow.

### 4. Configure and Maintain Firewall Rules

![Inbound SMB firewall rule](screenshots/10-block-smb-rule.png)

*Ref 10 — Inbound SMB control.* Created a Windows Defender Firewall rule to block inbound TCP port 445, a commonly exposed SMB service port.

![Outbound IP firewall rule](screenshots/11-outbound-ip-rule.png)

*Ref 11 — Outbound traffic control.* Created an outbound block rule for a specified test IP address, demonstrating host-based egress filtering.

![Modify and remove firewall rules](screenshots/12-firewall-rule-maintenance.png)

*Ref 12 — Rule lifecycle.* Practiced disabling, re-enabling, and removing firewall rules to demonstrate how security controls are maintained and reversed.

### 5. Perform Network Reconnaissance

![Nmap command output](screenshots/13-nmap-reconnaissance.png)

*Ref 13 — Nmap reconnaissance.* Ran an Nmap scan and examined the reported host/service information. Port-scan results provide a point of comparison with the local connection inventory.

### 6. Generate and Inspect Web Traffic

![Web page opened for traffic generation](screenshots/14-web-traffic-generation.png)

*Ref 14 — Browser-generated traffic.* Accessed a website to produce network activity for subsequent packet inspection.

![Wireshark HTTP capture](screenshots/15-http-analysis.png)

*Ref 15 — HTTP analysis.* Applied an HTTP display filter in Wireshark and reviewed requests, responses, and protocol metadata to identify web exchanges.

![Wireshark TLS records](screenshots/16-tls-analysis.png)

*Ref 16 — TLS inspection.* Examined TLS handshake and application-data records. TLS packet metadata remains observable even though the encrypted payload is not readable in a normal capture.

![Wireshark DNS packets](screenshots/17-dns-analysis.png)

*Ref 17 — DNS analysis.* Used the DNS filter to inspect name-resolution queries and responses, connecting domain lookups to the observed web traffic.

### 7. Investigate ICMP and Firewall Behavior

![Ping connectivity test](screenshots/18-icmp-connectivity.png)

*Ref 18 — ICMP baseline.* Ran `ping` against a domain and reviewed replies, latency, and packet loss as a basic connectivity test.

![Create ICMP firewall rule](screenshots/19-block-icmp-rule.png)

*Ref 19 — ICMP filtering rule.* Created an inbound ICMPv4 block rule. The screenshot documents successful rule creation, not a separate packet-drop validation.

![Remove ICMP firewall rule](screenshots/20-remove-icmp-rule.png)

*Ref 20 — Cleanup.* Removed the temporary ICMP rule to restore the lab's prior configuration.

### 8. Review the Full Packet Capture

![Wireshark packet capture overview](screenshots/21-wireshark-capture-overview.png)

*Ref 21 — Capture overview.* Reviewed the broader list of captured packets and their timing, source/destination information, and protocols to place filtered HTTP, TLS, and DNS observations in context.

## Key Takeaways

- Host-level network visibility improves when ports, PIDs, services, and packet captures are examined together.
- Firewall rules should be documented and their lifecycle managed carefully, including test-rule removal.
- Wireshark display filters help isolate protocols, while the full capture provides additional investigative context.
- This was a **hands-on lab**; successful rule creation and protocol inspection should not be represented as enterprise-scale security validation.

## Evidence

All 21 screenshots are supplied in the [`screenshots/`](screenshots/) directory and linked above.

---

**Author:** [Alexander Cox](https://www.linkedin.com/in/alexandercox25/) · [GitHub Portfolio](https://github.com/KerberosAC)
