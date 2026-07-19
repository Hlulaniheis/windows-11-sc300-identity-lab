```markdown
# Windows 11 SC-300 Identity & Access Management Lab

[![SC-300](https://img.shields.io/badge/SC--300-Identity%20%26%20Access%20Administrator-blue)](https://learn.microsoft.com/en-us/certifications/exams/sc-300/)
[![Entra ID](https://img.shields.io/badge/Entra%20ID-P2-green)](https://www.microsoft.com/en-us/security/business/identity-access/azure-active-directory-pricing)
[![Intune](https://img.shields.io/badge/Intune-Plan%201-orange)](https://www.microsoft.com/en-us/microsoft-365/enterprise-mobility-security/microsoft-intune)

## Overview

This repository documents a complete hands-on lab environment for the **Microsoft SC-300 (Identity and Access Administrator Associate)** certification. The lab is built on a production-like Entra ID tenant with an Intune-enrolled Windows 11 VM, demonstrating core identity governance skills required for the exam.

> **Lab Completed:** July 2026
> **Duration:** ~2-3 hours
> **Tenant:** Lani644.onmicrosoft.com

## What This Lab Demonstrates

| Category | Implemented Features |
|----------|---------------------|
| **Conditional Access** | MFA registration, User risk remediation (High risk → password reset), Sign-in risk (Medium/High → MFA), Device compliance enforcement |
| **Identity Protection** | Risk-based policies using Entra ID Protection signals |
| **Privileged Identity Management (PIM)** | Just-in-time Global Administrator access with MFA and justification |
| **Entitlement Management** | Self-service access packages with approval workflows and expiration |
| **Access Reviews** | Automated group membership reviews with auto-apply and removal |
| **Emergency Access** | Break-glass accounts excluded from all Conditional Access policies |
| **Device Management** | Windows 11 VM enrolled in Intune, marked compliant |

## Lab Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                     Lani644.onmicrosoft.com                     │
├─────────────────────────────────────────────────────────────────┤
│  ┌───────────────────────────────────────────────────────────┐ │
│  │              Conditional Access Policies                  │ │
│  │  ┌─────────────────────┐  ┌──────────────────────────┐  │ │
│  │  │ MFA Registration    │  │ Risk-Based Policies       │  │ │
│  │  │ Policy              │  │ (User & Sign-in Risk)    │  │ │
│  │  └─────────────────────┘  └──────────────────────────┘  │ │
│  └───────────────────────────────────────────────────────────┘ │
│  ┌───────────────────────────────────────────────────────────┐ │
│  │              Identity Governance                          │ │
│  │  ┌─────────────────────┐  ┌──────────────────────────┐  │ │
│  │  │ Access Reviews      │  │ Entitlement Management   │  │ │
│  │  │ (Group Membership)  │  │ (Access Packages)        │  │ │
│  │  └─────────────────────┘  └──────────────────────────┘  │ │
│  └───────────────────────────────────────────────────────────┘ │
│  ┌───────────────────────────────────────────────────────────┐ │
│  │              Identity Protection                         │ │
│  │  ┌─────────────────────┐  ┌──────────────────────────┐  │ │
│  │  │ User Risk Policy    │  │ Sign-in Risk Policy      │  │ │
│  │  │ (High Risk =        │  │ (Med/High Risk =         │  │ │
│  │  │  Remediation)       │  │  MFA Required)          │  │ │
│  │  └─────────────────────┘  └──────────────────────────┘  │ │
│  └───────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

## Lab Environment

| Component | Detail |
|-----------|--------|
| **Tenant** | Lani644.onmicrosoft.com |
| **Tenant ID** | 4bde1fe0-b5ee-4aa7-9a8b-76661b68ecf7 |
| **Admin User** | hlulanichavalala@lani644.onmicrosoft.com |
| **Licenses** | Entra ID P2 (Trial), Intune Plan 1 (Trial) |
| **Enrolled Device** | Windows 11 VM (Compliant) |
| **Conditional Access Policies** | 4 policies (all active) |

## Conditional Access Policies

| Policy Name | State | Grant Controls | Conditions |
|-------------|-------|----------------|------------|
| **Require-Compliant-Devices** | ✅ **ON** | Require compliant device, Require hybrid joined device | All users, All resources |
| **Policy-01-Require-MFA-Registration** | ✅ **ON** | Require MFA registration | All users, All resources |
| **Policy-02-User-Risk-Remediation** | ✅ **ON** | Require MFA, Require password change | All users, All resources, User risk: High |
| **Policy-03-Signin-Risk-MFA** | ✅ **ON** | Require MFA | All users, All resources, Sign-in risk: Medium + High |

## Emergency Access Configuration

| Component | Details |
|-----------|---------|
| **Break-glass Accounts** | breakglass1@lani644.onmicrosoft.com, breakglass2@lani644.onmicrosoft.com |
| **Emergency Group** | Emergency-Access-Admins (both break-glass accounts as members) |
| **Exclusion** | Excluded from ALL Conditional Access policies ✅ |
| **Role** | Global Administrator (both accounts) |

## Privileged Identity Management (PIM)

| Setting | Value |
|---------|-------|
| **Role** | Global Administrator |
| **Assignment Type** | Eligible (not permanently active) |
| **Activation Duration** | 2 hours |
| **MFA Required** | Yes |
| **Justification Required** | Yes |
| **Approval Required** | No (lab simplified) |

## Entitlement Management

| Component | Details |
|-----------|---------|
| **Catalog** | Project-SC300-Lab-Catalog |
| **Access Package** | Access-Package-SC300-Lab |
| **Resource** | SC300-Lab-Users (Security Group) |
| **Approval** | Required (HULANI CHAVALALA as approver) |
| **Expiration** | 09/09/2026 |

## Access Reviews

| Setting | Value |
|---------|-------|
| **Review Name** | Access-Review-SC300-Lab-Users |
| **Resource** | SC300-Lab-Users group |
| **Reviewers** | Group owner(s) |
| **Fallback Reviewers** | HULANI CHAVALALA |
| **Frequency** | One-time (7 days) |
| **Auto-apply Results** | Enabled |
| **If Reviewers Don't Respond** | Remove access |

## Repository Structure

```
windows-11-sc300-identity-lab/
├── README.md                         # This file
├── screenshots/
│   ├── README.md                     # Screenshot index
│   ├── 01-existing-compliant-devices-policy.png
│   ├── 02-licenses-entra-id-p2-intune.png
│   ├── 03-tenant-overview.png
│   ├── ... (54 screenshots total)
│   └── 54-final-all-policies-on.png
├── scripts/
│   ├── Get-ConditionalAccessPolicySummary.ps1
│   └── Invoke-SC300LabCheck.ps1
└── templates/
    ├── ConditionalAccessPolicies.json
    └── PIMSettings.json
```

## Skills Validated

| SC-300 Objective | Lab Component | Weight |
|------------------|---------------|--------|
| Implement MFA | MFA Registration Policy, Authentication Methods | 25-30% |
| Conditional Access | Risk-based policies, compliance check | 25-30% |
| Identity Protection | User/Sign-in risk policies | Included in CA |
| Entitlement Management | Access packages, catalogs | 15-20% |
| Access Reviews | Group and guest reviews | 15-20% |
| PIM | Azure AD role assignments | 10-15% |

## PowerShell Validation Script

A validation script is included in `/scripts/Invoke-SC300LabCheck.ps1` to verify your lab configuration:

```powershell
# Connect to Microsoft Graph
Connect-MgGraph -Scopes "Policy.Read.All", "RoleManagement.Read.All"

# Run lab validation
.\Invoke-SC300LabCheck.ps1
```

Expected output:
```
=== SC-300 Lab Validation ===

Conditional Access Policies:
  - Require-Compliant-Devices: On
  - Policy-01-Require-MFA-Registration: On
  - Policy-02-User-Risk-Remediation: On
  - Policy-03-Signin-Risk-MFA: On

PIM Eligible Assignments:
  - HULANI CHAVALALA: Global Administrator (Eligible)

=== Validation Complete ===
```

## Screenshots

All lab configuration screenshots are available in the `/screenshots` folder with detailed descriptions in `/screenshots/README.md`.

| Key Screenshot | Description |
|----------------|-------------|
| `01-existing-compliant-devices-policy.png` | Existing Conditional Access policy |
| `15-four-ca-policies.png` | All 4 Conditional Access policies |
| `32-pim-active-role.png` | PIM role activated |
| `54-final-all-policies-on.png` | Final state - all policies ON |

## How to Replicate This Lab

### Prerequisites

- Entra ID P2 license (trial available)
- Intune Plan 1 license (trial available)
- Global Administrator access
- Windows 11 VM (optional but recommended)

### Quick Start Steps

1. **Review existing configuration** - Document your tenant baseline
2. **Create MFA Registration Policy** - All users must register for MFA
3. **Create User Risk Policy** - High user risk → MFA + password reset
4. **Create Sign-in Risk Policy** - Medium/High sign-in risk → MFA
5. **Create Break-glass Accounts** - Emergency access accounts excluded from all policies
6. **Configure PIM** - Make Global Admin role eligible (not active)
7. **Create Access Package** - Self-service access with approval workflow
8. **Create Access Review** - Scheduled group membership reviews

## Security Considerations

| Consideration | Implementation |
|---------------|----------------|
| **Tenant Lockout Prevention** | Break-glass accounts excluded from all policies ✅ |
| **Just-in-Time Admin** | PIM with MFA and justification ✅ |
| **Risk-based Access** | User and sign-in risk policies ✅ |
| **Device Trust** | Intune compliance enforced ✅ |
| **Access Governance** | Access reviews and entitlements ✅ |

## Resources

- [Microsoft SC-300 Exam Guide](https://learn.microsoft.com/en-us/certifications/exams/sc-300/)
- [Microsoft Entra ID Documentation](https://learn.microsoft.com/en-us/entra/identity/)
- [Conditional Access Documentation](https://learn.microsoft.com/en-us/entra/identity/conditional-access/)
- [Microsoft Intune Documentation](https://learn.microsoft.com/en-us/mem/intune/)

## Important Notes

> **License Warning:** This lab was built using trial licenses. After the trial period expires, some features may be disabled.

> **Guest User Billing:** Beginning January 15, 2026, a linked Azure subscription is required to use Entra ID Governance features for guest users. This lab does not include guest users, so billing is not impacted.

> **Break-glass Accounts:** Store break-glass account passwords securely offline. They are critical for tenant recovery.

## License

This project is for educational purposes as part of SC-300 certification preparation. All Microsoft screenshots are property of Microsoft Corporation.

## Author

**HULANI CHAVALALA**


```
