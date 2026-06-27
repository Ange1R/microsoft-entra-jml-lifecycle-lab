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

### Final Group Memberships

- `SG-DM-Reception`
- `SG-DM-All-Employees`

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

- `SG-DM-Management`
- `SG-DM-All-Employees`

---

# Leaver Workflow — Ryan Howard

## Scenario

Ryan Howard was offboarded from Dunder Mifflin. His account was retained for audit purposes but disabled and stripped of active business access.

## Account Details

| Attribute | Before Offboarding | Final State |
|---|---|---|
| Display Name | Ryan Howard | Ryan Howard |
| Department | Sales | Sales |
| Job Title | Sales Representative | Sales Representative |
| Account Status | Enabled | Disabled |
| Starting Groups | `SG-DM-Sales`, `SG-DM-All-Employees` | N/A |
| Final Group | N/A | `SG-DM-Leaver-Hold` |

## Actions Performed

1. Created Ryan Howard as an active Sales employee.
2. Assigned `SG-DM-Sales` and `SG-DM-All-Employees` access.
3. Disabled Ryan's Microsoft Entra account.
4. Revoked active sign-in sessions.
5. Removed Ryan from `SG-DM-Sales`.
6. Removed Ryan from `SG-DM-All-Employees`.
7. Added Ryan to `SG-DM-Leaver-Hold`.
8. Retained the disabled account for audit and record-retention purposes.
9. Verified final account status and group membership through Microsoft Graph PowerShell.
10. Reviewed Entra audit logs to confirm successful offboarding actions.

## Result

Ryan's account remained in Microsoft Entra ID for audit and retention purposes, but sign-in was blocked and all active department and employee access was removed.

### Final Group Membership

- `SG-DM-Leaver-Hold`

---

# Final Validation

| User | Final Department | Final Job Title | Account Enabled | Final Groups |
|---|---|---|---|---|
| Erin Hannon | Reception | Receptionist | True | `SG-DM-Reception`, `SG-DM-All-Employees` |
| Jim Halpert | Management | Assistant Regional Manager | True | `SG-DM-Management`, `SG-DM-All-Employees` |
| Ryan Howard | Sales | Sales Representative | False | `SG-DM-Leaver-Hold` |

---

# Audit and Verification

Microsoft Entra ID audit logs were reviewed for each lifecycle workflow.

Audit evidence confirmed successful Microsoft Graph-initiated actions, including:

- User creation
- Password profile configuration
- User attribute updates
- Group membership assignment
- Group membership removal
- Account disablement
- Sign-in session revocation
- Retention-group assignment

---

# Skills Demonstrated

- Microsoft Entra ID administration
- Microsoft Graph PowerShell
- Joiner-Mover-Leaver lifecycle management
- User provisioning and deprovisioning
- Security group management
- Department-based access control
- Least-privilege access transitions
- Account disablement
- Session revocation
- Identity audit-log validation
- IAM workflow documentation

---

# Evidence

The screenshots below show the completed Microsoft Entra ID Joiner-Mover-Leaver workflow and Microsoft Graph PowerShell validation.

## Joiner — Erin Hannon

**Erin’s account attributes were created and validated through Microsoft Graph PowerShell.**

![Erin profile validation](screenshots/Entra-JML-Dunder-Mifflin-Lab/02-Joiner-Erin/02-Joiner-Erin%3A03-erin-profile-verified-powershell.png)

**Entra audit logs confirmed successful user provisioning and group assignments.**

![Erin audit logs](screenshots/Entra-JML-Dunder-Mifflin-Lab/02-Joiner-Erin/02-Joiner-Erin%3A09-erin-audit-logs.png)

## Mover — Jim Halpert

**Jim’s department and job title were updated from Sales Representative to Assistant Regional Manager.**

![Jim profile after move](screenshots/Entra-JML-Dunder-Mifflin-Lab/03-Mover-Jim/03-Mover-Jim%3A09-jim-profile-after-move.png)

**Jim’s legacy Sales access was removed and Management access was assigned.**

![Jim groups after move](screenshots/Entra-JML-Dunder-Mifflin-Lab/03-Mover-Jim/03-Mover-Jim%3A11-jim-groups-after-move.png)

**Audit logs confirmed the user update, Sales-group removal, and Management-group assignment.**

![Jim audit logs](screenshots/Entra-JML-Dunder-Mifflin-Lab/03-Mover-Jim/03-Mover-Jim%3A15-jim-audit-logs.png)

## Leaver — Ryan Howard

**Ryan’s account was disabled and retained for audit purposes.**

![Ryan disabled account verification](screenshots/Entra-JML-Dunder-Mifflin-Lab/04-Leaver-Ryan/04-Leaver-Ryan%3A07-ryan-account-disabled-verified.png)

**Ryan’s audit trail shows account disablement, session revocation, removal from active groups, and addition to the leaver-hold group.**

![Ryan audit logs](screenshots/Entra-JML-Dunder-Mifflin-Lab/04-Leaver-Ryan/04-Leaver-Ryan%3A15-ryan-audit-logs.png)

## Final Validation

**Final validation confirmed Erin retained Reception access, Jim retained Management access, and Ryan retained only the leaver-hold membership.**

![Final group validation](screenshots/Entra-JML-Dunder-Mifflin-Lab/05-Audit-Logs/05-Final-Validation%3A04-final-group-validation.png)
