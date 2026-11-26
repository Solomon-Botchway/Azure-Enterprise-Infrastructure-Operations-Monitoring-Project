# Azure NAT Gateway

## Project Overview

This project introduced Azure NAT Gateway to provide secure outbound Internet access for private Azure workloads without exposing virtual machines directly to the Internet.

The requirement was identified while deploying the first cloud-hosted Domain Controller. Windows activation, Azure KMS communication, Windows Update and Microsoft service connectivity required outbound Internet access while maintaining a private-only security posture.

---

# Project Objectives

- Eliminate Public IP dependency
- Enable outbound Internet connectivity
- Maintain private VM architecture
- Support Windows activation
- Support Microsoft service connectivity
- Implement enterprise egress design

---

# Business Requirement

AZ-DC01 was deployed without a Public IP address.

Initial testing revealed:

```text
DNS Resolution      : SUCCESS

RDP                 : SUCCESS

Internet Access     : FAILED

Windows Activation  : FAILED
```

Examples:

```powershell
Test-NetConnection www.microsoft.com -Port 443
```

Result:

```text
TcpTestSucceeded : False
```

---

# Solution Architecture

```mermaid
flowchart LR

    A[AZ-DC01]

    --> B[DomainControllers Subnet]

    --> C[NAT-SoloTech-US]

    --> D[PIP-NAT-SoloTech-US]

    --> E[Internet]
```

---

# NAT Gateway Configuration

Resource:

```text
NAT-SoloTech-US
```

Region:

```text
North Central US
```

Resource Group:

```text
RG-Management-US
```

---

# Public IP Configuration

Public IP:

```text
PIP-NAT-SoloTech-US
```

Configuration:

```text
IPv4

Static

Regional

Standard V2
```

---

# Subnet Association

Associated Subnet:

```text
DomainControllers

10.10.2.0/24
```

---

# Validation

## HTTPS Connectivity

Command:

```powershell
Test-NetConnection `
www.microsoft.com `
-Port 443
```

Result:

```text
TcpTestSucceeded : True
```

---

## Azure KMS Connectivity

Command:

```powershell
Test-NetConnection `
azkms.core.windows.net `
-Port 1688
```

Result:

```text
TcpTestSucceeded : True
```

---

## Browser Validation

Successfully accessed:

```text
https://www.msn.com
```

from:

```text
AZ-DC01
```

---

# Benefits

- Private workloads remain private
- No Public IP required on Domain Controllers
- Reduced attack surface
- Controlled outbound Internet access
- Enterprise-aligned networking design

---

# Lessons Learned

Inbound and outbound connectivity are different networking concepts.

Public IP addresses are not required for outbound communication when Azure NAT Gateway is implemented.

---

# Project Outcome

Successfully implemented Azure NAT Gateway.

Achievements:

✅ Outbound Internet Connectivity

✅ Secure Private Architecture

✅ Windows Activation Support

✅ Azure KMS Access

✅ Enterprise Egress Design
