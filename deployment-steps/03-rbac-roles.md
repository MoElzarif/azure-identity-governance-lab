# 03 — Azure RBAC and Directory Roles

## Objective
Enforce least privilege through scoped authorization.

| Principal | Role | Scope shown |
| --- | --- | --- |
| SG-CloudOps | Contributor | Governance resource group |
| SG-Engineering | Reader | Governance resource group |
| SG-Security | Reader | Governance resource group |
| Lab owner | Owner (inherited) | Subscription |

A separate screenshot shows an **Entra Security Reader** directory-role assignment. This is distinct from Azure resource RBAC.

## Procedure
1. Open **rg-northstar-governance > Access control (IAM)**.
2. Add the group-based Contributor and Reader assignments.
3. Inspect role assignments to confirm principal, role, and scope.
4. Review the Entra directory-role assignment separately.

**Why it matters:** The Engineering and Security groups can inspect resources without resource modification privileges, while CloudOps has resource-management capabilities.
