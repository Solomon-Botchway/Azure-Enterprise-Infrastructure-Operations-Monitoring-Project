## Azure Backup & Recovery

# Azure Backup Architecture
```mermaid
flowchart TB

    A[AZ-MGMT-SVR01<br>Windows Server 2022]

    A --> B[Azure Backup Service]

    B --> C[Snapshot Created]

    C --> D[Transfer To Vault]

    D --> E[REC-SERV-VAULT-SoloTech-US]

    E --> F[Recovery Point]

    F --> G[Restore VM]

    F --> H[Restore Disk]

    F --> I[File Recovery]
```
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
