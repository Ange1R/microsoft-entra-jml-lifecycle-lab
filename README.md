# Microsoft Entra ID Joiner-Mover-Leaver Lifecycle Lab

## Dunder Mifflin Identity Lifecycle Simulation

## Overview

This project documents a hands-on Joiner-Mover-Leaver (JML) identity lifecycle lab completed in Microsoft Entra ID using Microsoft Graph PowerShell.

The lab simulates common IAM administration tasks for a fictional Dunder Mifflin environment:

- **Joiner:** Provision a new employee account and assign role-based access.
- **Mover:** Update employee attributes and transition access when a user changes roles.
- **Leaver:** Disable an employee account, revoke active sessions, remove active access, and retain the account for audit purposes.

All lifecycle actions were completed through Microsoft Graph PowerShell and validated through Microsoft Entra ID audit logs.

---

## Environment

| Component | Details |
|---|---|
| Identity platform | Microsoft Entra ID Free |
| Automation tool | Microsoft Graph PowerShell SDK |
| PowerShell version | PowerShell 7 for macOS |
| Authentication | Delegated Microsoft Graph permissions |
| Group type | Assigned security groups |
| Audit source | Microsoft Entra ID Audit Logs |

---

## Tools Used

- Microsoft Entra ID
- Microsoft Graph PowerShell SDK
- PowerShell 7
- Microsoft Azure Portal
- Microsoft Entra Audit Logs

---

## Security Groups

The following security groups were created to simulate department-based and employee lifecycle access:

| Security Group | Purpose |
|---|---|
| `SG-DM-Reception` | Reception department access |
| `SG-DM-Sales` | Sales department access |
| `SG-DM-Management` | Management department access |
| `SG-DM-All-Employees` | General employee access |
| `SG-DM-Leaver-Hold` | Retention group for disabled former employees |

---

# Joiner Workflow — Erin Hannon

## Scenario

Erin Hannon was provisioned as a new Dunder Mifflin Reception employee.

## Account Details

| Attribute | Value |
|---|---|
| Display Name | Erin Hannon |
| Department | Reception |
| Job Title | Receptionist |
| Account Status | Enabled |
| Assigned Groups | `SG-DM-Reception`, `SG-DM-All-Employees` |

## Actions Performed

1. Created Erin Hannon as a cloud-only Microsoft Entra user.
2. Assigned Department, Job Title, Usage Location, and password profile attributes.
3. Required a password change at first sign-in.
4. Added Erin to the Reception security group.
5. Added Erin to the All Employees security group.
6. Verified account attributes and group memberships through Microsoft Graph PowerShell.
7. Reviewed Entra audit logs to confirm successful user creation and group assignment.

## Result

Erin was provisioned successfully as an enabled Reception employee with appropriate department-based access.

---

# Mover Workflow — Jim Halpert

## Scenario

Jim Halpert was initially provisioned as a Sales Representative. His role was then changed to Assistant Regional Manager, requiring an attribute update and access transition.

## Before Move

| Attribute | Value |
|---|---|
| Department | Sales |
| Job Title | Sales Representative |
| Account Status | Enabled |
| Group Memberships | `SG-DM-Sales`, `SG-DM-All-Employees` |

## Actions Performed

1. Created Jim Halpert as an active Sales employee.
2. Assigned Sales and All Employees access.
3. Updated Jim's Department from Sales to Management.
4. Updated Job Title from Sales Representative to Assistant Regional Manager.
5. Removed Jim from `SG-DM-Sales`.
6. Added Jim to `SG-DM-Management`.
7. Retained Jim's `SG-DM-All-Employees` membership.
8. Verified final attributes and memberships through Microsoft Graph PowerShell.
9. Reviewed Entra audit logs to confirm successful user and group changes.

## Result

Jim's outdated Sales access was removed and replaced with Management access.

### Final Group Memberships

```text
SG-DM-Management
SG-DM-All-Employees
