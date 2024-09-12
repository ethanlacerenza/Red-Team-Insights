# Information Gathering

## Overview
**Date:** January 12, 2024  
The goal of Penetration Testing (PT) is to detect security gaps. Penetration Testing is a cyclic activity, as the attack surface changes periodically. In this chapter, we will learn how to methodically map an attack surface using both passive and active methods.

## The Penetration Testing Lifecycle
**Date:** January 14, 2024  
The PT lifecycle includes the following stages:
- Defining the scope
- Information gathering
- Vulnerability detection
- Initial foothold
- Privilege escalation
- Lateral movement
- Reporting
- Remediation

Scoping is crucial before focusing on the main objectives.

## Whois Enumeration
**Date:** January 14, 2024  
Whois is a TCP service tool that provides public information about domain registrations. Registrars often charge a fee for private registration. Basic information obtained from Whois includes details like the IT security director.

## Google Hacking
**Date:** January 14, 2024  
Google hacking involves using specific operators to perform targeted searches:
- `site:git.it filetype:txt` - Searches for text files on the site.
- To exclude certain file types: `site:git.it -filetype:txt`

## Open-Source Code
**Date:** January 19, 2024  
Netcraft provides a free web portal for information gathering.

## GitHub Sensitive Information Disclosure
**Date:** January 20, 2024  
GitHub can be used to discover sensitive information. For example:
- `owner:megacorpone path:user` - Use GitHub dorks to find sensitive data.

## Shodan
**Date:** January 20, 2024  
Shodan is a search engine that crawls devices connected to the internet. It can be used to find all internet-connected devices using queries like:
- `hostname:git.it`

## DNS Enumeration
**Date:** January 20, 2024  
DNS Enumeration translates IP addresses into domain names. Types of DNS records include:
- **NS (Nameserver)**: Contains authoritative DNS servers for a domain.
- **A (Host Record)**: Contains IPv4 addresses for hostnames.
- **AAAA (Quad A)**: Contains IPv6 addresses for hostnames.
- **MX (Mail Exchange)**: Lists mail servers for a domain.

## DNS Enumeration (Part 2)
**Date:** January 20, 2024  
Additional DNS record types:
- **PTR (Pointer Records)**: Used in reverse DNS lookups to find the hostname associated with an IP address.
- **CNAME (Canonical Name Records)**: Used to create domain aliases.
- **TXT (Text Records)**: Can contain arbitrary data for purposes like domain ownership verification.

## DNS Enumeration (Part 3)
**Date:** January 20, 2024  
Commands for DNS enumeration:
- `host -t mx git.it` - Retrieve MX records.
- `dnsrecon -d (domain) -t (type)` - Perform DNS reconnaissance.

## TCP/UDP Port Scanning Theory
**Date:** January 27, 2024  
Port scanning is used to detect open ports and services running on a target. It generates traffic and can be intrusive. TCP port scanning often uses the "connect" scan, which involves a three-way handshake:
- Host sends a TCP SYN packet.
- If the port is open, the server responds with SYN-ACK.

## TCP/UDP Port Scanning Theory (Part 2)
**Date:** January 27, 2024  
UDP scanning involves sending an empty UDP packet to a specific port. The response depends on how the application handles empty packets.

## TCP/UDP Port Scanning Theory (Part 3)
**Date:** January 28, 2024  
UDP scanners may use ICMP port unreachable messages, but this can be unreliable due to firewalls filtering ICMP packets. UDP scanning can be problematic, and protocol-specific scanners may yield more accurate results.

## NETCAT Scanning
**Date:** January 28, 2024  
**TCP Scanning:**
- Command: `nc`
- Options: `-nvv` (verbose), `-w 1` (timeout of 1 second), `-z` (no data sent)

**UDP Scanning:**
- Command: `nc`
- Options: `-nv` (verbose), `-u` (use UDP), `-z` (no data sent), `-w 1` (timeout of 1 second)

## Port Scanning with Nmap
**Date:** January 31, 2024  
Nmap, written by Fyodor, is a popular and versatile port scanner. It requires root privileges for raw socket manipulation. Default TCP scans check the 1,000 most common ports and generate around 72KB of traffic. For a full scan of all 65,535 ports, traffic can reach 4MB.

## Port Scanning with Nmap (Part 2)
**Date:** January 31, 2024  
**SYN Scan** (`-sS`): Performs a stealth scan by not completing the three-way handshake. This method does not appear in application logs.

**TCP Scanning Method:** `-sT` (requires full TCP connection).

**UDP Scanning Method:** `-sU` (combined with SYN scanning for a complete view of the target).

## Network Sweeping
**Date:** January 31, 2024  
Network sweeping applies single-host scanning techniques to an entire network range using CIDR. Nmap sends various probes (ICMP, TCP SYN, TCP ACK) to identify live hosts. The `-oG` option saves results in a greppable format.

## Port Scanning with Nmap (Part 3)
**Date:** February 04, 2024  
**Network Sweep Options:**
- `-sn` - Host discovery
- `--top-ports=20` - Scans the 20 most common ports
- `-A` - Enables traceroute
- `-O` - Detects operating systems based on TCP/IP stack variations
- `--osscan-guess` - Attempts to guess the OS if fingerprinting is not accurate

## Port Scanning with Nmap (Part 4)
**Date:** February 05, 2024  
Nmap’s top ports are listed in `/usr/share/nmap/nmap-services`. Combining `-sU` (UDP) with `-sS` (TCP stealth) and using the `-A` option for OS and service enumeration can provide a comprehensive view of the target.

## Windows Port Scanning
**Date:** February 10, 2024  
Use `Test-NetConnection` to scan ports:
```powershell
Test-NetConnection -Port (port) -ComputerName (host)
```

Windows Port Scanning
Date: February 10, 2024
Script for scanning multiple ports:

powershell
```powershell
1..1025 | % {echo ((New-Object Net.Sockets.TcpClient).Connect("host", $_)) "TCP port $_ is open"} 2>$null
```

Date: March 02, 2024
## SMB (Server Message Block) protocol has various vulnerabilities. 
The NetBIOS service listens on TCP port 139 and several UDP ports. SMB and NetBIOS are separate protocols but often used together.

## SNMP Enumeration
Date: March 09, 2024
SNMP (Simple Network Management Protocol) uses UDP and is vulnerable to spoofing and replay attacks. SNMP MIB (Management Information Base) is a database organized like a tree, representing different network functions.

## SNMP Enumeration (Part 2)
Date: March 18, 2024
Tools for SNMP enumeration:

## onesixtyone: A brute-force tool for SNMP on port 161.
snmpwalk: Enumerates the MIB tree.
Example commands:

Enumerate listening ports:
```bash
snmpwalk -c public -v1 192.168.50.151 1.3.6.1.2.1.6.13.1.3
```
Enumerate processes:
```bash
snmpwalk -c public -v1 192.168.50.151 1.3.6.1.2.1.25.4.2.1.2
```
Enumerate software:

```bash
snmpwalk -c public -v1 192.168.50.151 1.3.6.1.2.1.25.6.3.1.2
```

