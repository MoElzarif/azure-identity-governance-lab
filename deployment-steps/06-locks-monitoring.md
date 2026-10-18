# 06 — Resource Locks and Monitoring

## Objective
Protect governed resources and establish an audit trail.

## Evidence
- A **Delete** management lock named `lock-northstar-delete` on the governance resource group.
- Azure Activity Log records for policy assignments, role assignments, locks, and resource-group updates.
- Microsoft Entra **audit logs** showing identity-related operations and their success/failure status.
- Microsoft Entra **sign-in logs** showing interactive sign-in outcomes.
- Final resource-group overview confirming Canada Central and governance tags.

## Procedure
1. Open the resource group **Locks** blade and create/review a Delete lock.
2. Inspect the resource-group **Activity log** for management events.
3. Inspect **Entra ID > Monitoring > Audit logs** and **Sign-in logs**.
4. Review group membership and resource-group configuration.

**Why it matters:** Locks reduce accidental deletion risk, while logs support troubleshooting and accountability. A Delete lock is not a replacement for access control or backups.
