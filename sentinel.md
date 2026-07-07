# Overview Unified Security

# What are unified security operations in the Microsoft Defender portal?

The Microsoft Defender portal provides unified security operations that integrate solutions for:

- Security information and event management (SIEM)

- Security orchestration, automation, and response (SOAR)

- Extended detection and response (XDR)

- Posture and exposure management

- Cloud security, threat intelligence, and generative AI

To cover all those capabilities, the Defender portal combines services like [Microsoft Defender XDR](/defender-xdr/microsoft-365-defender), [Microsoft Sentinel](/azure/sentinel/overview), [Microsoft Security Exposure Management](/security-exposure-management/microsoft-security-exposure-management), and [Microsoft Security Copilot](/copilot/security/microsoft-security-copilot) in the Microsoft Defender portal. Integrate more Microsoft Defender services to add security and provide integrated protection against sophisticated attacks. The Defender portal provides a single location to monitor, detect, investigate, remediate, and respond against pre- and post-breach cybersecurity risks and threats.

## Protect assets

Protect a wide range of assets by integrating Defender XDR, Microsoft Sentinel, and other Defender services in the Defender portal.

Microsoft Defender XDR services include the following asset protection capabilities:

|Capability  |Security product  |

|---------|---------|

|Identify, detect, and investigate Microsoft Entra ID threats.|[Microsoft Defender for Identity](/defender-for-identity/what-is)|

|Protect against threats posed by email messages, URL links, and Office 365 collaboration tools.     |   [Microsoft Defender for Office 365](/defender-office-365/mdo-about)      |

|Monitor and protect endpoint devices. Monitor, detect, and investigate device breaches, and automatically respond to security threats.    |     [Microsoft Defender for Endpoint](/defender-endpoint/microsoft-defender-endpoint)    |

|Identify and protect operational technology (OT) and IT resources by extending Defender XDR protection to OT environments.|[Microsoft Defender for IoT](/defender-for-iot/microsoft-defender-iot)|

|Identify assets and software inventory, and assess device posture to find security vulnerabilities.|[Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management)|

|Protect and control access to SaaS cloud apps.|[Microsoft Defender for Cloud Apps](/defender-cloud-apps/what-is-defender-for-cloud-apps)|

Asset protection for services not licensed with Microsoft Defender XDR includes the following capabilities:

|Capability  |Security product  |

|---------|---------|

|Monitor and protect non-Microsoft and on-premises devices, services, and solutions. | [Microsoft Sentinel](/azure/sentinel/overview) |

|Discover and assess assets, and remediate risk to reduce attack surfaces.|[Microsoft Security Exposure Management](/security-exposure-management/microsoft-security-exposure-management)|

|Improve multicloud and on-premises security posture, and protect cloud workloads against threats.|[Microsoft Defender for Cloud](/azure/defender-for-cloud/defender-for-cloud-introduction)|

## Simplify security management

Combine Microsoft security services like [Defender XDR](/defender-xdr/microsoft-365-defender), [Microsoft Sentinel](/azure/sentinel/overview), and more for end-to-end pre- and post-breach protection of endpoints, identities, cloud apps and workloads, and email across your organization.

The Defender portal provides a single, centralized view of organizational security posture and threat detections and response. It provides a combined incidents queue that groups together information about security risks and breaches.

Free up analyst time as unified security dashboards enable analysts to cross organization silos, prioritize the most critical threats, and hunt effectively for attempted breaches.

The following image shows the unified incident queue in the Defender portal, with incidents from multiple service sources.

## Reduce security risk and prevent attacks

Consistently reduce security risk and prevent cybersecurity attacks as a part of your organizational risk management framework. The Defender portal offers comprehensive exposure management and cloud protection capabilities with [Microsoft Security Exposure Management](/security-exposure-management/microsoft-security-exposure-management), and [Microsoft Defender for Cloud](/azure/defender-for-cloud/defender-for-cloud-introduction), as follows:

- Continuously discover organizational assets and assess their security posture.

- Protect cloud workloads from code to runtime.

- Aggregate data and threat intelligence to discover security gaps and weaknesses, including analysis of potential attack paths.

- Investigate and query to get insights into security posture.

- Prioritize asset remediation, with the focus on critical resources, to reduce security gaps and attack surfaces.

The following image shows the overview page for exposure management in the Defender portal:

## Reduce threat detection and response times

Standard cybersecurity metrics focus on the time to detect (TTD) and time to respond (TTR). Time to detect (TTD) measures how long it takes security teams to discover an incident. Time to respond (TTR) measures the amount of time it takes to respond after a threat is detected. The shorter the TTD and TTR, the more effective your detection, and response strategy is.

The Microsoft Defender portal correlates millions of signals from Defender products, Microsoft Sentinel, Microsoft security research, and threat intelligence to identify attacks in progress. It initiates automatic attack disruption to automatically contain attacks, limiting lateral movement early and reducing attack impact. Automatic attack disruption helps to reduce costs associated with loss of productivity, provide control to the SecOps team control to investigate and remediate compromised assets.

Automatic attack disruption responds to threats by containing devices and containing or disabling users to mitigate attacks.

The following image shows an example of an incident where automatic attack disruption was triggered.

For more information, see [Automatic attack disruption in Microsoft Defender XDR](/defender-xdr/automatic-attack-disruption).

## Transform SOC productivity with AI

Microsoft Security Copilot brings together the power of AI and human expertise to help your SOC team respond to attacks faster and more effectively. Security Copilot is embedded in the Defender portal to enable security teams to efficiently summarize incidents, analyze scripts and codes, analyze files, summarize device information, use guided responses to resolve incidents, generate KQL queries, and create incident reports. Security Copilot helps you to:

- **Reduce exposure and improve posture**. Prevent breaches with insights to uncover critical exposure risk, and risk reduction recommendations.

- **Prevent and disrupt threats**. Identify and prioritize with incident summaries MITRE ATT&CK framework mapping, and automatic alert enrichment.

- **Empower analysts**:

- Accelerate incident resolution with guided responses, automated remediation, and summary report generation.

- Provide intelligent assistance with tailored prompts based on best practices that analyze malicious scripts and files, and suggest KQL queries.

The following image shows the integration of Microsoft Copilot in an incident page in the Defender portal.

For more information, see [Microsoft Copilot in Microsoft Defender](/defender-xdr/security-copilot-in-microsoft-365-defender).

## Related content

- Blog post: [AI-powered, unified security operations](https://www.microsoft.com/security/business/solutions/ai-powered-unified-secops-platform)

- [Planning guidance for unified security operations in the Microsoft Defender portal](overview-plan.md)

- [Deploy for unified security operations](overview-deploy.md)


# Whats New

# What's new for Microsoft unified security operations

This article lists recent features added for unified security operations in the Microsoft Defender portal.

## February 2026

### New content types for cross-tenant distribution now generally available

The following content types are now generally available for [distribution across multiple tenants](./mto-distribution-profiles.md) in the Microsoft Defender multitenant portal:

- Analytics rules

- Automation rules

- Workbooks

## January 2026

### Updated date: Microsoft Sentinel in the Azure portal to be retired March 2027

Microsoft Sentinel is [generally available in the Microsoft Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal), including for customers without Microsoft Defender XDR or an E5 license. This means that you can use Microsoft Sentinel in the Defender portal even if you aren't using other Microsoft Defender services.

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal.

If you're currently using Microsoft Sentinel in the Azure portal, we recommend that you start planning your transition to the Defender portal now to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/unified-secops-platform/overview-unified-security).

For more information, see:

- [Microsoft Sentinel in the Microsoft Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal)

- [Transition your Microsoft Sentinel environment to the Defender portal](/azure/sentinel/move-to-defender)

- [Planning your move to Microsoft Defender portal for all Microsoft Sentinel customers](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613) (blog)

## November 2025

### Microsoft Threat Intelligence alert enhancements for Microsoft Sentinel customers in the Defender portal

Microsoft Sentinel customers using the Defender portal, or the Azure portal with the Microsoft Sentinel Defender XDR data connector, now also benefit from Microsoft Threat Intelligence alerts that highlight activity from nation-state actors, major ransomware campaigns, and fraudulent operations. To view these alert types, you must have the **Security Administrator** or **Global Administrator** role. The **Service Source**, **Detection Source**, and **Product Name** values for these alerts are listed as *Microsoft Threat Intelligence*.

For more information, see [Incidents and alerts in the Microsoft Defender portal](/defender-xdr/incidents-overview).

### New Entity Behavior Analytics (UEBA) experiences in the Defender portal (Preview)

Microsoft Sentinel introduces new UEBA experiences in the Defender portal, bringing behavioral insights directly into key analyst workflows. These enhancements help analysts prioritize investigations and apply UEBA context more effectively.

#### Anomaly-focused user investigations

In the Defender portal, users with behavioral anomalies are automatically tagged with **UEBA Anomalies**, helping analysts quickly identify which users to prioritize.

Analysts can view the top three anomalies from the past 30 days in a dedicated Top UEBA anomalies section, available in:

- User side panels accessible from various portal locations.

- The **Overview** tab of user entity pages.

This section also includes direct links to anomaly queries and the Sentinel events timeline, enabling deeper investigation and faster context gathering.

#### Drilldown to user anomalies from incident graphs

Analysts can quickly access all anomalies related to a user by selecting **Go Hunt > All user anomalies** from the incident graph. This built-in query provides immediate UEBA context to support deeper investigation.

#### Enriched advanced hunting and custom detections queries with behavior insights

Advanced hunting and custom detection experiences now include a contextual banner that prompts analysts to join the UEBA Anomalies table to queries that include UEBA data sources.

All features require UEBA to be enabled and are workspace-scoped to the currently selected workspace.

For more information, see [UEBA experiences in the Defender portal empower analysts and streamline workflows](/azure/sentinel/identify-threats-with-entity-behavior-analytics#ueba-experiences-in-the-defender-portal-empower-analysts-and-streamline-workflows).

## September 2025

### Manage Incident Workflows with Tasks in Microsoft Defender (Preview)

You can now use tasks in the Microsoft Defender portal to break down incident investigations into actionable steps and assign them across your operations teams. Tasks are displayed alongside Security Copilot insights, guided responses, and reports - giving your team a unified view of progress and next steps. When you onboard Microsoft Sentinel to the Defender portal, tasks you create in Microsoft Sentinel through the Azure portal are automatically synchronized to the Defender portal. For more information, see [Streamline incident response using tasks in the Microsoft Defender portal (Preview)](/defender-xdr/split-incidents-into-tasks?toc=/unified-secops-platform/toc.json&bc=/unified-secops-platform/breadcrumb/toc.json).

## August 2025

- [Viewing unified RBAC in multitenant management to GA](#viewing-unified-rbac-in-multitenant-management-to-ga)

- [Tenant groups in multitenant management renamed to distribution profiles](#tenant-groups-in-multitenant-management-renamed-to-distribution-profiles)

- [Distribute Microsoft Defender for Endpoint security policies with multitenant management](#distribute-microsoft-defender-for-endpoint-security-policies-with-multitenant-management)

### Edit workbooks directly in the Microsoft Defender portal

Now you can create and edit Microsoft Sentinel workbooks directly in the Microsoft Defender portal. This enhancement streamlines your workflow and allows you to manage your workbooks more efficiently and brings the workbook experience more closely aligned with the experience in the Azure portal.

Microsoft Sentinel workbooks are based on Azure Monitor workbooks, and help you visualize and monitor the data ingested to Microsoft Sentinel. Workbooks add tables and charts with analytics for your logs and queries to the tools already available.

Workbooks are available in the Defender portal under **Microsoft Sentinel > Threat management > Workbooks**. For more information, see [Visualize and monitor your data by using workbooks in Microsoft Sentinel](/azure/sentinel/monitor-your-data).

### Viewing unified RBAC in multitenant management to GA

Viewing unified role-based access control (RBAC) in the Microsoft Defender multitenant management portal is now generally available. This feature allows you to view a comprehensive view of permissions and access for your tenants.

Creating and editing custom roles remains in preview. For more information, see [Manage unified role-based access control in multitenant management](mto-urbac.md).

### Tenant groups in multitenant management renamed to distribution profiles

In the multitenant portal, tenant groups are now renamed to **content distribution profiles**.

Functionality remains the same: Content distribution profiles enable you to distribute security content, including custom detection rules and endpoint security policies, at scale across all of your tenants, based on categories like business groups or location. For example:

For more information, see [Content distribution using distribution profiles in multitenant management](mto-distribution-profiles.md).

### Distribute Microsoft Defender for Endpoint security policies with multitenant management

Microsoft Defender for Endpoint security policies can now be distributed as content across multiple tenants using the Defender multitenant portal, empowering security teams to manage endpoint security policies at scale. Distributed policies are shown in the **Configuration management > Endpoint security policies** page in a hierarchical view so that you can identify parent policies and their distributed copies across tenants.

The original policy’s page also shows the overall distribution status and lists recipient tenants and distribution profiles.

For more information, see [Endpoint security policies in multitenant management](mto-endpoint-security-policy.md) and [Content distribution in multitenant management](mto-distribution-profiles.md).

## July 2025

- [For new customers only: Automatic onboarding and redirection to the Microsoft Defender portal](#for-new-customers-only-automatic-onboarding-and-redirection-to-the-microsoft-defender-portal)

- [No limit on the number of workspaces you can onboard to the Defender portal](#no-limit-on-the-number-of-workspaces-you-can-onboard-to-the-defender-portal)

- [Microsoft Sentinel in the Azure portal to be retired July 2026](#microsoft-sentinel-in-the-azure-portal-to-be-retired-july-2026)

### For new customers only: Automatic onboarding and redirection to the Microsoft Defender portal

For this update, new Microsoft Sentinel customers are customers who are [onboarding the first workspace in their tenant to Microsoft Sentinel](/azure/sentinel/quickstart-onboard) after **July 1, 2025**.

Starting on **July 1 2025**, such new customers who are also:

- not Azure Lighthouse-delegated users and

- who have the permissions of a subscription [Owner](/azure/role-based-access-control/built-in-roles#owner) or a [User access administrator](/azure/role-based-access-control/built-in-roles#user-access-administrator)

Have their workspaces automatically onboarded to the Defender portal together with onboarding to Microsoft Sentinel. Users of such workspaces, who also aren't Azure Lighthouse-delegated users, see links in Microsoft Sentinel in the Azure portal that redirect them to the Defender portal.

For example:

Such users use Microsoft Sentinel in the Defender portal only.

New customers who don't have relevant permissions aren't automatically onboarded to the Defender portal, but they do still see redirection links in the Azure portal, together with prompts to have a user with relevant permissions manually onboard the workspace to the Defender portal.

This change streamlines the onboarding process and ensures that new customers can immediately take advantage of unified security operations capabilities without the extra step of manually onboarding their workspaces.

For more information, see:

- [Onboard Microsoft Sentinel](/azure/sentinel/quickstart-onboard)

- [Microsoft Sentinel in the Microsoft Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal)

- [Changes for new customers](https://aka.ms/changes-for-sentinel-customers-july-25)

### No limit on the number of workspaces you can onboard to the Defender portal

There is no longer any limit to the number of workspaces you can onboard to the Defender portal.

Limitations still apply to the number of workspaces you can include in a Log Analytics query, and in the number of workspaces you can or should include in a scheduled analytics rule.

For more information, see:

- [Connect Microsoft Sentinel to the Microsoft Defender portal](microsoft-sentinel-onboard.md)

- [Multiple Microsoft Sentinel workspaces in the Defender portal](/azure/sentinel/workspaces-defender-portal)

- [Extend Microsoft Sentinel across workspaces and tenants](/azure/sentinel/extend-sentinel-across-workspaces-tenants)

### Microsoft Sentinel in the Azure portal to be retired July 2026

Microsoft Sentinel is [generally available in the Microsoft Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal), including for customers without Microsoft Defender XDR or an E5 license. This means that you can use Microsoft Sentinel in the Defender portal even if you aren't using other Microsoft Defender services.

Starting in **July 2026**, Microsoft Sentinel will be supported in the Defender portal only, and any remaining customers using the Azure portal will be automatically redirected.

> [!NOTE]

> This date has been extended. Microsoft Sentinel in the Azure portal will be retired **March 31, 2027**.

If you're currently using Microsoft Sentinel in the Azure portal, we recommend that you start planning your transition to the Defender portal now to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/unified-secops-platform/overview-unified-security).

For more information, see:

- [Microsoft Sentinel in the Microsoft Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal)

- [Transition your Microsoft Sentinel environment to the Defender portal](/azure/sentinel/move-to-defender)

- [Planning your move to Microsoft Defender portal for all Microsoft Sentinel customers](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613) (blog)

## June 2025

### Case management now generally available in the Defender multitenant portal

The Microsoft Defender portal's case management feature is now generally available in the Defender multitenant portal. For more information, see [View and manage cases across multiple tenants in the Microsoft Defender multitenant portal](mto-manage-cases.md).

## May 2025

- [Unified role-based access control in multitenant portal (Preview)](#unified-role-based-access-control-in-multitenant-management-preview)

- [All Microsoft Sentinel use cases generally available in the Defender portal](#all-microsoft-sentinel-use-cases-generally-available-in-the-defender-portal)

- [Case management now available for the Defender multitenant portal (Preview)](#case-management-now-available-for-the-defender-multitenant-portal-preview)

### Unified role-based access control in multitenant management (Preview)

Unified role-based access control (URBAC) is now available in the Microsoft Defender multitenant management portal. You can create, delete, import, and edit roles in the multitenant management portal. This capability provides a comprehensive view of permissions and access for your tenants, and a centralized administration to manage these permissions.

For more information, see [Manage unified role-based access control in multitenant management](mto-urbac.md).

### All Microsoft Sentinel use cases generally available in the Defender portal

All Microsoft Sentinel use cases that are in general availability, including [multi-tenant](mto-overview.md) and [multi-workspace](/azure/sentinel/workspaces-defender-portal) capabilities and support for all government and commercial clouds, are now also supported for general availability in the Defender portal.

We recommend that you [onboard your workspaces to the Defender portal](microsoft-sentinel-onboard.md) to take advantage of a single location for all your security operations. For more information, see:

- [The Best of Microsoft Sentinel - now in Microsoft Defender](https://techcommunity.microsoft.com/blog/MicrosoftThreatProtectionBlog/the-best-of-microsoft-sentinel-%E2%80%94-now-in-microsoft-defender/4415822) (blog)

- [Transition your Microsoft Sentinel environment to the Defender portal](/azure/sentinel/move-to-defender?toc=%2Funified-secops-platform%2Ftoc.json&bc=%2Funified-secops-platform%2Fbreadcrumb%2Ftoc.json)

- [Microsoft Sentinel in the Microsoft Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal)

### Case management now available for the Defender multitenant portal (Preview)

SecOps teams for large organizations and managed security service providers (MSSPs) must manage cases across multiple tenants. This can now be done without leaving the Defender multitenant portal.

For more information, see [View and manage cases across multiple tenants in the Microsoft Defender multitenant portal](mto-manage-cases.md).

## April 2025

- [Merge incidents manually (Preview)](#merge-incidents-manually-preview)

- [Multi workspace and multi tenant support for Microsoft Sentinel (Preview)](#multi-workspace-and-multi-tenant-support-for-microsoft-sentinel-preview)

- [Case management now generally available](#case-management-now-generally-available)

### Merge incidents manually (Preview)

If two incidents should be merged because they describe the same attack story, but aren't merged for any of the reasons listed in ["When incidents aren't merged"](/defender-xdr/alerts-incidents-correlation#when-incidents-arent-merged), you can now merge the incidents manually after you fix the underlying reasons.

For example, if the incidents weren't merged because they were assigned to two different people, you can remove the assignment of one of the incidents and then merge the incidents manually.

To understand more about merging incidents, see [Alert correlation and incident merging in the Microsoft Defender portal](/defender-xdr/alerts-incidents-correlation).

For instructions on merging incidents manually, see [Merge incidents manually in the Microsoft Defender portal](/defender-xdr/merge-incidents-manually).

### Multi workspace and multi tenant support for Microsoft Sentinel (Preview)

Microsoft Sentinel now supports multiple workspaces in the Defender portal, using one primary workspace per tenant and multiple secondary workspaces.

A primary workspace's alerts are correlated with Defender XDR data, which results in incidents that include alerts from Microsoft Sentinel's primary workspace and Defender XDR. All other onboarded workspaces are considered secondary workspaces. Incidents are created based on the workspace’s data and won't include Defender XDR data.

If you're working with multiple tenants and multiple workspaces per tenant, you can also use Microsoft Defender multitenant management to view incidents and alerts, and to hunt for data in Advanced hunting, across both multiple workspaces and tenants.

For more information, see:

- [Multiple Microsoft Sentinel workspaces in the Defender portal](/azure/sentinel/workspaces-defender-portal)

- [Connect Microsoft Sentinel to the Microsoft Defender portal](microsoft-sentinel-onboard.md)

- [Microsoft Defender multitenant management](mto-overview.md)

- [View and manage incidents and alerts in Microsoft Defender multitenant management](mto-incidents-alerts.md)

- [Advanced hunting in Microsoft Defender multitenant management](mto-advanced-hunting.md)

### Cross-cloud multitenant management (Preview)

Multitenant management in Microsoft Defender now supports managing tenants in other Microsoft cloud environments. Security operations teams operating in government cloud environments can now manage their entire security operations, including tenants in other Microsoft cloud environments, in a single pane of glass. For more information, see [Manage tenants in other Microsoft cloud environments](mto-cross-cloud.md).

### Case management now generally available

The Microsoft Defender portal's case management feature is now generally available. For more information, see [Manage security operations cases natively in the Microsoft Defender portal](cases-overview.md).

## January 2025

- [Unified threat intelligence](#unified-threat-intelligence)

- [Manage SecOps work natively with case management (Preview)](#case-management-preview)

- [Unified device timeline in Microsoft Defender portal (Preview)](#unified-device-timeline-in-microsoft-defender-portal-preview)

- [SOC optimization updates for unified coverage management](#soc-optimization-updates-for-unified-coverage-management)

### Unified threat intelligence

Microsoft Sentinel-powered threat intelligence has moved in the Defender portal to **Intel management**, unifying threat intelligence features. In the Azure portal, the location remains unchanged.

Along with the new location, the management interface streamlines the creation and curation of threat intel with these key features:

- Define relationships as you create new STIX objects.

- Curate existing threat intelligence with the new relationship builder.

- Create multiple objects quickly by copying common metadata from a new or existing TI object with the duplicate feature.

- Use advanced search to sort and filter your threat intelligence objects without even writing a Log Analytics query.

For more information, see the following articles:

- [Uncover adversaries with threat intelligence across the Defender portal](threat-intelligence-overview.md)

- [New STIX objects in Microsoft Sentinel](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/announcing-public-preview-new-stix-objects-in-microsoft-sentinel/4369164)

- [Understand threat intelligence](/azure/sentinel/understand-threat-intelligence#create-and-manage-threat-intelligence)

### Case management (Preview)

Case management is the first installment of an end-to-end solution that provides seamless management of your security work. SecOps teams maintain security context, work more efficiently and respond faster to attacks when they manage case work without leaving the Defender portal. Here's the initial set of scenarios and features that case management supports.

- Define your own case workflow with custom status values

- Assign tasks to collaborators and configure due dates

- Handle escalations and complex cases by linking multiple incidents to a case

- Manage access to your cases using RBAC

This is just the start. Stay tuned for additional capabilities as we evolve this solution.

For more information, see the following articles:

- [Manage security operations cases natively in the Microsoft Defender portal](cases-overview.md)

- [Microsoft Sentinel blog - Improve SecOps collaboration with case management](https://techcommunity.microsoft.com/blog/MicrosoftSentinelBlog/improve-secops-collaboration-with-case-management/4369044)

### Unified device timeline in Microsoft Defender portal (Preview)

The **unified device timeline**, a single, cohesive view that integrates device activity from Microsoft Sentinel and Defender XDR into a single timeline, is now available in Preview. This feature streamlines security investigations by enabling analysts to access all relevant device activities in one place, reducing the need to switch between platforms and lowering incident response times.

For more information, see [Device entity page in Microsoft Defender](/defender-xdr/entity-page-device#timeline-tab).

### SOC optimization updates for unified coverage management

In workspaces enabled for unified security operations, SOC optimizations now support both SIEM and XDR data, with detection coverage from across Microsoft Defender services.

In the Defender portal, the **SOC optimizations** and **MITRE ATT&CK** pages also now provide extra functionality for threat-based coverage optimizations to help you understand the impact of the recommendations on your environment and help you prioritize which to implement first.

Enhancements include:

|Area | Details|

|-----|--------|

|**SOC optimizations Overview page** | - A **High**, **Medium**, or **Low** score for your current detection coverage. This sort of scoring can help you decide which recommendations to prioritize at a glance. <br><br>- An indication of the number of active Microsoft Defender products (services) out of all available products. This helps you understand whether there's a whole product that you're missing in your environment. |

| **Optimization details side pane**,<br> shown when you drill down to a specific optimization| - Detailed coverage analysis, including the number of user-defined detections, response actions, and products you have active. <br><br>- Detailed spider charts that show your coverage across different threat categories, for both user-defined and out-of-the-box detections. <br><br>- An option to jump to the specific threat scenario in the **MITRE ATT&CK** page instead of viewing MITRE ATT&CK coverage only in the side pane.<br><br>- An option to **View full threat scenario** to drill down to even further details about the security products and detections available to provide security coverage in your environment. |

|**MITRE ATT&CK page** | - A new toggle to view coverage by threat scenario. If you've jumped to the **MITRE ATT&CK** page from either a recommendation details side pane or from the **View full threat scenario** page, the **MITRE ATT&CK** page is pre-filtered for your threat scenario. <br><br>- The technique details pane, shown on the side when you select a specific MITRE ATT&CK technique, now shows the number of active detections out of all available detections for that technique. |

For more information, see [Optimize your security operations](/azure/sentinel/soc-optimization/soc-optimization-access?toc=%2Funified-secops-platform%2Ftoc.json&bc=%2Funified-secops-platform%2Fbreadcrumb%2Ftoc.json&tabs=defender-portal) and [Understand security coverage by the MITRE ATT&CK framework](/azure/sentinel/mitre-coverage).

## December 2024

- [New SOC optimization recommendations based on similar organizations (Preview)](#new-soc-optimization-recommendations-based-on-similar-organizations-preview)

- [Microsoft Sentinel workbooks now available to view directly in the Microsoft Defender portal](#microsoft-sentinel-workbooks-now-available-to-view-directly-in-the-microsoft-defender-portal)

### New SOC optimization recommendations based on similar organizations (Preview)

SOC optimizations now include new recommendations for adding data sources to your workspace based on the security posture of other organizations in similar industries and sectors as you, and with similar data ingestion patterns.

For more information, see [SOC optimization reference of recommendations](/azure/sentinel/soc-optimization/soc-optimization-reference).

### Microsoft Sentinel workbooks now available to view directly in the Microsoft Defender portal

Microsoft Sentinel workbooks are now available for viewing directly in the Microsoft Defender portal. Now, in the Defender portal, when you select **Microsoft Sentinel > Threat management > Workbooks**, you remain in the Defender portal instead of a new tab being opened for workbooks in the Azure portal. Continue tabbing out to the Azure portal only when you need to edit your workbooks.

Microsoft Sentinel workbooks are based on Azure Monitor workbooks, and help you visualize and monitor the data ingested to Microsoft Sentinel. Workbooks add tables and charts with analytics for your logs and queries to the tools already available.

For more information, see [Visualize and monitor your data by using workbooks in Microsoft Sentinel](/azure/sentinel/monitor-your-data) and [Connect Microsoft Sentinel to Microsoft Defender XDR](microsoft-sentinel-onboard.md).

## Related content

For more information on what's new with other Microsoft Defender security products and Microsoft Sentinel, see:

- [What's new in Microsoft Sentinel](/azure/sentinel/whats-new)

- [What's new in Microsoft Defender XDR](/defender-xdr/whats-new)

- [What's new in Microsoft Defender for Office 365](/defender-office-365/defender-for-office-365-whats-new)

- [What's new in Microsoft Defender for Endpoint](/defender-endpoint/whats-new-in-microsoft-defender-endpoint)

- [What's new in Microsoft Defender for Identity](/defender-for-identity/whats-new)

- [What's new in Microsoft Defender for Cloud Apps](/cloud-app-security/release-notes)

- [What's new in Microsoft Security Exposure Management](/security-exposure-management/whats-new)

You can also get product updates and important notifications through the [message center](https://admin.microsoft.com/Adminportal/Home#/MessageCenter).


# Overview Defender Portal

# Microsoft Defender portal

[Microsoft's unified security SecOps platform](overview-unified-security.md) combines Microsoft security services in the [Microsoft Defender portal](https://security.microsoft.com).

The portal provides a single location to monitor, manage, and configure pre-breach and post-breach security across on-premises and multicloud assets.

- **Pre-breach security**: Proactively visualize, assess, remediate, and monitor organizational security posture to reduce security risk and attack surfaces.

- **Post-breach security**: Continuously monitor, detect, investigate, and respond to real-time and emerging cybersecurity threats against organizational assets.

## Portal services

The Defender portal combines many Microsoft security services.

Service | Details

--- | ---

**Microsoft Defender XDR**<br/><br/> Detect and respond to cybersecurity threats. | [Defender XDR includes a suite of services](/defender-xdr/microsoft-365-defender) that come together in the Defender portal to provide unified threat protection across the enterprise.<br/><br/> Defender XDR services collect, correlate, and analyze threat data and signals across endpoints and devices, identities, email, apps, and OT/IoT assets. In the portal you can review, investigate, and respond to security alerts and incidents, automatically disrupt attacks, and proactively hunt for threats.<br/><br/>[Learn more](defender-xdr-portal.md) about Defender XDR in the Defender portal.

**Microsoft Sentinel**<br/><br/> Collect, analyze, and manage security data at scale using automation and orchestration.| Microsoft Sentinel fully integrates with Defender XDR in the Defender portal, providing additional threat protection capabilities such as attack disruption, unified entities and incidents, and SOC optimization.<br/><br/> For more information, see [Microsoft Sentinel in the Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal).

**Microsoft Defender Threat Intelligence**<br/><br/> Integrate threat intelligence into SOC operations. | The [Defender Threat Intelligence](/defender/threat-intelligence/what-is-microsoft-defender-threat-intelligence-defender-ti) platform extends the threat intelligence capabilities that are included in Defender XDR and Microsoft Sentinel.<br/><br/> Gather data from multiple sources to provide a pool of threat intelligence signals and data. Security teams use this data to understand adversary activities, analyze attacks, and hunt for security threats.

**Microsoft Security Exposure Management**<br/><br/> Proactively reduce security risk.| Use [Security Exposure Management](/security-exposure-management/microsoft-security-exposure-management) to reduce organizational attack surfaces and remediate security posture.<br/><br/> Continuously discover assets and data to get a comprehensive view of security across business assets. With the additional data context that Security Exposure Management provides, you can clearly visualize, analyze, and remediate weak areas of security.

**Microsoft Defender for Cloud**<br/><br/> Protect cloud workloads. | [Defender for Cloud](/defender-xdr/microsoft-365-security-center-defender-cloud) improves multicloud security posture, and protects cloud workloads against threats.<br/><br/> Defender for Cloud integrates into the Defender portal to provide a unified view of cloud security alerts, and a single location for investigations.

## Accessing the portal

In the Defender portal **Permissions** page, use the following methods to configure user access:

Methods | Details

--- | ---

[Global Microsoft Entra roles](/defender-xdr/m365d-permissions) | Accounts with the following Global Microsoft Entra roles can access Microsoft Defender XDR functionality and data: <ul><li>Security administrator or higher</li><li>Security Operator</li><li>Global Reader</li><li>Security Reader</li>

[Custom roles](/defender-xdr/custom-roles) | Allow access to specific data, tasks, and features using custom roles. Custom roles control granular access, and can be used together with Microsoft Entra global roles.

[Unified RBAC](/defender-xdr/manage-rbac) | Unified role-based access control (RBAC) provides a permissions management model for controlling user permissions in the Defender portal, and across services within the portal.

### Microsoft Sentinel permissions

When you're onboarded to the Microsoft Defender portal, existing Azure RBAC permissions are used to work with Microsoft Sentinel features in the Defender portal.

- Manage roles and permissions for Microsoft Sentinel users in the Azure portal.

- Any Azure RBAC changes are reflected in the Defender portal.

For more information, see [Roles and permissions in Microsoft Sentinel](/azure/sentinel/roles).

## Working in the portal

On the **Home** page, your view is determined by the services included in your subscriptions. Access settings are based on your [portal permissions](#accessing-the-portal).

Feature | Details

--- | ---

**Home page** | The Home page provides a view of your environment's security state. Review active threats, resources at risk, and a summary of all-up security posture. Use the dashboard for an up-to-date snapshot, and drill down to details as needed.

**Portal notifications** | Portal notifications keep you up-to-date with important information, including updates, events, complete or in-progress actions, and warnings and errors.<br/><br/> Notifications are sorted by their generated time in the notification panel, with the most recent displayed first. For more information, see [Configure alert notifications](/defender-xdr/configure-email-notifications?toc=/unified-secops-platform/toc.json&bc=/unified-secops-platform/).

**Search** | As you search the portal, results are categorized by sections related to your search terms.<br/><br/> Search provides results from within the portal, from the Microsoft Tech Community, and from Microsoft Learn documentation. Search history is stored in your browser and is accessible for 30 days.

**Guided tour** | Get a guided tour of managing endpoint security, or managing email and collaboration security.

**What's new** | Learn about the latest updates from the [Microsoft Defender XDR blog](https://techcommunity.microsoft.com/category/microsoftsecurityandcompliance/blog/microsoftthreatprotectionblog).

**Community** | Learn from others in [Microsoft security discussion spaces](https://techcommunity.microsoft.com/category/MicrosoftSecurityandCompliance) on Tech Community.

**Add cards** | Customize the **Home** page to get information that's most important to you.

## Exposure management

In **Exposure management**, review the overall state of your security posture, exposure, and risk.

Feature | Details

--- | ---

**Exposure management overview** | This dashboard provides a quick view of devices and cloud resources, including internet-facing devices and critical assets. Learn how well your key security initiatives are doing and drill down into top metrics for high-value vulnerabilities. Get exposure levels for different types of resources, and track security progress over time.

**Attack surfaces** | Visualize exposure data with the attack surface map.<br/>Explore resources and connections on the map, and drill down to focus on specific assets.<br/>In the **Attack path management** dashboard, review potential attack paths across your organization that attackers might exploit, together with choke points and critical assets in the path.

**Exposure insights** | Review and explore aggregated security posture data and insights across resources and workloads.<br/>Assess posture and readiness for your most important security projects, and track project metrics over time.<br/>Get security recommendations to remediate exposure issues.

**Secure score** | Review posture metrics based on [Microsoft Secure Score](/defender-xdr/microsoft-secure-score).

**Data connectors** | Connect third-party products to Security Exposure Management, and request new connectors.

For more information, see [Microsoft Security Exposure Management](/security-exposure-management/microsoft-security-exposure-management).

## Investigation and response

The **Investigation and response** section provides a single location for investigating security incidents, and responding to threats across the enterprise.

### Investigate incidents and alerts

Manage and investigate security incidents in a single location and from a single queue in the Defender portal. The **Incidents** and **Alerts** queues shows current security incidents and alerts across your services.

Feature | Details

--- | ---

**Incidents** | On the **Incidents** dashboard, review a list of the latest incidents and prioritize those marked as high severity. Each incident groups correlated alerts and associated data that makes up an attack. Drill down in an incident to get a full attack story, including information about associated alerts, devices, users, investigations, and evidence.

**Alerts** | In the **Alerts** dashboard, review alerts. Alerts are signals issued by portal services in response to threat detection activity.<br/><br/> The unified alerts queue displays new and in progress alerts from the last seven days, with the most recent alerts at the top. Filter on alerts to investigate as needed.

For more information, see [Incidents and alerts in the Microsoft Defender portal](/defender-xdr/incidents-overview).

### Hunt for threats

The **Hunting** area allows you to proactively inspect security events and data to locate known and potential threats.

Feature | Details

--- | ---

**Advanced hunting** | Explore and query up to 30 days of raw data. You can query using a guided query tool, use sample queries, or use [Kusto Query Language (KQL)](/kusto/query/?view=microsoft-sentinel&preserve-view=true) to build your own queries.

**Custom detection rules** | Create custom detection rules to proactively monitor and respond to events and system states. Use custom detection rules to trigger security alerts or automatic response actions.

For more information, see [Proactively hunt for threats with advanced hunting](/defender-xdr/advanced-hunting-overview) and [Custom detections overview](/defender-xdr/custom-detections-overview).

### Review pending threat remediations

Threat protection activity results in actions to remediate threats. Actions can be automated or manual. Actions that need approval or manual intervention are available in the **Action center**.

Feature | Details

--- | ---

**Action center** | Review the list of actions that need attention. Approve or reject actions one at a time, or in bulk. You can review action history to track remediation.

**Submissions** | Submit suspect spam, URLs, email issues and more to Microsoft.

For more information, see [Automated investigation and response](/defender-xdr/m365d-autoir) and [The Action center](/defender-xdr/m365d-action-center).

## Partner catalog

The **Partner catalog** section provides information about Defender partners.

The Defender portal supports the following types of partner integrations:

- **Third-party integrations** to help secure users with effective threat protection.

- **Professional services** that enhance detection, investigation, and threat intelligence capabilities.

## Threat intelligence

In the **Threat intelligence** section of the portal, get direct visibility into active and ongoing threat campaigns, and access threat intelligence information provided by the Defender Threat Intelligence platform.

Feature | Details

--- | ---

**Threat analytics** | Learn which threats are currently relevant in your organization.<br/><br/>Assess threat severity, drill down into specific threat reports, and identity actions to take. Different types of threat analytics reports are available.

**Intel profiles** | Review curated threat intelligence content organized by threat actors, tools, and known vulnerabilities.

**Intel Explorer** | Review threat intelligence information, and drill down to search and investigate.

**Intel projects** | Review and create projects to organize indicators of interest and indicators of compromise from an investigation. A project includes associated artifacts and a detailed history of names, descriptions, collaborators, and monitoring profiles.

For more information, see [Threat analytics](/defender-xdr/threat-analytics).

## Assets

The **Assets** page provides a unified view of discovered and protected assets, including devices, users, mailboxes, and apps. Review the total number of assets of each type, and drill down into specific asset details.

Feature | Details

--- | ---

**Devices** |On the **Device Inventory** page, get an overview of discovered devices in each tenant to which you have access. Review devices by type, and focus on high risk or critical devices.<br/><br/> Group devices logically by adding tags for context, and exclude devices you don't want to assess. Start an automated investigation for devices.

**Identities** | Get a summary of your user and account inventory.

For more information, see [Device entity page](/defender-xdr/entity-page-device) and [User entity page](/defender-xdr/investigate-users).

## Microsoft Sentinel

Access Microsoft Sentinel capabilities in the Defender portal.

Feature | Details

--- | ---

**Search** | [Search](/azure/sentinel/investigate-large-datasets) across logs, and access past searches.

**Threat management** | Visualize and monitor connected data with [workbooks](/azure/sentinel/monitor-your-data?tabs=defender-portal).<br/>[Investigate incidents](/azure/sentinel/investigate-incidents) and [classify alerts with entities](/azure/sentinel/customize-entity-activities?tabs=defender).<br/>Proactively [hunt for threats](/azure/sentinel/hunts) and [use notebooks](/azure/sentinel/hunting?tabs=azure-portal#notebooks-to-power-investigations) to power investigations.<br/> [Integrate threat intelligence](/azure/sentinel/threat-intelligence-integration) into threat detection, and [use the MITRE ATT&CK framework](/azure/sentinel/mitre-coverage) in analytics and incidents.

**Content management** | Discover and install out-of-the-box (OOTB) content from the [Content hub](/azure/sentinel/sentinel-solutions#discover-and-manage-microsoft-sentinel-content).<br/> Use [Microsoft Sentinel repositories](/azure/sentinel/ci-cd-custom-content) to connect to external source systems for continuous integration and delivery (CI/CD), rather than manually deploying and updating custom content.

**Configuration** | Ingest data by using [data connectors](/azure/sentinel/best-practices-data).<br/>[Create watchlists](/azure/sentinel/watchlists) to correlate and organize data sources.<br/>[Set up analytics rules](/azure/sentinel/threat-detection) to query and analyze collected data.<br/> [Automate](/azure/sentinel/automation/automation#automation-with-the-unified-security-operations-platform) threat responses.

For more information, see [Microsoft Sentinel](/azure/sentinel/overview) and [Microsoft Sentinel in the Microsoft Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal).

## Identities

In the **Identities** section of the Defender portal, monitor user and account health, and proactively manage identity-related risks with Defender for Identity.

Feature | Details

--- | ---

**Identity Security dashboard** | On the [Identity Security dashboard](/defender-for-identity/dashboard), get insights and real-time data about the security state of users and accounts.<br/><br/> The dashboard includes information about Defender for Identity deployment, information about highly privileged identities, and information about identity-related incidents.<br/><br/> If there's a problem with a Defender for Identity workspace, it's raised on the [Health issues page](/defender-for-identity/health-alerts).

**Health issues** | Any Defender for Identity global or sensor-based health issues are displayed on this page.

**Tools** | Access common tools to help you manage Defender for Identity.

For more information, see [Microsoft Defender for Identity](/defender-for-identity).

## Endpoints

In the **Endpoints** section of the portal, monitor and manage asset vulnerabilities with Microsoft Defender Vulnerability Management.

Feature | Details

--- | ---

**Vulnerability management** | Review vulnerability state in the dashboard. Get recommendations based on vulnerability assessment of devices, and remediate as needed.<br/> Review your organizational [software inventory](/defender-vulnerability-management/tvm-software-inventory), including vulnerable components, certificates, and hardware.<br/>Review [CVEs and security advisories](/defender-vulnerability-management/tvm-weaknesses-security-advisories).<br/> Review the [event timeline](/defender-vulnerability-management/threat-and-vuln-mgt-event-timeline) to determine the impact of vulnerabilities.<br/> Use [security baseline assessment](/defender-vulnerability-management/tvm-security-baselines) to assess devices against security benchmarks.

**Connected applications** | Get information about the [Microsoft Entra applications connected to Defender for Endpoint](/defender-endpoint/connected-applications).

**API explorer** | [Use the API explorer](/defender-endpoint/api/api-explorer) to construct and run API queries, test, and sent requests for available Defender for Endpoint API endpoints.

For more information, see [Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management) and [Microsoft Defender for Endpoint](/defender-endpoint/microsoft-defender-endpoint).

## Email and collaboration

In the **Email & collaboration** section, monitor, investigate, and manage security threats and responses to email and collaboration apps with Microsoft Defender for Office 365.

Feature | Details

--- | ---

**Investigations** | Run and review automated investigations.

**Explorer** | Hunt, investigate, and explore threats to emails and documents. Drill down into specific types of threats, including malware, phishing, and campaigns.

**Review** | Manage quarantined items and restricted senders.

**Campaigns** | Analyze coordinated attacks against your organization.

**Threat tracker** | Review saved and tracked queries, and follow trending campaigns.

**Policies and rules** | Configure and manage security policies to protect against threats, and receive activity alerts.

For more information, see [Microsoft Defender for Office 365](/defender-office-365/mdo-about).

## Cloud apps

In the **Cloud apps** section, review security to minimize risk and exposure to cloud apps using Microsoft Defender for Cloud Apps.

Feature | Details

--- | ---

**Cloud discovery** | Get an overview of cloud app security with [discovery reports](/defender-cloud-apps/set-up-cloud-discovery). Review a sample report, and create new reports.

**Cloud app catalog** | Get an overview of well-known cloud apps and their associated risk. You can sanction and unsanction apps as needed.

**OAuth apps** | Get visibility into [OAuth apps](/defender-cloud-apps/investigate-risky-oauth). Review apps, and filter settings to drill down.

**Activity log** | Review connected [app activity](/defender-cloud-apps/activity-filters) by cloud name, IP address, and related devices.

**Governance log** | Review [governance actions](/defender-cloud-apps/governance-actions).

**Policies** | Configure security policies for cloud apps.

For more information, see [Microsoft Defender for Cloud Apps](/defender-cloud-apps/what-is-defender-for-cloud-apps).

## SOC optimization

In the **SOC optimization** page, tighten up security controls to close threat coverage gaps, and tighten data ingestion rates  based on high-fidelity and actionable recommendations. SOC optimizations are tailored to your environment and based on your current coverage and threat landscape.

For more information, see [Optimize your security operations](/azure/sentinel/soc-optimization/soc-optimization-access).

## Reports

In the **Reports** page, review security reports across all areas, assets, and workloads. Available reports depend on the security services you have access to.

## Trials

In the **Trials** page, review trial solutions, designed to help you make decisions about upgrades and purchases.


# Defender Xdr Portal

# Microsoft Defender XDR in the Microsoft Defender portal

Microsoft Defender XDR unifies and coordinates threat protection across a broad range of assets, including devices and endpoints, identities, email, Microsoft 365 services, and SaaS apps.

Defender XDR consolidates threat signals and data across assets, so that you can monitor and manage security threats from a single location in the [Microsoft Defender portal](https://security.microsoft.com).

Defender XDR combines multiple Microsoft security services.

Service | Details

--- | ---

**[Protect against email threats with Defender for Office 365](/defender-office-365/mdo-sec-ops-guide)** | Helps protect email and Office 365 resources.

**[Protect devices with Defender for Endpoint](/defender-endpoint/mde-sec-ops-guide)** | Delivers preventative protection, post-breach detection, and automated investigation and response for devices.

**[Protect Active Directory with Defender for Identity](/defender-xdr/microsoft-365-security-center-mdi)** | Uses Active Directory signals to identify, detect, and investigate advanced threats, compromised identities, and malicious insider actions.

**[Protect SaaS cloud apps with Defender for Cloud Apps](/defender-xdr/microsoft-365-security-center-defender-cloud-apps)** | Provides deep visibility, strong data controls, and enhanced threat protection for SaaS and PaaS cloud apps.

**[Protect against a broad range of threats with Microsoft Sentinel](/azure/sentinel/microsoft-365-defender-sentinel-integration)** |  Microsoft Sentinel seamlessly integrates with Defender XDR to combine the capabilities of both products into a unified security platform for threat detection, investigation, hunting, and response.

## Detecting threats

Defender XDR provides continuous threat monitoring. When threats are detected [security alerts](/defender-xdr/alerts-incidents-correlation) are created. Defender automatically aggregates related alerts and security signals into [security incidents](/defender-xdr/alerts-incidents-correlation#incident-creation-and-alert-correlation).

Incidents define a complete picture of an attack. Incidents help SOC teams to understand attacks and respond more quickly. Incidents gather together related alerts, information about attack scope and progress, and the entities and assets involved in an attack.

A [single incident queue](/defender-xdr/incident-queue) in the Defender portal provides full visibility into the latest alerts and incidents, and historical data. You can search and query the incident queue, and prioritize responses based on severity.

## Automatically disrupting threats

Defender XDR uses [automatic attack disruption](/defender-xdr/automatic-attack-disruption) for containing attacks in progress, limiting attack impact, and providing more time for security teams to respond.

Automatic disruption relies on high-fidelity signals that are produced by incident correlation across million of Defender product signals and continuous investigation insights from Microsoft's security research team, to ensure a high signal-to-noise ratio.

Automatic disruption uses Defender XDR response actions when attacks are detected. Responses include containing or disabling assets.

Attack disruptions are clearly marked in the Defender XDR incident queue, and on specific incident pages.

## Hunting for threats

Proactive hunting inspects and investigates security events and data to locate known and potential security threats.

Defender XDR provides threat hunting capabilities in the Defender portal.

- **Advanced hunting**: SOC teams can use [advanced hunting](/defender-xdr/advanced-hunting-overview) with the Kusto Query Language (KQL) in the portal to create custom queries and rules for threat hunting across the enterprise. Analysts can search for indicators of compromise, anomalies, and suspicious activities across Defender XDR data sources.

If you're not familiar with KQL, Defender XDR provides a guided mode to create queries visually, and predefined query templates.

- **Custom detection rules**: In addition to advanced hunting, SOC teams can create [custom detection rules](/defender-xdr/custom-detections-overview) to proactively monitor and respond to events and system states. Rules can trigger alerts or automatic response actions.

## Responding to threats

Defender for XDR provides [automated investigation and response](/defender-xdr/m365d-autoir) capabilities. Automation reduces the volume of alerts that must be handled manually by SOC teams.

As alerts create incidents, automated investigations produce a verdict that determines whether a threat was found. When suspicious and malicious threats are identified, remediation actions include sending a file to quarantine, stopping a process, blocking a URL, or isolating a device.

You can view a summary of automated investigations and responses in the Home page of the portal. Pending remediation actions are handled in the portal Action Center.


# Zero Trust

# Zero Trust with unified security operations in the Microsoft Defender portal

Zero Trust is a security strategy for designing and implementing the following sets of security principles:

|Security principle |Description|

|---|---|

|**Verify explicitly** |Always authenticate and authorize based on all available data points. |

|**Use least privilege access** |Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection.      |

|**Assume breach** |Minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses. |

This article describes how the Microsoft Defender portal provides centralized access to the tools and capabilities necessary to implement a comprehensive Zero Trust solution with unified security operations.

## Verify explicitly with the Defender portal

To effectively verify explicitly, the Defender portal provides a variety of tools and services to ensure that every access request is authenticated and authorized based on comprehensive data analysis. For example:

- **Microsoft Defender XDR** provides extended detection and response across users, identities, devices, apps, and emails. Add **Microsoft Defender for Cloud** to stretch that threat protection across multi-cloud and hybrid environments, and **Microsoft Entra ID Protection** to help you evaluate risk data from sign-in attempts.

- **Microsoft Defender Threat Intelligence** enriches your data with the latest threat updates and indicators of compromise (IoCs).

- **Microsoft Security Copilot** provides AI-driven insights and recommendations that enhance and automate your security operations.

- Add **Microsoft Security Exposure Management** to enrich your asset information with extra security context.

- **Microsoft Sentinel** collects data from across the environment and analyzes threats and anomalies so that your organization and any automation implemented, can act based on all available and verified data points. Microsoft Sentinel automation can also help you use risk-based signals captured across the Defender portal to take action, such as blocking or authorizing traffic based on the level of risk.

For more information, see:

- [What is Microsoft Defender XDR?](/defender-xdr/microsoft-365-defender)

- [What is Microsoft Defender for Cloud?](/azure/defender-for-cloud/defender-for-cloud-introduction)

- [What is Microsoft Entra ID Protection?](/entra/id-protection/overview-identity-protection)

- [What is Microsoft Defender Threat Intelligence (Defender TI)?](/defender/threat-intelligence/what-is-microsoft-defender-threat-intelligence-defender-ti)

- [What is Microsoft Security Copilot?](/copilot/security/microsoft-security-copilot)

- [What is Microsoft Security Exposure Management?](/security-exposure-management/get-started-exposure-management)

- [What is Microsoft Sentinel?](/azure/sentinel/overview?tabs=defender-portal)

## Use least privileged access across the Defender portal

The Defender portal also provides a comprehensive set of tools to help you implement least privilege access across your environment. For example:

- Implement **Microsoft Defender XDR** unified role-based access control (RBAC) to assign permissions based on roles, ensuring users have only the access they need to perform their tasks.

- Provide just-in-time activations for privileged role assignments by using **Microsoft Entra ID Protection's** Privileged Identity Management (PIM).

- Implement **Microsoft Defender for Cloud Apps** Conditional Access policies to enforce adaptive access policies based on user, location, device, and risk signals to ensure secure access to resources.

- Configure **Microsoft Defender for Cloud** threat protection to block and flag risky behavior, and employ hardening mechanisms to implement least privilege access and JIT VM access.

**Microsoft Security Copilot** also authenticates users with on-behalf-of (OBO) authentication, ensuring that users have access only to the resources they need.

For more information, see:

- [Microsoft Defender unified role-based access control (RBAC)](/defender-xdr/manage-rbac)

- [What is Microsoft Entra Privileged Identity Management?](/entra/id-governance/privileged-identity-management/pim-configure)

- [Conditional Access app control in Microsoft Defender for Cloud Apps](/defender-cloud-apps/proxy-intro-aad)

- [Start planning multicloud protection with Defender for Cloud](/azure/defender-for-cloud/plan-multicloud-security-get-started)

- [Understand authentication in Microsoft Security Copilot](/copilot/security/authentication)

## Assume breach across the Defender portal

Assuming breach helps organizations prepare for and respond to security incidents more effectively. For example:

- Configure **Microsoft Defender XDR** automatic attack disruption to contain attacks in progress, limiting lateral movement and reducing impact with high-fidelity signals and continuous investigation insights.

- Automatically respond to security threats across the enterprise by using **Microsoft Sentinel's** automation rules and playbooks.

- Implement **Microsoft Defender for Cloud's** recommendations to block and flag risky or suspicious behavior, and automate responses across coverage areas with Azure Logic Apps.

- Enable **Microsoft Entra ID Protection** notifications so that you can respond appropriately when a user is flagged as at risk.

For more information, see:

- [Automatic attack disruption in Microsoft Defender XDR](/defender-xdr/automatic-attack-disruption)

- [Automation in Microsoft Sentinel - security orchestration, automation, and response (SOAR)](/azure/sentinel/automation/automation)

- [What's new in Defender for Cloud recommendations, alerts, and incidents](/azure/defender-for-cloud/release-notes-recommendations-alerts)

- [Microsoft Entra ID Protection notifications](/entra/id-protection/howto-identity-protection-configure-notifications)

## Next step

[Planning guidance for unified security operations in the Microsoft Defender portal](overview-plan.md)


# Overview Plan

# Planning guidance for unified security operations in the Microsoft Defender portal

This article describes how to plan your deployment for unified security operations in the Microsoft Defender portal. Unify security operations to help you reduce risk, prevent attacks, detect and disrupt cyberthreats in real time, and respond faster with AI-enhanced security capabilities, all from the [Microsoft Defender portal](https://security.microsoft.com).

## Plan your deployment

The Defender portal combines services like Microsoft Defender XDR, Microsoft Sentinel, Microsoft Security Exposure Management, and Microsoft Security Copilot for unified security operations.

The first step in planning your deployment is to select the services you want to use.

As a basic prerequisite, you'll need both [Microsoft Defender XDR](/defender-xdr/microsoft-365-defender) and [Microsoft Sentinel](/azure/sentinel/overview) to monitor and protect both Microsoft and non-Microsoft services and solutions, including both cloud and on-premises resources.

Deploy any of the following services to add security across your endpoints, identities, email, and applications to provide integrated protection against sophisticated attacks.

Microsoft Defender XDR services include:

| Service | Description |

| ------- | ----------- |

| [**Microsoft Defender for Office 365**](/defender-office-365/mdo-about) | Protects against threats posed by email messages, URL links, and Office 365 collaboration tools. |

| [**Microsoft Defender for Identity**](/defender-for-identity/what-is) | Identifies, detects, and investigates threats from both on-premises Active Directory and cloud identities like Microsoft Entra ID. |

| [**Microsoft Defender for Endpoint**](/defender-endpoint/microsoft-defender-endpoint) | Monitors and protects endpoint devices, detects and investigates device breaches, and automatically responds to security threats. |

| [**Microsoft Defender for IoT**](/defender-for-iot/microsoft-defender-iot) | Provides both IoT device discovery and security value for IoT devices. |

| [**Microsoft Defender Vulnerability Management**](/defender-vulnerability-management/defender-vulnerability-management) | Identifies assets and software inventory, and assesses device posture to find security vulnerabilities. |

| [**Microsoft Defender for Cloud Apps**](/defender-cloud-apps/what-is-defender-for-cloud-apps) | Protects and controls access to SaaS cloud apps. |

Other services supported in the Microsoft Defender portal, but not licensed with Microsoft Defender XDR, include:

| Service | Description |

| ------- | ----------- |

| [**Microsoft Security Exposure Management**](/security-exposure-management/microsoft-security-exposure-management) | Provides a unified view of security posture across company assets and workloads, enriching asset information with security context. |

| [**Microsoft Security Copilot**](/copilot/security/microsoft-security-copilot) | Provides AI-driven insights and recommendations to enhance your security operations. |

| [**Microsoft Defender for Cloud**](/azure/defender-for-cloud/) | Protects multi-cloud and hybrid environments with advanced threat detection and response. |

| [**Microsoft Defender Threat Intelligence**](/defender/threat-intelligence/what-is-microsoft-defender-threat-intelligence-defender-ti) | Streamlines threat intelligence workflows by aggregating and enriching critical data sources to correlate indicators of compromise (IOCs) with related articles, actor profiles, and vulnerabilities. |

| [**Microsoft Entra ID Protection**](/entra/id-protection/overview-identity-protection) | Evaluates risk data from sign-in attempts to evaluate the risk of each sign-in to your environment. |

| **[Microsoft Purview Insider Risk Management](/purview/insider-risk-management)** | Correlates various signals to identify potential malicious or inadvertent insider risks, such as IP theft, data leakage and security violations. |

## Review service prerequisites

Before you deploy Microsoft Defender services for unified security operations, review the prerequisites for each service you plan to use. The following table lists the services and links for more information:

| Security service         | Prerequisites                  |

| ------------------------ | ------------------------------ |

| **Required for unified security operations**       |      |

| Microsoft Defender XDR | [Microsoft Defender XDR prerequisites](/defender-xdr/prerequisites) |

| Microsoft Sentinel                                       | [Prerequisites to deploy Microsoft Sentinel](/azure/sentinel/prerequisites)  |

| **Optional Microsoft Defender XDR services**              |                                                 |

| Microsoft Defender for Office | [Microsoft Defender XDR prerequisites](/defender-xdr/prerequisites) |

| Microsoft Defender for Identity                          | Microsoft Defender for Identity prerequisites:<br>[Sensor v2.x](/defender-for-identity/deploy/prerequisites-sensor-version-2) / [Sensor v3.x (Preview)](/defender-for-identity/deploy/deploy-sensor-v3)  |

| Microsoft Defender for Endpoint                          | [Set up Microsoft Defender for Endpoint deployment](/defender-endpoint/production-deployment)   |

| Enterprise monitoring with Microsoft Defender for IoT    | [Prerequisites for Defender for IoT in the Defender portal](/defender-for-iot/prerequisites)   |

| Microsoft Defender Vulnerability Management              | [Prerequisites & Permissions for Microsoft Defender Vulnerability Management](/defender-vulnerability-management/tvm-prerequisites)   |

| Microsoft Defender for Cloud Apps                        | [Get started with Microsoft Defender for Cloud Apps](/defender-cloud-apps/get-started)   |

| **Other services supported in the Microsoft Defender portal**   |   |

| Microsoft Security Exposure Management                   | [Prerequisites and support](/security-exposure-management/prerequisites)  |

| Microsoft Security Copilot                               | [Minimum requirements](/copilot/security/get-started-security-copilot#minimum-requirements)  |

| Microsoft Defender for Cloud                             | [Start planning multicloud protection](/azure/defender-for-cloud/plan-multicloud-security-get-started) and other articles in the same section. |

| Microsoft Defender Threat Intelligence                   | [Prerequisites for Defender Threat Intelligence](/defender/threat-intelligence/learn-how-to-access-microsoft-defender-threat-intelligence-and-make-customizations-in-your-portal#prerequisites) |

| Microsoft Entra ID Protection                            | [Prerequisites for Microsoft Entra ID Protection](/entra/id-protection/how-to-deploy-identity-protection#prerequisites) |

| Microsoft Purview Insider Risk Management | [Get started with insider risk management](/purview/insider-risk-management-configure?tabs=purview-portal) |

## Review data security and privacy practices

Before you deploy Microsoft Defender services for unified security operations, make sure that you understand the data security and privacy practices for each service you plan to use. The following table lists the services and links for more information. Note that several services use the data security and retention practices for Microsoft Defender XDR instead of have separate practices of their own.

| Security service         | Data security and privacy |

| ------------------------ |--------------------------------------- |

| **Required for unified security operations**       | |

| Microsoft Defender XDR | [Data security and retention in Microsoft Defender XDR](/defender-xdr/data-privacy) |

| Microsoft Sentinel | [Geographical availability and data residency in Microsoft Sentinel](/azure/sentinel/geographical-availability-data-residency) |

| **Optional Microsoft Defender XDR services** | |

| Microsoft Defender for Office | [Data security and retention in Microsoft Defender XDR](/defender-xdr/data-privacy) |

| Microsoft Defender for Identity | [Privacy with Microsoft Defender for Identity](/defender-for-identity/privacy-compliance) |

| Microsoft Defender for Endpoint | [Microsoft Defender for Endpoint data storage and privacy](/defender-endpoint/data-storage-privacy) |

| Enterprise monitoring with Microsoft Defender for IoT | [Data security and retention in Microsoft Defender XDR](/defender-xdr/data-privacy) |

| Microsoft Defender Vulnerability Management | [Microsoft Defender for Endpoint data storage and privacy](/defender-endpoint/data-storage-privacy) |

| Microsoft Defender for Cloud Apps | [Privacy with Microsoft Defender for Cloud Apps](/defender-cloud-apps/cas-compliance-trust) |

| **Other services supported in the Microsoft Defender portal** | |

| Microsoft Security Exposure Management | [Data freshness, retention, and related functionality](/security-exposure-management/microsoft-security-exposure-management#data-freshness-retention-and-related-functionality) |

| Microsoft Security Copilot | [Privacy and data security in Microsoft Security Copilot](/copilot/security/privacy-data-security) |

| Microsoft Defender for Cloud | [Microsoft Defender for Cloud data security](/azure/defender-for-cloud/data-security) |

| Microsoft Defender Threat Intelligence | [Data security and retention in Microsoft Defender XDR](/defender-xdr/data-privacy) |

| Microsoft Entra ID Protection | [Microsoft Entra data retention](/entra/identity/monitoring-health/reference-reports-data-retention) |

| Microsoft Purview Insider Risk Management | [Microsoft Purview Insider Risk Management and Communication Compliance privacy guide](/purview/insider-risk-solution-privacy) <br><br> [Messaging Records Management (MRM) and Retention Policies in Microsoft 365](/microsoft-365/troubleshoot/retention/mrm-and-retention-policy) |

## Plan your Log Analytics workspace architecture

To get started with unified security operations using Microsoft Sentinel in the Defender portal, you first need a Log Analytics workspace enabled for Microsoft Sentinel. A single Log Analytics workspace might be sufficient for many environments, but many organizations create multiple workspaces to optimize costs and better meet different business requirements.

Design the Log Analytics workspace you want to enable for Microsoft Sentinel. Consider parameters such as any compliance requirements you have for data collection and storage and how to control access to Microsoft Sentinel data.

For more information, see:

1. [Design workspace architecture](/azure/azure-monitor/logs/workspace-design?toc=%2Fazure%2Fsentinel%2FTOC.json&bc=%2Fazure%2Fsentinel%2Fbreadcrumb%2Ftoc.json)

1. [Review sample workspace designs](/azure/sentinel/sample-workspace-designs)

## Plan Microsoft Sentinel costs and data sources

The Defender portal can natively ingest data from first-party Microsoft services, such as Microsoft Defender for Cloud Apps and Microsoft Defender for Cloud. We recommend expanding your coverage to other data sources in your environment by adding Microsoft Sentinel data connectors.

### Determine your data sources

Determine the full set of data sources you'll be ingesting data from, and the data size requirements to help you accurately project your deployment's budget and timeline. You might determine this information during your business use case review, or by evaluating a current SIEM that you already have in place. If you already have a SIEM in place, analyze your data to understand which data sources provide the most value and should be ingested into Microsoft Sentinel.

For example, you might want to use any of the following recommended data sources:

- **Azure services**: If any of the following services are deployed in Azure, use the following connectors to send these resources' Diagnostic Logs to Microsoft Sentinel:

- **Azure Firewall**

- **Azure Application Gateway**

- **Keyvault**

- **Azure Kubernetes Service**

- **Azure SQL**

- **Network Security Groups**

- **Azure-Arc Servers**

We recommend that you set up Azure Policy to require that their logs be forwarded to the underlying Log Analytics workspace. For more information, see [Create diagnostic settings at scale using Azure Policy](/azure/azure-monitor/essentials/diagnostic-settings-policy).

- **Virtual machines**: For virtual machines hosted on-premises or in other clouds that require their logs collected, use the following data connectors:

- **Windows Security Events using AMA**

- Events via **Defender for Endpoint** (for server)

- **Syslog**

- **Network virtual appliances / on-premises sources**: For network virtual appliances or other on-premises sources that generate [Common Event Format (CEF) or SYSLOG logs](/azure/sentinel/connect-cef-syslog-ama?branch=main&tabs=single%2Ccef%2Cportal), use the following data connectors:

- **Syslog via AMA**

- **Common Event Format (CEF) via AMA**

For more information, see [Prioritize data connectors](/azure/sentinel/prioritize-data-connectors).

### Plan your budget

Plan your Microsoft Sentinel budget, considering cost implications for each planned scenario. Make sure that your budget covers the cost of data ingestion for both Microsoft Sentinel and Azure Log Analytics, any playbooks that will be deployed, and so on.  For more information, see:

- [Log retention plans in Microsoft Sentinel](/azure/sentinel/log-plans)

- [Plan costs and understand Microsoft Sentinel pricing and billing](/azure/sentinel/billing?tabs=simplified%2Ccommitment-tiers)

## Understand Microsoft security portals and admin centers

While the Microsoft Defender portal is the home for monitoring and managing security across your identities, data, devices, and apps, you need to access various portals for certain specialized tasks.

Microsoft security portals include:

| Portal name | Description | Link |

|---|---|---|

| **Microsoft Defender portal** | Monitor and respond to threat activity and strengthen security posture across your identities, email, data, endpoints, and apps with [Microsoft Defender XDR](/defender-xdr/microsoft-365-defender) | [security.microsoft.com](https://security.microsoft.com/)  <br/><br/>The Microsoft Defender portal is where you view and manage alerts, incidents, settings, and more. |

| **Defender for Cloud portal** | Use [Microsoft Defender for Cloud](/azure/security-center/security-center-intro) to strengthen the security posture of your data centers and your hybrid workloads in the cloud | [portal.azure.com/#blade/Microsoft_Azure_Security](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/0) |

| **Microsoft Security Intelligence portal** | Get security intelligence updates for Microsoft Defender for Endpoint, submit samples, and explore the threat encyclopedia | [microsoft.com/wdsi](https://microsoft.com/wdsi) |

The following table describes portals for other workloads that can impact your security. Visit these portals to manage identities, permissions, device settings, and data handling policies.

| Portal name | Description | Link |

|---|---|---|

| **Microsoft Entra admin center** | Access and administer the [Microsoft Entra](/entra) family to protect your business with decentralized identity, identity protection, governance, and more, in a multicloud environment| [entra.microsoft.com](https://entra.microsoft.com/) |

| **Azure portal** | View and manage all your [Azure resources](/azure/azure-resource-manager/management/overview)  | [portal.azure.com](https://portal.azure.com/) |

| **Microsoft Purview portal** | Manage data handling policies and ensure [compliance with regulations](/compliance/regulatory/offering-home) | [purview.microsoft.com](https://purview.microsoft.com/) |

| **Microsoft 365 admin center** | Configure Microsoft 365 services; manage roles, licenses, and track updates to your Microsoft 365 services | [admin.microsoft.com](https://go.microsoft.com/fwlink/p/?linkid=2166757) |

| **Microsoft Intune admin center** | Use [Microsoft Intune](/mem/intune/fundamentals/what-is-intune) to manage and secure devices. Can also combine Intune and Configuration Manager capabilities. | [intune.microsoft.com](https://intune.microsoft.com/) |

| **Microsoft Intune portal** | Use [Microsoft Intune](/mem/intune/fundamentals/what-is-intune) to deploy device policies and monitor devices for compliance | [intune.microsoft.com](https://intune.microsoft.com/#blade/Microsoft_Intune_DeviceSettings/DevicesMenu/overview) |

## Plan roles and permissions

The Microsoft Defender portal unifies the following role-based access control (RBAC) models for unified security operations:

- [Microsoft Entra ID RBAC](/entra/identity/role-based-access-control/custom-overview), used for delegating access to Defender access, like device groups

- [Azure RBAC](/azure/role-based-access-control/), used by Microsoft Sentinel to delegate permissions

- [Defender unified RBAC](/defender-xdr/manage-rbac), used to delegate permissions across Defender solutions

While permissions granted through Azure RBAC for Microsoft Sentinel are federated during runtime with Defender's unified RBAC, Azure RBAC and Defender RBAC are still managed separately.

Defender's unified RBAC isn't required for your workspace to be onboarded to the Defender portal, and Microsoft Sentinel permissions continue to work as expected in the Defender portal even without unified RBAC. However, using unified RBAC does simplify the delegation of permissions across Defender solutions. For more information, see [Activate Microsoft Defender unified role-based access control (RBAC)](/defender-xdr/activate-defender-rbac).

[!INCLUDE [mininum-access-requirements](includes/mininum-access-requirements.md)]

For the following services, use the different roles available, or create custom roles, to give you fine-grained control over what users can see and do. For more information, see:

| Security service         | Link to role requirements                  |

| ------------------------ | ------------------------------------------- |

| **Required for unified security operations**                                                   |                           |

| Microsoft Defender XDR  | [Manage access to Microsoft Defender XDR with Microsoft Entra global roles](/defender-xdr/m365d-permissions)               |

| Microsoft Sentinel                                       | [Roles and permissions in Microsoft Sentinel](/azure/sentinel/roles)            |

| **Optional Microsoft Defender XDR services**                |  |

| Microsoft Defender for Identity                          | [Microsoft Defender for Identity role groups](/defender-for-identity/role-groups)          |

| Microsoft Defender for Office | [Microsoft Defender for Office 365 permissions in the Microsoft Defender portal](/defender-office-365/mdo-portal-permissions) |

| Microsoft Defender for Endpoint      | [Assign roles and permissions for Microsoft Defender for Endpoint deployment](/defender-endpoint/prepare-deployment)       |

| Microsoft Defender Vulnerability Management   | [Relevant permission options for Microsoft Defender Vulnerability Management ](/defender-vulnerability-management/tvm-prerequisites#relevant-permission-options)       |

| Microsoft Defender for Cloud Apps           | [Configure admin access for Microsoft Defender for Cloud Apps](/defender-cloud-apps/manage-admins)      |

| **Other services supported in the Microsoft Defender portal**             |             |

| Microsoft Security Exposure Management     | [Permissions for Microsoft Security Exposure Management](/security-exposure-management/prerequisites)   |

| Microsoft Defender for Cloud      | [User roles and permissions](/azure/defender-for-cloud/permissions) |

| Microsoft Purview Insider Risk Management | [Enable permissions for insider risk management](/purview/insider-risk-management-configure?tabs=purview-portal#step-1-required-enable-permissions-for-insider-risk-management) |

For more information, see:

- [Plan roles and permissions for Microsoft Sentinel](/azure/sentinel/roles)

- [Azure built-in roles](/azure/role-based-access-control/built-in-roles)

- [Microsoft Sentinel roles](/azure/role-based-access-control/built-in-roles#security)

- [Onboarding prerequisites](microsoft-sentinel-onboard.md#prerequisites)

- [Managing unified RBAC in Microsoft Defender](https://aka.ms/defender_RBAC) (video demo)

## Plan Zero Trust activities

Unified security operations in the Defender portal is part of [Microsoft's Zero Trust security model](zero-trust.md), which includes the following principles:

|Security principle |Description|

|---|---|

|**Verify explicitly** |Always authenticate and authorize based on all available data points. |

|**Use least privilege access** |Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection.      |

|**Assume breach** |Minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses. |

Zero Trust security is designed to protect modern digital environments by leveraging network segmentation, preventing lateral movement, providing least-privileged access, and using advanced analytics to detect and respond to threats.

For more information about implementing Zero Trust principles in the Defender portal, see Zero Trust content for the following services:

- [Microsoft Defender XDR](/defender-xdr/zero-trust-with-microsoft-365-defender?toc=/unified-secops-platform/toc.json&bc=/unified-secops-platform/breadcrumb/toc.json)

- [Microsoft Sentinel](/security/operations/siem-xdr-overview?toc=/unified-secops-platform/toc.json&bc=/unified-secops-platform/breadcrumb/toc.json)

- [Microsoft Defender for Identity](/defender-for-identity/zero-trust?toc=/unified-secops-platform/toc.json&bc=/unified-secops-platform/breadcrumb/toc.json)

- [Microsoft Defender for Office 365](/defender-office-365/zero-trust-with-microsoft-365-defender-office-365?toc=/unified-secops-platform/toc.json&bc=/unified-secops-platform/breadcrumb/toc.json)

- [Microsoft Defender for Endpoint](/defender-endpoint/zero-trust-with-microsoft-defender-endpoint?toc=/unified-secops-platform/toc.json&bc=/unified-secops-platform/breadcrumb/toc.json)

- [Microsoft Defender for Cloud Apps](/defender-cloud-apps/zero-trust?toc=/unified-secops-platform/toc.json&bc=/unified-secops-platform/breadcrumb/toc.json)

- [Microsoft Security Exposure Management](https://techcommunity.microsoft.com/blog/microsoftsecurityandcompliance/respond-to-trending-threats-and-adopt-zero-trust-with-exposure-management/4130133)

- [Microsoft Defender for Cloud](/azure/defender-for-cloud/zero-trust?toc=/unified-secops-platform/toc.json&bc=/unified-secops-platform/breadcrumb/toc.json)

- [Microsoft Security Copilot](/security/zero-trust/copilots/zero-trust-microsoft-copilot-for-security)

- [Microsoft Entra ID Protection](/entra/id-protection/how-to-deploy-identity-protection)

- [Microsoft Purview](/purview/zero-trust-microsoft-purview)

For more information, see the [Zero Trust Guidance Center](/security/zero-trust/zero-trust-overview).

## Next step

[Deploy for unified security operations](overview-deploy.md)


# Gov Support

# Microsoft Defender portal service support for US Government customers

This article provides information about support for US Government customers by unified security operations services in the Microsoft Defender portal.

## Feature availability

- All features in Microsoft's SecOps platform that are in general availability are available in commercial and GCC High and DoD clouds.

GCC is supported with the following limitation: [Advanced hunting](/defender-xdr/advanced-hunting-overview) queries that reference both Microsoft Sentinel and Microsoft Defender XDR tables aren't supported in GCC Moderate environments. If you use _Search_ or _Union *_ in your queries, consider replacing the _*_ with an explicit list of tables that are limited to Microsoft Sentinel only or Defender XDR only.

- Features still in preview are available only in the commercial cloud.

For more information, see:

- [Microsoft Defender XDR for US Government customers](/defender-xdr/usgov)

- [Microsoft Sentinel feature support for Azure commercial/other clouds](/azure/sentinel/feature-availability)

## Portal URLs

The following are the Microsoft Defender portal URLs for US Government customers:

- **GCC**:	https://security.microsoft.com

- **GCC High**:	https://security.microsoft.us

- **DoD**:	https://security.apps.mil

If you're a GCC customer and are moving from Microsoft Defender for Endpoint commercial to GCC, use https://transition.security.microsoft.com to access your Microsoft Defender for Endpoint commercial data.

## API access

When you use a US government cloud, use the following URIs instead of the public URIs listed in the API documentation:

- **Login**:

- **GCC**: `https://login.microsoftonline.com`

- **GCC High and DoD**: `https://login.microsoftonline.us`

- **Microsoft Defender XDR API**:

- **GCC**: `https://api-gcc.security.microsoft.us`

- **GCC High and DoD**: `https://api-gov.security.microsoft.us`


# Overview Deploy

# Deploy for unified security operations

The Microsoft Defender portal provides unified security operations with Microsoft Defender XDR, Microsoft Sentinel, and other services. Together, Defender portal services provide a comprehensive view of your organization's security posture and helps you to detect, investigate, and respond to threats across your organization.

Microsoft Security Exposure Management and Microsoft Threat Intelligence are available in any environment that meets the prerequisites, to users configured with required permissions.

## Prerequisites

- Before you deploy Microsoft Defender services for unified security operations, make sure that you have a plan in place, including a workspace design and an understanding of Microsoft Sentinel costs and billing.

For more information, see [Planning guidance for unified security operations in the Microsoft Defender portal](overview-plan.md).

## Deploy Microsoft Defender XDR services

Microsoft Defender XDR unifies incident response by integrating key capabilities across services, including Microsoft Defender for Endpoint, Microsoft Defender for Office 365, Microsoft Defender for Cloud Apps, and Microsoft Defender for Identity. This unified experience adds powerful features you can access in the Microsoft Defender portal.

1. Microsoft Defender XDR automatically turns on when eligible customers with the required permissions visit Microsoft Defender portal. For more information, see [Turn on Microsoft Defender XDR](/defender-xdr/m365d-enable).

1. Continue by deploying Microsoft Defender XDR services. We recommend using the following order:

1. [Deploy Microsoft Defender for Identity](/defender-for-identity/deploy/quick-installation-guide).

1. [Deploy Microsoft Defender for Office 365](/defender-xdr/pilot-deploy-defender-office-365?toc=%2Fdefender-office-365%2FTOC.json&bc=%2Fdefender-office-365%2Fbreadcrumb%2Ftoc.json).

1. [Deploy Microsoft Defender for Endpoint](/defender-endpoint/mde-planning-guide). Add [Microsoft Defender Vulnerability Management](/defender-vulnerability-management/get-defender-vulnerability-management) and/or [Enterprise monitoring for IoT devices](/azure/defender-for-iot/organizations/eiot-defender-for-endpoint), as relevant for your environment.

1. [Deploy Microsoft Defender for Cloud Apps](/defender-cloud-apps/general-setup).

## Configure Microsoft Entra ID Protection

Microsoft Defender XDR can ingest and include signals from Microsoft Entra ID Protection, which evaluates risk data from billions of sign-in attempts and evaluates the risk of each sign-in to your environment. Microsoft Entra ID Protection data is used by Microsoft Entra ID to allow or prevent account access, depending on how Conditional Access policies are configured.

Configure Microsoft Entra ID Protection to enhance your security posture and add Microsoft Entra signals to your unified security operations. For more information, see [Configure your Microsoft Entra ID Protection policies](/entra/id-protection/how-to-deploy-identity-protection).

## Deploy Microsoft Defender for Cloud

Microsoft Defender for Cloud provides a unified security management experience for your cloud resources, and can also send signals to Microsoft Defender XDR. For example, you might want to start by connecting your Azure subscriptions to Microsoft Defender for Cloud, and then move on to other cloud environments.

For more information, see [Connect your Azure subscriptions](/azure/defender-for-cloud/connect-azure-subscription).

## Onboard to Microsoft Security Copilot

Onboard to Microsoft Security Copilot to enhance your security operations by leveraging advanced AI capabilities. Security Copilot assists in threat detection, investigation, and response, providing actionable insights and recommendations to help you stay ahead of potential threats. Use Security Copilot to automate routine tasks, reduce the time to detect and respond to incidents, and improve the overall efficiency of your security team.

For more information, see [Get started with Security Copilot](/copilot/security/get-started-security-copilot).

## Architect your workspace and onboard to Microsoft Sentinel

The first step in using Microsoft Sentinel is to create a Log Analytics workspace, if you don't have one already. A single Log Analytics workspace might be sufficient for many environments, but many organizations create multiple workspaces to optimize costs and better meet different business requirements. The Defender portal supports a primary workspace and multiple secondary workspaces.

1. Create a Security resource group for governance purposes, which allows you to isolate Microsoft Sentinel resources and role-based access to the collection.

1. Create a Log Analytics workspace in the Security resource group and onboard Microsoft Sentinel into it.

For more information, see [Onboard Microsoft Sentinel](/azure/sentinel/quickstart-onboard) and [Multiple Microsoft Sentinel workspaces in the Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2310579).

## Configure roles and permissions

Provision your users based on the access plan you'd [prepared earlier](overview-plan.md#plan-roles-and-permissions). To comply with Zero Trust principles, we recommend that you use role-based access control (RBAC) to provide user access only to the resources that are allowed and relevant for each user, instead of providing access to the entire environment.

[!INCLUDE [mininum-access-requirements](includes/mininum-access-requirements.md)]

For more information, see:

- [Onboarding prerequisites](microsoft-sentinel-onboard.md#prerequisites)

- [Assign Microsoft Entra ID roles to users](/entra/identity/role-based-access-control/manage-roles-portal)

- [Grant a user access to Azure roles](/azure/role-based-access-control/quickstart-assign-role-user-portal)

- [Managing unified RBAC in Microsoft Defender](https://aka.ms/defender_RBAC) (video demo)

## Onboard to the Defender portal

When you onboard Microsoft Sentinel to the Defender portal, you unify capabilities with Microsoft Defender XDR like incident management and advanced hunting for unified security operations. For more information, see [Connect Microsoft Sentinel to Microsoft Defender](microsoft-sentinel-onboard.md).

## Fine-tune system configurations

Use the following Microsoft Sentinel configuration options to fine-tune your deployment:

### Enable health and auditing

Monitor the health and audit the integrity of supported Microsoft Sentinel resources by turning on the auditing and health monitoring feature in Microsoft Sentinel's Settings page. Get insights on health drifts, such as the latest failure events or changes from success to failure states, and on unauthorized actions, and use this information to create notifications and other automated actions.

For more information, see[Turn on auditing and health monitoring for Microsoft Sentinel](/azure/sentinel/enable-monitoring?tabs=azure-portal).

### Configure Microsoft Sentinel content

Based on the [data sources you selected](overview-plan.md#plan-microsoft-sentinel-costs-and-data-sources) when planning your deployment, install Microsoft Sentinel solutions and configure your data connectors. Microsoft Sentinel provides a wide range of built-in solutions and data connectors, but you can also build custom connectors and set up connectors to ingest CEF or Syslog logs.

For more information, see:

- [Configure content](/azure/sentinel/configure-content)

- [Discover and manage Microsoft Sentinel out-of-the-box content](/azure/sentinel/sentinel-solutions-deploy?tabs=azure-portal)

- [Find your data connector](/azure/sentinel/data-connectors-reference)

### Enable User and Entity Behavior Analytics (UEBA)

After setting up data connectors in Microsoft Sentinel, make sure to enable user entity behavior analytics to identify suspicious behavior that could lead to phishing exploits and eventually attacks such as ransomware. For more information, see [Enable UEBA in Microsoft Sentinel](/azure/sentinel/enable-entity-behavior-analytics?tabs=azure).

### Set up interactive and long-term data retention

Set up interactive and long-term data retention to make sure your organization retains the data that's important in the long term. For more information, see [Configure interactive and long-term data retention](/azure/sentinel/configure-data-retention-archive).

### Enable analytics rules

Analytics rules tell Microsoft Sentinel to alert you to events using a set of conditions that you consider to be important. The out-of-the-box decisions Microsoft Sentinel makes are based on user entity behavioral analytics (UEBA) and on correlations of data across multiple data sources. When turning on analytic rules for Microsoft Sentinel, prioritize enabling by connected data sources, organizational risk, and MITRE tactic.

For more information, see [Threat detection in Microsoft Sentinel](/azure/sentinel/threat-detection).

### Review anomaly rules

Microsoft Sentinel anomaly rules are available out-of-the-box and enabled by default. Anomaly rules are based on machine learning models and UEBA that train on the data in your workspace to flag anomalous behavior across users, hosts, and others. Review the anomaly rules and anomaly score threshold for each one. If you're observing false positives for example, consider duplicating the rule and modifying the threshold.

For more information, see [Work with anomaly detection analytics rules](/azure/sentinel/work-with-anomaly-rules#tune-anomaly-rules).

### Use the Microsoft Threat Intelligence analytics rule

Enable the out-of-the-box Microsoft Threat Intelligence analytics rule and verify that [this rule matches your log data with Microsoft-generated threat intelligence](/azure/sentinel/understand-threat-intelligence#detect-threats-with-threat-indicator-analytics). Microsoft has a vast repository of threat intelligence data, and this analytic rule uses a subset of it to generate high fidelity alerts and incidents for SOC (security operations centers) teams to triage.

### Avoid duplicate incidents

After you [connect Microsoft Sentinel to Microsoft Defender](microsoft-sentinel-onboard.md), a bi-directional sync between Microsoft Defender XDR incidents and Microsoft Sentinel is automatically established. To avoid creating duplicate incidents for the same alerts, we recommend that you turn off all Microsoft incident creation rules for Microsoft Defender XDR-integrated products, including Defender for Endpoint, Defender for Identity, Defender for Office 365, Defender for Cloud Apps, and Microsoft Entra ID Protection.

For more information, see [Microsoft incident creation ](/azure/sentinel/microsoft-365-defender-sentinel-integration?tabs=azure-portal).

### Conduct a MITRE ATT&CK crosswalk

With fusion, anomaly, and threat intelligence analytic rules enabled, conduct a MITRE Att&ck crosswalk to help you decide which remaining analytic rules to enable and to finish implementing a mature XDR (extended detection and response) process. This empowers you to detect and respond throughout the lifecycle of an attack.

For more information, see [Understand security coverage](/azure/sentinel/mitre-coverage).


# Microsoft Sentinel Onboard

# Connect Microsoft Sentinel to the Microsoft Defender portal

Microsoft Sentinel is generally available in the Microsoft Defender portal, with or without Microsoft Defender XDR or an E5 license. Using Microsoft Sentinel in the Defender portal together with Microsoft Defender XDR services, you unify capabilities like incident management and advanced hunting. Reduce tool switching and build a more context-focused investigation that expedites incident response and stops breaches faster.

This article is relevant for customers whose Microsoft Sentinel workspaces are not yet connected to the Defender portal. In many cases, customers onboarding to Microsoft Sentinel after **July 1, 2025** are automatically onboarded to the Defender portal.

For more information, see:

- [What are unified security operations?](overview-unified-security.md)

- [Microsoft Sentinel in the Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2263690)

- [Microsoft Defender XDR integration with Microsoft Sentinel](/azure/sentinel/microsoft-365-defender-sentinel-integration)

## Prerequisites

Before you begin, review the feature documentation to understand the product changes and limitations.

- [Microsoft Sentinel in the Microsoft Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal)

- [Advanced hunting in the Microsoft Defender portal](/defender-xdr/advanced-hunting-microsoft-defender)

- [Alerts, incidents, and correlation in Microsoft Defender XDR](/defender-xdr/alerts-incidents-correlation)

- [Microsoft Sentinel automation in the Defender portal](/azure/sentinel/automation#automation-with-the-unified-security-operations-platform)

The Microsoft Defender portal supports a single Microsoft Entra tenant and the connection to a primary workspace and multiple secondary workspaces. If you have only one workspace when you onboard Microsoft Sentinel, that workspace is designated as the primary workspace. For more information, see [Multiple Microsoft Sentinel workspaces in the Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2310579). In the context of this article, a workspace is a Log Analytics workspace with Microsoft Sentinel enabled.

### Microsoft Sentinel prerequisites

To onboard and use Microsoft Sentinel in the Defender portal for a single workspace, you need the following resources and access:

- A Log Analytics workspace that has Microsoft Sentinel enabled

- An Azure account with the appropriate roles to onboard, use, and create support requests for Microsoft Sentinel in the Defender portal. You won't see workspaces in the Defender portal to onboard where you don't have the required permissions.

The following table shows some of the key roles needed for a single workspace setup. For permissions related to multiple workspaces, see [Permissions to manage workspaces and view workspace data](/azure/sentinel/workspaces-defender-portal#permissions-to-manage-workspaces-and-view-workspace-data).

For onboarding, the [Owner](/azure/role-based-access-control/built-in-roles#owner) role assignment must be unconditional at the subscription scope.

|Task |Microsoft Entra or Azure built-in role required |Scope  |

|---------|---------|---------|

|**Onboard Microsoft Sentinel to the Defender portal**<sup>1</sup>|  At least a [Security Administrator](/entra/identity/role-based-access-control/permissions-reference#security-administrator) in Microsoft Entra ID <br><br> [Owner](/azure/role-based-access-control/built-in-roles#owner) (unconditional role assignment)<br> OR <br>[User Access Administrator](/azure/role-based-access-control/built-in-roles#user-access-administrator) and [Microsoft Sentinel Contributor](/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) |Tenant<br><br><br>- Subscription for Owner role|

|**View Microsoft Sentinel in the Defender portal**|[Microsoft Sentinel Reader](/azure/role-based-access-control/built-in-roles#microsoft-sentinel-reader) |Subscription, resource group, or workspace resource  |

|**Query Microsoft Sentinel data tables or view incidents**  |[Microsoft Sentinel Reader](/azure/role-based-access-control/built-in-roles#microsoft-sentinel-reader) or a role with the following actions:</br>- Microsoft.OperationalInsights/workspaces/read</br>- Microsoft.OperationalInsights/workspaces/query/read</br>- Microsoft.SecurityInsights/Incidents/read</br>- Microsoft.SecurityInsights/incidents/comments/read</br>- Microsoft.SecurityInsights/incidents/relations/read</br>- Microsoft.SecurityInsights/incidents/tasks/read|Subscription, resource group, or workspace resource       |

|**Take investigative actions on incidents** |[Microsoft Sentinel Contributor](/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) or a role with the following actions:</br>- Microsoft.OperationalInsights/workspaces/read</br>- Microsoft.OperationalInsights/workspaces/query/read</br>- Microsoft.SecurityInsights/incidents/read</br>- Microsoft.SecurityInsights/incidents/write</br>- Microsoft.SecurityInsights/incidents/comments/read</br>- Microsoft.SecurityInsights/incidents/comments/write</br>- Microsoft.SecurityInsights/incidents/relations/read</br>- Microsoft.SecurityInsights/incidents/relations/write</br>- Microsoft.SecurityInsights/incidents/tasks/read</br>- Microsoft.SecurityInsights/incidents/tasks/write    |Subscription, resource group, or workspace resource  |

|**Create a support request** |[Owner](/azure/role-based-access-control/built-in-roles#owner) or </br> [Contributor](/azure/role-based-access-control/built-in-roles#contributor) or </br> [Support request contributor](/azure/role-based-access-control/built-in-roles#support-request-contributor) or  a custom role with Microsoft.Support/*|Subscription  |

<sup>1</sup> If your tenant has exactly one workspace with Microsoft Sentinel enabled, use the permissions listed in the table. If your tenant has [more than one workspace with Microsoft Sentinel enabled](/azure/sentinel/workspaces-defender-portal#permissions-to-manage-workspaces-and-view-workspace-data), you must also be at least a [Security administrator](/entra/identity/role-based-access-control/permissions-reference#security-administrator) in Microsoft Entra ID.

If you're working with multiple tenants, note that [granular delegated admin privileges (GDAP)](/partner-center/gdap-introduction) with [Azure Lighthouse](/azure/sentinel/multiple-tenants-service-providers) isn't supported for Microsoft Sentinel data in the Defender portal. Instead, use [Microsoft Entra B2B authentication](/entra/external-id/what-is-b2b). For more information, see [Set up Microsoft Defender multitenant management](mto-requirements.md#review-the-requirements).

After you connect Microsoft Sentinel to the Defender portal, your existing Azure role-based access control (RBAC) permissions allow you to work with the Microsoft Sentinel features that you have access to. Continue to manage roles and permissions for your Microsoft Sentinel users from the Azure portal, as any Azure RBAC changes are reflected in the Defender portal.

For more information, see [Roles and permissions in Microsoft Sentinel](/azure/sentinel/roles) and [Manage access to Microsoft Sentinel data by resource](/azure/sentinel/resource-context-rbac).

> [!IMPORTANT]

> Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization.

### Unified security operations prerequisites

To unify Microsoft Defender XDR and Microsoft Sentinel security operations in the Defender portal, you must have the following resources and access:

- Licensing for Defender XDR, as described in [Microsoft Defender XDR prerequisites](/microsoft-365/security/mtp/prerequisites)

- Account for Defender XDR is a member of the same Microsoft Entra tenant with which Microsoft Sentinel is associated

- Access to Microsoft Defender XDR in the Defender portal, as described in [Microsoft Defender XDR prerequisites](/microsoft-365/security/mtp/prerequisites#required-permissions)

If applicable, complete these prerequisites:

|Service  |Prerequisite  |

|---------|---------|

|**Microsoft Purview Insider Risk Management**    |  If your organization uses Microsoft Purview Insider Risk Management, integrate that data by enabling the data connector **Microsoft 365 Insider Risk Management** on your primary workspace for Microsoft Sentinel. Disable that connector on any secondary workspaces for Microsoft Sentinel that you plan to onboard to the Defender portal. <br><br>- Install the **Microsoft Purview Insider Risk Management** solution from the **Content hub** on the primary workspace.<br>- Configure the data connector. <br><br>For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](/azure/sentinel/sentinel-solutions-deploy).        |

|**Microsoft Defender for Cloud**     | To stream Defender for Cloud incidents that are correlated across all subscriptions of the tenant to the primary workspace for Microsoft Sentinel: <br><br>-  Connect the **Tenant-based Microsoft Defender for Cloud (Preview)** data connector in the primary workspace.<br>  - Disconnect the **Subscription-based Microsoft Defender for Cloud (Legacy)** alerts connector from all workspaces in the tenant. <br><br>If you don't want to stream correlated tenant data for Defender for Cloud to the primary workspace, continue to use the **Subscription-based Microsoft Defender for Cloud (Legacy)** connector on your workspaces. For more information, see [Ingest Microsoft Defender for Cloud incidents with Microsoft Defender XDR integration](/azure/sentinel/ingest-defender-for-cloud-incidents).        |

## Onboard Microsoft Sentinel

This procedure describes how to onboard a Microsoft Sentinel-enabled workspace to the Defender portal.

1. Go to the [Microsoft Defender portal](https://security.microsoft.com/) and sign in.

1. Select **System** > **Settings** > **Microsoft Sentinel** > **Connect a workspace**.

1. Select the workspaces you want to connect and select **Next**.

1. Select the **Primary workspace**.

1. Read and understand the product changes associated with connecting your workspace.

1. Select **Connect**.

After your workspace is connected, the banner on the **Home** page shows that your environment is ready. The **Home** page is updated with new sections that include metrics from Microsoft Sentinel, like the number of data connectors and automation rules.

## Explore Microsoft Sentinel features in the Defender portal

After you connect your workspace to the Defender portal, **Microsoft Sentinel** is on the left-hand side navigation pane. If you have Defender XDR enabled, pages like  **Home**, **Incidents**, and **Advanced Hunting** have unified data from the primary workspace for Microsoft Sentinel and Defender XDR. If you don't have Defender XDR enabled, these pages just include data from Microsoft Sentinel. For more information about the unified capabilities and differences between portals, see  [Microsoft Sentinel in the Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2263690).

Many of the existing Microsoft Sentinel features are integrated into the Defender portal. For these features, notice that the experience between Microsoft Sentinel in the Azure portal and Defender portal are similar. Use the following articles to help you start working with Microsoft Sentinel in the Defender portal. When using these articles, keep in mind that your starting point in this context is the [Defender portal](https://security.microsoft.com/) instead of the Azure portal.

| Feature category   | Links |

|--------------------|----------|

| **Search**         | - [Search across long time spans in large datasets](/azure/sentinel/search-jobs?tabs=defender-portal)<br>- [Restore archived logs from search](/azure/sentinel/restore) |

| **Threat management** | - [Visualize and monitor your data by using workbooks](/azure/sentinel/monitor-your-data?tabs=defender-portal)<br>- [Conduct end-to-end threat hunting with Hunts](/azure/sentinel/hunts)<br>- [Use hunting bookmarks for data investigations](/azure/sentinel/bookmarks)<br>- [Use hunting Livestream in Microsoft Sentinel to detect threat](/azure/sentinel/livestream)<br>- [Hunt for security threats with Jupyter notebooks](/azure/sentinel/notebooks-hunt)<br>- [Add indicators in bulk to Microsoft Sentinel threat intelligence from a CSV or JSON file](/azure/sentinel/indicators-bulk-file-import?tabs=defender-portal)<br>- [Work with threat indicators in Microsoft Sentinel](/azure/sentinel/work-with-threat-indicators?tabs=defender-portal)<br>- [Understand security coverage by the MITRE ATT&CK framework](/azure/sentinel/mitre-coverage) |

| **Content management** | - [Discover and manage Microsoft Sentinel out-of-the-box content](/azure/sentinel/sentinel-solutions-deploy?tabs=defender-portal)<br>- [Microsoft Sentinel content hub catalog](/azure/sentinel/sentinel-solutions-catalog)<br>- [Deploy custom content from your repository](/azure/sentinel/ci-cd) |

| **Configuration**  | - [Find your Microsoft Sentinel data connector](/azure/sentinel/data-connectors-reference)<br>- [Create custom analytics rules to detect threats](/azure/sentinel/create-analytics-rules?tabs=defender-portal)<br>- [Work with near-real-time (NRT) detection analytics rules in Microsoft Sentinel](/azure/sentinel/create-nrt-rules?tabs=defender-portal)<br>- [Create watchlists](/azure/sentinel/watchlists-create?tabs=defender-portal)<br>- [Manage watchlists in Microsoft Sentinel](/azure/sentinel/watchlists-manage)<br>- [Create automation rules](/azure/sentinel/create-manage-use-automation-rules)<br>- [Create and customize Microsoft Sentinel playbooks from content templates](/azure/sentinel/use-playbook-templates) |

Find Microsoft Sentinel settings in the Defender portal under **System** > **Settings** > **Microsoft Sentinel**.

## Change the primary workspace

You can only have one primary workspace connected to the Defender portal at a time. But you can change the primary workspace.

1. In the [Defender portal](https://security.microsoft.com/), go to **System** > **Settings** > **Microsoft Sentinel** > **Workspaces**.

1. Select the name of the workspace that you want to make primary.

1. Select **Set as primary**.

1. Read and understand the product changes associated with changing the primary workspace.

1. Select **Confirm and proceed**.

When you switch the primary workspace for Microsoft Sentinel, the Defender XDR connector is connected to the new primary and disconnected from the former one automatically. For more information, see [Multiple Microsoft Sentinel workspaces in the Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2310579).

## Offboard Microsoft Sentinel

If you decide to offboard a workspace from the Defender portal, disconnect the workspace from the settings for Microsoft Sentinel.

If your workspace has the [Microsoft Defender XDR connector](/azure/sentinel/connect-microsoft-365-defender) configured, offboarding the workspace from the Defender portal will also disconnect the Microsoft Defender XDR connector.

1. Go to the [Microsoft Defender portal](https://security.microsoft.com/) and sign in.

1. In the Defender portal, under **System**, select **Settings** > **Microsoft Sentinel**.

1. On the **Workspaces** page, select the connected workspace and **Disconnect workspace**.

1. Provide a reason why you're disconnecting the workspace.

1. Confirm your selection.

When your workspace is disconnected, the **Microsoft Sentinel** section is removed from the left-hand side navigation of the Defender portal. Data from Microsoft Sentinel is no longer included on the **Home** page.

If you want to connect to a different workspace, from the **Workspaces** page, select the workspace and **Connect a workspace**.

## Related content

- [Microsoft Sentinel in the Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2263690)

- [Advanced hunting in the Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2264410)

- [Automatic attack disruption in Microsoft Defender XDR](/defender-xdr/automatic-attack-disruption)

- [Investigate incidents in Microsoft Defender portal](/defender-xdr/investigate-incidents)

- [Optimize your security operations](/azure/sentinel/soc-optimization/soc-optimization-access?tabs=defender-portal)


# Reduce Risk Overview

# Improve security posture management and reduce risk

Security teams need a comprehensive strategy to reduce vulnerabilities, prevent breaches, and mitigate threats in real time.

The Microsoft Defender portal provides a set of integrated tools and solutions that work together to help security teams proactively reduce security risk.

Proactive security management allows you to manage cybersecurity as an ongoing risk, rather than series of unpredictable events. Proactive risk management helps to reduce the likelihood of breaches, minimize business disruptions when attacks do occur, and raise security awareness as an ongoing practice across the business.

## Improve prebreach security

Security teams must address key activities for effective prebreach security.

Activity | Details

--- | ---

**Protect assets and workloads** | Teams must be able to improve posture across all types of corporate resources, including devices, identities, apps, and cloud workloads from code to runtime.

**Discover the digital estate** | Discovering organizational assets in the first step in understanding security posture. Centralizing assets into a single inventory provides unified and broad visibility across company silos.

**Understand asset connections** | In addition to continuously discovering and tracking assets, security teams must be able to visualize and understand complex connections and interactions between discovered resources.

**Aggregate asset data** | Collecting data and correlating signals from multiple sources to arrive at a single accurate contextual representation of each digital asset helps security teams to understand and uncover security gaps and weaknesses, including potential attack paths.

**Get security insights** | Security teams need the ability to investigate and query security findings to understand misconfigurations and security posture drift as risks change. Over time, insights help security teams to answer questions such as - How secure are we right now? How are we doing over time? Where do we stand on mitigation? What areas are weakest? Are we protected against the latest threats?

**Adhere to compliance standards** | Compliance standards provide structured, well-known guidelines around security controls and measures. Proactive and ongoing security posture management ensures that your organization meets compliance requirements.

**Remediate security** | Prioritizing asset remediation by focusing on critical resources helps focus team effort by reducing security gaps and attack surfaces in the most important areas of the business.

**Measure progress** | Security posture improvement and attack surface reduction are ongoing activities. Consistent measurement of how you're doing over time helps to ensure that you reach security targets and maintain compliance in your most critical security initiatives.

**Continuously improve** |  Use security posture management to provide fast and continuous feedback to risk management frameworks and SOC teams.

## Microsoft solutions

A range of solutions in the Microsoft Defender portal help security teams to proactively improve security posture.

Solution | Details | Capabilities

--- | --- | ---

**[Microsoft Security Exposure Management](/security-exposure-management/microsoft-security-exposure-management)**<br/><br/>Reduce security risk by reducing attack surfaces. | Automatically discover assets, including devices, identities, cloud apps, and more. Extend visibility to non-Microsoft solutions.<br/><br/>Organize data into security initiatives to monitor, track, measure, and prioritize posture in the areas that are most important to you.<br/><br/>Discover and visualize attack surfaces and potential blast radius.<br/><br/>[Get contextual insights to understand, prioritize, and mitigate security risk.](overview-msem-strategy.md)

**[Microsoft Defender for Cloud](/azure/defender-for-cloud/defender-for-cloud-introduction)**<br/><br/>Detect real-time threats to cloud workloads, and proactively improve security posture. | Cloud security posture management capabilities assess the posture of resources across Azure, AWS, GCP, and on-premises. Defender for Cloud improves security posture for machines, containers, sensitive data, databases, AI workloads, storage, and DevOps.<br/><br/>Security recommendations provide information and manual/automatic actions to remediate issues and harden resource security.

**[Microsoft Defender for Endpoint](/defender-endpoint/microsoft-defender-endpoint)**<br/><br/>Improve security posture and protect against threats. | Defender for Endpoint includes a number of security posture management features.<br/><br/>[Attack surface reduction](/defender-endpoint/overview-attack-surface-reduction) proactively blocks common activities associated with malicious actions, and provides [attack surface reduction rules](/defender-endpoint/attack-surface-reduction) to constrain risky software-based behavior.<br/><br/>Other features include [controlled folder access](/defender-endpoint/controlled-folders), [peripheral device control](/defender-endpoint/device-control-overview), [exploit protection](/defender-endpoint/exploit-protection), [network](/defender-endpoint/network-protection) and [web](/defender-endpoint/network-protection) protection.

**[Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management)**<br/><br/>Remediate security vulnerabilities across the organization. | Defender Vulnerability Management continuously identifies vulnerabilities and misconfigurations, providing contextual insights into potential threats and recommendations to mitigate them.

**[Microsoft Secure Score](/defender-xdr/microsoft-secure-score)**<br/><br/>Measure organizational security posture. | Secure Score helps to monitor the security posture of Microsoft 365 workloads, including devices, identities, and apps. [Compare Security Score with security posture in Security Exposure Management](/security-exposure-management/compare-secure-score-security-exposure-management).


# Overview Msem Strategy

# Microsoft Security Exposure Management for enhanced security posture

Security posture refers to an organization’s strength of protection over its networks, data, and systems (hardware and software). It measures how vulnerable your organization is to cyber-attacks or data breaches.

The cyber landscape is becoming more perilous with increasing threat actors, faster phishing attacks, and more password attacks. Cyber jobs are harder due to regulatory updates, numerous security tools, and open jobs. Organizations face exposure with critical assets and open attack paths.

Microsoft Security Exposure Management transforms the attack surface by providing tools to discover, assess, and reduce risk with confidence. It integrates with various Microsoft Defender products and offers a unified view of internal and external exposure, potential attack paths, and critical asset protection.

Proactively protecting your organization from potential data breaches is more effective than just doing damage control once a breach occurs.

## Scoping - Make a plan

A well-defined plan is essential for effective exposure management. Your plan should outline the purpose and objectives of posture management for your organization, aligning with legal and regulatory requirements and the risks to your organization's goals. Identify internal stakeholders and important external parties and establish clear roles and responsibilities.

## Discovery - Find vulnerabilities

The **Discovery** step identifies vulnerabilities within your infrastructure. This involves scanning networks, systems, and applications for potential weaknesses. By regularly conducting vulnerability assessments, you can stay ahead of emerging threats and ensure your security posture remains strong.

We recommend that you maintain an up-to-date inventory of your assets, including on-premises resources, cloud resources, and endpoints. Work with security governance teams to ensure assets are properly tagged and inventories are current. This helps incident responders quickly identify and address security issues.

## Education and training

Security posture management is a complex topic that requires a wide range of technical knowledge. Continuously educate and train your operations and incident response staff on Exposure Management technologies and how your organization uses them. This ensures your team is prepared to handle security incidents effectively.

The evolution of vulnerability management includes TI-Based, Risk-Based, and Exposure Management stages. Continuous exposure management involves attack surface management, attack path analysis, and unified exposure insights. Microsoft integrates exposure management data across Defender products to enhance security posture.

**Incident classification framework**

Define what constitutes a "security incident" for your organization and develop a method for classifying incidents. A classification framework helps prioritize response and preparation activities, collect useful metrics, and improve the performance of your posture management program. Categories might include denial of service, malware, or unauthorized access, with impact-based severity levels such as critical, high, medium, or low.

## Assess your security posture

Use Exposure Management to get a comprehensive view of your organization's security posture, including key metrics, critical assets, and potential vulnerabilities. Exposure Management provides a 360-degree view of your security landscape, helping you understand and quantify your attack surface exposure.

Learn more here, [What is Microsoft Security Exposure Management?](/security-exposure-management/microsoft-security-exposure-management)

## Identify attack entry points

Exposure Management helps you identify and map out potential attack paths, giving you visibility into critical choke points that need to be addressed. This proactive approach allows you to close down attack paths before they can be exploited.

80% of organizations have at least one open attack path to a critical asset. 61% of attack paths lead to sensitive user accounts. Only 1% of total assets in organizations are critical or sensitive.

Learn more here, [Overview of attack surface management](/security-exposure-management/cross-workload-attack-surfaces)

## Prioritize remediation efforts

Focus on the most critical vulnerabilities and attack paths first. Exposure Management provides recommendations for remediation actions to help you prioritize your efforts. This ensures that your resources are used effectively to mitigate the most significant risks.

Learn more here, [Review security recommendations](/security-exposure-management/security-recommendations)

## Validation – Test and confirm fixes

Incorporate the **Validation** step to test and confirm that remediation efforts effectively address identified vulnerabilities. This involves conducting penetration tests and security audits to ensure that vulnerabilities are properly mitigated and that the fixes are effective.

## Key considerations for users

For users new to Exposure Management, it's important to understand the following benefits:

- **Comprehensive view**: Exposure Management provides a 360-degree view of your organization's security posture, helping you understand the overall security landscape.

- **Prioritization**: Focus on the most critical vulnerabilities and attack paths first to maximize the impact of your remediation efforts.

- **Continuous monitoring**: Exposure Management continuously monitors your threat exposure and provides updates on your security posture.

For users with an established posture program, consider the following advanced features:

- **Integration**: Exposure Management integrates with existing security tools and solutions, providing a unified view of your security posture.

- **Advanced metrics**: Utilize advanced security metrics and insights provided by Exposure Management to fine-tune your security strategies.

- **Collaboration**: Work with different teams within your organization to ensure a coordinated approach to exposure management.

A great starting point for any user is to set a specific goal. For instance, you might choose to enhance Ransomware Protection initiative by 20%. Use Exposure Management metrics and recommendations to identify and mitigate vulnerabilities that could be exploited by ransomware attacks to achieve this improvement.

## Ensuring your security posture

Maintaining a robust security posture is essential for safeguarding your organization's networks, data, and systems against cyber threats. By using tools like Exposure Management, you can gain a comprehensive view of your security landscape, identify critical vulnerabilities, and prioritize remediation efforts effectively. Continuous monitoring and proactive measures are key to staying ahead of potential threats and ensuring that your security posture remains strong. Following the guidelines outlined here and fostering a culture of security awareness, your organization can better protect itself from cyber-attacks and data breaches, building trust with customers and stakeholders.


# Detect Threats Overview

# Threat detection in the Microsoft Defender portal

Cybersecurity threats abound in the current technology landscape. A lot of noise is created by the constant specter of breach and an abundance of signals available to security operation centers. The Defender portal separates actionable threats from the noise, where each service adds its own finely tuned detections to match the complexion of the solution it provides and puts it all together into a single dashboard. The Microsoft Defender portal pulls detections together in the form of alerts and incidents from Microsoft Defender XDR, Microsoft Sentinel, and Microsoft Defender for Cloud.

Security teams also need focus and clarity to eliminate false positives. The Microsoft Defender portal correlates and merges alerts and incidents from all supported Microsoft security and compliance solutions, and unifies threat detection from external solutions through Microsoft Sentinel and Microsoft Defender for Cloud. The correlation and merging of these signals brings rich context and prioritization. For example, an Adversary-in-The-Middle (AiTM) phishing attack might have pieces of the threat puzzle scattered across multiple sources. The Defender portal puts those pieces together into an attack story while providing attack disrupt and guided response to remediate the threat.

The following image shows the incidents dashboard correlating signals from multiple services, including the individual detection sources for a complete AiTM attack story.

Each supported Microsoft security product enabled unlocks more signals to stream into the Defender portal. For more information on how these signals are stitched together and prioritized, see [Incidents and alerts in the Microsoft Defender portal](/defender-xdr/incidents-overview).

## Microsoft Defender XDR threat detection

Defender XDR has a unique correlation capability that provides an extra layer of data analysis and threat detection. The following table gives examples of how supported security services are tuned to detect threats matching the character of its solution.

| Defender XDR service | Threat detection specialty |

|---|---|

| [**Microsoft Defender for Endpoint**](/defender-endpoint/microsoft-defender-endpoint) | Microsoft Defender antivirus detects polymorphic malware with behavior-based and heuristic analytics on endpoints such as mobile devices, desktops, and more.|

| [**Microsoft Defender for Office 365**](/defender-office-365/mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet) | Detects phishing, malware, weaponized links and more in email, Teams, and OneDrive.|

| [**Microsoft Defender for Identity**](/defender-for-identity/what-is) | Detects privilege escalation, lateral movement, discovery, defense evasion, persistence, and more across both on-premises and cloud identities.|

| [**Microsoft Defender for Cloud Apps**](/defender-cloud-apps/what-is-defender-for-cloud-apps) | Detects suspicious activities through user and entity behavioral analytics (UEBA) across cloud applications.|

| [**Microsoft Defender Vulnerability Management**](/defender-vulnerability-management/defender-vulnerability-management) | Detects vulnerabilities in devices providing meaningful context for investigations.|

| [**Microsoft Entra ID Protection**](/azure/active-directory/identity-protection/overview-identity-protection) | Detects risks associated with sign-ins like impossible travel, verified threat actor IPs, leaked credentials, password sprays and more.|

| [**Microsoft Data Loss Prevention**](/microsoft-365/compliance/dlp-learn-about-dlp) | Detects risks and behavior associated with oversharing and exfiltration of sensitive information across Microsoft 365 services, Office applications, endpoints, and more.|

For more information, see [What is Microsoft Defender XDR?](/defender-xdr/microsoft-365-defender)

## Microsoft Sentinel threat detection

Microsoft Sentinel connected to the Defender portal enables data collection from a vast number of Microsoft and non-Microsoft sources, but doesn't stop there. With Microsoft Sentinel's threat management capabilities, you gain the tools needed to detect and organize threats to your environment.

| Threat management feature | Detection capability | For more information |

|---|---|---|

| MITRE ATT&CK coverage | Organize your threat detection coverage and understand gaps. | [Understand security coverage by the MITRE ATT&CK® framework](/azure/sentinel/mitre-coverage) |

| Analytics | Rules constantly dig through your data to generate alerts and incidents and integrates those signals in the Defender portal. | [Detect threats out-of-the-box](/azure/sentinel/threat-detection) |

| Watchlists | Curate meaningful relationships in your environment to improve the quality and prioritization of detections. | [Watchlists in Microsoft Sentinel](/azure/sentinel/watchlists) |

| Workbooks | Detect threats with visual insights, especially to monitor the health of your data collection and understand gaps that prevent proper threat detection. | [Visualize your data with workbooks](/azure/sentinel/monitor-your-data?tabs=defender-portal) |

| Summary rules | Optimizes noisy, high volume logs to detect threat in low-security value data. | [Generate alerts on threat intelligence matches against network data](/azure/sentinel/summary-rules#generate-alerts-on-threat-intelligence-matches-against-network-data) |

For more information, see [Connect Microsoft Sentinel to the Microsoft Defender portal](microsoft-sentinel-onboard.md).

## Microsoft Defender for Cloud threat detection

Defender for Cloud provides threat detection to generate alerts and incidents by continuously monitoring your clouds' assets with advanced security analytics. Those signals are integrated directly into the Defender portal for correlation and severity classification. Each plan enabled in Defender for Cloud adds to the detection signals streamed into Defender portal. For more information, see [Alerts and incidents in Microsoft Defender XDR](/azure/defender-for-cloud/concept-integration-365).

Defender for Cloud detects threats across a wide variety of workloads. The following table gives examples of some of the threats it detects. For more information on specific alerts, see [Security alerts reference list](/azure/defender-for-cloud/alerts-reference).

| Defender for Cloud plan | Threat detection specialty |

|---|---|

| [Defender for Servers](/azure/defender-for-cloud/tutorial-enable-servers-plan) | Detects threats for Linux and Windows based on antimalware failures, fileless attacks, crypto mining and ransomware attacks, brute force attacks and many more. |

| [Defender for Storage](/azure/defender-for-cloud/tutorial-enable-storage-plan) | Detects phishing content and malware distribution, suspicious access and discovery, unusual data extraction and more. |

| [Defender for Containers](/azure/defender-for-cloud/tutorial-enable-containers-azure) | Detects threats at the control plane and workload runtime for risky exposure, malicious or crypto mining activity, web shell activity, custom simulations and more. |

| [Defender for Databases](/azure/defender-for-cloud/tutorial-enable-databases-plan) | Detects SQL injection, fuzzing, unusual access, brute force attempts and more.  |

| [Defender for APIs](/azure/defender-for-cloud/defender-for-apis-introduction) | Detects suspicious spikes in traffic, access from malicious IPs, discovery and enumeration techniques of API endpoints and more. |

| [AI threat protection](/azure/defender-for-cloud/ai-threat-protection) | Detects threats across generative AI applications for jailbreak attempts, sensitive data exposure, corrupted AI and more. |

For more information, see [Security alerts and incidents](/azure/defender-for-cloud/alerts-overview).

## Related content

- [Protect assets](overview-unified-security.md#protect-assets)

- [Microsoft Defender for Cloud integration with Microsoft Defender XDR](/azure/defender-for-cloud/concept-integration-365)

- [Microsoft Sentinel integration with Microsoft Defender XDR](/azure/sentinel/microsoft-365-defender-sentinel-integration)


# Threat Intelligence Overview

# Uncover adversaries with threat intelligence across the Defender portal

Uncover and neutralize modern adversaries with threat intelligence in the Microsoft Defender portal. Whether you use Microsoft's threat intelligence or other sources important to your security operations team, **Threat intelligence** in the Microsoft Defender portal unifies the tools needed to identify cyberattackers and their infrastructure.

_Threat intelligence in the Defender portal_

The emergence of new cybersecurity threats and threat actors and the continuous evolution of the threat landscape result in an ever-increasing amount of threat intelligence that security operations centers (SOCs) must investigate. This threat intelligence takes many forms—from specific indicators of compromise (IOCs) to reports and analyses—and can come from various sources. The Microsoft Defender portal consolidates all your threat intelligence in one location so SOCs can assess this intelligence quickly and accurately to make informed decisions. The Defender portal pulls threat intelligence from the following sources:

- Microsoft Defender XDR Threat analytics reports

- Microsoft Defender Threat Intelligence articles and data sets

- Microsoft Sentinel threat intelligence

## Threat analytics in Microsoft Defender XDR

**Threat analytics** is the [Microsoft Defender XDR](/defender-xdr/microsoft-365-defender) in-product threat intelligence solution from expert Microsoft security researchers. It's designed to assist security teams to be as efficient as possible while facing emerging threats, such as:

- Active threat actors and their campaigns

- Popular and new attack techniques

- Critical vulnerabilities

- Common attack surfaces

- Prevalent malware

_Analyst report section of a threat analytics report_

Each report provides an analysis of a tracked threat and extensive guidance on how to defend against that threat. It also incorporates data from your network, indicating whether the threat is active and if you have applicable protections in place.

For more information, see [Threat analytics in Microsoft Defender XDR](/defender-xdr/threat-analytics).

## Microsoft Defender Threat Intelligence

**Microsoft Defender Threat Intelligence** (Defender TI) helps streamline security analyst triage, incident response, threat hunting, and vulnerability management workflows. Defender TI aggregates and enriches critical threat information in an easy-to-use interface where users can correlate IOCs with related articles, actor profiles, and vulnerabilities. Defender TI also lets analysts collaborate with fellow Defender TI-licensed users within their tenant on investigations.

You can access Defender TI in the following pages within the **Threat intelligence** navigation menu of the Defender portal:

- **Intel profiles** - Access a comprehensive library of threat actor, tooling, and vulnerability profiles.

- **Intel explorer** - Browse threat intelligence for relevant analyses, artifacts, and indicators.

- **Intel projects** - Manage security artifacts for your entire tenant.

_Defender TI's **Intel explorer** page in the Defender portal_

For more information, see [What is Microsoft Defender Threat Intelligence?](/defender/threat-intelligence/what-is-microsoft-defender-threat-intelligence-defender-ti).

## Threat intelligence management

**Intel management** is powered by [Microsoft Sentinel](/azure/sentinel/overview) and provides tools to update, search, and create threat intelligence and manage it at scale.

The most common forms of threat intelligence are threat indicators, or IOCs. Another facet of threat intelligence represents threat actors, their techniques, tactics, and procedures (TTPs), their infrastructure, and their victims. Intel management supports managing all these facets using structured threat information expression (STIX), the open-source standard for exchanging threat intelligence.

Intel management operationalizes your threat intelligence while Microsoft Sentinel sources it with the following methods of ingestion:

- **Import threat intelligence** into Microsoft Sentinel by enabling data connectors to various threat intelligence platforms, including Microsoft’s own Defender TI.

- **Connect threat intelligence** to Microsoft Sentinel by using the upload API to connect various threat intelligence platforms or custom applications.

- **Create threat intelligence** individually or import using a file from the Intel management interface.

_Example of adding a new STIX object in Intel management_

For more information, see [Understand threat intelligence in Microsoft Sentinel](/azure/sentinel/understand-threat-intelligence).

## Related content

- [Microsoft Defender XDR integration with Microsoft Sentinel](/azure/sentinel/microsoft-365-defender-sentinel-integration)

- [Microsoft Security Copilot in Microsoft Defender Threat Intelligence](/defender/threat-intelligence/security-copilot-and-defender-threat-intelligence)

- [Infrastructure chaining](/defender/threat-intelligence/infrastructure-chaining)


# Hunting Overview

# Hunting in the Microsoft Defender portal

Hunting for security threats is a highly customizable activity that is most effective when accomplished across all stages of threat hunting: proactive, reactive, and post incident. The Defender portal provides effective hunting tools for every stage of threat hunting with unified security operations services. These tools are well fit for analysts who are just starting out in their career, or experienced threat hunters using advanced hunting methods. Threat hunters of all levels benefit from hunting tool features that allow them to share their techniques, queries, and findings with their team along the way.

## Hunting tools

The foundation of hunting queries in the Defender portal rests on Kusto Query Language (KQL). KQL is a powerful and flexible language that's optimized for searching through big-data stores in cloud environments. However, crafting complex queries isn't the only way to hunt for threats. Here are some more hunting tools and resources within the Defender portal designed to bring hunting into your reach:

- [**Security Copilot in advanced hunting**](/defender-xdr/advanced-hunting-security-copilot) generates KQL from natural language prompts.

- [**Guided hunting**](/defender-xdr/advanced-hunting-query-builder) uses a query builder for crafting meaningful hunting queries without knowing KQL or the data schema.

- [**Get help as you write queries**](/defender-xdr/advanced-hunting-query-language#get-help-as-you-write-queries) with features like autosuggest, schema tree, and sample queries.

- [**Content hub**](/azure/sentinel/sentinel-solutions-deploy?tabs=azure-portal#hunting-query) provides expert queries to match out-of-the-box solutions in Microsoft Sentinel.

- [**Microsoft Defender Experts for Hunting**](/defender-xdr/advanced-hunting-overview) compliments even the best threat hunters that want assistance.

Maximize the full extent of your team's hunting prowess with the following hunting tools in the Defender portal:

| Hunting tool | Description |

|---|---|

|[**Advanced hunting**](/defender-xdr/advanced-hunting-microsoft-defender) | View and query data sources available from Defender portal services and share queries with your team. Use all your existing Microsoft Sentinel workspace content, including queries and functions. |

|[**Microsoft Sentinel hunting**](/azure/sentinel/hunting) | Hunt for security threats across data sources. Use specialized search and query tools like **hunts**, **bookmarks** and **livestream**. |

|[**Go hunt**](/defender-xdr/advanced-hunting-go-hunt) | Quickly pivot an investigation to entities found within an incident. |

|[**Hunts**](/azure/sentinel/hunts) | An end-to-end, proactive threat hunting process with collaboration features. |

|[**Bookmarks**](/azure/sentinel/bookmarks) | Preserve queries and their results, adding notes and contextual observations.|

|[**Livestream**](/azure/sentinel/livestream) | Start an interactive hunting session and use any Log Analytics query. |

|[**Hunting with summary rules**](/azure/sentinel/summary-rules#quickly-find-a-malicious-ip-address-in-your-network-traffic) | Use summary rules to save costs hunting for threats in verbose logs.|

|[**MITRE ATT&CK map**](/azure/sentinel/mitre-coverage#use-the-mitre-attck-framework-in-analytics-rules-and-incidents) | When creating a new hunting query, select specific tactics and techniques to apply.|

|[**Restore historical data**](/azure/sentinel/restore) | Restore data from archived logs to use in high performing queries. |

|[**Search large data sets**](/azure/sentinel/search-jobs?tabs=defender-portal) | Search for specific events in logs up to seven years ago using KQL. |

|[**Infrastructure chaining**](/defender/threat-intelligence/infrastructure-chaining) | Hunt for new connections between threat actors, group similar attack activity and substantiate assumptions.|

|[**Threat explorer**](/defender-office-365/threat-explorer-threat-hunting) | Hunt for specialized threats related to email. |

## Hunting stages

The following table describes how you can make the most of the Defender portal's hunting tools across all stages of threat hunting:

| Hunting stage | Hunting tools |

| --- | --- |

| **Proactive** - Find the weak areas in your environment before threat actors do. Detect suspicious activity extra early. | - Regularly conduct end-to-end [hunts](/azure/sentinel/hunts) to proactively seek out undetected threats and malicious behaviors, validate hypotheses, and act on findings by creating new detections, incidents, or threat intelligence.<br><br> - Use the [MITRE ATT&CK map](/azure/sentinel/mitre-coverage#use-the-mitre-attck-framework-in-analytics-rules-and-incidents) to identify detection gaps, and then run predefined hunting queries for highlighted techniques.<br><br> - Insert new threat intelligence into proven queries to tune detections and confirm if a compromise is in process.<br><br> - Take proactive steps to build and test queries against data from new or updated sources.<br><br> - Use [advanced hunting](/defender-xdr/advanced-hunting-microsoft-defender) to find early-stage attacks or threats that don't have alerts. |

| **Reactive** - Use hunting tools during an active investigation. | - Use [livestream](/azure/sentinel/livestream) to run specific queries at consistent intervals to actively monitor events.<br><br> - Quickly pivot on incidents with the [**Go hunt**](/defender-xdr/advanced-hunting-go-hunt) button to search broadly for suspicious entities found during an investigation.<br><br> - Hunt through threat intelligence to perform [infrastructure chaining](/defender/threat-intelligence/infrastructure-chaining).<br><br> - Use [Security Copilot in advanced hunting](/defender-xdr/advanced-hunting-security-copilot) to generate queries at machine speed and scale. |

| **Post incident** - Improve coverage and insights to prevent similar incidents from recurring. | - Turn successful hunting queries into new [analytics and detection rules](/azure/sentinel/threat-detection), or refine existing ones.<br><br> - [Restore historical data](/azure/sentinel/restore) and [search large datasets](/azure/sentinel/search-jobs?tabs=defender-portal) for specialized hunting as part of full incident investigations. |

## Related content

- [Threat detection in the Microsoft Defender portal](/unified-secops-platform/detect-threats-overview)

- [Security posture management and risk reduction](/unified-secops-platform/reduce-risk-overview)

- [Service integration](/unified-secops-platform/overview-defender-portal)


# Plan Incident Response

# Plan an incident response workflow in the Microsoft Defender portal

In the Microsoft Defender portal, you can respond to security incidents that are collections of related alerts and tell the full story of an attack.

This article provides a set of steps that you can follow to investigate, analyze, and resolve security incidents in the Microsoft Defender portal, and also maps these steps to your security team's experience level and role.

## Incident response workflow example in the Microsoft Defender portal

Here's a workflow example for responding to incidents in the Microsoft Defender portal.

On an ongoing basis, identify the highest priority incidents for analysis and resolution in the incident queue and get them ready for response. This is a combination of:

- [Triage](/defender-xdr/incident-queue) to determining the highest priority incidents through filtering and sorting of the incident queue.

- [Manage](/defender-xdr/manage-incidents) incidents by modifying their title, assigning them to an analyst, and adding tags and comments.

You can use Microsoft Sentinel automation rules to automatically triage and manage (and even respond to) some incidents as they're created, removing the easiest-to-handle incidents from taking up space in your queue.

Consider these steps for your own incident response workflow:

| Stage | Steps |

| ----- | ----- |

| For each incident, begin an [attack and alert investigation and analysis](/defender-xdr/investigate-incidents). | - View the attack story of the incident to understand its scope, severity, detection source, and which asset entities are affected.<br>- Begin analyzing the alerts to understand their origin, scope, and severity with the alert story within the incident.<br>- As needed, gather information on impacted devices, users, and mailboxes with the graph. Select any entity to open a flyout with all the details. Follow through to the entity page for more insights.<br>- See how Microsoft Defender XDR has [automatically resolved some alerts](/defender-xdr/m365d-autoir) with the **Investigations** tab.<br>- As needed, use information in the data set for the incident for more information with the **Evidence and Response** tab. |

| After or during your analysis, perform containment to reduce any additional impact of the attack and eradication of the security threat. | For example,- Disable compromised users<br>- Isolate impacted devices<br>- Block hostile IP addresses. |

| As much as possible, recover from the attack by restoring your tenant resources to the state they were in before the incident.||

| [Resolve](/defender-xdr/manage-incidents#resolve-an-incident) the incident and document your findings. | Take time for post-incident learning to: - Understand the type of the attack and its impact.<br>- Research the attack in [Threat Analytics](/defender-xdr/threat-analytics) and the security community for a security attack trend.<br>- Recall the workflow you used to resolve the incident and update your standard workflows, processes, policies, and playbooks as needed.<br>- Determine whether changes in your security configuration are needed and implement them. |

If you're new to security analysis, see the [introduction to responding to your first incident](/defender-xdr/incidents-overview) for additional information and to step through an example incident.

For more information about incident response across Microsoft products, see [incident response overview](/security/operations/incident-response-overview).

## Plan initial incident management tasks

### Experience level

Follow this table for your level of experience with security analysis and incident response.

| Level | Steps |

|:-------|:-----|

| **New** | - See the [Respond to your first incident walkthrough](/defender-xdr/respond-first-incident-365-defender) to get a guided tour of a typical process of analysis, remediation, and post-incident review in the Microsoft Defender portal with an example attack. <br>- See which incidents should be [prioritized](/defender-xdr/incident-queue) based on severity and other factors.<br>- [Manage incidents](/defender-xdr/manage-incidents), which includes renaming, assigning, classifying, and adding tags and comments based on your incident management workflow. |

| **Experienced** | - Get started with the incident queue from the **Incidents** page of the Microsoft Defender portal. From here you can: <br>- See which incidents should be [prioritized](/defender-xdr/incident-queue) based on severity and other factors. <br>- [Manage incidents](/defender-xdr/manage-incidents), which includes renaming, assigning, classifying, and adding tags and comments based on your incident management workflow. <br>- Perform [investigations](/defender-xdr/investigate-incidents) of incidents. <br>- Track and respond to emerging threats with [threat analytics](/defender-xdr/threat-analytics). <br>- Proactively hunt for threats with [advanced threat hunting](/defender-xdr/advanced-hunting-overview). <br>- See these [incident response playbooks](/security/operations/incident-response-playbooks) for detailed guidance for phishing, password spray, and app consent grant attacks. |

### Security team role

Follow this table based on your security team role.

| Role | Steps |

|---|---|

| Incident responder (Tier 1) | Get started with the incident queue from the **Incidents** page of the Microsoft Defender portal. From here you can: - See which incidents should be [prioritized](/defender-xdr/incident-queue) based on severity and other factors. <br>- [Manage incidents](/defender-xdr/manage-incidents), which includes renaming, assigning, classifying, and adding tags and comments based on your incident management workflow. |

| Security investigator or analyst (Tier 2) | - Perform [investigations](/defender-xdr/investigate-incidents) of incidents from the **Incidents** page of the Microsoft Defender portal.<br>- See these [incident response playbooks](/security/operations/incident-response-playbooks) for detailed guidance for phishing, password spray, and app consent grant attacks. |

| Advanced security analyst or threat hunter (Tier 3) | - Perform [investigations](/defender-xdr/investigate-incidents) of incidents from the **Incidents** page of the Microsoft Defender portal. <br>- Track and respond to emerging threats with [threat analytics](/defender-xdr/threat-analytics). <br>- Proactively hunt for threats with [advanced threat hunting](/defender-xdr/advanced-hunting-overview). <br>- See these [incident response playbooks](/security/operations/incident-response-playbooks) for detailed guidance for phishing, password spray, and app consent grant attacks. |

| SOC manager | See how to [integrate Microsoft Defender XDR into your Security Operations Center (SOC)](/defender-xdr/integrate-microsoft-365-defender-secops). |

## Related items

To learn more about alert correlation and incident merging in the Defender portal, see [Alerts, incidents, and correlation in Microsoft Defender XDR](/defender-xdr/alerts-incidents-correlation).


# Respond Threats Overview

# Threat response in the Microsoft Defender portal

As cyber threats evolve and data stores and tooling grow in complexity, security solutions must adapt and respond faster in real time. This article explains how the advanced response features provided across the Microsoft Defender portal help contain threats as they're detected and neutralize them before causing damage.

## Threat response across the Defender portal

In the Defender portal, unified support for incident correlation and integrated threat intelligence across multiple attack surfaces helps security teams respond to threats effectively.

### Incident correlation

Related alerts from across multiple attack surfaces are grouped into a single incident in the Defender portal, improving the efficiency of incident response. Correlating alerts from various sources such as endpoints, identities, email, and cloud workloads helps security teams gain a holistic view of an attack campaign. This comprehensive perspective allows analysts to understand the full scope of an incident, identify the root cause, and determine the most effective remediation actions.

The following image shows a sample collection of alerts collected into a single incident in the Defender portal. In this example, alerts from Microsoft Defender for Endpoint, Microsoft Defender for Identity, Microsoft Defender XDR, Microsoft Defender for Office 365, and Microsoft Sentinel are all included in the same incident.

For more information, see [Alert correlation and incident merging in the Microsoft Defender portal](/defender-xdr/alerts-incidents-correlation).

### Integrated threat intelligence

Threat intelligence integrates across Defender portal services to enrich alerts with information on indicators of compromise (IOCs) such as malicious IP addresses, domains, and file hashes. This enrichment helps security teams quickly grasp threat context and severity, identifying false positives better and enabling faster, informed decision-making. Use threat intelligence from Microsoft and third-party sources to correlate alerts with attack patterns and tactics, techniques, and procedures (TTPs) employed by adversaries.

Continuous updates to threat intelligence feeds keep security teams ahead of emerging threats and improve the organization's overall resilience.

The following image shows an example of the incidents related to a **Human-operated ransomware** threat analytics report in the **Threat intelligence** area of the Defender portal.

For more information, see [Uncover adversaries with threat intelligence across the Defender portal](threat-intelligence-overview.md).

## Microsoft Defender XDR threat response features

Microsoft Defender XDR unifies threat protection by automating security across endpoints, identities, email, apps, and cloud workloads, helping organizations respond to threats effectively.

### Automated attack disruption

Automatic attack disruption boosts a SOC team's response by rapidly detecting and containing threats before escalation. It uses AI detection, predefined playbooks, and real-time threat intelligence to identify attack patterns and trigger immediate actions, such as isolating compromised endpoints or blocking malicious connections. This approach reduces the window for attackers and minimizes incident impact.

The following image shows an example of an incident tagged with attack disruption actions. The link in the notification takes you to a filtered view of the **Action center**, listing all the relevant automated attack disrupt actions taken.

The following image shows the **Action center** in this scenario. Select each item in the grid to show more details about the automated actions taken.

Automated attack disruption also improves collaboration across SOC teams by streamlining communication and responses. It alerts analysts and can suggest or execute actions based on predefined policies. This orchestration accelerates decision-making and ensures security teams can scale their efforts efficiently despite increasing threats.

Use Microsoft Defender XDR's automatic attack disruption to enhance your environment's overall resilience, reduce response times, and strengthen your organization's cybersecurity posture. For more information, see [Automatic attack disruption in Microsoft Defender XDR](/defender-xdr/automatic-attack-disruption?toc=/unified-secops-platform/toc.json&bc=/unified-secops-platform/breadcrumb/toc.json).

### Automated investigation and response (AIR)

Microsoft Defender XDR's AIR capabilities help security operations teams manage the high volume of alerts by automating investigation and response processes.

Acting as a virtual analyst, AIR mimics ideal investigation steps, working 24/7 to reduce response times and free up the security team for other tasks. When an alert triggers an incident, AIR initiates an automated investigation, resulting in verdicts such as *malicious*, *suspicious*, or *no threats*, and identifying necessary remediation actions, such as quarantining files or stopping processes.

The following image shows the automated investigation steps taken by Microsoft Defender XDR for the incident in our example. On the **Investigations** tab, select each investigation to view more details on the side.

Organizations can configure AIR capabilities to suit their needs, choosing either automatic remediation actions or ones that require security team approval. This automation significantly enhances the efficiency and effectiveness of security operations.

For more information, see [Automated investigation and response in Defender XDR](/defender-xdr/m365d-autoir?toc=/unified-secops-platform/toc.json&bc=/unified-secops-platform/breadcrumb/toc.json).

### Guided response with Microsoft Security Copilot

Microsoft Defender XDR's guided response features, powered by Microsoft Security Copilot, help security operations teams manage and resolve incidents efficiently with AI-driven recommendations. For response actions, guided responses propose specific measures to remediate threats and ensure comprehensive incident resolution.

Guided responses are shown together with other Copilot recommendations, as actionable cards that describe the suggested action, the targeted entity, and the rationale behind the recommendation. This structured approach enables incident response teams to confidently and swiftly apply appropriate measures, enhancing overall security posture.

The following image shows a sample of the **Guided response** section of the Copilot pane for a specific incident. If you have a lot of recommended actions to sort through, select the **Status** filter to show only some of the actions at a time

For more information, see [Triage and investigate incidents with guided responses from Microsoft Copilot in Microsoft Defender](/defender-xdr/security-copilot-m365d-guided-response).

### Extend response with the help of Microsoft Defender experts

Microsoft Defender Experts for XDR is a managed threat detection and response service that extends the capabilities of Microsoft’s security stack, providing proactive threat hunting and expert-driven analysis. This helps SOC teams focus on the most critical threats while reducing the burden of manual investigation.

Ask Defender Experts in Microsoft Defender XDR further enhances SOC teams’ efficiency by providing direct access to Microsoft’s security analysts. When an incident requires deeper investigation or expert insight, SOC teams can submit inquiries through the Defender portal. This feature allows security teams to get clarifications on complex attack patterns, guidance on remediation steps, and insights into emerging threats—all without disrupting their workflow. By leveraging Microsoft’s expertise, organizations can improve their threat response strategies, making their SOC teams more proactive and resilient against evolving cyber threats.

For more information, see:

- [Microsoft Defender Experts for XDR](/defender-xdr/dex-xdr-overview)

- [Collaborate with experts on demand](/defender-xdr/experts-on-demand)

## Microsoft Sentinel threat response features

Microsoft Sentinel provides cloud-native Security Information and Event Management (SIEM) and Security Orchestration, Automation, and Response (SOAR) features for intelligent security analytics and threat intelligence across the enterprise. This section describes how Microsoft Sentinel features add to your response capabilities.

### Automation rules

Microsoft Sentinel automation rules allow SOC teams to streamline and automate incident handling processes, ensuring structured responses across your environment. Automation rules can perform basic steps, such as adding incident tasks, suppressing noisy incidents, and changing incident statuses. They can also automate responses for multiple detections simultaneously, control the order of actions executed, and perform automation for limited time periods only, such as during testing or maintenance windows.

The following image shows an example of the sorts of configurations available for Microsoft Sentinel automation rules.

In the Defender portal, automation rules with incident triggers apply universally across both Microsoft Sentinel and Microsoft Defender XDR incidents, ensuring cohesive and comprehensive incident management.

For more information, see [Automate threat response in Microsoft Sentinel with automation rules](/azure/sentinel/automate-incident-handling-with-automation-rules?tabs=onboarded).

### Automated playbooks

Microsoft Sentinel playbooks are built using Azure Logic Apps and are automated workflows for streamlining and enhancing threat response in SOC teams. Have your playbooks trigger automatically in response to specific activity through configured automation rules, or run them manually as needed. For example, upon detecting a compromised account and machine, a playbook can isolate the affected machine from the network and block the compromised account before the SOC team is even alerted to the incident.

Common use cases for Microsoft Sentinel playbooks include data enrichment, bi-directional synchronization with ticketing systems, orchestration of incident management through communication platforms like Microsoft Teams or Slack, and immediate threat response actions. Microsoft Sentinel provides many playbooks out-of-the-box in solutions available from the **Content hub**.

The following image shows the Microsoft Sentinel **Content hub**, filtered for out-of-the-box playbooks available together with Microsoft Sentinel solutions.

To create and manage these playbooks, specific roles and permissions are required, and extra charges may apply for the usage of Azure Logic Apps. For more information, see [Automate threat response with playbooks in Microsoft Sentinel](/azure/sentinel/automation/automate-responses-with-playbooks).

### SOC optimizations

Security operations center (SOC) teams look for ways to improve processes and outcomes and ensure you have the data needed to address risks without extra ingestion costs. SOC teams want to make sure that you have all the necessary data to act against risks, without paying for more data than needed. At the same time, SOC teams must also adjust security controls as threats and business priorities change, doing so quickly and efficiently to maximize your return on investment.

SOC optimizations are actionable recommendations that surface ways that you can optimize your security controls, gaining more value from Microsoft security services as time goes on. Recommendations help you reduce costs without affecting SOC needs or coverage, and can help you add security controls and data where needed. These optimizations are tailored to your environment and based on your current coverage and threat landscape.

Use SOC optimization recommendations to help you close coverage gaps against specific threats and tighten your ingestion rates against data that doesn't provide security value. SOC optimizations help you optimize your Microsoft Sentinel workspace, without having your SOC teams spend time on manual analysis and research.

For more information, see [Microsoft Sentinel SOC optimizations](/azure/sentinel/soc-optimization/soc-optimization-access?tabs=defender-portal).

## Microsoft Security Exposure Management for potential threat response

[Microsoft Security Exposure Management](/security-exposure-management/microsoft-security-exposure-management) enables organizations to identify and mitigate potential attack paths before they can be exploited. Microsoft Security Exposure Management treats attack paths like incidents, providing a proactive approach to managing vulnerabilities and misconfigurations, and aiding in responses to in-progress attacks.

The following image shows an example of the number of attack paths detected over time in Microsoft Security Exposure Management.

An attack path analysis maps out potential attack vectors, providing remediation recommendations to reduce risk. Microsoft Security Exposure Management's security scoring system helps to prioritize vulnerabilities and misconfigurations that pose the greatest threat, and automated recommendations suggest the measures needed to strengthen an organization's overall security posture.

For more information, see [Start using Microsoft Security Exposure Management](/security-exposure-management/get-started-exposure-management) and [Overview of attack paths](/security-exposure-management/work-attack-paths-overview).

## Related content

For more information, see:

- [Incidents and alerts in the Microsoft Defender portal](/defender-xdr/incidents-overview?toc=/unified-secops-platform/toc.json&bc=/unified-secops-platform/breadcrumb/toc.json&tabs=defender-portal)

- [Threat detection in the Microsoft Defender portal](detect-threats-overview.md)

- [Uncover adversaries with threat intelligence across the Defender portal](threat-intelligence-overview.md)


# Cases Overview

# Manage security operations cases natively in the Microsoft Defender portal

Microsoft Defender case management is a collection of features and capabilities delivering a unified, security-focused case management experience. This experience is designed for managing unified security operations work natively in the Microsoft Defender portal, without the need for third-party tools. Security operations teams maintain security context, work more efficiently, and respond faster to attacks when they manage case work without leaving the Defender portal.

The current, introductory phase of the case management rollout centralizes rich collaboration, customization, evidence collection, and reporting across SecOps workloads.

<a name="what-is-case-management-preview"></a>

## What is case management?

Case management enables you to manage SecOps cases natively in the Defender portal. Even in its initial stages, SecOps teams are demonstrating the following use cases for case management:

- Responding to security events that span multiple incidents.

- Managing threat hunting.

- Tracking IoCs and threat actors.

- Tracking detection logic that needs tuning.

The following specific capabilities and features support these use cases and scenarios:

- Create and track your SecOps related cases in one place with the new **Cases** page.

- [Define your own case workflow by configuring custom status values](#customize-status).

- [Improve collaboration, quality, and accountability by assigning tasks and due dates](#tasks).

- [Handle escalations and complex cases by linking multiple incidents to a case](#link-incidents).

- [Manage access to your cases using RBAC](#requirements).

- [Add rich-text comments to provide links, tables, and formatting to the activity log](#activity-log).

- [Upload attachments to store files like documents, CSVs, and encrypted zip files containing malware samples](#attachments).

- [Manage cases in multiple tenants via the multitenant management portal](mto-manage-cases.md).

As we build on this foundation of case management, we're prioritizing these additional robust capabilities as we evolve this solution:

- Automation

- More evidence to add

- Workflow customization

- More Defender portal integrations

## Requirements

Case management is available in the Defender portal, and to use it, you must have a Microsoft Sentinel workspace connected. Cases are accessible only from the Defender portal; you can't see them in the Azure portal.

For more information, see [Connect Microsoft Sentinel to the Defender portal](microsoft-sentinel-onboard.md).

Use Defender unified RBAC or Microsoft Sentinel roles to grant access to case management features.

| Cases feature | Microsoft Defender unified RBAC | Microsoft Sentinel role |

| ------------- | ------------------------------- | ----------------------- |

| View only</br>- case queue</br>- case details</br>- tasks</br>- comments</br>- case audits | Security operations > Security data basics (read)| Microsoft Sentinel Reader |

| Create and Manage</br>- cases and case tasks</br>- assign</br>- update status</br>- link and unlink incidents | Security operations > Alerts (manage) | Microsoft Sentinel Responder |

| Customize case status options | Authorization and setting > Core Security settings (manage)| Microsoft Sentinel Contributor |

For more information, see [Microsoft Defender unified role-based access control (RBAC)](/defender-xdr/manage-rbac).

## Case queue

To start using case management, select **Cases** in the Defender portal to access the case queue. Filter, sort, or search your cases to find what you need to focus on.

## Case details

Each case has a page which allows analysts to manage the case and displays important details.

In the following example, a threat hunter is investigating a hypothetical "Burrowing" attack that consists of multiple MITRE ATT&CK&reg; techniques and indicators of compromise (IoCs).

Manage the following case details to describe, prioritize, assign, and track work:

| Displayed case feature | Manage case options | Default value |

|:---|:---|:---|

| **Priority** | `Very low`, `Low`, `Medium`, `High`, `Critical` | none |

| **Status** | Set by analysts, customizable by admins | Default statuses are `New`, `Open`, and `Closed`</br>Default value is `New`|

| **Assigned to** | A single user in the tenant | none |

| **Description** | Plain text | none |

| **Case details** | Case ID | Case IDs start at 1000 and aren't purged. Use custom statuses and filters to archive cases. Case numbers are automatically set.|

| | Created by</br>Created on</br>Last updated by</br>Last updated on | automatically set |

| | Due on</br>Linked incidents | none |

Manage cases further by setting customized status, assigning tasks, linking incidents, and adding comments.

### Customize status

Architect case management to fit the needs of your security operations center (SOC). Customize the status options available to your SecOps teams to fit the processes you have in place.

Following the burrowing attack case creation example, the SOC admins configured statuses enabling threat hunters to keep a backlog of threats for triage on a weekly basis. Custom statuses such as *Research phase* and *Generating hypothesis* match this threat hunting team's established process.

### Tasks

Add tasks to manage granular components of your cases. Each task comes with its own name, status, priority, owner, and due date. With this information, you always know who is accountable to complete which task and by what time. The task description summarizes the work to do and some space for describing the progress. Closing notes provide more context about the outcome of completed tasks.

*Image shows the following task statuses available: New, In progress, Failed, Partially completed, Skipped, Completed*

### Link objects

Linking a case to other objects in your environment helps your SecOps teams understand the broader context of a threat. You can link cases to incidents or [indicators of compromise (IoCs)](/defender-endpoint/indicators-overview).

#### Link incidents

Linking a case and an incident helps your SecOps teams collaborate in the method that works best for them. For example, a threat hunter who finds malicious activity creates an incident for the incident response (IR) team. That threat hunter links the incident to a case so it's clear they're related. Now the IR team understands the context of the hunt that found the activity.

Alternatively, if the IR team needs to escalate one or more incidents to the hunting team, they can create a case and link the incidents from the **Investigation & response** incident details page.

#### Link indicators (preview)

Linking a case to relevant indicators of compromise (IOCs) helps your SecOps teams understand the broader context of a threat.

To link the case to IOCs, go to the **Linked Objects** tab in the Case page and select **Indicators**. Then, select the **Add** button and the workspace the TI Indicator is in. Select the wanted TI Indicator and click on **Link**.

Alternatively, you can create a case and link the indicators from the Intel management indicators details page. Select your TI Indicator and then on **Link Cases**.

### Activity log

Need to write down notes, or that key detection logic to pass along? Create rich text comments and review the audit events in the activity log. Comments are a great place to quickly add information&mdash;including such things as queries, tables, links, and structured content&mdash;to a case.

Audit events are automatically added to the activity log of the case and the latest events are shown at the top. Change the filter if you need to focus on comments or audit history.

### Attachments

Share reports, emails, screenshots, log files, and more, all centralized in the **Attachments** tab of a case. Ensure you have all the necessary information to make quick and accurate decisions in your security investigations.

You can attach up to 10 files per comment.

#### Add attachment to a case

To add attachments to your case, go to the **Case details** page, select the **Attachments** tab, select **Upload**, select your file, and wait for the upload to complete. Once uploaded, the file is scanned in the background for malware. When the scan is complete, anyone with access to the case can download the file. If the file you want to upload is actually a malware sample, you can wrap it in a password-protected ZIP file.

#### Add attachment to a comment (preview)

To add an attachment to a comment:

1. Go to the comment area of the *Case* page.

1. Go to the text editor at the bottom of the screen, and select the paperclip icon to attach a file.

1. Select the file you want to attach from your computer.

1. Select **Send** to save the comment.

- To attach a screenshot to your comment, paste it into the text editor.

- To delete an attached file from the comment, select the bin icon while hovering over it.

### Delete Case (preview)

To delete a case:

1. Open the Cases screen, select the case you want to remove, and select **Delete**.

1. In the pop-up window, type *delete* and then select **Confirm**.

## Limitations

See [Case management limits](/azure/sentinel/sentinel-service-limits#case-management-limits).

## Related content

- [Microsoft Sentinel blog - Improve SecOps collaboration with case management](https://techcommunity.microsoft.com/blog/MicrosoftSentinelBlog/improve-secops-collaboration-with-case-management/4369044)

- [Microsoft Sentinel in the Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal)

- [View and manage cases across multiple tenants in the Microsoft Defender multitenant portal](mto-manage-cases.md)

- [Microsoft Defender multitenant management](mto-overview.md)


# Mto Overview

# Microsoft Defender multitenant management

Multitenant management for Microsoft Defender XDR and Microsoft Sentinel in the Defender portal provides your security operations teams with a single, unified view of all the tenants you manage. This view enables your teams to quickly investigate incidents and perform advanced hunting across data from multiple tenants, improving your security operations.

## Microsoft Sentinel support

For each tenant, the Defender portal allows you to connect to one primary workspace and multiple secondary workspaces for Microsoft Sentinel. In the context of this article, a workspace is a Log Analytics workspace with Microsoft Sentinel enabled.

If you have tenants with Microsoft Sentinel workspaces onboarded to the Defender portal, you can:

- Triage incidents and alerts across Security Information and Event Management (SIEM) and eXtended Detection and Response (XDR) data.

- Proactively search for SIEM and XDR data across multiple tenants.

- Manage cases across multiple tenants.

Each workspace must be onboarded to the Defender portal for each of your tenants separately, as you would in a single-tenant scenario.

For more information, see:

- [Connect Microsoft Sentinel to Microsoft Defender XDR](microsoft-sentinel-onboard.md)

- [Multitenant organizations documentation](/azure/active-directory/multi-tenant-organizations/)

- [Multiple Microsoft Sentinel workspaces in the Defender portal](/azure/sentinel/workspaces-defender-portal)

## Feature availability

Multitenant management is also available to US government customers. Refer to the following table for specific scenarios for GCC, GCC High, DoD, and Commercial customers.

| Scenario | Availability |

| ------ | ------ |

| Multitenant management | Available to all GCC, GCC High, DoD, and Commercial customers. |

| Cross-cloud collaboration | - Both DoD and GCC High customers can manage tenants in each other's clouds. </br></br> - GCC customers can manage tenants in the Commercial cloud. |

## Benefits of multitenant management

Some of the key benefits you get with multitenant management for Defender XDR and the Microsoft Sentinel in the Defender portal include:

- **A centralized place to manage incidents and cases across tenants**: A unified view provides SOC analysts with all the information they need to investigate incidents and cases across multiple tenants, eliminating the need to sign in and out of each one.

- **Streamlined threat hunting**: Multi-tenancy support enables SOC teams use Microsoft Defender XDR advanced hunting capabilities to create Kusto Query Language (KQL) queries that proactively hunt for threats across multiple tenants.

- **Multi-customer management for partners**: Managed Security Service Provider (MSSP) partners can now gain visibility into cases, security incidents, alerts, and threat hunting across multiple customers through a single pane of glass.

<a name='whats-included-in-multi-tenant-management-in-microsoft-365-defender'></a>

## What does multitenant management include?

The following key capabilities are available for each tenant you have access to in multitenant management for Microsoft Defender XDR and Microsoft Sentinel in the Defender portal:

| Capability | Description |

| ---------- | ----------- |

| **Incidents & alerts** > **[Incidents](mto-incidents-alerts.md)** | Manage incidents originating from multiple tenants. |

| **Incidents & alerts** > **[Alerts](mto-incidents-alerts.md)** | Manage alerts originating from multiple tenants. |

| **[Cases](cases-overview.md)** | Manage cases originating from multiple tenants. |

| **Hunting** > **[Advanced hunting](mto-advanced-hunting.md)** | Proactively hunt for intrusion attempts and breach activity across multiple tenants at the same time. |

| **Hunting** > **[Custom detection rules](/defender-xdr/custom-detections-overview)** | View and manage custom detection rules across multiple tenants. |

| **Assets** > **Devices** > **[Tenants](mto-tenant-devices.md)** | For all tenants and at a tenant-specific level, explore the device counts across different values such as device type, device value, onboarding status, and risk status. |

| **Endpoints** >**Vulnerability Management** > **[Dashboard](mto-dashboard.md)** | The Microsoft Defender Vulnerability Management dashboard provides both security administrators and security operations teams with aggregated vulnerability management information across multiple tenants. |

| **Endpoints** > **Vulnerability management** > **[Tenants](mto-dashboard.md)** | For all tenants and at a tenant-specific level, explore vulnerability management information across different values such as exposed devices, security recommendations, weaknesses, and critical CVEs. |

| **Configuration** > **Settings** | Lists the tenants you have access to. Use this page to view and manage your tenants. |

| **Multi-tenant management** > **[Tenant groups](mto-tenant-groups.md)** | Organize the tenants you manage into named groups and switch the multitenant view between those groups. |

## Limitations

Mutitenant management supports multitenant single workspaces. This means that you can query multiple tenants and their primary workspace through Advanced Hunting without Lighthouse.

[Azure Lighthouse](/azure/lighthouse/) is required when you want to query a secondary workspace in a different tenant (from Advanced Hunting, analytic rules, workbooks, etc.). For these queries, use the workspace() operator from either the multitenant management portal or `security.microsoft.com`.

## Next steps

- [Set up Microsoft Defender multitenant management](mto-requirements.md)

- [Create and manage tenant groups](mto-tenant-groups.md)


# Playbook Managed Security

# Microsoft Defender portal implementation guide for MSSPs

The Microsoft Defender portal is a unified security operations platform that brings together incident management, threat hunting, and workload management across multiple customer tenants. For a comprehensive overview of these capabilities and their benefits, see [Microsoft Defender multitenant management](mto-overview.md).

This guide focuses on implementing tenant management for Managed Security Service Providers (MSSPs). It covers the entire process from initial setup and customer onboarding through advanced operational workflows for MSSPs.

### Key Capabilities & Differentiators

Key features of the Microsoft Defender portal for MSSPs include:

- **Unified incident management**: A single unified incidents queue includes data from Microsoft Sentinel, Microsoft Defender, and third-party sources. For more information, see [Manage Security Operations across tenants](#manage-security-operations-across-tenants)

- **Cross-platform threat hunting**: Unified hunting capabilities across security data, eliminates the need to switch between portals and allows analysts to easily locate the data they need across their entire customer base. For more information, see [Advanced hunting](#advanced-hunting).

- **Proactive attack disruption**: Attack Disruption delivers proactive protection by stopping attacks in progress. It works on native Microsoft Defender technologies and across third-party environments, such as SAP, [AWS](/azure/sentinel/aws-disruption), Proofpoint, and Okta. Microsoft Defender reduces dwell time and prevents lateral movement by automatically revoking compromised credentials, isolating malicious sessions, and neutralizing attacker footholds.

- **Attack path analysis and exposure visualization**: Analyze attack paths and reduce exposure by visualizing how cyber attackers could exploit vulnerabilities to move laterally across exposed assets in customer environments. Get guided recommendations on reducing exposure and prioritize actions based on each exposure's potential impact. For more information, see [Microsoft Security Exposure Management](#exposure-management).

- **Enhanced detection accuracy**: Detect and investigate quickly and accurately by combining the depth of signals Microsoft Defender with the flexibility of log sources from Microsoft Sentinel. This results in an improved signal-to-noise ratio and enhanced alert correlation.

- **AI-powered security operations**: Take advantage of Microsoft Security Copilot for incident summaries and reports, guided investigation, autogenerated Microsoft Teams messages, code analysis, and more. For more information, see [Get started with agentic AI](#get-started-with-agentic-ai).

- **Scalable multitenant management**: Get aggregate views of your tenants' alerts, incidents, and assets, hunt over all your tenants' data, and maintain a consistent security baseline across your tenants using [content management and distribution features](#manage-and-distribute-content) for custom detection rules, endpoint security policies, analytics rules, automation rules, and more.

- **Continuous improvement insights**: Receive tailored, post-incident recommendations on preventing similar or repeat cyberattacks, which tie directly into [Microsoft Security Exposure Management](#exposure-management) initiatives to automatically improve readiness scores as actions are completed.

To build Security Operations on the Microsoft Defender Portal, read through the [prerequisites](#prerequisites), then follow these steps:

1. [Step 1](#step-1---prepare-your-environment) - Prepare your environment: Prepare your MSSP environment and onboard your customers to a multitenant configuration

1. [Step 2](#step-2---manage-content) - Content Management: Build security content once and deploy it across all customer tenants efficiently.

1. [Step 3](#step-3---multitenant-security-operations) - Multitenant Security Operations: Run daily incident response, threat hunting, and investigations across customer tenants.

## Prerequisites

Transitioning customers to the Microsoft Defender portal involves migrating Microsoft Sentinel workspaces and ensuring continuity of security operations.

- See [Connect Microsoft Sentinel to Microsoft Defender XDR](microsoft-sentinel-onboard.md) for the technical migration process.

- Establish clear timelines and expectations with customers before beginning the transition

- Review the multitenant access requirements and ensure proper delegation is configured for each customer tenant

- Determine the optimal workspace configuration (primary vs. secondary) based on each customer's environment and compliance requirements

## Step 1 - Prepare your environment

### Set up access to multiple customer tenants

MSSPs can delegate access to customer tenants through several methods. [Learn more about delegated access options](/partner-center/customers/gdap-introduction) so you can choose the approach that best fits your organization's needs and customer requirements.

>[!NOTE]

> There are scenarios where MSSPs shouldn't use cross-workspace rules. For example, when the same rule applies to multiple individual workspaces, data doesn't need to be correlated together. For this scenario, MSSPs should push the same rule to whatever workspaces it applies to.

#### Advanced automation rule/playbook scenario

Some advanced scenarios using automation rules and playbooks might still require using Azure Lighthouse. For example, to protect the intellectual property of a playbook hosted in the partner tenant when the playbook needs to execute actions in the customer tenant. Another example is described in [Automate threat response in Microsoft Sentinel with automation rules](/azure/sentinel/automate-incident-handling-with-automation-rules?tabs=onboarded#permissions-in-a-multitenant-architecture)

#### Unified RBAC

When looking at using unified RBAC in managing your Microsoft Defender for Office 365 customers, you must have Defender for Office 365 Plan 2 license. For more information, see:

- [Email and collaboration permissions mapping](/defender-xdr/compare-rbac-roles#email--collaboration-permissions-mapping)

- [Exchange Online permissions mapping](/defender-xdr/compare-rbac-roles#exchange-online-permissions-mapping)

#### Azure B2B

Azure B2B invited guests aren't supported by experiences that were previously under Microsoft Exchange Online RBAC. Since Defender for Office 365 unified RBAC leans on Exchange Online Admin APIs, actions performed in Defender for Office 365 have limitations. B2B guest admins might get errors when attempting to perform certain actions, such as:

- Managing spam and phishing policies

- Managing TABL

- Can't release emails from quarantine

- Missing Threat Explorer in navigation pane

### Manage entitlement

[Entitlement management](/entra/id-governance/entitlement-management-overview) is an [identity governance](/entra/id-governance/identity-governance-overview) feature that enables organizations to manage identity and access lifecycle at scale, by automating access request workflows, access assignments, reviews, and expiration.

Some typical entitlement management configurations are:

- B2B Collaboration

- Invite external users as guests into your tenant

- Supports Conditional Access, MFA, and lifecycle management

- Ideal for partners, suppliers, and contractors needing app/resource access that can be governed

- Cross-Tenant access settings

- Fine-grained control over inbound/outbound collaboration

- Trust MFA and device compliance claims across tenants

- Configure default or organization-specific policies

- B2B Direct Connect

- Enables mutual trust between two Microsoft Entra tenants

- Seamless collaboration via Teams shared channels without adding guests

- Perfect for ongoing partnerships where users keep home credentials

Often, a combination of B2B Collaboration and Cross-Tenant access settings are the most relevant choices for an MSSP.

This picture shows the B2B collaboration guest representation in the customer tenant.

For sample role assignments for different SOC roles, see the [Sample permission mappings of Microsoft Sentinel built-in roles to Microsoft Defender unified RBAC roles](/defender-xdr/compare-rbac-roles).

## Step 2 - Manage content

### Manage and distribute content

In Microsoft Sentinel, content refers to the building blocks that enable security operations. It includes analytics rules, data connectors, hunting queries, parsers, playbooks, watchlists, and workbooks. [Microsoft Sentinel provides out-of-the-box content](/azure/sentinel/sentinel-solutions) that you can use as-is or you can customize it. You can also create and distribute custom content to meet specific requirements. Effective content management and distribution ensure consistent security baselines, rapid threat response, and scalable operations across customer tenants.

MSSPs working in the Microsoft Defender portal have several tools for managing and distributing security content at scale:

| **Option**                               | **Best for**                                                   | **Technical details**                                                                                                      | **Key capabilities**                                                                                           | **Learn more**                                                                                     |

|------------------------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|

| **Native multitenant content distribution** | Quick deployment of standard content across many tenants | Uses Defender portal's built-in multitenant management. Ideal for OOB content or lightly customized content.              | <ul><li>Create once, deploy everywhere across multiple tenants</li><li>Execute content on target scopes (devices, workspaces)</li><li>Centralized tracking to reduce duplication and errors</li></ul> | [Content distribution in multitenant management](/unified-secops-platform/mto-distribution-profiles) |

| **Microsoft Sentinel repositories (content as code)** | Structured DevOps processes and moderate customization needs | Enables advanced governance and lifecycle management. Quick configuration and reduction in human error. | <ul><li>Manage SIEM content using automation</li><li>Apply CI/CD practices for version control, testing, and deployment</li><li>Supports hybrid workflows combining native distribution and DevOps</li></ul> | [Manage content as code with Microsoft Sentinel repositories (public preview)](https://aka.ms/microsoft-sentinel-repos) |

| **Custom CI/CD pipelines**              | Maximum customization and automation across tenants | Built using Azure DevOps or GitHub Actions. Requires custom scripts and configuration files. Current method for advanced content types. | <ul><li>Full flexibility for complex workflows</li><li>Custom testing and integration</li></ul> | [Customize repository deployments (public preview)](/azure/sentinel/ci-cd-custom-deploy) |

>[!TIP]

> We recommend a hybrid approach, combining native multitenant management content distribution capabilities for immediate deployment needs with CI/CD workflows for custom content development, testing, and advanced automation scenarios.

### Common repository architecture patterns for MSSPs

A key consideration with multi-customer CI/CD pipelines is choosing the best structure to serve all clients. While there’s no universal approach, here are three patterns we recommend considering:

#### Pattern 1: Central repository for generic content, customer-specific repositories for tailored content

- One central repository for common content deployed to all customers

- Individual repositories for customer-specific customizations

- Each customer workspace connects to both repositories

- Optimal for MSSPs with balanced common and tailored content needs

#### Pattern 2: Single repository with custom folders

- All content in one repository

- Folder structure based on shared data sources - for example, Entra ID Analytics - or customer names

- Deployment pipelines customized per customer connection

- Requires more initial setup but simplifies repository management

#### Pattern 3: One repository per customer

- Complete content separation across customers

- Full customization flexibility for each customer

- Best for customers with unique content requirements

- Higher management overhead but maximum isolation

To customize your CI/CD pipelines, use configuration files in each repository branch to prioritize deployment of high-priority content, exclude content you don’t want to deploy, and map parameter files to their corresponding content files. For more information, see [Customize your connection configuration](/azure/sentinel/ci-cd-custom-deploy#customize-your-connection-configuration).

For more information about how to use Azure DevOps in multitenant scenarios, see [Use Azure DevOps to manage Microsoft Sentinel for MSSPs and multitenant Environments](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/use-azure-devops-to-manage-sentinel-for-mssps-and-multi-tenant-environments/4008109).

### Shared content management considerations

When MSSPs and customers both manage content, conflicts can occur, especially if you're using both content-as-code and the portal for content management. Updates in your content-as-code repositories overwrite any changes made to that content through the portal.

To prevent such conflicts, we recommend:

- Centralized management only - Restrict permissions so only MSSP users can create and update content.

- Shared management with clear markers - Prefix MSSP-managed items with a naming convention. This allows local updates but reduces errors.

## Step 3 - Multitenant Security Operations

### Manage security operations across tenants

The Microsoft Defender portal provides all relevant information so you don't have to switch to another portal or page. Its unified incident queue and the ability to correlate events and alerts can reveal a larger, potentially more comprehensive attack, providing a complete attack story. It also lets you view the detection source and product names, and apply and share filters for these, making incident and alert triaging more efficient.

#### Manage incidents and alerts

- **Incident triage:** Triaging incidents is a core activity in a SOC, starting with the Investigation and response section in the Defender portal. The Microsoft Sentinel incident and alert integration with Defender consolidates all relevant information in one place, eliminating the need to switch between portals or pages. This streamlined workflow might require some analyst retraining and updates to existing SOC processes.

For more information, see [Update incident triage processes for the Defender portal](/azure/sentinel/move-to-defender?toc=%2Funified-secops-platform%2Ftoc.json&bc=%2Funified-secops-platform%2Fbreadcrumb%2Ftoc.json#update-incident-triage-processes-for-the-defender-portal).

- **Alert correlation and incident merging:** Defender's correlation engine merges incidents when it recognizes common elements between alerts in separate incidents. When a new alert meets [correlation](/defender-xdr/alerts-incidents-correlation#incident-creation-and-alert-correlation) criteria, Defender aggregates and correlates it with other related alerts from all detection sources into a new incident. The unified incident queue reveals a more comprehensive attack, making analysts more efficient and providing a complete attack story.

In [multi-workspace](/azure/sentinel/workspaces-defender-portal#primary-and-secondary-workspaces) scenarios, only alerts from a primary workspace are correlated with Microsoft Defender data. There are also scenarios where incidents can't be merged.

For more information, see [Understand how alerts are correlated and incidents are merged in the Defender portal](/azure/sentinel/move-to-defender?toc=%2Funified-secops-platform%2Ftoc.json&bc=%2Funified-secops-platform%2Fbreadcrumb%2Ftoc.json#understand-how-alerts-are-correlated-and-incidents-are-merged-in-the-defender-portal).

- **Multitenant organization:** You can view and manage incidents, alerts, and cases across customer tenants in a unified queue. Each analyst can set up their multitenant view with the tenants they're managing. For more information, see [Microsoft Defender multitenant management](mto-overview.md).

- **Integration with external ticketing systems:** If an external ticketing system fetches and synchronizes with the alerts and incidents you manage, we recommend that you use the [Microsoft Graph REST API v1.0](/graph/api/resources/security-api-overview) to ensure seamless integration and efficient management of incidents and alerts across different systems.

If you're using the Microsoft Sentinel SecurityInsights API to interact with Microsoft Sentinel incidents, you might need to update your automation conditions and trigger criteria due to changes in the response body.

For more information, see [Configure APIs](/azure/sentinel/move-to-defender?toc=%2Funified-secops-platform%2Ftoc.json&bc=%2Funified-secops-platform%2Fbreadcrumb%2Ftoc.json&branch=main#configure-apis).

#### Advanced hunting

Advanced hunting lets you proactively hunt for intrusion attempts and breach activity in email, data, devices, and accounts across multiple tenants and workspaces at the same time, in a single place. If you have multiple tenants with Microsoft Sentinel workspaces onboarded to the Microsoft Defender portal (MTO), you can query Microsoft Sentinel with data from all your workspaces, running queries across multiple workspaces and tenants using the workspace operator in your query.

For more information, see [Advanced hunting in Microsoft Defender multitenant management](mto-advanced-hunting.md).

### Manage workloads across tenants

This section explores the various actions you can take and methods you can use for managing specific workloads, either through MTO or other available means.

#### Endpoints

The multitenant view in the Defender portal provides security administrators a consolidated view of all security policies across their entire organization, including all tenants' policies, without needing to switch portals. To access this page, go to **Endpoints** > **Configuration Management** > **Endpoint Security Policies**.

Once the tenants are onboarded to multitenant management in Defender (MTO), endpoints across all onboarded tenants can be managed through the [**Devices**](https://mto.security.microsoft.com/machines) page. For more information, see [Devices in multitenant management](mto-tenant-devices.md).

>[!IMPORTANT]

>To manage security settings for multiple tenants in the multitenant view in the Defender portal, you must follow all the prerequisites to configure security settings for a single tenant for each of their tenants, including the following RBAC requirements:

>- For Microsoft Defender, use the security administrator role (or custom role with security configuration management permissions scoped to all devices)

>- For Microsoft Intune, use the Endpoint security manager role

>- The devices in each Defender tenant must be affiliated with the corresponding Microsoft Entra tenant

>

>For more information, see [Use Intune to manage Microsoft Defender settings on devices that aren't enrolled with Intune](/mem/intune/protect/mde-security-integration?toc=%2Fdefender-endpoint%2Ftoc.json&bc=%2Fdefender-endpoint%2Fbreadcrumb%2Ftoc.json).

>[!NOTE]

> Multitenant management in Defender (MTO) doesn't support Microsoft Defender for Business tenants.

#### Email and collaboration tools

When managing email and collaboration tools in the unified portal, there are some important distinctions to note around capabilities as they relate to managing customers through B2B and Granular Delegated Admin Privileges (GDAP).

#### Identities

The multitenant view in the Defender portal provides complex organizations with means to segregate regions and business units into individual tenants, without losing access to those tenant data.

Once the tenants are onboarded to multitenant management in Defender (MTO), identities across all onboarded tenants can be managed through the Identities page. For more information, see [Multitenant identities](multitenant-identities-inventory.md).

#### Cloud applications

**Microsoft Defender for Cloud Apps** is a software-as-a-service (SaaS) security solution that comes with relevant licenses and a compliance boundary of the tenant where the license is provisioned. Due to this architecture, only Microsoft 365 and Azure connectors ingest activities and trigger alerts for users within those tenants. However, you can still connect multiple third-party connectors.

Defender for Cloud Apps is natively integrated with Microsoft Defender and follows the same multitenancy capabilities. While connectors are limited to a specific tenant, the data ingested from each tenant in the `CloudAppEvents` table and incidents or alerts are available through MTO. You can hunt for events across tenants and triage incidents or that originate from Defender for Cloud Apps signals.

For more information, see [Microsoft Defender for Cloud Apps overview](/defender-cloud-apps/what-is-defender-for-cloud-apps).

#### Cloud

**Microsoft Defender for Cloud** is integrated with Microsoft Defender. This integration lets you access Defender for Cloud alerts and incidents within the Defender portal, and provides you with richer context to investigations that span cloud resources, devices, and identities. It allows security teams to get the complete picture of an attack, including suspicious and malicious events that happen in their cloud environment.

For more information, see [What is Microsoft Defender for Cloud?](/azure/defender-for-cloud/defender-for-cloud-introduction).

#### Exposure management

**Microsoft Security Exposure Management** is a security solution that provides a unified view of security posture across company assets and workloads. It enriches asset information with security context that helps you to proactively manage attack surfaces, protect critical assets, and explore and mitigate exposure risk.

For more information, see [What is Microsoft Security Exposure Management?](/security-exposure-management/microsoft-security-exposure-management).

#### Data

**Microsoft Purview** data security solutions provide unified data discovery, classification, and protection across clouds, SaaS, and on premises data stores. They complement Defender and Microsoft Sentinel by turning data risk into actionable security signals, helping you understand what sensitive data exists, where it lives, and how it is being accessed or shared. For more information, see [Microsoft Purview data security solutions](/purview/purview-security).

Key integrations include:

-	**Alert and incidents (Defender and Sentinel):** Microsoft Purview Data Loss Prevention, Insider Risk Management and sensitivity-label based detections generates alerts that flow into the unified incident queue. This enables correlation with device, identity, cloud application, and network signals, surfacing cross-domain attack stories and reducing context switching for analysts. When Microsoft Purview alerts are part of an incident, the unified portal displays the metadata and can be used in automation rules and playbooks through the Microsoft Graph security APIs, just like other Defender and Sentinel alerts.

-	**Hunting and investigations (advanced hunting):** Microsoft Purview events, such as data loss prevention (DLP) hits, file access anomalies, and label changes are available in Defender advanced hunting schema. You can run cross-tenant queries in the MTO portal to hunt for patterns that span data, identity, and endpoint signals. For example, a surge of high-sensitivity file downloads from a single user, followed by anomalous sign-in behavior.

-	**Context enrichment:** Purview's data inventory and classification enrich the Security Exposure Management story by mapping critical data assets to exposure insights and attack paths. This helps prioritize mitigations based on the business impact of exposed data.

### Manage cases

The unified security operations portal provides native case management to eliminate reliance on external ticketing systems and maintain security context within the Defender portal.

For complete guidance on case features, workflows, linking incidents and IoCs, RBAC requirements, and customization options, see [Cases overview](cases-overview.md). For multitenant case management, see [Manage cases in MTO](./mto-manage-cases.md).

**Note:** Case management supports custom workflows, task assignments, rich collaboration, and evidence linking.

### Get started with Microsoft Sentinel data lake

[Microsoft Sentinel](/azure/sentinel) includes a unified, security [data lake](/azure/sentinel/datalake/sentinel-lake-overview), designed to help optimize costs, simplify data management, and accelerate the adoption of AI in security operations. This data lake serves as the foundation for the Microsoft Sentinel platform. It has a cloud-native architecture and brings together all security data for greater visibility, deeper security analysis, and contextual awareness. It provides affordable, long-term retention allowing organizations to maintain robust security while not compromising on costs.

The Microsoft Sentinel platform lets you expand your MSSP offerings through professional services, managed services, and agentic solutions:

-	Offer advisory, consulting, and strategic guidance on lake architectures, with high-value opportunities in deployment, configuration, and cost optimization.

-	Provide ongoing management of Microsoft Sentinel data lake platforms and SOC operations, helping your customers lower data ingestion and retention costs while expanding recurring revenue streams through enhanced security protection opportunities.

-	Develop AI agentic solutions for automated threat enrichment and response, building analytics, and evolving SOAR to agent-based workflows.

### Get started with agentic AI

You have multiple opportunities to engage with your customers and diversify your MSSP offerings when it comes to agentic AI scenarios within the Microsoft Defender portal. We break down these benefits into **Sell**, **Build**, and **Use** buckets.

#### Sell

You can engage with your customers to sell consulting services that educate, enable, configure, and implement agentic solutions, such as:

- **Partner-developed consulting services** - Traditional consulting services available through the [Microsoft Marketplace](/partner-center/marketplace-offers/overview). Provide training workshops, implementation engagements, and assessments, proof-of-concepts, or proof-of-value deliveries. These services are great opportunities to improve your customer environment's security maturity, increase their staff's skilling and readiness, and showcase product return on investment with real-world use case scenarios.

- **Partner-developed security services** – Traditional security service offerings like partner-managed security services, partner-managed XDR solutions, and other partner-developed security services are available in the [Microsoft Security Store](/security/store/what-is-security-store).

- **Microsoft-developed Security Copilot agents** - [Microsoft-developed Security Copilot agents](/copilot/security/agents-security-copilot) that span across Microsoft Defender, Microsoft Sentinel, and other security solutions available within the Defender portal.

- **Partner-developed Security Copilot agents** - These agents are available for purchase and deployment through the Microsoft Security Store. You can integrate your own published Security Copilot agents or other partner agents into your customers' Microsoft Defender environment. For more information, see [Partner agents](/copilot/security/agents-other).

#### Build

Develop Security Copilot agents that can be monetized through the Microsoft Security Store. The agents can be a one-time purchase, subscription-based model for recurring agent updates, or provided at no cost. Partner-developed agent types include:

- **Role/Persona-based agents** - Designed with skills to perform a specific type of persona or role like an L1 SOC Analyst

- **Scenario-based agents** - Designed with skills for a specific type of scenario like phishing, insider threat, or advanced persistent threats (APTs)

- **Product-based agents** - Designed with skills to integrate with a specific product/solution like Microsoft Defender or a third-party security vendors

For more information, see [Microsoft Security Copilot agent development overview](/copilot/security/developer/custom-agent-overview).

#### Use

Partner developed agents within your customer's Microsoft Defender environment as part of their [partner managed SOC offering](https://www.microsoft.com/security/business/find-a-partner). This includes acting on behalf of your customer within their tenant as an augmentation of their internal team, or performing SOC activities from their tenant and applying multitenancy capabilities of Microsoft Defender through delegated access.

## Training and community resources

- Transition Guide: [Transition Your Microsoft Sentinel Environment to the Defender Portal](/azure/sentinel/move-to-defender)

- How to: [Connect Microsoft Sentinel to the Microsoft Defender](/unified-secops-platform/microsoft-sentinel-onboard)​

- Documentation: [Microsoft's unified security operations platform documentation](/unified-secops-platform/)  ​

- Blogs: [FAQ](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Ftechcommunity.microsoft.com%2Fblog%2Fmicrosoftsentinelblog%2Ffrequently-asked-questions-about-the-unified-security-operations-platform%2F4212048&data=05%7C02%7Ccatarinal%40microsoft.com%7Cdde550170daf4040099b08dd79270483%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C638799930724641836%7CUnknown%7CTWFpbGZsb3d8eyJFbXB0eU1hcGkiOnRydWUsIlYiOiIwLjAuMDAwMCIsIlAiOiJXaW4zMiIsIkFOIjoiTWFpbCIsIldUIjoyfQ%3D%3D%7C0%7C%7C%7C&sdata=TDXvftXRO1kjSkiZHRYFg2%2Fj1Sd%2FHCENeQeuMJHSr2Q%3D&reserved=0) \| [FAQ 2](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Ftechcommunity.microsoft.com%2Fblog%2Fmicrosoftsentinelblog%2Funified-security-operations-platform---technical-faq%2F4189136&data=05%7C02%7Ccatarinal%40microsoft.com%7Cdde550170daf4040099b08dd79270483%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C638799930724651830%7CUnknown%7CTWFpbGZsb3d8eyJFbXB0eU1hcGkiOnRydWUsIlYiOiIwLjAuMDAwMCIsIlAiOiJXaW4zMiIsIkFOIjoiTWFpbCIsIldUIjoyfQ%3D%3D%7C0%7C%7C%7C&sdata=N0Et6VOIFEU%2BMk76jVP%2Fdt3Cjrm%2FqamZPvfgNCRqNnU%3D&reserved=0)  ​

- Capability differences: [Microsoft Sentinel in the Microsoft Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal?toc=/microsoft-365/security/defender/toc.json&bc=/microsoft-365/security/defender/breadcrumb/toc.json)  ​

- Alert correlation and incident merging: [Alert correlation and incident merging in the Microsoft Defender portal](/defender-xdr/alerts-incidents-correlation)  ​

- What's new: [What's new in the Microsoft's unified SecOps platform](/unified-secops-platform/) ​

- [Transitioning Microsoft Sentinel into Microsoft Defender](https://www.youtube.com/playlist?list=PL3ZTgFEc7Lyska6WLWBzc8sob-kYA2jPj)– 10 video series:

- Recorded Webinars:

- [Transition to the Unified SOC Platform: Deep Dive and Interactive Q&A for SOC Professionals](https://www.youtube.com/watch?v=WIM6fbJDkK4)

- [The Unified SecOps Experience Using Microsoft Sentinel's Latest Features](https://www.bing.com/videos/riverview/relatedvideo?&q=Microsoft+Unified+SecOps+&&mid=9F8503C52E0CADCA16ED9F8503C52E0CADCA16ED&&FORM=VRDGAR)

- [What's New in Microsoft Sentinel and the Unified Security Operations Platform](https://www.youtube.com/watch?v=bPGI8Yu9ReA)

- [Unlocking the Power of the Unified SecOps: Mastering Multiple Workspaces and Tenants](https://www.youtube.com/watch?v=4MeLsbTT3Uk)

- Case Management: [Explore New Case Management Features](https://www.youtube.com/watch?v=7s1ZHiEfzws&t=4s) and [Exploring Case Management in the Unified SecOps Platform](https://www.youtube.com/watch?v=G-vfMJSL11g&list=PLmAptfqzxVEVeZJO1kj4wiUVhCPfCa0Fm)

- Join our security community: <https://aka.ms/SecurityCommunity>


# Governance Relationships

# Configure delegated access with governance relationships for multitenant organizations (preview)

This article explains how to configure governance relationships for multitenant organizations and managed security service providers (MSSPs) to manage delegated access to customer tenants through the Microsoft Defender portal.

> [!IMPORTANT]

> This feature is currently in preview.

## Overview

Governance relationships enable governing tenants to manage security operations across multiple customer tenants with fine-grained role assignments. This capability supports multitenant organizations (MTOs) and MSSPs that need to provide security services across multiple Microsoft Entra tenants.

This is the same governance relationships model used in [Microsoft Entra ID](/entra/id-governance/tenant-governance/governance-relationships) for delegating administrative access, but extended to support Microsoft Defender XDR workloads. By configuring governance relationships for Microsoft Defender, you can assign specific security roles to groups in the governing tenant, allowing them to manage security incidents, alerts, and configurations in the governed tenant without granting full administrative access.

### Key concepts

- **Governing tenant**: The home tenant that manages access to other tenants (also called *home tenant* or *managing tenant*)

- **Governed tenant**: The customer tenant that grants access to the governing tenant (also called *target tenant* or *managed tenant*)

- **Governance relationship**: directional connection between two Microsoft Entra tenants. One tenant acts as the *governing* tenant, and the other acts as the *governed* tenant.

- **CSP**: Cloud Solution Provider - Microsoft partners who sell cloud services

## Prerequisites

Before you configure delegated access, ensure you meet the following requirements:

Licenses:

- Both tenants require at least one Microsoft Entra ID P1 license.

- Both tenants require at least one Microsoft 365 E5 license or Microsoft Sentinel enabled in Microsoft Defender.

Permissions:

- A user with the [Tenant Governance Relationship Administrator](/entra/identity/role-based-access-control/permissions-reference#tenant-governance-relationship-administrator) role in the governing tenant.

- To send an invitation from the governed tenant, the user must have the [Tenant Governance Administrator](/entra/identity/role-based-access-control/permissions-reference#tenant-governance-administrator) role.

- To assign permissions to a remote tenant group, the user must have the [User Access Administrator](/azure/role-based-access-control/built-in-roles/privileged#user-access-administrator) role in Azure RBAC and at least a [User Administrator](/entra/identity/role-based-access-control/permissions-reference#user-administrator) role in Entra RBAC.

## Enable tenant governance settings

Before you can configure delegated access, you must enable your tenant to receive governance invitations. This setting is disabled by default.

Go to the Delegated access page and turn on the Enable invitations toggle.

## Set up delegated access

The tenant governance setup process involves three steps: the governed tenant sends an invitation, the governing tenant creates and sends an access request, and the governed tenant approves the request.

### Step 1: Send invitation from governed tenant

The governed tenant initiates the relationship by sending an invitation to the governing tenant.

1. In the governed tenant, sign in to the Microsoft Defender portal.

1. Navigate to **System** > **Permissions** > **Delegated Access**.

1. Select **Send invitation**.

1. Enter the tenant ID of the governing tenant that you want to invite.

1. Select **Send** to send the invitation.

### Step 2: Create and send access request from governing tenant

After it receives the invitation, the governing tenant creates a relationship template that defines delegated access permissions.

1. In the governing tenant, sign in to the Microsoft Defender MTO portal.

1. Navigate to **System** > **Delegated Access**.

1. Select **Create access template**.

1. Define the access template with the following information:

- **Template name**: A descriptive name for this access template

- **Microsoft Entra built-in roles**: Select one or more roles to assign

- **Security groups**: Select security groups from your governing tenant that will receive the assigned roles

1. Select **Send relationship request**.

1. Select the governed tenant that invited you, then select **Submit**.

### Step 3: Approve access request in governed tenant

The governed tenant administrator reviews and approves the delegated access request.

1. In the governed tenant, sign in to the Microsoft Defender portal.

1. Navigate to **System** > **Permissions** > **Microsoft XDR permissions**.

1. Review the pending access request and select **Approve** or **Reject**.

1. After approval, you'll see a confirmation message.

After the approval is complete, users in the specified security groups receive permissions in the governed tenant based on the defined roles.

## Configure tenant governance permissions for Microsoft Sentinel

Security groups used in the relationship template are synchronized to the governed tenant as "remote tenant groups." You can assign these groups to Microsoft Sentinel roles in the governed tenant to enable multitenant management capabilities.

You can assign these groups to Azure Resource Manager (ARM) resources to enable Microsoft Sentinel management capabilities.

Assigning Microsoft Sentinel roles enables multitenant management features including:

- Alert and incident management

- Threat intelligence

- Hunting

- Content distribution

- Direct management through the Defender portal

### Assign permissions to resource group

Follow these steps to grant Microsoft Sentinel permissions to your delegated access groups.

1. In the governed tenant, sign in to the [Azure portal](https://portal.azure.com).

1. Navigate to your resource group.

1. Select **Access Control (IAM)**.

1. Select **Add** > **Add role assignment**.

1. Select the Microsoft Sentinel role you want to assign (for example, Microsoft Sentinel Contributor).

1. On the **Members** tab, under **Assign access to**, select **Remote tenant group**.

1. Select the synchronized security groups from the governing tenant.

1. Select **Review + assign** to complete the assignment.

## Troubleshooting

### Security group not displayed when creating a template

**Symptom**: Your security group doesn't appear in the list when creating a relationship template.

**Cause**: Only security groups that meet specific criteria are supported for governance relationships delegation.

**Resolution**: Ensure your security group meets the following requirements:

- SecurityEnabled property is set to true

- IsAssignableToRole property is set to true

- Not a Microsoft 365 group (unified group)

Security groups that don't meet these criteria aren't supported for governance relationships delegation.

## Related content

- [Microsoft Entra governance relationships](/entra/id-governance/tenant-governance/governance-relationships)

- [MSSP portal access](/defender-xdr/mssp-access)


# Mto Requirements

# Set up Microsoft Defender multitenant management

This article describes the steps you need to take to start using multitenant management for Microsoft Defender XDR and Microsoft Sentinel in the Defender portal.

1. [Review the requirements](#review-the-requirements)

2. [Verify your tenant access](#verify-your-tenant-access)

3. [Set up Microsoft Defender multitenant management](#set-up-multitenant-management)

>[!Note]

>- In multitenant management, interactions between the multitenant user and the managed tenants could involve accessing data and managing configurations. The ability to undertake these actions is determined by the permissions a managed tenant has granted the multitenant user.

>- [Data privacy](/defender-xdr/data-privacy), [role-based access control (RBAC)](/defender-xdr/m365d-permissions) and [Licensing](/defender-xdr/prerequisites#licensing-requirements) are respected by Microsoft Defender multi-tenant management.

## Review the requirements

The following table lists the basic requirements you need to use multitenant management for Microsoft Defender XDR and Microsoft Sentinel in the Defender portal.

| Requirement | Description |

|:---|:---|

| Microsoft Defender XDR prerequisites | Verify you meet the [Microsoft Defender XDR prerequisites](/defender-xdr/prerequisites)|

| Microsoft Defender XDR for US Government customers | Check if you have the following applicable [licensing requirements](/defender-xdr/usgov#licensing-requirements)|

| Multitenant access | To view and manage the data you have access to in multitenant management, you need to ensure you have the necessary access. <br><br>**For Microsoft Defender data**, you must have either: <br>- [Granular delegated admin privileges (GDAP)](/partner-center/gdap-introduction)<br/>- [Microsoft Entra B2B authentication](/azure/active-directory/external-identities/what-is-b2b)<br><br>**To run cross-tenant queries on Microsoft Sentinel data**, you must set up [Azure Lighthouse](/azure/lighthouse/overview). For example, to run cross-workspace queries with the `workspace()` operator in advanced hunting and analytics rules.|

| Permissions | Users must be assigned the correct roles and permissions at the individual tenant level, in order to view and manage the associated data in multitenant management. To learn more, see: <br/><br/> - [Manage access to Microsoft Defender XDR with Microsoft Entra global roles](/defender-xdr/m365d-permissions) <br/> - [Custom roles in role-based access control for Microsoft Defender XDR](/defender-xdr/custom-roles)<br/><br/> To learn how to grant permissions for multiple users at scale, see [What is entitlement management](/azure/active-directory/governance/entitlement-management-overview).|

| Security information and event management (SIEM) data (Optional) |To include SIEM data with the extended detection and response (XDR) data, one or more tenants must include a Microsoft Sentinel workspace onboarded to Microsoft Defender. For more information, see [Connect Microsoft Sentinel to Microsoft Defender XDR](microsoft-sentinel-onboard.md).<br/><br/>The Defender portal allows you to connect to one primary workspace and multiple secondary workspaces for Microsoft Sentinel. For more information, see [Multiple Microsoft Sentinel workspaces in the Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2310579).<br/><br/> Access to Microsoft Sentinel data is available through [Microsoft Entra B2B authentication](/azure/active-directory/external-identities/what-is-b2b). Microsoft Sentinel doesn't support [granular delegated admin privileges (GDAP)](/partner-center/gdap-introduction) at this time. |

We recommend that you set up [multifactor authentication trust](/azure/active-directory/external-identities/authentication-conditional-access) for each tenant to avoid missing data in Microsoft Defender multitenant management.

## Verify your tenant access

In order to view and manage the data you have access to in Microsoft Defender multitenant management, you need to ensure you have the necessary permissions. For each tenant you want to view and manage, you need to either:

- [Verify your tenant access with Microsoft Entra B2B](#verify-your-tenant-access-with-microsoft-entra-b2b)

- [Verify your tenant access with GDAP](#verify-your-tenant-access-with-gdap)

### Verify your tenant access with Microsoft Entra B2B

1. Go to [My account](https://myaccount.microsoft.com/organizations).

2. Under **Organizations > Other organizations you collaborate with** see the list of organizations you have guest access to.

3. Verify all the tenants you plan to manage appear in the list.

4. For each tenant, go to the [Microsoft Defender portal](https://security.microsoft.com/?tid=tenant_id) and sign in to validate you can successfully access the tenant.

### Verify your tenant access with GDAP

GDAP is not supported for Microsoft Sentinel data, and provides access to Defender data only.

1. Go to the [Microsoft Partner Center](https://partner.microsoft.com/commerce/granularadminaccess/list).

2. Under **Customers** you can find the list of organizations you have guest access to.

3. Verify all the tenants you plan to manage appear in the list.

4. For each tenant, go to the [Microsoft Defender portal](https://security.microsoft.com/?tid=tenant_id) and sign in to validate you can successfully access the tenant.

## Set up multitenant management

The first time you use Microsoft Defender multitenant management, you need setup the tenants you want to view and manage. To get started:

1. Sign in to [Microsoft Defender multitenant management](https://mto.security.microsoft.com/)

2. Select **Add tenants**.

3. Choose the tenants you want to manage and select **Add**

> [!Note]

> The Microsoft Defender multitenant view currently has a limit of 100 target tenants.

The features available in multitenant management now appear on the navigation bar and you're ready to view and manage security data across all your tenants.

## Next step

Use these articles to get started with Microsoft Defender multitenant management:

- [View and manage incidents and alerts](mto-incidents-alerts.md)

- [Advanced hunting](mto-advanced-hunting.md)

- [Multitenant devices](mto-tenant-devices.md)

- [Vulnerability management](mto-dashboard.md)

- [Manage tenants](mto-tenants.md)


# Mto Incidents Alerts

# View and manage incidents and alerts in Microsoft Defender multitenant management

Multi-tenant management for Microsoft Defender XDR and Microsoft Sentinel in the Defender portal enables security operation center (SOC) analysts to access and analyze data from multiple tenants and workspaces in one place, allowing them to quickly identify and respond to threats. Triage incidents and alerts across security information and event management (SIEM) and extended detection and response (XDR) data for tenants that onboarded a Microsoft Sentinel workspace to the Defender platform.

Manage incidents & alerts originating from multiple tenants and workspaces under **Incidents & alerts**.

## View and investigate incidents

To view or investigate an incident:

1. Go to the [Incidents page](https://mto.security.microsoft.com/incidents) in Microsoft Defender multitenant management. The **Tenant name** and **Workspaces** columns show which tenant the incident originates from:

1. Select the incident you want to view. A flyout opens with the incident details pane, where you can:

- Select **Open incident page** to view this incident in a new tab for the specific tenant in the [Microsoft Defender portal](https://security.microsoft.com).

- Select **Manage incident** to assign the incident, set incident tags, set the incident status, and classify the incident.

To learn more, see [Investigate incidents](/defender-endpoint/investigate-incidents).

## Manage multiple incidents

To manage incidents across multiple tenants and workspaces:

1. Go to the [Incidents page](https://mto.security.microsoft.com/incidents) in Microsoft Defender multitenant management.

2. Choose the incidents you want to manage from the incidents list and select **Manage incidents**.

On the incidents flyout pane you can assign incidents, assign incidents tags, set the incident status, and classify multiple incidents for multiple tenants simultaneously.

>[!Note]

> Currently, you can only assign multiple incidents from same tenant.

To learn more about incidents in the Microsoft Defender portal, see [Manage incidents](/defender-endpoint/manage-incidents).

## View and investigate alerts

To view or investigate an alert:

1. Go to the [Alerts page](https://mto.security.microsoft.com/alerts) in multitenant management and select the alert you want to view. A flyout panel opens with the alert details page:

1. From the alert details pane you can:

- Select actions such as **Open alerts page**, **Move alert to another incident**, and **Tune alert** to view this alert in a new tab for the specific tenant in the [Microsoft Defender portal](https://security.microsoft.com).

- Select **Manage alert** to assign the alert, set the alert status, and classify the alert.

To learn more, see [Investigate alerts](/defender-endpoint/investigate-alerts).

## Manage multiple alerts

To manage alerts across multiple tenants and workspaces:

1. Go to the [Alerts page](https://mto.security.microsoft.com/alerts) in Microsoft Defender multitenant management.

1. Choose the alerts you want to manage from the alerts list and select **Manage alerts**.

Use the **Manage alerts** pane to set alert status, assign alerts, set classifications, and add comments for multiple alerts simultaneously. While alert status, classifications, and comments can be added across tenants, assigning alerts can only be done for alerts from the same tenant.

For more information, see [Manage alerts](/defender-xdr/investigate-alerts#manage-alerts).

## Move alerts

Move an alert to a different incident to help you better organize and correlate related security events. For example, you might find that multiple alerts are part of the same security breach, and want to include them all in the same incident. This ensures that all relevant information is grouped together, enabling more efficient investigation and response.

To move one or more alerts:

- On the **Alerts** page, select one or more alerts and then select **Move alerts**

- On an alert details pane or alert details page, select **Move alert to another incident**

In the **Move alert to another incident** pane, define whether you want to create a new incident, or use an existing incident. If you choose to use an existing incident, search for the incident by name or ID and add a reason for the change. In all cases, add a comment describing your change before you select **Save**.

## Related content

- [Set up Microsoft Defender multitenant management](mto-requirements.md)

- [Connect Microsoft Sentinel to Microsoft Defender XDR](microsoft-sentinel-onboard.md)

- [Advanced hunting in Microsoft Defender multitenant management](mto-advanced-hunting.md)

- [Multiple Microsoft Sentinel workspaces in the Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2310579)


# Mto Manage Cases

# View and manage cases across multiple tenants in the Microsoft Defender multitenant portal

Case management in the [**Microsoft Defender multitenant portal**](https://mto.security.microsoft.com) allows you to view and manage security operations (SecOps) cases from multiple tenants in a single queue. Case management supports a number of use cases:

- Define your own case workflow with custom status values

- Assign tasks to collaborators and configure due dates

- Handle escalations and complex cases by linking multiple incidents to a case

- Manage access to your cases using RBAC

- Manage cases from multiple tenants

## View cases in the multitenant portal

The cases experience in the multitenant portal is just like [that in the regular, single-tenant portal](cases-overview.md), but with a few extra features:

- The **Cases** queue contains columns for **Tenant** and **Tenant ID**, so you can see which tenant each case belongs to.

- If you are managing many tenants, you can search, sort, or filter the case queue by tenant. The existing sort, filter, and search capabilities also work across multiple tenants in one combined view.

- Role-based access control (RBAC) settings are applied at the tenant level, so you only see cases from the tenants you have access to.

For more information, see [Manage security operations cases natively in the Microsoft Defender portal](cases-overview.md).

## Manage a case in the multitenant portal

Manage cases from multiple tenants at a glance in the multitenant case queue.

- To see a preview flyout panel of a case's details, select the row of the desired case.

- To open a case's full details page, select the case's name.

Navigate effortlessly between cases in different tenants without leaving the multitenant queue or losing context.

For more information on managing cases, see [Manage security operations cases natively in the Microsoft Defender portal](cases-overview.md)

## Create a case in the multitenant portal

1. On the **Cases** page in the multitenant portal, select **+ Create**.

1. In the **Create case** pane, select the desired tenant from the drop-down at the top, then proceed as in the single-tenant experience.

The maximum allowed per tenant is 100,000 cases.

## Related content

- [Manage security operations cases natively in the Microsoft Defender portal](cases-overview.md)

- [Microsoft Defender multitenant management](mto-overview.md)

- [Microsoft Sentinel blog - Improve SecOps collaboration with case management](https://techcommunity.microsoft.com/blog/MicrosoftSentinelBlog/improve-secops-collaboration-with-case-management/4369044)

- [Microsoft Sentinel in the Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal)


# Mto Advanced Hunting

# Advanced hunting in Microsoft Defender multitenant management

Advanced hunting in Microsoft Defender multitenant management allows you to proactively hunt for intrusion attempts and breach activity in email, data, devices, and accounts across multiple tenants and workspaces at the same time. If you have multiple tenants with Microsoft Sentinel workspaces onboarded to the Microsoft Defender portal, search for security information and event management (SIEM) data together with extended detection and response (XDR) data across multiple tenants and workspaces.

Multiple workspaces per tenant are supported in multitenant Advanced hunting as preview.

## Quotas

In multitenant environments, advanced hunting queries can return a maximum of 50,000 records in total. The result set from each individual tenant is capped at 50,000 divided by the number of tenants queried.

For more information about service limits in advanced hunting, read [Understand advanced hunting quotas](/defender-xdr/advanced-hunting-limits#understand-advanced-hunting-quotas-and-usage-parameters).

## Run cross-tenant queries

You can run any query that you already have access to in the multitenant management **Advanced hunting** page.

1. Queries listed on the **Queries** tab are filtered by tenant. Select a tenant to view the queries available for each one.

1. Load a query in the query editor and select the tenant selector to specify the tenants and workspaces you want to run the query against.

1. In the side pane that opens, select the tenants you want to include in the query. Each tenant supports a single workspace. If you have multiple workspaces onboarded to the Defender portal in your tenant, select **Edit selection** to select the workspace you want to use.

When you select multiple tenants, the query runs independently in each tenant, and the combined results are displayed in a single table. For example, the sample query below (`DeviceEvents | take 10`) returns 10 results per tenant, resulting in a total equal to 10 multiplied by the number of tenants selected.

1. When you're done, select **Apply** > **Run query**.

The query results contain a column named **TenantId**. If you're using multiple workspaces, the values in this column show the workspace ID instead of the tenant ID. In such cases, we recommend that you use your query to rename the column in your results from **TenantId** to **WorkspaceId** to make it simpler to read. For example:

```kusto

DeviceEvents

| take 10

| project TenantId = WorkspaceID

```

Or, to query multiple workspaces in the same tenant, use a query similar to the following:

```kusto

Usage

| union workspace("WorkpaceA").Usage

| take 10

```

>[!IMPORTANT]

> Running queries across multiple tenants using the `adx(x)` operator will run separate ADX queries per tenant and aggregate them, which might return duplicate results. Use the `adx(x)` operator with multiple tenants only if you need to join tenant results with ADX data. For more information about ADX in Advanced hunting, see [Use Microsoft Sentinel functions, saved queries, and custom rules](/defender-xdr/advanced-hunting-defender-use-custom-rules#use-adx-operator-for-azure-data-explorer-queries).

To learn more about advanced hunting in Microsoft Defender XDR, read [Proactively hunt for threats with advanced hunting in Microsoft Defender XDR](/defender-xdr/advanced-hunting-overview).

## Run cross-workspace queries

To run queries across multiple workspaces in the same tenant, use the [workspace( ) expression](/azure/azure-monitor/logs/cross-workspace-query#query-across-log-analytics-workspaces-using-workspace), with the workspace identifier as the argument in your query to refer to a table in a different workspace.

If you're using [Azure Lighthouse](/azure/lighthouse/overview) to grant your tenant with permissions to other tenants workspaces, you can also query across both tenants and workspaces. To do so, select only one tenant in the **Tenant scope** selector. Then in the query, use the `workspace()` expression to call the names of any other workspaces you want to query in other tenants. For example, if you have tenants and workspaces named as follows:

- **TenantA**: *WorkspaceA1*, *WorkspaceA2*

- **TenantB**: *WorkspaceB1*, *WorkspaceB2*

And if you want to query across both *WorkspaceA1* and *WorkspaceB1*, select **TenantA** and **WorkspaceA1** in the **Tenant scope** selector. Then in your query, use the `workspace()` operator to call *WorkspaceB2*. For example:

```kusto

union workspace("WorkspaceB2").Usage, Usage

| where TimeGenerated > ago(1d)

| summarize TotalRecords = count() by Workspace = TenantId

```

Results show from both *WorkspaceA1* and *WorkspaceB2*.

For more information, see [Query multiple workspaces](/azure/sentinel/extend-sentinel-across-workspaces-tenants#query-multiple-workspaces) and [Manage workspaces across tenants using Azure Lighthouse](/azure/sentinel/extend-sentinel-across-workspaces-tenants#manage-workspaces-across-tenants-using-azure-lighthouse).

> [!NOTE]

> If you have tables with the same name but different schemas in multiple workspaces and want to use them in the same query, you should use the workspace operator to uniquely identify the table that you need.

## View schema tables

View the [advanced hunting schema tables](/defender-xdr/advanced-hunting-schema-tables) in the left pane inside the advanced hunting page under the **Schema** tab.

The schema list is a unified view of all tables from all your tenants regardless of the tenant selected in the upper right tenant selector.

This could mean that some tables that appear here might only be available for query in some tenants, like custom Microsoft Sentinel tables.

## View and manage custom detection rules

You can also manage custom detection rules from multiple tenants in the custom detection rules page.

### View custom detection rules by tenant

1. To view custom detection rules, go to the [Custom detection rules page](https://mto.security.microsoft.com/v2/custom_detection) in Microsoft Defender multitenant management.

2. View the **Tenant name** column to see which tenant the detection rule comes from:

To view only a specific tenant's custom detection rules, select **Filter**, choose the tenant or tenants and select **Apply**.

To read more about custom detection rules, read [Custom detections overview](/defender-xdr/custom-detections-overview).

### Manage custom detection rules

You can **Run**, **Turn off**, and **Delete** detection rules from Microsoft Defender multitenant management.

To manage detection rules:

1. Go to the [Custom detection rules page](https://mto.security.microsoft.com/v2/custom_detection) in Microsoft Defender multitenant management.

1. Choose the detection rule you want to manage.

When you select a single detection rule, a flyout panel opens with the detection rule details:

1. Select **Open detection rules** to view this rule in a new tab for the specific tenant in the [Microsoft Defender portal](https://security.microsoft.com). To learn more, see [Custom detection rules](/defender-xdr/custom-detection-rules).

## Related content

- [Set up Microsoft Defender multitenant management](mto-requirements.md)

- [Connect Microsoft Sentinel to Microsoft Defender XDR](microsoft-sentinel-onboard.md)

- [View and manage incidents and alerts](mto-incidents-alerts.md)

- [Multiple Microsoft Sentinel workspaces in the Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2310579)


# Mto Tenant Devices

# Devices

**Applies to:**

- [Microsoft Defender XDR](/defender-xdr/microsoft-365-defender)

The **Devices** page in multitenant management enables you to quickly manage tenants and devices.

## Tenant device list

The Tenants page in multitenant management lists each tenant you have access to. Each tenant page includes details such as the number of devices and device types, the number of high value and high exposure devices, and the number of devices available to onboard:

At the top of the page, you can view the number of tenants and the number of devices onboarded or discovered, across all tenants. You can also see the aggregate number of devices identified as:

- High risk

- High exposure

- Internet facing

- Can be onboarded

- Newly discovered

- High value

Select a tenant name to navigate to the device inventory for that tenant in the [Microsoft Defender XDR](https://security.microsoft.com/machines) portal where all data and inventory-related actions are available.

## Device inventory

The Device inventory page lists all the devices in each tenant that you have access to. The page is like the [Defender for Endpoint device inventory](/defender-endpoint/machines-view-overview) with the addition of the **Tenant name** column. Moreover, the device inventory page doesn't have the network, IOT, and uncategorized devices tabs.

You can navigate to the device inventory page by selecting **Assets > Devices** in Microsoft Defender XDR's navigation menu.

The total number of devices, critical assets, high risk devices, and internet-facing devices for all tenants are shown at the top of the page.

You can search a specific device with the search function. You can sort and filter the device list according to the following fields to customize your view:

- Tenant name

- Risk level

- Criticality level

- Mitigation status

- Cloud platforms

- Operating system (OS) platforms

- Windows OS version

- Sensor health state

- Antivirus status

- Tags

- First seen

- Internet facing

- Group

- Exclusion state

- Managed by

To manage a device, select a specific device from the list. Device management tasks like managing tags, device exclusion, and reporting inaccuracy becomes available at the top of the device list.

Selecting a device by clicking on the device name opens the device page in a new tab. You can further apply other actions on the device in the new tab.


# Multitenant Identities Inventory

# Identities

The **Identities** page in multitenant management enables you to quickly manage tenants and identities.

## Identity inventory

The Identity inventory page lists all the identities in each tenant that you have access to. The page is like the [Defender for Identity inventory](/defender-for-identity/identity-inventory) with the addition of the **Tenant name** column and filter.

You can navigate to the identity inventory page by selecting **Assets > Identities** in Microsoft Defender XDR's navigation menu.

At the top of the page, the following identities counts are available for all tenants:

**Total**: The total number of identities.

**Critical:** The number of your critical assets.

**Disabled:** The number of all disabled identities in your organization.

**Services:** The number of all service accounts both on-premises and cloud.

You can use this information to help you prioritize identities for security posture improvements.

Highly privileged identities card helps you investigate in Advanced hunting all sensitive accounts in your organization, including Microsoft Entra ID security administrators and Global admin users.

There are several options you can choose from to customize the identities list view. On the top navigation you can:

- Add or remove columns.

- Apply filters.

- Search for an identity by name or full UPN, SID, and Object ID.

- Export the list to a CSV file.

- Copy list link with the included filters configured.

> [!NOTE]

> When exporting the identities list to a CSV file, a maximum of 5,000 identities are displayed.

To view full identity details, select a specific identity from the list. Tenant ID and Tenant name are available in the identity side panel and page:


# Mto Dashboard

# Vulnerability management in multi-tenant management

**Applies to:**

- [Microsoft Defender XDR](/defender-xdr/microsoft-365-defender)

## Microsoft Defender Vulnerability Management dashboard

You can use the Defender Vulnerability Management dashboard in multi-tenant management to view aggregated and summarized information across all tenants, such as:

- Your exposure score and exposure level for devices across all tenants.

- Your most exposed tenants along with details of the number of weaknesses, exposed devices, and available recommendations for each tenant.

The Defender Vulnerability Management dashboard in multi-tenant management provides the following information across all the tenants you have access to:

|Area|Description|

|---|---|

|**Organization Exposure score**|See the current state of your organization's device exposure to threats and vulnerabilities across all tenants.|

|**Most exposed tenants**|Real time visibility into the tenants with the highest current exposure level.|

|**Tenants with the largest increase in exposure**|Identify tenants with the largest increase in exposure over the last 30 days.|

|**Device exposure distribution**|See how many devices are exposed based on their exposure level, across all tenants. Select a section in the doughnut chart to see the number of exposed devices at each level.|

|**Tenant exposure distribution**|View a summary of exposed tenants aggregated by exposure level.|

## Tenant vulnerability details

The **Tenants page** under **Vulnerability management** includes vulnerability information for all tenants, and at a tenant-specific level, such as exposed devices, security recommendations, weaknesses, and critical CVEs.

At the top of the page, you can view the number of tenants and the aggregate number of:

- Exposed devices

- Critical CVEs

- High severity CVEs

- Security recommendations

Select a tenant name to navigate to the Defender Vulnerability Management dashboard for that tenant in the [Microsoft Defender XDR](https://security.microsoft.com/machines) portal.

For more information, see [Microsoft Defender Vulnerability Management dashboard](/defender-vulnerability-management/tvm-dashboard-insights).

## Related articles

- [Exposure score](/defender-vulnerability-management/tvm-exposure-score)

- [Security recommendations](/defender-vulnerability-management/tvm-security-recommendation)


# Mto Tenants

# Manage tenants with Microsoft Defender multitenant management

Add or remove tenants from the settings page in Microsoft Defender multitenant management.

## View the tenants page

To view the list of tenants that appear in multitenant management, go to [Settings page](https://mto.security.microsoft.com/mtosettings) in Microsoft Defender multitenant management:

From the **Settings** page you can:

- **Add a tenant**: Select **Add tenants** > Choose the tenants to want to add > Select **Add tenant**.

- Select a tenant from the list to open the [Microsoft Defender portal](https://security.microsoft.com) for that tenant.

- **Remove a tenant**: Select the tenant you'd like to remove > select **Remove**.

## Multitenant management status indicator

The multitenant management status indicator provides information on whether data issues exist for the page you're viewing, such as data loading issues or permissions issues. The indicator appears in the bottom right corner of the page:

When no issue exists, the status indicator is a green tick:

- ![No data issues](media/mto-tenants/mto_nodata_issue.png)

When an issue exists, the status indicator shows a red warning sign:

- ![data issues](media/mto-tenants/mto-data-issues.png)

Hovering over the red warning sign displays the issues that occurred and the tenant information. By expanding each section, you see all the tenants with this issue.

- ![tenant data issues](media/mto-tenants/mto-tenantdata-issues.png)

## Related content

- [Microsoft Defender multitenant management](mto-overview.md)

- [Set up Microsoft Defender multitenant management](mto-requirements.md)


# Mto Tenant Groups

# Create and manage tenant groups in Microsoft Defender multitenant management

Tenant groups in Microsoft Defender multitenant management let you organize the tenants you manage into named collections and switch the multitenant view between them. Use tenant groups to focus on a specific set of tenants, such as those that belong to a single customer, business unit, or geographic region, instead of viewing every tenant you have access to at once.

> [!NOTE]

> The previous use of *tenant groups* for content distribution is now called [distribution profiles](mto-distribution-profiles.md). The name *tenant groups* now refers to the groups of tenants you create to switch the multitenant view, as described in this article.

## Prerequisites

Before you can create tenant groups, onboard your tenants to the Microsoft Defender multitenant portal. Only tenants that are already onboarded appear when you create or edit a tenant group. For more information, see [Set up Microsoft Defender multitenant management](mto-requirements.md) and [Manage tenants with Microsoft Defender multitenant management](mto-tenants.md).

## Permissions

To access tenant groups, you need the following permissions.

**Microsoft Entra ID roles**

- [Security Administrator](/entra/identity/role-based-access-control/permissions-reference#security-administrator)

- [Security Operator](/entra/identity/role-based-access-control/permissions-reference#security-operator)

**Product-specific RBAC (for example, Microsoft Defender for Endpoint or Microsoft Defender for Identity)**

- [Security Administrator](/entra/identity/role-based-access-control/permissions-reference#security-administrator)

- Custom RBAC roles that grant visibility across products. See [Custom roles for role-based access control](/defender-xdr/custom-roles).

**[Unified role-based access control (URBAC)](/defender-xdr/manage-rbac)**

- *Security / read* to view tenant groups

- *Security / manage* to create tenant groups

For more information about URBAC permissions in the multitenant portal, see [Manage unified role-based access control (URBAC) for multitenant management](mto-urbac.md).

Users only see the tenants they have permission to see through B2B or [granular delegated admin privileges (GDAP)](/partner-center/gdap-introduction), even when a tenant group contains more tenants than the user can access.

## Access tenant groups

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) with appropriate administrative credentials.

1. Go to **Multi-tenant management** > **Tenant groups**.

The first time you open the page, you see **My private group**, which contains all tenants from your previous multitenant settings. You can add or remove tenants from **My private group**, but you can't delete it.

## Create a tenant group

1. On the **Tenant groups** page, select **+ Create tenant group**.

1. Enter a descriptive name for the tenant group.

1. Optionally, enter a description.

1. Select the tenants you want to add to the group.

1. Select **Create**.

## Switch the view between tenant groups

1. In the top-left corner of the multitenant portal, select **Open multitenant management**.

1. Select the tenant group you want to view.

After you switch groups, browse the different views in the multitenant portal and confirm that the data shown comes only from the tenants in the selected group.

If someone edits a tenant group (by adding or removing tenants) while you have a view open for that group, the portal shows a notification that a change was detected. Refresh the view to load data for the updated set of tenants.

## Edit a tenant group

1. Go to **Multi-tenant management** > **Tenant groups**.

1. Select the tenant group you want to change, and then select **Edit**.

1. Add or remove tenants as needed, and then save your changes.

1. Switch the view to the edited tenant group to confirm the data reflects the updated membership.

## Related content

- [Microsoft Defender multitenant management](mto-overview.md)

- [Manage tenants with Microsoft Defender multitenant management](mto-tenants.md)

- [Content distribution using distribution profiles in multitenant management](mto-distribution-profiles.md)


# Mto Endpoint Security Policy

# Endpoint security policies in multitenant management

Microsoft Defender for Endpoint security policies help you manage security settings across your devices. In the Microsoft Defender multitenant management portal, the **Endpoints > Configuration management > Endpoint security policies** page allows you to manage security settings on your tenants' devices across multiple tenants.

For more information, see [Manage endpoint security policies in Microsoft Defender for Endpoint](/defender-endpoint/manage-security-policies).

## Prerequisites

- You must have Microsoft Defender for Endpoint to use endpoint security policies in multitenant management.

- Security administrators must have permissions in each tenant to access the endpoint security policies page in multitenant management.

- The **Endpoint security policies** page is available only for [users with the security administrator role in Microsoft Defender XDR](/defender-endpoint/assign-portal-access). Other user roles, like Security Reader, don't provide access to the **Endpoint security policies** page.

When a user has the required permissions to view policies in the Microsoft Defender portal, the data is presented based on Intune permissions. If the user is in scope for Intune role-based access control, it applies to the list of policies presented in the Microsoft Defender portal.

We recommend granting security administrators with the [Intune built-in role "Endpoint Security Manager"](/intune/intune-service/fundamentals/role-based-access-control#built-in-roles) to effectively align the level of permissions between Intune and Microsoft Defender XDR.

## Create a new or edit an existing security policy

Use the same procedure to create a new endpoint security policy in the multitenant management portal as you would in the single tenant portal. For more information, see [Create an endpoint security policy](/defender-endpoint/manage-security-policies#create-an-endpoint-security-policy).

Differences include:

- Before you start, select the tenant for which you want to create the policy. Each policy is created for a specific tenant, and you can only create policies for one tenant at a time.

For example:

- To edit the scope tags, you'll need to go to the [Microsoft Intune admin center](https://intune.microsoft.com/). Editing scope tags must be done in the single tenant portal as multitenant management is not yet supported in the Intune admin center.

Use the **Search** and **Filter** options to find a specific policy in the **Endpoint security policies** page. You can filter policies by tenant name, policy category, policy type, and targets.

Edit or delete a security policy by selecting the policy in the Endpoint security policies page, then selecting **Edit** or  **Delete**. For example:

## Verify endpoint security policy status

To verify that you have successfully created a policy, select the policy from the list and click on the policy name to open the policy page. You can also view the policy page through **Edit > Open policy page**. The policy page opens in a new tab.

The policy page displays details of an endpoint security policy, including the status, which devices the policy applies to, and the assigned groups.

You can also view the policy in the Microsoft Intune admin center. To do so, select the More actions ellipsis (…) in the policy page, then select **View in Intune**.

## View distributed policies

Endpoint security policies that are distributed across tenants with the multitenant management portal appear in a hierarchical view, with the original policy serving as the parent. You can find the policies that were distributed from your tenant under the original policy. For example:

The **Last Distribution Status** for the original policy reflects the overall status of its distributed copies, and the **Tenants** and **Distribution profiles** columns indicate the distribution profile recipients of the policy. For more information, see [Content distribution in multitenant management](mto-distribution-profiles.md).

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/defender-m3d-techcommunity.md)]


# Mto Distribution Profiles

# Content distribution in multitenant management

Content distribution in the Microsoft Defender multitenant portal helps you organize and manage content at scale across your tenants, based on categories like business groups or locations. Create distribution profiles to copy existing content, like custom detection rules, from the source tenant to the target tenants. The distributed content then runs in the target tenant in the selected scope.

## Supported content for distribution

Create distribution profiles to distribute the following types of content across multiple tenants:

- [Custom detection rules](/azure/sentinel/compare-analytics-rules-custom-detections)

- [Endpoint security](/defender-endpoint/microsoft-defender-endpoint) policies, supported for Microsoft Defender for Endpoint customers only

- [Analytics rules](/azure/sentinel/scheduled-rules-overview?) for Microsoft Sentinel customers only

- [Automation rules](/azure/sentinel/create-manage-use-automation-rules)for Microsoft Sentinel customers only

- [Workbooks](/azure/sentinel/monitor-your-data) for Microsoft Sentinel customers only

- Parsers, Saved Searches and Functions

## Prerequisites

The following table lists the requirements for using content distribution in the Microsoft Defender multitenant portal.

| Requirement | Description |

|:---|:---|

|**Licensing requirements** | Your organization must have a subscription to Microsoft 365 E5 or Office E5. To distribute Microsoft Sentinel content, you must have a Microsoft Sentinel subscription|

|**Permissions** | Users must be assigned the correct roles and permission at the individual tenant level to view and manage the associated data in multitenant management. <br/> Access to content distribution is granted through the Security settings (manage) or Security Data Basic (read) permission in [Microsoft Defender unified role-based access control (URBAC)](/defender-xdr/manage-rbac). By default, both of these roles are assigned to the **Security Administrator** and **Security Reader** Microsoft Entra built-in roles.|

|**Delegate access** |Delegated access via [Azure B2B](/entra/external-id/add-users-administrator) or [GDAP (CSP Parters only)](/microsoft-365/lighthouse/m365-lighthouse-setup-gdap) must be obtained for at least one other tenant.|

## Create distribution profiles

To create a new distribution profile:

1. In the Microsoft Defender multitenant portal, go to the [**Multi-tenant management > Content distribution**](https://mto.security.microsoft.com/contentdistribution) page.

1. Select **Create** to open the **Create content distribution profile** wizard. In the wizard, enter the following details, selecting **Next** as needed to navigate through the tabs. Some tabs are only relevant if you selected that type of content to distribute.

|Tab  |Instructions  |

|---------|---------|

|**Details**     | Enter a name and optional description for your content distribution profile.        |

|**Assign tenants**     |    Select **Add tenant** to see a list of available tenants that you can add to your distribution profile, select the tenants you want to add, and then select **Add**.     |

|**Select content type**     | Content types are all selected by default. Verify that the selection matches the content you want to distribute in this distribution profile.      |

|**Content type**      | 1. Select **Add content**. <br>2. Select the relevant content that you want to add to the distribution profile, and then select **Add to distribution profile**.         |

At this point, you need to define your tenant's scope. Distribution profiles support a single scope for the entire profile, or separate scopes per content type. Scopes can be device groups, workspaces, or Microsoft Entra groups.

Select **Single scope** or **Scope per content type** to toggle between these options, and **Edit scope** to make changes as needed.

1. In the **Summary** tab, review the details of the distribution profile you created. If you want to sync all authorized tenants now, leave the **Sync all authorized tenants** option checked. If you want to sync later, uncheck it.

1. Select **Submit** to finish your distribution profile creation.

If you chose to **Sync all authorized tenants**, all the tenants and scope within the tenants you have permission automatically syncs.

Your newly created distribution profile appears in the distribution profiles page after creation.

Select a distribution profile from the list to add or remove content, add, edit, or remove tenants, or sync the distribution profile. Use the toolbar options at the top of the page to edit, remove, or sync distribution profiles.

If you're syncing the profiles, check the sync results under the **Last sync result** column. If the result is *partially successful* or *failed*, select the result to investigate the cause. When you select the result, a side pane containing the errors, recommendations, and impacted assets appears. For example:

> [!NOTE]

> The maximum number of published items per publish operation is 9,500. Published items are calculated as the number of tenants multiplied by the number of templates. For example, if you publish 10 distribution profiles with 10 target tenants and 95 content templates, then the published items equals to 9,500.

## Syncing content among distribution profiles

To sync content across distribution profiles for the tenants you have permission for:

1. On the **Multi-tenant management > [Content distribution](https://mto.security.microsoft.com/contentdistribution)** page, select any distribution profiles you want to sync, and then select **Sync**.

1. At the prompt, select **Sync** again to confirm the sync operation. Once the sync is completed, you see one of the following statuses:

- Success

- Partially successful

- Failure

1. If you experience a partial success or failure, select the value in the **Last sync result** column to investigate the cause.

Sync results show the number of synced tenants and content. Synced tenants indicate how many tenants had custom detection rules applied successfully.

For example, if all rules are applied in 3 out of 3 tenants, the count is **3**; if only 2 tenants succeed, the count is **2**. Synced content represents the total custom detection rules synced across all target tenants.

## Limitations

Automation rules that trigger a playbook can't be distributed

## Troubleshooting and error handling

The following are some common reasons a sync might fail:

- User doesn't have permission to create custom detection rules on the target tenant.

- User doesn't have permission to read custom detection rules from **content source**.

- User doesn't have permission for the target device scope.

If the issue is with the target tenant, try creating an identical custom detection rule for further diagnosis. If the issue is with accessing the source data, try accessing the custom detection.

A known issue exists with distribution profile errors. In some scenarios, such as when a user without the required permissions selects **See the assignment** on a policy error, an indefinite loading state might be shown without a clear error message. Users might also encounter generic or unclear error messages if Microsoft Entra is temporarily unavailable. In such cases, close the error message and verify your permissions and Microsoft Entra availability.

## Related content

- [Create and manage custom detections rules](/defender-xdr/custom-detection-rules)

- [Add Microsoft Entra B2B collaboration users in the Microsoft Entra admin center](/entra/external-id/add-users-administrator)

- [Set up GDAP for your customers in Microsoft 365 Lighthouse](/microsoft-365/lighthouse/m365-lighthouse-setup-gdap)


# Mto Workbooks

# Workbooks in multitenant management

The Workbooks feature in Microsoft Sentinel enables users to manage and view workbooks across multiple tenants from a single page in the multitenant Organization portal. ​This feature allows users to access an out-of-the-box multitenant workbook, Situational Awareness, which provides insights into tenant health, trends, and metrics. ​This document walks you through the steps to access and use this feature effectively.

## Prerequisites

Before using Workbooks in multitenant management, ensure you have the following prerequisites:

* Access to Microsoft Sentinel on the Defender portal. ​

* Access to more than one tenant using B2B/GDAP.

* For the workbook aggregated view, at least one workbook must be available on one or more target tenants.

* For the Situational Awareness workbook, your home tenant (primary workspace) must have threat intelligence data. ​

## Access a workbook​

To navigate to the workbook page in the multitenant Organization portal in Microsoft Sentinel. ​

1. In the left-hand navigation pane, select **Microsoft Sentinel** > **Workbooks**. ​The Workbooks page displays an aggregated list of all workbooks across your tenants.

1. Use the search bar to find specific workbooks. Filter or browse through multiple pages of workbooks as needed.

1. Select the desired workbook from the list.

1. Select **View saved workbook** to open it in the Defender portal for the corresponding tenant.

## Open the situational awareness workbook

Use the workbook to get insights across your tenants, including health status, trends, and metrics. This workbook is multi tenant supported, so you can select which tenants to include.

1. From the multitenant management portal, select the button below the Situational Awareness card

1. To choose which tenants to include, use the tenant selector in the top-right corner. ​

Optionally, select **Edit selection** to select specific workspaces. ​

Ensure your home tenant is included in the scope and has threat intelligence data in the selected workspace, and select **Apply**.

## Explore the Workbook ​

* Use the global filters at the top of the workbook to refine the data displayed. ​

* Navigate through the subtabs to explore different categories of insights (for example, health status or threat insights).

* Review the charts and metrics provided to monitor trends and identify areas for investigation. ​

## Limitations

* The Situational Awareness workbook uses threat intelligence data exclusively from the home tenant, and this setting can't be changed.

* The Workbooks page doesn't currently support editing or creating workbooks. ​

* Workbook templates are currently not supported in the aggregated view.


# Mto Cross Cloud

# Manage tenants in other Microsoft cloud environments

[!INCLUDE[Prerelease information](../includes/prerelease.md)]

Multitenant management in Microsoft Defender supports government cloud environments to view their tenants in other cloud environments through cross-cloud visibility. Security operations teams operating in government cloud environments can now manage their entire security operations, including tenants in other cloud environments, in a single pane of glass.

Cross-cloud visibility allows GCC High and DoD multitenant customers to view and manage tenants in Microsoft GCC and Commercial cloud environments.

## Prerequisites

Cross-cloud visibility is available to government customers who have the applicable [licensing requirements](/defender-xdr/usgov#licensing-requirements).

In addition, ensure that the trust multi-factor authentication (MFA) from Microsoft Entra tenants is properly configured to successfully access tenants in Microsoft Commercial cloud environments. To configure MFA, see [Change inbound trust settings for MFA and device claims](/entra/external-id/cross-tenant-access-settings-b2b-collaboration#to-change-inbound-trust-settings-for-mfa-and-device-claims).

### B2B collaboration settings

Follow these steps to configure B2B collaboration settings.

#### Home tenant settings

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).

2. Navigate to **Identity > External identities > Cross-tenant access settings**, then select **Cross-tenant access settings**.

3. Select **Add organization**. Enter the tenant ID of the organization you want to add, then select **Add**.

> [!NOTE]

> By default, a B2B inherits the default settings of your tenant.

Configure your tenant settings to the following:

1. For the organization you added, select **Inbound access**.

2. Set B2B collaboration to **Block** for Access and Users.

3. On the Application tab, set access to **Block** and Applies to **All applications**, then select **Save**.

4. Select **B2B direct connect**, set access status to **Block** and Applies to **all users**.

5. On the Application tab, set access to **Block** and Applies to **All applications**, then select **Save**.

No other MFA Trust settings are required for the home tenant.

You then need to configure outbound access settings for the home tenant by following these steps:

1. In the **Cross-tenant access settings** pane, select **Outbound access**.

2. Configure B2B collaboration by setting access status to **Allow**.

3. In the Applies to, select any depending on your requirements.

4. Select **External applications** and set access status to **Allow**.

5. Set the Applies to to **All external applications**. Select **Save**.

6. Select **B2B direct connect** and set access status to **Block**.

7. In the Applies to, select **All users**.

8. Select **External applications** and set access status to **Block**.

9. Set the Applies to to **All external applications**. Select **Save**.

#### Target tenant settings

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).

2. Navigate to **Identity > External identities > Cross-tenant access settings**, then select **Cross-tenant access settings**.

3. Select **Add organization**. Enter the tenant ID of the organization you want to add, then select **Add**.

Configure the target tenant settings to the following:

1. For the organization you added, select **Inbound access**.

2. Set B2B collaboration to **Allow** for Access and Users.

3. On the Application tab, set access to **Allow** and Applies to **All applications**, then select **Save**.

4. Select **B2B direct connect**, set access status to **Block** and Applies to **All users**.

5. On the Application tab, set access to **Block** and Applies to **All applications**, then select **Save**.

6. Select **Trust settings**, then select **Trust multi-factor authentication from Microsoft Entra tenants**.

You then need to configure outbound access settings from the home tenant by following these steps:

1. In the **Cross-tenant access settings** pane, select **Outbound access**.

2. Configure B2B collaboration by setting access status to **Block**.

3. In the Applies to, select **All users**.

4. Select **External applications** and set access status to **Block**.

5. Set the Applies to to **All external applications**. Select **Save**.

6. Select **B2B direct connect** and set access status to **Block**.

7. In the Applies to, select **All users**.

8. Select **External applications** and set access status to **Block**.

9. Set the Applies to to **All external applications**. Select **Save**.

## Cross-cloud tenant management

To manage tenants from other Microsoft cloud environments:

1. Go to the [Settings page](https://mto.security.microsoft.com/settings) in Microsoft Defender multitenant management.

2. Select the dropdown beside **Add tenants**, then select **add from another cloud**.

3. In the next pane, type the tenant ID or domain where the tenant is to add a tenant, then select **Verify tenant**. The verification process looks at the added tenant’s information and permissions.

4. Once verified, select **Add tenant** to complete the process.

The tenants list now includes the tenants from the other cloud environment. You can now manage these tenants as you would any other tenant in Microsoft Defender.

If you get an error during the verification process, you can:

- Check the tenant ID or domain you entered.

- Ensure you have the correct permissions to access the tenant.

To remove tenants from the list, select the tenant, then select **Remove tenants**.

After successfully adding tenants from other clouds, you can view these tenants in other multitenant pages like the incidents and device inventory pages.

> [!NOTE]

> When a cross-cloud tenant is added to a distribution profile and subsequently removed from cross-cloud visibility, the tenant's name is removed from the tenant list and won’t be available for content management. This is a recognized limitation of cross-cloud visibility and is currently under review. See [Troubleshooting issues](mto-troubleshoot.md#content-assignment-failure-in-cross-cloud-tenant-management) for more information.

## Next steps

- [View and manage incidents and alerts in multitenant management](mto-incidents-alerts.md)

- [Device inventory in multitenant management](mto-tenant-devices.md#device-inventory)


# Mto Urbac

# Manage unified role-based access control in multitenant management

Use the Microsoft Defender multimanagement portal to manage unified role-based access control (URBAC) across multiple tenants. This capability provides a comprehensive view of permissions and access for your tenants and a centralized administration to manage these permissions.

## View custom roles

In the multitenant portal, navigate to the **Permissions & roles page** by selecting **System > Permissions**.

Create or edit a custom role, import and delete roles, and search for a specific role using the **Search** function from this page. You can also filter the roles according to assigned data sources, permissions category, assignee type, and tenant name.

## Create or edit a custom role (Preview)

You can create a custom role to provide flexibility and control over access to specific data. To create a custom role, follow these steps:

1. Sign in to multitenant management in Microsoft Defender, then navigate to **System > Permissions**.

2. Select **Create custom role**.

3. In the dropdown menu, select the tenant for which you want to create a new role. Select **Continue**.

4. In the **Basics** page, enter the name and description of the role. Select **Next**.

5. In the **Permissions** page, select the appropriate permissions for the role.

6. A new pane opens based on the permissions you selected. Select the appropriate permissions for the role, then select **Apply**. Here's an example.

7. Select **Next** to proceed to the next page.

8. In the **Assignments** page, select **Add assignment** or **Create assignment** to assign users and data sources.

9. In the **Add assignments** pane, add the assignment name and team members to be assigned, identify the data sources that they can access, and specify the identity scopes that users will have access to. Then select **Add**. Here's an example.

10. Select **Next**. Review the details you provided in the **Review and finish** page. You can edit the custom role’s name and description, permissions, and assignments in this page.

11. Select **Submit** to finish creating the custom role.

To edit an existing role, select the three dots beside the role name in the Permissions and roles list, then select **Edit**.

## Delete roles (Preview)

You can delete roles by selecting a role from the list and then selecting **Delete roles**. You can select multiple roles from various tenants to delete.

You can also delete a role by selecting the three dots beside the role name in the Permissions and roles list then selecting **Delete**.

The **Delete role** option is also available when editing a specific role.

## Import roles (Preview)

You can import existing roles from a tenant’s workloads to migrate permissions and assignments. Imported roles become available in the Permissions and roles list.

To import roles, follow these steps:

1. Navigate to **System > Permissions**.

2. Select **Import roles**.

3. In the **Import roles** pane, select the tenant from which you want to import roles in the dropdown menu. Select **Continue**.

4. In the **Workloads** page, select the workloads you want to import from. Select **Next**.

5. In the **Roles** page, select all or some of the roles that you want to import from the Eligible roles list. To review the permissions and assignments for a role, select the role name. Here's an example.

6. Review the details then select **Submit** to finish importing the roles.

To learn more about unified RBAC, see [Microsoft Defender unified role-based access control](/defender-xdr/manage-rbac).


# Mto Troubleshoot

# Troubleshoot multitenant management service issues

This article addresses potential issues that might arise as you use the multitenant management in Microsoft Defender. It provides guidance on how to troubleshoot these issues.

## Problem adding or removing tenants

When adding or removing tenants, you might encounter errors like the following:

The issue is resolved by refreshing the page and trying again.

## Some tenants are missing from the list

When loading the tenant list on the Settings page, you get the following error message:

The issue is due to [conditional access policy](/entra/identity/conditional-access/overview) requiring multifactor authentication (MFA) on your Azure Resource Manager app.

To resolve this issue, add *Microsoft 365 Security and Compliance Center app (80ccca67-54bd-44ab-8625-4b79c4dc7775)* to the same conditional access policy as your Azure Resource Manager app. This mitigation applies MFA on the origin tenant when a user tries to sign in to the Microsoft Defender portal.

Here’s an example of the policy setting in the Microsoft Entra admin center.

## Content assignment failure in cross-cloud tenant management

You see the following error when assigning content to distribution profiles:

When a cross-cloud tenant is added to a distribution profile and subsequently removed from cross-cloud visibility, the tenant's name is removed from the tenant list and won't be available for content management, which causes the error. This is a recognized limitation of cross-cloud tenant management and is currently under review.

## Related content

- [Set up Microsoft Defender multitenant management](mto-requirements.md)

- [Manage tenants](mto-tenants.md)


# Microsoft Threat Actor Naming

# How Microsoft names threat actors

Microsoft uses a weather-based naming taxonomy for threat actors. This taxonomy provides a more organized, articulate way to reference threat actors so that organizations can better prioritize and protect themselves, and so that security researchers already confronted with an overwhelming amount of threat intelligence data can more easily identify and track threats.

Microsoft categorizes threat actors into five key groups:

**Nation-state actors:** cyber operators acting on behalf of or directed by a nation/state-aligned program, irrespective of whether for espionage, financial gain, or retribution. Microsoft observed that most nation state actors continue to focus operations and attacks on government agencies, intergovernmental organizations, nongovernmental organizations, and think tanks for traditional espionage or surveillance objectives.

**Financially motivated actors:** cyber campaigns/groups directed by a criminal organization/person with motivations of financial gain and aren't associated with high confidence to a known non-nation state or commercial entity. This category includes ransomware operators, business email compromise, phishing, and other groups with purely financial or extortion motivations.

**Private sector offensive actors (PSOAs):** cyber activity led by commercial actors that are known/legitimate legal entities, that create and sell cyberweapons to customers who then select targets and operate the cyberweapons. These tools were observed targeting and surveiling dissidents, human rights defenders, journalists, civil society advocates, and other private citizens, threatening many global human rights efforts.

**Influence operations:** information campaigns communicated online or offline in a manipulative fashion to shift perceptions, behaviors, or decisions by target audiences to further a group or a nation's interests and objectives.

**Groups in development:** a temporary designation given to an unknown, emerging, or developing threat activity. This designation allows Microsoft to track a group as a discrete set of information until high confidence is reached about the origin or identity of the actor behind the operation. Once criteria are met, a group in development is converted to a named actor or merged into existing names.

In this taxonomy, a weather event or *family name* represents one of the above categories. For nation-state actors, a family name is assigned to a country/region of origin tied to attribution. For example, Typhoon indicates origin or attribution to China. For other actors, the family name represents a motivation. For example, Tempest indicates financially motivated actors.

Threat actors within the same weather family are given an adjective to distinguish actor groups with distinct tactics, techniques, and procedures (TTPs), infrastructure, objectives, or other identified patterns. For groups in development, a temporary designation of Storm and a four-digit number is used where there's a newly discovered, unknown, emerging, or developing cluster of threat activity.

The following table shows how the family names map to the threat actors that we track.

|Threat actor category|Origin/Type|Family name|

|:---|:---|:---|

|Nation-state|Australia<br>Canada<br>China<br>Germany<br>India<br>Iran<br>Israel<br>New Zealand<br>North Korea<br>Lebanon<br>Pakistan<br>Palestinian Authority<br>Russia<br>Singapore<br>South Korea<br>Spain<br>Syria<br>Türkiye<br>Ukraine<br>United Arab Emirates<br>United Kingdom<br>United States<br>Vietnam|Waterspout<br>Freeze<br>Typhoon<br>Gale<br>Monsoon<br>Sandstorm<br>Heatwave<br>Swell<br>Sleet<br>Rain<br>Vortex<br>Lightning<br>Blizzard<br>Squall<br>Hail<br>Derecho<br>Haze<br>Dust<br>Frost<br>Gust<br>Fog<br>Tornado<br>Cyclone|

|Financially motivated|Financially motivated|Tempest|

|Private sector offensive actors|PSOAs|Tsunami|

|Influence operations|Influence operations|Flood|

|Groups in development|Groups in development|Storm|

The following table lists publicly disclosed threat actor names with their origin or threat actor category, previous names, and corresponding names used by other security vendors where available. This page is updated as more info on other vendors' names become available.

|Threat actor name|Origin/Threat actor category|Other names|

|:-----|:-----|:---|

|Amethyst Rain|Lebanon|VolcanicTimber, Volatile Cedar|

|[Antique Typhoon](https://www.microsoft.com/en-us/security/blog/2023/07/14/analysis-of-storm-0558-techniques-for-unauthorized-email-access/)|China|Storm-0558|

|[Aqua Blizzard](https://www.microsoft.com/en-us/security/blog/2022/02/04/actinium-targets-ukrainian-organizations/)|Russia|ACTINIUM, PRIMITIVE BEAR, Gamaredon, Armageddon, UNC530, shuckworm, SectorC08|

|Berry Sandstorm|Iran|Storm-0852|

|Blue Tsunami|Israel, Private sector offensive actor||

|Brass Typhoon|China|BARIUM, WICKED PANDA, APT41|

|Brocade Typhoon|China|BORON, GOTHIC PANDA, UPS, APT3, OLDCARP, TG-0110, Red Sylvan, CYBRAN|

|Burgundy Sandstorm|Iran|REMIX KITTEN, Cadelle, Chafer|

|[Cadet Blizzard](https://www.microsoft.com/en-us/security/blog/2023/06/14/cadet-blizzard-emerges-as-a-novel-and-distinct-russian-threat-actor/)|Russia|DEV-0586, EMBER BEAR|

|Canary Typhoon|China|CIRCUIT PANDA, APT24, Palmerworm, BlackTech|

|Canvas Cyclone|Vietnam|BISMUTH, OCEAN BUFFALO, OceanLotus, APT32|

|Caramel Tsunami|Israel, Private sector offensive actor|DEV-0236|

|[Carmine Tsunami](https://www.microsoft.com/en-us/security/blog/2023/04/11/dev-0196-quadreams-kingspawn-malware-used-to-target-civil-society-in-europe-north-america-the-middle-east-and-southeast-asia/)|Private sector offensive actor||

|Charcoal Typhoon|China|CHROMIUM, AQUATIC PANDA, ControlX, RedHotel, BRONZE UNIVERSITY|

|Checkered Typhoon|China|CHLORINE, DEEP PANDA, ATG50, APT19, TG-3551, Red Gargoyle|

|Cinnamon Tempest|China, Financially motivated|DEV-0401, HighGround|

|Circle Typhoon|China|DEV-0322, EMISSARY PANDA, APT6, APT27|

|[Citrine Sleet](https://www.microsoft.com/en-us/security/blog/2024/08/30/north-korean-threat-actor-citrine-sleet-exploiting-chromium-zero-day/)|North Korea|Storm-0139, Storm-1222, LABYRINTH CHOLLIMA|

|Clay Typhoon|China|Storm-2416|

|Copper Typhoon|China|Tonto Team, Earth Akhlut, Sharp-R|

|[Coral Sleet](https://aka.ms/threat-actors-operationalize-ai)|North Korea|Storm-1877|

|Cotton Sandstorm|Iran|NEPTUNIUM, HAYWIRE KITTEN, Vice Leaker|

|[CovertNetwork-1658](https://www.microsoft.com/en-us/security/blog/2024/10/31/chinese-threat-actor-storm-0940-uses-credentials-from-password-spray-attacks-from-a-covert-network/)|Covert network|ORB07|

|Crescent Typhoon|China|CESIUM|

|Crimson Sandstorm|Iran|CURIUM, IMPERIAL KITTEN, Tortoise Shell, HOUSEBLEND, TA456|

|Cuboid Sandstorm|Iran|DEV-0228, IMPERIAL KITTEN|

|Daffodil Gust|United Arab Emirates|Stealth Falcon, Fruity Armor, Project Raven|

|[Denim Tsunami](https://www.microsoft.com/en-us/security/blog/2022/07/27/untangling-knotweed-european-private-sector-offensive-actor-using-0-day-exploits/)|Austria, Private sector offensive actor|DEV-0291|

|[Diamond Sleet](https://www.microsoft.com/en-us/security/blog/2023/11/22/diamond-sleet-supply-chain-compromise-distributes-a-modified-cyberlink-installer/)|North Korea|ZINC, LABYRINTH CHOLLIMA, Black Artemis, Lazarus|

|Emerald Sleet|North Korea|THALLIUM, VELVET CHOLLIMA, RGB-D5, Black Banshee, Kimsuky, Greendinosa|

|Fallow Squall|Singapore|PLATINUM, PARASITE, RUBYVINE, GINGERSNAP|

|[Flax Typhoon](https://www.microsoft.com/en-us/security/blog/2023/08/24/flax-typhoon-using-legitimate-software-to-quietly-access-taiwanese-organizations/)|China|Storm-0919, ETHEREAL PANDA|

|[Forest Blizzard](https://www.microsoft.com/en-us/security/blog/tag/forest-blizzard-strontium/)|Russia|STRONTIUM, FANCY BEAR, Sednit, ATG2, Sofacy, Blue Athena, Z-Lom Team, Operation Pawn Storm, Tsar Team, CrisisFour, HELLFIRE, APT28|

|[Fox Tempest](https://aka.ms/Fox-Tempest-MSaaS)|Financially motivated||

|Ghost Blizzard|Russia|BROMINE, BERSERK BEAR, TG-4192, Koala Team, Blue Kraken, Crouching Yeti, Dragonfly|

|Gingham Typhoon|China|GADOLINIUM, KRYPTONITE PANDA, TEMP.Periscope, Leviathan, JJDoor, APT40, Feverdream|

|Granite Typhoon|China|GALLIUM, PHANTOM PANDA|

|Gray Sandstorm|Iran|DEV-0343|

|Hazel Sandstorm|Iran|EUROPIUM, HELIX KITTEN, COBALT GYPSY, Crambus, OilRig, APT34|

|Heart Typhoon|China|HELIUM, AURORA PANDA, APT17, Hidden Lynx, ATG3, Red Typhoon, KAOS, TG-8153, SportsFans, DeputyDog, Tailgater|

|Hexagon Typhoon|China|HYDROGEN, NUMBERED PANDA, Calc Team, Red Anubis, APT12, DNS-Calc, HORDE|

|Houndstooth Typhoon|China|HASSIUM, DRAGNET PANDA, isoon, deepclif|

|Jade Sleet|North Korea|Storm-0954, LABYRINTH CHOLLIMA|

|[Jasper Sleet](https://www.microsoft.com/en-us/security/blog/2025/06/30/jasper-sleet-north-korean-remote-it-workers-evolving-tactics-to-infiltrate-organizations/)|North Korea|Storm-0287|

|Lace Tempest|Financially motivated|DEV-0950|

|Lemon Sandstorm|Iran|RUBIDIUM, PIONEER KITTEN|

|Leopard Typhoon|China|LEAD, WICKED PANDA, TG-2633, TG-3279, Mana, KAOS, Red Diablo, Winnti Group|

|Lilac Typhoon|China|DEV-0234|

|[Linen Typhoon](https://www.microsoft.com/en-us/security/blog/2025/07/22/disrupting-active-exploitation-of-on-premises-sharepoint-vulnerabilities/)|China|IODINE, EMISSARY PANDA, Red Phoenix, Hippo, Lucky Mouse, BOWSER, APT27, Wekby2, UNC215, TG-3390|

|Luna Tempest|Financially motivated||

|Magenta Dust|Türkiye|PROMETHIUM, StrongPity, SmallPity|

|Manatee Tempest|Russia|DEV-0243, INDRIK SPIDER|

|[Mango Sandstorm](https://www.microsoft.com/en-us/security/blog/2023/04/07/mercury-and-dev-1084-destructive-attack-on-hybrid-environment/)|Iran|MERCURY, STATIC KITTEN, SeedWorm, TEMP.Zagros, MuddyWater|

|[Marbled Dust](https://www.microsoft.com/en-us/security/blog/2025/05/12/marbled-dust-leverages-zero-day-in-output-messenger-for-regional-espionage/)|Türkiye|SILICON, COSMIC WOLF, Sea Turtle, UNC1326|

|Marigold Sandstorm|Iran|DEV-500, VENGEFUL KITTEN|

|[Midnight Blizzard](https://www.microsoft.com/en-us/security/blog/tag/midnight-blizzard-nobelium/)|Russia|NOBELIUM, COZY BEAR, UNC2452, APT29|

|[Mint Sandstorm](https://www.microsoft.com/en-us/security/blog/tag/mint-sandstorm-phosphorus/)|Iran|PHOSPHORUS, CHARMING KITTEN, Parastoo, Newscaster, APT35|

|[Moonstone Sleet](https://www.microsoft.com/en-us/security/blog/2024/05/28/moonstone-sleet-emerges-as-new-north-korean-threat-actor-with-new-bag-of-tricks/)|North Korea|Storm-1789, LABYRINTH CHOLLIMA|

|Mulberry Typhoon|China|MANGANESE, KEYHOLE PANDA, Backdoor-DPD, COVENANT, CYSERVICE, Bottle, Red Horus, Red Naga, Auriga, APT5, ATG48, TG-2754, tabcteng|

|Mustard Tempest|Financially motivated|DEV-0206, INDRIK SPIDER|

|[Neva Flood](https://blogs.microsoft.com/on-the-issues/2024/09/17/russian-election-interference-efforts-focus-on-the-harris-walz-campaign/)|Russia, Influence operations|Storm-1516, CopyCop|

|Night Tsunami|Israel|DEV-0336|

|Nylon Typhoon|China|NICKEL, VIXEN PANDA, Playful Dragon, RedRiver, ke3chang, APT15, Mirage|

|[Octo Tempest](https://www.microsoft.com/en-us/security/blog/2023/10/25/octo-tempest-crosses-boundaries-to-facilitate-extortion-encryption-and-destruction/)|Financially motivated|SCATTERED SPIDER, 0ktapus|

|[Oka Flood](https://blogs.microsoft.com/on-the-issues/2024/09/17/russian-election-interference-efforts-focus-on-the-harris-walz-campaign/)|Russia, Influence operations|Storm-1679|

|Onyx Sleet|North Korea|PLUTONIUM, SILENT CHOLLIMA, StoneFly, Tdrop2 campaign, DarkSeoul, Black Chollima, Andariel, APT45|

|Opal Sleet|North Korea|OSMIUM, VELVET CHOLLIMA, Planedown, Konni, APT43|

|Patched Lightning||Storm-0113|

|[Peach Sandstorm](https://www.microsoft.com/en-us/security/blog/2024/08/28/peach-sandstorm-deploys-new-custom-tickler-malware-in-long-running-intelligence-gathering-operations/)|Iran|HOLMIUM, REFINED KITTEN, APT33, Elfin|

|Pearl Sleet|North Korea|LAWRENCIUM|

|Pepper Typhoon|China|LIMINAL PANDA, CL-STA-0969|

|Periwinkle Tempest|Russia|DEV-0193, WIZARD SPIDER|

|Phlox Tempest|Israel, Financially motivated|DEV-0796|

|Pink Sandstorm|Iran|AMERICIUM, SPECTRAL KITTEN, Agrius, Deadwood, BlackShadow, SharpBoys, FireAnt, Justice Blade|

|Pinstripe Lightning||NIOBIUM, RENEGADE JACKAL, Desert Falcons, Scimitar, Arid Viper|

|Pistachio Tempest|Financially motivated|DEV-0237|

|[Plaid Rain](https://www.microsoft.com/en-us/security/blog/2022/06/02/exposing-polonium-activity-and-infrastructure-targeting-israeli-organizations/)|Lebanon|POLONIUM, INCENDIARY JACKAL|

|Pumpkin Sandstorm|Iran|DEV-0146|

|Purple Typhoon|China|POTASSIUM, STONE PANDA, GOLEM, Evilgrab, AEON, LIVESAFE, ChChes, APT10, Haymaker, Webmonder, Foxtrot, Foxmail, MenuPass, Red Apollo|

|Raspberry Typhoon|China|RADIUM, LOTUS PANDA, LotusBlossom, APT30|

|Red Sandstorm|Iran|Storm-0842, BANISHED KITTEN, Void Manticore|

|Ruby Sleet|North Korea|CERIUM, VELVET CHOLLIMA|

|Ruza Flood|Russia, Influence operations||

|Salmon Typhoon|China|SODIUM, MAVERICK PANDA, APT4|

|Salt Typhoon|China|OPERATOR PANDA, GhostEmperor, FamousSparrow|

|Sangria Tempest|Ukraine, Financially motivated|ELBRUS, CARBON SPIDER|

|[Sapphire Sleet](https://www.microsoft.com/en-us/security/blog/tag/sapphire-sleet/)|North Korea|COPERNICIUM, UNC1069, STARDUST CHOLLIMA, Alluring Pisces, BlueNoroff, CageyChameleon, CryptoCore|

|Satin Typhoon|China|SCANDIUM, DYNAMITE PANDA, COMBINE, TG-0416, SILVERVIPER, Red Wraith, APT18, Elderwood Group, Wekby|

|[Seashell Blizzard](https://www.microsoft.com/en-us/security/blog/2025/02/12/the-badpilot-campaign-seashell-blizzard-subgroup-conducts-multiyear-global-access-operation/)|Russia|IRIDIUM, VOODOO BEAR, BE2, UAC-0113, Blue Echidna, Sandworm, PHANTOM, BlackEnergy Lite, APT44|

|[Secret Blizzard](https://www.microsoft.com/en-us/security/blog/tag/secret-blizzard/)|Russia|KRYPTON, VENOMOUS BEAR, Uroburos, Snake, Blue Python, Turla, WRAITH, ATG26|

|Sefid Flood|Iran, Influence operations||

|Shadow Typhoon|China|Storm-0062, DarkShadow, Oro0lxy|

|Silk Typhoon|China|HAFNIUM, MURKY PANDA, timmy|

|Smoke Sandstorm|Iran|IMPERIAL KITTEN, UNC1549|

|Spandex Tempest|Financially motivated|MONTY SPIDER, TA505|

|[Star Blizzard](https://www.microsoft.com/en-us/security/blog/tag/star-blizzard-seaborgium/)|Russia|SEABORGIUM, COLDRIVER, Callisto Group, BlueCharlie, TA446|

|Storm-0133|Iran|HEXANE, Lyceum, Siamesekitten, Spirlin|

|Storm-0156|Pakistan|MYTHIC LEOPARD, SideCopy, APT36, Transparent Tribe|

|Storm-0216|Financially motivated|TUNNEL SPIDER, UNC2198|

|Storm-0230|Group in development|WIZARD SPIDER, Conti Team 1|

|Storm-0247|China|ToddyCat, Websiic|

|[Storm-0249](https://www.microsoft.com/en-us/security/blog/2025/08/21/think-before-you-clickfix-analyzing-the-clickfix-social-engineering-technique/)|Group in development||

|Storm-0252|Group in development|CHATTY SPIDER|

|[Storm-0259](https://www.microsoft.com/en-us/security/blog/2026/01/14/inside-redvds-how-a-single-virtual-desktop-provider-fueled-worldwide-cybercriminal-operations/)|Group in development||

|Storm-0288|Group in development|FIN8|

|Storm-0302|Group in development|NARWHAL SPIDER, TA544|

|[Storm-0408](https://www.microsoft.com/en-us/security/blog/2025/03/06/malvertising-campaign-leads-to-info-stealers-hosted-on-github/)|Group in development||

|[Storm-0485](https://www.microsoft.com/en-us/security/blog/2025/05/29/defending-against-evolving-identity-attack-techniques/)|Group in development||

|[Storm-0501](https://www.microsoft.com/en-us/security/blog/2025/08/27/storm-0501s-evolving-techniques-lead-to-cloud-based-ransomware/)|Financially motivated||

|Storm-0538|Group in development|SKELETON SPIDER, FIN6|

|[Storm-0539](https://www.microsoft.com/en-us/security/blog/2024/05/23/cyber-signals-inside-the-growing-risk-of-gift-card-fraud/)|Financially motivated||

|[Storm-0569](https://www.microsoft.com/en-us/security/blog/2022/11/17/dev-0569-finds-new-ways-to-deliver-royal-ransomware-various-payloads/)|Financially motivated||

|Storm-0593|Russia|InvisiMole|

|Storm-0671|Group in development|UNC2596, Tropicalscorpius|

|[Storm-0940](https://www.microsoft.com/en-us/security/blog/2024/10/31/chinese-threat-actor-storm-0940-uses-credentials-from-password-spray-attacks-from-a-covert-network/)|China||

|[Storm-0978](https://www.microsoft.com/en-us/security/blog/2023/07/11/storm-0978-attacks-reveal-financial-and-espionage-motives/)|Russia|RomCom, Underground Team|

|[Storm-1101](https://www.microsoft.com/en-us/security/blog/2023/03/13/dev-1101-enables-high-volume-aitm-campaigns-with-open-source-phishing-kit/)|Group in development||

|[Storm-1113](https://www.microsoft.com/en-us/security/blog/2023/12/28/financially-motivated-threat-actors-misusing-app-installer/)|Financially motivated|APOTHECARY SPIDER|

|Storm-1125|Belarus|MoustachedBouncer|

|[Storm-1152](https://blogs.microsoft.com/on-the-issues/2023/12/13/cybercrime-cybersecurity-storm-1152-fraudulent-accounts/)|Financially motivated||

|[Storm-1175](https://www.microsoft.com/en-us/security/blog/2026/04/06/storm-1175-focuses-gaze-on-vulnerable-web-facing-assets-in-high-tempo-medusa-ransomware-operations/)|China, Financially motivated||

|Storm-1194|Group in development|MONTI|

|[Storm-1249](https://www.microsoft.com/en-us/security/blog/2025/05/29/defending-against-evolving-identity-attack-techniques/)|Group in development||

|Storm-1516|Russia, Influence operations||

|[Storm-1567](https://www.microsoft.com/en-us/security/blog/2023/10/11/automatic-disruption-of-human-operated-attacks-through-containment-of-compromised-user-accounts/)|Financially motivated|PUNK SPIDER|

|[Storm-1575](https://www.microsoft.com/en-us/security/blog/2026/01/14/inside-redvds-how-a-single-virtual-desktop-provider-fueled-worldwide-cybercriminal-operations/)|Group in development||

|[Storm-1607](https://www.microsoft.com/en-us/security/blog/2025/08/21/think-before-you-clickfix-analyzing-the-clickfix-social-engineering-technique/)|Group in development||

|[Storm-1674](https://www.microsoft.com/en-us/security/blog/2023/12/28/financially-motivated-threat-actors-misusing-app-installer/)|Financially motivated||

|[Storm-1747](https://www.microsoft.com/en-us/security/blog/2026/03/04/inside-tycoon2fa-how-a-leading-aitm-phishing-kit-operated-at-scale/)|Group in development||

|[Storm-1811](https://www.microsoft.com/en-us/security/blog/2024/05/15/threat-actors-misusing-quick-assist-in-social-engineering-attacks-leading-to-ransomware/)|Financially motivated|CURLY SPIDER|

|Storm-1849|China|UAT4356|

|[Storm-1865](https://www.microsoft.com/en-us/security/blog/2025/03/13/phishing-campaign-impersonates-booking-com-delivers-a-suite-of-credential-stealing-malware/)|Group in development||

|Storm-1982|China|SneakyCheff, UNK_SweetSpecter|

|[Storm-2035](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/final/en-us/microsoft-brand/documents/5bc57431-a7a9-49ad-944d-b93b7d35d0fc.pdf)|Iran, Influence operations||

|[Storm-2077](https://www.microsoft.com/en-us/security/blog/2024/11/22/microsoft-shares-latest-intelligence-on-north-korean-and-chinese-threat-actors-at-cyberwarcon/#storm-2077)|China|TAG-100|

|[Storm-2227](https://www.microsoft.com/en-us/security/blog/2026/01/14/inside-redvds-how-a-single-virtual-desktop-provider-fueled-worldwide-cybercriminal-operations/)|Group in development||

|[Storm-2246](https://blogs.microsoft.com/on-the-issues/2025/09/16/microsoft-seizes-338-websites-to-disrupt-rapidly-growing-raccoono365-phishing-service/)|Group in development||

|[Storm-2372](https://www.microsoft.com/en-us/security/blog/2025/02/13/storm-2372-conducts-device-code-phishing-campaign/)|Group in development||

|[Storm-2460](https://www.microsoft.com/en-us/security/blog/2025/08/18/dissecting-pipemagic-inside-the-architecture-of-a-modular-backdoor-framework/)|Group in development||

|[Storm-2470](https://www.microsoft.com/en-us/security/blog/2026/01/14/inside-redvds-how-a-single-virtual-desktop-provider-fueled-worldwide-cybercriminal-operations/)|Group in development||

|[Storm-2477](https://www.microsoft.com/en-us/security/blog/2025/05/21/lumma-stealer-breaking-down-the-delivery-techniques-and-capabilities-of-a-prolific-infostealer/)|Group in development|Lumma Stealer|

|[Storm-2561](https://www.microsoft.com/en-us/security/blog/2026/03/12/storm-2561-uses-seo-poisoning-to-distribute-fake-vpn-clients-for-credential-theft/)|Group in development||

|[Storm-2603](https://www.microsoft.com/en-us/security/blog/2025/07/22/disrupting-active-exploitation-of-on-premises-sharepoint-vulnerabilities/)|China||

|[Storm-2657](https://www.microsoft.com/en-us/security/blog/2025/05/21/lumma-stealer-breaking-down-the-delivery-techniques-and-capabilities-of-a-prolific-infostealer/)|United States, Financially motivated|Payroll Pirates|

|[Storm-2755](https://www.microsoft.com/en-us/security/blog/2026/04/09/investigating-storm-2755-payroll-pirate-attacks-targeting-canadian-employees/)|Financially motivated||

|[Storm-2949](https://www.microsoft.com/en-us/security/blog/2026/05/18/storm-2949-turned-compromised-identity-into-cloud-wide-breach/)|Group in development||

|Storm-2981|Group in development|Coinbase Cartel|

|Storm-2999|Group in development|TeamPCP|

|Strawberry Tempest|Financially motivated|DEV-0537, SLIPPY SPIDER, LAPSUS$|

|Sunglow Blizzard||DEV-0665|

|Swirl Typhoon|China|TELLURIUM, STALKER PANDA, Tick, Bronze Butler, REDBALDKNIGHT|

|Taffeta Typhoon|China|TECHNETIUM, TURBINE PANDA, TG-0055, Red Kobold, JerseyMikes, APT26, BEARCLAW|

|Taizi Flood|China, Influence operations|Dragonbridge, Spamouflage|

|Tumbleweed Typhoon|China|THORIUM, Karst|

|Twill Typhoon|China|TANTALUM, MUSTANG PANDA, BRONZE PRESIDENT, LuminousMoth|

|[Vanilla Tempest](https://www.microsoft.com/en-us/security/blog/2022/10/25/dev-0832-vice-society-opportunistic-ransomware-campaigns-impacting-us-education-sector/)|Financially motivated|DEV-0832, VICE SPIDER, Vice Society|

|Velvet Tempest|Financially motivated|DEV-0504, ALPHA SPIDER|

|[Violet Typhoon](https://www.microsoft.com/en-us/security/blog/2025/07/22/disrupting-active-exploitation-of-on-premises-sharepoint-vulnerabilities/)|China|ZIRCONIUM, JUDGMENT PANDA, Chameleon, APT31, WebFans|

|[Void Blizzard](https://www.microsoft.com/en-us/security/blog/2025/05/27/new-russia-affiliated-actor-void-blizzard-targets-critical-sectors-for-espionage/)|Russia|Laundry Bear|

|Volga Flood|Russia, Influence operations|Storm-1841, Rybar|

|[Volt Typhoon](https://www.microsoft.com/security/blog/2023/05/24/volt-typhoon-targets-us-critical-infrastructure-with-living-off-the-land-techniques)|China|VANGUARD PANDA, BRONZE SILHOUETTE|

|Wheat Tempest|Financially motivated|GOLD, Gatak|

|Wisteria Tsunami|India, Private sector offensive actor|DEV-0605, MintedSoil|

|Yulong Flood|China, Influence operations|Storm-1852|

|Zigzag Hail|Korea|DUBNIUM, SHADOW CRANE, Nemim, TEMPLAR, TieOnJoe, Fallout Team, Purple Pygmy, Dark Hotel, Egobot, Tapaoux, PALADIN, APT-C-60|

Read the [threat actor naming taxonomy announcement](https://aka.ms/threatactorsblog) for more information.

## Putting intelligence into the hands of security professionals

[Intel profiles in Microsoft Defender Threat Intelligence](/defender-xdr/defender-threat-intelligence) bring crucial insights about threat actors. These insights enable security teams to get the context they need as they prepare for and respond to threats.

Additionally, the Microsoft Defender Threat Intelligence Intel Profiles API provides the most up-to-date threat actor infrastructure visibility in the industry today. Updated information is crucial in enabling threat intelligence and security operations (SecOps) teams to streamline their advanced threat hunting and analysis workflows. Learn more about this API in the documentation: [Use the threat intelligence APIs in Microsoft Graph (preview)](/graph/api/resources/security-threatintelligence-overview).

## Resources

Use the following query on Microsoft Defender XDR and other Microsoft security products supporting the Kusto query language (KQL) to get information about a threat actor using the old name, new name, or industry name:

```kusto

let TANames = externaldata(PreviousName: string, NewName: string, Origin: string, OtherNames: dynamic)[@"https://raw.githubusercontent.com/microsoft/mstic/master/PublicFeeds/ThreatActorNaming/MicrosoftMapping.json"] with(format="multijson", ingestionMapping='[{"Column":"PreviousName","Properties":{"Path":"$.Previous name"}},{"Column":"NewName","Properties":{"Path":"$.New name"}},{"Column":"Origin","Properties":{"Path":"$.Origin/Threat"}},{"Column":"OtherNames","Properties":{"Path":"$.Other names"}}]');

let GetThreatActorAlias = (Name: string) {

TANames

| where Name =~ NewName or Name =~ PreviousName or OtherNames has Name

};

GetThreatActorAlias("ZINC")

```

The following files containing the comprehensive mapping of old threat actor names with their new names are also available:

- [JSON format](https://github.com/microsoft/mstic/blob/master/PublicFeeds/ThreatActorNaming/MicrosoftMapping.json)

- [Downloadable Excel](https://download.microsoft.com/download/4/5/2/45208247-c1e9-432d-a9a2-1554d81074d9/Microsoft-threat-actor-list.xlsx)


# Malware Naming

# Malware names

We name the malware and unwanted software that we detect according to the Computer Antivirus Research Organization (CARO) malware naming scheme. The scheme uses the following format:

![How Microsoft determines names malware](media/malware-naming/naming-malware.png)

When our analysts research a particular threat, they determine what each of the components name is.

## Type

Type describes what the malware does on your computer. The following are the different types of malware that Microsoft products detect.

### Malware

Following are the types of malware that Microsoft detects. To know more about how Microsoft defines malware, see [How Microsoft identifies malware and potentially unwanted applications - Malware](criteria.md#malware).

```

* Backdoor

* Constructor

* DDoS

* Exploit

* HackTool

* Joke

* Password Stealer (PWS)

* Ransom

* Rogue

* Spammer

* Spoofer

* Trojan

* TrojanClicker

* TrojanDownloader

* TrojanNotifier

* TrojanProxy

* TrojanSpy

* VirTool

* Virus

* Worm

```

### Unwanted software

Following are the types of unwanted software that Microsoft products detect. For more information on what unwanted software is and what is classified as unwanted software, see [Unwanted software](criteria.md#unwanted-software).

```

* Adware

* BrowserModifier

* Misleading

* MonitoringTool

* Program

* SoftwareBundler

* UwS

```

### Potentially unwanted applications

Following are the types of potentially unwanted applications (PUAs) that Microsoft products detect. To know what PUAs are, see [Potentially unwanted application (PUA)](criteria.md#potentially-unwanted-application-pua).

```

* PUA

* App

* PUAAdvertising

* PUATorrent

* PUAMiner

* PUAMarketing

* PUABundler

* PUADlManager

```

### Tampering software

Tampering software, detected as ***Tampering** are tools that can lower device security. To know more, see [Tampering software](criteria.md#tampering-software).

### Vulnerable software

Following are the types of vulnerable software that Microsoft products detect. Know more about this detection in [Vulnerable software](criteria.md#vulnerable-software).

```

* Vulnerable

* VulnerableDriver

```

### Other malware types

Microsoft also detects ***Behavior** and ***Tool** types of malware.

## Platforms

Platforms guide the malware to its compatible operating system (such as Windows, macOS, and Android). The platform's guidance is also used for programming languages and file formats.

### Operating systems

```

* AndroidOS: Android operating system

* DOS: MS-DOS platform

* EPOC: Psion devices

* FreeBSD: FreeBSD platform

* iOS: iPhone operating system

* Linux: Linux platform

* macOS: MAC 9.x platform or earlier

* macOS_X: macOS X or later

* OS2: OS2 platform

* Palm: Palm operating system

* Solaris: System V-based Unix platforms

* SunOS: Unix platforms 4.1.3 or lower

* SymbOS: Symbian operating system

* Unix: general Unix platforms

* Win16: Win16 (3.1) platform

* Win2K: Windows 2000 platform

* Win32: Windows 32-bit platform

* Win64: Windows 64-bit platform

* Win95: Windows 95, 98 and ME platforms

* Win98: Windows 98 platform only

* WinCE: Windows CE platform

* WinNT: WinNT

```

### Scripting languages

```

* ABAP: Advanced Business Application Programming scripts

* ALisp: ALisp scripts

* AmiPro: AmiPro script

* ANSI: American National Standards Institute scripts

* AppleScript: compiled Apple scripts

* ASP: Active Server Pages scripts

* AutoIt: AutoIT scripts

* BAS: Basic scripts

* BAT: Basic scripts

* CorelScript: Corelscript scripts

* HTA: HTML Application scripts

* HTML: HTML Application scripts

* INF: Install scripts

* IRC: mIRC/pIRC scripts

* Java: Java binaries (classes)

* JS: JavaScript scripts

* LOGO: LOGO scripts

* MPB: MapBasic scripts

* MSH: Monad shell scripts

* MSIL: .NET intermediate language scripts

* Perl: Perl scripts

* PHP: Hypertext Preprocessor scripts

* Python: Python scripts

* SAP: SAP platform scripts

* SH: Shell scripts

* VBA: Visual Basic for Applications scripts

* VBS: Visual Basic scripts

* WinBAT: Winbatch scripts

* WinHlp: Windows Help scripts

* WinREG: Windows registry scripts

```

### Macros

```

* A97M: Access 97, 2000, XP, 2003, 2007, and 2010 macros

* HE: macro scripting

* O97M: Office 97, 2000, XP, 2003, 2007, and 2010 macros - those that affect Word, Excel, and PowerPoint

* PP97M: PowerPoint 97, 2000, XP, 2003, 2007, and 2010 macros

* V5M: Visio5 macros

* W1M: Word1Macro

* W2M: Word2Macro

* W97M: Word 97, 2000, XP, 2003, 2007, and 2010 macros

* WM: Word 95 macros

* X97M: Excel 97, 2000, XP, 2003, 2007, and 2010 macros

* XF: Excel formulas

* XM: Excel 95 macros

```

### Other file types

```

* ASX: XML metafile of Windows Media .asf files

* HC: HyperCard Apple scripts

* MIME: MIME packets

* Netware: Novell Netware files

* QT: Quicktime files

* SB: StarBasic (StarOffice XML) files

* SWF: Shockwave Flash files

* TSQL: MS SQL server files

* XML: XML files

```

## Family

Grouping of malware based on common characteristics, including attribution to the same authors. Security software providers sometimes use different names for the same malware family.

## Variant letter

Used sequentially for every distinct version of a malware family. For example, the detection for the variant **".AF"** is created after the detection for the variant **".AE"**.

## Suffixes

A suffix that begins with **!** is an indicator used by Microsoft internally.


# Criteria

# How Microsoft identifies malware and potentially unwanted applications

Microsoft aims to provide a delightful and productive Windows experience by working to ensure you're safe and in control of your devices. Microsoft helps protect you from potential threats by identifying and analyzing software and online content. When you download, install, and run software, Microsoft checks the reputation of downloaded programs and ensures you're protected against known threats. You're also warned about software that's unknown to Microsoft.

You can assist Microsoft by [submitting unknown or suspicious software for analysis](https://www.microsoft.com/wdsi/filesubmission/). Submissions help ensure that unknown or suspicious software is scanned by the system to start establishing reputation. [Learn more about submitting files for analysis](submission-guide.md).

The next sections provide an overview of the classifications Microsoft uses for applications and the types of behaviors that lead to that classification.

> [!NOTE]

> New forms of malware and potentially unwanted applications are being developed and distributed rapidly. The following list might not be comprehensive, and Microsoft reserves the right to adjust, expand, and update these classifications without prior notice or announcement.

## Unknown – Unrecognized software

No antivirus or protection technology is perfect. It takes time to identify and block malicious sites and applications, or trust newly released programs and certificates. With almost 2 billion websites on the internet and software continuously updated and released, it's impossible to have information about every single site and program.

Think of unknown or uncommonly downloaded warnings as an early warning system for potentially undetected malware. There's generally a delay from the time new malware is released until it's identified. Not all uncommon programs are malicious, but the risk in the unknown category is higher for the typical user. Warnings for unknown software aren't blocks. Users can choose to download and run the application normally if they wish to.

Once Microsoft gathers enough data, its security solutions can make a determination. They either find no threats or categorize an application or software as malware or potentially unwanted software.

## Malware

Malware is an application or code that compromises user security. Malware can steal your personal information, lock your device until you pay a ransom, use your device to send spam, or download other malware. In general, malware wants to trick, cheat, or defraud users, placing them in vulnerable states.

Microsoft classifies most malware into one of the following categories:

- **Backdoor:** A type of malware that gives malicious hackers remote access to and control of your device.

- **Command and Control:** A type of malware that infects your device and establishes communication with the hackers' command-and-control server to receive instructions. Once communication is established, hackers can send commands that can steal data, shut down and reboot the device, and disrupt web services.

- **Downloader:** A type of malware that downloads other malware onto your device. It must connect to the internet to download files.

- **Dropper:** A type of malware that installs other malware files onto your device. Unlike a downloader, a dropper doesn't need to connect to the internet to drop malicious files. The dropped files are typically embedded in the dropper itself.

- **Exploit:** A piece of code that uses software vulnerabilities to gain access to your device and perform other tasks, such as installing malware.

- **Hacktool:** A type of tool that can be used to gain unauthorized access to your device.

- **Macro virus:** A type of malware that spreads through infected documents, such as Microsoft Word or Excel documents. The virus runs when you open an infected document.

- **Obfuscator:** A type of malware that hides its code and purpose, making it more difficult for security software to detect or remove.

- **Password stealer:** A type of malware that gathers your personal information, such as usernames and passwords. It often works along with a key logger, which collects and sends information about the keys you press and websites you visit.

- **Ransomware:** A type of malware that encrypts your files or makes other modifications that can prevent you from using your device. It then displays a ransom note that states you must pay money or perform other actions before you can use your device again. [See more information about ransomware](/security/ransomware/human-operated-ransomware).

- **Rogue security software:** Malware that pretends to be security software but doesn't provide any protection. This type of malware usually displays alerts about nonexistent threats on your device. It also tries to convince you to pay for its services.

- **Trojan:** A type of malware that attempts to appear harmless. Unlike a virus or a worm, a trojan doesn't spread by itself. Instead, it tries to look legitimate to trick users into downloading and installing it. Once installed, trojans perform various malicious activities such as stealing personal information, downloading other malware, or giving attackers access to your device.

- **Trojan clicker:** A type of trojan that automatically clicks buttons or similar controls on websites or applications. Attackers can use this trojan to click on online advertisements. These clicks can skew online polls or other tracking systems and can even install applications on your device.

- **Worm:** A type of malware that spreads to other devices. Worms can spread through email, instant messaging, file sharing platforms, social networks, network shares, and removable drives. Sophisticated worms take advantage of software vulnerabilities to propagate.

## Unwanted software

Microsoft believes that you should have control over your Windows experience. Software running on Windows should keep you in control of your device through informed choices and accessible controls. Microsoft identifies software behaviors that ensure you stay in control. Microsoft classifies software that doesn't fully demonstrate these behaviors as "unwanted software".

### Lack of choice

You must be notified about what is happening on your device, including what software does and whether it's active.

Software that exhibits lack of choice might:

- Fail to provide prominent notice about the behavior of the software and its purpose and intent.

- Fail to clearly indicate when the software is active. It might also attempt to hide or disguise its presence.

- Install, reinstall, or remove software without your permission, interaction, or consent.

- Install other software without a clear indication of its relationship to the primary software.

- Circumvent user consent dialogs from the browser or operating system.

- Falsely claim to be software from Microsoft.

Software must not mislead or coerce you into making decisions about your device. This behavior limits your choices. In addition to the previous list, software that exhibits lack of choice might:

- Display exaggerated claims about your device's health.

- Make misleading or inaccurate claims about files, registry entries, or other items on your device.

- Display claims in an alarming manner about your device's health and require payment or certain actions in exchange for fixing the purported problems.

Software that stores or transmits your activities or data must:

- Give you notice and get consent to do so. Software shouldn't include an option that configures it to hide activities associated with storing or transmitting your data.

### Lack of control

You must be able to control software on your device. You must be able to start, stop, or otherwise revoke authorization to software.

Software that exhibits lack of control might:

- Prevent or limit you from viewing or modifying browser features or settings.

- Open browser windows without authorization.

- Redirect web traffic without giving notice and getting consent.

- Modify or manipulate webpage content without your consent.

Software that changes your browsing experience must only use the browser's supported extensibility model for installation, execution, disabling, or removal. Browsers that don't provide supported extensibility models are considered nonextensible and shouldn't be modified.

### Installation and removal

You must be able to start, stop, or otherwise revoke authorization given to software. Software should get your consent before installing, and it must provide a clear and straightforward way for you to install, uninstall, or disable it.

Software that delivers a *poor installation experience* might bundle or download other "unwanted software" as classified by Microsoft.

Software that delivers a *poor removal experience* might:

- Present confusing or misleading prompts or pop-ups when you try to uninstall it.

- Fail to use standard install or uninstall features, such as **Add or Remove Programs**.

### Advertising and advertisements

Software that promotes a product or service outside of the software itself can interfere with your computing experience. You should have clear choice and control when installing software that presents advertisements.

The advertisements that software presents must:

- Include an obvious way for users to close the advertisement. The act of closing the advertisement must not open another advertisement.

- Include the name of the software that presented the advertisement.

The software that presents these advertisements must:

- Provide a standard uninstall method for the software using the same name as shown in the advertisement it presents.

Advertisements shown to you must:

- Be distinguishable from website content.

- Not mislead, deceive, or confuse.

- Not contain malicious code.

- Not invoke a file download.

### Consumer opinion

Microsoft maintains a worldwide network of analysts and intelligence systems where you can [submit software for analysis](https://www.microsoft.com/wdsi/filesubmission). Your participation helps Microsoft identify new malware quickly. After analysis, Microsoft creates security intelligence for software that meets the described criteria. This security intelligence identifies the software as malware and is available to all users through Microsoft Defender Antivirus and other Microsoft anti-malware solutions.

## Tampering software

Tampering software includes a broad range of tools and threats that directly or indirectly lower the overall security of devices. Examples of common tampering actions include:

* **Disabling or uninstalling security software**: Tools and threats that attempt to evade defense mechanisms by disabling or uninstalling security software, such as antivirus, EDR, or network protection systems. These actions leave the system vulnerable to further attacks.

* **Abusing operating system features and settings**: Tools and threats that exploit features and settings within the operating system to compromise security. Examples include:

- **Firewall abuse**: Attackers use firewall components to indirectly tamper with security software or block legitimate network connections, which potentially enables unauthorized access or data exfiltration.

- **DNS manipulation**: Tampering with DNS settings to redirect traffic or block security updates, which leaves the system exposed to malicious activities.

- **Safe mode exploitation**: Using the legitimate Safe Mode setting to put the device in a state where security solutions might be bypassed, which allows for unauthorized access or malware execution.

* **Manipulating system components**: Tools and threats that target critical system components, such as kernel drivers or system services, to compromise the overall security and stability of the device.

* **Privilege escalation**: Techniques that elevate user privileges to gain control over the system's resources and potentially manipulate security settings.

* **Interfering with security updates**: Attempts to block or manipulate security updates, which leaves the system vulnerable to known vulnerabilities.

* **Disrupting critical services**: Actions that disrupt essential system services or processes, which potentially cause system instability and opens the door for other attacks.

* **Unauthorized registry changes**: Modifications to the Windows Registry or system settings that impact the security posture of the device.

* **Tampering with boot processes**: Efforts to manipulate the boot process, which can result in the loading of malicious code during startup.

## Potentially unwanted application (PUA)

PUA protection safeguards user productivity and ensures enjoyable Windows experiences. This protection helps deliver more productive, performant, and delightful Windows experiences. For instruction on how to enable PUA protection in Chromium-based Microsoft Edge and Microsoft Defender Antivirus, see [Detect and block potentially unwanted applications](/microsoft-365/security/defender-endpoint/detect-block-potentially-unwanted-apps-microsoft-defender-antivirus).

*PUAs aren't considered malware.*

Microsoft uses specific categories and the category definitions to classify software as a PUA.

- **Advertising software:** Software that displays advertisements or promotions, or prompts you to complete surveys for other products or services in software other than itself. This category includes software that inserts advertisements to webpages.

- **Torrent software (Enterprise only):** Software that you use to create or download torrents or other files used with peer-to-peer file-sharing technologies.

- **Cryptomining software (Enterprise only):** Software that uses your device resources to mine cryptocurrencies.

- **Bundling software:** Software that offers to install other software that isn't developed by the same entity or not required for the software to run. This category also includes software that offers to install other software that qualifies as PUA based on the criteria outlined in this document.

- **Marketing software:** Software that monitors and transmits the activities of users to applications or services other than itself for marketing research.

- **Evasion software:** Software that actively tries to evade detection by security products, including software that behaves differently in the presence of security products.

- **Poor industry reputation:** Trusted security providers detect this software with their security products. The security industry is dedicated to protecting customers and improving their experiences. Microsoft and other organizations in the security industry continuously exchange knowledge about files they analyze to provide users with the best possible protection.

## Vulnerable software

Vulnerable software is an application or code that has security flaws or weaknesses. Attackers can exploit these vulnerabilities to perform various malicious and potentially destructive actions. These vulnerabilities might stem from unintentional coding errors or design flaws. If exploited, they can lead to harmful activities such as unauthorized access, privilege escalation, tampering, and more.

### Vulnerable drivers

Despite strict requirements and reviews imposed on code running in kernel mode, device drivers remain susceptible to various types of vulnerabilities and bugs. These vulnerabilities and bugs include intentional design oversights that undermine the security promise of the operating system. Examples include memory corruption and arbitrary read and write bugs. Attackers can exploit these bugs to execute more significant malicious and destructive actions -– actions typically restricted in user mode. Terminating critical processes on a device is an example of such malicious action.


# Submission Guide

# Submit files for analysis

If you have a file that you suspect might be malware or is being incorrectly detected, you can submit it to us for analysis. This page has answers to some common questions about submitting a file for analysis.

> [!TIP]

> If your organization's subscription includes [Microsoft Defender for Endpoint Plan 2](/defender-endpoint/microsoft-defender-endpoint), [Microsoft Defender for Office 365 Plan 2](/defender-office-365/mdo-about), or [Microsoft Defender XDR](/defender-xdr/microsoft-365-defender), you can use the [new unified submissions portal](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/unified-submissions-in-microsoft-365-defender-now-generally/ba-p/3270770). To learn more, see [Submit files in Microsoft Defender for Endpoint](/defender-endpoint/admin-submissions-mde).

## How do I submit a file to Microsoft for analysis?

> [!IMPORTANT]

> Starting May 20, 2024, [file submissions](https://www.microsoft.com/en-us/wdsi/filesubmission) will be transitioning to a new [Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id). If your tenant requires admin consent to continue accessing this service, refer to [Overview of user and admin consent](/entra/identity/enterprise-apps/user-admin-consent-overview) and grant access to app ID: 6ba09155-cb24-475b-b24f-b4e28fc74365 with graph permissions for Directory.Read.All and User.Read.

### Send a malware file

You can send files that you think might be malware or files that were incorrectly detected through the [sample submission portal](https://www.microsoft.com/wdsi/filesubmission).

You can complete a quick analysis by providing detailed information about the product you were using and what you were doing when you found the file.

After you sign in, you'll be able to track your submissions.

> [!NOTE]

> You can use the Microsoft Security Intelligence submission feature even if you don't have Microsoft Defender for Endpoint Plan 2 or Microsoft Defender for Office Plan 2.

### Submit a suspected email attachment

Use the [Microsoft Defender portal](https://security.microsoft.com/) to submit suspected email attachments to Microsoft for review. For more information, see [Submit a suspected email attachment to Microsoft](/defender-office-365/submissions-admin).

### Submit a file or file hash

Use the unified submissions feature in Microsoft Defender for Endpoint to submit files and file hashes to Microsoft for review. For more information, see [Submit files in Microsoft Defender for Endpoint](/defender-endpoint/admin-submissions-mde).

## Can I send a sample by email?

No, we only accept submissions through our [sample submission portal](https://www.microsoft.com/wdsi/filesubmission).

## Can I submit a sample without signing in?

No. If you're an enterprise customer, you need to sign in so that we can prioritize your submission appropriately. If you're currently experiencing a virus outbreak or security-related incident, you should contact your designated Microsoft support professional or go to [Microsoft Support](https://support.microsoft.com/) for immediate assistance.

## What is the Software Assurance ID (SAID)?

The [Software Assurance ID (SAID)](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx) is for enterprise customers to track support entitlements. The submission portal accepts and retains SAID information and allows customers with valid SAIDs to make higher priority submissions.

### How do I dispute the detection of my program?

[Submit the file](https://www.microsoft.com/wdsi/filesubmission) in question as a software developer. Wait until your submission has a final determination.

If you're not satisfied with our determination of the submission, use the developer contact form provided with the submission results to reach Microsoft. We'll use the information you provide to investigate further if necessary.

We encourage all software vendors and developers to read about [how Microsoft identifies malware and unwanted software](criteria.md).

## How do I track or view past sample submissions?

You can track your submissions through the [submission history page](https://www.microsoft.com/wdsi/submissionhistory).

## What does the submission status mean?

Each submission is shown to be in one of the following status types:

* Submitted—the file has been received

* In progress—an analyst has started checking the file

* Closed—a final determination has been given by an analyst

You can see the status of any files you submit to us on the [submission history page](https://www.microsoft.com/wdsi/submissionhistory).

## How does Microsoft prioritize submissions

Processing submissions take dedicated analyst resource. Because we regularly receive a large number of submissions, we handle them based on a priority. The following factors affect how we prioritize submissions:

* Prevalent files with the potential to impact large numbers of computers are prioritized.

* Authenticated customers, especially enterprise customers with valid [Software Assurance IDs (SAIDs)](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx), are given priority.

* Submissions flagged as high priority by SAID holders are given immediate attention.

Your submission is immediately scanned by our systems to give you the latest determination even before an analyst starts handling your case. Note that the same file may have already been processed by an analyst. To check for updates to the determination, select rescan on the submission details page.

## See also

[Exclusions for Microsoft Defender for Endpoint and Microsoft Defender Antivirus](/defender-endpoint/defender-endpoint-antivirus-exclusions)


# Virus Initiative Criteria

# Microsoft Virus Initiative

The Microsoft Virus Initiative (MVI) helps organizations improve the security solutions our customers rely on to keep them safe. We provide tools, resources, and knowledge to support better-together experiences with great performance, reliability, and compatibility.

Microsoft collaborates with MVI partners to define and follow Safe Deployment Practices (SDP) to support the safety and resiliency of our mutual customers. Microsoft also engages MVI partners in the development of new platform capabilities to create highly available security solutions building on the foundational security features in Windows 11.

## Become a member

You can request membership if you're a representative of an organization that develops antimalware technology. Not all applicants are accepted into the program.

To be considered for the MVI program, your organization must meet all the following requirements:

1. Your commercially available security solution must provide real-time protection that detects, prevents, and remediates malicious software.

2. Your organization is responsible for both developing and distributing updates to end-customers that address compatibility with Windows.

3. Your organization must be active in the antimalware industry with a positive reputation, shown by participation in industry conferences, membership in industry organizations, or reviews in reports like AV-Comparatives, OPSWAT, or Gartner.

4. Your organization must sign a non-disclosure agreement with Microsoft.

5. Your organization must sign a program license agreement.

6. Your organization must be active in the program and meet all program requirements.

7. Your security solution must meet all program requirements, which requires use of [Trusted Signing](/azure/trusted-signing).

8. Your security solution must be certified within the last 12 months by at least one of the organizations listed below through independent testing. Yearly certification must be maintained.

|Test Provider|Lab Test Type|Minimum Level/Score|

|---|---|---|

|[AV-Comparatives](https://www.av-comparatives.org/testmethod/real-world-protection-tests)|Real-World Protection Test or Malware Protection Test|Certified/Approved/Standard|

|[AVLab Cybersecurity Foundation](https://avlab.pl/en/)|Advanced In-The-Wild Malware Test|Excellent (99.6%)|

|[AV-Test](https://www.av-test.org/en/about-the-institute/certification)|Real-World Protection Test for MVI, AV-Test|97% (Real-World Protection test for MVI)/Certified (AV-Test Home)/Approved (AV-Test Enterprise)|

|[MRG Effitas](https://www.mrg-effitas.com/)|360 Assessment and Certification|Level 2|

|[SE Labs](https://selabs.uk/en/reports/)|Endpoint Security (EPS) or Enterprise Advanced Security (EAS)|AAA|

|[SKD Labs](https://www.skdlabs.com/html/english/)|Starcheck Anti-malware Real-time protection and cleaning|Starcheck Certified|

|[VB 100](https://www.virusbulletin.com/testing/vb100/vb100-methodology/vb100-methodology-ver1-1)|VB100|Detection rate of 95% with Grade C or higher|

|[West Coast Labs](https://www.westcoastlabs.com/wclvalid)|WCL Validated for Malware Detection and Malware Remediation technologies|Product Rating A|

## Apply now

If your organization meets these criteria and is interested in joining, [apply for membership now](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbRxusDUkejalGp0OAgRTWC7BUQVRYUEVMNlFZUjFaUDY2T1U1UDVVU1NKVi4u). Applications are reviewed monthly.


# Mininum Access Requirements

The minimal required permission for an analyst to view Microsoft Sentinel data is to delegate permissions for the Azure RBAC Sentinel Reader role. These permissions are also applied to the unified portal. Without these permissions, the Microsoft Sentinel navigation menu isn't available on the unified portal, despite the analyst having access to the Microsoft Defender portal.

A best practice is to have all Microsoft Sentinel related resources in the same Azure resource group, then delegate Microsoft Sentinel role permissions (like the Sentinel Reader role) at the resource group level that contains the Microsoft Sentinel workspace. By doing this, the role assignment applies to all the resources that support Microsoft Sentinel.
