## Azure Backup & Recovery

Implemented Azure Backup protection for Azure virtual machines using Recovery Services Vault.

### Components

- Recovery Services Vault: REC-SERV-VAULT-SoloTech-US
- Protected Resource: AZ-MGMT-SVR01
- Policy Type: Enhanced Backup Policy
- Recovery Point Type: Crash Consistent Snapshot

### Backup Features

- Enhanced Policy
- Instant Restore Capability
- Immutable Recovery Points
- 30-Day Retention
- Geo-Redundant Vault Storage

### Skills Demonstrated

- Azure Backup
- Recovery Services Vault
- Recovery Point Management
- Backup Policies
- Business Continuity
- Infrastructure Protection

flowchart TB

A[AZ-MGMT-SVR01]
--> B[Azure Backup]

B --> C[REC-SERV-VAULT-SoloTech-US]

C --> D[Recovery Point]

D --> E[Restore Operations]
