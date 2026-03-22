## Project Phases
It's recommended to do this lab in an isolated, virtual environment. I am using Proxmox but theoretically this should also work similarly in VirtualBox or VMware setups. 

### Phase 1: Network Setup
If you do not have one already, create an isolated internal bridge with no upstream gateway and no NAT. Give this bridge a private subnet (like 10.10.10.0/24) with no DHCP if you want full control over IPs. 

### Phase 2: VM Provisioning
This lab can be done with 2 hosts, but for those wanting some additional security and practice, it's recommended to implement a jumpbox system. Completely optional, but it will add extra steps. 

- Jumpbox
	- Lightweight Linux
	- Two NICs: One on `vmbr0` (for your SSH access), on on `vmbr1` (to reach the lab)
	- Static IP on both interfaces
- Scanner 
	- Kali Linux
	- Single NIC on `vmbr1`
	- Static IP
	- Installed with Nessus Essentials
- Target
	- Metasploitable 2
	- Single NIC on `vmbr1`
	- Static IP

#### Phase 2.1: Accessing VMs
If you are not using a jumpbox, just access your VMs directly through SSH or their virtual desktop interface. If you are using a jumpbox though, you can access your machines a few ways. The simplest would through SSH hopping: SSH into your jumpbox, then SSH again into your hosts. This is simple and works fine but if you need to access to Nessus web interface, then SSH Forwarding will need to be set up.

### Phase 3: Nessus install and configuration
- Download the Nessus Essentials `.deb` package and install it on the scanner
- Register for a free activation code at tenable.com
- Access the Nessus web UI via your jumpbox (SSH port forward or browser proxied through the jump)
- Create a basic network scan policy targeting the Metasploitable 2 IP
- Key scan options to understand before running: scan type (basic vs advanced), credential vs non-credentialed scan, plugin families enabled

### Phase 4: Analysis
Refer to the Procedure above for basic overview of what we're doing here.
1. Begin with pre-scan prediction using STRIDE method, create threat tree
2. Run the Nessus scan
	1. Start with an unauthenticated scan to simulate external attacker perspective
	2. Optionally follow with a credentialed scan using metasploitable default credentials
3. Review scan report, then compare against predictions

### Phase 5: Reporting
As always, document findings, actions, and outcomes. The best type of report this project will fit into is a **Threat and Vulnerability Assessment (TVA)**. This will combine both our threat model and discovered vulnerabilities into an actionable report that can be presented to administrators. 

## Mitigation
Take the steps listed in the TVA to patch the issues in the vulnerable system. After patching is done, re-scan to prove security. 
