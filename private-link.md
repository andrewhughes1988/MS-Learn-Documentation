# Private Link Overview

# What is Azure Private Link?

Azure Private Link enables you to access Azure PaaS Services (for example, Azure Storage and SQL Database) and Azure hosted customer-owned/partner services over a [private endpoint](private-endpoint-overview.md) in your virtual network.

Traffic between your virtual network and the service travels the Microsoft backbone network. Exposing your service to the public internet is no longer necessary. You can create your own [private link service](private-link-service-overview.md) in your virtual network and deliver it to your customers. Setup and consumption using Azure Private Link is consistent across Azure PaaS, customer-owned, and shared partner services.

> [!IMPORTANT]

> Azure Private Link is now generally available. Both Private Endpoint and Private Link service (service behind standard load balancer) are generally available. Different Azure PaaS will onboard to Azure Private Link at different schedules. See [Private Link availability](availability.md) for an accurate status of Azure PaaS on Private Link. For known limitations, see [Private Endpoint](private-endpoint-overview.md#limitations) and [Private Link Service](private-link-service-overview.md#limitations).

> [!NOTE]

> The feature Private Link Service Direct Connect, which allows you to connect to any privately routable destination IP address, is now in public preview. For more information and known limitations, see [Private Link Service Direct Connect](configure-private-link-service-direct-connect.md)

> [!NOTE]

> Azure Private Link is one of the services that make up the Network Foundations category in Azure. Other services in this category include [Azure DNS](../dns/dns-overview.md) and [Azure Virtual Networks](../virtual-network/virtual-networks-overview.md). Each service has its own unique features and use cases. For more information on this service category, see [Network Foundations](../networking/foundations/network-foundations-overview.md).

For scenarios that involve public internet PaaS traffic, configure [network security perimeter](network-security-perimeter-concepts.md) to set up a secure logical boundary. Network security perimeter restricts communication to services within its perimeter, and it allows nonperimeter public traffic through inbound and outbound access rules.

[!INCLUDE [network-security-perimeter-preview-message](../../includes/network-security-perimeter-preview-message.md)]

## Key benefits

Azure Private Link provides the following benefits:

- **Privately access services on the Azure platform**: Connect your virtual network using private endpoints to all services that can be used as application components in Azure. Service providers can render their services in their own virtual network and consumers can access those services in their local virtual network. The Private Link platform handles the connectivity between the consumer and services over the Azure backbone network.

- **On-premises and peered networks**: Access services running in Azure from on-premises over ExpressRoute private peering, VPN tunnels, and peered virtual networks using private endpoints. There's no need to configure ExpressRoute Microsoft peering or traverse the internet to reach the service. Private Link provides a secure way to migrate workloads to Azure.

- **Protection against data leakage**: A private endpoint is mapped to an instance of a PaaS resource instead of the entire service. Consumers can only connect to the specific resource. Access to any other resource in the service is blocked. This mechanism provides protection against data leakage risks.

- **Global reach**: Connect privately to services running in other regions. The consumer's virtual network could be in region A and it can connect to services behind Private Link in region B.

- **Extend to your own services**: Enable the same experience and functionality to render your service privately to consumers in Azure. By placing your service behind a standard Azure Load Balancer, you can enable it for Private Link. The consumer can then connect directly to your service using a private endpoint in their own virtual network. You can manage the connection requests using an approval call flow. Azure Private Link works for consumers and services belonging to different Microsoft Entra tenants.

> [!NOTE]

> Azure Private Link, along with Azure Virtual Network, span across [Azure Availability Zones](/azure/reliability/availability-zones-overview) and are therefore zone resilient. To provide high availability for the Azure resource using a private endpoint, ensure that resource is zone resilient.

## Availability

For information on Azure services that support Private Link, see [Azure Private Link availability](availability.md).

For the most up-to-date notifications, check the [Azure Private Link updates page](https://azure.microsoft.com/updates/?product=private-link).

## Logging and monitoring

Azure Private Link has integration with Azure Monitor. This combination allows:

- Archival of logs to a storage account.

- Streaming of events to your Event Hubs.

- Azure Monitor logging.

You can access the following information on Azure Monitor:

- **Private endpoint**:

- Data processed by the Private Endpoint  (IN/OUT)

- **Private Link service**:

- Data processed by the Private Link service (IN/OUT)

- NAT port availability

## Pricing

For pricing details, see [Azure Private Link pricing](https://azure.microsoft.com/pricing/details/private-link/).

## FAQs

For FAQs, see [Azure Private Link FAQs](private-link-faq.yml).

## Limits

For limits, see [Azure Private Link limits](../azure-resource-manager/management/azure-subscription-service-limits.md#azure-private-link-limits).

## Service Level Agreement

For service level agreement, see [SLA for Azure Private Link](https://azure.microsoft.com/support/legal/sla/private-link/v1_0/).

## Next steps

- [Quickstart: Create a Private Endpoint using Azure portal](create-private-endpoint-portal.md)

- [Quickstart: Create a Private Link service by using the Azure portal](create-private-link-service-portal.md)

- [Learn module: Introduction to Azure Private Link](/training/modules/introduction-azure-private-link/)


# Private Endpoint Overview

# What is a private endpoint?

A private endpoint is a network interface that uses a private IP address from your virtual network. This network interface connects you privately and securely to a service that's powered by Azure Private Link. By enabling a private endpoint, you're bringing the service into your virtual network.

The service could be an Azure service such as:

* Azure Storage

* Azure Cosmos DB

* Azure SQL Database

* Your own service, using [Private Link service](private-link-service-overview.md).

## Private endpoint properties

A private endpoint specifies the following properties:

|Property  |Description |

|---------|---------|

|Name    |    A unique name within the resource group.      |

|Subnet    |  The subnet to deploy, where the private IP address is assigned. For subnet requirements, see the [Limitations](#limitations) section later in this article.         |

|Private-link resource    |   The private-link resource to connect by using a resource ID or alias, from the list of available types. A unique network identifier is generated for all traffic that's sent to this resource.       |

|Target subresource   |      The subresource to connect. Each private-link resource type has various options to select based on preference.    |

|Connection approval method    |  Automatic or manual. Depending on the Azure role-based access control permissions, your private endpoint can be approved automatically. If you're connecting to a private-link resource without Azure role based permissions, use the manual method to allow the owner of the resource to approve the connection.        |

|Request message     |  You can specify a message for requested connections to be approved manually. This message can be used to identify a specific request.        |

|Connection status   |   A read-only property that specifies whether the private endpoint is active. Only private endpoints in an approved state can be used to send traffic. More available states: <li>*Approved*: The connection was automatically or manually approved and is ready to be used.<li>*Pending*: The connection was created manually and is pending approval by the private-link resource owner.<li>*Rejected*: The connection was rejected by the private-link resource owner.<li>*Disconnected*: The connection was removed by the private-link resource owner. The private endpoint becomes informative and should be deleted for cleanup. </br>|

As you're creating private endpoints, consider the following:

- Private endpoints enable connectivity between the customers from the same:

- Virtual network

- Regionally peered virtual networks

- Globally peered virtual networks

- On-premises environments that use [VPN](https://azure.microsoft.com/services/vpn-gateway/) or [Express Route](https://azure.microsoft.com/services/expressroute/)

- Services that are powered by Private Link

- Network connections can be initiated only by clients that are connecting to the private endpoint. Service providers don't have a routing configuration to create connections into service customers. Connections can be established in a single direction only.

- A read-only network interface is *automatically created* for the lifecycle of the private endpoint. The interface is assigned a dynamic private IP address from the subnet that maps to the private-link resource. The value of the private IP address remains unchanged for the entire lifecycle of the private endpoint.

- The private endpoint must be deployed in the same region and subscription as the virtual network.

- The private-link resource can be deployed in a different region than the one for the virtual network and private endpoint.

- Multiple private endpoints can be created with the same private-link resource. For a single network using a common DNS server configuration, the recommended practice is to use a single private endpoint for a specified private-link resource. Use this practice to avoid duplicate entries or conflicts in DNS resolution.

- Multiple private endpoints can be created on the same or different subnets within the same virtual network. There are limits to the number of private endpoints you can create in a subscription. For more information, see [Azure limits](../azure-resource-manager/management/azure-subscription-service-limits.md#azure-networking-limits).

- The subscription that contains the private link resource must be registered with the Microsoft network resource provider. The subscription that contains the private endpoint must also be registered with the Microsoft network resource provider. For more information, see [Azure Resource Providers](../azure-resource-manager/management/resource-providers-and-types.md).

## Private-link resource

A private-link resource is the destination target of a specified private endpoint. The following table lists the available resources that support a private endpoint:

| Private-link resource name | Resource type | Sub-resources |

| ---------------------------| ------------- | ------------- |

| Application Gateway | Microsoft.Network/applicationgateways |Frontend IP Configuration name|

| Azure AI Search | Microsoft.Search/searchServices | searchService |

| Foundry Tools | Microsoft.CognitiveServices/accounts | account |

| Azure API for FHIR (Fast Healthcare Interoperability Resources) | Microsoft.HealthcareApis/services | fhir |

| Azure API Management | Microsoft.ApiManagement/service | Gateway |

| Azure App Configuration | Microsoft.Appconfiguration/configurationStores | configurationStores |

| Azure App Service | Microsoft.Web/hostingEnvironments | hosting environment |

| Azure App Service | Microsoft.Web/sites | sites |

| Azure Attestation Service | Microsoft.Attestation/attestationProviders | standard |

| Azure Automation | Microsoft.Automation/automationAccounts | Webhook, DSCAndHybridWorker |

| Azure Backup | Microsoft.RecoveryServices/vaults | AzureBackup, AzureSiteRecovery |

| Azure Batch | Microsoft.Batch/batchAccounts | batchAccount, nodeManagement |

| Azure Cache for Redis | Microsoft.Cache/Redis | redisCache |

| Azure Cache for Redis Enterprise | Microsoft.Cache/redisEnterprise | redisEnterprise |

| Azure Container Apps | Microsoft.App/ManagedEnvironments | managedEnvironments |

| Azure Container Registry | Microsoft.ContainerRegistry/registries | registry |

| Azure Cosmos DB | Microsoft.AzureCosmosDB/databaseAccounts | SQL, MongoDB, Cassandra, Gremlin, Table |

| Azure Cosmos DB for MongoDB vCore | Microsoft.DocumentDb/mongoClusters | mongoCluster |

| Azure Cosmos DB for PostgreSQL | Microsoft.DBforPostgreSQL/serverGroupsv2 | coordinator |

| Azure Data Explorer | Microsoft.Kusto/clusters | cluster |

| Azure Data Factory | Microsoft.DataFactory/factories | dataFactory |

| Azure Database for MariaDB | Microsoft.DBforMariaDB/servers | mariadbServer |

| Azure Database for MySQL - Flexible Server | Microsoft.DBforMySQL/flexibleServers | mysqlServer |

| Azure Database for MySQL - Single Server | Microsoft.DBforMySQL/servers | mysqlServer |

| Azure Database for PostgreSQL - Flexible server | Microsoft.DBforPostgreSQL/flexibleServers | postgresqlServer |

| Azure Database for PostgreSQL - Single server | Microsoft.DBforPostgreSQL/servers | postgresqlServer |

| Azure Databricks | Microsoft.Databricks/workspaces | databricks_ui_api, browser_authentication |

| Azure Device Provisioning Service | Microsoft.Devices/provisioningServices | iotDps |

| Azure Digital Twins | Microsoft.DigitalTwins/digitalTwinsInstances | API |

| Azure Durable Task Scheduler | Microsoft.DurableTask/schedulers | scheduler |

| Azure Event Grid | Microsoft.EventGrid/domains | domain |

| Azure Event Grid | Microsoft.EventGrid/topics  | topic |

| Azure Event Hub | Microsoft.EventHub/namespaces | namespace |

| Azure File Sync | Microsoft.StorageSync/storageSyncServices | File Sync Service |

| Azure HDInsight | Microsoft.HDInsight/clusters | cluster |

| Azure IoT Central | Microsoft.IoTCentral/IoTApps | IoTApps |

| Azure IoT Hub | Microsoft.Devices/IotHubs | iotHub |

| Azure Key Vault | Microsoft.KeyVault/vaults | vault |

| Azure Key Vault HSM (hardware security module) | Microsoft.Keyvault/managedHSMs | HSM |

| Azure Kubernetes Service - Kubernetes API | Microsoft.ContainerService/managedClusters | management |

| Azure Machine Learning | Microsoft.MachineLearningServices/registries | amlregistry |

| Azure Machine Learning | Microsoft.MachineLearningServices/workspaces | amlworkspace |

| Azure Managed Disks | Microsoft.Compute/diskAccesses | managed disk |

| Azure Managed Redis | Microsoft.Cache/redisEnterprise | redisEnterprise |

| Azure Media Services | Microsoft.Media/mediaservices | keydelivery, liveevent, streamingendpoint |

| Azure Migrate | Microsoft.Migrate/assessmentProjects | project |

| Azure Monitor Private Link Scope | Microsoft.Insights/privatelinkscopes | azuremonitor |

| Azure Relay | Microsoft.Relay/namespaces | namespace |

| Azure Service Bus | Microsoft.ServiceBus/namespaces | namespace |

| Azure SignalR Service | Microsoft.SignalRService/SignalR | signalr |

| Azure SignalR Service | Microsoft.SignalRService/webPubSub | webpubsub |

| Azure SQL Database | Microsoft.Sql/servers | SQL Server (sqlServer) |

| Azure SQL Managed Instance | Microsoft.Sql/managedInstances | managedInstance |

| Azure Static Web Apps | Microsoft.Web/staticSites | staticSites |

| Azure Storage | Microsoft.Storage/storageAccounts | Blob (blob, blob_secondary)<BR> Table (table, table_secondary)<BR> Queue (queue, queue_secondary)<BR> File (file, file_secondary)<BR> Web (web, web_secondary)<BR> Dfs (dfs, dfs_secondary) |

| Azure Synapse | Microsoft.Synapse/privateLinkHubs | web |

| Azure Synapse Analytics | Microsoft.Synapse/workspaces | Sql, SqlOnDemand, Dev |

| Azure AI Video Indexer | Microsoft.VideoIndexer/accounts | account |

| Azure Virtual Desktop - host pools | Microsoft.DesktopVirtualization/hostpools | connection |

| Azure Virtual Desktop - workspaces | Microsoft.DesktopVirtualization/workspaces | feed<br />global |

| Device Update for IoT Hub | Microsoft.DeviceUpdate/accounts | DeviceUpdate |

| Integration Account (Premium) | Microsoft.Logic/integrationAccounts | integrationAccount |

| Microsoft Purview | Microsoft.Purview/accounts | account |

| Microsoft Purview | Microsoft.Purview/accounts | portal |

| Power BI | Microsoft.PowerBI/privateLinkServicesForPowerBI | Power BI |

| Private Link service (your own service) |  Microsoft.Network/privateLinkServices | empty |

| Resource Management Private Links | Microsoft.Authorization/resourceManagementPrivateLinks | ResourceManagement |

> [!NOTE]

> You can create private endpoints only on a General Purpose v2 (GPv2) storage account.

## Network security of private endpoints

When you use private endpoints, traffic is secured to a private-link resource. The platform validates network connections, allowing only those that reach the specified private-link resource. To access more subresources within the same Azure service, more private endpoints with corresponding targets are required. In the case of Azure Storage, for instance, you would need separate private endpoints to access the *file* and *blob* subresources.

Private endpoints provide a privately accessible IP address for the Azure service, but don't necessarily restrict public network access to it. All other Azure services require additional [access controls](../event-hubs/event-hubs-ip-filtering.md), however. These controls provide an extra network security layer to your resources, providing protection that helps prevent access to the Azure service associated with the private-link resource.

Private endpoints support network policies. Network policies enable support for Network Security Groups (NSG), User Defined Routes (UDR), and Application Security Groups (ASG). For more information about enabling network policies for a private endpoint, see [Manage network policies for private endpoints](disable-private-endpoint-network-policy.md). To use an ASG with a private endpoint, see [Configure an application security group (ASG) with a private endpoint](configure-asg-private-endpoint.md).

## Access to a private-link resource using approval workflow

You can connect to a private-link resource by using the following connection approval methods:

- **Automatically approve**: Use this method when you own or have permissions for the specific private-link resource. The required permissions are based on the private-link resource type in the following format:

`Microsoft.<Provider>/<resource_type>/privateEndpointConnectionsApproval/action`

- **Manually request**: Use this method when you don't have the required permissions and want to request access. An approval workflow is initiated. The private endpoint and later private-endpoint connections are created in a *Pending* state. The private-link resource owner is responsible to approve the connection. After it's approved, the private endpoint is enabled to send traffic normally, as shown in the following approval workflow diagram:

Over a private-endpoint connection, a private-link resource owner can:

- Review all private-endpoint connection details.

- Approve a private-endpoint connection. The corresponding private endpoint is enabled to send traffic to the private-link resource.

- Reject a private-endpoint connection. The corresponding private endpoint is updated to reflect the status.

- Delete a private-endpoint connection in any state. The corresponding private endpoint is updated with a disconnected state to reflect the action. The private-endpoint owner can delete only the resource at this point.

> [!NOTE]

> Only private endpoints in an *Approved* state can send traffic to a specified private-link resource.

### Connect by using an alias

An alias is a unique moniker that's generated when a service owner creates a private-link service behind a standard load balancer. Service owners can share this alias offline with consumers of your service.

The consumers can request a connection to a private-link service by using either the resource URI or the alias. To connect by using the alias, create a private endpoint by using the manual connection approval method. To use the manual connection approval method, set the manual request parameter to *True* during the private-endpoint create flow. For more information, see [New-AzPrivateEndpoint](/powershell/module/az.network/new-azprivateendpoint) and [az network private-endpoint create](/cli/azure/network/private-endpoint#az-network-private-endpoint-create).

> [!NOTE]

> This manual request can be auto approved if the consumer's subscription is allow-listed on the provider side. To learn more, go to [controlling service access](./private-link-service-overview.md#control-service-access).

## DNS configuration

The DNS settings that you use to connect to a private-link resource are important. Existing Azure services might already have a DNS configuration you can use when you're connecting over a public endpoint. To connect to the same service over private endpoint, separate DNS settings, often configured via private DNS zones, are required. Ensure that your DNS settings are correct when you use the fully qualified domain name (FQDN) for the connection. The settings must resolve to the private IP address of the private endpoint.

The network interface associated with the private endpoint contains the information that's required to configure your DNS. The information includes the FQDN and private IP address for a private-link resource.

For complete, detailed information about recommendations to configure DNS for private endpoints, see [Private endpoint DNS configuration](private-endpoint-dns.md).

## Limitations

The following information lists the known limitations to the use of private endpoints:

### Static IP address

| Limitation | Description |

| --------- | ------------ |

| Static IP address configuration currently unsupported. | **Azure Kubernetes Service (AKS)** </br> **Azure Application Gateway** </br> **HD Insight** </br> **Recovery Services Vaults** </br> **Third party Private Link services** |

### Network security group

| Limitation | Description |

| --------- | ------------ |

| Effective routes and security rules unavailable for private endpoint network interface. | Effective routes and security rules won't be displayed for the private endpoint NIC in the Azure portal. |

| NSG flow logs unsupported. | NSG flow logs unavailable for inbound traffic destined for a private endpoint. |

| No more than 50 members in an Application Security Group. | Fifty is the number of IP Configurations that can be tied to each respective ASG that's coupled to the NSG on the private endpoint subnet. Connection failures may occur with more than 50 members. |

| Destination port ranges supported up to a factor of 250 K. | Destination port ranges are supported as a multiplication SourceAddressPrefixes, DestinationAddressPrefixes, and DestinationPortRanges. </br></br> Example inbound rule: </br> One source * one destination * 4K portRanges = 4K Valid </br>  10 sources * 10 destinations * 10 portRanges = 1 K Valid </br> 50 sources * 50 destinations * 50 portRanges = 125 K Valid </br> 50 sources * 50 destinations * 100 portRanges = 250 K Valid </br> 100 sources * 100 destinations * 100 portRanges = 1M Invalid, NSG has too many sources/destinations/ports. |

| Source port filtering is interpreted as * | Source port filtering isn't actively used as valid scenario of traffic filtering for traffic destined to a private endpoint. |

| Feature unavailable in select regions. | Currently unavailable in the following regions: </br> West India </br> Australia Central 2 </br> South Africa West </br> Brazil Southeast </br> All Government regions </br> All China regions |

### NSG more considerations

- Outbound traffic denied from a private endpoint isn't a valid scenario, as the service provider can't originate traffic.

- The following services may require all destination ports to be open when using a private endpoint and adding NSG security filters:

- Azure Cosmos DB - For more information, see [Service port ranges](/azure/cosmos-db/sql/sql-sdk-connection-modes#service-port-ranges).

### UDR

| Limitation | Description |

| --------- | --------- |

| SNAT is recommended. | Due to the variable nature of the private endpoint data-plane, it's recommended to SNAT traffic destined to a private endpoint to ensure return traffic is honored when going through an NVA. This limitation can be removed using [disableSnatOnPL tag](/azure/private-link/private-link-disable-snat) in your NVA. |

| Feature unavailable in select regions. | Currently unavailable in the following regions: </br> West India </br> Australia Central 2 </br> South Africa West </br> Brazil Southeast |

### Application security group

| Limitation | Description |

| --------- | --------- |

| Feature unavailable in select regions. | Currently unavailable in the following regions: </br> West India </br> Australia Central 2 </br> South Africa West </br> Brazil Southeast |

## Next steps

- For more information about private endpoints and Private Link, see [What is Azure Private Link?](private-link-overview.md)

- To get started with creating a private endpoint for a web app, see [Quickstart: Create a private endpoint by using the Azure portal](create-private-endpoint-portal.md).


# Private Link Service Overview

# What is Azure Private Link service?

Azure Private Link service is the reference to your own service that is powered by Azure Private Link. Your service that is running behind [Azure Standard Load Balancer](../load-balancer/load-balancer-overview.md) can be enabled for Private Link access so that consumers to your service can access it privately from their own VNets. Your customers can create a private endpoint inside their virtual network and map it to this service. This article explains concepts related to the service provider side.

*Figure: Azure Private Link Service.*

> [!IMPORTANT]

> The feature Private Link Service Direct Connect, which allows you to connect to any privately routable destination IP address, is now in public preview. For more information and known limitations, see [Private Link Service Direct Connect](configure-private-link-service-direct-connect.md)

## Workflow

*Figure: Azure Private Link service workflow.*

### Create your Private Link Service

- Configure your application to run behind a standard load balancer in your virtual network. If you already have your application configured behind a standard load balancer, you can skip this step.

- Create a Private Link Service referencing the load balancer above. In the load balancer selection process, choose the frontend IP configuration where you want to receive the traffic. Choose a subnet for NAT IP addresses for the Private Link Service. It's recommended to have at least eight NAT IP addresses available in the subnet. All consumer traffic will appear to originate from this pool of private IP addresses to the service provider. Choose the appropriate properties/settings for the Private Link Service.

> [!NOTE]

> Azure Private Link Service is only supported on Standard Load Balancer.

### Share your service

After you create a Private Link service, Azure will generate a globally unique named moniker called **alias** based on the name you provide for your service. You can share either the alias or resource URI of your service with your customers offline. Consumers can start a Private Link connection using the alias or the resource URI.

### Manage your connection requests

After a consumer initiates a connection, the service provider can accept or reject the connection request. All connection requests will be listed under the **privateendpointconnections** property on the Private Link service.

### Delete your service

If the Private Link service is no longer in use, you can delete it. However, before you delete the service, ensure that there are no private endpoint connections associated with it. You can reject all connections and delete the service.

## Properties

A Private Link service specifies the following properties:

|Property |Explanation  |

|---------|---------|

|Provisioning State (provisioningState)  |A read-only property that lists the current provisioning state for Private Link service. Applicable provisioning states are: **Deleting**, **Failed**,**Succeeded**,***Updating**. When the provisioning state is **Succeeded**, you've successfully provisioned your Private Link service.        |

|Alias (alias)     | Alias is a globally unique read-only string for your service. It helps you mask the customer data for your service and at the same time creates an easy-to-share name for your service. When you create a Private Link service, Azure generates the alias for your service that you can share with your customers. Your customers can use this alias to request a connection to your service.          |

|Visibility (visibility)     | Visibility is the property that controls the exposure settings for your Private Link service. Service providers can choose to limit the exposure to their service to subscriptions with Azure role-based access control permissions. A restricted set of subscriptions can also be used to limit exposure.         |

|Auto Approval (autoApproval)    |   Auto-approval controls the automated access to the Private Link service. The subscriptions specified in the auto-approval list are approved automatically when a connection is requested from private endpoints in those subscriptions.          |

|Load balancer frontend IP configuration (loadBalancerFrontendIpConfigurations)    |    Private Link service is tied to the frontend IP address of a Standard Load Balancer. All traffic destined for the service will reach the frontend of the SLB. You can configure SLB rules to direct this traffic to appropriate backend pools where your applications are running. Load balancer frontend IP configurations are different than NAT IP configurations.      |

|NAT IP configuration (ipConfigurations)    |    This property refers to the NAT (Network Address Translation) IP configuration for the Private Link service. The NAT IP can be chosen from any subnet in a service provider's virtual network. Private Link service performs destination side NAT-ing on the Private Link traffic. This NAT ensures that there's no IP conflict between source (consumer side) and destination (service provider) address space. On the destination or service provider side, the NAT IP address displays as **source IP** for all packets received by your service. **Destination IP** is displayed for all packets sent by your service.       |

|Private endpoint connections (privateEndpointConnections)     |  This property lists the private endpoints connecting to Private Link service. Multiple private endpoints can connect to the same Private Link service and the service provider can control the state for individual private endpoints.        |

|TCP Proxy V2 (EnableProxyProtocol)     |  This property lets the service provider use tcp proxy v2 to retrieve connection information about the service consumer. Service Provider is responsible for setting up receiver configs to be able to parse the proxy protocol v2 header.        |

### Details

- Private Link service can be accessed from approved private endpoints in any public region. The private endpoint can be reached from the same virtual network and regionally peered virtual networks. The private endpoint can be reached from globally peered virtual networks and on premises using private VPN or ExpressRoute connections.

- Upon creation of a Private Link Service, a network interface is created for the lifecycle of the resource. This interface isn't manageable by the customer.

- The Private Link Service must be deployed in the same region as the virtual network and the Standard Load Balancer.

- A single Private Link Service can be accessed from multiple Private Endpoints belonging to different virtual networks, subscriptions and/or Microsoft Entra tenants. The connection is established through a connection workflow.

- Multiple Private Link services can be created on the same Standard Load Balancer using different front-end IP configurations. There are limits to the number of Private Link services you can create per Standard Load Balancer and per subscription. For details, see [Azure limits](../azure-resource-manager/management/azure-subscription-service-limits.md#azure-networking-limits).

- Private Link service can have more than one NAT IP configurations linked to it. Choosing more than one NAT IP configurations can help service providers to scale. Today, service providers can assign up to eight NAT IP addresses per Private Link service. With each NAT IP address, you can assign more ports for your TCP connections and thus scale out. You can add multiple NAT IP addresses to a Private Link service, but you must maintain at least one NAT IP address once configured. You will be restricted from deleting the last remaining NAT IP to ensure that active connections aren't impacted as a result of unavailable NAT IP addresses.

## Alias

**Alias** is a globally unique name for your service. It helps you mask the customer data for your service and at the same time creates an easy-to-share name for your service. When you create a Private Link service, Azure generates an alias for your service that you can share with your customers. Your customers can use this alias to request a connection to your service.

The alias is composed of three parts: *Prefix*.*GUID*.*Suffix*

- Prefix is the service name. You can pick your own prefix. After "Alias" is created, you can't change it, so select your prefix appropriately.

- GUID will be provided by platform. This GUID makes the name globally unique.

- Suffix is appended by Azure: *region*.azure.privatelinkservice

Complete alias:  *Prefix*. {GUID}.*region*.azure.privatelinkservice

## Control service exposure

The Private Link service provides you with three options in the **Visibility** setting to control the exposure of your service. Your visibility setting determines whether a consumer can connect to your service. Here are the visibility setting options, from most restrictive to least restrictive:

- **Role-based access control only**: If your service is for private consumption from different virtual networks that you own, use role-based access control inside subscriptions that are associated with the same Microsoft Entra tenant. **Cross tenant visibility is permitted through role-based access control**.

- **Restricted by subscription**: If your service will be consumed across different tenants, you can restrict the exposure to a limited set of subscriptions that you trust. Authorizations can be pre-approved.

- **Anyone with your alias**: If you want to make your service public and allow anyone with your Private Link service alias to request a connection, select this option.

## Control service access

Consumers having exposure controlled by visibility setting to your Private Link service can create a private endpoint in their virtual networks and request a connection to your Private Link service. The private endpoint connection will be created in a **Pending** state on the Private Link service object. The service provider is responsible for acting on the connection request. You can either approve the connection, reject the connection, or delete the connection. Only connections that are approved can send traffic to the Private Link service.

The action of approving the connections can be automated by using the auto-approval property on the Private Link service. Auto-Approval is an ability for service providers to preapprove a set of subscriptions for automated access to their service. Customers will need to share their subscriptions offline for service providers to add to the auto-approval list. Auto-approval is a subset of the visibility array.

Visibility controls the exposure settings whereas auto-approval controls the approval settings for your service. If a customer requests a connection from a subscription in the auto-approval list, the connection is automatically approved, and the connection is established. Service providers don’t need to manually approve the request. If a customer requests a connection from a subscription in the visibility array and not in the auto-approval array, the request will reach the service provider. The service provider must manually approve the connections.

## Getting connection Information using TCP Proxy v2

> [!NOTE]

> TCP Proxy v2 configuration on a Private Link service activates for all load balancers and their backend VMs. If TCP Proxy v2 is configured on one PLS, configure it on other PLS resources if they are sharing the same load balancer or backend pool, otherwise health probes will fail.

In the private link service, the source IP address of the packets coming from private endpoint is network address translated (NAT) on the service provider side using the NAT IP allocated from the provider's virtual network. The applications receive the allocated NAT IP address instead of actual source IP address of the service consumers. If your application needs an actual source IP address from the consumer side, you can enable proxy protocol on your service and retrieve the information from the proxy protocol header. In addition to source IP address, proxy protocol header also carries the LinkID of the private endpoint. Combination of source IP address and LinkID can help service providers uniquely identify their consumers.

For more information on Proxy Protocol, visit [here](https://www.haproxy.org/download/1.8/doc/proxy-protocol.txt).

This information is encoded using a custom Type-Length-Value (TLV) vector as follows:

Custom TLV details:

|Field |Length (Octets)  |Description  |

|---------|---------|----------|

|Type  |1        |PP2_TYPE_AZURE (0xEE)|

|Length  |2      |Length of value|

|Value  |1     |PP2_SUBTYPE_AZURE_PRIVATEENDPOINT_LINKID (0x01)|

|  |4        |UINT32 (4 bytes) representing the LINKID of the private endpoint. Encoded in little endian format.|

> [!NOTE]

> The service provider is responsible for making sure that the service behind the standard load balancer is configured to parse the proxy protocol header as per the [specification](https://www.haproxy.org/download/1.8/doc/proxy-protocol.txt) when proxy protocol is enabled on private link service. The request will fail if proxy protocol setting is enabled on private link service but the service provider's service is not configured to parse the header. The request will fail if the service provider's service is expecting a proxy protocol header while the setting is not enabled on the private link service. Once proxy protocol setting is enabled, proxy protocol header will also be included in HTTP/TCP health probes from host to the backend virtual machines. Client information isn't contained in the header.

The matching `LINKID` that is part of the PROXYv2 (TLV) protocol can be found at the `PrivateEndpointConnection` as property `linkIdentifier`.

For more information, see [Private Link Services API](/../../../rest/api/virtualnetwork/private-link-services/get-private-endpoint-connection#privateendpointconnection).

## Limitations

The following are the known limitations when using the Private Link service:

- Supported only on Standard Load Balancer. Not supported on Basic Load Balancer.

- Supported only on Standard Load Balancer where backend pool is configured by NIC. Not supported on Standard Load Balancer where backend pool is configured by IP address.

- Supports IPv4 traffic only

- Supports TCP and UDP traffic only

- Private Link Service has an idle timeout of ~5 minutes (300 seconds). To avoid hitting this limit, applications connecting through Private Link Service must use TCP Keepalives lower than that time.

- For an Inbound NAT rule with type set to *backend pool* to operate with Azure Private Link Service, a load balancing rule must be configured.

- TCP Proxy v2 configuration on a Private Link service activates for all load balancers and their backend VMs. If TCP Proxy v2 is configured on one PLS, configure it on other PLS resources if they are sharing the same load balancer or backend pool, otherwise health probes will fail.

## Next steps

- [Create a private link service using Azure PowerShell](create-private-link-service-powershell.md)

- [Create a private link service using Azure CLI](create-private-link-service-cli.md)


# Create Private Link Service Portal

# Quickstart: Create a Private Link service by using the Azure portal

Get started creating a Private Link service that refers to your service. Give Private Link access to your service or resource deployed behind an Azure Standard Load Balancer. Users of your service have private access from their virtual network.

## Prerequisites

* An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## <a name="create-a-virtual-network"></a> Sign in to Azure

Sign in to the [Azure portal](https://portal.azure.com) with your Azure account.

[!INCLUDE [virtual-network-create.md](~/reusable-content/ce-skilling/azure/includes/virtual-network-create.md)]

### Create load balancer

Create an internal load balancer that load balances virtual machines.

During the creation of the load balancer, you configure:

* Frontend IP address

* Backend pool

* Inbound load-balancing rules

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

1. In the **Load balancer** page, select **+ Create**.

1. In the **Basics** tab of the **Create load balancer** page, enter, or select the following information:

| Setting              | Value                                |

|----------------------|--------------------------------------|

| **Project details**  |                                      |

| Subscription         | Select your subscription.            |

| Resource group       | Select **test-rg**. |

| **Instance details** |                                      |

| Name                 | Enter **load-balancer**             |

| Region               | Select **East US 2**.           |

| SKU                  | Leave the default **Standard**.      |

| Type                 | Select **Internal**.                 |

| Tier                 | Select **Regional**.                 |

1. Select **Next: Frontend IP configuration**.

1. In **Frontend IP configuration**, select **+ Add a frontend IP configuration**.

1. Enter or select the following information in **Add frontend IP configuration**.

| Setting | Value |

| ------- | ----- |

| Name | Enter **frontend**.|

| Virtual network | Select **vnet-1 (test-rg)**. |

| Subnet | Select **subnet-1 (10.0.0.0/24)**. |

| Assignment | Leave the default of **Dynamic**. |

| Availability zone | Leave the default of **Zone-redundant**. |

> [!NOTE]

> In regions with [Availability Zones](/azure/reliability/availability-zones-overview?toc=%2fazure%2fvirtual-network%2ftoc.json), you have the option to select no-zone (default option), a specific zone, or zone-redundant. The choice will depend on your specific domain failure requirements. In regions without Availability Zones, this field won't appear. </br> For more information on availability zones, see [Availability zones overview](/azure/reliability/availability-zones-overview).

1. Select **Add**.

1. Select **Next: Backend pools**.

1. In **Backend pools**, select **+ Add a backend pool**.

1. Enter **backend-pool** for **Name**.

1. Select **NIC** for **Backend Pool Configuration**.

> [!NOTE]

> Private Link service is supported on Standard Load Balancers with backend pools configured by NICs. It is not supported when backend pools are configured using IP addresses. For more information, see [Private Link service limitations](private-link-service-overview.md#limitations).

1. Select **Save**.

1. Select **Next: Inbound rules**.

1. In **Load balancing rule**, select **+ Add a load balancing rule**.

1. In **Add load balancing rule**, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| Name | Enter **http-rule** |

| IP Version | Select **IPv4** or **IPv6** depending on your requirements. |

| Frontend IP address | Select **frontend**. |

| Backend pool | Select **backend-pool**. |

| Protocol | Select **TCP**. |

| Port | Enter **80**. |

| Backend port | Enter **80**. |

| Health probe | Select **Create new**. </br> In **Name**, enter **health-probe**. </br> Select **HTTP** in **Protocol**. </br> Leave the rest of the defaults, and select **Save**. |

| Session persistence | Select **None**. |

| Idle timeout (minutes) | Enter or select **15**. |

| Enable TCP Reset | Select the box. |

| Enable Floating IP | Leave the box unchecked. |

1. Select **Save**.

1. Select the blue **Review + create** button.

1. Select **Create**.

## Create a private link service

Create a Private Link service behind the load balancer you created in the previous section.

1. In the search box at the top of the portal, enter **Private link**. Select **Private link services** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource Group | Select **test-rg**. |

| **Instance details** |  |

| Name | Enter **private-link-service**. |

| Region | Select **East US 2**. |

1. Select **Next: Outbound settings**.

1. In the **Outbound settings** tab, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| Load balancer | Select **load-balancer**. |

| Load balancer frontend IP address | Select **frontend (10.0.0.4)**. |

| Source NAT subnet | Select **vnet-1/subnet-1 (10.0.0.0/24)**. |

| Enable TCP proxy V2 | Leave the default of **No**. </br> If your application expects a TCP proxy v2 header, select **Yes**. |

| **Private IP address settings** |  |

| Leave the default settings |  |

1. Select **Next: Access security**.

1. Leave the default of **Role-based access control only** in the **Access security** tab.

1. Select **Next: Tags**.

1. Select **Next: Review + create**.

1. Select **Create**.

Your private link service is created and can receive traffic. If you want to see traffic flows, configure your application behind your standard load balancer.

## Create private endpoint

In this section, you map the private link service to a private endpoint. A virtual network contains the private endpoint for the private link service. This virtual network contains the resources that access your private link service.

### Create private endpoint virtual network

Repeat steps in [Create a virtual network](#create-a-virtual-network) to create a virtual network with the following settings:

| Setting | Value |

| ------- | ----- |

| Name | **vnet-pe** |

| Location | **East US 2** |

| Address space | **10.1.0.0/16** |

| Subnet name | **subnet-pe** |

| Subnet address range | **10.1.0.0/24** |

### Create private endpoint

1. In the search box at the top of the portal, enter **Private endpoint**. Select **Private endpoints** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** | |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. You created this resource group in the previous section.|

| **Instance details** |  |

| Name  | Enter **private-endpoint**. |

| Network Interface Name | Leave the default of **private-endpoint-nic**. |

| Region | Select **East US 2**. |

1. Select **Next: Resource**.

1. In the **Resource** tab, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| Connection method | Select **Connect to an Azure resource in my directory**. |

| Subscription | Select your subscription. |

| Resource type | Select **Microsoft.Network/privateLinkServices**. |

| Resource | Select **private-link-service**. |

1. Select **Next: Virtual Network**.

1. In **Virtual Network**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| **Networking** |  |

| Virtual network | Select **vnet-pe (test-rg)**. |

| Subnet | Select **subnet-pe**. |

| Network policy for private endpoints | Select **edit** to apply Network policy for private endpoints. </br> In **Edit subnet network policy**, in **Network policies setting for all private endpoints in this subnet**, select **Network security groups** and **Route Tables**. </br> Select **Save**. </br></br>For more information, see [Manage network policies for private endpoints](disable-private-endpoint-network-policy.md) |

# [**Dynamic IP**](#tab/dynamic-ip)

| Setting | Value |

| ------- | ----- |

| **Private IP configuration** | Select **Dynamically allocate IP address**. |

# [**Static IP**](#tab/static-ip)

| Setting | Value |

| ------- | ----- |

| **Private IP configuration** | Select **Statically allocate IP address**. |

| Name | Enter **ipconfig-1**. |

| Private IP | Enter **10.1.0.10**. |

---

1. Select **Next: DNS**.

1. Select **Next: Tags**.

1. Select **Next: Review + create**.

1. Select **Create**.

### IP address of private endpoint

In this section, you find the IP address of the private endpoint that corresponds with the load balancer and private link service. The following steps are only necessary if you selected **Dynamically allocate IP address** in the previous section.

1. Enter **test-rg** in the search box at the top of the portal. Select **test-rg** in the search results in **Resource Groups**.

1. In the **test-rg** resource group, select **private-endpoint**.

1. In the **Overview** page of **private-endpoint**, select the name of the network interface associated with the private endpoint. The network interface name begins with **private-endpoint.nic**.

1. In the **Overview** page of the private endpoint nic, the IP address of the endpoint is displayed in **Private IP address**.

[!INCLUDE [portal-clean-up.md](~/reusable-content/ce-skilling/azure/includes/portal-clean-up.md)]

## Next steps

In this quickstart, you:

* Created a virtual network and internal Azure Load Balancer.

* Created a private link service.

* Created a virtual network and a private endpoint for the private link service.

To learn more about Azure Private endpoint, continue to:

> [!div class="nextstepaction"]

> [Quickstart: Create a Private Endpoint using the Azure portal](create-private-endpoint-portal.md)


# Create Private Endpoint Portal

# Quickstart: Create a private endpoint by using the Azure portal

Get started with Azure Private Link by creating and using a private endpoint to connect securely to an Azure web app.

In this quickstart, create a private endpoint for an Azure App Services web app and then create and deploy a virtual machine (VM) to test the private connection.

You can create private endpoints for various Azure services, such as Azure SQL and Azure Storage.

## Prerequisites

- An Azure account with an active subscription. If you don't already have an Azure account, [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An Azure App Services web app with a Basic, Standard, PremiumV2, PremiumV3, IsolatedV2, Functions Premium (sometimes referred to as the Elastic Premium plan) app service plan, deployed in your Azure subscription.

- For more information and an example, see [Quickstart: Create an ASP.NET Core web app in Azure](../app-service/quickstart-dotnetcore.md).

- The example webapp in this article is named **webapp-1**. Replace the example with your webapp name.

## Sign in to Azure

Sign in to the [Azure portal](https://portal.azure.com).

## Create a resource group

1. In the portal, search for and select **Resource groups**.

1. Select **+ Create**.

1. In the **Basics** tab of **Create a resource group**, enter, or select the following information:

| Setting | Value |

| ------- | ----- |

| Subscription | Select your subscription. |

| Resource group | Enter **test-rg**. |

| Region | Select **East US 2**. |

1. Select **Review + create**.

1. Select **Create**.

## Create a virtual network

The following procedure creates a virtual network with a resource subnet.

1. In the portal, search for and select **Virtual networks**.

1. On the **Virtual networks** page, select **+ Create**.

1. On the **Basics** tab of **Create virtual network**, enter, or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |  |

| Name | Enter **vnet-1**. |

| Region | Select **East US 2**. |

1. Select **Next** to proceed to the **Security** tab.

1. Select **Next** to proceed to the **IP Addresses** tab.

1. In the address space box in **Subnets**, select the **default** subnet.

1. In **Edit subnet**, enter or select the following information:

| Setting | Value |

|---|---|

| **Subnet details** |  |

| Subnet template | Leave the default **Default**. |

| Name | Enter **subnet-1**. |

| Starting address | Leave the default of **10.0.0.0**. |

| Subnet size | Leave the default of **/24 (256 addresses)**. |

1. Select **Save**.

1. Select **Review + create** at the bottom of the screen, and when validation passes, select **Create**.

## Deploy Azure Bastion

Azure Bastion uses your browser to connect to VMs in your virtual network over Secure Shell (SSH) or Remote Desktop Protocol (RDP) by using their private IP addresses. The VMs don't need public IP addresses, client software, or special configuration. For more information about Azure Bastion, see [Azure Bastion](/azure/bastion/bastion-overview).

>[!NOTE]

>[!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

1. In the search box at the top of the portal, enter **Bastion**. Select **Bastions** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab of **Create a Bastion**, enter, or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |  |

| Name | Enter **bastion**. |

| Region | Select **East US 2**. |

| Tier | Select **Developer**. |

| **Configure virtual networks** |  |

| Virtual network | Select **vnet-1**. |

1. Select **Review + create**.

1. Select **Create**.

## Create a private endpoint

Next, you create a private endpoint for the web app that you created in the **Prerequisites** section.

> [!IMPORTANT]

> You must have a previously deployed Azure App Services web app to proceed with the steps in this article. For more information, see [Prerequisites](#prerequisites) .

1. In the search box at the top of the portal, enter **Private endpoint**. Select **Private endpoints**.

1. Select **+ Create** in **Private endpoints**.

1. In the **Basics** tab of **Create a private endpoint**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** |

| **Instance details** |   |

| Name | Enter **private-endpoint**. |

| Network Interface Name | Leave the default of **private-endpoint-nic**. |

| Region | Select **East US 2**. |

1. Select **Next: Resource**.

1. In the **Resource** pane, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| Connection method | Leave the default of **Connect to an Azure resource in my directory.** |

| Subscription | Select your subscription. |

| Resource type | Select **Microsoft.Web/sites**. |

| Resource | Select **webapp-1**. |

| Target subresource | Select **sites**. |

1. Select **Next: Virtual Network**.

1. In **Virtual Network**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| **Networking** |  |

| Virtual network | Select **vnet-1 (test-rg)**. |

| Subnet | Select **subnet-1**. |

| Network policy for private endpoints | Select **edit** to apply Network policy for private endpoints. </br> In **Edit subnet network policy**, select the checkbox next to **Network security groups** and **Route Tables** in the **Network policies setting for all private endpoints in this subnet** pull-down. </br> Select **Save**. </br></br>For more information, see [Manage network policies for private endpoints](disable-private-endpoint-network-policy.md) |

# [**Dynamic IP**](#tab/dynamic-ip)

| Setting | Value |

| ------- | ----- |

| **Private IP configuration** | Select **Dynamically allocate IP address**. |

# [**Static IP**](#tab/static-ip)

| Setting | Value |

| ------- | ----- |

| **Private IP configuration** | Select **Statically allocate IP address**. |

| Name | Enter **ipconfig-1**. |

| Private IP | Enter **10.0.0.10**. |

---

1. Select **Next: DNS**.

1. Leave the defaults in **DNS**. Select **Next: Tags**, then **Next: Review + create**.

1. Select **Create**.

[!INCLUDE [create-test-virtual-machine.md](~/reusable-content/ce-skilling/azure/includes/create-test-virtual-machine.md)]

## Test connectivity to the private endpoint

Use the virtual machine that you created earlier to connect to the web app across the private endpoint.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines**.

1. Select **vm-1**.

1. On the overview page for **vm-1**, select **Connect**, and then select the **Bastion** tab.

1. Select **Use Bastion**.

1. Enter the username and password that you used when you created the VM.

1. Select **Connect**.

1. After you've connected, open PowerShell on the server.

1. Enter `nslookup webapp-1.azurewebsites.net`. You receive a message that's similar to the following example:

```output

Server:  UnKnown

Address:  168.63.129.16

Non-authoritative answer:

Name:    webapp-1.privatelink.azurewebsites.net

Address:  10.0.0.10

Aliases:  webapp-1.azurewebsites.net

```

A private IP address of **10.0.0.10** is returned for the web app name if you chose static IP address in the previous steps. This address is in the subnet of the virtual network you created earlier.

1. In the bastion connection to **vm-1**, open the web browser.

1. Enter the URL of your web app, `https://webapp-1.azurewebsites.net`.

If your web app hasn't been deployed, you get the following default web app page:

1. Close the connection to **vm-1**.

[!INCLUDE [portal-clean-up.md](~/reusable-content/ce-skilling/azure/includes/portal-clean-up.md)]

## Next steps

In this quickstart, you created:

* A virtual network and bastion host

* A virtual machine

* A private endpoint for an Azure web app

You used the VM to test connectivity to the web app across the private endpoint.

For more information about the services that support private endpoints, see:

> [!div class="nextstepaction"]

> [What is Azure Private Link?](private-link-overview.md#availability)


# Private Endpoint Dns

# Azure Private Endpoint private DNS zone values

It's important to correctly configure your DNS settings to resolve the private endpoint IP address to the fully qualified domain name (FQDN) of the connection string.

Existing Microsoft Azure services might already have a DNS configuration for a public endpoint. This configuration must be overridden to connect using your private endpoint.

The network interface associated with the private endpoint contains the information to configure your DNS. The network interface information includes FQDN and private IP addresses for your private link resource.

You can use the following options to configure your DNS settings for private endpoints:

- **Use the host file (only recommended for testing)**. You can use the host file on a virtual machine to override the DNS.

- **Use a private DNS zone**. You can use [Private DNS Zones](../dns/private-dns-privatednszone.md) to override the DNS resolution for a private endpoint. A private DNS zone can be linked to your virtual network to resolve specific domains.

- **Use Azure Private Resolver (optional)**. You can use Azure Private Resolver to override the DNS resolution for a private link resource. For more information about Azure Private Resolver, see [What is Azure Private Resolver?](../dns/dns-private-resolver-overview.md)

> [!CAUTION]

>

> - It's not recommended to override a zone that's actively in use to resolve public endpoints. Connections to resources won't be able to resolve correctly without DNS forwarding to the public DNS. To avoid issues, create a different domain name or follow the suggested name for each service listed later in this article.

>

> - Existing Private DNS Zones linked to a single Azure service should not be associated with two different Azure service Private Endpoints. This will cause a deletion of the initial A-record and result in resolution issues when attempting to access that service from each respective Private Endpoint. Create a DNS zone for each Private Endpoint of like services. Don't place records for multiple services in the same DNS zone.

## Azure services DNS zone configuration

Azure creates a canonical name DNS record (CNAME) on the public DNS. The CNAME record redirects the resolution to the private domain name. You can override the resolution with the private IP address of your private endpoints.

Connection URLs for your existing applications don't change. Client DNS requests to a public DNS server resolve to your private endpoints. The process doesn't affect your existing applications.

DNS resolution and access control are independent. The CNAME chain in the public `privatelink.<service>.<region>.<suffix>` zone is deliberately resolvable from anywhere on the internet so that hybrid and gradual-migration scenarios continue to work without breaking existing clients. A successful public DNS lookup confirms only that a resource with that exact name exists in the global Azure namespace. It doesn't confirm that a private endpoint is attached, reveal the private endpoint's IP, or grant any data-plane access. When a resource has **Public network access** set to **Disabled** (or the service firewall denies the caller), the service rejects the connection at the front door regardless of DNS resolution. Resource existence is enumerable; resource access is not.

> [!IMPORTANT]

> Azure File Shares must be remounted if connected to the public endpoint.

> [!CAUTION]

>

> - Private networks using a Private DNS Zone for any given resource type (for example, privatelink.blob.core.windows.net/Storage Account) can only resolve DNS Queries to public resources/Public IPs if those public resources don't have any existing Private Endpoint Connections. If this applies, an additional DNS configuration is required on the Private DNS Zone to complete the DNS resolution sequence. Otherwise, the Private DNS Zone will respond to the DNS query with a NXDOMAIN as no matching DNS record would be found in the Private DNS Zone.

>

> > - [Fallback to Internet](../dns/private-dns-fallback.md) for Private DNS Zone Virtual Network Links can be implemented for proper DNS Resolution for the Public IP of the public resource. This allows DNS queries that reach Private DNS Zones to be forwarded to Azure DNS for public resolution.

> > - Alternatively, a manually entered A-record in the Private DNS Zone that contains the Public IP of the public resource would allow for proper DNS resolution. This procedure isn't recommended as the Public IP of the A record in the Private DNS Zone won't be automatically updated if the corresponding public IP address changes for the public resource.

>

> - Private endpoint private DNS zone configurations will only automatically generate if you use the recommended naming scheme in the following tables.

For Azure services, use the recommended zone names as described in the following tables:

## Commercial

### AI + Machine Learning

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Machine Learning workspace (Microsoft.MachineLearningServices/workspaces) | amlworkspace | privatelink.api.azureml.ms<br/>privatelink.notebooks.azure.net | api.azureml.ms<br/>notebooks.azure.net<br/>instances.azureml.ms<br/>aznbcontent.net<br/>inference.ml.azure.com |

> | Azure Machine Learning registry (Microsoft.MachineLearningServices/registries) | amlregistry | privatelink.api.azureml.ms | api.azureml.ms |

> | Foundry Tools (Microsoft.CognitiveServices/accounts) | account | privatelink.cognitiveservices.azure.com <br/> privatelink.openai.azure.com <br/> privatelink.services.ai.azure.com | cognitiveservices.azure.com <br/> openai.azure.com <br/> services.ai.azure.com |

> | Azure Bot Service (Microsoft.BotService/botServices) | Bot | privatelink.directline.botframework.com | directline.botframework.com |

> | Azure Bot Service (Microsoft.BotService/botServices) | Token | privatelink.token.botframework.com | token.botframework.com |

### Analytics

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Synapse Analytics (Microsoft.Synapse/workspaces) | Sql | privatelink.sql.azuresynapse.net | sql.azuresynapse.net |

> | Azure Synapse Analytics (Microsoft.Synapse/workspaces) | SqlOnDemand | privatelink.sql.azuresynapse.net | sql.azuresynapse.net |

> | Azure Synapse Analytics (Microsoft.Synapse/workspaces) | Dev | privatelink.dev.azuresynapse.net | dev.azuresynapse.net |

> | Azure Synapse Studio (Microsoft.Synapse/privateLinkHubs) | Web | privatelink.azuresynapse.net | azuresynapse.net |

> | Azure Event Hubs (Microsoft.EventHub/namespaces) | namespace | privatelink.servicebus.windows.net | servicebus.windows.net |

> | Azure Service Bus (Microsoft.ServiceBus/namespaces) | namespace | privatelink.servicebus.windows.net | servicebus.windows.net |

> | Azure Data Factory (Microsoft.DataFactory/factories) | dataFactory | privatelink.datafactory.azure.net | datafactory.azure.net |

> | Azure Data Factory (Microsoft.DataFactory/factories) | portal | privatelink.adf.azure.com | adf.azure.com |

> | Azure HDInsight (Microsoft.HDInsight/clusters) | gateway </br> headnode | privatelink.azurehdinsight.net | azurehdinsight.net |

> | Azure Data Explorer (Microsoft.Kusto/Clusters) | cluster | privatelink.{regionName}.kusto.windows.net </br> privatelink.blob.core.windows.net </br> privatelink.queue.core.windows.net </br> privatelink.table.core.windows.net | {regionName}.kusto.windows.net </br> blob.core.windows.net </br> queue.core.windows.net </br> table.core.windows.net |

> | Microsoft Power BI (Microsoft.PowerBI/privateLinkServicesForPowerBI) | tenant | privatelink.analysis.windows.net </br> privatelink.pbidedicated.windows.net </br> privatelink.prod.powerquery.microsoft.com | analysis.windows.net </br> pbidedicated.windows.net </br> prod.powerquery.microsoft.com |

> | Azure Databricks (Microsoft.Databricks/workspaces) | databricks_ui_api </br> browser_authentication | privatelink.azuredatabricks.net | azuredatabricks.net |

> | Microsoft Fabric (Microsoft.Fabric/privateLinkServicesForFabric) | workspace | privatelink.fabric.microsoft.com  | fabric.microsoft.com |

### Compute

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Batch (Microsoft.Batch/batchAccounts) | batchAccount | privatelink.batch.azure.com | {regionName}.batch.azure.com |

> | Azure Batch (Microsoft.Batch/batchAccounts) | nodeManagement | privatelink.batch.azure.com | {regionName}.service.batch.azure.com |

> | Azure Virtual Desktop (Microsoft.DesktopVirtualization/workspaces) | global | privatelink-global.wvd.microsoft.com | wvd.microsoft.com |

> | Azure Virtual Desktop (Microsoft.DesktopVirtualization/workspaces) | feed | privatelink.wvd.microsoft.com | wvd.microsoft.com |

> | Azure Virtual Desktop (Microsoft.DesktopVirtualization/hostpools) | connection | privatelink.wvd.microsoft.com | wvd.microsoft.com |

### Containers

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Kubernetes Service - Kubernetes API (Microsoft.ContainerService/managedClusters) | management | privatelink.{regionName}.azmk8s.io </br> {subzone}.privatelink.{regionName}.azmk8s.io | {regionName}.azmk8s.io |

> | Azure Container Apps (Microsoft.App/ManagedEnvironments) | managedEnvironments | privatelink.{regionName}.azurecontainerapps.io | azurecontainerapps.io |

> | Azure Container Registry (Microsoft.ContainerRegistry/registries) | registry | privatelink.azurecr.io </br> {regionName}.data.privatelink.azurecr.io<sup>1</sup> | azurecr.io </br> {regionName}.data.azurecr.io |

### Databases

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure SQL Database (Microsoft.Sql/servers) | sqlServer | privatelink.database.windows.net | database.windows.net |

> | Azure SQL Managed Instance (Microsoft.Sql/managedInstances) | managedInstance | privatelink.{dnsPrefix}.database.windows.net | {dnsPrefix}.database.windows.net |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | Sql | privatelink.documents.azure.com | documents.azure.com |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | MongoDB | privatelink.mongo.cosmos.azure.com | mongo.cosmos.azure.com |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | Cassandra | privatelink.cassandra.cosmos.azure.com | cassandra.cosmos.azure.com |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | Gremlin | privatelink.gremlin.cosmos.azure.com | gremlin.cosmos.azure.com |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | Table | privatelink.table.cosmos.azure.com | table.cosmos.azure.com |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | Analytical | privatelink.analytics.cosmos.azure.com | analytics.cosmos.azure.com |

> | Azure Cosmos DB (Microsoft.DBforPostgreSQL/serverGroupsv2) | coordinator | privatelink.postgres.cosmos.azure.com | postgres.cosmos.azure.com |

> | Azure Cosmos DB for MongoDB - vCore (Microsoft.DocumentDB/mongoClusters) | MongoCluster | privatelink.mongocluster.cosmos.azure.com | mongocluster.cosmos.azure.com |

> | Azure Database for PostgreSQL - Single server (Microsoft.DBforPostgreSQL/servers) | postgresqlServer | privatelink.postgres.database.azure.com | postgres.database.azure.com |

> | Azure Database for PostgreSQL - Flexible server (Microsoft.DBforPostgreSQL/flexibleServers) | postgresqlServer | privatelink.postgres.database.azure.com | postgres.database.azure.com |

> | Azure Database for MySQL - Single Server (Microsoft.DBforMySQL/servers) | mysqlServer | privatelink.mysql.database.azure.com | mysql.database.azure.com |

> | Azure Database for MySQL - Flexible Server (Microsoft.DBforMySQL/flexibleServers) | mysqlServer | privatelink.mysql.database.azure.com | mysql.database.azure.com |

> | Azure Database for MariaDB (Microsoft.DBforMariaDB/servers) | mariadbServer | privatelink.mariadb.database.azure.com | mariadb.database.azure.com |

> | Azure Cache for Redis (Microsoft.Cache/Redis) | redisCache | privatelink.redis.cache.windows.net | redis.cache.windows.net |

> | Azure Cache for Redis Enterprise (Microsoft.Cache/RedisEnterprise) | redisEnterprise | privatelink.redisenterprise.cache.azure.net | {cachename}.{region}.redisenterprise.cache.azure.net |

> | Azure Managed Redis (Microsoft.Cache/RedisEnterprise) | redisEnterprise | privatelink.redis.azure.net | {region}.redis.azure.net |

### Hybrid + multicloud

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Arc (Microsoft.HybridCompute/privateLinkScopes) | hybridcompute | privatelink.his.arc.azure.com <br/> privatelink.guestconfiguration.azure.com </br> privatelink.dp.kubernetesconfiguration.azure.com | his.arc.azure.com <br/> guestconfiguration.azure.com </br> dp.kubernetesconfiguration.azure.com |

### Integration

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Service Bus (Microsoft.ServiceBus/namespaces) | namespace | privatelink.servicebus.windows.net | servicebus.windows.net |

> | Azure Event Grid (Microsoft.EventGrid/topics) | topic | privatelink.eventgrid.azure.net | eventgrid.azure.net |

> | Azure Event Grid (Microsoft.EventGrid/domains) | domain | privatelink.eventgrid.azure.net | eventgrid.azure.net |

> | Azure Event Grid (Microsoft.EventGrid/namespaces) | topic | privatelink.eventgrid.azure.net | eventgrid.azure.net |

> | Azure Event Grid (Microsoft.EventGrid/namespaces) | topicSpace | privatelink.ts.eventgrid.azure.net | eventgrid.azure.net |

> | Azure Event Grid (Microsoft.EventGrid/partnerNamespaces) | partnernamespace | privatelink.eventgrid.azure.net | eventgrid.azure.net |

> | Azure API Management (Microsoft.ApiManagement/service) | Gateway | privatelink.azure-api.net | azure-api.net |

> | Azure Health Data Services (Microsoft.HealthcareApis/workspaces) | healthcareworkspace | privatelink.azurehealthcareapis.com </br> privatelink.dicom.azurehealthcareapis.com | workspace.azurehealthcareapis.com </br> fhir.azurehealthcareapis.com </br> dicom.azurehealthcareapis.com |

### Internet of Things (IoT)

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure IoT Hub (Microsoft.Devices/IotHubs) | iotHub | privatelink.azure-devices.net<br/>privatelink.servicebus.windows.net<sup>2</sup> | azure-devices.net<br/>servicebus.windows.net |

> | Azure IoT Hub Device Provisioning Service (Microsoft.Devices/ProvisioningServices) | iotDps | privatelink.azure-devices-provisioning.net | azure-devices-provisioning.net |

> | Device Update for IoT Hubs (Microsoft.DeviceUpdate/accounts) | DeviceUpdate | privatelink.api.adu.microsoft.com | api.adu.microsoft.com |

> | Azure IoT Central (Microsoft.IoTCentral/IoTApps) | iotApp | privatelink.azureiotcentral.com </br> privatelink.azure-devices.net </br> privatelink.servicebus.windows.net </br> privatelink.azure-devices-provisioning.net | azureiotcentral.com </br> privatelink.azure-devices.net </br> privatelink.servicebus.windows.net </br> privatelink.azure-devices-provisioning.net|

> | Azure Digital Twins (Microsoft.DigitalTwins/digitalTwinsInstances) | API | privatelink.digitaltwins.azure.net | digitaltwins.azure.net |

### Media

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Media Services (Microsoft.Media/mediaservices) | keydelivery </br> liveevent </br> streamingendpoint | privatelink.media.azure.net | media.azure.net |

> | Azure AI Video Indexer (Microsoft.VideoIndexer/accounts) | account | privatelink.api.videoindexer.ai | api.videoindexer.ai |

### Management and Governance

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Automation (Microsoft.Automation/automationAccounts) | Webhook <br> DSCAndHybridWorker | privatelink.azure-automation.net | {regionCode}.azure-automation.net |

> | Azure Backup (Microsoft.RecoveryServices/vaults) | AzureBackup | privatelink.{regionCode}.backup.windowsazure.com </br> privatelink.blob.core.windows.net </br> privatelink.queue.core.windows.net | {regionCode}.backup.windowsazure.com </br> blob.core.windows.net </br> queue.core.windows.net |

> | Azure Backup (Microsoft.RecoveryServices/vaults) | AzureBackup_secondary | privatelink.{regionCode}.backup.windowsazure.com </br> privatelink.blob.core.windows.net </br> privatelink.queue.core.windows.net | {regionCode}.backup.windowsazure.com </br> blob.core.windows.net </br> queue.core.windows.net |

> | Azure Site Recovery (Microsoft.RecoveryServices/vaults) | AzureSiteRecovery | privatelink.siterecovery.windowsazure.com | {regionCode}.siterecovery.windowsazure.com |

> | Azure Monitor (Microsoft.Insights/privateLinkScopes) | azuremonitor | privatelink.monitor.azure.com<br/> privatelink.oms.opinsights.azure.com <br/> privatelink.ods.opinsights.azure.com <br/> privatelink.agentsvc.azure-automation.net <br/> privatelink.blob.core.windows.net | monitor.azure.com<br/> oms.opinsights.azure.com<br/> ods.opinsights.azure.com<br/> agentsvc.azure-automation.net <br/> blob.core.windows.net <br/> services.visualstudio.com <br/> applicationinsights.azure.com |

> | Microsoft Purview (Microsoft.Purview/accounts) | account | privatelink.purview.azure.com | purview.azure.com |

> | Microsoft Purview (Microsoft.Purview/accounts) | portal | privatelink.purviewstudio.azure.com | purviewstudio.azure.com |

> | Microsoft Purview (Microsoft.Purview/accounts) | platform | privatelink.purview-service.microsoft.com | purview-service.microsoft.com |

> | Azure Migrate (Microsoft.Migrate/migrateProjects) | Default | privatelink.prod.migration.windowsazure.com | prod.migration.windowsazure.com |

> | Azure Migrate (Microsoft.Migrate/assessmentProjects) | Default | privatelink.prod.migration.windowsazure.com | prod.migration.windowsazure.com |

> | Azure Resource Manager (Microsoft.Authorization/resourceManagementPrivateLinks) | ResourceManagement | privatelink.azure.com | azure.com |

> | Azure Managed Grafana (Microsoft.Dashboard/grafana) | grafana | privatelink.grafana.azure.com | grafana.azure.com |

> | Azure Managed Prometheus (Microsoft.Monitor/accounts) | prometheusMetrics | privatelink.{region}.prometheus.monitor.azure.com | {region}.prometheus.monitor.azure.com |

### Security

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Key Vault (Microsoft.KeyVault/vaults) | vault | privatelink.vaultcore.azure.net | vault.azure.net <br> vaultcore.azure.net |

> | Azure Key Vault (Microsoft.KeyVault/managedHSMs) | managedhsm | privatelink.managedhsm.azure.net | managedhsm.azure.net

> | Azure App Configuration (Microsoft.AppConfiguration/configurationStores) | configurationStores | privatelink.azconfig.io | azconfig.io |

> | Azure Attestation (Microsoft.Attestation/attestationProviders) | standard | privatelink.attest.azure.net | attest.azure.net |

### Storage

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Storage account (Microsoft.Storage/storageAccounts) | blob </br> blob_secondary | privatelink.blob.core.windows.net | blob.core.windows.net |

> | Storage account (Microsoft.Storage/storageAccounts) | table </br> table_secondary | privatelink.table.core.windows.net | table.core.windows.net |

> | Storage account (Microsoft.Storage/storageAccounts) | queue </br> queue_secondary | privatelink.queue.core.windows.net | queue.core.windows.net |

> | Storage account (Microsoft.Storage/storageAccounts) | file | privatelink.file.core.windows.net | file.core.windows.net |

> | Storage account (Microsoft.Storage/storageAccounts) | web </br> web_secondary | privatelink.web.core.windows.net | web.core.windows.net |

> | Azure Data Lake File System Gen2 (Microsoft.Storage/storageAccounts) | dfs </br> dfs_secondary | privatelink.dfs.core.windows.net | dfs.core.windows.net |

> | Azure File Sync (Microsoft.StorageSync/storageSyncServices) | afs | privatelink.afs.azure.net | afs.azure.net |

> | Azure Managed Disks (Microsoft.Compute/diskAccesses) | disks | privatelink.blob.core.windows.net | blob.core.windows.net |

> | Azure Elastic SAN (Microsoft.ElasticSan/elasticSans) | volumegroup | privatelink.blob.core.windows.net | blob.storage.azure.net |

> | Azure Files (Microsoft.FileShares/fileShares) | FileShare | privatelink.file.core.windows.net | file.core.windows.net |

### Web

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Search (Microsoft.Search/searchServices) | searchService | privatelink.search.windows.net | search.windows.net |

> | Azure Relay (Microsoft.Relay/namespaces) | namespace | privatelink.servicebus.windows.net | servicebus.windows.net |

> | Azure Web Apps / Azure Function Apps (Microsoft.Web/sites) | sites | privatelink.azurewebsites.net </br> scm.privatelink.azurewebsites.net<sup>3</sup> | azurewebsites.net </br> scm.azurewebsites.net |

> | SignalR (Microsoft.SignalRService/SignalR) | signalr | privatelink.service.signalr.net | service.signalr.net |

> | Azure Static Web Apps (Microsoft.Web/staticSites) | staticSites | privatelink.azurestaticapps.net </br> privatelink.{partitionId}.azurestaticapps.net | azurestaticapps.net </br> {partitionId}.azurestaticapps.net |

> | Azure Maps (Microsoft.Maps/accounts) | account | privatelink.account.maps.azure.com | account.maps.azure.com |

> | Azure Web PubSub service (Microsoft.SignalRService/WebPubSub) | webpubsub | privatelink.webpubsub.azure.com | webpubsub.azure.com |

<sup>1</sup>If you are using Azure Private DNS Zones, do not deploy this as an additional zone. DNS entries will be automatically added to the existing DNS Zone `privatelink.azurecr.io`.

<sup>2</sup>To use with the IoT Hub built-in Event Hubs-compatible endpoint. For more information, see [IoT Hub support for virtual networks with Azure Private Link](../iot-hub/virtual-network-support.md#built-in-event-hubs-compatible-endpoint).

<sup>3</sup>To use with the Kudu console or Kudu REST API, you must create two DNS records that point to the private endpoint IP address in your Azure DNS private zone `privatelink.azurewebsites.net` or custom DNS server. The first record is for your app. The second record is for source control management (SCM) for your app. If you use private DNS zones in Azure, don't deploy this as an additional zone.

> [!Note]

> In the above text, **`{regionCode}`** refers to the region code (for example, **eus** for East US and **ne** for North Europe). Refer to the following lists for regions codes:

>

> - [All public clouds](https://download.microsoft.com/download/1/2/6/126a410b-0e06-45ed-b2df-84f353034fa1/AzureRegionCodesList.docx)

> - [Geo Code list in XML](/azure/backup/scripts/geo-code-list)

>

> **`{regionName}`** refers to the full region name (for example, **eastus** for East US and **northeurope** for North Europe). To retrieve a current list of Azure regions and their names and display names, use **`az account list-locations -o table`**.

## Government

### AI + Machine Learning

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Foundry Tools (Microsoft.CognitiveServices/accounts) | account | privatelink.cognitiveservices.azure.us | cognitiveservices.azure.us |

> | Azure Machine Learning (Microsoft.MachineLearningServices/workspaces) | amlworkspace | privatelink.api.ml.azure.us<br/>privatelink.notebooks.usgovcloudapi.net | api.ml.azure.us<br/>notebooks.usgovcloudapi.net <br/> instances.azureml.us<br/>aznbcontent.net <br/> inference.ml.azure.us |

### Analytics

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Event Hubs (Microsoft.EventHub/namespaces) | namespace | privatelink.servicebus.usgovcloudapi.net | servicebus.usgovcloudapi.net |

> | Azure Synapse Analytics (Microsoft.Synapse/workspaces) | Sql | privatelink.sql.azuresynapse.usgovcloudapi.net | sql.azuresynapse.usgovcloudapi.net |

> | Azure Synapse Analytics (Microsoft.Synapse/workspaces) | SqlOnDemand | privatelink.sql.azuresynapse.usgovcloudapi.net | {workspaceName}-ondemand.sql.azuresynapse.usgovcloudapi.net |

> | Azure Synapse Analytics (Microsoft.Synapse/workspaces) | Dev | privatelink.dev.azuresynapse.usgovcloudapi.net | dev.azuresynapse.usgovcloudapi.net |

> | Azure Synapse Studio (Microsoft.Synapse/privateLinkHubs) | Web | privatelink.azuresynapse.usgovcloudapi.net | azuresynapse.usgovcloudapi.net |

> | Azure Data Factory (Microsoft.DataFactory/factories) | dataFactory | privatelink.datafactory.azure.us | datafactory.azure.us |

> | Azure Data Factory (Microsoft.DataFactory/factories) | portal | privatelink.adf.azure.us | adf.azure.us |

> | Azure HDInsight (Microsoft.HDInsight) | gateway </br> headnode | privatelink.azurehdinsight.us | azurehdinsight.us |

> | Azure Databricks (Microsoft.Databricks/workspaces) | databricks_ui_api </br> browser_authentication | privatelink.databricks.azure.us | databricks.azure.us |

### Compute

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Batch (Microsoft.Batch/batchAccounts) | batchAccount | privatelink.batch.usgovcloudapi.net | {regionName}.batch.usgovcloudapi.net |

> | Azure Batch (Microsoft.Batch/batchAccounts) | nodeManagement | privatelink.batch.usgovcloudapi.net | {regionName}.service.batch.usgovcloudapi.net |

> | Azure Virtual Desktop (Microsoft.DesktopVirtualization/workspaces) | global | privatelink-global.wvd.azure.us | wvd.azure.us |

> | Azure Virtual Desktop (Microsoft.DesktopVirtualization/workspaces </br> Microsoft.DesktopVirtualization/hostpools) | feed <br> connection | privatelink.wvd.azure.us | wvd.azure.us |

### Containers

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Container Registry (Microsoft.ContainerRegistry/registries) | registry | privatelink.azurecr.us </br> {regionName}.privatelink.azurecr.us | azurecr.us </br> {regionName}.azurecr.us |

### Databases

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure SQL Database (Microsoft.Sql/servers) | sqlServer | privatelink.database.usgovcloudapi.net | database.usgovcloudapi.net |

> | Azure SQL Managed Instance (Microsoft.Sql/managedInstances) | managedInstance | privatelink.{dnsPrefix}.database.usgovcloudapi.net | {dnsPrefix}.database.usgovcloudapi.net |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | Sql | privatelink.documents.azure.us | documents.azure.us |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | MongoDB | privatelink.mongo.cosmos.azure.us | mongo.cosmos.azure.us |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | Cassandra | privatelink.cassandra.cosmos.azure.us | cassandra.cosmos.azure.us |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | Gremlin | privatelink.gremlin.cosmos.azure.us | gremlin.cosmos.azure.us |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | Table | privatelink.table.cosmos.azure.us | table.cosmos.azure.us |

> | Azure Database for PostgreSQL - Single server (Microsoft.DBforPostgreSQL/servers) | postgresqlServer | privatelink.postgres.database.usgovcloudapi.net | postgres.database.usgovcloudapi.net |

> | Azure Database for PostgreSQL - Flexible server (Microsoft.DBforPostgreSQL/flexibleServers) | postgresqlServer | privatelink.postgres.database.usgovcloudapi.net | postgres.database.usgovcloudapi.net |

> | Azure Database for MySQL - Single Server (Microsoft.DBforMySQL/servers) | mysqlServer | privatelink.mysql.database.usgovcloudapi.net | mysql.database.usgovcloudapi.net |

> | Azure Database for MySQL - Flexible Server (Microsoft.DBforMySQL/flexibleServers) | mysqlServer | privatelink.mysql.database.usgovcloudapi.net | mysql.database.usgovcloudapi.net |

> | Azure Database for MariaDB (Microsoft.DBforMariaDB/servers) | mariadbServer | privatelink.mariadb.database.usgovcloudapi.net| mariadb.database.usgovcloudapi.net |

> | Azure Cache for Redis (Microsoft.Cache/Redis) | redisCache | privatelink.redis.cache.usgovcloudapi.net | redis.cache.usgovcloudapi.net |

### Hybrid + multicloud

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

### Integration

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Service Bus (Microsoft.ServiceBus/namespaces) | namespace | privatelink.servicebus.usgovcloudapi.net | servicebus.usgovcloudapi.net |

> | Azure Event Grid (Microsoft.EventGrid/topics) | topic | privatelink.eventgrid.azure.us | eventgrid.azure.us |

> | Azure Event Grid (Microsoft.EventGrid/domains) | domain | privatelink.eventgrid.azure.us | eventgrid.azure.us |

> | Azure Health Data Services (Microsoft.HealthcareApis/workspaces) | healthcareworkspace | privatelink.workspace.azurehealthcareapis.us </br> privatelink.fhir.azurehealthcareapis.us </br> privatelink.dicom.azurehealthcareapis.us | workspace.azurehealthcareapis.us </br> fhir.azurehealthcareapis.us </br> dicom.azurehealthcareapis.us |

### Internet of Things (IoT)

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure IoT Hub (Microsoft.Devices/IotHubs) | iotHub | privatelink.azure-devices.us<br/>privatelink.servicebus.windows.us<sup>1</sup> | azure-devices.us<br/>servicebus.usgovcloudapi.net |

> | Azure IoT Hub Device Provisioning Service (Microsoft.Devices/ProvisioningServices) | iotDps | privatelink.azure-devices-provisioning.us | azure-devices-provisioning.us |

### Media

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

### Management and Governance

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Automation / (Microsoft.Automation/automationAccounts) | Webhook </br> DSCAndHybridWorker | privatelink.azure-automation.us | azure-automation.us |

> | Azure Backup (Microsoft.RecoveryServices/vaults) | AzureBackup | privatelink.{regionCode}.backup.windowsazure.us | {regionCode}.backup.windowsazure.us |

> | Azure Migrate (Microsoft.Migrate/migrateProjects) | Default | privatelink.prod.migration.windowsazure.us | prod.migration.windowsazure.us |

> | Azure Migrate (Microsoft.Migrate/assessmentProjects) | Default | privatelink.prod.migration.windowsazure.us | prod.migration.windowsazure.us |

> | Azure Site Recovery (Microsoft.RecoveryServices/vaults) | AzureSiteRecovery | privatelink.siterecovery.windowsazure.us | {regionCode}.siterecovery.windowsazure.us |

> | Azure Monitor (Microsoft.Insights/privateLinkScopes) | azuremonitor | privatelink.monitor.azure.us <br/> privatelink.adx.monitor.azure.us <br/> privatelink.oms.opinsights.azure.us <br/> privatelink.ods.opinsights.azure.us <br/> privatelink.agentsvc.azure-automation.us <br/> privatelink.blob.core.usgovcloudapi.net | monitor.azure.us <br/> adx.monitor.azure.us <br/> oms.opinsights.azure.us<br/> ods.opinsights.azure.us<br/> agentsvc.azure-automation.us <br/> blob.core.usgovcloudapi.net |

> | Microsoft Purview (Microsoft.Purview) | account | privatelink.purview.azure.us | purview.azure.us |

> | Microsoft Purview (Microsoft.Purview) | portal | privatelink.purviewstudio.azure.us | purview.azure.com </br> purviewstudio.azure.us |

### Security

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Key Vault (Microsoft.KeyVault/vaults) | vault | privatelink.vaultcore.usgovcloudapi.net | vault.usgovcloudapi.net <br> vaultcore.usgovcloudapi.net |

> | Azure App Configuration (Microsoft.AppConfiguration/configurationStores) | configurationStores | privatelink.azconfig.azure.us | azconfig.azure.us |

### Storage

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Storage account (Microsoft.Storage/storageAccounts) | blob </br> blob_secondary | privatelink.blob.core.usgovcloudapi.net | blob.core.usgovcloudapi.net |

> | Storage account (Microsoft.Storage/storageAccounts) | table </br> table_secondary | privatelink.table.core.usgovcloudapi.net | table.core.usgovcloudapi.net |

> | Storage account (Microsoft.Storage/storageAccounts) | queue </br> queue_secondary | privatelink.queue.core.usgovcloudapi.net | queue.core.usgovcloudapi.net |

> | Storage account (Microsoft.Storage/storageAccounts) | file </br> file_secondary | privatelink.file.core.usgovcloudapi.net | file.core.usgovcloudapi.net |

> | Storage account (Microsoft.Storage/storageAccounts) | web </br> web_secondary | privatelink.web.core.usgovcloudapi.net | web.core.usgovcloudapi.net |

> | Azure Data Lake File System Gen2 (Microsoft.Storage/storageAccounts) | dfs </br> dfs_secondary | privatelink.dfs.core.usgovcloudapi.net | dfs.core.usgovcloudapi.net |

### Web

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Search (Microsoft.Search/searchServices) | searchService | privatelink.search.azure.us | search.azure.us |

> | Azure Relay (Microsoft.Relay/namespaces) | namespace | privatelink.servicebus.usgovcloudapi.net | servicebus.usgovcloudapi.net |

> | Azure Web Apps (Microsoft.Web/sites) | sites | privatelink.azurewebsites.us </br> scm.privatelink.azurewebsites.us<sup>2</sup> | azurewebsites.us </br> scm.azurewebsites.us |

> | Azure Event Hubs (Microsoft.EventHub/namespaces) | namespace | privatelink.servicebus.usgovcloudapi.net | servicebus.usgovcloudapi.net |

<sup>1</sup>To use with the IoT Hub built-in Event Hubs-compatible endpoint. For more information, see [IoT Hub support for virtual networks with Azure Private Link](../iot-hub/virtual-network-support.md#built-in-event-hubs-compatible-endpoint).

<sup>2</sup>To use with the Kudu console or Kudu REST API, you must create two DNS records that point to the private endpoint IP address in your Azure DNS private zone `privatelink.azurewebsites.net` or custom DNS server. The first record is for your app. The second record is for SCM for your app. If you use private DNS zones in Azure, don't deploy this as an additional zone.

> [!Note]

> In the above text, `{regionCode}` refers to the region code (for example, **eus** for East US and **ne** for North Europe). Refer to the following lists for regions codes:

>

> - [US Gov](../azure-government/documentation-government-developer-guide.md)

> - [Geo Code list in XML](/azure/backup/scripts/geo-code-list)

>

> **`{regionName}`** refers to the full region name (for example, **eastus** for East US and **northeurope** for North Europe). To retrieve a current list of Azure regions and their names and display names, use **`az account list-locations -o table`**.

## China

### AI + Machine Learning

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Machine Learning (Microsoft.MachineLearningServices/workspaces) | amlworkspace | privatelink.api.ml.azure.cn<br/>privatelink.notebooks.chinacloudapi.cn | api.ml.azure.cn<br/>notebooks.chinacloudapi.cn <br/> instances.azureml.cn <br/> aznbcontent.net <br/> inference.ml.azure.cn |

### Analytics

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Data Factory (Microsoft.DataFactory/factories) | dataFactory | privatelink.datafactory.azure.cn | datafactory.azure.cn |

> | Azure Data Factory (Microsoft.DataFactory/factories) | portal | privatelink.adf.azure.cn | adf.azure.cn |

> | Azure HDInsight (Microsoft.HDInsight) | gateway </br> headnode | privatelink.azurehdinsight.cn | azurehdinsight.cn |

> | Azure Data Explorer (Microsoft.Kusto/Clusters) | cluster | privatelink.{regionName}.kusto.windows.cn | {regionName}.kusto.windows.cn |

### Compute

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Batch (Microsoft.Batch/batchAccounts) | batchAccount | privatelink.batch.chinacloudapi.cn | {region}.batch.chinacloudapi.cn |

> | Azure Batch (Microsoft.Batch/batchAccounts) | nodeManagement | privatelink.batch.chinacloudapi.cn | {region}.service.batch.chinacloudapi.cn |

> | Azure Virtual Desktop (Microsoft.DesktopVirtualization/workspaces) | global | privatelink-global.wvd.azure.cn | wvd.azure.cn |

> | Azure Virtual Desktop (Microsoft.DesktopVirtualization/workspaces and Microsoft.DesktopVirtualization/hostpools) | feed </br> connection | privatelink.wvd.azure.cn | wvd.azure.cn |

### Containers

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

### Databases

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure SQL Database (Microsoft.Sql/servers) | sqlServer | privatelink.database.chinacloudapi.cn | database.chinacloudapi.cn |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | Sql | privatelink.documents.azure.cn | documents.azure.cn |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | MongoDB | privatelink.mongo.cosmos.azure.cn | mongo.cosmos.azure.cn |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | Cassandra | privatelink.cassandra.cosmos.azure.cn | cassandra.cosmos.azure.cn |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | Gremlin | privatelink.gremlin.cosmos.azure.cn | gremlin.cosmos.azure.cn |

> | Azure Cosmos DB (Microsoft.DocumentDB/databaseAccounts) | Table | privatelink.table.cosmos.azure.cn | table.cosmos.azure.cn |

> | Azure Database for PostgreSQL - Single server (Microsoft.DBforPostgreSQL/servers) | postgresqlServer | privatelink.postgres.database.chinacloudapi.cn | postgres.database.chinacloudapi.cn |

> | Azure Database for PostgreSQL - Flexible server (Microsoft.DBforPostgreSQL/flexibleServers) | postgresqlServer | privatelink.postgres.database.chinacloudapi.cn | postgres.database.chinacloudapi.cn |

> | Azure Database for MySQL - Single Server (Microsoft.DBforMySQL/servers) | mysqlServer | privatelink.mysql.database.chinacloudapi.cn | mysql.database.chinacloudapi.cn |

> | Azure Database for MySQL - Flexible Server (Microsoft.DBforMySQL/flexibleServers) | mysqlServer | privatelink.mysql.database.chinacloudapi.cn | mysql.database.chinacloudapi.cn |

> | Azure Database for MariaDB (Microsoft.DBforMariaDB/servers) | mariadbServer | privatelink.mariadb.database.chinacloudapi.cn | mariadb.database.chinacloudapi.cn |

> | Azure Cache for Redis (Microsoft.Cache/Redis) | redisCache | privatelink.redis.cache.chinacloudapi.cn | redis.cache.chinacloudapi.cn |

### Hybrid + multicloud

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

### Integration

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Service Bus (Microsoft.ServiceBus/namespaces) | namespace | privatelink.servicebus.chinacloudapi.cn | servicebus.chinacloudapi.cn |

### Internet of Things (IoT)

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure IoT Hub (Microsoft.Devices/IotHubs) | iotHub | privatelink.azure-devices.cn <br/> privatelink.servicebus.chinacloudapi.cn <sup>1</sup> | azure-devices.cn<br/>servicebus.chinacloudapi.cn |

> | Azure IoT Hub Device Provisioning Service (Microsoft.Devices/ProvisioningServices) | iotDps | privatelink.azure-devices-provisioning.cn | azure-devices-provisioning.cn |

### Media

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

### Management and Governance

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Automation / (Microsoft.Automation/automationAccounts) | Webhook </br> DSCAndHybridWorker | privatelink.azure-automation.cn | azure-automation.cn |

### Security

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Key Vault (Microsoft.KeyVault/vaults) | vault | privatelink.vaultcore.azure.cn | vaultcore.azure.cn |

### Storage

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Storage account (Microsoft.Storage/storageAccounts) | blob </br> blob_secondary | privatelink.blob.core.chinacloudapi.cn | blob.core.chinacloudapi.cn |

> | Storage account (Microsoft.Storage/storageAccounts) | table </br> table_secondary | privatelink.table.core.chinacloudapi.cn | table.core.chinacloudapi.cn |

> | Storage account (Microsoft.Storage/storageAccounts) | queue </br> queue_secondary | privatelink.queue.core.chinacloudapi.cn | queue.core.chinacloudapi.cn |

> | Storage account (Microsoft.Storage/storageAccounts) | file </br> file_secondary | privatelink.file.core.chinacloudapi.cn | file.core.chinacloudapi.cn |

> | Storage account (Microsoft.Storage/storageAccounts) | web </br> web_secondary | privatelink.web.core.chinacloudapi.cn | web.core.chinacloudapi.cn |

> | Azure Data Lake File System Gen2 (Microsoft.Storage/storageAccounts) | dfs </br> dfs_secondary | privatelink.dfs.core.chinacloudapi.cn | dfs.core.chinacloudapi.cn |

> | Azure File Sync (Microsoft.StorageSync/storageSyncServices) | afs | privatelink.afs.azure.cn | afs.azure.cn

### Web

> [!div class="mx-tdBreakAll"]

> | Private link resource type | Subresource | Private DNS zone name | Public DNS zone forwarders |

> |---|---|---|---|

> | Azure Event Hubs (Microsoft.EventHub/namespaces) | namespace | privatelink.servicebus.chinacloudapi.cn | servicebus.chinacloudapi.cn |

> | Azure Relay (Microsoft.Relay/namespaces) | namespace | privatelink.servicebus.chinacloudapi.cn | servicebus.chinacloudapi.cn |

> | Azure Web Apps (Microsoft.Web/sites) | sites | privatelink.chinacloudsites.cn | chinacloudsites.cn |

> | SignalR (Microsoft.SignalRService/SignalR) | signalR | privatelink.signalr.azure.cn | service.signalr.azure.cn |

<sup>1</sup>To use with the IoT Hub built-in Event Hubs-compatible endpoint. For more information, see [IoT Hub support for virtual networks with Azure Private Link](../iot-hub/virtual-network-support.md#built-in-event-hubs-compatible-endpoint).

## Next step

To learn more about DNS integration and scenarios for Azure Private Link, continue to the following article:

> [!div class="nextstepaction"]

> [Azure Private Endpoint DNS ](private-endpoint-dns-integration.md)


# Tutorial Private Endpoint Storage Portal

# Tutorial: Connect to a storage account using an Azure Private Endpoint

Azure Private endpoint is the fundamental building block for Private Link in Azure. It enables Azure resources, like virtual machines (VMs), to privately and securely communicate with Private Link resources such as Azure Storage.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a virtual network and bastion host.

> * Create a storage account and disable public access.

> * Create a private endpoint for the storage account.

> * Create a virtual machine.

> * Test connectivity to the storage account private endpoint.

## Prerequisites

* An Azure subscription. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## <a name="create-storage-account-with-a-private-endpoint"></a> Sign in to Azure

Sign in to the [Azure portal](https://portal.azure.com).

## Create a resource group

A resource group is a logical container for Azure resources. This procedure creates a resource group for all resources used in this tutorial.

1. In the portal, search for and select **Resource groups**.

1. On the **Resource groups** page, select **+ Create**.

1. On the **Basics** tab, enter or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Enter **test-rg**. |

| **Resource details** |  |

| Region | Select **East US 2**. |

1. Select **Review + create**, and then select **Create**.

## Create a virtual network

The following procedure creates a virtual network with a resource subnet.

1. In the portal, search for and select **Virtual networks**.

1. On the **Virtual networks** page, select **+ Create**.

1. On the **Basics** tab of **Create virtual network**, enter, or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |  |

| Name | Enter **vnet-1**. |

| Region | Select **East US 2**. |

1. Select **Next** to proceed to the **Security** tab.

1. Select **Next** to proceed to the **IP Addresses** tab.

1. In the address space box in **Subnets**, select the **default** subnet.

1. In **Edit subnet**, enter or select the following information:

| Setting | Value |

|---|---|

| **Subnet details** |  |

| Subnet template | Leave the default **Default**. |

| Name | Enter **subnet-1**. |

| Starting address | Leave the default of **10.0.0.0**. |

| Subnet size | Leave the default of **/24 (256 addresses)**. |

1. Select **Save**.

1. Select **Review + create** at the bottom of the screen, and when validation passes, select **Create**.

## Deploy Azure Bastion

Azure Bastion uses your browser to connect to VMs in your virtual network over Secure Shell (SSH) or Remote Desktop Protocol (RDP) by using their private IP addresses. The VMs don't need public IP addresses, client software, or special configuration. For more information about Azure Bastion, see [Azure Bastion](/azure/bastion/bastion-overview).

>[!NOTE]

>[!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

1. In the search box at the top of the portal, enter **Bastion**. Select **Bastions** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab of **Create a Bastion**, enter, or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |  |

| Name | Enter **bastion**. |

| Region | Select **East US 2**. |

| Tier | Select **Developer**. |

| **Configure virtual networks** |  |

| Virtual network | Select **vnet-1**. |

1. Select **Review + create**.

1. Select **Create**.

[!INCLUDE [create-storage-account.md](~/reusable-content/ce-skilling/azure/includes/create-storage-account.md)]

## Disable public access to storage account

Before you create the private endpoint, it's recommended to disable public access to the storage account. Use the following steps to disable public access to the storage account.

1. In the search box at the top of the portal, enter **Storage account**. Select **Storage accounts** in the search results.

1. Select **storage1** or the name of your existing storage account.

1. In **Security + networking**, select **Networking**.

1. In the **Firewalls and virtual networks** tab in **Public network access**, select **Disabled**.

1. Select **Save**.

## Create private endpoint

1. In the search box at the top of the portal, enter **Private endpoint**. Select **Private endpoints**.

1. Select **+ Create** in **Private endpoints**.

1. In the **Basics** tab of **Create a private endpoint**, enter, or select the following information.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** |

| **Instance details** |   |

| Name | Enter **private-endpoint**. |

| Network Interface Name | Leave the default of **private-endpoint-nic**. |

| Region | Select **East US 2**. |

1. Select **Next: Resource**.

1. In the **Resource** pane, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| Connection method | Leave the default of **Connect to an Azure resource in my directory.** |

| Subscription | Select your subscription. |

| Resource type | Select **Microsoft.Storage/storageAccounts**. |

| Resource | Select **storage-1** or your storage account. |

| Target subresource | Select **blob**. |

> [!NOTE]

> If you later choose to enable a hierarchical namespace on this account, you need to create a private endpoint for both the **blob** and **dfs** sub-resources. Operations that target the Data Lake Storage (dfs) endpoint can be redirected to the Blob endpoint, and some operations - such as managing ACLs, creating directories, and deleting directories - require a DFS private endpoint. Creating private endpoints for both sub-resources ensures that all operations complete successfully. For more information, see [Use private endpoints for Azure Storage](../storage/common/storage-private-endpoints.md).

1. Select **Next: Virtual Network**.

1. In **Virtual Network**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| **Networking** |  |

| Virtual network | Select **vnet-1 (test-rg)**. |

| Subnet | Select **subnet-1**. |

| Network policy for private endpoints | Select **edit** to apply Network policy for private endpoints. </br> In **Edit subnet network policy**, select the checkbox next to **Network security groups** and **Route Tables** in the **Network policies setting for all private endpoints in this subnet** pull-down. </br> Select **Save**. </br></br>For more information, see [Manage network policies for private endpoints](disable-private-endpoint-network-policy.md) |

# [**Dynamic IP**](#tab/dynamic-ip)

| Setting | Value |

| ------- | ----- |

| **Private IP configuration** | Select **Dynamically allocate IP address**. |

# [**Static IP**](#tab/static-ip)

| Setting | Value |

| ------- | ----- |

| **Private IP configuration** | Select **Statically allocate IP address**. |

| Name | Enter **ipconfig-1**. |

| Private IP | Enter **10.0.0.10**. |

---

1. Select **Next: DNS**.

1. Leave the defaults in **DNS**. Select **Next: Tags**, then **Next: Review + create**.

1. Select **Create**.

[!INCLUDE [create-test-virtual-machine.md](~/reusable-content/ce-skilling/azure/includes/create-test-virtual-machine.md)]

## Storage access key

The storage access key is required for the later steps. Go to the storage account you created previously and copy the connection string with the access key for the storage account.

1. In the search box at the top of the portal, enter **Storage account**. Select **Storage accounts** in the search results.

1. Select the storage account you created in the previous steps or your existing storage account.

1. In the **Security + networking** section of the storage account, select **Access keys**.

1. Select **Show**, then select copy on the **Connection string** for **key1**.

## Add a blob container

1. In the search box at the top of the portal, enter **Storage account**. Select **Storage accounts** in the search results.

1. Select the storage account you created in the previous steps.

1. In the **Data storage** section, select **Containers**.

1. Select **+ Container** to create a new container.

1. Enter **container** in **Name** and select **Private (no anonymous access)** under **Public access level**.

1. Select **Create**.

## Test connectivity to private endpoint

In this section, you use the virtual machine you created in the previous steps to connect to the storage account across the private endpoint using **Microsoft Azure Storage Explorer**.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **vm-1**.

1. In **Connect**, select **Bastion**.

1. Enter the username and password that you entered during the virtual machine creation.

1. Select **Connect**.

1. Open Windows PowerShell on the server after you connect.

1. Enter `nslookup <storage-account-name>.blob.core.windows.net`. Replace **\<storage-account-name>** with the name of the storage account you created in the previous steps. The following example shows the output of the command.

```powershell

Server:  UnKnown

Address:  168.63.129.16

Non-authoritative answer:

Name:    storage1.privatelink.blob.core.windows.net

Address:  10.0.0.10

Aliases:  mystorageaccount.blob.core.windows.net

```

A private IP address of **10.0.0.10** is returned for the storage account name. This address is in **subnet-1** subnet of **vnet-1** virtual network you created previously.

1. Install [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md?tabs=windows&toc=%2fazure%2fstorage%2fblobs%2ftoc.json) on the virtual machine.

1. Select **Finish** after the **Microsoft Azure Storage Explorer** is installed. Leave the box checked to open the application.

1. Select the **Power plug** symbol to open the **Select Resource** dialog box in the left-hand toolbar.

1. In **Select Resource** , select **Storage account or service** to add a connection in **Microsoft Azure Storage Explorer** to your storage account that you created in the previous steps.

1. In the **Select Connection Method** screen, select **Connection string**, and then **Next**.

1. In the box under **Connection String**, paste the connection string from the storage account you copied in the previous steps. The storage account name automatically populates in the box under **Display name**.

1. Select **Next**.

1. Verify the settings are correct in **Summary**.

1. Select **Connect**

1. Select your storage account from the **Storage Accounts** in the explorer menu.

1. Expand the storage account and then **Blob Containers**.

1. The **container** you created previously is displayed.

1. Close the connection to **vm-1**.

[!INCLUDE [portal-clean-up.md](~/reusable-content/ce-skilling/azure/includes/portal-clean-up.md)]

## Next steps

In this tutorial, you learned how to create:

* Virtual network and bastion host.

* Virtual machine.

* Storage account and a container.

Learn how to connect to an Azure Cosmos DB account via Azure Private Endpoint:

> [!div class="nextstepaction"]

> [Connect to Azure Cosmos DB using Private Endpoint](tutorial-private-endpoint-cosmosdb-portal.md)


# Tutorial Inspect Traffic Azure Firewall

# Tutorial: Inspect private endpoint traffic with Azure Firewall

Azure Private Endpoint is the fundamental building block for Azure Private Link. Private endpoints enable Azure resources deployed in a virtual network to communicate privately with private link resources.

Private endpoints allow resources access to the private link service deployed in a virtual network. Access to the private endpoint through virtual network peering and on-premises network connections extend the connectivity.

You may need to inspect or block traffic from clients to the services exposed via private endpoints. Complete this inspection by using [Azure Firewall](../firewall/overview.md) or a third-party network virtual appliance.

For more information and scenarios that involve private endpoints and Azure Firewall, see [Azure Firewall scenarios to inspect traffic destined to a private endpoint](inspect-traffic-with-azure-firewall.md).

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a virtual network and bastion host for the test virtual machine.

> * Create the private endpoint virtual network.

> * Create a test virtual machine.

> * Deploy Azure Firewall.

> * Create an Azure SQL database.

> * Create a private endpoint for Azure SQL.

> * Create a network peer between the private endpoint virtual network and the test virtual machine virtual network.

> * Link the virtual networks to a private DNS zone.

> * Configure application rules in Azure Firewall for Azure SQL.

> * Route traffic between the test virtual machine and Azure SQL through Azure Firewall.

> * Test the connection to Azure SQL and validate in Azure Firewall logs.

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

- An Azure account with an active subscription.

- A Log Analytics workspace. For more information about the creation of a log analytics workspace, see [Create a Log Analytics workspace in the Azure portal](/azure/azure-monitor/logs/quick-create-workspace).

## Sign in to the Azure portal

Sign in to the [Azure portal](https://portal.azure.com).

## Create a resource group

A resource group is a logical container for Azure resources. This procedure creates a resource group for all resources used in this tutorial.

1. In the portal, search for and select **Resource groups**.

1. On the **Resource groups** page, select **+ Create**.

1. On the **Basics** tab, enter or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Enter **test-rg**. |

| **Resource details** |  |

| Region | Select **East US 2**. |

1. Select **Review + create**, and then select **Create**.

## Create a virtual network

The following procedure creates a virtual network with a resource subnet.

1. In the portal, search for and select **Virtual networks**.

1. On the **Virtual networks** page, select **+ Create**.

1. On the **Basics** tab of **Create virtual network**, enter, or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |  |

| Name | Enter **vnet-1**. |

| Region | Select **East US 2**. |

1. Select **Next** to proceed to the **Security** tab.

1. Select **Next** to proceed to the **IP Addresses** tab.

1. In the address space box in **Subnets**, select the **default** subnet.

1. In **Edit subnet**, enter or select the following information:

| Setting | Value |

|---|---|

| **Subnet details** |  |

| Subnet template | Leave the default **Default**. |

| Name | Enter **subnet-1**. |

| Starting address | Leave the default of **10.0.0.0**. |

| Subnet size | Leave the default of **/24 (256 addresses)**. |

1. Select **Save**.

1. Select **Review + create** at the bottom of the screen, and when validation passes, select **Create**.

## Deploy Azure Bastion

Azure Bastion uses your browser to connect to VMs in your virtual network over Secure Shell (SSH) or Remote Desktop Protocol (RDP) by using their private IP addresses. The VMs don't need public IP addresses, client software, or special configuration. For more information about Azure Bastion, see [Azure Bastion](/azure/bastion/bastion-overview).

>[!NOTE]

>[!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

1. In the search box at the top of the portal, enter **Bastion**. Select **Bastions** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab of **Create a Bastion**, enter, or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |  |

| Name | Enter **bastion**. |

| Region | Select **East US 2**. |

| Tier | Select **Developer**. |

| **Configure virtual networks** |  |

| Virtual network | Select **vnet-1**. |

1. Select **Review + create**.

1. Select **Create**.

[!INCLUDE [virtual-network-create-private-endpoint.md](../../includes/virtual-network-create-private-endpoint.md)]

## Create a test virtual machine

The following procedure creates a test virtual machine (VM) named **vm-1** in the virtual network.

1. In the portal, search for and select **Virtual machines**.

1. In **Virtual machines**, select **+ Create**, then select **Azure virtual machine**.

1. On the **Basics** tab of **Create a virtual machine**, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |   |

| Virtual machine name | Enter **vm-1**. |

| Region | Select **(US) East US 2**. |

| Availability options | Select **No infrastructure redundancy required**. |

| Security type | Select **Standard**. |

| Image | Select **Ubuntu Server 24.04 LTS - x64 Gen2**. |

| VM architecture | Leave the default of **x64**. |

| Size | Select a size. |

| **Administrator account** |   |

| Authentication type | Select **SSH public key**. |

| Username | Enter a username. |

| SSH public key source | Select **Generate new key pair**. |

| Key pair name | Enter **vm-1-key**. |

| **Inbound port rules** |  |

| Public inbound ports | Select **None**. |

1. Select **Next: Disks** then **Next: Networking**.

1. In the Networking tab, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Network interface** |   |

| Virtual network | Select **vnet-1**. |

| Subnet | Select **subnet-1 (10.0.0.0/24)**. |

| Public IP | Select **None**. |

| Network interface (NIC) network security group | Select **Advanced**. |

| Configure network security group | Select **Create new**.</br> In **Name** enter **nsg-1**.</br> Select **OK**. |

1. Leave the rest of the options at the defaults and select **Review + create**.

1. Select **Create**.

1. A **Generate new key pair** pop-up opens. Select **Download private key and create resource**.

1. The private key file is downloaded as **vm-1-key.pem**. Make sure you know where this file is downloaded so you can use it to sign in to the virtual machine in the next steps.

## Deploy Azure Firewall

1. In the search box at the top of the portal, enter **Firewall**. Select **Firewalls** in the search results.

1. In **Firewalls**, select **+ Create**.

1. Enter or select the following information in the **Basics** tab of **Create a firewall**:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |  |

| Name | Enter **firewall**. |

| Region | Select **East US 2**. |

| Availability zone | Select **None**. |

| Firewall SKU | Select **Standard**. |

| Firewall management | Select **Use a Firewall Policy to manage this firewall**. |

| Firewall policy | Select **Add new**. </br> Enter **firewall-policy** in **Policy name**. </br> Select **East US 2** in region. </br> Select **OK**. |

| Choose a virtual network | Select **Create new**. |

| Virtual network name | Enter **vnet-firewall**. |

| Address space | Enter **10.2.0.0/16**. |

| Subnet address space | Enter **10.2.1.0/26**. |

| Public IP address | Select **Add new**. </br> Enter **public-ip-firewall** in **Name**. </br> Select **OK**. |

1. Select **Review + create**.

1. Select **Create**.

Wait for the firewall deployment to complete before you continue.

## Enable firewall logs

In this section, you enable the firewall logs and send them to the log analytics workspace.

> [!NOTE]

> You must have a log analytics workspace in your subscription before you can enable firewall logs. For more information, see [Prerequisites](#prerequisites).

1. In the search box at the top of the portal, enter **Firewall**. Select **Firewalls** in the search results.

1. Select **firewall**.

1. In **Monitoring** select **Diagnostic settings**.

1. Select **+ Add diagnostic setting**.

1. In **Diagnostic setting** enter or select the following information:

| Setting | Value |

|---|---|

| Diagnostic setting name | Enter **diagnostic-setting-firewall**. |

| **Logs** |  |

| Categories | Select **Azure Firewall Application Rule (Legacy Azure Diagnostics)** and **Azure Firewall Network Rule (Legacy Azure Diagnostics)**. |

| **Destination details** |  |

| Destination | Select **Send to Log Analytics workspace**. |

| Subscription | Select your subscription. |

| Log Analytics workspace | Select your log analytics workspace. |

1. Select **Save**.

## Create an Azure SQL database

1. In the search box at the top of the portal, enter **SQL**. Select **SQL databases** in the search results.

1. In **SQL databases**, select **+ Create**.

1. In the **Basics** tab of **Create SQL Database**, enter or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Database details** |  |

| Database name | Enter **sql-db**. |

| Server | Select **Create new**. </br> Enter **server-name** in **Server name** (Server names must be unique, replace **server-name** with a unique value). </br> Select **(US) East US 2** in **Location**. </br> Select **Use SQL authentication**. </br> Enter a server admin sign-in and password. </br> Select **OK**. |

| Want to use SQL elastic pool? | Select **No**. |

| Workload environment | Leave the default of **Production**. |

| **Backup storage redundancy** |  |

| Backup storage redundancy | Select **Locally redundant backup storage**. |

1. Select **Next: Networking**.

1. In the **Networking** tab of **Create SQL Database**, enter or select the following information:

| Setting | Value |

|---|---|

| **Network connectivity** |  |

| Connectivity method | Select **Private endpoint**. |

| **Private endpoints** |  |

| Select **+Add private endpoint**. |   |

| **Create private endpoint** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| Location | Select **East US 2**. |

| Name | Enter **private-endpoint-sql**. |

| Target subresource | Select **SqlServer**. |

| **Networking** |  |

| Virtual network | Select **vnet-private-endpoint**. |

| Subnet | Select **subnet-private-endpoint**. |

| **Private DNS integration** |  |

| Integrate with private DNS zone | Select **Yes**. |

| Private DNS zone | Leave the default of **privatelink.database.windows.net**. |

1. Select **OK**.

1. Select **Review + create**.

1. Select **Create**.

## Connect virtual networks with virtual network peering

In this section, you connect the virtual networks with virtual network peering. The networks **vnet-1** and **vnet-private-endpoint** are connected to **vnet-firewall**. There isn't direct connectivity between **vnet-1** and **vnet-private-endpoint**.

1. In the search box at the top of the portal, enter **Virtual networks**. Select **Virtual networks** in the search results.

1. Select **vnet-firewall**.

1. In **Settings** select **Peerings**.

1. In **Peerings** select **+ Add**.

1. In **Add peering**, enter or select the following information:

| Setting | Value |

|---|---|

| **This virtual network** |  |

| Peering link name | Enter **vnet-firewall-to-vnet-1**. |

| Traffic to remote virtual network | Select **Allow (default)**. |

| Traffic forwarded from remote virtual network | Select **Allow (default)**. |

| Virtual network gateway or Route Server | Select **None (default)**. |

| **Remote virtual network** |  |

| Peering link name | Enter **vnet-1-to-vnet-firewall**. |

| Virtual network deployment model | Select **Resource manager**. |

| Subscription | Select your subscription. |

| Virtual network | Select **vnet-1**. |

| Traffic to remote virtual network | Select **Allow (default)**. |

| Traffic forwarded from remote virtual network | Select **Allow (default)**. |

| Virtual network gateway or Route Server | Select **None (default)**. |

1. Select **Add**.

1. In **Peerings** select **+ Add**.

1. In **Add peering**, enter or select the following information:

| Setting | Value |

|---|---|

| **This virtual network** |  |

| Peering link name | Enter **vnet-firewall-to-vnet-private-endpoint**. |

| Allow 'vnet-1' to access 'vnet-private-endpoint' | Leave the default of selected.  |

| Allow 'vnet-1' to receive forwarded traffic from 'vnet-private-endpoint' | Select the checkbox. |

| Allow gateway in 'vnet-1' to forward traffic to 'vnet-private-endpoint' | Leave the default of cleared. |

| Enable 'vnet-1' to use 'vnet-private-endpoint' remote gateway | Leave the default of cleared. |

| **Remote virtual network** |  |

| Peering link name | Enter **vnet-private-endpoint-to-vnet-firewall**. |

| Virtual network deployment model | Select **Resource manager**. |

| Subscription | Select your subscription. |

| Virtual network | Select **vnet-private-endpoint**. |

| Allow 'vnet-private-endpoint' to access 'vnet-1' | Leave the default of selected.  |

| Allow 'vnet-private-endpoint' to receive forwarded traffic from 'vnet-1' | Select the checkbox. |

| Allow gateway in 'vnet-private-endpoint' to forward traffic to 'vnet-1' | Leave the default of cleared. |

| Enable 'vnet-private-endpoint' to use 'vnet-1's' remote gateway | Leave the default of cleared. |

1. Select **Add**.

1. Verify the **Peering status** displays **Connected** for both network peers.

## Link the virtual networks to the private DNS zone

The private DNS zone created during the private endpoint creation in the previous section must be linked to the **vnet-1** and **vnet-firewall** virtual networks.

1. In the search box at the top of the portal, enter **Private DNS zone**. Select **Private DNS zones** in the search results.

1. Select **privatelink.database.windows.net**.

1. In **Settings** select **Virtual network links**.

1. Select **+ Add**.

1. In **Add virtual network link**, enter or select the following information:

| Setting | Value |

|---|---|

| **Virtual network link** |  |

| Virtual network link name | Enter **link-to-vnet-1**. |

| Subscription | Select your subscription. |

| Virtual network | Select **vnet-1 (test-rg)**. |

| Configuration | Leave the default of unchecked for **Enable auto registration**. |

1. Select **OK**.

1. Select **+ Add**.

1. In **Add virtual network link**, enter or select the following information:

| Setting | Value |

|---|---|

| **Virtual network link** |  |

| Virtual network link name | Enter **link-to-vnet-firewall**. |

| Subscription | Select your subscription. |

| Virtual network | Select **vnet-firewall (test-rg)**. |

| Configuration | Leave the default of unchecked for **Enable auto registration**. |

1. Select **OK**.

## Create route between vnet-1 and vnet-private-endpoint

A network link between **vnet-1** and **vnet-private-endpoint** doesn't exist. You must create a route to allow traffic to flow between the virtual networks through Azure Firewall.

The route sends traffic from **vnet-1** to the address space of virtual network **vnet-private-endpoint**, through the Azure Firewall.

1. In the search box at the top of the portal, enter **Route tables**. Select **Route tables** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab of **Create Route table**, enter or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |  |

| Region | Select **East US 2**. |

| Name | Enter **vnet-1-to-vnet-firewall**. |

| Propagate gateway routes | Leave the default of **Yes**. |

1. Select **Review + create**.

1. Select **Create**.

1. In the search box at the top of the portal, enter **Route tables**. Select **Route tables** in the search results.

1. Select **vnet-1-to-vnet-firewall**.

1. In **Settings** select **Routes**.

1. Select **+ Add**.

1. In **Add route**, enter or select the following information:

| Setting | Value |

|---|---|

| Route name | Enter **subnet-1-to-subnet-private-endpoint**. |

| Destination type | Select **IP Addresses**. |

| Destination IP addresses/CIDR ranges | Enter **10.1.0.0/16**. |

| Next hop type | Select **Virtual appliance**. |

| Next hop address | Enter **10.2.1.4**. |

1. Select **Add**.

1. In **Settings**, select **Subnets**.

1. Select **+ Associate**.

1. In **Associate subnet**, enter or select the following information:

| Setting | Value |

|---|---|

| Virtual network | Select **vnet-1(test-rg)**. |

| Subnet | Select **subnet-1**. |

1. Select **OK**.

## Configure an application rule in Azure Firewall

Create an application rule to allow communication from **vnet-1** to the private endpoint of the Azure SQL server **server-name.database.windows.net**. Replace **server-name** with the name of your Azure SQL server.

1. In the search box at the top of the portal, enter **Firewall**. Select **Firewall Policies** in the search results.

1. In **Firewall Policies**, select **firewall-policy**.

1. In **Settings** select **Application rules**.

1. Select **+ Add a rule collection**.

1. In **Add a rule collection**, enter or select the following information:

| Setting | Value |

|---|---|

| Name | Enter **rule-collection-sql**. |

| Rule collection type | Leave the selection of **Application**. |

| Priority | Enter **100**. |

| Rule collection action | Select **Allow**. |

| Rule collection group | Leave the default of **DefaultApplicationRuleCollectionGroup**. |

| **Rules** |  |

| **Rule 1** |  |

| Name | Enter **SQLPrivateEndpoint**. |

| Source type | Select **IP Address**. |

| Source | Enter **10.0.0.0/16** |

| Protocol | Enter **mssql:1433** |

| Destination type | Select **FQDN**. |

| Destination | Enter **server-name.database.windows.net**. |

1. Select **Add**.

## Test connection to Azure SQL from virtual machine

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **vm-1**.

1. Select **Connect** then **Connect via Bastion** in the **Overview** section.

1. In the **Bastion** connection page, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| Authentication Type | Select **SSH Private Key from Local File**. |

| Username | Enter the username you created. |

| Local File | Select the **vm-1-key** private key file you downloaded. |

1. Select **Connect**.

1. To verify name resolution of the private endpoint, enter the following command in the terminal window:

```bash

nslookup server-name.database.windows.net

```

You receive a message similar to the following example. The IP address returned is the private IP address of the private endpoint.

```output

Server:    127.0.0.53

Address:   127.0.0.53#53

Non-authoritative answer:

sql-server-8675.database.windows.netcanonical name = sql-server-8675.privatelink.database.windows.net.

Name:sql-server-8675.privatelink.database.windows.net

Address: 10.1.0.4

```

1. Install the SQL server command line tools from [Install the SQL Server command-line tools sqlcmd and bcp on Linux](/sql/linux/sql-server-linux-setup-tools). Proceed with the next steps after the installation is complete.

1. Use the following commands to connect to the SQL server you created in the previous steps.

* Replace **\<server-admin>** with the admin username you entered during the SQL server creation.

* Replace **\<admin-password>** with the admin password you entered during SQL server creation.

* Replace **server-name** with the name of your SQL server.

```bash

sqlcmd -S server-name.database.windows.net -U '<server-admin>' -P '<admin-password>'

```

1. A SQL command prompt is displayed on successful sign in. Enter **exit** to exit the **sqlcmd** tool.

## Validate traffic in the Azure Firewall logs

1. In the search box at the top of the portal, enter **Log Analytics**. Select **Log Analytics** in the search results.

1. Select your log analytics workspace. In this example, the workspace is named **log-analytics-workspace**.

1. In the General settings, select **Logs**.

1. In the example **Queries** in the search box, enter **Application rule**. In the returned results in **Network**, select the **Run** button for **Application rule log data**.

1. In the log query output, verify **server-name.database.windows.net** is listed under **FQDN** and **SQLPrivateEndpoint** is listed under **Rule**.

[!INCLUDE [portal-clean-up.md](~/reusable-content/ce-skilling/azure/includes/portal-clean-up.md)]

## Next steps

Advance to the next article to learn how to use a private endpoint with Azure Private Resolver:

> [!div class="nextstepaction"]

> [Create a private endpoint DNS infrastructure with Azure Private Resolver for an on-premises workload](tutorial-dns-on-premises-private-resolver.md)


# Private Endpoint Dns Integration

# Azure Private Endpoint DNS integration Scenarios

Azure Private Endpoint DNS integration is essential for enabling secure, private connectivity to Azure services within your virtual network. This article describes common DNS configuration scenarios for Azure Private Endpoints, including options for virtual networks, peered networks, and on-premises environments. Use these scenarios and best practices to ensure reliable and secure name resolution for your applications and services.

For private DNS zone settings for Azure services that support a private endpoint, see [Azure Private Endpoint private DNS zone values](private-endpoint-dns.md).

> [!CAUTION]

>

> - It's not recommended to override a zone that's actively in use to resolve public endpoints. Connections to resources won't be able to resolve correctly without DNS forwarding to the public DNS. To avoid issues, create a different domain name or follow the suggested name for each service listed later in this article.

>

> - Existing Private DNS Zones linked to a single Azure service should not be associated with two different Azure service Private Endpoints. This will cause a deletion of the initial A-record and result in resolution issues when attempting to access that service from each respective Private Endpoint. Create a DNS zone for each Private Endpoint of like services. Don't place records for multiple services in the same DNS zone.

## DNS configuration scenarios

The FQDN of the service automatically resolves to a public IP address. To resolve to the private IP address of the private endpoint, change your DNS configuration.

DNS is critical for your application to work correctly because it resolves the private endpoint IP address.

You can use the following DNS resolution scenarios:

- [Virtual network workloads without Azure Private Resolver](#virtual-network-workloads-without-azure-private-resolver)

- [Peered virtual network workloads without Azure Private Resolver](#virtual-network-workloads-without-custom-dns-server)

- [On-premises workloads using a DNS forwarder without Azure Private Resolver)](#on-premises-workloads-using-a-dns-forwarder-without-azure-private-resolver)

- [Azure Private Resolver for on-premises workloads](#azure-private-resolver-for-on-premises-workloads)

- [Azure Private Resolver with on-premises DNS forwarder](#on-premises-workloads-using-a-dns-forwarder)

- [Azure Private Resolver for virtual network and on-premises workloads](#virtual-network-and-on-premises-workloads-using-a-dns-forwarder)

## Virtual network workloads without Azure Private Resolver

This configuration is appropriate for virtual network workloads without a custom DNS server. In this scenario, the client queries for the private endpoint IP address to the Azure-provided DNS service [168.63.129.16](../virtual-network/what-is-ip-address-168-63-129-16.md). Azure DNS is responsible for DNS resolution of the private DNS zones.

> [!NOTE]

> This scenario uses the Azure SQL Database-recommended private DNS zone. For other services, you can adjust the model using the following reference: [Azure services DNS zone configuration](private-endpoint-dns.md).

To configure properly, you need the following resources:

- Client virtual network

- Private DNS zone [privatelink.database.windows.net](../dns/private-dns-privatednszone.md) with [type A record](../dns/dns-zones-records.md#record-types)

- Private endpoint information (FQDN record name and private IP address)

The following screenshot illustrates the DNS resolution sequence from virtual network workloads using the private DNS zone:

## <a name="virtual-network-workloads-without-custom-dns-server"></a> Peered virtual network workloads without Azure Private Resolver

You can extend this model to peered virtual networks associated to the same private endpoint. [Add new virtual network links](../dns/private-dns-virtual-network-links.md) to the private DNS zone for all peered virtual networks.

> [!IMPORTANT]

> - A single private DNS zone is required for this configuration. Creating multiple zones with the same name for different virtual networks would need manual operations to merge the DNS records.

>

> - If you're using a private endpoint in a hub-and-spoke model from a different subscription or even within the same subscription, link the same private DNS zones to all spokes and hub virtual networks that contain clients that need DNS resolution from the zones.

In this scenario, there's a [hub and spoke](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) networking topology. The spoke networks share a private endpoint. The spoke virtual networks are linked to the same private DNS zone.

## On-premises workloads using a DNS forwarder without Azure Private Resolver

For on-premises workloads to resolve the FQDN of a private endpoint, configure a DNS forwarder in Azure. The DNS forwarder should be deployed in the virtual network that is linked to the private DNS zone for your private endpoint.

A [DNS forwarder](/windows-server/identity/ad-ds/plan/reviewing-dns-concepts#resolving-names-by-using-forwarding) is typically a virtual machine running DNS services or a managed service like [Azure Firewall](../firewall/dns-settings.md). The DNS forwarder receives DNS queries from on-premises or other virtual networks and forwards them to Azure DNS.

> [!NOTE]

> DNS queries for private endpoints must originate from the virtual network that is linked to the private DNS zone. The DNS forwarder enables this by proxying queries on behalf of on-premises clients.

> This scenario uses the Azure SQL Database-recommended private DNS zone. For other services, you can adjust the model using the following reference: [Azure services DNS zone configuration](private-endpoint-dns.md).

The following scenario is for an on-premises network that has a DNS forwarder in Azure. This forwarder resolves DNS queries via a server-level forwarder to the Azure provided DNS [168.63.129.16](../virtual-network/what-is-ip-address-168-63-129-16.md).

To configure properly, you need the following resources:

- On-premises network with a custom DNS solution in place

- Virtual network [connected to on-premises](/azure/architecture/reference-architectures/hybrid-networking/)

- DNS solution in deployed in your Azure environment with the capability to conditionally forward DNS requests

- Private DNS zone [privatelink.database.windows.net](../dns/private-dns-privatednszone.md) with [type A record](../dns/dns-zones-records.md#record-types)

- Private endpoint information (FQDN record name and private IP address)

> [!IMPORTANT]

> The conditional forwarding must be made to the recommended public DNS zone forwarder. For example: `database.windows.net` instead of **privatelink**.database.windows.net.

- Extend this configuration for on-premises networks that already have a custom DNS solution.

- Configure your on-premises DNS solution with a [conditional forwarder](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-that-uses-your-own-dns-server) for the private DNS zone. The conditional forwarder should point to the DNS forwarder deployed in Azure, so DNS queries for private endpoints are correctly resolved.

The resolution is made by a private DNS zone [linked to a virtual network](../dns/private-dns-virtual-network-links.md):

## Azure Private Resolver for on-premises workloads

For on-premises workloads to resolve the FQDN of a private endpoint, use Azure Private Resolver to resolve the Azure service public DNS zone in Azure. Azure Private Resolver is an Azure managed service that can resolve DNS queries without the need for a virtual machine acting as a DNS forwarder.

The following scenario is for an on-premises network configured to use an Azure Private Resolver. The private resolver forwards the request for the private endpoint to Azure DNS.

> [!NOTE]

> This scenario uses the Azure SQL Database-recommended private DNS zone. For other services, you can adjust the model using the following reference: [Azure services DNS zone values](private-endpoint-dns.md).

The following resources are required for a proper configuration:

- On-premises network

- Virtual network [connected to on-premises](/azure/architecture/reference-architectures/hybrid-networking/)

- [Azure Private Resolver](/azure/dns/dns-private-resolver-overview)

- Private DNS zones [privatelink.database.windows.net](../dns/private-dns-privatednszone.md) with [type A record](../dns/dns-zones-records.md#record-types)

- Private endpoint information (FQDN record name and private IP address)

The following diagram illustrates the DNS resolution sequence from an on-premises network. The configuration uses a Private Resolver deployed in Azure. The resolution is made by a private DNS zone [linked to a virtual network](../dns/private-dns-virtual-network-links.md):

## <a name="on-premises-workloads-using-a-dns-forwarder"></a> Azure Private Resolver with on-premises DNS forwarder

This configuration can be extended for an on-premises network that already has a DNS solution in place.

The on-premises DNS solution is configured to forward DNS traffic to Azure DNS via a [conditional forwarder](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-that-uses-your-own-dns-server). The conditional forwarder references the Private Resolver deployed in Azure.

> [!NOTE]

> This scenario uses the Azure SQL Database-recommended private DNS zone. For other services, you can adjust the model using the following reference: [Azure services DNS zone values](private-endpoint-dns.md)

To configure properly, you need the following resources:

- On-premises network with a custom DNS solution in place

- Virtual network [connected to on-premises](/azure/architecture/reference-architectures/hybrid-networking/)

- [Azure Private Resolver](/azure/dns/dns-private-resolver-overview)

- Private DNS zones [privatelink.database.windows.net](../dns/private-dns-privatednszone.md) with [type A record](../dns/dns-zones-records.md#record-types)

- Private endpoint information (FQDN record name and private IP address)

The following diagram illustrates the DNS resolution from an on-premises network. DNS resolution is conditionally forwarded to Azure. The resolution is made by a private DNS zone [linked to a virtual network](../dns/private-dns-virtual-network-links.md).

> [!IMPORTANT]

> The conditional forwarding must be made to the recommended [public DNS zone forwarder](private-endpoint-dns.md). For example: `database.windows.net` instead of **privatelink**.database.windows.net.

## <a name="virtual-network-and-on-premises-workloads-using-a-dns-forwarder"></a> Azure Private Resolver for virtual network and on-premises workloads

For workloads accessing a private endpoint from virtual and on-premises networks, use Azure Private Resolver to resolve the Azure service [public DNS zone](private-endpoint-dns.md) deployed in Azure.

The following scenario is for an on-premises network with virtual networks in Azure. Both networks access the private endpoint located in a shared hub network.

The private resolver is responsible for resolving all the DNS queries via the Azure-provided DNS service [168.63.129.16](../virtual-network/what-is-ip-address-168-63-129-16.md).

> [!IMPORTANT]

> A single private DNS zone is required for this configuration. All client connections made from on-premises and [peered virtual networks](../virtual-network/virtual-network-peering-overview.md) must also use the same private DNS zone.

> [!NOTE]

> This scenario uses the Azure SQL Database-recommended private DNS zone. For other services, you can adjust the model using the following reference: [Azure services DNS zone configuration](private-endpoint-dns.md).

To configure properly, you need the following resources:

- On-premises network

- Virtual network [connected to on-premises](/azure/architecture/reference-architectures/hybrid-networking/)

- [Peered virtual network](../virtual-network/virtual-network-peering-overview.md)

- Azure Private Resolver

- Private DNS zones [privatelink.database.windows.net](../dns/private-dns-privatednszone.md)  with [type A record](../dns/dns-zones-records.md#record-types)

- Private endpoint information (FQDN record name and private IP address)

The following diagram shows the DNS resolution for both networks, on-premises and virtual networks. The resolution is using Azure Private Resolver.

The resolution is made by a private DNS zone [linked to a virtual network](../dns/private-dns-virtual-network-links.md):

## Private DNS zone group

If you choose to integrate your private endpoint with a private DNS zone, a private DNS zone group is also created. The DNS zone group has a strong association between the private DNS zone and the private endpoint. It helps with managing the private DNS zone records when there's an update on the private endpoint. For example, when you add or remove regions, the private DNS zone is automatically updated with the correct number of records.

Previously, the DNS records for the private endpoint were created via scripting (retrieving certain information about the private endpoint and then adding it on the DNS zone). With the DNS zone group, there's no need to write any extra CLI/PowerShell lines for every DNS zone. Also, when you delete the private endpoint, all the DNS records within the DNS zone group are deleted.

In a hub-and-spoke topology, a common scenario allows the creation of private DNS zones only once in the hub. This setup permits the spokes to register to it, instead of creating different zones in each spoke.

> [!NOTE]

> - Each DNS zone group can support up to five DNS zones.

> - Each DNS zone group can include only one private DNS zone per DNS zone name. For example, you can't associate more than one private DNS zone resource for `privatelink.blob.core.windows.net` to the same DNS zone group.

> - Adding multiple DNS zone groups to a single Private Endpoint isn't supported.

> - Delete and update operations for DNS records can be seen performed by **Azure Traffic Manager and DNS.** This is a normal platform operation necessary for managing your DNS Records.

## Related content

- [Learn about private endpoints](private-endpoint-overview.md)

- [Private endpoint private DNS zone values](private-endpoint-dns.md)


# Tutorial Private Endpoint Sql Portal

# Tutorial: Connect to an Azure SQL server using an Azure Private Endpoint using the Azure portal

Azure Private endpoint is the fundamental building block for Private Link in Azure. It enables Azure resources, like virtual machines (VMs), to privately and securely communicate with Private Link resources such as Azure SQL server.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a virtual network and bastion host.

> * Create a virtual machine.

> * Create an Azure SQL server and private endpoint.

> * Test connectivity to the SQL server private endpoint.

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

* An Azure subscription

## Sign in to Azure

Sign in to the [Azure portal](https://portal.azure.com).

[!INCLUDE [virtual-network-create-with-bastion.md](~/reusable-content/ce-skilling/azure/includes/virtual-network-create-with-bastion.md)]

[!INCLUDE [create-test-virtual-machine-linux.md](~/reusable-content/ce-skilling/azure/includes/create-test-virtual-machine-linux.md)]

## <a name ="create-a-private-endpoint"></a>Create an Azure SQL server and private endpoint

In this section, you create a SQL server in Azure.

1. In the search box at the top of the portal, enter **SQL**. Select **SQL databases** in the search results.

1. In **SQL databases**, select **+ Create**.

1. In the **Basics** tab of **Create SQL Database**, enter, or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Database details** |  |

| Database name | Enter **sql-db**. |

| Server | Select **Create new**. </br> Enter **sql-server-1** in **Server name** (Server names must be unique, replace **sql-server-1** with a unique value). </br> Select **(US) East US 2** in **Location**. </br> Select **Use SQL authentication**. </br> Enter a server admin sign-in and password. </br> Select **OK**. |

| Want to use SQL elastic pool? | Select **No**. |

| Workload environment | Leave the default of **Production**. |

| **Backup storage redundancy** |  |

| Backup storage redundancy | Select **Locally redundant backup storage**. |

1. Select **Next: Networking**.

1. In the **Networking** tab of **Create SQL Database**, enter, or select the following information:

| Setting | Value |

|---|---|

| **Network connectivity** |  |

| Connectivity method | Select **Private endpoint**. |

| **Private endpoints** |  |

| Select **+Add private endpoint**. |   |

| **Create private endpoint** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| Location | Select **East US 2**. |

| Name | Enter **private-endpoint-sql**. |

| Target subresource | Select **SqlServer**. |

| **Networking** |  |

| Virtual network | Select **vnet-1**. |

| Subnet | Select **subnet-1**. |

| **Private DNS integration** |  |

| Integrate with private DNS zone | Select **Yes**. |

| Private DNS zone | Leave the default of **privatelink.database.windows.net**. |

1. Select **OK**.

1. Select **Review + create**.

1. Select **Create**.

> [!IMPORTANT]

> When adding a Private endpoint connection, public routing to your Azure SQL server isn't blocked by default. The setting "Deny public network access" under the "Firewall and virtual networks" blade is left unchecked by default. To disable public network access, ensure this is checked.

## Disable public access to Azure SQL logical server

For this scenario, assume you would like to disable all public access to your Azure SQL server, and only allow connections from your virtual network.

1. In the search box at the top of the portal, enter **SQL server**. Select **SQL servers** in the search results.

1. Select **sql-server-1**.

1. in **Security**, select **Networking** tab, then select **Disable** for **Public network access**.

1. Select **Save**.

## Test connectivity to private endpoint

In this section, you use the virtual machine you created in the previous steps to connect to the SQL server across the private endpoint.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **vm-1**.

1. In **Operations** select **Bastion**.

1. Enter the username and password for the virtual machine.

1. Select **Connect**.

1. To verify name resolution of the private endpoint, enter the following command in the terminal window:

```bash

nslookup server-name.database.windows.net

```

You receive a message similar to the following example. The IP address returned is the private IP address of the private endpoint.

```output

Server:    unknown

Address:   172.0.0.53

Non-authoritative answer:

sql-server-8675.database.windows.netcanonical name = sql-server-8675.privatelink.database.windows.net.

Name:sql-server-8675.privatelink.database.windows.net

Address: 10.1.0.4

```

1. Install the SQL server command line tools from [Install the SQL Server command-line tools sqlcmd and bcp on Linux](/sql/linux/sql-server-linux-setup-tools). Proceed with the next steps after the installation is complete.

1. Use the following commands to connect to the SQL server you created in the previous steps.

* Replace **\<server-admin>** with the admin username you entered during the SQL server creation.

* Replace **\<admin-password>** with the admin password you entered during SQL server creation.

* Replace **sql-server-1** with the name of your SQL server.

```bash

sqlcmd -S server-name.database.windows.net -U '<server-admin>' -P '<admin-password>'

```

1. A SQL command prompt is displayed on successful sign in. Enter **exit** to exit the **sqlcmd** tool.

[!INCLUDE [portal-clean-up.md](~/reusable-content/ce-skilling/azure/includes/portal-clean-up.md)]

## Next steps

In this tutorial, you learned how to create:

* Virtual network and bastion host.

* Virtual machine.

* Azure SQL server with private endpoint.

You used the virtual machine to test connectivity privately and securely to the SQL server across the private endpoint.

As a next step, review the **Web app with private connectivity to Azure SQL Database** architecture scenario, which connects a web application outside of the virtual network to the private endpoint of a database.

> [!div class="nextstepaction"]

> [Web app with private connectivity to Azure SQL Database](/azure/architecture/example-scenario/private-web-app/private-web-app)


# How To Approve Private Link Cross Subscription

# Approve Private Link connections across subscriptions

Azure Private Link enables you to connect privately to Azure resources. Private Link connections are scoped to a specific subscription. This article shows you how to approve a private endpoint connection across subscriptions.

## Prerequisites

- Two active Azure subscriptions:

- One subscription hosts the Azure resource and the other subscription contains the consumer private endpoint and virtual network.

- An administrator account for each subscription or an account with permissions in each subscription to create and manage resources.

Resources used in this article:

| Resource | Subscription | Resource group | Location |

| --- | --- | --- | --- |

| **storage1** *(This name is unique. Replace with the name you create.)* | subscription-1 | test-rg | East US 2 |

| **vnet-1** | subscription-2 | test-rg | East US 2 |

| **private-endpoint** | subscription-2 | test-rg | East US 2 |

## Sign in to subscription-1

Sign in to **subscription-1** in the [Azure portal](https://portal.azure.com).

## Register the resource providers for subscription-1

For the private endpoint connection to complete successfully, the `Microsoft.Storage` and `Microsoft.Network` resource providers must be registered in **subscription-1**. Use the following steps to register the resource providers. If the `Microsoft.Storage` and `Microsoft.Network` resource providers are already registered, skip this step.

> [!IMPORTANT]

> If you're using a different resource type, you must register the resource provider for that resource type if it's not already registered.

1. In the search box at the top of the portal, enter **Subscription**. Select **Subscriptions** in the search results.

1. Select **subscription-1**.

1. In **Settings**, select **Resource providers**.

1. In the **Resource providers** filter box, enter **Microsoft.Storage**. Select **Microsoft.Storage**.

1. Select **Register**.

1. Repeat the previous steps to register the `Microsoft.Network` resource provider.

## Create a resource group

1. In the search box at the top of the portal, enter **Resource group**. Select **Resource groups** in the search results.

1. Select **+ Create**.

1. On the **Basics** tab of **Create a resource group**, enter, or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select **subscription-1**. |

| Resource group | Enter **test-rg**. |

| Region | Select **East US 2**. |

1. Select **Review + Create**.

1. Select **Create**.

[!INCLUDE [create-storage-account.md](~/reusable-content/ce-skilling/azure/includes/create-storage-account.md)]

## Obtain the storage account resource ID

You need the storage account resource ID to create the private endpoint connection in **subscription-2**. Use the following steps to obtain the storage account resource ID.

1. In the search box at the top of the portal, enter **Storage account**. Select **Storage accounts** in the search results.

1. Select **storage1** or the name of your existing storage account.

1. In **Settings**, select **Endpoints**.

1. Copy the entry in **Storage account resource ID**.

## Sign in to subscription-2

Sign in to **subscription-2** in the [Azure portal](https://portal.azure.com).

## Register the resource providers for subscription-2

For the private endpoint connection to complete successfully, the `Microsoft.Storage` and `Microsoft.Network` resource providers must be registered in **subscription-2**. Use the following steps to register the resource providers. If the `Microsoft.Storage` and `Microsoft.Network` resource providers are already registered, skip this step.

> [!IMPORTANT]

> If you're using a different resource type, you must register the resource provider for that resource type if it's not already registered.

1. In the search box at the top of the portal, enter **Subscription**. Select **Subscriptions** in the search results.

1. Select **subscription-2**.

1. In **Settings**, select **Resource providers**.

1. In the **Resource providers** filter box, enter **Microsoft.Storage**. Select **Microsoft.Storage**.

1. Select **Register**.

1. Repeat the previous steps to register the `Microsoft.Network` resource provider.

[!INCLUDE [virtual-network-create.md](~/reusable-content/ce-skilling/azure/includes/virtual-network-create.md)]

## Create private endpoint

1. In the search box at the top of the portal, enter **Private endpoint**. Select **Private endpoints**.

1. Select **+ Create** in **Private endpoints**.

1. On the **Basics** tab of **Create a private endpoint**, enter, or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select **subscription-2**. |

| Resource group | Select **test-rg**. |

| **Instance details** |   |

| Name | Enter **private-endpoint**. |

| Network Interface Name | Leave the default of **private-endpoint-nic**. |

| Region | Select **East US 2**. |

1. Select **Next: Resource**.

1. Select **Connect to an Azure resource by resource ID or alias**.

1. In **Resource ID or alias**, paste the storage account resource ID that you copied earlier.

1. In **Target sub-resource**, enter **blob**.

1. Select **Next: Virtual Network**.

1. In **Virtual Network**, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Networking** |  |

| Virtual network | Select **vnet-1 (test-rg)**. |

| Subnet | Select **subnet-1**. |

1. Select **Next: DNS**.

1. Select **Next: Tags**.

1. Select **Review + Create**.

1. Select **Create**.

## Approve private endpoint connection

The private endpoint connection is in a **Pending** state until approved. Use the following steps to approve the private endpoint connection in **subscription-1**.

1. In the search box at the top of the portal, enter **Private Link**. Select **Private Link** from the search results.

1. In **Network foundation**, expand **Private Link** in the left menu and select **Pending connections**.

1. Select the box next to your storage account in **subscription-1**.

1. Select **Approve**.

1. Select **Yes** in **Approve connection**.

## Next steps

In this article, you learned how to approve a private endpoint connection across subscriptions. To learn more about Azure Private Link, continue to the following articles:

- [Azure Private Link overview](private-link-overview.md)

- [Azure private endpoint overview](private-endpoint-overview.md)


# Disable Private Endpoint Network Policy

# Manage network policies for private endpoints

By default, network policies are disabled for a subnet in a virtual network. To use network policies like user-defined routes and network security group support, network policy support must be enabled for the subnet. This setting only applies to private endpoints in the subnet and affects all private endpoints in the subnet. For other resources in the subnet, access is controlled based on security rules in the network security group.

You can enable network policies either for network security groups only, for user-defined routes only, or for both.

If you enable network security policies for user-defined routes, you can use a custom address prefix length (subnet mask) equal to or larger than the virtual network address space prefix length to override the /32 default route propagated by the private endpoint. This capability can be useful if you want to ensure that private endpoint connection requests go through a firewall or virtual appliance. Otherwise, the /32 default route sends traffic directly to the private endpoint in accordance with the [longest prefix match algorithm](../virtual-network/virtual-networks-udr-overview.md#how-azure-selects-a-route).

> [!IMPORTANT]

> To override a private endpoint route, user-defined routes must have a prefix size that is equal to or smaller than the virtual network address space where the private endpoint is provisioned. For example, a user-defined routes default route (0.0.0.0/0) won't override private endpoint routes because it covers a broader range than the private endpoint's address space. The longest prefix match rule gives higher priority to more specific address prefixes. Additionally, ensure that network policies are enabled in the subnet hosting the private endpoint.

Use the following steps to enable or disable network policy for private endpoints:

* Azure portal

* Azure PowerShell

* Azure CLI

* Azure Resource Manager templates (ARM templates)

The following examples describe how to enable and disable `PrivateEndpointNetworkPolicies` for a virtual network named `myVNet` with a `default` subnet of `10.1.0.0/24` hosted in a resource group named `myResourceGroup`.

## Enable network policy

Follow these steps to configure Network Security Groups and Route tables for your private endpoints.

# [**Portal**](#tab/network-policy-portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal, enter **Virtual network**. Select **Virtual networks**.

1. Select **myVNet**.

1. In settings of **myVNet**, select **Subnets**.

1. Select the **default** subnet.

1. In the **Edit subnet** pane, under **Network Policy for Private Endpoints**, select the boxes for **Network security groups** or **Route tables** as needed.

1. Select **Save**.

# [**PowerShell**](#tab/network-policy-powershell)

Use [Get-AzVirtualNetwork](/powershell/module/az.network/get-azvirtualnetwork), [Set-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/set-azvirtualnetworksubnetconfig), and [Set-AzVirtualNetwork](/powershell/module/az.network/set-azvirtualnetwork) to enable the policy.

```azurepowershell

$net = @{

Name = 'myVNet'

ResourceGroupName = 'myResourceGroup'

}

$vnet = Get-AzVirtualNetwork @net

$sub = @{

Name = 'default'

VirtualNetwork = $vnet

AddressPrefix = '10.1.0.0/24'

PrivateEndpointNetworkPoliciesFlag = 'Enabled'  # Can be either 'Disabled', 'NetworkSecurityGroupEnabled', 'RouteTableEnabled', or 'Enabled'

}

Set-AzVirtualNetworkSubnetConfig @sub

$vnet | Set-AzVirtualNetwork

```

# [**CLI**](#tab/network-policy-cli)

Use [az network vnet subnet update](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-update) to enable the policy. The Azure CLI only supports the values `true` or `false`. It doesn't allow you to enable the policies selectively only for user-defined routes or network security groups:

```azurecli

az network vnet subnet update \

--disable-private-endpoint-network-policies false \

--name default \

--resource-group myResourceGroup \

--vnet-name myVNet

```

# [**JSON**](#tab/network-policy-json)

This section describes how to enable subnet private endpoint policies by using an ARM template. The possible values for `privateEndpointNetworkPolicies` are `Disabled`, `NetworkSecurityGroupEnabled`, `RouteTableEnabled`, and `Enabled`.

```json

{

"name": "myVNet",

"type": "Microsoft.Network/virtualNetworks",

"apiVersion": "2019-04-01",

"location": "WestUS",

"properties": {

"addressSpace": {

"addressPrefixes": [

"10.1.0.0/16"

]

},

"subnets": [

{

"name": "default",

"properties": {

"addressPrefix": "10.1.0.0/24",

"privateEndpointNetworkPolicies": "Enabled"

}

}

]

}

}

```

---

## Disable network policy

# [**Portal**](#tab/network-policy-portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal, enter **Virtual network**. Select **Virtual networks**.

1. Select **myVNet**.

1. In settings of **myVNet**, select **Subnets**.

1. Select the **default** subnet.

1. In the **Edit subnet** pane, under **Network Policy for Private Endpoints**, select the box **Disabled**.

1. Select **Save**.

# [**PowerShell**](#tab/network-policy-powershell)

Use [Get-AzVirtualNetwork](/powershell/module/az.network/get-azvirtualnetwork), [Set-AzVirtualNetwork](/powershell/module/az.network/set-azvirtualnetwork), and [Set-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/set-azvirtualnetworksubnetconfig) to disable the policy.

```azurepowershell

$net = @{

Name = 'myVNet'

ResourceGroupName = 'myResourceGroup'

}

$vnet = Get-AzVirtualNetwork @net

$sub = @{

Name = 'default'

VirtualNetwork = $vnet

AddressPrefix = '10.1.0.0/24'

PrivateEndpointNetworkPoliciesFlag = 'Disabled'

}

Set-AzVirtualNetworkSubnetConfig @sub

$vnet | Set-AzVirtualNetwork

```

# [**CLI**](#tab/network-policy-cli)

Use [az network vnet subnet update](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-update) to disable the policy.

```azurecli

az network vnet subnet update \

--disable-private-endpoint-network-policies true \

--name default \

--resource-group myResourceGroup \

--vnet-name myVNet

```

# [**JSON**](#tab/network-policy-json)

This section describes how to disable subnet private endpoint policies by using an ARM template.

```json

{

"name": "myVNet",

"type": "Microsoft.Network/virtualNetworks",

"apiVersion": "2019-04-01",

"location": "WestUS",

"properties": {

"addressSpace": {

"addressPrefixes": [

"10.1.0.0/16"

]

},

"subnets": [

{

"name": "default",

"properties": {

"addressPrefix": "10.1.0.0/24",

"privateEndpointNetworkPolicies": "Disabled"

}

}

]

}

}

```

---

> [!IMPORTANT]

> There are limitations to private endpoints in relation to the network policy feature and network security groups and user-defined routes. For more information, see [Limitations](private-endpoint-overview.md#limitations).

## Next steps

In this how-to guide, you enabled and disabled network policies for private endpoints in an Azure virtual network. You learned how to use the Azure portal, Azure PowerShell, Azure CLI, and Azure Resource Manager templates to manage network policies for private endpoints.

For more information about the services that support private endpoints, see:

> [!div class="nextstepaction"]

> [What is a private endpoint?](private-endpoint-overview.md)


# Network Security Perimeter Concepts

# What is a network security perimeter?

Azure Network Security Perimeter creates logical network boundaries around your platform-as-a-service (PaaS) resources that are deployed outside your virtual networks. Network security perimeter helps you control public network access to resources like Azure Storage accounts and Azure Key Vault by establishing a secure perimeter.

By default, network security perimeter restricts public access to PaaS resources within the boundary. You can grant exceptions through explicit access rules for inbound and outbound traffic. This approach helps prevent data exfiltration while maintaining necessary connectivity for your applications.

For access patterns involving traffic from virtual networks to PaaS resources, see [What is Azure Private Link?](private-link-overview.md)

Features of a network security perimeter include:

- Resource to resource access communication within perimeter members, preventing data exfiltration to nonauthorized destinations.

- External public access management with explicit rules for PaaS resources associated with the perimeter.

- Access logs for audit and compliance.

- Unified experience across PaaS resources.

[!INCLUDE [network-security-perimeter-preview-message](../../includes/network-security-perimeter-preview-message.md)]

## Components of a network security perimeter

A network security perimeter includes the following components:

| **Component** |**Description**|

|---------------------|------------------------------------------------------------------------------------------------------------|

| **Network security perimeter** | Top level resource defining logical network boundary to secure PaaS resources. |

| **Profile** | Collection of access rules that apply on resources associated with the profile. |

| **Access rule**| Inbound and outbound rules for resources in a perimeter to allow access outside the perimeter. |

| **Resource association** | Perimeter membership for a PaaS resource. |

| **Diagnostics settings** | Extension resource hosted by Microsoft Insights to collect logs & metrics for all resources in the perimeter. |

> [!NOTE]

> For organizational and informational safety, don't include any personally identifiable or sensitive data in the network security perimeter rules or other network security perimeter configurations.

## Network security perimeter properties

When creating a network security perimeter, you can specify the following properties:

| **Property** | **Description** |

|------------------|-------------|

| **Name** | A unique name within the resource group. |

| **Location** | A supported Azure region where the resource is located. |

| **Resource group name** | Name of the resource group where the network security perimeter should be present. |

## Access modes in network security perimeter

Administrators add PaaS resources to a perimeter by creating resource associations. These associations can be made in two access modes. The access modes are:

| **Mode** | **Description** |

|----------------|--------|

| **Transition mode (formerly Learning mode)**  | - Default access mode.</br>- Helps network administrators to understand the existing access patterns of their PaaS resources.</br>- Advised mode of use before transitioning to enforced mode.|

| **Enforced mode**  | - Must be set by the administrator.</br>- By default, all traffic except intra-perimeter traffic is denied in this mode unless an *Allow* access rule exists. |

Learn more on move from transition mode (formerly learning mode) to enforced mode in [Transitioning to a network security perimeter](network-security-perimeter-transition.md) article.

## Why use a network security perimeter?

Network security perimeter provides a secure perimeter for communication of PaaS services deployed outside the virtual network. It allows you to control network access to Azure PaaS resources. Some of the common use cases include:

- Create a secure boundary around  PaaS resources.

- Prevent data exfiltration by associating PaaS resources  to the perimeter.

- Enable access rules to grant access outside the secure perimeter.

- Manage access rules for all the PaaS resources within the network security perimeter in a single pane of glass.

- Enable diagnostic settings to generate access logs of PaaS resources within the perimeter for Audit and Compliance.

- Allow private endpoint traffic without the need for explicit access rules.

## How does a network security perimeter work?

When a network security perimeter is created and the PaaS resources are associated with the perimeter in enforced mode, all public traffic is denied by default thus preventing data exfiltration outside the perimeter.

Access rules can be used to approve public inbound and outbound traffic outside the perimeter. Public inbound access can be approved using Network and Identity attributes of the client such as source IP addresses, subscriptions. Public outbound access can be approved using FQDNs (Fully Qualified Domain Names) of the external destinations.

For example, upon creating a network security perimeter and associating a set of PaaS resources with the perimeter like Azure Key Vault and Azure Storage in enforced mode, all incoming and outgoing public traffic is denied to these PaaS resources by default. To allow any access outside the perimeter, necessary access rules can be created. Within the same perimeter, profiles can be created to group PaaS resources with similar set of inbound and outbound access requirements.

## Onboarded private link resources

A network security perimeter-aware private link resource is a PaaS resource that can be associated with a network security perimeter. Currently the list of onboarded private link resources are as follows:

| Private link resource name | Resource type | Resources | Public cloud Availability | Gov Cloud Availability |

|---------------------------|---------------|-----------| --------- | --------- |

| [Azure Monitor](/azure/azure-monitor/essentials/network-security-perimeter)             | Microsoft.Insights/dataCollectionEndpoints</br>Microsoft.Insights/ScheduledQueryRules</br>Microsoft.Insights/actionGroups</br>Microsoft.OperationalInsights/workspaces | Log Analytics Workspace, Application Insights, Alerts, Notification Service | Generally available | Not Available |

| [Azure AI Search](/azure/search/search-security-network-security-perimiter)          | Microsoft.Search/searchServices | | Generally Available | Not Available |

| [Cosmos DB](/azure/cosmos-db/how-to-configure-nsp)                | Microsoft.DocumentDB/databaseAccounts | | Public Preview | Not Available |

| [Event Hubs](/azure/event-hubs/network-security-perimeter)                | Microsoft.EventHub/namespaces | | Generally Available | Not Available |

| [Key Vault](/azure/key-vault/general/network-security#network-security-perimeter-preview)                 | Microsoft.KeyVault/vaults | | Generally Available | Generally Available |

| [SQL DB](/azure/azure-sql/database/network-security-perimeter)                    | Microsoft.Sql/servers | | Public Preview | Not Available |

| [Storage](/azure/storage/common/storage-network-security#network-security-perimeter-preview)               | Microsoft.Storage/storageAccounts | | Generally Available | Generally Available |

| [Azure OpenAI service](/azure/ai-services/openai/how-to/network-security-perimeter) | Microsoft.CognitiveServices(kind="OpenAI") | | Public Preview | Not Available |

| [Microsoft Foundry](/azure/ai-foundry/how-to/add-foundry-to-network-security-perimeter) | Microsoft.CognitiveServices/accounts<br>Microsoft.CognitiveServices(kind="AIServices") | | Generally Available | Generally Available |

| [Azure Service Bus](/azure/service-bus-messaging/network-security-perimeter) | Microsoft.ServiceBus/namespaces | | Generally Available | Not Available |

> [!IMPORTANT]

> The following onboarded services are in public preview with Network Security Perimeter:

> - Cosmos DB

> - SQL DB

> - Azure OpenAI Service

>

> These previews are provided without a service level agreement, and it's not recommended for production workloads.

> Certain features might not be supported or might have constrained capabilities.

> For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

> [!NOTE]

> Refer to the respective private link resource documentation for information on currently unsupported scenarios.

## Where is network security perimeter available?

Network security perimeter is currently available in all Azure public cloud regions and in Azure Government regions (US Gov Virginia, US Gov Texas, US Gov Arizona, US DoD East and US DoD Central).

## Supported access rule types

Network security perimeter supports the following access rule types:

| Direction | Access rule type |

|---------------------------|---------------|

| Inbound | Subscription-based rules |

| Inbound | IP-based rules (check respective onboarded private link resources for v6 support)|

| Outbound | FQDN-based rules |

> [!NOTE]

> Intra-perimeter traffic and inbound access rules that are subscription-based don't support authentication via shared access signature (SAS) token. In these scenarios, requests that use an SAS token are rejected and display an authentication error. Use an alternative supported authentication method per your specific resource.

## Limitations of a network security perimeter

### Logging limitations

While enabling access logs for network security perimeter, the Log Analytics workspace to be associated with the network security perimeter needs to be located in one of the Azure Monitor supported regions.

> [!NOTE]

> For PaaS resource logs, use **Log Analytics Workspace, Storage or Event Hub** as the log destination associated to the same perimeter as the PaaS resource.

### Microsoft Sentinel limitations

The following are known limitations:

* Network security perimeters aren't supported for Log Analytics workspaces enabled for Microsoft Sentinel. If a network security perimeter is enabled on the workspace, analytic rules are automatically disabled. For more information, see [Prerequisites for deploying Microsoft Sentinel](/azure/sentinel/prerequisites).

* Azure Backup is not supported for Storage Accounts enabled with network security perimeter. We recommend not associating a storage account with network security perimeter if you have backups enabled or if you plan to use Azure Backup.

* Querying workspaces with private link from Advanced hunting is not supported.

[!INCLUDE [network-security-perimeter-limits](../../includes/network-security-perimeter-limits.md)]

## Next steps

> [!div class="nextstepaction"]

> [Create a network security perimeter in the Azure portal](./create-network-security-perimeter-portal.md)


# Availability

# Azure Private Link availability

Azure Private Link enables you to access Azure PaaS Services (for example, Azure Storage and SQL Database) and Azure hosted customer-owned/partner services over a [private endpoint](private-endpoint-overview.md) in your virtual network.

> [!IMPORTANT]

> Azure Private Link is now generally available. Both Private Endpoint and Private Link service (service behind standard load balancer) are generally available. For known limitations, see [Private Endpoint](private-endpoint-overview.md#limitations) and [Private Link Service](private-link-service-overview.md#limitations).

> [!NOTE]

> The feature Private Link Service Direct Connect, which allows you to connect to any privately routable destination IP address, is now in public preview. For more information and known limitations, see [Private Link Service Direct Connect](configure-private-link-service-direct-connect.md)

## Service availability

The following tables list the Private Link services and the regions where they're available.

### AI + Machine Learning

|Supported services  |Available regions | Other considerations | Status  |

|:-------------------|:-----------------|:----------------|:--------|

|Azure Machine Learning | All public regions    |  | GA   <br/> [Learn how to create a private endpoint for Azure Machine Learning.](/azure/machine-learning/how-to-configure-private-link)   |

|Azure Bot Service | All public regions | Supported only on Direct Line App Service extension | GA </br> [Learn how to create a private endpoint for Azure Bot Service](/azure/bot-service/dl-network-isolation-concept) |

| Azure AI Search | All public regions | | GA </br> [Learn how to create a private endpoint for Azure AI Search](/azure/search/service-create-private-endpoint) |

| Foundry Tools | All public regions<br/>All Government regions      |   | GA   <br/> [Use private endpoints.](/azure/ai-services/cognitive-services-virtual-networks#use-private-endpoints)  |

| Azure AI Video Indexer | All public regions  |   | GA   <br/> [Use private endpoints with Azure AI Video Indexer.](/azure/azure-video-indexer/private-endpoint-overview)  |

### Analytics

|Supported services  |Available regions | Other considerations | Status  |

|:-------------------|:-----------------|:----------------|:--------|

|Azure Synapse Analytics| All public regions <br/> All Government regions |  Supported for Proxy [connection policy](/azure/azure-sql/database/connectivity-architecture#connection-policy) |GA <br/> [Learn how to create a private endpoint for Azure Synapse Analytics.](/azure/azure-sql/database/private-endpoint-overview)|

|Azure Event Hubs | All public regions<br/>All Government regions      |   | GA   <br/> [Learn how to create a private endpoint for Azure Event Hubs.](../event-hubs/private-link-service.md)  |

| Azure Monitor <br/>(Log Analytics & Application Insights) | All public regions      |  | GA   <br/> [Learn how to create a private endpoint for Azure Monitor.](/azure/azure-monitor/logs/private-link-security)   |

|Azure Data Factory | All public regions<br/> All Government regions<br/>All China regions    | Credentials need to be stored in an Azure key vault| GA   <br/> [Learn how to create a private endpoint for Azure Data Factory.](../data-factory/data-factory-private-link.md)   |

|Azure HDInsight | All public regions<br/>All Government regions      |   | GA   <br/> [Learn how to create a private endpoint for Azure HDInsight.](../hdinsight/hdinsight-private-link.md)  |

| Azure Data Explorer | All public regions | | GA </br> [Learn how to create a private endpoint for Azure Data Explorer.](/azure/data-explorer/security-network-private-endpoint) |

| Azure Stream Analytics | All public regions | | GA </br> [Learn how to create a private endpoint for Azure Stream Analytics.](../stream-analytics/private-endpoints.md) |

### Compute

|Supported services  |Available regions | Other considerations | Status  |

|:-------------------|:-----------------|:----------------|:--------|

|Azure managed disks | All public regions<br/> All Government regions<br/>All China regions    | [Select for known limitations](/azure/virtual-machines/disks-enable-private-links-for-import-export-portal#limitations) | GA   <br/> [Learn how to create a private endpoint for Azure managed disks.](/azure/virtual-machines/disks-enable-private-links-for-import-export-portal)   |

| Azure Batch (batchAccount) | All public regions<br/> All Government regions<br/>All China regions  | | GA <br/> [Learn how to create a private endpoint for Azure Batch.](../batch/private-connectivity.md) |

| Azure Batch (nodeManagement) | [Selected regions](../batch/simplified-compute-node-communication.md#supported-regions) | Supported for [simplified compute node communication](../batch/simplified-compute-node-communication.md) | GA <br/> [Learn how to create a private endpoint for Azure Batch.](../batch/private-connectivity.md) |

| Azure Functions | All public regions | | GA </br> [Learn how to create a private endpoint for Azure Functions.](../azure-functions/functions-create-vnet.md) |

### Containers

|Supported services  |Available regions | Other considerations | Status  |

|:-------------------|:-----------------|:----------------|:--------|

|Azure Container Registry | All public regions<br/> All Government regions    | Supported with premium tier of container registry. [Select for tiers](/azure/container-registry/container-registry-skus)| GA   <br/> [Learn how to create a private endpoint for Azure Container Registry.](/azure/container-registry/container-registry-private-link)   |

| Azure Container Apps | All public regions | Supported for workload profile environments for both Consumption and Dedicated plans. | Public Preview <br/> [Learn how to create a private endpoint for Azure Container Apps](/azure/container-apps/how-to-use-private-endpoint) |

|Azure Kubernetes Service - Kubernetes API | All public regions <br/> All Government regions  |  | GA   <br/> [Learn how to create a private endpoint for Azure Kubernetes Service.](/azure/aks/private-clusters)   |

### Databases

|Supported services  |Available regions | Other considerations | Status  |

|:-------------------|:-----------------|:----------------|:--------|

|  Azure SQL Database         | All public regions <br/> All Government regions<br/>All China regions      |  Supported for Proxy [connection policy](/azure/azure-sql/database/connectivity-architecture#connection-policy) | GA <br/> [Learn how to create a private endpoint for Azure SQL](./tutorial-private-endpoint-sql-portal.md)      |

| Azure Cosmos DB|  All public regions<br/> All Government regions</br> All China regions | |GA <br/> [Learn how to create a private endpoint for Azure Cosmos DB.](./tutorial-private-endpoint-cosmosdb-portal.md)|

|  Azure Database for PostgreSQL - Single server         | All public regions <br/> All Government regions<br/>All China regions     | Supported for General Purpose and Memory Optimized pricing tiers | GA <br/> [Learn how to create a private endpoint for Azure Database for PostgreSQL Single Server.](/azure/postgresql/concepts-data-access-and-security-private-link)      |

|  Azure Database for PostgreSQL - Flexible server         | All public regions <br/> All Government regions<br/>All China regions     |   | GA <br/> [Learn how to create a private endpoint for Azure Database for PostgreSQL Flexible Server.](/azure/postgresql/flexible-server/concepts-networking-private-link)      |

|  Azure Database for MySQL         | All public regions<br/> All Government regions<br/>All China regions      |  | GA <br/> [Learn how to create a private endpoint for Azure Database for MySQL.](/azure/mysql/concepts-data-access-security-private-link)     |

|  Azure Database for MariaDB         | All public regions<br/> All Government regions<br/>All China regions     |  | GA <br/> [Learn how to create a private endpoint for Azure Database for MariaDB.](/azure/mariadb/concepts-data-access-security-private-link)      |

| Azure Cache for Redis | All public regions<br/> All Government regions<br/>All China regions |  | GA <br/> [Learn how to create a private endpoint for Azure Cache for Redis.](../azure-cache-for-redis/cache-private-link.md) |

> [!NOTE]

> Azure Cache for Redis is being retired in September 2028. New cache creation will be unavailable starting April 2026. We recommend migrating to [Azure Managed Redis](/azure/azure-cache-for-redis/retirement-faq).

### Integration

|Supported services  |Available regions | Other considerations | Status  |

|:-------------------|:-----------------|:----------------|:--------|

|Azure Event Grid| All public regions<br/> All Government regions       |  | GA   <br/> [Learn how to create a private endpoint for Azure Event Grid.](../event-grid/network-security.md) |

|Azure Service Bus | All public region<br/>All Government regions  | Supported with premium tier of Azure Service Bus. [Select for tiers](../service-bus-messaging/service-bus-premium-messaging.md) | GA   <br/> [Learn how to create a private endpoint for Azure Service Bus.](../service-bus-messaging/private-link-service.md)  |

| Azure API Management | All public regions  |  | GA   <br/> [Connect privately to API Management using a private endpoint.](../api-management/private-endpoint.md) |

| Azure Logic Apps | All public regions  |  | GA   <br/> [Learn how to create a private endpoint for Azure Logic Apps.](../logic-apps/secure-single-tenant-workflow-virtual-network-private-endpoint.md) |

| Azure Data Manager for Energy | See [Products available by region](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/?products=energy-data-services&regions=all) | | GA <br/> [Create a private endpoint for Azure Data Manager for Energy](../energy-data-services/how-to-set-up-private-links.md) |

### Internet of Things (IoT)

|Supported services  |Available regions | Other considerations | Status  |

|:-------------------|:-----------------|:----------------|:--------|

| Azure IoT Hub | All public regions    |  | GA   <br/> [Learn how to create a private endpoint for Azure IoT Hub.](../iot-hub/virtual-network-support.md) |

| Azure IoT Device Provisioning Service | All public regions |  |  GA   <br/> [Learn how to create a private endpoint for Azure IoT Device Provisioning Service.](../iot-dps/virtual-network-support.md) |

|  Azure Digital Twins         | All public regions supported by Azure Digital Twins     |  | Preview <br/> [Learn how to create a private endpoint for Azure Digital Twins.](../api-management/private-endpoint.md)  |

### Management and Governance

| Supported services | Available regions | Other considerations | Status  |

| ------------ | ----------------| ------------| ----------------|

| Azure Automation  | All public regions<br/> All Government regions |  | GA </br> [Learn how to create a private endpoint for Azure Automation.](../automation/how-to/private-link-security.md)|

|Azure Backup | All public regions<br/> All Government regions   |  | GA <br/> [Learn how to create a private endpoint for Azure Backup.](../backup/private-endpoints.md)   |

| Microsoft Purview | Southeast Asia, Australia East, Brazil South, North Europe, West Europe, Canada Central, East US, East US 2, EAST US 2 EUAP, South Central US, West Central US, West US 2, Central India, UK South   | [Select for known limitations](../purview/catalog-private-link-troubleshoot.md#known-limitations) | GA <br/> [Learn how to create a private endpoint for Microsoft Purview.](../purview/catalog-private-link.md)   |

| Azure Migrate | All public regions<br/> All Government regions |  | GA </br> [Discover and assess servers for migration using Private Link.](../migrate/discover-and-assess-using-private-endpoints.md) |

### Security

|Supported services  |Available regions | Other considerations | Status  |

|:-------------------|:-----------------|:----------------|:--------|

|  Azure Key Vault         | All public regions<br/> All Government regions      |  | GA   <br/> [Learn how to create a private endpoint for Azure Key Vault.](/azure/key-vault/general/private-link-service)   |

|Azure App Configuration | All public regions<br/> All Government regions<br/>All China regions      |  | GA  </br> [Learn how to create a private endpoint for Azure App Configuration](../azure-app-configuration/concept-private-endpoint.md) |

|Azure Application Gateway | All public regions      |  | GA  </br> [Azure Application Gateway Private Link](../application-gateway/private-link.md) |

### Storage

|Supported services  |Available regions | Other considerations | Status  |

|:-------------------|:-----------------|:----------------|:--------|

| Azure Blob storage (including Data Lake Storage Gen2)       |  All public regions<br/> All Government regions       |  Supported only on Account Kind General Purpose V2 | GA <br/> [Learn how to create a private endpoint for blob storage.](tutorial-private-endpoint-storage-portal.md)  |

| Azure Files | All public regions<br/> All Government regions      | |   GA <br/> [Learn how to create Azure Files network endpoints.](../storage/files/storage-files-networking-endpoints.md)   |

| Azure File Sync | All public regions      | |   GA <br/> [Learn how to create Azure Files network endpoints.](../storage/file-sync/file-sync-networking-endpoints.md)   |

| Azure Queue storage       |  All public regions<br/> All Government regions       |  Supported only on Account Kind General Purpose V2 | GA <br/> [Learn how to create a private endpoint for queue storage.](tutorial-private-endpoint-storage-portal.md) |

| Azure Table storage       |  All public regions<br/> All Government regions       |  Supported only on Account Kind General Purpose V2 | GA <br/> [Learn how to create a private endpoint for table storage.](tutorial-private-endpoint-storage-portal.md)  |

### Web

|Supported services  |Available regions | Other considerations | Status  |

|:-------------------|:-----------------|:----------------|:--------|

| Azure SignalR | All Public Regions<br/> All China regions<br/> All Government Regions      | Supported on Standard Tier or above | GA   <br/> [Learn how to create a private endpoint for Azure SignalR.](../azure-signalr/howto-private-endpoints.md)   |

|Azure App Service | All public regions<br/> China North 2 & East 2    | Supported with Basic, Standard, Premium v2, Premium v3, Isolated v2 App Service Plans and Function Apps Premium plan  | GA   <br/> [Learn how to create a private endpoint for Azure App Service.](../app-service/networking/private-endpoint.md)   |

|Azure Search | All public regions <br/> All Government regions | Supported with service in Private Mode | GA   <br/> [Learn how to create a private endpoint for Azure Search.](/azure/search/service-create-private-endpoint)    |

|Azure Relay | All public regions      |  | GA   <br/> [Learn how to create a private endpoint for Azure Relay.](../azure-relay/private-link-service.md)  |

|Azure Static Web Apps | All public regions      |  | GA <br/> [Configure private endpoint in Azure Static Web Apps](../static-web-apps/private-endpoint.md)  |

### Private Link service

|Supported services  |Available regions | Other considerations | Status  |

|:-------------------|:-----------------|:----------------|:--------|

|Private Link services behind standard Azure Load Balancer | All public regions<br/> All Government regions<br/>All China regions  | Only supported on Standard Load Balancer with VM based backends | GA <br/> [Learn how to create a private link service.](create-private-link-service-portal.md) |

|Private Link Service Direct Connect | North Central US, East US 2, Central US, South Central US, West US, West US 2, West US 3, Asia Southeast, Australia East, Spain Central  | [See known limitations and considerations](configure-private-link-service-direct-connect.md#limitations) | Public Preview <br/> [Learn how to create Private Link Service Direct Connect](configure-private-link-service-direct-connect.md) |

## Next steps

Learn more about Azure Private Link service:

- [What is Azure Private Link?](private-link-overview.md)

- [Create a Private Endpoint using the Azure portal](create-private-endpoint-portal.md)


# Private Link Cost Optimization

# Azure Private Link Cost optimization principles

When you design your architecture, balance security and privacy requirements with financial constraints, and keep secure private connectivity to Azure services and custom workloads. For an overview of Private Link capabilities, see [What is Azure Private Link?](private-link-overview.md) Key considerations include:

- Do your allocated budgets let you meet security and connectivity goals?

- What's the spending pattern for private connectivity across your workloads?

- How can you maximize connectivity investment through better resource selection and use?

A cost-optimized Private Link strategy isn't always the lowest cost option. Balance security effectiveness with financial efficiency. Tactical cost-cutting can create security vulnerabilities and data leakage risks. To get long-term protection and financial responsibility, create a strategy with [risk-based prioritization](/azure/well-architected/cost-optimization/principles), continuous monitoring, and repeatable processes.

Start with the recommended approaches and justify the benefits for your connectivity requirements. After you set your strategy, use these principles through regular assessment and optimization cycles. For comprehensive guidance on cost management, see [Azure Cost Management documentation](/azure/cost-management-billing/) and the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/).

## Understanding Private Link billing components

Azure Private Link costs include several components that directly impact your monthly expenses:

| Cost Component | Description | Billing Model |

|---|---|---|

| **Private Endpoint** | Each private endpoint in your subscription | Per endpoint per hour |

| **Data Processing** | Data processed through private endpoints | Per GB processed |

| **Cross-Region Traffic** | Data transfer between regions via private endpoints | Per GB transferred |

| **Private Link Service** | Custom private link services you create | Per service per hour |

Understanding these billing components helps you make informed decisions about endpoint placement and traffic routing.

## Develop connectivity discipline

Cost optimization for Private Link requires understanding your connectivity requirements and aligning private endpoint investments with business priorities. Set up clear governance and accountability for connectivity decisions. For more on governance frameworks, see [Azure governance documentation](/azure/governance/).

| Recommendation | Benefit |

|---|---|

| **Develop a comprehensive service inventory** that lists all Azure PaaS services, their data classification levels, compliance needs, and business criticality. | A complete inventory lets you make risk-based connectivity decisions and helps prevent over-provisioning expensive private endpoints or leaving critical data paths exposed to the public internet. Prioritize private connectivity investments based on actual business impact and regulatory needs. |

| **Establish clear accountability** for connectivity decisions with defined roles for security, operations, and finance teams. | Clear accountability makes sure connectivity decisions consider both security needs and budget limits. Collaborative decision making helps prevent siloed choices that can compromise security or go over budget, while keeping compliance with organizational data policies. |

| **Create realistic budgets** that cover both immediate private connectivity needs and planned growth in Azure service use. | Proper budgeting lets you predict connectivity costs and helps prevent reactive decisions during security incidents. Plan private endpoint expansion as your service use grows and new compliance needs come up. |

| **Implement [risk assessment frameworks](/azure/cloud-adoption-framework/govern/assess-cloud-risks)** that set minimum connectivity security levels and standard policies for different service types based on data sensitivity and regulatory needs. | Risk-based frameworks give you a structured way to check data exposure risks and make consistent connectivity decisions. They help you find critical services, check data leakage risks, and choose the right private connectivity steps based on business impact and compliance needs, preventing both under-protection of sensitive workloads and over-investment in low-risk services. |

## Choose the right connectivity model

Azure Private Link offers different connectivity patterns with unique cost structures and security benefits. Choose the model that fits your service distribution and privacy needs. For details on Private Link pricing, see [Azure Private Link pricing](https://azure.microsoft.com/pricing/details/private-link/).

| Recommendation | Benefit |

|---|---|

| **Use dedicated private endpoints** for business-critical services with sensitive data or strict compliance needs like financial data, healthcare records, or intellectual property. | You get complete network isolation for sensitive workloads and pay per-endpoint costs only for critical services. This targeted approach gives you granular security control and helps you meet data residency and privacy rules. |

| **Implement shared connectivity patterns** using hub-and-spoke architectures where multiple workloads can use centralized private endpoints through [virtual network peering](/azure/virtual-network/virtual-network-peering-overview). | Shared connectivity reduces per-workload costs by consolidating private endpoints in hub networks. You get economies of scale for common services while maintaining security benefits and reducing operational complexity through centralized management. |

| **Develop phased connectivity rollout** plans that prioritize high-risk data flows and consider budget limits and virtual network design. | This approach gives immediate protection for sensitive data paths and helps manage costs. Expand private connectivity based on data classification, compliance needs, and available budget to optimize for both security and cost. |

## Design for architecture efficiency

Optimize your architecture to get the most value from private connectivity and avoid unnecessary private endpoints. Your architectural decisions directly affect connectivity costs and security. For architectural guidance, see [Azure Well-Architected Framework](/azure/well-architected/) and [Azure Architecture Center](/azure/architecture/).

| Recommendation | Benefit |

|---|---|

| **Use network segmentation strategies** like dedicated connectivity subnets and [DNS integration](/azure/private-link/private-endpoint-dns) to route traffic to private endpoints. | Optimize private endpoint placement and reduce DNS complexity while ensuring proper traffic routing. Efficient network design eliminates unnecessary private endpoints and simplified DNS management reduces operational overhead. |

| **Design application architecture** to consolidate service access patterns through proper use of [service grouping](/azure/private-link/private-endpoint-overview#private-link-resource) and [regional deployment strategies](/azure/architecture/framework/security/design-network-connectivity). | Architectural efficiency reduces the total number of private endpoints required. You can often serve multiple applications through strategically placed private endpoints rather than creating dedicated endpoints for each workload. Fewer private endpoints directly reduce monthly costs while maintaining security benefits through shared private connectivity. |

| **Implement cross-region strategies** that balance data residency requirements and cost efficiency by placing private endpoints in regions with the best pricing and latency. | Regional optimization helps you meet data sovereignty requirements and manage bandwidth and endpoint costs. Use regional pricing differences and minimize data transfer charges with proper endpoint placement. |

## Optimize resource utilization

Get the most value from your private connectivity investments by using included features and aligning endpoints with actual usage patterns.

| Recommendation | Benefit |

|---|---|

| **Take advantage of [Azure Monitor](/azure/azure-monitor/) integration** and built-in telemetry for private endpoint monitoring and traffic analysis without extra monitoring charges. | Get more value from your connectivity investment by using included monitoring features. See how private endpoints are used and analyze traffic patterns to optimize without extra costs. Use this data to decide if you need each endpoint. |

| **Implement [lifecycle management](/azure/private-link/disable-private-endpoint-network-policy)** for private endpoints to automatically clean up unused or redundant connections. | Dynamic lifecycle management stops costs from abandoned private endpoints. Align private connectivity costs with actual service use and avoid paying for endpoints that don't support active workloads. |

| **Consolidate service access** by grouping related services behind fewer private endpoints where security requirements permit, reducing the total number of billable endpoints. | Service consolidation maximizes endpoint utilization while reducing total costs. You can serve multiple related services through shared private connectivity, improving cost efficiency without compromising security for services with similar risk profiles. |

## Monitor and optimize over time

As your Azure environment expands and regulatory requirements evolve, your private connectivity strategy must adapt accordingly. Set up continuous monitoring and regular optimization cycles to maintain cost efficiency.

| Recommendation | Benefit |

|---|---|

| **Configure cost alerts** when Private Link spending approaches predefined budget thresholds using [Azure Cost Management](/azure/cost-management-billing/). | Proactive notifications prevent budget overruns and enable timely adjustments to connectivity strategy. You can respond to cost increases before they impact other initiatives and maintain predictable private connectivity spending. |

| **Conduct quarterly reviews** of private endpoints and their usage patterns to find optimization opportunities through [traffic analytics](/azure/private-link/monitor-private-link). | Regular reviews keep connectivity investments aligned with business priorities and actual usage. Find underused private endpoints or services that need more private connectivity as business requirements and data sensitivity change. |

| **Monitor connection patterns** and traffic flows to optimize endpoint placement and eliminate unused connections using [Private Link monitoring capabilities](monitor-private-link.md). | Understanding actual traffic patterns enables data-driven connectivity decisions. You can adjust private endpoint configurations based on real usage data rather than theoretical requirements, ensuring optimal resource utilization and cost efficiency. |

| **Track connectivity return on investment (ROI)** using [cost management best practices](/azure/cost-management-billing/costs/cost-analysis-common-uses) to measure security value and manage private endpoint decommissioning. | Measuring ROI shows the value of private connectivity and helps guide future investment decisions. Regularly clean up inactive or extra private endpoints to prevent spending that doesn't match security benefits, and free budget for higher-priority connectivity needs and new compliance requirements. |

## Next steps

- [Learn about Azure Private Link features](private-link-overview.md).

- [What is a private endpoint?](private-endpoint-overview.md)

- [Create a private endpoint](create-private-endpoint-portal.md).

- [Monitor Private Link](monitor-private-link.md).

- [Azure Cost Management documentation](/azure/cost-management-billing/).

- [Azure Private Link pricing](https://azure.microsoft.com/pricing/details/private-link/).

- [Azure Well-Architected Framework](/azure/well-architected/).

- [Azure Security Benchmark](/azure/security/benchmarks/introduction).


# Create Private Endpoint Powershell

# Quickstart: Create a private endpoint by using Azure PowerShell

Get started with Azure Private Link by creating and using a private endpoint to connect securely to an Azure App Services web app.

In this quickstart, create a private endpoint for an Azure App Services web app and then create and deploy a virtual machine (VM) to test the private connection.

You can create private endpoints for various Azure services, such as Azure SQL and Azure Storage.

## Prerequisites

- An Azure account with an active subscription. If you don't already have an Azure account, [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An Azure web app with a **PremiumV2-tier** or higher app service plan, deployed in your Azure subscription.

- For more information and an example, see [Quickstart: Create an ASP.NET Core web app in Azure](../app-service/quickstart-dotnetcore.md).

- The example webapp in this article is named **webapp-1**. Replace the example with your webapp name.

- Azure Cloud Shell or Azure PowerShell.

The steps in this quickstart run the Azure PowerShell cmdlets interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the commands in the Cloud Shell, select **Open Cloudshell** at the upper-right corner of a code block. Select **Copy** to copy the code and then paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure PowerShell locally](/powershell/azure/install-azure-powershell) to run the cmdlets. The steps in this article require Azure PowerShell module version 5.4.1 or later. Run `Get-Module -ListAvailable Az` to find your installed version. If you need to upgrade, see [Update the Azure PowerShell module](/powershell/azure/install-Az-ps#update-the-azure-powershell-module).

If you run PowerShell locally, run `Connect-AzAccount` to connect to Azure.

## Create a resource group

An Azure resource group is a logical container where Azure resources are deployed and managed.

Create a resource group with [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup):

```azurepowershell-interactive

$rg = @{

Name = 'test-rg'

Location = 'eastus2'

}

New-AzResourceGroup @rg

```

## Create a virtual network

1. Use [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork) to create a virtual network named **vnet-1** with IP address prefix **10.0.0.0/16** in the **test-rg** resource group and **eastus2** location.

```azurepowershell-interactive

$vnet = @{

Name = 'vnet-1'

ResourceGroupName = 'test-rg'

Location = 'eastus2'

AddressPrefix = '10.0.0.0/16'

}

$virtualNetwork = New-AzVirtualNetwork @vnet

```

1. Azure deploys resources to a subnet within a virtual network. Use [Add-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/add-azvirtualnetworksubnetconfig) to create a subnet configuration named **subnet-1** with address prefix **10.0.0.0/24**.

```azurepowershell-interactive

$subnet = @{

Name = 'subnet-1'

VirtualNetwork = $virtualNetwork

AddressPrefix = '10.0.0.0/24'

}

$subnetConfig = Add-AzVirtualNetworkSubnetConfig @subnet

```

1. Then associate the subnet configuration to the virtual network with [Set-AzVirtualNetwork](/powershell/module/az.network/Set-azVirtualNetwork).

```azurepowershell-interactive

$virtualNetwork | Set-AzVirtualNetwork

```

## Deploy Azure Bastion

Azure Bastion uses your browser to connect to VMs in your virtual network over secure shell (SSH) or remote desktop protocol (RDP) by using their private IP addresses. The VMs don't need public IP addresses, client software, or special configuration. For more information about Azure Bastion, see [Azure Bastion](/azure/bastion/bastion-overview).

>[!NOTE]

>[!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

1. Configure an Azure Bastion subnet for your virtual network. This subnet is reserved exclusively for Azure Bastion resources and must be named **AzureBastionSubnet**.

```azurepowershell-interactive

$subnet = @{

Name = 'AzureBastionSubnet'

VirtualNetwork = $virtualNetwork

AddressPrefix = '10.0.1.0/26'

}

$subnetConfig = Add-AzVirtualNetworkSubnetConfig @subnet

```

1. Set the configuration.

```azurepowershell-interactive

$virtualNetwork | Set-AzVirtualNetwork

```

1. Create a public IP address for Azure Bastion. The bastion host uses the public IP to access secure shell (SSH) and remote desktop protocol (RDP) over port 443.

```azurepowershell-interactive

$ip = @{

ResourceGroupName = 'test-rg'

Name = 'public-ip'

Location = 'eastus2'

AllocationMethod = 'Static'

Sku = 'Standard'

Zone = 1,2,3

}

New-AzPublicIpAddress @ip

```

1. Use the [New-AzBastion](/powershell/module/az.network/new-azbastion) command to create a new Standard SKU Azure Bastion host in the AzureBastionSubnet.

```azurepowershell-interactive

$bastion = @{

Name = 'bastion'

ResourceGroupName = 'test-rg'

PublicIpAddressRgName = 'test-rg'

PublicIpAddressName = 'public-ip'

VirtualNetworkRgName = 'test-rg'

VirtualNetworkName = 'vnet-1'

Sku = 'Basic'

}

New-AzBastion @bastion

```

It takes several minutes for the Bastion resources to deploy.

## Create a private endpoint

An Azure service that supports private endpoints is required to set up the private endpoint and connection to the virtual network. For the examples in this article, we're using an Azure App Services WebApp from the prerequisites. For more information on the Azure services that support a private endpoint, see [Azure Private Link availability](availability.md).

A private endpoint can have a static or dynamically assigned IP address.

> [!IMPORTANT]

> You must have a previously deployed Azure App Services WebApp to proceed with the steps in this article. For more information, see [Prerequisites](#prerequisites).

In this section, you'll:

- Create a private link service connection with [New-AzPrivateLinkServiceConnection](/powershell/module/az.network/new-azprivatelinkserviceconnection).

- Create the private endpoint with [New-AzPrivateEndpoint](/powershell/module/az.network/new-azprivateendpoint).

- Optionally create the private endpoint static IP configuration with [New-AzPrivateEndpointIpConfiguration](/powershell/module/az.network/new-azprivateendpointipconfiguration).

# [**Dynamic IP**](#tab/dynamic-ip)

```azurepowershell-interactive

## Place the previously created webapp into a variable. ##

$webapp = Get-AzWebApp -ResourceGroupName test-rg -Name webapp-1

## Create the private endpoint connection. ##

$pec = @{

Name = 'connection-1'

PrivateLinkServiceId = $webapp.ID

GroupID = 'sites'

}

$privateEndpointConnection = New-AzPrivateLinkServiceConnection @pec

## Place the virtual network you created previously into a variable. ##

$vnet = Get-AzVirtualNetwork -ResourceGroupName 'test-rg' -Name 'vnet-1'

## Create the private endpoint. ##

$pe = @{

ResourceGroupName = 'test-rg'

Name = 'private-endpoint'

Location = 'eastus2'

Subnet = $vnet.Subnets[0]

PrivateLinkServiceConnection = $privateEndpointConnection

}

New-AzPrivateEndpoint @pe

```

# [**Static IP**](#tab/static-ip)

```azurepowershell-interactive

## Place the previously created webapp into a variable. ##

$webapp = Get-AzWebApp -ResourceGroupName test-rg -Name webapp-1

## Create the private endpoint connection. ##

$pec = @{

Name = 'connection-1'

PrivateLinkServiceId = $webapp.ID

GroupID = 'sites'

}

$privateEndpointConnection = New-AzPrivateLinkServiceConnection @pec

## Place the virtual network you created previously into a variable. ##

$vnet = Get-AzVirtualNetwork -ResourceGroupName 'test-rg' -Name 'vnet-1'

## Create the static IP configuration. ##

$ip = @{

Name = 'ipconfig-1'

GroupId = 'sites'

MemberName = 'sites'

PrivateIPAddress = '10.0.0.10'

}

$ipconfig = New-AzPrivateEndpointIpConfiguration @ip

## Create the private endpoint. ##

$pe = @{

ResourceGroupName = 'test-rg'

Name = 'private-endpoint'

Location = 'eastus2'

Subnet = $vnet.Subnets[0]

PrivateLinkServiceConnection = $privateEndpointConnection

IpConfiguration = $ipconfig

}

New-AzPrivateEndpoint @pe

```

- When creating a private endpoint for storage, the connection name shown in a private endpoint tab is auto generated and is not editable.

---

## Configure the private DNS zone

A private DNS zone is used to resolve the DNS name of the private endpoint in the virtual network. For this example, we're using the DNS information for an Azure App Services web app, for more information on the DNS configuration of private endpoints, see [Azure Private Endpoint DNS configuration](private-endpoint-dns.md).

In this section, you'll:

- Create a new private Azure DNS zone with [New-AzPrivateDnsZone](/powershell/module/az.privatedns/new-azprivatednszone)

- Link the DNS zone to the virtual network you created previously with [New-AzPrivateDnsVirtualNetworkLink](/powershell/module/az.privatedns/new-azprivatednsvirtualnetworklink)

- Create a DNS zone configuration with [New-AzPrivateDnsZoneConfig](/powershell/module/az.network/new-azprivatednszoneconfig)

- Create a DNS zone group with [New-AzPrivateDnsZoneGroup](/powershell/module/az.network/new-azprivatednszonegroup)

```azurepowershell-interactive

## Place the virtual network into a variable. ##

$vnet = Get-AzVirtualNetwork -ResourceGroupName 'test-rg' -Name 'vnet-1'

## Create the private DNS zone. ##

$zn = @{

ResourceGroupName = 'test-rg'

Name = 'privatelink.azurewebsites.net'

}

$zone = New-AzPrivateDnsZone @zn

## Create a DNS network link. ##

$lk = @{

ResourceGroupName = 'test-rg'

ZoneName = 'privatelink.azurewebsites.net'

Name = 'dns-link'

VirtualNetworkId = $vnet.Id

}

$link = New-AzPrivateDnsVirtualNetworkLink @lk

## Configure the DNS zone. ##

$cg = @{

Name = 'privatelink.azurewebsites.net'

PrivateDnsZoneId = $zone.ResourceId

}

$config = New-AzPrivateDnsZoneConfig @cg

## Create the DNS zone group. ##

$zg = @{

ResourceGroupName = 'test-rg'

PrivateEndpointName = 'private-endpoint'

Name = 'zone-group'

PrivateDnsZoneConfig = $config

}

New-AzPrivateDnsZoneGroup @zg

```

## Create a test virtual machine

To verify the static IP address and the functionality of the private endpoint, a test virtual machine connected to your virtual network is required.

In this section, you'll:

- Create a sign-in credential for the virtual machine with [Get-Credential](/powershell/module/microsoft.powershell.security/get-credential)

- Create a network interface for the virtual machine with [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface)

- Create a virtual machine configuration with [New-AzVMConfig](/powershell/module/az.compute/new-azvmconfig), [Set-AzVMOperatingSystem](/powershell/module/az.compute/set-azvmoperatingsystem), [Set-AzVMSourceImage](/powershell/module/az.compute/set-azvmsourceimage), and [Add-AzVMNetworkInterface](/powershell/module/az.compute/add-azvmnetworkinterface)

- Create the virtual machine with [New-AzVM](/powershell/module/az.compute/new-azvm)

```azurepowershell-interactive

## Create the credential for the virtual machine. Enter a username and password at the prompt. ##

$cred = Get-Credential

## Place the virtual network into a variable. ##

$vnet = Get-AzVirtualNetwork -Name vnet-1 -ResourceGroupName test-rg

## Create a network interface for the virtual machine. ##

$nic = @{

Name = 'nic-1'

ResourceGroupName = 'test-rg'

Location = 'eastus2'

Subnet = $vnet.Subnets[0]

}

$nicVM = New-AzNetworkInterface @nic

## Create the configuration for the virtual machine. ##

$vm1 = @{

VMName = 'vm-1'

VMSize = 'Standard_DS1_v2'

}

$vm2 = @{

ComputerName = 'vm-1'

Credential = $cred

}

$vm3 = @{

PublisherName = 'MicrosoftWindowsServer'

Offer = 'WindowsServer'

Skus = '2022-Datacenter'

Version = 'latest'

}

$vmConfig =

New-AzVMConfig @vm1 | Set-AzVMOperatingSystem -Windows @vm2 | Set-AzVMSourceImage @vm3 | Add-AzVMNetworkInterface -Id $nicVM.Id

## Create the virtual machine. ##

New-AzVM -ResourceGroupName 'test-rg' -Location 'eastus2' -VM $vmConfig

```

>[!NOTE]

>Virtual machines in a virtual network with a bastion host don't need public IP addresses. Bastion provides the public IP, and the VMs use private IPs to communicate within the network. You can remove the public IPs from any VMs in bastion hosted virtual networks. For more information, see [Dissociate a public IP address from an Azure VM](../virtual-network/ip-services/remove-public-ip-address-vm.md).

[!INCLUDE [ephemeral-ip-note.md](~/reusable-content/ce-skilling/azure/includes/ephemeral-ip-note.md)]

## Test connectivity to the private endpoint

Use the virtual machine that you created earlier to connect to the web app across the private endpoint.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines**.

1. Select **vm-1**.

1. On the overview page for **vm-1**, select **Connect**, and then select the **Bastion** tab.

1. Select **Use Bastion**.

1. Enter the username and password that you used when you created the VM.

1. Select **Connect**.

1. After you've connected, open PowerShell on the server.

1. Enter `nslookup webapp-1.azurewebsites.net`. You receive a message that's similar to the following example:

```output

Server:  UnKnown

Address:  168.63.129.16

Non-authoritative answer:

Name:    webapp-1.privatelink.azurewebsites.net

Address:  10.0.0.10

Aliases:  webapp-1.azurewebsites.net

```

A private IP address of **10.0.0.10** is returned for the web app name if you chose static IP address in the previous steps. This address is in the subnet of the virtual network you created earlier.

1. In the bastion connection to **vm-1**, open the web browser.

1. Enter the URL of your web app, `https://webapp-1.azurewebsites.net`.

If your web app hasn't been deployed, you get the following default web app page:

## Clean up resources

When no longer needed, you can use the [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) command to remove the resource group, virtual network, and the remaining resources.

```azurepowershell-interactive

Remove-AzResourceGroup -Name 'test-rg'

```

## Next steps

For more information about the services that support private endpoints, see:

> [!div class="nextstepaction"]

> [What is Azure Private Link?](private-link-overview.md#availability)


# Create Private Endpoint Cli

# Quickstart: Create a private endpoint by using the Azure CLI

Get started with Azure Private Link by creating and using a private endpoint to connect securely to an Azure web app.

In this quickstart, create a private endpoint for an Azure App Services web app and then create and deploy a virtual machine (VM) to test the private connection.

You can create private endpoints for various Azure services, such as Azure SQL and Azure Storage.

## Prerequisites

* An Azure account with an active subscription. If you don't already have an Azure account, [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

* An Azure web app with a *PremiumV2-tier* or higher app service plan, deployed in your Azure subscription.

- For more information and an example, see [Quickstart: Create an ASP.NET Core web app in Azure](../app-service/quickstart-dotnetcore.md).

- The example webapp in this article is named **webapp-1**. Replace the example with your webapp name.

[!INCLUDE [azure-cli-prepare-your-environment.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment-no-header.md)]

## Create a resource group

An Azure resource group is a logical container where Azure resources are deployed and managed.

First, create a resource group by using **[az group create](/cli/azure/group#az-group-create)**:

```azurecli-interactive

az group create \

--name test-rg \

--location eastus2

```

## Create a virtual network and bastion host

A virtual network and subnet is required for to host the private IP address for the private endpoint. You create a bastion host to connect securely to the virtual machine to test the private endpoint. You create the virtual machine in a later section.

>[!NOTE]

>[!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

Create a virtual network with **[az network vnet create](/cli/azure/network/vnet#az-network-vnet-create)**.

```azurecli-interactive

az network vnet create \

--resource-group test-rg \

--location eastus2 \

--name vnet-1 \

--address-prefixes 10.0.0.0/16 \

--subnet-name subnet-1 \

--subnet-prefixes 10.0.0.0/24

```

Create a bastion subnet with **[az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-create)**.

```azurecli-interactive

az network vnet subnet create \

--resource-group test-rg \

--name AzureBastionSubnet \

--vnet-name vnet-1 \

--address-prefixes 10.0.1.0/26

```

Create a public IP address for the bastion host with **[az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create)**.

```azurecli-interactive

az network public-ip create \

--resource-group test-rg \

--name public-ip \

--sku Standard \

--zone 1 2 3

```

Create the bastion host with **[az network bastion create](/cli/azure/network/bastion#az-network-bastion-create)**.

```azurecli-interactive

az network bastion create \

--resource-group test-rg \

--name bastion \

--public-ip-address public-ip \

--vnet-name vnet-1 \

--location eastus2 \

--sku Basic

```

It can take a few minutes for the Azure Bastion host to deploy.

## Create a private endpoint

An Azure service that supports private endpoints is required to set up the private endpoint and connection to the virtual network. For the examples in this article, use the Azure WebApp from the prerequisites. For more information on the Azure services that support a private endpoint, see [Azure Private Link availability](availability.md).

A private endpoint can have a static or dynamically assigned IP address.

> [!IMPORTANT]

> You must have a previously deployed Azure App Services WebApp to proceed with the steps in this article. For more information, see [Prerequisites](#prerequisites) .

Place the resource ID of the web app that you created earlier into a shell variable with **[az webapp list](/cli/azure/webapp#az-webapp-list)**. Create the private endpoint with **[az network private-endpoint create](/cli/azure/network/private-endpoint#az-network-private-endpoint-create)**.

# [**Dynamic IP**](#tab/dynamic-ip)

```azurecli-interactive

id=$(az webapp list \

--resource-group test-rg \

--query '[].[id]' \

--output tsv)

az network private-endpoint create \

--connection-name connection-1 \

--name private-endpoint \

--private-connection-resource-id $id \

--resource-group test-rg \

--subnet subnet-1 \

--group-id sites \

--vnet-name vnet-1

```

# [**Static IP**](#tab/static-ip)

```azurecli-interactive

id=$(az webapp list \

--resource-group test-rg \

--query '[].[id]' \

--output tsv)

az network private-endpoint create \

--connection-name connection-1 \

--name private-endpoint \

--private-connection-resource-id $id \

--resource-group test-rg \

--subnet subnet-1 \

--group-id sites \

--ip-config name=ipconfig-1 group-id=sites member-name=sites private-ip-address=10.0.0.10 \

--vnet-name vnet-1

```

---

## Configure the private DNS zone

A private DNS zone is used to resolve the DNS name of the private endpoint in the virtual network. For this example, we're using the DNS information for an Azure WebApp, for more information on the DNS configuration of private endpoints, see [Azure Private Endpoint DNS configuration](private-endpoint-dns.md).

Create a new private Azure DNS zone with **[az network private-dns zone create](/cli/azure/network/private-dns/zone#az-network-private-dns-zone-create)**.

```azurecli-interactive

az network private-dns zone create \

--resource-group test-rg \

--name "privatelink.azurewebsites.net"

```

Link the DNS zone to the virtual network you created previously with **[az network private-dns link vnet create](/cli/azure/network/private-dns/link/vnet#az-network-private-dns-link-vnet-create)**.

```azurecli-interactive

az network private-dns link vnet create \

--resource-group test-rg \

--zone-name "privatelink.azurewebsites.net" \

--name dns-link \

--virtual-network vnet-1 \

--registration-enabled false

```

Create a DNS zone group with **[az network private-endpoint dns-zone-group create](/cli/azure/network/private-endpoint/dns-zone-group#az-network-private-endpoint-dns-zone-group-create)**.

```azurecli-interactive

az network private-endpoint dns-zone-group create \

--resource-group test-rg \

--endpoint-name private-endpoint \

--name zone-group \

--private-dns-zone "privatelink.azurewebsites.net" \

--zone-name webapp

```

## Create a test virtual machine

To verify the static IP address and the functionality of the private endpoint, a test virtual machine connected to your virtual network is required.

Create the virtual machine with **[az vm create](/cli/azure/vm#az-vm-create)**.

```azurecli-interactive

az vm create \

--resource-group test-rg \

--name vm-1 \

--image Win2022Datacenter \

--public-ip-address "" \

--vnet-name vnet-1 \

--subnet subnet-1 \

--admin-username azureuser

```

>[!NOTE]

>Virtual machines in a virtual network with a bastion host don't need public IP addresses. Bastion provides the public IP, and the VMs use private IPs to communicate within the network. You can remove the public IPs from any VMs in bastion hosted virtual networks. For more information, see [Dissociate a public IP address from an Azure VM](../virtual-network/ip-services/remove-public-ip-address-vm.md).

[!INCLUDE [ephemeral-ip-note.md](~/reusable-content/ce-skilling/azure/includes/ephemeral-ip-note.md)]

## Test connectivity to the private endpoint

Use the virtual machine that you created earlier to connect to the web app across the private endpoint.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines**.

1. Select **vm-1**.

1. On the overview page for **vm-1**, select **Connect**, and then select the **Bastion** tab.

1. Select **Use Bastion**.

1. Enter the username and password that you used when you created the VM.

1. Select **Connect**.

1. After you've connected, open PowerShell on the server.

1. Enter `nslookup webapp-1.azurewebsites.net`. You receive a message that's similar to the following example:

```output

Server:  UnKnown

Address:  168.63.129.16

Non-authoritative answer:

Name:    webapp-1.privatelink.azurewebsites.net

Address:  10.0.0.10

Aliases:  webapp-1.azurewebsites.net

```

A private IP address of **10.0.0.10** is returned for the web app name if you chose static IP address in the previous steps. This address is in the subnet of the virtual network you created earlier.

1. In the bastion connection to **vm-1**, open the web browser.

1. Enter the URL of your web app, `https://webapp-1.azurewebsites.net`.

If your web app hasn't been deployed, you get the following default web app page:

1. Close the connection to **vm-1**.

## Clean up resources

When no longer needed, use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, private link service, load balancer, and all related resources.

```azurecli-interactive

az group delete \

--name test-rg

```

## Next steps

For more information about the services that support private endpoints, see:

> [!div class="nextstepaction"]

> [What is Azure Private Link?](private-link-overview.md#availability)


# Create Private Endpoint Bicep

# Quickstart: Create a private endpoint using Bicep

In this quickstart, you'll use Bicep to create a private endpoint.

[!INCLUDE [About Bicep](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-bicep-introduction.md)]

You can also create a private endpoint by using the [Azure portal](create-private-endpoint-portal.md), [Azure PowerShell](create-private-endpoint-powershell.md), the [Azure CLI](create-private-endpoint-cli.md), or an [Azure Resource Manager Template](create-private-endpoint-template.md).

## Prerequisites

You need an Azure account with an active subscription. If you don't already have an Azure account, [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Review the Bicep file

This Bicep file creates a private endpoint for an instance of Azure SQL Database.

The Bicep file that this quickstart uses is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/private-endpoint-sql/).

The Bicep file defines multiple Azure resources:

- [**Microsoft.Sql/servers**](/azure/templates/microsoft.sql/servers): The instance of SQL Database with the sample database.

- [**Microsoft.Sql/servers/databases**](/azure/templates/microsoft.sql/servers/databases): The sample database.

- [**Microsoft.Network/virtualNetworks**](/azure/templates/microsoft.network/virtualnetworks): The virtual network where the private endpoint is deployed.

- [**Microsoft.Network/privateEndpoints**](/azure/templates/microsoft.network/privateendpoints): The private endpoint that you use to access the instance of SQL Database.

- [**Microsoft.Network/privateDnsZones**](/azure/templates/microsoft.network/privatednszones): The zone that you use to resolve the private endpoint IP address.

- [**Microsoft.Network/privateDnsZones/virtualNetworkLinks**](/azure/templates/microsoft.network/privatednszones/virtualnetworklinks)

- [**Microsoft.Network/privateEndpoints/privateDnsZoneGroups**](/azure/templates/microsoft.network/privateendpoints/privateDnsZoneGroups): The zone group that you use to associate the private endpoint with a private DNS zone.

- [**Microsoft.Network/publicIpAddresses**](/azure/templates/microsoft.network/publicIpAddresses): The public IP address that you use to access the virtual machine.

- [**Microsoft.Network/networkInterfaces**](/azure/templates/microsoft.network/networkinterfaces): The network interface for the virtual machine.

- [**Microsoft.Compute/virtualMachines**](/azure/templates/microsoft.compute/virtualmachines): The virtual machine that you use to test the connection of the private endpoint to the instance of SQL Database.

## Deploy the Bicep file

1. Save the Bicep file as **main.bicep** to your local computer.

1. Deploy the Bicep file using either Azure CLI or Azure PowerShell.

# [CLI](#tab/CLI)

```azurecli

az group create --name exampleRG --location eastus

az deployment group create --resource-group exampleRG --template-file main.bicep --parameters sqlAdministratorLogin=<admin-login> vmAdminUsername=<vm-login>

```

# [PowerShell](#tab/PowerShell)

```azurepowershell

New-AzResourceGroup -Name exampleRG -Location eastus

New-AzResourceGroupDeployment -ResourceGroupName exampleRG -TemplateFile ./main.bicep -sqlAdministratorLogin "<admin-login>" -vmAdminUsername "<vm-login>"

```

---

> [!NOTE]

> Replace **\<admin-login\>** with the username for the SQL logical server. Replace **\<vm-login\>** with the username for the virtual machine. You'll be prompted to enter **sqlAdministratorLoginPassword**. You'll also be prompted to enter **vmAdminPassword**, which must be at least 12 characters long and contain at least one lowercase and uppercase character and one special character.

When the deployment finishes, you should see a message indicating the deployment succeeded.

## Validate the deployment

> [!NOTE]

> The Bicep file generates a unique name for the virtual machine myVm<b>{uniqueid}</b> resource, and for the SQL Database sqlserver<b>{uniqueid}</b> resource. Substitute your generated value for **{uniqueid}**.

### Connect to a VM from the internet

Connect to the VM _myVm{uniqueid}_ from the internet by doing the following:

1. In the Azure portal search bar, enter _myVm{uniqueid}_.

1. Select **Connect**. **Connect to virtual machine** opens.

1. Select **Download RDP File**. Azure creates a Remote Desktop Protocol (RDP) file and downloads it to your computer.

1. Open the downloaded RDP file.

a. If you're prompted, select **Connect**.

b. Enter the username and password that you specified when you created the VM.

> [!NOTE]

> You might need to select **More choices** > **Use a different account** to specify the credentials you entered when you created the VM.

1. Select **OK**.

You might receive a certificate warning during the sign-in process. If you do, select **Yes** or **Continue**.

1. After the VM desktop appears, minimize it to go back to your local desktop.

### Access the SQL Database server privately from the VM

To connect to the SQL Database server from the VM by using the private endpoint, do the following:

1.  On the Remote Desktop of _myVM{uniqueid}_, open PowerShell.

1.  Run the following command:

`nslookup sqlserver{uniqueid}.database.windows.net`

You'll receive a message that's similar to this one:

```

Server:  UnKnown

Address:  168.63.129.16

Non-authoritative answer:

Name:    sqlserver.privatelink.database.windows.net

Address:  10.0.0.5

Aliases:  sqlserver.database.windows.net

```

1.  Install SQL Server Management Studio.

1.  On the **Connect to server** pane, do the following:

- For **Server type**, select **Database Engine**.

- For **Server name**, select **sqlserver{uniqueid}.database.windows.net**.

- For **Username**, enter the username that was provided earlier.

- For **Password**, enter the password that was provided earlier.

- For **Remember password**, select **Yes**.

1. Select **Connect**.

1. On the left pane, select **Databases**. Optionally, you can create or query information from _sample-db_.

1. Close the Remote Desktop connection to _myVm{uniqueid}_.

## Clean up resources

When you no longer need the resources that you created with the private link service, delete the resource group. This removes the private link service and all the related resources.

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

For more information about the services that support private endpoints, see:

> [!div class="nextstepaction"]

> [What is Azure Private Link?](private-link-overview.md#availability)


# Create Private Endpoint Template

# Quickstart: Create a private endpoint by using an ARM template

In this quickstart, you'll use an Azure Resource Manager template (ARM template) to create a private endpoint.

[!INCLUDE [About Azure Resource Manager](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-introduction.md)]

You can also create a private endpoint by using the [Azure portal](create-private-endpoint-portal.md), [Azure PowerShell](create-private-endpoint-powershell.md), or the [Azure CLI](create-private-endpoint-cli.md).

If your environment meets the prerequisites and you're familiar with using ARM templates, select the **Deploy to Azure** button here. The ARM template will open in the Azure portal.

## Prerequisites

You need an Azure account with an active subscription. If you don't already have an Azure account, [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Review the template

This template creates a private endpoint for an instance of Azure SQL Database.

The template that this quickstart uses is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/private-endpoint-sql/).

The template defines multiple Azure resources:

- [**Microsoft.Sql/servers**](/azure/templates/microsoft.sql/servers): The instance of SQL Database with the sample database.

- [**Microsoft.Sql/servers/databases**](/azure/templates/microsoft.sql/servers/databases): The sample database.

- [**Microsoft.Network/virtualNetworks**](/azure/templates/microsoft.network/virtualnetworks): The virtual network where the private endpoint is deployed.

- [**Microsoft.Network/privateEndpoints**](/azure/templates/microsoft.network/privateendpoints): The private endpoint that you use to access the instance of SQL Database.

- [**Microsoft.Network/privateDnsZones**](/azure/templates/microsoft.network/privatednszones): The zone that you use to resolve the private endpoint IP address.

- [**Microsoft.Network/privateDnsZones/virtualNetworkLinks**](/azure/templates/microsoft.network/privatednszones/virtualnetworklinks)

- [**Microsoft.Network/privateEndpoints/privateDnsZoneGroups**](/azure/templates/microsoft.network/privateendpoints/privateDnsZoneGroups): The zone group that you use to associate the private endpoint with a private DNS zone.

- [**Microsoft.Network/publicIpAddresses**](/azure/templates/microsoft.network/publicIpAddresses): The public IP address that you use to access the virtual machine.

- [**Microsoft.Network/networkInterfaces**](/azure/templates/microsoft.network/networkinterfaces): The network interface for the virtual machine.

- [**Microsoft.Compute/virtualMachines**](/azure/templates/microsoft.compute/virtualmachines): The virtual machine that you use to test the connection of the private endpoint to the instance of SQL Database.

## Deploy the template

Deploy the ARM template to Azure by doing the following:

1. Sign in to Azure and open the ARM template by selecting the **Deploy to Azure** button here. The template creates the private endpoint, the instance of SQL Database, the network infrastructure, and a virtual machine to be validated.

1. Select your resource group or create a new one.

1. Enter the SQL administrator sign-in name and password.

1. Enter the virtual machine administrator username and password.

1. Read the terms and conditions statement. If you agree, select **I agree to the terms and conditions stated above**, and then select **Purchase**. The deployment can take 20 minutes or longer to complete.

## Validate the deployment

> [!NOTE]

> The ARM template generates a unique name for the virtual machine myVm<b>{uniqueid}</b> resource, and for the SQL Database sqlserver<b>{uniqueid}</b> resource. Substitute your generated value for **{uniqueid}**.

### Connect to a VM from the internet

Connect to the VM _myVm{uniqueid}_ from the internet by doing the following:

1. In the portal's search bar, enter _myVm{uniqueid}_.

1. Select **Connect**. **Connect to virtual machine** opens.

1. Select **Download RDP File**. Azure creates a Remote Desktop Protocol (RDP) file and downloads it to your computer.

1. Open the downloaded RDP file.

a. If you're prompted, select **Connect**.

b. Enter the username and password that you specified when you created the VM.

> [!NOTE]

> You might need to select **More choices** > **Use a different account** to specify the credentials you entered when you created the VM.

1. Select **OK**.

You might receive a certificate warning during the sign-in process. If you do, select **Yes** or **Continue**.

1. After the VM desktop appears, minimize it to go back to your local desktop.

### Access the SQL Database server privately from the VM

To connect to the SQL Database server from the VM by using the private endpoint, do the following:

1.  On the Remote Desktop of _myVM{uniqueid}_, open PowerShell.

1.  Run the following command:

`nslookup sqlserver{uniqueid}.database.windows.net`

You'll receive a message that's similar to this one:

```

Server:  UnKnown

Address:  168.63.129.16

Non-authoritative answer:

Name:    sqlserver.privatelink.database.windows.net

Address:  10.0.0.5

Aliases:  sqlserver.database.windows.net

```

1.  Install SQL Server Management Studio.

1.  On the **Connect to server** pane, do the following:

- For **Server type**, select **Database Engine**.

- For **Server name**, select **sqlserver{uniqueid}.database.windows.net**.

- For **Username**, enter the username that was provided earlier.

- For **Password**, enter the password that was provided earlier.

- For **Remember password**, select **Yes**.

1. Select **Connect**.

1. On the left pane, select **Databases**. Optionally, you can create or query information from _sample-db_.

1. Close the Remote Desktop connection to _myVm{uniqueid}_.

## Clean up resources

When you no longer need the resources that you created with the private endpoint, delete the resource group. Doing so removes the private endpoint and all the related resources.

To delete the resource group, run the `Remove-AzResourceGroup` cmdlet:

```azurepowershell-interactive

Remove-AzResourceGroup -Name <your resource group name>

```

## Next steps

For more information about the services that support private endpoints, see:

> [!div class="nextstepaction"]

> [What is Azure Private Link?](private-link-overview.md#availability)


# Create Private Endpoint Terraform

# Quickstart: Create a private endpoint by using Terraform

In this quickstart, you use Terraform to create a private endpoint. The private endpoint connects to an Azure SQL Database. The private endpoint is associated with a virtual network and a private Domain Name System (DNS) zone. The private DNS zone resolves the private endpoint IP address. The virtual network contains a virtual machine that you use to test the connection of the private endpoint to the instance of the SQL Database.

The script generates a random password for the SQL server and a random SSH key for the virtual machine. The names of the created resources are output when the script is run.

[!INCLUDE [About Terraform](~/azure-dev-docs-pr/articles/terraform/includes/abstract.md)]

## Prerequisites

- You need an Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- [Install and configure Terraform](/azure/developer/terraform/quickstart-configure).

## Implement the Terraform code

> [!NOTE]

> The sample code for this article is located in the [Azure Terraform GitHub repo](https://github.com/Azure/terraform/tree/master/quickstart/201-private-link-sql-database).

>

> See more [articles and sample code showing how to use Terraform to manage Azure resources](/azure/terraform)

1. Create a directory in which to test and run the sample Terraform code and make it the current directory.

1. Create a file named `main.tf` and insert the following code:

1. Create a file named `outputs.tf` and insert the following code:

1. Create a file named `provider.tf` and insert the following code:

1. Create a file named `ssh.tf` and insert the following code:

1. Create a file named `variables.tf` and insert the following code:

## Initialize Terraform

[!INCLUDE [terraform-init.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-init.md)]

## Create a Terraform execution plan

[!INCLUDE [terraform-plan.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-plan.md)]

## Apply a Terraform execution plan

[!INCLUDE [terraform-apply-plan.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-apply-plan.md)]

## Verify the results

#### [Azure CLI](#tab/azure-cli)

1. Get the Azure resource group name.

```console

resource_group_name=$(terraform output -raw resource_group_name)

```

1. Get the SQL Server name.

```console

sql_server=$(terraform output -raw sql_server)

```

1. Run [az sql server show](/cli/azure/sql/server#az-sql-server-show) to display the details about the SQL Server private endpoint.

```azurecli

az sql server show \

--resource-group $resource_group_name \

--name $sql_server --query privateEndpointConnections \

--output tsv

```

#### [Azure PowerShell](#tab/azure-powershell)

1. Get the Azure resource group name.

```console

$resource_group_name=$(terraform output -raw resource_group_name)

```

1. Get the SQL Server name.

```console

$sql_server=$(terraform output -raw sql_server_name)

```

1. Run [Get-AzPrivateEndpoint](/powershell/module/az.network/get-azprivateendpoint) to display the details about the SQL Server private endpoint.

```azurepowershell

$sql = @{

ResourceGroupName = $resource_group_name

}

Get-AzPrivateEndpoint @sql

```

---

## Clean up resources

[!INCLUDE [terraform-plan-destroy.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-plan-destroy.md)]

## Troubleshoot Terraform on Azure

[Troubleshoot common problems when using Terraform on Azure.](/azure/developer/terraform/troubleshoot)

## Next steps

> [!div class="nextstepaction"]

> [Learn more about using Terraform in Azure](/azure/terraform)


# Create Private Link Service Powershell

# Quickstart: Create a Private Link service using Azure PowerShell

Get started creating a Private Link service that refers to your service.  Give Private Link access to your service or resource deployed behind an Azure Standard Load Balancer.  Users of your service have private access from their virtual network.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- Azure Cloud Shell or Azure PowerShell.

The steps in this quickstart run the Azure PowerShell cmdlets interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the commands in the Cloud Shell, select **Open Cloudshell** at the upper-right corner of a code block. Select **Copy** to copy the code and then paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also [install Azure PowerShell locally](/powershell/azure/install-azure-powershell) to run the cmdlets. The steps in this article require Azure PowerShell module version 5.4.1 or later. Run `Get-Module -ListAvailable Az` to find your installed version. If you need to upgrade, see [Update the Azure PowerShell module](/powershell/azure/install-Az-ps#update-the-azure-powershell-module).

If you run PowerShell locally, run `Connect-AzAccount` to connect to Azure.

## Create a resource group

An Azure resource group is a logical container into which Azure resources are deployed and managed.

Create a resource group with [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup):

```azurepowershell-interactive

New-AzResourceGroup -Name 'test-rg' -Location 'eastus2'

```

## Create an internal load balancer

In this section, you create a virtual network and an internal Azure Load Balancer.

### Virtual network

In this section, you create a virtual network and subnet to host the load balancer that accesses your Private Link service.

* Create a virtual network with [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork).

```azurepowershell-interactive

## Create backend subnet config ##

$subnet = @{

Name = 'subnet-1'

AddressPrefix = '10.0.0.0/24'

}

$subnetConfig = New-AzVirtualNetworkSubnetConfig @subnet

## Create the virtual network ##

$net = @{

Name = 'vnet-1'

ResourceGroupName = 'test-rg'

Location = 'eastus2'

AddressPrefix = '10.0.0.0/16'

Subnet = $subnetConfig

}

$vnet = New-AzVirtualNetwork @net

```

### Create standard load balancer

This section details how you can create and configure the following components of the load balancer:

* Create a front-end IP with [New-AzLoadBalancerFrontendIpConfig](/powershell/module/az.network/new-azloadbalancerfrontendipconfig) for the frontend IP pool. This IP receives the incoming traffic on the load balancer

* Create a back-end address pool with [New-AzLoadBalancerBackendAddressPoolConfig](/powershell/module/az.network/new-azloadbalancerbackendaddresspoolconfig) for traffic sent from the frontend of the load balancer. This pool is where your backend virtual machines are deployed.

* Create a health probe with [Add-AzLoadBalancerProbeConfig](/powershell/module/az.network/add-azloadbalancerprobeconfig) that determines the health of the backend VM instances.

* Create a load balancer rule with [Add-AzLoadBalancerRuleConfig](/powershell/module/az.network/add-azloadbalancerruleconfig) that defines how traffic is distributed to the VMs.

* Create a public load balancer with [New-AzLoadBalancer](/powershell/module/az.network/new-azloadbalancer).

```azurepowershell-interactive

## Place virtual network created in previous step into a variable. ##

$vnet = Get-AzVirtualNetwork -Name 'vnet-1' -ResourceGroupName 'test-rg'

## Create load balancer frontend configuration and place in variable. ##

$lbip = @{

Name = 'frontend'

PrivateIpAddress = '10.0.0.4'

SubnetId = $vnet.subnets[0].Id

}

$feip = New-AzLoadBalancerFrontendIpConfig @lbip

## Create backend address pool configuration and place in variable. ##

$bepool = New-AzLoadBalancerBackendAddressPoolConfig -Name 'backend-pool'

## Create the health probe and place in variable. ##

$probe = @{

Name = 'health-probe'

Protocol = 'http'

Port = '80'

IntervalInSeconds = '360'

ProbeCount = '5'

RequestPath = '/'

}

$healthprobe = New-AzLoadBalancerProbeConfig @probe

## Create the load balancer rule and place in variable. ##

$lbrule = @{

Name = 'http-rule'

Protocol = 'tcp'

FrontendPort = '80'

BackendPort = '80'

IdleTimeoutInMinutes = '15'

FrontendIpConfiguration = $feip

BackendAddressPool = $bePool

}

$rule = New-AzLoadBalancerRuleConfig @lbrule -EnableTcpReset

## Create the load balancer resource. ##

$loadbalancer = @{

ResourceGroupName = 'test-rg'

Name = 'load-balancer'

Location = 'eastus2'

Sku = 'Standard'

FrontendIpConfiguration = $feip

BackendAddressPool = $bePool

LoadBalancingRule = $rule

Probe = $healthprobe

}

New-AzLoadBalancer @loadbalancer

```

## Disable network policy

Before a private link service can be created in the virtual network, the setting `privateLinkServiceNetworkPolicies` must be disabled.

* Disable the network policy with [Set-AzVirtualNetwork](/powershell/module/az.network/Set-AzVirtualNetwork).

```azurepowershell-interactive

## Place the subnet name into a variable. ##

$subnet = 'subnet-1'

## Place the virtual network configuration into a variable. ##

$net = @{

Name = 'vnet-1'

ResourceGroupName = 'test-rg'

}

$vnet = Get-AzVirtualNetwork @net

## Set the policy as disabled on the virtual network. ##

($vnet | Select -ExpandProperty subnets | Where-Object {$_.Name -eq $subnet}).privateLinkServiceNetworkPolicies = "Disabled"

## Save the configuration changes to the virtual network. ##

$vnet | Set-AzVirtualNetwork

```

## Create a private link service

In this section, create a private link service that uses the Standard Azure Load Balancer created in the previous step.

* Create the private link service IP configuration with [New-AzPrivateLinkServiceIpConfig](/powershell/module/az.network/new-azprivatelinkserviceipconfig).

* Create the private link service with [New-AzPrivateLinkService](/powershell/module/az.network/new-azprivatelinkservice).

```azurepowershell-interactive

## Place the virtual network into a variable. ##

$vnet = Get-AzVirtualNetwork -Name 'vnet-1' -ResourceGroupName 'test-rg'

## Create the IP configuration for the private link service. ##

$ipsettings = @{

Name = 'ipconfig-1'

PrivateIpAddress = '10.0.0.5'

Subnet = $vnet.subnets[0]

}

$ipconfig = New-AzPrivateLinkServiceIpConfig @ipsettings

## Place the load balancer frontend configuration into a variable. ##

$par = @{

Name = 'load-balancer'

ResourceGroupName = 'test-rg'

}

$fe = Get-AzLoadBalancer @par | Get-AzLoadBalancerFrontendIpConfig

## Create the private link service for the load balancer. ##

$privlinksettings = @{

Name = 'private-link-service'

ResourceGroupName = 'test-rg'

Location = 'eastus2'

LoadBalancerFrontendIpConfiguration = $fe

IpConfiguration = $ipconfig

}

New-AzPrivateLinkService @privlinksettings

```

Your private link service is created and can receive traffic. If you want to see traffic flows, configure your application behind your standard load balancer.

## Create private endpoint

In this section, you map the private link service to a private endpoint. A virtual network contains the private endpoint for the private link service. This virtual network contains the resources that access your private link service.

### Create private endpoint virtual network

* Create a virtual network with [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork).

```azurepowershell-interactive

## Create backend subnet config ##

$subnet = @{

Name = 'subnet-pe'

AddressPrefix = '10.1.0.0/24'

}

$subnetConfig = New-AzVirtualNetworkSubnetConfig @subnet

## Create the virtual network ##

$net = @{

Name = 'vnet-pe'

ResourceGroupName = 'test-rg'

Location = 'eastus2'

AddressPrefix = '10.1.0.0/16'

Subnet = $subnetConfig

}

$vnetpe = New-AzVirtualNetwork @net

```

### Create endpoint and connection

* Use [Get-AzPrivateLinkService](/powershell/module/az.network/get-azprivatelinkservice) to place the configuration of the private link service you created early into a variable for later use.

* Use [New-AzPrivateLinkServiceConnection](/powershell/module/az.network/new-azprivatelinkserviceconnection) to create the connection configuration.

* Use [New-AzPrivateEndpoint](/powershell/module/az.network/new-azprivateendpoint) to create the endpoint.

```azurepowershell-interactive

## Place the private link service configuration into variable. ##

$par1 = @{

Name = 'private-link-service'

ResourceGroupName = 'test-rg'

}

$pls = Get-AzPrivateLinkService @par1

## Create the private link configuration and place in variable. ##

$par2 = @{

Name = 'connection-1'

PrivateLinkServiceId = $pls.Id

}

$plsConnection = New-AzPrivateLinkServiceConnection @par2

## Place the virtual network into a variable. ##

$par3 = @{

Name = 'vnet-pe'

ResourceGroupName = 'test-rg'

}

$vnetpe = Get-AzVirtualNetwork @par3

## Create private endpoint ##

$par4 = @{

Name = 'private-endpoint'

ResourceGroupName = 'test-rg'

Location = 'eastus2'

Subnet = $vnetpe.subnets[0]

PrivateLinkServiceConnection = $plsConnection

}

New-AzPrivateEndpoint @par4 -ByManualRequest

```

### Approve the private endpoint connection

In this section, you approve the connection you created in the previous steps.

* Use [Approve-AzPrivateEndpointConnection](/powershell/module/az.network/approve-azprivateendpointconnection) to approve the connection.

```azurepowershell-interactive

## Place the private link service configuration into variable. ##

$par1 = @{

Name = 'private-link-service'

ResourceGroupName = 'test-rg'

}

$pls = Get-AzPrivateLinkService @par1

$par2 = @{

Name = $pls.PrivateEndpointConnections[0].Name

ServiceName = 'private-link-service'

ResourceGroupName = 'test-rg'

Description = 'Approved'

PrivateLinkResourceType = 'Microsoft.Network/privateLinkServices'

}

Approve-AzPrivateEndpointConnection @par2

```

### IP address of private endpoint

In this section, you find the IP address of the private endpoint that corresponds with the load balancer and private link service.

* Use [Get-AzPrivateEndpoint](/powershell/module/az.network/get-azprivateendpoint) to retrieve the IP address.

```azurepowershell-interactive

## Get private endpoint and the IP address and place in a variable for display. ##

$par1 = @{

Name = 'private-endpoint'

ResourceGroupName = 'test-rg'

ExpandResource = 'networkinterfaces'

}

$pe = Get-AzPrivateEndpoint @par1

## Display the IP address by expanding the variable. ##

$pe.NetworkInterfaces[0].IpConfigurations[0].PrivateIpAddress

```

```powershell

❯ $pe.NetworkInterfaces[0].IpConfigurations[0].PrivateIpAddress

10.1.0.4

```

## Clean up resources

When no longer needed, you can use the [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) command to remove the resource group, load balancer, and the remaining resources.

```azurepowershell-interactive

Remove-AzResourceGroup -Name 'test-rg'

```

## Next steps

In this quickstart, you:

* Created a virtual network and internal Azure Load Balancer.

* Created a private link service

To learn more about Azure Private endpoint, continue to:

> [!div class="nextstepaction"]

> [Quickstart: Create a Private Endpoint using Azure PowerShell](create-private-endpoint-powershell.md)


# Create Private Link Service Cli

# Quickstart: Create a Private Link service using Azure CLI

Get started creating a Private Link service that refers to your service.  Give Private Link access to your service or resource deployed behind an Azure Standard Load Balancer.  Users of your service have private access from their virtual network.

[!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment.md)]

- This quickstart requires version 2.62.0 or later of the Azure CLI. If using Azure Cloud Shell, the latest version is already installed.

## Create a resource group

An Azure resource group is a logical container into which Azure resources are deployed and managed.

Create a resource group with [az group create](/cli/azure/group#az-group-create):

* Named **test-rg**.

* In the **eastus2** location.

```azurecli-interactive

az group create \

--name test-rg \

--location eastus2

```

## Create an internal load balancer

In this section, you create a virtual network and an internal Azure Load Balancer.

### Virtual network

In this section, you create a virtual network and subnet to host the load balancer that accesses your Private Link service.

Create a virtual network using [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create):

* Named **vnet-1**.

* Address prefix of **10.0.0.0/16**.

* Subnet named **subnet-1**.

* Subnet prefix of **10.0.0.0/24**.

* In the **test-rg** resource group.

* Location of **eastus2**.

* Disable the network policy for private link service on the subnet.

```azurecli-interactive

az network vnet create \

--resource-group test-rg \

--location eastus2 \

--name vnet-1 \

--address-prefixes 10.0.0.0/16 \

--subnet-name subnet-1 \

--subnet-prefixes 10.0.0.0/24

```

### Create standard load balancer

This section details how you can create and configure the following components of the load balancer:

* A frontend IP pool that receives the incoming network traffic on the load balancer.

* A backend IP pool where the frontend pool sends the load balanced network traffic.

* A health probe that determines health of the backend VM instances.

* A load balancer rule that defines how traffic is distributed to the VMs.

### Create the load balancer resource

Create a public load balancer with [az network lb create](/cli/azure/network/lb#az-network-lb-create):

* Named **load-balancer**.

* A frontend pool named **frontend**.

* A backend pool named **backend-pool**.

* Associated with the virtual network **vnet-1**.

* Associated with the backend subnet **subnet-1**.

```azurecli-interactive

az network lb create \

--resource-group test-rg \

--name load-balancer \

--sku Standard \

--vnet-name vnet-1 \

--subnet subnet-1 \

--frontend-ip-name frontend \

--backend-pool-name backend-pool

```

### Create the health probe

A health probe checks all virtual machine instances to ensure they can send network traffic.

A virtual machine with a failed probe check is removed from the load balancer. The virtual machine is added back into the load balancer when the failure is resolved.

Create a health probe with [az network lb probe create](/cli/azure/network/lb/probe#az-network-lb-probe-create):

* Monitors the health of the virtual machines.

* Named **health-probe**.

* Protocol **TCP**.

* Monitoring **Port 80**.

```azurecli-interactive

az network lb probe create \

--resource-group test-rg \

--lb-name load-balancer \

--name health-probe \

--protocol tcp \

--port 80

```

### Create the load balancer rule

A load balancer rule defines:

* Frontend IP configuration for the incoming traffic.

* The backend IP pool to receive the traffic.

* The required source and destination port.

Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#az-network-lb-rule-create):

* Named **http-rule**

* Listening on **Port 80** in the frontend pool **frontend**.

* Sending load-balanced network traffic to the backend address pool **backend-pool** using **Port 80**.

* Using health probe **health-probe**.

* Protocol **TCP**.

* Idle timeout of **15 minutes**.

* Enable TCP reset.

```azurecli-interactive

az network lb rule create \

--resource-group test-rg \

--lb-name load-balancer \

--name http-rule \

--protocol tcp \

--frontend-port 80 \

--backend-port 80 \

--frontend-ip-name frontend \

--backend-pool-name backend-pool \

--probe-name health-probe \

--idle-timeout 15 \

--enable-tcp-reset true

```

## Disable network policy

Before a private link service can be created in the virtual network, the setting `privateLinkServiceNetworkPolicies` must be disabled.

* Disable the network policy with [az network vnet subnet update](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-update).

```azurecli-interactive

az network vnet subnet update \

--name subnet-1 \

--vnet-name vnet-1 \

--resource-group test-rg \

--private-link-service-network-policies Disabled

```

## Create a private link service

In this section, create a private link service that uses the Azure Load Balancer created in the previous step.

Create a private link service using a standard load balancer frontend IP configuration with [az network private-link-service create](/cli/azure/network/private-link-service#az-network-private-link-service-create):

* Named **private-link-service**.

* In virtual network **vnet-1**.

* Associated with standard load balancer **load-balancer** and frontend configuration **frontend**.

* In the **eastus2** location.

```azurecli-interactive

az network private-link-service create \

--resource-group test-rg \

--name private-link-service \

--vnet-name vnet-1 \

--subnet subnet-1 \

--lb-name load-balancer \

--lb-frontend-ip-configs frontend \

--location eastus2

```

Your private link service is created and can receive traffic. If you want to see traffic flows, configure your application behind your standard load balancer.

## Create private endpoint

In this section, you map the private link service to a private endpoint. A virtual network contains the private endpoint for the private link service. This virtual network contains the resources that access your private link service.

### Create private endpoint virtual network

Create a virtual network using [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create):

* Named **vnet-pe**.

* Address prefix of **10.1.0.0/16**.

* Subnet named **subnet-pe**.

* Subnet prefix of **10.1.0.0/24**.

* In the **test-rg** resource group.

* Location of **eastus2**.

```azurecli-interactive

az network vnet create \

--resource-group test-rg \

--location eastus2 \

--name vnet-pe \

--address-prefixes 10.1.0.0/16 \

--subnet-name subnet-pe \

--subnet-prefixes 10.1.0.0/24

```

### Create endpoint and connection

* Use [az network private-link-service show](/cli/azure/network/private-link-service#az-network-private-link-service-show) to get the resource ID of the private link service. The command places the resource ID into a variable for later use.

* Use [az network private-endpoint create](/cli/azure/network/private-endpoint#az-network-private-endpoint-create) to create the private endpoint in the virtual network you created previously.

* Named **private-endpoint**.

* In the **test-rg** resource group.

* Connection name **connection-1**.

* Location of **eastus2**.

* In virtual network **vnet-pe** and subnet **subnet-pe**.

```azurecli-interactive

export resourceid=$(az network private-link-service show \

--name private-link-service \

--resource-group test-rg \

--query id \

--output tsv)

az network private-endpoint create \

--connection-name connection-1 \

--name private-endpoint \

--private-connection-resource-id $resourceid \

--resource-group test-rg \

--subnet subnet-pe \

--manual-request false \

--vnet-name vnet-pe

```

## Clean up resources

When no longer needed, use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, private link service, load balancer, and all related resources.

```azurecli-interactive

az group delete \

--name test-rg

```

## Next steps

In this quickstart, you:

* Created a virtual network and internal Azure Load Balancer.

* Created a private link service

To learn more about Azure Private endpoint, continue to:

> [!div class="nextstepaction"]

> [Quickstart: Create a Private Endpoint using Azure CLI](create-private-endpoint-cli.md)


# Create Private Link Service Bicep

# Quickstart: Create a private link service using Bicep

In this quickstart, you use Bicep to create a private link service.

[!INCLUDE [About Bicep](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-bicep-introduction.md)]

## Prerequisites

You need an Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Review the Bicep file

This Bicep file creates a private link service.

The Bicep file used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/privatelink-service/).

Multiple Azure resources are defined in the Bicep file:

- [**Microsoft.Network/virtualNetworks**](/azure/templates/microsoft.network/virtualnetworks): There's one virtual network for each virtual machine.

- [**Microsoft.Network/loadBalancers**](/azure/templates/microsoft.network/loadBalancers): The load balancer that exposes the virtual machines that host the service.

- [**Microsoft.Network/networkInterfaces**](/azure/templates/microsoft.network/networkinterfaces): There are two network interfaces, one for each virtual machine.

- [**Microsoft.Compute/virtualMachines**](/azure/templates/microsoft.compute/virtualmachines): There are two virtual machines, one that hosts the service and one that tests the connection to the private endpoint.

- [**Microsoft.Compute/virtualMachines/extensions**](/azure/templates/Microsoft.Compute/virtualMachines/extensions): The extension that installs a web server.

- [**Microsoft.Network/privateLinkServices**](/azure/templates/microsoft.network/privateLinkServices): The private link service to expose the service.

- [**Microsoft.Network/publicIpAddresses**](/azure/templates/microsoft.network/publicIpAddresses): There is a public IP address for the test virtual machine.

- [**Microsoft.Network/privateendpoints**](/azure/templates/microsoft.network/privateendpoints): The private endpoint to access the service.

## Deploy the Bicep file

1. Save the Bicep file as **main.bicep** to your local computer.

1. Deploy the Bicep file using either Azure CLI or Azure PowerShell.

# [CLI](#tab/CLI)

```azurecli

az group create --name exampleRG --location eastus

az deployment group create --resource-group exampleRG --template-file main.bicep --parameters vmAdminUsername=<admin-user>

```

# [PowerShell](#tab/PowerShell)

```azurepowershell

New-AzResourceGroup -Name exampleRG -Location eastus

New-AzResourceGroupDeployment -ResourceGroupName exampleRG -TemplateFile ./main.bicep -vmAdminUsername "<admin-user>"

```

---

> [!NOTE]

> Replace **\<admin-user\>** with the username for the virtual machine. You'll also be prompted to enter **vmAdminPassword**. The password must be at least 12 characters long and have uppercase and lowercase characters, a digit, and a special character.

When the deployment finishes, you should see a message indicating the deployment succeeded.

## Review deployed resources

Use the Azure portal, Azure CLI, or Azure PowerShell to list the deployed resources in the resource group.

# [CLI](#tab/CLI)

```azurecli-interactive

az resource list --resource-group exampleRG

```

# [PowerShell](#tab/PowerShell)

```azurepowershell-interactive

Get-AzResource -ResourceGroupName exampleRG

```

---

## Validate the deployment

> [!NOTE]

> The Bicep file generates a unique name for the virtual machine myConsumerVm<b>{uniqueid}</b> resource. Substitute your generated value for **{uniqueid}**.

### Connect to a VM from the internet

Connect to the VM _myConsumerVm{uniqueid}_ from the internet as follows:

1.  In the Azure portal search bar, enter _myConsumerVm{uniqueid}_.

2.  Select **Connect**. **Connect to virtual machine** opens.

3.  Select **Download RDP File**. Azure creates a Remote Desktop Protocol (_.rdp_) file and downloads it to your computer.

4.  Open the downloaded .rdp file.

a. If prompted, select **Connect**.

b. Enter the username and password you specified when you created the VM.

> [!NOTE]

> You might need to select **More choices** > **Use a different account**, to specify the credentials you entered when you created the VM.

5.  Select **OK**.

6.  You might receive a certificate warning during the sign-in process. If you receive a certificate warning, select **Yes** or **Continue**.

7.  After the VM desktop appears, minimize it to go back to your local desktop.

### Access the http service privately from the VM

Here's how to connect to the http service from the VM by using the private endpoint.

1.  Go to the Remote Desktop of _myConsumerVm{uniqueid}_.

2.  Open a browser, and enter the private endpoint address: `http://10.0.0.5/`.

3.  The default IIS page appears.

## Clean up resources

When you no longer need the resources that you created with the private link service, delete the resource group. This removes the private link service and all the related resources.

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

For more information on the services that support a private endpoint, see:

> [!div class="nextstepaction"]

> [Private Link availability](private-link-overview.md#availability)


# Create Private Link Service Template

# Quickstart: Create a private link service using an ARM template

In this quickstart, you use an Azure Resource Manager template (ARM template) to create a private link service.

[!INCLUDE [About Azure Resource Manager](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-introduction.md)]

You can also complete this quickstart by using the [Azure portal](create-private-link-service-portal.md), [Azure PowerShell](create-private-link-service-powershell.md), or the [Azure CLI](create-private-link-service-cli.md).

If your environment meets the prerequisites and you're familiar with using ARM templates, select the **Deploy to Azure** button. The template opens in the Azure portal.

## Prerequisites

You need an Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Review the template

This template creates a private link service.

The template used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/privatelink-service/).

Multiple Azure resources are defined in the template:

- [**Microsoft.Network/virtualNetworks**](/azure/templates/microsoft.network/virtualnetworks): There's one virtual network for each virtual machine.

- [**Microsoft.Network/loadBalancers**](/azure/templates/microsoft.network/loadBalancers): The load balancer that exposes the virtual machines that host the service.

- [**Microsoft.Network/networkInterfaces**](/azure/templates/microsoft.network/networkinterfaces): There are two network interfaces, one for each virtual machine.

- [**Microsoft.Compute/virtualMachines**](/azure/templates/microsoft.compute/virtualmachines): There are two virtual machines, one that hosts the service and one that tests the connection to the private endpoint.

- [**Microsoft.Compute/virtualMachines/extensions**](/azure/templates/Microsoft.Compute/virtualMachines/extensions): The extension that installs a web server.

- [**Microsoft.Network/privateLinkServices**](/azure/templates/microsoft.network/privateLinkServices): The private link service to expose the service.

- [**Microsoft.Network/publicIpAddresses**](/azure/templates/microsoft.network/publicIpAddresses): There are two public IP addresses, one for each virtual machine.

- [**Microsoft.Network/privateendpoints**](/azure/templates/microsoft.network/privateendpoints): The private endpoint to access the service.

## Deploy the template

Here's how to deploy the ARM template to Azure:

1. To sign in to Azure and open the template, select **Deploy to Azure**. The template creates a virtual machine, standard load balancer, private link service, private endpoint, networking, and a virtual machine to validate.

2. Select or create your resource group.

3. Enter the virtual machine administrator username and password.

4. Select **Review + create**.

5. Select **Create**.

The deployment takes a few minutes to complete.

## Validate the deployment

> [!NOTE]

> The ARM template generates a unique name for the virtual machine myConsumerVm<b>{uniqueid}</b> resource. Substitute your generated value for **{uniqueid}**.

### Connect to a VM from the internet

Connect to the VM _myConsumerVm{uniqueid}_ from the internet as follows:

1.  In the portal's search bar, enter _myConsumerVm{uniqueid}_.

2.  Select **Connect**. **Connect to virtual machine** opens.

3.  Select **Download RDP File**. Azure creates a Remote Desktop Protocol (_.rdp_) file and downloads it to your computer.

4.  Open the RDP file that was downloaded to your computer.

a. If prompted, select **Connect**.

b. Enter the username and password you specified when you created the VM.

> [!NOTE]

> You might need to select **More choices** > **Use a different account**, to specify the credentials you entered when you created the VM.

5.  Select **OK**.

6.  You might receive a certificate warning during the sign-in process. If you receive a certificate warning, select **Yes** or **Continue**.

7.  After the VM desktop appears, minimize it to go back to your local desktop.

### Access the http service privately from the VM

Here's how to connect to the http service from the VM by using the private endpoint.

1.  Go to the Remote Desktop of _myConsumerVm{uniqueid}_.

2.  Open a browser, and enter the private endpoint address: `http://10.0.0.5/`.

3.  The default IIS page appears.

## Clean up resources

When you no longer need the resources that you created with the private link service, delete the resource group. This operation removes the private link service and all the related resources.

To delete the resource group, call the `Remove-AzResourceGroup` cmdlet:

```azurepowershell-interactive

Remove-AzResourceGroup -Name <your resource group name>

```

## Next steps

For more information on the services that support a private endpoint, see:

> [!div class="nextstepaction"]

> [Private Link availability](private-link-overview.md#availability)


# Configure Private Link Service Direct Connect

# Configure Private Link service Direct Connect

Customers can now connect a Private Link service to any privately routable destination IP address.

Azure Private Link service allows service providers to make their applications available to their customers privately and securely by placing them behind a standard load balancer. Private Link service Direct Connect expands on this capability and allows customers to directly connect a private link service to any privately routable destination IP address. This configuration is particularly useful for scenarios that provide private connectivity to applications that require direct IP-based routing, such as database connections or custom applications.

This article explains Private Link service Direct Connect and how to create it using Azure PowerShell, Azure CLI, or Terraform.

> [!NOTE]

> This feature is in public preview and is available in select regions. Review all considerations before enabling it for your subscription.

> [!NOTE]

> Portal support is available via a preview link that activates the feature in your portal: ([aka.ms/PortalPLSDirectConnect](https://aka.ms/PortalPLSDirectConnect)). Full portal support without use of a preview link to access the feature is pending.

## Prerequisites

- An Azure account with an active subscription.

- Azure PowerShell installed locally or use Azure Cloud Shell. For more information, see [Install Azure PowerShell](/powershell/azure/install-azure-powershell).

- Azure CLI installed locally or use Azure Cloud Shell. For more information, see [Install the Azure CLI](/cli/azure/install-azure-cli).

- For Terraform: [Install and configure Terraform](/azure/developer/terraform/quickstart-configure).

- Enable the feature flag Microsoft.Network/AllowPrivateLinkserviceUDR in your subscription. Follow the instructions to register via Azure CLI or PowerShell: [Enable Azure preview features](/azure/azure-resource-manager/management/preview-features).

- A virtual network with a subnet.

- A routable IP address to set as the destination IP address.

## What is Private Link service Direct Connect?

Private Link service (PLS) Direct Connect allows you to:

- **Route traffic directly** to a specific, privately routable destination IP address within your virtual network.

- **Bypass load balancer requirements** for scenarios that need direct IP connectivity.

- **Support custom routing scenarios** where you need precise control over traffic destination.

- **Configure expanded scenarios** such as secure access to on-premises resources, third-party SaaS, and virtual appliances.

### Common use cases

- Connect directly to databases for applications requiring static IP connections

- Support custom application scenarios that don't work with load balancer forwarding

- Enable legacy applications that need direct IP-based routing

- Scenarios requiring user-defined routing (UDR) with Private Link

- Provide on-premises connectivity

## Key requirements

- **Provide a minimum of 2 IP configurations**: For this feature, at least 2 IP configurations in multiples of 2 are required for high availability.

- **Specify a static destination IP address**: The target IP must be reachable within your virtual network.

- **Disable the privateLinkServiceNetworkPolicies property** on the subnet: This property is not needed for this feature.

## Limitations

Note these limitations when using Private Link service Direct Connect:

- **On-premises connectivity via ExpressRoute**: Routing to on-premises destinations through a peered virtual network or globally peered virtual network's ExpressRoute gateway is not supported as the PLS Direct Connect and ExpressRoute gateway must be in the same virtual network.

- **Private Endpoint as a destination is not supported**: The destination IP address cannot be a Private Endpoint.

- **Minimum 2 IP configurations required**: At least 2 IP configurations, or multiples of 2 ([limit](/azure/azure-resource-manager/management/azure-subscription-service-limits) of 8 max) are required to deploy a PLS Direct Connect.

- **Maximum of 10 PLS per subscription**: There is a hardware limitation of 10 PLS per region per subscription.

- **Bandwidth limitation**: Each PLS Direct Connect can support a bandwidth of up to 10 Gbps.

- **Static IP requirement**: The target destination IP address must be allocated statically, there is no support for dynamically allocated target IP address.

- **Cross-region limitation**: The source private endpoint, private link service, and client VM must be in the same region. This restriction is to be removed when the feature is generally available.

- **Regional availability**: This feature is available in limited regions (North Central US, East US 2, Central US, South Central US, West US, West US 2, West US 3, Asia Southeast, Australia East, Spain Central).

## Considerations

- **No migration support**: Deploying this feature requires a new Private Link service. Migration of existing private link services isn't supported.

- **Available client support**: Use PowerShell, CLI, or Terraform to deploy this new Private Link service. Portal support is available via a preview link that activates the feature in portal: ([aka.ms/PortalPLSDirectConnect](https://aka.ms/PortalPLSDirectConnect)). Full portal support without use of a preview link to configure the feature is pending.

- **IP forwarding is enabled**: If there is a policy on the subscription that disables IP forwarding, the policy must be disabled to allow proper configuration. Although the Private Link service Direct Connect network interface (NIC) may show IP forwarding set to disabled (false), the service functionally operates as if IP forwarding is enabled.

## Create a Private Link service Direct Connect

# [PowerShell](#tab/powershell)

Use this script to create a Private Link service Direct Connect using Azure PowerShell:

```powershell

# Define variables

$resourceGroupName = "rg-pls-directconnect"

$location = "westus"

$vnetName = "pls-vnet"

$subnetName = "pls-subnet"

$plsName = "pls-directconnect"

$destinationIP = "10.0.1.100"

# Create resource group

New-AzResourceGroup -Name $resourceGroupName -Location $location

# Create virtual network (corrected parameter name)

$subnet = New-AzVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.1.0/24" -privateLinkServiceNetworkPoliciesFlag "Disabled"

$vnet = New-AzVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix "10.0.0.0/16" -Subnet $subnet

# Get subnet reference

$subnet = Get-AzVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName

# Create IP configurations for Private Link service (minimum 2 or in multiples of 2 required)

$ipConfig1 = @{

Name = "ipconfig1"

PrivateIpAllocationMethod = "Dynamic"

Subnet = $subnet

Primary = $true

}

$ipConfig2 = @{

Name = "ipconfig2"

PrivateIpAllocationMethod = "Dynamic"

Subnet = $subnet

Primary = $false

}

# Create Private Link service Direct Connect

$pls = New-AzPrivateLinkservice `

-Name $plsName `

-ResourceGroupName $resourceGroupName `

-Location $location `

-IpConfiguration @($ipConfig1, $ipConfig2) `

-DestinationIPAddress $destinationIP

Write-Output "Private Link service created successfully!"

Write-Output "Private Link service ID: $($pls.Id)"

Write-Output "Destination IP Address: $destinationIP"

```

# [Azure CLI](#tab/cli)

Use this script to create a Private Link service Direct Connect using Azure CLI:

```azurecli

# Define variables

resourceGroupName="rg-pls-directconnect"

location="westus"

vnetName="pls-vnet"

subnetName="pls-subnet"

plsName="pls-directconnect "

destinationIP="10.0.1.100"

# Create resource group

az group create --name $resourceGroupName --location $location

# Create virtual network and subnet

az network vnet create \

--resource-group $resourceGroupName \

--name $vnetName \

--address-prefix 10.0.0.0/16 \

--subnet-name $subnetName \

--subnet-prefix 10.0.1.0/24

# Disable Private Link service network policies on subnet

az network vnet subnet update \

--resource-group $resourceGroupName \

--vnet-name $vnetName \

--name $subnetName \

--private-link-service-network-policies Disabled

# Create Private Link service Direct Connect

az network private-link-service create \

--resource-group $resourceGroupName \

--name $plsName \

--destination-ip-address $destinationIP \

--location $location \

--ip-configurations '[

{

"name": "ipconfig1",

"primary": true,

"private-ip-allocation-method": "Static",

"private-ip-address": "10.0.1.10",

"subnet": {

"id": "/subscriptions/<your-subscription-id>/resourceGroups/'$resourceGroupName'/providers/Microsoft.Network/virtualNetworks/'$vnetName'/subnets/'$subnetName'"

}

},

{

"name": "ipconfig2",

"primary": false,

"private-ip-allocation-method": "Static",

"private-ip-address": "10.0.1.11",

"subnet": {

"id": "/subscriptions/<your-subscription-id>/resourceGroups/'$resourceGroupName'/providers/Microsoft.Network/virtualNetworks/'$vnetName'/subnets/'$subnetName'"

}

}

]'

echo "Private Link service created successfully!"

echo "Destination IP Address: $destinationIP"

```

# [Terraform](#tab/terraform)

Use this Terraform configuration to create a Private Link service Direct Connect:

```hcl

# Configure the Azure Provider

terraform {

required_providers {

azurerm = {

source  = "hashicorp/azurerm"

version = "~>4.0"

}

random = {

source  = "hashicorp/random"

version = "~>3.1"

}

}

}

# Configure the Microsoft Azure Provider

provider "azurerm" {

features {}

}

# Create a random pet name for unique resource naming

resource "random_pet" "rg_name" {

prefix = "rg"

}

# Create Resource Group

resource "azurerm_resource_group" "rg" {

name     = random_pet.rg_name.id

location = "REGION"

}

# Create Virtual Network

resource "azurerm_virtual_network" "vnet" {

name                = "${random_pet.rg_name.id}-vnet"

location            = azurerm_resource_group.rg.location

resource_group_name = azurerm_resource_group.rg.name

address_space       = ["10.0.0.0/16"]

}

# Create subnet for Private Link service

resource "azurerm_subnet" "pls_subnet" {

name                 = "pls-subnet"

resource_group_name  = azurerm_resource_group.rg.name

virtual_network_name = azurerm_virtual_network.vnet.name

address_prefixes     = ["10.0.1.0/24"]

# Required for Private Link service Direct Connect

private_link_service_network_policies_enabled = false

}

# Create Private Link service Direct Connect

resource "azurerm_private_link_service" "pls" {

name                = "${random_pet.rg_name.id}-pls"

location            = azurerm_resource_group.rg.location

resource_group_name = azurerm_resource_group.rg.name

# Destination IP address for direct routing

destination_ip_address = "10.0.1.100"

# Minimum 2 IP configurations required for destination IP

nat_ip_configuration {

name     = "ipconfig1"

primary  = true

subnet_id = azurerm_subnet.pls_subnet.id

}

nat_ip_configuration {

name     = "ipconfig2"

primary  = false

subnet_id = azurerm_subnet.pls_subnet.id

}

}

# Output the Private Link service details

output "private_link_service_id" {

description = "ID of the Private Link service"

value       = azurerm_private_link_service.pls.id

}

output "private_link_service_alias" {

description = "Alias of the Private Link service"

value       = azurerm_private_link_service.pls.alias

}

output "destination_ip_address" {

description = "Destination IP address"

value       = azurerm_private_link_service.pls.destination_ip_address

}

output "resource_group_name" {

description = "Name of the resource group"

value       = azurerm_resource_group.rg.name

}

```

---

## Create a private endpoint to test connectivity

After creating your Private Link service Direct Connect, create a Private Endpoint to test the connectivity:

# [PowerShell](#tab/powershell-pe)

```powershell

# Variables for Private Endpoint

$peResourceGroupName = "rg-pe-test"

$peVnetName = "pe-vnet"

$peSubnetName = "pe-subnet"

$privateEndpointName = "pe-to-pls"

$privateLinkserviceId = "/subscriptions/your-subscription-id/resourceGroups/rg-pls-destinationip/providers/Microsoft.Network/privateLinkservices/pls-directconnect"

# Create resource group for PE

New-AzResourceGroup -Name $peResourceGroupName -Location $location

# Create VNet for Private Endpoint

$peSubnet = New-AzVirtualNetworkSubnetConfig -Name $peSubnetName -AddressPrefix "10.1.1.0/24" -PrivateEndpointNetworkPoliciesFlag "Disabled"

$peVnet = New-AzVirtualNetwork -Name $peVnetName -ResourceGroupName $peResourceGroupName -Location $location -AddressPrefix "10.1.0.0/16" -Subnet $peSubnet

# Get subnet reference for Private Endpoint

$peSubnet = Get-AzVirtualNetworkSubnetConfig -VirtualNetwork $peVnet -Name $peSubnetName

# Create Private Endpoint

$privateLinkserviceConnection = @{

Name = "connection-to-pls"

PrivateLinkserviceId = $privateLinkserviceId

}

$privateEndpoint = New-AzPrivateEndpoint -Name $privateEndpointName -ResourceGroupName $peResourceGroupName -Location $location -Subnet $peSubnet -PrivateLinkserviceConnection $privateLinkserviceConnection

Write-Output "Private Endpoint created: $($privateEndpoint.Name)"

```

# [Azure CLI](#tab/cli-pe)

```azurecli

# Variables for Private Endpoint

peResourceGroupName="rg-pe-test"

peVnetName="pe-vnet"

peSubnetName="pe-subnet"

privateEndpointName="pe-to-pls"

privateLinkserviceId="/subscriptions/<your-subscription-id>/resourceGroups/rg-pls-directconnect/providers/Microsoft.Network/privateLinkservices/pls-directconnect"

# Create resource group for PE

az group create --name $peResourceGroupName --location $location

# Create VNet for Private Endpoint

az network vnet create \

--resource-group $peResourceGroupName \

--name $peVnetName \

--address-prefix 10.1.0.0/16 \

--subnet-name $peSubnetName \

--subnet-prefix 10.1.1.0/24

# Disable Private Endpoint network policies

az network vnet subnet update \

--resource-group $peResourceGroupName \

--vnet-name $peVnetName \

--name $peSubnetName \

--private-link-service-network-policies Disabled

# Create Private Endpoint

az network private-endpoint create \

--resource-group $peResourceGroupName \

--name $privateEndpointName \

--vnet-name $peVnetName \

--subnet $peSubnetName \

--private-connection-resource-id $privateLinkserviceId \

--connection-name "connection-to-pls"

echo "Private Endpoint created: $privateEndpointName"

```

# [Terraform](#tab/terraform-pe)

```hcl

# Create Private Endpoint to test PLS connectivity

resource "azurerm_resource_group" "pe_rg" {

name     = "${random_pet.rg_name.id}-pe"

location = "westus"

}

resource "azurerm_virtual_network" "pe_vnet" {

name                = "${random_pet.rg_name.id}-pe-vnet"

location            = azurerm_resource_group.pe_rg.location

resource_group_name = azurerm_resource_group.pe_rg.name

address_space       = ["10.1.0.0/16"]

}

resource "azurerm_subnet" "pe_subnet" {

name                 = "pe-subnet"

resource_group_name  = azurerm_resource_group.pe_rg.name

virtual_network_name = azurerm_virtual_network.pe_vnet.name

address_prefixes     = ["10.1.1.0/24"]

private_endpoint_network_policies_enabled = false

}

resource "azurerm_private_endpoint" "pe" {

name                = "${random_pet.rg_name.id}-pe"

location            = azurerm_resource_group.pe_rg.location

resource_group_name = azurerm_resource_group.pe_rg.name

subnet_id           = azurerm_subnet.pe_subnet.id

private_service_connection {

name                           = "connection-to-pls"

private_connection_resource_id = azurerm_private_link_service.pls.id

is_manual_connection           = false

}

}

output "private_endpoint_ip" {

description = "IP address of the Private Endpoint"

value       = azurerm_private_endpoint.pe.private_service_connection[0].private_ip_address

}

```

---

## Verify the configuration

After creating both the Private Link service and Private Endpoint, verify the configuration:

### Check Private Link service status

# [PowerShell](#tab/verify-powershell)

```powershell

# Get Private Link service details

$pls = Get-AzPrivateLinkservice -Name $plsName -ResourceGroupName $resourceGroupName

Write-Output "Private Link service: $($pls.Name)"

Write-Output "Provisioning State: $($pls.ProvisioningState)"

Write-Output "Destination IP: $($pls.DestinationIPAddress)"

Write-Output "IP Configurations: $($pls.IpConfigurations.Count)"

# Check Private Endpoint connections

$connections = $pls.PrivateEndpointConnections

foreach ($connection in $connections) {

Write-Output "PE Connection: $($connection.Name) - Status: $($connection.PrivateLinkserviceConnectionState.Status)"

}

```

# [Azure CLI](#tab/verify-cli)

```azurecli

# Get Private Link service details

az network private-link-service show \

--name $plsName \

--resource-group $resourceGroupName \

--query "{name:name, provisioningState:provisioningState, destinationIpAddress:destinationIpAddress, ipConfigCount:length(ipConfigurations)}"

# Check Private Endpoint connections

az network private-link-service show \

--name $plsName \

--resource-group $resourceGroupName \

--query "privateEndpointConnections[].{name:name, status:privateLinkserviceConnectionState.status}"

```

---

## Troubleshooting

### Common issues and solutions

**Issue**: "You must include a minimum of 2 IP configurations in multiples of 2"

**Solution**: Ensure you configure at least 2 IP configurations when configuring PLS Direct Connect.

**Issue**: "Cannot reach destination IP address"

**Solution**: Verify that:

- The destination IP is reachable within the virtual network

- There's no IP forwarding or NAT between the PLS and destination IP

- Network security groups allow the required traffic

## Clean up resources

After testing, clean up the resources to avoid ongoing charges:

# [PowerShell](#tab/cleanup-powershell)

```powershell

# Remove resource groups (this deletes all resources within them)

Remove-AzResourceGroup -Name $resourceGroupName -Force

Remove-AzResourceGroup -Name $peResourceGroupName -Force

```

# [Azure CLI](#tab/cleanup-cli)

```azurecli

# Remove resource groups (this deletes all resources within them)

az group delete --name $resourceGroupName --yes --no-wait

az group delete --name $peResourceGroupName --yes --no-wait

```

# [Terraform](#tab/cleanup-terraform)

```bash

# Destroy all Terraform-managed resources

terraform destroy -auto-approve

```

---

## FAQs

The feature flag isn't visible on portal. How do I register for the feature?

- Register the feature flag Microsoft.Network/AllowPrivateLinkserviceUDR via Azure CLI or PowerShell, see this for how-to: [Set up preview features in Azure subscription - Azure Resource Manager | Microsoft Learn](/azure/azure-resource-manager/management/preview-features).

Does the property privateLinkServiceNetworkPolicies ever need to be set to True, such as by GA?

- The property privateLinkServiceNetworkPolicies is not needed for this feature, so set it to false.

Why does the Private Link service Direct Connect NIC show IP forwarding disabled?

- The NIC is displayed with IP forwarding disabled to due to platform requirements. This is expected, the Private Link service Direct Connect still performs the required forwarding behavior internally, and traffic is routed correctly.

## Next steps

- [Azure Private Link overview](/azure/private-link/private-link-overview)

- [Azure Private Link service overview](/azure/private-link/private-link-service-overview)

- [Create a private endpoint using Terraform](/azure/private-link/create-private-endpoint-terraform)

- [Troubleshoot Azure Private Link connectivity problems](/azure/private-link/troubleshoot-private-link-connectivity)


# Private Link Disable Snat

# How to Guide: Disable SNAT requirement for Azure private endpoint traffic through NVA

Source network address translation (SNAT) is no longer required for private endpoint destined traffic passing through a network virtual appliance (NVA). You can now configure a tag on your NVA virtual machines to notify the Microsoft platform that you wish to opt into this feature. This means SNATing is no longer be necessary for private endpoint destined traffic traversing through your NVA.

Enabling this feature provides a more streamlined experience for guaranteeing symmetric routing without affecting nonprivate endpoint traffic. It also allows you to follow internal compliance standards where the source of traffic origination needs to be available during logging. This feature is available in all regions.

> [!NOTE]

> Disabling SNAT for private endpoint traffic passing through a Network Virtual Appliance (NVA) causes a one-time reset of all long-running private endpoint connections established through the NVA. To minimize disruption, it's recommended to configure this feature during a maintenance window. This update will only affect traffic passing through your NVA; private endpoint traffic that bypasses the NVA won't be affected.

## Prerequisites

* An active Azure account with a subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

* A configured private endpoint in your subscription. For more information on how to create a private endpoint, see [Create a private endpoint](./create-private-endpoint-portal.md).

* A network virtual appliance (NVA) deployed in your subscription. For the example in this article, a virtual machine (VM) is used as the NVA. For more information on how to deploy a virtual machine, see [Quickstart: Create a Windows virtual machine in the Azure portal](/azure/virtual-machines/windows/quick-create-portal).

* Understanding of how to add tags to Azure resources. For more information, see [Use tags to organize your Azure resources](../azure-resource-manager/management/tag-resources.md).

### Disable SNAT requirement for Private Endpoint traffic through NVA

The type of NVA you're using determines how to disable SNAT for private endpoint traffic passing through the NVA. For the virtual machine, you add a tag on the Network interface (NIC). On the virtual machine scale set you enable the tag on the virtual machine scale set instance.

#### Add Tag to your virtual machine NIC

Here we add the tag to the virtual machine's NIC.

# [Portal](#tab/vm-nic-portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search bar at the top, search for and select **virtual machines**.

1. From the list of virtual machines, select your virtual machine.

1. In the left navigation pane under **Settings**, select **Networking**, then select **Network settings**.

1. Under the **Network Interface** section, select on the NIC name. Now you are in the Network interface pane.

1. In the left navigation pane under **Overview**, select **Tags**.

1. Add a new tag with the following details:

| Field | Value |

|-------|-------|

| Name  | `disableSnatOnPL` |

| Value | `true` |

1. Select **Apply** to save the tag.

1. Select the **Overview** section, then select **Refresh** to see the updated tags.

> [!NOTE]

> The tag is case-sensitive. Ensure you enter it exactly as shown.

# [PowerShell](#tab/vm-nic-powershell)

* Use the following PowerShell command to add the tag to your virtual machine's NIC:

```azurepowershell-interactive

$nic = Get-AzNetworkInterface -Name "myNIC" -ResourceGroupName "MyResourceGroup"

$tags = @{

"disableSnatOnPL" = "true"

}

Set-AzResource -ResourceId $nic.Id -Tag $tags -Force

```

# [Azure CLI](#tab/vm-nic-cli)

* Use the following CLI command to add the tag to your virtual machine's NIC:

```azurecli-interactive

az network nic update --name "myNIC" --resource-group "MyResourceGroup" --set tags.disableSnatOnPL=\'true\'

```

---

### Add Tag to your Virtual Machine Scale Sets

Here we add the tag to the virtual machine scale set instance.

# [Portal](#tab/vmss-portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search bar at the top, search and select **virtual machine scale sets**.

1. From the list of scale sets, select your virtual machine scale set.

1. In the left navigation pane under **Overview**, select **Tags**.

1. Add a new tag with the following details:

| Field | Value |

|-------|-------|

| Name  | `disableSnatOnPL` |

| Value | `true` |

1. Select **Apply** to save the tag.

1. Select the **Overview** section, then select **Refresh** to see the updated tags.

> [!NOTE]

> The tag is case-sensitive. Ensure you enter it exactly as shown.

# [PowerShell](#tab/vmss-powershell)

* Use the following PowerShell command to add the tag to your virtual machine scale set:

```azurepowershell-interactive

$vmss = Get-AzVmss -ResourceGroupName "MyResourceGroup" -VMScaleSetName "myVmss"

$vmss.Tags.Add("disableSnatOnPL", "true")

Update-AzVmss -ResourceGroupName "MyResourceGroup" -Name "myVmss" -VirtualMachineScaleSet $vmss

```

# [Azure CLI](#tab/vmss-cli)

* Use the following Azure CLI command to add the tag to your virtual machine scale set:

```azurecli-interactive

az vmss update --name "myVmss" --resource-group "MyResourceGroup" --set tags.disableSnatOnPL=\'true\'

```

---

#### Validate the Tag

Verify the tag is present in the virtual machine's NIC settings or virtual machine scale set settings.

1. Navigate to the **Tags** service in the Azure portal.

1. In the **Filter by** field, type `disableSnatOnPL`.

1. Select the tag from the list. Here you see all resources with the tag.

1. Select the resource to view the tag details.

To learn more, see [View resources by tag](../azure-resource-manager/management/tag-resources-portal.md#view-resources-by-tag).

## Next Step

> [!div class="nextstepaction"]

> [Create a private endpoint](./create-private-endpoint-portal.md)

> [Manage Network Polices](./disable-private-endpoint-network-policy.md)


# Increase Private Endpoint Vnet Limits

# How-to: Increase Private Endpoint virtual network limits

Today, users are [limited](/azure/azure-resource-manager/management/azure-subscription-service-limits) to deploying only 1,000 private endpoints within their virtual network. It's common for users to navigate around this limitation by implementing a [Hub and Spoke](/azure/cloud-adoption-framework/ready/azure-best-practices/hub-spoke-network-topology) model or a [Mesh network](/azure/virtual-network-manager/concept-connectivity-configuration). Doing so would make it possible to deploy extra private endpoints across peered virtual networks to temporarily surpass the per virtual network limit. However, scaling in this manner places users at risk of a silently enforced limitation. Whenever users surpass 4,000 private endpoints across their peered virtual networks, they may experience connection health degradation.

For users looking to surpass these current limits, we recommend upgrading to *High Scale Private Endpoints*. This feature increases standard limits to 5,000 private endpoints in a singular virtual network and 20,000 private endpoints across peered networks. This article details how to opt into this feature and provide extra considerations before enablement.

## Prerequisites

* An active Azure account with a subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

* Understanding of [Hub and Spoke](/azure/cloud-adoption-framework/ready/azure-best-practices/hub-spoke-network-topology) or [Mesh network](/azure/virtual-network-manager/concept-connectivity-configuration) topology.

* A virtual network with private endpoint configured, see [Create a private endpoint](/azure/private-link/create-private-endpoint-portal).

* Private Endpoint Network Policies set to **Enabled** or **RouteTableEnabled** for all Private Endpoint Subnets, see [Manage network policies for private endpoints](/azure/private-link/disable-private-endpoint-network-policy).

### Confirm if you need to upgrade

If you need more than 1,000 private endpoints in a single virtual network or encounter a max private endpoint limit error, consider upgrading to *High Scale Private Endpoints*.

For customers using a Hub and Spoke or Mesh topology, determine how many private endpoints are connected to your central virtual network containing client virtual machines. Use the provided ARG query to facilitate this process.

```Azure Resource Graph

Resources

| where subscriptionId == "\<yourSubscriptionIDHere>"

| where type =~ 'Microsoft.Network/virtualnetworks'

| project id, remoteVNetIds = properties.virtualNetworkPeerings

| mv-expand remoteVNetIds

| project id, remoteVNetId = tostring(remoteVNetIds.properties.remoteVirtualNetwork.id)

| where isnotempty(remoteVNetId)

| join kind=leftouter (

Resources

| where type =~ 'Microsoft.Network/privateEndpoints'

| project id, subnetId = tostring(properties.subnet.id)

| extend VNetId = split(subnetId ,'/subnets/')[0]

| project id, VNetId = tostring(VNetId)

| summarize Count = count() by VNetId)

on $left.remoteVNetId == $right.VNetId

| extend Count = iff(isempty(Count), 0, Count)

| summarize TotalRemotePE = sum(Count) by ['id']

| join kind=leftouter (

Resources

| where type =~ 'Microsoft.Network/privateEndpoints'

| project id, subnetId = tostring(properties.subnet.id)

| extend VNetId = split(subnetId ,'/subnets/')[0]

| project id, VNetId = tostring(VNetId)

| summarize Count = count() by VNetId)

on $left.id == $right.VNetId

| extend TotalPE = iff(isempty(Count), 0, Count) + TotalRemotePE

| project VNetId = id, TotalPE

| order by TotalPE desc

| order by ['VNetId'] asc

```

### Enable High Scale Private Endpoints

To enable this feature, configure *Private Endpoint virtual network Policies*. We recommend enabling this property for all virtual networks you want to include in this feature and for all connected compute virtual networks in peering scenarios.

> [!WARNING]

> Upgrading or downgrading this feature triggers a platform update and results in a one-time connection reset. We recommend performing this action during a maintenance window.

#### [**PowerShell**](#tab/ARG-HSP-Powershell)

```azurepowershell-interactive

$vnetName = "myVirtualNetwork"

$resourceGroupName = "myResourceGroup"

$vnet = Get-AzVirtualNetwork -ResourceGroupName $resourceGroupName -Name $vnetName

$vnet.PrivateEndpointVNetPolicies = "Basic"

$vnet | Set-AzVirtualNetwork

```

#### [**CLI**](#tab/ARG-HSP-CLI)

```azurecli-interactive

vnetName="myVirtualNetwork"

resourceGroupName="myResourceGroup"

az network vnet update --name $vnetName --resource-group $resourceGroupName --pe-vnet-policies="Basic"

```

---

### Validate configuration

To validate the configuration, verify all necessary properties are set correctly. You can do this by checking the following:

#### [**Portal**](#tab/validate-portal)

1. In the search box at the top of the portal, enter **Virtual network**. Select **Virtual networks**.

1. Select **myVNet**.

1. In settings of **myVNet**, select **Subnets**.

1. Select your subnet.

1. In the **Edit subnet** pane, under **Network Policy for Private Endpoints**, confirm **Route Table** is selected.

1. In the virtual network overview page, select **JSON view** in the top right corner.

1. In the **Resource JSON** pane, select the latest API Version.

1. Validate that the virtual network property *privateEndpointVNetPolicies* is set to **Basic**.

1. Confirm that you can deploy more than 1,000 private endpoints in the respective virtual network.

#### [**PowerShell**](#tab/validate-PowerShell)

```azurepowershell-interactive

$vnetName = "myVirtualNetwork"

$resourceGroupName = "myResourceGroup"

$vnet = Get-AzVirtualNetwork `

-ResourceGroupName $resourceGroupName `

-Name $vnetName

$vnet.PrivateEndpointVNetPolicies

```

---

### Additional Considerations

* Upgrading or downgrading this feature triggers a platform update and results in a one-time connection reset of all long-running private endpoint connections. We recommend configuring High Scale Private Endpoints during a maintenance window.

* To downgrade from this feature, reduce the total private endpoint count in your virtual network to the limit before the feature was enabled.

* Monitoring Bytes In / Out will no longer be available on all high scale private endpoints.

* On-premises private endpoint traffic is now billed as an aggregate on your gateway virtual network. Previously, it was shown on the private endpoint resource in your billing cost center. This change doesn't affect your total bill.

### Limitations

| **Limit** | **Description** |

|---|---|

| Access to Baremetal subnets from an HSPE enabled peered VNet isn't supported | Connections destined to Azure baremetal subnets won't work  |

| Feature currently available in all public regions | Mooncake and Azure Gov regions aren't supported at this time |

## Next Steps

In this article, you learned how to enable High Scale Private Endpoints and the considerations that come with it. For more information on Azure Private Link, see the following articles:

* [Private Link Availability](/azure/private-link/availability)

* [Private Link DNS Zone Values](/azure/private-link/private-endpoint-dns)

* [Manage network policies for private endpoints](/azure/private-link/disable-private-endpoint-network-policy)

* [What is a private endpoint?](/azure/private-link/private-endpoint-overview)


# Create Network Security Perimeter Portal

# Quickstart: Create a network security perimeter - Azure portal

Get started with network security perimeter by creating a network security perimeter for an Azure Key Vault using the Azure portal. A [network security perimeter](network-security-perimeter-concepts.md) allows [Azure PaaS (PaaS)](./network-security-perimeter-concepts.md#onboarded-private-link-resources)resources to communicate within an explicit trusted boundary. Next, You create and update a PaaS resources association in a network security perimeter profile. Then you create and update network security perimeter access rules. When you're finished, you delete all resources created in this quickstart.

[!INCLUDE [network-security-perimeter-preview-message](../../includes/network-security-perimeter-preview-message.md)]

## Prerequisites

Before you begin, make sure you have the following:

- An Azure account with an active subscription and access to the Azure portal. If you don't already have an Azure account, [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Sign in to the Azure portal

Sign in to the [Azure portal](https://portal.azure.com) with your Azure account.

## Create a resource group and key vault

Before creating a network security perimeter, you create a resource group to hold all resources and a key vault that's protected by a network security perimeter.

> [!NOTE]

> Azure Key Vault requires a unique name. If you receive an error that the name is already in use, try a different name. In our example, we use a unique name by appending Year (YYYY), Month (MM), and Day (DD) to the name - **key-vault-YYYYDDMM**.

1. In the search box at the top of the portal, enter **Key vaults**. Select **Key vaults** in the search results.

1. In the Key vaults accounts window that appears, select **+ Create**.

1. In the **Create a key vault** window, enter the following information:

|**Setting**| **Value** |

| --- | --- |

| Subscription | Select the subscription you want to use for this key vault. |

| Resource group | Select **Create new**, then enter **resource-group** as the name. |

| Key vault name |  Enter **key-vault-`<RandomNameInformation>`**. |

| Region | Select the region in which you want your key vault to be created. For this quickstart, **(US) West Central US** is used. |

2. Leave the remaining default settings, and select **Review + Create** > **Create**.

## Create a network security perimeter

Once you create a key vault, you can proceed to create a network security perimeter.

> [!NOTE]

> For organizational and informational safety, it's advised **not to include any personally identifiable or sensitive data** in the network security perimeter rules or other network security perimeter configuration.

1. In the search box of the Azure portal, enter **network security perimeters**. Select **network security perimeters** from the search results.

2. In the **network security perimeters** window, select **+ Create**.

3. In the **Create a network security perimeter** window, enter the following information:

| **Setting** | **Value** |

| --- | --- |

| Subscription | Select the subscription you want to use for this network security perimeter. |

| Resource group | Select **resource-group**. |

| Name | Enter **network-security-perimeter**. |

| Region | Select the region in which you want your network security perimeter to be created. For this quickstart, **(US) West Central US** is used. |

| Profile name | Enter **profile-1**. |

4. Select the **Resources** tab or **Next** to proceed to the next step.

5. In the **Resources** tab, select **+ Add**.

6. In the **Select resources** window, check **key-vault-YYYYDDMM** and choose **Select**.

7. Select **Inbound access rules** and select **+ Add**.

8. In the **Add inbound access rule** window, enter the following information, and select **Add**:

| **Settings** | **Value** |

| --- | --- |

| Rule name | Enter **inbound-rule**. |

| Source type | Select **IP address ranges**. |

| Allowed Sources | Enter a public IP address range you wish to allow inbound traffic from. |

9. Select **Outbound access rules** and select **+ Add**.

10. In the **Add outbound access rule** window, enter the following information, and select **Add**:

| **Settings** | **Value** |

| --- | --- |

| Rule name | Enter **outbound-rule**. |

| Destination type | Select **FQDN**. |

| Allowed Destinations | Enter the FQDN of the destinations you want to allow. For example, **www.contoso.com**. |

11. Select **Review + create** and then **Create**.

12. Select **Go to resource** to view the newly created network security perimeter.

[!INCLUDE [network-security-perimeter-note-managed-id](../../includes/network-security-perimeter-note-managed-id.md)]

## Delete a network security perimeter

When you no longer need a network security perimeter and associated resources, you can delete the resource group that contains the network security perimeter and all associated resources. This action removes the network security perimeter and all resources within it.

1. In the Azure portal, select **Resource groups** from the left-hand menu.

1. Select **resource-group** from the list of resource groups.

1. In the **resource-group** window, select **Delete resource group** from the action bar.

1. In the **Delete a resource group** window, enter the name of the resource group to confirm the deletion.

1. Select **Delete** to remove the resource group and all resources within it.

1. Verify the resource group is no longer listed in the **Resource groups** window.

[!INCLUDE [network-security-perimeter-delete-resources](../../includes/network-security-perimeter-delete-resources.md)]

## Next steps

> [!div class="nextstepaction"]

> [Diagnostic logging for Azure Network Security Perimeter](./network-security-perimeter-diagnostic-logs.md)


# Create Network Security Perimeter Powershell

# Quickstart: Create a network security perimeter - Azure PowerShell

Get started with network security perimeter by creating a network security perimeter for an Azure Key Vault using Azure PowerShell. A [network security perimeter](network-security-perimeter-concepts.md) allows [Azure Platform as a Service (PaaS)](./network-security-perimeter-concepts.md#onboarded-private-link-resources) resources to communicate within an explicit trusted boundary. You create and update a PaaS resource's association in a network security perimeter profile. Then you create and update network security perimeter access rules. When you're finished, you delete all resources created in this quickstart.

[!INCLUDE [network-security-perimeter-preview-message](../../includes/network-security-perimeter-preview-message.md)]

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- Install the Az.Tools.Installer module:

```azurepowershell

# Install the Az.Tools.Installer module

Install-Module -Name Az.Tools.Installer -Repository PSGallery

```

- Install the preview build of the `Az.Network`:

```azurepowershell-interactive

# Install the preview build of the Az.Network module

Install-Module -Name Az.Network -AllowPrerelease -Force -RequiredVersion 7.13.0-preview

```

- You can choose to use Azure PowerShell locally or use [Azure Cloud Shell](/azure/cloud-shell/overview).

- To get help with the PowerShell cmdlets, use the `Get-Help` command:

```azurepowershell-interactive

# Get help for a specific command

Get-Help -Name <powershell-command> - full

# Example

Get-Help -Name New-AzNetworkSecurityPerimeter - full

```

## Sign in to your Azure account and select your subscription

To begin your configuration, sign in to your Azure account:

```azurepowershell

# Sign in to your Azure account

Connect-AzAccount

```

Then, connect to your subscription:

```azurepowershell

# List all subscriptions

Set-AzContext -Subscription <subscriptionId>

# Register the Microsoft.Network resource provider

Register-AzResourceProvider -ProviderNamespace Microsoft.Network

```

## Create a resource group and key vault

Before you can create a network security perimeter, you have to create a resource group and a key vault resource.

This example creates a resource group named `test-rg` in the WestCentralUS location and a key vault named `demo-keyvault-<RandomValue>` in the resource group with the following commands:

```azurepowershell-interactive

# Create a resource group

$rgParams = @{

Name = "test-rg"

Location = "westcentralus"

}

New-AzResourceGroup @rgParams

# Create a key vault

$keyVaultName = "demo-keyvault-$(Get-Random)"

$keyVaultParams = @{

Name = $keyVaultName

ResourceGroupName = $rgParams.Name

Location = $rgParams.Location

}

$keyVault = New-AzKeyVault @keyVaultParams

```

## Create a network security perimeter

In this step, create a network security perimeter with the following `New-AzNetworkSecurityPerimeter` command:

> [!NOTE]

> Please do not put any personal identifiable or sensitive data in the network security perimeter rules or other network security perimeter configuration.

```azurepowershell-interactive

# Create a network security perimeter

$nsp = @{

Name = 'demo-nsp'

location = 'westcentralus'

ResourceGroupName = $rgParams.name

}

$demoNSP=New-AzNetworkSecurityPerimeter @nsp

$nspId = $demoNSP.Id

```

## Create and update PaaS resources’ association with a new profile

In this step, you create a new profile and associate the PaaS resource, the Azure Key Vault with the profile using the `New-AzNetworkSecurityPerimeterProfile` and `New-AzNetworkSecurityPerimeterAssociation` commands.

1. Create a new profile for your network security perimeter with the following command:

```azurepowershell-interactive

# Create a new profile

$nspProfile = @{

Name = 'nsp-profile'

ResourceGroupName = $rgParams.name

SecurityPerimeterName = $nsp.name

}

$demoProfileNSP=New-AzNetworkSecurityPerimeterProfile @nspprofile

```

2. Associate the Azure Key Vault (PaaS resource) with the network security perimeter profile with the following command:

```azurepowershell-interactive

# Associate the PaaS resource with the above created profile

$nspAssociation = @{

AssociationName = 'nsp-association'

ResourceGroupName = $rgParams.name

SecurityPerimeterName = $nsp.name

AccessMode = 'Learning'

ProfileId = $demoProfileNSP.Id

PrivateLinkResourceId = $keyVault.ResourceID

}

New-AzNetworkSecurityPerimeterAssociation @nspassociation | format-list

```

3. Update association by changing the access mode to `enforced` with the `Update-AzNetworkSecurityPerimeterAssociation` command as follows:

```azurepowershell-interactive

# Update the association to enforce the access mode

$updateAssociation = @{

AssociationName = $nspassociation.AssociationName

ResourceGroupName = $rgParams.name

SecurityPerimeterName = $nsp.name

AccessMode = 'Enforced'

}

Update-AzNetworkSecurityPerimeterAssociation @updateAssociation | format-list

```

## Manage network security perimeter access rules

In this step, you create, update and delete network security perimeter access rules with public IP address prefixes.

```azurepowershell-interactive

# Create an inbound access rule for a public IP address prefix

$inboundRule = @{

Name = 'nsp-inboundRule'

ProfileName = $nspprofile.Name

ResourceGroupName = $rgParams.Name

SecurityPerimeterName = $nsp.Name

Direction = 'Inbound'

AddressPrefix = '192.0.2.0/24'

}

New-AzNetworkSecurityPerimeterAccessRule @inboundrule | format-list

# Update the inbound access rule to add more public IP address prefixes

$updateInboundRule = @{

Name = $inboundrule.Name

ProfileName = $nspprofile.Name

ResourceGroupName = $rgParams.Name

SecurityPerimeterName = $nsp.Name

AddressPrefix = @('192.0.2.0/24','198.51.100.0/24')

}

Update-AzNetworkSecurityPerimeterAccessRule @updateInboundRule | format-list

```

[!INCLUDE [network-security-pe~rimeter-note-managed-id](../../includes/network-security-perimeter-note-managed-id.md)]

## Delete all resources

When you no longer need the network security perimeter, remove all resources associated with the network security perimeter, remove the perimeter, and then remove the resource group.

```azurepowershell-interactive

# Retrieve the network security perimeter and place it in a variable

$nsp= Get-AzNetworkSecurityPerimeter -Name demo-nsp -ResourceGroupName $rg.Params.Name

# Delete the network security perimeter and all associated resources

$removeNsp = @{

Name = 'nsp-association'

ResourceGroupName = $rgParams.Name

SecurityPerimeterName = $nsp.Name

}

Remove-AzNetworkSecurityPerimeterAssociation @removeNsp

Remove-AzNetworkSecurityPerimeter -Name $nsp.Name -ResourceGroupName $rgParams.Name

# Remove the resource group

Remove-AzResourceGroup -Name $rgParams.Name -Force

```

[!INCLUDE [network-security-perimeter-delete-resources](../../includes/network-security-perimeter-delete-resources.md)]

## Next steps

> [!div class="nextstepaction"]

> [Diagnostic logging for Azure Network Security Perimeter](./network-security-perimeter-diagnostic-logs.md)


# Create Network Security Perimeter Cli

# Quickstart: Create a network security perimeter - Azure CLI

Get started with network security perimeter by creating a network security perimeter for an Azure Key Vault using Azure CLI. A [network security perimeter](network-security-perimeter-concepts.md) allows [Azure PaaS (PaaS)](./network-security-perimeter-concepts.md#onboarded-private-link-resources)resources to communicate within an explicit trusted boundary. Next, You create and update a PaaS resources association in a network security perimeter profile. Then you create and update network security perimeter access rules. When you're finished, you delete all resources created in this quickstart.

[!INCLUDE [network-security-perimeter-preview-message](../../includes/network-security-perimeter-preview-message.md)]

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- The [latest Azure CLI](/cli/azure/install-azure-cli), or you can use Azure Cloud Shell in the portal.

- This article **requires version 2.38.0 or later** of the Azure CLI. If using Azure Cloud Shell, the latest version is already installed.

- After upgrading to the latest version of Azure CLI, import the network security perimeter commands using `az extension add --name nsp`.

## Connect to your Azure account and select your subscription

To get started, connect to [Azure Cloud Shell](https://shell.azure.com) or use your local CLI environment.

1. If using Azure Cloud Shell, sign in and select your subscription.

1. If you installed CLI locally, sign in with the following command:

```azurecli-interactive

# Sign in to your Azure account

az login

```

1. Once in your shell, select your active subscription locally with the following command:

```azurecli-interactive

# List all subscriptions

az account set --subscription <Azure Subscription>

# Re-register the Microsoft.Network resource provider

az provider register --namespace Microsoft.Network

```

## Create a resource group and key vault

Before you can create a network security perimeter, you have to create a resource group and a key vault resource with [az group create](/cli/azure/group) and [az keyvault create](/cli/azure/keyvault).

This example creates a resource group named **resource-group** in the WestCentralUS location and a key vault named **key-vault-YYYYDDMM** in the resource group with the following commands:

```azurecli-interactive

az group create \

--name resource-group \

--location westcentralus

# Create a key vault using a datetime value to ensure a unique name

key_vault_name="key-vault-$(date +%s)"

az keyvault create \

--name $key_vault_name \

--resource-group resource-group \

--location westcentralus \

--query 'id' \

--output tsv

```

## Create a network security perimeter

In this step, create a network security perimeter with the [az network perimeter create](/cli/azure/network/perimeter#az-network-perimeter-create) command.

> [!NOTE]

> Please don't put any personal identifiable or sensitive data in the network security perimeter rules or other network security perimeter configuration.

```azurecli-interactive

az network perimeter create\

--name network-security-perimeter \

--resource-group resource-group \

-l westcentralus

```

## Create and update PaaS resources’ association with a new profile

In this step, you create a new profile and associate the PaaS resource, the Azure Key Vault with the profile using the [az network perimeter profile create](/cli/azure/network/perimeter#az-network-perimeter-profile) and [az network perimeter association create](/cli/azure/network/perimeter#az-network-perimeter-association) commands.

> [!NOTE]

> For the `--private-link-resource` and `--profile` parameter values, replace `<PaaSArmId>` and `<networkSecurityPerimeterProfileId>` with the values for the key vault and the profile ID, respectively.

1. Create a new profile for your network security perimeter with the following command:

```azurecli-interactive

# Create a new profile

az network perimeter profile create \

--name network-perimeter-profile \

--resource-group resource-group \

--perimeter-name network-security-perimeter

```

2. Associate the Azure Key Vault (PaaS resource) with the network security perimeter profile with the following commands.

```azurecli-interactive

# Get key vault id

az keyvault show \

--name $key_vault_name \

--resource-group resource-group \

--query 'id'

# Get the profile id

az network perimeter profile show \

--name network-perimeter-profile \

--resource-group resource-group \

--perimeter-name network-security-perimeter

# Associate the Azure Key Vault with the network security perimeter profile

# Replace <PaaSArmId> and <networkSecurityPerimeterProfileId> with the ID values for your key vault and profile

az network perimeter association create \

--name network-perimeter-association \

--perimeter-name network-security-perimeter \

--resource-group resource-group \

--access-mode Learning  \

--private-link-resource "{id:<PaaSArmId>}" \

--profile "{id:<networkSecurityPerimeterProfileId>}"

```

1. Update association by changing the access mode to **enforced** with the [az network perimeter association create](/cli/azure/network/perimeter#az-network-perimeter-association-create) command as follows:

```azurecli-interactive

az network perimeter association create \

--name network-perimeter-association \

--perimeter-name network-security-perimeter \

--resource-group resource-group \

--access-mode Enforced  \

--private-link-resource "{id:<PaaSArmId>}" \

--profile "{id:<networkSecurityPerimeterProfileId>}"

```

## Manage network security perimeter access rules

In this step, you create, update, and delete a network security perimeter access rules with public IP address prefixes using the [az network perimeter profile access-rule create](/cli/azure/network/perimeter#az-network-perimeter-profile-access-rule-create) command.

1. Create an inbound access rule with a public IP address prefix for the profile created with the following command:

```azurecli-interactive

# Create an inbound access rule

az network perimeter profile access-rule create \

--name access-rule \

--profile-name network-perimeter-profile \

--perimeter-name network-security-perimeter \

--resource-group resource-group \

--address-prefixes "[192.0.2.0/24]"

```

1. Update your inbound access rule with another public IP address prefix with the following command:

```azurecli-interactive

# Update the inbound access rule

az network perimeter profile access-rule create\

--name access-rule \

--profile-name network-perimeter-profile \

--perimeter-name network-security-perimeter \

--resource-group resource-group \

--address-prefixes "['198.51.100.0/24', '192.0.2.0/24']"

```

1. If you need to delete an access rule, use the [az network perimeter profile access-rule delete](/cli/azure/network/perimeter#az-network-perimeter-profile-access-rule-delete) command:

```azurepowershell-interactive

# Delete the access rule

az network perimeter profile access-rule delete \

--Name network-perimeter-association \

--profile-name network-perimeter-profile \

--perimeter-name network-security-perimeter \

--resource-group resource-group

[!INCLUDE [network-security-perimeter-note-managed-id](../../includes/network-security-perimeter-note-managed-id.md)]

## Delete all resources

To delete a network security perimeter and other resources in this quickstart, use the following [az network perimeter](/cli/azure/network/perimeter) commands:

```azurecli-interactive

# Delete the network security perimeter association

az network perimeter association delete \

--name network-perimeter-association \

--resource-group resource-group \

--perimeter-name network-security-perimeter

# Delete the network security perimeter

az network perimeter delete \

--resource-group resource-group \

--name network-security-perimeter --yes

# Delete the key vault

az keyvault delete \

--name $key_vault_name \

--resource-group resource-group

# Delete the resource group

az group delete \

--name resource-group \

--yes \

--no-wait

```

[!INCLUDE [network-security-perimeter-delete-resources](../../includes/network-security-perimeter-delete-resources.md)]

## Next steps

> [!div class="nextstepaction"]

> [Diagnostic logging for Azure Network Security Perimeter](./network-security-perimeter-diagnostic-logs.md)


# Create Network Security Perimeter Bicep

# Quickstart - Create a network security perimeter - Bicep

Get started with network security perimeter by creating a network security perimeter for an Azure Key Vault using Bicep. A [network security perimeter](network-security-perimeter-concepts.md) allows [Azure Platform as a Service (PaaS)](./network-security-perimeter-concepts.md#onboarded-private-link-resources) resources to communicate within an explicit trusted boundary. You create and update a PaaS resource's association in a network security perimeter profile. Then you create and update network security perimeter access rules. When you're finished, you delete all resources created in this quickstart.

[!INCLUDE [About Bicep](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-bicep-introduction.md)]

You can also create a network security perimeter by using the [Azure portal](create-network-security-perimeter-portal.md), [Azure PowerShell](create-network-security-perimeter-powershell.md), or the [Azure CLI](create-network-security-perimeter-cli.md).

[!INCLUDE [network-security-perimeter-preview-message](../../includes/network-security-perimeter-preview-message.md)]

## Prerequisites

- An Azure account with an active subscription. If you don't already have an Azure account, [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Review the Bicep file

This Bicep file creates a network security perimeter for an instance of Azure Key Vault.

The Bicep file that this quickstart uses is from [Azure Quickstart Templates](https://github.com/azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/network-security-perimeter-create).

The Bicep file defines multiple Azure resources:

- [**Microsoft.KeyVault/vaults**](/azure/templates/microsoft.keyvault/vaults): The instance of Key Vault with the sample database.

- [**Microsoft.Network/networkSecurityPerimeters**](/azure/templates/microsoft.network/networksecurityperimeters): The network security perimeter that you use to access the instance of Key Vault.

- [**Microsoft.Network/networkSecurityPerimeters/profiles**](/azure/templates/microsoft.network/networksecurityperimeters/profiles): The network security perimeter profile that you use to access the instance of Key Vault.

- [**Microsoft.Network/networkSecurityPerimeters/profiles/accessRules**](/azure/templates/microsoft.network/networksecurityperimeters/profiles/accessrules): The access rules that you use to access the instance of Key Vault.

- [**Microsoft.Network/networkSecurityPerimeters/resourceAssociations**](/azure/templates/microsoft.network/networksecurityperimeters/resourceassociations): The resource associations that you use to access the instance of Key Vault.

## Deploy the Bicep file

1. Save the Bicep file as **main.bicep** to your local computer.

1. Deploy the Bicep file using either Azure CLI or Azure PowerShell.

# [CLI](#tab/CLI)

```azurecli

az group create --name resource-group --location eastus

az deployment group create --resource-group resource-group --template-file main.bicep --parameters

networkSecurityPerimeterName=<network-security-perimeter-name>

```

# [PowerShell](#tab/PowerShell)

```powershell

New-AzResourceGroup -Name resource-group -Location eastus

New-AzResourceGroupDeployment -ResourceGroupName resource-group -TemplateFile main.bicep

```

When the deployment finishes, you should see a message indicating the deployment succeeded.

## Validate the deployment

1. Sign into the Azure portal.

1. Enter **Network security perimeter** in the search box at the top of the portal. Select **Network security perimeters** in the search results.

1. Select the **networkPerimeter** resource from the list of network security perimeters.

1. Verify that the **networkPerimeter** resource is created successfully. The **Overview** page shows the details of the network security perimeter, including the profiles and associated resources.

## Clean up resources

When you no longer need the resources that you created with the network security perimeter service, delete the resource group. This removes the network security perimeter service and all the related resources.

# [CLI](#tab/CLI)

```azurecli-interactive

az group delete --name resource-group

```

# [PowerShell](#tab/PowerShell)

```azurepowershell-interactive

Remove-AzResourceGroup -Name resource-group

```

---

[!INCLUDE [network-security-perimeter-delete-resources](../../includes/network-security-perimeter-delete-resources.md)]

## Next steps

> [!div class="nextstepaction"]

> [Diagnostic logging for Azure Network Security Perimeter](./network-security-perimeter-diagnostic-logs.md)


# Create Network Security Perimeter Template

# Quickstart - Create a network security perimeter - ARM Template

Get started with network security perimeter by creating a network security perimeter for an Azure key vault using Azure Resource Manager (ARM) template. A [network security perimeter](network-security-perimeter-concepts.md) allows [Azure Platform as a Service (PaaS)](./network-security-perimeter-concepts.md#onboarded-private-link-resources) resources to communicate within an explicit trusted boundary. You create and update a PaaS resource's association in a network security perimeter profile. Then you create and update network security perimeter access rules. When you're finished, you delete all resources created in this quickstart.

[!INCLUDE [About Azure Resource Manager](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-introduction.md)]

You can also create a network security perimeter by using the [Azure portal](create-network-security-perimeter-portal.md), [Azure PowerShell](create-network-security-perimeter-powershell.md), or the [Azure CLI](create-network-security-perimeter-cli.md).

If your environment meets the prerequisites and you're familiar with using ARM templates, select the **Deploy to Azure** button here. The ARM template will open in the Azure portal.

## Prerequisites

- An Azure account with an active subscription. If you don't already have an Azure account, [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Review the template

This template creates a private endpoint for an instance of Azure SQL Database.

The template that this quickstart uses is from [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/network-security-perimeter-create).

The template defines multiple Azure resources:

- [**Microsoft.KeyVault/vaults**](/azure/templates/microsoft.keyvault/vaults): The instance of Key Vault with the sample database.

- [**Microsoft.Network/networkSecurityPerimeters**](/azure/templates/microsoft.network/networksecurityperimeters): The network security perimeter that you use to access the instance of Key Vault.

- [**Microsoft.Network/networkSecurityPerimeters/profiles**](/azure/templates/microsoft.network/networksecurityperimeters/profiles): The network security perimeter profile that you use to access the instance of Key Vault.

- [**Microsoft.Network/networkSecurityPerimeters/profiles/accessRules**](/azure/templates/microsoft.network/networksecurityperimeters/profiles/accessrules): The access rules that you use to access the instance of Key Vault.

- [**Microsoft.Network/networkSecurityPerimeters/resourceAssociations**](/azure/templates/microsoft.network/networksecurityperimeters/resourceassociations): The resource associations that you use to access the instance of Key Vault.

## Deploy the template

Deploy the ARM template to Azure by doing the following:

1. Sign in to Azure and open the ARM template by selecting the **Deploy to Azure** button here. The template creates the network security perimeter and an Azure Key Vault instance.

1. Select your resource group or create a new one.

1. Enter the SQL administrator sign-in name and password.

1. Enter the virtual machine administrator username and password.

1. Read the terms and conditions statement. If you agree, select **I agree to the terms and conditions stated above**, and then select **Purchase**. The deployment can take 20 minutes or longer to complete.

## Validate the deployment

### Clean up resources

When you no longer need the resources that you created with the private endpoint, delete the resource group. Doing so removes the private endpoint and all the related resources.

To delete the resource group, run the `Remove-AzResourceGroup` cmdlet:

```azurepowershell-interactive

Remove-AzResourceGroup -Name <your resource group name>

```

## Next steps

For more information about the services that support private endpoints, see:

> [!div class="nextstepaction"]

> [What is Azure Private Link?](private-link-overview.md#availability)


# Network Security Perimeter Transition

# Transition to a network security perimeter in Azure

In this article, you learn about the different access modes and how to transition to a [network security perimeter](./network-security-perimeter-concepts.md) in Azure. Access modes control resource access and logging behavior, helping you secure your Azure resources.

## Access mode configuration point on resource associations

The **access mode** configuration point is part of a resource association on the perimeter and therefore can be set by the perimeter's administrator.

The property `accessMode` can be set in a resource association to control the resource's public network access.

The possible values of `accessMode` are currently **Enforced** and **Transition**.

| **Access Mode** | **Description** |

|-------------|-------------|

| **Transition** | This is the default access mode. Evaluation in this mode uses the network security perimeter configuration as a baseline. When it doesn't find a matching rule, evaluation falls back to the resource firewall configuration which can then approve access with existing settings. |

| **Enforced** | When explicitly set, the resource obeys **only** network security perimeter access rules. |

## Prevent connectivity disruptions while adopting network security perimeter

### Enable Transition mode

To prevent undesired connectivity disruptions while adopting network security perimeter to existing PaaS resources and ensure a smooth transition to secure configurations, administrators can add PaaS resources to network security perimeter in Transition mode (formerly Learning mode). This step means that the resource is not exclusively secured by a network security perimeter. Instead, it allows network security perimeter rules to co-exist with previous resource firewall rules and will:

- Allow connections to be established in accordance with the network security perimeter configuration. Additionally, resources in this configuration fallback to honoring resource-defined firewall rules and trusted access behavior when connections aren't permitted by the network security perimeter access rules.

- When diagnostic logs are enabled, generates logs detailing whether connections were approved based on network security perimeter configuration or the resource's configuration. Administrators can then analyze those logs to identify gaps in access rules, missing perimeter memberships, and undesired connections.

### Transition to enforced mode for existing resources

To fully secure your public access exclusively using a network security perimeter, it is essential to move to enforced mode. Things to consider before moving to enforced mode are the impact on public, private, trusted, and perimeter access. When in enforced mode, the behavior of network access on associated PaaS resources across different types of PaaS resources can be summarized as follows:

- **Public access:** Public access refers to inbound or outbound requests made through public networks. PaaS resources secured by a network security perimeter have their inbound and outbound public access disabled by default, but network security perimeter access rules  can be used to selectively allow public traffic that matches them.

- **Perimeter access:** Perimeter access refers to inbound or outbound requests between the resources part of the same network security perimeter. To prevent data infiltration and exfiltration, such perimeter traffic will never cross perimeter boundaries unless explicitly approved as public traffic at both source and destination in enforced mode. Managed identity needs to be assigned on resources for perimeter access.

- **Trusted access:** Trusted service access refers to a feature few Azure services that enables access through public networks when its origin is specific Azure services that are considered trusted. Since network security perimeter provides more granular control than trusted access, Trusted access isn't supported in enforced mode.

- **Private access:** Access via Private Links isn't impacted by network security perimeter.

## Moving new resources into network security perimeter

Network security perimeter supports secure by default behavior by introducing a new property under `publicNetworkAccess` called `SecuredbyPerimeter`. When set, it locks down public access and prevents PaaS resources from being exposed to public networks.

On resource creation, if `publicNetworkAccess` is set to `SecuredByPerimeter`, the resource is created in the lockdown mode even when not associated with a perimeter. Only private link traffic will be allowed if configured. Once associated to a perimeter, network security perimeter governs the resource access behavior. The following table summarizes access behavior in various modes and public network access configuration:

|  | Profile not associated | Association access mode: Transition | Association access mode: Enforced |

|--------------------------|----------------|------------------|---------------|

| Public Network Access: **Enabled** | **Inbound:** Resource rules<br>**Outbound:** Allowed | **Inbound:** Network security perimeter + Resource rules<br>**Outbound:** Network security perimeter rules + Allowed | **Inbound:** Network security perimeter rules<br>**Outbound:** Network security perimeter rules |

| Public Network Access: **Disabled** | **Inbound:** Denied<br>**Outbound:** Allowed | **Inbound:** Network security perimeter rules<br>**Outbound:** Network security perimeter rules + Allowed | **Inbound:** Network security perimeter rules<br>**Outbound:** Network security perimeter rules |

| Public Network Access: **SecuredByPerimeter** | **Inbound:** Denied<br>**Outbound:** Denied | **Inbound:** Network security perimeter rules<br>**Outbound:** Network security perimeter rules | **Inbound:** Network security perimeter rules<br>**Outbound:** Network security perimeter rules |

### Steps to configure publicNetworkAccess and accessMode properties

Both the `publicNetworkAccess` and `accessMode` properties can be set using the Azure portal by following these steps:

1. Navigate to your network security perimeter resource in the Azure portal.

2. Select **Settings** > **Associated resources** to view the list of resources associated with the perimeter.

3. Select *...* (ellipsis) next to the resource you want to configure.

4. From the dropdown menu, select **Configure public network access**, and then select the desired access mode from the three options available: **Enabled**, **Disabled**, or **SecuredByPerimeter**.

5. To set the access mode, select **Change access mode** from the dropdown menu, and then select the desired access mode from the two options available: **Transition** or **Enforced**.

## Next steps

> [!div class="nextstepaction"]

> [Create a network security perimeter in the Azure portal](./create-network-security-perimeter-portal.md)


# Private Endpoint Export Dns

# Export DNS records for a private endpoint by using the Azure portal

A private endpoint in Azure requires DNS records for name resolution of the endpoint. The DNS record resolves the private IP address of the endpoint for the configured resource. To export the DNS records of the endpoint, use the Private Link section in the Network foundation page in the portal.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- A private endpoint configured in your subscription. For the example in this article, a private endpoint to an Azure web app is used. For more information on how to create a private endpoint for a web app, see [Quickstart: Create a private endpoint by using the Azure portal](create-private-endpoint-portal.md).

## Export endpoint DNS records

In this section, you sign in to the Azure portal and select the private endpoints page.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal, enter **Private Link**.

1. Select **Private Link** from the search results.

1. In **Network foundation**, expand **Private Link** in the left menu and select **Private endpoints**.

1. In **Private endpoints**, select the endpoint for which you want to export the DNS records. Select **Generate hostfile** to download the endpoint DNS records in a host file format. If the button isn't visible in the toolbar, select the **More commands** (**...**) button to find it.

1. The downloaded host file records look similar to this example:

```text

# Exported from the Azure portal "2026-03-30 11:26:03Z"

# Private IP    FQDN    Private Endpoint Id

10.1.0.4    mywebapp8675.scm.azurewebsites.net    #/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Network/privateEndpoints/mywebappendpoint

10.1.0.4    mywebapp8675.azurewebsites.net    #/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Network/privateEndpoints/mywebappendpoint

```

## Next steps

To learn more about Azure Private Link and DNS, see [Azure private endpoint DNS configuration](private-endpoint-dns.md).

For more information on Azure Private Link, see:

* [What is Azure Private Link?](private-link-overview.md)

* [What is Azure Private Link service?](private-link-service-overview.md)

* [Azure Private Link frequently asked questions (FAQ)](private-link-faq.yml)


# Tutorial Private Endpoint Sql Powershell

# Tutorial: Connect to an Azure SQL server using an Azure Private Endpoint using Azure PowerShell

Azure Private endpoint is the fundamental building block for Private Link in Azure. It enables Azure resources, like virtual machines (VMs), to communicate with Private Link resources privately.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a virtual network and bastion host.

> * Create a virtual machine.

> * Create an Azure SQL server and private endpoint.

> * Test connectivity to the SQL server private endpoint.

## Prerequisites

* An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

* If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 5.4.1 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell). If you're running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

## Create a resource group

An Azure resource group is a logical container into which Azure resources are deployed and managed.

Create a resource group with [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup):

```azurepowershell-interactive

New-AzResourceGroup -Name 'CreateSQLEndpointTutorial-rg' -Location 'eastus'

```

## Create a virtual network and bastion host

In this section, you create a virtual network, subnet, and bastion host.

The bastion host is used to connect securely to the virtual machine for testing the private endpoint.

Create a virtual network and bastion host with:

* [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork)

* [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress)

* [New-AzBastion](/powershell/module/az.network/new-azbastion)

```azurepowershell-interactive

## Create backend subnet config. ##

$subnetConfig = New-AzVirtualNetworkSubnetConfig -Name myBackendSubnet -AddressPrefix 10.0.0.0/24

## Create Azure Bastion subnet. ##

$bastsubnetConfig = New-AzVirtualNetworkSubnetConfig -Name AzureBastionSubnet -AddressPrefix 10.0.1.0/24

## Create the virtual network. ##

$parameters1 = @{

Name = 'MyVNet'

ResourceGroupName = 'CreateSQLEndpointTutorial-rg'

Location = 'eastus'

AddressPrefix = '10.0.0.0/16'

Subnet = $subnetConfig, $bastsubnetConfig

}

$vnet = New-AzVirtualNetwork @parameters1

## Create public IP address for bastion host. ##

$parameters2 = @{

Name = 'myBastionIP'

ResourceGroupName = 'CreateSQLEndpointTutorial-rg'

Location = 'eastus'

Sku = 'Standard'

AllocationMethod = 'Static'

}

$publicip = New-AzPublicIpAddress @parameters2

## Create bastion host ##

$parameters3 = @{

ResourceGroupName = 'CreateSQLEndpointTutorial-rg'

Name = 'myBastion'

PublicIpAddress = $publicip

VirtualNetwork = $vnet

Sku = 'Basic'

}

New-AzBastion @parameters3

```

It can take a few minutes for the Azure Bastion host to deploy.

## Create test virtual machine

In this section, you create a virtual machine that is used to test the private endpoint.

Create the virtual machine with:

* [Get-Credential](/powershell/module/microsoft.powershell.security/get-credential)

* [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface)

* [New-AzVM](/powershell/module/az.compute/new-azvm)

* [New-AzVMConfig](/powershell/module/az.compute/new-azvmconfig)

* [Set-AzVMOperatingSystem](/powershell/module/az.compute/set-azvmoperatingsystem)

* [Set-AzVMSourceImage](/powershell/module/az.compute/set-azvmsourceimage)

* [Add-AzVMNetworkInterface](/powershell/module/az.compute/add-azvmnetworkinterface)

```azurepowershell-interactive

## Set credentials for server admin and password. ##

$cred = Get-Credential

## Command to get virtual network configuration. ##

$vnet = Get-AzVirtualNetwork -Name myVNet -ResourceGroupName CreateSQLEndpointTutorial-rg

## Command to create network interface for VM ##

$parameters1 = @{

Name = 'myNicVM'

ResourceGroupName = 'CreateSQLEndpointTutorial-rg'

Location = 'eastus'

Subnet = $vnet.Subnets[0]

}

$nicVM = New-AzNetworkInterface @parameters1

## Create a virtual machine configuration.##

$parameters2 = @{

VMName = 'myVM'

VMSize = 'Standard_DS1_v2'

}

$parameters3 = @{

ComputerName = 'myVM'

Credential = $cred

}

$parameters4 = @{

PublisherName = 'MicrosoftWindowsServer'

Offer = 'WindowsServer'

Skus = '2019-Datacenter'

Version = 'latest'

}

$vmConfig =

New-AzVMConfig @parameters2 | Set-AzVMOperatingSystem -Windows @parameters3 | Set-AzVMSourceImage @parameters4 | Add-AzVMNetworkInterface -Id $nicVM.Id

## Create the virtual machine ##

New-AzVM -ResourceGroupName 'CreateSQLEndpointTutorial-rg' -Location 'eastus' -VM $vmConfig

```

[!INCLUDE [ephemeral-ip-note.md](~/reusable-content/ce-skilling/azure/includes/ephemeral-ip-note.md)]

## Create an Azure SQL server

In this section, you create a SQL server and database using:

* [New-AzSqlServer](/powershell/module/az.sql/new-azsqlserver)

* [New-AzSQlDatabase](/powershell/module/az.sql/new-azsqldatabase)

Create SQL server and database. Replace **\<sql-server-name>** with your unique server name:

```azurepowershell-interactive

## Set and administrator and password for the SQL server. ##

$cred = Get-Credential

## Create SQL server ##

$parameters1 = @{

ResourceGroupName = 'CreateSQLEndpointTutorial-rg'

ServerName = '<sql-server-name>'

SqlAdministratorCredentials = $cred

Location = 'eastus'

}

New-AzSqlServer @parameters1

## Create database. ##

$parameters2 = @{

ResourceGroupName = 'CreateSQLEndpointTutorial-rg'

ServerName = '<sql-server-name>'

DatabaseName = 'mysqldatabase'

RequestedServiceObjectiveName = 'S0'

SampleName = 'AdventureWorksLT'

}

New-AzSqlDatabase @parameters2

```

## Create private endpoint

In this section, you create the private endpoint and connection using:

* [New-AzPrivateLinkServiceConnection](/powershell/module/az.network/New-AzPrivateLinkServiceConnection)

* [New-AzPrivateEndpoint](/powershell/module/az.network/new-azprivateendpoint)

```azurepowershell-interactive

## Place SQL server into variable. Replace <sql-server-name> with your server name ##

$server = Get-AzSqlServer -ResourceGroupName CreateSQLEndpointTutorial-rg -ServerName <sql-server-name>

## Create private endpoint connection. ##

$parameters1 = @{

Name = 'myConnection'

PrivateLinkServiceId = $server.ResourceID

GroupID = 'sqlserver'

}

$privateEndpointConnection = New-AzPrivateLinkServiceConnection @parameters1

## Place virtual network into variable. ##

$vnet = Get-AzVirtualNetwork -ResourceGroupName 'CreateSQLEndpointTutorial-rg' -Name 'myVNet'

## Disable private endpoint network policy ##

$vnet.Subnets[0].PrivateEndpointNetworkPolicies = "Disabled"

$vnet | Set-AzVirtualNetwork

## Create private endpoint

$parameters2 = @{

ResourceGroupName = 'CreateSQLEndpointTutorial-rg'

Name = 'myPrivateEndpoint'

Location = 'eastus'

Subnet = $vnet.Subnets[0]

PrivateLinkServiceConnection = $privateEndpointConnection

}

New-AzPrivateEndpoint @parameters2

```

## Configure the private DNS zone

In this section you create and configure the private DNS zone using:

* [New-AzPrivateDnsZone](/powershell/module/az.privatedns/new-azprivatednszone)

* [New-AzPrivateDnsVirtualNetworkLink](/powershell/module/az.privatedns/new-azprivatednsvirtualnetworklink)

* [New-AzPrivateDnsZoneConfig](/powershell/module/az.network/new-azprivatednszoneconfig)

* [New-AzPrivateDnsZoneGroup](/powershell/module/az.network/new-azprivatednszonegroup)

```azurepowershell-interactive

## Place virtual network into variable. ##

$vnet = Get-AzVirtualNetwork -ResourceGroupName 'CreateSQLEndpointTutorial-rg' -Name 'myVNet'

## Create private dns zone. ##

$parameters1 = @{

ResourceGroupName = 'CreateSQLEndpointTutorial-rg'

Name = 'privatelink.database.windows.net'

}

$zone = New-AzPrivateDnsZone @parameters1

## Create dns network link. ##

$parameters2 = @{

ResourceGroupName = 'CreateSQLEndpointTutorial-rg'

ZoneName = 'privatelink.database.windows.net'

Name = 'myLink'

VirtualNetworkId = $vnet.Id

}

$link = New-AzPrivateDnsVirtualNetworkLink @parameters2

## Create DNS configuration ##

$parameters3 = @{

Name = 'privatelink.database.windows.net'

PrivateDnsZoneId = $zone.ResourceId

}

$config = New-AzPrivateDnsZoneConfig @parameters3

## Create DNS zone group. ##

$parameters4 = @{

ResourceGroupName = 'CreateSQLEndpointTutorial-rg'

PrivateEndpointName = 'myPrivateEndpoint'

Name = 'myZoneGroup'

PrivateDnsZoneConfig = $config

}

New-AzPrivateDnsZoneGroup @parameters4

```

## Test connectivity to private endpoint

In this section, you use the virtual machine you created in the previous step to connect to the SQL server across the private endpoint.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. Select **Resource groups** in the left-hand navigation pane.

3. Select **CreateSQLEndpointTutorial-rg**.

4. Select **myVM**.

5. On the overview page for **myVM**, select **Connect** then **Bastion**.

6. Select the blue **Use Bastion** button.

7. Enter the username and password that you entered during the virtual machine creation.

8. Open Windows PowerShell on the server after you connect.

9. Enter `nslookup <sqlserver-name>.database.windows.net`. Replace **\<sqlserver-name>** with the name of the SQL server you created in the previous steps. You receive a message similar to what is displayed below:

```powershell

Server:  UnKnown

Address:  172.63.129.16

Non-authoritative answer:

Name:    mysqlserver8675.privatelink.database.windows.net

Address:  10.0.0.5

Aliases:  mysqlserver8675.database.windows.net

```

A private IP address of **10.0.0.5** is returned for the SQL server name. This address is in the subnet of the virtual network you created previously.

10. Install [SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&view=sql-server-2017) on **myVM**.

11. Open **SQL Server Management Studio**.

12. In **Connect to server**, enter or select this information:

| Setting | Value |

| ------- | ----- |

| Server type | Select **Database Engine**.|

| Server name | Enter **\<sql-server-name>.database.windows.net** |

| Authentication | Select **SQL Server Authentication**. |

| User name | Enter the username you entered during server creation |

| Password | Enter the password you entered during server creation |

| Remember password | Select **Yes**. |

13. Select **Connect**.

14. Browse databases from the left menu.

15. (Optionally) Create or query information from **mysqldatabase**.

16. Close the bastion connection to **myVM**.

## Clean up resources

When you're done using the private endpoint, SQL server, and the VM, delete the resource group and all of the resources it contains:

1. Enter **CreateSQLEndpointTutorial-rg** in the **Search** box at the top of the portal and select **CreateSQLEndpointTutorial-rg** from the search results.

2. Select **Delete resource group**.

3. Enter **CreateSQLEndpointTutorial-rg** for **TYPE THE RESOURCE GROUP NAME** and select **Delete**.

## Next steps

In this tutorial, you created a:

* Virtual network and bastion host.

* Virtual machine.

* Azure SQL server with private endpoint.

You used the virtual machine to test connectivity securely to the SQL server across the private endpoint.

As a next step, review the **Web app with private connectivity to Azure SQL database** architecture scenario, which connects a web application outside of the virtual network to the private endpoint of a database.

> [!div class="nextstepaction"]

> [Web app with private connectivity to Azure SQL database](/azure/architecture/example-scenario/private-web-app/private-web-app)


# Tutorial Private Endpoint Sql Cli

# Tutorial: Connect to an Azure SQL server using an Azure Private Endpoint using Azure CLI

Azure Private endpoint is the fundamental building block for Private Link in Azure. It enables Azure resources, like virtual machines (VMs), to communicate with Private Link resources privately.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a virtual network and bastion host.

> * Create a virtual machine.

> * Create an Azure SQL server and private endpoint.

> * Test connectivity to the SQL server private endpoint.

## Prerequisites

* An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

* Sign in to the Azure portal and check that your subscription is active by running `az login`.

* Check your version of the Azure CLI in a terminal or command window by running `az --version`. For the latest version, see the [latest release notes](/cli/azure/release-notes-azure-cli?tabs=azure-cli).

* If you don't have the latest version, update your installation by following the [installation guide for your operating system or platform](/cli/azure/install-azure-cli).

## Create a resource group

An Azure resource group is a logical container into which Azure resources are deployed and managed.

Create a resource group with [az group create](/cli/azure/group#az-group-create):

* Named **CreateSQLEndpointTutorial-rg**.

* In the **eastus** location.

```azurecli-interactive

az group create \

--name CreateSQLEndpointTutorial-rg \

--location eastus

```

## Create a virtual network and bastion host

In this section, you create a virtual network, subnet, and bastion host.

The bastion host is used to connect securely to the virtual machine for testing the private endpoint.

Create a virtual network with [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create)

* Named **myVNet**.

* Address prefix of **10.0.0.0/16**.

* Subnet named **myBackendSubnet**.

* Subnet prefix of **10.0.0.0/24**.

* In the **CreateSQLEndpointTutorial-rg** resource group.

* Location of **eastus**.

```azurecli-interactive

az network vnet create \

--resource-group CreateSQLEndpointTutorial-rg\

--location eastus \

--name myVNet \

--address-prefixes 10.0.0.0/16 \

--subnet-name myBackendSubnet \

--subnet-prefixes 10.0.0.0/24

```

Update the subnet to disable private endpoint network policies for the private endpoint with [az network vnet subnet update](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-update):

```azurecli-interactive

az network vnet subnet update \

--name myBackendSubnet \

--resource-group CreateSQLEndpointTutorial-rg \

--vnet-name myVNet \

--private-endpoint-network-policies Disabled

```

Use [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create) to create a public ip address for the bastion host:

* Create a standard zone redundant public IP address named **myBastionIP**.

* In **CreateSQLEndpointTutorial-rg**.

```azurecli-interactive

az network public-ip create \

--resource-group CreateSQLEndpointTutorial-rg \

--name myBastionIP \

--sku Standard

```

Use [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-create) to create a bastion subnet:

* Named **AzureBastionSubnet**.

* Address prefix of **10.0.1.0/24**.

* In virtual network **myVNet**.

* In resource group **CreateSQLEndpointTutorial-rg**.

```azurecli-interactive

az network vnet subnet create \

--resource-group CreateSQLEndpointTutorial-rg \

--name AzureBastionSubnet \

--vnet-name myVNet \

--address-prefixes 10.0.1.0/24

```

Use [az network bastion create](/cli/azure/network/bastion#az-network-bastion-create) to create a bastion host:

* Named **myBastionHost**.

* In **CreateSQLEndpointTutorial-rg**.

* Associated with public IP **myBastionIP**.

* Associated with virtual network **myVNet**.

* In **eastus** location.

```azurecli-interactive

az network bastion create \

--resource-group CreateSQLEndpointTutorial-rg \

--name myBastionHost \

--public-ip-address myBastionIP \

--vnet-name myVNet \

--sku Basic \

--location eastus

```

It can take a few minutes for the Azure Bastion host to deploy.

## Create test virtual machine

In this section, you create a virtual machine that is used to test the private endpoint.

Create a VM with [az vm create](/cli/azure/vm#az-vm-create). When prompted, provide a password to be used as the credentials for the VM:

* Named **myVM**.

* In **CreateSQLEndpointTutorial-rg**.

* In network **myVNet**.

* In subnet **myBackendSubnet**.

* Server image **Win2022AzureEditionCore**.

```azurecli-interactive

az vm create \

--resource-group CreateSQLEndpointTutorial-rg \

--name myVM \

--image Win2022AzureEditionCore \

--public-ip-address "" \

--vnet-name myVNet \

--subnet myBackendSubnet \

--admin-username azureuser

```

[!INCLUDE [ephemeral-ip-note.md](~/reusable-content/ce-skilling/azure/includes/ephemeral-ip-note.md)]

## Create an Azure SQL server

In this section, you create a SQL server and database.

Use [az sql server create](/cli/azure/sql/server#az-sql-server-create) to create a SQL server:

* Replace **\<sql-server-name>** with your unique server name.

* Replace **\<your-password>** with your password.

* In **CreateSQLEndpointTutorial-rg**.

* In **eastus** region.

```azurecli-interactive

az sql server create \

--name <sql-server-name> \

--resource-group CreateSQLEndpointTutorial-rg \

--location eastus \

--admin-user sqladmin \

--admin-password <your-password>

```

Use [az sql db create](/cli/azure/sql/db#az-sql-db-create) to create a database:

* Named **myDataBase**.

* In **CreateSQLEndpointTutorial-rg**.

* Replace **\<sql-server-name>** with your unique server name.

```azurecli-interactive

az sql db create \

--resource-group CreateSQLEndpointTutorial-rg  \

--server <sql-server-name> \

--name myDataBase \

--sample-name AdventureWorksLT

```

## Create private endpoint

In this section, you create the private endpoint.

Use [az sql server list](/cli/azure/sql/server#az-sql-server-list) to place the resource ID of the SQL server into a shell variable.

Use [az network private-endpoint create](/cli/azure/network/private-endpoint#az-network-private-endpoint-create) to create the endpoint and connection:

* Named **myPrivateEndpoint**.

* In resource group **CreateSQLEndpointTutorial-rg**.

* In virtual network **myVNet**.

* In subnet **myBackendSubnet**.

* Connection named **myConnection**.

```azurecli-interactive

id=$(az sql server list \

--resource-group CreateSQLEndpointTutorial-rg \

--query '[].[id]' \

--output tsv)

az network private-endpoint create \

--name myPrivateEndpoint \

--resource-group CreateSQLEndpointTutorial-rg \

--vnet-name myVNet --subnet myBackendSubnet \

--private-connection-resource-id $id \

--group-ids sqlServer \

--connection-name myConnection

```

## Configure the private DNS zone

In this section, you'll create and configure the private DNS zone using [az network private-dns zone create](/cli/azure/network/private-dns/zone#az-network-private-dns-zone-create).

You use [az network private-dns link vnet create](/cli/azure/network/private-dns/link/vnet#az-network-private-dns-link-vnet-create) to create the virtual network link to the dns zone.

You create a dns zone group with [az network private-endpoint dns-zone-group create](/cli/azure/network/private-endpoint/dns-zone-group#az-network-private-endpoint-dns-zone-group-create).

* Zone named **privatelink.database.windows.net**

* In virtual network **myVNet**.

* In resource group **CreateSQLEndpointTutorial-rg**.

* DNS link named **myDNSLink**.

* Associated with **myPrivateEndpoint**.

* Zone group named **MyZoneGroup**.

```azurecli-interactive

az network private-dns zone create \

--resource-group CreateSQLEndpointTutorial-rg \

--name "privatelink.database.windows.net"

az network private-dns link vnet create \

--resource-group CreateSQLEndpointTutorial-rg \

--zone-name "privatelink.database.windows.net" \

--name MyDNSLink \

--virtual-network myVNet \

--registration-enabled false

az network private-endpoint dns-zone-group create \

--resource-group CreateSQLEndpointTutorial-rg \

--endpoint-name myPrivateEndpoint \

--name MyZoneGroup \

--private-dns-zone "privatelink.database.windows.net" \

--zone-name sql

```

## Test connectivity to private endpoint

In this section, you use the virtual machine you created in the previous step to connect to the SQL server across the private endpoint.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. Select **Resource groups** in the left-hand navigation pane.

3. Select **CreateSQLEndpointTutorial-rg**.

4. Select **myVM**.

5. On the overview page for **myVM**, select **Connect** then **Bastion**.

6. Select the blue **Use Bastion** button.

7. Enter the username and password that you entered during the virtual machine creation.

8. Open Windows PowerShell on the server after you connect.

9. Enter `nslookup <sqlserver-name>.database.windows.net`. Replace **\<sqlserver-name>** with the name of the SQL server you created in the previous steps. You receive a message similar to what is displayed below:

```powershell

Server:  UnKnown

Address:  172.63.129.16

Non-authoritative answer:

Name:    mysqlserver8675.privatelink.database.windows.net

Address:  10.0.0.5

Aliases:  mysqlserver8675.database.windows.net

```

A private IP address of **10.0.0.5** is returned for the SQL server name. This address is in the subnet of the virtual network you created previously.

10. Install [SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&view=sql-server-2017) on **myVM**.

11. Open **SQL Server Management Studio**.

12. In **Connect to server**, enter or select this information:

| Setting | Value |

| ------- | ----- |

| Server type | Select **Database Engine**.|

| Server name | Enter **\<sql-server-name>.database.windows.net** |

| Authentication | Select **SQL Server Authentication**. |

| User name | Enter the username you entered during server creation |

| Password | Enter the password you entered during server creation |

| Remember password | Select **Yes**. |

13. Select **Connect**.

14. Browse databases from the left menu.

15. (Optionally) Create or query information from **mysqldatabase**.

16. Close the bastion connection to **myVM**.

## Clean up resources

When you're done using the private endpoint, SQL server, and the VM, delete the resource group and all of the resources it contains:

```azurecli-interactive

az group delete \

--name CreateSQLEndpointTutorial-rg

```

## Next steps

In this tutorial, you created a:

* Virtual network and bastion host.

* Virtual machine.

* Azure SQL server with private endpoint.

You used the virtual machine to test connectivity securely to the SQL server across the private endpoint.

As a next step, review the **Web app with private connectivity to Azure SQL database** architecture scenario, which connects a web application outside of the virtual network to the private endpoint of a database.

> [!div class="nextstepaction"]

> [Web app with private connectivity to Azure SQL database](/azure/architecture/example-scenario/private-web-app/private-web-app)


# Tutorial Dns On Premises Private Resolver

# Tutorial: Create a private endpoint DNS infrastructure with Azure Private Resolver for an on-premises workload

When an Azure Private Endpoint is created, it uses Azure Private DNS Zones for name resolution by default. For on-premises workloads to access the endpoint, a forwarder to a virtual machine in Azure hosting DNS or on-premises DNS records for the private endpoint were required. Azure Private Resolver alleviates the need to deploy a VM in Azure for DNS or manage the private endpoint DNS records on an on-premises DNS server.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create an Azure Virtual Network for the cloud network and a simulated on-premises network with virtual network peering.

> * Create a Azure Web App to simulate a cloud resource.

> * Create an Azure Private Endpoint for the web app in the Azure Virtual Network.

> * Create an Azure Private Resolver in the cloud network.

> * Create an Azure Virtual Machine in the simulated on-premises network to test the DNS resolution to the web app.

> [!NOTE]

> An Azure Virtual Network with peering is used to simulate an on-premises network for the purposes of this tutorial. In a production scenario, an **Express Route** or **site to site VPN** is required to connect to the Azure Virtual Network to access the private endpoint.

>

> The simulated network is configured with the Azure Private Resolver as the virtual network's DNS server. In a production scenario, the on-premises resources will use a local DNS server for name resolution. A conditional forwarder to the Azure Private Resolver is used on the on-premises DNS server to resolve the private endpoint DNS records. For more information about the configuration of conditional forwarders for your DNS server, see your provider's documentation.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## <a name="create-a-virtual-network"></a> Sign in to Azure

Sign in to the [Azure portal](https://portal.azure.com) with your Azure account.

## Overview

A virtual network for the Azure Web App and simulated on-premises network is used for the resources in the tutorial. You create two virtual networks and peer them to simulate an Express Route or VPN connection between on-premises and Azure. An Azure Bastion host is deployed in the simulated on-premises network to connect to the test virtual machine. The test virtual machine is used to test the private endpoint connection to the web app and DNS resolution.

The following resources are used in this tutorial to simulate an on-premises and cloud network infrastructure:

| Resource | Name | Description |

|----------|------|-------------|

| Simulated on-premises virtual network | **vnet-1** | The virtual network that simulates an on-premises network. |

| Cloud virtual network | **vnet-2** | The virtual network where the Azure Web App is deployed. |

| Bastion host | **bastion** | Bastion host used to connect to the virtual machine in the simulated on-premises network. |

| Test virtual machine | **vm-1** | Virtual machine used to test the private endpoint connection to the web app and DNS resolution. |

| Virtual network peer | **vnet-1-to-vnet-2** | Virtual network peer between the simulated on-premises network and cloud virtual network. |

| Virtual network peer | **vnet-2-to-vnet-1** | Virtual network peer between the cloud virtual network and simulated on-premises network. |

## Create a resource group

A resource group is a logical container for Azure resources. This procedure creates a resource group for all resources used in this tutorial.

1. In the portal, search for and select **Resource groups**.

1. On the **Resource groups** page, select **+ Create**.

1. On the **Basics** tab, enter or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Enter **test-rg**. |

| **Resource details** |  |

| Region | Select **East US 2**. |

1. Select **Review + create**, and then select **Create**.

## Create a virtual network

The following procedure creates a virtual network with a resource subnet.

1. In the portal, search for and select **Virtual networks**.

1. On the **Virtual networks** page, select **+ Create**.

1. On the **Basics** tab of **Create virtual network**, enter, or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |  |

| Name | Enter **vnet-1**. |

| Region | Select **East US 2**. |

1. Select **Next** to proceed to the **Security** tab.

1. Select **Next** to proceed to the **IP Addresses** tab.

1. In the address space box in **Subnets**, select the **default** subnet.

1. In **Edit subnet**, enter or select the following information:

| Setting | Value |

|---|---|

| **Subnet details** |  |

| Subnet template | Leave the default **Default**. |

| Name | Enter **subnet-1**. |

| Starting address | Leave the default of **10.0.0.0**. |

| Subnet size | Leave the default of **/24 (256 addresses)**. |

1. Select **Save**.

1. Select **Review + create** at the bottom of the screen, and when validation passes, select **Create**.

## Deploy Azure Bastion

Azure Bastion uses your browser to connect to VMs in your virtual network over Secure Shell (SSH) or Remote Desktop Protocol (RDP) by using their private IP addresses. The VMs don't need public IP addresses, client software, or special configuration. For more information about Azure Bastion, see [Azure Bastion](/azure/bastion/bastion-overview).

>[!NOTE]

>[!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

1. In the search box at the top of the portal, enter **Bastion**. Select **Bastions** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab of **Create a Bastion**, enter, or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |  |

| Name | Enter **bastion**. |

| Region | Select **East US 2**. |

| Tier | Select **Developer**. |

| **Configure virtual networks** |  |

| Virtual network | Select **vnet-1**. |

1. Select **Review + create**.

1. Select **Create**.

It takes a few minutes for the Bastion host deployment to complete. The Bastion host is used later in the tutorial to connect to the "on-premises" virtual machine to test the private endpoint. You can proceed to the next steps when the virtual network is created.

## Create cloud virtual network

Repeat the previous steps to create a cloud virtual network for the Azure Web App private endpoint. Replace the values with the following values for the cloud virtual network:

>[!NOTE]

> The Azure Bastion deployment section can be skipped for the cloud virtual network. The Bastion host is only required for the simulated on-premises network.

| Setting | Value |

| ------- | ----- |

| Name | **vnet-2** |

| Location | **East US 2** |

| Address space | **10.1.0.0/16** |

| Subnet name | **subnet-1** |

| Subnet address range | **10.1.0.0/24** |

[!INCLUDE [virtual-network-create-network-peer.md](~/reusable-content/ce-skilling/azure/includes/virtual-network-create-network-peer.md)]

[!INCLUDE [create-webapp.md](../../includes/create-webapp.md)]

## Create private endpoint

An Azure private endpoint creates a network interface for a supported Azure service in your virtual network. The private endpoint enables the Azure service to be accessed from a private connection in your Azure Virtual Network or on-premises network.

You create a private endpoint for the web app you created previously.

1. In the search box at the top of the portal, enter **Private endpoint**. Select **Private endpoints** in the search results.

2. Select **+ Create**.

3. Enter or select the following information in the **Basics** tab of **Create a private endpoint**:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription |

| Resource group | Select **test-rg**. |

| **Instance details** |   |

| Name | Enter **private-endpoint**. |

| Network Interface Name | Leave the default name. |

| Region | Select **East US 2**. |

4. Select **Next: Resource**.

5. Enter or select the following information in the **Resource** tab:

| Setting | Value |

| ------- | ----- |

| Connection method | Select **Connect to an Azure resource in my directory**. |

| Subscription | Select your subscription. |

| Resource type | Select **Microsoft.Web/sites**. |

| Resource | Select your webapp. The name **webapp8675** is used for the examples in this tutorial. |

| Target subresource | Select **sites**. |

6. Select **Next: Virtual Network**.

7. Enter or select the following information in the **Virtual Network** tab:

| Setting | Value |

| ------- | ----- |

| **Networking** |  |

| Virtual network | Select **vnet-2 (test-rg)**. |

| Subnet | Select **subnet-1**. |

| Network policy for private endpoints | Leave the default of **Disabled**. |

| **Private IP configuration** | Select **Statically allocate IP address**. |

| **Name** | Enter **ipconfig-1**. |

| **Private IP** | Enter **10.1.0.10**. |

8. Select **Next: DNS**.

9. Leave the defaults in the **DNS** tab.

10. Select **Next: Tags**, then **Next: Review + create**.

11. Select **Create**.

## Create a private resolver

You create a private resolver in the virtual network where the private endpoint resides. The resolver receives DNS requests from the simulated on-premises workload. Those requests are forwarded to the Azure provided DNS. The Azure provided DNS resolves the Azure Private DNS zone for the private endpoint and return the IP address to the on-premises workload.

1. In the search box at the top of the portal, enter **DNS private resolver**. Select **DNS private resolvers** in the search results.

2. Select **+ Create**.

3. Enter or select the following information in the **Basics** tab of **Create a DNS private resolver**:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription.|

| Resource group | Select **test-rg** |

| **Instance details** |   |

| Name | Enter **private-resolver**. |

| Region | Select **(US) East US 2**. |

| **Virtual Network** |   |

| Virtual Network | Select **vnet-2**. |

4. Select **Next: Inbound Endpoints**.

5. In **Inbound Endpoints**, select **+ Add an endpoint**.

6. Enter or select the following information in **Add an inbound endpoint**:

| Setting | Value |

| ------- | ----- |

| Endpoint name | Enter **inbound-endpoint**. |

| Subnet | Select **Create new**. </br> Enter **subnet-resolver** in **Name**. </br> Leave the default **Subnet address range**. </br> Select **Create**. |

7. Select **Save**.

8. Select **Review + create**.

9. Select **Create**.

When the private resolver deployment is complete, continue to the next steps.

### Set up DNS for simulated network

The following steps set the private resolver as the primary DNS server for the simulated on-premises network **vnet-1**.

In a production environment, these steps aren't needed and are only to simulate the DNS resolution for the private endpoint. Your local DNS server has a conditional forwarder to this IP address to resolve the private endpoint DNS records from the on-premises network.

1. In the search box at the top of the portal, enter **DNS private resolver**. Select **DNS private resolvers** in the search results.

2. Select **private-resolver**.

3. Select **Inbound endpoints** in **Settings**.

4. Make note of the **IP address** of the endpoint named **inbound-endpoint**. In the example for this tutorial, the IP address is **10.1.1.4**.

5. In the search box at the top of the portal, enter **Virtual network**. Select **Virtual networks** in the search results.

6. Select **vnet-1**.

7. Select **DNS servers** in **Settings**.

8. Select **Custom** in **DNS servers**.

9. Enter the IP address you noted previously. In the example for this tutorial, the IP address is **10.1.1.4**.

10. Select **Save**.

[!INCLUDE [create-test-virtual-machine.md](~/reusable-content/ce-skilling/azure/includes/create-test-virtual-machine.md)]

## Test connectivity to private endpoint

In this section, you use the virtual machine you created in the previous step to connect to the web app across the private endpoint.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

2. Select **vm-1**.

3. On the overview page for **vm-1**, select **Connect** then **Bastion**.

4. Enter the username and password that you entered during the virtual machine creation.

5. Select **Connect** button.

6. Open Windows PowerShell on the server after you connect.

7. Enter `nslookup <webapp-name>.azurewebsites.net`. Replace **\<webapp-name>** with the name of the web app you created in the previous steps. You receive a message similar to the following output:

```output

Server:  UnKnown

Address:  168.63.129.16

Non-authoritative answer:

Name:    webapp.privatelink.azurewebsites.net

Address:  10.1.0.10

Aliases:  webapp.azurewebsites.net

```

A private IP address of **10.1.0.10** is returned for the web app name. This address is in **subnet-1** subnet of **vnet-2** virtual network you created previously.

8. Open Microsoft Edge, and enter the URL of your web app, `https://<webapp-name>.azurewebsites.net`.

9. Verify you receive the default web app page.

10. Close the connection to **vm-1**.

11. Open a web browser on your local computer and enter the URL of your web app, `https://<webapp-name>.azurewebsites.net`.

12. Verify that you receive a **403** page. This page indicates that the web app isn't accessible externally.

[!INCLUDE [portal-clean-up.md](~/reusable-content/ce-skilling/azure/includes/portal-clean-up.md)]

## Next steps

In this tutorial, you learned how to deploy a private resolver and private endpoint. You tested the connection to the private endpoint from a simulated on-premises network.

Advance to the next article to learn how to...

> [!div class="nextstepaction"]

> [Connect to an Azure SQL server using an Azure Private Endpoint](tutorial-private-endpoint-sql-portal.md)


# Secure Private Link

# Secure your Azure Private Link deployment

Azure Private Link enables you to access Azure PaaS services and Azure-hosted customer-owned or partner services over a private endpoint in your virtual network. Traffic between your virtual network and the service travels the Microsoft backbone network, eliminating exposure to the public internet.

This article provides security recommendations for Azure Private Link. Following these recommendations helps you fulfill your security obligations and improve the overall security posture of your Private Link deployments. For an overview of Azure's network security services and how they work together, see [What is Azure network security?](../networking/security/network-security.md).

[!INCLUDE [Security horizontal Zero Trust statement](~/reusable-content/ce-skilling/azure/includes/security/zero-trust-security-horizontal.md)]

## Network security

- **Map private endpoints to specific resource instances to prevent data exfiltration**: Private endpoints are mapped to a single instance of a PaaS resource rather than the entire service. This instance-level mapping prevents an attacker from accessing any other resource, even within the same service. For more information, see [What is a private endpoint?](private-endpoint-overview.md).

- **Enable network security group (NSG) support on private endpoint subnets**: By default, network policies are disabled for subnets containing private endpoints. Enable NSG support to enforce inbound and outbound traffic rules on private endpoint traffic. For more information, see [Manage network policies for private endpoints](disable-private-endpoint-network-policy.md).

- **Use application security groups (ASGs) to group private endpoints for simplified rule management**: Associate private endpoints with ASGs to apply NSG rules to groups of endpoints rather than writing individual rules per IP address. For more information, see [Configure an application security group with a private endpoint](configure-asg-private-endpoint.md).

- **Route private endpoint traffic through Azure Firewall for deep packet inspection**: Enable user-defined routes (UDRs) on private endpoint subnets and route traffic through Azure Firewall to inspect and filter traffic using FQDN-based rules. Use application rules rather than network rules to maintain flow symmetry with SNAT. For broader firewall guidance, see [Secure your Azure Firewall deployment](../firewall/secure-firewall.md). For more information, see [Use Azure Firewall to inspect traffic destined to a private endpoint](inspect-traffic-with-azure-firewall.md).

- **Configure private DNS zones correctly to prevent DNS leakage**: Create Azure private DNS zones that match the recommended zone names for each service type. Link private DNS zones to all virtual networks that need to resolve private endpoint addresses. Incorrect DNS configuration can cause traffic to route over the public internet instead of through the private endpoint. For more information, see [Azure Private Endpoint DNS integration](private-endpoint-dns-integration.md).

- **Use Azure Private DNS Resolver for hybrid name resolution**: In hub-and-spoke or hybrid topologies, deploy Azure Private DNS Resolver to securely forward DNS queries between on-premises networks and Azure. This approach avoids deploying custom DNS forwarder VMs and centralizes DNS management. For more information, see [Azure Private Endpoint DNS integration](private-endpoint-dns-integration.md).

- **Associate resources with a Network Security Perimeter (NSP) to define a trusted network boundary**: Group supported PaaS resources into a perimeter that controls public inbound and outbound access. Start in Transition mode (formerly Learning mode) to validate access patterns, then explicitly move resource associations to Enforced mode so the resources obey only NSP access rules. In Enforced mode, trusted service access isn't supported, and private endpoint traffic isn't impacted by NSP. For more information, see [Transition to a network security perimeter](network-security-perimeter-transition.md).

- **Disable public network access on target resources after deploying private endpoints**: After confirming private endpoint connectivity, disable public network access on the target PaaS resource to ensure all traffic flows over the private link. For more information, see [What is Azure Private Link?](private-link-overview.md).

- **Configure Private Link Service NAT IP subnets correctly**: When publishing your own services via Private Link Service, use NAT IP configurations from a subnet where `privateLinkServiceNetworkPolicies` is disabled. A dedicated subnet isn't required for the Private Link Service, but other resources in the subnet remain governed by their NSG rules. For more information, see [Disable network policies for Private Link service source IP](disable-private-link-service-network-policy.md).

## Identity and access management

- **Assign least-privilege RBAC roles for private endpoint management**: Use the built-in Network Contributor role for users who need to create and manage private endpoints. For more granular control, create custom roles that include only the permissions listed in the Private Link RBAC reference (covering private endpoint, subnet join, target service, and approval actions as appropriate). For more information, see [Azure RBAC permissions for Azure Private Link](rbac-permissions.md).

- **Require manual approval for private endpoint connections from external tenants**: When exposing services through Private Link Service, configure the visibility and auto-approval settings to require manual approval for connections originating outside your organization. This prevents unauthorized cross-tenant access to your resources. For more information, see [What is Azure Private Link Service?](private-link-service-overview.md).

- **Use managed identities for applications that access private-endpoint-connected resources**: Where the hosting platform supports managed identities and the target PaaS service supports Microsoft Entra authentication, configure applications running in your virtual network to authenticate with managed identities rather than shared keys or connection strings when accessing resources through private endpoints. This eliminates the need to store credentials. For more information, see [What are managed identities for Azure resources?](/entra/identity/managed-identities-azure-resources/overview).

- **Assign granular RBAC roles for Network Security Perimeter management**: Separate NSP administration from general network management by assigning specific permissions for perimeter operations, profile management, and access rule management. For more information, see [Azure RBAC permissions for Network Security Perimeter](network-security-perimeter-role-based-access-control-requirements.md).

## Data protection

- **Use private endpoints to eliminate public internet exposure for data in transit**: Private endpoints route traffic over the Microsoft backbone network using a private IP address in your virtual network. This removes the need to allow public internet access to your PaaS resources, reducing the attack surface for data interception. For more information, see [What is a private endpoint?](private-endpoint-overview.md).

- **Enforce TLS encryption on connections through private endpoints**: Private Link doesn't change the encryption behavior of the underlying service. Continue to enforce TLS 1.2 or later on all services accessed through private endpoints to protect data in transit. For more information, see [Azure encryption overview](../security/fundamentals/encryption-overview.md).

- **Restrict Private Link Service visibility to specific subscriptions**: When publishing services through Private Link Service, use the visibility property to limit which subscriptions can discover and request connections to your service. Restrict auto-approval lists to subscriptions you own. For more information, see [What is Azure Private Link Service?](private-link-service-overview.md).

## Logging and monitoring

- **Monitor traffic volume for private endpoints**: Use Azure Monitor metrics to track private endpoint `Bytes In` and `Bytes Out` so you can identify unexpected traffic changes or connectivity issues. For more information, see [Supported metrics for Microsoft.Network/privateEndpoints](/azure/azure-monitor/reference/supported-metrics/microsoft-network-privateendpoints-metrics).

- **Set alerts on Private Link Service NAT port utilization**: For provider services that use Private Link Service, create Azure Monitor alerts on the `Nat Ports Usage` metric. High NAT port usage can indicate port pressure and affect connectivity for consumers. For more information, see [Supported metrics for Microsoft.Network/privateLinkServices](/azure/azure-monitor/reference/supported-metrics/microsoft-network-privatelinkservices-metrics).

- **Enable Network Security Perimeter diagnostic logs for access auditing**: Configure NSP diagnostic logs to capture inbound and outbound access decisions, including allowed and denied traffic by perimeter rules. Use these logs to audit access patterns and identify unauthorized access attempts. For more information, see [Diagnostic logs for Network Security Perimeter](network-security-perimeter-diagnostic-logs.md).

- **Monitor private endpoint connection state changes through activity logs**: Use Azure Activity logs to track when private endpoint connections are created, approved, rejected, or removed. Set up alerts for connection state changes to detect unexpected modifications. For more information, see [Monitor Azure Private Link](monitor-private-link.md).

## Compliance and governance

- **Use Azure Policy to audit or deploy private endpoints on supported services**: Assign service-specific built-in policies, such as *Storage accounts should use private link*, *Configure Storage account to use a private link connection*, *CosmosDB accounts should use private link*, and *Configure CosmosDB accounts with private endpoints*. Apply these policies at the management group or subscription level for consistent governance. For more information, see [Azure Policy built-in policy definitions](/azure/governance/policy/samples/built-in-policies).

- **Use Azure Policy to block public network access on PaaS resources**: Complement private endpoint policies with service-specific policies that deny or modify public network access on target services. This helps ensure that a resource with a private endpoint isn't also reachable over the public internet. For more information, see [Azure Policy built-in policy definitions](/azure/governance/policy/samples/built-in-policies).

- **Govern Network Security Perimeter configurations with documented controls**: Define the required perimeters, profiles, access rules, and association access modes in your deployment templates and change-management process. Use Transition mode to observe access patterns before explicitly moving associations to Enforced mode in production. For more information, see [Transition to a network security perimeter](network-security-perimeter-transition.md).

- **Tag and track all private endpoint resources for inventory management**: Apply a consistent tagging strategy to private endpoints, private DNS zones, and Private Link Service resources. Use Azure Resource Graph queries to audit your private connectivity inventory and identify resources that lack required tags or private connectivity. For more information, see [Azure Resource Graph overview](../governance/resource-graph/overview.md).

## Backup and recovery

- **Deploy private endpoints to zone-resilient services for high availability**: Azure Private Link and private endpoints span across Azure Availability Zones and are zone resilient. To fully benefit from this, ensure the target PaaS resource is also zone resilient. A private endpoint remains available even during an availability zone failure. For more information, see [What is Azure Private Link?](private-link-overview.md).

- **Document private endpoint configurations for disaster recovery**: Maintain infrastructure-as-code templates for all private endpoint deployments, associated DNS zone records, and NSG rules. Store these templates in version control so you can redeploy your private connectivity configurations in a secondary region if needed. For more information, see [Azure Resource Manager templates overview](../azure-resource-manager/templates/overview.md).

- **Plan private endpoint DNS resolution for multi-region deployments**: In multi-region disaster recovery scenarios, document how clients should resolve service FQDNs to the correct regional private endpoint and test DNS changes as part of your service-specific failover process. The DNS integration guidance explains private zone and resolver patterns, but it doesn't replace a full disaster recovery design. For more information, see [Azure Private Endpoint DNS integration](private-endpoint-dns-integration.md).

## Next steps

- [What is Azure Private Link?](private-link-overview.md)

- [What is a private endpoint?](private-endpoint-overview.md)

- [Azure Private Endpoint private DNS zone values](private-endpoint-dns.md)

- [Network Security Perimeter concepts](network-security-perimeter-concepts.md)

- [Monitor Azure Private Link](monitor-private-link.md)

- [Azure RBAC permissions for Azure Private Link](rbac-permissions.md)

- [Azure network security best practices](../security/fundamentals/network-best-practices.md)


# Configure Asg Private Endpoint

# Configure an application security group with a private endpoint

Azure Private Link private endpoints support application security groups (ASGs) for network security. You can associate private endpoints with an existing ASG in your current infrastructure alongside virtual machines and other network resources.

## Prerequisites

- An Azure account with an active subscription. If you don't already have an Azure account, [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An Azure web app with a Premium V2 tier or higher app service plan deployed in your Azure subscription.

- For more information and an example, see [Quickstart: Create an ASP.NET Core web app in Azure](../app-service/quickstart-dotnetcore.md).

- The example web app in this article is named **myWebApp1979**. Replace the example with your web app name.

- An existing ASG in your subscription. For more information about ASGs, see [Application security groups](../virtual-network/application-security-groups.md).

- The example ASG used in this article is named **myASG**. Replace the example with your application security group.

- An existing Azure virtual network and subnet in your subscription. For more information about creating a virtual network, see [Quickstart: Create a virtual network using the Azure portal](../virtual-network/quick-create-portal.md).

- The example virtual network used in this article is named **myVNet**. Replace the example with your virtual network.

- The latest version of the Azure CLI, installed.

- Check your version of the Azure CLI in a terminal or command window by running `az --version`. For the latest version, see the most recent [release notes](/cli/azure/release-notes-azure-cli?tabs=azure-cli).

- If you don't have the latest version of the Azure CLI, update it by following the [installation guide for your operating system or platform](/cli/azure/install-azure-cli).

If you choose to install and use PowerShell locally, this article requires Azure PowerShell module version 5.4.1 or later. To find the installed version, run `Get-Module -ListAvailable Az`. If you need to upgrade, see [Install the Azure PowerShell module](/powershell/azure/install-azure-powershell). If you're running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

## Create a private endpoint with an ASG

You can associate an ASG with a private endpoint when it's created. The following procedures demonstrate how to associate an ASG with a private endpoint when it's created.

# [**Portal**](#tab/portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal, enter **Private endpoint**. Select **Private endpoints** in the search results.

1. Select **+ Create** in **Private endpoints**.

1. On the **Basics** tab of **Create a private endpoint**, enter, or select the following information:

| Value | Setting |

| ----- | ------- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select your resource group. </br> In this example, it's **myResourceGroup**. |

| **Instance details** |   |

| Name | Enter **myPrivateEndpoint**. |

| Region | Select **East US**. |

1. Select **Next: Resource** at the bottom of the page.

1. On the **Resource** tab, enter or select the following information:

| Value | Setting |

| ----- | ------- |

| Connection method | Select **Connect to an Azure resource in my directory.** |

| Subscription | Select your subscription. |

| Resource type | Select **Microsoft.Web/sites**. |

| Resource | Select **mywebapp1979**. |

| Target subresource | Select **sites**. |

1. Select **Next: Virtual Network** at the bottom of the page.

1. On the **Virtual Network** tab, enter or select the following information:

| Value | Setting |

| ----- | ------- |

| **Networking** |   |

| Virtual network | Select **myVNet**. |

| Subnet | Select your subnet. </br> In this example, it's **myVNet/myBackendSubnet(10.0.0.0/24)**. |

| Enable network policies for all private endpoints in this subnet. | Leave the default selected. |

| **Application security group** |   |

| Application security group | Select **myASG**. |

1. Select **Next: DNS** at the bottom of the page.

1. Select **Next: Tags** at the bottom of the page.

1. Select **Next: Review + create**.

1. Select **Create**.

# [**PowerShell**](#tab/powershell)

```azurepowershell-interactive

## Place the previously created webapp into a variable. ##

$webapp = Get-AzWebApp -ResourceGroupName myResourceGroup -Name myWebApp1979

## Create the private endpoint connection. ##

$pec = @{

Name = 'myConnection'

PrivateLinkServiceId = $webapp.ID

GroupID = 'sites'

}

$privateEndpointConnection = New-AzPrivateLinkServiceConnection @pec

## Place the virtual network you created previously into a variable. ##

$vnet = Get-AzVirtualNetwork -ResourceGroupName 'myResourceGroup' -Name 'myVNet'

## Place the application security group you created previously into a variable. ##

$asg = Get-AzApplicationSecurityGroup -ResourceGroupName 'myResourceGroup' -Name 'myASG'

## Create the private endpoint. ##

$pe = @{

ResourceGroupName = 'myResourceGroup'

Name = 'myPrivateEndpoint'

Location = 'eastus'

Subnet = $vnet.Subnets[0]

PrivateLinkServiceConnection = $privateEndpointConnection

ApplicationSecurityGroup = $asg

}

New-AzPrivateEndpoint @pe

```

# [**CLI**](#tab/cli)

```azurecli-interactive

id=$(az webapp list \

--resource-group myResourceGroup \

--query '[].[id]' \

--output tsv)

asgid=$(az network asg show \

--name myASG \

--resource-group myResourceGroup \

--query id \

--output tsv)

az network private-endpoint create \

--connection-name myConnection \

--name myPrivateEndpoint \

--private-connection-resource-id $id \

--resource-group myResourceGroup \

--subnet myBackendSubnet \

--asg id=$asgid \

--group-id sites \

--vnet-name myVNet

```

---

## Associate an ASG with an existing private endpoint

You can associate an ASG with an existing private endpoint. The following procedures demonstrate how to associate an ASG with an existing private endpoint.

> [!IMPORTANT]

> You must have a previously deployed private endpoint to proceed with the steps in this section. The example endpoint used in this section is named **myPrivateEndpoint**. Replace the example with your private endpoint.

# [**Portal**](#tab/portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal, enter **Private endpoint**. Select **Private endpoints** in the search results.

1. In **Private endpoints**, select **myPrivateEndpoint**.

1. In **myPrivateEndpoint**, in **Settings**, select **Application security groups**.

1. In **Application security groups**, select **myASG** in the dropdown box.

1. Select **Save**.

# [**PowerShell**](#tab/powershell)

Associating an ASG with an existing private endpoint with Azure PowerShell is currently unsupported.

# [**CLI**](#tab/cli)

```azurecli-interactive

asgid=$(az network asg show \

--name myASG \

--resource-group myResourceGroup \

--query id \

--output tsv)

az network private-endpoint asg add \

--resource-group myResourceGroup \

--endpoint-name myPrivateEndpoint \

--asg-id $asgid

```

---

## Next steps

For more information about Azure Private Link, see:

- [What is Azure Private Link?](private-link-overview.md)


# Rbac Permissions

# Azure RBAC permissions for Azure Private Link

Access management for cloud resources is a critical function for any organization. Azure role-based access control (Azure RBAC) manages access and operations of Azure resources.

To deploy a private endpoint or private link service a user must have assigned a built-in role such as:

* [Owner](../role-based-access-control/built-in-roles.md?toc=%2fazure%2fprivate-link%2ftoc.json#owner)

* [Contributor](../role-based-access-control/built-in-roles.md?toc=%2fazure%2fprivate-link%2ftoc.json#contributor)

* [Network contributor](../role-based-access-control/built-in-roles.md?toc=%2fazure%2fprivate-link%2ftoc.json#network-contributor)

You can provide more granular access by creating a [custom role](../role-based-access-control/custom-roles.md?toc=%2fazure%2fprivate-link%2ftoc.json) with the permissions described in the following sections.

> [!IMPORTANT]

> This article lists the specific permissions to create a private endpoint or private link service. Ensure you add the specific permissions related to the service you would like to grant access through private link, such as Microsoft.SQL Contributor Role for Azure SQL. For more information about built-in roles, see [Role Based Access Control](../role-based-access-control/built-in-roles.md).

Microsoft.Network and the specific resource provider you are deploying, for example Microsoft.Sql, must be registered at the subscription level:

![image](https://user-images.githubusercontent.com/20302679/129105527-b946eee9-038a-46ef-b446-be371eb23ca9.png)

## Private endpoint

This section lists the granular permissions required to deploy a private endpoint, manage [private endpoint subnet policies](../private-link/disable-private-endpoint-network-policy.md), and deploy dependent resources

| Action                                                              | Description                                                                      |

| ---------                                                           | -------------                                                                 |

| Microsoft.Resources/deployments/*                                   | Create and manage a deployment                                                |

| Microsoft.Resources/subscriptions/resourcegroups/resources/read     | Read the resources for the resource group                                     |

| Microsoft.Network/virtualNetworks/read                              | Read the virtual network definition                                            |

| Microsoft.Network/virtualNetworks/subnets/read                      | Read a virtual network subnet definition                                      |

| Microsoft.Network/virtualNetworks/subnets/write                     | Creates a virtual network subnet or updates an existing virtual network subnet. <br/> *Not explicitly needed to deploy a private endpoint, but necessary for managing private endpoint subnet policies* |

| Microsoft.Network/virtualNetworks/subnets/join/action               | Allow a private endpoint to join a virtual network                              |

| Microsoft.Network/privateEndpoints/read                             | Read a private endpoint resource                                             |

| Microsoft.Network/privateEndpoints/write                            | Creates a new private endpoint, or updates an existing private endpoint       |

| Microsoft.Network/locations/availablePrivateEndpointTypes/read      | Read available private endpoint resources                                     |

Here is the JSON format of the above permissions. Input your own roleName, description, and assignableScopes:

```JSON

{

"properties": {

"roleName": "Role Name",

"description": "Description",

"assignableScopes": [

"/subscriptions/SubscriptionID/resourceGroups/ResourceGroupName"

],

"permissions": [

{

"actions": [

"Microsoft.Resources/deployments/*",

"Microsoft.Resources/subscriptions/resourceGroups/read",

"Microsoft.Network/virtualNetworks/read",

"Microsoft.Network/virtualNetworks/subnets/read",

"Microsoft.Network/virtualNetworks/subnets/write",

"Microsoft.Network/virtualNetworks/subnets/join/action",

"Microsoft.Network/privateEndpoints/read",

"Microsoft.Network/privateEndpoints/write",

"Microsoft.Network/locations/availablePrivateEndpointTypes/read"

],

"notActions": [],

"dataActions": [],

"notDataActions": []

}

]

}

}

```

## Private link service

This section lists the granular permissions required to deploy a private link service, manage [private link service subnet policies](../private-link/disable-private-link-service-network-policy.md), and deploy dependent resources

| Action | Description   |

| --------- | ------------- |

| Microsoft.Resources/deployments/*                                   | Create and manage a deployment                                                |

| Microsoft.Resources/subscriptions/resourcegroups/resources/read     | Read the resources for the resource group                                     |

| Microsoft.Network/virtualNetworks/read                              | Read the virtual network definition                                            |

| Microsoft.Network/virtualNetworks/subnets/read                      | Read a virtual network subnet definition                                      |

| Microsoft.Network/virtualNetworks/subnets/write                     | Creates a virtual network subnet or updates an existing virtual network subnet. <br/> *Not explicitly needed to deploy a private link service, but necessary for managing private link subnet policies* |

| Microsoft.Network/privateLinkServices/read                          | Read a private link service resource|

| Microsoft.Network/privateLinkServices/write                         | Creates a new private link service, or updates an existing private link service|

| Microsoft.Network/privateLinkServices/privateEndpointConnections/read | Read a private endpoint connection definition |

| Microsoft.Network/privateLinkServices/privateEndpointConnections/write | Creates a new private endpoint connection, or updates an existing private endpoint connection|

| Microsoft.Network/networkSecurityGroups/join/action                 | Joins a network security group |

| Microsoft.Network/loadBalancers/read                                | Read a load balancer definition |

| Microsoft.Network/loadBalancers/write                               | Creates a load balancer or updates an existing load balancer |

```JSON

{

"properties": {

"roleName": "Role Name",

"description": "Description",

"assignableScopes": [

"/subscriptions/SubscriptionID/resourceGroups/ResourceGroupName"

],

"permissions": [

{

"actions": [

"Microsoft.Resources/deployments/*",

"Microsoft.Resources/subscriptions/resourceGroups/read",

"Microsoft.Network/virtualNetworks/read",

"Microsoft.Network/virtualNetworks/subnets/read",

"Microsoft.Network/virtualNetworks/subnets/write",

"Microsoft.Network/virtualNetworks/subnets/join/action",

"Microsoft.Network/privateLinkServices/read",

"Microsoft.Network/privateLinkServices/write",

"Microsoft.Network/privateLinkServices/privateEndpointConnections/read",

"Microsoft.Network/privateLinkServices/privateEndpointConnections/write",

"Microsoft.Network/networkSecurityGroups/join/action",

"Microsoft.Network/loadBalancers/read",

"Microsoft.Network/loadBalancers/write"

],

"notActions": [],

"dataActions": [],

"notDataActions": []

}

]

}

}

```

## Approval RBAC for private endpoint

Typically, a network administrator creates a private endpoint. Depending on your Azure role-based access control (RBAC) permissions, a private endpoint that you create is either *automatically approved* to send traffic to the API Management instance, or requires the resource owner to *manually approve* the connection.

|Approval method     |Minimum RBAC permissions  |

|---------|---------|

|Automatic     | `Microsoft.Network/virtualNetworks/**`<br/>`Microsoft.Network/virtualNetworks/subnets/**`<br/>`Microsoft.Network/privateEndpoints/**`<br/>`Microsoft.Network/networkinterfaces/**`<br/>`Microsoft.Network/locations/availablePrivateEndpointTypes/read`<br/>`Microsoft.[ServiceProvider]/[resourceType]/privateEndpointConnectionsApproval/action`<br/>|

|Manual     | `"Microsoft.[ServiceProvider]/[resourceType]/privateEndpointConnections/read"`<br/>`"Microsoft.[ServiceProvider]/[resourceType]/privateEndpointConnections/write"`<br/>|

## Next steps

For more information on private endpoint and private link services in Azure Private link, see:

- [What is Azure Private Endpoint?](private-endpoint-overview.md)

- [What is Azure Private Link service?](private-link-service-overview.md)


# Network Security Perimeter Role Based Access Control Requirements

# Azure role-based access control permissions required for Azure Network Security Perimeter usage

In this article, you learn about the Azure role-based access control (RBAC) permissions required to use [network security perimeter](./network-security-perimeter-concepts.md) capabilities. You learn about the actions required for network security perimeter, profile, network security perimeter access rule, diagnostic settings, association, and appendix capabilities.

## Azure role-based access control permissions

[Azure role-based access control (Azure RBAC)](../role-based-access-control/overview.md) enables you to assign only the specific actions to members of your organization that they require to complete their assigned responsibilities. To use network security perimeter  capabilities, the account you log into Azure with, must be assigned to the [Owner, Contributor, or Network contributor built-in roles](../role-based-access-control/built-in-roles.md), or assigned to a [custom role](../role-based-access-control/custom-roles.md) that is assigned the actions listed for each network security perimeter  capability in the sections that follow. To learn how to check roles assigned to a user for a subscription, see [List Azure role assignments using the Azure portal](/azure/role-based-access-control/role-assignments-list-portal). If you can't see the role assignments, contact the respective subscription admin.

### Network security perimeter permissions

| Action | Description |

| --- | --- |

| Microsoft.Network/networkSecurityPerimeters/read | Gets a network security perimeter  |

| Microsoft.Network/networkSecurityPerimeters/write | Creates or updates a network security perimeter  |

| Microsoft.Network/networkSecurityPerimeters/delete | Deletes a network security perimeter  |

| Microsoft.Network/locations/perimeterAssociableResourceTypes/read | Gets network security perimeter associable resources |

### Network security perimeter profile permissions

| Action | Description |

| --- | --- |

| Microsoft.Network/networkSecurityPerimeters/profiles/read | Gets a network security perimeter profile |

| Microsoft.Network/networkSecurityPerimeters/profiles/write | Creates or updates a network security perimeter profile |

| Microsoft.Network/networkSecurityPerimeters/profiles/delete | Deletes a network security perimeter profile |

### Network security perimeter access rule permissions

| Action | Description |

| --- | --- |

| Microsoft.Network/networkSecurityPerimeters/profiles/accessRules/read | Gets a network security perimeter access rule. |

| Microsoft.Network/networkSecurityPerimeters/profiles/accessRules/write | Creates or updates a network security perimeter access rule. |

| Microsoft.Network/networkSecurityPerimeters/profiles/accessRules/delete | Deletes a network security perimeter access rule. |

| Microsoft.Resources/subscriptions/joinPerimeterRule/action | User must have *microsoft.resources/subscriptions/joinperimeterrule/action* role over the subscription |

> [!NOTE]

> User must have *subscription contributor* role to create/update subscription-based access rule.

### Network security perimeter association permissions

| **Action** | **Description** |

| --- | --- |

| Microsoft.Network/networkSecurityPerimeters/resourceAssociations/read | Gets a network security perimeter resource association |

| Microsoft.Network/networkSecurityPerimeters/resourceAssociations/write | Creates or updates a network security perimeter resource association |

| Microsoft.Network/networkSecurityPerimeters/profiles/join/action | Joins a network security perimeter profile. Linked access check is performed while associating the resource |

| Microsoft.Network/networkSecurityPerimeters/resourceAssociations/delete | Deletes a network security perimeter resource association |

> [!NOTE]

> To create or update an association, the following permissions are required to exist:

>

> - *Microsoft.Network/networkSecurityPerimeters/resourceAssociations/write* is required at the network security perimeter resource.

> - *Microsoft.Network/networkSecurityPerimeters/profiles/join/action* is required on the profile.

> - *{providerNamespace}/{resourceType}/joinPerimeter/action* is required on the respective PaaS resource.

## Next steps

> [!div class="nextstepaction"]

> [Create a network security perimeter in the Azure portal](./create-network-security-perimeter-portal.md)


# Monitor Private Link

# Monitor Azure Private Link

[!INCLUDE [azmon-horz-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-intro.md)]

## Collect data with Azure Monitor

This table describes how you can collect data to monitor your service, and what you can do with the data once collected:

|Data to collect|Description|How to collect and route the data|Where to view the data|Supported data|

|---------|---------|---------|---------|---------|

|Metric data|Metrics are numerical values that describe an aspect of a system at a particular point in time. Metrics can be aggregated using algorithms, compared to other metrics, and analyzed for trends over time.|- Collected automatically at regular intervals.</br> - You can route some platform metrics to a Log Analytics workspace to query with other data. Check the **DS export** setting for each metric to see if you can use a diagnostic setting to route the metric data.|[Metrics explorer](/azure/azure-monitor/essentials/metrics-getting-started)| [Private Link metrics supported by Azure Monitor](monitor-private-link-reference.md#metrics)|

|Resource log data|Logs are recorded system events with a timestamp. Logs can contain different types of data, and be structured or free-form text. You can route resource log data to Log Analytics workspaces for querying and analysis.|[Create a diagnostic setting](/azure/azure-monitor/essentials/create-diagnostic-settings) to collect and route resource log data.| [Log Analytics](/azure/azure-monitor/learn/quick-create-workspace)| |

|Activity log data|The Azure Monitor activity log provides insight into subscription-level events. The activity log includes information like when a resource is modified or a virtual machine is started.|- Collected automatically.</br> - [Create a diagnostic setting](/azure/azure-monitor/essentials/create-diagnostic-settings) to a Log Analytics workspace at no charge.|[Activity log](/azure/azure-monitor/essentials/activity-log)|  |

[!INCLUDE [azmon-horz-supported-data](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-supported-data.md)]

[!INCLUDE [azmon-horz-tools](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-tools.md)]

[!INCLUDE [azmon-horz-export-data](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-export-data.md)]

[!INCLUDE [azmon-horz-kusto](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-kusto.md)]

[!INCLUDE [azmon-horz-alerts-part-one](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-alerts-part-one.md)]

[!INCLUDE [azmon-horz-alerts-part-two](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-alerts-part-two.md)]

[!INCLUDE [azmon-horz-advisor](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-advisor.md)]

## Related content

- [Azure Private Link monitoring data reference](monitor-private-link-reference.md)

- [Monitoring Azure resources with Azure Monitor](/azure/azure-monitor/essentials/monitor-azure-resource)


# Disable Private Link Service Network Policy

# Disable network policies for Private Link service source IP

When configuring Azure Private Link service, the explicit setting `privateLinkServiceNetworkPolicies` must be disabled on the subnet. This setting only affects the Private Link service. For other resources in the subnet, access is controlled based on the network security group security rules definition.

When you use the portal to create an instance of the Private Link service, this setting is automatically disabled as part of the creation process. Deployments using any Azure client (PowerShell, Azure CLI, or templates) require an extra step to change this property.

To enable or disable the setting, use one of the following options:

* Azure PowerShell

* Azure CLI

* Azure Resource Manager templates

The following examples describe how to enable and disable `privateLinkServiceNetworkPolicies` for a virtual network named `myVNet` with a `default` subnet of `10.1.0.0/24` hosted in a resource group named `myResourceGroup`.

# [**PowerShell**](#tab/private-link-network-policy-powershell)

This section describes how to disable subnet private endpoint policies by using Azure PowerShell. In the following code, replace `default` with the name of your virtual subnet.

```azurepowershell

$subnet = 'default'

$net = @{

Name = 'myVNet'

ResourceGroupName = 'myResourceGroup'

}

$vnet = Get-AzVirtualNetwork @net

($vnet | Select -ExpandProperty subnets | Where-Object {$_.Name -eq $subnet}).privateLinkServiceNetworkPolicies = "Disabled"

$vnet | Set-AzVirtualNetwork

```

# [**CLI**](#tab/private-link-network-policy-cli)

This section describes how to disable subnet private endpoint policies by using the Azure CLI.

```azurecli

az network vnet subnet update \

--name default \

--vnet-name MyVnet \

--resource-group myResourceGroup \

--private-link-service-network-policies Disabled

```

# [**JSON**](#tab/private-link-network-policy-json)

This section describes how to disable subnet private endpoint policies by using Azure Resource Manager templates.

```json

{

"name": "myVNet",

"type": "Microsoft.Network/virtualNetworks",

"apiVersion": "2024-05-01",

"location": "WestUS",

"properties": {

"addressSpace": {

"addressPrefixes": [

"10.1.0.0/16"

]

},

"subnets": [

{

"name": "default",

"properties": {

"addressPrefix": "10.1.0.0/24",

"privateLinkServiceNetworkPolicies": "Disabled"

}

}

]

}

}

```

---

## Next steps

- Learn more about [Azure private endpoints](private-endpoint-overview.md).


# Manage Private Endpoint

# Manage Azure private endpoints

Azure private endpoints have several options for managing their configuration and deployment.

You can determine `GroupId` and `MemberName` values by querying the Azure Private Link resource. You need the `GroupId` and `MemberName` values to configure a static IP address for a private endpoint during creation.

A private endpoint has two custom properties: static IP address and network interface name. These properties must be set when the private endpoint is created.

With a service provider and consumer deployment of Private Link, an approval process is in place to make the connection.

## Determine GroupID and MemberName

During the creation of a private endpoint with Azure PowerShell and the Azure CLI, the `GroupId` and `MemberName` values of the private endpoint resource might be needed.

* `GroupId` is the subresource of the private endpoint.

* `MemberName` is the unique stamp for the private IP address of the endpoint.

For more information about private endpoint subresources and their values, see [Private Link resource](private-endpoint-overview.md#private-link-resource).

To determine the values of `GroupId` and `MemberName` for your private endpoint resource, use the following commands. `MemberName` is contained within the `RequiredMembers` property.

# [**PowerShell**](#tab/manage-private-link-powershell)

An Azure web app is used as the example private endpoint resource. Use [Get-AzPrivateLinkResource](/powershell/module/az.network/get-azprivatelinkresource) to determine the values for `GroupId` and `MemberName`.

```azurepowershell

## Place the previously created webapp into a variable. ##

$webapp =

Get-AzWebApp -ResourceGroupName myResourceGroup -Name myWebApp1979

$resource =

Get-AzPrivateLinkResource -PrivateLinkResourceId $webapp.ID

```

You should receive an output similar to the following example.

# [**Azure CLI**](#tab/manage-private-link-cli)

An Azure web app is used as the example private endpoint resource. Use [az network private-link-resource list](/cli/azure/network/private-link-resource#az-network-private-link-resource-list) to determine `GroupId` and `MemberName`. The parameter `--type` requires the namespace for the Private Link resource. For the web app used in this example, the namespace is `Microsoft.Web/sites`. To determine the namespace for your Private Link resource, see [Azure services DNS zone configuration](private-endpoint-dns.md#azure-services-dns-zone-configuration).

```azurecli

az network private-link-resource list \

--resource-group MyResourceGroup \

--name myWebApp1979 \

--type Microsoft.Web/sites

```

You should receive an output similar to the following example.

---

## Custom properties

Network interface rename and static IP address assignment are custom properties that you can set on a private endpoint during creation.

### Network interface rename

By default, when a private endpoint is created the network interface associated with the private endpoint is given a random name for its network interface. The network interface must be named when the private endpoint is created. The renaming of the network interface of an existing private endpoint is unsupported.

Use the following commands when you create a private endpoint to rename the network interface.

# [**PowerShell**](#tab/manage-private-link-powershell)

To rename the network interface when the private endpoint is created, use the `-CustomNetworkInterfaceName` parameter. The following example uses an Azure PowerShell command to create a private endpoint to an Azure web app. For more information, see [New-AzPrivateEndpoint](/powershell/module/az.network/new-azprivateendpoint).

```azurepowershell

## Place the previously created webapp into a variable. ##

$webapp = Get-AzWebApp -ResourceGroupName myResourceGroup -Name myWebApp1979

## Create the private endpoint connection. ##

$pec = @{

Name = 'myConnection'

PrivateLinkServiceId = $webapp.ID

GroupID = 'sites'

}

$privateEndpointConnection = New-AzPrivateLinkServiceConnection @pec

## Place the virtual network you created previously into a variable. ##

$vnet = Get-AzVirtualNetwork -ResourceGroupName 'myResourceGroup' -Name 'myVNet'

## Create the private endpoint. ##

$pe = @{

ResourceGroupName = 'myResourceGroup'

Name = 'myPrivateEndpoint'

Location = 'eastus'

Subnet = $vnet.Subnets[0]

PrivateLinkServiceConnection = $privateEndpointConnection

CustomNetworkInterfaceName = 'myPrivateEndpointNIC'

}

New-AzPrivateEndpoint @pe

```

# [**Azure CLI**](#tab/manage-private-link-cli)

To rename the network interface when the private endpoint is created, use the `--nic-name` parameter. The following example uses an Azure PowerShell command to create a private endpoint to an Azure web app. For more information, see [az network private-endpoint create](/cli/azure/network/private-endpoint#az-network-private-endpoint-create).

```azurecli

id=$(az webapp list \

--resource-group myResourceGroup \

--query '[].[id]' \

--output tsv)

az network private-endpoint create \

--connection-name myConnection \

--name myPrivateEndpoint \

--private-connection-resource-id $id \

--resource-group myResourceGroup \

--subnet myBackendSubnet \

--group-id sites \

--nic-name myPrivateEndpointNIC \

--vnet-name myVNet

```

---

### Static IP address

By default, when a private endpoint is created, the IP address for the endpoint is automatically assigned. The IP is assigned from the IP range of the virtual network configured for the private endpoint. A situation can arise when a static IP address for the private endpoint is required. The static IP address must be assigned when the private endpoint is created. The configuration of a static IP address for an existing private endpoint is currently unsupported.

For procedures to configure a static IP address when you create a private endpoint, see [Create a private endpoint using Azure PowerShell](create-private-endpoint-powershell.md) and [Create a private endpoint using the Azure CLI](create-private-endpoint-cli.md).

## Private endpoint connections

Private Link works on an approval model where the Private Link consumer can request a connection to the service provider for consuming the service.

The service provider can then decide whether to allow the consumer to connect or not. Private Link enables service providers to manage the private endpoint connection on their resources.

There are two connection approval methods that a Private Link consumer can choose from:

- **Automatic**: If the service consumer has Azure role-based access control (RBAC) permissions on the service provider resource, the consumer can choose the automatic approval method. When the request reaches the service provider resource, no action is required from the service provider and the connection is automatically approved.

- **Manual**: If the service consumer doesn't have RBAC permissions on the service provider resource, the consumer can choose the manual approval method. The connection request appears on the service resources as **Pending**. The service provider has to manually approve the request before connections can be established.

In manual cases, the service consumer can also specify a message with the request to provide more context to the service provider. The service provider has the following options to choose from for all private endpoint connections: **Approve**, **Reject**, and **Remove**.

> [!IMPORTANT]

> To approve connections with a private endpoint that's in a separate subscription or tenant, ensure that the provider subscription or tenant has registered `Microsoft.Network`. The consumer subscription or tenant should also have the resource provider of the destination resource registered.

The following table shows the various service provider actions and the resulting connection states for private endpoints. The service provider can change the connection state at a later time without consumer intervention. The action updates the state of the endpoint on the consumer side.

| Service provider action  | Service consumer private endpoint state | Description |

|---------|---------|---------|

| None    |    Pending     |    Connection is created manually and is pending for approval by the Private Link resource owner.       |

| Approve    |  Approved       |  Connection is automatically or manually approved and is ready to be used.     |

| Reject     | Rejected        | The Private Link resource owner rejects the connection.     |

| Remove    |  Disconnected       | The Private Link resource owner removes the connection, causing the private endpoint to become disconnected and it should be deleted for cleanup.        |

## Manage private endpoint connections on Azure PaaS resources

Use the following steps to manage a private endpoint connection in the Azure portal.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal, enter **Private Link**. In the search results, select **Private Link**.

1. In **Network foundation**, expand **Private Link** in the left menu and select **Private endpoints** or **Private link services**.

1. For each of your endpoints, you can view the number of private endpoint connections associated with it. You can filter the resources as needed.

1. Select the private endpoint. Under the connections listed, select the connection that you want to manage.

1. You can change the state of the connection by selecting from the options at the top.

## Manage private endpoint connections on a customer- or partner-owned Private Link service

Use the following PowerShell and Azure CLI commands to manage private endpoint connections on Microsoft partner services or customer-owned services.

# [**PowerShell**](#tab/manage-private-link-powershell)

Use the following PowerShell commands to manage private endpoint connections.

## Get Private Link connection states

Use [Get-AzPrivateEndpointConnection](/powershell/module/az.network/get-azprivateendpointconnection) to get the private endpoint connections and their states.

```azurepowershell

$get = @{

Name = 'myPrivateLinkService'

ResourceGroupName = 'myResourceGroup'

}

Get-AzPrivateEndpointConnection @get

```

## Approve a private endpoint connection

Use [Approve-AzPrivateEndpointConnection](/powershell/module/az.network/approve-azprivateendpointconnection) to approve a private endpoint connection.

```azurepowershell

$approve = @{

Name = 'myPrivateEndpointConnection'

ServiceName = 'myPrivateLinkService'

ResourceGroupName = 'myResourceGroup'

}

Approve-AzPrivateEndpointConnection @approve

```

## Deny a private endpoint connection

Use [Deny-AzPrivateEndpointConnection](/powershell/module/az.network/deny-azprivateendpointconnection) to reject a private endpoint connection.

```azurepowershell

$deny = @{

Name = 'myPrivateEndpointConnection'

ServiceName = 'myPrivateLinkService'

ResourceGroupName = 'myResourceGroup'

}

Deny-AzPrivateEndpointConnection  @deny

```

## Remove a private endpoint connection

Use [Remove-AzPrivateEndpointConnection](/powershell/module/az.network/remove-azprivateendpointconnection) to remove a private endpoint connection.

```azurepowershell

$remove = @{

Name = 'myPrivateEndpointConnection'

ServiceName = 'myPrivateLinkService'

ResourceGroupName = 'myResourceGroup'

}

Remove-AzPrivateEndpointConnection @remove

```

# [**Azure CLI**](#tab/manage-private-link-cli)

Use the following Azure CLI commands to manage private endpoint connections.

## Get Private Link connection states

Use [az network private-endpoint-connection show](/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-show) to get the private endpoint connections and their states.

```azurecli

az network private-endpoint-connection show \

--name myPrivateEndpointConnection \

--resource-group myResourceGroup

```

## Approve a private endpoint connection

Use [az network private-endpoint-connection approve](/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-approve) to approve a private endpoint connection.

```azurecli

az network private-endpoint-connection approve \

--name myPrivateEndpointConnection  \

--resource-group myResourceGroup

```

## Deny a private endpoint connection

Use [az network private-endpoint-connection reject](/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-reject) to reject a private endpoint connection.

```azurecli

az network private-endpoint-connection reject \

--name myPrivateEndpointConnection  \

--resource-group myResourceGroup

```

## Remove a private endpoint connection

Use [az network private-endpoint-connection delete](/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-delete) to remove a private endpoint connection.

```azurecli

az network private-endpoint-connection delete \

--name myPrivateEndpointConnection \

--resource-group myResourceGroup

```

---

> [!NOTE]

> Connections previously denied can't be approved. You must remove the connection and create a new one.

## Next steps

- [Learn about private endpoints](private-endpoint-overview.md)


# Network Security Perimeter Diagnostic Logs

# Diagnostic logs for Network Security Perimeter

In this article, you learn about the diagnostic logs for Network Security Perimeter and how to enable logging. You learn access logs categories used. Then, you discover the options for storing diagnostic logs and how to enable logging through the Azure portal.

[!INCLUDE [network-security-perimeter-preview-message](../../includes/network-security-perimeter-preview-message.md)]

## Access logs categories

Access logs categories for a network security perimeter are based on the results of access rules evaluation. The log categories chosen in the diagnostic settings are sent to the customer chosen storage location. The following are the descriptions for each of the access log categories including the modes in which they're applicable:

| **Log category** | **Description** | **Applicable to Modes** |

| --- | --- | --- |

| **NspPublicInboundPerimeterRulesAllowed** | Inbound access is allowed based on network security perimeter access rules. | Transition/Enforced |

| **NspPublicInboundPerimeterRulesDenied** | Public inbound access denied by network security perimeter. | Enforced |

| **NspPublicOutboundPerimeterRulesAllowed** | Outbound access is allowed based on network security perimeter access rules. | Transition/Enforced |

| **NspPublicOutboundPerimeterRulesDenied** | Public outbound access denied by network security perimeter. | Enforced |

| **NspOutboundAttempt** | Outbound attempt within network security perimeter. | Transition/Enforced |

| **NspIntraPerimeterInboundAllowed** | Inbound access within perimeter is allowed. | Transition/Enforced |

| **NspPublicInboundResourceRulesAllowed** | When network security perimeter rules deny, inbound access is allowed based on PaaS resource rules. | Transition |

| **NspPublicInboundResourceRulesDenied** | When network security perimeter rules deny, inbound access denied by PaaS resource rules. | Transition |

| **NspPublicOutboundResourceRulesAllowed** | When network security perimeter rules deny, outbound access allowed based on PaaS resource rules. | Transition |

| **NspPublicOutboundResourceRulesDenied** | When network security perimeter rules deny, outbound access denied by PaaS resource rules. | Transition |

| **NspPrivateInboundAllowed** | Private endpoint traffic is allowed. | Transition/Enforced |

> [!NOTE]

> The available access modes for a network security perimeter are **Transition** and **Enforced**. The **Transition** mode was previously named **Learning** mode. You may continue to see references to **Learning** mode in some instances.

## Access log schema

Every PaaS resource associated with the network security perimeter, generates access log(s) with unified log schema when enabled.

> [!NOTE]

> Network security perimeter access logs may have been aggregated. If the fields 'count' and 'timeGeneratedEndTime' are missing, consider the aggregation count as 1.

| **Value** | **Description** |

| --- | --- |

| **time** | The timestamp (UTC) of the first event in log aggregation window. |

| **timeGeneratedEndTime** | The timestamp (UTC) of the last event in the log aggregation window. |

| **count** | Number of logs aggregated. |

| **resourceId** | The resource Id of the network security perimeter.|

| **location** | The region of network security perimeter.|

| **operationName** | The name of the PaaS resource operation represented by this event. |

| **operationVersion** | The api-version associated with the operation. |

| **category** | Log categories defined for Access logs. |

| **properties** | Network security perimeter specific extended properties related to this category of events.|

| **resultDescription** | The static text description of this operation on the PaaS resource, e.g. “Get storage file.” |

## Network security perimeter specific properties

This section describes the network security perimeter specific properties in the log schema.

> [!NOTE]

> Application of the properties is subjected to log category type. Do refer respective log category schemas for applicability.

| **Value** | **Description** |

| --- | --- |

| **serviceResourceId** | Resource ID of PaaS resource emitting network security perimeter access logs. |

| **serviceFqdn** | Fully Qualified Domain Name of PaaS resource emitting network security perimeter access logs. |

| **profile** | Name of the network security perimeter profile associated to the resource. |

| **parameters** | List of optional PaaS resource properties in JSON string format. E.g., { {Param1}: {value1}, {Param2}: {value2}, ...}. |

| **appId** | Unique GUID representing the app ID of resource in the Azure Active Directory. |

| **matchedRule** | JSON property bag containing matched accessRule name, {"accessRule" : "{ruleName}"}. It can be either network security perimeter access rule Name or resource rule name (not the ArmId). |

| **source** | JSON property bag describing source of the inbound connection. |

| **destination** | JSON property bag describing destination of the outbound connection. |

| **accessRulesVersion** | JSON property bag containing access rule version of the resource. |

## Source properties

Properties describing source of inbound connection.

| **Value** | **Description** |

| --- | --- |

| **resourceId** | Resource ID of source PaaS resource for an inbound connection. Will exist if applicable. |

| **ipAddress** | IP address of source making inbound connection. Will exist if applicable. |

| **port** | Port number of inbound connection. May not exist for all resource types. |

| **protocol** | Application & transport layer protocols for inbound connection in format {AppProtocol}:{TptProtocol}. E.g., HTTPS:TCP. May not exist for all resource types. |

| **perimeterGuids** | List of perimeter GUIDs of source resource. It should be specified only if allowed based on perimeter GUID. |

| **appId** | Unique GUID representing the app ID of source in the Azure Active Directory. |

| **parameters** | List of optional source properties in JSON string format. E.g., { {Param1}: {value1}, {Param2}: {value2}, ...}. |

## Destination properties

Properties describing destination of outbound connection.

| **Value** | **Description** |

| --- | --- |

| **resourceId** | Resource ID of destination PaaS resource for an outbound connection. Will exist if applicable. |

| **fullyQualifiedDomainName** | Fully Qualified Domain (FQDN) name of the destination. |

| **parameters** | List of optional destination properties in JSON string format. E.g., { {Param1}: {value1}, {Param2}: {value2}, ...}. |

| **port** | Port number of outbound connection. May not exist for all resource types. |

| **protocol** | Application & transport layer protocols for outbound connection in the format {AppProtocol}:{TptProtocol}. E.g., HTTPS:TCP. May not exist for all resource types. |

## Sample log entry For inbound categories

``` json

{

"time" : "{timestamp}",

"timeGeneratedEndTime" : "{timestamp}",

"count" : "{countOfAggregatedLogs}",

"resourceId" : "/SUBSCRIPTIONS/{subsId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYPERIMETERS/{perimeterName}",

"operationName" : "{PaaSOperationName}" ,

"operationVersion" : "{api-version}",

"category" : "{inboundCategory}",

"location" : "{networksecurityperimeterRegion}",

"properties" : {

"serviceResourceId" : "/subscriptions/{paasSubsId}/resourceGroups/{paasResourceGroupName}/providers/{provider}/{resourceType}/{resourceName}",

"serviceFqdn": "{PaaSResourceFQDN}",

"accessRulesVersion" : "{accessRulesVersion}",

"profile" : "{networksecurityperimeterProfileName}",

"appId" : "{resourceAppId}",

"parameters" : "{ {ParameterType1}: {value1}, {ParameterType2}: {value2}, ...}", // Parsable JSON

"matchedRule" : {

"accessRule" : "{matchedRuleName}",

},

"source" : {

"resourceId" : "/subscriptions/{sourceSubscriptionId}/resourceGroups/{sourceResourceGroupName}/providers/{sourceProvider}/{sourceResourceType}/{sourceResourceName}",

"ipAddress": "{sourceIPAddress}",

"perimeterGuids" : ["{sourcePerimeterGuid}"], // Only included if request comes from perimeter

"appId" : "{sourceAppId}",

"port" : "{Port}",

"protocol" : "{Protocol}",

"parameters" : "{ {ParameterType1}: {value1}, {ParameterType2}: {value2}, ...}", // Parsable JSON

},

},

"resultDescription" : "The static text description of this operation on the PaaS resource. For example, \"Get storage file.\""

}

```

## Sample log entry for outbound categories

``` json

{

"time" : "{timestamp}",

"timeGeneratedEndTime" : "{timestamp}",

"count" : "{countOfAggregatedLogs}",

"resourceId" : "/SUBSCRIPTIONS/{subsId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYPERIMETERS/{perimeterName}",

"operationName" : "{PaaSOperationName}" ,

"operationVersion" : "{api-version}",

"category" : "{outboundCategory}",

"location" : "{networksecurityperimeterRegion}",

"properties" : {

"serviceResourceId" : "/subscriptions/{paasSubsId}/resourceGroups/{paasResourceGroupName}/providers/{provider}/{resourceType}/{resourceName}",

"serviceFqdn": "{PaaSResourceFQDN}",

"accessRulesVersion" : "{accessRulesVersion}",

"profile" : "{networksecurityperimeterProfileName}",

"appId" : "{resourceAppId}",

"parameters" : "{{ParameterType1}: {value1}, {ParameterType2}: {value2}, ...}", // Parsable JSON

"matchedRule" : {

"accessRule" : "{matchedRuleName}",

},

"destination" : {

"resourceId" : "/subscriptions/{destSubsId}/resourceGroups/{destResourceGroupName}/providers/{destProvider}/{destResourceType}/{destResourceName}",

"fullyQualifiedDomainName" : "{destFQDN}",

"appId" : "{destAppId}",

"port" : "{Port}",

"protocol" : "{Protocol}",

"parameters" : "{ {ParameterType1}: {value1}, {ParameterType2}: {value2}, ...}", // Parsable JSON

},

},

"resultDescription" : "The static text description of this operation on the PaaS resource. For example, \"Get storage file.\""

}

```

## Logging destination options for access logs

The destinations for storing diagnostic logs for a network security perimeter include services like Log Analytic workspace (**Table name: NSPAccessLogs**), Azure Storage account, and Azure Event Hubs. For the full list and details of supported destinations, see [Supported destinations for diagnostic logs](/azure/azure-monitor/essentials/diagnostic-settings).

## Enable logging through the Azure portal

You can enable diagnostic logging for a network security perimeter by using the Azure portal under Diagnostic settings. When adding a diagnostic setting, you can choose the log categories you want to collect and the destination where you want to deliver the logs.

> [!NOTE]

> When using Azure Monitor with a network security perimeter, the Log Analytics workspace to be associated with the network security perimeter needs to be located in one of the Azure Monitor supported regions.

> [!Warning]

> The log destinations must be within the same network security perimeter as the PaaS resource to ensure the proper flow of PaaS resource logs. Configuring/already configured Diagnostic Settings for resources not included in the list of [Onboarded private link resources](/azure/private-link/network-security-perimeter-concepts#onboarded-private-link-resources), will result in the cessation of log flow for those resources.

## Next steps

> [!div class="nextstepaction"]

> [Create a network security perimeter in the Azure portal](./create-network-security-perimeter-portal.md)


# Private Link Support Help

# Support and troubleshooting for Azure Private Link

Here are suggestions for where you can get help when developing your Azure Private Link solutions.

## Self help troubleshooting

Various articles explain how to determine, diagnose, and fix issues that you might encounter when using Azure Private Link. Use these articles to troubleshoot private endpoint connectivity problems, Private Link service issues, and more.

For a full list of self help troubleshooting content, see [Azure Private Link troubleshooting documentation](/troubleshoot/azure/private-link/welcome-azure-private-link).

## Post a question on Microsoft Q&A

For quick and reliable answers on your technical product questions from Microsoft Engineers, Azure Most Valuable Professionals (MVPs), or our expert community, engage with us on [Microsoft Q&A](/answers/products/azure), Azure's preferred destination for community support.

If you can't find an answer to your problem using search, submit a new question to Microsoft Q&A. Use the following tag when asking your question:

| Area | Tag |

| --- | --- |

| [Azure Private Link](./private-link-overview.md) | [azure-private-link](/answers/tags/73/azure-private-link) |

## Create an Azure support request

Explore the range of [Azure support options and choose the plan](https://azure.microsoft.com/support/plans) that best fits, whether you're a developer just starting your cloud journey or a large organization deploying business-critical, strategic applications. Azure customers can create and manage support requests in the Azure portal.

- If you already have an Azure Support Plan, [open a support request here](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest).

- To sign up for a new Azure Support Plan, [compare support plans](https://azure.microsoft.com/support/plans/) and select the plan that works for you.

## Create a GitHub issue

If you need help with the language and tools used to develop and manage Azure Private Link, open an issue in its repository on GitHub.

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

| Bicep | https://github.com/Azure/bicep/issues |

## Stay informed of updates and new releases

Learn about important product updates, roadmap, and announcements in [Azure Updates](https://azure.microsoft.com/updates/?category=networking).

News and information about Azure Private Link is shared at the [Azure Networking blog](https://techcommunity.microsoft.com/category/azure/blog/azurenetworkingblog).

## Next steps

Learn more about [Azure Private Link](./private-link-overview.md)


# Monitor Private Link Reference

# Azure Private Link monitoring data reference

[!INCLUDE [horz-monitor-ref-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-intro.md)]

See [Monitor Azure Private Link](monitor-private-link.md) for details on the data you can collect for Private Link and how to use it.

[!INCLUDE [horz-monitor-ref-metrics-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-intro.md)]

### Supported metrics for Microsoft.Network/privateLinkServices

The following table lists the metrics available for the Microsoft.Network/privateLinkServices resource type.

[!INCLUDE [horz-monitor-ref-metrics-tableheader](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-tableheader.md)]

[!INCLUDE [<ResourceType/namespace>](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/metrics/microsoft-network-privatelinkservices-metrics-include.md)]

[!INCLUDE [horz-monitor-ref-metrics-dimensions-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-dimensions-intro.md)]

[!INCLUDE [horz-monitor-ref-metrics-dimensions](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-dimensions.md)]

- PrivateLinkServiceIPAddress

[!INCLUDE [horz-monitor-ref-activity-log](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-activity-log.md)]

- [Microsoft.Networking resource provider operations](/azure/role-based-access-control/resource-provider-operations#networking)

## Related content

- See [Monitor Azure Private Link](monitor-private-link.md) for a description of monitoring Private Link.

- See [Monitor Azure resources with Azure Monitor](/azure/azure-monitor/essentials/monitor-azure-resource) for details on monitoring Azure resources.


# Inspect Traffic With Azure Firewall

# Azure Firewall scenarios to inspect traffic destined to a private endpoint

> [!NOTE]

> If you want to secure traffic to private endpoints in Azure Virtual WAN using secured virtual hub, see [Secure traffic destined to private endpoints in Azure Virtual WAN](../firewall-manager/private-link-inspection-secure-virtual-hub.md).

Azure Private Endpoint is the fundamental building block for Azure Private Link. Private endpoints enable Azure resources deployed in a virtual network to communicate privately with private link resources.

Private endpoints allow resources access to the private link service deployed in a virtual network. Access to the private endpoint through virtual network peering and on-premises network connections extend the connectivity.

You may need to inspect or block traffic from clients to the services exposed via private endpoints. Complete this inspection by using [Azure Firewall](../firewall/overview.md) or a third-party network virtual appliance.

The following limitations apply:

* Network security groups (NSG) traffic is bypassed from private endpoints due to network policies being disabled for a subnet in a virtual network by default. To utilize network policies like User-Defined Routes and Network Security Groups support, network policy support must be enabled for the subnet. This setting is only applicable to private endpoints within the subnet. This setting affects all private endpoints within the subnet. For other resources in the subnet, access is controlled based on security rules in the network security group.

* User-defined routes (UDR) traffic is bypassed from private endpoints. User-defined routes can be used to override traffic destined for the private endpoint.

* A single route table can be attached to a subnet

* A route table supports up to 400 routes

Azure Firewall filters traffic using either:

* [FQDN in network rules](../firewall/fqdn-filtering-network-rules.md) for TCP and UDP protocols

* [FQDN in application rules](../firewall/features-by-sku.md) for HTTP, HTTPS, and MSSQL.

> [!IMPORTANT]

> The use of application rules over network rules is recommended when inspecting traffic destined to private endpoints in order to maintain flow symmetry. Application rules are preferred over network rules to inspect traffic destined to private endpoints because Azure Firewall always SNATs traffic with application rules. If network rules are used, or an NVA is used instead of Azure Firewall, SNAT must be configured for traffic destined to private endpoints in order to maintain flow symmetry.

> [!NOTE]

> SQL FQDN filtering is supported in [proxy-mode](/azure/azure-sql/database/connectivity-architecture#connection-policy) only (port 1433). **Proxy** mode can result in more latency compared to *redirect*. If you want to continue using redirect mode, which is the default for clients connecting within Azure, you can filter access using FQDN in firewall network rules.

## Scenario 1: Hub and spoke architecture - Dedicated virtual network for private endpoints

This scenario is the most expandable architecture to connect privately to multiple Azure services using private endpoints. A route pointing to the network address space where the private endpoints are deployed is created. This configuration reduces administrative overhead and prevents running into the limit of 400 routes.

Connections from a client virtual network to the Azure Firewall in a hub virtual network incurs charges if the virtual networks are peered. Connections from Azure Firewall in a hub virtual network to private endpoints in a peered virtual network aren't charged.

For more information on charges related to connections with peered virtual networks, see the FAQ section of the [pricing](https://azure.microsoft.com/pricing/details/private-link/) page.

## Scenario 2: Hub and spoke architecture - Shared virtual network for private endpoints and virtual machines

This scenario is implemented when:

* It's not possible to have a dedicated virtual network for the private endpoints

* When only a few services are exposed in the virtual network using private endpoints

The virtual machines have /32 system routes pointing to each private endpoint. One route per private endpoint is configured to route traffic through Azure Firewall.

The administrative overhead of maintaining the route table increases as services are exposed in the virtual network. The possibility of hitting the route limit also increases.

Depending on your overall architecture, it's possible to run into the 400 routes limit. It's recommended to use scenario 1 whenever possible.

Connections from a client virtual network to the Azure Firewall in a hub virtual network incurs charges if the virtual networks are peered. Connections from Azure Firewall in a hub virtual network to private endpoints in a peered virtual network aren't charged.

For more information on charges related to connections with peered virtual networks, see the FAQ section of the [pricing](https://azure.microsoft.com/pricing/details/private-link/) page.

## Scenario 3: Single virtual network

Use this pattern when a migration to a hub and spoke architecture isn't possible. The same considerations as in scenario 2 apply. In this scenario, virtual network peering charges don't apply.

## Scenario 4: On-premises traffic to private endpoints

This architecture can be implemented if you have configured connectivity with your on-premises network using either:

* [ExpressRoute](../expressroute/expressroute-introduction.md)

* [Site to Site VPN](../vpn-gateway/tutorial-site-to-site-portal.md)

If your security requirements require client traffic to services exposed via private endpoints to be routed through a security appliance, deploy this scenario.

The same considerations as in scenario 2 above apply. In this scenario, there aren't virtual network peering charges. For more information about how to configure your DNS servers to allow on-premises workloads to access private endpoints, see [on-premises workloads using a DNS forwarder](./private-endpoint-dns-integration.md#on-premises-workloads-using-a-dns-forwarder).

## Next steps

In this article, you explored different scenarios that you can use to restrict traffic between a virtual machine and a private endpoint using Azure Firewall.

For a tutorial on how to configure Azure Firewall to inspect traffic destined to a private endpoint, see [Tutorial: Inspect private endpoint traffic with Azure Firewall](tutorial-inspect-traffic-azure-firewall.md)

To learn more about private endpoint, see [What is Azure Private Endpoint?](private-endpoint-overview.md)
