# Windows Password Policy Implementation Using Group Policy

**Focus:** Windows Server | Active Directory | Group Policy | NIST SP 800-53 | GRC

## Project Overview
This beginner-friendly security governance lab demonstrates how to configure, apply, and validate a Windows password policy using Group Policy. The exercise connects practical Windows administration with NIST SP 800-53 security control concepts, especially **IA-5 (Authenticator Management)** and related **AC-2 (Account Management)** practices.

> **Lab scope:** The password settings below are exercise-specific requirements, **not universal NIST SP 800-53 requirements**. NIST SP 800-53 is a control catalog rather than a fixed Windows password-policy checklist. Modern NIST digital identity guidance generally discourages routine password expiration absent evidence of compromise and favors longer passwords, screening against compromised passwords, and avoiding arbitrary composition rules. This lab illustrates a specified organizational policy, not a claim of full NIST compliance.

## Objective
- Create and link a Group Policy Object (GPO) in an authorized Windows Server lab.
- Configure the required password settings.
- Update Group Policy on a test machine and verify effective policy.
- Test password rejection and record evidence.
- Explain the relevance of IA-5 and AC-2.

## Lab Environment
- Windows Server with Active Directory Domain Services and Group Policy Management (for a domain GPO), or a standalone Windows system with Local Group Policy Editor.
- An authorized test user and a test workstation.
- Administrative privileges to manage the relevant policy.

**Important distinction:** Run `gpmc.msc` to open **Group Policy Management** for domain GPOs. Run `gpedit.msc` to edit **Local Group Policy**. These are different tools. For domain account password policy, configure a GPO linked at the **domain root** (commonly the Default Domain Policy or another appropriately prioritized domain-linked GPO). A GPO linked only to a workstation OU will not normally set the password policy for domain accounts. Fine-grained password policies are another option for different domain user groups.

## Lab Password Policy
| Setting | Lab value | Purpose |
|---|---|---|
| Minimum password length | 12 characters | Require longer passwords in this exercise |
| Password must meet complexity requirements | Enabled | Enforce the lab's composition rule |
| Enforce password history | 5 remembered passwords | Limit immediate reuse |
| Maximum password age | 90 days | Demonstrate an organization-defined expiration rule |

Before applying changes, verify that test accounts and recovery access are ready. Changing minimum length does **not** automatically invalidate existing shorter passwords; it is enforced when passwords are created or changed.

## Implementation
### 1. Open Group Policy Management
1. Sign in to the authorized Windows Server lab.
2. Press **Win + R**, enter `gpmc.msc`, and press Enter.
3. Locate the lab domain and the appropriate domain-linked GPO.
4. Create a new GPO if needed, then link it at the domain root and confirm its precedence. Avoid changing production policy without authorization.

![Group Policy Management and selected GPO](screenshots/01-gpo-overview.png)

### 2. Edit the Password Policy
Right-click the GPO and choose **Edit**. Navigate to:

`Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy`

![Password Policy settings](screenshots/02-password-policy.png)

### 3. Configure the Required Settings
- **Minimum password length:** 12 characters.
- **Password must meet complexity requirements:** Enabled.
- **Enforce password history:** 5 passwords remembered.
- **Maximum password age:** 90 days.

Save the changes and confirm the GPO is linked and applied at the intended scope.

![Minimum password length](screenshots/03-minimum-length.png)

![Complexity and password history](screenshots/04-complexity-history.png)

![Maximum password age](screenshots/05-maximum-age.png)

### 4. Apply and Verify
On the test workstation, open Command Prompt as appropriate and run:

```cmd
gpupdate /force
```

For a domain account policy, verify the effective policy at the domain level, rather than relying on the workstation's Group Policy refresh alone. Useful commands include:

```cmd
net accounts /domain
gpresult /r
```

`net accounts /domain` helps inspect the domain's effective account policy; `gpresult /r` helps identify applied GPOs but does not by itself prove the domain password settings. Replication and policy refresh timing can affect results.

![Group Policy refresh](screenshots/06-gpupdate.png)

### 5. Test the Policy
Using an **authorized disposable test account**, attempt to change the password to a value shorter than 12 characters or one that fails the configured complexity requirement. Record whether Windows rejects it. Then test a compliant password and confirm it is accepted. Avoid recording or publishing actual passwords.

For password-history testing, remember that the setting takes effect as passwords are changed and requires sufficient password history to exist. For maximum-age testing, inspect effective policy rather than waiting 90 days.

![Password policy validation](screenshots/07-password-rejection.png)

## Evidence and Results
> Replace the placeholders below only after completing the lab. Do not present expected results as observations.

| Check | Expected result | Actual result |
|---|---|---|
| GPO linked at domain root | Correct scope and precedence | Pending test |
| Minimum length | 12 characters | Pending test |
| Complexity | Enabled | Pending test |
| Password history | 5 remembered | Pending test |
| Maximum age | 90 days | Pending test |
| Policy update | Completed without relevant errors | Pending test |
| Weak password attempt | Rejected | Pending test |
| Compliant password attempt | Accepted | Pending test |

## NIST SP 800-53 Control Mapping
| Control | Relevance to this lab |
|---|---|
| **IA-5 — Authenticator Management** | Password/authenticator lifecycle, policy management, and protection; strongest direct mapping. |
| **AC-2 — Account Management** | Broader governance of user accounts and account-related processes; password settings alone do not implement the full control. |

**Compliance note:** The configuration does not establish NIST compliance by itself. Actual compliance requires organization-defined parameters, supporting processes, evidence, and assessment against the applicable control baseline and current identity guidance.

## Lessons Learned (complete after testing)
- How a domain-linked GPO differs from local Group Policy.
- How password requirements are defined and applied through Windows security policy.
- How to validate policy application instead of assuming `gpupdate` alone proves enforcement.
- How to map technical configuration evidence to IA-5 and related AC-2 governance.
- Why policy settings must be evaluated against current standards and organizational risk requirements.

## Repository Structure
```text
Windows-Password-Policy-GPO-NIST-800-53/
├── README.md
└── screenshots/
    ├── 01-gpo-overview.png
    ├── 02-password-policy.png
    ├── 03-minimum-length.png
    ├── 04-complexity-history.png
    ├── 05-maximum-age.png
    ├── 06-gpupdate.png
    └── 07-password-rejection.png
```

## References
- [NIST SP 800-53 Rev. 5 — Security and Privacy Controls](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final)
- [NIST SP 800-63B — Digital Identity Guidelines: Authentication and Lifecycle Management](https://pages.nist.gov/800-63-4/sp800-63b.html)
- [Microsoft Learn — Password Policy](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/password-policy)

## Disclaimer
This is an educational lab project. Use only authorized test systems and redact sensitive information from screenshots.
