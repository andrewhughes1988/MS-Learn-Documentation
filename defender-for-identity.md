# What Is

# Microsoft Defender for Identity overview

Microsoft Defender for Identity helps organizations detect, investigate, and respond to identity-based attacks across on-premises, cloud, and hybrid environments. Attackers frequently target identities such as users, applications, and service accounts to gain access, escalate privileges, and maintain persistence.

Defender for Identity monitors identity signals from on-premises Active Directory and Microsoft Entra ID, other IAM solutions (for example, Okta).  It analyzes these signals using behavioral analytics, threat intelligence, and known attack patterns to detect suspicious activity across the full identity attack lifecycle. Alerts include investigation context in the Microsoft Defender portal, helping security teams understand what happened, why it matters, and how to respond.

## Identity Security

Microsoft Defender for Identity is a core component of Microsoft Identity Security. Identity Security focuses on protecting identities by providing visibility into identity coverage and posture, detecting identity‑based threats, and enabling investigation and response across identity systems, applications, and infrastructure.

Defender for Identity streams identity signals into the Microsoft Defender portal, where they are correlated with data from endpoints, email, SaaS applications, cloud workloads, and other security sources. This correlation helps security teams identify anomalous behavior, track attacker movement, and respond through unified incidents that reflect the full scope of an attack rather than isolated alerts.

## Defender for Identity capabilities

Defender for Identity delivers a modern identity threat detection solution with:

- Proactive identity security posture assessments

- Real‑time threat detection using analytics and behavioral intelligence

- Investigation of suspicious activities with clear, actionable incident context

- Remediation actions for compromised identities

### Prevent breaches with proactive identity security posture assessments

Defender for Identity helps organizations proactively reduce their identity attack surface. It evaluates identity configurations and highlights security weaknesses that attackers commonly exploit, allowing teams to address risks before they are abused.

Key posture capabilities include:

- Identity security posture assessments available through Microsoft Secure Score

- Identification of risky configurations and exposures

- Analysis of lateral movement paths that reveal how an attacker could traverse the environment

These insights help organizations strengthen identity resilience and reduce the likelihood of successful compromise.

### Detect identity-based threats

Defender for Identity is designed to detect threats that specifically target identities, including both human and nonh-uman identities such as service accounts, synchronization accounts, and applications. Detection is based on behavioral analytics and signal correlation rather than single events.

Defender for Identity monitors and analyzes identity activity such as:

- Authentication and authorization behavior

- Credential abuse and risky sign ins

- Privilege escalation and suspicious role or group membership changes

- Lateral movement attempts within the environment

- Abnormal behavior related to service accounts and other non‑human identities

The following table shows how Defender for Identity detections align to key stages of an identity based attack:

| Attack stage | Defender for Identity detections |

|----|----|

| Reconnaissance | Identifies suspicious discovery activity, such as attempts to enumerate user names, group membership, IP addresses, and resources. |

| Compromised credentials | Detects attempts to compromise credentials using techniques such as brute force, repeated failed authentications, and suspicious changes to user group membership. |

| Lateral movement| Detects attempts to move laterally and expand control of sensitive identities and across different environments. |

| AD Domain dominance | Highlights behavior associated with full domain compromise, such as remote code execution on domain controllers, DCShadow, malicious domain controller replication, and Golden Ticket activity. |

Attackers often begin with any accessible identity and then move laterally toward high value targets such as privileged accounts such as domain administrators, global admin, application admins and sensitive data. Defender for Identity helps identify these behaviors early by building behavioral profiles for users, devices, and accounts and detecting deviations that indicate attacker activity.

### Investigate identity threats

Defender for Identity generates alerts that are enriched with context such as affected identities, related activity, and attacker techniques. Analysts can use this context to validate suspicious behavior and understand what happened.

Defender for Identity also supports identity investigation and hunting workflows. Identity entities and authentication activity are available within the Microsoft Defender portal, enabling security teams to investigate activity patterns and hunt for additional identity based threats across cloud, on-premises, and hybrid users.

### Respond to identity-based attacks

Defender for Identity supports response by:

- Correlating identity alerts into unified incidents in Microsoft Defender

- Providing identity context (users, accounts, roles, and lateral movement indicators) to scope impact and prioritize actions

- Enabling remediation actions in the Microsoft Defender portal for affected identities and related entities

## Microsoft Defender portal experience

The Microsoft Defender portal provides a unified experience for monitoring, investigating, and responding to identity threats. From the portal, security teams can:

- View identity based alerts and correlated incidents

- Investigate users, devices, and identity relationships

- Track identity security posture and remediation recommendations

- Perform response actions on compromised identities

By contributing rich identity context into unified incidents, Defender for Identity helps security teams understand attacker behavior, prioritize risk, and take action to disrupt identity based attacks across the organization.

## Architecture overview

Microsoft Defender for Identity uses lightweight [sensors](./deploy/deploy-defender-identity.md), API connectors, and a cloud‑based analytics service managed in the Microsoft Defender portal.

Sensors run on your identity infrastructure, capturing and parsing relevant network traffic and Windows events locally. API connectors integrate external Identity and Access Management (IAM) systems, to provide comprehensive identity protection.

Only the required signals are sent to the Defender for Identity cloud service, minimizing performance impact and avoiding complex network changes.

The cloud service analyzes identity signals and integrates them with other Microsoft Defender workloads, contributing identity intelligence to correlated alerts and incidents across Microsoft Defender XDR.

## Next steps

[Deploy Microsoft Defender for Identity](./deploy/deploy-defender-identity.md)


# Whats New

# What's new in Microsoft Defender for Identity

This article is updated frequently to let you know what's new in the latest releases of Microsoft Defender for Identity.

## What's new scope and references

Defender for Identity releases are deployed gradually across customer tenants. If there's a feature documented here that you don't see yet in your tenant, check back later for the update.

For more information, see also:

- [What's new in Microsoft Defender XDR](/microsoft-365/security/defender/whats-new)

- [What's new in Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/whats-new-in-microsoft-defender-endpoint)

- [What's new in Microsoft Defender for Cloud Apps](/cloud-app-security/release-notes)

For updates about versions and features released six months ago or earlier, see the [What's new archive for Microsoft Defender for Identity](whats-new-archive.md).

## June 2026

### New Defender for Identity security alerts

These new alerts were added to the Defender for Identity security alerts:

**New alerts related to Entra ID**:

- [Anomalous activity following Global Administrator elevation](alerts-xdr.md#anomalous-activity-following-global-administrator-elevation)

- [Reciprocal Temporary Access Pass creation between users](alerts-xdr.md#reciprocal-temporary-access-pass-creation-between-users)

- [Suspicious service principal sign-in following credential addition](alerts-xdr.md#suspicious-service-principal-sign-in-following-credential-addition)

- [Suspicious bulk user deletion via scripted activity](alerts-xdr.md#suspicious-bulk-user-deletion-via-scripted-activity)

- [Suspicious removal of privileged app role assignment through Graph API](alerts-xdr.md#suspicious-removal-of-privileged-app-role-assignment-through-graph-api)

- [Suspicious sign-in by a user exhibiting a spike in account update activity](alerts-xdr.md#suspicious-signin-by-a-user-exhibiting-a-spike-in-account-update-activity)

- [User exhibiting spike in distinct application-resource access combinations](alerts-xdr.md#user-exhibiting-spike-in-distinct-applicationresource-access-combinations)

**New alerts related to Active Directory**:

- [DCSync attack (replication of directory services)](alerts-xdr.md#dcsync-attack-replication-of-directory-services)

- [Suspicious Entra Connect account authentication](alerts-xdr.md#suspicious-entra-connect-account-authentication)

**New alerts related to other identity providers**:

- [SailPoint ISC suspected brute-force attack](alerts-xdr.md#sailpoint-isc-suspected-brute-force-attack)

## May 2026

### Sensor v3.x supports all identity roles on domain controllers

Defender for Identity sensor v3.x now supports domain controllers running all identity roles, including Microsoft Entra Connect, AD FS, and AD CS identity roles. For deployment details, see [Defender for Identity sensor v3.x prerequisites](deploy/deploy-sensor-v3.md).

### Increased sensor capacity

Defender for Identity now supports up to 1,000 sensors per workspace, increased from the previous limit of 350. To add more than 1,000 sensors, contact Defender for Identity support.

### New Defender for Identity security alerts

These new alerts were added to the Defender for Identity security alerts:

**New alerts related to Entra ID**:

- [Guest user account promoted to member](alerts-xdr.md#guest-user-account-promoted-to-member)

- [User was created and assigned to Global Administrator role](alerts-xdr.md#user-was-created-and-assigned-to-global-administrator-role)

- [Failed credential abuse attempt in Entra ID authentication](alerts-xdr.md#failed-credential-abuse-attempt-in-entra-id-authentication)

- [Malicious sign in from a randomized user agent](alerts-xdr.md#malicious-sign-in-from-a-randomized-user-agent)

- [Possible use of a stolen session cookie](alerts-xdr.md#possible-use-of-a-stolen-session-cookie)

- [Stolen session cookie replay detected](alerts-xdr.md#stolen-session-cookie-replay-detected)

- [Suspected Conditional Access bypass via non-compliant device](alerts-xdr.md#suspected-conditional-access-bypass-via-non-compliant-device)

- [Suspicious addition of default third‑party MFA method to user account](alerts-xdr.md#suspicious-addition-of-default-thirdparty-mfa-method-to-user-account)

### Known limitation: Migration of domain controllers with Windows Server 2025 from sensor v2.x to sensor v3.x is not supported

Migrating domain controllers running Windows Server 2025 to sensor v3.x isn't currently supported. Continue using the v2.x sensor on Windows Server 2025 domain controllers should until support for migration to v3.x is available.

For more information, see [Known Issues for migrating sensors](troubleshooting-known-issues.md#windows-server-2025-sensor-v3x-migration-not-supported).

## April 2026

### **Identity Explorer (Preview)**

The Identity page now includes the **Identity Explorer** tab for customers with a Microsoft Sentinel Data Lake license. This tab uses the [hunting graph](/defender-xdr/advanced-hunting-graph) to visualize identity attack paths and exposure scenarios as interactive graphs. Use predefined identity scenarios to discover lateral movement paths, privilege escalation routes, and credential-access risks. For more information, see [Investigate an identity](/defender-xdr/investigate-users#identity-explorer-tab-preview).

### **Custom account correlation rules (Preview)**

Custom account correlation rules let you link accounts that belong to the same identity, such as privileged accounts with unique naming conventions. You can correlate accounts that don't share strong identifiers such as account ID, SID, object ID, or UPN by defining rules based on UPN prefix, UPN suffix, or domain UPN. For more information, see [Create custom account correlation rules](custom-account-correlation-rules.md).

### Automatic Windows event auditing configuration for sensors v3.x is now generally available

The [Automatic Windows event-auditing configuration for sensors v3.x](deploy/configure-windows-event-collection.md#configure-defender-for-identity-to-collect-windows-events-automatically) is now generally available. Automatic Windows event-auditing streamlines deployment by automatically applying the required auditing settings to new sensors and correcting misconfigurations on existing ones.

## March 2026

### Sensor v3.x support for domain controllers with Microsoft Entra Connect identity roles

Defender for Identity sensor v3.x now supports domain controllers that run Microsoft Entra Connect, including detections and identity security posture management (ISPM) recommendations.

Detections and ISPM recommendations for additional identity roles, including AD FS and AD CS, will become available soon.

Domain controllers with Microsoft Entra Connect roles and v3.x of the sensor must run Windows Server 2019 or later and include at least the [March 2026 Cumulative Update](https://support.microsoft.com/topic/march-10-2026-kb5078766-os-build-20348-4893-fa3ee26a-0877-47d7-a4b2-9dd632ea8cea). For deployment details, see [Defender for Identity deployment overview](deploy/deploy-defender-identity.md) and [Sensor v3.x prerequisites](deploy/deploy-sensor-v3.md).

### Migrate Defender for Identity sensors from v2.x to v3.x

You can now migrate Defender for Identity sensors from v2.x to v3.x directly from the Microsoft Defender portal. The v2.x sensor continues running during the migration until the v3.x sensor is ready, so there's no downtime. Eligible servers appear as **Ready for migration** on the **Sensors** page, and migration takes up to 20 minutes. For more information, see [Migrate to Defender for Identity sensor v3.x](deploy/migrate-to-sensor-v3.md).

### Identity security enhancements

New identity security capabilities help you monitor and manage identity security for human and non-human identities:

- **Identity Security dashboard (Preview)**: The **Identity Security** dashboard provides summary cards for identity providers, on-premises identities, SaaS identities, PAM and IGA integrations, and non-human identities. Widgets show deployment status, highly privileged identities, users at risk, and domains with unsecured configurations. For more information, see [The Identity Security dashboard](dashboard.md).

The **Identity Security** dashboard is being rolled out gradually to customers, and might not yet be available in your organization.

- **Coverage and maturity page (Preview)**: The **Coverage and maturity** page shows your organization's identity security coverage for identity providers, on-premises identities, SaaS identities, and PAM and IGA integrations. Each source displays a maturity level, including Connected, Protected, Fortified, and Resilient, with identity counts, coverage scores, and prioritized setup tasks. For more information, see [Coverage and maturity](/defender-xdr/identity-security/coverage-maturity).

The **Coverage and maturity** page is being rolled out gradually to customers, and might not yet be available in your organization. If you don't see this feature in your environment yet, check back soon.

- **Identity inventory**: The **Identity inventory** page now shows human and non-human identities in separate tabs. Insight cards help you classify critical assets, view highly privileged identities, identify critical Active Directory service accounts, and view cloud application accounts. For more information, see [View the Identity inventory](identity-inventory.md).

- **Non-human identities (Preview)**: The **Non-human identities** tab on the **Identity inventory** page shows non-human identities, including Microsoft Entra ID apps, Active Directory service accounts, Google Workspace apps, and Salesforce apps. The tab includes statistics for risky, highly privileged, overprivileged, unused, and externally published identities. A separate investigation page lets you view details for each identity. For more information, see [Identity inventory](identity-inventory.md) and [Investigate non-human identities](/defender-xdr/investigate-non-human-identities).

- **Identity risk score (Preview)**: A new risk score for identities, ranging from 0 to 100, that indicates the likelihood of compromise and the potential impact based on criticality and privileged roles. The risk score is available in Microsoft Entra ID, where it can be used to inform conditional access policies and identity protection workflows. A new **Risk score** tab on the **Identity** page provides a detailed breakdown of the risk factors, including percentile comparison and risk trends. For more information, see [Investigate an identity](/defender-xdr/investigate-users).

- **Identity security recommendations (Preview)**: View recommendations for Active Directory, Microsoft Entra ID, and SaaS applications such as Microsoft, Atlassian, GitHub, Google Workspace, Salesforce, and ServiceNow. Recommendations are also available for non-Microsoft identity providers such as Okta, PingOne, CyberArk, and SailPoint. For more information, see [Identity security recommendations](/defender-xdr/identity-security/identity-security-recommendations).

- **Domain investigation page (Preview)**: The **Domain investigation** page shows Active Directory domain security, including domain properties, deployment health, identity summary, service account breakdown, sensitive entities, active recommendations, group policies, and trust relationships. For more information, see [Investigate a domain](investigate-domain.md).

- **Password protection page (Preview)**: The **Password protection** page shows identity password risk from Active Directory, Microsoft Entra ID, and Okta, with tabs for password hygiene, password policies, leaked credentials, and exposed passwords. For more information, see [Password protection](password-protection.md).

### Defender for Identity sensor updates

Sensor versions now display the full version number (for example, 2.255.19201.14651) instead of only the major/minor version (for example, 2.255). This makes it easier to identify the exact update installed on each sensor.

When you validate upgrades or troubleshoot, the last two numbers in the version (for example, 19201.14651) show which update is installed.

|Version number|Updates|

|---|---|

|2.255.19201.14651|This sensor update includes bug fixes.|

### Migrate Defender for Identity sensors from v2.x to v3.x

You can now migrate Defender for Identity sensors from v2.x to v3.x directly from the Microsoft Defender portal. The v2.x sensor continues running during the migration until the v3.x sensor is ready, so there's no downtime. Eligible servers appear as **Ready for migration** on the **Sensors** page, and migration takes up to 20 minutes. For more information, see [Migrate to Defender for Identity sensor v3.x](deploy/migrate-to-sensor-v3.md).

### Identity security enhancements

New identity security capabilities help you monitor and manage identity security for human and non-human identities:

- **Identity Security dashboard (Preview)**: The **Identity Security** dashboard provides summary cards for identity providers, on-premises identities, SaaS identities, PAM and IGA integrations, and non-human identities. Widgets show deployment status, highly privileged identities, users at risk, and domains with unsecured configurations. For more information, see [The Identity Security dashboard](dashboard.md).

The **Identity Security** dashboard is being rolled out gradually to customers, and might not yet be available in your organization.

- **Coverage and maturity page (Preview)**: The **Coverage and maturity** page shows your organization's identity security coverage for identity providers, on-premises identities, SaaS identities, and PAM and IGA integrations. Each source displays a maturity level, including Connected, Protected, Fortified, and Resilient, with identity counts, coverage scores, and prioritized setup tasks. For more information, see [Coverage and maturity](/defender-xdr/identity-security/coverage-maturity).

The **Coverage and maturity** page is being rolled out gradually to customers, and might not yet be available in your organization. If you don't see this feature in your environment yet, check back soon.

- **Identity inventory**: The **Identity inventory** page now shows human and non-human identities in separate tabs. Insight cards help you classify critical assets, view highly privileged identities, identify critical Active Directory service accounts, and view cloud application accounts. For more information, see [View the Identity inventory](identity-inventory.md).

- **Non-human identities (Preview)**: The **Non-human identities** tab on the **Identity inventory** page shows non-human identities, including Microsoft Entra ID apps, Active Directory service accounts, Google Workspace apps, and Salesforce apps. The tab includes statistics for risky, highly privileged, overprivileged, unused, and externally published identities. A separate investigation page lets you view details for each identity. For more information, see [Identity inventory](identity-inventory.md) and [Investigate non-human identities](/defender-xdr/investigate-non-human-identities).

- **Identity risk score (Preview)**: A new risk score for identities, ranging from 0 to 100, that indicates the likelihood of compromise and the potential impact based on criticality and privileged roles. The risk score is available in Microsoft Entra ID, where it can be used to inform conditional access policies and identity protection workflows. A new **Risk score** tab on the **Identity** page provides a detailed breakdown of the risk factors, including percentile comparison and risk trends. For more information, see [Investigate an identity](/defender-xdr/investigate-users).

- **Identity security recommendations (Preview)**: View recommendations for Active Directory, Microsoft Entra ID, and SaaS applications such as Microsoft, Atlassian, GitHub, Google Workspace, Salesforce, and ServiceNow. Recommendations are also available for non-Microsoft identity providers such as Okta, PingOne, CyberArk, and SailPoint. For more information, see [Identity security recommendations](/defender-xdr/identity-security/identity-security-recommendations).

- **Domain investigation page (Preview)**: The **Domain investigation** page shows Active Directory domain security, including domain properties, deployment health, identity summary, service account breakdown, sensitive entities, active recommendations, group policies, and trust relationships. For more information, see [Investigate a domain](investigate-domain.md).

- **Password protection page (Preview)**: The **Password protection** page shows identity password risk from Active Directory, Microsoft Entra ID, and Okta, with tabs for password hygiene, password policies, leaked credentials, and exposed passwords. For more information, see [Password protection](password-protection.md).

### Defender for Identity sensor updates

Sensor versions now display the full version number (for example, 2.255.19201.14651) instead of only the major/minor version (for example, 2.255). This makes it easier to identify the exact update installed on each sensor.

When you validate upgrades or troubleshoot, the last two numbers in the version (for example, 19201.14651) show which update is installed.

|Version number|Updates|

|---|---|

|2.255.19201.14651|This sensor update includes bug fixes.|

### New Defender for Identity security alerts

These new alerts were added to the Defender for Identity security alerts:

**New alerts related to Entra ID**:

- [Attempt to disable Defender for Identity service principal observed](alerts-xdr.md#attempt-to-disable-defender-for-identity-service-principal-observed)

- [Suspicious Entra account enablement after disruption](alerts-xdr.md#suspicious-entra-account-enablement-after-disruption)

- [Suspicious Intune device registration activity](alerts-xdr.md#suspicious-intune-device-registration-activity)

- [Suspicious OS switch sign-in](alerts-xdr.md#suspicious-os-switch-sign-in)

- [User sign‑in from shared client infrastructure exhibiting anomalous activity](alerts-xdr.md#user-signin-from-shared-client-infrastructure-exhibiting-anomalous-activity)

- [Suspicious sign-in from an unusual user agent and IP address using PowerShell](alerts-xdr.md#suspicious-sign-in-from-an-unusual-user-agent-and-ip-address-using-powershell)

- [Suspicious sign-in from an unusual user agent and IP address using device code flow](alerts-xdr.md#suspicious-sign-in-from-an-unusual-user-agent-and-ip-address-using-device-code-flow)

**New alerts related to Active Directory**:

- [Suspicious on-premises account enablement after disruption](alerts-xdr.md#suspicious-on-prem-account-enablement-after-disruption)

- [Suspicious resource-based constrained delegation (RBCD) attribute change](alerts-xdr.md#suspicious-resource-based-constrained-delegation-rbcd-attribute-change)

- [Suspicious resource-based constrained delegation (RBCD) authentication](alerts-xdr.md#suspicious-resource-based-constrained-delegation-rbcd-authentication)

### Suspected pass-the-ticket attack alert is now generally available

The [Suspected pass-the-ticket attack](alerts-xdr.md#suspected-pass-the-ticket-attack) alert is now generally available. This alert was previously available in public preview as *Pass-the-Ticket (PtT) attack*. For more information, see [Lateral movement alerts](alerts-xdr.md).

### Updates to Secure Score category calculations for increased accuracy

To improve accuracy and better protect organizational identities, some security recommendations categorized as **Cloud apps** recommendations are now considered identity‑related and grouped under the **Identity** category. While the total Secure Score remains unchanged, individual identity and app scores may change.

### Continued rollout of new health alert: Sensor v3.x RPC audit misconfigured

The **Sensor v3.x RPC Audit Misconfigured** health alert is continuing to be rolled out gradually to customers.  The new health alert helps identify v3.x sensors where Enhanced RPC auditing configuration is either missing or incorrectly applied. Enhanced RPC auditing is required for some Microsoft Defender for Identity advanced identity detections.  For more information, see [Configure RPC on sensors v3.x](deploy/deploy-sensor-v3.md#configure-rpc-auditing).

## February 2026

### Defender for Identity sensor updates

|Version number|Updates|

|---|---|

|2.255|This sensor update includes bug fixes.|

### New Defender for Identity security alerts

These new alerts were added to the Defender for Identity security alerts:

**New alerts related to Entra ID**:

- [Suspicious user configuration change activity from Entra ID sync application](alerts-xdr.md#suspicious-user-configuration-change-activity-from-entra-id-sync-application)

- [Anomalous OAuth device code authentication activity](alerts-xdr.md#anomalous-oauth-device-code-authentication-activity)

- [Suspicious Graph API request made from Entra ID sync application](alerts-xdr.md#suspicious-graph-api-request-made-from-entra-id-sync-application)

- [Suspicious sign-in observed from Entra ID sync application](alerts-xdr.md#suspicious-sign-in-observed-from-entra-id-sync-application)

- [Suspicious sign in with CSRF speedbump trigger](alerts-xdr.md#suspicious-sign-in-with-csrf-speedbump-trigger)

**New alerts related to Active Directory**:

- [Possible golden ticket attack (suspicious ticket)](alerts-xdr.md#possible-golden-ticket-attack-suspicious-ticket)

- [Possible Kerberos key list attack](alerts-xdr.md#possible-kerberos-key-list-attack)

## January 2026

### New Defender for Identity security alerts

These new alerts were added to the Defender for Identity security alerts:

**New alerts related to Entra ID**:

- [Suspicious sign-in observed from Entra ID sync application to an uncommon resource app](alerts-xdr.md#suspicious-sign-in-observed-from-entra-id-sync-application-to-an-uncommon-resource-app)

- [Suspicious sign-in observed to Entra ID sync application using an uncommon user agent](alerts-xdr.md#suspicious-sign-in-observed-to-entra-id-sync-application-using-an-uncommon-user-agent)

- [Possible OAuth code theft detected through consent abuse](alerts-xdr.md#possible-oauth-code-theft-detected-through-consent-abuse)

- [Possible adversary-in-the-middle (AiTM) attack detected (ConsentFix)](alerts-xdr.md#possible-adversary-in-the-middle-aitm-attack-detected-consentfix)

- [Skipped MFA on remembered device from uncommon ISP sign-in](alerts-xdr.md#skipped-mfa-on-remembered-device-from-uncommon-isp-sign-in)

**New alerts related to Active Directory**:

- [Pass-the-Ticket (PtT) attack](alerts-xdr.md#suspected-pass-the-ticket-attack)

- [Possible Active Directory Certificate Services enumeration](alerts-xdr.md#possible-active-directory-certificate-services-enumeration)

- [Possible Active Directory enumeration via ADWS](alerts-xdr.md#possible-active-directory-enumeration-via-adws)

- [Suspicious NTLM authentication](alerts-xdr.md#suspicious-ntlm-authentication)

- [Possible Kerberoasting attack using a stealthy LDAP search](alerts-xdr.md#possible-kerberoasting-attack-using-a-stealthy-ldap-search)

- [Suspicious Kerberos authentication (TGT request using TGS-REQ)](alerts-xdr.md#suspicious-kerberos-authentication-tgt-request-using-tgs-req)

### Identity inventory enhancements are now generally available

- **Accounts tab in Identity Inventory**: The new **Accounts*- tab provides a consolidated view of all accounts associated with an identity, including accounts from Active Directory, Microsoft Entra ID, and supported non-Microsoft identity providers. For more information, see [Manage related identities and accounts](manage-related-identities-accounts.md).

- **Manually link and unlink accounts**: Manually link or unlink accounts from an identity directly in the **Accounts*- tab. This capability helps you correlate identity components from different directory sources and provides a complete identity context during investigations. For more information, see [Manage related identities and accounts](manage-related-identities-accounts.md).

- **Identity-level remediation actions**: You can now perform remediation actions such as disabling accounts or resetting passwords on one or more accounts linked to an identity. For more information, see [Remediation actions](remediation-actions.md#roles-and-permissions).

- **New advanced hunting table**: Advanced hunting in Microsoft Defender now includes the **[IdentityAccountInfo](

/defender-xdr/advanced-hunting-identityaccountinfo-table)*- table. This table provides account information from various sources, including Microsoft Entra ID, and links to the identity that owns the account.

### New security posture assessments

- [Remove stale Active Directory accounts (Preview)](security-posture-assessments/accounts.md#remove-stale-active-directory-accounts-preview) lists any user accounts in Active Directory that are stale, meaning they haven't logged in at all during the past 90 days.

- [Microsoft Entra ID privileged user accounts that are also privileged in Active Directory (Preview)](security-posture-assessments/accounts.md#microsoft-entra-id-privileged-user-accounts-that-are-also-privileged-in-active-directory-preview) lists Microsoft Entra ID privileged user accounts that also have privileged roles in Active Directory.

### New Health Alert: Sensor v3.x RPC Audit Misconfigured

Enhanced RPC auditing is required for some Microsoft Defender for Identity advanced identity detections. A new health alert helps identify v3.x sensors where this configuration is either missing or incorrectly applied. The alert is being rolled out gradually to customers. For more information, see [Configure RPC on sensors v3.x](deploy/deploy-sensor-v3.md#configure-rpc-auditing).

### New Entra ID user roles to support remediation actions

For some [remediation actions](remediation-actions.md), Defender for Identity creates an enterprise application in Microsoft Entra ID. The Microsoft Defender for Identity enterprise application is created automatically in the tenant and is used only to execute remediation actions. When a user initiates an action from the Defender portal, the request is authorized based on the user’s Entra ID roles and executed by the Defender for Identity application, enforcing Entra ID role‑based access control (RBAC) and audit logging. These new Entra ID roles are supported:

- User Administrator

- Authentication Administrator

- Privileged Authentication Administrator

- Directory Writers

- Helpdesk Administrator

- Security Operator

### Automatic Windows event auditing configuration for Defender for Identity sensors v3.x

Weâ€™re gradually rolling out automatic Windows event-auditing configuration for sensors v3.x, along with related health alerts. Automatic Windows event-auditing streamlines deployment by automatically applying the required auditing settings to new sensors and correcting misconfigurations on existing ones.

This update might identify existing auditing configuration gaps that weren't previously detected.

To ensure consistent protection, we recommend that you make sure all servers with the v3 sensors are configured with:

- The latest Windows cumulative update.

- Automatic Windows event auditing enabled.

For more information, see [Configure automatic windows auditing](deploy/configure-windows-event-collection.md#configure-defender-for-identity-to-collect-windows-events-automatically).

### Sensor updates

|Version number|Updates|

|---|---|

|2.254|The sensor now supports a new DNS zone target for *.atp.gcc.azure.com. Make sure your sensors in GCC can access this zone with your sensor DNS prefix.|

### New security posture assessment: Identify service accounts in privileged groups

This identity security posture assessment lists Active Directory service accounts with direct or nested membership in privileged groups.

You can use this assessment to identify service accounts with elevated permissions and take action when privileged access isnâ€™t required.

For more information, see:[Security posture assessment: Identify service accounts in privileged groups](security-posture-assessments/accounts.md#identify-service-accounts-in-privileged-groups)

### New security posture assessment: Locate accounts in built-in Operator Groups

This identity security posture assessment lists Active Directory accounts that are members of built-in Operator Groups, including direct and indirect membership.

You can use this assessment to review legacy or unnecessary operator access and take action when elevated access isn't required.

For more information, see:[Security posture assessment: Locate accounts in built-in Operator Groups](security-posture-assessments/accounts.md#locate-accounts-in-built-in-operator-groups)

## December 2025

### New properties for 'sensorCandidate' resource type in Graph-API (preview)

|Property|Type|Description|

|---|---|---|

|domainName|String|The domain name of the sensor.|

|senseClientVersion|String|The version of the Defender for Identity sensor client.|

This capability is currently in preview and available in API preview version. Learn more [here](/graph/api/resources/security-sensorcandidate?view=graph-rest-beta&preserve-view=true)

### ADWS LDAP search in Advanced Hunting

New ADWS LDAP search activity is now available in the 'IdentityQueryEvents' table in Advanced Hunting. This can provides visibility into directory queries performed through ADWS, helping customers track these operations and create custom detection based on this data.

|Version number|Updates|

|---|---|

|2.253|Includes bug fixes and stability improvements for the Microsoft Defender for Identity sensor.|

|2.252|Includes bug fixes and stability improvements for the Microsoft Defender for Identity sensor.|

## November 2025

|Version number|Updates|

|---|---|

|2.251|The enhanced ADWS LDAP and legacy password-based LDAP query methods now capture a broader range of unique events at scale. As a result, you might notice an increase in recorded activity.|

### Identity Inventory enhancements: Accounts tab, manual account linking and unlinking, and expanded remediation actions

The following new features are now available in Microsoft Defender for Identity:

**Accounts tab in Identity Inventory**:

A new Accounts tab provides a consolidated view of all accounts associated with an identity, including accounts from Active Directory, Microsoft Entra ID, and supported non-Microsoft identity providers. For more information, see: [Manage related identities and accounts (Preview)](manage-related-identities-accounts.md)

**Manual link and unlink of accounts**:

You can now manually link or unlink accounts from an identity directly in the Accounts tab. This capability helps you correlate identity components from different directory sources and provides a complete identity context during investigations.

For more information, see: [Manage related identities and accounts](manage-related-identities-accounts.md).

**Identity-level remediation actions**:

You can now perform remediation actions such as disabling accounts or resetting passwords on one or more accounts linked to an identity. For more information, see: [Remediation actions](remediation-actions.md#roles-and-permissions).

### New security posture assessment: Change password for on-premises account with potentially leaked credentials (Preview)

The new security posture assessment lists users whose valid credentials were leaked. For more information, see: [Change password for on-premises account with potentially leaked credentials (Preview)](/defender-for-identity/security-posture-assessments/accounts#change-password-for-on-prem-account-with-potentially-leaked-credentials-preview)

### Microsoft Defender for Identity sensor version updates

|Version number|Updates|

|---|---|

|2.250|The improved event log query method captures a broader range of unique events at scale. As a result, you might notice an increase in captured activities. This update also includes security and performance improvements.|

### Expansion of identity scoping: Support for Organizational units (Preview)

In addition to the GA release of scoping by Active Directory domains a few months ago, you can now scope by **Organizational Units (OUs)*- as part of XDR user role-based access control (URBAC). This enhancement provides even more granular control over which entities and resources are included in security analysis.

For more information, see [Configure scoped access for Microsoft Defender for Identity](configure-scoped-access.md).

## Next steps

- [What is Microsoft Defender for Identity?](what-is.md)

- [Frequently asked questions](technical-faq.yml)

- [Defender for Identity prerequisites](prerequisites.md)

- [Defender for Identity capacity planning](capacity-planning.md)

- [Check out the Defender for Identity forum!](<https://aka.ms/MDIcommunity>)


# Zero Trust

# Zero Trust with Defender for Identity

[Zero Trust](/security/zero-trust/zero-trust-overview) is a security strategy for designing and implementing the following sets of security principles:

|Verify explicitly  |Use least privilege access  |Assume breach  |

|---------|---------|---------|

|Always authenticate and authorize based on all available data points.     | Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection.        | Minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses.        |

Defender for Identity is a primary component of a Zero Trust strategy and your XDR deployment with Microsoft Defender XDR. Defender for Identity uses Active Directory signals to detect sudden account changes like privilege escalation or high-risk lateral movement, and reports on easily exploited identity issues like unconstrained Kerberos delegation, for correction by the security team.

## Monitoring for Zero Trust

When monitoring for Zero Trust, make sure review and mitigate open alerts from Defender for Identity together with your other security operations. You may also want to use [advanced hunting queries in Microsoft Defender XDR](/microsoft-365/security/defender/advanced-hunting-overview) to look for threats across identities, devices, and cloud apps.

> [!TIP]

> Ingest your alerts into [Microsoft Sentinel with Microsoft Defender XDR](/azure/sentinel/microsoft-365-defender-sentinel-integration), a cloud-native, security information event management (SIEM) and security orchestration automated response (SOAR) solution to provide your Security Operations Center (SOC) with a single pane of glass for monitoring security events across your enterprise.

>

## Next steps

Learn more about Zero Trust and how to build an enterprise-scale strategy and architecture with the [Zero Trust Guidance Center](/security/zero-trust).

For more information, see:

- [Securing identity with Zero Trust](/security/zero-trust/deploy/identity)

- [Deploy your identity infrastructure for Microsoft 365](/microsoft-365/enterprise/deploy-identity-solution-overview)

- [Zero Trust deployment plan with Microsoft 365](/microsoft-365/security/microsoft-365-zero-trust)

- [Zero Trust with Microsoft Defender XDR](/microsoft-365/security/defender/zero-trust-with-microsoft-365-defender)


# Microsoft 365 Security Center Mdi

# Microsoft Defender for Identity in the Microsoft Defender portal

**Applies to:**

- What is Microsoft Defender XDR?

- [Microsoft Defender for Identity](/defender-for-identity/)

Microsoft Defender for Identity is part of the Microsoft Defender portal, the home for monitoring and managing security across your Microsoft identities, data, devices, apps, and infrastructure. The Microsoft Defender portal allows security admins to perform their security tasks in one location, which simplifies workflows and integrating functionality from other Microsoft Defender XDR services.

Microsoft Defender for Identity contributes identity focused information into the incidents and alerts that the Microsoft Defender portal presents. This information is key to providing context and correlating alerts from the other products within Microsoft Defender XDR.

<a name='converged-experiences-in-microsoft-365-defender'></a>

## Converged experiences in the Microsoft Defender portal

The [Microsoft Defender portal](https://security.microsoft.com) combines security capabilities that protect, detect, investigate, and respond to email, collaboration, identity, and device threats.

The following sections describe enhanced Defender for Identity features found in the Microsoft Defender portal.

> [!NOTE]

> Customers using the classic Defender for Identity portal are [automatically redirected to the Microsoft Defender portal](https://techcommunity.microsoft.com/t5/microsoft-365-defender-blog/leveraging-the-convergence-of-microsoft-defender-for-identity-in/ba-p/3856321), with no option to revert back to the classic portal.

### Configuration and posture

|Area |Description  |

|---------|---------|

|**Global exclusions**     |   Global exclusions allow you to define certain entities, such as IP addresses, devices, or domains, to be excluded across all Defender for Identity detections. For example, if you only exclude a device, the exclusion applies only to detections that have a *device* identification as part of the detection. <br><br> For more information, see [Global excluded entities](/defender-for-identity/exclusions).  |

|**Manage action and directory service accounts**     |  You might want to respond to compromised users by disabling their accounts or resetting their password. When you take either of these actions, the Microsoft Defender portal is configured by default to use the *local system* account. Therefore, you'll only need to configure action and directory service account settings if you want to have more control, and define a different user account to perform user remediation actions.<br><br> For more information, see [Microsoft Defender for Identity action accounts](/defender-for-identity/manage-action-accounts).      |

|**Custom permission roles**     |  The Microsoft Defender portal supports custom permission roles. <br><br>For more information, see  [Microsoft Defender XDR role-based access control (RBAC)](/defender-xdr/manage-rbac).     |

|**Microsoft Secure Score**     | Defender for Identity security posture assessments is available in [Microsoft Secure Score](https://security.microsoft.com/securescore). Each assessment is a downloadable report with instructions for use and tools to build an action plan for remediating or resolving the issue. Filter Microsoft Secure Score by **Identity** to view Defender for Identity assessments. <br><br> For more information, see [Microsoft Defender for Identity's security posture assessments](/defender-for-identity/security-assessment).     |

|**API**     | Use any of the following Microsoft Defender XDR APIs with Defender for Identity: <br><br>- [Query activities via API](/defender-xdr/api-advanced-hunting) <br>- [Manage security alerts via API](/defender-xdr/api-incident) <br>- [Stream security alerts and activities to Microsoft Sentinel](/defender-xdr/streaming-api)<br><br>**Tip**: The Microsoft Defender portal only stores advanced hunting data for 30 days.  If you need longer retention periods, stream the activities to Microsoft Sentinel or another partner security information and event management (SIEM) system.         |

| **Onboarding** | Defender for Identity onboarding is now automatic for new customers, with no need to configure a workspace. <br><br>If you need to delete your instance, open a Microsoft support case. |

### Investigation

|Area |Description  |

|---------|---------|

| **Identities** area| In the Microsoft Defender portal, expand the **Identities** area to view a **Dashboard** of graphs and widgets with commonly used data, and other identity security pages. The **Health issues** page, listing all health issues for your Defender for Identity deployment, is available under **Settings** > **Identities** > **Deployment**. <br><br>For more information, see [View the Identity Security dashboard](/defender-for-identity/dashboard) and [Defender for Identity health issues](/defender-for-identity/health-alerts). |

|**Identity page**     |  The Microsoft Defender portal identity details page provides inclusive data about each identity, such as: <br><br>- Any associated alerts <br>- Active Directory account control<br>- Risky lateral movement paths<br>- A timeline of activities and alerts<br>- Details about observed locations, devices, and groups. <br><br>For more information, see [Investigate users in the Microsoft Defender portal](/defender-xdr/investigate-users). |

|**Device page**     | The Microsoft Defender portal alert evidence lists all devices and users connected to each suspicious activity.  Investigate further by selecting a specific device in an alert to access a device details page.  <br><br>For more information, see [Investigate devices in the Microsoft Defender for Endpoint Devices list](/defender-endpoint/investigate-machines). |

|**Advanced hunting**     |  The Microsoft Defender portal helps you proactively search for threats and malicious activity by using advanced hunting queries. These powerful queries can be used to locate and review threat indicators and entities for both known and potential threats. <br><br>Build custom detection rules from advanced hunting queries to help you proactively watch for events that might be indicative of breach activity and misconfigured devices. <br><br>For more information, see [Proactively hunt for threats with advanced hunting in the Microsoft Defender portal](/defender-xdr/advanced-hunting-overview).    |

|**Global search**     | Use the search bar at the top of the Microsoft Defender portal page to search for any entity being monitored by Microsoft Defender XDR, including identities, endpoints, Office 365 data, Active Directory groups (Preview), and more. <br><br>Select results directly from the search drop-down, or select **All users** or **All devices** to see all entities associated with a given search term.  |

### Detection and response

|Area |Description  |

|---------|---------|

| **Alert and incident correlation** |Defender for Identity alerts is now included in the Microsoft Defender portal's alert queue, making them available to the automated incident correlation feature. <br><br>View all of your alerts in one place, and determine the scope of the breach even quicker than before. <br><br>For more information, see [Investigate Defender for Identity alerts in the Microsoft Defender portal](/defender-for-identity/manage-security-alerts). |

| **Alert exclusions** |The Microsoft Defender portal's alert interface is more user friendly, and includes a search function and global exclusions, meaning you can exclude any entity from all alerts generated by Defender for Identity. <br><br>For more information, see [Configure Defender for Identity detection exclusions in Microsoft Defender XDR](/defender-for-identity/exclusions).|

| **Alert  tuning** |Alert tuning, previously known as *alert suppression*, allows you to adjust and optimize your alerts. Alert tuning reduces false positives, allowing your SOC teams to focus on high-priority alerts, and improves threat detection coverage across your system.<br><br> In Microsoft Defender XDR, create rule conditions based on evidence types, and then apply your rule on any rule type that matches your conditions. For more information, see [Tune an alert](/defender-xdr/investigate-alerts#tune-an-alert).|

| **Remediation actions** |Defender for Identity remediation actions, such as disabling accounts or requiring password resets, are available from the Microsoft Defender portal user details page. <br><br>For more information, see [Remediation actions in Microsoft Defender for Identity](/defender-for-identity/remediation-actions).

## Quick reference for legacy portal users

The following table lists the changes in navigation between Microsoft Defender for Identity and the Microsoft Defender portal.

| **Defender for** Identity  | **The Microsoft Defender portal**                                   |

| -------------------------- | ------------------------------------------------------------ |

| **Timeline**                   |- Microsoft Defender portal Alerts/Incidents queue                |

| **Reports**                    |The following types of reports are available from the **Reports** > **Identities** > **Report management** page in the Microsoft Defender portal, either for immediate download or scheduled for a periodic email delivery: <br><br>- A summary report of alerts and health issues you should take care of. <br>- A list of each time a modification is made to sensitive groups. <br>- A list of source computer and account passwords that are detected as being sent in clear text. <br> For more information, see [Report management](/defender-for-identity/reports).  |

| **Identity page**                  | Microsoft Defender portal user details page                             |

| **Device page**                | Microsoft Defender portal device details page                           |

| **Group page**                 | Microsoft Defender portal groups side pane                      |

| **Alert page**                 | Microsoft Defender portal alert details page <br><br>**Tip**: Use [alert tuning](/defender-xdr/investigate-alerts#tune-an-alert) to optimize the alerts you see in the Microsoft Defender portal.                        |

| **Search**                     | Microsoft Defender portal global search                                |

| **Health issues**              | Microsoft Defender portal **Settings > Identities > Health issues**                          |

| **Entity activities**          | - **Advanced hunting** <br>- Device page > **Timeline** <br>- Identity page > **Timeline** tab  <br>- **Group** pane > **Timeline** tab                                           |

| **Settings**                   | **Settings** -> **Identities**                                       |

| **Users and accounts**         | **Assets** -> **Identities**                                         |

| **Identity security posture**  | [Microsoft Defender for Identity's security posture assessments](/defender-for-identity/security-assessment) |

| **Onboarding a new workspace** | **Settings** -> **Identities** (automatically)                       |

| **About** | **Settings > Identities > About** |

## Next steps

For more information, see:

- [Related videos for Microsoft Defender for Identity](https://learn-video.azurefd.net/vod/player?id=f4589332-7b78-40f0-b456-b896851a5aae)

- [Microsoft Defender XDR](/defender-xdr/microsoft-365-defender)

- [Microsoft Defender for Identity](/defender-for-identity/)

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/defender-m3d-techcommunity.md)]


# Us Govt Gcc High

# Microsoft Defender for Identity for US Government offerings

The Microsoft Defender for Identity GCC High offering uses the same underlying technologies and capabilities as the commercial workspace for Defender for Identity.

## Get started with US Government offerings

The Defender for Identity GCC, GCC High, and Department of Defense (DoD) offerings are built on the Microsoft Azure Government Cloud and are designed to inter-operate with Microsoft 365 GCC, GCC High, and DoD. Use Defender for Identity public documentation as a [starting point](deploy-defender-identity.md) for deploying and operating the service.

## Licensing requirements

Defender for Identity for US Government customers requires one of the following Microsoft volume licensing offers:

| **GCC**                                   | **GCC High**                              | **DoD**                                   |

| ----------------------------------------- | ----------------------------------------- | ----------------------------------------- |

| Microsoft 365 GCC G5                      | Microsoft 365 E5 for GCC High             | Microsoft 365 G5 for DOD                  |

| Microsoft 365 G5 Security GCC             | Microsoft 365 G5 Security for GCC High    | Microsoft 365 G5 Security for DOD         |

| Standalone Defender for Identity licenses | Standalone Defender for Identity licenses | Standalone Defender for Identity licenses |

## URLs

To access Microsoft Defender for Identity for US Government offerings, use the appropriate addresses in this table:

| US Government offering | Microsoft Defender portal | Sensor (agent) endpoint                           |

|------------------------|-------------------------------|---------------------------------------------------|

|DoD                     | `security.microsoft.us`       | `<your-workspace-name>sensorapi.atp.azure.us`      |

|GCC-H                   | `security.microsoft.us`       | `<your-workspace-name>sensorapi.atp.azure.us`      |

|GCC                     | `security.microsoft.com`      | `<your-workspace-name>sensorapi.atp.gcc.azure.com` |

You can also use the IP address ranges in our Azure service tag (**AzureAdvancedThreatProtection**) to enable access to Defender for Identity. For more information about service tags, see [Virtual network service tags](/azure/virtual-network/service-tags-overview) or download [the Azure IP Ranges and Service Tags – US Government Cloud file](https://www.microsoft.com/download/details.aspx?id=57063).

## Required connectivity settings

Use [this link](prerequisites.md#required-ports) to configure the minimum internal ports necessary that the Defender for Identity sensor requires.

## How to migrate from commercial to GCC

>[!NOTE]

> The following steps should only be taken after you have initiated the transition of Microsoft Defender for Endpoint and Microsoft Defender for Cloud Apps

1. Go to the [Azure portal](https://portal.azure.com/) > Microsoft Entra ID > Groups

1. Rename the following three groups (where _workspaceName_ is the name of your workspace), by adding to them a " - commercial" suffix:

- "Azure ATP _workspaceName_ Administrators" --> "Azure ATP _workspaceName_ Administrators - commercial"

- "Azure ATP _workspaceName_ Viewers" --> "Azure ATP _workspaceName_ Viewers - commercial"

- "Azure ATP _workspaceName_ Users" --> "Azure ATP _workspaceName_ Users - commercial"

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to the Settings -> Identities section to create a new workspace for Defender for Identity

1. Configure a Directory Service account

1. Download the new sensor agent package and copy the workspace key

1. Make sure sensors have access to *.atp.gcc.azure.com (directly or through proxy)

1. Uninstall existing sensor agents from the domain controllers, AD FS servers, AD CS servers and Entra Connect servers.

1. [Reinstall sensors with the new workspace](deploy-defender-identity.md)

1. Migrate any settings after the initial sync (use the https://transition.security.microsoft.com portal in a separate browser session to compare)

1. Eventually, delete the previous workspace (historical data will be lost)

>[!NOTE]

> No data is migrated from the commercial service.

## Feature parity with the commercial environment

Unless otherwise specified, new feature releases, including preview features, documented in [What's new with Defender for Identity](whats-new.md), will be available in GCC, GCC High, and DoD environments within 90 days of release in the Defender for Identity commercial environment. Preview features may not be supported in the GCC, GCC High, and DoD environments.

## Next steps

- [Deploy Microsoft Defender for Identity with Microsoft Defender XDR](deploy-defender-identity.md)

- [Check out the Defender for Identity forum!](<https://aka.ms/MDIcommunity>)


# Deploy Defender Identity

# Microsoft Defender for Identity deployment overview

Defender for Identity uses sensors to collect signals from your on-premises identity infrastructure to detect threats.

Defender for Identity detects threats like privilege escalation or high-risk lateral movement, and reports on easily exploited identity issues like unconstrained Kerberos delegation for correction by the security team.

Install Defender for Identity sensors on all domain controllers, including read-only domain controllers (RODCs). If you have AD FS, AD CS, or Microsoft Entra Connect servers in your environment that aren't domain controllers, install the v2.x sensor on each of those servers as well.

## Select your deployment method

The sensor version you deploy depends on the server role and operating system. Use the following table to select the appropriate deployment for each server in your environment.

| Server configuration | Server Operating System | Recommended deployment |

| --------- | --------- | --------- |

|Domain controller | Windows Server 2019 or later with at least the [March 2026 Cumulative Update](https://support.microsoft.com/topic/march-10-2026-kb5078766-os-build-20348-4893-fa3ee26a-0877-47d7-a4b2-9dd632ea8cea)|[Defender for Identity sensor v3.x](deploy-sensor-v3.md)|

|Domain controller with AD FS, AD CS, or Microsoft Entra Connect identity roles   | Windows Server 2019 or later with at least the [March 2026 Cumulative Update](https://support.microsoft.com/topic/march-10-2026-kb5078766-os-build-20348-4893-fa3ee26a-0877-47d7-a4b2-9dd632ea8cea)|[Defender for Identity sensor v3.x](deploy-sensor-v3.md)|

|Domain controller | Windows Server 2016 or earlier| [Defender for Identity sensor v2.x](prerequisites-sensor-version-2.md) |

|[AD FS server that isn't a domain controller](active-directory-federation-services.md)|Windows Server 2016 or later|[Defender for Identity sensor v2.x](prerequisites-sensor-version-2.md)|

|[AD CS server that isn't a domain controller](active-directory-federation-services.md)|Windows Server 2016 or later|[Defender for Identity sensor v2.x](prerequisites-sensor-version-2.md)|

|[Microsoft Entra Connect server that isn't a domain controller](active-directory-federation-services.md)|Windows Server 2016 or later|[Defender for Identity sensor v2.x](prerequisites-sensor-version-2.md)|

Defender for Identity supports mixed environments with both v3.x and v2.x sensors. For example, you might deploy v3.x on domain controllers running Windows Server 2019 or later, and v2.x on older domain controllers or on AD FS, AD CS, and Microsoft Entra Connect servers that aren't domain controllers. Both sensor versions work together and report to the same Defender for Identity workspace.

> [!IMPORTANT]

> If any of your sensors are v3.x, select **Automatically use the sensor's local system account** for all sensors. The v3.x sensors don't use gMSA accounts configured for v2.x sensors; they always use the local system account. For more information, see [Sensor v3.x service account requirements](deploy-sensor-v3.md#service-account-requirements).

Before you activate the Defender for Identity sensor v3.x, note that v3.x:

- Requires Defender for Endpoint deployed on the server. The endpoint deployment alone isn't a prerequisite; Defender for Endpoint must be onboarded on the server where the sensor runs.

- Doesn't support VPN integration.

- Doesn't support [syslog notifications](../notifications.md#configure-syslog-notifications).

- Has limitations working with Azure ExpressRoute. For more information, see [Azure ExpressRoute for Microsoft 365](/microsoft-365/enterprise/azure-expressroute).

## Deployment steps for sensor v3.x

Follow these steps to deploy the sensor v3.x on domain controllers running Windows Server 2019 or later, including domain controllers that also run AD FS, AD CS, or Microsoft Entra Connect roles:

1. [Verify prerequisites](deploy-sensor-v3.md#before-you-activate)

1. [Activate the sensor](activate-sensor.md)

1. [Configure Windows event auditing](configure-windows-event-collection.md#configure-defender-for-identity-to-collect-windows-events-automatically)

1. [Configure RPC auditing](deploy-sensor-v3.md#configure-rpc-auditing)

1. [Validate deployment](test-sensor.md)

## Deployment steps for sensor v2.x

Follow these steps to deploy the sensor v2.x on domain controllers running Windows Server 2016 or earlier, or on AD FS, AD CS, and Microsoft Entra Connect servers that aren't domain controllers:

1. [Verify prerequisites](prerequisites-sensor-version-2.md)

1. [Plan capacity](capacity-planning.md)

1. [Configure connectivity](configure-proxy.md)

1. [Install the sensor](install-sensor.md)

1. [Configure the sensor](configure-sensor-settings.md)

1. [Configure Windows event auditing](configure-windows-event-collection.md#configure-windows-event-collection-manually)

1. [Configure Directory Service accounts](directory-service-accounts.md)

1. [Configure for AD FS, AD CS, or Entra Connect (if applicable)](active-directory-federation-services.md)

1. [Validate deployment](test-sensor.md)

## Next steps

- [Prepare your environment for sensor v3](deploy-sensor-v3.md)

- [Prepare your environment for sensor v2](prerequisites-sensor-version-2.md)


# Deploy Sensor V3

# Deploy the Defender for Identity sensor v3.x

Deploy the Defender for Identity sensor v3.x on supported domain controllers. Complete the prerequisite checks before activation, then configure auditing and identity settings afterward.

## Before you activate

Complete these checks before activating the sensor.

### Sensor version limitations

Before you activate the Defender for Identity sensor v3.x, note that v3.x:

- Doesn't support VPN integration.

- Doesn't support [syslog notifications](../notifications.md#configure-syslog-notifications).

- Has limitations working with Azure ExpressRoute. For more information, see [Azure ExpressRoute for Microsoft 365](/microsoft-365/enterprise/azure-expressroute).

- Doesn't support the migration of domain controllers running Windows Server 2025 from sensor v2.x to sensor v3.x. For more information, see [known limitations for migrating to sensor v3](migrate-to-sensor-v3.md#known-limitations).

### Server requirements

Make sure that the server on which you're activating the sensor:

- Has Defender for Endpoint deployed on the server. The Microsoft Defender Antivirus component can be in either active or passive mode. Defender for Endpoint must be onboarded on the server where the sensor runs; endpoint-only deployment isn't sufficient.

- Doesn't have a Defender for Identity sensor v2.x already deployed.

- Is running Windows Server 2019 or later.

- Includes the [Windows Server cumulative update KB5078766 (March 2026 or later)](https://support.microsoft.com/en-us/topic/march-10-2026-kb5078766-os-build-20348-4893-fa3ee26a-0877-47d7-a4b2-9dd632ea8cea).

#### Supported server types

The v3.x sensor supports domain controllers, including domain controllers with these identity roles:

- Active Directory Federation Services (AD FS)

- Active Directory Certificate Services (AD CS)

- Microsoft Entra Connect

Use the [Defender for Identity sensor v2.x](prerequisites-sensor-version-2.md) for servers that aren't domain controllers and run AD FS, AD CS, or Microsoft Entra Connect.

### Licensing requirements

Deploying Defender for Identity requires one of the following Microsoft 365 licenses:

- Enterprise Mobility + Security E5 (EMS E5/A5)

- Microsoft 365 E5 (Microsoft E5/A5/G5)

- Microsoft 365 E5/A5/G5/F5* Security

- Microsoft 365 F5 Security + Compliance*

Both F5 licenses require Microsoft 365 F1/F3 or Office 365 F3 and Enterprise Mobility + Security E3. Purchase licenses in the Microsoft 365 portal or through Cloud Solution Partner (CSP) licensing. For more information, see [Licensing and privacy FAQs](/defender-for-identity/technical-faq#licensing-and-privacy).

### Roles and permissions

- To create your Defender for Identity workspace, you need a Microsoft Entra ID tenant.

- You must either be a [Security Administrator](/entra/identity/role-based-access-control/permissions-reference), or have the following [Unified RBAC](../role-groups.md#unified-role-based-access-control-rbac) permissions:

- `System settings (Read and manage)`

- `Security settings (All permissions)`

### Network requirements

The Defender for Identity sensor uses the same URIs as Microsoft Defender for Endpoint. Review the following documents for Defender for Endpoint, based on your system's connectivity, to find the complete list of required service endpoints.

- [Microsoft Defender for Endpoint streamlined connectivity URLs](/defender-endpoint/streamlined-device-connectivity-urls-commercial?tabs=Windows)

- [Microsoft Defender for Endpoint standard connectivity URLs](/defender-endpoint/standard-device-connectivity-urls-commercial)

### Memory requirements

The following table describes memory requirements on the server running the Defender for Identity sensor, depending on the type of virtualization you're using:

| VM running on | Description |

|------------|-------------|

|Hyper-V|Ensure that **Enable Dynamic Memory** isn't enabled for the VM.|

|VMware|Ensure that the amount of memory configured and the reserved memory are the same, or select the **Reserve all guest memory (All locked)** option in the VM settings.|

|Other virtualization host|Refer to the vendor-supplied documentation on how to ensure that memory is always fully allocated to the VMs.|

> [!IMPORTANT]

> When running as a virtual machine, always allocate all memory to the virtual machine.

Version 3 of the sensor prevents the sensor from overusing CPU or memory by limiting CPU utilization at 30%, and memory usage to 1.5 GB. However, if any other service uses substantial system resources, the domain controller might still experience performance strain.

Refer to the [Defender for Identity Capacity Planning documentation](/defender-for-identity/deploy/capacity-planning) to determine whether your domain controller servers have enough resources for a Microsoft Defender for Identity sensor.

### Service account requirements

The Defender for Identity sensor interacts with Active Directory in two ways:

- **Reading AD data** (querying objects, tracking changes, resolving entities). In v2.x, this uses a Directory Service Account (DSA). In v3.x, LocalSystem handles this automatically.

- **Performing remediation actions** (disabling accounts, resetting passwords). In v2.x, this uses an action account. In v3.x, LocalSystem handles this automatically.

The v3.x sensor uses the local system identity of the server for both purposes. It doesn't use Directory Service Accounts (DSA) or group Managed Service Accounts (gMSA). LocalSystem is the only supported identity for v3.x.

If you're migrating from sensor v2.x and previously had a gMSA configured for [action accounts](manage-action-accounts.md), select **Automatically use the sensor's local system account** in the Microsoft Defender portal (**Settings** > **Identities** > **Microsoft Defender for Identity** > **Manage action accounts**). The v3.x sensors don't use gMSA accounts configured for v2.x sensors.

> [!IMPORTANT]

> If any of your sensors are v3.x, select **Automatically use the sensor's local system account** for all sensors. The v3.x sensors use the local system account regardless of gMSA configuration.

#### DSA and gMSA health alerts in environments with both v2 and v3 sensors

If your workspace still has a Directory Service Account (DSA) or group Managed Service Account (gMSA) configured because v2 sensors on AD FS, AD CS, or Entra Connect servers still require it, DSA and gMSA credentials continue to be validated on all sensors in the workspace, including v3 sensors. If validation fails, the **Directory services user credentials are incorrect** health alert appears. Workspace-level validation of DSA and gMSA credentials on all sensors is by design. Defender for Identity validates DSA and gMSA credentials at the workspace level for all sensors as long as those accounts exist, regardless of whether individual sensors use them for auditing or response actions.

V3 sensors ignore the DSA and gMSA for auditing and response actions, but they're still included in workspace-level credential validation. To stop receiving this health alert on v3 sensors, remove the workspace-level DSA or gMSA after all sensors are fully migrated to v3 and no v2 sensors require it.

### Test your prerequisites

Run the [*Test-MdiReadiness.ps1*](https://github.com/microsoft/Microsoft-Defender-for-Identity/tree/main/Test-MdiReadiness) script to test whether your environment has the necessary prerequisites.

The *Test-MdiReadiness.ps1* script is also available from Microsoft Defender XDR, on the **Identities > Tools** page (Preview).

## Activate the sensor

After confirming all prerequisites, [activate the sensor from the Microsoft Defender portal](activate-sensor.md).

## After you activate

Complete these configuration steps after the sensor is activated and running.

### Configure Windows event auditing

Defender for Identity relies on Windows event logs for many detections. For v3.x sensors on domain controllers, [enable automatic auditing](configure-windows-event-collection.md#configure-defender-for-identity-to-collect-windows-events-automatically), which handles all auditing settings without manual configuration.

If automatic auditing isn't available or you opted out, [configure auditing manually](configure-windows-event-collection.md#configure-windows-event-collection-manually) or [use PowerShell](configure-windows-event-collection.md#configure-windows-event-collection-using-powershell).

### Configure RPC auditing

To improve security visibility and enable additional identity detections, apply the **Unified Sensor RPC Audit** tag to your devices. Once applied, the configuration is enforced on all existing and future devices that match the rule criteria. The tag is visible in the Device inventory for auditing purposes.

#### Prerequisites

- Devices must run Defender for Identity sensor version 3.0.4 or later.

Devices running earlier versions don’t support this feature and won’t generate RPC auditing health alerts.

To apply the tag:

1. In the **Microsoft Defender portal**, navigate to: **System > Settings > Microsoft Defender XDR > Asset Rule Management**.

1. Select **Create a new rule**.

1. In the side panel:

1. Enter a **Rule name** and **Description**.

1. Set **rule conditions** using `Device name`, `Domain`, or `Device tag` to target the desired machines. Target domain controllers with the sensor v3.x installed.

1. Make sure that the **Defender for Identity sensor v3.x** is already deployed on the selected devices.

1. Add the **Unified Sensor RPC Audit** tag to the selected devices.

1. Select **Next** to review and finish creating the rule, and then select **Submit**. The rule might take up to one hour to take effect.

Learn more about [asset management rules](/defender-xdr/configure-asset-rules).

### Recommended settings

Use the following recommended settings to help ensure stable sensor performance:

- Set the **Power Option** of the machine running the Defender for Identity sensor to **High Performance**.

- Synchronize the time on servers and domain controllers where you install the sensor to within five minutes of each other.

## Next step

[Activate the Microsoft Defender for Identity sensor](activate-sensor.md)


# Activate Sensor

# Activate the Defender for Identity sensor v3.x on a domain controller

For complete protection of your on-premises deployment, activate the Defender for Identity sensor on all applicable servers. Onboard domain controllers running Windows Server 2019 or later, including domain controllers that also run AD FS, AD CS, or Microsoft Entra Connect roles. For domain controllers running older operating systems, or for AD FS, AD CS, and Microsoft Entra Connect servers that aren't domain controllers, [deploy the Defender for Identity sensor v2.x](install-sensor.md) instead.

## Prerequisites

See [Microsoft Defender for Identity sensor v3.x prerequisites](deploy-sensor-v3.md) for all system requirements and [sensor version limitations](deploy-sensor-v3.md#sensor-version-limitations) before proceeding with activating the Defender for Identity sensor on eligible domain controllers.

<a name="the-activation-page"></a>

## Review the Activation page

The **Activation** page displays all servers from your device inventory. Defender for Identity detects all of your servers and their configuration. Each server's activation state lets you know what you need to do to onboard that domain controller to Defender for Identity.

You can choose to activate eligible domain controllers either automatically, where Defender for Identity activates them as soon as they're discovered, or manually, by selecting specific domain controllers from the list of eligible servers.

[![Screenshot that shows how to activate a new sensor.](media/activate-sensor/blog.png)](media/activate-sensor/blog.png#lightbox)

|Activation State  |Next steps  |

|---------|---------|

|Activate new sensor |The domain controller is already onboarded to Defender for Endpoint. [Activate the sensor](#activate-the-defender-for-identity-sensor).|

|Install classic sensor|[Deploy the classic Defender for Identity sensor](install-sensor.md) from the **Sensors page**.|

|OS upgrade is required     |This domain controller is running an unsupported operating system version for the new sensor. Upgrade the OS version to the latest version. |

## Activate the Defender for Identity sensor

Perform the following steps to activate the Defender for Identity sensor on a domain controller:

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **System** > **Settings** > **Identities** > **Activation**.

1. Select the domain controller where you want to activate Defender for Identity, and select **Activate**. Confirm your selection when prompted.

[![Screenshot that shows how to activate an new server.](media/activate-sensor/image.png)](media/activate-sensor/image.png#lightbox)

1. When sensor activation for the selected domain controller is complete, a green success banner appears. In the green success banner, select **Click here to see the onboarded servers**. Selecting this link takes you to the **Sensors** page, where you can check your sensor health.

## Confirm sensor activation

To confirm the sensor is working:

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **System** > **Settings** > **Identities** > **Sensors**.

1. Check that the activated domain controller is listed.

> [!NOTE]

> The first time you activate the Defender for Identity sensor on your domain controller, it might take up to an hour for the first sensor to show as **Running** on the **Sensors** page. Subsequent activations are shown within five minutes. The activation doesn't require a restart/reboot.

## Next steps

- [Manage and update Microsoft Defender for Identity sensors](../sensor-settings.md).


# Prerequisites Sensor Version 2

# Microsoft Defender for Identity sensor v2.x prerequisites

The Defender for Identity sensor v2.x has the following requirements. The v2.x sensor supports:

- Domain controllers running Windows Server 2016 or earlier

- AD FS, AD CS, and Microsoft Entra Connect servers that aren't domain controllers

> [!TIP]

> For domain controllers running Windows Server 2019 or later, we recommend deploying the [sensor v3.x](deploy-sensor-v3.md) instead.

## Licensing requirements

Deploying Defender for Identity requires one of the following Microsoft 365 licenses:

[!INCLUDE [licenses](../includes/licenses.md)]

For more information, see [Licensing and privacy FAQs](/defender-for-identity/technical-faq#licensing-and-privacy).

## Roles and permissions

- To create your Defender for Identity workspace, you need a Microsoft Entra ID tenant.

- You must have a user with a [Security administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#available-roles) role. For more information, see [Microsoft Defender for Identity role groups](../role-groups.md).

- We recommend using at least one Directory Service account, with read access to all objects in the monitored domains. For more information, see [Configure a Directory Service account for Microsoft Defender for Identity](directory-service-accounts.md).

## Network requirements

The Defender for Identity sensor must be able to communicate with the Defender for Identity cloud service, using one of the following methods:

|Method  |Description  |Considerations |Learn more |

|---------|---------|---------|---------|

|Proxy | Customers who have a forward proxy deployed can take advantage of the proxy to provide connectivity to the MDI cloud service.<br><br> If you choose this option, you'll need to configure your proxy later in the deployment process. Proxy configurations include allowing traffic to the sensor URL, and configuring Defender for Identity URLs to any explicit allow lists used by your proxy or firewall. |  Allows access to the internet for a single URL  <br><br>SSL inspection isn't supported      |    [Configure endpoint proxy and internet connectivity settings](configure-proxy.md) <br><br>[Run a silent installation with a proxy configuration](install-sensor.md#command-for-running-a-silent-installation-with-a-proxy-configuration)   |

|ExpressRoute  | ExpressRoute can be configured to forward MDI sensor traffic over customer's express route. <br><br> To route network traffic destined to the Defender for Identity cloud servers use ExpressRoute Microsoft peering and add the Microsoft Defender for Identity (12076:5220) service BGP community to your route filter.    |  Requires ExpressRoute      |       [Service to BGP community value](/azure/expressroute/expressroute-routing#service-to-bgp-community-value)  |

|Firewall, using the Defender for Identity Azure IP addresses  | Customers who don't have a proxy or ExpressRoute can configure their firewall with the IP addresses assigned to the MDI cloud service. This requires that the customer monitor the Azure IP address list for any changes in the IP addresses used by the MDI cloud service.  <br><br> If you chose this option, we recommend that you download the [Azure IP Ranges and Service Tags – Public Cloud](https://www.microsoft.com/download/details.aspx?id=56519) file and use the **AzureAdvancedThreatProtection** service tag to add the relevant IP addresses.      |  Customer must monitor Azure IP assignments       |   [Virtual network service tags](/azure/virtual-network/service-tags-overview)      |

## Server requirements

The following table summarizes the server requirements and recommendations for the Defender for Identity sensor.

| Prerequisite / Recommendation |Description  |

|---------|---------|

|Specifications  |  Make sure to install Defender for Identity on Windows version 2016 or higher, on a domain controller server with a minimum of:<br><br>- two cores<br>- 6 GB of RAM<br>- 6 GB of disk space required, 10 GB recommended, including space for Defender for Identity binaries and logs <br><br>Defender for Identity supports read-only domain controllers (RODC).     |

|Performance   | For optimal performance, set the **Power Option** of the machine running the Defender for Identity sensor to **High Performance**.        |

|Network interface configuration | If you're using VMware virtual machines, make sure the virtual machine's NIC configuration has Large Send Offload (LSO) disabled. For more information, see [VMware virtual machine sensor issue](../troubleshooting-known-issues.md#vmware-virtual-machine-sensor-issue) for more details.|

|Maintenance window|   We recommend scheduling a maintenance window for your domain controllers, as a restart might be required if the installation runs and a restart is already pending, or if .NET Framework needs to be installed. <br><br>If .NET Framework version 4.7 or later isn't already found on the system, .NET Framework version 4.7 is installed, and might require a restart.      |

|AD FS federation servers     |In AD FS environments, Defender for Identity sensors are supported only on the federation servers. They're not required on Web Application Proxy (WAP) servers.       |

|Microsoft Entra Connect servers     |For Microsoft Entra Connect servers, you need to install the sensors on both active and staging servers.       |

|AD CS servers    |Defender for Identity sensor for AD CS supports only AD CS servers with Certification Authority Role Service. You don't need to install sensors on any AD CS servers that are offline.       |

|Time synchronization|The servers and domain controllers onto which the sensor is installed must have time synchronized to within five minutes of each other.|

### Minimum operating system requirements

[!INCLUDE [server-requirements](../includes/server-requirements.md)]

#### Legacy operating systems

Windows Server 2012 and Windows Server 2012 R2 reached extended end of support on October 10, 2023. Sensors running on these operating systems continue to report to Defender for Identity and even receive the sensor updates, but some functionality that relies on operating system capabilities might not be available. We recommend that you upgrade any servers using these operating systems.

### Required ports

To enable the Defender for Identity sensor to communicate with the cloud service, allow outbound HTTPS traffic to your workspace sensor API URL in the following format: `https://<your-workspace-name>sensorapi.atp.azure.com`. For example, if your workspace name is "Contoso", allow traffic to `https://contoso-corpsensorapi.atp.azure.com`.

|Protocol   |Transport         |Port         |From       |To   |Notes|

|------------|---------|---------|-------|--------------|------|

|Internet ports       | | | | |  |

|SSL (\*.atp.azure.com)   |TCP      |443 |Defender for Identity sensor|Defender for Identity cloud service|Alternately, [configure access through a proxy](configure-proxy.md).|

|Internal ports          | | | | |  |

|DNS     |TCP and UDP           |53  |Defender for Identity sensor|DNS Servers           |

|RADIUS         |UDP      |1813|RADIUS         |Defender for Identity sensor      |  |

|Localhost port    | | | | |Required for the sensor service updater. By default, *localhost* to *localhost* traffic is allowed unless a custom firewall policy blocks it.|

|SSL|TCP      |444 |Sensor service|Sensor updater service            |   |

|Network Name Resolution (NNR) ports    | | | | |To resolve IP addresses to computer names, we recommend opening all ports listed. However, only one port is required. |

|NTLM over RPC |TCP      |Port 135         |Defender for Identity sensor|All devices on network (DCs, ADFS, ADCS, and Microsoft Entra Connect)|  |

|NetBIOS        |UDP      |137 |Defender for Identity sensor|All devices on network (DCs, ADFS, ADCS, and Microsoft Entra Connect)|  |

|RDP      |TCP      |3389 |Defender for Identity sensor|All devices on network (DCs, ADFS, ADCS, and Microsoft Entra Connect)|Only the first packet of **Client hello** queries the DNS server using reverse DNS lookup of the IP address (UDP 53)|

If you're working with [multiple forests](multi-forest.md), make sure that the following ports are opened on any machine where a Defender for Identity sensor is installed:

|Protocol|Transport|Port|To/From|Direction|

|----|----|----|----|----|

|Internet ports||||

|SSL (*.atp.azure.com)|TCP|443|Defender for Identity cloud service|Outbound|

|Internal ports||||

|LDAP|TCP and UDP|389|Domain controllers|Outbound|

|Secure LDAP (LDAPS)|TCP|636|Domain controllers|Outbound|

|LDAP to Global Catalog|TCP|3268|Domain controllers|Outbound|

|LDAPS to Global Catalog|TCP|3269|Domain controllers|Outbound|

> [!TIP]

> By default, Defender for Identity sensors query the directory using LDAP on ports 389 and 3268. To switch to LDAPS on ports 636 and 3269, open a support case. For more information, see [Microsoft Defender for Identity support](../support.md).

### Memory requirements

The following table describes memory requirements on the server used for the Defender for Identity sensor, depending on the type of virtualization you're using:

|VM running on|Description|

|------------|-------------|

|Hyper-V|Ensure that **Enable Dynamic Memory** isn't enabled for the VM.|

|VMware|Ensure that the amount of memory configured and the reserved memory are the same, or select the **Reserve all guest memory (All locked)** option in the VM settings.|

|Other virtualization host|Refer to the vendor supplied documentation on how to ensure that memory is fully allocated to the VM at all times. |

> [!IMPORTANT]

> When running as a virtual machine, all memory must be allocated to the virtual machine at all times.

## Configure Windows event auditing

Defender for Identity detections rely on specific Windows event log entries to enhance detections and provide extra information about the users performing specific actions, such as NTLM sign-ins and security group modifications.

[Configure Windows event auditing](configure-windows-event-collection.md) on your domain controller to support Defender for Identity detections in the Defender portal or using PowerShell.

## Test your prerequisites

We recommend running the [*Test-MdiReadiness.ps1*](https://github.com/microsoft/Microsoft-Defender-for-Identity/tree/main/Test-MdiReadiness) script to test and see if your environment has the necessary prerequisites.

The *Test-MdiReadiness.ps1* script is also available from Microsoft Defender XDR, on the **Identities > Tools** page (Preview).

## Next step

[Plan capacity for Microsoft Defender for Identity](capacity-planning.md)


# Capacity Planning

# Plan capacity for Microsoft Defender for Identity deployment

> [!NOTE]

> The capacity planning tool was designed for version 2.x of the sensor due to its resource-intensive network processes. Sensor v3.x does not require a sizing tool since it relies mainly on Windows events and event tracing, which significantly reduces resource requirements.

Use the Microsoft Defender for Identity sizing tool to determine whether your domain controller servers have enough resources for a Microsoft Defender for Identity sensor v2. Before you run the sizing tool, review the [Prerequisites](#prerequisites) section later in this article.

While domain controller performance may not be affected if the server doesn't have required resources, the Defender for Identity sensor may not operate as expected. For more information, see [Microsoft Defender for Identity prerequisites](prerequisites-sensor-version-2.md).

The sizing tool measures the capacity needed for domain controllers only. There is no need to run it against servers that are only AD FS, AD CS, or Entra Connect (unless those servers also function as a domain controller), as the performance impact on these servers is extremely minimal to not existent.

> [!TIP]

> By default, Defender for Identity supports up to 1000 sensors. To install more sensors, contact Defender for Identity support.

## Prerequisites

Before you run the sizing tool, complete the following prerequisites:

- Download the [Defender for Identity sizing tool](<https://aka.ms/mdi/sizingtool>).

- Review the [Defender for Identity prerequisites](prerequisites-sensor-version-2.md).

To ensure accurate results, only run the sizing tool *before* you've installed any Defender for Identity sensors in your environment.

## Use the sizing tool

1. Run the Defender for Identity sizing tool, **TriSizingTool.exe**, from the zip file you downloaded.

1. When the tool finishes running, open the Excel file results.

1. In the Excel file, locate and select the **Azure ATP Summary** sheet, and then check the **Sensor Supported** column for results that indicate whether your server is supported.

For example:

> [!NOTE]

> The other sheet in the file is used for [Advanced Threat Analytics (ATA)](/advanced-threat-analytics/what-is-ata) planning and isn't needed for Defender for Identity.

>

The sizing tool determines whether your server is supported based on the **Busy Packets/Second** value, which is calculated based on the 15 busiest minutes over a 24 hour period.

Common results include:

|Result  |Description  |

|---------|---------|

|**Yes**     |   The sensor is supported on your server.      |

|**Yes, but additional resources required** | The sensor is supported on your server as long you add any specified missing resources.  |

|**Maybe**     |     The current **Busy Packets/sec** value may be significantly higher at that point than average. Check the timestamps to understand the processes running at that time, and whether you can limit the bandwidth for those processes under normal circumstances.     |

|**Maybe, but additional resources required** |The sensor may be supported on your server as long you add any specified missing resources, or the **Busy packets/sec** may be above 60K. |

|**No**     |    The sensor isn't supported on your server. <br><br>The current **Busy Packets/sec** value may be significantly higher at that point than average. Check the timestamps to understand the processes running at that time, and whether you can limit the bandwidth for those processes under normal circumstances.    |

|**Missing OS Data**     |  There was an issue reading the operating system data. Make sure the connection to your server is able to query WMI remotely.   |

|**Missing Traffic Data**     | There was an issue reading the traffic data. Make sure the connection to your server is able to query performance counters remotely.        |

|**Missing RAM data**     |    There was an issue reading the RAM data. Make sure the connection to your server is able to query WMI remotely.       |

|**Missing core data**     |   There was an issue reading the core data. Make sure the connection to your server is able to query WMI remotely.          |

For example, the following image shows a set of results where the **Maybe** indicates that the **Busy Packets/sec** value is significantly higher at that point than average.  Note that the **Display DC Times as UTC/Local** is set to *Local DC Time*. This setting helps highlight the fact that the values were taken at around 3:30 AM.

<a name="sizing"></a>

## Defender for Identity sensor estimated sizing

The following table shows the estimated CPU and RAM capacity needed for a Defender for Identity sensor, based on the typical amount of network traffic generated by a domain controller.

**This table is an estimate. The final amount that the sensor parses is dependent on the amount of traffic and the distribution of traffic.**

|Busy packets / second|CPU (physical cores)|RAM (GB)|

|----|----|-----|

|0-1k|0.25|2.50|

|1k-5k|0.75|6.00|

|5k-10k|1.00|6.50|

|10k-20k|2.00|9.00|

|20k-50k|3.50|9.50|

|50k-75k |5.50|11.50|

|75k-100k|7.50|13.50|

In this table:

- CPU and RAM capacity refers to the **sensor's own consumption**, not the domain controller capacity.

- CPU capacity doesn't include hyper-threaded cores. We recommend that you don't work with hyper-threaded cores, which can result in health issues in the Defender for Identity sensor.

When determining sizing, keep in mind the total number of cores and total amount of memory that will be used by the sensor service.

## Manual sizing estimation for domain controllers

If you're unable to use the Defender for Identity sizing tool described earlier in this article, you can manually estimate whether your domain controller servers have enough resources for a Defender for Identity sensor instead.

Manually gather the packet/second counter information from all your domain controllers, over 24 hours with a low collection interval like 5 seconds. For each domain controller, calculate the daily average and the busiest period (15 minutes) average.

Various tools can help you discover the average packet/second counter for your domain controller. This procedure describes an example of how to use Performance Monitor to gather packet-per-second counter data for your domain controllers.

1. Open Performance Monitor and expand **Data Collector Sets**.

1. Right-click **User Defined** and select **New > Data Collector Set**.

1. Enter a meaningful name for the collector set and select **Create Manually (Advanced)**.

1. Under **What type of data do you want to include?**, select  **Create data logs, and Performance counter**.

1. Expand **Network Adapter** and then select **Packets/sec** and the relevant workspace. If you're not sure which workspace to select, select **&lt;All workspaces&gt;**. Select **Add** > **OK** to complete the step.

Alternately, if you're performing this step from the command line, run `ipconfig /all` to see the adapter name and configuration.

1. Change the **Sample interval** to **five seconds**, and define where you want the data to be saved.

1. Under **Create the data collector set**,  select **Start this data collector set now** > **Finish**.

You should now see the data collector set you created with a green triangle indicating that it's working.

1. After 24 hours, stop the data collector set. Right-click the data collector set and select **Stop**.

1. In File Explorer, browse to the folder where the **.blg** file was saved. Double-click it to open it in Performance Monitor.

1. Select the **Packets/sec** counter, and record the average and maximum values.

> [!NOTE]

> By default, Defender for Identity supports up to 350 sensors. If you want to install more sensors, contact Defender for Identity support.

> [!IMPORTANT]

> If your domain controller runs low on available memory, a corresponding health issue will appear in the Defender for Identity portal to alert you of this condition. Learn more about [Defender for Identity health alerts](../health-alerts.md).

## Next step

> [!div class="step-by-step"]

> [Configure endpoint proxy and internet connectivity settings »](configure-proxy.md)


# Multi Forest

# Microsoft Defender for Identity multi-forest considerations

Microsoft Defender for Identity supports organizations with multiple Active Directory forests, giving you the ability to easily monitor activity and profile users across forests.

Enterprise organizations typically have several Active Directory forests - often used for different purposes, including legacy infrastructure from corporate mergers and acquisitions, geographical distribution, and security boundaries (red forests).

Securing your multiple Active Directory forests with Defender for Identity provides the following advantages:

- **View and investigate** activities performed by users across multiple forests from a single location

- **Gain improved detection** and reduce false positives with advanced Active Directory integration and account resolution

- **Gain greater control and easier deployment**, with an improved set of health issues and reporting for cross-org coverage when your domain controllers are all monitored from a single Defender for Identity server

> [!NOTE]

> Each Defender for Identity sensor can only report to a single Defender for Identity workspace.

## Detection activity across multiple forests

To detect cross-forest activities, Defender for Identity sensors query domain controllers in remote forests to create profiles for all entities involved, including users and computers from remote forests.

- Defender for Identity sensors can be installed on domain controllers in all forests, even forests with no trust.

- [Add additional credentials](create-directory-service-account-gmsa.md#configure-a-directory-service-account-in-microsoft-defender-portal) on the **Directory services accounts** page to support any untrusted forests in your environment.

- Only one credential is required to support all forests with a two-way trust.

- Additional credentials are required for each forest with non-Kerberos trust or no trust.

- There's a default limit of 30 credentials per Defender for Identity workspace. [Contact support](../support.md) if you need to add more than 30 credentials.

For more information, see [Microsoft Defender for Identity Directory Service account recommendations](directory-service-accounts.md).

## Network traffic impact for multi-forest support

When Defender for Identity maps your forests, it uses the following process:

1. After the Defender for Identity sensor starts running, the sensor queries the remote Active Directory forests and retrieves a list of users and machine data for profile creation.

1. Every 5 minutes, each Defender for Identity sensor queries one domain controller from each domain, from each forest, to map all the forests in the network.

The Defender for Identity sensors map the forests using the `trustedDomain` Active Directory object, by signing in and checking the trust type.

You may see ad-hoc traffic when the Defender for Identity sensor detects cross forest activity. When this occurs, the Defender for Identity sensors will send an LDAP query to the relevant domain controllers to retrieve entity information.

## Related content

- [Deploy Microsoft Defender for Identity with Microsoft Defender](deploy-defender-identity.md)

- [Microsoft Defender for Identity prerequisites](prerequisites-sensor-version-2.md)

- [Directory Service Accounts for Microsoft Defender for Identity](directory-service-accounts.md)


# Configure Proxy

# Connect to the Defender for Identity service

Each Microsoft Defender for Identity sensor requires internet connectivity to the Defender for Identity cloud service to report sensor data and operate successfully.

In some organizations, the domain controllers aren't directly connected to the internet, but are connected through a web proxy connection, and SSL inspection and intercepting proxies are not supported for security reasons. In such cases, your proxy server must allow sensor traffic to pass directly from the Defender for Identity sensors to the relevant URLs without interception.

> [!IMPORTANT]

> Microsoft does not provide a proxy server. This article describes how to ensure that the required URLs are accessible via a proxy server that you configure.

## Enable access to Defender for Identity service URLs in the proxy server

To ensure maximal security and data privacy, Defender for Identity uses certificate-based, mutual authentication between each Defender for Identity sensor and the Defender for Identity cloud back-end. SSL inspection and interception are not supported, because these proxy behaviors interfere in the authentication process.

To enable access to Defender for Identity, make sure to allow traffic to the sensor URL, using the following syntax: `<your-workspace-name>sensorapi.atp.azure.com`. For example, `contoso-corpsensorapi.atp.azure.com`.

- To get your workspace name, see the [Defender for Identity settings page](https://security.microsoft.com/settings/identities) in the Microsoft Defender portal.

- If your proxy or firewall uses explicit allowlists, we also recommend ensuring that the following URLs are allowed:

- `crl.microsoft.com`

- `ctldl.windowsupdate.com`

- `www.microsoft.com/pkiops/*`

- `www.microsoft.com/pki/*`

- Occasionally, the Defender for Identity service IP addresses may change. If you manually configure IP addresses, or if your proxy automatically resolves DNS names to their IP address and uses them, we recommend that you periodically check that the configured IP addresses are still up-to-date.

- If you've previously configured your proxy using legacy options, including WiniNet or a registry key update, you'll need to make any changes using the method you used originally. For more information, see [Change proxy configuration using legacy methods](#change-proxy-configuration-using-legacy-methods).

### Enable access with a service tag

Instead of manually enabling access to specific endpoints, download the [Azure IP Ranges and Service Tags - Public Cloud](https://www.microsoft.com/download/details.aspx?id=56519), and use the IP address ranges in the **AzureAdvancedThreatProtection** Azure service tag to enable access to Defender for Identity.

For more information, see [Virtual network service tags](/azure/virtual-network/service-tags-overview). For US Government offerings, see [Get started with US Government offerings](../us-govt-gcc-high.md).

## Change proxy configuration using the CLI

**Prerequisites**: Locate the `Microsoft.Tri.Sensor.Deployment.Deployer.exe` file. This file is located together with the sensor installation. By default, this location is `C:\Program Files\Azure Advanced Threat Protection Sensor\version number\`

**To change the current sensor's proxy configuration**:

```cmd

Microsoft.Tri.Sensor.Deployment.Deployer.exe ProxyUrl="http://myproxy.contoso.local" ProxyUserName="CONTOSO\myProxyUser" ProxyUserPassword="myPr0xyPa55w0rd"

```

**To remove the current sensor's proxy configuration entirely**:

```cmd

Microsoft.Tri.Sensor.Deployment.Deployer.exe ClearProxyConfiguration

```

## Change proxy configuration using PowerShell

**Prerequisites**: Before running Defender for Identity PowerShell commands, make sure that you've downloaded the [Defender for Identity PowerShell module](https://www.powershellgallery.com/packages/DefenderForIdentity/).

You can view and change the proxy configuration for your sensor using PowerShell. To do so, sign into your sensor server and run commands as shown in the following examples:

**To view the current sensor's proxy configuration**:

```powershell

Get-MDISensorProxyConfiguration

```

**To change the current sensor's proxy configuration**:

```powershell

Set-MDISensorProxyConfiguration -ProxyUrl 'http://proxy.contoso.com:8080'

```

The preceding command sets the proxy configuration for the Defender for Identity sensor to use the specified proxy server without any credentials.

**To remove the current sensor's proxy configuration entirely**:

```powershell

Clear-MDISensorProxyConfiguration

```

For more information, see the following [DefenderForIdentity PowerShell references](/powershell/defenderforidentity/overview-defenderforidentity):

- [Get-MDISensorProxyConfiguration](/powershell/module/defenderforidentity/get-mdisensorproxyconfiguration)

- [Set-MDISensorProxyConfiguration](/powershell/module/defenderforidentity/set-mdisensorproxyconfiguration)

- [Clear-MDISensorProxyConfiguration](/powershell/module/defenderforidentity/clear-mdisensorproxyconfiguration)

## Change proxy configuration using legacy methods

If you'd previously configured your proxy settings via either WinINet or a registry key and need to update them, you'll need to use the matching method: update WinINet settings through WinINet, or update registry-based settings through the registry.

While configuring your proxy from the command line during installation ensures that only the Defender for Identity sensor services communicate through the proxy, using WinINet or a registry allow other services running under the LocalSystem or LocalService accounts to also direct traffic through the proxy.

### Configure a proxy server using WinINet

When configuring the proxy using WinINet, keep in mind that the embedded Defender for Identity sensor service runs in system context using the **LocalService** account, and that the Defender for Identity Sensor updater service runs in the system context using **LocalSystem** account.

- If you use WinHTTP for proxy configuration, you still need to configure Windows Internet (WinINet) browser proxy settings for communication between the sensor and the Defender for Identity cloud service.

- If you're using Transparent proxy or WPAD in your network topology, you don't need to configure WinINet for your proxy.

### Configure a proxy server using the registry

The following procedure describes how to configure a static proxy server manually by using a registry-based static proxy.

> [!IMPORTANT]

> Configuring a proxy via the registry affects all applications that use WinINet with the **LocalService** and **LocalSystem** accounts, including Windows services.

>

> Apply registry changes only to the **LocalService** and **LocalSystem** accounts.

>

To configure your proxy, copy your proxy configuration in user context to the **LocalSystem** and **LocalService** accounts as follows:

1. Back up your registry keys.

1. In the registry, search for the `DefaultConnectionSettings` value as `REG_BINARY`, under the `HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` registry key, and copy it.

1. If the `LocalSystem` doesn't have the correct proxy settings, copy the proxy setting from the `Current_User` to the `LocalSystem`, under the `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` registry key.

Make sure to paste the value from the `Current_User`'s `DefaultConnectionSettings` registry key as `REG_BINARY`.

This may happen if your proxy settings aren't configured, or if they're different from the `Current_User`.

1. If the `LocalService` doesn't have the correct proxy settings, then copy the proxy setting from the `Current_User` to the `LocalService`, under the `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` registry key.

Make sure to paste the value from the `Current_User`'s `DefaultConnectionSettings` registry key as `REG_BINARY`.

## Next step

> [!div class="step-by-step"]

> [Test Microsoft Defender for Identity connectivity »](test-connectivity.md)


# Test Connectivity

# Test Microsoft Defender for Identity connectivity

The Defender for Identity sensor requires network connectivity to the Defender for Identity service. Depending on which version of the sensor you deployed, see [Sensor v2.x prerequisites](prerequisites-sensor-version-2.md) or [Sensor v3.x prerequisites](prerequisites-sensor-version-2.md).

After preparing the server that you're going to use for your Microsoft Defender for Identity sensor we recommend that you test connectivity to make sure that your server can access the Defender for Identity cloud service. Use the connectivity test procedures below even after deploying if your sensor server is experiencing connectivity issues.

For more information, see [Required ports](../prerequisites.md#ports).

> [!NOTE]

> To get the name and other important details about your Defender for Identity workspace, see the [About page](../settings-about.md) in the [Microsoft Defender XDR](https://security.microsoft.com/) portal.

## Test connectivity using a browser

Perform the following steps to test sensor connectivity from a browser:

1. Open a browser. If you're using a proxy, make sure that your browser uses the same proxy settings being used by the sensor.

For example, if the proxy settings are defined for **Local System**, you'll need to use PSExec to open a session as **Local System** and open the browser from that session.

1. Browse to the following URL: `https://<your_workspace_name>sensorapi.atp.azure.com/tri/sensor/api/ping`. Replace `<your_workspace_name>` with the name of your Defender for Identity workspace.

> [!IMPORTANT]

> You must specify `HTTPS`, not `HTTP`, to properly test connectivity.

**Result**: You should get the latest sensor version number, which indicates you were successfully able to route to the Defender for Identity HTTPS endpoint. This is the desired result.

For some older workspaces, the message returned could be *Error 503 The service is unavailable*. This is a temporary state that still indicates success. For example:

Other results might include the following scenarios:

- If you don't get *Ok* message, then you may have a problem with your proxy configuration. Check your network and proxy settings.

- If you get a certificate error, ensure that you have the required trusted root certificates installed before continuing. For more information, see [Proxy authentication problem presents as a connection error](../troubleshooting-known-issues.md#proxy-authentication-problem-presents-as-a-connection-error). The certificate details should look like this:

## Test service connectivity using PowerShell

**Prerequisites**: Before running Defender for Identity PowerShell commands, make sure that you downloaded the [Defender for Identity PowerShell module](https://www.powershellgallery.com/packages/DefenderForIdentity/).

Sign into your server and run one of the following commands:

- To use the current server's settings, run:

```powershell

Test-MDISensorApiConnection

```

- To test settings that you're planning on using, but aren't currently configured on the server, run the command using the following syntax:

```powershell

Test-MDISensorApiConnection -BypassConfiguration -SensorApiUrl 'https://contososensorapi.atp.azure.com' -ProxyUrl 'https://myproxy.contoso.com:8080' -ProxyCredential $credential

```

Where:

- `https://contososensorapi.atp.azure.com` is an example of your sensor URL, where *contoso* is the name of your workspace.

- `https://myproxy.contoso.com:8080` is an example of your proxy URL

For more information, see the [MDI PowerShell documentation](/powershell/module/defenderforidentity/test-mdisensorapiconnection).

<a name="next-step"></a>

## Next steps

> [!div class="step-by-step"]

> [Download and install the Microsoft Defender for Identity sensor](install-sensor.md)


# Install Sensor

# Download and install a Microsoft Defender for Identity sensor v2.x

Download and install the Defender for Identity sensor v2.x on domain controllers, or on AD FS, AD CS, and Microsoft Entra Connect servers that aren't domain controllers. Standalone sensor installation is also covered in [Install the v2.x sensor in the Defender portal](#install-the-v2x-sensor-in-the-defender-portal). Before you begin, review the [prerequisites](#prerequisites), including .NET Framework, server specifications, and certificate requirements.

> [!TIP]

> For domain controllers running Windows Server 2019 or later, deploy the [Defender for Identity sensor v3.x](deploy-sensor-v3.md) instead. The v3.x sensor is activated from the Defender portal and doesn't require a downloaded installation package.

We recommend alternate installation methods for these use cases:

- When you're installing the sensor on Windows Server Core, or to deploy the sensor via a software deployment system, follow the steps to [perform a Defender for Identity silent installation](#perform-a-defender-for-identity-silent-installation) instead.

- If you're using a proxy, we recommend that you install the sensor and configure your proxy together by [running a silent installation with proxy configuration](#command-for-running-a-silent-installation-with-a-proxy-configuration). If you need to update your proxy settings later on, use PowerShell or the Azure CLI. For more information, see [Configure endpoint proxy and internet connectivity settings](configure-proxy.md).

## Prerequisites

Before you start, make sure that you have:

- Microsoft .NET Framework 4.7 or later installed on the machine. If Microsoft .NET Framework 4.7 or later isn't installed, the Defender for Identity sensor setup package installs it. Installation from the setup package might require a restart of the server.

- Relevant server specifications and network requirements. For more information, see:

- [Microsoft Defender for Identity prerequisites](prerequisites-sensor-version-2.md)

- [Configure sensors for AD FS, AD CS, and Microsoft Entra Connect](active-directory-federation-services.md)

- [Microsoft Defender for Identity standalone sensor prerequisites](prerequisites-standalone.md)

- Trusted root certificates on your machine. If your trusted root CA-signed certificates are missing, you might receive a connection error. For more information, see [Troubleshoot proxy authentication connection errors](../troubleshooting-known-issues.md#proxy-authentication-problem-presents-as-a-connection-error).

## Download the sensor package

1. In [Microsoft Defender XDR](https://security.microsoft.com), go to **System > Settings** > **Identities**.

1. Select the **Sensors** tab, which displays all of your Defender for Identity sensors. For example:

1. Select **Add sensor**. In the Add a new sensor pane, select **Continue with classic sensor**, and save the installation package locally. The downloaded zip file includes the following files:

- The Defender for Identity sensor installer

- The configuration setting file with the required information to connect to the Defender for Identity cloud service

- [Npcap OEM version 1.0](https://npcap.com/), automatically installed during the sensor installation

1. In the **Add a new sensor** pane, copy the **Access key** value and save it to a secured location. This access key is a one-time password for use when deploying the sensor, after which communication is performed using certificates for authentication and TLS encryption.

> [!TIP]

> We recommend regenerating the access key using the **Regenerate key** button regularly. It won't affect any previously deployed sensors, because it's only used for initial registration of the sensor.

1. Copy the downloaded installation package to the dedicated server or domain controller where you're installing the Defender for Identity sensor.

> [!Note]

> To download the installation package behind a firewall or proxy server, make sure you allow network traffic to the following FQDNs through TCP/443.

>

> sensorpackage-prd.mdi.securitycenter.microsoft.com

> sensorpackage-fm.mdi.securitycenter.microsoft.us

> sensorpackage-ff.mdi.securitycenter.microsoft.us

## Install the v2.x sensor in the Defender portal

Perform the following steps on the domain controller, Active Directory Federation Services (AD FS) server, Active Directory Certificate Services (AD CS) server, or Microsoft Entra Connect server.

1. Verify that the machine has connectivity to the relevant [Defender for Identity cloud service endpoints](configure-proxy.md#enable-access-to-defender-for-identity-service-urls-in-the-proxy-server).

1. Extract the installation files from the .zip file. Installing directly from the .zip file fails.

1. Run **Azure ATP sensor setup.exe** with elevated privileges (**Run as administrator**) and follow the setup wizard.

1. On the **Welcome** page, select your language and then select **Next**.

![Screenshot of the Welcome page showing language selection for the Defender for Identity sensor installation wizard.](../media/sensor-install-language.png)

The installation wizard automatically checks if the server is a domain controller, an AD FS server, an AD CS server, or a dedicated server. The server type determines the sensor type:

- If the server is a domain controller, AD FS server, or AD CS server, the Defender for Identity sensor is installed.

- If the server is dedicated, the Defender for Identity standalone sensor is installed.

For example, the wizard displays the following page to indicate that a Defender for Identity sensor is installed on domain controllers.

![Screenshot of the deployment type page showing that the Defender for Identity sensor is selected for installation on a domain controller.](../media/sensor-install-deployment-type.png)

1. Select **Next**.

The wizard issues a warning if the domain controller, AD FS server, AD CS server, or dedicated server doesn't meet the minimum hardware requirements for the installation.

The warning doesn't prevent you from selecting **Next** and proceeding with the installation, which might still be the right option. For example, you need less room for data storage when you're installing a small lab test environment.

For production environments, we highly recommend working with the [Defender for Identity sizing tool](capacity-planning.md) to make sure your domain controllers or dedicated servers meet the capacity requirements.

1. On the **Configure the sensor** page, enter the following information for the setup package:

- **Installation path**: The location where the Defender for Identity sensor is installed. By default, the path is `%programfiles%\Azure Advanced Threat Protection sensor`. Leave the default value.

- **Access key**: The one-time key copied from the **Add a new sensor** pane in Microsoft Defender XDR when you [downloaded the sensor package](#download-the-sensor-package). For details, see [Download the sensor package](#download-the-sensor-package).

![Screenshot of the Configure the sensor page showing the Installation path and Access key fields for the Defender for Identity sensor setup package.](../media/sensor-install-config.png)

1. Select **Install**. The following components are installed and configured during the installation of the Defender for Identity sensor:

- **Defender for Identity sensor service** and **Defender for Identity sensor updater service**

- **Npcap OEM version 1.0**

> [!IMPORTANT]

> Npcap OEM version 1.0 is automatically installed if no other version of Npcap is present. If you already have Npcap installed due to other software requirements or for any other reason, ensure that it's version 1.0 or later and that it has the [required settings for Defender for Identity](../technical-faq.yml#how-do-i-download-and-install-or-upgrade-the-npcap-driver).

### Viewing sensor versions

Beginning with sensor version 2.176, when you're installing the sensor from a new package, the version under **Add/Remove Programs** appears with the full number, such as **2.176.x.y**. Previously, the version appeared as the static **2.0.0.0**.

The version shown under **Add/Remove Programs** continues to appear even after the Defender for Identity cloud services run automatic updates.

View the sensor's real version on the Microsoft Defender XDR [sensor settings page](https://security.microsoft.com/settings/identities?tabid=sensor), in the executable path or in the file version.

## Perform a Defender for Identity silent installation

The Defender for Identity silent installation for sensors is configured to automatically restart the server at the end of the installation, if necessary.

Schedule a silent installation only during a maintenance window. Because of a Windows Installer bug, you can't reliably use the `norestart` flag to make sure the server doesn't restart.

To track your deployment progress, monitor the Defender for Identity installer logs in `%localappdata%\Temp`.

### Silent installation via a deployment system

When you're silently deploying a Defender for Identity sensor via System Center Configuration Manager or another software deployment system, we recommend that you create two deployment packages:

- .NET Framework 4.7 or later, which might include restarting the domain controller

- The Defender for Identity sensor

Make the Defender for Identity sensor package dependent on the deployment of the .NET Framework package deployment. If necessary, get the [.NET Framework 4.7 offline deployment package](https://support.microsoft.com/topic/the-net-framework-4-7-offline-installer-for-windows-f32bcb33-5f94-57ce-6120-62c9526a91f2).

### Commands for running a silent installation

Use the following commands to perform a fully silent installation of the Defender for Identity sensor, by using the access key you copied in [Download the sensor package](#download-the-sensor-package).

#### cmd.exe syntax

Use the following cmd.exe syntax for a silent installation:

```cmd

"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"

```

#### PowerShell syntax

Use the following PowerShell syntax for a silent installation:

```powershell

.\"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"

```

> [!NOTE]

> When you're using the PowerShell syntax, omitting the `.\` preface results in an error that prevents silent installation.

#### Installation options

|Name|Syntax|Mandatory for silent installation?|Description|

|-------------|----------|---------|---------|

|`Quiet`|`/quiet`|Yes|Runs the installer without displaying UI or prompts.|

|`Help`|`/help`|No|Provides help and quick reference. Displays the correct use of the setup command, including a list of all options and behaviors.|

|`NetFrameworkCommandLineArguments="/q"`|`NetFrameworkCommandLineArguments="/q"`|Yes|Specifies the parameters for the .NET Framework installation. Must be set to enforce the silent installation of .NET Framework.|

#### Installation parameters

|Name|Syntax|Mandatory for silent installation?|Description|

|-------------|----------|---------|---------|

|`InstallationPath`|`InstallationPath=""`|No|Sets the path for the installation of Defender for Identity sensor binaries. Default path: `%programfiles%\Azure Advanced Threat Protection Sensor`. |

|`AccessKey`|`AccessKey="\*\*"`|Yes|Sets the access key that's used to register the Defender for Identity sensor with the Defender for Identity workspace.|

|`AccessKeyFile`|`AccessKeyFile=""`|No|Sets the workspace access key from the provided text file path.|

|`DelayedUpdate`|`DelayedUpdate=true`|No|Sets the sensor's update mechanism to delay the update for 72 hours from the official release of each service update. For more information, see [Delayed sensor update](../sensor-settings.md#delayed-update-for-sensor-v2x).|

|`LogsPath`|`LogsPath=""`|No|Sets the path for the Defender for Identity sensor logs. Default path: `%programfiles%\Azure Advanced Threat Protection Sensor`.|

#### Examples

Use the following command to silently install the Defender for Identity sensor with the access key passed directly on the command line:

```cmd

"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<access key value>"

```

Alternatively, use the following command to read the access key from a text file, which avoids exposing the key in process history:

```cmd

"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKeyFile="C:\Path\myAccessKeyFile.txt"

```

### Command for running a silent installation with a proxy configuration

Use the following command to configure your proxy together with a silent installation:

```cmd

"Azure ATP sensor Setup.exe" [/quiet] [/Help] [ProxyUrl="http://proxy.internal.com"] [ProxyUserName="domain\proxyuser"] [ProxyUserPassword="ProxyPassword"]`

```

> [!NOTE]

> If you previously configured your proxy by using legacy options, including WinINet or a registry key update, you need to make any changes with the same method that you used originally. For more information, see [Change proxy configuration using legacy methods](configure-proxy.md#change-proxy-configuration-using-legacy-methods).

#### Installation parameters

|Name|Syntax|Mandatory for silent installation?|Description|

|-------------|----------|---------|---------|

|`ProxyUrl`|`ProxyUrl="http://proxy.contoso.com:8080"`|No|Specifies the proxy URL and port number for the Defender for Identity sensor.|

|`ProxyUserName`|`ProxyUserName="Contoso\ProxyUser"`|No|If your proxy service requires authentication, define a username in the `DOMAIN\user` format.|

|`ProxyUserPassword`|`ProxyUserPassword="P@ssw0rd"`|No|Specifies the password for your proxy username. <br><br>The Defender for Identity sensor encrypts credentials and stores them locally.|

> [!TIP]

> If you need to update your proxy settings later on, use PowerShell or the Azure CLI. For more information, see [Configure endpoint proxy and internet connectivity settings](configure-proxy.md). We recommend that you create and use a custom DNS A record for the proxy server. You can then use that record to change the proxy server's address when necessary and use the *hosts* file for testing.

## Related content

After you install a sensor, you can follow extra steps:

- If you installed the sensor on an AD FS or AD CS server, see [Post-installation steps (optional)](active-directory-federation-services.md#post-installation-steps-optional).

- If you installed a standalone sensor, see:

- [Listen for SIEM events on your Defender for Identity standalone sensor](configure-event-collection.md)

- [Configure port mirroring](configure-port-mirroring.md)

- [Configure Windows event forwarding to your Defender for Identity standalone sensor](configure-event-forwarding.md)

## Next step

> [!div class="step-by-step"]

> [Configure Microsoft Defender for Identity sensor settings](configure-sensor-settings.md)


# Configure Sensor Settings

# Configure Microsoft Defender for Identity sensor settings

In this article, you'll learn how to correctly configure Microsoft Defender for Identity sensor settings to start seeing data. You'll need to do additional configuration and integration to take advantage of Defender for Identity's full capabilities.

## View and configure sensor settings

After the Defender for Identity sensor is installed, do the following to view and configure Defender for Identity sensor settings:

1. In [Microsoft Defender XDR](https://security.microsoft.com), go to **Settings** > **Identities** > **Sensors**. For example:

The **Sensors** page displays all of your Defender for Identity sensors, listing the following details per sensor:

- Sensor name

- Sensor domain membership

- Sensor version number

- Whether updates should be [delayed (delayed sensor updates)](../sensor-settings.md#delayed-update-for-sensor-v2x)

- Sensor service status

- Sensor status

- Sensor health status

- The number of health issues

- When the sensor was created

For more information, see [Sensor details](../sensor-settings.md#sensor-details).

1. Select **Filters** to select the filters you want visible. For example:

[![Screenshot of the Sensors page filter options for narrowing the sensor list.](../media/sensor-filters.png)](../media/sensor-filters.png#lightbox)

1. Use the displayed filters to determine which sensors to display. For example:

1. Select a sensor to show a details pane with more information about the sensor and its health status. For example:

[![Screenshot of a sensor details pane showing health status and configuration.](../media/sensor-details.png)](../media/sensor-details.png#lightbox)

1. Scroll down and select **Manage sensor** to show a pane where you can configure sensor details. For example:

1. Configure the following sensor details:

|Name  |Description  |

|---------|---------|

|**Description**     |  Optional. Enter a description for the Defender for Identity sensor.       |

|**Domain Controllers (FQDN)**     |  Required for the Defender for Identity [standalone sensors](prerequisites-standalone.md) and [sensors installed on AD FS / AD CS servers](active-directory-federation-services.md), and can't be modified for the Defender for Identity sensor.   <br><br>Enter the complete FQDN of your domain controller and select the plus sign to add it to the list. For example,  **DC1.domain1.test.local**. <br><br>For any servers you define in the **Domain Controllers** list: <br><br> - All domain controllers whose traffic is being monitored via port mirroring by the Defender for Identity standalone sensor must be listed in the **Domain Controllers** list. If a domain controller isn't listed in the **Domain Controllers** list, detection of suspicious activities might not function as expected. <br><br> - At least one domain controller in the list should be a global catalog. This enables Defender for Identity to resolve computer and user objects in other domains in the forest. |

|**Capture Network adapters**     | Required.      <br><br>  - For Defender for Identity sensors, all network adapters that are used for communication with other computers in your organization.<br><br>      - For Defender for Identity standalone sensor on a dedicated server, select the network adapters that are configured as the destination mirror port. These network adapters receive the mirrored domain controller traffic.      |

1. On the **Sensors** page, select **Export** to export a list of your sensors to a **.csv** file. For example:

## Validate installations

Use the following procedures to validate your Defender for Identity sensor installation.

> [!NOTE]

> If you're installing on an AD FS or AD CS server, you use a different set of validations. For more information, see [Validate successful deployment on AD FS / AD CS servers](active-directory-federation-services.md#validate-successful-deployment).

>

### Validate successful deployment

To validate that the Defender for Identity sensor has been successfully deployed:

1. Check that the **Azure Advanced Threat Protection sensor** service is running on your sensor machine. After you save the Defender for Identity sensor settings, it might take a few seconds for the service to start.

1. If the service doesn't start, review the **Microsoft.Tri.sensor-Errors.log** file, located by default at `%programfiles%\Azure Advanced Threat Protection sensor\<sensor version>\Logs`, where `<sensor version>` is the version you deployed.

### Verify security alert functionality

The following procedure describes how to verify that security alerts are triggered as expected.

When using the examples in this validation procedure, make sure to replace `contosodc.contoso.azure` and `contoso.azure` with the fully qualified domain name (FQDN) of your Defender for Identity sensor and your domain name, respectively.

1. On a member-joined device, open a command prompt and enter `nslookup`

1. Enter `server` and the FQDN or IP address of the domain controller where the Defender for Identity sensor is installed. For example:  `server contosodc.contoso.azure`

1. Enter `ls -d contoso.azure`

1. Repeat the `server` and `ls -d` commands for each sensor you want to test.

1. Access the device details page for the computer you ran the connectivity test from, such as from the **Devices** page, by searching for device name, or from elsewhere in the Defender portal.

1. On the device details tab, select the **Timeline** tab to view the following activity:

- **Events**: DNS queries performed to a specified domain name

- **Action type** MdiDnsQuery

If the domain controller or AD FS / AD CS that you're testing is the first sensor you've deployed, wait at least 15 minutes before verifying any logical activity for that domain controller, allowing the database backend to complete the initial microservice deployments.

### Verify latest available sensor version

The Defender for Identity version is updated frequently. Check for the latest version in the Microsoft Defender XDR **Settings** > **Identities** > **About** page.

## Related content

Now that you've configured the Defender for Identity sensor settings, you can configure additional settings. Go to any of the pages below for more information:

- [Set entity tags: sensitive, honeytoken, and Exchange server](../entity-tags.md)

- [Configure detection exclusions](../exclusions.md)

- [Configure notifications: health issues, alerts, and Syslog](../notifications.md)

## Next step

> [!div class="step-by-step"]

> [Configure audit policies for Windows event logs](configure-windows-event-collection.md)


# Active Directory Federation Services

# Configure sensors for AD FS, AD CS, and Microsoft Entra Connect

Install and configure the Defender for Identity sensor v2.x on Active Directory Federation Services (AD FS), Active Directory Certificate Services (AD CS), and Microsoft Entra Connect servers that aren't domain controllers. Before you begin, make sure you've completed the [prerequisites](#prerequisites) listed later in this article.

> [!TIP]

> If your AD FS, AD CS, or Microsoft Entra Connect role runs on a domain controller with Windows Server 2019 or later, deploy the [sensor v3.x](deploy-sensor-v3.md) instead. This article applies only to servers that aren't domain controllers.

These considerations apply:

- For AD FS environments, Defender for Identity sensors are supported only on the federation servers. They're not required on Web Application Proxy (WAP) servers.

- For AD CS environments, you don't need to install sensors on any AD CS servers that are offline.

- For Microsoft Entra Connect servers, you need to install the sensors on both active and staging servers.

## Prerequisites

Prerequisites for installing Defender for Identity sensors on AD FS, AD CS, or Microsoft Entra Connect servers can be found in [Microsoft Defender for Identity prerequisites](prerequisites-sensor-version-2.md) article.

A sensor installed on an AD FS, AD CS, or Microsoft Entra Connect server can't use the local service account to connect to the domain. Instead, you need to configure a [Directory Service Account](directory-service-accounts.md).

In addition, the Defender for Identity sensor for AD CS supports only AD CS servers with Certification Authority Role Service.

## Configure event collection

If you're working with AD FS, AD CS, or Microsoft Entra Connect servers, make sure that you configured auditing as needed. For more information, see:

- AD FS:

- [Required AD FS events](configure-windows-event-collection.md#required-ad-fs-events)

- [Configure auditing on an AD FS server](configure-windows-event-collection.md#configure-auditing-on-an-ad-fs-server)

- AD CS:

- [Required AD CS events](configure-windows-event-collection.md#required-ad-cs-events)

- [Configure auditing on an AD CS server](configure-windows-event-collection.md#configure-auditing-on-an-ad-cs-server)

- Microsoft Entra Connect:

- [Required Microsoft Entra Connect events](configure-windows-event-collection.md#required-microsoft-entra-connect-events)

- [Configure auditing on Microsoft Entra Connect](configure-windows-event-collection.md#configure-auditing-on-microsoft-entra-connect)

## Configure read permissions for the AD FS database

For sensors running on AD FS servers to have access to the AD FS database, you need to grant read (*db_datareader*) permissions for the relevant [Directory Service Account](directory-service-accounts.md).

If you have more than one AD FS server, make sure to grant db_datareader read access for the Directory Service Account across all of them. Database permissions aren't replicated across servers.

Configure the SQL server to allow the Directory Service Account with the following permissions to the *AdfsConfiguration* database:

- *connect*

- *log in*

- *read*

- *select*

### Grant access to the AD FS database

Grant access to the AD FS database by using SQL Server Management Studio, Transact-SQL (T-SQL), or PowerShell.

For example, the following commands might be helpful if you're using the Windows Internal Database (WID) or an external SQL server.

In these sample codes:

- `[DOMAIN1\mdiSvc01]` is the directory services user of the workspace. If you're working with a gMSA, append `$` to the end of the username. For example: `[DOMAIN1\mdiSvc01$]`.

- `AdfsConfigurationV4` is an example of an AD FS database name and might vary.

- `server=\.\pipe\MICROSOFT##WID\tsql\query` is the connection string to the database if you're using WID.

> [!TIP]

> If you don't know your connection string, follow the steps in the [Windows Server documentation](/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-sql#to-acquire-the-sql-connection-string).

>

The following T-SQL script creates a SQL login for the Directory Service Account and grants it the required db_datareader, connect, and select permissions on the AD FS configuration database:

```tsql

USE [master]

CREATE LOGIN [DOMAIN1\mdiSvc01] FROM WINDOWS WITH DEFAULT_DATABASE=[master]

USE [AdfsConfigurationV4]

CREATE USER [DOMAIN1\mdiSvc01] FOR LOGIN [DOMAIN1\mdiSvc01]

ALTER ROLE [db_datareader] ADD MEMBER [DOMAIN1\mdiSvc01]

GRANT CONNECT TO [DOMAIN1\mdiSvc01]

GRANT SELECT TO [DOMAIN1\mdiSvc01]

GO

```

The following PowerShell script connects to the Windows Internal Database (WID) or external SQL server instance and creates the required SQL login, db_datareader role membership, and select permissions for the Directory Service Account on the AD FS configuration database:

```powershell

$ConnectionString = 'server=\\.\pipe\MICROSOFT##WID\tsql\query;database=AdfsConfigurationV4;trusted_connection=true;'

$SQLConnection= New-Object System.Data.SQLClient.SQLConnection($ConnectionString)

$SQLConnection.Open()

$SQLCommand = $SQLConnection.CreateCommand()

$SQLCommand.CommandText = @"

USE [master];

CREATE LOGIN [DOMAIN1\mdiSvc01] FROM WINDOWS WITH DEFAULT_DATABASE=[master];

USE [AdfsConfigurationV4];

CREATE USER [DOMAIN1\mdiSvc01] FOR LOGIN [DOMAIN1\mdiSvc01];

ALTER ROLE [db_datareader] ADD MEMBER [DOMAIN1\mdiSvc01];

GRANT CONNECT TO [DOMAIN1\mdiSvc01];

GRANT SELECT TO [DOMAIN1\mdiSvc01];

"@

$SqlDataReader = $SQLCommand.ExecuteReader()

$SQLConnection.Close()

```

## Configure permissions for the Microsoft Entra Connect (ADSync) database

> [!NOTE]

> This section is applicable only if the Microsoft Entra Connect database is hosted on an external SQL server instance.

>

> Microsoft recommends that you use the most secure authentication flow available. The authentication flow described in this procedure requires a very high degree of trust in the application, and carries risks that aren't present in other flows. You should only use this flow when other more secure flows, such as managed identities, aren't viable.

Sensors running on Microsoft Entra Connect servers need to have access to the ADSync database, and have execute permissions for the relevant stored procedures. If you have more than one Microsoft Entra Connect server, make sure to run the following PowerShell script on each server to grant ADSync database access and stored procedure permissions.

To grant the sensor permissions to the Microsoft Entra Connect ADSync database by using PowerShell:

```powershell

$entraConnectServerDomain = $env:USERDOMAIN

$entraConnectServerComputerAccount = $env:COMPUTERNAME

$entraConnectDBName = (Get-ItemProperty 'registry::HKLM\SYSTEM\CurrentControlSet\Services\ADSync\Parameters' -Name 'DBName').DBName

$entraConnectSqlServer = (Get-ItemProperty 'registry::HKLM\SYSTEM\CurrentControlSet\Services\ADSync\Parameters' -Name 'Server').Server

$entraConnectSqlInstance = (Get-ItemProperty 'registry::HKLM\SYSTEM\CurrentControlSet\Services\ADSync\Parameters' -Name 'SQLInstance').SQLInstance

$ConnectionString = 'server={0}\{1};database={2};trusted_connection=true;' -f $entraConnectSqlServer, $entraConnectSqlInstance, $entraConnectDBName

$SQLConnection= New-Object System.Data.SQLClient.SQLConnection($ConnectionString)

$SQLConnection.Open()

$SQLCommand = $SQLConnection.CreateCommand()

$SQLCommand.CommandText = @"

USE [master];

CREATE LOGIN [{0}\{1}$] FROM WINDOWS WITH DEFAULT_DATABASE=[master];

USE [{2}];

CREATE USER [{0}\{1}$] FOR LOGIN [{0}\{1}$];

GRANT CONNECT TO [{0}\{1}$];

GRANT SELECT TO [{0}\{1}$];

GRANT EXECUTE ON OBJECT::{2}.dbo.mms_get_globalsettings TO [{0}\{1}$];

GRANT EXECUTE ON OBJECT::{2}.dbo.mms_get_connectors TO [{0}\{1}$];

"@ -f $entraConnectServerDomain, $entraConnectServerComputerAccount, $entraConnectDBName

$SqlDataReader = $SQLCommand.ExecuteReader()

$SQLConnection.Close()

```

## Post-installation steps (optional)

During the sensor installation on an AD FS, AD CS, or Microsoft Entra Connect server, the closest domain controller is automatically selected. Use the following steps to check or modify the selected domain controller:

1. In [Microsoft Defender XDR](https://security.microsoft.com), go to **Settings** > **Identities** > **Sensors** to view all of your Defender for Identity sensors.

1. Locate and select the sensor that you installed on the server.

1. On the pane that opens, in the **Domain controller (FQDN)** box, enter the fully qualified domain name (FQDN) of the resolver domain controllers. Select **+ Add** to add the FQDN, and then select **Save**.

![Screenshot of Defender for Identity sensor settings pane showing the Domain controller (FQDN) field where you enter the resolver domain controller for an AD FS sensor.](../media/sensor-config-adfs-resolver.png)

Initializing the sensor might take a couple of minutes. When it finishes, the service status of the AD FS, AD CS, or Microsoft Entra Connect sensor changes from **stopped** to **running**.

## Validate successful deployment

To validate that you successfully deployed a Defender for Identity sensor on an AD FS or AD CS server:

1. Check that the **Azure Advanced Threat Protection sensor** service is running. After you save the Defender for Identity sensor settings, it might take a few seconds for the service to start.

1. If the service doesn't start, review the `Microsoft.Tri.sensor-Errors.log` file, located by default at `%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs`.

1. Use AD FS or AD CS to authenticate a user to any application, and then verify that Defender for Identity observed the authentication.

For example, select **Hunting** > **Advanced Hunting**. On the **Query** pane, enter and run one of the following queries:

- For AD FS:

```query

IdentityLogonEvents | where Protocol contains 'Adfs'

```

The results pane should include a list of events with a **LogonType** value of **Logon with ADFS authentication**.

- For AD CS:

```query

IdentityDirectoryEvents | where Protocol == "Adcs"

```

The results pane shows a list of events of failed and successful certificate issuance. Select a specific row to see additional details on the **Inspect record** pane.

## Related content

For more information, see:

- [Microsoft Defender for Identity prerequisites](prerequisites-sensor-version-2.md)

- [Install the Microsoft Defender for Identity sensor](install-sensor.md)


# Directory Service Accounts

# Directory Service Accounts for Microsoft Defender for Identity

Defender for Identity uses Directory Service Accounts (DSAs) to read data from Active Directory, such as querying objects, tracking changes, and resolving entities. This is separate from the [action account](manage-action-accounts.md), which performs remediation actions like disabling users or resetting passwords.

> [!NOTE]

> Directory Service Accounts apply to the Defender for Identity sensor v2.x only. The sensor v3.x doesn't use DSA or gMSA configuration and uses LocalSystem exclusively. For more information, see [Defender for Identity sensor v3.x service account requirements](deploy-sensor-v3.md#service-account-requirements).

>[!NOTE]

>Regardless of the Directory Service Accounts configured, the sensor service operates under the LocalSystem identity, and the updater service operates under the LocalSystem identity.

While a DSA is optional in some scenarios, we recommend that you configure a DSA for Defender for Identity for full security coverage.

For example, when you have a DSA configured, the DSA is used to connect to the domain controller at startup. A DSA can also be used to query the domain controller for data on entities seen in network traffic, monitored events, and monitored ETW activities

A DSA is required for the following features and functionality:

- When working with a sensor installed on an [AD FS / AD CS server](active-directory-federation-services.md).

- Requesting member lists for local administrator groups from devices seen in network traffic, events and ETW activities via a [SAM-R call](remote-calls-sam.md) made to the device.

- Accessing the *DeletedObjects* container to collect information about deleted users and computers.

- Domain and trust mapping, which occurs at sensor startup, and again every 10 minutes.

- Querying another domain via LDAP for details, when detecting activities from entities in those other domains.

When you're using a single DSA, the DSA must have *Read* permissions to all the domains in the forests. In an untrusted, multi-forest environment, a DSA account is required for each forest.

One sensor in each domain is defined as the *domain synchronizer*, and is responsible for tracking changes to the entities in the domain. For examples, changes might include objects created, entity attributes tracked by Defender for Identity, and so on.

>[!NOTE]

>By default, Defender for Identity supports up to 30 credentials. To add more credentials, contact Defender for Identity support.

## Supported DSA account options

Defender for Identity supports the following DSA options:

|Option  |Description  |Configuration  |

|---------|---------|---------|

|**Group Managed Service Account gMSA** (Recommended)     |  Provides a more secure deployment and password management. Active Directory manages the creation and rotation of the account's password, just like a computer account's password, and you can control how often the account's password is changed.       |    For more information, see [Configure a Directory Service Account for Defender for Identity with a gMSA](create-directory-service-account-gmsa.md).     |

|**Regular user account**     |   Easy to use when getting started, and simpler to configure *Read* permissions between trusted forests, but requires extra overhead for password management. <br><br>A regular user account is less secure, as it requires you to create and manage passwords, and can lead to downtime if the password expires and isn't updated for both the user and the DSA.   |   Create a new account in Active Directory to use as the DSA with *Read* permissions to all the objects, including permissions to the *DeletedObjects* container. For more information, see [Grant required DSA permissions](#grant-required-dsa-permissions).   |

| **Local service account** | The Local service account is used out of the box and used by default when there is no DSA configured. <br>Note: <li> SAM-R queries for potential lateral movement paths not supported in this scenario. <li> LDAP queries only within the domain the sensor is installed. Queries to other domains in the same forest or cross forest will fail. | None |

>[!NOTE]

>While the local service account is used with the sensor by default, and a DSA is optional in some scenarios, we recommend that you configure a DSA for Defender for Identity for full security coverage.

## DSA entry usage

This section describes how DSA entries are used, and how the sensor selects a DSA entry in any given scenario. Sensor attempts differ, depending on the type of DSA entry:

|Type  |Description  |

|---------|---------|

|**gMSA account**     | The sensor attempts to retrieve the gMSA account password from Active Directory, and then signs into the domain.   |

|**Regular user account**     |   The sensor attempts to sign into the domain using the configured username and password.      |

The following logic is applied:

1. The sensor looks for an entry with an exact match of the domain name for the target domain. If an exact match is found, the sensor attempts to authenticate using the credentials in that entry.

1. If there isn't an exact match, or if the authentication failed, the sensor searches the list for an entry to the parent domain using DNS FQDN, and attempts to authenticate using the credentials in the parent entry instead.

1. If there isn't an entry for the parent domain, or if the authentication failed, the sensor searches the list for a sibling domain entry, using the DNS FQDN, and attempts to authenticate using the credentials in the sibling entry instead.

1. If there isn't an entry for the sibling domain, or if the authentication failed, the sensor reviews the list again and tries to authenticate again with each entry until it succeeds. DSA gMSA entries have higher priority than regular DSA entries.

### Sample logic with a DSA

This section provides an example of how the sensor tries the DSA entires when you have multiple accounts, including both a gMSA account and a regular account.

The following logic is applied:

1. The sensor looks for a match between the DNS domain name of the target domain, such as `emea.contoso.com` and the DSA gMSA entry, such as `emea.contoso.com`.

1. The sensor looks for a match between the DNS domain name of the target domain, such as `emea.contoso.com` and the DSA regular entry DSA, such as `emea.contoso.com`

1. The sensor looks for a match in the root DNS name of the target domain, such as `emea.contoso.com` and the DSA gMSA entry domain name, such as `contoso.com`.

1. The sensor looks for a match in the root DNS name of the target domain, such as `emea.contoso.com` and the DSA regular entry domain name, such as `contoso.com`.

1. The sensor looks for the target domain name for a sibling domain, such as `emea.contoso.com` and the DSA gMSA entry domain name, such as `apac.contoso.com`.

1. The sensor looks for the target domain name for a sibling domain, such as `emea.contoso.com` and the DSA regular entry domain name, such as `apac.contoso.com`.

1. The sensor runs a round robin of all DSA gMSA entries.

1. The sensor runs a round robin of all DSA regular entries.

The logic shown in this example is implemented with the following configuration:

- **DSA entries**:

- `DSA1.emea.contoso.com`

- `DSA2.fabrikam.com`

- **Sensors and the DSA entry that's used first**:

| Domain controller FQDN | DSA entry used |

| --------------------------- | -------------------------------- |

| `DC01.emea.contoso.com`   | `DSA1.emea.contoso.com`            |

| `DC02.contoso.com`        | `DSA1.emea.contoso.com` |

| `DC03.fabrikam.com`       | `DSA2.fabrikam.com`                |

| `DC04.contoso.local`      | Round robin                      |

>[!IMPORTANT]

>If a sensor isn't able to successfully authenticate via LDAP to the Active Directory domain at startup, the sensor won't enter a running state and a health issue is generated. For more information, see [Defender for Identity health issues](../health-alerts.md).

## Grant required DSA permissions

[!INCLUDE [dsa-permissions](../includes/dsa-permissions.md)]

## Test your DSA permissions and delegations via PowerShell

Use the following PowerShell command to verify that your DSA doesn't have too many permissions, such as powerful admin permissions:

```powershell

Test-MDIDSA [-Identity] <String> [-Detailed] [<CommonParameters>]

```

For example, to check permissions for the **mdiSvc01** account and provide full details, run:

```powershell

Test-MDIDSA -Identity "mdiSvc01" -Detailed

```

For more information, see the [DefenderForIdentity PowerShell reference](/powershell/module/defenderforidentity/test-mdidsa).

## Next step

> [!div class="step-by-step"]

> [Configure a Directory Service Account for Defender for Identity with a gMSA »](create-directory-service-account-gmsa.md)


# Create Directory Service Account Gmsa

# Configure a gMSA directory service account for Defender for Identity

Create and configure a [group managed service account (gMSA)](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts) for the sensor v2.x to use when reading Active Directory data (querying objects, tracking changes, resolving entities). This is separate from the [action account](manage-action-accounts.md) used to perform remediation actions like disabling users or resetting passwords.

> [!IMPORTANT]

> This configuration applies to the sensor v2.x only. The sensor v3.x uses LocalSystem for all AD interactions and doesn't require a gMSA or any other Directory Service Account. If all your sensors are v3.x, skip this page.

## Prerequisites

Before you create the gMSA account, make sure the following prerequisites are met:

- Make sure you have permissions to create gMSAs and security groups in Active Directory.

- Assign permissions that allow the sensor to retrieve the gMSA password.

- Choose how to configure password retrieval:

- Assign the gMSA account directly to each of the sensors.

- Use a group that contains all the sensors that need to use the gMSA account.

- Choose the appropriate group based on your deployment:

- **Single-forest, single-domain deployment**: Use the built-in Domain Controllers security group if you're not installing sensors on Active Directory Federation Services (AD FS) or Active Directory Certificate Services (AD CS) servers.

- **Forest with multiple domains**: If you use a single Directory service account (DSA), we recommend creating a universal group and adding each of the domain controllers and AD FS or AD CS servers to the universal group.

- In multi-forest or multi-domain environments, make sure the domain where you create the gMSA trusts the sensors’ computer accounts.

- Create a universal group in each domain that contains sensor computer accounts so that all sensors can retrieve the gMSAs' passwords and perform cross-domain authentications.

## Create the gMSA account

1. If you've never used a gMSA account before, you might need to generate a new root key for the Microsoft Group Key Distribution Service (KdsSvc) within Active Directory. This step is required only once per forest.

To generate a new root key for immediate use, run the following command:

```powershell

Add-KdsRootKey -EffectiveImmediately

```

1. Run the PowerShell commands as an administrator. This script will:

- Create a gMSA account.

- Create a group for the gMSA account.

- Add the specified computer accounts to that group.

1. Before running the script:

- Update the variable values to match your environment.

- Make sure to give each gMSA a unique name for each forest or domain.

```powershell

# Variables:

# Specify the name of the gMSA you want to create:

$gMSA_AccountName = 'mdiSvc01'

# Specify the name of the group you want to create for the gMSA,

# or enter 'Domain Controllers' to use the built-in group when your environment is a single forest, and will contain only domain controller sensors.

$gMSA_HostsGroupName = 'mdiSvc01Group'

# Specify the computer accounts that will become members of the gMSA group and have permission to use the gMSA.

# If you are using the 'Domain Controllers' group in the $gMSA_HostsGroupName variable, then this list is ignored

$gMSA_HostNames = 'DC1', 'DC2', 'DC3', 'DC4', 'DC5', 'DC6', 'ADFS1', 'ADFS2'

# Import the required PowerShell module:

Import-Module ActiveDirectory

# Set the group

if ($gMSA_HostsGroupName -eq 'Domain Controllers') {

$gMSA_HostsGroup = Get-ADGroup -Identity 'Domain Controllers'

} else {

$gMSA_HostsGroup = New-ADGroup -Name $gMSA_HostsGroupName -GroupScope DomainLocal -PassThru

$gMSA_HostNames | ForEach-Object { Get-ADComputer -Identity $_ } |

ForEach-Object { Add-ADGroupMember -Identity $gMSA_HostsGroupName -Members $_ }

}

# Create the gMSA:

New-ADServiceAccount -Name $gMSA_AccountName -DNSHostName "$gMSA_AccountName.$env:USERDNSDOMAIN" `

-PrincipalsAllowedToRetrieveManagedPassword $gMSA_HostsGroup

```

## Refresh Kerberos tickets after changing group membership

The Kerberos ticket has a list of groups that an entity is a member of when the ticket is issued. If you add a computer account to the universal group after it already received a Kerberos ticket, it can't retrieve the gMSA's password until it gets a new ticket.

To refresh the Kerberos ticket, you can:

- **Wait for new Kerberos ticket to be issued**. Kerberos tickets are typically valid for 10 hours.

- **Reboot the server** to request a new Kerberos ticket with the new group membership.

- **Purge the existing Kerberos tickets** to force the domain controller to request a new Kerberos ticket. Run the following command to purge the tickets, from an administrator command prompt on the domain controller: `klist purge -li 0x3e7`

## Grant required directory service account permissions

[!INCLUDE [dsa-permissions](../includes/dsa-permissions.md)]

## Verify that the gMSA account has the required rights

The Defender for Identity sensor service, *Azure Advanced Threat Protection Sensor*, runs as a *LocalService* that impersonates the DSA account. If the *Log on as a service* policy is configured but the permission wasn't granted to the gMSA account, the impersonation fails. In that case, you see the following health issue: **Directory services user credentials are incorrect.**

If you see this alert, check to see if the *Log on as a service policy* is configured either in a Group Policy setting or in a Local Security Policy.

### Check the Local Security Policy

To verify the local policy assignment, perform the following steps:

1. Run `secpol.msc`

1. Select **Local Policies** > **User Rights Assignment**

1. Open the **Log on as a service policy** setting.

1. Once the policy is enabled, add the gMSA account to the list of accounts that can log on as a service.

### Check the Group Policy setting

To verify whether Group Policy configures this setting, perform the following steps:

1. Run `rsop.msc`

1. Go to **Computer Configuration -> Windows Settings -> Security Settings -> Local Policies -> User Rights Assignment -> Log on as a service.**

1. Once the setting is configured, add the gMSA account to the list of accounts that can log on as a service in the Group Policy Management Editor.

> [!NOTE]

> If you use the Group Policy Management Editor to configure the **Log on as a service** setting, make sure to add both **NT Service\All Services** and the gMSA account you created.

<a name="configure-a-directory-service-account-in-microsoft-defender-portal"></a>

## Configure a directory service account in the Microsoft Defender portal

To connect your sensors with your Active Directory domains, configure Directory service accounts in Microsoft Defender portal.

1. In [Microsoft Defender portal](https://security.microsoft.com/), go to **Settings > Identities**.

1. Select **Directory service accounts** to see which accounts are associated with which domains.

1. Select **Add credentials**

1. Enter the following details:

- **Account name**

- **Domain**

- **Password**

1. You can choose if it's a **Group managed service account** (gMSA), or if it belongs to a **Single label domain**.

|Field|Comments|

|---|---|

|**Account name** (required)|Enter the read-only AD username. For example: **DefenderForIdentityUser**. <br><br>- You must use a **standard** AD user or gMSA account. <br>- **Don't** use the UPN format for your username. <br>- When using a gMSA, the user string should end with the `$` sign. For example: `mdisvc$`<br /><br>**NOTE:** We recommend that you avoid using accounts assigned to specific users.|

|**Password** (required for standard AD user accounts)|For AD user accounts only, generate a strong password for the read-only user. For example: `PePR!BZ&}Y54UpC3aB`.|

|**Group managed service account** (required for gMSA accounts)|For gMSA accounts only, select **Group managed service account**.|

|**Domain** (required)|Enter the domain for the read-only user. For example: **contoso.com**. <br><br>It's important that you enter the complete FQDN of the domain where the user is located. For example, if the user's account is in domain corp.contoso.com, you need to enter `corp.contoso.com` not `contoso.com`. <br><br>For more information, see [Microsoft support for Single Label Domains](/troubleshoot/windows-server/networking/single-label-domains-support-policy).|

1. Select **Save**.

1. (Optional) Select an account to open the details pane and view its settings.

> [!NOTE]

> You can use the same procedure to change the password for standard Active Directory user accounts.

> gMSA accounts don't require passwords.

## Troubleshooting

For more information, see [Sensor failed to retrieve the gMSA credentials](../troubleshooting-known-issues.md#sensor-failed-to-retrieve-group-managed-service-account-gmsa-credentials).


# Manage Action Accounts

# Configure Microsoft Defender for Identity action accounts

Defender for Identity allows you to take [remediation actions](../remediation-actions.md) targeting on-premises Active Directory accounts in the event that an identity is compromised. To take these actions, Microsoft Defender for Identity needs to have the required permissions to do so. This is separate from the [Directory Service Account](directory-service-accounts.md), which is for reading AD data.

> [!IMPORTANT]

> This configuration applies to the Defender for Identity sensor v2.x on domain controllers only. Remediation actions aren't performed by sensors on AD FS, AD CS, or Microsoft Entra Connect servers that aren't domain controllers. The sensor v3.x always uses the domain controller's local system account for remediation actions. If all your sensors are v3.x, no action account configuration is needed.

By default, the Microsoft Defender for Identity sensor impersonates the `LocalSystem` account of the domain controller and performs the actions, including [attack disrupting scenarios from Microsoft Defender XDR](/microsoft-365/security/defender/automatic-attack-disruption).

If you need to change the default behavior of using the domain controller's `LocalSystem` account for remediation actions, set up a dedicated gMSA and scope the permissions that you need. For example:

> [!WARNING]

> The sensor v3.x does not use gMSA action accounts. It always uses the domain controller's local system account for remediation actions.

>

> If any of your sensors are v3.x, select **Automatically use the sensor's local system account**. The v3.x sensors use the local system account regardless of gMSA configuration. The v3.x sensors don't use gMSA accounts configured for v2.x sensors.

>

> For more information, see [Sensor v3.x service account requirements](deploy-sensor-v3.md#service-account-requirements).

> [!NOTE]

> Using a dedicated gMSA as an action account is optional. We recommend that you use the default settings for the `LocalSystem` account.

## Best practices for action accounts

We recommend that you avoid using the same gMSA account you configured for Defender for Identity managed actions on servers other than domain controllers. If you use the same account and the server is compromised, an attacker could retrieve the password for the account and gain the ability to change passwords and disable accounts.

We also recommend that you avoid using the same account as both the Directory Service account and the Manage Action account. This is because the Directory Service account requires only read-only permissions to Active Directory, and the Manage Action accounts needs write permissions on user accounts.

If you have multiple forests, your gMSA managed action account must be trusted in all of your forests, or create a separate one for each forest. For more information, see [Microsoft Defender for Identity multi-forest support](multi-forest.md).

## Create and configure a specific action account

1. Create a new gMSA account. For more information, see [Getting started with Group Managed Service Accounts](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts).

1. Assign the **Log on as a service** right to the gMSA account on each domain controller running the Defender for Identity sensor.

1. Grant the required permissions to the gMSA account as follows:

1. Open **Active Directory Users and Computers**.

1. Right-click the relevant domain or OU and select **Properties**. For example:

![Screenshot of the Properties dialog for a domain or OU in Active Directory Users and Computers, used to configure gMSA permissions.](../media/domain-properties.png)

1. Go the **Security** tab and select **Advanced**. For example:

![Screenshot of the Advanced Security Settings dialog showing the Security tab with the Add button to configure gMSA account permissions.](../media/advanced-security.png)

1. Select **Add** > **Select a principal**. For example:

![Screenshot of selecting a principal in the permission entry dialog.](../media/select-principal.png)

1. Make sure **Service accounts** is marked in **Object types**. For example:

![Screenshot of the Object Types dialog with Service accounts selected to enable gMSA principal lookup.](../media/object-types.png)

1. In the **Enter the object name to select** box, enter the name of the gMSA account and select **OK**.

1. In the **Applies to** field, select **Descendant User objects**, leave the existing settings, and add the permissions and properties shown in the following example:

![Screenshot of the Permission Entry dialog showing Descendant User objects scope with reset password and account control permissions for the gMSA account.](../media/permission-entry.png)

Required permissions include:

|Action  |Permissions  |Properties  |

|---------|---------|---------|

|**Enable force password reset**     |  Reset password       |   - `Read pwdLastSet` <br>- `Write pwdLastSet`      |

|**To disable user**     |    -     |                   - `Read userAccountControl` <br>- `Write userAccountControl`      |

1. (Optional) In the **Applies to** field, select **Descendant Group objects** and set the following properties:

- `Read members`

- `Write members`

1. Select **OK**.

## Add the gMSA account in the Microsoft Defender portal

Use the Microsoft Defender portal to add the gMSA action account:

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and select **Settings** -> **Identities** > **Microsoft Defender for Identity** > **Manage action accounts** > **+Create new account**.

For example:

![Screenshot of the Manage action accounts page in the Microsoft Defender portal showing the Create new account option.](../media/manage-action-accounts.png)

1. Enter the account name and domain and select **Save**.

Your action account is listed on the **Manage action accounts** page.

## Related content

For more information, see [Remediation actions in Microsoft Defender for Identity](../remediation-actions.md).


# Prerequisites Standalone

# Microsoft Defender for Identity standalone sensor prerequisites

This article lists prerequisites for deploying a Microsoft Defender for Identity standalone sensor where they differ from the [main deployment prerequisites](../prerequisites.md).

For more information, see [Plan capacity for Microsoft Defender for Identity deployment](../capacity-planning.md).

> [!IMPORTANT]

> Defender for Identity standalone sensors do not support the collection of Event Tracing for Windows (ETW) log entries that provide the data for multiple detections. For full coverage of your environment, we recommend deploying the Defender for Identity sensor.

## Extra system requirements for standalone sensors

Standalone sensors differ from Defender for Identity sensor [prerequisites](../prerequisites.md) as follows:

- Standalone sensors require a minimum of 5 GB of disk space

- Standalone sensors can also be installed on servers that are in a workgroup.

- Standalone sensors can support monitoring multiple domain controllers, depending on the amount of network traffic to and from the domain controllers.

- If you're working with [multiple forests](multi-forest.md), your standalone sensor machines must be allowed to communicate with all remote forest domain controllers using LDAP.

For information on using virtual machines with the Defender for Identity standalone sensor, see [Configure port mirroring](configure-port-mirroring.md).

## Network adapters for standalone sensors

Standalone sensors require at least one of each of the following network adapters:

- **Management adapters** - used for communications on your corporate network. The sensor uses this adapter to query the DC it's protecting and performing resolution to machine accounts.

Configure management adapters with static IP addresses, including a default gateway, and preferred and alternate DNS servers.

The **DNS suffix for this connection** should be the DNS name of the domain for each domain being monitored.

> [!NOTE]

> If the Defender for Identity standalone sensor is a member of the domain, this may be configured automatically.

- **Capture adapter** - used to capture traffic to and from the domain controllers.

> [!IMPORTANT]

>

> - [Configure port mirroring](configure-port-mirroring.md) for the capture adapter as the destination of the domain controller network traffic. Typically, you need to work with the networking or virtualization team to configure port mirroring.

> - Configure a static non-routable IP address (with /32 mask) for your environment with no default sensor gateway and no DNS server addresses. For example: `10.10.0.10/32. This configuration ensures that the capture network adapter can capture the maximum amount of traffic and that the management network adapter is used to send and receive the required network traffic.

>[!NOTE]

>If you run Wireshark on Defender for Identity standalone sensor, restart the Defender for Identity sensor service after you've stopped the Wireshark capture. If you don't restart the sensor service, the sensor stops capturing traffic.

If you attempt to install the Defender for Identity sensor on a machine configured with a NIC Teaming adapter, you receive an installation error. If you want to install the Defender for Identity sensor on a machine configured with NIC teaming, see [Defender for Identity sensor NIC teaming issue](../troubleshooting-known-issues.md#defender-for-identity-sensor-nic-teaming-issue).

### Ports for standalone sensors

The following table lists the extra ports that the Defender for Identity standalone sensor requires configured on the management adapter, in addition to ports listed for the [Defender for Identity sensor](../prerequisites.md#required-ports).

|Protocol|Transport|Port|From|To|

|------------|-------------|--------|-----------|---|

|**Internal ports**||||

|**LDAP**|TCP and UDP|389|Defender for Identity sensor|Domain controllers|

|**Secure LDAP (LDAPS)**|TCP|636|Defender for Identity sensor|Domain controllers|

|**LDAP to Global Catalog**|TCP|3268|Defender for Identity sensor|Domain controllers|

|**LDAPS to Global Catalog**|TCP|3269|Defender for Identity sensor|Domain controllers|

|**Kerberos**|TCP and UDP|88|Defender for Identity sensor|Domain controllers|

|**Windows Time**|UDP|123|Defender for Identity sensor|Domain controllers|

|**Syslog** (optional)|TCP/UDP|514, depending on configuration|SIEM Server|Defender for Identity sensor|

## Windows event log requirements

Defender for Identity detection relies on specific [Windows Event logs](configure-windows-event-collection.md) that the sensor parses from your domain controllers. For the correct events to be audited and included in the Windows Event log, your domain controllers require accurate Windows Advanced Audit Policy settings.

For more information, see, [Advanced audit policy check](../configure-windows-event-collection.md) and [Advanced security audit policies](/windows/security/threat-protection/auditing/advanced-security-auditing) in the Windows documentation.

- To make sure that [Windows Event 8004 is audited](../configure-windows-event-collection.md#configure-ntlm-auditing) as needed by the service, review your [NTLM audit settings](/archive/blogs/askds/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7).

- For sensors running on AD FS / AD CS servers, configure the auditing level to **Verbose**. For more information, see [Event auditing information for AD FS](/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-logging#event-auditing-information-for-ad-fs-on-windows-server-2016) and [Event auditing information for AD CS](/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-logging).

## Next steps

> [!div class="step-by-step"]

> [Configure port mirroring](configure-port-mirroring.md)


# Configure Port Mirroring

# Configure port mirroring

This article describes port mirroring options for Microsoft Defender for Identity, and is relevant only for standalone sensors. Defender for Identity mainly uses deep packet inspection over network traffic to and from your domain controllers. For Defender for Identity standalone sensors to see network traffic, you must either configure port mirroring, or use a Network TAP. Port mirroring copies the traffic from one port (the source port) to another port (the destination port).

When using port mirroring, configure port mirroring for each domain controller that you're monitoring as the source of your network traffic. We recommend working with your networking or virtualization team to configure port mirroring.

> [!IMPORTANT]

> Defender for Identity standalone sensors do not support the collection of Event Tracing for Windows (ETW) log entries that provide the data for multiple detections. For full coverage of your environment, we recommend deploying the Defender for Identity sensor.

>

## Choose a port mirroring method

Your domain controllers and Defender for Identity standalone sensor can be either physical or virtual. The following are common methods for port mirroring and some considerations. Your switch manufacturer might use different terminology. Refer to your specific switch or virtualization server product documentation for detailed configuration steps.

|Method  |Description  |

|---------|---------|

|**Switched Port Analyzer (SPAN)**     | Copies network traffic from one or more switch ports to another switch port on the same switch. Both the Defender for Identity standalone sensor and domain controllers must be connected to the same physical switch.        |

|**Remote Switch Port Analyzer (RSPAN)**     |   Allows you to monitor network traffic from source ports distributed over multiple physical switches. RSPAN copies the source traffic into a special RSPAN configured VLAN. This VLAN needs to be trunked to the other switches involved. RSPAN works at Layer 2.      |

|**Encapsulated Remote Switch Port Analyzer (ERSPAN)**     |    A Cisco proprietary technology working at Layer 3. ERSPAN allows you to monitor traffic across switches without the need for VLAN trunks and uses generic routing encapsulation (GRE) to copy monitored network traffic. <br><br>    Defender for Identity currently cannot directly receive ERSPAN traffic. Instead: <br>    1. Configure the ERSPAN destination where the traffic is decapsulated as a switch or router that can decapsulate the traffic.  <br> 1. Configure the switch or router to forward the decapsulated traffic to the Defender for Identity standalone sensor using either SPAN or RSPAN.|

> [!NOTE]

> - If the domain controller being port mirrored is connected over a WAN link, make sure the WAN link can handle the additional load of the ERSPAN traffic.

>

> - Defender for Identity only supports traffic monitoring when the traffic reaches the NIC and the domain controller in the same manner. Defender for Identity does not support traffic monitoring when the traffic is broken out to different ports.

## Supported port mirroring options

The following table describes Defender for Identity's support for port mirroring configurations:

|Defender for Identity standalone sensor|Domain controller|Considerations|

|---------------|---------------------|------------------|

|Virtual|Virtual on same host|The virtual switch needs to support port mirroring.<br /><br />Moving one of the virtual machines to another host by itself may break the port mirroring.|

|Virtual|Virtual on different hosts|Make sure your virtual switch supports this scenario.|

|Virtual|Physical|Requires a dedicated network adapter otherwise Defender for Identity sees all of the traffic coming in and out of the host, even the traffic the host sends to the Defender for Identity cloud service.|

|Physical|Virtual|Make sure your virtual switch supports this scenario - and port mirroring configuration on your physical switches based on the scenario:<br /><br />If the virtual host is on the same physical switch, you need to configure a switch level span.<br /><br />If the virtual host is on a different switch, you need to configure RSPAN or ERSPAN&#42;.|

|Physical|Physical on the same switch|Physical switch must support SPAN/Port Mirroring.|

|Physical|Physical on a different switch|Requires physical switches to support RSPAN or ERSPAN <br><br>ERSPAN is only supported when decapsulation is performed before the traffic is analyzed by Defender for Identity.|

> [!NOTE]

> The time on your domain controllers and the connected Defender for Identity sensor must be synchronized to within 5 minutes of eachother.

>

## Related content

For more information, see:

- [Configure Windows event auditing](configure-windows-event-collection.md)

- [Configure audit policies for Windows event logs](configure-windows-event-collection.md)

- [Listen for SIEM events on your Defender for Identity standalone sensor](configure-event-collection.md)


# Configure Event Forwarding

# Configure Windows event forwarding to your Defender for Identity standalone sensor

This article describes an example of how to configure Windows event forwarding to your Microsoft Defender for Identity standalone sensor. Event forwarding is one method for enhancing your detection abilities with extra Windows events that aren't available from the domain controller network. For more information, see [Configure Windows event auditing](configure-windows-event-collection.md).

> [!IMPORTANT]

>Defender for Identity standalone sensors don't support the collection of Event Tracing for Windows (ETW) log entries that provide the data for multiple detections. For full coverage of your environment, we recommend deploying the Defender for Identity sensor.

## Prerequisites

Before you start:

- Make sure that the domain controller is properly configured to capture the required events. For more information, see [Configure Windows event auditing](configure-windows-event-collection.md).

- [Configure port mirroring](configure-port-mirroring.md)

## Step 1: Add the network service account to the domain

This procedure describes how to add the Network Service account to the **Event Log Readers** group in the domain. For this scenario, assume that the Defender for Identity standalone sensor is a member of the domain.

1. In Active Directory's Users and Computers, go to the **Built-in** folder and double-click **Event Log Readers**.

1. Select **Members**.

1. If **Network Service** isn't listed, select **Add**, and then enter **Network Service** in the **Enter the object names to select** field.

1. Select **Check Names** and select **OK** twice.

After adding the **Network Service** to the **Event Log Readers** group, reboot the domain controllers for the change to take effect.

For more information, see [Active Directory accounts](/windows-server/identity/ad-ds/manage/understand-default-user-accounts).

## Step 2: Create a policy that sets the Configure target setting

This procedure describes how to create a policy on the domain controllers to set the **Configure target Subscription Manager** setting, which is the Group Policy setting that tells domain controllers where to forward events.

> [!TIP]

> You can create a group policy for these settings and apply the group policy to each domain controller monitored by the Defender for Identity standalone sensor. The following steps modify the local policy of the domain controller.

1. On each domain controller, run:

```cmd

winrm quickconfig

```

1. From a command prompt, enter

```cmd

gpedit.msc

```

1. Expand **Computer Configuration > Administrative Templates > Windows Components > Event Forwarding**. For example:

![Screenshot of Local Group Policy Editor expanded to Computer Configuration, Administrative Templates, Windows Components, Event Forwarding.](../media/wef-1-local-group-policy-editor.png)

1. Double-click **Configure target Subscription Manager** and then:

1. Select **Enabled**.

1. Under **Options**, select **Show**.

1. Under **SubscriptionManagers**, enter the following value and select **OK**:

**Server=http://`<fqdnMicrosoftDefenderForIdentitySensor>`:5985/wsman/SubscriptionManager/WEC,Refresh=10**

For example, using **Server=http://atpsensor.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10**:

![Screenshot of the Configure target Subscription Manager dialog with Enabled selected and the server URL entered in the SubscriptionManagers field.](../media/wef-2-config-target-sub-manager.png)

1. Select **OK**.

1. From an elevated command prompt, enter:

```cmd

gpupdate /force

```

### Step 3: Create and select a subscription on your sensor

This procedure describes how to create a subscription for use with Defender for Identity and then select it from your standalone sensor.

1. Open an elevated command prompt and enter

```cmd

wecutil qc

```

1. Open **Event Viewer**.

1. Right-click **Subscriptions** and select **Create Subscription**.

1. Enter a name and description for the subscription.

1. For **Destination Log**, confirm that **Forwarded Events** is selected. For Defender for Identity to read the events, the destination log must be **Forwarded Events**.

1. Select **Source computer initiated** > **Select Computers Groups** > **Add Domain Computer**.

1. Enter the name of the domain controller in the **Enter the object name to select** field.

1. Select **Check Names** > **OK** > **OK**.

1. Select **OK**. For example:

1. Select **Select Events** > **By log** > **Security**.

1. In the **Includes/Excludes Event ID** field type the event number and select **OK**. For example, enter **4776**:

![Screenshot of the Query filter dialog with the Security log selected and event ID 4776 entered in the Includes/Excludes Event ID field.](../media/wef-4-query-filter.png)

1. Return to the elevated command prompt where you ran `wecutil qc`. Run the following commands, replacing *SubscriptionName* with the name you created for the subscription.

```cmd

wecutil ss "SubscriptionName" /cm:"Custom"

wecutil ss "SubscriptionName" /HeartbeatInterval:5000

```

1. Return to the **Event Viewer** console. Right-click the created subscription and select **Runtime Status** to see if there are any issues with the status.

1. After a few minutes, check to see that the events you set to be forwarded is showing up in the Forwarded Events on the Defender for Identity standalone sensor.

For more information, see: [Configure the computers to forward and collect events](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc748890(v=ws.11)).

## Related content

For more information, see:

- [Configure port mirroring](configure-port-mirroring.md)

- [Listen for SIEM events on your Defender for Identity standalone sensor](configure-event-collection.md)


# Configure Event Collection

# Listen for SIEM events on your Defender for Identity standalone sensor

This article describes the required message syntax when configuring a Defender for Identity standalone sensor to listen for supported SIEM event types. Listening for SIEM events is one method for enhancing your detection abilities with extra Windows events that aren't available from the domain controller network.

For more information, see [Configure Windows event auditing](configure-windows-event-collection.md).

> [!IMPORTANT]

> Defender for Identity standalone sensors don't support the collection of Event Tracing for Windows (ETW) log entries that provide the data for multiple detections. For full coverage of your environment, we recommend deploying the Defender for Identity sensor.

<a name="rsa-security-analytics"></a>

## Configure RSA Security Analytics event collection

Use the following message syntax to configure your standalone sensor to listen for RSA Security Analytics events. In the example, `<Syslog Header>` represents the standard RFC 3164 syslog header prefix, which is optional:

```text

<Syslog Header>RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

```

In this syntax:

- The syslog header is optional.

- The `\n` character separator is required between all fields.

- The fields, in order, are:

1. (Required) RsaSA constant

1. The timestamp of the actual event. Make sure that it's not the timestamp of the *arrival* to the SIEM, or when it's sent to Defender for Identity. We highly recommend using an accuracy of milliseconds.

1. The Windows event ID

1. The Windows event provider name

1. The Windows event log name

1. The name of the computer receiving the event, such as the domain controller

1. The name of the user authenticating

1. The name of the source host name

1. The result code of the NTLM

> [!IMPORTANT]

> The order of the fields is important and nothing else should be included in the message.

<a name="microfocus-arcsight"></a>

## Configure MicroFocus ArcSight event collection

The following example shows a complete Common Event Format (CEF) event 4776 message with the required Extension keys populated. Use this syntax to configure your standalone sensor to listen for MicroFocus ArcSight events:

```text

CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|The domain controller attempted to validate the credentials for an account.|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

```

In this syntax:

- Your message must comply with the protocol definition.

- No syslog header is included.

- The header part, separated by a *pipe* (**|**) must be included, as stated in the protocol

- The following keys in the *Extension* part must be present in the event:

|Key  |Description  |

|---------|---------|

|**externalId**     | The Windows event ID        |

|**rt**     | The timestamp of the actual event. Make sure that the value isn't the timestamp of the *arrival* to the SIEM, or when it's sent to Defender for Identity. Also make sure to use an accuracy of milliseconds.   |

|**cat**     |     The Windows event log name    |

|**shost**     |   The source host name      |

|**dhost**     |   The computer receiving the event, such as the domain controller      |

|**duser**     |    The user authenticating     |

The order isn't important for the *Extension* part.

- You must have a custom key and **keyLable** for the following fields:

- `EventSource`

- `Reason or Error Code` = The result code of the NTLM

<a name="splunk"></a>

## Configure Splunk event collection

The following example shows a sample Splunk event message for event 4776 in key-value format, with the required fields in context. Use this syntax to configure your standalone sensor to listen for Splunk events:

```text

<Syslog Header>\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

```

In this syntax:

- The syslog header is optional.

- There's a `\r\n` character separator between all required fields. These are `CRLF` control characters, `0D0A` in hex, and not literal characters.

- The fields are in `key=value` format.

- The following keys must exist and have a value:

|Name  |Description  |

|---------|---------|

|**EventCode**     |   The Windows event ID      |

|**Logfile**     |The Windows event log name         |

|**SourceName**     |   The Windows event provider name      |

|**TimeGenerated**     |    The timestamp of the actual event. Make sure that the value isn't the timestamp of the *arrival* to the SIEM, or when it's sent to Defender for Identity. The timestamp format must be `The format should match yyyyMMddHHmmss.FFFFFF`, and you must use an accuracy of milliseconds.    |

|**ComputerName**     |    The source host name     |

|**Message**     |     The original event text from the Windows event    |

- The *Message Key* and value must be last.

- The order isn't important for the key=value pairs.

The following example shows the message body content of a Splunk event for Windows event 4776. You can use this sample to validate your sensor formatting:

```text

The computer attempted to validate the credentials for an account.

Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Logon Account: Administrator

Source Workstation: SIEM

Error Code: 0x0

```

<a name="qradar"></a>

## Configure QRadar event collection

QRadar enables event collection via an agent. If the data is gathered using an agent, the time format is gathered without millisecond data.

Because Defender for Identity needs millisecond data, you must first configure QRadar to use agentless Windows event collection. For more information, see [QRadar: Agentless Windows Events Collection using the MSRPC Protocol](https://www.ibm.com/support/pages/qradar-agentless-windows-events-collection-using-msrpc-protocol-msrpc-faq).

Use the following message syntax to configure your standalone sensor to listen for QRadar events:

```text

<13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

```

In this syntax, you must include the following fields:

- The agent type for the collection

- The Windows event log provider name

- The Windows event log source

- The DC fully qualified domain name

- The Windows event ID

- `TimeGenerated`, which is the timestamp of the actual event. Make sure that the value isn't the timestamp of the *arrival* to the SIEM, or when it's sent to Defender for Identity. The timestamp format must be `The format should match yyyyMMddHHmmss.FFFFFF`, and must have an accuracy of milliseconds.

Make sure that the message includes the original event text from the Windows event, and that you have `\t` between the key=value pairs.

>[!NOTE]

> Using WinCollect for Windows event collection isn't supported.

## Related content

For more information, see:

- [Configure port mirroring](configure-port-mirroring.md)

- [Configure Windows event forwarding to your Defender for Identity standalone sensor](configure-event-forwarding.md)


# Configure Windows Event Collection

# Configure Windows event auditing

Configure Windows event auditing to enable Defender for Identity detections. The sensor parses specific Windows event logs from your domain controllers, AD FS servers, AD CS servers, and Microsoft Entra Connect servers. For the correct events to be audited and included in the Windows event log, these servers need the correct advanced audit policy settings.

Configure auditing using one of these methods:

- [Automatic configuration](#configure-defender-for-identity-to-collect-windows-events-automatically) for sensor v3.x on domain controllers (recommended)

- [Manual configuration](#configure-windows-event-collection-manually) for sensor v2.x, servers that aren't domain controllers, or if you opted out of automatic auditing

- [PowerShell configuration](#configure-windows-event-collection-using-powershell)

- [Required Windows events](#required-windows-events) for all server types

Defender for Identity generates health alerts when it detects incorrect Windows event auditing configurations. For more information, see [Microsoft Defender for Identity health alerts](../health-alerts.md).

If you configure auditing properly, Windows event auditing has minimal effect on server performance.

## Configure Defender for Identity to collect Windows events automatically

If you're deploying sensor v3.x on domain controllers, use automatic Windows auditing. This is the recommended approach; it requires no manual configuration and handles all auditing settings for you.

### Turn on automatic Windows auditing

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings**, and then **Identities**.

1. In the **General** section, select **Advanced features**.

1. Turn on **Automatic Windows auditing configuration**.

### What automatic auditing configures

When enabled, the sensor automatically:

- Checks current Windows event auditing configuration.

- Identifies any gaps in the configuration.

- Applies any necessary changes, including all of the steps in the manual configuration:

- **Directory services advanced auditing**: Adds audit entries to the domain root object's System Access Control List (SACL) to enable required directory service auditing.

- **NTLM auditing**: Uses standard Windows Registry APIs to configure the required NTLM auditing registry values.

- **Domain object auditing**: Modifies the SACL on the Configuration partition to capture changes to directory service configuration objects.

- **ADFS auditing**: Adds audit entries to the object's System Access Control List (SACL) of the AD FS configuration container, to enable auditing of AD FS-related directory objects.

- **Windows audit policy**: Configures the local Windows audit policies using the Windows Local Security Authority (LSA) audit policy APIs.

- Applies auditing settings directly to the local system policy of the domain controller.

- Sends health alerts about the configuration state.

- Runs once every 24 hours.

> [!NOTE]

> - Automatic Windows event auditing is supported for domain controllers that use the Defender for Identity sensor version 3.x only. It doesn't apply to v2.x domain controllers or to AD FS, AD CS, and Microsoft Entra Connect servers that aren't domain controllers. For those servers, [configure Windows event auditing manually](#configure-windows-event-collection-manually).

> - If you don't turn on automatic Windows auditing, you **must** [configure Windows event auditing manually](#configure-windows-event-collection-manually) or by [configuring Windows event collection using PowerShell](#configure-windows-event-collection-using-powershell).

> - GPO settings can conflict with local settings set by the sensor.

## Required Windows events

This section lists the Windows events that the Defender for Identity sensor requires. The specific events depend on the server type where the sensor is installed.

### Required AD FS events

The following events are required for AD FS servers:

- 1202: The Federation Service validated a new credential

- 1203: The Federation Service failed to validate a new credential

- 4624: An account was successfully logged on

- 4625: An account failed to log on

For more information, see [Configure auditing on an AD FS server](#configure-auditing-on-an-ad-fs-server).

### Required AD CS events

The following events are required for AD CS servers:

- 4870: Certificate Services revoked a certificate

- 4882: The security permissions for Certificate Services changed

- 4885: The audit filter for Certificate Services changed

- 4887: Certificate Services approved a certificate request and issued a certificate

- 4888: Certificate Services denied a certificate request

- 4890: The certificate manager settings for Certificate Services changed

- 4896: One or more rows have been deleted from the certificate database

For more information, see [Configure auditing on an AD CS server](#configure-auditing-on-an-ad-cs-server).

### Required Microsoft Entra Connect events

The following event is required for Microsoft Entra Connect servers:

- 4624: An account was successfully logged on

For more information, see [Configure auditing on Microsoft Entra Connect](#configure-auditing-on-microsoft-entra-connect).

### Other required Windows events

The following general Windows events are required for all Defender for Identity sensors on domain controllers:

- 4662: An operation was performed on an object

- 4726: User Account Deleted

- 4728: Member Added to Global Security Group

- 4729: Member Removed from Global Security Group

- 4730: Global Security Group Deleted

- 4732: Member Added to Local Security Group

- 4733: Member Removed from Local Security Group

- 4741: Computer Account Added

- 4743: Computer Account Deleted

- 4753: Global Distribution Group Deleted

- 4756: Member Added to Universal Security Group

- 4757: Member Removed from Universal Security Group

- 4758: Universal Security Group Deleted

- 4763: Universal Distribution Group Deleted

- 4776: Domain Controller Attempted to Validate Credentials for an Account (NTLM)

- 5136: A directory service object was modified

- 7045: New Service Installed

- 8004: NTLM Authentication

For more information, see [Configure NTLM auditing](#configure-ntlm-auditing) and [Configure domain object auditing](#configure-domain-object-auditing).

### Event collection for standalone sensors

If you're working with a standalone Defender for Identity sensor, configure event collection manually by using one of the following methods:

- [Listen for security information and event management (SIEM) events on your Defender for Identity standalone sensor](configure-event-collection.md). Defender for Identity supports User Datagram Protocol (UDP) traffic from your SIEM system or your syslog server.

- [Configure Windows event forwarding to your Defender for Identity standalone sensor](configure-event-forwarding.md). When you're forwarding syslog data to a standalone sensor, make sure not to forward *all* syslog data to your sensor.

> [!IMPORTANT]

> Defender for Identity standalone sensors don't support the collection of Event Tracing for Windows (ETW) log entries that provide the data for multiple detections. For full coverage of your environment, deploy the Defender for Identity sensor.

For more information, see the product documentation for your SIEM system or your syslog server.

## Check your current configuration

Before configuring Windows event collection manually, you can run a PowerShell script to check your current configuration and generate a report of any adjustments you need to make:

1. Download the [Defender for Identity PowerShell module](https://www.powershellgallery.com/packages/DefenderForIdentity/).

1. Run the Defender for Identity `New-MDIConfigurationReport` PowerShell module to generate a report of your current Windows event auditing configuration.

```powershell

New-MDIConfigurationReport -Path "C:\Reports" -Mode Domain -Identity "DOMAIN\ServiceAccountName" -OpenHtmlReport

```

Where:

- `Path` is the directory where the report is saved.

- `Mode` indicates where the settings are collected from.

- In `Domain` mode, the settings are collected from the Group Policy objects (GPOs). When using `-Mode Domain`, include the `-Identity` parameter to avoid an interactive prompt.

- In `LocalMachine` mode, the settings are collected from the local machine.

- `OpenHtmlReport` opens the HTML report after the report is generated.

For example, to generate a report and open it in your default browser, run the following command:

```powershell

New-MDIConfigurationReport -Path "C:\Reports" -Mode Domain -OpenHtmlReport

```

For more information, see [New-MDIConfigurationReport](/powershell/module/defenderforidentity/new-mdiconfigurationreport?view=defenderforidentity-latest&preserve-view=true).

1. Review the report and make any necessary adjustments before configuring Windows event collection.

## Configure Windows event collection manually

This section includes instructions for manually configuring Windows event collection. Use these steps if you're deploying sensor v2.x, deploying on AD FS, AD CS, or Entra Connect servers that aren't domain controllers, or if you opted out of automatic auditing for sensor v3.x.

> [!NOTE]

> **Known issue:** In some v3 sensor environments, health alerts about Windows event auditing might persist even when auditing is correctly configured. This primarily occurs with manual auditing configuration, such as using Group Policy or PowerShell. The sensor remains healthy and detections aren't affected. To resolve, enable **Automatic Windows auditing configuration** in the Defender for Identity portal under **Settings** > **Advanced features**.

The following sections describe configuration for each server type:

- [Configure auditing on a domain controller](#configure-auditing-on-a-domain-controller)

- [Configure auditing on an AD FS server](#configure-auditing-on-an-ad-fs-server)

- [Configure auditing on an AD CS server](#configure-auditing-on-an-ad-cs-server)

- [Configure auditing on Microsoft Entra Connect](#configure-auditing-on-microsoft-entra-connect)

- [Configure auditing on the Configuration container](#configure-auditing-on-the-configuration-container)

### Configure auditing on a domain controller

To configure auditing on a domain controller, complete the following steps:

- [Configure Directory Services Advanced Auditing](#configure-directory-services-advanced-auditing)

- [Configure NTLM auditing](#configure-ntlm-auditing)

- [Configure Domain object auditing](#configure-domain-object-auditing)

- [Configure object-level auditing on the AD FS configuration folder](#configure-object-level-auditing-on-the-ad-fs-configuration-folder)

#### Configure Directory Services Advanced Auditing

This section describes how to modify your domain controller's Audit (Premium) Policy settings for Defender for Identity.

1. Sign in to the server as **Domain Administrator**.

1. Open the Group Policy Management Editor from **Server Manager** > **Tools** > **Group Policy Management**.

1. Expand **Domain Controllers Organizational Units**, right-click **Default Domain Controllers Policy**, and then select **Edit**.

> [!NOTE]

> Use the Default Domain Controllers policy or a dedicated GPO to set these policies.

1. Go to **Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings**. Depending on the policy you want to enable, do the following:

1. Go to **Advanced Audit Policy Configuration** > **Audit Policies**.

1. Under **Audit Policies**, edit each of the following policies and select **Configure the following audit events** for both **Success** and **Failure** events.

| Audit policy | Subcategory | Triggers event IDs |

| --- |---|---|

| **Account Logon** | **Audit Credential Validation** | 4776 |

| **Account Management** | **Audit Computer Account Management**<sup>[See note](#failure)</sup> | 4741, 4743 |

| **Account Management** | **Audit Distribution Group Management**<sup>[See note](#failure)</sup> | 4753, 4763 |

| **Account Management** | **Audit Security Group Management**<sup>[See note](#failure)</sup> | 4728, 4729, 4730, 4732, 4733, 4756, 4757, 4758 |

| **Account Management** | **Audit User Account Management** | 4726 |

| **DS Access** | **Audit Directory Service Changes**<sup>[See note](#failure)</sup> | 5136  |

| **System** | **Audit Security System Extension**<sup>[See note](#failure)</sup> | 7045 |

| **DS Access** | **Audit Directory Service Access** | 4662 - For this event, you must also [configure domain object auditing](#configure-domain-object-auditing).  |

> [!NOTE]

> <a name=failure>*</a> These subcategories don't support failure events. Add them for auditing purposes in case they're implemented in the future. For more information, see [Audit Computer Account Management](/windows/security/threat-protection/auditing/audit-computer-account-management), [Audit Security Group Management](/windows/security/threat-protection/auditing/audit-security-group-management), and [Audit Security System Extension](/windows/security/threat-protection/auditing/audit-security-system-extension).

1. To configure **Audit Security Group Management**, under **Account Management**, select **Audit Security Group Management**, and then select **Configure the following audit events** for both **Success** and **Failure** events.

1. From an elevated command prompt, enter `gpupdate`.

1. After you apply the policy via GPO, confirm that the new events appear in the Event Viewer, under **Windows Logs** > **Security**.

To test your audit policies from the command line, run the following command:

```cmd

auditpol.exe /get /category:*

```

For more information, see the [auditpol reference documentation](/windows-server/administration/windows-commands/auditpol).

#### Configure NTLM auditing

When a Defender for Identity sensor parses Windows event 8004, it enriches Defender for Identity NTLM authentication activities with the server-accessed data. This section describes the configuration steps for auditing Windows event 8004.

> [!NOTE]

> Apply domain group policies to collect Windows event 8004 *only* to domain controllers.

To configure NTLM auditing:

1. Open **Group Policy Management** and Expand **Domain Controllers Organizational Units**, right-click **Default Domain Controllers Policy**, and then select **Edit**.

1.  Go to **Default Domain Controllers Policy** > **Local Policies** > **Security Options**.

1. Configure the specified security policies as follows:

| Security policy setting | Value |

|---|---|

| **Network security: Restrict NTLM: Outgoing NTLM traffic to remote servers** | Audit all |

| **Network security: Restrict NTLM: Audit NTLM authentication in this domain** | Enable all |

| **Network security: Restrict NTLM: Audit Incoming NTLM Traffic** | Enable auditing for all accounts |

1. To configure **Outgoing NTLM traffic to remote servers**, under **Security Options**, double-click **Network security: Restrict NTLM: Outgoing NTLM traffic to remote servers**, and then select **Audit all**.

#### Configure domain object auditing

To collect events for object changes, such as for event 4662, you must also configure object auditing on the user, group, computer, and other objects. The following procedure describes how to enable auditing in the Active Directory domain.

To configure domain object auditing:

1. Go to the **Active Directory Users and Computers** console.

1. Select the domain that you want to audit.

1. Select the **View** menu, and then select **Advanced Features**.

1. Right-click the domain and select **Properties**.

1. Go to the **Security** tab, and then select **Advanced**.

1. In **Advanced Security Settings**, select the **Auditing** tab, and then select **Add**.

1. Choose **Select a principal**.

1. Under **Enter the object name to select**, enter **Everyone**. Then select **Check Names** > **OK**.

1. Go back to **Auditing Entry**. You need to create a separate auditing entry for **each** of the following object types:

- **Descendant User Objects**

- **Descendant Group Objects**

- **Descendant Computer Objects**

- **Descendant msDS-GroupManagedServiceAccount Objects**

- **Descendant msDS-ManagedServiceAccount Objects**

- **Descendant msDS-DelegatedManagedServiceAccount Objects** <sup>1</sup>

> [!IMPORTANT]

> Auditing must be configured for **all** of the listed object types, not just user objects. Configuring auditing for only one object type results in incomplete detection coverage.

For each object type, make the following selections:

1. For **Type**, select **Success**.

1. For **Applies to**, select the object type from the list.

1. Under **Permissions**, scroll down and select the **Clear all** button.

1. Scroll back up and select **Full Control**. All the permissions are selected.

1. Clear the selection for the **List contents**, **Read all properties**, and **Read permissions** permissions, and then select **OK**. This step sets all the **Properties** settings to **Write**.

Now, all relevant changes to directory services appear as 4,662 events when they're triggered.

> [!NOTE]

>

> - You can assign auditing permissions to **All descendant objects**, using only the object types detailed in the previous step.

> - The **msDS-DelegatedManagedServiceAccount** class is relevant only for domains running at least one Windows Server 2025 domain controller.

#### Configure Object-level auditing on the AD FS configuration folder

1. Go to the **Active Directory Users and Computers** console, and select the domain where you want to enable the logs.

1. Go to **Program Data** > **Microsoft** > **ADFS**.

1. Right-click **ADFS** and select **Properties**.

1. Go to the **Security** tab and select **Advanced** > **Advanced Security Settings**. Then go to the **Auditing** tab and select **Add** > **Select a principal**.

1. Under **Enter the object name to select**, enter **Everyone**. Then select **Check Names** > **OK**.

1. Return to **Auditing Entry**. Make the following selections:

- For **Type**, select **All**.

- For **Applies to**, select **This object and all descendant objects**.

- Under **Permissions**, scroll down and select **Clear all**. Scroll up and select **Read all properties** and **Write all properties**.

1. Select **OK**.

### Configure auditing on an AD FS server

This section describes how to modify your Active Directory Federation Services (AD FS) audit configurations for Defender for Identity.

#### Configure a Group Policy for event auditing

1. Create a group policy to apply to your Active Directory Federation Services (AD FS).

1. Configure the following auditing settings:

1. Go to **Computer Configuration\Policies\Windows Settings\Security Settings\Advanced Audit Policy Configuration\Audit Policies\Object Access\Audit Application Generated**.

1. Select the checkboxes to configure audit events for **Success** and **Failure**.

#### Configure AD FS event auditing in AD FS Management

1. Select **Start** > **Programs** > **Administrative Tools** > **AD FS Management**.

1. Go to **Actions** > **Edit Federation Service Properties**.

1. Select the **Events** tab.

1. Select the **Success audits** and **Failure audits** check boxes.

1. Select **OK**.

#### Configure Verbose logging for AD FS events

Sensors running on AD FS servers must have the auditing level set to **Verbose** for relevant events.

Use the following PowerShell command to configure the auditing level to **Verbose**:

```powershell

Set-AdfsProperties -AuditLevel Verbose

```

### Configure auditing on an AD CS server

If you're working with a dedicated server that has Active Directory Certificate Services (AD CS) configured, configure auditing as follows to view dedicated alerts and Secure Score reports:

1. Create a group policy to apply to your AD CS server. Edit it and configure the following auditing settings:

1. Go to **Computer Configuration\Policies\Windows Settings\Security Settings\Advanced Audit Policy Configuration\Audit Policies\Object Access\Audit Certification Services**.

1. Select the checkboxes to configure audit events for **Success** and **Failure**.

1. Configure auditing on the certificate authority (CA) using one of the following methods:

- **To configure CA auditing using PowerShell, run:**

```powershell

certutil -setreg CA\AuditFilter 127

Restart-Service certsvc

```

This command updates the CA audit settings and restarts the Certificate Services service so the changes take effect.

- **To configure CA auditing in the Defender portal:**

1. Select **Start** > **Certification Authority (MMC Desktop application)**. Right-click your CA's name and select **Properties**.

1. Select the **Auditing** tab, select all the events that you want to audit, and then select **Apply**.

> [!NOTE]

> Configuring **Start and Stop Active Directory Certificate Services** event auditing might cause restart delays when you're dealing with a large AD CS database. Consider removing irrelevant entries from the database. Alternatively, don't enable this specific type of event.

### Configure auditing on Microsoft Entra Connect

To configure auditing on Microsoft Entra Connect servers:

1. Create a group policy to apply to your Microsoft Entra Connect servers.

1. Edit the group policy and configure the following auditing settings:

1. Go to **Computer Configuration\Policies\Windows Settings\Security Settings\Advanced Audit Policy Configuration\Audit Policies\Logon/Logoff\Audit Logon**.

1. Select the checkboxes to configure audit events for **Success** and **Failure**.

### Configure auditing on the configuration container<a name="enable-auditing-on-an-exchange-object"></a>

You need the configuration container audit only for environments that currently have or previously had Microsoft Exchange. These environments have an Exchange container located within the domain's Configuration section.

1. Open the ADSI Edit tool.

1. Select **Start** > **Run**, enter `ADSIEdit.msc`, and then select **OK**.

1. In the **Action** menu, select **Connect to**.

1. Go to **Connection Settings** > **Select a well known Naming Context**, > **Configuration** and select **OK**.

1. Expand the **Configuration** container to show the **Configuration** node, which begins with **"CN=Configuration,DC=..."**.

1. Right-click the **Configuration** node and select **Properties**.

1. Select the **Security** tab, and then select **Advanced**.

1. In **Advanced Security Settings**, select the **Auditing** tab, and then select **Add**.

1. Choose **Select a principal**.

1. Under **Enter the object name to select**, enter **Everyone**. Then select **Check Names** > **OK**.

1. Return to **Auditing Entry**. Make the following selections:

- For **Type**, select **All**.

- For **Applies to**, select **This object and all descendant objects**.

- Under **Permissions**, scroll down and select **Clear all**. Scroll up and select **Write all properties**.

1. Select **OK**.

## Configure Windows event collection using PowerShell

For more information, see the [Defender for Identity PowerShell reference](/powershell/module/defenderforidentity/new-mdiconfigurationreport):

- [Set-MDIConfiguration](/powershell/module/defenderforidentity/set-mdiconfiguration)

- [Get-MDIConfiguration](/powershell/module/defenderforidentity/get-mdiconfiguration)

The following commands show how to modify your domain controller's Audit (Premium) Policy settings for Defender for Identity by using PowerShell.

**To view your audit policies:**

Use the `Get-MDIConfiguration` cmdlet to retrieve the current Defender for Identity configuration values in domain or local machine mode:

```powershell

Get-MDIConfiguration [-Mode] <String> [-Configuration] <String[]>

```

Where:

- `Mode` specifies whether to use `Domain` or `LocalMachine` mode. In `Domain` mode, the settings come from the Group Policy objects. In `LocalMachine` mode, the settings come from the local machine.

- `Configuration` specifies which configuration to get. Use `All` to get all configurations.

**To configure your settings:**

Use the following syntax to apply one or more Defender for Identity configurations in domain or local machine mode:

```powershell

Set-MDIConfiguration [-Mode] <String> [-Configuration] <String[]> [-CreateGpoDisabled] [-SkipGpoLink] [-Force]

```

Where:

- `Mode` specifies whether to use `Domain` or `LocalMachine` mode. In `Domain` mode, the settings come from the Group Policy objects. In `LocalMachine` mode, the settings come from the local machine.

- `Configuration` specifies which configuration to set. Use `All` to set all configurations.

- `CreateGpoDisabled` specifies if the GPOs are created and kept as disabled.

- `SkipGpoLink` specifies that GPO links aren't created.

- `Force` specifies that the configuration is set or GPOs are created without validating the current state.

The following example applies the full recommended Defender for Identity configuration set through Group Policy in domain mode, creates the group policy objects, and links them:

```powershell

Set-MDIConfiguration -Mode Domain -Configuration All

```

## Update legacy configurations

Defender for Identity no longer requires logging 1,644 events. If you enabled either of the following settings, remove them from the registry. These registry values configured NTDS diagnostic logging levels and search thresholds that were previously required for event 1644 collection but are no longer needed.

```reg

Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Diagnostics]

"15 Field Engineering"=dword:00000005

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters]

"Expensive Search Results Threshold"=dword:00000001

"Inefficient Search Results Threshold"=dword:00000001

"Search Time Threshold (msecs)"=dword:00000001

```

## Related content

For more information, see:

- [Windows security auditing](/windows/security/threat-protection/auditing/security-auditing-overview)

- [Advanced security audit policies](/windows/security/threat-protection/auditing/advanced-security-auditing)


# Migrate To Sensor V3

# Migrate from Defender for Identity sensor v2 to sensor v3.x (Preview)

You can migrate your Defender for Identity sensors from v2.x to v3.x directly from the Microsoft Defender portal. The migration automatically completes the switchover and maintains your server configurations and security monitoring, with no downtime or data duplication.

Before migrating, review the [sensor version limitations](deploy-sensor-v3.md#sensor-version-limitations), including that v3.x doesn't support VPN integration or syslog notifications.

## Prerequisites

To migrate, each server must meet the following requirements:

- Domain controller without additional identity roles

- Defender for Identity sensor v2.x (version 2.254.19112.470 or later)

- Windows Server 2019 or later

- Microsoft Defender for Endpoint deployed, with the [March 10, 2026 Windows Server update (KB5078766)](https://support.microsoft.com/en-us/topic/march-10-2026-kb5078766-os-build-20348-4893-fa3ee26a-0877-47d7-a4b2-9dd632ea8cea) or later cumulative update installed.

For the full list of v3.x requirements, see [Defender for Identity sensor v3.x prerequisites](deploy-sensor-v3.md).

## Known limitations

- **Windows Server 2025 domain controllers:** Migrating domain controllers running Windows Server 2025 to sensor v3.x isn't currently supported.

## Start the migration

Servers that meet all prerequisites appear as **Ready for migration** on the **Sensors** page.

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** > **Identities** > **On-premises** > **Sensors**.

1. Select one or more servers marked as **Ready for migration** and select **Migrate**.

1. In the confirmation prompt, review the details and confirm to start the migration.

> [!NOTE]

> The migration typically takes up to 20 minutes. During this time, the v2.x sensor continues to run until the v3.x sensor is ready, so your server stays protected without interruption.

### Migration states

The **Migration state** column on the **Sensors** page shows the current status of each server:

| State | Description |

|---|---|

| **Ready for migration** | The server meets all prerequisites and can be migrated. Select the server and choose **Migrate** to begin. |

| **Not ready for migration** | The server doesn't meet one or more prerequisites. |

| **Migrating** | The migration is in progress. The v2.x sensor continues running while the v3.x sensor is being activated. |

| **Migration failed** | The migration encountered an error. |

| **Up to date** | The server is running sensor v3.x. |

## Configure the v3.x sensor

For optimal protection and monitoring, complete the configuration steps described in [Defender for Identity sensor v3.x prerequisites](deploy-sensor-v3.md), including:

- [Configure RPC auditing](deploy-sensor-v3.md#configure-rpc-auditing).

- [Configure automatic Windows event auditing](deploy-sensor-v3.md#configure-windows-event-auditing). Existing auditing configurations from the v2.x sensor are preserved and converted for v3.x, but we recommend [enabling automatic Windows event auditing](configure-windows-event-collection.md#configure-defender-for-identity-to-collect-windows-events-automatically) for optimal configuration validation.

- [Switch action accounts from gMSA to local system](deploy-sensor-v3.md#service-account-requirements). The v3.x sensor uses the local system identity for response actions. If you had a gMSA configured for [action accounts](manage-action-accounts.md), select **Automatically use the sensor's local system account** in the Microsoft Defender portal. If gMSA remains enabled for action accounts, response actions (including attack disruption) won't work.

- [Understand DSA and gMSA health alerts in environments with both v2 and v3 sensors](deploy-sensor-v3.md#dsa-and-gmsa-health-alerts-in-environments-with-both-v2-and-v3-sensors). If your workspace still has a Directory Service Account (DSA) or group Managed Service Account (gMSA) configured for v2 sensors, DSA and gMSA credentials continue to be validated on all sensors, including v3 sensors. This is by design. V3 sensors ignore the DSA and gMSA for auditing and response actions, but credential validation occurs at the workspace level. To stop receiving the **Directory services user credentials are incorrect** health alert, remove the DSA or gMSA after all sensors are migrated to v3.

## Troubleshoot "Not ready for migration" status

If a server shows **Not ready for migration**, use the Microsoft Defender for Endpoint Client Analyzer and the following table to identify which condition is failing:

| Condition | How to verify | Resolution if failing |

|---|---|---|

| Defender for Endpoint sensor is running | Client Analyzer report shows **Sense service Status** is **Running**. | Verify Microsoft Defender for Endpoint onboarding is complete. |

| Defender for Endpoint onboarding info exists | Client Analyzer: Check `RegOnboardingInfoPolicy.Json` in the results ZIP. If empty, the policy key is missing. The connectivity log also shows *"OnboardingInfo could not be found in the registry"* if missing. | Re-onboard the server to Microsoft Defender for Endpoint. |

| Device has a registered Defender for Endpoint device ID | Client Analyzer report shows **Device ID** field contains a valid GUID. | Verify Microsoft Defender for Endpoint onboarding completed successfully. Re-onboard the server if `SenseMachineId` is empty. |

| Defender for Identity v2.x sensor is running | Go to the **Sensors** page in the portal and validate the **Service status** column shows **Running**, or run `sc query AATPSensorUpdater` and confirm the service state is **Running**. | Start the `AATPSensorUpdater` service. If the service fails to start, reinstall the v2.x sensor. |

| Defender for Identity v2.x sensor version is 2.254 or later | Check the installed sensor version in **Programs and Features** or on the **Sensors** page in the portal. | Update the Defender for Identity v2 sensor to version 2.254.19112.470 or later. Ensure delayed updates aren't blocking the update. |

| Defender for Endpoint sensor version is 10.8735 or later | Client Analyzer report: the **Sense version** field displays the installed version. | Update the Defender for Endpoint sensor to the latest version. |

| Windows Server 2019 or later with March 2026 cumulative update | Run `winver` to confirm the OS version and build number. | Upgrade the operating system to Windows Server 2019 or later and install the [March 10, 2026 cumulative update (KB5078766)](https://support.microsoft.com/en-us/topic/march-10-2026-kb5078766-os-build-20348-4893-fa3ee26a-0877-47d7-a4b2-9dd632ea8cea) or later. |

| Domain controller without additional identity roles | Verify the server is a pure domain controller and doesn't run AD FS, AD CS, or Entra Connect alongside the DC role. | Migration is only supported on pure domain controllers. Use the v2.x sensor for servers with additional roles. |

## Troubleshoot migration failures

If a server shows a **Migration failed** status, run the [Microsoft Defender for Endpoint Client Analyzer](/defender-endpoint/overview-client-analyzer) on the server to validate that the Defender for Endpoint sensor is running, healthy, and sending events. If the Client Analyzer results show the sensor is healthy, raise a support case for further assistance.

## Clean up the v2.x sensor

The migration disables the v2.x sensor service, but the v2.x sensor software remains installed on the server. Complete the following cleanup steps to fully clean your server from the v2.x sensor files:

- **Uninstall the v2.x sensor**: Remove the v2.x sensor software from the server. This step might require a server restart. For instructions, see [Delete and uninstall a sensor v2.x from a domain controller](../uninstall-sensor.md#delete-and-uninstall-a-sensor-v2x-from-a-domain-controller).

- **Remove Npcap**: Npcap was used by the v2.x sensor but isn't required by the v3.x sensor. If Npcap isn't used by other applications on the server, remove it. Leaving Npcap installed doesn't affect the v3.x sensor.

## Related content

- [Defender for Identity sensor v3.x prerequisites](deploy-sensor-v3.md)

- [Activate the Defender for Identity sensor v3.x](activate-sensor.md)

- [Manage and update sensors](../sensor-settings.md)

- [Remove the Microsoft Defender for Identity sensor](../uninstall-sensor.md)

- [Microsoft Defender for Endpoint Client Analyzer](/defender-endpoint/overview-client-analyzer)


# Test Sensor

# Validate sensor deployment on domain controllers

Use the following procedures to check that your sensors are working.

> [!NOTE]

> The first time you activate the sensor on your domain controller, it might take up to an hour for the sensor to show as **Running** on the **Sensors** page. Subsequent activations show within five minutes.

## Check the Identity Security dashboard

1. In the Defender portal, select **Identities** > **Dashboard**, and review the details shown. Check for expected results from your environment. For more information, see [Identity Security dashboard](../dashboard.md).

## Confirm entity data in the Defender portal

1. In the Defender portal, select **Assets > Devices**, and select the machine for your new sensor. Confirm that Defender for Identity events appear on the device timeline.

1. Select **Assets > Users** and check for users from a newly onboarded domain. You can also use the global search to find specific users. Confirm that user details pages include **Overview**, **Observed in organization**, and **Timeline** data.

1. Use the global search to find a user group, or pivot from a user or device details page where group details are shown. Confirm group membership details, group users, and group timeline data.

If no event data is found on the group timeline, you might need to create some manually. For example, add and remove users from the group in Active Directory.

For more information, see [Investigate assets](../investigate-assets.md).

## Verify data in advanced hunting tables

Use advanced hunting queries to confirm that sensor data is written to the expected tables.

1. In the Defender portal's **Advanced hunting** page, run the following queries to verify that data appears in the expected tables:

```kusto

IdentityDirectoryEvents

| where TargetDeviceName contains "DC_FQDN" // insert domain controller FQDN

IdentityInfo

| where AccountDomain contains "domain" // insert domain

IdentityQueryEvents

| where DeviceName contains "DC_FQDN" // insert domain controller FQDN

```

For more information, see [Advanced hunting in the Microsoft Defender portal](/microsoft-365/security/defender/advanced-hunting-microsoft-defender).

## Test Identity Security Posture Management (ISPM) recommendations

We recommend simulating risky behavior in a test environment to trigger supported assessments and verify that they appear as expected. For example:

1. Trigger a new **Resolve unsecure domain configurations** recommendation by setting your Active Directory configuration to a noncompliant state, and then returning it to a compliant state. For example, run the following commands:

**To set a non-compliant state**

```powershell

Set-ADObject -Identity ((Get-ADDomain).distinguishedname) -Replace @{"ms-DS-MachineAccountQuota"="10"}

```

**To return it to a compliant state**:

```powershell

Set-ADObject -Identity ((Get-ADDomain).distinguishedname) -Replace @{"ms-DS-MachineAccountQuota"="0"}

```

**To check your local configuration**:

```powershell

Get-ADObject -Identity ((Get-ADDomain).distinguishedname) -Properties ms-DS-MachineAccountQuota

```

1. In Microsoft Secure Score, select **Recommended Actions** to check for a new **Resolve unsecure domain configurations** recommendation. You might want to filter recommendations by the **Defender for Identity** product.

For more information, see [Microsoft Defender for Identity's security posture assessments](../security-assessment.md)

## Test alert functionality

Simulate risky activity in a test environment to verify that alerts are triggered as expected. For example:

1. Tag an account as a honeytoken account, and then try signing in to the honeytoken account against the activated domain controller.

1. Create a suspicious service on your domain controller.

1. Run a remote command on your domain controller as an administrator signed in from your workstation.

1. Verify that the expected alerts appear in the Defender portal.

For more information, see [Investigate Defender for Identity security alerts in Microsoft Defender](../manage-security-alerts.md).

## Test remediation actions

Test remediation actions on a test user. For example:

1. In the Defender portal, go to the user details page for a test user.

1. From the **Options** menu, select any of the available remediation actions.

1. Check Active Directory for the expected activity.

For more information, see [Remediation actions in Microsoft Defender for Identity](../remediation-actions.md).

## Next steps

For more information, see [Manage and update Microsoft Defender for Identity sensors](../sensor-settings.md).


# Defender For Identity Cyber Ark Overview

# How Microsoft Defender for Identity protects your CyberArk identity accounts (Preview)

CyberArk Identity is a SaaS-based privileged access management (PAM) solution that manages privileged accounts across cloud and enterprise environments.

When you connect CyberArk Identity with Microsoft Defender for Identity, identity data from CyberArk Identity is added to the identity inventory and correlated with identities from on-premises Active Directory and Microsoft Entra ID. Accounts that are managed by CyberArk Identity as PAM accounts are tagged in the inventory.

## What you can do after connecting CyberArk Identity to Microsoft Defender for Identity

After you connect CyberArk Identity, Microsoft Defender for Identity provides the following capabilities:

| Capability | Description |

|------------|------------|

| View CyberArk accounts in the identity inventory |  CyberArk users are added to the identity inventory in the Microsoft Defender portal. These accounts correlate with matching identities from Active Directory or Microsoft Entra ID, to allow unified tracking across platforms. <br> Additionally, Active Directory accounts that are managed by CyberArk Identity as PAM accounts are tagged in the inventory. <br> This applies only to AD accounts where the platform type in CyberArk Identity is a Windows Domain Account. |

| Improve CyberArk security posture | Evaluates CyberArk Identity accounts for security risks such as stale privileged accounts and excessive privileged role assignments, and generates posture recommendations. Example recommendations include: <br> - Change password for CyberArk Identity privileged user accounts<br>- Remove stale CyberArk Identity privileged accounts <br>- Limit the number of CyberArk Identity accounts with system admin role <br>- High number of CyberArk Identity accounts with a privileged role assigned |

| Use advanced hunting to investigate CyberArk identities and their related activities | Captures CyberArk Identity inventory The [IdentityInfo](/defender-xdr/advanced-hunting-identityinfo-table) table includes account metadata such as privilege level, group membership, and identity source. |

| Take remediation actions | If an identity is determined to be at risk, the following remediation actions can be taken from within the MicrosoftDefender portal: <br>- Disable user in CyberArk Identity <br> - Enable user in CyberArk Identity <br> - Reset password for PAM account in CyberArk Identity  |

## Next steps

- [Connect CyberArk Identity to Microsoft Defender for Identity](connect-cyber-ark.md)


# Connect Cyber Ark

# Connect CyberArk Identity to Microsoft Defender for Identity (Preview)

This section provides instructions for connecting Microsoft Defender for Identity to your existing CyberArk Identity account using the connector APIs. Connecting Defender for Identity to CyberArk Identity gives you visibility into and control over CyberArk identities.

## Prerequisites

Before connecting your CyberArk Identity to Microsoft Defender for Identity, make sure the following prerequisites are met:

**CyberArk Identity roles**

- The System Admin role is required to create an application.

**Microsoft Entra and Defender XDR role-based access options**

To configure the CyberArk Identity connector in Microsoft Defender for Identity, your account must have either of the following access configurations assigned:

- **Microsoft Entra roles:**

- Security Operator

- Security Admin

- **Defender XDR Unified RBAC permission:**

- Core security settings (manage)

## Connect CyberArk Identity to Microsoft Defender for Identity

The following instructions explain how to connect Microsoft Defender for Identity to your dedicated CyberArk Identity account by using the connector APIs. Connecting Defender for Identity to a dedicated CyberArk Identity account gives you visibility into and control over CyberArk Identity use.

### Create a custom CyberArk Identity role

Create a custom role in CyberArk Identity with User Management administrative rights:

1. Sign in to CyberArk Identity console as a system administrator.

1. Navigate to **Identity Administration > Core Services > Roles**

1. Select **Add Role**.

1. Add an appropriate name for the custom role.

1. Select **Save**.

1. Select **Administrative Rights** and add rights for **User Management**.

1. Select **Save**.

### Create a CyberArk OAuth Confidential Client

To support ongoing API access, create a new user and assign the custom role.

1. Sign in to CyberArk Identity console as a system administrator.

1. Navigate to **Identity Administration > Core Services > Users**.

1. Select **Add User**.

1. Enter the **Login Name** and **Display Name**.

1. Under **Status**, select **Is OAuth confidential client**.

1. Copy the username and password. You enter these credentials when you configure the CyberArk Identity connector in the Microsoft Defender portal.

1. Select **Create User**.

1. Navigate to the custom role that you created in [Create a custom CyberArk Identity role](#create-a-custom-cyberark-identity-role).

1. Select **Members** and add the user as a member.

1. Select **Save**.

1. Add the user to the **Privileged Cloud Auditors** role. This role is required to tag identities in the Microsoft Defender portal as privileged accounts.

### Connect CyberArk Identity to Defender for Identity

Configure the CyberArk Identity data connector in the Microsoft Defender portal:

1. Sign in to the [Microsoft Defender Portal](https://security.microsoft.com).

1. Go to **System > Data Management > Data Connectors**.

1. Select **Catalog > CyberArk Identity**.

1. Select on **Connect a connector**

1. Enter a name for your connector.

1. To determine the CyberArk Identity endpoint URL:

1. In CyberArk Identity, select the signed-in user.

1. Select **About**.

1. Copy the **Identity ID** value.

1. Add `.id.cyberark.cloud` to the Identity ID. For example, `contoso.id.cyberark.cloud`.

1. Enter your CyberArk Identity Privilege Cloud service endpoint.

1. In the CyberArk Identity Admin console, go to **Identity Administration > Settings > Integration** and locate the **PVWA URL**. Use the value after `https://`. For example,`contoso.privilegecloud.cyberark.cloud`

1. Enter the username and password for the Oauth user. Include the complete username and the CyberArk domain.

1. Select **Next**.

1. Select **Protection Types > Identity**, and select **Next**.

1. Review the information and select **Connect**.

1. Verify that the CyberArk Identity connector appears in the **My Connector** table as **Connection Status: Ok**.

1. To setup **Actions**, go to **Microsoft Sentinel > Configuration > Automation**.

1. Select **Integration profile** and create one for CyberArk by using the OAuth user's username and password.

## Related articles

- [How Microsoft Defender for Identity protects your CyberArk identity accounts](defender-for-identity-cyber-ark-overview.md)


# Okta Defender For Identity Overview

# How Microsoft Defender for Identity protects your Okta accounts

Okta is a cloud-based identity and access management (IAM) platform that helps organizations control how users and administrators sign in and access enterprise applications. Okta manages high-value identities, including privileged accounts and API tokens. As a result, it’s a frequent target for misuse or attack. Many organizations use Okta alongside on-premises systems like Active Directory and cloud services like Microsoft Entra ID. This hybrid model can make it harder to monitor identity activity and detect threats consistently across platforms.

When you connect Okta to Microsoft Defender for Identity, you can extend your identity threat detection and investigation capabilities to include Okta-managed users. Defender for Identity ingests user and activity data from Okta and correlates it with identity data from Active Directory and Microsoft Entra ID. This integration gives you a centralized view of user activity, posture risks, and suspicious behavior across your identity infrastructure, and you can take the necessary remediation actions.

> [!NOTE]

> The **Identity details** page in the Microsoft Defender portal shows the **Okta user risk score** only if the **Identity Threat Protection with Okta AI** feature is enabled. For more information, see [Risk scoring (Okta Identity Engine)](https://help.okta.com/oie/en-us/content/topics/security/security_risk_scoring.htm).

## What you can do after connecting Okta

With Okta connected, Defender for Identity provides the following capabilities:

|Capability  |Description  |

|---------|---------|

|View Okta accounts in the Identity Inventory    |  Defender for Identity adds Okta users to the identity inventory in the Microsoft Defender portal. These accounts correlate with matching identities from Active Directory or Microsoft Entra ID, to allow unified tracking across platforms.       |

|Improve Okta security posture    |   Defender for Identity evaluates identity configuration in Okta and surfaces posture recommendations in Microsoft Secure Score. Example recommendations include: <br> - [Assign multifactor authentication to Okta privileged user accounts](/defender-for-identity/security-posture-assessments/cloud-identities#assign-multifactor-authentication-to-okta-privileged-user-accounts)  <br> - [Change password for Okta privileged user accounts](/defender-for-identity/security-posture-assessments/cloud-identities#change-okta-password-privileged-user-accounts.md)  <br> - [High number of Okta accounts with privileged role assigned](/defender-for-identity/security-posture-assessments/cloud-identities#high-number-of-okta-accounts-with-privileged-role-assigned.md)  <br> - [Highly privileged Okta API token](/defender-for-identity/security-posture-assessments/cloud-identities#highly-privileged-okta-api-token)  <br> - [Limit the number of Okta Super Admin accounts](/defender-for-identity/security-posture-assessments/cloud-identities#limit-number-okta-super-admin-accounts.md)  <br> - [Remove dormant Okta privileged accounts](/defender-for-identity/security-posture-assessments/cloud-identities#remove-dormant-okta-privileged-accounts.md)      |

|Get alerts on suspicious Okta activity   |  Defender for Identity alerts you when it detects high-risk behavior in Okta, including anonymous sign-ins, privileged role assignments, and token abuse. These alerts are available in Microsoft Defender XDR. When connected, Defender for Identity raises the following alerts based on Okta activity:  <br> - Okta anonymous user access  <br> - Privileged API token created  <br> - Privileged API token updated  <br> - Privileged Role assignment to Application  <br> - Suspicious privileged role assignment  <br> For a full list of supported alerts, see: [Defender for Identity XDR alerts](/defender-for-identity/alerts-xdr#initial-access-alerts).       |

|Use advanced hunting to investigate Okta activity    |  Advanced hunting lets you investigate identity activity across different services including Okta, Active Directory, and Microsoft Entra ID. <br> The **IdentityInfo** table includes account metadata such as privilege level, group membership, and identity source. <br> The **IdentityEvents** table includes events related to those identities, such as sign-ins, authentication attempts, and identity-related alerts across supported identity providers.  <br> To explore the full schema and build your own queries, see:  <br> -  [IdentityInfo ](/defender-xdr/advanced-hunting-identityinfo-table)  <br> -  [IdentityEvents(Preview)](/defender-xdr/advanced-hunting-identityevents-table).       |

|Take remediation actions      |  When Microsoft Defender for Identity identifies an identity as at risk, you can take the following remediation actions directly from the Defender portal to update the user's status in Okta.  <br> - Revoke all user's sessions  <br> - Deactivate user in Okta  <br> - Set user risk in Okta  <br> For more information, see: [Remediation actions in Microsoft Defender for Identity](remediation-actions.md#roles-and-permissions).       |

## Next steps

- [Connect Okta to Microsoft Defender for Identity](okta-integration.md)


# Okta Integration

# Connect Okta to Microsoft Defender for Identity (Preview)

This page explains how to connect Microsoft Defender for Identity to your Okta account. This connection provides visibility into Okta activity and enables shared data collection across Microsoft security products. The connector allows Defender for Identity to collect Okta system logs once and share them with other supported Microsoft security products, such as Microsoft Sentinel. This reduces API usage, avoids duplicate data collection, and simplifies connector management.

> [!NOTE]

> If your Okta environment is already integrated with [Microsoft Defender for Cloud Apps](/defender-cloud-apps/protect-okta), connecting it to Microsoft Defender for Identity can cause duplicate Okta data, such as user activity, to appear in the Defender portal.

## Prerequisites

Before connecting your Okta account to Microsoft Defender for Identity, make sure the following prerequisites are met:

### Okta licenses

Your Okta environment must have one of the following licenses:

- Developer

- Enterprise

### Okta roles

The Super Admin role is required only to create the API token. After you create the token, remove the role and assign the Read-Only Administrator and Defender for Identity custom roles for ongoing API access.

### Microsoft Entra and Defender XDR role-based access options

To configure the Okta connector in Microsoft Defender for Identity, your account must have either of the following access configurations assigned:

- **Microsoft Entra roles:**

- Security Operator

- Security Admin

- **Defender unified RBAC permission:**

- Core security settings (manage)

### Connect Okta to Microsoft Defender for Identity

This section provides instructions for connecting Microsoft Defender for Identity to your dedicated Okta account using the connector APIs. This connection gives you visibility into and control over Okta use.

### Create a dedicated Okta account

1. Create a dedicated Okta account for Microsoft Defender for Identity use only.

1. Assign your Okta account as a Super Admin role.

1. Verify your Okta account.

1. Store the account credentials for later use.

1. Sign in to your dedicated Okta account created in step 1 to create an API token.

### Create an API token

1. In the Okta console, select **Admin**.

1. Select **Security** > **API**.

1. Select **Tokens**

1. Select **Create Token**.

1. In the Create token pop-up:

1. Enter a name for your Defender for Identity token.

2. Select **Any IP**.

3. Select **Create token**.

1. In the **Token created successfully** pop-up, copy the **Token value** and store it securely. This token is used to connect Okta to Defender for Identity.

### Add Custom user attributes

1. Select **Directory > Profile Editor**.

1. Select **User (default)**.

1. Select **Add Attributes**.

1. Set Data type to String.

1. Enter the Display name.

1. Enter the Variable name.

1. Set User permission to Read Only.

1. Enter the following attributes:

|Display Name |Variable Name |

|---------|---------|

|ObjectSid     | ObjectSid        |

|ObjectGuid     | ObjectGuid        |

|DistinguishedName    | DistinguishedName    |

1. Select Save.

1. Verify that the three custom attributes you added are displayed correctly.

### Create a custom Okta role

> [!NOTE]

> To support ongoing API access, you must assign both the **Read-Only Administrator role** and the **custom Microsoft Defender for Identity role.** These roles are mandatory to successfully configure the Okta connector. Configuration fails if either role is missing.

After you assign both roles, you can remove the **Super Admin role**. This approach ensures that only relevant permissions are assigned to your Okta account at all times.

1. Navigate to **Security > Administrator**.

1. Select the **Roles** tab.

1. Select **Create new role**.

1. Set the role name to **Microsoft Defender for Identity**.

1. Select the permissions you want to assign to this role. Include the following permissions:

- **Edit user's lifecycle states**

- **Edit user's authenticator operations**

- **View roles, resources, and admin assignments**

1. Select **Save role**.

### Create a resource set

1. Select the **Resources** tab.

1. Select **Create new resource set**.

1. Name the resource set **Microsoft Defender for Identity**.

1. Add the following resources:

- **All users**

- **All Identity and Access Management resources**

1. Select **Save selection**.

### Assign the custom role and resource set

To complete the configuration in Okta, assign the custom role and resource set to the dedicated account.

1. Assign the following roles to the dedicated Okta account:

- Read-Only Administrator.

- The custom Microsoft Defender for Identity role

1. Assign the Microsoft Defender for Identity resource set to the dedicated Okta account.

1. When you're done, remove the Super Admin role from the account.

### Connect Okta to Microsoft Defender for Identity

1. Navigate to the Microsoft Defender Portal.

1. Select **System** > **Data management** > **Data connectors** > **Catalog**

1. Select **Okta Single Sign-On** > **Connect a connector**.

1. Enter a name for your connector.

1. Enter your Okta domain (for example, my.project.okta.com).

1. Paste the API token you copied from your Okta account.

1. Select **Next**.

1. **Select products > Microsoft Defender for Identity**

1. Select **Next**

1. Review Okta details, and select **Connect**.

1. Verify that your Okta environment appears in the table as enabled.

> [!NOTE]

> Connecting the Okta connector can take up to 15 minutes.

## Related articles

- [How Defender for Identity helps protect your Okta environment](okta-defender-for-identity-overview.md).


# Sail Point Overview

# How Microsoft Defender for Identity protects your SailPoint Identity Security Cloud accounts (Preview)

Microsoft Defender for Identity helps protect your on-premises Active Directory and Microsoft Entra ID environments from advanced threats.

Connecting SailPoint Identity Security Cloud with Microsoft Defender for Identity (MDI) gives you the ability to detect, investigate, and respond to identity-based threats across both cloud and on-premises infrastructures.

## What you can do after connecting SailPoint Identity Security Cloud to Microsoft Defender for Identity

After you connect SailPoint Identity Security Cloud, Microsoft Defender for Identity provides the following capabilities:

| Capability | Description |

|------------|------------|

| View SailPoint accounts in the identity inventory | - Adds SailPoint Identity Security Cloud accounts into the identity inventory and correlates them with identities from on-premises, Active Directory and Microsoft Entra ID.  |

| Improve SailPoint security posture | Evaluates SailPoint Identity Security Cloud accounts for security risks such as stale privileged accounts and excessive privileged role assignments, and generates posture recommendations. Example recommendations include: <br> - Change password for SailPoint Identity Security Cloud privileged user accounts<br>- Remove stale SailPoint Identity Security Cloud privileged accounts <br>- Limit the number of SailPoint Identity Security Cloud accounts with system admin role <br>- High number of SailPoint Identity Security Cloud accounts with a privileged role assigned <br> - Assign multifactor authentication for SailPoint  privileged user accounts|

| Use advanced hunting to investigate SailPoint identities and their related activities |  The [IdentityInfo](/defender-xdr/advanced-hunting-identityinfo-table) and the [IdentityEvents](/defender-xdr/advanced-hunting-identityevents-table) advanced hunting tables include inventory and event data from SailPoint Identity Security Cloud for investigation. |

| Take remediation actions | If an identity is determined to be at risk, the following remediation actions can be taken from within the Microsoft Defender portal: <br>- Disable user in SailPoint Identity Security Cloud <br> - Enable user in SailPoint Identity Security Cloud  |

## Next steps

- [Connect SailPoint Identity to Microsoft Defender for Identity (Preview)](connect-sail-point.md).


# Connect Sail Point

# Connect SailPoint Identity Security Cloud to Microsoft Defender for Identity (Preview)

This article describes how to connect Defender for Identity to your SailPoint Identity Security Cloud account. This connection helps you see and manage SailPoint identities. Before you start, review the [prerequisites](#prerequisites).

## Prerequisites

Make sure you meet these requirements before you start:

**SailPoint Identity Security Cloud roles**

- The IdentityNow Admin role is required only to create an application.

**Microsoft Entra and Defender XDR role-based access options**

Your account needs one of these access options to set up the connector:

- **Microsoft Entra roles:**

- Security Operator

- Security Admin

- **Defender XDR Unified RBAC permission:**

- Core security settings (manage)

## Connect SailPoint Identity Security Cloud to Microsoft Defender for Identity

To set up the connection, create a personal access token in SailPoint and then configure the connector in the Defender portal.

### Create a SailPoint Identity Security Cloud Personal Access Token

Create a personal access token in SailPoint Identity Security Cloud for this integration:

1. Sign in to SailPoint Identity Security Cloud.

1. Create a dedicated SailPoint Identity Security Cloud user for this integration.

1. Go to **User's Preferences > Personal Access Tokens**.

1. Select **New Token**.

1. Add the following scopes to the token:

1. idn:accounts:read

1. idn:entitlement:read

1. sp:search:read

1. idn:accounts-state:manage

1. Copy the **Client ID** and **Secret**. You need these values later to finish the setup.

### Connect SailPoint Identity Security Cloud to Defender for Identity

Use the Defender portal to configure the SailPoint connector:

1. Sign in to the [Microsoft Defender Portal](https://security.microsoft.com).

1. Go to **System > Data Management > Data Connectors**.

1. Select **Catalog > SailPoint Identity Security Cloud**.

1. Select **Connect a connector**

1. Enter a name for your connector.

1. Enter your SailPoint Identity Security Cloud API Endpoint URL. Use the value after `https://` and make sure 'api' is included in the URL. For example, `contoso.api.identitynow.com`.

1. Enter your **Client ID** and **Client Secret**.

1. Select **Next**.

1. Select **Protection Types > Identity**, and then select **Next**.

1. Review the information and select **Connect**.

1. Verify that the SailPoint Identity connector appears in the **My Connector** table as **Connection Status: Ok**.

## Related articles

- [How Microsoft Defender for Identity protects your SailPoint identity accounts](sail-point-overview.md)


# Integrate Microsoft And Pam Services

# Integrate Defender for Identity with PAM services

## What are PAM services?

Privileged Access Management (PAM) solutions help reduce the risk of credential misuse by securing, monitoring, and controlling privileged account access to critical resources.

PAM solutions secure privileged accounts by storing their credentials in a secure vault, controlling access through approval workflows, and monitoring active sessions to enforce just-in-time (JIT) and just-enough-access (JEA) policies. Common PAM capabilities include, automated password rotation, multifactor authentication, session isolation, and anomaly detection.

## Defender for Identity and PAM

Defender for Identity helps identify and investigate suspicious activities related to privileged accounts, such as unusual sign in patterns or privilege escalation attempts.

When integrated with a PAM solution, Microsoft Defender for Identity can detect and investigate suspicious activity involving privileged accounts—such as abnormal sign-ins or privilege escalation attempts. The integration combines PAM’s access controls with Defender for Identity’s behavioral analytics for enhanced threat detection and containment.

## Technology partners

Microsoft Defender for Identity currently supports integration with the following PAM vendors. Dedicated integrations for each partner are now available in the Microsoft 365 Defender partner catalog for streamlined onboarding and visibility.

|Vendor |Description |

|---------|---------|

|CyberArk    | Provides credential vaulting, session monitoring, and threat remediation for privileged identities.       |

|BeyondTrust     | BeyondTrust Offers identity-centric controls to manage the privilege attack surface and mitigate internal and external threats.        |

|Delinea     | Delivers centralized authorization and session control for privileged identities across enterprise environments.       |

### Reset password

Once PAM integration is enabled, Microsoft Defender XDR automatically tags identities managed by your PAM solution, providing critical context during investigations.

Additionally, you can initiate a password reset for high-risk privileged accounts directly from the Microsoft Defender XDR console. This action uses the connected PAM system.

To reset a password:

1. Go to **Assets > Identities**.

2. Select the relevant identity.

3. Click the three-dot menu (**⋯**) in the top-right corner.

4. Select **Reset password**. The label might vary based on the vendor (for example, **Reset password by CyberArk**, **Reset password by BeyondTrust**).

This capability streamlines containment and response workflows by embedding privileged access controls directly into the investigation experience.

### Next steps

For more information, see:

[How to integrate Defender for Identity with Delinea](https://docs.delinea.com/online-help/integrations/microsoft/mdi/integrating-mdi.htm)

[How to integrate Defender for Identity with CyberArk](https://community.cyberark.com/marketplace/s/#a35Ht0000018sDVIAY-a39Ht000004GLaEIAW)

[How to integrate Defender for Identity with BeyondTrust](https://docs.beyondtrust.com/insights/docs/microsoft-defender)


# Identity Inventory

# View the Identity inventory

The **Identity inventory** provides a centralized view of all identities in your organization, so you can investigate, monitor, and manage them efficiently. At a glance, see key details like the identity's type, domain, tags, and other attributes to quickly spot identities that require attention.

When you [enable the Identity inventory integration](/defender-cloud-apps/general-setup#enable-identity-inventory-integration) in Microsoft Defender for Cloud Apps, SaaS and cloud application accounts are ingested into the Identity inventory. This provides a centralized view of identities across on-premises, cloud, and SaaS environments. With the integration enabled, you get access to unified experiences including the identity timeline, identity-centric response, improved identity correlation, and identity-centric protection.

> [!IMPORTANT]

> As Microsoft Defender moves toward a fully unified identity platform, some Defender for Cloud Apps data pipelines remain separate from the Identity inventory. As a result, identity correlations defined in the Identity inventory, including manual and policy-based correlations, don't currently affect the following Defender for Cloud Apps capabilities:

>

> - Built-in detections

> - UEBA (User and Entity Behavior Analytics)

> - Scoped deployment

> - Governance actions

> - Defender for Cloud Apps policies

> - Activity log

> - Cloud discovery user enrichment and anonymization

> - RBAC scoping

>

> These features continue to use the Cloud Application Accounts inventory. For more information, see the relevant Defender for Cloud Apps documentation.

The **Identity inventory** page includes tabs for:

- **Human identities**: Human identities discovered in your environment from Active Directory and Microsoft Entra ID. When the Identity inventory integration is enabled, this tab also includes SaaS and cloud application accounts from Defender for Cloud Apps.

- **Non-Human identities (Preview)**: Non-human identities discovered in your SaaS, Entra ID, and on-premises environments, including:

- OAuth apps registered in:

- Microsoft Entra ID

- Google Workspace

- Salesforce

- On-premises service accounts from Active Directory

From the top navigation:

- Add or remove columns.

- Apply filters.

- Sort the list by column values.

- Search for a specific identity.

- Export the list to a CSV file.

- Copy a link to the current filtered view.

> [!NOTE]

> When you export the identities list to a CSV file, only the first 5,000 identities are included in the export.

## Access the Identity inventory

In the [Microsoft Defender portal](https://security.microsoft.com), select **Assets** > **Identities**.

## Identity inventory insights

The top section of the Identity inventory page gives you quick insights into your identity landscape through the following cards:

- The **Classify critical assets** card lets you define identity groups as business critical. For more information, see [Microsoft Security Exposure Management](/security-exposure-management/microsoft-security-exposure-management).

- The **Highly privileged identities** card helps you investigate all sensitive accounts in your organization in Advanced hunting, including Microsoft Entra ID Security administrators and Global administrators.

- The **Critical Active Directory service accounts** card helps you quickly identify all Active Directory accounts designated as critical, making it easier to focus on identities most at risk.

- The **Cloud application accounts** card connects you to your [Cloud application accounts](/defender-cloud-apps/accounts) identified by the Defender for Cloud apps application connectors. When the Identity inventory integration is enabled, cloud application accounts also appear in the **Human identities** tab.

## The identity inventory lists

Select a tab to view details and available actions for each identity type.

## [Human identities](#tab/human-identities)

The **Human identities** tab consolidates all user identities from Active Directory and Microsoft Entra ID in one place, making it easier to view and manage user accounts. To investigate details about a specific user, see [Investigate users in Microsoft Defender XDR](/defender-xdr/investigate-users).

### Human identity statistics

These important statistics help you prioritize identities for security posture improvements:

| Name | Description |

| --------- | --------- |

| Total | The total number of identities. |

| Critical | The number of your critical assets. |

| Disabled | The number of all disabled identities in your organization. |

### Human identity details

The **Identities** list highlights key details for each human identity, including these columns by default:

| Column name | Description |

| --------- | --------- |

| Display name | The full name of the identity as shown in the directory. |

| Domain | The Active Directory domain to which the identity belongs. |

| Object ID | A unique identifier for the identity in Microsoft Entra ID. |

| UPN (User Principal Name) | The unique sign-in name of the identity in an email-like format. |

| Identity environment | Indicates whether the identity is on-premises (originates from Active Directory), Cloud only (Entra ID) or Hybrid (synced from Azure Active Directory to Microsoft Entra ID). |

| Identity provider | The name of the identity provider. |

| Risk score | The risk score dynamically calculated for the identity. |

| Criticality level | The criticality level assigned to the identity. |

| Tags | Custom labels that help categorize identities considered high-value assets. For example, **Sensitive**, **Honeytoken**, or **Privileged Accounts** managed by a [Privileged Identity Management](/entra/id-governance/privileged-identity-management/pim-configure) (PIM) service. |

| SID | The Security Identifier, a unique value used to identify the identity in Active Directory. |

| Account status | Shows whether the identity is enabled or disabled. |

| Type | Specifies if the identity is a user account or service account. |

| Created time | The timestamp of when the identity was first created. |

| Last updated | The timestamp of the most recent update to the identity's attributes in Active Directory. |

Nondefault columns: Email, Microsoft Entra ID risk level, and Cloud ID.

## [Non-Human identities (Preview)](#tab/non-human-identities)

The **Non-Human identities** tab consolidates all non-human identities in one place, making it easier to check ownership and assess risk. To investigate details about a specific non-human identity, see [View a non-human identity](/defender-xdr/investigate-non-human-identities).

### Non-human identity stats

These statistics highlight non-human identities that might need prioritization. Select a statistic to get a filtered list of identities to investigate.

| Name | Description |

| --------- | --------- |

| Risky | The number of non-human identities with a high risk score. Risk scores are based on factors described in the [Risk score tab of the identity](/defender-cloud-apps/app-governance-visibility-insights-view-apps#getting-detailed-information-on-an-app). |

| Highly privileged | The number of non-human identities with high-privilege permissions, such as admin consent or broad application permissions. |

| Overprivileged | The number of non-human identities with more permissions than they use. |

| Unused | The number of non-human identities with no recent sign-in activity. |

| External unverified publishers | The number of non-human identities from unverified external publishers. |

| New | The number of recently discovered non-human identities. |

### Non-human identity details

The **Non-Human identities** tab contains these sections:

- **Entra ID**: OAuth apps registered in Microsoft Entra ID.

- **Active Directory**: On-premises service accounts.

- **Salesforce**: OAuth apps registered in Salesforce.

- **Google Workspace**: OAuth apps registered in Google.

The **Identities** list highlights key details for each non-human identity, including these columns by default:

| Column name | Description |

| --------- | --------- |

| Display name | The full name of the identity as shown in the directory. |

| Status | Shows whether the identity is enabled or disabled, and if disabled, by whom. |

| Risk score | Shows the identity risk score (1-100). Higher values indicate greater risk. |

| Graph API access | Shows whether the identity has at least one Graph API permission. |

| Permission type | Shows whether the identity has application (app only), dedicated, or mixed permission. |

| Origin | Shows whether the identity originated in the tenant or is registered in an external tenant. |

| Content type | Shows whether the identity has admin or user-only consent. For identities with only user consent, the total consented users are shown. Identities with admin consent have broad access to all data, unless access policies and other restrictions limit that access. |

| Publisher | Publisher of the identity and their verification status. |

| Last used | Last time the identity signed in. This data is tracked only back to June 1, 2022. |

For Microsoft Entra ID identities, select **Create new policy** to set up a governance policy that automatically responds when high-risk apps appear. Use the built-in **New high risk app** template for a quick setup, or create a custom policy with risk score as a policy condition.

---

### Related articles

- [Investigate users in Microsoft Defender](/defender-xdr/investigate-users)

- [Investigate non-human identities in Microsoft Defender](/defender-xdr/investigate-users)

- [Investigate cloud application accounts](/defender-cloud-apps/accounts)


# Service Account Discovery

# Investigate and protect Service Accounts

### What are Service Accounts?

Service accounts are specialized identities within Active Directory used to run applications, services, and automated tasks. These accounts often require elevated privileges to perform their designated job. However, because they can't authenticate in the same way as human accounts, they typically don't benefit from the increased security of modern authentication methods like MFA (multifactor authentication). Given their potential elevated privilege and the inherent limitations of the access policies that govern them, careful management and monitoring are crucial to ensure they don't become a security vulnerability.

Service accounts are classified into several types:

- gMSA (Group Managed Service Accounts): gMSAs provide a single identity solution for multiple services that require mutual authentication across multiple servers, as they allow Windows to handle password management, reducing administrative overhead.

- sMSA (Managed Service Accounts): Designed for individual services on a single server rather than groups.

- User Account: These standard user accounts are typically used for interactive logins but can also be configured to run services.

The auto discovery feature quickly identifies gMSA and sMSA accounts and user accounts within Active Directory that meet specific criteria. These criteria include having a [Service Principal Name](/windows/win32/ad/service-principal-names)(SPN) and has an assigned ***password never expires*** attribute. The feature classifies these accounts as service accounts. These accounts are highlighted and presented, along with relevant information including insights into recent authentications and the sources and destinations of those interactions, as part of a dedicated inventory within the Defender experience. This helps you better understand the accounts' purpose so you can more easily spot anomalous activity and understand its implications.

Service account types are displayed in the **Identity Info** table within Advanced Hunting.

## Service accounts page

#### Navigate to the Service accounts page

In the Microsoft Defender portal at [https://security.microsoft.com](https://security.microsoft.com), go to Identities > Service Accounts.

The following image depicts the Service accounts page:

### Customize the page view

There are several options you can choose from to customize the identities list view. On the top navigation you can:

- Add or remove columns.

- Apply filters.

- Export the list to a CSV file.

- Sort and filter the Service accounts list.

> [!NOTE]

> When exporting the service accounts list to a CSV file, a maximum of 2,000 service accounts are displayed.

### Service account details

- Total: The total number of service accounts listed.

- Managed: The total number of service accounts that are gMSA (Group Managed Service Accounts) or sMSA (Managed Service Accounts).

- User: The total number of standard user accounts used for interactive logins or configured to run services.

- Critical: The total number of service accounts identified as critical.

You can use the sort and filter functionality on each service account tab to get a more focused view.

| Service account details   |  Description |

|---------|---------|

|**Display name** | The full name of the service account as shown in the directory.

|**SID**     | The Security Identifier, a unique value used to identify the identity in Active Directory.         |

|**Domain**    | The Active Directory domain to which the identity belongs.         |

|**Type**    | Specifies if the service account is gMSA (Group Managed Service Accounts), sMSA (Managed Service Accounts) or a user account.         |

|**Criticality level**     | Indicates the critical level of the service account, ranging from low to very high.         |

|**Tags**    | Sensitive or Honey Token        |

|**Auth protocols**   | Lists the available methods for verifying user identities, for example, Kerberos and NTLM (New Technology LAN Manager).         |

|**Sources**     |  The number of potential source logins.        |

|**Destinations**    | When a service account is trying to access a destination server, the request is directed to the target system, which can include many resources on that server. These resources might be a database, a file server, or other services hosted on the server.        |

|**Connections**   | The number of unique connections made between sources and destinations.         |

|**Created**    |The timestamp when the service account was first created.         |

|**Last updated**    | The timestamp of the most recent update to the service account.        |

|

### Connections

For a deeper dive into what's happening in your service account select the domain name to see the following information:

When you investigate a specific Service account, you see the following details under the connections tab:

|Service account connection details  |Description |

|---------|---------|

|Source  |  Where the network traffic or request originates from.       |

|Source type    | What kind of device or system is initiating the request. For example, server, workstation or domain controller.        |

|Source risk   | Identicates the risk posed to the source from no risk to high risk.         |

|Destination   | Where the request is being directed to. The target system that the service account is trying to access. For example, when trying to access a destination server, there can be multiple resources on that server (for example, a database and a file-server).        |

|Destination type    | Server, Workstation, or Domain controller.         |

|Auth protocols   | Kerberos and NTLM        |

|Service Class     | The services within a network that define the type of service being provided, often used for authentication and resource management. These include: Lightweight Directory Access Protocol (LDAP), Common Internet File System (CIFS), Remote Procedure Call (RPC), Remote Procedure Call Subsystem (RPCSS), "HTTP," Terminal Services (TERMSRV), and "HOST"        |

|Count | How many sign in events occurred over this connection in the last 180 days.

Last seen   | The date and time of the most recent sign in event over this connection.        |

### Define Service Account classification rules

Service account classification rules let you define your own criteria for identifying service accounts. These rules help you include service accounts that Defender for Identity doesn't identify automatically. For example, some organizations name all their service accounts with a prefix like `srv`. Defender for Identity doesn't automatically detect such naming conventions. By creating a classification rule based on that pattern, you can include those accounts in the Service accounts view.

Classification rules work alongside Defender for Identity’s automatic discovery and provide a more complete and customized view of service accounts in your environment.

To create a rule:

1. Go to Settings > Microsoft Defender XDR > Service accounts classification.

1. Select on **+ Create a new rule**.

1. Enter a name for the rule.

2. Optional: Add a description.

1. Select one or more of the following filters:

- **Account display name**

- **Account domain**

- **Account SAM name**

- **Organizational unit**

1. Select Create to save the rule.

For more information about Defender for Identity details, see: [Investigate assets](/defender-for-identity/investigate-assets#identity-details).

## Related content

- [Service principal names](/windows/win32/ad/service-principal-names)

- [How to configure SPN](/windows-server/identity/ad-ds/manage/how-to-configure-spn?tabs=add%2Caduc)

If you run into any problems, we're here to help. To get assistance or support for your product issue, see how to open a support ticket at [Microsoft Defender for Identity support](support.md).


# Dashboard

# Identity Security dashboard overview (Preview)

The Microsoft Defender for Identity **Dashboard** page shows data to help you better analyze your security posture, understand how well you're protected, identify vulnerabilities, and perform recommended actions.

Use the **Dashboard** page to view critical insights and real-time data about identity threat detection and response (ITDR). View graphs and widgets that showcase important information related to unauthorized access, account compromise, insider threats, and abnormal activities, and then proactively monitor and manage potential identity-related security risks.

>[!NOTE]

>The **Identity Security** dashboard is being rolled out gradually to customers, and might not yet be available in your organization.

## Prerequisites

To access the Identity Security dashboard, you need:

- A Microsoft Defender for Identity license and an Entra ID Identity Protection license.

- A user role with at least the [Security Reader](/azure/active-directory/roles/permissions-reference#security-reader) permissions.

- To view a full list of recommendations and select all recommended action links, you need the [Global Administrator](/azure/active-directory/roles/permissions-reference#global-administrator) role.

> [!IMPORTANT]

> Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to scenarios when you can't use an existing role.

## Access the dashboard

To access the dashboard, sign into Microsoft Defender and select **Identities > Dashboard**.

<a name="summary-cards"></a>

## Review summary cards

The top of the dashboard shows summary cards for each coverage source category. Select links in the cards for more details, such as documentation or related recommendations in [Microsoft Secure Score](/microsoft-365/security/defender/microsoft-secure-score).

Each card shows identity counts and a coverage score gauge:

| Name | Description |

| -------- | ------- |

| **Identity Providers** | Shows the count of human identities, non-human identities, and agentic identities (Preview) from connected identity providers like Microsoft Entra ID, along with the coverage score. |

| **SaaS Applications** | Shows the count of human identities and non-human identities from connected SaaS applications, along with the coverage score. |

| **On-premises** | Shows the count of human identities and non-human identities from on-premises Active Directory environments, along with the coverage score. |

| **PAM & IGA** | Shows the status of privileged access management (PAM) and identity governance and administration (IGA) integrations, and prompts you to connect available solutions. |

| **Non-human identities** | Shows a donut chart of non-human identities (OAuth apps and service accounts) broken down by source: Entra ID, SaaS, and on-premises. |

| **Human identities** | Shows a donut chart of human identities broken down by source: Entra ID, SaaS, and on-premises. |

<a name="top-insights"></a>

## Review top insights

The following table describes the key insights shown on the dashboard:

| Name | Description |

| ----- | ---- |

| **Users identified in a risky lateral movement path** | Indicates any sensitive accounts with risky lateral movement paths, which are windows of opportunity for attackers and can expose risks.<br><br>We recommend that you take action on any sensitive accounts found with risky lateral movement paths to minimize your risk. <br><br>For more information, see [Understand and investigate Lateral Movement Paths (LMPs) with Microsoft Defender for Identity](understand-lateral-movement-paths.md). |

| **Dormant Active Directory users** | Lists accounts that have been left unused for at least 180 days. <br><br>Inactive accounts that are a part of sensitive groups provide an easy path into your organization. We recommend removing those users from sensitive groups. |

<a name="dashboard-widgets"></a>

## Understand dashboard widgets

The following table describes the widgets available on the dashboard:

| Name | Description |

| ----- | ---- |

| **Identity Security Deployment Status** | Shows the number of identities that are Protected, Need Attention, and Not Protected, giving you a quick view of your identity protection deployment progress. Select **Configure your identity protection** to review and improve your deployment.  |

| **Identity posture (Secure score)** | The score shown represents your organization's security posture with a focus on the *identity* score, reflecting the collective security state of your identities. The score is automatically updated in real-time to reflect the data shown in graphs and recommended actions. <br><br>Microsoft Secure Score updates daily with system data with new points for each recommended action taken.<br><br> For more information, see [Microsoft Secure Score](/microsoft-365/security/defender/microsoft-secure-score). |

| **Entra ID highly privileged** | Lists a summary of the sensitive accounts in your organization, including Entra ID Global Admins, Security Administrators, and accounts tagged as sensitive. Select **View all identities** to go to the identity inventory. |

| **Identity related incidents** | Lists alerts from both Defender for Identity and [Microsoft Entra ID Protection](/azure/active-directory/identity-protection/overview-identity-protection), and any corresponding, relevant incidents from the last 30 days. |

| **Useful guides** | Provides links to key documentation, including [What is Identity Security in Microsoft Defender?](/defender-xdr/identity-security/identity-security-overview), [Conditional access policies in Microsoft](/entra/identity/conditional-access/overview), and [How to increase my Identity security coverage in Defender?](/defender-xdr/identity-security/coverage-maturity). |

| **Domains with unsecured configurations** |  Lists Active Directory domains that have unsecured configuration settings. <br><br>Active Directory domains hold many security-related configurations, which, when misconfigured, can make organizations more susceptible to cyber-attacks. Make sure to configure your domains in accordance with security best practices to decrease the likelihood of identity compromise.  <br><br>For more information, see [Security assessment: Unsecure domain configurations](security-posture-assessments/identity-infrastructure.md#resolve-unsecure-domain-configurations). |

| **Active users at risk** | Lists active user accounts that may be vulnerable to security threats, unusual activities, or potential compromises. <br><br>Identifying and managing users at risk is a crucial aspect of maintaining a secure IT environment. Select **View all users** to investigate further. For more information, see [Remediate risks and unblock users in Microsoft Entra ID Protection](/entra/id-protection/howto-identity-protection-remediate-unblock). |

## Next steps

For more information, see [Microsoft Defender for Identity in the Microsoft Defender portal](/microsoft-365/security/defender/microsoft-365-security-center-mdi?bc=/defender-for-identity/breadcrumb/toc.json&toc=/defender-for-identity/TOC.json).


# Identity Security Initiative

# Identity Security Initiative (Preview)

Identity security is the practice of protecting the digital identities of individuals and organizations. This includes protecting passwords, usernames, and other credentials that can be used to access sensitive data or systems. Identity security is essential for protecting against a wide range of cyber threats, including phishing, malware, and data breaches.

## Prerequisites

- Your organization must have a Microsoft Defender for Identity license.

- [Review prerequisites and permissions needed](/security-exposure-management/prerequisites) for working with Security Exposure Management.

## View Identity Security Initiatives

1. Navigate to the [Microsoft Defender portal](https://security.microsoft.com/).

1. From the Exposure management section on the navigation bar, select **Exposure insights** **>** **Initiatives** to open the Identity Security page.

## Review security metrics

Metrics in security initiatives help you to measure exposure risk for different areas within the initiative. Each metric gathers together one or more recommendations for similar assets.

Metrics can be associated with one or more initiatives.

On the **Metrics** tab of an initiative, or in the Metrics section of Exposure Insights, you can see the metric state, its effect, and relative importance in an initiative, and recommendations to improve the metric.

We recommend that you prioritize metrics with the highest impact on Initiative Score level. This composite measure considers both the weight value of each recommendation and the percentage of noncompliant recommendations.

|Metric property |Description  |

|---------|---------|

|**Metric name**    | The name of the metric.        |

|**Progress**   |Shows the improvement of the exposure level for the metric from 0 (high exposure) to 100 (no exposure).         |

|**State**   | Shows if the metric needs attention or if the target was met.       |

|**Total assets**  | Total number of assets under the metric scope.        |

|**Recommendations**   | Security recommendations associated with the metric.        |

|**Weight**    | The relative weight (importance) of the metric within the initiative, and its effect on the initiative score. Shown as High, Medium, and Low. It can also be defined as Risk accepted.        |

|**14-day trend** | Shows the metric value changes over the last 14 days.        |

|**Last updated** | Shows a timestamp of when the metric was last updated.

> [!NOTE]

> The Affected assets experience isn't fully supported during the Preview phase.

## View Identity security recommendations

The Security recommendations tab displays a list of prioritized remediation actions related to your identity security posture. Each recommendation is evaluated for compliance and mapped to its corresponding risk impact, workload, and domain. This view helps you triage and take action based on urgency and business relevance.

Sort the recommendations by any of the headings or filter them based on your task needs.

| **Column**             | **Description**                                                                 |

|------------------------|---------------------------------------------------------------------------------|

| **Name**               | The name of the recommended action (for example, *Configure VPN integration*, *Enable MFA*). |

| **State**              | Indicates whether the recommendation is *Compliant* or *Not Compliant*.         |

| **Impact**             | The security impact level (Low, Medium, or High) of implementing the recommendation. |

| **Workload**           | The Microsoft service area the recommendation applies to (for example, Defender for Identity, Microsoft Entra ID). |

| **Domain**             | The security domain (for example, identity, apps) associated with the recommendation.   |

| **Last calculated**    | The most recent time the recommendation's status was evaluated.                 |

| **Last state change**  | When the recommendation’s compliance state last changed.                        |

| **Related initiatives**| Number of security initiatives impacted by this recommendation.                 |

| **Related metrics**    | Number of security metrics that this recommendation contributes to.             |

Security Exposure Management categorizes recommendations by compliance status, as follows:

- **Compliant**: Indicates that the recommendation was implemented successfully.

- **Not complaint**: Indicates that the recommendation wasn't fixed.

## Set target score

You can set a customized target score for the initiative, taking your organization’s unique set of circumstances, priorities, and risk appetite into account.

To set a target store, select the initiative, and then select **Set target score** from the top of the initiative pane.

## Related content

- [Review security initiatives](/security-exposure-management/initiatives)

- [Investigate security initiative metrics](/security-exposure-management/security-metrics)


# Password Protection

# Investigate identity password protection (Preview)

Compromised credentials remain one of the most common ways attackers gain initial access, even in environments that use multifactor authentication and modern authentication protocols. Password risks are often spread between different tools and identity providers, which can make it difficult for security teams to assess exposure and prioritize remediation.

The **Password protection** page in Microsoft Defender consolidates password-related risks from your identity sources into a single, prioritized view. Use it to find leaked credentials, exposed passwords, weak password policies, and configuration issues in on-premises Active Directory, Microsoft Entra ID, federated identities, and non-Microsoft providers like Okta. For each issue, you can see why an account is at risk and take action—such as resetting a password or disabling an account—directly from the page.

## Prerequisites

To access the **Password protection** page, you need:

- A Microsoft Defender for Identity license, or another license that includes Defender for Identity (such as E5), and a Microsoft Entra ID Protection license.

- A user role with at least [Security Reader](/azure/active-directory/roles/permissions-reference#security-reader) permissions.

## The Password protection page

In the Microsoft Defender portal, select **Identities** > **Password protection**.

The page includes a left panel where you select the identity source you want to review. Supported identity sources include:

- **Active Directory**: Available on all four tabs.

- **Microsoft Entra ID**: Available on the Leaked Credentials tab.

- **Okta**: Available on the Password Hygiene and Password Policies tabs.

The page has four tabs:

- **Password Hygiene**: Shows accounts with password weaknesses that attackers commonly exploit. Each item is a recommendation you can act on to reduce risk.

- **Password Policies**: Shows password policies from your identity providers side by side. Use this tab to check whether your policies meet current security standards. See [Policy information](#policy-information) for details.

- **Leaked Credentials**: Shows accounts with credentials that were found outside your organization, for example on public paste sites or the dark web. From this tab, you can reset passwords or disable accounts, individually or in bulk.

- **Exposed Passwords**: Shows accounts and settings that store or expose passwords in insecure ways, such as in plain text or in easily discoverable locations. Examples include clear-text credentials in Active Directory attributes (identified using AI-based detection) and reversible passwords in Group Policy Objects (GPOs).

## Policy information

The **Password Policies** tab shows:

| Column | Description |

|---|---|

| **Name** | The name of the password policy. |

| **Provider** | The identity provider that enforces the policy. |

| **Maximum password age** | The maximum number of days before a password must be changed. |

| **Minimum password age** | The minimum number of days before a password can be changed. |

| **Password history length** | The number of previous passwords that can't be reused. |

| **Password complexity** | Whether password complexity requirements are enabled. |

| **Lockout threshold** | The number of failed sign-in attempts before the account is locked. |

| **Lockout duration** | The duration of the account lockout after the threshold is reached. |

## Account information

The **Password Hygiene**, **Leaked Credentials**, and **Exposed Passwords** tabs show account-level data with this information:

| Column | Description |

|---|---|

| **Name** | The display name of the account. |

| **SID** | The Security Identifier of the account. |

| **Entity type** | The type of entity (for example, User or Computer). |

| **Domain** | The Active Directory domain the account belongs to. |

| **Service account type** | The type of service account, if applicable. |

## Related content

- [The Identity Security dashboard](/defender-for-identity/dashboard)

- [View your identity coverage and maturity](/defender-xdr/identity-security/coverage-maturity)

- [Unified identity security recommendations](/defender-xdr/identity-security/identity-security-recommendations)


# Investigate Domain

# Investigate an Active Directory domain (Preview)

Active Directory domains are frequently targeted in identity-based attacks. Configuration issues such as unhealthy sensors, weak security policies, or risky trust relationships can expose an environment, but the information needed to assess a domain's security is often distributed between different tools and views.

The Active Directory domain page in Microsoft Defender brings together domain health, sensor coverage, security policies, trust relationships, and recommendations for your on-premises Active Directory environment into a single view. Use it to determine whether a domain is healthy and fully monitored, identify configuration or policy issues that increase risk, review trust relationships, and act on prioritized recommendations.

## Prerequisites

- A Microsoft Defender for Identity license, or another license that includes Defender for Identity (such as E5).

- A user role with at least [Security Reader](/azure/active-directory/roles/permissions-reference#security-reader) permissions.

## Access the Domain page

You can reach the Active Directory domain page through multiple entry points in Microsoft Defender:

- Select a domain name from the **Domain** column in the identity inventory.

- Select a domain from a domain-related security alert or incident.

- Search for a domain by name using the global search bar.

To switch between domains when you're on the domain page, use the domain selector at the top right of the page.

## Overview tab

The **Overview** tab provides a domain summary.

| Section | Description |

|---|---|

| **Domain details** | Shows key domain attributes: <ol><li>Provider</li><li>Domain name</li><li>Functional level</li><li>Creation date</li><li>Identities count</li><li>Service accounts count</li><li>Group accounts count</li><li>Computer accounts count</li></ol> Select any count to view the filtered list. |

| **Properties** | Shows the domain's **Canonical Name**, **SID**, and **ID**. |

| **Deployment Health** | Shows sensor deployment coverage and health status. A 100% coverage score means all domain controllers have sensors deployed. Select a deployment issue to navigate to sensor deployment settings. |

| **Health Score** | Displays an overall health score (Low, Medium, or High) based on identity infrastructure coverage, sensor health, and active recommendations. Select **How to fix** to view recommended actions. |

| **All Domain Identities** | Shows the total number of identities, including how many are classified as **Critical** or **Sensitive**. Select **View domain identities** to open the identity inventory filtered to this domain. |

| **Service accounts** | Shows a donut chart of service accounts by type: sMSA (standalone Managed Service Account), gMSA (group Managed Service Account), and User. Select **View domain service accounts** to open the service accounts page. |

| **Sensitive Entities** | Shows the count of sensitive identities, groups, and computers. Select any count to view the details. |

| **Active Recommendations** | Lists security recommendations that affect the health score, with links to remediation guidance. For example, the **Unsecure Domain Configurations** recommendation links to the corresponding security posture assessment. |

| **Group Policies** | Lists Group Policy Objects (GPOs) applied in the domain. Use this section to verify active policies and identify domains with no GPOs configured. |

## Incidents and alerts tab

Shows all incidents and alerts connected to the domain. Data on this tab includes only incidents and alerts created on or after February 1, 2026.

The tab includes default filters for **Status** (New, In progress) and **Alert severity** (High, Medium, Low). You can export, copy the list link, refresh, and customize columns.

| Column | Description |

|---|---|

| **Incident name** | The name of the incident. |

| **Incident Id** | The unique identifier of the incident. |

| **Priority score** | The priority score assigned to the incident. |

| **Tags** | Tags associated with the incident. |

| **Severity** | The severity level of the incident (High, Medium, Low). |

| **Investigation state** | The current state of the investigation. |

| **Categories** | The threat categories associated with the incident. |

| **Impacted assets** | The assets affected by the incident. |

| **Active alerts** | The number of active alerts in the incident. |

## Security Policies tab

Provides human-readable summaries of key Active Directory security policies in four cards. Use this tab to review critical Active Directory configurations and check whether they meet current security standards.

| Card | Details |

|---|---|

| **Password Policy** | Password maximum age, minimum age, history, complexity, authenticated password change only, no clear-text password change, admin lockout after failed attempts, password store clear text, and password change is refused. |

| **Account Lockout Policy** | Lockout duration and lockout threshold. |

| **Kerberos Policy** | Maximum ticket age and maximum renewal age. |

| **LDAP & Machine Account** | LDAP signing policy and machine account quota. If the domain has active recommendations for insecure configurations, a warning banner appears with a link to view the recommendations. |

## Trusts tab

Shows trust relationships for the domain. You can export the list.

| Column | Description |

|---|---|

| **Display Name** | The name of the trusted domain. |

| **Direction** | The direction of the trust (for example, Inbound, Outbound, or Bidirectional). |

| **Attributes** | The attributes of the trust relationship. |

Use this tab to review which domains trust each other and in which direction.

## Groups tab

Lists the groups in the domain. You can filter by tags, type, and scope. You can mark groups as sensitive to support exposure analysis and detect potential attack paths.

| Column | Description |

|---|---|

| **Name** | The name of the group. Select to view group details. |

| **Tags** | Tags assigned to the group, such as Sensitive. |

| **Type** | The group type (for example, Security). |

| **Scope** | The group scope (Universal, Global, or DomainLocal). |

| **Direct Members** | The number of direct members in the group. |

| **Canonical Name** | The full canonical name path of the group in Active Directory. |

| **Description** | The description of the group. |

## Computers tab

Lists the computer accounts in the domain. You can filter by tags. You can mark computer accounts as sensitive to support exposure analysis and detect potential attack paths.

| Column | Description |

|---|---|

| **Name** | The name of the computer account. Select to view computer details. |

| **Tags** | Tags assigned to the computer, such as Sensitive. |

| **Update Time** | The date and time the computer account was last updated. |

| **SID** | The Security Identifier of the computer account. |

| **Canonical Name** | The full canonical name path of the computer in Active Directory. |

| **Description** | The description of the computer account. |

## Related content

- [View the identity inventory](/defender-for-identity/identity-inventory)

- [Investigate and protect Service Accounts](/defender-for-identity/service-account-discovery)

- [Security posture assessments](/defender-for-identity/security-assessment)

- [Understand and investigate lateral movement paths](/defender-for-identity/understand-lateral-movement-paths)


# Security Assessment

# Microsoft Defender for Identity's security posture assessments

Typically, organizations of all sizes have limited visibility into whether or not their on-premise and cloud apps and services could introduce a security vulnerability to their organization. The problem of limited visibility is especially true regarding use of unsupported or outdated components.

While your company might invest significant time and effort on hardening identities and identity infrastructure (such as Active Directory, Active Directory Connect) as an ongoing project, it's easy to remain unaware of common misconfigurations and use of legacy components that represent one of the greatest threat risks to your organization.

Microsoft security research reveals that most identity attacks utilize common misconfigurations in Active Directory and continued use of legacy components (such as NTLMv1 protocol) to compromise identities and successfully breach your organization. To combat this effectively, Microsoft Defender for Identity now offers proactive identity security posture assessments to detect and recommend actions across your on-premise Active Directory configurations.

## What do Defender for Identity security assessments provide?

Defender for Identity security posture assessments are available in [Microsoft Secure Score](/microsoft-365/security/defender/microsoft-secure-score), and provide:

- **Detections and contextual data** on known exploitable components and misconfigurations, along with relevant paths for remediation.

- **Active monitoring for your on-premise and cloud identities and identity infrastructure**, watching for weak spots with the existing Defender for Identity sensor.

- **Accurate assessment reports** of your current organization security posture, for quick responses and effect monitoring in a continuous cycle.

Microsoft Secure Score is a measurement of an organization's security posture, with a higher number indicating more recommended actions taken. It can be found at <https://security.microsoft.com/securescore> in the [Microsoft Defender portal](/microsoft-365/security/defender/microsoft-365-defender).

### Categorization of Defender for Identity security posture assessments

Defender for Identity security posture assessments have five key categories. Each category addresses specific identity security risks and provides remediation guidance.

- **Hybrid security**: Identifies misconfigurations in environments that integrate on-premises (e.g., Active Directory) and cloud-based identity providers (e.g., Microsoft Entra ID, Okta). Assesses risks related to synchronization, authentication, and authorization across platforms.

- **Identity infrastructure**: Detects misconfigurations and vulnerabilities in core identity components, including domain controllers.

- **Certificates**: Assesses Active Directory Certificate Services (AD CS) for security gaps, such as misconfigured certificate templates or weak certificate authority settings. Identifying and addressing these issues helps prevent unauthorized access that could arise from certificate-related vulnerabilities.

- **Group policy**: Analyzes Group Policy configurations to identify settings that might allow privilege escalation or unauthorized lateral movement within the network. Ensuring secure Group Policy settings helps maintain proper access controls and system configurations.

- **Accounts**: Reviews users, devices, and groups to pinpoint security risks such as weak passwords, inactive accounts, or improper permissions.

- **Cloud identities**: Evaluates cloud identity configurations in Okta accounts for security gaps, such as missing MFA settings or privileged Okta accounts, and provides remediation guidance.

## Access Defender for Identity security posture assessments

> [!NOTE]

> You must have a Defender for Identity license to view Defender for Identity security posture assessments in Microsoft Secure Score.

>

> Additionally, while *certificate template* assessments are available to all customers with AD CS installed in their environment, *certificate authority* assessments are available only to customers who have installed a sensor on an AD CS server.

>

> Hybrid security recommendations will be available only if Microsoft Defender for Identity sensor is installed on servers running Microsoft Entra Connect services.

>

> For more information, see [Configuring sensors for AD FS, AD CS and Microsoft Entra Connect.](https://aka.ms/DeployMdiSensorOnYourIdentityInfrastructure)

**To access identity security posture assessments**:

1. Open the [Microsoft Secure Score dashboard](https://security.microsoft.com/securescore).

1. Select the **Recommended actions** tab. You can search for a particular recommended action, or filter the results (for example, by the category **Identity**).

[![Recommended actions.](media/recommended-actions.png)](media/recommended-actions.png#lightbox)

1. For more details, select the assessment.

[![Select the assessment.](media/select-assessment.png)](media/select-assessment.png#lightbox)

[!INCLUDE [secure-score-note](../includes/secure-score-note.md)]

## Next steps

- [Learn more about Microsoft Secure Score](/microsoft-365/security/defender/microsoft-secure-score)

- [Check out the Defender for Identity forum!](https://aka.ms/MDIcommunity)


# Hybrid Security

# Hybrid security posture assessments

This article lists all hybrid security posture assessments for Microsoft Defender for Identity.

> [!NOTE]

> While assessments are updated in near real time, scores and statuses are updated every 24 hours. While the list of impacted entities is updated within a few minutes of your implementing the recommendations, the status may still take time until it's marked as __Completed__.

## Change password for Microsoft Entra seamless SSO account

**Description**

This report lists all Microsoft Entra seamless SSO computer accounts with password last set over 90 days ago.

**User impact**

Microsoft Entra seamless SSO automatically signs in users when they're using their corporate desktops that are connected to your corporate network. Seamless SSO provides your users with easy access to your cloud-based applications without using any other on-premises components. When setting up Microsoft Entra Seamless SSO, a computer account named AZUREADSSOACC is created in Active Directory. By default, the password for this Azure SSO computer account isn't automatically updated every 30 days. This password functions as a shared secret between AD and Microsoft Entra, enabling Microsoft Entra to decrypt Kerberos tickets used in the seamless SSO process between Active Directory and Microsoft Entra ID. If an attacker gains control of this account, they can generate service tickets for the AZUREADSSOACC account on behalf of any user and impersonate any user within the Microsoft Entra tenant that has been synchronized from

**Implementation**

1. Review the recommended action at [https://security.microsoft.com/securescore?viewid=actions](https://security.microsoft.com/securescore?viewid=actions) for __Change password for Microsoft Entra seamless SSO account.__

1. Review the list of exposed entities to discover which of your Microsoft Entra SSO computer accounts have a password more than 90 days old.

1. Take appropriate action on those accounts by following the steps described in [how to roll over the Microsoft Entra SSO account password](https://aka.ms/RollOverAzureadssoAccount) article.

> [!NOTE]

> This security assessment is available only if Microsoft Defender for Identity sensor is installed on servers running Microsoft Entra Connect services and Sign on method as part of Microsoft Entra Connect configuration is set to single sign-on and the SSO computer account exists. Learn more about Microsoft Entra seamless sign-on [here](/entra/identity/hybrid/connect/how-to-connect-sso).

## Rotate password for Microsoft Entra Connect AD DS Connector account

**Description**

This report lists all MSOL accounts in your organization with password last set over 90 days ago.

**User impact**

Smart attackers are likely to target Microsoft Entra Connect in on-premises environments, and for good reason. The Microsoft Entra Connect server can be a prime target, especially based on the permissions assigned to the AD DS Connector account (created in on-premises AD with the MSOL_ prefix).

It's important to change the password of MSOL accounts every 90 days to prevent attackers from allowing use of the high privileges that the connector account typically holds - replication permissions, reset password and so on.

**Implementation**

1. Review the recommended action at[ https://security.microsoft.com/securescore?viewid=actions](https://security.microsoft.com/securescore?viewid=actions) for **Rotate password for Microsoft Entra Connect AD DS Connector account.**

1. Review the list of exposed entities to discover which of your AD DS Connector accounts have a password more than 90 days old.

1. Take appropriate action on those accounts by following the steps on [how to change the AD DS Connector account password](https://aka.ms/MicrosoftEntraIdPasswordChangeSyncService).

> [!NOTE]

> This security assessment is only available if Microsoft Defender for Identity sensor is installed on servers running Microsoft Entra Connect services.

## Remove unnecessary replication permissions for Microsoft Entra Connect AD DS Connector account

**Description**

Smart attackers are likely to target Microsoft Entra Connect in on-premises environments, and for good reason. The Microsoft Entra Connect server can be a prime target, especially based on the permissions assigned to the AD DS Connector account (created in on-premises AD with the MSOL_ prefix). In the default 'express' installation of Microsoft Entra Connect, the connector service account is granted replication permissions, among others, to ensure proper synchronization. If Password Hash Sync isn’t configured, it’s important to remove unnecessary permissions to minimize the potential attack surface.

> [!NOTE]

> - This security assessment is available only if Microsoft Defender for Identity sensor is installed on servers running Microsoft Entra Connect services.

>

> - If the Password Hash Sync (PHS) sign-on method is set up, AD DS Connector accounts with replication permissions won't be affected because those permissions are necessary.

> -  For environments with multiple Microsoft Entra Connect servers, it’s crucial to install sensors on each server to ensure Microsoft Defender for Identity can fully monitor your setup. If detected that your Microsoft Entra Connect configuration doesn't utilize Password Hash Sync, which means that replication permissions aren't necessary for the accounts in the Exposed Entities list. Ensure that each exposed MSOL account isn't required for Replication Permissions by any other applications.

**Implementation**

1. Review the recommended action at [https://security.microsoft.com/securescore?viewid=actions](https://security.microsoft.com/securescore?viewid=actions) for Remove unnecessary replication permissions for __Microsoft Entra Connect AD DS Connector account.__

1. Review the list of exposed entities to discover which of your AD DS Connector accounts have unnecessary replication permissions.

1. Take appropriate action on those accounts and remove their 'Replication Directory Changes' and 'Replication Directory Changes All' permissions by unchecking the following permissions:

## Remove unsafe permissions on sensitive Microsoft Entra Connect accounts

**Description**

Microsoft Entra Connect accounts like AD DS Connector account (also known as MSOL_) and Microsoft Entra Seamless SSO computer account (AZUREADSSOACC) have powerful privileges, including replication and password reset rights. If these accounts are granted unsafe permissions, attackers could exploit them to gain unauthorized access, escalate privileges, or take control of hybrid identity infrastructure. This could lead to account takeovers, unauthorized directory modifications, and a broader compromise of both on-premises and cloud environments.

> [!NOTE]

> This security assessment will be available only if Microsoft Defender for Identity sensor is installed on servers running Microsoft Entra Connect services and Sign on method as part of Microsoft Entra Connect configuration is set to single sign-on and the SSO computer account exists. Learn more about Microsoft Entra seamless sign-on **[here](/entra/identity/hybrid/connect/how-to-connect-sso)**.

**Implementation**

1. Review the recommended action at[ https://security.microsoft.com/securescore?viewid=actions](https://security.microsoft.com/securescore?viewid=actions) for Remove unsafe permissions on sensitive Microsoft Entra Connect accounts.

1. Review the list of exposed entities to identify accounts with unsafe permissions. For example:

1. If you select on "Click to expand" you can find more details about the granted permissions. For example:

1. For each exposed account, remove problematic permissions that allow unprivileged accounts to takeover critical hybrid assets.

## Replace Enterprise or Domain Admin account for Microsoft Entra Connect AD DS Connector account

**Description**

Smart attackers often target Microsoft Entra Connect in on-premises environments due to the elevated privileges associated with its AD DS Connector account (typically created in Active Directory with the MSOL_ prefix). Using an **Enterprise Admin** or **Domain Admin** account for this purpose significantly increases the attack surface, as these accounts have broad control over the directory.

Starting with [Entra Connect build 1.4.###.#](/entra/identity/hybrid/connect/reference-connect-accounts-permissions), Enterprise Admin and Domain Admin accounts can no longer be used as the AD DS Connector account. This best practice prevents over-privileging the connector account, reducing the risk of domain-wide compromise if the account is targeted by attackers. Organizations must now create or assign a lower-privileged account specifically for directory synchronization, ensuring better adherence to the principle of least privilege and protecting critical admin accounts.

> [!NOTE]

> This security assessment will be available only if Microsoft Defender for Identity sensor is installed on servers running Microsoft Entra Connect services.

**Implementation**

1. Review the recommended action at[ https://security.microsoft.com/securescore?viewid=actions](https://security.microsoft.com/securescore?viewid=actions) for Replace Enterprise or Domain Admin account for Microsoft Entra Connect AD DS Connector account.

1. Review the exposed accounts and their group memberships. The list contains members of Domain/Enterprise Admins through direct and recursive membership.

1. Perform one of the following actions:

- Remove MSOL_ user account user from privileged groups, ensuring it retains the necessary permissions to function as the Microsoft Entra Connect Connector account.

- Change the Microsoft Entra Connect AD DS Connector account (MSOL_) to a lower-privileged account.

## Next steps

[Learn more about Microsoft Secure Score](/microsoft-365/security/defender/microsoft-secure-score)


# Identity Infrastructure

# Identity infrastructure security assessments

Learn about Microsoft Defender for Identity security posture assessments for identity infrastructure.

> [!NOTE]

> While assessments are updated in near real time, scores and statuses are updated every 24 hours. While the list of impacted entities is updated within a few minutes of your implementing the recommendations, the status may still take time until it's marked as __Completed__.

## Built-in Active Directory Guest account is enabled

**Description**

This recommendation indicates whether an AD Guest account is enabled in your environment.

The goal is to **ensure** that the Guest account of the domain is **not enabled**.

**User impact**

The on-premises Guest account is a built-in, non-nominative account that allows anonymous access to Active Directory. Enabling this account permits access to the domain without requiring a password, potentially posing a security threat.

**Implementation**

1. Review the list of exposed entities to discover if there's a Guest account, which is enabled.

1. Take appropriate action on those accounts by **disabling** the account.

For example:

## Change Domain Controller computer account old password

**Description**

This recommendation lists all domain controller’s computer accounts with password last set over 45 days ago.

A Domain Controller (DC) is a server in an Active Directory (AD) environment that manages user authentication and authorization, enforces security policies, and stores the AD database. It handles logins, verifies permissions, and ensures secure access to network resources. Multiple DCs provide redundancy for high availability.

Domain Controllers with old passwords are at heightened risk of compromise and could be more easily taken over. Attackers can exploit outdated passwords, gaining prolonged access to critical resources and weakening network security. It could indicate a Domain controller that is no longer functioning in the domain.

**Implementation**

1. Verify Registry Values:

- HKLM\System\CurrentControlSet\Services\Netlogon\Parameters\DisablePasswordChange is set to 0 or is nonexistent.

- HKLM\System\CurrentControlSet\Services\Netlogon\Parameters\MaximumPasswordAge is set to 30.

1. Reset Incorrect Values:

- Reset any incorrect values to their default settings.

- Check Group Policy Objects (GPOs) to ensure they don't override these settings.

1. If these values are correct, check if the NETLOGON service is started with sc.exe query netlogon.

1. Validate Password Synchronization by Running nltest /SC_VERIFY: (with DomainName being the domain NetBIOS name) can check the synchronization status and should display0 0x0 NERR_Success for both verifications.

> [!TIP]

> For more information about computer account’s password process check this blog post about [Machine accounts password process](https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/machine-account-password-process/ba-p/396026).

## Disable Print spooler service on domain controllers

**Description**

Print spooler is a software service that manages printing processes. The spooler accepts print jobs from computers and makes sure that printer resources are available. The spooler also schedules the order in which print jobs are sent to the print queue for printing. In the early days of personal computers, users had to wait until files printed before performing other actions. Thanks to modern print spoolers, printing now has minimal impact on overall user productivity.

While seemingly harmless, any authenticated user can remotely connect to a domain controller's print spooler service, and request an update on new print jobs. Also, users can tell the domain controller to send the notification to the system with [unconstrained delegation](/defender-for-identity/security-assessment-unconstrained-kerberos). These actions test the connection and expose the domain controller computer account credential (**Print spooler** is owned by SYSTEM).

Due to the possibility for exposure, domain controllers and Active Directory admin systems need to have the **Print spooler** service disabled. The recommended way to do this is using a Group Policy Object (GPO).

While this security assessment focuses on domain controllers, any server is potentially at risk to this type of attack.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> to discover which of your domain controllers has the **Print spooler** service enabled.

1. Take appropriate action on the at-risk domain controllers and actively remove the Print spooler service either manually, through GPO or other types of remote commands.

1. Due to the possibility for exposure, domain controllers and Active Directory admin systems need to have the **Print spooler** service disabled. Fix this specific issue by disabling the Print Spooler service on all servers that don't require it.

> [!NOTE]

>

> - Make sure to investigate your **Print spooler** settings, configurations, and dependencies before disabling this service and preventing active printing workflows.

> - The domain controller role [adds a thread to the spooler service](/windows-server/security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server#print-spooler) that is responsible for performing print pruning – removing the stale print queue objects from the Active Directory. Therefore, the security recommendation to disable the **Print spooler** service is a trade-off between security and the ability to perform print pruning. To address the issue, you should consider periodically pruning stale print queue objects.

## Remove local admins on identity assets

**Description**

Accounts with indirect control over an identity system, such as AD FS, AD CS, Active Directory, and so on, have the rights to escalate their privileges within the environment, which can lead to obtaining Domain Admin access or equivalent.

Every local admin on a Tier-0 system is an indirect Domain Admin from an attacker's point of view.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> for **Remove local admins on identity assets**.

For example:

1. Review this list of exposed entities to discover which of your accounts have local admin rights on your identity assets.

1. Take appropriate action on those entities by removing their privileged access rights.

1. To achieve a full score, you must remediate all exposed entities.

## Unmonitored domain controllers

**Description**

An essential part of the Microsoft Defender for Identity solution requires that its sensors are deployed on all organizational domain controllers, providing a comprehensive view for all user activities from every device.

For this reason, Defender for Identity continuously monitors your environment to identify domain controllers without an installed Defender for Identity sensor, and reports on these unmonitored servers to assist you in managing full coverage of your environment.

In order to operate at maximum efficiency, all domain controllers must be monitored with Defender for Identity sensors. Organizations that fail to remediate unmonitored domain controllers, reduce visibility into their environment and potentially expose their assets to malicious actors.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> to discover which of your domain controllers are unmonitored.

1. Take appropriate action on those domain controllers by [installing and configuring monitoring sensors](/defender-for-identity/sensor-settings#domain-controller-status).

## Unmonitored ADCS servers

**Description**

Unmonitored Active Directory Certificate Services (AD CS) servers pose a significant risk to your organization’s identity infrastructure. AD CS, the backbone of certificate issuance and trust, is a high-value target for attackers aiming to escalate privileges or forge credentials. Without proper monitoring, attackers can exploit these servers to issue unauthorized certificates, enabling stealthy lateral movement and persistent access. Deploy Microsoft Defender for Identity version 2.0 sensors on all AD CS servers to mitigate this risk. These sensors provide real-time visibility into suspicious activity, detect advanced threats, and generate actionable alerts based on security events and network behavior.

**Implementation**

> [!NOTE]

> This security assessment is only available if Microsoft Defender for Endpoint detects eligible ADCS servers in the environment. In some cases, servers running ADCS might not be identified with the required role and therefore will not appear in this assessment, even if they exist in the environment.

1. Review the recommended action at https://security.microsoft.com/securescore?viewid=actions to discover which of your AD CS servers are unmonitored.

1. Go to the **Microsoft Defender portal > Settings > Identities > Sensors**. You can view the already installed sensors in your environment and download the install package to deploy them on your remaining servers.

1. Take appropriate action on those servers by [configuring monitoring sensors](/defender-for-identity/deploy/active-directory-federation-services).

## Unmonitored ADFS servers

This article describes the Microsoft Defender for Identity's unmonitored Active Directory Federation Services (ADFS) servers security posture assessment report.

**Description**

Unmonitored Active Directory Federation Services (ADFS) servers are a significant security risk to organizations. ADFS controls access to both cloud and on-premises resources as the gateway for federated authentication and single sign-on. If attackers compromise an ADFS server, they can issue forged tokens and impersonate any user, including privileged accounts. Such attacks might bypass multi-factor authentication (MFA), conditional access, and other downstream security controls, making them particularly dangerous. Without proper monitoring, suspicious activity on ADFS servers might go undetected for extended periods. Deploying Microsoft Defender for Identity version 2.0 sensors on ADFS servers is essential. These sensors enable real-time detection of suspicious behavior and help prevent token forgery, abuse of trust relationships, and stealthy lateral movement within the environment.

**Implementation**

> [!NOTE]

> This security assessment is only available if Microsoft Defender for Endpoint detects eligible ADFS servers in the environment. In some cases, servers running ADFS might not be identified with the required role and therefore will not appear in this assessment, even if they exist in the environment.

1. Review the recommended action at https://security.microsoft.com/securescore?viewid=actions to discover which of your ADFS servers are unmonitored.

1. Go to the **Microsoft Defender portal > Settings > Identities > Sensors**. You can view the already installed sensors in your environment and download the install package to deploy them on your remaining servers.

1. Take appropriate action on those servers by [configuring monitoring sensors](/defender-for-identity/deploy/active-directory-federation-services).

## Unmonitored Microsoft Entra Connect servers

**Description**

Unmonitored Microsoft Entra Connect servers (formerly Azure AD Connect) pose a significant security risk in hybrid identity environments. These servers synchronize identities between on-premises Active Directory and Entra ID. They can introduce, modify, or remove accounts and attributes that directly affect cloud access.

If an attacker compromises a Microsoft Entra Connect server, they can inject shadow admins, manipulate group memberships, or sync malicious changes into the cloud without triggering traditional alerts.

These servers operate at the intersection of on-premises and cloud identity, making them a prime target for privilege escalation and stealthy persistence. Without monitoring, such attacks can go undetected. Deploying Microsoft Defender for Identity version 2.0 sensors on Microsoft Entra Connect servers is critical. These sensors help detect suspicious activity in real time, protect the integrity of your hybrid identity bridge, and prevent full-domain compromise from a single point of failure.

**Implementation**

> [!NOTE]

> This security assessment is only available if Microsoft Defender for Endpoint detects eligible Microsoft Entra Connect servers in the environment. In some cases, servers running Entra Connect might not be identified with the required role and therefore will not appear in this assessment, even if they exist in the environment.

1. Review the recommended action at https://security.microsoft.com/securescore?viewid=actions to discover which of your Microsoft Entra Connect servers are unmonitored.

1. Go to the **Microsoft Defender portal > Settings > Identities > Sensors**. You can view the already installed sensors in your environment and download the install package to deploy them on your remaining servers.

1. Take appropriate action on those servers by [configuring monitoring sensors](/defender-for-identity/deploy/active-directory-federation-services).

## Resolve unsecure domain configurations

**Description**

Microsoft Defender for Identity continuously monitors your environment to identify domains with configurations values that expose a security risk, and reports on these domains to assist you in protecting your environment.

Organizations that fail to secure their domain configurations leave the door unlocked for malicious actors.

Malicious actors, much like thieves, often look for the easiest and quietest way into any environment. Domains configured with unsecure configurations are windows of opportunity for attackers and can expose risks.

For example, if LDAP signing isn't enforced, an attacker can compromise domain accounts. This is especially risky if the account has privileged access to other resources, as with the [KrbRelayUp attack](https://www.microsoft.com/security/blog/2022/05/25/detecting-and-preventing-privilege-escalation-attacks-leveraging-kerberos-relaying-krbrelayup/).

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> to discover which of your domains have unsecure configurations.

1. Take appropriate action on these domains by modifying or removing the relevant configurations.

1. Use the remediation appropriate to the relevant configurations as described in the following table.

| Recommended action | Remediation | Reason |

| --- | --- | --- |

|**Enforce LDAP Signing policy to "Require signing"** | We recommend you require domain controller level LDAP signing. To learn more about LDAP server signing, see [Domain controller LDAP server signing requirements](/windows/security/threat-protection/security-policy-settings/domain-controller-ldap-server-signing-requirements). | Unsigned network traffic is susceptible to man-in-the-middle attacks.

| **Set ms-DS-MachineAccountQuota to "0"**             | Set the [MS-DS-Machine-Account-Quota](/windows/win32/adschema/a-ms-ds-machineaccountquota) attribute to "0". | Limiting the ability of non-privileged users to register devices in the domain. For more information about this particular property and how it affects device registration, see [Default limit to number of workstations a user can join to the domain](/troubleshoot/windows-server/identity/default-workstation-numbers-join-domain). |

## Next steps

[Learn more about Microsoft Secure Score](/microsoft-365/security/defender/microsoft-secure-score)


# Certificates

# Security assessment: Certificates

This article describes Microsoft Defender for Identity's **Certificates** security posture assessment report.

> [!NOTE]

> Make sure to test your settings in a controlled environment before turning them on in production.

> While assessments are updated in near real time, scores and statuses are updated every 24 hours.  While the list of impacted entities is updated within a few minutes of your implementing the recommendations, the status may still take time until it's marked as **Completed**.

## Enforce encryption for RPC certificate enrollment interface (ESC11)

**Description**

Active Directory Certificate Services (AD CS) supports certificate enrollment using the RPC protocol, specifically with the MS-ICPR interface. In such cases, the CA settings determine the security settings for the RPC interface, including the requirement for packet privacy.

If the `IF_ENFORCEENCRYPTICERTREQUEST` flag is turned on, the RPC interface only accepts connections with the `RPC_C_AUTHN_LEVEL_PKT_PRIVACY` authentication level. This is the highest authentication level, and requires each packet to be signed and encrypted so as to prevent any kind of relay attack. This is similar to `SMB Signing` in the SMB protocol.

If the RPC enrollment interface doesn't require packet privacy, it becomes vulnerable to relay attacks (ESC11). The `IF_ENFORCEENCRYPTICERTREQUEST` flag is on by default, but is often turned off to allow clients that can't support the required RPC authentication level, such as clients running Windows XP.

>[!NOTE]

>This assessment is available only to customers who have installed a sensor on an AD CS server.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> for enforcing encryption for RPC certificate enrollment.

1. Research why the `IF_ENFORCEENCRYPTICERTREQUEST` flag is turned off.

1. Make sure to turn the `IF_ENFORCEENCRYPTICERTREQUEST` flag on to remove the vulnerability.

To turn on the flag, run:

```cmd

certutil -setreg CA\InterfaceFlags +IF_ENFORCEENCRYPTICERTREQUEST

```

To restart the service, run:

```cmd

net stop certsvc & net start certsvc

```

Make sure to test your settings in a controlled environment before turning them on in production.

## Edit insecure ADCS certificate enrollment IIS endpoints (ESC8)

**Description**

Active Directory Certificate Services (AD CS) supports certificate enrollment through various methods and protocols, including enrollment via HTTP using the Certificate Enrollment Service (CES) or the Web Enrollment interface (Certsrv).

If the IIS endpoint allows NTLM authentication without enforcing protocol signing (HTTPS) or without enforcing Extended Protection for Authentication (EPA), it becomes vulnerable to NTLM relay attacks (ESC8). Relay attacks can lead to complete domain takeover if an attacker manages to pull it off successfully.

> [!NOTE]

>This assessment is available only to customers who have installed a sensor on an AD CS server. For more information, see [Configure sensors for AD FS, AD CS, and Microsoft Entra Connect](../deploy/active-directory-federation-services.md).

**Implementation**

Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> for insecure AD CS certificate enrollment IIS endpoints.

The assessment lists the problematic HTTP endpoints in your organization and guidance to configuring the endpoints securely.

Once handled, the ESC8 attack risk is mitigated, reducing your attack surface significantly.

## Edit misconfigured certificate templates owner (ESC4)

This article provides an overview of Microsoft Defender for Identity's **Misconfigured certificate templates owner (ESC4)** security posture assessment report.

**Description**

A certificate template is an Active Directory object with an owner, who controls access to the object and the ability to edit the object.

If the owner permissions grant a built-in, unprivileged group with permissions that allow for template setting changes, an adversary can introduce a template misconfiguration, escalate privileges, and compromise the entire domain.

Examples of built-in, unprivileged groups are *Authenticated users*, *Domain users*, or *Everyone*. Examples of permissions that allow for template setting changes are *Full control* or *Write DACL*.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> for a misconfigured certificate template owner.

1. Research why the template owner might be misconfigured.

1. Remediate the issue by changing the owner to a privileged and monitored user.

## Edit misconfigured Certificate Authority ACL (ESC7)

**Description**

Certificate Authorities (CAs) maintain access control lists (ACLs) that outline roles and permissions for the CA. If access control isn't configured correctly, any user might be allowed to interfere with the CA settings, circumventing security measures, and potentially compromise the entire domain.

The effect of a misconfigured ACL varies based on the type of permission applied. For example:

- If an unprivileged user holds the *Manage Certificates* right, they can approve pending certificate requests, bypassing the *Manager approval* requirement.

- With the *Manage CA* right, the user can modify CA settings, such as adding the *User specifies SAN* flag (`EDITF_ATTRIBUTESUBJECTALTNAME2`), creating an artificial misconfiguration that might later lead to a complete domain compromise.

### Prerequisites

This assessment is available only to customers who installed a sensor on an AD CS server.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> for misconfigured Certificate Authority ACLs. For example:

1. Research why the CA ACL is misconfigured.

1. Remediate the issues by removing all permissions that grant unprivileged built-in groups with *Manage CA* and/or *Manage certificates* permissions.

## Edit misconfigured certificate templates ACL (ESC4)

**Description**

Certificate templates are Active Directory objects with an ACL controlling the access to the object. Besides determining enrollment permissions, the ACL also determines permissions for editing the object itself.

If for any reason, there's an entry in the ACL that grants a built-in, unprivileged group with permissions that allow for template setting changes, an adversary can introduce a template misconfiguration, escalate privileges, and compromise the entire domain.

Examples of built-in, unprivileged groups are *Authenticated users*, *Domain users*, or *Everyone*. Examples of permissions that allow for template setting changes are *Full control* or *Write DACL*.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> for a misconfigured certificate template ACL. For example:

1. Research why the template ACL might be misconfigured.

1. Remediate the issue by removing any entry that grants unprivileged group permissions that allow tampering with the template.

1. Remove the certificate template from being published by any CA if they're not needed.

## Edit misconfigured enrollment agent certificate template (ESC3)

**Description**

Typically, users have an Enrollment Agent that enrolls their certificates for them. Under specific circumstances, Enrollment Agent certificates can enroll certificates for any eligible user, posing a risk to your organization.

When Microsoft Defender for Identity reports about Enrollment Agent certificate templates that endanger your organization, risky Enrollment Agent templates are listed on the **Exposed entities** pane.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> for misconfgured enrollment agent certificate templates.  For example:

1. Remediate the issues by performing at least one of the following steps:

- Remove the *Certificate request agent* EKU.

- Remove overly permissive enrollment permissions, which allow any user to enroll certificates based on that certificate template. Templates marked as vulnerable by Defender for Identity have at least one access list entry that allows enrollment for a built-in unprivileged group, making this exploitable by any user. Examples of built-in, unprivileged groups are *Authenticated Users* or *Everyone*.

- Turn on the CA certificate *Manager approval* requirement.

- Remove the certificate template from being published by any CA. Templates that aren't published can't be requested, and therefore can't be exploited.

- Use Enrollment Agent restrictions on the Certificate Authority level. For example, you might want to restrict which users are allowed to act as an Enrollment Agent, and which templates can be requested.

## Edit overly permissive certificate template with privileged EKU (Any purpose EKU or No EKU) (ESC2)

**Description**

Digital certificates play a vital role in establishing trust and preserving integrity throughout an organization. This is true not only in Kerberos domain authentication, but also in other areas, such as code integrity, server integrity, and technologies that rely on certificates like Active Directory Federation Services (AD FS) and IPSec.

When a certificate template has no EKUs or has an *Any Purpose* EKU, and it's enrollable for any unprivileged user, certificates issued based on that template can be used maliciously by an adversary, compromising trust.

Even though the certificate can’t be used for impersonating user authentication, it compromises other components that relieve digital certificates for their trust model. Adversaries can craft TLS certificates and impersonate any website.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> for overly permissive certificate templates with a privileged EKU.  For example:

1. Research why the templates have a privileged EKU.

1. Remediate the issue by doing the following:

- Restrict the template's overly permissive permissions.

- Enforce extra mitigations like adding *Manager approval* and signing requirements if possible.

## Prevent Certificate Enrollment with arbitrary Application Policies (ESC15)

**Description**

This recommendation directly addresses the recently published [CVE-2024-49019](https://msrc.microsoft.com/update-guide/advisory/CVE-2024-49019), which highlights security risks associated with vulnerable AD CS configurations. This security posture assessment lists all vulnerable certificate templates found in customer environments due to unpatched AD CS servers.

Certificate templates that are vulnerable to [CVE-2024-49019](https://msrc.microsoft.com/update-guide/en-US/advisory/CVE-2024-49019) allow an attacker to issue a certificate with arbitrary Application Policies and Subject Alternative Name. The certificate can be used to escalate privileges, possibly resulting with full domain compromise.

These certificate templates expose organizations to significant risks, as they enable attackers to issue certificates with arbitrary Application Policies and Subject Alternative Names (SANs). Such certificates can be exploited to escalate privileges and potentially compromise the entire domain. In particular, these vulnerabilities allow non-privileged users to issue certificates that can authenticate as high-privileged accounts, posing a severe security threat.

> [!NOTE]

> This assessment is available only to customers who installed a sensor on an AD CS server. For more information, see [New sensor type for Active Directory Certificate Services (AD CS)](/defender-for-identity/whats-new).

**Implementation**

1. Review the recommended action at [Prevent Certificate Enrollment with arbitrary Application Policies (ESC15)](https://security.microsoft.com/securescore?viewid=actions).

2. **Identify the vulnerable certificate templates:**

- Remove enrollment permission for unprivileged users.

- Disable the **“Supply in the request”** option.

3. Identify the AD CS servers which are vulnerable to CVE-2024-49019 and apply the relevant patch.

## Prevent users to request a certificate valid for arbitrary users based on the certificate template (ESC1)  (Preview)

**Description**

Each certificate is associated with an entity through its subject field. However, certificates also include a *Subject Alternative Name* (SAN) field, which allows the certificate to be valid for multiple entities.

The SAN field is commonly used for web services hosted on the same server, supporting the use of a single HTTPS certificate instead of separate certificates for each service. When the specific certificate is also valid for authentication, by containing an appropriate EKU, such as *Client Authentication*, it can be used to authenticate several different accounts.

If a certificate template has the *Supply in the request* option turned on, the template is vulnerable, and attackers might be able to enroll a certificate that's valid for arbitrary users.

> [!IMPORTANT]

> If the certificate is also permitted for authentication and there aren't any mitigation measures enforced, such as *Manager approval* or required authorized signatures, the certificate template is dangerous as it allows any unprivileged user to take over any arbitrary user, including a domain admin user.

>

> This specific setting is one of the most common misconfigurations.

>

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> for certificate requests for arbitrary users. For example:

1. To remediate certificate requests for arbitrary users, perform at least one of the following steps:

- Turn off *Supply in the request* configuration.

- Remove any EKUs that enable user authentication, such as *Client Authentication*, *Smartcard logon*, *PKINIT client authentication*, or *Any purpose*.

- Remove overly permissive enrollment permissions, which allow any user to enroll certificate based on that certificate template.

Certificate templates marked as vulnerable by Defender for Identity have at least one access list entry that supports enrollment for a built-in, unprivileged group, making this exploitable by any user. Examples of built-in, unprivileged groups include *Authenticated Users* or *Everyone*.

- Turn on the CA certificate *Manager approval* requirement.

- Remove the certificate template from being published by any CA. Templates that aren't published can't be requested, and therefore can't be exploited.

## Edit vulnerable Certificate Authority setting (ESC6)  (Preview)

**Description**

Each certificate is associated with an entity through its subject field. However, a certificate also includes a *Subject Alternative Name* (SAN) field, which allows the certificate to be valid for multiple entities.

The SAN field is commonly used for web services hosted on the same server, supporting the use of a single HTTPS certificate instead of separate certificates for each service. When the specific certificate is also valid for authentication, by containing an appropriate EKU, such as *Client Authentication*, it can be used to authenticate several different accounts.

Unprivileged users that can specify the users in the SAN settings can lead to immediate compromise, and post a great risk to your organization.

If the AD CS `editflags` > `EDITF_ATTRIBUTESUBJECTALTNAME2` flag is turned on, each user can specify the SAN settings for their certificate request. This, in turn affects all certificate templates, whether they have the `Supply in the request` option turned on or not.

If there's a template where the `EDITF_ATTRIBUTESUBJECTALTNAME2` setting is turned on, and the template is valid for authentication, an attacker can enroll a certificate that can impersonate any arbitrary account.

> [!NOTE]

> This assessment is available only to customers who installed a sensor on an AD CS server.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> for editing vulnerable Certificate Authority settings.  For example:

1. Research why the `EDITF_ATTRIBUTESUBJECTALTNAME2` setting is turned on.

1. Turn off the setting by running:

```cmd

certutil -setreg policy\EditFlags -EDITF_ATTRIBUTESUBJECTALTNAME2

```

1. Restart the service by running:

```cmd

net stop certsvc & net start certsvc

```

## Next steps

- [Learn more about Microsoft Secure Score](/microsoft-365/security/defender/microsoft-secure-score)


# Group Policy

# Group policy security assessments

## GPO can be modified by unprivileged accounts

**Description**

This recommendation lists any Group Policy Objects in your environment that can be modified by standard users which can potentially lead to the compromise of the domain.

Attackers may attempt to obtain information on Group Policy settings to uncover vulnerabilities that can be exploited to gain higher levels of access, understand the security measures in place within a domain, and identify patterns in domain objects. This information can be used to plan subsequent attacks, such as identifying potential paths to exploit within the target network or finding opportunities to blend in or manipulate the environment.

**User impact**

A user, service or application that relies on these permissions may stop functioning.

**Implementation**

Carefully review each assigned permission, identify any dangerous permission granted, and modify them to remove any unnecessary or excessive user rights.

## Next steps

[Learn more about Microsoft Secure Score](/microsoft-365/security/defender/microsoft-secure-score)


# Accounts

# Accounts security posture assessments

> [!NOTE]

> While assessments are updated in near real time, scores and statuses are updated every 24 hours. While the list of impacted entities is updated within a few minutes of your implementing the recommendations, the status might still take time until it's marked as **Completed**.

## Remove stale Active Directory accounts (Preview)

**Description**

This recommendation lists any user accounts in Active Directory that are stale, meaning they haven't logged in at all during the past 90 days.

Excluded accounts:

- Service accounts

- Disabled or deleted accounts.

**User impact**

Stale accounts pose a security risk because they provide potential targets for attackers without being actively monitored. Compromised stale accounts can be used to gain unauthorized access, move laterally in the environment, or escalate privileges. Removing or disabling them reduces unnecessary exposure and strengthens overall security posture.

**Implementation**

1. Review the exposed entities to identify which stale user accounts haven't logged in for the past 90 days.

1. Disable the account if it's confirmed to be unused or remove it entirely according to your retention policy.

1. Disable and delete user accounts with no logons for 90 days after a monitoring period.

1. Remove accounts for former employees to prevent unauthorized access.

##  Microsoft Entra ID privileged user accounts that are also privileged in Active Directory (Preview)

**Description**

This recommendation lists any user accounts that have privileged roles in Microsoft Entra ID (such as Global Administrator) and are also members of highly privileged Active Directory groups (for example, Domain Admins, Enterprise Admins). These dual-privileged accounts significantly increase the organization’s attack surface.

> [!NOTE]

> Guests, external identities, and accounts not synchronized to Microsoft Entra ID are excluded from this report. Only accounts that are enabled and hold privileges in both Entra ID and Active Directory are included.

**User impact**

Accounts with privileges in both Microsoft Entra ID and Active Directory can be leveraged by attackers to gain full control over both cloud and on-premises environments. Compromise of a single account might allow lateral movement, privilege escalation, and access to sensitive resources across hybrid environments. Dual-privileged accounts are high-value targets and can accelerate attacks if not properly managed.

**Implementation**

1. Review the list of exposed entities to identify which accounts have privileged access in both Microsoft Entra ID and Active Directory.

1. Remediate the account by reducing privileges in one or both environments to enforce least privilege. Only retain dual privileges if necessary, and document justification.

1. Consider separating cloud and on-premises roles across different accounts or implementing just-in-time access to reduce standing exposure.

1. Use Microsoft Entra Privileged Identity Management (PIM) to enforce approval workflows and limit standing access for accounts that must retain elevated privileges.

For example:

- A user who is a Global Administrator in Microsoft Entra ID and a Domain Admin in Active Directory should have one of the roles reduced or replaced with delegated administrative access.

- If dual privileges are required for critical operations, enable MFA, monitor logins closely, and review memberships regularly.

## Identify service accounts in privileged groups

**Description**

Lists Active Directory service accounts within your environment that are members of privileged groups, including direct and nested membership.

**User impact**

Service accounts often have long-lived credentials and are used by applications, scripts, or automated tasks. When these accounts are members of highly privileged groups (for example, Domain Admins or Enterprise Admins), they increase the organization’s attack surface. Compromise of one of these accounts can grant an attacker broad administrative access to critical systems and data. Additionally, because service accounts aren't tied to a specific user and often lack interactive monitoring, malicious activity performed under these accounts might go unnoticed, delaying detection and response.

**Implementation**

1. Review the exposed entities to identify Active Directory service accounts that are members of privileged groups, such as Domain Admins, Enterprise Admins, or Administrators.

1. Remove the account from the privileged group if elevated access isn't required, or disable the account if it's unused.

For example:

- **Unused or decommissioned service account:**

- Disable the account in Active Directory after confirming no recent logons or dependencies.

- Monitor for a short period (7–14 days). If inactive, delete it according to your policy.

- **Active service account without need for admin rights:**

- Remove it from the privileged group as exposed on the report.

- Grant only the minimal required access through delegated permissions or scoped security groups.

- **Replace legacy accounts:**

- Migrate service accounts to Group Managed Service Accounts (gMSA) for automatic password rotation and reduced credential exposure.

- **Accounts that must stay privileged**

- Restrict where they can log on using the **Log on to** property.

- Limit interactive logons via Group Policy and enable focused auditing for their activity.

- Require ownership, documentation, and periodic review of the privileged membership.

## Locate accounts in built-in Operator Groups

**Description**

Lists Active Directory accounts (users, service accounts, and groups) that are members of built-in operator groups such as Server Operators, Backup Operators, Print Operators or Account Operators, including direct and indirect membership. These groups grant elevated privileges that can be used to compromise domain controllers or sensitive servers.

**User impact**

Operator groups provide broad control over servers, files, and system operations. Members of these groups can perform administrative actions such as stopping critical services, modifying files, or restoring data, which can be exploited to escalate privileges or gain persistence. Because these groups are rarely needed in modern environments, leaving accounts in them unnecessarily increases the risk of privilege abuse or lateral movement.

**Implementation**

1. Review the list of exposed entities to identify which of your AD accounts are members of one of the built-in operator groups (for example, Server Operators, Backup Operators, Print Operators, and Account Operators).

1. Remove the account from the operator group if elevated access isn't required, or disable the account if it's unused.

For example:

- Remove the membership or disable service or admin account that were added to Backup Operators for a legacy backup process that no longer runs.

- If an account still performs operational tasks but doesn't require broad operator rights, delegate only the specific permissions it needs (for example, file restore or print management on a single server).

- If operator group membership is essential for a specific administrative function, monitor the account, restrict it to required hosts, and review it regularly  periodically to confirm ongoing necessity.

## Accounts with non-default Primary Group ID

**Description**

This recommendation lists all computers and users accounts whose primaryGroupId (PGID) attribute isn't the default for domain users and computers in Active Directory.

**User impact**

The primaryGroupId attribute of a user or computer account grants implicit membership to a group. Membership through this attribute doesn't appear in the list of group members in some interfaces. This attribute might be used as an attempt to hide group membership. It might be a stealthy way for an attacker to escalate privileges without triggering normal auditing for group membership changes.

**Implementation**

1. Review the list of exposed entities to discover which of your accounts have a suspicious primaryGroupId.

1. Take appropriate action on those accounts by resetting their attribute to their default values or adding the member to the relevant group:

- User accounts: 513 (Domain Users) or 514 (Domain Guests);

- Computer accounts: 515 (Domain Computers);

- Domain controller accounts: 516 (Domain Controllers);

- Read-only domain controller (RODC) accounts: 521 (Read-only Domain Controllers).

##  Remove access rights on suspicious accounts with the Admin SDHolder permission

**Description**

Having non-sensitive accounts with **Admin SDHolder** (security descriptor holder) permissions can have significant security implications, including:

- Leading to unauthorized privilege escalation, where attackers can exploit these accounts to gain administrative access and compromise sensitive systems or data

- Increasing the attack surface, making it harder to track and mitigate security incidents, potentially exposing the organization to greater risks.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> for **Remove access rights on suspicious accounts with the Admin SDHolder permission**.

For example:

1. Review the list of exposed entities to discover which of your nonsensitive accounts have the **Admin SDHolder** permission.

1. Take appropriate action on those entities by removing their privileged access rights. For example:

1. Use the **ADSI Edit** tool to connect to your domain controller.

1. Browse to the **CN=System**> **CN=AdminSDHolder** container and open the **CN=AdminSDHolder** container properties.

1. Select the **Security** tab > **Advanced**, and remove any nonsensitive entities. These are the entities marked as exposed in the security assessment.

For more information, see [Active Directory Service Interfaces](/windows/win32/adsi/active-directory-service-interfaces-adsi) and [ADSI Edit](/previous-versions/windows/it-pro/windows-server-2003/cc773354(v=ws.10)) documentation

To achieve the full score, remediate all exposed entities.

## Change password for krbtgt account

**Description**

This recommendation lists any krbtgt account within your environment with password last set over 180 days ago.

**User impact**

The krbtgt account in Active Directory is a built-in account used by the Kerberos authentication service. It encrypts and signs all Kerberos tickets, enabling secure authentication within the domain. The account can't be deleted, and securing it's crucial, as compromise could allow attackers to forge authentication tickets.

If the KRBTGT account's password is compromised, an attacker can use its hash to generate valid Kerberos authentication tickets, allowing them to perform Golden Ticket attacks and gain access to any resource in the AD domain. Since Kerberos relies on the KRBTGT password to sign all tickets, closely monitoring and regularly changing this password is essential to mitigating the risk of such attacks.

**Implementation**

1. Review the list of exposed entities to discover which of your krbtgt accounts have an old password.

1. Take appropriate action on those accounts by resetting their password **twice** to invalidate the Golden Ticket attack.

> [!NOTE]

> The **krbtgt** Kerberos account in all Active Directory domains supports key storage in all Kerberos Key Distribution Centers (KDCs). To renew the Kerberos keys for TGT encryption, periodically change the **krbtgt** account password.

>

> We recommend resetting the password twice, waiting at least 10 hours between resets. This process invalidates  existing Kerberos tickets to help prevent Golden Ticket attacks.

>

> For the official and supported procedure, see [Reset the krbtgt password](/windows-server/identity/ad-ds/manage/forest-recovery-guide/ad-forest-recovery-reset-the-krbtgt-password).

## Change password for on-premises account with potentially leaked credentials (Preview)

**Description**

This report lists users whose valid credentials have been leaked. When cybercriminals compromise valid passwords of legitimate users, the criminals often share those credentials. This is done by posting them publicly on the dark web or paste sites or by trading or selling the credentials on the black market. The Microsoft leaked credentials service acquires username/password pairs by monitoring public and dark web sites and by working with  Researchers Law enforcement Security teams at Microsoft Other trusted sources.

**User impact**

When the service acquires user credentials from the dark web, paste sites or the above sources an account with compromised credentials can be exploited by malicious actors to gain unauthorized access.

**Implementation**

1.	Review the recommended action at [https://security.microsoft.com/securescore?viewid=actions](https://security.microsoft.com/securescore?viewid=actions) for **Change password for accounts with potentially leaked credentials**.

1.	Review the list of exposed entities to discover which of your account passwords were leaked.

1.	Take appropriate actions on those entities by removing the service account:

1. Open the Active Directory Users and Computers (ADUC) console and sign in with an administrator account.

2. Navigate to the organizational unit (OU) where the user account is located.

3. Find and select the user account that needs a password change.

4. Right-click on the user account, select **Reset Password**, enter the new password, and confirm it.

## Change password of built-in domain Administrator account

**Description**

This recommendation lists any built-in domain Administrator accounts within your environment with password last set over 180 days ago.

**User impact**

The built-in domain Administrator account is a default, highly privileged AD account with full control over the domain. It can't be deleted, has unrestricted access, and is critical for managing the domain's resources.

Regularly updating the built-in Administrator account's password is essential due to its high privileges, which make it a prime target for attackers. If compromised, it can grant unauthorized control over the domain. Since this account is often unused and its password might not be updated frequently, regular changes reduce exposure and enhance security.

**Implementation**

1. Review the list of exposed entities to discover which of your built-in domain Administrator accounts have an old password.

1. Take appropriate action on those accounts by resetting their password.

For example:

## Dormant entities in sensitive groups

**Description**

Microsoft Defender for Identity discovers if particular users are **sensitive** along with providing attributes that surface if they're inactive, disabled, or expired.

However, **Sensitive** accounts can also become *dormant* if they aren't used for a period of 180 days. Dormant sensitive entities are targets of opportunity for malicious actors to gain sensitive access to your organization.

For more information, see [Defender for Identity entity tags in Microsoft Defender](../entity-tags.md#default-sensitive-entities).

**User impact**

Organizations that fail to secure their dormant user accounts leave the door unlocked to their sensitive data safe.

Malicious actors, much like thieves, often look for the easiest and quietest way into any environment. An easy and quiet path deep into your organization is through **sensitive** user and service accounts that are no longer in use.

It doesn't matter if the cause is employee turnover or resource mismanagement -skipping this step leaves your organization's most sensitive entities vulnerable and exposed.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> to discover which of your sensitive accounts are dormant.

1. Take appropriate action on those user accounts by removing their privileged access rights or by deleting the account.

## Remove non-admin accounts with DCSync permissions

**Description**

Accounts with the DCSync permission can initiate domain replication. Attackers can potentially exploit domain replication to gain unauthorized access, manipulate domain data, or compromise the integrity and availability of your Active Directory environment.

It's crucial to carefully manage and restrict the membership of this group to ensure the security and integrity of your domain replication process.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> for **Remove non-admin accounts with DCSync permissions**.

1. Review this list of exposed entities to discover which of your accounts have DCSync permissions and are also nondomain admins.

1. Take appropriate action on those entities by removing their privileged access rights.

To achieve the maximum score, remediate all exposed entities.

You can access Active Directory Users and Computers by signing in to your domain controller.

To remove DCSync permissions from a non-admin account:

1. Open Active Directory Users and Computers.

1. Turn on Advanced Features.

This is required to display the Security tab on domain objects.

1. Open Domain properties, select your domain name (for example, contoso.local), and then select Properties.

1. Select the Security tab.

1. Select the target user or group and then select the non-admin user or service account that shouldn't have these permissions.

1. Uncheck replication permissions. Scroll through the "Permissions for [User]" list uncheck the following permissions if they're selected:

- Replicating Directory Changes

- Replicating Directory Changes All

1. Select Apply, and then select OK.

## Ensure privileged accounts are not delegated

**Description**

This recommendation lists all privileged accounts that don't have the "not delegated" setting enabled, highlighting those potentially exposed to delegation-related risks. Privileged accounts are accounts that are being members of a privileged group such as Domain admins, Schema admins, and so on.

- Domain Admins

- Enterprise Admins

- Service accounts with elevated privileges

**User impact**

If the sensitive flag is disabled, attackers could exploit Kerberos delegation to misuse privileged account credentials, leading to unauthorized access, lateral movement, and potential network-wide security breaches.

Enabling the setting **This account is sensitive and can't be delegated** doesn't affect the account’s ability to log in or its assigned permissions. The restriction applies only to delegation scenarios, such as constrained or unconstrained Kerberos delegation.

Privileged accounts such as Domain Admins or Enterprise Admins shouldn't be delegated, as this poses a significant security risk. Enabling this setting helps prevent Kerberos delegation attacks by ensuring these accounts can't be impersonated.

**Security recommendation**

We recommend that you enable this setting for:

Domain Admins

Enterprise Admins

Service accounts with elevated privileges

Avoid applying this setting to accounts that require delegation for legitimate business purposes unless the delegation model is redesigned.

**Implementation**

1. Review the list of exposed entities to discover which of your privileged accounts don’t have the configuration flag "this account is sensitive and can't be delegated."

1. Take appropriate action on those accounts:

- User accounts:

- Go to the **Accounts** tab >**Account options**.

- Select **Account is sensitive and cannot be delegated.** This prevents users from gaining access to the account and manipulating system settings.

- Device accounts:

The safest approach is to use a PowerShell script to configure the device to prevent it from being used in any delegation scenario, ensuring that credentials on this machine can't be forwarded to access other services.

```powershell

$name = "ComputerA"

Get-ADComputer -Identity $name |

Set-ADAccountControl -AccountNotDelegated:$true

```

Another option is to set the `UserAccountControl` attribute to `NOT_DELEGATED = 0x100000` under the Attribute Editor tab for the exposed device.

For example:

## Entities exposing credentials in clear text

**Description**

This security assessment monitors your traffic for any entities exposing credentials in clear text and alerts you to the current exposure risks (most impacted entities) in your organization with suggested remediation.

**User impact**

Entities exposing credentials in clear text are risky not only for the exposed entity in question, but for your entire organization.

The increased risk is because unsecure traffic such as LDAP simple-bind is highly susceptible to interception by attacker-in-the-middle attacks. These types of attacks result in malicious activities including credential exposure, in which an attacker can leverage credentials for malicious purposes.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions>.

1. Research why those entities are using LDAP in clear text.

1. Remediate the issues and stop the exposure.

1. After confirming remediation, we recommend you require domain controller level LDAP signing. To learn more about LDAP server signing, see [Domain controller LDAP server signing requirements](/windows/security/threat-protection/security-policy-settings/domain-controller-ldap-server-signing-requirements).

> [!NOTE]

> This assessment is updated in near real time.

> The reports show the affected entities from the last 30 days. After that time, entities no longer affected will be removed from the exposed entities list.

## Microsoft LAPS usage

**Description**

Microsoft's "Local Administrator Password Solution" (LAPS) provides management of local administrator account passwords for domain-joined computers. Passwords are randomized and stored in Active Directory (AD), protected by ACLs, so only eligible users can read it or request its reset.

This security assessment supports [legacy Microsoft LAPS](https://www.microsoft.com/en-us/download/details.aspx?id=46899) and [Windows LAPS](/windows-server/identity/laps/laps-overview).

**User impact**

LAPS provides a solution to the issue of using a common local account with an identical password on every computer in a domain. LAPS resolves this issue by setting a different, rotated random password for the common local administrator account on every computer in the domain.

LAPS simplifies password management while helping customers implement more recommended defenses against cyberattacks. In particular, the solution mitigates the risk of lateral escalation that results when customers use the same administrative local account and password combination on their computers. LAPS stores the password for each computer's local administrator account in AD, secured in a confidential attribute in the computer's corresponding AD object. The computer can update its own password data in AD, and domain administrators can grant read access to authorized users or groups, such as workstation helpdesk administrators.

> [!NOTE]

> In some cases, [Microsoft Entra hybrid joined](/azure/active-directory/devices/concept-hybrid-join) machines might still appear in the security posture assessment even if LAPS is configured in Microsoft Entra ID. This can be due to how the policy is applied or how the device reports its state.

> If this occurs, we suggest reviewing the LAPS configuration in Microsoft Entra ID to confirm everything is set up as expected. You can find more details [here](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/windows-local-administrator-password-solution-with-microsoft-entra-id-now-genera/3911999).

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> to discover which of your domains have some (or all) compatible Windows devices that aren't protected by LAPS, or that haven't had their LAPS managed password changed in the last 60 days.

1. For domains that are partially protected, select the relevant row to view the list of devices not protected by LAPS in that domain.

1. Take appropriate action on those devices by downloading, installing, and configuring or troubleshooting [Microsoft LAPS](https://go.microsoft.com/fwlink/?linkid=2104282) or [Windows LAPS](/windows-server/identity/laps/laps-overview).

## Remove discoverable passwords in Active Directory account attributes (Preview)

**Description**

Certain free-text attributes are often overlooked during hardening but are readable by any authenticated user in the domain. When credentials or clues are mistakenly stored in these attributes, attackers can abuse them to move laterally across the environment or escalate privileges.

Attackers seek low-friction paths to expand access. Exposed passwords in these attributes represent an easy win because:

- The attributes aren't access-restricted.

- They aren't monitored by default.

- They provide context attackers can exploit for lateral movement and privilege escalation.

Removing exposed credentials from these attributes reduces the risk of identity compromise and strengthens your organization’s security posture.

> [!NOTE]

> Findings can include false positives. Always validate the results before taking action.

Microsoft Defender for Identity detects potential credential exposure in Active Directory by analyzing commonly used free-text attributes. This includes looking for common password formats, hints,  `'description'`, `'info'`, and `'adminComment'` fields, and other contextual clues that might suggest the presence of credential misuse.

This recommendation uses GenAI-powered analysis of Active directory attributes to detect:

- Plaintext passwords or variations. For example, '`Password=Summer2025!'`

- Credential patterns, reset hints, or sensitive account information.

- Other indicators suggesting operational misuse of directory fields.

Detected matches are surfaced in **Secure Score** and the **Security Assessment report** for review and remediation.

**Implementation**

To address this security assessment, follow these steps:

1. Review the recommended action at [https://security.microsoft.com/securescore?viewid=actions](https://security.microsoft.com/securescore?viewid=actions) for Remove discoverable passwords in Active Directory account attributes.

1. Review the exposed entries in the security report. Identify any field content that includes:

- Cleartext passwords

- Reset instructions or credential clues

- Sensitive business or system information

1. Remove sensitive information from the listed attribute fields using standard directory management tools (for example, PowerShell or ADSI Edit).

1. Fully remove the sensitive information. Don’t just mask the value. Partial obfuscation (for example, P@ssw***) can still offer useful clues to attackers.

## Remove Stale Service Accounts (Preview)

**Description**

This recommendation lists Active Directory service accounts detected as stale within the past 90 days.

**User impact**

Unused service accounts create significant security risks, as some of them can carry elevated privileges. If attackers gain access, the result can be substantial damage. Stale service accounts might retain high or legacy permissions. When compromised, they provide attackers with discreet entry points into critical systems, granting far more access than a standard user account.

This exposure creates several risks:

- Unauthorized access to sensitive applications and data.

- Lateral movement across the network without detection.

**Implementation**

To use this security assessment effectively, follow these steps:

1. Review the recommended action at [https://security.microsoft.com/securescore?viewid=actions ](https://security.microsoft.com/securescore?viewid=actions) for Remove stale service account.

1. Review the list of exposed entities to discover which of your service accounts are stale and haven't performed any login activity in the last 90 days.

1. Take appropriate actions on those entities by removing the service account. For example:

- **Disable the account:** Prevent any usage by disabling the account identified as exposed.

- **Monitor for impact:** Wait several weeks and monitor for operational issues, such as service disruptions or errors.

- **Delete the account:** If no issues are observed, delete the account and fully remove its access.

## Unsecure Kerberos delegation

**Description**

Kerberos delegation is a delegation setting that allows applications to request end-user access credentials to access resources on behalf of the originating user.

**User impact**

Unsecure Kerberos delegation gives an entity the ability to impersonate you to any other chosen service. For example, imagine you have an IIS website, and the application pool account is configured with unconstrained delegation. The IIS website site also has Windows Authentication enabled, allowing native Kerberos authentication, and the site uses a back-end SQL Server for business data. With your Domain Admin account, you browse to the IIS website and authenticate to it. The website, using unconstrained delegation can get a service ticket from a domain controller to the SQL service, and do so in your name.

The main issue with Kerberos delegation is that you need to trust the application to always do the right thing. Malicious actors can instead force the application to do the wrong thing. If you're logged on as **domain admin**, the site can create a ticket to whatever other services it wishes, acting as you, the **domain admin**. For example, the site could choose a domain controller, and make changes to the **enterprise admin** group. Similarly, the site could acquire the hash of the KRBTGT account, or download an interesting file from your Human Resources department. The risk is clear and the possibilities with unsecure delegation are nearly endless.

The following is a description of the risk posed by different delegation types:

- **Unconstrained delegation**: Any service can be abused if one of their delegation entries is sensitive.

- **Constrained delegation**: Constrained entities can be abused if one of their delegation entries is sensitive.

- **Resource-based constrained delegation (RBCD)**: Resource-based constrained entities can be abused if the entity itself is sensitive.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> to discover which of your non-domain controller entities are configured for **unsecure Kerberos delegation**.

1. Take appropriate action on those at-risk users, such as removing their unconstrained attribute or changing it to a more secure constrained delegation.

1. Use the remediation appropriate to your delegation type.

1. Disable delegation or use one of the following Kerberos constrained delegation (KCD) types:

**Unconstrained delegation**

1. Select **Trust this computer for delegation to specified services only**.

1. Specify the **Services to which this account can present delegated credentials**.

**Constrained delegation**

Restricts which services this account can impersonate.

1. Review the sensitive users listed in the recommendations and remove them from the services to which the affected account can present delegated credentials.

**Resource-based constrained delegation (RBCD)**

Resource-based constrained delegation restricts which entities can impersonate this account. Resource-based KCD is configured using PowerShell.

1. You can use the [Set-ADComputer](/powershell/module/activedirectory/set-adcomputer) or [Set-ADUser](/powershell/module/activedirectory/set-aduser) cmdlets, depending on whether the impersonating account is a computer account or a user account / service account.

1. Review the sensitive users listed in the recommendations and remove them from the resource. For more information about configuring RBCD, see [Configure Kerberos constrained delegation (KCD) in Microsoft Entra Domain Services](/azure/active-directory-domain-services/deploy-kcd).

## Unsecure SID History attributes

**Description**

SID History is an attribute that supports [migration scenarios](/previous-versions/windows/it-pro/windows-server-2003/cc779590(v=ws.10)). Every user account has an associated [Security Identifier (SID)](/windows/win32/secauthz/security-identifiers) which is used to track the security principal and the access the account has when connecting to resources. SID History enables access for another account to effectively be cloned to another and is useful to ensure users retain access when moved (migrated) from one domain to another.

The assessment checks for accounts with SID History attributes which Microsoft Defender for Identity profiles to be risky.

**User impact**

Organizations that fail to secure their account attributes leave the door unlocked for malicious actors.

Malicious actors, much like thieves, often look for the easiest and quietest way into any environment. Accounts configured with an unsecure SID History attribute are windows of opportunities for attackers and can expose risks.

For example, a nonsensitive account in a domain can contain the Enterprise Admin SID in its SID History from another domain in the Active Directory forest, thus "elevating" access for the user account to an effective Domain Admin in all domains in the forest. If you have a forest trust without SID Filtering enabled (also called Quarantine), it's possible to inject a SID from another forest and it will be added to the user token when authenticated and used for access evaluations.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> to discover which of your accounts have an unsecure SID History attribute.

1. Take appropriate action to remove SID History attribute from the accounts using PowerShell using the following steps:

1. Identify the SID in the SIDHistory attribute on the account.

```powershell

Get-ADUser -Identity <account> -Properties SidHistory | Select-Object -ExpandProperty SIDHistory

```

2. Remove the SIDHistory attribute using the SID identified earlier.

```powershell

Set-ADUser -Identity <account> -Remove @{SIDHistory='S-1-5-21-...'}

```

## Unsecure account attributes

**Description**

Microsoft Defender for Identity continuously monitors your environment to identify accounts with attribute values that expose a security risk, and reports on these accounts to assist you in protecting your environment.

**User impact**

Organizations that fail to secure their account attributes leave the door unlocked for malicious actors.

Malicious actors, much like thieves, often look for the easiest and quietest way into any environment. Accounts configured with unsecure attributes are windows of opportunity for attackers and can expose risks.

For example, if the **PasswordNotRequired** attribute is enabled, an attacker can easily access the account. This is especially risky if the account has privileged access to other resources.

**Implementation**

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> to discover which of your accounts have unsecure attributes.

1. Take appropriate action on those user accounts by modifying or removing the relevant attributes.

1. Use the remediation appropriate to the relevant attribute as described in the following table:

| Recommended action | Remediation | Reason |

| --- | --- | --- |

| Remove Don't require Kerberos preauthentication| Remove this setting from account properties in Active Directory (AD) | Removing this setting requires a Kerberos pre-authentication for the account resulting in improved security. |

| Remove Store password using reversible encryption | Remove this setting from account properties in AD | Removing this setting prevents easy decryption of the account's password. |

| Remove Password not required | Remove this setting from account properties in AD | Removing this setting requires a password to be used with the account and helps prevent unauthorized access to resources. |

| Remove Password stored with weak encryption | Reset the account password | Changing the account's password enables stronger encryption algorithms to be used for its protection. |

| Enable Kerberos AES encryption support | Enable AES features on the account properties in AD | Enabling AES128_CTS_HMAC_SHA1_96 or AES256_CTS_HMAC_SHA1_96 on the account helps prevent the use of weaker encryption ciphers for Kerberos authentication. |

| Remove Use Kerberos DES encryption types for this account | Remove this setting from account properties in AD | Removing this setting enables the use of stronger encryption algorithms for the account's password. |

| Remove a Service Principal Name (SPN) | Remove this setting from account properties in AD | When a user account is configured with an SPN set, it means that the account has been associated with one or more SPNs. This typically occurs when a service is installed or registered to run under a specific user account, and the SPN is created to uniquely identify the service workspace for Kerberos authentication. This recommendation only showed for sensitive accounts. |

|Reset password as SmartcardRequired setting was removed|Reset the account password|Changing the account's password after the SmartcardRequired UAC flag was removed ensures it was set under current security policies. This helps prevent potential exposure from passwords created when smartcard enforcement was still active.|

4. Use the **UserAccountControl** (UAC) flag to manipulate user account profiles. For more information, see:

- [Windows Server troubleshooting](/troubleshoot/windows-server/identity/useraccountcontrol-manipulate-account-properties) documentation.

- [User Properties - Account Section](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd861342(v=ws.11))

- [Introduction to Active Directory Administrative Center Enhancements (Level 100)](/windows-server/identity/ad-ds/get-started/adac/introduction-to-active-directory-administrative-center-enhancements--level-100-)

- [Active Directory Administration Center](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd871105(v=ws.11))

## Next steps

- [Learn more about Microsoft Secure Score](/microsoft-365/security/defender/microsoft-secure-score)

- [Check out the Defender for Identity forum!](https://aka.ms/MDIcommunity)


# Cloud Identities

# Security assessments for cloud identities

This article describes the various security assessments available in Microsoft Defender for Identity related to cloud identities, specifically Okta. Each assessment highlights potential security risks and provides recommendations for mitigating these risks.

## Prerequisites

To use these security assessments, you must first connect your Okta instance in the Microsoft Defender portal.

For setup instructions, see [Connect your Okta instance](/defender-for-identity/okta-integration#connect-okta-to-defender-for-identity).

## Assign multifactor authentication to Okta privileged user accounts

**Description**

This report lists any Okta privileged accounts that don't have any multifactor authentication (MFA) methods assigned.

All privileged accounts should have multifactor authentication (MFA) enabled to strengthen security. By ensuring that privileged accounts such as Super Admin or Org Admin roles are secured with MFA, organizations can significantly reduce the risk of unauthorized access from compromised credentials. This strategy helps prevent attackers from gaining elevated access, safeguarding sensitive resources and protecting critical administrative functions from abuse.

**Implementation**

1. Review the recommended action at [https://security.microsoft.com/securescore?viewid=actions](https://security.microsoft.com/securescore?viewid=actions) for the "Assign multifactor authentication for Okta privileged user accounts" security assessment.

1. Review the list of exposed entities to discover which of your Okta privileged user accounts don't have any MFA method assigned.

1. Assign and enforce a multifactor authentication (MFA) method to the privileged accounts.

## Change password for Okta privileged User accounts

**Description**

This recommendation lists any Okta privileged accounts that use outdated passwords that were last set over 180 days ago.

**Impact**

Privileged accounts with old passwords create a significant security risk, as older credentials are more likely to be exposed through data breaches or other attack vectors. Enforcing regular password updates for privileged accounts reduces the likelihood of unauthorized access and strengthens overall security. Applying stringent password policies to accounts with elevated privileges protects sensitive resources and lowers the risk of exploitation.

**Implementation**

1. Review the recommended action at [https://security.microsoft.com/securescore?viewid=actions](https://security.microsoft.com/securescore?viewid=actions) for the "Change password for Okta privileged User accounts" security assessment.

1. Review the list of exposed entities to discover which of your Okta privileged user accounts have an old password.

1. Take appropriate action on those accounts by resetting their password.

## High number of Okta accounts with privileged role assigned

This article describes the security risks associated with having a high number of Okta accounts with privileged roles assigned and provides recommendations for mitigating these risks.

**Description**

This report lists Okta accounts with administrator roles - excluding Super Administrator, where the number of accounts assigned to these roles is greater than 25.

**User impact**

A high number of users with privileged roles increases the risk of misuse or unauthorized access to critical systems. By reducing the number of users assigned to roles such as Super Admin or Org Admin, organizations can better limit access to sensitive resources and reduce the attack surface. Maintaining a smaller, set of privileged accounts ensures more effective governance and minimizes potential security vulnerabilities.

**Implementation**

1. Review the recommended action at [https://security.microsoft.com/securescore?viewid=actions](https://security.microsoft.com/securescore?viewid=actions) for the "High number of Okta accounts with privileged role assigned" security assessment.

1. Review the list of exposed entities to discover which of your Okta accounts have privileged roles assigned.

1. Reduce the number of users assigned to administrator roles (other than Super-Admin) to the minimum necessary to ensure better control and align with least privilege best practices.

## Highly privileged Okta API token

**Description**

Okta’s API tokens inherit the permissions of the user who creates them. If a user with sensitive permissions generates an API token, it carries those permissions. Any API token created by a Super Admin has the same level of access as the Super Admin account. This can expose sensitive data and functionality to unauthorized users. If the token is stolen, it can grant the attacker access equivalent to the original user.

**Implementation**

1. Review the recommended action at [https://security.microsoft.com/securescore?viewid=actions](https://security.microsoft.com/securescore?viewid=actions) for the "Highly privileged Okta API token" security assessment.

1. Review the list of exposed entities to discover which of your Okta API tokens are highly privileged.

1. If the API token is no longer required, delete it to eliminate unnecessary exposure.

## Limit the number of Okta Super Admin accounts

**Description**

This report lists Okta accounts with Super Administrator role, where the number of users assigned to this role is greater than 5.

**User impact**

A high number of users with privileged roles increases the risk of misuse or unauthorized access to critical systems. By reducing the number of users assigned to roles such as Super Admin or Org Admin, organizations can better limit access to sensitive resources and reduce the attack surface. Maintaining a smaller, set of privileged accounts ensures more effective governance and minimizes potential security vulnerabilities.

**Implementation**

1. Review the recommended action at [https://security.microsoft.com/securescore?viewid=actions](https://security.microsoft.com/securescore?viewid=actions) for the "Limit the number of Okta Super Admin accounts" security assessment.

1. Review the list of exposed entities to discover which of your Okta accounts have Super Admin role assigned.

1. Limit Super Administrator access to the minimum number of users necessary to maintain control over highest level of privileged access.

##  Remove dormant Okta privileged accounts

**Description**

This assessment describes the security risks associated with dormant Okta privileged accounts and provides recommendations for mitigating these risks.

**User impact**

Dormant privileged accounts represent a significant security risk, as they can become targets for unauthorized access or misuse without detection. Deactivating or removing unused privileged accounts ensures that only active, monitored users have access to critical administrative capabilities.

**Implementation**

1. Review the recommended action at [https://security.microsoft.com/securescore?viewid=actions](https://security.microsoft.com/securescore?viewid=actions) for the "Remove dormant Okta privileged accounts" security assessment.

1. Review the list of exposed entities to identify Okta privileged user accounts not used in the last 90 days. This inactivity indicates that the account might be a dormant account or no longer needed.

1. If the account is no longer required, deactivate or remove it to eliminate unnecessary exposure.


# Alerts Overview

﻿---

title: Security alerts

description: This article provides a list of the security alerts issued by Microsoft Defender for Identity.

ms.date: 05/08/2025

ms.topic: reference

ms.reviewer: rlitinsky

---

# Security alerts in Microsoft Defender for Identity

## What are Microsoft Defender for Identity security alerts?

Microsoft Defender for Identity security alerts provide information about the suspicious activities detected by Defender for Identity, and the actors and computers involved in each threat. Alert evidence lists contain direct links to the involved users and computers, to help make your investigations easy and direct.

> [!NOTE]

> Defender for Identity isn't designed to serve as an auditing or logging solution that captures every single operation or activity on the servers where the sensor is installed. It only captures the data required for its detection and recommendation mechanisms.

The Identity alerts page gives you cross-domain signal enrichment and automated identity response capabilities. The benefit of investigating alerts with [Microsoft Defender XDR](/microsoft-365/security/defender/microsoft-365-defender) is that Microsoft Defender for Identity alerts are correlated with information obtained from each of the other products in the suite. These enhanced alerts are consistent with the other Microsoft Defender XDR alert formats originating from [Microsoft Defender for Office 365](/microsoft-365/security/office-365-security) and [Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint).

Alerts originating from Defender for Identity trigger [Microsoft Defender XDR automated investigation and response (AIR)](/microsoft-365/security/defender/m365d-autoir) capabilities, including automatically remediating alerts and the mitigation of tools and processes that can contribute to the suspicious activity.

Microsoft Defender for Identity alerts currently appear in two different layouts in the Microsoft Defender portal. While the alert views may show different information, all alerts are based on detections from Defender for Identity sensors. The differences in layout and information shown are part of an ongoing transition to a unified alerting experience across Microsoft Defender products.

To learn more about how to understand the structure, and common components of all Defender for Identity security alerts, see [View and manage alerts](understanding-security-alerts.md).

For information about **True positive (TP)**, **Benign true positive (B-TP)**, and **False positive (FP)**, see [security alert classifications](understanding-security-alerts.md#classify-security-alerts).

## Alerts categories

The alerts are divided into categories based on the phases seen in a typical cyber-attack kill chain. The categories differ slightly depending on whether the alert originates from using the classic Microsoft Defender for Identity alerting, or Microsoft Defender for XDR. The differences are part of an ongoing transition to a unified alerting experience across Microsoft Defender products.

For example, there are categories for:

- Reconnaissance and discovery alerts

- Persistence and privilege escalation alerts

- Credential access alerts

- Lateral movement alerts

For detailed information about each alert see:

- [Microsoft Defender for Identity classic alerts](alerts-mdi-classic.md)

- [Microsoft Defender for Identity XDR alerts](alerts-xdr.md)

## See Also

- [View and manage security alerts](understanding-security-alerts.md)

- [Investigate security alerts](/defender-for-identity/investigate-security-alerts)

- [Check out the Defender for Identity forum!](<https://aka.ms/MDIcommunity>)


# Alerts Mdi Classic

﻿---

title: Microsoft Defender for Identity classic security alerts

description: This article provides a list of the classic security alerts issued by Microsoft Defender for Identity.

ms.date: 10/23/2025

ms.topic: reference

ms.reviewer: rlitinsky

---

# Microsoft Defender for Identity classic alerts

Microsoft Defender for Identity alerts can appear in the Microsoft Defender portal in two different formats depending on if the alert originates from Defender for Identity or Defender XDR. All alerts are based on detections from Defender for Identity sensors. The differences in layout and information are part of an ongoing transition to a unified alerting experience across Microsoft Defender products.

To learn more about how to understand the structure, and common components of all Defender for Identity security alerts, see [View and manage alerts](understanding-security-alerts.md).

## Microsoft Defender for Identity classic alert categories

Defender for Identity security alerts are divided into the following categories or phases, like the phases seen in a typical cyber-attack kill chain. Learn more about each phase, the alerts designed to detect each attack, and how to use the alerts to help protect your network using the following links:

- [Reconnaissance and discovery alerts](#reconnaissance-and-discovery-alerts)

- [Persistence and privilege escalation alerts](#persistence-and-privilege-escalation-alerts)

- [Credential access alerts](#credential-access-alerts)

- [Lateral movement alerts](#lateral-movement-alerts)

- [Other alerts](#other-alerts)

## Reconnaissance and discovery alerts

Reconnaissance and discovery consist of techniques an adversary may use to gain knowledge about the system and internal network. These techniques help adversaries observe the environment and orient themselves before deciding how to act. They also allow adversaries to explore what they can control and what's around their entry point to discover how it could benefit their current objective. Native operating system tools are often used toward this post-compromise information-gathering objective. In Microsoft Defender for Identity, these alerts usually involve internal account enumeration with different techniques.

The following security alerts help you identify and remediate **Reconnaissance and discovery** phase suspicious activities detected by Defender for Identity in your network.

|Security alert name |Severity |External ID |

|---------------|---------|------------|

|<a name="account-enumeration-reconnaissance-ldap"></a><details><summary>Account Enumeration reconnaissance (LDAP) </summary><br>**Description**:<br>In account enumeration reconnaissance, an attacker uses a dictionary with thousands of user names, or tools such as Ldapnomnom in an attempt to guess user names in the domain.<br><br>**LDAP**: Attacker makes LDAP Ping requests (cLDAP) using these names to try to find a valid username in the domain. If a guess successfully determines a username, the attacker may receive a response indicating that the user exists in the domain.<br>In this alert detection, Defender for Identity detects where the account enumeration attack came from, the total number of guess attempts, and how many attempts were matched. If there are too many unknown users, Defender for Identity detects it as a suspicious activity. The alert is based on LDAP search activities from sensors running on domain controller servers. <br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Discovery (TA0007)](https://attack.mitre.org/tactics/TA0007/)<br> - **MITRE attack technique**: [Account Discovery (T1087)](https://attack.mitre.org/techniques/T1087/)<br> - **MITRE attack sub-technique**: [Domain Account (T1087.002)](https://attack.mitre.org/techniques/T1087/002/)<br></details>|Medium|2437|

|<a name="network-mapping-reconnaissance-dns"></a><details><summary>Network-mapping reconnaissance (DNS)</summary><br>**Previous name**: Reconnaissance using DNS.<br><br>**Description**:<br>Your DNS server contains a map of all the computers, IP addresses, and services in your network. This information is used by attackers to map your network structure and target interesting computers for later steps in their attack.<br>There are several query types in the DNS protocol. This Defender for Identity security alert detects suspicious requests, either requests using an AXFR (transfer) originating from non-DNS servers, or those using an excessive number of requests.<br><br>**Learning period**: Eight days from the start of domain controller monitoring.<br><br>**MITRE**:<br> -  **Primary MITRE tactic**: [Discovery (TA0007)](https://attack.mitre.org/tactics/TA0007) <br> -  **MITRE attack technique**:  [Account Discovery (T1087)](https://attack.mitre.org/techniques/T1087/), [Network Service Scanning (T1046)](https://attack.mitre.org/techniques/T1046/), [Remote System Discovery (T1018)](https://attack.mitre.org/techniques/T1018/)<br> -  **MITRE attack sub-technique**:  N/A <br><br>**Suggested steps for prevention**:<br>To prevent future attacks using AXFR queries, it's important to secure your internal DNS server.<br> - Secure your internal DNS server to prevent reconnaissance using DNS by disabling zone transfers or by [restricting zone transfers](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)) only to specified IP addresses. Modifying zone transfers is one task among a checklist that should be addressed for [securing your DNS servers from both internal and external attacks](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)).</details>|Medium|2007|

|<a name="user-and-group-membership-reconnaissance-samr"></a><details><summary>User and Group membership reconnaissance (SAMR)</summary><br>**Previous name**: Reconnaissance using directory services queries.<br><br>**Description**:<br>User and group membership reconnaissance are used by attackers to map the directory structure and target privileged accounts for later steps in their attack. The Security Account Manager Remote (SAM-R) protocol is one of the methods used to query the directory to perform this type of mapping.<br>In this detection, no alerts are triggered in the first month after Defender for Identity is deployed (learning period). During the learning period, Defender for Identity profiles which SAM-R queries are made from which computers, both enumeration and individual queries of sensitive accounts.<br><br>**Learning period**: Four weeks per domain controller starting from the first network activity of SAMR against the specific DC.<br><br>**MITRE**:<br> -  **Primary MITRE tactic**: [Discovery (TA0007)](https://attack.mitre.org/tactics/TA0007) <br> -  **MITRE attack technique**: [Account Discovery (T1087)](https://attack.mitre.org/techniques/T1087/), [Permission Groups Discovery (T1069)](https://attack.mitre.org/techniques/T1069/)    <br> -  **MITRE attack sub-technique**:  [Domain Account (T1087.002)](https://attack.mitre.org/techniques/T1087/002/), [Domain Group (T1069.002)](https://attack.mitre.org/techniques/T1069/002/)    <br><br>**Suggested steps for prevention**:<br> - Apply Network access and restrict clients allowed to make remote calls to SAM group policy.</details>|Medium|2021|

|<a name="honeytoken-was-queried-via-ldap"></a><details><summary>Honeytoken was queried via LDAP </summary><br>**Description**:<br>User reconnaissance is used by attackers to map the directory structure and target privileged accounts for later steps in their attack. Lightweight Directory Access Protocol (LDAP) is one of the most popular methods used for both legitimate and malicious purposes to query Active Directory.<br>In this detection, Microsoft Defender for Identity will trigger this alert for any reconnaissance activities against a pre-configured [honeytoken user](entity-tags.md).<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Discovery (TA0007)](https://attack.mitre.org/tactics/TA0007)<br> - **MITRE attack technique**: [Account Discovery (T1087)](https://attack.mitre.org/techniques/T1087/), [Permission Groups Discovery (T1069)](https://attack.mitre.org/techniques/T1069/)<br> - **MITRE attack sub-technique**: [Domain Account (T1087.002)](https://attack.mitre.org/techniques/T1087/002/), [Domain Group (T1069.002)](https://attack.mitre.org/techniques/T1069/002/)</details>|Low|2429|

## Persistence and privilege escalation alerts

After the attacker uses techniques to keep access to different on-premises resources they start the Privilege Escalation phase, which consists of techniques that adversaries use to gain higher-level permissions on a system or network. Adversaries can often enter and explore a network with unprivileged access but require elevated permissions to follow through on their objectives. Common approaches are to take advantage of system weaknesses, misconfigurations, and vulnerabilities.

The following security alerts help you identify and remediate **Persistence and privilege escalation** phase suspicious activities detected by Defender for Identity in your network.

|Security alert name |Severity |External ID |

|---------------|---------|------------|

|<a name="suspected-golden-ticket-usage-encryption-downgrade"></a><details><summary>Suspected Golden Ticket usage (encryption downgrade)</summary><br>**Previous name**: Encryption downgrade activity.<br><br>**Description**:<br>Encryption downgrade is a method of weakening Kerberos by downgrading the encryption level of different protocol fields that normally have the highest level of encryption. A weakened encrypted field can be an easier target to offline brute force attempts. Various attack methods utilize weak Kerberos encryption cyphers. In this detection, Defender for Identity learns the Kerberos encryption types used by computers and users, and alerts you when a weaker cypher is used that is unusual for the source computer and/or user and matches known attack techniques.<br>In a Golden Ticket alert, the encryption method of the TGT field of TGS_REQ (service request) message from the source computer was detected as downgraded compared to the previously learned behavior. This isn't based on a time anomaly (as in the other Golden Ticket detection). In addition, in the case of this alert, there was no Kerberos authentication request associated with the previous service request, detected by Defender for Identity.<br><br>**Learning period**: This alert has a learning period of five days from the start of domain controller monitoring.<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003)<br> - **Secondary MITRE tactic**: [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004), [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **MITRE attack technique**: [Steal or Forge Kerberos Tickets (T1558)](https://attack.mitre.org/techniques/T1558/)<br> - **MITRE attack sub-technique**: [Golden Ticket(T1558.001)](https://attack.mitre.org/techniques/T1558/001/)<br><br>**Suggested steps for prevention**:<br> - Make sure all domain controllers with operating systems up to Windows Server 2012 R2 are installed with [KB3011780](https://www.microsoft.com/download/details.aspx?id=44978) and all member servers and domain controllers up to 2012 R2 are up-to-date with [KB2496930](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privileg). For more information, see [Silver PAC](/security-updates/SecurityBulletins/2011/ms11-013) and [Forged PAC](/security-updates/SecurityBulletins/2014/ms14-068).</details>|Medium|2009|

|<a name="suspected-golden-ticket-usage-nonexistent-account"></a><details><summary>Suspected Golden Ticket usage (nonexistent account)</summary><br>**Previous name**: Kerberos golden ticket.<br><br>**Description**:<br>Attackers with domain admin rights can compromise the KRBTGT account. Using the KRBTGT account, they can create a Kerberos ticket granting ticket (TGT) that provides authorization to any resource and set the ticket expiration to any arbitrary time. This fake TGT is called a "Golden Ticket" and allows attackers to achieve network persistence. In this detection, an alert is triggered by a nonexistent account.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003)<br> - **Secondary MITRE tactic**: [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004), [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **MITRE attack technique**: - [Steal or Forge Kerberos Tickets (T1558)](https://attack.mitre.org/techniques/T1558/), [Exploitation for Privilege Escalation (T1068)](https://attack.mitre.org/techniques/T1068/), [Exploitation of Remote Services (T1210)](https://attack.mitre.org/techniques/T1210/)<br> - **MITRE attack sub-technique**: [Golden Ticket(T1558.001)](https://attack.mitre.org/techniques/T1558/001/)</details>|High|2027|

|<a name="suspected-golden-ticket-usage-ticket-anomaly"></a><details><summary>Suspected Golden Ticket usage (ticket anomaly) </summary><br>**Description**:<br>Attackers with domain admin rights can compromise the KRBTGT account. Using the KRBTGT account, they can create a Kerberos ticket granting ticket (TGT) that provides authorization to any resource and set the ticket expiration to any arbitrary time. This fake TGT is called a "Golden Ticket" and allows attackers to achieve network persistence. Forged Golden Tickets of this type have unique characteristics this detection is designed to identify.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003)<br> - **Secondary MITRE tactic**: [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004), [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **MITRE attack technique**: [Steal or Forge Kerberos Tickets (T1558)](https://attack.mitre.org/techniques/T1558/)<br> - **MITRE attack sub-technique**: [Golden Ticket(T1558.001)](https://attack.mitre.org/techniques/T1558/001/)</details>|High|2032|

|<a name="suspected-golden-ticket-usage-ticket-anomaly-using-rbcd"></a><details><summary>Suspected Golden Ticket usage (ticket anomaly using RBCD) </summary><br>**Description**:<br>Attackers with domain admin rights can compromise the KRBTGT account. Using the KRBTGT account, they can create a Kerberos ticket granting ticket (TGT) that provides authorization to any resource. This fake TGT is called a "Golden Ticket" and allows attackers to achieve network persistence. In this detection, the alert is triggered by a golden ticket that was created by setting Resource Based Constrained Delegation (RBCD) permissions using the KRBTGT account for account (user\computer) with SPN.<br><br>**Learning period**: None<br><br>**MITRE** <br> - **Primary MITRE tactic**: [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003) <br> - **Secondary MITRE tactic**: [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004)<br> - **MITRE attack technique**: [Steal or Forge Kerberos Tickets (T1558)](https://attack.mitre.org/techniques/T1558/)<br> - **MITRE attack sub-technique**: [Golden Ticket(T1558.001)](https://attack.mitre.org/techniques/T1558/001/)</details>|High|2040|

|<a name="suspected-golden-ticket-usage-time-anomaly"></a><details><summary>Suspected Golden Ticket usage (time anomaly)</summary><br>**Previous name**: Kerberos golden ticket.<br><br>**Description**:<br>Attackers with domain admin rights can compromise the KRBTGT account. Using the KRBTGT account, they can create a Kerberos ticket granting ticket (TGT) that provides authorization to any resource and set the ticket expiration to any arbitrary time. This fake TGT is called a "Golden Ticket" and allows attackers to achieve network persistence. This alert is triggered when a Kerberos ticket granting ticket is used for more than the allowed time permitted, as specified in the Maximum lifetime for user ticket.<br><br>**Learning period**: None<br><br>**MITRE** <br> - **Primary MITRE tactic**: [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003) <br> - **Secondary MITRE tactic**: [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004), [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **MITRE attack technique**: [Steal or Forge Kerberos Tickets (T1558)](https://attack.mitre.org/techniques/T1558/)<br> - **MITRE attack sub-technique**: [Golden Ticket(T1558.001)](https://attack.mitre.org/techniques/T1558/001/)</details>|High|2022|

|<a name="suspected-skeleton-key-attack-encryption-downgrade"></a><details><summary>Suspected skeleton key attack (encryption downgrade)</summary><br>**Previous name**: Encryption downgrade activity.<br><br>**Description**:<br>Encryption downgrade is a method of weakening Kerberos using a downgraded encryption level for different fields of the protocol that normally have the highest level of encryption. A weakened encrypted field can be an easier target to offline brute force attempts. Various attack methods utilize weak Kerberos encryption cyphers. In this detection, Defender for Identity learns the Kerberos encryption types used by computers and users. The alert is issued when a weaker cypher is used that is unusual for the source computer, and/or user, and matches known attack techniques.<br>Skeleton Key is malware that runs on domain controllers and allows authentication to the domain with any account without knowing its password. This malware often uses weaker encryption algorithms to hash the user's passwords on the domain controller. In this alert, the learned behavior of previous KRB_ERR message encryption from domain controller to the account requesting a ticket, was downgraded.<br><br>**Learning period**: None<br><br>**MITRE** <br> - **Primary MITRE tactic**: [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003) <br> - **Secondary MITRE tactic**: [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **MITRE attack technique**:  [Exploitation of Remote Services (T1210)](https://attack.mitre.org/techniques/T1210/),[Modify Authentication Process (T1556)](https://attack.mitre.org/techniques/T1556/)<br> - **MITRE attack sub-technique**: [Domain Controller Authentication (T1556.001)](https://attack.mitre.org/techniques/T1556/001/)</details>|Medium|2010|

|<a name="suspicious-additions-to-sensitive-groups"></a><details><summary>Suspicious additions to sensitive groups </summary><br>**Description**:<br>Attackers add users to highly privileged groups. Adding users is done to gain access to more resources, and gain persistency. This detection relies on profiling the group modification activities of users, and alerting when an abnormal addition to a sensitive group is seen. Defender for Identity profiles continuously.<br>For a definition of sensitive groups in Defender for Identity, see [Working with sensitive accounts](/defender-for-identity/entity-tags).<br>The detection relies on events audited on domain controllers. Make sure your domain controllers are [auditing the events needed](configure-windows-event-collection.md).<br><br>**Learning period**: Four weeks per domain controller, starting from the first event.<br><br>**MITRE**:<br> - Primary MITRE tactic: [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003) <br> - **Secondary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006)<br> - **MITRE attack technique**: [Account Manipulation (T1098)](https://attack.mitre.org/techniques/T1098/),[Domain Policy Modification (T1484)](https://attack.mitre.org/techniques/T1484/)<br> - **MITRE attack sub-technique**: N/A<br><br>**Suggested steps for prevention**:<br> - To help prevent future attacks, minimize the number of users authorized to modify sensitive groups.<br> - Set up Privileged Access Management for Active Directory if applicable.</details>|Medium|2024|

|<a name="suspected-netlogon-privilege-elevation-attempt-cve-2020-1472-exploitation"></a><details><summary>Suspected Netlogon privilege elevation attempt (CVE-2020-1472 exploitation) </summary><br>**Description**:<br>Microsoft published [CVE-2020-1472](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2020-1472) announcing that a new vulnerability exists that allows the elevation of privileges to the domain controller.<br>An elevation of privilege vulnerability exists when an attacker establishes a vulnerable Netlogon secure channel connection to a domain controller, using the Netlogon Remote Protocol ([MS-NRPC](/openspecs/windows_protocols/ms-nrpc/ff8f970f-3e37-40f7-bd4b-af7336e4792f)), also known as *Netlogon Elevation of Privilege Vulnerability*.<br><br>**Learning period**: None<br><br>**MITRE** <br> - **Primary MITRE tactic**: [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004) <br> - **MITRE attack technique**: N/A<br> - **MITRE attack sub-technique**: N/A<br><br>**Suggested steps for prevention**:<br> - Review [our guidance](https://support.microsoft.com/help/4557222/how-to-manage-the-changes-in-netlogon-secure-channel-connections-assoc) on managing changes in Netlogon secure channel connection which relate to and can prevent this vulnerability.</details>|High|2411|

|<a name="honeytoken-user-attributes-modified"></a><details><summary>Honeytoken user attributes modified </summary><br>**Description**:<br>Every user object in Active Directory has attributes that contain information such as first name, middle name, last name, phone number, address, and more. Sometimes attackers try to manipulate these objects for their benefit, for example by changing the phone number of an account to get access to any multifactor authentication attempt. Microsoft Defender for Identity triggers this alert for any attribute modification against a preconfigured [honeytoken user](entity-tags.md).<br><br>**Learning period**: None<br><br>**MITRE** <br> - **Primary MITRE tactic**: [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003) <br> - **MITRE attack technique**: [Account Manipulation (T1098)](https://attack.mitre.org/techniques/T1098/)<br> - **MITRE attack sub-technique**: N/A</details>|High|2427|

|<a name="honeytoken-group-membership-changed"></a><details><summary>Honeytoken group membership changed </summary><br>**Description**:<br>In Active Directory, each user is a member of one or more groups. After gaining access to an account, attackers might attempt to add or remove permissions from it to other users, by removing or adding them to security groups. Microsoft Defender for Identity triggers an alert whenever there's a change made to a preconfigured [honeytoken user account](entity-tags.md).<br><br>**Learning period**: None<br><br>**MITRE** <br> - **Primary MITRE tactic**: [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003) <br> - **MITRE attack technique**: [Account Manipulation (T1098)](https://attack.mitre.org/techniques/T1098/)<br> - **MITRE attack sub-technique**: N/A</details>|High|2428|

|<a name="suspected-sid-history-injection"></a><details><summary>Suspected SID-History injection </summary><br>**Description**:<br>SIDHistory is an attribute in Active Directory that allows users to retain their permissions and access to resources when their account is migrated from one domain to another. When a user account is migrated to a new domain, the user's SID is added to the SIDHistory attribute of their account in the new domain. This attribute contains a list of SIDs from the user's previous domain.<br>Adversaries may use the SIH history injection to escalate privileges and bypass access controls. This detection triggers when newly added SID was added to the SIDHistory attribute.<br><br>**Learning period**: None<br><br>**MITRE** <br> - **Primary MITRE tactic**: [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004) <br> - **MITRE attack technique**: [Account Manipulation (T1134)](https://attack.mitre.org/techniques/T1134/)<br> - **MITRE attack sub-technique**: [SID-History Injection(T1134.005)](https://attack.mitre.org/techniques/T1134/005/)</details>|High|1106|

|<a name="suspicious-modification-of-a-dnshostname-attribute-cve-2022-26923"></a><details><summary>Suspicious modification of a dNSHostName attribute (CVE-2022-26923) </summary><br>**Description**:<br>This attack involves the unauthorized modification of the dNSHostName attribute, potentially exploiting a known vulnerability (CVE-2022-26923). Attackers might manipulate this attribute to compromise the integrity of the Domain Name System (DNS) resolution process, leading to various security risks, including man-in-the-middle attacks or unauthorized access to network resources. <br>**Learning period**: None<br><br>**MITRE** <br> - **Primary MITRE tactic**: [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004) <br> - **Secondary MITRE tactic**: [Defense Evasion (TA0005)](https://attack.mitre.org/tactics/TA0005)<br> - **MITRE attack technique**: [Exploitation for Privilege Escalation (T1068)](https://attack.mitre.org/techniques/T1068/),[Access Token Manipulation (T1134)](https://attack.mitre.org/techniques/T1134/)<br> - **MITRE attack sub-technique**: [Token Impersonation/Theft (T1134.001)](https://attack.mitre.org/techniques/T1134/001/)</details>|High|2421|

|<a name="suspicious-modification-of-domain-adminsdholder"></a><details><summary>Suspicious modification of domain AdminSdHolder </summary><br>**Description**:<br>Attackers might target the Domain AdminSdHolder, making unauthorized modifications. This can lead to security vulnerabilities by altering the security descriptors of privileged accounts. Regular monitoring and securing of critical Active Directory objects are essential to prevent unauthorized changes.<br><br>**Learning period**: None<br><br>**MITRE** <br> - **Primary MITRE tactic**: [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003 ) <br> - **Secondary MITRE tactic**: [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004)<br> - **MITRE attack technique**:  [Account Manipulation (T1098)](https://attack.mitre.org/techniques/T1098/)<br> - **MITRE attack sub-technique**: N/A </details>|High|2430|

|<a name="suspicious-kerberos-delegation-attempt-by-a-newly-created-computer"></a><details><summary>Suspicious Kerberos delegation attempt by a newly created computer </summary><br>**Description**:<br>This attack involves a suspicious Kerberos ticket request by a newly created computer. Unauthorized Kerberos ticket requests can indicate potential security threats. Monitoring abnormal ticket requests, validating computer accounts, and promptly addressing suspicious activity are essential for preventing unauthorized access and potential compromise. <br>**Learning period**: None<br><br>**MITRE** <br> - **Primary MITRE tactic**: [Defense Evasion (TA0005)](https://attack.mitre.org/tactics/TA0005 ) <br> - **Secondary MITRE tactic**: [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004)<br> - **MITRE attack technique**:  [Domain Policy Modification (T1484)](https://attack.mitre.org/techniques/T1484/)<br> - **MITRE attack sub-technique**: N/A</details>|High|2422|

|<a name="suspicious-domain-controller-certificate-request-esc8"></a><details><summary>Suspicious Domain Controller certificate request (ESC8) </summary><br>**Description**:<br>An abnormal request for a Domain Controller certificate (ESC8) raises concerns about potential security threats. This could be an attempt to compromise the integrity of the certificate infrastructure, leading to unauthorized access and data breaches. <br>**Learning period**: None<br><br>**MITRE** <br> - **Primary MITRE tactic**: [Defense Evasion (TA0005)](https://attack.mitre.org/tactics/TA0005 ) <br> - **Secondary MITRE tactic**: [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003),[Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004/),[Initial Access (TA0001)](https://attack.mitre.org/tactics/TA0001/)<br> - **MITRE attack technique**:  [Valid Accounts (T1078)](https://attack.mitre.org/techniques/T1078/)<br> - **MITRE attack sub-technique**: N/A <br> **NOTE**: Suspicious Domain Controller certificate request (ESC8) alerts are only supported by Defender for Identity sensors on AD CS.</details>|High|2432|

|<a name="suspicious-modifications-to-the-ad-cs-security-permissionssettings"></a><details><summary>Suspicious modifications to the AD CS security permissions/settings </summary><br>**Description**:<br>Attackers may target the security permissions and settings of the Active Directory Certificate Services (AD CS) to manipulate the issuance and management of certificates. Unauthorized modifications can introduce vulnerabilities, compromise certificate integrity, and impact the overall security of the PKI infrastructure. <br>**Learning period**: None<br><br>**MITRE** <br> - **Primary MITRE tactic**: [Defense Evasion (TA0005)](https://attack.mitre.org/tactics/TA0005 ) <br> - **Secondary MITRE tactic**: [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004/) <br> - **MITRE attack technique**:  [Domain Policy Modification (T1484)](https://attack.mitre.org/techniques/T1484/) <br> - **MITRE attack sub-technique**: N/A <br> **Note**: Suspicious modifications to the AD CS security permissions/settings alerts are only supported by Defender for Identity sensors on AD CS.</details>|Medium|2435|

|<a name="suspicious-modification-of-the-trust-relationship-of-ad-fs-server"></a><details><summary>Suspicious modification of the trust relationship of AD FS server </summary><br>**Description**:<br>Unauthorized changes to the trust relationship of AD FS servers can compromise the security of federated identity systems. Monitoring and securing trust configurations are critical for preventing unauthorized access.<br><br>**Learning period**: None<br><br>**MITRE** <br> - **Primary MITRE tactic**: [Defense Evasion (TA0005)](https://attack.mitre.org/tactics/TA0005 ) <br> - **Secondary MITRE tactic**: [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004/) <br> - **MITRE attack technique**:  [Domain Policy Modification (T1484)](https://attack.mitre.org/techniques/T1484/)<br> - **MITRE attack sub-technique**: [Domain Trust Modification (T1484.002)](https://attack.mitre.org/techniques/T1562/002/)<br> **Note**: Suspicious modifications of the trust relationship of AD FS server alerts are only supported by Defender for Identity sensors on AD FS.</details>|Medium|2420|

|<a name="suspicious-modification-of-the-resource-based-constrained-delegation-attribute-by-a-machine-account"></a><details><summary>Suspicious modification of the Resource Based Constrained Delegation attribute by a machine account </summary><br>**Description**:<br>Unauthorized changes to the Resource-Based Constrained Delegation attribute by a machine account can lead to security breaches, allowing attackers to impersonate users and access resources. Monitoring and securing delegation configurations are essential for preventing misuse. <br>**Learning period**: None<br><br>**MITRE** <br> - **Primary MITRE tactic**: [Defense Evasion (TA0005)](https://attack.mitre.org/tactics/TA0005 ) <br> - **Secondary MITRE tactic**: [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004/) <br> - **MITRE attack technique**:  [Domain Policy Modification (T1484)](https://attack.mitre.org/techniques/T1484/)<br> - **MITRE attack sub-technique**: N/A</details>|High|2423|

## Credential access alerts

Credential Access consists of techniques for stealing credentials like account names and passwords. Techniques used to get credentials include keylogging or credential dumping. Using legitimate credentials can give adversaries access to systems, make them harder to detect, and provide the opportunity to create more accounts to help achieve their goals.

The following security alerts help you identify and remediate **Credential access** phase suspicious activities detected by Defender for Identity in your network.

|Security alert name |Severity |External ID|

|---------|---------|---------|

|<a name="suspected-golden-ticket-usage-forged-authorization-data"></a><details><summary>Suspected Golden Ticket usage (forged authorization data)</summary><br>**Previous name**: Privilege escalation using forged authorization data.<br><br>**Description**:<br>Known vulnerabilities in older versions of Windows Server allow attackers to manipulate the Privileged Attribute Certificate (PAC), a field in the Kerberos ticket that contains a user authorization data (in Active Directory this is group membership), granting attackers additional privileges.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006) <br> - **MITRE attack technique**: [Steal or Forge Kerberos Tickets (T1558)](https://attack.mitre.org/techniques/T1558/)<br> - **MITRE attack sub-technique**: [Golden Ticket (T1558.001)](https://attack.mitre.org/techniques/T1558/001/)  <br><br>**Suggested steps for prevention**:<br> - Make sure all domain controllers with operating systems up to Windows Server 2012 R2 are installed with [KB3011780](https://www.microsoft.com/download/details.aspx?id=44978) and all member servers and domain controllers up to 2012 R2 are up-to-date with [KB2496930](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privileg). For more information, see [Silver PAC](/security-updates/SecurityBulletins/2011/ms11-013) and [Forged PAC](/security-updates/SecurityBulletins/2014/ms14-068).</details>|High|2013|

|<a name="malicious-request-of-data-protection-api-master-key"></a><details><summary>Malicious request of Data Protection API master key</summary><br>**Previous name**: Malicious Data Protection Private Information Request.<br><br>**Description**:<br>The Data Protection API (DPAPI) is used by Windows to securely protect passwords saved by browsers, encrypted files, and other sensitive data. Domain controllers hold a backup master key that can be used to decrypt all secrets encrypted with DPAPI on domain-joined Windows machines. Attackers can use the master key to decrypt any secrets protected by DPAPI on all domain-joined machines.<br>In this detection, a Defender for Identity alert is triggered when the DPAPI is used to retrieve the backup master key.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006) <br> - **MITRE attack technique**: [Credentials from Password Stores (T1555)](https://attack.mitre.org/techniques/T1555/) <br> - **MITRE attack sub-technique**: N/A </details>|High|2020|

|<a name="suspected-brute-force-attack-kerberos-ntlm"></a><details><summary>Suspected Brute Force attack (Kerberos, NTLM)</summary><br>**Previous name**: Suspicious authentication failures.<br><br>**Description**:<br>In a brute-force attack, the attacker attempts to authenticate with multiple passwords on different accounts until a correct password is found or by using one password in a large-scale password spray that works for at least one account. Once found, the attacker logs in using the authenticated account.<br>In this detection, an alert is triggered when many authentication failures occur using Kerberos, NTLM, or use of a password spray is detected. Using Kerberos or NTLM, this type of attack is typically committed either *horizontal*, using a small set of passwords across many users, *vertical* with a large set of passwords on a few users, or any combination of the two.<br>In a password spray, after successfully enumerating a list of valid users from the domain controller, attackers try ONE carefully crafted password against ALL of the known user accounts (one password to many accounts). If the initial password spray fails, they try again, utilizing a different carefully crafted password, normally after waiting 30 minutes between attempts. The wait time allows attackers to avoid triggering most time-based account lockout thresholds. Password spray has quickly become a favorite technique of both attackers and pen testers. Password spray attacks prove to be effective at gaining an initial foothold in an organization, and for making subsequent lateral moves, trying to escalate privileges. The minimum period before an alert can be triggered is one week.<br><br>**Learning period**: One week<br> **MITRE**:<br> - **Primary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006)<br> - **MITRE attack technique**: [Brute Force (T1110)](https://attack.mitre.org/techniques/T1110/) <br> - **MITRE attack sub-technique**: [Password Guessing (T1110.001)](https://attack.mitre.org/techniques/T1110/001/), [Password Spraying (T1110.003)](https://attack.mitre.org/techniques/T1110/003/)<br><br>**Suggested steps for prevention**:<br> - Enforce [complex and long passwords](/windows/device-security/security-policy-settings/password-policy) in the organization. Doing so provides the necessary first level of security against future brute-force attacks. </details>|Medium|2023|

|<a name="security-principal-reconnaissance-ldap"></a><details><summary>Security principal reconnaissance (LDAP) </summary><br>**Description**:<br>Security principal reconnaissance is used by attackers to gain critical information about the domain environment. Information that helps attackers map the domain structure, and identify privileged accounts for use in later steps in their attack kill chain. Lightweight Directory Access Protocol (LDAP) is one the most popular methods used for both legitimate and malicious purposes to query Active Directory. LDAP focused security principal reconnaissance is commonly used as the first phase of a Kerberoasting attack. Kerberoasting attacks are used to get a target list of Security Principal Names (SPNs), which attackers then attempt to get Ticket Granting Server (TGS) tickets for.<br>To allow Defender for Identity to accurately profile and learn legitimate users, no alerts of this type are triggered in the first 10 days following Defender for Identity deployment. Once the Defender for Identity initial learning phase is completed, alerts are generated on computers that perform suspicious LDAP enumeration queries or queries targeted to sensitive groups that using methods not previously observed.<br><br>**Learning period**: 15 days per computer, starting from the day of the first event, observed from the machine.<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Discovery (TA0007)](https://attack.mitre.org/tactics/TA0007) <br> - **Secondary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006) <br> - **MITRE attack technique**: [Account Discovery (T1087)](https://attack.mitre.org/techniques/T1087/)  <br> - **MITRE attack sub-technique**: [Domain Account (T1087.002)](https://attack.mitre.org/techniques/T1087/002/)<br>**Kerberoasting specific suggested steps for prevention**:<br> - Require use of [long and complex passwords for users with service principal accounts](/windows/security/threat-protection/security-policy-settings/minimum-password-length).<br> - [Replace the user account by Group Managed Service Account (gMSA)](/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview).<br>> **Note**:> Security principal reconnaissance (LDAP) alerts are supported by Defender for Identity sensors only.</details>|Medium|2038|

|<a name="suspected-kerberos-spn-exposure"></a><details><summary>Suspected Kerberos SPN exposure </summary><br>**Description**:<br>Attackers use tools to enumerate service accounts and their respective SPNs (Service principal names), request a Kerberos service ticket for the services, capture the Ticket Granting Service (TGS) tickets from memory and extract their hashes, and save them for later use in an offline brute force attack.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006) <br> - **MITRE attack technique**: [Steal or Forge Kerberos Tickets (T1558)](https://attack.mitre.org/techniques/T1558/)<br> - **MITRE attack sub-technique**:  [Kerberoasting (T1558.003)](https://attack.mitre.org/techniques/T1558/003/) </details>|High|2410|

|<a name="suspected-as-rep-roasting-attack"></a><details><summary>Suspected AS-REP Roasting attack </summary><br>**Description**:<br>Attackers use tools to detect accounts with their *Kerberos preauthentication* disabled and send AS-REQ requests without the encrypted timestamp. In response they receive AS-REP messages with TGT data, which may be encrypted with an insecure algorithm such as RC4, and save them for later use in an offline password cracking attack (similar to Kerberoasting) and expose plaintext credentials.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006) <br> - **MITRE attack technique**: [Steal or Forge Kerberos Tickets (T1558)](https://attack.mitre.org/techniques/T1558/) <br> - **MITRE attack sub-technique**:  [AS-REP Roasting (T1558.004)](https://attack.mitre.org/techniques/T1558/004/)  <br><br>**Suggested steps for prevention**:<br> - Enable Kerberos preauthentication. For more information about account attributes and how to remediate them, see [Unsecure account attributes](/defender-for-identity/security-assessment-unsecure-account-attributes).</details>|High|2412|

|<a name="suspicious-modification-of-a-samnameaccount-attribute-cve-2021-42278-and-cve-2021-42287-exploitation"></a><details><summary>Suspicious modification of a sAMNameAccount attribute (CVE-2021-42278 and CVE-2021-42287 exploitation) </summary><br>**Description**:<br>An attacker can create a straightforward path to a Domain Admin user in an Active Directory environment that isn't patched. This escalation attack allows attackers to easily elevate their privilege to that of a Domain Admin once they compromise a regular user in the domain.<br>When performing an authentication using Kerberos, Ticket-Granting-Ticket (TGT) and the Ticket-Granting-Service (TGS) are requested from the Key Distribution Center (KDC). If a TGS was requested for an account that couldn't be found, the KDC attemptS to search it again with a trailing &dollar;.<br>When processing the TGS request, the KDC fails its lookup for the requestor machine *DC1* the attacker created. Therefore, the KDC performs another lookup appending a trailing &dollar;. The lookup succeeds. As a result, the KDC issues the ticket using the privileges of *DC1$*.<br>Combining CVEs CVE-2021-42278 and CVE-2021-42287, an attacker with domain user credentials can leverage them for granting access as a domain admin.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006) <br> - **MITRE attack technique**: [Access Token Manipulation (T1134)](https://attack.mitre.org/techniques/T1134),[Exploitation for Privilege Escalation (T1068)](https://attack.mitre.org/techniques/T1068),[Steal, or Forge Kerberos Tickets (T1558)](https://attack.mitre.org/techniques/T1558)  <br> - **MITRE attack sub-technique**: [Token Impersonation/Theft (T1134.001)](https://attack.mitre.org/techniques/T1134/001/)<br><a name="honeytoken-activity-external-id-2014"></a></details>|High|2419|

|<a name="honeytoken-authentication-activity"></a><details><summary>Honeytoken authentication activity</summary><br>**Previous name**: Honeytoken activity.<br><br>**Description**:<br>Honeytoken accounts are decoy accounts set up to identify and track malicious activity that involves these accounts. Honeytoken accounts should be left unused while having an attractive name to lure attackers (for example, SQL-Admin). Any authentication activity from them might indicate malicious behavior.<br>For more information on honeytoken accounts, see [Manage sensitive or honeytoken accounts](/defender-for-identity/entity-tags).<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006) <br> - **Secondary MITRE tactic**: [Discovery](https://attack.mitre.org/tactics/TA0007) <br> - **MITRE attack technique**: [Account Discovery (T1087)](https://attack.mitre.org/techniques/T1087/)<br> - **MITRE attack sub-technique**: [Domain Account (T1087.002)](https://attack.mitre.org/techniques/T1087/002/)   </details>|Medium|2014|

|<a name="suspected-dcsync-attack-replication-of-directory-services"></a><details><summary>Suspected DCSync attack (replication of directory services)</summary><br>**Previous name**: Malicious replication of directory services.<br><br>**Description**:<br>Active Directory replication is the process by which changes that are made on one domain controller are synchronized with all other domain controllers. Given necessary permissions, attackers can initiate a replication request, allowing them to retrieve the data stored in Active Directory, including password hashes.<br>In this detection, an alert is triggered when a replication request is initiated from a computer that isn't a domain controller.<br>> **Note**:> If you have domain controllers on which Defender for Identity sensors aren't installed, those domain controllers aren't covered by Defender for Identity. When deploying a new domain controller on an unregistered or unprotected domain controller, it might not immediately be identified by Defender for Identity as a domain controller. It's highly recommended to install the Defender for Identity sensor on every domain controller to get full coverage.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006) <br> - **Secondary MITRE tactic [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003)<br> - **MITRE attack technique**: [OS Credential Dumping (T1003)](https://attack.mitre.org/techniques/T1003/)<br> - **MITRE attack sub-technique**: [DCSync (T1003.006)](https://attack.mitre.org/techniques/T1003/006/)<br>**Suggested steps for prevention:**:<br>Validate the following permissions:<br> - Replicate directory changes.<br> - Replicate directory changes all.<br> - For more information, see [Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](/SharePoint/administration/user-profile-service-administration). You can use [AD ACL Scanner](/archive/blogs/pfesweplat/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool) or create a Windows PowerShell script to determine who in the domain has these permissions.</details>|High|2006|

|<a name="suspected-ad-fs-dkm-key-read"></a><details><summary>Suspected AD FS DKM key read </summary><br>**Description**:<br>The token signing and token decryption certificate, including the Active Directory Federation Services (AD FS) private keys, are stored in the AD FS configuration database. The certificates are encrypted using a technology called Distribute Key Manager. AD FS creates and uses these DKM keys when needed. To perform attacks like Golden SAML, the attacker would need the private keys that sign the SAML objects, similarly to how the **krbtgt** account is needed for Golden Ticket attacks. Using the AD FS user account, an attacker can access the DKM key and decrypt the certificates used to sign SAML tokens. This detection tries to find any actors that try to read the DKM key of AD FS object.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006) <br> - **MITRE attack technique**: [Unsecured Credentials (T1552)](https://attack.mitre.org/techniques/T1552/)<br - **MITRE attack sub-technique**: [Unsecured Credentials: Private Keys (T1552.004)](https://attack.mitre.org/techniques/T1552/004/)</details>|High|2413|

|<a name="suspected-dfscoerce-attack-using-distributed-file-system-protocol"></a><details><summary>Suspected DFSCoerce attack using Distributed File System Protocol </summary><br>**Description**:<br>DFSCoerce attack can be used to force a domain controller to authenticate against a remote machine which is under an attacker's control using the MS-DFSNM API, which triggers NTLM authentication. This, ultimately, enables a threat actor to launch an NTLM relay attack.  <br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006) <br> - **MITRE attack technique**: [Forced Authentication (T1187)](https://attack.mitre.org/techniques/T1187/)<br> - **:MITRE attack sub-technique**:N/A </details>|High|2426|

|<a name="suspicious-kerberos-delegation-attempt-using-bronzebit-method-cve-2020-17049-exploitation"></a><details><summary>Suspicious Kerberos delegation attempt using BronzeBit method (CVE-2020-17049 exploitation) </summary><br>**Description**:<br>Exploiting a vulnerability (CVE-2020-17049), attackers attempt suspicious Kerberos delegation using the BronzeBit method. This could lead to unauthorized privilege escalation and compromise the security of the Kerberos authentication process. <br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006) <br> - **MITRE attack technique**: [Steal or Forge Kerberos Tickets (T1558)](https://attack.mitre.org/techniques/T1558/)<br> - **MITRE attack sub-technique**: N/A </details>|Medium|2048|

|<a name="abnormal-active-directory-federation-services-ad-fs-authentication-using-a-suspicious-certificate"></a><details><summary>Abnormal Active Directory Federation Services (AD FS) authentication using a suspicious certificate </summary><br>**Description**:<br>Anomalous authentication attempts using suspicious certificates in Active Directory Federation Services (AD FS) might indicate potential security breaches. Monitoring and validating certificates during AD FS authentication are crucial for preventing unauthorized access. <br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006) <br> - **MITRE attack technique**: [Forge Web Credentials (T1606)](https://attack.mitre.org/techniques/T1606/)<br> - **MITRE attack sub-technique**: N/A<br>> **Note**:> Abnormal Active Directory Federation Services (AD FS) authentication using a suspicious certificate alerts are only supported by Defender for Identity sensors on AD FS.</details>|High|2424|

|<a name="suspected-account-takeover-using-shadow-credentials"></a><details><summary>Suspected account takeover using shadow credentials </summary><br>**Description**:<br>The use of shadow credentials in an account takeover attempt suggests malicious activity. Attackers may attempt to exploit weak or compromised credentials to gain unauthorized access and control over user accounts. <br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006) <br> -**MITRE attack technique**: [OS Credential Dumping (T1003)](https://attack.mitre.org/techniques/T1003/)<br> - **MITRE attack sub-technique**: N/A </details>|High|2431|

|<a name="suspected-suspicious-kerberos-ticket-request"></a><details><summary>Suspected suspicious Kerberos ticket request </summary><br>**Description**:<br>This attack involves the suspicion of abnormal Kerberos ticket requests. Attackers might attempt to exploit vulnerabilities in the Kerberos authentication process, potentially leading to unauthorized access and compromise of the security infrastructure.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006) <br>- **Secondary MITRE tactic**: [Collection (TA0009)](https://attack.mitre.org/tactics/TA0009) <br> - **MITRE attack technique**: [Adversary-in-the-Middle (T1557)](https://attack.mitre.org/techniques/T1557/)<br> - **MITRE attack sub-technique**: [LLMNR/NBT-NS Poisoning and SMB Relay (T1557.001)](https://attack.mitre.org/techniques/T1557/001/)</details>|High|2418|

## Lateral movement alerts

Lateral Movement consists of techniques that adversaries use to enter and control remote systems on a network. Following through on their primary objective often requires exploring the network to find their target and subsequently gaining access to it. Reaching their objective often involves pivoting through multiple systems and accounts to gain. Adversaries might install their own remote access tools to accomplish Lateral Movement or use legitimate credentials with native network and operating system tools, which may be stealthier. Microsoft Defender for Identity can cover different passing attacks (pass the ticket, pass the hash, etc.) or other exploitations against the domain controller, like PrintNightmare or remote code execution.

|Security alert name |Severity |External ID |

|---------------|---------|------------|

|<a name="suspected-exploitation-attempt-on-windows-print-spooler-service"></a><details><summary>Suspected exploitation attempt on Windows Print Spooler service </summary><br>**Description**:<br>Adversaries might exploit the Windows Print Spooler service to perform privileged file operations in an improper manner. An attacker who has (or obtains) the ability to execute code on the target, and who successfully exploits the vulnerability, could run arbitrary code with SYSTEM privileges on a target system. If run against a domain controller, the attack would allow a compromised non-administrator account to perform actions against a domain controller as SYSTEM.<br>This functionally allows any attacker who enters the network to instantly elevate privileges to Domain Administrator, steal all domain credentials, and distribute further malware as a Domain Admin.<br><br>**Learning period**: None<br> **MITRE**: <br> - **Primary MITRE tactic **: [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008) <br>- **MITRE attack technique**:  [Exploitation of Remote Services (T1210)](https://attack.mitre.org/techniques/T1210/)<br> - **MITRE attack sub-technique**: N/A**Suggested steps for prevention**:<br> - Due to the risk of the domain controller being compromised, install the security updates for [CVE-2021-34527](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-34527) on Windows domain controllers, before installing on member servers and workstations.<br> - You can use the Defender for Identity built-in security assessment that tracks the availability of Print spooler services on domain controllers. [Learn more](/defender-for-identity/security-assessment-print-spooler).</details>|High or Medium|2415|

|<a name="remote-code-execution-attempt-over-dns"></a><details><summary>Remote code execution attempt over DNS </summary><br>**Description**:<br>12/11/2018 Microsoft published [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626), announcing that a newly discovered remote code execution vulnerability exists in Windows Domain Name System (DNS) servers. In this vulnerability, servers fail to properly handle requests. An attacker who successfully exploits the vulnerability can run arbitrary code in the context of the Local System Account. Windows servers currently configured as DNS servers are at risk from this vulnerability.<br>In this detection, a Defender for Identity security alert is triggered when DNS queries suspected of exploiting the CVE-2018-8626 security vulnerability are made against a domain controller in the network.<br><br>**Learning period**: None<br> **MITRE**: <br> - **Primary MITRE tactic **: [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **Secondary MITRE tactic **: [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004)<br> - **MITRE attack technique**:  [Exploitation for Privilege Escalation (T1068)](https://attack.mitre.org/techniques/T1068/), [Exploitation of Remote Services (T1210)](https://attack.mitre.org/techniques/T1210/)<br> - **MITRE attack sub-technique**: N/A<br>**Suggested remediation and steps for prevention**:<br>- Make sure all DNS servers in the environment are up-to-date, and patched against [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626).</details>|Medium|2036|

|<a name="suspected-identity-theft-pass-the-hash"></a><details><summary>Suspected identity theft (pass-the-hash)</summary><br>**Previous name**: Identity theft using Pass-the-Hash attack.<br><br>**Description**:<br>Pass-the-Hash is a lateral movement technique in which attackers steal a user's NTLM hash from one computer and use it to gain access to another computer.<br><br>**Learning period**: None<br> **MITRE**: <br> - **Primary MITRE tactic **:  [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008) <br> - **MITRE attack technique**:  [Use Alternate Authentication Material (T1550)](https://attack.mitre.org/techniques/T1550/) <br> - **MITRE attack sub-technique**:  [Pass the Hash (T1550.002)](https://attack.mitre.org/techniques/T1550/002/)</details>|High|2017|

|<a name="suspected-identity-theft-pass-the-ticket"></a><details><summary>Suspected identity theft (pass-the-ticket)</summary><br>**Previous name**: Identity theft using Pass-the-Ticket attack.<br><br>**Description**:<br>Pass-the-Ticket is a lateral movement technique in which attackers steal a Kerberos ticket from one computer and use it to gain access to another computer by reusing the stolen ticket. In this detection, a Kerberos ticket is seen used on two (or more) different computers.<br><br>**Learning period**: None<br> **MITRE**:<br>** - **Primary MITRE tactic **:  [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **MITRE attack technique**:  [Use Alternate Authentication Material (T1550)](https://attack.mitre.org/techniques/T1550/)<br> - **MITRE attack sub-technique**:  [Pass the Ticket (T1550.003)](https://attack.mitre.org/techniques/T1550/003/) </details>|High or Medium|2018|

|<a name="suspected-ntlm-authentication-tampering"></a><details><summary>Suspected NTLM authentication tampering </summary><br>**Description**:<br>In June 2019, Microsoft published [Security Vulnerability CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040), announcing discovery of a new tampering vulnerability in Microsoft Windows, when a "man-in-the-middle" attack is able to successfully bypass NTLM MIC (Message Integrity Check) protection.<br>Malicious actors that successfully exploit this vulnerability have the ability to downgrade NTLM security features, and may successfully create authenticated sessions on behalf of other accounts. Unpatched Windows Servers are at risk from this vulnerability.<br>In this detection, a Defender for Identity security alert is triggered when NTLM authentication requests suspected of exploiting security vulnerability identified in [CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040) are made against a domain controller in the network.<br><br>**Learning period**: None<br> **MITRE**:<br>- **Primary MITRE tactic **:  [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008) **- Secondary MITRE tactic **:  [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004)   <br> - **MITRE attack technique**:  [Exploitation for Privilege Escalation (T1068)](https://attack.mitre.org/techniques/T1068/), [Exploitation of Remote Services (T1210)](https://attack.mitre.org/techniques/T1210/) <br> - **MITRE attack sub-technique**: N/A <br><br>**Suggested steps for prevention**:<br> - Force the use of sealed NTLMv2 in the domain, using the **Network security: LAN Manager authentication level** group policy. For more information, see [LAN Manager authentication level instructions](/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) for setting the group policy for domain controllers.<br> - Make sure all devices in the environment are up-to-date, and patched against [CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040).</details>|Medium|2039|

|<a name="suspected-ntlm-relay-attack-exchange-account"></a><details><summary>Suspected NTLM relay attack (Exchange account) </summary><br>**Description**:<br>An Exchange Server computer account can be configured to trigger NTLM authentication with the Exchange Server computer account to a remote http server, run by an attacker. The server waits for the Exchange Server communication to relay its own sensitive authentication to any other server, or even more interestingly to Active Directory over LDAP, and grabs the authentication information.<br>Once the relay server receives the NTLM authentication, it provides a challenge that was originally created by the target server. The client responds to the challenge, preventing an attacker from taking the response, and using it to continue NTLM negotiation with the target domain controller.<br>In this detection, an alert is triggered when Defender for Identity identify use of Exchange account credentials from a suspicious source.<br><br>**Learning period**: None<br> **MITRE**:<br> - **Primary MITRE tactic**: [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **Secondary MITRE tactic**:  [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004)   <br> - **MITRE attack technique**:  [Exploitation for Privilege Escalation (T1068)](https://attack.mitre.org/techniques/T1068/), [Exploitation of Remote Services (T1210)](https://attack.mitre.org/techniques/T1210/), [Man-in-the-Middle (T1557)](https://attack.mitre.org/techniques/T1557/)<br> - **MITRE attack sub-technique**: [LLMNR/NBT-NS Poisoning and SMB Relay (T1557.001)](https://attack.mitre.org/techniques/T1557/001/)   <br><br>**Suggested steps for prevention**:<br> - Force the use of sealed NTLMv2 in the domain, using the **Network security: LAN Manager authentication level** group policy. For more information, see [LAN Manager authentication level instructions](/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) for setting the group policy for domain controllers.</details>|Medium or Low if observed using signed NTLM v2 protocol|2037|

|<a name="suspected-overpass-the-hash-attack-kerberos"></a><details><summary>Suspected overpass-the-hash attack (Kerberos)</summary><br>**Previous name**: Unusual Kerberos protocol implementation (potential overpass-the-hash attack).<br><br>**Description**:<br>Attackers use tools that implement various protocols such as Kerberos and SMB in non-standard ways. While Microsoft Windows accepts this type of network traffic without warnings, Defender for Identity is able to recognize potential malicious intent. The behavior is indicative of techniques such as over-pass-the-hash, Brute Force, and advanced ransomware exploits such as WannaCry, are used.<br><br>**Learning period**: None<br> **MITRE**:<br> - **Primary MITRE tactic **:  [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **MITRE attack technique**: [Exploitation of Remote Services (T1210)](https://attack.mitre.org/techniques/T1210/),[Use Alternate Authentication Material (T1550)](https://attack.mitre.org/techniques/T1550/) <br>- **MITRE attack sub-technique**:  [Pass the Has (T1550.002)](https://attack.mitre.org/techniques/T1550/002/), [Pass the Ticket (T1550.003)](https://attack.mitre.org/techniques/T1550/003/)</details>|Medium|2002|

|<a name="suspected-rogue-kerberos-certificate-usage"></a><details><summary>Suspected rogue Kerberos certificate usage </summary><br>**Description**:<br>Rogue certificate attack is a persistence technique used by attackers after gaining control over the organization. Attackers compromise the Certificate Authority (CA) server and generate certificates that can be used as backdoor accounts in future attacks.<br><br>**Learning period**: None<br> **MITRE**: <br> - **Primary MITRE tactic **:  [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)**Secondary MITRE tactic **:  [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003), [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004)   <br> - **MITRE attack technique**: N/A <br> - **MITRE attack sub-technique**: N/A   </details>|High|2047|

|<a name="suspected-smb-packet-manipulation-cve-2020-0796-exploitation"></a><details><summary>Suspected SMB packet manipulation (CVE-2020-0796 exploitation) </summary><br>**Description**:<br>03/12/2020 Microsoft published [CVE-2020-0796](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796), announcing that a newly remote code execution vulnerability exists in the way that the Microsoft Server Message Block 3.1.1 (SMBv3) protocol handles certain requests. An attacker who successfully exploited the vulnerability could gain the ability to execute code on the target server or client. Unpatched Windows servers are at risk from this vulnerability.<br>In this detection, a Defender for Identity security alert is triggered when SMBv3 packet suspected of exploiting the CVE-2020-0796 security vulnerability are made against a domain controller in the network.<br><br>**Learning period**: None<br> **MITRE**:<br>- **Primary MITRE tactic **:  [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **MITRE attack technique**:  [Exploitation of Remote Services (T1210)](https://attack.mitre.org/techniques/T1210/) <br> - **MITRE attack sub-technique**:   N/A <br><br>**Suggested steps for prevention**:<br> - If your have computers with operating systems that don't support [KB4551762](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4551762), we recommend disabling the SMBv3 compression feature in the environment, as described in the [Workarounds](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796) section.<br> - Make sure all devices in the environment are up-to-date, and patched against [CVE-2020-0796](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796).</details>|High|2406|

|<a name="exchange-server-remote-code-execution-cve-2021-26855"></a><details><summary>Exchange Server Remote Code Execution (CVE-2021-26855) </summary><br>**Description**:<br>Some Exchange vulnerabilities can be used in combination to allow unauthenticated remote code execution on devices running Exchange Server. Microsoft has also observed subsequent web shell implantation, code execution, and data exfiltration activities during attacks. This threat may be exacerbated by the fact that numerous organizations publish Exchange Server deployments to the internet to support mobile and work-from-home scenarios. In many of the observed attacks, one of the first steps attackers took following successful exploitation of CVE-2021-26855, which allows unauthenticated remote code execution, was to establish persistent access to the compromised environment via a web shell.<br>Adversaries may create authentication bypass vulnerability results from having to treat requests to static resources as authenticated requests on the backend, because files such as scripts and images must be available even without authentication.<br>**Prerequisites**:<br>Defender for Identity needs Windows Event 4662 to be enabled and collected to monitor for this attack. For information on how to configure and collect this event, see [Configure Windows Event collection](configure-windows-event-collection.md), and follow the instructions for [Enable auditing on an Exchange object](configure-windows-event-collection.md#enable-auditing-on-an-exchange-object). <br>**Learning period**: None<br> **MITRE**:<br>**- Primary MITRE tactic **:  [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008) <br>- **MITRE attack technique**: [Exploitation of Remote Services (T1210)](https://attack.mitre.org/techniques/T1210/)<br>- **MITRE attack sub-technique**: N/A <br><br>**Suggested steps for prevention**:<br> Update your Exchange servers with the latest security patches. The vulnerabilities are addressed in the [March 2021 Exchange Server Security Updates](https://techcommunity.microsoft.com/t5/exchange-team-blog/released-march-2021-exchange-server-security-updates/ba-p/2175901).</details>|High|2414|

|<a name="suspected-brute-force-attack-smb"></a><details><summary>Suspected Brute Force attack (SMB)</summary><br>**Previous name**: Unusual protocol implementation (potential use of malicious tools such as Hydra).<br><br>**Description**:<br>Attackers use tools that implement various protocols such as SMB, Kerberos, and NTLM in non-standard ways. While this type of network traffic is accepted by Windows without warnings, Defender for Identity is able to recognize potential malicious intent. The behavior is indicative of brute force techniques.<br><br>**Learning period**: None<br> **MITRE**: <br> - **Primary MITRE tactic **:  [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008) <br> - **MITRE attack technique**: [Brute Force (T1110)](https://attack.mitre.org/techniques/T1110/)<br> - **MITRE attack sub-technique**: [Password Guessing (T1110.001)](https://attack.mitre.org/techniques/T1110/001/), [Password Spraying (T1110.003)](https://attack.mitre.org/techniques/T1110/003/) <br><br>**Suggested steps for prevention**:<br> - Enforce [Complex and long passwords](/windows/security/threat-protection/security-policy-settings/password-policy) in the organization. Complex and long passwords provide the necessary first level of security against future brute-force attacks.<br> - [Disable SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)</details>|Medium|2033|

|<a name="suspected-wannacry-ransomware-attack"></a><details><summary>Suspected WannaCry ransomware attack</summary><br>**Previous name**: Unusual protocol implementation (potential WannaCry ransomware attack).<br><br>**Description**:<br>Attackers use tools that implement various protocols in non-standard ways. While this type of network traffic is accepted by Windows without warnings, Defender for Identity is able to recognize potential malicious intent. The behavior is indicative of techniques used by advanced ransomware, such as WannaCry.<br><br>**Learning period**: None<br> **MITRE**: <br> - **Primary MITRE tactic **: [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **MITRE attack technique**: [Exploitation of Remote Services (T1210)](https://attack.mitre.org/techniques/T1210/) <br> - **MITRE attack sub-technique**: N/A<br><br>**Suggested steps for prevention**:<br> - Patch all of your machines, making sure to apply security updates.<br> - [Disable SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)</details>|Medium|2035|

|<a name="suspected-use-of-metasploit-hacking-framework"></a><details><summary>Suspected use of Metasploit hacking framework</summary><br>**Previous name**: Unusual protocol implementation (potential use of Metasploit hacking tools).<br><br>**Description**:<br>Attackers use tools that implement various protocols (SMB, Kerberos, NTLM) in non-standard ways. While this type of network traffic is accepted by Windows without warnings, Defender for Identity is able to recognize potential malicious intent. The behavior is indicative of techniques such as use of the Metasploit hacking framework.<br><br>**Learning period**: None<br> **MITRE**: <br> - **Primary MITRE tactic **:  [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **MITRE attack technique**: [Exploitation of Remote Services (T1210)](https://attack.mitre.org/techniques/T1210/)  <br> - **MITRE attack sub-technique**: N/A<br>**Suggested remediation and steps for prevention**:<br> - [Disable SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)</details>|Medium|2034|

|<a name="suspicious-certificate-usage-over-kerberos-protocol-pkinit"></a><details><summary>Suspicious certificate usage over Kerberos protocol (PKINIT) </summary><br>**Description**:<br>Attackers exploit vulnerabilities in the PKINIT extension of the Kerberos protocol by using suspicious certificates. This can lead to identity theft and unauthorized access. Possible attacks include the use of invalid or compromised certificates, man-in-the-middle attacks, and poor certificate management. Regular security audits and adherence to PKI best practices are crucial to mitigate these risks.<br><br>**Learning period**: None<br> **MITRE**: <br> - **Primary MITRE tactic **:  [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **MITRE attack technique**: [Use Alternate Authentication Material (T1550)](https://attack.mitre.org/techniques/T1550/) <br> - **MITRE attack sub-technique**: N/A <br>**Note: Suspicious certificate usage over Kerberos protocol (PKINIT) alerts are only supported by Defender for Identity sensors on AD CS.</details>|High|2425|

|<a name="suspected-over-pass-the-hash-attack-forced-encryption-type"></a><details><summary>Suspected over-pass-the-hash attack (forced encryption type) </summary><br>**Description**:<br>Over-pass-the-hash attacks involving forced encryption types can exploit vulnerabilities in protocols like Kerberos. Attackers attempt to manipulate network traffic, bypassing security measures and gaining unauthorized access. Defending against such attacks requires robust encryption configurations and monitoring.<br><br>**Learning period**: One month<br><br>**MITRE** <br> - **Primary MITRE tactic **:  [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)**Secondary MITRE tactic **:  [Defense Evasion (TA0005)](https://attack.mitre.org/tactics/TA0005) <br> - **MITRE attack technique**: [Use Alternate Authentication Material (T1550)](https://attack.mitre.org/techniques/T1550/)<br> - **MITRE attack sub-technique**: [Pass the Hash (T1550.002)](https://attack.mitre.org/techniques/T1550/002/), [Pass the Ticket (T1550.003)](https://attack.mitre.org/techniques/T1550/003/) </details>|Medium|2008|

## Other alerts

The following security alerts help you identify and remediate **Other** phase suspicious activities detected by Defender for Identity in your network.

|Security alert name |Severity |External ID |

|---------------|---------|------------|

|<a name="suspected-dcshadow-attack-domain-controller-promotion"></a><details><summary>Suspected DCShadow attack (domain controller promotion)</summary><br>**Previous name**: Suspicious domain controller promotion (potential DCShadow attack).<br><br>**Description**:<br>A domain controller shadow (DCShadow) attack is an attack designed to change directory objects using malicious replication. This attack can be performed from any machine by creating a rogue domain controller using a replication process.<br>In a DCShadow attack, RPC, and LDAP are used to:<br> - Register the machine account as a domain controller (using domain admin rights).<br> - Perform replication (using the granted replication rights) over DRSUAPI and send changes to directory objects.<br>In this Defender for Identity detection, a security alert is triggered when a machine in the network tries to register as a rogue domain controller.<br><br>**Learning period**: None <br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Defense Evasion (TA0005)](https://attack.mitre.org/tactics/TA0005)<br>- **MITRE attack technique**: [Rogue Domain Controller (T1207)](https://attack.mitre.org/techniques/T1207/) <br> - **MITRE attack subtechnique**: N/A<br><br>**Suggested steps for prevention**:<br>Validate the following permissions:<br> - Replicate directory changes.<br> - Replicate directory changes all.<br> - For more information, see [Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](/SharePoint/administration/user-profile-service-administration). You can use [AD ACL Scanner](/archive/blogs/pfesweplat/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool) or create a Windows PowerShell script to determine who has these permissions in the domain.<br>**Note**: Suspicious domain controller promotion (potential DCShadow attack) alerts are supported by Defender for Identity sensors only.</details>|High|2028|

|<a name="suspected-dcshadow-attack-domain-controller-replication-request"></a><details><summary>Suspected DCShadow attack (domain controller replication request)</summary><br>**Previous name**: Suspicious replication request (potential DCShadow attack).<br><br>**Description**:<br>Active Directory replication is the process by which changes that are made on one domain controller are synchronized with other domain controllers. Given necessary permissions, attackers can grant rights for their machine account, allowing them to impersonate a domain controller. Attackers strive to initiate a malicious replication request, allowing them to change Active Directory objects on a genuine domain controller, which can give the attackers persistence in the domain.<br>In this detection, an alert is triggered when a suspicious replication request is generated against a genuine domain controller protected by Defender for Identity. The behavior is indicative of techniques used in domain controller shadow attacks.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Defense Evasion (TA0005)](https://attack.mitre.org/tactics/TA0005)<br>- **MITRE attack technique**: [Rogue Domain Controller (T1207)](https://attack.mitre.org/techniques/T1207/)<br>- **MITRE attack subtechnique**: N/A <br>**Suggested remediation and steps for prevention**:<br>Validate the following permissions:<br> - Replicate directory changes.<br> - Replicate directory changes all.<br> - For more information, see [Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](/SharePoint/administration/user-profile-service-administration). You can use [AD ACL Scanner](/archive/blogs/pfesweplat/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool) or create a Windows PowerShell script to determine who in the domain has these permissions.<br>**Note**: Suspicious replication request (potential DCShadow attack) alerts are supported by Defender for Identity sensors only.</details>|High|2029|

|<a name="suspicious-vpn-connection"></a><details><summary>Suspicious VPN connection</summary><br>**Previous name**: Suspicious VPN connection.<br><br>**Description**:<br>Defender for Identity learns the entity behavior for users VPN connections over a sliding period of one month.<br>The VPN-behavior model is based on the machines users log in to and the locations the users connect from.<br>An alert is opened when there's a deviation from the user's behavior based on a machine learning algorithm.<br><br>**Learning period**: 30 days from the first VPN connection, and at least 5 VPN connections in the last 30 days, per user.<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Defense Evasion (TA0005)](https://attack.mitre.org/tactics/TA0005) <br> - **Secondary MITRE tactic**: [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003)<br> - **MITRE attack technique**: [External Remote Services (T1133)](https://attack.mitre.org/techniques/T1133/)<br> - **MITRE attack subtechnique**: N/A    </details>|Medium|2025|

|<a name="remote-code-execution-attempt"></a><details><summary>Remote code execution attempt</summary><br>**Previous name**: Remote code execution attempt.<br><br>**Description**:<br>Attackers who compromise administrative credentials or use a zero-day exploit can execute remote commands on your domain controller or AD FS / AD CS  server. This can be used for gaining persistency, collecting information, denial of service (DOS) attacks or any other reason. Defender for Identity detects PSexec, Remote WMI, and PowerShell connections.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Execution (TA0002)](https://attack.mitre.org/tactics/TA0002)<br> - **Secondary MITRE tactic**: [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **MITRE attack technique**: [Command and Scripting Interpreter (T1059)](https://attack.mitre.org/techniques/T1059/),[Remote Services (T1021)](https://attack.mitre.org/techniques/T1021/)<br> - **MITRE attack subtechnique**: [PowerShell (T1059.001)](https://attack.mitre.org/techniques/T1059/001/), [Windows Remote Management (T1021.006)](https://attack.mitre.org/techniques/T1021/006/) <br>**Suggested steps for prevention:**<br> - Restrict remote access to domain controllers from non-Tier 0 machines.<br> - Implement [privileged access](/windows-server/identity/securing-privileged-access/securing-privileged-access), allowing only hardened machines to connect to domain controllers for admins.<br> - Implement less-privileged access on domain machines to allow specific users the right to create services.<br>**Note**: Remote code execution attempt alerts on attempted use of PowerShell commands are only supported by Defender for Identity sensors.</details>|Medium|2019|

|<a name="suspicious-service-creation"></a><details><summary>Suspicious service creation</summary><br>**Previous name**: Suspicious service creation.<br><br>**Description**:<br>A suspicious service has been created on a domain controller or AD FS  / AD CS server in your organization. This alert relies on event 7045 to identify this suspicious activity.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Execution (TA0002)](https://attack.mitre.org/tactics/TA0002)<br> - **Secondary MITRE tactic: [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003), [Privilege Escalation (TA0004)](https://attack.mitre.org/tactics/TA0004), [Defense Evasion (TA0005)](https://attack.mitre.org/tactics/TA0005), [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008)<br> - **MITRE attack technique**: [Remote Services (T1021)](https://attack.mitre.org/techniques/T1021/), [Command, and Scripting Interpreter (T1059)](https://attack.mitre.org/techniques/T1059/), [System Services (T1569)](https://attack.mitre.org/techniques/T1569/), [Create or Modify System Process (T1543)](https://attack.mitre.org/techniques/T1543/)<br> - **MITRE attack subtechnique**: [Service Execution (T1569.002)](https://attack.mitre.org/techniques/T1569/002/), [Windows Service (T1543.003)](https://attack.mitre.org/techniques/T1543/003/)<br><br>**Suggested steps for prevention**:<br> - Restrict remote access to domain controllers from non-Tier 0 machines.<br> - Implement [privileged access](/windows-server/identity/securing-privileged-access/securing-privileged-access) to allow only hardened machines to connect to domain controllers for administrators.<br> - Implement less-privileged access on domain machines to give only specific users the right to create services.</details>|Medium|2026|

|<a name="suspicious-communication-over-dns"></a><details><summary>Suspicious communication over DNS</summary><br>**Previous name**: Suspicious communication over DNS.<br><br>**Description**:<br>The DNS protocol in most organizations is typically not monitored and rarely blocked for malicious activity. Enabling an attacker on a compromised machine, to abuse the DNS protocol. Malicious communication over DNS can be used for data exfiltration, command, and control, and/or evading corporate network restrictions.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Exfiltration (TA0010)](https://attack.mitre.org/tactics/TA0010)<br> - **MITRE attack technique**: [Exfiltration Over Alternative Protocol (T1048)](https://attack.mitre.org/techniques/T1048/), [Exfiltration Over C2 Channel (T1041)](https://attack.mitre.org/techniques/T1041/), [Scheduled Transfer (T1029)](https://attack.mitre.org/techniques/T1029/), [Automated Exfiltration (T1020)](https://attack.mitre.org/techniques/T1020/), [Application Layer Protocol (T1071)](https://attack.mitre.org/techniques/T1071/)<br> - **MITRE attack subtechnique**: [DNS (T1071.004)](https://attack.mitre.org/techniques/T1071/004/), [Exfiltration over Unencrypted/Obfuscated Non-C2 Protocol (T1048.003)](https://attack.mitre.org/techniques/T1048/003/)</details>|Medium|2031|

|<a name="data-exfiltration-over-smb"></a><details><summary>Data exfiltration over SMB </summary><br>**Description**:<br>Domain controllers hold the most sensitive organizational data. For most attackers, one of their top priorities is to gain domain controller access, to steal your most sensitive data. For example, exfiltration of the Ntds.dit file, stored on the DC, allows an attacker to forge Kerberos ticket granting tickets(TGT) providing authorization to any resource. Forged Kerberos TGTs enable the attacker to set the ticket expiration to any arbitrary time. A Defender for Identity **Data exfiltration over SMB** alert is triggered when suspicious transfers of data are observed from your monitored domain controllers.<br><br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Exfiltration (TA0010)](https://attack.mitre.org/tactics/TA0010) <br> - **Secondary MITRE tactic**: [Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008),[Command, and Control (TA0011)](https://attack.mitre.org/tactics/TA0011)<br> - **MITRE attack technique**: [Exfiltration Over Alternative Protocol (T1048)](https://attack.mitre.org/techniques/T1048/), [Lateral Tool Transfer (T1570)](https://attack.mitre.org/techniques/T1570/)<br> - **MITRE attack subtechnique**: [Exfiltration Over Unencrypted/Obfuscated Non-C2 Protocol (T1048.003)](https://attack.mitre.org/techniques/T1048/003/) </details>|High|2030|

|<a name="suspicious-deletion-of-the-certificate-database-entries"></a><details><summary>Suspicious deletion of the certificate database entries </summary><br>**Description**:<br>The deletion of certificate database entries is a red flag, indicating potential malicious activity. This attack could disrupt the functioning of Public Key Infrastructure (PKI) systems, impacting authentication, and data integrity. <br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Defense Evasion (TA0005)](https://attack.mitre.org/tactics/TA0005)<br>- **MITRE attack technique**: [Indicator Removal (T1070)](https://attack.mitre.org/techniques/T1070/)- **MITRE attack subtechnique**: N/A<br>**Note**: Suspicious deletions of the certificate database entries alerts are only supported by Defender for Identity sensors on AD CS.</details>|Medium|2433|

|<a name="suspicious-disable-of-audit-filters-of-ad-cs"></a><details><summary>Suspicious disable of audit filters of AD CS </summary><br>**Description**:<br>Disabling audit filters in AD CS can allow attackers to operate without being detected. This attack aims to evade security monitoring by disabling filters that would otherwise flag suspicious activities. <br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Defense Evasion (TA0005)](https://attack.mitre.org/tactics/TA0005 )<br>- **MITRE attack technique**: [Impair Defenses (T1562)](https://attack.mitre.org/techniques/T1562/)<br> - **MITRE attack subtechnique**: [Disable Windows Event Logging (T1562.002)](https://attack.mitre.org/techniques/T1562/002/)      </details>|Medium|2434|

|<a name="directory-services-restore-mode-password-change"></a><details><summary>Directory Services Restore Mode Password Change </summary><br>**Description**:<br>Directory Services Restore Mode (DSRM) is a special boot mode in Microsoft Windows Server operating systems that allows an administrator to repair or restore the Active Directory database. This mode is typically used when there are issues with the Active Directory and normal booting isn't possible. The DSRM password is set during the promotion of a server to a domain controller. In this detection, an alert is triggered when Defender for Identity detects a DSRM password is changed. <br>We recommend investigating the source computer and the user who made the request to understand if the DSRM password change was initiated from a legitimate administrative action or if it raises concerns about unauthorized access or potential security threats. <br>**Learning period**: None<br><br>**MITRE**:<br> - **Primary MITRE tactic**: [Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003)- **MITRE attack technique**: [Account Manipulation (T1098)](https://attack.mitre.org/techniques/T1098/)- **MITRE attack subtechnique**:  N/A       </details>|Medium|2438|

> [!NOTE]

> Contact support to disable security alerts.

## See Also

- [View and manage security alerts](understanding-security-alerts.md)

- [Investigate security alerts](/defender-for-identity/investigate-security-alerts)

- [Check out the Defender for Identity forum!](<https://aka.ms/MDIcommunity>)


# Alerts Xdr

# Microsoft Defender for Identity alerts in Microsoft Defender format

This article lists all Defender for Identity security alerts in the Defender format. Defender for Identity sends these alerts to the Microsoft Defender portal.

Defender for Identity generates alerts in both the Defender format and the [classic format](alerts-overview.md). The Defender format provides an alert structure that's consistent with other Microsoft Defender products. Both formats are based on the same underlying detections from Defender for Identity sensors, but they differ in structure, naming, and categorization.

To identify the format of each alert, check the **Detection source** field on the security alerts page.

## Alert name mapping

Alert names in the XDR structure differ from the alert names in the classic structure, but alert IDs stay consistent between the two structures.

For more information, see [Security alerts in Microsoft Defender XDR](/microsoft-365/security/defender/investigate-alerts) and [Investigate alerts in Microsoft Defender XDR](/microsoft-365/security/defender/investigate-alerts#alert-sources).

## Alerts by category

Defender for Identity XDR security alerts are divided by category, or phase, as seen in a typical cyber-attack kill chain.

Use the following links to jump directly to the relevant category and review the available alerts:

- [Command and Control alerts](#command-and-control-alerts)

- [Credential Access alerts](#credential-access-alerts)

- [Defense Evasion alerts](#defense-evasion-alerts)

- [Discovery alerts](#discovery-alerts)

- [Execution alerts](#execution-alerts)

- [Impact alerts](#impact-alerts)

- [Initial Access alerts](#initial-access-alerts)

- [Lateral Movement alerts](#lateral-movement-alerts)

- [Persistence alerts](#persistence-alerts)

- [Privilege Escalation alerts](#privilege-escalation-alerts)

## Command and Control alerts

The following alerts indicate that a malicious actor might be trying to communicate with compromised systems to control them.

| Security alert name | Severity | MITRE Technique | Detector ID |

|---|---|---|---|

|<a name="suspicious-dns-query-from-a-device-in-the-organization"></a><details><summary>Suspicious DNS query from a device in the organization</summary><br>**Description**:<br><br>A device in the organization performed a DNS query to a domain name which is identified as suspicious by Microsoft Threat Intelligence.</details> | Medium | [T1071.004](https://attack.mitre.org/techniques/T1071/004) | xdr_SuspiciousActiveDirectoryDnsQuery |

|<a name="suspicious-entra-graph-api-query-observed"></a><details><summary>Suspicious Entra Graph API query observed</summary><br>**Description**:<br><br>Suspicious Entra Graph API activity was observed, originating from an IP address identified by Microsoft Threat Intelligence.</details> | Medium | [T1071.001](https://attack.mitre.org/techniques/T1071/001) | xdr_SuspiciousEntraGraphCall |

## Credential Access alerts

The following alerts indicate that a malicious actor might be attempting to steal account names and passwords from your organization.

| Security alert name | Severity | MITRE Technique | Detector ID |

|---|---|---|---|

|<a name="a-compromised-user-account-signed-in"></a><details><summary>A compromised user account signed in</summary><br>**Description**:<br><br>Credential stuffing led to a successful sign in, confirming an account has been compromised and accessed by an unauthorized party.</details> | High | [T1078](https://attack.mitre.org/techniques/T1078) | xdr_CredentialStuffingToolObserved |

|<a name="anomalous-oauth-device-code-authentication-activity"></a><details><summary>Anomalous OAuth device code authentication activity</summary><br>**Description**:<br><br>An OAuth Device Code authentication was detected in an unusual context based on user behavior and sign-in patterns. Due to the design of Device Code flows, this activity requires immediate investigation as it may indicate unauthorized token issuance or post-authentication abuse.</details> | High | [T1528](https://attack.mitre.org/techniques/T1528), [T1078.004](https://attack.mitre.org/techniques/T1078/004) | xdr_AnomalousDeviceCodeAuth |

|<a name="as-rep-roasting"></a><details><summary>AS-REP roasting</summary><br>**Description**:<br><br>Multiple attempts to sign in without preauthentication were detected. This behavior might indicate an Authentication Server Response (AS-REP) roasting attack, which targets the Kerberos authentication protocol, specifically accounts that have turned off preauthentication.</details> | High | [T1558.004](https://attack.mitre.org/techniques/T1558/004) | xdr_AsrepRoastingAttack |

|<a name="dcsync-attack-replication-of-directory-services"></a><details><summary>DCSync attack (replication of directory services)</summary><br>**Description**:<br><br>A DCSync replication request was detected from {IPAddress}. This indicates an attacker may be using Directory Replication Service (DRS) to extract password hashes from Active Directory, potentially compromising all domain credentials.</details> | High | [T1003.006](https://attack.mitre.org/techniques/T1003/006) | xdr_DcSyncAttackDetected |

|<a name="honeytoken-activity"></a><details><summary>Honeytoken Activity</summary><br>**Description**:<br><br>Honeytoken user attempted to sign in</details> | High | [T1098](https://attack.mitre.org/techniques/T1098) | xdr_HoneytokenSignInAttempt |

|<a name="malicious-sign-in-from-a-randomized-user-agent"></a><details><summary>Malicious sign in from a randomized user agent</summary><br>**Description**:<br><br>A user's credentials were intercepted from an unusual user agent. This user agent has recently been observed in a sign-in pattern related to adversary-in-the-middle and password spraying attacks. We recommend that you promptly investigate this alert, as an attacker might already be using the stolen credentials to move laterally in the network.</details> | High | [T1539](https://attack.mitre.org/techniques/T1539), [T1110.003](https://attack.mitre.org/techniques/T1110/003), [T1110.001](https://attack.mitre.org/techniques/T1110/001) | xdr_AnomalousRandomUASignIn |

|<a name="multiple-failed-okta-authentication-attempts-detected"></a><details><summary>Multiple failed Okta authentication attempts detected</summary><br>**Description**:<br><br>Multiple failed Okta authentication attempts were detected for user {AccountUpn}. A total of {TotalFailedRequestCounts} failed attempts originated from IP address {IPAddress} within a 2 minute window. The attempts involved authentication actions {ActionType}. This activity indicates a brute force attack or credential stuffing attempt. The user agent string {UserAgent} was used across all attempts.</details> | High | [T1110](https://attack.mitre.org/techniques/T1110) | xdr_OktaMultipleFailedLogons |

|<a name="multiple-failed-okta-sign-in-attempts-followed-by-successful-sign-in-with-anomalous-user-behavior"></a><details><summary>Multiple failed Okta sign in attempts followed by successful sign in with anomalous user behavior</summary><br>**Description**:<br><br>Multiple failed sign-in attempts followed by a successful sign-in were observed for user {AccountUpn} within a short time span. The activity included high-risk properties {RiskyBehaviors}, classified by Okta as {RiskLevel}. All sign-in attempts originated from a single IP address {IPAddress}.</details> | High | [T1110](https://attack.mitre.org/techniques/T1110), [T1078](https://attack.mitre.org/techniques/T1078) | xdr_OktaMultipleFailedLogonsFollowedBySignIn |

|<a name="negoex-relay-attack"></a><details><summary>NEGOEX relay attack</summary><br>**Description**:<br><br>An attacker used NEGOEX to impersonate a server that a client wants to connect to so that the attacker can then relay the authentication process to any target. This allows the attacker to gain access to the target. NEGOEX is an authentication protocol designed to authenticate user accounts to Microsoft Entra joined devices.</details> | High | [T1187](https://attack.mitre.org/techniques/T1187), [T1557.001](https://attack.mitre.org/techniques/T1557/001) | xdr_NegoexRelayAttack |

|<a name="okta-fastpass-phishing-attack-detected"></a><details><summary>Okta FastPass phishing attack detected</summary><br>**Description**:<br><br>A successful Okta FastPass phishing attack was detected for user {AccountUpn}. An initial phishing attempt was declined at {phishingAttemptTime}, but the compromised session {SessionId} was later used for authentication actions at {Timestamp}. The session originated from IP address {PhishingIPAddress} and was subsequently reused from {ReuseIPAddress} with user agent {ReuseUserAgent}. Risk level: {SessionReuseRisk}.</details> | High | [T1539](https://attack.mitre.org/techniques/T1539), [T1550.004](https://attack.mitre.org/techniques/T1550/004) | xdr_OktaFastPassPhishingAttempt |

|<a name="okta-privileged-role-assigned-to-application"></a><details><summary>Okta privileged role assigned to application</summary><br>**Description**:<br><br>{ActorAliasName} assigned {RoleDisplayName} role to application: {ApplicationDisplayName}</details> | High | [T1003.006](https://attack.mitre.org/techniques/T1003/006) | xdr_OktaPrivilegedRoleAssignedToApplication |

|<a name="possible-account-secret-leak"></a><details><summary>Possible account secret leak</summary><br>**Description**:<br><br>A failed attempt to sign in to a user account by a credential stuffing tool was detected. The error code indicates that the secret was valid but misused. The user account's credentials might have been leaked or are in the possession of an unauthorized party.</details> | High | [T1078](https://attack.mitre.org/techniques/T1078) | xdr_CredentialStuffingToolObserved |

|<a name="possible-adversary-in-the-middle-aitm-attack-detected-consentfix"></a><details><summary>Possible adversary-in-the-middle (AiTM) attack detected (ConsentFix)</summary><br>**Description**:<br><br>A possible token theft has been detected. Threat actor tricked a user into granting consent or sharing an authorization code through social engineering or adversary-in-the-middle (AiTM) techniques. A stolen code is exchanged for access tokens. Threat actor then impersonates the user without a password or multifactor authentication (MFA). This allows unauthorized access to Microsoft 365 services and sensitive data.</details> | High | [T1557](https://attack.mitre.org/techniques/T1557) | xdr_PossibleAitMConsentFix |

|<a name="possible-as-rep-roasting-attack"></a><details><summary>Possible AS-REP roasting attack</summary><br>**Description**:<br><br>A suspicious Kerberos authentication request was made to accounts that do not require pre-authentication. An attacker might be performing an AS-REP roasting attack to steal passwords and gain further access into the network.</details> | Medium | [T1558.004](https://attack.mitre.org/techniques/T1558/004) | xdr_AsrepRoastingAttack |

|<a name="possible-golden-saml-attack"></a><details><summary>Possible Golden SAML attack</summary><br>**Description**:<br><br>A privileged user account authenticated with characteristics that might be related to a Golden SAML attack.</details> | High | [T1071](https://attack.mitre.org/techniques/T1071), [T1606.002](https://attack.mitre.org/techniques/T1606/002) | xdr_PossibleGoldenSamlAttack |

|<a name="possible-golden-ticket-attack"></a><details><summary>Possible golden ticket attack</summary><br>**Description**:<br><br>A suspicious Kerberos ticket granting service (TGS) request was observed. An attacker might be using stolen credentials of the KRBTGT account to attempt a golden ticket attack.</details> | High | [T1558.001](https://attack.mitre.org/techniques/T1558/001) | xdr_PossibleGoldenTicketAttacks |

|<a name="possible-golden-ticket-attack-cve-2021-42287-exploitation"></a><details><summary>Possible golden ticket attack (CVE-2021-42287 exploitation)</summary><br>**Description**:<br><br>A suspicious Kerberos ticket-granting ticket (TGT) containing anomalous Kerberos Privilege Attribute Certificate (PAC) was observed. An attacker may be using stolen credentials of the KRBTGT account to attempt a golden ticket attack. This alert triggers when an attacker forges or modifies a Kerberos PAC in an attempt to exploit the CVE-2021-42287 vulnerability. Successful exploitation allows attackers to escalate privileges and impersonate highly privileged accounts by causing the Key Distribution Center (KDC) to create a service ticket with a higher privilege level than that of a compromised account. The targeted domain controller is patched with KB5008380, which addresses this security bypass vulnerability.</details> | High | [T1558.001](https://attack.mitre.org/techniques/T1558/001) | xdr_PossibleGoldenTicketAttack_SuspiciousPac |

|<a name="possible-golden-ticket-attack-suspicious-ticket"></a><details><summary>Possible golden ticket attack (suspicious ticket)</summary><br>**Description**:<br><br>A suspicious Kerberos ticket-granting service (TGS) request originating from the IP address {SourceIpAddress} has been detected. This TGS ticket request is suspected to contain a forged or modified Kerberos ticket-granting ticket (TGT). An attacker might be using stolen credentials of the KRBTGT account to attempt a golden ticket attack.</details> | High | [T1558.001](https://attack.mitre.org/techniques/T1558/001) | xdr_PossibleGoldenTicketAttack_SuspiciousTicket |

|<a name="possible-kerberoasting-attack"></a><details><summary>Possible Kerberoasting attack</summary><br>**Description**:<br><br>One or more suspicious Kerberos ticket-granting service requests (TGS-REQ), originating from the IP address {SourceIpAddress}, have been detected. This activity might indicate a potential Kerberoasting attack, in which an attacker requests Kerberos service tickets for accounts with Service Principal Names (SPNs) in the Active Directory. The attacker then extracts and attempts to crack the encrypted tickets offline to obtain the plaintext passwords of those accounts. These targeted accounts might have been compromised, allowing the attacker to move laterally within the organization, escalate privileges, steal data, or set up backdoors for future access and persistence.</details> | High | [T1558.003](https://attack.mitre.org/techniques/T1558/003) | xdr_PossibleKerberoastingAttack |

|<a name="possible-kerberoasting-attack-following-a-suspicious-ldap-query"></a><details><summary>Possible Kerberoasting attack following a suspicious LDAP query</summary><br>**Description**:<br><br>Following a recent alert regarding a suspected Kerberoasting-related Lightweight Directory Access Protocol (LDAP) query, one or more suspicious Kerberos ticket-granting service requests (TGS-REQ) originating from the IP address {SourceIpAddress} have been detected. This activity might indicate a potential Kerberoasting attack, where an attacker enumerates accounts with Service Principal Names (that is, Kerberoastable accounts) in Active Directory and then requests Kerberos service tickets for these accounts. The attacker then extracts and attempts to crack the encrypted tickets offline to obtain the plaintext passwords of those accounts.</details> | High | [T1558.003](https://attack.mitre.org/techniques/T1558/003), [T1087.002](https://attack.mitre.org/techniques/T1087/002) | xdr_PossibleKerberoastingFollowingSuspiciousLdapQuery |

|<a name="possible-kerberoasting-attack-using-a-stealthy-ldap-search"></a><details><summary>Possible Kerberoasting attack using a stealthy LDAP search</summary><br>**Description**:<br><br>One or more stealthy Lightweight Directory Access Protocol (LDAP) queries exposing Service Principal Names (SPNs), followed by suspicious Kerberos ticket-granting service requests (TGS-REQ) originating from the IP address {SourceIpAddress}, have been detected. This activity might indicate an attacker's attempt at a stealthier Kerberoasting attack by avoiding the use of the '(servicePrincipalName=*)' LDAP query filter.</details> | High | [T1558.003](https://attack.mitre.org/techniques/T1558/003), [T1087.002](https://attack.mitre.org/techniques/T1087/002) | xdr_PossibleStealthyLdapKerberoastingAttack |

|<a name="possible-kerberos-key-list-attack"></a><details><summary>Possible Kerberos key list attack</summary><br>**Description**:<br><br>One or more suspicious Kerberos ticket-granting service (TGS) requests originating from the IP address {SourceIpAddress} have been detected. An attacker might be using stolen credentials of a read-only domain controller (RODC)-owned KRBTGT account to carry out a Kerberos key list attack. As part of this attack, the attacker forges an RODC golden ticket for a targeted account and then sends a specially crafted Kerberos TGS request containing the forged ticket. In response, the attacker may obtain the targeted account's long-term secret (for example, NT hash).</details> | High | [T1558.001](https://attack.mitre.org/techniques/T1558/001) | xdr_PossibleKerberosKeyListAttack |

|<a name="possible-netsync-attack"></a><details><summary>Possible NetSync attack</summary><br>**Description**:<br><br>NetSync is a module in Mimikatz, a post-exploitation tool, that requests the password hash of a target device's password by pretending to be a domain controller. An attacker might be performing malicious activities inside the network using this feature to gain access to the organization's resources.</details> | High | [T1003.006](https://attack.mitre.org/techniques/T1003/006) | xdr_PossibleNetsyncAttack |

|<a name="possible-oauth-code-theft-detected-through-consent-abuse"></a><details><summary>Possible OAuth code theft detected through consent abuse</summary><br>**Description**:<br><br>A possible OAuth authorization code theft has been detected. Threat actors tricked a user into granting consent or sharing an authorization code through social engineering or adversary-in-the-middle (AiTM) techniques. A stolen code is exchanged for access tokens. Threat actors then impersonate the user without a password or multifactor authentication (MFA). This allows unauthorized access to Microsoft 365 services and sensitive data.</details> | High | [T1557](https://attack.mitre.org/techniques/T1557) | xdr_PossibleOauthCodeTheft |

|<a name="possible-overpass-the-hash-attack"></a><details><summary>Possible overpass-the-hash attack</summary><br>**Description**:<br><br>A possible overpass-the-hash attack was detected. In this type of attack, an attacker uses the NT hash of a user account or other Kerberos keys to obtain Kerberos tickets, which allows unauthorized access to network resources.</details> | High | [T1550.002](https://attack.mitre.org/techniques/T1550/002) | xdr_PossibleOverPassTheHash |

|<a name="possible-service-principal-account-secret-leak"></a><details><summary>Possible service principal account secret leak</summary><br>**Description**:<br><br>A failed attempt to sign in to a service principal account by a credential stuffing tool was detected. The error code indicates that the secret was valid but misused. The service principal account's credentials might have been leaked or are in the possession of an unauthorized party.</details> | Medium | [T1078](https://attack.mitre.org/techniques/T1078) | xdr_CredentialStuffingToolObserved |

|<a name="possible-use-of-a-stolen-session-cookie"></a><details><summary>Possible use of a stolen session cookie</summary><br>**Description**:<br><br>An active user session was observed across different environments with inconsistent user-agent, network, or location attributes. This anomaly may indicate unauthorized session reuse and should be investigated for potential account compromise.</details> | High | [T1557](https://attack.mitre.org/techniques/T1557), [T1539](https://attack.mitre.org/techniques/T1539), [T1598](https://attack.mitre.org/techniques/T1598) | xdr_BrowserSessionCookieTheft |

|<a name="possibly-compromised-service-principal-account-signed-in"></a><details><summary>Possibly compromised service principal account signed in</summary><br>**Description**:<br><br>A possibly compromised service principal account signed in. A credential stuffing attempt was successfully authenticated, indicating that the service principal account's credentials might have been leaked or are in the possession of an unauthorized party.</details> | High | [T1078](https://attack.mitre.org/techniques/T1078) | xdr_CredentialStuffingToolObserved |

|<a name="possibly-compromised-service-principal-account-signed-in"></a><details><summary>Possibly compromised service principal account signed in</summary><br>**Description**:<br><br>A possibly compromised service principal account signed in. An automated tool used for discovery successfully logged into a service principal account, indicating that the service principal account's credentials might have been leaked or are in the possession of an unauthorized party.</details> | High | [T1078](https://attack.mitre.org/techniques/T1078) | xdr_DiscoveryToolObserved |

|<a name="possibly-compromised-user-account-signed-in"></a><details><summary>Possibly compromised user account signed in</summary><br>**Description**:<br><br>A possibly compromised user account signed in. An automated tool used for discovery successfully logged into a user account, indicating that the user account's credentials might have been leaked or are in the possession of an unauthorized party.</details> | High | [T1078](https://attack.mitre.org/techniques/T1078) | xdr_DiscoveryToolObserved |

|<a name="stolen-session-cookie-replay-detected"></a><details><summary>Stolen session cookie replay detected</summary><br>**Description**:<br><br>An active user session was observed across different environments with inconsistent user-agent, network, or location attributes. This anomaly may indicate unauthorized session reuse and should be investigated for potential account compromise.</details> | High | [T1557](https://attack.mitre.org/techniques/T1557), [T1539](https://attack.mitre.org/techniques/T1539), [T1598](https://attack.mitre.org/techniques/T1598) | xdr_BrowserSessionCookieTheft |

|<a name="sailpoint-isc-suspected-brute-force-attack"></a><details><summary>SailPoint ISC suspected brute-force attack</summary><br>**Description**:<br><br>Multiple failed authentication attempts were detected in SailPoint Identity Security Cloud from the IP address {IPAddress}. This activity might indicate a potential brute-force attack.</details> | High | [T1110.001](https://attack.mitre.org/techniques/T1110/001) | xdr_SailPointBruteforceAttack |

|<a name="suspected-brute-force-attack-kerberos-ntlm"></a><details><summary>Suspected brute-force attack (Kerberos, NTLM)</summary><br>**Description**:<br><br>Suspicious brute force has been detected. A threat actor might have carried out brute force on your Active Directory and possibly found passwords of users, could lead to serious security threats and data breach.</details> | Medium | [T1110.001](https://attack.mitre.org/techniques/T1110/001) | xdr_OnPremBruteforce |

|<a name="suspected-brute-force-attack-on-lightweight-directory-access-protocol-ldap-authentication"></a><details><summary>Suspected brute-force attack on Lightweight Directory Access Protocol (LDAP) authentication</summary><br>**Description**:<br><br>A series of suspicious login attempts from a single device was detected against a single user account.</details> | Medium | [T1110.001](https://attack.mitre.org/techniques/T1110/001) | xdr_LdapBindBruteforce |

|<a name="suspected-conditional-access-bypass-via-non-compliant-device"></a><details><summary>Suspected Conditional Access bypass via non-compliant device</summary><br>**Description**:<br><br>A sign-in was observed from non‑compliant devices where Conditional Access policies requiring device compliance were not enforced for the accessed resources. The previously compliant devices are no longer compliant, which might indicate post‑compromise changes. This pattern might be indicative of adversarial activity where an attacker degrades device compliance while continuing to sign in to targeted resources through Conditional Access bypass paths, enabling token issuance or further access. Go through the Recommendation section to immediately investigate and mitigate associated risks.</details> | Medium | [T1078.004](https://attack.mitre.org/techniques/T1078/004) | xdr_SuspectedCABwithNonCompliantDevice |

|<a name="suspected-password-spray-attack-kerberos-ntlm"></a><details><summary>Suspected password spray attack (Kerberos, NTLM)</summary><br>**Description**:<br><br>Suspicious password spray has been detected. A threat actor might have carried out password spray on your Active Directory and possibly found passwords of users, could lead to serious security threats and data breach.</details> | Medium | [T1110.003](https://attack.mitre.org/techniques/T1110/003) | xdr_OnPremPasswordSpray |

|<a name="suspected-password-spray-attack-on-lightweight-directory-access-protocol-ldap-authentication"></a><details><summary>Suspected password spray attack on Lightweight Directory Access Protocol (LDAP) authentication</summary><br>**Description**:<br><br>A single device was observed attempting logins across multiple user accounts, indicating a malicious authentication pattern.</details> | Medium | [T1110.003](https://attack.mitre.org/techniques/T1110/003) | xdr_LdapBindBruteforce |

|<a name="suspicious-creation-of-esxi-group"></a><details><summary>Suspicious creation of ESXi group</summary><br>**Description**:<br><br>A suspicious VMware ESXi group was created in the domain. This might indicate that an attacker is trying to get more permissions for later steps in an attack.</details> | High | [T1098](https://attack.mitre.org/techniques/T1098) | xdr_SuspiciousUserAdditionToEsxGroup |

|<a name="suspicious-dmsa-related-activity-detected"></a><details><summary>Suspicious DMSA related activity detected</summary><br>**Description**:<br><br>A suspicious Delegated Managed Service Account (DMSA) related activity was detected. This may indicate a compromised managed account or an attempt to exploit a DMSA account.</details> | High | [T1555](https://attack.mitre.org/techniques/T1555) | xdr_SuspiciousDmsaAction |

|<a name="suspicious-email-app-consent-grant"></a><details><summary>Suspicious email app consent grant</summary><br>**Description**:<br><br>A suspicious email application consent grant has been detected from a possibly compromised user account. An attacker might have leveraged the illicit consent grant to use the legitimate email application for unauthorized access to and collection of user data, persistence, or to maliciously send email on behalf of the user.</details> | Medium | [T1110.004](https://attack.mitre.org/techniques/T1110/004), [T1110.003](https://attack.mitre.org/techniques/T1110/003) | xdr_MfaTamperingAndEmailSoftwareAbuse |

|<a name="suspicious-entra-account-enablement-after-disruption"></a><details><summary>Suspicious Entra account enablement after disruption</summary><br>**Description**:<br><br>An account that was previously disabled as part of a disruption or containment action was subsequently re‑enabled. This behavior is highly suspicious and may indicate an attempt by a threat actor to restore access to a compromised identity or bypass containment measures.</details> | High | [T1098](https://attack.mitre.org/techniques/T1098) | xdr_SuspiciousAccountEnabled |

|<a name="suspicious-golden-gmsa-related-activity"></a><details><summary>Suspicious Golden gMSA related activity</summary><br>**Description**:<br><br>A suspicious read activity was made to sensitive group Managed Service Account (gMSA) objects, which could be associated with a threat actor trying to leverage the Golden gMSA attack.</details> | High | [T1555](https://attack.mitre.org/techniques/T1555) | xdr_SuspiciousGoldenGmsaActivity |

|<a name="suspicious-kerberos-authentication-ap-req"></a><details><summary>Suspicious Kerberos authentication (AP-REQ)</summary><br>**Description**:<br><br>A suspicious Kerberos application request (AP-REQ) was detected. An attacker might be using stolen credentials of a service account to attempt a silver ticket attack. In this kind of attack, an attacker forges a service ticket (Ticket Granting Service or TGS) for a specific service within a network, which allows the attacker to access that service without needing to interact with the domain controller after the initial compromise.</details> | High | [T1558.002](https://attack.mitre.org/techniques/T1558/002) | xdr_SuspiciousKerberosApReq |

|<a name="suspicious-kerberos-authentication-as-req"></a><details><summary>Suspicious Kerberos authentication (AS-REQ)</summary><br>**Description**:<br><br>A suspicious Kerberos authentication request (AS-REQ) for a ticket-granting ticket (TGT) was observed. This anomalous TGT request is suspected to have been specially crafted by an attacker. The attacker might be using stolen credentials to leverage this attack.</details> | Medium | [T1550](https://attack.mitre.org/techniques/T1550), [T1558](https://attack.mitre.org/techniques/T1558) | xdr_SusKerberosAuth_AsReq |

|<a name="suspicious-kerberos-authentication-tgs-req"></a><details><summary>Suspicious Kerberos authentication (TGS-REQ)</summary><br>**Description**:<br><br>A suspicious Kerberos ticket-granting service (TGS) ticket request has been observed. This anomalous TGS request is suspected to have been specially crafted by an attacker, possibly using a malicious tool. The attacker might also be using stolen credentials to carry out this attack. Anomalous Kerberos TGS requests are commonly observed in various attack techniques, including Kerberoasting, remote code execution (RCE), credential dumping, among others.</details> | Medium | [T1550](https://attack.mitre.org/techniques/T1550), [T1558](https://attack.mitre.org/techniques/T1558) | xdr_SusKerberosAuth_TgsReq |

|<a name="suspicious-kerberos-authentication-tgt-request-using-tgs-req"></a><details><summary>Suspicious Kerberos authentication (TGT request using TGS-REQ)</summary><br>**Description**:<br><br>A suspicious Kerberos ticket-granting service request (TGS-REQ) involving the Service for User to Self (S4U2self) extension was observed. This anomalous TGS request is suspected to have been specially crafted by an attacker. S4U2self is an extension that allows a service to obtain a Kerberos service ticket on behalf of another user, for itself. Successful authentication using this extension-when targeting the krbtgt service-can result in valid TGTs being issued on behalf of the targeted user.</details> | Medium | [T1550](https://attack.mitre.org/techniques/T1550), [T1558](https://attack.mitre.org/techniques/T1558) | xdr_SusKerberosAuth_S4U2selfTgsReq |

|<a name="suspicious-login-attempt-using-possibly-compromised-account-certificate"></a><details><summary>Suspicious login attempt using possibly compromised account certificate</summary><br>**Description**:<br><br>A suspicious login attempt using a possibly compromised account certificate has been observed. Previous attempts most likely have already occurred to steal or add the certificate to the service principal so the threat actor could use it in the future. The threat actor might have compromised the Entra service account certificate and used it for service principal account sign-in. If not mitigated, a compromised service principal account sign-in on an Entra service could lead to privilege escalation, account takeover, credential exposure, and unauthorized access to proprietary data and files.</details> | High | [T1649](https://attack.mitre.org/techniques/T1649) | xdr_SuspiciousLoginWithExchange |

|<a name="suspicious-network-connection-over-encrypting-file-system-remote-protocol"></a><details><summary>Suspicious network connection over Encrypting File System Remote Protocol</summary><br>**Description**:<br><br>A suspicious Encrypting File System Remote Protocol (EFSRPC) connection was observed from {SourceIpAddress}. This activity is associated with PetitPotam (CVE-2021-36942), where an attacker makes EFSRPC calls to a domain controller in an attempt to coerce NTLM authentication. If successfully exploited, it could allow credential theft and lateral movement. For more information about the vulnerability, see https://security.microsoft.com/intel-explorer/cves/CVE-2021-36942.</details> | Medium | [T1187](https://attack.mitre.org/techniques/T1187) | xdr_SuspiciousConnectionOverEFSRPC |

|<a name="suspicious-ntlm-authentication"></a><details><summary>Suspicious NTLM authentication</summary><br>**Description**:<br><br>One or more suspicious NTLM authentication attempts originating from the IP address {SourceIpAddress} have been detected. This anomalous NTLM authentication activity is suspected to have been specially crafted by an attacker, possibly as part of an attack involving a malicious tool. The attacker might also be using stolen credentials to carry out this attack. Anomalous NTLM behavior is commonly observed in various attack techniques, including pass-the-hash, reconnaissance, brute-force, remote code execution (RCE), and others.</details> | Medium | [T1550.002](https://attack.mitre.org/techniques/T1550/002), [T1087.002](https://attack.mitre.org/techniques/T1087/002) | xdr_SuspiciousNtlmAuthentication |

|<a name="suspicious-on-prem-account-enablement-after-disruption"></a><details><summary>Suspicious on-premises account enablement after disruption</summary><br>**Description**:<br><br>An account that was previously disabled as part of a disruption or containment action was subsequently re‑enabled. This behavior is highly suspicious and may indicate an attempt by a threat actor to restore access to a compromised identity or bypass containment measures.</details> | High | [T1098](https://attack.mitre.org/techniques/T1098) | xdr_SuspiciousAccountEnabled |

|<a name="suspicious-os-switch-sign-in"></a><details><summary>Suspicious OS switch sign-in</summary><br>**Description**:<br><br>An unexpected change in operating system is observed during a user sign‑in while the client profile remains consistent. Such shifts are uncommon for stable environments. This might indicate token replay, session hijacking, or authentication artifact reuse from a different platform. A potential identity compromise might be in progress through anomalous changes in the user’s device context. Go through the Recommended Action section to immediately investigate and mitigate associated risks.</details> | Medium | [T1078](https://attack.mitre.org/techniques/T1078) | xdr_SuspiciousOsSwitchSignIn |

|<a name="suspicious-sam-account-name-change"></a><details><summary>Suspicious SAM Account Name Change</summary><br>**Description**:<br><br>Detected a suspicious change of the SAM account name, which may indicate an attempt to exploit Kerberos authentication via NTP time manipulation (Timeroasting). This technique can allow attackers to brute-force or replay Kerberos tickets, leading to credential compromise and lateral movement.</details> | Medium | [T1110.001](https://attack.mitre.org/techniques/T1110/001), [T1558.003](https://attack.mitre.org/techniques/T1558/003) | xdr_SuspiciousChangeOfSamName |

|<a name="suspicious-sign-in-with-csrf-speedbump-trigger"></a><details><summary>Suspicious sign in with CSRF speedbump trigger</summary><br>**Description**:<br><br>Microsoft Entra ID detected a successful risky sign-in following CSRF (cross-site request forgery) speedbump trigger alert. This typically occurs when the sign-in flow deviates from expected browser behavior, such as session or cookie inconsistencies, missing or invalid forged tokens, or rapid automated request patterns.</details> | Medium | [T1557](https://attack.mitre.org/techniques/T1557), [T1185](https://attack.mitre.org/techniques/T1185) | xdr_CsrfSpeedbumpToRiskyLogin |

|<a name="user-exhibiting-spike-in-distinct-applicationresource-access-combinations"></a><details><summary>User exhibiting spike in distinct application‑resource access combinations</summary><br>**Description**:<br><br>A user account was observed interacting with an unusually high number of distinct cloud application‑resource combinations within a short time period and running uncommon cloud application actions. The observed activity corresponds to sign‑ins flagged as risky where multifactor authentication (MFA) was satisfied using a stored credential, and where the account password hasn't been updated recently. An increase in the diversity of accessed application‑resource combinations under these authentication conditions might reflect abnormal cloud service interaction patterns and should be reviewed.</details> | Medium | [T1087](https://attack.mitre.org/techniques/T1087) | xdr_SpikeAppResourceInSignIns |

|<a name="user-signin-from-shared-client-infrastructure-exhibiting-anomalous-activity"></a><details><summary>User sign‑in from shared client infrastructure exhibiting anomalous activity</summary><br>**Description**:<br><br>A suspicious shared client infrastructure activity has been observed. The suspicious sign‑in activity came from a client infrastructure with an unusual spike in distinct users and accessed resources. Repeated multifactor authentication (MFA) failures were followed by a successful MFA sign‑in, suggesting persistent authentication attempts from shared or automated infrastructure and potential account compromise. Go through the Recommended Action section to immediately investigate and mitigate associated risks.</details> | Medium | [T1078](https://attack.mitre.org/techniques/T1078) | xdr_SuspiciousSharedClientInfraActivity |

## Defense Evasion alerts

The following alerts indicate that a malicious actor might be attempting to evade detection in your organization.

| Security alert name | Severity | MITRE Technique | Detector ID |

|---|---|---|---|

|<a name="attempt-to-disable-defender-for-identity-service-principal-observed"></a><details><summary>Attempt to disable Defender for Identity service principal observed</summary><br>**Description**:<br><br>An actor attempted to disable or impair the security application responsible for generating identity and authentication alerts. This behavior is consistent with adversaries seeking to evade detection after initial access, maintain persistence, or disrupt monitoring by modifying, stopping, or uninstalling security services. Such activity often occurs following credential compromise, privilege escalation, or lateral movement.</details> | High | [T1562.001](https://attack.mitre.org/techniques/T1562/001) | xdr_SuspectedMDITampering |

|<a name="skipped-mfa-on-remembered-device-from-uncommon-isp-sign-in"></a><details><summary>Skipped MFA on remembered device from uncommon ISP sign-in</summary><br>**Description**:<br><br>A suspicious Microsoft Entra sign-in from an internet service provider (ISP) the account hasn't used in the past 30 days skipped multifactor authentication (MFA) on a remembered device. This indicates that an attacker might have used a stolen persistent cookie replayed from the attacker's infrastructure instead of the user's normal network. It's important to investigate and mitigate this urgently because skipped MFA could lead to potential security risks such as unauthorized access, session hijacking, and data breach.</details> | Medium | [T1550.004](https://attack.mitre.org/techniques/T1550/004), [T1078.004](https://attack.mitre.org/techniques/T1078/004) | xdr_SuspiciousMfaSkip |

|<a name="suspicious-access-denial-to-view-primary-group-id-of-an-object"></a><details><summary>Suspicious access denial to view primary group ID of an object</summary><br>**Description**:<br><br>An access control list (ACL) denied access to view the primary group ID of an object. An attacker might have compromised a user account and is looking to hide the group of a backdoor user.</details> | Medium | [T1564.002](https://attack.mitre.org/techniques/T1564/002) | xdr_SuspiciousDenyAccessToPrimaryGroupId |

|<a name="suspicious-account-link"></a><details><summary>Suspicious account link</summary><br>**Description**:<br><br>An account was linked through a cross tenant administrative action. The action was performed in a suspicious way that may indicate the account may be used in an attempt to bypass MFA.</details> | Medium | [T1556](https://attack.mitre.org/techniques/T1556) | xdr_SuspiciousAccountLink |

|<a name="suspicious-property-lock-deactivated-on-microsoft-entra-application"></a><details><summary>Suspicious property lock deactivated on Microsoft Entra application</summary><br>**Description**:<br><br>The servicePrincipalLockConfiguration.isEnabled property of a Microsoft Entra application or one of its associated service principals was modified. Disabling this lock removes essential built-in protections that guard against unauthorized credential rotation, redirect URI tampering, and illicit permission grants. Changes to this setting are rare during standard administrative operations and often signal suspicious activity. Threat actors can deliberately disable the lock to weaken the application's security posture, creating an opening for lateral movement or privilege escalation within the environment.</details> | Medium | [T1562.001](https://attack.mitre.org/techniques/T1562/001), [T1671](https://attack.mitre.org/techniques/T1671) | xdr_SuspiciousPropertyLockEntra |

## Discovery alerts

The following alerts indicate that a malicious actor might be attempting to gather information about your organization.

| Security alert name | Severity | MITRE Technique | Detector ID |

|---|---|---|---|

|<a name="anomalous-samr-activity-preview"></a><details><summary>Anomalous Samr activity (Preview)</summary><br>**Description**:<br><br>Anomalous Security Account Manager Remote (SAMR) protocol activity detected, indicating potential discovery attempts within the network. An attacker might be attempting to bypass security controls for discovery.</details> | Medium | [T1069](https://attack.mitre.org/techniques/T1069), [T1087](https://attack.mitre.org/techniques/T1087) | xdr_SamrReconnaissanceSecurityAlert |

|<a name="discovery-tool-was-observed"></a><details><summary>Discovery tool was observed</summary><br>**Description**:<br><br>A failed attempt to sign in to a user account by a tool used for discovery was detected. An attacker might be performing discovery activities in preparation for an attack.</details> | High | [T1087](https://attack.mitre.org/techniques/T1087) | xdr_DiscoveryToolObserved |

|<a name="okta-sync-service-principal-enumerated"></a><details><summary>Okta sync service principal enumerated</summary><br>**Description**:<br><br>A suspicious LDAP (Lightweight Directory Access Protocol) enumeration to find the Okta sync service account was detected. This behavior might indicate that a user account has been compromised and an attacker is using it to carry out malicious activities.</details> | High | [T1087.002](https://attack.mitre.org/techniques/T1087/002) | xdr_OktaSyncServicePrincipalEnumeration |

|<a name="possible-active-directory-certificate-services-enumeration"></a><details><summary>Possible Active Directory Certificate Services enumeration</summary><br>**Description**:<br><br>One or more potential Active Directory Certificate Services (AD CS) enumeration activities originating from the IP address {SourceIpAddress} have been detected. This enumeration might indicate an attacker's reconnaissance within the organization, potentially searching for AD CS vulnerabilities or misconfigurations, which could enable subsequent attack stages such as ESC techniques.</details> | Medium | [T1649](https://attack.mitre.org/techniques/T1649), [T1087](https://attack.mitre.org/techniques/T1087) | xdr_PossibleActiveDirectoryCertificateServicesEnumeration |

|<a name="possible-active-directory-enumeration-via-adws"></a><details><summary>Possible Active Directory enumeration via ADWS</summary><br>**Description**:<br><br>One or more potential Active Directory (AD) enumeration activities via Active Directory Web Services (ADWS) have been detected. This enumeration might indicate an attacker's reconnaissance within the organization, potentially enabling subsequent stages of attacks.</details> | Medium | [T1087.002](https://attack.mitre.org/techniques/T1087/002), [T1069.002](https://attack.mitre.org/techniques/T1069/002), [T1615](https://attack.mitre.org/techniques/T1615) | xdr_PossibleActiveDirectoryEnumerationAdws |

|<a name="possible-kerberoasting-ldap-reconnaissance"></a><details><summary>Possible Kerberoasting LDAP reconnaissance</summary><br>**Description**:<br><br>One or more suspicious Kerberoasting-related Lightweight Directory Access Protocol (LDAP) discovery activities originating from the IP address {SourceIpAddress} have been detected. This activity might indicate a potential Kerberoasting attack, where an attacker enumerates accounts with Service Principal Names (that is, Kerberoastable accounts) in Active Directory and then requests Kerberos service tickets for these accounts. The attacker then extracts and attempts to crack the encrypted tickets offline to obtain the plaintext passwords of those accounts. These targeted accounts might have been compromised, allowing the attacker to move laterally within the organization, escalate privileges, steal data, or set up backdoors for future access and persistence. Investigate immediately to mitigate the associated security risks.</details> | High | [T1087.002](https://attack.mitre.org/techniques/T1087/002), [T1558.003](https://attack.mitre.org/techniques/T1558/003) | xdr_PossibleKerberoastingLdapRecon |

|<a name="possible-spn-enumeration-via-adws"></a><details><summary>Possible SPN enumeration via ADWS</summary><br>**Description**:<br><br>One or more potential Service Principal Name (SPN) scanning activities via Active Directory Web Services (ADWS) have been detected. This enumeration might indicate an attacker's reconnaissance within the organization and could be used in attacks such as Kerberoasting.</details> | Medium | [T1087.002](https://attack.mitre.org/techniques/T1087/002) | xdr_PossibleSpnEnumerationAdws |

|<a name="possible-spn-enumeration-via-ldap"></a><details><summary>Possible SPN enumeration via LDAP</summary><br>**Description**:<br><br>One or more potential Service Principal Name (SPN) scanning activities via Lightweight Directory Access Protocol (LDAP), originating from the IP address {SourceIpAddress}, have been detected. This enumeration might indicate an attacker's reconnaissance within the organization and could be used in attacks such as Kerberoasting.</details> | Medium | [T1087.002](https://attack.mitre.org/techniques/T1087/002) | xdr_PossibleSpnEnumerationLdap |

|<a name="suspected-account-enumeration-kerberos-ntlm-ad-fs"></a><details><summary>Suspected account enumeration (Kerberos, NTLM, AD FS)</summary><br>**Description**:<br><br>Suspected account enumeration has been detected. A threat actor may have enumerated accounts in Active Directory to identify and map out weaknesses or vulnerabilities. If not mitigated, this activity can lead to serious security threats and data breach.</details> | Medium | [T1087.002](https://attack.mitre.org/techniques/T1087/002) | xdr_SuspectedAccountEnumeration |

|<a name="suspicious-addition-of-device-on-premises"></a><details><summary>Suspicious addition of device on-premises</summary><br>**Description**:<br><br>A suspicious addition of device on-premises has been observed. This could pose several risks such as compliance issues, unauthorized access to sensitive or confidential work-related data or intellectual property, malware or phishing attack, or data breach. Investigate immediately to mitigate associated security risks.</details> | High | [T1098.005](https://attack.mitre.org/techniques/T1098/005) | xdr_SuspiciousAdditionOfOnPremDevice |

|<a name="suspicious-entra-device-join-or-registration"></a><details><summary>Suspicious Entra device join or registration</summary><br>**Description**:<br><br>A user was suspiciously registered or joined into a new device to Entra, originating from an IP address identified by Microsoft Threat Intelligence. An attacker might have compromised the user account to perform persistence and lateral movement. Investigate immediately to mitigate associated security risks.</details> | High | [T1098.005](https://attack.mitre.org/techniques/T1098/005) | xdr_SuspiciousDeviceRegistration |

|<a name="suspicious-ldap-query"></a><details><summary>Suspicious LDAP query</summary><br>**Description**:<br><br>A suspicious Lightweight Directory Access Protocol (LDAP) query associated with a known attack tool was detected. An attacker might be performing reconnaissance for later steps.</details> | High | [T1087.002](https://attack.mitre.org/techniques/T1087/002) | xdr_SuspiciousLdapQuery |

|<a name="suspicious-ldap-query-targeting-sensitive-attributes"></a><details><summary>Suspicious LDAP query targeting sensitive attributes</summary><br>**Description**:<br><br>A suspicious LDAP query containing sensitive attributes that are uncommon for the source device has been detected in Active Directory. Attackers might be attempting to determine and plan their lateral movement in the domain. Active Directory LDAP attribute queries are used by attackers to gain critical information about the domain environment.</details> | Medium | [T1087.002](https://attack.mitre.org/techniques/T1087/002), [T1069.002](https://attack.mitre.org/techniques/T1069/002) | xdr_SuspiciousSensitiveAttributeLdapQuery |

|<a name="suspicious-server-message-block-smb-enumeration-from-untrusted-host"></a><details><summary>Suspicious Server Message Block (SMB) enumeration from untrusted host</summary><br>**Description**:<br><br>Suspicious SMB session enumeration targeting the MDI sensor. This indicates adversary reconnaissance aimed at identifying active user sessions on the host.</details> | Medium | [T1049](https://attack.mitre.org/techniques/T1049) | xdr_SmbSessionEnumeration |

## Execution alerts

The following alerts indicate that a malicious actor might be attempting to run malicious code in your organization.

| Security alert name | Severity | MITRE Technique | Detector ID |

|---|---|---|---|

|<a name="suspicious-remote-service-installation"></a><details><summary>Suspicious remote service installation</summary><br>**Description**:<br><br>A suspicious service installation was detected. This service was created to execute potentially malicious commands. An attacker might be using stolen credentials to leverage this attack. This might also indicate that a pass-the-hash attack was used.</details> | Medium | [T1569.002](https://attack.mitre.org/techniques/T1569/002) | xdr_SuspiciousRemoteServiceInstallation |

## Impact alerts

This section describes alerts indicating that a malicious actor might be attempting to manipulate, interrupt, or destroy your systems and data in your organization.

| Security alert name | Severity | MITRE Technique | Detector ID |

|---|---|---|---|

|<a name="suspicious-bulk-user-deletion-via-scripted-activity"></a><details><summary>Suspicious bulk user deletion via scripted activity</summary><br>**Description**:<br><br>A high volume of user deletion operations was detected from a single account within a short time window using a Python-based user agent. This behavior is consistent with an attacker using automated scripting to mass-delete user accounts after gaining administrative access, potentially causing widespread disruption to organizational identity infrastructure. Attackers may leverage stolen credentials or compromised service principals to delete users in bulk, disrupting business operations and removing evidence of previously compromised accounts.</details> | Medium | [T1531](https://attack.mitre.org/techniques/T1531) | None |

## Initial Access alerts

The following alerts indicate that a malicious actor might be attempting to gain initial access to your organization.

| Security alert name | Severity | MITRE Technique | Detector ID |

|---|---|---|---|

|<a name="failed-credential-abuse-attempt-in-entra-id-authentication"></a><details><summary>Failed credential abuse attempt in Entra ID authentication</summary><br>**Description**:<br><br>A failed authentication attempt was detected that aligns with patterns commonly associated with credential abuse or identity attacks. This activity may indicate an attempt to use advanced attack techniques targeting identity infrastructure.</details> | Low | [T1078.004](https://attack.mitre.org/techniques/T1078/004) | xdr_SuspiciousEntraFailedAuthentication |

|<a name="okta-anonymous-user-access"></a><details><summary>Okta anonymous user access</summary><br>**Description**:<br><br>Anonymous User access was detected.</details> | High | [T1078](https://attack.mitre.org/techniques/T1078) | xdr_OktaAnonymousUserAccess |

|<a name="password-spray-against-onelogin"></a><details><summary>Password spray against OneLogin</summary><br>**Description**:<br><br>A suspicious IP address attempted to authenticate to OneLogin using multiple valid accounts. An attacker might be attempting to find valid user account credentials for later follow-on behavior.</details> | Medium | [T1110.003](https://attack.mitre.org/techniques/T1110/003) | xdr_OneLoginPasswordSpray |

|<a name="potential-credential-abuse-in-entra-id-authentication"></a><details><summary>Potential credential abuse in Entra ID authentication</summary><br>**Description**:<br><br>A successful authentication attempt was detected that aligns with patterns commonly associated with credential abuse or identity attacks. This activity may indicate an attempt to use advanced attack techniques targeting identity infrastructure.</details> | High | [T1078.004](https://attack.mitre.org/techniques/T1078/004) | xdr_SuspiciousEntraAuthentication |

|<a name="suspicious-account-sign-in-and-configuration-changes"></a><details><summary>Suspicious account sign-in and configuration changes</summary><br>**Description**:<br><br>Suspicious sign-in and configuration changes have been observed from this account. This behavior might indicate that the user account was compromised and is being used for malicious activities.</details> | Low | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_SuspiciousSignInAndUserTampering |

|<a name="suspicious-entra-connect-account-authentication"></a><details><summary>Suspicious Entra Connect account authentication</summary><br>**Description**:<br><br>A suspicious authentication by an Entra Connect account originating from the IP address {SourceIpAddress} was detected. This authentication is anomalous because it does not match typical Entra Connect activity and is therefore suspected to originate from a non-Entra Connect server. This might indicate that the Entra Connect account has been compromised and is being used by an attacker to leverage its permissions for attacks such as DCSync.</details> | High | [T1078](https://attack.mitre.org/techniques/T1078), [T1556.007](https://attack.mitre.org/techniques/T1556/007) | xdr_SuspiciousEntraConnectAccountAuthentication |

|<a name="suspicious-entra-cookie-request-from-suspicious-ip-address"></a><details><summary>Suspicious Entra cookie request from suspicious IP address</summary><br>**Description**:<br><br>A successful sign-in originating from a threat intelligence (TI)-associated IP address attempted to request a Primary Refresh Token (PRT) cookie in Microsoft Entra. This activity may indicate an attacker-controlled host attempting to abuse PRT authentication.</details> | Medium | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_SuspiciousEntraSignIn |

|<a name="suspicious-entra-p2p-certificate-request-from-suspicious-ip-address"></a><details><summary>Suspicious Entra P2P certificate request from suspicious IP address</summary><br>**Description**:<br><br>A successful sign-in originating from a threat intelligence (TI)-associated IP address attempted to request a peer-to-peer (P2P) certificate in Microsoft Entra. This activity may indicate an attacker-controlled host attempting to abuse certificate-based authentication.</details> | Medium | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_SuspiciousEntraSignIn |

|<a name="suspicious-graph-api-request-made-from-entra-id-sync-application"></a><details><summary>Suspicious Graph API request made from Entra ID sync application</summary><br>**Description**:<br><br>An unexpected Graph API request made by Entra ID synchronization service application was detected. This behavior might indicate that the application was compromised and is being used for malicious activities. Go through the recommended actions to investigate immediately and mitigate associated risks.</details> | Medium | [T1087](https://attack.mitre.org/techniques/T1087), [T1069](https://attack.mitre.org/techniques/T1069) | xdr_SuspiciousConnectSyncProvisioningGraphAPIActivity |

|<a name="suspicious-okta-account-enumeration"></a><details><summary>Suspicious Okta account enumeration</summary><br>**Description**:<br><br>A suspicious IP address enumerated Okta accounts. An attacker might be attempting to perform discovery activities for later follow-on behavior.</details> | High | [T1078.004](https://attack.mitre.org/techniques/T1078/004) | xdr_SuspiciousOktaAccountEnumeration |

|<a name="suspicious-onelogin-mfa-fatigue"></a><details><summary>Suspicious OneLogin MFA fatigue</summary><br>**Description**:<br><br>A suspicious IP address sent several OneLogin multifactor authentication (MFA) challenge attempts for a user account. An attacker might have compromised the user's account credentials and is trying to flood and bypass the MFA mechanism.</details> | Medium | [T1110.003](https://attack.mitre.org/techniques/T1110/003) | xdr_OneLoginMfaFatigue |

|<a name="suspicious-sign-in-from-an-unusual-user-agent-and-ip-address"></a><details><summary>Suspicious sign-in from an unusual user agent and IP address</summary><br>**Description**:<br><br>A successful sign-in using an uncommon user agent and a potentially malicious IP address was detected in Microsoft Entra. This activity may indicate a password spray or credential stuffing attack originating from the attacker-controlled IP, or in rare cases, a compromised account being used for unauthorized access.</details> | Medium | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_SuspiciousEntraSignIn |

|<a name="suspicious-sign-in-from-an-unusual-user-agent-and-ip-address-using-device-code-flow"></a><details><summary>Suspicious sign-in from an unusual user agent and IP address using device code flow</summary><br>**Description**:<br><br>A successful sign-in was detected using an uncommon or atypical user agent combined with a potentially risky IP address. This pattern is frequently associated with password spray, credential stuffing, or other unauthorized authentication attempts originating from attacker-controlled infrastructure. In some cases, it may also indicate the use of compromised credentials for unauthorized access.</details> | Medium | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_SuspiciousEntraSignIn |

|<a name="suspicious-sign-in-from-an-unusual-user-agent-and-ip-address-using-powershell"></a><details><summary>Suspicious sign-in from an unusual user agent and IP address using PowerShell</summary><br>**Description**:<br><br>A successful sign-in was detected using an uncommon or atypical user agent combined with a potentially risky IP address. This pattern is frequently associated with password spray, credential stuffing, or other unauthorized authentication attempts originating from attacker-controlled infrastructure. In some cases, it may also indicate the use of compromised credentials for unauthorized access.</details> | Medium | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_SuspiciousEntraSignIn |

|<a name="suspicious-sign-in-made-to-an-admin-account"></a><details><summary>Suspicious sign-in made to an admin account</summary><br>**Description**:<br><br>An admin account sign-in was performed in a suspicious manner. This behavior might indicate that a user account was compromised and is being used for malicious activities.</details> | Low | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_SuspiciousAdminAccountSignIn |

|<a name="suspicious-sign-in-made-using-a-malicious-certificate"></a><details><summary>Suspicious sign-in made using a malicious certificate</summary><br>**Description**:<br><br>A user signed in to the organization using a malicious certificate. This behavior might indicate that a user account was compromised and is being used for malicious activities, and that a malicious domain with Azure AD Internals certificate is registered in the organization.</details> | High | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_SignInUsingMaliciousCertificate |

|<a name="suspicious-sign-in-observed-from-entra-id-sync-application"></a><details><summary>Suspicious sign-in observed from Entra ID sync application</summary><br>**Description**:<br><br>A suspicious sign-in from the Entra ID synchronization service application has been detected. This behavior might indicate that the application was compromised and is being used for malicious activities. Go through the recommended actions to investigate immediately and mitigate associated risks.</details> | Medium | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_SuspiciousConnectSyncProvisioningSignIn |

|<a name="suspicious-sign-in-observed-from-entra-id-sync-application-to-an-uncommon-resource-app"></a><details><summary>Suspicious sign-in observed from Entra ID sync application to an uncommon resource app</summary><br>**Description**:<br><br>A suspicious sign-in from the Entra ID synchronization service application to an uncommon resource application has been detected. This behavior might indicate that the application was compromised and is being used for malicious activities. Go through the recommended actions to investigate immediately and mitigate associated risks.</details> | Medium | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_SuspiciousConnectSyncProvisioningSignIn |

|<a name="suspicious-sign-in-observed-to-entra-id-sync-application-using-an-uncommon-user-agent"></a><details><summary>Suspicious sign-in observed to Entra ID sync application using an uncommon user agent</summary><br>**Description**:<br><br>A suspicious sign-in from the Entra ID synchronization service application using an uncommon user agent has been detected. This behavior might indicate that the application was compromised and is being used for malicious activities. Go through the recommended actions to investigate immediately and mitigate associated risks.</details> | Medium | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_SuspiciousConnectSyncProvisioningSignIn |

|<a name="suspicious-sign-in-to-a-web-app-following-mfa-phone-number-tampering-activity"></a><details><summary>Suspicious sign-in to a web app following MFA phone number tampering activity</summary><br>**Description**:<br><br>A suspicious sign-in to a web app was observed following configuration changes in a user account. This behavior might indicate that the user account was compromised and is being used for malicious activities.</details> | High | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_MfaPhoneNumberTamperingToSuspiciousWebAppSignIn |

|<a name="suspicious-sign-in-to-microsoft-sentinel-app-made-using-entra-id-sync-account"></a><details><summary>Suspicious sign-in to Microsoft Sentinel app made using Entra ID sync account</summary><br>**Description**:<br><br>A Microsoft Entra ID Connect sync account signed in to a Microsoft Sentinel resource in an unusual manner. This behavior might indicate that a user account was compromised and is being used for malicious activities.</details> | Low | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_SuspiciousMicrosoftSentinelAccessByEntraIdSyncAccount |

|<a name="suspicious-tool-used-by-a-microsoft-entra-sync-account"></a><details><summary>Suspicious tool used by a Microsoft Entra Sync account</summary><br>**Description**:<br><br>A suspicious authentication to a Microsoft Entra ID account typically used for syncing operations was detected. This behavior might indicate that a user account has been compromised and an attacker is using it to carry out malicious activities.</details> | High | [T1078.004](https://attack.mitre.org/techniques/T1078/004) | xdr_SuspiciousToolSyncAccountSignIn |

|<a name="suspicious-user-agent-sign-in-on-microsoft-entra"></a><details><summary>Suspicious user agent sign-in on Microsoft Entra</summary><br>**Description**:<br><br>A suspicious user agent signed-in on Microsoft Entra. This might indicate that the user account was compromised and is being used for malicious activities.</details> | Medium | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_SuspiciousEntraSignIn |

|<a name="suspicious-user-configuration-change-activity-from-entra-id-sync-application"></a><details><summary>Suspicious user configuration change activity from Entra ID sync application</summary><br>**Description**:<br><br>A suspicious user configuration change from the Entra ID synchronization service application has been observed. This behavior might indicate that the application was compromised and is being used for malicious activities. Go through the recommended actions to investigate and mitigate associated risks immediately.</details> | Medium | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_ConnectSyncProvisioningNonSyncActivity |

|<a name="sync-account-risky-sign-in-to-an-uncommon-app"></a><details><summary>Sync account risky sign-in to an uncommon app</summary><br>**Description**:<br><br>A Microsoft Entra ID Connect sync account that signed in to a risky session performed unusual activities. This behavior might indicate that a user account was compromised and is being used for malicious activities.</details> | High | [T1078.001](https://attack.mitre.org/techniques/T1078/001) | xdr_RiskyEntraIDSyncAccount |

## Lateral Movement alerts

The following alerts indicate that a malicious actor might be attempting to move between resources or identities in your organization.

| Security alert name | Severity | MITRE Technique | Detector ID |

|---|---|---|---|

|<a name="possible-authentication-silo-bypass"></a><details><summary>Possible authentication silo bypass</summary><br>**Description**:<br><br>A possible attempt to bypass authentication silo policies and authenticate against a silo-protected service was detected on this device.</details> | High | [T1550](https://attack.mitre.org/techniques/T1550) | xdr_PossibleAuthenticationSiloBypass |

|<a name="possible-takeover-of-a-microsoft-entra-seamless-sso-account"></a><details><summary>Possible takeover of a Microsoft Entra seamless SSO account</summary><br>**Description**:<br><br>A Microsoft Entra seamless SSO (single sign-on) account object, AZUREADSSOACC, was modified suspiciously. An attacker might be moving laterally from the on-premises environment to the cloud.</details> | High | [T1556](https://attack.mitre.org/techniques/T1556) | xdr_SuspectedAzureSsoAccountTakeover |

|<a name="suspected-pass-the-ticket-attack"></a><details><summary>Suspected pass-the-ticket attack</summary><br>**Description**:<br><br>A Pass-the-Ticket (PtT), also known as a ticket replay attack, has been detected on this account. A ticket for the account {SourceAccountName} originating from the device {TargetDeviceName} has been re-used on the device {DeviceName}. In this attack, a threat actor steals a valid Kerberos authentication ticket and reuses it to access other devices across the network. By replaying the stolen ticket, the threat actor can impersonate the user, move through the network, and escalate privileges without needing the account password.</details> | Medium | [T1550](https://attack.mitre.org/techniques/T1550) | xdr_PassTheTicketAttack |

|<a name="suspicious-activity-after-password-sync"></a><details><summary>Suspicious activity after password sync</summary><br>**Description**:<br><br>A user performed an uncommon action on an application after a recent password sync. An attacker might have compromised a user's account to perform malicious activities in the organization.</details> | Medium | [T1021.007](https://attack.mitre.org/techniques/T1021/007) | xdr_SuspiciousActivityAfterPasswordSync |

|<a name="suspicious-authentication-attempt"></a><details><summary>Suspicious authentication attempt</summary><br>**Description**:<br><br>A suspicious authentication attempt has been observed. This anomalous authentication request is suspected to have been specially crafted by an attacker. The attacker might be using stolen hash or clear text password for authentication, possibly leveraging pass-the-hash or over-pass-the-hash attack. Investigate immediately to protect the account and organization from security breach.</details> | Medium | [T1550.002](https://attack.mitre.org/techniques/T1550/002) | xdr_SuspiciousAuthAttempt |

|<a name="suspicious-kerberos-spn-request"></a><details><summary>Suspicious Kerberos SPN request</summary><br>**Description**:<br><br>A suspicious Kerberos SPN request has been observed. This anomalous request is suspected to have been specially crafted by an attacker. The attacker might be using stolen credentials from a compromised user and is leveraging them for a Kerberoasting attack.</details> | Medium | [T1558.003](https://attack.mitre.org/techniques/T1558/003) | xdr_SuspiciousAuthAttempt |

|<a name="suspicious-resource-based-constrained-delegation-rbcd-authentication"></a><details><summary>Suspicious resource-based constrained delegation (RBCD) authentication</summary><br>**Description**:<br><br>A Kerberos authentication pattern consistent with Resource-Based Constrained Delegation (RBCD) abuse was detected. The account '{DelegatingMachine}' requested a Kerberos service ticket to '{ServiceName}' while impersonating user '{SourceAccountName}' via delegation. RBCD abuse is a sophisticated attack technique that allows an attacker to impersonate users when accessing services hosted on a targeted account. This behavior might indicate an attacker's attempt to achieve lateral movement, privilege escalation, and establish persistence within the organization.</details> | Medium | [T1558](https://attack.mitre.org/techniques/T1558) | xdr_SuspiciousRBCDAuthentication |

|<a name="suspicious-smb-ntlm-authentication-attempt"></a><details><summary>Suspicious SMB NTLM authentication attempt</summary><br>**Description**:<br><br>A suspicious Server Message Block (SMB) NTLM (New Technology LAN Manager) authentication attempt was observed from {SourceIpAddress} IP address. An attacker might have specially-crafted this anomalous authentication request using stolen credentials. This might also indicate a pass-the-hash attack or a brute-force attack, a potential security breach, or compromise within your network.</details> | Medium | [T1021.002](https://attack.mitre.org/techniques/T1021/002) | xdr_SuspiciousSmbNtlmAuthenticationAttempt |

## Persistence alerts

The following alerts indicate that a malicious actor might be attempting to maintain a foothold in your organization.

| Security alert name | Severity | MITRE Technique | Detector ID |

|---|---|---|---|

|<a name="guest-user-account-promoted-to-member"></a><details><summary>Guest user account promoted to member</summary><br>**Description**:<br><br>A guest (external) user account was promoted to a member (internal) account. Guest accounts typically have restricted access, while member accounts are treated as internal users and may inherit broader permissions, access to resources, and eligibility for privileged roles. This can also be abused by adversaries to escalate privileges, bypass external access restrictions, or establish persistence within the tenant.</details> | Medium | [T1098](https://attack.mitre.org/techniques/T1098) | xdr_GuestToMemberPromotion |

|<a name="oauth-app-created-a-user"></a><details><summary>OAuth app created a user</summary><br>**Description**:<br><br>A new user account was created by an OAuth application. An attacker might have compromised this application for persistence in the organization.</details> | Medium | [T1136.003](https://attack.mitre.org/techniques/T1136/003) | xdr_OAuthAppCreatedAUser |

|<a name="okta-privileged-api-token-created"></a><details><summary>Okta privileged API token created</summary><br>**Description**:<br><br>{ActorAliasName} created an API token. If stolen, it can grant the attacker access with the user's permission.</details> | High | [T1078.004](https://attack.mitre.org/techniques/T1078/004) | xdr_OktaPrivilegedApiTokenCreated |

|<a name="okta-privileged-api-token-updated"></a><details><summary>Okta privileged API token updated</summary><br>**Description**:<br><br>{ActorAliasName} updated a Privileged API token Configuration to be more promiscuous. If stolen, it can grant the attacker access with the user's permission.</details> | High | [T1078.004](https://attack.mitre.org/techniques/T1078/004) | xdr_OktaPrivilegedApiTokenUpdated |

|<a name="reciprocal-temporary-access-pass-creation-between-users"></a><details><summary>Reciprocal Temporary Access Pass creation between users</summary><br>**Description**:<br><br>Two users created Temporary Access Passes (TAPs) for each other within a short time window. This behavior may indicate a compromised account establishing circular persistence by using TAP credentials and then removing traces of the temporary credential.</details> | High | [T1098](https://attack.mitre.org/techniques/T1098) | None |

|<a name="shadow-credentials-added-to-account"></a><details><summary>Shadow credentials added to account</summary><br>**Description**:<br><br>A shadow credential injection has been detected on the account. This could be an indication of persistence or lateral movement. Attackers inject shadow credentials to Active Directory (AD) accounts to gain or maintain access to the account they're hacking.</details> | High | [T1098](https://attack.mitre.org/techniques/T1098) | xdr_ShadowCredentialsAttack |

|<a name="shadow-credentials-added-to-account-and-used-for-authentication"></a><details><summary>Shadow Credentials Added to Account and Used for Authentication</summary><br>**Description**:<br><br>An account had shadow credentials injected into it, and they have been used for authentication. When this happens, attackers could bypass traditional credential theft methods to gain persistent access to a user account. Aside from persistence, this could also be an indication of lateral movement.</details> | High | [T1098](https://attack.mitre.org/techniques/T1098) | xdr_ShadowCredentialsAttack |

|<a name="suspicious-addition-of-acl-on-premises"></a><details><summary>Suspicious addition of ACL on-premises</summary><br>**Description**:<br><br>Suspicious addition of ACL on-premises has been observed. This can lead to unauthorized access, gaining elevated permissions, account and resource compromise, lateral movement, among others. Investigate immediately to mitigate associated security risks.</details> | High | [T1098](https://attack.mitre.org/techniques/T1098) | xdr_SuspiciousAdditionOfAcl |

|<a name="suspicious-addition-of-alternative-phone-number"></a><details><summary>Suspicious addition of alternative phone number</summary><br>**Description**:<br><br>A new alternative phone number was added for a user or users in a suspicious way. An attacker might have done this to manipulate multifactor authentication and leverage mobile phone authentication to fraudulently gain persistence in the organization.</details> | Medium | [T1556.006](https://attack.mitre.org/techniques/T1556/006) | xdr_SuspiciousMFAAddition |

|<a name="suspicious-addition-of-default-thirdparty-mfa-method-to-user-account"></a><details><summary>Suspicious addition of default third‑party MFA method to user account</summary><br>**Description**:<br><br>A new third‑party multifactor authentication method was set as the default for a user account. Changing the default MFA provider could allow sign‑ins to be approved outside of the organization’s standard authentication flow and might indicate account manipulation intended to persist access or weaken enforcement. Go through the Recommendation section to immediately investigate and mitigate associated risks.</details> | Medium | [T1556.006](https://attack.mitre.org/techniques/T1556/006) | xdr_Suspicious3rdPartyMfaAddition |

|<a name="suspicious-addition-of-email"></a><details><summary>Suspicious addition of email</summary><br>**Description**:<br><br>New email was added for multiple users in a suspicious way. An attacker might have done this to gain persistence in the organization.</details> | Medium | [T1556.006](https://attack.mitre.org/techniques/T1556/006) | xdr_SuspiciousMFAAddition |

|<a name="suspicious-change-to-primary-group-id"></a><details><summary>Suspicious change to primary group ID</summary><br>**Description**:<br><br>A user's primary group ID was modified. An attacker might have compromised a user account and assigned a backdoor user with strong permissions in the domain for later use.</details> | High | [T1098](https://attack.mitre.org/techniques/T1098) | xdr_SuspiciousChangeInUserPrimaryGroupId |

|<a name="suspicious-entra-device-join-or-registration"></a><details><summary>Suspicious Entra device join or registration</summary><br>**Description**:<br><br>A user was suspiciously registered or joined into a new device to Entra. An attacker might have compromised the user account to perform persistence and lateral movement. Investigate immediately to mitigate associated security risks.</details> | Medium | [T1098.005](https://attack.mitre.org/techniques/T1098/005) | xdr_SuspiciousAdditionOfEntraDevice |

|<a name="suspicious-entra-role-addition"></a><details><summary>Suspicious Entra role addition</summary><br>**Description**:<br><br>A user was suspiciously assigned to a sensitive role. An attacker might have compromised the user account to perform persistence and lateral movement. Investigate immediately to mitigate associated security risks.</details> | Medium | [T1098.003](https://attack.mitre.org/techniques/T1098/003) | xdr_SuspiciousAdditionOfRoleToUser |

|<a name="suspicious-guest-user-invitation"></a><details><summary>Suspicious guest user invitation</summary><br>**Description**:<br><br>A new guest user was invited and accepted in a suspicious way. An attacker might have compromised a user account in the organization and is using it to add an unauthorized user for persistence purposes.</details> | Medium | [T1136.003](https://attack.mitre.org/techniques/T1136/003) | xdr_SuspiciousGuestUserInvitation |

|<a name="suspicious-intune-device-registration-activity"></a><details><summary>Suspicious Intune device registration activity</summary><br>**Description**:<br><br>Microsoft Entra ID detected a potentially suspicious device registration attempt in Microsoft Intune. The device enrollment activity deviates from normal user or organizational behavior and may indicate unauthorized device onboarding or account misuse. Review the registering user, device details, location, and authentication context to confirm whether the registration was legitimate.</details> | Medium | [T1098.005](https://attack.mitre.org/techniques/T1098/005) | xdr_SuspiciousIntuneDeviceRegistration |

|<a name="suspicious-mfa-tampering-activity-by-admin-account"></a><details><summary>Suspicious MFA tampering activity by admin account</summary><br>**Description**:<br><br>An administrator account performed multifactor authentication (MFA) tampering activity after a risky authentication. An attacker might have compromised an admin account to manipulate MFA settings for possible lateral movement activity.</details> | Low | [T1556.006](https://attack.mitre.org/techniques/T1556/006) | xdr_AdminAccountTakeover |

|<a name="suspicious-removal-of-privileged-app-role-assignment-through-graph-api"></a><details><summary>Suspicious removal of privileged app role assignment through Graph API</summary><br>**Description**:<br><br>A privileged app role assignment was deleted through Microsoft Graph API. This activity might indicate unauthorized removal or modification of application privileges.</details> | High | [T1114](https://attack.mitre.org/techniques/T1114) | xdr_SuspiciousAppRoleAssignmentDeletion |

|<a name="suspicious-resource-based-constrained-delegation-rbcd-attribute-change"></a><details><summary>Suspicious resource-based constrained delegation (RBCD) attribute change</summary><br>**Description**:<br><br>One or more suspicious Resource-Based Constrained Delegation (RBCD)-related Active Directory (AD) attribute changes were detected. Such activity is often an initial step in RBCD attacks and might allow an attacker to impersonate users when accessing the targeted account affected by the RBCD attribute change. This behavior might indicate an attacker's attempt to achieve privilege escalation and establish persistence within the organization.</details> | Medium | [T1098](https://attack.mitre.org/techniques/T1098) | xdr_SuspiciousRbcdAttributeChange |

|<a name="suspicious-service-principal-sign-in-following-credential-addition"></a><details><summary>Suspicious service principal sign-in following credential addition</summary><br>**Description**:<br><br>Anomalous service principal sign-in to access {ResourceDisplayName} detected, shortly after new credentials are added. Such activity may indicate application persistence, unauthorized credential implantation, privilege escalation, or Service Principal compromise.</details> | Medium | [T1098.001](https://attack.mitre.org/techniques/T1098/001) | xdr_AnomalousSPNSignInAfterCredAddition |

|<a name="suspicious-signin-by-a-user-exhibiting-a-spike-in-account-update-activity"></a><details><summary>Suspicious sign‑in by a user exhibiting a spike in account update activity</summary><br>**Description**:<br><br>A user account that exhibited an unusual increase in account update operations, including changes to authentication methods such as the removal of multifactor authentication (MFA), was also observed performing a suspicious sign‑in activity. This pattern might indicate attempts to modify authentication settings or access the account in a manner consistent with unauthorized use.</details> | Medium | [T1098](https://attack.mitre.org/techniques/T1098) | xdr_SuspiciousSpikeUserUpdate |

|<a name="user-was-created-and-assigned-to-global-administrator-role"></a><details><summary>User was created and assigned to Global Administrator role</summary><br>**Description**:<br><br>A new user was created and assigned to Global Administrator role. An attacker might have compromised the user account to perform persistence and lateral movement.</details> | High | [T1136.003](https://attack.mitre.org/techniques/T1136/003), [T1098.003](https://attack.mitre.org/techniques/T1098/003) | xdr_SuspiciousUserCreationAndSensitiveRoleAssignment |

|<a name="user-was-created-and-assigned-to-sensitive-role"></a><details><summary>User was created and assigned to sensitive role</summary><br>**Description**:<br><br>A new user was created and assigned to a sensitive role. An attacker might have compromised the user account to perform persistence and lateral movement.</details> | Medium | [T1136.003](https://attack.mitre.org/techniques/T1136/003), [T1098.003](https://attack.mitre.org/techniques/T1098/003) | xdr_SuspiciousUserCreationAndSensitiveRoleAssignment |

## Privilege Escalation alerts

The following alerts indicate that a malicious actor might be attempting to gain higher-level permissions in your organization.

| Security alert name | Severity | MITRE Technique | Detector ID |

|---|---|---|---|

|<a name="anomalous-activity-following-global-administrator-elevation"></a><details><summary>Anomalous activity following Global Administrator elevation</summary><br>**Description**:<br><br>Anomalous behavior was observed on a user account around Global Administrator role elevation. The activity includes unusual Graph API patterns such as persistence, credential manipulation, policy changes, and reconnaissance, along with burst call behavior, failed access attempts, and risky sign-in events from unfamiliar locations or devices. This activity might indicate credential abuse, privilege escalation, backdoor creation, or compromise of the elevated Global Administrator account.</details> | Medium | [T1078.004](https://attack.mitre.org/techniques/T1078/004), [T1098](https://attack.mitre.org/techniques/T1098) | xdr_AnomalousGlobalAdminActivity |

|<a name="okta-privilege-escalation-following-anomalous-sign-in-by-actoraliasname"></a><details><summary>Okta privilege escalation following anomalous sign in by {ActorAliasName}</summary><br>**Description**:<br><br>An anomalous Okta sign in attempt (event {AnomalousLoginEventId}) at {AnomalousLoginTime} from IP address {IPAddress} was followed by privileged action {PrivilegedActionType} within the same session {SessionId} at {Timestamp}. Time delta between events: {DeltaSeconds}s.</details> | High | [T1110](https://attack.mitre.org/techniques/T1110), [T1548](https://attack.mitre.org/techniques/T1548) | xdr_OktaPrivilegeEscalationFollowingSignIn |

|<a name="okta-session-impersonation-leading-to-privileged-action-for-accountupn"></a><details><summary>Okta session impersonation leading to privileged action for {AccountUpn}</summary><br>**Description**:<br><br>An Okta impersonation session (event {ImpersonationStartEventId}) was initiated at {ImpersonateSessionTime} from IP address {IPAddress}. A privileged action {PrivilegedActionType} occurred within the same session {SessionId} at {Timestamp}. The time between events was {DeltaSeconds}s</details> | High | [T1548](https://attack.mitre.org/techniques/T1548), [T1134](https://attack.mitre.org/techniques/T1134) | xdr_OktaUserSessionImpersonationPrivilegedAction |

|<a name="risky-sign-in-followed-by-privilege-role-grant"></a><details><summary>Risky sign in followed by privilege role grant</summary><br>**Description**:<br><br>A user account flagged with a high risk Microsoft Entra sign in assessment was assigned to a high privilege directory role such as Global Administrator or Privileged Role Administrator shortly after logging in, using the Add member to role operation. This sequence strongly suggests a compromised credential followed by rapid privilege escalation.</details> | Medium | [T1078.004](https://attack.mitre.org/techniques/T1078/004), [T1098.003](https://attack.mitre.org/techniques/T1098/003) | xdr_RiskySignInFollowedByPrivilegedRoleGrant |

|<a name="suspected-certificate-enrollment-abuse-esc15"></a><details><summary>Suspected certificate enrollment abuse (ESC15)</summary><br>**Description**:<br><br>A certificate was enrolled suspiciously. An attacker might be using the ESC15 technique to exploit CVE-2024-49019 (https://msrc.microsoft.com/update-guide/vulnerability/CVE-2024-49019) and escalate privileges in the forest.</details> | High | [T1068](https://attack.mitre.org/techniques/T1068) | xdr_SuspectedCertificateEnrollmentESC15 |

|<a name="suspicious-addition-and-removal-of-elevated-privileges"></a><details><summary>Suspicious addition and removal of elevated privileges</summary><br>**Description**:<br><br>A high-privilege Entra ID role (for example, Global Administrator or Privileged Role Administrator) was granted to user or service principal and was quickly revoked after. This rapid role assignment and removal pattern is uncommon in regular administrative workflows and might indicate an attempt to evade detection during privilege escalation. Investigate this alert immediately to prevent or mitigate any unauthorized access, privilege escalation, and security breach.</details> | Medium | [T1078.004](https://attack.mitre.org/techniques/T1078/004) | xdr_SuspiciousAdditionAndRemovalOfPrivilegedRole |

|<a name="suspicious-entra-domain-addition-observed"></a><details><summary>Suspicious Entra domain addition observed</summary><br>**Description**:<br><br>A domain addition classified as suspicious by Microsoft Threat Intelligence has been observed.</details> | Medium | [T1484.002](https://attack.mitre.org/techniques/T1484/002) | xdr_SuspiciousEntraDomainAddition |

|<a name="suspicious-spn-was-added-to-a-user"></a><details><summary>Suspicious SPN was added to a user</summary><br>**Description**:<br><br>A suspicious service principal name (SPN) was added to a sensitive user. An attacker might be attempting to gain elevated access for lateral movement within the organization.</details> | High | [T1098](https://attack.mitre.org/techniques/T1098) | xdr_SuspiciousAdditionOfSpnToUser |


# Understanding Security Alerts

# View and Manage security alerts

The alerts queue shows a list of alerts that were flagged from identities in your network. By default, the queue displays alerts seen in the last seven days in a grouped view. The most recent alerts are shown at the top of the list helping you see the most recent alerts first.

## View the alerts queue

In the [Microsoft Defender portal](https://security.microsoft.com), go to **Incidents & alerts** and then to **Alerts**.

Alerts from the last seven days are displayed with the following information:

- Alert name

- Tags

- Severity

- Investigation state

- Status

- Category

- Detection source

- Impacted assets

- First activity

- Last activity

## Customize the view of the alerts queue

You can customize the view of the alerts queue in a few ways. Using the tools at the top of the page, you can:

- Customize the view to add or remove columns.

- Apply filters.

- Customize the duration. Display the alerts for a particular duration, such as 1 Day, 3 Days, 1 Week, 30 Days, and 6 Months.

- Export a detailed Excel report for analysis.

### Filter the alerts view

You can apply the following filters to get a more focused view of the alerts.

|Alert |Description  |

|---------|---------|

|**Severity**    |   Alert severity is based on several factors, including how much access the attacker might have, the potential impact if the attack succeeds, and the likelihood that the alert is a true positive. For a full list of alert types and their assigned severity levels, see [Security alert name mapping and unique external IDs](alerts-overview.md)     |

|**Status**    | You can choose to filter the list of alerts based on their Status. For example, you can filter to show only alerts that are **New**, **In Progress**, or **Resolved**.        |

|**Detection sources**    |  You can filter the alerts based on the following Detection sources:   **Microsoft Defender for Identity** or **Microsoft Defender XDR**     |

|**Tags**    | You can filter the alerts based on Tags assigned to alerts. |

### View an alert

You can access individual alerts from multiple locations, by selecting the alert name from any of the following:

- The **Alerts** page

- The **Incidents** page

- The **Identities** page

- The pages of individual **Devices**

- The **Advanced hunting** page

## The alerts page

The alerts page provides context into the alert, by combining attack signals and alerts related to the selected alert to construct a detailed alert story. The alerts page helps you quickly triage, investigate, and take effective action on alerts.

> [!NOTE]

> Microsoft Defender for Identity alerts currently appear in two different layouts in the Microsoft Defender portal.

> While the alert views show different information, all alerts are based on Defender for Identity collected data. The differences in layout and information shown are part of an ongoing transition to a unified alerting experience across Microsoft Defender products.

To view alerts from both Defender for Identity and Defender XDR, select **Filter**, then under **Service sources** choose **Microsoft Defender for Identity** and **Defender XDR**, and select **Apply**:

### Microsoft Defender for Identity alerts

At the top of the page, there are sections for the **Accounts**, **Destination Host**, and **Source Host** of the alert. Depending on the alert, you might see details about additional hosts, accounts, IP addresses, domains, and security groups. Select any of them to get more details about the entities involved.

- The **Alert story** section gives information to provide a complete story with the details of the alert. The alert story is divided into two sections:

- **What happened** includes the alert's timeline and the entities involved in the alert.

- **Alert graph** provides a visual representation of the alert, including the entities involved in the alert and their relationships. The graph helps you understand how the entities are connected and how they relate to the alert.

- **Important information** provides technical context that supports alert investigation. You can use this information to validate whether the activity was expected or suspicious and decide what actions to take to contain or escalate the incident.

- **Activity details** provides detailed information, including the timestamp, the base object, the search scope, and other details about the alert.

- The **details pane** on the right side of the page provides additional information about the alert, including the **Alert details**, **Comments & history**. The details pane also provides additional options, such as:

- Manage alert

- Export alert

- Move alert to another incident

- Classify an alert

### Microsoft Defender XDR alerts

At the top of the page, there are sections for the **Accounts**, **Destination Host**, and **Source Host** of the alert. Depending on the alert, you might see buttons for details about additional hosts, accounts, IP addresses, domains, and security groups. Select any of them to get more details about the entities involved.

- The **Alert story** section gives information to provide a complete story with the details of the alert. The alert story is divided into two sections:

- **What happened** includes the alert's timeline and the entities involved in the alert.

- The **details pane** on the right side of the page provides additional information about the alert, including the **Alert details**, **Comments & history**. The details pane also provides additional options, such as:

- Manage alert

- Move alert to another incident

- Classify an alert

## Manage security alerts

Selecting an alert opens the Alert management pane, where you can perform the following actions:

### Change the status of an alert

You can categorize alerts as New, In Progress, or Resolved by changing their status as your investigation progresses. This helps you organize and manage how your team can respond to alerts. For example, a team leader can review all New alerts, and decide to assign them to the In Progress queue for further analysis. The team leader might assign the alert to the Resolved queue if they know the alert is benign, or coming from a device that is irrelevant (such as one belonging to a security administrator), or is being dealt with through an earlier alert.

### Move an alert to another incident

You can create a new incident from the alert or link to an existing incident.

### Assign alerts

If an alert isn't yet assigned, you can select Assign to me to assign the alert to yourself.

### Add comments to an alert

You can add comments to an alert to provide additional context or information. This is useful for sharing insights with your team or documenting your investigation process.

Whenever a change or comment is made to an alert, it's recorded in the Comments and history section.

### Classify security alerts

For each alert, ask the following questions to determine the alert classification and help decide what to do next:

1. Is the security alert a TP, B-TP, or FP?

1. How common is this specific security alert in your environment?

1. Was the alert triggered by the same types of computers or users?

For example, servers with the same role or users from the same group/department? If the computers or users were similar, you might decide to exclude it to avoid extra future FP alerts.

Following proper investigation, all Defender for Identity security alerts can be classified as one of the following activity types:

- **True positive (TP)**: A malicious action detected by Defender for Identity.

- **Benign true positive (B-TP)**: An action detected by Defender for Identity that is real, but not malicious, such as a penetration test or known activity generated by an approved application.

- **False positive (FP)**: A false alarm, meaning the activity didn't happen.

> [!NOTE]

> An increase of alerts of the exact same type typically reduces the suspicious/importance level of the alert. For repeated alerts, verify configurations, and use security alert details and definitions to understand exactly what is happening that trigger the repeats.

### Tuning alerts

Tune your alerts to adjust and optimize them, reducing false positives. Alert tuning allows your SOC teams to focus on high-priority alerts and improve threat detection coverage across your system. In Microsoft Defender XDR, create rule conditions based on evidence types, and then apply your rule on any rule type that matches your conditions.

For more information, see [Tune an alert](/microsoft-365/security/defender/investigate-alerts#tune-an-alert).

## Related content

- [Investigate a user](/defender-for-identity/investigate-assets#investigation-steps-for-suspicious-users)

- [Investigate a computer](/defender-for-identity/investigate-assets#investigation-steps-for-suspicious-devices)


# Monitored Activities

# Microsoft Defender for Identity monitored activities

Microsoft Defender for Identity monitors information generated from your organization's Active Directory, network activities and event activities to detect suspicious activity. The monitored activity information enables Defender for Identity to help you determine the validity of each potential threat and correctly triage and respond.

In the case of a valid threat, or **true positive**, Defender for Identity enables you to discover the scope of the breach for each incident, investigate which entities are involved, and determine how to remediate them.

The information monitored by Defender for Identity is presented in the form of activities. Defender for Identity currently supports monitoring of the following activity types:

> [!NOTE]

> - This article is relevant for all Defender for Identity sensor types.

> - Defender for Identity monitored activities appear on both the user and machine profile page.

> - Defender for Identity monitored activities are also available in [Microsoft Defender XDR's Advanced Hunting](/defender-xdr/advanced-hunting-overview) page.

> [!TIP]

> For detailed information on all supported event types (`ActionType` values) in Advanced Hunting Identity-related tables, use the built-in schema reference available in Microsoft Defender XDR.

## Monitored user activities: User account AD attribute changes

|Monitored activity|Description|

|---------------------|------------------|

|Account Constrained Delegation State Changed|The account state is now enabled or disabled for delegation.|

|Account Constrained Delegation SPNs Changed|Constrained delegation restricts the services to which the specified server can act on behalf of the user.|

|Account Delegation Changed | Changes to the account delegation settings. |

|Account Disabled Changed|Indicates whether an account is disabled or enabled.|

|Account Expired|Date when the account expires.|

|Account Expiry Time Changed|Change to the date when the account expires.|

|Account Locked Changed|Changes to the account lock settings.|

|Account Password Changed|User changed their password.|

|Account Password Expired|User's password expired.|

|Account Password Never Expires Changed|User's password changed to never expire.|

|Account Password Not Required Changed|User account was changed to allow logging in with a blank password.|

|Account Smartcard Required Changed|Account changes to require users to log on to a device using a smart card.|

|Account Supported Encryption Types Changed|Kerberos supported encryption types were changed (types: Des, AES 129, AES 256).|

|Account Unlock changed | Changes to the account unlock settings. |

|Account UPN Name Changed|User's principal name was changed.|

|Group Membership Changed|User was added/removed, to/from a group, by another user or by themselves.|

|User Mail Changed|Users email attribute was changed.|

|User Manager Changed|User's manager attribute was changed.|

|User Phone Number Changed|User's phone number attribute was changed.|

|User Title Changed|User's title attribute was changed.|

## Monitored user activities: AD security principal operations

|Monitored activity|Description|

|---------------------|------------------|

|User Account Created|User account was created.|

|Computer Account Created|Computer account was created.|

|Security Principal Deleted Changed|Account was deleted/restored (both user and computer).|

|Security Principal Display Name Changed|Account display name was changed from X to Y.|

|Security Principal Name Changed|Account name attribute was changed.|

|Security Principal Path Changed|Account Distinguished name was changed from X to Y.|

|Security Principal Sam Name Changed|SAM name changed (SAM is the logon name used to support clients and servers running earlier versions of the operating system).|

## Monitored user activities: Domain controller based user operations

|Monitored activity|Description|

|---------------------|------------------|

|Directory Service Replication|User tried to replicate the directory service.|

|DNS Query|Type of query user performed against the domain controller (**AXFR**,**TXT**, **MX**, **NS**, **SRV**, **ANY**, **DNSKEY**).|

|gMSA Password retrieval | gMSA account password was retrieved by a user. <br> To monitor this activity, event 4662 must be collected. For more information, see [Configure Windows Event collection](configure-windows-event-collection.md).|

|LDAP Query | User performed an LDAP query.|

|Potential lateral movement |  A lateral movement was identified.|

|PowerShell execution | User attempted to remotely execute a PowerShell method.|

|Private Data Retrieval|User attempted/succeeded to query private data using LSARPC protocol.|

|Service Creation|User attempted to remotely create a specific service to a remote machine.|

|SMB Session Enumeration|User attempted to enumerate all users with open SMB sessions on the domain controllers.|

|SMB file copy|User copied files using SMB.|

|SAMR Query|User performed a SAMR query.|

|Task Scheduling|User tried to remotely schedule X task to a remote machine.|

|Wmi Execution|User attempted to remotely execute a WMI method.|

## Monitored user activities: Login operations

For more information, see [Supported logon types](/microsoft-365/security/defender/advanced-hunting-identitylogonevents-table#supported-logon-types) for the `IdentityLogonEvents` table.

## Monitored machine activities: Machine account

|Monitored activity|Description|

|---------------------|------------------|

|Computer Operating System Changed|Change to the computer OS.|

|SID-History changed | Changes to the computer SID history. |

## See Also

- [Managing security alerts](/defender-for-identity/manage-security-alerts)

- [Security alert guide](/defender-for-identity/alerts-overview)

- [Investigate assets](/defender-for-identity/investigate-assets)

- [Check out the Defender for Identity forum!](<https://aka.ms/MDIcommunity>)


# Nnr Policy

# Network Name Resolution (NNR) in Microsoft Defender for Identity

Network Name Resolution (NNR) is a key component of Microsoft Defender for Identity functionality. Defender for Identity captures activities based on network traffic, Windows events, and ETW. These activities normally contain IP data.

By using NNR, Defender for Identity can correlate raw activities that contain IP addresses with the relevant computers involved in each activity. Based on the raw activities, Defender for Identity profiles entities, including computers, and generates security alerts for suspicious activities.

## NNR with the Defender for Identity sensor v3.x

The Defender for Identity sensor v3.x automatically performs name resolution by using the Defender device inventory and events that the sensor collects, without needing to open extra ports in your environment.

## NNR with the Defender for Identity sensor v2.x

To resolve IP addresses to computer names, Defender for Identity sensors look up the IP addresses by using the following methods:

Primary methods:

- NTLM over RPC (TCP port 135)

- NetBIOS (UDP port 137)

- RDP (TCP port 3389) - only the first packet of **Client hello**

Secondary method:

- Queries the DNS server using reverse DNS lookup of the IP address (UDP 53)

For the best results, we recommend using at least one of the primary methods.

The sensor performs reverse DNS lookup of the IP address only when:

- There's no response from any of the primary methods.

- There's a conflict in the response received from two or more primary methods.

> [!NOTE]

> No authentication is performed on any of the ports.

Defender for Identity evaluates and determines the device operating system based on network traffic. After retrieving the computer name, the Defender for Identity sensor checks Active Directory and uses TCP fingerprints to see if there's a correlated computer object with the same computer name. Using TCP fingerprints helps identify unregistered and non-Windows devices, aiding in your investigation process.

When the Defender for Identity sensor finds the correlation, the sensor associates the IP to the computer object.

In cases where no name is retrieved, an **unresolved computer profile by IP** is created with the IP and the relevant detected activity.

NNR data is crucial for detecting the following threats:

- Suspected identity theft (pass-the-ticket)

- Suspected DCSync attack (replication of directory services)

- Network-mapping reconnaissance (DNS)

To improve your ability to determine if an alert is a **True Positive (TP)** or **False Positive (FP)**, Defender for Identity includes the degree of certainty of computer naming resolving into the evidence of each security alert.

For example, when computer names are resolved with  **high certainty** it increases the confidence in the resulting security alert as a **True Positive** or **TP**.

The evidence includes the time, IP, and computer name the IP was resolved to. When the resolution certainty is **low**, use this information to investigate and verify which device was the true source of the IP at this time.

After confirming the device, you can then determine if the alert is a **False Positive** or **FP**, similar to the following examples:

- Suspected identity theft (pass-the-ticket) – the alert was triggered for the same computer.

- Suspected DCSync attack (replication of directory services) – the alert was triggered from a domain controller.

- Network-mapping reconnaissance (DNS) – the alert was triggered from a DNS Server.

[![Evidence certainty.](media/nnr-high-certainty.png)](media/nnr-high-certainty.png#lightbox)

## Configuration recommendations

- NTLM over RPC:

- Check that TCP port 135 is open for inbound communication from Defender for Identity Sensors, on all computers in the environment.

- Check all network configuration, such as firewalls, as this can prevent communication to the relevant ports.

- NetBIOS:

- Check that UDP port 137 is open for inbound communication from Defender for Identity Sensors, on all computers in the environment.

- Check all network configuration, such as firewalls, as this can prevent communication to the relevant ports.

- RDP:

- Check that TCP port 3389 is open for inbound communication from Defender for Identity Sensors, on all computers in the environment.

- Check all network configuration, such as firewalls, as this can prevent communication to the relevant ports.

>[!NOTE]

>

> - Only one of these protocols is required, but we recommend using all of them.

> - Customized RDP ports aren't supported.

- Reverse DNS:

- Check that the Sensor can reach the DNS server and that Reverse Lookup Zones are enabled.

## Health issues

To ensure Defender for Identity works correctly and the environment is configured properly, Defender for Identity checks the resolution status of each sensor. It generates a health alert for each method and provides a list of the Defender for Identity sensors with a low success rate of active name resolution for each method.

When an observed IP address can't resolve to a computer name, Microsoft Defender for Identity records it as an unresolved computer entity. If these unresolved entities accumulate over time, the sensor’s active name resolution success rate decreases. This might trigger a low success rate of active name resolution health alert. This alert indicates reduced enrichment of network activity with device identity which might lower confidence in some detections. It doesn't indicate a sensor failure.

Each health alert provides specific details of the method, sensors, the problematic policy, and configuration recommendations. For more information about health issues, see [Microsoft Defender for Identity sensor health issues](health-alerts.md).

> [!NOTE]

> To disable an optional NNR method in Defender for Identity to fit the needs of your environment, open a support case.

## See Also

- [Defender for Identity sensor v2.x prerequisites](deploy/prerequisites-sensor-version-2.md) and [Defender for Identity sensor v3.x prerequisites](deploy/deploy-sensor-v3.md)

- [Configure event collection](deploy/configure-event-collection.md)


# Investigate Security Alerts

# Investigate alerts in Microsoft Defender for Identity

Investigate alerts that are affecting your environment, understand what they mean, and how to resolve them.

Begin your investigation by selecting an alert from the **Alerts** page in the Microsoft Defender portal. The alerts page displays a list of all security alerts generated by Defender for Identity, including their severity, status, and impacted assets. Selecting an alert opens the alert page, which contains the alert title, the affected assets, the details side pane, and in some cases, an alert story.

## Investigate using the alert story

The alert story provides a chronological view of the events related to the alert. It shows what happened, when it happened, and which entities were involved before and after the triggering event. It helps you follow the sequence of events and understand how the alert was generated.

The alert graph visually maps the users, devices, and domain controllers involved in the alert. It shows how these entities interacted, making it easier to identify relationships and patterns at a glance.

The Important information section includes additional technical details that support your investigation. It helps you understand what actions were taken, who initiated them, and where the activity originated. This section gives you raw evidence that can help validate the alert and guide your next steps.

Together, the alert story, alert graph, and Important information give you a complete picture of the alert. They help you understand what triggered the alert, which entities were involved, and whether the activity requires further investigation or action.

> [!NOTE]

> The **alert story** is only visible for alerts that use the classic Defender for Identity structure.

> For more information about differences in how alerts are presented in the Defender portal, see [View and manage alerts](understanding-security-alerts.md).

## Take action from the details pane

Once you've selected an alert of interest, the details pane changes to display information about the selected alert, historic information when it's available, and offer recommended actions to take action on this alert.

After completing your investigation, return to the selected alert, mark its status as Resolved, and classify it as either False alert or True alert. Classifying alerts helps tune this capability to provide more true alerts and less false alerts.

### Advanced security alert investigation

To get more details on a security alert, select **Export** on an alert details page to download the detailed Excel alert report.

> [!NOTE]

> The **export to Excel** option is also only available for alerts that use the classic Defender for Identity structure.

> For more information about differences in how alerts are presented in the Defender portal, see [View and manage alerts](understanding-security-alerts.md).

The downloaded file includes summary details about the alert on the first tab, including:

- Title

- Description

- Start Time (UTC)

- End Time (UTC)

- Severity – Low/Medium/High

- Status – Open/Closed

- Status Update Time (UTC)

- View in browser

All involved entities, including accounts, computers, and resources are listed, separated by their role. Details are provided for the source, destination, or attacked entity, depending on the alert.

Most of the tabs include the following data per entity:

- Name

- Details

- Type

- SamName

- Source Computer

- Source User (if available)

- Domain Controllers

- Accessed Resource: Time, Computer, Name, Details, Type, Service.

- Related entities: ID, Type, Name, Unique Entity Json, Unique Entity Profile Json

- All raw activities captured by Defender for Identity Sensors related to the alert (network or event activities) including:

- Network Activities

- Event Activities

Some alerts have extra tabs, such as details about:

- Attacked accounts when the suspected attack used Brute Force.

- Domain Name System (DNS) servers when the suspected attacked involved network mapping reconnaissance (DNS).

For example:

## How can I use Defender for Identity information in an investigation?

Investigations can be as detailed as needed. Here are some ideas of ways to investigate using the data provided by Defender for Identity.

### Related entities

In each alert, the last tab provides the **Related Entities**. Related entities are all entities involved in a suspicious activity, without the separation of the "role" they played in the alert. Each entity has two Json files, the Unique Entity Json and Unique Entity Profile Json. Use these two Json files to learn more about the entity and to help you investigate the alert.

<a name="unique-entity-json-file"></a>

#### Unique Entity JSON file format

The Unique Entity JSON file includes the data that Defender for Identity learned from Active Directory about the entity's account. This includes all attributes such as *Distinguished Name*, *SID*, *LockoutTime*, and *PasswordExpiryTime*. For user accounts, includes data such as *Department*, *Mail*, and *PhoneNumber*. For computer accounts, includes data such as *OperatingSystem*, *IsDomainController*, and *DnsName*.

<a name="unique-entity-profile-json-file"></a>

#### Unique Entity Profile JSON file format

The Unique Entity Profile JSON file includes all data that Defender for Identity profiled on the entity. Defender for Identity uses the network and event activities captured to learn about the environment's users and computers. Defender for Identity profiles relevant information per entity. This information contributes Defender for Identity's threat identification capabilities.

For more information about how to work with Defender for Identity security alerts, see [Working with security alerts](/defender-for-identity/understanding-security-alerts).

## Related content

- [Network Name Resolution in Microsoft Defender for Identity](nnr-policy.md)

- [Reconnaissance and discovery alerts](reconnaissance-discovery-alerts.md)

- [Persistence and privilege escalation alerts](persistence-privilege-escalation-alerts.md)


# Remediation Actions

# Remediation actions in Microsoft Defender for Identity

Applies to:

- Microsoft Defender for Identity

- Microsoft Defender XDR

Microsoft Defender for Identity allows you to respond to compromised users by disabling their accounts or resetting their password. After taking action on users, you can check on the activity details in the action center.

The response actions on users are available directly from the user page, the user side panel, the advanced hunting page, or in the action center.

## How remediation actions work

Remediation actions are initiated by a user in the Microsoft Defender portal and are authorized using role-based access control (RBAC) based on Microsoft Entra ID roles. If the initiating user isn’t authorized, the action is blocked before execution.

After authorization, the action is executed by the identity system that manages the affected account:

- **Active Directory**

Actions are executed by the Microsoft Defender for Identity sensor on the domain controller. Only sensors installed on domain controllers perform remediation actions; sensors on AD FS, AD CS, or Microsoft Entra Connect servers don't perform remediation actions. The sensor uses the domain controller's local system account to perform the action.

> [!IMPORTANT]

> Make sure the **Automatically use the sensor's local system account** option is selected. This is required for sensor v3.x and recommended for all environments, including mixed (v2.x and v3.x) deployments. To verify, in the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** > **Identities** > **Microsoft Defender for Identity** > **Manage action accounts**.

- **Microsoft Entra ID**

Microsoft Defender for Identity creates and uses a Microsoft‑managed enterprise application to execute remediation actions in Entra ID.

- **Application name:** *Microsoft Defender for Identity*. In older tenants, the application might appear with the name *Radius Aad Syncer*.

- **Application ID:** `60ca1954-583c-4d1f-86de-39d835f3e452`

- **Supported non‑Microsoft identity providers (IdPs)**

Actions are executed using the source IdP’s APIs based on the credentials configured for the integration.

Remediation actions are recorded by the identity system where the action is executed and are visible in Microsoft Defender audit logs.

## Remediation actions in Automatic Attack Disruption

Remediation actions can also be applied automatically by Microsoft Defender's automatic attack disruption. When an active attack is detected, attack disruption uses Defender for Identity remediation capabilities to contain the threat without manual intervention. For details, see [automatic attack disruption](/defender-xdr/automatic-attack-disruption).

## Supported actions

The following Defender for Identity actions can be performed on Identities.

Depending on your Microsoft Entra ID roles, you might see additional Microsoft Entra ID actions, such as requiring users to sign in again and confirming a user as compromised. For more information, see [Remediate risks and unblock users](/entra/id-protection/howto-identity-protection-remediate-unblock).

| Remediation Action | Description | Supported Identity systems |

| ------------------ | ----------- | ------ |

| Disable | Disables all accounts linked to an identity or a specific account. Disabling prevents sign-in and access to network resources until the accounts are re-enabled. This action doesn't delete the identity profile or associated data such as documents, calendar events, or email messages. | <ul><li>Active Directory</li><li>Microsoft Entra ID</li><li>Okta</li></ul> |

| Enable | Re-enables accounts that were previously disabled for the selected identity. | <ul><li>Active Directory</li><li>Microsoft Entra ID</li><li>Okta</li></ul> |

| Revoke session | Revokes active sessions for the selected identity. | <ul><li>Microsoft Entra ID</li><li>Okta</li></ul> |

| Mark as compromised | Marks all accounts linked to the selected identity as compromised in Microsoft Entra ID. | Microsoft Entra ID |

| Force password change | Forces a password change for one or more accounts linked to the selected identity. The user must change their password at next sign-in, which prevents further use of compromised credentials. | Active Directory |

| Deactivate | Permanently deactivates a non-legitimate malicious account. | Okta |

| Set account risk to High/Medium/Low | Sets account risk scoring to one of the defined levels. Available only when the [Risk Scoring](https://help.okta.com/en-us/Content/Topics/Security/Security_Risk_Scoring.htm) feature is enabled in Okta. | Okta |

## Roles and permissions

This table lists the remediation actions supported by Defender for Identity and the roles required to initiate each action.

| Remediation Action | Active Directory |Microsoft Entra ID | Okta |

| ---- | ---- | ---- | ---- |

| Disable | See [Required permissions Defender for Identity in Microsoft Defender XDR](/defender-for-identity/role-groups#required-permissions-defender-for-identity-in-microsoft-defender-xdr) | <ul><li>Global Administrator</li><li>User Administrator</li><li>Authentication Administrator</li><li>Privileged Authentication Administrator</li><li>Directory Writers</li></ul> | <ul><li>Security Operator</li><li>Security Administrator</li><li>Global Administrator</li></ul> |

| Enable | See [Required permissions Defender for Identity in Microsoft Defender XDR](/defender-for-identity/role-groups#required-permissions-defender-for-identity-in-microsoft-defender-xdr) |<ul><li>Global Administrator</li><li>User Administrator</li><li>Authentication Administrator</li><li>Privileged Authentication Administrator</li><li>Directory Writers</li></ul> |<ul><li>Security Operator</li><li>Security Administrator</li><li>Global Administrator</li></ul> |

| Revoke session | N/A |<ul><li>Global Administrator</li><li>User Administrator</li><li>Authentication Administrator</li><li>Privileged Authentication Administrator</li><li>Directory Writers</li><li>Helpdesk Administrator</li></ul> |<ul><li>Security Operator</li><li>Security Administrator</li><li>Global Administrator</li></ul> |

| Mark as compromised | N/A |<ul><li>Global Administrator</li><li>Security Administrator</li><li>Security Operator</li></ul> | N/A |

| Force password change | See [Required permissions Defender for Identity in Microsoft Defender XDR](/defender-for-identity/role-groups#required-permissions-defender-for-identity-in-microsoft-defender-xdr) | N/A | N/A |

| Deactivate | N/A | N/A |<ul><li>Security Operator</li><li>Security Administrator</li><li>Global Administrator</li></ul> |

| Set identity risk to High/Medium/Low | N/A | N/A |<ul><li>Security Operator</li><li>Security Administrator</li><li>Global Administrator</li></ul> |

> [!NOTE]

> There are some limitations for Microsoft Entra ID when performing certain actions on other roles. For more information, see the [Graph API documentation](/graph/api/resources/users?view=graph-rest-1.0&preserve-view=true).

## Prerequisites

To perform any of the [supported actions](#supported-actions), you need to:

- **Configure the account that Microsoft Defender for Identity uses to perform actions.** Make sure the **Automatically use the sensor's local system account** option is selected. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** > **Identities** > **Microsoft Defender for Identity** > **Manage action accounts**. This setting is required if any of your sensors are v3.x. For more information, see [Manage action accounts](deploy/manage-action-accounts.md).

- **Sign in to the Microsoft Defender portal with the required permissions.** For Defender for Identity actions, you'll need a custom role with **Response (manage)** permissions. For more information, see [Create custom roles with Microsoft Defender unified RBAC](/microsoft-365/security/defender/create-custom-rbac-roles). For details on the specific roles required for each action, see [Roles and permissions](#roles-and-permissions).

To apply a remediation action to an identity:

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to one of the following locations:

- **Identity page**: Go to **Assets** > **Identities**, and select the identity you want to act on.

- **Advanced hunting page**: Go to **Hunting** > **Advanced hunting**, and identify a result that includes an identity entity.

- **Action center**: Go to **Actions & submissions** > **Action center** to review and manage pending or completed actions.

1. Select **Actions** or right-click the identity to open the actions menu.

1. Select the remediation action you want to apply, such as **Disable**, **Revoke session**, or **Force password change**.

1. Confirm the action when prompted.

The action is submitted and executed by the relevant identity system. You can track the status in the **Action center**.

## Related video

- [Remediation actions in Microsoft Defender for Identity](https://learn-video.azurefd.net/vod/id/adc6068b-225c-457d-b053-db6b64dedb79)

## See also

[Microsoft Defender for Identity action accounts](deploy/manage-action-accounts.md)


# Role Groups

# Microsoft Defender for Identity role groups

Microsoft Defender for Identity offers role-based security to safeguard data according to your organization's specific security and compliance needs. We recommend that you use role groups to manage access to Defender for Identity, segregating responsibilities across your security team and granting only the amount of access that users need to do their jobs.

## Unified role-based access control (RBAC)

Users that are already have the [Security Administrators](/entra/identity/role-based-access-control/permissions-reference) on your tenant's Microsoft Entra ID are also automatically Defender for Identity administrator. Microsoft Entra Security Administrators don't need extra permissions to access Defender for Identity.

For other users, enable and use Microsoft 365 role-based access control (RBAC) to create custom roles and to support more Entra ID roles such as Security operator or Security Reader by default to manage access to Defender for Identity.

> [!IMPORTANT]

>Starting March 2, 2025, new Microsoft Defender for Identity tenants can only configure permissions through Microsoft Defender XDR [Unified Role-Based Access Control (RBAC)](/defender-xdr/manage-rbac). Tenants with roles assigned or exported before this date will retain their current configuration.

When creating your custom roles, make sure that you apply the permissions listed in the following table:

|Defender for Identity access level | Minimum required Microsoft 365 unified RBAC permissions      |

| ------------------------------------- | ------------------------------------------------------------ |

|**Administrators**                             | - `Authorization and settings/Security settings/Read` <br/>- `Authorization and settings/Security settings/All permissions` <br/> - `Authorization and settings/System settings/Read`<br/>- `Authorization and settings/System settings/All permissions`<br/> - `Security operations/Security data/Alerts (manage)`<br/> -`Security operations/Security data /Security data basics (Read)`<br/>- `Authorization and settings/Authorization/All permissions` <br> - `Authorization and settings/Authorization/Read` |

|**Users**                               | - `Security operations/Security data /Security data basics (Read)`<br/>- `Authorization and settings/System settings/Read`<br/>- `Authorization and settings/Security settings/Read`<br/>- `Security operations/Security data/Alerts (manage)`<br/>- `microsoft.xdr/configuration/security/manage` |

|**Viewers**                            | - `Security operations/Security data /Security data basics (Read)`<br/>- `Authorization and settings / System settings (Read and manage)` <br>- `Authorization and settings / Security setting (All permissions)` |

For more information, see [Custom roles in role-based access control for Microsoft Defender XDR](/microsoft-365/security/defender/custom-roles) and [Create custom roles with Microsoft Defender unified RBAC](/microsoft-365/security/defender/create-custom-rbac-roles).

> [!NOTE]

> Information included from the [Defender for Cloud Apps activity log](classic-mcas-integration.md#activities) may still contain Defender for Identity data. This content adheres to existing Defender for Cloud Apps permissions.

>

> Exception: If you have configured [Scoped deployment](/defender-cloud-apps/scoped-deployment) for Microsoft Defender for Identity alerts in Microsoft Defender for Cloud Apps, these permissions do not carry over and you will have to explicitly grant the Security operations \ Security data \ Security data basics (read) permissions for the relevant portal users.

## Required permissions Defender for Identity in Microsoft Defender XDR

The following table details the specific permissions required for Defender for Identity activities in [Microsoft Defender XDR](/microsoft-365/security/defender/microsoft-365-security-center-mdi).

| Activity      | Least required permissions                                      |

| ------------------- | ---------------------- |

| **Onboard Defender for Identity** (create workspace)   |  [Security Administrator](/entra/identity/role-based-access-control/permissions-reference) |

| **Configure Defender for Identity settings**      | One of the following Microsoft Entra roles:<br>- [Security Administrator](/entra/identity/role-based-access-control/permissions-reference)<br>- [Security Operator](/entra/identity/role-based-access-control/permissions-reference)<br> **Or** <br>The following [Unified RBAC permissions](#unified-role-based-access-control-rbac):<br />- `Authorization and settings/Security settings/Read`<br/>- `Authorization and settings/Security settings/All permissions`<br/>- `Authorization and settings/System settings/Read`<br/>- `Authorization and settings/System settings/All permissions` |

|**View Defender for Identity settings**      | Microsoft Entra roles:<br>- [Security Reader](/entra/identity/role-based-access-control/permissions-reference) <br> **Or** <br>The following [Unified RBAC permissions](#unified-role-based-access-control-rbac):<br />- `Authorization and settings/Security settings/Read` <br/>- `Authorization and settings/System settings/Read`|

|**Manage Defender for Identity security alerts and activities**                           | One of the following Microsoft Entra roles:<br>- [Security Operator](/entra/identity/role-based-access-control/permissions-reference)<br> **Or** <br>The following [Unified RBAC permissions](#unified-role-based-access-control-rbac):<br />- `Security operations/Security data/Alerts (Manage)`<br/>- `Security operations/Security data /Security data basics (Read)` |

| **View Defender for Identity security assessments** <br> (now part of Microsoft Secure Score) | [Permissions](/microsoft-365/security/defender/microsoft-secure-score#required-permissions) to access Microsoft Secure Score <br> **And** <br> The following [Unified RBAC permissions](#unified-role-based-access-control-rbac): `Security operations/Security data /Security data basics (Read)`|

|**View the Assets / Identities page**|[Permissions](/defender-cloud-apps/manage-admins) to access Defender for Cloud Apps <br> **Or** <br> One of the Microsoft Entra roles required by [Microsoft Defender XDR](/microsoft-365/security/defender/m365d-permissions) |

|**Perform Defender for Identity response actions** |A [custom role](/microsoft-365/security/defender/create-custom-rbac-roles) defined with permissions for **Response (manage)**<br> **Or** <br> One of the following Microsoft Entra roles:<br>- [Security Operator](/entra/identity/role-based-access-control/permissions-reference) |

## Defender for Identity security groups

> [!IMPORTANT]

> Starting March 2, Defender for Identity will no longer create Microsoft Entra ID security groups. Tenants can still configure the same permissions through  Microsoft Defender XDR [Unified Role-Based Access Control (RBAC)](/defender-xdr/manage-rbac)

Defender for Identity provides the following security groups to help manage access to Defender for Identity resources:

- **Azure ATP *(workspace name)* Administrators**

- **Azure ATP *(workspace name)* Users**

- **Azure ATP *(workspace name)* Viewers**

The following table lists the activities available for each security group:

|Activity |Azure ATP *(workspace name)* Administrators|Azure ATP *(Workspace name)* Users|Azure ATP *(Workspace name)* Viewers|

|----|----|----|----|

|**Change health issue status**|Available|Not available|Not available|

|**Change security alert status** (reopen, close, exclude, suppress)|Available|Available|Not available|

|**Delete workspace**|Available|Not available|Not available|

|**Download a report**|Available|Available|Available|

|**Sign in**|Available|Available|Available|

|**Share/Export security alerts** (via email, get link, download details)|Available|Available|Available|

|**Update Defender for Identity configuration** (updates)|Available|Not available|Not available|

|**Update Defender for Identity configuration** (entity tags, including both sensitive and honeytoken)|Available|Available|Not available|

|**Update Defender for Identity configuration** (exclusions)|Available|Available|Not available|

|**Update Defender for Identity configuration** (language)|Available|Available|Not available|

|**Update Defender for Identity configuration** (notifications, including both email and syslog)|Available|Available|Not available|

|**Update Defender for Identity configuration** (preview detections) |Available|Available|Not available|

|**Update Defender for Identity configuration** (scheduled reports) |Available|Available|Not available|

|**Update Defender for Identity configuration** (data sources, including directory services, SIEM, VPN, Defender for Endpoint)|Available|Not available|Not available|

|**Update Defender for Identity configuration** (sensor management, including downloading software, regenerating keys, configuring, deleting)|Available|Not available|Not available|

|**View entity profiles and security alerts**|Available|Available|Available|

## Add and remove users

Defender for Identity uses Microsoft Entra security groups as a basis for role groups.

Manage your role groups from [Groups management page](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/AllGroups) on the Azure portal. Only Microsoft Entra users can be added or removed from security groups.

## Assign Identity scoping

User Role-Based Access Control (URBAC) enables organizations to define custom roles that restrict visibility to specific Active Directory domains. Individuals assigned to these scoped roles will only see data, such as alerts, identities, and activities, related to the Active Directory domains included in their Defender XDR role assignment.

For more information, see: [Scoped access for Microsoft Defender for Identity](configure-scoped-access.md)

## Next step

> [!div class="step-by-step"]

> [Configure a Directory Service account for Microsoft Defender for Identity »](directory-service-accounts.md)


# Manage Related Identities Accounts

# Manage related identities and accounts in Microsoft Defender for Identity

In enterprise environments, identities are often fragmented. A single user might have multiple accounts across systems, including personal, privileged, legacy, cloud-based, or orphaned accounts. These accounts can cover on-premises Active Directory, Microsoft Entra ID, or non-Microsoft identity providers such as Okta and Ping.

Fragmentation makes it difficult to maintain a unified view of identity across the organization. Manually linking or unlinking related accounts in Microsoft Defender for Identity helps you:

- Correlate identity components across different systems.

- Improve protection by creating a complete identity context.

- Support investigations and response actions with unified identity views.

For example:

- **Personal and privileged accounts**: A user might have two accounts, one for everyday work and another with elevated permissions for administrative tasks. For example:

- `rick.hofer@contoso.onmicrosoft.com` (regular account)

- `rhofer@contoso.onmicrosoft.com` (privileged account)

- **Multiple domains**: Large organizations often manage several domains. Linking accounts across these domains provides full visibility into a user's activity. For example:

- `chris@fabrikam.com`

- `chris@contoso.com`

- **Personal and service accounts**: A user might have both a personal account and a service account they own or manage. Linking those accounts helps connect ownership and responsibility to the same identity. For example:

- `valeria.barrios@contoso.com`

- `backup.service@contoso.com`

- **Legacy accounts**: A user might still have an active account in a legacy system. Linking accounts ensures the legacy account is monitored and tied back to the correct identity. For example:

- `gabriela.laureano@contoso.com`

- `glaureano@contosolegacy.local`

- **Accounts in multiple services**: A user might have a Microsoft Entra ID account, an Okta account, and a Ping account. Manually linking these accounts to the user's identity creates a consolidated view that supports identity-centric protection and investigation.

Use the procedures in this article to manually link accounts to identities, and to manually unlink unused, legacy, or orphaned accounts from identities in Defender for Identity.

> [!NOTE]

> As Microsoft Defender moves toward a fully unified identity platform, some Defender for Cloud Apps data pipelines remain separate from the Identity inventory. Manual and policy-based identity correlations defined in the Identity inventory don't currently affect the following Defender for Cloud Apps features:

>

> - Built-in detections

> - UEBA (User and Entity Behavior Analytics)

> - Scoped deployment

> - Governance actions

> - Defender for Cloud Apps policies

> - Activity log

> - Cloud discovery user enrichment and anonymization

> - RBAC scoping

>

> The preceding features continue to use the Cloud Application Accounts inventory.

> [!TIP]

> To automatically correlate accounts using naming conventions, see [Create custom account correlation rules](custom-account-correlation-rules.md).

## Prerequisites

Before you begin, ensure that you meet the following requirement:

- You must have [Unified role-based access control (URBAC)](/defender-for-identity/role-groups) roles: Global Administrator or Security Data (Manage).

## Manually link accounts to an identity in Defender for Identity

Use the following steps to manually link accounts to an identity in Defender for Identity.

1. In the Microsoft Defender portal at <https://security.microsoft.com>, go to **Assets** \> **Identities**. Or, to go directly to the **Identity Inventory** page, use <https://security.microsoft.com/identity-inventory>.

1. On the **Identities** tab of the **Identity Inventory** page, select an identity from the list by clicking on the **Display name** value.

1. On the identity details page that opens, select the **Observed in organization** tab, and verify the **Accounts** tab is selected.

1. On the **Accounts** tab, select :::image type="icon" source="media/link-accounts.png" border="false"::: **Link**.

1. The **Link accounts** wizard opens. On the **Select accounts** page, use the search box to find an account. You can search by:

- Display name

- User principal name (UPN)

- Security identifier (SID)

- Source provider account

Select one account by selecting the check box next to the **Display name** column, and then select **Next**.

1. On the **Enter justification** page, enter a short explanation why you're linking these accounts. A valid explanation includes:

- Up to 50 characters.

- Letters, numbers, spaces, `@`, or `_`.

Select **Next**.

1. On the **Review and finish** page, review the information, and select **Back** to make changes. When you're finished, select **Submit**.

After the account is successfully linked, select **Done**

## Manually unlink legacy, orphaned, or unused accounts from an identity in Defender for Identity

Use the following steps to manually unlink legacy, orphaned, or unused accounts from an identity.

1. On the **Identities** tab of the **Identity Inventory** page at <https://security.microsoft.com/identity-inventory>, select an **Identity** from the list by clicking on the **Display name** value.

1. On the identity details page that opens, select the **Observed in organization** tab, and verify the **Accounts** tab is selected.

1. On the **Accounts** tab, select the account you want to unlink from the identity by selecting the check box next to the **Display name** column, and then select :::image type="icon" source="media/unlink-accounts.png" border="false"::: **Unlink**.

1. In the **Unlink accounts from ...** confirmation dialog that opens, read the information, and then select **Unlink accounts**.

## What to expect after linking or unlinking an account in Defender for Identity

After you link or unlink an account, the following changes occur:

- The selected accounts are linked or unlinked immediately.

- The system updates the identity context and refreshes the account list.

## See also

- [Investigate users](/microsoft-365/security/defender/investigate-users)

- [Investigate assets](/defender-for-identity/investigate-assets)


# Custom Account Correlation Rules

# Create custom account correlation rules (Preview)

Custom account correlation rules allow you to correlate accounts that don't share strong identifiers such as account ID, SID, object ID, or UPN. This is especially useful for privileged accounts with unique naming conventions. By defining custom policies, you get full visibility and better protection for all accounts.

## Prerequisites

- An active Microsoft Defender for Identity (MDI) license, or another license that includes MDI (such as E5). Without the required license, the policies page is read-only.

- At least one of the following roles to **view** policies:

- **Microsoft Entra ID roles**: Security Reader, Security Operator, or Security Administrator

- **Defender roles**: Security operations, Security data, Alerts (manage)

- One of the following roles to **create, edit, or remove** policies:

- **Microsoft Entra ID roles**: At least Security Administrator

- **Defender roles**: Security operations, Security data, Alerts (manage)

> [!TIP]

> Use the least-privileged role that meets your needs. If your organization uses [Microsoft Entra Privileged Identity Management (PIM)](/entra/id-governance/privileged-identity-management/pim-configure), request just-in-time role activation instead of permanent role assignments.

## Choose a correlation type

Before you create a rule, decide which correlation type fits your scenario. The following table describes the available options:

| Correlation type | Description | Example |

|---|---|---|

| **Root UPN Prefix** | Correlates accounts with matching prefixes before the '@' symbol. | `user@acme.com` and `adm_user@acme.com` share the prefix `user`. |

| **Root UPN Suffix** | Correlates accounts with matching suffixes after the '@' symbol. | `user@acme.com` and `user_svc@acme.com` share the suffix `@acme.com`. |

| **Domain UPN** | Correlates accounts across different domains with the same username. | `user@acme.com` and `user@contoso.com`. |

## Add a correlation rule

1. In the Microsoft Defender portal at [https://security.microsoft.com](https://security.microsoft.com), go to **Settings** > **Identities**.

1. Select **Account Correlation Rules**.

1. Select **Add Rule**.

1. In the wizard, enter a **Rule Name** (up to 50 characters). You can use letters, numbers, and the following special characters: `. - _ ! # ^ ~`.

1. Select the **Correlation Type** (Root UPN Prefix, Root UPN Suffix, or Domain UPN).

1. Enter the required values for the selected correlation type, such as prefixes, suffixes, or domains.

1. Review the summary, which includes the rule name, correlation type, and selected values.

1. Select **Submit** to create the rule. Correlation rule changes take effect within 12 hours.

## Edit a correlation rule

1. On the **Account Correlation Rules** page, select the checkbox next to the rule you want to edit. You can select only one rule at a time.

1. Select **Edit**.

1. In the wizard, update the rule configuration as needed.

1. Review your changes, and then select **Save**. Changes take effect within 12 hours.

## Remove a correlation rule

1. On the **Account Correlation Rules** page, select the checkbox next to the rule you want to remove.

1. Select **Delete**.

1. In the confirmation prompt, select **Remove** to confirm, or **Cancel** to abort. Correlation rule changes take effect within 12 hours.

## Related content

- [Manage related identities and accounts](/defender-for-identity/manage-related-identities-accounts)

- [View the identity inventory](/defender-for-identity/identity-inventory)


# Health Alerts

# Microsoft Defender for Identity health issues

The Microsoft Defender for Identity Health Issues page lists issues affecting your Defender for Identity deployment and sensors. It alerts you to detected problems that might result from configuration or environmental factors.

Configure [automatic Windows event auditing](deploy/configure-windows-event-collection.md) to help prevent issues related to Windows event collection.

## Health issues page

The Microsoft Defender for Identity **Health issues** page lets you know when there's a problem with your Defender for Identity workspace, by raising a health issue. You can see health issues for both your general Defender for Identity environment and specific sensors.

Defender for Identity supports the following types of health alerts:

- **Domain-related or aggregated health issues**, listed on the **Global health issues** tab

- **Sensor-specific health issues**, listed on the **Sensor health issues** tab

To access the page, follow these steps:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com)

1. Go to **Settings** > **Identities**.

1. Under **Deployment**, select **Health issues**.

1. Filter issues by status, issue name, or severity to help you find the issue you're looking for.

1. Select any issue for more details and the option to close or suppress the issue.

## Health issue status

Health issues in Microsoft Defender for Identity can have different statuses depending on their state and how they're handled.

- **Open:** The health issue is marked as open.

- **Closed:** A health issue is automatically marked as **Closed** when Microsoft Defender for Identity detects that the underlying issue is resolved. If you have the [Azure ATP (workspace name) Administrator](/defender-for-identity/role-groups#defender-for-identity-security-groups) role, you can also manually close a health issue.

- **Suppressed:** If you have Azure ATP (workspace name) Administrators permissions, you can suppress the health alert for seven days. Suppress a health alert if you're aware of an expected temporary known issue, for example, taking down a machine for maintenance.

For example, if a domain controller is taken offline for maintenance, a "Sensor stopped communicating" alert might be triggered. You can use the API to change the alert status from Open to Suppressed. After the domain controller is back online, revert the status to Open and let Microsoft Defender for Identity close the alert automatically when the issue is resolved.

<a name="health-issues"></a>

## Review health issue details

> [!NOTE]

> In some v3 sensor environments, health alerts about Windows event auditing might persist even when Windows auditing is correctly configured. This primarily occurs with manual auditing configuration, such as using Group Policy or PowerShell. The sensor remains healthy and detections aren't affected. To resolve, enable **Automatic Windows auditing configuration** in the Defender for Identity portal under **Settings** > **Advanced features**.

The tables in this section list all health issues by component, with causes and resolution steps.

Each health issue table includes a **Displayed in** column that indicates whether the issue appears on the **Sensor health issues** tab or the **Global health issues** tab.

|Alert|Description|Resolution|Severity|Displayed in|Supported by Sensor version|

|----|----|----|----|----|----|

|**Network configuration mismatch for sensors running on VMware**|The virtual machines that the listed Defender for Identity sensors is installed on has a network configuration mismatch. This issue might affect the performance and reliability of the sensors.|Review the network interface settings, including disabling the Large Send Offload (LSO), and follow the [VMware sensor network configuration instructions](https://aka.ms/mdi/vmware-sensor-issue).|High|Sensors health issues tab|2.x|

|**A domain controller is unreachable by a sensor**|The Defender for Identity sensor has limited functionality due to connectivity issues to the configured domain controller. This affects Defender for Identity's ability to detect suspicious activities related to domain controllers monitored by this Defender for Identity sensor.| Make sure the domain controllers are up and running and that this Defender for Identity sensor can open LDAP connections to them. In addition, in **Settings** make sure to configure a Directory Service account for every deployed forest.|Medium|Sensors health issues tab|2.x|

|**All/Some of the selected capture network adapters on the Defender for Identity sensor are disabled or disconnected**|Network traffic for some/all of the domain controllers is no longer captured by the Defender for Identity sensor. This issue affects the ability to detect suspicious activities, related to those domain controllers.|Make sure these selected capture network adapters on the Defender for Identity sensor are enabled and connected.|Medium|Sensors health issues tab|2.x|

|**Directory services user credentials are incorrect**|The credentials for the directory services user account are incorrect. This issue affects sensors' ability to detect activities using LDAP queries against domain controllers.|- For a **standard** AD accounts: Verify that the username, password, and domain in the **Directory services** configuration page are correct.<br>- For **group Managed Service Accounts:** Verify that the username and domain in the **Directory Services** configuration page are correct. Also check all the other **gMSA account** prerequisites described on the [Directory Service account recommendations](directory-service-accounts.md) page.<br>- For **v3.x sensors in environments with both v2 and v3 sensors:** DSA and gMSA credentials continue to be validated on all sensors, including v3 sensors, as long as a workspace-level DSA or gMSA exists. This is by design. V3 sensors ignore the DSA and gMSA for auditing and response actions, but credential validation occurs at the workspace level. To stop receiving this alert, remove the DSA or gMSA after all sensors are migrated to v3. For more information, see [DSA and gMSA health alerts in environments with both v2 and v3 sensors](deploy/deploy-sensor-v3.md#dsa-and-gmsa-health-alerts-in-environments-with-both-v2-and-v3-sensors). <br> - For information about gMSA password rotation and temporary credential alerts, see the **Directory services user credentials are incorrect** note at the end of this section.|Medium|Global health issues tab|All|

|**Low success rate of active name resolution**|The listed Defender for Identity sensors are failing to resolve IP addresses to device names more than 90% of the time using the following methods:<br />- NTLM over RPC<br />- NetBIOS<br />- Reverse DNS. This issue affects Defender for Identity's detections capabilities and might increase the number of false positive alarms.|- For NTLM over RPC: Check that port 135 is open for inbound communication from Defender for Identity sensors on all computers in the environment.<br />- For reverse DNS: Check that the sensors can reach the DNS server and that Reverse Lookup Zones are enabled.<br />- For NetBIOS: Check that port 137 is open for inbound communication from Defender for Identity sensors on all computers in the environment.<br />Additionally, make sure that the network configuration (such as firewalls) isn't preventing communication to the relevant ports.|Low|Sensors health issues tab and Global health issues tab|2.x|

|**No traffic received from domain controller**|No traffic was received from any domain controller via this Defender for Identity sensor. This issue might indicate that port mirroring from the domain controllers to the Defender for Identity sensor isn't configured yet or not working.|Verify that [port mirroring is configured properly on your network devices](deploy/configure-port-mirroring.md).<br></br>On the Defender for Identity sensor capture NIC, disable these features in Advanced Settings:<br></br>Receive Segment Coalescing (IPv4)<br></br>Receive Segment Coalescing (IPv6)|Medium|Sensors health issues tab and Global health issues tab|2.x|

|**Read-only user password to expire shortly**|The read-only user password, used to perform resolution of entities against Active Directory, is about to expire in less than 30 days. If the password for this user expires, all Defender for Identity sensors stop running and no new data is collected.|Change the domain connectivity password and then [update the Directory Service account](directory-service-accounts.md) password.|Medium|Global health issues tab|2.x|

|**Read-only user password expired**|The read-only user password, used to get directory data, expired. All Defender for Identity sensors stop running, or will stop running soon, and no new data is collected.|Change the domain connectivity password and then [update the Directory Service account](directory-service-accounts.md) password.|High|Global health issues tab|2.x|

|**Sensor outdated (v2)**|A Defender for Identity sensor is running a version that can't communicate with the Defender for Identity cloud infrastructure.|Manually update the sensor and check to see why the sensor isn't automatically updating. If this option doesn't work, download the latest sensor installation package and uninstall and reinstall the sensor. For more information, see [Download the Microsoft Defender for Identity sensor](download-sensor.md) and [Install the Microsoft Defender for Identity sensor](install-sensor.md).|Medium|Sensors health issues tab and Global health issues tab|2.x|

|**Sensor outdated (v3)**|A Defender for Identity sensor is running on a server that doesn't have the required Windows cumulative update to support the latest sensor capabilities.|Update the server with the latest Windows cumulative update and verify that updates are installed successfully. After updating, confirm in the Portal > Sensors page that the sensor version is up to date. For more information, review the [Defender for Identity v3.x sensor requirements](deploy/prerequisites-sensor-version-3.md).|Medium|Sensors health issues tab and Global health issues tab|3.x|

|**Sensor reached a memory resource limit**|The Defender for Identity sensor stopped itself and restarts automatically to protect the domain controller from a low memory condition. The Defender for Identity sensor enforces memory limitations upon itself to prevent the domain controller from experiencing resource limitations. This issue occurs when memory usage on the domain controller is high. Data from this domain controller is only partly monitored.|Increase the amount of memory (RAM) on the domain controller or add more domain controllers in this site to better distribute the load of this domain controller.|Medium|Sensors health issues tab|2.x|

|**Sensor service failed to start**|The Defender for Identity sensor service failed to start for at least 30 minutes. This issue can affect the ability to detect suspicious activities originating from domain controllers monitored by this Defender for Identity sensor.|Monitor Defender for Identity sensor logs to understand the root cause for Defender for Identity sensor service failure.|High|Sensors health issues tab|All|

|**Sensor stopped communicating**|There has been no communication from the Defender for Identity sensor. The default time span for this alert is 5 minutes. This issue indicates that the sensor failed to send data or a keep-alive signal to the Defender for Identity services for a period exceeding the allowed time. This issue typically suggests either a network issue in the environment that prevented data transmission or a server restart that took longer than the acceptable time frame, impacting Defender for Identity's ability to detect suspicious activities.|Check that the communication between the Defender for Identity sensor and Defender for Identity cloud service isn't blocked by any routers or firewalls.|Medium|Sensors health issues tab|All|

|**Some Windows events are not being analyzed**|The Defender for Identity sensor is receiving more events than it can process which causes some Windows events aren't being analyzed. This issue can affect the ability to detect suspicious activities originating from domain controllers monitored by this Defender for Identity sensor.|Consider [adding more processors and memory](capacity-planning.md) as required. If you're using a standalone Defender for Identity sensor, verify that only the required events are forwarded to the sensor. Or, try forwarding some events to another Defender for Identity sensor.|Medium|Sensors health issues tab and Global health issues tab|2.x|

|**Some network traffic could not be analyzed**|The Defender for Identity sensor is receiving more network traffic than it can process which causes some network traffic couldn't be analyzed. This issue can affect the ability to detect suspicious activities originating from domain controllers monitored by this Defender for Identity sensor.|Consider [adding more processors and memory](capacity-planning.md) as required. If you're using a standalone Defender for Identity sensor, reduce the number of domain controllers being monitored.<br></br>This issue can also happen if you're using domain controllers on VMware virtual machines. To avoid these issues, you can check that the following settings are set to **0** or **Disabled** in the virtual machine (in the Windows OS, not in the VMware settings):<br></br>- **Large Send Offload V2 (IPv4)**<br></br>- **IPv4 TSO Offload**<br></br>The names can vary depending on your VMware version. For more information, see your VMware documentation.|Medium|Sensors health issues tab and Global health issues tab|2.x|

|**Some ETW events are not being analyzed**|The Defender for Identity sensor is receiving more Event Tracing for Windows (ETW) events than it can process which causes some Event Tracing for Windows (ETW) events aren't being analyzed. This issue can affect the ability to detect suspicious activities originating from domain controllers monitored by this Defender for Identity sensor.|Consider [adding more processors and memory](capacity-planning.md) as required.|Medium|Sensors health issues tab and Global health issues tab|2.x|

|**Sensor running on an operating system that will soon become unsupported**|The Defender for Identity sensor is running on an operating system that will soon become unsupported. Windows Server 2012 and 2012 R2 reached end of support on October 10, 2023. More details can be found at: <https://aka.ms/mdi/oseos> |The operating system on the server should be upgraded to the latest supported operating system. For more information, see [Minimum operating system requirements](deploy/prerequisites-sensor-version-2.md#minimum-operating-system-requirements).|Medium|Sensors health issues tab|2.x|

|**Sensor running on an unsupported operating system**|The Defender for Identity sensor is running on an unsupported operating system. Windows Server 2012 and 2012 R2 reached end of support on October 10, 2023. More details can be found at: <https://aka.ms/mdi/oseos> |The operating system on the server should be upgraded to the latest supported operating system. For more information, see [Minimum operating system requirements](deploy/prerequisites-sensor-version-2.md#minimum-operating-system-requirements).|High|Sensors health issues tab|All|

|**Sensor has issues with packet capturing component**|The Defender for Identity sensor is using WinPcap drivers instead of Npcap drivers. All customers should be using Npcap drivers instead of the WinPcap drivers. Starting with Defender for Identity version 2.184, the installation package installs Npcap 1.0 OEM.|Install Npcap according to the guidance as described in: <https://aka.ms/mdi/npcap>|High|Sensors health issues tab|2.x|

|**Sensor has issues with packet capturing component**|The Defender for Identity sensor is running an Npcap version older than the minimum required version. The minimum Npcap version supported is 1.0. Starting with Defender for Identity version 2.184, the installation package installs Npcap 1.0 OEM.|Upgrade Npcap according to the guidance as described in: <https://aka.ms/mdi/npcap>|Medium|Sensors health issues tab|2.x|

|**Sensor has issues with packet capturing component**|The Defender for Identity sensor is running an Npcap component that isn't configured as required. The Npcap installation is missing the required configuration options.|Install Npcap according to the guidance as described in: <https://aka.ms/mdi/npcap>|High|Sensors health issues tab|2.x|

|**NTLM Auditing is not enabled**|NTLM Auditing (for event ID 8004) isn't enabled on the server. (This configuration is validated once a day, per sensor.)|Enable NTLM Auditing events according to the guidance as described at the [Event ID 8004](configure-windows-event-collection.md#configure-ntlm-auditing) section, in the [Configure Windows Event collection](configure-windows-event-collection.md) page.|Medium|Sensors health issues tab|All|

|**Directory Services Advanced Auditing is not enabled as required**|The Directory Services Advanced Auditing configuration doesn't include all the categories and subcategories as required. (This configuration is validated once a day, per sensor.)|Enable the Directory Services Advanced Auditing events. For more information, see [Configure audit policies for Windows event logs](configure-windows-event-collection.md).|Medium|Sensors health issues tab|All|

|**Directory Services Object Auditing is not enabled as required**|The Directory Services Object Auditing configuration doesn't include all the object types and permissions as required. (This configuration is validated once a day, per domain.)|Enable the Directory Services Object Auditing events according to the guidance as described in the [Configure domain object auditing](configure-windows-event-collection.md#configure-domain-object-auditing) section, in the [Configure Windows Event collection](configure-windows-event-collection.md) page.|Medium|Global health issues tab|All|

|**Auditing on the Configuration container is not enabled as required**|The Directory Services Auditing on the Domain's Configuration container isn't enabled as required. (This configuration is validated once a day, per domain.)|Enable the Directory Services Auditing on the Domain's Configuration container according to the guidance as described in the [Configure Audit Policies](configure-windows-event-collection.md#enable-auditing-on-an-exchange-object) section, in the [Configure Windows Event collection](configure-windows-event-collection.md) page.|Medium|Global health issues tab|All|

|**Auditing on the ADFS container is not enabled as required**|The Directory Services Auditing on the ADFS container isn't enabled as required. (This configuration is validated once a day, per domain.)|Enable the Directory Services Auditing on the ADFS container according to the guidance as described in the [Configure auditing on an Active Directory Federation Services (AD FS)](configure-windows-event-collection.md#configure-auditing-on-an-active-directory-federation-services-ad-fs) section, in the [Configure Windows Event collection](configure-windows-event-collection.md) page.|Medium|Global health issues tab|All|

|**Power mode isn't configured for optimal processor performance**|The operating system's power mode isn't configured to the optimal processor performance settings. (This configuration is validated once a day, per sensor.) This issue can affect the server's performance and the sensors' ability to detect suspicious activities.|Do one of the following: <br><br>- Configure the power option of the machine running the Defender for Identity sensor to *High Performance*<br>- Set both the minimum and maximum processor state to *100*<br><br>For more information, see the [Server requirements](deploy/prerequisites-sensor-version-2.md#server-requirements) section in the [Defender for Identity prerequisites](deploy/prerequisites-sensor-version-2.md) page.|Low|Sensors health issues tab|2.x|

|**Sensor failed to write to the custom log path**|The custom log path provided in the sensor configuration can't be created.|1. Stop the `AATPSensorUpdater` and `AATPSensor` services. <br>2. Change the `SensorCustomLogLocation` in the sensor configuration file to a valid path or set it to null. <br>3. Start the `AATPSensorUpdater` and `AATPSensor` services again.|Low|Sensors health issues tab|2.x|

|**Radius accounting (VPN integration) data ingestion failures**|The listed Defender for Identity sensors have radius accounting (VPN integration) data ingestion failures.|Validate that the shared secret in the Defender for Identity configuration settings matches your VPN server, according to the guidance described [Configure VPN in Defender for Identity](vpn-integration.md#configure-vpn-in-defender-for-identity) section, in the [Defender for Identity VPN integration](vpn-integration.md) page.|Low|Health issues page|2.x|

|**Auditing for AD CS servers isn't enabled as required**|The Advanced Auditing Policy Configuration or AD CS auditing isn't enabled as required. (This configuration is validated once a day, per sensor.)|Enable the Advanced Auditing Policy Configuration and AD CS auditing according to the guidance as described in the [Configure auditing on AD CS](configure-windows-event-collection.md#configure-auditing-on-ad-cs) section, in the [Configure Windows Event collection](configure-windows-event-collection.md) page.|Medium|Sensors health issues tab|2.x|

|**Sensor failed to retrieve Microsoft Entra Connect service configuration**|The sensor is unable to retrieve the configuration from the Microsoft Entra Connect service (also known as Microsoft Azure AD sync).|Ensure that the Microsoft Entra connect service **(Microsoft Azure AD Sync)** is running and follow the instructions in [Configure permissions for the Microsoft Entra Connect (ADSync) database](deploy/active-directory-federation-services.md#configure-permissions-for-the-microsoft-entra-connect-adsync-database) to grant the sensor the necessary permissions. If the issue persists, follow the troubleshooting guidance at [SQL connectivity issues with Microsoft Entra Connect](/entra/identity/hybrid/connect/tshoot-connect-tshoot-sql-connectivity).|Medium|Sensors health issues tab|2.x|

|**Sensor v3.x RPC Audit Misconfigured**|The sensor is missing the required Unified Sensor RPC Audit configuration tag, or the tag was not applied correctly.|This issue affects the sensor’s ability to enable enhanced RPC auditing, which is required for certain advanced identity detections on V3.x sensors. Without this configuration, some identity-based detections might not function, reducing Defender for Identity’s visibility into suspicious activities. Verify that the Unified Sensor RPC Audit configuration is correctly applied to the relevant devices by following the instructions at [Configure RPC auditing](deploy/deploy-sensor-v3.md#configure-rpc-auditing). Once the tag is applied, the configuration is enforced automatically on matching devices, restoring full detection capability.|Medium|Sensors health issues tab|3.x|

>[!NOTE]

> **Directory services user credentials are incorrect:**

> Automatic group managed service account (gMSA) password rotation can temporarily trigger directory credential-related health alerts. During password rotation, a sensor might briefly fail to authenticate until it retrieves the updated gMSA password.

> These alerts are expected to resolve automatically after the sensor successfully updates its credentials. If the alert closes automatically and does not reoccur, no manual remediation is required. Administrators should verify that the gMSA is correctly configured and that the affected sensor returns to a healthy state.

>

> In environments with both v2 and v3 sensors, DSA and gMSA credentials continue to be validated on all sensors in the workspace as long as those accounts are configured, regardless of sensor version. V3 sensors ignore the DSA and gMSA for auditing and response actions, but the workspace-level credential validation still includes them. To stop receiving this alert on v3 sensors, remove the DSA or gMSA after all sensors are migrated to v3 and no v2 sensors require it. For more information, see [DSA and gMSA health alerts in environments with both v2 and v3 sensors](deploy/deploy-sensor-v3.md#dsa-and-gmsa-health-alerts-in-environments-with-both-v2-and-v3-sensors).

## See also

- [Work with Defender for Identity's Identity Security dashboard](dashboard.md)

- [Defender for Identity community forum](https://aka.ms/MDIcommunity)


# Security Testing Best Practices

# Best Practices before Offensive Security Testing for Microsoft Defender for Identity

This article summarizes the best practices and items to review before you begin Offensive Security Testing for Microsoft Defender for Identity.

## Common issues that affect testing

Here are some common issues that can affect your offensive security testing:

### Infrastructure protection issues

- **Incomplete infrastructure protection**: Deploy Microsoft Defender for Identity sensors on all domain controllers.

- **Missing Microsoft Defender for Endpoint**: Endpoint protection adds detection capabilities for activities on identity infrastructure that may not be covered by identity-based detections alone.

### Detection accuracy issues

- **Insufficient learning period**: The learning period for alerts is used to tune alert detections. Without this learning period, detections won't be as accurate.

- **Using accounts with established admin patterns**: Avoid using users or computers that regularly run administrative tasks, as the system learns these as normal behavior. Instead, use:

- **Existing computer**: Use a computer that doesn't regularly run admin or attack simulation activities.

- **Existing standard user**: Use a user that doesn't regularly run admin or attack simulation activities.

### Configuration issues

- **Network configuration mismatch**: Sensors running on VMware might experience Microsoft Defender for Identity health issues. See [VMware virtual machine sensor issue](troubleshooting-known-issues.md#vmware-virtual-machine-sensor-issue).

- **Unhealthy Network Name Resolution (NNR)**: This issue can lead to problems with certain detections.

- **Incomplete attack simulation**: Test with actual attack scenarios rather than single TTPs. Defender for Identity detections focus on complete attack stories. Performing only one segment of a kill chain without other steps yields incomplete results and decreased detection outcomes.

- **Incompatible penetration testing tools**: Some tools might return false results. Cross-check relevant audit logs to confirm successful attacks.

## Best practices checklist

|Recommendation |Description  |Links to Documentation for related tasks  |

|---------|---------|---------|

|Check that Defender for Identity is deployed on all domain controllers  |Deployment on all domain controllers ensures that you're getting all of the signals for threat detection. Not having full protection can lead to missed detections or false positives.   |[Microsoft Defender for Identity deployment overview](deploy/deploy-defender-identity.md)   |

|Check that Defender for Identity is deployed on all AD FS, AD CS, and Microsoft Entra Connect servers     |Deployment on all these servers ensures that you're getting all of the signals for threat detection. Not having full protection can lead to missed detections or false positives.| [Configure sensors for AD FS, AD CS, and Microsoft Entra Connect](deploy/active-directory-federation-services.md)  |

|Check the health of your Defender for Identity sensors     |It's critical that your sensor is healthy and reporting as expected to ensure optimal performance. Having an unhealthy sensor can lead to missed detections. Review all health alerts before running any tests.  |[Microsoft Defender for Identity health issues](health-alerts.md) |

|Consider integrating with Microsoft XDR|Defender for Identity provides alerting on identity-based threats. Integrating with Microsoft Defender XDR lets you correlate these alerts with other signals for a more comprehensive view of threats and potential solutions.<br></br>Microsoft Defender XDR is a unified pre-breach and post-breach enterprise defense suite that natively coordinates detection, prevention, investigation, and response across endpoints, identities, email, and applications to provide integrated protection against sophisticated attacks.|[Microsoft Defender](/defender-xdr/microsoft-365-defender-train-security-staff).|

|Check Windows event collection configuration|Optimal event collection is essential for Defender for Identity to analyze and detect threats effectively. Check your configuration before running any tests. |- [Configure Windows event collection for domain controllers](deploy/configure-windows-event-collection.md)</br> - [Configure Windows event collection for AD CS](deploy/configure-windows-event-collection.md#configure-auditing-on-an-ad-cs-server)</br> - [Configure Windows event collection for AD FS](deploy/configure-windows-event-collection.md#configure-auditing-on-an-ad-fs-server)</br> - [Configure Windows event collection for Microsoft Entra Connect](deploy/configure-windows-event-collection.md#configure-auditing-on-microsoft-entra-connect)</br> - [Use PowerShell to check your configuration](https://www.powershellgallery.com/packages/DefenderForIdentity/1.0.0.4)|

|Check that NNR is configured correctly|NNR is a critical component of Defender for Identity. Defender for Identity uses NNR to correlate between raw activities containing IP addresses and the computers involved in each activity. Defender for Identity profiles entities, including computers, and generates security alerts for suspicious activities. It's important for NNR to be configured correctly for a successful deployment and to help detect advanced threats.|[Configure Network Name Resolution (NNR) for Microsoft Defender for Identity](nnr-policy.md)|

|Check that you have a Directory Service account (DSA) |While a DSA is optional in some scenarios, we recommend that you configure a DSA for Defender for Identity for full security protection. When you have a DSA configured: <br> - The DSA connects to the domain controller at startup.<br> - The DSA queries the domain controller for data on entities seen in network traffic, monitored events, and monitored Event Tracing for Windows (ETW) activities.<br><br>A DSA is required for the following features and functionality:<br> - When working with a sensor installed on an AD FS / AD CS server<br> - To access the DeletedObjects container to collect information about deleted users and computers<br> - For domain and trust mapping, which occurs at sensor startup, and again every 10 minutes.<br> - To query another domain via LDAP for details, when detecting activities from entities in those other domains. |[Directory Service Accounts for Microsoft Defender for Identity](deploy/directory-service-accounts.md)|

|Check the alert learning periods|Alerts rely on learning periods to build a profile of patterns and then distinguish between legitimate and suspicious activities. Each alert incorporates specific conditions within the detection logic, such as thresholds and filtering of popular activities. Check [these alerts](#security-alert-learning-periods) to make sure that they meet the required learning periods. |[Alerts overview](alerts-overview.md)|

|Check the alert thresholds|The threshold level of an alert influences the number of alerts you receive for that trigger. The default threshold for all alerts is **High**. You can customize the threshold level for individual alerts to **High**, **Medium**, or **Low**. Lowering the threshold of an alert increases the number of alerts generated by Microsoft Defender for Identity. Alerts that are triggered when threshold is set to **Medium** or **Low** contain text that indicates the alert threshold.<br>When you enable the **Recommended Test Mode** button, all alert threshold levels are set to **Low**. When the threshold is low, you get more alerts, including some related to legitimate traffic and activities. This setting can be useful to get more data into a nonproduction environment that doesn't have enough entity historical data or profiles.<br>Lowering the threshold to **Low** also leads to more false positives and isn't recommended for production environments. |[Adjust alert threshold settings or enable recommended test mode](advanced-settings.md#adjust-alert-thresholds)|

|Review the Secure Score recommendations for Defender for Identity|Following Secure Score recommendations helps improve your security posture and enhances the effectiveness of Defender for Identity in detecting threats.|[Microsoft Secure Score](https://security.microsoft.com/securescore?viewid=actions)|

### Security alert learning periods

Make sure that the learning periods for the alerts listed below have been met before you begin your offensive security testing.

| Alert | Learning Period |

|-------|-----------------|

| [Network-mapping reconnaissance (DNS) (External ID 2007)](alerts-mdi-classic.md#network-mapping-reconnaissance-dns) | Eight days from the start of domain controller monitoring |

| [User and Group membership reconnaissance (SAMR) (External ID 2021)](alerts-mdi-classic.md#user-and-group-membership-reconnaissance-samr) | Four weeks per domain controller starting from the first network activity of SAMR against the specific DC |

| [Suspected Golden Ticket usage (encryption downgrade) (External ID 2009)](alerts-mdi-classic.md#suspected-golden-ticket-usage-encryption-downgrade) | Five days from the start of domain controller monitoring |

| [Suspicious additions to sensitive groups (External ID 2024)](alerts-mdi-classic.md#suspicious-additions-to-sensitive-groups) | Four weeks per domain controller, starting from the first event |

| [Suspected Brute Force attack (Kerberos, NTLM) (External ID 2023)](alerts-mdi-classic.md#suspected-brute-force-attack-kerberos-ntlm) | One week |

| [Security principal reconnaissance (LDAP) (External ID 2038)](alerts-mdi-classic.md#security-principal-reconnaissance-ldap) | 15 days per computer, starting from the day of the first event, observed from the machine |

| [Suspected over-pass-the-hash attack (forced encryption type) (External ID 2008)](alerts-mdi-classic.md#suspected-over-pass-the-hash-attack-forced-encryption-type) | One month |

| [Suspicious VPN connection (External ID 2025)](alerts-mdi-classic.md#suspicious-vpn-connection) | 30 days from the first VPN connection, and at least 5 VPN connections in the last 30 days, per user |

## Related content

- The Microsoft Defender XDR [Security operations overview](/security/operations/overview).


# Reports

# Download and schedule Defender for Identity reports in Microsoft Defender XDR (Preview)

Microsoft Defender XDR provides Defender for Identity reports, which you can either generate on demand or configure to be sent periodically by email.

## Access Defender for Identity reports in Microsoft Defender XDR

To access Defender for Identity reports in Microsoft Defender XDR, from the navigation menu on the left, select **Reports** > **Identities** > **Report management**.

Available reports include:

|Report name  |Description  |

|---------|---------|

|**Summary**| Presents a dashboard of your system status, including: <br><br>- **Summary**: A summary of detected network activity <br>- **Open health issues**: Lists Defender for Identity health issues you should take care of. <br><br> Suspicious activities and health issues are listed by type. |

|**Modification to sensitive groups**     |    Lists every time a modification is made to sensitive groups, such as admins, or manually tagged accounts or groups. <br><br>If you're using Defender for Identity standalone sensors, make sure that [events are forwarded from your domain controllers to the standalone sensors](deploy/configure-event-forwarding.md) in order to receive a full report about your sensitive groups.     |

|**Passwords exposed in cleartext**     | Lists all source computer and account passwords detected by Defender for Identity being sent in clear text. <br><br>**Note**: Some services use the LDAP non-secure protocol to send account credentials in plain text. This can even happen for sensitive accounts. Attackers monitoring network traffic can catch and then reuse these credentials for malicious purposes.     |

## Generate a report on demand

To generate a report on demand:

1. In Microsoft Defender XDR, select **Reports** > **Identities** > **Report management**.

1. On the **Identities reports** page, select a report and then select **Download**.

1. In the download report pane that appears on the right, define a time period for your report and then select **Download Report**.

Your report is downloaded by your browser, where you can open or save it. Downloaded reports include a maximum of 100,000 rows.

## Schedule a report by email

To define a schedule for a report to be sent to you by email:

1. In Microsoft Defender XDR, select **Reports** > **Identities** > **Report management**.

1. On the **Identities reports** page, select a report and then select **Schedule report**.

1. Use the wizard to define the following details:

1. On the **Set schedule** page, define the conditions in which you want to send the report, and the time you want it sent.

Your report is sent according to your Microsoft Defender XDR time zone settings (*Local* or UTC). For more information, see [Set the time zone for Microsoft Defender XDR](/microsoft-365/security/defender/m365d-time-zone).

1. On the **Recipients** page, enter and add email addresses for anyone you want to receive the report. Select **Next** to complete the scheduling.

1. The **Finish** page shows a confirmation message. Select **Close** to close the wizard.

Once the scheduling is configured, repeat this procedure to edit the scheduled time or recipients.

### Remove all scheduled reports

To remove a scheduled report and stop it from being sent:

1. In Microsoft Defender XDR, select **Reports** > **Identities** > **Reports management**.

1. On the **Identities reports** page, select the report you want to stop sending and then select **Reset schedule**.

1. In the confirmation message, select **Reset** to complete the process.

## Related content

- [Investigate assets](investigate-assets.md)

- [Microsoft Defender for Identity's security posture assessments](security-assessment.md)


# Settings About

# About page for Defender for Identity

This article explains how to use the About page to collect important details about your Defender for Identity workspace in Microsoft Defender XDR.

## Details on About page

To access the About page, in  [Microsoft Defender XDR](https://security.microsoft.com), go to **Settings** and then **Identities**. Under **General**, select **About**.

The About page provides the following details:

- Sensor version: The latest software version available for sensor updates.

- Geolocation: The geographic location of the workspace where your data is stored.

- Workspace ID: The identifier of your workspace.

- Workspace name: The name of your workspace.

- Total licenses: The total number of Microsoft Denfender for Identity licenses assigned to the tenant.

- Active identities during the past 28 days: The total number of on-premises identities that had activity detected by Defender for Identity.

This information can be helpful when troubleshooting issues and opening support tickets. Additionally, you can find the name of your workspace (workspace) which is necessary for configuring your [proxy or firewall](configure-proxy.md#enable-access-to-defender-for-identity-service-urls-in-the-proxy-server).

## See also

- [Defender for Identity prerequisites](prerequisites.md)

- [Check out the Defender for Identity forum!](<https://aka.ms/MDIcommunity>)


# Sensor Settings

# Manage and update Microsoft Defender for Identity sensors

This article explains how to view, manage, and update Defender for Identity sensors in the Microsoft Defender portal.

## View sensor settings and status

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** > **Identities**.

1. In the left sidebar, under **Deployment**, select **On-premises**.

1. Select the **Sensors** tab.

The **Sensors** tab shows all Defender for Identity sensors deployed in your environment. From this tab you can:

- **Filter** sensors by type, domain, delayed update, service status, sensor status, migration state, or health status.

- **Export** the sensor list to a .csv file.

- **Onboard a sensor** using the **+ Add sensor** option.

- **Customize columns** to show or hide specific fields.

- **Search** for a specific sensor by name.

Select a sensor row to open a details pane with information about the sensor and its health status. From the details pane, you can select **Manage sensor** to update sensor configuration, or select a health issue to see more details and reopen closed issues.

## Sensor details

The **Sensors** tab shows the following columns. For columns with multiple possible values, see the tables below.

- **Sensor**: The sensor's NetBIOS computer name.

- **Type**: The sensor type. For possible values, see [Type](#type).

- **Domain**: The fully qualified domain name of the Active Directory domain where the sensor is installed.

- **Migration state**: Indicates if sensors are eligible for [migration from v2.x to v3.x](deploy/migrate-to-sensor-v3.md). For possible values, see [Migration state](#migration-state).

- **Service status**: The current state of the sensor service on the server. For possible values, see [Service status](#service-status).

- **Sensor status**: The current update and configuration state of the sensor software. For possible values, see [Sensor status](#sensor-status).

- **Version**: The sensor version installed.

- **Delayed update**: Whether delayed updates are enabled or disabled. Delayed updates are supported by version 2 of the sensor. For more information, see [Delayed sensor update](#delayed-update-for-sensor-v2x).

- **Health issues**: The count of open health issues on the sensor.

- **Health status**: The overall health of the sensor based on the highest severity open health issue. For possible values, see [Health status](#health-status).

- **Created**: The date the sensor was installed.

### Type

The type column indicates the sensor type based on the server role where the sensor is installed. If a sensor is installed on a domain controller that also runs Entra Connect or AD CS, the type shows as **Domain controller sensor**.

| Type | Description |

| --- | --- |

| **Domain controller sensor** | Installed on an Active Directory domain controller. |

| **AD FS sensor** | Installed on an Active Directory Federation Services (AD FS) server. |

| **Standalone sensor** | Installed on a dedicated server that monitors domain controller traffic via port mirroring. |

| **Entra Connect sensor** | Installed on a Microsoft Entra Connect server. |

| **ADCS sensor** | Installed on an Active Directory Certificate Services (AD CS) server. |

### Migration state

The migration state column shows if the sensor is eligible for [migration from v2.x to v3.x](deploy/migrate-to-sensor-v3.md).

For a server to be eligible for migration, it must be:

- A domain controller without additional identity roles (AD FS, AD CS, or Microsoft Entra Connect) running. Domain controllers with identity roles support v3.x for new deployments, but in-place migration isn't currently supported for these servers.

- Running a Defender for Identity sensor v2.x.

- Running Windows Server 2019 or later.

- Includes the [March 2026 or later](https://support.microsoft.com/en-us/topic/march-10-2026-kb5078766-os-build-20348-4893-fa3ee26a-0877-47d7-a4b2-9dd632ea8cea) cumulative update.

- Have Microsoft Defender for Endpoint deployed.

For the full list of v3.x requirements, see [Defender for Identity sensor v3.x prerequisites](./deploy/deploy-sensor-v3.md).

| State | Description |

| --- | --- |

| **Ready for migration** | The server meets all prerequisites and can be migrated. |

| **Not ready for migration** | The server doesn't meet one or more prerequisites. |

| **Migrating** | The migration is in progress. |

| **Up to date** | The migration completed successfully. The server is running sensor v3.x. |

| **Migration failed** | The migration encountered an error. You can retry the migration. |

### Service status

The service status column indicates the current operational state of the sensor service on the server.

| Status | Description |

|---|---|

| **Running** | The sensor service is running. |

| **Starting** | The sensor service is starting. |

| **Disabled** | The sensor service is disabled. |

| **Stopped** | The sensor service is stopped. |

| **Unknown** | The sensor is disconnected or unreachable. |

### Sensor status

The sensor status column indicates the current update and configuration state of the sensor software.

| Status | Description |

| --- | --- |

| **Up to date** | The sensor is running the current version. |

| **Outdated** | The sensor is running a version that is at least three versions behind the current version. |

| **Updating** | The sensor software is being updated. |

| **Update failed** | The sensor failed to update to a new version. |

| **Not Configured** | The sensor requires more configuration before it's fully operational. This applies to sensors on AD FS, AD CS, or standalone servers. |

| **Start failed** | The sensor didn't pull configuration for more than 30 minutes. |

| **Syncing** | The sensor has configuration updates pending but didn't yet pull the new configuration. |

| **Disconnected** | No communication from this sensor in 10 minutes. |

| **Unreachable** | The domain controller was deleted from Active Directory, but the sensor wasn't uninstalled before decommissioning. You can safely delete this entry. |

### Health status

The health status column indicates the overall health of the sensor based on the severity of any open health issues.

| Status | Description |

| --- | --- |

| **Healthy** (green icon) | No open health issues. |

| **Not healthy** (yellow icon) | The highest severity open health issue is low. |

| **Not healthy** (orange icon) | The highest severity open health issue is medium. |

| **Not healthy** (red icon) | The highest severity open health issue is high. |

## Update sensors

Defender for Identity sensor v3.x is delivered as a component of Microsoft Defender for Endpoint and is updated automatically through Windows Updates. No manual sensor update process is required for v3.x sensors.

The rest of this section applies only to Defender for Identity sensor v2.x.

### Defender for Identity sensor v2.x update types

The Defender for Identity service is typically updated a few times a month with new detections, features, and performance improvements. These updates usually include a corresponding minor update to the sensors.

Defender for Identity sensors v2.x support two kinds of updates:

- Minor version updates:

- Frequent

- Requires no MSI install, and no registry changes

- Restarted: Defender for Identity sensor services

- Major version updates:

- Rare

- Contains significant changes

- Restarted: Defender for Identity sensor services

> [!NOTE]

>

> Defender for Identity sensors v2.x always reserve at least 15% of the available memory and CPU on the domain controller where the sensor is installed. If the service consumes too much memory, it's automatically stopped and restarted by the sensor updater service.

### Delayed update for sensor v2.x

You can define a subset of your sensors as a delayed update ring. Sensors not in the delayed ring are updated automatically each time the service is updated. Sensors set to **Delayed update** are updated 72 hours later, giving you time to confirm that the automatically updated sensors are working correctly.

> [!NOTE]

> If an error occurs and a sensor does not update, open a support ticket. To further harden your proxy to only communicate with your workspace, see [Proxy configuration](configure-proxy.md).

Authentication between your sensors and the Azure cloud service uses certificate-based mutual authentication. A self-signed client certificate is created during sensor installation and is valid for 2 years. The sensor updater service generates a new certificate before the existing one expires, using a 2-phase validation process to avoid authentication disruptions during the rollover.

To set a sensor to delayed update:

1. In the **Sensors** page, select the sensor you want to set for delayed updates.

1. Select the **Enabled delayed update** button.

1. In the confirmation window, select **Enable**.

To disable delayed updates, select the sensor and then select the **Disabled delayed update** button.

### Sensor v2.x update process

Every few minutes, v2.x sensors check whether a newer version is available. When the cloud service is updated, sensors start the update process:

1. The cloud service updates to the latest version.

1. The sensor updater service detects the new version.

1. Sensors that aren't set to **Delayed update** start the update process one at a time:

1. The sensor updater service pulls the updated version from the cloud service (in *.cab* file format).

1. The sensor updater validates the file signature.

1. The sensor updater extracts the cab file to a new folder in the sensor's installation folder. By default it's extracted to *C:\Program Files\Azure Advanced Threat Protection Sensor\<version number>*

1. The sensor service points to the new files extracted from the cab file.

1. The sensor updater restarts the sensor service.

> [!NOTE]

> Minor sensor updates install no MSI, change no registry values or any system files. A pending restart does not affect a sensor update.

1. The sensor runs the newly updated version.

1. The sensor receives clearance from the cloud service. You can verify sensor status on the **Sensors** tab.

1. The next sensor starts the update process.

1. Sensors selected for **Delayed update** start their update process 72 hours after the Defender for Identity cloud service is updated. These sensors will then use the same update process as automatically updated sensors.

For any sensor that fails to complete the update process, a relevant [health alert](health-alerts.md) is triggered, and is sent as a notification.

### Silently update the Defender for Identity v2.x sensor

Use the following command to silently update the Defender for Identity v2.x sensor:

**Syntax**:

```cmd

"Azure ATP sensor Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]

```

**Installation options**:

> [!div class="mx-tableFixed"]

>

> |Name|Syntax|Mandatory for silent installation?|Description|

> |-------------|----------|---------|---------|

> |Quiet|/quiet|Yes|Runs the installer displaying no UI and no prompts.|

> |Help|/help|No|Provides help and quick reference. Displays the correct use of the setup command including a list of all options and behaviors.|

> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Yes|Specifies the parameters for the .Net Framework installation. Must be set to enforce the silent installation of .Net Framework.|

**Examples**:

To update the Defender for Identity sensor silently:

```cmd

"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"

```

## Remove RPC auditing from a device

If you configured RPC auditing for a v3.x sensor using the **Unified Sensor RPC Audit** tag, you can remove it by deleting the asset rule or modifying the rule conditions so the device no longer matches.

To manage asset rules, in the [Microsoft Defender portal](https://security.microsoft.com), go to **System > Settings > Microsoft Defender XDR > Asset Rule Management**.

> [!NOTE]

> It might take up to one hour for changes to be reflected in the portal.

Learn more about [asset management rules](/defender-xdr/configure-asset-rules).

## Configure proxy settings

We recommend that you configure initial proxy settings during silent installation [using command line switches](deploy/install-sensor.md#perform-a-defender-for-identity-silent-installation). If you need to update your proxy settings later on, use either the [CLI](deploy/configure-proxy.md#change-proxy-configuration-using-the-cli) or [PowerShell](deploy/configure-proxy.md#change-proxy-configuration-using-powershell).

If you'd previously configured your proxy settings via either WinINet or a registry key and need to update them, you'll need to [use the same method](deploy/configure-proxy.md#change-proxy-configuration-using-legacy-methods) you used originally.

For more information, see [Configure endpoint proxy and internet connectivity settings](deploy/configure-proxy.md).

## Next steps

- [Defender for Identity sensor v2.x prerequisites](deploy/prerequisites-sensor-version-2.md) and [Defender for Identity sensor v3.x prerequisites](deploy/deploy-sensor-v3.md)

- [Configure event forwarding](deploy/configure-event-forwarding.md)

- [Defender for Identity community forum](<https://aka.ms/MDIcommunity>)


# Uninstall Sensor

# Remove the Microsoft Defender for Identity sensor

This article describes how to uninstall the Microsoft Defender for Identity sensor from domain controllers.

## Delete a sensor

### For sensor v3.x

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** > **Identities** > **Sensors**.

2. Select the domain controller where you want to deactivate Defender for Identity capabilities, select **Delete**, and confirm your selection.

>[!NOTE]

>This action removes the v3.x sensor and stops monitoring on that domain controller.

## Delete and uninstall a sensor v2.x from a domain controller

> [!IMPORTANT]

> We recommend removing the sensor from the domain controller before demoting the domain controller.

>

1. Sign in to the domain controller with administrative privileges.

2. From the Windows **Start** menu, select **Settings** > **Control Panel** > **Add/ Remove Programs**.

3. Select the sensor installation, select **Uninstall**, and follow the instructions to remove the sensor.

4. After uninstallation is complete, go to the Microsoft Defender portal > Settings > Identities > Sensors, select the domain controller, and choose Delete.

## Remove an orphaned sensor

A sensor can be orphaned when a domain controller was deleted without first uninstalling the sensor, and the sensor still appears in the Microsoft Defender portal.

1. In the [Defender portal](https://security.microsoft.com), go to **Settings** and then **Identities**. Select **Sensors** on the left to display all your Defender for Identity sensors.

1. Locate the orphaned sensor and select **Delete** (trash can icon).

![Delete orphaned Defender for Identity sensor from sensors page](media/delete-orphaned-sensor.png)

## Remove a duplicate sensor

This scenario may occur after an in-place sensor upgrade, and the sensor appears twice in the Microsoft Defender portal.

1. In [Defender portal](https://security.microsoft.com), go to **Settings** and then **Identities**. Select **Sensors** on the left to display all your Defender for Identity sensors.

1. Locate the duplicate sensor. It will be the one whose status is set to **Unknown**. Then, at the end of the row, select **Delete** (trash can icon).

## Uninstall the Defender for Identity sensor silently

Use the following command to perform a silent uninstall of the Defender for Identity sensor:

**Syntax**:

```cmd

"Azure ATP sensor Setup.exe" [/quiet] [/Uninstall] [/Help]

```

**Installation options**:

> [!div class="mx-tableFixed"]

>

> |Name|Syntax|Mandatory for silent uninstallation?|Description|

> |-------------|----------|---------|---------|

> |Quiet|/quiet|Yes|Runs the uninstaller displaying no UI and no prompts.|

> |Uninstall|/uninstall|Yes|Runs the silent uninstallation of the Defender for Identity sensor from the server.|

> |Help|/help|No|Provides help and quick reference. Displays the correct use of the setup command including a list of all options and behaviors.|

**Examples**:

To silently uninstall the Defender for Identity sensor from the server:

```cmd

"Azure ATP sensor Setup.exe" /quiet /uninstall

```

## See also

- [Manage and update Microsoft Defender for Identity sensors](sensor-settings.md)


# Configure Scoped Access

# Configure scoped access for Microsoft Defender for Identity

As your organization grows, you need to control who can access which resources. Microsoft Defender for Identity scoping lets you focus monitoring on specific Active Directory domains or organizational units. This reduces noise from data you don't need and helps you focus on critical assets. You can also limit visibility to specific entities so that access matches each person's role.

To set up scoped access, [create a custom role using Microsoft Defender unified RBAC](/defender-xdr/create-custom-rbac-roles). When you configure the role, you choose which users or Entra ID groups can access specific Active Directory domains or organizational units.

## Prerequisites

Before you begin, make sure you meet the following requirements:

- A Microsoft Defender for Identity sensor is installed.

- The [Identity workload in Microsoft Defender unified RBAC](/defender-xdr/activate-defender-rbac#activate-from-the-permissions-and-roles-page) is turned on.

- You have the [Security Administrator](/entra/identity/role-based-access-control/permissions-reference) role in Microsoft Entra ID.

- Authorization permissions are set up through [URBAC](/defender-xdr/manage-rbac) if you want to manage roles without the Security Administrator role.

### Configure scoping rules

To enable identity scoping, follow these steps:​

1. Navigate to **Permissions > Microsoft Defender XDR > Roles​**.

1. Select **+ Create custom role** and follow the instructions in [Create custom roles with Microsoft Defender unified RBAC.](/defender-xdr/create-custom-rbac-roles#create-a-custom-role)

1. You can edit the role at any time. Select the role from the list of custom roles and choose **Edit**.

1. Select Add assignments and add the Assignment name.

1. Under **Assign users and groups**, enter the usernames or Microsoft Entra ID groups you want to assign to the role.

1. Select Microsoft Defender for Identity as the data source.

1. Under **Scope**, select the user groups (AD domains or OU's) that will be scoped to the assignment. For an optimal experience, use the filter or search box.

![Screenshot of the scoped assignment page with a user group selected for the assignment.](media/configure-scoped-access/add-scope.png)

![Screenshot of the custom scope creation page with options for defining a custom scope.](media/configure-scoped-access/custom-scope.png)

1. Select **Apply** and **Add**.

### Known limitations

The following table lists the current limitations and supported scenarios for scoped access in Microsoft Defender for Identity.

> [!NOTE]

> - Custom roles apply only to new alerts and activities. Alerts and activities triggered before a custom role was created aren't retroactively tagged or filtered.

> - The Exposure Management section in the Defender Portal is not visible to users with an MDI scope assignment.

> - Microsoft Entra ID IP alerts aren't included within scoped MDI detections.

|Defender for Identity experience |Scoping by OU's|Scoping by AD domain|

|---------| -------- |---------|

|MDI alerts and incidents  |Available| Available|

|Hunting tables: AlertEvidence+Info, IdentityInfo, IdentityDirectoryEvents, IdentityLogonEvents, IdentityQueryEvents     |Available|   Available      |

|User page and user global search  |Available|   Available      |

|MDI alerts based on XDR detection platform (detection source is XDR and service source is MDI)     |Available|   Available      |

|Health issues       |Unavailable|   Available      |

|Identities inventory and service accounts discovery page     |Available|  Available      |

|Identities settings: manual tagging|Available|Available|

|Identities settings: sensors page, health issues notifications  |Unavailable|   Available      |

|Defender XDR Incident email notifications     |Available| Unavailable      |

|ISPMs and exposure management     |Unavailable|   Unavailable      |

|Download scheduled reports and Graph API    |Unavailable|   Unavailable      |

|Device and group global search and entity page     |Available|   Available      |

|Alert tuning and critical asset management   |Unavailable|   Unavailable      |

### Related articles

- [Microsoft Defender for Identity role groups](role-groups.md)

- [Microsoft Defender unified role-based access control (RBAC)](/defender-xdr/manage-rbac)

- [Create custom roles with Microsoft Defender unified RBAC](/defender-xdr/create-custom-rbac-roles)

- [Import roles to Microsoft Defender unified role-based access control (RBAC)](/defender-xdr/import-rbac-roles)

- [Activate Microsoft Defender unified role-based access control (RBAC)](/defender-xdr/activate-defender-rbac)


# Vpn Integration

# Defender for Identity VPN integration in Microsoft Defender XDR

>[!NOTE]

>This feature is currently supported only by the Defender for Identity sensor version 2.x.

Microsoft Defender for Identity can integrate with your VPN solution by listening to RADIUS accounting events forwarded to Defender for Identity sensors, such as the IP addresses and locations where connections originated. VPN accounting data can help your investigations by providing more information about user activity, such as the locations from where computers are connecting to the network, and an extra detection for abnormal VPN connections.

Defender for Identity's VPN integration is based on standard RADIUS Accounting ([RFC 2866](https://tools.ietf.org/html/rfc2866)), and supports the following VPN vendors:

- Microsoft

- F5

- Check Point

- Cisco ASA

VPN integration is not supported in environments adhering to Federal Information Processing Standards (FIPS)

Defender for Identity's VPN integration supports both primary UPNs and alternate user principal names. Calls to resolve external IP addresses to a location are anonymous and no personal identifier is sent in the call.

## Prerequisites

Before you start, make sure that you have:

- [Microsoft Defender for Identity deployed](deploy-defender-identity.md)

- Access to the **Settings** area in Microsoft Defender XDR. For more information, see [Microsoft Defender for Identity role groups](role-groups.md).

- The ability to configure RADIUS on your VPN system.

This article provides an example of how to configure Microsoft Defender for Identity to collect accounting information from VPN solutions, using Microsoft Routing and Remote Access Server (RRAS). If you're using a third-party VPN solution, consult their documentation for instructions on how to enable RADIUS Accounting.

> [!NOTE]

> When you [configure the VPN integration](#configure-vpn-in-defender-for-identity), the Defender for Identity sensor enables a pre-provisioned Windows firewall policy called **Microsoft Defender for Identity Sensor**. This policy allows incoming RADIUS Accounting on port UDP 1813.

>

## Configure RADIUS accounting on your VPN system

This procedure describes how to configure RADIUS accounting on an RRAS server for integrating a VPN system with Defender for Identity. Your system's instructions may differ.

**On your RRAS server**:

1. Open the **Routing and Remote Access** console.

1. Right-click the server name and select **Properties**.

1. In the **Security** tab, under **Accounting provider**, select **RADIUS Accounting** > **Configure**. For example:

![Screenshot of the Security tab.](media/radius-setup.png)

1. In the **Add RADIUS Server** dialog, enter the **Server name** of the closest Defender for Identity sensor with network connectivity. For high availability, you can add more Defender for Identity sensors as RADIUS Servers.

1. Under **Port**, make sure the default value of `1813` is configured.

1. Select **Change** and enter a new shared secret string of alphanumeric characters. Take note of the new shared secret string, as you'll need it later when configuring the VPN integration in Defender for Identity.

1. Check the **Send RADIUS Account On and Accounting Off messages** box and select **OK** on all open dialog boxes. For example:

![Screenshot of the Send RADIUS Account On and Accounting Off messages button.](media/vpn-set-accounting.png)

## Configure VPN in Defender for Identity

This procedure describes how to configure Defender for Identity's VPN integration in Microsoft Defender XDR.

1. Sign into [Microsoft Defender XDR](https://security.microsoft.com) and select **Settings** > **Identities** > **VPN**.

1. Select **Enable radius accounting** and enter the **Shared Secret** you'd previously configured on your RRAS VPN server. For example:

![Screenshot of the Enable radius accounting option.](media//vpn-integration.png)

1. Select **Save** to continue.

After you've saved your selection, your Defender for Identity sensors start listening on port 1813 for RADIUS accounting events, and your VPN setup is complete.

When the Defender for Identity sensor receives VPN events and sends them to the Defender for Identity cloud service for processing, the entity profile indicates distinct VPN locations that were accessed, and profile activities indicate locations.

## Related content

For more information, see [Configure event collection](deploy/configure-event-collection.md).


# Entity Tags

# Defender for Identity entity tags in Microsoft Defender XDR

This article describes how to apply Microsoft Defender for Identity entity tags, for sensitive, Exchange server, or honeytoken accounts.

- You must tag sensitive accounts for Defender for Identity detections that rely on an entity's sensitivity status, for example, sensitive group modification detections.

While Defender for Identity automatically tags Exchange servers as high-value, sensitive assets, you can also manually tag devices as Exchange servers.

- Tag honeytoken accounts to set traps for malicious actors. Since honeytoken accounts are usually dormant, any authentication associated with a honeytoken account triggers an alert.

## Prerequisites

To set Defender for Identity entity tags in Microsoft Defender XDR, you'll need Defender for Identity [deployed in your environment, as described in the Defender for Identity deployment guide](deploy-defender-identity.md), and administrator or user access to Microsoft Defender XDR.

For more information, see [Microsoft Defender for Identity role groups](role-groups.md).

## Tag entities manually

To manually tag an entity in Microsoft Defender XDR, such as a honeytoken account or an entity not automatically tagged as *Sensitive*, use the following steps:

1. Sign into [Microsoft Defender XDR](https://security.microsoft.com) and select **Settings** > **Identities**.

1. Select the type of tag you want to apply: **Sensitive**, **Honeytoken**, or **Exchange server**.

The page lists the entities already tagged in your system, listed on separate tabs for each entity type:

- The *Sensitive* tag supports users, devices, and groups.

- The *Honeytoken* tag supports users and devices.

- The *Exchange server* tag supports devices only.

1. To tag additional entities, select the **Tag ...** button, such as **Tag users**. A pane opens on the right listing the available entities for you to tag.

1. Use the search box to find your entity if you need to. Select the entities you want to tag, and then select **Add selection**.

For example:

## Default sensitive entities

The groups in the following list are considered **Sensitive** by Defender for Identity. Any entity that is a member of one of these Active Directory groups, including nested groups and their members, is automatically considered sensitive:

- Administrators

- Power Users

- Account Operators

- Server Operators

- Print Operators

- Backup Operators

- Replicators

- Network Configuration Operators

- Incoming Forest Trust Builders

- Domain Admins

- Domain Controllers

- Group Policy Creator Owners

- Read-only Domain Controllers

- Enterprise Read-only Domain Controllers

- Schema Admins

- Enterprise Admins

- Microsoft Exchange Servers

> [!NOTE]

> Until September 2018, Remote Desktop Users were also automatically considered sensitive by Defender for Identity. Remote Desktop entities or groups added after this date are no longer automatically marked as sensitive while Remote Desktop entities or groups added before this date may remain marked as Sensitive. This Sensitive setting can now be changed manually.

In addition to these groups, Defender for Identity identifies the following high value asset servers and automatically tags them as **Sensitive**:

- Certificate Authority Server

- DHCP Server

- DNS Server

- Microsoft Exchange Server

- Replicating Directory Changes Permissions

<a name="defender-for-identity-integrations"></a>

## Supported integrations for entity tags

The following roles are designated as Sensitive by Microsoft Defender for Identity. Any entity assigned membership in these roles is automatically classified as sensitive.

<a name="okta"></a>

### Okta sensitive roles

The following Okta roles are designated as Sensitive by Defender for Identity:

- Super Administrator

- Application Administrator

- Group Administrator

- API Access Management Administrator

- Group Membership Administrator

- Help Desk Administrator

- Mobile Administrator

- Organization Administrator

- Read-only Administrator

- Report Administrator

<a name="cyberark-identity"></a>

### CyberArk Identity sensitive roles

The following CyberArk Identity roles are designated as Sensitive by Defender for Identity:

- Administration Role

- Cloud Onboarding Admin

- Connector Management Admin

- Flows Admin

- Privilege Cloud Administrators

- Privilege Cloud Administrators Basic

- Privilege Cloud Administrators Lite

- Privilege Cloud Safe Managers

- Privilege Cloud Safe Managers Basic

- Privilege Cloud Safe Managers Lite

- Privilege Cloud Session Admin

- Privilege Cloud Session Risk Managers

- System Administrator

<a name="sailpoint-identity-security-cloud"></a>

### SailPoint Identity Security Cloud sensitive roles

<a name="entra-id-roles"></a>

#### Entra ID roles used for tagging

The following Entra ID roles are designated as Sensitive by Defender for Identity:

- Global Administrator

- User Administrator

- Authentication Administrator

- Privileged Authentication Administrator

- Helpdesk Administrator

- Agent ID Administrator

- Application Administrator

- Directory Writers

- Domain Name Administrator

- Password Administrator

- Privileged Role Administrator

- Hybrid Identity Administrator

- Cloud Application Administrator

<a name="sailpoint-identity-security-cloud-roles"></a>

#### SailPoint Identity Security Cloud roles used for tagging

The following SailPoint Identity Security Cloud role is designated as Sensitive by Defender for Identity:

- IdentityNow Administrator

## Related content

For more information, see [Investigate Defender for Identity security alerts in Microsoft Defender XDR](manage-security-alerts.md).


# Exclusions

# Configure Defender for Identity detection exclusions in Microsoft Defender XDR

This article explains how to configure [Microsoft Defender for Identity](/defender-for-identity) detection exclusions in [Microsoft Defender XDR](/microsoft-365/security/defender/overview-security-center).

Microsoft Defender for Identity enables the exclusion of specific IP addresses, computers, domains, or users from a number of detections.

For example, a **DNS Reconnaissance** alert could be triggered by a security scanner that uses DNS as a scanning mechanism. Creating an exclusion helps Microsoft Defender for Identity ignore such scanners and reduce false positives.

> [!NOTE]

> - We recommend that you [tune an alert in Microsoft Defender XDR](/microsoft-365/security/defender/investigate-alerts#tune-an-alert) instead of using exclusions. Alert tuning rules allow more granular conditions than exclusions, and allow you to review the alerts, which were tuned.

>

>- Among the most common domains with [Suspicious communication over DNS](other-alerts.md#suspicious-communication-over-dns-external-id-2031) alerts, we observed the domains that were most frequently excluded from the alert. These domains are added to the exclusions list by default, but you have the option to remove them.

## How to add detection exclusions

To add detection exclusions, complete the following steps.

> [!NOTE]

> When replacing an existing exclusion with an alert tuning rule, identify the detection associated with the excluded entity and map it to the corresponding detector in alert tuning. After creating the tuning rule, verify that the detector appears under Alert tuning in the Microsoft Defender portal to ensure that the intended alert scope is preserved.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/)

1.  Go to **System** > **Settings** and then **Identities**.

1. Select **Excluded entities**. You can set exclusions using two methods: **Exclusions by detection rule** and **Global excluded entities**.

## Exclusions by detection rule

To configure exclusions for a specific detection rule, follow these steps:

1. Select **Exclusions by detection rule**.

1. For each detection you want to configure, do the following steps:

1. Select a detection rule from the list.

1. View the detection rule details.

1. To add an exclusion, select the **Excluded entities** button.

1. Choose the exclusion type. Different excluded entities are available for each rule. They include users, devices, domains, and IP addresses. In this example, the choices are **Exclude devices** and **Exclude IP addresses**.

1. After choosing the exclusion type, select the **+** button to add the exclusion.

1. Select **+ Add** to add the excluded entity to the list.

1. Select **Exclude IP addresses** (in this example) to complete the exclusion.

1. Once you've added exclusions, you can export the list or remove the exclusions by returning to the **Excluded entities** button. In this example, we've returned to **Exclude devices**. To export the list, select the down arrow button.

1. To delete an exclusion, select the exclusion and select the trash icon.

## Global excluded entities

You can now also configure exclusions by **Global excluded entities**. Global exclusions allow you to define certain entities (IP addresses, subnets, devices, or domains) to be excluded across all of the detections Microsoft Defender for Identity has. So for example, if you exclude a device, the exclusion will only apply to those detections that have device identification as part of the detection.

1. Select **Global excluded entities** to see the categories of entities that you can exclude.

1. Choose an exclusion type. In this example, we selected **Exclude domains**.

1. A pane opens where you can add a domain to be excluded. Add the domain you want to exclude.

1. The domain is added to the list. Select **Exclude domains** to complete the exclusion.

1. You'll then see the domain in the list of entities to be excluded from all detection rules. You can export the list, or remove the entities by choosing them and selecting the **Remove** button.

## Next steps

- [Configure event collection](deploy/configure-event-collection.md)

- [Microsoft Defender for Identity community forum](<https://aka.ms/MDIcommunity>)


# Notifications

# Defender for Identity notifications in Microsoft Defender XDR

>[!NOTE]

>This feature is currently supported only by the Defender for Identity sensor version 2.x.

Microsoft Defender for Identity provides notifications for health issues and security alerts, either via email notifications or to a Syslog server.

This article describes how to configure Defender for Identity notifications so that you're aware of any health issues or security alerts detected.

> [!TIP]

> In addition to email or Syslog notifications, we recommend that SOC admins use Microsoft Sentinel to view all alerts in a single portal.

> For more information, see [Microsoft Defender XDR integration with Microsoft Sentinel](/azure/sentinel/microsoft-365-defender-sentinel-integration).

> To integrate other SIEM tools, see [Integrate your SIEM tools with Microsoft Defender XDR](/microsoft-365/security/defender/configure-siem-defender).

## Configure email notifications

This section describes how to configure email notifications for Defender for Identity health issues.

1. In [Microsoft Defender XDR](https://security.microsoft.com), select **Settings** > **Identities**.

1. Under **Notifications**, select **Health issues notifications**.

1. In the **Add recipient email**, enter the email address(es) where you want to receive email notifications, and select **+ Add**.

Whenever Defender for Identity detects a health issue, configured recipients receive an email notification with the details, with a link to Microsoft Defender XDR for more details.

> [!NOTE]

> To receive email notifications about Incidents, please use the [Email Notifications](https://security.microsoft.com/securitysettings/defender/email_notifications) page under Defender XDR Settings for new and existing notifications rules. [Learn more](https://aka.ms/IncidentsNotificationsDefenderXdr).

## Configure Syslog notifications

This section describes how to configure Defender for Identity to send health issues and security events to a Syslog server through a configured sensor.

Events aren't sent from the Defender for Identity service to your Syslog server directly, but only through the sensor.

**To configure Syslog notifications**:

1. In [Microsoft Defender XDR](https://security.microsoft.com), select **Settings** > **Identities**.

1. Under **Notifications**, select **Syslog notifications**, and then toggle on the **Syslog service** option.

1. Select **Configure service** to open the **Syslog service** pane.

1. Enter the following details:

- **Sensor**: Select the sensor you want to send notifications to the Syslog server.

- **Service endpoint** and **Port**: Enter the IP address or fully qualified domain name (FQDN) for the Syslog server, and then enter the port number. You can configure only one Syslog endpoint.

- **Transport**: Select the **Transport** protocol (TCP or UDP).

- **Format**: Select the format (RFC 3164 or RFC 5424).

1. Select **Send test SIEM notification** and then verify the message is received in your Syslog infrastructure solution.

1. When you've confirmed that the test works, select **Save**.

1. After configuring the Syslog service, select the types of notifications to send to your Syslog server, including whenever:

- A new security alert is detected

- An existing security alert is updated

- A new health issue is detected

> [!TIP]

> When working with Syslog in TLS mode, make sure to install the required certificates on the designated sensor.

## Creating automation scripts for Defender for Identity SIEM logs

If you're creating automation scripts for Defender for Identity SIEM logs, we recommend using the **externalId** field to identify the alert type instead of using the alert name.

While alert names may occasionally be modified, the **externalId** of each alert is permanent. For more information, see [Defender for Identity SIEM log reference](cef-format-sa.md).

## Related content

For more information, see [Configure event collection](deploy/configure-event-collection.md).


# Advanced Settings

# Adjust alert thresholds

This article describes how to configure the number of false positives by adjusting thresholds for specific Microsoft Defender for Identity alerts.

Some Defender for Identity alerts rely on *learning periods* to build a profile of patterns, and then distinguish between legitimate and suspicious activities. Each alert also has specific conditions within the detection logic to help distinguish between legitimate and suspicious activities, such as alert thresholds and filtering for popular activities.

Use the **Adjust alert thresholds** page to customize the threshold level for specific alerts to influence their alert volume. For example, if you're running comprehensive testing, you might want to lower alert thresholds to trigger as many alerts as possible.

Alerts are triggered immediately if the **Recommended test mode** option is selected, or if a threshold level is set to **Medium** or **Low**, regardless of whether the alert's learning period has already completed.

> [!NOTE]

> The **Adjust alert thresholds** page was previously named **Advanced settings**.

## Prerequisites

To view the **Adjust alerts thresholds** page in Microsoft Defender XDR, you need access at least as a *Security viewer*.

To make changes on the **Adjust alerts thresholds** page, you need access at least as a *Security administrator*.

## Define alert thresholds

We recommend changing alert thresholds from the default (**High**) only after careful consideration.

For example, if you have NAT or VPN, we recommend that you consider any changes to relevant detections carefully, including *Suspected DCSync attack (replication of directory services)* and *Suspected identity theft* detections.

**To define your alert thresholds**:

1. In [Microsoft Defender XDR](https://security.microsoft.com), go to **Settings** > **Identities** > **Adjust alert thresholds**.

1. Locate the alert where you want to adjust the alert threshold and select the threshold level you want to apply.

- **High** is the default value, and applies standard thresholds to reduce false positives.

- **Medium** and **Low** thresholds increase the number of alerts generated by Defender for Identity.

When you select **Medium** or **Low**, details are bolded in the **Information** column to help you understand how the change affects the alert behavior.

1. Select **Apply changes** to save changes.

> [!WARNING]

> Reverting to default is irreversible and any changes made to your threshold levels are lost.

1. To reset all alerts to the default threshold (**High**), select **Revert to default** and then **Apply changes**.

## Switch to Recommended test mode

The **Recommended test mode** option is designed to help you understand all Defender for Identity alerts, including some related to legitimate traffic and activities so that you can thoroughly evaluate Defender for Identity as efficiently as possible.

If you recently deployed Defender for Identity and want to test it, select the **Recommended test mode** option to switch all alert thresholds to **Low** and increase the number of alerts triggered.

Threshold levels are read-only when the **Recommended test mode** option is selected.

> [!NOTE]

> Test mode is time-limited to a maximum of 60 days.

> When turning on Recommended test mode, you must specify an end time. The selected end time is displayed next to the toggle for as long as test mode is enabled.

When you're finished testing, toggle the Recommended test mode option back off to return to your previous settings. Select **Apply changes** to save changes.

## Supported detections for threshold configurations

The following table describes the types of detections that support adjustments for threshold levels, including the effects of **Medium** and **Low** thresholds.

Cells marked with N/A indicate that the threshold level isn't supported for the detection.

| Detection | Medium | Low |

| --- | --- | --- |

| **[Security principal reconnaissance (LDAP)](credential-access-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)** | When set to **Medium**, this detection triggers alerts immediately, without waiting for a learning period, and also disables any filtering for popular queries in the environment.| When set to **Low**, all support for the **Medium** threshold applies, plus a lower threshold for queries, single scope enumeration, and more. |

| **[Suspicious additions to sensitive groups](persistence-privilege-escalation-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)** |N/A | When set to **Low**, this detection avoids the sliding window and ignores any previous learnings. |

| **[Suspected AD FS DKM key read](credential-access-alerts.md#suspected-ad-fs-dkm-key-read-external-id-2413)** |  N/A | When set to **Low**, this detection triggers immediately, without waiting for a learning period. |

| **[Suspected Brute Force attack (Kerberos, NTLM)](credential-access-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)** | When set to **Medium**, this detection ignores any learning done and has a lower threshold for failed passwords. | When set to **Low**, this detection ignores any learning done and has the lowest possible threshold for failed passwords. |

| **[Suspected DCSync attack (replication of directory services)](credential-access-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)** | When set to **Medium**, this detection triggers immediately, without waiting for a learning period. | When set to **Low**, this detection triggers immediately, without waiting for a learning period, and avoids IP filtering like NAT or VPN. |

| **[Suspected Golden Ticket usage (forged authorization data)](credential-access-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)** | N/A| When set to **Low**, this detection triggers immediately, without waiting for a learning period. |

| **[Suspected Golden Ticket usage (encryption downgrade)](persistence-privilege-escalation-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)** | N/A| When set to **Low**, this detection triggers an alert based on lower confidence resolution of a device. |

| **[Suspected identity theft (pass-the-ticket)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)** | N/A | When set to **Low**, this detection triggers immediately, without waiting for a learning period, and avoids IP filtering like NAT or VPN. |

| **[User and Group membership reconnaissance (SAMR)](reconnaissance-discovery-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)** | When set to **Medium**, this detection triggers immediately, without waiting for a learning period. | When set to **Low**, this detection triggers immediately and includes a lower alert threshold. |

For more information, see [Security alerts in Microsoft Defender for Identity](alerts-overview.md).

## Next step

For more information, see [Investigate Defender for Identity security alerts in Microsoft Defender XDR](manage-security-alerts.md).


# Troubleshooting Known Issues

# Troubleshooting Microsoft Defender for Identity known issues

This article describes how to troubleshoot known issues in Microsoft Defender for Identity.

## Sensor service fails to start

**Sensor log entries:**

`Warn DirectoryServicesClient CreateLdapConnectionAsync failed to retrieve group managed service account password. [DomainControllerDnsName=DC1.CONTOSO.LOCAL Domain=contoso.local UserName=mdiSvc01]`

### Cause 1

The domain controller doesn't have rights to access the password of the gMSA account.

**Resolution 1:**

Verify that the domain controller has rights to access the password. You should have a Security Group in Active Directory that contains the domain controller, Microsoft Entra Connect, Active Directory Federation Services (AD FS) / Active Directory Certificate Services (AD CS) server and standalone sensors computer accounts included. If the Security group doesn't exist, we recommend that you create one.

You can use the following command to check if a computer account or security group is added to the parameter. Replace *mdiSvc01* with the name you created.

```powershell

Get-ADServiceAccount mdiSvc01 -Properties PrincipalsAllowedToRetrieveManagedPassword

```

The results should look like this:

![Powershell results.](media/troubleshooting-known-issues/gmsa-retrieve-password-results.png)

In this example, we can see that a group named *mdiSvc01Group* is added. If the domain controller or the security group hasn't been added, you can use the following commands to add it. Replace *mdiSvc01* with the name of gMSA, and replace *DC1* with the name of the domain controller, or *mdiSvc01Group* with the name of the security group.

```powershell

# To set the specific domain controller only:

$specificDC = Get-ADComputer -Identity DC1

Set-ADServiceAccount mdiSvc01 -PrincipalsAllowedToRetrieveManagedPassword $specificDC

# To set a security group that contains the relevant computer accounts:

$group = Get-ADGroup -Identity mdiSvc01Group

Set-ADServiceAccount mdiSvc01 -PrincipalsAllowedToRetrieveManagedPassword $group

```

If the domain controller or security group is already added, but you're still seeing the error, you can try the following steps:

- Reboot the server to sync the recent changes

- Purge the Kerberos ticket, forcing the server to request a new Kerberos ticket. From an administrator command prompt, run the following command `klist -li 0x3e7 purge`

### Cause 2

Due to a known scenario related to Secure Time Seeding, the gMSA attribute PasswordLastSet can be set to a future date, causing the sensor to be unable to start.

The following command can be used to confirm if the gMSA account falls in the scenario, when the PasswordLastSet and LastLogonDate values show a future date:

```powershell

Get-ADServiceAccount mdiSvc01 -Properties PasswordLastSet, LastLogonDate

```

**Resolution 2:**

As an interim solution, a new gMSA can be created which has the correct date for the attribute. It’s advisable to open a support request with directory services to identify the root cause and explore options for a comprehensive resolution.

## Sensor failure communication error

If you receive the following sensor failure error:

```cmd

System.Net.Http.HttpRequestException:

An error occurred while sending the request. ---> System.Net.WebException:

Unable to connect to the remote server --->

System.Net.Sockets.SocketException: A connection attempt failed because the

connected party did not properly respond after a period of time, or established

connection failed because connected host has failed to respond...

```

**Resolution:**

Make sure that communication isn't blocked for localhost, TCP port 444. To learn more about Microsoft Defender for Identity prerequisites, see [ports](prerequisites.md#required-ports).

## Deployment log location

The Defender for Identity deployment logs are located in the temp directory of the user who installed the product. In the default installation location, it can be found at: **C:\Users\Administrator\AppData\Local\Temp** (or one directory above **%temp%**). For more information, see [Troubleshooting Defender for Identity using logs](troubleshooting-using-logs.md).

## Proxy authentication problem presents as a licensing error

If during sensor installation you receive the following error:  **The sensor failed to register due to licensing issues.**

**Deployment log entries:**

`[1C60:1AA8][2018-03-24T23:59:13]i000: 2018-03-25 02:59:13.1237 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [validateCreateSensorResult=LicenseInvalid]]`

`[1C60:1AA8][2018-03-24T23:59:56]i000: 2018-03-25 02:59:56.4856 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [validateCreateSensorResult=LicenseInvalid]]`

`[1C60:1AA8][2018-03-25T00:27:56]i000: 2018-03-25 03:27:56.7399 Debug SensorBootstrapperApplication Engine.Quit [deploymentResultStatus=1602 isRestartRequired=False]]`

`[1C60:15B8][2018-03-25T00:27:56]i500: Shutting down, exit code: 0x642`

**Cause:**

In some cases, when communicating via a proxy, during authentication it might respond to the Defender for Identity sensor with error 401 or 403 instead of error 407. The Defender for Identity sensor interprets error 401 or 403 as a licensing issue and not as a proxy authentication issue.

**Resolution:**

Ensure that the sensor can browse to *.atp.azure.com through the configured proxy without authentication. For more information, see [Configure proxy to enable communication](configure-proxy.md).

## Proxy authentication problem presents as a connection error

If during sensor installation you receive the following error: **The sensor failed to connect to service.**

**Cause:**

The issue can be caused when the trusted root certification authorities certificates required by Defender for Identity are missing.

**Resolution:**

Run the following PowerShell cmdlet to verify that the required certificates are installed.

In the following example, the "DigiCert Global Root G2" certificate is for commercial customers and the "DigiCert Global Root CA" certificate for US Government GCC High customers, as indicated.

```powershell

# Certificate for commercial customers

Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "AA11BB22CC33DD44EE55FF66AA77BB88CC99DD00"} | fl

# Certificate for US Government GCC High customers

Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "BB22CC33DD44EE55FF66AA77BB88CC99DD00EE11"} | fl

```

Output for certificate for commercial customers certificate:

```Output

Subject      : CN=DigiCert Global Root G2, OU=www.digicert.com, O=DigiCert Inc, C=US

Issuer       : CN=DigiCert Global Root G2, OU=www.digicert.com, O=DigiCert Inc, C=US

Thumbprint   : AA11BB22CC33DD44EE55FF66AA77BB88CC99DD00

FriendlyName : DigiCert Global Root G2

NotBefore    : 01/08/2013 15:00:00

NotAfter     : 15/01/2038 14:00:00

Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}

```

Output for certificate for US Government GCC High customers:

```Output

Subject      : CN=DigiCert Global Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US

Issuer       : CN=DigiCert Global Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US

Thumbprint   : BB22CC33DD44EE55FF66AA77BB88CC99DD00EE11

FriendlyName : DigiCert

NotBefore    : 11/9/2006 4:00:00 PM

NotAfter     : 11/9/2031 4:00:00 PM

Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}

```

If you don't see the expected output, use the following steps:

1. Download the following certificates to the machine:

- For commercial customers, download the [DigiCert Global Root G2](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt) certificate

- For US Government GCC High customers, download the [DigiCert Global Root CA](https://cacerts.digicert.com/DigiCertGlobalRootCA.crt) certificate

1. Run the following PowerShell cmdlet to install the certificate.

```powershell

# For commercial customers, install certificate

Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\DigiCertGlobalRootG2.crt" -CertStoreLocation Cert:\LocalMachine\Root

# For US Government GCC High customers, install certificate

Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\DigiCertGlobalRootCA.crt" -CertStoreLocation Cert:\LocalMachine\Root

```

## Silent installation error when attempting to use PowerShell

If during silent sensor installation you attempt to use PowerShell and receive the following error:

```powershell

"Azure ATP sensor Setup.exe" "/quiet" NetFrameworkCommandLineArguments="/q" Acce ... Unexpected token '"/quiet"' in expression or statement."

```

**Cause:**

Failure to include the ./ prefix required to install when using PowerShell causes this error.

**Resolution:**

Use the complete command to successfully install.

```powershell

./"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"

```

## Defender for Identity sensor NIC teaming issue

When you install the Defender for Identity sensor on a machine configured with a NIC teaming adapter and the Winpcap driver, you receive an installation error. If you want to install the Defender for Identity sensor on a machine configured with NIC teaming, make sure you replace the Winpcap driver with Npcap by following the [instructions here](/defender-for-identity/technical-faq#how-do-i-download-and-install-or-upgrade-the-npcap-driver).

## Multiprocessor Group mode

For Windows Operating systems 2008R2 and 2012, the Defender for Identity sensor isn't supported in a Multiprocessor Group mode.

Suggested possible workarounds:

- If hyper threading is on, turn it off. This might reduce the number of logical cores enough to avoid needing to run in **Multiprocessor Group** mode.

- If your machine has less than 64 logical cores and is running on an HP host, you might be able to change the **NUMA Group Size Optimization** BIOS setting from the default of **Clustered** to **Flat**.

## VMware virtual machine sensor issue

If you have a Defender for Identity sensor on VMware virtual machines, you might receive one or both of the following health alerts **Some network traffic is not being analyzed** and **Network configuration mismatch for sensors running on VMware**. This can happen because of a configuration mismatch in VMware Guest OS NIC and [MDI Sensor requirements](deploy/prerequisites-sensor-version-2.md#server-requirements).

To resolve the issue:

On the Guest OS, set the following to **Disabled** in the virtual machine's NIC configuration: **IPv4 TSO Offload**.

![VMware sensor issue.](media/vm-sensor-issue.png)

Use the following command to check if Large Send Offload (LSO) is enabled or disabled:

`Get-NetAdapterAdvancedProperty | Where-Object DisplayName -Match "^Large*"`

![Check LSO status.](media/missing-network-traffic-health-alert.png)

If LSO is enabled, use the following command to disable it:

`Disable-NetAdapterLso -Name {name of adapter}`

![Disable LSO status.](media/disable-lso-vmware.png)

> [!NOTE]

>

> - Depending on your configuration, these actions might cause a brief loss of network connectivity.

> - You might need to restart your machine for these changes to take effect.

> - These steps might vary depending on your VMware version. Check VMware documentation for information about how to disable LSO/TSO for your VMware version.

## Sensor failed to retrieve group managed service account (gMSA) credentials

If you receive the following health alert: **Directory services user credentials are incorrect**

**Sensor log entries:**

`2020-02-17 14:01:36.5315 Info ImpersonationManager CreateImpersonatorAsync started [UserName=account_name Domain=domain1.test.local IsGroupManagedServiceAccount=True]`

`2020-02-17 14:01:36.5750 Info ImpersonationManager CreateImpersonatorAsync finished [UserName=account_name Domain=domain1.test.local IsSuccess=False]`

**Sensor Updater log entries:**

`2020-02-17 14:02:19.6258 Warn GroupManagedServiceAccountImpersonationHelper GetGroupManagedServiceAccountAccessTokenAsync failed GMSA password could not be retrieved [errorCode=AccessDenied AccountName=account_name DomainDnsName=domain1.test.local]`

The sensor failed to retrieve the password of the gMSA account.

### Cause 1

The domain controller doesn't have permissions to retrieve the password of the gMSA account.

**Resolution 1**:

Validate that the computer running the sensor has been granted permissions to retrieve the password of the gMSA account. For more information, see [Grant permissions to retrieve the gMSA account's password](deploy/create-directory-service-account-gmsa.md#prerequisites).

### Cause 2

The sensor service runs as *LocalService* and performs impersonation of the Directory Service account.

If the user rights assignment policy **Log on as a service** is configured for this domain controller, impersonation fails unless the gMSA account is granted the **Log on as a service** permission.

**Resolution 2**:

Configure **Log on as a service** for the gMSA accounts, when the user rights assignment policy **Log on as a service** is configured on the affected domain controller. For more information, see [Verify that the gMSA account has the required rights](deploy/create-directory-service-account-gmsa.md#verify-that-the-gmsa-account-has-the-required-rights).

### Cause 3

If the domain controller Kerberos ticket was issued before the domain controller was added to the security group with the proper permissions, this group won't be part of the Kerberos ticket. So it can't retrieve the password of the gMSA account.

**Resolution 3**:

Do one of the following to resolve this issue:

- Reboot the domain controller.

- Purge the Kerberos ticket, forcing the domain controller to request a new Kerberos ticket. From an administrator command prompt on the domain controller, run the following command:

`klist -li 0x3e7 purge`

- Assign the permission to retrieve the gMSA's password to a group the domain controller is already a member of, such as the Domain Controllers group.

## Access to the registry key 'Global' is denied

The sensor service fails to start, and the sensor log contains an entry similar to:

`2021-01-19 03:45:00.0000 Error RegistryKey System.UnauthorizedAccessException: Access to the registry key 'Global' is denied.`

**Cause:**

The gMSA configured for this domain controller or AD FS / AD CS server doesn't have permissions to the performance counter's registry keys.

**Resolution:**

Add the gMSA to the **Performance Log Users** group on the server.

## Report downloads can't contain more than 300,000 entries

Defender for Identity doesn't support report downloads that contain more than 300,000 entries per report. Reports render as incomplete if more than 300,000 entries are included.

**Cause:**

This is an engineering limitation.

**Resolution:**

No known resolution.

## Sensor fails to enumerate event logs

If you observe a limited number, or lack of, security event alerts or logical activities within the Defender for Identity console but no health issues are triggered.

**Sensor log entries:**

`Error EventLogException System.Diagnostics.Eventing.Reader.EventLogException: The handle is invalid

at void System.Diagnostics.Eventing.Reader.EventLogException.Throw(int errorCode)

at object System.Diagnostics.Eventing.Reader.NativeWrapper.EvtGetEventInfo(EventLogHandle handle, EvtEventPropertyId enumType)

at string System.Diagnostics.Eventing.Reader.EventLogRecord.get_ContainerLog()`

**Cause:**

A Discretionary Access Control List is limiting access to the required event logs by the Local Service account.

**Resolution:**

Ensure that the Discretionary Access Control List (DACL) includes the following entry (this is the SID of the AATPSensor service).

`(A;;0x1;;;S-1-5-80-818380073-2995186456-1411405591-3990468014-3617507088)`

Check if the DACL for the Security Event Log was configured by a GPO:

`Policies > Administrative Templates > Windows Components > Event Log Service > Security > Configure log access`

Append the entry above to the existing policy. Run `C:\Windows\System32\wevtutil.exe gl security` afterwards to verify that the entry was added.

The local Defender for Identity logs should now display:

`Info WindowsEventLogReader EnableEventLogWatchers EventLogWatcher enabled [name=Security]`

## ApplyInternal failed two way SSL connection to service error

If during the sensor installation you receive the following error: **ApplyInternal failed two way SSL connection to service** and the sensor log contains an entry similar to:

``2021-01-19 03:45:00.0000 Error CommunicationWebClient+\<SendWithRetryAsync\>d__9`1``

ApplyInternal failed two way SSL connection to service.

The issue can be caused by a proxy with SSL inspection enabled.

[_workspaceApplicationSensorApiEndpoint=Unspecified/contoso.atp.azure.com:443 Thumbprint=CC33DD44EE55FF66AA77BB88CC99DD00EE11FF22]`

**Cause:**

The issue can be caused when the **SystemDefaultTlsVersions** or **SchUseStrongCrypto** registry values aren't set to their default value of 1.

**Resolution:**

Verify the **SystemDefaultTlsVersions** and **SchUseStrongCrypto** registry values are set to 1:

```reg

Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]

"SystemDefaultTlsVersions"=dword:00000001

"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]

"SystemDefaultTlsVersions"=dword:00000001

"SchUseStrongCrypto"=dword:00000001

```

<a name="problem-installing-the-sensor-on-windows-server-2019-with-kb5009557-installed"></a>

## Problem installing the sensor on Windows Server 2019 with KB5009557 installed, or on a server with hardened EventLog permissions

Installing the sensor may fail with the error message:

`System.UnauthorizedAccessException: Attempted to perform an unauthorized operation.`

**Resolution:**

There are two possible workarounds for this issue:

1. Install the sensor with PSExec:

```cmd

psexec -s -i "C:\MDI\Azure ATP Sensor Setup.exe"

```

1. Install the sensor with a Scheduled Task configured to run as **LocalSystem**. The command-line syntax to use is mentioned in [Defender for Identity sensor silent installation](install-sensor.md#defender-for-identity-sensor-silent-installation).

## Sensor installation fails due to certificate management client

If the sensor installation fails, and the Microsoft.Tri.Sensor.Deployment.Deployer.log file contains an entry similar to:

`2022-07-15 03:45:00.0000 Error IX509CertificateRequestCertificate2 Deployer failed [arguments=128Ve980dtms0035h6u3Bg==] System.Runtime.InteropServices.COMException (0x80090008): CertEnroll::CX509CertificateRequestCertificate::Encode: Invalid algorithm specified. 0x80090008 (-2146893816 NTE_BAD_ALGID)`

**Cause:**

The issue can be caused when a certificate management client such as Entrust Entelligence Security Provider (EESP) is preventing the sensor installation from creating a self-signed certificate on the machine.

**Resolution:**

Uninstall the certificate management client, install the Defender for Identity sensor, and then reinstall the certificate management client.

>[!NOTE]

>

> The self-signed certificate is renewed every two years, and the autorenewal process might fail if the certificate management client prevents the self-signed certificate creation.

> This causes the sensor to stop communicating with the backend, which requires a sensor reinstallation using the workaround mentioned above.

## Sensor installation fails due to network connectivity issues

If the sensor installation fails with an error code of 0x80070643, and the installation log file contains an entry similar to:

`[22B8:27F0][2016-06-09T17:21:03]e000: Error 0x80070643: Failed to install MSI package.`

**Cause:**

The issue can be caused when the installation process can't access the Defender for Identity cloud services for the sensor registration.

**Resolution:**

Ensure that the sensor can browse to \*.atp.azure.com directly or through the configured proxy. If needed, set the proxy server settings for the installation using the command line:

`"Azure ATP sensor Setup.exe" [ProxyUrl="http://proxy.internal.com"] [ProxyUserName="domain\proxyuser"] [ProxyUserPassword="ProxyPassword"]`

For more information, see [Run a silent installation with a proxy configuration](install-sensor.md#run-a-silent-installation-with-a-proxy-configuration) and [Install the Microsoft Defender for Identity sensor](deploy/install-sensor.md).

> [!IMPORTANT]

> Microsoft recommends that you use the most secure authentication flow available. The authentication flow described in this procedure requires a very high degree of trust in the application, and carries risks that aren't present in other flows. You should only use this flow when other more secure flows, such as managed identities, aren't viable.

## Sensor service couldn't run and remains in Starting state

The following errors will appear in the **System log** in **Event viewer**:

- The Open procedure for service ".NETFramework" in DLL "C:\Windows\system32\mscoree.dll" failed with error code Access is denied. Performance data for this service won't be available.

- The Open procedure for service "Lsa" in DLL "C:\Windows\System32\Secur32.dll" failed with error code Access is denied. Performance data for this service won't be available.

- The Open procedure for service "WmiApRpl" in DLL "C:\Windows\system32\wbem\wmiaprpl.dll" failed with error code "The device isn't ready". Performance data for this service won't be available.

The Microsoft.TriSensorError.log will contain an error similar to this:

`Microsoft.Tri.Sensor.DirectoryServicesClient.TryCreateLdapConnectionAsync(DomainControllerConnectionData domainControllerConnectionData, bool isGlobalCatalog, bool isTraversing)

2021-07-13 14:56:20.2976 Error DirectoryServicesClient Microsoft.Tri.Infrastructure.ExtendedException: Failed to communicate with configured domain controllers

at new Microsoft.Tri.Sensor.DirectoryServicesClient(IConfigurationManager`

**Cause:**

NT Service\All Services don't have the right to log on as a service.

**Resolution:**

Add Domain Controller Policy with the logon as a service. For more information, see [Verify that the gMSA account has the required rights](deploy/create-directory-service-account-gmsa.md#verify-that-the-gmsa-account-has-the-required-rights).

<a name='your-workspace-wasnt-created-because-a-security-group-with-the-same-name-already-exists-in-azure-active-directory'></a>

## Your workspace wasn't created because a security group with the same name already exists in Microsoft Entra ID

**Cause:**

The issue can come up when a Defender for Identity workspace license expires and is deleted when the retention period has ended, but the Microsoft Entra groups weren't deleted.

**Resolution:**

1. Go to the [Azure portal](https://portal.azure.com/) -> [Microsoft Entra ID](https://portal.azure.com/#view/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/~/Overview) -> [Groups](https://portal.azure.com/#view/Microsoft_AAD_IAM/GroupsManagementMenuBlade/~/AllGroups)

1. Rename the following three groups (where workspaceName is the name of your workspace), by adding to them a " - old" suffix:

- "Azure ATP workspaceName Administrators" -> "Azure ATP workspaceName Administrators - old"

- "Azure ATP workspaceName Viewers" -> "Azure ATP workspaceName Viewers - old"

- "Azure ATP workspaceName Users" -> "Azure ATP workspaceName Users - old"

1. Then you can go back in the [Microsoft Defender portal](https://security.microsoft.com), to the [Settings](https://security.microsoft.com/securitysettings) -> [Identities](https://security.microsoft.com/settings/identities) section to create the new workspace for Defender for Identity.

## Entra Connect sensor experiences loss of database permissions following the update to Microsoft Entra Connect

**Cause:**

Updating Microsoft Entra Connect might cause the Entra Connect sensor to lose previously configured database permissions. To investigate, check the Microsoft Defender logs for relevant indicators. Refer to [Troubleshooting Microsoft Defender for Identity sensor using the Defender for Identity logs](troubleshooting-using-logs.md) for log locations and further details.

Sample logs that might indicate the issue:

`GetEntraConnectGlobalSettingsAsync GetEntraConnectGlobalSettingsAsync failed. Exception - The EXECUTE permission was denied on the object 'mms_get_globalsettings', database Contoso', schema 'dbo'`

`GetEntraConnectConnectivityParametersAsync GetEntraConnectConnectivityParametersAsync failed. Exception - The EXECUTE permission was denied on the object 'mms_get_connectors', database Contoso, schema 'dbo'`

**Resolution:**

If permissions need to be reconfigured, follow the steps outlined in this [guide](deploy/active-directory-federation-services.md).

## Auditing health alerts persist on sensor v3

In some v3 sensor environments, auditing health alerts might persist even when Windows auditing is correctly configured. This primarily occurs with manual auditing configuration, such as using Group Policy or PowerShell. The sensor remains healthy and detections aren't affected. To resolve, enable **Automatic Windows auditing configuration** in the Defender for Identity portal under **Settings** > **Advanced features**.

## Windows Server 2025 sensor v3.x migration not supported

Migrating domain controllers running Windows Server 2025 to sensor v3.x isn't currently supported. Continue using the v2.x sensor on Windows Server 2025 domain controllers until support for migration to v3.x is available.

## Next steps

- [Defender for Identity sensor v2.x prerequisites](deploy/prerequisites-sensor-version-2.md) and [Defender for Identity sensor v3.x prerequisites](deploy/deploy-sensor-v3.md)

- [Defender for Identity capacity planning](deploy/capacity-planning.md)

- [Configure event collection](deploy/configure-event-collection.md)

- [Configuring Windows event forwarding](deploy/configure-event-forwarding.md)

- [Check out the Defender for Identity forum!](<https://aka.ms/MDIcommunity>)


# Troubleshooting Using Logs

# Troubleshooting Microsoft Defender for Identity sensor using the Defender for Identity logs

The Defender for Identity logs provide insight into what each component of Microsoft Defender for Identity sensor is doing at any given point in time.

The Defender for Identity logs are located in a subfolder called **Logs** where Defender for Identity is installed; the default location is: `C:\Program Files\Azure Advanced Threat Protection Sensor`. In the default installation location, it can be found at: `C:\Program Files\Azure Advanced Threat Protection Sensor\version number\Logs`.

## Defender for Identity sensor logs

The Defender for Identity sensor has the following logs:

- **Microsoft.Tri.Sensor.log** – This log contains everything that happens in the Defender for Identity sensor (including resolution and errors). Its main use is getting the overall status of all operations in the chronological order in which they occurred.

- **Microsoft.Tri.Sensor-Errors.log** – This log contains just the errors that are caught by the Defender for Identity sensor. Its main use is performing health checks and investigating issues that need to be correlated to specific times.

- **Microsoft.Tri.Sensor.Updater.log** - This log is used for the sensor updater process, which is responsible for updating the Defender for Identity sensor if configured to do so automatically.

- **Microsoft.Tri.Sensor.Updater-Errors.log** – This log contains just the errors that are caught by the Defender for Identity sensor updater. Its main use is performing health checks and investigating issues that need to be correlated to specific times.

> [!NOTE]

> The log files have a maximum size of up to 50 MB. When that size is reached, a new log file is opened and the previous one is renamed to "&lt;original file name&gt;-Archived-00000" where the number increments each time it is renamed. By default, if more than 10 files from the same type already exist, the oldest are deleted.

## Defender for Identity deployment logs

The Defender for Identity deployment logs are located in the temp directory of the user who installed the product. Typically, you can find these logs at `%USERPROFILE%\AppData\Local\Temp`. If the deployment was performed by a service, the logs might be located in `C:\Windows\Temp` or `C:\Windows\SystemTemp`, depending on your Windows version and patch level.

Defender for Identity sensor deployment logs:

- **Azure Advanced Threat Protection Microsoft.Tri.Sensor.Deployment.Deployer_YYYYMMDDHHMMSS.log** - This log file provides the entire process of sensor deployment and can be found in the temp folder mentioned previously.

- **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS.log** - This log lists the steps in the process of the deployment of the Defender for Identity sensor. Its main use is tracking the Defender for Identity sensor deployment process.

- **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS_001_MsiPackage.log** - This log file lists the steps in the process of the deployment of the Defender for Identity sensor binaries. Its main use is tracking the deployment of the Defender for Identity sensor binaries.

> [!NOTE]

> In addition to the deployment logs mentioned here, there are other logs that begin with "Azure Advanced Threat Protection" that can also provide additional information on the deployment process.

## Related content

- [Defender for Identity sensor v2.x prerequisites](deploy/prerequisites-sensor-version-2.md) and [Defender for Identity sensor v3.x prerequisites](deploy/deploy-sensor-v3.md)

- [Defender for Identity capacity planning](deploy/capacity-planning.md)

- [Configure event collection](deploy/configure-event-collection.md)

- [Configuring Windows event forwarding](deploy/configure-event-forwarding.md)

- [Check out the Defender for Identity forum!](<https://aka.ms/MDIcommunity>)


# Ops Guide

# Microsoft Defender for Identity operational guide

This article summarizes the Microsoft Defender for Identity activities we recommend for your team on a daily, weekly, and monthly basis.

|Cadence  |Tasks  |

|---------|---------|

|**Daily**     | - [Triage incidents by priority](ops-guide-daily.md#triage-incidents-by-priority) <br>- [Configure tuning rules for benign true positives / false positive alerts](ops-guide-daily.md#configure-tuning-rules-for-benign-true-positives--false-positive-alerts)<br> - [Review the Identity Security dashboard](ops-guide-daily.md#review-the-identity-security-dashboard) <br>- [Proactively hunt](ops-guide-daily.md#proactively-hunt) <br> - [Review Defender for Identity health issues](ops-guide-daily.md#review-defender-for-identity-health-issues)   |

|**Weekly**     |- [Review Secure score recommendations](ops-guide-weekly.md#review-secure-score-recommendations) <br>  - [Review and respond to emerging threats](ops-guide-weekly.md#review-and-respond-to-emerging-threats) <br>- [Proactively hunt](ops-guide-weekly.md#proactively-hunt)   |

|**Monthly**     | - [Review tuned alerts and adjust tuning if needed](ops-guide-monthly.md#review-tuned-alerts-and-adjust-tuning-if-needed) <br> - [Track new changes in Microsoft Defender XDR and Defender for Identity](ops-guide-monthly.md#track-new-changes-in-microsoft-defender-xdr-and-defender-for-identity)     |

| **Quarterly / Ad hoc** <br>Depending on your organization's needs and processes | - [Review Microsoft service health](ops-guide-quarterly.md#review-microsoft-service-health) <br> - [Review server setup process to include sensors](ops-guide-quarterly.md#review-server-setup-process-to-include-sensors) <br>- [Check domain configuration via PowerShell](ops-guide-quarterly.md#check-domain-configuration-via-powershell) |

You might want to proactively hunt on a daily or weekly basis, depending on your level as a SOC analyst.

## Related content

- [Daily operational guide](ops-guide-daily.md)

- [Weekly operational guide](ops-guide-weekly.md)

- [Monthly operational guide](ops-guide-monthly.md)

- [Quarterly / Ad hoc operational guide](ops-guide-quarterly.md)

- The Microsoft Defender [Security operations overview](/security/operations/overview).


# Ops Guide Daily

# Daily operational guide - Microsoft Defender for Identity

This article reviews the Microsoft Defender for Identity activities we recommend for your team on a daily basis.

## Review the Identity Security dashboard

**Where**: In Microsoft Defender, under select **Identities** > **Dashboard**.

**Persona**: SOC analysts, security administrators, identity, and access management administrators

Use Defender for Identity's **Dashboard** page to view critical insights and real-time data about identity security. On a daily basis, we recommend that you focus on the **Top insights**, **Identity related incidents**, and **Entra ID users at risk** widgets.

For more information, see [Work with Defender for Identity's Identity Security dashboard (Preview)](../dashboard.md).

## Triage incidents by priority

**Where**: In Microsoft Defender, select **Incidents & alerts**

**Persona**: SOC analysts

**When triaging incidents**:

1. In the incident dashboard, filter for the following items:

|Filter   |Values  |

|---------|---------|

|**Status**     |   New, In progress      |

|**Severity**     |  High, Medium, Low       |

|**Service source**     |  Keep all service sources checked. This selection should list alerts with the most fidelity, with correlation across other Microsoft XDR workloads. Select **Defender for Identity** to view items that come specifically from Defender for Identity.       |

1. Select each incident to review all details. Review all tabs in the incident, the activity log, and advanced hunting.

1. In the incident's **Evidence and response** tab, select each evidence item. Select the options menu > **Investigate** and then select **Activity log** or **Go hunt** as needed.

1. Triage your incidents. For each incident, select **Manage incident** and then select one of the following options:

- True positive

- False positive

- Informational, expected activity

For true alerts, specify the threat type to help your security team see threat patterns and defend your organization from risk.

1. When you're ready to start your active investigation, assign the incident to a user and update the incident status to **In progress**.

1. When the incident is remediated, resolve it to resolve all linked and related active alerts and set a classification.

## Configure tuning rules for benign true positives / false positive alerts

**Where**: In Microsoft Defender, select **Hunting > Advanced hunting**

**Persona**: Security and compliance administrators, SOC analysts

If you find either benign true positives or outright false positives, we recommend that you tune your alerts to reduce the number of alerts you need to triage to match your risk appetite. Tuning alerts resolves alerts automatically based on your configurations and rule conditions.

We recommend creating new rules as needed as your network grows to make sure that your alert tuning remains relevant and effective.

For more information, see [Tune an alert](/microsoft-365/security/defender/investigate-alerts#tune-an-alert).

## Proactively hunt

**Where**: In Microsoft Defender, select **Hunting > Advanced hunting**.

**Persona**: SOC analysts

You might want to proactively hunt on a daily or weekly basis, depending on your level as a SOC analyst.

Use Microsoft Defender advanced hunting to proactively explore through the last 30 days of raw data, including Defender for Identity data correlated with data streaming from other Microsoft Defender services.

Inspect events in your network to locate threat indicators and entities, including both known and potential threats.

We recommend that beginners use guided advanced hunting, which provides a query builder. If you're comfortable using Kusto Query Language (KQL), build queries from scratch as needed for your investigations.

For more information, see [Proactively hunt for threats with advanced hunting in Microsoft Defender](/microsoft-365/security/defender/advanced-hunting-overview).

## Review Defender for Identity health issues

**Where**: In Microsoft Defender, select **Identities > Health issues**.

**Persona**: Security administrators, Active Directory administrators

We recommend checking the **Health Issues** page regularly to check for any problems in your Defender for Identity deployment, such as connectivity or sensor issues. Make sure to check both the **Global** and **Sensor** tabs to view both types of issues.

We also recommend setting up email notifications for service issues so that you can catch issues as they happen.

For more information, see [Microsoft Defender for Identity health issues](../health-alerts.md) and [Configure email notifications](../notifications.md#configure-email-notifications).

## Related content

For more information, see:

- [Microsoft Defender Security operations overview](/security/operations/overview)

- [Microsoft Defender for Identity operational guide](ops-guide.md)

- [Weekly operational guide - Microsoft Defender for Identity](ops-guide-weekly.md)

- [Monthly operational guide - Microsoft Defender for Identity](ops-guide-monthly.md)

- [Quarterly / Ad hoc operational guide - Microsoft Defender for Identity](ops-guide-quarterly.md)


# Ops Guide Weekly

# Weekly operational guide - Microsoft Defender for Identity

This article reviews the Microsoft Defender for Identity activities we recommend for your team on a weekly basis.

## Review Secure score recommendations

**Where**: In Microsoft Defender, select **Secure score**.

**Persona**: Security and compliance administrators, SOC analysts

Microsoft Secure score recommendations are based on the Microsoft security recommendations that are most relevant to your organization. Secure score recommendations for Defender for Identity include monitoring for on-premises identities and identity infrastructure weak points.

To view Secure Score recommendations per product, in Microsoft Defender, select **Secure score > Recommended actions**, and group the list by **Product**.

For more information, see:

- [Microsoft Defender for Identity's security posture assessments](../security-assessment.md)

- [Microsoft Secure Score](/microsoft-365/security/defender/microsoft-secure-score)

## Review and respond to emerging threats

**Where**: In Microsoft Defender, select **Hunting > Advanced hunting**

**Persona**: Security and compliance administrators, SOC analysts

We recommend that you configure custom detections in Microsoft Defender to monitor and respond to various events and system states, such as suspected breach activity and misconfigured endpoints.

Custom detection rules can automatically trigger both alerts and response actions, and are based on advanced hunting queries. Run your custom detection rules regularly to generate alerts and take relevant response actions.

For more information, see:

- [Custom detections overview](/microsoft-365/security/defender/custom-detections-overview)

- [Create and manage custom detections rules](/microsoft-365/security/defender/custom-detection-rules)

## Proactively hunt

**Where**: In Microsoft Defender, select **Hunting > Advanced hunting**.

**Persona**: SOC analysts

You might want to proactively hunt on a daily or weekly basis, depending on your level as a SOC analyst.

Use Microsoft Defender advanced hunting to proactively explore through the last 30 days of raw data, including Defender for Identity data correlated with data streaming from other Microsoft Defender services.

Inspect events in your network to locate threat indicators and entities, including both known and potential threats.

We recommend that beginners use guided advanced hunting, which provides a query builder. If you're comfortable using Kusto Query Language (KQL), build queries from scratch as needed for your investigations.

For more information, see [Proactively hunt for threats with advanced hunting in Microsoft Defender](/microsoft-365/security/defender/advanced-hunting-overview).

## Related content

For more information, see:

- [Microsoft Defender Security operations overview](/security/operations/overview)

- [Microsoft Defender for Identity operational guide](ops-guide.md)

- [Daily operational guide - Microsoft Defender for Identity](ops-guide-daily.md)

- [Monthly operational guide - Microsoft Defender for Identity](ops-guide-monthly.md)

- [Quarterly / Ad hoc operational guide - Microsoft Defender for Identity](ops-guide-quarterly.md)


# Ops Guide Monthly

# Monthly operational guide - Microsoft Defender for Identity

This article reviews the Microsoft Defender for Identity activities we recommend for your team on a monthly basis.

## Review tuned alerts and adjust tuning if needed

**Where**: In Microsoft Defender, select **Hunting > Advanced hunting**

**Persona**: Security and compliance administrators, SOC analysts

Microsoft Defender allows you to *tune* alerts, helping you reduce the number of alerts you need to triage. Tuning alerts resolves alerts automatically based on your configurations and rule conditions.

We recommend reviewing your tuning configurations regularly to make sure that they're still relevant and effective. For example:

- Check to see if your existing rules have matches as expected

- If a rule has no matches, consider whether you still need it or if you can remove it

For more information, see [Investigate Defender for Identity security alerts in Microsoft Defender](../manage-security-alerts.md).

<a name="track-new-changes-in-microsoft-defender-xdr-and-defender-for-identity"></a>

## Track new changes in Microsoft Defender and Defender for Identity

**Where**:

- In the Microsoft 365 admin center, select **Health > Message center**. For more information, see [Track new and changed features in the Microsoft 365 Message center](/microsoft-365/admin/manage/message-center).

- The [Microsoft Defender XDR monthly news](https://techcommunity.microsoft.com/t5/microsoft-defender-xdr-blog/bg-p/MicrosoftThreatProtectionBlog/label-name/Defender%20News).

- For details about Defender for Identity updates, see [What's new in Microsoft Defender for Identity](../whats-new.md).

**Persona**: Security administrators, SOC analysts

## Related content

For more information, see:

- [Microsoft Defender Security operations overview](/security/operations/overview)

- [Microsoft Defender for Identity operational guide](ops-guide.md)

- [Daily operational guide - Microsoft Defender for Identity](ops-guide-daily.md)

- [Weekly operational guide - Microsoft Defender for Identity](ops-guide-weekly.md)

- [Quarterly / Ad hoc operational guide - Microsoft Defender for Identity](ops-guide-quarterly.md)


# Ops Guide Quarterly

# Quarterly / ad hoc operational guide - Microsoft Defender for Identity

This article reviews the Microsoft Defender for Identity activities we recommend for your team on a quarterly or ad-hoc basis, depending on your organization's needs and processes.

Perform ad hoc activities as issues arise in your organization, or as part of a quarterly operational review.

## Review Microsoft service health

**Where**: Check the following locations:

- In the Microsoft 365 admin center, select **Health > Service health**

- [Microsoft 365 Service health status](https://status.office365.com/)

- X: https://twitter.com/MSFT365status

**Persona**: Security and compliance administrators

If you're experiencing issues with a cloud service, we recommend checking service health updates to determine whether it's a known issue, with a resolution in progress, before you call support or spend time troubleshooting.

For more information, see [Review Defender for Identity health issues](ops-guide-daily.md#review-defender-for-identity-health-issues).

## Review server setup process to include sensors

**Where**: Your organization's internal process documentation

**Persona**: Security administrators

We recommend that you periodically verify your organization's server setup process to make sure that it includes installing the Defender for Identity sensor. This ensures that all new domain controllers, AD CS, and AD FS servers are protected right away.

For more information, see [Deploy Microsoft Defender for Identity with Microsoft Defender](../deploy/deploy-defender-identity.md).

## Check domain configuration via PowerShell

**Where**: PowerShell on your Defender for Identity sensor machines

**Persona**: Security administrators

We recommend that you periodically run the **Test-MDIConfiguration** PowerShell command to test whether your domain controller Advanced Audit Policy settings are configured correctly. Misconfigured Advanced Audit Policy settings can cause gaps in the Event Log and incomplete Defender for Identity coverage.

For more information, see:

- [Configure audit policies for Windows event logs](../deploy/configure-windows-event-collection.md)

- [Test-MDIConfiguration](/powershell/module/defenderforidentity/test-mdiconfiguration) PowerShell documentation

## Related content

For more information, see:

- [Microsoft Defender Security operations overview](/security/operations/overview)

- [Microsoft Defender for Identity operational guide](ops-guide.md)

- [Daily operational guide - Microsoft Defender for Identity](ops-guide-daily.md)

- [Weekly operational guide - Microsoft Defender for Identity](ops-guide-weekly.md)

- [Monthly operational guide - Microsoft Defender for Identity](ops-guide-monthly.md)


# Cef Format Sa

# Microsoft Defender for Identity SIEM log reference

Defender for Identity can forward security alert and health alert events to your SIEM. Alerts and events are in the CEF format. This reference article provides samples of the logs sent to your SIEM.

> [!NOTE]

> We recommend using the streaming API or REST APIs to [Integrate your SIEM tools with Microsoft Defender XDR](/defender-xdr/configure-siem-defender). This approach enables you to forward all events and alerts from all Defender XDR products, rather than just the Defender for Identity events and alerts.

## Sample Defender for Identity security alerts in CEF format

The following fields and their values are forwarded to your SIEM:

|Detail|Explanation|

|---------|---------------|

|start|Time the alert started|

|suser|Account (usually the user account) involved in the alert|

|shost|Account (usually the machine account) involved in the alert|

|outcome|When relevant, success or failure of the suspicious activity in the alert|

|msg|Description of the alert|

|cnt|For alerts that have a count of the number of times the activity happened (for example, brute force has an amount of guessed passwords)|

|app |Protocol used in this alert|

|externalId|Event ID Defender for Identity writes to the event log that corresponds to each type of alert.|

|cs#label|Customer strings allowed by CEF, where cs#label is the name of the new field |

|cs#|Customer strings allowed by CEF, where cs# is the value.|

- For example: `cs1Label=url cs1=https\://security.microsoft.com/alerts/aa5909ae198ca1ec04d05e65fa`

The cs1 field is the alert URL.

- For example: `cs2Label=trigger cs2=new`

The cs2 field identifies if the alert is new or updated.

- For example: `cs3Label=shostfqdn cs3=client1.contoso.com`

The cs3 field identifies the fully qualified domain name of the source computer name.

> [!NOTE]

> If you plan to create automation or scripts for Defender for Identity SIEM logs, we recommend using the **externalId** field to identify the alert type instead of using the alert name for this purpose. Alert names may occasionally be modified, while the **externalId** of each alert is permanent. For a list of external IDs, see [Security alerts](alerts-overview.md).

## Sample logs

The log examples comply with RFC 5424, but Defender for Identity also supports RFC 3164.

>[!NOTE]

>The list below is a sample of logs sent to a SIEM. For a full list of alert details, see [Security alerts](alerts-overview.md).

Priorities:

- 3=Low

- 5=Medium

- 10=High

### Account enumeration reconnaissance

`02-21-2018 16:19:35 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:27.540731+00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|AccountEnumerationSecurityAlert|Reconnaissance using account enumeration|5|start=2018-02-21T14:19:02.6045416Z app=Kerberos shost=CLIENT1 suser=LMaldonado msg=Suspicious account enumeration activity using the Kerberos protocol, originating from CLIENT1, was observed and successfully guessed Lamon Maldonado (Software Engineer). externalId=2003 cs1Label=url cs1=https\://security.microsoft.com/alerts/aaeb6a35da-ff7f-4ab5-a1b5-a07529a89e6d cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Data exfiltration over SMB

`12-19-2018 14:17:46 Auth.Error 127.0.0.1 1 2018-12-19T12:17:34.645993+00:00 DC1 CEF 3288 SmbDataExfiltrationSecurityAlert |Microsoft|Azure ATP|2.60.0.0|SmbDataExfiltrationSecurityAlert|[PREVIEW] Data exfiltration over SMB|10|start=2018-12-19T12:14:12.4932821Z app=Smb shost=CLIENT1 msg=Eugene Jenkins (Software Engineer) on DC2 copied suspicious files to CLIENT1. externalId=2030 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa3ca2ec9d-2c67-44cc-a2d6-391716611bb6 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Honeytoken activity

`02-21-2018 16:20:36 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:34.106162+00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|HoneytokenActivitySecurityAlert|Honeytoken activity|5|start=2018-02-21T14:20:26.6705617Z app=Kerberos suser=honey msg=The following activities were performed by honey:\r\nLogged in to CLIENT2 via DC1. externalId=2014 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa9249fe9a-c883-46dd-a4da-2a1fca5f211c cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Malicious request of Data Protection API master key

`10-29-2018 11:22:04 Auth.Error 192.168.0.202 1 2018-10-29T09:22:00.350864+00:00 DC3 CEF 3908 RetrieveDataProtectionBackupKeyS |Microsoft|Azure ATP|2.52.5704.46184|RetrieveDataProtectionBackupKeySecurityAlert|Malicious Data Protection Private Information Request|10|start=2018-10-29T09:19:45.6307993Z app=LsaRpc shost=CLIENT1 msg=user1 performed 1 successful attempts from CLIENT1 to retrieve DPAPI domain backup key from DC1. externalId=2020 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa2f5717cb-2434-4d54-8af4-b2c6d14bc15c cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Network-mapping reconnaissance (DNS)

`10-29-2018 11:20:02 Auth.Warning 192.168.0.202 1 2018-10-29T09:19:59.056894+00:00 DC3 CEF 3908 DnsReconnaissanceSecurityAlert |Microsoft|Azure ATP|2.52.5704.46184|DnsReconnaissanceSecurityAlert|Reconnaissance using DNS|5|start=2018-10-29T09:19:43.5033765Z app=Dns shost=CLIENT1 msg=Suspicious DNS activity was observed, originating from CLIENT1 (which is not a DNS server) against DC1. externalId=2007 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa23937d33-ff71-484d-be0a-3c417fe573ce cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Reconnaissance using directory services queries

`02-21-2018 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|SamrReconnaissanceSecurityAlert| Reconnaissance using directory services enumeration |5|start=2018-02-21T14:19:41.9912772Z app= Samr shost=CLIENT1 suser=user1 outcome=Success msg= The following directory services enumerations using SAMR protocol were attempted against DC1 from CLIENT1:\r\nSuccessful enumeration of all groups in domain1.test.local by user1. externalId=2019 cs1Label=url cs1=https\://security.microsoft.com/alerts/aaf295029a-ffae-408b-9dd0-55424c81eac0 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Remote code execution attempt

`10-29-2018 11:22:04 Auth.Warning 192.168.0.202 1 2018-10-29T09:22:00.100856+00:00 DC3 CEF 3908 RemoteExecutionSecurityAlert |Microsoft|Azure ATP|2.52.5704.46184|RemoteExecutionSecurityAlert|Remote code execution attempt|5|start=2018-10-29T09:19:45.0552367Z shost=CLIENT1 msg=The following remote code execution attempts were performed on DC1 from CLIENT1:\r\nSuccessful remote scheduling of one or more tasks by user1.\r\nFailed remote scheduling of one or more tasks by user1.\r\nSuccessful remote execution of one or more WMI methods by user1. externalId=2019 cs1Label=url cs1=https\://security.microsoft.com/alerts/aaf063c778-830c-4e9f-98d1-bc6c11c94e11 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Remote code execution attempt over DNS

`1-17-2019 08:24:54 Auth.Warning 192.168.0.202 1 2019-01-17T08:24:54.100856+00:00 DC3 CEF 3908 DnsRemoteCodeExecutionSecurityAlert |Microsoft|Azure ATP|2.63.0.0|DnsRemoteCodeExecutionSecurityAlert|[PREVIEW] Remote code execution over DNS|5|start=2019-01-17T08:24:54.5293800Z app=Dns shost=CLIENT1 msg=An actor attempted to run commands remotely on CLIENT1 from DC1, over DNS protocol. externalId=2036 cs1Label=url cs1=https\:////security.microsoft.com/alerts/aa591f9769-d904-40b1-89fa-c307c2ca814f cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Security principal reconnaissance (LDAP)

`02-18-2019 16:48:08 Auth.Warning 127.0.0.1 1 2019-02-18T14:48:02.912264+00:00 DC1 CEF 4656 LdapSearchReconnaissanceSecurity |Microsoft|Azure ATP|2.66.0.0|LdapSearchReconnaissanceSecurityAlert|[PREVIEW] Reconnaissance using LDAP Queries|5|start=2019-02-18T14:46:29.4644276Z app=LdapSearch shost=CLIENT1 msg=An actor on CLIENT1 sent suspicious LDAP queries to DC1, searching for 4 types of enumeration and Server Operators (Members can administer domain servers) in 2 domains externalId=2038 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa81ea99c4-ce1f-4581-ac8f-7440fbed7cd0 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected brute force attack (LDAP)

`02-21-2018 16:20:21 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:06.156238+00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|LdapBruteForceSecurityAlert|Brute force attack using LDAP simple bind|5|start=2018-02-21T14:19:41.7422810Z app=Ldap suser=Wofford Thurston shost=CLIENT1 msg=A brute force attack using the Ldap protocol was attempted on Wofford Thurston (Software Engineer) from CLIENT1 (100 guess attempts). cnt=100 externalId=2004 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa57b8ac96-7907-4971-9b27-ec77ad8c029a cs2Label=trigger cs2=update cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected brute force attack (Kerberos, NTLM)

`10-29-2018 11:20:47 Auth.Warning 192.168.0.202 1 2018-10-29T09:20:44.478827+00:00 DC3 CEF 3908 BruteForceSecurityAlert |Microsoft|Azure ATP|2.52.5704.46184|BruteForceSecurityAlert|Suspicious authentication failures|5|start=2018-10-29T09:19:44.9512286Z app=Kerberos shost=CLIENT1 msg=Suspicious authentication failures indicating a potential brute-force attack were detected from CLIENT1. externalId=2023 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa85042c8e-27fa-49b3-8667-dabc1aa31580 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected DCSync attack (replication of directory services)

`02-21-2018 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.254930+00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity |Microsoft|Azure ATP|2.22.4228.22540|MaliciousServiceCreationSecurityAlert|Suspicious service creation|5|start=2018-02-21T14:19:41.7897808Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 created MaliciousService in order to execute potentially malicious commands on CLIENT1. externalId=2026 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa179229b6-b791-4895-b5aa-fdf3747a325c cs2Label=trigger cs2=update cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected Golden Ticket usage (encryption downgrade)

`10-29-2018 11:25:07 Auth.Warning 192.168.0.202 1 2018-10-29T09:25:01.007701+00:00 DC3 CEF 3908 GoldenTicketEncryptionDowngradeS |Microsoft|Azure ATP|2.52.5704.46184|GoldenTicketEncryptionDowngradeSecurityAlert|Encryption downgrade activity (potential golden ticket attack)|5|start=2018-10-29T09:37:49.0849130Z app=Kerberos msg=W10-000007-Lap used a weaker encryption method (RC4), in the Kerberos service request (TGS_REQ), from W10-000007-Lap, to access host/domain1.test.local. externalId=2009 cs1Label=url cs1=https\://security.microsoft.com/alerts/aaf01f8403-88b2-437e-b4ad-d72485fe05ac cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected Golden Ticket usage (non-existent account)

`07-01-2018 14:28:49 Auth.Error 192.168.0.100 1 2018-07-01T11:28:35.546638+00:00 CENTER CEF 38768 ForgedPrincipalSecurityAlert |Microsoft|Azure ATP|2.39.0.0|ForgedPrincipalSecurityAlert|Kerberos Golden Ticket - non-existing account|10|start=2018-07-01T09:48:31.2567987Z app=Kerberos suser=domain1.test.local\fake msg=domain1.test.local\fake, which does not exist in Active Directory, used a Kerberos ticket. The ticket was detected from 2 computers to access 3 resources. This may indicate a potential Golden Ticket attack. externalId=2027 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa98f050d4-9134-429c-8e54-d8eeb19849c4 cs2Label=trigger cs2=update cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected Golden Ticket usage (ticket anomaly)

`2018-11-18T10:46:23.346946+00:00 MAXIMG-7050 CEF 24284 GoldenTicketSizeAnomalySecurityA 0|Microsoft|Azure ATP|2.56.0.0|GoldenTicketSizeAnomalySecurityAlert|[PREVIEW] Suspected Golden Ticket usage (ticket anomaly)|10|start=2018-11-18T10:44:12.9317797Z app=Kerberos shost=CLIENT2 suser=RFosdyke msg=Renzo Fosdyke (Software Engineer) used a suspicious Kerberos ticket from CLIENT2 to access ldap/domain1.test.local. externalId=2032 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa63600e03-f423-49bf-a92d-4010e1d52b9f cs2Label=trigger cs2=update cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected Golden Ticket usage (time anomaly)

`02-21-2018 16:22:39 Auth.Error 192.168.0.220 1 2018-02-21T14:22:34.274054+00:00 CENTER CEF 6076 GoldenTicketSecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|GoldenTicketSecurityAlert|Kerberos Golden Ticket activity|10|start=2018-02-21T14:19:03.2416152Z app=Kerberos suser=Lanell Campos msg=Suspicious usage of Lanell Campos (Software Engineer)'s Kerberos ticket, indicating a potential Golden Ticket attack, was detected. externalId=2022 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa702c836e-6f49-4479-9892-80e8bccbfac0 cs2Label=trigger cs2=update cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected Golden Ticket usage (forged authorization data)

`10-29-2018 11:22:04 Auth.Error 192.168.0.202 1 2018-10-29T09:21:59.288337+00:00 DC3 CEF 3908 ForgedPacSecurityAlert |Microsoft|Azure ATP|2.52.5704.46184|ForgedPacSecurityAlert|Privilege escalation using forged authorization data|10|start=2018-10-29T09:19:43.6403358Z app=Kerberos suser=user1 msg=user1 failed to escalate privileges against DC1 to host/domain1.test.local from CLIENT1 by using forged authorization data. externalId=2013 cs1Label=url cs1=https\://security.microsoft.com/alerts/aab698d438-5013-4bca-be0b-f219f8b69108 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected identity theft (Pass-the-Hash)

`02-21-2018 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheHashSecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|PassTheHashSecurityAlert|Identity theft using Pass-the-Hash attack|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (Software Engineer)'s hash was stolen from one of the computers previously logged into by Eugene Jenkins (Software Engineer) and used from CLIENT1. externalId=2017 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=update cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected identity theft (Pass-the-Ticket)

`02-21-2018 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheTicketSecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|PassTheTicketSecurityAlert|Identity theft using Pass-the-Ticket attack|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (Software Engineer)'s Kerberos tickets were stolen from Admin-PC to Victim-PC and used to access krbtgt/DOMAIN1.TEST.LOCAL. externalId=2018 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected NTLM authentication tampering

`07-17-2019 18:18:44 Auth.Warning 192.168.0.77 1 2019-07-09T15:18:30.967118+00:00 CENTER CEF 7144 AbnormalNtlmSigningSecurityAlert |Microsoft|Azure ATP|2.86.0.0|AbnormalNtlmSigningSecurityAlert|[PREVIEW] Suspected NTLM authentication tampering|5|start=2019-07-09T15:14:57.5280720Z app=Ntlm shost=CLIENT1 msg=2 accounts on CLIENT1 is suspiciously trying to authenticate against 2 computers over NTLM. externalId=2039 cs1Label=url cs1=https\://security.microsoft.com/alerts/aad4ce6252-2c0f-47f6-a534-47ee8ad983be cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected Over-Pass-the-Hash attack (encryption downgrade)

`02-21-2018 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Encryption downgrade activity|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg= The encryption method of the Encrypted_Timestamp field of AS_REQ message from CLIENT1 has been downgraded based on previously learned behavior. This may be a result of a credential theft using Overpass-the-Hash from CLIENT1. externalId=2008 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=update cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected Skeleton Key attack (encryption downgrade)

`02-21-2018 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Encryption downgrade activity|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg=The encryption method of the ETYPE_INFO2 field of KRB_ERR message from CLIENT1 has been downgraded based on previously learned behavior. This may be a result of a Skeleton Key on DC1. externalId=2010 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspicious authentication failures

`02-21-2018 16:19:20 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:15.397995+00:00 CENTER CEF 6076 BruteForceSecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|BruteForceSecurityAlert|Suspicious authentication failures|5|start=2018-02-21T14:19:03.3831122Z app=Kerberos shost=CLIENT1 msg=Suspicious authentication failures indicating a potential brute-force attack were detected from CLIENT1. externalId=2023 cs1Label=url cs1=https\://security.microsoft.com/alerts/aafea88fc7-4110-454d-816d-349032474fd6 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspicious communication over DNS

`10-04-2018 14:49:38 Auth.Warning 192.168.0.202 1 2018-10-04T11:49:25.954059+00:00 DC3 CEF 3604 DnsSuspiciousCommunicationSecuri |Microsoft|Azure ATP|2.49.5589.58606|DnsSuspiciousCommunicationSecurityAlert|Suspicious Communication over DNS|5|start=2018-10-04T11:49:11.0822077Z app=DnsEvent dhost= suspiciousdomainname msg=CLIENT1 sent suspicious DNS queries resolving suspiciousdomainname externalId=2031 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa0fc77777-49ca-40b3-a7ba-7644f355539e cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspicious domain controller promotion (potential DcShadow attack)

`07-12-2018 11:18:07 Auth.Error 192.168.0.200 1 2018-07-12T08:18:06.883880+00:00 DC1 CEF 3868 DirectoryServicesRoguePromotionS |Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRoguePromotionSecurityAlert| **Suspicious domain controller promotion (potential DcShadow attack)**|10|start=2018-07-12T08:17:55.4067092Z app=Ldap shost=CLIENT1 msg=CLIENT1, which is a computer in domain1.test.local, registered as a domain controller on DC1. externalId=2028 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa97c59b43-dc18-44ee-9826-8fd5d03bd53 cs2Label=trigger cs2=update cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspicious additions to sensitive groups

`10-29-2018 11:21:03 Auth.Warning 192.168.0.202 1 2018-10-29T09:20:49.667014+00:00 DC3 CEF 3908 AbnormalSensitiveGroupMembership |Microsoft|Azure ATP|2.52.5704.46184|AbnormalSensitiveGroupMembershipChangeSecurityAlert|Suspicious modification of sensitive groups|5|start=2018-10-29T09:19:43.3013729Z app=GroupMembershipChangeEvent suser=user1 msg=user1 has uncharacteristically modified sensitive group memberships. externalId=2024 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa6f7e677e-f068-41e5-bada-708cd5a322b9 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspicious replication of directory services

`02-21-2018 16:21:22 Auth.Error 192.168.0.220 1 2018-02-21T14:21:13.978554+00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu |Microsoft|Azure ATP|2.22.4228.22540|DirectoryServicesReplicationSecurityAlert|Malicious replication of directory services|10|start=2018-02-21T14:19:03.9975656Z app=Drsr shost=CLIENT1 msg=Malicious replication requests were successfully performed by user1, from CLIENT1 against DC1. outcome=Success externalId=2006 cs1Label=url cs1=https\://security.microsoft.com/alerts/aacb95648e-1b6f-4d3b-81b9-7605532787d7 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspicious replication request (potential DcShadow attack)

`07-12-2018 11:18:37 Auth.Error 192.168.0.200 1 2018-07-12T08:18:32.265989+00:00 DC1 CEF 3868 DirectoryServicesRogueReplicatio |Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRogueReplicationSecurityAlert| **Suspicious replication request (potential DcShadow attack)**|10|start=2018-07-12T08:17:55.3816102Z **app=Replication Activity** shost=CLIENT1 msg=CLIENT1, which is not a valid domain controller in domain1.test.local, sent changes to directory objects on DC1. externalId=2029 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa1d5d1444-12cf-4db9-be48-39ebc2f51515 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspicious service creation

`10-29-2018 11:20:02 Auth.Warning 192.168.0.202 1 2018-10-29T09:19:59.164874+00:00 DC3 CEF 3908 MaliciousServiceCreationSecurity |Microsoft|Azure ATP|2.52.5704.46184|MaliciousServiceCreationSecurityAlert|Suspicious service creation|5|start=2018-10-29T09:19:44.9471965Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 created MaliciousService in order to execute potentially malicious commands on CLIENT1. externalId=2026 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa118bbe3d-fe72-40de-80d0-2678b68aa027 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspicious VPN Connection

`07-03-2018 13:13:12 Auth.Warning 192.168.0.200 1 2018-07-03T10:13:06.187834+00:00 DC1 CEF 2520 AbnormalVpnSecurityAlert |Microsoft|Azure ATP|2.39.0.0|AbnormalVpnSecurityAlert|Suspicious VPN Connection|5|start=2018-06-30T15:34:05.3887333Z app=VpnConnection suser=user1 msg=user1 connected to a VPN using 3 computers from 3 Locations. externalId=2025 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa88c46b0e-372f-4c06-9935-67bd512c4f68 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected WannaCry ransomware attack

`02-21-2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedWannaCryRansomwareAttack|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=There were attempts to authenticate from CLIENT2 against DC1 using an unusual protocol implementation. May be a result of malicious tools used to execute attacks such as WannaCry. externalId=2035 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected brute force attack (SMB)

`002-21-2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedBrutForceAttack|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=There were attempts to authenticate from CLIENT2 against DC1 using an unusual protocol implementation. May be a result of malicious tools used to execute attacks such as Hydra. externalId=2033 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected use of Metasploit hacking framework

`002-21-2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedAttackUsingMetasploit|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=There were attempts to authenticate from CLIENT2 against DC1 using an unusual protocol implementation. May be a result of malicious tools used to execute attacks such as Metasploit. externalId=2034 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### Suspected overpass-the-hash attack (Kerberos)

`002-21-2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedOverPassTheHashAttack|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=There were attempts to authenticate from CLIENT2 against DC1 using an unusual protocol implementation. May be a result of malicious acts using the Kerberos protocol. externalId=2002 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

### User and IP address reconnaissance (SMB)

`002-21-2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert |Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|ReconnaissanceusingSMBSessionEnumeration|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=There were attempts to authenticate from CLIENT2 against DC1 using an unusual protocol implementation. May be a result of malicious tools used to execute attacks such as Metasploit. externalId=2034 cs1Label=url cs1=https\://security.microsoft.com/alerts/aa40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new cs3Label=shostfqdn cs3=client1.contoso.com`

## See Also

- [Security alerts](alerts-overview.md).

- [Configure event collection](deploy/configure-event-collection.md)

- [Configuring Windows event forwarding](deploy/configure-event-forwarding.md)

- [Check out the Defender for Identity forum](https://aka.ms/MDIcommunity)


# Privacy Compliance

# Privacy with Microsoft Defender for Identity

This article describes how Microsoft Defender for Identity collects data in a manner that protects personal privacy.

[!INCLUDE [gdpr-hybrid-note](../includes/gdpr-hybrid-note.md)]

## What data is collected?

Microsoft Defender for Identity monitors information generated from your organization's Active Directory, network activities, and event activities to detect suspicious activity. The monitored activity information enables Defender for Identity to help you determine the validity of each potential threat and correctly triage and respond.

For more information, see: [Microsoft Defender for Identity monitored activities](monitored-activities.md).

## Data location

Defender for Identity operates in the Microsoft Azure data centers in the following locations:

- Asia (Southeast Asia)

- Australia (Australia East, Australia Southeast)

- Europe (West Europe, North Europe)

- India (Central India, South India)

- North America (East US, West US, West US2)

- Switzerland (Switzerland North, Switzerland West)

- United Arab Emirates (UAE North and UAE Central)

- United Kingdom (UK South)

Customer data collected by the service might be stored as follows:

- Your workspace is automatically created in the data center that's geographically closest to your Microsoft Entra ID. Once created, Defender for Identity workspaces can't be moved to another data center. Your workspace's data center is listed in the Microsoft Defender portal, under **Settings** > **Identity** > **About** > **Geolocation**.

- A geographic location as defined by the data storage rules of an online service, if the online service is used by Defender for Identity to process such data.

## Data retention

Microsoft Defender for Identity retains data for 180 days, which is visible across the portal.

Your data is kept and is available to you while the license is under grace period or suspended mode. At the end of this period, that data will be erased from Microsoft's systems to make it unrecoverable, no later than 180 days from contract termination or expiration.

## Data sharing

Defender for Identity shares data, including customer data, among any of the following Microsoft products that are also licensed by the customer. For customers in the Government Community Cloud (GCC), data sharing between government and commercial cloud environments may occur, depending on the location of the service offering.

- Microsoft Defender XDR

- Microsoft Defender for Cloud Apps

- Microsoft Defender for Endpoint

- Microsoft Defender for Cloud

- Microsoft Sentinel

- Microsoft Security Exposure Management (public preview)

## Related content

For more information, see:

- The [Microsoft Service Trust portal](https://www.microsoft.com/en-us/trust-center/product-overview)

- [Licensing and privacy FAQ](technical-faq.yml#licensing-and-privacy)


# Whats New Archive

# What's new archive for Microsoft Defender for Identity

This article lists Microsoft Defender for Identity release notes for versions and features released over 6 months ago.

For information about the latest versions and features, see [What's new in Microsoft Defender for Identity](whats-new.md).

> [!NOTE]

> Starting June 15 2022, Microsoft will no longer support the Defender for Identity sensor on devices running Windows Server 2008 R2. We recommend that you identify any remaining Domain Controllers (DCs) or AD FS servers that are still running Windows Server 2008 R2 as an operating system and make plans to update them to a supported operating system.

>

>For the two months after June 15 2022, the sensor will continue to function. After this two-month period, starting August 15, 2022, the sensor will no longer function on Windows Server 2008 R2 platforms. More details can be found at: <https://aka.ms/mdi/2008r2>

## October 2025

We're excited to announce that the Microsoft Defender for Identity sensor v3.x is now generally available (GA).

The [Microsoft Defender for Identity sensor v3.x](/defender-for-identity/deploy/activate-sensor) provides enhanced coverage, improved performance across your environment and offering easier deployment and management for domain controllers.

### Microsoft Defender for Identity sensor version updates

|Version number|Updates|

|---|---|

|2.249|The improved event log query method now captures a broader range of unique events at scale. As a result, you might notice an increase in captured activities. This update also delivers other security enhancements and performance improvements.|

## September 2025

### Defender for Identity alerts transitioned to the unified Defender alerting experience

As part of the ongoing transition to a unified alerting experience across Microsoft Defender products, the following alerts were converted from the Microsoft Defender for Identity classic format to the unified Defender alerting format. Keep in mind that all alerts are based on detections from Defender for Identity sensors.

|Classic Alert Title|External ID|XDR Alert Name|Detector ID|

|---|---|---|---|

|Active Directory attributes Reconnaissance using LDAP|2210|[LDAP reconnaissance attributes in Active Directory](alerts-xdr.md)|xdr_LdapSensitiveAttributeReconnaissance|

|User and IP address reconnaissance|2012|[Suspicious Server Message Block (SMB) enumeration from untrusted host](alerts-xdr.md#suspicious-server-message-block-smb-enumeration-from-untrusted-host)|xdr_SmbSessionEnumeration|

|Account enumeration reconnaissance|2003|[Suspected account enumeration (Kerberos, NTLM, AD FS)](alerts-xdr.md#suspected-account-enumeration-kerberos-ntlm-ad-fs)|xdr_SuspectedAccountEnumeration|

|Suspected brute-force attack (LDAP)|2004|[Suspected brute-force attack on Lightweight Directory Access Protocol (LDAP) authentication](alerts-xdr.md#suspected-brute-force-attack-on-lightweight-directory-access-protocol-ldap-authentication)|xdr_LdapBindBruteforce|

|||[Suspected password spray attack on Lightweight Directory Access Protocol (LDAP) authentication](alerts-xdr.md#suspected-password-spray-attack-on-lightweight-directory-access-protocol-ldap-authentication)|xdr_LdapBindBruteforce|

|Suspicious network connection over Encrypting File System Remote Protocol|2416|[Suspicious network connection over Encrypting File System Remote Protocol](alerts-xdr.md#suspicious-network-connection-over-encrypting-file-system-remote-protocol)|xdr_SuspiciousConnectionOverEFSRPC|

### Additional security value in the Defender for Identity sensor v3.x

Apply the **Unified sensor RPC audit*- tag to your Defender for Identity sensor v3.x in the **Asset rule management*- page for enhanced protection. Learn more [here](/defender-for-identity/deploy/deploy-sensor-v3).

### Identity posture recommendations view on the identity page (preview)

A new tab on the Identity profile page contains all active identity-related identity security posture assessments (ISPMs). This page consolidates all identity-specific security posture assessments into a single contextual view, helping security teams quickly spot weaknesses and take targeted actions.

For more information, see [Investigate users in Microsoft Defender XDR](/microsoft-365/security/defender/investigate-users).

### New Regional Availability: United Arab Emirates

Defender for Identity data centers are now also deployed in the United Arab Emirates, North, and Central regions. For the most current list of regional deployments, see [Defender for Identity data locations](/defender-for-identity/privacy-compliance/#data-location).

### New API support for the Defender for Identity sensor v3.x (Preview)

We're excited to announce the availability of a new Graph-based API for managing the Defender for Identity sensor v3.x server actions.

This capability is currently in preview and available in API Beta version.

This API allows customers to:

- Monitor the status of servers deployed with the Defender for Identity sensor v3.x.

- Enable or disable the automatic activation of eligible servers.

- Activate or deactivate the sensor on eligible server.

For more information, see [Managing the Defender for Identity sensor v3.x actions using Graph API](/graph/api/resources/security-api-overview?view=graph-rest-beta&preserve-view=true).

### Microsoft Defender for Identity sensor version updates

|Version number|Updates|

|---|---|

|2.249|Includes bug fixes and stability improvements for the Microsoft Defender for Identity sensor.|

### Updates to multiple detections to reduce noise and improve alert accuracy

Several Defender for Identity detections are being updated to reduce noise and improve accuracy, making alerts more reliable and actionable. As the rollout continues, you might see a decrease in the number of alerts raised.

The improvements will gradually take effect across the following detections:

- Suspicious communication over DNS

- Suspected Netlogon privilege elevation attempt (CVE-2020-1472)

- Honeytoken authentication activity

- Remote code execution attempt over DNS

- Suspicious password reset by Microsoft Entra Connect account

- Data exfiltration over SMB

- Suspected skeleton key attack (encryption downgrade)

- Suspicious modification of Resource Based Constrained Delegation by a machine account

- Remote code execution attempt

### Unified connectors is now available for Okta single sign-on connectors (Preview)

Microsoft Defender for Identity supports the [Unified connectors](/azure/sentinel/unified-connector) experience, starting with the Okta single sign-on connector. The unified connector enables Defender for Identity to collect Okta system logs once and share them across supported Microsoft security products, reducing API usage and improving connector efficiency.

For more information, see: [Connect Okta to Microsoft Defender for Identity (Preview)](okta-integration.md)

## August 2025

### Microsoft Entra ID risk level is now available in near real time in Microsoft Defender for Identity (Preview)

Microsoft Entra ID risk level is now available on the Identity Inventory assets page, the identity details page, and in the IdentityInfo table in Advanced Hunting, and includes the Microsoft Entra ID risk score. SOC analysts can use this data to correlate risky users with sensitive or highly privileged users, create custom detections based on current or historical user risk, and improve investigation context.

Previously, Defender for Identity tenants received Microsoft Entra ID risk level in the IdentityInfo table through user and entity behavior analytics (UEBA). With this update, the Microsoft Entra ID risk level is now updated in near real time through Microsoft Defender for Identity.

For UEBA tenants without a Microsoft Defender for Identity license, synchronization of Microsoft Entra ID risk level to the IdentityInfo table remains unchanged.

### New security assessment: Remove inactive service accounts

Microsoft Defender for Identity now includes a new security assessment that helps you identify and remove inactive service accounts in your organization. This assessment lists Active Directory service accounts that were inactive for the past 90 days, to help you mitigate security risks associated with unused accounts.

For more information, see: Security Assessment: [Remove Inactive Service Accounts (Preview)](/defender-for-identity/remove-inactive-service-account).

### New Graph based API for response actions (preview)

We're excited to announce a new Graph-based API for initiating and managing remediation actions in Microsoft Defender for Identity.

This capability is currently in preview and available in API Beta version.

For more information, see [Managing response actions through Graph API](/graph/api/resources/security-identityaccounts?view=graph-rest-beta&preserve-view=true).

### Identity scoping is now generally available (GA)

Identity scoping is now generally available across all environments. Organizations can now define and refine the scope of MDI monitoring and gain granular control over which entities and resources are included in security analysis.

For more information, see [Configure scoped access for Microsoft Defender for Identity](configure-scoped-access.md).

### New security posture assessment: Remove discoverable passwords in Active Directory account attributes (Preview)

The new security posture assessment highlights unsecured Active Directory attributes that contain passwords or credential clues and recommends steps to remove them, helping reduce the risk of identity compromise.

For more information, see: [Security Assessment: Remove discoverable passwords in Active Directory account attributes (Preview)](/defender-for-identity/security-posture-assessments/accounts#remove-discoverable-passwords-in-active-directory-account-attributes-preview)

### Microsoft Defender for Identity sensor version updates

|Version number|Updates|

|---|---|

|2.247|Includes bug fixes and stability improvements for the Microsoft Defender for Identity sensor.|

|2.246|Includes bug fixes and stability improvements for the Microsoft Defender for Identity sensor.|

### Detection update: Suspected Brute Force attack (Kerberos, NTLM)

Improved detection logic to include scenarios where accounts were locked during attacks. As a result, the number of triggered alerts might increase.

## July 2025

### Expanded coverage in ITDR deployment health widget

The Identity Threat Detection and Response (ITDR) deployment health widget now provides visibility into the deployment status of additional server types. Previously, it only reflected the status for Active Directory domain controllers. With this update, the widget also includes deployment status for ADFS, ADCS, and Microsoft Entra Connect servers - making it easier to track and ensure full sensor coverage across all supported identity infrastructure.

### Time limit added to Recommended test mode

Recommended test mode configuration on the [Adjust alert thresholds page](/defender-for-identity/advanced-settings), now requires you to set an expiration time (up to 60 days) when enabling it. The end time is shown next to the toggle while test mode is active. For customers who have already enabled Recommended test mode, a 60-day expiration is automatically applied.

### Identity scoping is now available in Governance environments

Scoping is now supported in government (GOV) environments. Organizations can now define and refine the scope of MDI monitoring and gain granular control over which entities and resources are included in security analysis.

For more information, see [Configure scoped access for Microsoft Defender for Identity](configure-scoped-access.md).

### New security posture assessments for unmonitored identity servers

Microsoft Defender for Identity three new security posture assessments detect when Microsoft Entra Connect, Active Directory Federation Services (ADFS), or Active Directory Certificate Services (ADCS) servers are present in your environment but aren't monitored.

Use these assessments to improve monitoring coverage and strengthen your hybrid identity security posture.

For more information, see:

- [Security Assessment: Unmonitored ADCS servers](/defender-for-identity/security-posture-assessments/identity-infrastructure#unmonitored-adcs-servers)

- [Security Assessment: Unmonitored ADFS servers](/defender-for-identity/security-posture-assessments/identity-infrastructure#unmonitored-adfs-servers)

- [Security Assessment: Unmonitored Microsoft Entra Connect servers](/defender-for-identity/security-posture-assessments/identity-infrastructure#unmonitored-microsoft-entra-connect-servers)

## June 2025

### Scoped access by Active Directory domain now supported (Preview)

MDI scoping is now available as part of XDR User Role-Based Access Control (URBAC). Organizations can now define and refine the scope of MDI monitoring, providing granular control over which entities and resources are included in security analysis.

Scoping by Active Directory domains helps:

- Optimize performance: Focus monitoring on critical assets and reduce noise from nonessential data.

- Enhance visibility control: Tailor MDI coverage to specific domains and user groups.

- Support operational boundaries: Align access for SOC analysts, identity administrators, and regional teams.

For more information, see: [Configure scoped access for Microsoft Defender for Identity](configure-scoped-access.md).

### Okta integration is now available in Microsoft Defender for Identity

Microsoft Defender for Identity now supports integration with Okta, enabling detection of identity-based threats across cloud and on-premises environments. This integration helps identify suspicious sign-ins, risky role assignments, and potential privilege misuse within your Okta environment.

For prerequisites and configuration steps, see [Integrate Okta with Microsoft Defender for Identity](okta-integration.md).

### Service account classification rules now available

You can now create custom classification rules to identify service accounts based on your organization's specific criteria. This complements automatic discovery, enabling more accurate identification of service accounts.

For more information, see [Service account discovery](service-account-discovery.md).

### Defender For Identity PowerShell module updates (version 1.0.0.4)

New Features and Improvements:

- Added remote domain functionality.

- Added SensorType parameter to Test-MDISensorApiConnection to inform endpoint URL.

- Added ability to Get/Set/Test the Deleted Objects container permissions.

- Added auditing for Delegated Managed Service Accounts (dMSA) in the DomainObjectAuditing configuration.

Bug Fixes:

- Fixed audit verification checks for non-English operating systems.

- Fixed DomainObjectAuditing identity redundant parameter bug.

- Fixed Domain Controller detection logic to confirm AD Web Services is running on the server.

- Fixed issue with Test-MDIDSA not parsing Deleted Object permissions.

- Other reliability fixes.

## May 2025

### Improved Visibility into Defender for Identity New Sensor Eligibility in the Activation page

The Activation Page now displays all servers from your device inventory, including those not currently eligible for the new Defender for Identity sensor. This enhancement increases transparency into sensor eligibility, helping you identify noneligible servers and take action to update and onboard them for enhanced identity protection.

### Local administrators collection (using SAM-R queries) feature is disabled

The remote collection of local administrators group members from endpoints using SAM-R queries in Microsoft Defender for Identity will be disabled by mid-May 2025. This data is currently used to build potential lateral movement path maps, which will no longer be updated after this change. An alternative method is being explored. The change occurs automatically by the specified date, and no administrative action is required.

### New Health Issue

New [health issue](health-alerts.md) for cases where sensors running on VMware have network configuration mismatch.

## April 2025

### Privileged Identity Tag Now Visible in Defender for Identity Inventory

Identities listed in the [Identity inventory](identity-inventory.md) in Microsoft Defender portal now include a **Privileged account** tag for accounts managed by a **Privileged Identity Management (PIM)** service.

Privileged accounts are prime targets for attackers. Tagging them in the inventory helps you quickly identify high-risk or high-value accounts, prioritize investigation and mitigation efforts, and streamline incident response workflows.

Learn more about [Privileged Identity Management.](/entra/id-governance/privileged-identity-management/pim-configure)

### New Defender for Identity and PAM Integration

Microsoft Defender for Identity now supports integration with industry-leading Privileged Access Management (PAM) platforms to enhance detection and response for privileged identities.

**Supported PAM vendors**:

- CyberArk

- Delinea

- BeyondTrust

For more information, see: [Integrations Defender for Identity and PAM services.](Integrate-microsoft-and-pam-services.md)

## March 2025

### New Service Account Discovery page

Microsoft Defender for Identity now includes a Service Account Discovery capability, offering you  centralized visibility into service accounts across your Active Directory environment.

This update provides:

- Automatic identification of Group Managed Service Accounts, Managed Service Accounts, and user accounts operating as service accounts.

- A centralized Service Accounts inventory, displaying key attributes like account type, authentication type, unique connections, last sign in, service class and criticality.

- A Service Account details page, including an overview, a timeline of activities, alerts, and a new connections tab.

For more information, see: [Investigate and protect Service Accounts | Microsoft Defender for Identity](service-account-discovery.md).

### Enhanced Identity Inventory

The Identities page under *Assets* was updated to provide better visibility and management of identities across your environment.

The updated Identities Inventory page now includes the following tabs:

- Identities: A consolidated view of identities across Active Directory, Microsoft Entra ID. This Identities tab highlights key details, including identity types, and user's information.

- Cloud application accounts: Displays a list of cloud application accounts, including those from application connectors and non-Microsoft sources (original available in the previous version based on Microsoft Defender for Cloud Apps).

For more information, see [Identity inventory details](/defender-for-identity/identity-inventory).

### New LDAP query events added to the IdentityQueryEvents table in Advanced Hunting

New LDAP query events were added to the `IdentityQueryEvents` table in Advanced Hunting to provide more visibility into additional LDAP search queries running in the customer environment.

## February 2025

### DefenderForIdentity PowerShell module updates (version 1.0.0.3)

New Features and Improvements:

- Support for getting, testing, and setting the Active Directory Recycle Bin in Get/Set/Test MDI Configuration.

- Support for getting, testing, and setting the proxy configuration on new MDI sensor.

- The Active Directory Certificate Services registry value for audit filtering now properly sets the type.

- New-MDIConfigurationReport now shows the name of the tested GPO and supports Server and Identity arguments.

Bug Fixes:

- Improved reliability for DeletedObjects container permissions on non-English operating systems.

- Fixed extraneous output for KDS root key creation.

- Other reliability fixes.

### New attack paths tab on the Identity profile page

This tab provides visibility into potential attack paths leading to a critical identity or involving it within the path, helping assess security risks. For more information, see [Overview of attack path within Exposure Management.](/security-exposure-management/work-attack-paths-overview)

Additional identity page enhancements:

- New side panel with more information for each entry on the user timeline.

- Filtering capabilities on the Devices tab under Observed in organization.

### Updating 'Protect and manage local admin passwords with Microsoft LAPS' posture recommendation

This update aligns the security posture assessment within Secure Score with the latest version of [Windows LAPS](/windows-server/identity/laps/laps-overview), ensuring it reflects current security best practices for managing local administrator passwords.

### New and updated events in the Advanced hunting IdentityDirectoryEvents table

We have added and updated the following events in the `IdentityDirectoryEvents` table in Advanced Hunting:

- User Account control flag has been changed

- Security group creation in Active directory

- Failed attempt to change an account password

- Successful account password change

- Account primary group ID has been changed

Additionally, the **built-in schema reference** for Advanced Hunting in Microsoft Defender XDR has been updated to include detailed information on all supported event types (**`ActionType`** values) in identity-related tables, ensuring complete visibility into available events. For more information, see [Advanced hunting schema details](/defender-xdr/advanced-hunting-schema-tables).

## January 2025

### New Identity guide tour

Explore key MDI features with the new **Identities Tour** in the Microsoft 365 portal. Navigate Incidents, Hunting, and Settings to enhance identity security and threat investigation.

## December 2024

### New security posture assessment: Prevent Certificate Enrollment with arbitrary Application Policies (ESC15)

Defender for Identity has added the new **Prevent Certificate Enrollment with arbitrary Application Policies (ESC15)** recommendation in Microsoft Secure Score.

This recommendation directly addresses the recently published [CVE-2024-49019](https://msrc.microsoft.com/update-guide/en-US/advisory/CVE-2024-49019), which highlights security risks associated with vulnerable AD CS configurations. This security posture assessment lists all vulnerable certificate templates found in customer environments due to unpatched AD CS servers.

The new recommendation is added to other AD CS-related recommendations. Together, these assessments offer security posture reports that surface security issues and severe misconfigurations that pose risks to the entire organization, together with related detections.

For more information, see:

- [Security assessment: Prevent Certificate Enrollment with arbitrary Application Policies (ESC15)](https://go.microsoft.com/fwlink/?linkid=2296922)

- [Microsoft Defender for Identity's security posture assessments](security-assessment.md)

## October 2024

### MDI is expanding coverage to 10 new Identity posture recommendations (preview)

The new Identity security posture assessments (ISPMs) can help customers monitor misconfiguration by watching for weak spots and reduce the risk of potential attack on on-premises infrastructure.

These new identity recommendations, as part of Microsoft Secure Score, are new security posture reports related to Active Directory infrastructure and Group policy Objects:

- [Accounts with nondefault Primary Group ID](/defender-for-identity/accounts-with-non-default-pgid)

- [Change Domain Controller computer account old password](/defender-for-identity/domain-controller-account-password-change)

- [GPO assigns unprivileged identities to local groups with elevated privileges](/defender-for-identity/gpo-assigns-unprivileged-identities)

- [GPO can be modified by unprivileged accounts](/defender-for-identity/modified-unprivileged-accounts-gpo)

- [Reversible passwords found in GPOs](/defender-for-identity/reversible-passwords-group-policy)

- [Built-in Active Directory Guest account is enabled](/defender-for-identity/built-in-active-directory-guest-account-is-enabled)

- [Unsafe permissions on the DnsAdmins group](/defender-for-identity/unsafe-permissions-dns-admins-group)

- [Ensure that all privileged accounts have the configuration flag "this account is sensitive and can't be delegated"](/defender-for-identity/ensure-privileged-accounts-with-sensitive-flag)

- [Change password of krbtgt account](/defender-for-identity/change-password-krbtgt-account)

- [Change password of built-in domain Administrator account](/defender-for-identity/change-password-domain-administrator-account)

Additionally, we updated the existing recommendation of "Modify unsecure Kerberos delegations to prevent impersonation" to include indication of Kerberos Constrained Delegation with Protocol Transition to a privileged service.

## August 2024

### New Microsoft Entra Connect sensor

As part of our ongoing effort to enhance Microsoft Defender for Identity coverage in hybrid identity environments, we have introduced a new sensor for Microsoft Entra Connect servers. Additionally, we've released new hybrid security detections and new identity posture recommendations specifically for Microsoft Entra Connect, helping customers stay protected and mitigate potential risks.

**New Microsoft Entra Connect Identity posture recommendations:**

- **Rotate password for Microsoft Entra Connect connector account**

- A compromised Microsoft Entra Connect connector account (AD DS connector account, commonly shown as MSOL_XXXXXXXX) can grant access to high-privilege functions like replication and password resets, allowing attackers to modify synchronization settings and compromise security in both cloud and on-premises environments as well as offering several paths for compromising the entire domain. In this assessment, we recommend customers change the password of MSOL accounts with the password last set over 90 days ago. For more information, select [Rotate password for Microsoft Entra Connect connector account](../defender-for-identity/security-posture-assessments/hybrid-security.md#rotate-password-for-microsoft-entra-connect-ad-ds-connector-account).

- **Remove unnecessary replication permissions for Microsoft Entra Connect Account**

- By default, the Microsoft Entra Connect connector account has extensive permissions to ensure proper synchronization (even if they aren't required). If Password Hash Sync isn't configured, it's important to remove unnecessary permissions to reduce the potential attack surface. For more information, see [Remove replication permissions for Microsoft Entra account](/defender-for-identity/security-posture-assessments/hybrid-security#remove-unnecessary-replication-permissions-for-microsoft-entra-connect-ad-ds-connector-account).

- **Change password for Microsoft Entra seamless SSO account configuration**

- This report lists all [Microsoft Entra seamless SSO](/entra/identity/hybrid/connect/how-to-connect-sso) computer accounts with password last set over 90 days ago. The password for the Azure SSO computer account isn't automatically changed every 30 days. If an attacker compromises this account, they can generate service tickets for the AZUREADSSOACC account on behalf of any user and impersonate any user in the Microsoft Entra tenant that is synchronized from Active Directory. An attacker can use this to move laterally from Active Directory into Microsoft Entra ID. For more information, see: [Change password for Microsoft Entra seamless SSO account configuration](/defender-for-identity/security-posture-assessments/hybrid-security#change-password-for-microsoft-entra-seamless-sso-account).

**New Microsoft Entra Connect detections:**

- **Suspicious Interactive Logon to the Microsoft Entra Connect Server**

- Direct logins to Microsoft Entra Connect servers are highly unusual and potentially malicious. Attackers often target these servers to steal credentials for broader network access. Microsoft Defender for Identity can now detect abnormal logins to Microsoft Entra Connect servers, helping you identify and respond to these potential threats faster. It's applicable when the Microsoft Entra Connect server is a standalone server and not operating as a Domain Controller.

- **User Password Reset by Microsoft Entra Connect Account**

- The Microsoft Entra Connect connector account often holds high privileges, including the ability to reset user's passwords. Microsoft Defender for Identity now has visibility into those actions and detects any usage of those permissions that were identified as malicious and non-legitimate. This alert is triggered only if the [password writeback feature](/entra/identity/authentication/concept-sspr-writeback) is disabled.

- **Suspicious writeback by Microsoft Entra Connect on a sensitive user**

- While Microsoft Entra Connect already prevents writeback for users in privileged groups, Microsoft Defender for Identity expands this protection by identifying additional types of sensitive accounts. This enhanced detection helps prevent unauthorized password resets on critical accounts, which can be a crucial step in advanced attacks targeting both cloud and on-premises environments.

**Additional improvements and capabilities:**

- New activity of any **failed password reset on a sensitive account** available in the 'IdentityDirectoryEvents' table in Advanced Hunting. This can help customers track failed password reset events and create custom detection based on this data.

- Enhanced accuracy for the **DC sync attack** detection.

- New [health issue](health-alerts.md) for cases where the sensor is unable to retrieve the configuration from the Microsoft Entra Connect service.

- Extended monitoring for security alerts, such as PowerShell Remote Execution Detector, by enabling the new sensor on Microsoft Entra Connect servers.

[Learn more about the new sensor](deploy/active-directory-federation-services.md).

### Updated DefenderForIdentity PowerShell module

The DefenderForIdentity PowerShell module has been updated, incorporating new functionality and addressing several bug fixes. Key improvements include:

- **New `New-MDIDSA` Cmdlet**: Simplifies creation of service accounts, with a default setting for Group Managed Service Accounts (gMSA) and an option to create standard accounts.

- **Automatic PDCe Detection**: Improves Group Policy Object (GPO) creation reliability by automatically targeting the Primary Domain Controller Emulator (PDCe) for most Active Directory operations.

- **Manual Domain Controller Targeting**: New Server parameter for `Get/Set/Test-MDIConfiguration` cmdlets, allowing you to specify a domain controller for targeting instead of the PDCe.

For more information, see:

- [DefenderForIdentity PowerShell module (PowerShell Gallery)](https://www.powershellgallery.com/packages/DefenderForIdentity/)

- [DefenderForIdentity PowerShell reference documentation](/powershell/defenderforidentity/overview-defenderforidentity)

## July 2024

Six new detections are now in preview:

- **Possible NetSync attack**

- NetSync is a module in Mimikatz, a post-exploitation tool, that requests the password hash of a target device's password by pretending to be a domain controller. An attacker might be performing malicious activities inside the network using this feature to gain access to the organization's resources.

- **Possible takeover of a Microsoft Entra seamless SSO account**

- A Microsoft Entra seamless SSO (single sign-on) account object, AZUREADSSOACC, was modified suspiciously. An attacker might be moving laterally from the on-premises environment to the cloud.

- **Suspicious LDAP query**

- A suspicious Lightweight Directory Access Protocol (LDAP) query associated with a known attack tool was detected. An attacker might be performing reconnaissance for later steps.

- **Suspicious SPN was added to a user**

- A suspicious service principal name (SPN) was added to a sensitive user. An attacker might be attempting to gain elevated access for lateral movement within the organization

- **Suspicious creation of ESXi group**

- A suspicious VMware ESXi group was created in the domain. This might indicate that an attacker is trying to get more permissions for later steps in an attack.

- **Suspicious ADFS authentication**

- A domain-joined account signed in using Active Directory Federation Services (ADFS) from a suspicious IP address. An attacker might have stolen a user's credentials and is using it to move laterally in the organization.

### Defender for Identity release 2.238

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## June 2024

### Easily Go Hunt For user Information From the ITDR Dashboard

The Shield Widget provides a quick overview of the number of users in hybrid, cloud, and on-premises environments. This feature now includes direct links to the Advanced Hunting platform, offering detailed user information at your fingertips.

### ITDR Deployment Health Widget now includes Microsoft Entra Conditional Access and Microsoft Entra Private Access

Now you can view the license availability for Microsoft Entra Workload Conditional Access, Microsoft Entra User Conditional Access, and Microsoft Entra Private Access.

### Defender for Identity release 2.237

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## May 2024

### Defender for Identity release 2.236

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.235

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## April 2024

### Easily detect CVE-2024-21427 Windows Kerberos Security Feature Bypass Vulnerability

To help customers better identify and detect attempts to bypass security protocols according to [this vulnerability](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2024-21427), we added a new activity within Advanced Hunting that monitors Kerberos AS authentication.

With this data, customers can now easily create their own [custom detection rules within Microsoft Defender XDR](https://aka.ms/CustomDetectionsDocs) and automatically trigger alerts for this type of activity.

Access Microsoft Defender portal -> Hunting -> Advanced Hunting.

Now, you can copy our recommended query as provided below, and select on "Create detection rule". Our provided query also tracks failed sign in attempts, which might generate information unrelated to a potential attack. Therefore, feel free to customize the query to suit your specific requirements.

```kusto

IdentityLogonEvents

| where Application == "Active Directory"

| where Protocol == "Kerberos"

| where LogonType in("Resource access", "Failed logon")

| extend Error =  AdditionalFields["Error"]

| extend KerberosType = AdditionalFields['KerberosType']

| where KerberosType == "KerberosAs"

| extend Spns = AdditionalFields["Spns"]

| extend DestinationDC = AdditionalFields["TO.DEVICE"]

| where  Spns !contains "krbtgt" and Spns !contains "kadmin"

| project Timestamp, ActionType, LogonType, AccountUpn, AccountSid, IPAddress, DeviceName, KerberosType, Spns, Error, DestinationDC, DestinationIPAddress, ReportId

```

### Defender for Identity release 2.234

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.233

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## March 2024

### New read-only permissions for viewing Defender for Identity settings

Now you can configure Defender for Identity users with read-only permissions to view Defender for Identity settings.

For more information, see [Required permissions Defender for Identity in Microsoft Defender XDR](role-groups.md#required-permissions-defender-for-identity-in-microsoft-defender-xdr).

### New Graph based API for viewing and managing Health issues

Now you can view and manage Microsoft Defender for Identity health issues through the Graph API.

For more information, see [Managing Health issues through Graph API](/graph/api/resources/security-healthissue?view=graph-rest-beta&preserve-view=true).

### Defender for Identity release 2.232

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.231

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## February 2024

### Defender for Identity release 2.230

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### New security posture assessment for insecure AD CS IIS endpoint configuration

Defender for Identity added the new **Edit insecure ADCS certificate enrollment IIS endpoints (ESC8)** recommendation in Microsoft Secure Score.

Active Directory Certificate Services (AD CS) supports certificate enrollment through various methods and protocols, including enrollment via HTTP using the Certificate Enrollment Service (CES) or the Web Enrollment interface (Certsrv). Insecure configurations of the CES or Certsrv IIS endpoints might create vulnerabilities to relay attacks (ESC8).

The new **Edit insecure ADCS certificate enrollment IIS endpoints (ESC8)** recommendation is added to other AD CS-related recommendations recently released. Together, these assessments offer security posture reports that surface security issues and severe misconfigurations that pose risks to the entire organization, together with related detections.

For more information, see:

- [Security assessment: Edit insecure ADCS certificate enrollment IIS endpoints (ESC8)](/defender-for-identity/security-posture-assessments/certificates#edit-insecure-adcs-certificate-enrollment-iis-endpoints-esc8)

- [Security posture assessments for AD CS sensors](#security-posture-assessments-for-ad-cs-sensors-preview)

- [Microsoft Defender for Identity's security posture assessments](security-assessment.md)

### Defender for Identity release 2.229

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Enhanced user experience for adjusting alert thresholds (Preview)

The Defender for Identity **Advanced Settings** page is now renamed to **Adjust alert thresholds** and provides a refreshed experience with enhanced flexibility for adjusting alert thresholds.

Changes include:

- We removed the previous **Remove learning period** option, and added a new **Recommended test mode** option. Select **Recommended test mode** to set all threshold levels to **Low**, increasing the number of alerts, and sets all other threshold levels to read-only.

- The previous **Sensitivity level** column is now renamed as **Threshold level**, with newly defined values. By default, all alerts are set to a **High** threshold, which represents the default behavior and a standard alert configuration.

The following table lists the mapping between the previous **Sensitivity level** values and the new **Threshold level** values:

|Sensitivity level (previous name)|Threshold level (new name)|

|---|---|

|**Normal**|**High**|

|**Medium**|**Medium**|

|**High**|**Low**|

If you had specific values defined on the **Advanced Settings** page, we transferred them to the new **Adjust alert thresholds** page as follows:

|Advanced settings page configuration|New Adjust alert thresholds page configuration|

|---|---|

|**Remove learning period** toggled on|**Recommended test mode** toggled off. <br/><br/> Alert threshold configuration settings remain the same.|

|**Remove learning period** toggled off|**Recommended test mode** toggled off. <br/><br/> Alert threshold configuration settings are all reset to their default values, with a **High** threshold level.|

Alerts are always triggered immediately if the **Recommended test mode** option is selected, or if a threshold level is set to **Medium** or **Low**, regardless of whether the alert's learning period already completed.

For more information, see [Adjust alert thresholds](advanced-settings.md).

### Device details pages now include device descriptions (Preview)

Microsoft Defender XDR now includes device descriptions on device details panes and device details pages. The descriptions are populated from the device's Active Directory [Description](/windows/win32/adschema/a-description) attribute.

For example, on the device details side pane:

For more information, see [Investigation steps for suspicious devices](investigate-assets.md#investigation-steps-for-suspicious-devices).

### Defender for Identity release 2.228

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor, and the following new alerts:

- [Account Enumeration reconnaissance (LDAP) (external ID 2437)](reconnaissance-discovery-alerts.md#account-enumeration-reconnaissance-ldap-external-id-2437-preview) (Preview)

- [Directory Services Restore Mode Password Change (external ID 2438)](other-alerts.md#directory-services-restore-mode-password-change-external-id-2438) (Preview)

## January 2024

### Defender for Identity release 2.227

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Timeline tab added for group entities

Now you can view Active Directory group entity-related activities and alerts from the last 180 days in Microsoft Defender XDR, such as group membership changes, LDAP queries and so on.

To access the group timeline page, select **Open timeline** on the group details pane.

For example:

For more information, see [Investigation steps for suspicious groups](investigate-assets.md#investigation-steps-for-suspicious-groups).

### Configure and validate your Defender for Identity environment via PowerShell

Defender for Identity now supports the new *DefenderForIdentity* PowerShell module, which is designed to help you configure and validate your environment for working with Microsoft Defender for Identity.

Using the PowerShell commands to avoid misconfigurations and save time and avoiding unnecessary load on your system.

We added the following procedures to the Defender for Identity documentation to help you use the new PowerShell commands:

- [Change proxy configuration using PowerShell](configure-proxy.md#change-proxy-configuration-using-powershell)

- [Configure, get, and test audit policies using PowerShell](configure-windows-event-collection.md#configure-get-and-test-audit-policies-using-powershell)

- [Generate a report with current configurations via PowerShell](configure-windows-event-collection.md#generate-a-report-with-current-configurations-via-powershell)

- [Test your DSA permissions and delegations via PowerShell](directory-service-accounts.md#test-your-dsa-permissions-and-delegations-via-powershell)

- [Test service connectivity using PowerShell](deploy/test-connectivity.md#test-service-connectivity-using-powershell)

For more information, see:

- [DefenderForIdentity PowerShell module (PowerShell Gallery)](https://www.powershellgallery.com/packages/DefenderForIdentity/)

- [DefenderForIdentity PowerShell reference documentation](/powershell/defenderforidentity/overview-defenderforidentity)

### Defender for Identity release 2.226

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.225

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## December 2023

> [!NOTE]

> If you're seeing a decreased number of *Remote code execution attempt* alerts, see our updated [September announcements](#september-2023), which include an [update to the Defender for Identity detection logic](#decreased-number-of-alerts-for-remote-code-execution-attempts). Defender for Identity continues to record the remote code execution activities as before.

### New Identities area and dashboard in Microsoft Defender XDR  (Preview)

Defender for Identity customers now have a new **Identities** area in Microsoft Defender XDR for information about identity security with Defender for Identity.

In Microsoft Defender XDR, select **Identities** to see any of the following new pages:

- **Dashboard**: This page shows graphs and widgets to help you monitor identity threat detection and response activities. For example:

For more information, see [Work with Defender for Identity's ITDR dashboard](dashboard.md).

- **Health issues**: This page is moved from the **Settings > Identities** area, and lists any current health issues for your general Defender for Identity deployment and specific sensors. For more information, see [Microsoft Defender for Identity sensor health issues](health-alerts.md).

- **Tools**: This page contains links to helpful information and resources when working with Defender for Identity. On this page, find links to documentation, specifically on the [capacity planning tool](capacity-planning.md), and the [*Test-MdiReadiness.ps1*](https://github.com/microsoft/Microsoft-Defender-for-Identity/tree/main/Test-MdiReadiness) script.

### Defender for Identity release 2.224

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Security posture assessments for AD CS sensors (Preview)

Defenders for Identity's security posture assessments proactively detect and recommend actions across your on-premises Active Directory configurations.

Recommended actions now include the following new security posture assessments, specifically for certificate templates and certificate authorities.

- **Certificate templates recommended actions**:

- [Prevent users to request a certificate valid for arbitrary users based on the certificate template (ESC1)](/defender-for-identity/security-posture-assessments/certificates#prevent-users-to-request-a-certificate-valid-for-arbitrary-users-based-on-the-certificate-template-esc1--preview)

- [Edit overly permissive certificate template with privileged EKU (Any purpose EKU or No EKU) (ESC2)](/defender-for-identity/security-posture-assessments/certificates#edit-overly-permissive-certificate-template-with-privileged-eku-any-purpose-eku-or-no-eku-esc2)

- [Misconfigured enrollment agent certificate template (ESC3)](/defender-for-identity/security-posture-assessments/certificates#edit-misconfigured-enrollment-agent-certificate-template-esc3)

- [Edit misconfigured certificate templates ACL (ESC4)](/defender-for-identity/security-posture-assessments/certificates#edit-misconfigured-certificate-templates-acl-esc4)

- [Edit misconfigured certificate templates owner (ESC4)](/defender-for-identity/security-posture-assessments/certificates#edit-misconfigured-certificate-templates-owner-esc4)

- **Certificate authority recommended actions**:

- [Edit vulnerable Certificate Authority setting (ESC6)](/defender-for-identity/security-posture-assessments/certificates#security-assessment-edit-vulnerable-ca-setting)

- [Edit misconfigured Certificate Authority ACL (ESC7)](/defender-for-identity/security-posture-assessments/certificates#security-assessment-edit-misconfigured-ca-acl)

- [Enforce encryption for RPC certificate enrollment interface (ESC11)](/defender-for-identity/security-posture-assessments/certificates#security-assessment-enforce-encryption-rpc)

The new assessments are available in Microsoft Secure Score, surfacing security issues, and severe misconfigurations that pose risks to the entire organization, alongside detections. Your score is updated accordingly.

For example:

For more information, see [Microsoft Defender for Identity's security posture assessments](security-assessment.md).

> [!NOTE]

> While *certificate template* assessments are available to all customers that have AD CS installed on their environment, *certificate authority* assessments are available only to customers who have installed a sensor on an AD CS server. For more information, see [New sensor type for Active Directory Certificate Services (AD CS)](#new-sensor-type-for-active-directory-certificate-services-ad-cs).

### Defender for Identity release 2.223

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.222

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.221

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## November 2023

### Defender for Identity release 2.220

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.219

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Identity timeline includes more than 30 days of data (Preview)

Defender for Identity is gradually rolling out extended data retentions on identity details to more than 30 days.

The identity details page **Timeline** tab, which includes activities from Defender for Identity, Microsoft Defender for Cloud Apps, and Microsoft Defender for Endpoint, currently includes a minimum of 150 days and is growing. There might be some variation in data retention rates over the next few weeks.

To view activities and alerts on the identity timeline within a specific time frame, select the default **30 Days** and then select **Custom range**. Filtered data from more than 30 days ago is shown for a maximum of seven days at a time.

For example:

For more information, see [Investigate assets](investigate-assets.md) and [Investigate users in Microsoft Defender XDR](/microsoft-365/security/defender/investigate-users).

### Defender for Identity release 2.218

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## October 2023

### Defender for Identity release 2.217

This version includes the following improvements:

- **Summary report**: The summary report is updated to include two new columns in the *Health issues* tab:

- Details: Additional information on the issue, such as a list of impacted objects or specific sensors on which the issue occurs.

- Recommendations: A list of recommended actions that can be taken to resolve the issue, or how to investigate the issue further.

For more information, see [Download and schedule Defender for Identity reports in Microsoft Defender XDR (Preview)](reports.md).

- **Health issues**: The 'Remove learning period' toggle was automatically switched off for this tenant's health issue.

This version also includes bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.216

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## September 2023

### Decreased number of alerts for Remote Code Execution Attempts

To better align Defender for Identity and Microsoft Defender for Endpoint alerts, we updated the detection logic for the Defender for Identity [Remote code execution attempt](other-alerts.md#remote-code-execution-attempt-external-id-2019) detections.

While this change results in a decreased number of *Remote code execution attempt* alerts, Defender for Identity continues to record the remote code execution activities. Customers can continue to build their own [advanced hunting queries](/microsoft-365/security/defender/advanced-hunting-overview) and create [custom detection policies](/microsoft-365/security/defender/custom-detection-rules).

### Alert sensitivity settings and learning period enhancements

Some Defenders for Identity alerts wait for a *learning period* before alerts are triggered, while building a profile of patterns to use when distinguishing between legitimate and suspicious activities.

Defender for Identity now provides the following enhancements for the learning period experience:

- Administrators can now use the **Remove learning period** setting to configure the sensitivity used for specific alerts. Define the sensitivity as *Normal* to configure the **Remove learning period** setting as *Off* for the selected type of alert.

- After you deploy a new sensor in a new Defender for Identity workspace, the **Remove learning period** setting is automatically turned *On* for 30 days. When 30 days are complete, the **Remove learning period** setting is automatically turned *Off,* and alert sensitivity levels are returned to their default functionality.

To have Defender for Identity use standard learning period functionality, where alerts aren't generated until the learning period is done, configure the **Remove learning periods** setting to *Off*.

If you previously updated the **Remove learning period** setting, your setting remains as you'd configured it.

For more information, see [Advanced settings](advanced-settings.md).

> [!NOTE]

> The **Advanced Settings** page originally listed the *Account enumeration reconnaissance* alert under the **Remove learning period** options as configurable for sensitivity settings. This alert was removed from the list and replaced with the *Security principal reconnaissance (LDAP)* alert. This user interface bug was fixed in November 2023.

### Defender for Identity release 2.215

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity reports moved to the main Reports area

Now you can access Defender for Identity reports from Microsoft Defender XDR's main **Reports** area instead of the **Settings** area. For example:

For more information, see [Download and schedule Defender for Identity reports in Microsoft Defender XDR (Preview)](reports.md).

### Go hunt button for groups in Microsoft Defender XDR

Defender for Identity added the **Go hunt** button for groups in Microsoft Defender XDR. Users can use the **Go hunt** button to query for group-related activities and alerts during an investigation.

For example:

For more information, see [Quickly hunt for entity or event information with go hunt](/microsoft-365/security/defender/advanced-hunting-go-hunt).

### Defender for Identity release 2.214

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Performance enhancements

Defender for Identity made internal improvements for latency, stability, and performance when transferring real-time events from Defender for Identity services to Microsoft Defender XDR. Customers should expect no delays in Defender for Identity data appearing in Microsoft Defender XDR, such as alerts or activities for advanced hunting.

For more information, see:

- [Security alerts in Microsoft Defender for Identity](alerts-overview.md)

- [Microsoft Defender for Identity's security posture assessments](security-assessment.md)

- [Proactively hunt for threats with advanced hunting in Microsoft Defender XDR](/microsoft-365/security/defender/advanced-hunting-overview)

## August 2023

### Defender for Identity release 2.213

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.212

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.211

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### New sensor type for Active Directory Certificate Services (AD CS)

Defender for Identity now supports the new **ADCS** sensor type for a dedicated server with Active Directory Certificate Services (AD CS) configured.

You see the new sensor type identified in the **Settings > Identities > Sensors** page in Microsoft Defender XDR. For more information, see [Manage and update Microsoft Defender for Identity sensors](sensor-settings.md#sensor-details).

Together with the new sensor type, Defender for Identity also now provides related AD CS alerts and Secure Score reports. To view the new alerts and Secure Score reports, make sure that the required events are being collected and logged on your server. For more information, see [Configure auditing for Active Directory Certificate Services (AD CS) events](configure-windows-event-collection.md#configure-auditing-for-active-directory-certificate-services-ad-cs).

AD CS is a Windows Server role that issues and manages public key infrastructure (PKI) certificates in secure communication and authentication protocols. For more information, see [What is Active Directory Certificate Services?](/windows-server/identity/ad-cs/active-directory-certificate-services-overview)

### Defender for Identity release 2.210

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## July 2023

### Defender for Identity release 2.209

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Search for Active Directory groups in Microsoft Defender XDR (Preview)

The Microsoft Defender XDR global search now supports searching by Active Directory group name. Any groups found are shown in the results on a separate **Groups** tab. Select an Active Directory group from your search results to see more details, including:

- Type

- Scope

- Domain

- SAM name

- SID

- Group creation time

- The first time an activity by the group was observed

- Groups that contain the selected group

- A list of all group members

For example:

For more information, see [Microsoft Defender for Identity in Microsoft Defender XDR](/microsoft-365/security/defender/microsoft-365-security-center-mdi?bc=/defender-for-identity/breadcrumb/toc.json&toc=/defender-for-identity/TOC.json).

### New security posture reports

Defender for Identity's identity security posture assessments proactively detect and recommend actions across your on-premises Active Directory configurations.

The following new security posture assessments are now available in Microsoft Secure Score:

- [Remove access rights on suspicious accounts with the Admin SDHolder permission](/defender-for-identity/security-posture-assessments/accounts#remove-access-rights-on-suspicious-accounts-with-the-admin-sdholder-permission)

- [Remove nonadmin accounts with DCSync permissions](/defender-for-identity/security-posture-assessments/accounts#remove-non-admin-accounts-with-dcsync-permissions)

- [Remove local admins on identity assets](/defender-for-identity/security-posture-assessments/identity-infrastructure/#security-assessment-remove-local-admins.md)

- [Start your Defender for Identity deployment](security-assessment-deploy-defender-for-identity.md)

For more information, see [Microsoft Defender for Identity's security posture assessments](security-assessment.md).

### Automatic redirection for the classic Defender for Identity portal

The Microsoft Defender for Identity portal experience and functionality are converged into Microsoft’s extended detection and response (XDR) platform, Microsoft Defender XDR. As of July 6, 2023, customers using the classic Defender for Identity portal are automatically redirected to Microsoft Defender XDR, with no option to revert back to the classic portal.

For more information, see our [blog post](https://techcommunity.microsoft.com/t5/microsoft-365-defender-blog/leveraging-the-convergence-of-microsoft-defender-for-identity-in/ba-p/3856321) and [Microsoft Defender for Identity in Microsoft Defender XDR](/microsoft-365/security/defender/microsoft-365-security-center-mdi).

### Defender for Identity report downloads and scheduling in Microsoft Defender XDR (Preview)

Now you can download and schedule periodic Defender for Identity reports from the Microsoft Defender portal, creating parity in report functionality with the legacy [classic Defender for Identity portal](classic-reports.md).

Download and schedule reports in Microsoft Defender XDR from the **Settings > Identities > Report management** page. For example:

For more information, see [Microsoft Defender for Identity reports in Microsoft Defender XDR](reports.md).

### Defender for Identity release 2.208

- This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.207

- This version provides the new **AccessKeyFile** installation parameter. Use the **AccessKeyFile** parameter during a silent installation of a Defender for Identity sensor, to set the workspace Access Key from a provided text path. For more information, see [Install the Microsoft Defender for Identity sensor](install-sensor.md#defender-for-identity-sensor-silent-installation).

- This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## June 2023

### Defender for Identity release 2.206

- This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Advanced hunting with an enhanced IdentityInfo table

- For tenants with Defender for Identity deployed, the Microsoft 365 **IdentityInfo** advanced hunting table now includes more attributes per identity, and identities detected by the Defender for Identity sensor from your on-premises environment.

For more information, see the [Microsoft Defender XDR advanced hunting documentation](/microsoft-365/security/defender/advanced-hunting-identityinfo-table).

### Defender for Identity release 2.205

- This version includes improvements and bug fixes for internal sensor infrastructure.

## May 2023

### Enhanced Active Directory account control highlights

The Microsoft Defender XDR **Identity** > user details page now includes new Active Directory account control data.

On the user details **Overview** tab, we've added the new **Active Directory account controls** card to highlight important security settings and Active directory controls. For example, use this card to learn whether a specific user is able to bypass password requirements or has a password that never expires.

For example:

For more information, see the [User-Account-Control attribute](/windows/win32/adschema/a-useraccountcontrol) documentation.

### Defender for Identity release 2.204

Released May 29, 2023

- New health alert for VPN (radius) integration data ingestion failures. For more information, see [Microsoft Defender for Identity sensor health alerts](health-alerts.md).

- This version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.203

Released May 15, 2023

- New health alert for verifying that ADFS Container Auditing is configured correctly. For more information, see [Microsoft Defender for Identity sensor health alerts](health-alerts.md).

- The Microsoft Defender 365 **Identity** page includes UI updates for the lateral movement path experience. No functionality was changed.

- This version includes improvements and bug fixes for internal sensor infrastructure.

### Identity timeline enhancements

The identity **Timeline** tab now contains new and enhanced features! With the updated timeline, you can now filter by *Activity type*, *Protocol*, and *Location*, in addition to the original filters. You can also export the timeline to a CSV file and find additional information about activities associated with MITRE ATT&CK techniques. For more information, see [Investigate users in Microsoft Defender XDR](/microsoft-365/security/defender/investigate-users).

### Alert tuning in Microsoft Defender XDR

Alert tuning, now available in Microsoft Defender XDR, allows you to adjust your alerts and optimize them. Alert tuning reduces false positives, allows your SOC teams to focus on high-priority alerts, and improves threat detection coverage across your system.

In Microsoft Defender XDR, create rule conditions based on evidence types, and then apply your rule on any rule type that matches your conditions. For more information, see [Tune an alert](/microsoft-365/security/defender/investigate-alerts#public-preview-tune-an-alert).

## April 2023

### Defender for Identity release 2.202

Released April 23, 2023

- New health alert for verifying that Directory Services Configuration Container Auditing is configured correctly, as described in the [health alerts page](health-alerts.md).

- New workspaces for AD tenants mapped to New Zealand are created in the Australia East region.

- Version includes improvements and bug fixes for internal sensor infrastructure.

## March 2023

### Defender for Identity release 2.201

Released March 27, 2023

- We're in the process of disabling the SAM-R honeytoken alert. While these types of accounts should never be accessed or queried, certain legacy systems might use these accounts as part of their regular operations. If this functionality is necessary for you, you can always create an advanced hunting query and use it as a custom detection. We're also reviewing the LDAP honeytoken alert over the coming weeks, but remains functional for now.

- We fixed detection logic issues in the [Directory Services Object Auditing health alert](health-alerts.md) for non-English operating systems, and for Windows 2012 with Directory Services schemas earlier than version 87.

- We removed the prerequisite of configuring a Directory Services account for the sensors to start. For more information, see [Microsoft Defender for Identity Directory Service account recommendations](directory-service-accounts.md).

- We no longer require logging 1,644 events. If you have this registry setting enabled, you can remove it. For more information, see  [Event ID 1644](configure-windows-event-collection.md#legacy-configurations).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.200

Released March 16, 2023

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.199

Released March 5, 2023

- Some exclusions for the **Honeytoken was queried via SAM-R** alert weren't functioning properly. In these instances, alerts were being triggered even for excluded entities. This error is now fixed.

- **Updated NTLM protocol name for the Identity Advanced Hunting tables**: The old protocol name `Ntlm` is now listed as the new protocol name `NTLM` in Advanced Hunting Identity tables: IdentityLogonEvents, IdentityQueryEvents, IdentityDirectoryEvents.

If you're currently using the `Ntlm` protocol in case-sensitive format from the Identity event tables, you should change it to `NTLM`.

- Version includes improvements and bug fixes for internal sensor infrastructure.

## February 2023

### Defender for Identity release 2.198

Released February 15, 2023

- **Identity timeline is now available as part of the new Identity page in Microsoft Defender XDR**: The updated User page in Microsoft Defender XDR now has a new look and feel, with an expanded view of related assets and a new dedicated timeline tab. The timeline represents activities and alerts from the last 30 days, and it unifies the user’s identity entries across all available workloads (Defender for Identity/Defender for Cloud Apps/Defender for Endpoint). By using the timeline, you can easily focus on activities that the user performed (or were performed on them), in specific timeframes. For more information, see [Investigate users in Microsoft Defender XDR](/microsoft-365/security/defender/investigate-users)

- **Further improvements for honeytoken alerts**: In [release 2.191](whats-new-archive.md#defender-for-identity-release-2191), we introduced several new scenarios to the honeytoken activity alert.

Based on customer feedback, we've decided to split the honeytoken activity alert into five separate alerts:

- Honeytoken user was queried via SAM-R.

- Honeytoken user was queried via LDAP.

- Honeytoken user authentication activity

- Honeytoken user had attributes modified.

- Honeytoken group membership changed.

Additionally, we have added exclusions for these alerts, providing a customized experience for your environment.

We're looking forward to hearing your feedback so we can continue to improve.

- New security alert - **Suspicious certificate usage over Kerberos protocol (PKINIT).**: Many of the techniques for abusing Active Directory Certificate Services (AD CS) involve the use of a certificate in some phase of the attack. Microsoft Defender for Identity now alerts users when it observes such suspicious certificate usage. This behavioral monitoring approach provides comprehensive protection against AD CS attacks, triggering an alert when a suspicious certificate authentication is attempted against a domain controller with a Defender for Identity sensor installed. For more information, see [Microsoft Defender for Identity now detects suspicious certificate usage](https://techcommunity.microsoft.com/t5/security-compliance-and-identity/microsoft-defender-for-identity-now-detects-suspicious/ba-p/3743335).

- **Automatic attack disruption**: Defender for Identity now works together with Microsoft Defender XDR to offer Automated Attack Disruption. This integration means that, for signals coming from Microsoft Defender XDR, we can trigger the **Disable User** action. These actions are triggered by high-fidelity XDR signals, combined with insights from the continuous investigation of thousands of incidents by Microsoft’s research teams. The action suspends the compromised user account in Active Directory and syncs this information to Microsoft Entra ID. For more information about automatic attack disruption, read [the blog post by Microsoft Defender XDR](https://techcommunity.microsoft.com/t5/microsoft-365-defender-blog/what-s-new-in-xdr-at-microsoft-ignite/ba-p/3648872).

You can also exclude specific users from the automated response actions. For more information, see [Configure Defender for Identity automated response exclusions](automated-response-exclusions.md).

- **Remove learning period**: The alerts generated by Defender for Identity are based on various factors such as profiling, deterministic detection, machine learning, and behavioral algorithms that it has learned about your network. The full learning process for Defender for Identity can take up to 30 days per domain controller. However, there might be instances where you would like to receive alerts even before the full learning process has been completed. For example, when you install a new sensor on a domain controller or when you're evaluating the product, you might want to get alerts immediately. In such cases, you can turn off the learning period for the affected alerts by enabling the **Remove learning period** feature. For more information, see [Advanced settings](advanced-settings.md).

- **New way of sending alerts to M365D**: A year ago, we announced that all of [Microsoft Defender for Identity experiences are available in the Microsoft Defender portal](https://techcommunity.microsoft.com/t5/security-compliance-and-identity/all-microsoft-defender-for-identity-features-now-available-in/ba-p/3130037). Our primary alert pipeline is now gradually switching from *Defender for Identity > Defender for Cloud Apps > Microsoft Defender XDR* to *Defender for Identity > Microsoft Defender XDR*. This integration means that status updates in Defender for Cloud Apps **will not be** reflected in Microsoft Defender XDR and vice versa. This change should significantly reduce the time it takes for alerts to appear in the Microsoft Defender portal. As part of this migration, all Defender for Identity policies will no longer be available in the Defender for Cloud Apps portal as of March 5. As always, we recommend using the Microsoft Defender portal for all Defender for Identity experiences.

- Version includes improvements and bug fixes for internal sensor infrastructure.

## January 2023

### Defender for Identity release 2.197

Released January 22, 2023

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.196

Released January 10, 2023

- New health alert for verifying that Directory Services Object Auditing is configured correctly, as described in the [health alerts page](health-alerts.md).

- New health alert for verifying that the sensor’s power settings are configured for optimal performance, as described in the [health alerts page](health-alerts.md).

- We've added [MITRE ATT&CK](https://attack.mitre.org/) information to the IdentityLogonEvents, IdentityDirectoryEvents, and IdentityQueryEvents tables in Microsoft Defender XDR Advanced Hunting. In the **AdditionalFields** column, you can find details about the Attack Techniques and the Tactic (Category) associated with some of our logical activities.

- Since all major Microsoft Defender for Identity features are now available in the Microsoft Defender portal, the portal redirection setting is automatically enabled for each tenant starting January 31, 2023. For more information, see [Redirecting accounts from Microsoft Defender for Identity to Microsoft Defender XDR](/microsoft-365/security/defender/microsoft-365-security-mdi-redirection#what-to-expect).

## December 2022

### Defender for Identity release 2.195

Released December 7, 2022

- Defender for Identity data centers are now also deployed in the Australia East region. For the most current list of regional deployment, see [Defender for Identity components](architecture.md#defender-for-identity-components).

- Version includes improvements and bug fixes for internal sensor infrastructure.

## November 2022

### Defender for Identity release 2.194

Released November 10, 2022

- New health alert for verifying that Directory Services Advanced Auditing is configured correctly, as described in the [health alerts page](health-alerts.md).

- Some of the changes introduced in [Defender for Identity release 2.191](#defender-for-identity-release-2191) regarding honeytoken alerts weren't enabled properly. Those issues have been resolved now.

- From the end of November, manual integration with Microsoft Defender for Endpoint is no longer supported. However, we highly recommend using the Microsoft Defender portal (<https://security.microsoft.com>) which has the integration built in.

- Version includes improvements and bug fixes for internal sensor infrastructure.

## October 2022

### Defender for Identity release 2.193

Released October 30, 2022

- **New security alert: Abnormal Active Directory Federation Services (AD FS) authentication using a suspicious certificate**

This new technique is linked with the infamous NOBELIUM actor and was dubbed "MagicWeb" – it allows an adversary to implant a backdoor on compromised AD FS servers, which will enable impersonation as any domain user and thus access to external resources.

To learn more about this attack, read [this blog post](https://techcommunity.microsoft.com/t5/microsoft-365-defender-blog/protect-your-environment-against-hybrid-identity-attacks/ba-p/3646450).

- Defender for Identity can now use the LocalSystem account on the domain controller to perform remediation actions (enable/disable user, force user reset password), in addition to the gMSA option that was available before. This enables out of the box support for remediation actions. For more information, see [Microsoft Defender for Identity action accounts](deploy/manage-action-accounts.md).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.192

Released October 23, 2022

- New health alert for verifying that the NTLM Auditing is enabled, as described in the [health alerts page](health-alerts.md).

- Version includes improvements and bug fixes for internal sensor infrastructure.

## September 2022

### Defender for Identity release 2.191

Released September 19, 2022

- **More activities to trigger honeytoken alerts**

Microsoft Defender for Identity offers the ability to define honeytoken accounts, which are used as traps for malicious actors. Any authentication associated with these honeytoken accounts (normally dormant), triggers a honeytoken activity (external ID 2014) alert. New for this version, any LDAP, or SAMR query against these honeytoken accounts will trigger an alert. In addition, if event 5136 is audited, an alert is triggered when one of the attributes of the honeytoken was changed or if the group membership of the honeytoken was changed.

For more information, see [Configure Windows Event collection](configure-windows-event-collection.md).

### Defender for Identity release 2.190

Released September 11, 2022

- **Updated assessment: Unsecure domain configurations**

The unsecure domain configuration assessment available through Microsoft Secure Score now assesses the domain controller LDAP signing policy configuration and alerts if it finds an unsecure configuration. For more information, see [Security assessment: Unsecure domain configurations](/defender-for-identity/security-posture-assessments/identity-infrastructure#security-assessment-unsecure-domain-configurations).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.189

Released September 4, 2022

- Version includes improvements and bug fixes for internal sensor infrastructure.

## August 2022

### Defender for Identity release 2.188

Released August 28, 2022

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.187

Released August 18, 2022

- We have changed some of the logic behind how we trigger the [Suspected DCSync attack (replication of directory services) (external ID 2006)](domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006) alert. This detector now covers cases where the source IP address seen by the sensor appears to be a NAT device.

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.186

Released August 10, 2022

- Health alerts will now show the sensor's fully qualified domain name (FQDN) instead of the NetBIOS name.

- New health alerts are available for capturing component type and configuration, as described in the [health alerts page](health-alerts.md).

- Version includes improvements and bug fixes for internal sensor infrastructure.

## July 2022

### Defender for Identity release 2.185

Released July 18, 2022

- An issue was fixed where [Suspected Golden Ticket usage (nonexistent account) (external ID 2027)](domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027) would wrongfully detect macOS devices.

- User actions: We've decided to divide the **Disable User** action on the user page into two different actions:

- Disable User – which disables the user on the Active Directory level

- Suspend User – which disables the user on the Microsoft Entra ID level

We understand that the time it takes to sync from Active Directory to Microsoft Entra ID can be crucial, so now you can choose to disable users in one after the other, to remove the dependency on the sync itself. If a user is disabled only in Microsoft Entra ID, it will be overwritten by Active Directory if the user is still active there.

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.184

Released July 10, 2022

- **New security assessments**

Defender for Identity now includes the following new security assessment:

- Unsecure domain configurations

Microsoft Defender for Identity continuously monitors your environment to identify domains with configuration values that expose a security risk, and reports on these domains to assist you in protecting your environment. For more information, see [Security assessment: Unsecure domain configurations](/defender-for-identity//security-posture-assessments/identity-infrastructure#security-assessment-unsecure-domain-configurations).

- The Defender for Identity installation package will now install the Npcap component instead of the WinPcap drivers. For more information, see [WinPcap and Npcap drivers](/defender-for-identity/technical-faq#winpcap-and-npcap-drivers).

- Version includes improvements and bug fixes for internal sensor infrastructure.

## June 2022

### Defender for Identity release 2.183.15436.10558 (Hotfix)

Released June 20, 2022 (updated July 4, 2022)

- New security alert: Suspected DFSCoerce attack using Distributed File System Protocol

In response to the publishing of a recent attack tool that uses a flow in the DFS protocol, Microsoft Defender for Identity will trigger a security alert whenever an attacker is using this attack method. To learn more about this attack, [read the blog post](https://techcommunity.microsoft.com/t5/security-compliance-and-identity/how-microsoft-defender-for-identity-protects-against-dfscoerce/ba-p/3562912).

### Defender for Identity release 2.183

Released June 20, 2022

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.182

Released June 4, 2022

- A new **About** page for Defender for Identity is available. You can find it in the [Microsoft Defender portal](https://security.microsoft.com), under **Settings** -> **Identities** -> **About**. It provides several important details about your Defender for Identity instance, including the instance name, version, ID, and the geolocation of your instance. This information can be helpful when troubleshooting issues and opening support tickets.

- Version includes improvements and bug fixes for internal sensor infrastructure.

## May 2022

### Defender for Identity release 2.181

Released May 22, 2022

- You can now take [remediation actions](remediation-actions.md) directly on your on-premises accounts, using Microsoft Defender for Identity.

- **Disable user** – This temporarily prevents a user from logging in to the network. It can help prevent compromised users from moving laterally and attempting to exfiltrate data or further compromise the network.

- **Reset user password** – This prompts the user to change their password at the next sign-in, ensuring that this account can't be used for further impersonation attempts.

These actions can be performed from several locations in Microsoft Defender XDR: the user page, the user page side panel, advanced hunting, and even custom detections. This requires setting up a privileged gMSA account that Microsoft Defender for Identity will use to perform the actions. For more information about the requirements, see [Microsoft Defender for Identity action accounts](deploy/manage-action-accounts.md).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.180

Released May 12, 2022

- New security alert: Suspicious modification of a dNSHostName attribute (CVE-2022-26923)

In response to the publishing of a recent CVE, Microsoft Defender for Identity will trigger a security alert whenever an attacker is trying to exploit CVE-2022 -26923. To learn more about this attack, read [the blog post](https://techcommunity.microsoft.com/t5/security-compliance-and-identity/detecting-dnshostname-spoofing-with-microsoft-defender-for/ba-p/3352349).

- In version 2.177, we released additional LDAP activities that can be covered by Defender for Identity. However, we found a bug that causes the events not to be presented and ingested in the Defender for Identity portal. This has been fixed in this release. From version 2.180 onward, when you enable event ID 1644 you don't just get visibility into LDAP activities over Active Directory Web Services, but also other LDAP activities will include  the user who performed the LDAP activity on the source computer. This applies for security alerts and logical activities that are based on LDAP events.

- As a response to the recent KrbRelayUp exploitation, we've released a silent detector to help us evaluate our response to this exploitation. The silent detector allows us to evaluate the effectiveness of the detection, and gather information based on events we're collecting. If this detection will be shown to be in high quality, we'll release a new security alert in the next version.

- We've renamed **Remote code execution over DNS** to **Remote code execution attempt over DNS**, as it better reflects the logic behind these security alerts.

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.179

Released May 1, 2022

- Version includes improvements and bug fixes for internal sensor infrastructure.

## April 2022

### Defender for Identity release 2.178

Released April 10, 2022

- Version includes improvements and bug fixes for internal sensor infrastructure.

## March 2022

### Defender for Identity release 2.177

Released March 27, 2022

- Microsoft Defender for Identity can now monitor additional LDAP queries in your network. These LDAP activities are sent over the Active Directory Web Service protocol and act like normal LDAP queries. To have visibility into these activities, you need to enable event 1644 on your domain controllers. This event covers LDAP activities in your domain and is primarily used to identify expensive, inefficient, or slow Lightweight Directory Access Protocol (LDAP) searches that are serviced by Active Directory domain controllers. For more information, see

[Legacy configurations](configure-windows-event-collection.md#legacy-configurations).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.176

Released March 16, 2022

- Beginning with this version, when installing the sensor from a new package, the sensor's version under **Add/Remove Programs** appear with the full version number (for example, 2.176.x.y), as opposed to the static 2.0.0.0 that was previously shown. It continues to show that version (the one installed through the package) even though the version will be updated through the automatic updates from the Defender for Identity cloud services. The real version can be seen in the [sensor settings page](https://security.microsoft.com/settings/identities?tabid=sensor) in the portal, in the executable path or in the file version.

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.175

Released March 6, 2022

- Version includes improvements and bug fixes for internal sensor infrastructure.

## February 2022

### Defender for Identity release 2.174

Released February 20, 2022

- We've added the **shost** FQDN of the account involved in the alert to the message sent to the SIEM. For more information, see [Microsoft Defender for Identity SIEM log reference](cef-format-sa.md).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.173

Released February 13, 2022

- All Microsoft Defender for Identity features now available in the Microsoft Defender portal. For more information, see [this blog post](https://techcommunity.microsoft.com/t5/security-compliance-and-identity/all-microsoft-defender-for-identity-features-now-available-in/ba-p/3130037).

- This release fixes [issues when installing the sensor on Windows Server 2019 with KB5009557 installed, or on a server with hardened EventLog permissions](troubleshooting-known-issues.md#problem-installing-the-sensor-on-windows-server-2019-with-kb5009557-installed-or-on-a-server-with-hardened-eventlog-permissions).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.172

Released February 8, 2022

- Version includes improvements and bug fixes for internal sensor infrastructure.

## January 2022

### Defender for Identity release 2.171

Released January 31, 2022

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.170

Released January 24, 2022

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.169

Released January 17, 2022

- We're happy to release the ability to configure an action account for Microsoft Defender for Identity. This is the first step in the ability to take actions on users directly from the product. As first step, you can define the gMSA account Microsoft Defender for Identity will use to take the actions. We highly recommend you start creating these users to enjoy the Actions feature once it's live. For more information, see [Manage action accounts](deploy/manage-action-accounts.md).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.168

Released January 9, 2022

- Version includes improvements and bug fixes for internal sensor infrastructure.

## December 2021

### Defender for Identity release 2.167

Released December 29, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.166

Released December 27, 2021

- Version includes a new security alert: [Suspicious modification of a sAMNameAccount attribute (CVE-2021-42278 and CVE-2021-42287 exploitation) (external ID 2419)](compromised-credentials-alerts.md#suspicious-modification-of-a-samnameaccount-attribute-cve-2021-42278-and-cve-2021-42287-exploitation-external-id-2419).

In response to the publishing of recent CVEs, Microsoft Defender for Identity will trigger a security alert whenever an attacker is trying to exploit CVE-2021-42278 and CVE-2021-42287. To learn more about this attack, [read the blog post](https://techcommunity.microsoft.com/t5/security-compliance-and-identity/sam-name-impersonation/ba-p/3042699).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.165

Released December 6, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

## November 2021

### Defender for Identity release 2.164

Released November 17, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.163

Released November 8, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.162

Released November 1, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

## September 2021

### Defender for Identity release 2.161

Released September 12, 2021

- Version includes new monitored activity: gMSA account password was retrieved by a user. For more information, see [Microsoft Defender for Identity monitored activities](monitored-activities.md#monitored-user-activities-domain-controller-based-user-operations)

- Version includes improvements and bug fixes for internal sensor infrastructure.

## August 2021

### Defender for Identity release 2.160

Released August 22, 2021

- Version includes various improvements and covers more scenarios according to the latest changes in the PetitPotam exploitation.

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.159

Released August 15, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

- Version includes an improvement to the newly published alert: Suspicious network connection over Encrypting File System Remote Protocol (external ID 2416).

We extended the support for this detection to trigger when a potential attacker communicating over an encrypted EFS-RPCchannel. Alerts triggered when the channel is encrypted will be treated as a Medium severity alert, as opposed to High when it’s not encrypted. To learn more about the alert, see [Suspicious network connection over Encrypting File System Remote Protocol (external ID 2416)](lateral-movement-alerts.md#suspicious-network-connection-over-encrypting-file-system-remote-protocol-external-id-2416).

### Defender for Identity release 2.158

Released August 8, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

- Version includes a new security alert: Suspicious network connection over Encrypting File System Remote Protocol (external ID 2416).

In this detection, Microsoft Defender for Identity will trigger a security alert whenever an attacker is trying to exploit the EFS-RPC against the domain controller. This attack vector is associated with the recent PetitPotam attack. To learn more about the alert, see [Suspicious network connection over Encrypting File System Remote Protocol (external ID 2416)](lateral-movement-alerts.md#suspicious-network-connection-over-encrypting-file-system-remote-protocol-external-id-2416).

- Version includes a new security alert: Exchange Server Remote Code Execution (CVE-2021-26855) (external ID 2414)

In this detection, Microsoft Defender for Identity will trigger a security alert whenever an attacker tries to change the "msExchExternalHostName" attribute on the Exchange object for remote code execution. To learn more about this alert, see [Exchange Server Remote Code Execution (CVE-2021-26855) (external ID 2414)](lateral-movement-alerts.md#exchange-server-remote-code-execution-cve-2021-26855-external-id-2414). This detection relies on Windows event 4662, so it must be enabled beforehand. For information on how to configure and collect this event, see [Configure Windows Event collection](configure-windows-event-collection.md), and follow the instructions for [Enable auditing on an Exchange object](configure-windows-event-collection.md#enable-auditing-on-an-exchange-object).

### Defender for Identity release 2.157

Released August 1, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

## July 2021

### Defender for Identity release 2.156

Released July 25, 2021

- Starting from this version, we're adding the Npcap driver executable to the sensor installation package. For more information, see [WinPcap and Npcap drivers](/defender-for-identity/technical-faq#winpcap-and-npcap-drivers).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.155

Released July 18, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.154

Released July 11, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

- Version includes added improvements and detections for the print spooler exploitation known as PrintNightmare detection, to cover more attack scenarios.

### Defender for Identity release 2.153

Released July 4, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

- Version includes a new security alert: Suspected Windows Print Spooler service exploitation attempt (CVE-2021-34527 exploitation) (external ID 2415).

In this detection, Defender for Identity triggers a security alert whenever an attacker tries to exploit the Windows Print Spooler Service against the domain controller. This attack vector is associated with the print spooler exploitation, and is known as PrintNightmare. [Learn more](lateral-movement-alerts.md#suspected-exploitation-attempt-on-windows-print-spooler-service-external-id-2415) about this alert.

## June 2021

### Defender for Identity release 2.152

Released June 27, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.151

Released June 20, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.150

Released June 13, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

## May 2021

### Defender for Identity release 2.149

Released May 31, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.148

Released May 23, 2021

- If you [configure and collect](configure-windows-event-collection.md) event ID 4662, Defender for Identity will report which user made the [Update Sequence Number (USN)](/powershell/module/activedirectory/get-adreplicationuptodatenessvectortable#description) change to various Active Directory object properties. For example, if an account password is changed, and event 4662 is enabled, the event records who changed the password.

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.147

Released May 9, 2021

- Based on customer feedback, we're increasing the default number of allowed sensors from 200 to 350, and the Directory Services credentials from 10 to 30.

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.146

Released May 2, 2021

- Email notifications for both health issues and security alerts will now have the investigation URL for both Microsoft Defender for Identity and Microsoft Defender XDR.

- Version includes improvements and bug fixes for internal sensor infrastructure.

## April 2021

### Defender for Identity release 2.145

Released April 22, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.144

Released April 12, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

## March 2021

### Defender for Identity release 2.143

Released March 14, 2021

- We've added Windows Event 4741 to detect *computer accounts added to Active Directory* activities. [Configure the new event](configure-windows-event-collection.md) to be collected by Defender for Identity. Once configured, collected events are available to view in the activity log and the Microsoft Defender XDR Advanced Hunting.

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.142

Released March 7, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

## February 2021

### Defender for Identity release 2.141

Released February 21, 2021

- **New security alert: Suspected AS-REP Roasting attack (external ID 2412)**

Defender for Identity's *Suspected AS-REP Roasting attack (external ID 2412)* security alert is now available. In this detection, a Defender for Identity security alert is triggered when an attacker targets accounts with disabled Kerberos preauthentication, and attempts to obtain Kerberos TGT data. The attacker's intent might be to extract the credentials from the data using offline password cracking attacks. For more information, see [Kerberos AS-REP Roasting exposure (external ID 2412)](compromised-credentials-alerts.md#suspected-as-rep-roasting-attack-external-id-2412).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.140

Released February 14, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

## January 2021

### Defender for Identity release 2.139

Released January 31, 2021

- We've updated the severity for the Suspected Kerberos SPN exposure to high to better reflect the impact of the alert. For more information about the alert, see [Suspected Kerberos SPN exposure (external ID 2410)](compromised-credentials-alerts.md#suspected-kerberos-spn-exposure-external-id-2410)

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.138

Released January 24, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.137

Released January 17, 2021

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.136

Released January 3, 2021

- Defender for Identity now supports installing sensors on Active Directory Federation Services (AD FS) servers. Installing the sensor on [compatible AD FS Servers](deploy/active-directory-federation-services.md) extends Microsoft Defender for Identity visibility into hybrid environment by monitoring this critical infrastructure component. We also refreshed some of our existing detections ([Suspicious service creation](domain-dominance-alerts.md#suspicious-service-creation-external-id-2026), [Suspected Brute Force attack (LDAP)](compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004), [Account enumeration reconnaissance](reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)) to work on AD FS data as well. To start deployment of the Microsoft Defender for Identity sensor for AD FS server, [download the latest deployment package](install-sensor.md) from the sensor configuration page.

- Version includes improvements and bug fixes for internal sensor infrastructure.

## December 2020

### Defender for Identity release 2.135

Released December 20, 2020

- We've improved our [Active Directory attributes reconnaissance (LDAP) (external ID 2210)](reconnaissance-alerts.md#active-directory-attributes-reconnaissance-ldap-external-id-2210) alert to also detect techniques used to obtain the information needed in order to generate security tokens, such as seen as part of the [Solorigate campaign](https://aka.ms/solorigate).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.134

Released December 13, 2020

- Our [recently released NetLogon detector](#azure-atp-release-2127) has been enhanced to also work when the Netlogon channel transaction occurs over an encrypted channel. For more information about the detector, see [Suspected Netlogon privilege elevation attempt](compromised-credentials-alerts.md#suspected-netlogon-priv-elev-2411).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.133

Released December 6, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

## November 2020

### Defender for Identity release 2.132

Released November 17, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Defender for Identity release 2.131

Released November 8, 2020

- **New security alert: Suspected Kerberos SPN exposure (external ID 2410)**

Defender for Identity's *Suspected Kerberos SPN exposure (external ID 2410)* security alert is now available. In this detection, a Defender for Identity security alert is triggered when an attacker enumerates service accounts and their respective SPNs, and then requests Kerberos TGS tickets for the services. The attacker's intent might be to extract the hashes from the tickets and save them for later use in offline brute force attacks. For more information, see [Kerberos SPN exposure](compromised-credentials-alerts.md#suspected-kerberos-spn-exposure-external-id-2410).

- Version includes improvements and bug fixes for internal sensor infrastructure.

## October 2020

### Defender for Identity release 2.130

Released October 25, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.129

Released October 18, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

## September 2020

### Azure ATP release 2.128

Released September 27, 2020

- **Modified email notifications configuration**

We're removing the **Mail notification** toggles for turning on email notifications. To receive email notifications, simply add an address. For more information, see [Set notifications](notifications.md).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.127

Released September 20, 2020

- **New security alert: Suspected Netlogon privilege elevation attempt (external ID 2411)**

Azure ATP's *Suspected Netlogon privilege elevation attempt (CVE-2020-1472 exploitation) (external ID 2411)* security alert is now available. In this detection, an Azure ATP security alert is triggered when an attacker establishes a vulnerable Netlogon secure channel connection to a domain controller, using the Netlogon Remote Protocol ([MS-NRPC](/openspecs/windows_protocols/ms-nrpc/ff8f970f-3e37-40f7-bd4b-af7336e4792f)), also known as *Netlogon Elevation of Privilege Vulnerability*. For more information, see [Suspected Netlogon privilege elevation attempt](compromised-credentials-alerts.md#suspected-netlogon-priv-elev-2411).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.126

Released September 13, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.125

Released September 6, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

## August 2020

### Azure ATP release 2.124

Released August 30, 2020

- **New security alerts**

Azure ATP security alerts now include the following new detections:

- **Active Directory attributes reconnaissance (LDAP) (external ID 2210)**

In this detection, an Azure ATP security alert is triggered when an attacker is suspected of successfully gaining critical information about the domain for use in their attack kill chain. For more information, see [Active Directory attributes reconnaissance](reconnaissance-alerts.md#active-directory-attributes-reconnaissance-ldap-external-id-2210).

- **Suspected rogue Kerberos certificate usage (external ID 2047)**

In this detection, an Azure ATP security alert is triggered when an attacker that has gained control over the organization by compromising the certificate authority server is suspected of generating certificates that can be used as backdoor accounts in future attacks, such as moving laterally in your network. For more information, see [Suspected rogue Kerberos certificate usage](lateral-movement-alerts.md#suspected-rogue-kerberos-certificate-usage-external-id-2047).

- **Suspected golden ticket usage (ticket anomaly using RBCD) (external ID 2040)**

Attackers with domain admin rights can compromise the KRBTGT account. Using the KRBTGT account, they can create a Kerberos ticket-granting ticket (TGT) that provides authorization to any resource.

This forged TGT is called a "Golden Ticket" because it allows attackers to achieve lasting network persistence using Resource Based Constrained Delegation (RBCD). Forged Golden Tickets of this type have unique characteristics this new detection is designed to identify.

For more information, see [Suspected golden ticket usage (ticket anomaly using RBCD)](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-using-rbcd-external-id-2040).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.123

Released August 23, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.122

Released August 16, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.121

Released August 2, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

## July 2020

### Azure ATP release 2.120

Released July 26, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.119

Released July 5, 2020

- **Feature enhancement: New *Excluded domain controllers* tab in Excel report**

To improve the accuracy of our domain controller coverage calculation, we'll be excluding domain controllers with external trusts from the calculation toward achieving 100% coverage. Excluded domain controllers are surfaced in the new *excluded domain controllers* tab in the domain coverage Excel report download. For information about downloading the report, see [Domain controller status](/defender-for-identity/sensor-settings#domain-controller-status).

- Version includes improvements and bug fixes for internal sensor infrastructure.

## June 2020

### Azure ATP release 2.118

Released June 28, 2020

- **New security assessments**

Azure ATP security assessments now include the following new assessments:

- **Riskiest lateral movement paths**

This assessment continuously monitors your environment to identify **sensitive** accounts with the riskiest lateral movement paths that expose a security risk, and reports on these accounts to assist you in managing your environment. Paths are considered risky if they have three or more non-sensitive accounts that can expose the sensitive account to credential theft by malicious actors. For more information, see [Security assessment: Riskiest lateral movement paths (LMP)](/defender-for-identity/security-assessment-riskiest-lmp).

- **Unsecure account attributes**

This assessment Azure ATP continuously monitors your environment to identify accounts with attribute values that expose a security risk, and reports on these accounts to assist you in protecting your environment. For more information, see [Security assessment: Unsecure account attributes](/defender-for-identity/security-assessment-unsecure-account-attributes).

- **Updated sensitivity definition**

We're expanding our sensitivity definition for on-premises accounts to include entities that are allowed to use Active Directory replication.

### Azure ATP release 2.117

Released June 14, 2020

- **Feature enhancement: Additional activity details available**

We've extended the device information we send to Defender for Cloud Apps including device names, IP addresses, account UPNs, and used port. For more information about our integration with Defender for Cloud Apps, see [Using Azure ATP with Defender for Cloud Apps](/defender-for-identity/deploy-defender-identity).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.116

Released June 7, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

## May 2020

### Azure ATP release 2.115

Released May 31, 2020

- **New security assessments**

Azure ATP security assessments now include the following new assessments:

- **Unsecure SID History attributes**

This assessment reports on SID History attributes that can be used by malicious attackers to gain access to your environment. For more information, see [Security assessment: Unsecure SID History attributes](/defender-for-identity/security-assessment-unsecure-sid-history-attribute).

- **Microsoft LAPS usage**

This assessment reports on local administrator accounts not using Microsoft's "Local Administrator Password Solution" (LAPS) to secure their passwords. Using LAPS simplifies password management and also helps defend against cyberattacks. For more information, see [Security assessment: Microsoft LAPS usage](/defender-for-identity/security-assessment-laps).

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.114

Released May 17, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.113

Released May 5, 2020

- **Feature enhancement: Enriched Resource Access Activity with NTLMv1**

Starting from this version, Azure ATP now provides information for resource access activities showing whether the resource uses NTLMv1 authentication. This resource configuration is unsecure and poses a risk that malicious actors can force the application to their advantage. For more information about the risk, see [Legacy protocols usage](/defender-for-identity/security-assessment-legacy-protocols).

- **Feature enhancement: Suspected Brute Force attack (Kerberos, NTLM) alert**

Brute Force attack is used by attackers to gain a foothold into your organization and is a key method for threat and risk discovery in Azure ATP. To help you focus on the critical risks to your users, this update makes it easier and faster to analyze and remediate risks, by limiting and prioritizing the volume of alerts.

## March 2020

### Azure ATP release 2.112

Released March 15, 2020

- **New Azure ATP instances automatically integrate with Microsoft Defender for Cloud Apps**

When creating an Azure ATP instance (formerly instance), the integration with Microsoft Defender for Cloud Apps is enabled by default. For more information about the integration, see [Using Azure ATP with Microsoft Defender for Cloud Apps](/defender-for-identity/deploy-defender-identity).

- **New monitored activities**

The following activity monitors are now available:

- Interactive Logon with Certificate

- Failed Logon with Certificate

- Delegated Resource Access

Learn more about which [activities Azure ATP monitors](monitored-activities.md), and how to [filter and search monitored activities](/defender-for-identity/monitored-activities) in the portal.

- **Feature enhancement: Enriched Resource Access Activity**

Starting from this version, Azure ATP now provides information for resource access activities showing whether the resource is trusted for unconstrained delegation. This resource configuration is unsecure and poses a risk that malicious actors can force the application to their advantage. For more information about the risk, see [Security assessment: Unsecure Kerberos delegation](/defender-for-identity/security-assessment-unconstrained-kerberos).

- **Suspected SMB packet manipulation (CVE-2020-0796 exploitation) - (preview)**

Azure ATP's [Suspected SMB packet manipulation](lateral-movement-alerts.md) security alert is now in public preview. In this detection, an Azure ATP security alert is triggered when SMBv3 packets are suspected of exploiting the [CVE-2020-0796](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2020-0796) security vulnerability are made against a domain controller in the network.

### Azure ATP release 2.111

Released March 1, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

## February 2020

### Azure ATP release 2.110

Released February 23, 2020

- **New security assessment: Unmonitored domain controllers**

Azure ATP security assessments now include a report on unmonitored domain controllers, servers without a sensor, to help you in managing full coverage of your environment. For more information, see [Unmonitored domain controllers](/defender-for-identity/security-assessment-unmonitored-domain-controller).

### Azure ATP release 2.109

Released February 16, 2020

- **Feature enhancement: Sensitive entities**

Starting from this version (2.109), machines identified as Certificate Authority, DHCP, or DNS Servers by Azure ATP are now automatically tagged as **Sensitive**.

### Azure ATP release 2.108

Released February 9, 2020

- **New feature: Support for group Managed Service Accounts**

Azure ATP now supports using group Managed Service Accounts (gMSA) for improved security when connecting Azure ATP sensors to your Microsoft Entra forests. For more information about using gMSA with Azure ATP sensors, see [Connect to your Active Directory Forest](/defender-for-identity/directory-service-accounts#prerequisites).

- **Feature enhancement: Scheduled report with too much data**

When a scheduled report has too much data, the email now informs you of the fact by displaying the following text: There was too much data during the specified period to generate a report. This replaces the previous behavior of only discovering the fact after clicking the report link in the email.

- **Feature enhancement: Updated domain controller coverage logic**

We've updated our domain controller coverage report logic to include additional information from Microsoft Entra ID, resulting in a more accurate view of domain controllers without sensors on them. This new logic should also have a positive effect on the corresponding Microsoft Secure Score.

### Azure ATP release 2.107

Released February 3, 2020

- **New monitored activity: SID history change**

SID history change is now a monitored and filterable activity. Learn more about which [activities Azure ATP monitors](monitored-activities.md), and how to [filter and search monitored activities](/defender-for-identity/monitored-activities) in the portal.

- **Feature enhancement: Closed or suppressed alerts are no longer reopened**

Once an alert is closed or suppressed in the Azure ATP portal, if the same activity is detected again within a short period of time, a new alert is opened. Previously, under the same conditions, the alert was reopened.

- **TLS 1.2 required for portal access and sensors**

TLS 1.2 is now required to use Azure ATP sensors and the cloud service. Access to the Azure ATP portal will no longer be possible using browsers that don't support TLS 1.2.

## January 2020

### Azure ATP release 2.106

Released January 19, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.105

Released January 12, 2020

- Version includes improvements and bug fixes for internal sensor infrastructure.

## December 2019

### Azure ATP release 2.104

Released December 23, 2019

- **Sensor version expirations eliminated**

Azure ATP sensor deployment and sensor installation packages no longer expire after a number of versions and now only update themselves once. The result of this feature is that previously downloaded sensor installation packages can now be installed even if they're older than our max number of lapsed versions.

- **Confirm compromise**

You can now confirm compromise of specific Microsoft 365 users and set their risk level to **high**. This workflow allows your security operations teams another response capability to reduce their security incidents Time-To-Resolve thresholds. Learn more about [how to confirm compromise](/cloud-app-security/tutorial-ueba?branch=pr-en-us-1204#phase-4-protect-your-organization) using Azure ATP and Defender for Cloud Apps.

- **New experience banner**

On Azure ATP portal pages where a new experience is available in the Defender for Cloud Apps portal, new banners are displayed describing what's available with access links.

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.103

Released December 15, 2019

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.102

Released December 8, 2019

- Version includes improvements and bug fixes for internal sensor infrastructure.

## November 2019

### Azure ATP release 2.101

Released November 24, 2019

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.100

Released November 17, 2019

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.99

Released November 3, 2019

- **Feature enhancement:  Added user interface notification of Defender for Cloud Apps portal availability to the Azure ATP portal**

Ensuring all users are aware of the availability of the enhanced features available using the Defender for Cloud Apps portal, notification was added for the portal from the existing Azure ATP alert timeline.

- Version includes improvements and bug fixes for internal sensor infrastructure.

## October 2019

### Azure ATP release 2.98

Released October 27, 2019

- **Feature enhancement: Suspected brute force attack alert**

Improved the [Suspected brute force attack (SMB)](compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033) alert using additional analysis, and improved detection logic to reduce **benign true positive (B-TP)** and **false positive (FP)** alert results.

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.97

Released October 6, 2019

- Version includes improvements and bug fixes for internal sensor infrastructure.

## September 2019

### Azure ATP release 2.96

Released September 22, 2019

- **Enriched NTLM authentication data using Windows Event 8004**

Azure ATP sensors are now able to automatically read and enrich the NTLM authentications activities with your accessed server data when NTLM auditing is enabled, and Windows Event 8004 is turned on. Azure ATP parses Windows Event 8004 for NTLM authentications in order to enrich the NTLM authentication data used for Azure ATP threat analysis and alerts. This enhanced capability provides resource access activity over NTLM data and enriched failed logon activities including the destination computer, which the user attempted but failed to access.

Learn more about NTLM authentication activities [using Windows Event 8004](configure-windows-event-collection.md#configure-ntlm-auditing).

- Version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.95

Released September 15, 2019

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.94

Released September 8, 2019

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.93

Released September 1, 2019

- Version includes improvements and bug fixes for internal sensor infrastructure.

## August 2019

### Azure ATP release 2.92

Released August 25, 2019

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.91

Released August 18, 2019

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.90

Released August 11, 2019

- Version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.89

Released August 4, 2019

- **Sensor method improvements**

To avoid excess NTLM traffic generation in creation of accurate Lateral Movement Path (LMP) assessments, improvements have been made to Azure ATP sensor methods to rely less on NTLM usage and make more significant use of Kerberos.

- **Alert enhancement: Suspected Golden Ticket usage (nonexistent account)**

SAM name changes have been added to the supporting evidence types listed in this type of alert. To learn more about the alert, including how to prevent this type of activity and remediate, see  [Suspected Golden Ticket usage (nonexistent account)](domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027).

- **General availability: Suspected NTLM authentication tampering**

The [Suspected NTLM authentication tampering](lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039) alert is no longer in preview mode and is now generally available.

- Version includes improvements and bug fixes for internal sensor infrastructure.

## July 2019

### Azure ATP release 2.88

Released July 28, 2019

- This version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.87

Released July 21, 2019

- **Feature enhancement: Automated Syslog event collection for Azure ATP standalone sensors**

Incoming Syslog connections for Azure ATP standalone sensors are now fully automated, while removing the toggle option from the configuration screen. These changes have no effect on outgoing Syslog connections.

- This version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.86

Released July 14, 2019

- **New security alert: Suspected NTLM authentication tampering (external ID 2039)**

Azure ATP's new [Suspected NTLM authentication tampering](lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039) security alert is now in public preview.    In this detection, an Azure ATP security alert is triggered when use of "man-in-the-middle" attack is suspected of successfully bypassing NTLM Message Integrity Check (MIC), a security vulnerability detailed in Microsoft [CVE-2019-1040](https://msrc.microsoft.com/update-guide/advisory/CVE-2019-1040). These types of attacks attempt to downgrade NTLM security features and successfully authenticate, with the ultimate goal of making successful lateral movements.

- **Feature enhancement: Enriched device operating system identification**

Until now, Azure ATP provided entity device operating system information based on the available attribute in Active Directory. Previously, if operating system information was unavailable in Active Directory, the information was also unavailable on Azure ATP entity pages. Starting from this version, Azure ATP now provides this information for devices where Active Directory doesn't have the information, or aren't registered in Active Directory, by using enriched device operating system identification methods.

The addition of enriched device operating system identification data helps identify unregistered and non-Windows devices, while simultaneously aiding in your investigation process. For learn more about Network Name Resolution in Azure ATP, see [Understanding Network Name Resolution (NNR)](nnr-policy.md).

- **New feature: Authenticated proxy - preview**

Azure ATP now supports authenticated proxy. Specify the proxy URL using the sensor command line and specify Username/Password to use proxies that require authentication. For more information about how to use authenticated proxy, see [Configure the proxy](configure-proxy.md).

- **Feature enhancement: Automated domain synchronizer process**

The process of designating and tagging domain controllers as domain synchronizer candidates during setup and ongoing configuration is now fully automated. The toggle option to manually select domain controllers as domain synchronizer candidates is removed.

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.85

Released July 7, 2019

- This version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.84

Released July 1, 2019

- **New location support: Azure UK data center**

Azure ATP instances are now supported in the Azure UK data center. To learn more about creating Azure ATP instances and their corresponding data center locations, see [Step 1 of Azure ATP installation](/defender-for-identity/deploy-defender-identity).

- **Feature enhancement: New name and features for the Suspicious additions to sensitive groups alert (external ID 2024)**

The **Suspicious additions to sensitive groups** alert was previously named the **Suspicious modifications to sensitive groups** alert. The external ID of the alert (ID 2024) remains the same. The descriptive name change more accurately reflects the purpose of alerting on additions to your **sensitive** groups. The enhanced alert also features new evidence and improved descriptions. For more information, see [Suspicious additions to sensitive groups](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024).

- **New documentation feature: Guide for moving from Advanced Threat Analytics to Azure ATP**

This new article includes prerequisites, planning guidance, and configuration and verification steps for moving from ATA to Azure ATP service. For more information, see [Move from ATA to Azure ATP](migrate-from-ata-overview.md).

- This version also includes improvements and bug fixes for internal sensor infrastructure.

## June 2019

### Azure ATP release 2.83

Released June 23, 2019

- **Feature enhancement: Suspicious service creation alert (external ID 2026)**

This alert now features an improved alert page with additional evidence and a new description. For more information, see [Suspicious service creation security alert](domain-dominance-alerts.md#suspicious-service-creation-external-id-2026).

- **Instance naming support: Support added for digit only domain prefix**

Support added for Azure ATP instance creation using initial domain prefixes that only contain digits. For example, use of digit only initial domain prefixes such as  123456.contoso.com are now supported.

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.82

Released June 18, 2019

- **New public preview**

Azure ATP's identity threat investigation experience is now in **Public Preview**, and available to all Azure ATP protected tenants. See [Azure ATP Microsoft Defender for Cloud Apps investigation experience](/defender-for-identity/deploy-defender-identity) to learn more.

- **General availability**

Azure ATP support for untrusted forests is now in general availability. See [Azure ATP multi-forest](deploy/multi-forest.md) to learn more.

- This version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.81

Released June 10, 2019

- This version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.80

Released June 2, 2019

- **Feature enhancement: Suspicious VPN connection alert**

This alert now includes enhanced evidence and texts for better usability. For more information about alert features, and suggested remediation steps and prevention, see the [Suspicious VPN connection alert description](compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025).

- This version also includes improvements and bug fixes for internal sensor infrastructure.

## May 2019

### Azure ATP release 2.79

Released May 26, 2019

- **General availability: Security principal reconnaissance (LDAP) (external ID 2038)**

This alert is now in GA (general availability). For more information about the alert,  alert features and suggested remediation and prevention, see the [Security principal reconnaissance (LDAP) alert description](reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.78

Released May 19, 2019

- **Feature enhancement: Sensitive entities**

Manual Sensitive tagging for Exchange Servers

You can now manually tag entities as Exchange Servers during configuration.

To manually tag an entity as an Exchange Server:

1. In the Azure ATP portal, select **Configuration**.

2. Under **Detection**, select **Entity tags**, then select **Sensitive**.

3. Select **Exchange Servers** and then add the entity you wish to tag.

After tagging a computer as an Exchange Server, it will be tagged as Sensitive and display that it was tagged as an Exchange Server. The Sensitive tag appears in the computer's entity profile, and the computer will be considered in all detections that are based on Sensitive accounts and Lateral Movement Paths.

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.77

Released May 12, 2019

- This version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.76

Released May 6, 2019

- This version includes improvements and bug fixes for internal sensor infrastructure.

## April 2019

### Azure ATP release 2.75

Released April 28, 2019

- **Feature enhancement: Sensitive entities**

Starting from this version (2.75), machines identified as Exchange Servers by Azure ATP are now automatically tagged as **Sensitive**.

Entities that are automatically tagged as **Sensitive** because they function as Exchange Servers list this classification as the reason they're tagged.

- This version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.74

Releasing April 14, 2019

- This version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.73

Released April 10, 2019

- This version includes improvements and bug fixes for internal sensor infrastructure.

## March 2019

### Azure ATP release 2.72

Released March 31, 2019

- **Feature enhancement: Lateral Movement Path (LMP) scoped depth**

Lateral movement paths (LMPs) are a key method for threat and risk discovery in Azure ATP. To help keep focus on the critical risks to your most sensitive users, this update makes it easier and faster to analyze and remediate risks to the sensitive users on each LMP, by limiting the scope and depth of each graph displayed.

See [Lateral Movement Paths](/defender-for-identity/understand-lateral-movement-paths) to learn more about how Azure ATP uses LMPs to surface access risks to each entity in your environment.

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.71

Released March 24, 2019

- **Feature enhancement: Network Name Resolution (NNR) health alerts**

Health alerts were added for confidence levels associated with Azure ATP security alerts that are based on NNR. Each health alert includes actionable and detailed recommendations to help resolve low NNR success rates.

See [What is Network Name Resolution](nnr-policy.md) to learn more about how Azure ATP uses NNR and why it's important for alert accuracy.

- **Server support: Support added for Server 2019 with use of KB4487044**

Support added for use of Windows Server 2019, with a patch level of KB4487044. Use of Server 2019 without the patch isn't supported, and is blocked starting from this update.

- **Feature enhancement: User-based alert exclusion**

Extended alert exclusion options now allow for excluding specific users from specific alerts. Exclusions can help avoid situations where use or configuration of certain types of internal software repeatedly triggered benign security alerts.

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.70

Released March 17, 2019

- **Feature enhancement: Network Name Resolution (NNR) confidence level added to multiple alerts**  Network Name Resolution or (NNR) is used to help positively identify the source entity identity of suspected attacks. By adding the NNR confidence levels to Azure ATP alert evidence lists, you can now instantly assess and understand the level of NNR confidence related to the possible sources identified, and remediate appropriately.

NNR confidence level evidence was added to the following alerts:

- [Network mapping reconnaissance (DNS)](reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)

- [Suspected identity theft (pass-the-ticket)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)

- [Suspected NTLM relay attack (Exchange account)-preview](lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)

- [Suspected DCSync attack (replication of directory services)](domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)

- **Additional health alert scenario: Azure ATP sensor service failed to start**

In instances where the Azure ATP sensor failed to start due to a network capturing driver issue, a sensor health alert is now triggered. [Troubleshooting Azure ATP sensor with Azure ATP logs](troubleshooting-using-logs.md) for more information about Azure ATP logs and how to use them.

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.69

Released March 10, 2019

- **Feature enhancement: Suspected identity theft (pass-the-ticket) alert**   This alert now features new evidence showing the details of connections made by using remote desktop protocol (RDP). The added evidence makes it easy to remediate the known issue of (B-TP) Benign-True Positive alerts caused by use of Remote Credential Guard over RDP connections.

- **Feature enhancement: Remote code execution over DNS alert**

This alert now features new evidence showing your domain controller security update status, informing you when updates are required.

- **New documentation feature: Azure ATP Security alert MITRE ATT&CK Matrix&trade;**

To explain and make it easier to map the relationship between Azure ATP security alerts and the familiar MITRE ATT&CK Matrix, we've added the relevant MITRE techniques to Azure ATP security alert listings. This additional reference makes it easier to understand the suspected attack technique potentially in use when an Azure ATP security alert is triggered. Learn more about the [Azure ATP security alert guide](/defender-for-identity/alerts-overview).

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.68

Released March 3, 2019

- **Feature enhancement: Suspected brute force attack (LDAP) alert**

Significant usability improvements were made to this security alert including a revised description, provision of additional source information, and guess attempt details for faster remediation.

Learn more about [Suspected brute force attack (LDAP)](compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004) security alerts.

- **New documentation feature: Security alert lab**

To explain the power of Azure ATP in detecting the real threats to your working environment, we've added a new **Security alert lab** to this documentation. The **Security alert lab** helps you quickly set up a lab or testing environment, and explains the best defensive posturing against common, real-world threats and attacks.

The [step-by-step lab](/defender-for-identity/what-is) is designed to ensure you spend minimal time building, and more time learning about your threat landscape and available Azure ATP alerts and protection. We're excited to hear your feedback.

- This version also includes improvements and bug fixes for internal sensor infrastructure.

## February 2019

### Azure ATP release 2.67

Released February 24, 2019

- **New security alert: Security principal reconnaissance (LDAP) – (preview)**

Azure ATP's [Security principal reconnaissance (LDAP) - preview](reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038) security alert is now in public preview.    In this detection, an Azure ATP security alert is triggered when security principal reconnaissance is used by attackers to gain critical information about the domain environment. This information helps attackers map the domain structure, and identify privileged accounts for use in later steps in their attack kill chain.

Lightweight Directory Access Protocol (LDAP) is one the most popular methods used for both legitimate and malicious purposes to query Active Directory. LDAP focused security principal reconnaissance is commonly used as the first phase of a Kerberoasting attack. Kerberoasting attacks are used to get a target list of Security Principal Names (SPNs), which attackers then attempt to get Ticket Granting Server (TGS) tickets for.

- **Feature enhancement: Account enumeration reconnaissance (NTLM) alert**

Improved **Account enumeration reconnaissance (NTLM)** alert using additional analysis, and improved detection logic to reduce **B-TP** and **FP** alert results.

- **Feature enhancement: Network mapping reconnaissance (DNS) alert**

New types of detections added to Network mapping reconnaissance (DNS) alerts. In addition to detecting suspicious AXFR requests, Azure ATP now detects suspicious types of requests originating from non-DNS servers using an excessive number of requests.

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.66

Released February 17, 2019

- **Feature enhancement: Suspected DCSync attack (replication of directory services) alert**

Usability improvements were made to this security alert including a revised description, provision of additional source information, new infographic, and more evidence.

Learn more about [Suspected DCSync attack (replication of directory services)](domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006) security alerts.

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.65

Released February 10, 2019

- **New security alert: Suspected NTLM relay attack (Exchange account) – (preview)**

Azure ATP's [Suspected NTLM relay attack (Exchange account) - preview](lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037) security alert is now in public preview. In this detection, an Azure ATP security alert is triggered when use of Exchange account credentials from a suspicious source is identified. These types of attacks attempt to use NTLM relay techniques to gain domain controller exchange privileges and are known as **ExchangePriv**. Learn more about the **ExchangePriv** technique from the [ADV190007 advisory](https://msrc.microsoft.com/update-guide/advisory/ADV190007) first published January 31, 2019, and the [Azure ATP alert response](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/How-to-win-the-latest-security-race-over-NTLM-relay/ba-p/334511).

- **General availability: Remote code execution over DNS**

This alert is now in GA (general availability). For more information and alert features, see the [Remote code execution over DNS alert description page](lateral-movement-alerts.md#remote-code-execution-attempt-over-dns-external-id-2036).

- **General availability: Data exfiltration over SMB**

This alert is now in GA (general availability). For more information and alert features, see the [Data exfiltration over SMB alert description page](exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030).

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.64

Released February 4, 2019

- **General availability: Suspected Golden Ticket usage (ticket anomaly)**

This alert is now in GA (general availability). For more information and alert features, see the [Suspected Golden Ticket usage (ticket anomaly) alert description page](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032).

- **Feature enhancement: Network mapping reconnaissance (DNS)**

Improved alert detection logic deployed for this alert to minimize false-positives and alert noise. This alert now has a learning period of eight days before the alert will possibly trigger for the first time. For more information about this alert, see [Network mapping reconnaissance (DNS) alert description page](reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007).

**Due to the enhancement of this alert, the nslookup method should no longer be used to test Azure ATP connectivity during initial configuration.**

- **Feature enhancement:**

This version includes redesigned alert pages, and new evidence, providing better alert investigation.

- [Suspected brute force attack (SMB)](compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)

- [Suspected Golden Ticket usage (time anomaly) alert description page](domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)

- [Suspected overpass-the-hash attack (Kerberos)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)

- [Suspected use of Metasploit hacking framework](compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)

- [Suspected WannaCry ransomware attack](compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)

- This version also includes improvements and bug fixes for internal sensor infrastructure.

## January 2019

### Azure ATP release 2.63

Released January 27, 2019

- **New feature: Untrusted forest support – (preview)**

Azure ATP's support for sensors in untrusted forests is now in public preview.

From the Azure ATP portal **Directory services** page, configure additional sets of credentials to enable Azure ATP sensors to connect to different Active Directory forests, and report back to the Azure ATP service. See [Azure ATP multi-forest](deploy/multi-forest.md) to learn more.

- **New feature: Domain controller coverage**

Azure ATP now provides coverage information for Azure ATP monitored domain controllers.

From the Azure ATP portal **Sensors** page, view the number of the monitored and unmonitored domain controllers detected by Azure ATP in your environment. Download the monitored domain controller list for further analysis, and to build an action plan. See the [Domain controller monitoring](/defender-for-identity/sensor-settings) how-to guide to learn more.

- **Feature enhancement: Account enumeration reconnaissance**

The Azure ATP account enumeration reconnaissance detection now detects and issues alerts for enumeration attempts using Kerberos and NTLM. Previously, the detection only worked for attempts using Kerberos. See [Azure ATP reconnaissance alerts](reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003) to learn more.

- **Feature enhancement: Remote code execution attempt alert**

- All remote execution activities, such as service creation, WMI execution, and the new **PowerShell** execution, were added to the profile timeline of the destination machine. The destination machine is the domain controller the command was executed on.

- **PowerShell** execution was added to the list of remote code execution activities listed in the entity profile alert timeline.

- See [Remote code execution attempt](domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019) to learn more.

- **Windows Server 2019 LSASS issue and Azure ATP**

In response to customer feedback regarding Azure ATP usage with domain controllers running Windows Server 2019, this update includes additional logic to avoid triggering the reported behavior on Windows Server 2019 machines. Full support for Azure ATP sensor on Windows Server 2019 is planned for a future Azure ATP update, however installing and running Azure ATP on Windows Servers 2019 is **not** currently supported. See [Azure ATP sensor requirements](prerequisites.md#) to learn more.

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.62

Released January 20, 2019

- **New security alert: Remote code execution over DNS – (preview)**

Azure ATP's [Remote code execution over DNS](lateral-movement-alerts.md#remote-code-execution-attempt-over-dns-external-id-2036) security alert is now in public preview.    In this detection, an Azure ATP security alert is triggered when DNS queries suspected of exploiting security vulnerability [CVE-2018-8626](https://msrc.microsoft.com/update-guide/advisory/CVE-2018-8626) are made against a domain controller in the network.

- **Feature Enhancement: 72 hour delayed sensor update**

Changed option to delay sensor updates on selected sensors to 72 hours (instead of the previous 24-hour delay) after each release update of Azure ATP. See [Azure ATP sensor update](/defender-for-identity/sensor-settings) for configuration instructions.

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.61

Released January 13, 2019

- **New Security Alert: Data exfiltration over SMB - (preview)**

Azure ATP's [Data exfiltration over SMB](exfiltration-alerts.md) security alert is now in public preview. Attackers with domain admin rights can compromise the KRBTGT account. Using the KRBTGT account, attackers can create a Kerberos ticket granting ticket (TGT) that provide authorization to any resource.

- **Feature Enhancement: Remote code execution attempt** security alert

A new alert description and extra evidence were added to help make the alert easier to understand, and provide better investigation workflows.

- **Feature Enhancement: DNS query logical activities**

Additional query types were added to [Azure ATP monitored activities](monitored-activities.md) including: **TXT**, **MX**, **NS**, **SRV**, **ANY**, **DNSKEY**.

- **Feature Enhancement: Suspected Golden Ticket usage (ticket anomaly) and Suspected Golden Ticket usage (nonexistent account)**

Improved detection logic has been applied to both alerts to reduce the number of FP alerts, and deliver more accurate results.

- **Feature Enhancement: Azure ATP Security Alert documentation**

Azure ATP security alert documentation has been enhanced and expanded to include better alert descriptions, more accurate alert classifications, and explanations of evidence, remediation, and prevention. Get familiar with the new security alert documentation design using the following links:

- [Azure ATP Security Alerts](/defender-for-identity/alerts-overview)

- [Understanding security alerts](understanding-security-alerts.md)

- [Reconnaissance phase alerts](reconnaissance-alerts.md)

- [Compromised credential phase alerts](compromised-credentials-alerts.md)

- [Lateral movement phase alerts](lateral-movement-alerts.md)

- [Domain dominance phase alerts](domain-dominance-alerts.md)

- [Exfiltration phase alerts](exfiltration-alerts.md)

- [Investigate a computer](/defender-for-identity/investigate-assets)

- [Investigate a user](/defender-for-identity/investigate-assets)

- This version also includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.60

Released January 6, 2019

- This version includes improvements and bug fixes for internal sensor infrastructure.

## December 2018

### Azure ATP release 2.59

Released December 16, 2018

- This version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.58

Released December 9, 2018

- **Security Alert Enhancement: Unusual Protocol Implementation alert split**

Azure ATP's series of Unusual Protocol Implementation security alerts that previously shared 1 externalId (2002), are now split into four distinctive alerts, with a corresponding unique external ID.

#### New alert externalIds

> |New security alert name|Previous security alert name|Unique external ID|

> |---------|----------|---------|

> |Suspected brute force attack (SMB)|Unusual protocol implementation (potential use of malicious tools such as Hydra)|2033

> |Suspected overpass-the-hash attack (Kerberos)|Unusual Kerberos protocol implementation (potential overpass-the-hash attack)|2002|

> |Suspected use of Metasploit hacking framework|Unusual protocol implementation (potential use of Metasploit hacking tools)|2034

> |Suspected WannaCry ransomware attack|Unusual protocol implementation (potential WannaCry ransomware attack)|2035

> |

- **New monitored activity: File copy through SMB**

Copying of files using SMB is now a monitored and filterable activity. Learn more about which [activities Azure ATP monitors](monitored-activities.md), and how to [filter and search monitored activities](/defender-for-identity/monitored-activities) in the portal.

- **Large Lateral Movement Path image enhancement**

When viewing large lateral movement paths, Azure ATP now highlights only the nodes connected to a selected entity,  instead of blurring the other nodes. This change introduces a significant improvement in large LMP rendering speed.

- This version includes improvements and bug fixes for internal sensor infrastructure.

### Azure ATP release 2.57

Released December 2, 2018

- **New Security Alert: Suspected Golden ticket usage- ticket anomaly (preview)**

Azure ATP's [Suspected Golden Ticket usage - ticket anomaly](/defender-for-identity/alerts-overview) security alert is now in public preview.    Attackers with domain admin rights can compromise the KRBTGT account. Using the KRBTGT account, attackers can create a Kerberos ticket granting ticket (TGT) that provides authorization to any resource.

This forged TGT is called a "Golden Ticket" because it allows attackers to achieve lasting network persistence. Forged Golden Tickets of this type have unique characteristics this new detection is designed to identify.

- **Feature Enhancement: Automated Azure ATP instance (instance) creation**

From today, Azure ATP *instances* are renamed Azure ATP *instances*. Azure ATP now supports one Azure ATP instance per Azure ATP account. Instances for new customers are created using the instance creation wizard in the [Azure ATP portal](https://portal.atp.azure.com). Existing Azure ATP instances are converted automatically to Azure ATP instances with this update.

- Simplified instance creation for faster deployment and protection using [create your Azure ATP instance](/defender-for-identity/deploy-defender-identity).

- All [data privacy and compliance](privacy-compliance.md) remains the same.

To learn more about Azure ATP instances, see [Create your Azure ATP instance](/defender-for-identity/deploy-defender-identity).

- This version includes improvements and bug fixes for internal sensor infrastructure.

## November 2018

### Azure ATP release 2.56

Released November 25, 2018

- **Feature Enhancement: Lateral Movement Paths (LMPs)**

Two additional features are added to enhance Azure ATP Lateral Movement Path (LMP) capabilities:

- LMP history is now saved and discoverable per entity, and when using LMP reports.

- Follow an entity in an LMP via the activity timeline, and investigate using additional evidence provided for discovery of potential attack paths.

See [Azure ATP Lateral Movement Paths](/defender-for-identity/understand-lateral-movement-paths) to learn more about how to use and investigate with enhanced LMPs.

- **Documentation enhancements: Lateral Movement Paths and Security Alert names**

Additions and updates were made to Azure ATP articles describing Lateral Movement Path descriptions and features, name mapping was added for all instances of old security alert names to new names and externalIds.

- See [Azure ATP Lateral Movement Paths](/defender-for-identity/understand-lateral-movement-paths), [Investigate  Lateral Movement Paths](/defender-for-identity/understand-lateral-movement-paths), and [Security Alert Guide](/defender-for-identity/alerts-overview) to learn more.

- This version includes improvements and bug fixes for internal sensor infrastructure.

For details of each Defender for Identity release before (and including) release 2.55, see the [Defender for Identity release reference](/defender-for-identity/whats-new).

## Next steps

> [!div class="nextstepaction"]

> [What's new in Microsoft Defender for Identity](whats-new.md)


# Migrate From Ata Overview

# Advanced Threat Analytics (ATA) to Microsoft Defender for Identity

This article describes how to migrate from an existing ATA installation to a Microsoft Defender for Identity sensor, and includes the following steps:

> [!div class="checklist"]

>

> - Review and confirm Defender for Identity service prerequisites

> - Document your existing ATA configuration

> - Plan your migration

> - Set up and configure your Defender for Identity service

> - Perform post-migration checks and verifications

> - Decommission ATA

ATA is a standalone on-premises solution with multiple components, such as the ATA Center that requires dedicated hardware on-premises.

Defender for Identity is a cloud-based security solution that uses your on-premises Active Directory signals. The solution is highly scalable and is frequently updated.

In contrast to the ATA sensor, the Defender for Identity sensor also uses data sources such as Event Tracing for Windows (ETW) enabling Defender for Identity to deliver extra detections. Defender for Identity also provides:

- Support for [multi-forest environments](deploy/multi-forest.md)

- [Microsoft Secure Score posture assessments](/defender-for-identity/security-assessment)

- Direct integrations with other services like Microsoft Defender for Cloud Apps and Microsoft Entra for a hybrid view of what's taking place in both on-premises and hybrid environments

- And more

Defender for Identity also uses the Microsoft 365 security portfolio to automatically analyze cross-domain threat data, building a complete picture of each attack in a single dashboard.

> [!IMPORTANT]

> This migration guide is designed for Defender for Identity sensors only, and not standalone sensors.

>

> While you can migrate to Defender for Identity from any ATA version, your ATA data isn't migrated. Therefore, we recommend that you plan to retain your ATA Data Center and any alerts required for ongoing investigations until all ATA alerts are closed or remediated.

>

> [!NOTE]

> The final release of ATA is [generally available](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9). ATA ended Mainstream Support on January 12, 2021. Extended Support will continue until January 2026. For more information, read [our blog](https://techcommunity.microsoft.com/t5/microsoft-security-and/end-of-mainstream-support-for-advanced-threat-analytics-january/ba-p/1539181).

## Prerequisites

To migrate from ATA to Defender for Identity, you must have an environment and domain controllers that meet Defender for Identity sensor requirements. For more information, see [Microsoft Defender for Identity prerequisites](prerequisites.md).

Make sure that all the domain controllers you plan to use have sufficient internet access to the Defender for Identity service. For more information, see [Configure endpoint proxy and internet connectivity settings](configure-proxy.md).

## Plan your migration

Before starting the migration, gather all of the following information:

- **Account details for your [Directory Services](directory-service-accounts.md) account**.

- **Syslog notification [settings](/defender-for-identity/notifications)**.

- **Email [notification details](notifications.md)**.

- **All [ATA role group memberships](/advanced-threat-analytics/ata-role-groups)**.

- **[VPN integration details](vpn-integration.md)**.

- **Alert exclusions**. Exclusions are not transferable from ATA to Defender for Identity, so details of each exclusion are required to [replicate the exclusions as Defender for Identity](exclusions.md) in Microsoft Defender XDR.

- **Account details for entity tags**. If you don't already have dedicated entity tags, create new ones for use with Defender for Identity. For more information, see [Defender for Identity entity tags in Microsoft Defender XDR](entity-tags.md).

- **A complete list of all entities, such as computers, groups, or users, that you want to manually tag as *Sensitive* entities**. For more information, see [Defender for Identity entity tags in Microsoft Defender XDR](entity-tags.md).

- **Report scheduling [details](/defender-for-identity/classic-reports)**, including a list of all reports and scheduled timing.

> [!CAUTION]

> Do not uninstall the ATA Center until all ATA Gateways are removed. Uninstalling the ATA Center with ATA Gateways still running leaves your organization exposed with no threat protection.

## Move to Defender for Identity

Use the following steps to migrate to Defender for Identity:

1. [Create your new Defender for Identity workspace](deploy-defender-identity.md#start-using-microsoft-defender-xdr).

1. Uninstall the ATA Lightweight Gateway on all domain controllers.

1. Install the Defender for Identity Sensor on all domain controllers:

1. [Download and install the Defender for Identity sensor](deploy/install-sensor.md) on your domain controllers.

1. [Configure the your Defender for Identity sensor](configure-sensor-settings.md).

After the migration is complete, allow two hours for the initial sync to be completed before moving on with validation tasks.

## Validate your migration

In Microsoft Defender XDR, check the following areas to validate your migration:

- Review any [health issues](health-alerts.md) for signs of service issues.

- Review Defender for Identity [sensor error logs](troubleshooting-using-logs.md) for any unusual errors.

## Post-migration activities

After completing your migration to Defender for Identity, do the following to clean up your legacy ATA resources:

1. Make sure that you've recorded or remediated all existing ATA alerts. Existing ATA security alerts aren't imported to Defender for Identity with the migration.

1. Do one or both of the following:

- **Decommission the ATA Center**. We recommend keeping ATA data online for a period of time.

- **Back up Mongo DB** if you want to keep the ATA data indefinitely. For more information, see [Backing up the ATA database](/advanced-threat-analytics/ata-database-management#backing-up-the-ata-database).

## Related information

After migrating to Defender for Identity, learn more about investigating alerts in Microsoft Defender XDR. For more information, see:

- [Understanding security alerts](understanding-security-alerts.md)

- [Investigate Defender for Identity security alerts in Microsoft Defender XDR](manage-security-alerts.md)


# Licenses

- Enterprise Mobility + Security E5 (EMS E5/A5)

- Microsoft 365 E5 (Microsoft E5/A5/G5)

- Microsoft 365 E5/A5/G5/F5[*](#req) Security

- Microsoft 365 F5 Security + Compliance[*](#req)

- A standalone Defender for Identity license

<a name=req></a>* Both F5 licenses require Microsoft 365 F1/F3 or Office 365 F3 and Enterprise Mobility + Security E3.

Acquire licenses directly via the [Microsoft 365 portal](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) or use the Cloud Solution Partner (CSP) licensing model.


# Server Requirements

Defender for Identity sensors can be installed on the following operating systems:

- **Windows Server 2016**

- **Windows Server 2019**. Requires [KB4487044](https://support.microsoft.com/topic/february-12-2019-kb4487044-os-build-17763-316-6502eb5d-dde8-6902-e149-27ef359ed616) or a newer cumulative update. Sensors installed on Server 2019 without this update will be automatically stopped if the `ntdsai.dll` file version found in the system directory is older `than 10.0.17763.316`

- **Windows Server 2022**

- **Windows Server 2025**

For all operating systems:

- Both servers with desktop experience and server cores are supported.

- Nano servers aren't supported.

- Installations are supported for domain controllers, AD FS, AD CS, and Entra Connect servers.


# Dsa Permissions

The DSA requires read only permissions on **all** the objects in Active Directory, including the **Deleted Objects Container**.

The read-only permissions on the **Deleted Objects** container allows Defender for Identity to detect user deletions from your Active Directory.

Use the following code sample to help you grant the required read permissions on the **Deleted Objects** container, whether or not you're using a gMSA account.

> [!TIP]

> If the DSA you want to grant the permissions to is a Group Managed Service Account (gMSA), you must first create a security group, add the gMSA as a member, and add the permissions to that group. For more information, see [Configure a Directory Service Account for Defender for Identity with a gMSA](../deploy/create-directory-service-account-gmsa.md).

>

```powershell

# Declare the identity that you want to add read access to the deleted objects container:

$Identity = 'mdiSvc01'

# If the identity is a gMSA, first to create a group and add the gMSA to it:

$groupName = 'mdiUsr01Group'

$groupDescription = 'Members of this group are allowed to read the objects in the Deleted Objects container in AD'

if(Get-ADServiceAccount -Identity $Identity -ErrorAction SilentlyContinue) {

$groupParams = @{

Name           = $groupName

SamAccountName = $groupName

DisplayName    = $groupName

GroupCategory  = 'Security'

GroupScope     = 'Universal'

Description    = $groupDescription

}

$group = New-ADGroup @groupParams -PassThru

Add-ADGroupMember -Identity $group -Members ('{0}$' -f $Identity)

$Identity = $group.Name

}

# Get the deleted objects container's distinguished name:

$distinguishedName = ([adsi]'').distinguishedName.Value

$deletedObjectsDN = 'CN=Deleted Objects,{0}' -f $distinguishedName

# Take ownership on the deleted objects container:

$params = @("$deletedObjectsDN", '/takeOwnership')

C:\Windows\System32\dsacls.exe $params

# Grant the 'List Contents' and 'Read Property' permissions to the user or group:

$params = @("$deletedObjectsDN", '/G', ('{0}\{1}:LCRP' -f ([adsi]'').name.Value, $Identity))

C:\Windows\System32\dsacls.exe $params

# To remove the permissions, uncomment the next 2 lines and run them instead of the two prior ones:

# $params = @("$deletedObjectsDN", '/R', ('{0}\{1}' -f ([adsi]'').name.Value, $Identity))

# C:\Windows\System32\dsacls.exe $params

```

For more information, see [Changing permissions on a deleted object container](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816824(v=ws.10)).


# Security Assessment Deploy Defender For Identity

# Security assessment: Start your Defender for Identity deployment

This article describes the **Start your Defender for Identity deployment** security assessment, which encourages you to install sensors on domain controllers and other eligible servers.

## Why is not having Defender for Identity deployed considered a risk?

If you've obtained a Defender for Identity license, but haven't yet deployed Defender for Identity sensors, not only are you not yet using your purchased services, but you may be missing advanced threats in your identity infrastructure.

Defender for Identity uses your on-premises Active Directory signals to identify, detect, and investigate advanced threats, compromised identities, and malicious insider actions directed at your organization.

Defender for Identity is also part of monitoring for Zero Trust. You may also want to use [advanced hunting queries in Microsoft Defender XDR](/microsoft-365/security/defender/advanced-hunting-overview) to look for threats across identities, devices, and cloud apps.

For more information, see:

- [What is Microsoft Defender for Identity?](what-is.md)

- [Zero Trust with Defender for Identity](zero-trust.md)

## How do I use this security assessment?

1. Review the recommended action at <https://security.microsoft.com/securescore?viewid=actions> to be alerted if you have a Defender for Identity license, but don't have Defender for Identity deployed.

1. Take appropriate action by deploying Defender for Identity. For more information, see [Deploy Microsoft Defender for Identity with Microsoft Defender XDR](deploy-defender-identity.md).

> [!NOTE]

> While assessments are updated in near real time, scores and statuses are updated every 24 hours.  While the list of impacted entities is updated within a few minutes of your implementing the recommendations, the status may still take time until it's marked as **Completed**.

>

## See also

- [Learn more about Microsoft Secure Score](/microsoft-365/security/defender/microsoft-secure-score)

- [Check out the Defender for Identity forum!](<https://aka.ms/MDIcommunity>)
