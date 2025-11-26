# Security Overview

This document summarizes the security posture of the **Serverless Data Lakehouse** architecture.

## Defense-in-Depth

The lakehouse applies multiple layers of security controls:

### Identity & Access (IAM)

- Least-privilege IAM roles for Glue, Athena, and EMR
- Lake Formation for fine-grained access control
- Column-level and row-level security policies
- Cross-account data sharing with resource policies

### Data Protection

- **At rest**: S3 SSE-KMS encryption for all data
- **In transit**: TLS 1.2+ for all service communication
- **Delta Lake**: Transaction logs encrypted
- **Query results**: Encrypted Athena result buckets

### Network Isolation

- VPC endpoints for S3, Glue, and Athena
- Private subnets for EMR Serverless
- No public internet access for data plane
- Security groups for EMR cluster access

### Data Governance

- Lake Formation data catalog permissions
- Column-level masking for sensitive data
- Data lineage tracking
- Audit logging via CloudTrail

## ACID Transactions

Delta Lake provides:

- Atomic writes for data consistency
- Schema enforcement and evolution
- Time travel for data recovery
- Audit history for compliance

## Compliance Considerations

The architecture supports:

- SOC 2 Type II controls
- GDPR data protection (with Lake Formation)
- HIPAA data handling requirements
- PCI-DSS data security

> For detailed security configurations, see `SECURITY.md` in the project root.
