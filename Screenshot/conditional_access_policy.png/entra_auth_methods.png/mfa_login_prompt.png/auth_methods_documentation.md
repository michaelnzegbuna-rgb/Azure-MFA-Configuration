# Authentication Strategy Evaluation for Microsoft Entra ID

## Introduction

This document examines the authentication methods enabled within the Microsoft Entra ID environment and explains the rationale behind each selection. Every method is assessed using two primary factors:

* **Security Strength** – the level of protection provided against modern cyber threats.
* **User Experience** – the ease and convenience of the authentication process for end users.

The chosen authentication portfolio supports a Zero Trust security model by balancing strong identity protection with practical usability requirements.

---

## Authentication Methods Summary

| Authentication Method                                        | Security Rating | User Experience | Primary Limitation                        | Recommended Use Case                        |
| ------------------------------------------------------------ | --------------- | --------------- | ----------------------------------------- | ------------------------------------------- |
| Microsoft Authenticator (Push Approval with Number Matching) | High            | High            | Mobile device compromise or session theft | Standard workforce authentication           |
| FIDO2 Security Keys / Passkeys                               | Very High       | Medium          | Loss or theft of the hardware token       | Privileged and administrative accounts      |
| Temporary Access Pass (TAP)                                  | High            | Medium          | Potential social engineering risks        | User onboarding and passwordless enrollment |
| Software OATH Tokens                                         | Moderate        | High            | Vulnerable to phishing attacks            | Alternative authenticator applications      |
| SMS-Based Authentication                                     | Low to Moderate | High            | SIM-swap and interception attacks         | Emergency backup authentication             |
| Email One-Time Passcodes                                     | Low             | High            | Dependence on email account security      | External users and guest access             |

---

# Microsoft Authenticator

## Purpose and Security Benefits

Microsoft Authenticator serves as the primary authentication method for most users across the organization.

One of its strongest security enhancements is the implementation of **number matching**, which was successfully validated during testing. Rather than approving sign-in requests with a single tap, users must enter a code displayed on the sign-in screen. This additional verification step significantly reduces the effectiveness of MFA fatigue attacks and unsolicited approval requests.

The application also provides contextual information during authentication, including:

* The application requesting access
* Geographic location information
* Sign-in details

These indicators help users identify suspicious login attempts before granting approval.

Although the solution offers strong protection against conventional phishing campaigns, advanced adversary-in-the-middle attacks may still succeed if additional protections such as device binding are not implemented.

## User Experience Considerations

From a usability perspective, push notifications provide a fast and intuitive sign-in experience. In situations where internet connectivity is unavailable, the application can generate time-based one-time passwords (TOTP) that allow offline authentication.

The primary challenge is user acceptance, as some individuals may be reluctant to install corporate authentication software on personal devices.

---

# FIDO2 Security Keys and Passkeys

## Purpose and Security Benefits

Passkeys and FIDO2 security keys represent the most secure authentication option available within the environment.

Unlike traditional authentication methods, they rely on public-key cryptography rather than shared secrets. Authentication is cryptographically bound to the legitimate website domain, preventing credentials from being used on fraudulent or phishing websites.

Additional security advantages include:

* Resistance to phishing attacks
* Protection against adversary-in-the-middle attacks
* Private keys never leave the user's device
* Hardware-backed identity verification

Within a Zero Trust architecture, this method provides strong proof of user identity through possession of a trusted device.

## User Experience Considerations

Deployment requires either dedicated hardware tokens or devices equipped with biometric capabilities such as:

* Windows Hello
* Face ID
* Touch ID

Although initial enrollment requires additional effort, daily authentication is extremely fast and convenient once configured.

---

# Temporary Access Pass (TAP)

## Purpose and Security Benefits

Temporary Access Passes provide a secure method for onboarding users into passwordless authentication environments.

Rather than distributing temporary passwords through email or other insecure channels, administrators generate a short-term passcode that enables users to register stronger authentication methods such as:

* Microsoft Authenticator
* FIDO2 Security Keys
* Passkeys

This approach reduces the organization's dependence on traditional passwords and improves overall credential security.

## User Experience Considerations

TAP codes are intentionally short-lived and expire automatically after a predefined period. This minimizes risk if a passcode is intercepted while still providing sufficient time for enrollment activities.

---

# SMS Authentication

## Purpose and Security Benefits

SMS-based authentication delivers a one-time verification code to a registered mobile phone number.

While still widely used, SMS is considered one of the weaker multifactor authentication methods available today due to several known attack vectors, including:

* SIM swapping
* Mobile carrier compromise
* SS7 protocol exploitation
* Phishing attacks targeting verification codes

Because SMS codes can be intercepted or relayed, they do not provide the same level of protection as modern passwordless solutions.

## User Experience Considerations

Despite its security limitations, SMS remains highly accessible because it requires no additional applications, hardware devices, or internet connectivity.

For this reason, it is retained as a secondary recovery mechanism rather than a primary authentication method.

---

# Building a Layered Authentication Strategy

## Security Architecture Approach

The authentication design follows a layered security model where different authentication methods are assigned according to user risk levels.

### Standard Users

Most employees authenticate using Microsoft Authenticator because it provides a strong balance between protection and convenience.

### Privileged Accounts

Administrative accounts require stronger controls and therefore utilize FIDO2 security keys or passkeys due to their superior resistance to phishing attacks.

### User Enrollment

Temporary Access Passes streamline secure onboarding while eliminating the need for temporary passwords.

### Backup Authentication

SMS and email-based verification remain available as contingency methods for account recovery and exceptional access scenarios.

---

# Alignment with Zero Trust Principles

The selected authentication methods support key Zero Trust concepts:

### Continuous Verification

Every authentication request is evaluated independently rather than automatically trusted.

### Risk-Based Decision Making

Sign-in events are assessed using contextual signals such as:

* Device compliance status
* User location
* Sign-in behavior
* Risk indicators generated by Microsoft Entra ID

### Human-Centered Security Controls

Features such as number matching are specifically designed to reduce user error and prevent social engineering attacks by requiring deliberate user interaction during authentication.

---

# Final Assessment

The implemented authentication strategy combines multiple layers of identity protection while maintaining an acceptable user experience. Microsoft Authenticator serves as the primary authentication method for general users, FIDO2 security keys provide maximum protection for privileged accounts, and Temporary Access Passes support secure passwordless onboarding.

Together, these methods establish a resilient identity security framework that aligns with modern Zero Trust principles and significantly strengthens protection against credential theft, phishing, and unauthorized access attempts.
