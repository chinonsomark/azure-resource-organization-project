# Azure Resource Organisation and Resource Groups Project

## Overview

This project demonstrates core Azure governance practices, including subscription and resource group structure, naming conventions, tagging strategy, role-based access control (RBAC), and resource lifecycle management.

## Naming Convention

All resource groups follow the pattern:

```
rg-<purpose>-<environment>-<region>-<sequence>
```

| Component   | Description                                  | Example                  |
|-------------|-----------------------------------------------|---------------------------|
| purpose     | The application or service the group supports | shared-services, webapp  |
| environment | Deployment environment                         | prod, dev (omitted for shared services) |
| region      | Azure region, abbreviated                      | eastus                    |
| sequence    | Three-digit number for uniqueness              | 001                       |

Examples used in this project:

- `rg-shared-services-eastus-001`
- `rg-webapp-prod-eastus-001`
- `rg-webapp-dev-eastus-001` (deleted as part of lifecycle testing — see below)

Storage account names follow Azure's stricter naming rules (lowercase letters and numbers only, no hyphens, globally unique), using the pattern `st<purpose><environment><region><suffix>`, e.g. `stwebappdeveastusaj1`.

## Resource Group Structure

### 1. rg-shared-services-eastus-001
Houses shared infrastructure used across environments.

- **Resource:** `stwebappsharedeastusaj1` (Storage Account, Standard LRS, East US)

### 2. rg-webapp-prod-eastus-001
Production tier for the web application. Access is restricted to minimize risk of accidental changes to live resources.

- **Resources:** _[add any resources deployed here, e.g. storage account / App Service]_

### 3. rg-webapp-dev-eastus-001 (deleted)
Development/testing tier, used to demonstrate resource deployment, tagging, RBAC, and bulk lifecycle deletion.

- **Resource:** `stwebappdeveastusaj1` (Storage Account, Standard LRS, East US) — deleted along with the resource group as part of Task 6.

## Tagging Strategy

| Tag Key      | Purpose                                         | Example Values                  |
|--------------|--------------------------------------------------|----------------------------------|
| environment  | Identifies the deployment stage                 | Shared, Production, Development |
| Owner        | Team responsible for the resource               | TeamA, TeamB, TeamC              |
| project      | Groups resources by initiative                  | azure-learning                   |
| costcenter   | Enables cost allocation and billing reports     | cc-001, cc-002                   |
| createdby    | Tracks who provisioned the resource             | Ajagu                            |

These tags support cost tracking (via `costcenter`), accountability (via `Owner` and `createdby`), and environment-based filtering or automation (via `environment`).

## RBAC Summary

See [rbac-report.md](./rbac-report.md) for full details on role assignments and the rationale behind each.

## Screenshots

All supporting screenshots are located in the [screenshots/](./screenshots) folder, documenting:

- Resource group creation across all three groups
- Tagging configuration on resource groups and resources
- RBAC role assignments on production and development resource groups
- Before/after deletion of the development resource group

## Lifecycle Management

To demonstrate cleanup of temporary environments, `rg-webapp-dev-eastus-001` (including its storage account) was deleted in full after all required screenshots were captured. See `screenshots/09-dev-rg-deleted.png` for confirmation that the resource group no longer appears in the resource group list.

## Infrastructure as Code (Optional)

_[If you completed the optional IaC task, describe your CLI/Bicep/Terraform files here and reference the `iac/` folder.]_
