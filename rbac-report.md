# RBAC Summary Report

This document summarizes the Role-Based Access Control (RBAC) assignments made at the resource group level, and the rationale behind each.

## Role Assignments

| Resource Group              | User / Team       | Role        | Scope          | Rationale |
|------------------------------|--------------------|-------------|----------------|-----------|
| rg-webapp-prod-eastus-001     | mark               | Contributor | This resource  | The project lead/admin retains full management access to production for deployments and emergency fixes. |
| rg-webapp-prod-eastus-001     | Prod User TeamB    | Reader      | This resource  | General team members can view production resources for monitoring and auditing but cannot make changes — minimizing the risk of accidental production changes. |
| rg-webapp-dev-eastus-001       | mark / chinonso    | Contributor | This resource (deleted) | Developers need full create, modify, and delete access in the development environment to iterate and test freely without impacting production. |
| rg-shared-services-eastus-001 | _[add if configured]_ | _[role]_  | _[scope]_      | _[rationale]_ |

## Principle of Least Privilege

Access levels were assigned based on the sensitivity of each environment:

- **Production (`rg-webapp-prod-eastus-001`)** is the most restricted. Only the admin/lead has Contributor access, while the rest of the team has Reader (view-only) access. This reduces the risk of unintended changes to live, customer-facing resources.
- **Development (`rg-webapp-dev-eastus-001`)** grants broader Contributor access since this environment is meant for active experimentation and testing. Mistakes here have minimal real-world impact, so developers are given the freedom to create, modify, and delete resources as needed.
- **Shared services (`rg-shared-services-eastus-001`)** _[describe access strategy here, e.g. "Contributor access limited to the platform team responsible for maintaining shared infrastructure used across environments."]_

## Notes

- Owner roles shown at the **Subscription** scope are inherited by all resource groups under the subscription and are pre-existing — they are not part of this project's deliberate RBAC configuration, but are included in screenshots for completeness.
- All role assignments shown above were scoped to the **resource group level** (not individual resources), which keeps access management simple as resources are added or removed within each group.
