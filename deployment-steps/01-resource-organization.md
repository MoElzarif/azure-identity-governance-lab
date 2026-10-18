# 01 — Resource Organization and Cost Governance

## Objective
Establish a governed Azure environment for the fictional Northstar Technologies organization.

## Evidence and implementation

- Resource group: `rg-northstar-governance`, located in **Canada Central**.
- Tags: `Environment=Lab`, `Project=Identity-Governance`, `Department=CloudOps`, `ManagedBy=CloudTeam`.
- Subscription-scoped monthly budget: **10** (subscription currency), with **50%, 80%, and 100%** actual-cost alerts.

## Procedure
1. Create a resource group in Canada Central.
2. Add organizational tags to identify the environment, owner, and department.
3. Open **Cost Management > Budgets** and create a monthly budget.
4. Configure alert thresholds and an email recipient.
5. Confirm the resource group overview and budget summary.

**Why it matters:** Tags help resource organization; budgets give cost visibility. Budget alerts do not automatically stop spending.
