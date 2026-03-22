# Metasploitable 2 Threat Modeling Lab

## Overview
This project is a threat-modeling and mitigation exercise. The goal is to create a threat model, scan the test environment for vulnerabilities, measure them with a CVSS score. The scan and analysis results will be included in an actionable Threat and Vulnerability Assessment. These threats will then be mitigated to create a secure system.

## Environment
The lab environment will be an isolated network within a Proxmox hypervisor. It will contain 3 hosts:
1. Target Machine (Metasploitable 2)
2. Scanning Machine (Kali + Nessus)
3. Jumpbox host

## Procedure
We will follow some simple but realistic guidelines for this lab. The plan of action is as follows:
1. Predict: STRIDE pre-scan analysis
2. Scan: With Nessus
3. Compare: Prediction with actual scan
4. Mitigate

### Predict
This will be passive / manual observation first, using the [STRIDE](https://owasp.org/www-community/Threat_Modeling_Process#stride) model. In a real engagement, this would be OSINT, architecture review, and documentation review. Here, we're reviewing several things:
- Target OS and version
- What services are known to us
- What the network topology looks like
- Any known default credentials

Then we're piping this information into STRIDE. We will look into common vulnerabilities associated to the information that was discovered, then analyzing what type of attack can be performed against them and how it could be mitigated. The attack paths, root causes, and necessary mitigation controls will be mapped in a threat tree, and all of this information together will create our threat model.

### Scan
After a prediction of our threat landscape has been completed, the network will be scanned with a vulnerability scanner. In this case it is Nessus. CVSS scores for each vulnerability present will be gathered and compared in the next step. 

### Compare
It's extremely useful to analysts to compare predicted threats versus actual threats. Taking the threat tree that was created and comparing it against the realized CVSS scores can highlight unrealized threats and help guide analysts on where to look in the future. 

### Mitigate
Take the appropriate steps to mitigate each vulnerability identified. Document steps taken, then re-scan to confirm successful mitigations.
