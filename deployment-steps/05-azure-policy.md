# 05 — Azure Policy: Canada Central Only

## Objective
Restrict resource deployments to the organization's approved region: **Canada Central**.

## Controls
- **Audit assignment** (`audit-northstar-region`) to identify resources outside the approved region.
- **Deny assignment** (`deny-northstar-region`) to block disallowed deployments.
- Both screenshots show allowed locations set to `canadacentral` at the governance resource-group scope.

## Intentional negative test
1. Apply the Audit and Deny region-policy assignments.
2. Attempt to create a **network security group in East US**.
3. Observe the red policy-denial message: the organization's policy permits resources only in Canada Central.
4. Capture the rejection as **successful preventive-control validation**.

**Important:** The East US rejection is deliberate, not a failed lab. The screenshot demonstrates that the policy blocked a noncompliant attempt.

## Compliance interpretation
The portal screenshot shows **100% compliance with zero evaluated resources**. It is evidence of assignment status at that moment, **not proof that existing resources were tested and compliant**. The negative deployment test is the direct evidence of enforcement.
