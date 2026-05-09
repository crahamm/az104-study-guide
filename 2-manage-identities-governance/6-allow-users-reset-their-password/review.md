# Self-Service Password Reset - Study Review

## Core Idea

Microsoft Entra self-service password reset (SSPR) lets users reset forgotten or expired passwords without help-desk intervention. SSPR reduces administrator workload and helps users regain access to Microsoft Entra ID, Microsoft 365, Azure, and apps that use Microsoft Entra ID for authentication.

This module maps to `Manage Microsoft Entra users and groups`, specifically `Configure self-service password reset (SSPR)`.

## Key Capabilities

- Enable SSPR for no users, selected users, or all users.
- Require one or two authentication methods.
- Choose allowed authentication methods.
- Require users to register authentication information.
- Configure password reset notifications.
- Customize helpdesk contact information and sign-in branding.
- Support password writeback in hybrid environments.

## How SSPR Works

A user starts reset from the password reset portal or the `Can't access your account` link.

SSPR flow:

- `Localization`: portal uses the browser locale.
- `Verification`: user enters username and completes CAPTCHA.
- `Authentication`: user proves identity using configured methods.
- `Password reset`: user enters and confirms a new password.
- `Notification`: user receives confirmation.

A user is considered registered for SSPR after registering at least the number of authentication methods required by the policy.

## Authentication Methods

SSPR authentication methods include:

- `Mobile app notification`
- `Mobile app code`
- `Email`
- `Mobile phone`
- `Office phone`
- `Security questions`

Recommendations:

- Enable at least two methods.
- Prefer Microsoft Authenticator notification or code as a primary method.
- Also enable email or office phone for users without mobile devices.
- Avoid relying on mobile phone SMS as a primary method because SMS can be abused.
- Use security questions only with another method because answers might be known or guessed.

Trial Microsoft Entra organizations do not support phone call options.

## Administrator Accounts

Accounts associated with administrator roles are protected by stronger SSPR requirements.

Important points:

- A strong two-method authentication policy always applies to administrator accounts.
- This admin requirement applies regardless of the configuration for other users.
- Security questions are not available for accounts associated with administrator roles.

## Notifications

Notification options:

- `Notify users on password resets`: sends email to the user's primary and secondary email addresses.
- `Notify all admins when other admins reset their password`: alerts administrators when an administrator resets their password.

These notifications help detect suspicious resets.

## Licensing And Hybrid Writeback

Signed-in users can change their password regardless of Microsoft Entra edition.

SSPR for users who cannot sign in because they forgot their password or it expired requires a supported paid license such as:

- Microsoft Entra ID `P1`
- Microsoft Entra ID `P2`
- Microsoft 365 Apps for business
- Microsoft 365

Hybrid password writeback writes cloud password changes back to on-premises Active Directory. Password writeback is supported with Microsoft Entra ID P1 or P2 and supported Microsoft 365 licensing.

SSPR with password writeback can be deployed with:

- `Microsoft Entra Connect`
- `Cloud sync`

You can use both side by side in different domains. Cloud sync can provide higher availability because it does not depend on a single Microsoft Entra Connect instance.

## Configure SSPR

Prerequisites:

- Microsoft Entra organization with P1 or P2 trial/license.
- Account with `Authentication Policy Administrator`.
- Non-administrative test user.
- Security group for a limited rollout.

Enablement options for `Self-service password reset enabled`:

- `None`: no users can use SSPR. This is the default.
- `Selected`: only members of a selected security group can use SSPR.
- `All`: all users in the Microsoft Entra organization can use SSPR.

Configuration areas:

- `Properties`: enable SSPR and choose scope.
- `Authentication methods`: choose required method count and allowed methods.
- `Registration`: require registration and set reconfirmation frequency.
- `Notifications`: choose user and admin notifications.
- `Customization`: add helpdesk email or URL.

## Directory Branding

Company branding helps users recognize the legitimate sign-in and password reset experience.

Branding requirements from the exercise:

- Background image: PNG or JPG, `1920 x 1080`, smaller than `300 KB`.
- Logo/favicon image: PNG or JPG, `32 x 32`, smaller than `5 KB`.

Configure branding in `Microsoft Entra ID` > `Company branding`.

## When To Use

- Use SSPR to reduce password reset help-desk volume.
- Use `Selected` rollout for pilot groups.
- Use `All` after testing is complete.
- Use password writeback when cloud resets must update on-premises Active Directory.
- Use Authenticator app methods when stronger reset authentication is needed.
- Use branding when users need confidence that the sign-in page is legitimate.

## When Not To Use

- Do not enable SSPR for everyone before testing with a selected group.
- Do not use security questions alone for strong reset authentication.
- Do not use an administrative account as the only SSPR test account.
- Do not expect free or pay-as-you-go-only tenants to provide full SSPR capability.
- Do not forget to configure password writeback for hybrid users who authenticate against on-premises AD.

## Exam Triggers

- Forgotten or expired password without help desk: `SSPR`.
- Pilot rollout: `Selected` plus a security group.
- No SSPR for any users: `None`.
- Tenant-wide SSPR: `All`.
- Configure SSPR: `Microsoft Entra ID` > `Password reset`.
- SSPR setup portal: `https://aka.ms/ssprsetup`.
- SSPR reset portal: `https://aka.ms/sspr`.
- Required setup count met: user is registered for SSPR.
- Admin account SSPR: always requires two strong methods.
- Security questions for admins: not available.
- Hybrid cloud reset updates on-prem AD: password writeback.
- Password writeback deployment tools: `Microsoft Entra Connect` or `cloud sync`.
- SSPR configuration role: `Authentication Policy Administrator`.
- User reassurance on sign-in page: Microsoft Entra company branding.

## Knowledge Check Answers

1. A user is registered for SSPR when they have registered at least the number of methods required to reset a password.
2. When SSPR is enabled, users can reset their passwords when they cannot sign in.
