# Azure Multi-Factor Authentication (MFA) Configuration Program

Welcome to the **Azure MFA Configuration Learning Program** repository. In modern cloud environments, identity has become the primary security perimeter. This project demonstrates how to strengthen cloud security by implementing and configuring Multi-Factor Authentication (MFA) within Microsoft Azure Active Directory (now **Microsoft Entra ID**), adhering to the principles of Zero Trust and Defense in Depth.

---

## 📋 Table of Contents
1. [Project Overview & Goals](#-project-overview--goals)
2. [Documentation Index](#-documentation-index)
3. [Configuration Highlights & Verification](#-configuration-highlights--verification)
4. [Design Justification Summary](#-design-justification-summary)
5. [Key Troubleshooting Scenarios](#-key-troubleshooting-scenarios)

---

## 🎯 Project Overview & Goals

This project provides hands-on implementation details for securing cloud identities using advanced authentication mechanisms, replacing insecure password-only authentication.

### Core Goals:
*   **Establish Identity as the Security Perimeter**: Enforcing strong verification at the boundary of all cloud transactions.
*   **MFA Configuration**: Deploying tenant-wide authentication methods in Microsoft Entra ID.
*   **Conditional Access (CA) Implementation**: Designing policies that enforce MFA based on real-time signals (user risk, location, device compliance).
*   **Self-Service Enrollment**: Verifying the user onboarding flow and registration of secondary verification factors.
*   **Operational Resilience**: Troubleshooting common deployment issues and documenting resolution steps.

---

## 🗂️ Documentation Index

The repository is structured into the following detailed markdown reports:

*   📄 **[Summary Report (Step-by-Step Configuration)](./summary_report.md)**: Walkthrough of administrative configurations in the Microsoft Entra admin center, user creation, enrollment, and testing.
*   📄 **[Authentication Methods & Justifications](./auth_methods_documentation.md)**: Analysis of supported authentication factors (Authenticator App, FIDO2 Security Keys, SMS) with security and usability trade-offs.
*   📄 **[Troubleshooting & Diagnostics Log](./troubleshooting_log.md)**: A collection of real-world MFA issues, root cause analyses, and their resolved states.

---

## 🖼️ Configuration Highlights & Verification

Below are key verification screenshots demonstrating the configuration and login flow:

### 1. Entra ID Authentication Methods
The central policies page showing the tenant's permitted authentication methods, ensuring SMS is restricted and passwordless/push methods are prioritized.


![Microsoft Entra ID Authentication Methods Policies](./screenshots/entra_auth_methods.png)
<img width="1908" height="976" alt="entra_auth_methods" src="https://github.com/user-attachments/assets/d5f72edb-f2aa-4bb9-a77f-96094bdc7747" />

### 2. Conditional Access Policy Design
A granular Conditional Access policy configured to prompt for MFA whenever a user attempts to access any cloud resource from external networks or with administrative roles.

![Conditional Access Policy UI](./screenshots/conditional_access_policy.png)
<img width="1912" height="1020" alt="conditional_access_policy" src="https://github.com/user-attachments/assets/2e6fc56b-0a5f-48e7-bc84-adef2fd92408" />

### 3. User Self-Service Security Registration
The end-user configuration portal (`mysignins.microsoft.com`) verifying successful registration of secondary factors (Microsoft Authenticator App on iPhone 12 Pro).

![End-User Security Info Dashboard](./screenshots/user_mfa_registration.png)
<img width="1917" height="1016" alt="user_mfa_registration" src="https://github.com/user-attachments/assets/49feec75-c81e-4938-8677-534dde231b59" />

### 4. Verification Prompt During Registration
The setup verification flow displaying the "Let's try it out" screen with the verification code (64) during Microsoft Authenticator onboarding.

![MFA Number Matching Onboarding Prompt](./screenshots/mfa_login_prompt.png)
<img width="1918" height="1022" alt="mfa_login_prompt" src="https://github.com/user-attachments/assets/9bae1a6a-cb62-426e-a1ac-3e05d97a50ab" />

---

## 🛡️ Design Justification Summary
This implementation follows a **Zero Trust** strategy by selecting **Microsoft Authenticator (Push Notifications with Number Matching)** as the primary verification factor. 
*   **Security**: Mitigates prompt-bombing (MFA fatigue) attacks by requiring the user to match a 2-digit code shown on the screen.
*   **Usability**: Allows users to approve requests with a single tap, eliminating manual entry of 6-digit codes.
*   *For a complete security vs. usability comparison of other methods (FIDO2, SMS, OTP), see the full [Authentication Methods Documentation](./auth_methods_documentation.md).*

---

## 🔧 Key Troubleshooting Scenarios
The project logs and resolves three common administrative issues:
1.  **Registration Policy Conflicts**: Users blocked from registering MFA when off-site due to over-restrictive setup policies.
2.  **MFA Fatigue Bypass**: Blocking prompt-bombing attempts by enforcing number-matching across the tenant.
3.  **Authenticator App Sync Issues**: Time-drift errors on mobile devices causing One-Time Passcodes (OTP) to fail validation.
*   *For detailed diagnostic steps and log outputs, see the [Troubleshooting Log](./troubleshooting_log.md).*
