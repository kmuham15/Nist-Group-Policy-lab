# Windows Password Policy Implementation Using Group Policy

## Objective
- Strengthened password security by configuring minimum password requirements.
- Enabled password complexity to improve account protection.
- Enforced password history to prevent immediate password reuse.
- Configured password expiration to support security compliance.
- Applied and updated Group Policy settings to enforce security requirements.
- Validated password policy enforcement through testing.
- Aligned technical security configurations with NIST SP 800-53 controls to demonstrate practical GRC implementation.


## 1. Enforcing Minimum Password Length
1. Sign in to your Windows Server lab with administrator privileges.
2. Press Win + R, type gpedit.msc, and press Enter.
3. Navigate to:
  ```spl
 Computer Configuration → Windows Settings → Security Settings → Account Policies → Password Policy
```
4. Double-click Minimum password length.
5. Set the minimum password length to 14 characters.
6. Click Apply, then OK to save the configuration.
7. Open Command Prompt as Administrator and run:

```spl
gpupdate /force
```
<img width="1376" height="715" alt="Windows Server Password Policy Settings (1)" src="https://github.com/user-attachments/assets/8e4f6d4b-a65b-4f66-860b-5325c36ed39c" />

  
## 2. Edit the Password Policy
Enabled 
"Password must meet complexity requirements" to enforce stronger password standards, prevent weak password creation, and enhance account security against unauthorized access.


<img width="1314" height="829" alt="Windows 11 Password Policy Settings" src="https://github.com/user-attachments/assets/7ac2e8bc-45e8-4c82-94a0-7cd5519c1b14" />



## 3. Enforcing Password History

Configured Windows Group Policy to remember the 5 most recent passwords, preventing users from immediately reusing previous credentials and strengthening overall account security.

<img width="895" height="905" alt="Windows Password Policy Settings Dialog" src="https://github.com/user-attachments/assets/7c05fbb7-05fa-4187-a9a3-4e303da46896" />


## 4. Enforcing Maximum Password Age

Configured Windows Group Policy to enforce a 90-day maximum password age, requiring users to update their passwords after the specified period to support password lifecycle management and account security.

For a domain account policy, verify the effective policy at the domain level, rather than relying on the workstation's Group Policy refresh alone. Useful commands include:

<img width="763" height="824" alt="Windows 11 Password Age Settings" src="https://github.com/user-attachments/assets/310debc5-8442-4188-b422-f01101c8d3f2" />

## 5. Applying the Updated Group Policy

After configuring the password security policies, I opened Command Prompt with administrator privileges and executed:

```spl
gpupdate /force
```

This command refreshed the Group Policy settings to apply the latest security configurations.

Both Computer Policy and User Policy updates completed successfully, confirming that the policy refresh was processed without errors.

<img width="677" height="383" alt="Screenshot 2026-10-27 184702" src="https://github.com/user-attachments/assets/339b8cad-2241-4f8d-96eb-c7adbd890abf" />

## 6. Testing and Validating Password Policy Enforcement

After applying the updated Group Policy settings, I used a dedicated test account named `PolicyTest` to evaluate password policy enforcement.

I executed the following command to initiate password changes:

```
net user PolicyTest *
```

This testing process helped validate whether the configured password security requirements were actively enforced, rather than simply applied within Group Policy.


## 7. Weak Password Validation Test

Attempted to set a password that failed to meet the configured security requirements.

Windows successfully rejected the password and displayed a policy violation message, confirming that the password security controls were actively enforced and functioning as intended.

<img width="1644" height="888" alt="Windows 11 Administrator Command Prompt" src="https://github.com/user-attachments/assets/47d35e16-4e19-4cff-ac83-23d84d6b3d61" />

## 8. Strong Password Validation Test

Repeated the password validation test using a password that met all configured security requirements.

Windows successfully accepted the password and displayed the confirmation message:

`The command completed successfully`

This verified that the password policy was functioning as intended, allowing compliant passwords while rejecting those that failed to meet the established security standards.

<img width="1635" height="856" alt="Windows 11 Administrator Command Prompt Session" src="https://github.com/user-attachments/assets/55c0239d-ff05-4073-bad5-5da6d2c601af" />

## 9. NIST 800-53 Control Mapping

 AC-2 – Account Management

NIST 800-53 AC-2 focuses on the administration, monitoring, and protection of system accounts.

The password policies configured in this lab complement account management practices by strengthening authentication requirements and reducing the risk of unauthorized account access.

IA-5 – Authenticator Management

NIST 800-53 IA-5 addresses the secure management of authentication credentials, including passwords.

This lab demonstrated the practical implementation of authenticator management controls by enforcing password complexity, establishing minimum password lengths, restricting password reuse, and configuring password expiration policies to strengthen account security.

## Validation Results

This lab successfully demonstrated the security control implementation lifecycle:

Configure → Apply → Test → Validate

 Key Outcomes

- Successfully established a 14-character minimum password length.
- Enabled password complexity requirements to strengthen authentication security.
- Enforced password history to prevent reuse of the previous 5 passwords.
- Configured a 90-day maximum password age.
- Successfully applied updated security settings using Group Policy.
- Verified that weak passwords were rejected for failing security requirements.
- Confirmed that compliant passwords were accepted.
- Validated that the configured password security controls operated as intended.

These results demonstrated the successful implementation and testing of password security policies while reinforcing practical knowledge of NIST 800-53 security control implementation and validation.

## Key Takeaways

This lab provided valuable hands-on experience in translating **NIST 800-53 security requirements into practical Windows Server configurations**.

Rather than focusing solely on security policies and compliance frameworks, I implemented password security controls, tested their effectiveness, and verified that they operated as intended.

Throughout this lab, I strengthened my skills in:

- Windows Group Policy administration
- Password policy configuration and enforcement
- Authentication and account security
- Security control implementation and validation
- Windows command-line administration
- Microsoft Azure Windows Server management
- NIST 800-53 security control mapping
- Governance, Risk, and Compliance (GRC)

**My biggest takeaway** Implementing a security control is only part of the process. Effective security requires continuous testing, validation, and documented evidence to ensure controls are functioning as intended.

This lab reinforced my understanding of how technical security measures support organizational security policies, risk management, and compliance objectives.
