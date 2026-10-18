# Azure Identity & Governance Lab

**Microsoft Entra ID · Azure RBAC · Azure Policy · MFA · Resource Protection · Cost Governance · Monitoring**

## Project Overview

This hands-on Azure administration project demonstrates the foundational identity and governance controls for **Northstar Technologies**, a fictional organization. The lab focuses on organizing resources, managing identities, applying least-privilege access, restricting deployment locations, protecting against accidental deletion, setting cost alerts, and reviewing security and activity evidence.

The key security objective was to permit deployments in **Canada Central** while **intentionally testing that an East US deployment would be blocked**.

## Lab Configuration

| Component | Configuration |
|---|---|
| Governance resource group | `rg-northstar-governance` |
| Approved region | **Canada Central** |
| Users and groups | Four Entra users, three security groups |
| RBAC | CloudOps: Contributor; Engineering and Security: Reader |
| Identity security | Security defaults and Authenticator MFA registration |
| Azure Policy | Audit and Deny assignments for approved location |
| Negative test | **East US network security group denied as designed** |
| Resource protection | Delete lock |
| Cost governance | Monthly budget of 10, alerts at 50%, 80%, 100% |
| Monitoring | Activity logs, audit logs, sign-in logs |

## Implementation and Evidence Walkthrough

The following sequence documents the configuration, its purpose, and the corresponding validation captured during the lab.

### 01. Subscription Budget

A monthly subscription budget named `budget-northstar-lab` was configured with a limit of **10 in the subscription currency** and cost alerts at **50%, 80%, and 100%**. Evaluated spend was zero at the time of capture. Budgets provide notifications rather than a hard spending cap.

### 02. Governance Resource Group

The resource group `rg-northstar-governance` was established in **Canada Central** with tags for environment, project, department, and management ownership. This establishes the scope for the lab's access and policy controls.

### 03. Microsoft Entra Users

Four lab user accounts were created in Microsoft Entra ID to represent different organizational responsibilities and demonstrate identity administration.

### 04. Departmental Security Groups

Three security groups—`SG-CloudOps`, `SG-Engineering`, and `SG-Security`—were configured to organize identities by job function rather than granting every permission individually.

### 05. Resource-Group RBAC

At the governance resource-group scope, CloudOps received **Contributor** while Engineering and Security received **Reader**. The portal also shows an inherited subscription **Owner** assignment. This demonstrates role separation and scoped authorization.

### 06. Entra Security Reader Role

A Microsoft Entra **Security Reader** directory-role assignment was reviewed. Directory roles govern Entra permissions and are distinct from Azure resource-group RBAC.

### 07. Security Defaults

Microsoft Entra **security defaults** were enabled to provide baseline identity protections, including MFA-related safeguards.

### 08. Authenticator MFA Registration

The security information page demonstrates registration of **Microsoft Authenticator push MFA** for a lab identity. Registration is evidence of setup, not proof of MFA enforcement on every sign-in.

### 09. Location Audit Policy

The `audit-northstar-region` policy assignment was configured for **Canada Central** with the **Audit** effect. It provides visibility into resources that violate the approved location requirement.

### 10. Location Deny Policy

The `deny-northstar-region` assignment uses the **Deny** effect with the same approved Canada Central location. Its purpose is to reject noncompliant resource creation.

### 11. Security Validation — East US Blocked

**This was an intentional negative test.** A network security group was deliberately configured for **East US**, outside the approved region. Azure rejected the request with a policy-denial message stating that Northstar resources are permitted only in **Canada Central**. The blocked attempt is evidence that the preventive control worked.

### 12. Resource Delete Lock

A resource-group **Delete** lock named `lock-northstar-delete` was applied to help prevent accidental deletion of the governance resource group.

### 13. Azure Activity Log

The Activity Log shows management events for role assignments, policy assignments, locks, and resource-group updates. These records help establish a change trail.

### 14. Policy Compliance Review

The portal showed both region policies as **Compliant** and **100%** overall compliance, but also **zero evaluated resources**. That result should not be interpreted as a fleet-wide compliance assessment; the East US denial is the direct enforcement test.

### 15. Microsoft Entra Sign-In Logs

Interactive sign-in logs were reviewed to inspect successful and interrupted authentication attempts and their associated applications.

### 16. Microsoft Entra Audit Logs

Directory audit logs showed user-management, authentication-method, and application-management activity, including successful and failed events. This demonstrates identity-level traceability.

### 17. CloudOps Membership

The CloudOps group membership view verifies the direct member associated with the group granted Contributor access.

### 18. Engineering Membership

The Engineering group membership view verifies the direct member associated with the group granted Reader access.

### 19. Security Membership

The Security group membership view verifies the direct member associated with the group granted Reader access; a separate Entra Security Reader role was also documented.

### 20. Final Governance Review

The final resource-group overview confirms **Canada Central**, the Northstar governance tags, and the overall lab scope. The resource list was empty at capture time; the lab focuses on governance and identity controls rather than deploying a production workload.

## Deployment Guides

1. [Resource organization and cost governance](deployment-steps/01-resource-organization.md)
2. [Microsoft Entra users and security groups](deployment-steps/02-entra-users-groups.md)
3. [Azure RBAC and directory roles](deployment-steps/03-rbac-roles.md)
4. [Security defaults and MFA](deployment-steps/04-mfa-security.md)
5. [Azure Policy and Canada Central enforcement](deployment-steps/05-azure-policy.md)
6. [Resource locks and monitoring](deployment-steps/06-locks-monitoring.md)

## Key Lessons

- **Audit and Deny serve different purposes:** Audit surfaces violations, while Deny prevents matching deployments.
- **Negative tests demonstrate enforcement:** The intentionally rejected East US request is direct evidence that the regional control worked.
- **Permissions must be scoped:** Azure RBAC and Entra directory roles control different surfaces.
- **Compliance dashboards need context:** 100% with zero evaluated resources does not demonstrate fleet-wide compliance.
- **Governance is layered:** Cost alerts, resource locks, role assignments, MFA, policies, and logs each address different risks.

## Tools and Technologies

Microsoft Azure Portal · Microsoft Entra ID · Azure RBAC · Azure Policy · Azure Cost Management · Azure Activity Log · Microsoft Authenticator

## Project Scope

This is an educational governance lab documented from Azure portal configuration and test evidence, not a production deployment or independent compliance certification.
