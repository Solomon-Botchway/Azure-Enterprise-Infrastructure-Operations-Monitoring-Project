# Azure-Enterprise-Infrastructure-Operations-Monitoring-Project
Designed and deployed an enterprise-style Azure infrastructure environment including network segmentation, security controls, Azure virtual machines, Log Analytics, Azure Monitor, Azure CLI, Azure PowerShell, operational monitoring, budgeting, governance controls, and cloud administration tooling.

# Enterprise Azure Infrastructure & Operations Lab

## Project Overview

This project documents the design, deployment, administration, monitoring, and operational management of a Microsoft Azure infrastructure environment built from scratch.

The objective was to simulate a real-world enterprise Azure deployment and gain hands-on experience in:

- Azure Infrastructure Administration
- Azure Governance
- Azure Networking
- Azure Virtual Machines
- Azure Monitoring
- Azure Operations
- Cost Management
- Cloud Security
- Azure Automation Foundations

This lab was built after completing:

- Active Directory Infrastructure
- DNS & DHCP Administration
- Group Policy Management
- File Services
- Microsoft 365 Administration
- Exchange Online Administration
- SharePoint Online Administration
- Microsoft Purview
- Microsoft Entra ID
- Hybrid Identity
- Microsoft Entra Connect

The Azure project represents the next phase of the cloud engineering journey.

---

# Project Goals

The objectives of the project were:

- Design enterprise-style Azure infrastructure
- Implement governance and cost controls
- Build secure network segmentation
- Deploy Azure Virtual Machines
- Create an Azure administration workstation
- Learn Azure CLI and Azure PowerShell
- Configure Azure Monitor
- Deploy Azure Monitor Agent
- Collect operational telemetry
- Implement Log Analytics monitoring
- Build Azure operational skills

---

# Azure Architecture

```text
Azure Subscription 2 Free Plan
│
├── Cost Management
│   ├── Budget Controls
│   ├── Forecast Alerts
│   └── Usage Monitoring
│
├── RG-Management-US
│
├── VNET-SoloTech-US
│
│   ├── Management
│   │    10.10.1.0/24
│   │
│   │    └── AZ-MGMT-SVR01
│   │         10.10.1.4
│   │
│   ├── DomainControllers
│   │    10.10.2.0/24
│   │
│   ├── Applications
│   │    10.10.3.0/24
│   │
│   ├── Servers
│   │    10.10.4.0/24
│   │
│   └── DMZ
│        10.10.5.0/24
│
├── NSG-Management
│
├── NSG-Servers
│
├── AZ-MGMT-SVR01
│
├── LOG-ANL-SoloTech-US
│
├── AZ-MNT-SoloTech-US
│
├── DCR-4-MGMT-SVR01
│
└── Azure Monitor Agent
```

---

# Azure Subscription Planning

## Initial Subscription Discovery

During deployment it was discovered that two Azure subscriptions existed:

### Subscription 1

Original Azure plan associated with the tenant.

### Subscription 2

Azure Free Plan containing:

- Azure Free Services
- Free Trial Credits
- Budget Monitoring Requirements

---

## Challenge Encountered

Initial networking resources were deployed into the incorrect subscription.

Resources included:

```text
RG-Management
VNET-SoloTech
NSG-Management
NSG-Servers
```

---

## Resolution

Resources were evaluated and migrated into the Free Plan subscription to ensure:

- Free credits were consumed correctly
- Billing remained controlled
- Future Azure workloads remained governed

### Skills Demonstrated

- Azure Subscription Administration
- Cost Governance
- Resource Migration
- Azure Billing Awareness

---

# Cost Management & Governance

## Azure Budget Creation

Created:

```text
Azure-Lab-Budget
```

Monthly Budget:

```text
£10
```

---

## Alert Configuration

### Forecasted Cost

```text
50%
```

Purpose:

Early warning of projected overspend.

---

### Actual Cost

```text
80%
```

Purpose:

Warning threshold.

---

### Actual Cost

```text
100%
```

Purpose:

Critical notification.

---

## Governance Lessons Learned

Before deploying workloads:

- Validate billing scope
- Confirm subscription ownership
- Configure budget alerts
- Enable spending visibility

---

# Virtual Network Design

## Virtual Network

```text
VNET-SoloTech-US
```

Address Space:

```text
10.10.0.0/16
```

Region:

```text
North Central US
```

---

# Enterprise Subnet Design

| Subnet | Address Range | Purpose |
|----------|----------|----------|
| Management | 10.10.1.0/24 | Administrative Systems |
| DomainControllers | 10.10.2.0/24 | Directory Services |
| Applications | 10.10.3.0/24 | Business Applications |
| Servers | 10.10.4.0/24 | Infrastructure Servers |
| DMZ | 10.10.5.0/24 | Public Facing Systems |

---

## Design Rationale

The Management network was intentionally positioned as the first subnet because:

- The first deployed workload would be a management server
- Administrative systems require separation
- Future monitoring, backup and automation servers will reside here

---

# Network Security

## NSG-Management

Purpose:

Protect Azure administration systems.

### Rules

#### Allow RDP

```text
TCP 3389
```

Restricted to:

```text
Home Public IP Address
```

instead of:

```text
Any
```

---

### Default Azure Rules

```text
AllowVnetInBound
AllowAzureLoadBalancerInBound
DenyAllInBound
```

---

## NSG-Servers

Purpose:

Future application and infrastructure workloads.

### Rules

#### Allow RDP

```text
TCP 3389
```

#### Allow HTTPS

```text
TCP 443
```

---

## Security Lessons Learned

Avoid:

```text
Source = Any
```

Use:

```text
Source = Known Public IP
```

for administrative access whenever possible.

---

# Azure Virtual Machine Deployment

## VM Name

```text
AZ-MGMT-SVR01
```

---

## Purpose

Management Server

Functions:

- Azure Administration
- PowerShell Automation
- Azure CLI Management
- Monitoring Operations
- Backup Administration
- Cloud Operations

---

## VM Configuration

| Setting | Configuration |
|----------|----------|
| Region | North Central US |
| VM Size | B2als_v2 |
| OS | Windows Server 2022 Azure Edition |
| Disk | Standard SSD |
| Security | Trusted Launch |
| Secure Boot | Enabled |
| vTPM | Enabled |

---

## Network Configuration

### Private Address

```text
10.10.1.4
```

### Subnet

```text
Management
10.10.1.0/24
```

### Public IP

Assigned through Azure Public IP resource.

---

# Mobile Operations

## Azure Mobile App

Configured and tested.

Capabilities:

- VM Monitoring
- VM Start/Stop
- Alert Visibility
- Resource Administration

---

## Microsoft Remote Desktop

Configured for:

```text
AZ-MGMT-SVR01
```

Administration directly from mobile devices.

---

## Operational Benefits

Cloud resources can be:

- Monitored remotely
- Started remotely
- Stopped remotely
- Managed during incidents

without requiring a workstation.

---

# Management Server Build

AZ-MGMT-SVR01 was configured as a dedicated Azure Administration Workstation.

---

## PowerShell 7 Installation

Installed:

```text
PowerShell 7.6.9
```

Verification:

```powershell
$PSVersionTable
```

---

## Azure CLI

Installed:

```text
Azure CLI 2.92.0
```

Verification:

```powershell
az version
```

Authentication:

```powershell
az login
```

---

## Azure PowerShell

Installed:

```powershell
Install-Module Az
```

Authentication:

```powershell
Connect-AzAccount
```

Verification:

```powershell
Get-AzResourceGroup
Get-AzVM
Get-AzNetworkSecurityGroup
```

---

# Azure Monitoring Project

## Initial Objective

Implement enterprise-style monitoring using:

- Azure Monitor
- Azure Monitor Agent
- Log Analytics Workspace
- Data Collection Rules

---

# Log Analytics Workspace

Created:

```text
LOG-ANL-SoloTech-US
```

Purpose:

Centralized log collection and analysis.

---

# Azure Monitor Workspace

Created:

```text
AZ-MNT-SoloTech-US
```

Purpose:

Metrics collection and observability.

---

# Azure Monitor Agent

Installed on:

```text
AZ-MGMT-SVR01
```

Purpose:

Collect telemetry from virtual machines.

---

# Monitoring Challenge

Initial onboarding appeared successful however no results were returned.

Example:

```kusto
Heartbeat
| take 10
```

Result:

```text
No records returned
```

---

# Investigation Process

Validated:

✅ Azure Monitor Agent

✅ Agent Version

✅ Network Connectivity

✅ Data Collection Rule

✅ Resource Association

✅ Data Flow Validation

---

# Root Cause Analysis

Discovered:

```text
Azure Monitor Workspace
```

was receiving Metrics.

However:

```text
Log Analytics Workspace
```

had no configured destination receiving log data.

---

# Troubleshooting Activities

Reviewed:

- Data Collection Rules
- Data Collection Endpoint
- Azure Monitor Workspace
- Log Analytics Workspace
- Data Flow Status
- Resource Associations

Identified:

```text
No Log Analytics destination configured.
```

---

# Resolution

Created custom Data Collection Rule:

```text
DCR-4-MGMT-SVR01
```

Assigned:

```text
AZ-MGMT-SVR01
```

---

## Data Sources

### Windows Event Logs

Collected:

```text
Application
System
Security
```

Levels:

```text
Critical
Error
Warning
Information
```

---

### Performance Counters

Collected:

```text
CPU
Memory
Disk
Network
System Uptime
```

---

### Destination

```text
LOG-ANL-SoloTech-US
```

---

# Successful Telemetry Validation

## Heartbeat Query

```kusto
Heartbeat
| take 1000
```

Successful Result:

```text
AZ-MGMT-SVR01
```

Heartbeat entries collected.

---

## Performance Query

```kusto
Perf
| take 100
```

Successful Result:

```text
CPU Metrics
Disk Metrics
Thread Count
Disk Reads/sec
System Uptime
```

---

# Example KQL Queries

## Heartbeat

```kusto
Heartbeat
| sort by TimeGenerated desc
```

---

## Performance Data

```kusto
Perf
| take 100
```

---

## Recent Events

```kusto
Event
| take 100
```

---

# Key Technical Lessons Learned

## Subscription Governance

Validate billing scope before deployment.

---

## Cost Management

Implement budgets before deploying workloads.

---

## Azure Networking

Separate workloads using dedicated subnets.

---

## Security

Restrict RDP to trusted public IP addresses.

---

## Azure Monitoring

A critical lesson learned:

```text
Azure Monitor Workspace
≠
Log Analytics Workspace
```

Understanding the difference is essential when building modern Azure monitoring platforms.

---

# Skills Demonstrated

## Azure Governance

- Subscription Management
- Resource Migration
- Budget Management
- Cost Monitoring

---

## Azure Networking

- Virtual Networks
- Subnets
- Network Security Groups
- IP Address Planning

---

## Azure Compute

- Azure Virtual Machines
- Windows Server 2022 Azure Edition
- Trusted Launch
- Secure Boot
- vTPM

---

## Azure Security

- Network Segmentation
- Access Restrictions
- Least Privilege Design

---

## Azure Operations

- Azure CLI
- Azure PowerShell
- PowerShell 7
- Mobile Administration

---

## Azure Monitoring

- Azure Monitor
- Azure Monitor Agent
- Log Analytics Workspace
- Azure Monitor Workspace
- Data Collection Rules
- Kusto Query Language
- Performance Monitoring
- Event Collection

---

# Current Project Status

## Completed

✅ Subscription Governance

✅ Cost Governance

✅ Virtual Networking

✅ Network Security

✅ Azure VM Deployment

✅ Azure Administration Workstation

✅ Azure CLI

✅ Azure PowerShell

✅ Azure Monitor

✅ Azure Monitor Agent

✅ Data Collection Rules

✅ Log Analytics

✅ KQL Monitoring

---

# Next Phase

## Azure Backup & Recovery

Planned Components:

```text
RSV-SoloTech-US
Recovery Services Vault
Azure VM Backup
Recovery Points
Restore Operations
Business Continuity
Disaster Recovery
```

---

## Author

**Solo Gates**

Azure Infrastructure & Operations Lab

Built as part of a structured journey from:

```text
Active Directory
        ↓
Microsoft 365
        ↓
Hybrid Identity
        ↓
Azure Infrastructure
        ↓
Azure Operations
```
