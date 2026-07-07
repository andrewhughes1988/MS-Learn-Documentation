# Overview

# What is Azure Web Application Firewall?

**Applies to:** :heavy_check_mark: Application Gateway :heavy_check_mark: Front Door Standard/Premium :heavy_check_mark: Front Door (classic) :heavy_check_mark: CDN Standard from Microsoft (classic)

Azure Web Application Firewall provides centralized protection of your web applications from common exploits and vulnerabilities. Web applications increasingly encounter malicious attacks that exploit commonly known vulnerabilities. SQL injection and cross-site scripting are among the most common attacks.

> [!VIDEO https://learn-video.azurefd.net/vod/player?id=b23e4db1-5007-4f42-ae55-3a564a4ab7d3]

![Diagram that shows Azure Web Application Firewall blocking certain types of access to network resources.](media/overview/wafoverview.png)

Preventing such attacks in application code is challenging. It can require rigorous maintenance, patching, and monitoring at multiple layers of the application topology. A centralized web application firewall (WAF) helps make security management simpler. A WAF also gives application administrators better assurance of protection against threats and intrusions.

A WAF solution can react to a security threat faster by centrally patching a known vulnerability, instead of securing each individual web application.

> [!NOTE]

> Azure Web Application Firewall is one of the services in the category of network security for Azure. Other services in this category include [Azure DDoS Protection](../ddos-protection/ddos-protection-overview.md) and [Azure Firewall](../firewall/overview.md). Each service has its own unique features and use cases. For more information on this service category, see [What is Azure network security?](../networking/security/network-security.md)

## Supported services

Azure Web Application Firewall can be deployed with these Microsoft services:

- Azure Application Gateway

- Azure Application Gateway for Containers

- Azure Front Door

- Azure Content Delivery Network

Azure Web Application Firewall on Azure Content Delivery Network is currently in preview. Azure Web Application Firewall has features that are customized for each specific service.

## Related content

- [What is Azure Web Application Firewall on Azure Application Gateway?](./ag/ag-overview.md)

- [Azure Web Application Firewall on Azure Application Gateway for Containers?](/azure/application-gateway/for-containers/web-application-firewall)

- [Azure Web Application Firewall on Azure Front Door](./afds/afds-overview.md)

- [Azure Web Application Firewall on Azure Content Delivery Network](./cdn/cdn-overview.md)

- [Introduction to Azure Web Application Firewall](/training/modules/introduction-azure-web-application-firewall/) (training module)

- [Azure network security documentation](../networking/security/index.yml)


# Ag Overview

# What is Azure Web Application Firewall on Azure Application Gateway?

**Applies to:** :heavy_check_mark: Application Gateway

An Azure Web Application Firewall deployment on Azure Application Gateway actively safeguards your web applications against common exploits and vulnerabilities. As web applications become more frequent targets for malicious attacks, these attacks often exploit well-known vulnerabilities such as SQL injection and cross-site scripting.

Azure Web Application Firewall on Application Gateway is based on the [Core Rule Set (CRS)](application-gateway-crs-rulegroups-rules.md) from the Open Web Application Security Project (OWASP).

All of the following Azure Web Application Firewall features exist inside a web application firewall (WAF) policy. You can create multiple policies and associate them with an application gateway, with individual listeners, or with path-based routing rules on an application gateway. This association enables you to define separate policies for each site behind your application gateway if necessary. For more information on WAF policies, see [Create WAF policies for Application Gateway](create-waf-policy-ag.md).

> [!NOTE]

> Application Gateway has two versions of a web application firewall: WAF_v1 and WAF_v2. WAF policy associations are supported only for WAF_v2.

Application Gateway operates as an application delivery controller. It offers Transport Layer Security (TLS) (previously known as Secure Sockets Layer or SSL) termination, cookie-based session affinity, round-robin load distribution, content-based routing, the ability to host multiple websites, and security enhancements.

Application Gateway enhances security through TLS policy management and end-to-end TLS support. Integrating Azure Web Application Firewall into Application Gateway fortifies application security. This combination actively defends your web applications against common vulnerabilities and offers a centrally manageable location.

## Benefits

This section describes the core benefits that Azure Web Application Firewall on Application Gateway provides.

### Protection

- Protect your web applications from web vulnerabilities and attacks without modifying back-end code.

- Protect multiple web applications at the same time. One instance of Application Gateway can host up to 40 websites that use a web application firewall.

- Create custom WAF policies for different sites behind the same WAF.

- Protect your web applications from malicious bots by using the IP Reputation Rule Set.

- Protect your application against DDoS attacks. For more information, see [Application (Layer 7) DDoS protection](../shared/application-ddos-protection.md).

### Monitoring

- Monitor attacks against your web applications by using a real-time WAF log. [Azure Monitor](/azure/azure-monitor/overview?toc=/azure/web-application-firewall/toc.json) integrates with the log to track WAF alerts and monitor trends.

- Microsoft Defender for Cloud integrates with the Application Gateway WAF. Defender for Cloud provides a central view of the security state of all your Azure, hybrid, and multicloud resources.

### Customization

- Customize WAF rules and rule groups to suit your application requirements and eliminate false positives.

- Associate a WAF policy for each site behind your WAF to allow for site-specific configuration.

- Create custom rules to suit the needs of your application.

## Features

- Protection against SQL injection.

- Protection against cross-site scripting.

- Protection against other common web attacks, such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion.

- Protection against HTTP protocol violations.

- Protection against HTTP protocol anomalies such as missing `Host`, `User-Agent`, and `Accept` headers.

- Protection against crawlers and scanners.

- Detection of common application misconfigurations (for example, Apache and IIS).

- Configurable request size limits with lower and upper bounds.

- Exclusion lists that let you omit certain request attributes from a WAF evaluation. A common example is Active Directory-inserted tokens that are used for authentication or password fields.

- Ability to create custom rules to suit the specific needs of your applications.

- Ability to geo-filter traffic, to allow or block certain countries/regions from gaining access to your applications.

- Bot Manager Rule Set that helps protect your applications from bots.

- Ability to inspect JSON and XML in the request body.

## WAF policy and rules

To use a web application firewall on Application Gateway, you must create a WAF policy. This policy contains all of the managed rules, custom rules, exclusions, and other customizations, such as the file upload limit.

You can configure a WAF policy and associate that policy with one or more application gateways for protection. A WAF policy consists of two types of security rules:

- Custom rules that you create

- Managed rule sets that are collections of Azure-managed preconfigured rules

When both types of rules are present, the WAF processes custom rules before it processes the rules in a managed rule set.

A rule consists of a match condition, a priority, and an action. Supported action types are `ALLOW`, `BLOCK`, and `LOG`. By combining managed and custom rules, you can create a fully customized policy that meets your specific requirements for application protection.

The WAF processes rules within a policy in priority order. Priority is a unique integer that defines the order of rules to process. A smaller integer value denotes a higher priority, so the WAF evaluates those rules before rules that have a higher integer value. After the WAF matches a rule with a request, it applies the corresponding action that the rule defines to the request. After the WAF processes such a match, it doesn't process rules that have lower priorities.

A web application that Application Gateway delivers can have a WAF policy associated with it at the global level, at a per-site level, or at a per-URI level.

### Custom rules

Application Gateway supports the creation of your own custom rules. Application Gateway evaluates custom rules for each request that passes through the WAF. These rules have a higher priority than the rest of the rules in the managed rule sets. If a request meets a set of conditions, the WAF takes an action to allow or block. For more information on custom rules, see [Custom rules for Application Gateway](custom-waf-rules-overview.md).

The `Geomatch` operator is now available for custom rules. For more information, see [Geomatch custom rules](geomatch-custom-rules.md).

### Rule sets

Application Gateway supports multiple rule sets, including CRS 3.2, CRS 3.1, and CRS 3.0. These rules help protect your web applications from malicious activity. For more information, see [Web application firewall DRS and CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).

#### Bot Manager Rule Set

You can enable a managed Bot Manager Rule Set to take custom actions on requests from all bot categories.

Application Gateway supports three bot categories:

- **Bad bots**: Bots that have malicious IP addresses or that falsify their identities. Malicious IP addresses might come from the Microsoft Threat Intelligence feed's high-confidence IP Indicators of Compromise and from IP reputation feeds. Bad bots also include bots that identify themselves as good bots but have IP addresses that don't belong to legitimate bot publishers.

- **Good bots**: Trusted user agents. Rules for good bots are sorted into multiple categories to provide granular control over WAF policy configuration. These categories include:

- Verified search engine bots (such as Googlebot and Bingbot).

- Validated link checker bots.

- Verified social media bots (such as FacebookBot and LinkedInBot).

- Verified advertising bots.

- Verified content checker bots.

- Validated miscellaneous bots.

- **Unknown bots**: User agents without additional validation. Unknown bots might also have malicious IP addresses that come from the Microsoft Threat Intelligence feed's medium-confidence IP Indicators of Compromise.

Azure Web Application Firewall actively manages and dynamically updates the bot signatures.

When you turn on bot protection, it blocks, allows, or logs incoming requests that match bot rules based on the configured action. It blocks malicious bots, allows verified search engine crawlers, blocks unknown search engine crawlers, and logs unknown bots by default. You can set custom actions to block, allow, or log various types of bots.

You can access WAF logs from a storage account, an event hub, or Log Analytics. You can also send logs to a partner solution.

For more information about Application Gateway bot protection, see [Web Application Firewall on Application Gateway bot protection overview](bot-protection-overview.md).

### WAF modes

You can configure the Application Gateway WAF to run in the following modes:

- **Detection mode**: Monitors and logs all threat alerts. Turn on logging diagnostics for Application Gateway in the **Diagnostics** section. You must also make sure that the WAF log is selected and turned on. A web application firewall doesn't block incoming requests when it's operating in detection mode.

- **Prevention mode**: Blocks intrusions and attacks that the rules detect. The attacker receives a "403 unauthorized access" exception, and the connection is closed. Prevention mode records such attacks in the WAF logs.

> [!NOTE]

> Run a newly deployed WAF in detection mode for a short period in a production environment. This period provides the opportunity to obtain [firewall logs](../../application-gateway/application-gateway-diagnostics.md#firewall-log) and update any exceptions or [custom rules](./custom-waf-rules-overview.md) before transitioning to prevention mode. It also helps reduce the occurrence of unexpected blocked traffic.

### WAF engine

The WAF engine is the component that inspects traffic and detects whether a request contains a signature that indicates a potential attack. When you use CRS 3.2 or later, your web application firewall runs the new [WAF engine](waf-engine.md), which gives you higher performance and an improved set of features. When you use earlier versions of the CRS, your WAF runs on an older engine. New features are available only on the new WAF engine.

### WAF actions

Choose which action the WAF runs when a request matches a rule condition. Application Gateway supports the following actions:

- **Allow**: The request passes through the WAF and is forwarded to the back end. No further lower-priority rules can block this request. These actions apply only to the Bot Manager Rule Set. They don't apply to the CRS.

- **Block**: The request is blocked. The WAF sends a response to the client without forwarding the request to the back end.

- **Log**: The request is logged in the WAF logs. The WAF continues to evaluate lower-priority rules.

- **Anomaly score**: This action is the default for the CRS. The total anomaly score is incremented when a request matches a rule with this action. Anomaly scoring doesn't apply to the Bot Manager Rule Set.

### Anomaly scoring mode

OWASP has two modes for deciding whether to block traffic: traditional and anomaly scoring.

In traditional mode, traffic that matches any rule is considered independently of any other rule matches. This mode is easy to understand, but the lack of information about how many rules match a specific request is a limitation. So, anomaly scoring mode was introduced as the default for OWASP 3.*x*.

In anomaly scoring mode, traffic that matches any rule isn't immediately blocked when the firewall is in prevention mode. Rules have a certain severity: **Critical**, **Error**, **Warning**, or **Notice**. That severity affects a numeric value for the request, which is the anomaly score. For example, one **Warning** rule match contributes 3 to the score. One **Critical** rule match contributes 5.

|Severity  |Value  |

|---------|---------|

|Critical     |5|

|Error        |4|

|Warning      |3|

|Notice       |2|

There's a threshold of 5 for the anomaly score to block traffic. So, a single **Critical** rule match is enough for the Application Gateway WAF to block a request in prevention mode. But one **Warning** rule match only increases the anomaly score by 3, which isn't enough by itself to block the traffic.

> [!NOTE]

> The message that's logged when a WAF rule matches traffic includes the action value **Matched**. If the total anomaly score of all matched rules is 5 or greater, and the WAF policy is running in prevention mode, the request triggers a mandatory anomaly rule with the action value **Blocked**, and the request is stopped. If the WAF policy is running in detection mode, the request triggers the action value **Detected**, and the request is logged and passed to the back end. For more information, see [Understand WAF logs](web-application-firewall-troubleshoot.md#understand-waf-logs).

### Configuration

You can configure and deploy all WAF policies by using the Azure portal, REST APIs, Azure Resource Manager templates, and Azure PowerShell. You can also configure and manage WAF policies at scale by using Azure Firewall Manager integration. For more information, see [Configure WAF policies using Azure Firewall Manager](../shared/manage-policies.md).

### WAF monitoring

Monitoring the health of your application gateway is important. You can achieve this monitoring by integrating your WAF (and the applications that it helps protect) with Microsoft Defender for Cloud, Azure Monitor, and Azure Monitor Logs.

#### Azure Monitor

Application Gateway logs are integrated with [Azure Monitor](/azure/azure-monitor/overview?toc=/azure/web-application-firewall/toc.json) so that you can track diagnostic information, including WAF alerts and logs. You can access this capability in the Azure portal, on the **Diagnostics** tab of the Application Gateway resource. Or you can access it directly in Azure Monitor.

To learn more about using logs, see [Diagnostic logs for Application Gateway](../../application-gateway/application-gateway-diagnostics.md).

#### Microsoft Defender for Cloud

[Defender for Cloud](../../security-center/security-center-introduction.md?toc=/azure/web-application-firewall/toc.json) helps you prevent, detect, and respond to threats. It provides increased visibility into, and control over, the security of your Azure resources. Application Gateway is [integrated with Defender for Cloud](../../security-center/security-center-partner-integration.md#integrated-azure-security-solutions).

Defender for Cloud scans your environment to detect unprotected web applications. It can recommend an Application Gateway WAF to help protect these vulnerable resources.

You create the firewalls directly from Defender for Cloud. These WAF instances are integrated with Defender for Cloud. They send alerts and health information to Defender for Cloud for reporting.

#### Microsoft Sentinel

[Microsoft Sentinel](/azure/sentinel/overview?toc=/azure/web-application-firewall/toc.json) is a scalable, cloud-native solution that encompasses security information event management (SIEM) and security orchestration automated response (SOAR). Microsoft Sentinel delivers intelligent security analytics and threat intelligence across the enterprise. It provides a single solution for alert detection, threat visibility, proactive hunting, and threat response.

With the firewall events workbook built into Azure Web Application Firewall, you can get an overview of the security events on your WAF. The overview includes matched rules, blocked rules, and all other logged firewall activity.

#### Azure Monitor workbook for WAF

The Azure Monitor workbook for WAF enables custom visualization of security-relevant WAF events across several filterable panels. It works with all WAF types, including Application Gateway, Azure Front Door, and Azure Content Delivery Network.

You can filter this workbook based on WAF type or a specific WAF instance. You import it via Azure Resource Manager template or gallery template.

To deploy this workbook, see the [GitHub repository for Azure Web Application Firewall](https://aka.ms/AzWAFworkbook).

#### Logging

The Application Gateway WAF provides detailed reporting on each threat that it detects. Logging is integrated with Azure Diagnostics logs. Alerts are recorded in JSON format. You can integrate these logs with [Azure Monitor Logs](/previous-versions/azure/azure-monitor/insights/azure-networking-analytics?toc=/azure/web-application-firewall/toc.json).

```json

{

"resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupId}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{appGatewayName}",

"operationName": "ApplicationGatewayFirewall",

"time": "2017-03-20T15:52:09.1494499Z",

"category": "ApplicationGatewayFirewallLog",

"properties": {

{

"instanceId": "ApplicationGatewayRole_IN_0",

"clientIp": "203.0.113.145",

"clientPort": "0",

"requestUri": "/",

"ruleSetType": "OWASP",

"ruleSetVersion": "3.0",

"ruleId": "920350",

"ruleGroup": "920-PROTOCOL-ENFORCEMENT",

"message": "Host header is a numeric IP address",

"action": "Matched",

"site": "Global",

"details": {

"message": "Warning. Pattern match \"^[\\\\d.:]+$\" at REQUEST_HEADERS:Host ....",

"data": "127.0.0.1",

"file": "rules/REQUEST-920-PROTOCOL-ENFORCEMENT.conf",

"line": "791"

},

"hostname": "127.0.0.1",

"transactionId": "16861477007022634343"

"policyId": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/drewRG/providers/Microsoft.Network/ApplicationGatewayWebApplicationFirewallPolicies/globalWafPolicy",

"policyScope": "Global",

"policyScopeName": " Global "

}

}

}

```

## Application Gateway WAF pricing

The WAF_v1 and WAF_v2 versions use different pricing models. For more information, see [Application Gateway pricing](https://azure.microsoft.com/pricing/details/application-gateway/).

## What's new

To learn what's new with Azure Web Application Firewall, see [Azure updates](https://azure.microsoft.com/updates?filters=%5B%22Web+Application+Firewall%22%5D).

## Related content

- [Azure Web Application Firewall DRS and CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md)

- [Custom rules for Azure Web Application Firewall v2 on Azure Application Gateway](custom-waf-rules-overview.md)

- [Azure Web Application Firewall on Azure Front Door](../afds/afds-overview.md)

- [Azure network security documentation](../../networking/security/index.yml)


# Afds Overview

# Azure Web Application Firewall on Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard/Premium :heavy_check_mark: Front Door (classic) :heavy_check_mark: CDN Standard from Microsoft (classic)

Azure Web Application Firewall on Azure Front Door provides centralized protection for your web applications. A web application firewall (WAF) defends your web services against common exploits and vulnerabilities. It keeps your service highly available for your users and helps you meet compliance requirements.

Azure Web Application Firewall on Azure Front Door is a global and centralized solution. It's deployed on Azure network edge locations around the globe. WAF-enabled web applications inspect every incoming request delivered by Azure Front Door at the network edge.

A WAF prevents malicious attacks close to the attack sources before they enter your virtual network. You get global protection at scale without sacrificing performance. A WAF policy easily links to any Azure Front Door profile in your subscription. New rules can be deployed within minutes, so you can respond quickly to changing threat patterns.

[!INCLUDE [ddos-waf-recommendation](../../../includes/ddos-waf-recommendation.md)]

Azure Front Door has [two tiers](../../frontdoor/standard-premium/overview.md):

- Standard

- Premium

Azure Web Application Firewall is natively integrated with Azure Front Door Premium with full capabilities. For Azure Front Door Standard, only [custom rules](#custom-authored-rules) are supported.

## Protection

Azure Web Application Firewall protects your:

* Web applications from web vulnerabilities and attacks without modifications to back-end code.

* Web applications from malicious bots with the IP Reputation Rule Set.

* Applications against DDoS attacks. For more information, see [Application DDoS protection](../shared/application-ddos-protection.md).

## WAF policy and rules

You can configure a [WAF policy](waf-front-door-create-portal.md) and associate that policy to one or more Azure Front Door domains for protection. A WAF policy consists of two types of security rules:

- Custom rules that the customer created.

- Managed rule sets that are a collection of Azure-managed preconfigured sets of rules.

When both are present, custom rules are processed before processing the rules in a managed rule set. A rule is made of a match condition, a priority, and an action. Action types supported are ALLOW, BLOCK, LOG, and REDIRECT. You can create a fully customized policy that meets your specific application protection requirements by combining managed and custom rules.

Rules within a policy are processed in a priority order. Priority is a unique integer that defines the order of rules to process. A smaller integer value denotes a higher priority, and those rules are evaluated before rules with a higher integer value. After a rule is matched, the corresponding action that was defined in the rule is applied to the request. After such a match is processed, rules with lower priorities aren't processed further.

A web application delivered by Azure Front Door can have only one WAF policy associated with it at a time. However, you can have an Azure Front Door configuration without any WAF policies associated with it. If a WAF policy is present, it's replicated to all of our edge locations to ensure consistent security policies across the world.

## WAF modes

You can configure a WAF policy to run in two modes:

- **Detection**: When a WAF runs in detection mode, it only monitors and logs the request and its matched WAF rule to WAF logs. It doesn't take any other actions. You can turn on logging diagnostics for Azure Front Door. When you use the portal, go to the **Diagnostics** section.

- **Prevention**: In prevention mode, a WAF takes the specified action if a request matches a rule. If a match is found, no further rules with lower priority are evaluated. Any matched requests are also logged in the WAF logs.

## WAF actions

WAF customers can choose to run from one of the actions when a request matches a rule's conditions:

- **Allow**: The request passes through the WAF and is forwarded to the origin. No further lower priority rules can block this request.

- **Block**: The request is blocked and the WAF sends a response to the client without forwarding the request to the origin.

- **Log**: The request is logged in the WAF logs and the WAF continues evaluating lower priority rules.

- **Redirect**: The WAF redirects the request to the specified URI. The URI specified is a policy-level setting. After configuration, all requests that match the **Redirect** action are sent to that URI.

- **Anomaly score**: The total anomaly score is increased incrementally when a rule with this action is matched. This default action is for Default Rule Set 2.0 or later. It isn't applicable for the Bot Manager Rule Set.

## WAF rules

A WAF policy can consist of two types of security rules:

- Custom rules, authored by the customer and managed rule sets

- Azure-managed preconfigured sets of rules

### Custom-authored rules

To configure custom rules for a WAF, use the following controls:

- **IP allow list and block list**: You can control access to your web applications based on a list of client IP addresses or IP address ranges. Both IPv4 and IPv6 address types are supported. This list can be configured to either block or allow those requests where the source IP matches an IP in the list.

- **Geographic-based access control**: You can control access to your web applications based on the country code that's associated with a client's IP address.

- **HTTP parameters-based access control**: You can base rules on string matches in HTTP/HTTPS request parameters. Examples include query strings, POST args, Request URI, Request Header, and Request Body.

- **Request method-based access control**: You base rules on the HTTP request method of the request. Examples include GET, PUT, or HEAD.

- **Size constraint**: You can base rules on the lengths of specific parts of a request, such as query string, Uri, or Request Body.

- **Rate limiting rules**: A rate limiting rule limits abnormally high traffic from any client IP address. You might configure a threshold on the number of web requests allowed from a client IP during a one-minute duration. This rule is distinct from an IP list-based allow/block custom rule that either allows all or blocks all requests from a client IP. Rate limits can be combined with other match conditions, such as HTTP(S) parameter matches for granular rate control.

### Azure-managed rule sets

Azure-managed rule sets provide an easy way to deploy protection against a common set of security threats. Because Azure manages these rule sets, the rules are updated as needed to protect against new attack signatures. The Azure-managed Default Rule Set includes rules against the following threat categories:

- Cross-site scripting

- Java attacks

- Local file inclusion

- PHP injection attacks

- Remote command execution

- Remote file inclusion

- Session fixation

- SQL injection protection

- Protocol attackers

Custom rules are always applied before rules in the Default Rule Set are evaluated. If a request matches a custom rule, the corresponding rule action is applied. The request is either blocked or passed through to the back end. No other custom rules or the rules in the Default Rule Set are processed. You can also remove the Default Rule Set from your WAF policies.

For more information, see [Web Application Firewall Default Rule Set rule groups and rules](waf-front-door-drs.md).

### Bot protection rule set

You can enable a managed bot protection rule set to take custom actions on requests from all bot categories.

Three bot categories are supported: *Bad*, *Good*, and *Unknown*. The WAF platform manages and dynamically updates bot signatures.

- **Bad**: Bad bots are bots with malicious IP addresses and bots that falsified their identities. Bad bots include malicious IP addresses that are sourced from the Microsoft Threat Intelligence feed’s high confidence IP Indicators of Compromise and IP reputation feeds. Bad bots also include bots that identify themselves as good bots but their IP addresses don’t belong to legitimate bot publishers.

- **Good**: Good Bots are trusted user agents. Good bot rules are categorized into multiple categories to provide granular control over WAF policy configuration. These categories include verified search engine bots (such as Googlebot and Bingbot), validated link checker bots, verified social media bots (such as Facebookbot and LinkedInBot), verified advertising bots, verified content checker bots, and validated miscellaneous bots.

- **Unknown**: Unknown bots are user agents without additional validation. Unknown bots also include malicious IP addresses that are sourced from Microsoft Threat Intelligence feed’s medium confidence IP Indicators of Compromise.

The WAF platform manages and dynamically updates bot signatures. You can set custom actions to block, allow, log, or redirect for different types of bots.

If bot protection is enabled, incoming requests that match bot rules are blocked, allowed, or logged based on the configured action. Bad bots are blocked, good bots are allowed, and unknown bots are logged by default. You can set custom actions to block, allow, log, or JS challenge for different types of bots. You can access WAF logs from a storage account, event hub, log analytics, or send logs to a partner solution.

The Bot Manager 1.1 rule set is available on Azure Front Door premium version.

For more information, see [Azure WAF’s Bot Manager 1.1 and JavaScript Challenge: Navigating the Bot Threat Terrain](https://techcommunity.microsoft.com/t5/azure-network-security-blog/azure-waf-s-bot-manager-1-1-and-javascript-challenge-navigating/ba-p/4249652).

## Configuration

You can configure and deploy all WAF policies by using the Azure portal, REST APIs, Azure Resource Manager templates, and Azure PowerShell. You can also configure and manage Azure WAF policies at scale by using Firewall Manager integration. For more information, see [Use Azure Firewall Manager to manage Azure Web Application Firewall policies](../shared/manage-policies.md).

## Monitoring

Monitoring for a WAF on Azure Front Door is integrated with Azure Monitor to track alerts and easily monitor traffic trends. For more information, see [Azure Web Application Firewall monitoring and logging](waf-front-door-monitor.md).

## Next steps

- Learn about [Azure Web Application Firewall on Azure Application Gateway](../ag/ag-overview.md).

- Learn more about [Azure network security](../../networking/security/index.yml).


# Cdn Overview

# Azure Web Application Firewall on Azure Content Delivery Network

An Azure Web Application Firewall deployment on Azure Content Delivery Network provides centralized protection for your web content. Azure Web Application Firewall defends your web services against common exploits and vulnerabilities. It helps keep your service highly available for your users and helps you meet compliance requirements.

> [!IMPORTANT]

> The preview of Azure Web Application Firewall on Azure Content Delivery Network is no longer accepting new customers. We encourage customers to use [Azure Web Application Firewall on Azure Front Door](../afds/afds-overview.md) instead.

>

> We provide existing customers with a preview service-level agreement. Certain features might not be supported or might have constrained capabilities. For details, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Azure Web Application Firewall on Azure Content Delivery Network is a global and centralized solution. It's deployed on Azure network edge locations around the globe. Azure Web Application Firewall stops malicious attacks close to the attack sources, before they reach your origin. You get global protection at scale without sacrificing performance.

A web application firewall (WAF) policy links to any content delivery network (CDN) endpoint in your subscription. You can deploy new rules within minutes, so you can respond quickly to changing threat patterns.

![Diagram that shows how Azure Web Application Firewall on Azure Content Delivery Network takes action on incoming requests.](../media/cdn-overview/waf-cdn-overview.png)

## WAF policy and rules

You can configure a WAF policy and associate that policy with one or more CDN endpoints for protection. A WAF policy consists of two types of security rules:

- **Custom rules**: Rules that you can create yourself.

- **Managed rule sets**: Azure-managed preconfigured rules that you can enable.

When both are present, the WAF processes custom rules before processing the rules in a managed rule set.

A rule consists of a match condition, a priority, and an action. Supported action types are `ALLOW`, `BLOCK`, `LOG`, and `REDIRECT`. You can create a fully customized policy that meets your specific requirements for application protection by combining managed and custom rules.

The WAF processes rules within a policy in a priority order. Priority is a unique integer that defines the order of rules to process. Smaller numbers are a higher priority, and the WAF evaluates those rules before rules that have a larger value. After the WAF matches a rule with a request, it applies the corresponding action that the rule defines to the request. After the WAF processes such a match, rules that have lower priorities aren't processed further.

A web application hosted on Azure Content Delivery Network can have only one WAF policy associated with it at a time. However, you can have a CDN endpoint without any WAF policies associated with it. If a WAF policy is present, it's replicated to all edge locations to ensure consistent security policies across the world.

### Custom rules

Custom rules can include:

- **Match rules**: You can configure the following custom match rules:

- **IP allowlist and blocklist**: You can control access to your web applications based on a list of client IP addresses or IP address ranges. Both IPv4 and IPv6 address types are supported.

IP list rules use the `RemoteAddress` IP contained in the `X-Forwarded-For` request header and not the `SocketAddress` value that the WAF uses. You can configure IP lists to either block or allow requests where the `RemoteAddress` IP matches an IP in the list.

If you have a requirement to block requests on the source IP address that the WAF uses (for example, the proxy server address if the user is behind a proxy), you should use the Azure Front Door Standard or Premium tier. For more information, see [Configure an IP restriction rule with a WAF for Azure Front Door](../afds/waf-front-door-configure-ip-restriction.md).

- **Geographic-based access control**: You can control access to your web applications based on the country code that's associated with a client's IP address.

- **HTTP parameters-based access control**: You can base rules on string matches in HTTP or HTTPS request parameters. Examples include query strings, `POST` arguments, request URI, request header, and request body.

- **Request method-based access control**: You can base rules on the HTTP request method of the request. Examples include `GET`, `PUT`, and `HEAD`.

- **Size constraint**: You can base rules on the lengths of specific parts of a request, such as query string, URI, or request body.

- **Rate control rules**: These rules limit abnormally high traffic from any client IP address.

You can configure a threshold on the number of web requests allowed from a client IP address during a one-minute duration. This rule is distinct from an IP list-based custom rule that either allows all or blocks all requests from a client IP address.

Rate limits can be combined with more match conditions, such as HTTP or HTTPS parameter matches, for granular rate control.

### Azure-managed rule sets

Azure-managed rule sets provide a way to deploy protection against a common set of security threats. Because Azure manages these rule sets, the rules are updated as needed to protect against new attack signatures. The Azure-managed Default Rule Set includes rules against the following threat categories:

- Cross-site scripting

- Java attacks

- Local file inclusion

- PHP injection attacks

- Remote command execution

- Remote file inclusion

- Session fixation

- SQL injection protection

- Protocol attackers

The version number of the Default Rule Set increments when new attack signatures are added to the rule set.

The Default Rule Set is enabled by default in *detection* mode in your WAF policies. You can disable or enable individual rules within the Default Rule Set to meet your application requirements. You can also set specific actions (`ALLOW`, `BLOCK`, `LOG`, and `REDIRECT`) per rule. The default action for the managed Default Rule Set is `BLOCK`.

Custom rules are always applied before the WAF evaluates the rules in the Default Rule Set. If a request matches a custom rule, the WAF applies the corresponding rule action. The request is either blocked or passed through to the back end. No other custom rules or rules in the Default Rule Set are processed. You can also remove the Default Rule Set from your WAF policies.

## WAF modes

You can configure a WAF policy to run in the following two modes:

- **Detection mode**: The WAF doesn't take any other actions other than monitoring and logging the request and its matched WAF rule to WAF logs. You can turn on logging diagnostics for Azure Content Delivery Network. When you use the Azure portal, go to the **Diagnostics** section.

- **Prevention mode**: The WAF takes the specified action if a request matches a rule. If it finds a match, it doesn't evaluate any further rules that have a lower priority. Any matched requests are also logged in the WAF logs.

## WAF actions

You can choose one of the following actions when a request matches a rule's conditions:

- `ALLOW`: The request passes through the WAF and is forwarded to the back end. No further lower-priority rules can block this request.

- `BLOCK`: The request is blocked. The WAF sends a response to the client without forwarding the request to the back end.

- `LOG`: The request is logged in the WAF logs. The WAF continues to evaluate lower-priority rules.

- `REDIRECT`: The WAF redirects the request to the specified URI. The specified URI is a policy-level setting. After you configure the setting, all requests that match the `REDIRECT` action are sent to that URI.

## Configuration

You can configure and deploy all WAF rule types by using the Azure portal, REST APIs, Azure Resource Manager templates, and Azure PowerShell.

## Monitoring

Monitoring for Azure Web Application Firewall on Azure Content Delivery Network is integrated with Azure Monitor to help you track alerts and monitor traffic trends.

## Related content

- [Command reference for managing WAF policies](/cli/azure/network/front-door/waf-policy)


# Application Gateway Web Application Firewall Portal

# Tutorial: Create an application gateway with a Web Application Firewall using the Azure portal

**Applies to:** :heavy_check_mark: Application Gateway V2

This tutorial shows you how to use the Azure portal to create an Application Gateway with a Web Application Firewall (WAF). The WAF uses [OWASP](https://owasp.org/www-project-modsecurity-core-rule-set/) rules to protect your application. These rules include protection against attacks such as SQL injection, cross-site scripting attacks, and session hijacks. After creating the application gateway, you test it to make sure it's working correctly. With Azure Application Gateway, you direct your application web traffic to specific resources by assigning listeners to ports, creating rules, and adding resources to a backend pool. For the sake of simplicity, this tutorial uses a simple setup with a public front-end IP, a basic listener to host a single site on this application gateway, two Linux virtual machines used for the backend pool, and a basic request routing rule.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create an application gateway with WAF enabled

> * Create the virtual machines used as backend servers

> * Create a storage account and configure diagnostics

> * Test the application gateway

[!INCLUDE [updated-for-az](~/reusable-content/ce-skilling/azure/includes/updated-for-az.md)]

## Prerequisites

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Sign in to Azure

Sign in to the [Azure portal](https://portal.azure.com).

## Create an application gateway

1. Select **Create a resource** on the left menu of the Azure portal. The **Create a resource** window appears.

2. Select **Networking** and then select **Application Gateway** in the **Popular Azure services** list.

### Basics tab

1. On the **Basics** tab, enter these values for the following application gateway settings:

- **Resource group**: Select **myResourceGroupAG** for the resource group. If it doesn't exist, select **Create new** to create it.

- **Application gateway name**: Enter *myAppGateway* for the name of the application gateway.

- **Tier**: select **WAF V2**.

- **WAF Policy**: Select **Create new**, type a name for the new policy, and then select **OK**.

This creates a basic WAF policy with a managed Core Rule Set (CRS).

2.  For Azure to communicate between the resources that you create, it needs a virtual network. You can either create a new virtual network or use an existing one. In this example, you create a new virtual network at the same time that you create the application gateway. Application Gateway instances are created in separate subnets. You create two subnets in this example: one for the application gateway, and then later add another for the backend servers.

Under **Configure virtual network**,  select **Create new** to create a new virtual network. In the **Create virtual network** window that opens, enter the following values to create the virtual network and a subnet:

- **Name**: Enter *myVNet* for the name of the virtual network.

- **Address space** : Accept the **10.0.0.0/16** address range.

- **Subnet name** (Application Gateway subnet): The **Subnets** area shows a subnet named *Default*. Change the name of this subnet to *myAGSubnet*, and leave the default IPv4 Address range of **10.0.0.0/24**.<br>The application gateway subnet can contain only application gateways. No other resources are allowed.

Select **OK** to close the **Create virtual network** window and save the virtual network settings.

3. On the **Basics** tab, accept the default values for the other settings and then select **Next: Frontends**.

### Frontends tab

1. On the **Frontends** tab, verify **Frontend IP address type** is set to **Public**. <br>You can configure the Frontend IP to be **Public** or **Both** as per your use case. In this example, you choose a Public Frontend IP.

> [!NOTE]

> For the Application Gateway v2 SKU, **Public** and **Both** Frontend IP address types are supported today.  **Private** frontend IP configuration only is not currently supported.

2. Choose **Add new** for the **Public IP address** and enter *myAGPublicIPAddress* for the public IP address name, and then select **OK**.

3. Select **Next: Backends**.

### Backends tab

The backend pool is used to route requests to the backend servers that serve the request. Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multitenant back-ends like Azure App Service. In this example, you create an empty backend pool with your application gateway and then later add backend targets to the backend pool.

1. On the **Backends** tab, select **Add a backend pool**.

2. In the **Add a backend pool** window that opens, enter the following values to create an empty backend pool:

- **Name**: Enter *myBackendPool* for the name of the backend pool.

- **Add backend pool without targets**: Select **Yes** to create a backend pool with no targets. You'll add backend targets after creating the application gateway.

3. In the **Add a backend pool** window, select **Add** to save the backend pool configuration and return to the **Backends** tab.

4. On the **Backends** tab, select **Next: Configuration**.

### Configuration tab

On the **Configuration** tab, you connect the frontend and backend pool you created using a routing rule.

1. Select **Add a routing rule** in the **Routing rules** column.

2. In the **Add a routing rule** window that opens, enter *myRoutingRule* for the **Rule name**.

1. For **Priority**, type a priority number.

3. A routing rule requires a listener. On the **Listener** tab within the **Add a routing rule** window, enter the following values for the listener:

- **Listener name**: Enter *myListener* for the name of the listener.

- **Frontend IP Protocol**: Select **Public IPv4** to choose the public IP you created for the frontend.

Accept the default values for the other settings on the **Listener** tab, then select the **Backend targets** tab to configure the rest of the routing rule.

4. On the **Backend targets** tab, select **myBackendPool** for the **Backend target**.

5. For the **Backend settings**, select **Add new** to create a new Backend setting. This setting determines the behavior of the routing rule. In the **Add Backend setting** window that opens, enter *myBackendSetting* for the **Backend settings name**. Accept the default values for the other settings in the window, then select **Add** to return to the **Add a routing rule** window.

6. On the **Add a routing rule** window, select **Add** to save the routing rule and return to the **Configuration** tab.

7. Select **Next: Tags** and then **Next: Review + create**.

### Review + create tab

Review the settings on the **Review + create** tab, and then select **Create** to create the virtual network, the public IP address, and the application gateway. It might take several minutes for Azure to create the application gateway.

Wait until the deployment finishes successfully before moving on to the next section.

## Add the backend server subnet

1. Open the myVNet virtual network.

1. Under **Settings**, select **Subnets**.

1. Select **+ Subnet**.

1. For **Name**, type **myBackendSubnet**.

1. For **Starting address**, type **10.0.1.0**.

1. Select **Add** to add the subnet.

## Add backend targets

In this example, you use virtual machines as the target backend. You can either use existing virtual machines or create new ones. You create two virtual machines that Azure uses as backend servers for the application gateway.

To do this, you'll:

1. Create two new Linux VMs, *myVM* and *myVM2*, to be used as backend servers.

2. Install NGINX on the virtual machines to verify that the application gateway was created successfully.

3. Add the backend servers to the backend pool.

### Create a virtual machine

1. On the Azure portal, select **Create a resource**. The **Create a resource** window appears.

2. Under **Virtual machine**, select **Create**.

3. Enter these values in the **Basics** tab for the following virtual machine settings:

- **Resource group**: Select **myResourceGroupAG** for the resource group name.

- **Virtual machine name**: Enter *myVM* for the name of the virtual machine.

- **Image**: Ubuntu Server 20.04 LTS - Gen2.

- **Authentication type**: Password

- **Username**: Enter a name for the administrator username.

- **Password**: Enter a password for the administrator password.

- **Public inbound ports**: Select **None**.

4. Accept the other defaults and then select **Next: Disks**.

5. Accept the **Disks** tab defaults and then select **Next: Networking**.

6. On the **Networking** tab, verify that **myVNet** is selected for the **Virtual network** and the **Subnet** is set to **myBackendSubnet**.

1. For **Public IP**, select **None**.

1. Accept the other defaults and then select **Next: Management**.

1. Select **Next: Monitoring**, set **Boot diagnostics** to **Disable**. Accept the other defaults and then select **Review + create**.

1. On the **Review + create** tab, review the settings, correct any validation errors, and then select **Create**.

1. Wait for the virtual machine creation to complete before continuing.

### Install NGINX for testing

In this example, you install NGINX on the virtual machines only to verify Azure created the application gateway successfully.

1. Open a Bash Cloud Shell. To do so, select the **Cloud Shell** icon from the top navigation bar of the Azure portal and then select **Bash** from the drop-down list.

1. Ensure your bash session is set for your subscription:

`az account set --subscription "<your subscription name>"`

2. Run the following command to install NGINX on the virtual machine:

```azurecli-interactive

az vm extension set \

--publisher Microsoft.Azure.Extensions \

--version 2.0 \

--name CustomScript \

--resource-group myResourceGroupAG \

--vm-name myVM \

--settings '{ "fileUris": ["https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/install_nginx.sh"], "commandToExecute": "./install_nginx.sh" }'

```

3. Create a second virtual machine and install NGINX using these steps that you previously completed. Use *myVM2* for the virtual machine name and for the `--vm-name` setting of the cmdlet.

### Add backend servers to backend pool

1. Select **All resources**, and then select **myAppGateway**.

2. Select **Backend pools** from the left menu.

3. Select **myBackendPool**.

4. Under **Target type**, select **Virtual machine** from the drop-down list.

5. Under **Target**, select the associated network interface for **myVM** from the drop-down list.

6. Repeat for **myVM2**.

7. Select **Save**.

8. Wait for the deployment to complete before proceeding to the next step.

## Test the application gateway

Although NGINX isn't required to create the application gateway, you installed it to verify whether Azure successfully created the application gateway. Use the web service to test the application gateway:

1. Find the public IP address for the application gateway on its **Overview** page.

Or, you can select **All resources**, enter *myAGPublicIPAddress* in the search box, and then select it in the search results. Azure displays the public IP address on the **Overview** page.

1. Copy the public IP address, and then paste it into the address bar of your browser.

1. Check the response. A valid response verifies that the application gateway was successfully created and it can successfully connect with the backend.

## Clean up resources

When you no longer need the resources that you created with the application gateway, remove the resource group. By removing the resource group, you also remove the application gateway and all its related resources.

To remove the resource group:

1. On the left menu of the Azure portal, select **Resource groups**.

2. On the **Resource groups** page, search for **myResourceGroupAG** in the list, then select it.

3. On the **Resource group page**, select **Delete resource group**.

4. Enter *myResourceGroupAG* for **TYPE THE RESOURCE GROUP NAME** and then select **Delete**.

## Next step

> [!div class="nextstepaction"]

> [Learn more about Web Application Firewall](../overview.md)


# Waf Front Door Create Portal

# Tutorial: Create a WAF policy on Azure Front Door by using the Azure portal

**Applies to:** :heavy_check_mark: Front Door Standard/Premium :heavy_check_mark: Front Door (classic)

This tutorial shows you how to create a basic web application firewall (WAF) policy and apply it to a front-end host at Azure Front Door.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a WAF policy.

> * Associate it with a front-end host.

> * Configure WAF rules.

## Prerequisites

Create an Azure [Front Door](../../frontdoor/quickstart-create-front-door.md) instance or an [Azure Front Door Standard or Premium](../../frontdoor/standard-premium/create-front-door-portal.md) profile.

## Create a WAF policy

First, create a basic WAF policy by using the Azure portal.

1. In the upper-left corner of the screen, select **Create a resource**. Search for **WAF**, select **Web Application Firewall (WAF)**, and select **Create**.

1. On the **Basics** tab of the **Create a WAF policy** page, enter or select the following information and accept the defaults for the remaining settings.

| Setting                 | Value                                              |

| ---                     | ---                                                |

| Policy for              | Select **Global WAF (Front Door)**. |

| Front door tier         | Select between **Classic**, **Standard**, and **Premium** tiers. |

| Subscription            | Select your Azure subscription.|

| Resource group          | Select your Azure Front Door resource group name.|

| Policy name             | Enter a unique name for your WAF policy.|

| Policy state            | Set as **Enabled**. |

1. On the **Association** tab, select **Associate a Front door profile**, enter the following settings, and select **Add**.

| Setting                 | Value                                              |

| ---                     | ---                                                |

| Front door profile              | Select your Azure Front Door profile name. |

| Domains          | Select the domains you want to associate the WAF policy to and then select **Add**. |

> [!NOTE]

> If you associate the domain to a WAF policy, it's shown as grayed out. You must first remove the domain from the associated policy and then re-associate the domain to a new WAF policy.

1. Select **Review + create** > **Create**.

## Configure WAF rules (optional)

Follow these steps to configure WAF rules.

### Change mode

When you create a WAF policy, the default mode is **Detection**. In **Detection** mode, the WAF doesn't block any requests. Instead, it logs requests that match the WAF rules.

To see the WAF in action, change the mode settings from **Detection** to **Prevention**. In **Prevention** mode, the WAF blocks and logs requests that match defined rules.

### Custom rules

To create a custom rule, under the **Custom rules** section, select **Add custom rule** to open the custom rule configuration page.

The following example shows how to configure a custom rule to block a request if the query string contains **blockme**.

### Default Rule Set

The Azure-managed Default Rule Set is enabled by default for the Premium and Classic tiers of Azure Front Door. The current DRS for the Premium tier of Azure Front Door is Microsoft_DefaultRuleSet_2.1. Microsoft_DefaultRuleSet_1.1 is the current DRS for the Classic tier of Azure Front Door. On the **Managed rules** page, select **Assign** to assign a different DRS.

To disable an individual rule, select the checkbox in front of the rule number and select **Disable** at the top of the page. To change action types for individual rules within the rule set, select the checkbox in front of the rule number and select **Change action** at the top of the page.

> [!NOTE]

> Managed rules are only supported in the Azure Front Door Premium tier and Azure Front Door Classic tier policies.

## Clean up resources

When you no longer need the resources, delete the resource group and all related resources.

## Next step

> [!div class="nextstepaction"]

> [Learn more about Azure Front Door tiers](../../frontdoor/standard-premium/tier-comparison.md)


# Application Gateway Customize Waf Rules Portal

# Customize Web Application Firewall rules using the Azure portal

**Applies to:** :heavy_check_mark: Application Gateway V2

The Azure Application Gateway Web Application Firewall (WAF) provides protection for web applications. These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS). Some rules can cause false positives and block real traffic. For this reason, Application Gateway provides the capability to customize rule groups and rules. For more information on the specific rule groups and rules, see [List of Web Application Firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).

>[!NOTE]

> If your application gateway is not using the WAF tier, the option to upgrade the application gateway to the WAF tier appears in the right pane.

## View rule groups and rules

**To view rule groups and rules**

1. Browse to the application gateway, and then select **Web application firewall**.

2. Select your **WAF Policy**.

2. Select **Managed Rules**.

This view shows a table on the page of all the rule groups provided with the chosen rule set. All of the rule's check boxes are selected.

## Disable rule groups and rules

> [!IMPORTANT]

> Use caution when disabling any rule groups or rules. This may expose you to increased security risks. The [anomaly score](ag-overview.md#anomaly-scoring-mode) is not incremented and no logging happens for disabled rules.

**To disable rule groups or specific rules**

1. Search for the rules or rule groups that you want to disable.

2. Select the check boxes for the rules that you want to disable.

3. Select the action at the top of the page (enable/disable) for the selected rules.

2. Select **Save**.

## Mandatory rules

The following list contains conditions that cause the WAF to block the request while in Prevention Mode. In Detection Mode, they're logged as exceptions.

These can't be configured or disabled:

* Failure to parse the request body results in the request being blocked, unless body inspection is turned off (XML, JSON, form data)

* Request body (with no files) data length is larger than the configured limit

* Request body (including files) is larger than the limit

* An internal error happened in the WAF engine

CRS 3.x specific:

* Inbound anomaly score exceeded threshold

## Next steps

After you configure your disabled rules, you can learn how to view your WAF logs. For more information, see [Application Gateway diagnostics](../../application-gateway/application-gateway-diagnostics.md#diagnostic-logging).


# Application Gateway Crs Rulegroups Rules

# Web Application Firewall DRS and CRS rule groups and rules

**Applies to:** :heavy_check_mark: Application Gateway

The Azure-managed Default Rule Set (DRS) in the Application Gateway web application firewall (WAF) actively protect web applications from common vulnerabilities and exploits. These rule sets, managed by Azure, receive updates as necessary to guard against new attack signatures. The default rule set also incorporates the Microsoft Threat Intelligence Collection rules. The Microsoft Intelligence team collaborates in writing these rules, ensuring enhanced coverage, specific vulnerability patches, and improved false positive reduction.

You can disable rules individually, or set specific actions for each rule. This article lists the current rules and rule sets available. If a published rule set requires an update, we'll document it here.

> [!NOTE]

> When you change a ruleset version in a WAF Policy, you should forward your existing rule action and state overrides and exclusions to apply on the new ruleset version. For more information, see [Upgrading or changing ruleset version](upgrade-ruleset-version.md).

## Default rule set 2.2

Default rule set (DRS) 2.2 is based on Open Web Application Security Project (OWASP) Core Rule Set 3.3.4, bringing refinements to existing detections and new protections, including rules that detect content types declared outside the actual content-type header and enhanced remote code execution (RCE) detections. DRS 2.2 includes additional proprietary protections rules developed by Microsoft Threat Intelligence team, which expand coverage across SQL injection, XSS, and application-security attack patterns.

DRS 2.2 offers a new engine and new rule sets defending against Java injections, an initial set of file upload checks, and fewer false positives compared with older DRS and CRS versions. You can also [customize rules to suit your needs](application-gateway-customize-waf-rules-portal.md). Learn more about the new [Azure WAF engine](waf-engine.md).

DRS 2.2 includes 18 rule groups, as shown in the following table. Each group contains multiple rules, and you can customize behavior for individual rules, rule groups, or entire rule set.

|Threat Type|Rule Group Name|

|---|---|

|General|**[General](?tabs=drs22#general-22)**|

|Lock-down methods (PUT, PATCH)|**[METHOD-ENFORCEMENT](?tabs=drs22#drs911-22)**|

|Protocol and encoding issues|**[PROTOCOL-ENFORCEMENT](?tabs=drs22#drs920-22)**|

|Header injection, request smuggling, and response splitting|**[PROTOCOL-ATTACK](?tabs=drs22#drs921-22)**|

|File and path attacks|**[LFI](?tabs=drs22#drs930-22)**|

|Remote file inclusion (RFI) attacks|**[RFI](?tabs=drs22#drs931-22)**|

|Remote code execution attacks|**[RCE](?tabs=drs22#drs932-22)**|

|PHP-injection attacks|**[PHP](?tabs=drs22#drs933-22)**|

|Node JS attacks|**[NodeJS](?tabs=drs22#drs934-22)**|

|Cross-site scripting attacks|**[XSS](?tabs=drs22#drs941-22)**|

|SQL-injection attacks|**[SQLI](?tabs=drs22#drs942-22)**|

|Session-fixation attacks|**[SESSION-FIXATION](?tabs=drs22#drs943-22)**|

|JAVA attacks|**[SESSION-JAVA](?tabs=drs22#drs944-22)**|

|Web shell attacks (MS)|**[MS-ThreatIntel-WebShells](?tabs=drs22#drs9905-22)**|

|AppSec attacks (MS)|**[MS-ThreatIntel-AppSec](?tabs=drs22#drs9903-22)**|

|SQL-injection attacks (MS)|**[MS-ThreatIntel-SQLI](?tabs=drs22#drs99031-22)**|

|CVE attacks (MS)|**[MS-ThreatIntel-CVEs](?tabs=drs22#drs99001-22)**|

|XSS attacks (MS)|**[MS-ThreatIntel-XSS](?tabs=drs22#drs99032-22)**|

#### Disabled rules

DRS 2.2 rules configured in Paranoia Level 2 are disabled by default. You can leave their state as disabled if you wish to keep you WAF policy configured in Paranoia Level 1. If you wish to increase the policy's paranoia level, you can safely change these rules' state to enabled and their action to log mode. Analyze the logs, make the required fine tuning and enable the rules accordingly. For more information, see [Paranoia level](?tabs=drs22%2Cowasp32#paranoia-level) and [Tuning of managed rule sets](?tabs=drs22%2Cowasp32#tuning-of-managed-rule-sets).

Some OWASP rules are superseded by Microsoft-authored replacements. The original rules are disabled by default and their descriptions end with “(replaced by …)”.

## Default rule set 2.1

While you can still use default rule set (DRS) 2.1, it's recommended to use the latest version of DRS 2.2.

Default rule set (DRS) 2.1 is baselined off the Open Web Application Security Project (OWASP) Core Rule Set (CRS) 3.3.2 and includes additional proprietary protections rules developed by Microsoft Threat Intelligence team and updates to signatures to reduce false positives. It also supports transformations beyond just URL decoding.

DRS 2.1 offers a new engine and new rule sets defending against Java injections, an initial set of file upload checks, and fewer false positives compared with CRS versions. You can also [customize rules to suit your needs](application-gateway-customize-waf-rules-portal.md). Learn more about the new [Azure WAF engine](waf-engine.md).

DRS 2.1 includes 17 rule groups, as shown in the following table. Each group contains multiple rules, and you can customize behavior for individual rules, rule groups, or entire rule set.

|Threat Type|Rule Group Name|

|---|---|

|General|**[General](?tabs=drs21#general-21)**|

|Lock-down methods (PUT, PATCH)|**[METHOD-ENFORCEMENT](?tabs=drs21#drs911-21)**|

|Protocol and encoding issues|**[PROTOCOL-ENFORCEMENT](?tabs=drs21#drs920-21)**|

|Header injection, request smuggling, and response splitting|**[PROTOCOL-ATTACK](?tabs=drs21#drs921-21)**|

|File and path attacks|**[LFI](?tabs=drs21#drs930-21)**|

|Remote file inclusion (RFI) attacks|**[RFI](?tabs=drs21#drs931-21)**|

|Remote code execution attacks|**[RCE](?tabs=drs21#drs932-21)**|

|PHP-injection attacks|**[PHP](?tabs=drs21#drs933-21)**|

|Node JS attacks|**[NodeJS](?tabs=drs21#drs934-21)**|

|Cross-site scripting attacks|**[XSS](?tabs=drs21#drs941-21)**|

|SQL-injection attacks|**[SQLI](?tabs=drs21#drs942-21)**|

|Session-fixation attacks|**[SESSION-FIXATION](?tabs=drs21#drs943-21)**|

|JAVA attacks|**[SESSION-JAVA](?tabs=drs21#drs944-21)**|

|Web shell attacks (MS)|**[MS-ThreatIntel-WebShells](?tabs=drs21#drs9905-21)**|

|AppSec attacks (MS)|**[MS-ThreatIntel-AppSec](?tabs=drs21#drs9903-21)**|

|SQL-injection attacks (MS)|**[MS-ThreatIntel-SQLI](?tabs=drs21#drs99031-21)**|

|CVE attacks (MS)|**[MS-ThreatIntel-CVEs](?tabs=drs21#drs99001-21)**|

## Fine-tuning guidance for DRS 2.1

Use the following guidance to tune WAF while you get started with DRS 2.1 on Application Gateway WAF:

|Rule ID|Rule Group|Description|Recommendation|

|---------|---------|---------|---------|

|942110|SQLI|SQL Injection Attack: Common Injection Testing Detected|Disable rule 942110, replaced by MSTIC rule 99031001|

|942150|SQLI|SQL Injection Attack|Disable rule 942150, replaced by MSTIC rule 99031003|

|942260|SQLI|Detects basic SQL authentication bypass attempts 2/3|Disable rule 942260, replaced by MSTIC rule 99031004|

|942430|SQLI|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12)|Disable rule 942430, it triggers too many false positives|

|942440|SQLI|SQL Comment Sequence Detected|Disable rule 942440, replaced by MSTIC rule 99031002|

|99005006|MS-ThreatIntel-WebShells|Spring4Shell Interaction Attempt|Keep the rule enabled to prevent against SpringShell vulnerability|

|99001014|MS-ThreatIntel-CVEs|Attempted Spring Cloud routing-expression injection [CVE-2022-22963](https://www.cve.org/CVERecord?id=CVE-2022-22963)|Keep the rule enabled to prevent against SpringShell vulnerability|

|99001015|MS-ThreatIntel-CVEs|Attempted Spring Framework unsafe class object exploitation [CVE-2022-22965](https://www.cve.org/CVERecord?id=CVE-2022-22965)|Keep the rule enabled to prevent against SpringShell vulnerability|

|99001016|MS-ThreatIntel-CVEs|Attempted Spring Cloud Gateway Actuator injection [CVE-2022-22947](https://www.cve.org/CVERecord?id=CVE-2022-22947)|Keep the rule enabled to prevent against SpringShell vulnerability|

|99001017|MS-ThreatIntel-CVEs|Attempted Apache Struts file upload exploitation [CVE-2023-50164](https://www.cve.org/CVERecord?id=CVE-2023-50164)|Set action to Block to prevent against Apache Struts vulnerability. Anomaly Score not supported for this rule|

## Tuning of Managed rule sets

Both DRS and CRS are enabled by default in Detection mode in your WAF policies. You can disable or enable individual rules within the Managed Rule Set to meet your application requirements. You can also set specific actions per rule. The DRS/CRS supports block, log, and anomaly score actions. The Bot Manager ruleset supports the allow, block, and log actions.

Sometimes you might need to omit certain request attributes from a WAF evaluation. A common example is Active Directory-inserted tokens that are used for authentication. You can configure exclusions to apply when specific WAF rules are evaluated, or to apply globally to the evaluation of all WAF rules. Exclusion rules apply to your whole web application. For more information, see [Web Application Firewall (WAF) with Application Gateway exclusion lists](application-gateway-waf-configuration.md).

By default, Azure WAF uses anomaly scoring when a request matches a rule. Additionally, you can configure custom rules in the same WAF policy if you want to bypass any of the preconfigured rules in the Core Rule Set.

Custom rules are always applied before rules in the Core Rule Set are evaluated. If a request matches a custom rule, the corresponding rule action is applied. The request is either blocked or passed through to the back-end. No other custom rules or the rules in the Core Rule Set are processed.

### Anomaly scoring

When you use CRS or DRS 2.1 and later, your WAF is configured to use anomaly scoring by default. Traffic that matches any rule isn't immediately blocked, even when your WAF is in prevention mode. Instead, the OWASP rule sets define a severity for each rule: Critical, Error, Warning, or Notice. The severity affects a numeric value for the request, which is called the anomaly score:

| Rule severity | Value contributed to anomaly score |

| - | - |

| Critical | 5 |

| Error | 4 |

| Warning | 3 |

| Notice | 2 |

If the anomaly score is 5 or greater, and the WAF is in Prevention mode, the request is blocked. If the anomaly score is 5 or greater, and the WAF is in Detection mode, the request is logged but not blocked.

For example, a single *Critical* rule match is enough for the WAF to block a request when in Prevention mode, because the overall anomaly score is 5. However, one *Warning* rule match only increases the anomaly score by 3, which isn't enough by itself to block the traffic. When an anomaly rule is triggered, it shows a "Matched" action in the logs. If the anomaly score is 5 or greater, there's a separate rule triggered with either "Blocked" or "Detected" action depending on whether WAF policy is in Prevention or Detection mode. For more information, see [Anomaly Scoring mode](ag-overview.md#anomaly-scoring-mode).

## Paranoia level

Each rule is assigned in a specific Paranoia Level (PL). Rules configured in Paranoia Level 1 (PL1) are less aggressive and hardly ever trigger a false positive. They provide baseline security with minimal need for fine tuning. Rules in PL2 detect more attacks, but they're expected to trigger false positives that should be fine-tuned.

By default, DRS 2.2 is configured at Paranoia Level 1 (PL1), and all PL2 rules are disabled. To run WAF at PL2, you can manually enable any or all PL2 rules.

For earlier rule sets, DRS 2.1 and CRS 3.2 include rules defined for Paranoia Level 2, which covers both PL1 and PL2 rules. If you prefer to operate strictly at PL1, you can disable specific PL2 rules or set their action to Log.

Paranoia Levels 3 and 4 aren't currently supported in Azure WAF.

> [!NOTE]

> CRS 3.2 ruleset includes rules in PL3 and PL4, but these rules are always inactive and can't be enabled, regardless of their configured state or action.

## Upgrading or changing ruleset version

If you're upgrading, or assigning a new ruleset version, and would like to preserve existing rule overrides and exclusions, it's recommended to use PowerShell, CLI, REST API, or a template to make ruleset version changes. A new version of a ruleset can have newer rules or additional rule groups, which you might want to validate safely. It's recommended to validate changes in a test environment, fine tune if necessary, and then deploy in a production environment.

For more information, see [Upgrade CRS or DRS ruleset version](upgrade-ruleset-version.md)

If you're using the Azure portal to assign a new managed ruleset to a WAF policy, all the previous customizations from the existing managed ruleset such as rule state, rule actions, and rule level exclusions will be reset to the new managed ruleset's defaults. However, any custom rules, policy settings, and global exclusions will remain unaffected during the new ruleset assignment. You'll need to redefine rule overrides and validate changes before deploying in a production environment.

## Understanding CVE protection in Azure WAF

Azure Application Gateway WAF protects against CVEs through:

- **Generic protections (DRS / OWASP CRS)**: Many CVEs are already mitigated by existing rules that detect common attack patterns such as SQL injection, XSS, and RCE.

- **CVE-specific protections (Microsoft Threat Intelligence)**: For high-impact vulnerabilities, dedicated rules are released in the [MS-ThreatIntel-CVEs](?tabs=drs22#drs99001-22) rule group.

Always use the latest Default Rule Set (DRS) for the most up-to-date protection and reduced false positives.

To check coverage:

- Review the [MS-ThreatIntel-CVEs](?tabs=drs22#drs99001-22) rule group

- Check rule descriptions for CVE references

- Keep in mind that many CVEs are covered by generic protections even if not explicitly listed

If a CVE isn’t explicitly covered:

- Upgrade to the latest DRS

- Validate against existing rules or use custom rules if needed

- Contact Azure support if you require protection for a specific high-priority CVE not currently covered

## Core rule sets (CRS) - legacy

The recommended managed rule set is the latest Default Rule Set 2.2, which is baselined off the Open Web Application Security Project (OWASP) Core Rule Set (CRS) 3.3.4 and includes additional proprietary protections rules developed by Microsoft Threat Intelligence team and updates to signatures to reduce false positives. When creating a new WAF policy you should use the latest, recommended ruleset version DRS 2.2. If you have an existing WAF policy using DRS 2.1, CRS 3.2 or CRS 3.1, it's recommended to upgrade to DRS 2.2. For more information, see [Upgrade CRS or DRS ruleset version](upgrade-ruleset-version.md).

> [!NOTE]

> - CRS 3.2 is only available on the WAF_v2 SKU. You can't downgrade from CRS 3.2 to CRS 3.1 or earlier because CRS 3.2 runs on the new Azure WAF engine. It's recommended to upgrade to the latest DRS 2.1 directly and validate new rules safely by changing the new rules' action to log mode. For more information, see [Validate new rules safely](upgrade-ruleset-version.md#validate-new-rules-safely).

>

> - Web Application Firewall (WAF) running on Application Gateway for Containers doesn't support the Core Ruleset (CRS).

### Bot Manager 1.0

The Bot Manager 1.0 rule set provides protection against malicious bots and detection of good bots. The rules provide granular control over bots detected by WAF by categorizing bot traffic as Good, Bad, or Unknown bots.

|Rule group|Description|

|---|---|

|**[BadBots](?tabs=bot#bot100)**|Protect against bad bots|

|**[GoodBots](?tabs=bot#bot200)**|Identify good bots|

|**[UnknownBots](?tabs=bot#bot300)**|Identify unknown bots|

### Bot Manager 1.1

The Bot Manager 1.1 rule set is an enhancement to Bot Manager 1.0 rule set. It provides enhanced protection against malicious bots, and increases good bot detection.

|Rule group|Description|

|---|---|

|**[BadBots](?tabs=bot11#bot11-100)**|Protect against bad bots|

|**[GoodBots](?tabs=bot11#bot11-200)**|Identify good bots|

|**[UnknownBots](?tabs=bot11#bot11-300)**|Identify unknown bots|

The following rule groups and rules are available when using Web Application Firewall on Application Gateway.

# [DRS 2.2](#tab/drs22)

## <a name="drs22"></a> 2.2 rule sets

### <a name="general-22"></a> General

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|200002|Critical - 5|1|Failed to parse request body.|

|200003|Critical - 5|1|Multipart request body failed strict validation|

### <a name="drs911-22"></a> Method enforcement

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|911100|Critical - 5|1|Method isn't allowed by policy|

### <a name="drs920-22"></a> Protocol enforcement

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|920100|Notice - 2|1|Invalid HTTP Request Line|

|920120|Critical - 5|1|Attempted multipart/form-data bypass|

|920121|Critical - 5|2|Attempted multipart/form-data bypass|

|920160|Critical - 5|1|Content-Length HTTP header isn't numeric.|

|920170|Critical - 5|1|GET or HEAD Request with Body Content.|

|920171|Critical - 5|1|GET or HEAD Request with Transfer-Encoding.|

|920180|Notice - 2|1|POST without Content-Length or Transfer-Encoding headers.|

|920181|Warning - 3|1|Content-Length and Transfer-Encoding headers present|

|920190|Warning - 3|1|Range: Invalid Last Byte Value.|

|920200|Warning - 3|2|Range: Too many fields (6 or more)|

|920201|Warning - 3|2|Range: Too many fields for pdf request (63 or more)|

|920210|Warning - 3|1|Multiple/Conflicting Connection Header Data Found.|

|920220|Warning - 3|1|URL Encoding Abuse Attack Attempt|

|920230|Warning - 3|2|Multiple URL Encoding Detected|

|920240|Warning - 3|1|URL Encoding Abuse Attack Attempt|

|920260|Warning - 3|1|Unicode Full/Half Width Abuse Attack Attempt|

|920270|Critical - 5|1|Invalid character in request (null character)|

|920271|Critical - 5|2|Invalid character in request (non printable characters)|

|920280|Warning - 3|1|Request Missing a Host Header|

|920290|Warning - 3|1|Empty Host Header|

|920300|Notice - 2|2|Request Missing an Accept Header|

|920310|Notice - 2|1|Request Has an Empty Accept Header|

|920311|Notice - 2|1|Request Has an Empty Accept Header|

|920320|Notice - 2|2|Missing User Agent Header|

|920330|Notice - 2|1|Empty User Agent Header|

|920340|Notice - 2|1|Request Containing Content, but Missing Content-Type header|

|920341|Critical - 5|2|Request Containing Content Requires Content-Type header|

|920350|Warning - 3|1|Host header is a numeric IP address|

|920420|Critical - 5|2|Request content type is not allowed by policy|

|920430|Critical - 5|1|HTTP protocol version is not allowed by policy|

|920440|Critical - 5|1|URL file extension is restricted by policy|

|920450|Critical - 5|1|HTTP header is restricted by policy|

|920470|Critical - 5|1|Illegal Content-Type header|

|920480|Critical - 5|1|Request content type charset is not allowed by policy|

|920500|Critical - 5|1|Attempt to access a backup or working file|

|920530|Critical - 5|1|Restrict charset parameter inside content type header to occur max once|

|920620|Critical - 5|1|Multiple Content-Type Request Headers|

### <a name="drs921-22"></a> Protocol attack

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|921110|Critical - 5|1|HTTP Request Smuggling Attack|

|921120|Critical - 5|1|HTTP Response Splitting Attack|

|921130|Critical - 5|1|HTTP Response Splitting Attack|

|921140|Critical - 5|1|HTTP Header Injection Attack via headers|

|921150|Critical - 5|1|HTTP Header Injection Attack via payload (CR/LF detected)|

|921151|Critical - 5|2|HTTP Header Injection Attack via payload (CR/LF detected)|

|921160|Critical - 5|1|HTTP Header Injection Attack via payload (CR/LF and header-name detected)|

|921190|Critical - 5|1|HTTP Splitting (CR/LF in request filename detected)|

|921200|Critical - 5|1|LDAP Injection Attack|

|921422|Critical - 5|2|Detect content types in the Content-Type header outside of the actual content type declaration|

### <a name="drs930-22"></a> LFI: Local file inclusion

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|930100|Critical - 5|1|Path Traversal Attack (/../)|

|930110|Critical - 5|1|Path Traversal Attack (/../)|

|930120|Critical - 5|1|OS File Access Attempt|

|930130|Critical - 5|1|Restricted File Access Attempt|

### <a name="drs931-22"></a> RFI: Remote file inclusion

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|931100|Critical - 5|2|Possible Remote File Inclusion (RFI) Attack: URL Parameter using IP Address|

|931110|Critical - 5|1|Possible Remote File Inclusion (RFI) Attack: Common RFI Vulnerable Parameter Name used w/URL Payload|

|931120|Critical - 5|1|Possible Remote File Inclusion (RFI) Attack: URL Payload Used w/Trailing Question Mark Character (?)|

|931130|Critical - 5|2|Possible Remote File Inclusion (RFI) Attack: Off-Domain Reference/Link|

### <a name="drs932-22"></a> RCE: Remote command execution

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|932100|Critical - 5|1|Remote Command Execution: Unix Command Injection|

|932105|Critical - 5|1|Remote Command Execution: Unix Command Injection|

|932110|Critical - 5|1|Remote Command Execution: Windows Command Injection|

|932115|Critical - 5|1|Remote Command Execution: Windows Command Injection|

|932120|Critical - 5|1|Remote Command Execution: Windows PowerShell Command Found|

|932130|Critical - 5|1|Remote Command Execution: Unix Shell Expression or Confluence Vulnerability (CVE-2022-26134) Found|

|932140|Critical - 5|1|Remote Command Execution: Windows FOR/IF Command Found|

|932150|Critical - 5|1|Remote Command Execution: Direct Unix Command Execution|

|932160|Critical - 5|1|Remote Command Execution: Unix Shell Code Found|

|932170|Critical - 5|1|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932171|Critical - 5|1|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932180|Critical - 5|1|Restricted File Upload Attempt|

### <a name="drs933-22"></a> PHP attacks

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|933100|Critical - 5|1|PHP Injection Attack: PHP Open Tag Found|

|933110|Critical - 5|1|PHP Injection Attack: PHP Script File Upload Found|

|933120|Critical - 5|1|PHP Injection Attack: Configuration Directive Found|

|933130|Critical - 5|1|PHP Injection Attack: Variables Found|

|933140|Critical - 5|1|PHP Injection Attack: I/O Stream Found|

|933150|Critical - 5|1|PHP Injection Attack: High-Risk PHP Function Name Found|

|933151|Critical - 5|2|PHP Injection Attack: Medium-Risk PHP Function Name Found|

|933160|Critical - 5|1|PHP Injection Attack: High-Risk PHP Function Call Found|

|933170|Critical - 5|1|PHP Injection Attack: Serialized Object Injection|

|933180|Critical - 5|1|PHP Injection Attack: Variable Function Call Found|

|933200|Critical - 5|1|PHP Injection Attack: Wrapper scheme detected|

|933210|Critical - 5|1|PHP Injection Attack: Variable Function Call Found|

### <a name="drs934-22"></a> Node JS attacks

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|934100|Critical - 5|1|Node.js Injection Attack|

### <a name="drs941-22"></a> XSS: Cross-site scripting

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|941100|Critical - 5|1|XSS Attack Detected via libinjection|

|941101|Critical - 5|2|XSS Attack Detected via libinjection|

|941110|Critical - 5|1|XSS Filter - Category 1: Script Tag Vector|

|941120|Critical - 5|2|XSS Filter - Category 2: Event Handler Vector|

|941130|Critical - 5|1|XSS Filter - Category 3: Attribute Vector|

|941140|Critical - 5|1|XSS Filter - Category 4: JavaScript URI Vector|

|941150|Critical - 5|2|XSS Filter - Category 5: Disallowed HTML Attributes|

|941160|Critical - 5|1|NoScript XSS InjectionChecker: HTML Injection|

|941170|Critical - 5|1|NoScript XSS InjectionChecker: Attribute Injection|

|941180|Critical - 5|1|Node-Validator Blacklist Keywords|

|941190|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941200|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941210|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941220|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941230|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941240|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941250|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941260|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941270|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941280|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941290|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941300|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941310|Critical - 5|1|US-ASCII Malformed Encoding XSS Filter - Attack Detected.|

|941320|Critical - 5|2|Possible XSS Attack Detected - HTML Tag Handler|

|941330|Critical - 5|2|IE XSS Filters - Attack Detected.|

|941340|Critical - 5|2|IE XSS Filters - Attack Detected.|

|941350|Critical - 5|1|UTF-7 Encoding IE XSS - Attack Detected.|

|941360|Critical - 5|1|JSFuck / Hieroglyphy obfuscation detected|

|941370|Critical - 5|1|JavaScript global variable found|

|941380|Critical - 5|2|AngularJS client side template injection detected|

### <a name="drs942-22"></a> SQLI: SQL injection

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|942100|Critical - 5|1|SQL Injection Attack Detected via libinjection|

|942110|Warning - 3|2|SQL Injection Attack: Common Injection Testing Detected|

|942120|Critical - 5|2|SQL Injection Attack: SQL Operator Detected|

|942140|Critical - 5|1|SQL Injection Attack: Common DB Names Detected|

|942150|Critical - 5|2|SQL Injection Attack (replaced by rule #99031003)|

|942160|Critical - 5|1|Detects blind sqli tests using sleep() or benchmark().|

|942170|Critical - 5|1|Detects SQL benchmark and sleep injection attempts including conditional queries|

|942180|Critical - 5|2|Detects basic SQL authentication bypass attempts 1/3|

|942190|Critical - 5|1|Detects MSSQL code execution and information gathering attempts|

|942200|Critical - 5|2|Detects MySQL comment-/space-obfuscated injections and backtick termination|

|942210|Critical - 5|2|Detects chained SQL injection attempts 1/2|

|942220|Critical - 5|1|Looking for integer overflow attacks, these are taken from skipfish, except 3.0.00738585072007e-308 is the "magic number" crash|

|942230|Critical - 5|1|Detects conditional SQL injection attempts|

|942240|Critical - 5|1|Detects MySQL charset switch and MSSQL DoS attempts|

|942250|Critical - 5|1|Detects MATCH AGAINST, MERGE and EXECUTE IMMEDIATE injections|

|942260|Critical - 5|2|Detects basic SQL authentication bypass attempts 2/3 (replaced by rule #99031004)|

|942270|Critical - 5|1|Looking for basic SQL injection. Common attack string for MySQL, Oracle, and others.|

|942280|Critical - 5|1|Detects Postgres pg_sleep injection, waitfor delay attacks and database shutdown attempts|

|942290|Critical - 5|1|Finds basic MongoDB SQL injection attempts|

|942300|Critical - 5|2|Detects MySQL comments, conditions and ch(a)r injections|

|942310|Critical - 5|2|Detects chained SQL injection attempts 2/2|

|942320|Critical - 5|1|Detects MySQL and PostgreSQL stored procedure/function injections|

|942330|Critical - 5|2|Detects classic SQL injection probings 1/3|

|942340|Critical - 5|2|Detects basic SQL authentication bypass attempts 3/3 (replaced by rule #99031006)|

|942350|Critical - 5|1|Detects MySQL UDF injection and other data/structure manipulation attempts|

|942360|Critical - 5|1|Detects concatenated basic SQL injection and SQLLFI attempts|

|942361|Critical - 5|2|Detects basic SQL injection based on keyword alter or union|

|942370|Critical - 5|2|Detects classic SQL injection probings 2/3|

|942380|Critical - 5|2|SQL Injection Attack|

|942390|Critical - 5|2|SQL Injection Attack|

|942400|Critical - 5|2|SQL Injection Attack|

|942410|Critical - 5|2|SQL Injection Attack|

|942430|Warning - 3|2|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12) (replaced by rule #99031005)|

|942440|Critical - 5|2|SQL Comment Sequence Detected (replaced by rule #99031002).|

|942450|Critical - 5|2|SQL Hex Encoding Identified|

|942470|Critical - 5|2|SQL Injection Attack|

|942480|Critical - 5|2|SQL Injection Attack|

|942500|Critical - 5|1|MySQL in-line comment detected.|

|942510|Critical - 5|2|SQLi bypass attempt by ticks or backticks detected.|

### <a name="drs943-22"></a> Session fixation

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|943100|Critical - 5|1|Possible Session Fixation Attack: Setting Cookie Values in HTML|

|943110|Critical - 5|1|Possible Session Fixation Attack: SessionID Parameter Name with Off-Domain Referer|

|943120|Critical - 5|1|Possible Session Fixation Attack: SessionID Parameter Name with No Referer|

### <a name="drs944-22"></a> Java attacks

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|944100|Critical - 5|1|Remote Command Execution: Suspicious Java class detected|

|944110|Critical - 5|1|Remote Command Execution: Java process spawn (CVE-2017-9805)|

|944120|Critical - 5|1|Remote Command Execution: Java serialization (CVE-2015-5842)|

|944130|Critical - 5|1|Suspicious Java class detected|

|944200|Critical - 5|2|Magic bytes Detected, probable java serialization in use|

|944210|Critical - 5|2|Magic bytes Detected Base64 Encoded, probable java serialization in use|

|944240|Critical - 5|2|Remote Command Execution: Java serialization and Log4j vulnerability (CVE-2021-44228, CVE-2021-45046)|

|944250|Critical - 5|2|Remote Command Execution: Suspicious Java method detected|

### <a name="drs9905-22"></a> MS-ThreatIntel-WebShells

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99005002|Critical - 5|2|Web Shell Interaction Attempt (POST)|

|99005003|Critical - 5|2|Web Shell Upload Attempt (POST) - CHOPPER PHP|

|99005004|Critical - 5|2|Web Shell Upload Attempt (POST) - CHOPPER ASPX|

|99005005|Critical - 5|2|Web Shell Interaction Attempt|

|99005006|Critical - 5|2|Spring4Shell Interaction Attempt|

### <a name="drs9903-22"></a> MS-ThreatIntel-AppSec

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99030001|Critical - 5|2|Path Traversal Evasion in Headers (/.././../)|

|99030002|Critical - 5|2|Path Traversal Evasion in Request Body (/.././../)|

|99030003|Critical - 5|2|URL encoded file path|

|99030004|Critical - 5|2|Missing brotli encoding from supporting browser with https referer|

|99030005|Critical - 5|2|Missing brotli encoding from supporting browser over HTTP/2|

|99030006|Critical - 5|2|Illegal character in requested filename|

### <a name="drs99031-22"></a> MS-ThreatIntel-SQLI

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99031001|Warning - 3|2|SQL Injection Attack: Common Injection Testing Detected (replacing rule #942110)|

|99031002|Critical - 5|2|SQL Comment Sequence Detected (replacing rule #942440).|

|99031003|Critical - 5|2|SQL Injection Attack (replacing rule #942150)|

|99031004|Critical - 5|2|Detects basic SQL authentication bypass attempts 2/3 (replacing rule #942260)|

|99031005|Warning - 3|2|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12) (replacing rule #942430)|

|99031006|Critical - 5|2|Detects basic SQL authentication bypass attempts 3/3 (replacing rule #942340)|

### <a name="drs99001-22"></a> MS-ThreatIntel-CVEs

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99001001|Critical - 5|2|Attempted F5 tmui (CVE-2020-5902) REST API exploitation with known credentials|

|99001002|Critical - 5|2|Attempted Citrix NSC_USER directory traversal [CVE-2019-19781](https://www.cve.org/CVERecord?id=CVE-2019-19781)|

|99001003|Critical - 5|2|Attempted Atlassian Confluence Widget Connector exploitation [CVE-2019-3396](https://www.cve.org/CVERecord?id=CVE-2019-3396)|

|99001004|Critical - 5|2|Attempted Pulse Secure custom template exploitation [CVE-2020-8243](https://www.cve.org/CVERecord?id=CVE-2019-8243)|

|99001005|Critical - 5|2|Attempted SharePoint type converter exploitation [CVE-2020-0932](https://www.cve.org/CVERecord?id=CVE-2019-0932)|

|99001006|Critical - 5|2|Attempted Pulse Connect directory traversal [CVE-2019-11510](https://www.cve.org/CVERecord?id=CVE-2019-11510)|

|99001007|Critical - 5|2|Attempted Junos OS J-Web local file inclusion [CVE-2020-1631](https://www.cve.org/CVERecord?id=CVE-2019-1631)|

|99001008|Critical - 5|2|Attempted Fortinet path traversal [CVE-2018-13379](https://www.cve.org/CVERecord?id=CVE-2019-13379)|

|99001009|Critical - 5|2|Attempted Apache struts ognl injection [CVE-2017-5638](https://www.cve.org/CVERecord?id=CVE-2019-5638)|

|99001010|Critical - 5|2|Attempted Apache struts ognl injection [CVE-2017-12611](https://www.cve.org/CVERecord?id=CVE-2019-12611)|

|99001011|Critical - 5|2|Attempted Oracle WebLogic path traversal [CVE-2020-14882](https://www.cve.org/CVERecord?id=CVE-2019-14882)|

|99001012|Critical - 5|2|Attempted Telerik WebUI insecure deserialization exploitation [CVE-2019-18935](https://www.cve.org/CVERecord?id=CVE-2019-18935)|

|99001013|Critical - 5|2|Attempted SharePoint insecure XML deserialization [CVE-2019-0604](https://www.cve.org/CVERecord?id=CVE-2019-0604)|

|99001014|Critical - 5|2|Attempted Spring Cloud routing-expression injection [CVE-2022-22963](https://www.cve.org/CVERecord?id=CVE-2022-22963)|

|99001015|Critical - 5|2|Attempted Spring Framework unsafe class object exploitation [CVE-2022-22965](https://www.cve.org/CVERecord?id=CVE-2022-22965)|

|99001016|Critical - 5|2|Attempted Spring Cloud Gateway Actuator injection [CVE-2022-22947](https://www.cve.org/CVERecord?id=CVE-2022-22947)|

|99001017|Critical - 5|2|Attempted Apache Struts file upload exploitation [CVE-2023-50164](https://www.cve.org/CVERecord?id=CVE-2023-50164)|

|99001018|Critical - 5|1|Attempted React2Shell remote code execution exploitation [CVE-2025-55182](https://www.cve.org/CVERecord?id=CVE-2025-55182)|

### <a name="drs99032-22"></a> MS-ThreatIntel-XSS

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99032001|Critical - 5|1|XSS Filter - Category 2: Event Handler Vector (replacing rule #941120)|

|99032002|Critical - 5|2|Possible Remote File Inclusion (RFI) Attack: Off-Domain Reference/Link (replacing rule #931130)|

# [DRS 2.1](#tab/drs21)

## <a name="drs21"></a> 2.1 rule sets

### <a name="general-21"></a> General

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|200002|Critical - 5|PL1|Failed to parse request body|

|200003|Critical - 5|PL1|Multipart request body failed strict validation|

### <a name="drs911-21"></a> METHOD ENFORCEMENT

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|911100|Critical - 5|PL1|Method isn't allowed by policy|

### <a name="drs920-21"></a> PROTOCOL-ENFORCEMENT

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|920100|Notice - 2|PL1|Invalid HTTP Request Line|

|920120|Critical - 5|PL1|Attempted multipart/form-data bypass|

|920121|Critical - 5|PL2|Attempted multipart/form-data bypass|

|920160|Critical - 5|PL1|Content-Length HTTP header isn't numeric|

|920170|Critical - 5|PL1|GET or HEAD Request with Body Content|

|920171|Critical - 5|PL1|GET or HEAD Request with Transfer-Encoding|

|920180|Notice - 2|PL1|POST request missing Content-Length Header|

|920181|Warning - 3|PL1|Content-Length and Transfer-Encoding headers present 99001003|

|920190|Warning - 3|PL1|Range: Invalid Last Byte Value|

|920200|Warning - 3|PL2|Range: Too many fields (6 or more)|

|920201|Warning - 3|PL2|Range: Too many fields for pdf request (35 or more)|

|920210|Critical - 5|PL1|Multiple/Conflicting Connection Header Data Found|

|920220|Warning - 3|PL1|URL Encoding Abuse Attack Attempt|

|920230|Warning - 3|PL2|Multiple URL Encoding Detected|

|920240|Warning - 3|PL1|URL Encoding Abuse Attack Attempt|

|920260|Warning - 3|PL1|Unicode Full/Half Width Abuse Attack Attempt|

|920270|Error - 4|PL1|Invalid character in request (null character)|

|920271|Critical - 5|PL2|Invalid character in request (non printable characters)|

|920280|Warning - 3|PL1|Request Missing a Host Header|

|920290|Warning - 3|PL1|Empty Host Header|

|920300|Notice - 2|PL2|Request Missing an Accept Header|

|920310|Notice - 2|PL1|Request Has an Empty Accept Header|

|920311|Notice - 2|PL1|Request Has an Empty Accept Header|

|920320|Notice - 2|PL2|Missing User Agent Header|

|920330|Notice - 2|PL1|Empty User Agent Header|

|920340|Notice - 2|PL1|Request Containing Content, but Missing Content-Type header|

|920341|Critical - 5|PL1|Request containing content requires Content-Type header|

|920350|Warning - 3|PL1|Host header is a numeric IP address|

|920420|Critical - 5|PL1|Request content type isn't allowed by policy|

|920430|Critical - 5|PL1|HTTP protocol version isn't allowed by policy|

|920440|Critical - 5|PL1|URL file extension is restricted by policy|

|920450|Critical - 5|PL1|HTTP header is restricted by policy|

|920470|Critical - 5|PL1|Illegal Content-Type header|

|920480|Critical - 5|PL1|Request content type charset isn't allowed by policy|

|920500|Critical - 5|PL1|Attempt to access a backup or working file|

### <a name="drs921-21"></a> PROTOCOL-ATTACK

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|921110|Critical - 5|PL1|HTTP Request Smuggling Attack|

|921120|Critical - 5|PL1|HTTP Response Splitting Attack|

|921130|Critical - 5|PL1|HTTP Response Splitting Attack|

|921140|Critical - 5|PL1|HTTP Header Injection Attack via headers|

|921150|Critical - 5|PL1|HTTP Header Injection Attack via payload (CR/LF detected)|

|921151|Critical - 5|PL2|HTTP Header Injection Attack via payload (CR/LF detected)|

|921160|Critical - 5|PL1|HTTP Header Injection Attack via payload (CR/LF and header-name detected)|

|921190|Critical - 5|PL1|HTTP Splitting (CR/LF in request filename detected)|

|921200|Critical - 5|PL1|LDAP Injection Attack|

### <a name="drs930-21"></a> LFI - Local File Inclusion

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|930100|Critical - 5|PL1|Path Traversal Attack (/../)|

|930110|Critical - 5|PL1|Path Traversal Attack (/../)|

|930120|Critical - 5|PL1|OS File Access Attempt|

|930130|Critical - 5|PL1|Restricted File Access Attempt|

### <a name="drs931-21"></a> RFI - Remote File Inclusion

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|931100|Critical - 5|PL1|Possible Remote File Inclusion (RFI) Attack: URL Parameter using IP Address|

|931110|Critical - 5|PL1|Possible Remote File Inclusion (RFI) Attack: Common RFI Vulnerable Parameter Name used w/URL Payload|

|931120|Critical - 5|PL1|Possible Remote File Inclusion (RFI) Attack: URL Payload Used w/Trailing Question Mark Character (?)|

|931130|Critical - 5|PL2|Possible Remote File Inclusion (RFI) Attack: Off-Domain Reference/Link|

### <a name="drs932-21"></a> RCE - Remote Command Execution

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|932100|Critical - 5|PL1|Remote Command Execution: Unix Command Injection|

|932105|Critical - 5|PL1|Remote Command Execution: Unix Command Injection|

|932110|Critical - 5|PL1|Remote Command Execution: Windows Command Injection|

|932115|Critical - 5|PL1|Remote Command Execution: Windows Command Injection|

|932120|Critical - 5|PL1|Remote Command Execution: Windows PowerShell Command Found|

|932130|Critical - 5|PL1|Remote Command Execution: Unix Shell Expression or Confluence Vulnerability (CVE-2022-26134) Found|

|932140|Critical - 5|PL1|Remote Command Execution: Windows FOR/IF Command Found|

|932150|Critical - 5|PL1|Remote Command Execution: Direct Unix Command Execution|

|932160|Critical - 5|PL1|Remote Command Execution: Unix Shell Code Found|

|932170|Critical - 5|PL1|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932171|Critical - 5|PL1|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932180|Critical - 5|PL1|Restricted File Upload Attempt|

### <a name="drs933-21"></a> PHP Attacks

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|933100|Critical - 5|PL1|PHP Injection Attack: Opening/Closing Tag Found|

|933110|Critical - 5|PL1|PHP Injection Attack: PHP Script File Upload Found|

|933120|Critical - 5|PL1|PHP Injection Attack: Configuration Directive Found|

|933130|Critical - 5|PL1|PHP Injection Attack: Variables Found|

|933140|Critical - 5|PL1|PHP Injection Attack: I/O Stream Found|

|933150|Critical - 5|PL1|PHP Injection Attack: High-Risk PHP Function Name Found|

|933151|Critical - 5|PL2|PHP Injection Attack: Medium-Risk PHP Function Name Found|

|933160|Critical - 5|PL1|PHP Injection Attack: High-Risk PHP Function Call Found|

|933170|Critical - 5|PL1|PHP Injection Attack: Serialized Object Injection|

|933180|Critical - 5|PL1|PHP Injection Attack: Variable Function Call Found|

|933200|Critical - 5|PL1|PHP Injection Attack: Wrapper scheme detected|

|933210|Critical - 5|PL1|PHP Injection Attack: Variable Function Call Found|

### <a name="drs934-21"></a> Node JS Attacks

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|934100|Critical - 5|PL1|Node.js Injection Attack|

### <a name="drs941-21"></a> XSS - Cross-site Scripting

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|941100|Critical - 5|PL1|XSS Attack Detected via libinjection|

|941101|Critical - 5|PL2|XSS Attack Detected via libinjection.<br />This rule detects requests with a *Referer* header|

|941110|Critical - 5|PL1|XSS Filter - Category 1: Script Tag Vector|

|941120|Critical - 5|PL1|XSS Filter - Category 2: Event Handler Vector|

|941130|Critical - 5|PL1|XSS Filter - Category 3: Attribute Vector|

|941140|Critical - 5|PL1|XSS Filter - Category 4: JavaScript URI Vector|

|941150|Critical - 5|PL2|XSS Filter - Category 5: Disallowed HTML Attributes|

|941160|Critical - 5|PL1|NoScript XSS InjectionChecker: HTML Injection|

|941170|Critical - 5|PL1|NoScript XSS InjectionChecker: Attribute Injection|

|941180|Critical - 5|PL1|Node-Validator Blocklist Keywords|

|941190|Critical - 5|PL1|XSS Using style sheets|

|941200|Critical - 5|PL1|XSS using VML frames|

|941210|Critical - 5|PL1|XSS using obfuscated JavaScript|

|941220|Critical - 5|PL1|XSS using obfuscated VB Script|

|941230|Critical - 5|PL1|XSS using 'embed' tag|

|941240|Critical - 5|PL1|XSS using 'import' or 'implementation' attribute|

|941250|Critical - 5|PL1|IE XSS Filters - Attack Detected|

|941260|Critical - 5|PL1|XSS using 'meta' tag|

|941270|Critical - 5|PL1|XSS using 'link' href|

|941280|Critical - 5|PL1|XSS using 'base' tag|

|941290|Critical - 5|PL1|XSS using 'applet' tag|

|941300|Critical - 5|PL1|XSS using 'object' tag|

|941310|Critical - 5|PL1|US-ASCII Malformed Encoding XSS Filter - Attack Detected|

|941320|Critical - 5|PL2|Possible XSS Attack Detected - HTML Tag Handler|

|941330|Critical - 5|PL2|IE XSS Filters - Attack Detected|

|941340|Critical - 5|PL2|IE XSS Filters - Attack Detected|

|941350|Critical - 5|PL1|UTF-7 Encoding IE XSS - Attack Detected|

|941360|Critical - 5|PL1|JavaScript obfuscation detected|

|941370|Critical - 5|PL1|JavaScript global variable found|

|941380|Critical - 5|PL2|AngularJS client side template injection detected|

### <a name="drs942-21"></a> SQLI - SQL Injection

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|942100|Critical - 5|PL1|SQL Injection Attack Detected via libinjection|

|942110|Warning - 3|PL2|SQL Injection Attack: Common Injection Testing Detected|

|942120|Critical - 5|PL2|SQL Injection Attack: SQL Operator Detected|

|942130|Critical - 5|PL2|SQL Injection Attack: SQL Tautology Detected|

|942140|Critical - 5|PL1|SQL Injection Attack: Common DB Names Detected|

|942150|Critical - 5|PL2|SQL Injection Attack|

|942160|Critical - 5|PL1|Detects blind sqli tests using sleep() or benchmark()|

|942170|Critical - 5|PL1|Detects SQL benchmark and sleep injection attempts including conditional queries|

|942180|Critical - 5|PL2|Detects basic SQL authentication bypass attempts 1/3|

|942190|Critical - 5|PL1|Detects MSSQL code execution and information gathering attempts|

|942200|Critical - 5|PL2|Detects MySQL comment-/space-obfuscated injections and backtick termination|

|942210|Critical - 5|PL2|Detects chained SQL injection attempts 1/2|

|942220|Critical - 5|PL1|Looking for integer overflow attacks, these are taken from skipfish, except 3.0.00738585072007e-308 is the "magic number" crash|

|942230|Critical - 5|PL1|Detects conditional SQL injection attempts|

|942240|Critical - 5|PL1|Detects MySQL charset switch and MSSQL DoS attempts|

|942250|Critical - 5|PL1|Detects MATCH AGAINST, MERGE and EXECUTE IMMEDIATE injections|

|942260|Critical - 5|PL2|Detects basic SQL authentication bypass attempts 2/3|

|942270|Critical - 5|PL1|Looking for basic SQL injection. Common attack string for MySQL, Oracle, and others|

|942280|Critical - 5|PL1|Detects Postgres pg_sleep injection, waitfor delay attacks and database shutdown attempts|

|942290|Critical - 5|PL1|Finds basic MongoDB SQL injection attempts|

|942300|Critical - 5|PL2|Detects MySQL comments, conditions, and ch(a)r injections|

|942310|Critical - 5|PL2|Detects chained SQL injection attempts 2/2|

|942320|Critical - 5|PL1|Detects MySQL and PostgreSQL stored procedure/function injections|

|942330|Critical - 5|PL2|Detects classic SQL injection probings 1/2|

|942340|Critical - 5|PL2|Detects basic SQL authentication bypass attempts 3/3|

|942350|Critical - 5|PL1|Detects MySQL UDF injection and other data/structure manipulation attempts|

|942360|Critical - 5|PL1|Detects concatenated basic SQL injection and SQLLFI attempts|

|942361|Critical - 5|PL2|Detects basic SQL injection based on keyword alter or union|

|942370|Critical - 5|PL2|Detects classic SQL injection probings 2/2|

|942380|Critical - 5|PL2|SQL Injection Attack|

|942390|Critical - 5|PL2|SQL Injection Attack|

|942400|Critical - 5|PL2|SQL Injection Attack|

|942410|Critical - 5|PL2|SQL Injection Attack|

|942430|Warning - 3|PL2|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12)|

|942440|Critical - 5|PL2|SQL Comment Sequence Detected|

|942450|Critical - 5|PL2|SQL Hex Encoding Identified|

|942470|Critical - 5|PL2|SQL Injection Attack|

|942480|Critical - 5|PL2|SQL Injection Attack|

|942500|Critical - 5|PL1|MySQL in-line comment detected|

|942510|Critical - 5|PL2|SQLi bypass attempt by ticks or backticks detected|

### <a name="drs943-21"></a> SESSION-FIXATION

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|943100|Critical - 5|PL1|Possible Session Fixation Attack: Setting Cookie Values in HTML|

|943110|Critical - 5|PL1|Possible Session Fixation Attack: SessionID Parameter Name with Off-Domain Referrer|

|943120|Critical - 5|PL1|Possible Session Fixation Attack: SessionID Parameter Name with No Referrer|

### <a name="drs944-21"></a> JAVA Attacks

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|944100|Critical - 5|PL1|Remote Command Execution: Apache Struts, Oracle WebLogic|

|944110|Critical - 5|PL1|Detects potential payload execution|

|944120|Critical - 5|PL1|Possible payload execution and remote command execution|

|944130|Critical - 5|PL1|Suspicious Java classes|

|944200|Critical - 5|PL2|Exploitation of Java deserialization Apache Commons|

|944210|Critical - 5|PL2|Possible use of Java serialization|

|944240|Critical - 5|PL2|Remote Command Execution: Java serialization and Log4j vulnerability ([CVE-2021-44228](https://www.cve.org/CVERecord?id=CVE-2021-44228), [CVE-2021-45046](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-45046))|

|944250|Critical - 5|PL2|Remote Command Execution: Suspicious Java method detected|

### <a name="drs9905-21"></a> MS-ThreatIntel-WebShells

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99005002|Critical - 5|PL2|Web Shell Interaction Attempt (POST)|

|99005003|Critical - 5|PL2|Web Shell Upload Attempt (POST) - CHOPPER PHP|

|99005004|Critical - 5|PL2|Web Shell Upload Attempt (POST) - CHOPPER ASPX|

|99005005|Critical - 5|PL2|Web Shell Interaction Attempt|

|99005006|Critical - 5|PL2|Spring4Shell Interaction Attempt|

### <a name="drs9903-21"></a> MS-ThreatIntel-AppSec

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99030001|Critical - 5|PL2|Path Traversal Evasion in Headers (/.././../)|

|99030002|Critical - 5|PL2|Path Traversal Evasion in Request Body (/.././../)|

### <a name="drs99031-21"></a> MS-ThreatIntel-SQLI

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99031001|Warning - 3|PL2|SQL Injection Attack: Common Injection Testing Detected|

|99031002|Critical - 5|PL2|SQL Comment Sequence Detected|

|99031003|Critical - 5|PL2|SQL Injection Attack|

|99031004|Critical - 5|PL2|Detects basic SQL authentication bypass attempts 2/3|

### <a name="drs99001-21"></a> MS-ThreatIntel-CVEs

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99001001|Critical - 5|PL2|Attempted F5 tmui (CVE-2020-5902) REST API Exploitation with known credentials|

|99001002|Critical - 5|PL2|Attempted Citrix NSC_USER directory traversal [CVE-2019-19781](https://www.cve.org/CVERecord?id=CVE-2019-19781)|

|99001003|Critical - 5|PL2|Attempted Atlassian Confluence Widget Connector exploitation [CVE-2019-3396](https://www.cve.org/CVERecord?id=CVE-2019-3396)|

|99001004|Critical - 5|PL2|Attempted Pulse Secure custom template exploitation [CVE-2020-8243](https://www.cve.org/CVERecord?id=CVE-2019-8243)|

|99001005|Critical - 5|PL2|Attempted SharePoint type converter exploitation [CVE-2020-0932](https://www.cve.org/CVERecord?id=CVE-2019-0932)|

|99001006|Critical - 5|PL2|Attempted Pulse Connect directory traversal [CVE-2019-11510](https://www.cve.org/CVERecord?id=CVE-2019-11510)|

|99001007|Critical - 5|PL2|Attempted Junos OS J-Web local file inclusion [CVE-2020-1631](https://www.cve.org/CVERecord?id=CVE-2019-1631)|

|99001008|Critical - 5|PL2|Attempted Fortinet path traversal [CVE-2018-13379](https://www.cve.org/CVERecord?id=CVE-2019-13379)|

|99001009|Critical - 5|PL2|Attempted Apache struts ognl injection [CVE-2017-5638](https://www.cve.org/CVERecord?id=CVE-2019-5638)|

|99001010|Critical - 5|PL2|Attempted Apache struts ognl injection [CVE-2017-12611](https://www.cve.org/CVERecord?id=CVE-2019-12611)|

|99001011|Critical - 5|PL2|Attempted Oracle WebLogic path traversal [CVE-2020-14882](https://www.cve.org/CVERecord?id=CVE-2019-14882)|

|99001012|Critical - 5|PL2|Attempted Telerik WebUI insecure deserialization exploitation [CVE-2019-18935](https://www.cve.org/CVERecord?id=CVE-2019-18935)|

|99001013|Critical - 5|PL2|Attempted SharePoint insecure XML deserialization [CVE-2019-0604](https://www.cve.org/CVERecord?id=CVE-2019-0604)|

|99001014|Critical - 5|PL2|Attempted Spring Cloud routing-expression injection [CVE-2022-22963](https://www.cve.org/CVERecord?id=CVE-2022-22963)|

|99001015|Critical - 5|PL2|Attempted Spring Framework unsafe class object exploitation [CVE-2022-22965](https://www.cve.org/CVERecord?id=CVE-2022-22965)|

|99001016|Critical - 5|PL2|Attempted Spring Cloud Gateway Actuator injection [CVE-2022-22947](https://www.cve.org/CVERecord?id=CVE-2022-22947)|

|99001017*|N/A|N/A|Attempted Apache Struts file upload exploitation [CVE-2023-50164](https://www.cve.org/CVERecord?id=CVE-2023-50164)|

|99001018|Critical - 5|PL1|Attempted React2Shell remote code execution exploitation [CVE-2025-55182](https://www.cve.org/CVERecord?id=CVE-2025-55182)|

*<sup>This rule's action is set to log by default. Set action to Block to prevent against Apache Struts vulnerability. Anomaly Score not supported for this rule.</sup>

# [Bot Manager 1.0](#tab/bot)

## <a name="bot"></a> 1.0 rule sets

### <a name="bot100"></a> Bad bots

|RuleId|Description|

|---|---|

|Bot100100|Malicious bots detected by threat intelligence|

|Bot100200|Malicious bots that have falsified their identity|

Bot100100 scans both client IP addresses and IPs in the `X-Forwarded-For` header.

### <a name="bot200"></a> Good bots

|RuleId|Description|

|---|---|

|Bot200100|Search engine crawlers|

|Bot200200|Unverified search engine crawlers|

### <a name="bot300"></a> Unknown bots

|RuleId|Description|

|---|---|

|Bot300100|Unspecified identity|

|Bot300200|Tools and frameworks for web crawling and attacks|

|Bot300300|General-purpose HTTP clients and SDKs|

|Bot300400|Service agents|

|Bot300500|Site health monitoring services|

|Bot300600|Unknown bots detected by threat intelligence|

|Bot300700|Other bots|

Bot300600 scans both client IP addresses and IPs in the `X-Forwarded-For` header.

# [Bot Manager 1.1](#tab/bot11)

## <a name="bot11"></a> 1.1 rule sets

### <a name="bot11-100"></a> Bad bots

|RuleId|Description|

|---|---|

|Bot100100|Malicious bots detected by threat intelligence|

|Bot100200|Malicious bots that have falsified their identity|

|Bot100300|High risk bots detected by threat intelligence|

Bot100100 scans both client IP addresses and IPs in the `X-Forwarded-For` header.

### <a name="bot11-200"></a> Good bots

|RuleId|Description|

|---|---|

|Bot200100|Search engine crawlers|

|Bot200200|Verified miscellaneous bots|

|Bot200300|Verified link checker bots|

|Bot200400|Verified social media bots|

|Bot200500|Verified content fetchers|

|Bot200600|Verified feed fetchers|

|Bot200700|Verified advertising bots|

### <a name="bot11-300"></a> Unknown bots

|RuleId|Description|

|---|---|

|Bot300100|Unspecified identity|

|Bot300200|Tools and frameworks for web crawling and attacks|

|Bot300300|General-purpose HTTP clients and SDKs|

|Bot300400|Service agents|

|Bot300500|Site health monitoring services|

|Bot300600|Unknown bots detected by threat intelligence. This rule also includes IP addresses matched to the Tor network|

|Bot300700|Other bots|

Bot300600 scans both client IP addresses and IPs in the `X-Forwarded-For` header.

---

> [!NOTE]

> When reviewing your WAF's logs, you might see rule ID 949110. The description of the rule might include *Inbound Anomaly Score Exceeded*.

>

> This rule indicates that the total anomaly score for the request exceeded the maximum allowable score. For more information, see [Anomaly scoring](./ag-overview.md#anomaly-scoring-mode).

Below are previous Core Rule Set versions. If you're using CRS 3.2, CRS 3.1, CRS 3.0, or CRS 2.2.9, it's recommended to upgrade to the latest ruleset version of DRS 2.1. For more information, see [Upgrading or changing ruleset version](upgrade-ruleset-version.md).

# [OWASP 3.2 (legacy)](#tab/owasp32)

## <a name="owasp32"></a> 3.2 rule sets

### <a name="general-32"></a> General

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|200002|Critical - 5|PL1|Failed to Parse Request Body|

|200003|Critical - 5|PL1|Multipart Request Body Strict Validation|

|200004|Critical - 5|PL1|Possible Multipart Unmatched Boundary|

### <a name="crs800-32"></a> KNOWN-CVES

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|800100|Critical - 5|PL2|Rule to help detect and mitigate log4j vulnerability [CVE-2021-44228](https://www.cve.org/CVERecord?id=CVE-2021-44228), [CVE-2021-45046](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-45046)|

|800110|Critical - 5|PL2|Spring4Shell Interaction Attempt|

|800111|Critical - 5|PL2|Attempted Spring Cloud routing-expression injection - [CVE-2022-22963](https://www.cve.org/CVERecord?id=CVE-2022-22963)|

|800112|Critical - 5|PL2|Attempted Spring Framework unsafe class object exploitation - [CVE-2022-22965](https://www.cve.org/CVERecord?id=CVE-2022-22965)|

|800113|Critical - 5|PL2|Attempted Spring Cloud Gateway Actuator injection - [CVE-2022-22947](https://www.cve.org/CVERecord?id=CVE-2022-22947)|

|800114*|Critical - 5|PL2|Attempted Apache Struts file upload exploitation - [CVE-2023-50164](https://www.cve.org/CVERecord?id=CVE-2023-50164)|

|800115|Critical - 5|PL1|Attempted React2Shell remote code execution exploitation [CVE-2025-55182](https://www.cve.org/CVERecord?id=CVE-2025-55182)|

*<sup>This rule's action is set to log by default. Set action to Block to prevent against Apache Struts vulnerability. Anomaly Score not supported for this rule.</sup>

### <a name="crs911-32"></a> REQUEST-911-METHOD-ENFORCEMENT

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|911100|Critical - 5|PL1|Method isn't allowed by policy|

### <a name="crs913-32"></a> REQUEST-913-SCANNER-DETECTION

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|913100|Critical - 5|PL1|Found User-Agent associated with security scanner|

|913101|Critical - 5|PL2|Found User-Agent associated with scripting/generic HTTP client|

|913102|Critical - 5|PL2|Found User-Agent associated with web crawler/bot|

|913110|Critical - 5|PL1|Found request header associated with security scanner|

|913120|Critical - 5|PL1|Found request filename/argument associated with security scanner|

### <a name="crs920-32"></a> REQUEST-920-PROTOCOL-ENFORCEMENT

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|920100|Warning - 3|PL1|Invalid HTTP Request Line|

|920120|Critical - 5|PL1|Attempted multipart/form-data bypass|

|920121|Critical - 5|PL2|Attempted multipart/form-data bypass|

|920160|Critical - 5|PL1|Content-Length HTTP header isn't numeric|

|920170|Critical - 5|PL1|GET or HEAD Request with Body Content|

|920171|Critical - 5|PL1|GET or HEAD Request with Transfer-Encoding|

|920180|Warning - 3|PL1|POST request missing Content-Length Header|

|920190|Warning - 3|PL1|Range: Invalid Last Byte Value|

|920200|Warning - 3|PL2|Range: Too many fields (6 or more)|

|920201|Warning - 3|PL2|Range: Too many fields for pdf request (35 or more)|

|920210|Warning - 3|PL1|Multiple/Conflicting Connection Header Data Found|

|920220|Warning - 3|PL1|URL Encoding Abuse Attack Attempt|

|920230|Warning - 3|PL2|Multiple URL Encoding Detected|

|920240|Warning - 3|PL1|URL Encoding Abuse Attack Attempt|

|920250|Warning - 3|PL1|UTF8 Encoding Abuse Attack Attempt|

|920260|Warning - 3|PL1|Unicode Full/Half Width Abuse Attack Attempt|

|920270|Critical - 5|PL1|Invalid character in request (null character)|

|920271|Critical - 5|PL2|Invalid character in request (non printable characters)|

|920280|Warning - 3|PL1|Request Missing a Host Header|

|920290|Warning - 3|PL1|Empty Host Header|

|920300|Notice - 2|PL2|Request Missing an Accept Header|

|920310|Notice - 2|PL1|Request Has an Empty Accept Header|

|920311|Notice - 2|PL1|Request Has an Empty Accept Header|

|920320|Notice - 2|PL2|Missing User Agent Header|

|920330|Notice - 2|PL1|Empty User Agent Header|

|920340|Notice - 2|PL1|Request Containing Content, but Missing Content-Type header|

|920341|Critical - 5|PL2|Request containing content requires Content-Type header|

|920350|Warning - 3|PL1|Host header is a numeric IP address|

|920420|Critical - 5|PL1|Request content type isn't allowed by policy|

|920430|Critical - 5|PL1|HTTP protocol version isn't allowed by policy|

|920440|Critical - 5|PL1|URL file extension is restricted by policy|

|920450|Critical - 5|PL1|HTTP header is restricted by policy (%{MATCHED_VAR})|

|920470|Critical - 5|PL1|Illegal Content-Type header|

|920480|Critical - 5|PL1|Restrict charset parameter within the content-type header|

### <a name="crs921-32"></a> REQUEST-921-PROTOCOL-ATTACK

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|921110|Critical - 5|PL1|HTTP Request Smuggling Attack|

|921120|Critical - 5|PL1|HTTP Response Splitting Attack|

|921130|Critical - 5|PL1|HTTP Response Splitting Attack|

|921140|Critical - 5|PL1|HTTP Header Injection Attack via headers|

|921150|Critical - 5|PL1|HTTP Header Injection Attack via payload (CR/LF detected)|

|921151|Critical - 5|PL2|HTTP Header Injection Attack via payload (CR/LF detected)|

|921160|Critical - 5|PL1|HTTP Header Injection Attack via payload (CR/LF and header-name detected)|

### <a name="crs930-32"></a> REQUEST-930-APPLICATION-ATTACK-LFI

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|930100|Critical - 5|PL1|Path Traversal Attack (/../)|

|930110|Critical - 5|PL1|Path Traversal Attack (/../)|

|930120|Critical - 5|PL1|OS File Access Attempt|

|930130|Critical - 5|PL1|Restricted File Access Attempt|

### <a name="crs931-32"></a> REQUEST-931-APPLICATION-ATTACK-RFI

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|931100|Critical - 5|PL1|Possible Remote File Inclusion (RFI) Attack: URL Parameter using IP Address|

|931110|Critical - 5|PL1|Possible Remote File Inclusion (RFI) Attack: Common RFI Vulnerable Parameter Name used w/URL Payload|

|931120|Critical - 5|PL1|Possible Remote File Inclusion (RFI) Attack: URL Payload Used w/Trailing Question Mark Character (?)|

|931130|Critical - 5|PL2|Possible Remote File Inclusion (RFI) Attack: Off-Domain Reference/Link|

### <a name="crs932-32"></a> REQUEST-932-APPLICATION-ATTACK-RCE

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|932100|Critical - 5|PL1|Remote Command Execution: Unix Command Injection|

|932105|Critical - 5|PL1|Remote Command Execution: Unix Command Injection|

|932110|Critical - 5|PL1|Remote Command Execution: Windows Command Injection|

|932115|Critical - 5|PL1|Remote Command Execution: Windows Command Injection|

|932120|Critical - 5|PL1|Remote Command Execution: Windows PowerShell Command Found|

|932130|Critical - 5|PL1|Remote Command Execution: Unix Shell Expression or Confluence Vulnerability (CVE-2022-26134) or Text4Shell ([CVE-2022-42889](https://nvd.nist.gov/vuln/detail/CVE-2022-42889)) Found|

|932140|Critical - 5|PL1|Remote Command Execution: Windows FOR/IF Command Found|

|932150|Critical - 5|PL1|Remote Command Execution: Direct Unix Command Execution|

|932160|Critical - 5|PL1|Remote Command Execution: Unix Shell Code Found|

|932170|Critical - 5|PL1|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932171|Critical - 5|PL1|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932180|Critical - 5|PL1|Restricted File Upload Attempt|

### <a name="crs933-32"></a> REQUEST-933-APPLICATION-ATTACK-PHP

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|933100|Critical - 5|PL1|PHP Injection Attack: Opening/Closing Tag Found|

|933110|Critical - 5|PL1|PHP Injection Attack: PHP Script File Upload Found|

|933120|Critical - 5|PL1|PHP Injection Attack: Configuration Directive Found|

|933130|Critical - 5|PL1|PHP Injection Attack: Variables Found|

|933140|Critical - 5|PL1|PHP Injection Attack: I/O Stream Found|

|933150|Critical - 5|PL1|PHP Injection Attack: High-Risk PHP Function Name Found|

|933151|Critical - 5|PL2|PHP Injection Attack: Medium-Risk PHP Function Name Found|

|933160|Critical - 5|PL1|PHP Injection Attack: High-Risk PHP Function Call Found|

|933170|Critical - 5|PL1|PHP Injection Attack: Serialized Object Injection|

|933180|Critical - 5|PL1|PHP Injection Attack: Variable Function Call Found|

|933200|Critical - 5|PL1|PHP Injection Attack: Wrapper scheme detected|

|933210|Critical - 5|PL1|PHP Injection Attack: Variable Function Call Found|

### <a name="crs941-32"></a> REQUEST-941-APPLICATION-ATTACK-XSS

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|941100|Critical - 5|PL1|XSS Attack Detected via libinjection|

|941101|Critical - 5|PL2|XSS Attack Detected via libinjection <br />This rule detects requests with a *Referer* header|

|941110|Critical - 5|PL1|XSS Filter - Category 1: Script Tag Vector|

|941120|Critical - 5|PL1|XSS Filter - Category 2: Event Handler Vector|

|941130|Critical - 5|PL1|XSS Filter - Category 3: Attribute Vector|

|941140|Critical - 5|PL1|XSS Filter - Category 4: JavaScript URI Vector|

|941150|Critical - 5|PL2|XSS Filter - Category 5: Disallowed HTML Attributes|

|941160|Critical - 5|PL1|NoScript XSS InjectionChecker: HTML Injection|

|941170|Critical - 5|PL1|NoScript XSS InjectionChecker: Attribute Injection|

|941180|Critical - 5|PL1|Node-Validator Blacklist Keywords|

|941190|Critical - 5|PL1|XSS Using style sheets|

|941200|Critical - 5|PL1|XSS using VML frames|

|941210|Critical - 5|PL1|XSS using obfuscated JavaScript or Text4Shell ([CVE-2022-42889](https://nvd.nist.gov/vuln/detail/CVE-2022-42889))|

|941220|Critical - 5|PL1|XSS using obfuscated VB Script|

|941230|Critical - 5|PL1|XSS using 'embed' tag|

|941240|Critical - 5|PL1|XSS using 'import' or 'implementation' attribute|

|941250|Critical - 5|PL1|IE XSS Filters - Attack Detected|

|941260|Critical - 5|PL1|XSS using 'meta' tag|

|941270|Critical - 5|PL1|XSS using 'link' href|

|941280|Critical - 5|PL1|XSS using 'base' tag|

|941290|Critical - 5|PL1|XSS using 'applet' tag|

|941300|Critical - 5|PL1|XSS using 'object' tag|

|941310|Critical - 5|PL1|US-ASCII Malformed Encoding XSS Filter - Attack Detected|

|941320|Critical - 5|PL2|Possible XSS Attack Detected - HTML Tag Handler|

|941330|Critical - 5|PL2|IE XSS Filters - Attack Detected|

|941340|Critical - 5|PL2|IE XSS Filters - Attack Detected|

|941350|Critical - 5|PL1|UTF-7 Encoding IE XSS - Attack Detected|

|941360|Critical - 5|PL1|JavaScript obfuscation detected|

### <a name="crs942-32"></a> REQUEST-942-APPLICATION-ATTACK-SQLI

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|942100|Critical - 5|PL1|SQL Injection Attack Detected via libinjection|

|942110|Warning - 3|PL2|SQL Injection Attack: Common Injection Testing Detected|

|942120|Critical - 5|PL2|SQL Injection Attack: SQL Operator Detected|

|942130|Critical - 5|PL2|SQL Injection Attack: SQL Tautology Detected|

|942140|Critical - 5|PL1|SQL Injection Attack: Common DB Names Detected|

|942150|Critical - 5|PL2|SQL Injection Attack|

|942160|Critical - 5|PL1|Detects blind sqli tests using sleep() or benchmark()|

|942170|Critical - 5|PL1|Detects SQL benchmark and sleep injection attempts including conditional queries|

|942180|Critical - 5|PL2|Detects basic SQL authentication bypass attempts 1/3|

|942190|Critical - 5|PL1|Detects MSSQL code execution and information gathering attempts|

|942200|Critical - 5|PL2|Detects MySQL comment-/space-obfuscated injections and backtick termination|

|942210|Critical - 5|PL2|Detects chained SQL injection attempts 1/2|

|942220|Critical - 5|PL1|Looking for integer overflow attacks, these are taken from skipfish, except 3.0.00738585072007e-308 is the "magic number" crash|

|942230|Critical - 5|PL1|Detects conditional SQL injection attempts|

|942240|Critical - 5|PL1|Detects MySQL charset switch and MSSQL DoS attempts|

|942250|Critical - 5|PL1|Detects MATCH AGAINST, MERGE, and EXECUTE IMMEDIATE injections|

|942260|Critical - 5|PL2|Detects basic SQL authentication bypass attempts 2/3|

|942270|Critical - 5|PL1|Looking for basic SQL injection. Common attack string for MySQL, Oracle, and others|

|942280|Critical - 5|PL1|Detects Postgres pg_sleep injection, waitfor delay attacks and database shutdown attempts|

|942290|Critical - 5|PL1|Finds basic MongoDB SQL injection attempts|

|942300|Critical - 5|PL2|Detects MySQL comments, conditions, and ch(a)r injections|

|942310|Critical - 5|PL2|Detects chained SQL injection attempts 2/2|

|942320|Critical - 5|PL1|Detects MySQL and PostgreSQL stored procedure/function injections|

|942330|Critical - 5|PL2|Detects classic SQL injection probings 1/2|

|942340|Critical - 5|PL2|Detects basic SQL authentication bypass attempts 3/3|

|942350|Critical - 5|PL1|Detects MySQL UDF injection and other data/structure manipulation attempts|

|942360|Critical - 5|PL1|Detects concatenated basic SQL injection and SQLLFI attempts|

|942361|Critical - 5|PL2|Detects basic SQL injection based on keyword alter or union|

|942370|Critical - 5|PL2|Detects classic SQL injection probings 2/2|

|942380|Critical - 5|PL2|SQL Injection Attack|

|942390|Critical - 5|PL2|SQL Injection Attack|

|942400|Critical - 5|PL2|SQL Injection Attack|

|942410|Critical - 5|PL2|SQL Injection Attack|

|942430|Warning - 3|PL2|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12)|

|942440|Critical - 5|PL2|SQL Comment Sequence Detected|

|942450|Critical - 5|PL2|SQL Hex Encoding Identified|

|942470|Critical - 5|PL2|SQL Injection Attack|

|942480|Critical - 5|PL2|SQL Injection Attack|

|942500|Critical - 5|PL1|MySQL in-line comment detected|

### <a name="crs943-32"></a> REQUEST-943-APPLICATION-ATTACK-SESSION-FIXATION

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|943100|Critical - 5|PL1|Possible Session Fixation Attack: Setting Cookie Values in HTML|

|943110|Critical - 5|PL1|Possible Session Fixation Attack: SessionID Parameter Name with Off-Domain Referer|

|943120|Critical - 5|PL1|Possible Session Fixation Attack: SessionID Parameter Name with No Referer|

### <a name="crs944-32"></a> REQUEST-944-APPLICATION-ATTACK-JAVA

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|944100|Critical - 5|PL1|Remote Command Execution: Apache Struts, Oracle WebLogic|

|944110|Critical - 5|PL1|Detects potential payload execution|

|944120|Critical - 5|PL1|Possible payload execution and remote command execution|

|944130|Critical - 5|PL1|Suspicious Java classes|

|944200|Critical - 5|PL2|Exploitation of Java deserialization Apache Commons|

|944210|Critical - 5|PL2|Possible use of Java serialization|

|944240|Critical - 5|PL1|Remote Command Execution: Java serialization|

|944250|Critical - 5|PL1|Remote Command Execution: Suspicious Java method detected|

### <a name="crs944-32"></a> Inactive Rules

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|920202|Warning - 3|PL4|(Inactive rule, should be ignored) Range: Too many fields for pdf request (6 or more)|

|920272|Critical - 5|PL3|(Inactive rule, should be ignored) Invalid character in request (outside of printable chars below ascii 127)|

|920273|Critical - 5|PL4|(Inactive rule, should be ignored) Invalid character in request (outside of very strict set)|

|920274|Critical - 5|PL4|(Inactive rule, should be ignored) Invalid character in request headers (outside of very strict set)|

|920460|Critical - 5|PL4|(Inactive rule, should be ignored) Abnormal Escape Characters|

|921170|N/A|PL3|(Inactive rule, should be ignored) HTTP Parameter Pollution|

|921180|Critical - 5|PL3|(Inactive rule, should be ignored) HTTP Parameter Pollution (%{TX.1})|

|932106|Critical - 5|PL3|(Inactive rule, should be ignored) Remote Command Execution: Unix Command Injection|

|932190|Critical - 5|PL3|(Inactive rule, should be ignored) Remote Command Execution: Wildcard bypass technique attempt|

|933111|Critical - 5|PL3|(Inactive rule, should be ignored) PHP Injection Attack: PHP Script File Upload Found|

|933131|Critical - 5|PL3|(Inactive rule, should be ignored) PHP Injection Attack: Variables Found|

|933161|Critical - 5|PL3|(Inactive rule, should be ignored) PHP Injection Attack: Low-Value PHP Function Call Found|

|933190|Critical - 5|PL3|(Inactive rule, should be ignored) PHP Injection Attack: PHP Closing Tag Found|

|942251|Critical - 5|PL3|(Inactive rule, should be ignored) Detects HAVING injections|

|942420|Warning - 3|PL3|(Inactive rule, should be ignored) Restricted SQL Character Anomaly Detection (cookies): # of special characters exceeded (8)|

|942421|Warning - 3|PL4|(Inactive rule, should be ignored) Restricted SQL Character Anomaly Detection (cookies): # of special characters exceeded (3)|

|942431|Warning - 3|PL3|(Inactive rule, should be ignored) Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (6)|

|942432|Warning - 3|PL4|(Inactive rule, should be ignored) Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (2)|

|942460|Warning - 3|PL3|(Inactive rule, should be ignored) Meta-Character Anomaly Detection Alert - Repetitive Non-Word Characters|

|942490|Critical - 5|PL3|(Inactive rule, should be ignored) Detects classic SQL injection probings 3/3|

# [OWASP 3.1 (support end date set)](#tab/owasp31)

## <a name="owasp31"></a> 3.1 rule sets

### <a name="general-31"></a> General

|RuleId|Description|

|---|---|

|200004|Possible Multipart Unmatched Boundary|

### <a name="crs800-31"></a> KNOWN-CVES

|RuleId|Description|

|---|---|

|800100|Rule to help detect and mitigate log4j vulnerability [CVE-2021-44228](https://www.cve.org/CVERecord?id=CVE-2021-44228), [CVE-2021-45046](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-45046)|

|800110|Spring4Shell Interaction Attempt|

|800111|Attempted Spring Cloud routing-expression injection - [CVE-2022-22963](https://www.cve.org/CVERecord?id=CVE-2022-22963)|

|800112|Attempted Spring Framework unsafe class object exploitation - [CVE-2022-22965](https://www.cve.org/CVERecord?id=CVE-2022-22965)|

|800113|Attempted Spring Cloud Gateway Actuator injection - [CVE-2022-22947](https://www.cve.org/CVERecord?id=CVE-2022-22947)|

|800114*|Attempted Apache Struts file upload exploitation - [CVE-2023-50164](https://www.cve.org/CVERecord?id=CVE-2023-50164)|

|800115|Attempted React2Shell remote code execution exploitation [CVE-2025-55182](https://www.cve.org/CVERecord?id=CVE-2025-55182)|

*<sup>Older WAFs running CRS 3.1 only support logging mode for this rule. To enable block mode you will need to upgrade to a newer ruleset version.</sup>

### <a name="crs911-31"></a> REQUEST-911-METHOD-ENFORCEMENT

|RuleId|Description|

|---|---|

|911100|Method isn't allowed by policy|

### <a name="crs913-31"></a> REQUEST-913-SCANNER-DETECTION

|RuleId|Description|

|---|---|

|913100|Found User-Agent associated with security scanner|

|913101|Found User-Agent associated with scripting/generic HTTP client|

|913102|Found User-Agent associated with web crawler/bot|

|913110|Found request header associated with security scanner|

|913120|Found request filename/argument associated with security scanner|

### <a name="crs920-31"></a> REQUEST-920-PROTOCOL-ENFORCEMENT

|RuleId|Description|

|---|---|

|920100|Invalid HTTP Request Line|

|920120|Attempted multipart/form-data bypass|

|920121|Attempted multipart/form-data bypass|

|920130|Failed to parse request body|

|920140|Multipart request body failed strict validation|

|920160|Content-Length HTTP header isn't numeric|

|920170|GET or HEAD Request with Body Content|

|920171|GET or HEAD Request with Transfer-Encoding|

|920180|POST request missing Content-Length Header|

|920190|Range = Invalid Last Byte Value|

|920200|Range = Too many fields (6 or more)|

|920201|Range = Too many fields for pdf request (35 or more)|

|920202|Range = Too many fields for pdf request (6 or more)|

|920210|Multiple/Conflicting Connection Header Data Found|

|920220|URL Encoding Abuse Attack Attempt|

|920230|Multiple URL Encoding Detected|

|920240|URL Encoding Abuse Attack Attempt|

|920250|UTF8 Encoding Abuse Attack Attempt|

|920260|Unicode Full/Half Width Abuse Attack Attempt|

|920270|Invalid character in request (null character)|

|920271|Invalid character in request (non printable characters)|

|920272|Invalid character in request (outside of printable chars below ascii 127)|

|920273|Invalid character in request (outside of very strict set)|

|920274|Invalid character in request headers (outside of very strict set)|

|920280|Request Missing a Host Header|

|920290|Empty Host Header|

|920300|Request Missing an Accept Header|

|920310|Request Has an Empty Accept Header|

|920311|Request Has an Empty Accept Header|

|920320|Missing User Agent Header|

|920330|Empty User Agent Header|

|920340|Request Containing Content but Missing Content-Type header|

|920341|Request containing content requires Content-Type header|

|920350|Host header is a numeric IP address|

|920420|Request content type isn't allowed by policy|

|920430|HTTP protocol version isn't allowed by policy|

|920440|URL file extension is restricted by policy|

|920450|HTTP header is restricted by policy (%@{MATCHED_VAR})|

|920460|Abnormal Escape Characters|

|920470|Illegal Content-Type header|

|920480|Restrict charset parameter within the content-type header|

### <a name="crs921-31"></a> REQUEST-921-PROTOCOL-ATTACK

|RuleId|Description|

|---|---|

|921110|HTTP Request Smuggling Attack|

|921120|HTTP Response Splitting Attack|

|921130|HTTP Response Splitting Attack|

|921140|HTTP Header Injection Attack via headers|

|921150|HTTP Header Injection Attack via payload (CR/LF detected)|

|921151|HTTP Header Injection Attack via payload (CR/LF detected)|

|921160|HTTP Header Injection Attack via payload (CR/LF and header-name detected)|

|921170|HTTP Parameter Pollution|

|921180|HTTP Parameter Pollution (%{TX.1})|

### <a name="crs930-31"></a> REQUEST-930-APPLICATION-ATTACK-LFI

|RuleId|Description|

|---|---|

|930100|Path Traversal Attack (/../)|

|930110|Path Traversal Attack (/../)|

|930120|OS File Access Attempt|

|930130|Restricted File Access Attempt|

### <a name="crs931-31"></a> REQUEST-931-APPLICATION-ATTACK-RFI

|RuleId|Description|

|---|---|

|931100|Possible Remote File Inclusion (RFI) Attack = URL Parameter using IP Address|

|931110|Possible Remote File Inclusion (RFI) Attack = Common RFI Vulnerable Parameter Name used w/URL Payload|

|931120|Possible Remote File Inclusion (RFI) Attack = URL Payload Used w/Trailing Question Mark Character (?)|

|931130|Possible Remote File Inclusion (RFI) Attack = Off-Domain Reference/Link|

### <a name="crs932-31"></a> REQUEST-932-APPLICATION-ATTACK-RCE

|RuleId|Description|

|---|---|

|932100|Remote Command Execution: Unix Command Injection|

|932105|Remote Command Execution: Unix Command Injection|

|932106|Remote Command Execution: Unix Command Injection|

|932110|Remote Command Execution: Windows Command Injection|

|932115|Remote Command Execution: Windows Command Injection|

|932120|Remote Command Execution = Windows PowerShell Command Found|

|932130|Remote Command Execution: Unix Shell Expression or Confluence Vulnerability (CVE-2022-26134) or Text4Shell ([CVE-2022-42889](https://nvd.nist.gov/vuln/detail/CVE-2022-42889)) Found|

|932140|Remote Command Execution = Windows FOR/IF Command Found|

|932150|Remote Command Execution: Direct Unix Command Execution|

|932160|Remote Command Execution = Unix Shell Code Found|

|932170|Remote Command Execution = Shellshock (CVE-2014-6271)|

|932171|Remote Command Execution = Shellshock (CVE-2014-6271)|

|932180|Restricted File Upload Attempt|

|932190|Remote Command Execution: Wildcard bypass technique attempt|

### <a name="crs933-31"></a> REQUEST-933-APPLICATION-ATTACK-PHP

|RuleId|Description|

|---|---|

|933100|PHP Injection Attack = Opening/Closing Tag Found|

|933110|PHP Injection Attack = PHP Script File Upload Found|

|933111|PHP Injection Attack: PHP Script File Upload Found|

|933120|PHP Injection Attack = Configuration Directive Found|

|933130|PHP Injection Attack = Variables Found|

|933131|PHP Injection Attack: Variables Found|

|933140|PHP Injection Attack: I/O Stream Found|

|933150|PHP Injection Attack = High-Risk PHP Function Name Found|

|933151|PHP Injection Attack: Medium-Risk PHP Function Name Found|

|933160|PHP Injection Attack = High-Risk PHP Function Call Found|

|933161|PHP Injection Attack: Low-Value PHP Function Call Found|

|933170|PHP Injection Attack: Serialized Object Injection|

|933180|PHP Injection Attack = Variable Function Call Found|

|933190|PHP Injection Attack: PHP Closing Tag Found|

### <a name="crs941-31"></a> REQUEST-941-APPLICATION-ATTACK-XSS

|RuleId|Description|

|---|---|

|941100|XSS Attack Detected via libinjection|

|941101|XSS Attack Detected via libinjection.<br />This rule detects requests with a *Referer* header|

|941110|XSS Filter - Category 1 = Script Tag Vector|

|941120|XSS Filter - Category 2 = Event Handler Vector|

|941130|XSS Filter - Category 3 = Attribute Vector|

|941140|XSS Filter - Category 4 = JavaScript URI Vector|

|941150|XSS Filter - Category 5 = Disallowed HTML Attributes|

|941160|NoScript XSS InjectionChecker: HTML Injection|

|941170|NoScript XSS InjectionChecker: Attribute Injection|

|941180|Node-Validator Blocklist Keywords|

|941190|XSS using style sheets|

|941200|XSS using VML frames|

|941210|XSS using obfuscated JavaScript or Text4Shell ([CVE-2022-42889](https://nvd.nist.gov/vuln/detail/CVE-2022-42889))|

|941220|XSS using obfuscated VB Script|

|941230|XSS using 'embed' tag|

|941240|XSS using 'import' or 'implementation' attribute|

|941250|IE XSS Filters - Attack Detected|

|941260|XSS using 'meta' tag|

|941270|XSS using 'link' href|

|941280|XSS using 'base' tag|

|941290|XSS using 'applet' tag|

|941300|XSS using 'object' tag|

|941310|US-ASCII Malformed Encoding XSS Filter - Attack Detected|

|941320|Possible XSS Attack Detected - HTML Tag Handler|

|941330|IE XSS Filters - Attack Detected|

|941340|IE XSS Filters - Attack Detected|

|941350|UTF-7 Encoding IE XSS - Attack Detected|

### <a name="crs942-31"></a> REQUEST-942-APPLICATION-ATTACK-SQLI

|RuleId|Description|

|---|---|

|942100|SQL Injection Attack Detected via libinjection|

|942110|SQL Injection Attack: Common Injection Testing Detected|

|942120|SQL Injection Attack: SQL Operator Detected|

|942130|SQL Injection Attack: SQL Tautology Detected|

|942140|SQL Injection Attack = Common DB Names Detected|

|942150|SQL Injection Attack|

|942160|Detects blind sqli tests using sleep() or benchmark()|

|942170|Detects SQL benchmark and sleep injection attempts including conditional queries|

|942180|Detects basic SQL authentication bypass attempts 1/3|

|942190|Detects MSSQL code execution and information gathering attempts|

|942200|Detects MySQL comment-/space-obfuscated injections and backtick termination|

|942210|Detects chained SQL injection attempts 1/2|

|942220|Looking for integer overflow attacks, these are taken from skipfish, except 3.0.00738585072|

|942230|Detects conditional SQL injection attempts|

|942240|Detects MySQL charset switch and MSSQL DoS attempts|

|942250|Detects MATCH AGAINST, MERGE, and EXECUTE IMMEDIATE injections|

|942251|Detects HAVING injections|

|942260|Detects basic SQL authentication bypass attempts 2/3|

|942270|Looking for basic SQL injection. Common attack string for MySQL, Oracle, and others|

|942280|Detects Postgres pg_sleep injection, waitfor delay attacks, and database shutdown attempts|

|942290|Finds basic MongoDB SQL injection attempts|

|942300|Detects MySQL comments, conditions, and ch(a)r injections|

|942310|Detects chained SQL injection attempts 2/2|

|942320|Detects MySQL and PostgreSQL stored procedure/function injections|

|942330|Detects classic SQL injection probings 1/2|

|942340|Detects basic SQL authentication bypass attempts 3/3|

|942350|Detects MySQL UDF injection and other data/structure manipulation attempts|

|942360|Detects concatenated basic SQL injection and SQLLFI attempts|

|942361|Detects basic SQL injection based on keyword alter or union|

|942370|Detects classic SQL injection probings 2/2|

|942380|SQL Injection Attack|

|942390|SQL Injection Attack|

|942400|SQL Injection Attack|

|942410|SQL Injection Attack|

|942420|Restricted SQL Character Anomaly Detection (cookies): # of special characters exceeded (8)|

|942421|Restricted SQL Character Anomaly Detection (cookies): # of special characters exceeded (3)|

|942430|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12)|

|942431|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (6)|

|942432|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (2)|

|942440|SQL Comment Sequence Detected|

|942450|SQL Hex Encoding Identified|

|942460|Meta-Character Anomaly Detection Alert - Repetitive Non-Word Characters|

|942470|SQL Injection Attack|

|942480|SQL Injection Attack|

|942490|Detects classic SQL injection probings 3/3|

### <a name="crs943-31"></a> REQUEST-943-APPLICATION-ATTACK-SESSION-FIXATION

|RuleId|Description|

|---|---|

|943100|Possible Session Fixation Attack = Setting Cookie Values in HTML|

|943110|Possible Session Fixation Attack = SessionID Parameter Name with Off-Domain Referrer|

|943120|Possible Session Fixation Attack = SessionID Parameter Name with No Referrer|

### <a name="crs944-31"></a> REQUEST-944-APPLICATION-ATTACK-SESSION-JAVA

|RuleId|Description|

|---|---|

|944100|Remote Command Execution: Apache Struts, Oracle WebLogic|

|944110|Detects potential payload execution|

|944120|Possible payload execution and remote command execution|

|944130|Suspicious Java classes|

|944200|Exploitation of Java deserialization Apache Commons|

|944210|Possible use of Java serialization|

|944240|Remote Command Execution: Java serialization and Log4j vulnerability ([CVE-2021-44228](https://www.cve.org/CVERecord?id=CVE-2021-44228), [CVE-2021-45046](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-45046))|

|944250|Remote Command Execution: Suspicious Java method detected|

# [OWASP 3.0 (support end date set)](#tab/owasp30)

## <a name="owasp30"></a> 3.0 rule sets

### <a name="general-30"></a> General

|RuleId|Description|

|---|---|

|200004|Possible Multipart Unmatched Boundary|

### <a name="crs800-30"></a> KNOWN-CVES

|RuleId|Description|

|---|---|

|800100|Rule to help detect and mitigate log4j vulnerability [CVE-2021-44228](https://www.cve.org/CVERecord?id=CVE-2021-44228), [CVE-2021-45046](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-45046)|

|800110|Spring4Shell Interaction Attempt|

|800111|Attempted Spring Cloud routing-expression injection - [CVE-2022-22963](https://www.cve.org/CVERecord?id=CVE-2022-22963)|

|800112|Attempted Spring Framework unsafe class object exploitation - [CVE-2022-22965](https://www.cve.org/CVERecord?id=CVE-2022-22965)|

|800113|Attempted Spring Cloud Gateway Actuator injection - [CVE-2022-22947](https://www.cve.org/CVERecord?id=CVE-2022-22947)|

### <a name="crs911-30"></a> REQUEST-911-METHOD-ENFORCEMENT

|RuleId|Description|

|---|---|

|911100|Method isn't allowed by policy|

### <a name="crs913-30"></a> REQUEST-913-SCANNER-DETECTION

|RuleId|Description|

|---|---|

|913100|Found User-Agent associated with security scanner|

|913110|Found request header associated with security scanner|

|913120|Found request filename/argument associated with security scanner|

|913101|Found User-Agent associated with scripting/generic HTTP client|

|913102|Found User-Agent associated with web crawler/bot|

### <a name="crs920-30"></a> REQUEST-920-PROTOCOL-ENFORCEMENT

|RuleId|Description|

|---|---|

|920100|Invalid HTTP Request Line|

|920120|Attempted multipart/form-data bypass|

|920130|Failed to parse request body|

|920140|Multipart request body failed strict validation|

|920160|Content-Length HTTP header isn't numeric|

|920170|GET or HEAD Request with Body Content|

|920180|POST request missing Content-Length Header|

|920190|Range = Invalid Last Byte Value|

|920210|Multiple/Conflicting Connection Header Data Found|

|920220|URL Encoding Abuse Attack Attempt|

|920240|URL Encoding Abuse Attack Attempt|

|920250|UTF8 Encoding Abuse Attack Attempt|

|920260|Unicode Full/Half Width Abuse Attack Attempt|

|920270|Invalid character in request (null character)|

|920280|Request Missing a Host Header|

|920290|Empty Host Header|

|920310|Request Has an Empty Accept Header|

|920311|Request Has an Empty Accept Header|

|920330|Empty User Agent Header|

|920340|Request Containing Content but Missing Content-Type header|

|920350|Host header is a numeric IP address|

|920420|Request content type isn't allowed by policy|

|920430|HTTP protocol version isn't allowed by policy|

|920440|URL file extension is restricted by policy|

|920450|HTTP header is restricted by policy (%@{MATCHED_VAR})|

|920200|Range = Too many fields (6 or more)|

|920201|Range = Too many fields for pdf request (35 or more)|

|920230|Multiple URL Encoding Detected|

|920300|Request Missing an Accept Header|

|920271|Invalid character in request (non printable characters)|

|920320|Missing User Agent Header|

|920272|Invalid character in request (outside of printable chars below ascii 127)|

|920202|Range = Too many fields for pdf request (6 or more)|

|920273|Invalid character in request (outside of very strict set)|

|920274|Invalid character in request headers (outside of very strict set)|

|920460|Abnormal escape characters|

### <a name="crs921-30"></a> REQUEST-921-PROTOCOL-ATTACK

|RuleId|Description|

|---|---|

|921100|HTTP Request Smuggling Attack|

|921110|HTTP Request Smuggling Attack|

|921120|HTTP Response Splitting Attack|

|921130|HTTP Response Splitting Attack|

|921140|HTTP Header Injection Attack via headers|

|921150|HTTP Header Injection Attack via payload (CR/LF detected)|

|921160|HTTP Header Injection Attack via payload (CR/LF and header-name detected)|

|921151|HTTP Header Injection Attack via payload (CR/LF detected)|

|921170|HTTP Parameter Pollution|

|921180|HTTP Parameter Pollution (%@{TX.1})|

### <a name="crs930-30"></a> REQUEST-930-APPLICATION-ATTACK-LFI

|RuleId|Description|

|---|---|

|930100|Path Traversal Attack (/../)|

|930110|Path Traversal Attack (/../)|

|930120|OS File Access Attempt|

|930130|Restricted File Access Attempt|

### <a name="crs931-30"></a> REQUEST-931-APPLICATION-ATTACK-RFI

|RuleId|Description|

|---|---|

|931100|Possible Remote File Inclusion (RFI) Attack = URL Parameter using IP Address|

|931110|Possible Remote File Inclusion (RFI) Attack = Common RFI Vulnerable Parameter Name used w/URL Payload|

|931120|Possible Remote File Inclusion (RFI) Attack = URL Payload Used w/Trailing Question Mark Character (?)|

|931130|Possible Remote File Inclusion (RFI) Attack = Off-Domain Reference/Link|

### <a name="crs932-30"></a> REQUEST-932-APPLICATION-ATTACK-RCE

|RuleId|Description|

|---|---|

|932100|Remote Command Execution: Unix Command Injection|

|932105|Remote Command Execution: Unix Command Injection|

|932110|Remote Command Execution: Windows Command Injection|

|932115|Remote Command Execution: Windows Command Injection|

|932120|Remote Command Execution = Windows PowerShell Command Found|

|932130|**Application Gateway WAF v2**: Remote Command Execution: Unix Shell Expression or Confluence Vulnerability (CVE-2022-26134) or Text4Shell ([CVE-2022-42889](https://nvd.nist.gov/vuln/detail/CVE-2022-42889)) Found<br><br>**Application Gateway WAF v1**: Remote Command Execution: Unix Shell Expression|

|932140|Remote Command Execution = Windows FOR/IF Command Found|

|932150|Remote Command Execution: Direct Unix Command Execution|

|932160|Remote Command Execution = Unix Shell Code Found|

|932170|Remote Command Execution = Shellshock (CVE-2014-6271)|

|932171|Remote Command Execution = Shellshock (CVE-2014-6271)|

### <a name="crs933-30"></a> REQUEST-933-APPLICATION-ATTACK-PHP

|RuleId|Description|

|---|---|

|933100|PHP Injection Attack = Opening/Closing Tag Found|

|933110|PHP Injection Attack = PHP Script File Upload Found|

|933120|PHP Injection Attack = Configuration Directive Found|

|933130|PHP Injection Attack = Variables Found|

|933140|PHP Injection Attack: I/O Stream Found|

|933150|PHP Injection Attack = High-Risk PHP Function Name Found|

|933160|PHP Injection Attack = High-Risk PHP Function Call Found|

|933170|PHP Injection Attack: Serialized Object Injection|

|933180|PHP Injection Attack = Variable Function Call Found|

|933151|PHP Injection Attack = Medium-Risk PHP Function Name Found|

|933131|PHP Injection Attack = Variables Found|

|933161|PHP Injection Attack = Low-Value PHP Function Call Found|

|933111|PHP Injection Attack = PHP Script File Upload Found|

### <a name="crs941-30"></a> REQUEST-941-APPLICATION-ATTACK-XSS

|RuleId|Description|

|---|---|

|941100|XSS Attack Detected via libinjection|

|941110|XSS Filter - Category 1 = Script Tag Vector|

|941120|XSS Filter - Category 2: Event Handler Vector|

|941130|XSS Filter - Category 3 = Attribute Vector|

|941140|XSS Filter - Category 4 = JavaScript URI Vector|

|941150|XSS Filter - Category 5 = Disallowed HTML Attributes|

|941160|NoScript XSS InjectionChecker: HTML Injection|

|941170|NoScript XSS InjectionChecker: Attribute Injection|

|941180|Node-Validator Blocklist Keywords|

|941190|XSS using style sheets|

|941200|XSS using VML frames|

|941210|XSS using obfuscated JavaScript or Text4Shell ([CVE-2022-42889](https://nvd.nist.gov/vuln/detail/CVE-2022-42889))|

|941220|XSS using obfuscated VB Script|

|941230|XSS using 'embed' tag|

|941240|XSS using 'import' or 'implementation' attribute|

|941250|IE XSS Filters - Attack Detected|

|941260|XSS using 'meta' tag|

|941270|XSS using 'link' href|

|941280|XSS using 'base' tag|

|941290|XSS using 'applet' tag|

|941300|XSS using 'object' tag|

|941310|US-ASCII Malformed Encoding XSS Filter - Attack Detected|

|941330|IE XSS Filters - Attack Detected|

|941340|IE XSS Filters - Attack Detected|

|941350|UTF-7 Encoding IE XSS - Attack Detected|

|941320|Possible XSS Attack Detected - HTML Tag Handler|

### <a name="crs942-30"></a> REQUEST-942-APPLICATION-ATTACK-SQLI

|RuleId|Description|

|---|---|

|942100|SQL Injection Attack Detected via libinjection|

|942110|SQL Injection Attack: Common Injection Testing Detected|

|942120|SQL Injection Attack: SQL Operator Detected|

|942130|SQL Injection Attack: SQL Tautology Detected|

|942140|SQL Injection Attack = Common DB Names Detected|

|942160|Detects blind sqli tests using sleep() or benchmark()|

|942170|Detects SQL benchmark and sleep injection attempts including conditional queries|

|942180|Detects basic SQL authentication bypass attempts 1/3|

|942190|Detects MSSQL code execution and information gathering attempts|

|942200|Detects MySQL comment-/space-obfuscated injections and backtick termination|

|942210|Detects chained SQL injection attempts 1/2|

|942220|Looking for integer overflow attacks, these are taken from skipfish, except 3.0.00738585072007e-308 is the \"magic number\" crash'|

|942230|Detects conditional SQL injection attempts|

|942240|Detects MySQL charset switch and MSSQL DoS attempts|

|942250|Detects MATCH AGAINST, MERGE, and EXECUTE IMMEDIATE injections|

|942260|Detects basic SQL authentication bypass attempts 2/3|

|942270|Looking for basic SQL injection. Common attack string for MySQL, Oracle, and others|

|942280|Detects Postgres pg_sleep injection, waitfor delay attacks, and database shutdown attempts|

|942290|Finds basic MongoDB SQL injection attempts|

|942300|Detects MySQL comments, conditions, and ch(a)r injections|

|942310|Detects chained SQL injection attempts 2/2|

|942320|Detects MySQL and PostgreSQL stored procedure/function injections|

|942330|Detects classic SQL injection probings 1/2|

|942340|Detects basic SQL authentication bypass attempts 3/3|

|942350|Detects MySQL UDF injection and other data/structure manipulation attempts|

|942360|Detects concatenated basic SQL injection and SQLLFI attempts|

|942370|Detects classic SQL injection probings 2/2|

|942380|SQL Injection Attack|

|942390|SQL Injection Attack|

|942400|SQL Injection Attack|

|942150|SQL Injection Attack|

|942410|SQL Injection Attack|

|942420|Restricted SQL Character Anomaly Detection (cookies): # of special characters exceeded (8)|

|942421|Restricted SQL Character Anomaly Detection (cookies): # of special characters exceeded (3)|

|942430|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12)|

|942431|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (6)|

|942432|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (2)|

|942440|SQL Comment Sequence Detected|

|942450|SQL Hex Encoding Identified|

|942251|Detects HAVING injections|

|942460|Meta-Character Anomaly Detection Alert - Repetitive Non-Word Characters|

### <a name="crs943-30"></a> REQUEST-943-APPLICATION-ATTACK-SESSION-FIXATION

|RuleId|Description|

|---|---|

|943100|Possible Session Fixation Attack = Setting Cookie Values in HTML|

|943110|Possible Session Fixation Attack = SessionID Parameter Name with Off-Domain Referrer|

|943120|Possible Session Fixation Attack = SessionID Parameter Name with No Referrer|

# [OWASP 2.2.9 - no longer supported](#tab/owasp2)

## <a name="owasp229"></a> 2.2.9 rule sets

### <a name="crs20"></a> crs_20_protocol_violations

|RuleId|Description|

|---|---|

|960911|Invalid HTTP Request Line|

|981227|Apache Error = Invalid URI in Request|

|960912|Failed to parse request body|

|960914|Multipart request body failed strict validation|

|960915|Multipart parser detected a possible unmatched boundary|

|960016|Content-Length HTTP header isn't numeric|

|960011|GET or HEAD Request with Body Content|

|960012|POST request missing Content-Length Header|

|960902|Invalid Use of Identity Encoding|

|960022|Expect Header Not Allowed for HTTP 1.0|

|960020|Pragma Header requires Cache-Control Header for HTTP/1.1 requests|

|958291|Range = field exists and begins with 0|

|958230|Range = Invalid Last Byte Value|

|958295|Multiple/Conflicting Connection Header Data Found|

|950107|URL Encoding Abuse Attack Attempt|

|950109|Multiple URL Encoding Detected|

|950108|URL Encoding Abuse Attack Attempt|

|950801|UTF8 Encoding Abuse Attack Attempt|

|950116|Unicode Full/Half Width Abuse Attack Attempt|

|960901|Invalid character in request|

|960018|Invalid character in request|

### <a name="crs21"></a> crs_21_protocol_anomalies

|RuleId|Description|

|---|---|

|960008|Request Missing a Host Header|

|960007|Empty Host Header|

|960015|Request Missing an Accept Header|

|960021|Request Has an Empty Accept Header|

|960009|Request Missing a User Agent Header|

|960006|Empty User Agent Header|

|960904|Request Containing Content but Missing Content-Type header|

|960017|Host header is a numeric IP address|

### <a name="crs23"></a> crs_23_request_limits

|RuleId|Description|

|---|---|

|960209|Argument name too long|

|960208|Argument value too long|

|960335|Too many arguments in request|

|960341|Total arguments size exceeded|

|960342|Uploaded file size too large|

|960343|Total uploaded files size too large|

### <a name="crs30"></a> crs_30_http_policy

|RuleId|Description|

|---|---|

|960032|Method isn't allowed by policy|

|960010|Request content type isn't allowed by policy|

|960034|HTTP protocol version isn't allowed by policy|

|960035|URL file extension is restricted by policy|

|960038|HTTP header is restricted by policy|

### <a name="crs35"></a> crs_35_bad_robots

|RuleId|Description|

|---|---|

|990002|Request Indicates a Security Scanner Scanned the Site|

|990901|Request Indicates a Security Scanner Scanned the Site|

|990902|Request Indicates a Security Scanner Scanned the Site|

|990012|Rogue web site crawler|

### <a name="crs40"></a> crs_40_generic_attacks

|RuleId|Description|

|---|---|

|960024|Meta-Character Anomaly Detection Alert - Repetitive Non-Word Characters|

|950008|Injection of Undocumented ColdFusion Tags|

|950010|LDAP Injection Attack|

|950011|SSI injection Attack|

|950018|Universal PDF XSS URL Detected|

|950019|Email Injection Attack|

|950012|HTTP Request Smuggling Attack|

|950910|HTTP Response Splitting Attack|

|950911|HTTP Response Splitting Attack|

|950117|Remote File Inclusion Attack|

|950118|Remote File Inclusion Attack|

|950119|Remote File Inclusion Attack|

|950120|Possible Remote File Inclusion (RFI) Attack = Off-Domain Reference/Link|

|981133|Rule 981133|

|981134|Rule 981134|

|950009|Session Fixation Attack|

|950003|Session Fixation|

|950000|Session Fixation|

|950005|Remote File Access Attempt|

|950002|System Command Access|

|950006|System Command Injection|

|959151|PHP Injection Attack|

|958976|PHP Injection Attack|

|958977|PHP Injection Attack|

### <a name="crs41sql"></a> crs_41_sql_injection_attacks

|RuleId|Description|

|---|---|

|981231|SQL Comment Sequence Detected|

|981260|SQL Hex Encoding Identified|

|981320|SQL Injection Attack = Common DB Names Detected|

|981300|Rule 981300|

|981301|Rule 981301|

|981302|Rule 981302|

|981303|Rule 981303|

|981304|Rule 981304|

|981305|Rule 981305|

|981306|Rule 981306|

|981307|Rule 981307|

|981308|Rule 981308|

|981309|Rule 981309|

|981310|Rule 981310|

|981311|Rule 981311|

|981312|Rule 981312|

|981313|Rule 981313|

|981314|Rule 981314|

|981315|Rule 981315|

|981316|Rule 981316|

|981317|SQL SELECT Statement Anomaly Detection Alert|

|950007|Blind SQL Injection Attack|

|950001|SQL Injection Attack|

|950908|SQL Injection Attack|

|959073|SQL Injection Attack|

|981272|Detects blind sqli tests using sleep() or benchmark()|

|981250|Detects SQL benchmark and sleep injection attempts including conditional queries|

|981241|Detects conditional SQL injection attempts|

|981276|Looking for basic SQL injection. Common attack string for MySQL, Oracle, and others|

|981270|Finds basic MongoDB SQL injection attempts|

|981253|Detects MySQL and PostgreSQL stored procedure/function injections|

|981251|Detects MySQL UDF injection and other data/structure manipulation attempts|

### <a name="crs41xss"></a> crs_41_xss_attacks

|RuleId|Description|

|---|---|

|973336|XSS Filter - Category 1 = Script Tag Vector|

|973338|XSS Filter - Category 3 = JavaScript URI Vector|

|981136|Rule 981136|

|981018|Rule 981018|

|958016|Cross-site Scripting (XSS) Attack|

|958414|Cross-site Scripting (XSS) Attack|

|958032|Cross-site Scripting (XSS) Attack|

|958026|Cross-site Scripting (XSS) Attack|

|958027|Cross-site Scripting (XSS) Attack|

|958054|Cross-site Scripting (XSS) Attack|

|958418|Cross-site Scripting (XSS) Attack|

|958034|Cross-site Scripting (XSS) Attack|

|958019|Cross-site Scripting (XSS) Attack|

|958013|Cross-site Scripting (XSS) Attack|

|958408|Cross-site Scripting (XSS) Attack|

|958012|Cross-site Scripting (XSS) Attack|

|958423|Cross-site Scripting (XSS) Attack|

|958002|Cross-site Scripting (XSS) Attack|

|958017|Cross-site Scripting (XSS) Attack|

|958007|Cross-site Scripting (XSS) Attack|

|958047|Cross-site Scripting (XSS) Attack|

|958410|Cross-site Scripting (XSS) Attack|

|958415|Cross-site Scripting (XSS) Attack|

|958022|Cross-site Scripting (XSS) Attack|

|958405|Cross-site Scripting (XSS) Attack|

|958419|Cross-site Scripting (XSS) Attack|

|958028|Cross-site Scripting (XSS) Attack|

|958057|Cross-site Scripting (XSS) Attack|

|958031|Cross-site Scripting (XSS) Attack|

|958006|Cross-site Scripting (XSS) Attack|

|958033|Cross-site Scripting (XSS) Attack|

|958038|Cross-site Scripting (XSS) Attack|

|958409|Cross-site Scripting (XSS) Attack|

|958001|Cross-site Scripting (XSS) Attack|

|958005|Cross-site Scripting (XSS) Attack|

|958404|Cross-site Scripting (XSS) Attack|

|958023|Cross-site Scripting (XSS) Attack|

|958010|Cross-site Scripting (XSS) Attack|

|958411|Cross-site Scripting (XSS) Attack|

|958422|Cross-site Scripting (XSS) Attack|

|958036|Cross-site Scripting (XSS) Attack|

|958000|Cross-site Scripting (XSS) Attack|

|958018|Cross-site Scripting (XSS) Attack|

|958406|Cross-site Scripting (XSS) Attack|

|958040|Cross-site Scripting (XSS) Attack|

|958052|Cross-site Scripting (XSS) Attack|

|958037|Cross-site Scripting (XSS) Attack|

|958049|Cross-site Scripting (XSS) Attack|

|958030|Cross-site Scripting (XSS) Attack|

|958041|Cross-site Scripting (XSS) Attack|

|958416|Cross-site Scripting (XSS) Attack|

|958024|Cross-site Scripting (XSS) Attack|

|958059|Cross-site Scripting (XSS) Attack|

|958417|Cross-site Scripting (XSS) Attack|

|958020|Cross-site Scripting (XSS) Attack|

|958045|Cross-site Scripting (XSS) Attack|

|958004|Cross-site Scripting (XSS) Attack|

|958421|Cross-site Scripting (XSS) Attack|

|958009|Cross-site Scripting (XSS) Attack|

|958025|Cross-site Scripting (XSS) Attack|

|958413|Cross-site Scripting (XSS) Attack|

|958051|Cross-site Scripting (XSS) Attack|

|958420|Cross-site Scripting (XSS) Attack|

|958407|Cross-site Scripting (XSS) Attack|

|958056|Cross-site Scripting (XSS) Attack|

|958011|Cross-site Scripting (XSS) Attack|

|958412|Cross-site Scripting (XSS) Attack|

|958008|Cross-site Scripting (XSS) Attack|

|958046|Cross-site Scripting (XSS) Attack|

|958039|Cross-site Scripting (XSS) Attack|

|958003|Cross-site Scripting (XSS) Attack|

|973300|Possible XSS Attack Detected - HTML Tag Handler|

|973301|XSS Attack Detected|

|973302|XSS Attack Detected|

|973303|XSS Attack Detected|

|973304|XSS Attack Detected|

|973305|XSS Attack Detected|

|973306|XSS Attack Detected|

|973307|XSS Attack Detected|

|973308|XSS Attack Detected|

|973309|XSS Attack Detected|

|973311|XSS Attack Detected|

|973313|XSS Attack Detected|

|973314|XSS Attack Detected|

|973331|IE XSS Filters - Attack Detected|

|973315|IE XSS Filters - Attack Detected|

|973330|IE XSS Filters - Attack Detected|

|973327|IE XSS Filters - Attack Detected|

|973326|IE XSS Filters - Attack Detected|

|973346|IE XSS Filters - Attack Detected|

|973345|IE XSS Filters - Attack Detected|

|973324|IE XSS Filters - Attack Detected|

|973323|IE XSS Filters - Attack Detected|

|973348|IE XSS Filters - Attack Detected|

|973321|IE XSS Filters - Attack Detected|

|973320|IE XSS Filters - Attack Detected|

|973318|IE XSS Filters - Attack Detected|

|973317|IE XSS Filters - Attack Detected|

|973329|IE XSS Filters - Attack Detected|

|973328|IE XSS Filters - Attack Detected|

### <a name="crs42"></a> crs_42_tight_security

|RuleId|Description|

|---|---|

|950103|Path Traversal Attack|

### <a name="crs45"></a> crs_45_trojans

|RuleId|Description|

|---|---|

|950110|Backdoor access|

|950921|Backdoor access|

|950922|Backdoor access|

----

## Related content

- [Customize Web Application Firewall rules using the Azure portal](application-gateway-customize-waf-rules-portal.md)

- [Learn more about Azure network security](../../networking/security/index.yml)


# Waf Front Door Policy Configure Bot Protection

# Configure bot protection for Web Application Firewall

**Applies to:** :heavy_check_mark: Front Door Premium

The Azure Web Application Firewall (WAF) for Front Door provides bot rules to identify good bots and protect from bad bots. For more information on the bot protection rule set, see [Bot protection rule set](afds-overview.md#bot-protection-rule-set).

This article shows how to enable bot protection rules on the Azure Front Door Premium tier.

## Prerequisites

Create a basic WAF policy for Front Door by following the instructions described in [Create a WAF policy for Azure Front Door by using the Azure portal](waf-front-door-create-portal.md).

## Enable the bot protection rule set

1. In the Azure portal, navigate to your WAF policy.

1. Select **Managed rules**, then select **Assign**.

1. In the **Additional rule set** drop-down list, select the version of the bot protection rule set that you want to use. It's usually a good practice to use the most recent version of the rule set.

1. Select **Save**.

## Get your WAF policy's current configuration

Use the [Get-AzFrontDoorWafPolicy](/powershell/module/az.frontdoor/get-azfrontdoorwafpolicy) cmdlet to retrieve the current configuration of your WAF policy. Ensure that you use the correct resource group name and WAF policy name for your own environment.

```azurepowershell

$frontDoorWafPolicy = Get-AzFrontDoorWafPolicy `

-ResourceGroupName 'FrontDoorWafPolicy' `

-Name 'WafPolicy'

```

## Add the bot protection rule set

Use the [New-AzFrontDoorWafManagedRuleObject](/powershell/module/az.frontdoor/new-azfrontdoorwafmanagedruleobject) cmdlet to select the bot protection rule set, including the version of the rule set. Then, add the rule set to the WAF's configuration.

The example below adds version 1.0 of the bot protection rule set to the WAF's configuration.

```azurepowershell

$botProtectionRuleSet = New-AzFrontDoorWafManagedRuleObject `

-Type 'Microsoft_BotManagerRuleSet' `

-Version '1.0'

$frontDoorWafPolicy.ManagedRules.Add($botProtectionRuleSet)

```

## Apply the configuration

Use the [Update-AzFrontDoorWafPolicy](/powershell/module/az.frontdoor/update-azfrontdoorwafpolicy) cmdlet to update your WAF policy to include the configuration you created above.

```azurepowershell

$frontDoorWafPolicy | Update-AzFrontDoorWafPolicy

```

## Enable the bot protection rule set

Use the [az network front-door waf-policy managed-rules add](/cli/azure/network/front-door/waf-policy/managed-rules#az-network-front-door-waf-policy-managed-rules-add) command to update your WAF policy to add the bot protection rule set.

The example below adds version 1.0 of the bot protection rule set to the WAF. Ensure that you use the correct resource group name and WAF policy name for your own environment.

```azurecli

az network front-door waf-policy managed-rules add \

--resource-group FrontDoorWafPolicy \

--policy-name WafPolicy \

--type Microsoft_BotManagerRuleSet \

--version 1.0

```

The following example Bicep file shows how to do the following steps:

- Create a Front Door WAF policy.

- Enable version 1.0 of the bot protection rule set.

```bicep

param wafPolicyName string = 'WafPolicy'

@description('The mode that the WAF should be deployed using. In "Prevention" mode, the WAF will block requests it detects as malicious. In "Detection" mode, the WAF will not block requests and will simply log the request.')

@allowed([

'Detection'

'Prevention'

])

param wafMode string = 'Prevention'

resource wafPolicy 'Microsoft.Network/frontDoorWebApplicationFirewallPolicies@2022-05-01' = {

name: wafPolicyName

location: 'Global'

sku: {

name: 'Premium_AzureFrontDoor'

}

properties: {

policySettings: {

enabledState: 'Enabled'

mode: wafMode

}

managedRules: {

managedRuleSets: [

{

ruleSetType: 'Microsoft_BotManagerRuleSet'

ruleSetVersion: '1.0'

}

]

}

}

}

```

## Next steps

- Learn how to [monitor WAF](waf-front-door-monitor.md).


# Waf Front Door Configure Custom Response Code

# Configure a custom response for Azure Web Application Firewall

By default, when Azure Front Door Web Application Firewall (WAF) blocks a request because of a matched rule, it returns a 403 status code with the message "The request is blocked." The default message also includes the tracking reference string that's used to link to [log entries](./waf-front-door-monitor.md) for the request.

In this article, you learn how to configure a custom response status code and a custom message with a reference string for your use case using the Azure portal, PowerShell, or the Azure CLI.

## Prerequisites

# [**Portal**](#tab/portal)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- Sign in to the [Azure portal](https://portal.azure.com) with your Azure account.

# [**PowerShell**](#tab/powershell)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- Azure Cloud Shell or Azure PowerShell.

The steps in this article run the Azure PowerShell cmdlets interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the cmdlets in the Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code and then paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure PowerShell locally](/powershell/azure/install-azure-powershell) to run the cmdlets. This article requires the Azure PowerShell module. If you run PowerShell locally, sign in to Azure using the [Connect-AzAccount](/powershell/module/az.accounts/connect-azaccount) cmdlet.

# [**Azure CLI**](#tab/cli)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- Azure Cloud Shell or Azure CLI.

The steps in this article run the Azure CLI commands interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the commands in the Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code, and paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure CLI locally](/cli/azure/install-azure-cli) to run the commands. This article requires the Azure CLI version 2.67.0 or higher and  **front-door** extension. Run [az --version](/cli/azure/reference-index#az-version) command to find the installed version. If you run Azure CLI locally, sign in to Azure using the [az login](/cli/azure/reference-index#az-login) command.

---

## Configure a custom response status code and message

# [**Portal**](#tab/portal)

To customize the response status code and body, follow these steps:

1. Go to your Front Door WAF policy in the Azure portal.

1. Under **Settings**, select **Policy settings**.

1. Enter the custom response status code and response body in the **Block response status code** and **Block response body** boxes, respectively.

> [!NOTE]

> The [JavaScript challenge](../waf-javascript-challenge.md) and [CAPTCHA](captcha-challenge.md) features are available only in WAF policies on the Azure Front Door Premium tier.

1. Select **Save**.

# [**PowerShell**](#tab/powershell)

To customize the response status code and body, use [Update-AzFrontDoorWafPolicy](/powershell/module/az.frontdoor/Update-AzFrontDoorWafPolicy) cmdlet.

```azurepowershell-interactive

# Update WAF policy settings to customize response body and status code

Update-AzFrontDoorWafPolicy `

-Name 'myWAFPolicy' `

-ResourceGroupName 'myResourceGroup' `

-RequestBodyCheck 'Enabled' `

-RedirectUrl 'https://learn.microsoft.com/en-us/azure/web-application-firewall/' `

-CustomBlockResponseStatusCode '403' `

-CustomBlockResponseBody '<html><head><title>WAF Demo</title></head><body><p><h1><strong>WAF Custom Response Page</strong></h1></p><p>Please contact us with this information:<br>{{azure-ref}}</p></body></html>'

```

# [**Azure CLI**](#tab/cli)

To customize the response status code and body, use [az network front-door waf-policy update](/cli/azure/network/front-door/waf-policy#az-network-front-door-waf-policy-update) command.

```azurecli-interactive

# Update WAF policy settings to customize response body and status code

az network front-door waf-policy update \

--name 'myWAFPolicy' \

--resource-group 'myResourceGroup' \

--request-body-check 'Enabled' \

--redirect-url 'https://learn.microsoft.com/en-us/azure/web-application-firewall/' \

--custom-block-response-status-code '403' \

--custom-block-response-body 'PGh0bWw+PGhlYWQ+PHRpdGxlPldBRiBEZW1vPC90aXRsZT48L2hlYWQ+PGJvZHk+PHA+PGgxPjxzdHJvbmc+V0FGIEN1c3RvbSBSZXNwb25zZSBQYWdlPC9zdHJvbmc+PC9oMT48L3A+PHA+UGxlYXNlIGNvbnRhY3QgdXMgd2l0aCB0aGlzIGluZm9ybWF0aW9uOjxicj57e2F6dXJlLXJlZn19PC9wPjwvYm9keT48L2h0bWw+'

```

> [!NOTE]

> The value of the `--custom-block-response-body` parameter must be a **base64** encoded string.

---

In the previous example, the response code was kept as 403 with a custom message: "*Please contact us with this information:*".

> [!NOTE]

> `{{azure-ref}}` inserts the unique reference string in the response body. The value matches the TrackingReference field in the `FrontDoorAccessLog` and `FrontDoorWebApplicationFirewallLog` logs.

> [!IMPORTANT]

> If you leave the block response body blank, the WAF returns a ***403 Forbidden*** response for normal WAF blocks and a ***429 Too many requests*** for rate limit blocks.

## Next step

> [!div class="nextstepaction"]

> [Configure a Web Application Firewall rate-limit rule](../afds/waf-front-door-rate-limit-configure.md)


# Web Application Firewall Logs

# Resource logs for Azure Web Application Firewall

**Applies to:** :heavy_check_mark: Application Gateway

You can monitor Web Application Firewall resources using logs. You can save performance, access, and other data or consume it from a resource for monitoring purposes.

[!INCLUDE [updated-for-az](~/reusable-content/ce-skilling/azure/includes/updated-for-az.md)]

## Diagnostic logs

You can use different types of logs in Azure to manage and troubleshoot application gateways. You can access some of these logs through the portal. All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Azure Monitor logs](/previous-versions/azure/azure-monitor/insights/azure-networking-analytics), Excel, and Power BI. You can learn more about the different types of logs from the following list:

* **Activity log**: You can use [Azure activity logs](/azure/azure-monitor/essentials/activity-log) to view all operations that are submitted to your Azure subscription, and their status. Activity log entries are collected by default, and you can view them in the Azure portal.

* **Access Resource log**: You can use this log to view Application Gateway access patterns and analyze important information. This includes the caller's IP, requested URL, response latency, return code, and bytes in and out. This log contains individual records for each request and associates that request to the unique Application Gateway that processed the request. Unique Application Gateway instances can be identified by the property instanceId.

* **Performance Resource log**: You can use this log to view how Application Gateway instances are performing. This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count. A performance log is collected every 60 seconds. The Performance log is available only for the v1 SKU. For the v2 SKU, use [Metrics](../../application-gateway/application-gateway-metrics.md) for performance data.

* **Firewall Resource log**: You can use this log to view the requests that are logged through either detection or prevention mode of an application gateway that is configured with the web application firewall.

> [!NOTE]

> Logs are available only for resources deployed in the Azure Resource Manager deployment model. You cannot use logs for resources in the classic deployment model. For a better understanding of the two models, see the [Understanding Resource Manager deployment and classic deployment](../../azure-resource-manager/management/deployment-models.md) article.

You have three options for storing your logs:

* **Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.

* **Event hubs**: Event hubs are a great option for integrating with other security information and event management (SIEM) tools to get alerts on your resources.

* **Azure Monitor logs**: Azure Monitor logs is best used for general real-time monitoring of your application or looking at trends.

### Enable logging through PowerShell

Activity logging is automatically enabled for every Resource Manager resource. You must enable access and performance logging to start collecting the data available through those logs. To enable logging, use the following steps:

1. Note your storage account's resource ID, where the log data is stored. This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>. You can use any storage account in your subscription. You can use the Azure portal to find this information.

![Portal: resource ID for storage account](../media/web-application-firewall-logs/diagnostics1.png)

2. Note your application gateway's resource ID for which logging is enabled. This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>. You can use the portal to find this information.

![Portal: resource ID for application gateway](../media/web-application-firewall-logs/diagnostics2.png)

3. Enable resource logging by using the following PowerShell cmdlet:

```powershell

Set-AzDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true

```

> [!TIP]

>Activity logs do not *require* a separate storage account. The use of storage for access and performance logging incurs service charges.

### Enable logging through the Azure portal

1. In the Azure portal, find your resource and select **Diagnostic settings**.

For Application Gateway, three logs are available:

* Access log

* Performance log

* Firewall log

2. Select **Add diagnostic setting**.

3. The **Diagnostic setting** page provides the settings for the resource logs. In this example, Log Analytics stores the logs. You can also use an event hub, a storage account, or a partner solution to save the resource logs.

5. Type a name for the settings, confirm the settings, and select **Save**.

## Activity log

Azure generates the activity log by default. The logs are preserved for 90 days in the Azure event logs store. Learn more about these logs by reading the [View events and activity log](/azure/azure-monitor/essentials/activity-log) article.

## Access log

The access log is generated only if you've enabled it on each Application Gateway instance, as detailed in the preceding steps. The data is stored in the storage account that you specified when you enabled the logging. Each access of Application Gateway is logged in JSON format, as shown in the following example for v1:

|Value  |Description  |

|---------|---------|

|instanceId     | Application Gateway instance that served the request.        |

|clientIP     | Originating IP for the request.        |

|clientPort     | Originating port for the request.       |

|httpMethod     | HTTP method used by the request.       |

|requestUri     | URI of the received request.        |

|RequestQuery     | **Server-Routed**: Back-end pool instance that was sent the request.</br>**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for the request. It can be used to troubleshoot traffic issues on the back-end servers. </br>**SERVER-STATUS**: HTTP response code that Application Gateway received from the back end.       |

|UserAgent     | User agent from the HTTP request header.        |

|httpStatus     | HTTP status code returned to the client from Application Gateway.       |

|httpVersion     | HTTP version of the request.        |

|receivedBytes     | Size of packet received, in bytes.        |

|sentBytes| Size of packet sent, in bytes.|

|timeTaken| Length of time (in milliseconds) that it takes for a request to be processed and its response to be sent. This is calculated as the interval from the time when Application Gateway receives the first byte of an HTTP request to the time when the response send operation finishes. It's important to note that the Time-Taken field usually includes the time that the request and response packets are traveling over the network. |

|sslEnabled| Whether communication to the back-end pools used TLS/SSL. Valid values are on and off.|

|host| The hostname with which the request has been sent to the backend server. If backend hostname is being overridden, this name will reflect that.|

|originalHost| The hostname with which the request was received by the Application Gateway from the client.|

```json

{

"resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",

"operationName": "ApplicationGatewayAccess",

"timestamp": "2017-04-26T19:27:38Z",

"category": "ApplicationGatewayAccessLog",

"properties": {

"instanceId": "ApplicationGatewayRole_IN_0",

"clientIP": "203.0.113.97",

"clientPort": 46886,

"httpMethod": "GET",

"requestUri": "/phpmyadmin/scripts/setup.php",

"requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e&SERVER-STATUS=404",

"userAgent": "-",

"httpStatus": 404,

"httpVersion": "HTTP/1.0",

"receivedBytes": 65,

"sentBytes": 553,

"timeTaken": 205,

"sslEnabled": "off",

"host": "www.contoso.com",

"originalHost": "www.contoso.com"

}

}

```

For Application Gateway and WAF v2, the logs show a little more information:

|Value  |Description  |

|---------|---------|

|instanceId     | Application Gateway instance that served the request.        |

|clientIP     | Originating IP for the request.        |

|clientPort     | Originating port for the request.       |

|httpMethod     | HTTP method used by the request.       |

|requestUri     | URI of the received request.        |

|UserAgent     | User agent from the HTTP request header.        |

|httpStatus     | HTTP status code returned to the client from Application Gateway.       |

|httpVersion     | HTTP version of the request.        |

|receivedBytes     | Size of packet received, in bytes.        |

|sentBytes| Size of packet sent, in bytes.|

|timeTaken| Length of time (in milliseconds) that it takes for a request to be processed and its response to be sent. This is calculated as the interval from the time when Application Gateway receives the first byte of an HTTP request to the time when the response send operation finishes. It's important to note that the Time-Taken field usually includes the time that the request and response packets are traveling over the network. |

|sslEnabled| Whether communication to the back-end pools used TLS. Valid values are on and off.|

|sslCipher| Cipher suite being used for TLS communication (if TLS is enabled).|

|sslProtocol| TLS protocol being used (if TLS is enabled).|

|serverRouted| The backend server that application gateway routes the request to.|

|serverStatus| HTTP status code of the backend server.|

|serverResponseLatency| Latency of the response from the backend server.|

|host| Address listed in the host header of the request.|

```json

{

"resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",

"operationName": "ApplicationGatewayAccess",

"time": "2017-04-26T19:27:38Z",

"category": "ApplicationGatewayAccessLog",

"properties": {

"instanceId": "appgw_1",

"clientIP": "203.0.113.97",

"clientPort": 46886,

"httpMethod": "GET",

"requestUri": "/phpmyadmin/scripts/setup.php",

"userAgent": "-",

"httpStatus": 404,

"httpVersion": "HTTP/1.0",

"receivedBytes": 65,

"sentBytes": 553,

"timeTaken": 205,

"sslEnabled": "off",

"sslCipher": "",

"sslProtocol": "",

"serverRouted": "104.41.114.59:80",

"serverStatus": "200",

"serverResponseLatency": "0.023",

"host": "www.contoso.com",

}

}

```

## Performance log

The performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in the preceding steps. The data is stored in the storage account that you specified when you enabled the logging. The performance log data is generated in 1-minute intervals. It is available only for the v1 SKU. For the v2 SKU, use [Metrics](../../application-gateway/application-gateway-metrics.md) for performance data. The following data is logged:

|Value  |Description  |

|---------|---------|

|instanceId     |  Application Gateway instance for which performance data is being generated. For a multiple-instance application gateway, there is one row per instance.        |

|healthyHostCount     | Number of healthy hosts in the back-end pool.        |

|unHealthyHostCount     | Number of unhealthy hosts in the back-end pool.        |

|requestCount     | Number of requests served.        |

|latency | Average latency (in milliseconds) of requests from the instance to the back end that serves the requests. |

|failedRequestCount| Number of failed requests.|

|throughput| Average throughput since the last log, measured in bytes per second.|

```json

{

"resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",

"operationName": "ApplicationGatewayPerformance",

"time": "2016-04-09T00:00:00Z",

"category": "ApplicationGatewayPerformanceLog",

"properties":

{

"instanceId":"ApplicationGatewayRole_IN_1",

"healthyHostCount":"4",

"unHealthyHostCount":"0",

"requestCount":"185",

"latency":"0",

"failedRequestCount":"0",

"throughput":"119427"

}

}

```

> [!NOTE]

> Latency is calculated from the time when the first byte of the HTTP request is received to the time when the last byte of the HTTP response is sent. It's the sum of the Application Gateway processing time plus the network cost to the back end, plus the time that the back end takes to process the request.

## Firewall log

The firewall log is generated only if you have enabled it for each application gateway, as detailed in the preceding steps. This log also requires that the web application firewall is configured on an application gateway. The data is stored in the destination that you specified when you enabled the logging. The following data is logged:

# [Application Gateway](#tab/AppGW)

## <a name="AppGW"></a> Application Gateway

### <a name="AppGW-Format"></a> Log Format

|Value  |Description  |

|---------|---------|

|instanceId     | Application Gateway instance for which firewall data is being generated. For a multiple-instance application gateway, there is one row per instance.         |

|clientIp     |   Originating IP for the request.      |

|requestUri     | URL of the received request.       |

|ruleSetType     | Rule set type. The available value is OWASP.        |

|ruleSetVersion     | Rule set version used. Available values are 2.2.9 and 3.0.     |

|ruleId     | Rule ID of the triggering event.        |

|message     | User-friendly message for the triggering event. More details are provided in the details section.        |

|action     |**Policy Mode:** Detection</br>- **Detected** - This is the only action for the WAF when in detection mode. All the conditions for a given rule were matched and the request was logged then passed to the backend.</br></br>**Policy Mode:** Prevention</br>   - **Allowed** - All conditions were matched for a given rule and the request was passed to the backend.</br>   - **Blocked** - All of the conditions were matched for a given rule and the request was blocked.</br>   - **Matched** - One/more conditions were matched for a given rule, but the decision to block or pass the request will need further evaluation and will be evaluated based on the final anomaly scoring rule.<br><br>**Policy Mode:** JS challenge<br>- **JSChallengeIssued**: Issued due to missing/invalid challenge clearance, missing answer.<br><br>This log is created when a client requests access to a web application for the first time and has not been challenged previously. This client receives the JS challenge page and proceeds to compute the JS challenge. Upon successful computation, the client is granted the validity cookie.<br><br>- **JSChallengePass**: Passed due to valid challenge answer.<br><br>This log is created when a client solves the JS challenge and resubmits the request with the correct answer. In this case, Azure WAF validates the cookie and proceeds to process the remaining rules without generating another JS challenge.<br><br>- **JSChallengeValid**: Logged/passthrough due to valid challenge<br><br>This log is created when a client has previously solved a challenge. In this case, Azure WAF logs the request and proceeds to process the remaining rules.<br><br>- **JSChallengeBlock**: Blocked<br><br>This log is created when a JS challenge computation fails.   |

|site     | Site for which the log was generated. Currently, only Global is listed because rules are global.|

|details     | Details of the triggering event.        |

|details.message     | Description of the rule.        |

|details.data     | Specific data found in request that matched the rule.         |

|details.file     | Configuration file that contained the rule.        |

|details.line     | Line number in the configuration file that triggered the event.       |

|hostname   | Hostname or IP address of the Application Gateway.    |

|transactionId  | Unique ID for a given transaction which helps group multiple rule violations that occurred within the same request.   |

|policyId   | Unique ID of the Firewall Policy associated with the Application Gateway, Listener, or Path.   |

|policyScope    | The location of the policy - values can be "Global", "Listener", or "Location".   |

|policyScopeName   | The name of the object where the policy is applied.    |

### <a name="AppGW-Example"></a> Example

```json

{

"resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",

"operationName": "ApplicationGatewayFirewall",

"time": "2017-03-20T15:52:09.1494499Z",

"category": "ApplicationGatewayFirewallLog",

"properties": {

"instanceId": "ApplicationGatewayRole_IN_0",

"clientIp": "203.0.113.147",

"requestUri": "/",

"ruleSetType": "OWASP",

"ruleSetVersion": "3.0",

"ruleId": "920350",

"ruleGroup": "920-PROTOCOL-ENFORCEMENT",

"message": "Host header is a numeric IP address",

"action": "Matched",

"site": "Global",

"details": {

"message": "Warning. Pattern match \"^[\\\\d.:]+$\" at REQUEST_HEADERS:Host ....",

"data": "127.0.0.1",

"file": "rules/REQUEST-920-PROTOCOL-ENFORCEMENT.conf",

"line": "791"

},

"hostname": "127.0.0.1",

"transactionId": "16861477007022634343",

"policyId": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/drewRG/providers/Microsoft.Network/ApplicationGatewayWebApplicationFirewallPolicies/perListener",

"policyScope": "Listener",

"policyScopeName": "httpListener1"

}

}

}

```

# [Application Gateway for Containers](#tab/AGC)

## <a name="AGC"></a> Application Gateway for Containers

| Value            | Description                                                                                                                                                                                                            |

|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

| TimeGenerated    | Time (UTC) when the log was created.                                                                                                                                                                                   |

| OperationName    | Name of the operation.                                                                                                                                                                                                 |

| InstanceId       | Application Gateway instance for which firewall data is being generated. For a multiple-instance application gateway, there is one row per instance.                                                                   |

| ClientIp         | Originating IP for the request.                                                                                                                                                                                        |

| ClientPort       | Originating port for the request.                                                                                                                                                                                      |

| Action           | Action taken on the request. Available values are Blocked and Allowed (for custom rules), Matched (when a rule matches a part of the request), and Detected and Blocked (these are both for mandatory rules).          |

| Message          | User-friendly message for the triggering event. More details are provided in the details section.                                                                                                                      |

| DetailedMessage  | Description of the rule for the triggered event.                                                                                                                                                                       |

| DetailedData     | Specific data found in request that matched the rule for the triggered event.                                                                                                                                          |

| FileDetails      | Configuration file that contained the rule for the triggered event.                                                                                                                                                    |

| LineDetails      | Line number in the configuration file that triggered the event.                                                                                                                                                        |

| Hostname         | Hostname or IP address of the Application Gateway.                                                                                                                                                                     |

| PolicyId         | Resource ID of the web application firewall policy.                                                                                                                                                                    |

| PolicyScope      | A named scope consisting of Kubernetes resource references the scope is applied to.                                                                                                                                    |

| PolicyScopeName  | The name to the type of scope assignment the web application firewall policy is assigned to.                                                                                                                           |

| RequestUri       | URL of the received request.                                                                                                                                                                                           |

| RuleSetType      | Rule set type. The available value is Microsoft_DefaultRuleSet or Microsoft_BotManagerRuleSet.                                                                                                                         |

| RuleSetVersion   | Rule set version used for Microsoft_DefaultRuleSet or Microsoft_BotManagerRuleSet.                                                                                                                                     |

| RuleId           | Rule ID of the triggering event.                                                                                                                                                                                       |

| TrackingId       | Generated guid by Application Gateway

### <a name="AGC-Format"></a> Log Format

```json

{

"timeStamp": "2025-06-17T20:06:05+00:00",

"resourceId": "/SUBSCRIPTIONS/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/RESOURCEGROUPS/YYYYYY/PROVIDERS/MICROSOFT.SERVICENETWORKING/TRAFFICCONTROLLERS/ZZZZZZZ",

"operationName": "TrafficControllerFirewall",

"category": "TrafficControllerFirewallLog",

"properties": {

"instanceId": "8a02ae47-8435-4f3d-84a5-6f5ded3763f5",

"clientIp": "xxx.xxx.xxx.xxx",

"requestUri": "\/?1=1=1",

"ruleSetType": "Microsoft_DefaultRuleSet",

"ruleSetVersion": "2.1",

"ruleId": "949110",

"ruleGroup": "BLOCKING-EVALUATION",

"message": "Inbound Anomaly Score Exceeded (Total Score: 5)",

"action": "Blocked",

"details": {

"message": "Greater and Equal to Tx:inbound_anomaly_score_threshold at TX:anomaly_score.",

"data": "",

"file": "BLOCKING-EVALUATION.conf",

"line": "36"

},

"hostName": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.fzXX.alb.azure.com",

"trackingId": "0ef125db-7fb7-48a0-b3fe-03fe0ffed873",

"policyId": "/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/YYYYYY/providers/Microsoft.Network/ApplicationGatewayWebApplicationFirewallPolicies/ZZZZZZZ",

"policyScope": "HTTPRoute-test-infra-contoso-waf-route-rule-0-match-0-waf.fzXX.alb.azure.com",

"policyScopeName": "Route",

"engine": "Azwaf"

},

"location": "northcentralus"

}

```

----

## View and analyze the activity log

You can view and analyze activity log data by using any of the following methods:

* **Azure tools**: Retrieve information from the activity log through Azure PowerShell, the Azure CLI, the Azure REST API, or the Azure portal. Step-by-step instructions for each method are detailed in the [Activity operations with Resource Manager](/azure/azure-monitor/essentials/activity-log) article.

* **Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free. By using the [Power BI template apps](/power-bi/service-template-apps-overview), you can analyze your data.

## View and analyze the access, performance, and firewall logs

[Azure Monitor logs](/previous-versions/azure/azure-monitor/insights/azure-networking-analytics) can collect the counter and event log files from your Blob storage account. It includes visualizations and powerful search capabilities to analyze your logs.

You can also connect to your storage account and retrieve the JSON log entries for access and performance logs. After you download the JSON files, you can convert them to CSV and view them in Excel, Power BI, or any other data-visualization tool.

> [!TIP]

> If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.

>

>

#### Analyzing Access logs through GoAccess

We have published a Resource Manager template that installs and runs the popular [GoAccess](https://goaccess.io/) log analyzer for Application Gateway Access Logs. GoAccess provides valuable HTTP traffic statistics such as Unique Visitors, Requested Files, Hosts, Operating Systems, Browsers, HTTP Status codes and more. For more details, please see the [Readme file in the Resource Manager template folder in GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/demos/application-gateway-logviewer-goaccess).

## Next steps

* Visualize counter and event logs by using [Azure Monitor logs](/previous-versions/azure/azure-monitor/insights/azure-networking-analytics).

* [Visualize your Azure activity log with Power BI](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) blog post.

* [View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.


# Waf Copilot

# Azure Web Application Firewall integration in Microsoft Security Copilot

Microsoft Security Copilot is a cloud-based AI platform that provides natural language copilot experience. It can help support security professionals in different scenarios, like incident response, threat hunting, and intelligence gathering. For more information, see [What is Microsoft Security Copilot?](/security-copilot/microsoft-security-copilot)

Azure Web Application Firewall (WAF) integration in Microsoft Security Copilot enables deep investigation of Azure WAF events. It can help you investigate WAF logs triggered by Azure WAF in a matter of minutes and provide related attack vectors using natural language responses at machine speed. It provides visibility into your environment’s threat landscape. It allows you to retrieve a list of most frequently triggered WAF rules  and identify the top offending IP addresses in your environment.

Microsoft Security Copilot integration is supported on both Azure WAF on Azure Application Gateway and Azure WAF on Azure Front Door.

## Know before you begin

If you're new to Microsoft Security Copilot, you should familiarize yourself with it by reading these articles:

- [What is Microsoft Security Copilot?](/security-copilot/microsoft-security-copilot)

- [Microsoft Security Copilot experiences](/security-copilot/experiences-security-copilot)

- [Get started with Microsoft Security Copilot](/security-copilot/get-started-security-copilot)

- [Understand authentication in Microsoft Security Copilot](/security-copilot/authentication)

- [Prompting in Microsoft Security Copilot](/security-copilot/prompting-security-copilot)

## Microsoft Security Copilot integration in Azure WAF

This integration supports the standalone experience and is accessed through [https://securitycopilot.microsoft.com](https://securitycopilot.microsoft.com). This is a chat-like experience that you can use to ask questions and get answers about your data. For more information, see [Microsoft Security Copilot experiences](/security-copilot/experiences-security-copilot#standalone-and-embedded-experiences).

## Key features

Azure Web Application Firewall integration in Microsoft Security Copilot provides several powerful capabilities to help you analyze and understand your security posture. These features use AI to translate complex WAF logs into actionable insights through natural language responses.

- Providing a list of top Azure WAF rules triggered in the customer environment and generating deep context with related attack vectors.

This capability provides details about Azure WAF rules that are triggered due to a WAF block. It provides an ordered list of rules based on trigger frequency in the desired time period. The analysis processes Azure WAF logs and connects related logs over a specific time period. The result is an easy-to-understand natural language explanation of why a particular request was blocked.

- Providing a list of malicious IP addresses in the customer environment and generating related threats.

This capability provides details about client IP addresses blocked by the Azure WAF. The analysis processes Azure WAF logs and connects related logs over a specific time period. The result is an easy-to-understand natural language explanation of which IP addresses the WAF blocked and the reason for the blocks.

- Summarizing SQL injection (SQLi) attacks.

This capability provides details about SQL injection (SQLi) attacks that were blocked by Azure WAF. By analyzing Azure WAF logs and correlating related data over a specific time period, this skill delivers an easy-to-understand natural language explanation of why SQLi requests were blocked.

- Summarizing Cross-site scripting (XSS) attacks.

This Azure WAF skill helps you understand why Azure WAF blocked Cross Site Scripting (XSS) attacks to web applications. The skill analyzes Azure WAF logs and connects related incidents over a specific time period. The result is an easy-to-understand natural language explanation of why an XSS request was blocked.

## Enable the Azure WAF integration in Security Copilot

To enable the integration, follow these steps:

1.	Ensure that you have at least Copilot contributor permissions.

2.	Open [https://securitycopilot.microsoft.com/](https://securitycopilot.microsoft.com).

3.	Open the Security Copilot menu.

4.	Open **Sources** in the prompt bar.

5.	On the Plugins page, set the Azure Web Application Firewall toggle to **On**.

6.	Select the Settings on the Azure Web Application Firewall plugin to configure the Log Analytics workspace for Azure Front Door WAF or the Azure Application Gateway WAF.

7.	To start using the skills, use the prompt bar.

## Sample Azure WAF prompts

You can create your own prompts in Microsoft Security Copilot to perform analysis on the attacks based on WAF logs. This section shows some ideas and examples.

### Before you begin

- Be clear and specific with your prompts. You might get better results if you include specific device IDs/names, app names, or policy names in your prompts.

It might also help to add WAF to your prompt. For example:

- Was there any SQL injection attack in my regional WAF in the last day?

- Tell me more about the top rules triggered in my global WAF

- Experiment with different prompts and variations to see what works best for your use case. Chat AI models vary, so iterate and refine your prompts based on the results you receive

For guidance on writing effective prompts, see Creating your own prompts.

The following example prompts might be helpful.

### Summarize information about SQL injection attacks

- Was there a SQL injection attack in my global WAF in the last day?

- Show me IP addresses related to the top SQL injection attack in my global WAF

- Show me all SQL injection attacks in regional WAF in the last 24 hours

### Summarize information about cross-site scripting attacks

- Was any XSS attack detected in my Application Gateway WAF in the last 12 hours?

- Show me list of all XSS attacks in my Azure Front Door WAF

### Generate a list of threats in my environment based on WAF rules

- What were the top global WAF rules triggered in the last 24 hours?

- What are top threats related to the WAF Rule in my environment? \<enter rule ID\>

- Was there any bot attack in my regional WAF in the last day?

- Summarize custom rule blocks triggered by Azure Front Door WAF in the last day.

### Generate a list of threats in my environment based on malicious IP addresses

- What was the top offending IP in regional WAF in the last day?

- Summarize list of malicious IP addresses in my Azure Front Door WAF in the last six hours?

## Provide feedback

Your feedback on the Azure WAF integration with Microsoft Security Copilot helps with development. To provide feedback in Copilot, select **How’s this response?** At the bottom of each completed prompt and choose any of the following options:

- Looks right - Select if the results are accurate, based on your assessment.

- Needs improvement - Select if any detail in the results is incorrect or incomplete, based on your assessment.

- Inappropriate - Select if the results contain questionable, ambiguous, or potentially harmful information.

For each feedback item, you can provide more information in the next dialog box that appears. Whenever possible, and when the result is Needs improvement, write a few words explaining what can be done to improve the outcome.

## Limitation

If you migrate to Azure Log Analytics dedicated tables in the Application Gateway WAF V2 version, the Microsoft Security Copilot WAF Skills aren't functional. As a temporary workaround, enable Azure Diagnostics as the destination table in addition to the resource-specific table.

**Application Gateway for Containers WAF**: Application Gateway for Containers WAF doesn't support Security Copilot.

## Privacy and data security in Microsoft Security Copilot

To understand how Microsoft Security Copilot handles your prompts and the data that’s retrieved from the service (prompt output), see [Privacy and data security in Microsoft Security Copilot](/security-copilot/privacy-data-security).

## Related content

- [What is Microsoft Security Copilot?](/copilot/security/microsoft-security-copilot)

- [Microsoft Security Copilot experiences](/security-copilot/experiences-security-copilot)

- [Get started with Microsoft Security Copilot](/security-copilot/get-started-security-copilot)


# Waf Application Gateway For Containers Overview

# What is Azure Web Application Firewall on Application Gateway for Containers?

Azure Web Application Firewall on [Azure Application Gateway for Containers](../../application-gateway/for-containers/overview.md) provides comprehensive protection for your Kubernetes workloads against common web vulnerabilities and attacks. For example, it addresses SQL injection, cross-site scripting (XSS), and other Open Web Application Security Project (OWASP) top 10 threats.

Application Gateway for Containers is an application-layer (Layer 7) solution for [load balancing](/azure/architecture/guide/technology-choices/load-balancing-overview) and dynamic traffic management. It's designed specifically for workloads running in Kubernetes clusters. It represents the evolution of the [Application Gateway Ingress Controller (AGIC)](../../application-gateway/ingress-controller-overview.md).

Azure Web Application Firewall provides real-time protection for these application-layer workloads through a set of proprietary managed rule sets and a framework for the creation of user-generated custom rules. All of these protections exist as part of a web application firewall (WAF) policy that's attached to your Application Gateway for Containers deployment via a `SecurityPolicy` resource.

### Security policy

Application Gateway for Containers introduces a new child resource called `SecurityPolicy` in Azure Resource Manager. The `SecurityPolicy` resource brings scope to which Azure Web Application Firewall policies the ALB Controller can reference.

### Kubernetes custom resource

Application Gateway for Containers introduces a new custom resource called `WebApplicationFirewallPolicy`. The custom resource is responsible for defining which Azure Web Application Firewall policy should be used at which scope.

The WebApplicationFirewallPolicy resource can target the following Kubernetes resources:

* `Gateway`

* `HTTPRoute`

The WebApplicationFirewallPolicy resource can also reference the following sections by name for further granularity:

* `Gateway`: `Listener`

### Example implementations

#### Scope a policy to a Gateway resource

Here's an example YAML configuration that shows targeting a Gateway resource, which would apply to all listeners on a given Application Gateway for Containers' frontend resource.

```yaml

apiVersion: alb.networking.azure.io/v1

kind: WebApplicationFirewallPolicy

metadata:

name: sample-waf-policy

namespace: test-infra

spec:

targetRef:

group: gateway.networking.k8s.io

kind: Gateway

name: contoso-waf-route

namespace: test-infra

webApplicationFirewall:

id: /subscriptions/.../Microsoft.Network/applicationGatewayWebApplicationFirewallPolicies/waf-policy-0

```

#### Scope policy to a specific listener of a Gateway resource

Within a `Gateway` resource, you may have different hostnames defined by different listeners (e.g. contoso.com and fabrikam.com). If contoso.com is a hostname of listenerA and fabrikam.com is a hostname of listenerB, you can define the `sectionNames` property to select the proper listener (for example, listenerA for contoso.com).

```yaml

apiVersion: alb.networking.azure.io/v1

kind: WebApplicationFirewallPolicy

metadata:

name: sample-waf-policy

namespace: test-infra

spec:

targetRef:

group: gateway.networking.k8s.io

kind: Gateway

name: contoso-waf-route

namespace: test-infra

sectionNames: ["contoso-listener"]

webApplicationFirewall:

id: /subscriptions/.../Microsoft.Network/applicationGatewayWebApplicationFirewallPolicies/waf-policy-0

```

#### Scope policy across all routes and paths

This example shows how to target a defined HTTPRoute resource to apply the policy to any routing rules and paths within a given HTTPRoute resource.

```yaml

apiVersion: alb.networking.azure.io/v1

kind: WebApplicationFirewallPolicy

metadata:

name: sample-waf-policy

namespace: test-infra

spec:

targetRef:

group: gateway.networking.k8s.io

kind: HTTPRoute

name: contoso-pathA

namespace: test-infra

webApplicationFirewall:

id: /subscriptions/.../Microsoft.Network/applicationGatewayWebApplicationFirewallPolicies/waf-policy-0

```

#### Scope policy to a particular path

To use different WAF policies to different paths of the same `Gateway` or Gateway -> Listener sectionName, you can define two HTTPRoute resources, each with a unique path, that each references its applicable WAF policy.

```yaml

apiVersion: alb.networking.azure.io/v1

kind: WebApplicationFirewallPolicy

metadata:

name: sample-waf-policy-A

namespace: test-infra

spec:

targetRef:

group: gateway.networking.k8s.io

kind: HTTPRoute

name: contoso-pathA

namespace: test-infra

webApplicationFirewall:

id: /subscriptions/.../Microsoft.Network/applicationGatewayWebApplicationFirewallPolicies/waf-policy-0

---

apiVersion: alb.networking.azure.io/v1

kind: WebApplicationFirewallPolicy

metadata:

name: sample-waf-policy-B

namespace: test-infra

spec:

targetRef:

group: gateway.networking.k8s.io

kind: HTTPRoute

name: contoso-pathB

namespace: test-infra

webApplicationFirewall:

id: /subscriptions/.../Microsoft.Network/applicationGatewayWebApplicationFirewallPolicies/waf-policy-1

```

## Limitations

The following functionality isn't supported on a WAF policy that's associated with an Application Gateway for Containers instance:

- **Cross-region, cross-subscription policy**: Your WAF policy must be in the same subscription and region as your Application Gateway for Containers resource.

- **Core Rule Set (CRS) managed rules**: An Application Gateway for Containers WAF supports only Default Rule Set (DRS) 2.1 managed rule set.

- **Legacy Bot Manager Rule Set**: Bot Manager Ruleset 0.1 isn't supported, but Bot Manager Ruleset versions 1.0 and 1.1 are supported.

- **JavaScript challenge actions on Bot Manager rules**: You can't set the action on a Bot Manager rule to JavaScript challenge.

- **Captcha challenge actions on Bot Manager rules**: You can't set the action on a Bot Manager rule to Captcha.

- **Microsoft Security Copilot**: The Security Copilot is not supported on Application Gateway for Containers WAF.

- **Custom Block Response**: Setting a custom block response in your WAF policy is not supported on Application Gateway for Containers WAF.

- **X-Forwarded-For Header (XFF)**: Application Gateway for Containers WAF doesn't support the XFF variable in custom rules.

- **HTTP DDoS Ruleset**: This managed ruleset isn't currenlty supported on Application Gateway for Containers.

## Pricing

For pricing details, see [Application Gateway for Containers pricing](../../application-gateway/for-containers/understanding-pricing.md).

## Related content

- [What is Azure Web Application Firewall?](../../web-application-firewall/overview.md)

- [What is Azure Web Application Firewall on Azure Application Gateway?](ag-overview.md)

- [Deploy Application Gateway for Containers ALB Controller](../../application-gateway/for-containers/quickstart-deploy-application-gateway-for-containers-alb-controller.md)


# Tutorial Restrict Web Traffic Powershell

# Enable Web Application Firewall using Azure PowerShell

You can restrict traffic on an application gateway with a [Web Application Firewall (WAF)](ag-overview.md). The WAF uses [OWASP](https://owasp.org/www-project-modsecurity-core-rule-set/) rules to protect your application. These rules include protection against attacks such as SQL injection, cross-site scripting attacks, and session hijacks.

In this article, you learn how to:

* Set up the network

* Create an application gateway with WAF enabled

* Create a virtual machine scale set

* Create a storage account and configure diagnostics

If you prefer, you can complete this article using the [Azure portal](application-gateway-web-application-firewall-portal.md) or the [Azure CLI](tutorial-restrict-web-traffic-cli.md).

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

[!INCLUDE [updated-for-az](~/reusable-content/ce-skilling/azure/includes/updated-for-az.md)]

[!INCLUDE [cloud-shell-try-it.md](~/reusable-content/ce-skilling/azure/includes/cloud-shell-try-it.md)]

If you choose to install and use the PowerShell locally, this article requires the Azure PowerShell module version 1.0.0 or later. Run `Get-Module -ListAvailable Az` to find the version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell). If you're running PowerShell locally, you also need to run `Login-AzAccount` to create a connection with Azure.

## Create a resource group

A resource group is a logical container into which Azure resources are deployed and managed. Create an Azure resource group using [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup).

```azurepowershell-interactive

$location = "eastus"

$rgname = New-AzResourceGroup -Name myResourceGroupAG -Location $location

```

## Create network resources

Create the subnet configurations named *myBackendSubnet* and *myAGSubnet* using [New-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/new-azvirtualnetworksubnetconfig). Create the virtual network named *myVNet* using [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork) with the subnet configurations. And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress). These resources are used to provide network connectivity to the application gateway and its associated resources.

```azurepowershell-interactive

$backendSubnetConfig = New-AzVirtualNetworkSubnetConfig `

-Name myBackendSubnet `

-AddressPrefix 10.0.1.0/24

$agSubnetConfig = New-AzVirtualNetworkSubnetConfig `

-Name myAGSubnet `

-AddressPrefix 10.0.2.0/24

$vnet = New-AzVirtualNetwork `

-ResourceGroupName myResourceGroupAG `

-Location eastus `

-Name myVNet `

-AddressPrefix 10.0.0.0/16 `

-Subnet $backendSubnetConfig, $agSubnetConfig

$pip = New-AzPublicIpAddress `

-ResourceGroupName myResourceGroupAG `

-Location eastus `

-Name myAGPublicIPAddress `

-AllocationMethod Static `

-Sku Standard

```

## Create an application gateway

In this section, you create resources that support the application gateway, and then finally create it and a WAF. The resources that you create include:

- *IP configurations and frontend port* - Associates the subnet that you previously created to the application gateway and assigns a port to use to access it.

- *Default pool* - All application gateways must have at least one backend pool of servers.

- *Default listener and rule* - The default listener listens for traffic on the port that was assigned and the default rule sends traffic to the default pool.

### Create the IP configurations and frontend port

Associate *myAGSubnet* that you previously created to the application gateway using [New-AzApplicationGatewayIPConfiguration](/powershell/module/az.network/new-azapplicationgatewayipconfiguration). Assign *myAGPublicIPAddress* to the application gateway using [New-AzApplicationGatewayFrontendIPConfig](/powershell/module/az.network/new-azapplicationgatewayfrontendipconfig).

```azurepowershell-interactive

$vnet = Get-AzVirtualNetwork `

-ResourceGroupName myResourceGroupAG `

-Name myVNet

$subnet=$vnet.Subnets[1]

$gipconfig = New-AzApplicationGatewayIPConfiguration `

-Name myAGIPConfig `

-Subnet $subnet

$fipconfig = New-AzApplicationGatewayFrontendIPConfig `

-Name myAGFrontendIPConfig `

-PublicIPAddress $pip

$frontendport = New-AzApplicationGatewayFrontendPort `

-Name myFrontendPort `

-Port 80

```

### Create the backend pool and settings

Create the backend pool named *appGatewayBackendPool* for the application gateway using [New-AzApplicationGatewayBackendAddressPool](/powershell/module/az.network/new-azapplicationgatewaybackendaddresspool). Configure the settings for the backend address pools using [New-AzApplicationGatewayBackendHttpSettings](/powershell/module/az.network/new-azapplicationgatewaybackendhttpsetting).

```azurepowershell-interactive

$defaultPool = New-AzApplicationGatewayBackendAddressPool `

-Name appGatewayBackendPool

$poolSettings = New-AzApplicationGatewayBackendHttpSettings `

-Name myPoolSettings `

-Port 80 `

-Protocol Http `

-CookieBasedAffinity Enabled `

-RequestTimeout 120

```

### Create the default listener and rule

A listener is required to enable the application gateway to route traffic appropriately to the backend address pools. In this example, you create a basic listener that listens for traffic at the root URL.

Create a listener named *mydefaultListener* using [New-AzApplicationGatewayHttpListener](/powershell/module/az.network/new-azapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created. A rule is required for the listener to know which backend pool to use for incoming traffic. Create a basic rule named *rule1* using [New-AzApplicationGatewayRequestRoutingRule](/powershell/module/az.network/new-azapplicationgatewayrequestroutingrule).

```azurepowershell-interactive

$defaultlistener = New-AzApplicationGatewayHttpListener `

-Name mydefaultListener `

-Protocol Http `

-FrontendIPConfiguration $fipconfig `

-FrontendPort $frontendport

$frontendRule = New-AzApplicationGatewayRequestRoutingRule `

-Name rule1 `

-RuleType Basic `

-Priority 1000 `

-HttpListener $defaultlistener `

-BackendAddressPool $defaultPool `

-BackendHttpSettings $poolSettings

```

### Create the application gateway with the WAF

Now that you created the necessary supporting resources, specify parameters for the application gateway using [New-AzApplicationGatewaySku](/powershell/module/az.network/new-azapplicationgatewaysku). Specify the Firewall Policy using [New-AzApplicationGatewayFirewallPolicy](/powershell/module/az.network/new-azapplicationgatewayfirewallpolicy). And then create the application gateway named *myAppGateway* using [New-AzApplicationGateway](/powershell/module/az.network/new-azapplicationgateway).

```azurepowershell-interactive

$sku = New-AzApplicationGatewaySku `

-Name WAF_v2 `

-Tier WAF_v2 `

-Capacity 2

$policySetting = New-AzApplicationGatewayFirewallPolicySetting `

-Mode Prevention -State Enabled `

-MaxRequestBodySizeInKb 100 -MaxFileUploadInMb 256

$wafPolicy = New-AzApplicationGatewayFirewallPolicy -Name wafpolicyNew -ResourceGroup myResourceGroupAG `

-Location $location -PolicySetting $PolicySetting

$appgw = New-AzApplicationGateway `

-Name myAppGateway `

-ResourceGroupName myResourceGroupAG `

-Location eastus `

-BackendAddressPools $defaultPool `

-BackendHttpSettingsCollection $poolSettings `

-FrontendIpConfigurations $fipconfig `

-GatewayIpConfigurations $gipconfig `

-FrontendPorts $frontendport `

-HttpListeners $defaultlistener `

-RequestRoutingRules $frontendRule `

-Sku $sku `

-FirewallPolicy $wafPolicy

```

## Create a virtual machine scale set

In this example, you create a virtual machine scale set to provide servers for the backend pool in the application gateway. You assign the scale set to the backend pool when you configure the IP settings.

> [!NOTE]

> The virtual machine scale set instances in the backend pool don't have public IP addresses and aren't directly accessible from the internet. Management access to the instances, if needed, can be configured through [Azure Bastion](/azure/bastion/bastion-overview).

Replace *\<username>* and *\<password>* with your values before you run this script.

```azurepowershell-interactive

$vnet = Get-AzVirtualNetwork `

-ResourceGroupName myResourceGroupAG `

-Name myVNet

$appgw = Get-AzApplicationGateway `

-ResourceGroupName myResourceGroupAG `

-Name myAppGateway

$backendPool = Get-AzApplicationGatewayBackendAddressPool `

-Name appGatewayBackendPool `

-ApplicationGateway $appgw

$ipConfig = New-AzVmssIpConfig `

-Name myVmssIPConfig `

-SubnetId $vnet.Subnets[0].Id `

-ApplicationGatewayBackendAddressPoolsId $backendPool.Id

$vmssConfig = New-AzVmssConfig `

-Location eastus `

-SkuCapacity 2 `

-SkuName Standard_DS2 `

-UpgradePolicyMode Automatic

Set-AzVmssStorageProfile $vmssConfig `

-ImageReferencePublisher MicrosoftWindowsServer `

-ImageReferenceOffer WindowsServer `

-ImageReferenceSku 2016-Datacenter `

-ImageReferenceVersion latest `

-OsDiskCreateOption FromImage

Set-AzVmssOsProfile $vmssConfig `

-AdminUsername <username> `

-AdminPassword "<password>" `

-ComputerNamePrefix myvmss

Add-AzVmssNetworkInterfaceConfiguration `

-VirtualMachineScaleSet $vmssConfig `

-Name myVmssNetConfig `

-Primary $true `

-IPConfiguration $ipConfig

New-AzVmss `

-ResourceGroupName myResourceGroupAG `

-Name myvmss `

-VirtualMachineScaleSet $vmssConfig

```

### Install IIS

```azurepowershell-interactive

$publicSettings = @{ "fileUris" = (,"https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/appgatewayurl.ps1");

"commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File appgatewayurl.ps1" }

$vmss = Get-AzVmss -ResourceGroupName myResourceGroupAG -VMScaleSetName myvmss

Add-AzVmssExtension -VirtualMachineScaleSet $vmss `

-Name "customScript" `

-Publisher "Microsoft.Compute" `

-Type "CustomScriptExtension" `

-TypeHandlerVersion 1.8 `

-Setting $publicSettings

Update-AzVmss `

-ResourceGroupName myResourceGroupAG `

-Name myvmss `

-VirtualMachineScaleSet $vmss

```

## Create a storage account and configure diagnostics

In this article, the application gateway uses a storage account to store data for detection and prevention purposes. You could also use Azure Monitor logs or Event Hub to record data.

### Create the storage account

Create a storage account named *myagstore1* using [New-AzStorageAccount](/powershell/module/az.storage/new-azstorageaccount).

```azurepowershell-interactive

$storageAccount = New-AzStorageAccount `

-ResourceGroupName myResourceGroupAG `

-Name myagstore1 `

-Location eastus `

-SkuName "Standard_LRS"

```

### Configure diagnostics

Configure diagnostics to record data into the ApplicationGatewayAccessLog, ApplicationGatewayPerformanceLog, and ApplicationGatewayFirewallLog logs using [Set-AzDiagnosticSetting](/powershell/module/az.monitor/set-azdiagnosticsetting).

```azurepowershell-interactive

$appgw = Get-AzApplicationGateway `

-ResourceGroupName myResourceGroupAG `

-Name myAppGateway

$store = Get-AzStorageAccount `

-ResourceGroupName myResourceGroupAG `

-Name myagstore1

Set-AzDiagnosticSetting `

-ResourceId $appgw.Id `

-StorageAccountId $store.Id `

-Category ApplicationGatewayAccessLog, ApplicationGatewayPerformanceLog, ApplicationGatewayFirewallLog `

-Enabled $true `

-RetentionEnabled $true `

-RetentionInDays 30

```

## Test the application gateway

You can use [Get-AzPublicIPAddress](/powershell/module/az.network/get-azpublicipaddress) to get the public IP address of the application gateway. Copy the public IP address, and then paste it into the address bar of your browser.

```azurepowershell-interactive

Get-AzPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress

```

![Test base URL in application gateway](../media/tutorial-restrict-web-traffic-powershell/application-gateway-iistest.png)

## Clean up resources

When no longer needed, remove the resource group, application gateway, and all related resources using [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup).

```azurepowershell-interactive

Remove-AzResourceGroup -Name myResourceGroupAG

```

## Next steps

- [Customize web application firewall rules](application-gateway-customize-waf-rules-portal.md)


# Tutorial Restrict Web Traffic Cli

# Enable Web Application Firewall using the Azure CLI

You can restrict traffic on an application gateway with a [Web Application Firewall (WAF)](ag-overview.md). The WAF uses [OWASP](https://owasp.org/www-project-modsecurity-core-rule-set/) rules to protect your application. These rules include protection against attacks such as SQL injection, cross-site scripting attacks, and session hijacks.

In this article, you learn how to:

* Set up the network

* Create an application gateway with WAF enabled

* Create a virtual machine scale set

* Create a storage account and configure diagnostics

If you prefer, you can complete this procedure using [Azure PowerShell](tutorial-restrict-web-traffic-powershell.md).

[!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment.md)]

- This article requires version 2.0.4 or later of the Azure CLI. If using Azure Cloud Shell, the latest version is already installed.

## Create a resource group

A resource group is a logical container into which Azure resources are deployed and managed. Create an Azure resource group named *myResourceGroupAG* with [az group create](/cli/azure/group#az-group-create).

```azurecli-interactive

az group create --name myResourceGroupAG --location eastus

```

## Create network resources

The virtual network and subnets are used to provide network connectivity to the application gateway and its associated resources. Create a virtual network named *myVNet* and a subnet named *myAGSubnet*.

then create a public IP address named *myAGPublicIPAddress*.

```azurecli-interactive

az network vnet create \

--name myVNet \

--resource-group myResourceGroupAG \

--location eastus \

--address-prefix 10.0.0.0/16 \

--subnet-name myBackendSubnet \

--subnet-prefix 10.0.1.0/24

az network vnet subnet create \

--name myAGSubnet \

--resource-group myResourceGroupAG \

--vnet-name myVNet \

--address-prefix 10.0.2.0/24

az network public-ip create \

--resource-group myResourceGroupAG \

--name myAGPublicIPAddress \

--allocation-method Static \

--sku Standard

```

## Create an application gateway with a WAF policy

You can use [az network application-gateway create](/cli/azure/network/application-gateway) to create the application gateway named *myAppGateway*. When you create an application gateway using the Azure CLI, you specify configuration information, such as capacity, sku, and HTTP settings. The application gateway is assigned to *myAGSubnet* and *myAGPublicIPAddress*.

```azurecli-interactive

az network application-gateway waf-policy create \

--name waf-pol \

--resource-group myResourceGroupAG \

--type OWASP \

--version 3.2

az network application-gateway create \

--name myAppGateway \

--location eastus \

--resource-group myResourceGroupAG \

--vnet-name myVNet \

--subnet myAGSubnet \

--capacity 2 \

--sku WAF_v2 \

--http-settings-cookie-based-affinity Disabled \

--frontend-port 80 \

--http-settings-port 80 \

--http-settings-protocol Http \

--public-ip-address myAGPublicIPAddress \

--waf-policy waf-pol \

--priority 1

```

It may take several minutes for the application gateway to be created. After the application gateway is created, you can see these new features of it:

- *appGatewayBackendPool* - An application gateway must have at least one backend address pool.

- *appGatewayBackendHttpSettings* - Specifies that port 80 and an HTTP protocol is used for communication.

- *appGatewayHttpListener* - The default listener associated with *appGatewayBackendPool*.

- *appGatewayFrontendIP* - Assigns *myAGPublicIPAddress* to *appGatewayHttpListener*.

- *rule1* - The default routing rule that is associated with *appGatewayHttpListener*.

## Create a virtual machine scale set

In this example, you create a virtual machine scale set that provides two servers for the backend pool in the application gateway. The virtual machines in the scale set are associated with the *myBackendSubnet* subnet. To create the scale set, you can use [az vmss create](/cli/azure/vmss#az-vmss-create).

> [!NOTE]

> The virtual machine scale set instances in the backend pool don't have public IP addresses and aren't directly accessible from the internet. Management access to the instances, if needed, can be configured through [Azure Bastion](/azure/bastion/bastion-overview).

Replace \<username> and \<password> with your values before you run this.

```azurecli-interactive

az vmss create \

--name myvmss \

--resource-group myResourceGroupAG \

--image Ubuntu2204 \

--admin-username <username> \

--admin-password <password> \

--instance-count 2 \

--vnet-name myVNet \

--subnet myBackendSubnet \

--vm-sku Standard_DS2 \

--upgrade-policy-mode Automatic \

--app-gateway myAppGateway \

--backend-pool-name appGatewayBackendPool

```

### Install NGINX

```azurecli-interactive

az vmss extension set \

--publisher Microsoft.Azure.Extensions \

--version 2.0 \

--name CustomScript \

--resource-group myResourceGroupAG \

--vmss-name myvmss \

--settings '{ "fileUris": ["https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/install_nginx.sh"],"commandToExecute": "./install_nginx.sh" }'

```

## Create a storage account and configure diagnostics

In this article, the application gateway uses a storage account to store data for detection and prevention purposes. You could also use Azure Monitor logs or Event Hub to record data.

### Create a storage account

Create a storage account named *myagstore1* with [az storage account create](/cli/azure/storage/account#az-storage-account-create).

```azurecli-interactive

az storage account create \

--name myagstore1 \

--resource-group myResourceGroupAG \

--location eastus \

--sku Standard_LRS \

--encryption-services blob

```

### Configure diagnostics

Configure diagnostics to record data into the ApplicationGatewayAccessLog, ApplicationGatewayPerformanceLog, and ApplicationGatewayFirewallLog logs. Replace `<subscriptionId>` with your subscription identifier and then configure diagnostics with [az monitor diagnostic-settings create](/cli/azure/monitor/diagnostic-settings#az-monitor-diagnostic-settings-create).

```azurecli-interactive

appgwid=$(az network application-gateway show --name myAppGateway --resource-group myResourceGroupAG --query id -o tsv)

storeid=$(az storage account show --name myagstore1 --resource-group myResourceGroupAG --query id -o tsv)

az monitor diagnostic-settings create --name appgwdiag --resource $appgwid \

--logs '[ { "category": "ApplicationGatewayAccessLog", "enabled": true, "retentionPolicy": { "days": 30, "enabled": true } }, { "category": "ApplicationGatewayPerformanceLog", "enabled": true, "retentionPolicy": { "days": 30, "enabled": true } }, { "category": "ApplicationGatewayFirewallLog", "enabled": true, "retentionPolicy": { "days": 30, "enabled": true } } ]' \

--storage-account $storeid

```

## Test the application gateway

To get the public IP address of the application gateway, use [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show). Copy the public IP address, and then paste it into the address bar of your browser.

```azurecli-interactive

az network public-ip show \

--resource-group myResourceGroupAG \

--name myAGPublicIPAddress \

--query [ipAddress] \

--output tsv

```

![Test base URL in application gateway](../media/tutorial-restrict-web-traffic-cli/application-gateway-nginxtest.png)

## Clean up resources

When no longer needed, remove the resource group, application gateway, and all related resources.

```azurecli-interactive

az group delete --name myResourceGroupAG

```

## Next steps

[Customize web application firewall rules](application-gateway-customize-waf-rules-portal.md)


# Quick Create Template

# Quickstart: Create an Azure Web Application Firewall v2 using an ARM template

In this quickstart, you use an Azure Resource Manager template (ARM template) to create an Azure Web Application Firewall (WAF) v2 on Azure Application Gateway.

[!INCLUDE [About Azure Resource Manager](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-introduction.md)]

If your environment meets the prerequisites and you're familiar with using ARM templates, you can select the **Deploy to Azure** button to open the template in the Azure portal.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, you can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Review the template

This template creates a simple Web Application Firewall v2 on Azure Application Gateway. The template creates a public IP frontend IP address, HTTP settings, a rule with a basic listener on port 80, and a backend pool. A WAF policy with a custom rule blocks traffic to the backend pool based on an IP address match type.

The template defines the following Azure resources:

- [Microsoft.Network/applicationgateways](/azure/templates/microsoft.network/applicationgateways)

- [Microsoft.Network/ApplicationGatewayWebApplicationFirewallPolicies](/azure/templates/microsoft.network/ApplicationGatewayWebApplicationFirewallPolicies)

- [Microsoft.Network/publicIPAddresses](/azure/templates/microsoft.network/publicipaddresses), one for the application gateway and two for the virtual machines (VMs)

- [Microsoft.Network/networkSecurityGroups](/azure/templates/microsoft.network/networksecuritygroups)

- [Microsoft.Network/virtualNetworks](/azure/templates/microsoft.network/virtualnetworks)

- [Microsoft.Compute/virtualMachines](/azure/templates/microsoft.compute/virtualmachines), two VMs

- [Microsoft.Network/networkInterfaces](/azure/templates/microsoft.network/networkinterfaces), one for each VM

- [Microsoft.Compute/virtualMachine/extensions](/azure/templates/microsoft.compute/virtualmachines/extensions) to configure IIS and the web pages

This template is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/ag-docs-wafv2/).

## Deploy the template

Deploy the ARM template to Azure:

1. Select **Deploy to Azure** to sign in to Azure and open the template. The template creates an application gateway, the network infrastructure, and two VMs in the backend pool running IIS.

1. Select or create a resource group.

1. Select **Review + create**, and when validation passes, select **Create**. The deployment can take 10 minutes or longer to complete.

## Validate the deployment

Although IIS isn't required, the template installs IIS on the backend servers so you can verify that Azure successfully created a WAF v2 on the application gateway.

Use IIS to test the application gateway:

1. Copy the public IP address for the application gateway from its **Overview** page.

![Screenshot that shows the application gateway public IP address.](../../application-gateway/media/application-gateway-create-gateway-portal/application-gateway-record-ag-address.png)

You can also search for *application gateways* in the Azure search box. The list of application gateways shows the public IP addresses in the **Public IP address** column.

1. Paste the IP address into the address bar of your browser to browse that address.

1. Check the response. A **403 Forbidden** response verifies that the WAF is successfully blocking connections to the backend pool.

1. To change the custom rule to allow traffic, run the following Azure PowerShell script, replacing your resource group name:

```azurepowershell

$rg = "<your resource group name>"

$AppGW = Get-AzApplicationGateway -Name myAppGateway -ResourceGroupName $rg

$pol = Get-AzApplicationGatewayFirewallPolicy -Name WafPol01 -ResourceGroupName $rg

$pol[0].customrules[0].action = "allow"

$rule = $pol.CustomRules

Set-AzApplicationGatewayFirewallPolicy -Name WafPol01 -ResourceGroupName $rg -CustomRule $rule

$AppGW.FirewallPolicy = $pol

Set-AzApplicationGateway -ApplicationGateway $AppGW

```

1. Refresh your browser several times. You should see connections to both myVM1 and myVM2.

## Clean up resources

When you no longer need the resources you created in this quickstart, delete the resource group to remove the application gateway and all its related resources.

To delete the resource group, call the `Remove-AzResourceGroup` cmdlet:

```azurepowershell-interactive

Remove-AzResourceGroup -Name "<your resource group name>"

```

## Next step

> [!div class="nextstepaction"]

> [Create an application gateway with a Web Application Firewall using the Azure portal](application-gateway-web-application-firewall-portal.md)


# Quick Create Bicep

# Quickstart: Create an Azure WAF v2 on Application Gateway using Bicep

In this quickstart, you use Bicep to create an Azure Web Application Firewall v2 on Application Gateway.

[!INCLUDE [About Bicep](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-bicep-introduction.md)]

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Review the Bicep file

This Bicep file creates a simple Web Application Firewall v2 on Azure Application Gateway. This includes a public IP frontend IP address, HTTP settings, a rule with a basic listener on port 80, and a backend pool. The file also creates a WAF policy with a custom rule to block traffic to the backend pool based on an IP address match type.

The Bicep file used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/ag-docs-wafv2/).

Multiple Azure resources are defined in the Bicep file:

- [**Microsoft.Network/applicationgateways**](/azure/templates/microsoft.network/applicationgateways)

- [**Microsoft.Network/ApplicationGatewayWebApplicationFirewallPolicies**](/azure/templates/microsoft.network/ApplicationGatewayWebApplicationFirewallPolicies)

- [**Microsoft.Network/publicIPAddresses**](/azure/templates/microsoft.network/publicipaddresses) : one for the application gateway, and two for the virtual machines.

- [**Microsoft.Network/networkSecurityGroups**](/azure/templates/microsoft.network/networksecuritygroups)

- [**Microsoft.Network/virtualNetworks**](/azure/templates/microsoft.network/virtualnetworks)

- [**Microsoft.Compute/virtualMachines**](/azure/templates/microsoft.compute/virtualmachines) : two virtual machines

- [**Microsoft.Network/networkInterfaces**](/azure/templates/microsoft.network/networkinterfaces) : two for the virtual machines

- [**Microsoft.Compute/virtualMachine/extensions**](/azure/templates/microsoft.compute/virtualmachines/extensions) : to configure IIS and the web pages

## Deploy the Bicep file

1. Save the Bicep file as **main.bicep** to your local computer.

1. Deploy the Bicep file using either Azure CLI or Azure PowerShell.

# [CLI](#tab/CLI)

```azurecli

az group create --name exampleRG --location eastus

az deployment group create --resource-group exampleRG --template-file main.bicep --parameters adminUsername=<admin-user>

```

# [PowerShell](#tab/PowerShell)

```azurepowershell

New-AzResourceGroup -Name exampleRG -Location eastus

New-AzResourceGroupDeployment -ResourceGroupName exampleRG -TemplateFile ./main.bicep -adminUsername "<admin-user>"

```

---

> [!NOTE]

> You'll be prompted to enter **adminPassword**, which is the password for the admin account on the backend servers. The password must be between 8-123 characters long and must contain at least three of the following: an uppercase character, a lowercase character, a numeric digit, or a special character.

When the deployment finishes, you should see a message indicating the deployment succeeded. The deployment can take 10 minutes or longer to complete.

## Validate the deployment

Although IIS isn't required to create the application gateway, it's installed on the backend servers to verify if Azure successfully created a WAF v2 on the application gateway.

Use IIS to test the application gateway:

1. Find the public IP address for the application gateway on its **Overview** page.![Record application gateway public IP address](../../application-gateway/media/application-gateway-create-gateway-bicep/app-gateway-ip-address-bicep.png)

2. Copy the public IP address, and then paste it into the address bar of your browser to browse that IP address.

3. Check the response. A **403 Forbidden** response verifies that the WAF was successfully created and is blocking connections to the backend pool.

4. Change the custom rule to **Allow traffic** using Azure PowerShell.

```azurepowershell

$rgName = "exampleRG"

$appGWName = "myAppGateway"

$fwPolicyName = "WafPol01"

# Pull the existing Azure resources

$appGW = Get-AzApplicationGateway -Name $appGWName -ResourceGroupName $rgName

$pol = Get-AzApplicationGatewayFirewallPolicy -Name $fwPolicyName -ResourceGroupName $rgName

# Update the resources

$pol[0].CustomRules[0].Action = "allow"

$appGW.FirewallPolicy = $pol

# Push your changes to Azure

Set-AzApplicationGatewayFirewallPolicy -Name $fwPolicyName -ResourceGroupName $rgName -CustomRule $pol.CustomRules

Set-AzApplicationGateway -ApplicationGateway $appGW

```

---

Refresh your browser multiple times and you should see connections to both myVM1 and myVM2.

## Clean up resources

When you no longer need the resources that you created with the application gateway, use the Azure portal, Azure CLI, or Azure PowerShell to delete the resource group. This removes the application gateway and all the related resources.

# [CLI](#tab/CLI)

```azurecli-interactive

az group delete --name exampleRG

```

# [PowerShell](#tab/PowerShell)

```azurepowershell-interactive

Remove-AzResourceGroup -Name exampleRG

```

---

## Next steps

> [!div class="nextstepaction"]

> [Tutorial: Create an application gateway with a Web Application Firewall using the Azure portal](application-gateway-web-application-firewall-portal.md)


# Quickstart Web Application Firewall Terraform

# Quickstart: Use Terraform to configure Azure Web Application Firewall v2 on Azure Application Gateway

In this quickstart, you use Terraform to create an Azure Application Gateway with an Azure Web Application Firewall (WAF) v2 policy. A key component of creating scalable, reliable, and secure web front ends in Azure, Application Gateway is a web traffic load balancer that helps you to manage traffic to your web applications. Application Gateway bases how it routes traffic on factors that include round-robin, cookie-based sessions, and more. In addition to an Application Gateway, this code also creates a resource group, virtual network, subnet within the virtual network, public IP address, and a WAF policy with custom rules to block traffic from a specific IP address.

[!INCLUDE [About Terraform](~/azure-dev-docs-pr/articles/terraform/includes/abstract.md)]

> [!div class="checklist"]

> * Define the IP address that the WAF custom rule should block.

> * Create an Azure resource group with a unique name.

> * Establish a virtual network with a specific name and address.

> * Generate a random name for the subnet, and create a subnet in the virtual network.

> * Generate a public IP address.

> * Create a WAF policy.

> * Configure settings and define managed rules for the WAF policy.

> * Create a custom rule to block traffic from a specific IP address.

> * Set up the Application Gateway.

> * Configure the SKU and capacity of the Application Gateway.

> * Enable autoscaling for the Application Gateway.

> * Configure the gateway's IP settings.

> * Set up the front-end IP configuration, and define the front-end port.

> * Define the back-end address pool with IP addresses, and configure back-end HTTP settings.

> * Define the HTTP listener.

> * Define the request routing rule.

> * Associate the WAF policy with the Application Gateway.

> * Output the resource group name, public IP address, Application Gateway ID, WAF policy ID, and Application Gateway.

## Prerequisites

- An Azure account with an active subscription. You can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- Terraform. For more information, see [Install and configure Terraform](/azure/developer/terraform/quickstart-configure).

## Implement the Terraform code

The sample code for this article is located in the [Azure Terraform GitHub repo](https://github.com/Azure/terraform/tree/master/quickstart/101-web-application-firewall). You can view the log file containing the [test results from current and previous versions of Terraform](https://github.com/Azure/terraform/tree/master/quickstart/101-web-application-firewall/TestRecord.md). See more [articles and sample code showing how to use Terraform to manage Azure resources](/azure/terraform).

1. Create a directory in which to test and run the sample Terraform code, and make it the current directory.

1. Create a file named `main.tf`, and insert the following code:

>[!NOTE]

> Use `waf_configuration` to define WAF settings directly on the Application Gateway. Use `firewall_policy_id` to associate an existing WAF policy resource with the Application Gateway. Only one method should be used in practice.

1. Create a file named `outputs.tf`, and insert the following code:

1. Create a file named `providers.tf`, and insert the following code:

1. Create a file named `variables.tf`, and insert the following code:

> [!IMPORTANT]

> If you're using the 4.x azurerm provider, you must [explicitly specify the Azure subscription ID](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/guides/4.0-upgrade-guide#specifying-subscription-id-is-now-mandatory) to authenticate to Azure before running the Terraform commands.

>

> One way to specify the Azure subscription ID without putting it in the `providers` block is to specify the subscription ID in an environment variable named `ARM_SUBSCRIPTION_ID`.

>

> For more information, see the [Azure provider reference documentation](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs#argument-reference).

## Initialize Terraform

[!INCLUDE [terraform-init.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-init.md)]

## Create a Terraform execution plan

[!INCLUDE [terraform-plan.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-plan.md)]

## Apply a Terraform execution plan

[!INCLUDE [terraform-apply-plan.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-apply-plan.md)]

## Verify the results

### [Azure CLI](#tab/azure-cli)

1. Get the Azure resource group name.

```console

resource_group_name=$(terraform output -raw resource_group_name)

```

1. Get the public IP address.

```console

public_ip_address=$(terraform output -raw public_ip_address)

```

1. Get the WAF policy ID.

```console

web_application_firewall_policy_id=$(terraform output -raw web_application_firewall_policy_id)

```

1. Get the Application Gateway ID.

```console

application_gateway_id=$(terraform output -raw application_gateway_id)

```

1. Run `az network application-gateway show` to view the Application Gateway.

```azurecli

az appservice ase show --name $application_gateway_name --resource-group $resource_group_name

```

### [Azure PowerShell](#tab/azure-powershell)

1. Get the Azure resource group name.

```console

$resource_group_name=$(terraform output -raw resource_group_name)

```

1. Get the public IP address.

```console

$public_ip_address=$(terraform output -public_ip_address)

```

1. Get the WAF policy ID.

```console

$web_application_firewall_policy_id=$(terraform output -web_application_firewall_policy_id)

```

1. Get the Application Gateway ID.

```console

$application_gateway_id=$(terraform output -application_gateway_id)

```

1. Run `Get-AzAppServiceEnvironment` to view the Application Gateway.

```azurepowershell

Get-AzApplicationGateway -Name $application_gateway_name -ResourceGroupName $resource_group_name

```

---

## Clean up resources

[!INCLUDE [terraform-plan-destroy.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-plan-destroy.md)]

## Troubleshoot Terraform on Azure

[Troubleshoot common problems when using Terraform on Azure](/azure/developer/terraform/troubleshoot).

## Related content

- [Create Web Application Firewall policies for Application Gateway](/azure/web-application-firewall/ag/create-waf-policy-ag)

- [Associate a WAF policy with an existing Application Gateway](/azure/web-application-firewall/ag/associate-waf-policy-existing-gateway)

- [Customize Web Application Firewall rules](/azure/web-application-firewall/ag/application-gateway-customize-waf-rules-portal)


# Waf Front Door Custom Rules Powershell

# Configure a WAF policy by using Azure PowerShell

A web application firewall (WAF) policy defines the inspections that are required when a request arrives at Azure Front Door.

This article shows how to configure a WAF policy that consists of some custom rules and has the Azure-managed Default Rule Set enabled.

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

Before you begin to set up a rate limit policy, set up your PowerShell environment and create an Azure Front Door profile.

### Set up your PowerShell environment

Azure PowerShell provides a set of cmdlets that use the [Azure Resource Manager](../../azure-resource-manager/management/overview.md) model for managing your Azure resources.

You can install [Azure PowerShell](/powershell/azure/) on your local machine and use it in any PowerShell session. Follow the instructions on the page to sign in with your Azure credentials. Then install the Az PowerShell module.

#### Sign in to Azure

```

Connect-AzAccount

```

Before you install the Azure Front Door module, make sure you have the current version of PowerShellGet installed. Run the following command and reopen PowerShell.

```

Install-Module PowerShellGet -Force -AllowClobber

```

#### Install the Az.FrontDoor module

```

Install-Module -Name Az.FrontDoor

```

### Create an Azure Front Door profile

Create an Azure Front Door profile by following the instructions described in [Quickstart: Create an Azure Front Door profile](../../frontdoor/quickstart-create-front-door.md).

## Custom rule based on HTTP parameters

The following example shows how to configure a custom rule with two match conditions by using [New-AzFrontDoorWafMatchConditionObject](/powershell/module/az.frontdoor/new-azfrontdoorwafmatchconditionobject). Requests are from a specified site as defined by referrer, and the query string doesn't contain `password`.

```powershell-interactive

$referer = New-AzFrontDoorWafMatchConditionObject -MatchVariable RequestHeader -OperatorProperty Equal -Selector "Referer" -MatchValue "www.mytrustedsites.com/referpage.html"

$password = New-AzFrontDoorWafMatchConditionObject -MatchVariable QueryString -OperatorProperty Contains -MatchValue "password"

$AllowFromTrustedSites = New-AzFrontDoorWafCustomRuleObject -Name "AllowFromTrustedSites" -RuleType MatchRule -MatchCondition $referer,$password -Action Allow -Priority 1

```

## Custom rule based on an HTTP request method

Create a rule blocking a PUT method by using [New-AzFrontDoorWafCustomRuleObject](/powershell/module/az.frontdoor/new-azfrontdoorwafcustomruleobject).

```powershell-interactive

$put = New-AzFrontDoorWafMatchConditionObject -MatchVariable RequestMethod -OperatorProperty Equal -MatchValue PUT

$BlockPUT = New-AzFrontDoorWafCustomRuleObject -Name "BlockPUT" -RuleType MatchRule -MatchCondition $put -Action Block -Priority 2

```

## Create a custom rule based on size constraint

The following example creates a rule blocking requests with a URL that's longer than 100 characters by using Azure PowerShell.

```powershell-interactive

$url = New-AzFrontDoorWafMatchConditionObject -MatchVariable RequestUri -OperatorProperty GreaterThanOrEqual -MatchValue 100

$URLOver100 = New-AzFrontDoorWafCustomRuleObject -Name "URLOver100" -RuleType MatchRule -MatchCondition $url -Action Block -Priority 3

```

## Add a managed Default Rule Set

The following example creates a managed Default Rule Set by using Azure PowerShell.

```powershell-interactive

$managedRules =  New-AzFrontDoorWafManagedRuleObject -Type DefaultRuleSet -Version 1.0

```

## Configure a security policy

Find the name of the resource group that contains the Azure Front Door profile by using `Get-AzResourceGroup`. Next, configure a security policy with created rules in the previous steps by using [New-AzFrontDoorWafPolicy](/powershell/module/az.frontdoor/new-azfrontdoorwafpolicy) in the specified resource group that contains the Azure Front Door profile.

```powershell-interactive

$myWAFPolicy=New-AzFrontDoorWafPolicy -Name $policyName -ResourceGroupName $resourceGroupName -Customrule $AllowFromTrustedSites,$BlockPUT,$URLOver100 -ManagedRule $managedRules -EnabledState Enabled -Mode Prevention

```

## Link policy to an Azure Front Door front-end host

Link the security policy object to an existing Azure Front Door front-end host and update Azure Front Door properties. First, retrieve the Azure Front Door object by using [Get-AzFrontDoor](/powershell/module/Az.FrontDoor/Get-AzFrontDoor).

Next, set the front-end `WebApplicationFirewallPolicyLink` property to the `resourceId` of the `$myWAFPolicy$` created in the previous step by using [Set-AzFrontDoor](/powershell/module/Az.FrontDoor/Set-AzFrontDoor).

> [!NOTE]

> For Azure Front Door Standard and Premium, you should use [Get-AzFrontDoorCdnProfile](/powershell/module/az.cdn/Get-AzFrontDoorCdnProfile).

The following example uses the resource group name `myResourceGroupFD1` with the assumption that you've created the Azure Front Door profile by using instructions provided in [Quickstart: Create an Azure Front Door](../../frontdoor/quickstart-create-front-door.md). Also, in the following example, replace `$frontDoorName` with the name of your Azure Front Door profile.

```powershell-interactive

$FrontDoorObjectExample = Get-AzFrontDoor `

-ResourceGroupName myResourceGroupFD1 `

-Name $frontDoorName

$FrontDoorObjectExample[0].FrontendEndpoints[0].WebApplicationFirewallPolicyLink = $myWAFPolicy.Id

Set-AzFrontDoor -InputObject $FrontDoorObjectExample[0]

```

> [!NOTE]

> You only need to set the `WebApplicationFirewallPolicyLink` property once to link a security policy to an Azure Front Door front end. Subsequent policy updates are automatically applied to the front end.

## Next steps

- Learn more about [Azure Front Door](../../frontdoor/front-door-overview.md).

- Learn more about [Azure Web Application Firewall on Azure Front Door](afds-overview.md).


# Policy Overview

# Azure Web Application Firewall (WAF) policy overview

**Applies to:** :heavy_check_mark: Application Gateway V2

Web Application Firewall Policies contain all the WAF settings and configurations. This includes exclusions, custom rules, managed rules, and so on. These policies are then associated to an application gateway (global), a listener (per-site), or a path-based rule (per-URI) for them to take effect.

There's no limit on the number of policies you can create. When you create a policy, it must be associated to an application gateway to take effect. It can be associated with any combination of application gateways, listeners, and path-based rules.

> [!Note]

> Application Gateway has two versions of the WAF SKU: Application Gateway WAF_v1 and Application Gateway WAF_v2. WAF policy associations are only supported for the Application Gateway WAF_v2 SKU.

## Global WAF policy

When you associate a WAF policy globally, every site behind your Application Gateway WAF is protected with the same managed rules, custom rules, exclusions, and any other configured settings.

If you want a single policy to apply to all sites, you can associate the policy with the application gateway. For more information, see [Create Web Application Firewall policies for Application Gateway](create-waf-policy-ag.md) to create and apply a WAF policy using the Azure portal.

## Per-site WAF policy

With per-site WAF policies, you can protect multiple sites with differing security needs behind a single WAF by using per-site policies. For example, if there are five sites behind your WAF, you can have five separate WAF policies (one for each listener) to customize the exclusions, custom rules, managed rule sets, and all other WAF settings for each site.

Say your application gateway has a global policy applied to it. Then you apply a different policy to a listener on that application gateway. The listener's policy now takes effect for just that listener. The application gateway’s global policy still applies to all other listeners and path-based rules that don't have a specific policy assigned to them.

## Per-URI policy

For even more customization down to the URI level, you can associate a WAF policy with a path-based rule. If there are certain pages within a single site that require different policies, you can make changes to the WAF policy that only affect a given URI. This might apply to a payment or sign-in page, or any other URIs that need an even more specific WAF policy than the other sites behind your WAF.

As with per-site WAF policies, more specific policies override less specific ones. This means a per-URI policy on a URL path map overrides any per-site or global WAF policy above it.

### Example

Say you have three sites: contoso.com, fabrikam.com, and adatum.com all behind the same application gateway. You want a WAF applied to all three sites, but you need added security with adatum.com because that's where customers visit, browse, and purchase products.

You can apply a global policy to the WAF, with some basic settings, exclusions, or custom rules if necessary to stop some false positives from blocking traffic. In this case, there's no need to have global SQL injection rules running because fabrikam.com and contoso.com are static pages with no SQL backend. So you can disable those rules in the global policy.

This global policy is suitable for contoso.com and fabrikam.com, but you need to be more careful with adatum.com where sign-in information and payments are handled. You can apply a per-site policy to the Adatum listener and leave the SQL rules running. Also assume there's a cookie blocking some traffic, so you can create an exclusion for that cookie to stop the false positive.

The adatum.com/payments URI is where you need to be careful. So apply another policy on that URI and leave all rules enabled, and also remove all exclusions.

In this example, you have a global policy that applies to two sites. You have a per-site policy that applies to one site, and then a per-URI policy that applies to one specific path-based rule. See [Configure per-site WAF policies using Azure PowerShell](per-site-policies.md) for the corresponding PowerShell for this example.

## Existing WAF configurations

All new Web Application Firewall's WAF settings (custom rules, managed rule set configurations, exclusions, and so on) exist in a WAF policy. If you have an existing WAF, these settings might still exist in your WAF configuration. For more information about moving to the new WAF policy, [Migrate WAF Config to a WAF Policy](./migrate-policy.md).

## Next steps

- [Create per-site and per-URI policies using Azure PowerShell](per-site-policies.md).


# Create Waf Policy Ag

# Create Web Application Firewall policies for Application Gateway

**Applies to:** :heavy_check_mark: Application Gateway V2

Associating a WAF policy with listeners allows for multiple sites behind a single WAF to be protected by different policies. For example, if there are five sites behind your WAF, you can have five separate WAF policies (one for each listener) to customize the exclusions, custom rules, and managed rulesets for one site without effecting the other four. If you want a single policy to apply to all sites, you can just associate the policy with the Application Gateway, rather than the individual listeners, to make it apply globally. Policies can also be applied to a path-based routing rule.

You can make as many policies as you want. Once you create a policy, it must be associated to an Application Gateway to go into effect, but it can be associated with any combination of Application Gateways and listeners.

If your Application Gateway has an associated policy, and then you associate a different policy to a listener on that Application Gateway, the listener's policy takes effect, but just for the listeners that they're assigned to. The Application Gateway policy still applies to all other listeners that don't have a specific policy assigned to them.

> [!NOTE]

> Once a Firewall Policy is associated to a WAF, there must always be a policy associated to that WAF. You can overwrite that policy, but disassociating a policy from the WAF entirely isn't supported.

All new Web Application Firewall's WAF settings (custom rules, managed ruleset configurations, exclusions, etc.) live inside of a WAF Policy. If you have an existing WAF, these settings might still exist in your WAF config. For steps on how to move to the new WAF Policy, see [Upgrade your WAF Config to a WAF Policy](#upgrade) later in this article.

WAF policies need to be in the enabled state to inspect request traffic, log events and take action on requests. WAF policies in detection mode log events when WAF rules are triggered, but doesn't take any other action. Policies in prevention mode take action on requests and log the event in the logs.

## Create a policy

First, create a basic WAF policy with a managed Default Rule Set (DRS) using the Azure portal.

1. On the upper left side of the portal, select **Create a resource**. Search for **WAF**, select **Web Application Firewall**, then select **Create**.

2. On **Create a WAF policy** page, **Basics** tab, enter or select the following information and accept the defaults for the remaining settings:

|Setting  |Value  |

|---------|---------|

|Policy for     |Regional WAF (Application Gateway)|

|Subscription     |Select your subscription name|

|Resource group     |Select your resource group|

|Policy name     |Type a unique name for your WAF policy.|

3. On the **Association** tab, select **Add association**, then select one of the following settings:

|Setting  |Value  |

|---------|---------|

|Application Gateway     |Select the application gateway, and then select **Add**.|

|HTTP Listener     |Select the application gateway, select the listeners, then select **Add**.|

|Route Path|Select the application gateway, select the listener, select the routing rule, and then select **Add**.

> [!NOTE]

> If you assign a policy to your Application Gateway (or listener) that already has a policy in place, the original policy is overwritten and replaced by the new policy.

4. Select **Review + create**, then select **Create**.

## Configure WAF rules (optional)

When you create a WAF policy, by default it is in *Detection* mode. In Detection mode, WAF doesn't block any requests. Instead, the matching WAF rules are logged in the WAF logs. To see WAF in action, you can change the mode settings to *Prevention*. In Prevention mode, matching rules defined in the Microsoft Managed Rulesets you selected are blocked and/or logged in the WAF logs.

## Managed rules

Azure-managed OWASP rules are enabled by default. To disable an individual rule within a rule group, expand the rules within that rule group, select the check box in front of the rule number, and select **Disable**.

## Custom rules

To create a custom rule, select **Add custom rule** under the **Custom rules** tab. This opens the custom rule configuration page. The following screenshot shows an example custom rule configured to block a request if the query string contains the text `blockme`.

## <a name="upgrade"></a>Upgrade your WAF Config to a WAF Policy

If you have an existing WAF, you might notice some changes in the portal. First you need to identify what kind of Policy you've enabled on your WAF. There are three potential states:

1. No WAF Policy

2. Custom Rules only Policy

3. WAF Policy

You can tell which state your WAF is in by looking at it in the portal. If the WAF settings are visible and can be changed from within the Application Gateway view, your WAF is in state 1.

[ ![WAF configuration](../media/create-waf-policy-ag/waf-configure.png) ](../media/create-waf-policy-ag/waf-configure-lrg.png#lightbox)

If you select **Web Application Firewall** and it shows you an associated policy, the WAF is in state 2 or state 3. After navigating to the policy, if it shows **only** custom rules, and Associated Application Gateways, then it's a Custom Rules only Policy.

![WAF custom rules](../media/create-waf-policy-ag/waf-custom-rules.png)

If it also shows Policy Settings and Managed Rules, then it's a full Web Application Firewall policy.

![Screenshot showing WAF policy settings.](../media/create-waf-policy-ag/waf-policy-settings.png)

## Upgrade to WAF Policy

If you have a Custom Rules only WAF Policy, then you might want to move to the new WAF Policy. A policy supports WAF policy settings, managed rulesets, exclusions, and disabled rule-groups. Essentially, all the WAF configurations that were previously done inside the Application Gateway are now done through the WAF Policy.

Edits to the custom rule only WAF policy are disabled. To edit any WAF settings such as disabling rules, adding exclusions, etc. you have to upgrade to a new top-level firewall policy resource.

To do so, create a *Web Application Firewall Policy* and associate it to your Application Gateways and listeners of choice. This new Policy must be exactly the same as the current WAF config, meaning every custom rule, exclusion, disabled rule, etc. must be copied into the new Policy you're creating. Once you have a Policy associated with your Application Gateway, then you can continue to make changes to your WAF rules and settings. You can also do this with Azure PowerShell. For more information, see [Associate a WAF policy with an existing Application Gateway](associate-waf-policy-existing-gateway.md).

Optionally, you can use a migration script to upgrade to a WAF policy. For more information, see [Upgrade Web Application Firewall policies using Azure PowerShell](migrate-policy.md).

## Force mode

If you don't want to copy everything into a policy that is exactly the same as your current config, you can set the WAF into "force" mode. Run the following Azure PowerShell code to put your WAF in force mode. Then you can associate any WAF Policy to your WAF, even if it doesn't have the exact same settings as your config.

```azurepowershell-interactive

$appgw = Get-AzApplicationGateway -Name <your Application Gateway name> -ResourceGroupName <your Resource Group name>

$appgw.ForceFirewallPolicyAssociation = $true

```

Then proceed with the steps to associate a WAF Policy to your application gateway. For more information, see [Associate a WAF Policy with an existing Application Gateway.](associate-waf-policy-existing-gateway.md)

## Next step

> [!div class="nextstepaction"]

> [Web Application Firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md)


# Per Site Policies

# Configure per-site WAF policies using Azure PowerShell

Web Application Firewall (WAF) settings are contained in WAF policies, and to change your WAF configuration you modify the WAF policy.

When associated with your Application Gateway, the policies and all the settings are reflected globally. So, if you have five sites behind your WAF, all five sites are protected by the same WAF Policy. This is great if you need the same security settings for every site. But you can also apply WAF policies to individual listeners to allow for site-specific WAF configuration.

By applying WAF policies to a listener, you can configure WAF settings for individual sites without the changes affecting every site. The most specific policy takes precedent. If there's a global policy, and a per-site policy (a WAF policy associated with a listener), then the per-site policy overrides the global WAF policy for that listener. Other listeners without their own policies will only be affected by the global WAF policy.

In this article, you learn how to:

* Set up the network

* Create a WAF policy

* Create an application gateway with WAF enabled

* Apply the WAF policy globally, per-site, and per-URI

* Create a virtual machine scale set

* Create a storage account and configure diagnostics

* Test the application gateway

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

[!INCLUDE [updated-for-az](~/reusable-content/ce-skilling/azure/includes/updated-for-az.md)]

[!INCLUDE [cloud-shell-try-it.md](~/reusable-content/ce-skilling/azure/includes/cloud-shell-try-it.md)]

If you choose to install and use the PowerShell locally, this article requires the Azure PowerShell module version 1.0.0 or later. Run `Get-Module -ListAvailable Az` to find the version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell). If you're running PowerShell locally, you also need to run `Login-AzAccount` to create a connection with Azure.

## Create a resource group

A resource group is a logical container into which Azure resources are deployed and managed. Create an Azure resource group using [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup).

```azurepowershell-interactive

$rgname = New-AzResourceGroup -Name myResourceGroupAG -Location eastus

```

## Create network resources

Create the subnet configurations named *myBackendSubnet* and *myAGSubnet* using [New-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/new-azvirtualnetworksubnetconfig). Create the virtual network named *myVNet* using [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork) with the subnet configurations. And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress). These resources are used to provide network connectivity to the application gateway and its associated resources.

```azurepowershell-interactive

$backendSubnetConfig = New-AzVirtualNetworkSubnetConfig `

-Name myBackendSubnet `

-AddressPrefix 10.0.1.0/24

$agSubnetConfig = New-AzVirtualNetworkSubnetConfig `

-Name myAGSubnet `

-AddressPrefix 10.0.2.0/24

$vnet = New-AzVirtualNetwork `

-ResourceGroupName myResourceGroupAG `

-Location eastus `

-Name myVNet `

-AddressPrefix 10.0.0.0/16 `

-Subnet $backendSubnetConfig, $agSubnetConfig

$pip = New-AzPublicIpAddress `

-ResourceGroupName myResourceGroupAG `

-Location eastus `

-Name myAGPublicIPAddress `

-AllocationMethod Static `

-Sku Standard

```

## Create an application gateway

In this section, you create resources that support the application gateway, and then finally create it and a WAF. The resources that you create include:

- *IP configurations and frontend port* - Associates the subnet that you previously created to the application gateway and assigns a port to use to access it.

- *Default pool* - All application gateways must have at least one backend pool of servers.

- *Default listener and rule* - The default listener listens for traffic on the port that was assigned and the default rule sends traffic to the default pool.

### Create the IP configurations and frontend port

Associate *myAGSubnet* that you previously created to the application gateway using [New-AzApplicationGatewayIPConfiguration](/powershell/module/az.network/new-azapplicationgatewayipconfiguration). Assign *myAGPublicIPAddress* to the application gateway using [New-AzApplicationGatewayFrontendIPConfig](/powershell/module/az.network/new-azapplicationgatewayfrontendipconfig).

```azurepowershell-interactive

$vnet = Get-AzVirtualNetwork `

-ResourceGroupName myResourceGroupAG `

-Name myVNet

$subnet=$vnet.Subnets[1]

$gipconfig = New-AzApplicationGatewayIPConfiguration `

-Name myAGIPConfig `

-Subnet $subnet

$fipconfig = New-AzApplicationGatewayFrontendIPConfig `

-Name myAGFrontendIPConfig `

-PublicIPAddress $pip

$frontendport80 = New-AzApplicationGatewayFrontendPort `

-Name myFrontendPort `

-Port 80

$frontendport8080 = New-AzApplicationGatewayFrontendPort `

-Name myFrontendPort `

-Port 8080

```

### Create the backend pool and settings

Create the backend pool named *appGatewayBackendPool* for the application gateway using [New-AzApplicationGatewayBackendAddressPool](/powershell/module/az.network/new-azapplicationgatewaybackendaddresspool). Configure the settings for the backend address pools using [New-AzApplicationGatewayBackendHttpSettings](/powershell/module/az.network/new-azapplicationgatewaybackendhttpsetting).

```azurepowershell-interactive

$defaultPool = New-AzApplicationGatewayBackendAddressPool `

-Name appGatewayBackendPool

$poolSettings = New-AzApplicationGatewayBackendHttpSettings `

-Name myPoolSettings `

-Port 80 `

-Protocol Http `

-CookieBasedAffinity Enabled `

-RequestTimeout 120

```

### Create two WAF policies

Create two WAF policies, one global and one per-site, and add custom rules.

The per-site policy restricts the file upload limit to 5 MB. Everything else is the same.

```azurepowershell-interactive

$variable = New-AzApplicationGatewayFirewallMatchVariable -VariableName RequestUri

$condition = New-AzApplicationGatewayFirewallCondition -MatchVariable $variable -Operator Contains -MatchValue "globalAllow"

$rule = New-AzApplicationGatewayFirewallCustomRule -Name globalAllow -Priority 5 -RuleType MatchRule -MatchCondition $condition -Action Allow

$variable1 = New-AzApplicationGatewayFirewallMatchVariable -VariableName RequestUri

$condition1 = New-AzApplicationGatewayFirewallCondition -MatchVariable $variable1 -Operator Contains -MatchValue "globalBlock"

$rule1 = New-AzApplicationGatewayFirewallCustomRule -Name globalBlock -Priority 10 -RuleType MatchRule -MatchCondition $condition1 -Action Block

$variable2 = New-AzApplicationGatewayFirewallMatchVariable -VariableName RequestUri

$condition2 = New-AzApplicationGatewayFirewallCondition -MatchVariable $variable2 -Operator Contains -MatchValue "siteAllow"

$rule2 = New-AzApplicationGatewayFirewallCustomRule -Name siteAllow -Priority 5 -RuleType MatchRule -MatchCondition $condition2 -Action Allow

$variable3 = New-AzApplicationGatewayFirewallMatchVariable -VariableName RequestUri

$condition3 = New-AzApplicationGatewayFirewallCondition -MatchVariable $variable3 -Operator Contains -MatchValue "siteBlock"

$rule3 = New-AzApplicationGatewayFirewallCustomRule -Name siteBlock -Priority 10 -RuleType MatchRule -MatchCondition $condition3 -Action Block

$variable4 = New-AzApplicationGatewayFirewallMatchVariable -VariableName RequestUri

$condition4 = New-AzApplicationGatewayFirewallCondition -MatchVariable $variable4 -Operator Contains -MatchValue "URIAllow"

$rule4 = New-AzApplicationGatewayFirewallCustomRule -Name URIAllow -Priority 5 -RuleType MatchRule -MatchCondition $condition4 -Action Allow

$variable5 = New-AzApplicationGatewayFirewallMatchVariable -VariableName RequestUri

$condition5 = New-AzApplicationGatewayFirewallCondition -MatchVariable $variable5 -Operator Contains -MatchValue "URIBlock"

$rule5 = New-AzApplicationGatewayFirewallCustomRule -Name URIBlock -Priority 10 -RuleType MatchRule -MatchCondition $condition5 -Action Block

$policySettingGlobal = New-AzApplicationGatewayFirewallPolicySetting `

-Mode Prevention `

-State Enabled `

-MaxRequestBodySizeInKb 100 `

-MaxFileUploadInMb 256

$wafPolicyGlobal = New-AzApplicationGatewayFirewallPolicy `

-Name wafpolicyGlobal `

-ResourceGroup myResourceGroupAG `

-Location eastus `

-PolicySetting $PolicySettingGlobal `

-CustomRule $rule, $rule1

$policySettingSite = New-AzApplicationGatewayFirewallPolicySetting `

-Mode Prevention `

-State Enabled `

-MaxRequestBodySizeInKb 100 `

-MaxFileUploadInMb 5

$wafPolicySite = New-AzApplicationGatewayFirewallPolicy `

-Name wafpolicySite `

-ResourceGroup myResourceGroupAG `

-Location eastus `

-PolicySetting $PolicySettingSite `

-CustomRule $rule2, $rule3

```

### Create the default listener and rule

A listener is required to enable the application gateway to route traffic appropriately to the backend address pools. In this example, you create a basic listener that listens for traffic at the root URL.

Create a listener named *mydefaultListener* using [New-AzApplicationGatewayHttpListener](/powershell/module/az.network/new-azapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created. A rule is required for the listener to know which backend pool to use for incoming traffic. Create a basic rule named *rule1* using [New-AzApplicationGatewayRequestRoutingRule](/powershell/module/az.network/new-azapplicationgatewayrequestroutingrule).

```azurepowershell-interactive

$globalListener = New-AzApplicationGatewayHttpListener `

-Name mydefaultListener `

-Protocol Http `

-FrontendIPConfiguration $fipconfig `

-FrontendPort $frontendport80

$frontendRule = New-AzApplicationGatewayRequestRoutingRule `

-Name rule1 `

-RuleType Basic `

-HttpListener $globallistener `

-BackendAddressPool $defaultPool `

-BackendHttpSettings $poolSettings

$siteListener = New-AzApplicationGatewayHttpListener `

-Name mydefaultListener `

-Protocol Http `

-FrontendIPConfiguration $fipconfig `

-FrontendPort $frontendport8080 `

-FirewallPolicy $wafPolicySite

$frontendRuleSite = New-AzApplicationGatewayRequestRoutingRule `

-Name rule2 `

-RuleType Basic `

-HttpListener $siteListener `

-BackendAddressPool $defaultPool `

-BackendHttpSettings $poolSettings

```

### Create the application gateway with the WAF

Now that you created the necessary supporting resources, specify parameters for the application gateway using [New-AzApplicationGatewaySku](/powershell/module/az.network/new-azapplicationgatewaysku). Specify the Firewall Policy using [New-AzApplicationGatewayFirewallPolicy](/powershell/module/az.network/new-azapplicationgatewayfirewallpolicy). And then create the application gateway named *myAppGateway* using [New-AzApplicationGateway](/powershell/module/az.network/new-azapplicationgateway).

```azurepowershell-interactive

$sku = New-AzApplicationGatewaySku `

-Name WAF_v2 `

-Tier WAF_v2 `

-Capacity 2

$appgw = New-AzApplicationGateway `

-Name myAppGateway `

-ResourceGroupName myResourceGroupAG `

-Location eastus `

-BackendAddressPools $defaultPool `

-BackendHttpSettingsCollection $poolSettings `

-FrontendIpConfigurations $fipconfig `

-GatewayIpConfigurations $gipconfig `

-FrontendPorts $frontendport80 `

-HttpListeners $globallistener `

-RequestRoutingRules $frontendRule `

-Sku $sku `

-FirewallPolicy $wafPolicyGlobal

```

### Apply a per-URI policy

To apply a per-URI policy, simply create a new policy and apply it to the path rule config.

```azurepowershell-interactive

$policySettingURI = New-AzApplicationGatewayFirewallPolicySetting `

-Mode Prevention `

-State Enabled `

-MaxRequestBodySizeInKb 100 `

-MaxFileUploadInMb 5

$wafPolicyURI = New-AzApplicationGatewayFirewallPolicy `

-Name wafPolicyURI `

-ResourceGroup myResourceGroupAG `

-Location eastus `

-PolicySetting $PolicySettingURI `

-CustomRule $rule4, $rule5

$appgw = Get-AzApplicationGateway `

-ResourceGroupName myResourceGroupAG `

-Name myAppGateway

$PathRuleConfig = New-AzApplicationGatewayPathRuleConfig -Name "base" `

-Paths "/base" `

-BackendAddressPool $defaultPool `

-BackendHttpSettings $poolSettings `

-FirewallPolicy $wafPolicyURI

$PathRuleConfig1 = New-AzApplicationGatewayPathRuleConfig `

-Name "base" -Paths "/test" `

-BackendAddressPool $defaultPool `

-BackendHttpSettings $poolSettings

$URLPathMap = New-AzApplicationGatewayUrlPathMapConfig -Name "PathMap" `

-PathRules $PathRuleConfig, $PathRuleConfig1 `

-DefaultBackendAddressPoolId $defaultPool.Id `

-DefaultBackendHttpSettingsId $poolSettings.Id

Add-AzApplicationGatewayRequestRoutingRule -ApplicationGateway $appgw `

-Name "RequestRoutingRule" `

-RuleType PathBasedRouting `

-HttpListener $siteListener `

-UrlPathMap $URLPathMap

```

## Create a virtual machine scale set

In this example, you create a virtual machine scale set to provide servers for the backend pool in the application gateway. You assign the scale set to the backend pool when you configure the IP settings.

Replace your own values for `-AdminUsername` and `-AdminPassword`.

```azurepowershell-interactive

$vnet = Get-AzVirtualNetwork `

-ResourceGroupName myResourceGroupAG `

-Name myVNet

$appgw = Get-AzApplicationGateway `

-ResourceGroupName myResourceGroupAG `

-Name myAppGateway

$backendPool = Get-AzApplicationGatewayBackendAddressPool `

-Name appGatewayBackendPool `

-ApplicationGateway $appgw

$ipConfig = New-AzVmssIpConfig `

-Name myVmssIPConfig `

-SubnetId $vnet.Subnets[0].Id `

-ApplicationGatewayBackendAddressPoolsId $backendPool.Id

$vmssConfig = New-AzVmssConfig `

-Location eastus `

-SkuCapacity 2 `

-SkuName Standard_DS2 `

-UpgradePolicyMode Automatic

Set-AzVmssStorageProfile $vmssConfig `

-ImageReferencePublisher MicrosoftWindowsServer `

-ImageReferenceOffer WindowsServer `

-ImageReferenceSku 2016-Datacenter `

-ImageReferenceVersion latest `

-OsDiskCreateOption FromImage

Set-AzVmssOsProfile $vmssConfig `

-AdminUsername <username> `

-AdminPassword <password> `

-ComputerNamePrefix myvmss

Add-AzVmssNetworkInterfaceConfiguration `

-VirtualMachineScaleSet $vmssConfig `

-Name myVmssNetConfig `

-Primary $true `

-IPConfiguration $ipConfig

New-AzVmss `

-ResourceGroupName myResourceGroupAG `

-Name myvmss `

-VirtualMachineScaleSet $vmssConfig

```

### Install IIS

```azurepowershell-interactive

$publicSettings = @{ "fileUris" = (,"https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/appgatewayurl.ps1");

"commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File appgatewayurl.ps1" }

$vmss = Get-AzVmss -ResourceGroupName myResourceGroupAG -VMScaleSetName myvmss

Add-AzVmssExtension -VirtualMachineScaleSet $vmss `

-Name "customScript" `

-Publisher "Microsoft.Compute" `

-Type "CustomScriptExtension" `

-TypeHandlerVersion 1.8 `

-Setting $publicSettings

Update-AzVmss `

-ResourceGroupName myResourceGroupAG `

-Name myvmss `

-VirtualMachineScaleSet $vmss

```

## Create a storage account and configure diagnostics

In this article, the application gateway uses a storage account to store data for detection and prevention purposes. You could also use Azure Monitor logs or Event Hub to record data.

### Create the storage account

Create a storage account named *myagstore1* using [New-AzStorageAccount](/powershell/module/az.storage/new-azstorageaccount).

```azurepowershell-interactive

$storageAccount = New-AzStorageAccount `

-ResourceGroupName myResourceGroupAG `

-Name myagstore1 `

-Location eastus `

-SkuName "Standard_LRS"

```

### Configure diagnostics

Configure diagnostics to record data into the ApplicationGatewayAccessLog, ApplicationGatewayPerformanceLog, and ApplicationGatewayFirewallLog logs using [Set-AzDiagnosticSetting](/powershell/module/az.monitor/set-azdiagnosticsetting).

```azurepowershell-interactive

$appgw = Get-AzApplicationGateway `

-ResourceGroupName myResourceGroupAG `

-Name myAppGateway

$store = Get-AzStorageAccount `

-ResourceGroupName myResourceGroupAG `

-Name myagstore1

Set-AzDiagnosticSetting `

-ResourceId $appgw.Id `

-StorageAccountId $store.Id `

-Category ApplicationGatewayAccessLog, ApplicationGatewayPerformanceLog, ApplicationGatewayFirewallLog `

-Enabled $true `

-RetentionEnabled $true `

-RetentionInDays 30

```

## Test the application gateway

You can use [Get-AzPublicIPAddress](/powershell/module/az.network/get-azpublicipaddress) to get the public IP address of the application gateway. Then use this IP address to curl against (replace the 1.1.1.1 shown below).

```azurepowershell-interactive

Get-AzPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress

#should be blocked

curl 1.1.1.1/globalBlock

curl 1.1.1.1/?1=1

#should be allowed

curl 1.1.1.1/globalAllow?1=1

#should be blocked

curl 1.1.1.1:8080/siteBlock

curl 1.1.1.1/?1=1

#should be allowed

curl 1.1.1.1:8080/siteAllow?1=1

#should be blocked

curl 1.1.1.1/URIBlock

curl 1.1.1.1/?1=1

#should be allowed

curl 1.1.1.1/URIAllow?1=1

```

![Test base URL in application gateway](../media/tutorial-restrict-web-traffic-powershell/application-gateway-iistest.png)

## Clean up resources

When no longer needed, remove the resource group, application gateway, and all related resources using [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup).

```azurepowershell-interactive

Remove-AzResourceGroup -Name myResourceGroupAG

```

## Next steps

[Customize web application firewall rules](application-gateway-customize-waf-rules-portal.md)


# Associate Waf Policy Existing Gateway

# Associate a WAF policy with an existing Application Gateway

You can use Azure PowerShell to [create a WAF Policy](create-waf-policy-ag.md), but you might already have an Application Gateway and just want to associate a WAF Policy to it. In this article, you do just that; you create a WAF Policy and associate it to an already existing Application Gateway.

> [!NOTE]

> The WAF policy must be in the same region and subscription as the Application Gateway for it to be associated.

1. Get your Application Gateway and Firewall Policy. If you don't have an existing Firewall Policy, see step 2.

```azurepowershell-interactive

Connect-AzAccount

Select-AzSubscription -Subscription "<sub id>"`

#Get Application Gateway and existing policy object or create new`

$gw = Get-AzApplicationGateway -Name <Waf v2> -ResourceGroupName <RG name>`

$policy = Get-AzApplicationGatewayFirewallPolicy -Name <policy name> -ResourceGroupName <RG name>`

```

2. (Optional) Create a Firewall Policy.

```azurepowershell-interactive

New-AzApplicationGatewayFirewallPolicy -Name <policy name> -ResourceGroupName <RG name>'

$policy = Get-AzApplicationGatewayFirewallPolicy -Name <policy name> -ResourceGroupName <RG name>`

```

> [!NOTE]

> If you are creating this WAF Policy to transition from a WAF Config to a WAF Policy, then the Policy needs to be an exact copy of your old Config. This means that every exclusion, custom rule, disabled rule group, etc. needs to be the exact same as it is in the WAF Config.

3. (Optional) You can configure the WAF policy to suit your needs. This includes custom rules, disabling rules/rule groups, exclusions,    setting file upload limits, etc. If you skip this step, all defaults will be selected.

4. Save the policy, and attach it to your Application Gateway.

```azurepowershell-interactive

#Save the policy itself

Set-AzApplicationGatewayFirewallPolicy -InputObject $policy`

#Attach the policy to an Application Gateway

$gw.FirewallPolicy = $policy`

#Save the Application Gateway

Set-AzApplicationGateway -ApplicationGateway $gw`

```

## Next steps

[Learn about Custom Rules.](configure-waf-custom-rules.md)


# Upgrade Ag Waf Policy

# Upgrade to Azure Application Gateway WAF policy

**Applies to:** :heavy_check_mark: Application Gateway V2

> [!IMPORTANT]

> On **March 15, 2024**, Microsoft announced the deprecation of WAF configuration on Application Gateway WAF V2 SKU. WAF configuration on Application Gateway WAF v2 retires on **March 15, 2027**. Microsoft isn't making any further investments in WAF configuration on Application Gateway WAF v2. Upgrade from WAF Configuration to **WAF Policy** for easier management, better scale, and a richer feature set at no extra cost. For more information, see [Retirement: Support for Application Gateway Web Application Firewall v2 Configuration is ending](https://azure.microsoft.com/updates/retirement-support-for-application-gateway-web-application-firewall-v2-configuration-is-ending).

Azure Web Application Firewall (WAF) provides centralized protection for your web applications from common exploits and vulnerabilities. Web Application Firewall policies contain all the WAF settings and configurations. This configuration includes exclusions, custom rules, managed rules, and more. Associate these policies with an application gateway (global), a listener (per-site), or a path-based rule (per-URI) for them to take effect.

Azure Application Gateway WAF v2 natively supports WAF policy. Upgrade your legacy WAF configuration to WAF policies.

- Policies offer a richer set of advanced features. This set includes newer managed rule sets, custom rules, per rule exclusions, bot protection, and the next generation of WAF engine. You get these advanced features at no extra cost.

- WAF policies provide higher scale and better performance.

- Unlike legacy WAF configuration, you can define WAF policies once and share them across multiple gateways, listeners, and URL paths. This sharing simplifies the management and deployment experience.

- The latest features and future enhancements are only available through WAF policies.

## Retirement timelines

- Deprecation announcement: March 15, 2024

- No creation of new WAF configuration deployments: March 15, 2025. The ability to create new WAF configuration deployments on the Application Gateway WAF V2 SKU is discontinued.

- Retirement: March 15, 2027

## Upgrade Application Gateway Standard v2 to Application Gateway WAF v2

1. Locate the Application Gateway in the Azure portal. Select the Application Gateway. From the **Settings** menu, select **Configuration**.

1. Under **Tier**, select **WAF V2**.

1. Select **Save** to complete the upgrade from Application Gateway Standard to Application Gateway WAF.

## Upgrade WAF v2 with legacy WAF configuration to WAF policy

You can upgrade existing Application Gateways with WAF v2 from WAF legacy configuration to WAF policy directly without any downtime. You can upgrade by using the portal, Firewall Manager, or Azure PowerShell.

# [Portal](#tab/portal)

1. Sign in to the Azure portal and select the Application Gateway WAF v2 that has a legacy WAF configuration.

1. Select **Web Application Firewall** from the left menu, and then select **Upgrade from WAF configuration**.

1. Enter a name for the new WAF policy and then select **Upgrade**. This action creates a new WAF policy based on the WAF configuration. You can also choose to associate an existing WAF policy instead of creating a new one.

1. When the upgrade finishes, a new WAF policy incorporating the previous WAF configuration and rules is created.

# [Firewall Manager](#tab/fwm)

See [Configure WAF policies using Azure Firewall Manager](../shared/manage-policies.md).

# [PowerShell](#tab/powershell)

See [Upgrade Web Application Firewall policies using Azure PowerShell](migrate-policy.md).

---

## Upgrade Application Gateway v1 to WAF v2 with WAF policy

> [!IMPORTANT]

> Microsoft announced the deprecation of the Application Gateway V1 SKU (Standard and WAF) on April 28, 2023. This version retires on April 28, 2026. For more information, see [Migrate your Application Gateways from V1 SKU to V2 SKU by April 28, 2026](../../application-gateway/v1-retirement.md).

Application Gateway v1 doesn't support WAF policy. Upgrading to WAF policy is a two-step process:

- Upgrade Application Gateway v1 to v2 version.

- Upgrade legacy WAF configuration to WAF policy.

1. Upgrade from v1 to v2 Application Gateway.

For more information, see [Upgrade Azure Application Gateway and Web Application Firewall from v1 to v2](../../application-gateway/migrate-v1-v2.md).

When you complete the upgrade of v1 to v2, the Application Gateway v2 has a legacy WAF configuration.

1. Upgrade to Application Gateway WAF v2 with WAF Policy.

- If in Step 1 you upgraded from Application Gateway Standard v1 to v2, see the previous section [Upgrade Application Gateway Standard v2 to Application Gateway WAF v2](#upgrade-application-gateway-standard-v2-to-application-gateway-waf-v2).

- If in Step 1, you upgraded from Application Gateway WAF v1 to Application Gateway WAF v2 with legacy configuration, see the previous section [Upgrade WAF v2 with legacy WAF configuration to WAF policy](#upgrade-waf-v2-with-legacy-waf-configuration-to-waf-policy) to migrate to Application Gateway WAF v2 SKU with WAF policy.

## Related content

- [Azure Web Application Firewall (WAF) policy overview](policy-overview.md)

- [Application Gateway V1 SKU retirement](../../application-gateway/v1-retirement.md)


# Migrate Policy

# Upgrade Web Application Firewall policies using Azure PowerShell

This script makes it easy to transition from a WAF config, or a custom rules-only WAF policy, to a full WAF policy. You might see a warning in the portal that says *upgrade to WAF policy*, or you might want the new WAF features such as Geomatch custom rules, per-site WAF policy, and per-URI WAF policy, or the bot mitigation ruleset. To use any of these features, you need a full WAF policy associated to your application gateway.

For more information about creating a new WAF policy, see [Create Web Application Firewall policies for Application Gateway](create-waf-policy-ag.md). For information about migrating, see [upgrade to WAF policy](create-waf-policy-ag.md#upgrade-to-waf-policy).

## To upgrade to WAF policy using the migration script

Use the following steps to run the migration script:

1. Open the following  Cloud Shell window, or open one from within the portal.

2. Copy the script into the Cloud Shell window and run it.

3. The script asks for Subscription ID, Resource Group name, the name of the Application Gateway that the WAF config is associated with, and the name of the new WAF policy that you create. Once you enter these inputs, the script  runs and creates your new WAF policy

4. Verify the new WAF policy is associated with your application gateway. Go to the WAF policy in the portal and select the **Associated Application Gateways** tab. Verify the Application Gateway is associated with the WAF policy.

> [!NOTE]

> The script does not complete a migration if the following conditions exist:

> - An entire ruleset is disabled. To complete a migration, make sure an entire rulegroup is not disabled.

>

> For more information, see the *ValidateInput* function in the script.

```azurepowershell-interactive

<#PSScriptInfo

.DESCRIPTION

Will be used to upgrade to the application-gateway to a top level waf policy experience.

.VERSION 1.0

.GUID b6fedd43-ebd0-41ed-9847-4f1c1c43be22

.AUTHOR Venkat.Krishnan

.PARAMETER subscriptionId

Subscription Id of where the resources are present.

.PARAMETER resourceGroupName

Resource-group where the resources are present.

.PARAMETER applicationGatewayName

Application-Gateway name

.PARAMETER wafPolicyName

Name of the web application firewall policy

.EXAMPLE

./migrateToWafPolicy.ps1 -subscriptionId  <your-subscription-id> -applicationGatewayName <your-appgw-name> -resourceGroupName <your-resource-group-name> -wafPolicyName <new-waf-policy-name>

#>

param(

[Parameter(Mandatory=$true)]

[string] $subscriptionId,

[Parameter(Mandatory=$true)]

[string] $resourceGroupName,

[Parameter(Mandatory=$true)]

[string] $applicationGatewayName,

[Parameter(Mandatory=$true)]

[string] $wafPolicyName

)

function ValidateInput ($appgwName, $resourceGroupName) {

# Obtain the application-gateway

$appgw = Get-AzApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName

if (-not $appgw) {

Write-Error "ApplicationGateway: $applicationGatewayName is not present in ResourceGroup: $resourceGroupName"

return $false

}

# Check if already have a global firewall policy

if ($appgw.FirewallPolicy) {

$fp = Get-AzResource -ResourceId $appgw.FirewallPolicy.Id

if ($fp.PolicySettings) {

Write-Error "ApplicationGateway: $applicationGatewayName already has a global firewall policy: $fp.Name. Please use portal for changing the policy."

return $false

}

}

if ($appgw.WebApplicationFirewallConfiguration) {

# Throw an error, since ruleGroup disabled case can't be migrated now.

if ($appgw.WebApplicationFirewallConfiguration.DisabledRuleGroups) {

foreach ($disabled in $appgw.WebApplicationFirewallConfiguration.DisabledRuleGroups) {

if ($disabled.Rules.Count -eq 0) {

$ruleGroupName = $disabled.RuleGroupName

Write-Error "The ruleGroup '$ruleGroupName' is disabled. Currently we can't upgrade to a firewall policy when an entire ruleGroup is disabled. This feature will be delivered shortly. To continue, kindly ensure the entire rulegroups are not disabled. "

return $false

}

}

}

}

if ($appgw.Sku.Name -ne "WAF_v2" -or $appgw.Sku.Tier -ne "WAF_v2") {

Write-Error " Cannot associate a firewall policy to application gateway :$applicationGatewayName since the Sku is not on WAF_v2"

return $false

}

return $true

}

function Login() {

$context = Get-AzContext

if ($null -eq $context -or $null -eq $context.Account) {

Login-AzAccount

}

}

function createNewTopLevelWafPolicy ($subscriptionId, $resourceGroupName, $applicationGatewayName, $wafPolicyName) {

Select-AzSubscription -Subscription $subscriptionId

$retVal = ValidateInput -appgwName $applicationGatewayName -resourceGroupName $resourceGroupName

if (!$retVal) {

return

}

$appgw = Get-AzApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName

# Get the managedRule and PolicySettings

$managedRule = New-AzApplicationGatewayFirewallPolicyManagedRule

$policySetting = New-AzApplicationGatewayFirewallPolicySetting

if ($appgw.WebApplicationFirewallConfiguration) {

$ruleGroupOverrides = [System.Collections.ArrayList]@()

if ($appgw.WebApplicationFirewallConfiguration.DisabledRuleGroups) {

foreach ($disabled in $appgw.WebApplicationFirewallConfiguration.DisabledRuleGroups) {

$rules = [System.Collections.ArrayList]@()

if ($disabled.Rules.Count -gt 0) {

foreach ($rule in $disabled.Rules) {

$ruleOverride = New-AzApplicationGatewayFirewallPolicyManagedRuleOverride -RuleId $rule

$_ = $rules.Add($ruleOverride)

}

}

$ruleGroupOverride = New-AzApplicationGatewayFirewallPolicyManagedRuleGroupOverride -RuleGroupName $disabled.RuleGroupName -Rule $rules

$_ = $ruleGroupOverrides.Add($ruleGroupOverride)

}

}

$managedRuleSet = New-AzApplicationGatewayFirewallPolicyManagedRuleSet -RuleSetType $appgw.WebApplicationFirewallConfiguration.RuleSetType -RuleSetVersion $appgw.WebApplicationFirewallConfiguration.RuleSetVersion

if ($ruleGroupOverrides.Count -ne 0) {

$managedRuleSet = New-AzApplicationGatewayFirewallPolicyManagedRuleSet -RuleSetType $appgw.WebApplicationFirewallConfiguration.RuleSetType -RuleSetVersion $appgw.WebApplicationFirewallConfiguration.RuleSetVersion -RuleGroupOverride $ruleGroupOverrides

}

$exclusions = [System.Collections.ArrayList]@()

if ($appgw.WebApplicationFirewallConfiguration.Exclusions) {

foreach ($excl in $appgw.WebApplicationFirewallConfiguration.Exclusions) {

if ($excl.MatchVariable -and $excl.SelectorMatchOperator -and $excl.Selector) {

$exclusionEntry = New-AzApplicationGatewayFirewallPolicyExclusion -MatchVariable  $excl.MatchVariable -SelectorMatchOperator $excl.SelectorMatchOperator -Selector $excl.Selector

$_ = $exclusions.Add($exclusionEntry)

}

if ($excl.MatchVariable -and !$excl.SelectorMatchOperator -and !$excl.Selecto) {

# Equals Any exclusion

$exclusionEntry = New-AzApplicationGatewayFirewallPolicyExclusion -MatchVariable  $excl.MatchVariable -SelectorMatchOperator "EqualsAny" -Selector "*"

$_ = $exclusions.Add($exclusionEntry)

}

}

}

$managedRule = New-AzApplicationGatewayFirewallPolicyManagedRule -ManagedRuleSet $managedRuleSet

$exclCount = $exclusions.Count

if ($exclCount -ne 0) {

$managedRule = New-AzApplicationGatewayFirewallPolicyManagedRule -ManagedRuleSet $managedRuleSet -Exclusion $exclusions

}

$policySetting = New-AzApplicationGatewayFirewallPolicySetting -MaxFileUploadInMb $appgw.WebApplicationFirewallConfiguration.FileUploadLimitInMb -MaxRequestBodySizeInKb $appgw.WebApplicationFirewallConfiguration.MaxRequestBodySizeInKb -Mode Detection -State Disabled

if ($appgw.WebApplicationFirewallConfiguration.FirewallMode -eq "Prevention") {

$policySetting.Mode = "Prevention"

}

if ($appgw.WebApplicationFirewallConfiguration.Enabled) {

$policySetting.State = "Enabled"

}

$policySetting.RequestBodyCheck = $appgw.WebApplicationFirewallConfiguration.RequestBodyCheck;

}

if ($appgw.FirewallPolicy) {

$customRulePolicyId = $appgw.FirewallPolicy.Id

$rg = Get-AzResourceGroup -Name $resourceGroupName

$crPolicyName = $customRulePolicyId.Substring($customRulePolicyId.LastIndexOf("/") + 1)

$customRulePolicy = Get-AzApplicationGatewayFirewallPolicy -ResourceGroupName $rg.ResourceGroupName -Name $crPolicyName

$wafPolicy = New-AzApplicationGatewayFirewallPolicy -ResourceGroupName $rg.ResourceGroupName -Name $wafPolicyName -CustomRule $customRulePolicy.CustomRules -ManagedRule $managedRule -PolicySetting $policySetting -Location $appgw.Location

} else {

$wafPolicy = New-AzApplicationGatewayFirewallPolicy -Name $wafPolicyName -ResourceGroupName $resourceGroupName -PolicySetting $policySetting -ManagedRule $managedRule -Location $appgw.Location

}

if (!$wafPolicy) {

return

}

$appgw.WebApplicationFirewallConfiguration = $null

$appgw.FirewallPolicy = $wafPolicy

$appgw = Set-AzApplicationGateway -ApplicationGateway $appgw

Write-Host " firewallPolicy: $wafPolicyName has been created/updated successfully and applied to applicationGateway: $applicationGatewayName!"

return $wafPolicy

}

function Main() {

Login

$policy = createNewTopLevelWafPolicy -subscriptionId $subscriptionId -resourceGroupName $resourceGroupName -applicationGatewayName $applicationGatewayName -wafPolicyName $wafPolicyName

return $policy

}

Main

```

## Next steps

Learn more about [Web Application Firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).


# Ruleset Support Policy

# Azure Web Application Firewall managed ruleset support policy

Azure Web Application Firewall supports a defined set of managed ruleset versions to ensure strong security protections, predictable behavior, and a clear upgrade path for customers. Azure manages the Default Rule Set (DRS), selected Core Rule Set (CRS) versions, Bot Management and HTTP DDoS rulesets, and periodically releases new rule set versions that include new protections, updated signatures, and rule improvements.

Azure Web Application Firewall supports a defined set of managed ruleset versions to ensure strong security protections, predictable behavior, and a clear upgrade path for customers. Azure manages the Default Rule Set (DRS), Bot Management, and HTTP DDoS rulesets versions and periodically releases new rule set versions that include new protections, updated signatures, and rule improvements.

## Supported versions

Starting February 2026, Azure WAF actively **supports the latest three ruleset releases** in the following format:

- **N:** Latest available rule set version (for example, **DRS 2.2**)

- **N-1:** Previous rule set version (for example, **DRS 2.1**)

- **N-2:** Second previous rule set version (for example, **CRS 3.2**)

- **N-2:** Second previous rule set version (for example, **DRS 2.0**)

Only **N, N-1, and N-2 versions** are supported for general use and receive ongoing updates, improvements, and rule tuning from the Azure WAF team.

## Extended support for older rule sets

When a newer rule set version (**N**) is released to general availability, the ruleset that becomes **N-3** will enter a **final support phase**:

- Once the newer ruleset version (N) is released, new Azure WAF policies can't be created with the **N-3** version, and any existing WAF policies with the N-3 version can't be attached.

- Once the newer ruleset version (N) is released, new Azure WAF policies can't be created with the **N-3** version.

- The **N-3 version continues to be supported for 12 months** from the release date of the new **N** rule set, for existing WAF policies only. During these 12 months period, the N-3 version is eligible to receive **only critical security updates**.

- After the 12-month period, the N-3 version will no longer be supported. It won't receive any further updates, fixes, or support from the support team.

This rolling support window helps ensure that users have ample time to plan and migrate to supported versions while maintaining a clear lifecycle for managed rule sets.

## Upgrade recommendations

Users are encouraged to:

- Use the **latest rule set version (N)** where possible to benefit from the most current protections and rule coverage.

- Plan upgrades early, taking advantage of the **12-month final support period** for older rule sets.

- Review [Upgrade CRS or DRS ruleset version](/azure/web-application-firewall/ag/upgrade-ruleset-version) for breaking changes, added rules, and tuning guidance when moving between major rule set versions.

> [!WARNING]

> Failure to upgrade beyond the final support period might expose applications to unpatched vulnerabilities and reduced managed rule coverage.

## Ruleset support schedule

The following tables summarize the current support status and planned end of support dates for managed rulesets of Azure WAF on Application Gateway:

The following tables summarize the current support status and planned end of support dates for managed rulesets of Azure WAF on Front Door:

### Default rulesets

| Ruleset version | Release date | Support status | New policy creation end date | End of support for existing policies |

|---|---|---|---|

| **DRS 2.2** | February 2026 | Supported | Not defined yet | Not defined yet |

| **DRS 2.1** | October 2023 | Supported | Not defined yet | Not defined yet |

| **CRS 3.2** | August 2021 | Supported | Not defined yet | Not defined yet. Support ends one year after the release of the **first** DRS version newer than DRS 2.2 |

| **CRS 3.1** <br> **CRS 3.0** | N/A | Supported | June 1, 2026 | February 26, 2027 |

| **CRS 2.2.9** | N/A | Not supported | March 15, 2025 | March 15, 2025 |

| Ruleset version | Release date | Support status | New policy creation end date | End of support for existing policies |

|---|---|---|---|

| **DRS 2.2** | February 2026 | Supported | Not defined yet | Not defined yet |

| **DRS 2.1** | October 2023 | Supported | Not defined yet | Not defined yet |

| **DRS 2.0** | August 2021 | Supported | Not defined yet | Not defined yet. Support ends one year after the release of the **first** DRS version newer than DRS 2.2 |

| **DRS 1.2** <br> **DRS 1.1** <br> **DRS 1.0** | N/A | Supported | June 1, 2026 | February 26, 2027 |

### Bot management ruleset

| **Ruleset version** | **Release date** | **Support status** | **Support end date** |

|----|----|----|----|

| **Bot Management 1.1** | October 2024 | Supported | Not defined yet |

| **Bot Management 1.0** | July 2021 | Supported | Not defined yet |

| **Bot Management 0.1** | N/A | Not supported | Preview version - not supported |

### HTTP DDoS ruleset

| **Ruleset version** | **Release date** | **Support status** | **Support end date** |

|----|----|----|----|

| **HTTP DDoS Ruleset 1.0** | November 2025 | Supported | Not defined yet |

| **Ruleset version** | **Release date** | **Support status** | **Support end date** |

|----|----|----|----|

| **Bot Management 1.1** | October 2024 | Supported | Not defined yet |

| **Bot Management 1.0** | July 2021 | Supported | Not defined yet |

## Related content

- [DRS and CRS rule groups and rules](/azure/web-application-firewall/ag/application-gateway-crs-rulegroups-rules)

- [Upgrade CRS or DRS ruleset version](/azure/web-application-firewall/ag/upgrade-ruleset-version)

- [Customize WAF rules](/azure/web-application-firewall/ag/application-gateway-customize-waf-rules-portal)

- [DRS rule groups and rules](/azure/web-application-firewall/afds/waf-front-door-drs)

- [WAF exclusion lists](/azure/web-application-firewall/afds/waf-front-door-exclusion)


# Application Gateway Waf Configuration

# Web Application Firewall exclusion lists

**Applies to:** :heavy_check_mark: Application Gateway V2

The Azure Application Gateway Web Application Firewall (WAF) provides protection for web applications. This article describes the configuration for WAF exclusion lists. These settings are located in the WAF policy associated to your Application Gateway. To learn more about WAF policies, see [Azure Web Application Firewall on Azure Application Gateway](ag-overview.md) and [Create Web Application Firewall policies for Application Gateway](create-waf-policy-ag.md).

Sometimes WAF might block a request that you want to allow for your application. WAF exclusion lists allow you to omit certain request attributes from a WAF evaluation. The rest of the request is evaluated as normal.

For example, Active Directory inserts tokens that are used for authentication. When used in a request header, these tokens can contain special characters that might trigger a false positive detection from the WAF rules. By adding the header to an exclusion list, you can configure WAF to ignore the header, but WAF still evaluates the rest of the request.

You can configure exclusions to apply when specific WAF rules are evaluated, or to apply globally to the evaluation of all WAF rules. Exclusion rules apply to your whole web application.

## Identify request attributes to exclude

When you configure a WAF exclusion, you must specify the attributes of the request that should be excluded from the WAF evaluation. You can configure a WAF exclusion for the following request attributes:

* Request headers

* Request cookies

* Request attribute name (args) can be added as an exclusion element, such as:

* Form field name

* JSON entity

* URL query string args

You can specify an exact request header, body, cookie, or query string attribute match. Or, you can specify partial matches. Use the following operators to configure the exclusion:

- **Equals**:  This operator is used for an exact match. As an example, for selecting a header named **bearerToken**, use the equals operator with the selector set as **bearerToken**.

- **Starts with**: This operator matches all fields that start with the specified selector value.

- **Ends with**:  This operator matches all request fields that end with the specified selector value.

- **Contains**: This operator matches all request fields that contain the specified selector value.

- **Equals any**: This operator matches all request fields. * is the selector value. For example, you would use this operator when you don't know the exact values for a given match variable but want to make sure that the request traffic still gets excluded from rules evaluation.

When processing exclusions the WAF engine performs a case sensitive/insensitive match based on the following table. Additionally, regular expressions aren't allowed as selectors and XML request bodies aren't supported.

| Request Body Part | CRS 3.1 and Earlier | CRS 3.2 and Later |

|-|-|-|

| Header* | Case Insensitive | Case Insensitive |

| Cookie* | Case Insensitive | Case Sensitive |

| Query String* | Case Insensitive | Case Sensitive |

| URL-Encoded Body | Case Insensitive | Case Sensitive |

| JSON Body | Case Insensitive | Case Sensitive |

| XML Body | Not Supported | Not Supported |

| Multipart Body | Case Insensitive | Case Sensitive |

*Depending on your application, the names, and values, of your headers, cookies and query args can be case sensitive or insensitive.

> [!NOTE]

> For more information and troubleshooting help, see [WAF troubleshooting](web-application-firewall-troubleshoot.md).

### Request attributes by keys and values

When you configure an exclusion, you need to determine whether you want to exclude the key or the value from WAF evaluation.

For example, suppose your requests include this header:

```

My-Header: 1=1

```

The value of the header (`1=1`) might be detected as an attack by the WAF. But if you know this is a legitimate value for your scenario, you can configure an exclusion for the *value* of the header. To do so, you use the **RequestHeaderValues** match variable, the operator **contains**, and the selector (`My-Header`). This configuration stops evaluation of all values for the header `My-Header`.

> [!NOTE]

> Request attributes by key and values are only available in CRS 3.2 or newer and Bot Manager 1.0 or newer.

>

> Request attributes by names work the same way as request attributes by values, and are included for backward compatibility with CRS 3.1 and earlier versions. We recommend you use request attributes by values instead of attributes by names. For example, use **RequestHeaderValues** instead of **RequestHeaderNames**.

In contrast, if your WAF detects the header's name (`My-Header`) as an attack, you could configure an exclusion for the header *key* by using the **RequestHeaderKeys** request attribute. The **RequestHeaderKeys** attribute is only available in CRS 3.2 or newer and Bot Manager 1.0 or newer.

#### Request attribute examples

The following table shows some examples of how you might structure your exclusion for a given match variable.

| Attribute to Exclude | matchVariable | selectorMatchOperator | Example selector | Example request | What gets excluded |

|-|-|-|-|-|-|

| Query string | RequestArgKeys | Equals | `/etc/passwd` | Uri: `http://localhost:8080/?/etc/passwd=test` | `/etc/passwd` |

| Query string | RequestArgKeys | EqualsAny | N/A | Uri: `http://localhost:8080/?/etc/passwd=test&.htaccess=test2` | `/etc/passwd` and `.htaccess` |

| Query string | RequestArgNames | Equals | `text` | Uri: `http://localhost:8080/?text=/etc/passwd` | `/etc/passwd` |

| Query string | RequestArgNames | EqualsAny | N/A | Uri: `http://localhost:8080/?text=/etc/passwd&text2=.cshrc` | `/etc/passwd` and `.cshrc` |

| Query string | RequestArgValues | Equals | `text` | Uri: `http://localhost:8080/?text=/etc/passwd` | `/etc/passwd` |

| Query string | RequestArgValues | EqualsAny | N/A | Uri: `http://localhost:8080/?text=/etc/passwd&text2=.cshrc` | `/etc/passwd` and `.cshrc` |

| Request body | RequestArgKeys | Contains | `sleep` | Request body: `{"sleep(5)": "test"}` | `sleep(5)` |

| Request body | RequestArgKeys | EqualsAny | N/A | Request body: `{".zshrc": "value", "sleep(5)":"value2"}` | `.zshrc` and `sleep(5)` |

| Request body | RequestArgNames | Equals | `test` | Request body: `{"test": ".zshrc"}` | `.zshrc` |

| Request body | RequestArgNames | EqualsAny | N/A | Request body: `{"key1": ".zshrc", "key2":"sleep(5)"}` | `.zshrc` and `sleep(5)` |

| Request body | RequestArgValues | Equals | `test` | Request body: `{"test": ".zshrc"}` | `.zshrc` |

| Request body | RequestArgValues | EqualsAny | N/A | Request body: `{"key1": ".zshrc", "key2":"sleep(5)"}` | `.zshrc` and `sleep(5)` |

| Header | RequestHeaderKeys | Equals | `X-Scanner` | Header: `{"X-Scanner": "test"}` | `X-scanner` |

| Header | RequestHeaderKeys | EqualsAny | N/A | Header: `{"X-Scanner": "test", "x-ratproxy-loop": "value"}` | `X-Scanner` and `x-ratproxy-loop` |

| Header | RequestHeaderNames | Equals | `head1` | Header: `{"head1": "X-Scanner"}` | `X-scanner` |

| Header | RequestHeaderNames | EqualsAny | N/A | Header: `{"head1": "myvar=1234", "User-Agent": "(hydra)"}` | `myvar=1234` and `(hydra)` |

| Header | RequestHeaderValues | Equals | `head1` | Header: `{"head1": "X-Scanner"}` | `X-scanner` |

| Header | RequestHeaderValues | EqualsAny | N/A | Header: `{"head1": "myvar=1234", "User-Agent": "(hydra)"}` | `myvar=1234` and `(hydra)` |

| Cookie | RequestCookieKeys | Contains | `/etc/passwd` | Header: `{"Cookie": "/etc/passwdtest=hello1"}` | `/etc/passwdtest` |

| Cookie | RequestCookieKeys | EqualsAny | N/A | Header: `{"Cookie": "/etc/passwdtest=hello1", "Cookie": ".htaccess=test1"}` | `/etc/passwdtest` and `.htaccess` |

| Cookie | RequestCookieNames | Equals | `arg1` | Header: `{"Cookie": "arg1=/etc/passwd"}` | `/etc/passwd` |

| Cookie | RequestCookieNames | EqualsAny | N/A | Header: `{"Cookie": "arg1=/etc/passwd", "Cookie": "arg1=.cshrc"}` | `/etc/passwd` and `.cshrc` |

| Cookie | RequestCookieValues | Equals | `arg1` | Header: `{"Cookie": "arg1=/etc/passwd"}` | `/etc/passwd` |

| Cookie | RequestCookieValues | EqualsAny | N/A | Header: `{"Cookie": "arg1=/etc/passwd", "Cookie": "arg1=.cshrc"}` | `/etc/passwd` and `.cshrc` |

> [!NOTE]

> If you create an exclusion using the selectorMatchOperator `EqualsAny`, anything you put in the selector field gets converted to "*" by the backend when the exclusion is created.

## Exclusion scopes

Exclusions can be configured to apply to a specific set of WAF rules, to rulesets, or globally across all rules.

> [!TIP]

> It's a good practice to make exclusions as narrow and specific as possible, to avoid accidentally leaving room for attackers to exploit your system. When you need to add an exclusion rule, use per-rule exclusions wherever possible.

### Per-rule exclusions

You can configure an exclusion for a specific rule, group of rules, or rule set. You must specify the rule or rules that the exclusion applies to. You also need to specify the request attribute that should be excluded from the WAF evaluation. To exclude a complete group of rules, only provide the `ruleGroupName` parameter, the `rules` parameter is only useful when you want to limit the exclusion to specific rules of a group.

Per-rule exclusions are available when you use the OWASP (CRS) ruleset version 3.2 or later or Bot Manager ruleset version 1.0 or later.

#### Example

Suppose you want the WAF to ignore the value of the `User-Agent` request header. The `User-Agent` header contains a characteristic string that allows the network protocol peers to identify the application type, operating system, software vendor, or software version of the requesting software user agent. For more information, see [User-Agent](https://developer.mozilla.org/docs/Web/HTTP/Headers/User-Agent).

There can be any number of reasons to disable evaluating this header. There could be a string that the WAF detects and assumes it’s malicious. For example, the `User-Agent` header might include the classic SQL injection attack `x=x` in a string. In some cases, this can be legitimate traffic. So you might need to exclude this header from WAF evaluation.

You can use the following approaches to exclude the `User-Agent` header from evaluation by all of the SQL injection rules:

# [Azure portal](#tab/portal)

To configure a per-rule exclusion by using the Azure portal, follow these steps:

1. Navigate to the WAF policy, and select **Managed rules**.

1. Select **Add exclusions**.

1. In **Applies to**, select the CRS ruleset to apply the exclusion to, such as **OWASP_3.2**.

1. Select **Add rules**, and select the rules you want to apply exclusions to.

1. Configure the match variable, operator, and selector. Then select **Save**.

You can configure multiple exclusions.

# [Azure PowerShell](#tab/powershell)

```azurepowershell

$ruleGroupEntry = New-AzApplicationGatewayFirewallPolicyExclusionManagedRuleGroup `

-RuleGroupName 'REQUEST-942-APPLICATION-ATTACK-SQLI'

$exclusionManagedRuleSet = New-AzApplicationGatewayFirewallPolicyExclusionManagedRuleSet `

-RuleSetType 'OWASP' `

-RuleSetVersion '3.2' `

-RuleGroup $ruleGroupEntry

$exclusionEntry = New-AzApplicationGatewayFirewallPolicyExclusion `

-MatchVariable "RequestHeaderValues" `

-SelectorMatchOperator 'Equals' `

-Selector 'User-Agent' `

-ExclusionManagedRuleSet $exclusionManagedRuleSet

$wafPolicy = Get-AzApplicationGatewayFirewallPolicy `

-Name $wafPolicyName `

-ResourceGroupName $resourceGroupName

$wafPolicy.ManagedRules[0].Exclusions.Add($exclusionEntry)

$wafPolicy | Set-AzApplicationGatewayFirewallPolicy

```

# [Azure CLI](#tab/cli)

```azurecli

az network application-gateway waf-policy managed-rule exclusion rule-set add \

--resource-group $resourceGroupName \

--policy-name $wafPolicyName \

--type OWASP \

--version 3.2 \

--group-name 'REQUEST-942-APPLICATION-ATTACK-SQLI' \

--match-variable 'RequestHeaderValues' \

--match-operator 'Equals' \

--selector 'User-Agent'

```

# [Bicep](#tab/bicep)

```bicep

resource wafPolicy 'Microsoft.Network/ApplicationGatewayWebApplicationFirewallPolicies@2021-08-01' = {

name: wafPolicyName

location: location

properties: {

managedRules: {

managedRuleSets: [

{

ruleSetType: 'OWASP'

ruleSetVersion: '3.2'

}

]

exclusions: [

{

matchVariable: 'RequestHeaderValues'

selectorMatchOperator: 'Equals'

selector: 'User-Agent'

exclusionManagedRuleSets: [

{

ruleSetType: 'OWASP'

ruleSetVersion: '3.2'

ruleGroups: [

{

ruleGroupName: 'REQUEST-942-APPLICATION-ATTACK-SQLI'

rules: [

{

ruleId: '942150'

}

{

ruleId: '942410'

}

]

}

]

}

]

}

]

}

}

}

```

# [ARM template](#tab/armtemplate)

```json

{

"type": "Microsoft.Network/ApplicationGatewayWebApplicationFirewallPolicies",

"apiVersion": "2021-08-01",

"name": "[parameters('wafPolicyName')]",

"location": "[parameters('location')]",

"properties": {

"managedRules": {

"managedRuleSets": [

{

"ruleSetType": "OWASP",

"ruleSetVersion": "3.2"

}

],

"exclusions": [

{

"matchVariable": "RequestHeaderValues",

"selectorMatchOperator": "Equals",

"selector": "User-Agent",

"exclusionManagedRuleSets": [

{

"ruleSetType": "OWASP",

"ruleSetVersion": "3.2",

"ruleGroups": [

{

"ruleGroupName": "REQUEST-942-APPLICATION-ATTACK-SQLI",

"rules": [

{

"ruleId": "942150"

},

{

"ruleId": "942410"

}

]

}

]

}

]

}

]

}

}

}

```

---

You can also exclude the `User-Agent` header from evaluation just by rule 942270:

# [Azure portal](#tab/portal)

Follow the steps described in the preceding example, and select rule 942270 in step 4.

# [Azure PowerShell](#tab/powershell)

```azurepowershell

$ruleEntry = New-AzApplicationGatewayFirewallPolicyExclusionManagedRule `

-Rule '942270'

$ruleGroupEntry = New-AzApplicationGatewayFirewallPolicyExclusionManagedRuleGroup `

-RuleGroupName 'REQUEST-942-APPLICATION-ATTACK-SQLI' `

-Rule $ruleEntry

$exclusionManagedRuleSet = New-AzApplicationGatewayFirewallPolicyExclusionManagedRuleSet `

-RuleSetType 'OWASP' `

-RuleSetVersion '3.2' `

-RuleGroup $ruleGroupEntry

$exclusionEntry = New-AzApplicationGatewayFirewallPolicyExclusion `

-MatchVariable "RequestHeaderValues" `

-SelectorMatchOperator 'Equals' `

-Selector 'User-Agent' `

-ExclusionManagedRuleSet $exclusionManagedRuleSet

$wafPolicy = Get-AzApplicationGatewayFirewallPolicy `

-Name $wafPolicyName `

-ResourceGroupName $resourceGroupName

$wafPolicy.ManagedRules[0].Exclusions.Add($exclusionEntry)

$wafPolicy | Set-AzApplicationGatewayFirewallPolicy

```

# [Azure CLI](#tab/cli)

```azurecli

az network application-gateway waf-policy managed-rule exclusion rule-set add \

--resource-group $resourceGroupName \

--policy-name $wafPolicyName \

--type OWASP \

--version 3.2 \

--group-name 'REQUEST-942-APPLICATION-ATTACK-SQLI' \

--rule-ids 942270 \

--match-variable 'RequestHeaderValues' \

--match-operator 'Equals' \

--selector 'User-Agent'

```

# [Bicep](#tab/bicep)

```bicep

resource wafPolicy 'Microsoft.Network/ApplicationGatewayWebApplicationFirewallPolicies@2021-08-01' = {

name: wafPolicyName

location: location

properties: {

managedRules: {

managedRuleSets: [

{

ruleSetType: 'OWASP'

ruleSetVersion: '3.2'

}

]

exclusions: [

{

matchVariable: 'RequestHeaderValues'

selectorMatchOperator: 'Equals'

selector: 'User-Agent'

exclusionManagedRuleSets: [

{

ruleSetType: 'OWASP'

ruleSetVersion: '3.2'

ruleGroups: [

{

ruleGroupName: 'REQUEST-942-APPLICATION-ATTACK-SQLI'

rules: [

{

ruleId: '942270'

}

]

}

]

}

]

}

]

}

}

}

```

# [ARM template](#tab/armtemplate)

```json

{

"type": "Microsoft.Network/ApplicationGatewayWebApplicationFirewallPolicies",

"apiVersion": "2021-08-01",

"name": "[parameters('wafPolicyName')]",

"location": "[parameters('location')]",

"properties": {

"managedRules": {

"managedRuleSets": [

{

"ruleSetType": "OWASP",

"ruleSetVersion": "3.2"

}

],

"exclusions": [

{

"matchVariable": "RequestHeaderValues",

"selectorMatchOperator": "Equals",

"selector": "User-Agent",

"exclusionManagedRuleSets": [

{

"ruleSetType": "OWASP",

"ruleSetVersion": "3.2",

"ruleGroups": [

{

"ruleGroupName": "REQUEST-942-APPLICATION-ATTACK-SQLI",

"rules": [

{

"ruleId": "942270"

}

]

}

]

}

]

}

]

}

}

}

```

---

### Global exclusions

You can configure an exclusion to apply across all WAF rules.

#### Example

Suppose you want to exclude the value in the *user* parameter that is passed in the request via the URL. For example, say it’s common in your environment for the `user` query string argument to contain a string that the WAF views as malicious content, so it blocks it. You can exclude all query string arguments where the name begins with the word `user`, so that the WAF doesn't evaluate the field's value.

The following example shows how you can exclude the `user` query string argument from evaluation:

# [Azure portal](#tab/portal)

To configure a global exclusion by using the Azure portal, follow these steps:

1. Navigate to the WAF policy, and select **Managed rules**.

1. Select **Add exclusions**.

1. In **Applies to**, select **Global**

1. Configure the match variable, operator, and selector. Then select **Save**.

You can configure multiple exclusions.

# [Azure PowerShell](#tab/powershell)

```azurepowershell

$exclusion = New-AzApplicationGatewayFirewallExclusionConfig `

-MatchVariable 'RequestArgNames' `

-SelectorMatchOperator 'StartsWith' `

-Selector 'user'

```

# [Azure CLI](#tab/cli)

```azurecli

az network application-gateway waf-policy managed-rule exclusion add \

--resource-group $resourceGroupName \

--policy-name $wafPolicyName \

--match-variable 'RequestArgNames' \

--selector-match-operator 'StartsWith' \

--selector 'user'

```

# [Bicep](#tab/bicep)

```bicep

resource wafPolicy 'Microsoft.Network/ApplicationGatewayWebApplicationFirewallPolicies@2021-08-01' = {

name: wafPolicyName

location: location

properties: {

managedRules: {

managedRuleSets: [

{

ruleSetType: 'OWASP'

ruleSetVersion: '3.2'

}

]

exclusions: [

{

matchVariable: 'RequestArgNames'

selectorMatchOperator: 'StartsWith'

selector: 'user'

}

]

}

}

}

```

# [ARM template](#tab/armtemplate)

```json

{

"type": "Microsoft.Network/ApplicationGatewayWebApplicationFirewallPolicies",

"apiVersion": "2021-08-01",

"name": "[parameters('wafPolicyName')]",

"location": "[parameters('location')]",

"properties": {

"managedRules": {

"managedRuleSets": [

{

"ruleSetType": "OWASP",

"ruleSetVersion": "3.2"

}

],

"exclusions": [

{

"matchVariable": "RequestArgNames",

"selectorMatchOperator": "StartsWith",

"selector": "user"

}

]

}

}

}

```

---

So if the URL `http://www.contoso.com/?user%3c%3e=joe` is scanned by the WAF, it doesn't evaluate the string **joe**, but it still evaluates the parameter name **user%3c%3e**.

## Related content

- [WAF DRS and CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md)

- [Application Gateway diagnostics](../../application-gateway/application-gateway-diagnostics.md#diagnostic-logging).

- [Upgrade CRS or DRS ruleset version](upgrade-ruleset-version.md)


# Application Gateway Exceptions

# Azure Application Gateway WAF exceptions list (preview)

**Applies to:** :heavy_check_mark: Application Gateway V2

The Azure Application Gateway Web Application Firewall (WAF) helps protect your web applications from common threats and attacks. This article describes how to configure WAF exception lists in a WAF policy associated with your Application Gateway.

For an overview of WAF policies, see [Azure Web Application Firewall on Azure Application Gateway](/azure/web-application-firewall/ag/ag-overview) and [Create Web Application Firewall policies for Application Gateway](/azure/web-application-firewall/ag/create-waf-policy-ag).

In some cases, WAF might block requests that are safe and expected for your application. Exception lists allow you to bypass WAF inspection for specific requests. You can configure exceptions at the rule, rule group, or managed ruleset level.

Only the next generation of WAF engine supports exceptions, and you can use them only if your managed ruleset version is CRS 3.2, DRS 2.1, or later. For more information, see [Upgrade CRS or DRS ruleset version](/azure/web-application-firewall/ag/upgrade-ruleset-version).

> [!IMPORTANT]

> Exceptions in Azure Application Gateway Web Application Firewall (WAF) is currently in PREVIEW.

> See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Define request attributes

When you create an exception, specify which request attributes identify the traffic that should bypass WAF evaluation. Supported attributes include:

- Request URI

- Remote IP address

- Request header name and value

Match attributes either exactly or partially by using the following operators:

- **Equals:** Matches the exact value.

**Example:** To select the header bearerToken, use the *Equals* operator with bearerToken as the selector.

- **Starts with:** Matches values beginning with the specified selector.

- **Ends with:** Matches values ending with the specified selector.

- **Contains:** Matches values containing the specified selector.

- **IP Match:** Matches one or more IP addresses.

## Set the exception scope

Scope exceptions to:

- A specific rule

- A rule group

- An entire managed ruleset

When you define an exception:

- Specify the rules, rule group, or managed ruleset it applies to.

- Define the request attribute that identifies the traffic to exclude.

- To exclude an entire rule group, provide the `ruleGroupName` parameter. Use the `rules` parameter only when narrowing the exception to specific rules within that group.

> [!TIP]

> Always make exceptions as narrow as possible. Broad exceptions might unintentionally expose your application to attacks. Whenever possible, use per-rule exceptions.

## Apply an exception to your WAF policy

Suppose you don't want WAF to inspect requests to `/login.php` and `/logout.php` when it evaluates SQL injection rules. Configure exceptions as follows:

# [**Portal**](#tab/portal)

1. Go to the WAF policy where you want to add exceptions.

1. Under **Settings**, select **Managed rules**.

1. In the **Exceptions** tab, select **Add exceptions**.

1. In **Applies to**, select the DRS ruleset to apply the exception to, such as *Microsoft_DefaultRuleSet_2.1*, and select the scope (rule group, specific rules, or the entire ruleset).

1. Select **Add exception** and configure the match variable, value match operator, and the values.

1. Select **Add** and then **Save** to apply the new exception.

The new exception appears in the **Exceptions** tab.

# [**PowerShell**](#tab/powershell)

Use [New-AzApplicationGatewayFirewallPolicyException](/powershell/module/az.network/new-azapplicationgatewayfirewallpolicyexception) to create an exception on your WAF policy.

```azurepowershell-interactive

$ruleGroupEntry = New-AzApplicationGatewayFirewallPolicyExclusionManagedRuleGroup `

-RuleGroupName 'REQUEST-942-APPLICATION-ATTACK-SQLI'

$exclusionManagedRuleSet = New-AzApplicationGatewayFirewallPolicyExclusionManagedRuleSet `

-RuleSetType 'Microsoft_DefaultRuleSet' `

-RuleSetVersion '2.1' `

-RuleGroup $ruleGroupEntry

$exceptionEntry = New-AzApplicationGatewayFirewallPolicyException `

-MatchVariable "RequestURI" `

-ValueMatchOperator 'Equals' `

-Values login.php, logout.php `

-ExceptionManagedRuleSet $exceptionManagedRuleSet

$wafPolicy = Get-AzApplicationGatewayFirewallPolicy `

-Name $wafPolicyName `

-ResourceGroupName $resourceGroupName

$wafPolicy.ManagedRules[0].Exceptions.Add($exceptionEntry)

$wafPolicy | Set-AzApplicationGatewayFirewallPolicy

```

# [**Azure CLI**](#tab/cli)

Use [az network application-gateway waf-policy managed-rule exception add](/cli/azure/network/application-gateway/waf-policy/managed-rule/exception#az-network-application-gateway-waf-policy-managed-rule-exception-add) to create an exception on your WAF policy.

```azurecli-interactive

az network application-gateway waf-policy managed-rule exception add \

-g "myResourceGroup" \

--policy-name "myWAF" \

--match-variable "RequestURI" \

--value-operator Equals \

--values "login.php" "default.aspx" "account/images" \

--rule-sets [0].rule-set-type=Microsoft_Default_Ruleset [0].rule-set-version=2.1

```

---

## Limitations

The following limitations apply to WAF exceptions:

- Each Azure WAF policy supports up to **60 exceptions**.

- Each Application Gateway supports up to **60 exceptions in total**, calculated as the sum of all exceptions across the WAF policies associated with that gateway.

- Within a **single exception**, you can configure up to:

- **600 IP addresses**, or

- **10 URIs**, or

- **10 request headers**.

## Options to allow traffic through Azure WAF

Azure Web Application Firewall (WAF) provides several mechanisms to safely allow traffic when needed while maintaining protection. Depending on whether you want to bypass inspection for part of a request, or the entire request, use **Exclusions**, **Exceptions**, or **Custom rules**.

### Allow specific parts of a request using exclusions

Use **Exclusions** when you want WAF to skip inspection of a specific element within a request, such as a header, query parameter, or cookie, while still applying inspection to the rest of the request.

**Example:** If a legitimate application sends a session cookie with random characters that frequently trigger SQL Injection false positives, you can configure an exclusion for that cookie. WAF skips inspection for the cookie value but still enforces protections on the rest of the request.

### Allow entire requests by using custom rules and exceptions

To allow an entire request to bypass WAF inspection, use one of the following options:

#### Custom rule with an *Allow* action

When you configure a custom rule with the *Allow* action, the request bypasses inspection by the Default Rule Set (DRS), the Core Rule Set (CRS), and the Bot Protection ruleset.

> [!IMPORTANT]

> This bypass is absolute for these rulesets and can't be changed or selectively applied. Once the *Allow* action is triggered, none of these rulesets evaluate the request. However, the **HTTP DDoS protection ruleset** still processes the request. This ruleset ensures requests are checked for volumetric or flood-style attacks even if all other rulesets are skipped.

Use this configuration only when you fully trust the traffic source or application, since it effectively disables signature and anomaly detection.

**Example:** If you have a trusted partner API that frequently triggers DRS rules due to its payload format, you can create a custom *Allow* rule for traffic coming from the partner’s IP range. This configuration ensures the traffic is never blocked by DRS, CRS, or Bot Protection, while still benefiting from HTTP DDoS safeguards.

#### Exceptions (more granular control)

In contrast, exceptions let you bypass inspection only for specific rules, rule groups, or entire rulesets rather than disabling all of them at once.

You can apply exceptions to DRS, CRS, Bot Protection, and even the HTTP DDoS ruleset.

This approach provides fine-grained control, so you can disable inspection for one problematic rule while keeping the rest of the protections active.

**Example:** If a single DRS rule (for example *Restrict Content-Type Header*) blocks valid mobile app requests, you can create an exception for that rule only. All other DRS rules, Bot Protection, and DDoS protections continue to run on the traffic.

## Related content

- [Azure Web Application Firewall on Azure Application Gateway](ag-overview.md)

- [Web Application Firewall DRS and CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md)

- [Upgrade CRS or DRS ruleset version](upgrade-ruleset-version.md)


# Upgrade Ruleset Version

# Upgrade CRS or DRS ruleset version

**Applies to:** :heavy_check_mark: Application Gateway V2

The Azure-managed **Default Rule Set (DRS)** in Azure Application Gateway Web Application Firewall (WAF) protects web applications against common vulnerabilities and exploits, including the OWASP top 10 attack types. The default rule set also incorporates the Microsoft Threat Intelligence Collection rules. Always run the **latest ruleset version**, which includes the most recent security updates, rule enhancements, and fixes.

The Azure-managed Default Rule Set (DRS) is the latest generation of rulesets in Azure WAF, replacing all previous Core Rule Set (CRS) versions. Among DRS releases, always use the highest available version (**DRS 2.2**) to ensure you have the most up-to-date protections.

This article provides PowerShell examples for upgrading your Azure WAF policy to **DRS 2.2** from CRS 3.0, CRS 3.1, CRS 3.2, or DRS 2.1.

> [!NOTE]

> PowerShell snippets are examples only. Replace all placeholders with values from your environment.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An existing Azure WAF policy with a Core Rule Set (CRS) or Default Rule Set (DRS) applied. If you don't have a WAF policy yet, see [Create Web Application Firewall policies for Application Gateway](create-waf-policy-ag.md).

- Latest version of [Azure PowerShell installed locally](/powershell/azure/install-azure-powershell). This article requires the [Az.Network Module](/powershell/module/az.network).

## Key considerations when upgrading

When upgrading your Azure WAF ruleset version, make sure to:

- **Preserve existing customizations**: carry over your rule action overrides, rule status (enabled or disabled) overrides, and exclusions.

- **Drop customizations for removed rules**: don't carry over overrides or exclusions for rules that no longer exist in DRS 2.2. Carrying over an override for a rule that DRS 2.2 doesn't contain causes the policy update to fail with an error such as `The override Rule '<id>' is unknown for RuleGroup '<group>'`.

- **Account for the Paranoia Level baseline**: DRS 2.2 operates at Paranoia Level 1 (PL1) by default, and all PL2 rules are disabled by default. In CRS 3.2 and DRS 2.1, PL2 rules were active. Any PL2 rules you previously customized are disabled by default in DRS 2.2 until you explicitly re-enable them.

- **Validate new rules safely**: newly added rules that are enabled by default (PL1) are initially set to **log mode**, so you can monitor their impact and fine-tune them before enabling blocking.

## Prepare your environment and variables

1. Set the context for your selected subscription, resource group, and Azure WAF policy.

```powershell

Import-Module Az.Network

Set-AzContext -SubscriptionId "<subscription_id>"

$resourceGroupName = "<resource_group>"

$wafPolicyName = "<policy_name>"

```

1. Get the WAF policy object and retrieve its definitions. The current managed ruleset can be a CRS (`OWASP`) or a DRS (`Microsoft_DefaultRuleSet`) type.

```powershell

$wafPolicy = Get-AzApplicationGatewayFirewallPolicy `

-Name $wafPolicyName `

-ResourceGroupName $resourceGroupName

$currentExclusions = $wafPolicy.ManagedRules.Exclusions

$currentManagedRuleset = $wafPolicy.ManagedRules.ManagedRuleSets |

Where-Object { $_.RuleSetType -eq "OWASP" -or $_.RuleSetType -eq "Microsoft_DefaultRuleSet" }

$currentVersion = $currentManagedRuleset.RuleSetVersion

```

## Preserve existing customizations

1. Carry over an override or exclusion only if the rule still exists in **DRS 2.2**. The following function validates a rule ID against the complete set of DRS 2.2 rules and returns `$true` for any rule that was removed (including legacy and inactive rules such as `920460`, `942130`, and `920250`). Using an allowlist of valid rule IDs avoids per-rule maintenance and prevents the policy update from failing on an unknown rule.

```powershell

function Test-RuleIsRemovedFromDRS22 {

param (

[string]$RuleId,

[string]$CurrentRulesetVersion  # Retained for compatibility; not used

)

# Complete set of rule IDs that exist in DRS 2.2.

# Any override or exclusion for a rule NOT in this set is dropped during migration.

$drs22RuleIds = @(

"200002","200003",

"911100",

"920100","920120","920121","920160","920170","920171","920180","920181","920190","920200","920201","920210","920220","920230","920240","920260","920270","920271","920280","920290","920300","920310","920311","920320","920330","920340","920341","920350","920420","920430","920440","920450","920470","920480","920500","920530","920620",

"921110","921120","921130","921140","921150","921151","921160","921190","921200","921422",

"930100","930110","930120","930130",

"931100","931110","931120","931130",

"932100","932105","932110","932115","932120","932130","932140","932150","932160","932170","932171","932180",

"933100","933110","933120","933130","933140","933150","933151","933160","933170","933180","933200","933210",

"934100",

"941100","941101","941110","941120","941130","941140","941150","941160","941170","941180","941190","941200","941210","941220","941230","941240","941250","941260","941270","941280","941290","941300","941310","941320","941330","941340","941350","941360","941370","941380",

"942100","942110","942120","942140","942150","942160","942170","942180","942190","942200","942210","942220","942230","942240","942250","942260","942270","942280","942290","942300","942310","942320","942330","942340","942350","942360","942361","942370","942380","942390","942400","942410","942430","942440","942450","942470","942480","942500","942510",

"943100","943110","943120",

"944100","944110","944120","944130","944200","944210","944240","944250",

"99005002","99005003","99005004","99005005","99005006",

"99030001","99030002","99030003","99030004","99030005","99030006",

"99031001","99031002","99031003","99031004","99031005","99031006",

"99001001","99001002","99001003","99001004","99001005","99001006","99001007","99001008","99001009","99001010","99001011","99001012","99001013","99001014","99001015","99001016","99001017","99001018",

"99032001","99032002"

)

return -not ($drs22RuleIds -contains $RuleId)

}

```

1. When creating new override objects, use the **DRS 2.2 group names**. The following function maps legacy CRS group names to DRS groups. DRS source group names that aren't in the map (for example, when upgrading from DRS 2.1) are returned unchanged:

```powershell

function Get-DrsRuleGroupName {

param (

[Parameter(Mandatory = $true)]

[string]$SourceGroupName

)

$groupMap = @{

"REQUEST-930-APPLICATION-ATTACK-LFI"             = "LFI"

"REQUEST-931-APPLICATION-ATTACK-RFI"             = "RFI"

"REQUEST-932-APPLICATION-ATTACK-RCE"             = "RCE"

"REQUEST-933-APPLICATION-ATTACK-PHP"             = "PHP"

"REQUEST-941-APPLICATION-ATTACK-XSS"             = "XSS"

"REQUEST-942-APPLICATION-ATTACK-SQLI"            = "SQLI"

"REQUEST-943-APPLICATION-ATTACK-SESSION-FIXATION" = "FIX"

"REQUEST-944-APPLICATION-ATTACK-JAVA"            = "JAVA"

"REQUEST-921-PROTOCOL-ATTACK"                    = "PROTOCOL-ATTACK"

"REQUEST-911-METHOD-ENFORCEMENT"                 = "METHOD-ENFORCEMENT"

"REQUEST-920-PROTOCOL-ENFORCEMENT"               = "PROTOCOL-ENFORCEMENT"

"REQUEST-913-SCANNER-DETECTION"                  = $null  # No direct mapping

"Known-CVEs"                                     = "MS-ThreatIntel-CVEs"

"General"                                        = "General"

}

if ($groupMap.ContainsKey($SourceGroupName)) {

return $groupMap[$SourceGroupName]

} else {

return $SourceGroupName  # No known mapping; pass through (DRS source group names)

}

}

```

1. Use the following PowerShell code to define the rules' overrides, duplicating overrides from the existing ruleset version:

```powershell

$groupOverrides = @()

foreach ($group in $currentManagedRuleset.RuleGroupOverrides) {

$mappedGroupName = Get-DrsRuleGroupName $group.RuleGroupName

if (-not $mappedGroupName) { continue }  # Skip groups with no DRS equivalent

foreach ($existingRule in $group.Rules) {

if (-not (Test-RuleIsRemovedFromDRS22 $existingRule.RuleId $currentVersion)) {

$existingGroup = $groupOverrides | Where-Object { $_.RuleGroupName -eq $mappedGroupName }

if ($existingGroup) {

if (-not ($existingGroup.Rules | Where-Object { $_.RuleId -eq $existingRule.RuleId })) {

$existingGroup.Rules.Add($existingRule)

}

} else {

$newGroup = New-AzApplicationGatewayFirewallPolicyManagedRuleGroupOverride `

-RuleGroupName $mappedGroupName `

-Rule @($existingRule)

$groupOverrides += $newGroup

}

}

}

}

```

1. Use the following PowerShell code to duplicate your existing exclusions and apply them on DRS 2.2:

```powershell

# Create new exclusion objects

$newRuleSetExclusions = @()

if ($currentExclusions -ne $null -and $currentExclusions.Count -gt 0) {

foreach ($exclusion in $currentExclusions) {

$newExclusion = New-AzApplicationGatewayFirewallPolicyExclusion `

-MatchVariable $exclusion.MatchVariable `

-SelectorMatchOperator $exclusion.SelectorMatchOperator `

-Selector $exclusion.Selector

# Migrate scopes: RuleSet, RuleGroup, or individual Rules

if ($exclusion.ExclusionManagedRuleSets) {

foreach ($scope in $exclusion.ExclusionManagedRuleSets) {

# Create RuleGroup objects from existing RuleGroups

$ruleGroups = @()

foreach ($group in $scope.RuleGroups) {

$drsGroupName = Get-DrsRuleGroupName $group.RuleGroupName

if ($drsGroupName) {

$exclusionRules = @()

foreach ($rule in $group.Rules) {

if (-not (Test-RuleIsRemovedFromDRS22 $rule.RuleId $currentVersion)) {

$exclusionRules += New-AzApplicationGatewayFirewallPolicyExclusionManagedRule `

-RuleId $rule.RuleId

}

}

if ($exclusionRules -ne $null -and $exclusionRules.Count -gt 0) {

$ruleGroups += New-AzApplicationGatewayFirewallPolicyExclusionManagedRuleGroup `

-Name $drsGroupName `

-Rule $exclusionRules

} else {

$ruleGroups += New-AzApplicationGatewayFirewallPolicyExclusionManagedRuleGroup `

-Name $drsGroupName

}

}

}

# Create the ManagedRuleSet scope object with the updated RuleGroups

if ($ruleGroups.Count -gt 0) {

$newRuleSetScope = New-AzApplicationGatewayFirewallPolicyExclusionManagedRuleSet `

-Type "Microsoft_DefaultRuleSet" `

-Version "2.2" `

-RuleGroup $ruleGroups

# Add to the new exclusion object

$newExclusion.ExclusionManagedRuleSets += $newRuleSetScope

}

}

}

if (-not $newExclusion.ExclusionManagedRuleSets) {

$newExclusion.ExclusionManagedRuleSets = @()

}

$newRuleSetExclusions += $newExclusion

}

}

```

## Validate new rules safely

When you upgrade, new DRS 2.2 rules that belong to Paranoia Level 1 are enabled by default. If your WAF is in *Prevention* mode, set these new rules to *log* mode first so you can review logs before enabling blocking.

Rules that belong to Paranoia Level 2 are disabled by default in DRS 2.2 and don't block traffic, so they don't require this step. If you want to operate at Paranoia Level 2, enable the relevant PL2 rules explicitly and follow the same validate-in-log approach.

1. Use the definition that matches the version you're upgrading **from**. Each definition lists the rules that are introduced and enabled by default in DRS 2.2 compared to that version.

```powershell

# Added and enabled by default in DRS 2.2 compared to CRS 3.0

$rulesAddedInThisVersionByGroup = @{

"General"              = @("200002", "200003")

"PROTOCOL-ENFORCEMENT" = @("920171", "920181", "920470", "920480", "920500", "920530", "920620")

"PROTOCOL-ATTACK"      = @("921190", "921200")

"RCE"                  = @("932180")

"PHP"                  = @("933200", "933210")

"NODEJS"               = @("934100")

"XSS"                  = @("941360", "941370")

"SQLI"                 = @("942500")

"JAVA"                 = @("944100", "944110", "944120", "944130")

"MS-ThreatIntel-CVEs"  = @("99001018")

"MS-ThreatIntel-XSS"   = @("99032001")

}

```

```powershell

# Added and enabled by default in DRS 2.2 compared to CRS 3.1

$rulesAddedInThisVersionByGroup = @{

"General"              = @("200002", "200003")

"PROTOCOL-ENFORCEMENT" = @("920181", "920500", "920530", "920620")

"PROTOCOL-ATTACK"      = @("921190", "921200")

"PHP"                  = @("933200", "933210")

"NODEJS"               = @("934100")

"XSS"                  = @("941360", "941370")

"SQLI"                 = @("942500")

"MS-ThreatIntel-CVEs"  = @("99001018")

"MS-ThreatIntel-XSS"   = @("99032001")

}

```

```powershell

# Added and enabled by default in DRS 2.2 compared to CRS 3.2

$rulesAddedInThisVersionByGroup = @{

"PROTOCOL-ENFORCEMENT" = @("920181", "920500", "920530", "920620")

"PROTOCOL-ATTACK"      = @("921190", "921200")

"NODEJS"               = @("934100")

"XSS"                  = @("941370")

"MS-ThreatIntel-CVEs"  = @("99001018")

"MS-ThreatIntel-XSS"   = @("99032001")

}

```

```powershell

# Added and enabled by default in DRS 2.2 compared to DRS 2.1

$rulesAddedInThisVersionByGroup = @{

"PROTOCOL-ENFORCEMENT" = @("920530", "920620")

"MS-ThreatIntel-XSS"   = @("99032001")

}

```

1. Use the following PowerShell code to add the new rule overrides to the existing `$groupOverrides` object defined previously:

```powershell

foreach ($groupName in $rulesAddedInThisVersionByGroup.Keys) {

$ruleOverrides = @()

foreach ($ruleId in $rulesAddedInThisVersionByGroup[$groupName]) {

$existingGroup = $groupOverrides | Where-Object { $_.RuleGroupName -eq $groupName }

$alreadyExists = $false

if ($existingGroup) {

$alreadyExists = $existingGroup.Rules | Where-Object { $_.RuleId -eq $ruleId }

}

if (-not $alreadyExists) {

$ruleOverrides += New-AzApplicationGatewayFirewallPolicyManagedRuleOverride `

-RuleId $ruleId `

-Action "Log" `

-State "Enabled"

}

}

# Only create or update the group override if we added rules to it

if ($ruleOverrides.Count -gt 0) {

$existingGroup = $groupOverrides | Where-Object { $_.RuleGroupName -eq $groupName }

if ($existingGroup) {

foreach ($ruleOverride in $ruleOverrides) {

$existingGroup.Rules.Add($ruleOverride)

}

} else {

$groupOverrides += New-AzApplicationGatewayFirewallPolicyManagedRuleGroupOverride `

-RuleGroupName $groupName `

-Rule $ruleOverrides

}

}

}

```

## Apply customizations and upgrade

Define your updated Azure WAF policy object, incorporating the duplicated and updated rule overrides and exclusions:

```powershell

$managedRuleSet = New-AzApplicationGatewayFirewallPolicyManagedRuleSet `

-RuleSetType "Microsoft_DefaultRuleSet" `

-RuleSetVersion "2.2" `

-RuleGroupOverride $groupOverrides

# Replace the existing CRS (OWASP) or DRS (Microsoft_DefaultRuleSet) managed rule set

for ($i = 0; $i -lt $wafPolicy.ManagedRules.ManagedRuleSets.Count; $i++) {

if ($wafPolicy.ManagedRules.ManagedRuleSets[$i].RuleSetType -eq "OWASP" -or

$wafPolicy.ManagedRules.ManagedRuleSets[$i].RuleSetType -eq "Microsoft_DefaultRuleSet") {

$wafPolicy.ManagedRules.ManagedRuleSets[$i] = $managedRuleSet

break

}

}

# Assign the migrated exclusions to the policy

$wafPolicy.ManagedRules.Exclusions = $newRuleSetExclusions

# Apply the updated WAF policy

Set-AzApplicationGatewayFirewallPolicy -InputObject $wafPolicy

```

## Related content

- [Web Application Firewall DRS and CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md)

- [Customize Web Application Firewall rules using the Azure portal](application-gateway-customize-waf-rules-portal.md)


# Application Gateway Customize Waf Rules Powershell

# Customize Web Application Firewall rules using PowerShell

The Azure Application Gateway Web Application Firewall (WAF) provides protection for web applications. These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS). Some rules can cause false positives and block real traffic. For this reason, Application Gateway provides the capability to customize rule groups and rules. For more information on the specific rule groups and rules, see [List of Web Application Firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).

## View rule groups and rules

The following code examples show how to view rules and rule groups that are configurable on a WAF-enabled application gateway.

### View rule groups

The following example shows how to view rule groups:

```powershell

Get-AzApplicationGatewayAvailableWafRuleSets

```

The following output is a truncated response from the preceding example:

```

OWASP (Ver. 3.0):

General:

Description:

Rules:

RuleId     Description

------     -----------

200004     Possible Multipart Unmatched Boundary.

REQUEST-911-METHOD-ENFORCEMENT:

Description:

Rules:

RuleId     Description

------     -----------

911011     Rule 911011

911012     Rule 911012

911100     Method is not allowed by policy

911013     Rule 911013

911014     Rule 911014

911015     Rule 911015

911016     Rule 911016

911017     Rule 911017

911018     Rule 911018

REQUEST-913-SCANNER-DETECTION:

Description:

Rules:

RuleId     Description

------     -----------

913011     Rule 913011

913012     Rule 913012

913100     Found User-Agent associated with security scanner

913110     Found request header associated with security scanner

913120     Found request filename/argument associated with security scanner

913013     Rule 913013

913014     Rule 913014

913101     Found User-Agent associated with scripting/generic HTTP client

913102     Found User-Agent associated with web crawler/bot

913015     Rule 913015

913016     Rule 913016

913017     Rule 913017

913018     Rule 913018

...        ...

```

## Disable rules

The following example disables rules `911011` and `911012` on an application gateway:

```powershell

$disabledrules=New-AzApplicationGatewayFirewallDisabledRuleGroupConfig -RuleGroupName REQUEST-911-METHOD-ENFORCEMENT -Rules 911011,911012

Set-AzApplicationGatewayWebApplicationFirewallConfiguration -ApplicationGateway $gw -Enabled $true -FirewallMode Detection -RuleSetVersion 3.0 -RuleSetType OWASP -DisabledRuleGroups $disabledrules

Set-AzApplicationGateway -ApplicationGateway $gw

```

## Mandatory rules

The following list contains conditions that cause the WAF to block the request while in Prevention Mode (in Detection Mode they are logged as exceptions). These can't be configured or disabled:

* Failure to parse the request body results in the request being blocked, unless body inspection is turned off (XML, JSON, form data)

* Request body (with no files) data length is larger than the configured limit

* Request body (including files) is larger than the limit

* An internal error happened in the WAF engine

CRS 3.x specific:

* Inbound anomaly score exceeded threshold

## Next steps

After you configure your disabled rules, you can learn how to view your WAF logs. For more information, see [Application Gateway Diagnostics](../../application-gateway/application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png

[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png

[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png

[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png


# Application Gateway Customize Waf Rules Cli

# Customize Web Application Firewall rules using the Azure CLI

The Azure Application Gateway Web Application Firewall (WAF) provides protection for web applications. These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS). Some rules can cause false positives and block real traffic. For this reason, Application Gateway provides the capability to customize rule groups and rules. For more information on the specific rule groups and rules, see [List of Web Application Firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).

## View rule groups and rules

The following code examples show how to view rules and rule groups that are configurable.

### View rule groups

The following example shows how to view the rule groups:

```azurecli-interactive

az network application-gateway waf-config list-rule-sets --type OWASP

```

The following output is a truncated response from the preceding example:

```json

[

{

"id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",

"location": null,

"name": "OWASP_3.0",

"provisioningState": "Succeeded",

"resourceGroup": "",

"ruleGroups": [

{

"description": "",

"ruleGroupName": "REQUEST-910-IP-REPUTATION",

"rules": null

},

...

],

"ruleSetType": "OWASP",

"ruleSetVersion": "3.0",

"tags": null,

"type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"

},

{

"id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",

"location": null,

"name": "OWASP_2.2.9",

"provisioningState": "Succeeded",

"resourceGroup": "",

"ruleGroups": [

{

"description": "",

"ruleGroupName": "crs_20_protocol_violations",

"rules": null

},

...

],

"ruleSetType": "OWASP",

"ruleSetVersion": "2.2.9",

"tags": null,

"type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"

}

]

```

### View rules in a rule group

The following example shows how to view rules in a specified rule group:

```azurecli-interactive

az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"

```

The following output is a truncated response from the preceding example:

```json

[

{

"id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",

"location": null,

"name": "OWASP_3.0",

"provisioningState": "Succeeded",

"resourceGroup": "",

"ruleGroups": [

{

"description": "",

"ruleGroupName": "REQUEST-910-IP-REPUTATION",

"rules": [

{

"description": "Rule 910011",

"ruleId": 910011

},

...

]

}

],

"ruleSetType": "OWASP",

"ruleSetVersion": "3.0",

"tags": null,

"type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"

}

]

```

## Disable rules

The following example disables rules `910018` and `910017` on an application gateway:

```azurecli-interactive

az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017

```

## Mandatory rules

The following list contains conditions that cause the WAF to block the request while in Prevention Mode (in Detection Mode they're logged as exceptions). These conditions can't be configured or disabled:

* Failure to parse the request body results in the request being blocked, unless body inspection is turned off (XML, JSON, form data)

* Request body (with no files) data length is larger than the configured limit

* Request body (including files) is larger than the limit

* An internal error happened in the WAF engine

CRS 3.x specific:

* Inbound `anomaly score` exceeded threshold

## Next steps

After you configure your disabled rules, you can learn how to view your WAF logs. For more information, see [Application Gateway diagnostics](../../application-gateway/application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png

[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png

[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png

[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png


# Ddos Ruleset

# HTTP DDoS Ruleset in Azure Application Gateway WAF (preview)

**Applies to:** :heavy_check_mark: Application Gateway V2

> [!IMPORTANT]

> The Microsoft HTTP DDoS Ruleset in the Azure Application Gateway Web Application Firewall (WAF) v2 is currently in PREVIEW.

> See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

HTTP‑layer floods remain the most frequent driver of application availability incidents, and static controls (IP/geo filters, fixed rate limits) often can't keep pace with distributed botnets. The new HTTP DDoS ruleset is Azure Web Application Firewall's (WAF) first automated layer 7 protection model that learns, detects, and defends with minimal user configuration. Once assigned, the ruleset continuously baselines normal traffic for each application gateway and when surges indicate an attack, selectively blocks offending clients with no emergency tuning required.

## How the HTTP DDoS ruleset works

Once the HTTP DDoS ruleset is applied to a policy that's attached to a gateway, traffic baselines are learned for a minimum of 24 hours. The ruleset doesn't detect or block attacks until the 24-hour learning phase is completed.

Request thresholds are learned at the global gateway level. If a single WAF policy configured with the HTTP DDoS ruleset is assigned to multiple gateways, the traffic thresholds are computed separately for each gateway to which the policy is attached.

The HTTP DDoS ruleset learns both a global gateway threshold and individual IP-based thresholds. IP-based thresholds are only enforced when the global gateway threshold for requests is exceeded. Once the gateway threshold is breached, any IP address that exceeds its learned baseline is placed in the penalty box. This design prevents the ruleset from blocking spikes from individual IP addresses when the total request rate to the gateway doesn't cross the threshold.

Each rule in the HTTP DDoS ruleset offers three sensitivity levels, each corresponding to a different threshold. A higher sensitivity setting applies a lower threshold for that rule, while a lower sensitivity setting applies a higher threshold. Medium sensitivity is the default and recommended setting.

The HTTP DDoS ruleset is the first ruleset evaluated by the Azure WAF, even before custom rules.

> [!IMPORTANT]

> Any custom rules configured with *Allow* action won't bypass the HTTP DDoS ruleset, but will bypass all other WAF inspections.

## Ruleset rules

The HTTP DDoS ruleset currently has two rules, and each can be configured with different sensitivity and action settings. Each rule maintains different traffic baselines for traffic that matches the rule criteria.

- **Rule 500100: Anomaly detected on high rate of client requests:** This rule tracks and establishes a baseline for all traffic on the Application Gateway a policy is attached to. When a client exceeds the established threshold, it's placed in the penalty box and blocked for the defined time (15 minutes).

- **Rule 501100: Suspected bots sending high rates of requests:** This rule tracks and establishes a baseline for traffic that's coming from suspected bots based on Microsoft Threat Intelligence. Generally, the thresholds for this traffic are much stricter than the thresholds for traffic in rule 500100. When bot's requests exceed the established threshold, it's placed in the penalty box and blocked for the defined time (15 minutes). Bots classified as high risk are blocked immediately by this rule when the global gateway threshold is breached.

## The penalty box

Once traffic from a client exceeds the threshold for one of the rules in the HTTP DDoS ruleset, they're placed in a penalty box for a period of time (15 minutes), and during that time the client IP is blocked by the WAF. Once the penalty box time is up, the IP will be allowed to access the site unless it exceeds the threshold again, which then will result in going back into the penalty box.

When an IP address exceeds a threshold, a rule hit for the HTTP DDoS ruleset is logged, and the IP is placed in the penalty box. Additional blocks while that IP is in the penalty box aren't logged.

## Monitoring the HTTP DDoS ruleset

- When an IP address breaches a threshold, a log entry is recorded with a *Block* action for the HTTP DDoS ruleset, and the WAF Managed Rule Match metric is incremented by one. Each subsequent blocked request from an IP in the Penalty Box is logged and increments the WAF Managed Rule Match metric.

- Two new metrics have also been introduced for Azure monitor, Penalty box size and Penalty box blocks.  These metrics track the number of IPs currently in the penalty box as well as the number of blocks that occur due to IPs in the penalty box.

## Limitations

During the preview, there is no ability for traffic from specific IP addresses to bypass the DDoS ruleset or penalty box.

## Related content

- [Azure Application Gateway WAF policy](/azure/web-application-firewall/ag/policy-overview)

- [Managed rules for Application Gateway WAF](/azure/web-application-firewall/ag/application-gateway-crs-rulegroups-rules)

- [Custom rules for Application Gateway WAF](/azure/web-application-firewall/ag/custom-waf-rules-overview)


# Bot Protection Overview

# Azure Web Application Firewall on Azure Application Gateway bot protection overview

**Applies to:** :heavy_check_mark: Application Gateway V2

Roughly 20% of all Internet traffic comes from bad bots. They do things like scraping, scanning, and looking for vulnerabilities in your web application. When these bots are stopped at the Web Application Firewall (WAF), they can’t attack you. They also can’t use up your resources and services, such as your backends and other underlying infrastructure.

You can enable a managed bot protection rule set for your WAF to block or log requests from known malicious IP addresses. The IP addresses are sourced from the Microsoft Threat Intelligence feed. Intelligent Security Graph powers Microsoft threat intelligence and is used by multiple services including Microsoft Defender for Cloud.

> [!NOTE]

> The Bot Protection Ruleset is only supported in the Azure public cloud, Azure China, and Azure US Government. The Bot Protection Ruleset is not supported in air-gapped clouds.

## Use with OWASP rulesets

You can use the Bot Protection ruleset alongside any of the OWASP rulesets with the Application Gateway WAF v2 SKU. Only one OWASP ruleset can be used at any given time. The bot protection ruleset contains another rule that appears in its own ruleset. It's titled **Microsoft_BotManagerRuleSet_1.1**, and you can  enable or disable it like the other OWASP rules.

## Ruleset update

The bot mitigation ruleset list of known bad IP addresses updates multiple times per day from the Microsoft Threat Intelligence feed to stay in sync with the bots. Your web applications are continuously protected even as the bot attack vectors change.

## Log example

Here's an example log entry for bot protection:

```

{

"timeStamp": "0000-00-00T00:00:00+00:00",

"resourceId": "appgw",

"operationName": "ApplicationGatewayFirewall",

"category": "ApplicationGatewayFirewallLog",

"properties": {

"instanceId": "vm1",

"clientIp": "1.2.3.4",

"requestUri": "/hello.php?arg1=aaaaaaabccc",

"ruleSetType": "MicrosoftBotProtection",

"message": "IPReputationTriggered",

"action": "Blocked",

"hostname": "example.com",

"transactionId": "abc",

"policyId": "waf policy 1",

"policyScope": "Global",

"policyScopeName": "Default Policy",

"engine": "Azwaf"

}

}

```

## Next steps

- [Configure bot protection for Web Application Firewall on Azure Application Gateway](bot-protection.md)


# Bot Protection

# Configure bot protection for Web Application Firewall on Azure Application Gateway

This article shows you how to configure a bot protection rule in Azure Web Application Firewall (WAF) for Application Gateway  using the Azure portal.

You can enable a managed bot protection rule set for your WAF to block or log requests from known malicious IP addresses. The IP addresses are sourced from the Microsoft Threat Intelligence feed. Intelligent Security Graph powers Microsoft threat intelligence and is used by multiple services including Microsoft Defender for Cloud.

## Prerequisites

Create a WAF policy for Application Gateway by following the instructions described in [Create Web Application Firewall policies for Application Gateway](create-waf-policy-ag.md).

## Enable bot protection rule set

1. In the Application Gateway WAF policy that you created previously, under **Settings**, select **Managed Rules**.

1. Select **Assign**.

1. On the **Assign managed rule sets** page, under **Additional rule set**, select the desired Bot Manager rule set.

1. Select **Save**.

## Next step

For more information about the Bot Manager rule set, see [Web Application Firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md?tabs=bot).


# Custom Waf Rules Overview

# Custom rules for Web Application Firewall v2 on Azure Application Gateway

**Applies to:** :heavy_check_mark: Application Gateway V2

The Azure Application Gateway Web Application Firewall (WAF) v2 includes a preconfigured, platform-managed ruleset that protects against many different types of attacks. These attacks include cross-site scripting, SQL injection, and others. If you're a WAF admin, you might want to write your own rules to augment the core rule set (CRS) rules. Your custom rules can block, allow, or log requested traffic based on matching criteria. If you set the WAF policy to detection mode and a custom block rule triggers, the request is logged and no blocking action is taken.

Use custom rules to create your own rules that the WAF evaluates for each request. These rules have a higher priority than the rest of the rules in the managed rule sets. The custom rules contain a rule name, rule priority, and an array of matching conditions. If these conditions are met, the WAF takes an action to allow, block, or log. If a custom rule triggers and the WAF takes an allow or block action, the WAF doesn't take any further actions from custom or managed rules. In the event of a custom rule triggering an allow or block action, you might still see some log events for rule matches from configured ruleset (Core Rule Set/Default Rule Set) but those rules aren't enforced. The log events show merely due to the optimization enforced by the WAF engine for parallel rule processing and can be safely ignored. You can enable or disable custom rules on demand.

For example, you can block all requests from an IP address in the range 192.168.5.0/24. In this rule, the operator is *IPMatch*, the matchValues is the IP address range (192.168.5.0/24), and the action is to block the traffic. You also set the rule's name, priority, and enabled or disabled state.

Custom rules support using compounding logic to make more advanced rules that address your security needs. For example, you  can use two custom rules to create the following logic ((rule1:Condition 1 **and** rule1:Condition 2) **or** rule2:Condition 3). This logic means that if Condition 1 **and** Condition 2 are met, **or** if Condition 3 is met, the WAF should take the action specified in the custom rules.

Different matching conditions within the same rule are always compounded using **and**. For example, block traffic from a specific IP address, and only if they're using a certain browser.

If you want to use **or** between two different conditions, then the two conditions must be in different rules. For example, block traffic from a specific IP address or block traffic if they're using a specific browser.

Custom rules also support regular expressions, just like in the CRS rulesets. For examples, see Examples 3 and 5 in [Create and use custom web application firewall rules](create-custom-waf-rules.md).

> [!NOTE]

> You can create up to 100 WAF custom rules. For more information about Application Gateway limits, see [Azure subscription and service limits, quotas, and constraints](../../azure-resource-manager/management/azure-subscription-service-limits.md#azure-application-gateway-limits).

> [!CAUTION]

> Any redirect rules you apply at the application gateway level bypass WAF custom rules. For more information, see [Application Gateway redirect overview](../../application-gateway/redirect-overview.md).

## Allowing vs. blocking

You can easily allow or block traffic by using custom rules. For example, you can block all traffic from a range of IP addresses. You can create another rule to allow traffic if the request comes from a specific browser.

To allow something, set the `-Action` parameter to **Allow**. To block something, set the `-Action` parameter to **Block**.

```azurepowershell

$AllowRule = New-AzApplicationGatewayFirewallCustomRule `

-Name example1 `

-Priority 2 `

-RuleType MatchRule `

-MatchCondition $condition `

-Action Allow `

-State Enabled

$BlockRule = New-AzApplicationGatewayFirewallCustomRule `

-Name example2 `

-Priority 2 `

-RuleType MatchRule `

-MatchCondition $condition `

-Action Block `

-State Enabled

```

The previous `$BlockRule` maps to the following custom rule in Azure Resource Manager:

```json

"customRules": [

{

"name": "blockEvilBot",

"priority": 2,

"ruleType": "MatchRule",

"action": "Block",

"state": "Enabled",

"matchConditions": [

{

"matchVariables": [

{

"variableName": "RequestHeaders",

"selector": "User-Agent"

}

],

"operator": "Contains",

"negationCondition": false,

"matchValues": [

"evilbot"

],

"transforms": [

"Lowercase"

]

}

]

}

],

```

This custom rule contains a name, priority, an action, and the array of matching conditions that must be met for the action to take place. For further explanation of these fields, see the following field descriptions. For example custom rules, see [Create and use custom web application firewall rules](create-custom-waf-rules.md).

> [!NOTE]

> WAF custom rules don't support allowing or blocking requests based on filenames or file types.

## Fields for custom rules

### Name [optional]

The name of the rule. It appears in the logs.

### Enable rule [optional]

Turn this rule on or off. Custom rules are enabled by default.

### Priority [required]

- Determines the rule valuation order. The lower the value, the earlier the evaluation of the rule. The allowable range is from 1 to 100.

- Must be unique across all custom rules. A rule with priority 40 is evaluated before a rule with priority 80.

### Rule type [required]

Currently, must be **MatchRule**.

### Match variable [required]

Must be one of the variables:

- RemoteAddr – IPv4 address or range of the remote computer connection

- RequestMethod – HTTP request method

- QueryString – Variable in the URI

- PostArgs – Arguments sent in the POST body. Custom rules that use this match variable apply only if the 'Content-Type' header is set to 'application/x-www-form-urlencoded' or 'multipart/form-data.' CRS version 3.2 or greater supports an additional content type of `application/json`, along with bot protection rule set and geo-match custom rules.

- RequestUri – URI of the request

- RequestHeaders – Headers of the request

- RequestBody – This variable contains the entire request body as a whole. Custom rules that use this match variable apply only if the 'Content-Type' header is set to `application/x-www-form-urlencoded` media type. CRS version 3.2 or greater supports additional content types of `application/soap+xml, application/xml, text/xml`, along with bot protection rule set and geo-match custom rules.

- RequestCookies – Cookies of the request

### Selector [optional]

Describes the field of the matchVariable collection. For example, if the matchVariable is RequestHeaders, the selector could be on the *User-Agent* header.

### Operator [required]

Use one of the following operators:

- `IPMatch` - Use only when the Match Variable is *RemoteAddr* and it supports only IPv4.

- `Equal` - Use when the input is the same as the MatchValue.

- `Any` - Use when there's no MatchValue. It's recommended for Match Variable with a valid Selector.

- `Contains` - Use when MatchValue is an explicit value only. Wildcard and regex aren't supported.

- `LessThan`

- `GreaterThan`

- LessThanOrEqual

- GreaterThanOrEqual

- BeginsWith

- `EndsWith`

- `Regex`

- `Geomatch`

### Negate condition [optional]

Negates the current condition.

### Transform [optional]

A list of string values that specify transformations to apply before attempting a match. The available transformations include:

- Lowercase

- Uppercase

- Trim

- UrlDecode

- UrlEncode

- RemoveNulls

- HtmlEntityDecode

### Match values [required]

A list of values to match against, which you can think of as being *OR*'ed. For example, the list could contain IP addresses or other strings. The value format depends on the previous operator.

> [!NOTE]

> If your WAF is running Core Rule Set (CRS) 3.1, or any other earlier CRS version, the match value only accepts letters, numbers, and punctuation marks. Quotation marks `"`, `'`, and spaces aren't supported.

Supported HTTP request method values include:

- GET

- HEAD

- POST

- OPTIONS

- PUT

- DELETE

- PATCH

### Action [required]

In WAF policy detection mode, if a custom rule is triggered, the action is always logged regardless of the action value set on the custom rule.

- Allow – Authorizes the transaction, skipping all other rules. The specified request is added to the allowlist and once matched, the request stops further evaluation and is sent to the backend pool. Rules that are on the allowlist aren't evaluated for any further custom rules or managed rules.

- Block - Blocks or logs the transaction based on SecDefaultAction (detection or prevention mode).

- Prevention mode - Blocks the transaction based on SecDefaultAction. Just like the `Allow` action, once the request is evaluated and added to the blocklist, evaluation stops and the request is blocked. Any request after that meets the same conditions isn't evaluated and is blocked.

- Detection mode - Logs the transaction based on SecDefaultAction after which evaluation stops. Any request after that meets the same conditions isn't evaluated and is logged.

- Log – Lets the rule write to the log, but lets the rest of the rules run for evaluation. The other custom rules are evaluated in order of priority, followed by the managed rules.

## Copying and duplicating custom rules

You can duplicate custom rules within a given policy. When you duplicate a rule, you need to specify a unique name for the rule and a unique priority value. Additionally, you can copy custom rules from one Application Gateway WAF policy to another as long as the policies are both in the same subscription. When you copy a rule from one policy to another, you need to select the Application Gateway WAF policy you wish to copy the rule into. Once you select the WAF policy, you need to give the rule a unique name, and assign a priority rank.

## Geomatch custom rules

Custom rules let you create tailored rules to suit the exact needs of your applications and security policies. You can restrict access to your web applications by country or region. For more information, see [Geomatch custom rules](geomatch-custom-rules.md).

## Next step

> [!div class="nextstepaction"]

> [Create your own custom rules](create-custom-waf-rules.md)


# Geomatch Custom Rules

# Geomatch custom rules

**Applies to:** :heavy_check_mark: Application Gateway V2

Custom rules let you create tailored rules to suit the exact needs of your applications and security policies. You can now restrict access to your web applications by country or region. As with all custom rules, you can combine this logic with other rules to suit the needs of your application.

To create a geo-filtering custom rule in the Azure portal, select *Geo location* as the Match Type, and then select the country or region or countries and regions you want to allow or block from your application. When creating geomatch rules by using Azure PowerShell or Azure Resource Manager, use the match variable `RemoteAddr` and the operator `Geomatch`. For more information, see [how to create custom rules in PowerShell](configure-waf-custom-rules.md) and more [custom rule examples](create-custom-waf-rules.md).

> [!NOTE]

> Geo-filtering works by mapping each request's IP address to a country or region. Some IP addresses in the data set might not yet be mapped to a country or region. To avoid accidentally blocking legitimate users, Application Gateway's WAF allows requests from unknown IP addresses.

> [!IMPORTANT]

> Include the country code **ZZ** whenever you use geo-filtering. The **ZZ** country code (or *Unknown* country/region) captures IP addresses that aren't yet mapped to a country or region in the dataset. This code avoids false positives.

## Country/region codes

> [!NOTE]

> Azure public cloud, Azure China, and Azure Government support geo-filtering custom rules. Air-gapped clouds don't support geo-filtering custom rules.

If you use the *geomatch* operator, use any of the following two-digit country/region codes.

| Country/region code | Country/region name |

| ----- | ----- |

| AD | Andorra |

| AE | United Arab Emirates |

| AF | Afghanistan |

| AG | Antigua and Barbuda |

| AI | Anguilla |

| AL | Albania |

| AM | Armenia |

| AO | Angola |

| AQ | Antarctica |

| AR | Argentina |

| AS | American Samoa |

| AT | Austria |

| AU | Australia |

| AW | Aruba |

| AX | Åland Islands |

| AZ | Azerbaijan |

| BA | Bosnia and Herzegovina |

| BB | Barbados |

| BD | Bangladesh |

| BE | Belgium |

| BF | Burkina Faso |

| BG | Bulgaria |

| BH | Bahrain |

| BI | Burundi |

| BJ | Benin |

| BL | Saint Barthélemy |

| BM | Bermuda |

| BN | Brunei |

| BO | Bolivia |

| BQ | Bonaire, Sint Eustatius, and Saba |

| BR | Brazil |

| BS | Bahamas |

| BT | Bhutan |

| BV | Bouvet Island |

| BW | Botswana |

| BY | Belarus |

| BZ | Belize |

| CA | Canada |

| CC | Cocos (Keeling) Islands |

| CD | Congo (DRC) |

| CF | Central African Republic |

| CG | Congo |

| CH | Switzerland |

| CI | Cote d'Ivoire |

| CK | Cook Islands |

| CL | Chile |

| CM | Cameroon |

| CN | China |

| CO | Colombia |

| CR | Costa Rica |

| CU | Cuba |

| CV | Cabo Verde |

| CW | Curaçao |

| CX | Christmas Island |

| CY | Cyprus |

| CZ | Czechia |

| DE | Germany |

| DJ | Djibouti |

| DK | Denmark |

| DM | Dominica |

| DO | Dominican Republic |

| DZ | Algeria |

| EC | Ecuador |

| EE | Estonia |

| EG | Egypt |

| ER | Eritrea |

| ES | Spain |

| ET | Ethiopia |

| FI | Finland |

| FJ | Fiji |

| FK | Falkland Islands |

| FM | Micronesia |

| FO | Faroe Islands |

| FR | France |

| GA | Gabon |

| GB | United Kingdom |

| GD | Grenada |

| GE | Georgia |

| GF | French Guiana |

| GG | Guernsey |

| GH | Ghana |

| GI | Gibraltar |

| GL | Greenland |

| GM | Gambia |

| GN | Guinea |

| GP | Guadeloupe |

| GQ | Equatorial Guinea |

| GR | Greece |

| GS | South Georgia and South Sandwich Islands |

| GT | Guatemala |

| GU | Guam |

| GW | Guinea-Bissau |

| GY | Guyana |

| HK | Hong Kong SAR |

| HM | Heard Island and McDonald Islands |

| HN | Honduras |

| HR | Croatia |

| HT | Haiti |

| HU | Hungary |

| ID | Indonesia |

| IE | Ireland |

| IL | Israel |

| IM | Isle of Man |

| IN | India |

| IO | British Indian Ocean Territory |

| IQ | Iraq |

| IR | Iran |

| IS | Iceland |

| IT | Italy |

| JE | Jersey |

| JM | Jamaica |

| JO | Jordan |

| JP | Japan |

| KE | Kenya |

| KG | Kyrgyzstan |

| KH | Cambodia |

| KI | Kiribati |

| KM | Comoros |

| KN | Saint Kitts and Nevis |

| KP | North Korea |

| KR | Korea |

| KW | Kuwait |

| KY | Cayman Islands |

| KZ | Kazakhstan |

| LA | Laos |

| LB | Lebanon |

| LC | Saint Lucia |

| LI | Liechtenstein |

| LK | Sri Lanka |

| LR | Liberia |

| LS | Lesotho |

| LT | Lithuania |

| LU | Luxembourg |

| LV | Latvia |

| LY | Libya |

| MA | Morocco |

| MC | Monaco |

| MD | Moldova |

| ME | Montenegro |

| MF | Saint Martin |

| MG | Madagascar |

| MH | Marshall Islands |

| MK | North Macedonia |

| ML | Mali |

| MM | Myanmar |

| MN | Mongolia |

| MO | Macao SAR |

| MP | Northern Mariana Islands |

| MQ | Martinique |

| MR | Mauritania |

| MS | Montserrat |

| MT | Malta |

| MU | Mauritius |

| MV | Maldives |

| MW | Malawi |

| MX | Mexico |

| MY | Malaysia |

| MZ | Mozambique |

| NA | Namibia |

| NC | New Caledonia |

| NE | Niger |

| NF | Norfolk Island |

| NG | Nigeria |

| NI | Nicaragua |

| NL | Netherlands |

| NO | Norway |

| NP | Nepal |

| NR | Nauru |

| NU | Niue |

| NZ | New Zealand |

| OM | Oman |

| PA | Panama |

| PE | Peru |

| PF | French Polynesia |

| PG | Papua New Guinea |

| PH | Philippines |

| PK | Pakistan |

| PL | Poland |

| PM | Saint Pierre and Miquelon |

| PN | Pitcairn Islands |

| PR | Puerto Rico |

| PS | Palestinian Authority |

| PT | Portugal |

| PW | Palau |

| PY | Paraguay |

| QA | Qatar |

| RE | Reunion |

| RO | Romania |

| RS | Serbia |

| RU | Russia |

| RW | Rwanda |

| SA | Saudi Arabia |

| SB | Solomon Islands |

| SC | Seychelles |

| SD | Sudan |

| SE | Sweden |

| SG | Singapore |

| SH | St Helena, Ascension, Tristan da Cunha |

| SI | Slovenia |

| SJ | Svalbard and Jan Mayen |

| SK | Slovakia |

| SL | Sierra Leone |

| SM | San Marino |

| SN | Senegal |

| SO | Somalia |

| SR | Suriname |

| SS | South Sudan |

| ST | São Tomé and Príncipe |

| SV | El Salvador |

| SX | Sint Maarten |

| SY | Syria |

| SZ | Eswatini |

| TC | Turks and Caicos Islands |

| TD | Chad |

| TF | French Southern Territories |

| TG | Togo |

| TH | Thailand |

| TJ | Tajikistan |

| TK | Tokelau |

| TL | Timor-Leste |

| TM | Turkmenistan |

| TN | Tunisia |

| TO | Tonga |

| TR | Türkiye |

| TT | Trinidad and Tobago |

| TV | Tuvalu |

| TW | Taiwan |

| TZ | Tanzania |

| UA | Ukraine |

| UG | Uganda |

| UM | U.S. Outlying Islands |

| US | United States |

| UY | Uruguay |

| UZ | Uzbekistan |

| VA | Vatican City |

| VC | Saint Vincent and the Grenadines |

| VE | Venezuela |

| VG | British Virgin Islands |

| VI | Virgin Islands, U.S. |

| VN | Vietnam |

| VU | Vanuatu |

| WF | Wallis and Futuna |

| WS | Samoa |

| YE | Yemen |

| YT | Mayotte |

| ZA | South Africa |

| ZM | Zambia |

| ZW | Zimbabwe |

## Related content

- [Create your own custom rules](create-custom-waf-rules.md)

- [Use Azure WAF geomatch custom rules to enhance network security](../geomatch-custom-rules-examples.md)


# Rate Limiting Overview

# What is rate limiting for Web Application Firewall on Application Gateway?

**Applies to:** :heavy_check_mark: Application Gateway V2

Rate limiting for Web Application Firewall on Application Gateway allows you to detect and block abnormally high levels of traffic destined for your application. By using rate limiting on Application Gateway WAF v2, you can mitigate many types of denial-of-service attacks, protect against clients that have accidentally been misconfigured to send large volumes of requests in a short time period, or control traffic rates to your site from specific geographies.

## Rate limiting policies

Rate limiting is configured using custom WAF rules in a policy.

> [!NOTE]

> Rate limit rules are only supported on Web Application Firewalls running the [latest WAF engine](waf-engine.md). In order to ensure you're using the latest engine, select CRS 3.2 for the default rule set. Additionally, rate limit rules are not supported in air-gapped clouds.

When you configure a rate limit rule, you must specify the threshold: the number of requests allowed within the specified time period. Rate limiting on Application Gateway WAF v2 uses a sliding window algorithm to determine when traffic has breached the threshold and needs to be dropped. During the first window where the threshold for the rule is breached, any more traffic matching the rate limit rule is dropped. From the second window onwards, traffic up to the threshold within the window configured is allowed, producing a throttling effect.

You must also specify a match condition, which tells the WAF when to activate the rate limit. You can configure multiple rate limit rules that match different variables and paths within your policy.

Application Gateway WAF v2 also introduces a *GroupByUserSession*, which must be configured. The *GroupByUserSession* specifies how requests are grouped and counted for a matching rate limit rule.

The following three *GroupByVariables* are currently available:

- ***ClientAddr*** – This is the default setting and it means that each rate limit threshold and mitigation applies independently to every unique source IP address.

- ***GeoLocation*** - Traffic is grouped by their geography based on a Geo-Match on the client IP address. So for a rate limit rule, traffic from the same geography is grouped together.

- ***None*** - All traffic is grouped together and counted against the threshold of the Rate Limit rule. When the threshold is breached, the action triggers against all traffic matching the rule and doesn't maintain independent counters for each client IP address or geography. It's recommended to use *None* with specific match conditions such as a sign-in page or a list of suspicious User-Agents.

- ***ClientAddrXFFHeader*** - Each rate limit threshold and mitigation applies independtly based on the IP Address found in the X-Forwarded-For header of the HTTP Request

- ***GeoLocationXFFHeader*** - Traffic is grouped by their geography based on a Geo-Match on the IP address found in the X-Forwarded-For header of the HTTP Request. For a rate limit rule, traffic from the same geography is grouped together.

## Rate limiting details

The configured rate limit thresholds are counted and tracked independently for each endpoint the Web Application Firewall policy is attached to. For example, a single WAF policy attached to five different listeners maintains independent counters and threshold enforcement for each of the listeners.

The rate limit thresholds aren't always enforced exactly as defined, so it shouldn't be used for fine-grain control of application traffic. Instead, it's recommended for mitigating anomalous rates of traffic and for maintaining application availability.

The  sliding window algorithm blocks all matching traffic for the first window in which the threshold is exceeded, and then throttles traffic in future windows. Use caution when defining thresholds when configuring wide-matching rules with either *GeoLocation* or *None* as the *GroupByVariables*. Incorrectly configured thresholds could lead to frequent short outages for matching traffic.

## Next step

> [!div class="nextstepaction"]

> [Create rate limiting custom rules for Application Gateway WAF v2](rate-limiting-configure.md)


# Configure Waf Custom Rules

# Configure Web Application Firewall v2 on Application Gateway with a custom rule using Azure PowerShell

Custom rules allow you to create your own rules evaluated for each request that passes through the Web Application Firewall (WAF) v2. These rules hold a higher priority than the rest of the rules in the managed rule sets. The custom rules have an action (to allow or block), a match condition, and an operator to allow full customization.

This article creates an Application Gateway WAF v2 that uses a custom rule. The custom rule blocks traffic if the request header contains User-Agent *evilbot*.

To see more custom rule examples, see [Create and use custom web application firewall rules](create-custom-waf-rules.md)

If you want run the Azure PowerShell in this article in one continuous script that you can copy, paste, and run, see [Azure Application Gateway PowerShell samples](powershell-samples.md).

## Prerequisites

### Azure PowerShell module

If you choose to install and use Azure PowerShell locally, this script requires the Azure PowerShell module version 2.1.0 or later.

1. To find the version, run `Get-Module -ListAvailable Az`. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell).

2. To create a connection with Azure, run `Connect-AzAccount`.

[!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

## Example script

### Set up variables

```azurepowershell

$rgname = "CustomRulesTest"

$location = "East US"

$appgwName = "WAFCustomRules"

```

### Create a resource group

```azurepowershell

$resourceGroup = New-AzResourceGroup -Name $rgname -Location $location

```

### Create a VNet

```azurepowershell

$sub1 = New-AzVirtualNetworkSubnetConfig -Name "appgwSubnet" -AddressPrefix "10.0.0.0/24"

$sub2 = New-AzVirtualNetworkSubnetConfig -Name "backendSubnet" -AddressPrefix "10.0.1.0/24"

$vnet = New-AzvirtualNetwork -Name "Vnet1" -ResourceGroupName $rgname -Location $location `

-AddressPrefix "10.0.0.0/16" -Subnet @($sub1, $sub2)

```

### Create a Static Public VIP

```azurepowershell

$publicip = New-AzPublicIpAddress -ResourceGroupName $rgname -name "AppGwIP" `

-location $location -AllocationMethod Static -Sku Standard

```

### Create pool and frontend port

```azurepowershell

$gwSubnet = Get-AzVirtualNetworkSubnetConfig -Name "appgwSubnet" -VirtualNetwork $vnet

$gipconfig = New-AzApplicationGatewayIPConfiguration -Name "AppGwIpConfig" -Subnet $gwSubnet

$fipconfig01 = New-AzApplicationGatewayFrontendIPConfig -Name "fipconfig" -PublicIPAddress $publicip

$pool = New-AzApplicationGatewayBackendAddressPool -Name "pool1" `

-BackendIPAddresses testbackend1.westus.cloudapp.azure.com, testbackend2.westus.cloudapp.azure.com

$fp01 = New-AzApplicationGatewayFrontendPort -Name "port1" -Port 80

```

### Create a listener, http setting, rule, and autoscale

```azurepowershell

$listener01 = New-AzApplicationGatewayHttpListener -Name "listener1" -Protocol Http `

-FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01

$poolSetting01 = New-AzApplicationGatewayBackendHttpSettings -Name "setting1" -Port 80 `

-Protocol Http -CookieBasedAffinity Disabled

$rule01 = New-AzApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType basic `

-BackendHttpSettings $poolSetting01 -HttpListener $listener01 -BackendAddressPool $pool -Priority 1000

$autoscaleConfig = New-AzApplicationGatewayAutoscaleConfiguration -MinCapacity 3

$sku = New-AzApplicationGatewaySku -Name WAF_v2 -Tier WAF_v2

```

### Create two custom rules and apply it to WAF policy

```azurepowershell

# Create a User-Agent header custom rule

$variable = New-AzApplicationGatewayFirewallMatchVariable -VariableName RequestHeaders -Selector User-Agent

$condition = New-AzApplicationGatewayFirewallCondition -MatchVariable $variable -Operator Contains -MatchValue "evilbot" -Transform Lowercase -NegationCondition $False

$rule = New-AzApplicationGatewayFirewallCustomRule -Name blockEvilBot -Priority 2 -RuleType MatchRule -MatchCondition $condition -Action Block -State Enabled

# Create a geo-match custom rule

$var2 = New-AzApplicationGatewayFirewallMatchVariable -VariableName RemoteAddr

$condition2 = New-AzApplicationGatewayFirewallCondition -MatchVariable $var2 -Operator GeoMatch -MatchValue "US"  -NegationCondition $False

$rule2 = New-AzApplicationGatewayFirewallCustomRule -Name allowUS -Priority 14 -RuleType MatchRule -MatchCondition $condition2 -Action Allow -State Enabled

# Create a firewall policy

$policySetting = New-AzApplicationGatewayFirewallPolicySetting -Mode Prevention -State Enabled

$wafPolicy = New-AzApplicationGatewayFirewallPolicy -Name wafpolicyNew -ResourceGroup $rgname -Location $location -PolicySetting $PolicySetting -CustomRule $rule,$rule2

```

### Create the Application Gateway

```azurepowershell

$appgw = New-AzApplicationGateway -Name $appgwName -ResourceGroupName $rgname `

-Location $location -BackendAddressPools $pool `

-BackendHttpSettingsCollection  $poolSetting01 `

-GatewayIpConfigurations $gipconfig -FrontendIpConfigurations $fipconfig01 `

-FrontendPorts $fp01 -HttpListeners $listener01 `

-RequestRoutingRules $rule01 -Sku $sku -AutoscaleConfiguration $autoscaleConfig `

-FirewallPolicy $wafPolicy

```

## Update your WAF

After you create your WAF, you can update it using a procedure similar to the following code:

```azurepowershell

# Get the existing policy

$policy = Get-AzApplicationGatewayFirewallPolicy -Name $policyName -ResourceGroupName $RGname

# Add an existing rule named $rule

$policy.CustomRules.Add($rule)

# Update the policy

Set-AzApplicationGatewayFirewallPolicy -InputObject $policy

```

## Next steps

[Learn more about Web Application Firewall on Application Gateway](ag-overview.md)


# Create Custom Waf Rules

# Create and use Web Application Firewall v2 custom rules on Application Gateway

**Applies to:** :heavy_check_mark: Application Gateway V2

The Web Application Firewall (WAF) v2 on Azure Application Gateway provides protection for web applications. This protection is provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS). In some cases, you may need to create your own custom rules to meet your specific needs. For more information about WAF custom rules, see [Custom web application firewall rules overview](custom-waf-rules-overview.md).

This article shows you some example custom rules that you can create and use with your v2 WAF. To learn how to deploy a WAF with a custom rule using Azure PowerShell, see [Configure Web Application Firewall custom rules using Azure PowerShell](configure-waf-custom-rules.md).

The JSON snippets shown in this article are derived from a [ApplicationGatewayWebApplicationFirewallPolicies](/azure/templates/microsoft.network/applicationgatewaywebapplicationfirewallpolicies) resource.

>[!NOTE]

> If your application gateway isn't using the WAF tier, the option to upgrade the application gateway to the WAF tier appears in the right pane.

## Example 1

You know there's a bot named *evilbot* that you want to block from crawling your website. In this case, you block on the User-Agent *evilbot* in the request headers.

Logic: p

```azurepowershell

$variable = New-AzApplicationGatewayFirewallMatchVariable `

-VariableName RequestHeaders `

-Selector User-Agent

$condition = New-AzApplicationGatewayFirewallCondition `

-MatchVariable $variable `

-Operator Contains `

-MatchValue "evilbot" `

-Transform Lowercase `

-NegationCondition $False

$rule = New-AzApplicationGatewayFirewallCustomRule `

-Name blockEvilBot `

-Priority 2 `

-RuleType MatchRule `

-MatchCondition $condition `

-Action Block `

-State Enabled

```

Corresponding JSON:

```json

{

"customRules": [

{

"name": "blockEvilBot",

"priority": 2,

"ruleType": "MatchRule",

"action": "Block",

"state": "Enabled",

"matchConditions": [

{

"matchVariables": [

{

"variableName": "RequestHeaders",

"selector": "User-Agent"

}

],

"operator": "Contains",

"negationCondition": false,

"matchValues": [

"evilbot"

],

"transforms": [

"Lowercase"

]

}

]

}

]

}

```

To see a WAF deployed using this custom rule, see [Configure a Web Application Firewall custom rule using Azure PowerShell](configure-waf-custom-rules.md).

### Example 1a

You can accomplish the same thing using a regular expression:

```azurepowershell

$variable = New-AzApplicationGatewayFirewallMatchVariable `

-VariableName RequestHeaders `

-Selector User-Agent

$condition = New-AzApplicationGatewayFirewallCondition `

-MatchVariable $variable `

-Operator Regex `

-MatchValue "evilbot" `

-Transform Lowercase `

-NegationCondition $False

$rule = New-AzApplicationGatewayFirewallCustomRule `

-Name blockEvilBot `

-Priority 2 `

-RuleType MatchRule `

-MatchCondition $condition `

-Action Block `

-State Enabled

```

Corresponding JSON:

```json

{

"customRules": [

{

"name": "blockEvilBot",

"priority": 2,

"ruleType": "MatchRule",

"action": "Block",

"state": "Enabled",

"matchConditions": [

{

"matchVariables": [

{

"variableName": "RequestHeaders",

"selector": "User-Agent"

}

],

"operator": "Regex",

"negationCondition": false,

"matchValues": [

"evilbot"

],

"transforms": [

"Lowercase"

]

}

]

}

]

}

```

## Example 2

You want to allow traffic only from the United States using the GeoMatch operator and still have the managed rules apply:

```azurepowershell

$variable = New-AzApplicationGatewayFirewallMatchVariable `

-VariableName RemoteAddr `

$condition = New-AzApplicationGatewayFirewallCondition `

-MatchVariable $variable `

-Operator GeoMatch `

-MatchValue "US" `

-Transform Lowercase `

-NegationCondition $True

$rule = New-AzApplicationGatewayFirewallCustomRule `

-Name "allowUS" `

-Priority 2 `

-RuleType MatchRule `

-MatchCondition $condition `

-Action Block `

-State Enabled

```

Corresponding JSON:

```json

{

"customRules": [

{

"name": "allowUS",

"priority": 2,

"ruleType": "MatchRule",

"action": "Block",

"state": "Enabled",

"matchConditions": [

{

"matchVariables": [

{

"variableName": "RemoteAddr"

}

],

"operator": "GeoMatch",

"negationCondition": true,

"matchValues": [

"US"

],

"transforms": [

"Lowercase"

]

}

]

}

]

}

```

## Example 3

You want to block all requests from IP addresses in the range 198.168.5.0/24.

In this example, you block all traffic that comes from an IP addresses range. The name of the rule is *myrule1* and the priority is set to 10.

Logic: p

```azurepowershell

$variable1 = New-AzApplicationGatewayFirewallMatchVariable `

-VariableName RemoteAddr

$condition1 = New-AzApplicationGatewayFirewallCondition `

-MatchVariable $variable1 `

-Operator IPMatch `

-MatchValue "192.168.5.0/24" `

-NegationCondition $False

$rule = New-AzApplicationGatewayFirewallCustomRule `

-Name myrule1 `

-Priority 10 `

-RuleType MatchRule `

-MatchCondition $condition1 `

-Action Block `

-State Enabled

```

Corresponding JSON:

```json

{

"customRules": [

{

"name": "myrule1",

"priority": 10,

"ruleType": "MatchRule",

"action": "Block",

"state": "Enabled",

"matchConditions": [

{

"matchVariables": [

{

"variableName": "RemoteAddr"

}

],

"operator": "IPMatch",

"negationCondition": false,

"matchValues": [

"192.168.5.0/24"

],

"transforms": []

}

]

}

]

}

```

Corresponding CRS rule:

`SecRule REMOTE_ADDR "@ipMatch 192.168.5.0/24" "id:7001,deny"`

## Example 4

For this example, you want to block User-Agent *evilbot*, and traffic in the range 192.168.5.0/24. To accomplish this action, you can create two separate match conditions, and put them both in the same rule. This configuration ensures that if both *evilbot* in the User-Agent header **and** IP addresses from the range 192.168.5.0/24 are matched, then the request is blocked.

Logic: p **and** q

```azurepowershell

$variable1 = New-AzApplicationGatewayFirewallMatchVariable `

-VariableName RemoteAddr

$variable2 = New-AzApplicationGatewayFirewallMatchVariable `

-VariableName RequestHeaders `

-Selector User-Agent

$condition1 = New-AzApplicationGatewayFirewallCondition `

-MatchVariable $variable1 `

-Operator IPMatch `

-MatchValue "192.168.5.0/24" `

-NegationCondition $False

$condition2 = New-AzApplicationGatewayFirewallCondition `

-MatchVariable $variable2 `

-Operator Contains `

-MatchValue "evilbot" `

-Transform Lowercase `

-NegationCondition $False

$rule = New-AzApplicationGatewayFirewallCustomRule `

-Name myrule `

-Priority 10 `

-RuleType MatchRule `

-MatchCondition $condition1, $condition2 `

-Action Block `

-State Enabled

```

Corresponding JSON:

```json

{

"customRules": [

{

"name": "myrule",

"priority": 10,

"ruleType": "MatchRule",

"action": "Block",

"state": "Enabled",

"matchConditions": [

{

"matchVariables": [

{

"variableName": "RemoteAddr"

}

],

"operator": "IPMatch",

"negationCondition": false,

"matchValues": [

"192.168.5.0/24"

],

"transforms": []

},

{

"matchVariables": [

{

"variableName": "RequestHeaders",

"selector": "User-Agent"

}

],

"operator": "Contains",

"negationCondition": false,

"matchValues": [

"evilbot"

],

"transforms": [

"Lowercase"

]

}

]

}

]

}

```

## Example 5

For this example, you want to block if the request is either outside of the IP address range *192.168.5.0/24*, or the user agent string isn't *chrome* (meaning the user isn’t using the Chrome browser). Since this logic uses **or**, the two conditions are in separate rules as seen in the following example. *myrule1* and *myrule2* both need to match to block the traffic.

Logic: **not** (p **and** q) = **not** p **or not** q.

```azurepowershell

$variable1 = New-AzApplicationGatewayFirewallMatchVariable `

-VariableName RemoteAddr

$variable2 = New-AzApplicationGatewayFirewallMatchVariable `

-VariableName RequestHeaders `

-Selector User-Agent

$condition1 = New-AzApplicationGatewayFirewallCondition `

-MatchVariable $variable1 `

-Operator IPMatch `

-MatchValue "192.168.5.0/24" `

-NegationCondition $True

$condition2 = New-AzApplicationGatewayFirewallCondition `

-MatchVariable $variable2 `

-Operator Contains `

-MatchValue "chrome" `

-Transform Lowercase `

-NegationCondition $True

$rule1 = New-AzApplicationGatewayFirewallCustomRule `

-Name myrule1 `

-Priority 10 `

-RuleType MatchRule `

-MatchCondition $condition1 `

-Action Block `

-State Enabled

$rule2 = New-AzApplicationGatewayFirewallCustomRule `

-Name myrule2 `

-Priority 20 `

-RuleType MatchRule `

-MatchCondition $condition2 `

-Action Block `

-State Enabled

```

Corresponding JSON:

```json

{

"customRules": [

{

"name": "myrule1",

"priority": 10,

"ruleType": "MatchRule",

"action": "Block",

"state": "Enabled",

"matchConditions": [

{

"matchVariables": [

{

"variableName": "RemoteAddr"

}

],

"operator": "IPMatch",

"negationCondition": true,

"matchValues": [

"192.168.5.0/24"

],

"transforms": []

}

]

},

{

"name": "myrule2",

"priority": 20,

"ruleType": "MatchRule",

"action": "Block",

"state": "Enabled",

"matchConditions": [

{

"matchVariables": [

{

"variableName": "RequestHeaders",

"selector": "User-Agent"

}

],

"operator": "Contains",

"negationCondition": true,

"matchValues": [

"chrome"

],

"transforms": [

"Lowercase"

]

}

]

}

]

}

```

## Example 6

You want to only allow requests from specific known user agents and block any requests where the user agent isn't present. You will need to create two custom rules for this scenario; one to block any requests where user agent is missing, and a second rule to block any requests with an unauthorized user agent.

### Rule 1

```azurepowershell

$variable = New-AzApplicationGatewayFirewallMatchVariable `

-VariableName RequestHeaders `

-Selector User-Agent

$condition = New-AzApplicationGatewayFirewallCondition `

-MatchVariable $variable `

-Operator Any `

-NegationCondition $True

$rule = New-AzApplicationGatewayFirewallCustomRule `

-Name BlockMissingUserAgents `

-Priority 1 `

-RuleType MatchRule `

-MatchCondition $condition `

-Action Block `

-State Enabled

```

Corresponding JSON:

```json

[

{

"name": "BlockMissingUserAgents",

"priority": 1,

"ruleType": "MatchRule",

"matchConditions": [

{

"matchVariables": [

{

"variableName": "RequestHeaders",

"selector": "User-Agent"

}

],

"operator": "Any",

"negationConditon": true,

"matchValues": [

".*"

],

"transforms": []

}

],

"action": "Block",

"state": "Enabled"

},

```

### Rule 2

Because the logic used here is **or**, and all the values are in the *User-Agent* header, all of the *MatchValues* can be in a comma-separated list.

Logic: p **or** q **or** r

```azurepowershell

$variable = New-AzApplicationGatewayFirewallMatchVariable `

-VariableName RequestHeaders `

-Selector User-Agent

$condition = New-AzApplicationGatewayFirewallCondition `

-MatchVariable $variable `

-Operator Equal `

-MatchValue @('user1', 'user2') `

-NegationCondition $True

$rule = New-AzApplicationGatewayFirewallCustomRule `

-Name BlockUnknownUserAgents `

-Priority 2 `

-RuleType MatchRule `

-MatchCondition $condition `

-Action Block `

-State Enabled

```

Corresponding JSON:

```json

{

"customRules": [

{

"name": "BlockUnknownUserAgents",

"priority": 2,

"ruleType": "MatchRule",

"action": "Block",

"state": "Enabled",

"matchConditions": [

{

"matchVariables": [

{

"variableName": "RequestHeaders",

"selector": "User-Agent"

}

],

"operator": "Equal",

"negationCondition": true,

"matchValues": [

"user1",

"user2"

],

"transforms": []

}

]

}

]

}

```

## Example 7

It isn't uncommon to see Azure Front Door deployed in front of Application Gateway. In order to make sure the traffic received by Application Gateway comes from the Front Door deployment, the best practice is to check if the `X-Azure-FDID` header contains the expected unique value.  For more information on securing access to your application using Azure Front Door, see [How to lock down the access to my backend to only Azure Front Door](../../frontdoor/front-door-faq.yml#what-are-the-steps-to-restrict-the-access-to-my-backend-to-only-azure-front-door-)

Logic: **not** p

```azurepowershell

$expectedFDID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

$variable = New-AzApplicationGatewayFirewallMatchVariable `

-VariableName RequestHeaders `

-Selector X-Azure-FDID

$condition = New-AzApplicationGatewayFirewallCondition `

-MatchVariable $variable `

-Operator Equal `

-MatchValue $expectedFDID `

-Transform Lowercase `

-NegationCondition $True

$rule = New-AzApplicationGatewayFirewallCustomRule `

-Name blockNonAFDTraffic `

-Priority 2 `

-RuleType MatchRule `

-MatchCondition $condition `

-Action Block `

-State Enabled

```

Corresponding JSON:

```json

{

"customRules": [

{

"name": "blockNonAFDTraffic",

"priority": 2,

"ruleType": "MatchRule",

"action": "Block",

"state": "Enabled",

"matchConditions": [

{

"matchVariables": [

{

"variableName": "RequestHeaders",

"selector": "X-Azure-FDID"

}

],

"operator": "Equal",

"negationCondition": true,

"matchValues": [

"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

],

"transforms": [

"Lowercase"

]

}

]

}

]

}

```

## Next step

After you create your custom rules, you can learn how to view your WAF logs. For more information, see [Application Gateway diagnostics](../../application-gateway/application-gateway-diagnostics.md#diagnostic-logging).


# Rate Limiting Configure

# Create rate limiting custom rules for Application Gateway WAF v2

**Applies to:** :heavy_check_mark: Application Gateway V2

Rate limiting enables you to detect and block abnormally high levels of traffic destined for your application. Rate Limiting works by counting all traffic that matches the configured Rate Limit rule and performing the configured action for traffic matching that rule which exceeds the configured threshold. For more information, see [Rate limiting overview](rate-limiting-overview.md).

## Configure Rate Limit Custom Rules

Use the following information to configure Rate Limit Rules for Application Gateway WAFv2.

**Scenario One** -  Create rule to rate-limit traffic by Client IP that exceeds the configured threshold, matching all traffic.

#### [Portal](#tab/browser)

1. Open an existing Application Gateway WAF Policy.

1. Select **Custom Rules**.

1. Select **Add Custom Rule**.

1. Type a name for the custom rule.

1. For the **Rule type**, select **Rate limit**.

1. Type a **Priority** for the rule.

1. Choose **1 minute** for **Rate limit duration**.

1. Type **200** for **Rate limit threshold (requests)**.

1. Select **Client address** for **Group rate limit traffic by**.

1. Under **Conditions**, choose **IP address** for **Match type**.

1. For **Operation**, select **Does not contain**.

1. For match condition, under **IP address or range**, type **255.255.255.255/32**.

1. Leave action setting to **Deny traffic**.

1. Select **Add** to add the custom rule to the policy.

1. Select **Save** to save the configuration and make the custom rule active for the WAF policy.

#### [PowerShell](#tab/powershell)

```azurepowershell

$variable = New-AzApplicationGatewayFirewallMatchVariable -VariableName RemoteAddr

$condition = New-AzApplicationGatewayFirewallCondition -MatchVariable $variable -Operator IPMatch -MatchValue 255.255.255.255/32 -NegationCondition $True

$groupByVariable = New-AzApplicationGatewayFirewallCustomRuleGroupByVariable -VariableName ClientAddr

$groupByUserSession = New-AzApplicationGatewayFirewallCustomRuleGroupByUserSession -GroupByVariable $groupByVariable

$ratelimitrule = New-AzApplicationGatewayFirewallCustomRule -Name ClientIPRateLimitRule -Priority 90 -RateLimitDuration OneMin -RateLimitThreshold 100 -RuleType RateLimitRule -MatchCondition $condition -GroupByUserSession $groupByUserSession -Action Block -State Enabled

```

#### [CLI](#tab/cli)

```azurecli

az network application-gateway waf-policy custom-rule create --policy-name ExamplePolicy --resource-group ExampleRG --action Block --name ClientIPRateLimitRule --priority 90 --rule-type RateLimitRule --rate-limit-threshold 100 --group-by-user-session '[{'"groupByVariables"':[{'"variableName"':'"ClientAddr"'}]}]'

az network application-gateway waf-policy custom-rule match-condition add --match-variables RemoteAddr --operator IPMatch --policy-name ExamplePolicy --name ClientIPRateLimitRule --resource-group ExampleRG --value 255.255.255.255/32 --negate true

```

* * *

**Scenario Two** - Create Rate Limit Custom Rule to match all traffic except for traffic originating from the United States.  Traffic is grouped, counted, and rate limited based on the GeoLocation of the Client Source IP address

#### [Portal](#tab/browser)

1. Open an existing Application Gateway WAF Policy.

1. Select **Custom Rules**.

1. Select **Add Custom Rule**.

1. Type a name for the custom rule.

1. For the **Rule type**, select **Rate limit**.

1. Type a **Priority** for the rule.

1. Choose **1 minute** for **Rate limit duration**.

1. Type **500** for **Rate limit threshold (requests)**.

1. Select **Geo location** for **Group rate limit traffic by**.

1. Under **Conditions**, choose **Geo location** for **Match type**.

1. In the **Match variables section, select **RemoteAddr** for **Match variable**.

1. Select **Is not** for **Operation**.

1. Select **United States** for **Country/Region**.

1. Leave action setting to **Deny traffic**.

1. Select **Add** to add the custom rule to the policy.

1. Select **Save** to save the configuration and make the custom rule active for the WAF policy.

#### [PowerShell](#tab/powershell)

```azurepowershell

$variable = New-AzApplicationGatewayFirewallMatchVariable -VariableName RemoteAddr

$condition = New-AzApplicationGatewayFirewallCondition -MatchVariable $variable -Operator GeoMatch -MatchValue "US" -NegationCondition $True

$groupByVariable = New-AzApplicationGatewayFirewallCustomRuleGroupByVariable -VariableName GeoLocation

$groupByUserSession = New-AzApplicationGatewayFirewallCustomRuleGroupByUserSession -GroupByVariable $groupByVariable

$ratelimitrule = New-AzApplicationGatewayFirewallCustomRule -Name GeoRateLimitRule -Priority 95 -RateLimitDuration OneMin -RateLimitThreshold 500 -RuleType RateLimitRule -MatchCondition $condition -GroupByUserSession $groupByUserSession -Action Block -State Enabled

```

#### [CLI](#tab/cli)

```azurecli

az network application-gateway waf-policy custom-rule create --policy-name ExamplePolicy --resource-group ExampleRG --action Block --name GeoRateLimitRule --priority 95 --rule-type RateLimitRule --rate-limit-threshold 500 --group-by-user-session '[{'"groupByVariables"':[{'"variableName"':'"GeoLocation"'}]}]'

az network application-gateway waf-policy custom-rule match-condition add --match-variables RemoteAddr --operator GeoMatch --policy-name ExamplePolicy --name GeoRateLimitRule --resource-group ExampleRG --value US --negate true

```

* * *

**Scenario Three** - Create Rate Limit Custom Rule matching all traffic for the login page, and using the GroupBy None variable.  This will group and count all traffic which matches the rule as one, and apply the action across all traffic matching the rule (/login).

#### [Portal](#tab/browser)

1. Open an existing Application Gateway WAF Policy.

1. Select **Custom Rules**.

1. Select **Add Custom Rule**.

1. Type a name for the custom rule.

1. For the **Rule type**, select **Rate limit**.

1. Type a **Priority** for the rule.

1. Choose **1 minute** for **Rate limit duration**.

1. Type **100** for **Rate limit threshold (requests)**.

1. Select **None** for **Group rate limit traffic by**.

1. Under **Conditions**, choose **String** for **Match type**.

1. In the **Match variables** section, select **RequestUri** for **Match variable**.

1. Select **Is** for **Operation**.

1. For **Operator** select **Contains**.

1. Selecting a transformation is optional.

1. Enter Login page path for match Value.  In this example we use **/login**.

1. Leave action setting to **Deny traffic**.

1. Select **Add** to add the custom rule to the policy

1. Select **Save** to save the configuration and make the custom rule active for the WAF policy.

#### [PowerShell](#tab/powershell)

```azurepowershell

$variable = New-AzApplicationGatewayFirewallMatchVariable -VariableName RequestUri

$condition = New-AzApplicationGatewayFirewallCondition -MatchVariable $variable -Operator Contains -MatchValue "/login" -NegationCondition $True

$groupByVariable = New-AzApplicationGatewayFirewallCustomRuleGroupByVariable -VariableName None

$groupByUserSession = New-AzApplicationGatewayFirewallCustomRuleGroupByUserSession -GroupByVariable $groupByVariable

$ratelimitrule = New-AzApplicationGatewayFirewallCustomRule -Name LoginRateLimitRule -Priority 99 -RateLimitDuration OneMin -RateLimitThreshold 100 -RuleType RateLimitRule -MatchCondition $condition -GroupByUserSession $groupByUserSession -Action Block -State Enabled

```

#### [CLI](#tab/cli)

```azurecli

az network application-gateway waf-policy custom-rule create --policy-name ExamplePolicy --resource-group ExampleRG --action Block --name LoginRateLimitRule --priority 99 --rule-type RateLimitRule --rate-limit-threshold 100 --group-by-user-session '[{'"groupByVariables"':[{'"variableName"':'"None"'}]}]'

az network application-gateway waf-policy custom-rule match-condition add --match-variables RequestUri --operator Contains --policy-name ExamplePolicy --name LoginRateLimitRule --resource-group ExampleRG --value '/login'

```

* * *

## Next steps

[Customize web application firewall rules](application-gateway-customize-waf-rules-portal.md)


# Geomatch Custom Rules Examples

# Use Azure WAF geomatch custom rules to enhance network security

Web application firewall (WAF) is an important tool that helps protect web applications from harmful attacks. It can filter, monitor, and stop web traffic using both preset and custom rules. You can make your own rule that the WAF checks for every request it gets. Custom rules have higher priority than the managed rules and are checked first.

One of the most powerful features of Azure Web Application Firewall is geomatch custom rules. These rules let you match web requests to the geographic location of where they come from. You might want to stop requests from certain places known for harmful activity, or you might want to allow requests from places important to your business. Geomatch custom rules can also help you follow data sovereignty and privacy laws by limiting access to your web applications based on the location of the people using them.

Use the priority parameter wisely when using geomatch custom rules to avoid unnecessary processing or conflicts. Azure WAF evaluates rules in the order determined by the priority parameter, a numerical value ranging from 1 to 100, with lower values indicating higher priority. The priority must be unique across all custom rules. Assign higher priority to critical or specific rules for your web application security and lower priority to less essential or general rules. Doing so ensures WAF applies the most appropriate actions to your web traffic. For example, the scenario where you identify an explicit URI path is the most specific and should have a higher priority rule than other types of patterns. Having the highest priority protects a critical path on the application while allowing more generic traffic to be evaluated across other custom rules or managed rulesets.

Always test your rules before applying them to production environment and regularly monitor their performance and impact. By following these best practices, you can enhance your web application security using the power of geomatch custom rules.

This article introduces Azure WAF geomatch custom rules and shows you how to create and manage them using the Azure portal, Bicep, and Azure PowerShell.

## Geomatch custom rule patterns

Geomatch custom rules enable you to meet diverse security goals, such as blocking requests from high-risk areas and permitting requests from trusted locations. They're effective in mitigating distributed denial-of-service (DDoS) attacks, which seek to inundate your web application with a multitude of requests from various sources. With geomatch custom rules, you can promptly pinpoint and block regions generating the most DDoS traffic, while still granting access to legitimate users. In this article, you learn about various custom rule patterns that you can employ to optimize your Azure WAF using geomatch custom rules.

### Scenario 1 - Block traffic from all countries or regions except "x"

Geomatch custom rules prove useful when you aim to block traffic from all countries or regions, barring one. For instance, if your web application caters exclusively to users in the United States, you can formulate a geomatch custom rule that obstructs all requests not originating from the US. This strategy effectively minimizes your web application’s attack surface and deters unauthorized access from other regions. This specific technique employs a negating condition to facilitate this traffic pattern. For creating a geomatch custom rule that obstructs traffic from all countries or regions except the US, see to the following portal, PowerShell, or Bicep examples:

# [**Portal**](#tab/portal)

> [!NOTE]

> On the Azure Front Door WAF, you use `SocketAddr` as the match variable and not `RemoteAddr`. The `RemoteAddr` variable is the original client IP address that's usually sent via the `X-Forwarded-For` request header. The `SocketAddr` variable is the source IP address the WAF sees.

# [**PowerShell**](#tab/powershell)

```azurepowershell-interactive

$RGname = "rg-waf "

$policyName = "waf-pol"

$variable = New-AzApplicationGatewayFirewallMatchVariable -VariableName RemoteAddr

$condition = New-AzApplicationGatewayFirewallCondition -MatchVariable $variable -Operator GeoMatch -MatchValue "US" -NegationCondition $true

$rule = New-AzApplicationGatewayFirewallCustomRule -Name GeoRule1 -Priority 10 -RuleType MatchRule -MatchCondition $condition -Action Block

$policy = Get-AzApplicationGatewayFirewallPolicy -Name $policyName -ResourceGroupName $RGname

$policy.CustomRules.Add($rule)

Set-AzApplicationGatewayFirewallPolicy -InputObject $policy

```

```azurepowershell-interactive

$RGname = "rg-waf"

$policyName = "wafafdpol"

$matchCondition = New-AzFrontDoorWafMatchConditionObject -MatchVariable SocketAddr -OperatorProperty GeoMatch -MatchValue "US" -NegateCondition $true

$customRuleObject = New-AzFrontDoorWafCustomRuleObject -Name "GeoRule1" -RuleType MatchRule -MatchCondition $matchCondition -Action Block -Priority 10

$afdWAFPolicy= Get-AzFrontDoorWafPolicy -Name $policyName -ResourceGroupName $RGname

Update-AzFrontDoorWafPolicy -InputObject $afdWAFPolicy -Customrule $customRuleObject

```

# [**Bicep**](#tab/bicep)

```Bicep

properties: {

customRules: [

{

name: 'GeoRule1'

priority: 10

ruleType: 'MatchRule'

action: 'Block'

matchConditions: [

{

matchVariables: [

{

variableName: 'RemoteAddr'

}

]

operator: 'GeoMatch'

negationCondition: true

matchValues: [

'US'

]

transforms: []

}

]

state: 'Enabled'

}

```

```Bicep

properties: {

customRules: {

rules: [

{

name: 'GeoRule1'

enabledState: 'Enabled'

priority: 10

ruleType: 'MatchRule'

matchConditions: [

{

matchVariable: 'SocketAddr'

operator: 'GeoMatch'

negateCondition: true

matchValue: [

'US'

]

transforms: []

}

]

action: 'Block'

}

```

---

### Scenario 2 - Block traffic from all countries or regions except "x" and "y" that target the URI "foo" or "bar"

Consider a scenario where you need to use geomatch custom rules to block traffic from all countries or regions, except for two or more specific ones, targeting a specific URI. Suppose your web application has specific URI paths intended only for users in the US and Canada. In this case, you create a geomatch custom rule that blocks all requests not originating from these countries or regions.

This pattern processes request payloads from the US and Canada through the managed rulesets, catching any malicious attacks, while blocking requests from all other countries or regions. This approach ensures that only your target audience can access your web application, avoiding unwanted traffic from other regions.

To minimize potential false positives, include the country code **ZZ** in the list to capture IP addresses not yet mapped to a country or region in Azure’s dataset. This technique uses a negate condition for the Geolocation type and a non-negate condition for the URI match.

To create a geomatch custom rule that blocks traffic from all countries or regions except the US and Canada to a specified URI, refer to the portal, PowerShell, and Bicep examples.

# [**Portal**](#tab/portal)

# [**PowerShell**](#tab/powershell)

```azurepowershell-interactive

$RGname = "rg-waf "

$policyName = "waf-pol"

$variable1a = New-AzApplicationGatewayFirewallMatchVariable -VariableName RemoteAddr

$condition1a = New-AzApplicationGatewayFirewallCondition -MatchVariable $variable1a -Operator GeoMatch -MatchValue @(“US”, “CA”) -NegationCondition $true

$variable1b = New-AzApplicationGatewayFirewallMatchVariable -VariableName RequestUri

$condition1b = New-AzApplicationGatewayFirewallCondition -MatchVariable $variable1b -Operator Contains -MatchValue @(“/foo”, “/bar”) -NegationCondition $false

$rule1 = New-AzApplicationGatewayFirewallCustomRule -Name GeoRule2 -Priority 11 -RuleType MatchRule -MatchCondition $condition1a, $condition1b -Action Block

$policy = Get-AzApplicationGatewayFirewallPolicy -Name $policyName -ResourceGroupName $RGname

$policy.CustomRules.Add($rule1)

Set-AzApplicationGatewayFirewallPolicy -InputObject $policy

```

```azurepowershell-interactive

$RGname = "rg-waf"

$policyName = "wafafdpol"

$matchCondition1a = New-AzFrontDoorWafMatchConditionObject -MatchVariable SocketAddr -OperatorProperty GeoMatch -MatchValue @(“US”, "CA") -NegateCondition $true

$matchCondition1b = New-AzFrontDoorWafMatchConditionObject -MatchVariable RequestUri -OperatorProperty Contains -MatchValue @(“/foo”, “/bar”) -NegateCondition $false

$customRuleObject1 = New-AzFrontDoorWafCustomRuleObject -Name "GeoRule2" -RuleType MatchRule -MatchCondition $matchCondition1a, $matchCondition1b -Action Block -Priority 11

$afdWAFPolicy= Get-AzFrontDoorWafPolicy -Name $policyName -ResourceGroupName $RGname

Update-AzFrontDoorWafPolicy -InputObject $afdWAFPolicy -Customrule $customRuleObject1

```

# [**Bicep**](#tab/bicep)

```Bicep

properties: {

customRules: [

{

name: 'GeoRule2'

priority: 11

ruleType: 'MatchRule'

action: 'Block'

matchConditions: [

{

matchVariables: [

{

variableName: 'RemoteAddr'

}

]

operator: 'GeoMatch'

negationCondition: true

matchValues: [

'US'

'CA'

]

transforms: []

}

{

matchVariables: [

{

variableName: 'RequestUri'

}

]

operator: 'Contains'

negationCondition: false

matchValues: [

'/foo'

'/bar'

]

transforms: []

}

]

state: 'Enabled'

}

```

```Bicep

properties: {

customRules: {

rules: [

{

name: 'GeoRule2'

enabledState: 'Enabled'

priority: 11

ruleType: 'MatchRule'

matchConditions: [

{

matchVariable: 'SocketAddr'

operator: 'GeoMatch'

negateCondition: true

matchValue: [

'US'

'CA'

]

transforms: []

}

{

matchVariable: 'RequestUri'

operator: 'Contains'

negateCondition: false

matchValue: [

'/foo'

'/bar'

]

transforms: []

}

]

action: 'Block'

}

```

---

### Scenario 3 - Block traffic specifically from country or region "x"

You can use geomatch custom rules to block traffic from specific countries or regions. For instance, if your web application receives many malicious requests from country or region "x", create a geomatch custom rule to block all requests from that country or region. This protects your web application from potential attacks and reduces resource load. Apply this pattern to block multiple malicious or hostile countries or regions. This technique requires a match condition for the traffic pattern. To block traffic from country or region "x", see the following portal, PowerShell, and Bicep examples.

# [**Portal**](#tab/portal)

# [**PowerShell**](#tab/powershell)

```azurepowershell-interactive

$RGname = "rg-waf "

$policyName = "waf-pol"

$variable2 = New-AzApplicationGatewayFirewallMatchVariable -VariableName RemoteAddr

$condition2 = New-AzApplicationGatewayFirewallCondition -MatchVariable $variable2 -Operator GeoMatch -MatchValue "US" -NegationCondition $false

$rule2 = New-AzApplicationGatewayFirewallCustomRule -Name GeoRule3 -Priority 12 -RuleType MatchRule -MatchCondition $condition2 -Action Block

$policy = Get-AzApplicationGatewayFirewallPolicy -Name $policyName -ResourceGroupName $RGname

$policy.CustomRules.Add($rule2)

Set-AzApplicationGatewayFirewallPolicy -InputObject $policy

```

```azurepowershell-interactive

$RGname = "rg-waf"

$policyName = "wafafdpol"

$matchCondition2 = New-AzFrontDoorWafMatchConditionObject -MatchVariable SocketAddr -OperatorProperty GeoMatch -MatchValue "US" -NegateCondition $false

$customRuleObject2 = New-AzFrontDoorWafCustomRuleObject -Name "GeoRule3" -RuleType MatchRule -MatchCondition $matchCondition2 -Action Block -Priority 12

$afdWAFPolicy= Get-AzFrontDoorWafPolicy -Name $policyName -ResourceGroupName $RGname

Update-AzFrontDoorWafPolicy -InputObject $afdWAFPolicy -Customrule $customRuleObject2

```

# [**Bicep**](#tab/bicep)

```Bicep

properties: {

customRules: [

{

name: 'GeoRule3'

priority: 12

ruleType: 'MatchRule'

action: 'Block'

matchConditions: [

{

matchVariables: [

{

variableName: 'RemoteAddr'

}

]

operator: 'GeoMatch'

negationCondition: false

matchValues: [

'US'

]

transforms: []

}

]

state: 'Enabled'

}

```

```Bicep

properties: {

customRules: {

rules: [

{

name: 'GeoRule3'

enabledState: 'Enabled'

priority: 12

ruleType: 'MatchRule'

matchConditions: [

{

matchVariable: 'SocketAddr'

operator: 'GeoMatch'

negateCondition: false

matchValue: [

'US'

]

transforms: []

}

]

action: 'Block'

}

```

---

## Geomatch custom rule anti-patterns

Avoid anti-patterns when using geomatch custom rules, such as setting the custom rule action to `allow` instead of `block`. This can have unintended consequences, like allowing traffic to bypass the WAF and potentially exposing your web application to other threats.

Instead of using an `allow` action, use a `block` action with a negate condition, as shown in previous patterns. This ensures only traffic from desired countries or regions is allowed and the WAF blocks all other traffic.

### Scenario 4 - allow traffic from country or region "x"

Avoid setting the geomatch custom rule to allow traffic from a specific country or region. For example, if you want to allow traffic from the United States because of a large customer base, creating a custom rule with the action `allow` and the value `United States` might seem like the solution. However, this rule allows all traffic from the United States, regardless of whether it has a malicious payload or not, as the `allow` action bypasses further rule processing of managed rulesets. Additionally, the WAF still processes traffic from all other countries or regions, consuming resources. This exposes your web application to malicious requests from the United States that the WAF would otherwise block.

### Scenario 5 - Allow traffic from all counties except "x"

Avoid setting the rule action to `allow` and specifying a list of countries or regions to exclude when using geomatch custom rules. For example, if you want to allow traffic from all countries or regions except the United States, where you suspect malicious activity, this approach can have unintended consequences. It might allow traffic from unverified or unsafe countries/regions or countries/regions with low or no security standards, exposing your web application to potential vulnerabilities or attacks. Using the `allow` action for all countries or regions except the US indicates to the WAF to stop processing request payloads against managed rulesets. All rule evaluation ceases once the custom rule with `allow` is processed, exposing the application to unwanted malicious attacks.

Instead, use a more restrictive and specific rule action, such as block, and specify a list of countries or regions to allow with a negate condition. This ensures only traffic from trusted and verified sources can access your web application while blocking any suspicious or unwanted traffic.

## Related content

- [Geomatch custom rules](ag/geomatch-custom-rules.md)

- [Create and use Web Application Firewall v2 custom rules on Application Gateway](ag/create-custom-waf-rules.md)


# Application Gateway Waf Request Size Limits

# Web Application Firewall request and file upload size limits

**Applies to:** :heavy_check_mark: Application Gateway V2

Web Application Firewall allows you to configure request size limits within a lower and upper boundary. Application Gateways Web Application Firewalls running Core Rule Set 3.2 or later have more request and file upload size controls, including the ability to disable max size enforcement for requests and/or file uploads.

## Limits

The request body size field and the file upload size limit are both configurable within the Web Application Firewall. The maximum request body size field is specified in kilobytes and controls overall request size limit excluding any file uploads. The file upload limit field is specified in megabytes and it governs the maximum allowed file upload size. For the request size limits and file upload size limit, see [Application Gateway limits](../../azure-resource-manager/management/azure-subscription-service-limits.md#azure-application-gateway-limits).

For Application Gateway v2 Web Application Firewalls running Core Rule Set 3.2, or newer, the maximum request body size enforcement and max file upload size enforcement can be disabled and the Web Application Firewall no longer rejects a request, or file upload, for being too large. When maximum request body size enforcement and max file upload size enforcement are disabled within the Web Application Firewall, Application Gateway's limits determine the maximum size allowable. For more information, see [Application Gateway limits](../../azure-resource-manager/management/azure-subscription-service-limits.md#azure-application-gateway-limits).

Only requests with Content-Type of *multipart/form-data* are considered for file uploads. For content to be considered as a file upload, it has to be a part of a multipart form with a *filename* header. For all other content types, the request body size limit applies.

>[!NOTE]

>If you're running Core Rule Set 3.2 or later, and you have a high priority custom rule that takes action based on the content of a request's headers, cookies, or URI, this will take precedence over any max request size, or max file upload size, limits. This optimization lets the Web Application Firewall run high priority custom rules that don't require reading the full request first.

>

>**Example:** If you have a custom rule with priority 1 (the highest priority) set to allow a request with the header xyz, even if the request's size is larger than your maximum request size limit, it will get allowed before the max size limit is enforced

>[!NOTE]

>There's a 4 KB buffer on the file upload limit. The file size restriction won't be enforced until the file upload exceeds your set limit plus this buffer.

## Request body inspection

Web Application Firewall offers a configuration setting to enable or disable the request body inspection. By default, the request body inspection is enabled. If the request body inspection is disabled, Web Application Firewall doesn't evaluate the contents of an HTTP message's body. In such cases, Web Application Firewall continues to enforce Web Application Firewall rules on headers, cookies, and URI. In Web Application Firewalls running Core Rule Set 3.1 (or lower), if the request body inspection is turned off, then maximum request body size field isn't applicable and can't be set.

For Policy Web Application Firewalls running Core Rule Set 3.2 (or newer), request body inspection can be enabled/disabled independently of request body size enforcement and file upload size limits. Additionally, policy Web Application Firewalls running Core Rule Set 3.2 (or newer) can set the maximum request body inspection limit independently of the maximum request body size. The maximum request body inspection limit tells the Web Application Firewall how deep into a request it should inspect and apply rules; setting a lower value for this field can improve Web Application Firewall performance but might allow for uninspected malicious content to pass through your Web Application Firewall.

For older Web Application Firewalls running Core Rule Set 3.1 (or lower), turning off the request body inspection allows for messages larger than 128 KB to be sent to Web Application Firewall, but the message body isn't inspected for vulnerabilities. For Policy Web Application Firewalls running Core Rule Set 3.2 (or newer), you can achieve the same outcome by disabling maximum request body limit.

When your Web Application Firewall receives a request that's over the size limit, the behavior depends on the mode of your Web Application Firewall and the version of the managed ruleset you use.

- When your Web Application Firewall policy is in prevention mode, Web Application Firewall logs and blocks requests and file uploads that are over the size limits.

- When your Web Application Firewall policy is in detection mode, Web Application Firewall inspects the body up to the limit specified and ignores the rest. If the `Content-Length` header is present and is greater than the file upload limit, Web Application Firewall ignores the entire body and logs the request.

## Troubleshooting

If you're an Application Gateway v2 Web Application Firewall customer running Core Rule Set 3.2 or later and you have issues with requests, or file uploads, getting rejected incorrectly for maximum size, or if you see requests not getting inspected fully, you might need to verify that all values are set correctly. Using PowerShell or the Azure Command Line Interface you can verify what each value is set to, and update any values as needed.

**Enforce request body inspection**

- PowerShell: "RequestBodyCheck"

- CLI: "request_body_check"

- Controls if your Web Application Firewall inspects the request body and apply managed and custom rules to the request body traffic per your Web Application Firewall policy’s settings.

**Maximum request body inspection limit (KB)**

- PowerShell: "RequestBodyInspectLimitInKB"

- CLI: "request_body_inspect_limit_in_kb"

- Controls how deep into a request body the Web Application Firewall inspects and applies managed/custom rules. Generally speaking, you’d want to set this to the max possible setting, but some customers might want to set it to a lower value to improve performance.

**Enforce maximum request body limit**

- PowerShell: "RequestBodyEnforcement"

- CLI: "request_body_enforcement"

- Control if your Web Application Firewall enforces a max size limit on request bodies; when turned off it doesn't reject any requests for being too large.

**Maximum request body size (KB)**

- PowerShell: "MaxRequestBodySizeInKB"

- CLI: "max_request_body_size_in_kb"

- Controls how large a request body can be before the Web Application Firewall rejects it for exceeding the max size setting.

**Enforce maximum file upload limit**

- PowerShell: "FileUploadEnforcement"

- CLI: "file_upload_enforcement"

- Controls if your Web Application Firewall enforces a max size limit on file uploads; when turned off it doesn't reject any file uploads for being too large.

**Maximum file upload size (MB)**

- PowerShell: "FileUploadLimitInMB"

- CLI: file_upload_limit_in_mb

- Controls how large a file upload can be before the Web Application Firewall rejects it for exceeding the max size setting.

>[!NOTE]

>**"Inspect request body"** previously controlled if the request body was inspected and rules applied as well as if a maximum size limit was enforced on request bodies. Now this is handled by two separate fields that can be turned ON/OFF independently.

### PowerShell

You can use the following PowerShell commands to return your Azure policy and look at its current settings.

```azurepowershell-interactive

$plcy = Get-AzApplicationGatewayFirewallPolicy -Name <policy-name> -ResourceGroupName <resourcegroup-name>

$plcy.PolicySettings

```

You can use these commands to update the policy settings to the desired values for inspection limit and max size limitation related fields. You can swap out 'RequestBodyEnforcement' in the following example for one of the other values that you want to update.

```azurepowershell-interactive

$plcy = Get-AzApplicationGatewayFirewallPolicy -Name <policy-name> -ResourceGroupName <resourcegroup-name>

$plcy.PolicySettings.RequestBodyEnforcement=false

Set-AzApplicationGatewayFirewallPolicy -InputObject $plcy

```

- [Get Web Application Firewall Policy](/powershell/module/az.network/get-azapplicationgatewayfirewallpolicy)

- [Policy Settings Properties](/dotnet/api/microsoft.azure.commands.network.models.psapplicationgatewaywebapplicationfirewallpolicy.policysettings)

- [Policy Settings Class](/dotnet/api/microsoft.azure.commands.network.models.psapplicationgatewayfirewallpolicysettings)

- [New Policy Settings](/powershell/module/az.network/new-azapplicationgatewayfirewallpolicysetting)

### Command line interface

You can use Azure CLI to return the current values for these fields from your Azure policy settings and update the fields to the desired values using [these commands](/cli/azure/network/application-gateway/waf-policy/policy-setting).

```azurecli-interactive

az network application-gateway waf-policy update --name <WAF Policy name> --resource-group <WAF policy RG> --set policySettings.request_body_inspect_limit_in_kb='128' policySettings.max_request_body_size_in_kb='128' policySettings.file_upload_limit_in_mb='100' --query policySettings -o table

```

**Output:**

```azurecli-interactive

FileUploadEnforcement    FileUploadLimitInMb    MaxRequestBodySizeInKb    Mode       RequestBodyCheck    RequestBodyEnforcement    RequestBodyInspectLimitInKB    State

-----------------------  ---------------------  ------------------------  ---------  ------------------  ------------------------  -----------------------------  -------

True                     100                   128                      Detection  True                True                      128                           Enabled

```

## Next steps

- After you configure your Web Application Firewall settings, you can learn how to view your Web Application Firewall logs. For more information, see [Application Gateway diagnostics](../../application-gateway/application-gateway-diagnostics.md#diagnostic-logging).

- [Learn more about Azure network security](../../networking/security/index.yml)


# Configure Custom Response Code

# Configure custom response code and body for Azure Application Gateway WAF

By default, when Azure Web Application Firewall (WAF) on Azure Application Gateway blocks a request due to a matched rule, it returns a 403 status code with the message "The request is blocked." You can customize the response by configuring a custom status code and message to better suit your use case.

This article shows you how to configure a custom response page when Azure Application Gateway's Web Application Firewall (WAF) blocks a request using the Azure portal. You can also configure custom responses using the [Azure CLI](/cli/azure/network/application-gateway/waf-policy/policy-setting) or [PowerShell](/powershell/module/az.network/new-azapplicationgatewayfirewallpolicysetting).

> [!IMPORTANT]

> Custom response in Azure Application Gateway Web Application Firewall (WAF) is currently in PREVIEW.

> See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Configure a custom response status code and message

To customize the response status code and body, take the following steps:

1. Go to your Application Gateway WAF policy in the Azure portal.

1. Under **Settings**, select **Policy settings**.

1. Enter the custom response status code and response body in **Block response status code** and **Block response body** respectively.

1. Select **Save**.

In this example, we changed the default 403 response code to 429 and set a brief message stating, *The request has been blocked*.

## Limitations

The following limitations apply when configuring custom responses for Azure Application Gateway WAF:

- You can enable up to 20 WAF policies with custom block response status code and body within one Application Gateway.

- You can use one of the following custom status codes: 200, 403, 405, 406, 429, 990, 991, 992, 993, 994, 995, 996, 997, 998, 999.

- The maximum size for the custom block response body is 32KB.

- You must use base64 encoding for the custom block response body when you use Azure Resource Manager (ARM) API.

- Custom block response status code and body aren't supported on Application Gateway for Containers WAF.

## Related content

- [Azure Web Application Firewall policy](policy-overview.md)

- [Create Web Application Firewall policies for Application Gateway](create-waf-policy-ag.md)

- [Azure Web Application Firewall on Application Gateway](ag-overview.md)


# Waf Engine

# WAF engine on Azure Application Gateway

The Azure Web Application Firewall (WAF) engine inspects traffic, detects potential attacks based on request signatures, and takes appropriate action according to the configuration.

## Next generation of WAF engine

The new WAF engine is a high-performance, scalable Microsoft proprietary engine and has significant improvements over the previous WAF engine.

The new engine, released with CRS 3.2, provides the following benefits:

* **Improved performance:** Significant improvements in WAF latency, including P99 POST and GET latencies. We observed a significant reduction in P99 tail latencies with up to approximately 8x reduction in processing POST requests and approximately 4x reduction in processing GET requests.

* **Increased scale:** Higher requests per second (RPS), using the same compute power and with the ability to process larger request sizes. Our next-generation engine can scale up to eight times more RPS using the same compute power, and has an ability to process 16 times larger request sizes (up to 2-MB request sizes), which wasn't possible with the previous engine.

* **Better protection:** New redesigned engine with efficient regex processing offers better protection against RegEx denial of service (DOS) attacks while maintaining a consistent latency experience.

* **Richer feature set:** New features and future enhancement are available only through the new engine.

## Support for new features

There are many new features that are only supported in the Azure WAF engine. The features include:

* [CRS 3.2](application-gateway-crs-rulegroups-rules.md#core-rule-sets-crs---legacy)

* Increased request body size limit to 2 MB

* Increased file upload limit to 4 GB

* [DRS 2.1](application-gateway-crs-rulegroups-rules.md#default-rule-set-21) and later DRS versions

* [WAF v2 metrics](application-gateway-waf-metrics.md#application-gateway-waf-v2-metrics)

* [Per rule exclusions](application-gateway-waf-configuration.md#per-rule-exclusions) and support for [exclusion attributes by name](application-gateway-waf-configuration.md#request-attributes-by-keys-and-values).

* [Increased scale limits](../../azure-resource-manager/management/azure-subscription-service-limits.md#azure-application-gateway-limits)

* HTTP listeners limit

* WAF IP address ranges per match condition

* Exclusions limit

* [Rate-limit Custom Rules](rate-limiting-overview.md)

* [Inspection Limit & Max Size Enforcement](application-gateway-waf-request-size-limits.md) can be turned on/off independently of each other and the values for each field can be set independently

New WAF features are only released with later versions of CRS on the new WAF engine.

## Request logging for custom rules

There's a difference between how the previous engine and the new WAF engine log requests when a custom rule defines the action type as *Log*.

When your WAF runs in prevention mode, the previous engine logs the request's action type as *Blocked* even though the request is allowed through by the custom rule. In detection mode, the previous engine logs the same request's action type as *Detected*.

In contrast, the new WAF engine logs the request action type as *Log*, whether the WAF is running in prevention or detection mode.

## Next step

> [!div class="nextstepaction"]

> [WAF managed rules](application-gateway-crs-rulegroups-rules.md)


# Waf Front Door Policy Settings

# Policy settings for Web Application Firewall in Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Premium

A web application firewall (WAF) policy allows you to control access to your web applications by a set of custom and managed rules. The WAF policy name must be unique. You receive a validation error if you try to use an existing name. Multiple policy-level settings apply to all rules specified for that policy as described in this article.

## WAF state

A WAF policy for Azure Front Door has one of the following two states:

- **Enabled:** When a policy is enabled, WAF actively inspects incoming requests and takes corresponding actions according to rule definitions.

- **Disabled:** When a policy is disabled, WAF inspection is paused. Incoming requests bypass WAF and are sent to back ends based on Azure Front Door routing.

## WAF mode

You can configure a WAF policy to run in the following two modes:

- **Detection mode**: When run in detection mode, the WAF doesn't take any actions other than to monitor and log the request and its matched WAF rule to WAF logs. Turn on logging diagnostics for Azure Front Door when you use the Azure portal. (Go to the **Diagnostics** section in the Azure portal.)

- **Prevention mode**: When a WAF is configured to run in prevention mode, the WAF takes the specified action if a request matches a rule. Any matched requests are also logged in the WAF logs.

## WAF response for blocked requests

By default, when the WAF blocks a request because of a matched rule, it returns a 403 status code with the message "The request is blocked." A reference string is also returned for logging.

You can define a custom response status code and response message when the WAF blocks a request. The following custom status codes are supported:

- 200    OK

- 403    Forbidden

- 405    Method not allowed

- 406    Not acceptable

- 429    Too many requests

A custom response status code with a response message is a policy-level setting. After it's configured, all blocked requests get the same custom response status and response message.

## URI for redirect action

You're required to define a URI to redirect requests to if the `REDIRECT` action is selected for any of the rules contained in a WAF policy. This redirect URI needs to be a valid HTTP(S) site. After it's configured, all requests matching rules with a `REDIRECT` action are redirected to the specified site.

## Next steps

Learn how to define WAF [custom responses](waf-front-door-configure-custom-response-code.md).


# Waf Front Door Drs

# Web Application Firewall DRS rule groups and rules

**Applies to:** :heavy_check_mark: Front Door Premium :heavy_check_mark: Front Door (classic)

Azure Web Application Firewall on Azure Front Door protects web applications from common vulnerabilities and exploits. Azure-managed rule sets provide an easy way to deploy protection against a common set of security threats. Because Azure manages these rule sets, the rules are updated as needed to protect against new attack signatures.

The Default Rule Set (DRS) also includes the Microsoft Threat Intelligence Collection rules that are written in partnership with the Microsoft Intelligence team to provide increased coverage, patches for specific vulnerabilities, and better false positive reduction.

> [!NOTE]

> When a ruleset version is changed in a WAF Policy, any existing customizations you made to your ruleset will be reset to the defaults for the new ruleset. See: [Upgrading or changing ruleset version](#upgrading-or-changing-ruleset-version).

## Default rule sets

The Azure-managed DRS includes rules against the following threat categories:

- Cross-site scripting

- Java attacks

- Local file inclusion

- PHP injection attacks

- Remote command execution

- Remote file inclusion

- Session fixation

- SQL injection protection

- Protocol attackers

The version number of the DRS increments when new attack signatures are added to the rule set.

DRS is enabled by default in Detection mode in your WAF policies. You can disable or enable individual rules within the DRS to meet your application requirements. You can also set specific actions per rule. The available actions are [Allow, Block, Log, and Redirect](afds-overview.md#waf-actions).

Sometimes you might need to omit certain request attributes from a web application firewall (WAF) evaluation. A common example is Active Directory-inserted tokens that are used for authentication. You might configure an exclusion list for a managed rule, a rule group, or the entire rule set. For more information, see [Azure Web Application Firewall on Azure Front Door exclusion lists](./waf-front-door-exclusion.md).

By default, DRS versions 2.0 and above use anomaly scoring when a request matches a rule. DRS versions earlier than 2.0 block requests that trigger the rules. Also, custom rules can be configured in the same WAF policy if you want to bypass any of the preconfigured rules in the DRS.

Custom rules are always applied before rules in the DRS are evaluated. If a request matches a custom rule, the corresponding rule action is applied. The request is either blocked or passed through to the back end. No other custom rules or the rules in the DRS are processed. You can also remove the DRS from your WAF policies.

### Microsoft Threat Intelligence Collection rules

The Microsoft Threat Intelligence Collection rules are written in partnership with the Microsoft Threat Intelligence team to provide increased coverage, patches for specific vulnerabilities, and better false positive reduction.

By default, the Microsoft Threat Intelligence Collection rules replace some of the built-in DRS rules, causing them to be disabled. For example, rule ID 942440, *SQL Comment Sequence Detected*, has been disabled and replaced by the Microsoft Threat Intelligence Collection rule 99031002. The replaced rule reduces the risk of false positive detections from legitimate requests.

### <a name="anomaly-scoring-mode"></a>Anomaly scoring

When you use DRS 2.0 or later, your WAF uses *anomaly scoring*. Traffic that matches any rule isn't immediately blocked, even when your WAF is in prevention mode. Instead, the OWASP rule sets define a severity for each rule: *Critical*, *Error*, *Warning*, or *Notice*. The severity affects a numeric value for the request, which is called the *anomaly score*. If a request accumulates an anomaly score of 5 or greater, the WAF takes action on the request.

| Rule severity | Value contributed to anomaly score |

|-|-|

| Critical | 5 |

| Error | 4 |

| Warning | 3 |

| Notice | 2 |

When you configure your WAF, you can decide how the WAF handles requests that exceed the anomaly score threshold of 5. The three anomaly score action options are Block, Log, or Redirect. The anomaly score action you select at the time of configuration is applied to all requests that exceed the anomaly score threshold.

For example, if the anomaly score is 5 or greater on a request, and the WAF is in Prevention mode with the anomaly score action set to Block, the request is blocked. If the anomaly score is 5 or greater on a request, and the WAF is in Detection mode, the request is logged but not blocked.

A single *Critical* rule match is enough for the WAF to block a request when in Prevention mode with the anomaly score action set to Block because the overall anomaly score is 5. However, one *Warning* rule match only increases the anomaly score by 3, which isn't enough by itself to block the traffic. When an anomaly rule is triggered, it shows a "matched" action in the logs. If the anomaly score is 5 or greater, there a separate rule is triggered with the anomaly score action configured for the rule set. Default anomaly score action is Block, which results in a log entry with the action `blocked`.

When your WAF uses an older version of the Default Rule Set (before DRS 2.0), your WAF runs in the traditional mode. Traffic that matches any rule is considered independently of any other rule matches. In traditional mode, you don't have visibility into the complete set of rules that a specific request matched.

The version of the DRS that you use also determines which content types are supported for request body inspection. For more information, see [What content types does WAF support](waf-faq.yml#what-content-types-does-the-waf-support-) in the FAQ.

## Paranoia level

Each rule is assigned in a specific Paranoia Level (PL). Rules configured in Paranoia Level 1 (PL1) are less aggressive and hardly ever trigger a false positive. They provide baseline security with minimal need for fine tuning. Rules in PL2 detect more attacks, but they're expected to trigger false positives, which should be fine-tuned.

By default, DRS 2.2 is configured at Paranoia Level 1 (PL1), and all PL2 rules are disabled. To run WAF at PL2, you can manually enable any or all PL2 rules.

For earlier rule sets, DRS 2.1 and CRS 3.2 include rules defined for Paranoia Level 2, which covers both PL1 and PL2 rules. If you prefer to operate strictly at PL1, you can disable specific PL2 rules or set their action to Log.

Paranoia Levels 3 and 4 aren't currently supported in Azure WAF.

### Upgrading or changing ruleset version

If you're upgrading, or assigning a new ruleset version, and would like to preserve existing rule overrides and exclusions, it's recommended to use PowerShell, CLI, REST API, or a template to make ruleset version changes. A new version of a ruleset can have newer rules, additional rule groups, and may have updates to existing signatures to enforce better security and reduce false positives. It's recommended to validate changes in a test environment, fine tune if necessary, and then deploy in a production environment.

> [!NOTE]

> If you're using the Azure portal to assign a new managed ruleset to a WAF policy, all the previous customizations from the existing managed ruleset such as rule state, rule actions, and rule level exclusions will be reset to the new managed ruleset's defaults. However, any custom rules, or policy settings will remain unaffected during the new ruleset assignment. You need to redefine rule overrides and validate changes before deploying in a production environment.

### DRS 2.2

DRS 2.2 rules offer better protection than earlier versions of the DRS. It includes other rules developed by the Microsoft Threat Intelligence team and updates to signatures to reduce false positives. It also supports transformations beyond just URL decoding.

DRS 2.2 includes 18 rule groups, as shown in the following table. Each group contains multiple rules, and you can customize behavior for individual rules, rule groups, or an entire rule set. DRS 2.2 is baselined off the Open Web Application Security Project (OWASP) Core Rule Set (CRS) 3.3.4 and includes additional proprietary protections rules developed by Microsoft Threat Intelligence team.

#### Disabled rules

DRS 2.2 rules configured in Paranoia Level 2 are disabled by default. You can leave their state as disabled if you wish to keep your WAF policy configured in Paranoia Level 1. If you wish to increase the policy's paranoia level, you can safely change these rules' state to enabled and their action to log mode. Analyze the log, make the required fine tuning and enable the rules accordingly. For more information, see [Tuning Web Application Firewall (WAF) for Azure Front Door](waf-front-door-tuning.md) and [Paranoia level](#paranoia-level).

Some OWASP rules are superseded by Microsoft-authored replacements. The original rules are disabled by default and their descriptions end with "(replaced by …)".

|Rule group|ruleGroupName|Description|

|---|---|---|

|[General](?tabs=drs22#general-22)|General|General group|

|[METHOD-ENFORCEMENT](?tabs=drs22#drs911-22)|METHOD-ENFORCEMENT|Lock-down methods (PUT, PATCH)|

|[PROTOCOL-ENFORCEMENT](?tabs=drs22#drs920-22)|PROTOCOL-ENFORCEMENT|Protect against protocol and encoding issues|

|[PROTOCOL-ATTACK](?tabs=drs22#drs921-22)|PROTOCOL-ATTACK|Protect against header injection, request smuggling, and response splitting|

|[APPLICATION-ATTACK-LFI](?tabs=drs22#drs930-22)|LFI|Protect against file and path attacks|

|[APPLICATION-ATTACK-RFI](?tabs=drs22#drs931-22)|RFI|Protect against remote file inclusion (RFI) attacks|

|[APPLICATION-ATTACK-RCE](?tabs=drs22#drs932-22)|RCE|Protect again remote code execution attacks|

|[APPLICATION-ATTACK-PHP](?tabs=drs22#drs933-22)|PHP|Protect against PHP-injection attacks|

|[APPLICATION-ATTACK-NodeJS](?tabs=drs22#drs934-22)|NODEJS|Protect against Node JS attacks|

|[APPLICATION-ATTACK-XSS](?tabs=drs22#drs941-22)|XSS|Protect against cross-site scripting attacks|

|[APPLICATION-ATTACK-SQLI](?tabs=drs22#drs942-22)|SQLI|Protect against SQL-injection attacks|

|[APPLICATION-ATTACK-SESSION-FIXATION](?tabs=drs22#drs943-22)|FIX|Protect against session-fixation attacks|

|[APPLICATION-ATTACK-SESSION-JAVA](?tabs=drs22#drs944-22)|JAVA|Protect against JAVA attacks|

|[MS-ThreatIntel-WebShells](?tabs=drs22#drs9905-22)|MS-ThreatIntel-WebShells|Protect against Web shell attacks|

|[MS-ThreatIntel-AppSec](?tabs=drs22#drs9903-22)|MS-ThreatIntel-AppSec|Protect against AppSec attacks|

|[MS-ThreatIntel-SQLI](?tabs=drs22#drs99031-22)|MS-ThreatIntel-SQLI|Protect against SQLI attacks|

|[MS-ThreatIntel-CVEs](?tabs=drs22#drs99001-22)|MS-ThreatIntel-CVEs|Protect against CVE attacks|

|[MS-ThreatIntel-XSS](?tabs=drs22#drs99032-22)|MS-ThreatIntel-XSS|Protect against XSS attacks|

### DRS 2.1

DRS 2.1 rules offer better protection than earlier versions of the DRS. It includes other rules developed by the Microsoft Threat Intelligence team and updates to signatures to reduce false positives. It also supports transformations beyond just URL decoding.

DRS 2.1 includes 17 rule groups, as shown in the following table. Each group contains multiple rules, and you can customize behavior for individual rules, rule groups, or an entire rule set. DRS 2.1 is baselined off the Open Web Application Security Project (OWASP) Core Rule Set (CRS) 3.3.2 and includes additional proprietary protections rules developed by Microsoft Threat Intelligence team.

For more information, see [Tuning Web Application Firewall (WAF) for Azure Front Door](waf-front-door-tuning.md).

> [!NOTE]

> DRS 2.1 is only available on Azure Front Door Premium.

|Rule group|ruleGroupName|Description|

|---|---|---|

|[General](?tabs=drs21#general-21)|General|General group|

|[METHOD-ENFORCEMENT](?tabs=drs21#drs911-21)|METHOD-ENFORCEMENT|Lock-down methods (PUT, PATCH)|

|[PROTOCOL-ENFORCEMENT](?tabs=drs21#drs920-21)|PROTOCOL-ENFORCEMENT|Protect against protocol and encoding issues|

|[PROTOCOL-ATTACK](?tabs=drs21#drs921-21)|PROTOCOL-ATTACK|Protect against header injection, request smuggling, and response splitting|

|[APPLICATION-ATTACK-LFI](?tabs=drs21#drs930-21)|LFI|Protect against file and path attacks|

|[APPLICATION-ATTACK-RFI](?tabs=drs21#drs931-21)|RFI|Protect against remote file inclusion (RFI) attacks|

|[APPLICATION-ATTACK-RCE](?tabs=drs21#drs932-21)|RCE|Protect again remote code execution attacks|

|[APPLICATION-ATTACK-PHP](?tabs=drs21#drs933-21)|PHP|Protect against PHP-injection attacks|

|[APPLICATION-ATTACK-NodeJS](?tabs=drs21#drs934-21)|NODEJS|Protect against Node JS attacks|

|[APPLICATION-ATTACK-XSS](?tabs=drs21#drs941-21)|XSS|Protect against cross-site scripting attacks|

|[APPLICATION-ATTACK-SQLI](?tabs=drs21#drs942-21)|SQLI|Protect against SQL-injection attacks|

|[APPLICATION-ATTACK-SESSION-FIXATION](?tabs=drs21#drs943-21)|FIX|Protect against session-fixation attacks|

|[APPLICATION-ATTACK-SESSION-JAVA](?tabs=drs21#drs944-21)|JAVA|Protect against JAVA attacks|

|[MS-ThreatIntel-WebShells](?tabs=drs21#drs9905-21)|MS-ThreatIntel-WebShells|Protect against Web shell attacks|

|[MS-ThreatIntel-AppSec](?tabs=drs21#drs9903-21)|MS-ThreatIntel-AppSec|Protect against AppSec attacks|

|[MS-ThreatIntel-SQLI](?tabs=drs21#drs99031-21)|MS-ThreatIntel-SQLI|Protect against SQLI attacks|

|[MS-ThreatIntel-CVEs](?tabs=drs21#drs99001-21)|MS-ThreatIntel-CVEs|Protect against CVE attacks|

#### Disabled rules

The following rules are disabled by default for DRS 2.1.

|Rule ID  |Rule group|Description  |Details|

|---------|---------|---------|---------|

|942110      |SQLI|SQL Injection Attack: Common Injection Testing Detected |Replaced by MSTIC rule 99031001 |

|942150      |SQLI|SQL Injection Attack|Replaced by MSTIC rule 99031003 |

|942260      |SQLI|Detects basic SQL authentication bypass attempts 2/3 |Replaced by MSTIC rule 99031004 |

|942430      |SQLI|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12)|Too many false positives|

|942440      |SQLI|SQL Comment Sequence Detected|Replaced by MSTIC rule 99031002 |

|99005006|MS-ThreatIntel-WebShells|Spring4Shell Interaction Attempt|Enable rule to prevent against SpringShell vulnerability|

|99001014|MS-ThreatIntel-CVEs|Attempted Spring Cloud routing-expression injection [CVE-2022-22963](https://www.cve.org/CVERecord?id=CVE-2022-22963)|Enable rule to prevent against SpringShell vulnerability|

|99001015|MS-ThreatIntel-WebShells|Attempted Spring Framework unsafe class object exploitation [CVE-2022-22965](https://www.cve.org/CVERecord?id=CVE-2022-22965)|Enable rule to prevent against SpringShell vulnerability|

|99001016|MS-ThreatIntel-WebShells|Attempted Spring Cloud Gateway Actuator injection [CVE-2022-22947](https://www.cve.org/CVERecord?id=CVE-2022-22947)|Enable rule to prevent against SpringShell vulnerability|

|99001017|MS-ThreatIntel-CVEs|Attempted Apache Struts file upload exploitation [CVE-2023-50164](https://www.cve.org/CVERecord?id=CVE-2023-50164)|Enable rule to prevent against Apache Struts vulnerability|

### DRS 2.0

DRS 2.0 rules offer better protection than earlier versions of the DRS. DRS 2.0 also supports transformations beyond just URL decoding.

DRS 2.0 includes 17 rule groups, as shown in the following table. Each group contains multiple rules. You can disable individual rules and entire rule groups.

> [!NOTE]

> DRS 2.0 is only available on Azure Front Door Premium.

|Rule group|ruleGroupName|Description|

|---|---|---|

|[General](?tabs=drs20#general-20)|General|General group|

|[METHOD-ENFORCEMENT](?tabs=drs20#drs911-20)|METHOD-ENFORCEMENT|Lock-down methods (PUT, PATCH)|

|[PROTOCOL-ENFORCEMENT](?tabs=drs20#drs920-20)|PROTOCOL-ENFORCEMENT|Protect against protocol and encoding issues|

|[PROTOCOL-ATTACK](?tabs=drs20#drs921-20)|PROTOCOL-ATTACK|Protect against header injection, request smuggling, and response splitting|

|[APPLICATION-ATTACK-LFI](?tabs=drs20#drs930-20)|LFI|Protect against file and path attacks|

|[APPLICATION-ATTACK-RFI](?tabs=drs20#drs931-20)|RFI|Protect against remote file inclusion (RFI) attacks|

|[APPLICATION-ATTACK-RCE](?tabs=drs20#drs932-20)|RCE|Protect again remote code execution attacks|

|[APPLICATION-ATTACK-PHP](?tabs=drs20#drs933-20)|PHP|Protect against PHP-injection attacks|

|[APPLICATION-ATTACK-NodeJS](?tabs=drs20#drs934-20)|NODEJS|Protect against Node JS attacks|

|[APPLICATION-ATTACK-XSS](?tabs=drs20#drs941-20)|XSS|Protect against cross-site scripting attacks|

|[APPLICATION-ATTACK-SQLI](?tabs=drs20#drs942-20)|SQLI|Protect against SQL-injection attacks|

|[APPLICATION-ATTACK-SESSION-FIXATION](?tabs=drs20#drs943-20)|FIX|Protect against session-fixation attacks|

|[APPLICATION-ATTACK-SESSION-JAVA](?tabs=drs20#drs944-20)|JAVA|Protect against JAVA attacks|

|[MS-ThreatIntel-WebShells](?tabs=drs20#drs9905-20)|MS-ThreatIntel-WebShells|Protect against Web shell attacks|

|[MS-ThreatIntel-AppSec](?tabs=drs20#drs9903-20)|MS-ThreatIntel-AppSec|Protect against AppSec attacks|

|[MS-ThreatIntel-SQLI](?tabs=drs20#drs99031-20)|MS-ThreatIntel-SQLI|Protect against SQLI attacks|

|[MS-ThreatIntel-CVEs](?tabs=drs20#drs99001-20)|MS-ThreatIntel-CVEs|Protect against CVE attacks|

### DRS 1.1

|Rule group|ruleGroupName|Description|

|---|---|---|

|[PROTOCOL-ATTACK](?tabs=drs11#drs921-11)|PROTOCOL-ATTACK|Protect against header injection, request smuggling, and response splitting|

|[APPLICATION-ATTACK-LFI](?tabs=drs11#drs930-11)|LFI|Protect against file and path attacks|

|[APPLICATION-ATTACK-RFI](?tabs=drs11#drs931-11)|RFI|Protection against remote file inclusion attacks|

|[APPLICATION-ATTACK-RCE](?tabs=drs11#drs932-11)|RCE|Protection against remote command execution|

|[APPLICATION-ATTACK-PHP](?tabs=drs11#drs933-11)|PHP|Protect against PHP-injection attacks|

|[APPLICATION-ATTACK-XSS](?tabs=drs11#drs941-11)|XSS|Protect against cross-site scripting attacks|

|[APPLICATION-ATTACK-SQLI](?tabs=drs11#drs942-11)|SQLI|Protect against SQL-injection attacks|

|[APPLICATION-ATTACK-SESSION-FIXATION](?tabs=drs11#drs943-11)|FIX|Protect against session-fixation attacks|

|[APPLICATION-ATTACK-SESSION-JAVA](?tabs=drs11#drs944-11)|JAVA|Protect against JAVA attacks|

|[MS-ThreatIntel-WebShells](?tabs=drs11#drs9905-11)|MS-ThreatIntel-WebShells|Protect against Web shell attacks|

|[MS-ThreatIntel-AppSec](?tabs=drs11#drs9903-11)|MS-ThreatIntel-AppSec|Protect against AppSec attacks|

|[MS-ThreatIntel-SQLI](?tabs=drs11#drs99031-11)|MS-ThreatIntel-SQLI|Protect against SQLI attacks|

|[MS-ThreatIntel-CVEs](?tabs=drs11#drs99001-11)|MS-ThreatIntel-CVEs|Protect against CVE attacks|

### DRS 1.0

|Rule group|ruleGroupName|Description|

|---|---|---|

|[PROTOCOL-ATTACK](?tabs=drs10#drs921-10)|PROTOCOL-ATTACK|Protect against header injection, request smuggling, and response splitting|

|[APPLICATION-ATTACK-LFI](?tabs=drs10#drs930-10)|LFI|Protect against file and path attacks|

|[APPLICATION-ATTACK-RFI](?tabs=drs10#drs931-10)|RFI|Protection against remote file inclusion attacks|

|[APPLICATION-ATTACK-RCE](?tabs=drs10#drs932-10)|RCE|Protection against remote command execution|

|[APPLICATION-ATTACK-PHP](?tabs=drs10#drs933-10)|PHP|Protect against PHP-injection attacks|

|[APPLICATION-ATTACK-XSS](?tabs=drs10#drs941-10)|XSS|Protect against cross-site scripting attacks|

|[APPLICATION-ATTACK-SQLI](?tabs=drs10#drs942-10)|SQLI|Protect against SQL-injection attacks|

|[APPLICATION-ATTACK-SESSION-FIXATION](?tabs=drs10#drs943-10)|FIX|Protect against session-fixation attacks|

|[APPLICATION-ATTACK-SESSION-JAVA](?tabs=drs10#drs944-10)|JAVA|Protect against JAVA attacks|

|[MS-ThreatIntel-WebShells](?tabs=drs10#drs9905-10)|MS-ThreatIntel-WebShells|Protect against Web shell attacks|

|[MS-ThreatIntel-CVEs](?tabs=drs10#drs99001-10)|MS-ThreatIntel-CVEs|Protect against CVE attacks|

### Bot Manager 1.0

The Bot Manager 1.0 rule set provides protection against malicious bots and detection of good bots. The rules provide granular control over bots detected by WAF by categorizing bot traffic as Good, Bad, or Unknown bots.

|Rule group|Description|

|---|---|

|[BadBots](?tabs=bot#bot100)|Protect against bad bots|

|[GoodBots](?tabs=bot#bot200)|Identify good bots|

|[UnknownBots](?tabs=bot#bot300)|Identify unknown bots|

### Bot Manager 1.1

The Bot Manager 1.1 rule set is an enhancement to Bot Manager 1.0 rule set. It provides enhanced protection against malicious bots, and increases good bot detection.

|Rule group|Description|

|---|---|

|[BadBots](?tabs=bot11#bot11-100)|Protect against bad bots|

|[GoodBots](?tabs=bot11#bot11-200)|Identify good bots|

|[UnknownBots](?tabs=bot11#bot11-300)|Identify unknown bots|

The following rule groups and rules are available when you use Azure Web Application Firewall on Azure Front Door.

# [DRS 2.2](#tab/drs22)

## <a name="drs22"></a> 2.2 rule sets

### <a name="general-22"></a> General

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|200002|Critical - 5|1|Failed to parse request body.|

|200003|Critical - 5|1|Multipart request body failed strict validation|

### <a name="drs911-22"></a> Method enforcement

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|911100|Critical - 5|1|Method isn't allowed by policy|

### <a name="drs920-22"></a> Protocol enforcement

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|920100|Notice - 2|1|Invalid HTTP Request Line|

|920120|Critical - 5|1|Attempted multipart/form-data bypass|

|920121|Critical - 5|2|Attempted multipart/form-data bypass|

|920160|Critical - 5|1|Content-Length HTTP header isn't numeric.|

|920170|Critical - 5|1|GET or HEAD Request with Body Content.|

|920171|Critical - 5|1|GET or HEAD Request with Transfer-Encoding.|

|920180|Notice - 2|1|POST without Content-Length or Transfer-Encoding headers.|

|920181|Warning - 3|1|Content-Length and Transfer-Encoding headers present|

|920190|Warning - 3|1|Range: Invalid Last Byte Value.|

|920200|Warning - 3|2|Range: Too many fields (6 or more)|

|920201|Warning - 3|2|Range: Too many fields for pdf request (63 or more)|

|920210|Warning - 3|1|Multiple/Conflicting Connection Header Data Found.|

|920220|Warning - 3|1|URL Encoding Abuse Attack Attempt|

|920230|Warning - 3|2|Multiple URL Encoding Detected|

|920240|Warning - 3|1|URL Encoding Abuse Attack Attempt|

|920260|Warning - 3|1|Unicode Full/Half Width Abuse Attack Attempt|

|920270|Critical - 5|1|Invalid character in request (null character)|

|920271|Critical - 5|2|Invalid character in request (non printable characters)|

|920280|Warning - 3|1|Request Missing a Host Header|

|920290|Warning - 3|1|Empty Host Header|

|920300|Notice - 2|2|Request Missing an Accept Header|

|920310|Notice - 2|1|Request Has an Empty Accept Header|

|920311|Notice - 2|1|Request Has an Empty Accept Header|

|920320|Notice - 2|2|Missing User Agent Header|

|920330|Notice - 2|1|Empty User Agent Header|

|920340|Notice - 2|1|Request Containing Content, but Missing Content-Type header|

|920341|Critical - 5|2|Request Containing Content Requires Content-Type header|

|920350|Warning - 3|1|Host header is a numeric IP address|

|920420|Critical - 5|2|Request content type is not allowed by policy|

|920430|Critical - 5|1|HTTP protocol version is not allowed by policy|

|920440|Critical - 5|1|URL file extension is restricted by policy|

|920450|Critical - 5|1|HTTP header is restricted by policy|

|920470|Critical - 5|1|Illegal Content-Type header|

|920480|Critical - 5|1|Request content type charset is not allowed by policy|

|920500|Critical - 5|1|Attempt to access a backup or working file|

|920530|Critical - 5|1|Restrict charset parameter inside content type header to occur max once|

|920620|Critical - 5|1|Multiple Content-Type Request Headers|

### <a name="drs921-22"></a> Protocol attack

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|921110|Critical - 5|1|HTTP Request Smuggling Attack|

|921120|Critical - 5|1|HTTP Response Splitting Attack|

|921130|Critical - 5|1|HTTP Response Splitting Attack|

|921140|Critical - 5|1|HTTP Header Injection Attack via headers|

|921150|Critical - 5|1|HTTP Header Injection Attack via payload (CR/LF detected)|

|921151|Critical - 5|2|HTTP Header Injection Attack via payload (CR/LF detected)|

|921160|Critical - 5|1|HTTP Header Injection Attack via payload (CR/LF and header-name detected)|

|921190|Critical - 5|1|HTTP Splitting (CR/LF in request filename detected)|

|921200|Critical - 5|1|LDAP Injection Attack|

|921422|Critical - 5|2|Detect content types in the Content-Type header outside of the actual content type declaration|

### <a name="drs930-22"></a> LFI: Local file inclusion

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|930100|Critical - 5|1|Path Traversal Attack (/../)|

|930110|Critical - 5|1|Path Traversal Attack (/../)|

|930120|Critical - 5|1|OS File Access Attempt|

|930130|Critical - 5|1|Restricted File Access Attempt|

### <a name="drs931-22"></a> RFI: Remote file inclusion

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|931100|Critical - 5|2|Possible Remote File Inclusion (RFI) Attack: URL Parameter using IP Address|

|931110|Critical - 5|1|Possible Remote File Inclusion (RFI) Attack: Common RFI Vulnerable Parameter Name used w/URL Payload|

|931120|Critical - 5|1|Possible Remote File Inclusion (RFI) Attack: URL Payload Used w/Trailing Question Mark Character (?)|

|931130|Critical - 5|2|Possible Remote File Inclusion (RFI) Attack: Off-Domain Reference/Link|

### <a name="drs932-22"></a> RCE: Remote command execution

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|932100|Critical - 5|1|Remote Command Execution: Unix Command Injection|

|932105|Critical - 5|1|Remote Command Execution: Unix Command Injection|

|932110|Critical - 5|1|Remote Command Execution: Windows Command Injection|

|932115|Critical - 5|1|Remote Command Execution: Windows Command Injection|

|932120|Critical - 5|1|Remote Command Execution: Windows PowerShell Command Found|

|932130|Critical - 5|1|Remote Command Execution: Unix Shell Expression or Confluence Vulnerability (CVE-2022-26134) Found|

|932140|Critical - 5|1|Remote Command Execution: Windows FOR/IF Command Found|

|932150|Critical - 5|1|Remote Command Execution: Direct Unix Command Execution|

|932160|Critical - 5|1|Remote Command Execution: Unix Shell Code Found|

|932170|Critical - 5|1|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932171|Critical - 5|1|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932180|Critical - 5|1|Restricted File Upload Attempt|

### <a name="drs933-22"></a> PHP attacks

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|933100|Critical - 5|1|PHP Injection Attack: PHP Open Tag Found|

|933110|Critical - 5|1|PHP Injection Attack: PHP Script File Upload Found|

|933120|Critical - 5|1|PHP Injection Attack: Configuration Directive Found|

|933130|Critical - 5|1|PHP Injection Attack: Variables Found|

|933140|Critical - 5|1|PHP Injection Attack: I/O Stream Found|

|933150|Critical - 5|1|PHP Injection Attack: High-Risk PHP Function Name Found|

|933151|Critical - 5|2|PHP Injection Attack: Medium-Risk PHP Function Name Found|

|933160|Critical - 5|1|PHP Injection Attack: High-Risk PHP Function Call Found|

|933170|Critical - 5|1|PHP Injection Attack: Serialized Object Injection|

|933180|Critical - 5|1|PHP Injection Attack: Variable Function Call Found|

|933200|Critical - 5|1|PHP Injection Attack: Wrapper scheme detected|

|933210|Critical - 5|1|PHP Injection Attack: Variable Function Call Found|

### <a name="drs934-22"></a> Node JS attacks

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|934100|Critical - 5|1|Node.js Injection Attack|

### <a name="drs941-22"></a> XSS: Cross-site scripting

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|941100|Critical - 5|1|XSS Attack Detected via libinjection|

|941101|Critical - 5|2|XSS Attack Detected via libinjection|

|941110|Critical - 5|1|XSS Filter - Category 1: Script Tag Vector|

|941120|Critical - 5|2|XSS Filter - Category 2: Event Handler Vector|

|941130|Critical - 5|1|XSS Filter - Category 3: Attribute Vector|

|941140|Critical - 5|1|XSS Filter - Category 4: Javascript URI Vector|

|941150|Critical - 5|2|XSS Filter - Category 5: Disallowed HTML Attributes|

|941160|Critical - 5|1|NoScript XSS InjectionChecker: HTML Injection|

|941170|Critical - 5|1|NoScript XSS InjectionChecker: Attribute Injection|

|941180|Critical - 5|1|Node-Validator Blacklist Keywords|

|941190|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941200|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941210|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941220|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941230|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941240|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941250|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941260|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941270|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941280|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941290|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941300|Critical - 5|1|IE XSS Filters - Attack Detected.|

|941310|Critical - 5|1|US-ASCII Malformed Encoding XSS Filter - Attack Detected.|

|941320|Critical - 5|2|Possible XSS Attack Detected - HTML Tag Handler|

|941330|Critical - 5|2|IE XSS Filters - Attack Detected.|

|941340|Critical - 5|2|IE XSS Filters - Attack Detected.|

|941350|Critical - 5|1|UTF-7 Encoding IE XSS - Attack Detected.|

|941360|Critical - 5|1|JSFuck / Hieroglyphy obfuscation detected|

|941370|Critical - 5|1|JavaScript global variable found|

|941380|Critical - 5|2|AngularJS client side template injection detected|

### <a name="drs942-22"></a> SQLI: SQL injection

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|942100|Critical - 5|1|SQL Injection Attack Detected via libinjection|

|942110|Warning - 3|2|SQL Injection Attack: Common Injection Testing Detected|

|942120|Critical - 5|2|SQL Injection Attack: SQL Operator Detected|

|942140|Critical - 5|1|SQL Injection Attack: Common DB Names Detected|

|942150|Critical - 5|2|SQL Injection Attack (replaced by rule #99031003)|

|942160|Critical - 5|1|Detects blind sqli tests using sleep() or benchmark().|

|942170|Critical - 5|1|Detects SQL benchmark and sleep injection attempts including conditional queries|

|942180|Critical - 5|2|Detects basic SQL authentication bypass attempts 1/3|

|942190|Critical - 5|1|Detects MSSQL code execution and information gathering attempts|

|942200|Critical - 5|2|Detects MySQL comment-/space-obfuscated injections and backtick termination|

|942210|Critical - 5|2|Detects chained SQL injection attempts 1/2|

|942220|Critical - 5|1|Looking for integer overflow attacks, these are taken from skipfish, except 3.0.00738585072007e-308 is the "magic number" crash|

|942230|Critical - 5|1|Detects conditional SQL injection attempts|

|942240|Critical - 5|1|Detects MySQL charset switch and MSSQL DoS attempts|

|942250|Critical - 5|1|Detects MATCH AGAINST, MERGE and EXECUTE IMMEDIATE injections|

|942260|Critical - 5|2|Detects basic SQL authentication bypass attempts 2/3 (replaced by rule #99031004)|

|942270|Critical - 5|1|Looking for basic sql injection. Common attack string for mysql, oracle and others.|

|942280|Critical - 5|1|Detects Postgres pg_sleep injection, waitfor delay attacks and database shutdown attempts|

|942290|Critical - 5|1|Finds basic MongoDB SQL injection attempts|

|942300|Critical - 5|2|Detects MySQL comments, conditions and ch(a)r injections|

|942310|Critical - 5|2|Detects chained SQL injection attempts 2/2|

|942320|Critical - 5|1|Detects MySQL and PostgreSQL stored procedure/function injections|

|942330|Critical - 5|2|Detects classic SQL injection probings 1/3|

|942340|Critical - 5|2|Detects basic SQL authentication bypass attempts 3/3 (replaced by rule #99031006)|

|942350|Critical - 5|1|Detects MySQL UDF injection and other data/structure manipulation attempts|

|942360|Critical - 5|1|Detects concatenated basic SQL injection and SQLLFI attempts|

|942361|Critical - 5|2|Detects basic SQL injection based on keyword alter or union|

|942370|Critical - 5|2|Detects classic SQL injection probings 2/3|

|942380|Critical - 5|2|SQL Injection Attack|

|942390|Critical - 5|2|SQL Injection Attack|

|942400|Critical - 5|2|SQL Injection Attack|

|942410|Critical - 5|2|SQL Injection Attack|

|942430|Warning - 3|2|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12) (replaced by rule #99031005)|

|942440|Critical - 5|2|SQL Comment Sequence Detected (replaced by rule #99031002).|

|942450|Critical - 5|2|SQL Hex Encoding Identified|

|942470|Critical - 5|2|SQL Injection Attack|

|942480|Critical - 5|2|SQL Injection Attack|

|942500|Critical - 5|1|MySQL in-line comment detected.|

|942510|Critical - 5|2|SQLi bypass attempt by ticks or backticks detected.|

### <a name="drs943-22"></a> Session fixation

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|943100|Critical - 5|1|Possible Session Fixation Attack: Setting Cookie Values in HTML|

|943110|Critical - 5|1|Possible Session Fixation Attack: SessionID Parameter Name with Off-Domain Referer|

|943120|Critical - 5|1|Possible Session Fixation Attack: SessionID Parameter Name with No Referer|

### <a name="drs944-22"></a> Java attacks

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|944100|Critical - 5|1|Remote Command Execution: Suspicious Java class detected|

|944110|Critical - 5|1|Remote Command Execution: Java process spawn (CVE-2017-9805)|

|944120|Critical - 5|1|Remote Command Execution: Java serialization (CVE-2015-5842)|

|944130|Critical - 5|1|Suspicious Java class detected|

|944200|Critical - 5|2|Magic bytes Detected, probable java serialization in use|

|944210|Critical - 5|2|Magic bytes Detected Base64 Encoded, probable java serialization in use|

|944240|Critical - 5|2|Remote Command Execution: Java serialization and Log4j vulnerability (CVE-2021-44228, CVE-2021-45046)|

|944250|Critical - 5|2|Remote Command Execution: Suspicious Java method detected|

### <a name="drs9905-22"></a> MS-ThreatIntel-WebShells

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99005002|Critical - 5|2|Web Shell Interaction Attempt (POST)|

|99005003|Critical - 5|2|Web Shell Upload Attempt (POST) - CHOPPER PHP|

|99005004|Critical - 5|2|Web Shell Upload Attempt (POST) - CHOPPER ASPX|

|99005005|Critical - 5|2|Web Shell Interaction Attempt|

|99005006|Critical - 5|2|Spring4Shell Interaction Attempt|

### <a name="drs9903-22"></a> MS-ThreatIntel-AppSec

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99030001|Critical - 5|2|Path Traversal Evasion in Headers (/.././../)|

|99030002|Critical - 5|2|Path Traversal Evasion in Request Body (/.././../)|

|99030003|Critical - 5|2|URL encoded file path|

|99030004|Critical - 5|2|Missing brotli encoding from supporting browser with https referer|

|99030005|Critical - 5|2|Missing brotli encoding from supporting browser over HTTP/2|

|99030006|Critical - 5|2|Illegal character in requested filename|

### <a name="drs99031-22"></a> MS-ThreatIntel-SQLI

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99031001|Warning - 3|2|SQL Injection Attack: Common Injection Testing Detected (replacing rule #942110)|

|99031002|Critical - 5|2|SQL Comment Sequence Detected (replacing rule #942440).|

|99031003|Critical - 5|2|SQL Injection Attack (replacing rule #942150)|

|99031004|Critical - 5|2|Detects basic SQL authentication bypass attempts 2/3 (replacing rule #942260)|

|99031005|Warning - 3|2|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12) (replacing rule #942430)|

|99031006|Critical - 5|2|Detects basic SQL authentication bypass attempts 3/3 (replacing rule #942340)|

### <a name="drs99001-22"></a> MS-ThreatIntel-CVEs

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99001001|Critical - 5|2|Attempted F5 tmui (CVE-2020-5902) REST API exploitation with known credentials|

|99001002|Critical - 5|2|Attempted Citrix NSC_USER directory traversal [CVE-2019-19781](https://www.cve.org/CVERecord?id=CVE-2019-19781)|

|99001003|Critical - 5|2|Attempted Atlassian Confluence Widget Connector exploitation [CVE-2019-3396](https://www.cve.org/CVERecord?id=CVE-2019-3396)|

|99001004|Critical - 5|2|Attempted Pulse Secure custom template exploitation [CVE-2020-8243](https://www.cve.org/CVERecord?id=CVE-2019-8243)|

|99001005|Critical - 5|2|Attempted SharePoint type converter exploitation [CVE-2020-0932](https://www.cve.org/CVERecord?id=CVE-2019-0932)|

|99001006|Critical - 5|2|Attempted Pulse Connect directory traversal [CVE-2019-11510](https://www.cve.org/CVERecord?id=CVE-2019-11510)|

|99001007|Critical - 5|2|Attempted Junos OS J-Web local file inclusion [CVE-2020-1631](https://www.cve.org/CVERecord?id=CVE-2019-1631)|

|99001008|Critical - 5|2|Attempted Fortinet path traversal [CVE-2018-13379](https://www.cve.org/CVERecord?id=CVE-2019-13379)|

|99001009|Critical - 5|2|Attempted Apache struts ognl injection [CVE-2017-5638](https://www.cve.org/CVERecord?id=CVE-2019-5638)|

|99001010|Critical - 5|2|Attempted Apache struts ognl injection [CVE-2017-12611](https://www.cve.org/CVERecord?id=CVE-2019-12611)|

|99001011|Critical - 5|2|Attempted Oracle WebLogic path traversal [CVE-2020-14882](https://www.cve.org/CVERecord?id=CVE-2019-14882)|

|99001012|Critical - 5|2|Attempted Telerik WebUI insecure deserialization exploitation [CVE-2019-18935](https://www.cve.org/CVERecord?id=CVE-2019-18935)|

|99001013|Critical - 5|2|Attempted SharePoint insecure XML deserialization [CVE-2019-0604](https://www.cve.org/CVERecord?id=CVE-2019-0604)|

|99001014|Critical - 5|2|Attempted Spring Cloud routing-expression injection [CVE-2022-22963](https://www.cve.org/CVERecord?id=CVE-2022-22963)|

|99001015|Critical - 5|2|Attempted Spring Framework unsafe class object exploitation [CVE-2022-22965](https://www.cve.org/CVERecord?id=CVE-2022-22965)|

|99001016|Critical - 5|2|Attempted Spring Cloud Gateway Actuator injection [CVE-2022-22947](https://www.cve.org/CVERecord?id=CVE-2022-22947)|

|99001017|Critical - 5|2|Attempted Apache Struts file upload exploitation [CVE-2023-50164](https://www.cve.org/CVERecord?id=CVE-2023-50164)|

### <a name="drs99032-22"></a> MS-ThreatIntel-XSS

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99032001|Critical - 5|1|XSS Filter - Category 2: Event Handler Vector (replacing rule #941120)|

|99032002|Critical - 5|2|Possible Remote File Inclusion (RFI) Attack: Off-Domain Reference/Link (replacing rule #931130)|

> [!NOTE]

> - When you review your WAF's logs, you might see rule ID 949110. The description of the rule might include *Inbound Anomaly Score Exceeded*. This rule indicates that the total anomaly score for the request exceeded the maximum allowable score. For more information, see [Anomaly scoring](#anomaly-scoring-mode).

>

>

> - When you tune your WAF policies, you need to investigate the other rules that were triggered by the request so that you can adjust your WAF's configuration. For more information, see [Tuning Azure Web Application Firewall for Azure Front Door](waf-front-door-tuning.md).

# [DRS 2.1](#tab/drs21)

## <a name="drs21"></a> 2.1 rule sets

### <a name="general-21"></a> General

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|200002|Critical - 5|1|Failed to parse request body|

|200003|Critical - 5|1|Multipart request body failed strict validation|

### <a name="drs911-21"></a> Method enforcement

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|911100|Critical - 5|1|Method isn't allowed by policy|

### <a name="drs920-21"></a> Protocol enforcement

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|920100|Notice - 2|1|Invalid HTTP Request Line|

|920120|Critical - 5|1|Attempted multipart/form-data bypass|

|920121|Critical - 5|2|Attempted multipart/form-data bypass|

|920160|Critical - 5|1|Content-Length HTTP header isn't numeric|

|920170|Critical - 5|1|GET or HEAD Request with Body Content|

|920171|Critical - 5|1|GET or HEAD Request with Transfer-Encoding|

|920180|Notice - 2|1|POST request missing Content-Length Header|

|920181|Warning - 3|1|Content-Length and Transfer-Encoding headers present 99001003|

|920190|Warning - 3|1|Range: Invalid Last Byte Value|

|920200|Warning - 3|2|Range: Too many fields (6 or more)|

|920201|Warning - 3|2|Range: Too many fields for pdf request (35 or more)|

|920210|Warning - 3|1|Multiple/Conflicting Connection Header Data Found|

|920220|Warning - 3|1|URL Encoding Abuse Attack Attempt|

|920230|Warning - 3|2|Multiple URL Encoding Detected|

|920240|Warning - 3|1|URL Encoding Abuse Attack Attempt|

|920260|Warning - 3|1|Unicode Full/Half Width Abuse Attack Attempt|

|920270|Critical - 5|1|Invalid character in request (null character)|

|920271|Critical - 5|2|Invalid character in request (nonprintable characters)|

|920280|Warning - 3|1|Request Missing a Host Header|

|920290|Warning - 3|1|Empty Host Header|

|920300|Notice - 2|2|Request Missing an Accept Header|

|920310|Notice - 2|1|Request Has an Empty Accept Header|

|920311|Notice - 2|1|Request Has an Empty Accept Header|

|920320|Notice - 2|2|Missing User Agent Header|

|920330|Notice - 2|1|Empty User Agent Header|

|920340|Notice - 2|1|Request Containing Content, but Missing Content-Type header|

|920341|Critical - 5|2|Request containing content requires Content-Type header|

|920350|Warning - 3|1|Host header is a numeric IP address|

|920420|Critical - 5|1|Request content type isn't allowed by policy|

|920430|Critical - 5|1|HTTP protocol version isn't allowed by policy|

|920440|Critical - 5|1|URL file extension is restricted by policy|

|920450|Critical - 5|1|HTTP header is restricted by policy|

|920470|Critical - 5|1|Illegal Content-Type header|

|920480|Critical - 5|1|Request content type charset isn't allowed by policy|

|920500|Critical - 5|1|Attempt to access a backup or working file|

### <a name="drs921-21"></a> Protocol attack

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|921110|Critical - 5|1|HTTP Request Smuggling Attack|

|921120|Critical - 5|1|HTTP Response Splitting Attack|

|921130|Critical - 5|1|HTTP Response Splitting Attack|

|921140|Critical - 5|1|HTTP Header Injection Attack via headers|

|921150|Critical - 5|1|HTTP Header Injection Attack via payload (CR/LF detected)|

|921151|Critical - 5|2|HTTP Header Injection Attack via payload (CR/LF detected)|

|921160|Critical - 5|1|HTTP Header Injection Attack via payload (CR/LF and header-name detected)|

|921190|Critical - 5|1|HTTP Splitting (CR/LF in request filename detected)|

|921200|Critical - 5|1|LDAP Injection Attack|

### <a name="drs930-21"></a> LFI: Local file inclusion

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|930100|Critical - 5|1|Path Traversal Attack (/../)|

|930110|Critical - 5|1|Path Traversal Attack (/../)|

|930120|Critical - 5|1|OS File Access Attempt|

|930130|Critical - 5|1|Restricted File Access Attempt|

### <a name="drs931-21"></a> RFI: Remote file inclusion

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|931100|Critical - 5|1|Possible Remote File Inclusion (RFI) Attack: URL Parameter using IP address|

|931110|Critical - 5|1|Possible Remote File Inclusion (RFI) Attack: Common RFI Vulnerable Parameter Name used w/URL Payload|

|931120|Critical - 5|1|Possible Remote File Inclusion (RFI) Attack: URL Payload Used w/Trailing Question Mark Character (?)|

|931130|Critical - 5|2|Possible Remote File Inclusion (RFI) Attack: Off-Domain Reference/Link|

### <a name="drs932-21"></a> RCE: Remote command execution

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|932100|Critical - 5|1|Remote Command Execution: Unix Command Injection|

|932105|Critical - 5|1|Remote Command Execution: Unix Command Injection|

|932110|Critical - 5|1|Remote Command Execution: Windows Command Injection|

|932115|Critical - 5|1|Remote Command Execution: Windows Command Injection|

|932120|Critical - 5|1|Remote Command Execution: Windows PowerShell Command Found|

|932130|Critical - 5|1|Remote Command Execution: Unix Shell Expression or Confluence Vulnerability (CVE-2022-26134) Found|

|932140|Critical - 5|1|Remote Command Execution: Windows FOR/IF Command Found|

|932150|Critical - 5|1|Remote Command Execution: Direct Unix Command Execution|

|932160|Critical - 5|1|Remote Command Execution: Unix Shell Code Found|

|932170|Critical - 5|1|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932171|Critical - 5|1|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932180|Critical - 5|1|Restricted File Upload Attempt|

### <a name="drs933-21"></a> PHP attacks

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|933100|Critical - 5|1|PHP Injection Attack: Opening/Closing Tag Found|

|933110|Critical - 5|1|PHP Injection Attack: PHP Script File Upload Found|

|933120|Critical - 5|1|PHP Injection Attack: Configuration Directive Found|

|933130|Critical - 5|1|PHP Injection Attack: Variables Found|

|933140|Critical - 5|1|PHP Injection Attack: I/O Stream Found|

|933150|Critical - 5|1|PHP Injection Attack: High-Risk PHP Function Name Found|

|933151|Critical - 5|2|PHP Injection Attack: Medium-Risk PHP Function Name Found|

|933160|Critical - 5|1|PHP Injection Attack: High-Risk PHP Function Call Found|

|933170|Critical - 5|1|PHP Injection Attack: Serialized Object Injection|

|933180|Critical - 5|1|PHP Injection Attack: Variable Function Call Found|

|933200|Critical - 5|1|PHP Injection Attack: Wrapper scheme detected|

|933210|Critical - 5|1|PHP Injection Attack: Variable Function Call Found|

### <a name="drs934-21"></a> Node JS attacks

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|934100|Critical - 5|1|Node.js Injection Attack|

### <a name="drs941-21"></a> XSS: Cross-site scripting

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|941100|Critical - 5|1|XSS Attack Detected via libinjection|

|941101|Critical - 5|2|XSS Attack Detected via libinjection<br />Rule detects requests with a `Referer` header|

|941110|Critical - 5|1|XSS Filter - Category 1: Script Tag Vector|

|941120|Critical - 5|1|XSS Filter - Category 2: Event Handler Vector|

|941130|Critical - 5|1|XSS Filter - Category 3: Attribute Vector|

|941140|Critical - 5|1|XSS Filter - Category 4: JavaScript URI Vector|

|941150|Critical - 5|2|XSS Filter - Category 5: Disallowed HTML Attributes|

|941160|Critical - 5|1|NoScript XSS InjectionChecker: HTML Injection|

|941170|Critical - 5|1|NoScript XSS InjectionChecker: Attribute Injection|

|941180|Critical - 5|1|Node-Validator Blocklist Keywords|

|941190|Critical - 5|1|XSS using style sheets|

|941200|Critical - 5|1|XSS using VML frames|

|941210|Critical - 5|1|XSS using obfuscated JavaScript|

|941220|Critical - 5|1|XSS using obfuscated VB Script|

|941230|Critical - 5|1|XSS using `embed` tag|

|941240|Critical - 5|1|XSS using `import` or `implementation` attribute|

|941250|Critical - 5|1|IE XSS Filters - Attack Detected|

|941260|Critical - 5|1|XSS using `meta` tag|

|941270|Critical - 5|1|XSS using `link` href|

|941280|Critical - 5|1|XSS using `base` tag|

|941290|Critical - 5|1|XSS using `applet` tag|

|941300|Critical - 5|1|XSS using `object` tag|

|941310|Critical - 5|1|US-ASCII Malformed Encoding XSS Filter - Attack Detected|

|941320|Critical - 5|2|Possible XSS Attack Detected - HTML Tag Handler|

|941330|Critical - 5|2|IE XSS Filters - Attack Detected|

|941340|Critical - 5|2|IE XSS Filters - Attack Detected|

|941350|Critical - 5|1|UTF-7 Encoding IE XSS - Attack Detected|

|941360|Critical - 5|1|JavaScript obfuscation detected|

|941370|Critical - 5|1|JavaScript global variable found|

|941380|Critical - 5|2|AngularJS client side template injection detected|

### <a name="drs942-21"></a> SQLI: SQL injection

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|942100|Critical - 5|1|SQL Injection Attack Detected via libinjection|

|942110|Warning - 3|2|SQL Injection Attack: Common Injection Testing Detected|

|942120|Critical - 5|2|SQL Injection Attack: SQL Operator Detected|

|942140|Critical - 5|1|SQL Injection Attack: Common DB Names Detected|

|942150|Critical - 5|2|SQL Injection Attack|

|942160|Critical - 5|1|Detects blind SQLI tests using sleep() or benchmark()|

|942170|Critical - 5|1|Detects SQL benchmark and sleep injection attempts including conditional queries|

|942180|Critical - 5|2|Detects basic SQL authentication bypass attempts 1/3|

|942190|Critical - 5|1|Detects MSSQL code execution and information gathering attempts|

|942200|Critical - 5|2|Detects MySQL comment-/space-obfuscated injections and backtick termination|

|942210|Critical - 5|2|Detects chained SQL injection attempts 1/2|

|942220|Critical - 5|1|Looking for integer overflow attacks, these are taken from skipfish, except 3.0.00738585072007e-308 is the "magic number" crash|

|942230|Critical - 5|1|Detects conditional SQL injection attempts|

|942240|Critical - 5|1|Detects MySQL charset switch and MSSQL DoS attempts|

|942250|Critical - 5|1|Detects MATCH AGAINST, MERGE, and EXECUTE IMMEDIATE injections|

|942260|Critical - 5|2|Detects basic SQL authentication bypass attempts 2/3|

|942270|Critical - 5|1|Looking for basic SQL injection. Common attack string for MySQL, Oracle, and others|

|942280|Critical - 5|1|Detects Postgres pg_sleep injection, wait for delay attacks, and database shutdown attempts|

|942290|Critical - 5|1|Finds basic MongoDB SQL injection attempts|

|942300|Critical - 5|2|Detects MySQL comments, conditions, and ch(a)r injections|

|942310|Critical - 5|2|Detects chained SQL injection attempts 2/2|

|942320|Critical - 5|1|Detects MySQL and PostgreSQL stored procedure/function injections|

|942330|Critical - 5|2|Detects classic SQL injection probings 1/2|

|942340|Critical - 5|2|Detects basic SQL authentication bypass attempts 3/3|

|942350|Critical - 5|1|Detects MySQL UDF injection and other data/structure manipulation attempts|

|942360|Critical - 5|1|Detects concatenated basic SQL injection and SQLLFI attempts|

|942361|Critical - 5|2|Detects basic SQL injection based on keyword alter or union|

|942370|Critical - 5|2|Detects classic SQL injection probings 2/2|

|942380|Critical - 5|2|SQL Injection Attack|

|942390|Critical - 5|2|SQL Injection Attack|

|942400|Critical - 5|2|SQL Injection Attack|

|942410|Critical - 5|2|SQL Injection Attack|

|942430|Warning - 3|2|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12)|

|942440|Critical - 5|2|SQL Comment Sequence Detected|

|942450|Critical - 5|2|SQL Hex Encoding Identified|

|942470|Critical - 5|2|SQL Injection Attack|

|942480|Critical - 5|2|SQL Injection Attack|

|942500|Critical - 5|1|MySQL in-line comment detected|

|942510|Critical - 5|2|SQLi bypass attempt by ticks or backticks detected|

### <a name="drs943-21"></a> Session fixation

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|943100|Critical - 5|1|Possible Session Fixation Attack: Setting Cookie Values in HTML|

|943110|Critical - 5|1|Possible Session Fixation Attack: SessionID Parameter Name with Off-Domain Referrer|

|943120|Critical - 5|1|Possible Session Fixation Attack: SessionID Parameter Name with No Referrer|

### <a name="drs944-21"></a> Java attacks

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|944100|Critical - 5|1|Remote Command Execution: Apache Struts, Oracle WebLogic|

|944110|Critical - 5|1|Detects potential payload execution|

|944120|Critical - 5|1|Possible payload execution and remote command execution|

|944130|Critical - 5|1|Suspicious Java classes|

|944200|Critical - 5|2|Exploitation of Java deserialization Apache Commons|

|944210|Critical - 5|2|Possible use of Java serialization|

|944240|Critical - 5|2|Remote Command Execution: Java serialization and Log4j vulnerability ([CVE-2021-44228](https://www.cve.org/CVERecord?id=CVE-2021-44228), [CVE-2021-45046](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-45046))|

|944250|Critical - 5|2|Remote Command Execution: Suspicious Java method detected|

### <a name="drs9905-21"></a> MS-ThreatIntel-WebShells

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99005002|Critical - 5|2|Web Shell Interaction Attempt (POST)|

|99005003|Critical - 5|2|Web Shell Upload Attempt (POST) - CHOPPER PHP|

|99005004|Critical - 5|2|Web Shell Upload Attempt (POST) - CHOPPER ASPX|

|99005005|Critical - 5|2|Web Shell Interaction Attempt|

|99005006|Critical - 5|2|Spring4Shell Interaction Attempt|

### <a name="drs9903-21"></a> MS-ThreatIntel-AppSec

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99030001|Critical - 5|2|Path Traversal Evasion in Headers (/.././../)|

|99030002|Critical - 5|2|Path Traversal Evasion in Request Body (/.././../)|

### <a name="drs99031-21"></a> MS-ThreatIntel-SQLI

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99031001|Warning - 3|2|SQL Injection Attack: Common Injection Testing Detected|

|99031002|Critical - 5|2|SQL Comment Sequence Detected|

|99031003|Critical - 5|2|SQL Injection Attack|

|99031004|Critical - 5|2|Detects basic SQL authentication bypass attempts 2/3|

### <a name="drs99001-21"></a> MS-ThreatIntel-CVEs

|Rule ID|Anomaly score severity|Paranoia Level|Description|

|---|---|--|--|

|99001001|Critical - 5|2|Attempted F5 tmui (CVE-2020-5902) REST API exploitation with known credentials|

|99001002|Critical - 5|2|Attempted Citrix NSC_USER directory traversal [CVE-2019-19781](https://www.cve.org/CVERecord?id=CVE-2019-19781)|

|99001003|Critical - 5|2|Attempted Atlassian Confluence Widget Connector exploitation [CVE-2019-3396](https://www.cve.org/CVERecord?id=CVE-2019-3396)|

|99001004|Critical - 5|2|Attempted Pulse Secure custom template exploitation [CVE-2020-8243](https://www.cve.org/CVERecord?id=CVE-2019-8243)|

|99001005|Critical - 5|2|Attempted SharePoint type converter exploitation [CVE-2020-0932](https://www.cve.org/CVERecord?id=CVE-2019-0932)|

|99001006|Critical - 5|2|Attempted Pulse Connect directory traversal [CVE-2019-11510](https://www.cve.org/CVERecord?id=CVE-2019-11510)|

|99001007|Critical - 5|2|Attempted Junos OS J-Web local file inclusion [CVE-2020-1631](https://www.cve.org/CVERecord?id=CVE-2019-1631)|

|99001008|Critical - 5|2|Attempted Fortinet path traversal [CVE-2018-13379](https://www.cve.org/CVERecord?id=CVE-2019-13379)|

|99001009|Critical - 5|2|Attempted Apache struts ognl injection [CVE-2017-5638](https://www.cve.org/CVERecord?id=CVE-2019-5638)|

|99001010|Critical - 5|2|Attempted Apache struts ognl injection [CVE-2017-12611](https://www.cve.org/CVERecord?id=CVE-2019-12611)|

|99001011|Critical - 5|2|Attempted Oracle WebLogic path traversal [CVE-2020-14882](https://www.cve.org/CVERecord?id=CVE-2019-14882)|

|99001012|Critical - 5|2|Attempted Telerik WebUI insecure deserialization exploitation [CVE-2019-18935](https://www.cve.org/CVERecord?id=CVE-2019-18935)|

|99001013|Critical - 5|2|Attempted SharePoint insecure XML deserialization [CVE-2019-0604](https://www.cve.org/CVERecord?id=CVE-2019-0604)|

|99001014|Critical - 5|2|Attempted Spring Cloud routing-expression injection [CVE-2022-22963](https://www.cve.org/CVERecord?id=CVE-2022-22963)|

|99001015|Critical - 5|2|Attempted Spring Framework unsafe class object exploitation [CVE-2022-22965](https://www.cve.org/CVERecord?id=CVE-2022-22965)|

|99001016|Critical - 5|2|Attempted Spring Cloud Gateway Actuator injection [CVE-2022-22947](https://www.cve.org/CVERecord?id=CVE-2022-22947)|

|99001017|Critical - 5|2|Attempted Apache Struts file upload exploitation [CVE-2023-50164](https://www.cve.org/CVERecord?id=CVE-2023-50164)|

> [!NOTE]

> When you review your WAF's logs, you might see rule ID 949110. The description of the rule might include *Inbound Anomaly Score Exceeded*.

>

> This rule indicates that the total anomaly score for the request exceeded the maximum allowable score. For more information, see [Anomaly scoring](#anomaly-scoring-mode).

>

> When you tune your WAF policies, you need to investigate the other rules that were triggered by the request so that you can adjust your WAF's configuration. For more information, see [Tuning Azure Web Application Firewall for Azure Front Door](waf-front-door-tuning.md).

# [DRS 2.0](#tab/drs20)

## <a name="drs20"></a> 2.0 rule sets

### <a name="general-20"></a> General

|Rule ID|Description|

|---|---|

|200002|Failed to parse request body|

|200003|Multipart request body failed strict validation|

### <a name="drs911-20"></a> Method enforcement

|Rule ID|Description|

|---|---|

|911100|Method isn't allowed by policy|

### <a name="drs920-20"></a> Protocol enforcement

|Rule ID|Description|

|---|---|

|920100|Invalid HTTP Request Line|

|920120|Attempted multipart/form-data bypass|

|920121|Attempted multipart/form-data bypass|

|920160|Content-Length HTTP header isn't numeric|

|920170|GET or HEAD Request with Body Content|

|920171|GET or HEAD Request with Transfer-Encoding|

|920180|POST request missing Content-Length Header|

|920190|Range: Invalid Last Byte Value|

|920200|Range: Too many fields (6 or more)|

|920201|Range: Too many fields for pdf request (35 or more)|

|920210|Multiple/Conflicting Connection Header Data Found|

|920220|URL Encoding Abuse Attack Attempt|

|920230|Multiple URL Encoding Detected|

|920240|URL Encoding Abuse Attack Attempt|

|920260|Unicode Full/Half Width Abuse Attack Attempt|

|920270|Invalid character in request (null character)|

|920271|Invalid character in request (nonprintable characters)|

|920280|Request Missing a Host Header|

|920290|Empty Host Header|

|920300|Request Missing an Accept Header|

|920310|Request Has an Empty Accept Header|

|920311|Request Has an Empty Accept Header|

|920320|Missing User Agent Header|

|920330|Empty User Agent Header|

|920340|Request Containing Content, but Missing Content-Type header|

|920341|Request containing content requires Content-Type header|

|920350|Host header is a numeric IP address|

|920420|Request content type isn't allowed by policy|

|920430|HTTP protocol version isn't allowed by policy|

|920440|URL file extension is restricted by policy|

|920450|HTTP header is restricted by policy|

|920470|Illegal Content-Type header|

|920480|Request content type charset isn't allowed by policy|

### <a name="drs921-20"></a> Protocol attack

|Rule ID|Description|

|---|---|

|921110|HTTP Request Smuggling Attack|

|921120|HTTP Response Splitting Attack|

|921130|HTTP Response Splitting Attack|

|921140|HTTP Header Injection Attack via headers|

|921150|HTTP Header Injection Attack via payload (CR/LF detected)|

|921151|HTTP Header Injection Attack via payload (CR/LF detected)|

|921160|HTTP Header Injection Attack via payload (CR/LF and header-name detected)|

### <a name="drs930-20"></a> LFI: Local file inclusion

|Rule ID|Description|

|---|---|

|930100|Path Traversal Attack (/../)|

|930110|Path Traversal Attack (/../)|

|930120|OS File Access Attempt|

|930130|Restricted File Access Attempt|

### <a name="drs931-20"></a> RFI: Remote file inclusion

|Rule ID|Description|

|---|---|

|931100|Possible Remote File Inclusion (RFI) Attack: URL Parameter using IP Address|

|931110|Possible Remote File Inclusion (RFI) Attack: Common RFI Vulnerable Parameter Name used w/URL Payload|

|931120|Possible Remote File Inclusion (RFI) Attack: URL Payload Used w/Trailing Question Mark Character (?)|

|931130|Possible Remote File Inclusion (RFI) Attack: Off-Domain Reference/Link|

### <a name="drs932-20"></a> RCE: Remote command execution

|Rule ID|Description|

|---|---|

|932100|Remote Command Execution: Unix Command Injection|

|932105|Remote Command Execution: Unix Command Injection|

|932110|Remote Command Execution: Windows Command Injection|

|932115|Remote Command Execution: Windows Command Injection|

|932120|Remote Command Execution: Windows PowerShell Command Found|

|932130|Remote Command Execution: Unix Shell Expression or Confluence Vulnerability (CVE-2022-26134) or Text4Shell ([CVE-2022-42889](https://nvd.nist.gov/vuln/detail/CVE-2022-42889)) Found|

|932140|Remote Command Execution: Windows FOR/IF Command Found|

|932150|Remote Command Execution: Direct Unix Command Execution|

|932160|Remote Command Execution: Unix Shell Code Found|

|932170|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932171|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932180|Restricted File Upload Attempt|

### <a name="drs933-20"></a> PHP attacks

|Rule ID|Description|

|---|---|

|933100|PHP Injection Attack: Opening/Closing Tag Found|

|933110|PHP Injection Attack: PHP Script File Upload Found|

|933120|PHP Injection Attack: Configuration Directive Found|

|933130|PHP Injection Attack: Variables Found|

|933140|PHP Injection Attack: I/O Stream Found|

|933150|PHP Injection Attack: High-Risk PHP Function Name Found|

|933151|PHP Injection Attack: Medium-Risk PHP Function Name Found|

|933160|PHP Injection Attack: High-Risk PHP Function Call Found|

|933170|PHP Injection Attack: Serialized Object Injection|

|933180|PHP Injection Attack: Variable Function Call Found|

|933200|PHP Injection Attack: Wrapper scheme detected|

|933210|PHP Injection Attack: Variable Function Call Found|

### <a name="drs934-20"></a> Node JS attacks

|Rule ID|Description|

|---|---|

|934100|Node.js Injection Attack|

### <a name="drs941-20"></a> XSS: Cross-site scripting

|Rule ID|Description|

|---|---|

|941100|XSS Attack Detected via libinjection|

|941101|XSS Attack Detected via libinjection.<br />This rule detects requests with a `Referer` header|

|941110|XSS Filter - Category 1: Script Tag Vector|

|941120|XSS Filter - Category 2: Event Handler Vector|

|941130|XSS Filter - Category 3: Attribute Vector|

|941140|XSS Filter - Category 4: JavaScript URI Vector|

|941150|XSS Filter - Category 5: Disallowed HTML Attributes|

|941160|NoScript XSS InjectionChecker: HTML Injection|

|941170|NoScript XSS InjectionChecker: Attribute Injection|

|941180|Node-Validator Blocklist Keywords|

|941190|XSS Using style sheets|

|941200|XSS using VML frames|

|941210|IE XSS Filters - Attack Detected or Text4Shell ([CVE-2022-42889](https://nvd.nist.gov/vuln/detail/CVE-2022-42889))|

|941220|XSS using obfuscated VB Script|

|941230|XSS using `embed` tag|

|941240|XSS using `import` or `implementation` attribute|

|941250|IE XSS Filters - Attack Detected|

|941260|XSS using `meta` tag|

|941270|XSS using `link` href|

|941280|XSS using `base` tag|

|941290|XSS using `applet` tag|

|941300|XSS using `object` tag|

|941310|US-ASCII Malformed Encoding XSS Filter - Attack Detected|

|941320|Possible XSS Attack Detected - HTML Tag Handler|

|941330|IE XSS Filters - Attack Detected|

|941340|IE XSS Filters - Attack Detected|

|941350|UTF-7 Encoding IE XSS - Attack Detected|

|941360|JavaScript obfuscation detected|

|941370|JavaScript global variable found|

|941380|AngularJS client side template injection detected|

### <a name="drs942-20"></a> SQLI: SQL injection

|Rule ID|Description|

|---|---|

|942100|SQL Injection Attack Detected via libinjection|

|942110|SQL Injection Attack: Common Injection Testing Detected|

|942120|SQL Injection Attack: SQL Operator Detected|

|942140|SQL Injection Attack: Common DB Names Detected|

|942150|SQL Injection Attack|

|942160|Detects blind SQLI tests using sleep() or benchmark()|

|942170|Detects SQL benchmark and sleep injection attempts including conditional queries|

|942180|Detects basic SQL authentication bypass attempts 1/3|

|942190|Detects MSSQL code execution and information gathering attempts|

|942200|Detects MySQL comment-/space-obfuscated injections and backtick termination|

|942210|Detects chained SQL injection attempts 1/2|

|942220|Looking for integer overflow attacks, these are taken from skipfish, except 3.0.00738585072007e-308 is the "magic number" crash|

|942230|Detects conditional SQL injection attempts|

|942240|Detects MySQL charset switch and MSSQL DoS attempts|

|942250|Detects MATCH AGAINST, MERGE, and EXECUTE IMMEDIATE injections|

|942260|Detects basic SQL authentication bypass attempts 2/3|

|942270|Looking for basic SQL injection. Common attack string for MySQL, Oracle, and others|

|942280|Detects Postgres pg_sleep injection, wait for delay attacks and database shutdown attempts|

|942290|Finds basic MongoDB SQL injection attempts|

|942300|Detects MySQL comments, conditions, and ch(a)r injections|

|942310|Detects chained SQL injection attempts 2/2|

|942320|Detects MySQL and PostgreSQL stored procedure/function injections|

|942330|Detects classic SQL injection probings 1/2|

|942340|Detects basic SQL authentication bypass attempts 3/3|

|942350|Detects MySQL UDF injection and other data/structure manipulation attempts|

|942360|Detects concatenated basic SQL injection and SQLLFI attempts|

|942361|Detects basic SQL injection based on keyword alter or union|

|942370|Detects classic SQL injection probings 2/2|

|942380|SQL Injection Attack|

|942390|SQL Injection Attack|

|942400|SQL Injection Attack|

|942410|SQL Injection Attack|

|942430|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12)|

|942440|SQL Comment Sequence Detected|

|942450|SQL Hex Encoding Identified|

|942460|Meta-Character Anomaly Detection Alert - Repetitive Non-Word Characters|

|942470|SQL Injection Attack|

|942480|SQL Injection Attack|

|942500|MySQL in-line comment detected|

|942510|SQLi bypass attempt by ticks or backticks detected|

### <a name="drs943-20"></a> Session fixation

|Rule ID|Description|

|---|---|

|943100|Possible Session Fixation Attack: Setting Cookie Values in HTML|

|943110|Possible Session Fixation Attack: SessionID Parameter Name with Off-Domain Referrer|

|943120|Possible Session Fixation Attack: SessionID Parameter Name with No Referrer|

### <a name="drs944-20"></a> Java attacks

|Rule ID|Description|

|---|---|

|944100|Remote Command Execution: Apache Struts, Oracle WebLogic|

|944110|Detects potential payload execution|

|944120|Possible payload execution and remote command execution|

|944130|Suspicious Java classes|

|944200|Exploitation of Java deserialization Apache Commons|

|944210|Possible use of Java serialization|

|944240|Remote Command Execution: Java serialization and Log4j vulnerability ([CVE-2021-44228](https://www.cve.org/CVERecord?id=CVE-2021-44228), [CVE-2021-45046](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-45046))|

|944250|Remote Command Execution: Suspicious Java method detected|

### <a name="drs9905-20"></a> MS-ThreatIntel-WebShells

|Rule ID|Description|

|---|---|

|99005002|Web Shell Interaction Attempt (POST)|

|99005003|Web Shell Upload Attempt (POST) - CHOPPER PHP|

|99005004|Web Shell Upload Attempt (POST) - CHOPPER ASPX|

|99005006|Spring4Shell Interaction Attempt|

### <a name="drs9903-20"></a> MS-ThreatIntel-AppSec

|Rule ID|Description|

|---|---|

|99030001|Path Traversal Evasion in Headers (/.././../)|

|99030002|Path Traversal Evasion in Request Body (/.././../)|

### <a name="drs99031-20"></a> MS-ThreatIntel-SQLI

|Rule ID|Description|

|---|---|

|99031001|SQL Injection Attack: Common Injection Testing Detected|

|99031002|SQL Comment Sequence Detected|

### <a name="drs99001-20"></a> MS-ThreatIntel-CVEs

|Rule ID|Description|

|---|---|

|99001001|Attempted F5 tmui (CVE-2020-5902) REST API Exploitation with known credentials|

|99001014|Attempted Spring Cloud routing-expression injection [CVE-2022-22963](https://www.cve.org/CVERecord?id=CVE-2022-22963)|

|99001015|Attempted Spring Framework unsafe class object exploitation [CVE-2022-22965](https://www.cve.org/CVERecord?id=CVE-2022-22965)|

|99001016|Attempted Spring Cloud Gateway Actuator injection [CVE-2022-22947](https://www.cve.org/CVERecord?id=CVE-2022-22947)

|99001017|Attempted Apache Struts file upload exploitation [CVE-2023-50164](https://www.cve.org/CVERecord?id=CVE-2023-50164)|

> [!NOTE]

> When you review your WAF's logs, you might see rule ID 949110. The description of the rule might include *Inbound Anomaly Score Exceeded*.

>

> This rule indicates that the total anomaly score for the request exceeded the maximum allowable score. For more information, see [Anomaly scoring](#anomaly-scoring-mode).

>

> When you tune your WAF policies, you need to investigate the other rules that were triggered by the request so that you can adjust your WAF's configuration. For more information, see [Tuning Azure Web Application Firewall for Azure Front Door](waf-front-door-tuning.md).

# [DRS 1.1](#tab/drs11)

## <a name="drs11"></a> 1.1 rule sets

### <a name="drs921-11"></a> Protocol attack

|Rule ID|Description|

|---|---|

|921110|HTTP Request Smuggling Attack|

|921120|HTTP Response Splitting Attack|

|921130|HTTP Response Splitting Attack|

|921140|HTTP Header Injection Attack via headers|

|921150|HTTP Header Injection Attack via payload (CR/LF detected)|

|921151|HTTP Header Injection Attack via payload (CR/LF detected)|

|921160|HTTP Header Injection Attack via payload (CR/LF and header-name detected)|

### <a name="drs930-11"></a> LFI: Local file inclusion

|Rule ID|Description|

|---|---|

|930100|Path Traversal Attack (/../)|

|930110|Path Traversal Attack (/../)|

|930120|OS File Access Attempt|

|930130|Restricted File Access Attempt|

### <a name="drs931-11"></a> RFI: Remote file inclusion

|Rule ID|Description|

|---|---|

|931100|Possible Remote File Inclusion (RFI) Attack: URL Parameter using IP Address|

|931110|Possible Remote File Inclusion (RFI) Attack: Common RFI Vulnerable Parameter Name used w/URL Payload|

|931120|Possible Remote File Inclusion (RFI) Attack: URL Payload Used w/Trailing Question Mark Character (?)|

|931130|Possible Remote File Inclusion (RFI) Attack: Off-Domain Reference/Link|

### <a name="drs932-11"></a> RCE: Remote command execution

|Rule ID|Description|

|---|---|

|932100|Remote Command Execution: Unix Command Injection|

|932105|Remote Command Execution: Unix Command Injection|

|932110|Remote Command Execution: Windows Command Injection|

|932115|Remote Command Execution: Windows Command Injection|

|931120|Remote Command Execution: Windows PowerShell Command Found|

|932130|Remote Command Execution: Unix Shell Expression or Confluence Vulnerability (CVE-2022-26134) or Text4Shell ([CVE-2022-42889](https://nvd.nist.gov/vuln/detail/CVE-2022-42889)) Found|

|932140|Remote Command Execution: Windows FOR/IF Command Found|

|932150|Remote Command Execution: Direct Unix Command Execution|

|932160|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932170|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932171|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932180|Restricted File Upload Attempt|

### <a name="drs933-11"></a> PHP attacks

|Rule ID|Description|

|---|---|

|933100|PHP Injection Attack: PHP Open Tag Found|

|933110|PHP Injection Attack: PHP Script File Upload Found|

|933120|PHP Injection Attack: Configuration Directive Found|

|933130|PHP Injection Attack: Variables Found|

|933140|PHP Injection Attack: I/O Stream Found|

|933150|PHP Injection Attack: High-Risk PHP Function Name Found|

|933151|PHP Injection Attack: Medium-Risk PHP Function Name Found|

|933160|PHP Injection Attack: High-Risk PHP Function Call Found|

|933170|PHP Injection Attack: Serialized Object Injection|

|933180|PHP Injection Attack: Variable Function Call Found|

### <a name="drs941-11"></a> XSS: Cross-site scripting

|Rule ID|Description|

|---|---|

|941100|XSS Attack Detected via libinjection|

|941101|XSS Attack Detected via libinjection.<br />This rule detects requests with a `Referer` header|

|941110|XSS Filter - Category 1: Script Tag Vector|

|941120|XSS Filter - Category 2: Event Handler Vector|

|941130|XSS Filter - Category 3: Attribute Vector|

|941140|XSS Filter - Category 4: JavaScript URI Vector|

|941150|XSS Filter - Category 5: Disallowed HTML Attributes|

|941160|NoScript XSS InjectionChecker: HTML Injection|

|941170|NoScript XSS InjectionChecker: Attribute Injection|

|941180|Node-Validator Blocklist Keywords|

|941190|IE XSS Filters - Attack Detected|

|941200|IE XSS Filters - Attack Detected|

|941210|IE XSS Filters - Attack Detected or Text4Shell ([CVE-2022-42889](https://nvd.nist.gov/vuln/detail/CVE-2022-42889)) found|

|941220|IE XSS Filters - Attack Detected|

|941230|IE XSS Filters - Attack Detected|

|941240|IE XSS Filters - Attack Detected|

|941250|IE XSS Filters - Attack Detected|

|941260|IE XSS Filters - Attack Detected|

|941270|IE XSS Filters - Attack Detected|

|941280|IE XSS Filters - Attack Detected|

|941290|IE XSS Filters - Attack Detected|

|941300|IE XSS Filters - Attack Detected|

|941310|US-ASCII Malformed Encoding XSS Filter - Attack Detected|

|941320|Possible XSS Attack Detected - HTML Tag Handler|

|941330|IE XSS Filters - Attack Detected|

|941340|IE XSS Filters - Attack Detected|

|941350|UTF-7 Encoding IE XSS - Attack Detected|

### <a name="drs942-11"></a> SQLI: SQL injection

|Rule ID|Description|

|---|---|

|942100|SQL Injection Attack Detected via libinjection|

|942110|SQL Injection Attack: Common Injection Testing Detected|

|942120|SQL Injection Attack: SQL Operator Detected|

|942140|SQL Injection Attack: Common DB Names Detected|

|942150|SQL Injection Attack|

|942160|Detects blind SQLI tests using sleep() or benchmark()|

|942170|Detects SQL benchmark and sleep injection attempts including conditional queries|

|942180|Detects basic SQL authentication bypass attempts 1/3|

|942190|Detects MSSQL code execution and information gathering attempts|

|942200|Detects MySQL comment-/space-obfuscated injections and backtick termination|

|942210|Detects chained SQL injection attempts 1/2|

|942220|Looking for integer overflow attacks, these are taken from skipfish, except 3.0.00738585072007e-308 is the "magic number" crash|

|942230|Detects conditional SQL injection attempts|

|942240|Detects MySQL charset switch and MSSQL DoS attempts|

|942250|Detects MATCH AGAINST, MERGE, and EXECUTE IMMEDIATE injections|

|942260|Detects basic SQL authentication bypass attempts 2/3|

|942270|Looking for basic SQL injection. Common attack string for MySQL, Oracle, and others|

|942280|Detects Postgres pg_sleep injection, wait for delay attacks and database shutdown attempts|

|942290|Finds basic MongoDB SQL injection attempts|

|942300|Detects MySQL comments, conditions, and ch(a)r injections|

|942310|Detects chained SQL injection attempts 2/2|

|942320|Detects MySQL and PostgreSQL stored procedure/function injections|

|942330|Detects classic SQL injection probings 1/3|

|942340|Detects basic SQL authentication bypass attempts 3/3|

|942350|Detects MySQL UDF injection and other data/structure manipulation attempts|

|942360|Detects concatenated basic SQL injection and SQLLFI attempts|

|942361|Detects basic SQL injection based on keyword alter or union|

|942370|Detects classic SQL injection probings 2/3|

|942380|SQL Injection Attack|

|942390|SQL Injection Attack|

|942400|SQL Injection Attack|

|942410|SQL Injection Attack|

|942430|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12)|

|942440|SQL Comment Sequence Detected|

|942450|SQL Hex Encoding Identified|

|942470|SQL Injection Attack|

|942480|SQL Injection Attack|

### <a name="drs943-11"></a> Session fixation

|Rule ID|Description|

|---|---|

|943100|Possible Session Fixation Attack: Setting Cookie Values in HTML|

|943110|Possible Session Fixation Attack: SessionID Parameter Name with Off-Domain Referrer|

|943120|Possible Session Fixation Attack: SessionID Parameter Name with No Referrer|

### <a name="drs944-11"></a> Java attacks

|Rule ID|Description|

|---|---|

|944100|Remote Command Execution: Suspicious Java class detected|

|944110|Possible Session Fixation Attack: Setting Cookie Values in HTML|

|944120|Remote Command Execution: Java serialization (CVE-2015-5842)|

|944130|Suspicious Java class detected|

|944200|Magic bytes Detected, probable Java serialization in use|

|944210|Magic bytes Detected Base64 Encoded, probable Java serialization in use|

|944240|Remote Command Execution: Java serialization and Log4j vulnerability ([CVE-2021-44228](https://www.cve.org/CVERecord?id=CVE-2021-44228), [CVE-2021-45046](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-45046))|

|944250|Remote Command Execution: Suspicious Java method detected|

### <a name="drs9905-11"></a> MS-ThreatIntel-WebShells

|Rule ID|Description|

|---|---|

|99005002|Web Shell Interaction Attempt (POST)|

|99005003|Web Shell Upload Attempt (POST) - CHOPPER PHP|

|99005004|Web Shell Upload Attempt (POST) - CHOPPER ASPX|

|99005006|Spring4Shell Interaction Attempt|

### <a name="drs9903-11"></a> MS-ThreatIntel-AppSec

|Rule ID|Description|

|---|---|

|99030001|Path Traversal Evasion in Headers (/.././../)|

|99030002|Path Traversal Evasion in Request Body (/.././../)|

### <a name="drs99031-11"></a> MS-ThreatIntel-SQLI

|Rule ID|Description|

|---|---|

|99031001|SQL Injection Attack: Common Injection Testing Detected|

|99031002|SQL Comment Sequence Detected|

### <a name="drs99001-11"></a> MS-ThreatIntel-CVEs

|Rule ID|Description|

|---|---|

|99001001|Attempted F5 tmui (CVE-2020-5902) REST API Exploitation with known credentials|

|99001014|Attempted Spring Cloud routing-expression injection [CVE-2022-22963](https://www.cve.org/CVERecord?id=CVE-2022-22963)|

|99001015|Attempted Spring Framework unsafe class object exploitation [CVE-2022-22965](https://www.cve.org/CVERecord?id=CVE-2022-22965)|

|99001016|Attempted Spring Cloud Gateway Actuator injection [CVE-2022-22947](https://www.cve.org/CVERecord?id=CVE-2022-22947)|

|99001017|Attempted Apache Struts file upload exploitation [CVE-2023-50164](https://www.cve.org/CVERecord?id=CVE-2023-50164)|

# [DRS 1.0](#tab/drs10)

## <a name="drs10"></a> 1.0 rule sets

### <a name="drs921-10"></a> Protocol attack

|Rule ID|Description|

|---|---|

|921110|HTTP Request Smuggling Attack|

|921120|HTTP Response Splitting Attack|

|921130|HTTP Response Splitting Attack|

|921140|HTTP Header Injection Attack via headers|

|921150|HTTP Header Injection Attack via payload (CR/LF detected)|

|921151|HTTP Header Injection Attack via payload (CR/LF detected)|

|921160|HTTP Header Injection Attack via payload (CR/LF and header-name detected)|

### <a name="drs930-10"></a> LFI: Local file inclusion

|Rule ID|Description|

|---|---|

|930100|Path Traversal Attack (/../)|

|930110|Path Traversal Attack (/../)|

|930120|OS File Access Attempt|

|930130|Restricted File Access Attempt|

### <a name="drs931-10"></a> RFI: Remote file inclusion

|Rule ID|Description|

|---|---|

|931100|Possible Remote File Inclusion (RFI) Attack: URL Parameter using IP Address|

|931110|Possible Remote File Inclusion (RFI) Attack: Common RFI Vulnerable Parameter Name used w/URL Payload|

|931120|Possible Remote File Inclusion (RFI) Attack: URL Payload Used w/Trailing Question Mark Character (?)|

|931130|Possible Remote File Inclusion (RFI) Attack: Off-Domain Reference/Link|

### <a name="drs932-10"></a> RCE: Remote command execution

|Rule ID|Description|

|---|---|

|932100|Remote Command Execution: Unix Command Injection|

|932105|Remote Command Execution: Unix Command Injection|

|932110|Remote Command Execution: Windows Command Injection|

|932115|Remote Command Execution: Windows Command Injection|

|932120|Remote Command Execution: Windows PowerShell Command Found|

|932130|Remote Command Execution: Unix Shell Expression or Confluence Vulnerability (CVE-2022-26134) or Text4Shell ([CVE-2022-42889](https://nvd.nist.gov/vuln/detail/CVE-2022-42889)) Found|

|932140|Remote Command Execution: Windows FOR/IF Command Found|

|932150|Remote Command Execution: Direct Unix Command Execution|

|932160|Remote Command Execution: Unix Shell Code Found|

|932170|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932171|Remote Command Execution: Shellshock (CVE-2014-6271)|

|932180|Restricted File Upload Attempt|

### <a name="drs933-10"></a> PHP attacks

|Rule ID|Description|

|---|---|

|933100|PHP Injection Attack: Opening/Closing Tag Found|

|933110|PHP Injection Attack: PHP Script File Upload Found|

|933120|PHP Injection Attack: Configuration Directive Found|

|933130|PHP Injection Attack: Variables Found|

|933140|PHP Injection Attack: I/O Stream Found|

|933150|PHP Injection Attack: High-Risk PHP Function Name Found|

|933151|PHP Injection Attack: Medium-Risk PHP Function Name Found|

|933160|PHP Injection Attack: High-Risk PHP Function Call Found|

|933170|PHP Injection Attack: Serialized Object Injection|

|933180|PHP Injection Attack: Variable Function Call Found|

### <a name="drs941-10"></a> XSS: Cross-site scripting

|Rule ID|Description|

|---|---|

|941100|XSS Attack Detected via libinjection|

|941101|XSS Attack Detected via libinjection.<br />This rule detects requests with a `Referer` header|

|941110|XSS Filter - Category 1: Script Tag Vector|

|941120|XSS Filter - Category 2: Event Handler Vector|

|941130|XSS Filter - Category 3: Attribute Vector|

|941140|XSS Filter - Category 4: JavaScript URI Vector|

|941150|XSS Filter - Category 5: Disallowed HTML Attributes|

|941160|NoScript XSS InjectionChecker: HTML Injection|

|941170|NoScript XSS InjectionChecker: Attribute Injection|

|941180|Node-Validator Blocklist Keywords|

|941190|XSS Using style sheets|

|941200|XSS using VML frames|

|941210|IE XSS Filters - Attack Detected or Text4Shell ([CVE-2022-42889](https://nvd.nist.gov/vuln/detail/CVE-2022-42889))|

|941220|XSS using obfuscated VB Script|

|941230|XSS using `embed` tag|

|941240|XSS using `import` or `implementation` attribute|

|941250|IE XSS Filters - Attack Detected|

|941260|XSS using `meta` tag|

|941270|XSS using `link` href|

|941280|XSS using `base` tag|

|941290|XSS using `applet` tag|

|941300|XSS using `object` tag|

|941310|US-ASCII Malformed Encoding XSS Filter - Attack Detected|

|941320|Possible XSS Attack Detected - HTML Tag Handler|

|941330|IE XSS Filters - Attack Detected|

|941340|IE XSS Filters - Attack Detected|

|941350|UTF-7 Encoding IE XSS - Attack Detected|

### <a name="drs942-10"></a> SQLI: SQL injection

|Rule ID|Description|

|---|---|

|942100|SQL Injection Attack Detected via libinjection|

|942110|SQL Injection Attack: Common Injection Testing Detected|

|942120|SQL Injection Attack: SQL Operator Detected|

|942140|SQL Injection Attack: Common DB Names Detected|

|942150|SQL Injection Attack|

|942160|Detects blind SQLI tests using sleep() or benchmark()|

|942170|Detects SQL benchmark and sleep injection attempts including conditional queries|

|942180|Detects basic SQL authentication bypass attempts 1/3|

|942190|Detects MSSQL code execution and information gathering attempts|

|942200|Detects MySQL comment-/space-obfuscated injections and backtick termination|

|942210|Detects chained SQL injection attempts 1/2|

|942220|Looking for integer overflow attacks, these are taken from skipfish, except 3.0.00738585072007e-308 is the "magic number" crash|

|942230|Detects conditional SQL injection attempts|

|942240|Detects MySQL charset switch and MSSQL DoS attempts|

|942250|Detects MATCH AGAINST, MERGE, and EXECUTE IMMEDIATE injections|

|942260|Detects basic SQL authentication bypass attempts 2/3|

|942270|Looking for basic SQL injection. Common attack string for MySQL, Oracle, and others|

|942280|Detects Postgres pg_sleep injection, wait for delay attacks and database shutdown attempts|

|942290|Finds basic MongoDB SQL injection attempts|

|942300|Detects MySQL comments, conditions, and ch(a)r injections|

|942310|Detects chained SQL injection attempts 2/2|

|942320|Detects MySQL and PostgreSQL stored procedure/function injections|

|942330|Detects classic SQL injection probings 1/2|

|942340|Detects basic SQL authentication bypass attempts 3/3|

|942350|Detects MySQL UDF injection and other data/structure manipulation attempts|

|942360|Detects concatenated basic SQL injection and SQLLFI attempts|

|942361|Detects basic SQL injection based on keyword alter or union|

|942370|Detects classic SQL injection probings 2/2|

|942380|SQL Injection Attack|

|942390|SQL Injection Attack|

|942400|SQL Injection Attack|

|942410|SQL Injection Attack|

|942430|Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12)|

|942440|SQL Comment Sequence Detected|

|942450|SQL Hex Encoding Identified|

|942470|SQL Injection Attack|

|942480|SQL Injection Attack|

### <a name="drs943-10"></a> Session fixation

|Rule ID|Description|

|---|---|

|943100|Possible Session Fixation Attack: Setting Cookie Values in HTML|

|943110|Possible Session Fixation Attack: SessionID Parameter Name with Off-Domain Referrer|

|943120|Possible Session Fixation Attack: SessionID Parameter Name with No Referrer|

### <a name="drs944-10"></a> Java attacks

|Rule ID|Description|

|---|---|

|944100|Remote Command Execution: Apache Struts, Oracle WebLogic|

|944110|Detects potential payload execution|

|944120|Possible payload execution and remote command execution|

|944130|Suspicious Java classes|

|944200|Exploitation of Java deserialization Apache Commons|

|944210|Possible use of Java serialization|

|944240|Remote Command Execution: Java serialization and Log4j vulnerability ([CVE-2021-44228](https://www.cve.org/CVERecord?id=CVE-2021-44228), [CVE-2021-45046](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-45046))|

|944250|Remote Command Execution: Suspicious Java method detected|

### <a name="drs9905-10"></a> MS-ThreatIntel-WebShells

|Rule ID|Description|

|---|---|

|99005006|Spring4Shell Interaction Attempt|

### <a name="drs99001-10"></a> MS-ThreatIntel-CVEs

|Rule ID|Description|

|---|---|

|99001014|Attempted Spring Cloud routing-expression injection [CVE-2022-22963](https://www.cve.org/CVERecord?id=CVE-2022-22963)|

|99001015|Attempted Spring Framework unsafe class object exploitation [CVE-2022-22965](https://www.cve.org/CVERecord?id=CVE-2022-22965)|

|99001016|Attempted Spring Cloud Gateway Actuator injection [CVE-2022-22947](https://www.cve.org/CVERecord?id=CVE-2022-22947)|

|99001017|Attempted Apache Struts file upload exploitation [CVE-2023-50164](https://www.cve.org/CVERecord?id=CVE-2023-50164)|

# [Bot Manager 1.0](#tab/bot)

## <a name="bot"></a> 1.0 rule sets

### <a name="bot100"></a> Bad bots

|Rule ID|Description|

|---|---|

|Bot100100|Malicious bots detected by threat intelligence|

|Bot100200|Malicious bots that have falsified their identity|

Bot100100 scans both client IP addresses and IPs in the `X-Forwarded-For` header.

### <a name="bot200"></a> Good bots

|Rule ID|Description|

|---|---|

|Bot200100|Search engine crawlers|

|Bot200200|Unverified search engine crawlers|

### <a name="bot300"></a> Unknown bots

|Rule ID|Description|

|---|---|

|Bot300100|Unspecified identity|

|Bot300200|Tools and frameworks for web crawling and attacks|

|Bot300300|General-purpose HTTP clients and SDKs|

|Bot300400|Service agents|

|Bot300500|Site health monitoring services|

|Bot300600|Unknown bots detected by threat intelligence|

|Bot300700|Other bots|

Bot300600 scans both client IP addresses and IPs in the `X-Forwarded-For` header.

# [Bot Manager 1.1](#tab/bot11)

## <a name="bot11"></a> 1.1 rule sets

### <a name="bot11-100"></a> Bad bots

|Rule ID|Description|

|---|---|

|Bot100100|Malicious bots detected by threat intelligence|

|Bot100200|Malicious bots that have falsified their identity|

|Bot100300|High risk bots detected by threat intelligence|

Bot100100 scans both client IP addresses and IPs in the `X-Forwarded-For` header.

### <a name="bot11-200"></a> Good bots

|Rule ID|Description|

|---|---|

|Bot200100|Search engine crawlers|

|Bot200200|Verified miscellaneous bots|

|Bot200300|Verified link checker bots|

|Bot200400|Verified social media bots|

|Bot200500|Verified content fetchers|

|Bot200600|Verified feed fetchers|

|Bot200700|Verified advertising bots|

### <a name="bot11-300"></a> Unknown bots

|Rule ID|Description|

|---|---|

|Bot300100|Unspecified identity|

|Bot300200|Tools and frameworks for web crawling and attacks|

|Bot300300|General-purpose HTTP clients and SDKs|

|Bot300400|Service agents|

|Bot300500|Site health monitoring services|

|Bot300600|Unknown bots detected by threat intelligence. This rule also includes IP addresses matched to the Tor network|

|Bot300700|Other bots|

Bot300600 scans both client IP addresses and IPs in the `X-Forwarded-For` header.

---

## Related content

- [Custom rules for Azure Web Application Firewall on Azure Front Door](waf-front-door-custom-rules.md)

- [Policy settings for Web Application Firewall in Azure Front Door](/azure/web-application-firewall/afds/waf-front-door-policy-settings)

- [Learn more about Azure network security](../../networking/security/index.yml)


# Waf Front Door Exclusion

# Web Application Firewall with Azure Front Door exclusion lists

**Applies to:** :heavy_check_mark: Front Door Premium

Sometimes Azure Web Application Firewall in Azure Front Door blocks a legitimate request. As part of tuning your web application firewall (WAF), you can configure the WAF to allow the request for your application. WAF exclusion lists allow you to omit specific request attributes from a WAF evaluation. The rest of the request is evaluated as normal.

For example, Microsoft Entra ID provides tokens that are used for authentication. When these tokens are used in a request header, they can contain special characters that trigger a false positive detection by one or more WAF rules. You can add the header to an exclusion list, which tells the WAF to ignore the header. The WAF still inspects the rest of the request for suspicious content.

## Exclusion scopes

You can create exclusions at the following scopes:

- **Rule set**: These exclusions apply to all rules within a rule set.

- **Rule group**: These exclusions apply to all the rules of a particular category within a rule set. For example, you can configure an exclusion that applies to all the SQL injection rules.

- **Rule**: These exclusions apply to a single rule.

> [!TIP]

> Make exclusions as narrow and specific as possible to avoid accidentally leaving room for attackers to exploit your system. When you need to add an exclusion rule, use per-rule exclusions wherever possible.

## Exclusion selectors

Exclusion selectors identify the parts of requests to which the exclusion applies. The WAF ignores any detections that it finds in the specified parts of the request. You can specify multiple exclusion selectors in a single exclusion.

Each exclusion selector specifies a match variable, an operator, and a selector. Multiple matches in a single exclusion are treated as "OR" statements.

### Match variables

Add the following request attributes to an exclusion:

* Request header name

* Request cookie name

* Query string args name

* Request body POST args name

* Request body JSON args name *(supported on DRS 2.0 or greater)*

The values of the fields you use aren't evaluated against WAF rules, but their names are evaluated. The exclusion lists disable inspection of the field's value. However, the field names are still evaluated. For more information, see [Exclude other request attributes](#exclude-other-request-attributes).

### Operators

Specify an exact request header, body, cookie, or query string attribute to match. Or optionally specify partial matches. The following operators are supported for match criteria:

- **Equals**: Match all request fields that exactly match the specified selector value. For example, to select a header named **bearerToken**, use the `Equals` operator with the selector set to **bearerToken**.

- **Starts with**: Match all request fields that start with the specified selector value.

- **Ends with**: Match all request fields that end with the specified selector value.

- **Contains**: Match all request fields that contain the specified selector value.

- **Equals any**: Match all request fields. When you use the `Equals any` operator, the selector value is automatically set to `*`. For example, use the `Equals any` operator to configure an exclusion that applies to all request headers.

### Case sensitivity

Header and cookie names aren't case sensitive. Query strings, POST arguments, and JSON arguments are case sensitive.

### Body contents inspection

Some of the managed rules evaluate the raw payload of the request body before it's parsed into POST arguments or JSON arguments. So in some situations, you might see log entries with a `matchVariableName` value of `InitialBodyContents` or `DecodedInitialBodyContents`.

For example, suppose you create an exclusion with a match variable of `Request body POST args` and a selector to identify and ignore POST arguments named `FOO`. You no longer see any log entries with a `matchVariableName` value of `PostParamValue:FOO`. However, if a POST argument named `FOO` contains text that triggers a rule, the log might show the detection in the initial body contents. You can't currently create exclusions for initial body contents.

## <a name="define-exclusion-based-on-web-application-firewall-logs"></a> Define exclusion rules based on Azure Web Application Firewall logs

You can use logs to view the details of a blocked request, including the parts of the request that triggered the rule. For more information, see [Azure Web Application Firewall monitoring and logging](waf-front-door-monitor.md).

Sometimes a specific WAF rule produces false positive detections from the values included in a request header, cookie, POST argument, query string argument, or JSON field in a request body. If these false positive detections happen, you can configure the rule to exclude the relevant part of the request from its evaluation.

The following table shows example values from WAF logs and the corresponding exclusion selectors that you could create.

| matchVariableName from WAF logs | Rule exclusion in portal |

|-|-|

| CookieValue:SOME_NAME	| Request cookie name Equals SOME_NAME |

| HeaderValue:SOME_NAME	| Request header name Equals SOME_NAME |

| PostParamValue:SOME_NAME | Request body POST args name Equals SOME_NAME |

| QueryParamValue:SOME_NAME | Query string args name Equals SOME_NAME |

| JsonValue:SOME_NAME | Request body JSON args name Equals SOME_NAME |

### Exclusions for JSON request bodies

Starting with DRS version 2.0, the WAF inspects JSON request bodies. For example, consider this JSON request body:

```json

{

"posts": [

{

"id": 1,

"comment": ""

},

{

"id": 2,

"comment": "\"1=1\""

}

]

}

```

The request includes a SQL comment character sequence, which the WAF detects as a potential SQL injection attack.

If you determine that the request is legitimate, create an exclusion with a match variable of `Request body JSON args name`, an operator of `Equals`, and a selector of `posts.comment`.

## Exclude other request attributes

If your WAF log entry shows a `matchVariableName` value that isn't in the preceding table, you can't create an exclusion. For example, you can't currently create exclusions for cookie names, header names, POST parameter names, or query parameter names.

Instead, consider taking one of the following actions:

- Disable the rules that give false positives.

- Create a custom rule that explicitly allows those requests. The requests bypass all WAF inspection.

When the `matchVariableName` value is `CookieName`, `HeaderName`, `PostParamName`, or `QueryParamName`, it means the name of the field, rather than its value, triggered the rule. Rule exclusion doesn't support these `matchVariableName` values.

## Next steps

- [Configure exclusion lists on your Azure Front Door WAF](waf-front-door-exclusion-configure.md).

- After you configure your WAF settings, learn how to view your WAF logs. For more information, see [Azure Front Door diagnostics](../afds/waf-front-door-monitor.md).


# Waf Front Door Exclusion Configure

# Configure web application firewall exclusion lists

Sometimes Azure Web Application Firewall in Azure Front Door might block a legitimate request. As part of tuning your web application firewall (WAF), you can configure the WAF to allow the request for your application. WAF exclusion lists allow you to omit specific request attributes from a WAF evaluation. The rest of the request is evaluated as normal. For more information about exclusion lists, see [Azure Web Application Firewall with Azure Front Door exclusion lists](waf-front-door-exclusion.md).

An exclusion list can be configured by using [Azure PowerShell](/powershell/module/az.frontdoor/New-AzFrontDoorWafManagedRuleExclusionObject), the [Azure CLI](/cli/azure/network/front-door/waf-policy/managed-rules/exclusion#az-network-front-door-waf-policy-managed-rules-exclusion-add), the [REST API](/rest/api/frontdoorservice/webapplicationfirewall/policies/createorupdate), Bicep, Azure Resource Manager templates, and the Azure portal.

## Scenario

Suppose you've created an API. Your clients send requests to your API that include headers with names like `userid` and `user-id`.

While tuning your WAF, you notice that some legitimate requests were blocked because the user headers included character sequences that the WAF detected as SQL injection attacks. Specifically, rule ID 942230 detects the request headers and blocks the requests. [Rule 942230 is part of the SQLI rule group.](waf-front-door-drs.md#drs942-20)

You decide to create an exclusion to allow these legitimate requests to pass through without the WAF blocking them.

## Create an exclusion

1. Open your Azure Front Door WAF policy.

1. Select **Managed rules** > **Manage exclusions**.

1. Select **Add**.

1. Configure the exclusion's **Applies to** section:

| Field | Value |

|-|-|

| Rule set | Microsoft_DefaultRuleSet_2.0 |

| Rule group | SQLI |

| Rule | 942230 Detects conditional SQL injection attempts |

1. Configure the exclusion match conditions:

| Field | Value |

|-|-|

| Match variable | Request header name |

| Operator | Starts with |

| Selector | User |

1. Review the exclusion, which should look like the following screenshot:

This exclusion applies to any request headers that start with the word `user`. The match condition is case insensitive, so headers that start with `User` are also covered by the exclusion. If WAF rule 942230 detects a risk in these header values, it ignores the header and moves on.

1. Select **Save**.

## Define an exclusion selector

Use the [New-AzFrontDoorWafManagedRuleExclusionObject](/powershell/module/az.frontdoor/new-azfrontdoorwafmanagedruleexclusionobject) cmdlet to define a new exclusion selector.

The following example identifies request headers that start with the word `user`. The match condition is case insensitive, so headers that start with `User` are also covered by the exclusion.

```azurepowershell

$exclusionSelector = New-AzFrontDoorWafManagedRuleExclusionObject `

-Variable RequestHeaderNames `

-Operator StartsWith `

-Selector 'user'

```

## Define a per-rule exclusion

Use the [New-AzFrontDoorWafManagedRuleOverrideObject](/powershell/module/az.frontdoor/new-azfrontdoorwafmanagedruleoverrideobject) cmdlet to define a new per-rule exclusion, which includes the selector you created in the previous step.

The following example creates an exclusion for rule ID 942230.

```azurepowershell

$exclusion = New-AzFrontDoorWafManagedRuleOverrideObject `

-RuleId '942230' `

-Exclusion $exclusionSelector

```

## Apply the exclusion to the rule group

Use the [New-AzFrontDoorWafRuleGroupOverrideObject](/powershell/module/az.frontdoor/new-azfrontdoorwafrulegroupoverrideobject) cmdlet to create a rule group override, which applies the exclusion to the appropriate rule group.

The following example uses the SQLI rule group because that group contains rule ID 942230.

```azurepowershell

$ruleGroupOverride = New-AzFrontDoorWafRuleGroupOverrideObject `

-RuleGroupName 'SQLI' `

-ManagedRuleOverride $exclusion

```

## Configure the managed rule set

Use the [New-AzFrontDoorWafManagedRuleObject](/powershell/module/az.frontdoor/new-azfrontdoorwafmanagedruleobject) cmdlet to configure the managed rule set, including the rule group override that you created in the previous step.

The following example configures the DRS 2.0 rule set with the rule group override and its exclusion.

```azurepowershell

$managedRuleSet = New-AzFrontDoorWafManagedRuleObject `

-Type 'Microsoft_DefaultRuleSet' `

-Version '2.0' `

-Action Block `

-RuleGroupOverride $ruleGroupOverride

```

## Apply the managed rule set configuration to the WAF profile

Use the [Update-AzFrontDoorWafPolicy](/powershell/module/az.frontdoor/update-azfrontdoorwafpolicy) cmdlet to update your WAF policy to include the configuration you created. Ensure that you use the correct resource group name and WAF policy name for your own environment.

```azurepowershell

Update-AzFrontDoorWafPolicy `

-ResourceGroupName 'FrontDoorWafPolicy' `

-Name 'WafPolicy'

-ManagedRule $managedRuleSet

```

## Create an exclusion

Use the [`az network front-door waf-policy managed-rules exclusion add`](/cli/azure/network/front-door/waf-policy/managed-rules/exclusion) command to update your WAF policy to add a new exclusion.

The exclusion identifies request headers that start with the word `user`. The match condition is case insensitive, so headers that start with `User` are also covered by the exclusion.

Ensure that you use the correct resource group name and WAF policy name for your own environment.

```azurecli

az network front-door waf-policy managed-rules exclusion add \

--resource-group FrontDoorWafPolicy \

--policy-name WafPolicy \

--type Microsoft_DefaultRuleSet \

--rule-group-id SQLI \

--rule-id 942230 \

--match-variable RequestHeaderNames \

--operator StartsWith \

--value user

```

## Example Bicep file

The following example Bicep file shows how to:

- Create an Azure Front Door WAF policy.

- Enable the DRS 2.0 rule set.

- Configure an exclusion for rule 942230, which exists within the SQLI rule group. This exclusion applies to any request headers that start with the word `user`. The match condition is case insensitive, so headers that start with `User` are also covered by the exclusion. If WAF rule 942230 detects a risk in these header values, it ignores the header and moves on.

```bicep

param wafPolicyName string = 'WafPolicy'

@description('The mode that the WAF should be deployed using. In "Prevention" mode, the WAF will block requests it detects as malicious. In "Detection" mode, the WAF will not block requests and will simply log the request.')

@allowed([

'Detection'

'Prevention'

])

param wafMode string = 'Prevention'

resource wafPolicy 'Microsoft.Network/frontDoorWebApplicationFirewallPolicies@2022-05-01' = {

name: wafPolicyName

location: 'Global'

sku: {

name: 'Premium_AzureFrontDoor'

}

properties: {

policySettings: {

enabledState: 'Enabled'

mode: wafMode

}

managedRules: {

managedRuleSets: [

{

ruleSetType: 'Microsoft_DefaultRuleSet'

ruleSetVersion: '2.0'

ruleSetAction: 'Block'

ruleGroupOverrides: [

{

ruleGroupName: 'SQLI'

rules: [

{

ruleId: '942230'

enabledState: 'Enabled'

action: 'AnomalyScoring'

exclusions: [

{

matchVariable: 'RequestHeaderNames'

selectorMatchOperator: 'StartsWith'

selector: 'user'

}

]

}

]

}

]

}

]

}

}

}

```

## Next steps

Learn more about [Azure Front Door](../../frontdoor/front-door-overview.md).


# Front Door Exceptions

# Azure Front Door WAF exceptions list (preview)

**Applies to:** :heavy_check_mark: Front Door Premium

The Azure Front Door Web Application Firewall (WAF) helps protect your web applications from common threats and attacks. This article describes how to configure WAF exception lists in a WAF policy associated with your Azure Front Door.

For an overview of WAF policies, see [Azure Web Application Firewall on Azure Front Door](afds-overview.md) and [WAF policy settings](waf-front-door-policy-settings.md).

In some cases, WAF might block requests that are safe and expected for your application. Exception lists allow you to bypass WAF inspection for specific requests. You can configure exceptions at the rule, rule group, or managed ruleset level.

Only the next generation of WAF engine supports exceptions, and you can use them only if your managed ruleset version is DRS 2.1, or later. For more information, see [DRS rule groups and rules](waf-front-door-drs.md).

> [!IMPORTANT]

> Exceptions in Azure Front Door Web Application Firewall (WAF) is currently in PREVIEW.

> See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Define request attributes

When you create an exception, specify which request attributes identify the traffic that should bypass WAF evaluation. Supported attributes include:

- Request URI

- Remote IP address

- Request header name and value

Match attributes either exactly or partially by using the following operators:

- **Equals:** Matches the exact value. **Example:** To select the header bearerToken, use the *Equals* operator with bearerToken as the selector.

- **Starts with:** Matches values beginning with the specified selector.

- **Ends with:** Matches values ending with the specified selector.

- **Contains:** Matches values containing the specified selector.

- **IP Match:** Matches one or more IP addresses.

## Set the exception scope

Scope exceptions to:

- A specific rule

- A rule group

- An entire managed ruleset

When you define an exception:

- Specify the rules, rule group, or managed ruleset it applies to.

- Define the request attribute that identifies the traffic to exclude.

- To exclude an entire rule group, provide the `ruleGroupName` parameter. Use the `rules` parameter only when narrowing the exception to specific rules within that group.

> [!TIP]

> Always make exceptions as narrow as possible. Broad exceptions might unintentionally expose your application to attacks. Whenever possible, use per-rule exceptions.

## Apply an exception to your WAF policy

Suppose you don't want WAF to inspect requests to `/login.php` and `/logout.php` when it evaluates SQL injection rules. Configure exceptions as follows:

1. Go to the WAF policy where you want to add exceptions.

1. Under **Settings**, select **Managed rules**.

1. In the **Exceptions** tab, select **Add exceptions**.

1. In **Applies to**, select the DRS ruleset to apply the exception to, such as *Microsoft_DefaultRuleSet_2.1*, and select the scope (**Entire ruleset**, **Rule group**, or **Specific rules**).

1. Select **Add exception** and configure the match variable, value match operator, and the values.

1. Select **Add** and then **Save** to apply the new exception.

1. Go to the **Exceptions** tab to see the new exception.

## Limitations

The following limitations apply to WAF exceptions:

- Each Azure WAF policy supports up to **60 exceptions**.

- Each Azure Front Door supports up to **60 exceptions in total**, calculated as the sum of all exceptions across the WAF policies associated with that gateway.

- Within a **single exception**, you can configure up to:

- **600 IP addresses**, or

- **10 URIs**, or

- **10 request headers**.

## Options to allow traffic through Azure WAF

Azure Web Application Firewall (WAF) provides several mechanisms to safely allow traffic when needed while maintaining protection. Depending on whether you want to bypass inspection for part of a request, or the entire request, use **Exclusions**, **Exceptions**, or **Custom rules**.

### Allow specific parts of a request using exclusions

Use **Exclusions** when you want WAF to skip inspection of a specific element within a request, such as a header, query parameter, or cookie, while still applying inspection to the rest of the request.

**Example:** If a legitimate application sends a session cookie with random characters that frequently trigger SQL Injection false positives, you can configure an exclusion for that cookie. WAF skips inspection for the cookie value but still enforces protections on the rest of the request.

### Allow entire requests by using custom rules and exceptions

To allow an entire request to bypass WAF inspection, use one of the following options:

#### Custom rule with an *Allow* action

When you configure a custom rule with the *Allow* action, the request bypasses inspection by the Default Rule Set (DRS), the Core Rule Set (CRS), and the Bot Protection ruleset.

> [!IMPORTANT]

> This bypass is absolute for these rulesets and can't be changed or selectively applied. Once the *Allow* action is triggered, none of these rulesets evaluate the request. However, the **HTTP DDoS protection ruleset** still processes the request. This ruleset ensures requests are checked for volumetric or flood-style attacks even if all other rulesets are skipped.

Use this configuration only when you fully trust the traffic source or application, since it effectively disables signature and anomaly detection.

**Example:** If you have a trusted partner API that frequently triggers DRS rules due to its payload format, you can create a custom *Allow* rule for traffic coming from the partner’s IP range. This configuration ensures the traffic is never blocked by DRS, CRS, or Bot Protection, while still benefiting from HTTP DDoS safeguards.

#### Exceptions (more granular control)

In contrast, exceptions let you bypass inspection only for specific rules, rule groups, or entire rulesets rather than disabling all of them at once.

You can apply exceptions to DRS, CRS, Bot Protection, and even the HTTP DDoS ruleset.

This approach provides fine-grained control, so you can disable inspection for one problematic rule while keeping the rest of the protections active.

**Example:** If a single DRS rule (for example *Restrict Content-Type Header*) blocks valid mobile app requests, you can create an exception for that rule only. All other DRS rules, Bot Protection, and DDoS protections continue to run on the traffic.

## Related content

- [Azure Web Application Firewall on Azure Front Door](afds-overview.md)

- [Azure Web Application Firewall DRS rule groups and rules](waf-front-door-drs.md)

- [Azure Web Application Firewall policy settings](waf-front-door-policy-settings.md)


# Http Ddos Ruleset

# HTTP DDoS Ruleset in Azure Front Door WAF (preview)

> [!IMPORTANT]

> The Microsoft HTTP DDoS Ruleset in the Azure Front Door Web Application Firewall (WAF) is currently in PREVIEW.

> See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

HTTP‑layer floods remain the most frequent driver of application availability incidents, and static controls (IP/geo filters, fixed rate limits) often can’t keep pace with distributed botnets. The new HTTP DDoS ruleset is Azure Web Application Firewall's (WAF) first automated layer 7 protection model that learns, detects, and defends with minimal user configuration. Once assigned, the ruleset continuously baselines normal traffic for each Azure Front Door profile and when surges indicate an attack, selectively blocks offending clients with no emergency tuning required.

## How the HTTP DDoS ruleset works

Once the DDoS ruleset is applied to a policy attached to an Azure Front Door Premium profile, traffic baselines are calculated using a rolling window. For profiles that have received traffic for at least 50% of the past seven days, the ruleset will calculate baselines and begins detecting spikes within 24 to 36 hours. If the Front Door profile hasn't received sufficient traffic (less than 50% of the past seven days), the ruleset won't detect or block attacks until enough traffic is present to establish reliable baselines.

Request thresholds are learned at the global profile level. If a single WAF policy configured with the HTTP DDoS ruleset is assigned to multiple Azure Front Door profiles, traffic thresholds are computed separately for each profile to which the policy is attached.

The HTTP DDoS ruleset learns both a global profile threshold and a per-IP address threshold. Until the profile threshold for requests is breached, IP-based thresholds won't trigger. Once the profile threshold is breached, IP thresholds are enforced, and any IP address that exceeds its baseline is throttled at the learned baseline rate. This approach prevents the ruleset from blocking traffic spikes from a few IP addresses unless they cause the total request rate across the profile to exceed the threshold.

Each rule in the HTTP DDoS ruleset offers three sensitivity levels, each corresponding to a different threshold. A higher sensitivity setting applies a lower threshold for that rule, while a lower sensitivity setting applies a higher threshold. The default and recommended setting is medium sensitivity.

The HTTP DDoS ruleset is the first ruleset evaluated by the Azure WAF, even before the custom rules.

> [!IMPORTANT]

> Any custom rules configured with *Allow* action won't bypass the HTTP DDoS ruleset, but will bypass all other WAF inspections.

## Ruleset rules

The HTTP DDoS ruleset currently has two rules, each configurable with different sensitivity and action settings. Each rule maintains separate traffic baselines for traffic that matches its criteria.

- **Rule 500100: Anomaly detected on high rate of client requests:** This rule tracks and establishes a baseline for all traffic on the profile to which a policy is attached. When a client exceeds the established threshold, the corresponding configured action is triggered.

- **Rule 500110: Suspected bots sending high rates of requests:** This rule allows you to set different sensitivity levels based on traffic classified as bots by Microsoft Threat Intelligence. For suspected bots, the default threshold is stricter than the default threshold for all other IP addresses. Bots classified as high risk are blocked immediately by this rule when the global profile threshold is breached.

## Monitoring the HTTP DDoS ruleset

Some monitoring capabilities are limited during the preview. The following monitoring options are currently available for the HTTP DDoS ruleset:

- When an IP address first breaches a threshold, a log entry is recorded for that IP address as a *Block* action for the HTTP DDoS ruleset, and the WAF managed rule *Match* metric is incremented.

- You can monitor the number of blocks using the Web Application Firewall *Request count* metric and filter by *Rule name*.

- The Web Application Firewall HTTPDDoSRuleset Is Active metric will have a value of "1" once the DDoS Ruleset has completed learning and is ready to take action on traffic breaching the learned threasholds.

## Limitations

The following limitations apply to the HTTP DDoS ruleset during the preview:

- There's no ability to allow traffic from specific IP addresses to bypass the DDoS ruleset or penalty box.  This capability will be addressed by an upcoming feature before the HTTP DDoS ruleset general availability.

## Related content

- [Policy settings for Azure Front Door WAF](/azure/web-application-firewall/afds/waf-front-door-policy-settings)

- [Managed rules for Azure Front Door WAF](/azure/web-application-firewall/afds/waf-front-door-drs)

- [Custom rules for Azure Front Door WAF](/azure/web-application-firewall/afds/waf-front-door-custom-rules)


# Waf Front Door Custom Rules

# Custom rules for Azure Web Application Firewall on Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Azure Web Application Firewall on Azure Front Door allows you to control access to your web applications based on the conditions you define. A custom web application firewall (WAF) rule consists of a priority number, rule type, match conditions, and an action.

There are two types of custom rules: match rules and rate limit rules. A match rule controls access based on a set of matching conditions. A rate limit rule controls access based on matching conditions and the rates of incoming requests. You can disable a custom rule to prevent it from being evaluated but still keep the configuration.

For more information on rate limiting, see [What is rate limiting for Azure Front Door?](waf-front-door-rate-limit.md)

## Priority, action types, and match conditions

You can control access with a custom WAF rule that defines a priority number, a rule type, an array of match conditions, and an action.

- **Priority**

A unique integer that describes the order of evaluation of WAF rules. Rules with lower-priority values are evaluated before rules with higher values. The rule evaluation stops on any rule action except for *Log*. Priority numbers must be unique among all custom rules.

- **Action**

Defines how to route a request if a WAF rule is matched. You can choose one of the following actions to apply when a request matches a custom rule.

- **Allow**: The WAF allows the request to process, logs an entry in WAF logs, and exits.

- **Block**: Request is blocked. The WAF sends a response to a client without forwarding the request further. The WAF logs an entry in WAF logs and exits.

- **Log**: The WAF logs an entry in WAF logs and continues to evaluate the next rule in the priority order.

- **Redirect**: The WAF redirects the request to a specified URI, logs an entry in WAF logs, and exits.

- **Match condition**

Defines a match variable, an operator, and a match value. Each rule can contain multiple match conditions. A match condition might be based on geo-location, client IP addresses (CIDR), size, AS Number, Client Fingerprint, Service Tag, or string match. String match can be against a list of match variables.

- **Match variable**

- RequestMethod

- QueryString

- PostArgs

- RequestUri

- RequestHeader

- RequestBody

- Cookies

- **Operator**

- Any: Often used to define default action if no rules are matched. Any is a match all operator.

- Equal

- Contains

- LessThan: Size constraint

- GreaterThan: Size constraint

- LessThanOrEqual: Size constraint

- GreaterThanOrEqual: Size constraint

- BeginsWith

- EndsWith

- Regex

- **Regex**

Doesn't support the following operations:

- Backreferences and capturing subexpressions

- Arbitrary zero-width assertions

- Subroutine references and recursive patterns

- Conditional patterns

- Backtracking control verbs

- The \C single-byte directive

- The \R newline match directive

- The \K start of match reset directive

- Callouts and embedded code

- Atomic grouping and possessive quantifiers

- **Negate [optional]**

You can set the `negate` condition to *true* if the result of a condition should be negated.

- **Transform [optional]**

A list of strings with names of transformations to do before the match is attempted. These can be the following transformations:

- Uppercase

- Lowercase

- Trim

- RemoveNulls

- UrlDecode

- UrlEncode

- **Match value**

Supported HTTP request method values include:

- GET

- POST

- PUT

- HEAD

- DELETE

- LOCK

- UNLOCK

- PROFILE

- OPTIONS

- PROPFIND

- PROPPATCH

- MKCOL

- COPY

- MOVE

- PATCH

- CONNECT

## Examples

Consider the following examples.

### Match based on HTTP request parameters

Suppose you need to configure a custom rule to allow requests that match the following two conditions:

- The `Referer` header's value is equal to a known value.

- The query string doesn't contain the word `password`.

Here's an example JSON description of the custom rule:

```json

{

"name": "AllowFromTrustedSites",

"priority": 1,

"ruleType": "MatchRule",

"matchConditions": [

{

"matchVariable": "RequestHeader",

"selector": "Referer",

"operator": "Equal",

"negateCondition": false,

"matchValue": [

"www.mytrustedsites.com/referpage.html"

]

},

{

"matchVariable": "QueryString",

"operator": "Contains",

"matchValue": [

"password"

],

"negateCondition": true

}

],

"action": "Allow"

}

```

### Block HTTP PUT requests

Suppose you need to block any request that uses the HTTP PUT method.

Here's an example JSON description of the custom rule:

``` json

{

"name": "BlockPUT",

"priority": 2,

"ruleType": "MatchRule",

"matchConditions": [

{

"matchVariable": "RequestMethod",

"selector": null,

"operator": "Equal",

"negateCondition": false,

"matchValue": [

"PUT"

]

}

],

"action": "Block"

}

```

### Size constraint

An Azure Front Door WAF enables you to build custom rules that apply a length or size constraint on a part of an incoming request. This size constraint is measured in bytes.

Suppose you need to block requests where the URL is longer than 100 characters.

Here's an example JSON description of the custom rule:

```json

{

"name": "URLOver100",

"priority": 5,

"ruleType": "MatchRule",

"matchConditions": [

{

"matchVariable": "RequestUri",

"selector": null,

"operator": "GreaterThanOrEqual",

"negateCondition": false,

"matchValue": [

"100"

]

}

],

"action": "Block"

}

```

### Match based on request URI

Suppose you need to allow requests where the URI contains 'login'.

Here's an example JSON description of the custom rule:

```json

{

"name": "URIContainsLogin",

"priority": 5,

"ruleType": "MatchRule",

"matchConditions": [

{

"matchVariable": "RequestUri",

"selector": null,

"operator": "Contains",

"negateCondition": false,

"matchValue": [

"login"

]

}

],

"action": "Allow"

}

```

## Copying and duplicating custom rules

Custom rules can be duplicated within a given policy. When duplicating a rule, you need to specify a unique name for the rule and a unique priority value. Additionally, custom rules can be copied from one Azure Front Door WAF policy to another as long as the policies are both in the same subscription. When copying a rule from one policy to another, you need to select the Azure Front Door WAF policy you wish to copy the rule into. Once you select the WAF policy you need to give the rule a unique name, and assign a priority rank.

## Related content

- [Configure a WAF policy by using Azure PowerShell](waf-front-door-custom-rules-powershell.md)

- [Azure Web Application Firewall on Azure Front Door](afds-overview.md)

- [Create an Azure Front Door instance](../../frontdoor/quickstart-create-front-door.md)


# Waf Front Door Rate Limit

# What is rate limiting for Azure Front Door?

**Applies to:** :heavy_check_mark: Front Door Standard/Premium :heavy_check_mark: Front Door (classic)

Rate limiting enables you to detect and block abnormally high levels of traffic from any socket IP address. By using Azure Web Application Firewall in Azure Front Door, you can mitigate some types of denial-of-service attacks. Rate limiting also protects you against clients that were accidentally misconfigured to send large volumes of requests in a short time period.

The socket IP address is the address of the client that initiated the TCP connection to Azure Front Door. Typically, the socket IP address is the IP address of the user, but it might also be the IP address of a proxy server or another device that sits between the user and Azure Front Door. If you have multiple clients that access Azure Front Door from different socket IP addresses, they each have their own rate limits applied.

## Configure a rate limit policy

Rate limiting is configured by using [custom WAF rules](./waf-front-door-custom-rules.md).

When you configure a rate limit rule, you specify the *threshold*. The threshold is the number of web requests that are allowed from each socket IP address within a time period of either one minute or five minutes.

You also must specify at least one *match condition*, which tells Azure Front Door when to activate the rate limit. You can configure multiple rate limits that apply to different paths within your application.

If you need to apply a rate limit rule to all your requests, consider using a match condition like the following example:

The preceding match condition identifies all requests with a `Host` header of a length greater than `0`. Because all valid HTTP requests for Azure Front Door contain a `Host` header, this match condition has the effect of matching all HTTP requests.

## Rate limits and Azure Front Door servers

Requests from the same client often arrive at the same Azure Front Door server. In that case, you see requests are blocked as soon as the rate limit is reached for each of the client IP addresses.

It's possible that requests from the same client might arrive at a different Azure Front Door server that hasn't refreshed the rate limit counters yet. For example, the client might open a new TCP connection for each request, and each TCP connection could be routed to a different Azure Front Door server.

If the threshold is low enough, the first request to the new Azure Front Door server could pass the rate limit check. So, for a low threshold (for example, less than about 200 requests per minute), you might see some requests above the threshold get through.

A few considerations to keep in mind while you determine threshold values and time windows for rate limiting:

- A larger window size with the smallest acceptable request count threshold is the most effective configuration for preventing DDoS attacks. This configuration is more effective because when an attacker reaches the threshold they're blocked for the remainder of the rate limit window. Therefore, if an attacker is blocked in the first 30 seconds of a one-minute window, they're only rate limited for the remaining 30 seconds. If an attacker is blocked in the first minute of a five-minute window, they're rate limited for the remaining four minutes.

- Setting larger time window sizes (for example, five minutes over one minute) and larger threshold values (for example, 200 over 100) tend to be more accurate in enforcing close to rate limit's thresholds than using the shorter time window sizes and lower threshold values.

- Azure Front Door WAF rate limiting operates on a fixed time period. Once a rate limit threshold is breached, all traffic matching that rate limiting rule is blocked for the remainder of the fixed window.

## Related content

- [Configure rate limiting on your Azure Front Door WAF](waf-front-door-rate-limit-configure.md).

- [Rate limiting best practices](waf-front-door-best-practices.md#rate-limiting-best-practices).


# Waf Front Door Geo Filtering

# What is geo-filtering on a domain for Azure Front Door?

**Applies to:** :heavy_check_mark: Front Door Standard/Premium :heavy_check_mark: Front Door (classic)

By default, Azure Front Door responds to all user requests regardless of the location where the request comes from. In some scenarios, you might want to restrict access to your web application by countries or regions. You can use Azure Web Application Firewall in Azure Front Door to define a policy by using custom access rules for a specific path on your endpoint to allow or block access from specified countries or regions.

A web application firewall (WAF) policy contains a set of custom rules. The rule consists of match conditions, an action, and a priority. In a match condition, you define a match variable, operator, and match value.

For a geo-filtering rule, the match variable is either `RemoteAddr` or `SocketAddr`. The `RemoteAddr` variable is the original client IP that's usually sent via the `X-Forwarded-For` request header. `SocketAddr` is the source IP address WAF sees. If your user is behind a proxy, the `SocketAddr` variable is usually the IP address of the proxy server.

The operator for this geo-filtering rule is `GeoMatch`. The value is a two-letter country or region code of interest. The `ZZ` country code or `Unknown` country/region captures IP addresses that aren't yet mapped to a country or region in our dataset. You can add `ZZ` to your match condition to avoid false positives. You can combine a `GeoMatch` condition and a `REQUEST_URI` string match condition to create a path-based geo-filtering rule.

You can configure a geo-filtering policy for your Azure Front Door instance by using [Azure PowerShell](../../frontdoor/front-door-tutorial-geo-filtering.md) or a [Bicep file or Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/blob/master/quickstarts/microsoft.cdn/front-door-standard-premium-geo-filtering/).

> [!IMPORTANT]

> Include the country code `ZZ` whenever you use geo-filtering. The `ZZ` country code (or `Unknown` country/region) captures IP addresses that aren't yet mapped to a country or region in our dataset. Use this code to avoid false positives.

> [!Note]

> You can only include a maximum of ten country/region codes in a single custom rule.

## Country/Region code reference

|Country/Region code | Country/Region name |

| ----- | ----- |

| AD | Andorra|

| AE | United Arab Emirates|

| AF | Afghanistan|

| AG | Antigua and Barbuda|

| AI | Anguilla|

| AL | Albania|

| AM | Armenia|

| AO | Angola|

| AQ | Antarctica|

| AR | Argentina|

| AS | American Samoa|

| AT | Austria|

| AU | Australia|

| AW | Aruba|

| AX | Åland Islands|

| AZ | Azerbaijan|

| BA | Bosnia and Herzegovina|

| BB | Barbados|

| BD | Bangladesh|

| BE | Belgium|

| BF | Burkina Faso|

| BG | Bulgaria|

| BH | Bahrain|

| BI | Burundi|

| BJ | Benin|

| BL | Saint Barthélemy|

| BM | Bermuda|

| BN | Brunei|

| BO | Bolivia|

| BQ | Bonaire, Sint Eustatius and Saba|

| BR | Brazil|

| BS | Bahamas|

| BT | Bhutan|

| BV | Bouvet Island|

| BW | Botswana|

| BY | Belarus|

| BZ | Belize|

| CA | Canada|

| CC | Cocos (Keeling) Islands|

| CD | Congo (DRC)|

| CF | Central African Republic|

| CG | Congo|

| CH | Switzerland|

| CI | Côte d'Ivoire|

| CK | Cook Islands|

| CL | Chile|

| CM | Cameroon|

| CN | China|

| CO | Colombia|

| CR | Costa Rica|

| CU | Cuba|

| CV | Cabo Verde|

| CW | Curaçao|

| CX | Christmas Island|

| CY | Cyprus|

| CZ | Czechia|

| DE | Germany|

| DJ | Djibouti|

| DK | Denmark|

| DM | Dominica|

| DO | Dominican Republic|

| DZ | Algeria|

| EC | Ecuador|

| EE | Estonia|

| EG | Egypt|

| ER | Eritrea|

| ES | Spain|

| ET | Ethiopia|

| FI | Finland|

| FJ | Fiji|

| FK | Falkland Islands|

| FM | Micronesia|

| FO | Faroe Islands|

| FR | France|

| GA | Gabon|

| GB | United Kingdom|

| GD | Grenada|

| GE | Georgia|

| GF | French Guiana|

| GG | Guernsey|

| GH | Ghana|

| GI | Gibraltar|

| GL | Greenland|

| GM | Gambia|

| GN | Guinea|

| GP | Guadeloupe|

| GQ | Equatorial Guinea|

| GR | Greece|

| GS | South Georgia and South Sandwich Islands|

| GT | Guatemala|

| GU | Guam|

| GW | Guinea-Bissau|

| GY | Guyana|

| HK | Hong Kong SAR|

| HM | Heard Island and McDonald Islands|

| HN | Honduras|

| HR | Croatia|

| HT | Haiti|

| HU | Hungary|

| ID | Indonesia|

| IE | Ireland|

| IL | Israel|

| IM | Isle of Man|

| IN | India|

| IO | British Indian Ocean Territory|

| IQ | Iraq|

| IR | Iran|

| IS | Iceland|

| IT | Italy|

| JE | Jersey|

| JM | Jamaica|

| JO | Jordan|

| JP | Japan|

| KE | Kenya|

| KG | Kyrgyzstan|

| KH | Cambodia|

| KI | Kiribati|

| KM | Comoros|

| KN | Saint Kitts and Nevis|

| KP | North Korea|

| KR | Korea|

| KW | Kuwait|

| KY | Cayman Islands|

| KZ | Kazakhstan|

| LA | Laos|

| LB | Lebanon|

| LC | Saint Lucia|

| LI | Liechtenstein|

| LK | Sri Lanka|

| LR | Liberia|

| LS | Lesotho|

| LT | Lithuania|

| LU | Luxembourg|

| LV | Latvia|

| LY | Libya|

| MA | Morocco|

| MC | Monaco|

| MD | Moldova|

| ME | Montenegro|

| MF | Saint Martin|

| MG | Madagascar|

| MH | Marshall Islands|

| MK | North Macedonia|

| ML | Mali|

| MM | Myanmar|

| MN | Mongolia|

| MO | Macao SAR|

| MP | Northern Mariana Islands|

| MQ | Martinique|

| MR | Mauritania|

| MS | Montserrat|

| MT | Malta|

| MU | Mauritius|

| MV | Maldives|

| MW | Malawi|

| MX | Mexico|

| MY | Malaysia|

| MZ | Mozambique|

| NA | Namibia|

| NC | New Caledonia|

| NE | Niger|

| NF | Norfolk Island|

| NG | Nigeria|

| NI | Nicaragua|

| NL | Netherlands|

| NO | Norway|

| NP | Nepal|

| NR | Nauru|

| NU | Niue|

| NZ | New Zealand|

| OM | Oman|

| PA | Panama|

| PE | Peru|

| PF | French Polynesia|

| PG | Papua New Guinea|

| PH | Philippines|

| PK | Pakistan|

| PL | Poland|

| PM | Saint Pierre and Miquelon|

| PN | Pitcairn Islands|

| PR | Puerto Rico|

| PS | Palestinian Authority|

| PT | Portugal|

| PW | Palau|

| PY | Paraguay|

| QA | Qatar|

| RE | Réunion|

| RO | Romania|

| RS | Serbia|

| RU | Russia|

| RW | Rwanda|

| SA | Saudi Arabia|

| SB | Solomon Islands|

| SC | Seychelles|

| SD | Sudan|

| SE | Sweden|

| SG | Singapore|

| SH | St Helena, Ascension, Tristan da Cunha|

| SI | Slovenia|

| SJ | Svalbard and Jan Mayen|

| SK | Slovakia|

| SL | Sierra Leone|

| SM | San Marino|

| SN | Senegal|

| SO | Somalia|

| SR | Suriname|

| SS | South Sudan|

| ST | São Tomé and Príncipe|

| SV | El Salvador|

| SX | Sint Maarten|

| SY | Syria|

| SZ | Eswatini|

| TC | Turks and Caicos Islands|

| TD | Chad|

| TF | French Southern Territories|

| TG | Togo|

| TH | Thailand|

| TJ | Tajikistan|

| TK | Tokelau|

| TL | Timor-Leste|

| TM | Turkmenistan|

| TN | Tunisia|

| TO | Tonga|

| TR | Türkiye|

| TT | Trinidad and Tobago|

| TV | Tuvalu|

| TW | Taiwan|

| TZ | Tanzania|

| UA | Ukraine|

| UG | Uganda|

| UM | U.S. Outlying Islands|

| US | United States|

| UY | Uruguay|

| UZ | Uzbekistan|

| VA | Vatican City|

| VC | Saint Vincent and the Grenadines|

| VE | Venezuela|

| VG | British Virgin Islands|

| VI | U.S. Virgin Islands|

| VN | Vietnam|

| VU | Vanuatu|

| WF | Wallis and Futuna|

| WS | Samoa|

| XK | Kosovo|

| YE | Yemen|

| YT | Mayotte|

| ZA | South Africa|

| ZM | Zambia|

| ZW | Zimbabwe|

## Next steps

- Learn about [application layer security with Azure Front Door](../../frontdoor/front-door-application-security.md).

- Learn how to [create an instance of Azure Front Door](../../frontdoor/quickstart-create-front-door.md).


# Waf Front Door Rate Limit Configure

# Configure a Web Application Firewall rate-limit rule

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

The Azure Web Application Firewall rate-limit rule for Azure Front Door controls the number of requests allowed from a particular source IP address to the application during a rate-limit duration. For more information about rate limiting, see [What is rate limiting for Azure Front Door?](waf-front-door-rate-limit.md)

This article shows how to configure a web application firewall (WAF) rate-limit rule on Azure Front Door Standard and Premium tiers.

## Scenario

Suppose you're responsible for a public website. You've just added a page with information about a promotion your organization is running. You're concerned that if clients visit that page too often, some of your back-end services might not scale quickly and the application might have performance issues.

You decide to create a rate-limit rule that restricts each source IP address to a maximum of 1,000 requests per minute. You only apply this rule to requests that contain `*/promo*` in the request URL.

> [!TIP]

> If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Create an Azure Front Door profile and WAF policy

1. In the Azure portal, select **Create a resource**.

1. Search for **Front Door**, and select **Front Door and CDN profiles**.

1. Select **Create**.

1. Select **Continue to create a Front Door** to use the *quick create* portal creation process.

1. Enter the information required on the **Basics** page:

- **Resource group**: Select an existing resource group, or create a new resource group for the Azure Front Door and WAF resources.

- **Name**: Enter the name of your Azure Front Door profile.

- **Tier**: Select **Standard** or **Premium**. For this scenario, both tiers support rate limiting.

- **Endpoint name**: Provide a unique name for your endpoint because Azure Front Door endpoints must have globally unique names.

- **Origin type** and **Origin host name**: Select the origin application that you want to protect with your rate-limit rule.

1. Next to **WAF policy**, select **Create new**.

1. Enter the name of a WAF policy and select **Create**.

1. Select **Review + create** > **Create**.

1. After the deployment is finished, select **Go to resource**.

## Create a rate-limit rule

1. Select **Custom rules** > **Add custom rule**.

1. Enter the information required to create a rate-limit rule:

- **Custom rule name**: Enter the name of the custom rule, such as **rateLimitRule**.

- **Rule type**: Select **Rate limit**.

- **Priority**: Enter the priority of the rule, such as **1**.

- **Rate limit duration**: Select **1 minute**.

- **Rate limit threshold (requests)**: Enter **1000**.

1. In **Conditions**, enter the information required to specify a match condition to identify requests where the URL contains the string `*/promo*`:

- **Match type**: Select **String**.

- **Match variable**: Enter **RequestUri**.

- **Operation**: Select **is**.

- **Operator**: Select **Contains**.

- **Match values**: Enter **/promo**.

1. For **Action**, select **Log** or **Block**.

Rate-limit rules only support `Log` and `Block` actions. `Allow` isn't supported.

1. Select **Add**.

1. Select **Save**.

## Use prevention mode on the WAF

By default, the Azure portal creates WAF policies in detection mode. This setting means that the WAF doesn't block requests. For more information, see [WAF modes](afds-overview.md#waf-modes).

[Tune your WAF](waf-front-door-tuning.md) before you use prevention mode. Tuning helps to avoid false positive detections. It also helps to prevent your WAF from blocking legitimate requests.

Here you reconfigure the WAF to use prevention mode.

1. Open the WAF policy.

Notice that **Policy mode** is set at **Detection**.

1. Select **Switch to prevention mode**.

## Prerequisites

Before you begin to set up a rate-limit policy, set up your PowerShell environment and create an Azure Front Door profile.

### Set up your PowerShell environment

Azure PowerShell provides a set of cmdlets that use the [Azure Resource Manager](../../azure-resource-manager/management/overview.md) model for managing your Azure resources.

You can install [Azure PowerShell](/powershell/azure/) on your local machine and use it in any PowerShell session. Here you sign in with your Azure credentials and install the Azure PowerShell module for Azure Front Door Standard or Premium.

#### Connect to Azure with an interactive dialog for sign-in

Sign in to Azure by running the following command:

```azurepowershell

Connect-AzAccount

```

#### Install PowerShellGet

Ensure that the current version of [PowerShellGet](/powershell/gallery/powershellget/overview) is installed. Run the following command:

```azurepowershell

Install-Module PowerShellGet -Force -AllowClobber

```

Then, restart PowerShell to ensure that you use the latest version.

#### Install the Azure Front Door PowerShell modules

Install the `Az.FrontDoor` and `Az.Cdn` PowerShell modules to work with Azure Front Door Standard or Premium from PowerShell.

```azurepowershell

Install-Module -Name Az.FrontDoor

Install-Module -Name Az.Cdn

```

You use the `Az.Cdn` module to work with Azure Front Door Standard or Premium resources. Use the `Az.FrontDoor` module to work with WAF resources.

### Create a resource group

Use the [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup) cmdlet to create a new resource group for your Azure Front Door profile and WAF policy. Update the resource group name and location for your own requirements:

```azurepowershell

$resourceGroupName = 'FrontDoorRateLimit'

New-AzResourceGroup -Name $resourceGroupName -Location 'westus'

```

### Create an Azure Front Door profile

Use the [New-AzFrontDoorCdnProfile](/powershell/module/az.cdn/new-azfrontdoorcdnprofile) cmdlet to create a new Azure Front Door profile.

In this example, you create an Azure Front Door standard profile named `MyFrontDoorProfile`:

```azurepowershell

$frontDoorProfile = New-AzFrontDoorCdnProfile `

-Name 'MyFrontDoorProfile' `

-ResourceGroupName $resourceGroupName `

-Location global `

-SkuName Standard_AzureFrontDoor

```

### Create an Azure Front Door endpoint

Use the [New-AzFrontDoorCdnEndpoint](/powershell/module/az.cdn/new-azfrontdoorcdnendpoint) cmdlet to add an endpoint to your Azure Front Door profile.

Azure Front Door endpoints must have globally unique names, so update the value of the `$frontDoorEndpointName` variable to something unique.

```azurepowershell

$frontDoorEndpointName = '<unique-front-door-endpoint-name>'

$frontDoorEndpoint = New-AzFrontDoorCdnEndpoint `

-EndpointName $frontDoorEndpointName `

-ProfileName $frontDoorProfile.Name `

-ResourceGroupName $frontDoorProfile.ResourceGroupName `

-Location $frontDoorProfile.Location

```

## Define a URL match condition

Use the [New-AzFrontDoorWafMatchConditionObject](/powershell/module/az.frontdoor/new-azfrontdoorwafmatchconditionobject) cmdlet to create a match condition to identify requests that should have the rate limit applied.

The following example matches requests where the `RequestUri` variable contains the string */promo*:

```azurepowershell

$promoMatchCondition = New-AzFrontDoorWafMatchConditionObject `

-MatchVariable RequestUri `

-OperatorProperty Contains `

-MatchValue '/promo'

```

## Create a custom rate-limit rule

Use the [New-AzFrontDoorWafCustomRuleObject](/powershell/module/az.frontdoor/new-azfrontdoorwafcustomruleobject) cmdlet to create the rate-limit rule, which includes the match condition you defined in the previous step and the request threshold.

The following example sets the limit to `1000`:

```azurepowershell

$promoRateLimitRule = New-AzFrontDoorWafCustomRuleObject `

-Name 'rateLimitRule' `

-RuleType RateLimitRule `

-MatchCondition $promoMatchCondition `

-RateLimitThreshold 1000 `

-Action Block `

-Priority 1

```

When any source IP address sends more than 1,000 requests within one minute, the WAF blocks subsequent requests until the next minute starts.

## Create a WAF policy

Use the [New-AzFrontDoorWafPolicy](/powershell/module/az.frontdoor/new-azfrontdoorwafpolicy) cmdlet to create a WAF policy, which includes the custom rule you created.

```azurepowershell

$wafPolicy = New-AzFrontDoorWafPolicy `

-Name 'MyWafPolicy' `

-ResourceGroupName $frontDoorProfile.ResourceGroupName `

-Sku Standard_AzureFrontDoor `

-CustomRule $promoRateLimitRule

```

## Configure a security policy to associate your Azure Front Door profile with your WAF policy

Use the [New-AzFrontDoorCdnSecurityPolicy](/powershell/module/az.cdn/new-azfrontdoorcdnsecuritypolicy) cmdlet to create a security policy for your Azure Front Door profile. A security policy associates your WAF policy with domains that you want to be protected by the WAF rule.

In this example, you associate the endpoint's default hostname with your WAF policy:

```azurepowershell

$securityPolicyAssociation = New-AzFrontDoorCdnSecurityPolicyWebApplicationFirewallAssociationObject `

-PatternsToMatch @("/*") `

-Domain @(@{"Id"=$($frontDoorEndpoint.Id)})

$securityPolicyParameters = New-AzFrontDoorCdnSecurityPolicyWebApplicationFirewallParametersObject `

-Association $securityPolicyAssociation `

-WafPolicyId $wafPolicy.Id

$frontDoorSecurityPolicy = New-AzFrontDoorCdnSecurityPolicy `

-Name 'MySecurityPolicy' `

-ProfileName $frontDoorProfile.Name `

-ResourceGroupName $frontDoorProfile.ResourceGroupName `

-Parameter $securityPolicyParameters

```

## Prerequisites

Before you begin to set up a rate-limit policy, set up your Azure CLI environment and create an Azure Front Door profile.

### Set up your Azure CLI environment

The Azure CLI provides a set of commands that use the [Azure Resource Manager](../../azure-resource-manager/management/overview.md) model for managing your Azure resources.

You can install the [Azure CLI](/cli/azure/install-azure-cli) on your local machine and use it in any shell session. Here you sign in with your Azure credentials and install the Azure CLI extension for Azure Front Door Standard or Premium.

#### Connect to Azure with an interactive dialog for sign-in

Sign in to Azure by running the following command:

```azurecli

az login

```

#### Install the Azure Front Door extension for the Azure CLI

Install the `front-door` extension to work with the Azure Front Door WAF from the Azure CLI:

```azurecli

az extension add --name front-door

```

You use the `az afd` commands to work with Azure Front Door Standard or Premium resources. Use the `az network front-door waf-policy` commands to work with WAF resources.

### Create a resource group

Use the [az group create](/cli/azure/group#az-group-create) command to create a new resource group for your Azure Front Door profile and WAF policy. Update the resource group name and location for your own requirements:

```azurecli

resourceGroupName='FrontDoorRateLimit'

az group create \

--name $resourceGroupName \

--location westus

```

## Create an Azure Front Door profile

Use the [az afd profile create](/cli/azure/afd/profile#az-afd-profile-create) command to create a new Azure Front Door profile.

In this example, you create an Azure Front Door standard profile named `MyFrontDoorProfile`:

```azurecli

frontDoorProfileName='MyFrontDoorProfile'

az afd profile create \

--profile-name $frontDoorProfileName \

--resource-group $resourceGroupName \

--sku Standard_AzureFrontDoor

```

### Create an Azure Front Door endpoint

Use the [az afd endpoint create](/cli/azure/afd/endpoint#az-afd-endpoint-create) command to add an endpoint to your Azure Front Door profile.

Azure Front Door endpoints must have globally unique names, so update the value of the `frontDoorEndpointName` variable to something unique.

```azurecli

frontDoorEndpointName='<unique-front-door-endpoint-name>'

az afd endpoint create \

--endpoint-name $frontDoorEndpointName \

--profile-name $frontDoorProfileName \

--resource-group $resourceGroupName \

```

## Create a WAF policy

Use the [az network front-door waf-policy create](/cli/azure/network/front-door/waf-policy#az-network-front-door-waf-policy-create) command to create a WAF policy:

```azurecli

wafPolicyName='MyWafPolicy'

az network front-door waf-policy create \

--name $wafPolicyName \

--resource-group $resourceGroupName \

--sku Standard_AzureFrontDoor

```

## Prepare to add a custom rate-limit rule

Use the [az network front-door waf-policy rule create](/cli/azure/network/front-door/waf-policy/rule#az-network-front-door-waf-policy-rule-create) command to create a custom rate-limit rule. The following example sets the limit to 1,000 requests per minute.

Rate-limit rules must contain a match condition, which you create in the next step. In this command, you include the `--defer` argument, which tells the Azure CLI not to submit the rule to Azure yet.

```azurecli

az network front-door waf-policy rule create \

--name rateLimitRule \

--policy-name $wafPolicyName \

--resource-group $resourceGroupName \

--rule-type RateLimitRule \

--rate-limit-duration 1 \

--rate-limit-threshold 1000 \

--action Block \

--priority 1 \

--defer

```

When any source IP address sends more than 1,000 requests within one minute, the WAF blocks subsequent requests until the next minute starts.

## Add a match condition

Use the [az network front-door waf-policy rule match-condition add](/cli/azure/network/front-door/waf-policy/rule/match-condition#az-network-front-door-waf-policy-rule-match-condition-add) command to add a match condition to your custom rule. The match condition identifies requests that should have the rate limit applied.

The following example matches requests where the `RequestUri` variable contains the string */promo*:

```azurecli

az network front-door waf-policy rule match-condition add \

--match-variable RequestUri \

--operator Contains \

--values '/promo' \

--name rateLimitRule \

--policy-name $wafPolicyName \

--resource-group $resourceGroupName

```

When you submit this command, the Azure CLI creates the rate-limit rule and match condition together.

## Configure a security policy to associate your Azure Front Door profile with your WAF policy

Use the [az afd security-policy create](/cli/azure/afd/security-policy#az-afd-security-policy-create) command to create a security policy for your Azure Front Door profile. A security policy associates your WAF policy with domains that you want to be protected by the WAF rule.

In this example, you associate the endpoint's default hostname with your WAF policy:

```azurecli

securityPolicyName='MySecurityPolicy'

wafPolicyResourceId=$(az network front-door waf-policy show --name $wafPolicyName --resource-group $resourceGroupName --query id --output tsv)

frontDoorEndpointResourceId=$(az afd endpoint show --endpoint-name $frontDoorEndpointName --profile-name $frontDoorProfileName --resource-group $resourceGroupName --query id --output tsv)

az afd security-policy create \

--security-policy-name $securityPolicyName \

--profile-name $frontDoorProfileName \

--resource-group $resourceGroupName \

--domains $frontDoorEndpointResourceId \

--waf-policy $wafPolicyResourceId

```

The preceding code looks up the Azure resource identifiers for the WAF policy and Azure Front Door endpoint so that it can associate them with your security policy.

> [!NOTE]

> Whenever you make changes to your WAF policy, you don't need to re-create the Azure Front Door security policy. WAF policy updates are automatically applied to the Azure Front Door domains.

## Quickstart

To create an Azure Front Door profile with a rate-limit rule by using Bicep, see the [Azure Front Door Standard or Premium with rate limit](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium-rate-limit/) Bicep quickstart.

## Next steps

Learn more about [Azure Front Door](../../frontdoor/front-door-overview.md).


# Waf Front Door Tutorial Geo Filtering

# Set up a geo-filtering WAF policy for Azure Front Door

This tutorial shows how to use Azure PowerShell to create a sample geo-filtering policy and associate the policy with your existing Azure Front Door front-end host. This sample geo-filtering policy blocks requests from all other countries or regions except the United States.

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) now.

## Prerequisites

Before you begin to set up a geo-filter policy, set up your PowerShell environment and create an Azure Front Door profile.

### Set up your PowerShell environment

Azure PowerShell provides a set of cmdlets that use the [Azure Resource Manager](../../azure-resource-manager/management/overview.md) model for managing your Azure resources.

You can install [Azure PowerShell](/powershell/azure/) on your local machine and use it in any PowerShell session. Follow the instructions on the page to sign in with your Azure credentials. Then install the Az PowerShell module.

#### Connect to Azure with an interactive dialog for sign-in

```

Install-Module -Name Az

Connect-AzAccount

```

Make sure you have the current version of PowerShellGet installed. Run the following command and reopen PowerShell.

```

Install-Module PowerShellGet -Force -AllowClobber

```

#### Install the Az.FrontDoor module

```

Install-Module -Name Az.FrontDoor

```

### Create an Azure Front Door profile

Create an Azure Front Door profile by following the instructions described in [Quickstart: Create an Azure Front Door profile](../../frontdoor/quickstart-create-front-door.md).

## Define a geo-filtering match condition

Create a sample match condition that selects requests not coming from "US" by using [New-AzFrontDoorWafMatchConditionObject](/powershell/module/az.frontdoor/new-azfrontdoorwafmatchconditionobject) on parameters when you create a match condition.

Two-letter country or region codes to country or region mapping are provided in [What is geo-filtering on a domain for Azure Front Door?](waf-front-door-geo-filtering.md)

```azurepowershell-interactive

$nonUSGeoMatchCondition = New-AzFrontDoorWafMatchConditionObject `

-MatchVariable SocketAddr `

-OperatorProperty GeoMatch `

-NegateCondition $true `

-MatchValue "US"

```

## Add a geo-filtering match condition to a rule with an action and a priority

Create a `CustomRule` object `nonUSBlockRule` based on the match condition, an action, and a priority by using [New-AzFrontDoorWafCustomRuleObject](/powershell/module/az.frontdoor/new-azfrontdoorwafcustomruleobject). A custom rule can have multiple match conditions. In this example, `Action` is set to `Block`. `Priority` is set to `1`, which is the highest priority.

```

$nonUSBlockRule = New-AzFrontDoorWafCustomRuleObject `

-Name "geoFilterRule" `

-RuleType MatchRule `

-MatchCondition $nonUSGeoMatchCondition `

-Action Block `

-Priority 1

```

## Add rules to a policy

Find the name of the resource group that contains the Azure Front Door profile by using `Get-AzResourceGroup`. Next, create a `geoPolicy` object that contains `nonUSBlockRule` by using [New-AzFrontDoorWafPolicy](/powershell/module/az.frontdoor/new-azfrontdoorwafpolicy) in the specified resource group that contains the Azure Front Door profile. You must provide a unique name for the geo policy.

The following example uses the resource group name `myResourceGroupFD1` with the assumption that you've created the Azure Front Door profile by using instructions provided in [Quickstart: Create an Azure Front Door](../../frontdoor/quickstart-create-front-door.md). In the following example, replace the policy name `geoPolicyAllowUSOnly` with a unique policy name.

```

$geoPolicy = New-AzFrontDoorWafPolicy `

-Name "geoPolicyAllowUSOnly" `

-resourceGroupName myResourceGroupFD1 `

-Customrule $nonUSBlockRule  `

-Mode Prevention `

-EnabledState Enabled

```

## Link a WAF policy to an Azure Front Door front-end host

Link the WAF policy object to the existing Azure Front Door front-end host. Update Azure Front Door properties.

To do so, first retrieve your Azure Front Door object by using [Get-AzFrontDoor](/powershell/module/az.frontdoor/get-azfrontdoor).

```

$geoFrontDoorObjectExample = Get-AzFrontDoor -ResourceGroupName myResourceGroupFD1

$geoFrontDoorObjectExample[0].FrontendEndpoints[0].WebApplicationFirewallPolicyLink = $geoPolicy.Id

```

Next, set the front-end `WebApplicationFirewallPolicyLink` property to the resource ID of the geo policy by using [Set-AzFrontDoor](/powershell/module/az.frontdoor/set-azfrontdoor).

```

Set-AzFrontDoor -InputObject $geoFrontDoorObjectExample[0]

```

> [!NOTE]

> You only need to set the `WebApplicationFirewallPolicyLink` property once to link a WAF policy to an Azure Front Door front-end host. Subsequent policy updates are automatically applied to the front-end host.

## Next steps

- Learn about [Azure Web Application Firewall](../overview.md).

- Learn how to [create an instance of Azure Front Door](../../frontdoor/quickstart-create-front-door.md).


# Waf Front Door Configure Ip Restriction

# Configure an IP restriction rule with a WAF for Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

This article shows you how to configure IP restriction rules in a web application firewall (WAF) for Azure Front Door by using the Azure portal, the Azure CLI, Azure PowerShell, or an Azure Resource Manager template.

An IP address–based access control rule is a custom WAF rule that you use to control access to your web applications. The rule specifies a list of IP addresses or IP address ranges in Classless Inter-Domain Routing (CIDR) format.

An IP address match has two types of match variables: `RemoteAddr` and `SocketAddr`. The `RemoteAddr` variable is the original client IP that's usually sent through the `X-Forwarded-For` request header. The `SocketAddr` variable is the source IP address the WAF sees. If your user is behind a proxy, `SocketAddr` is often the proxy server address.

By default, your web application is accessible from the internet. If you want to limit access to clients from a list of known IP addresses or IP address ranges, create an IP matching rule that contains the list of IP addresses as matching values, sets the operator to `Not` (negate is true), and sets the action to `Block`. After you apply an IP restriction rule, requests that originate from addresses outside this allowed list receive a 403 Forbidden response.

## Configure a WAF policy

#### [Portal](#tab/browser)

Follow these steps to configure a WAF policy using the Azure portal.

### Prerequisites

Create an Azure Front Door profile by following the instructions described in [Quickstart: Create an Azure Front Door instance for a highly available global web application](../../frontdoor/quickstart-create-front-door.md).

### Create a WAF policy

1. On the Azure portal, select **Create a resource**. Enter **Web application firewall** in the **Search services and marketplace** search box and select Enter. Then select **Web Application Firewall (WAF)**.

1. Select **Create**.

1. On the **Create a WAF policy** page, use the following values to complete the **Basics** tab.

|Setting  |Value  |

|---------|---------|

|Policy for     |Global WAF (Front Door).|

|Front door tier| Select Premium or Standard to match your Azure Front Door tier.|

|Subscription     |Select your subscription.|

|Resource group     |Select the resource group where your Azure Front Door instance is located.|

|Policy name     |Enter a name for your policy.|

|Policy state     |Selected|

|Policy mode|Prevention|

1. Select **Next: Managed rules**.

1. Select **Next: Policy settings**.

1. On the **Policy settings** tab, enter **You've been blocked!** for the **Block response body** so that you can see that your custom rule is in effect.

1. Select **Next: Custom rules**.

1. Select **Add custom rule**.

1. On the **Add custom rule** page, use the following test values to create a custom rule.

|Setting  |Value  |

|---------|---------|

|Custom rule name     |FdWafCustRule|

|Status     |Enabled|

|Rule type     |Match|

|Priority    |100|

|Match type     |IP address|

|Match variable|SocketAddr|

|Operation|Does not contain|

|IP address or range|10.10.10.0/24|

|Then|Deny traffic|

Select **Add**.

1. Select **Next: Association**.

1. Select **Associate a Front door profile**.

1. For **Frontend profile**, select your front-end profile.

1. For **Domain**, select the domain.

1. Select **Add**.

1. Select **Review + create**.

1. After your policy validation passes, select **Create**.

### Test your WAF policy

1. After your WAF policy deployment completes, browse to your Azure Front Door front-end host name.

1. You should see your custom block message.

> [!NOTE]

> A private IP address is used in the custom rule to guarantee the rule triggers. In an actual deployment, create *allow* and *deny* rules by using IP addresses for your particular situation.

#### [CLI](#tab/azure-devops-cli)

Follow these steps to configure a WAF policy using the Azure CLI.

### Prerequisites

Before you begin to configure an IP restriction policy, set up your CLI environment and create an Azure Front Door profile.

#### Set up the Azure CLI environment

1. Install the [Azure CLI](/cli/azure/install-azure-cli) or use Azure Cloud Shell. Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal. It has the Azure CLI preinstalled and configured to use with your account. Select the **Try it** button in the CLI commands that follow. Then sign in to your Azure account in the Cloud Shell session that opens. After the session starts, enter `az extension add --name front-door` to add the Azure Front Door extension.

1. If you're using the CLI locally in Bash, sign in to Azure by using `az login`.

#### Create an Azure Front Door profile

Create an Azure Front Door profile by following the instructions described in [Quickstart: Create an Azure Front Door instance for a highly available global web application](../../frontdoor/quickstart-create-front-door.md).

### Create a WAF policy

Create a WAF policy by using the [az network front-door waf-policy create](/cli/azure/network/front-door/waf-policy#az-network-front-door-waf-policy-create) command.

In the following example, replace the policy name *IPAllowPolicyExampleCLI* with a unique policy name.

```azurecli-interactive

az network front-door waf-policy create \

--resource-group <resource-group-name> \

--subscription <subscription ID> \

--name IPAllowPolicyExampleCLI

```

### Add a custom IP access control rule

Use the [az network front-door waf-policy custom-rule create](/cli/azure/network/front-door/waf-policy/rule#az-network-front-door-waf-policy-rule-create) command to add a custom IP access control rule for the WAF policy you created.

In the following examples:

-  Replace *IPAllowPolicyExampleCLI* with your unique policy created earlier.

-  Replace *ip-address-range-1*, *ip-address-range-2* with your own range.

First, create an IP allow rule for the policy created from the previous step.

> [!NOTE]

> `--defer` is required because a rule must have a match condition to be added in the next step.

```azurecli

az network front-door waf-policy rule create \

--name IPAllowListRule \

--priority 1 \

--rule-type MatchRule \

--action Block \

--resource-group <resource-group-name> \

--policy-name IPAllowPolicyExampleCLI --defer

```

Next, add a match condition to the rule:

```azurecli

az network front-door waf-policy rule match-condition add \

--match-variable SocketAddr \

--operator IPMatch \

--values "ip-address-range-1" "ip-address-range-2" \

--negate true \

--name IPAllowListRule \

--resource-group <resource-group-name> \

--policy-name IPAllowPolicyExampleCLI

```

### Find the ID of a WAF policy

Find a WAF policy's ID by using the [az network front-door waf-policy show](/cli/azure/network/front-door/waf-policy#az-network-front-door-waf-policy-show) command. Replace *IPAllowPolicyExampleCLI* in the following example with your unique policy that you created earlier.

```azurecli

az network front-door  waf-policy show \

--resource-group <resource-group-name> \

--name IPAllowPolicyExampleCLI

```

### Link a WAF policy to an Azure Front Door front-end host

Set the Azure Front Door *WebApplicationFirewallPolicyLink* ID to the policy ID by using the [az network front-door update](/cli/azure/network/front-door#az-network-front-door-update) command. Replace *IPAllowPolicyExampleCLI* with your unique policy that you created earlier.

```azurecli

az network front-door update \

--set FrontendEndpoints[0].WebApplicationFirewallPolicyLink.id=/subscriptions/<subscription ID>/resourcegroups/resource-group-name/providers/Microsoft.Network/frontdoorwebapplicationfirewallpolicies/IPAllowPolicyExampleCLI \

--name <frontdoor-name> \

--resource-group <resource-group-name>

```

In this example, the WAF policy is applied to `FrontendEndpoints[0]`. You can link the WAF policy to any of your front ends.

> [!Note]

> You need to set the `WebApplicationFirewallPolicyLink` property only once to link a WAF policy to an Azure Front Door front end. Subsequent policy updates are automatically applied to the front end.

#### [Azure PowerShell](#tab/powershell)

Follow these steps to configure a WAF policy using Azure PowerShell.

### Prerequisites

Before you begin to configure an IP restriction policy, set up your PowerShell environment and create an Azure Front Door profile.

#### Set up your PowerShell environment

Azure PowerShell provides a set of cmdlets that use the [Azure Resource Manager](../../azure-resource-manager/management/overview.md) model for managing Azure resources.

You can install [Azure PowerShell](/powershell/azure/) on your local machine and use it in any PowerShell session. Follow the instructions on the page to sign in to PowerShell by using your Azure credentials and then install the Az PowerShell module.

1. Connect to Azure by using the following command and then use an interactive dialog to sign in.

```

Connect-AzAccount

```

1. Before you install an Azure Front Door module, make sure you have the current version of the PowerShellGet module installed. Run the following command and then reopen PowerShell.

```

Install-Module PowerShellGet -Force -AllowClobber

```

1. Install the Az.FrontDoor module by using the following command:

```

Install-Module -Name Az.FrontDoor

```

### Create an Azure Front Door profile

Create an Azure Front Door profile by following the instructions in [Quickstart: Create a Front Door for a highly available global web application](../../frontdoor/quickstart-create-front-door.md).

### Define an IP match condition

Use the [New-AzFrontDoorWafMatchConditionObject](/powershell/module/az.frontdoor/new-azfrontdoorwafmatchconditionobject) command to define an IP match condition.

In the following example, replace *ip-address-range-1* and *ip-address-range-2* with your own ranges.

```powershell

$IPMatchCondition = New-AzFrontDoorWafMatchConditionObject `

-MatchVariable  SocketAddr `

-OperatorProperty IPMatch `

-MatchValue "ip-address-range-1", "ip-address-range-2"

-NegateCondition 1

```

### Create a custom IP allow rule

Use the [New-AzFrontDoorWafCustomRuleObject](/powershell/module/Az.FrontDoor/New-azfrontdoorwafcustomruleobject) command to define an action and set a priority. In the following example, requests from client IPs that don't match the list are blocked.

```azurepowershell

$IPAllowRule = New-AzFrontDoorWafCustomRuleObject `

-Name "IPAllowRule" `

-RuleType MatchRule `

-MatchCondition $IPMatchCondition `

-Action Block -Priority 1

```

### Configure a WAF policy

Find the name of the resource group that contains the Azure Front Door profile by using `Get-AzResourceGroup`. Next, configure a WAF policy with the IP rule by using [New-AzFrontDoorWafPolicy](/powershell/module/az.frontdoor/new-azfrontdoorwafpolicy).

```azurepowershell

$IPAllowPolicyExamplePS = New-AzFrontDoorWafPolicy `

-Name "IPRestrictionExamplePS" `

-resourceGroupName <resource-group-name> `

-Customrule $IPAllowRule`

-Mode Prevention `

-EnabledState Enabled

```

> [!TIP]

> For an existing WAF policy, use [Update-AzFrontDoorWafPolicy](/powershell/module/az.frontdoor/update-azfrontdoorwafpolicy) to update the policy.

### Link a WAF policy to an Azure Front Door front-end host

Link a WAF policy object to an existing front-end host and update Azure Front Door properties. First, retrieve the Azure Front Door object by using [Get-AzFrontDoor](/powershell/module/Az.FrontDoor/Get-AzFrontDoor). Next, set the `WebApplicationFirewallPolicyLink` property to the resource ID of `$IPAllowPolicyExamplePS`, created in the previous step, by using the [Set-AzFrontDoor](/powershell/module/Az.FrontDoor/Set-AzFrontDoor) command.

```azurepowershell

$FrontDoorObjectExample = Get-AzFrontDoor `

-ResourceGroupName <resource-group-name> `

-Name $frontDoorName

$FrontDoorObjectExample[0].FrontendEndpoints[0].WebApplicationFirewallPolicyLink = $IPBlockPolicy.Id

Set-AzFrontDoor -InputObject $FrontDoorObjectExample[0]

```

> [!NOTE]

> In this example, the WAF policy is applied to `FrontendEndpoints[0]`. You can link a WAF policy to any of your front ends. You need to set the `WebApplicationFirewallPolicyLink` property only once to link a WAF policy to an Azure Front Door front end. Subsequent policy updates are automatically applied to the front end.

#### [Template](#tab/yaml)

To view the Resource Manager template that creates an Azure Front Door policy and a WAF policy with custom IP restriction rules, go to [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-waf-clientip).

---

## Next steps

Learn how to [create an Azure Front Door profile](../../frontdoor/quickstart-create-front-door.md).


# Waf Front Door Tuning

# Tune Azure Web Application Firewall for Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard/Premium :heavy_check_mark: Front Door (classic)

The Microsoft-managed default rule set is based on the [OWASP Core Rule Set](https://github.com/SpiderLabs/owasp-modsecurity-crs/tree/v3.1/dev) and includes Microsoft Threat Intelligence collection rules.

It's often expected that web application firewall (WAF) rules must be tuned to suit the specific needs of the application or organization that's using the WAF. Organizations commonly achieve tuning by taking one of the following actions:

- Defining rule exclusions.

- Creating custom rules.

- Disabling rules that might be causing issues or false positives.

This article describes what you can do if requests that should pass through your WAF are blocked.

> [!NOTE]

> The Microsoft-managed rule set isn't available for the Azure Front Door Standard SKU. For more information about the different tier SKUs, see [Feature comparison between tiers](../../frontdoor/standard-premium/tier-comparison.md#feature-comparison-between-tiers).

Read the [Azure Front Door WAF overview](afds-overview.md) and the [WAF Policy for Azure Front Door](waf-front-door-create-portal.md) documents. Also, enable [WAF monitoring and logging](waf-front-door-monitor.md). These articles explain how the WAF functions, how the WAF rule sets work, and how to access WAF logs.

## Understand WAF logs

The purpose of WAF logs is to show every request that's matched or blocked by the WAF. It's a collection of all evaluated requests that are matched or blocked. If you notice that the WAF blocks a request that it shouldn't (a false positive), you can do a few things.

First, narrow down and find the specific request. You can [configure a custom response message](./waf-front-door-configure-custom-response-code.md) to include the `trackingReference` field to easily identify the event and perform a log query on that specific value. Look through the logs to find the specific URI, timestamp, or client IP of the request. When you find the related log entries, you can act on false positives.

For example, say you have legitimate traffic that contains the string `1=1` that you want to pass through your WAF. Here's what the request looks like:

```

POST http://afdwafdemosite.azurefd.net/api/Feedbacks HTTP/1.1

Host: afdwafdemosite.azurefd.net

Content-Type: application/x-www-form-urlencoded

Content-Length: 55

UserId=20&captchaId=7&captchaId=15&comment="1=1"&rating=3

```

If you try the request, the WAF blocks traffic that contains your `1=1` string in any parameter or field. This string is often associated with a SQL injection attack. You can look through the logs and see the timestamp of the request and the rules that blocked or matched.

The following example shows a log entry that was generated based on a rule match. You can use the following Log Analytics query to find requests that were blocked within the last 24 hours.

```kusto

AzureDiagnostics

| where Category == 'FrontDoorWebApplicationFirewallLog'

| where TimeGenerated > ago(1d)

| where action_s == 'Block'

```

```kusto

AzureDiagnostics

| where Category == 'FrontdoorWebApplicationFirewallLog'

| where TimeGenerated > ago(1d)

| where action_s == 'Block'

```

In the `requestUri` field, you can see the request was made to `/api/Feedbacks/` specifically. Going further, find the rule ID `942110` in the `ruleName` field. Knowing the rule ID, you could go to the [OWASP ModSecurity Core Rule Set official repository](https://github.com/coreruleset/coreruleset) and search by that rule ID to review its code and understand exactly what this rule matches on.

Then, by checking the `action` field, you can see that this rule is set to block requests upon matching. You can confirm that the request was blocked by the WAF because the `policyMode` is set to `prevention`.

Now, check the information in the `details` field. This field is where you can see the `matchVariableName` and the `matchVariableValue` information. This rule was triggered because someone input `1=1` in the `comment` field of the web app.

```json

{

"time": "2020-09-24T16:43:04.5422943Z",

"resourceId": "/SUBSCRIPTIONS/<Subscription ID>/RESOURCEGROUPS/<Resource Group Name>/PROVIDERS/MICROSOFT.CDN/PROFILES/AFDWAFDEMOSITE",

"category": "FrontDoorWebApplicationFirewallLog",

"operationName": "Microsoft.Cdn/Profiles/WebApplicationFirewallLog/Write",

"properties": {

"clientIP": "1.1.1.1",

"clientPort": "53566",

"socketIP": "1.1.1.1",

"requestUri": "http://afdwafdemosite.azurefd.net:80/api/Feedbacks/",

"ruleName": "DefaultRuleSet-1.0-SQLI-942110",

"policy": "AFDWAFDemoPolicy",

"action": "Block",

"host": "afdwafdemosite.azurefd.net",

"trackingReference": "0mMxsXwAAAABEalekYeI4S55qpi5R7R0/V1NURURHRTA4MTIAZGI4NGQzZDgtNWQ5Ny00ZWRkLTg2ZGYtZDJjNThlMzI2N2I4",

"policyMode": "prevention",

"details": {

"matches": [

{

"matchVariableName": "PostParamValue:comment",

"matchVariableValue": "\"1=1\""

}

],

"msg": "SQL Injection Attack: Common Injection Testing Detected",

"data": "Matched Data: \"1=1\" found within PostParamValue:comment: \"1=1\""

}

}

}

```

```json

{

"time": "2020-09-24T16:43:04.5422943Z",

"resourceId": "/SUBSCRIPTIONS/<Subscription ID>/RESOURCEGROUPS/<Resource Group Name>/PROVIDERS/MICROSOFT.NETWORK/FRONTDOORS/AFDWAFDEMOSITE",

"category": "FrontdoorWebApplicationFirewallLog",

"operationName": "Microsoft.Network/FrontDoor/WebApplicationFirewallLog/Write",

"properties": {

"clientIP": "1.1.1.1",

"clientPort": "53566",

"socketIP": "1.1.1.1",

"requestUri": "http://afdwafdemosite.azurefd.net:80/api/Feedbacks/",

"ruleName": "DefaultRuleSet-1.0-SQLI-942110",

"policy": "AFDWAFDemoPolicy",

"action": "Block",

"host": "afdwafdemosite.azurefd.net",

"trackingReference": "0mMxsXwAAAABEalekYeI4S55qpi5R7R0/V1NURURHRTA4MTIAZGI4NGQzZDgtNWQ5Ny00ZWRkLTg2ZGYtZDJjNThlMzI2N2I4",

"policyMode": "prevention",

"details": {

"matches": [

{

"matchVariableName": "PostParamValue:comment",

"matchVariableValue": "\"1=1\""

}

],

"msg": "SQL Injection Attack: Common Injection Testing Detected",

"data": "Matched Data: \"1=1\" found within PostParamValue:comment: \"1=1\""

}

}

}

```

There's also value in checking the access logs to expand your knowledge about a given WAF event. Next, review the log that was generated as a response to the preceding event.

You can see these logs are related because the `trackingReference` value is the same. Among various fields that provide general insight, such as `userAgent` and `clientIP`, notice the `httpStatusCode` and `httpStatusDetails` fields. Here, you can see that the client received an HTTP 403 response, which confirms that this request was denied and blocked.

```json

{

"time": "2020-09-24T16:43:04.5430764Z",

"resourceId": "/SUBSCRIPTIONS/<Subscription ID>/RESOURCEGROUPS/<Resource Group Name>/PROVIDERS/MICROSOFT.CDN/PROFILES/AFDWAFDEMOSITE",

"category": "FrontDoorAccessLog",

"operationName": "Microsoft.Cdn/Profiles/AccessLog/Write",

"properties": {

"trackingReference": "0mMxsXwAAAABEalekYeI4S55qpi5R7R0/V1NURURHRTA4MTIAZGI4NGQzZDgtNWQ5Ny00ZWRkLTg2ZGYtZDJjNThlMzI2N2I4",

"httpMethod": "POST",

"httpVersion": "1.1",

"requestUri": "http://afdwafdemosite.azurefd.net:80/api/Feedbacks/",

"requestBytes": "2160",

"responseBytes": "324",

"userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36",

"clientIp": "1.1.1.1",

"socketIp": "1.1.1.1",

"clientPort": "53566",

"timeToFirstByte": "0.01",

"timeTaken": "0.011",

"securityProtocol": "",

"routingRuleName": "DemoBERoutingRule",

"rulesEngineMatchNames": [],

"backendHostname": "13.88.65.130:3000",

"isReceivedFromClient": true,

"httpStatusCode": "403",

"httpStatusDetails": "403",

"pop": "WST",

"cacheStatus": "CONFIG_NOCACHE"

}

}

```

```json

{

"time": "2020-09-24T16:43:04.5430764Z",

"resourceId": "/SUBSCRIPTIONS/<Subscription ID>/RESOURCEGROUPS/<Resource Group Name>/PROVIDERS/MICROSOFT.NETWORK/FRONTDOORS/AFDWAFDEMOSITE",

"category": "FrontdoorAccessLog",

"operationName": "Microsoft.Network/FrontDoor/AccessLog/Write",

"properties": {

"trackingReference": "0mMxsXwAAAABEalekYeI4S55qpi5R7R0/V1NURURHRTA4MTIAZGI4NGQzZDgtNWQ5Ny00ZWRkLTg2ZGYtZDJjNThlMzI2N2I4",

"httpMethod": "POST",

"httpVersion": "1.1",

"requestUri": "http://afdwafdemosite.azurefd.net:80/api/Feedbacks/",

"requestBytes": "2160",

"responseBytes": "324",

"userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36",

"clientIp": "1.1.1.1",

"socketIp": "1.1.1.1",

"clientPort": "53566",

"timeToFirstByte": "0.01",

"timeTaken": "0.011",

"securityProtocol": "",

"routingRuleName": "DemoBERoutingRule",

"rulesEngineMatchNames": [],

"backendHostname": "13.88.65.130:3000",

"isReceivedFromClient": true,

"httpStatusCode": "403",

"httpStatusDetails": "403",

"pop": "WST",

"cacheStatus": "CONFIG_NOCACHE"

}

}

```

## Resolve false positives

To make an informed decision about handling a false positive, it's important to familiarize yourself with the technologies your application uses. For example, say there isn't a SQL server in your technology stack, and you're getting false positives related to those rules. Disabling those rules doesn't necessarily weaken your security.

With this information, and the knowledge that rule 942110 is the one that matched the `1=1` string in the example, you can do a few things to stop this legitimate request from being blocked:

* **Use exclusion lists.** For more information about exclusion lists, see [Azure Web Application Firewall with Azure Front Door exclusion lists](waf-front-door-exclusion.md).

* **Change WAF actions.** For more information about what actions can be taken when a request matches a rule's conditions, see [WAF Actions](afds-overview.md#waf-actions).

* **Use custom rules.** For more information about custom rules, see [Custom rules for Azure Web Application Firewall with Azure Front Door](waf-front-door-custom-rules.md).

* **Disable rules.**

> [!TIP]

> When you select an approach to allow legitimate requests through the WAF, try to make it as narrow as you can. For example, it's better to use an exclusion list than to disable a rule entirely.

### Use exclusion lists

One benefit of using an exclusion list is that only the match variable you select to exclude will no longer be inspected for that given request. That is, you can choose between specific request headers, request cookies, query string arguments, or request body post arguments to be excluded if a certain condition is met, as opposed to excluding the whole request from being inspected. The other nonspecified variables of the request are inspected normally.

Exclusions are a global setting. The configured exclusion applies to all traffic that passes through your WAF, not just a specific web app or URI. For example, this could be a concern if `1=1` is a valid request in the body for a certain web app, but not for others under the same WAF policy.

If it makes sense to use different exclusion lists for different applications, consider using different WAF policies for each application and applying them to each application's front end.

When you configure exclusion lists for managed rules, you can choose to exclude:

- All rules within a rule set.

- All rules within a rule group.

- An individual rule.

You can configure an exclusion list by using [PowerShell](/powershell/module/az.frontdoor/New-AzFrontDoorWafManagedRuleExclusionObject), the [Azure CLI](/cli/azure/network/front-door/waf-policy/managed-rules/exclusion), the [REST API](/rest/api/frontdoorservice/webapplicationfirewall/policies/createorupdate), Bicep, Azure Resource Manager templates, or the Azure portal.

* **Exclusions at a rule level:** Applying exclusions at a rule level means that the specified exclusions won't be analyzed against that individual rule only. It will still be analyzed by all other rules in the rule set. This is the most granular level for exclusions. You can use it to fine-tune the managed rule set based on the information you find in the WAF logs when you troubleshoot an event.

* **Exclusions at a rule group level:** Applying exclusions at a rule group level means that the specified exclusions won't be analyzed against that specific set of rule types. For example, selecting **SQLI** as an excluded rule group indicates the defined request exclusions won't be inspected by any of the SQLI-specific rules. It will still be inspected by rules in other groups, such as **PHP**, **RFI**, or **XSS**. This type of exclusion can be useful when you're sure the application isn't susceptible to specific types of attacks. For example, an application that doesn't have any SQL databases could have all SQLI rules excluded without it being detrimental to its security level.

* **Exclusions at a rule set level:** Applying exclusions at a rule set level means that the specified exclusions won't be analyzed against any of the security rules available in that rule set. This exclusion is comprehensive, so use it carefully.

In this example, you perform an exclusion at the most granular level by applying an exclusion to a single rule. You want to exclude the match variable **Request body post args name** that contains `comment`. You can see the match variable details in the firewall log: `"matchVariableName": "PostParamValue:comment"`. The attribute is `comment`. You can also find this attribute name a few other ways. For more information, see [Find request attribute names](#find-request-attribute-names).

![Screenshot that shows exclusion rules.](../media/waf-front-door-tuning/exclusion-rules.png)

![Screenshot that shows rule exclusion for a specific rule.](../media/waf-front-door-tuning/exclusion-rule.png)

Occasionally, there are cases where specific parameters get passed into the WAF in a manner that might not be intuitive. For example, a token gets passed when you authenticate by using Microsoft Entra ID. The token `__RequestVerificationToken` usually gets passed in as a request cookie.

In some cases where cookies are disabled, this token is also passed in as a request post argument. For this reason, to address Microsoft Entra token false positives, you must ensure that `__RequestVerificationToken` is added to the exclusion list for both `RequestCookieNames` and `RequestBodyPostArgsNames`.

Exclusions on a field name (**Selector**) means that the value will no longer be evaluated by the WAF. The field name itself continues to be evaluated and in rare cases it might match a WAF rule and trigger an action.

![Screenshot that shows rule exclusion for a rule set.](../media/waf-front-door-tuning/exclusion-rule-selector.png)

### Change WAF actions

Another way to handle the behavior of WAF rules is by choosing the action it takes when a request matches a rule's conditions. The available actions are [Allow, Block, Log, and Redirect](afds-overview.md#waf-actions).

In this example, the default action **Block** changed to the **Log** action on rule 942110. This action causes the WAF to log the request and continue evaluating the same request against the remaining lower priority rules.

![Screenshot that shows WAF actions.](../media/waf-front-door-tuning/actions.png)

After you perform the same request, you can refer back to the logs and see that this request was a match on rule ID 942110. The `action_s` field now indicates **Log** instead of **Block**. The log query was then expanded to include the `trackingReference_s` information to see what else happened with this request.

![Screenshot that shows a log showing multiple rule matches.](../media/waf-front-door-tuning/actions-log.png)

Now you can see a different SQLI rule match that occurs milliseconds after rule ID 942110 was processed. The same request matched on rule ID 942310, and this time the default action **Block** was triggered.

Another advantage of using the **Log** action during WAF tuning or troubleshooting is that you can identify if multiple rules within a specific rule group are matching and blocking a given request. You can then create your exclusions at the appropriate level, that is, at the rule or rule group level.

### Use custom rules

After you identify what's causing a WAF rule match, you can use custom rules to adjust how the WAF responds to the event. Custom rules are processed before managed rules. They can contain more than one condition, and their actions can be [Allow, Deny, Log, or Redirect](afds-overview.md#waf-actions).

> [!WARNING]

> When a request matches a custom rule, the WAF engine stops processing the request. Managed rules won't be processed for this request and neither will other custom rules with a lower priority.

The following example shows a custom rule with two conditions. The first condition looks for the `comment` value in the request body. The second condition looks for the `/api/Feedbacks/` value in the request URI.

By using a custom rule, you can be the most granular so that you can fine-tune your WAF rules and deal with false positives. In this case, you're not taking action only based on the `comment` request body value, which could exist across multiple sites or apps under the same WAF policy.

When you include another condition to also match on a particular request URI `/api/Feedbacks/`, you ensure this custom rule truly applies to this explicit use case that you vetted out. In this way, the same attack, if performed against different conditions, is still inspected and prevented by the WAF engine.

![Screenshot that shows a log.](../media/waf-front-door-tuning/custom-rule.png)

When you explore the log, you can see that the `ruleName_s` field contains the name given to the custom rule  `redirectcomment`. In the `action_s` field, you can see that the **Redirect** action was taken for this event. In the `details_matches_s` field, you can see the details for both conditions were matched.

### Disable rules

Another way to get around a false positive is to disable the rule that matched the input the WAF thought was malicious. Because you parsed the WAF logs and narrowed the rule down to 942110, you can disable it in the Azure portal. For more information, see [Customize Azure Web Application Firewall rules by using the Azure portal](../ag/application-gateway-customize-waf-rules-portal.md#disable-rule-groups-and-rules).

Disabling a rule is a benefit when you're sure that all requests meeting that specific condition are legitimate requests, or when you're sure the rule doesn't apply to your environment (such as disabling a SQL injection rule because you have non-SQL back ends).

Disabling a rule is a global setting that applies to all front-end hosts associated to the WAF policy. When you choose to disable a rule, you might be leaving vulnerabilities exposed without protection or detection for any other front-end hosts associated to the WAF policy.

If you want to use Azure PowerShell to disable a managed rule, see the [`PSAzureManagedRuleOverride`](/powershell/module/az.frontdoor/new-azfrontdoorwafmanagedruleoverrideobject) object documentation. If you want to use the Azure CLI, see the [`az network front-door waf-policy managed-rules override`](/cli/azure/network/front-door/waf-policy/managed-rules/override) documentation.

> [!TIP]

> Document any changes you make to your WAF policy. Include example requests to illustrate the false positive detection. Explain why you added a custom rule, disabled a rule or rule set, or added an exception. If you redesign your application in the future, you might need to verify that your changes are still valid. Or you might be audited or need to justify why you reconfigured the WAF policy from its default settings.

## Find request fields

By using a browser proxy like [Fiddler](https://www.telerik.com/fiddler), you can inspect individual requests and determine what specific fields of a webpage are called. This technique is helpful when you need to exclude certain fields from inspection by using exclusion lists in the WAF.

### Find request attribute names

In this example, the field where the `1=1` string was entered is called `comment`. This data was passed in the body of a POST request.

![Screenshot that shows the body of a Fiddler request.](../media/waf-front-door-tuning/fiddler-request-attribute-name.png)

You can exclude this field. To learn more about exclusion lists, see [Web application firewall exclusion lists](./waf-front-door-exclusion.md). You can exclude the evaluation in this case by configuring the following exclusion:

![Screenshot that shows an exclusion rule.](../media/waf-front-door-tuning/fiddler-request-attribute-name-exclusion.png)

You can also examine the firewall logs to get the information to see what you need to add to the exclusion list. To enable logging, see [Monitor metrics and logs in Azure Front Door](./waf-front-door-monitor.md).

Examine the firewall log in the `PT1H.json` file for the hour that the request you want to inspect occurred. The `PT1H.json` files are available in the storage account containers where the `FrontDoorWebApplicationFirewallLog` and the `FrontDoorAccessLog` diagnostic logs are stored.

Examine the firewall log in the `PT1H.json` file for the hour that the request you want to inspect occurred. The `PT1H.json` files are available in the storage account containers where the `FrontdoorWebApplicationFirewallLog` and the `FrontdoorAccessLog` diagnostic logs are stored.

In this example, you can see the rule that blocked the request (with the same Transaction Reference) and that occurred at the same time.

```json

{

"time": "2020-09-24T16:43:04.5422943Z",

"resourceId": "/SUBSCRIPTIONS/<Subscription ID>/RESOURCEGROUPS/<Resource Group Name>/PROVIDERS/MICROSOFT.CDN/PROFILES/AFDWAFDEMOSITE",

"category": "FrontDoorWebApplicationFirewallLog",

"operationName": "Microsoft.Cdn/Profiles/WebApplicationFirewallLog/Write",

"properties": {

"clientIP": "1.1.1.1",

"clientPort": "53566",

"socketIP": "1.1.1.1",

"requestUri": "http://afdwafdemosite.azurefd.net:80/api/Feedbacks/",

"ruleName": "DefaultRuleSet-1.0-SQLI-942110",

"policy": "AFDWAFDemoPolicy",

"action": "Block",

"host": "afdwafdemosite.azurefd.net",

"trackingReference": "0mMxsXwAAAABEalekYeI4S55qpi5R7R0/V1NURURHRTA4MTIAZGI4NGQzZDgtNWQ5Ny00ZWRkLTg2ZGYtZDJjNThlMzI2N2I4",

"policyMode": "prevention",

"details": {

"matches": [

{

"matchVariableName": "PostParamValue:comment",

"matchVariableValue": "\"1=1\""

}

],

"msg": "SQL Injection Attack: Common Injection Testing Detected",

"data": "Matched Data: \"1=1\" found within PostParamValue:comment: \"1=1\""

}

}

}

```

```json

{

"time": "2020-09-24T16:43:04.5422943Z",

"resourceId": "/SUBSCRIPTIONS/<Subscription ID>/RESOURCEGROUPS/<Resource Group Name>/PROVIDERS/MICROSOFT.NETWORK/FRONTDOORS/AFDWAFDEMOSITE",

"category": "FrontdoorWebApplicationFirewallLog",

"operationName": "Microsoft.Network/FrontDoor/WebApplicationFirewallLog/Write",

"properties": {

"clientIP": "1.1.1.1",

"clientPort": "53566",

"socketIP": "1.1.1.1",

"requestUri": "http://afdwafdemosite.azurefd.net:80/api/Feedbacks/",

"ruleName": "DefaultRuleSet-1.0-SQLI-942110",

"policy": "AFDWAFDemoPolicy",

"action": "Block",

"host": "afdwafdemosite.azurefd.net",

"trackingReference": "0mMxsXwAAAABEalekYeI4S55qpi5R7R0/V1NURURHRTA4MTIAZGI4NGQzZDgtNWQ5Ny00ZWRkLTg2ZGYtZDJjNThlMzI2N2I4",

"policyMode": "prevention",

"details": {

"matches": [

{

"matchVariableName": "PostParamValue:comment",

"matchVariableValue": "\"1=1\""

}

],

"msg": "SQL Injection Attack: Common Injection Testing Detected",

"data": "Matched Data: \"1=1\" found within PostParamValue:comment: \"1=1\""

}

}

}

```

With your knowledge of how the Azure-managed rule sets work, you know that the rule with the `action: Block` property is blocking based on the data matched in the request body. (For more information, see [Azure Web Application Firewall in Azure Front Door](afds-overview.md).) You can see in the details that it matched a pattern (`1=1`) and the field is named `comment`. Follow the same previous steps to exclude the request body post args name that contains `comment`.

### Find request header names

Fiddler is a useful tool to find request header names. The following screenshot shows the headers for this GET request, which include `Content-Type` and `User-Agent`. You can also use request headers to create exclusions and custom rules in the WAF.

![Screenshot that shows the header of a Fiddler request.](../media/waf-front-door-tuning/fiddler-request-header-name.png)

Another way to view request and response headers is to look inside the developer tools of your browser, such as Microsoft Edge or Chrome. You can select F12 or right-click **Inspect** > **Developer Tools**. Select the **Network** tab. Load a webpage and select the request you want to inspect.

![Screenshot that shows a Network inspector request.](../media/waf-front-door-tuning/network-inspector-request.png)

### Find request cookie names

If the request contains cookies, select the **Cookies** tab to view them in Fiddler. Cookie information can also be used to create exclusions or custom rules in the WAF.

## Anomaly scoring rule

If you see rule ID 949110 during the process of tuning your WAF, its presence indicates that the request was blocked by the [anomaly scoring](waf-front-door-drs.md#anomaly-scoring-mode) process.

Review the other WAF log entries for the same request by searching for the log entries with the same tracking reference. Look at each of the rules that were triggered. Tune each rule by following the guidance in this article.

> [!WARNING]

> When assigning a new managed ruleset to a WAF policy, all the previous customizations from the existing managed rulesets such as rule state, rule actions and rule level exclusions will be reset to the new managed ruleset's defaults. However, any custom rules and policy settings will remain unaffected during the new ruleset assignment.

## Next steps

- Learn about [Azure Web Application Firewall](../overview.md).

- Learn how to [create an instance of Azure Front Door](../../frontdoor/quickstart-create-front-door.md).


# Waf Azure Policy

# Azure Web Application Firewall and Azure Policy

Azure Web Application Firewall (WAF) combined with Azure Policy can help enforce organizational standards and assess compliance at-scale for WAF resources. Azure Policy is a governance tool that provides an aggregated view to evaluate the overall state of the environment, with the ability to drill down to the per-resource, per-policy granularity. Azure Policy also helps to bring your resources to compliance through bulk remediation for existing resources and automatic remediation for new resources.

## Azure Policy for Web Application Firewall

There are multiple built-in Azure Policy definitions to manage WAF resources. A breakdown of the policy definitions and their functionalities are as follows:

### Enable Web Application Firewall (WAF)

- **Azure Web Application Firewall should be enabled for Azure Front Door entry-points**: Azure Front Door Services are evaluated on if there's a WAF present or not. The policy definition has three effects: Audit, Deny, and Disable. Audit tracks when an Azure Front Door Service doesn't have a WAF and lets users see what Azure Front Door Service doesn't comply. Deny prevents any Azure Front Door Service from being created if a WAF isn't attached. Disabled turns off the policy assignment.

- **Web Application Firewall (WAF) should be enabled for Application Gateway**: Application Gateways are evaluated on if there's a WAF present on resource creation. The policy definition has three effects: Audit, Deny, and Disable. Audit tracks when an Application Gateway doesn't have a WAF and lets users see what Application Gateway doesn't comply. Deny prevents any Application Gateway from being created if a WAF isn't attached. Disabled turns off the policy assignment.

### Mandate Detection or Prevention Mode

- **Web Application Firewall (WAF) should use the specified mode for Azure Front Door Service**: Mandates the use of 'Detection' or 'Prevention' mode to be active on all Web Application Firewall policies for Azure Front Door Service. The policy definition has three effects: Audit, Deny, and Disable. Audit tracks when a WAF doesn't fit the specified mode. Deny prevents any WAF from being created if it isn't in the correct mode. Disabled turns off the policy assignment.

- **Web Application Firewall (WAF) should use the specified mode for Application Gateway**: Mandates the use of 'Detection' or 'Prevention' mode to be active on all Web Application Firewall policies for Application Gateway. The policy definition has three effects: Audit, Deny, and Disable. Audit tracks when a WAF doesn't fit the specified mode. Deny prevents any WAF from being created if it isn't in the correct mode. Disabled turns off the policy assignment.

### Require Request Inspection

- **Azure Web Application Firewall on Azure Front Door should have request body inspection enabled**: Ensure that Web Application Firewalls associated to Azure Front Doors have Request body inspection enabled. This functionality allows the WAF to inspect properties within the HTTP body that may not be evaluated in the HTTP headers, cookies, or URI.

- **Azure Web Application Firewall on Azure Application Gateway should have request body inspection enabled**: Ensure that Web Application Firewalls associated to Azure Application Gateways have Request body inspection enabled. This functionality allows the WAF to inspect properties within the HTTP body that may not be evaluated in the HTTP headers, cookies, or URI.

### Require Resource Logs

- **Azure Front Door should have Resource logs enabled**: Mandates the enabling of Resource logs and Metrics on the Azure Front Door classic Service, including WAF. The policy definition has two effects: AuditIfNotExists and Disable. AuditIfNotExists tracks when a Front Door service doesn't have resource logs, metrics enabled and notifies the user that the service doesn't comply. Disabled turns off the policy assignment.

- **Azure Front Door Standard or Premium (Plus WAF) should have resource logs enabled**: Mandates the enabling of Resource logs and Metrics on the Azure Front Door standard and premium Services, including WAF. The policy definition has two effects: AuditIfNotExists and Disable. AuditIfNotExists tracks when a Front Door service doesn't have resource logs, metrics enabled and notifies the user that the service doesn't comply. Disabled turns off the policy assignment.

- **Azure Application Gateway should have Resource logs enabled**: Mandates the enabling of Resource logs and Metrics on all Application Gateways, including WAF. The policy definition has two effects: AuditIfNotExists and Disable. AuditIfNotExists tracks when an Application Gateway doesn't have resource logs, metrics enabled and notifies the user that the Application Gateway doesn't comply. Disabled turns off the policy assignment.

### Recommended WAF Configurations

- **Azure Front Door profiles should use Premium tier that supports managed WAF rules and private link**: Mandates that all of your Azure Front Door profiles are on the premium tier instead of the standard tier. Azure Front Door Premium is optimized for security, and gives you access to the most up to date WAF rulesets and functionality like bot protection.

- **Enable Rate Limit rule to protect against DDoS attacks on Azure Front Door WAF**: Rate limiting can help protect your application against DDoS attacks. The Azure Web Application Firewall (WAF) rate limit rule for Azure Front Door helps protect against DDoS by controlling the number of requests allowed from a particular client IP address to the application during a rate limit duration.

- **Migrate WAF from WAF Config to WAF Policy on Application Gateway**: If you have WAF Config instead of WAF Policy, then you may want to move to the new WAF Policy. Web Application Firewall (WAF) policies offer a richer set of advanced features over WAF config, provide a higher scale, better performance, and unlike legacy WAF configuration, WAF policies can be defined once and shared across multiple gateways, listeners, and URL paths. Going forward, the latest features and future enhancements are only available via WAF policies.

## Create an Azure Policy

1.	On the Azure home page, type Policy in the search bar and select the Azure Policy icon.

2.	On the Azure Policy service, under **Authoring**, select **Assignments**.

3.	On the Assignments page, select the **Assign policy** icon at the top.

4.	On the Assign Policy page basics tab, update the following fields:

1.	**Scope**: Select what Azure subscriptions and resource groups the policies apply to.

2.	**Exclusions**: Select any resources from the scope to exclude from the policy assignment.

3.	**Policy Definition**: Select the policy definition to apply to the scope with exclusions. Type "Web Application Firewall" in the search bar to choose the relevant Web Application Firewall Azure Policy.

5.	Select the **Parameters** tab and update the policy assignment parameters. To further clarify what the parameter does, hover over the info icon next to the parameter name for further clarification.

6.	Select **Review + create** to finalize your policy assignment. The policy assignment takes approximately 15 minutes until it's active for new resources.


# Manage Policies

# Configure WAF policies using Azure Firewall Manager

Azure Firewall Manager is a platform to manage and protect your network security resources at scale. You can associate your WAF policies to an Application Gateway or Azure Front Door within Azure Firewall Manager, all in a single place.

## View and manage WAF policies

In Azure Firewall Manager, you can create and view all WAF policies in one central place across subscriptions and regions.

To navigate to WAF policies, select the **Web Application Firewall Policies** tab on the left, under **Security**.

## Associate or dissociate WAF policies

In Azure Firewall Manager, you can create and view all WAF policies in your subscriptions. These policies can be associated or dissociated with an application delivery platform. Select the service and then select **Manage Security**.

## Upgrade Application Gateway WAF configuration to WAF policy

For Application Gateway with WAF configuration, you can upgrade the WAF configuration to a WAF policy associated with Application Gateway.

The WAF policy can be shared to multiple application gateways. Also, a WAF policy allows you to take advantage of advanced and new features like bot protection, newer rule sets, and reduced false positives. New features are only released on WAF policies.

To upgrade a WAF configuration to a WAF policy, select **Upgrade from WAF configuration** from the desired application gateway.

## Next steps

- [Manage Azure Web Application Firewall policies](../../firewall-manager/manage-web-application-firewall-policies.md)


# Protect Api Hosted Apim By Waf

# Protect APIs hosted on API Management using Azure Web Application Firewall

There are a growing number of enterprises adhering to API-first approach for their internal applications, and the number and complexity of security attacks against web applications is constantly evolving. This situation requires enterprises to adopt a strong security strategy to protect APIs from various web application attacks.

[Azure Web Application Firewall (WAF)](../overview.md) is an Azure Networking product that protects APIs from various [OWASP top 10](https://owasp.org/www-project-top-ten/) web attacks, CVE’s, and malicious bot attacks.

This article describes how to use [Azure Web Application Firewall on Azure Front Door](afds-overview.md) to protect APIs hosted on [Azure API Management](../../api-management/api-management-key-concepts.md)

## Create an APIM instance and publish an API in APIM that generates a mock API response

1. Create an APIM instance. For more information, see [Quickstart: Create a new Azure API Management service instance by using the Azure portal](../../api-management/get-started-create-service-instance.md).

The following screenshot shows that an APIM instance called **contoso-afd-apim-resource** has been created. It can take up to 30 to 40 minutes to create and activate an API Management service.

2. Create an API and generate mock API responses. For more information, see [Tutorial: Mock API responses](../../api-management/mock-api-responses.md#add-an-operation-to-the-test-api).

Replace the name of API from **Test API** given in the above tutorial with **Book API**.

The Book API does a GET operation for `_/test_` as the URL path for the API. You can see the response for the API is set as **200 OK** with content type as application/json with text as `{“Book”:” $100”}`.

3. Deselect **Subscription required** check box under the API settings tab and select **Save**.

4. Test the mock responses from the APIM interface. You should receive a **200 OK** response.

Now, the Book API has been created. A successful call to this URL returns a **200 OK** response and returns the price of a book as $100.

## Create an Azure Front Door Premium instance with APIM hosted API as the origin

The Microsoft-managed Default Rule Set is based on the [OWASP Core Rule Set](https://github.com/coreruleset/coreruleset//) and includes Microsoft Threat Intelligence rules.

> [!NOTE]

> Managed Rule Set is not available for Azure Front Door Standard SKU. For more information about the different SKUs, see [Azure Front Door tier comparison](../../frontdoor/standard-premium/tier-comparison.md#feature-comparison-between-tiers).

Use the steps described in quick create option to create an Azure Front Door Premium profile with an associated WAF security policy in the same resource group:

[Quickstart: Create an Azure Front Door profile - Azure portal](../../frontdoor/create-front-door-portal.md)

Use the following settings when creating the Azure Front Door profile:

- Name: myAzureFrontDoor

- Endpoint Name: bookfrontdoor

- Origin type: API Management

- Origin host name: contoso-afd-apim-resource.azure-api.net(contoso-afd-apim-resource)

- WAF policy: Create a new WAF policy with name **bookwafpolicy**.

All other settings remain at default values.

## Enable Azure Web Application Firewall in prevention mode

Select the "bookwafpolicy" Azure WAF policy  and ensure the Policy mode is set to

["Prevention" in the overview tab of the policy](waf-front-door-create-portal.md#change-mode)

Azure WAF detection mode is used for testing and validating the policy. Detection doesn't block the call but logs all threats detected, while prevention mode blocks the call if an attack is detected. Typically, you test the scenario before switching to prevention mode. For this exercise, we switch to prevention mode.

[Azure Web Application Firewall on Azure Front Door](afds-overview.md#waf-modes) has more information about various WAF policy modes.

## Restrict APIM access through the Azure Front Door only

Requests routed through the Front Door include headers specific to your Front Door configuration. You can configure the

[check-header policy](../../api-management/api-management-policies.md#authentication-and-authorization) as an inbound APIM policy to filter incoming requests based on the unique value of the X-Azure-FDID HTTP request header that is sent to API Management. This header value is the Azure Front Door ID, which is available on the AFD Overview page.

1. Copy the Front Door ID from the AFD overview page.

2. Access the APIM API page, select the Book API, select **Design** and **All operations**.  In the Inbound policy, select **+ Add policy**.

3. Select Other policies

4. Select “Show snippets" and select **Check HTTP header**.

Add the following code to the inbound policy for HTTP header `X-Azure-FDID`. Replace the `{FrontDoorId}`  with the AFD ID copied in the first step of this section.

```

<check-header name="X-Azure-FDID" failed-check-httpcode="403" failed-check-error-message="Invalid request" ignore-case="false">

<value>{FrontDoorId}</value>

</check-header>

```

5. Select **Save**.

At this point, APIM access is restricted to the Azure Front Door endpoint only.

## Verify the API call is routed through Azure Front Door and protected by Azure Web Application Firewall

1. Obtain the newly created Azure Front Door endpoint from the **Front Door Manager**.

2. Look at origin groups and confirm that the origin host name is __contoso-afd-apim-resource.azure-api.net.__ This step verifies that the APIM instance is an origin in the newly configured Azure Front Door premium.

3. Under the **Security Policies** section, verify that the WAF policy **bookwafpolicy** is provisioned.

4. Select **bookwafpolicy** and verify that the **bookwafpolicy** has Managed rules provisioned. The latest versions of Microsoft_DefaultRueSet and Microsoft_BotManagerRuleSet is provisioned which protects the origin against OWASP top 10 vulnerabilities and malicious bot attacks.

At this point, the end-to-end call is set up, and the API is protected by Azure Web Application Firewall.

## Verify the setup

1. Access the API through the Azure Front Door endpoint from your browser. The API should return the following response:

2. Verify that APIM isn't accessible directly over the Internet and accessible only via the AFD:

3. Now try to invoke the AFD endpoint URL via any OWASP Top 10 attack or bot attack and you should receive `REQUEST IS BLOCKED` message and the request is blocked. The API has been protected from web attack by Azure Web Application Firewall.

## Related content

- [What is Azure Web Application Firewall?](../overview.md)

- [Recommendations to mitigate OWASP API Security Top 10 threats using API Management](../../api-management/mitigate-owasp-api-threats.md)

- [Configure Front Door Standard/Premium in front of Azure API Management](../../api-management/front-door-api-management.md)


# Protect Azure Open Ai

# Protect Azure OpenAI using Azure Web Application Firewall on Azure Front Door

There are a growing number of enterprises using Azure OpenAI APIs, and the number and complexity of security attacks against web applications is constantly evolving. A strong security strategy is necessary to protect Azure OpenAI APIs from various web application attacks.

Azure Web Application Firewall (WAF) is an Azure Networking product that protects web applications and APIs from various OWASP top 10 web attacks, Common Vulnerabilities and Exposures (CVEs), and malicious bot attacks.

This article describes how to use Azure Web Application Firewall (WAF) on Azure Front Door to protect Azure OpenAI endpoints.

## Prerequisites

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Create Azure OpenAI instance using the gpt-35-turbo model

First, create an OpenAI instance.

1. Create an Azure OpenAI instance and deploy a gpt-35-turbo model using [Create and deploy an Azure OpenAI Service resource](/azure/ai-services/openai/how-to/create-resource).

1. Identify the Azure OpenAI endpoint and the API key.

Open the Azure OpenAI service in the Microsoft Foundry portal and open the **Chat** option under **Playground**.

Use the **View code** option to display the endpoint and the API key.

1. Validate Azure OpenAI call using your favorite API test method, such as [Visual Studio](/aspnet/core/test/http-files) or [Insomnia](https://insomnia.rest/).

Use the Azure OpenAPI endpoint and api-key values found in the earlier steps.

Use these lines of code in the POST body:

```json

{

"model":"gpt-35-turbo",

"messages": [

{

"role": "user",

"content": "What is Azure OpenAI?"

}

]

}

```

1. In response to the POST, you should receive a *200 OK*.

The Azure OpenAI also generates a response using the GPT model.

## Create an Azure Front Door instance with Azure WAF

Now use the Azure portal to create an Azure Front Door instance with Azure WAF.

1. Create an Azure Front Door premium optimized tier with an associated WAF security policy in the same resource group. Use the **Custom create** option.

1. [Quickstart: Create an Azure Front Door profile - Azure portal](../../frontdoor/create-front-door-portal.md#create-a-front-door-for-your-application)

1. Add endpoints and routes.

1. Add the origin hostname: The origin hostname is `testazureopenai.openai.azure.com`.

1. Add the WAF policy.

## Configure a WAF policy to protect against web application and API vulnerabilities

Enable the WAF policy in prevention mode and ensure **Microsoft_DefaultRuleSet_2.1** and **Microsoft_BotManagerRuleSet_1.0** are enabled.

## Verify access to Azure OpenAI via Azure Front Door endpoint

Now verify your Azure Front Door endpoint.

1. Retrieve the Azure Front Door endpoint from the Front Door Manager.

2. Use your favorite API test method, such as [Visual Studio](/aspnet/core/test/http-files) or [Insomnia](https://insomnia.rest/) to send a POST request to the Azure Front Door endpoint.

3. Replace the Azure OpenAI endpoint with the AFD endpoint in the POST request.

Azure OpenAI also generates a response using the GPT model.

## Validate WAF blocks an OWASP attack

Send a POST request simulating an OWASP attack on the Azure OpenAI endpoint. WAF blocks the call with a *403 Forbidden response* code.

## Configure IP restriction rules using WAF

To restrict access to the Azure OpenAI endpoint to the required IP addresses, see [Configure an IP restriction rule with a WAF for Azure Front Door](waf-front-door-configure-ip-restriction.md).

## Common issues

The following items are common issues you may encounter when using Azure OpenAI with Azure Front Door and Azure WAF.

- You get a *401: Access Denied* message when you send a POST request to your Azure OpenAI endpoint.

If you attempt to send a POST request to your Azure OpenAI endpoint immediately after you create it, you may receive a *401: Access Denied* message even if you have the correct API key in your request. This issue will usually resolve itself after some time without any direct intervention.

- You get a *415: Unsupported Media Type* message when you send a POST request to your Azure OpenAI endpoint.

If you attempt to send a POST request to your Azure OpenAI endpoint with the Content-Type header `text/plain`, you get this message. Make sure to update your Content-Type header to `application/json` in the header section in your test.


# Secure Web Application Firewall

# Secure your Azure Web Application Firewall deployment

Azure Web Application Firewall (WAF) provides centralized protection for your web applications from common exploits and vulnerabilities such as SQL injection, cross-site scripting, and other OWASP Top 10 attacks. As a critical security component that sits between your applications and potential threats, it's essential to properly secure your WAF deployment to maximize its effectiveness and maintain your overall security posture.

This article provides guidance on how to best secure your Azure Web Application Firewall deployment.

## Network security

Network security for Azure Web Application Firewall focuses on protecting your applications through proper traffic management, blocking malicious IP addresses, and configuring WAF modes appropriately. These controls help ensure that only legitimate traffic reaches your applications while maintaining comprehensive protection against web-based attacks.

* **Configure WAF in Prevention mode after baseline period**: Start with Detection mode to understand your traffic patterns and identify false positives, then switch to Prevention mode to actively block attacks. Prevention mode blocks intrusions and attacks detected by the rules, sending attackers a "403 unauthorized access" exception. See [WAF modes on Application Gateway](/azure/web-application-firewall/ag/ag-overview#waf-modes) and [WAF modes on Front Door](/azure/web-application-firewall/afds/afds-overview#waf-modes).

* **Use custom rules to block malicious IP addresses**: Create custom rules to allow and block traffic based on IP addresses, ranges, or geographic locations. This provides granular control over who can access your applications and helps prevent attacks from known bad actors. See [Web Application Firewall CRS rule groups and rules](/azure/web-application-firewall/ag/application-gateway-crs-rulegroups-rules).

* **Customize WAF rules to reduce false positives**: Apply site-specific WAF policies and customize rules and rule groups to suit your web application requirements. This helps eliminate false positives while maintaining protection against genuine threats. Associate a unique Azure WAF Policy for each site to allow for site-specific configuration.

* **Enable comprehensive logging and monitoring**: Turn on Diagnostics and WAF logs when operating in Detection mode to monitor and log all threat alerts. This provides visibility into what your WAF is evaluating, matching, and blocking. See [Logging overview](/azure/web-application-firewall/ag/ag-overview#logging).

* **Use tags for organized network security management**: Apply tags to network security groups associated with your WAF in your Azure Application Gateway subnet and related network security resources. Use the "Description" field for individual NSG rules to specify business needs and duration. See [How to create and use tags](/azure/azure-resource-manager/management/tag-resources).

* **Monitor network resource configurations**: Use Azure Activity Log to monitor network resource configurations and detect changes for network settings and resources related to your WAF deployments. Create alerts within Azure Monitor that trigger when changes to critical network settings occur. See [How to view and retrieve Azure Activity Log events](/azure/azure-monitor/essentials/activity-log#view-the-activity-log).

* **Implement rate limiting to prevent DDoS attacks**: Configure rate limiting rules to control the number of requests allowed from each client IP address over a specified time period. Set rate limit thresholds high enough to avoid blocking legitimate traffic while protecting against retry storms and DDoS attacks. See [What is rate limiting for Azure Front Door?](./afds/waf-front-door-rate-limit.md)

* **Enable bot protection to block malicious bots**: Use the bot protection managed rule set to identify and block bad bots while allowing legitimate bots like search engine crawlers. Bot protection rules categorize bots as good, bad, or unknown and can automatically block malicious bot traffic. See [Configure bot protection for Web Application Firewall](./afds/waf-front-door-policy-configure-bot-protection.md).

* **Implement geo-filtering for regional applications**: If your application serves users from specific geographic regions, configure geo-filtering to block requests from outside expected countries or regions. Include the unknown (ZZ) location to avoid blocking valid requests from unmapped IP addresses. See [What is geo-filtering on a domain for Azure Front Door?](./afds/waf-front-door-tutorial-geo-filtering.md)

* **Use the latest managed rule set versions**: Regularly update to the latest Azure-managed rule set versions to protect against current threats. Microsoft regularly updates managed rules based on the threat landscape and OWASP Top 10 attack types. See [Azure Web Application Firewall DRS rule groups and rules](./afds/waf-front-door-drs.md).

## Identity management

Identity management for Azure Web Application Firewall ensures that administrative access to your WAF resources is properly controlled and monitored. This includes maintaining inventories of administrative accounts, using centralized identity systems, and implementing strong authentication mechanisms for anyone managing your WAF deployment.

* **Use Azure Active Directory for centralized authentication**: Use Azure AD as your central authentication and authorization system for managing WAF resources. Azure AD protects data with strong encryption and provides consistent identity management across your Azure environment. See [How to create and configure an Azure AD instance](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).

* **Maintain inventory of administrative accounts**: Use Azure AD built-in roles that are queryable and must be explicitly assigned. Use the Azure AD PowerShell module to perform queries and discover accounts that are members of administrative groups with access to WAF resources. See [How to get a directory role in Azure AD with PowerShell](/powershell/module/azuread/get-azureaddirectoryrole).

* **Enable multifactor authentication for administrative access**: Require MFA for all users with administrative access to WAF resources. This adds a crucial additional layer of security even if passwords are compromised. Follow Microsoft Defender for Cloud's Identity and Access Management recommendations. See [How to enable multifactor authentication in Azure](/azure/active-directory/authentication/howto-mfa-getstarted).

* **Use dedicated administrative accounts with standard procedures**: Create standard operating procedures around the use of dedicated administrative accounts that have access to Azure WAF instances. Use Microsoft Defender for Cloud's Identity and Access Management features to monitor the number of administrative accounts. See [Understand Microsoft Defender for Cloud Identity and Access](/azure/security-center/security-center-identity-access).

* **Manage access from approved locations only**: Configure Conditional Access policies with named locations to restrict access to your WAF resources. Create logical groupings of IP address ranges or countries and regions, and restrict access to sensitive resources to your configured named locations. See [What is the location condition in Azure Active Directory Conditional Access](/azure/active-directory/reports-monitoring/quickstart-configure-named-locations).

* **Monitor and alert on suspicious account activities**: Use Azure AD security reports and Microsoft Defender for Cloud to monitor identity and access activity. Set up alerts for suspicious or unsafe activity and integrate with Microsoft Sentinel for advanced threat detection. See [How to identify Azure AD users flagged for risky activity](/azure/active-directory/identity-protection/overview-identity-protection).

## Privileged access

Privileged access controls for Azure Web Application Firewall focus on limiting and monitoring administrative access to your WAF resources. These measures help prevent unauthorized changes to your security configurations and ensure that privileged operations are properly tracked and audited.

* **Use Azure RBAC to control resource access**: Control access to your Azure WAF resources using Azure role-based access control. Apply the principle of least privilege by assigning only the minimum necessary permissions to users and services. See [How to configure Azure RBAC in Azure](/azure/role-based-access-control/role-assignments-portal).

* **Use Privileged Access Workstations for administrative tasks**: Use dedicated, hardened workstations with multifactor authentication configured for logging into and configuring Azure WAF and related resources. This reduces the risk of administrative compromise through standard user workstations. See [Learn about Privileged Access Workstations](/security/compass/overview).

* **Regularly review and reconcile user access**: Use Azure Identity Access Reviews to efficiently manage group memberships, access to enterprise applications, and role assignments for WAF resources. Review user access regularly to ensure only active users have continued access. See [How to use Azure Identity Access Reviews](/azure/active-directory/governance/access-reviews-overview).

* **Monitor access to deactivated credentials**: Integrate Azure AD Sign-in Activity, Audit, and Risk Event log sources with Microsoft Sentinel or other SIEM tools. Create Diagnostic Settings for Azure AD user accounts and send audit and sign-in logs to a Log Analytics workspace for monitoring. See [How to integrate Azure Activity Logs into Azure Monitor](/azure/active-directory/reports-monitoring/howto-integrate-activity-logs-with-log-analytics).

* **Configure automated responses to suspicious activities**: Use Azure AD's Risk and Identity Protection features to configure automated responses to detected suspicious actions related to user identities. Ingest data into Microsoft Sentinel for further investigation and response. See [How to configure and enable Identity Protection risk policies](/azure/active-directory/identity-protection/howto-identity-protection-configure-risk-policies).

## Logging and threat detection

Comprehensive logging and threat detection are essential for maintaining visibility into your Web Application Firewall's security posture. These capabilities help you detect threats, investigate incidents, and maintain compliance by collecting and analyzing security events across your WAF deployment.

* **Enable centralized log management with Microsoft Sentinel**: Configure Azure WAF logs to be sent to Microsoft Sentinel or a third-party SIEM. This includes Azure Activity, Diagnostic, and real-time WAF logs that provide insight into what data your WAF is evaluating, matching, and blocking. See [Connect data from Microsoft web application firewall to Microsoft Sentinel](/azure/sentinel/connect-azure-waf).

* **Enable comprehensive audit logging**: Turn on logging for your Azure WAF resources to capture audit, security, and diagnostic logs. Azure WAF provides detailed reporting on each detected threat through configured diagnostic logs, including event source, date, user, timestamp, and addresses. See [Logging overview](/azure/web-application-firewall/ag/ag-overview#logging).

* **Configure log storage retention policies**: Send Azure WAF logs to a custom storage account and define retention policies based on your organization's compliance requirements. Use Azure Monitor to set your Log Analytics workspace retention period appropriately. See [Configure monitoring for a storage account](/azure/storage/common/manage-storage-analytics-logs#configure-logging).

* **Monitor and review logs regularly**: Review WAF logs that provide detailed reporting on each detected threat. Use Microsoft Defender for Cloud's recommendations to detect unprotected web applications and protect vulnerable resources. Leverage Microsoft Sentinel's built-in WAF workbook for security event overview. See [How to enable diagnostic settings for Azure Application Gateway](/azure/application-gateway/application-gateway-diagnostics).

* **Create alerts for anomalous activities**: Enable Azure Activity Log diagnostic settings and WAF diagnostic settings, sending logs to a Log Analytics workspace. Create alerts for anomalous activity based on WAF metrics, such as when blocked requests exceed defined thresholds. See [How to create alerts within Azure](/azure/azure-monitor/alerts/tutorial-response).

* **Use approved time synchronization sources**: Create network rules for Azure WAF to allow access to NTP servers with appropriate ports and protocols, such as port 123 over UDP, ensuring accurate timestamps in your logs and events.

* **Enable sensitive data protection with log scrubbing**: Configure log scrubbing rules to remove sensitive information like passwords, IP addresses, and personal data from your WAF logs. This protects customer data while maintaining security visibility. See [What is Azure Web Application Firewall Sensitive Data Protection?](./afds/waf-sensitive-data-protection-frontdoor.md) and [Azure Web Application Firewall Sensitive Data Protection](./ag/waf-sensitive-data-protection.md).

* **Configure diagnostic settings for comprehensive logging**: Enable diagnostic settings on your WAF resources to save logs to Log Analytics, Storage Account, or Event Hub. Regular log review helps tune your WAF policies and understand attack patterns against your applications. See [Azure Web Application Firewall monitoring and logging](./afds/waf-front-door-monitor.md).

## Data protection

Data protection for Azure Web Application Firewall involves securing sensitive information processed by your WAF, implementing proper encryption, and maintaining appropriate access controls. These measures help protect your applications and the data they handle from unauthorized access and disclosure.

* **Tag resources handling sensitive information**: Use tags to identify and track Azure WAF and related resources that store or process sensitive information. This helps with compliance reporting and ensures appropriate security controls are applied. See [How to create and use tags](/azure/azure-resource-manager/management/tag-resources).

* **Implement environment isolation**: Use separate subscriptions and management groups for different security domains such as development, test, and production environments. This prevents cross-environment data exposure and allows for environment-specific security controls. See [How to create additional Azure subscriptions](/azure/cost-management-billing/manage/create-subscription).

* **Ensure encryption in transit**: Verify that clients connecting to your Azure WAF instances and related resources can negotiate TLS 1.2 or greater. Follow Microsoft Defender for Cloud recommendations for encryption at rest and in transit. See [Understand encryption in transit with Azure](/azure/security/fundamentals/encryption-overview#encryption-of-data-in-transit).

* **Use encryption at rest for WAF resources**: Apply encryption at rest for all Azure resources including Azure WAF and related resources. Microsoft recommends allowing Azure to manage encryption keys, but you can manage your own keys when specific requirements exist. See [Understand encryption at rest in Azure](/azure/security/fundamentals/encryption-atrest).

* **Monitor changes to critical resources**: Configure your Azure WAF to run in Prevention mode after establishing baselines, and use Azure Monitor to create alerts when changes occur to critical WAF resources or configurations. See [WAF modes on Application Gateway](/azure/web-application-firewall/ag/ag-overview#waf-modes).

* **Enable request body inspection**: Configure WAF policies to inspect HTTP request bodies, not just headers, cookies, and URIs. This allows the WAF to detect threats hidden in POST data and JSON payloads. See [Azure Web Application Firewall and Azure Policy](./shared/waf-azure-policy.md).

* **Use customer-managed keys for enhanced encryption**: Consider using customer-managed keys stored in Azure Key Vault for encryption requirements that exceed platform-managed keys. This provides additional control over encryption key lifecycle and access. See [How to configure customer-managed encryption keys](/azure/storage/common/customer-managed-keys-configure-key-vault).

## Asset management

Effective asset management helps you maintain visibility and control over your Web Application Firewall resources. This includes automated discovery, proper tagging, regular inventory reconciliation, and policy enforcement to ensure your WAF deployment remains secure and compliant.

* **Use automated asset discovery**: Use Azure Resource Graph to query and discover all WAF-related resources including compute, storage, network, ports, and protocols within your subscriptions. Ensure you have appropriate read permissions and can enumerate all Azure subscriptions and resources. See [How to create queries with Azure Resource Graph](/azure/governance/resource-graph/first-query-portal).

* **Maintain asset metadata with tags**: Apply tags to Azure WAF policies and related resources to logically organize access and management. Tags can be associated with resources and applied to organize access to these resources within your subscription. See [How to create and use Tags](/azure/azure-resource-manager/management/tag-resources).

* **Organize and track resources systematically**: Use tagging, management groups, and separate subscriptions to organize and track Azure WAF and related resources. Reconcile inventory regularly and ensure unauthorized resources are deleted from subscriptions in a timely manner. See [How to create Management Groups](/azure/governance/management-groups/create-management-group-portal).

* **Define and maintain approved resource inventory**: Create an inventory of approved resources including their configurations based on organizational needs. Use Azure Policy to restrict the types of resources that can be created in your subscriptions and ensure all present resources are approved. See [How to configure and manage Azure Policy](/azure/governance/policy/tutorials/create-and-manage).

* **Monitor for unapproved resources**: Use Azure Policy to put restrictions on resource types and monitor for unapproved Azure WAF resources within your subscriptions. Use Azure Resource Graph to query and discover resources, ensuring that all Azure WAF and related resources in your environment are approved. See [How to create queries with Azure Graph](/azure/governance/resource-graph/first-query-portal).

* **Limit Azure Resource Manager access**: Use Azure Conditional Access to limit users' ability to interact with Azure Resource Manager by configuring "Block access" for the "Microsoft Azure Management" app. This helps prevent unauthorized changes to your WAF resources. See [How to configure Conditional Access to block access to Azure Resources Manager](/azure/role-based-access-control/conditional-access-azure-management).

## Policy compliance and governance

Policy compliance and governance ensure that your Web Application Firewall deployments meet organizational standards and regulatory requirements. These controls help maintain consistent security configurations across your environment and provide automated compliance monitoring and enforcement.

* **Use Azure Policy to enforce WAF deployment**: Implement Azure Policy definitions to require WAF deployment on Azure Front Door and Application Gateway resources. Configure policies to audit, deny, or automatically remediate non-compliant resources. See [Azure Web Application Firewall and Azure Policy](./shared/waf-azure-policy.md).

* **Mandate WAF mode compliance**: Use Azure Policy to enforce that all WAF policies operate in Prevention mode after initial tuning. This ensures consistent protection across your environment and prevents accidental deployment of WAFs in Detection-only mode. See [Azure Web Application Firewall and Azure Policy](./shared/waf-azure-policy.md).

* **Require resource logging compliance**: Implement policies that mandate enabling of resource logs and metrics on all WAF-enabled services. This ensures consistent logging for security monitoring and compliance requirements across your organization. See [Azure Web Application Firewall and Azure Policy](./shared/waf-azure-policy.md).

* **Enforce Premium tier usage for enhanced security**: Use Azure Policy to require Azure Front Door Premium tier for all profiles, ensuring access to advanced WAF features like managed rule sets, bot protection, and private link capabilities. See [Azure Web Application Firewall and Azure Policy](./shared/waf-azure-policy.md).

* **Define WAF configuration as code**: Implement infrastructure as code practices using ARM templates, Bicep, or Terraform to maintain consistent WAF configurations across environments. This approach simplifies rule exclusion management and reduces configuration drift. See [Best practices for Azure Web Application Firewall in Azure Front Door](./afds/waf-front-door-best-practices.md).

* **Implement automated compliance monitoring**: Use Microsoft Defender for Cloud and Azure Policy to continuously monitor WAF compliance and receive recommendations for unprotected web applications. Configure automated alerts for policy violations and compliance drift. See [Azure Web Application Firewall and Azure Policy](./shared/waf-azure-policy.md).

## Related content

- [Security baseline](/security/benchmark/azure/baselines/web-application-firewall-security-baseline?toc=/azure/web-application-firewall/toc.json)

- [Azure Well-Architected Framework: Security pillar](/azure/well-architected/security/)

- [Cloud Adoption Framework: Secure overview](/azure/cloud-adoption-framework/secure/overview)


# Waf Sensitive Data Protection

# What is Azure Web Application Firewall Sensitive Data Protection?

The Web Application Firewall's (WAF) Log Scrubbing tool helps you remove sensitive data from your WAF logs. It works by using a rules engine that allows you to build custom rules to identify specific portions of a request that contain sensitive information. In order to work correctly, your content-type header and request body type must match. Once specified sensitive content is identified, the tool scrubs that information from your logs and replaces it with _*******_.

> [!NOTE]

> When you enable the log scrubbing feature, Microsoft still retains IP addresses in our internal logs to support critical security features.

## Default log behavior

Normally, when a WAF rule is triggered, the WAF logs the details of the request in clear text. If the portion of the request triggering the WAF rule contains sensitive data (such as customer passwords or IP addresses), that sensitive data is viewable by anyone with access to the WAF logs. To protect customer data, you can set up Log Scrubbing rules targeting this sensitive data for protection.

> [!IMPORTANT]

> Selectors are case insensitive for the RequestHeaderNames match variable only. All other match variables are case sensitive.

## Fields

The following fields can be scrubbed from the logs:

- IP address

- Request header name

- Request cookie name

- Request args name

- Post arg name

- JSON arg name

## Next steps

- [How to mask sensitive data on Azure Web Application Firewall](waf-sensitive-data-protection-configure.md)


# Waf Sensitive Data Protection Configure

# How to mask sensitive data on Azure Web Application Firewall

The Web Application Firewall's (WAF's) Log Scrubbing tool helps you remove sensitive data from your WAF logs. It works by using a rules engine that allows you to build custom rules to identify specific portions of a request that contain sensitive data. In order to work correctly, your content-type header and request body type must match. Once specified sensitive content is identified, the tool scrubs that information from your logs and replaces it with _*******_.

> [!NOTE]

> The log scrubbing feature is only supported on Web Application Firewalls running the [latest WAF engine](waf-engine.md).  Select OWASP CRS 3.2 or Default Rule Set 2.1 as the managed rule set.

> [!NOTE]

> When you enable the log scrubbing feature, Microsoft still retains IP addresses in our internal logs to support critical security features.

The following table shows examples of log scrubbing rules that can be used to protect your sensitive data:

| Match Variable | Operator | Selector | What gets scrubbed |

| --- | --- | --- | --- |

| Request Header Names | Equals | X-Forwarded-For | REQUEST_HEADERS:x-forwarded-for.","data":"******" |

| Request Cookie Names | Equals | cookie1 | "Matched Data: ****** found within REQUEST_COOKIES:cookie1: ******" |

| Request Arg Names | Equals | arg1 | "requestUri":"\/?arg1=******" |

| Request Post Arg Names | Equals | Post1 | "data":"Matched Data: ****** found within ARGS:post1: ******" |

| Request JSON Arg Names | Equals | Jsonarg | "data":"Matched Data: ****** found within ARGS:jsonarg: ******" |

| Request IP Address* | Equals Any | NULL | "clientIp":"******" |

\* Request IP Address rules only support the *equals any* operator and scrubs all instances of the requester's IP address that appears in the WAF logs.

For more information, see [What is Azure Web Application Firewall Sensitive Data Protection?](waf-sensitive-data-protection.md)

## Enable Sensitive Data Protection

Use the following information to enable and configure Sensitive Data Protection.

#### [Portal](#tab/browser)

To enable Sensitive Data Protection:

1. Open an existing Application Gateway WAF policy.

1. Under **Settings**, select **Sensitive data**.

1. On the **Sensitive data** page, select **Enable log scrubbing**.

To configure Log Scrubbing rules for Sensitive Data Protection:

1. Under **Log scrubbing rules**, select a **Match variable**.

1. Select an **Operator** (if applicable).

1. Type a **Selector** (if applicable).

1. Select **Save**.

Repeat to add more rules.

#### [PowerShell](#tab/powershell)

Use the following Azure PowerShell commands to [create](/powershell/module/az.network/new-azapplicationgatewayfirewallpolicylogscrubbingrule) and [configure](/powershell/module/az.network/new-azapplicationgatewayfirewallpolicylogscrubbingconfiguration) Log Scrubbing rules for Sensitive Data Protection:

```azurepowershell

$logScrubbingRule1 = New-AzApplicationGatewayFirewallPolicyLogScrubbingRule `

-State <String> -MatchVariable <String> `

-SelectorMatchOperator <String> -Selector <String>

$logScrubbingRuleConfig = New-AzApplicationGatewayFirewallPolicyLogScrubbingConfiguration `

-State <String> -ScrubbingRule $logScrubbingRule1

```

#### [CLI](#tab/cli)

Use the following Command Line Interface commands to [create and configure](/cli/azure/network/application-gateway/waf-policy/policy-setting) Log Scrubbing rules for Sensitive Data Protection:

```CLI

az network application-gateway waf-policy policy-setting update -g <MyResourceGroup> --policy-name <MyPolicySetting> --log-scrubbing-state <Enabled/Disabled> --scrubbing-rules "[{state:<Enabled/Disabled>,match-variable:<MatchVariable>,selector-match-operator:<Operator>,selector:<Selector>}]"

```

---

## Verify Sensitive Data Protection

To verify your Sensitive Data Protection rules, open the Application Gateway firewall log and search for _******_ in place of the sensitive fields.

## Next steps

- [Use Log Analytics to examine Application Gateway Web Application Firewall (WAF) logs](../ag/log-analytics.md)


# Waf Sensitive Data Protection Frontdoor

# What is Azure Web Application Firewall on Azure Front Door sensitive data protection?

The Web Application Firewall's (WAF) log scrubbing tool helps you remove sensitive data from your WAF logs. It works by using a rules engine that allows you to build custom rules to identify specific portions of a request that contain sensitive information. Once identified, the tool scrubs that information from your logs and replaces it with _*******_.

> [!NOTE]

> When you enable the log scrubbing feature, Microsoft still retains IP addresses in our internal logs to support critical security features.

## Default log behavior

Normally, when a WAF rule is triggered, the WAF logs the details of the request in clear text. If the portion of the request triggering the WAF rule contains sensitive data (such as customer passwords or IP addresses), that sensitive data is viewable by anyone with access to the WAF logs. To protect customer data, you can set up Log Scrubbing rules targeting this sensitive data for protection.

## Fields

The following fields can be scrubbed from the logs:

-   Request Header Names

-   Request Cookie Names

-   Request Body Post Arg Names

-   Request Body JSON Arg Names

-   Query String Arg Names

-   Request URI

-   Request IP Address

## Related content

- [How to mask sensitive data on Azure Web Application Firewall for Azure Front Door](waf-sensitive-data-protection-configure-frontdoor.md)

- [Azure Web Application Firewall monitoring and logging](../afds/waf-front-door-monitor.md)

- [A Closer Look at Azure WAF’s Data Masking Capabilities for Azure Front Door](https://techcommunity.microsoft.com/t5/azure-network-security-blog/a-closer-look-at-azure-waf-s-data-masking-capabilities-for-azure/ba-p/4167558)


# Waf Sensitive Data Protection Configure Frontdoor

# How to mask sensitive data on Azure Web Application Firewall on Azure Front Door

The Web Application Firewall's (WAF) Log Scrubbing tool helps you remove sensitive data from your WAF logs. It works by using a rules engine that allows you to build custom rules to identify specific portions of a request that contain sensitive data. Once identified, the tool scrubs that information from your logs and replaces it with _*******_.

> [!NOTE]

> When you enable the log scrubbing feature, Microsoft still retains IP addresses in our internal logs to support critical security features.

The following table shows examples of log scrubbing rules that can be used to protect your sensitive data:

| Match variable | Operator | Selector | What gets scrubbed |

| --- | --- | --- | --- |

| Request Header Names | Equals | keytoblock | {"matchVariableName":"HeaderValue:keytoblock","matchVariableValue":"****"} |

| Request Cookie Names | Equals | cookietoblock | {"matchVariableName":"CookieValue:cookietoblock","matchVariableValue":"****"} |

| Request Body Post Arg Names <sup>1</sup> | Equals | var | {"matchVariableName":"PostParamValue:var","matchVariableValue":"****"} |

| Request Body JSON Arg Names <sup>1</sup> | Equals | JsonValue | {"matchVariableName":"JsonValue:key","matchVariableValue":"****"} |

| Query String Arg Names | Equals | foo | {"matchVariableName":"QueryParamValue:foo","matchVariableValue":"****"} |

| Request IP Address <sup>2</sup> | Equals Any | NULL | {"matchVariableName":"ClientIP","matchVariableValue":"****"} |

| Request URI | Equals Any | NULL | {"matchVariableName":"URI","matchVariableValue":"****"} |

<sup>1</sup> If a request triggers a rule that scans the request body, and the content type is either `application/x-www-form-urlencoded` or `application/json`,  the WAF will scrub all request details from the logs to prevent any potential storage of PII.

<sup>2</sup> Request IP Address and Request URI rules only support the *equals any* operator and scrubs all instances of the requester's IP address that appears in the WAF logs.

For more information, see [What is Azure Web Application Firewall on Azure Front Door Sensitive Data Protection?](waf-sensitive-data-protection-frontdoor.md)

## Enable sensitive data protection

Use the following information to enable and configure Sensitive Data Protection.

#### [Portal](#tab/portal)

To enable Sensitive Data Protection:

1. Open an existing Front Door WAF policy.

1. Under **Settings**, select **Sensitive data**.

1. On the **Sensitive data** page, select **Enable log scrubbing**.

To configure Log Scrubbing rules for Sensitive Data Protection:

1. Under **Log scrubbing rules**, select a **Match variable**.

1. Select an **Operator** (if applicable).

1. Type a **Selector** (if applicable).

1. Select **Save**.

Repeat to add more rules.

#### [PowerShell](#tab/powershell)

Use the following Azure PowerShell commands to create and configure Log Scrubbing rules for Sensitive Data Protection:

```azurepowershell-interactive

New-AzFrontDoorWafLogScrubbingRuleObject -MatchVariable <String> -SelectorMatchOperator <String>

-State <String> [-Selector <String>] [-DefaultProfile <IAzureContextContainer>]

[<CommonParameters>]

New-AzFrontDoorWafLogScrubbingSettingObject -ScrubbingRule <PSFrontDoorWafLogScrubbingRule[]> -State <String>

[-DefaultProfile <IAzureContextContainer>] [<CommonParameters>]

```

#### [Azure CLI](#tab/cli)

Use the following Command Line Interface commands to [create and configure](/cli/azure/network/front-door/waf-policy) Log Scrubbing rules for Sensitive Data Protection:

```azurecli-interactive

az network front-door waf-policy update -g <MyResourceGroup> -n <MyPolicyName> --log-scrubbing "{scrubbing-rules:[{match-variable:<MatchVariable>,selector-match-operator:<Operator>}],state:<Enabled/Disabled>}"

```

---

## Verify sensitive data protection

To verify your Sensitive Data Protection rules, open the Front Door firewall log and search for _******_ in place of the sensitive fields.

## Related content

- [What is Azure Web Application Firewall on Azure Front Door sensitive data protection?](waf-sensitive-data-protection-frontdoor.md)

- [Azure Web Application Firewall monitoring and logging](../afds/waf-front-door-monitor.md)

- [A Closer Look at Azure WAF’s Data Masking Capabilities for Azure Front Door](https://techcommunity.microsoft.com/t5/azure-network-security-blog/a-closer-look-at-azure-waf-s-data-masking-capabilities-for-azure/ba-p/4167558)


# Waf Sentinel

# Using Microsoft Sentinel with Azure Web Application Firewall

Azure Web Application Firewall (WAF) combined with Microsoft Sentinel can provide security information event management for WAF resources. Microsoft Sentinel provides security analytics using Log Analytics, which allows you to easily break down and view your WAF data. Using Microsoft Sentinel, you can access pre-built workbooks and modify them to best fit your organization's needs. The workbook can show analytics for WAF on Azure Content Delivery Network (CDN), WAF on Azure Front Door, and WAF on Application Gateway across several subscriptions and workspaces.

## WAF log analytics categories

WAF log analytics are broken down into the following categories:

- All WAF actions taken

- Top 40 blocked request URI addresses

- Top 50 event triggers,

- Messages over time

- Full message details

- Attack events by messages

- Attack events over time

- Tracking ID filter

- Tracking ID messages

- Top 10 attacking IP addresses

- Attack messages of IP addresses

## WAF workbook examples

The following WAF workbook examples show sample data:

## Launch a WAF workbook

The WAF workbook works for all Azure Front Door, Application Gateway, and CDN WAFs. Before connecting the data from these resources, log analytics must be enabled on your resource.

To enable log analytics for each resource, go to your individual Azure Front Door, Application Gateway, or CDN resource:

1. Select **Diagnostic settings**.

1. Select **+ Add diagnostic setting**.

1. In the Diagnostic setting page:

1. Type a name.

1. Select **Send to Log Analytics**.

1. Choose the log destination workspace.

1. Select the log types that you want to analyze:

1. Application Gateway: ‘ApplicationGatewayAccessLog’ and ‘ApplicationGatewayFirewallLog’

1. Azure Front Door Standard/Premium: ‘FrontDoorAccessLog’ and ‘FrontDoorFirewallLog’

1. Azure Front Door classic: ‘FrontdoorAccessLog’ and ‘FrontdoorFirewallLog’

1. CDN: ‘AzureCdnAccessLog’

1. Select **Save**.

1. On the Azure home page, type *Microsoft Sentinel* in the search bar and select the **Microsoft Sentinel** resource.

1. Select an already active workspace or create a new workspace.

1. In Microsoft Sentinel, under **Content management**, select **Content hub**.

1. Find and select the **Azure Web Application Firewall** solution.

1. On the toolbar at the top of the page, select **Install/Update**.

1. In Microsoft Sentinel, on the left-hand side under **Configuration**, select **Data Connectors**.

1. Search for and select **Azure Web Application Firewall (WAF)**. Select **Open connector page** on the bottom right.

1. Follow the instructions under **Configuration** for each WAF resource that you want to have log analytic data for if you haven't done so previously.

1. Once finished configuring individual WAF resources, select the **Next steps** tab. Select one of the recommended workbooks. This workbook will use all log analytic data that was enabled previously. A working WAF workbook should now exist for your WAF resources.

## Automatically detect and respond to threats

Using Sentinel ingested WAF logs, you can use Sentinel analytics rules to automatically detect security attacks, create security incident, and automatically respond to security incident using playbooks. Learn more [Use playbooks with automation rules in Microsoft Sentinel](/azure/sentinel/tutorial-respond-threats-playbook?tabs=LAC).

Azure WAF also comes in with built-in Sentinel detection rules templates for SQLi, XSS, and Log4J attacks. These templates can be found under the Analytics tab in the 'Rule Templates' section of Sentinel. You can use these templates or define your own templates based on the WAF logs.

The automation section of these rules can help you automatically respond to the incident by running a playbook. An example of such a playbook to respond to attack can be found in network security GitHub repository [here](https://github.com/Azure/Azure-Network-Security/tree/master/Azure%20WAF/Playbook%20-%20WAF%20Sentinel%20Playbook%20Block%20IP%20-%20New). This playbook automatically creates WAF policy custom rules to block the source IPs of the attacker as detected by the WAF analytics detection rules.

## Next steps

- [Learn more about Microsoft Sentinel](/azure/sentinel/overview)

- [Learn more about Azure Monitor Workbooks](/azure/azure-monitor/visualize/workbooks-overview)


# Waf New Threat Detection

# Detect new threats using Microsoft Sentinel with Azure Web Application Firewall

Web applications face frequent malicious attacks that exploit well-known vulnerabilities, such as Code Injection and Path Traversal Attacks. These attacks are hard to prevent in the application code, as they require constant maintenance, patching, and monitoring at multiple levels of the application architecture. A Web Application Firewall (WAF) solution can provide faster and centralized security by patching a known vulnerability for all web applications, rather than securing each one individually. Azure Web Application Firewall is a cloud-native service that protects web apps from common web-hacking techniques. It can be deployed quickly to gain full visibility into the web application traffic and block malicious web attacks.

By integrating Azure WAF with Microsoft Sentinel (a cloud native [SIEM](https://www.microsoft.com/en-us/security/business/security-101/what-is-siem) solution), you can automate the detection and response to threats/incidents/alerts and save time and effort updating the WAF policy. This article shows you how to build Analytic rules/detections in Microsoft Sentinel for attacks such as Code Injection.

## Detection queries for web application attacks

The [Azure Network Security GitHub repository](https://github.com/Azure/Azure-Network-Security/tree/9170800bbb0322ca1c904803954fbb477dff8421/Azure%20WAF/Playbook%20-%20Sentinel%20additional%20detections) contains the following pre-built queries that you can use to create analytic rules in Microsoft Sentinel. These analytic rules help with automated detection and response for attacks like Code Injection, Path Traversal and scanner-based attacks.

- **Code Injection attacks (Application Gateway and Front Door WAF)**

A code injection attack is a type of cyberattack that involves injecting malicious code into an application. The application then interprets or runs the code, affecting the performance and function of the application.

- **Path Traversal attacks (Application Gateway and Front Door WAF)**

A path traversal attack is a type of cyberattack that involves manipulating the file paths of an application to access files and directories that are stored outside the web root folder. The attacker can use special character sequences, such as `…/` or `…\`, to move up the directory hierarchy and access sensitive or confidential data, such as configuration files, source code, or system files.

- **Scanner-based attacks (Application Gateway WAF)**

A scanner-based web attack is a type of cyberattack that involves using a web vulnerability scanner to find and exploit security weaknesses in web applications. A web vulnerability scanner is a tool that automatically scans web applications for common vulnerabilities, such as SQL injection, XSS, CSRF, and path traversal. The attacker can use the scanner to identify the vulnerable targets and launch attacks to compromise them.

## Set up analytic rules in Sentinel for web application attacks

The following prerequisites are required to set up analytic rules:

- A working WAF and a Log Analytics Workspace that is configured to receive logs from the respective Azure Application Gateway or Azure Front Door. For more information, see [Resource logs for Azure Web Application Firewall](ag/web-application-firewall-logs.md).

- Additionally, Microsoft Sentinel should be enabled for the Log Analytics Workspace that is being used here. For more information, see [Quickstart: Onboard Microsoft Sentinel](/azure/sentinel/quickstart-onboard).

Use the following steps to configure an analytic rule in Sentinel:

1. Go to Microsoft Sentinel and select the **Analytics** tab. Select **Create** and then select **Scheduled query rule**.

The tactics and techniques provided here are informational only and are sourced from [MITRE Attack Knowledgebase](https://attack.mitre.org/) This is a knowledge base of adversary tactics and techniques based on real-world observations.

1. You can use the Analytics rule wizard to set a severity level for this incident. Since these are major attacks, High Severity is selected.

1. On the **Set rule logic** page, enter the following prebuilt Code Injection query: You can find this query in the [Azure Network Security GitHub repository](https://github.com/Azure/Azure-Network-Security/blob/9170800bbb0322ca1c904803954fbb477dff8421/Azure%20WAF/Playbook%20-%20Sentinel%20additional%20detections/Code-Injection-AppGW-WAF-CRS3-2.json). Likewise, you can use any other query that is available in the repository to create Analytic rules and detect respective attack patterns.

```

let Threshold = 3;

AzureDiagnostics

| where Category == "ApplicationGatewayFirewallLog"

| where action_s == "Matched"

| where Message has "Injection" or Message has "File Inclusion"

| where ruleGroup_s == "REQUEST-932-APPLICATION-ATTACK-RCE" or ruleGroup_s ==    "REQUEST-931-APPLICATION-ATTACK-RFI" or ruleGroup_s == "REQUEST-932-APPLICATION-ATTACK-RCE" or    ruleGroup_s == "REQUEST-933-APPLICATION-ATTACK-PHP" or ruleGroup_s ==    "REQUEST-942-APPLICATION-ATTACK-SQLI" or ruleGroup_s == "REQUEST-921-PROTOCOL-ATTACK" or ruleGroup_s    == "REQUEST-941-APPLICATION-ATTACK-XSS"

| project transactionId_g, hostname_s, requestUri_s, TimeGenerated, clientIp_s, Message,    details_message_s, details_data_s

| join kind = inner(

AzureDiagnostics

| where Category == "ApplicationGatewayFirewallLog"

| where action_s == "Blocked") on transactionId_g

| extend Uri = strcat(hostname_s,requestUri_s)

| summarize StartTime = min(TimeGenerated), EndTime = max(TimeGenerated), TransactionID = make_set   (transactionId_g,100), Message = make_set(Message,100), Detail_Message = make_set(details_message_s,   100), Detail_Data = make_set(details_data_s,100), Total_TransactionId = dcount(transactionId_g) by    clientIp_s, Uri, action_s

| where Total_TransactionId >= Threshold

```

> [!NOTE]

> It is important to ensure that the WAF logs are already in the Log Analytics workspace before you create this Analytical rule. Otherwise, Sentinel will not recognize some of the columns in the query and you will have to add extra input like `| extend action_s = column_ifexists(“action_s”, “”), transactionId_g = column_ifexists(“transactionId_g”, “”)` for each column that gives an error. This input creates the column names manually and assigns them null values. To skip this step, send the WAF logs to the workspace first.

1. On the **Incident Settings** page, Enable the **Create incidents from alerts triggered by this analytics rule.** The alert grouping can be configured as required.

1. Optionally, you can also add any automated response to the incident if needed. See [Automated detection and response for Azure WAF with Microsoft Sentinel](afds/automated-detection-response-with-sentinel.md) for more detailed information on automated response configuration.

1. Finally, select **Save** on the **Review and create** tab.

This analytic rule enables Sentinel to create an incident based on the WAF logs that record any Code Injection attacks. The Azure WAF blocks these attacks by default, but the incident creation provides more support for the security analyst to respond to future threats.

You can configure Analytic Rules in Sentinel for various web application attacks using the pre-built detection queries available in the [Azure Network Security GitHub repository](https://github.com/Azure/Azure-Network-Security/blob/9170800bbb0322ca1c904803954fbb477dff8421/Azure%20WAF/Playbook%20-%20Sentinel%20additional%20detections/Code-Injection-AppGW-WAF-CRS3-2.json). These queries will be added directly to Sentinel Detection Templates. Once added, these queries will be directly available in the Analytic Rule Templates section of Sentinel.

## Next steps

- [Learn more about Microsoft Sentinel](/azure/sentinel/overview)

- [Learn more about Azure Monitor Workbooks](/azure/azure-monitor/visualize/workbooks-overview)


# Automated Detection Response With Sentinel

# Automated detection and response for Azure WAF with Microsoft Sentinel

Malicious attackers increasingly target web applications by exploiting commonly known vulnerabilities such as SQL injection and Cross-site scripting. Preventing these attacks in application code poses a challenge, requiring rigorous maintenance, patching, and monitoring at multiple layers of the application topology. A Web Application Firewall (WAF) solution can react to a security threat faster by centrally patching a known vulnerability, instead of securing each individual web application. Azure Web Application Firewall (WAF) is a cloud-native service that protects web apps from common web-hacking techniques. You can deploy this service in a matter of minutes to gain complete visibility into the web application traffic and block malicious web attacks.

Integrating Azure WAF with Microsoft Sentinel (a cloud-native SIEM/SOAR solution) for automated detection and response to threats/incidents/alerts is an added advantage and reduces the manual intervention needed to update the WAF policy.

In this article, you learn about WAF detection templates in Sentinel, deploy a playbook, and configure the detection and response in Sentinel using these templates and the playbook.

## Prerequisites

- If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

- An Azure Front Door deployment with an associated WAF policy. For more information, see [Quickstart: Create a Front Door Standard/Premium using an ARM template](../../frontdoor/create-front-door-template.md), and [Tutorial: Create a WAF policy on Azure Front Door by using the Azure portal](waf-front-door-create-portal.md).

- An Azure Front Door configured to capture logs in a Log Analytics workspace. For more information, see [Configure Azure Front Door logs](../../frontdoor/standard-premium/how-to-logs.md).

## Deploy the playbook

You install a Sentinel playbook named *Block-IPAzureWAF* from a template on GitHub. This playbook runs in response to WAF incidents. The goal is to create or modify a custom rule in a WAF policy to block requests from a certain IP address. This is accomplished using the Azure REST API.

You install the playbook from a template on GitHub.

1. Go to the [GitHub repository](https://github.com/Azure/Azure-Network-Security/tree/master/Azure%20WAF/Playbook%20-%20WAF%20Sentinel%20Playbook%20Block%20IP%20-%20New) and select **Deploy to Azure** to launch the template.

1. Fill in the required parameters. You can get your Front Door ID from the Azure portal. The Front Door ID is the resource ID of the Front Door resource.

1. Select **Review + create** and then **Create**.

## Authorize the API connection

An API connection named *azuresentinel-Block-IPAzureWAF* is created as part of this deployment. You must authorize it with your Azure ID to allow the playbook to make changes to your WAF policy.

1. In the Azure portal, select the *azuresentinel-Block-IPAzureWAF* API connection.

1. Select **Edit API connection**.

1. Under **Display Name**, type your Azure ID.

1. Select **Authorize**.

1. Select **Save**.

## Configure the Contributor role assignment

The playbook must have the necessary permissions to query and modify the existing WAF policy via the REST API.  You can assign the playbook a system-assigned Managed Identity with Contributor permissions on the Front Door resource along with their associated WAF policies. You can assign permissions only if your account has been assigned Owner or User Access Administrator roles to the underlying resource.

This can be done using the IAM section in the respective resource by adding a new role assignment to this playbook.

1. In the Azure portal, select the Front Door resource.

1. In the left pane, select **Access control (IAM)**.

1. Select **Role assignments**.

1. Select **Add** then **Add role assignment**.

1. Select **Privileged administrator roles**.

1. Select **Contributor** and then select **Next**.

1. Select **Select members**.

1. Search for **Block-IPAzureWAF** and select it. There may be multiple entries for this playbook. The one you recently added usually the last one in the list.

1. Select **Block-IPAzureWAF** and select **Select**.

1. Select **Review + assign**.

Repeat this procedure for the WAF policy resource.

## Add Microsoft Sentinel to your workspace

1. In the Azure portal, search for and then open Microsoft Sentinel.

1. Select **Create**.

1. Select your workspace, and then select **Add**.

## Configure the Logic App Contributor role assignment

Your account must have owner permissions on any resource group to which you want to grant Microsoft Sentinel permissions, and you must have the **Logic App Contributor** role on any resource group containing playbooks you want to run.

1. In the Azure portal, select the resource group that contains the playbook.

1. In the left pane, select **Access control (IAM)**.

1. Select **Role assignments**.

1. Select **Add** then **Add role assignment**.

1. Select search for **Logic App Contributor**, select it, and then select **Next**.

1. Select **Select members**.

1. Search for your account and select it.

1. Select **Select**.

1. Select **Next**.

1. Select **Review + assign**.

## Configure detection and response

There are detection query templates for SQLi and XSS attacks in Sentinel for Azure WAF. You can download these templates from the Content hub. By using these templates, you can create analytic rules that detect specific type of attack patterns in the WAF logs and further notify the security analyst by creating an incident. The automation section of these rules can help you respond to this incident by blocking the source IP of the attacker on the WAF policy, which then stops subsequent attacks upfront from these source IP addresses. Microsoft is continuously working to include more Detection Templates for more detection and response scenarios.

### Install the templates

1. From Microsoft Sentinel, under **Configuration** in the left pane, select **Analytics**.

1. At the top of the page, select **More content at Content hub**.

1. Search for **Azure Web Application Firewall**, select it and then select **Install**.

### Create an analytic rule

1. From Microsoft Sentinel, under **Configuration** in the left pane, select **Analytics**.

1. Select **Rule templates**. It may take a few minutes for the templates to appear.

1. Select the **Front Door Premium WAF - SQLi Detection** template.

1. On the right pane, select **Create rule**.

1. Accept all the defaults and continue through to **Automated response**. You can edit these settings later to customize the rule.

> [!TIP]

> If you see an error in the rule query, it might be because you don't have any WAF logs in your workspace. You can generate some logs by sending test traffic to your web app. For example, you can simulate a SQLi attack by sending a request like this: `http://x.x.x.x/?text1=%27OR%27%27=%27`. Replace `x.x.x.x` with your Front Door URL.

1. On the **Automated response** page, select **Add new**.

1. On the **Create new automation rule** page, type a name for the rule.

1. Under **Trigger**, select **When alert is created**.

1. Under **Actions**, select **Manage playbook permissions**.

1. On the **Manage permissions** page, select your resource group and select **Apply**.

1. Back on the **Create new automation rule** page, under **Actions** select the **Block-IPAzureWAF** playbook from the drop down list.

1. Select **Apply**.

1. Select **Next: Review + create**.

1. Select **Save**.

Once the Analytic rule is created with respective Automation rule settings, you're now ready for *Detection and Response*. The following flow of events happens during an attack:

- Azure WAF logs traffic when an attacker attempts to target one of the web apps behind it. Sentinel then ingests these logs.

- The Analytic/Detection rule that you configured detects the pattern for this attack and generates an incident to notify an analyst.

- The automation rule that is part of the analytic rule triggers the respective playbook that you configured previously.

- The playbook creates a custom rule called *SentinelBlockIP* in the respective WAF policy, which includes the source IP of the attacker.

- WAF blocks subsequent attack attempts, and if the attacker tries to use another source IP, it appends the respective source IP to the block rule.

An important point is that by default Azure WAF blocks any malicious web attacks with the help of core ruleset of the Azure WAF engine. However, this automated detection and response configuration further enhances the security by modifying or adding new custom block rules on the Azure WAF policy for the respective source IP addresses. This ensures that the traffic from these source IP addresses gets blocked before it even hits the Azure WAF engine ruleset.

## Related content

- [Using Microsoft Sentinel with Azure Web Application Firewall](../waf-sentinel.md)


# Application Ddos Protection

# Application (Layer 7) DDoS protection

Azure WAF includes several defense mechanisms that help prevent distributed denial of service (DDoS) attacks. DDoS attacks can target both the network layer (L3/L4) and the application layer (L7). Azure DDoS Protection defends you against large network layer volumetric attacks. Azure WAF, operating at layer 7, protects web applications against L7 DDoS attacks such as HTTP floods. These defenses prevent attackers from reaching your application and affecting your application's availability and performance.

## How can you protect your services?

Mitigate these attacks by adding a Web Application Firewall (WAF) or placing DDoS Protection in front of the service to filter out bad requests. Azure offers WAF running at the network edge with Azure Front Door and in data centers with Application Gateway. Adjust these steps to fit your application requirements.

- Deploy [Azure Web Application Firewall (WAF)](../overview.md) with Azure Front Door Premium or Application Gateway WAF v2 SKU to protect against L7 application layer attacks.

- Scale up your origin instance count so that there's sufficient spare capacity.

- Enable [Azure DDoS Protection](../../ddos-protection/ddos-protection-overview.md) on the origin public IPs to protect your public IPs against layer 3 (L3) and layer 4 (L4) DDoS attacks. Azure’s DDoS offerings automatically protect most sites from L3 and L4 volumetric attacks that send large numbers of packets towards a website. Azure also offers infrastructure level protection to all sites hosted on Azure by default.

## Azure WAF with Azure Front Door

Azure WAF includes many features that you can use to mitigate different types of attacks, like HTTP floods, cache bypass, and attacks launched by botnets.

- Use the bot protection managed rule set to protect against known bad bots. For more information, see [Configuring bot protection](../afds/waf-front-door-policy-configure-bot-protection.md).

- Apply rate limits to prevent IP addresses from calling your service too frequently. For more information, see [Rate limiting](../afds/waf-front-door-rate-limit.md).

- Block IP addresses and ranges that you identify as malicious. For more information, see [IP restrictions](../afds/waf-front-door-configure-ip-restriction.md).

- Block or redirect to a static web page any traffic from outside a defined geographic region, or within a defined region that doesn't fit the application traffic pattern. For more information, see [Geo-filtering](../afds/waf-front-door-geo-filtering.md).

- Create [custom WAF rules](../afds/waf-front-door-custom-rules.md) to automatically block and rate limit HTTP or HTTPS attacks that have known signatures. Signatures include a specific user-agent or a specific traffic pattern, such as headers, cookies, query string parameters, or a combination of multiple signatures.

Beyond WAF, Azure Front Door also offers default Azure infrastructure DDoS protection to protect against L3/L4 DDoS attacks. Enabling caching on Azure Front Door can help absorb sudden peak traffic volume at the edge and protect backend origins from attack as well.

For more information on features and DDoS protection on Azure Front Door, see [DDoS protection on Azure Front Door](../../frontdoor/front-door-ddos.md).

## Azure WAF with Azure Application Gateway

Use the Application Gateway WAF v2 SKU, which includes the latest features such as L7 DDoS mitigation features, to protect against L7 DDoS attacks.

You can use Application Gateway WAF SKUs to mitigate many L7 DDoS attacks:

- Set your Application Gateway to autoscale and don't enforce the number of max instances.

- Use the bot protection managed rule set to protect against known bad bots. For more information, see [Configuring bot protection](../ag/bot-protection.md).

- Apply rate limits to prevent IP addresses from calling your service too frequently. For more information, see [Configuring Rate limiting custom rules](../ag/rate-limiting-configure.md).

- Block IP addresses and ranges that you identify as malicious. For more information, see examples at [Create and use v2 custom rules](../ag/create-custom-waf-rules.md).

- Block or redirect to a static web page any traffic from outside a defined geographic region, or within a defined region that doesn't fit the application traffic pattern. For more information, see examples at [Create and use v2 custom rules](../ag/create-custom-waf-rules.md).

- Create [custom WAF rules](../ag/configure-waf-custom-rules.md) to automatically block and rate limit HTTP or HTTPS attacks that have known signatures. Signatures include a specific user-agent or a specific traffic pattern that includes headers, cookies, query string parameters, or a combination of multiple signatures.

## Other considerations

- Lock down access to public IPs on origin and restrict inbound traffic to only allow traffic from Azure Front Door or Application Gateway to origin. Refer to the [guidance on Azure Front Door](../../frontdoor/front-door-faq.yml#what-are-the-steps-to-restrict-the-access-to-my-backend-to-only-azure-front-door-). Ensure there aren't any publicly exposed IP addresses in the Application Gateway's virtual network.

- Switch WAF policy to the prevention mode. Deploying the policy in detection mode operates in the log only and doesn't block traffic. After verifying and testing your WAF policy with production traffic and fine tuning to reduce any false positives, turn policy to prevention mode (block/defend mode).

- Monitor traffic using Azure WAF logs for any anomalies. You can create custom rules to block any offending traffic – suspected IPs sending unusually high number of requests, unusual user-agent string, anomalous query string patterns, and more.

- You can bypass the WAF for known legitimate traffic by creating Match Custom Rules with the action of Allow to reduce false positives. Configure these rules with a high priority (lower numeric value) than other block and rate limit rules.

- At a minimum, have a rate limit rule that blocks high rate of requests from any single IP address. For example, you can configure a rate limit rule to not allow any single *Client IP address* to send more than XXX traffic per window to your site. Azure WAF supports two windows for tracking requests, one and five minutes. Use the five-minute window for better mitigation of HTTP Flood attacks. This rule should be the lowest priority rule (priority is ordered with 1 being the highest priority), so that more specific Rate Limit rules or Match rules can be created to match before this rule. If you're using Application Gateway WAF v2, you can use other rate limiting configurations to track and block clients by methods other than Client IP. More information on rate limits on Application Gateway WAF can be found at [Rate limiting overview](../ag/rate-limiting-overview.md).

The following Log Analytics query can be helpful in determining the threshold you should use for the previous rule. For a similar query but with Application Gateway, replace `FrontdoorAccessLog` with `ApplicationGatewayAccessLog`.

```

AzureDiagnostics

| where Category == "FrontdoorAccessLog"

| summarize count() by bin(TimeGenerated, 5m), clientIp_s

| summarize max(count_), percentile(count_, 99), percentile(count_, 95)

```

- Managed rules, while not directly targeted for defenses against DDoS attacks, provide protection against other common attacks. For more information, see [Managed rules (Azure Front Door)](../afds/waf-front-door-drs.md) or [Managed rules (Application Gateway)](../ag/application-gateway-crs-rulegroups-rules.md) to learn more about various attack types these rules can help protect against.

## WAF log analysis

You can analyze WAF logs in Log Analytics using the following query.

### Azure Front Door

```

AzureDiagnostics

| where Category == "FrontdoorWebApplicationFirewallLog"

```

For more information, see [Azure WAF with Azure Front Door](../afds/waf-front-door-monitor.md).

### Azure Application Gateway

```

AzureDiagnostics

| where Category == "ApplicationGatewayFirewallLog"

```

For more information, see [Azure WAF with Azure Application Gateway](../ag/web-application-firewall-logs.md).

## Related content

- [Create a WAF policy](../afds/waf-front-door-create-portal.md) for Azure Front Door.

- [Create an Application Gateway](../ag/application-gateway-web-application-firewall-portal.md) with a Web Application Firewall.

- Learn how Azure Front Door can help [protect against DDoS attacks](../../frontdoor/front-door-ddos.md).

- Protect your application gateway with [Azure DDoS Network Protection](../../application-gateway/tutorial-protect-application-gateway-ddos.md).

- Learn more about the [Azure DDoS Protection](../../ddos-protection/ddos-protection-overview.md).


# Waf Javascript Challenge

# Azure Web Application Firewall JavaScript challenge

Azure Web Application Firewall (WAF) on Azure Application Gateway offers a JavaScript (JS) challenge feature as one of the mitigation options for advanced bot protection.

Azure Web Application Firewall (WAF) on Azure Front Door offers a JavaScript (JS) challenge feature as one of the mitigation options for advanced bot protection. It's available on the premium version as an action in the custom rule set and the Bot Manager 1.x ruleset.

The JavaScript challenge is an invisible web challenge that distinguishes between legitimate users and bots. Malicious bots fail the challenge, protecting your web applications. Additionally, the JavaScript challenge reduces friction for legitimate users because it doesn't require human intervention.

> [!IMPORTANT]

> Azure Web Application Firewall JavaScript challenge on Azure Application Gateway is currently in PREVIEW.

> See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## How it works

When the JavaScript challenge is active on Azure WAF and a client's HTTP(S) request matches a specific rule, the client is shown a Microsoft JavaScript challenge page. The user sees this page for a few seconds while the browser computes the challenge. If the user's browser successfully computes the challenge, it sends a response back to an Azure endpoint that's exposed when you have WAF configured. This endpoint is exposed to the public, however, requests sent to this endpoint aren't forwarded to the backend and don't count towards rate limiting features. If the browser's call to this endpoint contains the correct values indicating a successful computation, the user passes the challenge.

The client's browser must successfully compute a JavaScript challenge on this page to receive validation from Azure WAF. When the computation succeeds, WAF validates the request as a nonbot client and runs the rest of the WAF rules. Requests that fail to successfully compute the challenge are blocked.

Cross-origin resource sharing (CORS) requests are challenged on each access attempt. So if a client accesses a page that triggers the JavaScript challenge from a domain different from the domain hosting the challenge, the client faces the challenge again even if the client previously passed the challenge.

In addition, if a client solves the JavaScript challenge and then the client's IP address changes, the challenge is issued again.

Here's an example JavaScript challenge page:

## Expiration

The WAF policy setting defines the JavaScript challenge cookie validity lifetime in minutes. The user is challenged after the lifetime expires. The lifetime is an integer between 5 and 1,440 minutes and the default is 30 minutes. The JavaScript challenge cookie name is `appgw_azwaf_jsclearance` on Azure Application Gateway.

The WAF policy setting defines the JavaScript challenge cookie validity lifetime in minutes. The user is challenged after the lifetime expires. The lifetime is an integer between 5 and 1,440 minutes and the default is 30 minutes. The JavaScript challenge cookie name is `afd_azwaf_jsclearance` on Azure Front Door.

> [!NOTE]

> The JavaScript challenge expiration cookie is injected into the user's browser after successfully completing the challenge.

## Limitations

- **AJAX and API calls aren't supported**: JavaScript challenge doesn't apply to AJAX and API requests.

- **POST body size restriction**: The first request that triggers a JavaScript challenge is blocked if its POST body exceeds 128 KB on Azure Application Gateway.

- **POST body size restriction**: The first request that triggers a JavaScript challenge is blocked if its POST body exceeds 64 KB on Azure Front Door.

- **Non-HTML embedded resources**: JavaScript challenge is designed for HTML resources. Challenges for non-HTML resources embedded in a page, such as images, CSS, JavaScript files, or similar resources, aren't supported. However, if there was a prior successful JavaScript challenge request, those limitations are lifted.

- **Browser compatibility**: JavaScript challenge isn't supported on Microsoft Internet Explorer. It's compatible with the latest versions of Microsoft Edge, Chrome, Firefox, and Safari web browsers.

- **Rate limit isn't supported**: The JavaScript challenge action on Application Gateway isn't supported for *Rate Limit* type custom rules during the preview.

- **Application Gateway for Containers WAF**: Application Gateway for Containers WAF doesn't support JavaScript challenge.

## Related content

- [Front Door Web Application Firewall CAPTCHA](./afds/captcha-challenge.md)

- [Configure a custom response for Front Door WAF](./afds/waf-front-door-configure-custom-response-code.md)

- [Azure WAF’s Bot Manager 1.1 and JavaScript Challenge: Navigating the Bot Threat Terrain](https://techcommunity.microsoft.com/t5/azure-network-security-blog/azure-waf-s-bot-manager-1-1-and-javascript-challenge-preview/ba-p/4249652)


# Captcha Challenge

# Azure Front Door Web Application Firewall CAPTCHA

**Applies to:** :heavy_check_mark: Front Door Premium

Azure Web Application Firewall (WAF) offers a CAPTCHA feature designed to differentiate human users from automated bots. This interactive challenge requires suspected traffic to complete a CAPTCHA test, blocking malicious automated requests while allowing legitimate users to proceed seamlessly. As a result, WAF helps protect applications from bot-driven attacks, including brute-force attempts and account takeover risks.

CAPTCHA on Azure WAF is useful in login and sign-up flows where human authentication is crucial to protect sensitive user data. It acts as a strong defense against various automated threats, preventing bots from accessing critical website elements like login pages and forms, and reducing spam by ensuring only real users can submit comments, register accounts, or complete transactions.

Incorporating CAPTCHA into Azure WAF not only enhances security but also minimizes friction for legitimate users. This balance strengthens the overall protection of web applications against sophisticated automated threats.

> [!NOTE]

> The CAPTCHA feature incurs additional usage-based charges. For detailed information on pricing, see [Azure Front Door pricing](https://azure.microsoft.com/pricing/details/frontdoor/).

## How it works

When the CAPTCHA challenge is active on Azure WAF, any client's HTTP(s) request matches a specific rule prompts an interactive Microsoft CAPTCHA page. This challenge requires user participation to verify they're human before their request is validated by Azure WAF. Upon successful completion, WAF recognizes the request as originating from a legitimate user, and proceeds with standard rule processing. Requests that fail to complete the challenge are blocked, thus preventing automated bots from accessing protected resources.

## Expiration

The WAF **Policy settings** define the CAPTCHA challenge cookie validity lifetime in minutes, determining how long a user remains validated before facing a new challenge. Once the lifetime expires, the user must complete the CAPTCHA challenge again to verify their identity. The lifetime is configurable between 5 and 1,440 minutes, with a default setting of 30 minutes. The CAPTCHA challenge cookie name is `afd_azwaf_captcha` on Azure Front Door.

> [!NOTE]

> The CAPTCHA challenge expiration cookie is injected into the user’s browser after successfully completing the challenge.

## Limitations

- **Mobile Apps**: Not supported.

- **AJAX and API calls aren't supported**: CAPTCHA verification doesn't apply to AJAX and API requests.

- **POST body size restriction**: The first request that triggers a CAPTCHA challenge is blocked if its POST body exceeds 64 KB on Azure Front Door.

- **Non-HTML embedded resources**: CAPTCHA is designed for HTML resources. Placing CAPTCHA in front of non-HTML resources, such as images, CSS, or JavaScript files, may likely result in issues with content loading and rendering.

- **Browser compatibility**: CAPTCHA isn't supported on Microsoft Internet Explorer. It's compatible with the latest versions of Microsoft Edge, Chrome, Firefox, and Safari.

## Related content

- [Web Application Firewall JavaScript challenge](/azure/web-application-firewall/waf-javascript-challenge)

- [Configure a custom response for Front Door WAF](/azure/web-application-firewall/afds/waf-front-door-configure-custom-response-code)


# Best Practices

# Best practices for Azure Web Application Firewall (WAF) on Azure Application Gateway

**Applies to:** :heavy_check_mark: Application Gateway V2

This article summarizes the best practices for using Azure Web Application Firewall (WAF) on Azure Application Gateway.

## General best practices

### Enable the WAF

For internet-facing applications, enable a web application firewall (WAF) and configure it to use managed rules. When you use a WAF and Microsoft-managed rules, you protect your application from a range of attacks.

### Use WAF policies

WAF policies are the new resource type for managing your Application Gateway WAF. If you have older WAFs that use WAF configuration resources, migrate to WAF policies to take advantage of the latest features.

For more information, see the following resources:

- [Upgrade to Azure Application Gateway WAF policy](./upgrade-ag-waf-policy.md)

- [Upgrade Web Application Firewall policies using Azure PowerShell](./migrate-policy.md)

- [Upgrade Application Gateway WAF configuration to WAF policy using Azure Firewall Manager](../shared/manage-policies.md#upgrade-application-gateway-waf-configuration-to-waf-policy)

### Tune your WAF

Tune the rules in your WAF for your workload. If you don't tune your WAF, it might accidentally block requests that should be allowed. Tuning might involve creating [rule exclusions](application-gateway-waf-configuration.md) to reduce false positive detections.

While you tune your WAF, consider using [detection mode](create-waf-policy-ag.md#configure-waf-rules-optional), which logs requests and the actions the WAF would normally take, but doesn't actually block any traffic.

For more information, see [Troubleshoot Web Application Firewall (WAF) for Azure Application Gateway](web-application-firewall-troubleshoot.md).

### Use prevention mode

After you tune your WAF, configure it to [run in **prevention** mode](create-waf-policy-ag.md#configure-waf-rules-optional). By running in **prevention** mode, you ensure the WAF actually blocks requests that it detects as malicious. Running in **detection** mode is useful for testing purposes while you tune and configure your WAF but it provides no protection. It logs the traffic, but it doesn't take any actions such as *allow* or *deny*.

### Define your WAF configuration as code

When you tune your WAF for your application workload, you typically create a set of rule exclusions to reduce false positive detections. If you manually configure these exclusions by using the Azure portal, then when you upgrade your WAF to use a newer ruleset version, you need to reconfigure the same exceptions against the new ruleset version. This process can be time-consuming and error-prone.

Instead, consider defining your WAF rule exclusions and other configurations as code, such as by using the Azure CLI, Azure PowerShell, Bicep, or Terraform. Then, when you need to update your WAF ruleset version, you can easily reuse the same exclusions.

## Managed ruleset best practices

### Enable core rule sets

Microsoft's core rule sets are designed to protect your application by detecting and blocking common attacks. The rules are based on various sources including the OWASP top 10 attack types and information from Microsoft Threat Intelligence.

For more information, see [Web Application Firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).

### Enable bot management rules

Bots are responsible for a significant proportion of traffic to web applications. The WAF's bot protection rule set categorizes bots based on whether they're good, bad, or unknown. Bad bots can then be blocked, while good bots like search engine crawlers are allowed through to your application.

For more information, see [Azure Web Application Firewall on Azure Application Gateway bot protection overview](bot-protection-overview.md).

### Use the latest ruleset versions

Microsoft regularly updates the managed rules to take account of the current threat landscape. Ensure that you regularly check for updates to Azure-managed rule sets.

For more information, see [Web Application Firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).

## Geo-filtering best practices

### Geo-filter traffic

Many web applications are designed for users within a specific geographic region. If this situation applies to your application, consider implementing geo-filtering to block requests that come from outside of the countries or regions you expect to receive traffic from.

For more information, see [Geomatch custom rules](geomatch-custom-rules.md).

## Logging

### Add diagnostic settings to save your WAF's logs

Application Gateway's WAF integrates with Azure Monitor. It's important to enable the diagnostic settings and save the WAF logs to a destination like Log Analytics. You should review the WAF logs regularly. Reviewing logs helps you to [tune your WAF policies to reduce false-positive detections](#tune-your-waf), and to understand whether your application was the subject of attacks.

For more information, see [Azure Web Application Firewall Monitoring and Logging](application-gateway-waf-metrics.md).

### Send logs to Microsoft Sentinel

Microsoft Sentinel is a security information and event management (SIEM) system that imports logs and data from multiple sources to understand the threat landscape for your web application and overall Azure environment. You should import Application Gateway's WAF logs into Microsoft Sentinel or another SIEM so that your internet-facing properties are included in its analysis. For Microsoft Sentinel, use the Azure WAF connector to easily import your WAF logs.

For more information, see [Using Microsoft Sentinel with Azure Web Application Firewall](../waf-sentinel.md).

## Related content

- [Web Application Firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md)

- [Web Application Firewall exclusion lists](application-gateway-waf-configuration.md)

- [Web Application Firewall (WAF) v2 custom rules on Application Gateway](custom-waf-rules-overview.md)


# Application Gateway Waf Metrics

# Azure Web Application Firewall Monitoring and Logging

**Applies to:** :heavy_check_mark: Application Gateway

Azure Web Application Firewall (WAF) monitoring and logging are provided through logging and integration with Azure Monitor and Azure Monitor logs.

## Azure Monitor

WAF with Application Gateway log is integrated with [Azure Monitor](/azure/azure-monitor/overview). Azure Monitor allows you to track diagnostic information including WAF alerts and logs. You can configure WAF monitoring within the Application Gateway resource in the portal under the **Diagnostics** tab or through the Azure Monitor service directly.

## Logs and diagnostics

WAF with Application Gateway provides detailed reporting on each threat it detects. Logging is integrated with Azure Diagnostics logs and alerts are recorded in a json format. These logs can be integrated with [Azure Monitor logs](/previous-versions/azure/azure-monitor/insights/azure-networking-analytics).

For more information about diagnostics logs, see [Application Gateway WAF resource logs](../ag/web-application-firewall-logs.md). If logging is enabled and a WAF rule is triggered, any matching patterns are logged in plain text to help you analyze and debug the WAF policy behavior. You can use exclusions to fine tune rules and exclude any data that you want to be excluded from the logs. For more information, see [Web application firewall exclusion lists in Azure Application Gateway](../ag/application-gateway-waf-configuration.md).

## Application Gateway WAF v2 Metrics

New WAF metrics are only available for Core Rule Set 3.2 or greater, or with bot protection and geo-filtering. The metrics can be further filtered on the supported dimensions.

|**Metrics**|**Description**|**Dimension**|

| :------------------| :-------------------------------------| :-----------------|

|**WAF Total Requests**|Count of successful requests that WAF engine has served| Action, Country/Region, Method, Mode, Policy Name, Policy Scope|

|**WAF Managed Rule Matches**|Count of total managed rule matches| Action, Country/Region, Mode, Policy Name, Policy Scope, Rule Group, Rule ID, Rule Set Name|

|**WAF Custom Rule Matches**|Count of custom rule matches| Action, Country/Region, Mode, Policy Name, Policy Scope, Rule Name|

|**WAF Bot Protection Matches**<sup>1</sup>|Count of total bot protection rule matches that have been blocked or logged from malicious IP addresses. The IP addresses are sourced from the Microsoft Threat Intelligence feed.| Action, Country/Region, Bot Type, Mode, Policy Name, Policy Scope|

|**WAF JS Challenge Request Count**<sup>3</sup>|Count the number of requests that match JS Challenge WAF rules.|Action, Policy Name, Policy Scope, Rule<sup>2</sup>|

<sup>1</sup> Only Bot Manager Rule Set 0.1 will be displayed under “WAF Bot Protection Matches”. Requests matching Bot Manager Rule Set 1.0 will increase “WAF Total Requests” metrics, not “WAF Bot Protection Matches”.

<sup>2</sup> Rule name for custom rules and Rule ID for the Bot Manager Rule Set.

<sup>3</sup> Application Gateway for Containers WAF does not support JavaScript challenge.

For metrics supported by Application Gateway V2 SKU, see [Application Gateway v2 metrics](../../application-gateway/application-gateway-metrics.md#metrics-supported-by-application-gateway-v2-sku)

## Application Gateway WAF v1 Metrics

|**Metrics**|**Description**|**Dimension**|

| :------------------| :-------------------------------------| :-----------------|

|**Web Application Firewall Blocked Requests Count**|Count of total requests that have been blocked by the WAF engine||

|**Web Application Firewall Blocked Requests Distribution**|Total number of rules hit distribution for the blocked requests by Rule Group and Rule ID|Rule Group, Rule ID|

|**Web Application Firewall Total Rule Distribution**|Count of total matched requests distribution by Rule Group and Rule ID |Rule Group, Rule ID|

For metrics supported by Application Gateway V1 SKU, see [Application Gateway v1 metrics](../../application-gateway/monitor-application-gateway-reference.md#metrics-for-application-gateway-v1-sku)

## Access WAF Metrics in Azure portal

1. From the Azure portal menu, select **All Resources** >> **\<your-Application-Gateway-profile>**.

2. Under **Monitoring**, select **Metrics**:

3. In **Metrics**, select the metric to add:

4. Select Add filter to add a filter:

5. Select New chart to add a new chart

## Configure Alerts in Azure portal

1. Set up alerts on Azure Application Gateway by selecting **Monitoring** >> **Alerts**.

1. Select **New alert rule** for metrics listed in Metrics section.

Alert will be charged based on Azure Monitor. For more information about alerts, see [Azure Monitor alerts](/azure/azure-monitor/alerts/alerts-overview).

## Next steps

- Learn about [Web Application Firewall](../overview.md).

- Learn about [Web Application Firewall Logs](../ag/web-application-firewall-logs.md).


# Insights

# Azure Application Gateway Web Application Firewall (WAF) Insights (preview)

> [!IMPORTANT]

> The WAF Insights for Azure Application Gateway is currently in PREVIEW.

> See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

The WAF Insights dashboards for Azure Application Gateway provide a unified experience for monitoring, investigation, and reporting of WAF activity. They help security and operations teams detect attack patterns, validate WAF policy effectiveness, identify misconfigurations, and accelerate incident response through deep drill-down analysis. By combining high-level visibility with detailed request-level insights, the dashboards support both strategic monitoring and hands-on troubleshooting.

The solution includes two main dashboards:

**Monitor tab** - designed for continuous visibility. It surfaces high-level metrics and trends such as total request volumes, managed rule matches, custom rule matches, and JavaScript challenge activity. The Monitor tab helps operators detect anomalies, track the effectiveness of WAF protections, and understand overall application security posture at a glance.

**Triage tab** - designed for investigation. It provides drill-down views to identify affected hosts, URLs, requests, and rules involved in a specific security event. This supports root cause analysis and faster incident response.

## Prerequisites

To view WAF data in the dashboards, **Diagnostic Settings** must be enabled for the Application Gateway associations you want to monitor. Without diagnostic logs, no WAF data will be available in the dashboards. To learn more about how to enable diagnostic settings, see [Monitor logs for Azure Web Application Firewall](/azure/web-application-firewall/ag/web-application-firewall-logs?tabs=AppGW) and [Diagnostic logs - Azure Application Gateway](/azure/application-gateway/application-gateway-diagnostics)

## Azure workbooks

Both dashboards are implemented as Azure Monitor workbooks, allowing customization, exploration, and extension of visualizations based on operational and security needs.

## Data sources and architecture

The dashboards combine **Metrics** and **Logs**, which complement each other:

| Source | Description | Retention | Best for |

|----|----|----|----|

| **Metrics** | Aggregated counters collected at minute intervals. Optimized for trend analysis. | Controlled by Azure Monitor metrics retention settings. | Near real-time anomaly detection, activity trends. |

| **Logs (Azure diagnostics)** | Full per-request event data from WAF diagnostic logging. | Controlled by Log Analytics Workspace retention policy. | Deep forensic investigation, compliance, and auditing. |

> [!IMPORTANT]

> - Metrics are ideal for fast anomaly detection but don't contain full request details.

> - Logs contain full forensic information but may take longer to query for large datasets.

## Dashboard structure

The WAF Insights experience is divided into two main tabs:

- **Monitor** - High-level reporting and trend tracking.

- **Triage** - Drill-down investigations of events.

Each tab offers a different perspective and is often used together: monitor overall health in the **Monitor tab**, then use the **Triage tab** to investigate anomalies.

### Monitor tab

The Monitor tab provides visibility and reporting through two main views – **WAF logs** and **WAF metrics**.

The **WAF logs** view gives a detailed request-level perspective sourced from the AzureDiagnostics table in LAW. It includes visualizations such as total WAF requests by rule group, WAF actions by type (for example, Blocked), top blocked URIs, top triggered rules, rules over time, and details of triggered rule events with timestamps, hosts, AppGW instances, and client IPs. Analysts can also correlate data by tracking ID, review top offending IPs, and inspect related requests to detect targeted attacks, validate rule effectiveness, and support audits or compliance reviews.

The **WAF metrics** view provides near real-time visibility into WAF activity using Azure Monitor metrics. It includes visualizations showing total WAF requests, managed rule matches by association (both blocked and non-blocked), JS challenge request counts, and custom rule matches. This data helps detect sudden traffic surges, monitor rule behavior, evaluate JS challenge enforcement, and verify correct policy configuration. Metrics offer an operational perspective that complements the detailed forensic insights provided by logs.

### Triage tab

The Triage tab is built for investigation and troubleshooting of WAF events. It uses data from AzureDiagnostics within the Log Analytics Workspace (LAW) and supports two investigation modes: **Triage by Rule** and **Triage by URL**.

Except for the first visualization, each component dynamically filters based on selections from the previous step, allowing a natural drill-down flow that narrows from a broad scope to specific impacted requests.

#### Triage by rule

In **Triage by Rule**, investigation starts from a triggered rule. The flow begins with selecting the WAF policy scope (Listener, URI Path, or Global). Next, you can view an overview of triggered rules, including rule ID, action, ruleset version, scope, and the number of impacted requests. From there, the investigation drills down to the affected hosts, URLs, and individual transactions. This approach helps identify which rules are responsible for most of the blocked traffic, detect false positives, and understand which hosts and URLs are most affected.

#### Triage by URL

In **Triage by URL**, investigation begins with a URL path. Analysts select the relevant Application Gateway and policy scope, identify the hosts or IPs targeting specific URLs, and view the rules triggered for those impacted requests. This approach is useful for investigating suspicious activity on sensitive endpoints such as login pages, verifying whether blocked requests are legitimate or malicious, and mapping attack patterns across URLs.

## Summary of dashboards

| **Dashboard** | **Purpose** | **Investigation flow** | **Example use cases** |

|----|----|----|----|

| **Monitor - WAF logs** | Log-based monitoring | Pulls structured data from LAW | Validate policy effectiveness, perform audits, investigate requests |

| **Monitor - WAF metrics** | Metric-based monitoring | Uses Azure Monitor metrics | Near real-time monitoring, detect anomalies, track trends |

| **Triage by rule** | Investigate by rule ID | Scope → Rule → Hosts → URLs → Requests | Identify noisy rules, analyze blocks, fine-tune rules |

| **Triage by URL** | Investigate by URL path | Scope → URL → Hosts → Rules → Requests | Investigate attacks on sensitive endpoints, validate rule effectiveness |

## Glossary

**Association**: The binding between a WAF policy and an Application Gateway listener or path.

**Scope**: The level at which a WAF policy applies (Listener, URI Path, Global).

**Rule ID**: Identifier of a managed rule triggered by the WAF.

**LAW (Log Analytics workspace)**: Repository where logs are stored and queried.

**Metrics**: Aggregated counters optimized for fast monitoring.

## Limitations and considerations

- **Latency:** Metrics are near real-time, but Logs may have ingestion delay (typically 1-5 minutes).

- **Retention:** Ensure Log Analytics retention is configured to match compliance/audit needs.

- **Scale:** Large volumes of diagnostic logs can increase query latency and storage costs.

- **Resource-specific mode:** Resource-specific tables are currently not supported. The solution relies on Diagnostic settings streaming to Log Analytics in Azure Diagnostics mode only.

## Best practices

- Always enable **both metrics and logs** to balance visibility and detail.

- Use the **Monitor tab daily** for operational awareness, and the **Triage tab on demand** during incidents.

- Periodically review *noisy rules* in the **Triage by rule** view to fine-tune WAF configuration.

- Configure alerts on **sudden spikes** in WAF metrics (for example, challenge requests or blocked requests).

- Align dashboard use with **incident response workflows**, ensuring security and networking teams collaborate using the same views.

## Related content

- [Monitor Azure Application Gateway](/azure/application-gateway/monitor-application-gateway)

- [Examining logs using Azure Log Analytics - Azure Application Gateway](/azure/application-gateway/log-analytics)

- [Diagnostic logs - Azure Application Gateway](/azure/application-gateway/application-gateway-diagnostics)

- [Azure Monitor metrics for Application Gateway](/azure/application-gateway/application-gateway-metrics)

- [Azure Workbooks overview - Azure Monitor](/azure/azure-monitor/visualize/workbooks-overview)

- [Monitoring metrics for Azure Application Gateway Web Application Firewall](/azure/web-application-firewall/ag/application-gateway-waf-metrics)

- [Monitor logs for Azure Web Application Firewall](/azure/web-application-firewall/ag/web-application-firewall-logs?tabs=AppGW)


# Log Analytics

# Use Log Analytics to examine Application Gateway Web Application Firewall (WAF) logs

Once your Application Gateway WAF is operational, you can enable logs to inspect what is happening with each request. Firewall logs give insight to what the WAF is evaluating, matching, and blocking. With Azure Monitor Log Analytics, you can examine the data inside the firewall logs to give even more insights. For more information about creating a Log Analytics workspace, see [Create a Log Analytics workspace in the Azure portal](/azure/azure-monitor/logs/quick-create-workspace). For more information about log queries, see [Overview of log queries in Azure Monitor](/azure/azure-monitor/logs/log-query-overview).

## Import WAF logs

To import your firewall logs into Log Analytics, see [Back-end health, resource logs, and metrics for Application Gateway](../../application-gateway/application-gateway-diagnostics.md#diagnostic-logging). When you have the firewall logs in your Log Analytics workspace, you can view data, write queries, create visualizations, and add them to your portal dashboard.

## Explore data with examples

To view the raw data in the firewall log, you can run the following query:

```

AzureDiagnostics

| where ResourceProvider == "MICROSOFT.NETWORK" and Category == "ApplicationGatewayFirewallLog"

```

This will look similar to the following query:

You can drill down into the data, and plot graphs or create visualizations from here. See the following queries as a starting point:

### Matched/Blocked requests by IP

```

AzureDiagnostics

| where ResourceProvider == "MICROSOFT.NETWORK" and Category == "ApplicationGatewayFirewallLog"

| summarize count() by clientIp_s, bin(TimeGenerated, 1m)

| render timechart

```

### Matched/Blocked requests by URI

```

AzureDiagnostics

| where ResourceProvider == "MICROSOFT.NETWORK" and Category == "ApplicationGatewayFirewallLog"

| summarize count() by requestUri_s, bin(TimeGenerated, 1m)

| render timechart

```

### Top matched rules

```

AzureDiagnostics

| where ResourceProvider == "MICROSOFT.NETWORK" and Category == "ApplicationGatewayFirewallLog"

| summarize count() by ruleId_s, bin(TimeGenerated, 1m)

| where count_ > 10

| render timechart

```

### Top five matched rule groups

```

AzureDiagnostics

| where ResourceProvider == "MICROSOFT.NETWORK" and Category == "ApplicationGatewayFirewallLog"

| summarize Count=count() by details_file_s, action_s

| top 5 by Count desc

| render piechart

```

## Add to your dashboard

Once you create a query, you can add it to your dashboard.  Select the **Pin to dashboard** in the top right of the log analytics workspace. With the previous four queries pinned to an example dashboard, this is the data you can see at a glance:

![Screenshot shows an Azure dashboard where you can add your query.](../media/log-analytics/dashboard.png)

## Next steps

[Back-end health, resource logs, and metrics for Application Gateway](../../application-gateway/application-gateway-diagnostics.md)


# Waf Front Door Best Practices

# Best practices for Azure Web Application Firewall in Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Premium

This article summarizes best practices for using Azure Web Application Firewall in Azure Front Door.

## General best practices

This section discusses general best practices.

### Enable the WAF

For internet-facing applications, enable a web application firewall (WAF) and configure it to use managed rules. When you use a WAF and Microsoft-managed rules, you protect your application from a range of attacks.

### Tune your WAF

Tune the rules in your WAF for your workload. If you don't tune your WAF, it might accidentally block requests that should be allowed. Tuning might involve creating [rule exclusions](waf-front-door-exclusion.md) to reduce false positive detections.

While you tune your WAF, consider using [detection mode](waf-front-door-policy-settings.md#waf-mode). This mode logs requests and the actions the WAF would normally take, but it doesn't actually block any traffic.

For more information, see [Tune Azure Web Application Firewall for Azure Front Door](waf-front-door-tuning.md).

### Use prevention mode

After you tune your WAF, configure it to [run in prevention mode](waf-front-door-policy-settings.md#waf-mode). By running in prevention mode, you ensure that the WAF blocks requests that it detects are malicious. Running in detection mode is useful while you tune and configure your WAF, but it provides no protection.

### Define your WAF configuration as code

When you tune your WAF for your application workload, you typically create a set of rule exclusions to reduce false positive detections. If you manually configure these exclusions by using the Azure portal, when you upgrade your WAF to use a newer rule-set version, you need to reconfigure the same exceptions against the new rule-set version. This process can be time consuming and error prone.

Instead, consider defining your WAF rule exclusions and other configuration as code, such as by using the Azure CLI, Azure PowerShell, Bicep, or Terraform. When you need to update your WAF rule-set version, you can easily reuse the same exclusions.

## Managed rule-set best practices

This section discusses best practices for rule sets.

### Enable default rule sets

Microsoft's default rule sets are designed to protect your application by detecting and blocking common attacks. The rules are based on various sources, including the OWASP top-10 attack types and information from Microsoft Threat Intelligence.

For more information, see [Azure-managed rule sets](afds-overview.md#azure-managed-rule-sets).

### Enable bot management rules

Bots are responsible for a significant proportion of traffic to web applications. The WAF's bot protection rule set categorizes bots based on whether they're good, bad, or unknown. Bad bots can then be blocked, while good bots like search engine crawlers are allowed through to your application.

For more information, see [Bot protection rule set](afds-overview.md#bot-protection-rule-set).

### Use the latest rule set versions

Microsoft regularly updates the managed rules to take account of the current threat landscape. Ensure that you regularly check for updates to Azure-managed rule sets.

For more information, see [Azure Web Application Firewall DRS rule groups and rules](waf-front-door-drs.md).

## Rate limiting best practices

This section discusses best practices for rate limiting.

### Add rate limiting

The Azure Front Door WAF enables you to control the number of requests allowed from each client's IP address over a period of time. Add rate limiting to reduce the effect of clients accidentally or intentionally sending large amounts of traffic to your service, such as during a [retry storm](/azure/architecture/antipatterns/retry-storm/).

For more information, see the following resources:

- [What is rate limiting for Azure Front Door?](waf-front-door-rate-limit.md)

- [Configure an Azure Web Application Firewall rate limit rule by using Azure PowerShell](waf-front-door-rate-limit-configure.md).

- [Why do additional requests above the threshold configured for my rate limit rule get passed to my back-end server?](waf-faq.yml#why-do-additional-requests-above-the-threshold-configured-for-my-rate-limit-rule-get-passed-to-my-back-end-server-)

### Use a high threshold for rate limits

Set your rate limit threshold to be high. For example, if you know that a single client IP address might send around 10 requests to your server each minute, consider specifying a threshold of 20 requests per minute.

High rate-limit thresholds avoid blocking legitimate traffic. These thresholds still provide protection against very high numbers of requests that might overwhelm your infrastructure.

## Geo-filtering best practices

This section discusses best practices for geo-filtering.

### Geo-filter traffic

Many web applications are designed for users within a specific geographic region. If this situation applies to your application, consider implementing geo-filtering to block requests that come from outside of the countries or regions from which you expect to receive traffic.

For more information, see [What is geo-filtering on a domain for Azure Front Door?](waf-front-door-tutorial-geo-filtering.md)

### Specify the unknown (ZZ) location

Some IP addresses aren't mapped to locations in the dataset. When an IP address can't be mapped to a location, the WAF assigns the traffic to the unknown (ZZ) country or region. To avoid blocking valid requests from these IP addresses, consider allowing the unknown (ZZ) country or region through your geo-filter.

For more information, see [What is geo-filtering on a domain for Azure Front Door?](waf-front-door-tutorial-geo-filtering.md)

## Logging

This section discusses logging.

### Add diagnostic settings to save your WAF's logs

The Azure Front Door WAF integrates with Azure Monitor. It's important to save the WAF logs to a destination like Log Analytics. Review the WAF logs regularly. Reviewing logs helps you to [tune your WAF policies to reduce false-positive detections](#tune-your-waf) and to understand whether your application is the subject of attacks.

For more information, see [Azure Web Application Firewall monitoring and logging](waf-front-door-monitor.md).

### Send logs to Microsoft Sentinel

Microsoft Sentinel is a security information and event management (SIEM) system that imports logs and data from multiple sources to help you understand the threat landscape for your web application and overall Azure environment. Import Azure Front Door WAF logs into Microsoft Sentinel or another SIEM so that your internet-facing properties are included in its analysis. For Microsoft Sentinel, use the Azure WAF connector to easily import your WAF logs.

For more information, see [Use Microsoft Sentinel with Azure Web Application Firewall](../waf-sentinel.md).

## Related content

- [Create an Azure Front Door WAF policy](waf-front-door-create-portal.md)

- [Tune Azure Web Application Firewall for Azure Front Door](waf-front-door-tuning.md)

- [Azure Web Application Firewall DRS rule groups and rules](waf-front-door-drs.md)


# Waf Front Door Monitor

# Azure Web Application Firewall monitoring and logging

**Applies to:** :heavy_check_mark: Front Door Standard/Premium :heavy_check_mark: Front Door (classic)

Azure Web Application Firewall on Azure Front Door provides extensive logging and telemetry to help you understand how your web application firewall (WAF) is performing and the actions it takes.

The Azure Front Door WAF log is integrated with [Azure Monitor](/azure/azure-monitor/overview). Azure Monitor enables you to track diagnostic information, including WAF alerts and logs. You can configure WAF monitoring within the Azure Front Door resource in the Azure portal under the **Diagnostics** tab, through infrastructure as code approaches, or by using Azure Monitor directly.

## Metrics

Azure Front Door automatically records metrics to help you understand the behavior of your WAF.

To access your WAF's metrics:

1. Sign in to the [Azure portal](https://portal.azure.com) and go to your Azure Front Door profile.

1. On the leftmost pane under **Monitoring**, select the **Metrics** tab.

1. Add the **Web Application Firewall Request Count** metric to track the number of requests that match WAF rules.

You can create custom filters based on action types and rule names. Metrics include requests with terminating actions like `Block` and `Allow` as well as requests where the WAF took no action. Since multiple non-terminating `Log` actions can be triggered by a single request, they are excluded from this metric to avoid duplicating request counts.

## JavaScript challenge (preview) metrics

To access your JavaScript challenge WAF metrics:

- Add the Web Application Firewall `JS Challenge Request Count` metric to track the number of requests that match JavaScript challenge WAF rules.

The following filters are provided as part of this metric:

- **PolicyName**: This is the WAF policy name

- **Rule**: This can be any custom rule or bot rule

- **Action**: There are four possible values for JS Challenge action

- **Issued**:  JS Challenge is invoked the first time

- **Passed**: JS Challenge computation succeeded and an answer was received

- **Valid**: JS Challenge validity cookie was present

- **Blocked**: JS Challenge computation failed

## Logs and diagnostics

The Azure Front Door WAF provides detailed reporting on each request and each threat that it detects. Logging is integrated with Azure's diagnostics logs and alerts by using [Azure Monitor logs](/azure/azure-monitor/insights/azure-networking-analytics).

Logs aren't enabled by default. You must explicitly enable logs. You can configure logs in the Azure portal by using the **Diagnostic settings** tab.

If logging is enabled and a WAF rule is triggered, any matching patterns are logged in plain text to help you analyze and debug the WAF policy behavior. You can use exclusions to fine-tune rules and exclude any data that you want to be excluded from the logs. For more information, see [Web application firewall exclusion lists in Azure Front Door](../afds/waf-front-door-exclusion.md).

You can enable three types of Azure Front Door logs:

- WAF logs

- Access logs

- Health probe logs

Activity logs are enabled by default and provide visibility into the operations performed on your Azure resources, such as configuration changes to your Azure Front Door profile.

### WAF logs

The log `FrontDoorWebApplicationFirewallLog` includes requests that match a WAF rule.

The log `FrontdoorWebApplicationFirewallLog` includes any request that matches a WAF rule.

The following table shows the values logged for each request.

| Property  | Description |

| ------------- | ------------- |

| Action |Action taken on the request. Logs include requests with all actions. Actions are:<ul> <li>`Allow` and `allow`: The request was allowed to continue processing.</li> <li>`Block` and `block`: The request matched a WAF rule configured to block the request. Alternatively, the [anomaly scoring](waf-front-door-drs.md#anomaly-scoring-mode) threshold was reached and the request was blocked.</li> <li>`Log` and `log`: The request matched a WAF rule configured to use the `Log` action.</li> <li> `AnomalyScoring` and `logandscore`: The request matched a WAF rule. The rule contributes to the [anomaly score](waf-front-door-drs.md#anomaly-scoring-mode). The request might or might not be blocked depending on other rules that run on the same request.</li> <li> `JS Challenge` and `JSChallengeIssued`: Issued due to missing/invalid challenge clearance, missing answer.<br><br>The log is created when a client requests access to a web application for the first time and has not been challenged previously. This client receives the JS challenge  page and proceeds to compute the JS challenge. Upon successful computation, the client is granted the validity cookie.</li> <li>`JS Challenge` and `JSChallengePass`:  Passed due to valid challenge answer.<br><br>This log is created when a client solves the JS challenge and resubmits the request with the correct answer. In this case, Azure WAF validates the cookie and proceeds to process the remaining rules without generating another JS challenge.</li> <li> `JS Challenge` and `JSChallengeValid`: Logged/passthrough due to valid challenge.<br><br>This log is created when a client has previously solved a challenge. In this case, Azure WAF logs the request and proceeds to process the remaining rules.</li><li>`JS Challenge` and `JSChallengeBlock`: Blocked<br><br>This log is created when a JS challenge computation fails.</ul> |

| ClientIP | The IP address of the client that made the request. If there was an `X-Forwarded-For` header in the request, the client IP address is taken from that header field instead. |

| ClientPort | The IP port of the client that made the request. |

| Details | More details on the request, including any threats that were detected. <br />`matchVariableName`: HTTP parameter name of the request matched, for example, header names (up to 100 characters maximum).<br /> `matchVariableValue`: Values that triggered the match (up to 100 characters maximum). |

| Host | The `Host` header of the request. |

| Policy | The name of the WAF policy that processed the request. |

| PolicyMode | Operations mode of the WAF policy. Possible values are `Prevention` and `Detection`. |

| RequestUri | Full URI of the request. |

| RuleName | The name of the WAF rule that the request matched. |

| SocketIP | The source IP address seen by WAF. This IP address is based on the TCP session and doesn't consider any request headers. |

| TrackingReference | The unique reference string that identifies a request served by Azure Front Door. This value is sent to the client in the `X-Azure-Ref` response header. Use this field when you search for a specific request in the log. |

The following example query shows the requests that the Azure Front Door WAF blocked:

```kusto

AzureDiagnostics

| where ResourceProvider == "MICROSOFT.CDN" and Category == "FrontDoorWebApplicationFirewallLog"

| where action_s == "Block"

```

```kusto

AzureDiagnostics

| where ResourceType == "FRONTDOORS" and Category == "FrontdoorWebApplicationFirewallLog"

| where action_s == "Block"

```

The following snippet shows an example log entry, including the reason that the request was blocked:

```json

{

"time": "2020-06-09T22:32:17.8376810Z",

"category": "FrontdoorWebApplicationFirewallLog",

"operationName": "Microsoft.Cdn/Profiles/Write",

"properties": {

"clientIP": "xxx.xxx.xxx.xxx",

"clientPort": "52097",

"socketIP": "xxx.xxx.xxx.xxx",

"requestUri": "https://wafdemofrontdoorwebapp.azurefd.net:443/?q=%27%20or%201=1",

"ruleName": "Microsoft_DefaultRuleSet-1.1-SQLI-942100",

"policy": "WafDemoCustomPolicy",

"action": "Block",

"host": "wafdemofrontdoorwebapp.azurefd.net",

"trackingReference": "08Q3gXgAAAAAe0s71BET/QYwmqtpHO7uAU0pDRURHRTA1MDgANjMxNTAwZDAtOTRiNS00YzIwLTljY2YtNjFhNzMyOWQyYTgy",

"policyMode": "prevention",

"details": {

"matches": [

{

"matchVariableName": "QueryParamValue:q",

"matchVariableValue": "' or 1=1"

}

]

}

}

}

```

```json

{

"time": "2020-06-09T22:32:17.8376810Z",

"category": "FrontdoorWebApplicationFirewallLog",

"operationName": "Microsoft.Network/FrontDoorWebApplicationFirewallLog/Write",

"properties": {

"clientIP": "xxx.xxx.xxx.xxx",

"clientPort": "52097",

"socketIP": "xxx.xxx.xxx.xxx",

"requestUri": "https://wafdemofrontdoorwebapp.azurefd.net:443/?q=%27%20or%201=1",

"ruleName": "Microsoft_DefaultRuleSet-1.1-SQLI-942100",

"policy": "WafDemoCustomPolicy",

"action": "Block",

"host": "wafdemofrontdoorwebapp.azurefd.net",

"trackingReference": "08Q3gXgAAAAAe0s71BET/QYwmqtpHO7uAU0pDRURHRTA1MDgANjMxNTAwZDAtOTRiNS00YzIwLTljY2YtNjFhNzMyOWQyYTgy",

"policyMode": "prevention",

"details": {

"matches": [

{

"matchVariableName": "QueryParamValue:q",

"matchVariableValue": "' or 1=1"

}

]

}

}

}

```

For more information about the other Azure Front Door logs, see [Monitor metrics and logs in Azure Front Door](../../frontdoor/front-door-diagnostics.md#logs).

## Related content

- [Best practices for Azure Front Door WAF](waf-front-door-best-practices.md)

- [Create a WAF policy on Azure Front Door](waf-front-door-create-portal.md)

- [Azure Web Application Firewall on Azure Front Door](afds-overview.md)


# Support Help

# Support and troubleshooting for Azure Web Application Firewall

Here are suggestions for where you can get help when developing your Azure Web Application Firewall (WAF) solutions.

## Self help troubleshooting

Various articles explain how to determine, diagnose, and fix issues that you might encounter when using Azure Web Application Firewall. Use these articles to troubleshoot connectivity problems, performance issues, circuit configuration, and more.

For a full list of self help troubleshooting content, see [Azure Web Application Firewall troubleshooting documentation](/troubleshoot/azure/web-application-firewall/welcome-azure-web-application-firewall).

## Post a question on Microsoft Q&A

For quick and reliable answers on your technical product questions from Microsoft Engineers, Azure Most Valuable Professionals (MVPs), or our expert community, engage with us on [Microsoft Q&A](/answers/products/azure), Azure's preferred destination for community support.

If you can't find an answer to your problem using search, submit a new question to Microsoft Q&A. Use the [azure-web-application-firewall](/answers/topics/azure-web-application-firewall.html) tag when asking your question:

## Create an Azure support request

Explore the range of [Azure support options and choose the plan](https://azure.microsoft.com/support/plans) that best fits, whether you're a developer just starting your cloud journey or a large organization deploying business-critical, strategic applications. Azure customers can create and manage support requests in the Azure portal.

- If you already have an Azure Support Plan, [open a support request here](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest).

- To sign up for a new Azure Support Plan, [compare support plans](https://azure.microsoft.com/support/plans/) and select the plan that works for you.

## Create a GitHub issue

If you need help with the language and tools used to develop and manage Azure Web Application Firewall, open an issue in its repository on GitHub.

| Library | GitHub issues URL|

| --- | --- |

| Azure PowerShell | https://github.com/Azure/azure-powershell/issues |

| Azure CLI | https://github.com/Azure/azure-cli/issues |

| Azure REST API | https://github.com/Azure/azure-rest-api-specs/issues |

| Azure SDK for Java | https://github.com/Azure/azure-sdk-for-java/issues |

| Azure SDK for Python | https://github.com/Azure/azure-sdk-for-python/issues |

| Azure SDK for .NET | https://github.com/Azure/azure-sdk-for-net/issues |

| Azure SDK for JavaScript | https://github.com/Azure/azure-sdk-for-js/issues |

| Terraform | https://github.com/Azure/terraform/issues |

## Stay informed of updates and new releases

Learn about important product updates, roadmap, and announcements in [Azure Web Application Firewall Updates](https://azure.microsoft.com/updates/?filters=%5B"Web+Application+Firewall"%5D).

News and information about Azure Web Application Firewall is shared at the [Azure blog](https://azure.microsoft.com/blog/).

## Next step

> [!div class="nextstepaction"]

> [Azure Web Application Firewall](index.yml)
