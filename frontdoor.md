# Front Door Overview

# What is Azure Front Door?

Whether you're delivering content and files or developing global applications and APIs, Azure Front Door enhances your user experience by providing higher availability, reduced latency, increased scalability, and improved security. It provides these benefits no matter where your users are located.

Azure Front Door is an advanced content delivery network (CDN) for the cloud. It's designed to provide fast, reliable, and secure access to your applications' static and dynamic web content globally. By using Microsoft's extensive global edge network, Azure Front Door provides efficient content delivery through [global and local points of presence (PoPs)](edge-locations-by-region.md) strategically positioned close to both enterprise and consumer users.

[!INCLUDE [ddos-waf-recommendation](../../includes/ddos-waf-recommendation.md)]

Azure Front Door is one of the services in the category of load-balancing and content delivery services in Azure. Other services in this category include [Azure Load Balancer](../load-balancer/load-balancer-overview.md) and [Azure Application Gateway](../application-gateway/overview.md). Each service has its own unique features and use cases. For more information on this service category, see [What is load balancing and content delivery?](../networking/load-balancer-content-delivery/load-balancing-content-delivery-overview.md)

## Why use Azure Front Door?

> [!VIDEO https://www.youtube.com/embed/-4FQYxV9mAE]

Azure Front Door enables internet-facing applications to:

* *Build and operate modern internet-first architectures* that have dynamic, high-quality digital experiences with highly automated, secure, and reliable platforms.

* *Accelerate and deliver your applications and content globally* at scale to your users wherever they are. This ability creates opportunities for you to compete and quickly adapt to new demand and markets.

* *Help secure your digital estate* against known and new threats with intelligent security that embraces a Zero Trust framework.

## What are the key benefits?

### Global delivery scale through the Microsoft network

Scale out and improve the performance of your applications and content by using Microsoft's global cloud CDN and wide area network (WAN):

* Take advantage of more than [118 edge locations](edge-locations-by-region.md) across 100 metro areas connected to Azure by using a private enterprise-grade WAN. Improve latency for applications by up to three times.

* Accelerate application performance by using the Azure Front Door [anycast](front-door-traffic-acceleration.md#select-the-front-door-edge-location-for-the-request-anycast) network and [split TCP](front-door-traffic-acceleration.md#connect-to-the-front-door-edge-location-split-tcp) connections.

* Terminate SSL offload at the edge and use integrated [certificate management](standard-premium/how-to-configure-https-custom-domain.md).

* Natively support end-to-end IPv6 connectivity and the HTTP/2 protocol.

### Delivery of modern apps and architectures

Modernize your internet-first applications on Azure with cloud-native experiences:

* Integrate with DevOps-friendly command-line tools across SDKs of different languages, Bicep, Azure Resource Manager templates, the Azure CLI, and PowerShell.

* Define your own [custom domain](standard-premium/how-to-add-custom-domain.md) with flexible domain validation.

* Load balance and route traffic across [origins](origin.md). Use intelligent [health probe](health-probes.md) monitoring across apps or content hosted in Azure or anywhere.

* Integrate with other Azure services, such as Azure DNS, the Web Apps feature of Azure App Service, Azure Storage, and many more for domain and origin management.

* Move your routing business logic to the edge with [enhanced rules engine](front-door-rules-engine.md) capabilities, including regular expressions and server variables.

* Analyze [built-in reports](standard-premium/how-to-reports.md) with an all-in-one dashboard for both Azure Front Door and security patterns.

* [Monitor your Azure Front Door traffic in real time](standard-premium/how-to-monitor-metrics.md), and configure alerts that integrate with Azure Monitor.

* [Log each Azure Front Door request](standard-premium/how-to-logs.md) and failed health probes.

### Simplicity and cost-effectiveness

* Unified static and dynamic delivery offered in a single tier to accelerate and scale your application through caching, SSL offload, and layer 3-4 DDoS protection.

* Free, [autorotation-managed SSL certificates](end-to-end-tls.md) that save time and help quickly secure apps and content.

* Low entry fee and a simplified cost model that reduces billing complexity by having fewer meters to plan for.

* Integrated egress pricing that removes the separate egress charge from Azure regions to Azure Front Door. For more information, see [Azure Front Door pricing](https://azure.microsoft.com/pricing/details/frontdoor/).

### Intelligent, secure internet perimeter

* Help secure applications with built-in layer 3-4 DDoS protection, a seamlessly attached [WAF](../web-application-firewall/afds/afds-overview.md), and [Azure DNS to help protect your domains](how-to-configure-endpoints.md).

* Help protect your applications against layer 7 DDoS attacks by using a WAF. For more information, see [Application DDoS protection](../web-application-firewall/shared/application-ddos-protection.md).

* Help protect your applications from malicious actors with bot manager rules based on Microsoft Threat Intelligence.

* Privately connect to your origin behind Azure Front Door by using [Azure Private Link](private-link.md), and embrace a Zero Trust access model.

* Provide a centralized security experience for your application via Azure Policy and Azure Advisor that provides consistent security features across apps.

## How do you choose between Azure Front Door tiers?

For a comparison of supported features in Azure Front Door, see [Tier comparison](standard-premium/tier-comparison.md).

## Where is the service available?

Azure Front Door Standard, Premium, and Classic tiers are available in Microsoft Azure (Commercial) and Microsoft Azure Government (US).

## What's the pricing?

For pricing information, see [Azure Front Door pricing](https://azure.microsoft.com/pricing/details/frontdoor/). For information about service-level agreement (SLA), see [Microsoft SLA for online services](https://www.microsoft.com/licensing/docs/view/Service-Level-Agreements-SLA-for-Online-Services).

## What's new?

Subscribe to the RSS feed, and view the latest Azure Front Door feature updates on the [Azure Updates](https://azure.microsoft.com/updates?filters=%5B%22Azure+Front+Door%22%5D) page.

## Related content

* Learn about [Azure Front Door routing architecture](front-door-routing-architecture.md).

* Learn how to [create an Azure Front Door profile](create-front-door-portal.md).


# Create Front Door Portal

# Quickstart: Create an Azure Front Door using the Azure portal

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

This quickstart shows you how to create an Azure Front Door profile by using the Azure portal. You can create an Azure Front Door profile by using either Quick create or Custom create. The Quick create option helps you configure the basic settings of your profile, while the Custom create option enables you to customize your profile with more advanced settings.

In this quickstart, use the Custom create option to create an Azure Front Door profile. First, deploy two App Services as your origin servers. Then, configure the Azure Front Door profile to route traffic to your App Services based on certain rules. Finally, test the connectivity to your App Services by accessing the Azure Front Door frontend hostname.

[!INCLUDE [ddos-waf-recommendation](../../includes/ddos-waf-recommendation.md)]

## Prerequisites

An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Create an Azure Front Door profile

#### [Quick create](#tab/quick)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Go to the home page or the Azure menu and select **+ Create a resource**. Enter *Front Door and CDN profiles* in the search box and select **Create**.

1. On **Compare offerings**, select **Quick create**, and then select **Continue to create a Front Door**.

1. On **Create a Front Door profile**, enter the following information:

| Setting | Description |

| --- | --- |

| **Subscription**  | Select your subscription. |

| **Resource group**  | Select **Create new** and enter *myAFDResourceGroup*.|

| **Name** | Enter a name for your profile, such as **myAzureFrontDoor**. |

| **Tier** | Select either Standard or Premium. Standard is optimized for content delivery, while Premium focuses on security. See [Tier Comparison](standard-premium/tier-comparison.md). |

| **Endpoint name** | Enter a globally unique name for your endpoint. |

| **Origin type** | Select the type of resource for your origin. For this example, select an App service with Private Link enabled. |

| **Origin host name** | Enter the hostname for your origin. |

| **Private link** (Premium only) | Enable private link service for a private connection between Azure Front Door and your origin. Supported origins include internal load balancers, Azure Storage Blobs, Azure App services, and Azure Storage Static Website. See [Private Link service with Azure Front Door](private-link.md). |

| **Caching** | Select the check box to cache content closer to users globally by using Azure Front Door's edge POPs and the Microsoft network. |

| **WAF policy** | Select **Create new** or choose an existing WAF policy from the dropdown to enable this feature. |

> [!NOTE]

> When you create a new Azure Front Door profile, you can only select an origin from the same subscription where you create the Front Door.

1. Select **Review + Create** and then **Create** to deploy your Azure Front Door profile.

> [!NOTE]

> * It can take a few minutes for the Azure Front Door configuration to propagate to all edge POPs.

> * If you enabled Private Link, go to the origin's resource page, select **Networking** > **Configure Private Link**, select the pending request from Azure Front Door, and then select **Approve**. After a few seconds, your origin is accessible through Azure Front Door securely.

#### [Custom create](#tab/custom)

Create an Azure Front Door profile by using *Custom create* and deploy two App services that your Azure Front Door profile uses as your origins.

### Create two Web App instances

If you already have services to use as an origin, skip to [create a Front Door for your application](#create-a-front-door-for-your-application).

This example demonstrates how to create two Web App instances deployed in different Azure regions. Both web application instances operate in an active/active mode, meaning they can both handle incoming traffic. This configuration differs from an active/standby configuration, where one instance serves as a backup for the other.

To create the two Web Apps for this example, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com).

1. To start creating the first Web App, select the **+ Create a resource** button on the top left corner of the portal. Then, type *Web App* in the search box and select **Create** to proceed with the configuration.

1. On the **Create Web App** page, fill in the required information on the **Basics** tab.

| Setting | Description |

|--|--|

| **Subscription** | Select your subscription. |

| **Resource group** | Select **Create new** and enter *myAppResourceGroup* in the text box. |

| **Name** | Enter a unique **Name** for your web app. This example uses *webapp-contoso-001*. |

| **Publish** | Select **Code**. |

| **Runtime stack** | Select **.NET Core 3.1 (LTS)**. |

| **Operating System** | Select **Windows**. |

| **Region** | Select **Central US**. |

| **Windows Plan** | Select **Create new** and enter *myAppServicePlanCentralUS* in the text box. |

| **Sku and size** | Select **Standard S1 100 total ACU, 1.75-GB memory**. |

1. To complete the creation of the Web App, select **Review + create** button and verify the summary of the settings. Then, select the **Create** button to start the deployment process, which can take up to a minute.

1. To create a second Web App, follow the same steps as for the first Web App, but make the following changes in the settings:

| Setting | Description |

|--|--|

| **Resource group** | Select **Create new** and enter *myAppResourceGroup2*. |

| **Name** | Enter a unique name for your Web App, in this example, *webapp-contoso-002*. |

| **Region** | A different region, in this example, *South Central US* |

| **App Service plan** > **Windows Plan** | Select **New** and enter *myAppServicePlanSouthCentralUS*, and then select **OK**. |

### Create a Front Door for your application

In this step, you configure Azure Front Door to route user traffic to the nearest Web App origin based on latency. Additionally, you apply a Web Application Firewall (WAF) policy to protect your Azure Front Door from malicious attacks.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. From the home page or the Azure menu, select **+ Create a resource**, search for *Front Door and CDN profiles*, and select **Create**.

1. In the *Endpoint* tab, select **Add an endpoint**, enter a globally unique name (for example, contoso-frontend), and select **Add**. You can create more endpoints after the initial deployment.

1. To configure routing to your Web App origin, select **+ Add a route**.

1. On the **Add a route** page, enter or select the following information and then select **Add** to add the route to the endpoint configuration.

| Setting | Description |

|--|--|

| **Name** | Provide a name that identifies the mapping between domains and origin group. |

| **Domains** | The system generates a domain name for you to use. To add a custom domain, select **Add a new domain**. This example uses the default domain name. |

| **Patterns to match** | Specify the URLs that this route accepts. This example uses the default setting, which accepts all URL paths. |

| **Accepted protocols** | Choose the protocol that the route accepts. This example accepts both HTTP and HTTPS requests. |

| **Redirect** | Turn on this setting to redirect all HTTP requests to the HTTPS endpoint. |

| **Origin group** | To create a new origin group, select **Add a new origin group** and enter *myOriginGroup* as the origin group name. Then select **+ Add an origin** and enter *WebApp1* for the **Name** and *App services* for the **Origin Type**. In the **Host name**, select *webapp-contoso-001.azurewebsites.net* and select **Add** to add the origin to the origin group. Repeat the steps to add the second Web App as an origin with *WebApp2* as the **Name** and *webapp-contoso-002.azurewebsites.net* as the **Host name**. Choose a **priority** for each origin, with the lowest number having the highest priority. If you need Azure Front Door to serve both origins, use a priority of 1. Choose a weight for each origin, with the weight determining how traffic is routed to the origins. Use equal weights of 1000 if the traffic needs to be routed to both origins equally. Once both Web App origins are added, select **Add** to save the origin group configuration. |

| **Origin path** | Leave this field empty. |

| **Forwarding protocol** | Choose the protocol that the origin group receives. This example uses the same protocol as the incoming requests. |

| **Caching** | Select the check box if you want to use Azure Front Door’s edge POPs and the Microsoft network to cache contents closer to your users globally. |

| **Rules** | After deploying the Azure Front Door profile, you can use Rules to customize your route. |

1. Select **+ Add a policy** to apply a Web Application Firewall (WAF) policy to one or more domains in the Azure Front Door profile.

1. To create a security policy, provide a name that uniquely identifies it. Next, choose the domains that you want to apply the policy to. You can also select an existing WAF policy or create a new one. To finish, select **Save** to add the security policy to the endpoint configuration.

1. To deploy the Azure Front Door profile, select **Review + Create** and then **Create**. The configuration propagates to all edge locations within a few minutes.

---

## Verify Azure Front Door

The global deployment of the Azure Front Door profile takes a few minutes to complete. After that, you can access the frontend host by entering its endpoint hostname in a browser. For example, `contoso-frontend.z01.azurefd.net`. The request is automatically routed to the closest server among the specified servers in the origin group.

To test the instant global failover feature, follow these steps if you created the apps in this quickstart. You see an information page with the app details.

1. Enter the endpoint hostname in a browser, for example, `contoso-frontend.z01.azurefd.net`.

1. In the Azure portal, search for and select **App services**. Locate one of your Web Apps, such as **WebApp-Contoso-001**.

1. Select the Web App from the list and then select **Stop**. Confirm your action by selecting **Yes**.

1. Reload the browser to see the information page again.

> [!TIP]

> Traffic may take some time to switch to the second Web App. You might need to reload the browser again.

1. To stop the second Web App, select it from the list and then choose **Stop**. Confirm your action by selecting **Yes**.

1. Reload the web page. You should encounter an error message after the refresh.

## Clean up resources

If you no longer need the environment, delete all the resources you created. Deleting a resource group also removes all its contents. To avoid incurring unnecessary charges, delete these resources if you don't plan to use this Azure Front Door.

1. In the Azure portal, search for and select **Resource groups**, or go to **Resource groups** from the Azure portal menu.

1. Use the filter option or scroll down the list to locate the resource groups, such as **myAFDResourceGroup**, **myAppResourceGroup**, or **myAppResourceGroup2**.

1. Select the resource group you want to delete, and then choose the **Delete** option.

> [!WARNING]

> Deleting a resource group is irreversible. You can't recover the resources within the resource group once deleted.

1. Enter the name of the resource group to confirm, and then select the **Delete** button.

1. Repeat these steps for the remaining resource groups.

## Next steps

Proceed to the next article to learn how to configure a custom domain for your Azure Front Door.

> [!div class="nextstepaction"]

> [Add a custom domain](standard-premium/how-to-add-custom-domain.md)


# Edge Locations By Region

# Azure Front Door POP locations by metro

**Applies to:** :heavy_check_mark: Front Door Standard/Premium :heavy_check_mark: Front Door (classic) :heavy_check_mark: CDN Standard from Microsoft (classic)

This article lists current metro cities with Azure Front Door point-of-presence (POP), sorted by regions. Each metro may contain more than one POP. Currently, Azure Front Door has 192 edge locations across 109 metro cities. Azure Front Door also has four edge locations across four Azure US Government cloud regions.

## Microsoft POP locations

> [!NOTE]

> A location might contain more than one POP, noted by the number in parentheses.

[!INCLUDE [front-door-edge-locations](../../includes/front-door-edge-locations.md)]

## Related content

* View [Azure Front Door edge locations by abbreviation](edge-locations-abbreviation.md).

* To get the latest list of edge nodes for Azure Front Door, see [Edge Nodes List - REST API](/rest/api/cdn/edge-nodes/list).

* Learn how to [create an Azure Front Door profile](quickstart-create-front-door.md).

* Learn how to [create an Azure Front Door Standard/Premium profile](standard-premium/create-front-door-portal.md).


# Routing Methods

# Traffic routing methods to origin

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium :heavy_check_mark: Front Door (classic)

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

Azure Front Door supports four traffic routing methods to manage how your HTTP/HTTPS traffic is distributed among different origins. When user requests reach the Front Door edge locations, the configured routing method ensures requests are forwarded to the best backend resource.

> [!NOTE]

> In this article, an *Origin* refers to the backend, and an *origin group* refers to the backend pool in the Azure Front Door (classic) configuration.

The four traffic routing methods are:

* **[Latency](#latency):** Routes requests to the origins with the lowest latency within an acceptable sensitivity range, ensuring requests are sent to the nearest origins in terms of network latency.

* **[Priority](#priority):** Allows you to set a priority for your origins, designating a primary origin to handle all traffic and a secondary origin as a backup if the primary becomes unavailable.

* **[Weighted](#weighted):** Assigns a weight to each origin to distribute traffic evenly or according to specified weight coefficients. Traffic is distributed based on weight values if the origins' latencies are within the acceptable sensitivity range.

* **[Session Affinity](#affinity):** Ensures requests from the same end user are sent to the same origin by configuring session affinity for your frontend hosts or domains.

> [!NOTE]

> In Azure Front Door Standard and Premium tiers, **Endpoint name** is referred to as **Frontend host** in Azure Front Door (classic).

All Front Door configurations include backend health monitoring and automated global failover. For more information, see [Front Door backend monitoring](front-door-health-probes.md). Azure Front Door can use a single routing method or combine multiple methods to create an optimal routing topology based on your application needs.

> [!NOTE]

> By using the [Front Door rules engine](front-door-rules-engine.md), you can configure rules to [override route configurations](front-door-rules-engine-actions.md#route-configuration-overrides) in Azure Front Door Standard and Premium tiers or [override the backend pool](front-door-rules-engine-actions.md#route-configuration-overrides) in Azure Front Door (classic) for a request. The origin group or backend pool set by the rules engine overrides the routing process described in this article.

## Overall decision flow

The following diagram illustrates the overall decision flow:

The decision steps are:

1. **Available origins:** Select all origins that are enabled and healthy (200 OK) based on the health probe.

- *Example: If there are six origins A, B, C, D, E, and F, and C is unhealthy and E is disabled, the available origins are A, B, D, and F.*

1. **Priority:** Select the top priority origins from the available ones.

- *Example: If origins A, B, and D have priority 1 and origin F has priority 2, the selected origins are A, B, and D.*

1. **Latency signal (based on health probe):** Select origins within the allowable latency range from the Front Door environment where the request arrived. This range is based on the latency sensitivity setting of the origin group and the latency of the closest origins.

- *Example: If the latency to origin A is 15 ms, to B is 30 ms, and to D is 60 ms, and the latency sensitivity is set to 30 ms, the selected origins are A and B, as D exceeds the 30-ms range.*

1. **Weights:** Distribute traffic among the final selected origins based on the specified weight ratios.

- *Example: If origin A has a weight of 3 and origin B has a weight of 7, traffic is distributed 3/10 to A and 7/10 to B.*

If you enable session affinity, the first request in a session follows the flow previously explained. Subsequent requests go to the origin selected in the first request.

## <a name = "latency"></a>Lowest latencies based traffic-routing

Deploying origins in multiple global locations can enhance your application's responsiveness by routing traffic to the origin that is "closest" to your end users. The Latency routing method is the default for Azure Front Door configurations. This method directs user requests to the origin with the lowest network latency, rather than the closest geographic location, ensuring optimal performance.

Azure Front Door's anycast architecture, combined with the Latency routing method, ensures that each user experiences the best performance based on their location. Each Front Door environment independently measures the latency to origins, meaning users in different locations are routed to the origin that offers the best performance for their specific environment.

> [!NOTE]

> By default, the latency sensitivity property is set to 0 ms. With this setting, requests are always forwarded to the fastest available origins. Weights on the origins only take effect if two origins have the same network latency.

For more information, see [Azure Front Door routing architecture](front-door-routing-architecture.md).

## <a name="priority"></a>Priority-based traffic-routing

To ensure high availability, deploy backup services to take over if the primary service fails. This setup is known as Active/Standby or Active/Passive deployment. The *Priority* traffic-routing method in Azure Front Door helps you implement this failover pattern.

By default, Azure Front Door routes traffic to the origins with the highest priority (lowest priority value). If these primary origins become unavailable, it routes traffic to the secondary origins (next lowest priority value). This process continues with tertiary origins if both primary and secondary origins are unavailable. Health probes monitor the availability of origins based on their configured status and health.

### Configuring priority for origins

Each origin in your Azure Front Door origin group has a *Priority* property, which you can set to a value between 1 and 5. Lower values indicate higher priority. Multiple origins can share the same priority value.

## <a name="weighted"></a>Weighted traffic-routing method

> [!NOTE]

> For customers with very low RPS (requests per second), due to the nature of how distributed AFD POPs and machines are, Azure Front Door can't guarantee that the weights you configure are strictly followed and the load balancing might appear skewed.

The *Weighted* traffic-routing method distributes traffic based on predefined weights.

In this method, you assign a weight to each origin in your Azure Front Door origin group. The weight is an integer between 1 and 1,000, with a default value of **50**.

Traffic is distributed among available origins by using a round-robin mechanism based on the specified weight ratios, provided the origins meet the acceptable latency sensitivity. If you set the latency sensitivity to **0** milliseconds, weights only take effect if two origins have the same network latency.

The weighted method supports several scenarios:

* **Gradual application upgrade**: Route a percentage of traffic to a new origin and gradually increase it over time.

* **Application migration to Azure**: Create an origin group with both Azure and external origins. Adjust weights to prefer new origins, gradually increasing their traffic share until they handle most traffic, then disable and remove less preferred origins.

* **Cloud-bursting for additional capacity**: Expand on-premises deployments into the cloud by adding or enabling more origins and specifying traffic distribution.

## <a name="affinity"></a>Session affinity

By default, Azure Front Door forwards requests from the same client to different origins. However, session affinity is useful for stateful applications or scenarios where subsequent requests from the same user need to be processed by the same origin. This feature ensures that the same origin handles a user's session, which is beneficial for scenarios like client authentication.

Azure Front Door uses cookie-based session affinity, where managed cookies with SHA256 of the origin URL as the identifier are used. This method directs subsequent traffic from a user session to the same origin.

You can enable session affinity at the origin group level in Azure Front Door Standard and Premium tiers, and at the frontend host level in Azure Front Door (classic) for each configured domain or subdomain. When you enable this feature, Azure Front Door adds cookies named `ASLBSA` and `ASLBSACORS` to the user's session. These cookies help identify different users even if they share the same IP address, which allows for a more even distribution of traffic among origins.

The cookie's lifetime matches the user's session, as Front Door currently supports only session cookies.

> [!NOTE]

> The browser session cookie maintains session affinity at the domain level. Subdomains under the same wildcard domain can share session affinity as long as the user's browser sends requests for the same origin resource.

>

> Public proxies might interfere with session affinity because establishing a session requires Front Door to add a session affinity cookie to the response. This action can't be done if the response is cacheable, as it would disrupt cookies for other clients requesting the same resource. To prevent this problem, session affinity **isn't** established if the origin sends a cacheable response. If the session is already established, the cacheability of the response doesn't matter.

>

> Session affinity is established in the following circumstances beyond the standard non-cacheable scenarios:

> - The response includes the `Cache-Control` header with *no-store*.

> - The response contains a valid `Authorization` header.

> - The response is an HTTP 302 status code.

## Next steps

- Learn how to [create an Azure Front Door](quickstart-create-front-door.md).

- Learn [how Azure Front Door works](front-door-routing-architecture.md).


# Health Probes

# Health probes

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

> [!NOTE]

> In this article, an *origin* and an *origin group* refer to the backend and backend pool of an Azure Front Door (classic) configuration.

>

To determine the health and proximity of each origin for a given Azure Front Door environment, each Front Door profile periodically sends a synthetic HTTP or HTTPS request to all your configured origins. Front Door then uses responses from the health probe to determine the *best* origin to route your client requests to.

> [!WARNING]

> Since each Azure Front Door edge location sends health probes to your origins, the health probe volume for your origins can be high. The number of probes depends on your customer's traffic location and your health probe frequency. If the Azure Front Door edge locations don't receive real traffic from your end users, the frequency of the health probe from the edge location decreases from the configured frequency. If there's traffic to all the Azure Front Door edge locations, the health probe volume can be high depending on your health probes frequency.

>

> To roughly estimate the health probe volume per minute to an origin when using the default probe frequency of 30 seconds, multiply the number of edge locations by two requests per minute. The probing requests are fewer if there's no traffic sent to all of the edge locations. For a list of edge locations, see [edge locations by region](edge-locations-by-region.md).

## Supported protocols

Azure Front Door supports sending probes over either HTTP or HTTPS protocols. These probes use the same TCP ports configured for routing client requests, and you can't override them. Front Door HTTP or HTTPS probes include a `User-Agent` header set with the value `Edge Health Probe`.

## Supported HTTP methods for health probes

Azure Front Door supports the following HTTP methods for sending the health probes:

- **GET:** The GET method retrieves whatever information (in the form of an entity) gets identified by the Request-URI.

- **HEAD:** The HEAD method is identical to GET except that the server **MUST NOT** return a message-body in the response. For new Front Door profiles, the probe method is set as HEAD by default.

> [!TIP]

> To lower the load and cost to your origins, use HEAD requests for health probes.

## Health probe responses

| Responses  | Description |

| ------------- | ------------- |

| Determining health  | A **200 OK** status code indicates the origin is healthy. Any other status code is considered a failure. If for any reason a valid HTTP response isn't received for a probe, the probe is counted as a failure. |

| Measuring latency  | Latency is the wall-clock time measured from the moment immediately before the probe request gets sent to the moment when Front Door receives the last byte of the response. Front Door uses a new TCP connection for each request. The measurement isn't biased towards origins with existing warm connections. |

## How Front Door determines origin health

Azure Front Door uses a three-step process across all algorithms to determine health.

1. Exclude disabled origins.

1. Exclude origins that have health probe errors:

* Front Door looks at the last _n_ health probe responses. If at least _x_ responses are healthy, the origin is considered healthy.

* Change the **SampleSize** property in load-balancing settings to set _n_.

* Change the **SuccessfulSamplesRequired** property in load-balancing settings to set _x_.

1. For sets of healthy origins in an origin group, Front Door measures and maintains the latency for each origin.

> [!NOTE]

> If a single endpoint is a member of multiple origin groups, Front Door optimizes the number of health probes it sends to the origin to reduce the load on the origin. Front Door sends health probe requests based on the lowest configured sample interval. The responses from the same health probes determine the health of the endpoint in all origin groups.

## Complete health probe failure

If health probes fail for every origin in an origin group, Front Door considers all origins unhealthy and routes traffic in a round robin distribution across all of them. When an origin returns to a healthy state, Front Door resumes the normal load-balancing algorithm.

## Disabling health probes

If your origin group has a single origin, you can disable health probes to reduce the load on your application. If your origin group has multiple origins and more than one origin is enabled, you can't disable health probes.

> [!NOTE]

> If your origin group has only a single origin, the single origin gets few health probes. This condition might lead to a dip in origin health metrics but your traffic isn't impacted.

## Related content

- [Create an Azure Front Door profile](create-front-door-portal.md)

- [Front Door routing architecture](front-door-routing-architecture.md)


# End To End Tls

# TLS encryption with Azure Front Door

Transport Layer Security (TLS), previously known as Secure Sockets Layer (SSL), is the standard security technology for establishing an encrypted link between a web server and a client, like a web browser. This link ensures that all data passed between the server and the client remain private and encrypted.

To meet your security or compliance requirements, Azure Front Door supports end-to-end TLS encryption. Front Door TLS/SSL offload terminates the TLS connection, decrypts the traffic at the Azure Front Door, and re-encrypts the traffic before forwarding it to the origin. When connections to the origin use the origin's public IP address, it's a good security practice to configure HTTPS as the forwarding protocol on your Azure Front Door. By using HTTPS as the forwarding protocol, you can enforce end-to-end TLS encryption for the entire processing of the request from the client to the origin. TLS/SSL offload is also supported if you deploy a private origin with Azure Front Door Premium using the [Private Link](private-link.md) feature.

This article explains how Azure Front Door works with TLS connections. For more information about how to use TLS certificates with your own custom domains, see [HTTPS for custom domains](domain.md#https-for-custom-domains). To learn how to configure a TLS certificate on your own custom domain, see [Configure a custom domain on Azure Front Door using the Azure portal](standard-premium/how-to-add-custom-domain.md).

## End-to-end TLS encryption

End-to-end TLS allows you to secure sensitive data while in transit to the origin while benefiting from Azure Front Door features like global load balancing and caching. Some of the features also include URL-based routing, TCP split, caching on edge location closest to the clients, and customizing HTTP requests at the edge.

Azure Front Door offloads the TLS sessions at the edge and decrypts client requests. It then applies the configured routing rules to route the requests to the appropriate origin in the origin group. Azure Front Door then starts a new TLS connection to the origin and re-encrypts all data using the origin's certificate before transmitting the request to the origin. Any response from the origin is encrypted through the same process back to the end user. You can configure your Azure Front Door to use HTTPS as the forwarding protocol to enable end-to-end TLS.

## Supported TLS versions

Azure Front Door supports two versions of the TLS protocol: TLS versions 1.2 and 1.3. All Azure Front Door profiles created after September 2019 use TLS 1.2 as the default minimum with TLS 1.3 enabled. Currently, Azure Front Door doesn't support client/mutual authentication (mTLS).

> [!IMPORTANT]

> TLS 1.0 and 1.1 aren't supported.

For Azure Front Door Standard and Premium, you can configure predefined TLS policy or choose the TLS cipher suite based on your organization's security needs. For more information, see [Azure Front Door TLS policy](/azure/frontdoor/standard-premium/tls-policy) and [configure TLS policy on a Front Door custom domain](/azure/frontdoor/standard-premium/tls-policy-configure).

For Azure Front Door classic and Microsoft CDN classic, you can configure the minimum TLS version in Azure Front Door in the custom domain HTTPS settings using the Azure portal or the [Azure REST API](/rest/api/frontdoorservice/frontdoor/frontdoors/createorupdate#minimumtlsversion). For a minimum TLS version 1.2, the negotiation will attempt to establish TLS 1.3 and then TLS 1.2. When Azure Front Door initiates TLS traffic to the origin, it will attempt to negotiate the best TLS version that the origin can reliably and consistently accept. Supported TLS versions for origin connections are TLS 1.2 and TLS 1.3. If you want to custom the cipher suite per needs, [migrate Front Door classic](/azure/frontdoor/tier-migration) and [Microsoft CDN classic](/azure/cdn/tier-migration?toc=/azure/frontdoor/TOC.json) to Azure Front Door standard and premium.

> [!NOTE]

> - Clients with TLS 1.3 enabled are required to support one of the Microsoft SDL compliant EC Curves, including Secp384r1, Secp256r1, and Secp521, in order to successfully make requests with Azure Front Door using TLS 1.3.

> - It's recommended that clients use one of these curves as their preferred curve during requests to avoid increased TLS handshake latency, which might result from multiple round trips to negotiate the supported EC curve.

## Supported certificates

When you create your TLS/SSL certificate, you must create a complete certificate chain with an allowed Certificate Authority (CA) that is part of the [Microsoft Trusted CA List](https://ccadb.my.salesforce-sites.com/microsoft/IncludedCACertificateReportForMSFT). If you use a non-allowed CA, your request will be rejected.

Certificates from internal CAs or self-signed certificates aren't allowed.

## Online Certificate Status Protocol (OCSP) stapling

OCSP stapling is supported by default in Azure Front Door and no configuration is required.

## <a name="backend-tls-connection-azure-front-door-to-origin"></a> Origin TLS connection (Azure Front Door to origin)

For HTTPS connections, Azure Front Door expects that your origin presents a certificate from a valid certificate authority (CA) with a subject name matching the origin *hostname*. As an example, if your origin hostname is set to `myapp-centralus.contoso.net` and the certificate that your origin presents during the TLS handshake doesn't have `myapp-centralus.contoso.net` or `*.contoso.net` in the subject name, then Azure Front Door refuses the connection and the client sees an error.

> [!NOTE]

> The certificate must have a complete certificate chain with leaf and intermediate certificates. The root CA must be part of the [Microsoft Trusted CA List](https://ccadb.my.salesforce-sites.com/microsoft/IncludedCACertificateReportForMSFT). If a certificate without complete chain is presented, the requests that involve that certificate aren't guaranteed to work as expected.

In certain use cases, such as testing, you can disable certificate subject name checks for your Azure Front Door as a workaround for resolving failing HTTPS connections. The origin must still present a certificate with a valid, trusted chain, but it doesn't need to match the origin hostname.

In Azure Front Door Standard and Premium, you can configure an origin to disable the certificate subject name check.

In Azure Front Door (classic), you can disable the certificate subject name check by changing the Azure Front Door settings in the Azure portal. You can also configure the check by using the backend pool's settings in the Azure Front Door APIs.

> [!NOTE]

> From a security standpoint, Microsoft doesn't recommend disabling the certificate subject name check.

## Frontend TLS connection (client to Azure Front Door)

To enable the HTTPS protocol for secure delivery of contents on an Azure Front Door custom domain, you can choose to use a certificate that is managed by Azure Front Door or use your own certificate.

For more information, see [HTTPS for custom domains](domain.md#https-for-custom-domains).

Azure Front Door's managed certificate provides a standard TLS/SSL certificate via DigiCert and is stored in Azure Front Door's Key Vault.

If you choose to use your own certificate, you can onboard a certificate from a supported CA that can be a standard TLS, extended validation certificate, or even a wildcard certificate. Self-signed certificates aren't supported. Learn [how to enable HTTPS for a custom domain](front-door-custom-domain-https.md).

### Certificate autorotation

For the Azure Front Door Standard/Premium managed certificate option, the certificates are managed and auto-rotates within 45 days of expiry time by Azure Front Door. For the Azure Front Door Classic and Azure CDN Classic managed certificate option, the certificates are managed and auto-rotates within 90 days of expiry time by Azure Front Door.  If you're using classic SKUs managed certificate and see that the certificate expiry date is less than 60 days away or 30 days for the Standard/Premium SKU, file a support ticket.

> [!IMPORTANT]

> - For Azure Front Door Classic and Azure CDN Classic, managed certificates will no longer be supported starting August 15, 2025. To avoid service disruption, either switch to **Bring Your Own Certificate (BYOC)** or migrate to Azure Front Door Standard/Premium before this date. Existing managed certificates will continue to autorenew until August 15, 2025, and remain valid until April 14, 2026. However, it's highly recommended to switch to **BYOC** or migrate to Front Door Standard/Premium before August 15, 2025, to avoid unexpected certificate revocation.

> - Azure Front Door (AFD) Standard and Premium use DigiCert‑issued managed TLS certificates, and DigiCert is retiring the G1 root certificate that expires on April 14, 2026, replacing it with the G2 root certificate. Azure Front Door will automatically rotate AFD‑managed certificates before expiration for custom domains that directly CNAME to the Azure Front Door endpoint, and no customer action is required. Customers whose domains do not directly CNAME to Azure Front Door must manually rotate their certificates to use the DigiCert G2 root certificate before April 14, 2026 to avoid TLS connectivity issues.

For your own custom TLS/SSL certificate:

1. Set the secret version to 'Latest' for the certificate to be automatically rotated to the latest version when a newer version of the certificate is available in your key vault. For custom certificates, the certificate gets auto-rotated within 3-4 days with a newer version of certificate, no matter what the certificate expired time is.

1. If a specific version is selected, autorotation isn’t supported. You'll have to reselect the new version manually to rotate certificate. It takes up to 24 hours for the new version of the certificate/secret to be deployed.

> [!NOTE]

> Azure Front Door (AFD) Standard and Premium automatically rotate managed certificates only when the custom domain CNAME points directly to the AFD endpoint; for indirect CNAME configurations, we strongly recommend using a bring‑your‑own certificate, as AFD will attempt domain validation via file‑based token validation when traffic reaches AFD but successful validation is not guaranteed.

The service principal for Front Door must have access to the key vault. The updated certificate rollout operation by Azure Front Door won't cause any production downtime, as long as the subject name or subject alternate name (SAN) for the certificate hasn't changed.

## Supported cipher suites

For TLS 1.2/1.3, the following cipher suites are supported:

- TLS_AES_256_GCM_SHA384 (TLS 1.3 only)

- TLS_AES_128_GCM_SHA256 (TLS 1.3 only)

- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384

- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256

- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384

- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256

> [!NOTE]

> Older TLS versions and weak ciphers are no longer supported.

> Support for DHE cipher suites retired on April 1, 2026. See [documentation](diffie-hellman-ciphers.md) for more details.

Use *TLS policy* to configure specific cipher suites. Azure Front Door Standard and Premium offer two mechanisms for controlling TLS policy: you can use either a predefined policy or a custom policy per your own needs. For more information, see [Configure TLS policy on a Front Door custom domain](standard-premium/tls-policy-configure.md).

> [!NOTE]

> For Windows 10 and later versions, we recommend enabling one or both of the ECDHE_GCM cipher suites for better security. Windows 8.1, 8, and 7 aren't compatible with these ECDHE_GCM cipher suites. The ECDHE_CBC cipher suites have been provided for compatibility with those operating systems.

## Related content

- [Azure Front Door TLS policy](standard-premium/tls-policy.md)

- [Domains in Azure Front Door](domain.md)

- [Configure a custom domain on Azure Front Door](standard-premium/how-to-add-custom-domain.md)

- [Configure a custom domain for Azure Front Door (classic)](front-door-custom-domain.md)

- [Configure HTTPS on an Azure Front Door (classic) custom domain](front-door-custom-domain-https.md)


# Private Link

# Secure your origin with Private Link in Azure Front Door Premium

**Applies to:** :heavy_check_mark: Front Door Premium

[Azure Private Link](../private-link/private-link-overview.md) enables you to access Azure PaaS services and services hosted in Azure over a private endpoint in your virtual network. Traffic between your virtual network and the service goes over the Microsoft backbone network, eliminating exposure to the public Internet.

Azure Front Door Premium can connect to your origin using Private Link. Your origin can be hosted in a virtual network or hosted as a PaaS service such as Azure Web App or Azure Storage. Private Link removes the need for your origin to be accessed publicly.

## How Private Link works

When you enable Private Link to your origin in Azure Front Door Premium, Front Door creates a private endpoint on your behalf from an Azure Front Door managed regional private network. You receive an Azure Front Door private endpoint request at the origin pending your approval.

You must approve the private endpoint connection before traffic can pass to the origin privately. You can approve private endpoint connections by using the Azure portal, Azure CLI, or Azure PowerShell. For more information, see [Manage a Private Endpoint connection](../private-link/manage-private-endpoint.md).

After you enable an origin for Private Link and approve the private endpoint connection, it can take a few minutes for the connection to be established. During this time, requests to the origin receives an Azure Front Door error message. The error message goes away once the connection is established.

Once your request is approved, a dedicated private endpoint gets assigned for routing your traffic from the Azure Front Door managed virtual network. Traffic from your clients reaches Azure Front Door Global POPs and is then routed over the Microsoft backbone network to the Front Door regional cluster, which hosts the managed virtual network containing the dedicated private endpoint. The traffic is then routed to your origin via the private link platform over Microsoft backbone network. Hence the incoming traffic to your origin secured upon the moment it arrives to Azure Front Door.

> [!NOTE]

> Azure Front Door doesn't support client/mutual authentication (mTLS) for public origins or private link enabled origins.

## Supported origins

Origin support for direct private endpoint connectivity is currently limited to the following origin types.

| Origin type | Documentation |

|--|--|

| App Service (Web App, Function App) | [Connect Azure Front Door to a Web App / Function App origin with Private Link](standard-premium/how-to-enable-private-link-web-app.md) |

| Blob Storage | [Connect Azure Front Door to a storage account origin with Private Link](standard-premium/how-to-enable-private-link-storage-account.md) |

| Storage Static Website | [Connect Azure Front Door to a storage static website origin with Private Link](how-to-enable-private-link-storage-static-website.md) |

| Internal load balancers, or any services that expose internal load balancers such as Azure Kubernetes Service, or Azure Red Hat OpenShift | [Connect Azure Front Door to an internal load balancer origin with Private Link](standard-premium/how-to-enable-private-link-internal-load-balancer.md) |

| API Management | [Connect Azure Front Door to an API Management origin with Private Link](standard-premium/how-to-enable-private-link-apim.md) |

| Application Gateway | [Connect Azure Front Door to an application gateway origin with Private Link](how-to-enable-private-link-application-gateway.md) |

| Azure Container Apps | [Connect Azure Front Door to an Azure Container Apps origin with Private Link](../container-apps/how-to-integrate-with-azure-front-door.md) |

> [!NOTE]

> This feature isn't supported with Azure App Service Slots and Azure Static Web App.

## Region availability

Azure Front Door private link is available in the following regions:

| Americas | Europe | Middle East and Africa | Asia Pacific |

|--|--|--|--|

| Brazil South | France Central | South Africa North | Australia East |

| Canada Central | Germany West Central | UAE North | Central India |

| Central US | North Europe | | Japan East |

| East US | Norway East | | Korea Central |

| East US 2 | UK South | | East Asia |

| South Central US | West Europe | | South East Asia |

| West US 2 | Sweden Central | | China East 3 |

| West US 3 | | | China North 3 |

| US Gov Arizona | | | |

| US Gov Texas | | | |

| US Gov Virginia | | | |

| US Nat East | | | |

| US Nat West | | | |

| US Sec East | | | |

| US Sec West | | | |

> [!NOTE]

> Azure Front Door Private Link is only available in regions with Availability Zone support. This is to ensure zonal resiliency for region based feature like Private link.

The Azure Front Door Private Link feature is region agnostic but for the best latency, you should always pick an Azure region closest to your origin when choosing to enable Azure Front Door Private Link endpoint. If your origin's region isn't supported in the list of regions Front Door Private Link supports, pick the next nearest region. Traffic flows from the client to the Azure Front Door Private Link endpoint in the supported region, then traverses the Microsoft backbone network to your origin, maintaining private connectivity. Be aware that this configuration introduces additional latency due to the extra network hop between regions.

You can use [Azure network round-trip latency statistics](../networking/azure-network-latency.md) to determine the additional latency due to choosing the next nearest region.  Once a new region is supported, you can follow these [instructions](blue-green-deployment.md) to gradually shift traffic to the new region.

## Association of a private endpoint with an Azure Front Door profile

### Private endpoint creation

Within a single Azure Front Door profile, if two or more Private Link enabled origins are created with the same set of resource ID, group ID and region, then for all such origins only one private endpoint gets created. Connections to the backend can be enabled using this private endpoint. This setup means you only have to approve the private endpoint once because only one private endpoint gets created. If you create more Private Link enabled origins using the same set of Private Link location, resource ID, and group ID, you don't need to approve any more private endpoints.

> [!WARNING]

> Avoid configuring multiple private link enabled origins that point to the same resource (with identical resource ID, group ID, and region), if each origin uses a different HTTP or HTTPS port. This setup can lead to routing issues between Front Door and the origin due to a platform limitation.

#### Single private endpoint

For example, a single private endpoint gets created for all the different origins across different origin groups but in the same Azure Front Door profile as shown in the following table:

#### Multiple private endpoints

A new private endpoint gets created in the following scenario:

* If the region, resource ID, or group ID changes, Azure Front Door considers that the Private Link location and the hostname has changed, resulting in extra private endpoints created and each one needs to be approved.

* Enabling Private Link for origins in different Azure Front Door profiles will create extra private endpoints and requires approval for each one.

### Private endpoint removal

When an Azure Front Door profile gets deleted, private endpoints associated with the profile also get deleted.

#### Single private endpoint

If AFD-Profile-1 gets deleted, then the PE1 private endpoint across all the origins also gets deleted.

#### Multiple private endpoints

* If AFD-Profile-1 gets deleted, all private endpoints from PE1 through to PE4 gets deleted.

* Deleting an Azure Front Door profile doesn't affect private endpoints created for a different Azure Front Door profile.

For example:

* If AFD-Profile-2 gets deleted, only PE5 is removed.

* If AFD-Profile-3 gets deleted, only PE6 is removed.

* If AFD-Profile-4 gets deleted, only PE7 is removed.

* If AFD-Profile-5 gets deleted, only PE8 is removed.

## Frequently asked questions

1. Does this feature support private link connectivity from client to Azure Front Door?

* No. This feature only supports private link connectivity from your Azure Front Door to your origin.

2. How to improve redundancy while using Private Link with Azure Front Door?

* To improve redundancy at origin level, make sure you have multiple private link enabled origins within the same origin group so that Azure Front Door can distribute traffic across multiple instances of the application. If one instance is unavailable, then other origins can still receive traffic.

* To route Private Link traffic, requests are routed from Azure Front Door POPs to the Front Door managed virtual network hosted in Front Door regional clusters. To have redundancy in case the regional cluster isn't reachable, it's recommended to configure multiple origins (each with a different Private Link region) under the same Azure Front Door origin group. This way even if one regional cluster is unavailable, then other origins can still receive traffic via a different regional cluster. Below is how an origin group with both origin level and region level redundancy would look like.

3. Can I mix public and private origins in the same origin group?

* No. Azure Front Door doesn't allow mixing public and private origins in the same origin group. This can cause configuration errors or traffic routing issues. Keep all public origins in one origin group and all private origins in a separate origin group.

4. Why do I see the error “Origin Group can only have origins with private links or origins without private links. They cannot have a mix of both” when enabling Private Link simultaneously for multiple public origins?

* This error can occur when you enable Private Link for more than one public origin in the same origin group at the same time. Although both origins are intended to be private, the update operation processes origins sequentially, not simultaneously. When the first origin is updated, the second origin is still technically public, creating a temporary mixed state, resulting in an error.

* To avoid this error, enable Private Link for one origin at a time:

1.	Remove origins from the origin group till only a single origin remains.

2.	Enable Private Link for that origin and approve its Private Endpoint.

3.	After approval, add the second origin and enable Private Link for it.

6. Why do I see an error when trying to access the private endpoint details by double clicking on the private endpoint in Azure portal?

* While approving the private endpoint connection or after approving the private endpoint connection, if you double click on the private endpoint, you'll see an error message saying "You don't have access. Copy the error details and send them to your administrator to get access to this page." This is expected as the private endpoint is hosted within a subscription managed by Azure Front Door.

6. What are the rate limits for Private Link traffic and how can I handle high traffic scenarios?

* For platform protection, each Front Door regional cluster has a limit of 7200 RPS (requests per second) per Front Door profile. Requests beyond 7200 RPS at a region will be rate limited with "429 Too Many Requests".

* If you're onboarding or expecting traffic more than 7200 RPS, we recommend deploying multiple origins (each with a different Private Link region) so that traffic is spread across multiple Front Door regional clusters. It's recommended that each origin is a separate instance of your application to improve origin level redundancy. But if you can’t maintain separate instances, you can still configure multiple origins at Front Door level with each origin pointing to the same hostname but the regions are kept different. This way, Front Door will route the traffic to the same instance but via different regional clusters.

7. For private link enabled origins, will health probes also follow the same network path as actual traffic?

* Yes.

## Related content

* [Connect Azure Front Door Premium to a Web App origin with Private Link](standard-premium/how-to-enable-private-link-web-app.md)

* [Connect Azure Front Door Premium to a storage account origin with Private Link](standard-premium/how-to-enable-private-link-storage-account.md)

* [Connect Azure Front Door Premium to an internal load balancer origin with Private Link](standard-premium/how-to-enable-private-link-internal-load-balancer.md)

* [Connect Azure Front Door Premium to a storage static website origin with Private Link](how-to-enable-private-link-storage-static-website.md)

* [Connect Azure Front Door Premium to an application gateway origin with Private Link](how-to-enable-private-link-application-gateway.md)

* [Connect Azure Front Door Premium to an API Management origin with Private Link](standard-premium/how-to-enable-private-link-apim.md)

* [Connect Azure Front Door Premium to an Azure Container Apps origin with Private Link](../container-apps/how-to-integrate-with-azure-front-door.md)


# Front Door Ddos

# DDoS protection on Azure Front Door

Azure Front Door is a Content Delivery Network (CDN) that helps protect your origins from HTTP(S) DDoS attacks by distributing traffic across its 192 edge points of presence (POPs) worldwide. These POPs use Azure's large private WAN to deliver your web applications and services faster and more securely to your end users. Azure Front Door includes layer 3, 4, and 7 DDoS protection and a Web Application Firewall (WAF) to safeguard your applications from common exploits and vulnerabilities.

## Infrastructure DDoS protection

Azure Front Door benefits from the [default Azure infrastructure DDoS protection](../ddos-protection/ddos-protection-overview.md). This protection monitors and mitigates network layer attacks in real time by using the global scale and capacity of Azure Front Door’s network. It has a proven track record of safeguarding Microsoft’s enterprise and consumer services from large-scale attacks.

## Protocol blocking

Azure Front Door supports only HTTP and HTTPS protocols and requires a valid `Host` header for each request. This behavior helps prevent common DDoS attack types such as volumetric attacks that use various protocols and ports, DNS amplification attacks, and TCP poisoning attacks.

## Capacity absorption

Azure Front Door is a large-scale, globally distributed service that serves many customers, including Microsoft’s own cloud products, which handle hundreds of thousands of requests per second. Positioned at the edge of Azure’s network, Azure Front Door can intercept and geographically isolate large volume attacks, preventing malicious traffic from reaching beyond the edge of the Azure network.

## Caching

Use Azure Front Door [caching capabilities](./front-door-caching.md) to protect your backends from large traffic volumes generated by an attack. Azure Front Door edge nodes return cached resources, so they don't forward these resources to your backend. Even short cache expiry times (seconds or minutes) on dynamic responses can significantly reduce the load on your backend services. For more information about caching concepts and patterns, see [Caching considerations](/azure/architecture/best-practices/caching) and [Cache-aside pattern](/azure/architecture/patterns/cache-aside).

## Web Application Firewall (WAF)

Use [Azure Web Application Firewall (WAF)](../web-application-firewall/afds/afds-overview.md) to protect against various types of attacks:

- The managed rule set protects your application from many common attacks. For more information, see [Managed rules](../web-application-firewall/afds/waf-front-door-drs.md).

- Block or redirect traffic from specific geographic regions to a static webpage. For more information, see [Geo-filtering](../web-application-firewall/afds/waf-front-door-geo-filtering.md).

- Block IP addresses and ranges identified as malicious. For more information, see [IP restrictions](../web-application-firewall/afds/waf-front-door-configure-ip-restriction.md).

- Apply rate limiting to prevent IP addresses from calling your service too frequently. For more information, see [Rate limiting](../web-application-firewall/afds/waf-front-door-rate-limit.md).

- Create [custom WAF rules](../web-application-firewall/afds/waf-front-door-custom-rules.md) to automatically block and rate limit HTTP or HTTPS attacks with known signatures.

- The bot protection managed rule set protects your application from known bad bots. For more information, see [Configuring bot protection](../web-application-firewall/afds/waf-front-door-policy-configure-bot-protection.md).

For guidance on using Azure WAF to protect against DDoS attacks, see [Application DDoS protection](../web-application-firewall/shared/application-ddos-protection.md).

## Protect virtual network origins

Enable [Azure DDoS Protection](../ddos-protection/ddos-protection-overview.md) on your origin virtual network to safeguard your public IPs from DDoS attacks. This service offers more benefits such as cost protection, an SLA guarantee, and access to the DDoS Rapid Response Team for expert assistance during an attack.

## Private Link

Enhance the security of your Azure-hosted origins by using [Azure Private Link](private-link.md) to restrict access to Azure Front Door. This feature establishes a private network connection between Azure Front Door and your application servers, eliminating the need to expose your origins to the public internet.

## Related content

- Set up a [WAF policy for Azure Front Door](front-door-waf.md).

- Create an [Azure Front Door profile](quickstart-create-front-door.md).

- Understand [how Azure Front Door works](front-door-routing-architecture.md).


# How To Enable Private Link Web App

# Connect Azure Front Door Premium to an App Service (Web App or Function App) origin with Private Link

**Applies to:** :heavy_check_mark: Front Door Premium

This article shows you how to configure Azure Front Door Premium to connect to your App Service (Web App or Function App) privately using Azure Private Link.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An Azure Front Door Premium profile with an origin group. For more information, see [Create an Azure Front Door](../create-front-door-portal.md).

- A Private Link. For more information, see [Create a Private Link service](../../private-link/create-private-link-service-portal.md).

- Sign in to the [Azure portal](https://portal.azure.com) with your Azure account.

- An Azure Front Door Premium profile with an origin group. For more information, see [Create an Azure Front Door](../create-front-door-powershell.md).

- A Private Link. For more information, see [Create a Private Link service](../../private-link/create-private-link-service-powershell.md).

- Azure Cloud Shell or Azure PowerShell.

The steps in this article run the Azure PowerShell cmdlets interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the cmdlets in the Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code and then paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure PowerShell locally](/powershell/azure/install-azure-powershell) to run the cmdlets. If you run PowerShell locally, sign in to Azure using the [Connect-AzAccount](/powershell/module/az.accounts/connect-azaccount) cmdlet.

- An Azure Front Door Premium profile with an origin group. For more information, see [Create an Azure Front Door](../create-front-door-cli.md).

- A Private Link. For more information, see [Create a Private Link service](../../private-link/create-private-link-service-cli.md).

- Azure Cloud Shell or Azure CLI.

The steps in this article run the Azure CLI commands interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the commands in the Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code, and paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure CLI locally](/cli/azure/install-azure-cli) to run the commands. If you run Azure CLI locally, sign in to Azure using the [az login](/cli/azure/reference-index#az-login) command.

> [!NOTE]

> Private endpoints require your App Service plan to meet specific requirements. For more information, see [Using Private Endpoints for Azure Web App](../../app-service/networking/private-endpoint.md). This feature isn't supported with App Service Slots.

## Enable Private Link to an App Service (Web App or Function App) in Azure Front Door Premium

In this section, you map the Private Link service to a private endpoint within Azure Front Door's private network.

1. In your Azure Front Door Premium profile, go to *Settings* and select **Origin groups**.

1. Choose the origin group that should contain the App Service (Web App or Function App) origin you want to enable Private Link for.

1. Select **+ Add an origin** to add a new origin or select an existing one from the list. Use the following table to configure the settings for the origin:

| Setting | Value |

| ------- | ----- |

| Name | Enter a name to identify this origin. |

| Origin Type | App services |

| Host name | Select the host from the dropdown that you want as an origin. |

| Origin host header | Customize the host header of the origin or leave it as default. |

| HTTP port | 80 (default) |

| HTTPS port | 443 (default) |

| Priority | Assign different priorities to origins for primary, secondary, and backup purposes. |

| Weight | 1000 (default). Use weights to distribute traffic among different origins. |

| Region | Select the region that matches or is closest to your origin. |

| Target sub resource | Choose *site* as the subresource type for the selected resource. |

| Request message | Enter a custom message to display while approving the Private Endpoint. |

1. Select **Add** to save your configuration, then select **Update** to save the origin group settings.

1. Use the [Get-AzResource](/powershell/module/az.resources/get-azresource) cmdlet to get the resource ID of the App Service to be used as the origin for Azure Front Door:

```azurepowershell-interactive

Get-AzResource -Name testWebAppAFD `

-ResourceGroupName testRG

```

1. Use the [New-AzFrontDoorCdnOrigin](/powershell/module/az.cdn/new-azfrontdoorcdnorigin) cmdlet to add your App Service origin to your origin group:

```azurepowershell-interactive

# Add App Service origin to the Azure Front Door profile with Private Link

$origin1 = New-AzFrontDoorCdnOrigin `

-OriginGroupName default-origin-group `

-OriginName test-origin `

-ProfileName testAFD `

-ResourceGroupName testRG `

-HostName testwebapp.canadacentral-01.azurewebsites.net `

-OriginHostHeader testwebapp.canadacentral-01.azurewebsites.net `

-HttpPort 80 `

-HttpsPort 443 `

-Priority 1 `

-Weight 1000 `

-PrivateLinkId /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/testRG/providers/Microsoft.Web/sites/testWebAppAFD `

-SharedPrivateLinkResourceGroupId sites `

-SharedPrivateLinkResourcePrivateLinkLocation "Central US" `

-SharedPrivateLinkResourceRequestMessage "testWebAppAFDPL Private Link request"

```

Use the [az afd origin create](/cli/azure/afd/origin#az-afd-origin-create) command to create a new Azure Front Door origin. The `private-link-location` value must be from the [available regions](../private-link.md#region-availability) and the `private-link-sub-resource-type` value is **sites**.

```azurecli-interactive

az afd origin create --enabled-state Enabled \

--resource-group 'myResourceGroup' \

--origin-group-name 'og1' \

--origin-name 'myapporigin' \

--profile-name 'contosoAFD' \

--host-name 'example.contoso.com' \

--origin-host-header 'example.contoso.com' \

--http-port 80 \

--https-port 443 \

--priority 1 \

--weight 500 \

--enable-private-link true \

--private-link-location 'EastUS' \

--private-link-request-message 'AFD app service origin Private Link request.' \

--private-link-resource /'subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/webapp1/appServices' \

--private-link-sub-resource-type sites

```

## Approve Azure Front Door Premium private endpoint connection from App Service

1. Go to the App Service that you configured with Private Link in the previous section. Under **Settings**, select **Networking**.

1. In the **Networking** section, select **Configure your private endpoint connections**.

1. Find the *pending* private endpoint request from Azure Front Door Premium and select **Approve**.

1. Use the [Get-AzPrivateEndpointConnection](/powershell/module/az.network/get-azprivateendpointconnection) cmdlet to list the private endpoint connections for your App Service. Note the `Name` of the private endpoint connection available in your App Service from the output.

```azurepowershell-interactive

# PrivateLinkResourceId is the resource ID of the WebApp

Get-AzPrivateEndpointConnection -PrivateLinkResourceId '/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/testRG/providers/Microsoft.Web/sites/testWebAppAFD'

```

1. Use the [Approve-AzPrivateEndpointConnection](/powershell/module/az.network/approve-azprivateendpointconnection) cmdlet to approve the private endpoint connection.

```azurepowershell-interactive

Approve-AzPrivateEndpointConnection -ResourceId '/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/webapp1/privateEndpointConnections/a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1'

```

1. Use the [Get-AzPrivateEndpointConnection](/powershell/module/az.network/get-azprivateendpointconnection) cmdlet to verify the status of the private endpoint connection.

```azurepowershell-interactive

Get-AzPrivateEndpointConnection -PrivateLinkResourceId '/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/testRG/providers/Microsoft.Web/sites/testWebAppAFD'

```

1. Use the [az network private-endpoint-connection list](/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-list) command to list the private endpoint connections for your web app. Note the `Resource ID` of the private endpoint connection on the first line of the output.

```azurecli-interactive

az network private-endpoint-connection list --name 'webapp1' --resource-group 'myResourceGroup' --type 'Microsoft.Web/sites'

```

1. Use the [az network private-endpoint-connection approve](/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-approve) command to approve the private endpoint connection.

```azurecli-interactive

az network private-endpoint-connection approve --id '/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/webapp1/privateEndpointConnections/a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1'

```

It can take a few minutes for the connection to fully establish after approval. Once established, you can access your web app or function app through Azure Front Door Premium. Direct access to the app from the public internet is disabled once private endpoint is enabled.

## Common mistakes to avoid

A common mistake when configuring an origin with Azure Private Link enabled is:

- Adding the origin with Azure Private Link enabled to an existing origin group that contains public origins. Azure Front Door doesn't allow mixing public and private origins in the same origin group.

## Related content

- [Connect Azure Front Door Premium to an Azure Application Gateway with Private Link](../how-to-enable-private-link-application-gateway.md)

- [Use private endpoints for Azure App Service apps](../../app-service/networking/private-endpoint.md)


# Billing

# Understand Azure Front Door billing

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Azure Front Door provides a rich set of features for your internet-facing workloads. Front Door helps you to accelerate your application's performance, improves your security, and provides you with tools to inspect and modify your HTTP traffic.

Front Door's billing model includes several components. Front Door charges a base fee for each profile that you deploy. You're also charged for requests and data transfer based on your usage. *Billing meters* collect information about your Front Door usage. Your monthly Azure bill aggregates the billing information across the month and applies the pricing to determine the amount you need to pay.

This article explains how Front Door pricing works so that you can understand and predict your monthly Azure Front Door bill.

For Azure Front Door pricing information, see [Azure Front Door pricing](https://azure.microsoft.com/pricing/details/frontdoor/).

> [!TIP]

> The Azure pricing calculator helps you to calculate a pricing estimate for your requirements. Use the [pre-created pricing calculator estimate](https://azure.com/e/bdc0d6531fbb4760bf5cdd520af1e4cc?azure-portal=true) as a starting point, and customize it for your own solution.

> [!NOTE]

> This article explains how billing works for Azure Front Door Standard and Premium SKUs. For information about Azure Front Door (classic), see [Azure Front Door pricing](https://azure.microsoft.com/pricing/details/frontdoor/).

## Base fees

Each Front Door profile incurs an hourly fee. You're billed for each hour, or partial hour, that your profile is deployed. The rate you're charged depends on the Front Door tier that you deploy.

A single Front Door profile can contain multiple [endpoints](endpoint.md). You're not billed extra for each endpoint.

You don't pay extra fees to use features like [traffic acceleration](front-door-traffic-acceleration.md), [response caching](front-door-caching.md), [response compression](front-door-caching.md#file-compression), the [rules engine](front-door-rules-engine.md), [Front Door's inherent DDoS protection](front-door-ddos.md), and [custom web application firewall (WAF) rules](web-application-firewall.md#custom-rules). If you use Front Door Premium, you also don't pay extra fees to use [managed WAF rule sets](web-application-firewall.md#managed-rules) or [Private Link origins](private-link.md).

## Request processing and traffic fees

Each request that goes through Front Door incur request processing and traffic fees:

Each part of the request process is billed separately:

1. Number of requests from client to Front Door

1. Data transfer from Front Door edge to origin

1. Data transfer from origin to Front Door (nonbillable)

1. Data transfer from Front Door to client

The following sections describe each of these request components in more detail.

### Number of requests from client to Front Door

Front Door charges a fee for the number of requests that are received at a Front Door edge location for your profile. Front Door identifies requests by using the `Host` header on the HTTP request. If the `Host` header matches one from your Front Door profile, it counts as a request to your profile.

The price is different depending on the geographical region of the Front Door edge location that serves the request. The price is also different for the Standard and Premium SKUs.

### Data transfer from Front Door edge to origin

Front Door charges for the bytes that are sent from the Front Door edge location to your origin server. The price is different depending on the geographical region of the Front Door edge location that serves the request. The location of the origin doesn't affect the price.

The price per gigabyte is lower when you have higher volumes of traffic.

If the request can be served from the Front Door edge location's cache, Front Door doesn't send any request to the origin server, and you aren't billed for this component.

### Data transfer from origin to Front Door

When your origin server processes a request, it sends data back to Front Door so that it can be returned to the client. This traffic doesn't get billed by Front Door, even if the origin is in a different region to the Front Door edge location for the request.

If your origin is within Azure, the data egress from the Azure origin to Front Door isn't charged. However, you should determine whether those Azure services might bill you to process your requests.

If your origin is outside of Azure, you might incur charges from other network providers.

### Data transfer from Front Door to client

Front Door charges for the bytes that are sent from the Front Door edge location back to the client. The price is different depending on the geographical region of the Front Door edge location that serves the request.

If a response is compressed, Front Door only charges for the compressed data.

## Private Link origins

When you use the Premium tier, Front Door can [connect to your origin by using Private Link](private-link.md).

Front Door Premium has a higher base fee and request processing fee. You don't pay extra for Private Link traffic compared to traffic that uses an origin's public endpoint.

When you configure a Private Link origin, you select a region for the private endpoint to use. A [subset of Azure regions support Private Link traffic for Front Door](private-link.md#region-availability). If the region you select is different to the region the origin is deployed to, there isn't an extra charge for cross-region traffic. However, the request latency likely is greater.

## Cross-region traffic

Some of the Front Door billing meters have different rates depending on the location of the Front Door edge location that processes a request. Usually, [the Front Door edge location that processes a request is the one that's closest to the client](front-door-traffic-acceleration.md#select-the-front-door-edge-location-for-the-request-anycast), which helps to reduce latency and maximize performance.

Front Door charges for traffic from the edge location to the origin. Traffic is charged at different rates depending on the location of the Front Door edge location. If your origin is in a different Azure region, you aren't billed extra for inter-region traffic.

## Example scenarios

### Example 1: Azure origin without caching

Contoso hosts their website on Azure App Service, which runs in the West US region. Contoso deployed Front Door with the standard tier. They disabled caching.

Suppose a request from a client in California is sent to the Contoso website, sending a 1-KB request and receiving a 100-KB response:

The following billing meters are incremented:

| Meter | Incremented by | Billing region |

|-|-|-|

| Number of requests from client to Front Door | 1 | North America |

| Data transfer from Front Door edge to origin | 1 KB | North America |

| Data transfer from Front Door to client | 100 KB | North America |

Azure App Service might charge other fees.

### Example 2: Azure origin with compression enabled

Suppose Contoso updates their Front Door configuration to enable [content compression](front-door-caching.md#file-compression). Now, the same response as in example 1 might be able to be compressed down to 30 KB:

The following billing meters are incremented:

| Meter | Incremented by | Billing region |

|-|-|-|

| Number of requests from client to Front Door | 1 | North America  |

| Data transfer from Front Door edge to origin | 1 KB | North America |

| Data transfer from Front Door to client | 30 KB | North America |

Azure App Service might charge other fees.

### Example 3: Request served from cache

Suppose a second request arrives at the same Front Door edge location and a valid cached response is available:

The following billing meters are incremented:

| Meter | Incremented by | Billing region |

|--|--|--|

| Number of requests from client to Front Door | 1 | North America |

| Data transfer from Front Door edge to origin | *none when request is served from cache* |  |

| Data transfer from Front Door to client | 30 KB | North America |

### Example 4: Cross-region traffic

Suppose a request to Contoso's website comes from a client in Australia, and can't be served from cache:

The following billing meters are incremented:

| Meter | Incremented by | Billing region |

|-|-|-|

| Number of requests from client to Front Door | 1 | Australia |

| Data transfer from Front Door edge to origin | 1 KB | Australia |

| Data transfer from Front Door to client | 30 KB | Australia |

### Example 5: Non-Azure origin

Fabrikam runs an eCommerce site on another cloud provider. Their site is hosted in Europe. They configured Azure Front Door to serve the traffic without caching or compression.

Suppose a request from a client is sent to the Fabrikam website from a client in New York. The client sends a 2-KB request and receives a 350-KB response:

The following billing meters are incremented:

| Meter | Incremented by | Billing region |

|-|-|-|

| Number of requests from client to Front Door | 1 | North America |

| Data transfer from Front Door edge to origin | 2 KB | North America |

| Data transfer from Front Door to client | 350 KB | North America |

The external cloud provider might charge other fees.

### Example 6: Request blocked by web application firewall

When a request gets blocked by the web application firewall (WAF), it isn't sent to the origin. However, Front Door charges the request, and also charges to send a response.

Suppose a Front Door profile includes a custom WAF rule to block requests from a specific IP address in South America. The WAF is configured with a custom error response page, which is 1 KB in size. If a client from the blocked IP address sends a 1-KB request:

The following billing meters are incremented:

| Meter | Incremented by | Billing region |

|-|-|-|

| Number of requests from client to Front Door | 1 | South America |

| Data transfer from Front Door edge to origin | *none* | South America |

| Data transfer from Front Door to client | 1 KB | South America |

## Next steps

Learn how to [create an Front Door profile](create-front-door-portal.md).


# Understanding Pricing

# Compare pricing between Azure Front Door tiers

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium :heavy_check_mark: Front Door (classic)

> [!NOTE]

> Prices shown in this article are examples and are for illustration purposes only. For pricing information according to your region, see the [Pricing page](https://azure.microsoft.com/pricing/details/frontdoor/)

Azure Front Door has three tiers: Standard, Premium, and (classic). This article describes the billing model for Azure Front Door and compares the pricing for the Standard, Premium, and (classic) tiers. When migrating from Azure Front Door (classic) to Standard or Premium, we recommend you do a cost analysis to understand the pricing differences between the tiers. We show you how to evaluate cost that you can apply your environment.

## Pricing model comparison

| Pricing dimensions | Standard | Premium | Classic |

|--|--|--|--|

| Base fees (per month) | $35 | $330 | N/A |

| Outbound data transfer from edge location to client (per GB) | Varies by 8 zones | Same as standard | - Varies by 5 zones </br>- Higher unit rates when compared to Standard/Premium |

| Outbound data transfer from edge to the origin (per GB) | Varies by 8 zones | Same as standard | Free |

| Incoming requests from client to Front Door’s edge location (per 10,000 requests) | Varies by 8 zones | - Varies by 8 zones </br>- Higher unit rate than Standard | Free |

| First 5 routing rules (per hour) | Free | Free | $0.03 |

| Per additional routing rule (per hour) | Free | Free | $0.012 |

| Inbound data transfer (per GB) | Free | Free | $0.01 |

| Web Application Firewall custom rules | Free | Free | - $5/month/policy </br>- $1/month & $0.06 per million requests </br></br>For more information, see [Azure Web Application Firewall pricing](https://azure.microsoft.com/pricing/details/web-application-firewall/) |

| Web Application Firewall managed rules | Not supported | Free | - $5/month/policy </br>- $20/month + $1 per million requests </br></br>For more information, see [Azure Web Application Firewall pricing](https://azure.microsoft.com/pricing/details/web-application-firewall/) |

| Data transfer from an origin in Azure data center to Front Door's edge location | Free | Free | See [Bandwidth pricing](https://azure.microsoft.com/pricing/details/bandwidth/) |

| Private link to origin | Not supported | Free | Not supported |

| First 100 custom domains per month | Free | Free | Free |

| Per additional custom domain (per month) | Free | Free | $5 |

## Cost assessment

> [!NOTE]

> Azure Front Door Standard and Premium have a lower total cost of ownership than Azure Front Door (classic). If you have a request heavy workload, it's recommended to estimate the impact of the request meter of the new tiers. If you have multiple instances of Azure Front Door, it's recommended to estimate the impact of the base fee of the new tiers.

The following are general guidance for getting the right metrics to estimate the cost of the new tiers.

1. Pull the invoice for the Azure Front Door (classic) profile to get the monthly charges.

1. Compute the Azure Front Door Standard/Premium pricing using the following table:

| Azure Front Door Standard/Premium meter | How to calculate from Azure Front Door (classic) metrics |

|--|--|

| Base fee | - If you need managed WAF (Web Application Firewall) rules, bot protection, or Private Link: **$330/month** </br> - If you only need custom WAF rules: **$35/month** |

| Requests | **For Standard:** </br>1. Go to your Azure Front Door (classic) profile, select **Metrics** from under *Monitor* in the left side menu pane. </br>2. Select the **Request Count** from the *Metrics* drop-down menu. </br> 3. To view regional metrics, you can apply a split to the data by selecting **Client Country** or **Client Region**. </br> 4. If you select *Client Country*, you need to map them to the corresponding Azure Front Door pricing zone. </br> :::image type="content" source="./media/understanding-pricing/request-count.png" alt-text="Screenshot of the request count metric for Front Door (classic)." lightbox="./media/understanding-pricing/request-count.png"::: </br> **For Premium:** </br>You can look at the **Request Count** and the **WAF Request Count** metric in the Azure Front Door (classic) profile. </br> :::image type="content" source="./media/understanding-pricing/waf-request-count.png" alt-text="Screenshot of the Web Application Firewall request count metric for Front Door (classic)." lightbox="./media/understanding-pricing/waf-request-count.png"::: |

| Egress from Azure Front Door edge to client | You can obtain this data from your Azure Front Door (classic) invoice or from the **Billable Response Size** metric in the Azure Front Door (classic) profile. To get a more accurate estimation, apply split by *Client Count* or *Client Region*.</br> :::image type="content" source="./media/understanding-pricing/billable-response-size.png" alt-text="Screenshot of the billable response size metric for Front Door (classic)." lightbox="./media/understanding-pricing/billable-response-size.png"::: |

| Ingress from Azure Front Door edge to origin | You can obtain this data from your Azure Front Door (classic) invoice. Refer to the quantities for Data transfer from client to edge location as an estimation. |

1. Go to the [pricing calculator](https://azure.microsoft.com/pricing/calculator/?service=frontdoor-standard-premium).

1. Select the appropriate Azure Front Door tier and zone.

1. Calculate the total cost for the Azure Front Door Standard/Premium profile from the metrics you obtained in the previous step.

## Example scenarios

Azure Front Door Standard/Premium cost less than Azure Front Door (classic) in the first three scenarios. However, in scenario 4 and 5 there are situations where Azure Front Door Standard/Premium can incur higher charges than Azure Front Door (classic). In these scenarios, you can use the cost assessment to estimate the cost of the new tiers.

### Scenario 1: A static website with custom WAF rules

* 10 routing rules and 10 WAF custom rules are configured.

* 20 TB of outbound data transfer.

* 200 million requests from client to Azure Front Door edge. (Including 100 million custom WAF requests).

* 100 GB outbound data transfer (cache hit ratio = 95%)

* Traffic originates from North America and Europe.

| Cost dimensions | Azure Front Door (classic) | Azure Front Door Standard |

|--|--|--|

| Base fee | $0 | $35 |

| Egress from Azure Front Door edge to client | $3,200 = (10 TB * $0.17/GB) + (10 TB * $0.15/GB) | $1,490 = (10 TB * $0.083/GB) + (10 GB * $0.066/GB) |

| Egress from Azure Front Door edge to origin | $0 | $2 = 100 GB * $0.02/GB |

| Ingress from client to Azure Front Door edge | $1 = 100 GB * $0.01/GB | $0 |

| Ingress from origin to Azure Front Door edge | $78.30 = (0.1 TB * $0/GB) + (0.9 TB * $0.087/GB) | $ |

| Requests | $0 | $180 = 200M requests * $0.009/10k requests |

| Routing rules | $153.15 = (($0.03 * 5 rules) + ($0.012 * 5 rules)) * 730 hours | $0 |

| WAF policy | $5 =  $1 * 1 policy/month | $0 |

| WAF custom rules | $10 = $1 = * 10 rules/month | $0 |

| WAF custom rules requests processed |  $60 = 100 million requests * $0.60/1 million requests | $0 |

| Total | $3,507.50 | $1,727 |

Azure Front Door Standard is ~45% cheaper than Azure Front Door (classic) for static websites with custom WAF rules because of the lower egress cost and the free routing rules.

### Scenario 2: A static website with managed WAF rules

* 30 routing rules and 1 WAF managed rule set are configured.

* 20 TB of outbound data transfer.

* 200 million requests from client to Azure Front Door edge (Including 100 million managed WAF requests).

* Cache hit ration = 95%.

* Traffic originates from Asia Pacific (including Japan).

| Cost dimensions | Azure Front Door (classic) | Azure Front Door Premium |

|--|--|--|

| Base fee | $0 | $330 |

| Egress from Azure Front Door edge to client | $4,700 = (10 TB * $ 0.25/GB) + (10 TB * $ 0.22/GB) | $2,130 = (10 TB * $ 0.115/GB) + 10 TB * ($ 0.098/GB)  |

| Egress from Azure Front Door edge to origin | $0 | $2 = 100 GB * $0.02/GB |

| Ingress from client to Azure Front Door edge | $1 = 100 GB * $0.01/GB | $0 |

| Ingress from origin to Azure Front Door edge | $108 = (0.1 TB * $ 0/GB) + (0.9 TB * $ 0.12/GB) | $0 |

| Requests | $0 | $300 = 200M requests * $0.015/10K requests |

| Routing rules | $328.5 = (($0.03 * 5 rules) + ($.012 * 25 rules)) * 730 hrs  | $0 |

| WAF policy | $5 = $1 * 1 policy/month  | $0 |

| WAF managed/default rule set | $20 = $20 * 1 rule set/month | $0 |

| WAF managed/ defaults rule set requests processed | $100 = 100 million requests * $1/1 million requests |

| Total | $5,263.50 | $2,762 |

Azure Front Door Premium is ~45% cheaper than Azure Front Door (classic) for static websites with managed WAF rules because of the lower egress cost and the free routing rules.

### Scenario 3: File downloads

* Two routing rules are configured.

* 150 TB of outbound data transfer.

* 1.5 million requests from client to Azure Front Door edge (cache hit ration = 95%)

* Traffic originates from India.

| Cost dimensions | Azure Front Door (classic) | Azure Front Door Standard |

|--|--|--|

| Base fee | $0 | $35 |

| Egress from Azure Front Door edge to client | $39,500 = (10 TB * $ 0.34/GB) + (40 TB * $ 0.29/GB) + (100 TB * $ 0.245/GB) | $12,790 = (10 TB * $ 0.109/GB) + (40 TB * $ 0.085/GB) + (100 TB * $ 0.083/GB) |

| Egress from Azure Front Door edge to origin | $0 | $0.72= 4.5 GB * $0.16/GB |

| Ingress from client to Azure Front Door edge | $0.05 = 4.5 GB * $0.01  | $0 |

| Ingress from origin to Azure Front Door edge | $900 = 0.1 TB * $ 0/GB + 7.5 TB * $ 0.12/GB | $0 |

| Requests | $0 | $1.62 = 1.5 million requests * $0.0108 per 10,000 requests |

| Routing rules | $$43.8 = ($0.03 * 2 rules) * 730 hrs  | $0 |

| Total | $40,444 | $12,827.34 |

Azure Front Door Standard is ~68% cheaper than Azure Front Door (classic) for file downloads because of the lower egress cost.

### Scenario 4: Request heavy scenario with WAF protection

* 150 routing rules are configured to origins in different countries/regions.

* 20 TB of outbound data transfer.

* 10 TB of inbound data transfer.

* 5 billion requests from client to Azure Front Door edge.

* 2.4 billion WAF requests (1.2 billion managed WAF rule requests and 1.2 billion custom WAF rule requests).

* Traffic originates from North America

| Cost dimensions | Azure Front Door (classic) | Azure Front Door Premium |

|--|--|--|

| Base fee | $0 | $330 = $330 * 1 profile |

| Egress from Azure Front Door edge to client | $3,200 = (10 TB * $0.17/GB) + (10 TB * $0.15/GB) | $1,490 = (10 TB * $0.083/GB) + (10 TB * $0.066/GB) |

| Egress from Azure Front Door edge to origin | $0 | $200 = 10 TB * $0.02/GB  |

| Ingress from client to Azure Front Door edge | $100 = 10 TB * $.01/GB   | $0 |

| Ingress from origin to Azure Front Door edge | $1,692 = (0.1 TB * $ 0/GB) + (9.9 TB * $ 0.087/GB) + (10 TB * $ 0.083/GB) | $0 |

| Requests | $0 | $6,748 |

| Routing rules | $1380 = (($0.03 * 5 rules) + ($0.012 * 145 rules)) * 730 hrs   | $0 |

| WAF policy | $5 = $5 * 1 policy/month| $0 |

| WAF custom rules | $1 = $1 * 1 rule/month | $0 |

| WAF custom rule request processed | $720 = 1.2 billion requests * $0.60 per million requests | $0 |

| WAF managed/default rule set | $20 = $20 * 1 rule set/month | $0 |

| WAF managed/ defaults rule set requests processed | $1200 = 1.2 billion requests * $1 per million requests | $0 |

| Total | $8,318 | $8,768 |

In this comparison, Azure Front Door Premium is ~5% more expensive than Azure Front Door (classic) because of the higher request cost and the base fee. You're paying less for outbound data transfer and don't have to pay for each routing rule, WAF rules and data transfer from the origin to the edge separately. If the cost increase is significant, reach out to your Microsoft sales representative to discuss options.

### Scenario 5: Social media application with multiple Front Door (classic) profiles with WAF protection

* The application is designed in a micro-services architecture with static and dynamic traffic. Each micro service component is deployed in a separate Azure Front Door (classic) profile. In total, there are 80 Azure Front Door (classic) profiles (30 dev/test, 50 production).

* In each profile, there are 10 routing rules configured to route traffic to different backends based on the path.

* There are two WAF policies with two rule sets to protect the application from top CVE attacks.

* 50 million requests per month.

* 50 TB of outbound data transfer from Azure Front Door edge to client.

* 1 TB of outbound data transfer from Azure Front Door edge to origin (20 million requests get blocked by WAF).

* Traffic mostly originates from North America.

| Cost dimensions | Azure Front Door (classic) | Azure Front Door Premium |

|--|--|--|

| Base fee | $0 | $26,400 = $330 x 80 profiles |

| Egress from Azure Front Door edge to client | $7,700 = (10 TB * $0.17/GB) + (40 TB * $0.15/GB) | $3,470 = (10 TB * $0.083/GB) + (40 TB * $0.066/GB) |

| Egress from Azure Front Door edge to origin | $0 | $200 = 10 TB * $0.02/GB  |

| Ingress from client to Azure Front Door edge | $10 = 1 TB * $.01/GB | $0 |

| Ingress from origin to Azure Front Door edge | $2106.30 = (0.1 TB * $0/GB) + (9.9 TB * $0.087/GB) + (15 TB * $0.083/GB) | $0 |

| Requests | $0 | $75 = 50 million requests * $0.15 per 10,000 requests |

| Routing rules | $7665 = (($0.03 * 5 rules) + ($0.012 * 5 rules)) * 730 hrs * 80 instances | $0 |

| WAF policy | $10 = $5 * 2 policy/month | $0 |

| WAF managed/default rule set | $40 = $20 * 2 rule set/month | $0 |

| WAF managed/ defaults rule set requests processed | $20 = 20 million requests * $1 per million requests | $0 |

| Total | $17,551 .30| $29,945 |

In this comparison, Azure Front Door Premium is 1.7x more expensive than Azure Front Door (classic) because of the higher base fee for each profile. The outbound data transfer is 45% less for Azure Front Door Premium compared to Azure Front Door (classic). With Premium tier, you don't have to pay for route rules, which account for $7,700 of the total cost.

#### Suggestion to reduce cost

* Check if all 80 instances of Azure Front Door (classic) are required. Remove unnecessary resources, such as temporary testing environments.

* Migrate your most important Front Door (classic) profiles to Azure Front Door Standard/Premium based on the necessity of features available in the upgrade tier.

* You can manually create Azure Front Door Premium profiles with multiple endpoints to reflect each Azure Front Door (classic) profile.

The following table shows the cost breakdown for migrating 60 Azure Front Door (classic) profiles to four Azure Front Door Premium profiles with 15 endpoints each. The overall cost saving is about 27% less for Azure Front Door Premium compared to Azure Front Door (classic).

| Cost dimensions | Azure Front Door (classic) | Azure Front Door Premium |

|--|--|--|

| Configuration | 60 profiles | 30 production microservices, 300 routing rules (30 endpoints * 10 routing rules) </br> - 2 profiles with 15 endpoints and 150 routing rules per profile </br>30 dev/testing microservices, 300 routing rules (30 endpoints * 10 routing rules)</br> - 2 profiles with 15 endpoints and 150 routing rules per profile |

| Base fee | $0 | $1320 = $330 * 4 profiles |

| Egress from Azure Front Door edge to client | $7,700 = (10 TB * $0.17/GB) + (40 TB * $0.15/GB) | $3,470 = (10 TB * $0.083/GB) + (40 TB * $0.066/GB) |

| Egress from Azure Front Door edge to origin | $0 | $20 = 1 TB * $0.02/GB  |

| Ingress from client to Azure Front Door edge | $10 = 1 TB * $.01/GB | $0 |

| Ingress from origin to Azure Front Door edge | $2106.30 = (0.1 TB * $0/GB) + (9.9 TB * $0.087/GB) + (15 TB * $0.083/GB) | $0 |

| Requests | $0 | $75 = 50 million requests * $0.15 per 10,000 requests |

| Routing rules | $7665 = (($0.03 * 5 rules) + ($0.012 * 5 rules)) * 730 hrs * 80 instances | $0 |

| WAF policy | $10 = $5 * 2 policy/month | $0 |

| WAF managed/default rule set | $40 = $20 * 2 rule set/month | $0 |

| WAF managed/ defaults rule set requests processed | $20 = 20 million requests * $1 per million requests | $0 |

| Total | $17,551.30 | $4,885 |

## Related content

* Learn about how [settings are mapped](tier-mapping.md) from Azure Front Door (classic) to Azure Front Door Standard/Premium.

* Learn about [Azure Front Door (classic) tier migration](tier-migration.md).

* Learn how to [migrate from Azure Front Door (classic) to Azure Front Door Standard/Premium](migrate-tier.md).


# Domain

# Domains in Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

A *domain* represents a custom domain name that Azure Front Door uses to receive your application's traffic. Azure Front Door supports adding three types of domain names:

- **Subdomains** are the most common type of custom domain name. An example subdomain is `myapplication.contoso.com`.

- **Apex domains** don't contain a subdomain. An example apex domain is `contoso.com`. For more information about using apex domains with Azure Front Door, see [Apex domains](./apex-domain.md).

- **Wildcard domains** allow traffic to be received for any subdomain. An example wildcard domain is `*.contoso.com`. For more information about using wildcard domains with Azure Front Door, see [Wildcard domains](./front-door-wildcard-domain.md).

Domains are added to your Azure Front Door profile. You can use a domain in multiple routes within an endpoint, if you use different paths in each route.

To learn how to add a custom domain to your Azure Front Door profile, see [Configure a custom domain on Azure Front Door using the Azure portal](standard-premium/how-to-add-custom-domain.md).

## DNS configuration

When you add a domain to your Azure Front Door profile, you configure two records in your DNS server:

* A DNS TXT record, which is required to validate ownership of your domain name. For more information on the DNS TXT records, see [Domain validation](#domain-validation).

* A DNS CNAME record, which controls the flow of internet traffic to Azure Front Door.

> [!TIP]

> You can add a domain name to your Azure Front Door profile before making any DNS changes. This approach can be helpful if you need to set your Azure Front Door configuration together, or if you have a separate team that changes your DNS records.

>

> You can also add your DNS TXT record to validate your domain ownership before you add the CNAME record to control traffic flow. This approach can be useful to avoid experiencing migration downtime if you have an application already in production.

## Domain validation

All domains added to Azure Front Door must be validated. Validation helps to protect you from accidental misconfiguration, and also helps to protect other people from domain spoofing. In some situation, domains can be *prevalidated* by another Azure service. Otherwise, you need to follow the Azure Front Door domain validation process to prove your ownership of the domain name.

* **Azure pre-validated domains** are domains that have been validated by another supported Azure service. If you onboard and validate a domain to another Azure service, and then configure Azure Front Door later, you might work with a prevalidated domain. You don't need to validate the domain through Azure Front Door when you use this type of domain.

> [!NOTE]

> Azure Front Door currently only accepts pre-validated domains that have been configured with [Azure Static Web Apps](https://azure.microsoft.com/products/app-service/static/).

* **Non-Azure validated domains** are domains that aren't validated by a supported Azure service. This domain type can be hosted with any DNS service, including [Azure DNS](https://azure.microsoft.com/products/dns/), and requires that domain ownership is validated by Azure Front Door.

### TXT record validation

To validate a domain, you need to create a DNS TXT record. The name of the TXT record must be of the form `_dnsauth.{subdomain}`. Azure Front Door provides a unique value for your TXT record when you start to add the domain to Azure Front Door.

For example, suppose you want to use the custom subdomain `myapplication.contoso.com` with Azure Front Door. First, you should add the domain to your Azure Front Door profile, and note the TXT record value that you need to use. Then, you should configure a DNS record with the following properties:

| Property | Value |

|-|-|

| Record name | `_dnsauth.myapplication` |

| Record value | *use the value provided by Azure Front Door* |

| Time to live (TTL) | 1 hour |

After your domain has been validated successfully, you can safely delete the TXT record from your DNS server.

For more information on adding a DNS TXT record for a custom domain, see [Configure a custom domain on Azure Front Door using the Azure portal](standard-premium/how-to-add-custom-domain.md).

### Domain validation states

The following table lists the validation states that a domain might show.

| Domain validation state | Description and actions |

|--|--|

| Submitting | The custom domain is being created. <br /><br /> Wait until the domain resource is ready. |

| Pending | The DNS TXT record value has been generated, and Azure Front Door is ready for you to add the DNS TXT record. <br /><br /> Add the DNS TXT record to your DNS provider and wait for the validation to complete. If the status remains **Pending** even after the TXT record has been updated with the DNS provider, select **Regenerate** to refresh the TXT record then add the TXT record to your DNS provider again. |

| Pending revalidation | The managed certificate is less than 45 days from expiring. <br /><br /> If you have a CNAME record already pointing to the Azure Front Door endpoint, no action is required for certificate renewal. If the custom domain is pointed to another CNAME record, select the **Pending re-validation** status, and then select **Regenerate** on the *Validate the custom domain* page. Lastly, select **Add** if you're using Azure DNS or manually add the TXT record with your own DNS provider’s DNS management. |

| Refreshing validation token | A domain goes into a *Refreshing Validation Token* state for a brief period after the **Regenerate** button is selected. Once a new TXT record value is issued, the state changes to **Pending**. <br /> No action is required. |

| Approved | The domain has been successfully validated, and Azure Front Door can accept traffic that uses this domain. <br /><br /> No action is required. |

| Rejected | The certificate provider/authority has rejected the issuance for the managed certificate. For example, the domain name might be invalid. <br /><br /> Select the **Rejected** link and then select **Regenerate** on the *Validate the custom domain* page, as shown in the screenshots below this table. Then, select **Add** to add the TXT record in the DNS provider. |

| Timeout | The TXT record wasn't added to your DNS provider within seven days, or an invalid DNS TXT record was added. <br /><br /> Select the **Timeout** link and then select **Regenerate** on the *Validate the custom domain* page. Then select **Add** to add a new TXT record to the DNS provider. Ensure that you use the updated value. |

| Internal error | An unknown error occurred. <br /><br /> Retry validation by selecting the **Refresh** or **Regenerate** button. If you're still experiencing issues, submit a support request to Azure support. |

> [!NOTE]

> - The default TTL for TXT records is 1 hour. When you need to regenerate the TXT record for re-validation, pay attention to the TTL for the previous TXT record. If it doesn't expire, the validation will fail until the previous TXT record expires.

> - If the **Regenerate** button doesn't work, delete and recreate the domain.

> - If the domain state doesn't reflect as expected, select the **Refresh** button.

## HTTPS for custom domains

By using the HTTPS protocol on your custom domain, you ensure your sensitive data is delivered securely with TLS/SSL encryption when it's sent across the internet. When a client, like a web browser, is connected to a website by using HTTPS, the client validates the website's security certificate, and ensures it was issued by a legitimate certificate authority. This process provides security and protects your web applications from attacks.

Azure Front Door supports using HTTPS with your own domains, and offloads transport layer security (TLS) certificate management from your origin servers. When you use custom domains, you can either use Azure-managed TLS certificates (recommended), or you can purchase and use your own TLS certificates.

For more information on how Azure Front Door works with TLS, see [End-to-end TLS with Azure Front Door](end-to-end-tls.md).

### Azure Front Door-managed TLS certificates

Azure Front Door can automatically manage TLS certificates for subdomains and apex domains. When you use managed certificates, you don't need to create keys or certificate signing requests, and you don't need to upload, store, or install the certificates. Additionally, Azure Front Door can automatically rotate (renew) managed certificates without any human intervention. This process avoids downtime caused by a failure to renew your TLS certificates in time.

The process of generating, issuing, and installing a managed TLS certificate can take from several minutes to an hour to complete, and occasionally it can take longer.

> [!NOTE]

> Azure Front Door (Standard and Premium) managed certificates are automatically rotated if the domain CNAME record points directly to a Front Door endpoint. Otherwise, you need to re-validate the domain ownership to rotate the certificates.

#### Domain types

The following table summarizes the features available with managed TLS certificates when you use different types of domains:

| Consideration | Subdomain | Apex domain | Wildcard domain |

|-|-|-|-|

| Managed TLS certificates available | Yes | Yes | Yes |

| Managed TLS certificates are rotated automatically | Yes | See below | No |

When you use Azure Front Door-managed TLS certificates with apex domains, the automated certificate rotation might require you to revalidate your domain ownership. For more information, see [Apex domains in Azure Front Door](apex-domain.md#azure-front-door-managed-tls-certificate-rotation).

#### Managed certificate issuance

Azure Front Door's certificates are issued by our partner certification authority, DigiCert. For some domains, you must explicitly allow DigiCert as a certificate issuer by creating a [CAA domain record](https://wikipedia.org/wiki/DNS_Certification_Authority_Authorization) with the value: `0 issue digicert.com`.

Azure fully manages the certificates on your behalf, so any aspect of the managed certificate, including the root issuer, can change at any time. These changes are outside your control. Make sure to avoid hard dependencies on any aspect of a managed certificate, such as checking the certificate thumbprint, or pinning to the managed certificate or any part of the certificate hierarchy. If you need to pin certificates, you should use a customer-managed TLS certificate, as explained in the next section.

### Customer-managed TLS certificates

Sometimes, you might need to provide your own TLS certificates. Common scenarios for providing your own certificates include:

* Your organization requires you to use certificates issued by a specific certification authority.

* You want Azure Key Vault to issue your certificate by using a partner certification authority.

* You need to use a TLS certificate that a client application recognizes.

* You need to use the same TLS certificate on multiple systems.

* You use [wildcard domains](front-door-wildcard-domain.md). Azure Front Door doesn't provide managed certificates for wildcard domains.

> [!NOTE]

> * As of September 2023, Azure Front Door supports Bring Your Own Certificates (BYOC) for domain ownership validation. Front Door approves the domain ownership if the Certificate Name (CN) or Subject Alternative Name (SAN) of the certificate matches the custom domain. If you select Azure managed certificate, the domain validation uses the DNS TXT record.

> * For custom domains created before BYOC based validation, and the domain validation status isn't **Approved**, you need to trigger the auto approval of the domain ownership validation by selecting the **Validation State** and clicking on the **Revalidate** button in the portal. If you use the command line tool, you can trigger domain validation by sending an empty PATCH request to the domain API.

#### Certificate requirements

To use your certificate with Azure Front Door, it must meet the following requirements:

- **Complete certificate chain:** When you create your TLS/SSL certificate, you must create a complete certificate chain with an allowed certificate authority (CA) that is part of the [Microsoft Trusted CA List](https://ccadb.my.salesforce-sites.com/microsoft/IncludedCACertificateReportForMSFT). If you use a nonallowed CA, your request is rejected. The root CA must be part of the [Microsoft Trusted CA List](https://ccadb.my.salesforce-sites.com/microsoft/IncludedCACertificateReportForMSFT). If a certificate without complete chain is presented, the requests that involve that certificate aren't guaranteed to work as expected.

- **Common name:** The common name (CN) of the certificate must match the domain configured in Azure Front Door.

- **Algorithm:** Azure Front Door doesn't support certificates with elliptic curve (EC) cryptography algorithms.

- **File (content) type:** Your certificate must be uploaded to your key vault from a PFX file, which uses the `application/x-pkcs12` content type.

#### Import a certificate to Azure Key Vault

Custom TLS certificates must be imported into Azure Key Vault before you can use it with Azure Front Door. To learn how to import a certificate to a key vault, see [Tutorial: Import a certificate in Azure Key Vault](/azure/key-vault/certificates/tutorial-import-certificate).

The key vault must be in the same Azure subscription as your Azure Front Door profile.

> [!WARNING]

> Azure Front Door only supports key vaults in the same subscription as the Front Door profile. Choosing a key vault under a different subscription than your Azure Front Door profile will result in a failure.

Certificates must be uploaded as a **certificate** object, rather than a **secret**.

#### Grant access to Azure Front Door

Azure Front Door needs to access your key vault to read your certificate. You need to configure both the key vault's network firewall and the vault's access control.

If your key vault has network access restrictions enabled, you must configure your key vault to allow trusted Microsoft services to bypass the firewall.

There are two ways you can configure access control on your key vault:

* Azure Front Door can use a managed identity to access your key vault. You can use this approach when your key vault uses Microsoft Entra authentication. For more information, see [Use managed identities with Azure Front Door Standard/Premium](managed-identity.md).

* Alternatively you can grant Azure Front Door's service principal access to your key vault. You can use this approach when you use vault access policies.

#### Add your custom certificate to Azure Front Door

After you've imported your certificate to a key vault, create an Azure Front Door secret resource, which is a reference to the certificate you added to your key vault.

Then, configure your domain to use the Azure Front Door secret for its TLS certificate.

For a guided walkthrough of these steps, see [Configure HTTPS on an Azure Front Door custom domain using the Azure portal](standard-premium/how-to-configure-https-custom-domain.md#use-your-own-certificate).

### Switch between certificate types

You can change a domain between using an Azure Front Door-managed certificate and a user-managed certificate.

* It might take up to an hour for the new certificate to be deployed when you switch between certificate types.

* If your domain state is *Approved*, switching the certificate type between a user-managed and a managed certificate won't cause any downtime.

* When switching to a managed certificate, Azure Front Door continues to use the previous certificate until the domain ownership is revalidated and the domain state becomes *Approved*.

* If you switch from BYOC to managed certificate, domain revalidation is required. If you switch from managed certificate to BYOC, you're not required to revalidate the domain.

### Certificate renewal

#### Renew Azure Front Door-managed certificates

For most custom domains, Azure Front Door automatically renews (rotates) managed certificates when they're close to expiry, and you don't need to do anything.

However, Azure Front Door won't automatically rotate certificates in the following scenarios:

* The custom domain's CNAME record is pointing to a DNS record other than your Azure Front Door endpoint's domain.

* The custom domain points to the Azure Front Door endpoint through a chain.

* The custom domain uses an A record. We recommend you always use a CNAME record to point to Azure Front Door.

* The custom domain is an [apex domain](apex-domain.md) and uses CNAME flattening.

If one of the scenarios above applies to your custom domain, then 45 days before the managed certificate expire, the domain validation state becomes *Pending Revalidation*. The *Pending Revalidation* state indicates that you need to create a new DNS TXT record to revalidate your domain ownership.

> [!NOTE]

> DNS TXT records expire after seven days. If you previously added a domain validation TXT record to your DNS server, you need to replace it with a new TXT record. Ensure you use the new value, otherwise the domain validation process will fail.

If your domain can't be validated, the domain validation state becomes *Rejected*. This state indicates that the certificate authority has rejected the request for reissuing a managed certificate.

For more information on the domain validation states, see [Domain validation states](#domain-validation-states).

#### Renew Azure-managed certificates for domains prevalidated by other Azure services

Azure-managed certificates are automatically rotated by the Azure service that validates the domain.

#### <a name="rotate-own-certificate"></a>Renew customer-managed TLS certificates

When you update the certificate in your key vault, Azure Front Door can automatically detect and use the updated certificate. For this functionality to work, set the secret version to 'Latest' when you configure your certificate in Azure Front Door.

If you select a specific version of your certificate, you have to reselect the new version manually when you update your certificate.

It takes up to 72 hours for the new version of the certificate/secret to be automatically deployed.

If you want to change the secret version from ‘Latest’ to a specified version or vice versa, add a new certificate.

## Security policies

You can use Azure Front Door's web application firewall (WAF) to scan requests to your application for threats, and to enforce other security requirements.

To use the WAF with a custom domain, use an Azure Front Door security policy resource. A security policy associates a domain with a WAF policy. You can optionally create multiple security policies so that you can use different WAF policies with different domains.

## Related content

* To learn how to add a custom domain to your Azure Front Door profile, see [Configure a custom domain on Azure Front Door using the Azure portal](standard-premium/how-to-add-custom-domain.md).

* Learn more about how [End-to-end TLS with Azure Front Door](end-to-end-tls.md).


# Front Door Url Redirect

# URL redirect

Azure Front Door can redirect traffic at each of the following levels: protocol, hostname, path, and query string. You can configure these functionalities for individual microservices since the redirection is path-based. This setup simplifies application configuration by optimizing resource usage, and supports new redirection scenarios including global and path-based redirection.

In Azure Front Door Standard/Premium tier, you can configure URL redirect using a Rule Set.

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

## Redirection types

A redirect type sets the response status code so clients understand the purpose of the redirect. Azure Front Door supports the following types of redirection:

- **301 (Moved permanently)**: Indicates that the target resource has a new permanent URI. Any future references to this resource use one of the enclosed URIs. Use the 301 status code for HTTP to HTTPS redirection.

- **302 (Found)**: Indicates that the target resource is temporarily under a different URI. Since the redirection can change on occasion, the client should continue to use the effective request URI for future requests.

- **307 (Temporary redirect)**: Indicates that the target resource is temporarily under a different URI. The user agent **must not** change the request method if it does an automatic redirection to that URI. Since the redirection can change over time, the client ought to continue using the original effective request URI for future requests.

- **308 (Permanent redirect)**: Indicates that the target resource has a new permanent URI. Any future references to this resource should use one of the enclosed URIs.

## Redirection protocol

Set the protocol for redirection. The most common use case for the redirect feature is to set HTTP to HTTPS redirection.

- **HTTPS only**: Set the protocol to HTTPS only if you want to redirect the traffic from HTTP to HTTPS. Azure Front Door recommends that you always set the redirection to HTTPS only.

- **HTTP only**: Redirects the incoming request to HTTP. Use this value only if you want to keep your traffic HTTP, which is nonencrypted.

- **Match request**: This option keeps the protocol used by the incoming request. So, an HTTP request remains HTTP and an HTTPS request remains HTTPS after redirection.

## Destination host

As part of configuring a redirect routing, you can also change the hostname or domain for the redirect request. You can set this field to change the hostname in the URL for the redirection or otherwise preserve the hostname from the incoming request. So, using this field you can redirect all requests sent on `https://www.contoso.com/*` to `https://www.fabrikam.com/*`.

## Destination path

If you want to replace the path segment of a URL as part of redirection, set this field with the new path value. Otherwise, choose to preserve the path value as part of redirect. By using this field, you can redirect all requests sent to `https://www.contoso.com/*` to  `https://www.contoso.com/redirected-site`.

## Query string parameters

The set of query strings to use in the redirect URL. The value of this field overwrites the incoming query strings. Leaving this field empty preserves the incoming query string. Query string must be in `<key>=<value>` format, separated by `&`.

## Destination fragment

The destination fragment is the portion of URL after `#`, which the browser uses to land on a specific section of a web page. Set this field to add a fragment to the redirect URL.

## Related content

* Learn how to [create a Front Door](quickstart-create-front-door.md).

* Learn more about [Azure Front Door Rule Set](front-door-rules-engine.md).

* Learn [how Front Door works](front-door-routing-architecture.md).


# How To Reports

# Azure Front Door reports

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Azure Front Door analytics reports provide a built-in, all-around view of how your Azure Front Door profile behaves, along with associated web application firewall (WAF) metrics. You can also take advantage of [Azure Front Door's logs](../front-door-diagnostics.md?pivot=front-door-standard-premium) to do further troubleshooting and debugging.

The built-in reports include information about your traffic and your application's security. Azure Front Door provides traffic reports and security reports.

| Traffic report | Details |

|---------|---------|

| [Key metrics in all reports](#key-metrics-included-in-all-reports) | Shows overall data that were sent from Azure Front Door edge points of presence (PoPs) to clients, including:<ul><li>Peak bandwidth</li><li>Requests</li><li>Cache hit ratio</li><li>Total latency</li><li>5XX error rate</li></ul> |

| [Traffic by domain](#traffic-by-domain-report) | Provides an overview of all the domains within your Azure Front Door profile:<ul><li>Breakdown of data transferred out from the Azure Front Door edge to the client</li><li>Total requests</li><li>3XX/4XX/5XX response code by domains</li></ul> |

| [Traffic by location](#traffic-by-location-report) | <ul><li>Shows a map view of request and usage by top countries/regions<br/></li><li>Trend view of top countries/regions</li></ul> |

| [Usage](#usage-report) | <ul><li>Data transfer out from Azure Front Door edge to clients<br/></li><li>Data transfer out from origin to Azure Front Door edge<br/></li><li>Bandwidth from Azure Front Door edge to clients<br/></li><li>Bandwidth from origin to Azure Front Door edge<br/></li><li>Requests<br/></li><li>Total latency<br/></li><li>Request count trend by HTTP status code</li></ul> |

| [Caching](#caching-report) | <ul><li>Shows cache hit ratio by request count<br/></li><li>Trend view of hit and miss requests</li></ul> |

| [Top URL](#top-url-report) | <ul><li>Shows request count <br/></li><li>Data transferred <br/></li><li>Cache hit ratio <br/></li><li>Response status code distribution for the most requested 50 assets</li></ul> |

| [Top referrer](#top-referrer-report) | <ul><li>Shows request count <br/></li><li>Data transferred <br/></li><li>Cache hit ratio <br/></li><li>Response status code distribution for the top 50 referrers that generate traffic</li></ul> |

| [Top user agent](#top-user-agent-report) | <ul><li>Shows request count <br/></li><li>Data transferred <br/></li><li>Cache hit ratio <br/></li><li>Response status code distribution for the top 50 user agents that were used to request content</li></ul> |

| Security report | Details |

|---------|---------|

| Overview of key metrics | <ul><li>Shows matched WAF rules<br/></li><li>Matched OWASP rules<br/></li><li>Matched bot protection rules<br/></li><li>Matched custom rules</li></ul> |

| Metrics by dimensions | <ul><li>Breakdown of matched WAF rules trend by action<br/></li><li>Doughnut chart of events by Rule Set Type and event by rule group<br/></li><li>Break down list of top events by rule ID, countries/regions, IP address, URL, and user agent</li></ul>  |

> [!NOTE]

> Security reports are only available when you use the Azure Front Door premium tier.

Reports are free of charge. Most reports are based on access log data, but you don't need to enable access logs or make any configuration changes to use the reports.

## How to access reports

Reports are accessible through the Azure portal and through the Azure Resource Manager API. You can also [download reports as comma-separated values (CSV) files](#export-reports-in-csv-format).

Reports support any selected date range from the previous 90 days. With data points of every 5 mins, every hour, or every day based on the date range selected. Normally, you can view data with delay of within an hour and occasionally with delay of up to a few hours.

### Access reports by using the Azure portal

1. Sign in to the [Azure portal](https://portal.azure.com) and select your Azure Front Door Standard/Premium profile.

1. In the navigation pane, select **Reports** or **Security** under *Analytics*.

1. Select the report you want to view.

* Traffic by domain

* Usage

* Traffic by location

* Cache

* Top url

* Top referrer

* Top user agent

1. After choosing the report, you can select different filters.

- **Show data for:** Select the date range for which you want to view traffic by domain. Available ranges are:

* Last 24 hours

* Last 7 days

* Last 30 days

* Last 90 days

* This month

* Last month

* Custom date

By default, data is shown for the last seven days. For reports with line charts, the data granularity goes with the date ranges you selected as the default behavior.

* 5 minutes - one data point every 5 minutes for date ranges less than or equal to 24 hours. This granularity level can be used for date ranges that are 14 days or shorter.

* By hour – one data point every hour for date ranges between 24 hours and 30 days.

* By day – one data point per day for date ranges longer than 30 days.

Select **Aggregation** to change the default aggregation granularity.

- **Location:** Select one or more countries/regions to filter by the client locations. Countries/regions are grouped into six regions: North America, Asia, Europe, Africa, Oceania, and South America. Refer to [countries/regions mapping](https://en.wikipedia.org/wiki/Subregion). By default, all countries are selected.

- **Protocol:** Select either HTTP or HTTPS to view traffic data for the selected protocol.

- **Domains** - Select one or more endpoints or custom domains. By default, all endpoints and custom domains are selected.

* If you delete an endpoint or a custom domain in one profile and then recreate the same endpoint or domain in another profile, the report counts the new endpoint as a different endpoint.

* If you delete a custom domain and bind it to a different endpoint, the behavior depends on how you view the report. If you view the report by custom domains, then they're treated as one custom domain. If you view the report by endpoint, they're treated as separate items.

1. If you want to export the data to a CSV file, select the *Download CSV* link on the selected tab.

### Export reports in CSV format

You can download any of the Azure Front Door reports as a CSV file. Every CSV report includes some general information and the information is available in all CSV files:

| Value | Description |

|---------|---------|

| Report | The name of the report. |

| Domains | The list of the endpoints or custom domains for the report. |

| StartDateUTC | The start of the date range for which you generated the report, in Coordinated Universal Time (UTC). |

| EndDateUTC | The end of the date range for which you generated the report, in Coordinated Universal Time (UTC). |

| GeneratedTimeUTC | The date and time when you generated the report, in Coordinated Universal Time (UTC). |

| Location | The list of the countries/regions where the client requests originated. The value is **All** by default. Not applicable to the *Security* report. |

| Protocol | The protocol of the request, which is either HTTP or HTTPS. Not applicable to *Top URL*, *Traffic by user agent*, and *Security* reports. |

| Aggregation | The granularity of data aggregation in each row, every 5 minutes, every hour, and every day. Not applicable to *Traffic by domain*, *Top URL*, *Traffic by user agent* reports, and *Security* reports. |

Each report also includes its own variables. Select a report to view the variables that the report includes.

# [Traffic by domain](#tab/traffic-by-domain)

The *Traffic by domain* report includes these fields:

* Domain

* Total Request

* Cache Hit Ratio

* 3XX Requests

* 4XX Requests

* 5XX Requests

* ByteTransferredFromEdgeToClient

# [Traffic by location](#tab/traffic-by-location)

The *Traffic by location* report includes the below fields. The location split is done based on client location.

* Location

* TotalRequests

* Request%

* BytesTransferredFromEdgeToClient

# [Usage](#tab/usage)

There are three reports in the usage report's CSV file: one for HTTP protocol, one for HTTPS protocol, and one for HTTP status codes.

The *Usage* report's HTTP and HTTPS data sets include these fields:

* Time

* Protocol

* DataTransferred(bytes)

* TotalRequest

* bpsFromEdgeToClient

* 2XXRequest

* 3XXRequest

* 4XXRequest

* 5XXRequest

The *Usage* report's HTTP status codes data set include these fields:

* Time

* DataTransferred(bytes)

* TotalRequest

* bpsFromEdgeToClient

* 2XXRequest

* 3XXRequest

* 4XXRequest

* 5XXRequest

# [Caching](#tab/caching)

The *Caching* report includes these fields:

* Time

* CacheHitRatio

* HitRequests

* MissRequests

# [Top URL](#tab/top-url)

The *Top URL* report includes these fields:

* URL

* TotalRequests

* Request%

* DataTransferred(bytes)

* DataTransferred%

# [Top user agent](#tab/topuser-agent)

The *Top user agent* report includes these fields:

* UserAgent

* TotalRequests

* Request%

* DataTransferred(bytes)

* DataTransferred%

# [Security](#tab/security)

The *Security* report includes seven tables:

* Time

* Rule ID

* Countries/regions

* IP address

* URL

* Hostname

* User agent

All of the tables in the *Security* report include the following fields:

* BlockedRequests

* AllowedRequests

* LoggedRequests

* RedirectedRequests

* OWASPRuleRequests

* CustomRuleRequests

* BotRequests

---

## Key metrics included in all reports

The following metrics are used within the reports.

| Metric | Description |

|---------|---------|

| Data Transferred | Shows data transferred from Azure Front Door edge PoPs to client for the selected time frame, client locations, domains, and protocols. |

| Peak Bandwidth | Peak bandwidth usage in bits per seconds from Azure Front Door edge PoPs to clients for the selected time frame, client locations, domains, and protocols. |

| Total Requests | The number of requests that Azure Front Door edge PoPs responded to clients for the selected time frame, client locations, domains, and protocols. |

| Cache Hit Ratio | The percentage of all the cacheable requests for which Azure Front Door served the contents from its edge caches for the selected time frame, client locations, domains, and protocols. |

| 5XX Error Rate | The percentage of requests for which the HTTP status code to client was a 5XX for the selected time frame, client locations, domains, and protocols. |

| Total Latency | Average latency of all the requests for the selected time frame, client locations, domains, and protocols. The latency for each request is measured as the total time of when the client request gets received by Azure Front Door until the last response byte sent from Azure Front Door to client. |

## Traffic by domain report

The **traffic by domain** report provides a grid view of all the domains under this Azure Front Door profile.

In this report, you can view:

* Request counts

* Data transferred out from Azure Front Door to client

* Requests with status code (3XX, 4XX, and 5XX) of each domain

Domains include endpoint domains and custom domains.

You can go to other tabs to investigate further or view access log for more information if you find the metrics below your expectation.

## Usage report

The **usage report** shows the trends of traffic and response status code by various dimensions.

The dimensions included in the usage report are:

* Data transferred from edge to client and from origin to edge, in a line chart.

* Data transferred from edge to client by protocol, in a line chart.

* Number of requests from edge to clients, in a line chart.

* Number of requests from edge to clients by protocol (HTTP and HTTPS), in a line chart.

* Bandwidth from edge to client, in a line chart.

* Total latency, which measures the total time from the client request received by Azure Front Door until the last response byte sent from Azure Front Door to the client, in a line chart.

* Number of requests from edge to clients by HTTP status code, in a line chart. Every request generates an HTTP status code. HTTP status code appears as the HTTPStatusCode in the raw access log. The status code describes how the Azure Front Door edge PoP handled the request. For example, a 2XX status code indicates that the request was successfully served to a client. While a 4XX status code indicates that an error occurred.

* Number of requests from the edge to clients by HTTP status code, in a line chart. The percentage of requests by HTTP status code is shown in a grid.

## Traffic by location report

The **traffic by location** report displays:

* The top 50 countries/regions of visitors that access your assets the most.

* A breakdown of metrics by countries/regions and gives you an overall view of countries/regions where the most traffic gets generated.

* The countries/regions that have higher cache hit ratios, and higher 4XX/5XX error code rates.

The following items are included in the reports:

* A world map view of the top 50 countries/regions by data transferred out or requests of your choice.

* Two line charts showing a trend view of the top five countries/regions by data transferred out and requests of your choice.

* A grid of the top countries or regions with corresponding data transferred out from Azure Front Door to clients, the percentage of data transferred out, the number of requests, the percentage of requests by the country or region, cache hit ratio, 4XX response code counts, and 5XX response code counts.

## Caching report

The **caching report** provides a chart view of cache hits and misses, and the cache hit ratio, based on requests. Understanding how Azure Front Door caches your content helps you to improve your application's performance because cache hits give you the fastest performance. You can optimize data delivery speeds by minimizing cache misses.

The caching report includes:

* Cache hit and miss count trend, in a line chart.

* Cache hit ratio, in a line chart.

Cache hits/misses describe the request number cache hits and cache misses for client requests.

* Hits: client requests that get served directly from Azure Front Door edge PoPs. Refers to those requests whose values for CacheStatus in the raw access logs are *HIT*, *PARTIAL_HIT*, or *REMOTE_HIT*.

* Miss: client requests that get served by Azure Front Door edge POPs fetching contents from origin. Refers to those requests whose values for the field CacheStatus in the raw access raw logs are *MISS*.

**Cache hit ratio** describes the percentage of cached requests that are served from edge directly. The formula of the cache hit ratio is: `(PARTIAL_HIT +REMOTE_HIT+HIT/ (HIT + MISS + PARTIAL_HIT + REMOTE_HIT)*100%`.

Requests that meet the following requirements are included in the calculation:

* The requested content was cached on an Azure Front Door PoP.

* Partial cached contents for [object chunking](../front-door-caching.md#delivery-of-large-files).

It excludes all of the following cases:

* Requests that are denied because of a Rule Set.

* Requests that contain matching Rules Set, which is set to disable the cache.

* Requests that get blocked by the Azure Front Door WAF.

* Requests when the origin response headers indicate that they shouldn't be cached. For example, requests with `Cache-Control: private`, `Cache-Control: no-cache`, or `Pragma: no-cache` headers prevent the response from being cached.

## Top URL report

The **top URL report** allow you to view the amount of traffic incurred through a particular endpoint or custom domain. You see data for the most requested 50 assets during any period in the past 90 days.

Popular URLs are displayed with the following values:

* URL, which refers to the full path of the requested asset in the format of `http(s)://contoso.com/index.html/images/example.jpg`. URL refers to the value of the RequestUri field in the raw access log.

* Request counts.

* Request counts as a percentage of the total requests served by Azure Front Door.

* Data transferred.

* Data transferred percentage.

* Cache hit ratio percentage.

* Requests with response codes of 4XX.

* Requests with response codes of 5XX.

User can sort URLs by request count, request count percentage, data transferred, and data transferred percentage. The system aggregates all metrics by hour, and they might vary based on the selected time frame.

> [!NOTE]

> Top URLs might change over time. To get an accurate list of the top 50 URLs, Azure Front Door counts all your URL requests by hour and keep the running total over the course of a day. The URLs at the bottom of the 50 URLs may rise onto or drop off the list over the day, so the total number of these URLs are approximations.

>

> The top 50 URLs may rise and fall in the list, but they rarely disappear from the list, so the numbers for top URLs are usually reliable. When a URL drops off the list and rise up again over a day, the number of request during the period when they are missing from the list is estimated based on the request number of the URL that appear in that period.

## Top referrer report

The **top referrer** report shows you the top 50 referrers to a particular Azure Front Door endpoint or custom domain. You can view data for any period in the past 90 days. A referrer indicates the URL from which a request was generated. Referrer might come from a search engine or other websites. If a user types a URL (for example, `https://contoso.com/index.html`) directly into the address bar of a browser, the referrer for the requested is *Empty*.

The top referrer report includes the following values.

* Referrer, which is the value of the Referrer field in the raw access log.

* Request counts.

* Request count as a percentage of total requests served by Azure Front Door in the selected time period.

* Data transferred.

* Data transferred percentage.

* Cache hit ratio percentage.

* Requests with response code as 4XX.

* Requests with response code as 5XX.

You can sort by request count, request %, data transferred and data transferred %. The system aggregates all metrics by hour, and they might vary based on the selected time frame.

## Top user agent report

The **top user agent** report shows graphical and statistics views of the top 50 user agents that were used to request content. The following list shows example user agents:

* Mozilla/5.0 (Windows NT 10.0; WOW64)

* AppleWebKit/537.36 (KHTML, like Gecko)

* Chrome/86.0.4240.75

* Safari/537.36.

A grid displays the request counts, request %, data transferred and data transferred, cache Hit Ratio %, requests with response code as 4XX and requests with response code as 5XX. User Agent refers to the value of UserAgent in access logs.

> [!NOTE]

> Top user agents might change over time. To get an accurate list of the top 50 user agents, Azure Front Door counts all your user agent requests by hour and keep the running total over the course of a day. The user agents at the bottom of the 50 user agents may rise onto or drop off the list over the day, so the total number of these user agents are approximations.

>

> The top 50 user agents may rise and fall in the list, but they rarely disappear from the list, so the numbers for top user agents are usually reliable. When a user agent drops off the list and rise up again over a day, the number of request during the period when they are missing from the list is estimated based on the request number of the user agents that appear in that period.

## Security report

The **security report** provides graphical and statistics views of WAF activity.

| Dimensions | Description |

|---------|---------|

| Overview metrics - Matched WAF rules | Requests that match custom WAF rules, managed WAF rules and bot protection rules. |

| Overview metrics - Blocked Requests | The percentage of requests that gets blocked by WAF rules among all the requests that matched WAF rules. |

| Overview metrics - Matched Managed Rules | Requests that match managed WAF rules. |

| Overview metrics - Matched Custom Rule | Requests that match custom WAF rules. |

| Overview metrics - Matched Bot Rule | Requests that match bot protection rules. |

| WAF request trend by action | Four line-charts trend for requests by action. Actions are *Block*, *Log*, *Allow*, and *Redirect*. |

| Events by Rule Type | Doughnut chart of the WAF requests distribution by rule type. Rule types include bot protection rules, custom rules, and managed rules. |

| Events by Rule Group | Doughnut chart of the WAF requests distribution by rule group. |

| Requests by actions | A table of requests by actions, in descending order. |

| Requests by top Rule IDs | A table of requests by top 50 rule IDs, in descending order. |

| Requests by top  countries/regions |  A table of requests by top 50 countries/regions, in descending order. |

| Requests by top client IPs |  A table of requests by top 50 IPs, in descending order. |

| Requests by top Request URL |  A table of requests by top 50 URLs, in descending order. |

| Request by top Hostnames | A table of requests by top 50 hostname, in descending order. |

| Requests by top user agents | A table of requests by top 50 user agents, in descending order. |

## Next steps

Learn about [Azure Front Door real time monitoring metrics](how-to-monitor-metrics.md).


# How To Logs

# Configure Azure Front Door logs

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Azure Front Door captures several types of logs. Logs can help you monitor your application, track requests, and debug your Front Door configuration. For more information about Azure Front Door's logs, see [Monitor metrics and logs in Azure Front Door](../front-door-diagnostics.md).

Access logs, health probe logs, and Web Application Firewall (WAF) logs aren't enabled by default. In this article, you learn how to enable diagnostic logs for your Azure Front Door profile.

## Configure logs

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal, search for **Front Door** and then select the relevant Azure Front Door profile.

1. Under **Monitoring**, select **Diagnostic settings** and then select **+ Add diagnostic setting**.

1. In **Diagnostic setting**, enter a name for **Diagnostic setting name**.

1. Under **Logs**, select **audit**, **allLogs**, or the individual log you want. Available logs are: **FrontDoor Access Log**, **FrontDoor Health Probe Log**, and **FrontDoor WebApplicationFirewall Log**.

1. Select the **Destination details**. The destination options are:

- **Send to Log Analytics**

- Azure Log Analytics in Azure Monitor is best used for general real-time monitoring and analysis of Azure Front Door performance.

- Select the *Subscription* and *Log Analytics workspace*.

- **Archive to a storage account**

- Storage accounts are best used for scenarios when logs are stored for a longer duration and are reviewed when needed.

- Select the *Subscription* and *Storage Account*.

- **Stream to an event hub**

- Event hubs are a great option for integrating with other security information and event management (SIEM) tools or external data stores, such as Splunk, Datadog, or Sumo.

- Select the *Subscription*, *Event hub namespace*, *Event hub name (optional)*, and *Event hub policy name*.

- **Send to partner solution**

- Partner solutions are fully integrated solutions with Azure. For more information, see [Destinations in Azure Monitor diagnostic settings](/azure/azure-monitor/platform/diagnostic-settings#destinations) and [Azure Monitor partner solutions](/azure/partner-solutions/partners#observability).

- Select the *Subscription* and *Destination*.

> [!TIP]

> Microsoft recommends using Log Analytics for real-time monitoring and analysis of Azure Front Door performance.

1. Select **Save** to begin logging.

## View your activity logs

To view activity logs:

1. Select your Azure Front Door profile.

1. Select **Activity log**.

1. Choose a filtering scope.

## Related content

- [Monitor Azure Front Door](../monitor-front-door.md)

- [Azure Front Door reports](how-to-reports.md)

- [Azure Front Door monitoring data reference](../monitor-front-door-reference.md)


# Front Door Caching

# Caching with Azure Front Door

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

Azure Front Door is a modern content delivery network (CDN), with dynamic site acceleration and load balancing capabilities. When caching is configured on your route, the edge site that receives each request checks its cache for a valid response. Caching helps to reduce the amount of traffic sent to your origin server. If no cached response is available, the request is forwarded to the origin.

Each Front Door edge site manages its own cache, and requests might get served by different edge sites. As a result, you might still see some traffic reach your origin, even if you served cached responses.

Caching can significantly decrease latency and reduce the load on origin servers. However, not all types of traffic can benefit from caching. Static assets such as images, CSS, and JavaScript files are ideal for caching. While dynamic assets, such as authenticated API endpoints, shouldn't be cached to prevent the leakage of personal information. It's recommended to have separate routes for static and dynamic assets, with caching disabled for the latter.

> [!WARNING]

> Before you enable caching, thoroughly review the public documentation, and test all possible scenarios before enabling caching. As noted previously, with misconfiguration you can inadvertently cache user specific data that can be shared by multiple users resulting privacy incidents.

## Request methods

Only requests that use the `GET` request method are cacheable. All other request methods are always proxied through the network.

## Delivery of large files

Azure Front Door delivers large files without a cap on file size. If caching is enabled, Front Door uses a technique called *object chunking*. When a large file is requested, Front Door retrieves smaller pieces of the file from the origin. After Front Door receives a full file request or byte-range file request, the Front Door environment requests the file from the origin in chunks of 8 MB.

After the chunk arrives at the Azure Front Door environment, it's cached and immediately served to the user. Front Door then prefetches the next chunk in parallel. This prefetch ensures that the content stays one chunk ahead of the user, which reduces latency. This process continues until the entire file gets downloaded (if requested) or the client closes the connection. For more information on the byte-range request, see [RFC 7233](https://www.rfc-editor.org/info/rfc7233).

Front Door caches any chunks as they're received so the entire file doesn't need to be cached on the Front Door cache. Subsequent requests for the file or byte ranges are served from the cache. If the chunks aren't all cached, prefetching is used to request chunks from the origin.

This optimization relies on the origin's ability to support byte-range requests. If the origin doesn't support byte-range requests, or if it doesn't handle range requests correctly, then this optimization isn't effective.

When your origin responds to a request with a `Range` header, it must respond in one of the following ways:

- **Return a ranged response.** The response must use HTTP status code 206. Also, the `Content-Range` response header must be present, and must match the actual length of the content that your origin returns. If your origin doesn't send the correct response headers with valid values, Azure Front Door doesn't cache the response, and you might see inconsistent behavior.

> [!TIP]

> If your origin compresses the response, ensure that the `Content-Range` header value matches the actual length of the compressed response.

- **Return a non-ranged response.** If your origin can't handle range requests, it can ignore the `Range` header and return a nonranged response. Ensure that the origin returns a response status code other than 206. For example, the origin might return a 200 OK response.

If the origin uses Chunked Transfer Encoding (CTE) to send data to the Azure Front Door POP, response sizes greater than 8 MB aren't supported.

## File compression

See [improve performance by compressing files](standard-premium/how-to-compression.md) in Azure Front Door.

Azure Front Door (classic) can dynamically compress content on the edge, resulting in a smaller and faster response time to your clients. In order for a file to be eligible for compression, caching must be enabled and the file must be of a MIME type to be eligible for compression. Currently, Front Door (classic) doesn't allow this list to be changed. The current list is:

- "application/eot"

- "application/font"

- "application/font-sfnt"

- "application/javascript"

- "application/json"

- "application/opentype"

- "application/otf"

- "application/pkcs7-mime"

- "application/truetype"

- "application/ttf",

- "application/vnd.ms-fontobject"

- "application/xhtml+xml"

- "application/xml"

- "application/xml+rss"

- "application/x-font-opentype"

- "application/x-font-truetype"

- "application/x-font-ttf"

- "application/x-httpd-cgi"

- "application/x-mpegurl"

- "application/x-opentype"

- "application/x-otf"

- "application/x-perl"

- "application/x-ttf"

- "application/x-javascript"

- "font/eot"

- "font/ttf"

- "font/otf"

- "font/opentype"

- "image/svg+xml"

- "text/css"

- "text/csv"

- "text/html"

- "text/javascript"

- "text/js", "text/plain"

- "text/richtext"

- "text/tab-separated-values"

- "text/xml"

- "text/x-script"

- "text/x-component"

- "text/x-java-source"

Additionally, the file must also be between 1 KB and 8 MB in size, inclusive.

These profiles support the following compression encodings:

- [Gzip (GNU zip)](https://en.wikipedia.org/wiki/Gzip)

- [Brotli](https://en.wikipedia.org/wiki/Brotli)

If a request supports gzip and Brotli compression, Brotli compression takes precedence.

When a request for an asset specifies compression and the request results in a cache miss, Azure Front Door (classic) does compression of the asset directly on the POP server. Afterward, the compressed file is served from the cache. The resulting item is returned with a `Transfer-Encoding: chunked` response header.

If the origin uses Chunked Transfer Encoding (CTE) to send data to the Azure Front Door POP, then compression isn't supported.

> [!NOTE]

> Range requests may be compressed into different sizes. Azure Front Door requires the content-length values to be the same for any GET HTTP request. If clients send byte range requests with the `Accept-Encoding` header that leads to the Origin responding with different content lengths, then Azure Front Door will return a 503 error. You can either disable compression on the origin, or create a Rules Engine rule to remove the `Accept-Encoding` header from the request for byte range requests.

## Query string behavior

With Azure Front Door, you can control how files are cached for a web request that contains a query string.

In a web request with a query string, the query string is that portion of the request that occurs after a question mark (`?`). A query string can contain one or more key-value pairs, in which the field name and its value are separated by an equals sign (`=`). Each key-value pair is separated by an ampersand (&).

For example, the URL `http://www.contoso.com/content.mov?field1=value1&field2=value2` contains two query strings:

- `field1`, with a value of `value1`.

- `field2`, with a value of `value2`.

If there's more than one key-value pair in a query string of a request then their order doesn't matter.

When you configure caching, you specify how the cache should handle query strings. The following behaviors are supported:

* **Ignore Query String**: In this mode, Azure Front Door passes the query strings from the client to the origin on the first request and caches the asset. Future requests for the asset that are served from the Front Door environment ignore the query strings until the cached asset expires.

* **Use Query String**: In this mode, each request with a unique URL, including the query string, is treated as a unique asset with its own cache. For example, the response from the origin for a request for `www.example.ashx?q=test1` is cached at the Front Door environment and returned for ensuing caches with the same query string. A request for `www.example.ashx?q=test2` is cached as a separate asset with its own time-to-live setting.

The order of the query string parameters doesn't matter. For example, if the Azure Front Door environment includes a cached response for the URL `www.example.ashx?q=test1&r=test2`, then a request for `www.example.ashx?r=test2&q=test1` is also served from the cache.

* **Ignore Specified Query Strings** and **Include Specified Query Strings**: In this mode, you can configure Azure Front Door to include or exclude specified parameters when the cache key is generated.

For example, suppose that the default cache key is `/foo/image/asset.html`, and a request is made to the URL `https://contoso.com/foo/image/asset.html?language=EN&userid=100&sessionid=200`. If there's a rules engine rule to exclude the `userid` query string parameter, then the query string cache key would be `/foo/image/asset.html?language=EN&sessionid=200`.

Configure the query string behavior on the Front Door route.

## Cache purge

To learn how to configure cache purge, see [Purge cache in Azure Front Door](cache-purge.md).

Azure Front Door caches assets until the asset's time-to-live (TTL) expires. Whenever a client requests an asset with expired TTL, the Front Door environment retrieves a new updated copy of the asset to serve the request and then stores the refreshed cache.

The best practice to make sure your users always obtain the latest copy of your assets is to version your assets for each update and publish them as new URLs. Front Door will immediately retrieve the new assets for the next client requests. Sometimes you may wish to purge cached content from all edge nodes and force them all to retrieve new updated assets. The reason could be because of updates to your web application, or to quickly update assets that contain incorrect information.

Select the assets you want to purge from the edge nodes. To clear all assets, select **Purge all**. Otherwise, in **Path**, enter the path of each asset you want to purge.

These formats are supported in the lists of paths to purge:

- **Single path purge**: Purge individual assets by specifying the full path of the asset (without the protocol and domain), with the file extension, for example, /pictures/strasbourg.png;

- **Wildcard purge**: Asterisk (\*) may be used as a wildcard. Purge all folders, subfolders, and files under an endpoint with /\* in the path or purge all subfolders and files under a specific folder by specifying the folder followed by /\*, for example, /pictures/\*.

- **Root domain purge**: Purge the root of the endpoint with "/" in the path.

> [!NOTE]

> **Purging wildcard domains**: Specifying cached paths for purging as discussed in this section doesn't apply to any wildcard domains that are associated with the Front Door. Currently, we don't support directly purging wildcard domains. You can purge paths from specific subdomains by specifying that specific subdomain and the purge path. For example, if my Front Door has `*.contoso.com`, I can purge assets of my subdomain `foo.contoso.com` by typing `foo.contoso.com/path/*`. Currently, specifying host names in the purge content path is limited to subdomains of wildcard domains, if applicable.

Cache purges on the Front Door are case-insensitive. Additionally, they're query string agnostic, which means that purging a URL purges all query string variations of it.

## Cache expiration

The following order of headers is used to determine how long an item gets stored in our cache:

1. `Cache-Control: s-maxage=<seconds>`

1. `Cache-Control: max-age=<seconds>`

1. `Expires: <http-date>`

Some `Cache-Control` response header values indicate that the response isn't cacheable. These values include `private`, `no-cache`, and `no-store`. Front Door honors these header values and doesn't cache the responses, even if you override the caching behavior by using the Rules Engine.

If the `Cache-Control` header isn't present on the response from the origin, by default Front Door randomly determines a cache duration between one and three days.

> [!NOTE]

> Cache expiration can't be greater than **366 days**.

You may see `REVALIDATED_HIT` in the `Cache-Control` response header. This indicates that the cached content in Azure Front Door was revalidated with the origin server before being served to the client. This can happen when the cached content has expired, but the origin server indicates that the content hasn't changed. In this case, the cached content is served to the client, and the cache expiration is reset.

## Request headers

The following request headers don't get forwarded to the origin when caching is enabled:

- `Content-Length`

- `Transfer-Encoding`

- `Accept`

- `Accept-Charset`

- `Accept-Language`

- `Vary`

> [!NOTE]

> Requests that include authorization header won't be cached, unless the response contains a Cache-Control directive that allows caching. The following Cache-Control directives have such an effect: must-revalidate, public, and s-maxage.

## Response headers

If the origin response is cacheable, then the `Set-Cookie` header is removed before the response is sent to the client. If an origin response isn't cacheable, Front Door doesn't strip the header. For example, if the origin response includes a `Cache-Control` header with a `max-age` value indicates to Front Door that the response is cacheable, and the `Set-Cookie` header is stripped.

In addition, Front Door attaches the `X-Cache` header to all responses. The `X-Cache` response header includes one of the following values:

- `TCP_HIT` or `TCP_REMOTE_HIT`: The first 8-MB chunk of the response is a cache hit, and the content is served from the Front Door cache.

- `TCP_MISS`: The first 8-MB chunk of the response is a cache miss, and the content is fetched from the origin.

- `PRIVATE_NOSTORE`: Request can't be cached because the *Cache-Control* response header is set to either *private* or *no-store*.

- `CONFIG_NOCACHE`: Request is configured to not cache in the Front Door profile.

> [!NOTE]

> Azure Front Door strips the `Content-Type` header for empty files when caching is enabled. To continue sending this header to clients, use Azure Front Door rules engine (Action - Modify response header, Operator - Overwrite, Header name - Content-Type) to manually override it for such files. You also can disable caching for empty files, but this approach is less recommended as it increases the load on your origin and may impact performance.

## Logs and reports

The [access log](front-door-diagnostics.md#access-log) includes the cache status for each request. Also, [reports](standard-premium/how-to-reports.md#caching-report) include information about how Azure Front Door's cache is used in your application.

The [access log](front-door-diagnostics.md#access-log) includes the cache status for each request.

## Cache behavior and duration

Cache behavior and duration can be configured in Rules Engine. Rules Engine caching configuration always overrides the route configuration.

* **When caching is disabled**, Azure Front Door doesn’t cache the response contents, irrespective of the origin response directives.

* **When caching is enabled**, the cache behavior is different depending on the cache behavior value applied by the Rules Engine:

* **Honor origin**: Azure Front Door always honors origin response header directive. If the origin directive is missing, Azure Front Door caches contents anywhere from one to three days.

* **Override always**: Azure Front Door always overrides with the cache duration, meaning that it caches the contents for the cache duration ignoring the values from origin response directives. This behavior only applies if the response is cacheable.

* **Override if origin missing**: If the origin doesn’t return caching TTL values, Azure Front Door uses the specified cache duration. This behavior only applies if the response is cacheable.

> [!NOTE]

> * Azure Front Door makes no guarantees about the amount of time that the content is stored in the cache. Cached content may be removed from the edge cache before the content expiration if the content isn't frequently used.

> * Front Door might be able to serve data from the cache even if the cached data has expired or if the origin is returning error responses. This behavior can help your site to remain partially available when your origins are offline.

> * Origins may specify not to cache specific responses using the Cache-Control header with a value of no-cache, private, or no-store. When used in an HTTP response from the origin server to the Azure Front Door POPs, Azure Front Door supports Cache-control directives and honors caching behaviors for Cache-Control directives in [RFC 7234 - Hypertext Transfer Protocol (HTTP/1.1): Caching (ietf.org)](https://www.rfc-editor.org/rfc/rfc7234#section-5.2.2.8).

Cache behavior and duration can be configured in both the Front Door designer routing rule and in Rules Engine. Rules Engine caching configuration always overrides the Front Door designer routing rule configuration.

* **When caching is disabled**, Azure Front Door (classic) doesn’t cache the response contents, irrespective of origin response directives.

* **When caching is enabled**, the cache behavior is different for different values of *Use cache default duration*.

* When *Use cache default duration* is set to **Yes**, Azure Front Door (classic) always honor origin response header directive. If the origin directive is missing, Front Door caches contents anywhere from one to three days.

* When *Use cache default duration* is set to **No**, Azure Front Door (classic) always override with the *cache duration* (required fields), meaning that it caches the contents for the cache duration ignoring the values from origin response directives.

> [!NOTE]

> * Azure Front Door (classic) makes no guarantees about the amount of time that the content is stored in the cache. Cached content may be removed from the edge cache before the content expiration if the content isn't frequently used.

> * Azure Front Door (classic) might be able to serve data from the cache even if the cached data has expired or the backend is returning error responses. This behavior can help your site to remain partially available when your backends are offline.

> * The *cache duration* set in the Front Door designer routing rule is the **minimum cache duration**. This override doesn't work if the cache control header from the origin has a greater TTL than the override value.

## Related content

- Learn how to [create an Azure Front Door (classic)](quickstart-create-front-door.md).

- Learn [how Azure Front Door (classic) works](front-door-routing-architecture.md).

- Learn more about [Rule set match conditions](standard-premium/concept-rule-set-match-conditions.md)

- Learn more about [Rule set actions](front-door-rules-engine-actions.md)


# How To Compression

# Improve performance by compressing files in Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

File compression is an effective method to improve file transfer speed and increase page-load performance. The server compresses the file to reduce its size before sending it. File compression can reduce bandwidth costs and provide a better experience for your users.

There are two ways to enable file compression:

- Enabling compression on your origin server. Azure Front Door passes along the compressed files and delivers them to clients that request them.

- Enabling compression directly on the Azure Front Door POP servers (*compression on the fly*). In this case, Azure Front Door compresses the files and sends them to the end users.

> [!NOTE]

> Range requests may be compressed into different sizes. Azure Front Door requires the `Content-Length` response header values to be the same for any GET HTTP request. If clients send byte range requests with the `Accept-Encoding` header that leads to the origin responding with different content lengths, then Azure Front Door returns a 503 error. You can either disable compression on the origin/Azure Front Door, or create a Rules Engine rule to remove the `Accept-Encoding` header from byte range requests.

> [!IMPORTANT]

> Azure Front Door configuration changes take up to 10 mins to propagate throughout the network. If you're setting up compression for the first time for your CDN endpoint, consider waiting 1-2 hours before you troubleshoot to ensure the compression settings have propagated to all the POPs.

## Enabling compression

> [!NOTE]

> In Azure Front Door, compression is part of **Enable Caching** in Route. Only when you **Enable Caching**, can you take advantage of compression in Azure Front Door.

You can enable compression in the following ways:

* During quick create - When you enable caching, you can enable compression.

* During custom, create - Enable caching and compression when you're adding a route.

* In Front Door manager.

* On the Optimization page.

### Enable compression in Front Door manager

1. From the Azure Front Door Standard/Premium profile page, go to **Front Door manager** and select the endpoint you want to enable compression.

1. Within the endpoint, select the **route** you want to enable compression on.

1. Ensure **Enable caching** is checked, then select the checkbox for **Enable compression**.

1. Select **Update** to save the configuration.

### Enable compression in Optimizations

1. From the Azure Front Door Standard/Premium profile page, go to **Optimizations** under Settings. Expand the endpoint to see the list of routes.

1. Select the three dots next to the **route** that has compression *Disabled*. Then select **Configure route**.

1. Ensure **Enable caching** is checked, then select the checkbox for **Enable compression**.

1. Select **Update**.

## Modify compression content type

You can modify the default list of MIME types on Optimizations page.

1. From the Azure Front Door Standard/Premium profile page, go to **Optimizations** under Settings. Then select the **route** that has compression *Enabled*.

1. Select the three dots next to the **route** that has compression *Enabled*. Then select **View Compressed file types**.

1. Delete default formats or select **Add** to add new content types.

1. Select **Save** to update the compression configuration.

## Disabling compression

You can disable compression in the following ways:

* Disable compression in Azure Front Door manager route.

* Disable compression in Optimizations page.

### Disable compression in Azure Front Door manager

1. From the Azure Front Door Standard/Premium profile page, go to **Front Door manager** under Settings.

1. Select the **route** you want to disable compression on. Uncheck the **Enable compression** box.

1. Select **Update** to save the configuration.

### Disable compression in Optimizations

1. From the Azure Front Door Standard/Premium profile page, go to **Optimizations** under Settings. Then select the **route** that has compression *Enabled*.

1. Select the three dots next to the **route** that has compression *Enabled*, then select *Configure route*.

1. Uncheck the **Enable compression** box.

1. Select **Update** to save the configuration.

## Compression rules

In Azure Front Door, only eligible files are compressed. To be eligible for compression, a file must:

* Be of a MIME type

* Be larger than 1 KB

* Be smaller than 8 MB

These profiles support the following compression encodings:

* gzip (GNU zip)

* brotli

If the request supports more than one compression type, brotli compression takes precedence.

When a request for an asset specifies gzip compression and the request results in a cache miss, Azure Front Door does gzip compression of the asset directly on the POP server. Afterward, the compressed file is served  from the cache.

If the origin uses Chunked Transfer Encoding (CTE) to send data to the Azure Front Door POP, then compression isn't supported.

## Next steps

- Learn how to configure your first [Rules Set](how-to-configure-rule-set.md)

- Learn more about [Rule Set Match Conditions](concept-rule-set-match-conditions.md)

- Learn more about [Azure Front Door Rule Set](../front-door-rules-engine.md)


# Front Door Cdn Comparison

# Comparison between Azure Front Door and Azure Content Delivery Network

Azure Front Door and Azure Content Delivery Network are Azure services that offer global content delivery with intelligent routing and caching capabilities at the application layer.

Both services can help you optimize and accelerate your applications by providing a globally distributed network of points of presence (PoPs) close to your users. Both services also offer features to help you secure your applications from malicious attacks and to help you monitor your applications' health and performance.

## Important information about service tiers

Here's a timeline for changes to the service tiers and actions that you need to take:

- As of August 15, 2025, Azure Front Door (classic) and Azure CDN from Microsoft (classic) no longer support new domain onboarding or profile creation. To create new domains or profiles, migrate to [Azure Front Door Standard or Premium](/azure/frontdoor/tier-migration). [Learn more](https://azure.microsoft.com/updates?id=498522).

- As of August 15, 2025, Azure Front Door (classic) and Azure CDN from Microsoft (classic) [no longer support managed certificates](/azure/security/fundamentals/managed-tls-changes). To avoid service disruption, you need to either switch to bring your own certificate (BYOC) or migrate to [Azure Front Door Standard or Premium](/azure/frontdoor/tier-migration) by August 15, 2025. Existing managed certificates that were automatically renewed before August 15, 2025, remain valid until April 14, 2026. [Learn more](https://azure.microsoft.com/updates?id=498522).

- Azure Front Door (classic) is retiring on March 31, 2027. To avoid service disruption, ⁠[migrate to Azure Front Door Standard or Premium](/azure/frontdoor/tier-migration). ⁠[Learn more](https://azure.microsoft.com/updates?id=azure-front-door-classic-will-be-retired-on-31-march-2027).

- Azure CDN Standard from Microsoft (classic) is retiring on September 30, 2027. To avoid service disruption, ⁠[migrate to Azure Front Door Standard or Premium](/azure/cdn/migrate-tier). ⁠[Learn more](https://azure.microsoft.com/updates?id=Azure-CDN-Standard-from-Microsoft-classic-will-be-retired-on-30-September-2027).

To switch between tiers:

- From Azure Front Door (classic) to the Standard or Premium tier: use the [migration capability](migrate-tier.md).

- From Azure CDN Standard from Microsoft (classic) to the Azure Front Door Standard or Premium tier: use the [migration capability](../cdn/migrate-tier.md).

- From Azure Front Door Standard to Premium: use the [upgrade capability](tier-upgrade.md).

- From Azure Front Door Premium to Standard: No seamless downgrade tool exists. You can re-create the profile instead.

## Service comparison

The following table provides a comparison between the Azure Front Door and Azure Content Delivery Network services.

| Features and optimizations | Front Door Standard | Front Door Premium | Front Door (classic) | CDN Standard from Microsoft (classic) |

| --- | --- | --- | --- | --- |

| **Delivery and acceleration** | | | | |

| Static file delivery | &check; | &check; | &check; | &check; |

| Dynamic site delivery | &check; | &check; | &check; | |

| WebSockets | &check; | &check; | | |

| **Domains and certificates** | | | | |

| Custom domains | &check; | &check; | &check; | &check; |

| Prevalidated domain integration with Azure platform as a service | &check; | &check; | | |

| HTTPS support | &check; | &check; | &check; | &check; |

| Custom domain HTTPS | &check; | &check; | &check; | &check; |

| Bring your own certificate | &check; | &check; | &check; | &check; |

| Supported TLS versions | TLS 1.3, TLS 1.2 | TLS 1.3, TLS 1.2 | TLS 1.3, TLS 1.2 | TLS 1.3, TLS 1.2 |

| **Caching** | | | | |

| Query string caching | &check; | &check; | &check; | &check; |

| Cache management (purge, rules, and compression) | &check; | &check; | &check; | &check; |

| Cache behavior settings | &check; (using standard rules engine) | &check; (using standard rules engine) | &check; (using standard rules engine) | &check; (using standard rules engine) |

| **Routing** | | | | |

| Origin load balancing | &check; | &check; | &check; | &check; |

| Path-based routing | &check; | &check; | &check; | &check; |

| Rules engine | &check; | &check; | &check; | &check; |

| Server variable | &check; | &check; | | |

| Regular expression in rules engine | &check; | &check; | | |

| URL redirect/rewrite | &check; | &check; | &check; | &check; |

| IPv4/IPv6 dual stack | &check; | &check; | &check; | &check; |

| HTTP/2 support | &check; | &check; | &check; | &check; |

| Routing preference unmetered | Not required, because data transfer from the Azure origin to Azure Front Door is free and the path is directly connected | Not required, because data transfer from the Azure origin to Azure Front Door is free and the path is directly connected | Not required, because data transfer from the Azure origin to Azure Front Door is free and the path is directly connected | Not required, because data transfer from the Azure origin to Content Delivery Network is free and the path is directly connected |

| Origin port | All TCP ports | All TCP ports | All TCP ports | All TCP ports |

| Customizable, rules-based content delivery engine | &check; | &check; | &check; | &check; (using standard rules engine) |

| Mobile device rules | &check; | &check; | &check; | &check; (using standard rules engine) |

| **Security** | | | | |

| Custom web application firewall (WAF) rules | &check; | &check; | &check; | |

| Microsoft-managed rule set | | &check; | &check; (only default rule set 1.1 or earlier) | |

| Bot protection | | &check; | &check; (only bot manager rule set 1.0) | |

| Private Link connection to origin | | &check; | | |

| Geo-filtering | &check; | &check; | &check; | &check; |

| DDoS protection | &check; | &check; | &check; | &check; |

| Domain fronting block | &check; | &check; | &check; | &check; |

| Managed identities for origin authentication | Preview | Preview | | |

| **Analytics and reporting** | | | | |

| Monitoring metrics | &check; (more metrics than classic) | &check; (more metrics than classic) | &check; | &check; |

| Advanced analytics/built-in reports | &check; | &check; (includes WAF report) | | |

| Raw logs: access logs and WAF logs | &check; | &check; | &check; | &check; |

| Health probe log | &check; | &check; | | |

| **Ease of use** | | | | |

| Integration with Azure services, such as Azure Storage and Web Apps | &check; | &check; | &check; | &check; |

| Management via REST API, .NET, D3.js, or PowerShell | &check; | &check; | &check; | &check; |

| Compression MIME types | Configurable | Configurable | Configurable | Configurable |

| Compression encodings | gzip, Brotli | gzip, Brotli | gzip, Brotli | gzip, Brotli |

| Azure Policy integration | &check; | &check; | &check; | |

| Azure Advisor integration | &check; | &check; | | &check; |

| Managed identities with Azure Key Vault | &check; | &check; | | |

| **Pricing** | [Azure Front Door pricing](https://azure.microsoft.com/pricing/details/frontdoor/) | [Azure Front Door pricing](https://azure.microsoft.com/pricing/details/frontdoor/) | [Azure Front Door pricing](https://azure.microsoft.com/pricing/details/frontdoor/) | [Content Delivery Network pricing](https://azure.microsoft.com/pricing/details/cdn/) |

| Simplified pricing | &check; | &check; | | &check; |

## Services on a retirement path

The following table lists services that are on a retirement path, frequently asked questions regarding retirement, and migration guidance.

| Details | Front Door (classic) | CDN Standard from Microsoft (classic) |

| --- | --- | --- |

| Retirement date | March 31, 2027 | September 30, 2027 |

| Cutoff date for creating new resources | March 31, 2025 | August 15, 2025 |

| Documentation | [Azure update](https://azure.microsoft.com/updates/azure-front-door-classic-will-be-retired-on-31-march-2027/), [FAQ](classic-retirement-faq.md) | [Azure update](https://azure.microsoft.com/updates/v2/Azure-CDN-Standard-from-Microsoft-classic-will-be-retired-on-30-September-2027), [FAQ](../cdn/classic-cdn-retirement-faq.md) |

| Migration | [Considerations](tier-migration.md), [step-by-step instructions](migrate-tier.md) | [Considerations](../cdn/tier-migration.md), [step-by-step instructions](../cdn/migrate-tier.md) |

As of August 15, 2025, Azure-managed certificates are no longer supported on Azure Front Door (classic) and CDN Standard from Microsoft (classic). Existing managed certificates remain valid until April 14, 2026. [Learn more](https://azure.microsoft.com/updates?id=498522).

## Related content

- [Create an Azure Front Door profile](create-front-door-portal.md)

- [Azure Front Door routing architecture](front-door-routing-architecture.md)

- [Best practices for Azure Front Door](best-practices.md)


# Best Practices

# Best practices for Azure Front Door

This article summarizes best practices for using Azure Front Door.

## General best practices

### Understand when to combine Traffic Manager and Azure Front Door

For most solutions, we recommend the use of *either* Azure Front Door *or* [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md), but not both. Traffic Manager is a DNS-based load balancer. It sends traffic directly to your origin's endpoints. In contrast, Azure Front Door terminates connections at points of presence (PoPs) near to the client and establishes separate long-lived connections to the origins. The products work differently and are intended for different use cases.

If you need content caching and delivery, TLS termination, advanced routing capabilities, or a web application firewall (WAF), consider using Azure Front Door. For simple global load balancing with direct connections from your client to your endpoints, consider using Traffic Manager. For more information about selecting a load balancing option, see [Load-balancing options](/azure/architecture/guide/technology-choices/load-balancing-overview).

As part of a [complex architecture that requires high availability](/azure/architecture/guide/networking/global-web-applications/mission-critical-content-delivery), you can put Traffic Manager in front of Azure Front Door. In the unlikely event that Azure Front Door is unavailable, Traffic Manager can then route traffic to an alternative destination, such as Azure Application Gateway or a partner content delivery network (CDN).

> [!IMPORTANT]

> Don't put Traffic Manager behind Azure Front Door. Traffic Manager should always be in front of Azure Front Door.

### Restrict traffic to your origins

The features of Azure Front Door work best when traffic flows only through Azure Front Door. You should configure your origin to block traffic that isn't sent through Azure Front Door. For more information, see [Secure traffic to Azure Front Door origins](origin-security.md).

### Use the latest API version and SDK version

When you work with Azure Front Door by using APIs, Azure Resource Manager templates, Bicep, or Azure SDKs, it's important to use the latest available API or SDK version. API and SDK updates occur when new functionality is available, and they contain important security patches and bug fixes.

### Configure logs

Azure Front Door tracks extensive performance data for every request. When you enable caching, your origin servers might not receive every request. It's important that you use the Azure Front Door logs to understand how your solution is running and responding to your clients. For more information about the metrics and logs that Azure Front Door records, see [Monitor metrics and logs in Azure Front Door](front-door-diagnostics.md) and [WAF logs](../web-application-firewall/afds/waf-front-door-monitor.md#waf-logs).

To configure logging for your own application, see [Configure Azure Front Door logs](./standard-premium/how-to-logs.md).

## TLS best practices

### Use end-to-end TLS

Azure Front Door terminates TCP and TLS connections from clients. It then establishes new connections from each PoP to the origin. It's a good practice to secure each of these connections with TLS, even for origins that are hosted in Azure. This approach keeps your data encrypted during transit.

For more information, see [End-to-end TLS with Azure Front Door](end-to-end-tls.md).

### Use HTTP-to-HTTPS redirection

It's a good practice for clients to use HTTPS to connect to your service. However, sometimes you need to accept HTTP requests to allow for older clients or clients that might not follow the best practice.

You can configure Azure Front Door to automatically redirect HTTP requests to use the HTTPS protocol. You should enable the **Redirect all traffic to use HTTPS** setting on your route.

### Use managed TLS certificates

When Azure Front Door manages your TLS certificates, it reduces your operational costs and helps you avoid costly outages caused by forgetting to renew a certificate. Azure Front Door automatically issues and rotates the managed TLS certificates.

For more information, see [Configure HTTPS on an Azure Front Door custom domain using the Azure portal](standard-premium/how-to-configure-https-custom-domain.md).

### Use the latest version for customer-managed certificates

If you decide to use your own TLS certificates, consider setting the Azure Key Vault certificate version to **Latest**. By using **Latest**, you avoid having to reconfigure Azure Front Door to use new versions of your certificate and waiting for the certificate to be deployed throughout Azure Front Door environments.

For more information, see [Select the certificate for Azure Front Door to deploy](standard-premium/how-to-configure-https-custom-domain.md#select-the-certificate-for-azure-front-door-to-deploy).

## Domain best practices

### Adopt custom domains

Adopt custom domains for your Azure Front Door endpoints to ensure better availability and flexibility while managing your domains and traffic. Don't hardcode Azure Front Door-provided domains (like `*.azurefd.z01.net`) in your clients, codebases, or firewall. Use custom domains for such scenarios.

### Use the same domain name on Azure Front Door and your origin

Azure Front Door can rewrite the `Host` header of incoming requests. This feature can be helpful when you manage a set of customer-facing custom domain names that route to a single origin. This feature can also help when you want to avoid configuring custom domain names in Azure Front Door and at your origin.

However, when you rewrite the `Host` header, request cookies and URL redirections might break. In particular, when you use platforms like Azure App Service, features like [session affinity](../app-service/configure-common.md#configure-general-settings) and [authentication and authorization](../app-service/overview-authentication-authorization.md) might not work correctly.

Before you rewrite the `Host` header of your requests, carefully consider whether your application will work correctly. For more information, see [Preserve the original HTTP host name between a reverse proxy and its back-end web application](/azure/architecture/best-practices/host-name-preservation).

## WAF best practices

For internet-facing applications, we recommend that you enable the Azure Front Door WAF and configure it to use managed rules. Using a WAF and Microsoft-managed rules helps protect your application from a wide range of attacks. For more information, see [Web Application Firewall (WAF) on Azure Front Door](web-application-firewall.md).

The WAF for Azure Front Door has its own set of best practices for its configuration and use. For more information, see [Best practices for Web Application Firewall in Azure Front Door](../web-application-firewall/afds/waf-front-door-best-practices.md).

## Best practices for health probes

### Disable health probes when there's only one origin in an origin group

Health probes in Azure Front Door can detect situations where an origin is unavailable or unhealthy. You can configure Azure Front Door to send traffic to another origin in the origin group when a health probe detects a problem with an origin.

If you have only a single origin, Azure Front Door always routes traffic to that origin even if its health probe reports an unhealthy status. The status of the health probe doesn't do anything to change the behavior of Azure Front Door. In this scenario, health probes don't provide a benefit and you should disable them to reduce the traffic on your origin.

For more information, see [Health probes](health-probes.md).

### Select good endpoints

Consider the location where you want an Azure Front Door health probe to do its monitoring. It's usually a good idea to monitor a webpage or location that you specifically design for health monitoring. Your application logic can consider the status of all of the critical components required to serve production traffic, including application servers, databases, and caches. That way, if any component fails, Azure Front Door can route your traffic to another instance of your service.

For more information, see [Health Endpoint Monitoring pattern](/azure/architecture/patterns/health-endpoint-monitoring).

### Use HEAD health probes

Health probes can use either the `GET` or `HEAD` HTTP method. It's a good practice to use the `HEAD` method for health probes, because it reduces the amount of traffic load on your origins.

For more information, see [Supported HTTP methods for health probes](health-probes.md#supported-http-methods-for-health-probes).

## Next step

> [!div class="nextstepaction"]

> [Create an Azure Front Door profile](create-front-door-portal.md)


# Front Door Routing Architecture

# Routing architecture overview

Azure Front Door traffic routing takes place over multiple stages. First, traffic is routed from the client to the Front Door. Then, Front Door uses your configuration to determine the origin to send the traffic to. The Front Door web application firewall, routing rules, rules engine, and caching configuration can all affect the routing process.

The following diagram illustrates the routing architecture:

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

The following diagram illustrates the routing architecture:

The following sections describe these steps in detail.

## Name resolution by Azure Front Door's Traffic Manager profile returns PoP unicast IP

The user or client application initiates a connection to the origin behind Azure Front Door. The domain name resolves to the Front Door's Azure Traffic Manager endpoint. The Traffic Manager consumes health and availability signals from all the Front Door PoPs across the world. It determines the optimal PoP to serve the request and returns the unicast IP of that PoP.

## Connect to Azure Front Door PoP Unicast IP

Client makes a direct connection to the returned IP address of the Front Door PoP location.

## Match request to a Front Door profile

When Front Door receives an HTTP request, it uses the request's `Host` header to match the request to the correct customer's Front Door profile. If the request is using a [custom domain name](standard-premium/how-to-add-custom-domain.md), the domain name must be registered with Front Door to enable requests to get matched to your profile.

## Select and connect to the Front Door edge location

The user or client application initiates a connection to the Front Door. The connection terminates at an edge location closest to the end user. Front Door's edge location processes the request.

For more information about how requests are made to Front Door, see [Front Door traffic acceleration](front-door-traffic-acceleration.md).

## Match request to a front door

When Front Door receives an HTTP request, it uses the request's `Host` header to match the request to the correct customer's Front Door instance. If the request is using a [custom domain name](front-door-custom-domain.md), the domain name must be registered with Front Door to enable requests to get matched to your Front door.

The client and server perform a TLS handshake using the TLS certificate you configured for your custom domain name, or by using the Front Door certificate when the `Host` header ends with `*.azurefd.net`.

## Evaluate WAF rules

If your domain has Web Application Firewall enabled, WAF rules are evaluated.

If your frontend has Web Application Firewall enabled, WAF rules are evaluated.

If a rule gets violated, Front Door returns an error to the client and the request processing stops.

## Match a route

Front Door matches the request to a route. Learn more about the [route matching process](front-door-route-matching.md).

The route specifies the [origin group](standard-premium/concept-origin.md) that the request should be sent to.

## Match a routing rule

Front Door matches the request to a routing rule. Learn more about the [route matching process](front-door-route-matching.md).

The route specifies the [backend pool](front-door-backend-pool.md) that the request should be sent to.

## Evaluate rule sets

If you define [rule sets](front-door-rules-engine.md) for the route, they get process in the order configured. [Rule sets can override the origin group](front-door-rules-engine-actions.md#RouteConfigurationOverride) specified in a route. Rule sets can also trigger a redirection response to the request instead of forwarding it to an origin.

## Evaluate rules engines

If you define [rules engines](front-door-rules-engine.md) for the route, they get process in the order configured. [Rules engines can override the backend pool](front-door-rules-engine-actions.md#route-configuration-overrides) specified in a routing rule. Rules engines can also trigger a redirection response to the request instead of forwarding it to a backend.

## Return cached response

If the Front Door routing rule has [caching](front-door-caching.md) enabled, and the Front Door edge location's cache includes a valid response for the request, then Front Door returns the cached response.

If caching is disabled or no response is available, the request is forwarded to the origin.

If the Front Door routing rule has [caching](front-door-caching.md) enabled, and the Front Door edge location's cache includes a valid response for the request, then Front Door returns the cached response.

If caching is disabled or no response is available, the request is forwarded to the backend.

## Select origin

Front Door selects an origin to use within the origin group. Origin selection is based on several factors, including:

- Health of each origin, which Front Door monitors by using [health probes](front-door-health-probes.md).

- [Routing method](front-door-routing-methods.md) for your origin group.

- If you enable [session affinity](front-door-routing-methods.md#affinity)

## Forward the request to the origin

Finally, the request is forwarded to the origin.

## Select backend

Front Door selects a backend to use within the backend pool. Backend selection is based on several factors, including:

- Health of each backend, which Front Door monitors by using [health probes](front-door-health-probes.md).

- [Routing method](front-door-routing-methods.md) for your backend pool.

- If you have enable [session affinity](front-door-routing-methods.md#affinity)

## Forward the request to the backend

Finally, the request is forwarded to the backend.

## Next step

> [!div class="nextstepaction"]

> [Create an Azure Front Door profile](standard-premium/create-front-door-portal.md)

> [!div class="nextstepaction"]

> [Create an Azure Front Door (classic) profile](quickstart-create-front-door.md)


# Front Door Route Matching

# How requests get matched to a route configuration

A *route* in Azure Front Door defines how traffic is handled when an incoming request arrives at the Azure Front Door edge. The route settings establish an association between a domain and an origin group. By using advanced features such as *Pattern to Match* and *Rule sets*, you can have granular control over traffic to your backend resources.

> [!NOTE]

> When you use the [Front Door rule sets](front-door-rules-engine.md), you can configure a rule to [override the origin group](front-door-rules-engine-actions.md#RouteConfigurationOverride) for a request. The origin group set by the rule set overrides the routing process described in this article.

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

When a request arrives at the Azure Front Door (classic) edge, one of the first steps is to determine how to route the matching request to a backend resource and then take a defined action in the routing configuration. This document explains how Front Door determines which route configuration to use when processing a request.

## Structure of a Front Door route configuration

A Front Door routing rule consists of two major parts: the "left-hand side" and the "right-hand side". Front Door matches the incoming request to the left-hand side of the route, while the right-hand side defines how the request is processed.

### Incoming match (left-hand side)

The following properties determine whether the incoming request matches the routing rule (left-hand side):

* **HTTP Protocols** - HTTP or HTTPS

* **Domain** - For example: www\.foo.com, \*.bar.com

* **Paths** - For example: /\*, /users/\*, /file.gif

These properties are expanded internally so that every combination of Protocol/Domain/Path is a potential match set.

### Routing decision (right-hand side)

The decision on how to process the request depends on whether caching is enabled for the route. If a cached response isn't available, the request is forwarded to the appropriate origin.

## Route matching

This section explains how Front Door matches requests to routing rules. The basic principle is that Front Door always matches to the **most-specific request** by evaluating the "left-hand side" properties: protocol, domain, and path, in that order.

### Frontend host matching

Azure Front Door uses the following steps to match frontend hosts:

1. Check for routes with an exact match on the frontend host.

1. If it doesn't find an exact match, it rejects the request with a 404: Bad Request error.

The following tables illustrate three different routing rules with their frontend hosts and paths:

| Routing rule | Frontend hosts                            | Path            |

|--------------|-------------------------------------------|-----------------|

| A            | foo.contoso.com                           | /\*             |

| B            | foo.contoso.com                           | /users/\*       |

| C            | www.fabrikam.com, foo.adventure-works.com | /\*, /images/\* |

The following table shows the matching results for the routing rules in the previous table:

| Incoming frontend host   | Matched routing rules |

|--------------------------|-------------------------|

| foo.contoso.com          | A, B                    |

| www.fabrikam.com         | C                       |

| images.fabrikam.com      | Error 404: Bad Request  |

| foo.adventure-works.com  | C                       |

| contoso.com              | Error 404: Bad Request  |

| www.adventure-works.com  | Error 404: Bad Request  |

| www.northwindtraders.com | Error 404: Bad Request  |

### Path matching

After Azure Front Door determines the specific frontend host and filters possible routing rules, it selects the routing rules based on the request path. The service uses the following logic:

1. Check for routing rules with an exact match to the request path.

1. If it doesn't find an exact match, look for a routing rule with a wildcard path that matches.

1. If it doesn't find a matching path, reject the request with a 404: Bad Request error.

> [!NOTE]

> The wildcard character `*` is only valid for paths that don't have any other characters after it. Additionally, the wildcard character `*` must be preceded by a slash `/`. Paths without a wildcard are considered exact-match paths. A path that ends in a slash `/` is also an exact-match path. Ensure that your paths follow these rules to avoid errors.

> [!NOTE]

> * Paths without a wildcard are considered exact-match paths. A path ending with a `/` is also an exact match.

> * Path patterns are case insensitive. For example, `/FOO` and `/foo` are treated as duplicates and aren't allowed in the Patterns to match setting.

The following table lists routing rules with their frontend host and path combinations:

| Routing rule | Frontend host    | Path    |

|--------------|------------------|---------|

| A            | www.contoso.com  | /       |

| B            | www.contoso.com  | /\*     |

| C            | www.contoso.com  | /ab     |

| D            | www.contoso.com  | /abc    |

| E            | www.contoso.com  | /abc/   |

| F            | www.contoso.com  | /abc/\* |

| G            | www.contoso.com  | /abc/def|

| H            | www.contoso.com  | /path/  |

The following table shows which routing rule matches an incoming request at the Azure Front Door edge:

| Incoming Request            | Matched Route |

|-----------------------------|---------------|

| www.contoso.com/            | A             |

| www.contoso.com/a           | B             |

| www.contoso.com/ab          | C             |

| www.contoso.com/abc         | D             |

| www.contoso.com/abzzz       | B             |

| www.contoso.com/abc/        | E             |

| www.contoso.com/abc/d       | F             |

| www.contoso.com/abc/def     | G             |

| www.contoso.com/abc/defzzz  | F             |

| www.contoso.com/abc/def/ghi | F             |

| www.contoso.com/path        | B             |

| www.contoso.com/path/       | H             |

| www.contoso.com/path/zzz    | B             |

> [!WARNING]

> If there are no routing rules for an exact-match frontend host without a catch-all route path (/*), no routing rule will be matched.

>

> Example configuration:

>

> | Route | Host                | Path    |

> |-------|---------------------|---------|

> | A     | profile.contoso.com | /api/\* |

>

> Matching table:

>

> | Incoming request         | Matched Route |

> |--------------------------|---------------|

> | profile.domain.com/other | None. Error 404: Bad Request |

### Routing decision

Once Azure Front Door matches a routing rule, it decides how to process the request. If a cached response is available, it sends that response back to the client.

If you configure a [rule set](front-door-rules-engine.md) for the matched routing rule, Azure Front Door processes it in order. Rule sets can [override a route](front-door-rules-engine-actions.md#RouteConfigurationOverride) by directing traffic to a specific origin group. If you don't define a rule set, Azure Front Door forwards the request to the origin group without changes.

If Azure Front Door (classic) doesn't have a cached response, it checks for a [URL rewrite](front-door-url-rewrite.md) configuration. If you don't define a custom forwarding path, Azure Front Door forwards the request to the appropriate backend in the configured backend pool. If you define a custom forwarding path, Azure Front Door updates the request path accordingly and then forwards it to the backend.

## Next steps

- [Create an Azure Front Door](standard-premium/create-front-door-portal.md).

- Learn about the [Azure Front Door routing architecture](front-door-routing-architecture.md).

- [Create an Azure Front Door (classic)](quickstart-create-front-door.md).

- Learn about the [Azure Front Door routing architecture](front-door-routing-architecture.md).


# Front Door Routing Limits

# Front Door routing limits

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium :heavy_check_mark: Front Door (classic)

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

Each Front Door profile has a *composite route limit*.

Your Front Door profile's composite route metric is derived from the number of routes, and the front end domains, protocols, and paths associated with that route.

The composite route metric for each Front Door profile can't exceed 5000.

> [!TIP]

> Most Front Door profiles don't approach the composite route limit. However, if you have a large Front Door profile, consider whether you could exceed the limit and plan accordingly.

The number of origin groups, origins, and endpoints don't affect your composite routing limit. However, there are other limits that apply to these resources. For more information, see [Azure subscription and service limits, quotas, and constraints](../azure-resource-manager/management/azure-subscription-service-limits.md#azure-front-door-standard-and-premium-service-limits).

## Calculate your profile's composite limit

The composite limit of a profile is the sum of the composite routes and the composite override routes. Each route has a composite route metric, which is computed as follows:

### Composite route calculation

1. Select a route from your profile.

1. Multiply the number of HTTP domains by the number of HTTP paths.

1. Multiply the number of HTTPS domains by the number of HTTPS paths.

1. Add the results of steps 1a and 1b together to give the composite route metric for this individual route.

1. Repeat these steps for each route in your profile.

### Composite route overrides calculation

The composite route overrides metric is a variation of the composite route metrics, where the number of domains is multiplied by the number of route overrides instead of the number of paths. The list of rules for each route determines the route overrides.

1. Select a route from your profile. Let **n** be the number of route overrides present in the list of rules for this route.

1. Multiply the number of HTTP domains by **n**.

1. Multiply the number of HTTPS domains by **n**.

1. Add the results of steps 1a and 1b together to give the composite override route metric for this individual route.

1. Repeat these steps for each route in your profile.

Add together all of the composite route and route override metrics for each route. This number is your profile's composite limit.

### Example

Suppose you have two routes in your Front Door profile. The routes are named *Route 1* and *Route 2*. You plan to configure the routes as follows:

* *Route 1* has 50 domains associated to it, and requires HTTPS for all inbound requests. *Route 1* specifies 80 paths. *Route 1* also has two route overrides.

* *Route 2* has 25 domains associated to it. *Route 2* specifies 25 paths, and supports both the HTTP and HTTPS protocols. *Route 2* also has one route override.

The following calculation illustrates how to determine the composite route metric for this scenario:

```

Profile composite route metric = Route 1 composite route metric + Route 1 composite route override metric+ Route 2 composite route metric + Route 2 composite route override metric

= Route 1 [HTTPS (50 Domains * 80 Paths)] + Route 1 [Route Override (50 Domains * 2 route overrides)] + Route 2 [HTTP (25 Domains * 25 Paths) + HTTPS(25 Domains * 25 Paths)] + Route 2 [HTTP (25 Domains * 1 route override) + HTTPS(25 Domains * 1 route override)]

= [50 * 80] + [50 * 2] + [(25 * 25) + (25 * 25)] + [(25 * 1) + (25 * 1)]

= 5400

```

The calculated metric of 5400 exceeds the limit of 5000, so you can't configure a Front Door profile in this way.

## Mitigation

If your profile's composite route metric exceed 5000, consider the following mitigation strategies:

- Deploy multiple Front Door profiles, and spread your routes across them. The composite route limit applies within a single profile.

- Use [wildcard domains](front-door-wildcard-domain.md) instead of specifying subdomains individually, which might help to reduce the number of domains in your profile.

- Require HTTPS for inbound traffic, which reduces the number of HTTP routes in your profile and also improves your solution's security.

## Next step

> [!div class="nextstepaction"]

> [Create a Front Door](quickstart-create-front-door.md)


# Scenarios

# Accelerate and secure your web application with Azure Front Door

Azure Front Door is a globally distributed content delivery network (CDN) that provides lower latency and faster delivery of your web application and content. Moreover, Front Door allows for your content to be available with the highest levels of resiliency, and provides a wide range of features including an advanced application load balancer, traffic acceleration, and security.

Consider deploying Front Door in front of any publicly facing web application.

## Well-architected solutions on Azure

The [Azure Well-Architected Framework](/azure/architecture/framework/) describes five pillars of architectural excellence. Azure Front Door helps you to address each of the five pillars by using its built-in features and capabilities.

### Performance efficiency

Front Door provides several features to help to accelerate the performance of your application.

- **Caching:** Front Door provides a powerful content delivery network (CDN) to [cache content at the network edge](front-door-caching.md). Almost all web applications contain cacheable content. Static assets like images and JavaScript files are cacheable. Also, many APIs return responses that can be cached, even for a short duration. Caching helps to improve the performance of your application, and to reduce the load on your application servers.

- **Compression:** [Many response types can be compressed](standard-premium/how-to-compression.md), which can improve your application's response time.

- **Global traffic acceleration:** Front Door's global traffic acceleration capabilities help to [improve the performance of dynamic web applications](front-door-traffic-acceleration.md) by routing requests through Microsoft's high-speed backbone network.

- **TLS termination:** Connections to Front Door terminate at the closest Front Door point of presence (PoP). TLS decryption is performed by the PoP. The biggest performance hit when doing TLS decryption is the initial handshake. To improve performance, the server doing the decryption caches TLS session IDs and manages TLS session tickets. If TLS connections are terminated at the Front Door PoP, all requests from the same client can use the cached values. If it's done on the origin servers, then each time the client's requests go to a different server the client must reauthenticate. The use of TLS tickets can help mitigate this issue, but they aren't supported by all clients and can be difficult to configure and manage.

### Security

Front Door's security capabilities help to protect your application servers from several different types of threats.

- **End-to-end TLS:** Front Door supports end-to-end TLS encryption. Front Door TLS/SSL offload terminates the TLS connection, decrypts the traffic at the Azure Front Door, and re-encrypts the traffic before forwarding it to the backend.

- **Managed TLS certificates:** Front Door can [issue and manage certificates](domain.md#https-for-custom-domains), ensuring that your applications are protected by strong encryption and trust.

- **Custom TLS certificates:** If you need to bring your own TLS certificates, Front Door enables you to use a [managed identity to access the key vault](managed-identity.md) that contains the certificate.

- **Web application firewall:** Front Door's web application firewall (WAF) provides a range of security capabilities to your application. [Managed rule sets](../web-application-firewall/afds/waf-front-door-drs.md) scan incoming requests for suspicious content. [Bot protection rules](../web-application-firewall/afds/afds-overview.md#bot-protection-rule-set) identify and respond to traffic from bots. [Geo-filtering](../web-application-firewall/afds/waf-front-door-geo-filtering.md) and [rate limiting](../web-application-firewall/afds/waf-front-door-rate-limit.md) features protect your application servers from unexpected traffic.

- **Protocol blocking:** Front Door only accepts traffic on the HTTP and HTTPS protocols, and will only process valid requests with a known `Host` header. Because of this behavior, your application is protected against many types of attacks across a range of protocols.

- **DDoS protection:** Because of Front Door's architecture, it can also absorb large [distributed denial of service (DDoS) attacks](front-door-ddos.md) and prevent the traffic from reaching your application.

- **Private Link origins:** [Private Link integration](private-link.md) helps you to protect your backend applications, ensuring that traffic can only reach your application by passing through Front Door and its security protections.

When you have strict network security requirements, you can use Azure Front Door to manage inbound HTTP and HTTPS traffic to your application, and use [Azure Firewall](../firewall/overview.md) to control non-HTTP and egress traffic.

### Reliability

By using Front Door, you can create resilient, highly available solutions.

- **Load balancing and failover:** Front Door is a global load balancer. Front Door monitors the health of your origin servers, and if an origin becomes unavailable, [Front Door can route requests to an alternative origin](routing-methods.md). You can also use Front Door to spread traffic across your origins to reduce the load on any one origin server.

- **Automatic routing:** Front Door itself has a [large number of PoPs](edge-locations-by-region.md), each of which can serve traffic for any request. [Azure Front Door's routing architecture](front-door-traffic-acceleration.md) automatically steers traffic to the closest available Front Door PoP, and if a PoP is unavailable, clients are automatically routed to the next closest PoP.

- **Caching:** By using the Front Door cache, you reduce the load on your application servers. If your servers are unavailable, Front Door might be able to continue to serve cached responses until your application recovers.

### Cost optimization

Front Door can help you to reduce the cost of running your Azure solution.

- **Caching:** By enabling [caching](front-door-caching.md), content is returned from global Front Door edge nodes. This approach reduces global bandwidth charges and improves performance.

- **Compression:** When Front Door [compresses your responses](standard-premium/how-to-compression.md), it can reduce the bandwidth charges for your solution.

- **Spread traffic across origins:** Use Front Door to reduce the need to scale your application servers, or overprovision the capacity of your servers for traffic spikes. Each Front Door PoP can return cached content if it's available, which reduces the load on your application servers. You can also spread traffic across multiple backend servers, reducing the load on each individual server.

- **Shared profile:** You can use a single Front Door profile for many different applications. When you configure multiple applications in Front Door, you share the cost across each application, and you can reduce the configuration you need to perform.

### Operational excellence

Front Door can help to reduce the operational burden of running a modern internet application, and enable you to make some kinds of changes to your solution without modifying your applications.

- **Managed TLS certificates:** Front Door can [issue and manage certificates](domain.md#https-for-custom-domains). This feature means you don't need to manage certificate renewals, and you reduce the likelihood of an outage that's caused by using an invalid or expired TLS certificate.

- **Wildcard TLS certificates:** Front Door's support for [wildcard domains](front-door-wildcard-domain.md), including DNS and TLS certificates, enables you to use multiple hostnames without reconfiguring Front Door for each subdomain.

- **HTTP/2:** Front Door can help you to modernize your legacy applications with [HTTP/2 support](front-door-http2.md) without modifying your application servers.

- **Rules engine:** The Front Door [rules engine](front-door-rules-engine.md) enables you to change the internal architecture of your solution without affecting your clients.

- **Infrastructure as code:** You can also deploy and configure Front Door by using infrastructure as code (IaC) technologies including Bicep, Terraform, ARM templates, Azure PowerShell, and the Azure CLI.

## Solution architecture

When you deploy a solution that uses Azure Front Door, you should consider how your traffic flows from your client to Front Door, and from Front Door to your origins.

The following diagram illustrates a generic solution architecture using Front Door:

### Client to Front Door

Traffic from the client first arrives at a Front Door PoP. Front Door has a [large number of PoPs](edge-locations-by-region.md) distributed worldwide, and [Azure Front Door's routing architecture](front-door-traffic-acceleration.md) automatically routes traffic to the closest available Front Door PoP.

When the request is received by Front Door's PoP, Front Door uses your [custom domain name](front-door-custom-domain.md) to serve the request. Front Door performs [TLS offload](end-to-end-tls.md) by using either a Front Door-managed TLS certificate or a custom TLS certificate.

The PoP performs many functions based on the configuration you specify in your Front Door profile, including:

- Protecting your solution against many types of [DDoS attacks](front-door-ddos.md).

- Scanning the request for known vulnerabilities, by using the [Front Door WAF](web-application-firewall.md).

- Returning [cached responses](front-door-caching.md) to improve performance, if they're stored at the Front Door PoP and are valid for the request.

- [Compressing responses](standard-premium/how-to-compression.md) to improve performance.

- Returning [HTTP redirect responses](front-door-url-redirect.md) directly from Front Door.

- Selecting the best origin to receive the traffic based on the [routing architecture](front-door-routing-architecture.md).

- Modifying a request by using the [rules engine](front-door-rules-engine.md).

After Front Door finishes processing the inbound request, it either responds directly to the client (for example, when it returns a cached result) or forwards the request to the origin.

### Front Door to origin

Front Door can send traffic to your origin in two different ways: by using Private Link, and by using public IP addresses.

The premium SKU of Front Door supports sending traffic to some origin types by using Private Link. When you configure Private Link for your origin, traffic uses private IP addresses. This approach can be used to ensure that your origin only accepts traffic from your specific Front Door instance, and you can block traffic that came from the internet.

When the Front Door PoP sends requests to your origin by using a public IP address, it initiates a new TCP connection. Because of this behavior, your origin server sees the request originating from Front Door's IP address instead of the client.

Whichever approach you use to send traffic to your origin, it's usually a good practice to configure your origin to expect traffic from your Front Door profile, and to block traffic that doesn't flow through Front Door. For more information, see [Secure traffic to Azure Front Door origins](origin-security.md).

## Response processing

Front Door's PoP also processes the outbound response. Response processing might include the following steps:

- Saving a response to the PoP's cache to accelerate later requests.

- Modifying a response header by using the [rules engine](front-door-rules-engine-actions.md#modify-response-header).

## Analytics and reporting

Because Front Door processes all incoming requests, it has visibility of all traffic flowing through your solution. You can use Front Door's [reports](standard-premium/how-to-reports.md), [metrics](standard-premium/how-to-monitor-metrics.md) and [logs](standard-premium/how-to-logs.md), to understand your traffic patterns.

> [!TIP]

> When you use Front Door, some requests might not be processed by your origin server. For example, Front Door's WAF might block some requests, and it might return cached responses for other requests. Use Front Door's telemetry to understand your solution's traffic patterns.

## Next steps

Learn how to [create a Front Door profile](create-front-door-portal.md).


# Scenario Storage Blobs

# Use Azure Front Door with Azure Storage Blobs

Azure Front Door enhances the delivery of static content from Azure Storage blobs, providing a secure and scalable architecture. This setup is ideal for various use cases, such as website hosting and file delivery.

## Architecture

In this reference architecture, a storage account and an Azure Front Door profile with a single origin are deployed.

## Data flow

The data flows through the scenario as follows:

1. The client establishes a secure connection to Azure Front Door using a custom domain name and a Front Door-provided TLS certificate. The connection terminates at a nearby Front Door point of presence (PoP).

1. Azure Front Door web application firewall (WAF) scans the request. If the WAF determines the request is too risky, it blocks the request and returns an HTTP 403 error response.

1. If the Front Door PoP's cache contains a valid response, Front Door returns the response immediately.

1. If not, the PoP sends the request to the origin storage account using Microsoft's backbone network, using a separate, long-lived TCP connection. In this scenario, Private Link securely connects to the storage account.

1. The storage account sends a response to the Front Door PoP.

1. The PoP stores the response in its cache for future requests.

1. The PoP returns the response to the client.

1. Any direct requests to the storage account through the internet get blocked by the Azure Storage firewall.

## Components

- [Azure Storage](https://azure.microsoft.com/products/storage/blobs): Stores static content in blobs.

- [Azure Front Door](https://azure.microsoft.com/services/frontdoor/): Receives inbound connections from clients, scans them with the WAF, securely forwards the requests to the storage account, and caches responses.

### Alternatives

If you store static files with another cloud storage provider or on your own infrastructure, this scenario still largely applies. However, you need to ensure that incoming traffic to your origin server is verified to come through Front Door. If your storage provider doesn't support Private Link, consider using an alternative approach like [allowlisting the Front Door service tag and inspecting the `X-Azure-FDID` header](origin-security.md).

## Scenario details

Static content delivery is beneficial in many situations, such as:

- Delivering images, CSS files, and JavaScript files for a web application.

- Serving files and documents, such as PDF or JSON files.

- Delivering nonstreaming video.

Static content typically doesn't change frequently and can be large in size, making it ideal for caching to improve performance and reduce costs.

In complex scenarios, a single Front Door profile can serve both static and dynamic content. You can use separate origin groups for each type of content and use the routing capabilities to direct incoming requests to the appropriate origin.

## Considerations

### Scalability and performance

Azure Front Door acts as a content delivery network (CDN), caching content at its globally distributed PoPs. When a cached response is available, Azure Front Door quickly serves it, enhancing performance and reducing the load on the origin. If the PoP lacks a valid cached response, Azure Front Door's traffic acceleration capabilities expedite content delivery from the origin.

### Security

#### Authentication

Azure Front Door is designed for internet-facing scenarios and is optimized for publicly accessible blobs. To authenticate access to blobs, consider using [shared access signatures (SAS)](../storage/common/storage-sas-overview.md). Ensure you enable the [*Use Query String* behavior](front-door-caching.md#query-string-behavior) to prevent Azure Front Door from serving requests to unauthenticated clients. This approach might limit the effectiveness of caching, as each request with a different SAS must be sent to the origin.

#### Origin security

- If you're using the premium tier, Azure Front Door can connect securely to the Azure Storage account using [Private Link](private-link.md). The storage account can be configured to deny public network access, allowing requests only through the private endpoint used by Azure Front Door. This setup ensures all requests get processed by Azure Front Door, protecting your storage account from direct internet exposure.

- If you're using the standard tier, you can secure requests with a [shared access signature (SAS)](../storage/common/storage-sas-overview.md) and either have clients include the SAS in their requests or use the Azure Front Door [rules engine](front-door-rules-engine.md) to attach it. The storage account's network access must be publicly accessible (from all networks or from Front Door IP addresses in `AzureFrontDoor.Backend` service tag).

#### Custom domain names

Azure Front Door supports custom domain names and can manage TLS certificates for these domains. Using custom domains ensures clients receive files from a trusted source, with TLS encrypting every connection to Azure Front Door. Azure Front Door's management of TLS certificates helps avoid outages and security issues from invalid or outdated certificates.

#### Web Application Firewall

The Azure Front Door WAF's managed rule sets scan requests for common and emerging security threats. We recommend using the WAF and managed rules for both static and dynamic applications.

Additionally, the Azure Front Door WAF can perform [rate limiting](../web-application-firewall/afds/waf-front-door-rate-limit.md) and [geo-filtering](../web-application-firewall/afds/waf-front-door-geo-filtering.md) if needed.

### Resiliency

Azure Front Door is a highly available service with a globally distributed architecture, making it resilient to failures in individual Azure regions and PoPs.

Using the Azure Front Door cache reduces the load on your storage account. If your storage account becomes unavailable, Azure Front Door might continue to serve cached responses until your application recovers.

To further improve resiliency, consider the redundancy of your storage account. For more information, see [Azure Storage redundancy](../storage/common/storage-redundancy.md). Alternatively, deploy multiple storage accounts and configure multiple origins in your Azure Front Door origin group. Set up fail over between origins by configuring each origin's priority. For more information, see [Origins and origin groups in Azure Front Door](origin.md).

### Cost optimization

Caching helps reduce the cost of delivering static content. Azure Front Door's PoPs store copies of responses and can deliver these cached responses for subsequent requests, reducing the request load on the origin. In high-scale static content solutions, especially those delivering large files, caching can significantly reduce traffic costs.

To use Private Link in this solution, deploy the premium tier of Azure Front Door. The standard tier can be used if you don't need to block direct traffic to your storage account. For more information, see [Origin security](#origin-security).

## Deploy this scenario

To deploy this scenario using Bicep or JSON ARM templates, [see this quickstart](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-premium-storage-blobs-private-link).

To deploy this scenario using Terraform, [see this quickstart](https://github.com/Azure/terraform/tree/master/quickstart/101-front-door-premium-storage-blobs-private-link).

## Next step

Learn how to [create an Azure Front Door profile](create-front-door-portal.md).


# Scenario Upload Storage Blobs

# Reliable file upload to Azure Storage Blob through Azure Front Door

Utilizing Azure Front Door to upload files to Azure Storage offers many benefits, including enhanced resiliency, scalability, and extra security measures. These measures include the scanning of uploaded content with Web Application Firewall (WAF) and the use of custom Transport Layer Security (TLS) certificates for storage accounts.

## Architecture

![Architecture diagram showing traffic flowing through Front Door to the storage accounts when uploading blobs.](media/scenario-storage-blobs-upload/upload-blob-front-door-architecture-highres.png)

In this reference architecture, multiple Azure storage accounts and an Azure Front Door profile with various origins are deployed. Utilizing multiple storage accounts for content upload improve performance and reliability and facilitates load distribution by having different clients use storage accounts in different orders. You deploy as well Azure App Service to host API, and Azure Service Bus queue.

## Dataflow

The dataflow in this scenario is as follows:

1. The client app initiates a web-based API, retrieving a list of multiple upload locations. For each file that the client uploads, the API generates a list of possible upload locations, with one in each of the existing storage accounts. Each URL contains a Shared Access Signature (SAS), ensuring the exclusive use of the URL for uploading to the designated blob URL.

2. The client application attempts to upload a blob using first URL from the list returned by API. The client establishes a secure connection to Azure Front Door by using a custom domain name and custom TLS certificate.

3. The Azure Front Door WAF scans the request. If the WAF determines the request's risk level is too high, it blocks the request and Azure Front Door returns an HTTP 403 error response. If not, the request is routed to the desired storage account.

4. The file is uploaded into Azure Storage account. If this request fails, the client application will attempt to upload to an alternative storage account using next URL in the list returned by the API.

5. The client application notifies the API that the file upload is complete.

6. The API places an item in Azure Service Bus queue for further processing of uploaded file.

## Components

- Azure App Service is responsible for generating the upload URLs and SAS for blobs.

- Azure Front Door handles client connections, scans them with the WAF, and routes the upload request to Azure storage account.

- Azure Storage is utilized for storing uploaded files in blobs.

- Azure Service Bus serves as a queue to trigger further processing of uploaded content.

## Scenario details

Often the responsibility of file upload is assigned to the API or backend systems. However, by enabling the client application to directly upload JSON files into blob storage, we ensure that the compute resource (the API layer handling the uploads from the client) isn't the bottleneck. This approach also reduces the overall cost, since the API no longer expends compute time on file uploads.

The API is responsible for ensuring an even distribution of files across storage accounts. This implies that you must define a logic to determine the default storage account for the client application to use.

The combination of Azure Front Door and Azure Storage accounts provides a single point of entry (a single domain) for content upload.

### Azure Front Door configuration with multiple storage account origins

The configuration of Azure Front Door includes the following steps for each storage account:

- Origin configuration

- Route configuration

- Rule set configuration

1. In the *origin configuration*, you need to define the origin type as a blob storage account and select the appropriate storage account available within your subscription.

1. In the *Origin group route*, you have to define a path for processing with in the origin group. Ensure to select the newly created origin group and specify the path to the container within the storage account.

1. Finally, you need to create a new Rule set configuration. It's important to configure *Preserve unmatched path* setting, which allows appending the remaining path after the source pattern to the new path.

## Considerations

### Scalability and performance

The proposed architecture allows you to achieve horizontal scalability by using multiple storage accounts for content upload.

### Resiliency

Azure Front Door, with its globally distributed architecture, is a highly available service that is resilient to failures of a single Azure region and Point of Presence (PoPs).

This architecture, which deploys multiple storage accounts in different regions, increases resiliency and helps to achieve load distribution by having different clients using storage accounts in different orders.

### Cost optimization

The cost structure of Azure Storage allows for creation of any amount of storage account as required without increasing the costs of the solution. The amount and size of the stored files affect the costs.

### Security

By using Azure Front Door you're benefiting from security features, such as DDoS protection. The default Azure infrastructure DDoS protection, which monitors and mitigates network layer attacks in real-time by using the global scale and capacity of Azure Front Door’s network. The use of Web Application Firewall (WAF) protects your web services against common exploits and vulnerabilities. You can also use Azure Front Door WAF to perform rate limiting and geo-filtering if your application requires those capabilities.

It's also possible to secure Azure Storage accounts by using Private Link. The storage account can be configured to deny direct access from the internet, and to only allow requests through the private endpoint connection used by Azure Front Door. This configuration ensures that every request gets processed by Front Door, and avoids exposing the contents of your storage account directly to the internet. However, this configuration requires the premium tier of Azure Front Door. If you use the standard tier, your storage account must be publicly accessible.

### Custom domain names

Azure Front Door supports custom domain names, and can issue and manage TLS certificates for those domains. By using custom domains, you can ensure that your clients receive files from a trusted and familiar domain name, and that TLS encrypts every connection to Front Door. When Front Door manages your TLS certificates, you avoid outages and security issues due to invalid or outdated TLS certificates.

Azure Storage also supports custom domain names, but doesn't support HTTPS when using a custom domain. Front Door is the best approach to use a custom domain name with a storage account.

## Deploy this scenario

To deploy this scenario by using Bicep, see deploy [Azure Front Door Premium with blob origin and Private Link](/samples/azure/azure-quickstart-templates/front-door-standard-premium-storage-blobs-upload/).

## Next steps

Learn how to [create a Front Door profile](create-front-door-portal.md).


# Create Front Door Powershell

# Quickstart: Create an Azure Front Door using Azure PowerShell

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

In this quickstart, you learn how to create an Azure Front Door profile using Azure PowerShell. You use two Web Apps as your origin and verify connectivity through the Azure Front Door endpoint hostname.

[!INCLUDE [ddos-waf-recommendation](../../includes/ddos-waf-recommendation.md)]

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- Azure PowerShell installed locally or Azure Cloud Shell.

[!INCLUDE [updated-for-az](~/reusable-content/ce-skilling/azure/includes/updated-for-az.md)]

[!INCLUDE [cloud-shell-try-it.md](~/reusable-content/ce-skilling/azure/includes/cloud-shell-try-it.md)]

## Create a resource group

Create a resource group with [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup):

```azurepowershell-interactive

New-AzResourceGroup -Name myRGFD -Location centralus

```

## Create two web app instances

Create two web app instances in different Azure regions using [New-AzWebApp](/powershell/module/az.websites/new-azwebapp):

```azurepowershell-interactive

# Create first web app in Central US region.

$webapp1 = New-AzWebApp `

-Name "WebAppContoso-01" `

-Location centralus `

-ResourceGroupName myRGFD `

-AppServicePlan myAppServicePlanCentralUS

# Create second web app in East US region.

$webapp2 = New-AzWebApp `

-Name "WebAppContoso-02" `

-Location EastUS `

-ResourceGroupName myRGFD `

-AppServicePlan myAppServicePlanEastUS

```

## Create an Azure Front Door

### Create an Azure Front Door profile

Run [New-AzFrontDoorCdnProfile](/powershell/module/az.cdn/new-azfrontdoorcdnprofile) to create an Azure Front Door profile:

```azurepowershell-interactive

$fdprofile = New-AzFrontDoorCdnProfile `

-ResourceGroupName myRGFD `

-Name contosoAFD `

-SkuName Premium_AzureFrontDoor `

-Location Global

```

### Add an endpoint

Run [New-AzFrontDoorCdnEndpoint](/powershell/module/az.cdn/new-azfrontdoorcdnendpoint) to create an endpoint in your profile:

```azurepowershell-interactive

$FDendpoint = New-AzFrontDoorCdnEndpoint `

-EndpointName contosofrontend `

-ProfileName contosoAFD `

-ResourceGroupName myRGFD `

-Location Global

```

### Create an origin group

Create health probe and load balancing settings, then create an origin group using [New-AzFrontDoorCdnOriginGroup](/powershell/module/az.cdn/new-azfrontdoorcdnorigingroup):

```azurepowershell-interactive

# Create health probe settings

$HealthProbeSetting = New-AzFrontDoorCdnOriginGroupHealthProbeSettingObject `

-ProbeIntervalInSecond 60 `

-ProbePath "/" `

-ProbeRequestType GET `

-ProbeProtocol Http

# Create load balancing settings

$LoadBalancingSetting = New-AzFrontDoorCdnOriginGroupLoadBalancingSettingObject `

-AdditionalLatencyInMillisecond 50 `

-SampleSize 4 `

-SuccessfulSamplesRequired 3

# Create origin group

$originpool = New-AzFrontDoorCdnOriginGroup `

-OriginGroupName og `

-ProfileName contosoAFD `

-ResourceGroupName myRGFD `

-HealthProbeSetting $HealthProbeSetting `

-LoadBalancingSetting $LoadBalancingSetting

```

### Add origins to the group

Add your Web App origins to the origin group using [New-AzFrontDoorCdnOrigin](/powershell/module/az.cdn/new-azfrontdoorcdnorigin):

```azurepowershell-interactive

# Add first web app origin to origin group.

$origin1 = New-AzFrontDoorCdnOrigin `

-OriginGroupName og `

-OriginName contoso1 `

-ProfileName contosoAFD `

-ResourceGroupName myRGFD `

-HostName webappcontoso-01.azurewebsites.net `

-OriginHostHeader webappcontoso-01.azurewebsites.net `

-HttpPort 80 `

-HttpsPort 443 `

-Priority 1 `

-Weight 1000

# Add second web app origin to origin group.

$origin2 = New-AzFrontDoorCdnOrigin `

-OriginGroupName og `

-OriginName contoso2 `

-ProfileName contosoAFD `

-ResourceGroupName myRGFD `

-HostName webappcontoso-02.azurewebsites.net `

-OriginHostHeader webappcontoso-02.azurewebsites.net `

-HttpPort 80 `

-HttpsPort 443 `

-Priority 1 `

-Weight 1000

```

### Add a route

Map your endpoint to the origin group using [New-AzFrontDoorCdnRoute](/powershell/module/az.cdn/new-azfrontdoorcdnroute):

```azurepowershell-interactive

$Route = New-AzFrontDoorCdnRoute `

-EndpointName contosofrontend `

-Name defaultroute `

-ProfileName contosoAFD `

-ResourceGroupName myRGFD `

-ForwardingProtocol MatchRequest `

-HttpsRedirect Enabled `

-LinkToDefaultDomain Enabled `

-OriginGroupId $originpool.Id `

-SupportedProtocol Http,Https

```

## Test the Azure Front Door

After you create the Azure Front Door profile, it takes a few minutes for the configuration to be deployed globally. Once completed, access the frontend host you created.

Run [Get-AzFrontDoorCdnEndpoint](/powershell/module/az.cdn/get-azfrontdoorcdnendpoint) to get the hostname of the Azure Front Door endpoint:

```azurepowershell-interactive

$fd = Get-AzFrontDoorCdnEndpoint `

-EndpointName contosofrontend `

-ProfileName contosoafd `

-ResourceGroupName myRGFD

$fd.hostname

```

In a browser, go to the endpoint hostname: `contosofrontend-<hash>.z01.azurefd.net`. Your request is routed to the web app with the lowest latency in the origin group.

To test instant global failover:

1. Open a browser and go to the endpoint hostname: `contosofrontend-<hash>.z01.azurefd.net`.

1. Stop one of the Web Apps by running [Stop-AzWebApp](/powershell/module/az.websites/stop-azwebapp):

```azurepowershell-interactive

Stop-AzWebApp -ResourceGroupName myRGFD -Name "WebAppContoso-01"

```

1. Refresh your browser. You should see the same information page.

1. Stop the other web app:

```azurepowershell-interactive

Stop-AzWebApp -ResourceGroupName myRGFD -Name "WebAppContoso-02"

```

1. Refresh your browser. This time, you should see an error message.

1. Restart one of the Web Apps by running [Start-AzWebApp](/powershell/module/az.websites/start-azwebapp). Refresh your browser and the page go back to normal:

```azurepowershell-interactive

Start-AzWebApp -ResourceGroupName myRGFD -Name "WebAppContoso-01"

```

## Clean up resources

When you no longer need the resources created with the Azure Front Door, delete the resource group. This action deletes the Azure Front Door and all its related resources. Run [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup):

```azurepowershell-interactive

Remove-AzResourceGroup -Name myRGFD

```

## Next steps

To learn how to add a custom domain to your Azure Front Door, continue to the Azure Front Door tutorials.

> [!div class="nextstepaction"]

> [Add a custom domain](front-door-custom-domain.md)


# Create Front Door Cli

# Quickstart: Create an Azure Front Door using Azure CLI

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

In this quickstart, you learn how to create an Azure Front Door using Azure CLI. You set up a profile with two Azure Web Apps as origins and add a WAF security policy. Finally, you verify connectivity to your Web Apps using the Azure Front Door endpoint hostname.

[!INCLUDE [ddos-waf-recommendation](../../includes/ddos-waf-recommendation.md)]

[!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment](~/reusable-content/azure-cli/azure-cli-prepare-your-environment.md)]

## Create a resource group

In Azure, related resources are allocated to a resource group. You can use an existing resource group or create a new one.

Run [az group create](/cli/azure/group) to create a resource group.

```azurecli-interactive

az group create --name myRGFD --location centralus

```

## Create an Azure Front Door profile

Next, create the Azure Front Door profile that your two App Services uses as origins.

Run [az afd profile create](/cli/azure/afd/profile#az-afd-profile-create) to create an Azure Front Door profile.

> [!NOTE]

> If you want to deploy Azure Front Door Standard instead of Premium, substitute the value of the sku parameter with `Standard_AzureFrontDoor`. Managed rules with WAF Policy are not available with the Standard SKU. For a detailed comparison, see [Azure Front Door tier comparison](standard-premium/tier-comparison.md).

```azurecli-interactive

az afd profile create \

--profile-name contosoafd \

--resource-group myRGFD \

--sku Premium_AzureFrontDoor

```

## Create two instances of a web app

In this step, you create two web app instances running in different Azure regions. Both instances operate in Active/Active mode, meaning either can handle traffic. This setup is different from an Active/Stand-By configuration, where one instance serves as a failover.

### Create app service plans

First, create two app service plans: one in *Central US* and another in *East US*.

Run the following commands to create the app service plans:

```azurecli-interactive

az appservice plan create \

--name myAppServicePlanCentralUS \

--resource-group myRGFD \

--location centralus

```

```azurecli-interactive

az appservice plan create \

--name myAppServicePlanEastUS \

--resource-group myRGFD \

--location eastus

```

### Create web apps

Next, create a web app in each of the app service plans created in the previous step. Web app names must be globally unique.

Run the following commands to create the web apps:

```azurecli-interactive

az webapp create \

--name WebAppContoso-01 \

--resource-group myRGFD \

--plan myAppServicePlanCentralUS

```

```azurecli-interactive

az webapp create \

--name WebAppContoso-02 \

--resource-group myRGFD \

--plan myAppServicePlanEastUS

```

Make a note of the default host names for each web app, as you'll need them to define the backend addresses when deploying the Azure Front Door in the next step.

## Create an Azure Front Door

### Create an Azure Front Door profile

Run [az afd profile create](/cli/azure/afd/profile#az-afd-profile-create) to create an Azure Front Door profile.

> [!NOTE]

> To deploy an Azure Front Door Standard instead of Premium, set the `sku` parameter to `Standard_AzureFrontDoor`. Managed rules with WAF Policy are not available with the Standard SKU. For a detailed comparison, see [Azure Front Door tier comparison](standard-premium/tier-comparison.md).

```azurecli-interactive

az afd profile create \

--profile-name contosoafd \

--resource-group myRGFD \

--sku Premium_AzureFrontDoor

```

### Add an endpoint

Create an endpoint in your Azure Front Door profile. An *endpoint* is a logical grouping of one or more routes associated with domain names. Each endpoint is assigned a domain name by Azure Front Door, and you can associate endpoints with custom domains using routes. Azure Front Door profiles can contain multiple endpoints.

Run [az afd endpoint create](/cli/azure/afd/endpoint#az-afd-endpoint-create) to create an endpoint in your profile.

```azurecli-interactive

az afd endpoint create \

--resource-group myRGFD \

--endpoint-name contosofrontend \

--profile-name contosoafd \

--enabled-state Enabled

```

For more information about endpoints in Azure Front Door, see [Endpoints in Azure Front Door](./endpoint.md).

### Create an origin group

Create an origin group that defines the traffic and expected responses for your app instances. Origin groups also define how origins get evaluated by health probes.

Run [az afd origin-group create](/cli/azure/afd/origin-group#az-afd-origin-group-create) to create an origin group containing your two web apps.

```azurecli-interactive

az afd origin-group create \

--resource-group myRGFD \

--origin-group-name og \

--profile-name contosoafd \

--probe-request-type GET \

--probe-protocol Http \

--probe-interval-in-seconds 60 \

--probe-path / \

--sample-size 4 \

--successful-samples-required 3 \

--additional-latency-in-milliseconds 50

```

### Add origins to the origin group

Add both of your app instances created earlier as origins to your new origin group. Origins in Azure Front Door refer to applications that Azure Front Door retrieves content from when caching isn't enabled or when a cache miss occurs.

Run [az afd origin create](/cli/azure/afd/origin#az-afd-origin-create) to add your first app instance as an origin to your origin group.

```azurecli-interactive

az afd origin create \

--resource-group myRGFD \

--host-name webappcontoso-01.azurewebsites.net \

--profile-name contosoafd \

--origin-group-name og \

--origin-name contoso1 \

--origin-host-header webappcontoso-01.azurewebsites.net \

--priority 1 \

--weight 1000 \

--enabled-state Enabled \

--http-port 80 \

--https-port 443

```

Repeat this step to add your second app instance as an origin to your origin group.

```azurecli-interactive

az afd origin create \

--resource-group myRGFD \

--host-name webappcontoso-02.azurewebsites.net \

--profile-name contosoafd \

--origin-group-name og \

--origin-name contoso2 \

--origin-host-header webappcontoso-02.azurewebsites.net \

--priority 1 \

--weight 1000 \

--enabled-state Enabled \

--http-port 80 \

--https-port 443

```

For more information about origins, origin groups, and health probes, see [Origins and origin groups in Azure Front Door](./origin.md).

### Add a route

Add a route to map the endpoint you created earlier to the origin group. This route forwards requests from the endpoint to your origin group.

Run [az afd route create](/cli/azure/afd/route#az-afd-route-create) to map your endpoint to the origin group.

```azurecli-interactive

az afd route create \

--resource-group myRGFD \

--profile-name contosoafd \

--endpoint-name contosofrontend \

--forwarding-protocol MatchRequest \

--route-name route \

--https-redirect Enabled \

--origin-group og \

--supported-protocols Http Https \

--link-to-default-domain Enabled

```

To learn more about routes in Azure Front Door, see [Traffic routing methods to origin](./routing-methods.md).

## Create a new security policy

Azure Web Application Firewall (WAF) on Azure Front Door provides centralized protection for your web applications, defending them against common exploits and vulnerabilities.

In this tutorial, you create a WAF policy that includes two managed rules. You can also create WAF policies with custom rules.

### Create a WAF policy

Run [az network front-door waf-policy create](/cli/azure/network/front-door/waf-policy#az-network-front-door-waf-policy-create) to create a new WAF policy for your Azure Front Door. This example creates a policy that is enabled and in prevention mode.

> [!NOTE]

> Managed rules are only available with the Azure Front Door Premium tier. You can use custom rules with the Standard tier.

```azurecli-interactive

az network front-door waf-policy create \

--name contosoWAF \

--resource-group myRGFD \

--sku Premium_AzureFrontDoor \

--disabled false \

--mode Prevention

```

> [!NOTE]

> If you select `Detection` mode, your WAF will not block any requests.

To learn more about WAF policy settings for Azure Front Door, see [Policy settings for Web Application Firewall on Azure Front Door](../web-application-firewall/afds/waf-front-door-policy-settings.md).

### Assign managed rules to the WAF policy

Azure-managed rule sets provide an easy way to protect your application against common security threats.

Run [az network front-door waf-policy managed-rules add](/cli/azure/network/front-door/waf-policy/managed-rules#az-network-front-door-waf-policy-managed-rules-add) to add managed rules to your WAF Policy. This example adds Microsoft_DefaultRuleSet_2.1 and Microsoft_BotManagerRuleSet_1.0 to your policy.

```azurecli-interactive

az network front-door waf-policy managed-rules add \

--policy-name contosoWAF \

--resource-group myRGFD \

--type Microsoft_DefaultRuleSet \

--action Block \

--version 2.1

```

```azurecli-interactive

az network front-door waf-policy managed-rules add \

--policy-name contosoWAF \

--resource-group myRGFD \

--type Microsoft_BotManagerRuleSet \

--version 1.0

```

To learn more about managed rules in Azure Front Door, see [Web Application Firewall DRS rule groups and rules](../web-application-firewall/afds/waf-front-door-drs.md).

### Apply the security policy

Now, apply the WAF policies to your Azure Front Door by creating a security policy. This setting applies the Azure-managed rules to the endpoint you defined earlier.

Run [az afd security-policy create](/cli/azure/afd/security-policy#az-afd-security-policy-create) to apply your WAF policy to the endpoint's default domain.

> [!NOTE]

> Replace 'mysubscription' with your Azure Subscription ID in the domains and waf-policy parameters. Run [az account subscription list](/cli/azure/account/subscription#az-account-subscription-list) to get Subscription ID details.

```azurecli-interactive

az afd security-policy create \

--resource-group myRGFD \

--profile-name contosoafd \

--security-policy-name contososecurity \

--domains /subscriptions/mysubscription/resourcegroups/myRGFD/providers/Microsoft.Cdn/profiles/contosoafd/afdEndpoints/contosofrontend \

--waf-policy /subscriptions/mysubscription/resourcegroups/myRGFD/providers/Microsoft.Network/frontdoorwebapplicationfirewallpolicies/contosoWAF

```

## Test the Azure Front Door

After you create the Azure Front Door profile, it takes a few minutes for the configuration to be deployed globally. Once completed, you can access the frontend host you created.

Run [az afd endpoint show](/cli/azure/afd/endpoint#az-afd-endpoint-show) to get the hostname of the Azure Front Door endpoint.

```azurecli-interactive

az afd endpoint show --resource-group myRGFD --profile-name contosoafd --endpoint-name contosofrontend

```

In a browser, go to the endpoint hostname: `contosofrontend-<hash>.z01.azurefd.net`. Your request is routed to the least latent Web App in the origin group.

To test instant global failover, follow these steps:

1. Open a browser and go to the endpoint hostname: `contosofrontend-<hash>.z01.azurefd.net`.

2. Stop one of the Web Apps by running [az webapp stop](/cli/azure/webapp#az-webapp-stop&preserve-view=true):

```azurecli-interactive

az webapp stop --name WebAppContoso-01 --resource-group myRGFD

```

3. Refresh your browser. You should see the same information page.

> [!TIP]

> There might be a slight delay for these actions. You may need to refresh again.

4. Stop the other web app as well:

```azurecli-interactive

az webapp stop --name WebAppContoso-02 --resource-group myRGFD

```

5. Refresh your browser. This time, you should see an error message.

6. Restart one of the Web Apps by running [az webapp start](/cli/azure/webapp#az-webapp-start&preserve-view=true). Refresh your browser, and the page should return to normal.

```azurecli-interactive

az webapp start --name WebAppContoso-01 --resource-group myRGFD

```

## Clean up resources

When you no longer need the resources created for the Azure Front Door, you can delete the resource group. This action removes the Azure Front Door and all associated resources.

Run the following command to delete the resource group:

```azurecli-interactive

az group delete --name myRGFD

```

## Next steps

Proceed to the next article to learn how to add a custom domain to your Azure Front Door.

> [!div class="nextstepaction"]

> [Add a custom domain](standard-premium/how-to-add-custom-domain.md)


# Create Front Door Bicep

# Quickstart: Create a Front Door using Bicep

This quickstart guides you through using Bicep to create an Azure Front Door with a Web App as the origin.

[!INCLUDE [ddos-waf-recommendation](../../includes/ddos-waf-recommendation.md)]

[!INCLUDE [About Bicep](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-bicep-introduction.md)]

## Prerequisites

* An active Azure subscription. Create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) if you don't have one.

* The IP address or FQDN of a website or web application.

## Review the Bicep file

The Bicep file used in this quickstart is available from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/front-door-standard-premium-app-service-public/).

In this quickstart, you will create an Azure Front Door profile, an Azure App Service, and configure the app service to validate that traffic comes through the Azure Front Door origin.

The Bicep file defines multiple Azure resources:

* [**Microsoft.Cdn/profiles**](/azure/templates/microsoft.cdn/profiles) - Azure Front Door Standard/Premium profile

* [**Microsoft.Web/serverfarms**](/azure/templates/microsoft.web/serverfarms) - App service plan to host web apps

* [**Microsoft.Web/sites**](/azure/templates/microsoft.web/sites) - Web app origin servicing requests for Front Door

## Deploy the Bicep file

1. Save the Bicep file as **main.bicep** on your local computer.

1. Deploy the Bicep file using either Azure CLI or Azure PowerShell.

# [CLI](#tab/CLI)

```azurecli

az group create --name exampleRG --location eastus

az deployment group create --resource-group exampleRG --template-file main.bicep

```

# [PowerShell](#tab/PowerShell)

```azurepowershell

New-AzResourceGroup -Name exampleRG -Location eastus

New-AzResourceGroupDeployment -ResourceGroupName exampleRG -TemplateFile ./main.bicep

```

---

After the deployment completes, you should see output similar to:

## Validate the deployment

Use Azure CLI or Azure PowerShell to list the resources deployed in the resource group.

# [CLI](#tab/CLI)

```azurecli-interactive

az resource list --resource-group exampleRG

```

# [PowerShell](#tab/PowerShell)

```azurepowershell-interactive

Get-AzResource -ResourceGroupName exampleRG

```

---

You can also validate the deployment using the Azure portal.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Select **Resource groups** from the left pane.

1. Select the resource group you created in the previous section.

1. Select the Front Door you created. You will see the endpoint hostname. Copy the hostname and paste it into the address bar of a browser. Press enter, and your requests will be routed to the web app.

## Clean up resources

When no longer needed, use the Azure portal, Azure CLI, or Azure PowerShell to delete the Front Door service and the resource group. The Front Door and all the related resources are removed.

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

In this quickstart, you created a:

* Front Door

* App Service plan

* Web App

To learn how to add a custom domain to your Front Door, continue to the Front Door tutorials.

> [!div class="nextstepaction"]

> [Front Door tutorials](front-door-custom-domain.md)


# Create Front Door Template

# Quickstart: Create an Azure Front Door using an ARM template

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

This quickstart shows you how to use an Azure Resource Manager (ARM) template to create an Azure Front Door with an Azure Web App as the origin.

[!INCLUDE [About Azure Resource Manager](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-introduction.md)]

If you meet the prerequisites and are familiar with ARM templates, select the **Deploy to Azure** button to open the template in the Azure portal.

## Prerequisites

* An Azure subscription. Create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) if you don't have one.

* The IP or FQDN of a website or web application.

## Review the template

The template used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/front-door-standard-premium-app-service-public/).

In this quickstart, you'll create an Azure Front Door Standard/Premium, an App Service, and configure the App Service to validate that traffic has come through the Azure Front Door origin.

The template defines multiple Azure resources:

* [**Microsoft.Network/frontDoors**](/azure/templates/microsoft.network/frontDoors)

* [**Microsoft.Web/serverfarms**](/azure/templates/microsoft.web/serverfarms) (App service plan to host web apps)

* [**Microsoft.Web/sites**](/azure/templates/microsoft.web/sites) (Web app origin servicing request for Azure Front Door)

## Deploy the template

1. Select **Try it** from the following code block to open Azure Cloud Shell, and then follow the instructions to sign in to Azure.

> [!NOTE]

> To deploy Azure Front Door Premium instead of Standard, substitute the value of the sku parameter with `Premium_AzureFrontDoor`. For detailed comparison, view [Azure Front Door tier comparison](standard-premium/tier-comparison.md).

```azurepowershell-interactive

$projectName = Read-Host -Prompt "Enter a project name that is used for generating resource names"

$location = Read-Host -Prompt "Enter the location (i.e. centralus)"

$templateUri = "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.cdn/front-door-standard-premium-app-service-public/azuredeploy.json"

$resourceGroupName = "${projectName}rg"

New-AzResourceGroup -Name $resourceGroupName -Location "$location"

New-AzResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateUri $templateUri -frontDoorSkuName Standard_AzureFrontDoor

Read-Host -Prompt "Press [ENTER] to continue ..."

```

Wait until you see the prompt from the console.

1. Select **Copy** from the previous code block to copy the PowerShell script.

1. Right-click the shell console pane and then select **Paste**.

1. Enter the values.

The template deployment creates an Azure Front Door with a web app as origin.

The resource group name is the project name with **rg** appended.

> [!NOTE]

> **frontDoorName** needs to be a globally unique name for the template to deploy successfully. If deployment fails, start over with Step 1.

It takes a few minutes to deploy the template. When completed, the output is similar to:

Azure PowerShell is used to deploy the template. In addition to Azure PowerShell, you can also use the Azure portal, Azure CLI, and REST API. To learn other deployment methods, see [Deploy templates](../azure-resource-manager/templates/deploy-portal.md).

## Validate the deployment

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Select **Resource groups** from the left pane.

1. Select the resource group that you created in the previous section. The default resource group name is the project name with **rg** appended.

1. Select the Azure Front Door you created previously and you'll be able to see the endpoint hostname. Copy the hostname and paste it into the address bar of a browser. Press enter and your request will automatically get routed to the web app.

## Clean up resources

When you no longer need the Azure Front Door service, delete the resource group. This will remove the Azure Front Door and all related resources.

To delete the resource group, call the `Remove-AzResourceGroup` cmdlet:

```azurepowershell-interactive

Remove-AzResourceGroup -Name <your resource group name>

```

## Next steps

In this quickstart, you created a:

* Azure Front Door

* App Service plan

* Web App

To learn how to add a custom domain to your Azure Front Door, continue to the Azure Front Door tutorials.

> [!div class="nextstepaction"]

> [Azure Front Door tutorials](front-door-custom-domain.md)


# Create Front Door Terraform

# Quickstart: Create an Azure Front Door using Terraform

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

This quickstart describes how to use Terraform to create a Front Door profile to set up high availability for a web endpoint.

[!INCLUDE [ddos-waf-recommendation](../../includes/ddos-waf-recommendation.md)]

In this article, you learn how to:

> [!div class="checklist"]

> * Create a random value for the Azure resource group name using [random_pet](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/pet).

> * Create an Azure resource group using [azurerm_resource_group](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group).

> * Create a random value for the Front Door endpoint resource name and App Service app name using [random_id](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/id).

> * Create a Front Door profile using [azurerm_cdn_frontdoor_profile](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/cdn_frontdoor_profile).

> * Create a Front Door endpoint using [azurerm_cdn_frontdoor_endpoint](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/cdn_frontdoor_endpoint).

> * Create a Front Door origin group using [azurerm_cdn_frontdoor_origin_group](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/cdn_frontdoor_origin_group)

> * Create a Front Door origin, which refers to the App Service app, using [azurerm_cdn_frontdoor_origin](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/cdn_frontdoor_origin).

> * Create a Front Door route using [azurerm_cdn_frontdoor_route](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/cdn_frontdoor_route).

> * Create an App Service plan using [azurerm_service_plan](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/service_plan).

> * Create an App Service app using [azurerm_windows_web_app](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/windows_web_app).

## Prerequisites

- [Install and configure Terraform](/azure/developer/terraform/quickstart-configure)

## Implement the Terraform code

> [!NOTE]

> The sample code for this article is located in the [Azure Terraform GitHub repo](https://github.com/Azure/terraform/tree/master/quickstart/101-front-door-standard-premium). You can view the log file containing the [test results from current and previous versions of Terraform](https://github.com/Azure/terraform/tree/master/quickstart/101-front-door-standard-premium/TestRecord.md).

>

> See more [articles and sample code showing how to use Terraform to manage Azure resources](/azure/terraform)

1. Create a directory in which to test the sample Terraform code and make it the current directory.

1. Create a file named `providers.tf` and insert the following code:

1. Create a file named `main.tf` and insert the following code:

1. Create a file named `app-service.tf` and insert the following code:

1. Create a file named `variables.tf` and insert the following code:

1. Create a file named `outputs.tf` and insert the following code:

## Initialize Terraform

[!INCLUDE [terraform-init.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-init.md)]

## Create a Terraform execution plan

[!INCLUDE [terraform-plan.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-plan.md)]

## Apply a Terraform execution plan

[!INCLUDE [terraform-apply-plan.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-apply-plan.md)]

## Verify the results

1. Get the Front Door endpoint:

```console

terraform output -raw frontDoorEndpointHostName

```

1. Paste the endpoint into a browser.

## Clean up resources

[!INCLUDE [terraform-plan-destroy.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-plan-destroy.md)]

## Troubleshoot Terraform on Azure

[Troubleshoot common problems when using Terraform on Azure](/azure/developer/terraform/troubleshoot)

## Next steps

> [!div class="nextstepaction"]

> [Overview of Azure Front Door](front-door-overview.md)


# Endpoint

# Endpoints in Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

In Azure Front Door, an *endpoint* is a logical grouping of one or more routes associated with domain names. Each endpoint is [assigned a domain name](#endpoint-domain-names) by Front Door, and you can also associate your own custom domains through routes.

## How many endpoints should I create?

A Front Door profile can contain multiple endpoints, but in many cases, a single endpoint is enough.

Consider the following factors when planning your endpoints:

- If all your domains use the same or similar route paths, it's likely best to combine them into a single endpoint.

- If you use different routes and route paths for each domain, consider creating separate endpoints, such as one for each custom domain.

- If you need to enable or disable all your domains together, consider using a single endpoint, as you can enable or disable an entire endpoint at once.

## Endpoint domain names

You automatically generate endpoint domain names when you create a new endpoint. Front Door generates a unique domain name based on several components, including:

- The endpoint's name.

- A pseudorandom hash value determined by Front Door, which helps protect against [subdomain takeover](../security/fundamentals/subdomain-takeover.md) attacks.

- The base domain name for your Front Door environment, generally `z01.azurefd.net`.

For example, if you create an endpoint named `myendpoint`, the endpoint domain name might be `myendpoint-mdjf2jfgjf82mnzx.z01.azurefd.net`.

You can access the endpoint domain when you associate it with a route.

### Reuse of an endpoint domain name

When you delete and redeploy an endpoint, you might expect to get the same pseudorandom hash value and, therefore, the same endpoint domain name. Front Door enables you to control how these pseudorandom hash values are reused on an endpoint-by-endpoint basis.

You can reuse an endpoint's domain within the same tenant, subscription, or resource group scope level. You can also choose to not allow the reuse of an endpoint domain. By default, Front Door allows reuse of the endpoint domain within the same Microsoft Entra tenant.

You can configure the scope level of the endpoint's domain reuse behavior using Bicep, an Azure Resource Manager (ARM) template, the Azure CLI, or Azure PowerShell. Additionally, you can configure it for all Front Door endpoints in your organization by using Azure Policy. The Azure portal uses the scope level you define through the command line once you change it.

The following table lists the allowable values for the endpoint's domain reuse behavior:

| Value | Description |

|--|--|

| `TenantReuse` | This value is the default. Endpoints with the same name in the same Microsoft Entra tenant receive the same domain label. |

| `SubscriptionReuse` | Endpoints with the same name in the same Azure subscription receive the same domain label. |

| `ResourceGroupReuse` | Endpoints with the same name in the same resource group receive the same domain label. |

| `NoReuse` | Endpoints always receive a new domain label. |

> [!NOTE]

> You can't modify the reuse behavior for an existing Front Door endpoint. It only applies to newly created endpoints.

The following examples demonstrate how to create a new Front Door endpoint with the reuse scope set to `SubscriptionReuse`:

### Azure CLI

```azurecli

az afd endpoint create \

--resource-group MyResourceGroup \

--profile-name MyProfile \

--endpoint-name myendpoint \

--name-reuse-scope SubscriptionReuse

```

### Azure PowerShell

```azurepowershell

New-AzFrontDoorCdnEndpoint `

-ResourceGroupName MyResourceGroup `

-ProfileName MyProfile `

-EndpointName myendpoint `

-Location global `

-AutoGeneratedDomainNameLabelScope SubscriptionReuse

```

### Bicep

```bicep

resource endpoint 'Microsoft.Cdn/profiles/afdEndpoints@2021-06-01' = {

name: endpointName

parent: profile

location: 'global'

properties: {

autoGeneratedDomainNameLabelScope: 'SubscriptionReuse'

}

}

```

---

## Next steps

* [Configure an origin](origin.md) for Azure Front Door.


# Manager

# What is Azure Front Door Manager?

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Azure Front Door Manager in Azure Front Door Standard and Premium provides an overview of the endpoints configured for your Azure Front Door profile. With Front Door Manager, you can manage your collection of endpoints, configure routing rules, domains, origin groups, and apply security policies to protect your web application.

## Routes within an Endpoint

An [*endpoint*](endpoint.md) is a logical grouping of one or more routes associated with domain names. A route contains the origin group configuration and routing rules between domains and origins. An endpoint can have one or more routes, and a route can have multiple domains but only one origin group. You need at least one configured route for traffic to route between your domains and the origin group.

> [!NOTE]

> * You can *enable* or *disable* an endpoint or a route.

> * Traffic will only flow to origins once both the endpoint and route are **enabled**.

Domains within a route can be either a custom domain or an endpoint domain. For more information about custom domains, see [create a custom domain](standard-premium/how-to-add-custom-domain.md) with Azure Front Door. Endpoint domains refer to the auto-generated domain name when you create a new endpoint. The name is a unique endpoint hostname with a hash value in the format of `endpointname-hash.z01.azurefd.net`. The endpoint domain is accessible if associated with a route.

## Security Policy in an Endpoint

A security policy is an association of one or more domains with a Web Application Firewall (WAF) policy. The WAF policy provides centralized protection for your web applications. If you manage security policies using the Azure portal, you can only associate a security policy with domains in the Routes configuration of that endpoint.

> [!TIP]

> * If one of your domains is unhealthy, select the domain to go to the domains page and take appropriate actions to troubleshoot the issue.

> * If you have a large Azure Front Door profile, review [**Azure Front Door service limits**](../azure-resource-manager/management/azure-subscription-service-limits.md#azure-front-door-standard-and-premium-service-limits) and [**Azure Front Door routing limits**](front-door-routing-limits.md) to better manage your Azure Front Door.

## Next steps

* Discover more about [endpoints](endpoint.md).

* Learn to [configure endpoints using Front Door Manager](how-to-configure-endpoints.md).

* Understand the Azure Front Door [routing architecture](front-door-routing-architecture.md).

* Find out [how traffic is matched to a route](front-door-routing-architecture.md) in Azure Front Door.


# How To Configure Endpoints

# Add a new endpoint with Front Door manager

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

This article shows you how to add a new endpoint to an existing Azure Front Door profile in the Front Door manager.

## Prerequisites

Before you can create a new endpoint with Front Door manager, you must have an Azure Front Door profile created. To create an Azure Front Door profile, see [create an Azure Front Door](create-front-door-portal.md). The profile must have at least one endpoint.

## Create a new Front Door endpoint

1. Sign in to the [Azure portal](https://portal.azure.com) and navigate to your Azure Front Door profile.

1. Select **Front Door manager** under *Settings* from the left side menu pane. Then select **+ Add an endpoint** to create a new endpoint.

1. On **Add an endpoint**, enter a unique name for the endpoint.

| Field                | Description                                                                                                                |

|----------------------|----------------------------------------------------------------------------------------------------------------------------|

| **Name**             | Enter a unique name for the new Front Door endpoint. Azure Front Door generates a unique endpoint hostname based on the endpoint name in the form of `<endpointname>-*.z01.azurefd.net`. |

| **Endpoint hostname**| A deterministic DNS (domain name system) name that helps prevent subdomain takeover. This name is used to access your resources through your Azure Front Door at the domain `<endpointname>-*.z01.azurefd.net`. |

| **Status**           | Set as checked to enable this endpoint.                                                                                    |

### Add a route

1. To add a new **route**, first expand an endpoint from the list of endpoints in the Front Door manager.

1. In the endpoint configuration pane, select **+ Add a route** to configure the mapping of your domains and routing configuration to your origin group.

1. On **Add a route**, enter or select the following information:

| Field | Description |

|--|--|

| **Name** | Enter a unique name for the new route. |

| **Enable route** | Select to enable this route. |

| **Domains** | Select one or more validated domains that aren't associated to another route. For more information, see [add a custom domain](standard-premium/how-to-add-custom-domain.md). |

| **Patterns to match** | Configure all URL path patterns that this route accepts. For example, set the pattern to match to `/images/*` to accept all requests on the URL `www.contoso.com/images/*`. Azure Front Door determines the traffic based on exact match first. If no paths match exactly, then Front Door looks for a wildcard path that matches. If no routing rules are found with a matching path, then the request gets rejected and returns a 400: Bad Request error HTTP response. Patterns to match paths aren't case sensitive, meaning paths with different casing are treated as duplicates. For example, you have a host using the same protocol with paths `/FOO` and `/foo`. These paths are considered duplicates, and aren't allowed in the *Patterns to match* field. |

| **Accepted protocols** | Specify the protocols you want Azure Front Door to accept when the client makes the request. You can specify HTTP, HTTPS, or both. |

| **Redirect** | Specify whether HTTPS is enforced for the incoming HTTP requests. |

| **Origin group** | Select the origin group to forward traffic to when requests are made to the origin. For more information, see [configure an origin group](standard-premium/how-to-create-origin.md). |

| **Origin path** | This path is used to rewrite the URL that Front Door uses when forwarding the request to the origin. By default, this path isn't provided, so Front Door uses the incoming URL path in the request to the origin. You can also specify a wildcard path, which copies any matching part of the incoming path to the request path to the origin. The origin path is case sensitive. |

| **Forwarding protocol** | Select the protocol used for forwarding request. You can specify HTTP only, HTTPS only, or match incoming request. |

| **Caching** | Select this option to enable caching of static content with Azure Front Door. For more information, see [caching with Front Door](front-door-caching.md). |

| **Rules** | Select rule sets that get applied to this route. For more information, see [rule sets for Front Door](front-door-rules-engine.md). |

1. Here's an example of how the *Origin path* field works:

| Field                | Description                |

|----------------------|----------------------------|

| **Pattern to match**     | `/foo/*`                     |

| **Origin path**          | `/fwd/`                     |

| **Incoming URL path**    | `/foo/a/b/c/`                |

| **URL from Front Door to origin** | `fwd/a/b/c`         |

1. Select **Add** to create the new route. The route appears in the list of routes for the endpoints.

### Add security policy

1. Select **+ Add a policy** in the *Security policy* pane to apply or create a new web application firewall policy to associate with your domains.

1. On **Add security policy**, enter or select the following information:

| Field                       | Description                                                                                                      |

|-----------------------------|------------------------------------------------------------------------------------------------------------------|

| **Name**                    | Enter a unique name within this Front Door profile for the security policy.                                       |

| **Domains**                 | Select one or more domains you want to apply this security policy to.                                             |

| **WAF (Web Application Firewall) Policy** | Select an existing or create a new WAF policy. When you select an existing WAF policy, it must be the same tier as the Front Door profile. For more information, see [configure WAF policy for Front Door](../web-application-firewall/afds/waf-front-door-create-portal.md). |

1. Select **Save** to create the security policy and associate it with the endpoint.

## Configure origin timeout

Origin timeout is the amount of time Azure Front Door waits until it considers the connection to origin valid. You can set this value on the overview page of the Azure Front Door profile. This value applies to all endpoints in the profile.

## Clean up resources

To remove an endpoint, first remove any security policies associated with the endpoint. Then select **Delete endpoint** to remove the endpoint from the Azure Front Door profile.

## Related content

* Learn about the use of [origins and origin groups](origin.md) in an Azure Front Door configuration.

* Learn about [rules match conditions](rules-match-conditions.md) in an Azure Front Door rule set.

* Learn more about [policy settings](../web-application-firewall/afds/waf-front-door-policy-settings.md) for WAF with Azure Front Door.

* Learn how to create [custom rules](../web-application-firewall/afds/waf-front-door-custom-rules.md) to protect your Azure Front Door profile.


# How To Add Custom Domain

# Configure a custom domain on Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

When you use Azure Front Door for application delivery, a custom domain lets your own domain name appear in user requests. This visibility can enhance customer convenience and support branding efforts.

By default, when you create an Azure Front Door Standard or Premium profile and endpoint, the endpoint host is a subdomain of `azurefd.net`. For example, the URL might look like `https://contoso-frontend-mdjf2jfgjf82mnzx.z01.azurefd.net/activeusers.htm`.

To make your URLs more user-friendly and branded, Azure Front Door allows you to associate a custom domain. You can deliver your content by using a custom domain in the URL, such as `https://www.contoso.com/photo.png`, instead of the default Azure Front Door domain.

## Prerequisites

- An Azure Front Door profile. For more information, see [Quickstart: Create an Azure Front Door Standard/Premium](create-front-door-portal.md).

- A custom domain. If you don't have a custom domain, you must first purchase one from a domain provider. For more information, see [Buy a custom domain name](/azure/app-service/manage-custom-dns-buy-domain?toc=/azure/frontdoor/TOC.json).

- If you're using Azure to host your DNS domains, you must delegate the domain provider's domain name system (DNS) to an Azure DNS. For more information, see [Delegate a domain to Azure DNS](/azure/dns/dns-delegate-domain-azure-dns?toc=/azure/frontdoor/TOC.json). Otherwise, if you're using a domain provider to handle your DNS domain, you must manually validate the domain by entering prompted DNS TXT records.

## Add a new custom domain

> [!NOTE]

> If you validate a custom domain in an Azure Front Door or Microsoft CDN profile, you can't add it to another profile.

To configure a custom domain, go to the **Domains** pane of your Azure Front Door profile. You can set up and validate a custom domain before associating it with an endpoint. You can only associate a custom domain and its subdomains with a single endpoint at a time. However, you can use different subdomains from the same custom domain for different Azure Front Door profiles. You can also map custom domains with different subdomains to the same Azure Front Door endpoint.

1. Under **Settings**, select **Domains** for your Azure Front Door profile. Then select **+ Add**.

1. On **Add a domain**, select the domain type. Choose **Non-Azure validated domain** or **Azure pre-validated domain**.

* **Non-Azure validated domain**: The domain requires ownership validation. Use the Azure-managed DNS option. You can also use your own DNS provider. If you choose Azure-managed DNS, select an existing DNS zone and either select an existing custom subdomain or create a new one. If you're using another DNS provider, manually enter the custom domain name. Then select **Add** to add your custom domain.

* **Azure pre-validated domain**: The domain is already validated by another Azure service, so domain ownership validation isn't required from Azure Front Door. A dropdown list of validated domains by different Azure services appear.

> [!NOTE]

> - Azure Front Door supports both Azure-managed certificates and Bring Your Own Certificates (BYOCs). For non-Azure validated domains, Azure-managed certificates are issued and managed by Azure Front Door. For Azure prevalidated domains, the Azure-managed certificate is issued and managed by the Azure service that validates the domain. To use your own certificate, see [Configure HTTPS on a custom domain](how-to-configure-https-custom-domain.md).

> - Azure Front Door supports Azure prevalidated domains and Azure DNS zones in different subscriptions.

> - Currently, Azure prevalidated domains only support domains validated by Azure Static Web Apps.

A new custom domain initially has a validation state of **Submitting**.

> [!NOTE]

> - As of September 2023, Azure Front Door supports BYOC-based domain ownership validation. Azure Front Door automatically approves domain ownership if the Certificate Name (CN) or Subject Alternative Name (SAN) of the provided certificate matches the custom domain. When you select **Azure managed certificate**, domain ownership continues to be validated via the DNS TXT record.

> - For custom domains created before BYOC-based validation support, if the domain validation status isn't **Approved**, trigger auto-approval by selecting **Validation State** > **Revalidate** in the portal. If you're using the command-line tool, trigger domain validation by sending an empty `PATCH` request to the domain API.

> - An Azure prevalidated domain has a validation state of **Pending**. It automatically changes to **Approved** after a few minutes. Once approved, proceed to [Associate the custom domain with your Front Door endpoint](#associate-the-custom-domain-with-your-azure-front-door-endpoint) and complete the remaining steps.

After a few minutes, the validation state changes to **Pending**.

1. Select the **Pending** validation state. A new pane appears with the DNS TXT record information required to validate the custom domain. The TXT record is in the format `_dnsauth.<your_subdomain>`.

- If you're using an Azure DNS-based zone, select **Add** to create a new TXT record with the provided value in the Azure DNS zone.

- If you're using another DNS provider, manually create a new TXT record named `_dnsauth.<your_subdomain>` with the value shown on the pane.

1. Close the pane to return to the custom domains list. The provisioning state of the custom domain changes to **Provisioned**, and the validation state changes to **Approved**.

For more information about domain validation states, see [Domains in Azure Front Door](../domain.md#domain-validation).

## Associate the custom domain with your Azure Front Door endpoint

After validating your custom domain, you can associate it with your Azure Front Door Standard or Premium endpoint.

1. Select the **Unassociated** link to open the **Associate endpoint and routes** pane. Select the endpoint and routes you want to associate with the domain, and then select **Associate** to update your configuration.

The **Endpoint association** status updates to reflect the endpoint currently associated with the custom domain.

1. Select the **DNS state** link.

> [!NOTE]

> For an Azure prevalidated domain, manually update the CNAME record from the other Azure service endpoint to the Azure Front Door endpoint in your DNS hosting service. This step is required regardless of whether the domain is hosted with Azure DNS or another DNS service. The link to update the CNAME from the **DNS state** column isn't available for this type of domain.

1. The **Add or update the CNAME record** pane appears with the necessary CNAME record information. If you're using Azure DNS hosted zones, you can create the CNAME records by selecting **Add** on the pane. If you're using another DNS provider, manually enter the CNAME record name and value as shown on the pane.

1. After you create the CNAME record and associate the custom domain with the Azure Front Door endpoint, traffic starts flowing.

> [!NOTE]

> - If you enable HTTPS, certificate provisioning and propagation might take a few minutes as it propagates to all edge locations.

> - If your domain CNAME indirectly points to an Azure Front Door endpoint, such as through Azure Traffic Manager for multi-CDN failover, the **DNS state** column might show **CNAME/Alias record currently not detected**. Azure Front Door can't guarantee 100% detection of the CNAME record in this scenario. If you configured an Azure Front Door endpoint to Traffic Manager and still see this message, it doesn't necessarily mean there's an issue with your setup. No further action is required.

## Verify the custom domain

After validating and associating the custom domain, make sure the custom domain correctly references your endpoint.

Finally, verify that your application content is served by using a browser.

## Related content

- [Enable HTTPS on your custom domain](how-to-configure-https-custom-domain.md)

- [Custom domains in Azure Front Door](../domain.md)

- [End-to-end TLS with Azure Front Door](../end-to-end-tls.md)


# How To Configure Https Custom Domain

# Configure HTTPS on an Azure Front Door custom domain

Azure Front Door enables secure Transport Layer Security (TLS) delivery to your applications by default when you use your own custom domains. To learn more about custom domains, including how custom domains work with HTTPS, see [Domains in Azure Front Door](../domain.md).

Azure Front Door supports Azure-managed certificates and customer-managed certificates. In this article, you learn how to configure both types of certificates for your Azure Front Door custom domains.

## Prerequisites

- An Azure Front Door profile. For more information, see [Quickstart: Create an Azure Front Door Standard/Premium](create-front-door-portal.md).

- A custom domain. If you don't have a custom domain, you must first purchase one from a domain provider. For more information, see [Buy a custom domain name](/azure/app-service/manage-custom-dns-buy-domain?toc=/azure/frontdoor/TOC.json).

- If you're using Azure to host your [DNS domains](../../dns/dns-overview.md), you must delegate the domain provider's domain name system (DNS) to an Azure DNS. For more information, see [Delegate a domain to Azure DNS](../../dns/dns-delegate-domain-azure-dns.md?toc=/azure/frontdoor/TOC.json). Otherwise, if you're using a domain provider to handle your DNS domain, you must manually validate the domain by entering prompted DNS TXT records.

## Azure Front Door-managed certificates for non-Azure prevalidated domains

If you have your own domain and the domain isn't already associated with [another Azure service that prevalidates domains for Azure Front Door](../domain.md#domain-validation), follow these steps:

1. Under **Settings**, select **Domains** for your Azure Front Door profile. Then select **+ Add** to add a new domain.

1. On **Add a domain**, enter or select the following information. Then select **Add** to onboard the custom domain.

| Setting | Value |

|--|--|

| Domain type | Select **Non-Azure pre-validated domain**. |

| DNS management | Select **Azure managed DNS (Recommended)**. |

| DNS zone | Select the Azure DNS zone that hosts the custom domain. |

| Custom domain | Select an existing domain or add a new domain. |

| HTTPS | Select **AFD managed (Recommended)**. |

1. Validate and associate the custom domain to an endpoint by following the steps to enable a [custom domain](how-to-add-custom-domain.md).

1. After you associate the custom domain with an endpoint, Azure Front Door generates a certificate and deploys it. This process might take several minutes to an hour.

## Azure-managed certificates for Azure prevalidated domains

If you have your own domain and associate it with [another Azure service that prevalidates domains for Azure Front Door](../domain.md#domain-validation), follow these steps:

1. Under **Settings**, select **Domains** for your Azure Front Door profile. Then select **+ Add** to add a new domain.

1. On **Add a domain**, enter or select the following information. Then select **Add** to onboard the custom domain.

| Setting | Value |

|--|--|

| Domain type | Select **Azure pre-validated domain**. |

| Pre-validated custom domains | Select a custom domain name from the dropdown list of Azure services. |

| HTTPS | Select **Azure managed**. |

1. Validate and associate the custom domain to an endpoint by following the steps to enable a [custom domain](how-to-add-custom-domain.md).

1. After the custom domain is successfully associated with an endpoint, an Azure Front Door-managed certificate gets deployed to Azure Front Door. This process might take from several minutes to an hour to finish.

## Use your own certificate

You can also choose to use your own TLS certificate. Your TLS certificate must meet certain requirements. For more information, see [Certificate requirements](../domain.md?pivot=front-door-standard-premium#certificate-requirements).

#### Prepare your key vault and certificate

Create a separate Azure Key Vault instance in which you store your Azure Front Door TLS certificates. For more information, see [Create a Key Vault instance](/azure/key-vault/general/quick-create-portal). If you already have a certificate, you can upload it to your new Key Vault instance. Otherwise, you can create a new certificate through Key Vault from one of the certificate authority (CA) partners.

Currently, two methods authenticate Azure Front Door to access your Key Vault:

- **Managed identity**: Azure Front Door uses a managed identity to authenticate to your Key Vault. Use this method because it's more secure and doesn't require you to manage credentials. For more information, see [Use managed identities in Azure Front Door](../managed-identity.md). If you're using this method, see [Select the certificate for Azure Front Door to deploy](#select-the-certificate-for-azure-front-door-to-deploy).

- **App registration**: Azure Front Door uses an app registration to authenticate to your Key Vault. This method is being deprecated and will be retired in the future. For more information, see [Use app registration in Azure Front Door](#register-azure-front-door).

> [!WARNING]

> - Azure Front Door currently only supports Key Vault in the same subscription. Selecting Key Vault under a different subscription results in a failure.

> - Azure Front Door doesn't support certificates with elliptic curve cryptography algorithms. Also, your certificate must have a complete certificate chain with leaf and intermediate certificates. The root CA also must be part of the [Microsoft Trusted CA List](https://ccadb.my.salesforce-sites.com/microsoft/IncludedCACertificateReportForMSFT).

#### Register Azure Front Door

Register the service principal for Azure Front Door as an app in your Microsoft Entra ID using Microsoft Graph PowerShell or the Azure CLI.

> [!NOTE]

> - This action requires you to have User Access Administrator permissions in Microsoft Entra ID. The registration only needs to be performed *once per Microsoft Entra tenant*.

> - The application IDs of **205478c0-bd83-4e1b-a9d6-db63a3e1e1c8** and **d4631ece-daab-479b-be77-ccb713491fc0** are predefined by Azure for Azure Front Door Standard and Premium across all Azure tenants and subscriptions. Azure Front Door (classic) has a different application ID.

# [Microsoft Graph PowerShell](#tab/powershell)

1. If needed, install [Microsoft Graph PowerShell](/powershell/microsoftgraph/installation) in PowerShell on your local machine.

1. Use PowerShell to run the following command:

Azure public cloud:

```azurepowershell-interactive

New-MgServicePrincipal -AppId '205478c0-bd83-4e1b-a9d6-db63a3e1e1c8'

```

Azure Government cloud:

```azurepowershell-interactive

New-MgServicePrincipal -AppId 'd4631ece-daab-479b-be77-ccb713491fc0'

```

# [Azure CLI](#tab/cli)

1. If needed, install the [Azure CLI](/cli/azure/install-azure-cli) on your local machine.

1. Use the Azure CLI to run the following command:

Azure public cloud:

```azurecli-interactive

az ad sp create --id 205478c0-bd83-4e1b-a9d6-db63a3e1e1c8

```

Azure Government cloud:

```azurecli-interactive

az ad sp create --id d4631ece-daab-479b-be77-ccb713491fc0

```

---

#### Grant Azure Front Door access to your key vault

Grant Azure Front Door permission to access the certificates in the new Key Vault account that you created specifically for Azure Front Door. You only need to give `GET` permission to the certificate and secret in order for Azure Front Door to retrieve the certificate.

1. In your Key Vault account, select **Access policies**.

1. Select **Add new** or **Create** to create a new access policy.

1. In **Secret permissions**, select **Get** to allow Azure Front Door to retrieve the certificate.

1. In **Certificate permissions**, select **Get** to allow Azure Front Door to retrieve the certificate.

1. In **Select principal**, search for **205478c0-bd83-4e1b-a9d6-db63a3e1e1c8** and select **Microsoft.AzureFrontDoor-Cdn**. Select **Next**.

1. In **Application**, select **Next**.

1. In **Review + create**, select **Create**.

> [!NOTE]

> If your key vault is protected with network access restrictions, make sure to allow trusted Microsoft services to access your key vault.

Azure Front Door can now access this key vault and the certificates it contains.

#### Select the certificate for Azure Front Door to deploy

1. Return to your Azure Front Door Standard/Premium in the portal.

1. Under **Security**, go to **Secrets** and select **+ Add certificate**.

1. On the **Add certificate** pane, select the checkbox for the certificate you want to add to Azure Front Door Standard/Premium.

1. When you select a certificate, you must [select the certificate version](../domain.md#rotate-own-certificate). If you select **Latest**, Azure Front Door automatically updates whenever the certificate is rotated (renewed). You can also select a specific certificate version if you prefer to manage certificate rotation yourself.

Leave the version selection as **Latest** and select **Add**.

1. After the certificate gets provisioned successfully, you can use it when you add a new custom domain.

1. Under **Settings**, go to **Domains** and select **+ Add** to add a new custom domain. On the **Add a domain** pane, for **HTTPS**, select **Bring Your Own Certificate (BYOC)**. For **Secret**, select the certificate you want to use from the dropdown list.

> [!NOTE]

> The Certificate Name (CN) or Subject Alternative Name (SAN) of the certificate must match the custom domain being added.

1. Follow the onscreen steps to validate the certificate. Then associate the newly created custom domain to an endpoint as outlined in [Configure a custom domain](how-to-add-custom-domain.md).

## Switch between certificate types

You can change a domain between using an Azure Front Door-managed certificate and a customer-managed certificate. For more information, see [Domains in Azure Front Door](../domain.md#switch-between-certificate-types).

1. Select the certificate state to open the **Certificate details** pane.

1. On the **Certificate details** pane, you can change between **Azure Front Door managed** and **Bring Your Own Certificate (BYOC)**.

If you select **Bring Your Own Certificate (BYOC)**, follow the preceding steps to select a certificate.

1. Select **Update** to change the associated certificate with a domain.

## Related content

- [Caching with Azure Front Door](../front-door-caching.md)

- [Custom domains in Azure Front Door](../domain.md)

- [End-to-end TLS with Azure Front Door](../end-to-end-tls.md)


# Apex Domain

# Apex domains in Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Apex domains, also called *root domains*, or *naked domains*, are at the root of a Domain Name System (DNS) zone and don't contain subdomains. For example, `contoso.com` is an apex domain.

Azure Front Door supports apex domains, but requires special considerations. This article describes how apex domains work in Azure Front Door.

To add a root or apex domain to your Azure Front Door profile, see [Onboard a root or apex domain on your Azure Front Door profile](front-door-how-to-onboard-apex-domain.md).

## DNS CNAME flattening

The DNS protocol prevents the assignment of CNAME records at the zone apex. For example, if your domain is `contoso.com`, you can create a CNAME record for `myapplication.contoso.com`, but you can't create a CNAME record for `contoso.com` itself.

Azure Front Door doesn't expose the frontend public IP address associated with your Azure Front Door endpoint. So, you can't map an apex domain to an Azure Front Door IP address.

> [!WARNING]

> Don't create an A record with the public IP address of your Azure Front Door endpoint. Your Azure Front Door endpoint's public IP address might change and we don't provide any guarantees that it will remain the same.

However, this problem can be resolved by using alias records in Azure DNS. Unlike CNAME records, alias records are created at the zone apex. You can point a zone apex record to an Azure Front Door profile that has public endpoints. Multiple application owners can point to the same Azure Front Door endpoint used for any other domain within their DNS zone. For example, `contoso.com` and `www.contoso.com` can point to the same Azure Front Door endpoint.

Mapping your apex or root domain to your Azure Front Door profile uses *CNAME flattening*, sometimes called *DNS chasing*. CNAME flattening is where a DNS provider recursively resolves CNAME entries until it resolves an IP address. Azure DNS supports this functionality for Azure Front Door endpoints.

> [!NOTE]

> Other DNS providers support CNAME flattening or DNS chasing. However, Azure Front Door recommends using Azure DNS for hosting your apex domains.

## TXT record validation

To validate a domain, you need to create a DNS TXT record. The name of the TXT record must be of the form `_dnsauth.{subdomain}`. Azure Front Door provides a unique value for your TXT record when you start to add the domain to Azure Front Door.

For example, suppose you want to use the apex domain `contoso.com` with Azure Front Door. First, you should add the domain to your Azure Front Door profile, and note the TXT record value that you need to use. Then, you should configure a DNS record with the following properties:

| Property | Value |

|--|--|

| Record name | `_dnsauth` |

| Record value | *use the value provided by Azure Front Door* |

| Time to live (TTL) | 1 hour |

## Azure Front Door-managed TLS certificate rotation

When you use an Azure Front Door-managed certificate, Azure Front Door attempts to automatically rotate (renew) the certificate. Before it does so, Azure Front Door checks whether the DNS CNAME record is still pointed to the Azure Front Door endpoint. Apex domains don't have a CNAME record pointing to an Azure Front Door endpoint, so the autorotation for managed certificate fails until the domain ownership is revalidated.

Select the **Pending revalidation** link and then select the **Regenerate** button to regenerate the TXT token. After that, add the TXT token to the DNS provider settings.

> [!NOTE]

> Azure Front Door's DNS TXT records for domain name validation need to be updated when the certificate is renewed. When you see the *Pending revalidation* domain validation state, ensure that you generate a new TXT record and update your DNS server.

## Next steps

To add a root or apex domain to your Azure Front Door profile, see [Onboard a root or apex domain on your Azure Front Door profile](front-door-how-to-onboard-apex-domain.md).


# Front Door How To Onboard Apex Domain

# Onboard a root or apex domain to Azure Front Door

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

Azure Front Door uses CNAME records to validate domain ownership for the onboarding of custom domains. Azure Front Door doesn't expose the front-end IP address associated with your Azure Front Door profile. So, you can't map your apex domain to an IP address if your intent is to onboard it to Azure Front Door.

The Domain Name System (DNS) protocol prevents the assignment of CNAME records at the zone apex. For example, if your domain is `contoso.com`, you can create CNAME records for `somelabel.contoso.com`, but you can't create a CNAME record for `contoso.com` itself. This restriction presents a problem for application owners who load balance applications behind Azure Front Door. Because using an Azure Front Door profile requires creation of a CNAME record, it isn't possible to point at the Azure Front Door profile from the zone apex.

You can resolve this problem by using alias records in Azure DNS. Unlike CNAME records, alias records are created at the zone apex. Application owners can use it to point their zone apex record to an Azure Front Door profile that has public endpoints. Application owners can point to the same Azure Front Door profile used for any other domain within their DNS zone. For example, `contoso.com` and `www.contoso.com` can point to the same Azure Front Door profile.

Mapping your apex or root domain to your Azure Front Door profile requires *CNAME flattening* or *DNS chasing*, which is when the DNS provider recursively resolves CNAME entries until it resolves an IP address. Azure DNS supports this functionality for Azure Front Door endpoints.

> [!NOTE]

> Other DNS providers support CNAME flattening or DNS chasing. However, Azure Front Door recommends using Azure DNS for its customers for hosting their domains.

You can use the Azure portal to onboard an apex domain on your Azure Front Door and enable HTTPS on it by associating it with a Transport Layer Security (TLS) certificate. Apex domains are also referred to as *root* or *naked* domains.

Apex domains are at the root of a DNS zone and don't contain subdomains. For example, `contoso.com` is an apex domain. Azure Front Door supports adding apex domains when you use Azure DNS. For more information about apex domains, see [Domains in Azure Front Door](domain.md).

You can use the Azure portal to onboard an apex domain on your Azure Front Door profile, and you can enable HTTPS on it by associating it with a TLS certificate.

## Onboard the custom domain to your Azure Front Door profile

1. Under **Settings**, select **Domains** for your Azure Front Door profile. Then select **+ Add** to add a new custom domain.

1. On the **Add a domain** pane, you enter information about the custom domain. You can choose Azure-managed DNS (recommended), or you can choose to use your DNS provider.

- **Azure-managed DNS**: Select an existing DNS zone. For **Custom domain**, select **Add new**. Select **APEX domain** from the pop-up. Then select **OK** to save.

- **Another DNS provider**: Make sure the DNS provider supports CNAME flattening and follow the steps for [adding a custom domain](standard-premium/how-to-add-custom-domain.md#add-a-new-custom-domain).

1. Select the **Pending** validation state. A new pane appears with the DNS TXT record information needed to validate the custom domain. The TXT record is in the form of `_dnsauth.<your_subdomain>`.

- **Azure DNS-based zone**: Select **Add** to create a new TXT record with the value that appears in the Azure DNS zone.

- If you're using another DNS provider, manually create a new TXT record with the name `_dnsauth.<your_subdomain>` with the record value as shown on the pane.

1. Close the **Validate the custom domain** pane and return to the **Domains** pane for the Azure Front Door profile. You should see **Validation state** change from **Pending** to **Approved**. If not, wait up to 10 minutes for changes to appear. If your validation doesn't get approved, make sure your TXT record is correct and that name servers are configured correctly if you're using Azure DNS.

1. Select **Unassociated** from the **Endpoint association** column to add the new custom domain to an endpoint.

1. On the **Associate endpoint and route** pane, select the endpoint and route to which you want to associate the domain. Then select **Associate**.

1.	Under the **DNS state** column, select **CNAME record is currently not detected** to add the alias record to the DNS provider.

- **Azure DNS**: Select **Add**.

- **A DNS provider that supports CNAME flattening**: You must manually enter the alias record name.

1. After the alias record gets created and the custom domain is associated with the Azure Front Door endpoint, traffic starts flowing.

> [!NOTE]

> * The **DNS state** column is used for CNAME mapping check. An apex domain doesn't support a CNAME record, so the DNS state shows **CNAME record is currently not detected** even after you add the alias record to the DNS provider.

> * When you place a service like an Azure Web App behind Azure Front Door, you need to configure the web app with the same domain name as the root domain in Azure Front Door. You also need to configure the back-end host header with that domain name to prevent a redirect loop.

> * Apex domains don't have CNAME records pointing to the Azure Front Door profile. Managed certificate autorotation always fails unless domain validation is finished between rotations.

> * The **Microsoft.Network** resource provider is required to create alias records.

## Enable HTTPS on your custom domain

Follow the guidance for [configuring HTTPS for your custom domain](standard-premium/how-to-configure-https-custom-domain.md) to enable HTTPS for your apex domain.

## Create an alias record for zone apex

1. Open **Azure DNS** configuration for the domain to be onboarded.

1. Create or edit the record for zone apex.

1. Select the record type as **A**. For **Alias record set**, select **Yes**. Set **Alias type** to **Azure resource**.

1. Select the Azure subscription that contains your Azure Front Door profile. Then select the Azure Front Door resource from the **Azure resource** dropdown list.

1. Select **OK** to submit your changes.

1. The preceding step creates a zone apex record that points to your Azure Front Door resource. It also creates a CNAME record mapping **afdverify** (for example, `afdverify.contosonews.com`) that's used for onboarding the domain on your Azure Front Door profile.

## Onboard the custom domain on your Azure Front Door

1. On the Azure Front Door designer tab, select the **+** icon on the **Frontend hosts** section to add a new custom domain.

1. Enter the root or apex domain name in the **Custom host name** field. An example is `contosonews.com`.

1. After the CNAME mapping from the domain to your Azure Front Door is validated, select **Add** to add the custom domain.

1. Select **Save** to submit the changes.

## Enable HTTPS on your custom domain

1. Select the custom domain that was added. Under the section **Custom domain HTTPS**, change the status to **Enabled**.

1. For **Certificate management type**, select **Use my own certificate**.

> [!WARNING]

> An Azure Front Door-managed certificate management type isn't currently supported for apex or root domains. The only option available for enabling HTTPS on an apex or root domain for Azure Front Door is to use your own custom TLS/SSL certificate hosted on Azure Key Vault.

1. Ensure that you set up the right permissions for Azure Front Door to access your key vault, as noted in the UI, before you proceed to the next step.

1. Choose a **Key Vault account** from your current subscription. Then select the appropriate **Secret** and **Secret version** to map to the right certificate.

1. Select **Update** to save the selection. Then select **Save**.

1. Select **Refresh** after a couple of minutes. Then select the custom domain again to see the progress of certificate provisioning.

> [!WARNING]

> Ensure that you created appropriate routing rules for your apex domain or added the domain to existing routing rules.

## Related content

- Learn how to [create an Azure Front Door profile](quickstart-create-front-door.md)

- Learn [how Azure Front Door works](front-door-routing-architecture.md)


# Front Door Wildcard Domain

# Wildcard domains in Azure Front Door

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

Wildcard domains allow Azure Front Door to receive traffic for any subdomain of a top-level domain. An example wildcard domain is `*.contoso.com`.

By using wildcard domains, you can simplify the configuration of your Azure Front Door profile. You don't need to modify the configuration to add or specify each subdomain separately. For example, you can define the routing for `customer1.contoso.com`, `customer2.contoso.com`, and `customerN.contoso.com` by using the same route and adding the wildcard domain `*.contoso.com`.

Wildcard domains give you several advantages, including:

- You don't need to onboard each subdomain in your Azure Front Door profile. For example, suppose you create new subdomains every customer, and route all customers' requests to a single origin group. Whenever you add a new customer, Azure Front Door understands how to route traffic to your origin group even though the subdomain isn't explicitly configured.

- You don't need to generate a new Transport Layer Security (TLS) certificate, or manage any subdomain-specific HTTPS settings, to bind a certificate for each subdomain.

- You can use a single web application firewall (WAF) policy for all of your subdomains.

Commonly, wildcard domains are used to support software as a service (SaaS) solutions, and other multitenant applications. When you build these application types, you need to give special consideration to how you route traffic to your origin servers. For more information, see [Use Azure Front Door in a multitenant solution](/azure/architecture/guide/multitenant/service/front-door).

> [!NOTE]

> When you use Azure DNS to manage your domain's DNS records, you need to configure wildcard domains by using the Azure Resource Manager API, Bicep, PowerShell, and the Azure CLI. Support for adding and managing Azure DNS wildcard domains in the Azure portal isn't available.

## Add a wildcard domain and certificate binding

You can add a wildcard domain by following steps similar to those for subdomains. For more information about adding a subdomain to Azure Front Door, see [Configure a custom domain on Azure Front Door using the Azure portal](standard-premium/how-to-add-custom-domain.md).

> [!NOTE]

> - Azure DNS supports wildcard records.

> - You can't [purge the Azure Front Door cache](front-door-caching.md#cache-purge) for a wildcard domain. You must specify a subdomain when purging the cache.

To accept HTTPS traffic on your wildcard domain, you must enable HTTPS on the wildcard domain. The certificate binding for a wildcard domain requires a wildcard certificate. That is, the subject name of the certificate should also have the wildcard domain.

> [!NOTE]

> - You can choose to use the same wildcard certificate from Azure Key Vault or from Azure Front Door managed certificates for subdomains.

> - If you want to add a subdomain of the wildcard domain that’s already validated in the Azure Front Door Standard or Premium profile, the domain validation is automatically approved. This condition applies to Bring Your Own Certificate. Domain ownership is required for managed certificate for subdomains.

> - If a wildcard domain is validated and already added to one profile, a single-level subdomain can still be added to another profile as long as it's also validated.

## Define a subdomain explicitly

You can add as many single-level subdomains of the wildcard as you want. For example, for the wildcard domain `*.contoso.com`, you can also add subdomains to your Azure Front Door profile for `image.contoso.com`, `cart.contoso.com`, and so forth. The configuration that you explicitly specify for the subdomain takes precedence over the configuration of the wildcard domain.

You might need to explicitly add subdomains in these situations:

- You need to define a different route for a subdomain than the rest of the domains (from the wildcard domain). For example, your customers might use subdomains like `customer1.contoso.com`, `customer2.contoso.com`, and so forth, and these subdomains should all be routed to your main application servers. However, you might also want to route `images.contoso.com` to an Azure Storage blob container.

- You need to use a different WAF policy for a specific subdomain.

Subdomains like `www.image.contoso.com` aren't a single-level subdomain of `*.contoso.com`.

## Adding wildcard domains

You can add a wildcard domain under the section for front-end hosts or domains. Similar to subdomains, Azure Front Door (classic) validates that there's CNAME record mapping for your wildcard domain. This Domain Name System (DNS) mapping can be a direct CNAME record mapping like `*.contoso.com` mapped to `endpoint.azurefd.net`. Or you can use *afdverify* temporary mapping. For example, `afdverify.contoso.com` mapped to `afdverify.endpoint.azurefd.net` validates the CNAME record map for the wildcard.

> [!NOTE]

> Azure DNS supports wildcard records.

You can add as many single-level subdomains of the wildcard domain in front-end hosts, up to the limit of the front-end hosts. This functionality might be required for:

- Defining a different route for a subdomain than the rest of the domains (from the wildcard domain).

- Having a different WAF policy for a specific subdomain. For example, `*.contoso.com` allows adding `foo.contoso.com` without having to again prove domain ownership. But it doesn't allow `foo.bar.contoso.com` because it isn't a single level subdomain of `*.contoso.com`. To add `foo.bar.contoso.com` without extra domain ownership validation, `*.bar.contoso.com` needs to be added.

You can add wildcard domains and their subdomains with certain limitations:

- If you add a wildcard domain to an Azure Front Door (classic) profile:

- You can't add the wildcard domain to any other Azure Front Door (classic) profile.

- You can't add first-level subdomains of the wildcard domain to another Azure Front Door (classic) profile or an Azure Content Delivery Network profile.

- If you already added a subdomain of a wildcard domain to an Azure Front Door (classic) profile or an Azure Content Delivery Network profile, you can't use the wildcard domain for other Azure Front Door (classic) profile.

- If two profiles (Azure Front Door or Azure Content Delivery Network) have various subdomains of a root domain, you can't add wildcard domains to either of the profiles.

## Certificate binding

To accept HTTPS traffic on your wildcard domain, you must enable HTTPS on the wildcard domain. The certificate binding for a wildcard domain requires a wildcard certificate. That is, the subject name of the certificate should also have the wildcard domain.

> [!NOTE]

> Currently, you can enable HTTPS for wildcard domains only by using your own custom SSL certificate. You can't use Azure Front Door managed certificates for wildcard domains.

You can choose to use the same wildcard certificate from Azure Key Vault or from Azure Front Door managed certificates for subdomains.

If you add a subdomain for a wildcard domain that already has a certificate associated with it, you can't disable HTTPS for the subdomain. The subdomain uses the certificate binding for the wildcard domain, unless a different Key Vault or Azure Front Door managed certificate overrides it.

## WAF policies

You can attach WAF policies to wildcard domains, just like other domains. You can apply a different WAF policy to a subdomain of a wildcard domain. Subdomains automatically inherit the WAF policy from the wildcard domain if you don't associate an explicit WAF policy to the subdomain. However, if you add the subdomain to a different profile from the wildcard domain profile, the subdomain can't inherit the WAF policy associated with the wildcard domain.

You can attach WAF policies to wildcard domains, just like other domains. You can apply a different WAF policy to a subdomain of a wildcard domain. For the subdomains, you must specify the WAF policy to use even if it's the same policy as the wildcard domain. Subdomains *don't* automatically inherit the WAF policy from the wildcard domain.

If you don't want a WAF policy to run for a subdomain, you can create an empty WAF policy with no managed or custom rulesets.

## Routes

When you configure a route, select a wildcard domain as an origin. You can also set different route behavior for wildcard domains and subdomains. Azure Front Door chooses the most specific match for the domain across different routes. For more information, see [How requests are matched to a routing rule](front-door-route-matching.md).

> [!IMPORTANT]

> You must use matching path patterns across your routes, or your clients see failures.

>

> For example, suppose you have two routing rules:

> - Route 1 (`*.foo.com/*` mapped to origin group A).

> - Route 2 (`bar.foo.com/somePath/*` mapped to origin group B). <br>

> If a request arrives for `bar.foo.com/anotherPath/*`, Azure Front Door selects route 2 based on a more specific domain match, but it finds no matching path patterns across the routes.

## Routing rules

When you configure a routing rule, select a wildcard domain as a front-end host. You can set different route behavior for wildcard domains and subdomains. Azure Front Door chooses the most specific match for the domain across different routes. For more information, see [How requests are matched to a routing rule](front-door-route-matching.md).

> [!IMPORTANT]

> You must use matching path patterns across your routes, or your clients see failures.

>

> For example, suppose you have two routing rules:

> - Route 1 (`*.foo.com/*` mapped to backend pool A).

> - Route 2 (`bar.foo.com/somePath/*` mapped to backend pool B). <br>

> If a request arrives for `bar.foo.com/anotherPath/*`, Azure Front Door selects route 2 based on a more specific domain match, but it finds no matching path patterns across the routes.

## Related content

- Learn how to [create an Azure Front Door profile](create-front-door-portal.md).

- Learn how to [add a custom domain](standard-premium/how-to-add-custom-domain.md) to your Azure Front Door.

- Learn how to [enable HTTPS on a custom domain](standard-premium/how-to-configure-https-custom-domain.md).

- Learn how to [create an Azure Front Door profile](quickstart-create-front-door.md).

- Learn how to [add a custom domain](front-door-custom-domain.md) to your Azure Front Door.

- Learn how to [enable HTTPS on a custom domain](front-door-custom-domain-https.md).


# Front Door Rules Engine

# What is a rule set in Azure Front Door?

A rule set is a customized rules engine that groups a combination of rules into a single set. You can associate a rule set with multiple routes. A Rule set allows you to customize how requests get processed and handled at the Azure Front Door edge.

## Common supported scenarios

* Implementing security headers to prevent browser-based vulnerabilities like HTTP Strict-Transport-Security (HSTS), X-XSS-Protection, Content-Security-Policy, X-Frame-Options, and Access-Control-Allow-Origin headers for Cross-Origin Resource Sharing (CORS) scenarios. Security-based attributes can also be defined with cookies.

* Route requests to mobile or desktop versions of your application based on the client device type.

* Using redirect capabilities to return 301, 302, 307, and 308 redirects to the client to direct them to new hostnames, paths, query strings, or protocols.

* Dynamically modify the caching configuration of your route based on the incoming requests.

* Rewrite the request URL path and forwards the request to the appropriate origin in your configured origin group.

* Add, modify, or remove request/response header to hide sensitive information or capture important information through headers.

* Support server variables to dynamically change the request header, response headers, or URL rewrite paths/query strings. For example, when a new page load or when a form gets posted. Server variable is currently supported in **[rule set actions](front-door-rules-engine-actions.md)** only.

* Populate or modify a response header based on a request header value (e.g., adding the same FQDN in Access-Control-Allow-Origin as the request Origin header).

* Rename a response header generated by a cloud provider to a brand-specific one by adding a new response header and deleting the original.

* Redirect to a destination host using a value captured from an incoming query string key/value pair in format of {http_req_arg_key1}.

* Leverage URL path segment capture in URL redirect and rewrite, e.g. extract tenantID from your incoming URL path `/abc/<tenantID>/<otherID>/index.html` and insert elsewhere in the URL path by using "{url_path:seg1}" in the destination.

## Architecture

Rule sets handle requests at the Front Door edge. When a request arrives at your Front Door endpoint, WAF (Web Application Firewall) is processed first, followed by the settings configured in route. Those settings include the rule set associated to the route. Rule sets are processed in the order they appear under the routing configuration. Rules in a rule set also get processed in the order they appear. In order for all the actions in each rule to run, all the match conditions within a rule have to be met. If a request doesn't match any of the conditions in your rule set configuration, then only the default route settings get applied.

If the **Stop evaluating remaining rules** is selected, then any remaining rule sets associated with the route don't get ran.

### Example

In the following diagram, WAF policies get processed first. Then the rule set configuration appends a response header. The header changes the max-age of the cache control if the match condition is true.

## Terminology

With a Front Door rule set, you can create any combination of configurations, each composed of a set of rules. The following out lines some helpful terminologies you come across when configuring your rule set.

* *Rule set*: A set of rules that gets associated to one or multiple [routes](front-door-route-matching.md).

* *Rule set rule*: A rule composed of up to 10 match conditions and 5 actions. Rules are local to a rule set and can't be exported to use across other rule sets. You can create the same rule in different rule sets.

* *Match condition*: There are many match conditions that you can configure to parse an incoming request. A rule can contain up to 10 match conditions. Match conditions are evaluated with an **AND** operator. *Regular expression is supported in conditions*. A full list of match conditions can be found in [Rule set match conditions](rules-match-conditions.md).

* *Action*: An action dictates how Front Door handles the incoming requests based on the matching conditions. You can modify caching behaviors, modify request headers, response headers, set URL rewrite, and URL redirection. *Server variables are supported with Action*. A rule can contain up to five actions. A full list of actions can be found in [Rule set actions](front-door-rules-engine-actions.md).

## ARM template support

Rule sets can be configured using Azure Resource Manager templates. For an example, see [Front Door Standard/Premium with rule set](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium-rule-set). You can customize the behavior by using the JSON or Bicep snippets included in the documentation examples for [match conditions](rules-match-conditions.md) and [actions](front-door-rules-engine-actions.md).

## Limitations

For information about quota limits, refer to [Front Door limits, quotas, and constraints](../azure-resource-manager/management/azure-subscription-service-limits.md#azure-front-door-standard-and-premium-service-limits).

## Next steps

* Learn how to [create an Azure Front Door profile](create-front-door-portal.md).

* Learn how to configure your first [rule set](standard-premium/how-to-configure-rule-set.md).

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

A Rules engine configuration allows you to customize how HTTP requests get handled at the Front Door edge and provides controlled behavior to your web application. Rules Engine for Azure Front Door (classic) has several key features, including:

* Enforces HTTPS to ensure all your end users interact with your content over a secure connection.

* Implements security headers to prevent browser-based vulnerabilities like HTTP Strict-Transport-Security (HSTS), X-XSS-Protection, Content-Security-Policy, X-Frame-Options, and Access-Control-Allow-Origin headers for Cross-Origin Resource Sharing (CORS) scenarios. Security-based attributes can also be defined with cookies.

* Route requests to mobile or desktop versions of your application based on the patterns of request headers contents, cookies, or query strings.

* Use redirect capabilities to return 301, 302, 307, and 308 redirects to the client to direct to new hostnames, paths, or protocols.

- Dynamically modify the caching configuration of your route based on the incoming requests.

- Rewrite the request URL path and forward the request to the appropriate backend in your configured backend pool.

## Architecture

Rules engine handles requests at the edge. When a request enters your Azure Front Door (classic) endpoint, WAF is processed first, followed by the Rules engine configuration associated with your frontend domain. If a Rules engine configuration gets processed, that means a match condition was found. In order for all actions in each rule to be processed, all the match conditions within a rule has to be met. If a request doesn't match any of the conditions in your Rules engine configuration, then the default routing configuration is processed.

For example, in the following diagram, a Rules engine is configured to append a response header. The header changes the max-age of the cache control if the request file has an extension of *.jpg*.

In this second example, you see Rules engine is configured to redirect users to a mobile version of the website if the requesting device is of type *Mobile*.

In both of these examples, when none of the match conditions are met, the specified routing rule is what gets processed.

## Terminology

In Azure Front Door (classic) you can create Rules engine configurations of many combinations, each composed of a set of rules. The following outlines some helpful terminology you come across when configuring your Rules Engine.

- *Rules engine configuration*: A set of rules that are applied to single route. Each configuration is limited to 25 rules. You can create up to 10 configurations.

- *Rules engine rule*: A rule composed of up to 10 match conditions and 5 actions.

- *Match condition*: There are many match conditions that can be utilized to parse your incoming requests. A rule can contain up to 10 match conditions. Match conditions are evaluated with an **AND** operator. For a full list of match conditions, see [Rules match conditions](rules-match-conditions.md).

- *Action*: Actions dictate what happens to your incoming requests - request/response header actions, forwarding, redirects, and rewrites are all available today. A rule can contain up to five actions; however, a rule might only contain one route configuration override. For a full list of actions, see [Rules actions](front-door-rules-engine-actions.md).

## Next steps

- Learn how to configure your first [Rules engine configuration](front-door-tutorial-rules-engine.md).

- Learn how to [create an Azure Front Door (classic) profile](quickstart-create-front-door.md).

- Learn about [Azure Front Door (classic) routing architecture](front-door-routing-architecture.md).


# Rules Match Conditions

# Rules match conditions

In Azure Front Door [Rule sets](front-door-rules-engine.md), a rule consists of one or more match conditions and an action. This article provides detailed descriptions of the match conditions you can use in Azure Front Door rule sets.

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

In Azure Front Door (classic) [Rules engines](front-door-rules-engine.md), a rule consists of one or more match conditions and an action. This article provides detailed descriptions of the match conditions you can use in Azure Front Door (classic) Rules engines.

A rule starts with a match condition or a set of match conditions. A rule can have up to 10 match conditions. A match condition identifies specific types of requests for which defined actions are performed. If you use multiple match conditions, they're grouped together using AND logic. For match conditions that support multiple values, OR logic is used.

You can use a match condition to:

* Filter requests based on a specific IP address, port, or country/region.

* Filter requests by header information.

* Filter requests from mobile devices or desktop devices.

* Filter requests by request file name and file extension.

* Filter requests by hostname, SSL protocol, request URL, protocol, path, query string, post arguments, and other values.

* Filter requests based on a specific IP address or country/region.

* Filter requests by header information.

* Filter requests from mobile devices or desktop devices.

* Filter requests by request file name and file extension.

* Filter requests by request URL, protocol, path, query string, post arguments, and other values.

## Device type

Use the **device type** match condition to identify requests that is from a mobile device or desktop device.

### Properties

| Property | Supported values |

|-------|------------------|

| Operator | <ul><li>In the Azure portal: `Equal`, `Not Equal`</li><li>In ARM templates: `Equal`; use the `negateCondition` property to specify _Not Equal_</li></ul> |

| Value | `Mobile`, `Desktop` |

### Example

In this example, we match all requests that were detected as coming from a mobile device.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "IsDevice",

"parameters": {

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"Mobile"

],

"typeName": "DeliveryRuleIsDeviceConditionParameters"

}

}

```

```json

{

"name": "IsDevice",

"parameters": {

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"Mobile"

],

"@odata.type": "#Microsoft.Azure.Cdn.Models.DeliveryRuleIsDeviceConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'IsDevice'

parameters: {

operator: 'Equal'

negateCondition: false

matchValues: [

'Mobile'

]

typeName: 'DeliveryRuleIsDeviceConditionParameters'

}

}

```

```bicep

{

name: 'IsDevice'

parameters: {

operator: 'Equal'

negateCondition: false

matchValues: [

'Mobile'

]

'@odata.type': '#Microsoft.Azure.Cdn.Models.DeliveryRuleIsDeviceConditionParameters'

}

}

```

---

## HTTP version

Use the **HTTP version** match condition to identify requests that are made by using a specific version of the HTTP protocol.

> [!NOTE]

> The **HTTP version** match condition is only available on Azure Front Door Standard/Premium.

### Properties

| Property | Supported values |

|-------|------------------|

| Operator | <ul><li>In the Azure portal: `Equal`, `Not Equal`</li><li>In ARM templates: `Equal`; use the `negateCondition` property to specify _Not Equal_</li></ul> |

| Value | `2.0`, `1.1`, `1.0`, `0.9` |

### Example

In this example, we match all requests that were sent by using the HTTP 2.0 protocol.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "HttpVersion",

"parameters": {

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"2.0"

],

"typeName": "DeliveryRuleHttpVersionConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'HttpVersion'

parameters: {

operator: 'Equal'

negateCondition: false

matchValues: [

'2.0'

]

typeName: 'DeliveryRuleHttpVersionConditionParameters'

}

}

```

---

## Request cookies

Use the **request cookies** match condition to identify requests that includes a specific cookie.

> [!NOTE]

> The **request cookies** match condition is only available on Azure Front Door Standard/Premium.

### Properties

| Property | Supported values |

|-------|------------------|

| Cookie name | A string value representing the name of the cookie. |

| Operator | Any operator from the [standard operator list](#operator-list). |

| Value | One or more string or integer values representing the value of the request header to match. If multiple values are specified, they're evaluated using OR logic. |

| Case transform | Any transform from the [standard string transforms list](#string-transform-list). |

### Example

In this example, we match all requests that have a cookie named `deploymentStampId` with a value of `1`.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "Cookies",

"parameters": {

"selector": "deploymentStampId",

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"1"

],

"transforms": [],

"typeName": "DeliveryRuleCookiesConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'Cookies'

parameters: {

selector: 'deploymentStampId'

operator: 'Equal'

negateCondition: false

matchValues: [

'1'

]

typeName: 'DeliveryRuleCookiesConditionParameters'

}

}

```

---

## Post args

Use the **post args** match condition to identify requests based on the arguments provided within a POST request's body. A single match condition matches a single argument from the POST request's body. You can specify multiple values to match, which can be combined using OR logic.

> [!NOTE]

> The **post args** match condition works with the `application/x-www-form-urlencoded` content type.

### Properties

| Property | Supported values |

|-|-|

| Post args | A string value representing the name of the POST argument. |

| Operator | Any operator from the [standard operator list](#operator-list). |

| Value | One or more string or integer values representing the value of the POST argument to match. If multiple values are specified, they're evaluated using OR logic. |

| Case transform | Any transform from the [standard string transforms list](#string-transform-list). |

### Example

In this example, we match all POST requests where a `customerName` argument is provided in the request body, and where the value of `customerName` begins with the letter `J` or `K`. We use a case transform to convert the input values to uppercase so that values beginning with `J`, `j`, `K`, and `k` are all matched.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "PostArgs",

"parameters": {

"selector": "customerName",

"operator": "BeginsWith",

"negateCondition": false,

"matchValues": [

"J",

"K"

],

"transforms": [

"Uppercase"

],

"typeName": "DeliveryRulePostArgsConditionParameters"

}

```

```json

{

"name": "PostArgs",

"parameters": {

"selector": "customerName",

"operator": "BeginsWith",

"negateCondition": false,

"matchValues": [

"J",

"K"

],

"transforms": [

"Uppercase"

],

"@odata.type": "#Microsoft.Azure.Cdn.Models.DeliveryRulePostArgsConditionParameters"

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'PostArgs'

parameters: {

selector: 'customerName'

operator: 'BeginsWith'

negateCondition: false

matchValues: [

'J'

'K'

]

transforms: [

'Uppercase'

]

typeName: 'DeliveryRulePostArgsConditionParameters'

}

}

```

```bicep

{

name: 'PostArgs'

parameters: {

selector: 'customerName'

operator: 'BeginsWith'

negateCondition: false

matchValues: [

'J'

'K'

]

transforms: [

'Uppercase'

]

'@odata.type': '#Microsoft.Azure.Cdn.Models.DeliveryRulePostArgsConditionParameters'

}

}

```

---

## Query string

Use the **query string** match condition to identify requests that contain a specific query string. You can specify multiple values to match, which can be combined using OR logic.

> [!NOTE]

> The entire query string is matched as a single string, without the leading `?`.

### Properties

| Property | Supported values |

|-|-|

| Operator | All operators from the [standard operator list](#operator-list) are supported. However, the **Any** match condition matches every request, and the **Not Any** match condition doesn't match any request, when used with the **query string** match condition. |

| Query string | One or more string or integer values representing the value of the query string to match. Don't include the `?` at the start of the query string. If multiple values are specified, they're evaluated using OR logic. |

| Case transform | Any transform from the [standard string transforms list](#string-transform-list). |

### Example

In this example, we match all requests where the query string contains the string `language=en-US`. We want the match condition to be case-sensitive, so we don't transform the case.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "QueryString",

"parameters": {

"operator": "Contains",

"negateCondition": false,

"matchValues": [

"language=en-US"

],

"typeName": "DeliveryRuleQueryStringConditionParameters"

}

}

```

```json

{

"name": "QueryString",

"parameters": {

"operator": "Contains",

"negateCondition": false,

"matchValues": [

"language=en-US"

],

"@odata.type": "#Microsoft.Azure.Cdn.Models.DeliveryRuleQueryStringConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'QueryString'

parameters: {

operator: 'Contains'

negateCondition: false

matchValues: [

'language=en-US'

]

typeName: 'DeliveryRuleQueryStringConditionParameters'

}

}

```

```bicep

{

name: 'QueryString'

parameters: {

operator: 'Contains'

negateCondition: false

matchValues: [

'language=en-US'

]

'@odata.type': '#Microsoft.Azure.Cdn.Models.DeliveryRuleQueryStringConditionParameters'

}

}

```

---

## Remote address

The **remote address** match condition identifies requests based on the requester's location or IP address. You can specify multiple values to match, which can be combined using OR logic.

* Use CIDR notation when specifying IP address blocks. The syntax for an IP address block is the base IP address followed by a forward slash and the prefix size. For example:

* **IPv4 example**: `5.5.5.64/26` matches any requests that arrive from addresses 5.5.5.64 through 5.5.5.127.

* **IPv6 example**: `1:2:3:/48` matches any requests that arrive from addresses 1:2:3:0:0:0:0:0 through 1:2:3: ffff:ffff:ffff:ffff:ffff.

* When you specify multiple IP addresses and IP address blocks, 'OR' logic is applied.

* **IPv4 example**: if you add two IP addresses `1.2.3.4` and `10.20.30.40`, the condition is matched for any requests that arrive from either address 1.2.3.4 or 10.20.30.40.

* **IPv6 example**: if you add two IP addresses `1:2:3:4:5:6:7:8` and `10:20:30:40:50:60:70:80`, the condition is matched for any requests that arrive from either address 1:2:3:4:5:6:7:8 or 10:20:30:40:50:60:70:80.

* The remote address represents the original client IP that is either from the network connection or typically the X-Forwarded-For request header if the user is behind a proxy. Use the [socket address](#socket-address) match condition (available in Standard/Premium), if you need to match based on the TCP request's IP address.

### Properties

| Property | Supported values |

|-|-|

| Operator | <ul><li>In the Azure portal: `Geo Match`, `Geo Not Match`, `IP Match`, or `IP Not Match`</li><li>In ARM templates: `GeoMatch`, `IPMatch`; use the `negateCondition` property to specify _Geo Not Match_ or _IP Not Match_</li></ul> |

| Value | <ul><li>For the `IP Match` or `IP Not Match` operators: specify one or more IP address ranges. If multiple IP address ranges are specified, they're evaluated using OR logic.</li><li>For the `Geo Match` or `Geo Not Match` operators: specify one or more locations using their country code.</li></ul> |

### Example

In this example, we match all requests where the request didn't originate from the United States.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "RemoteAddress",

"parameters": {

"operator": "GeoMatch",

"negateCondition": true,

"matchValues": [

"US"

],

"typeName": "DeliveryRuleRemoteAddressConditionParameters"

}

}

```

```json

{

"name": "RemoteAddress",

"parameters": {

"operator": "GeoMatch",

"negateCondition": true,

"matchValues": [

"US"

],

"@odata.type": "#Microsoft.Azure.Cdn.Models.DeliveryRuleRemoteAddressConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'RemoteAddress'

parameters: {

operator: 'GeoMatch'

negateCondition: true

matchValues: [

'US'

]

typeName: 'DeliveryRuleRemoteAddressConditionParameters'

}

}

```

```bicep

{

name: 'RemoteAddress'

parameters: {

operator: 'GeoMatch'

negateCondition: true

matchValues: [

'US'

]

'@odata.type': '#Microsoft.Azure.Cdn.Models.DeliveryRuleRemoteAddressConditionParameters'

}

}

```

---

## Request body

The **request body** match condition identifies requests based on specific text that appears in the body of the request. You can specify multiple values to match, which can be combined using OR logic.

> [!NOTE]

> If a request body exceeds 64KB in size, only the first 64KB will be considered for the **request body** match condition.

### Properties

| Property | Supported values |

|-|-|

| Operator | All operators from the [standard operator list](#operator-list) are supported. However, the **Any** match condition matches every request, and the **Not Any** match condition doesn't match any request, when used with the **request body** match condition. |

| Value | One or more string or integer values representing the value of the request body text to match. If multiple values are specified, they're evaluated using OR logic. |

| Case transform | Any transform from the [standard string transforms list](#string-transform-list). |

### Example

In this example, we match all requests where the request body contains the string `ERROR`. We transform the request body to uppercase before evaluating the match, so `error` and other case variations also triggers this match condition.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "RequestBody",

"parameters": {

"operator": "Contains",

"negateCondition": false,

"matchValues": [

"ERROR"

],

"transforms": [

"Uppercase"

],

"typeName": "DeliveryRuleRequestBodyConditionParameters"

}

}

```

```json

{

"name": "RequestBody",

"parameters": {

"operator": "Contains",

"negateCondition": false,

"matchValues": [

"ERROR"

],

"transforms": [

"Uppercase"

],

"@odata.type": "#Microsoft.Azure.Cdn.Models.DeliveryRuleRequestBodyConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'RequestBody'

parameters: {

operator: 'Contains'

negateCondition: false

matchValues: [

'ERROR'

]

transforms: [

'Uppercase'

]

typeName: 'DeliveryRuleRequestBodyConditionParameters'

}

}

```

```bicep

{

name: 'RequestBody'

parameters: {

operator: 'Contains'

negateCondition: false

matchValues: [

'ERROR'

]

transforms: [

'Uppercase'

]

'@odata.type': '#Microsoft.Azure.Cdn.Models.DeliveryRuleRequestBodyConditionParameters'

}

}

```

---

## Request file name

The **request file name** match condition identifies requests that include the specified file name in the request URL. You can specify multiple values to match, which can be combined using OR logic.

### Properties

| Property | Supported values |

|-|-|

| Operator | All operators from the [standard operator list](#operator-list) are supported. However, the **Any** match condition matches every request, and the **Not Any** match condition doesn't match any request, when used with the **request file name** match condition. |

| Value | One or more string or integer values representing the value of the request file name to match. If multiple values are specified, they're evaluated using OR logic. |

| Case transform | Any transform from the [standard string transforms list](#string-transform-list). |

### Example

In this example, we match all requests where the request file name is `media.mp4`. We transform the file name to lowercase before evaluating the match, so `MEDIA.MP4` and other case variations also triggers this match condition.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "UrlFileName",

"parameters": {

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"media.mp4"

],

"transforms": [

"Lowercase"

],

"typeName": "DeliveryRuleUrlFilenameConditionParameters"

}

}

```

```json

{

"name": "UrlFileName",

"parameters": {

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"media.mp4"

],

"transforms": [

"Lowercase"

],

"@odata.type": "#Microsoft.Azure.Cdn.Models.DeliveryRuleUrlFilenameConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'UrlFileName'

parameters: {

operator: 'Equal'

negateCondition: false

matchValues: [

'media.mp4'

]

transforms: [

'Lowercase'

]

typeName: 'DeliveryRuleUrlFilenameConditionParameters'

}

}

```

```bicep

{

name: 'UrlFileName'

parameters: {

operator: 'Equal'

negateCondition: false

matchValues: [

'media.mp4'

]

transforms: [

'Lowercase'

]

'@odata.type': '#Microsoft.Azure.Cdn.Models.DeliveryRuleUrlFilenameConditionParameters'

}

}

```

---

## Request file extension

The **request file extension** match condition identifies requests that include the specified file extension in the file name in the request URL. You can specify multiple values to match, which can be combined using OR logic.

> [!NOTE]

> Don't include a leading period. For example, use `html` instead of `.html`.

### Properties

| Property | Supported values |

|-|-|

| Operator | All operators from the [standard operator list](#operator-list) are supported. However, the **Any** match condition matches every request, and the **Not Any** match condition doesn't match any request, when used with the **request file extension** match condition. |

| Value | One or more string or integer values representing the value of the request file extension to match. Don't include a leading period. If multiple values are specified, they're evaluated using OR logic. |

| Case transform | Any transform from the [standard string transforms list](#string-transform-list). |

### Example

In this example, we match all requests where the request file extension is `pdf` or `docx`. We transform the request file extension to lowercase before evaluating the match, so `PDF`, `DocX`, and other case variations also trigger this match condition.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "UrlFileExtension",

"parameters": {

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"pdf",

"docx"

],

"transforms": [

"Lowercase"

],

"typeName": "DeliveryRuleUrlFileExtensionMatchConditionParameters"

}

```

```json

{

"name": "UrlFileExtension",

"parameters": {

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"pdf",

"docx"

],

"transforms": [

"Lowercase"

],

"@odata.type": "#Microsoft.Azure.Cdn.Models.DeliveryRuleUrlFileExtensionMatchConditionParameters"

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'UrlFileExtension'

parameters: {

operator: 'Equal'

negateCondition: false

matchValues: [

'pdf'

'docx'

]

transforms: [

'Lowercase'

]

typeName: 'DeliveryRuleUrlFileExtensionMatchConditionParameters'

}

}

```

```bicep

{

name: 'UrlFileExtension'

parameters: {

operator: 'Equal'

negateCondition: false

matchValues: [

'pdf'

'docx'

]

transforms: [

'Lowercase'

]

'@odata.type': '#Microsoft.Azure.Cdn.Models.DeliveryRuleUrlFileExtensionMatchConditionParameters'

}

}

```

---

## Request header

The **request header** match condition identifies requests that include a specific header in the request. You can use this match condition to check if a header exists or to check if the header matches a specified value. You can specify multiple values to match, which can be combined using OR logic.

### Properties

| Property | Supported values |

|-|-|

| Header name | A string value representing the name of the POST argument. |

| Operator | Any operator from the [standard operator list](#operator-list). |

| Value | One or more string or integer values representing the value of the request header to match. If multiple values are specified, they're evaluated using OR logic. |

| Case transform | Any transform from the [standard string transforms list](#string-transform-list). |

### Example

In this example, we match all requests where the request contains a header named `MyCustomHeader`, regardless of its value.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "RequestHeader",

"parameters": {

"selector": "MyCustomHeader",

"operator": "Any",

"negateCondition": false,

"typeName": "DeliveryRuleRequestHeaderConditionParameters"

}

}

```

```json

{

"name": "RequestHeader",

"parameters": {

"selector": "MyCustomHeader",

"operator": "Any",

"negateCondition": false,

"@odata.type": "#Microsoft.Azure.Cdn.Models.DeliveryRuleRequestHeaderConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'RequestHeader'

parameters: {

selector: 'MyCustomHeader',

operator: 'Any'

negateCondition: false

typeName: 'DeliveryRuleRequestHeaderConditionParameters'

}

}

```

```bicep

{

name: 'RequestHeader'

parameters: {

selector: 'MyCustomHeader',

operator: 'Any'

negateCondition: false

'@odata.type': '#Microsoft.Azure.Cdn.Models.DeliveryRuleRequestHeaderConditionParameters'

}

}

```

---

## Request method

The **request method** match condition identifies requests that use the specified HTTP request method. You can specify multiple values to match, which can be combined using OR logic.

### Properties

| Property | Supported values |

|-|-|

| Operator | <ul><li>In the Azure portal: `Equal`, `Not Equal`</li><li>In ARM templates: `Equal`; use the `negateCondition` property to specify _Not Equal_</li></ul> |

| Request method | One or more HTTP methods from: `GET`, `POST`, `PUT`, `DELETE`, `HEAD`, `OPTIONS`, `TRACE`. If multiple values are specified, they're evaluated using OR logic. |

### Example

In this example, we match all requests where the request uses the `DELETE` method.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "RequestMethod",

"parameters": {

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"DELETE"

],

"typeName": "DeliveryRuleRequestMethodConditionParameters"

}

}

```

```json

{

"name": "RequestMethod",

"parameters": {

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"DELETE"

],

"@odata.type": "#Microsoft.Azure.Cdn.Models.DeliveryRuleRequestMethodConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'RequestMethod'

parameters: {

operator: 'Equal'

negateCondition: false

matchValues: [

'DELETE'

]

typeName: 'DeliveryRuleRequestMethodConditionParameters'

}

}

```

```bicep

{

name: 'RequestMethod'

parameters: {

operator: 'Equal'

negateCondition: false

matchValues: [

'DELETE'

]

'@odata.type': '#Microsoft.Azure.Cdn.Models.DeliveryRuleRequestMethodConditionParameters'

}

}

```

---

## Request path

The **request path** match condition identifies requests that include the specified path in the request URL. You can specify multiple values to match, which can be combined using OR logic.

> [!NOTE]

> The path is the part of the URL after the hostname and a slash. For example, in the URL `https://www.contoso.com/files/secure/file1.pdf`, the path is `files/secure/file1.pdf`.

### Properties

| Property | Supported values |

|-|-|

| Operator | <ul><li>All operators from the [standard operator list](#operator-list) are supported. However, the **Any** match condition matches every request, and the **Not Any** match condition doesn't match any request, when used with the **request path** match condition.</li><li>**Wildcard**: Matches when the request path matches a wildcard expression. A wildcard expression can include the `*` character to match zero or more characters within the path. For example, the wildcard expression `files/customer*/file.pdf` matches the paths `files/customer1/file.pdf`, `files/customer109/file.pdf`, and `files/customer/file.pdf`, but doesn't match `files/customer2/anotherfile.pdf`.<ul><li>In the Azure portal: `Wildcards`, `Not Wildcards`</li><li>In ARM templates: `Wildcard`; use the `negateCondition` property to specify _Not Wildcards_</li></ul></li></ul> |

| Value | One or more string or integer values representing the value of the request path to match. If you specify a leading slash, it gets ignored. If multiple values are specified, they're evaluated using OR logic. |

| Case transform | Any transform from the [standard string transforms list](#string-transform-list). |

| Property | Supported values |

|-|-|

| Operator | All operators from the [standard operator list](#operator-list) are supported. However, the **Any** match condition matches every request, and the **Not Any** match condition doesn't match any request, when used with the **request path** match condition. |

| Value | One or more string or integer values representing the value of the request path to match. If you specify a leading slash, it gets ignored. If multiple values are specified, they're evaluated using OR logic. |

| Case transform | Any transform from the [standard string transforms list](#string-transform-list). |

### Example

In this example, we match all requests where the request file path begins with `files/secure/`. We transform the request file extension to lowercase before evaluating the match, so requests to `files/SECURE/` and other case variations also triggers this match condition.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "UrlPath",

"parameters": {

"operator": "BeginsWith",

"negateCondition": false,

"matchValues": [

"files/secure/"

],

"transforms": [

"Lowercase"

],

"typeName": "DeliveryRuleUrlPathMatchConditionParameters"

}

}

```

```json

{

"name": "UrlPath",

"parameters": {

"operator": "BeginsWith",

"negateCondition": false,

"matchValues": [

"files/secure/"

],

"transforms": [

"Lowercase"

],

"@odata.type": "#Microsoft.Azure.Cdn.Models.DeliveryRuleUrlPathMatchConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'UrlPath'

parameters: {

operator: 'BeginsWith'

negateCondition: false

matchValues: [

'files/secure/'

]

transforms: [

'Lowercase'

]

typeName: 'DeliveryRuleUrlPathMatchConditionParameters'

}

}

```

```bicep

{

name: 'UrlPath'

parameters: {

operator: 'BeginsWith'

negateCondition: false

matchValues: [

'files/secure/'

]

transforms: [

'Lowercase'

]

'@odata.type': '#Microsoft.Azure.Cdn.Models.DeliveryRuleUrlPathMatchConditionParameters'

}

}

```

---

## Request protocol

The **request protocol** match condition identifies requests that use the specified protocol (HTTP or HTTPS).

> [!NOTE]

> *Protocol* is sometimes also called *scheme*.

### Properties

| Property | Supported values |

|-|-|

| Operator | <ul><li>In the Azure portal: `Equal`, `Not Equal`</li><li>In ARM templates: `Equal`; use the `negateCondition` property to specify _Not Equal_</li></ul> |

| Request method | `HTTP`, `HTTPS` |

### Example

In this example, we match all requests where the request uses the `HTTP` protocol.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "RequestScheme",

"parameters": {

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"HTTP"

],

"typeName": "DeliveryRuleRequestSchemeConditionParameters"

}

}

```

```json

{

"name": "RequestScheme",

"parameters": {

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"HTTP"

],

"@odata.type": "#Microsoft.Azure.Cdn.Models.DeliveryRuleRequestSchemeConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'RequestScheme'

parameters: {

operator: 'Equal'

negateCondition: false

matchValues: [

'HTTP'

]

typeName: 'DeliveryRuleRequestSchemeConditionParameters'

}

}

```

```bicep

{

name: 'RequestScheme'

parameters: {

operator: 'Equal'

negateCondition: false

matchValues: [

'HTTP'

]

'@odata.type': '#Microsoft.Azure.Cdn.Models.DeliveryRuleRequestSchemeConditionParameters'

}

}

```

---

## Request URL

Identifies requests that match the specified URL. The entire URL is evaluated, including the protocol and query string, but not the fragment. You can specify multiple values to match, which can be combined using OR logic.

> [!TIP]

> When you use this rule condition, be sure to include the protocol and a trailing forward slash `/`. For example, use `https://www.contoso.com/` instead of just `www.contoso.com`.

### Properties

| Property | Supported values |

|-|-|

| Operator | All operators from the [standard operator list](#operator-list) are supported. However, the **Any** match condition matches every request, and the **Not Any** match condition doesn't match any request, when used with the **request URL** match condition. |

| Value | One or more string or integer values representing the value of the request URL to match. If multiple values are specified, they're evaluated using OR logic. |

| Case transform | Any transform from the [standard string transforms list](#string-transform-list). |

### Example

In this example, we match all requests where the request URL begins with `https://api.contoso.com/customers/123`. We transform the request file extension to lowercase before evaluating the match, so requests to `https://api.contoso.com/Customers/123` and other case variations will also trigger this match condition.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "RequestUri",

"parameters": {

"operator": "BeginsWith",

"negateCondition": false,

"matchValues": [

"https://api.contoso.com/customers/123"

],

"transforms": [

"Lowercase"

],

"typeName": "DeliveryRuleRequestUriConditionParameters"

}

}

```

```json

{

"name": "RequestUri",

"parameters": {

"operator": "BeginsWith",

"negateCondition": false,

"matchValues": [

"https://api.contoso.com/customers/123"

],

"transforms": [

"Lowercase"

],

"@odata.type": "#Microsoft.Azure.Cdn.Models.DeliveryRuleRequestUriConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'RequestUri'

parameters: {

operator: 'BeginsWith'

negateCondition: false

matchValues: [

'https://api.contoso.com/customers/123'

]

transforms: [

'Lowercase'

]

typeName: 'DeliveryRuleRequestUriConditionParameters'

}

}

```

```bicep

{

name: 'RequestUri'

parameters: {

operator: 'BeginsWith'

negateCondition: false

matchValues: [

'https://api.contoso.com/customers/123'

]

transforms: [

'Lowercase'

]

'@odata.type': '#Microsoft.Azure.Cdn.Models.DeliveryRuleRequestUriConditionParameters'

}

}

```

---

## Host name

The **host name** match condition identifies requests based on the specified hostname in the request from the client. The match condition uses the `Host` header value to evaluate the hostname. You can specify multiple values to match, which can be combined using OR logic.

### Properties

| Property | Supported values |

|-------|------------------|

| Operator | All operators from the [standard operator list](#operator-list) are supported. However, the **Any** match condition matches every request, and the **Not Any** match condition doesn't match any request, when used with the **host name** match condition. |

| Value | One or more string values representing the value of request hostname to match. If multiple values are specified, they're evaluated using OR logic. |

| Case transform | Any case transform from the [standard string transforms list](#string-transform-list). |

### Example

In this example, we match all requests with a `Host` header that ends with `contoso.com`.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "HostName",

"parameters": {

"operator": "EndsWith",

"negateCondition": false,

"matchValues": [

"contoso.com"

],

"transforms": [],

"typeName": "DeliveryRuleHostNameConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'HostName'

parameters: {

operator: 'EndsWith'

negateCondition: false

matchValues: [

'contoso.com'

]

transforms: []

typeName: 'DeliveryRuleHostNameConditionParameters'

}

}

```

---

## SSL protocol

The **SSL protocol** match condition identifies requests based on the SSL protocol of an established TLS connection. You can specify multiple values to match, which can be combined using OR logic.

### Properties

| Property | Supported values |

|-------|------------------|

| Operator | <ul><li>In the Azure portal: `Equal`, `Not Equal`</li><li>In ARM templates: `Equal`; use the `negateCondition` property to specify _Not Equal_</li></ul> |

| SSL protocol | <ul><li>In the Azure portal: `1.0`, `1.1`, `1.2`</li><li>In ARM templates: `TLSv1`, `TLSv1.1`, `TLSv1.2`</li></ul> |

### Example

In this example, we match all requests that use the TLS 1.2 protocol.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "SslProtocol",

"parameters": {

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"TLSv1.2"

],

"typeName": "DeliveryRuleSslProtocolConditionParameters"

}

},

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'SslProtocol'

parameters: {

operator: 'Equal'

negateCondition: false

matchValues: [

'TLSv1.2'

]

typeName: 'DeliveryRuleSslProtocolConditionParameters'

}

}

```

---

## Socket address

The **socket address** match condition identifies requests based on the IP address of the direct connection to Azure Front Door edge. You can specify multiple values to match, which can be combined using OR logic.

> [!NOTE]

> If the client used an HTTP proxy or a load balancer to send the request, the socket address is the IP address of the proxy or load balancer.

>

> Use the [remote address](#remote-address) match condition if you need to match based on the client's original IP address.

* Use CIDR notation when specifying IP address blocks. This means that the syntax for an IP address block is the base IP address followed by a forward slash and the prefix size. For example:

* **IPv4 example**: `5.5.5.64/26` matches any requests that arrive from addresses 5.5.5.64 through 5.5.5.127.

* **IPv6 example**: `1:2:3:/48` matches any requests that arrive from addresses 1:2:3:0:0:0:0:0 through 1:2:3: ffff:ffff:ffff:ffff:ffff.

* When you specify multiple IP addresses and IP address blocks, 'OR' logic is applied.

* **IPv4 example**: if you add two IP addresses `1.2.3.4` and `10.20.30.40`, the condition is matched for any requests that arrive from either address 1.2.3.4 or 10.20.30.40.

* **IPv6 example**: if you add two IP addresses `1:2:3:4:5:6:7:8` and `10:20:30:40:50:60:70:80`, the condition is matched for any requests that arrive from either address 1:2:3:4:5:6:7:8 or 10:20:30:40:50:60:70:80.

### Properties

| Property | Supported values |

|-------|------------------|

| Operator | <ul><li>In the Azure portal: `IP Match`, `Not IP Match`</li><li>In ARM templates: `IPMatch`; use the `negateCondition` property to specify _Not IP Match_</li></ul> |

| Value | Specify one or more IP address ranges. If multiple IP address ranges are specified, they're evaluated using OR logic. |

### Example

In this example, we match all requests from IP addresses in the range 5.5.5.64/26.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "SocketAddr",

"parameters": {

"operator": "IPMatch",

"negateCondition": false,

"matchValues": [

"5.5.5.64/26"

],

"typeName": "DeliveryRuleSocketAddrConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'SocketAddr'

parameters: {

operator: 'IPMatch'

negateCondition: false

matchValues: [

'5.5.5.64/26'

]

typeName: 'DeliveryRuleSocketAddrConditionParameters'

}

}

```

---

## Client port

The **client port** match condition identifies requests based on the TCP port of the client that made the request. You can specify multiple values to match, which can be combined using OR logic.

### Properties

| Property | Supported values |

|-------|------------------|

| Operator | All operators from the [standard operator list](#operator-list) are supported. However, the **Any** match condition matches every request, and the **Not Any** match condition doesn't match any request, when used with the **client port** match condition. |

| Value | One or more port numbers, expressed as integers. If multiple values are specified, they're evaluated using OR logic. |

### Example

In this example, we match all requests with a client port of 1234.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "ClientPort",

"parameters": {

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"1111"

],

"typeName": "DeliveryRuleClientPortConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'ClientPort'

parameters: {

operator: 'Equal'

negateCondition: false

matchValues: [

'1111'

]

typeName: 'DeliveryRuleClientPortConditionParameters'

}

}

```

---

## Server port

The **server port** match condition identifies requests based on the TCP port of the Azure Front Door server that accepted the request. The port must be 80 or 443. You can specify multiple values to match, which can be combined using OR logic.

### Properties

| Property | Supported values |

|-------|------------------|

| Operator | All operators from the [standard operator list](#operator-list) are supported. However, the **Any** match condition matches every request, and the **Not Any** match condition doesn't match any request, when used with the **server port** match condition. |

| Value | A port number, which must be either 80 or 443. If multiple values are specified, they're evaluated using OR logic. |

### Example

In this example, we match all requests with a server port of 443.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "ServerPort",

"parameters": {

"operator": "Equal",

"negateCondition": false,

"matchValues": [

"443"

],

"typeName": "DeliveryRuleServerPortConditionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'ServerPort'

parameters: {

operator: 'Equal'

negateCondition: false

matchValues: [

'443'

]

typeName: 'DeliveryRuleServerPortConditionParameters'

}

}

```

---

## Operator list

For rules that accept values from the standard operator list, the following operators are valid:

| Operator                   | Description                                                                                                                    | ARM template support                                            |

|----------------------------|--------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|

| Any                        | Matches when there's any value, regardless of what it is.                                                                     | `operator`: `Any`                                               |

| Equal                      | Matches when the value exactly matches the specified string.                                                                   | `operator`: `Equal`                                             |

| Contains                   | Matches when the value contains the specified string.                                                                          | `operator`: `Contains`                                          |

| Less Than                  | Matches when the length of the value is less than the specified integer.                                                       | `operator`: `LessThan`                                          |

| Greater Than               | Matches when the length of the value is greater than the specified integer.                                                    | `operator`: `GreaterThan`                                       |

| Less Than or Equal         | Matches when the length of the value is less than or equal to the specified integer.                                           | `operator`: `LessThanOrEqual`                                   |

| Greater Than or Equal      | Matches when the length of the value is greater than or equal to the specified integer.                                        | `operator`: `GreaterThanOrEqual`                                |

| Begins With                | Matches when the value begins with the specified string.                                                                       | `operator`: `BeginsWith`                                        |

| Ends With                  | Matches when the value ends with the specified string.                                                                         | `operator`: `EndsWith`                                          |

| Not Any                    | Matches when there's no value.                                                                                                | `operator`: `Any` and `negateCondition` : `true`                |

| Not Equal                  | Matches when the value doesn't match the specified string.                                                                    | `operator`: `Equal` and `negateCondition` : `true`              |

| Not Contains               | Matches when the value doesn't contain the specified string.                                                                  | `operator`: `Contains` and `negateCondition` : `true`           |

| Not Less Than              | Matches when the length of the value isn't less than the specified integer.                                                   | `operator`: `LessThan` and `negateCondition` : `true`           |

| Not Greater Than           | Matches when the length of the value isn't greater than the specified integer.                                                | `operator`: `GreaterThan` and `negateCondition` : `true`        |

| Not Less Than or Equal     | Matches when the length of the value isn't less than or equal to the specified integer.                                       | `operator`: `LessThanOrEqual` and `negateCondition` : `true`    |

| Not Greater Than or Equals | Matches when the length of the value isn't greater than or equal to the specified integer.                                    | `operator`: `GreaterThanOrEqual` and `negateCondition` : `true` |

| Not Begins With            | Matches when the value doesn't begin with the specified string.                                                               | `operator`: `BeginsWith` and `negateCondition` : `true`         |

| Not Ends With              | Matches when the value doesn't end with the specified string.                                                                 | `operator`: `EndsWith` and `negateCondition` : `true`           |

| Operator                   | Description                                                                                                                    | ARM template support                                            |

|----------------------------|--------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|

| Any                        | Matches when there's any value, regardless of what it is.                                                                     | `operator`: `Any`                                               |

| Equal                      | Matches when the value exactly matches the specified string.                                                                   | `operator`: `Equal`                                             |

| Contains                   | Matches when the value contains the specified string.                                                                          | `operator`: `Contains`                                          |

| Less Than                  | Matches when the length of the value is less than the specified integer.                                                       | `operator`: `LessThan`                                          |

| Greater Than               | Matches when the length of the value is greater than the specified integer.                                                    | `operator`: `GreaterThan`                                       |

| Less Than or Equal         | Matches when the length of the value is less than or equal to the specified integer.                                           | `operator`: `LessThanOrEqual`                                   |

| Greater Than or Equal      | Matches when the length of the value is greater than or equal to the specified integer.                                        | `operator`: `GreaterThanOrEqual`                                |

| Begins With                | Matches when the value begins with the specified string.                                                                       | `operator`: `BeginsWith`                                        |

| Ends With                  | Matches when the value ends with the specified string.                                                                         | `operator`: `EndsWith`                                          |

| RegEx                      | Matches when the value matches the specified regular expression. [See below for further details.](#regular-expressions)        | `operator`: `RegEx`                                             |

| Not Any                    | Matches when there's no value.                                                                                                | `operator`: `Any` and `negateCondition` : `true`                |

| Not Equal                  | Matches when the value doesn't match the specified string.                                                                    | `operator`: `Equal` and `negateCondition` : `true`              |

| Not Contains               | Matches when the value doesn't contain the specified string.                                                                  | `operator`: `Contains` and `negateCondition` : `true`           |

| Not Less Than              | Matches when the length of the value isn't less than the specified integer.                                                   | `operator`: `LessThan` and `negateCondition` : `true`           |

| Not Greater Than           | Matches when the length of the value isn't greater than the specified integer.                                                | `operator`: `GreaterThan` and `negateCondition` : `true`        |

| Not Less Than or Equal     | Matches when the length of the value isn't less than or equal to the specified integer.                                       | `operator`: `LessThanOrEqual` and `negateCondition` : `true`    |

| Not Greater Than or Equals | Matches when the length of the value isn't greater than or equal to the specified integer.                                    | `operator`: `GreaterThanOrEqual` and `negateCondition` : `true` |

| Not Begins With            | Matches when the value doesn't begin with the specified string.                                                               | `operator`: `BeginsWith` and `negateCondition` : `true`         |

| Not Ends With              | Matches when the value doesn't end with the specified string.                                                                 | `operator`: `EndsWith` and `negateCondition` : `true`           |

| Not RegEx                  | Matches when the value doesn't match the specified regular expression. [See below for further details.](#regular-expressions) | `operator`: `RegEx` and `negateCondition` : `true`              |

> [!TIP]

> For numeric operators like *Less than* and *Greater than or equals*, the comparison used is based on length. The value in the match condition should be an integer that specifies the length you want to compare.

### Regular expressions

Regular expressions don't support the following operations:

* Backreferences and capturing subexpressions.

* Arbitrary zero-width assertions.

* Subroutine references and recursive patterns.

* Conditional patterns.

* Backtracking control verbs.

* The `\C` single-byte directive.

* The `\R` newline match directive.

* The `\K` start of match reset directive.

* Callouts and embedded code.

* Atomic grouping and possessive quantifiers.

## String transform list

For rules that can transform strings, the following transforms are valid:

| Transform | Description | ARM template support |

|-|-|-|

| To lowercase | Converts the string to the lowercase representation. | `Lowercase` |

| To uppercase | Converts the string to the uppercase representation. | `Uppercase` |

| Trim | Trims leading and trailing whitespace from the string. | `Trim` |

| Remove nulls | Removes null values from the string. | `RemoveNulls` |

| URL encode | URL-encodes the string. | `UrlEncode` |

| URL decode | URL-decodes the string. | `UrlDecode` |

## Next steps

* Learn more about Azure Front Door (classic) [Rules Engine](front-door-rules-engine.md)

* Learn how to [configure your first Rules Engine](front-door-tutorial-rules-engine.md).

* Learn more about [Rules actions](front-door-rules-engine-actions.md)

* Learn more about Azure Front Door [Rule Set](front-door-rules-engine.md).

* Learn how to [configure your first Rule Set](standard-premium/how-to-configure-rule-set.md).

* Learn more about [Rule actions](front-door-rules-engine-actions.md).


# Front Door Rules Engine Actions

# Rule set actions

An Azure Front Door [rule set](front-door-rules-engine.md) consist of rules with a combination of match conditions and actions. This article provides a detailed description of actions you can use in a rule set. An action defines the behavior that gets applied to a request type that a match condition(s) identifies. In a rule set, a rule can have up to five actions. Front Door also supports [server variable](rule-set-server-variables.md) in a rule set action.

The following actions are available for use in a rule set:

## <a name="RouteConfigurationOverride"></a> Route configuration override

The **route configuration override** action is used to override the origin group or the caching configuration for the request. You can choose to override or honor the origin group configurations specified in the route. However, when you override the route configuration, you must configure caching. Otherwise, caching gets disabled for the request.

You can also override how files get cached for specific requests, including:

- Override the caching behavior specified by the origin.

- How query string parameters are used to generate the request's cache key.

- The time to live (TTL) value to control how long contents stay in cache.

### Properties

| Property | Supported values |

|----------|------------------|

| Override origin group | <ul><li>**Yes:** Override the origin group used for the request.</li> <li>**No:** Use the origin group specified in the route.</li></ul> |

| Caching | <ul><li>**Enabled:** Force caching to be enabled for the request.</li><li>**Disabled:** Force caching to be disabled for the request.</li></ul> |

When **Override origin group** is set to **Yes**, set the following properties:

| Property | Supported values |

|----------|------------------|

| Origin group | The origin group that the request should be routed to. This setting overrides the configuration specified in the Front Door endpoint route. |

| Forwarding protocol | The protocol for Front Door to use when forwarding the request to the origin. Supported values are HTTP only, HTTPS only, Match incoming request. This setting overrides the configuration specified in the Front Door endpoint route. |

When **Caching** is set to **Enabled**, set the following properties:

| Property | Supported values |

|-------|------------------|

| Query string caching behavior | <ul><li>**Ignore Query String:** Query strings aren't considered when the cache key gets generated. In ARM templates, set the `queryStringCachingBehavior` property to `IgnoreQueryString`.</li><li>**Use query string:** Each unique URL has its own cache key. In ARM templates, use the `queryStringCachingBehavior` of `UseQueryString`.</li><li>**Ignore specified query string:** Query strings specified in the parameters get excluded when the cache key gets generated. In ARM templates, set the `queryStringCachingBehavior` property to `IgnoreSpecifiedQueryStrings`.</li><li>**Include specified query string:** Query strings specified in the parameters get included when the cache key gets generated. In ARM templates, set the `queryStringCachingBehavior` property to `IncludeSpecifiedQueryStrings`.</li></ul> |

| Query parameters | The list of query string parameter names, separated by commas. This property is only set when *Query string caching behavior* is set to *Ignore Specified Query Strings* or *Include Specified Query Strings*. |

| Compression | <ul><li>**Enabled:** Front Door dynamically compresses content at the edge, resulting in a smaller and faster response. For more information, see [File compression](front-door-caching.md#file-compression). In ARM templates, set the `isCompressionEnabled` property to `Enabled`.</li><li>**Disabled.** Front Door doesn't perform compression. In ARM templates, set the `isCompressionEnabled` property to `Disabled`.</li></ul> |

| Cache behavior | <ul><li>**Honor origin:** Front Door always honors origin response header directive. If the origin directive is missing, Front Door caches contents anywhere from 1 to 3 days. In ARM templates, set the `cacheBehavior` property to `HonorOrigin`.</li><li>**Override always:** The TTL value returned from your origin is overwritten with the value specified in the action. This behavior only gets applied if the response is cacheable. In ARM templates, set the `cacheBehavior` property to `OverrideAlways`.</li><li>**Override if origin missing:** If no TTL value gets returned from your origin, the rule sets the TTL to the value specified in the action. This behavior only gets applied if the response is cacheable. In ARM templates, set the `cacheBehavior` property to `OverrideIfOriginMissing`.</li></ul> |

| Cache duration | When _Cache behavior_ is set to `Override always` or `Override if origin missing`, these fields must specify the cache duration to use. The maximum duration is 366 days. This property is only set when *Cache behavior* is set to *Override always* or *Override if origin missing*.<ul><li>In the Azure portal: specify the days, hours, minutes, and seconds.</li><li>In ARM templates: use the `cacheDuration` to specify the duration in the format `d.hh:mm:ss`. |

### Examples

In this example, we route all matched requests to an origin group named `MyOriginGroup`, regardless of the configuration in the Front Door endpoint route.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "RouteConfigurationOverride",

"parameters": {

"originGroupOverride": {

"originGroup": {

"id": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.Cdn/profiles/<profile-name>/originGroups/MyOriginGroup"

},

"forwardingProtocol": "MatchRequest"

},

"cacheConfiguration": null,

"typeName": "DeliveryRuleRouteConfigurationOverrideActionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'RouteConfigurationOverride'

parameters: {

originGroupOverride: {

originGroup: {

id: '/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.Cdn/profiles/<profile-name>/originGroups/MyOriginGroup'

}

forwardingProtocol: 'MatchRequest'

}

cacheConfiguration: null

typeName: 'DeliveryRuleRouteConfigurationOverrideActionParameters'

}

}

```

---

In this example, we set the cache key to include a query string parameter named `customerId`. Compression is enabled, and the origin's caching policies are honored.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "RouteConfigurationOverride",

"parameters": {

"cacheConfiguration": {

"queryStringCachingBehavior": "IncludeSpecifiedQueryStrings",

"queryParameters": "customerId",

"isCompressionEnabled": "Enabled",

"cacheBehavior": "HonorOrigin",

"cacheDuration": null

},

"originGroupOverride": null,

"typeName": "DeliveryRuleRouteConfigurationOverrideActionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'RouteConfigurationOverride'

parameters: {

cacheConfiguration: {

queryStringCachingBehavior: 'IncludeSpecifiedQueryStrings'

queryParameters: 'customerId'

isCompressionEnabled: 'Enabled'

cacheBehavior: 'HonorOrigin'

cacheDuration: null

}

originGroupOverride: null

typeName: 'DeliveryRuleRouteConfigurationOverrideActionParameters'

}

}

```

---

In this example, we override the cache expiration to 6 hours for matched requests that don't specify a cache duration already. Front Door ignores the query string when it determines the cache key, and compression is enabled.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "RouteConfigurationOverride",

"parameters": {

"cacheConfiguration": {

"queryStringCachingBehavior": "IgnoreQueryString",

"cacheBehavior": "OverrideIfOriginMissing",

"cacheDuration": "0.06:00:00",

},

"originGroupOverride": null,

"typeName": "DeliveryRuleRouteConfigurationOverrideActionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'RouteConfigurationOverride'

parameters: {

cacheConfiguration: {

queryStringCachingBehavior: 'IgnoreQueryString'

cacheBehavior: 'OverrideIfOriginMissing'

cacheDuration: '0.06:00:00'

}

originGroupOverride: null

typeName: 'DeliveryRuleRouteConfigurationOverrideActionParameters'

}

}

```

---

## <a name="ModifyRequestHeader"></a> Modify request header

Use the **modify request header** action to modify the headers in the request when it's sent to your origin.

### Properties

| Property | Supported values |

|-------|------------------|

| Operator | <ul><li>**Append:** The specified header gets added to the request with the specified value. If the header is already present, the value is appended to the existing header value using string concatenation. No delimiters are added. In ARM templates, use the `headerAction` of `Append`.</li><li>**Overwrite:** The specified header gets added to the request with the specified value. If the header is already present, the specified value overwrites the existing value. In ARM templates, use the `headerAction` of `Overwrite`.</li><li>**Delete:** If the header specified in the rule is present, the header gets deleted from the request. In ARM templates, use the `headerAction` of `Delete`.</li></ul> |

| Header name | The name of the header to modify. |

| Header value | The value to append or overwrite. |

### Example

In this example, we append the value `AdditionalValue` to the `MyRequestHeader` request header. If the origin set the response header to a value of `ValueSetByClient`, then after this action is applied, the request header would have a value of `ValueSetByClientAdditionalValue`.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "ModifyRequestHeader",

"parameters": {

"headerAction": "Append",

"headerName": "MyRequestHeader",

"value": "AdditionalValue",

"typeName": "DeliveryRuleHeaderActionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'ModifyRequestHeader'

parameters: {

headerAction: 'Append'

headerName: 'MyRequestHeader'

value: 'AdditionalValue'

typeName: 'DeliveryRuleHeaderActionParameters'

}

}

```

---

> [!NOTE]

> Certain Azure Front Door reserved headers can't be modified using rules engine actions, including the actions to modify request headers and response headers. The following list of reserved headers can't be modified, along with any headers prefixed with `x-ec` and `x-fd`.

>

> * `Accept-Ranges`

> * `Host`

> * `Connection`

> * `Content-Length`

> * `Transfer-Encoding`

> * `TE`

> * `Last-Modified`

> * `Keep-Alive`

> * `Expect`

> * `Upgrade`

> * `If-Modified-Since`

> * `If-Unmodified-Since`

> * `If-None-Match`

> * `If-Match`

> * `Range`

> * `If-Range`

> * `X-Ms-Via`

> * `X-Ms-Force-Refresh`

> * `X-MSEdge-Ref`

> * `Warning`

> * `Forwarded`

> * `Via`

> * `X-Forwarded-For`

> * `X-Forwarded-Proto`

> * `X-Forwarded-Host`

> * `X-Azure-RequestChain`

> * `X-Azure-FDID`

> * `X-Azure-RequestChainv2`

> * `X-Azure-Ref`

## <a name="ModifyResponseHeader"></a> Modify response header

Use the **modify response header** action to modify headers that are present in responses before they're returned to your clients.

### Properties

| Property | Supported values |

|-------|------------------|

| Operator | <ul><li>**Append:** The specified header gets added to the response with the specified value. If the header is already present, the value is appended to the existing header value using string concatenation. No delimiters are added. In ARM templates, use the `headerAction` of `Append`.</li><li>**Overwrite:** The specified header gets added to the response with the specified value. If the header is already present, the specified value overwrites the existing value. In ARM templates, use the `headerAction` of `Overwrite`.</li><li>**Delete:** If the header specified in the rule is present, the header gets deleted from the response.  In ARM templates, use the `headerAction` of `Delete`.</li></ul> |

| Header name | The name of the header to modify. |

| Header value | The value to append or overwrite. |

### Example

In this example, we delete the header with the name `X-Powered-By` from the responses before they're returned to the client.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "ModifyResponseHeader",

"parameters": {

"headerAction": "Delete",

"headerName": "X-Powered-By",

"typeName": "DeliveryRuleHeaderActionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'ModifyResponseHeader'

parameters: {

headerAction: 'Delete'

headerName: 'X-Powered-By'

typeName: 'DeliveryRuleHeaderActionParameters'

}

}

```

---

> [!NOTE]

> Certain Azure Front Door reserved headers can't be modified using rules engine actions, including the actions to modify request headers and response headers. The following list of reserved headers can't be modified, along with any headers prefixed with `x-ec` and `x-fd`.

>

> * `Accept-Ranges`

> * `Host`

> * `Connection`

> * `Content-Length`

> * `Transfer-Encoding`

> * `TE`

> * `Last-Modified`

> * `Keep-Alive`

> * `Expect`

> * `Upgrade`

> * `If-Modified-Since`

> * `If-Unmodified-Since`

> * `If-None-Match`

> * `If-Match`

> * `Range`

> * `If-Range`

> * `X-Ms-Via`

> * `X-Ms-Force-Refresh`

> * `X-MSEdge-Ref`

> * `Warning`

> * `Forwarded`

> * `Via`

> * `X-Forwarded-For`

> * `X-Forwarded-Proto`

> * `X-Forwarded-Host`

> * `X-Azure-RequestChain`

> * `X-Azure-FDID`

> * `X-Azure-RequestChainv2`

> * `X-Azure-Ref`

## <a name="UrlRedirect"></a> URL redirect

Use the **URL redirect** action to redirect clients to a new URL. Clients are sent a redirection response from Front Door. Azure Front Door supports dynamic capture of URL path with `{url_path:seg#}` server variable, and converts URL path to lowercase or uppercase with `{url_path.tolower}` or `{url_path.toupper}`. For more information, see [Server variables](rule-set-server-variables.md).

### Properties

| Property | Supported values |

|----------|------------------|

| Redirect type | The response type to return to the requester. <ul><li>In the Azure portal: Found (302), Moved (301), Temporary Redirect (307), Permanent Redirect (308).</li><li>In ARM templates: `Found`, `Moved`, `TemporaryRedirect`, `PermanentRedirect`</li></ul> |

| Redirect protocol | <ul><li>In the Azure portal: `Match Request`, `HTTP`, `HTTPS`</li><li>In ARM templates: `MatchRequest`, `Http`, `Https`</li></ul> |

| Destination host | The host name you want the request to be redirected to. Leave blank to preserve the incoming host. |

| Destination path | The path to use in the redirect. Include the leading `/`. Leave blank to preserve the incoming path. |

| Query string | The query string used in the redirect. Don't include the leading `?`. Leave blank to preserve the incoming query string. |

| Destination fragment | The fragment to use in the redirect. Leave blank to preserve the incoming fragment. |

### Example

In this example, we redirect the request to `https://contoso.com/exampleredirection?clientIp={client_ip}`, while preserving the fragment. An HTTP Temporary Redirect (307) is used. The IP address of the client is used in place of the `{client_ip}` token within the URL by using the `client_ip` [server variable](rule-set-server-variables.md).

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "UrlRedirect",

"parameters": {

"redirectType": "TemporaryRedirect",

"destinationProtocol": "Https",

"customHostname": "contoso.com",

"customPath": "/exampleredirection",

"customQueryString": "clientIp={client_ip}",

"typeName": "DeliveryRuleUrlRedirectActionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'UrlRedirect'

parameters: {

redirectType: 'TemporaryRedirect'

destinationProtocol: 'Https'

customHostname: 'contoso.com'

customPath: '/exampleredirection'

customQueryString: 'clientIp={client_ip}'

typeName: 'DeliveryRuleUrlRedirectActionParameters'

}

}

```

---

## <a name="UrlRewrite"></a> URL rewrite

Use the **URL rewrite** action to rewrite the path of a request that's en route to your origin. Azure Front Door supports dynamic capture of URL path with `{url_path:seg#}` server variable, and converts URL path to lowercase or uppercase with `{url_path.tolower}` or `{url_path.toupper}`. For more information, see [Server variables](rule-set-server-variables.md).

### Properties

| Property | Supported values |

|----------|------------------|

| Source pattern | Define the source pattern in the URL path to replace. Currently, source pattern uses a prefix-based match. To match all URL paths, use a forward slash (`/`) as the source pattern value. Note that only the path after the patterns to match in the route configuration is taken into consideration for the source pattern. For more information, see [source pattern.](front-door-url-rewrite.md?pivots=front-door-standard-premium#source-pattern) |

| Destination | Define the destination path to use in the rewrite. The destination path overwrites the source pattern. |

| Preserve unmatched path | If set to _Yes_, the remaining path after the source pattern is appended to the new destination path. |

### Example

In this example, we rewrite all requests to the path `/redirection`, and don't preserve the remainder of the path.

# [Portal](#tab/portal)

# [JSON](#tab/json)

```json

{

"name": "UrlRewrite",

"parameters": {

"sourcePattern": "/",

"destination": "/redirection",

"preserveUnmatchedPath": false,

"typeName": "DeliveryRuleUrlRewriteActionParameters"

}

}

```

# [Bicep](#tab/bicep)

```bicep

{

name: 'UrlRewrite'

parameters: {

sourcePattern: '/'

destination: '/redirection'

preserveUnmatchedPath: false

typeName: 'DeliveryRuleUrlRewriteActionParameters'

}

}

```

---

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

In Azure Front Door (classic), a [Rules engine](front-door-rules-engine.md) can consist up to 25 rules containing matching conditions and associated actions. This article provides a detailed description of each action you can define in a rule.

An action defines the behavior that gets applied to the request type that matches the condition or set of match conditions. In the Rules engine configuration, a rule can have up to 10 matching conditions and 5 actions. You can only have one *Override Routing Configuration* action in a single rule.

The following actions are available to use in Rules engine configuration.

## Modify request header

Use these actions to modify headers that are present in requests sent to your backend.

### Required fields

| Action | HTTP header name | Value |

| ------ | ---------------- | ----- |

| Append | When this option gets selected and the rule matches, the header specified in **Header name** gets added to the request with the specified value. If the header is already present, the value is appended to the existing value. | String |

| Overwrite | When this option is selected and the rule matches, the header specified in **Header name** gets added to the request with the specified value. If the header is already present, the specified value overwrites the existing value. | String |

| Delete | When this option gets selected with matching rules and the header specified in the rule is present, the header gets deleted from the request. | String |

## Modify response header

Use these actions to modify headers that are present in responses returned to your clients.

### Required fields

| Action | HTTP Header name | Value |

-------|------------------|------

| Append | When this option gets selected and the rule matches, the header specified in **Header name** gets added to the response by using the specified **Value**. If the header is already present, **Value** is appended to the existing value. | String |

| Overwrite | When this option is selected and the rule matches, the header specified in **Header name** is added to the response by using the specified **Value**. If the header is already present, **Value** overwrites the existing value. | String |

| Delete | When this option gets selected with matching rules and the header specified in the rule is present, the header gets deleted from the response. | String |

## Route configuration overrides

### Route Type: Redirect

Use these actions to redirect clients to a new URL.

#### Required fields

| Field | Description |

| ----- | ----------- |

| Redirect type | Redirect is a way to send users/clients from one URL to another. A redirect type sets the status code used by clients to understand the purpose of the redirect. <br><br/>You can select the following redirect status codes: Found (302), Moved (301), Temporary redirect (307), and Permanent redirect (308). |

| Redirect protocol | Retain the protocol as per the incoming request, or define a new protocol for the redirection. For example, select 'HTTPS' for HTTP to HTTPS redirection. |

| Destination host | Set this value to change the hostname in the URL for the redirection or otherwise retain the hostname from the incoming request. |

| Destination path | Either retain the path as per the incoming request, or update the path in the URL for the redirection. |

| Query string | Set this value to replace any existing query string from the incoming request URL or otherwise retain the original set of query strings. |

| Destination fragment | The destination fragment is the portion of URL after '#', normally used by browsers to land on a specific section on a page. Set this value to add a fragment to the redirect URL. |

### Route Type: Forward

Use these actions to forward clients to a new URL. These actions also contain sub actions for URL rewrites and caching.

| Field | Description |

| ----- | ----------- |

| Backend pool | Select the backend pool to override and serve the requests, you see all your preconfigured backend pools currently in your Front Door profile. |

| Forwarding protocol | Protocol to use for forwarding request to backend or match the protocol from incoming request. |

| URL rewrite | Path to use when constructing the request for URL rewrite to forward to the backend. |

| Caching | Enable caching for this routing rule. When enabled, Azure Front Door caches your static content. |

#### URL rewrite

Use this setting to configure an optional **Custom Forwarding Path** to use when constructing the request to forward to the backend.

| Field | Description |

| ----- | ----------- |

| Custom forwarding path | Define a path for which requests get forwarded to. |

#### Caching

Use these settings to control how files get cached for requests that contain query strings. Whether to cache your content based on all parameters or on selected parameters. You can use these settings to overwrite the time to live (TTL) value to control how long contents stay in cache. To force caching as an action, set the caching field to "Enabled." When you force caching, the following options appear:

| Cache behavior |  Description |

| -------------- | ------------ |

| Ignore Query String | Once the asset is cached, all ensuing requests ignore the query strings until the cached asset expires. |

| Use Query String | Each request with a unique URL, including the query string, is treated as a unique asset with its own cache. |

| Ignore Specified Query Strings | Request URL query strings listed in "Query parameters" setting are ignored for caching. |

| Include Specified Query Strings | Request URL query strings listed in "Query parameters" setting are used for caching. |

| Other fields |  Description

------------------|---------------

| Dynamic compression | Front Door can dynamically compress content on the edge, resulting in a smaller and faster response. |

| Query parameters | A comma-separated list of allowed or disallowed parameters to use as a basis for caching.

| Use default cache duration | Set to use Azure Front Door default caching duration or define a caching duration that ignores the origin response directive. |

## Next steps

- Learn how to configure your first [Rule set](front-door-tutorial-rules-engine.md).

- Learn more about [Rule set match conditions](front-door-rules-engine-match-conditions.md).

- Learn more about [Azure Front Door Rule sets](front-door-rules-engine.md).


# How To Configure Rule Set

# Configure rule sets in Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

This article demonstrates how to create rule sets and your first set of rules using the Azure portal. You also learn how to associate a rule set to a route from the rule sets page or from the Front Door manager.

## Prerequisites

* Before configuring rule sets, you must first create an Azure Front Door Standard or Premium profile. For more information, see [create an Azure Front Door profile](../create-front-door-portal.md).

## Configure Rule Set in Azure portal

1. Go to your Azure Front Door profile. Select **Rule sets** under *Settings* in the left side menu pane. Select **+ Add**, then give the rule set a name.

1. To create your first rule, give it a name. Then select **+ Add condition** and **+ Add action** to define your rule. You can add up to 10 conditions and 5 actions for one rule. In this example, we use a server variable to append "Device type" to the response header for requests coming from a "Mobile" device type. For more information, see [match conditions](../rules-match-conditions.md) and [actions](../front-door-rules-engine-actions.md).

> [!NOTE]

> * To delete a condition or action from a rule, use the trash can icon on the right-hand side of the specific condition or action.

> * To create a rule that applies to all incoming traffic, do not specify any conditions.

> * To stop evaluating remaining rules if a specific rule is met, check **Stop evaluating remaining rule**. If this option is checked, all remaining rules in that Rule Set, as well as all remaining Rule Sets associated with the route, will not be executed regardless of the matching conditions being met.

> * All paths in Rules Engine are case-sensitive.

> * Header names should adhere to [RFC 7230](https://datatracker.ietf.org/doc/html/rfc7230#section-3.2.6).

1. You can set the priority of the rules within your Rule Set by using the arrow buttons to move the rules up or down. The list is in ascending order, so the highest priority rule is listed first.

> [!TIP]

> To verify when changes are propagated to Azure Front Door, create a custom response header in the rule using the following example. Add a response header `_X-<RuleName>-Version_` and change the value each time the rule is updated.

>

> :::image type="content" source="./../media/front-door-rules-engine/rules-version.png" alt-text="Screenshot of custom version header rule." lightbox="./../media/front-door-rules-engine/rules-version-expanded.png":::

> After the changes are updated, go to the URL to confirm the rule version being invoked:

> :::image type="content" source="./../media/front-door-rules-engine/version-output.png" alt-text="Screenshot of custom header version output.":::

1. Once you create all the rules you need, select **Save** to complete the creation of your rule set.

1. Now you can associate the rule set to a route so it can take effect. You can associate the rule set on the Rule sets page or from the Front Door manager.

**Rule set page**:

1. On the *Rule set page*, select the **Unassociated** link to associate the rule set to a route.

1. On the **Associate a route** page, select the endpoint and route you want to associate the rule set with.

1. Select **Next** to change the rule set order if you have multiple rule sets for the selected route. The rule sets process in the order listed. You can change the order by selecting the rule set and using the buttons at the top of the page. Select **Associate** to complete the route association.

> [!NOTE]

> You can only associate one rule set with a single route on this page. To associate a rule set with another route, use the Front Door manager.

1. The rule set is now associated with a route. You can check the response header to confirm that the Device Type is added.

**Front Door manager**:

1. In the Front Door manager, select the **...** next to the route you want to configure, then select **Edit route**.

1. On the **Update route** page, under *Rules*, select the rule sets you want to associate with the route from the dropdown. You can also change the order of the rule sets.

1. Select **Update** to save the route configuration.

## Delete a rule set

If you no longer need a rule set in your Azure Front Door profile, follow these steps to remove it:

1. Navigate to the **Rule set** page under *Settings*.

1. Select the **...** next to the rule set you want to remove and select **Disassociate from all routes**.

1. After the rule set is disassociated, select the **...** again. Select **Delete** and then confirm by selecting **Yes**.

1. Repeat these steps to remove any other rule sets in your Azure Front Door profile.

## Next steps

Learn how to add [Security headers with rules Set](how-to-add-security-headers.md).


# Front Door Add Rules Cli

# Tutorial: Add and customize delivery rules for Azure Front Door Standard/Premium with Azure CLI

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Azure Front Door Standard/Premium  is a fast and secure modern cloud CDN.  Azure Front Door uses the Microsoft global edge network and integrates with intelligent threat protection. Azure Front Door Standard focuses on content delivery. Azure Front Door Premium adds extensive security capabilities and customization. This tutorial focuses on creating an Azure Front Door profile, then adding delivery rules for more granular control over your web app behaviors.

In this tutorial, you learn how to:

> [!div class="checklist"]

> - Create an Azure Front Door profile.

> - Create two instances of a web app.

> - Create a new security policy.

> - Verify connectivity to your web apps.

> - Create a rule set.

> - Create a rule and add it to the rule set.

> - Add actions or conditions to your rules.

[!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment](~/reusable-content/azure-cli/azure-cli-prepare-your-environment.md)]

## Create an Azure Front Door

### Create a resource group

For this quickstart, you'll need two resource groups. One in *Central US* and the second in *East US*.

Run [az group create](/cli/azure/group#az-group-create) to create resource groups.

```azurecli

az group create \

--name myRGFDCentral \

--location centralus

az group create \

--name myRGFDEast \

--location eastus

```

### Create an Azure Front Door profile

Run [az afd profile create](/cli/azure/afd/profile#az-afd-profile-create) to create an Azure Front Door profile.

```azurecli

az afd profile create \

--profile-name contosoafd \

--resource-group myRGFDCentral \

--sku Premium_AzureFrontDoor \

--subscription mysubscription

```

### Create two instances of a web app

You need two instances of a web application that run in different Azure regions for this tutorial. Both the web application instances run in Active/Active mode, so either one can service traffic.

If you don't already have a web app, use the following script to set up two example web apps.

#### Create app service plans

Before you can create the web apps, you must have two app service plans, one in *Central US* and the second in *East US*.

Run [az appservice plan create](/cli/azure/appservice/plan#az-appservice-plan-create&preserve-view=true) to create your app service plans.

```azurecli

az appservice plan create \

--name myAppServicePlanCentralUS \

--resource-group myRGFDCentral

az appservice plan create \

--name myAppServicePlanEastUS \

--resource-group myRGFDEast

```

#### Create web apps

Run [az webapp create](/cli/azure/webapp#az-webapp-create&preserve-view=true) to create a web app in each of the app service plans in the previous step. Web app names have to be globally unique.

Run [az webapp list-runtimes](/cli/azure/webapp#az-webapp-create&preserve-view=true) to see a list of built-in stacks for web apps.

```azurecli

az webapp create \

--name WebAppContoso-001 \

--resource-group myRGFDCentral \

--plan myAppServicePlanCentralUS \

--runtime "DOTNETCORE|2.1"

az webapp create \

--name WebAppContoso-002 \

--resource-group myRGFDEast \

--plan myAppServicePlanEastUS \

--runtime "DOTNETCORE|2.1"

```

Make note of the default host name of each web app so you can define the backend addresses when you deploy the Front Door in the next step.

### Add an endpoint

Run [az afd endpoint create](/cli/azure/afd/endpoint#az-afd-endpoint-create) to create an endpoint in your profile. You can create multiple endpoints in your profile after finishing the create experience.

```azurecli

az afd endpoint create \

--resource-group myRGFDCentral \

--endpoint-name contoso-frontend \

--profile-name contosoafd \

--origin-response-timeout-seconds 60 \

--enabled-state Enabled

```

### Create an origin group

Run [az afd origin-group create](/cli/azure/afd/origin-group#az-afd-origin-group-create) to create an origin group that contains your two web apps.

```azurecli

az afd origin-group create \

--resource-group myRGFDCentral \

--origin-group-name og1 \

--profile-name contosoafd \

--probe-request-type GET \

--probe-protocol Http \

--probe-interval-in-seconds 120 \

--probe-path /test1/azure.txt \

--sample-size 4 \

--successful-samples-required 3 \

--additional-latency-in-milliseconds 50

```

#### Add origins to the group

Run [az afd origin create](/cli/azure/afd/origin#az-afd-origin-create) to add an origin to your origin group.

```azurecli

az afd origin create \

--resource-group myRGFDCentral \

--host-name webappcontoso-1.azurewebsites.net

--profile-name contosoafd \

--origin-group-name og1 \

--origin-name contoso1 \

--origin-host-header webappcontoso-1.azurewebsites.net \

--priority 1 \

--weight 1000 \

--enabled-state Enabled \

--http-port 80 \

--https-port 443

```

Repeat this step and add your second origin.

```azurecli

az afd origin create \

--resource-group myRGFDCentral \

--host-name webappcontoso-2.azurewebsites.net

--profile-name contosoafd \

--origin-group-name og1 \

--origin-name contoso2 \

--origin-host-header webappcontoso-2.azurewebsites.net \

--priority 1 \

--weight 1000 \

--enabled-state Enabled \

--http-port 80 \

--https-port 443

```

### Add a route

Run [az afd route create](/cli/azure/afd/route#az-afd-route-create) to map your frontend endpoint to the origin group. This route forwards requests from the endpoint to *og1*.

```azurecli

az afd route create \

--resource-group myRGFDCentral \

--endpoint-name contoso-frontend \

--profile-name contosoafd \

--route-name route1 \

--https-redirect Enabled \

--origin-group og1 \

--supported-protocols Https \

--link-to-default-domain Enabled \

--forwarding-protocol MatchRequest

```

## Create a new security policy

### Create a WAF policy

Run [az network front-door waf-policy create](/cli/azure/network/front-door/waf-policy#az-network-front-door-waf-policy-create) to create a WAF policy for one of your resource groups.

Create a new WAF policy for your Front Door. This example creates a policy that's enabled and in prevention mode.

```azurecli

az network front-door waf-policy create

--name contosoWAF /

--resource-group myRGFDCentral /

--sku Premium_AzureFrontDoor

--disabled false /

--mode Prevention

```

> [!NOTE]

> If you select `Detection` mode, your WAF doesn't block any requests.

### Create the security policy

Run [az afd security-policy create](/cli/azure/afd/security-policy#az-afd-security-policy-create) to apply your WAF policy to the endpoint's default domain.

```azurecli

az afd security-policy create \

--resource-group myRGFDCentral \

--profile-name contosoafd \

--security-policy-name contososecurity \

--domains /subscriptions/mysubscription/resourcegroups/myRGFDCentral/providers/Microsoft.Cdn/profiles/contosoafd/afdEndpoints/contoso-frontend.z01.azurefd.net \

--waf-policy /subscriptions/mysubscription/resourcegroups/myRGFDCentral/providers/Microsoft.Network/frontdoorwebapplicationfirewallpolicies/contosoWAF

```

## Verify Azure Front Door

When you create the Azure Front Door Standard/Premium profile, it takes a few minutes for the configuration to be deployed globally. Once completed, you can access the frontend host you created. In a browser, go to `contoso-frontend.z01.azurefd.net`. Your request will automatically get routed to the nearest server from the specified servers in the origin group.

To test instant global failover, use the following steps:

1. Open a browser, and go to the frontend address: `contoso-frontend.azurefd.net`.

2. In the Azure portal, search for and select *App services*. Scroll down to find one of your web apps, **WebAppContoso-1** in this example.

3. Select your web app, and then select **Stop**, and **Yes** to verify.

4. Refresh your browser. You should see the same information page.

>[!TIP]

>Some delay is expected for this action. You might need to refresh again.

5. Find the other web app, and stop it as well.

6. Refresh your browser. This time, you should see an error message.

## Create a rule set

Create a rule set to customize how HTTP requests are handled at the edge. Delivery rules added to the rule set provide more control over your web application behaviors. Run [az afd rule-set create](/cli/azure/afd/rule-set#az-afd-rule-set-create) to create a rule set in your Azure Front Door profile.

```azurecli

az afd rule-set create \

--profile-name contosoafd \

--resource-group myRGFDCentral \

--rule-set-name contosorules

```

## Create a delivery rule and add it to your rule set

Create a new delivery rule within your rule set. Run [az afd rule create](/cli/azure/afd/rule#az-afd-rule-create) to create a delivery rule in your rule set. For this example, we'll create a rule for an http to https redirect.

```azurecli

az afd rule create \

--resource-group myRGFDCentral \

--rule-set-name contosorules \

--profile-name contosoafd \

--order 1 \

--match-variable RequestScheme \

--operator Equal \

--match-values HTTP \

--rule-name "redirect" \

--action-name "UrlRedirect" \

--redirect-protocol Https \

--redirect-type Moved

```

## Add an action or condition to your delivery rule

You might find that you need to further customize your new delivery rule. You can add actions or conditions as needed after creation. Run [az afd rule action add](/cli/azure/afd/rule/action#az-afd-rule-action-add) or [az afd rule condition add](/cli/azure/afd/rule/condition#az-afd-rule-condition-add) to update your rule.

### Add an action

```azurecli

az afd rule action add \

--resource-group myRGFDCentral \

--rule-set-name contosorules \

--profile-name contosoafd \

--rule-name redirect \

--action-name "CacheExpiration" \

--cache-behavior BypassCache

```

### Add a condition

```azurecli

az afd rule condition add \

--resource-group myRGFDCentral \

--rule-set-name contosorules \

--profile-name contosoafd \

--rule-name redirect \

--match-variable RemoteAddress \

--operator GeoMatch \

--match-values "TH"

```

## Clean up resources

When you don't need the resources for the Front Door, delete both resource groups. Deleting the resource groups also deletes the Front Door and all its related resources.

Run [az group delete](/cli/azure/group#az-group-delete&preserve-view=true):

```azurecli

az group delete \

--name myRGFDCentral

az group delete \

--name myRGFDEast

```


# Rules Engine Scenarios

# Azure Front Door rules engine scenarios and configurations

The Azure Front Door rules engine allows users to easily customize processing and routing logic at the Front Door edge by configuring match condition and action pairs.

You can define various rule [actions](front-door-rules-engine-actions.md) based on combination of 19 supported match conditions from incoming requests. These rules allow you to:

1.	Manage cache policy dynamically

1.	Forward requests to different origins or versions

1.	Modify request or response headers to hide sensitive information or passthrough important information through headers. For example, implementing security headers to prevent browser-based vulnerabilities like:

- HTTP strict-transport-security (HSTS)

- X-XSS-protection

- Content-security-policy

- X-frame-options

- Access-Control-Allow-Origin headers for cross-origin resource sharing (CORS) scenarios.

Security-based attributes can also be defined with cookies.

1.	Rewrite URL paths or redirect requests to new destinations

1.	Enable complex scenarios using regex and server variables: capture dynamic values from incoming requests or responses, and combine them with static strings or other variables.

This article covers common use cases supported by the Azure Front Door rules engine, and provides detailed configuration examples to meet various business and technical requirements.

## Scenario 1: Redirect using query string, URL path segments, or incoming hostname captures

Managing redirects is critical for search engine optimization (SEO), user experience, and the proper functioning of a website. Azure Front Door's rules engine and server variables allow you to efficiently manage batch redirects based on various parameters.

- **Redirect based on query string parameters:** You can redirect requests using query fields of the incoming URL by capturing the value of a specific query string key in the format `{http_req_arg_<key>}`.

For example, extract the value of `cdpb` query key from an incoming URL: `https://example.mydomain.com/testcontainer/123.zip?sig=fffff&cdpb=teststorageaccount` and use it to configure the *Destination host* into outgoing URL: `https://teststorageaccount.blob.core.windows.net/testcontainer/123.zip?sig=fffff&cdpb=teststorageaccount`.

This approach enables dynamic redirects without having to create a separate rule for each `cdpb` value, significantly reducing the number of rules required.

# [**Portal**](#tab/portal)

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/RedirectQueryStringCapture')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]"

],

"properties": {

"order": 100,

"conditions": [],

"actions": [

{

"name": "UrlRedirect",

"parameters": {

"typeName": "DeliveryRuleUrlRedirectActionParameters",

"redirectType": "PermanentRedirect",

"destinationProtocol": "MatchRequest",

"customHostname": "{http_req_arg_cdpb}.blob.core.windows.net"

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

- **Redirect based on fixed-length URL path segments:** You can redirect requests to different origins based on fixed-length URL path segment by capturing the URL segments using `{variable:offset:length}`. For more information, see [Server variable format](/azure/frontdoor/rule-set-server-variables#server-variable-format).

For example, consider a scenario where the tenant ID is embedded in the URL segment and is always six characters long, such as: `https://api.contoso.com/{tenantId}/xyz`. To extract `{tenantId}` from the URL and decide the correct redirect to use in the format of `tenantId.backend.com/xyz`.

This approach eliminates the need to create a separate rule for each tenant ID, allowing you to handle dynamic routing with fewer rules.

# [**Portal**](#tab/portal)

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/RedirectURLSegmentCapture')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]"

],

"properties": {

"order": 101,

"conditions": [],

"actions": [

{

"name": "UrlRedirect",

"parameters": {

"typeName": "DeliveryRuleUrlRedirectActionParameters",

"redirectType": "PermanentRedirect",

"destinationProtocol": "MatchRequest",

"customPath": "/xyz",

"customHostname": "{url_path:0:6}.backend.com"

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

- **Redirect based on dynamic-length URL path segments:** When the URL path segment has a dynamic length, you can extract it using the `{url_path:seg#}`. For more information, see [Server variable format](/azure/frontdoor/rule-set-server-variables#server-variable-format).

For example, if a tenant ID or location is embedded in the URL segment, such as: `https://api.contoso.com/{tenantId}/xyz`, you can extract `{tenantId}` from the URL and decide the correct redirect in the format of `tenantId.backend.com/xyz` with server variable `{url_path:seg0}.backend.com` in the redirect destination host.

This method avoids creating separate rules for each tenant ID, enabling more efficient configuration.

# [**Portal**](#tab/portal)

N/A

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/RedirectURLSegmentCapture')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]"

],

"properties": {

"order": 101,

"conditions": [],

"actions": [

{

"name": "UrlRedirect",

"parameters": {

"typeName": "DeliveryRuleUrlRedirectActionParameters",

"redirectType": "PermanentRedirect",

"destinationProtocol": "MatchRequest",

"customPath": "/xyz",

"customHostname": "{url_path:seg0}.backend.com"

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

- **Redirect based on part of the incoming hostname:** You can redirect requests to different origins by extracting part of the incoming hostname.

For example, you can capture `tenantName` from `https://[tenantName].poc.contoso.com/GB` to redirect the request to `s1.example.com/Buyer/Main?realm=[tenantName]&examplename=example1` using the offset and length in server variable in the format of `{hostname:0:-16}`. For more information, see [Server variable format](/azure/frontdoor/rule-set-server-variables#server-variable-format).

# [**Portal**](#tab/portal)

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/RedirectHostnameCapture')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]"

],

"properties": {

"order": 102,

"conditions": [

{

"name": "HostName",

"parameters": {

"typeName": "DeliveryRuleHostNameConditionParameters",

"operator": "EndsWith",

"negateCondition": false,

"matchValues": [

"poc.contoso.com"

],

"transforms": []

}

}

],

"actions": [

{

"name": "UrlRedirect",

"parameters": {

"typeName": "DeliveryRuleUrlRedirectActionParameters",

"redirectType": "PermanentRedirect",

"destinationProtocol": "MatchRequest",

"customQueryString": "realm={hostname:0:-16}&examplename=example1",

"customPath": "/Buyer/Main",

"customHostname": "s1.example.com"

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

## Scenario 2: Populate or modify a response header based on a request header value

In some scenarios, you might need to populate or modify a response header based on a request header value.

For example, you can add CORS header where needed to serve scripts on multiple origins from the same CDN domain, and response must contain the same FQDN in `Access-Control-Allow-Origin` header as the request origin header, rather than a wildcard allowing all domains (*) to enhance security. You can achieve it by using the `{http_req_header_Origin}` server variable to set the response header.

# [**Portal**](#tab/portal)

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/OverwriteRespHeaderUsingReqHeaderCapture')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]"

],

"properties": {

"order": 103,

"conditions": [

{

"name": "RequestHeader",

"parameters": {

"typeName": "DeliveryRuleRequestHeaderConditionParameters",

"operator": "Contains",

"selector": "Origin",

"negateCondition": false,

"matchValues": [

"my-domain-01.com"

],

"transforms": []

}

}

],

"actions": [

{

"name": "ModifyResponseHeader",

"parameters": {

"typeName": "DeliveryRuleHeaderActionParameters",

"headerAction": "Overwrite",

"headerName": "Access-Control-Allow-Origin",

"value": "{http_req_header_Origin}"

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

## Scenario 3: Rename a response header to a brand-specific one

You can rename a response header generated by a cloud provider by adding a new custom response header and deleting the original.

For example, you can replace the response header `X-Azure-Backend-ID` with a brand-specific header `X-Contoso-Scale-ID`.

# [**Portal**](#tab/portal)

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/RenameResponseHeaders')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]"

],

"properties": {

"order": 104,

"conditions": [],

"actions": [

{

"name": "ModifyResponseHeader",

"parameters": {

"typeName": "DeliveryRuleHeaderActionParameters",

"headerAction": "Append",

"headerName": "X-Contoso-Scale-ID",

"value": "{http_resp_header_X-Azure-Backend-ID}"

}

},

{

"name": "ModifyResponseHeader",

"parameters": {

"typeName": "DeliveryRuleHeaderActionParameters",

"headerAction": "Delete",

"headerName": "X-Azure-Backend-ID"

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

## Scenario 4: A/B testing (experimentation)

Splitting incoming traffic into two origin groups can be is useful in A/B testing, rolling deployments, or load balancing without complex backend logic.

For example, you can split incoming traffic based on the client port number. A rule can match client ports that end in 1, 3, 5, 7, or 9 and forward those requests to an *experiment-origin-group*. All other traffic continues to the default origin group per route settings. The previous regex is just an example. You can explore and test your own expressions using tools like [regex101](https://regex101.com/).

> [!NOTE]

> Since client ports are random, this method typically results in an approximate 50/50 traffic split. However, the presence of any proxies or load balancers between clients and the Front Door might affect this assumption due to factors like connection reuse or source port rewriting. Use logs or metrics to validate the actual behavior in your environment.

# [**Portal**](#tab/portal)

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/ABExperimentation')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]",

"[resourceId('Microsoft.Cdn/profiles/origingroups', parameters('profiles_rulesengineblog_name'), 'experiment-origin-group')]"

],

"properties": {

"order": 105,

"conditions": [

{

"name": "ClientPort",

"parameters": {

"typeName": "DeliveryRuleClientPortConditionParameters",

"operator": "RegEx",

"negateCondition": false,

"matchValues": [

"^.*[13579]$"

],

"transforms": []

}

}

],

"actions": [

{

"name": "RouteConfigurationOverride",

"parameters": {

"typeName": "DeliveryRuleRouteConfigurationOverrideActionParameters",

"originGroupOverride": {

"originGroup": {

"id": "[resourceId('Microsoft.Cdn/profiles/origingroups', parameters('profiles_rulesengineblog_name'), 'experiment-origin-group')]"

},

"forwardingProtocol": "MatchRequest"

}

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

## Scenario 5: Redirect with URL path modification and preserve capability

In some scenarios, you might need to add new segments or remove some segments while preserving the rest of the URL path.

For example, if you want to redirect `https://domain.com/seg0/seg1/seg2/seg3` to `https://example.com/seg0/insert/seg2/seg3`. In this scenario, you replace URL path’s `{seg1}` with `/insert/` while preserving the rest of the URL path. Azure Front Door achieves the desired redirect by combining values extracted from server variables (URL segments) and combining static string segment `/insert/`. You can use `Int32.Max (2147483647)` for URL segment’s length field to keep all segments from *seg2* to *segn*. For more information, see [Server variable format](/azure/frontdoor/rule-set-server-variables#server-variable-format).

> [!NOTE]

> Similar configuration can be done for URL rewrite action by inputting source pattern as `/` and destination as `/{url_path:seg0}/insert/{url_path:seg2:2147483647}` for redirect action as shown in the following portal example.

# [**Portal**](#tab/portal)

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/redirectWithSegCap01')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]"

],

"properties": {

"order": 106,

"conditions": [],

"actions": [

{

"name": "UrlRedirect",

"parameters": {

"typeName": "DeliveryRuleUrlRedirectActionParameters",

"redirectType": "Found",

"destinationProtocol": "Https",

"customPath": "/{url_path:seg0}/insert/{url_path:seg2:2147483647}"

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

## Scenario 6: Redirect by removing fixed parts of a URL path

You can remove fixed segments of known size from a URL path, such as country codes (us) or locales (en-us), while preserving the rest of the URL path.

For example, if you want to redirect `https://domain.com/us/seg1/seg2/seg3/` to `https://example.com/seg1/seg2/seg3/`, you need to remove the country code `/us/` and keep the rest of the URL path unchanged.

To achieve this, use `{variable:offset} `, which includes the server variable after a specific offset, until the end of the variable. For more information, see [Server variable format](/azure/frontdoor/rule-set-server-variables#server-variable-format).

> [!NOTE]

> Similar configuration can be done for URL rewrite action by inputting source pattern as `/` and destination as `/“{url_path:3}` for redirect action as shown in the following portal example.

# [**Portal**](#tab/portal)

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/RedirectByRemovingFixedUrlLength')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]"

],

"properties": {

"order": 107,

"conditions": [

{

"name": "RequestUri",

"parameters": {

"typeName": "DeliveryRuleRequestUriConditionParameters",

"operator": "RegEx",

"negateCondition": false,

"matchValues": [

"\\/[a-zA-Z0-9]{2}\\/"

],

"transforms": []

}

}

],

"actions": [

{

"name": "UrlRedirect",

"parameters": {

"typeName": "DeliveryRuleUrlRedirectActionParameters",

"redirectType": "Found",

"destinationProtocol": "Https",

"customPath": "/{url_path:3}"

"customHostname": "example.com"

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

## Scenario 7: URL rewrite by removing one or more segments of URL path

You can remove one or more segments from a URL path, such as country codes (us) or locales (en-us), while preserving the rest of the URL path.

For example, if you want to rewrite `https://domain.com/us/seg1/seg2/seg3/` to `https://origin.com/seg2/seg3/`, you need to remove both the country code and an additional segment `/us/seg1/` while keeping the rest of the URL path intact.

To achieve this, use the `{url_path:seg#:length}` server variable format to capture specific URL segments starting from a particular segment number. In this example, use `{url_path:seg2:2147483647}` to capture all segments starting from `seg2` to the end. The value `2147483647` (Int32.Max) ensures all remaining segments are included. For more information, see [Server variable format](/azure/frontdoor/rule-set-server-variables#server-variable-format).

# [**Portal**](#tab/portal)

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/URLRewriteRemovingOneorMoreSegments')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]"

],

"properties": {

"order": 108,

"conditions": [],

"actions": [

{

"name": "UrlRewrite",

"parameters": {

"typeName": "DeliveryRuleUrlRewriteActionParameters",

"sourcePattern": "/",

"destination": "/{url_path:seg2:2147483647}",

"preserveUnmatchedPath": false

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

> [!NOTE]

> When using server variables like `{url_path}` in the **Destination** field, the **Preserve unmatched path** setting becomes less relevant because server variables give you explicit control over which parts of the URL path to include.

## Scenario 8: Use regex to reduce the number of rule conditions and avoid hitting limits

Using regex in rule conditions can significantly reduce the number of rules required, which helps avoid rule limits that can be a blocker for customers who need conditions or actions for hundreds of clients.

For example, if a customer wants to identify their clients with a specific ID pattern to allow access to a resource behind Azure Front Door, clients send a header like `x-client-id: SN1234-ABCD56`. This header follows a specific format: `x-client-id: <SN + 4 digits + - + 4 uppercase letters + 2 digits>`.

Instead of creating individual rules for each possible client ID, you can use a single regex pattern `^SN[0-9]{4}-[A-Z]{4}[0-9]{2}$` to match all valid client IDs in one rule, for example, `SN1234-ABCD56`, `SN0001-ZYXW99`, `SN2025-QWER12`, `SN9876-MNOP34`, `SN3141-TEST42`, etc. This approach allows you to handle hundreds of different client IDs with a single rule configuration.

# [**Portal**](#tab/portal)

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/UseRegexTogroupConditions')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]",

"[resourceId('Microsoft.Cdn/profiles/origingroups', parameters('profiles_rulesengineblog_name'), 'default-origin-group')]"

],

"properties": {

"order": 109,

"conditions": [

{

"name": "RequestHeader",

"parameters": {

"typeName": "DeliveryRuleRequestHeaderConditionParameters",

"operator": "RegEx",

"selector": "x-client-id",

"negateCondition": false,

"matchValues": [

"^SN[0-9]{4}-[A-Z]{4}[0-9]{2}$"

],

"transforms": []

}

}

],

"actions": [

{

"name": "RouteConfigurationOverride",

"parameters": {

"typeName": "DeliveryRuleRouteConfigurationOverrideActionParameters",

"originGroupOverride": {

"originGroup": {

"id": "[resourceId('Microsoft.Cdn/profiles/origingroups', parameters('profiles_rulesengineblog_name'), 'default-origin-group')]"

},

"forwardingProtocol": "MatchRequest"

}

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

> [!NOTE]

> You can use [regex101](https://regex101.com/) to test and validate your regex patterns before implementing them in Azure Front Door.

## Scenario 9: Modify origin redirects using response header captures

You can make action fields dynamic by using response header values as server variables. This is useful when origin servers issue redirects that reference their own domain names.

**The Problem:** Origin servers like Azure App Service commonly issue redirect URLs that reference their own domain name (for example, `contoso.azurewebsites.net`). If these URLs reach the client unmodified, the next request bypasses Azure Front Door, which disrupts the user's navigation experience.

**The Solution:** Capture the origin's `Location` header and rewrite just the host portion so it always reflects the hostname that the client originally used.

For example, if the frontend client's host header to Azure Front Door is `contoso.com` and the origin is `contoso.azurewebsites.net`, when the origin issues an absolute redirect URL like Location: `https://contoso.azurewebsites.net/login/`, you can modify the location header back to use the original hostname Location: `https://contoso.com/login/`

This is achieved using the server variable format: `https://{hostname}{http_resp_header_location:33}`, where:

- `{hostname}` represents the original client hostname (`contoso.com`)

- `{http_resp_header_location:33}` captures the Location header content starting from offset 33 (the `/login/` part)

For more information, see [Preserve the original HTTP host name between a reverse proxy and its back-end web application](/azure/architecture/best-practices/host-name-preservation).

# [**Portal**](#tab/portal)

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/RewriteLocationHeaderToModifyRedirect')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]"

],

"properties": {

"order": 110,

"conditions": [

{

"name": "UrlPath",

"parameters": {

"typeName": "DeliveryRuleUrlPathMatchConditionParameters",

"operator": "Contains",

"negateCondition": false,

"matchValues": [

"login",

"update"

],

"transforms": []

}

}

],

"actions": [

{

"name": "ModifyResponseHeader",

"parameters": {

"typeName": "DeliveryRuleHeaderActionParameters",

"headerAction": "Overwrite",

"headerName": "Location",

"value": " https://{hostname}{http_resp_header_location:33}"

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

> [!NOTE]

> - This rule can be used when rule condition is based on request parameters or when invoked unconditionally.

>

> - For consistent offset calculation, all origin servers in the origin group should have domain names of the same length, for example, all 33 characters like `https://contoso.azurewebsites.net`. Ideally, there should be just one origin server, but multiple origins are acceptable if their names have identical lengths.

>

> - You can apply the same server variable capture technique to extract and reuse request query string parameters in different rule actions.

## Scenario 10: If-elseif-else rules

The Azure Front Door rules engine doesn't natively support traditional conditional logic with "if-elseif-else" structures. By default, all rules are independently evaluated as "if condition1 then action1", "if condition2 then action2", and so forth. When multiple conditions are met simultaneously, multiple corresponding actions are executed.

However, you can emulate "if-elseif-else" logic by using the **Stop evaluating remaining rules** feature to create conditional branching that resembles:

- If condition1 is satisfied, execute action1 and stop

- Else if condition2 is satisfied (but condition1 is not), execute action2 and stop

- Else if condition3 is satisfied (but condition1 and condition2 are not), execute action3 and stop

- Else, execute a default action

**How it works:** When multiple conditions would normally be satisfied simultaneously, only the first matching rule executes because rule evaluation stops after the first match. This effectively simulates traditional conditional branching.

# [**Portal**](#tab/portal)

**Configuration steps:**

1. Create a new ruleset (for example, "IfElseifElseRuleset")

2. Create rules in priority order, with the most specific conditions first

3. For each rule, check the **Stop evaluating remaining rules** option

> [!IMPORTANT]

> The if-elseif-else paradigm only works if the ruleset is attached as the **final** ruleset for that route.

# [**ARM**](#tab/arm)

N/A

---

## Scenario 11: Remove query strings from incoming URLs using URL redirects

You can remove query strings from incoming URLs by implementing a 3xx URL redirect that guides users back to the Azure Front Door endpoint with the query strings removed.

> [!NOTE]

> Users will notice the change of the request URL with this operation.

The following example demonstrates how to remove the entire query string from incoming URLs. If you need to strip part of it, you can adjust the offset/length as desired. For more information, see [Server variable format](/azure/frontdoor/rule-set-server-variables#server-variable-format).

# [**Portal**](#tab/portal)

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/RemoveQueryStrings')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]"

],

"properties": {

"order": 111,

"conditions": [

{

"name": "QueryString",

"parameters": {

"typeName": "DeliveryRuleQueryStringConditionParameters",

"operator": "GreaterThan",

"negateCondition": false,

"matchValues": [

"0"

],

"transforms": []

}

}

],

"actions": [

{

"name": "UrlRedirect",

"parameters": {

"typeName": "DeliveryRuleUrlRedirectActionParameters",

"redirectType": "Moved",

"destinationProtocol": "MatchRequest",

"customQueryString": "{query_string:0:0}"

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

## Scenario 12: Append SAS token in query string to authenticate Azure Front Door to Azure Storage

You can protect files in your storage account by changing the access to your storage containers from public to private and using Shared Access Signatures (SAS) to grant restricted access rights to your Azure Storage resources from Azure Front Door without exposing your account key. You can also accomplish this using Managed Identity. For more information, see [Use managed identities to authenticate to origins](/azure/frontdoor/origin-authentication-with-managed-identities).

**How SAS token injection works:** Capture the incoming URL path and append the SAS token to the query string using redirect or rewrite rules. Since URL rewrite only acts on the path, use redirect rules when you need to modify query strings.

For example, if you want to append a SAS token to the incoming URL: `https://www.contoso.com/dccp/grammars/0.1.0-59/en-US/grammars/IVR/ssn0100_CollectTIN_QA_dtmf.grxml?version=1.0_1719342835399`, the rewrite URL will be: `https://www.contoso.com/grammars/0.1.0-59/en-US/grammars/IVR/ssn0100_CollectTIN_QA_dtmf.grxml?version=1.0_1719342835399&<SASTOKEN>`

In this example, the incoming URL already has query parameters, and you want to preserve the existing query string while appending the SAS token by configuring URL redirect using `/{url_path:seg1:20}?{query_string}&<SASToken>`.

The rule configuration redirects all HTTPS requests that don't already contain the SAS token (identified by the absence of `sp=rl` in the query string).

# [**Portal**](#tab/portal)

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/RedirectForAppendSASToken')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]"

],

"properties": {

"order": 100,

"conditions": [

{

"name": "RequestScheme",

"parameters": {

"typeName": "DeliveryRuleRequestSchemeConditionParameters",

"matchValues": [

"HTTPS"

],

"operator": "Equal",

"negateCondition": false,

"transforms": []

}

},

{

"name": "QueryString",

"parameters": {

"typeName": "DeliveryRuleQueryStringConditionParameters",

"operator": "Contains",

"negateCondition": true,

"matchValues": [

"sp=rl"

],

"transforms": []

}

}

],

"actions": [

{

"name": "UrlRedirect",

"parameters": {

"typeName": "DeliveryRuleUrlRedirectActionParameters",

"redirectType": "Found",

"destinationProtocol": "MatchRequest",

"customQueryString": "{ {query_string}&<replace with your SAS token>",

"customPath": "/{url_path:seg1:20}"

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

> [!IMPORTANT]

> - Update your route configuration to ensure routes for `/grammars/*` are properly configured after the redirect

>

> - Replace the SAS token with the proper token. In the example, the SAS token starts with `sp=rl`, and you want to redirect all requests to apply this rule which doesn’t contain the `sp=rl`

## Scenario 13: Add security headers with rules engine

You can use the Azure Front Door rules engine to add security headers that help prevent browser-based vulnerabilities, such as HTTP Strict-Transport-Security (HSTS), X-XSS-Protection, Content-Security-Policy, and X-Frame-Options.

For example, you can add a *Content-Security-Policy* header to all incoming requests that match the path defined in the route associated with your rules engine configuration. In this configuration, use `script-src 'self' https://apiphany.portal.azure-api.net` as the header value to only allow scripts from the trusted site `https://apiphany.portal.azure-api.net` to run on the application. For more information, see [Add security headers with rules engine](/azure/frontdoor/front-door-security-headers#add-a-content-security-policy-header-in-azure-portal).

# [**Portal**](#tab/portal)

# [**ARM**](#tab/arm)

```json

{

"type": "Microsoft.Cdn/profiles/rulesets/rules",

"apiVersion": "2025-04-15",

"name": "[concat(parameters('profiles_rulesengineblog_name'), '/RulesBlogScenarios/ContentSecurityPolicyExample')]",

"dependsOn": [

"[resourceId('Microsoft.Cdn/profiles/rulesets', parameters('profiles_rulesengineblog_name'), 'RulesBlogScenarios')]",

"[resourceId('Microsoft.Cdn/profiles', parameters('profiles_rulesengineblog_name'))]"

],

"properties": {

"order": 100,

"conditions": [],

"actions": [

{

"name": "ModifyResponseHeader",

"parameters": {

"typeName": "DeliveryRuleHeaderActionParameters",

"headerAction": "Append",

"headerName": "Content-Security-Policy",

"value": "script-src 'self' https://apiphany.portal.azure-api.net"

}

}

],

"matchProcessingBehavior": "Continue"

}

}

```

---

## Related content

- [What is a rule set in Azure Front Door?](/azure/frontdoor/front-door-rules-engine)

- [Rule set actions](/azure/frontdoor/front-door-rules-engine-actions)

- [Configure rule sets in Azure Front Door](/azure/frontdoor/standard-premium/how-to-configure-rule-set)


# Rule Set Server Variables

# Azure Front Door Rule set server variables

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Rule set server variables provide access to structured information about the request when you work with [Rule sets](front-door-rules-engine.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json).

When you use [Rule set match conditions](rules-match-conditions.md), server variables are available as match conditions so that you can identify requests with specific properties.

When you use [Rule set actions](front-door-rules-engine-actions.md), you can use server variables to dynamically change the request and response headers, and rewrite URLs, paths, and query strings, for example, when a new page load or when a form gets posted.

> [!NOTE]

> Server variables are only available with Azure Front Door Standard and Premium tiers.

## Supported variables

| Variable name | Description |

|-|-|

| `socket_ip`      | The IP address of the direct connection to Azure Front Door edge. If the client used an HTTP proxy or a load balancer to send the request, the value of `socket_ip` is the IP address of the proxy or load balancer.<br/> To access this server variable in a match condition, use [Socket address](rules-match-conditions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#socket-address). |

| `client_ip`      | The IP address of the client that made the original request. If there was an `X-Forwarded-For` header in the request, then the client IP address is picked from the header.<br />To access this server variable in a match condition, use [Remote address](rules-match-conditions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#remote-address) and configure the *Operator* to *IP Match* or *IP Not Match*. |

| `client_port`    | The IP port of the client that made the request. <br/> To access this server variable in a match condition, use [Client port](rules-match-conditions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#client-port).|

| `hostname`       | The host name in the request from the client. <br/> To access this server variable in a match condition, use [Host name](rules-match-conditions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#host-name).|

| `geo_country`    | Indicates the requester's country/region of origin through its country/region code. <br/> To access this server variable in a match condition, use [Remote address](rules-match-conditions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#remote-address) and configure the *Operator* to *Geo Match* or *Geo Not Match*.|

| `http_method`    | The method used to make the URL request, such as `GET` or `POST`.<br/> To access this server variable in a match condition, use [Request method](rules-match-conditions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#request-method).|

| `http_version`   | The request protocol. Usually `HTTP/1.0`, `HTTP/1.1`, or `HTTP/2.0`.<br/> To access this server variable in a match condition, use [HTTP version](rules-match-conditions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#http-version).|

| `query_string`   | The list of variable/value pairs that follows the `?` in the requested URL.<br />For example, in the request `http://contoso.com:8080/article.aspx?id=123&title=fabrikam`, the `query_string` value is `id=123&title=fabrikam`.<br/> To access this server variable in a match condition, use [Query string](rules-match-conditions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#query-string).|

| `request_scheme` | The request scheme: `http` or `https`.<br/> To access this server variable in a match condition, use [Request protocol](rules-match-conditions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#request-protocol).|

| `request_uri`    | The full original request URI (with arguments).<br />For example, in the request `http://contoso.com:8080/article.aspx?id=123&title=fabrikam`, the `request_uri` value is `http://contoso.com:8080/article.aspx?id=123&title=fabrikam`.<br/> To access this server variable in a match condition, use [Request URL](rules-match-conditions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#request-url).|

| `ssl_protocol`   | The protocol of an established TLS connection.<br/> To access this server variable in a match condition, use [SSL protocol](rules-match-conditions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#ssl-protocol).|

| `server_port`    | The port of the server that accepted a request.<br/> To access this server variable in a match condition, use [Server port](rules-match-conditions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#server-port).|

| `url_path`       | Identifies the specific resource in the host that the web client wants to access. This is the part of the request URI without the arguments or leading slash.<br />For example, in the request `http://contoso.com:8080/article.aspx?id=123&title=fabrikam`, the `url_path` value is `article.aspx`. <br /> Azure Front Door supports dynamic capture of URL path with `{url_path:seg#}` server variable, and converts URL path to lowercase or uppercase with `{url_path.tolower}` or `{url_path.toupper}`. For more information, see [Server variable format](#server-variable-format) and [Server variables](rule-set-server-variables.md). <br/> To access this server variable in a match condition, use [Request path](rules-match-conditions.md#request-path) condition. |

| `http_req_header_<headername>`       | Captures the value of a request header. E.g. for request header Device: Desktop, the variable is http_req_header_Device, the value of this variable is Desktop. <br /> The header name in the variable syntax support alphanumeric and hyphen (a-z, A-Z, 0-9 and “-”).   |

| `http_req_arg_<querystringkeyname>`       | Captures the value from a query string key value pair. E.g. in the request `http://contoso.com:8080/article.aspx?id=123&title=fabrikam`, the variable is http_req_header_id, the value of this variable is 123.  <br /> The query string key in the variable syntax support alphanumeric and hyphen (a-z, A-Z, 0-9 and “-”).  |

| `http_resp_header_<headername>`       | Captures the value of a response header from origin. E.g. for a response header Access-Control-Allow-Origin `https://learn.microsoft.com`, the variable is http_req_header_ header Access-Control-Allow-Origin, the value of this variable is `https://learn.microsoft.com`. <br /> The header name in the variable syntax support alphanumeric and hyphen (a-z, A-Z, 0-9 and “-”). |

## Server variable format

When you work with Rule Set actions, specify server variables by using the following formats:

* `{variable}`: Include the entire server variable. For example, if the client IP address is `111.222.333.444` then the `{client_ip}` token would evaluate to `111.222.333.444`.

* `{variable:offset}`: Include the server variable after a specific offset, until the end of the variable. The offset is zero-based. For example, if the client IP address is `111.222.333.444` then the `{client_ip:3}` token would evaluate to `.222.333.444`.

* `{variable:offset:length}`: Include the server variable after a specific offset, up to the specified length. The offset is zero-based. For example, For example, when the variable var is 'AppId=01f592979c584d0f9d679db3e66a3e5e',

* Offsets within range, no lengths: `{var:0}` = `AppId=01f592979c584d0f9d679db3e66a3e5e`, `{var:6}` = `01f592979c584d0f9d679db3e66a3e5e`, `{var:-8}` = `e66a3e5e`

* Offsets out of range, no lengths: `{var:-128}` = `AppId=01f592979c584d0f9d679db3e66a3e5e`, `{var:128}` = null

* Offsets and lengths within range: `{var:0:5}` = `AppId`, `{var:7:7}` = `1f59297`, `{var:7:-7}` = `1f592979c584d0f9d679db3e`

* Zero lengths: `{var:0:0}` = null,  `{var:4:0}` = null

* Offsets within range and lengths out of range: `{var:0:100}` = `AppId=01f592979c584d0f9d679db3e66a3e5e`, `{var:5:100}` = `=01f592979c584d0f9d679db3e66a3e5e`,  `{var:0:-48}` = null,  `{var:4:-48}` = null

* To experiment with how {variable:offset:length} works, open a Linux bash terminal or use bash terminal in [Azure Cloud Shell](https://shell.azure.com/). Enter the following example into the terminal and examine the output to understand how the substring extraction behaves.

```azurecli-interactive

variable=helloworld123; echo ${variable:5} #Output = world123

```

```azurecli-interactive

variable=helloworld123; echo ${variable:0:5}  #Output = hello

```

> [!NOTE]

> In Bash, a space is required before a negative number in parameter expansion to avoid syntax errors.

```azurecli-interactive

variable=helloworld123; echo ${variable: -3:3} #Output=123

```

```azurecli-interactive

variable=helloworld123; echo ${variable:5: -3} #Output = world

```

* `{url_path:seg#}`: Allow users to capture and use the desired URL path segment in URL Redirect, URL Rewrite, or any meaningful action. User can also capture multiple segments by using the same style as substring capture `{url_path:seg1:3}`. For example, for a source pattern `/id/12345/default` and a URL rewrite Destination `/{url_path:seg1}/home`, the expected URL path after rewrite is `/12345/home`. For a multiple-segment capture, when the source pattern is `/id/12345/default/location/test`, a URL rewrite destination `/{url_path:seg1:3}/home` results in `/12345/default/location/home`. Segment capture includes the location path, so if route is `/match/*`, segment 0 will be match.

Offset corresponds to the index of the start segment, and length refers to how many segments to capture, including the one at index = offset.

Assuming offset and length are positive, the following logic applies:

* If length isn't included, capture the segment at index = offset.

* When length is included, capture segments from index = offset up till index = offset + length.

The following special cases are also handled:

* If offset is negative, count backwards from end of the path to get the starting segment.

* If offset is a negative value greater than or equal to the number of segments, set to 0.

* If offset is greater than the number of segments, the result is empty.

* If length is 0, the return the single segment specified by offset

* If length is negative, treat it as a second offset and calculate backwards from the end of the path. If the value is less than offset, it results in an empty string.

* If length is greater than the number of segments, return what remains in the path.

*  `{url_path.tolower}`/`{url_path.toupper}`: Convert the URL path to lowercase or uppercase. For example, a destination `{url_path.tolower}` in URL rewrite/redirect for `/lowercase/ABcDXyZ/EXAMPLE` results in `/lowercase/abcdxyz/example`. A destination `{url_path.toupper}` in URL rewrite/redirect for `/ABcDXyZ/example` results in `/ABCDXYZ/EXAMPLE`.

## Supported rule set actions

Server variables are supported on the following Rule set actions:

* Query string caching behavior in [Route configuration override](front-door-rules-engine-actions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#RouteConfigurationOverride)

* [Modify request header](front-door-rules-engine-actions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#ModifyRequestHeader)

* [Modify response header](front-door-rules-engine-actions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#ModifyResponseHeader)

* [URL redirect](front-door-rules-engine-actions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#UrlRedirect)

* [URL rewrite](front-door-rules-engine-actions.md?toc=%2fazure%2ffrontdoor%2fstandard-premium%2ftoc.json#UrlRewrite)

## Next steps

* Learn more about [Azure Front Door Rule set](front-door-rules-engine-actions.md).

* Learn more about [Rule set match conditions](rules-match-conditions.md).

* Learn more about [Rule set actions](front-door-rules-engine-actions.md).


# Front Door Url Rewrite

# URL rewrite

Azure Front Door provides support for URL rewrite, enabling you to modify the request path that is being routed to your origin. This powerful feature allows you to define conditions that determine when the URL or specified headers should be rewritten. These conditions are based on the information present in the request and response.

By using URL rewrite, you have the ability to redirect your end users to different origins based on factors such as their device type or the type of file they're requesting. The URL rewrite action can be easily configured within the rule set, providing you with fine-grained control over your routing behavior.

## Source pattern

The **source pattern** represents the URL path in the initial request that you wish to replace. Currently, the source pattern utilizes a prefix-based matching approach. To match all URL paths, you can specify a forward slash (`/`) as the value for the source pattern.

In the context of a URL rewrite action, only the path after the *patterns to match* in the route configuration is taken into consideration for the source pattern. For instance, the rule set considers only `/source-pattern` as the source pattern to be rewritten if you have an incoming URL format of `contoso.com/pattern-to-match/source-pattern`. After the URL rewrite is applied, the outgoing URL format will be `contoso.com/pattern-to-match/destination`.

In cases where you need to remove the `/pattern-to-match` segment of the URL, you can set the **origin path** for the origin group in the route configuration to `/`.

## Destination

The destination path represents the path that replaces the source pattern. For instance, if the request URL path is `contoso.com/foo/1.jpg`, and the source pattern is `/foo/`, specifying the destination as `/bar/` results in the content being served from `contoso.com/bar/1.jpg` from the origin.

## Preserve unmatched path

Preserve unmatched path allows you to control how the remaining path after the source pattern is handled. By setting preserve unmatched path to **Yes**, the remaining path is appended to the new path. On the other hand, setting it to **No** (default) will remove the remaining path after the source pattern.

Here's an example showcasing the behavior of preserve unmatched path:

| Preserve unmatched path | Source pattern | Destination | Incoming request | Content served from origin |

|--|--|--|--|--|

| Yes | / | /foo/ | contoso.com/sub/1.jpg | /foo/sub/1.jpg |

| Yes | /sub/ | /foo/ | contoso.com/sub/image/1.jpg | /foo/image/1.jpg |

| No | /sub/ | /foo/2.jpg | contoso.com/sub/image/1.jpg | /foo/2.jpg |

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

Azure Front Door (classic) provides support for URL rewrite by configuring a **Custom forwarding path** when setting up the forward routing type rule. By default, if only a forward slash (`/*`) is defined, Front Door replicates the incoming URL path in the forwarded request. The host header used in the forwarded request is based on the configuration of the selected backend. For more detailed information, see the [Backend host header](origin.md#origin-host-header) documentation.

The key aspect of URL rewrite lies in the ability to copy any matching part of the incoming path to the forwarded path when using a custom forwarding path with a wildcard match. The following table illustrates an example of an incoming request and the corresponding forwarded path when utilizing a custom forwarding path of `/fwd/`. The section denoted as **a/b/c** represents the portion that replaces the wildcard match.

| Incoming URL path | Match path | Custom forwarding path | Forwarded path |

|--|--|--|--|

| /foo/a/b/c | /foo/* | /fwd/ |  /fwd/a/b/c |

## URL rewrite example

Consider a routing rule with the following combination of frontend hosts and paths are configured:

| Hosts | Paths |

|--|--|

| www\.contoso.com | /\* |

|  | /foo |

|  | /foo/\* |

|  | /foo/bar/\* |

The following table illustrates examples of incoming requests and their corresponding most-specific matching routes. It also provides examples of custom forwarding paths and the resulting forwarded paths.

For instance, consider the second row of the table. If the incoming request is `www.contoso.com/sub`, and the custom forwarding path is set to `/`, then the forwarded path would be `/sub`. However, if the custom forwarding path is set to `/fwd/`, then the forwarded path would be `/fwd/sub`. The emphasized parts of the paths indicate the portions that are part of the wildcard match.

| Incoming request | Most-specific match path | / | /fwd/ | /foo/ | /foo/bar/ |

|--|--|--|--|--|--|

| www\.contoso.com/ | /\* | / | /fwd/ | /foo/ | /foo/bar/ |

| www\.contoso.com/**sub** | /\* | /**sub** | /fwd/**sub** | /foo/**sub** | /foo/bar/**sub** |

| www\.contoso.com/**a/b/c** | /\* | /**a/b/c** | /fwd/**a/b/c** | /foo/**a/b/c** | /foo/bar/**a/b/c** |

| www\.contoso.com/foo | /foo | / | /fwd/ | /foo/ | /foo/bar/ |

| www\.contoso.com/foo/ | /foo/\* | / | /fwd/ | /foo/ | /foo/bar/ |

| www\.contoso.com/foo/**bar** | /foo/\* | /**bar** | /fwd/**bar** | /foo/**bar** | /foo/bar/**bar** |

> [!NOTE]

> Azure Front Door (classic) only supports URL rewrite from a static path to another static path. Preserve unmatched path is supported with Azure Front Door Standard and Premium. For more information, see [Preserve unmatched path](front-door-url-rewrite.md#preserve-unmatched-path).

>

## Optional settings

**Cache configuration** - If disabled or not specified, requests that match to this routing rule doesn't attempt to use cached content and instead always fetch from the backend. For more information, see [caching with Azure Front Door](front-door-caching.md).

## Next steps

- Learn how to [create an Azure Front Door profile](create-front-door-portal.md).

- Learn more about [Azure Front Door rule set](front-door-rules-engine.md)

- Learn about [Azure Front Door routing architecture](front-door-routing-architecture.md).


# Troubleshoot Cross Origin Resources

# Using Azure Front Door Standard/Premium with Cross-Origin Resource Sharing (CORS)

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

## What is CORS?

CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain to access resources in another domain. To reduce the possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](https://www.w3.org/Security/wiki/Same_Origin_Policy). This prevents a web page from calling APIs in a different domain. CORS provides a secure way to allow one origin (the origin domain) to call APIs in another origin.

## How it works

There are two types of CORS requests, *simple requests* and *complex requests.*

### For simple requests:

1. The browser sends the CORS request with another **Origin** HTTP request header. The value of this header is the origin that served the parent page, which is defined as the combination of *protocol,* *domain,* and *port.*  When a page from https\://www.contoso.com attempts to access a user's data in the fabrikam.com origin, the following request header would be sent to fabrikam.com:

`Origin: https://www.contoso.com`

2. The server might respond with any of the following responses:

* An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed. For example:

`Access-Control-Allow-Origin: https://www.contoso.com`

* An HTTP error code such as 403 if the server doesn't allow the cross-origin request after checking the Origin header

* An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:

`Access-Control-Allow-Origin: *`

### For complex requests:

A complex request is a CORS request where the browser is required to send a *preflight request* (that is, a preliminary probe) before sending the actual CORS request. The preflight request asks the server permission if the original CORS request can continue and is an `OPTIONS` request to the same URL.

> [!TIP]

> For more details on CORS flows and common pitfalls, view the [Guide to CORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).

>

>

## Wildcard or single origin scenarios

CORS on Azure Front Door works automatically with no extra configuration when the **Access-Control-Allow-Origin** header is set to wildcard (*) or a single origin. Azure Front Door caches the first response and ensuing requests use the same header.

If requests were sent to the Azure Front Door before CORS being set on your origin, you need to purge content on your endpoint content to reload the content with the **Access-Control-Allow-Origin** header.

## Multiple origin scenarios

If you need to allow a specific list of origins to be allowed for CORS, things get a little more complicated. The problem occurs when the CDN caches the **Access-Control-Allow-Origin** header for the first CORS origin. When a different CORS origin makes another request, the CDN serves the cached **Access-Control-Allow-Origin** header, which doesn't match. There are several ways to correct this problem.

### Azure Front Door Rule Set

On Azure Front Door, you can create a rule in the Azure Front Door [Rules Set](../front-door-rules-engine.md) to check the **Origin** header on the request. If it's a valid origin, your rule sets the **Access-Control-Allow-Origin** header with the correct value. In this case, the **Access-Control-Allow-Origin** header from the file's origin server is ignored and the AFD's rules engine completely manages the allowed CORS origins.

> [!TIP]

> You can add more actions to your rule to modify other response headers, such as **Access-Control-Allow-Methods**.

>

## Next step

Learn how to [create a Front Door](create-front-door-portal.md).


# Origin

# Origins and origin groups in Azure Front Door

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

> [!NOTE]

> *Origin* and *origin group* in this article refers to the backend and backend pool of the Azure Front Door (classic) configuration.

This article describes concepts about how to map your web application deployment with Azure Front Door. You learn about what an *origin* and *origin group* is in the Azure Front Door configuration.

## Origin

An origin refers to the application deployment that Azure Front Door retrieves contents from. Azure Front Door supports origins hosted in Azure and applications hosted in your on-premises datacenter or with another cloud provider. An origin shouldn't be confused with your database tier or storage tier. The origin should be viewed as the endpoint for your application backend. When you add an origin to an origin group in the Front Door configuration, you must also configure the following settings:

* **Origin type:** The type of resource you want to add. Front Door supports autodiscovery of your application backends from App Service, Cloud Service, or Storage. If you want a different resource in Azure or even a non-Azure backend, select **Custom host**.

>[!IMPORTANT]

>During configuration, APIs doesn't validate if the origin isn't accessible from the Front Door environment. Make sure that Front Door can reach your origin.

* **Subscription and origin host name:** If you didn't select **Custom host** for your backend host type, select your backend by choosing the appropriate subscription and the corresponding backend host name.

* **Private Link:** Azure Front Door Premium tier supports sending traffic to an origin by using Private Link. For more information, see [Secure your Origin with Private Link](private-link.md).

* **Certificate subject name validation:** during Azure Front Door to origin TLS connection, Azure Front Door validates if the request host name matches the host name in the certificate provided by the origin. From a security standpoint, Microsoft doesn't recommend disabling certificate subject name check. For more information, see [End-to-end TLS encryption](end-to-end-tls.md), especially if you want to disable this feature.

* **Origin host header:** The host header value sent to the backend for each request. For more information, see [Origin host header](#origin-host-header).

* **Priority**. Assign priorities to your different backends when you want to use a primary service backend for all traffic. Also, provide backups if the primary or the backup backends are unavailable. For more information, see [Priority](routing-methods.md#priority).

* **Weight**. Assign weights to your different backends to distribute traffic across a set of backends, either evenly or according to weight coefficients. For more information, see [Weights](routing-methods.md#weighted).

> [!IMPORTANT]

> When an origin is **disabled**, both routing and health probes to the origin are also disabled.

### Origin host header

Requests that get forwarded by Azure Front Door to an origin include a host header field that the origin uses to retrieve the targeted resource. The value for this field typically comes from the origin URI that has the host header and port.

For example, a request made for `www.contoso.com` has the host header `www.contoso.com`. If you use the Azure portal to configure your origin, the default value for this field is the host name of the origin. If your origin is `contoso-westus.azurewebsites.net`, in the Azure portal, the autopopulated value for the origin host header is `contoso-westus.azurewebsites.net`. However, if you use Azure Resource Manager templates or another method without explicitly setting this field, Front Door sends the incoming host name as the value for the host header. If the request was made for `www.contoso.com`, and your origin `contoso-westus.azurewebsites.net` has an empty header field, Front Door sets the host header as `www.contoso.com`.

Most app backends (Azure Web Apps, Blob storage, and Cloud Services) require the host header to match the domain of the backend. However, the frontend host that routes to your origin uses a different hostname such as `www.contoso.net`.

If your origin requires the host header to match the origin hostname, make sure that the origin host header includes the hostname of the origin.

> [!NOTE]

> If you're using an App Service as an origin, make sure that the App Service also has the custom domain name configured. For more information, see [set up an existing custom domain name for your app](../app-service/app-service-web-tutorial-custom-domain.md).

#### Configure the origin host header for the origin

To configure the **origin host header** field for an origin in the origin group section:

1. Open your Front Door resource and select the origin group with the origin to configure.

1. Add an origin or edit an existing one.

1. Set the origin host header field to a custom value or leave it blank. The hostname for the incoming request gets used as the host header value.

## Origin group

An origin group in Azure Front Door refers to a set of origins that receives similar traffic for their application. You can define the origin group as a logical grouping of your application instances across the world that receives the same traffic and responds with an expected behavior. These origins can be deployed across different regions or within the same region. All origins can be deployed in an Active/Active or Active/Passive configuration.

An origin group defines how origins get evaluated by health probes. It also defines the load balancing method between them.

### Health probes

Azure Front Door sends periodic HTTP/HTTPS probe requests to each of your configured origins. Probe requests determine the proximity and health of each origin to load balance your end-user requests. Health probe settings for an origin group define how we poll the health status of app backends. The following settings are available for load-balancing configuration:

* **Path**: The URL used for probe requests for all the origins in the origin group. For example, if one of your origins is `contoso-westus.azurewebsites.net` and the path gets set to /probe/test.aspx, then Front Door sends health probe requests to `http://contoso-westus.azurewebsites.net/probe/test.aspx` if the protocol is set to HTTP.

* **Protocol**: Defines whether to send the health probe requests from Front Door to your origins with HTTP or HTTPS protocol.

* **Method**: The HTTP method to be used for sending health probes. Options include GET or HEAD (default).

> [!NOTE]

> For lower load and cost on your backends, Front Door recommends using HEAD requests for health probes.

* **Interval (seconds)**: Defines the frequency of health probes to your origins, or the intervals in which each of the Front Door environments sends a probe.

> [!NOTE]

> For faster failovers, set the interval to a lower value. The lower the value, the higher the health probe volume your backends receive. For example, if the interval is set to 30 seconds with 100 Front Door POPs globally, each backend will receive about 200 probe requests per minute.

For more information, see [Health probes](health-probes.md).

### Load-balancing settings

Load-balancing settings for the origin group define how we evaluate health probes. These settings determine if the origin is healthy or unhealthy. They also check how to load-balance traffic between different origins in the origin group. The following settings are available for load-balancing configuration:

* **Sample size:** Identifies how many samples of health probes we need to consider for origin health evaluation.

* **Successful sample size:** Defines the sample size as previously mentioned, the number of successful samples needed to call the origin healthy. For example, assume a Front Door health probe interval is 30 seconds, sample size is 5, and successful sample size is 3. Each time we evaluate the health probes for your origin, we look at the last five samples over 150 seconds (5 x 30). At least three successful probes are required to declare the origin as healthy.

* **Latency sensitivity (extra latency):** Defines if you want Front Door to send the request to the origin within the latency measurement sensitivity range or forward the request to the closest backend.

For more information, see [Least latency based routing method](routing-methods.md#latency).

## Related content

- Learn how to [create an Azure Front Door profile](create-front-door-portal.md).

- Learn about [Azure Front Door routing architecture](front-door-routing-architecture.md?pivots=front-door-standard-premium).

- Learn how to [create an Azure Front Door (classic) profile](quickstart-create-front-door.md).

- Learn about [Azure Front Door (classic) routing architecture](front-door-routing-architecture.md?pivots=front-door-classic).


# Front Door Traffic Acceleration

# Traffic acceleration

Front Door optimizes the traffic path from the end user to the origin server. This article describes how traffic is routed from the user to Front Door and to the origin.

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

Front Door optimizes the traffic path from the end user to the backend server. This article describes how traffic is routed from the user to Front Door and from Front Door to the backend.

## Select the Front Door edge location for the request (Anycast)

Globally, [Front Door has over 150 edge locations](edge-locations-by-region.md), or points of presence (PoPs), located in many countries/regions. Every Front Door PoP can serve traffic for any request.

Traffic routed to the Azure Front Door edge locations uses [Anycast](https://en.wikipedia.org/wiki/Anycast) for both DNS (Domain Name System) and HTTP (Hypertext Transfer Protocol) traffic. Anycast allows for user requests to reach the closest edge location in the fewest network hops. This architecture offers better round-trip times for end users by maximizing the benefits of [Split TCP](#connect-to-the-front-door-edge-location-split-tcp).

Front Door organizes its edge locations into primary and fallback *rings*. The outer ring has edge locations that are closer to users, offering lower latencies.  The inner ring has edge locations that can handle the failover for the outer ring edge location in case any issues happen.

The outer ring is the preferred target for all traffic, and the inner ring is designed to handle traffic overflow from the outer ring. Each frontend host or domain served by Front Door gets assigned primary and fallback VIPs (Virtual Internet Protocol addresses), which gets announced by edge locations in both the inner and outer ring.

Front Door's architecture ensures that requests from your end users always reach the closest Front Door edge locations. If the preferred Front Door edge location is unhealthy, all traffic automatically moves to the next closest edge location.

## Select the Front Door edge location for the request (Unicast)

Azure Front Door has edge locations or points of presence (PoPs) worldwide. Every Front Door PoP can serve traffic for any request.

Traffic routed to the Azure Front Door edge locations uses Unicast for both DNS (Domain Name System) and HTTP (Hypertext Transfer Protocol) traffic. Unicast routing in combination with Azure Front Door's Traffic Manager based load management architecture, allows the request to reach the optimal PoP location directly using the unicast IP. This architecture offers better round-trip times for end users by maximizing the benefits of Split TCP.

Front Door organizes its edge locations into primary and fallback rings. The outer ring has edge locations that are closer to users, offering lower latencies. The inner ring has edge locations that can handle the failover for the outer ring edge location in case any issues happen.

The outer ring is the preferred target for all traffic, and the inner ring is designed to handle traffic overflow from the outer ring. Each frontend host or domain served by Front Door gets assigned primary and fallback VIPs (Virtual Internet Protocol addresses), which gets announced by edge locations in both the inner and outer ring.

Front Door's architecture ensures that requests from your end users always reach the optimal Front Door edge locations. If the preferred Front Door edge location is unhealthy, all traffic automatically moves to the next optimal edge location.

## Connect to the Front Door edge location (Split TCP)

[Split TCP](https://en.wikipedia.org/wiki/Performance-enhancing_proxy) is a technique to reduce latencies and TCP problems by breaking a connection that would incur a high round-trip time into smaller pieces.

Split TCP enables the client's TCP connection to terminate inside a Front Door edge location close to the user. A separate TCP connection is established to the origin, and this separate connection might have a large round-trip time (RTT).

The following diagram illustrates how three users, in different geographical locations, connect to a Front Door edge location close to their location. Front Door then maintains the longer-lived connection to the origin in Europe:

Establishing a TCP connection requires 3-5 roundtrips from the client to the server. Front Door's architecture improves the performance of establishing the connection. The "short connection" between the end user and the Front Door edge location means the connection gets established over 3-5 short roundtrips instead of 3-5 long round trips, which results in saving latency. The "long connection" between the Front Door edge location and the origin can be pre-established and then reused across other end users requests save connectivity time. The effect of Split TCP is multiplied when establishing a SSL/TLS (Transport Layer Security) connection, because there are more round trips to secure a connection.

## Connect to the Front Door edge location (Split TCP)

[Split TCP](https://en.wikipedia.org/wiki/Performance-enhancing_proxy) is a technique to reduce latencies and TCP problems by breaking a connection that would incur a high round-trip time into smaller pieces.

Split TCP enables the client's TCP connection to terminate inside a Front Door edge location close to the user. A separate TCP connection is established to the backend, and this separate connection might have a large round-trip time (RTT).

The following diagram illustrates how three users, in different geographical locations, connect to a Front Door edge location close to their location. Front Door then maintains the longer-lived connection to the backend in Europe:

Establishing a TCP connection requires 3-5 roundtrips from the client to the server. Front Door's architecture improves the performance of establishing the connection. The "short connection" between the end user and the Front Door edge location means the connection gets established over 3-5 short roundtrips instead of 3-5 long round trips, which results in saving latency. The "long connection" between the Front Door edge location and the backend can be pre-established and then reused across other end users requests save connectivity time. The effect of Split TCP is multiplied when establishing a SSL/TLS (Transport Layer Security) connection, because there are more round trips to secure a connection.

## Next step

> [!div class="nextstepaction"]

> [Front Door routing architecture](front-door-routing-architecture.md)


# How To Configure Origin

# How to configure an origin for Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

This article shows you how to create an Azure Front Door origin in a new origin group. The origin group can be then associated with a route to determine how traffic reaches your origins.

> [!NOTE]

> An *Origin* and an *origin group* in this article refers to the backend and backend pool of the Azure Front Door (classic) configuration.

>

## Prerequisites

Before you can create an Azure Front Door origin, you must have an Azure Front Door Standard or Premium tier profile. For more information, see [create a Azure Front Door](create-front-door-portal.md).

## Create a new origin group

1. Sign in to the [Azure portal](https://portal.azure.com) and navigate to your Azure Front Door profile.

1. Select **Origin groups** from under *Settings** in the left hand side menu pane and then select **+ Add** to create a new origin group.

1. On the **Add an origin group** page, enter a unique **Name** for the new origin group. Then select **+ Add an origin** to add a new origin.

## Add an origin

1. On the **Add an origin** page, enter, or select the values based on your requirements:

| Field                          | Description                                                                                                                                                                                                                       |

|-------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

| **Name**                       | Enter a unique name for the new origin.                                                                                                                                                                                           |

| **Origin type**                | The type of resource you want to add. Front Door supports autodiscovery of your Azure origin such as Azure App services, Azure Cloud service, and Azure Storage. If you want a non-Azure backend, you can select **Custom**.       |

| **Host name**                  | Select your backend origin host name in the dropdown. If you selected **Custom** as origin host type, then enter the host name of your backend origin.                                                                             |

| **Origin host header**         | Enter the host header value being sent to the backend for each request. For more information, see [origin host header](origin.md#origin-host-header).                                                                              |

| **Certificate subject name validation** | During the Azure Front Door and origin TLS connection, Azure Front Door validates if the request host name matches the host name in the certificate provided by the origin. For more information, see [End-to-end TLS](end-to-end-tls.md). |

| **HTTP Port**                  | Default value is 80. Enter the value for the port that the origin supports for HTTP protocol.                                                                                                                                      |

| **HTTPS Port**                 | Default value is 443. Enter the value for the port that the origin supports for HTTPS protocol.                                                                                                                                    |

| **Priority**                   | You can determine if this origin has higher priority than other origins in the origin group. With this value you can set primary, secondary, and backup origins. Default value is 1 for all origins. For more information, see [Priority](routing-methods.md#priority). |

| **Weight**                     | Default value is 1000. Assign weights to your origins to determine how traffic gets distributed. For example, if you have two origins with weights 1000 and 2000, then the second origin receives twice as much traffic as the first origin. For more information, see [Weights](routing-methods.md#weighted). |

| **Private link**               | You can enable the private link service to secure connectivity to your origin. Supported origin types are Azure blob storages, Azure static websites, App services, and internal load balancers.                                   |

| **Status**                     | Select this option to enable the origin.                                                                                                                                                                                           |

> [!IMPORTANT]

> * During configuration, the Azure portal doesn't validate if the origin is accessible from Azure Front Door environments. You need to verify that Azure Front Door can reach your origin.

> * When an origin is **disabled**, both routing and health probes to the origin are also disabled.

1. Select **Add** once you have completed the origin settings. The origin should now appear in the origin group.

1. Configure the rest of the origin group settings. You can update *Health probes* and *Load balancing* settings to meet your requirements.

> [!NOTE]

> * You can configure session affinity to ensure requests from the same end user gets directed to the same origin. For more information, see [session affinity](routing-methods.md#affinity).

> * The health probe path is **case sensitive**.

>

1. Select **Add** to save the origin group configuration. The new origin group should appear on the origin group page.

## Origin response timeout

1. Origin response timeout can be found on the **Overview** page of your Azure Front Door profile.

> [!IMPORTANT]

> This timeout value is applied to all endpoints in the Azure Front Door profile.

>

1. The value of the response timeout must be between 16 and 240 seconds.

## Clean up resources

To delete an origin group when you no longer needed it, select the **...** and then select **Delete** from the drop-down.

To remove an origin when you no longer need it, select the **...** and then select **Delete** from the drop-down.

## Next steps

To learn about custom domains, see [adding a custom domain](standard-premium/how-to-add-custom-domain.md) to your Azure Front Door endpoint.


# Origin Authentication With Managed Identities

# Use managed identities to authenticate to origins (preview)

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Managed identities provided by Microsoft Entra ID enables your Azure Front Door Standard/Premium instance to securely access other Microsoft Entra protected resources, such as Azure Blob Storage, without the need to manage credentials. For more information, see [What is  managed identities for Azure resources?](/entra/identity/managed-identities-azure-resources/overview)

After you enable managed identity for Azure Front Door and granting the managed identity necessary permissions to your origin, Front Door will use the managed identity to obtain an access token from Microsoft Entra ID for accessing the specified resource. After successfully obtaining the token, Front Door will set the value of the token in the Authorization header using the Bearer scheme and then forward the request to the origin. Front Door caches the token until it expires.

> [!Note]

> This feature is currently not supported for origins with Private Link enabled in Front Door.

Azure Front Door supports two types of managed identities:

* **System-assigned identity**: This identity is tied to your service and is deleted if the service is deleted. Each service can have only one system-assigned identity.

* **User-assigned identity**: This is a standalone Azure resource that can be assigned to your service. Each service can have multiple user-assigned identities.

Managed identities are specific to the Microsoft Entra tenant where your Azure subscription is hosted. If a subscription is moved to a different directory, you need to recreate and reconfigure the identity.

## Prerequisites

* An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

* An Azure Front Door Standard or Premium profile. To create a new profile, see [create an Azure Front Door](create-front-door-portal.md).

## Enable managed identity

1. Navigate to your existing Azure Front Door profile. Select **Identity** under *Security* in the left menu.

1. Choose either a **System assigned** or **User assigned** managed identity.

* **[System assigned](#system-assigned)** - A managed identity tied to the Azure Front Door profile lifecycle.

* **[User assigned](#user-assigned)** - A standalone managed identity resource with its own lifecycle.

### System assigned

1. Toggle the *Status* to **On** and select **Save**.

1. Confirm the creation of a system managed identity for your Front Door profile by selecting **Yes** when prompted.

### User assigned

To use a user-assigned managed identity, you must have one already created. For instructions on creating a new identity, see [create a user-assigned managed identity](../active-directory/managed-identities-azure-resources/how-manage-user-assigned-managed-identities.md).

1. In the **User assigned** tab, select **+ Add** to add a user-assigned managed identity.

1. Search for and select the user-assigned managed identity. Then select **Add** to attach it to the Azure Front Door profile.

1. The name of the selected user-assigned managed identity appears in the Azure Front Door profile.

## Associating the identity to an origin group

> [!Note]

> The association will only work if

> * the origin group does not contain any origins with private link enabled.

> * the health probe protocol is set to 'HTTPS' under origin group settings.

> * the forwarding protocol is set to 'HTTPS Only' under route settings.

> * the forwarding protocol is set to 'HTTPS Only' in case you are using a 'Route configuration override' action in rulesets.

> [!Warning]

> From here onwards, if you are using origin authentication between Front Door and Storage, the sequence of steps for enabling origin authentication are very important and cause issues if the appropriate sequence is not followed.

> * If you are using a storage account with public anonymous access enabled, follow the below steps in the exact sequence - 'Associating the identity to an origin group' followed by 'Providing access at the origin resource'. Once all steps are complete, you can disable public anonymous access to only allow access to your storage account from Front Door.

> * If you are using a storage account with public anonymous access disabled, you have to follow a different sequence. First do the steps for 'Providing access at the origin resource' followed by 'Associating the identity to an origin group'. Start sending traffic via Front Door to the storage account only after completing all the steps in the aforementioned sequence.

1.	Navigate to your existing Azure Front Door profile and open origin groups.

2.	Select an existing origin group which has origins already configured.

3.	Scroll down to the **Authentication** section.

4.	Enable **Origin authentication**.

5.	Choose between system assigned or user assigned managed identity.

6.	Enter the correct [scope](/entra/identity-platform/scopes-oidc) within the **Scope** field.

7.	Click on **Update**.

## Providing access at the origin resource

1.	Navigate to the management page of your origin resource. For example, if the origin is an Azure Blob Storage, go to that Storage Account management page.

> [!Note]

> The next steps assume your origin is an Azure Blob Storage. If you're using a different resource type, make sure to select the appropriate **job function role** during role assignment. Otherwise, the steps remain the same for most resource types.

2. Go to the **Access Control (IAM)** section and click on **Add**. Choose **Add role assignment** from the dropdown menu.

3.	Under **Job function roles** in the **Roles** tab, select an appropriate role (for example, Storage Blob Data Reader) from the list and then select **Next**.

> [!IMPORTANT]

> When granting any identity, including a managed identity, permissions to access services, always grant the least permissions needed to perform the desired actions. For example, if a managed identity is used to read data from a storage account, there's no need to allow that identity permissions to also write data to the storage account. Granting extra permissions, for example, making the managed identity a contributor of a storage account when it’s not needed, can make requests coming via AFD capable of write and delete operations.

5.	In the **Members** tab, under the **Assign access to**, choose **Managed identity** and then click on **Select members**.

6. The **Select managed identities** window opens. Choose the subscription where your Front Door is located and under **Managed identity** dropdown, choose **Front Door and CDN profiles**. Under the **Select** dropdown, choose the managed identity created for your Front Door. Click on the **Select** button in the bottom.

7.	Select **Review and assign** and then select **Review and assign** once more after the validation is complete.

## Tips while using origin authentication

* If you are facing errors during origin group configuration,

* Ensure that the health probe protocol is set to HTTPS.

* Ensure that forwarding protocol within route settings and/or route configuration override settings (in rulesets) is set to 'HTTPS Only'.

* Ensure that there are no private link enabled origins within the origin group.

* If you see 'Access Denied; responses from origin, verify that the Managed Identity has the appropriate role assigned to access the origin resource.

* Transition from SAS Tokens for Storage: If transitioning from SAS tokens to Managed Identities, follow a step-wise approach to avoid downtime. Enable Managed Identity, associate it with the origin, and then stop using SAS tokens.

* After you enable origin authentication in origin group settings, you should not directly disable/delete the identities from the Identity settings under Front Door portal, nor directly delete the user-assigned managed identity under the Managed Identity portal. Doing so will cause origin authentication to fail immediately. Instead, if you want to stop using the origin authentication feature or want to delete/disable the identities, first disable the access restrictions under the Access Control (IAM) section of the origin resource so that the origin is accessible without the need of a managed identity or Entra ID token. Then disable origin authentication under Front Door origin group settings. Wait for some time for the configuration to be updated and then delete/disable the identity if required.

* If your clients are already sending their own tokens under the Authorization header, the token value will be overwritten by AFD with the origin authentication token. If you want AFD to send the client token to the origin, you can configure an AFD rule using the server variable {http_req_header_Authorization} to send the token under a separate header.

* It is recommended that you use different managed identities for origin authentication and for AFD to Azure Key Vault authentication.

* For best practices while using managed identities, refer to [Managed identity best practice recommendations](/entra/identity/managed-identities-azure-resources/managed-identity-best-practice-recommendations).

* For best practices while assigning RBAC role for Azure storage account, refer to [Assign an Azure role for access to blob data](../storage/blobs/assign-azure-role-data-access.md)

* When origin authentication is enabled on an origin group, Front Door includes the access token in the Authorization header for health probes probing the origins within the origin group, not just for end-user traffic requests.


# How To Enable Private Link Internal Load Balancer

# Connect Azure Front Door Premium to an internal load balancer origin with Private Link

**Applies to:** :heavy_check_mark: Front Door Premium

This article guides you through how to configure Azure Front Door Premium to connect to your internal load balancer origin using the Azure Private Link service.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An Azure Front Door Premium profile. For more information, see [Create an Azure Front Door](../create-front-door-portal.md).

- A Private Link for your origin web servers. For more information, see [Create a Private Link service](../../private-link/create-private-link-service-portal.md).

- Review the [Secure your origin with Private Link](../private-link.md) article to better understand how Private Link works with Azure Front Door.

## Enable private connectivity to an internal load balancer

In this section, you map the Private Link service to a private endpoint created in Azure Front Door.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Navigate to your Azure Front Door Premium profile, then select **Origin groups** from under *Settings* in the left side menu pane.

1. Select an existing origin group or create a new one to add to an internal load balancer origin.

1. Select **+ Add an origin** to add new origin. Select or enter the following settings to configure the internal load balancer origin.

> [!NOTE]

> The hostname must be a valid domain name, IPv4, or IPv6. The hostname can be the private IP of the internal load balancer or a domain name.

* **Name** - Enter a name to identify this origin.

* **Origin type** - Select the **Custom** origin type.

* **Host name** - The host name is used for SNI (SSL negotiation) and should match your server side certificate. |

* **Origin host header** - The origin host header can be the private link private IP for the internal load balancer or a valid domain name. When a private link service is enabled, this field is used only for the HTTP request header.

* **Certificate subject name validation** - Select the checkbox to enable certificate subject name validation. This validation checks the certificate subject name against the host name. If the certificate subject name doesn't match the host name, the connection is rejected. **This validation is required if private link is enabled.**

* **HTTP port** - 80 (default)

* **HTTPS port** 443 (default)

* **Priority** - You can determine if this origin has higher priority than other origins in the origin group. With this value you can set primary, secondary, and backup origins. Default value is **1** for all origins.

* **Weight** - 1000 (default). Assign weights to your origins to determine how traffic gets distributed. For example, if you have two origins with weights 1000 and 2000, then the second origin receives twice as much traffic as the first origin.

* **Private link** - Select the checkbox to enable private link for this origin.

* **Select a private link**:

* **In my directory** - Select this option if you want to use your own private link service.

* **By ID or alias** - Select this option if you want to use a private link service that is shared with you. You need to enter the resource ID of the private link service.

* **Region** - Select the region that is the same or closest to your origin.

* **Request message** - This message is sent to the resource owner to assist them in the connection management process.

* **Status** - Leave checked to enable the origin.

1. Select **Add** to add the internal load balancer origin and then select **Update** to save the origin group settings.

## Approve private endpoint connection

1. Go to the Private Link Center and select **Private link services**. Then select the private link service you created for the internal load balancer.

1. Select **Private endpoint connections** from under *Settings* in the left side menu pane.

1. Select the *pending* private endpoint request from Azure Front Door then select **Approve**. When prompted, select **Yes** to confirm you want to establish this connection.

1. The *connection state* should change to **Approved**. It might take a couple of minutes for the connection to fully establish. You can now access your internal load balancer from Azure Front Door.

## Common mistakes to avoid

The following are common mistakes when configuring an origin with Azure Private Link enabled:

* Adding the origin with Azure Private Link enabled to an existing origin group that contains public origins. Azure Front Door doesn't allow mixing public and private origins in the same origin group.

* Private Link changes how the **Host name** and the **Origin host header** fields operate. It doesn't change the NAT behavior of the flow to the private link service origin.

## Related content

- [Secure your origin with Private Link](../private-link.md)

- [Private Link service](../../private-link/private-link-service-overview.md)


# How To Enable Private Link Storage Account

# Connect Azure Front Door Premium to a storage account origin with Private Link

**Applies to:** :heavy_check_mark: Front Door Premium

This article guides you through configuring Azure Front Door Premium to connect privately to a storage account origin using Azure Private Link service.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- A Private Link. For more information, see [Create a Private Link service](../../private-link/create-private-link-service-portal.md).

- Sign in to the [Azure portal](https://portal.azure.com) with your Azure account.

- A Private Link. For more information, see [Create a Private Link service](../../private-link/create-private-link-service-cli.md).

- Azure Cloud Shell or Azure CLI.

The steps in this article run the Azure CLI commands interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the commands in the Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code, and paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure CLI locally](/cli/azure/install-azure-cli) to run the commands. If you run Azure CLI locally, sign in to Azure using the [az login](/cli/azure/reference-index#az-login) command.

> [!NOTE]

> Private endpoints require your Storage Account to meet specific requirements. For more information, see [Using Private Endpoints for Azure Storage](../../storage/common/storage-private-endpoints.md).

## Enable Private Link to a storage account in Azure Front Door

In this section, you map the Private Link service to a private endpoint created in Azure Front Door's private network.

1. Within your Azure Front Door Premium profile, under **Settings**, select **Origin groups**.

1. Select the origin group that contains the storage account origin you want to enable Private Link for.

1. Select **+ Add an origin** to add a new storage account origin or select a previously created storage account origin from the list.

1. Select or enter the following values to configure the storage blob you want Azure Front Door Premium to connect with privately.

| Setting | Value |

| ------- | ----- |

| Name | Enter a name to identify this storage blog origin. |

| Origin type | Storage (Azure Blobs) |

| Host name | Select the host from the dropdown that you want as an origin. |

| Origin host header | You can customize the host header of the origin or leave it as default. |

| HTTP port | 80 (default) |

| HTTPS port | 443 (default) |

| Priority | Different origin can have different priorities to provide primary, secondary, and backup origins. |

| Weight | 1000 (default). Assign weights to your different origin when you want to distribute traffic.|

| Region | Select the region that is the same or closest to your origin. |

| Target sub resource | The type of subresource for the resource selected previously that your private endpoint can access. |

| Request message | Custom message to see while approving the Private Endpoint. |

1. Select **Add** to save your configuration.

1. Select **Update** to save the origin group settings.

> [!NOTE]

> Ensure the **origin path** in your routing rule is configured correctly with the storage container file path so file requests can be acquired.

Use the [az afd origin create](/cli/azure/afd/origin#az-afd-origin-create) command to create a new Azure Front Door origin. The `private-link-location` value must be from the [available regions](../private-link.md#region-availability) and the `private-link-sub-resource-type` value is **blob**.

```azurecli-interactive

az afd origin create --enabled-state Enabled \

--resource-group 'myResourceGroup' \

--origin-group-name 'og1' \

--origin-name 'mystorageorigin' \

--profile-name 'contosoAFD' \

--host-name 'mystorage.blob.core.windows.net' \

--origin-host-header 'mystorage.blob.core.windows.net' \

--http-port 80 \

--https-port 443 \

--priority 1 \

--weight 500 \

--enable-private-link true \

--private-link-location 'EastUS' \

--private-link-request-message 'AFD storage origin Private Link request.' \

--private-link-resource '/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorage' \

--private-link-sub-resource-type blob

```

## Approve Front Door private endpoint connection from the storage account

1. Go to the storage account you configured Private Link for in the previous section.

1. Under **Settings**, select **Networking**.

1. In **Networking**, select **Private endpoint connections**.

1. Select the **pending** private endpoint request from Azure Front Door Premium then select **Approve**.

1. Use the [az network private-endpoint-connection list](/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-list) command to list the private endpoint connections for your storage account. Note the `Resource ID` of the private endpoint connection from the output.

```azurecli-interactive

az network private-endpoint-connection list --name 'mystorage' --resource-group 'myResourceGroup' --type 'Microsoft.Storage/storageAccounts'

```

2. Use the [az network private-endpoint-connection approve](/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-approve) command to approve the private endpoint connection.

```azurecli-interactive

az network private-endpoint-connection approve --id '/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorage/privateEndpointConnections/mystorage.aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e'

```

It takes a few minutes for the connection to fully establish after approval. Once established, you can access your storage account privately through Azure Front Door Premium. Public internet access to the storage account is disabled once the private endpoint is enabled.

> [!NOTE]

> If the blob or container within the storage account doesn't permit anonymous access, requests made against the blob/container should be authorized. One option for authorizing a request is by using [shared access signatures](../../storage/common/storage-sas-overview.md).

## Common mistakes to avoid

The following are common mistakes when configuring an origin with Azure Private Link enabled:

- Adding the origin with Azure Private Link enabled to an existing origin group that contains public origins. Azure Front Door doesn't allow mixing public and private origins in the same origin group.

- Not using SAS tokens while connecting to storage account that doesn't allow anonymous access.

## Related content

- [Connect Azure Front Door to an internal load balancer origin with Private Link](how-to-enable-private-link-internal-load-balancer.md)

- [Private Link service with storage account](../../storage/common/storage-private-endpoints.md)


# How To Enable Private Link Storage Static Website

# Connect Azure Front Door Premium to a storage static website with Private Link

**Applies to:** :heavy_check_mark: Front Door Premium

This article shows you how to configure Azure Front Door Premium tier to connect to your storage static website privately using the Azure Private Link service.

## Prerequisites

- An Azure account with an active subscription. You can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An Azure Front Door Premium profile with an origin group. For more information, see [Create an Azure Front Door](create-front-door-portal.md).

- A Private Link. For more information, see [Create a Private Link service](../private-link/create-private-link-service-portal.md).

- Storage static website is enabled on your storage account. Learn how to [enable static website](../storage/blobs/storage-blob-static-website-how-to.md?tabs=azure-portal).

- Sign in to the [Azure portal](https://portal.azure.com) with your Azure account.

- An Azure Front Door Premium profile with an origin group. For more information, see [Create an Azure Front Door](create-front-door-cli.md).

- A Private Link. For more information, see [Create a Private Link service](../private-link/create-private-link-service-cli.md).

- Storage static website is enabled on your storage account. Learn how to [enable static website](../storage/blobs/storage-blob-static-website-how-to.md?tabs=azure-cli).

- Azure Cloud Shell or Azure CLI.

The steps in this article run the Azure CLI commands interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the commands in the Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code, and paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure CLI locally](/cli/azure/install-azure-cli) to run the commands. If you run Azure CLI locally, sign in to Azure using the [az login](/cli/azure/reference-index#az-login) command.

## Enable Private Link to a storage static website

In this section, you map the Private Link service to a private endpoint created in Azure Front Door's private network.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Within your Azure Front Door Premium profile, under *Settings*, select **Origin groups**.

1. Select the origin group that contains the storage static website origin you want to enable Private Link for.

1. Select **+ Add an origin** to add a new storage static website origin or select a previously created storage static website origin from the list.

1. The following table has the information of what values to select in the respective fields while enabling private link with Azure Front Door. Select or enter the following settings to configure the storage static website you want Azure Front Door Premium to connect with privately.

| Setting | Value |

| ------- | ----- |

| Name | Enter a name to identify this storage static website origin. |

| Origin Type | Storage (Static website) |

| Host name | Select the host from the dropdown that you want as an origin. |

| Origin host header | You can customize the host header of the origin or leave it as default. |

| HTTP port | 80 (default) |

| HTTPS port | 443 (default) |

| Priority | Different origin can have different priorities to provide primary, secondary, and backup origins. |

| Weight | 1000 (default). Assign weights to your different origin when you want to distribute traffic.|

| Region | Select the region that is the same or closest to your origin. |

| Target sub resource | The type of subresource for the resource selected previously that your private endpoint can access. You can select *web* or *web_secondary*. |

| Request message | Custom message to see while approving the Private Endpoint. |

1. Then select **Add** to save your configuration. Then select **Update** to save your changes.

## Approve private endpoint connection from storage account

1. Go to the storage account that you want to connect to Azure Front Door Premium privately. Select **Networking** under *Settings*.

1. In **Networking**, select **Private endpoint connections**.

1. Select the pending private endpoint request from Azure Front Door Premium then select **Approve**.

1. Once approved, you can see the private endpoint connection status is **Approved**.

## Create private endpoint connection to web_secondary

When creating a private endpoint connection to the storage static website's secondary sub resource, you need to add a **-secondary** suffix to the origin host header. For example, if your origin host header is *contoso.z13.web.core.windows.net*, you need to change it to *contoso-secondary.z13.web.core.windows.net*.

Once the origin is added and the private endpoint connection is approved, you can test your private link connection to your storage static website.

## Enable Private Link to a Storage Static Website in Azure Front Door Premium

1. Run [az afd origin create](/cli/azure/afd/origin#az-afd-origin-create) to create a new Azure Front Door origin. Enter the following settings to configure the Storage Static Website you want Azure Front Door Premium to connect with privately. Notice the `private-link-location` must be in one of the [available regions](private-link.md#region-availability) and the `private-link-sub-resource-type` must be **web**.

```azurecli-interactive

az afd origin create --enabled-state Enabled \

--resource-group testRG \

--origin-group-name default-origin-group \

--origin-name pvtStaticSite \

--profile-name testAFD \

--host-name example.z13.web.core.windows.net\

--origin-host-header example.z13.web.core.windows.net\

--http-port 80 \

--https-port 443 \

--priority 1 \

--weight 500 \

--enable-private-link true \

--private-link-location EastUS \

--private-link-request-message 'AFD Storage static website origin Private Link request.' \

--private-link-resource /subscriptions/00000000-0000-0000-0000-00000000000/resourceGroups/testRG/providers/Microsoft.Storage/storageAccounts/testingafdpl \

--private-link-sub-resource-type web

```

## Approve Private Endpoint Connection from Storage Account

1. Run [az network private-endpoint-connection list](/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-list) to list the private endpoint connections for your storage account. Note down the 'Resource ID' of the private endpoint connection available in your storage account, in the first line of your output.

```azurecli-interactive

az network private-endpoint-connection list -g testRG -n testingafdpl --type Microsoft.Storage/storageAccounts

```

2. Run [az network private-endpoint-connection approve](/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-approve) to approve the private endpoint connection.

```azurecli-interactive

az network private-endpoint-connection approve --id /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testRG/providers/Microsoft.Storage/storageAccounts/testingafdpl/privateEndpointConnections/testingafdpl.00000000-0000-0000-0000-000000000000

```

## Create Private Endpoint Connection to Web_Secondary

When creating a private endpoint connection to the storage static website's secondary sub-resource, you need to add a **-secondary** suffix to the origin host header. For example, if your origin host header is `example.z13.web.core.windows.net`, you need to change it to `example-secondary.z13.web.core.windows.net`.

Once the origin is added and the private endpoint connection is approved, you can test your private link connection to your storage static website.

## Common mistakes to avoid

The following are common mistakes when configuring an origin with Azure Private Link enabled:

- Adding the origin with Azure Private Link enabled to an existing origin group that contains public origins. Azure Front Door doesn't allow mixing public and private origins in the same origin group.

## Next step

> [!div class="nextstepaction"]

> [Private Link service with storage account](../storage/common/storage-private-endpoints.md)


# How To Enable Private Link Application Gateway

# Connect Azure Front Door Premium to an Azure Application Gateway with Private Link

**Applies to:** :heavy_check_mark: Front Door Premium

This article guides you through the steps to configure an Azure Front Door Premium to connect privately to your Azure Application Gateway using Azure Private Link.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An Azure Front Door Premium profile and an endpoint. For more information, see [Create an Azure Front Door](create-front-door-portal.md).

- An Azure Application Gateway. For more information on how to create an Application Gateway, see [Direct web traffic with Azure Application Gateway using Azure portal](../application-gateway/quick-create-portal.md).

- Sign in to the [Azure portal](https://portal.azure.com) with your Azure account.

- An Azure Front Door Premium profile and an endpoint. For more information, see [Create an Azure Front Door](create-front-door-powershell.md).

- An Azure Application Gateway. For more information on how to create an Application Gateway, see [Direct web traffic with Azure Application Gateway using Azure PowerShell](../application-gateway/quick-create-powershell.md).

- Azure Cloud Shell or Azure PowerShell.

The steps in this article run the Azure PowerShell cmdlets interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the cmdlets in the Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code and then paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure PowerShell locally](/powershell/azure/install-azure-powershell) to run the cmdlets. If you run PowerShell locally, sign in to Azure using the [Connect-AzAccount](/powershell/module/az.accounts/connect-azaccount) cmdlet.

- An Azure Front Door Premium profile with an origin group. For more information, see [Create an Azure Front Door](create-front-door-cli.md).

- An Azure Application Gateway. For more information on how to create an Application Gateway, see [Direct web traffic with Azure Application Gateway using Azure CLI](../application-gateway/quick-create-cli.md).

- Azure Cloud Shell or Azure CLI.

The steps in this article run the Azure CLI commands interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the commands in the Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code, and paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure CLI locally](/cli/azure/install-azure-cli) to run the commands. If you run Azure CLI locally, sign in to Azure using the [az login](/cli/azure/reference-index#az-login) command.

> [!NOTE]

> While configuring via Azure portal, the region you choose in Azure Front Door origin configuration must be the same region where the Application Gateway is located. If you want the Azure Front Door origin region and the Application Gateway region to be different, use CLI or PowerShell. You might need to you different regions in cases where the Application Gateway is located in a region where Azure Front Door doesn't support Private Link.

## Enable private connectivity to Azure Application Gateway

1. Follow the instructions in [Configure Azure Application Gateway Private Link](../application-gateway/private-link-configure.md), but don't complete the final step of creating a private endpoint.

1. Go to your Application Gateway's **Overview** tab, and note the resource group name, Application Gateway name, and subscription ID.

1. Under **Settings**, select **Private Link**. Note the name of the private link service that appears under the **Name** column in **Private link configurations**.

1. Construct the resource ID of the private link service using the values from previous steps. The format is `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/privateLinkServices/_e41f87a2_{applicationGatewayName}_{privateLinkResource.Name}`. Use this resource ID when configuring the Front Door origin.

## Create an origin group and add the application gateway as an origin

1. In your Azure Front Door Premium profile, go to *Settings* and select **Origin groups**.

1. Select **Add**.

1. Enter a name for the origin group.

1. Select **+ Add an origin**.

1. Use the following table to configure the settings for the origin:

| Setting | Value |

| ------- | ----- |

| Name | Enter a name to identify this origin. |

| Origin Type | Custom |

| Host name | Enter the hostname of the listener of your Application Gateway |

| Origin host header | Enter the hostname of the listener of your Application Gateway |

| HTTP port | 80 (default) |

| HTTPS port | 443 (default) |

| Priority | Assign different priorities to origins for primary, secondary, and backup purposes. |

| Weight | 1000 (default). Use weights to distribute traffic among different origins. |

| Private link | Enable private link service |

| Select a private link | By ID or alias |

| ID/alias | Enter the private link service resource ID obtained while configuring the Application Gateway. |

| Region | Select the region where Application Gateway is located. |

| Request message | Enter a custom message to display while approving the Private Endpoint.  |

1. Select **Add** to save your origin settings.

1. Select **Add** to save the origin group settings.

## Approve the private endpoint

1. Go to the Application Gateway that you configured with Private Link in the previous section. Under **Settings**, select **Private link**.

1. Select the **Private endpoint connections** tab.

1. Find the *pending* private endpoint request from Azure Front Door Premium and select **Approve**.

1. After approval, the connection status updates. It can take a few minutes for the connection to fully establish. Once established, you can access your Application Gateway through Front Door. Direct access to the Application Gateway from the public internet is disabled once private endpoint is enabled.

## Enable private connectivity to Azure Application Gateway

Follow the instructions in [Configure Azure Application Gateway Private Link](../application-gateway/private-link-configure.md), but don't complete the final step of creating a private endpoint.

## Create an origin group and add the application gateway as an origin

1. Use [New-AzFrontDoorCdnOriginGroupHealthProbeSettingObject](/powershell/module/az.cdn/new-azfrontdoorcdnorigingrouphealthprobesettingobject) to create an in-memory object for storing the health probe settings.

```azurepowershell-interactive

$healthProbeSetting = New-AzFrontDoorCdnOriginGroupHealthProbeSettingObject `

-ProbeIntervalInSecond 60 `

-ProbePath "/" `

-ProbeRequestType GET `

-ProbeProtocol Http

```

1. Use [New-AzFrontDoorCdnOriginGroupLoadBalancingSettingObject](/powershell/module/az.cdn/new-azfrontdoorcdnorigingrouploadbalancingsettingobject) to create an in-memory object for storing load balancing settings.

```azurepowershell-interactive

$loadBalancingSetting = New-AzFrontDoorCdnOriginGroupLoadBalancingSettingObject `

-AdditionalLatencyInMillisecond 50 `

-SampleSize 4 `

-SuccessfulSamplesRequired 3

```

1. Run [New-AzFrontDoorCdnOriginGroup](/powershell/module/az.cdn/new-azfrontdoorcdnorigingroup) to create an origin group that contains your application gateway.

```azurepowershell-interactive

$origingroup = New-AzFrontDoorCdnOriginGroup `

-OriginGroupName myOriginGroup `

-ProfileName myFrontDoorProfile `

-ResourceGroupName myResourceGroup `

-HealthProbeSetting $healthProbeSetting `

-LoadBalancingSetting $loadBalancingSetting

```

1. Get the frontend IP configuration name of the Application Gateway with the [Get-AzApplicationGatewayFrontendIPConfig](/powershell/module/az.network/get-azapplicationgatewayfrontendipconfig) command.

```azurepowershell-interactive

$AppGw = Get-AzApplicationGateway -Name myAppGateway -ResourceGroupName myResourceGroup

$FrontEndIPs= Get-AzApplicationGatewayFrontendIPConfig  -ApplicationGateway $AppGw

$FrontEndIPs.name

```

1. Use the [New-AzFrontDoorCdnOrigin](/powershell/module/az.cdn/new-azfrontdoorcdnorigin) command to add your application gateway to the origin group.

```azurepowershell-interactive

New-AzFrontDoorCdnOrigin `

-OriginGroupName myOriginGroup `

-OriginName myAppGatewayOrigin `

-ProfileName myFrontDoorProfile `

-ResourceGroupName myResourceGroup `

-HostName www.contoso.com `

-HttpPort 80 `

-HttpsPort 443 `

-OriginHostHeader www.contoso.com `

-Priority 1 `

-PrivateLinkId /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Network/applicationGateways/myAppGateway `

-SharedPrivateLinkResourceGroupId $FrontEndIPs.name `

-SharedPrivateLinkResourcePrivateLinkLocation CentralUS `

-SharedPrivateLinkResourceRequestMessage 'Azure Front Door private connectivity request' `

-Weight 1000 `

```

> [!NOTE]

> `SharedPrivateLinkResourceGroupId` is the name of the Azure Application Gateway frontend IP configuration.

## Approve the private endpoint

1. Run [Get-AzPrivateEndpointConnection](/powershell/module/az.network/get-azprivateendpointconnection) to retrieve the connection name of the private endpoint connection that needs approval.

```azurepowershell-interactive

Get-AzPrivateEndpointConnection -ResourceGroupName myResourceGroup -ServiceName myAppGateway -PrivateLinkResourceType Microsoft.Network/applicationgateways

```

1. Run [Approve-AzPrivateEndpointConnection](/powershell/module/az.network/approve-azprivateendpointconnection) to approve the private endpoint connection details. Use the *Name* value from the output in the previous step for approving the connection.

```azurepowershell-interactive

Get-AzPrivateEndpointConnection -Name aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb.bbbbbbbb-1111-2222-3333-cccccccccccc -ResourceGroupName myResourceGroup -ServiceName myAppGateway -PrivateLinkResourceType Microsoft.Network/applicationgateways

```

## Complete Azure Front Door setup

Use the [New-AzFrontDoorCdnRoute](/powershell/module/az.cdn/new-azfrontdoorcdnroute) command to create a route that maps your endpoint to the origin group. This route forwards requests from the endpoint to your origin group.

```azurepowershell-interactive

# Create a route to map the endpoint to the origin group

$Route = New-AzFrontDoorCdnRoute `

-EndpointName myFrontDoorEndpoint `

-Name myRoute `

-ProfileName myFrontDoorProfile `

-ResourceGroupName myResourceGroup `

-ForwardingProtocol MatchRequest `

-HttpsRedirect Enabled `

-LinkToDefaultDomain Enabled `

-OriginGroupId $origingroup.Id `

-SupportedProtocol Http,Https

```

Your Azure Front Door profile is fully functional after you complete this final step.

## Enable private connectivity to Azure Application Gateway

Follow the steps in [Configure Azure Application Gateway Private Link](../application-gateway/private-link-configure.md), skipping the last step of creating a private endpoint.

## Create an origin group and add the application gateway as an origin

1. Run [az afd origin-group create](/cli/azure/afd/origin-group#az-afd-origin-group-create) to create an origin group.

```azurecli-interactive

az afd origin-group create \

--resource-group myResourceGroup \

--origin-group-name myOriginGroup \

--profile-name myFrontDoorProfile \

--probe-request-type GET \

--probe-protocol Http \

--probe-interval-in-seconds 60 \

--probe-path / \

--sample-size 4 \

--successful-samples-required 3 \

--additional-latency-in-milliseconds 50

```

1. Run [az network application-gateway frontend-ip list](/cli/azure/network/application-gateway/frontend-ip#az-network-application-gateway-frontend-ip-list) to get the frontend IP configuration name of the Application Gateway.

```azurecli-interactive

az network application-gateway frontend-ip list --gateway-name myAppGateway --resource-group myResourceGroup

```

1. Run [az afd origin create](/cli/azure/afd/origin#az-afd-origin-create) to add an application gateway as an origin to the origin group.

```azurecli-interactive

az afd origin create \

--enabled-state Enabled \

--resource-group myResourceGroup \

--origin-group-name myOriginGroup \

--origin-name myAppGatewayOrigin \

--profile-name myFrontDoorProfile \

--host-name www.contoso.com \

--origin-host-header www.contoso.com \

--http-port 80  \

--https-port 443 \

--priority 1 \

--weight 500 \

--enable-private-link true \

--private-link-location centralus \

--private-link-request-message 'Azure Front Door private connectivity request.' \

--private-link-resource /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myRGAG/providers/Microsoft.Network/applicationGateways/myAppGateway \

--private-link-sub-resource-type myAppGatewayFrontendIPName

```

> [!NOTE]

> `private-link-sub-resource-type` is the Azure Application Gateway frontend IP configuration name.

## Approve the private endpoint connection

1. Run [az network private-endpoint-connection list](/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-list) to get the **id** of the private endpoint connection that needs approval.

```azurecli-interactive

az network private-endpoint-connection list --name myAppGateway --resource-group myResourceGroup --type Microsoft.Network/applicationgateways

```

1. Run [az network private-endpoint-connection approve](/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-approve) to approve the private endpoint connection by using the **id** from the previous step.

```azurecli-interactive

az network private-endpoint-connection approve --id /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Network/applicationGateways/myAppGateway/privateEndpointConnections/aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb.bbbbbbbb-1111-2222-3333-cccccccccccc

```

## Complete Azure Front Door setup

Run [az afd route create](/cli/azure/afd/route#az-afd-route-create) to create a route that maps your endpoint to the origin group. This route forwards requests from the endpoint to your origin group.

```azurecli-interactive

az afd route create \

--resource-group myResourceGroup \

--profile-name myFrontDoorProfile \

--endpoint-name myFrontDoorEndpoint \

--forwarding-protocol MatchRequest \

--route-name myRoute \

--https-redirect Enabled \

--origin-group myOriginGroup \

--supported-protocols Http Https \

--link-to-default-domain Enabled

```

Your Azure Front Door profile is fully functional after you complete this final step.

## Common mistakes to avoid

Avoid these common mistakes when configuring an Azure Application Gateway origin with Azure Private Link enabled:

1. Configuring Azure Front Door origin before configuring Azure Private Link on the Azure Application Gateway.

1. Adding the Azure Application Gateway origin with Azure Private Link to an existing origin group that contains public origins. Azure Front Door doesn't allow mixing public and private origins in the same origin group.

1. Exceeding 70 characters in the combined length of the Application Gateway name and Private Link configuration name, which causes deployment failures.

1. Not associating the Application Gateway frontend IP with a listener.

1. Configuring the origin with origin type as 'Application Gateway' instead of 'Custom'. When you choose the origin type as 'Application Gateway', the origin hostname is autopopulated with the IP address of the Application Gateway. This autopopulated IP address can lead to a `CertificateNameValidation` error. To avoid this error for public origins, disable certificate subject name validation. For private link enabled origins, certificate subject name validation is mandatory.

1. Providing an incorrect Azure Application Gateway frontend IP configuration name as the value for `SharedPrivateLinkResourceGroupId`.

1. Providing an incorrect Azure Application Gateway frontend IP configuration name as the value for `private-link-sub-resource-type`.

## Next step

> [!div class="nextstepaction"]

> [Private Link service with storage account](../storage/common/storage-private-endpoints.md)


# How To Enable Private Link Apim

# Connect Azure Front Door Premium to an Azure API Management with Private Link

**Applies to:** :heavy_check_mark: Front Door Premium

This article guides you through the steps to configure an Azure Front Door Premium to connect privately to your Azure API Management origin using Azure Private Link.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An Azure API Management instance. For more information on how to create an API Management instance, see [Create a new Azure API Management instance](../../api-management/get-started-create-service-instance.md). For v1 tiers, the instance should be deployed in public mode and not in virtual network mode.

- An Azure Front Door Premium profile and an endpoint. For more information on how to create an Azure Front Door profile, see [Create a Front Door using the Azure portal](../create-front-door-portal.md).

- Sign in to the [Azure portal](https://portal.azure.com) with your Azure account.

- An Azure Front Door Premium profile and an endpoint. For more information on how to create an Azure Front Door profile, see [Create a Front Door using Azure PowerShell](../create-front-door-powershell.md)

- Azure Cloud Shell or Azure PowerShell.

The steps in this article run the Azure PowerShell cmdlets interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the cmdlets in the Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code and then paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure PowerShell locally](/powershell/azure/install-azure-powershell) to run the cmdlets. If you run PowerShell locally, sign in to Azure using the [Connect-AzAccount](/powershell/module/az.accounts/connect-azaccount) cmdlet.

- An Azure Front Door Premium profile and an endpoint. For more information on how to create an Azure Front Door profile, see [Create a Front Door using the Azure CLI](../create-front-door-cli.md).

- Azure Cloud Shell or Azure CLI.

The steps in this article run the Azure CLI commands interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the commands in the Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code, and paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure CLI locally](/cli/azure/install-azure-cli) to run the commands. If you run Azure CLI locally, sign in to Azure using the [az login](/cli/azure/reference-index#az-login) command.

## Create an origin group and add the API Management instance as an origin

1. Under **Settings** of your Azure Front Door Premium profile, select **Origin groups**.

1. Select **Add**

1. Enter a name for the origin group.

1. Select **+ Add an origin**

1. Use the following table to configure the origin settings:

| Setting | Value |

| ------- | ----- |

| Name | Enter a name to identify this origin. |

| Origin Type | Select **API Management**. |

| Host name | Select the host from the dropdown that you want as an origin. |

| Origin host header | Will be autopopulated with the host of the chosen API Management instance. |

| HTTP port | 80 (default). |

| HTTPS port | 443 (default). |

| Priority | Assign different priorities to origins for primary, secondary, and backup purposes. |

| Weight | 1000 (default). Use weights to distribute traffic among different origins. |

| Region | Select the region that matches or is closest to your origin. |

| Target sub resource | Select **Gateway**. |

| Request message | Enter a custom message to display while approving the Private Endpoint.  |

1. Select **Add** to save your origin settings

1. Select **Add** to save the origin group settings.

## Approve the private endpoint

1. Go to the API Management instance you configured with Private Link in the previous section.

1. Under **Deployment + infrastructure**, select **Network**.

1. Select **Inbound private endpoint connections** tab.

1. Find the *pending* private endpoint request from Azure Front Door Premium and select **Approve**.

1. After approval, the connection status will update. It can take a few minutes for the connection to fully establish. Once established, you can access your API Management through Front Door.

## Create an origin group and add the API Management instance as an origin

1. Use [New-AzFrontDoorCdnOriginGroupHealthProbeSettingObject](/powershell/module/az.cdn/new-azfrontdoorcdnorigingrouphealthprobesettingobject) to create an in-memory object for storing the health probe settings.

```azurepowershell-interactive

$healthProbeSetting = New-AzFrontDoorCdnOriginGroupHealthProbeSettingObject `

-ProbeIntervalInSecond 60 `

-ProbePath "/" `

-ProbeRequestType GET `

-ProbeProtocol Http

```

1. Use [New-AzFrontDoorCdnOriginGroupLoadBalancingSettingObject](/powershell/module/az.cdn/new-azfrontdoorcdnorigingrouploadbalancingsettingobject) to create an in-memory object for storing load balancing settings.

```azurepowershell-interactive

$loadBalancingSetting = New-AzFrontDoorCdnOriginGroupLoadBalancingSettingObject `

-AdditionalLatencyInMillisecond 50 `

-SampleSize 4 `

-SuccessfulSamplesRequired 3

```

1. Run [New-AzFrontDoorCdnOriginGroup](/powershell/module/az.cdn/new-azfrontdoorcdnorigingroup) to create an origin group that contains your API Management instance.

```azurepowershell-interactive

$origingroup = New-AzFrontDoorCdnOriginGroup `

-OriginGroupName myOriginGroup `

-ProfileName myFrontDoorProfile `

-ResourceGroupName myResourceGroup `

-HealthProbeSetting $healthProbeSetting `

-LoadBalancingSetting $loadBalancingSetting

```

1. Use the [New-AzFrontDoorCdnOrigin](/powershell/module/az.cdn/new-azfrontdoorcdnorigin) command to add your API Management instance to the origin group.

```azurepowershell-interactive

New-AzFrontDoorCdnOrigin `

-OriginGroupName myOriginGroup `

-OriginName myAPIMOrigin `

-ProfileName myFrontDoorProfile `

-ResourceGroupName myResourceGroup `

-HostName myapim.azure-api.net `

-HttpPort 80 `

-HttpsPort 443 `

-OriginHostHeader myapim.azure-api.net `

-Priority 1 `

-PrivateLinkId /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.ApiManagement/service/myAPIM `

-SharedPrivateLinkResourceGroupId Gateway `

-SharedPrivateLinkResourcePrivateLinkLocation CentralUS `

-SharedPrivateLinkResourceRequestMessage 'Azure Front Door private connectivity request' `

-Weight 1000 `

```

## Approve the private endpoint

1. Run [Get-AzPrivateEndpointConnection](/powershell/module/az.network/get-azprivateendpointconnection) to retrieve the connection name of the private endpoint connection that needs approval.

```azurepowershell-interactive

$PrivateEndpoint = Get-AzPrivateEndpointConnection -ResourceGroupName myResourceGroup -ServiceName myAPIM -PrivateLinkResourceType Microsoft.ApiManagement/service

```

2. Run [Approve-AzPrivateEndpointConnection](/powershell/module/az.network/approve-azprivateendpointconnection) to approve the private endpoint connection details. Use the *Name* value from the output in the previous step for approving the connection.

```azurepowershell-interactive

Get-AzPrivateEndpointConnection -Name $PrivateEndpoint.Name -ResourceGroupName myResourceGroup -ServiceName myAPIM -PrivateLinkResourceType Microsoft.ApiManagement/service

```

## Complete Azure Front Door setup

Use the [New-AzFrontDoorCdnRoute](/powershell/module/az.cdn/new-azfrontdoorcdnroute) command to create a route that maps your endpoint to the origin group. This route forwards requests from the endpoint to your origin group.

```azurepowershell-interactive

# Create a route to map the endpoint to the origin group

$Route = New-AzFrontDoorCdnRoute `

-EndpointName myFrontDoorEndpoint `

-Name myRoute `

-ProfileName myFrontDoorProfile `

-ResourceGroupName myResourceGroup `

-ForwardingProtocol MatchRequest `

-HttpsRedirect Enabled `

-LinkToDefaultDomain Enabled `

-OriginGroupId $origingroup.Id `

-SupportedProtocol Http,Https

```

Your Azure Front Door profile is now fully functional after completing the final step.

## Create an origin group and add the API Management instance as an origin

1. Run [az afd origin-group create](/cli/azure/afd/origin-group#az-afd-origin-group-create) to create an origin group.

```azurecli-interactive

az afd origin-group create \

--resource-group myResourceGroup \

--origin-group-name myOriginGroup \

--profile-name myFrontDoorProfile \

--probe-request-type GET \

--probe-protocol Http \

--probe-interval-in-seconds 60 \

--probe-path / \

--sample-size 4 \

--successful-samples-required 3 \

--additional-latency-in-milliseconds 50

```

1. Run [az afd origin create](/cli/azure/afd/origin#az-afd-origin-create) to add the API Management instance as an origin to the origin group.

```azurecli-interactive

az afd origin create \

--enabled-state Enabled \

--resource-group myResourceGroup \

--origin-group-name myOriginGroup \

--origin-name myAPIMOrigin \

--profile-name myFrontDoorProfile \

--host-name myapim.azure-api.net \

--origin-host-header myapim.azure-api.net \

--http-port 80  \

--https-port 443 \

--priority 1 \

--weight 500 \

--enable-private-link true \

--private-link-location centralus \

--private-link-request-message 'Azure Front Door private connectivity request.' \

--private-link-resource /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.ApiManagement/service/myAPIM \

--private-link-sub-resource-type Gateway

```

## Approve the private endpoint connection

1. Run [az network private-endpoint-connection list](/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-list) to get the **name** of the private endpoint connection that needs approval.

```azurecli-interactive

az network private-endpoint-connection list --name myAPIM --resource-group myResourceGroup --type Microsoft.ApiManagement/service

```

1. Run [az network private-endpoint-connection approve](/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-approve) to approve the private endpoint connection using the **name** from the previous step.

```azurecli-interactive

az network private-endpoint-connection approve --id /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.ApiManagement/service/myAPIM/privateEndpointConnections/aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb

```

## Complete Azure Front Door setup

Run [az afd route create](/cli/azure/afd/route#az-afd-route-create) to create a route that maps your endpoint to the origin group. This route forwards requests from the endpoint to your origin group.

```azurecli-interactive

az afd route create \

--resource-group myResourceGroup \

--profile-name myFrontDoorProfile \

--endpoint-name myFrontDoorEndpoint \

--forwarding-protocol MatchRequest \

--route-name myRoute \

--https-redirect Enabled \

--origin-group myOriginGroup \

--supported-protocols Http Https \

--link-to-default-domain Enabled

```

Your Azure Front Door profile is now fully functional after completing the final step.

## Common mistakes to avoid

The following are common mistakes when configuring an Azure API Management origin with Azure Private Link enabled:

* Adding the Azure API Management origin with Azure Private Link to an existing origin group that contains public origins. Azure Front Door doesn't allow mixing public and private origins in the same origin group.

## Next step

> [!div class="nextstepaction"]

> [Private Link service with storage account](../../storage/common/storage-private-endpoints.md)


# How To Configure Caching

# Configure caching on Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

This article shows you how to configure caching on Azure Front Door. To learn more about caching, see [Caching with Azure Front Door](front-door-caching.md).

## Prerequisites

Before you can create an Azure Front Door endpoint with Front Door manager, you must have an Azure Front Door profile created. The profile must have at least one or more endpoints. To organize your Azure Front Door endpoints by internet domains, web applications, or other criteria, you can use multiple profiles.

To create an Azure Front Door profile and endpoint, see [Create an Azure Front Door profile](create-front-door-portal.md).

Caching can significantly decrease latency and reduce the load on origin servers. However, not all types of traffic can benefit from caching. Static assets such as images, CSS, and JavaScript files are ideal for caching. While dynamic assets, such as authenticated API endpoints, shouldn't be cached to prevent the leakage of personal information. We recommend having separate routes for static and dynamic assets, with caching disabled for the latter.

> [!WARNING]

> Before you enable caching, thoroughly review the caching documentation, and test all possible scenarios before enabling caching. As noted previously, with misconfiguration you can inadvertently cache user specific data that can be shared by multiple users resulting privacy incidents.

## Configure caching by using the Azure portal

1. Sign in to the [Azure portal](https://portal.azure.com?azure-portal=true) and navigate to your Azure Front Door profile.

1. Select **Front Door manager** and then select your route.

1. Select **Enable caching**.

1. Specify the query string caching behavior. For more information, see [Caching with Azure Front Door](front-door-caching.md#query-string-behavior).

1. Optionally, select **Enable compression** for Front Door to compress responses to the client.

1. Select **Update**.

## Next steps

* Learn about the use of [origins and origin groups](origin.md) in an Azure Front Door configuration.

* Learn about [rules match conditions](rules-match-conditions.md) in an Azure Front Door rule set.

* Learn more about [policy settings](../web-application-firewall/afds/waf-front-door-policy-settings.md) for Web Application Firewall (WAF) with Azure Front Door.

* Learn how to create [custom rules](../web-application-firewall/afds/waf-front-door-custom-rules.md) to protect your Azure Front Door profile.


# Cache Purge

# Purge cache in Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Azure Front Door caches assets until their time-to-live (TTL) expires. When a client requests an asset with an expired TTL, Azure Front Door retrieves and caches a new copy of the asset to serve the request.

To ensure users always get the latest assets, version your assets for each update and publish them with new URLs. Azure Front Door then fetches the new assets on subsequent client requests.

When you update your application or need to quickly remove incorrect content, purge cached content from all point-of-presence (PoP) locations. This action forces Azure Front Door to fetch fresh content from your origin.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- Review [Caching with Azure Front Door](front-door-caching.md) to understand how caching works.

- An Azure Front Door profile. For more information, see [Create an Azure Front Door](create-front-door-portal.md).

- Sign in to the [Azure portal](https://portal.azure.com) and open your Azure Front Door profile.

- An Azure Front Door profile. For more information, see [Create an Azure Front Door](create-front-door-powershell.md).

- Azure Cloud Shell or Azure PowerShell.

The steps in this article run the Azure PowerShell cmdlets interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the cmdlets in the Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code and then paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure PowerShell locally](/powershell/azure/install-azure-powershell) to run the cmdlets. If you run PowerShell locally, sign in to Azure using the [Connect-AzAccount](/powershell/module/az.accounts/connect-azaccount) cmdlet.

- An Azure Front Door profile. For more information, see [Create an Azure Front Door](create-front-door-cli.md).

- Azure Cloud Shell or Azure CLI.

The steps in this article run the Azure CLI commands interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the commands in the Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code, and paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure CLI locally](/cli/azure/install-azure-cli) to run the commands. If you run Azure CLI locally, sign in to Azure using the [az login](/cli/azure/reference-index#az-login) command.

## Purge cache

1. Go to the overview page of your Azure Front Door profile and select **Purge cache**.

1. Choose an endpoint, and then select the domain or subdomain that you want to purge from Front Door POPs. You can select multiple domains or subdomains.

1. To clear all assets, select **Purge all assets for the selected domains**. Otherwise, enter the **Paths** of each asset you want to purge.

Run [Clear-AzFrontDoorCdnEndpointContent](/powershell/module/az.cdn/clear-azfrontdoorcdnendpointcontent) to purge cache by specifying parameters such as:

- Resource group name.

- Azure Front Door profile name within the resource group.

- Endpoints with assets to purge.

- Domains and subdomains with assets to purge.

```azurepowershell-interactive

Clear-AzFrontDoorCdnEndpointContent `

-ResourceGroupName myRGFD `

-ProfileName contosoafd `

-EndpointName myendpoint `

-Domain www.contoso.com `

-ContentPath /scripts/*

```

Run [az afd endpoint purge](/cli/azure/afd/endpoint#az-afd-endpoint-purge) with the necessary parameters to purge cache:

- Resource group name

- Azure Front Door profile name within the resource group

- Endpoints with assets to purge

- Domains and subdomains with assets to purge

```azurecli-interactive

az afd endpoint purge \

--resource-group myRGFD \

--profile-name contosoafd \

--endpoint-name myendpoint \

--domains www.contoso.com \

--content-paths '/scripts/*'

```

### Supported path formats

- **Single path purge**: Purge one asset by specifying its full path without protocol and domain, including file extension. For example, `/pictures/strasbourg.png`.

- **Root domain purge**: Purge the root of the endpoint with `/*` in the path.

> [!IMPORTANT]

> Cache purge for wildcard domains isn't supported directly. Specify subdomains for wildcard domains. For example, for `*.contoso.com`, specify subdomains such as `dev.contoso.com` or `test.contoso.com`. For more information, see [Wildcard domains in Azure Front Door](front-door-wildcard-domain.md).

Cache purges on Azure Front Door are case-insensitive and query-string agnostic. Purging a URL purges all query-string variations of that URL.

> [!NOTE]

> Cache purging can take up to 10 minutes to propagate across all Azure Front Door POP locations.

## Next step

> [!div class="nextstepaction"]

> [Create an Azure Front Door profile](create-front-door-portal.md)


# Integrate Storage Account

# Integrate an Azure Storage account with Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Azure Front Door can be used to deliver high-bandwidth content by caching blobs from Azure Storage. In this article, you create an Azure Storage account and enable Front Door to cache and accelerate content from Azure Storage.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Sign in to the Azure portal

Sign in to the [Azure portal](https://portal.azure.com) with your Azure account.

## Create a storage account

A storage account provides access to Azure Storage services. It represents the highest level of the namespace for accessing each Azure Storage service component: Azure Blob, Queue, and Table storage. For more information, see [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).

1. In the Azure portal, select **+ Create a resource** in the upper left corner. The **Create a resource** pane appears.

1. On the **Create a resource** page, search for **Storage account** and select **Storage account** from the list. Then select **Create**.

1. On the **Create a storage account** page, enter or select the following information for the new storage account:

| Setting | Value |

| --- | --- |

| Resource group | Select **Create new** and enter the name **AFDResourceGroup**. You can also select an existing resource group. |

| Storage account name | Enter a name for the account using 3-24 lowercase letters and numbers only. The name must be unique across Azure and becomes the host name in the URL used to address blob, queue, or table resources for the subscription. To address a container resource in Blob storage, use a URI in the following format: http://*&lt;storageaccountname&gt;*.blob.core.windows.net/*&lt;container-name&gt;*. |

| Region | Select an Azure region closest to you from the drop-down list. |

Leave all other settings as default. Select the **Review** tab, select **Create**, and then select **Review + Create**.

1. The creation of the storage account can take a few minutes to complete. Once creation is complete, select **Go to resource** to go to the new storage account resource.

## Enable Azure Front Door CDN for the storage account

1. From the storage account resource, select **Front Door and CDN** under **Security + networking** in the left menu.

1. In the **New endpoint** section, enter the following information:

| Setting  | Value |

| -------- | ----- |

| Service type | Select **Azure Front Door**. |

| Create new/use existing profile | Choose to create a new Front Door profile or select an existing one. |

| Profile name | Enter a name for the Front Door profile. If you selected **Use existing**, choose from the available profiles. |

| Endpoint name | Enter your endpoint hostname, such as *contoso1234*. This name is used to access your cached resources at the URL _&lt;endpoint-name + hash value&gt;_.z01.azurefd.net. |

| Origin hostname | By default, a new Front Door endpoint uses the hostname of your storage account as the origin server. |

| Pricing tier | Select **Standard** for content delivery or **Premium** for content delivery with security features. |

| Caching | *Optional* - Toggle on to [enable caching](front-door-caching.md) for your static content. Choose an appropriate query string behavior and enable compression if needed. |

| WAF | *Optional* - Toggle on to protect your endpoint from vulnerabilities, malicious actors, and bots with [Web Application Firewall](web-application-firewall.md). Use an existing policy from the WAF policy dropdown or create a new one. |

| Private link | *Optional* - Toggle on to keep your storage account private, not exposed to the public internet. Select the region that matches your storage account or is closest to your origin. Choose **blob** as the target subresource. |

> [!NOTE]

> * With the Standard tier, you can only use custom rules with WAF. To deploy managed rules and bot protection, choose the Premium tier. For a detailed comparison, see [Azure Front Door tier comparison](./standard-premium/tier-comparison.md).

> * The Private Link feature is **only** available with the Premium tier.

1. Select **Create** to create the new endpoint. After creation, it appears in the endpoint list.

> [!NOTE]

> * The endpoint list will only show Front Door and CDN profiles within the same subscription.

## Extra features

From the storage account **Front Door and CDN** page, select the endpoint from the list to open the Front Door endpoint configuration page. Here, you can enable other Azure Front Door features such as the [rules engine](front-door-rules-engine.md) and configure traffic [load balancing](routing-methods.md).

For best practices, refer to [Use Azure Front Door with Azure Storage blobs](scenario-storage-blobs.md).

## Enable SAS

To grant limited access to private storage containers, use the Shared Access Signature (SAS) feature of your Azure Storage account. A SAS is a URI that grants restricted access rights to your Azure Storage resources without exposing your account key.

## Access CDN content

To access cached content with Azure Front Door, use the Front Door URL provided in the portal. The address for a cached blob follows this format:

http://<*endpoint-name-with-hash-value*\>.z01.azurefd.net/<*myPublicContainer*\>/<*BlobName*\>

> [!NOTE]

> After enabling Azure Front Door access to a storage account, all publicly available objects are eligible for Front Door POP (Point-of-presence) caching. If you modify an object that is currently cached in Front Door, the new content won't be available until Front Door refreshes its content after the time-to-live period expires.

## Add a custom domain

Using a custom domain with Azure Front Door allows your own domain name to be visible in end-user requests, which can enhance customer convenience and support branding efforts.

To add a custom domain:

1. Navigate to the storage account *Front Door and CDN** page.

1. Select **View custom domains** for the Azure Front Door endpoint.

1. On the domains page, add a new custom domain to access your storage account.

For detailed instructions, see [Configure a custom domain with Azure Front Door](./standard-premium/how-to-add-custom-domain.md).

## Purge cached content from Azure Front Door

If you no longer want to cache an object in Azure Front Door, you can purge the cached content.

1. Navigate to the storage account **Front Door and CDN** page.

1. Select the Azure Front Door endpoint from the list to open the Azure Front Door endpoint configuration page.

1. Select on the **Purge cache** option at the top of the page.

1. Select the endpoint, domain, and path you want to purge.

> [!NOTE]

> An object already cached in Azure Front Door will remain cached until the time-to-live period expires or until you purge the endpoint.

## Clean up resources

In the preceding steps, you created an Azure Front Door profile and an endpoint in a resource group. If you no longer need these resources, you can delete them to avoid incurring charges.

1. In the Azure portal, select **Resource groups** from the left-hand menu, then select **AFDResourceGroup**.

1. On the **Resource group** page, select **Delete resource group**. Enter **AFDResourceGroup** in the text box, then select **Delete**. This action deletes the resource group, profile, and endpoint created in this guide.

1. To delete your storage account, select the storage account from the dashboard, then select **Delete** from the top menu.

## Next steps

* Learn how to use [Azure Front Door with Azure Storage blobs](scenario-storage-blobs.md)

* Learn how to [enable Azure Front Door Private Link with Azure Blob Storage](standard-premium/how-to-enable-private-link-storage-account.md)

* Learn how to [enable Azure Front Door Private Link with Storage Static Website](how-to-enable-private-link-storage-static-website.md)


# Tier Migration

# Azure Front Door (classic) to Standard/Premium tier migration

**Applies to:** :heavy_check_mark: Front Door (classic)

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

Azure Front Door Standard and Premium tier were released in March 2022 as the next generation content delivery network service. The newer tiers combine the capabilities of Azure Front Door (classic), Microsoft CDN (classic), and Web Application Firewall (WAF). With features such as Private Link integration, enhanced rules engine and advanced diagnostics you have the ability to secure and accelerate your web applications to bring a better experience to your customers.

We recommend migrating your classic profile to one of the newer tier to benefit from the new features and improvements. To ease the move to the new tiers, Azure Front Door provides a zero-downtime migration to move your workload from Azure Front Door (classic) to either Standard or Premium.

In this article you'll learn about the migration process, understand the breaking changes involved, and what to do before, during and after the migration.

## Migration process overview

Migrating to Standard or Premium tier for Azure Front Door happens in either three or five phases depending on if you're using your certificate. The time it takes to migrate depends on the complexity of your Azure Front Door (classic) profile. You can expect the migration to take a few minutes for a simple Azure Front Door profile and longer for a profile that has multiple frontend domains, backend pools, routing rules and rule engine rules.

### Phases of migration

#### Validate compatibility

The migration tool checks to see if your Azure Front Door (classic) profile is compatible for migration. If validation fails, you're provided with suggestions on how to resolve any issues before you can validate again.

* Azure Front Door Standard and Premium require all custom domains to use HTTPS. If you don't have your own certificate, you can use an Azure Front Door managed certificate. The certificate is free of charge and gets managed for you.

* Session affinity gets enabled in the origin group settings for an Azure Front Door Standard or Premium profile. In Azure Front Door (classic), session affinity is set at the domain level. As part of the migration, session affinity is based on the Front Door (classic) profile settings. If you have two domains in your Front Door (classic) profile that shares the same backend pool, session affinity has to be consistent across both domains in order for migration validation to pass.

* If you're using BYOC (Bring Your Own Certificate) for Azure Front Door (classic), you need to [grant Key Vault access](standard-premium/how-to-configure-https-custom-domain.md#register-azure-front-door) to Azure Front Door Standard or Premium. This step is required for Azure Front Door Standard or Premium to access your certificate in Key Vault. If you're using Azure Front Door managed certificate, you don't need to grant Key Vault access.

> [!NOTE]

> Managed certificate is currently **not supported** for Azure Front Door Standard or Premium in Azure Government Cloud. You need to use BYOC for Azure Front Door Standard or Premium in Azure Government Cloud or wait until this capability is available..

#### Prepare for migration

Azure Front Door creates a new Standard or Premium profile based on your Front Door (classic) profile's configuration. The new Front Door profile tier depends on the Web Application Firewall (WAF) policy settings you associate with the profile.

* **Premium** - If your WAF policy has **managed WAF rules** associated to the Azure Front Door (classic) profile.

* **Standard** - If your WAF policy only has **custom WAF rules** associated to the Azure Front Door (classic) profile.

> [!NOTE]

> A standard tier Front Door profile **can** be upgraded to premium tier after migration. However, a premium tier Front Door profile **can't** be downgraded to standard tier after migration.

During the preparation phase, Azure Front Door creates a copy of each WAF policy associated to the Front Door (classic) profile. The WAF policy tier is specific to the tier you're migrating to. A default name is provided for each WAF policy and you can change the name during this phase. You also can select an existing WAF policy that matches the tier you're migrating to instead of making a copy. Once the preparation phase is completed, a read-only view of the new Front Door profile is provided for you to verify configurations.

> [!IMPORTANT]

> You won't be able to make changes to the Front Door (classic) configuration once the preparation phase has been initiated.

#### Enable managed identity

During this step, you configure managed identity for Azure Front Door to access your certificate in an Azure Key Vault. Managed identity is required if you're using BYOC (Bring Your Own Certificate) for Azure Front Door (classic). If you're using Azure Front Door managed certificate, you don't need to grant Key Vault access.

#### Grant managed identity to Key Vault

This step adds managed identity access to all Azure Key Vaults used in the Front Door (classic) profile.

#### Migrate

Before committing to migration in this step, if you decided you no longer want to move forward with the migration process, you can select **Abort migration**. Aborting the migration deletes the new Front Door profile that was created. The Azure Front Door (classic) profile remains active and you can continue to use it. Any WAF policy copies need to be manually deleted.

**However, once customer commits to migration in this step, there is no abortion or rollback.** Once migration begins, the Azure Front Door (classic) profile gets disabled and the Azure Front Door Standard, or Premium profile gets activated. Traffic starts flowing through the new profile once the migration completes.

The migration is on control plane and the data plane remains the same. In normal cases, the migration won't fail. However, in rare cases, if the migration fails at this step, there is no impact on traffic delivery. The only impact is customer won't be able to make changes to AFD profile.

Service charges for Azure Front Door Standard or Premium tier start once migration is completed.

## Breaking changes when migrating to Standard or Premium tier

> [!IMPORTANT]

> * If your Azure Front Door (classic) profile can qualify to migrate to Standard tier but the number of resources exceeds the Standard tier quota limit, it will be migrated to Premium tier instead.

> * If you use Azure PowerShell, Azure CLI, API, or Terraform to do the migration, then you need to create WAF policies separately.

### DevOps

Azure Front Door Standard and Premium use a different resource provider namespace of *Microsoft.Cdn*, while Azure Front Door (classic) uses *Microsoft.Network*. After you migrate your Azure Front Door profile, you'll need to change your DevOps script to use the new namespace, updated Azure PowerShell module, CLI commands, and APIs.

### Endpoint with hash value

Azure Front Door Standard and Premium endpoints are generated to include a hash value to prevent your domain from being taken over. The format of the endpoint name is `<endpointname>-<hashvalue>.z01.azurefd.net`. The Front Door (classic) endpoint name will continue to work after migration but we recommend replacing it with the newly created endpoint name from your new Standard or Premium profile. For more information, see [Endpoint domain names](endpoint.md#endpoint-domain-names).

### Logs and metrics

Diagnostic logs and metrics aren't migrated. Azure Front Door Standard and Premium log fields are different from Azure Front Door (classic). Standard and Premium tier has heath probe logging and we recommend that you enable diagnostic logging after you migrate. Standard and Premium tier also supports built-in reports that start displaying data once the migration is completed. For more information, see [Azure Front Door reports](standard-premium/how-to-reports.md).

### Web Application Firewall (WAF)

The default Azure Front Door tier selected for migration gets determined by the type of rules contain in the WAF policy. In this section, we cover scenarios for different rule types for a WAF policy.

**Classic WAF policy with only custom rules** - the new Azure Front Door profile defaults to Standard tier and can be upgraded to Premium during the migration. If you use the portal for migration, Azure creates custom WAF rules for Standard. If you upgrade to Premium during migration, custom WAF rules are created as part of the migration process. You'll need to add managed WAF rules manually after migration if you want to use managed rules.

**Classic WAF policy with only managed WAF rules, or both managed and custom WAF rules** - the new Azure Front Door profile defaults to Premium tier and can't be downgraded during the migration. If you want to use Standard tier, then you need to remove the WAF policy association or delete the managed WAF rules from the Front Door (classic) WAF policy.

> [!NOTE]

> To avoid creating duplicate WAF policies during migration, the migration capability provides the option to either create copies or use an existing Azure Front Door Standard or Premium WAF policy.

### Azure Policy for Azure Front Door WAF

[Azure Policy for WAF](../web-application-firewall/shared/waf-azure-policy.md) isn't available for Azure Front Door Standard and Premium. Azure Policy lets you set and check WAF standards for your organization at a large scale.

## Naming convention used for migration

During the migration, a default profile name is used in the format of `<endpointprefix>-migrated`. For example, an Azure Front Door (classic) endpoint named `myEndpoint.azurefd.net`, has the default name of `myEndpoint-migrated`.

A WAF policy name has `-standard` or `-premium` appended to the classic WAF policy name. For example, a Front Door (classic) WAF policy named `contosoWAF1`, has the default name of `contosoWAF1-premium`. You can rename both the Front Door profile and WAF policy during migration process. Renaming of rules engine configuration and routes aren't supported and instead default names are assigned.

URL redirect and URL rewrite are supported through rules engine in Azure Front Door Standard and Premium, while Azure Front Door (classic) supports them through routing rules. During migration, these two rules get created as rule set rules in a Standard and Premium profile. The namings of these rules are `urlRewriteMigrated` and `urlRedirectMigrated`.

## Resource states

The following table explains the various stages of the migration process and if changes can be made to the profile.

| Migration state | Front Door (classic) resource state | Can make changes? | Front Door Standard/Premium | Can make changes? |

|--|--|--|--|--|

| Before migration | Active | Yes | N/A | N/A |

| Validating compatibility | Active | Yes | N/A | N/A |

| Prepare for migration | Migrating | No | Creating | No |

| Committing migration | Migrating | No | CommittingMigration | No |

| Committed migration | Migrated | No | Active | Yes |

| Aborting migration | AbortingMigration | No | Deleting | No |

| Aborted migration | Active | Yes | Deleted | N/A |

## Related content

* Understand the [settings mapping between Azure Front Door tiers](tier-mapping.md).

* Learn how to [migrate from Azure Front Door (classic) to Standard or Premium tier](migrate-tier.md) using the Azure portal.

* Learn how to [migrate from Azure Front Door (classic) to Standard or Premium tier](migrate-tier-powershell.md) using Azure PowerShell.


# Tier Mapping

# Settings mapped between Azure Front Door (classic) and Standard/Premium tier

**Applies to:** :heavy_check_mark: Front Door (classic)

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

When migrating from Azure Front Door (classic) to Azure Front Door Standard or Premium, some configurations are changed or relocated for a better management experience. This article explains how routing rules, cache duration, rules engine configuration, WAF policy, and custom domains are mapped in the new Azure Front Door tier.

## Routing rules

| Azure Front Door (classic) settings | Mapping in Azure Front Door Standard and Premium |

|--|--|

| Route status - enable/disable | Changes to **Enable route** with a checkbox. Location remains the same. |

| Accepted protocol | Copied from Azure Front Door (classic) profile. |

| Frontend/domains | Changes to **Domains**. Copied from Azure Front Door (classic) profile. |

| Patterns to match | Copied from Azure Front Door (classic) profile. |

| Rules engine configuration | The rules engine configuration name changes to rule set but retains its association with routes from the Azure Front Door (classic) profile. |

| Route type: *Forwarding* | Backend pool changes to origin group. Forwarding protocol is copied from the Azure Front Door (classic) profile.</br> - If URL rewrite is **disabled**, the origin path in the Standard or Premium profile is *blank*.</br> - If URL rewrite is **enabled**, the *Custom forwarding path* of the Azure Front Door (classic) profile is set as the *origin path*. |

| Route type: Redirect | A URL redirect rule set called *URLRedirectMigratedRuleSet1* is created with a URL redirect rule. |

## Cache duration

In Azure Front Door (classic), the *Minimum cache duration* is configured in the routing rules settings, and the *Use default cache duration* is set in the Rules engine configuration. Azure Front Door Standard and Premium only support changing caching duration in a Rule set rule.

| Azure Front Door (classic) | Mapping in Azure Front Door Standard and Premium |

|--|--|

| Caching is **disabled** and default caching is used. | Caching is set to **disabled**. |

| Caching is **enabled** and the default caching duration is used. | Caching is set to **enabled**, and the origin caching behavior is honored. |

| Caching is **enabled** and minimum caching duration is set. | Caching is set to **enabled** and the cache behavior is set to **override always** with the minimum cache duration from Azure Front Door (classic). |

| N/A | Caching is set to **enabled**. The caching behavior is set to override if the origin is missing, and the input cache duration is used. |

## Route configuration override in rules engine configuration

In Azure Front Door Standard and Premium, the route configuration override in a rules engine configuration from Azure Front Door (classic) is divided into three separate actions: URL redirect, URL rewrite, and route configuration override.

| Actions in rules engine configuration | Mapping in Azure Front Door Standard and Premium |

|--|--|

| Route type set to **Forward** | 1. If URL rewrite is **disabled**, all settings are copied to the Standard or Premium profile.</br>2. If URL rewrite is **enabled**, two rule actions are created: one for URL rewrite and one for the route configuration override. The *custom forwarding path* in the Azure Front Door (classic) profile is set as the **destination** for the URL rewrite action. |

| Route type set to **Redirect** | URL redirect action settings are copied over. |

| Route configuration override | Backend pool is mapped to an origin group. Caching settings remain the same. Query string is mapped to query string caching behavior, and dynamic compression is mapped to compression. |

| Use default cache duration | For more information, see the [cache duration](#cache-duration) section. |

## Next steps

* Learn more about the [Azure Front Door migration process](tier-migration.md).

* Learn how to migrate from Azure Front Door (classic) to Azure Front Door Standard or Premium using the [Azure portal](migrate-tier.md) or [Azure PowerShell](migrate-tier-powershell.md).


# Migrate Tier

# Migrate Azure Front Door (classic) to Standard or Premium tier

**Applies to:** :heavy_check_mark: Front Door (classic)

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

Azure Front Door Standard and Premium tiers offer advanced cloud delivery network features, enhanced security, and improved performance by using the Microsoft global network. This guide helps you migrate your Azure Front Door (classic) profile to a Standard or Premium tier profile.

## Prerequisites

* Review the [About Azure Front Door tier migration](tier-migration.md) article.

* Ensure your Azure Front Door (classic) profile meets the migration requirements:

* Azure Front Door Standard and Premium require all custom domains to use HTTPS. If you don't have your own certificate, you can use an Azure Front Door managed certificate, which is free and managed for you.

* Session affinity is enabled in the origin group settings for Azure Front Door Standard or Premium profiles. In Azure Front Door (classic), session affinity is set at the domain level. During migration, session affinity settings are based on the Azure Front Door (classic) profile. If you have two domains in your classic profile sharing the same backend pool (origin group), session affinity must be consistent across both domains for migration validation to pass.

> [!NOTE]

> No DNS changes are required before or during the migration. However, after migration completes and traffic is flowing through your new Azure Front Door profile, you must update your DNS records. For more information, see [Update DNS records](#update-dns-records).

## Validate compatibility

1. Navigate to your Azure Front Door (classic) resource and select **Migration** under *Settings*.

1. Select **Validate** to check if your Azure Front Door (classic) profile is compatible for migration. Validation can take up to two minutes depending on the complexity of your profile.

If the migration isn't compatible, select **View errors** to see the list of errors and recommendations for resolving them.

1. Once your Azure Front Door (classic) profile passes validation and is deemed compatible for migration, proceed to the preparation phase.

## Prepare for migration

1. A default name is provided for the new Azure Front Door profile. You can change this name before proceeding.

1. The Azure Front Door tier is automatically selected based on the Azure Front Door (classic) WAF policy settings.

* **Standard** - Selected if you only have custom WAF rules associated with the Azure Front Door (classic) profile. You can choose to upgrade to a Premium tier.

* **Premium** - Selected if you use managed WAF rules associated with the Azure Front Door (classic) profile. To use the Standard tier, remove the managed WAF rules from the Azure Front Door (classic) profile.

1. Select **Configure WAF policy upgrades** to decide whether to upgrade your current WAF policies or use an existing compatible WAF policy.

> [!NOTE]

> The **Configure WAF policy upgrades** link appears only if you have WAF policies associated with the Azure Front Door (classic) profile.

For each WAF policy associated with the Azure Front Door (classic) profile, select an action. You can copy the WAF policy to match the tier you're migrating to or use an existing compatible WAF policy. You can also change the WAF policy name from the default provided name. When you finish, select **Apply** to save your Azure Front Door WAF settings.

1. Select **Prepare**, and when prompted, select **Yes** to confirm that you want to proceed with the migration process. After you confirm, you can't make further changes to the Azure Front Door (classic) profile.

1. Select the link that appears to view the configuration of the new Azure Front Door profile. Review each setting to ensure they're correct. When done, select the **X** in the top right corner to return to the migration screen.

## Enable managed identities

If you're using your own certificate, you need to enable managed identity so Azure Front Door can access the certificate in your Azure Key Vault. Managed identity is a feature of Microsoft Entra ID that you can use to securely connect to other Azure services without managing credentials. For more information, see [What are managed identities for Azure resources?](../active-directory/managed-identities-azure-resources/overview.md)

> [!NOTE]

> * If you're not using your own certificate, you don't need to enable managed identities or grant access to the Key Vault. You can skip to the [**Migrate**](#migrate) phase.

1. Select **Enable** and then choose either **System assigned** or **User assigned** depending on the type of managed identity you want to use.

* **System assigned** - Toggle the status to **On** and then select **Save**.

* **User assigned** - To create a user-assigned managed identity, see [Create a user-assigned identity](../active-directory/managed-identities-azure-resources/how-manage-user-assigned-managed-identities.md). If you already have a user-assigned managed identity, select the identity, and then select **Add**.

1. Close the page to return to the migration page. You see that managed identities are successfully enabled.

## Grant managed identity access to Azure Key Vault

Select **Grant** to add the managed identity to all Azure Key Vaults used with the Azure Front Door (classic) profile.

## Migrate

1. Select **Migrate** to start the migration process. Confirm by selecting **Yes** when prompted. The migration duration depends on the complexity of your Azure Front Door (classic) profile.

> [!NOTE]

> If you cancel the migration, only the new Azure Front Door profile is deleted. You must manually delete any new WAF policy copies.

1. After migration completes, select the banner at the top of the page or the link in the success message to access the new Azure Front Door profile.

1. The Azure Front Door (classic) profile is now **Disabled** and can be deleted from your subscription.

> [!WARNING]

> Deleting the new profile after migration deletes the production environment, which is irreversible.

## Update DNS records

Azure Front Door (classic) uses a different fully qualified domain name (FQDN) than Azure Front Door Standard or Premium. For example, a classic endpoint might be `contoso.azurefd.net`, while a Standard or Premium endpoint might be `contoso-mdjf2jfgjf82mnzx.z01.azurefd.net`. For more information, see [Endpoints in Azure Front Door](endpoint.md).

You don't need to update your DNS records before or during the migration. Azure Front Door automatically routes traffic from the classic endpoint to your new Standard or Premium profile without any configuration changes.

After migration, update your DNS records to point to the new Azure Front Door endpoint. This update ensures your profile continues to function properly in the future. Updating DNS records doesn't cause any downtime and can be done at your convenience.

## Next steps

* Understand the [mapping between Azure Front Door tiers](tier-mapping.md) settings.

* Learn more about the [Azure Front Door tier migration process](tier-migration.md).


# Migrate Tier Powershell

# Migrate Azure Front Door (classic) to Standard/Premium tier with Azure PowerShell

**Applies to:** :heavy_check_mark: Front Door (classic)

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

Azure Front Door Standard and Premium tier bring the latest cloud delivery network features to Azure. With enhanced security features and an all-in-one service, your application content is secured and closer to your end users using the Microsoft global network. This article guides you through the migration process to move your Azure Front Door (classic) profile to either a Standard or Premium tier profile with Azure PowerShell.

## Prerequisites

* Review the [About Front Door tier migration](tier-migration.md) article.

* Ensure your Front Door (classic) profile can be migrated:

* Azure Front Door Standard and Premium require all custom domains to use HTTPS. If you don't have your own certificate, you can use an Azure Front Door managed certificate. The certificate is free of charge and gets managed for you.

* Session affinity gets enabled in the origin group settings for an Azure Front Door Standard or Premium profile. In Azure Front Door (classic), session affinity is set at the domain level. As part of the migration, session affinity is based on the Front Door (classic) profile settings. If you have two domains in your classic profile that shares the same backend pool (origin group), session affinity has to be consistent across both domains in order for migration validation to pass.

* Latest Azure PowerShell module installed locally or Azure Cloud Shell. For more information, see [Install and configure Azure PowerShell](/powershell/azure/install-azure-powershell).

> [!NOTE]

> You don't need to make any DNS changes before or during the migration process. However, once the migration completes and traffic is flowing through your new Azure Front Door profile, you need to update your DNS records. For more information, see [Update DNS records](#update-dns-records).

## Validate compatibility

1. Open Azure PowerShell and connect to your Azure account. For more information, see [Connect to Azure PowerShell](/powershell/azure/authenticate-azureps).

1. Test your Azure Front Door (classic) profile to see if it's compatible for migration. You can use the [Test-AzFrontDoorCdnProfileMigration](/powershell/module/az.cdn/test-azfrontdoorcdnprofilemigration) command to test your profile. Replace the values for the resource group name and resource ID with your own values. Use [Get-AzFrontDoor](/powershell/module/az.frontdoor/get-azfrontdoor) to get the resource ID for your Front Door (classic) profile.

Replace the following values in the command:

* `<subscriptionId>`: Your subscription ID.

* `<resourceGroupName>`: The resource group name of the Front Door (classic).

* `<frontdoorClassicName>`: The name of the Front Door (classic) profile.

```powershell-interactive

Test-AzFrontDoorCdnProfileMigration -ResourceGroupName <resourceGroupName> -ClassicResourceReferenceId /subscriptions/<subscriptionId>/resourcegroups/<resourceGroupName>/providers/Microsoft.Network/frontdoors/<frontdoorClassicName>

```

If the migration is compatible for migration, you see the following output:

```

CanMigrate DefaultSku

---------- ----------

True       Standard_AzureFrontDoor or Premium_AzureFrontDoor

```

If the migration isn't compatible, you see the following output:

```

CanMigrate DefaultSku

---------- ----------

False

```

## Prepare for migration

> [!NOTE]

> * Managed certificate is currently **not supported** for Azure Front Door Standard or Premium in Azure Government Cloud. You need to use BYOC for Azure Front Door Standard or Premium in Azure Government Cloud or wait until this capability is available.

#### [Without WAF and BYOC (Bring your own certificate)](#tab/without-waf-byoc)

Run the [Start-AzFrontDoorCdnProfilePrepareMigration](/powershell/module/az.cdn/start-azfrontdoorcdnprofilepreparemigration) command to prepare for migration. Replace the values for the resource group name, resource ID, profile name with your own values. For *SkuName* use either **Standard_AzureFrontDoor** or **Premium_AzureFrontDoor**. The *SkuName* is based on the output from the [Test-AzFrontDoorCdnProfileMigration](/powershell/module/az.cdn/test-azfrontdoorcdnprofilemigration) command.

Replace the following values in the command:

* `<subscriptionId>`: Your subscription ID.

* `<resourceGroupName>`: The resource group name of the Front Door (classic).

* `<frontdoorClassicName>`: The name of the Front Door (classic) profile.

```powershell-interactive

Start-AzFrontDoorCdnProfilePrepareMigration -ResourceGroupName <resourceGroupName> -ClassicResourceReferenceId /subscriptions/<subscriptionId>/resourcegroups/<resourceGroupName>/providers/Microsoft.Network/frontdoors/<frontdoorClassicName> -ProfileName myAzureFrontDoor -SkuName Premium_AzureFrontDoor

```

The output looks similar to the following:

```

Starting the parameter validation process.

The parameters have been successfully validated.

Your new Front Door profile is being created. Please wait until the process has finished completely. This may take several minutes.

Your new Front Door profile with the configuration has been successfully created.

```

#### [With WAF](#tab/with-waf)

1. Run the [Get-AzFrontDoorWafPolicy](/powershell/module/az.frontdoor/get-azfrontdoorwafpolicy) command to get the resource ID for your WAF policy. Replace the values for the resource group name and WAF policy name with your own values.

```powershell-interactive

Get-AzFrontDoorWafPolicy -ResourceGroupName myAFDResourceGroup -Name myClassicFrontDoorWAF

```

The output looks similar to the following:

```

PolicyMode                    : Detection

PolicyEnabledState            : Enabled

RedirectUrl                   :

CustomBlockResponseStatusCode : 403

CustomBlockResponseBody       :

RequestBodyCheck              : Disabled

CustomRules                   : {}

ManagedRules                  : {Microsoft.Azure.Commands.FrontDoor.Models.PSAzureManagedRule}

Etag                          :

ProvisioningState             : Succeeded

Sku                           : Classic_AzureFrontDoor

Tags                          :

Id                            : /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourcegroups/myAFDResourceGroup/providers/Microsoft.Network/frontdoorwebapplicationfirewallpolicies/myClassicFrontDoorWAF

Name                          : myFrontDoorWAF

Type                          :

```

1. Run the [New-AzFrontDoorCdnMigrationWebApplicationFirewallMappingObject](/powershell/module/az.cdn/new-azfrontdoorcdnmigrationwebapplicationfirewallmappingobject) command to create an in-memory object for WAF policy migration. Use the WAF ID in the last step for `MigratedFromId`. To use an existing WAF policy, replace the value for `MigratedToId` with a resource ID of a WAF policy that matches the Front Door tier you're migrating to. If you're creating a new WAF policy copy, you can change the name of the WAF policy in the resource ID.

```powershell-interactive

$wafMapping = New-AzFrontDoorCdnMigrationWebApplicationFirewallMappingObject -MigratedFromId /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourcegroups/myAFDResourceGroup/providers/Microsoft.Network/frontdoorwebapplicationfirewallpolicies/myClassicFrontDoorWAF -MigratedToId  /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourcegroups/myAFDResourceGroup/providers/Microsoft.Network/frontdoorwebapplicationfirewallpolicies/myFrontDoorWAF

1. Run the [Start-AzFrontDoorCdnProfilePrepareMigration](/powershell/module/az.cdn/start-azfrontdoorcdnprofilepreparemigration) command to prepare for migration. Replace the values for the resource group name, resource ID, profile name with your own values. For *SkuName* use either **Standard_AzureFrontDoor** or **Premium_AzureFrontDoor**. The *SkuName* is based on the output from the [Test-AzFrontDoorCdnProfileMigration](/powershell/module/az.cdn/test-azfrontdoorcdnprofilemigration) command.

Replace the following values in the command:

* `<subscriptionId>`: Your subscription ID.

* `<resourceGroupName>`: The resource group name of the Front Door (classic).

* `<frontdoorClassicName>`: The name of the Front Door (classic) profile.

```powershell-interactive

Start-AzFrontDoorCdnProfilePrepareMigration -ResourceGroupName <resourceGroupName> -ClassicResourceReferenceId /subscriptions/<subscriptionId>/resourcegroups/<resourceGroupName>/providers/Microsoft.Network/frontdoors/<frontdoorClassicName> -ProfileName myAzureFrontDoor -SkuName Premium_AzureFrontDoor -MigrationWebApplicationFirewallMapping $wafMapping

```

The output looks similar to the following:

```

Starting the parameter validation process.

The parameters have been successfully validated.

Your new Front Door profile is being created. Please wait until the process has finished completely. This may take several minutes.

Your new Front Door profile with the configuration has been successfully created.

```

#### [With BYOC](#tab/with-byoc)

If you're migrating a Front Door profile with BYOC, you need to enable managed identity on the Front Door profile. You need to grant the Front Door profile access to the key vault where the certificate is stored.

Run the [Start-AzFrontDoorCdnProfilePrepareMigration](/powershell/module/az.cdn/start-azfrontdoorcdnprofilepreparemigration) command to prepare for migration. Replace the values for the resource group name, resource ID, profile name with your own values. For *SkuName* use either **Standard_AzureFrontDoor** or **Premium_AzureFrontDoor**. The *SkuName* is based on the output from the [Test-AzFrontDoorCdnProfileMigration](/powershell/module/az.cdn/test-azfrontdoorcdnprofilemigration) command.

### System assigned

For *IdentityType* use **SystemAssigned**.

```powershell-interactive

Start-AzFrontDoorCdnProfilePrepareMigration -ResourceGroupName myAFDResourceGroup -ClassicResourceReferenceId /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourcegroups/myAFDResourceGroup/providers/Microsoft.Network/Frontdoors/myAzureFrontDoorClassic -ProfileName myAzureFrontDoor -SkuName Premium_AzureFrontDoor -IdentityType SystemAssigned

```

### User assigned

1. Run the [Get-AzUserAssignedIdentity](/powershell/module/az.managedserviceidentity/get-azuserassignedidentity) command to the get the resource ID for a user assigned identity.

```powershell-interactive

$id = Get-AzUserAssignedIdentity -ResourceGroupName myResourceGroup -Name afduseridentity

$id.Id

```

The output looks similar to the following:

```

/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourcegroups/myAFDResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/afduseridentity

```

1. For IdentityType use UserAssigned and for IdentityUserAssignedIdentity,* use the resource ID from the previous step.

Replace the following values in the command:

* `<subscriptionId>`: Your subscription ID.

* `<resourceGroupName>`: The resource group name of the Front Door (classic).

* `<frontdoorClassicName>`: The name of the Front Door (classic) profile.

```powershell-interactive

Start-AzFrontDoorCdnProfilePrepareMigration -ResourceGroupName <resourceGroupName> -ClassicResourceReferenceId /subscriptions/<subscriptionId>/resourcegroups/<resourceGroupName>/providers/Microsoft.Network/frontdoors/<frontdoorClassicName> -ProfileName myAzureFrontDoor -SkuName Premium_AzureFrontDoor -IdentityType UserAssigned -IdentityUserAssignedIdentity @{"/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/afduseridentity" = @{}}

```

The output looks similar to the following:

```

Starting the parameter validation process.

The parameters have been successfully validated.

Your new Front Door profile is being created. Please wait until the process has finished completely. This may take several minutes.

Your new Front Door profile with the configuration has been successfully created.

```

#### [Multiple WAF and managed identity](#tab/multiple-waf-managed-identity)

This example shows how to migrate a Front Door profile with multiple WAF policies and enable both system assigned and user assigned identity.

1. Run the [Get-AzFrontDoorWafPolicy](/powershell/module/az.frontdoor/get-azfrontdoorwafpolicy) command to get the resource ID for your WAF policy. Replace the values for the resource group name and WAF policy name with your own values.

```powershell-interactive

Get-AzFrontDoorWafPolicy -ResourceGroupName myAFDResourceGroup -Name myClassicFrontDoorWAF

```

The output looks similar to the following:

```

PolicyMode                    : Detection

PolicyEnabledState            : Enabled

RedirectUrl                   :

CustomBlockResponseStatusCode : 403

CustomBlockResponseBody       :

RequestBodyCheck              : Disabled

CustomRules                   : {}

ManagedRules                  : {Microsoft.Azure.Commands.FrontDoor.Models.PSAzureManagedRule}

Etag                          :

ProvisioningState             : Succeeded

Sku                           : Classic_AzureFrontDoor

Tags                          :

Id                            : /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourcegroups/myAFDResourceGroup/providers/Microsoft.Network/frontdoorwebapplicationfirewallpolicies/myClassicFrontDoorWAF

Name                          : myFrontDoorWAF

Type                          :

```

1. Run the [New-AzFrontDoorCdnMigrationWebApplicationFirewallMappingObject](/powershell/module/az.cdn/new-azfrontdoorcdnmigrationwebapplicationfirewallmappingobject) command to create an in-memory object for WAF policy migration. Use the WAF ID in the last step for `MigratedFromId`. To use an existing WAF policy, replace the value for `MigratedToId` with a resource ID of a WAF policy that matches the Front Door tier you're migrating to. If you're creating a new WAF policy copy, you can change the name of the WAF policy in the resource ID.

```powershell-interactive

$wafMapping1 = New-AzFrontDoorCdnMigrationWebApplicationFirewallMappingObject -MigratedFromId /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourcegroups/myAFDResourceGroup/providers/Microsoft.Network/frontdoorwebapplicationfirewallpolicies/myClassicFrontDoorWAF1 -MigratedToId  /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourcegroups/myAFDResourceGroup/providers/Microsoft.Network/frontdoorwebapplicationfirewallpolicies/myFrontDoorWAF1

$wafMapping2 = New-AzFrontDoorCdnMigrationWebApplicationFirewallMappingObject -MigratedFromId /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourcegroups/myAFDResourceGroup/providers/Microsoft.Network/frontdoorwebapplicationfirewallpolicies/myClassicFrontDoorWAF2 -MigratedToId  /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourcegroups/myAFDResourceGroup/providers/Microsoft.Network/frontdoorwebapplicationfirewallpolicies/myFrontDoorWAF2

```

1. Specify both managed identity types in a variable.

```powershell-interactive

$identityType = "SystemAssigned, UserAssigned"

```

1. Run the [Get-AzUserAssignedIdentity](/powershell/module/az.managedserviceidentity/get-azuserassignedidentity) command to the get the resource ID for a user assigned identity.

```powershell-interactive

$id1 = Get-AzUserAssignedIdentity -ResourceGroupName myResourceGroup -Name afduseridentity1

$id1.Id

$id2 = Get-AzUserAssignedIdentity -ResourceGroupName myResourceGroup -Name afduseridentity2

$id2.Id

```

The output looks similar to the following:

```

/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourcegroups/myAFDResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/afduseridentity1

/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourcegroups/myAFDResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/afduseridentity2

```

1.  Specify the user assigned identity resource ID in a variable.

```powershell-interactive

$userInfo = @{

"subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/afduseridentity1" = @{}}

"subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/afduseridentity2" = @{}}

}

```

1. Run the [Start-AzFrontDoorCdnProfilePrepareMigration](/powershell/module/az.cdn/start-azfrontdoorcdnprofilepreparemigration) command to prepare for migration. Replace the values for the resource group name, resource ID, profile name with your own values. For *SkuName* use either **Standard_AzureFrontDoor** or **Premium_AzureFrontDoor**. The *SkuName* is based on the output from the [Test-AzFrontDoorCdnProfileMigration](/powershell/module/az.cdn/test-azfrontdoorcdnprofilemigration) command. The *MigrationWebApplicationFirewallMapping* parameter takes an array of WAF policy migration objects. The *IdentityType* parameter takes a comma separated list of identity types. The *IdentityUserAssignedIdentity* parameter takes a hash table of user assigned identity resource IDs.

Replace the following values in the command:

* `<subscriptionId>`: Your subscription ID.

* `<resourceGroupName>`: The resource group name of the Front Door (classic).

* `<frontdoorClassicName>`: The name of the Front Door (classic) profile.

```powershell-interactive

Start-AzFrontDoorCdnProfilePrepareMigration -ResourceGroupName <resourceGroupName> -ClassicResourceReferenceId /subscriptions/<subscriptionId>/resourcegroups/<resourceGroupName>/providers/Microsoft.Network/frontdoors/<frontdoorClassicName> -ProfileName myAzureFrontDoor -SkuName Premium_AzureFrontDoor -MigrationWebApplicationFirewallMapping @($wafMapping1, $wafMapping2) -IdentityType $identityType -IdentityUserAssignedIdentity $userInfo

```

The output looks similar to the following:

```

Starting the parameter validation process.

The parameters have been successfully validated.

Your new Front Door profile is being created. Please wait until the process has finished completely. This may take several minutes.

Your new Front Door profile with the configuration has been successfully created.

```

---

## Migrate

#### [Migrate profile](#tab/migrate-profile)

Run the [Enable-AzFrontDoorCdnProfileMigration](/powershell/module/az.cdn/enable-azfrontdoorcdnprofilemigration) command to migrate your Front Door (classic).

```powershell-interactive

Enable-AzFrontDoorCdnProfileMigration -ProfileName myAzureFrontDoor -ResourceGroupName myAFDResourceGroup

```

The output looks similar to the following:

```

Start to migrate.

This process will disable your Front Door (classic) profile and move all your traffic and configurations to the new Front Door profile.

Migrate succeeded.

```

#### [Abort migration](#tab/abort-migration)

Run the [Stop-AzFrontDoorCdnProfileMigration](/powershell/module/az.cdn/stop-azfrontdoorcdnprofilemigration) command to abort the migration process.

```powershell-interactive

Stop-AzFrontDoorCdnProfileMigration -ProfileName myAzureFrontDoor -ResourceGroupName myAFDResourceGroup

```

The output looks similar to the following:

```

Start to abort the migration.

Your new Front Door Profile will be deleted and your existing profile will remain active. WAF policies will not be deleted.

Please wait until the process has finished completely. This may take several minutes.

Abort succeeded.

```

---

## Update DNS records

Your old Azure Front Door (classic) instance uses a different fully qualified domain name (FQDN) than Azure Front Door Standard and Premium. For example, an Azure Front Door (classic) endpoint might be `contoso.azurefd.net`, while the Azure Front Door Standard or Premium endpoint might be `contoso-mdjf2jfgjf82mnzx.z01.azurefd.net`. For more information about Azure Front Door Standard and Premium endpoints, see [Endpoints in Azure Front Door](endpoint.md).

You don't need to update your DNS records before or during the migration process. Azure Front Door automatically sends traffic that it receives on the Azure Front Door (classic) endpoint to your Azure Front Door Standard or Premium profile without you making any configuration changes.

However, once your migration is finished, we strongly recommend that you update your DNS records to direct traffic to the new Azure Front Door Standard or Premium endpoint. Changing your DNS records helps to ensure that your profile continues to work in the future. The change in DNS record doesn't cause any downtime. You don't need to plan ahead for this update to happen, and can schedule it at your convenience.

## Next steps

* Understand the [mapping between Front Door tiers](tier-mapping.md) settings.

* Learn more about the [Azure Front Door tier migration process](tier-migration.md).


# Migration Faq

# Azure Front Door (classic) and CDN Standard from Microsoft (classic) Migration FAQ

This article provides answers to frequently asked questions about the migration from Azure Front Door (classic) and CDN Standard from Microsoft (classic) to Front Door Standard or Premium.

## Does the migration involve any downtime?

No, there's no downtime during the migration. The process is a control plane-only migration, meaning traffic delivery is unaffected.

During migration, the Azure Front Door (classic) endpoint `mydomain.azurefd.net` is created as a dummy custom domain on Front Door standard/premium. Both classic endpoint and standard/premium endpoints point to the same Front Door IP so the final resolution remains the same before and after DNS propagation. It continues to receive traffic until you update the DNS record of the Front Door custom domain `www.mydomain.com` to `mydomain.randomstring.z01.azurefd.net` directly. We recommend changing the CNAME from classic endpoint to Front Door standard/premium endpoint after verification.

Even in rare cases where the migration fails, traffic delivery continues to work as expected.

There's no rollback support. If migration fails, reach out to the support team for help.

## What should I do after migration?

After migration, follow these steps:

1. Verify traffic delivery continues to work.

1. Update the DNS CNAME record for your custom domain to point to the Front Door Standard/Premium endpoint `exampledomain-hash.z01.azurefd.net` instead of the classic endpoint (`exampledomain.azurefd.net` for Front Door (classic) or `exampledomain.azureedge.net`). Wait for the DNS update propagation until DNS TTL expires, depending on how long TTL is configured on DNS provider.

1. Verify again that traffic works in the custom domain.

1. Once confirmed, delete the pseudo custom domain (that is, the classic endpoint that was pointing to the Front Door Standard/Premium endpoint) from the Front Door Standard/Premium profile.

1. Then delete the classic resource.

## When I change my DNS CNAME from Front Door (classic) endpoint to Front Door Standard/Premium endpoint, does DNS propagation cause downtime?

No, both classic endpoint and Standard/Premium endpoints point to the same IP, so the final resolution remains the same before and after DNS propagation.

## When should I delete the classic tier?

For Front Door (classic): After verifying that traffic works and the DNS record was updated to point to the Front Door Standard/Premium endpoint, you can safely delete the classic resource.

For CDN Standard from Microsoft (classic): You don't need to delete the classic resource. Migration is treated as a tier upgrade, and the classic resource can remain.

## Do I need to update my DevOps pipeline?

Yes. After migration, make sure to update your DevOps pipeline to reflect the new Front Door Standard or Premium configuration and endpoints. [Learn more](post-migration-dev-ops-experience.md).

## Related content

- Understand the [settings mapping between Azure Front Door tiers](tier-mapping.md).

- Learn how to [migrate from Azure Front Door (classic) to Standard or Premium tier](migrate-tier.md) using the Azure portal.

- Learn how to [migrate from Azure Front Door (classic) to Standard or Premium tier](migrate-tier-powershell.md) using Azure PowerShell.

- Learn how to [migrate from Azure CDN from Microsoft (classic)](migrate-tier.md) to Azure Front Door using the Azure portal.


# Post Migration Dev Ops Experience

# Post Migration Dev-Ops Experience

After migrating from Azure Front Door (Classic) or CDN Classic to Azure Front Door Standard/Premium, update your DevOps pipeline scripts to deploy and manage the new Front Door Standard/Premium resources. Use the guidance below for various tools and pipeline types.

## Terraform

### Prerequisites

- Ensure the Terraform CLI is installed. See [Install Terraform](https://developer.hashicorp.com/terraform/tutorials/azure-get-started/install-cli).

- Install the Azure Resource Manager Export extension for Terraform to export existing Azure resources to Terraform templates. See [Overview of Azure Export for Terraform](/azure/developer/terraform/azure-export-for-terraform/export-terraform-overview).

### Steps

After migration, all classic AFD resources are migrated to AFD Standard and Premium. Then:

- **Export the new AFD Standard/Premium configuration**: Use Azure’s export tool to generate Terraform configurations for your new Front Door Standard/Premium resources. Follow [Quickstart: Export your first resources using Azure Export for Terraform](/azure/developer/terraform/azure-export-for-terraform/export-first-resources?tabs=azure-cli) to export the Front Door Standard/Premium resources into Terraform files.

- **Update Terraform templates in your pipeline**: Replace references to Front Door Classic resources with the exported Standard/Premium configuration.

- For AFD Classic, the Terraform resource is [`azurerm_frontdoor`](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/frontdoor).

- For CDN Classic, use the [`azurerm_cdn_*`](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/cdn_endpoint) resources.

- For AFD Standard/Premium (AFDx), use the [`azurerm_cdn_frontdoor_*`](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/cdn_frontdoor_profile) resources.

- Check in the updated Terraform code to your pipeline and run plan/apply to start managing the new Front Door via Terraform.

## ARM template

### Steps

After migration, all classic AFD resources are migrated to AFD Standard and Premium.

- **Export ARM templates for Front Door Standard/Premium** using any of the following:

- **Azure portal**: [Export template in Azure portal](../azure-resource-manager/templates/export-template-portal.md).

- **Azure CLI**: [Export template in Azure CLI](../azure-resource-manager/templates/export-template-cli.md).

- **Azure PowerShell**: [Export template in Azure PowerShell](../azure-resource-manager/templates/export-template-powershell.md).

- **Update ARM templates in your pipeline** to use the new Front Door Standard/Premium template instead of the Front Door (Classic) template. In Azure DevOps or GitHub Actions, update the template path and parameters in your deployment step, then deploy the new template.

- **Validate**: Remove or archive references to the classic Front Door template to avoid confusion.

## Bicep

### Prerequisites

- Install the Bicep CLI and tools. See [Set up Bicep development and deployment environments](../azure-resource-manager/bicep/install.md).

### Steps

After migration, all classic AFD resources are migrated to AFD Standard and Premium.

- **Generate a Bicep template for Front Door Standard/Premium** by decompiling an exported ARM template. See [Decompile ARM template JSON to Bicep](../azure-resource-manager/bicep/decompile.md?tabs=azure-cli).

- **Update Bicep files in your pipeline**: Replace Front Door Classic definitions with Standard/Premium. This may include updating resource types such as [`Microsoft.Cdn/profiles`](/azure/templates/microsoft.cdn/profiles?pivots=deployment-language-bicep) and child resources (endpoints, routes, etc.).

- **Test** a deployment (for example, `az deployment group create`) to verify provisioning of AFD Standard/Premium.

## PowerShell

### Prerequisites

Make sure you have the latest Azure PowerShell Az modules installed (Az.Cdn module version that supports AFD Standard/Premium). See [Install Azure PowerShell](/powershell/azure/install-azps-windows).

### Steps

- **Update PowerShell deployment scripts**: Replace any Front Door (Classic) cmdlets with AFD Standard/Premium cmdlets. For examples, see the [Azure Front Door PowerShell quickstart](create-front-door-powershell.md).

- **Incorporate new configuration and remove old references**: Ensure scripts configure required components (origins, origin groups, routes, rules, etc.). Remove or comment commands that manage Classic Front Door.

- Command group mapping:

- AzFrontDoorCdn commands under the [Az.Cdn module](/powershell/module/az.cdn/) are for AFD Standard/Premium.

- AzCdn commands under the [Az.Cdn module](/powershell/module/az.cdn/) are for CDN Classic.

- The [Az.FrontDoor module](/powershell/module/az.frontdoor/) is for AFD Classic.

- **Test** your script (locally or in a test pipeline) to verify creation or updates to AFD Standard/Premium, then commit changes to your pipeline.

## CLI

### Prerequisites

- Ensure Azure CLI is installed and updated to a version that supports the `afd` command group (for example, 2.63.0 or later). See [Install Azure CLI](/cli/azure/install-azure-cli).

- Log in (`az login`) and set the correct subscription context.

### Steps

- **Update CLI commands in scripts**: Use the Azure Front Door Standard/Premium command group: [`az afd`](/cli/azure/afd).

- **Replace or remove Front Door Classic CLI usage**:

- CDN Classic commands: [`az cdn`](/cli/azure/cdn)

- AFD Classic commands: [`az network front-door`](/cli/azure/network/front-door)

- **Validate** the updated CLI script manually or in a staging pipeline to ensure successful configuration of Front Door Standard/Premium.

## Next step

* For more questions, refer to the [AFD and CDN Classic Migration FAQ](migration-faq.md).

* Understand the [settings mapping between Azure Front Door tiers](tier-mapping.md).


# Tier Upgrade

# Upgrade from Azure Front Door Standard to Premium

**Applies to:** :heavy_check_mark: Front Door Standard

Upgrade your Azure Front Door Standard to Premium for advanced capabilities and increased quota limits without any downtime. For a detailed comparison, see [Tier comparison](standard-premium/tier-comparison.md).

This guide explains how to upgrade your Azure Front Door Standard profile. After upgrading, you'll be billed for the Azure Front Door Premium monthly base fee at an hourly rate.

> [!IMPORTANT]

> Downgrading from **Premium** to **Standard** isn't supported.

## Prerequisite

Ensure you have an Azure Front Door Standard profile in your subscription.

## Upgrade tier

1. Navigate to the Azure Front Door Standard profile you want to upgrade and select **Configuration** under *Settings*.

2. Select **Upgrade** to start the upgrade process. If no WAF policies are associated with your profile, confirm to proceed.

3. If WAF policies are associated, you're directed to the *Upgrade WAF policies* page. Choose to copy the WAF policies or use an existing premium WAF policy. You can rename the new WAF policy copy.

> [!NOTE]

> Enable managed WAF rules manually for the new premium WAF policy copies after upgrading.

4. Select **Upgrade** after setting up WAF policies. Confirm by selecting **Yes**.

5. The upgrade process creates a new premium WAF policy and associates it with the Azure Front Door Premium profile. The process can take a few minutes.

6. Once the upgrade is complete, **Tier: Premium** is displayed on the *Configuration* page.

> [!NOTE]

> Billing for Azure Front Door Premium is at an hourly rate.

## Next steps

* Learn more about [Managed rule for Azure Front Door WAF policy](../web-application-firewall/afds/waf-front-door-drs.md).

* Enable [Private Link to origin resources in Azure Front Door](private-link.md).


# Tier Upgrade Powershell

# Upgrade from Azure Front Door Standard to Premium with Azure PowerShell

**Applies to:** :heavy_check_mark: Front Door Standard

Azure Front Door allows upgrading from Standard to Premium for enhanced capabilities and increased quota limits. This upgrade doesn't cause any downtime to your services or applications. For more information on the differences between Standard and Premium, see [Tier comparison](standard-premium/tier-comparison.md).

This guide explains how to upgrade an Azure Front Door Standard profile to Premium. After the upgrade, you'll be charged the Azure Front Door Premium monthly base fee at an hourly rate.

> [!IMPORTANT]

> Downgrading from **Premium** to **Standard** is not supported.

## Prerequisites

* Ensure you have an Azure Front Door Standard profile in your subscription.

* Install the latest Azure PowerShell module locally or use Azure Cloud Shell. For more information, see [Install and configure Azure PowerShell](/powershell/azure/install-azure-powershell).

## Upgrade Tier

Run the [Update-AzFrontDoorCdnProfile](/powershell/module/az.cdn/update-azfrontdoorcdnprofile) command to upgrade your Azure Front Door Standard profile to Premium. The following example upgrades a profile named **myAzureFrontDoor** in the resource group **myAFDResourceGroup**.

### No WAF Policies Associated

```powershell-interactive

Update-AzFrontDoorCdnProfile -ProfileName myAzureFrontDoor -ResourceGroupName myAFDResourceGroup -ProfileUpgradeParameter @{}

```

Example output:

```

Location Name              Kind      ResourceGroupName

-------- ----              ----      -----------------

Global   myAzureFrontDoor  frontdoor myAFDResourceGroup

```

### WAF Policies Associated

1. Run the [New-AzFrontDoorCdnProfileChangeSkuWafMappingObject](/powershell/module/az.cdn/new-azfrontdoorcdnprofilechangeskuwafmappingobject) command to create a WAF policy mapping object. This maps the standard WAF policy to the premium WAF policy resource ID. Replace the `WafPolicyId` value with the resource ID of the premium WAF policy. If creating a new one, replace `premiumWAFPolicyName` with the name of the new premium WAF policy. This example creates two premium WAF policies named **myPremiumWAFPolicy1** and **myPremiumWAFPolicy2**.

```powershell-interactive

# Replace the following values:

# <subscriptionId>: Your subscription ID.

# <resourceGroupName>: The resource group name of the WAF policy.

# <standardWAFPolicyName>: The name of the standard WAF policy.

$waf1 = New-AzFrontDoorCdnProfileChangeSkuWafMappingObject SecurityPolicyName <standardWAFPolicyName> -WafPolicyId /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/frontDoorWebApplicationFirewallPolicies/myPremiumWAFPolicy1

$waf2 = New-AzFrontDoorCdnProfileChangeSkuWafMappingObject SecurityPolicyName <standardWAFPolicyName> -WafPolicyId /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/frontDoorWebApplicationFirewallPolicies/myPremiumWAFPolicy2

```

2. Run the [New-AzFrontDoorCdnProfileUpgradeParametersObject](/powershell/module/az.cdn/new-azfrontdoorcdnprofileupgradeparametersobject) command to create an upgrade parameters object.

```powershell-interactive

$upgradeParams = New-AzFrontDoorCdnProfileUpgradeParametersObject -WafPolicyMapping @{$waf1, $waf2}

```

3. Run the [Update-AzFrontDoorCdnProfile](/powershell/module/az.cdn/update-azfrontdoorcdnprofile) command to upgrade your Azure Front Door Standard profile to Premium. The following example upgrades a profile named **myAzureFrontDoor** in the resource group **myAFDResourceGroup**.

```powershell-interactive

Update-AzFrontDoorCdnProfile -ProfileName myAzureFrontDoor -ResourceGroupName myAFDResourceGroup -ProfileUpgradeParameter $upgradeParams

```

Example output:

```

Location Name              Kind      ResourceGroupName

-------- ----              ----      -----------------

Global   myAzureFrontDoor  frontdoor myAFDResourceGroup

```

> [!NOTE]

> You will now be billed for Azure Front Door Premium at an hourly rate.

## Next Steps

* Learn more about [Managed rule for Azure Front Door WAF policy](../web-application-firewall/afds/waf-front-door-drs.md).

* Learn how to enable [Private Link to origin resources in Azure Front Door](private-link.md).


# Classic Retirement Faq

# Azure Front Door (classic) retirement FAQ

**Applies to:** :heavy_check_mark: Front Door (classic)

Azure Front Door introduced two new tiers named Standard and Premium on March 29, 2022. These tiers offer improvements over the current product offerings of Azure Front Door (Classic), incorporating capabilities such as Azure Private Link integration, Bot management, advanced Web Application Firewall (WAF) enhancements with DRS 2.1, anomaly scoring-based detection and bot management, out-of-the-box reports and enhanced diagnostic logs, a simplified pricing model, and much more.

In our ongoing efforts to provide the best product experience and streamline our portfolio of products and tiers, we're announcing the retirement of the Azure Front Door (Classic) tier. This retirement affects the public cloud and the Azure Government regions of Arizona and Texas, effective March 31, 2027. We'll communicate retirement plan of Azure Front Door classic in Azure Government regions US DoD Central and US DoD East in a future announcement. To avoid service disruption, transition to Azure Front Door Standard or Premium.

> [!IMPORTANT]

> - Azure Front Door (classic) doesn't support profile creation, new domain onboarding, or managed certificates and retires on **March 31, 2027**. To avoid service disruption, ⁠[**migrate to Azure Front Door Standard or Premium**](/azure/frontdoor/tier-migration). For more information, see ⁠[Azure Front Door (classic) retirement](https://azure.microsoft.com/updates?id=azure-front-door-classic-will-be-retired-on-31-march-2027).

> - If you migrate to Azure Front Door Standard or Premium after your managed certificates already expired, then after migration, the certificates change to *Pending Revalidation* state or start to rotate after 1-2 days. Alternatively, rotate the Front Door Standard and Premium managed certificates by refreshing the validation token using either **[Powershell](/powershell/module/az.cdn/update-azfrontdoorcdncustomdomainvalidationtoken)** or **[CLI](/cli/azure/afd/custom-domain#az-afd-custom-domain-regenerate-validation-token)**. After adding the new TXT record token to your DNS zone, the custom domain is revalidated and a new certificate is deployed.

## Frequently asked questions

### When is the retirement for Azure Front Door (classic)?

Azure Front Door (classic) retires on March 31, 2027.

### Why is Azure Front Door (classic) being retired?

Azure Front Door (classic) is a legacy service that provides dynamic site acceleration and global load balancing capabilities. In March 2022, Microsoft announced the general availability of Azure Front Door Standard and Premium. These new tiers serve as a modern Content Delivery Network platform that supports both dynamic and static scenarios with enhanced Web Application Firewall capabilities, Private Link integration, simplified pricing model, and many more enhancements. As part of Microsoft's plans to offer the best product experience and simplify the product portfolio, Microsoft is retiring the Azure Front Door (classic) tier.

### What advantages does migrating to Azure Front Door Standard or Premium tier offer?

Azure Front Door Standard and Premium tiers are enhanced versions of Azure Front Door (classic). They maintain the same service level agreement (SLA) and offer more benefits, including:

* A unified static and dynamic delivery platform, with a simplified cost model.

* Enhanced security features, such as [Private Link integration](private-link.md), advanced WAF enhancements with DRS 2.1, anomaly scoring based detection and bot management, and many more to come.

* Deep integration with Azure services to deliver secure, accelerated, and user friendly end-to-end cloud solutions. These integrations include:

* DNS deterministic name library integrations to prevent subdomain take over

* [Prevalidated domain integration with PaaS service with  one-time domain validation](./standard-premium/how-to-add-custom-domain.md#associate-the-custom-domain-with-your-azure-front-door-endpoint).

* [One-click enablement on Static Web Apps](../static-web-apps/front-door-manual.md)

* Use [managed identities](managed-identity.md) to access Azure Key Vault certificates

* Azure Advisor integration to provide best practice recommendations

* Improved capabilities such as simplified, more flexible [rules engine](front-door-rules-engine.md) with regular expressions and server variables, enhanced and richer [analytics](./standard-premium/how-to-reports.md) and [logging](front-door-diagnostics.md) capabilities, and more.

* The ability to update separate resources without updating the whole Azure Front Door instance through DevOps tools.

* Access to all future features and updates on Azure Front Door Standard and Premium tier.

For more information about supported features, see [comparison between Azure Front Door and Azure CDN services](front-door-cdn-comparison.md).

### How does the performance of the Azure Front Door Standard or Premium tier compare to that of Azure Front Door (classic)?

Azure Front Door Standard and Premium tiers have the same service level agreement (SLA). Microsoft aims to ensure Azure Front Door Standard and Premium delivers optimal performance and reliability.

### What happens after March 31, 2027 when the service is retired?

After the service is retired, you lose the ability to:

* Create or manage Azure Front Door (classic) resources.

* Access the data through the Azure portal or the APIs/SDKs/client tools.

* Receive service updates to Azure Front Door (classic) or APIs/SDKs/Client tools.

* Receive support for issues on Azure Front Door (classic) through phone, email, or web.

### How can I complete the migration without causing downtime to my applications? Where can I learn more about the migration to Azure Front Door Standard or Premium?

Microsoft provides a zero-downtime migration tool. To help you understand and perform the migration process, the following resources are available:

* Familiarize yourself with the [zero-downtime migration tool](tier-migration.md). Pay attention to the section **Breaking changes when migrating to Standard or Premium tier**.

* Understand the [settings mapping](tier-mapping.md) between the different Azure Front Door tiers.

* Learn the process of migrating from Azure Front Door (classic) to Standard or Premium tier using the [Azure portal](migrate-tier.md) or [Azure PowerShell](migrate-tier-powershell.md).

### How does migrating to Azure Front Door Standard or Premium affect the total cost of ownership (TCO)?

For more information, see the [pricing comparison](understanding-pricing.md) between Azure Front Door tiers.

### Which clouds does Azure Front Door (classic) retirement apply to?

Currently, Azure Front Door (classic) retirement affects the public cloud and Azure Government in the regions of Arizona and Texas.

### Can I make updates to Azure Front Door (classic) resources?

You can still update your existing Azure Front Door (classic) resources by using the Azure portal, Terraform, and all command line tools until March 31, 2027. However, you can't create new Azure Front Door (classic) resources starting April 1, 2025. Starting August 15, 2025, Azure Front Door (classic) no longer supports managed certificates. Migrate to Azure Front Door Standard or Premium tier as soon as possible.

### Can I roll back to Azure Front Door (classic) after migration?

No, once migration is completed successfully, you can't roll back to classic. If you encounter any issues, raise a support ticket for assistance.

### How are Azure Front Door (classic) resources handled after migration?

Delete the Azure Front Door (classic) resource once migration successfully completes. Azure Front Door sends notification through Azure Advisor to remind users to delete the migrated classic resources.

### What resources are available for support and feedback?

If you have a support plan and need technical assistance, create a [support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest) with the following information:

* *Issue type*, select **Technical**.

* *Subscription*, select the subscription you need assistance with.

* *Service*, select **My services**, and then select **Front Door Service**.

* *Resource*, select the **Azure Front Door resource**.

* *Summary*, describe the problem you're experiencing with the migration.

* *Problem type*, select **Migrating Front Door Classic to Front Door Standard or Premium**.

## Next step

> [!div class="nextstepaction"]

> [Migrate Azure Front Door (classic) to Standard or Premium tier](migrate-tier.md)


# Diffie Hellman Ciphers

# TLS_DHE cipher suites on Azure Front Door and Azure CDN

**Applies to:** :heavy_check_mark: Front Door Standard/Premium :heavy_check_mark: Front Door (classic) :heavy_check_mark: CDN Standard from Microsoft (classic)

On April 1, 2026, Azure Front Door (Standard, Premium, and classic) and Azure CDN from Microsoft (classic) services will stop negotiating the following weak DHE cipher suites for both client to service and service to origin TLS connections:

* TLS_DHE_RSA_WITH_AES_256_GCM_SHA384

* TLS_DHE_RSA_WITH_AES_128_GCM_SHA256

## Who is affected?

You're affected if any of the following are true:

* Your clients (browsers/agents/devices) must require one of the DHE cipher suites when connecting to your Front Door/CDN endpoint.

* Your origins must require one of the retired DHE cipher suites when Front Door/ CDN connects to your origin.

## How will I know if I'm impacted?

* Impacted subscriptions and resources will receive Azure service health notification and email notifications.

* The impacted connection leg ('client to service' or 'service to origin' or both) will be mentioned in the notification.

## What is the impact if I don't act?

* Connections that can only use the retired DHE ciphers will fail the TLS handshake (for clients) or fail on service to origin negotiation (for origins).

* Typical symptoms include handshake failure / no shared cipher errors / invalid cipher error in clients or origin server logs.

## Action required

1.	Ensure your origin servers disable DHE ciphers and enable the recommended cipher suites.

3.	Inform your clients to disable DHE ciphers and enable the recommended cipher suites.

## Recommended cipher suites

For best compatibility and security on Azure Front Door / Azure CDN endpoints and origins, we recommend using the following cipher suites:

* TLS_AES_256_GCM_SHA384 (TLS 1.3 only)

* TLS_AES_128_GCM_SHA256 (TLS 1.3 only)

* TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384

* TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256

* TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384

* TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256

## Updating cipher suites for common origin types

| Service |	Configuration Method |

| -- | -- |

| Azure App Service | 	[Use TLS/SSL settings to set a "Minimum TLS Version" or use ARM templates for fine-grained cipher control.](../app-service/configure-ssl-bindings.md) |

| Azure Application Gateway | 	[Create a SSL Policy (Predefined or Custom) to select specific cipher suites.](../application-gateway/application-gateway-ssl-policy-overview.md) |

| Azure API Management | 	[Modify the Service Instance Settings to disable specific ciphers via the "Protocols and Ciphers" blade.](../api-management/api-management-howto-manage-protocols-ciphers.md)	|

## Frequently asked questions

- Does this affect both client and origin connections?

Yes. The retirement applies to both the client to service and service to origin legs. Update both sides to avoid issues.

- What if I still need legacy client compatibility?

The chances of a modern client or server requiring TLS_DHE ciphers as a "must-have" are extremely low as in most places these ciphers have been replaced with the more secure TLS_ECDHE ciphers. Inform your legacy clients to support TLS 1.2/1.3 with ECDHE. If you operate controlled clients, update their TLS policy.

- Should I make any changes to my Front Door or CDN profiles?

As an optional measure, for Front Door Standard/Premium profiles, you can also use the [Configure Azure Front Door TLS policy](/azure/frontdoor/standard-premium/tls-policy) feature to disable the DHE ciphers in advance before 1 April 2026. This option isn't available for other tiers.

For all Front Door (Standard, Premium, classic) and Azure CDN from Microsoft (classic) profiles, Microsoft team will disable the DHE ciphers after 1 April 2026.


# Secure Front Door

# Secure your Azure Front Door deployment

Azure Front Door is a modern cloud content delivery network (CDN) service that delivers high performance, scalability, and secure user experiences for your content and applications. As a global entry point for your applications, Azure Front Door handles massive amounts of traffic and serves as a critical security boundary, making it essential to implement robust security measures to protect against threats and ensure reliable service delivery.

This article provides guidance on how to best secure your Azure Front Door deployment.

## Network security

Network security for Azure Front Door focuses on establishing secure connections between your CDN service and backend origins while protecting against external threats. Since Front Door operates at the network edge and handles global traffic distribution, implementing proper network controls ensures that your applications remain protected and accessible only through authorized channels.

* **Secure backend connections with Private Link**: Use Azure Private Link to establish secure, private connections between Azure Front Door and your backend services. This prevents traffic from traversing the public internet and reduces exposure to network-based attacks. For more information, see [Secure your Origin with Private Link in Azure Front Door](/azure/frontdoor/private-link).

* **Protect against DDoS attacks with built-in protection**: Azure Front Door includes infrastructure DDoS protection that monitors and mitigates network layer attacks in real-time using the global scale of Azure's network. The service blocks unsupported protocols and requires valid Host headers to prevent common DDoS attack vectors. For more information, see [DDoS Protection on Azure Front Door](./front-door-ddos.md).

* **Configure Web Application Firewall for application-layer protection**: Deploy Azure Web Application Firewall (WAF) to protect your applications from common web vulnerabilities and exploits. WAF provides managed rule sets for OWASP Top 10 protection, bot management, and custom rules for specific threat patterns. For more information, see [Web Application Firewall (WAF) on Azure Front Door](./web-application-firewall.md).

* **Implement origin security controls**: Configure your origins to accept traffic only from Azure Front Door by using managed identities or IP filtering with the `AzureFrontDoor.Backend` service tag and validating the X-Azure-FDID header value. This prevents attackers from bypassing Front Door's security features. For more information, see [Secure traffic to Azure Front Door origins](./origin-security.md).

* **Use rate limiting to prevent abuse**: Configure WAF rate limiting rules to protect against high-volume attacks and prevent individual IP addresses from overwhelming your service. Rate limiting helps mitigate application-layer DDoS attacks and abusive traffic patterns. For more information, see [Rate limiting](/azure/web-application-firewall/afds/waf-front-door-rate-limit).

## Identity management

Identity management for Azure Front Door centers on using managed identities to securely access Azure resources without managing credentials. Proper identity management ensures that Front Door can authenticate to services like Azure Key Vault for certificate management while maintaining security boundaries.

* **Enable managed identities for secure authentication**: Use system-assigned or user-assigned managed identities to allow Azure Front Door to securely access Azure Key Vault and other Azure services without storing credentials. Managed identities provide automatic credential rotation and eliminate the risk of credential exposure. For more information, see [Use managed identities to access Azure Key Vault certificates](./managed-identity.md).

* **Configure origin authentication with managed identities**: Use managed identities to authenticate Azure Front Door to your origin services that support Microsoft Entra ID authentication. This provides a secure, credential-free way to establish trust between Front Door and your backend applications. For more information, see [Use managed identities to authenticate to origins (preview)](./origin-authentication-with-managed-identities.md).

## Data protection

Data protection in Azure Front Door ensures that sensitive information remains secure both in transit and when stored, while providing you with control over encryption keys and certificates. Protecting data as it flows through your CDN infrastructure is critical for maintaining customer trust and meeting compliance requirements.

* **Leverage automatic encryption in transit**: Azure Front Door automatically encrypts all data in transit using TLS, protecting communications between clients and your service without requiring additional configuration. This ensures that sensitive data remains protected as it travels across the network. For more information, see [End-to-end TLS with Azure Front Door](./end-to-end-tls.md).

* **Configure strong TLS policies**: Set minimum TLS versions and cipher suites to meet your security requirements. Use predefined security policies or create custom TLS policies to control which encryption standards are acceptable for your applications. For more information, see [Configure TLS policy on a Front Door custom domain](./standard-premium/tls-policy-configure.md).

* **Manage encryption keys with Azure Key Vault**: Store and manage your encryption keys in Azure Key Vault to maintain control over the key lifecycle, including generation, rotation, and revocation. Use key hierarchies with separate data encryption keys (DEK) and key encryption keys (KEK) for enhanced security. For more information, see [Secure your Origin with Private Link in Azure Front Door](/azure/frontdoor/private-link).

* **Manage SSL/TLS certificates with Azure Key Vault**: Use Azure Key Vault to securely store, manage, and automatically rotate SSL/TLS certificates for your Azure Front Door endpoints. Configure automatic certificate renewal to prevent service disruptions and ensure continuous protection. For more information, see [Create a Front Door for your application with certificates in Azure Key Vault](/azure/frontdoor/create-front-door-portal).

## Logging and threat detection

Logging and threat detection for Azure Front Door provides visibility into traffic patterns, security events, and potential threats targeting your applications. Comprehensive logging enables you to detect suspicious activities, investigate security incidents, and maintain compliance with audit requirements.

* **Enable comprehensive resource logging**: Configure Azure Front Door resource logs to capture detailed information about Web Application Firewall events, access patterns, and security incidents. Send these logs to Azure Monitor Log Analytics or your preferred security information and event management (SIEM) solution for analysis and alerting. For more information, see [Resource logs](/azure/frontdoor/standard-premium/how-to-logs).

* **Monitor Web Application Firewall activity**: Enable and review WAF logs to track blocked requests, attack patterns, and potential security threats. Use these logs to fine-tune WAF rules and improve protection against emerging threats targeting your applications.

* **Configure security alerts and monitoring**: Set up Azure Monitor alerts to notify you of security events such as high numbers of blocked requests, unusual traffic patterns, or policy violations. Create custom queries to detect suspicious behavior and automate response actions.

## Asset management

Asset management for Azure Front Door involves implementing configuration monitoring and policy enforcement to ensure your CDN deployment remains compliant with security standards. Proper asset management helps maintain consistent security configurations across your infrastructure and provides visibility into potential security drift.

* **Monitor configurations with Azure Policy**: Use Azure Policy to continuously monitor and enforce security configurations across your Azure Front Door resources. Configure policies to audit compliance with your organization's security standards and automatically remediate configuration drift. For more information, see [Azure Front Door Policies](/azure/governance/policy/tutorials/create-and-manage).

* **Implement configuration alerts**: Set up Azure Monitor alerts to notify you when Azure Front Door configurations deviate from approved security baselines. Use policy effects like "deny" and "deploy if not exists" to automatically enforce secure configurations across your resources.

## Related content

- [Security baseline](/security/benchmark/azure/baselines/azure-front-door-security-baseline?toc=/azure/frontdoor/toc.json)

- [Azure Well-Architected Framework: Security pillar](/azure/well-architected/security/)

- [Cloud Adoption Framework: Secure overview](/azure/cloud-adoption-framework/secure/overview)


# Tls Policy

# Azure Front Door TLS policy

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Azure Front Door supports [end-to-end TLS encryption](../end-to-end-tls.md). When you add a custom domain to Azure Front Door, HTTPS is required, and you need to define a TLS policy which includes control of the TLS protocol version and the cipher suites during a TLS handshake.

Azure Front Door supports two versions of the TLS protocol: TLS versions 1.2 and 1.3. Currently, Azure Front Door doesn't support client/mutual authentication (mTLS).

Azure Front Door Standard and Premium offer two mechanisms for controlling TLS policy. You can use either a predefined policy or a custom policy per your own needs. If you use Azure Front Door (classic) and Microsoft CDN (classic), you'll continue to use the minimum TLS 1.2 version.

- Azure Front Door offers several predefined TLS policies. You can configure your AFD with any of these policies to get the appropriate level of security. These predefined policies are configured keeping in mind the best practices and recommendations from the Microsoft Security team. We recommend that you use the newest TLS policies to ensure the best TLS security.

- If a TLS policy needs to be configured for your own business and security requirements, you can use a Custom TLS policy. With a custom TLS policy, you have complete control over the minimum TLS protocol version to support, and the supported cipher suites.

For a minimum TLS version 1.2, the negotiation will attempt to establish TLS 1.3 and then TLS 1.2. The client must support at least one of the supported ciphers to establish an HTTPS connection with Azure Front Door. Azure Front Door chooses a cipher in the listed order from the client-supported ciphers.

When Azure Front Door initiates TLS traffic to the origin, it will attempt to negotiate the best TLS version that the origin can reliably and consistently accept. Supported TLS versions for origin connections are TLS 1.2, and TLS 1.3.

> [!NOTE]

> Clients with TLS 1.3 enabled are required to support one of the Microsoft SDL compliant EC Curves, including Secp384r1, Secp256r1, and Secp521, in order to successfully make requests with Azure Front Door using TLS 1.3. It's recommended that clients use one of these curves as their preferred curve during requests to avoid increased TLS handshake latency, which may result from multiple round trips to negotiate the supported EC curve.

## Predefined TLS policy

Azure Front Door offers several predefined TLS policies. You can configure your AFD with any of these policies to get the appropriate level of security. The policy names are annotated by the minimum TLS versions and the year in which they were configured (TLSv1.2_2023>). Each policy offers different TLS protocol versions and/or cipher suites. These predefined policies are configured keeping in mind the best practices and recommendations from the Microsoft Security team. We recommend that you use the newest TLS policies to ensure the best TLS security.

The following table shows the list of cipher suites and minimum protocol version support for each predefined policy. The ordering of the cipher suites determines the priority order during TLS negotiation.

By default, TLSv1.2_2023 will be selected. TLSv1.2_2022 maps to the minimum TLS 1.2 version in previous design.

| **OpenSSL** | **Cipher** **Suite** | **TLSv1.2_2023** | **TLSv1.2_2022** |

|---|---|---|---|

| **Minimum Protocol version** | | **1.2** | **1.2** |

| **Supported Protocols** | | **1.3/1.2** | **1.3./1.2** |

| **TLS_AES_256_GCM_SHA384** | TLS_AES_256_GCM_SHA384 | Yes | Yes |

| **TLS_AES_128_GCM_SHA256** | TLS_AES_128_GCM_SHA256 | Yes | Yes |

| **ECDHE-RSA-AES256-GCM-SHA384** | TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 | Yes | Yes |

| **ECDHE-RSA-AES128-GCM-SHA256** | TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 | Yes | Yes |

| **ECDHE-RSA-AES256-SHA384** | TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384 | | Yes |

| **ECDHE-RSA-AES128-SHA256** | TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256 | | Yes |

## Custom TLS policy

If a TLS policy needs to be configured for your requirements, you can use a Custom TLS policy. With a custom TLS policy, you have complete control over the minimum TLS protocol version to support, and the supported cipher suites and their priority order.

> [!NOTE]

> TLS 1.3 is always enabled no matter what minimum version is enabled.

### Cipher suites

Azure Front Door supports the following cipher suites from which you can choose your custom policy. The ordering of the cipher suites determines the priority order during TLS negotiation.

- TLS_AES_256_GCM_SHA384 (TLS 1.3 only)

- TLS_AES_128_GCM_SHA256 (TLS 1.3 only)

- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256

- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384

- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256

- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384

> [!NOTE]

> For Windows 10 and later versions, we recommend enabling one or both of the ECDHE_GCM cipher suites for better security. Windows 8.1, 8, and 7 aren't compatible with these ECDHE_GCM cipher suites. The ECDHE_CBC cipher suites have been provided for compatibility with those operating systems.

## Next step

> [!div class="nextstepaction"]

> [Configure TLS policy on Front Door](tls-policy-configure.md)


# Tls Policy Configure

# Configure TLS policy on a Front Door custom domain

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Azure Front Door Standard and Premium offer two mechanisms for controlling TLS policy. You can use either a predefined policy or a custom policy based on your own needs. If you use Azure Front Door (classic) or Microsoft CDN (classic), you continue to use the minimum TLS 1.2 version.

- Azure Front Door offers several predefined TLS policies. You can configure your Azure Front Door with any of these policies to get the appropriate level of security. The Microsoft Security team configures these predefined policies based on best practices and recommendations. Use the newest TLS policies to ensure the best TLS security.

- If you need to configure a TLS policy for your own business and security requirements, use a custom TLS policy. By using a custom TLS policy, you have complete control over the minimum TLS protocol version to support, and the supported cipher suites.

In this article, you learn how to configure TLS policy on a Front Door custom domain.

## Prerequisites

- A Front Door. For more information, see [Quickstart: Create a Front Door using the Azure portal](/azure/frontdoor/quickstart-create-front-door).

- A custom domain. If you don't have a custom domain, you must first purchase one from a domain provider. For more information, see [Buy a custom domain name](/azure/app-service/manage-custom-dns-buy-domain?toc=/azure/frontdoor/TOC.json).

- If you're using Azure to host your [DNS domains](/azure/dns/dns-overview), you must delegate the domain provider's domain name system (DNS) to an Azure DNS. For more information, see [Delegate a domain to Azure DNS](/azure/dns/dns-delegate-domain-azure-dns?toc=/azure/frontdoor/TOC.json). Otherwise, if you're using a domain provider to handle your DNS domain, see [Create a CNAME DNS record](/azure/frontdoor/front-door-custom-domain).

## Configure TLS policy

1. Go to your Azure Front Door profile that you want to configure the TLS policy for.

1. Under **Settings**, select **Domains**. Then select **+ Add** to add a new domain.

1. On **Add a domain**, follow the instructions in [Configure a custom domain on Azure Front Door](/azure/frontdoor/standard-premium/how-to-add-custom-domain) and [Configure HTTPS on an Azure Front Door custom domain](/azure/frontdoor/standard-premium/how-to-configure-https-custom-domain) to configure the domain.

1. For **TLS policy**, select the predefined policy from the dropdown list or **Custom** to customize the cipher suites per your needs.

Select **View policy details** to see the supported cipher suites.

When you select **Custom**, you can choose the minimum TLS version and the corresponding cipher suites by selecting **Select cipher suites**.

> [!NOTE]

> To reuse the custom TLS policy setting from other domains in the portal, select the domain in **Reuse setting from other domain**.

1. After you customize the TLS policy, select **Add** to add the domain.

## Verify TLS policy configurations

View the supported cipher suite of your domain by using [www.ssllabs.com/ssltest](https://www.ssllabs.com/ssltest/) or use the sslscan tool.

## Related content

- [Azure Front Door TLS Policy](tls-policy.md)

- [Add a custom domain on Azure Front Door](how-to-add-custom-domain.md)

- [Configure HTTPS for your custom domain on Azure Front Door](how-to-configure-https-custom-domain.md)


# Managed Identity

# Use managed identities to access Azure Key Vault certificates

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Managed identities provided by Microsoft Entra ID enable your Azure Front Door instance to securely access other Microsoft Entra protected resources, such as Azure Key Vault, without the need to manage credentials. For more information, see [What are managed identities for Azure resources?](../active-directory/managed-identities-azure-resources/overview.md)

After you enable managed identity for Azure Front Door and granting the necessary permissions to your Azure Key Vault, Front Door will use the managed identity to access certificates. Without these permissions, custom certificate autorotation and adding new certificates fail. If managed identity is disabled, Azure Front Door will revert to using the original configured Microsoft Entra App, which isn't recommended and will be deprecated in the future.

Azure Front Door supports two types of managed identities:

- **System-assigned identity**: This identity is tied to your service and is deleted if the service is deleted. Each service can have only one system-assigned identity.

- **User-assigned identity**: This identity is a standalone Azure resource that can be assigned to your service. Each service can have multiple user-assigned identities.

Managed identities are specific to the Microsoft Entra tenant where your Azure subscription is hosted. If a subscription is moved to a different directory, you need to recreate and reconfigure the identity.

You can configure Azure Key Vault access using either [role-based access control (RBAC)](#role-based-access-control-rbac) or [access policy](#access-policy).

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An Azure Front Door Standard or Premium profile. To create a new profile, see [create an Azure Front Door](create-front-door-portal.md).

## Enable managed identity

1. Go to your existing Azure Front Door profile. Select **Identity** under *Security* in the left menu.

1. Choose either a **System assigned** or **User assigned** managed identity.

- **[System assigned](#system-assigned)** - A managed identity tied to the Azure Front Door profile lifecycle, used to access Azure Key Vault.

- **[User assigned](#user-assigned)** - A standalone managed identity resource with its own lifecycle, used to authenticate to Azure Key Vault.

### System assigned

1. Toggle the *Status* to **On** and select **Save**.

1. Confirm the creation of a system managed identity for your Front Door profile by selecting **Yes** when prompted.

1. Once created and registered with Microsoft Entra ID, use the **Object (principal) ID** to grant Azure Front Door access to your Azure Key Vault.

### User assigned

To use a user-assigned managed identity, you must have one already created. For instructions on creating a new identity, see [create a user-assigned managed identity](../active-directory/managed-identities-azure-resources/how-manage-user-assigned-managed-identities.md).

1. In the **User assigned** tab, select **+ Add** to add a user-assigned managed identity.

1. Search for and select the user-assigned managed identity. Then select **Add** to attach it to the Azure Front Door profile.

1. The name of the selected user-assigned managed identity appears in the Azure Front Door profile.

## Configure Key Vault access

You can configure Azure Key Vault access using either of the following methods:

- **[Role-based access control (RBAC)](#role-based-access-control-rbac)** - Provides fine-grained access control using Azure Resource Manager.

- **[Access policy](#access-policy)** - Uses native Azure Key Vault access control.

For more information, see [Azure role-based access control (Azure RBAC) vs. access policy](/azure/key-vault/general/rbac-access-policy).

### Role-based access control (RBAC)

1. Go to your Azure Key Vault. Select **Access control (IAM)** from the *Settings* menu, then select **+ Add** and choose **Add role assignment**.

1. On the *Add role assignment* page, search for **Key Vault Secret User** and select it from the search results.

1. Go to the **Members** tab, select **Managed identity**, then select **+ Select members**.

1. Choose the *system-assigned* or *user-assigned* managed identity associated with your Azure Front Door, then select **Select**.

1. Select **Review + assign** to finalize the role assignment.

### Access policy

1. Go to your Azure Key Vault. Under *Settings*, select **Access policies** and then select **+ Create**.

1. On the *Create an access policy* page, go to the **Permissions** tab. Under *Secret permissions*, select **List** and **Get**. Then select **Next** to proceed to the principal tab.

1. On the *Principal* tab, enter the **object (principal) ID** for a system-assigned managed identity or the **name** for a user-assigned managed identity. Then select **Review + create**. The *Application* tab is skipped as Azure Front Door is automatically selected.

1. Review the access policy settings and select **Create** to finalize the access policy.

## Verify access

1. Go to the Azure Front Door profile where you enabled managed identity and select **Secrets** under **Security**.

1. Confirm that **Managed identity** appears under the *Access role* column for the certificate used in Front Door. If setting up managed identity for the first time, add a certificate to Front Door to see this column.

## Related content

- [End-to-end TLS encryption](end-to-end-tls.md)

- [Configure HTTPS on an Azure Front Door custom domain](standard-premium/how-to-configure-https-custom-domain.md)


# Sensitive Data Protection

# Azure Front Door sensitive data protection

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

The Azure Front Door log scrubbing tool helps you remove sensitive data (for example, personal identifiable information) from your Azure Front Door logs. It works by enabling log scrubbing at Azure Front Door Standard or Premium profile level and selecting the log fields to be scrubbed. Once enabled, the tool scrubs that information from your logs generated under this profile and replaces it with `****`.

Log scrubbing is only supported on Azure Front Door Standard and Premium. If you're using Azure Front Door classic, migrate to Azure Front Door standard or premium to use log scrubbing. For more information, see [About Azure Front Door (classic) to Standard/Premium tier migration](..\tier-migration.md).

## Default log behavior

When Azure Front Door serves a request, Azure Front Door logs the details of the request in clear text. Sensitive data might be included in the request URI (such as passwords), and client IP and socket IP are logged. This data is viewable by anyone with access to the Azure Front Door access logs. To protect customer data, you can set up log scrubbing rules targeting this sensitive data for protection.

## Scrubbing fields

The following fields can be scrubbed from the logs:

| Information | Description | Samples after enablement |

| --- | --- | --- |

| Request URI | RequestUri, OriginUrl | `****` |

| Request IP address | ClientIp, SocketIp | `****` |

| Query string | Querystring in RequestUri and OriginUrl  | `https://contoso.com/bar/temp.txt?20240423&q=****&foo=****` |

> [!NOTE]

> When you enable log scrubbing feature, Microsoft still retains IP addresses in its internal logs to support critical security features.

## Next step

> [!div class="nextstepaction"]

> [Protect sensitive data in Azure Front Door logs](how-to-protect-sensitive-data.md)


# How To Protect Sensitive Data

# Protect sensitive data in Azure Front Door logs

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

In this article, you learn how to use the log scrubbing tool to protect sensitive data in Azure Front Door logs. For more information about sensitive data protection in Azure Front Door, see [Azure Front Door sensitive data protection](sensitive-data-protection.md).

## Prerequisites

Before you can use the log scrubbing tool, you must have an Azure Front Door Standard or Premium tier profile. For more information, see [Create an Azure Front Door profile](../create-front-door-portal.md).

## Enable log scrubbing to protect sensitive data

1. Go to the Azure Front Door Standard or Premium profile.

1. Under **Settings**, select **Configuration**.

1. Under **Scrub sensitive data from access logs**, select **Manage log scrubbing**.

1. In **Manage log scrubbing**, select **Enable access log scrubbing** to enable scrubbing.

1. Select the log fields that you want to scrub, then select **Save**.

1. In the **Configuration** page, you can now see that log scrubbing became **Enabled**.

To verify your sensitive data protection rules, open the Azure Front Door log and search for `****` in place of the sensitive fields.

## Related content

- [Learn about Azure Front Door sensitive data protection](../create-front-door-portal.md).

- [Learn how to create an Azure Front Door profile](sensitive-data-protection.md).

- [Learn how to migrate Azure Front Door (classic) to Standard/Premium tier](../migrate-tier.md).


# Origin Security

# Secure traffic to Azure Front Door origins

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

Azure Front Door's features work best when traffic only flows through Front Door. You should configure your origin to block traffic that hasn't been sent through Front Door. Otherwise, traffic might bypass Front Door's web application firewall, DDoS protection, and other security features.

| Approach | Supported tiers |

|--|--|

| Private Link | Premium |

| Managed Identities | Standard, Premium |

| IP address filtering | Classic, Standard, Premium |

| Front Door identifier | Classic, Standard, Premium |

> [!NOTE]

> *Origin* and *origin group* in this article refers to the backend and backend pool of the Azure Front Door (classic) configuration.

Front Door provides several approaches that you can use to restrict your origin traffic.

## Private Link enabled origins

When you use the premium tier of Azure Front Door, you can use Private Link to send traffic to your origin. [Learn more about Private Link origins.](private-link.md)

You should configure your origin to disallow traffic that doesn't come through Private Link. The way that you restrict traffic depends on the type of Private Link origin you use:

- Azure App Service and Azure Functions automatically disable access through public internet endpoints when you use Private Link. For more information, see [Using Private Endpoints for Azure Web App](../app-service/networking/private-endpoint.md).

- Azure Storage provides a firewall, which you can use to deny traffic from the internet. For more information, see [Configure Azure Storage firewalls and virtual networks](../storage/common/storage-network-security.md).

- Internal load balancers with Azure Private Link service aren't publicly routable. You can also configure network security groups to ensure that you disallow access to your virtual network from the internet.

## Managed Identities

Managed identities provided by Microsoft Entra ID enable your Front Door instance to securely access other Microsoft Entra protected resources, such as Azure Blob Storage, without the need to manage credentials. After you enable managed identity for Front Door and granting the managed identity necessary permissions to your origin, Front Door will use the managed identity to obtain an access token from Microsoft Entra ID for accessing the specified resource. After successfully obtaining the token, Front Door will set the value of the token in the Authorization header using the Bearer scheme and then forward the request to the origin. Front Door caches the token until it expires. For more information, see [use managed identities to authenticate to origins (preview)](origin-authentication-with-managed-identities.md).

## Public IP address-based origins

When you use public IP address-based origins, there are two approaches you should use together to ensure that traffic flows through your Front Door instance:

- Configure IP address filtering to ensure that requests to your origin are only accepted from the Front Door IP address ranges.

- Configure your application to verify the `X-Azure-FDID` header value, which Front Door attaches to all requests to the origin, and ensure that its value matches your Front Door's identifier.

### IP address filtering

Configure IP address filtering for your origins to accept traffic from Azure Front Door's backend IP address space and Azure's infrastructure services only.

The *AzureFrontDoor.Backend* service tag provides a list of the IP addresses that Front Door uses to connect to your origins. You can use this service tag within your [network security group rules](../virtual-network/network-security-groups-overview.md#security-rules). You can also download the [Azure IP Ranges and Service Tags](https://www.microsoft.com/download/details.aspx?id=56519) data set, which is updated regularly with the latest IP addresses.

You should also allow traffic from Azure's [basic infrastructure services](../virtual-network/network-security-groups-overview.md#azure-platform-considerations) through the virtualized host IP addresses `168.63.129.16` and `169.254.169.254`.

> [!WARNING]

> Front Door's IP address space changes regularly. Ensure that you use the *AzureFrontDoor.Backend* service tag instead of hard-coding IP addresses.

### Front Door identifier

IP address filtering alone isn't sufficient to secure traffic to your origin, because other Azure customers use the same IP addresses. You should also configure your origin to ensure that traffic has originated from *your* Front Door profile.

Azure generates a unique identifier for each Front Door profile. You can find the identifier in the Azure portal, by looking for the *Front Door ID* value in the Overview page of your profile.

When Front Door makes a request to your origin, it adds the `X-Azure-FDID` request header. Your origin should inspect the header on incoming requests, and reject requests where the value doesn't match your Front Door profile's identifier.

### Example configuration

The following examples show how you can secure different types of origins.

# [App Service and Functions](#tab/app-service-functions)

You can use [App Service access restrictions](../app-service/app-service-ip-restrictions.md#restrict-access-to-a-specific-azure-front-door-instance) to perform IP address filtering as well as header filtering. The capability is provided by the platform, and you don't need to change your application or host.

# [Application Gateway](#tab/application-gateway)

Application Gateway is deployed into your virtual network. Configure a network security group rule to allow inbound access on ports 80 and 443 from the *AzureFrontDoor.Backend* service tag, and disallow inbound traffic on ports 80 and 443 from the *Internet* service tag.

Use a custom Web Application Firewall (WAF) rule to check the `X-Azure-FDID` header value. For more information, see [Create and use Web Application Firewall v2 custom rules on Application Gateway](../web-application-firewall/ag/create-custom-waf-rules.md#example-7).

# [Application Gateway for Containers](#tab/agc)

To configure traffic routing in Azure Kubernetes Service (AKS) with Application Gateway for Containers, set up an HTTPRoute rule to match incoming traffic from Azure Front Door using the X-Azure-FDID header.

```yaml

apiVersion: gateway.networking.k8s.io/v1

kind: HTTPRoute

metadata:

name: http-route

namespace: {namespace}

spec:

parentRefs:

- name: {gateway-name}

rules:

- matches:

- headers:

- type: Exact

name: X-Azure-FDID

value: "xxxxxxxx-xxxx-xxxx-xxxx-xxx"

backendRefs:

- name: {backend-name}

port: {port}

```

# [IIS](#tab/iis)

When you run [Microsoft Internet Information Services (IIS)](https://www.iis.net/) on an Azure-hosted virtual machine, you should create a network security group in the virtual network that hosts the virtual machine. Configure a network security group rule to allow inbound access on ports 80 and 443 from the *AzureFrontDoor.Backend* service tag, and disallow inbound traffic on ports 80 and 443 from the *Internet* service tag.

Use an IIS configuration file like in the following example to inspect the `X-Azure-FDID` header on your incoming requests:

```xml

<?xml version="1.0" encoding="UTF-8"?>

<configuration>

<system.webServer>

<rewrite>

<rules>

<rule name="Filter_X-Azure-FDID" patternSyntax="Wildcard" stopProcessing="true">

<match url="*" />

<conditions>

<add input="{HTTP_X_AZURE_FDID}" pattern="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" negate="true" />

</conditions>

<action type="AbortRequest" />

</rule>

</rules>

</rewrite>

</system.webServer>

</configuration>

```

# [AKS NGINX controller](#tab/aks-nginx)

When you run [AKS with an NGINX ingress controller](/azure/aks/ingress-basic), you should create a network security group in the virtual network that hosts the AKS cluster. Configure a network security group rule to allow inbound access on ports 80 and 443 from the *AzureFrontDoor.Backend* service tag, and disallow inbound traffic on ports 80 and 443 from the *Internet* service tag.

Use a Kubernetes ingress configuration file like in the following example to inspect the `X-Azure-FDID` header on your incoming requests:

```yaml

apiVersion: networking.k8s.io/v1

kind: Ingress

metadata:

name: frontdoor-ingress

annotations:

kubernetes.io/ingress.class: nginx

nginx.ingress.kubernetes.io/enable-modsecurity: "true"

nginx.ingress.kubernetes.io/modsecurity-snippet: |

SecRuleEngine On

SecRule &REQUEST_HEADERS:X-Azure-FDID \"@eq 0\"  \"log,deny,id:106,status:403,msg:\'Front Door ID not present\'\"

SecRule REQUEST_HEADERS:X-Azure-FDID \"@rx ^(?!xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx).*$\"  \"log,deny,id:107,status:403,msg:\'Wrong Front Door ID\'\"

spec:

#section omitted on purpose

```

---

## Related content

- Learn how to configure a [WAF profile on Front Door](front-door-waf.md).

- Learn how to [create a Front Door](quickstart-create-front-door.md).

- Learn [how Front Door works](front-door-routing-architecture.md).


# Web Application Firewall

# Web Application Firewall (WAF) on Azure Front Door

Azure Web Application Firewall (WAF) on Azure Front Door offers centralized protection for your web applications. It safeguards against common exploits and vulnerabilities, ensuring high availability and compliance. This article outlines the features of Azure Web Application Firewall on Azure Front Door. For more information, see [WAF on Azure Front Door](../web-application-firewall/afds/afds-overview.md).

## Policy settings

A Web Application Firewall (WAF) policy allows you to control access to your web applications using custom and managed rules. You can adjust the policy state or configure its mode. Depending on the settings, you can inspect incoming requests, monitor them, or take actions against requests that match a rule. You can also set the WAF to detect threats without blocking them, which is useful when first enabling the WAF. After evaluating its impact, you can reconfigure the WAF to prevention mode. For more information, see [WAF policy settings](../web-application-firewall/afds/waf-front-door-policy-settings.md).

## Managed rules

Azure Front Door WAF protects web applications from common vulnerabilities and exploits. Azure-managed rule sets offer easy deployment against common security threats. Azure updates these rules to protect against new attack signatures. The default rule set includes Microsoft Threat Intelligence Collection rules, providing increased coverage, specific vulnerability patches, and better false positive reduction. For more information, see [WAF managed rules](../web-application-firewall/afds/waf-front-door-drs.md).

> [!NOTE]

> * Managed rules are supported only by Azure Front Door Premium and Azure Front Door (classic).

> * Azure Front Door (classic) supports only DRS 1.1 or below.

## Custom rules

Azure Web Application Firewall (WAF) with Front Door allows you to control access to your web applications based on defined conditions. A custom WAF rule includes a priority number, rule type, match conditions, and an action. There are two types of custom rules: match rules and rate limit rules. Match rules control access based on specific conditions, while rate limit rules control access based on conditions and the rate of incoming requests. For more information, see [WAF custom rules](../web-application-firewall/afds/waf-front-door-custom-rules.md).

## Exclusion lists

Azure Web Application Firewall (WAF) can sometimes block requests that you want to allow. WAF exclusion lists let you omit certain request attributes from WAF evaluation, allowing the rest of the request to be processed normally. For more information, see [WAF exclusion lists](../web-application-firewall/afds/waf-front-door-exclusion.md).

## Geo-filtering

By default, Azure Front Door responds to all user requests regardless of their location. Geo-filtering allows you to restrict access to your web application by countries/regions. For more information, see [WAF geo-filtering](../web-application-firewall/afds/waf-front-door-geo-filtering.md).

## Bot protection

Azure Web Application Firewall (WAF) for Front Door includes bot protection rules to identify and allow good bots while blocking bad bots. For more information, see [configure bot protection](../web-application-firewall/afds/waf-front-door-policy-configure-bot-protection.md).

## IP restriction

IP restriction rules in Azure WAF help you control access to your web applications by specifying allowed or blocked IP addresses or IP address ranges. For more information, see [configure IP restriction](../web-application-firewall/afds/waf-front-door-configure-ip-restriction.md).

## Rate limiting

Rate limiting rules in Azure WAF control access based on matching conditions and the rate of incoming requests. For more information, see [What is rate limiting for Azure Front Door Service?](../web-application-firewall/afds/waf-front-door-rate-limit.md)

## Tuning

Azure WAF's Default Rule Set is based on the [OWASP Core Rule Set (CRS)](https://github.com/SpiderLabs/owasp-modsecurity-crs/tree/v3.1/dev) and includes Microsoft Threat Intelligence Collection rules. You can tune WAF rules to meet your application's specific needs by defining rule exclusions, creating custom rules, and disabling rules. For more information, see [WAF Tuning](../web-application-firewall/afds/waf-front-door-tuning.md).

## Monitoring and logging

Azure WAF provides monitoring and logging through integration with Azure Monitor and Azure Monitor logs. For more information, see [Azure Web Application Firewall (WAF) logging and monitoring](../web-application-firewall/afds/waf-front-door-monitor.md).

## Related content

- [Create and apply Web Application Firewall policy](../web-application-firewall/afds/waf-front-door-create-portal.md)

- [Web Application Firewall (WAF) FAQ](../web-application-firewall/afds/waf-faq.yml)


# High Availability

# High-availability implementation guide for using Azure Front Door and alternate ingress solutions

Azure Front Door is designed to provide exceptional resilience and availability for both external customers and Microsoft's internal properties. Although the architecture of Azure Front Door meets or exceeds the needs of most production workloads, no distributed system is immune to failure.

This article provides high‑level, step‑by‑step instructions for implementing Azure Traffic Manager to enable manual failover from Azure Front Door to either an alternate content delivery network (CDN) or an Azure Application Gateway web application firewall (WAF) during rare Azure Front Door service interruptions. It supplements the guidance in [Global routing redundancy for mission-critical web applications](/azure/architecture/guide/networking/global-web-applications/overview).

Multiple strategies exist within the industry for achieving high availability (HA) in CDN and web application architectures. The approach outlined in this article focuses on a straightforward, manual "break‑glass" failover pattern. Customers can use the pattern to quickly redirect traffic during an outage and seamlessly restore routing back to Azure Front Door after service health is confirmed.

The article also includes guidance for implementing HA patterns in production environments, establishing health monitoring, and creating operational runbooks to support ongoing readiness.

## Key operational differences

This guide presents two proven architectures that use Traffic Manager to provide automated failover. The following table summarizes key operational differences to consider:

| Aspect | Scenario 1 (Azure Front Door + Application Gateway) | Scenario 2 (Azure Front Door + other CDN) |

| ---- | ---- | ---- |

| Failover target | Secondary Traffic Manager instance and multiple Application Gateway instances. | Single other CDN endpoint. |

| Caching during failover | No. Application Gateway doesn't cache. | Yes. |

| Geographic distribution | Two specific Azure regions. | Other CDN's global edge network. |

| WAF protection | Azure Web Application Firewall (consistent rule sets). | Other CDN's WAF (different rule sets). |

| Cost during standby | Fixed compute costs. Application Gateway charges even when idle: ~\$200-400/month for WAF_v2 with minimal capacity. | Dependent on the CDN vendor's pricing. |

## Considerations for production environments

When you're implementing HA architectures for production workloads, consider the following best practices and important notes:

- Don't configure the primary Traffic Manager instance for automatic failover.

Azure Traffic Manager health probes originate only from US-based Azure regions. For probes of Azure Front Door endpoints (or any CDN by using anycast routing), these US-based probes almost always reach US POP servers and leave the health of non-US POP servers unverified. This situation prevents Traffic Manager from automatically failing over between Azure Front Door and another ingress service based on the true global health of the anycast CDN, such as Azure Front Door.

For global workloads that require health validation from multiple geographies, manual failover with weighted routing and monitoring disabled provides more reliable control than automated health-based routing.

- If you're currently using Azure Front Door-managed certifications, you must migrate to bring-your-own (BYO) certificates. By using your own certificate, you can keep the TLS certificates consistent regardless of which ingress path the traffic follows.

Ensure that your TLS certificates are compatible with Azure Front Door. For more information, see [Configure HTTPS on an Azure Front Door custom domain](/azure/frontdoor/standard-premium/how-to-configure-https-custom-domain) and [TLS encryption with Azure Front Door](/azure/frontdoor/end-to-end-tls).

- Always test failover procedures in non-production environments first.

- Traffic Manager doesn't support CNAME flattening at the DNS zone apex (root domain). If you require Traffic Manager at the apex, you must use DNS providers that support alias records or similar mechanisms. [Azure DNS](/azure/dns/dns-alias) is one such DNS provider.

- Use short DNS time-to-live (TTL) values of 300-600 seconds. Monitor DNS TTL propagation times.

- Lock down Application Gateway with network security groups (NSGs) and access control lists (ACLs). Allow required platform ranges and inbound application ports. Keep origins secured for all ingress paths. For more information, see [Network security groups](/azure/application-gateway/configuration-infrastructure#network-security-groups).

Although an Application Gateway WAF mitigates HTTP/L7 attacks, NSGs provide packet filtering only and don't protect against volumetric or protocol-level (L3/L4) DDoS attacks. All Azure public endpoints benefit from baseline, always-on DDoS protection in the Azure platform. It helps protect the Azure infrastructure but doesn't include workload-specific tuning, telemetry, cost protection, or availability guarantees.

For production and mission-critical workloads, consider using the Azure DDoS Protection service to help protect Application Gateway public IPs. For more information, see [Azure DDoS Protection pricing](https://azure.microsoft.com/pricing/details/ddos-protection).

- Document WAF rule differences between Azure Front Door and failover solutions.

- We don't recommend Azure Private Link for these HA architectures because alternate CDN platforms can't access origins protected by Private Link integration in Azure Front Door.

Also, Application Gateway requires extra virtual network and private endpoint configuration to reach private origins. Application Gateway can't use the native Private Link capabilities of Azure Front Door.

For production environments that use Azure Front Door alongside other CDN providers, consider using alternative, CDN‑agnostic origin‑security controls to enforce origin trust when you can't use Private Link or `X‑Azure‑FDID` validation. These controls might include token‑based origin authentication (HMAC or signed URLs), mutual TLS (mTLS), custom origin headers, and IP address filtering.

- Edit the sample commands listed in this guide so that they're tailored to your environment for automation and runbooks.

- Establish clear runbooks. Test failover and failback procedures.

- Configure comprehensive monitoring and alerting for all endpoints.

- Validate functionality during failover to alternate ingress solutions.

- Test certificate renewal processes across all platforms.

- Regularly validate that failover endpoints remain functional. We recommend quarterly testing.

- This guide uses Azure CLI sample commands that you run from PowerShell.

- Before you proceed, review [Global routing redundancy for mission-critical web applications](/azure/architecture/guide/networking/global-web-applications/overview).

## Scenario 1: Traffic Manager failover from Azure Front Door to an Application Gateway WAF

This DNS-based load-balancing solution uses multiple Azure Traffic Manager profiles. In the unlikely event of an availability problem with Azure Front Door, Traffic Manager redirects traffic through the Application Gateway WAF. The primary Traffic Manager instance routes traffic between Azure Front Door (primary) and a nested secondary Traffic Manager instance that points to multi-region Application Gateway instances. During an Azure Front Door outage, traffic is manually failed over to regional Application Gateway deployments that have WAF protection.

- **Traffic flow (normal operation)**: User → DNS query → primary Traffic Manager instance (weighted/always-serve routing) → Azure Front Door (priority 1) → origin servers.

- **Traffic flow (Azure Front Door failure)**: User → DNS query → primary Traffic Manager instance (weighted/always-serve routing) → secondary Traffic Manager instance (priority mode) → Application Gateway → origin servers.

### Pre-deployment: Azure Front Door vs. Application Gateway

It's important to understand the feature differences between Azure Front Door and an Application Gateway WAF, in case you're using any features that an Application Gateway WAF doesn't offer. The following tables provide an overview.

> [!IMPORTANT]

> This solution assumes that you're currently using Azure Front Door to serve traffic across multiple regions or globally. In this design, the steps that follow introduce a secondary Traffic Manager instance that's configured with performance routing between the primary Traffic Manager instance and regional Application Gateway instances.

>

> This approach is necessary because Azure Front Door is a global Layer‑7 service. The secondary Traffic Manager instance effectively replaces global latency‑based routing in Azure Front Door by acting as the global load‑balancing layer. As a result, Traffic Manager preserves latency‑optimized user routing for a geographically distributed audience.

>

> Given this architectural shift, you must evaluate global traffic patterns and deploy Application Gateway instances in regions that have meaningful user volume to ensure optimal performance and resilience.

#### Feature differences

| Feature | Azure Front Door | Application Gateway |

| --- | --- | --- |

| **Core architecture and features** | | |

| Service scope | Global service | Regional service |

| OSI layer | Layer 7 (application layer) | Layer 7 (application layer) |

| Load-balancing level | Across regions | Within a region or virtual network |

| Deployment model | Single global instance | Per-region instances |

| Backend scope | Any public endpoint (Azure or external), and selected Private Link endpoints | Any public endpoint (Azure or external), private IP addresses, and Kubernetes pods in a virtual network |

| Content edge caching | Yes | No |

| Network architecture | Microsoft's global edge network with anycast | Azure regional deployment (no anycast) |

| **Configuration differences** | | |

| Path pattern syntax | `/path/*` or exact `/path` | Regex patterns, path maps |

| WAF rule sets | Default rule set (OWASP), bot manager ruleset, HTTP DDoS ruleset | Default rule set (OWASP), bot manager ruleset, HTTP DDoS ruleset |

| Health probe evaluation | Latency + health for routing | Health status only |

| Backend selection | Based on priority, weight, latency | Round-robin, cookie affinity |

| **Routing rules** | | |

| Path-based routing | ✓ Yes | ✓ Yes |

| Pattern matching | Exact-match paths, wildcard paths (`/*`), case-insensitive, wildcard must be preceded by `/` | URL path maps, path-based rules, regex patterns supported |

| Host-based routing | ✓ Multiple frontend hosts | ✓ Multi-site hosting |

| URL rewrite | Static path to static path (classic) | URL path rewrite |

| Routing methods | Priority, weight, latency-based | Load aware for latency optimization*, weighted*, session affinity (*available with Application Gateway for Containers) |

| **Routing features** | | |

| Rules engine/rewrite rules | Rule sets with conditions and actions | Rewrite rule sets with conditions and actions |

| Regex in path patterns | Not supported in **Patterns to match** | Supported with PCRE |

| **Header and request manipulation** | | |

| Header rewrite | ✓ Request and response headers | ✓ Request and response headers |

| Header value character limit | No documented limit | 1,000 characters in rewrite rules |

| Host header rewrite | ✓ Supported | ✓ Supported (can't rewrite to external domains) |

| Server variables | ✓ Supported | ✓ Supported |

| Header pattern matching | Conditions with patterns | Regex pattern matching |

| **Security features** | | |

| WAF availability | ✓ Optional (Premium tier) | ✓ Optional (WAF tier) |

| L3/4 DDoS protection | ✓ Built-in | Via Azure DDoS Protection service |

| SSL/TLS policies | ✓ Configurable | ✓ Configurable |

| End-to-end SSL | ✓ Supported | ✓ Supported |

| Private Link support | ✓ Premium tier | ✓ V2 tier |

| WAF custom rules | ✓ Supported | ✓ Supported |

#### WAF differences

| Azure Front Door | Application Gateway |

| ---- | ---- |

| Microsoft Default Rule Set (DRS) 2.1 | OWASP Core Rule Set (CRS) 3.2 or 4.0 |

| Rule IDs: 949xxx series | Rule IDs: 9xxxxx series |

| Azure Front Door WAF (DRS): inspects first 128 KB of request body | Application Gateway WAF (CRS 3.2+): up to 2-MB inspection; 4-GB file upload; enforcement and inspection can be configured independently |

### Recommendations

- Because you must maintain distinct rule sets for each WAF, use the Azure Front Door rule set as your baseline. Create an Application Gateway rule set that matches the Azure Front Door rule set as closely as possible.

- Test the Application Gateway WAF separately and independently.

- Document all custom exclusions for both platforms.

- Regularly audit rule sets for consistency.

- Adhere to the network guidance in [Azure Application Gateway infrastructure configuration](/azure/application-gateway/configuration-infrastructure). Be sure to exercise the following virtual network and subnet requirements:

- Use the following subnet sizing (per region):

- Minimum: /27 (32 addresses)

- Recommended: /24 (256 addresses) for autoscaling and hitless maintenance

- Formula: (maximum instances \* 10) + 5 Azure reserved IPs

- Example: 20 maximum instances → (20 \* 10) + 5 = 205 IPs → use /24

- For optimal security, use a dedicated subnet for Application Gateway (no other resources).

- Make sure that the inbound connection allows:

- 443/80 from the internet (or specific source ranges)

- 65200-5535 from Azure Gateway Manager (Application Gateway v2)

- Azure Load Balancer

- Block other inbound connections. Don't block required outbound internet connections.

- Use application security groups for backend segmentation and least-privilege rules.

For capacity planning and autoscaling strategy, see [Architecture best practices for Azure Application Gateway v2](/azure/well-architected/service-guides/azure-application-gateway).

### Key implementation steps

#### Step 1: Provision prerequisites

- Azure Front Door configured with a custom domain and BYO certificate.

- A lower DNS TTL for your CNAME record so that Azure Front Door serves traffic to the lowest time setting.

- Azure subscription with permissions to create virtual networks, an Application Gateway instance, and a Traffic Manager instance.

- SSL/TLS certificate in Azure Key Vault or available for upload.

- Origin servers accessible from Azure virtual networks.

> [!IMPORTANT]

> If you're currently using Azure Front Door-managed certificates, you must migrate to BYO certificates before implementing this solution. Azure Front Door-managed certificates can't be exported and installed on alternative CDNs. For more information, see [Configure HTTPS on an Azure Front Door custom domain](/azure/frontdoor/standard-premium/how-to-configure-https-custom-domain).

#### Step 2: Deploy Application Gateway in the first region

1. Create a network infrastructure for Application Gateway. For more information, see [Application Gateway infrastructure configuration](/azure/application-gateway/configuration-infrastructure).

1. Create a managed identity and grant Key Vault access. For more information, see [TLS termination with Key Vault certificates](/azure/application-gateway/key-vault-certs).

Application Gateway requires the SSL/TLS certificate in PFX format with a private key. The certificate must be accessible from Key Vault or uploaded directly. Use the same certificate that Azure Front Door uses to ensure consistent TLS behavior.

1. Create a WAF policy. For more information, see [Create WAF policies for Application Gateway](/azure/web-application-firewall/ag/create-waf-policy-ag).

1. Create an Application Gateway instance with HTTPS and WAF. For more information, see [Configure an Application Gateway instance with TLS termination](/azure/application-gateway/create-ssl-portal).

1. Configure a backend host header. For more information, see [Troubleshoot backend health issues in Application Gateway](/azure/application-gateway/application-gateway-backend-health-troubleshooting).

1. Verify Application Gateway:

```

# Get Application Gateway public IP

$APPGW_IP = az network public-ip show `

--name $APPGW_PIP_NAME_R1 `

--resource-group $RESOURCE_GROUP `

--query ipAddress -o tsv

Write-Host "Application Gateway IP: $APPGW_IP"

# Test Application Gateway directly (SkipCertificateCheck because certificate is for domain, not IP)

Invoke-WebRequest -Uri "https://$APPGW_IP/index.html" -Method Head -SkipCertificateCheck

```

The expected result is status code 200. If you get "502 Bad Gateway," ensure that the backend HTTP settings have `--host-name-from-backend-pool true` enabled.

#### Step 3: Configure WAF policy settings (optional)

By default, a WAF is created in detection mode. Prevention mode actively blocks malicious requests. Test thoroughly before you enable prevention mode in production.

Evaluate your global traffic patterns and deploy Application Gateway instances in regions that have a meaningful user volume. If you're deploying Application Gateway in multiple regions, repeat steps 2 and 3 for each additional region (for example, West US 2). Use different virtual network address spaces (10.2.0.0/16, 10.3.0.0/16, and so on) and region-specific variable suffixes (R2, R3, and so on).

#### Step 4: Create a Traffic Manager architecture to support the Application Gateway WAF endpoints

1. Create a secondary Traffic Manager instance in performance mode, as shown earlier in the diagram for this scenario. For more information, see [Create a Traffic Manager profile](/azure/traffic-manager/traffic-manager-create-profile).

For a single-region configuration, use these details:

- **Routing method**: Priority.

- **Endpoint**: Single Application Gateway public IP address.

For a multi-region configuration, use these details:

- **Routing method**: Performance (routes users to nearest healthy Application Gateway instance).

- **Endpoints**: Multiple Application Gateway public IP addresses across regions.

- **Endpoint locations**: The Azure region for each endpoint (required for performance routing).

Use these configuration settings:

| Setting | Value | Notes |

| ---- | ---- | ---- |

| **Routing method** | **Performance** (multi-region) or **Priority** (single-region) | **Performance** optimizes latency for a multi-region configuration. |

| **Protocol** | **HTTPS** | Validates Application Gateway health via HTTPS. |

| **Port** | **443** | Standard HTTPS port. |

| **Path** | `/health` or `/index.html` | Must match the path of the Application Gateway backend health probe. |

| **TTL** | **300 seconds** | Balances DNS query load and responsiveness. |

> [!NOTE]

> By default, Azure public IPs for Application Gateway don't have DNS names configured. You must use the public IP address directly in Traffic Manager endpoints, not a DNS name. The `--endpoint-location` parameter is required for performance routing to enable geographic routing.

1. Create a primary weighted/always-serve Traffic Manager instance, as shown earlier in the diagram for this scenario. For more information, see [Create a Traffic Manager profile](/azure/traffic-manager/traffic-manager-create-profile).

For both endpoints, use these configurations:

| Setting | Value | Notes |

| ---- | ---- | ---- |

| **Routing Method** | **Weighted** | Allows manual control via endpoint status (enabled or disabled). |

| **Weight** | **100** |   |

| **Protocol** | **HTTPS** | Required for validating SSL/TLS endpoints. |

| **Port** | **443** | Standard HTTPS port. |

| **Path** | `/index.html` | Choose a lightweight endpoint for health checks. |

| **TTL** | **300 seconds** | DNS TTL. Lower values enable faster failover but increase DNS queries. |

| **Health Check** | **Always serve traffic** | Don't enable health checks. |

These configurations are specific to the primary endpoint:

- **Type**: **External endpoint**

- **Name**: **endpoint-afd-primary**

- **Fully-qualified domain name (FQDN) or IP address**: Host name of the Azure Front Door endpoint (for example, `myapp-12345.z01.azurefd.net`)

- **Enable Endpoint**: Selected (enabled)

- **Custom Header settings**: `Host=$CUSTOM_DOMAIN` (required for Azure Front Door to route to the correct custom domain)

- **Health Checks**: **Always serve traffic** (disable health checks)

These configurations are specific to the secondary endpoint:

- **Type**: **External endpoint**

- **Name**: **endpoint-appgw-secondary**

- **Fully-qualified domain name (FQDN) or IP address**: Secondary Traffic Manager FQDN (for example, `myapp-appgw.trafficmanager.net`)

- **Enable Endpoint**: Cleared (disabled)

1. Verify Traffic Manager health:

```azurecli

# Check endpoint health status

az network traffic-manager profile show `

--name $ATM_PRIMARY_PROFILE `

--resource-group $RESOURCE_GROUP `

--query "{ProfileStatus:profileStatus, MonitorStatus:monitorConfig.profileMonitorStatus, Endpoints:endpoints\[\].{Name:name, Target:target, Priority:priority, Status:endpointMonitorStatus}}"

```

Both endpoints should show `Status: Online`. If an endpoint shows `Degraded` or `CheckingEndpoint`, wait 1-2 minutes for health probes to finish.

#### Step 5: Update DNS CNAME to Traffic Manager and verify the update

> [!WARNING]

> The following steps will redirect your production traffic from Azure Front Door directly to Traffic Manager and cause a potential service impact. Before you proceed:

>

> - Test these steps in a non-production environment first. For example, temporarily modify the local `hosts` file on a non‑production workstation to resolve the custom domain to the Traffic Manager endpoint. This modification allows validation without affecting live traffic.

> - Reduce your DNS CNAME TTL to the lowest value possible (for example, 60-300 seconds) at least 24 hours before you make changes.

> - Plan for a maintenance window during low-traffic periods if possible.

> - Have rollback procedures ready in case problems arise.

1. Update your DNS CNAME record to point to the primary Traffic Manager instance instead of directly to Azure Front Door.

| Field | Old value | New value |

| ---- | ---- | ---- |

| **Name/Host** | **www** | **www** (no change) |

| **Value/Points to** | Host name of the Azure Front Door endpoint | `$ATM_DNS_NAME.trafficmanager.net` |

1. Verify Traffic Manager resolution:

```

# Verify Traffic Manager profile is resolving

nslookup "$ATM_DNS_NAME.trafficmanager.net"

```

The test should return the IP address of the Azure Front Door endpoint.

1. Wait for DNS propagation, and then test HTTPS connectivity. DNS propagation typically takes 5-10 minutes but can take up to 48 hours globally.

```

# Check DNS from different resolvers

nslookup $CUSTOM_DOMAIN 8.8.8.8 # Google DNS

# Test HTTPS connectivity

Invoke-WebRequest -Uri "https://$CUSTOM_DOMAIN/index.html" -Method Head

```

This test should return status code 200.

1. After the DNS cutover, actively monitor the following Azure Front Door metrics:

- **Request count**: The count should remain consistent, with no drop in traffic.

- **Response time**: The time should remain within normal ranges.

- **Error rates**: 4xx/5xx errors shouldn't increase.

- **Origin health**: Backend health should remain `Online`.

#### Step 6: Test failover procedures

1. Simulate Azure Front Door failure (manual failover to Application Gateway):

```

# Manual failover to Application Gateway

# Disable Azure Front Door endpoint

az network traffic-manager endpoint update `

--name "endpoint-afd-primary" `

--profile-name $ATM_PRIMARY_PROFILE `

--resource-group $RESOURCE_GROUP `

--type externalEndpoints `

--endpoint-status Disabled

# Enable secondary Traffic Manager endpoint (Application Gateway)

az network traffic-manager endpoint update `

--name "endpoint-appgw-secondary" `

--profile-name $ATM_PRIMARY_PROFILE `

--resource-group $RESOURCE_GROUP `

--type externalEndpoints `

--endpoint-status Enabled

# Verify Traffic Manager endpoint status

az network traffic-manager endpoint list `

--profile-name $ATM_PRIMARY_PROFILE `

--resource-group $RESOURCE_GROUP `

--query "[].{Name:name, Status:endpointStatus, Health:endpointMonitorStatus}" `

--output table

# Flush DNS cache (Windows)

ipconfig /flushdns

# Verify DNS resolution (should now point to secondary Traffic Manager instance and Application Gateway)

nslookup $CUSTOM_DOMAIN

# Test - should now work via Application Gateway

curl --head https://$CUSTOM_DOMAIN/

```

> [!NOTE]

> DNS TTL affects failover time. With a TTL of 60 seconds, clients might take up to 60 seconds to see the change. Use `nslookup` to verify that resolution points to Application Gateway.

2. Fail back to Azure Front Door:

```

# Re-enable Azure Front Door endpoint

az network traffic-manager endpoint update `

--name "endpoint-afd-primary" `

--profile-name $ATM_PRIMARY_PROFILE `

--resource-group $RESOURCE_GROUP `

--type externalEndpoints `

--endpoint-status Enabled

# Disable Application Gateway (via Secondary Traffic Manager)

az network traffic-manager endpoint update `

--name "endpoint-appgw-secondary" `

--profile-name $ATM_PRIMARY_PROFILE `

--resource-group $RESOURCE_GROUP `

--type externalEndpoints `

--endpoint-status Disabled

# Verify endpoint status

az network traffic-manager endpoint list `

--profile-name $ATM_PRIMARY_PROFILE `

--resource-group $RESOURCE_GROUP `

--query "[].{Name:name, Status:endpointStatus, Health:endpointMonitorStatus}" `

--output table

# Flush DNS cache (Windows)

ipconfig /flushdns

# Verify DNS resolution (should now point back to Azure Front Door)

nslookup $CUSTOM_DOMAIN

# Test - should now work via Azure Front Door

curl --head https://$CUSTOM_DOMAIN/

```

3. Verify the current routing:

```

# Check which endpoint is serving traffic

nslookup $CUSTOM_DOMAIN

Invoke-WebRequest -Uri "https://$CUSTOM_DOMAIN/index.html" -Method Head | Select-Object -ExpandProperty Headers

```

The response headers can help identify the serving endpoint:

- Azure Front Door includes the `x-azure-ref` header.

- Traffic that passes through Application Gateway might include `Server: Microsoft-IIS` or similar.

## Scenario 2: Traffic Manager failover from Azure Front Door to an alternative CDN

This solution uses a single Traffic Manager profile with weighted/always-serve routing so that you can manually switch over traffic between Azure Front Door and an alternative CDN.

- **Primary endpoint**: Azure Front Door custom domain endpoint.

- **Secondary endpoint**: Alternative CDN endpoint.

- **Traffic flow (normal operation)**: User → DNS query → Traffic Manager (weighted/always-serve routing) → Azure Front Door (priority 1) → origin servers.

- **Traffic flow (Azure Front Door failure)**: User → DNS query → Traffic Manager (weighted/always-serve routing) → alternative CDN (priority 2) → origin servers.

### Key implementation steps

#### Step 1: Provision prerequisites

Configure your secondary CDN provider with:

- Azure Front Door configured with a custom domain and a BYO certificate.

- An alternative CDN account.

- A lower DNS TTL for your CNAME record so that Azure Front Door serves traffic to the lowest time setting.

- Origin servers that both Azure Front Door and the alternative CDN can access.

- A custom domain that can modify DNS records.

> [!IMPORTANT]

> If you're currently using Azure Front Door-managed certificates, you must migrate to BYO certificates before implementing this HA solution. Azure Front Door-managed certificates can't be exported and installed on alternative CDNs. For more information and configuration instructions for BYO certificates, see [Configure HTTPS on an Azure Front Door custom domain](/azure/frontdoor/standard-premium/how-to-configure-https-custom-domain).

#### Step 2: Configure an alternative CDN

Configure your secondary CDN provider:

- Set up the CDN zone or property with your custom domain.

- Configure origin servers the same way that you configured the Azure Front Door backend pool.

- Upload the BYO SSL/TLS certificate. This certificate is the same one that you used in Azure Front Door.

- Configure CDN caching rules to match Azure Front Door behavior. For example, configure cache durations and query string handling.

- Set up caching settings, control headers, and compression settings to match your Azure Front Door configuration.

- Set up WAF rules if the CDN provider offers WAF capabilities. Try to match the Azure Front Door WAF policy.

- Configure a custom domain to match your Azure Front Door custom domain (for example, `www.contoso.com`).

- Record the CDN edge's host name for Traffic Manager configuration (for example, `your-site.cdn.provider.net`).

#### Step 3: Create a Traffic Manager profile

Apply the following configurations to create the Traffic Manager profile. For more information, see [Create a Traffic Manager profile](/azure/traffic-manager/quickstart-create-traffic-manager-profile).

| Setting | Value | Notes |

| ---- | ---- | ---- |

| **Routing Method** | **Weighted** | Allows manual control via endpoint status (enabled or disabled). |

| **Weight** | **100** | Enter **100** when the Traffic Manager profile is created and for both endpoints. |

| **Protocol** | **HTTPS** | Required for validating SSL/TLS endpoints. |

| **Port** | **443** | Standard HTTPS port. |

| **Path** | `/index.html` | Choose a lightweight endpoint for health checks. |

| **TTL** | **300 seconds** | DNS TTL. Lower values enable faster failover but increase DNS queries. |

#### Step 4: Configure Traffic Manager endpoints

Create two endpoints within the Traffic Manager profile.

Use these configurations for the primary endpoint (Azure Front Door):

- **Type**: **External endpoint**

- **Name**: **endpoint-afd-primary**

- **Fully-qualified domain name (FQDN) or IP address**: Host name of the Azure Front Door endpoint (for example, `myapp-endpoint-12345.z01.azurefd.net`)

- **Weight**: **100**

- **Enable Endpoint**: Selected (enabled) initially

- **Custom Header settings**: `Host=$CUSTOM_DOMAIN` (required for Azure Front Door to route to the correct custom domain)

- **Health Checks**: **Always serve traffic** (disable health checks)

> [!NOTE]

> The `--custom-headers "Host=$CUSTOM_DOMAIN"` parameter is critical for Azure Front Door endpoints. Without it, Azure Front Door might not properly route requests to your custom domain configuration. It's a supported feature of Azure Traffic Manager.

Use these configurations for the secondary endpoint (alternative CDN):

- **Type**: **External endpoint**

- **Name**: **endpoint-cdn-secondary**

- **Fully-qualified domain name (FQDN) or IP address**: CDN edge's host name (for example, `myapp.cdn.net`)

- **Weight**: **100**

- **Enable Endpoint**: Cleared (disabled) initially for standby mode

#### Step 5: Update DNS CNAME to Traffic Manager and verify the update

> [!WARNING]

> The following steps will redirect your production traffic from Azure Front Door directly to Traffic Manager. Before you proceed:

>

> - Test these steps in a non-production environment first.

> - Reduce your DNS CNAME TTL to the lowest value possible (for example, 60-300 seconds) at least 24 hours before you make changes.

> - Plan for a maintenance window during low-traffic periods if possible.

> - Have rollback procedures ready in case problems arise.

1. Update your DNS CNAME record to point to Traffic Manager instead of directly to Azure Front Door:

| Field | Old value | New value |

| ---- | ---- | ---- |

| **Name/Host** | **www** | **www** (no change) |

| **Value/Points to** | Host name of the Azure Front Door endpoint | `$ATM_CDN_DNS_NAME.trafficmanager.net` |

DNS propagation typically takes 5-10 minutes but can take up to 48 hours globally.

2. Verify Traffic Manager resolution. Wait for DNS propagation, and then test HTTPS connectivity.

```

# Verify Traffic Manager profile is resolving

nslookup "$ATM_CDN_DNS_NAME.trafficmanager.net"

# Expected result: Should return IP address of Azure Front Door endpoint

# Check DNS from different resolvers

nslookup $CUSTOM_DOMAIN 8.8.8.8    # Google DNS

# Test HTTPS connectivity

Invoke-WebRequest -Uri "https://$CUSTOM_DOMAIN/index.html" -Method Head

# Expected result: Status code 200

```

3. After the DNS cutover, actively monitor the following Azure Front Door metrics:

- **Request count**: The count should remain consistent, with no drop in traffic.

- **Response time**: The time should remain within normal ranges.

- **Error rates**: 4xx/5xx errors shouldn't increase.

- **Origin health**: Backend health should remain `Online`.

#### Step 6: Test failover procedures

1. Manually fail over to the alternative CDN:

```

# Failover: Disable Azure Front Door and enable CDN

az network traffic-manager endpoint update `

--name "endpoint-afd-primary" `

--profile-name $ATM_CDN_PROFILE_NAME `

--resource-group $RESOURCE_GROUP `

--type externalEndpoints `

--endpoint-status Disabled

az network traffic-manager endpoint update `

--name "endpoint-cdn-secondary" `

--profile-name $ATM_CDN_PROFILE_NAME `

--resource-group $RESOURCE_GROUP `

--type externalEndpoints `

--endpoint-status Enabled

# Verify endpoint status

az network traffic-manager profile show `

--name $ATM_CDN_PROFILE_NAME `

--resource-group $RESOURCE_GROUP `

--query "endpoints[].{Name:name, Status:endpointStatus, Health:endpointMonitorStatus, Target:target}"

# Flush local DNS cache and verify resolution

ipconfig /flushdns

nslookup "$ATM_CDN_DNS_NAME.trafficmanager.net"

# Test HTTPS access

curl --head https://$CUSTOM_DOMAIN/

```

2. Fail back to Azure Front Door:

```

# Failback: Enable Azure Front Door, disable CDN

az network traffic-manager endpoint update `

--name "endpoint-afd-primary" `

--profile-name $ATM_CDN_PROFILE_NAME `

--resource-group $RESOURCE_GROUP `

--type externalEndpoints `

--endpoint-status Enabled

az network traffic-manager endpoint update `

--name "endpoint-cdn-secondary" `

--profile-name $ATM_CDN_PROFILE_NAME `

--resource-group $RESOURCE_GROUP `

--type externalEndpoints `

--endpoint-status Disabled

# Verify

az network traffic-manager profile show `

--name $ATM_CDN_PROFILE_NAME `

--resource-group $RESOURCE_GROUP `

--query "endpoints[].{Name:name, Status:endpointStatus, Health:endpointMonitorStatus}"

```

## Monitoring

> [!IMPORTANT]

> Configure synthetic monitors to alert immediately on failures. These alerts should trigger manual failover if automatic failover is insufficient (for example, Azure Front Door custom domain problems that Traffic Manager can't detect).

We recommend the following monitoring solutions for production environments:

- **Azure Monitor workbooks**: Track Traffic Manager queries, Azure Front Door requests, and Application Gateway health. For more information, see the [overview of workbooks](/azure/azure-monitor/visualize/workbooks-overview).

- **Outside-in monitoring to detect global Azure Front Door problems**: Implement outside-in global synthetic monitoring solutions (such as Catchpoint or ThousandEyes) to monitor endpoints. Services like [WebPageTest](https://www.webpagetest.org/) offer a free alternative that provides limited global visibility.

- **Application Insights availability tests**: Use multi-region HTTP checks. For more information, see [Application Insights availability tests](/azure/azure-monitor/app/availability-overview).

- **DNS monitoring**: Validate CNAME resolution chain and TTL propagation via DNSPerf, Pingdom, or Uptime.com.

- **Certificate monitoring**: Use [SSL Server Test](https://www.ssllabs.com/ssltest/) from Qualys SSL Labs to analyze your server's configuration.


# Video On Demand Live Streaming

# Delivering video on-demand and live streaming with Azure Front Door

Azure Front Door's architecture is designed to optimize global content delivery by leveraging Microsoft's private backbone network together with a large global-edge footprint.

Azure Front Door minimizes latency and avoids congested public internet paths by routing traffic across Microsoft's private network between distributed edge locations, providing highly resilient delivery infrastructure. Combined with Microsoft's extensive peering relationships and redundant network paths, this architecture enables streaming workloads to reach deep into regional and last-mile networks and deliver a stable playback experience for end users with minimal buffering, whether your audience is a few thousand internal viewers or a global audience of concurrent users.

## Azure Front Door DASH streaming configuration optimization

The following configuration examples illustrate how Azure Front Door is tuned to optimize delivery of MPEG-DASH video-on-demand (VOD) streaming workloads.

| Front Door configuration category | Configuration | Why it matters |

|---------------------------|---------------|----------------|

| Rules | Disable compression for segment files (*.m4s* and *.mp4*) | DASH and HLS media segments are already compressed video and audio data. Recompressing them provides no benefit and introduces unnecessary CPU overhead and latency during delivery. |

| Rules | Enable compression for manifest and playlist files (*.mpd* and *.m3u8*) | DASH and HLS manifests are small text-based XML or plain-text files that compress efficiently (often 70–80% size reduction). Enabling compression reduces manifest transfer time and improves initial player startup and playlist refresh performance. |

| Rules | Cache *.m3u8* and *.mpd* playlist files for 3 hours | For VOD, playlist files are static after publication. They don't change between viewer sessions. Caching them aggressively at the edge eliminates repeated round-trips to origin and accelerates startup time for every viewer. <br> **Note:** this TTL is specific to VOD and must not be applied to live streaming manifests. |

| Rules | Cache *.m4s* segment files for 1 hour (or longer with `immutable`) | VOD video segments are immutable once encoded and published. They never change. Caching them at the edge for extended durations prevents redundant origin fetches and improves throughput consistency. For truly immutable VOD assets, consider setting `Cache-Control: max-age=86400, immutable` at the origin to signal that the segment is never invalidated. |

| Rules | Ignore query string for caching | Some players append transient query parameters (for example: timestamps, client session IDs) to segment requests. Ignoring query strings prevents cache fragmentation and ensures identical media segments are served from the same cached object. Important exception: if your deployment uses URL-based token authentication (for example: Azure SAS tokens appended as query parameters), don't ignore query strings globally. Instead, configure Azure Front Door to pass through specific security parameters while ignoring nonsecurity ones. See the Content Protection note in the infrastructure considerations section below for a discussion of access control patterns and their caching trade-offs. |

| Route | Enable caching at the route level | Route-level caching ensures that requests matched by the path are cached by Azure Front Door's edge even if no specific rule explicitly enables caching. This configuration acts as a catch-all baseline for the streaming content path. |

| Route | Query string caching behavior: *Ignore query string* | This setting reinforces the rule-level configuration and ensures consistent cache behavior for all requests matching the route, including requests that don't match a more specific rule. |

| Route | Forwarding protocol: **HTTP only** (to origin) | If the origin resides within a trusted private network boundary behind Azure Front Door (such as Azure Blob Storage on a private endpoint), removing the TLS negotiation hop between Azure Front Door edge and origin reduces latency on every cache miss. <br> **Caveat:** if your content is DRM-protected (for example: PlayReady, Widevine) or your origin serves license or key material, maintain HTTPS to origin regardless of network topology. The sensitivity of encryption keys warrants the added latency overhead. |

| Route | Redirect client traffic to **HTTPS** | Viewer traffic remains encrypted end-to-end from the client to the Azure Front Door edge, which is the required security posture for any media delivery workload. It's essential for DRM playback environments where browsers enforce secure contexts. |

| Route | Pattern match /content/* (scope to streaming path) | Scoping rules to the specific content path ensures that these optimizations apply only to streaming assets and don't inadvertently affect other endpoints - such as APIs, auth services, or web app traffic - served by the same Azure Front Door instance. |

> [!NOTE]

> The caching TTLs and rules in the preceding table apply specifically to MPEG‑DASH VOD delivery, where media segments are immutable after publication and manifest files change far less frequently than in live streaming workflows. Live streaming manifests require a fundamentally different caching strategy. Playlist files must not be cached (or cached only briefly, typically for one to two segment durations) so that players always receive the current segment list. See the Live Streaming section for live‑specific guidance.

## Where Azure Front Door fits in a modern streaming architecture

Modern streaming delivery architectures combine multiple layers of infrastructure to optimize scale, resiliency, and performance. What that looks like in practice varies significantly depending on the size and nature of the operation - from a media team publishing training videos to a global OTT platform serving millions of concurrent streams. Azure Front Door is designed to play a meaningful role across this entire spectrum.

### Streaming use cases

Azure Front Door's private backbone routing, global edge footprint, and tight integration with Azure services make it a strong delivery tier across the following scenarios:

**Small and mid-size businesses and enterprises:** For organizations delivering internal communications, training libraries, customer-facing video portals, or product marketing content, Azure Front Door provides a complete delivery stack without the operational overhead of a dedicated media CDN. Pairing Azure Front Door with Azure Blob Storage for VOD - and with encoding and packaging partners from the Azure ecosystem - gives teams a globally distributed pipeline that scales automatically and integrates with existing Azure security, identity, and monitoring tooling.

**Large virtual events and high-audience live broadcasts:** Conferences, product launches, company town halls, and live sports broadcasts benefit from Azure Front Door's unicast routing and Microsoft's backbone - which keeps traffic off congested public internet paths during peak concurrent load. For broadcast-grade live events with very high concurrent viewer counts, Azure Front Door can operate as the primary delivery tier or as part of a multi-CDN strategy with automated failover between providers.

**Regional and emerging OTT platforms:** Growing streaming services that are building scalable distribution infrastructure - and that operate in geographies where Microsoft has strong peering and last-mile reach - will find Azure Front Door a competitive alternative to established media CDN providers. As Azure Front Door's media-specific feature set continues to mature, it's increasingly capable of supporting the operational demands of continuous, high-volume streaming at scale.

**Hyperscale multi-CDN environments:** For platforms operating at the scale of the largest global OTT providers - where delivery architectures span multiple CDNs, custom origin infrastructure, and proprietary caching layers - Azure Front Door can integrate naturally as a high-performance delivery tier within a broader multi-CDN strategy. Azure Front Door's Rules Engine, real-time health probes, and origin group failover give platform engineers the control surface needed to manage Azure Front Door alongside other CDN providers and route traffic intelligently based on performance, cost, or geography.

## Infrastructure considerations

Successful Azure Front Door streaming deployments require attention to several infrastructure aspects:

- **CORS headers:** Any video player running in a browser issues cross-origin requests for media segments and manifest files. Without correct Cross-Origin Resource Sharing (CORS) headers, specifically Access-Control-Allow-Origin on segment and manifest responses, browser-based playback fails entirely due to browser security policy enforcement. Configure CORS headers either at the origin or via Azure Front Door's response header modification rules. This configuration is important when your player UI is served from a different domain than your media CDN endpoint.

- **DRM integration:** Commercial VOD and live streaming deployments that require content protection use Digital Rights Management - typically some combination of Microsoft PlayReady, Google Widevine, and Apple FairPlay depending on the target device ecosystem. DRM license server requests must not be cached and should be routed separately from media segments. Azure Front Door can forward license requests to a DRM license origin while caching media segments independently. Plan your Azure Front Door route configuration to distinguish between licensable media paths and license acquisition endpoints from the start.

- **Content protection:** Azure Front Door's WAF provides baseline geo-filtering and rate limiting at the policy level. Native cryptographic URL request signing at the edge is on the Azure Front Door roadmap but isn't currently available in production releases. In the interim, access control for streaming content typically involves a lightweight origin-side or middleware token validation layer - for example, an Azure Function that issues short-lived access tokens, which are validated before content requests are proxied through Azure Front Door. One important nuance for any signed URL approach in streaming: signed URLs applied to individual media segments fragment your CDN cache, since each viewer receives a unique signed URL and the CDN treats each variant as a distinct cache key. For high-scale streaming, the cache-friendly pattern is cookie-based session authentication - validate the viewer's entitlement once on manifest request, issue a short-lived session cookie, and let segment requests flow through cleanly with shared cache efficiency.

## Related content

- [Improve performance by compressing files in Azure Front Door](./standard-premium/how-to-compression.md)

- [High-availability implementation guide for using Azure Front Door](high-availability.md)

- [Architecture best practices for Azure Front Door](/azure/well-architected/service-guides/azure-front-door?toc=/azure/frontdoor/toc.json)

- [Caching with Azure Front Door](front-door-caching.md)


# Websocket

# Azure Front Door WebSocket

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Azure Front Door supports WebSocket on both Standard and Premium tiers without requiring any extra configurations. WebSocket, standardized in [RFC6455](https://tools.ietf.org/html/rfc6455), is a TCP-based protocol that facilitates full-duplex communication between a server and a client over a long-running TCP connection. It eliminates the need for polling as required in HTTP and avoids some of the overhead of HTTP. It can reuse the same TCP connection for multiple requests or responses, resulting in a more efficient utilization of resources. This enables more interactive and real-time scenarios.

WebSocket is ideal for applications needing real-time updates or continuous data streams, such as chat apps, dashboards, financial updates, GPS, online education, live streaming, and gaming. For instance, a trading website can use WebSocket to push and update pricing data in real-time.

> [!Note]

> Front Door does not support Server-Sent Events (SSE).

## Use WebSocket on Azure Front Door

When using WebSocket on Azure Front Door, consider the following:

- Once a connection is upgraded to WebSocket, Azure Front Door transmits data between clients and the origin server without performing any inspections or manipulations during the established connection.

- Web Application Firewall (WAF) inspections are applied during the WebSocket establishment phase. After the connection is established, the WAF doesn't perform further inspections.

- Health probes to origins are conducted using the HTTP protocol.

- Disable caching for WebSocket routes. For routes with caching enabled, Azure Front Door doesn't forward the WebSocket Upgrade header to the origin and treats it as an HTTP request, disregarding cache rules. This results in a failed WebSocket upgrade request.

- The idle timeout is 5 minutes. If Azure Front Door doesn't detect any data transmission from the origin or the client within the past 5 minutes, the connection is considered idle and is closed.

- Currently, WebSocket connections on Azure Front Door remain open for no longer than 4 hours. The WebSocket connection can be dropped due to underlying server upgrades or other maintenance activities. We highly recommend you implement retry logic in your application.

- Currently, each Azure Front Door profile supports up to 3,000 concurrent global connections. For more information, see [Azure Front Door Standard and Premium service limits](../../azure-resource-manager/management/azure-subscription-service-limits.md#azure-front-door-standard-and-premium-service-limits).

## How the WebSocket protocol works

WebSocket protocols use port 80 for standard WebSocket connections and port 443 for WebSocket connections over TLS/SSL. As a stateful protocol, the connection between clients and the server remains active until terminated by either party. WebSocket connections begin as an HTTP Upgrade request with the `ws:` or `wss:` scheme. These connections are established by upgrading an HTTP request/response using the `Connection: Upgrade`, `Upgrade: websocket`, `Sec-WebSocket-Key`, and `Sec-WebSocket-Version` headers, as shown in the request header examples.

The handshake from the client looks as follows:

```

GET /chat HTTP/1.1

Host: server.example.com

Upgrade: websocket

Connection: Upgrade

Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==

Origin: http://example.com

Sec-WebSocket-Protocol: chat, superchat

Sec-WebSocket-Version: 13

```

The server responds with a `101 Switching Protocols` status code to indicate that it's switching to the WebSocket protocol as requested by the client. The response includes the `Connection: Upgrade` and `Upgrade: websocket` headers, confirming the protocol switch. The `Sec-WebSocket-Accept` header is returned to validate that the connection was successfully upgraded.

The handshake from the server looks as follows:

```

HTTP/1.1 101 Switching Protocols

Upgrade: websocket

Connection: Upgrade

Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=

Sec-WebSocket-Protocol: chat

```

After the client receives the server response, the WebSocket connection is open to start transmitting data. If the WebSocket connection gets disconnected by the client or server, or by a network disruption, the client application is expected to reinitiate the connection with the server.

## Next steps

- Learn how to [create an Azure Front Door](../create-front-door-portal.md) profile.

- Learn how Azure Front Door [routes traffic](../front-door-routing-architecture.md) to your origin.


# Front Door Http2

# HTTP/2 support in Azure Front Door

Currently, HTTP/2 support is enabled for all Azure Front Door configurations, requiring no extra actions.

HTTP/2 is a significant update to HTTP/1.1, offering faster web performance by reducing response times. It retains the familiar HTTP methods, status codes, and semantics of HTTP/1.1 to enhance user experience. Although HTTP/2 works with both HTTP and HTTPS, many web browsers only support HTTP/2 over Transport Layer Security (TLS).

> [!NOTE]

> HTTP/2 protocol support is available only for requests from clients to Front Door. Communication from Front Door to back ends in the back-end pool uses HTTP/1.1.

### Benefits of HTTP/2

HTTP/2 offers several benefits:

* **Multiplexing and concurrency**: Unlike HTTP/1.1, which requires multiple TCP connections for multiple resource requests, HTTP/2 allows multiple resources to be requested over a single TCP connection, reducing performance costs.

* **Header compression**: Compressing HTTP headers for served resources reduces the amount of data sent over the network.

* **Stream dependencies**: Clients can indicate resource priorities to the server, optimizing resource loading.

## Browser Support for HTTP/2

All major browsers support HTTP/2 in their current versions. Browsers that don't support HTTP/2 automatically revert to HTTP/1.1.

| Browser         | Minimum Version |

|-----------------|-----------------|

| Microsoft Edge  | 12              |

| Google Chrome   | 43              |

| Mozilla Firefox | 38              |

| Opera           | 32              |

| Safari          | 9               |

## Next Steps

To learn more about HTTP/2, visit the following resources:

- [HTTP/2 specification homepage](https://http2.github.io/)

- [Official HTTP/2 FAQ](https://http2.github.io/faq/)

- Learn how to [create a Front Door](quickstart-create-front-door.md)

- Learn [how Front Door works](front-door-routing-architecture.md)


# Blue Green Deployment

# Blue/Green Deployments Using Azure Front Door

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium :heavy_check_mark: Front Door (classic)

*Blue/Green deployment* is a software release strategy that gradually introduces application updates to a small group of users. If the updates are successful, the number of users accessing the new deployment is gradually increased until all users are on the new version. If issues arise, traffic can be redirected to the old version, ensuring minimal disruption. This approach is safer than deploying updates to all users at once.

Azure Front Door is Microsoft's modern cloud Content Delivery Network (CDN) that offers fast, reliable, and secure access to your application's static and dynamic web content globally. This article explains how to use Azure Front Door's global load balancing capabilities to implement a blue/green deployment model for your backends.

## Prerequisites

* An Azure subscription. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Create an Azure Front Door profile

1. Sign in to the [Azure portal](https://portal.azure.com/?WT.mc_id=A261C142F).

1. Select **Create a resource** from the home page, search for *Front Door and CDN profiles*, and select **Create**.

1. Select **Custom create** on the *Compare offerings* page, and then select **Continue to create a Front Door**.

1. On the **Basics** tab, enter or select the following information:

| Settings | Values |

|--|--|

| Subscription | Select your subscription. |

| Resource group | Select **Create new** and enter `myAFDResourceGroup`. |

| Resource group location | Select **East US**. |

| Name | Enter a unique name for your Front Door profile. |

| Tier | Select **Standard**. |

1. Select the **Endpoints** tab, and then select **Add endpoint**. Enter a globally unique name for your endpoint, and then select **Add**. You can create more endpoints after the deployment.

1. Select **+ Add a route** to configure routing to your Web App origin.

1. Provide a name for the route and configure the route settings based on the needs of your application. For more information, see [Create a Front Door for your application](create-front-door-portal.md#create-a-front-door-for-your-application).

1. To create a new origin group, select **Add a new origin group** and enter `myOriginGroup` as the name.

1. Select **+ Add** to add an origin to the origin group. Enter the following information for the existing version of the application:

| Settings | Values |

|--|--|

| Name | Enter `CurrentWebApp`. |

| Origin type | Select *App Service* from the dropdown. |

| Hostname | Enter the hostname of your Web App, for example, `webapp-current.azurewebsites.net`. |

| Priority | Enter `1`. |

| Weight | Enter `75`. |

| Status | Select the check box for **Enable this origin**. |

1. Select **+ Add** to add another origin to the origin group. Enter the following information for the new version of the application:

| Settings | Values |

|--|--|

| Name | Enter `NewWebApp`. |

| Origin type | Select *App Service* from the dropdown. |

| Hostname | Enter the hostname of your Web App, for example, `webapp-new.azurewebsites.net`. |

| Priority | Enter `1`. |

| Weight | Enter `25`. |

| Status | Leave **Enable this origin** unchecked. |

> [!NOTE]

> Initially, set the weight of the current origin higher than the new origin to ensure most traffic is routed to the current origin. Gradually increase the weight of the new origin and decrease the weight of the current origin as you test. The total weight doesn't need to be 100, but it helps visualize traffic distribution. The example sets the existing origin to receive three times as much traffic as the new origin.

1. Enable session affinity if your application requires it. For more information, see [Session affinity](routing-methods.md).

> [!NOTE]

> *Session affinity* ensures the end user is routed to the same origin after the first request. Enable this feature based on your application and the type of enhancements being rolled out. For major revisions, enable session affinity to keep users on the new codebase. For minor enhancements, you can leave session affinity disabled. When in doubt, enable session affinity.

1. Health probe settings can be left at the default values. Adjust the probe settings based on your application's needs. For more information, see [Health probes](health-probes.md).

1. Under **Load balancing settings**, enter the following information:

| Settings | Values |

|--|--|

| Sample size | Enter `4`. |

| Successful samples required | Enter `3`. |

| Latency sensitivity (in milliseconds) | Enter `500`. |

> [!NOTE]

> Set the latency sensitivity to 500 milliseconds (half a second) or higher to ensure both origins are used, as one origin might be faster than the other.

1. Select **Add** to add the origin group. Then select **Review + create** to review the settings of your Front Door profile. Select **Create** to create the profile.

## Start Blue/Green Deployment

To begin the blue/green deployment, enable the new origin to start routing traffic to it while retaining the option to revert to the old origin if necessary.

1. Once the Front Door profile is created, navigate to the origin group you set up earlier. Select the new origin and check **Enable this origin** to start routing traffic to it.

1. Monitor the new origin to ensure it functions correctly. Gradually increase the weight of the new origin while decreasing the weight of the old origin as you gain confidence in the new origin's performance. Continue adjusting the weights until all traffic is routed to the new origin.

1. If any issues arise with the new origin, disable it to route all traffic back to the old origin. This allows you to address and resolve issues without affecting users.

## Next steps

[Secure traffic to your Azure Front Door origins](origin-security.md)


# Monitor Front Door

# Monitor Azure Front Door

[!INCLUDE [azmon-horz-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-intro.md)]

[Reports](standard-premium/how-to-reports.md) provide insight into how your traffic flows through Azure Front Door, the web application firewall (WAF), and to your application.

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

## Collect data with Azure Monitor

This table describes how you can collect data to monitor your service, and what you can do with the data once collected:

|Data to collect|Description|How to collect and route the data|Where to view the data|Supported data|

|---------|---------|---------|---------|---------|

|Metric data|Metrics are numerical values that describe an aspect of a system at a particular point in time. You can aggregate metrics by using algorithms, compare them to other metrics, and analyze them for trends over time.|- Collected automatically at regular intervals.</br>- You can route some platform metrics to a Log Analytics workspace to query with other data. Check the **DS export** setting for each metric to see if you can use a diagnostic setting to route the metric data.|[Metrics explorer](/azure/azure-monitor/essentials/metrics-getting-started)| [Azure Front Door metrics supported by Azure Monitor](monitor-front-door-reference.md#metrics)|

|Resource log data|Logs are recorded system events with a timestamp. Logs can contain different types of data, and be structured or free-form text. You can route resource log data to Log Analytics workspaces for querying and analysis.|[Create a diagnostic setting](/azure/azure-monitor/essentials/create-diagnostic-settings) to collect and route resource log data.| [Log Analytics](/azure/azure-monitor/learn/quick-create-workspace)|[Azure Front Door resource log data supported by Azure Monitor](monitor-front-door-reference.md#resource-logs)  |

|Activity log data|The Azure Monitor activity log provides insight into subscription-level events. The activity log includes information like when a resource is modified or a virtual machine is started.|- Collected automatically.</br>- [Create a diagnostic setting](/azure/azure-monitor/essentials/create-diagnostic-settings) to a Log Analytics workspace at no charge.|[Activity log](/azure/azure-monitor/essentials/activity-log)|  |

[!INCLUDE [azmon-horz-supported-data](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-supported-data.md)]

## Built-in monitoring for Azure Front Door

Logs track all requests that pass through Azure Front Door. It can take a few minutes for the system to process and store logs.

There are multiple Front Door logs, which you can use for different purposes:

- [Access logs](#access-log) can be used to identify slow requests, determine error rates, and understand how Front Door's caching behavior is working for your solution.

- Web application firewall (WAF) logs can be used to detect potential attacks, and false positive detections that might indicate legitimate requests that the WAF blocked. For more information on the WAF logs, see [Azure Web Application Firewall monitoring and logging](../web-application-firewall/afds/waf-front-door-monitor.md).

- [Health probe logs](#health-probe-log) can be used to identify origins that are unhealthy or that don't respond to requests from some of Front Door's geographically distributed PoPs.

- Activity logs provide visibility into the operations performed on your Azure resources, such as configuration changes to your Azure Front Door profile.

Access logs and WAF logs include a *tracking reference*, which is also propagated in requests to origins and to client responses by using the `X-Azure-Ref` header. You can use the tracking reference to gain an end-to-end view of your application request processing.

Access logs, health probe logs, and WAF logs aren't enabled by default. To enable and store your diagnostic logs, see [Configure Azure Front Door logs](./standard-premium/how-to-logs.md). Activity log entries are collected by default, and you can view them in the Azure portal.

### <a name="access-log"></a>Access log

The access log records information about every request. Each access log entry contains the information listed in the following table.

| Property | Description |

|----------|-------------|

| TrackingReference | The unique reference string that identifies a request served by Azure Front Door. The `X-Azure-Ref` headers send the tracking reference to the client and to the origin. Use the tracking reference when searching for a specific request in the access or WAF logs. |

| Time | The date and time when the Azure Front Door edge delivered requested contents to client (in UTC). For WebSocket connections, the time represents when the connection gets closed. |

| HttpMethod | HTTP method used by the request: DELETE, GET, HEAD, OPTIONS, PATCH, POST, or PUT. |

| HttpVersion | The HTTP version that the client specified in the request. |

| RequestUri | The URI of the received request. This field contains the full scheme, port, domain, path, and query string. |

| HostName | The host name in the request from client. If you enable custom domains and have wildcard domain (`*.contoso.com`), the HostName log field's value is `subdomain-from-client-request.contoso.com`. If you use the Azure Front Door domain (`contoso-123.z01.azurefd.net`), the HostName log field's value is `contoso-123.z01.azurefd.net`. |

| RequestBytes | The size of the HTTP request message in bytes, including the request headers and the request body. For WebSocket connections, this value is the total number of bytes sent from the client to the server through the connection.|

| ResponseBytes | The size of the HTTP response message in bytes. For WebSocket connections, this value is the total number of bytes sent from the server to the client through the connection.|

| UserAgent | The user agent that the client used. Typically, the user agent identifies the browser type. |

| ClientIp | The IP address of the client that made the original request. If the request includes an `X-Forwarded-For` header, the client IP address comes from the header. |

| SocketIp | The IP address of the direct connection to the Azure Front Door edge. If the client used an HTTP proxy or a load balancer to send the request, the value of SocketIp is the IP address of the proxy or load balancer. |

| TimeTaken | The duration from when the Azure Front Door edge received the client's request to when the last byte of the response was sent to the client, measured in seconds. This metric excludes network latency and TCP buffering. For WebSocket connections, it represents the connection duration from establishment to closure. |

| RequestProtocol | The protocol specified by the client in the request. Possible values include: **HTTP**, **HTTPS**. For WebSocket, the protocols are **WS**, **WSS**. Only requests that successfully upgrade to WebSocket have WS/WSS. |

| SecurityProtocol | The TLS/SSL protocol version used by the request, or null if the request didn't use encryption. Possible values include: **SSLv3**, **TLSv1**, **TLSv1.1**, **TLSv1.2**. |

| SecurityCipher | When the value for the request protocol is HTTPS, this field indicates the TLS/SSL cipher negotiated by the client and Azure Front Door. |

| Endpoint | The domain name of the Azure Front Door endpoint, such as `contoso-123.z01.azurefd.net`. |

| HttpStatusCode | The HTTP status code returned from Azure Front Door. If the request to the origin timed out, the value for the HttpStatusCode field is **0**. If the client closed the connection, the value for the HttpStatusCode field is **499**. |

| Pop | The Azure Front Door edge point of presence (PoP) that responded to the user request.  |

| Cache Status | How the Azure Front Door cache handles the request. Possible values are: <ul><li>**HIT** and **REMOTE_HIT**: The HTTP request was served from the Azure Front Door cache.</li><li>**MISS**: The HTTP request was served from origin. </li><li> **PARTIAL_HIT**: Some of the bytes were served from the Front Door edge PoP cache, and other bytes were served from the origin. This status indicates an [object chunking](./front-door-caching.md#delivery-of-large-files) scenario. </li><li> **CACHE_NOCONFIG**: The request was forwarded without caching settings, including bypass scenarios. </li><li> **PRIVATE_NOSTORE**: There was no cache configured in the caching settings by the customer. </li><li> **N/A**: A signed URL or WAF rule denied the request.</li></ul> |

| MatchedRulesSetName | The names of the Rules Engine rules that were processed. |

| RouteName | The name of the route that the request matched. |

| ClientPort | The IP port of the client that made the request. |

| SslJA4 | TLS Client Hello fingerprint, enabling identification of client applications and detection of anomalous or malicious traffic patterns across encrypted connections. |

| Referrer | The URL of the site that originated the request. |

| TimetoFirstByte | The length of time, in seconds, from when the Azure Front Door edge received the request to the time the first byte was sent to client, as measured by Azure Front Door. This property doesn't measure the client data. |

| ErrorInfo | If an error occurred during the processing of the request, this field provides detailed information about the error. Possible values are: <ul><li> **NoError**: Indicates no error was found. </li><li> **CertificateError**: Generic SSL certificate error. </li><li> **CertificateNameCheckFailed**: The host name in the SSL certificate is invalid or doesn't match the requested URL. </li><li> **ClientDisconnected**: The request failed because of a client network connection issue. </li><li> **ClientGeoBlocked**: The client was blocked due to the geographical location of the IP address. </li><li> **UnspecifiedClientError**: Generic client error. </li><li> **InvalidRequest**: Invalid request. This response indicates a malformed header, body, or URL. </li><li> **DNSFailure**: A failure occurred during DNS resolution. </li><li> **DNSTimeout**: The DNS query to resolve the origin IP address timed out. </li><li> **DNSNameNotResolved**: The server name or address couldn't be resolved. </li><li> **OriginConnectionAborted**: The connection with the origin was disconnected abnormally. </li><li> **OriginConnectionError**: Generic origin connection error. </li><li> **OriginConnectionRefused**: The connection with the origin wasn't established. </li><li> **OriginError**: Generic origin error. </li><li> **ResponseHeaderTooBig**: The origin returned a too large of a response header. </li><li> **OriginInvalidResponse**: The origin returned an invalid or unrecognized response. </li><li> **OriginTimeout**: The time-out period for the origin request expired. </li><li> **ResponseHeaderTooBig**: The origin returned a too large of a response header. </li><li> **RestrictedIP**: The request was blocked because of restricted IP address. </li><li> **SSLHandshakeError**: Azure Front Door was unable to establish a connection with the origin because of an SSL handshake failure. </li><li> **SSLInvalidRootCA**: The root certification authority's certificate was invalid. </li><li> **SSLInvalidCipher**: The HTTPS connection was established using an invalid cipher. </li><li> **OriginConnectionAborted**: The connection with the origin was disconnected abnormally. </li><li> **OriginConnectionRefused**: The connection with the origin wasn't established. </li><li> **UnspecifiedError**: An error occurred that didn’t fit in any of the errors in the table. </li></ul> |

| OriginURL | The full URL of the origin where the request was sent. The URL is composed of the scheme, host header, port, path, and query string. <br> **URL rewrite**: If the Rules Engine rewrites the request URL, the path refers to the rewritten path. <br> **Cache on edge PoP**: If the request was served from the Azure Front Door cache, the origin is **N/A**. <br> **Large request**: If the requested content is large and there are multiple chunked requests going back to the origin, this field corresponds to the first request to the origin. For more information, see [Object Chunking](./front-door-caching.md#delivery-of-large-files). |

| OriginIP | The IP address of the origin that served the request. <br> **Cache on edge PoP**: If the request was served from the Azure Front Door cache, the origin is **N/A**. <br> **Large request**: If the requested content is large and there are multiple chunked requests going back to the origin, this field corresponds to the first request to the origin. For more information, see [Object Chunking](./front-door-caching.md#delivery-of-large-files). |

| OriginName| The full hostname (DNS name) of the origin. <br> **Cache on edge PoP**: If the request was served from the Azure Front Door cache, the origin is **N/A**. <br> **Large request**: If the requested content is large and there are multiple chunked requests going back to the origin, this field corresponds to the first request to the origin. For more information, see [Object Chunking](./front-door-caching.md#delivery-of-large-files). |

| Result | `SSLMismatchedSNI` is a status code that signifies a successful request with a mismatch warning between the SNI and the host header. This status code implies domain fronting, a technique that violates Azure Front Door’s terms of service. Requests with `SSLMismatchedSNI` are rejected after January 22, 2024.|

| Sni | This field specifies the Server Name Indication (SNI) that is sent during the TLS/SSL handshake. It can be used to identify the exact SNI value if there was a `SSLMismatchedSNI` status code. Additionally, it can be compared with the host value in the `requestUri` field to detect and resolve the mismatch issue. |

### Health probe log

Azure Front Door logs every failed health probe request. These logs can help you diagnose problems with an origin. Use the logs to investigate the failure reason and then bring the origin back to a healthy status.

Some scenarios where this log can be useful include:

- You notice Azure Front Door traffic is sent to a subset of the origins. For example, you might notice that only three out of four origins receive traffic. You want to know if the origins are receiving and responding to health probes so you know whether the origins are healthy.

- You notice the origin health percentage metric is lower than you expected. You want to know which origins are recorded as unhealthy and the reason for the health probe failures.

Each health probe log entry has the following schema:

| Property | Description |

| --- | --- |

| HealthProbeId  | A unique ID to identify the health probe request. |

| Time | The date and time when the health probe was sent (in UTC). |

| HttpMethod | The HTTP method used by the health probe request. Values include **GET** and **HEAD**, based on the health probe's configuration. |

| Result | The status of health probe. The value is either **success** or a description of the error the probe received. |

| HttpStatusCode  | The HTTP status code returned by the origin. |

| ProbeURL | The full target URL to where the probe request was sent. The URL is composed of the scheme, host header, path, and query string. |

| OriginName  | The name of the origin that the health probe was sent to. This field helps you locate origins of interest if origin is configured to use an FQDN. |

| POP | The edge PoP that sent the probe request. |

| Origin IP | The IP address of the origin that the health probe was sent to. |

| TotalLatency | The time from when the Azure Front Door edge sent the health probe request to the origin to when the origin sent the last response to Azure Front Door. |

| ConnectionLatency| The time spent setting up the TCP connection to send the HTTP probe request to the origin. |

| DNSResolution Latency | The time spent on DNS resolution. This field only has a value if the origin is configured to be an FQDN instead of an IP address. If the origin is configured to use an IP address, the value is **N/A**. |

The following example JSON snippet shows a health probe log entry for a failed health probe request.

```json

{

"records": [

{

"time": "2021-02-02T07:15:37.3640748Z",

"resourceId": "/SUBSCRIPTIONS/mySubscriptionID/RESOURCEGROUPS/myResourceGroup/PROVIDERS/MICROSOFT.CDN/PROFILES/MyProfile",

"category": "FrontDoorHealthProbeLog",

"operationName": "Microsoft.Cdn/Profiles/FrontDoorHealthProbeLog/Write",

"properties": {

"healthProbeId": "9642AEA07BA64675A0A7AD214ACF746E",

"POP": "MAA",

"httpVerb": "HEAD",

"result": "OriginError",

"httpStatusCode": "400",

"probeURL": "http://www.example.com:80/",

"originName": "www.example.com",

"originIP": "PublicI:Port",

"totalLatencyMilliseconds": "141",

"connectionLatencyMilliseconds": "68",

"DNSLatencyMicroseconds": "1814"

}

}

]

}

```

### Web application firewall log

For more information on the Front Door web application firewall (WAF) logs, see [Azure Web Application Firewall monitoring and logging](../web-application-firewall/afds/waf-front-door-monitor.md).

For classic Azure Front Door, built-in monitoring includes diagnostic logs.

### <a name="diagnostic-logging"></a>Diagnostic logs

Diagnostic logs provide rich information about operations and errors that are important for auditing and troubleshooting. Diagnostic logs differ from activity logs.

Activity logs provide insights into the operations done on Azure resources. Diagnostic logs provide insight into operations that your resource does. For more information, see [Azure Monitor diagnostic logs](/azure/azure-monitor/essentials/platform-logs-overview).

To configure diagnostic logs for your Azure Front Door (classic):

1. Select your Azure Front Door (classic) profile.

1. Choose **Diagnostic settings**.

1. Select **Turn on diagnostics**. Archive diagnostic logs along with metrics to a storage account, stream them to an event hub, or send them to Azure Monitor logs.

Front Door currently provides diagnostic logs. Diagnostic logs provide individual API requests with each entry having the following schema:

| Property  | Description |

| ------------- | ------------- |

| BackendHostname | If request was being forwarded to a backend, this field represents the hostname of the backend. This field is blank if the request gets redirected or forwarded to a regional cache (when caching gets enabled for the routing rule). |

| CacheStatus | For caching scenarios, this field defines the cache hit/miss at the POP |

| ClientIp | The IP address of the client that made the request. If there was an X-Forwarded-For header in the request, then the Client IP is picked from the same. |

| ClientPort | The IP port of the client that made the request. |

| HttpMethod | HTTP method used by the request. |

| HttpStatusCode | The HTTP status code returned from the proxy. If a request to the origin times out, the value for HttpStatusCode is set to **0**.|

| HttpStatusDetails | Resulting status on the request. Meaning of this string value can be found at a Status reference table. |

| HttpVersion | Type of the request or connection. |

| POP | Short name of the edge where the request landed. |

| RequestBytes | The size of the HTTP request message in bytes, including the request headers and the request body. |

| RequestUri | URI of the received request. |

| ResponseBytes | Bytes sent by the backend server as the response.  |

| RoutingRuleName | The name of the routing rule that the request matched. |

| RulesEngineMatchNames | The names of the rules that the request matched. |

| SecurityProtocol | The TLS/SSL protocol version used by the request or null if no encryption. |

| SentToOriginShield </br> (deprecated) * **See notes on deprecation in the following section.**| If true, it means that request was answered from origin shield cache instead of the edge pop. Origin shield is a parent cache used to improve cache hit ratio. |

| isReceivedFromClient | If true, it means that the request came from the client. If false, the request is a miss in the edge (child POP) and is responded from origin shield (parent POP). |

| TimeTaken | The length of time from first byte of request into Front Door to last byte of response out, in seconds. |

| TrackingReference | The unique reference string that identifies a request served by Front Door, also sent as X-Azure-Ref header to the client. Required for searching details in the access logs for a specific request. |

| UserAgent | The browser type that the client used. |

| ErrorInfo | This field contains the specific type of error for further troubleshooting. </br>Possible values include: </br>**NoError**: Indicates no error was found. </br>**CertificateError**: Generic SSL certificate error. </br>**CertificateNameCheckFailed**: The host name in the SSL certificate is invalid or doesn't match. </br>**ClientDisconnected**: Request failure because of client network connection. </br>**UnspecifiedClientError**: Generic client error. </br>**InvalidRequest**: Invalid request. It might occur because of malformed header, body, and URL. </br>**DNSFailure**: DNS Failure. </br>**DNSNameNotResolved**: The server name or address couldn't be resolved. </br>**OriginConnectionAborted**: The connection with the origin was stopped abruptly. </br>**OriginConnectionError**: Generic origin connection error. </br>**OriginConnectionRefused**: The connection with the origin wasn't able to established. </br>**OriginError**: Generic origin error. </br>**OriginInvalidResponse**: Origin returned an invalid or unrecognized response. </br>**OriginTimeout**: The time-out period for origin request expired. </br>**ResponseHeaderTooBig**: The origin returned too large of a response header. </br>**RestrictedIP**: The request was blocked because of restricted IP. </br>**SSLHandshakeError**: Unable to establish connection with origin because of SSL hand shake failure. </br>**UnspecifiedError**: An error occurred that didn’t fit in any of the errors in the table. </br>**SSLMismatchedSNI**: The request was invalid because the HTTP message header didn't match the value presented in the TLS SNI extension during SSL/TLS connection setup.|

| Result | `SSLMismatchedSNI` is a status code that signifies a successful request with a mismatch warning between the SNI and the host header. This status code implies domain fronting, a technique that violates Azure Front Door’s terms of service. Requests with `SSLMismatchedSNI` are rejected after January 22, 2024.|

| Sni | This field specifies the Server Name Indication (SNI) that is sent during the TLS/SSL handshake. It can be used to identify the exact SNI value if there was a `SSLMismatchedSNI` status code. Additionally, it can be compared with the host value in the `requestUri` field to detect and resolve the mismatch issue. |

#### Sent to origin shield deprecation

The raw log property **isSentToOriginShield** is deprecated and replaced by a new field **isReceivedFromClient**. Use the new field if you're already using the deprecated field.

Raw logs include logs generated from both CDN edge (child POP) and origin shield. Origin shield refers to parent nodes that are strategically located across the globe. These nodes communicate with origin servers and reduce the traffic load on origin.

For every request that goes to an origin shield, there are two log entries:

- One for edge nodes

- One for origin shield

To differentiate the egress or responses from the edge nodes vs. origin shield, you can use the field **isReceivedFromClient** to get the correct data.

If the value is false, then it means the request is responded from origin shield to edge nodes. This approach is effective to compare raw logs with billing data. Charges aren't incurred for egress from origin shield to the edge nodes. Charges are incurred for egress from the edge nodes to clients.

**Kusto query sample to exclude logs generated on origin shield in Log Analytics.**

`AzureDiagnostics

| where Category == "FrontdoorAccessLog" and isReceivedFromClient_b == true`

> [!NOTE]

> For various routing configurations and traffic behaviors, some fields like `backendHostname`, `cacheStatus`, `isReceivedFromClient`, and `POP` might return different values. The following table explains the different values these fields have for various scenarios:

| Scenarios | Count of log entries | POP | BackendHostname | isReceivedFromClient | CacheStatus |

| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |

| Routing rule without caching enabled | 1 | Edge POP code | Backend where request was forwarded | True | CONFIG_NOCACHE |

| Routing rule with caching enabled. Cache hit at the edge POP | 1 | Edge POP code | Empty | True | HIT |

| Routing rule with caching enabled. Cache misses at edge POP but cache hit at parent cache POP | 2 | 1. Edge POP code</br>2. Parent cache POP code | 1. Parent cache POP hostname</br>2. Empty | 1. True</br>2. False | 1. MISS</br>2. HIT |

| Routing rule with caching enabled. Cache misses at edge POP but PARTIAL cache hit at parent cache POP | 2 | 1. Edge POP code</br>2. Parent cache POP code | 1. Parent cache POP hostname</br>2. Backend that helps populate cache | 1. True</br>2. False | 1. MISS</br>2. PARTIAL_HIT |

| Routing rule with caching enabled. Cache PARTIAL_HIT at edge POP but cache hit at parent cache POP | 2 | 1. Edge POP code</br>2. Parent cache POP code | 1. Edge POP code</br>2. Parent cache POP code | 1. True</br>2. False | 1. PARTIAL_HIT</br>2. HIT |

| Routing rule with caching enabled. Cache misses at both edge and parent cache POP | 2 | 1. Edge POP code</br>2. Parent cache POP code | 1. Edge POP code</br>2. Parent cache POP code | 1. True</br>2. False | 1. MISS</br>2. MISS |

| Error processing the request |  |  |  |  | N/A |

> [!NOTE]

> For caching scenarios, the value for `CacheStatus` is a `PARTIAL_HIT` when some of the bytes for a request come from the Azure Front Door edge or origin shield cache while some of the bytes come from the origin for large objects.

Azure Front Door uses a technique called object chunking. When a large file is requested, Azure Front Door retrieves smaller pieces of the file from the origin. After the Azure Front Door POP server receives a full or byte-ranges of the file requested, the Azure Front Door edge server requests the file from the origin in chunks of 8 MB.

After the chunk arrives at the Azure Front Door edge, it's cached and immediately served to the user. The Azure Front Door then prefetches the next chunk in parallel. This prefetch ensures the content stays one chunk ahead of the user, which reduces latency. This process continues until the entire file gets downloaded (if requested), all byte ranges are available (if requested), or the client closes the connection. For more information on the byte-range request, see RFC 7233. The Azure Front Door caches any chunks as they're received. The entire file doesn't need to be cached on the Front Door cache. Ensuing requests for the file or byte ranges are served from the Azure Front Door cache. If not all the chunks are cached on the Azure Front Door, prefetch is used to request chunks from the origin. This optimization relies on the ability of the origin server to support byte-range requests. If the origin server doesn't support byte-range requests, this optimization isn't effective.

[!INCLUDE [azmon-horz-tools](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-tools.md)]

[!INCLUDE [azmon-horz-export-data](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-export-data.md)]

[!INCLUDE [azmon-horz-kusto](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-kusto.md)]

[!INCLUDE [azmon-horz-alerts-part-one](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-alerts-part-one.md)]

[!INCLUDE [azmon-horz-alerts-part-two](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-alerts-part-two.md)]

[!INCLUDE [azmon-horz-advisor](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-advisor.md)]

## Related content

- [Azure Front Door monitoring data reference](monitor-front-door-reference.md)

- [Monitoring Azure resources with Azure Monitor](/azure/azure-monitor/essentials/monitor-azure-resource)


# Monitor Front Door Reference

# Azure Front Door monitoring data reference

[!INCLUDE [horz-monitor-ref-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-intro.md)]

See [Monitor Azure Front Door](monitor-front-door.md) for details on the data you can collect for Azure Front Door and how to use it.

[!INCLUDE [horz-monitor-ref-metrics-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-intro.md)]

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

### Supported metrics for Microsoft.Network/frontdoors

The following table lists the metrics available for the Microsoft.Network/frontdoors resource type.

[!INCLUDE [horz-monitor-ref-metrics-tableheader](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-tableheader.md)]

[!INCLUDE [Microsoft.Network/frontdoors](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/metrics/microsoft-network-frontdoors-metrics-include.md)]

### Supported metrics for Microsoft.Cdn/profiles

The following table lists the metrics available for the Microsoft.Cdn/profiles resource type.

[!INCLUDE [horz-monitor-ref-metrics-tableheader](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-tableheader.md)]

[!INCLUDE [Microsoft.Cdn/profiles](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/metrics/microsoft-cdn-profiles-metrics-include.md)]

> [!NOTE]

> The metrics are recorded and stored free of charge for a limited period of time. For an extra cost, you can store for a longer period of time.

The following table provides more detailed descriptions for the metrics.

| Metrics | Description |

|:--|:--|

| Byte Hit Ratio | The percentage of traffic that was served from the Azure Front Door cache, computed against the total egress traffic. The byte hit ratio is  low if most of the traffic is forwarded to the origin rather than served from the cache. <br/><br/> **Byte Hit Ratio** = (egress from edge - egress from origin)/egress from edge. <br/><br/> Scenarios excluded from bytes hit ratio calculations:<ul><li>You explicitly disable caching, either through the Rules Engine or query string caching behavior.</li><li>You explicitly configure a `Cache-Control` directive with the `no-store` or `private` cache directives.</li></ul> |

| Origin Health Percentage | The percentage of successful health probes sent from Azure Front Door to origins. |

| Origin Latency | Azure Front Door calculates the time from sending the request to the origin to receiving the last response byte from the origin. WebSocket is excluded from the origin latency.|

| Origin Request Count | The number of requests sent from Azure Front Door to origins. |

| Percentage of 4XX | The percentage of all the client requests for which the response status code is 4XX. |

| Percentage of 5XX | The percentage of all the client requests for which the response status code is 5XX. |

| Request Count | The number of client requests served through Azure Front Door, including requests served entirely from the cache. |

| Request Size | The number of bytes sent in requests from clients to Azure Front Door. |

| Response Size | The number of bytes sent as responses from Front Door to clients. |

| Total Latency | Azure Front Door receives the client request and sends the last response byte to the client. This value is the total time taken. For WebSocket, this metric refers to the time it takes to establish the WebSocket connection. |

| Web Application Firewall Request Count | The number of requests processed by the Azure Front Door web application firewall. |

> [!NOTE]

> If a request to the origin times out, the value of the *Http Status* dimension is **0**.

[!INCLUDE [horz-monitor-ref-metrics-dimensions-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-dimensions-intro.md)]

[!INCLUDE [horz-monitor-ref-metrics-dimensions](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-dimensions.md)]

- Action

- Backend

- BackendPool

- ClientCountry

- ClientRegion

- HttpStatus

- HttpStatusGroup

- PolicyName

- RuleName

- Action

- ClientCountry

- ClientRegion

- Endpoint

- HttpStatus

- HttpStatusGroup

- Origin

- OriginGroup

- PolicyName

- RuleName

[!INCLUDE [horz-monitor-ref-resource-logs](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-resource-logs.md)]

### Supported resource logs for Microsoft.Network/frontdoors

[!INCLUDE [Microsoft.Network/frontdoors](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/logs/microsoft-network-frontdoors-logs-include.md)]

### Supported resource logs for Microsoft.Cdn/profiles

[!INCLUDE [Microsoft.Cdn/profiles](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/logs/microsoft-cdn-profiles-logs-include.md)]

### Supported resource logs for Microsoft.Cdn/profiles/endpoints

[!INCLUDE [Microsoft.Cdn/profiles/endpoints](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/logs/microsoft-cdn-profiles-endpoints-logs-include.md)]

[!INCLUDE [horz-monitor-ref-logs-tables](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-logs-tables.md)]

### Azure Front Door Microsoft.Network/frontdoors

- [AzureActivity](/azure/azure-monitor/reference/tables/azureactivity#columns)

- [AzureMetrics](/azure/azure-monitor/reference/tables/azuremetrics#columns)

- [AzureDiagnostics](/azure/azure-monitor/reference/tables/azurediagnostics#columns)

### Azure Front Door Microsoft.Cdn/profiles

- [AzureActivity](/azure/azure-monitor/reference/tables/azureactivity#columns)

- [AzureDiagnostics](/azure/azure-monitor/reference/tables/azurediagnostics#columns)

[!INCLUDE [horz-monitor-ref-activity-log](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-activity-log.md)]

- [Microsoft.Network resource provider operations](/azure/role-based-access-control/resource-provider-operations#microsoftnetwork)

- [Microsoft.Cdn resource provider operations](/azure/role-based-access-control/resource-provider-operations#networking)

## Related content

- See [Monitor Azure Front Door](monitor-front-door.md) for a description of monitoring Azure Front Door.

- See [Monitor Azure resources with Azure Monitor](/azure/azure-monitor/essentials/monitor-azure-resource) for details on monitoring Azure resources.


# Compare Cdn Front Door Price

# Compare the pricing of Azure CDN Standard Microsoft and Azure Front Door

**Applies to:** :heavy_check_mark: CDN Standard from Microsoft (classic)

> [!IMPORTANT]

> Azure CDN Standard from Microsoft (Classic) doesn't support profile creation, new domain onboarding, or managed certificates and retires on **September 30, 2027**. To avoid service disruption, ⁠[**migrate to Azure Front Door Standard or Premium**](/azure/cdn/migrate-tier). For more information, see ⁠[**Azure CDN Standard from Microsoft (classic) retirement**](https://azure.microsoft.com/updates?id=Azure-CDN-Standard-from-Microsoft-classic-will-be-retired-on-30-September-2027).

> [!NOTE]

> The prices presented in this article serve as examples and are intended solely for illustration purposes. For region-specific pricing information, see the pricing pages of [Azure Front Door](https://azure.microsoft.com/pricing/details/frontdoor/) and [Azure CDN](https://azure.microsoft.com/pricing/details/cdn).

This article provides a comparative analysis of the pricing structure for Azure CDN Standard Microsoft (classic) and Azure Front Door. Conduct a cost analysis before migrating from Azure CDN Standard Microsoft (classic) to Azure Front Door to understand the pricing differences between the tiers.

## Pricing model comparison

| Pricing Dimensions | Azure CDN Standard from Microsoft (Classic) | Azure Front Door Standard | Azure Front Door Premium |

|--|--|--|--|

| Monthly base fees | Not applicable | $35 | $330 |

| Outbound data transfer (Edge location to client, per GB) | Varies (5 Zones) | Varies (8 Zones) | Identical to Azure Front Door Standard |

| Outbound data transfer (Edge to Origin, per GB) | Free | Varies (8 Zones) | Identical to Azure Front Door Standard |

| Incoming requests (Client to Front Door’s Edge location, per 10,000 requests) | Free | Varies (8 Zones) | Varies (8 Zones, higher unit rate than standard) |

| Rules Engine - Rules | First five rules free, additional rules at $1 per rule per month | Free | Free |

| Rules Engine – Requests processed | $0.60 per million requests | Free | Free |

| Data transfer (Origin in Azure data center to Front Door's edge location) | Free | Free | Free |

| Web Application Firewall custom rules | $5/Month/Policy, $1/Month & $0.06 per million requests (For more information, see [Azure Web Application Firewall pricing](https://azure.microsoft.com/pricing/details/web-application-firewall/)) | Free | Free |

| Web Application Firewall managed rules | $5/Month/Policy, $20/Month + $1 per Million Requests (For more information, see [Azure Web Application Firewall pricing](https://azure.microsoft.com/pricing/details/web-application-firewall/)) | Not supported | Free |

| Private Link to origin | Not supported | Not supported | Free |

## Cost assessment

> [!NOTE]

> For workloads with a high volume of requests, estimate the impact of the request meter for the new tiers. If you're operating multiple Azure CDN instances, assess the impact of the base fee associated with the new tiers.

The following steps provide a general guide for obtaining the necessary metrics to estimate cost for the new tiers:

1. Retrieve the invoice for the Azure CDN Standard Microsoft (classic) profile to get the monthly charges.

1. Calculate the Azure Front Door pricing using the following table:

| Azure Front Door meter | Method to calculate from Azure CDN Standard Microsoft (classic) metrics |

|--|--|

| Base fee | - If managed WAF rules, bot protection, or Private Link are required: **$330/month** </br> - If only custom WAF rules are needed: **$35/month** |

| Requests | <ol><li>Go to your Azure CDN Standard Microsoft (classic) profile, and under *Monitor*, select **Metrics** from the left side menu pane.</li><li>Select the **Request Count** from the *Metrics* drop-down menu.</li><li>To view regional metrics, apply a split to the data by selecting **Client Country** or **Client Region**.</li><li>If you select *Client Country*, map them to the corresponding Azure Front Door pricing zone.</li></ol> |

| Egress from Azure Front Door edge to client | Get this data from your Azure CDN Standard Microsoft (classic) invoice or from the **Response Size** metric in the Azure CDN Standard Microsoft (classic) profile. For a more accurate estimation, apply split by *Client Count* or *Client Region*. |

| Ingress from Azure Front Door edge to origin | This information isn't readily available, but the amount is negligible for caching traffic with high cache hit ratio, such as 95%. |

1. Visit the [pricing calculator](https://azure.microsoft.com/pricing/calculator/?service=frontdoor-standard-premium).

1. Select the appropriate Azure Front Door tier and zone.

1. Compute the total cost for the Azure Front Door profile using the metrics obtained in the previous step.

## Example scenarios

### Scenario 1: A static website with small traffic volume

* 5 TB of outbound data transfer.

* 100 million client-to-edge requests.

* 2.5-GB outbound data transfer from edge to origin (assuming cache hit ratio of 95%).

* Traffic primarily originating from North America.

| Cost factors | Azure CDN Standard Microsoft (classic) | Azure Front Door Standard |

|--|--|--|

| Base fee | $0 | $35 |

| Egress from Azure Front Door edge to client | $405 (calculated as 5 TB * $0.081/GB) | $415 (calculated as 5 TB * $0.083/GB) |

| Egress from Azure Front Door edge to origin | $0 | $0.05 (calculated as 2.5 GB * $0.02/GB) |

| Requests | $0 | $90 (calculated as 100M requests * $0.009/10k requests) |

| Total | $405 | $540.05 |

In this scenario, Azure Front Door Standard is approximately 33% more expensive than Azure CDN Standard from Microsoft (classic) due to extra charges associated with the base fee and requests meter.

### Scenario 2: A static website with medium traffic volume

* 50 TB of outbound data transfer.

* 500 million client-to-edge requests.

* 12.5-GB outbound data transfer from edge to origin (assuming cache hit ratio of 95%).

* Traffic primarily originating from North America.

| Cost factors | Azure CDN Standard Microsoft (classic) | Azure Front Door Standard |

|--|--|--|

| Base fee | $0 | $35 |

| Egress from Azure Front Door edge to client | $3,810  (calculated as (10 TB * $0.081/GB) + (40 TB * $0.075/GB)) | $3,470 (calculated as (10 TB * $0.083/GB) + (40 TB * $0.066/GB)) |

| Egress from Azure Front Door edge to origin | $0 | $0.25 (calculated as 12.5 GB * $0.02/GB) |

| Requests | $0 | $450 (calculated as 500M requests * $0.009/10k requests) |

| Total | $3,810 | $3,955.25 |

In this comparison, Azure Front Door Standard is approximately 4% more expensive than Azure CDN Standard from Microsoft (classic). However, the cost is relatively similar because the reduced egress rate for Azure Front Door Standard (10-50 TB) offsets the extra charges from base fee and requests meter.

### Scenario 3: File downloads - Large volume traffic

* 150 TB of outbound data transfer.

* 1.5 million requests from client to Azure Front Door edge (assuming cache hit ratio of 95%).

* Traffic primarily originating from North America.

| Cost factors | Azure CDN Standard Microsoft (classic) | Azure Front Door Standard |

|--|--|--|

| Base fee | $0 | $35 |

| Egress from Azure Front Door edge to client | $9,410 (calculated as (10 TB * $ 0.081/GB) + (40 TB * $ 0.075/GB) + (100 TB * $ 0.056/GB)) | $9,170 (calculated as (10 TB * $ 0.083/GB) + (40 TB * $ 0.066/GB) + (100 TB * $ 0.057/GB)) |

| Egress from Azure Front Door edge to origin | $0 | $0.8 (calculated as 40 GB * $0.02/GB) |

| Requests | $0 | $1.35 (calculated as 500M requests * $0.009/10k requests) |

| Total | $9,410 | $9,207.15 |

In comparison, Azure CDN Standard from Microsoft (classic) is 2% more expensive than Azure Front Door Standard. This difference comes from the lower egress rate for Azure Front Door Standard for the 10-50 TB range.

### Scenario 4: A static website with medium traffic volume and rules engine enabled

* 50 TB of outbound data transfer.

* 500 million requests from client to edge.

* 12.5-GB outbound data transfer from edge to origin (assuming cache hit ratio of 95%).

* 10 rules enabled in rules engine, processing 500 million requests.

* Traffic primarily originating from North America.

| Cost factors | Azure CDN Standard Microsoft (classic) | Azure Front Door Standard |

|--|--|--|

| Base fee | $0 | $35 |

| Egress from Azure Front Door edge to client | $3,810 (calculated as (10 TB * $0.081/GB) + (40 TB * $0.075/GB)) | $3,470 (calculated as (10 TB * $0.083/GB) + (40 TB * $0.066/GB)) |

| Egress from Azure Front Door edge to origin | $0 | $0.25 (calculated as 12.5 GB * $0.02/GB) |

| Requests | $0 | $450 (calculated as 500M requests * $0.009/10k requests) |

| Rules engine - Rules | $5 (calculated as first five rules free + 5 rules * $1) | $0 |

| Rules engine - Requests processed	 | $300 (calculated as 500M * $0.60/M requests)	| $0 |

| Total | $4,115| $3,955.25 |

In this comparison, Azure CDN Standard from Microsoft (classic) is 4% more expensive than Azure Front Door Standard. This difference exists because Azure Front Door Standard includes a complimentary rules engine and offers a reduced egress rate for the 10-50 TB range.

## Recommendations to reduce cost while migrating to Azure Front Door

* Avoid migrating nonessential CDN profiles, such as temporary testing environments, to Azure Front Door. Instead, manually recreate them as an endpoint under the Azure Front Door profile after migration.

* Migrate your most important Azure Front Door (classic) profiles to Azure Front Door based on the necessity of features available in the upgrade tier.

## Next step

> [!div class="nextstepaction"]

> [Comparison between Azure Front Door and Azure Content Delivery Network](front-door-cdn-comparison.md)


# Subscription Offers

# Azure Front Door Standard/Premium subscription offers and bandwidth throttling

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

Azure Front Door Standard/Premium profiles are subject to bandwidth throttling based on your subscription type.

## Free and trial subscriptions

Bandwidth throttling is applied to these subscription types.

## Pay-as-you-go

Bandwidth is throttled until the subscription is verified to be in good standing with a sufficient payment history. This verification process occurs automatically after the first payment is received.

If throttling persists after payment, you can request removal by [contacting support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## Enterprise agreements

Refer to the bandwidth limits in [Azure Front Door limits](../../azure-resource-manager/management/azure-subscription-service-limits.md#azure-front-door-standard-and-premium-service-limits).

## Other offer types

The same rules as Pay-as-you-go apply to these subscription types:

- Visual Studio

- MSDN

- Students

- CSP

## Next step

Learn how to [create an Azure Front Door Standard/Premium profile](create-front-door-portal.md).


# Support Help

# Support and troubleshooting for Azure Front Door

Here are suggestions for where you can get help when developing your Azure Front Door solutions.

## Self help troubleshooting

Various articles explain how to determine, diagnose, and fix issues that you might encounter when using Azure Front Door. Use these articles to troubleshoot connectivity problems, performance issues, circuit configuration, and more.

For a full list of self help troubleshooting content, see [Azure Front Door troubleshooting documentation](/troubleshoot/azure/front-door/welcome-front-door).

## Post a question on Microsoft Q&A

For quick and reliable answers on your technical product questions from Microsoft Engineers, Azure Most Valuable Professionals (MVPs), or our expert community, engage with us on [Microsoft Q&A](/answers/products/azure), Azure's preferred destination for community support.

If you can't find an answer to your problem using search, submit a new question to Microsoft Q&A. Use one of the following tags when asking your question:

| Area | Tag |

| --- | --- |

| Azure Front Door | [azure-front-door](/answers/topics/azure-front-door.html) |

| CDN Standard from Microsoft (classic) | [azure-cdn](/answers/topics/azure-cdn.html) |

## Create an Azure support request

Explore the range of [Azure support options and choose the plan](https://azure.microsoft.com/support/plans) that best fits, whether you're a developer just starting your cloud journey or a large organization deploying business-critical, strategic applications. Azure customers can create and manage support requests in the Azure portal.

- If you already have an Azure Support Plan, [open a support request here](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest).

- To sign up for a new Azure Support Plan, [compare support plans](https://azure.microsoft.com/support/plans/) and select the plan that works for you.

## Create a GitHub issue

If you need help with the language and tools used to develop and manage Azure Front Door, open an issue in its repository on GitHub.

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

Learn about important product updates, roadmap, and announcements in [Azure Front Door Updates](https://azure.microsoft.com/updates/?filters=%5B"Azure+Front+Door"%5D).

News and information about Azure Front Door is shared at the [Azure blog](https://azure.microsoft.com/blog/).

## Next step

Learn more about [Azure Front Door](index.yml)


# Classic Overview

# What is Azure Front Door (classic)?

**Applies to:** :heavy_check_mark: Front Door (classic)

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

Azure Front Door (classic) is a global, scalable entry point that uses the Microsoft global edge network to deliver fast, secure, and highly scalable web applications. It enables you to transform your global consumer and enterprise applications into robust, high-performing, and personalized modern applications that reach a global audience through Azure.

Front Door (classic) operates at Layer 7 (HTTP/HTTPS layer) using anycast protocol with split TCP and Microsoft's global network to enhance global connectivity. Depending on your routing method, Front Door (classic) ensures that client requests are routed to the fastest and most available application backend. An application backend can be any Internet-facing service hosted inside or outside of Azure. Front Door (classic) offers various [traffic-routing methods](front-door-routing-methods.md) and [backend health monitoring options](front-door-health-probes.md) to meet different application needs and support automatic failover scenarios. Similar to [Traffic Manager](../traffic-manager/traffic-manager-overview.md), Azure Front Door (classic) is resilient to failures, including failures affecting an entire Azure region.

> [!NOTE]

> Azure provides a suite of fully managed load-balancing solutions for various scenarios:

> * For DNS-based global routing without the need for Transport Layer Security (TLS) protocol termination ("SSL offload") or per-HTTP/HTTPS request/application-layer processing, consider [Traffic Manager](../traffic-manager/traffic-manager-overview.md).

> * For application layer load balancing within a region, consider [Application Gateway](../application-gateway/overview.md).

> * For network layer load balancing, consider [Load Balancer](../load-balancer/load-balancer-overview.md).

>

> Combining these solutions might benefit your end-to-end scenarios. For a comparison of Azure load-balancing options, see [Overview of load-balancing options in Azure](/azure/architecture/guide/technology-choices/load-balancing-overview).

## Why use Azure Front Door (classic)?

Azure Front Door (classic) helps you efficiently build, operate, and scale dynamic web applications and static content. It optimizes global web traffic routing for top-tier end-user performance and reliability through quick global failover. Key features include:

* Accelerated application performance using **[split TCP](front-door-traffic-acceleration.md?pivots=front-door-classic#connect-to-the-front-door-edge-location-split-tcp)** and **[anycast protocol](front-door-traffic-acceleration.md?pivots=front-door-classic#select-the-front-door-edge-location-for-the-request-anycast)**.

* Intelligent **[health probe](front-door-health-probes.md)** monitoring for backend resources.

* **[URL-path based](front-door-route-matching.md?pivots=front-door-classic)** routing for requests.

* Hosting multiple websites for efficient application infrastructure.

* Cookie-based **[session affinity](front-door-routing-methods.md#affinity)**.

* **[SSL offloading](front-door-custom-domain-https.md)** and certificate management.

* Custom **[domain](front-door-custom-domain.md)** definition.

* Application security with integrated **[Web Application Firewall (WAF)](../web-application-firewall/overview.md)**.

* HTTP to HTTPS redirection with **[URL redirect](front-door-url-rewrite.md?pivots=front-door-classic)**.

* Custom forwarding paths with **[URL rewrite](front-door-url-rewrite.md?pivots=front-door-classic)**.

* Native support for end-to-end IPv6 connectivity and **[HTTP/2 protocol](front-door-http2.md)**.

## Pricing

For pricing details, see [Front Door Pricing](https://azure.microsoft.com/pricing/details/frontdoor/). For service level agreements, see [SLA for online services](https://www.microsoft.com/licensing/docs/view/Service-Level-Agreements-SLA-for-Online-Services).

## Next step

> [!div class="nextstepaction"]

> [Azure Front Door (classic) to Standard/Premium tier migration](tier-migration.md)


# Front Door Custom Domain

# Add a custom domain to Azure Front Door

**Applies to:** :heavy_check_mark: Front Door (classic)

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

This article shows how to add a custom domain to your Front Door. When you use Azure Front Door for application delivery, a custom domain is necessary if you want your own domain name to be visible in your end-user request. Having a visible domain name can be convenient for your customers and useful for branding purposes.

After you create a Front Door profile, the default frontend host is a subdomain of `azurefd.net`. This name is included in the URL for delivering Front Door content to your backend by default. For example, `https://contoso-frontend.azurefd.net`. For your convenience, Azure Front Door provides the option to associate a custom domain to the endpoint. With this capability, you can deliver your content with your URL instead of the Front Door default domain name, such as `https://www.contoso.com/photo.png`.

[!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

> [!NOTE]

> Front Door does **not** support custom domains with [punycode](https://en.wikipedia.org/wiki/Punycode) characters.

## Prerequisites

* Before you can complete the steps in this tutorial, you must first create a Front Door. For more information, see [Quickstart: Create a Front Door](quickstart-create-front-door.md).

* If you don't already have a custom domain, you must first purchase one with a domain provider. For example, see [Buy a custom domain name](../app-service/manage-custom-dns-buy-domain.md).

* If you're using Azure to host your [DNS domains](../dns/dns-overview.md), you must delegate the domain provider's domain name system (DNS) to an Azure DNS. For more information, see [Delegate a domain to Azure DNS](../dns/dns-delegate-domain-azure-dns.md). Otherwise, if you're using a domain provider to handle your DNS domain, continue to [Create a CNAME DNS record](#create-a-cname-dns-record).

## Create a CNAME DNS record

Before you can use a custom domain with your Front Door, you must first create a canonical name (CNAME) record with your domain provider to point to the Front Door default frontend host. A CNAME record is a type of DNS record that maps a source domain name to a destination domain name. In Azure Front Door, the source domain name is your custom domain name and the destination domain name is your Front Door default hostname. Once Front Door verifies the CNAME record gets created, traffic to the source custom domain gets routed to the specified destination Front Door default frontend host.

A custom domain can only be associated with one Front Door profile at a time. However, you can have different subdomains of an apex domain in the same or a different Front Door profile.

## Map the temporary afdverify subdomain

When you map an existing domain that's in production, consider the impact. While you're registering your custom domain in the Azure portal, a brief period of downtime for the domain might occur. To avoid interruption of web traffic, map your custom domain to your Front Door default frontend host by using the Azure afdverify subdomain first to create a temporary CNAME mapping. Your users can access your domain without interruption when the DNS mapping occurs.

If you're using your custom domain for the first time with no production traffic, you can directly map your custom domain to your Front Door. You can skip ahead to [Map the permanent custom domain](#map-the-permanent-custom-domain).

To create a CNAME record by using the afdverify subdomain:

1. Sign in to the website of the domain provider for your custom domain.

1. Find the page for managing DNS records by consulting the provider's documentation or searching for areas of the website labeled **Domain Name**, **DNS**, or **Name server management**.

1. Create a CNAME record entry for your custom domain and complete the fields as shown in the following table (field names might vary):

| Source                    | Type  | Destination                     |

|---------------------------|-------|---------------------------------|

| afdverify.www.contoso.com | CNAME | afdverify.contoso-frontend.azurefd.net |

- **Source:** Enter your custom domain name, including the `afdverify` subdomain, in the following format: `afdverify.<custom domain name>`. For example, `afdverify.www.contoso.com`. If you're mapping a wildcard domain, like `*.contoso.com`, the source value is the same as it would be without the wildcard: `afdverify.contoso.com`.

- **Type:** Enter *CNAME*.

- **Destination:** Enter your default Front Door frontend host, including the afdverify subdomain, in the following format: `afdverify.<endpoint name>.azurefd.net`. For example, `afdverify.contoso-frontend.azurefd.net`.

1. Save your changes.

For example, the procedure for the GoDaddy domain registrar is as follows:

1. Sign in and select the custom domain you want to use.

1. In the **Domains** section, select **Manage All**, and then select **DNS** | **Manage Zones**.

1. For **Domain Name**, enter your custom domain, and then select **Search**.

1. From the **DNS Management** page, select **Add**, and then select **CNAME** in the **Type** list.

1. Complete the following fields of the CNAME entry:

- Type: Leave *CNAME* selected.

- Host: Enter the subdomain of your custom domain for use, including the afdverify subdomain name. For example, `afdverify.www`.

- Points to: Enter the host name of your default Front Door frontend host, including the afdverify subdomain name. For example, `afdverify.contoso-frontend.azurefd.net`.

- TTL: Leave *one Hour* selected.

1. Select **Save**.

The CNAME entry is added to the DNS records table.

## Associate the custom domain with your Front Door

After you register your custom domain, add it to your Front Door.

1. Sign in to the [Azure portal](https://portal.azure.com/) and browse to the Front Door containing the frontend host that you want to map to a custom domain.

1. On the **Front Door designer** page, select **+** to add a custom domain.

3. Specify **Custom domain**.

1. For **Frontend host**, the frontend host to use as the destination domain of your CNAME record is predetermined and is derived from your Front Door: *&lt;default hostname&gt;*.azurefd.net. You can't change it.

1. For **Custom hostname**, enter your custom domain, including the subdomain, to use as the source domain of your CNAME record. For example, www\.contoso.com or cdn.contoso.com. Don't use the afdverify subdomain name.

1. Select **Add**.

Azure verifies that the CNAME record exists for the custom domain name you entered. If the CNAME is correct, your custom domain gets validated.

> [!WARNING]

> You **must** ensure that each of the frontend hosts (including custom domains) in your Front Door has a routing rule with a default path ('/\*') associated with it. That is, across all of your routing rules there must be at least one routing rule for each of your frontend hosts defined at the default path ('/\*'). If you don't configure this setting, your end-user traffic might not route correctly.

## Verify the custom domain

After you complete the registration of your custom domain, verify that the custom domain references your default Front Door frontend host.

In your browser, go to the address of the file by using the custom domain. For example, if your custom domain is robotics.contoso.com, the URL to the cached file should be similar to the following URL: `http://robotics.contoso.com/my-public-container/my-file.jpg`. Verify that the result is the same as when you access the Front Door directly at *&lt;Front Door host&gt;*.azurefd.net.

## Map the permanent custom domain

To map the custom domain directly to your default Front Door frontend host, first make sure that the afdverify subdomain is successfully mapped to your Front Door. Once verified, you can proceed with mapping the custom domain.

To create a CNAME record for your custom domain:

1. Sign in to the website of the domain provider for your custom domain.

1. Find the page for managing DNS records by consulting the provider's documentation or searching for areas of the website labeled **Domain Name**, **DNS**, or **Name Server Management**.

1. Create a CNAME record entry for your custom domain and complete the fields as shown in the following table (field names might vary):

| Source          | Type  | Destination           |

|-----------------|-------|-----------------------|

| <www.contoso.com> | CNAME | contoso-frontend.azurefd.net |

- Source: Enter your custom domain name (for example, www\.contoso.com).

- Type: Enter *CNAME*.

- Destination: Enter your default Front Door frontend host. It must be in the following format:_&lt;hostname&gt;_.azurefd.net. For example, contoso-frontend.azurefd.net.

1. Save your changes.

1. If you previously created a temporary afdverify subdomain CNAME record, delete it.

1. If you're using this custom domain in production for the first time, follow the steps for [Associate the custom domain with your Front Door](#associate-the-custom-domain-with-your-front-door) and [Verify the custom domain](#verify-the-custom-domain).

For example, the procedure for the GoDaddy domain registrar is as follows:

1. Sign in and select the custom domain you want to use.

1. In the **Domains** section, select **Manage All**, and then select **DNS** | **Manage Zones**.

1. For **Domain Name**, enter your custom domain, and then select **Search**.

1. From the **DNS Management** page, select **Add**, and then select **CNAME** in the **Type** list.

1. Complete the fields of the CNAME entry:

- Type: Leave *CNAME* selected.

- Host: Enter the subdomain of your custom domain to use. For example, www or profile.

- Points to: Enter the default host name of your Front Door. For example, contoso.azurefd.net.

- TTL: Leave *one Hour* selected.

1. Select **Save**.

The CNAME entry is added to the DNS records table.

1. If you have an afdverify CNAME record, select the pencil icon next to it, and then select the trash can icon.

1. Select **Delete** to delete the CNAME record.

## Clean up resources

In the preceding steps, you added a custom domain to a Front Door. If you no longer want to associate your Front Door with a custom domain, remove the custom domain by following these steps:

1. Go to your DNS provider, and either delete the CNAME record for the custom domain or update the CNAME record for the custom domain to a non-Front Door endpoint.

> [!Important]

> To prevent dangling DNS entries and the security risks they create, starting from April 9, 2021, Azure Front Door requires removal of the CNAME records to Front Door endpoints before you can delete the resources. Resources include Front Door custom domains, Front Door endpoints, or Azure resource groups that have Front Door custom domains enabled.

1. In your Front Door designer, select the custom domain that you want to remove.

1. Select **Delete** from the context menu for the custom domain. The custom domain is removed from your endpoint.

## Next step

> [!div class="nextstepaction"]

> [Enable HTTPS for a custom domain](front-door-custom-domain-https.md)


# Custom Domain

# Azure Front Door: Deploy custom domain

**Applies to:** :heavy_check_mark: Front Door (classic)

[!INCLUDE [Azure Front Door (classic) retirement notice](../../../includes/front-door-classic-retirement.md)]

This Azure CLI script example demonstrates how to deploy a custom domain name and TLS certificate on an Azure Front Door front-end. The script automates the provisioning of Azure Front Door with a custom domain name (hosted by Azure DNS) and a TLS certificate.

> [!IMPORTANT]

> Ensure that an Azure DNS public zone already exists for your domain name. For a tutorial, see [Host your domain in Azure DNS](../../dns/dns-delegate-domain-azure-dns.md).

[!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment.md)]

## Sample script

[!INCLUDE [cli-launch-cloud-shell-sign-in.md](~/reusable-content/ce-skilling/azure/includes/cli-launch-cloud-shell-sign-in.md)]

### Getting started

The script:

1. Creates a resource group.

1. Creates a storage account to host a single-page application (SPA).

1. Enables SPA hosting on the storage account.

1. Uploads a "Hello world!" `index.html` file.

1. Creates a Front Door profile.

1. Creates a DNS alias for the Apex that resolves to the Front Door.

1. Creates a CNAME for the `adverify` hostname.

1. Creates a Front Door front-end endpoint for the custom domain.

1. Adds a route from the custom domain front-end to the SPA origin.

1. Adds a routing rule to redirect HTTP to HTTPS.

1. Enables HTTPS with a Front Door managed certificate.

### Run the script

To run this script, copy the following code to a `.sh` file, change the hardcoded variables to your domain values, and then execute the following command to pass these variables into the script:

```sh

AZURE_DNS_ZONE_NAME=www.contoso.com AZURE_DNS_ZONE_RESOURCE_GROUP=contoso-rg ./deploy-custom-apex-domain.sh

```

## Clean up resources

[!INCLUDE [cli-clean-up-resources.md](~/reusable-content/ce-skilling/azure/includes/cli-clean-up-resources.md)]

```azurecli

az group delete --name $resourceGroup

```

## Sample reference

This script uses the following commands. Each command in the table links to command-specific documentation.

| Command | Description |

|---|---|

| [az group create](/cli/azure/group#az-group-create) | Creates a resource group to store all resources. |

| [az storage account create](/cli/azure/storage/account) | Creates an Azure Storage account in the specified resource group. |

| [az storage blob service-properties update](/cli/azure/storage/blob/service-properties#az-storage-blob-service-properties-update) | Updates storage blob service properties. |

| [az storage blob upload](/cli/azure/storage/blob#az-storage-blob-upload) | Uploads a blob to a container. |

| [az storage account show](/cli/azure/storage/account#az-storage-account-show) | Shows storage account properties. |

| [az network front-door create](/cli/azure/network/front-door#az-network-front-door-create) | Creates a Front Door. |

| [az network dns record-set](/cli/azure/network/dns/record-set) | Manages DNS records and record sets. |

| [az network front-door](/cli/azure/network/front-door) | Manages Front Doors. |


# Front Door Custom Domain Https

# Configure HTTPS on an Azure Front Door (classic) custom domain

**Applies to:** :heavy_check_mark: Front Door (classic)

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

This article explains how to enable HTTPS for a custom domain associated with your Front Door (classic). Using HTTPS on your custom domain (for example, `https://www.contoso.com`) ensures secure data transmission via TLS/SSL encryption. When a web browser connects to a website using HTTPS, it validates the website's security certificate and verifies its legitimacy, providing security and protecting your web applications from malicious attacks.

Azure Front Door supports HTTPS by default on its default hostname (for example, `https://contoso.azurefd.net`). However, you need to enable HTTPS separately for custom domains like `www.contoso.com`.

Key attributes of the custom HTTPS feature include:

- **No extra cost**: No costs for certificate acquisition, renewal, or HTTPS traffic.

- **Simple enablement**: One-select provisioning via the [Azure portal](https://portal.azure.com), REST API, or other developer tools.

- **Complete certificate management**: Automatic certificate procurement and renewal, eliminating the risk of service interruption due to expired certificates.

In this tutorial, you learn to:

> [!div class="checklist"]

> - Enable HTTPS on your custom domain.

> - Use an AFD-managed certificate.

> - Use your own TLS/SSL certificate.

> - Validate the domain.

> - Disable HTTPS on your custom domain.

## Prerequisites

# [**PowerShell**](#tab/powershell)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An Azure Front Door with at least one custom domain onboarded. For more information, see [Tutorial: Add a custom domain to your Front Door](front-door-custom-domain.md).

- Azure Cloud Shell or Azure PowerShell to register Front Door service principal in your Microsoft Entra ID when [using your own certificate](#option-2-use-your-own-certificate).

The steps in this article run the Azure PowerShell cmdlets interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the cmdlets in the Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code and then paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure PowerShell locally](/powershell/azure/install-azure-powershell) to run the cmdlets. If you run PowerShell locally, sign in to Azure using the [Connect-AzAccount](/powershell/module/az.accounts/connect-azaccount) cmdlet.

# [**Azure CLI**](#tab/cli)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An Azure Front Door with at least one custom domain onboarded. For more information, see [Tutorial: Add a custom domain to your Front Door](front-door-custom-domain.md).

- Azure Cloud Shell or Azure CLI to register Front Door service principal in your Microsoft Entra ID when [using your own certificate](#option-2-use-your-own-certificate).

The steps in this article run the Azure CLI commands interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the commands in the Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code, and paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure CLI locally](/cli/azure/install-azure-cli) to run the commands. If you run Azure CLI locally, sign in to Azure using the [az login](/cli/azure/reference-index#az-login) command.

---

## TLS/SSL certificates

To enable HTTPS on a Front Door (classic) custom domain, you need a TLS/SSL certificate. You can either use a certificate managed by Azure Front Door or your own certificate.

### Option 1 (default): Use a certificate managed by Front Door

If you use a certificate managed by Azure Front Door Classic, you can turn on HTTPS by changing a few settings. Azure Front Door Classic takes care of all certificate management tasks, including getting and renewing the certificate. This option supports custom domains that use direct CNAME to Azure Front Door Classic endpoint.

> [!IMPORTANT]

> - As of May 8, 2025, DigiCert no longer supports the WHOIS-based domain validation method. If your domain uses an indirect CNAME mapping to Azure Front Door Classic endpoint, you must use the **Bring Your Own Certificate (BYOC)** feature.

> - Due to changes in WHOIS-based domain validation, managed certificates issued using WHOIS-based domain validation can't be autorenewed until you have a direct CNAME pointing to Azure Front Door Classic.

> - Managed certificates aren't available for root or apex domains (for example, `contoso.com`). If your Azure Front Door Classic custom domain is a root or apex domain, you must use the **Bring Your Own Certificate (BYOC)** feature.

> - Managed certificate autorenewal requires that your custom domain be directly mapped to your Azure Front Door Classic endpoint using a CNAME record.

To enable HTTPS on a custom domain:

1. In the [Azure portal](https://portal.azure.com), go to your **Front Door** profile.

1. Select the custom domain you want to enable HTTPS for from the list of frontend hosts.

1. Under **Custom domain HTTPS**, select **Enabled** and choose **Front Door managed** as the certificate source.

1. Select **Save**.

1. Proceed to [Validate the domain](#validate-the-domain).

> [!NOTE]

> - DigiCert’s 64 character limit is enforced for Azure Front Door-managed certificates. Validation fails if this limit is exceeded.

> - Enabling HTTPS via Front Door managed certificate isn't supported for apex/root domains (for example, contoso.com). Use your own certificate for this scenario (see Option 2).

### Option 2: Use your own certificate

You can use your own certificate through an integration with Azure Key Vault. Ensure your certificate is from a [Microsoft Trusted CA List](https://ccadb.my.salesforce-sites.com/microsoft/IncludedCACertificateReportForMSFT) and has a complete certificate chain.

#### Prepare your key vault and certificate

- Create a key vault account in the same Azure subscription as your Front Door.

- Configure your key vault to allow trusted Microsoft services to bypass the firewall if network access restrictions are enabled.

- Use the *Key Vault access policy* permission model.

- Upload your certificate as a **certificate** object, not a **secret**.

> [!NOTE]

> Front Door doesn't support certificates with elliptic curve (EC) cryptography algorithms. The certificate must have a complete certificate chain with leaf and intermediate certificates, and root CA must be part of the [Microsoft Trusted CA list](https://ccadb.my.salesforce-sites.com/microsoft/IncludedCACertificateReportForMSFT).

#### Register Azure Front Door

Register the Azure Front Door service principal in your Microsoft Entra ID using Azure PowerShell or Azure CLI.

# [**PowerShell**](#tab/powershell)

Use [New-AzADServicePrincipal](/powershell/module/az.resources/new-azadserviceprincipal) cmdlet to register the Front Door service principal in your Microsoft Entra ID.

```azurepowershell-interactive

New-AzADServicePrincipal -ApplicationId "ad0e1c7e-6d38-4ba4-9efd-0bc77ba9f037"

```

# [**Azure CLI**](#tab/cli)

Use the [az-ad-sp create](/cli/azure/ad/sp#az-ad-sp-create) command to register the Front Door service principal in your Microsoft Entra ID.

```azurecli-interactive

az ad sp create --id ad0e1c7e-6d38-4ba4-9efd-0bc77ba9f037

```

---

#### Grant Azure Front Door access to your key vault

1. In your key vault account, select **Access policies**.

1. Select **Create** to create a new access policy.

1. In **Secret permissions**, select **Get**.

1. In **Certificate permissions**, select **Get**.

1. In **Select principal**, search for **ad0e1c7e-6d38-4ba4-9efd-0bc77ba9f037** and select **Microsoft.Azure.Frontdoor**. Select **Next**.

1. Select **Next** in **Application**.

1. Select **Create** in **Review + create**.

> [!NOTE]

> If your key vault has network access restrictions, allow trusted Microsoft services to access your key vault.

#### Select the certificate for Azure Front Door to deploy

1. Return to your Front Door in the portal.

1. Select the custom domain for which you want to enable HTTPS.

1. Under **Certificate management type**, select **Use my own certificate**.

1. Select a key vault, Secret, and Secret version.

> [!NOTE]

> To enable automatic certificate rotation, set the secret version to **Latest**. If you select a specific version, you must manually update it for certificate rotation.

> [!WARNING]

> Ensure your service principal has **GET** permission on the Key Vault. To see the certificate in the portal drop-down, your user account must have **LIST** and **GET** permissions on the Key Vault.

1. When you use your own certificate, domain validation isn't required. Proceed to [Wait for propagation](#wait-for-propagation).

## Validate the domain

If your CNAME record still exists and doesn't contain the `afdverify` subdomain, DigiCert automatically validates ownership of your custom domain.

Your CNAME record should be in the following format:

| Name            | Type  | Value                 |

|-----------------|-------|-----------------------|

| <www.contoso.com> | CNAME | contoso.azurefd.net |

For more information about CNAME records, see [Create the CNAME DNS record](../cdn/cdn-map-content-to-custom-domain.md).

If your CNAME record is in the correct format, DigiCert automatically verifies your custom domain name and creates a certificate for your domain. The certificate is valid for one year and is autorenewed before it expires. Automatic validation typically takes a few hours. If you don't see your domain validated in 24 hours, open a support ticket.

Continue to [Wait for propagation](#wait-for-propagation).

> [!NOTE]

> If you have a Certificate Authority Authorization (CAA) record with your DNS provider, it must include DigiCert as a valid CA. For more information, see [Manage CAA records](https://support.dnsimple.com/articles/manage-caa-record/).

## Wait for propagation

After domain validation, it can take up to 6-8 hours for the custom domain HTTPS feature to activate. When complete, the custom HTTPS status in the Azure portal is set to **Enabled**.

### Operation progress

The following table shows the operation progress when enabling HTTPS:

| Operation step | Operation substep details |

| --- | --- |

| 1. Submitting request | Submitting request |

| | Your HTTPS request is being submitted. |

| | Your HTTPS request was submitted successfully. |

| 2. Domain validation | Domain is automatically validated if CNAME mapped to the default .azurefd.net frontend host. |

| | Your domain ownership was successfully validated. |

| | Domain ownership validation request expired (customer likely didn't respond within six days). HTTPS isn't enabled on your domain. * |

| | Domain ownership validation request rejected by the customer. HTTPS isn't enabled on your domain. * |

| 3. Certificate provisioning | The certificate authority is issuing the certificate needed to enable HTTPS on your domain. |

| | The certificate was issued and is being deployed for your Front Door. This process could take several minutes to an hour. |

| | The certificate was successfully deployed for your Front Door. |

| 4. Complete | HTTPS was successfully enabled on your domain. |

\* This message appears only if an error occurs.

If an error occurs before the request is submitted, the following error message is displayed:

<code>

We encountered an unexpected error while processing your HTTPS request. Please try again and contact support if the issue persists.

</code>

## Frequently asked questions

1. **Who is the certificate provider and what type of certificate is used?**

A dedicated/single certificate, provided by DigiCert, is used for your custom domain.

1. **Do you use IP-based or SNI TLS/SSL?**

Azure Front Door uses SNI TLS/SSL.

1. **What if I don't receive the domain verification email from DigiCert?**

If you have a CNAME entry for your custom domain that points directly to your endpoint hostname and you aren't using the afdverify subdomain name, you don't receive a domain verification email. Validation occurs automatically. Otherwise, if you don't have a CNAME entry and didn't receive an email within 24 hours, contact Microsoft support.

1. **Is using a SAN certificate less secure than a dedicated certificate?**

A SAN certificate follows the same encryption and security standards as a dedicated certificate. All issued TLS/SSL certificates use SHA-256 for enhanced server security.

1. **Do I need a Certificate Authority Authorization record with my DNS provider?**

No, you don't currently need a Certificate Authority Authorization record. However, if you have one, it must include DigiCert as a valid CA.

## Clean up resources

To disable HTTPS on your custom domain:

### Disable the HTTPS feature

1. In the [Azure portal](https://portal.azure.com), go to your **Azure Front Door** configuration.

1. Select the custom domain for which you want to disable HTTPS.

1. Select **Disabled** and select **Save**.

### Wait for propagation

After disabling the custom domain HTTPS feature, it can take up to 6-8 hours to take effect. When complete, the custom HTTPS status in the Azure portal is set to **Disabled**.

#### Operation progress

The following table shows the operation progress when disabling HTTPS:

| Operation progress | Operation details |

| --- | --- |

| 1. Submitting request | Submitting your request |

| 2. Certificate deprovisioning | Deleting certificate |

| 3. Complete | Certificate deleted |

## Next step

> [!div class="nextstepaction"]

> [Set up a geo-filtering policy](/azure/web-application-firewall/afds/waf-front-door-tutorial-geo-filtering?toc=/azure/frontdoor/toc.json)


# Front Door Tutorial Rules Engine

# Tutorial: Configure your rules engine

**Applies to:** :heavy_check_mark: Front Door (classic)

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

This tutorial shows how to create a Rules engine configuration and your first rule in both Azure portal and CLI.

In this tutorial, you learn how to:

> [!div class="checklist"]

> - Configure Rules Engine using the portal.

> - Configure Rules Engine using Azure CLI.

## Prerequisites

* Before you can complete the steps in this tutorial, you must first create an Azure Front Door (classic). For more information, see [Create an Azure Front Door (classic)](quickstart-create-front-door.md).

## Configure Rules Engine in the Azure portal

1. In your Azure Front Door (classic) resource, select **Rule Engine configuration** under *Settings* in the left menu. Select **+ Add**, enter a name for your configuration, and start creating your first Rules Engine configuration.

1. Enter a name for your first rule. Then select **+ Add condition** or **+ Add action** to define your rule.

> [!NOTE]

> - To delete a condition or action from a rule, use the trash can icon on the right-hand side of the specific condition or action.

> - To create a rule that applies to all incoming traffic, don't specify any conditions.

> - To stop evaluating rules once the first match condition is met, check **Stop evaluating remaining rule**. If this condition is met, the remaining rules in the configuration aren't executed.

> - All paths in the rules engine configuration are case sensitive.

> - Header names should adhere to [RFC 7230](https://datatracker.ietf.org/doc/html/rfc7230#section-3.2.6).

1. Determine the priority of the rules within your configuration by using the **Move up**, **Move down**, and **Move to top** buttons. The priority is in ascending order, meaning the rule first listed is the most important rule.

> [!TIP]

> If you want to verify when the changes are propagated to Azure Front Door (classic), you can create a custom response header in the rule by using the following example. You can add a response header `_X-<RuleName>-Version_` and change the value each time the rule is updated.

>

> :::image type="content" source="./media/front-door-rules-engine/rules-version.png" alt-text="Screenshot of custom version header rule." lightbox="./media/front-door-rules-engine/rules-version-expanded.png":::

> After the changes are updated, you can go to the URL to confirm the rule version being invoked:

> :::image type="content" source="./media/front-door-rules-engine/version-output.png" alt-text="Screenshot of custom header version output.":::

1. When you create one or more rules, select **Save**. This action creates your rules engine configuration.

1. After you create a rules engine configuration, associate the configuration with a routing rule. You can apply a single configuration to multiple routing rules, but a routing rule can only have one rules engine configuration. To associate the configuration, go to the **Azure Front Door (classic) designer** and select a **Route**. Then select the **Rules engine configuration** to associate with the routing rule.

## Configure Rules Engine in Azure CLI

1. Install the [Azure CLI](/cli/azure/install-azure-cli) and add the "front-door" extension:

```azurecli

az extension add --name front-door

```

Sign in and switch to your subscription:

```azurecli

az account set --subscription <name_or_Id>

```

1. Create a Rules Engine with one rule, including a header-based action and a match condition:

```azurecli

az network front-door rules-engine rule create -f {front_door} -g {resource_group} --rules-engine-name {rules_engine} --name {rule1} --priority 1 --action-type RequestHeader --header-action Overwrite --header-name Rewrite --header-value True --match-variable RequestFilenameExtension --operator Contains --match-values jpg png --transforms Lowercase

```

1. List all the rules:

```azurecli

az network front-door rules-engine rule list -f {front_door} -g {rg} --name {rules_engine}

```

1. Add a forwarding route override action:

```azurecli

az network front-door rules-engine rule action add -f {front_door} -g {rg} --rules-engine-name {rules_engine} --name {rule1} --action-type ForwardRouteOverride --backend-pool {backend_pool_name} --caching Disabled

```

1. List all the actions in a rule:

```azurecli

az network front-door rules-engine rule action list -f {front_door} -g {rg} -r {rules_engine} --name {rule1}

```

1. Link a rules engine configuration to a routing rule:

```azurecli

az network front-door routing-rule update -g {rg} -f {front_door} -n {routing_rule_name} --rules-engine {rules_engine}

```

1. Unlink the rules engine:

```azurecli

az network front-door routing-rule update -g {rg} -f {front_door} -n {routing_rule_name} --remove rulesEngine

```

For more information, see the full list of [Azure Front Door (classic) Rules engine commands](/cli/azure/network/front-door/rules-engine).

## Clean up resources

To remove the Rules Engine configuration from your Front Door (classic):

1. Select the three dots next to the rule engine name, and then select **Associate routing rule** to disassociate any routing rules from the rule engine configuration:

1. Uncheck all routing rules associated with this Rule Engine configuration, and then select **Save**:

1. Delete the Rule Engine configuration from your Front Door:

## Next steps

In this tutorial, you learned how to:

* Create a Rule engine configuration

* Associate a configuration to a routing rule

To learn how to add security headers by using Rule engine, continue to the next tutorial.

> [!div class="nextstepaction"]

> [Security headers with Rules Engine](front-door-security-headers.md)


# Front Door How To Redirect Https

# Configure HTTP to HTTPS redirection using the Azure portal

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

This guide explains how to redirect traffic from HTTP to HTTPS for an Azure Front Door (classic) profile using the Azure portal. This setup ensures that all traffic to your domain is securely redirected to HTTPS.

## Prerequisites

* An existing Azure Front Door (classic) profile. For more information, see [create a Front Door (classic) profile](quickstart-create-front-door.md).

## Create HTTP to HTTPS redirect rule

1. Sign in to the [Azure portal](https://portal.azure.com).

2. Navigate to the Azure Front Door (classic) profile you want to configure. Select **Front Door designer** under *Settings* in the left-hand menu.

3. Select the **+** icon under *Routing rules* to create a new route. Name the route, for example, **HttpToHttpsRedirect**, and set the *Accepted Protocol* to **HTTP only**. Choose the *Frontend/domains* you want to redirect from HTTP to HTTPS.

4. In the *Route Details* section, set the *Route Type* to **Redirect**. Choose **Moved (301)** for *Redirect type* and **HTTPS only** for *Redirect protocol*.

5. Select **Add** to create the routing rule for HTTP to HTTPS redirection.

## Create forwarding rule

1. Add another routing rule for handling HTTPS traffic. Select the **+** icon under *Routing rules* to add a new route. Name the route, for example, **DefaultForwardingRoute**, and set the *Accepted Protocols* to **HTTPS only**. Select the appropriate *Frontend/domains* for accepting this traffic.

2. In the *Route Details* section, set the *Route Type* to **Forward**. Choose a backend pool to forward the traffic to and set the *Forwarding Protocol* to **HTTPS only**.

3. Select **Add** to create the forwarding route, then select **Save** to apply the changes to the Front Door profile.

> [!NOTE]

> Creating this redirect rule will incur a small charge.

## Next steps

- Learn more about [Azure Front Door routing architecture](front-door-routing-architecture.md).

- Learn more about [Azure Front Door URL redirect](front-door-url-redirect.md).


# Front Door Security Headers

# Tutorial: Add security headers with rules engine

**Applies to:** :heavy_check_mark: Front Door (classic)

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

This tutorial demonstrates how to implement security headers to prevent browser-based vulnerabilities such as HTTP Strict-Transport-Security (HSTS), X-XSS-Protection, Content-Security-Policy, and X-Frame-Options. Security attributes can also be defined with cookies.

The example in this tutorial shows how to add a Content-Security-Policy header to all incoming requests that match the path defined in the route associated with your rules engine configuration. In this scenario, only scripts from the trusted site `https://apiphany.portal.azure-api.net` are allowed to run on the application.

In this tutorial, you learn how to:

> [!div class="checklist"]

> - Configure a Content-Security-Policy within rules engine.

## Prerequisites

* An Azure subscription.

* An Azure Front Door. To complete this tutorial, you must have an Azure Front Door configured with rules engine. For more information, see [Create an Azure Front Door](quickstart-create-front-door.md) and [Configure your rules engine](front-door-tutorial-rules-engine.md).

## Add a Content-Security-Policy header in Azure portal

1. In your Azure Front Door resource, select **Rules engine configuration** under **Settings**. Choose the rules engine where you want to add the security header.

2. Select **Add rule** to create a new rule. Name the rule and then select **Add an Action** > **Response Header**.

3. Set the Operator to **Append** to add this header to all incoming requests for this route.

4. Enter the header name: *Content-Security-Policy* and specify the values for this header. In this example, use *`script-src 'self' https://apiphany.portal.azure-api.net`*. Select **Save**.

> [!NOTE]

> Header values are limited to 640 characters.

5. After adding the rules, associate your Rules engine configuration with the Route Rule of your chosen route. This step is necessary for the rule to take effect.

> [!NOTE]

> In this example, no [match conditions](front-door-rules-engine-match-conditions.md) were added to the rule. The rule will apply to all incoming requests that match the path defined in the Route Rule. To apply it to a subset of requests, add specific **match conditions** to the rule.

## Clean up resources

If you no longer need the security header rule configured in the previous steps, you can remove it by selecting **Delete rule** in the rules engine.

## Next step

> [!div class="nextstepaction"]

> [Web Application Firewall and Azure Front Door](front-door-waf.md)


# Front Door Waf

# Tutorial: Quickly scale and protect a web application using Azure Front Door and Azure Web Application Firewall (WAF)

**Applies to:** :heavy_check_mark: Front Door (classic)

[!INCLUDE [Azure Front Door (classic) retirement notice](../../includes/front-door-classic-retirement.md)]

Web applications often experience traffic surges and malicious attacks, such as denial-of-service attacks. Azure Front Door with Azure WAF can help scale your application and protect it from such threats. This tutorial guides you through configuring Azure Front Door with Azure WAF for any web app, whether it runs inside or outside of Azure.

We use the Azure CLI for this tutorial. You can also use the Azure portal, Azure PowerShell, Azure Resource Manager, or Azure REST APIs.

In this tutorial, you learn to:

> [!div class="checklist"]

> - Create a Front Door.

> - Create an Azure WAF policy.

> - Configure rule sets for a WAF policy.

> - Associate a WAF policy with Front Door.

> - Configure a custom domain.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- This tutorial uses the Azure CLI. [Get started with the Azure CLI](/cli/azure/get-started-with-azure-cli).

> [!TIP]

> An easy way to get started with the Azure CLI is using [Bash in Azure Cloud Shell](../cloud-shell/quickstart.md).

- Ensure the `front-door` extension is added to the Azure CLI:

```azurecli-interactive

az extension add --name front-door

```

> [!NOTE]

> For more information about the commands used in this tutorial, see the [Azure CLI reference for Front Door](/cli/azure/).

## Create an Azure Front Door resource

```azurecli-interactive

az network front-door create --backend-address <backend-address> --accepted-protocols <protocols> --name <name> --resource-group <resource-group>

```

- `--backend-address`: The fully qualified domain name (FQDN) of the application you want to protect, for example, `myapplication.contoso.com`.

- `--accepted-protocols`: Protocols supported by Azure Front Door, for example, `--accepted-protocols Http Https`.

- `--name`: The name of your Azure Front Door resource.

- `--resource-group`: The resource group for this Azure Front Door resource. Learn more about [managing resource groups](../azure-resource-manager/management/manage-resource-groups-portal.md).

Note the `hostName` value from the response, as you need it later. The `hostName` is the DNS name of the Azure Front Door resource.

## Create an Azure WAF profile for Azure Front Door

```azurecli-interactive

az network front-door waf-policy create --name <name> --resource-group <resource-group> --disabled false --mode Prevention

```

- `--name`: The name of the new Azure WAF policy.

- `--resource-group`: The resource group for this WAF resource.

The previous command creates a WAF policy in prevention mode.

> [!NOTE]

> Consider creating the WAF policy in detection mode first to observe and log malicious requests without blocking them before switching to prevention mode.

Note the `ID` value from the response, as you need it later. The `ID` should be in this format:

`/subscriptions/<subscription-id>/resourcegroups/<resource-group>/providers/Microsoft.Network/frontdoorwebapplicationfirewallpolicies/<WAF-policy-name>`

## Add managed rule sets to the WAF policy

Add the default rule set:

```azurecli-interactive

az network front-door waf-policy managed-rules add --policy-name <policy-name> --resource-group <resource-group> --type DefaultRuleSet --version 1.0

```

Add the bot protection rule set:

```azurecli-interactive

az network front-door waf-policy managed-rules add --policy-name <policy-name> --resource-group <resource-group> --type Microsoft_BotManagerRuleSet --version 1.0

```

- `--policy-name`: The name of your Azure WAF resource.

- `--resource-group`: The resource group for the WAF resource.

## Associate the WAF policy with the Azure Front Door resource

```azurecli-interactive

az network front-door update --name <name> --resource-group <resource-group> --set frontendEndpoints[0].webApplicationFirewallPolicyLink='{"id":"<ID>"}'

```

- `--name`: The name of your Azure Front Door resource.

- `--resource-group`: The resource group for the Azure Front Door resource.

- `--set`: Update the `WebApplicationFirewallPolicyLink` attribute for the `frontendEndpoint` with the new WAF policy ID.

> [!NOTE]

> If you're not using a custom domain, you can skip the next section. Provide your customers with the `hostName` obtained when you created the Azure Front Door resource.

## Configure the custom domain for your web application

Update your DNS records to point the custom domain to the Azure Front Door `hostName`. Refer to your DNS service provider's documentation for specific steps. If you use Azure DNS, see [update a DNS record](../dns/dns-operations-recordsets-cli.md).

For zone apex domains (for example, contoso.com), use Azure DNS and its [alias record type](../dns/dns-alias.md).

Update your Azure Front Door configuration to [add the custom domain](./front-door-custom-domain.md).

To enable HTTPS for your custom domain, [set up certificates in Azure Front Door](./front-door-custom-domain-https.md).

## Lock down your web application

Ensure only Azure Front Door edges can communicate with your web application. See [How to lock down access to my backend to only Azure Front Door](./front-door-faq.yml#what-are-the-steps-to-restrict-the-access-to-my-backend-to-only-azure-front-door-).

## Clean up resources

When no longer needed, delete the resource group, Front Door, and WAF policy:

```azurecli-interactive

az group delete --name <resource-group>

```

- `--name`: The name of the resource group for all resources used in this tutorial.

## Next steps

To troubleshoot your Front Door, see:

> [!div class="nextstepaction"]

> [Troubleshooting common routing issues](front-door-troubleshoot-routing.md)


# Front Door Http Headers Protocol

# Protocol support for HTTP headers in Azure Front Door

This article outlines the protocol that Front Door supports with parts of the call path (see image). In the following sections, you find information about HTTP headers supported by Front Door.

> [!IMPORTANT]

> Azure Front Door doesn't certify any HTTP headers that aren't documented in this article.

## From the client to the Front Door

Azure Front Door accepts most headers for the incoming request without modifying them. Some reserved headers are removed from the incoming request if sent, including headers with the `X-FD-*` prefix.

The debug request header, `X-Azure-DebugInfo`, provides extra debugging information about the Front Door. You need to send `X-Azure-DebugInfo: 1` request header from the client to the Azure Front Door to receive [optional response headers](#optional-debug-response-headers) when Azure Front Door response to the client.

## From the Front Door to the backend

Azure Front Door includes headers for an incoming request unless they're removed because of restrictions. Azure Front Door also appends the following headers:

| Header  | Example and description |

| ------------- | ------------- |

| Via |  `Via: 1.1 Azure` </br> Front Door adds the client's HTTP version followed by *Azure* as the value for the Via header. This header indicates the client's HTTP version and that Front Door was an intermediate recipient for the request between the client and the backend.  |

| X-Azure-ClientIP | `X-Azure-ClientIP: 127.0.0.1` </br> Represents the client IP address associated with the request being processed. For example, a request coming from a proxy might add the X-Forwarded-For header to indicate the IP address of the original caller. |

| X-Azure-SocketIP |  `X-Azure-SocketIP: 127.0.0.1` </br> Represents the socket IP address associated with the TCP connection that the current request originated from. A request's client IP address might not be equal to its socket IP address because the client IP can be arbitrarily overwritten by a user.|

| X-Azure-Ref | `X-Azure-Ref: 0zxV+XAAAAABKMMOjBv2NT4TY6SQVjC0zV1NURURHRTA2MTkANDM3YzgyY2QtMzYwYS00YTU0LTk0YzMtNWZmNzA3NjQ3Nzgz` </br> A unique reference string that identifies a request served by Azure Front Door. This string is used to search access logs and critical for troubleshooting.|

| X-Azure-RequestChain | `X-Azure-RequestChain: hops=1` </br> A header that Front Door uses to detect request loops, and users shouldn't take a dependency on it. |

| X-Azure-FDID | `X-Azure-FDID: a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1` <br/> A reference string that identifies the request came from a specific Front Door resource. The value can be seen in the Azure portal or retrieved using the management API. You can use this header in combination with IP ACLs to lock down your endpoint to only accept requests from a specific Front Door resource. See the FAQ for [more detail](front-door-faq.yml#what-are-the-steps-to-restrict-the-access-to-my-backend-to-only-azure-front-door-) |

| X-Forwarded-For | `X-Forwarded-For: 127.0.0.1` </br> The X-Forwarded-For (XFF) HTTP header field often identifies the originating IP address of a client connecting to a web server through an HTTP proxy or load balancer. If there's an existing XFF header, then Front Door appends the client socket IP to it or adds the XFF header with the client socket IP. |

| X-Forwarded-Host | `X-Forwarded-Host: contoso.azurefd.net` </br> The X-Forwarded-Host HTTP header field is a common method used to identify the original host requested by the client in the Host HTTP request header. This is because the host name from Azure Front Door might differ for the backend server handling the request. Any previous value is overridden by Azure Front Door. |

| X-Forwarded-Proto | `X-Forwarded-Proto: http` </br> The `X-Forwarded-Proto` HTTP header field is often used to identify the originating protocol of an HTTP request. Front Door based on configuration might communicate with the backend by using HTTPS. This is true even if the request to the reverse proxy is HTTP. Any previous value will be overridden by Front Door. |

| X-FD-HealthProbe | `X-FD-HealthProbe` HTTP header field is used to identify the health probe from Front Door. If this header is set to 1, the request is from the health probe. It can be used to restrict access from Front Door with a particular value for the `X-Forwarded-Host` header field. |

| X-Azure-JA4-Fingerprint | `X-Azure-JA4-Fingerprint` HTTP header field is used to uniquely identify client behavior based on TLS client hello attributes. It enables better detection of bots, anomalies, and malicious traffic across sessions.|

## From the Front Door to the client

Any headers sent to Azure Front Door from the backend are also passed through to the client. Front Door also attaches the following headers to all responses to the client:

| Header  | Example and description |

| ------------- | ------------- |

| X-Azure-Ref |  `X-Azure-Ref: 0zxV+XAAAAABKMMOjBv2NT4TY6SQVjC0zV1NURURHRTA2MTkANDM3YzgyY2QtMzYwYS00YTU0LTk0YzMtNWZmNzA3NjQ3Nzgz` </br> This is a unique reference string that identifies a request served by Front Door, which is critical for troubleshooting as it's used to search access logs.|

| X-Cache | `X-Cache:` This header describes the caching status of the request. For more information, see [Caching with Azure Front Door](front-door-caching.md#response-headers). |

### Optional debug response headers

You need to send `X-Azure-DebugInfo: 1` request header to enable the following optional response headers.

| Header  | Example and description |

| ------------- | ------------- |

| X-Azure-OriginStatusCode |  `X-Azure-OriginStatusCode: 503` </br> This header contains the HTTP status code returned by the backend. Using this header you can identify the HTTP status code returned by the application running in your backend without going through backend logs. This status code might be different from the HTTP status code in the response sent to the client by Front Door. This header allows you to determine if the backend is misbehaving or if the issue is with the Front Door service. |

| X-Azure-InternalError | This header contains the error code that Azure Front Door comes across when processing the request. This error indicates the issue is internal to the Azure Front Door service/infrastructure. Report issue to support.  |

| X-Azure-ExternalError | `X-Azure-ExternalError: 0x830c1011, The certificate authority is unfamiliar` </br> This header shows the error code that Front Door servers come across while establishing connectivity to the backend server to process a request. This header helps identify issues in the connection between Front Door and the backend application. This header includes a detailed error message to help you identify connectivity issues to your backend (for example, DNS resolution, invalid cert, and so on.). |

## Related content

- Learn how to [create an Azure Front Door profile](quickstart-create-front-door.md)

- Learn about [how Azure Front Door works](front-door-routing-architecture.md)


# Edge Locations By Abbreviation

# Azure Front Door POP Locations by Abbreviation

**Applies to:** :heavy_check_mark: Front Door Standard/Premium :heavy_check_mark: Front Door (classic) :heavy_check_mark: CDN Standard from Microsoft (classic)

This article provides a list of Azure Front Door point-of-presence (POP) locations, organized by their abbreviations.

## POP Locations

[!INCLUDE [front-door-edge-locations-by-abbreviation](../../includes/front-door-edge-locations-by-abbreviation.md)]

## Next Steps

* View Azure Front Door [POP locations by metro](edge-locations-by-region.md).

* Get the latest list of edge nodes for Azure Front Door from the [Edge Nodes List - REST API](/rest/api/cdn/edge-nodes/list).

* Learn how to [create an Azure Front Door (classic) profile](quickstart-create-front-door.md).

* Learn how to [create an Azure Front Door profile](standard-premium/create-front-door-portal.md).


# Front Door Quickstart Template Samples

# Bicep and Azure Resource Manager deployment model templates for Front Door

The following table includes links to Bicep and Azure Resource Manager deployment model templates for Azure Front Door.

| Sample | Description |

|-|-|

| [Front Door (quick create)](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium/) | Creates a basic Front Door profile including an endpoint, origin group, origin, and route.  |

| [Rule set](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium-rule-set/) | Creates a Front Door profile and rule set.  |

|**Custom domains**| **Description** |

| [Custom domain and managed TLS certificate](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium-custom-domain/) | Creates a Front Door profile with a custom domain and a Microsoft-managed TLS certificate.  |

| [Custom domain and customer-managed TLS certificate](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium-custom-domain-customer-certificate/) | Creates a Front Door profile with a custom domain and use your own TLS certificate by using Key Vault.  |

| [Custom domain and Azure DNS](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium-custom-domain-azure-dns/) | Creates a Front Door profile with a custom domain and an Azure DNS zone.  |

|**Web Application Firewall**| **Description** |

| [WAF policy with managed rule set](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-premium-waf-managed/) | Creates a Front Door profile and WAF with managed rule set.  |

| [WAF policy with custom rule](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium-waf-custom/) | Creates a Front Door profile and WAF with custom rule.  |

| [WAF policy with rate limit](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium-rate-limit/) | Creates a Front Door profile and WAF with a custom rule to perform rate limiting.  |

| [WAF policy with geo-filtering](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium-geo-filtering/) | Creates a Front Door profile and WAF with a custom rule to perform geo-filtering.  |

|**App Service origins**| **Description** |

| [App Service](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium-app-service-public) | Creates an App Service app with a public endpoint, and a Front Door profile.  |

| [App Service with Private Link](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-premium-app-service-private-link) | Creates an App Service app with a private endpoint, and a Front Door profile.  |

|**Azure Functions origins**| **Description** |

| [Azure Functions](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium-function-public/) | Creates an Azure Functions app with a public endpoint, and a Front Door profile.  |

|**API Management origins**| **Description** |

| [API Management (external)](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium-api-management-external) | Creates an API Management instance with external VNet integration, and a Front Door profile.  |

|**Storage origins**| **Description** |

| [Storage static website](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium-storage-static-website) | Creates an Azure Storage account and static website with a public endpoint, and a Front Door profile.  |

| [Storage blobs with Private Link](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-premium-storage-blobs-private-link) | Creates an Azure Storage account and blob container with a private endpoint, and a Front Door profile.  |

|**Application Gateway origins**| **Description** |

| [Application Gateway](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-standard-premium-application-gateway-public) | Creates an Application Gateway, and a Front Door profile. |

|**Virtual machine origins**| **Description** |

| [Virtual machine with Private Link service](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.cdn/front-door-premium-vm-private-link) | Creates a virtual machine and Private Link service, and a Front Door profile. |

| | |

| Template | Description |

| ---| ---|

| [Create a basic Front Door](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-create-basic)| Creates a basic Front Door configuration with a single backend. |

| [Create a Front Door with multiple backends and backend pools and URL based routing](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-create-multiple-backends)| Creates a Front Door with load balancing configured for multiple backends in a backend pool and also across backend pools based on URL path. |

| [Onboard a custom domain and managed TLS certificate with Front Door](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-custom-domain)| Add a custom domain to your Front Door and use a Front Door-managed TLS certificate. |

| [Onboard a custom domain and customer-managed TLS certificate with Front Door](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-custom-domain-customer-certificate)| Add a custom domain to your Front Door and use your own TLS certificate by using Key Vault. |

| [Create Front Door with geo filtering](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-geo-filtering)| Create a Front Door that allows/blocks traffic from certain countries/regions. |

| [Control Health Probes for your backends on Front Door](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-health-probes)| Update your Front Door to change the health probe settings by updating the probe path and also the intervals in which the probes will be sent. |

| [Create Front Door with Active/Standby backend configuration](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-priority-lb)| Creates a Front Door that demonstrates priority-based routing for Active/Standby application topology, that is, by default send all traffic to the primary (highest-priority) backend until it becomes unavailable. |

| [Create Front Door with caching enabled for certain routes](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-create-caching)| Creates a Front Door with caching enabled for the defined routing configuration thus caching any static assets for your workload. |

| [Configure Session Affinity for your Front Door host names](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-session-affinity) | Updates a Front Door to enable session affinity for your frontend host, thereby, sending subsequent traffic from the same user session to the same backend. |

| [Configure Front Door for client IP allowlisting or blocklisting](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-waf-clientip)| Configures a Front Door to restrict traffic certain client IPs using custom  access control using client IPs. |

| [Configure Front Door to take action with specific http parameters](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-waf-http-params)| Configures a Front Door to allow or block certain traffic based on the http parameters in the incoming request by using custom rules for access control using http parameters. |

| [Configure Front Door rate limiting](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-rate-limiting)| Configures a Front Door to rate limit incoming traffic for a given frontend host. |

| | |

## Next steps

- Learn how to [create a Front Door profile](standard-premium/create-front-door-portal.md).

- Learn how to [create a Front Door](quickstart-create-front-door.md).


# Terraform Samples

# Terraform deployment model templates for Front Door

The following table includes links to Terraform deployment model templates for Azure Front Door.

| Sample | Description |

|-|-|

|**App Service origins**| **Description** |

| [App Service](https://github.com/Azure/terraform/tree/master/quickstart/101-front-door-standard-premium) | Creates an App Service app and a Front Door profile.  |

|**Storage origins**| **Description** |

| [Storage blobs with Private Link](https://github.com/Azure/terraform/tree/master/quickstart/101-front-door-premium-storage-blobs-private-link) | Creates an Azure Storage account and blob container with a private endpoint, and a Front Door profile.  |

| | |

| Template | Description |

| ---| ---|

| [Create a basic Front Door](https://github.com/Azure/terraform/tree/master/quickstart/101-front-door-classic)| Creates a basic Front Door configuration with a single backend. |

| | |

## Next steps

- Learn how to [create a Front Door profile](standard-premium/create-front-door-portal.md).

- Learn how to [create a Front Door](quickstart-create-front-door.md).


# How To Add Security Headers

# Configure security headers with Azure Front Door Standard/Premium Rule Set

**Applies to:** :heavy_check_mark: Front Door Standard :heavy_check_mark: Front Door Premium

This article shows how to implement security headers to prevent browser-based vulnerabilities like HTTP Strict-Transport-Security (HSTS), X-XSS-Protection, Content-Security-Policy, or X-Frame-Options. Security-based attributes can also be defined with cookies.

The following example shows you how to add a Content-Security-Policy header to all incoming requests that matches the path in the Route. Here, we only allow scripts from our trusted site, `https://contoso.azure-api.net` to run on our application.

## Prerequisites

- Azure Front Door. For more information, see [Quickstart: Create a Front Door](create-front-door-portal.md).

- Review how to [Set up a Rule Set](how-to-configure-rule-set.md) if you're new to the Rule Set feature.

## Add a Content-Security-Policy header in Azure portal

1. Go to the Azure Front Door Standard/Premium profile and select **Rule Set** under **Settings.**

1. Select **Add** to add a new rule set. Give the Rule Set a **Name** and then provide a **Name** for the rule. Select **Add an Action** and then select **Response Header**.

1. Set the operator to **Append** to add this header as a response to all of the incoming requests for this route.

1. Add the header name: **Content-Security-Policy** and define the values this header should accept. In this scenario, we choose `"script-src 'self' https://contoso.azure-api.net"`.

1. After adding all the rules you want to your configuration, remember to associate the rule set with a route. This step is **required** for the rule set to take action.

> [!NOTE]

> In this scenario, we didn't add [match conditions](concept-rule-set-match-conditions.md) to the rule. All incoming requests that match the path defined in the associated route have this rule applied. To apply it only to a subset of those requests, add your specific **match conditions** to this rule.

> [!IMPORTANT]

> If you're using Web Application Firewall (WAF) with your Azure Front Door, and it blocks a request, HSTS headers won't be added to the request even if they're enabled on the Azure Front Door.

## Clean up resources

### Deleting a Rule

In the preceding steps, you configured Content-Security-Policy header with Rule set. If you no longer want a rule, you can select the **Rule Set** and then select **Delete rule**.

### Deleting a Rule Set

If you want to delete a Rule Set, make sure you disassociate it from all routes before deleting. For detailed guidance on deleting a rule set, see [Configure rule sets in Azure Front Door](how-to-configure-rule-set.md).

## Next step

To learn how to configure a Web Application Firewall for your Front Door, see:

> [!div class="nextstepaction"]

> [Web Application Firewall and Front Door](../../web-application-firewall/afds/afds-overview.md)
