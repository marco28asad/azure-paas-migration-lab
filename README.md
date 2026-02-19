# azure-paas-migration-lab
Migrating from IaaS to PaaS - Azure SQL Database with Key Vault and Managed Identity

# Azure PaaS Migration Lab - SQL Database with Key Vault

## Overview
Migrated from IaaS to PaaS by replacing a database VM with Azure SQL Database. Implemented secure credential management using Azure Key Vault and Managed Identity for passwordless authentication.

## Architecture

**Before (IaaS):**
```
vm-web-01 ←→ vm-db-01 (manual management, patching, backups)
```

**After (PaaS):**
```
vm-web-01 → Key Vault → Azure SQL Database
(Managed Identity for passwordless auth)
```

## What I Built

**Azure SQL Database (PaaS)**
- Service Tier: Basic (5 DTUs, cost-optimized at ~$5/month)
- Automatic backups, patching, and high availability
- No infrastructure management required

**Azure Key Vault**
- Secure storage for database password
- Eliminates hardcoded credentials
- Integrated with Managed Identity

**Managed Identity**
- System-assigned identity on vm-web-01
- Passwordless authentication to Key Vault
- Principle of least privilege (Get/List permissions only)

## Problem Solved

**Challenge:** Database VM required constant maintenance (patching, backups, monitoring) and stored credentials insecurely in configuration files, creating security risks and operational overhead.

**Solution Approach:**
1. **Analyzed trade-offs** between IaaS and PaaS options
2. **Selected Azure SQL Database** to eliminate infrastructure management
3. **Implemented Key Vault** to remove credentials from code/config
4. **Configured Managed Identity** for passwordless authentication
5. **Optimized costs** by selecting appropriate service tier (Basic vs Hyperscale)

**Result:**
-  85% cost reduction (~$50/month → ~$6/month)
-  Zero infrastructure maintenance required
-  Eliminated credential exposure risk
-  Automatic backups and high availability included
-  Built-in monitoring without additional configuration

## Real-World Applications

**Enterprise Use Cases:**
- **SaaS Platforms:** Multi-tenant applications need secure, managed databases without infrastructure overhead
- **Startups:** Fast-moving teams can focus on product development instead of database administration
- **Financial Services:** Key Vault audit logs satisfy PCI-DSS and SOX compliance requirements
- **Healthcare:** HIPAA-compliant credential management with zero-trust architecture

**DevOps Workflows:**
- **CI/CD Pipelines:** Applications retrieve database credentials securely without embedding passwords in code repositories
- **Container Deployments:** Kubernetes pods use Managed Identity to access databases without storing secrets in container images
- **Infrastructure as Code:** Terraform/ARM templates reference Key Vault secrets instead of plaintext passwords

**Security Scenarios:**
- **Credential Rotation:** Update database password in Key Vault once, all applications automatically use new credential
- **Access Auditing:** Track which applications accessed which secrets and when (compliance requirement)
- **Breach Prevention:** Compromised application code doesn't expose database passwords since they're not stored in code

## Key Steps

1. Decommissioned old database VM (vm-db-01)
2. Deployed Azure SQL Database with firewall rules
3. Created Key Vault and stored SQL password as secret
4. Enabled Managed Identity on web server
5. Configured Key Vault access policy for VM
6. Validated with Azure Monitor metrics

## Technologies Used
Azure SQL Database | Azure Key Vault | Managed Identity | Azure Monitor | Azure Virtual Machines

## Skills Demonstrated
- PaaS migration strategy and execution
- Secure credential management architecture
- Cost optimization through service tier analysis
- Azure RBAC and access policy configuration
- Cloud security best practices (zero-trust, least privilege)
- Problem analysis and solution design

---

**Marco Asad** - Cloud Engineer  
[LinkedIn](https://www.linkedin.com/in/marco-asad-6a56a03ab/) |
