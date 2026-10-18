# Azure Identity & Governance Lab

**Microsoft Entra ID · Azure RBAC · Azure Policy · MFA · Cost Management · Resource Locks · Monitoring**

## Project Overview

This hands-on Microsoft Azure project demonstrates how I built an identity and governance foundation for **Northstar Technologies**, a fictional organization. The lab focuses on user and group management, least-privilege authorization, identity security, regional policy enforcement, resource protection, cost governance, and audit visibility.

The environment uses **Canada Central** as its approved Azure region. A deployment to **East US was intentionally attempted and successfully blocked** to validate the Azure Policy control.

## Implementation & Evidence

### 1. Configure Cost Governance

I started by creating a monthly Azure budget named `budget-northstar-lab`. The budget limit was set to **10 in the subscription currency**, with alert thresholds at **50%, 80%, and 100%**. This provides early visibility into unexpected lab spending and demonstrates basic Azure Cost Management governance.

![1. Configure Cost Governance](01-budget-configuration.png)

**Evidence:** The budget configuration shows the monthly limit and the three cost alert thresholds used for the lab.

---

### 2. Create the Governance Resource Group

I created `rg-northstar-governance` in **Canada Central**, the approved region for Northstar Technologies. I also applied tags for `Environment`, `Project`, `Department`, and `ManagedBy` so the environment can be identified and organized consistently.

![2. Create the Governance Resource Group](02-resource-group-overview.png)

**Evidence:** The resource group overview confirms the Canada Central location and the governance tags applied to the lab.

---

### 3. Create Microsoft Entra Users

I created four lab identities in Microsoft Entra ID to represent users with different responsibilities. These identities provide the foundation for testing group-based access, directory roles, authentication security, and audit logging.

![3. Create Microsoft Entra Users](03-entra-users.png)

**Evidence:** The Entra users page shows the lab identities created for the Northstar environment.

---

### 4. Organize Access with Security Groups

Instead of managing permissions separately for every user, I created three security groups: `SG-CloudOps`, `SG-Engineering`, and `SG-Security`. This models a more scalable approach where access is assigned according to job function.

![4. Organize Access with Security Groups](04-entra-security-groups.png)

**Evidence:** The Entra groups page confirms the three security groups used to separate CloudOps, Engineering, and Security responsibilities.

---

### 5. Apply Azure RBAC at the Resource-Group Scope

I assigned **Contributor** to the CloudOps group and **Reader** to the Engineering and Security groups at `rg-northstar-governance`. This gives CloudOps resource-management capability while allowing the other teams to inspect resources without modifying them. The portal also shows an inherited Owner assignment from the subscription.

![5. Apply Azure RBAC at the Resource-Group Scope](05-rbac-role-assignments.png)

**Evidence:** The IAM role-assignment view provides evidence of the group-based Contributor and Reader permissions and their scope.

---

### 6. Assign the Entra Security Reader Role

I also reviewed an Entra **Security Reader** directory-role assignment. This is separate from Azure resource RBAC: Azure RBAC controls access to Azure resources, while Entra directory roles control permissions within Microsoft Entra ID.

![6. Assign the Entra Security Reader Role](06-entra-security-reader-role.png)

**Evidence:** The role assignment confirms Security Reader access at the Microsoft Entra directory layer.

---

### 7. Enable Microsoft Entra Security Defaults

I enabled **Security defaults** to provide baseline identity protections for the tenant. This strengthens the lab's identity-security posture and introduces MFA-related safeguards without building a custom Conditional Access design.

![7. Enable Microsoft Entra Security Defaults](07-entra-security-defaults.png)

**Evidence:** The tenant settings show Security defaults enabled.

---

### 8. Register Microsoft Authenticator for MFA

I registered **Microsoft Authenticator** as an authentication method for a lab identity. This demonstrates the user-side setup required for stronger authentication.

![8. Register Microsoft Authenticator for MFA](08-mfa-registration.png)

**Evidence:** The security information page confirms Microsoft Authenticator registration. It demonstrates method setup, not that every sign-in in the tenant was challenged with MFA.

---

### 9. Create a Location Audit Policy

I configured `audit-northstar-region` with **Canada Central** as the allowed location. The Audit effect provides visibility into resources that do not meet the regional standard without blocking their creation.

![9. Create a Location Audit Policy](09-azure-policy-location-audit.png)

**Evidence:** The policy assignment shows the Canada Central allowed-location parameter and Audit-based governance control.

---

### 10. Create a Location Deny Policy

I then configured `deny-northstar-region` for the same approved location. Unlike Audit, the **Deny** effect acts as a preventive control by rejecting resource deployments that violate the location requirement.

![10. Create a Location Deny Policy](10-azure-policy-deny.png)

**Evidence:** The Deny policy assignment confirms Canada Central as the approved deployment region.

---

### 11. Validate the Policy with an Intentional East US Deployment

To prove that the preventive control worked, I deliberately attempted to create a **network security group in East US**. East US was intentionally selected because it is outside the approved Canada Central region. Azure rejected the deployment because of the assigned policy.

![11. Validate the Policy with an Intentional East US Deployment](11-policy-deny-test.png)

**Evidence:** **Successful security test:** the deployment denial is the expected result. It proves that the regional Deny policy prevented a noncompliant resource from being created.

---

### 12. Protect the Resource Group with a Delete Lock

I added a **Delete** management lock named `lock-northstar-delete` to the governance resource group. The lock adds protection against accidental deletion and complements access-control permissions.

![12. Protect the Resource Group with a Delete Lock](12-resource-group-lock.png)

**Evidence:** The Locks page confirms the Delete lock applied to the governance scope.

---

### 13. Review Azure Activity Logs

I reviewed the Azure Activity Log to verify management-plane changes made during the lab, including policy assignments, role assignments, locks, and resource-group operations.

![13. Review Azure Activity Logs](13-azure-activity-log.png..png)

**Evidence:** The Activity Log provides a traceable record of administrative changes made to Azure resources and governance controls.

---

### 14. Review Azure Policy Compliance

I reviewed the policy compliance dashboard after assigning the regional controls. The captured view reports **100% compliance**, but it also shows **zero evaluated resources**. For that reason, this screenshot is treated as assignment/compliance-dashboard evidence rather than proof that a deployed resource fleet was fully compliant.

![14. Review Azure Policy Compliance](14-azure-policy-compliance.png..png)

**Evidence:** The compliance view documents the policy state at capture time. The intentional East US denial in the previous test is the stronger direct evidence that enforcement worked.

---

### 15. Review Microsoft Entra Sign-In Logs

I reviewed Microsoft Entra sign-in logs to examine interactive authentication activity and sign-in outcomes. Sign-in monitoring is important for investigating authentication issues and suspicious access patterns.

![15. Review Microsoft Entra Sign-In Logs](Save%20as%2015-entra-signin-logs.png..png)

**Evidence:** The sign-in log captures authentication events generated by the lab identities.

---

### 16. Review Microsoft Entra Audit Logs

I reviewed Entra audit logs to inspect directory-level changes such as identity, authentication-method, and application-management operations. These logs provide accountability for changes within the identity platform.

![16. Review Microsoft Entra Audit Logs](16-entra-audit-logs.png..png)

**Evidence:** The audit log demonstrates the directory audit trail available for identity and configuration changes.

---

### 17. Verify CloudOps Group Membership

I verified the direct membership of `SG-CloudOps`. Because this group received the Contributor role, membership determines which lab identity inherits resource-management access through the group.

![17. Verify CloudOps Group Membership](17-cloudops-group-membership.png..png)

**Evidence:** The membership view connects the CloudOps identity to the group used for Contributor access.

---

### 18. Verify Engineering Access

I verified the Engineering team's access configuration and membership. `SG-Engineering` was assigned the Reader role so the team can inspect resources without receiving modification privileges.

![18. Verify Engineering Access](18-engineering-access-verification.png)

**Evidence:** The Engineering verification screenshot provides evidence of the identity-to-access relationship used in the RBAC design.

---

### 19. Verify Security Team Membership

I verified the membership of `SG-Security`, which was assigned Reader access at the Azure resource-group level. The lab separately demonstrates the Entra Security Reader directory role, showing the distinction between resource and directory permissions.

![19. Verify Security Team Membership](19-security-team-membership.png..png)

**Evidence:** The Security group membership view confirms the identity associated with the group-based Azure Reader assignment.

---

### 20. Final Governance Review

I finished by reviewing the Northstar governance resource group and its configuration. The final state brings together regional organization, tagging, identity, role-based access, policy enforcement, cost controls, resource protection, and monitoring.

![20. Final Governance Review](20-northstar-final-governance-review.png)

**Evidence:** The final resource-group view confirms the governance scope in Canada Central. The lab focuses on identity and governance controls rather than hosting a production workload.

---

## Skills Demonstrated

Microsoft Azure · Microsoft Entra ID · Identity and Access Management · Azure RBAC · Least Privilege · MFA · Azure Policy · Policy Enforcement Testing · Azure Cost Management · Resource Locks · Activity Logs · Entra Audit Logs · Sign-In Monitoring

## Supporting Documentation

Detailed implementation notes are available in the [deployment-steps](deployment-steps) directory for resource organization, Entra identities, RBAC, MFA, Azure Policy, resource protection, and monitoring.

## Project Scope

This project is an educational Azure identity and governance lab. The screenshots document the configuration and validation performed in the Azure portal; the environment is not presented as a production deployment or independent compliance certification.
