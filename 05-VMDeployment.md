# Azure Virtual Machine Deployment

## Project Objective

Deploy a secure Azure management server for administration and operations.

---

# VM Information

Name:

```text
AZ-MGMT-SVR01
```

Role:

```text
Azure Management Server
Jump Server
Administration Workstation
```

---

# Infrastructure Placement

Resource Group:

```text
RG-Management-US
```

Region:

```text
North Central US
```

Subnet:

```text
Management
10.10.1.0/24
```

---

# Security Configuration

## Trusted Launch

Enabled

---

## Secure Boot

Enabled

---

## vTPM

Enabled

---

# Operating System

```text
Windows Server 2022 Datacenter Azure Edition
```

---

# VM Size Evaluation

Several VM sizes were evaluated.

Challenge:

Many UK regions did not support required subscriptions and VM sizes.

Final Selection:

```text
Standard B2als_v2
```

Benefits:

- 2 vCPU
- 4 GB RAM
- Better administrative performance
- Suitable for monitoring workloads

---

# Disk Configuration

```text
Standard SSD
```

Benefits:

- Cost effective
- Improved performance
- Suitable for management workloads

---

# Network Design

```mermaid
flowchart TB

[Internet]

↓

[NSG-Management]

↓

[Management Subnet]

↓

[AZ-MGMT-SVR01]

10.10.1.4
```

---

# IP Addressing

Private IP:

```text
10.10.1.4
```

Public IP:

Assigned by Azure.

---

# Operational Controls

Enabled:

```text
Daily Shutdown
Boot Diagnostics
Trusted Launch Security
```

---

# Lessons Learned

Validation required:

```text
Region
SKU Availability
Billing Scope
Subscription
```

before deployment.

---

# Skills Demonstrated

- Azure Virtual Machines
- Trusted Launch
- Windows Server Azure Edition
- Secure Deployment
- VM Sizing
- Network Placement
