# Support-Ticket---IT-0001-Compromised-Account-Containment
This incident-response ticket is a high-priority identity security event in Microsoft Entra ID. A Client Services employee, David Cho, reported that his company laptop and corporate phone were stolen from his vehicle overnight.

Because both devices were already authenticated to the organization, the primary risk was not only future password-based sign-in attempts, it was also the possibility that existing sessions could provide immediate access to Microsoft 365 resources such as email, Teams, OneDrive, SharePoint, client data, and internal applications.

The objective was to rapidly contain the account compromise by invalidating active sessions, disabling the user account, and requiring fresh MFA enrollment once the user’s identity could be verified.

Ticket Details:

| Field          | Value                                                                                        |
| -------------- | -------------------------------------------------------------------------------------------- |
| Ticket ID      | IT-0001                                                                                      |
| Status         | Resolved / Contained                                                                         |
| Priority       | Critical                                                                                     |
| Category       | Identity and Access Management / Security Incident                                           |
| Platform       | Microsoft Entra ID                                                                           |
| Affected User  | David Cho                                                                                    |
| Reported Issue | Corporate laptop and mobile phone stolen while signed in to the employee’s corporate account |
| Business Risk  | Unauthorized access to email, client files, collaboration tools, and internal systems        |
| Assigned To    | IT Support / Security Operations                                                             |

Incident Scenario:

At approximately 8:47 AM, the security team received notification that David Cho’s company-issued laptop and phone had been stolen. Both devices were actively signed into David’s corporate Microsoft 365 account.

An attacker in possession of the devices could potentially access sensitive business information through existing authentication tokens or active sessions, even without immediately knowing the user’s password. Since the mobile device also contained the user’s authenticator application, its MFA registration could no longer be considered trusted.

This incident required immediate identity containment.

Objectives:

The response followed three containment priorities:

Revoke all active sessions to invalidate existing authentication tokens on the stolen devices.

Disable the account to prevent new sign-ins, including sign-ins using a potentially compromised password.

Require MFA re-registration so the stolen phone could no longer serve as a trusted authentication factor.

Actions Performed:

1. Located the affected user
I signed in to the Microsoft Entra admin center using an authorized support account and navigated to:

Microsoft Entra admin center
→ Users
→ All users
→ Search: David Cho
I opened David Cho’s user profile to review and manage his identity security settings.

2. Revoked active sessions
From the user’s profile, I selected Revoke sessions and confirmed the action.

This was the first containment action because active sessions may remain valid on devices that are already authenticated. Revoking sessions invalidates refresh tokens and forces reauthentication across Microsoft 365 services.

This reduced the immediate risk of continued access to:

Outlook and Exchange Online email

Microsoft Teams

OneDrive and SharePoint files

Microsoft 365 applications

Enterprise applications integrated with Entra ID

Other resources protected by the user’s Microsoft identity

3. Disabled account sign-in
From David Cho’s Overview page, I located the Account status section and edited the account configuration.

I cleared the Account enabled setting and saved the change.

Disabling the account prevented new interactive sign-ins. This control is important because a threat actor may have access to the user’s password, a cached browser session, or another authentication method associated with the stolen devices.

4. Required MFA re-registration
I navigated to:

User profile
→ Authentication methods
→ Require re-register multifactor authentication
I initiated the MFA re-registration requirement.

Because David’s authenticator app was installed on the stolen corporate phone, the existing MFA registration could not be trusted. Requiring re-registration ensures that, after identity verification and account restoration, David must enroll MFA again using a device he controls.

Containment Validation
The following containment actions were completed:

Control	Result	Security Purpose
Active sessions revoked	Completed	Invalidated existing sessions and forced reauthentication
Account sign-in disabled	Completed	Prevented new sign-ins while the incident is investigated
MFA re-registration required	Completed	Removed trust in the authenticator registration on the stolen phone
Security Rationale
This incident demonstrated the importance of treating a stolen, signed-in device as an active identity compromise—not merely a lost hardware asset.

A password reset alone may not immediately terminate every active cloud session. Similarly, MFA can become a risk rather than a safeguard when the enrolled device is stolen. The containment sequence therefore focused on reducing access in the correct order:

Revoke sessions first to interrupt potentially active access.

Disable the account to block new authentication attempts.

Reset MFA registration to ensure the stolen phone cannot remain a valid authentication factor.

This approach prioritizes immediate access containment while preserving a clear path for secure account recovery.

Recommended Follow-Up Actions:

After immediate containment, the organization should complete recovery and investigation activities:

Verify David Cho’s identity through an approved out-of-band process before restoring access.

Reset the user’s password before re-enabling the account.

Review Microsoft Entra sign-in logs for suspicious locations, IP addresses, devices, applications, and authentication failures.

Review Microsoft 365 audit logs for suspicious mailbox, file, SharePoint, Teams, or OneDrive activity.

Confirm whether the stolen laptop was encrypted and enrolled in Microsoft Intune or another endpoint-management platform.

Issue a remote lock or remote wipe command if device management is available.

Review Conditional Access policies to ensure lost or unmanaged devices cannot access sensitive resources.

Provide a replacement device and guide the user through secure MFA re-enrollment.

Document incident timeline, actions taken, evidence reviewed, and final remediation outcome.

Skills Demonstrated:

Microsoft Entra ID user administration

Identity incident response and account containment

Session revocation and token invalidation

User account disablement

MFA lifecycle management

Security-first prioritization during a critical incident

Microsoft 365 access-risk assessment

Incident documentation and operational communication

Key Takeaway:

When a corporate device is stolen, the response must focus on the associated identity, not just the physical asset. Revoking active sessions, disabling the account, and requiring MFA re-registration rapidly limits an attacker’s ability to use existing access and creates a controlled path for secure recovery.
