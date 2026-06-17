# Microsoft Entra ID Multi-Factor Authentication (MFA) Deployment and Validation Report

## Overview

This document outlines the configuration, implementation, and testing of Multi-Factor Authentication (MFA) within the Microsoft Entra ID tenant **`olamc.onmicrosoft.com`**. The objective was to strengthen account security by enabling modern authentication methods, creating a test user, enforcing Conditional Access policies, and validating the end-user MFA experience from enrollment through sign-in.

---

## 🌐 Phase 1: Accessing the Microsoft Entra Administration Portal

The MFA configuration process began by accessing the Microsoft Entra administrative interface.

### Procedure

1. Open a web browser and navigate to the Microsoft Entra Admin Center (`https://entra.microsoft.com`).
2. Sign in using the tenant administrator account:

   * **[michaelnzegbuna@nzemikez.onmicrosoft.com](mailto:michaelnzegbuna@nzemikez.onmicrosoft.com)**
3. After authentication, use the left-hand navigation menu to access identity, user, and security management features.

This portal serves as the centralized location for configuring authentication methods, Conditional Access policies, and user security settings.

---

## 🔐 Phase 2: Configuring Authentication Methods

To support secure and flexible user authentication, multiple verification methods were enabled through the Authentication Methods policy.

### Configuration Path

**Identity → Protection → Authentication Methods → Policies**

### Enabled Authentication Methods

| Authentication Method         | Availability | Purpose                                                            |
| ----------------------------- | ------------ | ------------------------------------------------------------------ |
| Microsoft Authenticator       | All Users    | Primary MFA method using push notifications and number matching    |
| Passkeys (FIDO2)              | All Users    | Passwordless authentication using hardware or platform credentials |
| SMS Verification              | All Users    | Backup authentication via text message                             |
| Temporary Access Pass (TAP)   | All Users    | Temporary credentials for onboarding and account recovery          |
| Software OATH Tokens          | All Users    | Time-based one-time passcodes from authenticator applications      |
| Email One-Time Passcode (OTP) | All Users    | Secondary verification method delivered via email                  |

### Outcome

All selected authentication methods were activated successfully and made available tenant-wide. The configuration provides multiple recovery and verification options while maintaining strong security controls.

---

## 👤 Phase 3: Creating a Validation User Account

A dedicated test account was provisioned to validate registration and MFA enforcement workflows.

### User Configuration

| Setting             | Value                                  |
| ------------------- | -------------------------------------- |
| User Principal Name | `testusermfa@nzemikez.onmicrosoft.com` |
| Display Name        | `test userMFA`                         |
| Password            | Automatically generated                |
| Usage Location      | United States                          |
| License Assigned    | Microsoft Entra ID P2                  |

### Deployment Steps

1. Navigate to:

   **Identity → Users → All Users → New User**

2. Create a new cloud-only user account.

3. Assign the required attributes and location settings.

4. Allocate a Microsoft Entra ID P2 license to enable Conditional Access capabilities.

5. Save and create the account.

### Result

The user account was created successfully and became available for MFA registration and policy testing.

---

## 🛡️ Phase 4: Implementing Conditional Access Enforcement

A Conditional Access policy was created to require MFA during sign-in rather than relying on legacy per-user MFA settings.

### Configuration Path

**Identity → Protection → Conditional Access → Policies**

### Policy Details

| Setting          | Configuration                          |
| ---------------- | -------------------------------------- |
| Policy Name      | `CA001: Enforce MFA`                   |
| Target Users     | `testusermfa@nzemikez.onmicrosoft.com` |
| Target Resources | All Resources                          |
| Grant Control    | Require Multi-Factor Authentication    |
| Policy State     | Enabled                                |

### Configuration Process

1. Create a new Conditional Access policy.
2. Select the designated test account as the target user.
3. Apply the policy to all cloud resources.
4. Configure the grant requirement to enforce MFA.
5. Enable and save the policy.

### Security Benefit

This approach ensures authentication requirements are evaluated dynamically and consistently across applications while supporting Microsoft's Zero Trust security framework.

---

## 📲 Phase 5: User Registration and MFA Enrollment

The next stage involved enrolling the test account in Microsoft Authenticator and registering MFA methods.

### Enrollment Procedure

1. Open a private browser session.

2. Navigate to:

   `https://mysignins.microsoft.com/security-info`

3. Sign in using the test account credentials.

4. After authentication, the user receives a prompt requesting additional security information.

5. Select **Microsoft Authenticator** as the preferred authentication method.

6. Install Microsoft Authenticator on the mobile device used for testing (**iPhone 12 Pro**).

7. Scan the QR code presented by the registration wizard.

8. Complete the verification challenge by entering the displayed number into the mobile application.

### Verification Example

During enrollment, the setup wizard displayed a number-matching challenge code:

```
64
```

Entering the same number in the Microsoft Authenticator application successfully verified device ownership and completed registration.

### Result

The Authenticator method was registered successfully and appeared in the user's Security Information profile.

---

## 🧪 Phase 6: MFA Authentication Testing

Following enrollment, a complete authentication test was performed to verify policy enforcement and user experience.

### Test Procedure

1. Launch a new Incognito or Private browsing session.

2. Navigate to:

   `https://portal.azure.com`

3. Sign in as:

   `testusermfa@olamc.onmicrosoft.com`

4. Enter the account password.

5. Observe the Conditional Access policy trigger an MFA challenge.

6. Review the two-digit verification number displayed during sign-in.

7. Open the Microsoft Authenticator notification on the registered mobile device.

8. Enter the matching verification number and approve the request.

### Expected Outcome

* MFA challenge appears after password authentication.
* Authenticator receives the push notification.
* Number matching is completed successfully.
* User gains access to the Azure Portal.

### Result

The sign-in process completed successfully, confirming that:

* Conditional Access policy enforcement was working correctly.
* Microsoft Authenticator was functioning as intended.
* Number matching verification was operational.
* MFA-protected access to Azure resources was successfully established.

---

## ✅ Conclusion

The Microsoft Entra ID tenant was successfully configured with multiple authentication methods and a Conditional Access policy requiring Multi-Factor Authentication. A dedicated test account was created, enrolled in Microsoft Authenticator, and used to validate the complete MFA sign-in workflow.

The deployment demonstrates effective implementation of modern identity security practices by combining Conditional Access, Microsoft Authenticator number matching, and passwordless-ready authentication methods. This configuration significantly improves protection against credential theft, phishing attacks, and unauthorized account access while maintaining a user-friendly authentication experience.
