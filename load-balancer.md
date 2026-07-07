# Load Balancer Overview

# What is Azure Load Balancer?

>[!Important]

>On September 30, 2025, Basic Load Balancer was retired. For more information, see the [official announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). If you are currently using Basic Load Balancer, make sure to upgrade to Standard Load Balancer as soon as possible. For guidance on upgrading, visit [Upgrading from Basic Load Balancer - Guidance](load-balancer-basic-upgrade-guidance.md).

Azure Load Balancer is a cloud service that distributes incoming network traffic across backend virtual machines (VMs) or virtual machine scale sets (VMSS). This article explains Azure Load Balancer's key features, architecture, and scenarios, helping you decide if it fits your organization's load balancing needs for scalable, highly available workloads.

*Load balancing* refers to efficiently distributing incoming network traffic across a group of backend virtual machines (VMs) or virtual machine scale sets (VMSS).

> [!NOTE]

> Azure Load Balancer is one of the services that make up the Load Balancing and Content Delivery category in Azure. Other services in this category include [Azure Front Door](../frontdoor/front-door-overview.md) and [Azure Application Gateway](../application-gateway/overview.md). Each service has its own unique features and use cases. For more information on this service category, see [Load Balancing and Content Delivery](../networking/load-balancer-content-delivery/load-balancing-content-delivery-overview.md).

## Load balancer overview

Azure Load Balancer operates at layer 4 of the Open Systems Interconnection (OSI) model. It's the single point of contact for clients. The service distributes inbound flows that arrive at the load balancer's frontend to backend pool instances. These flows are distributed according to configured load-balancing rules and health probes. The backend pool instances can be Azure virtual machines (VMs) or virtual machine scale sets.

A [public load balancer](./components.md#frontend-ip-configurations) can provide both inbound and outbound connectivity for the VMs inside your virtual network. For inbound traffic scenarios, Azure Load Balancer can load balance internet traffic to your VMs. For outbound traffic scenarios, the service can translate the VMs' private IP addresses to public IP addresses for any outbound connections that originate from your VMs.

Alternatively, an [internal (or private) load balancer](./components.md#frontend-ip-configurations) are used to load balance traffic inside a virtual network. With internal load balancer, you can provide inbound connectivity to your VMs in private network connectivity scenarios, such as accessing a load balancer frontend from an on-premises network in a hybrid scenario.

For more information on the service's individual components, see [Azure Load Balancer components](./components.md).

Azure Load Balancer has three stock-keeping units (SKUs) - Basic, Standard, and Gateway. Each SKU is catered towards a specific scenario and has differences in scale, features, and pricing. For more information, see [Azure Load Balancer SKUs](skus.md).

## Why use Azure Load Balancer

With Azure Load Balancer, you can scale your applications and create highly available services. The service supports both inbound and outbound scenarios, provides low latency and high throughput, and scales up to millions of flows for all TCP and UDP applications.

### Core capabilities

Azure Load Balancer provides:

- **High availability**: Distribute resources [within](./tutorial-load-balancer-standard-public-zonal-portal.md) and [across](./quickstart-load-balancer-standard-public-portal.md) availability zones

- **Scalability**: Handle millions of flows for TCP and UDP applications

- **Low latency**: Use pass-through load balancing for ultralow latency

- **Flexibility**: Support for [multiple ports, multiple IP addresses, or both](./load-balancer-multivip-overview.md)

- **Health monitoring**: Use [health probes](./load-balancer-custom-probe-overview.md) to ensure traffic is only sent to healthy instances

### Traffic distribution scenarios

- Load balance [internal](./quickstart-load-balancer-standard-internal-portal.md) and [external](./quickstart-load-balancer-standard-public-portal.md) traffic to Azure virtual machines

- Configure [outbound connectivity](./load-balancer-outbound-connections.md) for Azure virtual machines

- Load balance TCP and UDP flow on all ports simultaneously using [high-availability ports](./load-balancer-ha-ports-overview.md)

- Enable [port forwarding](./tutorial-load-balancer-port-forwarding-portal.md) to access virtual machines by public IP address and port

### Advanced features

- **IPv6 support**: Enable [load balancing of IPv6](./virtual-network-ipv4-ipv6-dual-stack-standard-load-balancer-powershell.md) traffic

- **Cross-region mobility**: Move [internal](./move-across-regions-internal-load-balancer-portal.md) and [external](./move-across-regions-external-load-balancer-portal.md) load balancer resources across Azure regions

- **Gateway load balancer integration**: Chain Standard Load Balancer and [Gateway Load Balancer](./tutorial-create-gateway-load-balancer.md)

- **Global load balancing integration**: Distribute traffic [across multiple Azure regions](./cross-region-overview.md) for global applications

- **Admin State**: [Override health probe behavior](./manage-admin-state-how-to.md) for maintenance and operational management

### Monitoring and insights

- **Comprehensive metrics**: Use multidimensional metrics through [Azure Monitor](/azure/azure-monitor/overview)

- **Pre-built dashboards**: Access [Insights for Azure Load Balancer](./load-balancer-insights.md) with useful visualizations

- **Diagnostics**: Review [Standard load balancer diagnostics](load-balancer-standard-diagnostics.md) for performance insights

- **Health Event Logs**: Monitor load balancer [health events](./load-balancer-health-event-logs.md) and status changes for proactive management

- **Load Balancer health status**: Gain deeper insights into the health of your load balancer through [health status](./load-balancer-manage-health-status.md) monitoring

### <a name="securebydefault"></a>Security features

Azure Load Balancer implements security through multiple layers:

#### Zero Trust security model

- **Standard Load Balancer** is built on the Zero Trust network security model

- Part of your virtual network, which is private and isolated by default

#### Network access controls

- Standard load balancers and public IP addresses are **closed to inbound connections by default**

- **Network Security Groups (NSGs)** must explicitly permit allowed traffic

- Traffic is blocked if no NSG exists on a subnet or NIC

#### Data protection

- Azure Load Balancer **doesn't store customer data**

- All traffic processing happens in real-time without data persistence

> [!IMPORTANT]

> Basic Load Balancer is open to the internet by default and will be retired on September 30, 2025. Migrate to Standard Load Balancer for enhanced security.

To learn about NSGs and how to apply them to your scenario, see [Network security groups](../virtual-network/network-security-groups-overview.md).

## Pricing and SLA

For [Standard Load Balancer](https://github.com/MicrosoftDocs/azure-docs/blob/main/articles/load-balancer/skus.md) pricing information, see [Load Balancer pricing](https://azure.microsoft.com/pricing/details/load-balancer/). For service-level agreements (SLAs), see the [Microsoft licensing information for online services](https://aka.ms/lbsla).

Basic Load Balancer is offered at no charge and has no SLA. It was retired on September 30, 2025.

## What's new?

Subscribe to the RSS feed and view the latest Azure Load Balancer updates on the [Azure Updates](https://azure.microsoft.com/updates?filters=%5B%22Load+Balancer%22%5D) page.

## Related content

- [Create a public load balancer](quickstart-load-balancer-standard-public-portal.md)

- [Azure Load Balancer components](./components.md)


# Gateway Overview

# Gateway Load Balancer

Gateway Load Balancer is a SKU of the Azure Load Balancer portfolio catered for high performance and high availability scenarios with third-party Network Virtual Appliances (NVAs). With the capabilities of Gateway Load Balancer, you can easily deploy, scale, and manage NVAs. Chaining a Gateway Load Balancer to your public endpoint only requires one selection.

You can insert appliances transparently for different kinds of scenarios such as:

1. Firewalls

1. Advanced packet analytics

1. Intrusion detection and prevention systems

1. Traffic mirroring

1. DDoS protection

1. Custom appliances

With Gateway Load Balancer, you can easily add or remove advanced network functionality without extra management overhead. It provides the bump-in-the-wire technology you need to ensure all traffic to and from a public endpoint is first sent to the appliance before your application. In scenarios with NVAs, it's especially important that flows are symmetrical. Gateway Load Balancer maintains flow stickiness to a specific instance in the backend pool along with flow symmetry. As a result, a consistent route to your network virtual appliance is ensured – without further manual configuration. As a result, packets traverse the same network path in both directions and appliances that need this key capability are able to function seamlessly.

The health probe listens across all ports and routes traffic to the backend instances using the HA ports rule. Traffic sent to and from Gateway Load Balancer uses the VXLAN protocol.

## Benefits

Gateway Load Balancer has the following benefits:

1. Integrate virtual appliances transparently into the network path.

1. Easily add or remove network virtual appliances in the network path.

1. Scale with ease while managing costs.

1. Improve network virtual appliance availability.

1. Chain applications across tenants and subscriptions

## Configuration and supported scenarios

A Standard Public Load Balancer or a Standard IP configuration of a virtual machine can be chained to a Gateway Load Balancer. "Chaining" refers to the load balancer frontend or NIC IP configuration containing a reference to a Gateway Load Balancer frontend IP configuration. Once the Gateway Load Balancer is chained to a consumer resource, no other configuration such as UDRs is needed to ensure traffic to and from the application endpoint is sent to the Gateway Load Balancer.

Gateway Load Balancer supports both inbound and outbound traffic inspection. For inserting NVAs in the path of outbound traffic with Standard Load Balancer, Gateway Load Balancer must be chained to the frontend IP configurations selected in the configured outbound rules.

> [!NOTE]

> Configuring a Gateway Load Balancer's frontend IP as the next hop in user-defined routes (UDRs) is not supported. Gateway Load Balancer resources must be chained/referenced by a supported consumer resource such as a Standard Public Load Balancer or Standard NIC IP configuration.

## Data path diagram

With Gateway Load Balancer, traffic intended for the consumer application through a Standard Load Balancer will be encapsulated with VXLAN headers and forwarded first to the Gateway Load Balancer and its configured NVAs in the backend pool. The traffic then returns to the consumer resource (in this case a Standard Load Balancer) and arrives at the consumer application virtual machines with its source IP preserved. The consumer virtual network and provider virtual network can be in different subscriptions or tenants, reducing management overhead.

*Figure: Diagram of gateway load balancer.*

## Components

Gateway Load Balancer consists of the following components:

* **Frontend IP configuration** - The IP address of your Gateway Load Balancer. This IP is private only.

* **Load-balancing rules** - A load balancer rule is used to define how incoming traffic is distributed to all the instances within the backend pool. A load-balancing rule maps a given frontend IP configuration and port to multiple backend IP addresses and ports.

* Gateway Load Balancer rules can only be HA port rules.

* A Gateway Load Balancer rule can be associated with up to two backend pools.

* **Backend pool(s)** - The group of virtual machines or instances in a Virtual Machine Scale Set that's serving the incoming request. To scale cost-effectively to meet high volumes of incoming traffic, computing guidelines generally recommend adding more instances to the backend pool. Load Balancer instantly reconfigures itself via automatic reconfiguration when you scale instances up or down. Adding or removing VMs from the backend pool reconfigures the load balancer without extra operations. The scope of the backend pool is any virtual machine in a single virtual network.

* **Tunnel interfaces** - Gateway Load balancer backend pools have another component called the tunnel interfaces. The tunnel interface enables the appliances in the backend to ensure network flows are handled as expected. Each backend pool can have up to two tunnel interfaces. Tunnel interfaces can be either internal or external. For traffic coming to your backend pool, you should use the external type. For traffic going from your appliance to the application, you should use the internal type.

* **Chain** - A Gateway Load Balancer can be referenced by a Standard Public Load Balancer frontend or a Standard Public IP configuration on a virtual machine. The addition of advanced networking capabilities in a specific sequence is known as service chaining. As a result, this reference is called a chain. A Cross tenant chain involves chaining a Load Balancer frontend or Public IP configuration to a Gateway Load Balancer that is in another subscription. For cross tenant chaining, users need:

* Permission for the resource provider operation `Microsoft.Network/loadBalancers/frontendIPConfigurations/join/action`.

* Guest access to the subscription of the Gateway Load Balancer.

## Pricing

For pricing, see [Load Balancer pricing](https://azure.microsoft.com/pricing/details/load-balancer/).

## Limitations

1. Gateway Load Balancer doesn't work with the Global Load Balancer tier.

1. Cross-tenant chaining isn't supported through the Azure portal.

## Next steps

1. See [Create a Gateway Load Balancer using the Azure portal](tutorial-create-gateway-load-balancer.md) to create a gateway load balancer.

1. Learn how to use [Gateway Load Balancer for outbound connectivity scenarios](tutorial-gateway-outbound-connectivity.md).

1. Learn more about [Azure Load Balancer](load-balancer-overview.md).


# Cross Region Overview

# Global Load Balancer

Azure Standard Load Balancer supports global load balancing enabling geo-redundant high availability scenarios such as:

- Incoming traffic originating from multiple regions.

- [Instant global failover](#regional-redundancy) to the next optimal regional deployment.

- Load distribution across regions to the closest Azure region with [ultra-low latency](#ultra-low-latency).

- Ability to [scale up/down](#ability-to-scale-updown-behind-a-single-endpoint) behind a single endpoint.

- Static anycast global IP address

- [Client IP preservation](#client-ip-preservation)

- [Build on existing load balancer](#build-cross-region-solution-on-existing-azure-load-balancer) solution with no learning curve

The frontend IP configuration of your global load balancer is static and advertised across [most Azure regions](#participating-regions-in-azure).

> [!NOTE]

> The backend port of your load balancing rule on global load balancer should match the frontend port of the load balancing rule/inbound nat rule on regional standard load balancer.

### Regional redundancy

Configure regional redundancy by seamlessly linking a global load balancer to your existing regional load balancers.

If one region fails, the traffic is routed to the next closest healthy regional load balancer.

The health probe of the global load balancer gathers information about availability of each regional load balancer every 5 seconds. If one regional load balancer drops its availability to 0, global load balancer detects the failure. The regional load balancer is then taken out of rotation.

### Ultra-low latency

The geo-proximity load-balancing algorithm is based on the geographic location of your users and your regional deployments.

Traffic started from a client hits the closest participating region and travel through the Microsoft global network backbone to arrive at the closest regional deployment.

For example, you have a global load balancer with standard load balancers in Azure regions:

- West US

- North Europe

If a flow is started from Seattle, traffic enters West US. This region is the closest participating region from Seattle. The traffic is routed to the closest region load balancer, which is West US.

Azure global load balancer uses geo-proximity load-balancing algorithm for the routing decision.

The configured load distribution mode of the regional load balancers is used for making the final routing decision when multiple regional load balancers are used for geo-proximity.

For more information, see [Configure the distribution mode for Azure Load Balancer](./load-balancer-distribution-mode.md).

Egress traffic follows the routing preference set on the regional load balancers.

### Ability to scale up/down behind a single endpoint

When you expose the global endpoint of a global load balancer to customers, you can add or remove regional deployments behind the global endpoint without interruption.

### Static anycast global IP address

Global load balancer comes with a static public IP, which ensures the IP address remains the same. Both IPv4 and IPv6 configurations are supported. To learn more about static IP, read more [here.](../virtual-network/ip-services/public-ip-addresses.md#ip-address-assignment)

### Client IP Preservation

Global load balancer is a Layer-4 pass-through network load balancer. This pass-through preserves the original IP of the packet. The original IP is available to the code running on the virtual machine. This preservation allows you to apply logic that is specific to an IP address.

### Floating IP

Floating IP can be configured at both the global IP level and regional IP level. For more information, visit [Multiple frontends for Azure Load Balancer.](./load-balancer-multivip-overview.md)

It's important to note that floating IP configured on the Azure global Load Balancer operates independently of floating IP configurations on backend regional load balancers. If floating IP is enabled on the global load balancer, the appropriate loopback interface needs to be added to the backend VMs.

### Health Probes

Azure global Load Balancer utilizes the health of the backend regional load balancers when deciding where to distribute traffic to. Health checks by global load balancer are done automatically every 5 seconds, given that health probes are set up on their regional load balancer.

## Build cross region solution on existing Azure Load Balancer

The backend pool of global load balancer contains one or more regional load balancers.

Add your existing load balancer deployments to a global load balancer for a highly available, global deployment.

### Home regions and participating regions

**Home region** is where the global load balancer or Public IP Address of Global tier is deployed.

This region doesn't affect how the traffic is routed. If a home region goes down, traffic flow is unaffected.

#### Home regions in Azure

- Central US

- East Asia

- East US 2

- North Europe

- Southeast Asia

- UK South

- US Gov Virginia

- West Europe

- West US

- China North 2

> [!NOTE]

> You can only deploy your global load balancer or Public IP in Global tier in one of the listed Home regions.

A **participating region** is where the Global public IP of the load balancer is being advertised.

Traffic started by the user travels to the closest participating region through the Microsoft core network.

Global load balancer routes the traffic to the appropriate regional load balancer.

#### Participating regions in Azure

- Australia East

- Australia Southeast

- Central India

- Central US

- East Asia

- East US

- East US 2

- Japan East

- North Central US

- North Europe

- South Central US

- Southeast Asia

- UK South

- US DoD Central

- US DoD East

- US Gov Arizona

- US Gov Texas

- US Gov Virginia

- West Central US

- West Europe

- West US

- West US 2

> [!NOTE]

> The backend regional load balancers can be deployed in any publicly available Azure Region and isn't limited to just participating regions.

## Limitations of global load balancer

- Global frontend IP configurations are public only. An internal frontend is currently not supported.

- Private or internal load balancer can't be added to the backend pool of a global load balancer

- NAT64 translation isn't supported at this time. The frontend and backend IPs must be of the same type (v4 or v6).

- UDP traffic on port 3 isn't supported on global load balancer

- Outbound rules aren't supported on global load balancer. For outbound connections, utilize [outbound rules](./outbound-rules.md) on the regional load balancer or [NAT gateway](../nat-gateway/nat-overview.md).

- Regional load balancers can't be upgraded to the global tier. Only new load balancers can be created as the global tier.

- When placing the same NIC(s) behind multiple regional load balancers with global load balancer, the load balancing rules on each regional load balancer with the same frontend port must also be configured to the same backend port.

- ICMP protocol is not supported for global load balancer and ICMP Ping is expected to fail.

## Pricing and SLA

Global load balancer shares the [SLA](https://azure.microsoft.com/support/legal/sla/load-balancer/v1_0/) of standard load balancer.

## Next steps

- See [Tutorial: Create a global load balancer using the Azure portal](tutorial-cross-region-portal.md) to create a global load balancer.

- Learn more about [global load balancer](https://www.youtube.com/watch?v=3awUwUIv950).

- Learn more about [Azure Load Balancer](load-balancer-overview.md).


# Cross Subscription Overview

# Cross-subscription Load balancer

Azure Load Balancer supports cross-subscription load balancing, where the frontend IP and/or the backend pool instances can be in a different subscription than the Azure Load Balancer.

This article provides an overview of cross-subscription load balancing with Azure Load Balancer, and the scenarios it supports.

## What is cross-subscription load balancing?

Cross-subscription load balancing allows you to deploy Azure Load Balancer resources across multiple subscriptions. This feature enables you to deploy a load balancer in one subscription and have the frontend IP and backend pool instances in a different subscription. This capability is useful for organizations that have separate subscriptions for networking and application resources.

This table illustrates some of the possible scenarios cross-subscription load balancing supports.

| **Subscription 1** | **Subscription 2** |

|----------------|----------------|

| Load Balancer | Backend pool resources and Frontend IP address |

| Load Balancer and Backend pool resources | Frontend IP address |

| Load Balancer and Frontend IP address | Backend pool resources |

## Cross-subscription frontend IP configurations

Cross-subscription frontends allow the frontend IP configuration to reside in a different subscription other than the load balancer’s subscription. To enable cross-subscription frontend IP configurations, all backend pools need to have the `SyncMode` property configured.

### Public frontend IP configurations

Public IP addresses utilized by an Azure Load Balancer can reside in different subscription than the load balancer. If multiple public IP addresses are attached to a load balancer, each IP address can come from a different subscription. For example, if we have a Load Balancer (deployed in subscription C) with two frontend IPs, the first IP address can reside in subscription B and the second IP address can reside in subscription A.

An important note is that once a frontend IP configuration is set, its subscription can’t be modified. However, the frontend IP configuration can be updated with a different IP address within the same subscription. For example, if a frontend IP configuration is attached to IP address A in subscription 1, it can be updated to IP address B also in subscription 1.

Cross-subscription public IP addresses are only supported on the regional tier standard load balancer

### Internal frontend IP configurations

Like public load balancers, internal load balancers can also have cross-subscription frontend IP configurations. In this case, the subnet/virtual network can reside in a different subscription than the load balancer. However, unlike public frontends, all internal frontend configurations must come from the same subnet/virtual network. Furthermore, all backend pools must be configured to the same virtual network as the frontend IP configurations.

## Cross-subscription backend pools

Cross-subscription backends allow backend instances to reside in a different subscription other than the load balancer’s subscription. For example, the load balancer could be in subscription 1 and my backend VMs could be located in subscription 2.

The backend instances and the virtual network they refer to can be located in a different subscription. Cross-subscription backend pools must utilize a new property known as *SyncMode*.

### What is SyncMode

The *SyncMode* property is a parameter that you can specify when you create a backend pool by using IP addresses and virtual network IDs. This property must be set when using cross-subscription frontends or backends. It has two possible values: *Automatic* or *Manual*.

In addition, this property replaces the concept of NIC-based or IP-based backend pools. As a result, backend pools with the SyncMode property configured are a distinct type of backend pool, separate from NIC or IP-based backend pools. Backend pools can either be exclusively NIC-based, IP-based, or SyncMode enabled.

#### When should I use Automatic SyncMode

With SyncMode configured as *Automatic*, backend pool instances are synchronized with the load balancer configuration. As a result, changes to the backend pool instances are automatically reflected in the load balancer’s backend pool configuration. This change is relevant when using virtual machine scale sets in the backend pool. When the scale set scales in/out, the backend pool members are automatically added or removed from the pool accordingly.

Like NIC (network interface cards) based backend pools, if SyncMode is set to *Automatic*, then each backend instance’s NIC must also reference the load balancer backend pool. As a result, backend instances are added to *Automatic* SyncMode backend pools by updating the NIC resource’s reference to the load balancer.

#### When should I use Manual SyncMode

With SyncMode configured as *Manual*, backend pool instances aren't synchronized with the load balancer configuration. This mode allows you to create a backend pool with pre-provisioned private IP addresses that can be used for scenarios such as disaster recovery, active-passive, or dynamic provisioning. When using *Manual* SyncMode backend pools, you're responsible for updating the backend pool when any changes to your backend instances occur, such as with a scale set autoscaling.

## Cross-subscription Global Load Balancer

In addition, cross-subscription load balancing is supported for Azure global Load Balancer. With cross-subscription global load balancer, backend regional load balancers can each be located in different subscriptions. Cross-subscription backends on a global load balancer don't need other parameters or changes to the backend pool.

> [!NOTE]

>  Cross-subscription frontends aren't supported on Azure global Load Balancer today.

## Authorization

To enable cross-subscription load balancing, a user must be assigned to the *Network Contributor* role or to a custom role that is assigned the appropriate actions listed in the following table on both subscriptions:

### Cross-subscription Frontends

#### Public Frontends

Microsoft.Network/loadBalancers/frontendIPConfigurations/join/action

Microsoft.Network/publicIPAddresses/join/action

#### Internal Frontends

Microsoft.Network/loadBalancers/frontendIPConfigurations/join/action

### Cross-subscription Backends

Microsoft.Network/loadBalancers/backendAddressPools/write

Microsoft.Network/loadBalancers/backendAddressPools/join/action

Microsoft.Network/virtualNetworks/write

Microsoft.Network/networkInterfaces/write

### Cross-tenant

When working cross-tenant, a user must be assigned to the *Network Contributor* role or to a custom role that is assigned the appropriate actions for cross-subscription frontends in both subscriptions. More information on cross-tenant linkage, see [Authenticate requests across tenants](../azure-resource-manager/management/authenticate-multi-tenant.md).

## Limitations

- SyncMode can only be set on new backend pools

- The SyncMode property must be explicitly set – by default, the SyncMode property is unspecified

- API version 2023-04-01 and above needs to be used to when deploying/updating the load balancers

- Once configured, the SyncMode property can't be changed on a backend pool

- A virtual network must be specified when the SyncMode property is configured. Once a virtual network is configured, it can’t be updated on the backend pool

- Inbound NAT pools aren’t supported for cross-subscription load balancers. Utilize inbound NAT rules

- All resources must be deployed in the same region as the load balancer

- SyncMode property isn't supported on cross-region load balancer backend pools

- Cross-subscription load balancers can't be chained to Gateway Load Balancers

- Gateway Load Balancers can't have cross-subscription components

## Next steps

> [!div class="nextstepaction"]

> [ Create a cross-subscription internal load balancer](./cross-subscription-how-to-internal-load-balancer.md)


# Load Balancer Custom Probe Overview

# Azure Load Balancer health probes

An Azure Load Balancer health probe is a feature that detects the health status of your application instances. It sends a request to the instances to check if they're available and responding to requests. The health probe can be configured to use different protocols such as TCP, HTTP, or HTTPS. It's an important feature because it helps you to detect application failures, manage load, and plan for downtime.

Azure Load Balancer rules require a health probe to detect the endpoint status. The configuration of the health probe and probe responses determines which backend pool instances receive new connections. Use health probes to detect the failure of an application. Generate a custom response to a health probe. Use the health probe for flow control to manage load or planned downtime. When a health probe fails, the load balancer stops sending new connections to the respective unhealthy instance. Outbound connectivity isn't affected, only inbound.

## Probe protocols

Health probes support multiple protocols. The availability of a specific health probe protocol varies by Load Balancer SKU. Additionally, the behavior of the service varies by Load Balancer SKU as shown in this table:

| SKU | [Probe protocol](#probe-protocol) | [Probe down behavior](#probe-down-behavior) |

| --- | --- | --- |

| Standard | TCP, HTTP, HTTPS | All probes down, all TCP flows continue. |

| Basic | TCP, HTTP | All probes down, all TCP flows expire. |

## Probe properties

Health probes have the following properties:

| Health Probe property name | Details|

| --- | --- |

| Name | Name of the health probe. This is a name you get to define for your health probe |

| Protocol | Protocol of health probe. This is the protocol type you would like the health probe to use. Options are: TCP, HTTP, HTTPS |

| Port | Port of the health probe. The destination port you would like the health probe to use when it connects to the virtual machine to check its health |

| Interval (seconds) | Interval of health probe. The amount of time (in seconds) between different probes on two consecutive health check attempts to the virtual machine |

| Threshold | Threshold of the health probe. The number of times the health probe needs to succeed or fail in order to allow or deny traffic from being delivered to the virtual machine

| Used by | List of load balancer rules using this health probe. You should have at least one rule using the health probe for it to be effective |

## Probe configuration

Health probe configuration consists of the following elements:

| Health Probe configuration | Details |

| --- | --- |

| Protocol | Protocol of health probe. This is the protocol type you would like the health probe to use. Available options are: TCP, HTTP, HTTPS |

| Port | Port of the health probe. The destination port you would like the health probe to use when it connects to the virtual machine to check the virtual machine's health status. You must ensure that the virtual machine is also listening on this port (that is, the port is open). |

| Interval | Interval of health probe. The amount of time (in seconds) between consecutive health check attempts to the virtual machine |

## Probe protocol

The protocol used by the health probe can be configured to one of the following options: TCP, HTTP, HTTPS.

| Scenario | TCP probe | HTTP/HTTPS probe |

| --- | --- | --- |

| Overview | TCP probes initiate a connection by performing a three-way open TCP handshake with the defined port. TCP probes terminate a connection with a four-way close TCP handshake. | HTTP and HTTPS issue an HTTP GET with the specified path. Both of these probes support relative paths for the HTTP GET. HTTPS probes are the same as HTTP probes with the addition of a Transport Layer Security (TLS). HTTP / HTTPS probes can be useful to implement your own logic to remove instances from load balancer if the probe port is also the listener for the service. |

| Probe failure behavior | A TCP probe fails when:</br> 1. The TCP listener on the instance doesn't respond at all during the timeout period. A probe is marked down based on the number of timed-out probe requests, which were configured to go unanswered before marking down the probe.</br> 2. The probe receives a TCP reset from the instance. | An HTTP/HTTPS probe fails when:</br> 1. Probe endpoint returns an HTTP response code other than 200 (for example, 403, 404, or 500).</br> 2. Probe endpoint doesn't respond at all during the minimum of the probe interval and 30-second timeout period. Multiple probe requests can go unanswered before the probe gets marked as not running and until the sum of all timeout intervals is reached.</br> 3. Probe endpoint closes the connection via a TCP reset.

| Probe up behavior | TCP health probes are considered healthy and mark the backend endpoint as healthy when:</br> 1. The health probe is successful once after the VM boots.</br> 2. Any backend endpoint in a healthy state is eligible for receiving new flows. | The health probe is marked up when the instance responds with an HTTP status 200 within the timeout period. HTTP/HTTPS health probes are considered healthy and mark the backend endpoint as healthy when:</br> 1. The health probe is successful once after the VM boots.</br> 2. Any backend endpoint in a healthy state is eligible for receiving new flows.

> [!NOTE]

> The HTTPS probe requires the use of certificates based that have a minimum signature hash of SHA256 in the entire chain.

## Probe down behavior

| Scenario | TCP connections | UDP datagrams |

| --- | --- | --- |

| Single instance probes down |  New TCP connections succeed to remaining healthy backend endpoint. Established TCP connections to this backend endpoint continue. |   Existing UDP flows move to another healthy instance in the backend pool.|

| All instances probe down | No new flows are sent to the backend pool. Standard Load Balancer allows established TCP flows to continue given that a backend pool has more than one backend instance. Basic Load Balancer terminates all existing TCP flows to the backend pool. |  All existing UDP flows terminate. |

## Probe interval & timeout

The interval value determines how frequently the health probe checks for a response from your backend pool instances. If the health probe fails, your backend pool instances are immediately marked as unhealthy. If the health probe succeeds on the next healthy probe up, Azure Load Balancer marks your backend pool instances as healthy. The health probe attempts to check the configured health probe port every 5 seconds by default in the Azure portal, but can be explicitly set to another value.

In order to ensure a timely response is received, HTTP/S health probes have built-in timeouts. The following are the timeout durations for TCP and HTTP/S probes:

- TCP probe timeout duration: N/A (probes will fail once the configured probe interval duration is passed and the next probe is sent)

- HTTP/S probe timeout duration: 30 seconds

For HTTP/S probes, if the configured interval is longer than the above timeout period, the health probe times out and fails if no response is received during the timeout period. For example, if an HTTP health probe is configured with a probe interval of 120 seconds (every 2 minutes), and no probe response is received within the first 30 seconds, the probe reaches its timeout period and fails. When the configured interval is shorter than the above timeout period, the health probe will fail if no response is received before the configured interval period completes and the next probe will be sent immediately.

## Probe threshold

The probe threshold value is the number of times a health probe will need to succeed or fail consecutively in order for the probe to mark a backend instance as healthy or unhealthy, respectively.

For TCP probes, if the probe threshold is configured to 2, the probe will need to receive 2 consecutive responses before a backend instance begins to receive traffic. Similarly, once a backend instance is deemed healthy, 2 consecutive failures or timeouts are required for the instance to be considered unhealthy and stop receiving new traffic.

For HTTP probes, explicit responses will immediately mark the probe as up or down for 200 and non-200 responses, and will effectively reset the threshold. This means that the threshold value only applies to HTTP probes if the probe times out due to no response.

## Design guidance

- When you design the health model for your application, probe a port on a backend endpoint that reflects the health of the instance and the application service. The application port and the probe port aren't required to be the same. In some scenarios, it can be desirable for the probe port to be different than the port your application uses but generally it's recommended that probes use the same port.

- It can be useful for your application to generate a health probe response, and signal the load balancer whether your instance should receive new connections. You can manipulate the probe response to throttle delivery of new connections to an instance by failing the health probe. You can prepare for maintenance of your application and initiate draining of connections to your application. A [probe down](#probe-down-behavior) signal always allows TCP flows to continue until idle timeout or connection closure in a Standard Load Balancer.

- For a UDP load-balanced application, generate a custom health probe signal from the backend endpoint. Use either TCP, HTTP, or HTTPS for the health probe that matches the corresponding listener.

- [HA Ports load-balancing rule](load-balancer-ha-ports-overview.md) with [Standard Load Balancer](./load-balancer-overview.md). All ports are load balanced and a single health probe response must reflect the status of the entire instance.

- Don't translate or proxy a health probe through the instance that receives the health probe to another instance in your virtual network. This configuration can lead to failures in your scenario. For example: A set of third-party appliances is deployed in the backend pool of a load balancer to provide scale and redundancy for the appliances. The health probe is configured to probe a port that the third-party appliance proxies or translates to other virtual machines behind the appliance. If you probe the same port used to translate or proxy requests to the other virtual machines behind the appliance, any probe response from a single virtual machine marks down the appliance. This configuration can lead to a cascading failure of the application. The trigger can be an intermittent probe failure that causes the load balancer to mark down the appliance instance. This action can disable your application. Probe the health of the appliance itself. The selection of the probe to determine the health signal is an important consideration for network virtual appliances (NVA) scenarios. Consult your application vendor for the appropriate health signal is for such scenarios.

- If you have multiple interfaces configured in your virtual machine, ensure you respond to the probe on the interface you received it on. You may need to source network address translate this address in the VM on a per interface basis.

- A probe definition isn't mandatory or checked for when using Azure PowerShell, Azure CLI, Templates, or API. Probe validation tests are only done when using the Azure portal.

- If the health probe fluctuates, the load balancer waits longer before it puts the backend endpoint back in the healthy state. This extra wait time protects the user and the infrastructure and is an intentional policy.

- Ensure your virtual machine instances are running. For each running instance in the backend pool, the health probe checks for availability. If an instance is stopped, it will not be probed until it has been started again.

- Don't configure your virtual network with the Microsoft owned IP address range that contains 168.63.129.16. The configuration collides with the IP address of the health probe and can cause your scenario to fail.

- To test a health probe failure or mark down an individual instance, use a [network security group](../virtual-network/network-security-groups-overview.md) to explicitly block the health probe. Create an NSG rule to block the destination port or [source IP](#probe-source-ip-address) to simulate the failure of a probe.

- Unlike load balancing rules, inbound NAT rules don't need a health probe attached to it.

- It isn't recommended to block the Azure Load Balancer health probe IP or port with NSG rules. This is an unsupported scenario and can cause the NSG rules to take delayed effect, resulting in the health probes to inaccurately represent the availability of your backend instances.

## Monitoring

[Standard Load Balancer](./load-balancer-overview.md) exposes per endpoint and backend endpoint health probe status through [Azure Monitor](./monitor-load-balancer.md). Other Azure services or partner applications can consume these metrics. Azure Monitor logs aren't supported for Basic Load Balancer.

## Probe source IP address

For Azure Load Balancer's health probe to mark up your instance, you must allow 168.63.129.16 IP address in any Azure [network security groups](../virtual-network/network-security-groups-overview.md) and local firewall policies. The `AzureLoadBalancer` service tag identifies this source IP address in your [network security groups](../virtual-network/network-security-groups-overview.md) and permits health probe traffic by default. You can learn more about this IP [here](/azure/virtual-network/what-is-ip-address-168-63-129-16).

If you don't allow the [source IP](#probe-source-ip-address) of the probe in your firewall policies, the health probe fails as it is unable to reach your instance. In turn, Azure Load Balancer marks your instance as -down- due to the health probe failure. This misconfiguration can cause your load balanced application scenario to fail. All IPv4 Load Balancer health probes originate from the IP address 168.63.129.16 as their source. IPv6 probes use a link-local address (fe80::1234:5678:9abc) as their source. For a dual-stack Azure Load Balancer, you must [configure a Network Security Group](./virtual-network-ipv4-ipv6-dual-stack-standard-load-balancer-cli.md#create-a-network-security-group-rule-for-inbound-and-outbound-connections) for the IPv6 health probe to function.

## Limitations

- HTTPS probes don't support mutual authentication with a client certificate.

- HTTP probes don't support using hostnames for probes backends.

- Enabling TCP timestamps can cause throttling or other performance issues, which can then cause health probes to time out.

- A Basic SKU load balancer health probe isn't supported with a virtual machine scale set.

- HTTP probes don't support probing on the following ports due to security concerns: 19, 21, 25, 70, 110, 119, 143, 220, 993.

## Next steps

- Learn more about [Standard Load Balancer](./load-balancer-overview.md)

- Learn [how to manage health probes](../load-balancer/manage-probes-how-to.md)

- [Get started creating a public load balancer in Resource Manager by using PowerShell](quickstart-load-balancer-standard-public-powershell.md)

- [REST API for health probes](/rest/api/load-balancer/loadbalancerprobes/)


# Admin State Overview

# Administrative State (Admin State) in Azure Load Balancer

Administrative state (Admin state) is a feature of Azure Load Balancer that allows you to override the Load Balancer's health probe behavior on a per backend pool instance basis. This feature is useful in scenarios where you would like to take down your backend instance for maintenance, patching, or testing.

## Why use admin state?

Admin state is useful in scenarios where you want to have more control over the behavior of your Load Balancer. For example, you can set the admin state to up to always consider the backend instance eligible for new connections, even if the health probe indicates otherwise. Conversely, you can set the admin state to down to prevent new connections, even if the health probe indicates that the backend instance is healthy. This can be useful for maintenance or other scenarios where you want to temporarily take a backend instance out of rotation.

## Types of admin state values

There are three types of admin state values: **Up**, **Down**, **None**. The following table describes the effects of each state on new connections and existing connections:

| **Admin State** | **New Connections** | **Existing Connections** |

|-------------|-----------------|----------------------|

| **Up**         | Load balancer ignores the health probe and always considers the backend instance as eligible for new connections. | Load balancer disregards the configured health probe's response and always allows existing connections to persist to the backend instance.|

| **Down**       | Load balancer ignores the health probe and doesn't allow new connections to the backend instance. | Load balancer ignores the health probe and existing connections are determined according to the following protocols: </br>TCP: Established TCP connections to the backend instance persists.</br>UDP: Existing UDP flows move to another healthy instance in the backend pool.</br> **Note**: This is similar to a [Probe Down behavior](load-balancer-custom-probe-overview.md#probe-down-behavior).   |

| **None**       | Load balancer respects the health probe behavior. | Load balancer respects the health probe behavior. |

> [!NOTE]

> Load Balancer Health Probe Status metrics and Load Balancer's Insights topology reflect your configured admin state value changes.

## Design considerations

When deploying a load balancer with admin state, consider the following design considerations:

1. Admin state takes effect on a per backend pool instance basis

1. In a scenario where a virtual machine instance is in more than one backend pool, the admin state applied on one backend pool doesn't affect the other backend pool.

1. In a scenario where a backend pool is part of multiple load balancing rules, the admin state applied on the backend pool affects all associated load balancing rules.

1. Admin state will only take effect when there's a health probe configured on the load balancing rules.

## Limitations

When deploying a load balancer with admin state, consider the following limitations:

1. Admin state isn't supported with inbound NAT rule.

1. Admin state isn't supported for nonprobed load balancing rules.

1. Admin state can't be configured during the creation of a NIC-based Load Balancer backend pool.

## Next steps

> [!div class="nextstepaction"]

> [Manage Administrative State in Azure Load Balancer](manage-admin-state-how-to.md)


# Skus

# Azure Load Balancer SKUs

>[!Important]

>On September 30, 2025, Basic Load Balancer was retired. For more information, see the [official announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). If you are currently using Basic Load Balancer, make sure to upgrade to Standard Load Balancer as soon as possible. For guidance on upgrading, visit [Upgrading from Basic Load Balancer - Guidance](load-balancer-basic-upgrade-guidance.md).

## <a name="skus"></a> SKU comparison

Azure Load Balancer has three stock-keeping units (SKUs) - Basic(Retired), Standard, and Gateway. Each SKU is catered towards a specific scenario and has differences in scale, features, and pricing.

To compare and understand the differences between Basic(Retired) and Standard SKU, see the following table.

| | Standard Load Balancer | Basic Load Balancer (retired) |

| --- | --- | --- |

| **Scenario** |  Equipped for load-balancing network layer traffic when high performance and ultra-low latency is needed. Routes traffic within and across regions, and to availability zones for high resiliency. | Equipped for small-scale applications that don't need high availability or redundancy. Not compatible with availability zones. |

| **Backend type** | IP based, NIC based | NIC based |

| **Protocol** | TCP, UDP | TCP, UDP |

| **Backend pool endpoints** | Any virtual machines or virtual machine scale sets in a single virtual network | Virtual machines in a single availability set or virtual machine scale set |

| **[Health probes](./load-balancer-custom-probe-overview.md#probe-protocol)** | TCP, HTTP, HTTPS | TCP, HTTP |

| **[Health probe down behavior](./load-balancer-custom-probe-overview.md#probe-down-behavior)** | TCP connections stay alive on an instance probe down __and__ on all probes down. | TCP connections stay alive on an instance probe down. All TCP connections end when all probes are down. |

| **Availability Zones** | Zone-redundant or zonal frontend IP configurations can be used for inbound and outbound traffic | Not available |

| **Type** | Internal, Public | Internal, Public |

| **Frontend IP configuration** | When using a Public Standard Load Balancer, the SKU of the public IP must be Standard. Basic Public IPs are not supported on Standard LB | When using a Public Basic Load Balancer, the SKU of the public IP must be Basic. Standard Public IPs are not supported on Basic LB |

| **Diagnostics** | [Azure Monitor multi-dimensional metrics](./load-balancer-standard-diagnostics.md) | Not supported |

| **HA Ports** | [Available for Internal Load Balancer](./load-balancer-ha-ports-overview.md) | Not available |

| **Secure by default** | Closed to inbound flows unless allowed by a network security group. Internal traffic from the virtual network to the internal load balancer is allowed. | Open by default. Network security group optional. |

| **Outbound Rules** | [Declarative outbound NAT configuration](./load-balancer-outbound-connections.md#outboundrules) | Not available |

| **TCP Reset on Idle** | [Available on any rule](./load-balancer-tcp-reset.md) | Not available |

| **[Multiple front ends](./load-balancer-multivip-overview.md)** | Inbound and [outbound](./load-balancer-outbound-connections.md) | Inbound only |

| **Management Operations** | Most operations < 30 seconds | 60-90+ seconds typical |

| **SLA** | [99.99%](https://azure.microsoft.com/support/legal/sla/load-balancer/v1_0/) | Not available |

| **Global VNet Peering Support** | Standard Internal Load Balancer is supported via Global VNet Peering | Not supported |

| **[NAT Gateway Support](../virtual-network/nat-gateway/nat-overview.md)** | Both Standard Internal Load Balancer and Standard Public Load Balancer are supported via Nat Gateway | Not supported |

| **[Private Link Support](../private-link/private-link-overview.md)** | Standard Internal Load Balancer is supported via Private Link | Not supported |

| **[Global tier](./cross-region-overview.md)** | Standard Load Balancer supports the Global tier for Public Load Balancers enabling cross-region load balancing | Not supported |

For more information, see [Load balancer limits](../azure-resource-manager/management/azure-subscription-service-limits.md#load-balancer). For Standard Load Balancer details, see [overview](./load-balancer-overview.md), [pricing](https://aka.ms/lbpricing), and [SLA](https://aka.ms/lbsla). For information on Gateway SKU - catered for third-party network virtual appliances (NVAs), see [Gateway Load Balancer overview](gateway-overview.md)

## Limitations

- A standalone virtual machine resource, availability set resource, or virtual machine scale set resource can reference one SKU, never both.

- [Move operations](../azure-resource-manager/management/move-resource-group-and-subscription.md):

- [Resource group move operations](../azure-resource-manager/management/move-support-resources.md#microsoftnetwork) (within same subscription) are **supported** for Standard Load Balancer and Standard Public IP.

- [Subscription move operations](../azure-resource-manager/management/move-support-resources.md#microsoftnetwork) are **not supported** for Standard Load Balancers.

## Next steps

- See [Create a public Standard Load Balancer](quickstart-load-balancer-standard-public-portal.md) to get started with using a Load Balancer.

- Learn about using [Standard Load Balancer and Availability Zones](load-balancer-standard-availability-zones.md).

- Learn about [Health Probes](load-balancer-custom-probe-overview.md).

- Learn about using [Load Balancer for outbound connections](load-balancer-outbound-connections.md).

- Learn about [Standard Load Balancer with HA Ports load balancing rules](load-balancer-ha-ports-overview.md).

- Learn more about [Network Security Groups](../virtual-network/network-security-groups-overview.md).


# Quickstart Load Balancer Standard Public Portal

# Quickstart: Create a public load balancer to load balance VMs using the Azure portal

Get started with Azure Load Balancer by using the Azure portal to create a public load balancer for a backend pool with two virtual machines. Other resources include Azure Bastion, NAT Gateway, a virtual network, and the required subnets.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Sign in to Azure

Sign in to the [Azure portal](https://portal.azure.com).

[!INCLUDE [load-balancer-nat-gateway](../../includes/load-balancer-nat-gateway.md)]

[!INCLUDE [load-balancer-create-bastion](../../includes/load-balancer-create-bastion.md)]

## Create load balancer

In this section, you create a zone redundant load balancer that load balances virtual machines. With zone-redundancy, one or more availability zones can fail and the data path survives as long as one zone in the region remains healthy.

During the creation of the load balancer, you configure:

* Frontend IP address

* Backend pool

* Inbound load-balancing rules

* Health probe

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

1. In the **Load balancer** page, select **+ Create**.

1. In the **Basics** tab of the **Create load balancer** page, enter or select the following information:

| Setting                 | Value                                              |

| ---                     | ---                                                |

| **Project details** |   |

| Subscription               | Select your subscription |

| Resource group         | Select **load-balancer-rg** |

| **Instance details** |   |

| Name                   | Enter **load-balancer** |

| Region         | Select **East US** |

| SKU           | Leave the default **Standard** |

| Type          | Select **Public** |

| Tier          | Leave the default **Regional** |

1. Select **Next: Frontend IP configuration** at the bottom of the page.

1. In **Frontend IP configuration**, select **+ Add a frontend IP configuration**.

1. Enter **lb-frontend** in **Name**.

1. Select **IPv4** for the **IP version**.

1. Select **IP address** for the **IP type**.

> [!NOTE]

> For more information on IP prefixes, see [Azure Public IP address prefix](../virtual-network/ip-services/public-ip-address-prefix.md).

1. Select **Create new** in **Public IP address**.

1. In **Add a public IP address**, enter **lb-frontend-ip** for **Name**.

1. Select **Zone-redundant** in **Availability zone**.

> [!NOTE]

> In regions with [Availability Zones](/azure/reliability/availability-zones-overview?toc=%2fazure%2fvirtual-network%2ftoc.json), you can select zone-redundant (default option) or a specific zone. The choice depends on your specific domain failure requirements. In regions without Availability Zones, this field won't appear.</br> For more information on availability zones, see [Availability zones overview](/azure/reliability/availability-zones-overview).

1. Leave the default of **Microsoft Network** for **Routing preference**.

1. Select **Save**.

1. Select **Save**.

1. Select **Next: Backend pools** at the bottom of the page.

1. In the **Backend pools** tab, select **+ Add a backend pool**.

1. Enter **lb-backend-pool** for **Name** in **Add backend pool**.

1. Select **lb-vnet** in **Virtual network**.

1. Select **IP Address** for **Backend Pool Configuration**.

1. Select **Save**.

1. Select **Next: Inbound rules** at the bottom of the page.

1. Under **Load balancing rule** in the **Inbound rules** tab, select **+ Add a load balancing rule**.

1. In **Add load balancing rule**, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| Name | Enter **lb-HTTP-rule** |

| IP Version | Select **IPv4** or **IPv6** depending on your requirements |

| Frontend IP address | Select **lb-frontend (To be created)** |

| Backend pool | Select **lb-backend-pool** |

| Protocol | Select **TCP** |

| Port | Enter **80** |

| Backend port | Enter **80** |

| Health probe | Select **Create new**.</br> In **Name**, enter **lb-health-probe**.</br> Select **HTTP** in **Protocol**.</br> Leave the rest of the defaults, and select **Save**. |

| Session persistence | Select **None**. |

| Idle timeout (minutes) | Enter or select **15** |

| Enable TCP reset | Select checkbox |

| Enable Floating IP | Leave unchecked |

| Outbound source network address translation (SNAT) | Leave the default of **(Recommended) Use outbound rules to provide backend pool members access to the internet.** |

1. Select **Save**.

1. Select the blue **Review + create** button at the bottom of the page.

1. Select **Create**.

> [!NOTE]

> In this example we'll create a NAT gateway to provide outbound Internet access. The outbound rules tab in the configuration is bypassed as it's optional and isn't needed with the NAT gateway. For more information on Azure NAT gateway, see [What is Azure Virtual Network NAT?](../virtual-network/nat-gateway/nat-overview.md)

> For more information about outbound connections in Azure, see [Source Network Address Translation (SNAT) for outbound connections](../load-balancer/load-balancer-outbound-connections.md)

[!INCLUDE [load-balancer-create-2-virtual-machines](../../includes/load-balancer-create-2-virtual-machines.md)]

[!INCLUDE [ephemeral-ip-note.md](~/reusable-content/ce-skilling/azure/includes/ephemeral-ip-note.md)]

## Install IIS

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **lb-VM1**.

1. On the **Overview** page, select **Connect**, then **Bastion**.

1. Enter the username and password entered during VM creation.

1. Select **Connect**.

1. On the server desktop, navigate to **Start** > **Windows PowerShell** > **Windows PowerShell**.

1. In the PowerShell Window, run the following commands to:

* Install the IIS server.

* Remove the default iisstart.htm file.

* Add a new iisstart.htm file that displays the name of the VM:

```powershell

# Install IIS server role

Install-WindowsFeature -name Web-Server -IncludeManagementTools

# Remove default htm file

Remove-Item  C:\inetpub\wwwroot\iisstart.htm

# Add a new htm file that displays server name

Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)

```

1. Close the Bastion session with **lb-VM1**.

1. Repeat steps 1 to 8 to install IIS and the updated iisstart.htm file on **lb-VM2**.

## Test the load balancer

1. In the search box at the top of the page, enter **Public IP**. Select **Public IP addresses** in the search results.

1. In **Public IP addresses**, select **frontend-ip**.

1. Copy the item in **IP address**. Paste the public IP into the address bar of your browser. The custom VM page of the IIS Web server is displayed in the browser.

## Clean up resources

When no longer needed, delete the resource group, load balancer, and all related resources. To do so, select the resource group **load-balancer-rg** that contains the resources and then select **Delete**.

## Next steps

In this quickstart, you:

* Created an Azure Load Balancer

* Attached 2 VMs to the load balancer

* Tested the load balancer

To learn more about Azure Load Balancer, continue to:

> [!div class="nextstepaction"]

> [What is Azure Load Balancer?](load-balancer-overview.md)


# Quickstart Load Balancer Standard Internal Portal

# Quickstart: Create an internal load balancer to load balance VMs using the Azure portal

Get started with Azure Load Balancer by using the Azure portal to create an internal load balancer for a backend pool with two virtual machines. Other resources include Azure Bastion, NAT Gateway, a virtual network, and the required subnets.

> [!NOTE]

> In this example, you create a NAT gateway to provide outbound Internet access. The outbound rules tab in the configuration is bypassed and isn't needed with the NAT gateway. For more information on Azure NAT gateway, see [What is Azure Virtual Network NAT?](../virtual-network/nat-gateway/nat-overview.md)

> For more information about outbound connections in Azure, see [Source Network Address Translation (SNAT) for outbound connections](../load-balancer/load-balancer-outbound-connections.md)

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Sign in to Azure

Sign in to the [Azure portal](https://portal.azure.com).

[!INCLUDE [load-balancer-nat-gateway](../../includes/load-balancer-nat-gateway.md)]

[!INCLUDE [load-balancer-create-bastion](../../includes/load-balancer-create-bastion.md)]

## Create load balancer

In this section, you create a load balancer that load balances virtual machines.

During the creation of the load balancer, you configure:

- Frontend IP address

- Backend pool

- Inbound load-balancing rules

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

1. In the **Load balancer** page, select **Create**.

1. In the **Basics** tab of the **Create load balancer** page, enter, or select the following information:

| Setting                 | Value   |

| ---                     | ---     |

| **Project details** |   |

| Subscription               | Select your subscription. |

| Resource group         | Select **load-balancer-rg**. |

| **Instance details** |   |

| Name                   | Enter **load-balancer**. |

| Region         | Select **East US**. |

| SKU           | Leave the default **Standard**. |

| Type          | Select **Internal**. |

| Tier | Leave the default of **Regional**. |

1. Select **Next: Frontend IP configuration** at the bottom of the page.

1. In **Frontend IP configuration**, select **+ Add a frontend IP configuration**, then enter or select the following information:

| Setting | Value |

| ------- | ----- |

| Name | Enter **lb-frontend**. |

| Private IP address version | Select **IPv4** or **IPv6** depending on your requirements. |

| Setting | Value |

| ------- | ----- |

| Name | Enter **lb-frontend**. |

| Virtual network | Select **lb-vnet**. |

| Subnet | Select **backend-subnet**. |

| Assignment | Select **Dynamic**. |

| Availability zone | Select **Zone-redundant**. |

1. Select **Save**.

1. Select **Next: Backend pools** at the bottom of the page.

1. In the **Backend pools** tab, select **+ Add a backend pool**.

1. Enter **lb-backend-pool** for **Name** in **Add backend pool**.

1. Select **IP Address** for **Backend Pool Configuration**.

1. Select **Save**.

1. Select the **Next: Inbound rules** button at the bottom of the page.

1. In **Load balancing rule** in the **Inbound rules** tab, select **+ Add a load balancing rule**.

1. In **Add load balancing rule**, enter or select the following information:

| **Setting** | **Value** |

| ----------- | --------- |

| Name | Enter **lb-HTTP-rule**. |

| IP Version | Select **IPv4** or **IPv6** depending on your requirements. |

| Frontend IP address | Select **lb-frontend(Dynamic)**. |

| Backend pool | Select **lb-backend-pool**. |

| Protocol | Select **TCP**. |

| Port | Enter **80**. |

| Backend port | Enter **80**. |

| Health probe | Select **Create new**.</br> In **Name**, enter **lb-health-probe**.</br> Select **TCP** in **Protocol**.</br> Leave the rest of the defaults, and select **Save**. |

| Session persistence | Select **None**. |

| Idle timeout (minutes) | Enter or select **15**. |

| Enable TCP reset | Select **checkbox**. |

| Enable Floating IP | Leave the default of unselected. |

1. Select **Save**.

1. Select the blue **Review + create** button at the bottom of the page.

1. Select **Create**.

[!INCLUDE [load-balancer-create-2-virtual-machines](../../includes/load-balancer-create-2-virtual-machines.md)]

[!INCLUDE [ephemeral-ip-note.md](~/reusable-content/ce-skilling/azure/includes/ephemeral-ip-note.md)]

## Create test virtual machine

In this section, you create a VM named **lb-TestVM**. This VM is used to test the load balancer configuration.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. In **Virtual machines**, select **+ Create** > **Azure virtual machine**.

1. In **Create a virtual machine**, enter or select the values in the **Basics** tab:

| Setting | Value                                        |

|----------------------- | ---------------------------------- |

| **Project Details** |  |

| Subscription | Select your Azure subscription. |

| Resource Group | Select **load-balancer-rg**. |

| **Instance details** |  |

| Virtual machine name | Enter **lb-TestVM**. |

| Region | Select **(US) East US**. |

| Availability Options | Select **No infrastructure redundancy required**. |

| Security type | Select **Standard**. |

| Image | Select **Windows Server 2022 Datacenter - x64 Gen2**. |

| Azure Spot instance | Leave the default of unselected. |

| Size | Choose VM size or take default setting. |

| **Administrator account** |  |

| Username | Enter a username. |

| Password | Enter a password. |

| Confirm password | Reenter password. |

| **Inbound port rules** |   |

| Public inbound ports | Select **None**. |

1. Select the **Networking** tab, or select **Next: Disks**, then **Next: Networking**.

1. In the **Networking** tab, select or enter:

| Setting | Value |

|-|-|

| **Network interface** |  |

| Virtual network | **lb-vnet**. |

| Subnet | **backend-subnet**. |

| Public IP | Select **None**. |

| NIC network security group | Select **Advanced**. |

| Configure network security group | Select **lb-NSG** created in the previous step.|

1. Select **Review + create**.

1. Review the settings, and then select **Create**.

## Install IIS

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **lb-vm1**.

1. In the **Overview** page, select **Connect**, then **Bastion**.

1. Enter the username and password entered during VM creation.

1. Select **Connect**.

1. On the server desktop, navigate to **Windows Administrative Tools** > **Windows PowerShell** > **Windows PowerShell**.

1. In the PowerShell Window, execute the following commands to:

1. Install the IIS server.

1. Remove the default iisstart.htm file.

1. Add a new iisstart.htm file that displays the name of the VM.

```powershell

# Install IIS server role

Install-WindowsFeature -name Web-Server -IncludeManagementTools

# Remove default htm file

Remove-Item  C:\inetpub\wwwroot\iisstart.htm

# Add a new htm file that displays server name

Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)

```

1. Close the Bastion session with **lb-vm1**.

1. Repeat steps 1 through 8 to install IIS and the updated iisstart.htm file on **lb-VM2**.

## Test the load balancer

In this section, you test the load balancer by connecting to the **lb-TestVM** and verifying the webpage.

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

1. Select **load-balancer**.

1. Make note or copy the address next to **Private IP address** in the **Overview** of **load-balancer**. If you can't see the **Private IP address** field, select **See more** in the information window.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **lb-TestVM**.

1. In the **Overview** page, select **Connect**, then **Bastion**.

1. Enter the username and password entered during VM creation.

1. Open **Microsoft Edge** on **lb-TestVM**.

1. Enter the IP address from the previous step into the address bar of the browser. The custom page displaying one of the backend server names is displayed on the browser. In this example, it's **10.1.0.4**.

1. To see the load balancer distribute traffic across both VMs, navigate to the VM shown in the browser message, and stop the VM.

1. Refresh the browser window. The page should still display the customized page. The load balancer is now only sending traffic to the remaining VM.

## Clean up resources

When no longer needed, delete the resource group, load balancer, and all related resources. To do so, select the resource group **load-balancer-rg** that contains the resources and then select **Delete**.

## Next steps

In this quickstart, you:

- Created an internal Azure Load Balancer

- Attached two VMs to the load balancer

- Configured the load balancer traffic rule, health probe, and then tested the load balancer

To learn more about Azure Load Balancer, continue to:

> [!div class="nextstepaction"]

> [What is Azure Load Balancer?](load-balancer-overview.md)


# Whats New

# What's new in Azure Load Balancer?

Azure Load Balancer is updated regularly. Stay up to date with the latest announcements. This article provides you with information about:

- The latest releases

- Known issues

- Bug fixes

- Deprecated functionality (if applicable)

You can also find the latest Azure Load Balancer updates and subscribe to the RSS feed on the [Azure updates page](https://azure.microsoft.com/updates?filters=%5B%22Load+Balancer%22%5D).

## Recent releases

| Type |Name |Description  |Date added  |

| ------ |---------|---------|---------|

| Feature | [Azure Load Balancer bandwidth metrics now support Protocol dimension](https://azure.microsoft.com/updates?id=536747) | Bandwidth metrics for Azure Load Balancer are now published with metric dimension Protocol. When viewing Byte, Packet, and SYN Count metrics, you can now filter by Protocol dimension where TCP traffic is denoted by Protocol=6 and UDP traffic by Protocol=17. The Protocol dimension is available in all Azure public regions, China cloud regions, and Government cloud regions. Learn more about [Azure Load Balancer supported metrics](/azure/azure-monitor/reference/supported-metrics/microsoft-network-loadbalancers-metrics). | December 2025 |

| Feature | [Azure Load Balancer health event logs generally available](https://azure.microsoft.com/updates/?id=481818) | Health event logs are now fully available in all public, Azure China, and Government regions under the Azure Monitor resource log category LoadBalancerHealthEvent, providing you with enhanced capabilities to monitor and troubleshoot your load balancer resources. Learn more about [Azure Load Balancer health overview](https://aka.ms/lbhealthoverview). | February 2025 |

| Feature | [Azure Load Balancer health status general availability](https://azure.microsoft.com/updates?id=467610) | Announcing the general availability of Azure Load Balancer Health Status, a powerful feature designed to provide detailed information about the health of backend instances in your Azure Load Balancer backend pool. The Health Status feature offers valuable insights into the state of health of your backend instances and specific reasons for their health status. Learn more about [Azure Load Balancer health status](https://go.microsoft.com/fwlink/?linkid=2296757). | November 2024 |

| Feature | [Azure Load Balancer Admin State general availability](https://azure.microsoft.com/updates?id=467625) | Admin State enables you to override the health probe behavior for each instance without additional configuration changes to your Load Balancer such as changing network security rules or closing ports. This makes management, especially during maintenance easy, allowing you to set instances as up or down and control connection behavior with no extra overhead. Learn more about [Azure Load Balancer Admin State](https://go.microsoft.com/fwlink/?linkid=2296089). | November 2024 |

| Feature | [Azure cross-subscription Load Balancer general availability](https://azure.microsoft.com/updates?id=467605) | Cross-subscription load balancing enables the load balancers components to be located in different subscriptions. For example, the frontend IP address or the backend instances could be located in a different subscription from the one that the load balancer belongs to. Learn more about [cross-subscription load balancing](https://go.microsoft.com/fwlink/?linkid=2277544). | November 2024 |

| Feature | [Azure Load Balancer health event logs public preview](https://azure.microsoft.com/updates/?id=public-preview-azure-load-balancer-health-event-logs) | By using health event logs, you can collect, store, and analyze information to help understand the health of your Azure Load Balancer resource. These built-in logs help you troubleshoot specific scenarios and allow you to identify and alert on availability issues affecting your load balancer. Learn more about [Azure Load Balancer health overview](https://aka.ms/lbhealthoverview). | May 2024 |

| Feature | [Gateway Load Balancer IPv6 support is now generally available](https://azure.microsoft.com/updates/?id=general-availability-gateway-load-balancer-ipv6-support/) | Azure Gateway Load Balancer now supports IPv6 traffic, enabling you to distribute IPv6 traffic through Gateway Load Balancer before it reaches your dual-stack applications. Now you can add IPv6 frontend IP addresses and backend pools to Gateway Load Balancer. This allows you to inspect, protect, or mirror both IPv4 and IPv6 traffic flows using third-party or custom network virtual appliances (NVAs). Both internet inbound and outbound IPv6 traffic flows can now be routed through Gateway Load Balancer. Learn more about [Gateway Load Balancer](gateway-overview.md) or our supported [third-party partners](gateway-partners.md). | September 2023 |

| Feature | [Azure’s cross-region Load Balancer is now generally available](https://azure.microsoft.com/updates/azure-s-crossregion-load-balancer-is-now-generally-available/) | Azure Load Balancer’s Global tier is a cloud-native global network load balancing solution. With cross-region Load Balancer, you can distribute traffic across multiple Azure regions with ultra-low latency and high performance. Azure cross-region Load Balancer provides customers a static globally anycast IP address. Through this global IP address, you can easily add or remove regional deployments without interruption. Learn more about [cross-region load balancer](cross-region-overview.md) | July 2023 |

| Feature | [Inbound ICMPv6 pings and traceroute are now supported on Azure Load Balancer (General Availability)](https://azure.microsoft.com/updates/general-availability-inbound-icmpv6-pings-and-traceroute-are-now-supported-on-azure-load-balancer/) | Azure Load Balancer now supports ICMPv6 pings to its frontend and inbound traceroute support to both IPv4 and IPv6 frontends. Learn more about [how to test reachability of your load balancer](load-balancer-test-frontend-reachability.md). | June 2023 |

| Feature | [Inbound ICMPv4 pings are now supported on Azure Load Balancer (General Availability)](https://azure.microsoft.com/updates/general-availability-inbound-icmpv4-pings-are-now-supported-on-azure-load-balancer/) | Azure Load Balancer now supports ICMPv4 pings to its frontend, enabling the ability to test reachability of your load balancer. Learn more about [how to test reachability of your load balancer](load-balancer-test-frontend-reachability.md). | May 2023 |

| SKU | [Basic Load Balancer is retiring on September 30, 2025](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/) | Basic Load Balancer will retire on 30 September 2025. Make sure to [migrate to Standard SKU](load-balancer-basic-upgrade-guidance.md) before this date. | September 2022 |

| SKU | [Gateway Load Balancer now generally available](https://azure.microsoft.com/updates/generally-available-azure-gateway-load-balancer/) | Gateway Load Balancer is a new SKU of Azure Load Balancer targeted for scenarios requiring transparent NVA (network virtual appliance) insertion. Learn more about [Gateway Load Balancer](gateway-overview.md) or our supported [third party partners](gateway-partners.md). | July 2022 |

| SKU | [Gateway Load Balancer public preview](https://azure.microsoft.com/updates/gateway-load-balancer-preview/) | Gateway Load Balancer is a fully managed service enabling you to deploy, scale, and enhance the availability of third party network virtual appliances (NVAs) in Azure. You can add your favorite third party appliance whether it's a firewall, inline DDoS appliance, deep packet inspection system, or even your own custom appliance into the network path transparently – all with a single action.| November 2021 |

| Feature | [Support for IP-based backend pools (General Availability)](https://azure.microsoft.com/updates/iplbga/) | Azure Load Balancer supports adding and removing resources from a backend pool via an IPv4 or IPv6 addresses. This enables easy management of containers, virtual machines, and Virtual Machine Scale Sets associated with Load Balancer. It will also allow IP addresses to be reserved as part of a backend pool before the associated resources are created. Learn more about [backend pool management](backend-pool-management.md)|March 2021 |

| Feature | [Instance Metadata support for Standard SKU Load Balancers and Public IPs](https://azure.microsoft.com/updates/standard-load-balancer-and-ip-addresses-metadata-now-available-through-azure-instance-metadata-service-imds/)|Metadata of Standard Public IP addresses  and Standard Load Balancer can now be retrieved through Azure Instance Metadata Service (IMDS). The metadata is available from within the running instances of virtual machines (VMs) and Virtual Machine Scale Sets instances. You can use the metadata to manage your virtual machines. Learn more about [Instance Metadata Service for Load Balancer](instance-metadata-service-load-balancer.md)| February 2021 |

| Feature | [Public IP SKU upgrade from Basic to Standard without losing IP address](https://azure.microsoft.com/updates/public-ip-sku-upgrade-generally-available/) | As you move from Basic to Standard Load Balancers, retain your public IP address. Learn more about [upgrading a public IP address](../virtual-network/ip-services/public-ip-upgrade-portal.md)| January 2021|

| Feature | Support for moves across resource groups | Standard Load Balancer and Standard Public IP support for [resource group moves](https://azure.microsoft.com/updates/standard-resource-group-move/). | October 2020 |

| Feature | [Cross-region load balancing with Global tier on Standard LB](https://azure.microsoft.com/updates/preview-azure-load-balancer-now-supports-crossregion-load-balancing/) | Azure Load Balancer supports Cross Region Load Balancing. Previously, Standard Load Balancer had a regional scope. With this release, you can load balance across multiple Azure regions via a single, static, global anycast Public IP address. | September 2020 |

| Feature| Azure Load Balancer Insights using Azure Monitor | Built as part of Azure Monitor for Networks, customers now have topological maps for all their Load Balancer configurations and health dashboards for their Standard Load Balancers preconfigured with metrics in the Azure portal. [Get started and learn more](https://azure.microsoft.com/blog/introducing-azure-load-balancer-insights-using-azure-monitor-for-networks/) | June 2020 |

| Validation | Addition of validation for HA ports | A validation was added to ensure that HA port rules and non HA port rules are only configurable when Floating IP is enabled. Previously, this configuration would go through, but not work as intended. No change to functionality was made. You can learn more about [HA ports limitations](load-balancer-ha-ports-overview.md#limitations)| June 2020 |

| Feature| IPv6 support for Azure Load Balancer (generally available) | You can have IPv6 addresses as your frontend for your Azure Load Balancers. Learn how to [create a dual stack application here](./virtual-network-ipv4-ipv6-dual-stack-standard-load-balancer-powershell.md) |April 2020|

| Feature| TCP Resets on Idle Timeout (generally available)| Use TCP resets to create a more predictable application behavior. [Learn more](load-balancer-tcp-reset.md)| February 2020 |

## Blog posts

Stay informed with the latest insights, tutorials, and deep-dive blogs from the Azure Load Balancer team and community:

| Title | Description | Date |

|-------|-------------|------|

| [Accelerate designing, troubleshooting & securing your network with Gen-AI powered tools, now GA](https://techcommunity.microsoft.com/blog/azurenetworkingblog/accelerate-designing-troubleshooting--securing-your-network-with-gen-ai-powered-/4402527) | Learn how to leverage Gen-AI powered tools to accelerate network design, troubleshooting, and security for Azure Load Balancer and other networking services. | June 2025 |

| [A Guide to Azure Data Transfer Pricing](https://techcommunity.microsoft.com/blog/azurenetworkingblog/a-guide-to-azure-data-transfer-pricing/4374538) | Comprehensive guide to understanding data transfer costs and pricing models for Azure Load Balancer and related networking services. | May 2025 |

| [Announcing the General Availability of Azure Load Balancer Health Event Logs](https://techcommunity.microsoft.com/blog/azurenetworkingblog/announcing-the-general-availability-of-azure-load-balancer-health-event-logs/4389063) | Deep dive into the new health event logs feature for enhanced monitoring and troubleshooting capabilities. | March 2025 |

| [How to build highly resilient applications with Azure Load Balancer](https://techcommunity.microsoft.com/blog/azurenetworkingblog/how-to-build-highly-resilient-applications-with-azure-load-balancer/4359370) | Best practices and architectural patterns for building resilient applications using Azure Load Balancer. | December 2024 |

| [Introducing Azure Copilot for Networking: Your AI-Powered Azure Networking Assistant](https://techcommunity.microsoft.com/blog/azurenetworkingblog/introducing-copilot-in-azure-for-networking-your-ai-powered-azure-networking-ass/4298663) | Discover how AI-powered assistance can help manage and optimize your Azure Load Balancer configurations. | December 2024 |

| [Troubleshoot health probe failures with Azure Load Balancer Health Status](https://techcommunity.microsoft.com/blog/azurenetworkingblog/troubleshoot-health-probe-failures-with-azure-load-balancer-health-status/4287244) | Step-by-step guide to diagnosing and resolving health probe issues using the Health Status feature. | October 2024 |

| [Routing options for VMs from Private Subnets](https://techcommunity.microsoft.com/blog/azurenetworkingblog/routing-options-for-vms-from-private-subnets/4271244) | Explore different routing strategies for VMs in private subnets when using Azure Load Balancer. | October 2024 |

| [Using Admin State to Control Your Azure Load Balancer Backend Instances](https://techcommunity.microsoft.com/blog/azurenetworkingblog/using-admin-state-to-control-your-azure-load-balancer-backend-instances/4155457) | Practical guide to using the Admin State feature for easier maintenance and instance management. | August 2024 |

| [Build scalable cross-subscription applications with Azure Load Balancer](https://techcommunity.microsoft.com/blog/azurenetworkingblog/build-scalable-cross-subscription-applications-with-azure-load-balancer/4167505) | Learn how to architect applications that span multiple subscriptions using Azure Load Balancer. | June 2024 |

> [!TIP]

> Subscribe to the [Azure Networking blog](https://techcommunity.microsoft.com/category/azure/blog/azurenetworkingblog) to receive notifications about new Load Balancer articles and updates.

## Retirements

| Name |Description  | Retirement Date  |

|---------|---------|---------|

| [Azure Load Balancer numberOfProbes property](https://azure.microsoft.com/updates/?id=end-of-support-announcement-for-azure-load-balancer-numberofprobes-property-on-1-september-2027) | Support for [Azure Load Balancer numberOfProbes property](https://aka.ms/VersionHowTo) ends on September 1, 2027. To avoid service disruption, upgrade your apps to API version 2022-05-01 or higher and start using Azure Load Balancer probeThreshold property. We will not be supporting the property numberOfProbes after September 1, 2027. | September 2027 |

| [Inbound NAT rule V1 for Azure Virtual Machines and Azure Virtual Machine Scale Sets](https://azure.microsoft.com/updates/?id=retirement-notice-azure-load-balancer-inbound-nat-rule-v1-for-azure-vms-and-azure-vmss-will-be-retired) | On September 30, 2027, Inbound NAT rule V1 for Azure Virtual Machines and Azure Virtual Machine Scale Sets in Azure Load Balancer will be retired. To avoid service disruptions, you’ll need to [migrate](https://go.microsoft.com/fwlink/?linkid=2286671) to Inbound NAT rule V2 by that date. | September 2027 |

| [Azure Basic Load Balancer](https://azure.microsoft.com/updates/?id=azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer) | On 30 September 2025, Azure Basic Load Balancer will be [retired](https://aka.ms/lbbasictostandard). You can continue to use your existing Basic Load Balancers until then, but you'll no longer be able to deploy new ones after 31 March 2025. | September 2025 |

## Known issues

The following are known issues and limitations that may affect your deployment. Where a resolution is in progress, it is noted. For issues without a planned resolution, recommended mitigations are provided.

|Issue |Description  |Mitigation  |

| ---------- |---------|---------|

| IP-based Load Balancer outbound IP | IP-based Load Balancers are currently not secure-by-default and will use the backend instances' default outbound access IPs for outbound connections. If the Load Balancer is a public Load Balancer, either the default outbound access IPs or the Load Balancer's frontend IP may be used. | In order to prevent backend instances behind an IP-based Load Balancer from using default outbound access, use NAT Gateway for a predictable IP address and to prevent SNAT port exhaustion, or use the private subnet feature to secure your Load Balancer. |

| numberOfProbes, "Unhealthy threshold" | Health probe configuration property numberOfProbes, otherwise known as "Unhealthy threshold" in Portal, isn't respected. Load Balancer health probes will probe up/down immediately after one probe regardless of the property's configured value. | To control the number of successful or failed consecutive probes necessary to mark backend instances as healthy or unhealthy, use the property ["probeThreshold"](/azure/templates/microsoft.network/loadbalancers?pivots=deployment-language-arm-template#probepropertiesformat-1) instead. |

## Next steps

For more information about Azure Load Balancer, see [What is Azure Load Balancer?](load-balancer-overview.md) and [frequently asked questions](load-balancer-faqs.yml).


# Manage

# Azure Load Balancer portal settings

As you create Azure Load Balancer, information in this article helps you learn more about the individual settings and what the right configuration is for you.

## Create load balancer

Azure Load Balancer is a network load balancer that distributes traffic across VM instances in the backend pool.

To create a load balancer in the portal, at the top of the page select the search box. Enter **Load balancer**. Select **Load balancers** in the search results. Select **+ Create** in the **Load balancers** page.

### Basics

In the **Basics** tab of the create load balancer portal page, you see the following information:

| Setting |  Details |

| ---------- | ---------- |

| Subscription  | Select your subscription. This selection is the subscription you want your load balancer to be deployed in. |

| Resource group | Select **Create new** and type in the name for your resource group in the text box. If you have an existing resource group created, select it. |

| Name | This setting is the name for your Azure Load Balancer. |

| Region | Select an Azure region you'd like to deploy your load balancer in. |

| SKU  | Select **Standard**. </br> Load balancer has three SKUs: </br> **Basic** </br>**Standard** </br> **Gateway**. </br> Basic has limited functionality. </br> Standard is recommended for production workloads. </br> Gateway caters to non-Microsoft network virtual appliances (NVAs) </br> Learn more about [SKUs](skus.md). |

| Type | Load balancer has two types: </br> **Internal (Private)** </br> **Public (External)**.</br> An internal load balancer (ILB) routes traffic to backend pool members via a private IP address.</br> A public load balancer directs requests from clients over the internet to the backend pool.</br> Learn more about [load balancer types](components.md#frontend-ip-configuration-).|

| Tier | Load balancer has two tiers: </br> **Regional** </br> **Global** </br> A regional load balancer is constrained to load balancing within a region. Global refers to a cross-region load balancer that load-balances across regions. </br> For more information on the **Global** tier, see [Cross-region load balancer (preview)](cross-region-overview.md)

### Frontend IP configuration

In the **Frontend IP configuration** tab of the create load balancer portal page, select **+ Add a frontend IP configuration** to open the creation page.

#### **Add frontend IP configuration**

##### Public load balancer

If you select **Public** as your load balancer type in the **Basics** tab, you see the following information:

| Setting | Details |

| ------- | ------- |

| Name | The name of the frontend added to the load balancer. |

| IP version | **IPv4** </br> **IPv6** </br> Load balancer supports IPv4 and IPv6 frontends. </br> Learn more about [load Balancer and IPv6](load-balancer-ipv6-overview.md). |

| IP type | **IP address** </br> **IP prefix** </br> Load balancer supports an IP address or an IP prefix for the frontend IP address. For more information, see [Azure Public IP address prefix](../virtual-network/ip-services/public-ip-address-prefix.md). |

| Gateway Load Balancer | If you're using a Gateway Load Balancer, choose the **Azure Resource Manager ID** of the Gateway Load Balancer you want to chain to your frontend IP Configuration. |

###### IP address

If you select **IP address** for **IP type**, you see the following information:

| Setting | Details |

| ------- | ------- |

| Public IP address | Select **Create new** to create a public IP address for your public load balancer. </br> If you have an existing public IP, select it in the pull-down box. |

| Name | The name of the public IP address resource. |

| SKU | Public IP addresses have two SKUs: **Basic** and **Standard**. </br> Basic doesn't support zone-resiliency and zonal attributes. </br> **Standard** is recommended for production workloads. </br> Load balancer and public IP address SKUs **must match**. |

| Tier | **Regional** </br> **Global** </br> Depending on type of load balancer tier determines what is selected. Regional for traditional load balancer, global for cross-region. |

| Assignment | **Static** is auto selected for standard. </br> Basic public IPs have two types: **Dynamic** and **Static**. </br> Dynamic public IP addresses aren't assigned until creation. </br> IPs can be lost if the resource is deleted. </br> Static IP addresses are recommended. |

| Availability zone | Select **Zone-redundant** to create a resilient load balancer. </br> To create a zonal load balancer, select a specific zone from **1**, **2**, or **3**. </br> Standard load balancer and public IPs support zones. </br> Learn more about [load balancer and availability zones](load-balancer-standard-availability-zones.md). </br> You won't see zone selection for basic. Basic load balancer doesn't support zones. |

| Routing preference | Select **Microsoft Network**. </br> Microsoft Network means that traffic is routed via the Microsoft global network. </br> Internet means that traffic is routed through the internet service provider network. </br> Learn more about [Routing Preferences](../virtual-network/ip-services/routing-preference-overview.md)|

###### IP Prefix

If you select **IP prefix** for **IP type**, you see the following information:

| Setting | Details |

| ------- | ------- |

| Public IP prefix | Select **Create new** to create a public IP prefix for your public load balancer. </br> If you have an existing public prefix, select it in the pull-down box. |

| Name | The name of the public IP prefix resource. |

| SKU | Public IP prefixes have one SKU, **Standard**. |

| IP version | **IPv4** or **IPv6**. </br> The version displayed corresponds to the version chosen. |

| Prefix size | IPv4 or IPv6 prefixes are displayed depending on the selection above. </br> **IPv4** </br> /24 (256 addresses) </br> /25 (128 addresses) </br> /26 (64 addresses) </br> /27 (32 addresses) </br> /28 (16 addresses) </br> /29 (8 addresses) </br> /30 (4 addresses) </br> /31 (2 addresses) </br> **IPv6** </br> /124 (16 addresses) </br> /125 (8 addresses) </br> 126 (4 addresses) </br> 127 (2 addresses) |

| Availability zone | Select **Zone-redundant** to create a resilient load balancer. </br> To create a zonal load balancer, select a specific zone from **1**, **2**, or **3**. </br> Standard load balancer and public IP prefixes support zones. </br> Learn more about [load balancer and availability zones](load-balancer-standard-availability-zones.md).

##### Internal load balancer

If you select **Internal** as your load balancer type in the **Basics** tab, you see the following information:

| Setting |  Details |

| ---------- | ---------- |

| Virtual network | The virtual network your internal load balancer will connect to. </br> The private frontend IP address you select for your internal load balancer is from this virtual network. |

| Subnet | The subnets available for the IP address of the frontend IP are displayed here. |

| Assignment | Your options are **Static** or **Dynamic**. </br> Static ensures the IP doesn't change. A dynamic IP could change. |

| Availability zone | Your options are: </br> **Zone redundant** </br> **Zone 1** </br> **Zone 2** </br> **Zone 3** </br> To create a load balancer that is highly available and resilient to availability zone failures, select a **zone-redundant** IP. |

### Backend pools

In the **Backend pools** tab of the create load balancer portal page, select **+ Add a backend pool** to open the creation page.

#### **Add backend pool**

The following is displayed in the **Add backend pool** creation page:

| Setting | Details |

| ---------- |  ---------- |

| Name | The name of your backend pool. |

| Virtual network | The virtual network your backend instances are. |

| Backend pool configuration | Your options are: </br> **NIC** </br> **IP address** </br> NIC configures the backend pool to use the network interface card of the virtual machines. </br> IP address configures the backend pool to use the IP address of the virtual machines. </br> For more information on backend pool configuration, see [Backend pool management](backend-pool-management.md).

##### NIC backend pool configuration

You can add virtual machines or Virtual Machine Scale Sets to the backend pool of your Azure Load Balancer. Create the virtual machines or Virtual Machine Scale Sets first.

Under **IP configurations**, select **+ Add** to choose your IP configurations.

In **Add IP configuration to backend pool** page, select the virtual machine or Virtual Machine Scale Set resources, and select **Add** and **Save**.

### Inbound rules

There are two sections in the **Inbound rules** tab, **Load balancing rule** and **Inbound NAT rule**.

In the **Inbound rules** tab of the create load balancer portal page, select **+ Add a load balancing rule** to open the creation page.

#### **Add load balancing rule**

The following is displayed in the **Add load balancing rule** creation page:

| Setting | Details |

| ---------- | ---------- |

| Name | The name of the load balancer rule. |

| IP Version | Your options are **IPv4** or **IPv6**.  |

| Frontend IP address | Select the frontend IP address. </br> The frontend IP address of your load balancer you want the load balancer rule associated to.|

| Backend pool | The backend pool you would like this load balancer rule to be applied on. |

| HA Ports | This setting enables load balancing on all TCP and UDP ports. |

| Protocol | Azure Load Balancer is a layer 4 network load balancer. </br> Your options are: **TCP** or **UDP**. |

| Port | This setting is the port associated with the frontend IP that you want traffic to be distributed based on this load-balancing rule. |

| Backend port | This setting is the port on the instances in the backend pool you would like the load balancer to send traffic to. This setting can be the same as the frontend port or different if you need the flexibility for your application. |

| Health probe | Select **Create new**, to create a new probe.  </br> Only healthy instances receive new traffic. |

| Session persistence |  Your options are: </br> **None** </br> **Client IP** </br> **Client IP and protocol**</br> </br> Maintain traffic from a client to the same virtual machine in the backend pool. This traffic is maintained during the session. </br> **None** specifies that successive requests from the same client can be handled by any virtual machine. </br> **Client IP** specifies that successive requests from the same client IP address are handled by the same virtual machine. </br> **Client IP and protocol** ensure that successive requests from the same client IP address and protocol are handled by the same virtual machine. </br> Learn more about [distribution modes](load-balancer-distribution-mode.md). |

| Idle timeout (minutes) | Keep a **TCP** or **HTTP** connection open without relying on clients to send keep-alive messages |

| TCP reset | Load balancer can send **TCP resets** to help create a more predictable application behavior on when the connection is idle. </br> Learn more about [TCP reset](load-balancer-tcp-reset.md)|

| Floating IP | Floating IP is Azure's terminology for a portion of what is known as **Direct Server Return (DSR)**. </br> DSR consists of two parts: <br> 1. Flow topology </br> 2. An IP address-mapping scheme at a platform level. </br></br> Azure Load Balancer always operates in a DSR flow topology whether floating IP is enabled or not. </br> This operation means that the outbound part of a flow is always correctly rewritten to flow directly back to the origin. </br> Without floating IP, Azure exposes a traditional load-balancing IP address-mapping scheme, the VM instances' IP. </br> Enabling floating IP changes the IP address mapping to the frontend IP of the load Balancer to allow for more flexibility. </br> For more information, see [Multiple frontends for Azure Load Balancer](load-balancer-multivip-overview.md).|

#### Create health probe

If you selected **Create new** in the health probe configuration of the load-balancing rule above, the following options are displayed:

| Setting | Details |

| ---------- | ---------- |

| Name | The name of your health probe. |

| Protocol | The protocol you select determines the type of check used to determine if the backend instance(s) are healthy. </br> Your options are: </br> **TCP** </br> **HTTPS** </br> **HTTP** </br> Ensure you're using the right protocol. This selection depends on the nature of your application. </br> The configuration of the health probe and probe responses determines which backend pool instances receive new flows. </br> You can use health probes to detect the failure of an application on a backend endpoint. </br> Learn more about [health probes](load-balancer-custom-probe-overview.md). |

| Port | The destination port for the health probe. </br> This setting is the port on the backend instance the health probe uses to determine the instance's health. |

| Interval | The number of seconds in between probe attempts. </br> The interval determines how frequently the health probe attempts to reach the backend instance. </br> If you select 5, the second probe attempt is made after 5 seconds and so on. |

In the **Inbound rules** tab of the create load balancer portal page, select **+ Add an inbound NAT rule** to open the creation page.

#### **Add an inbound NAT rule**

Inbound NAT rules can be configured for traffic sent to an individual virtual machines or a set of machines in a backend pool. Each destination resource has specific creation settings on the creation page

##### Azure Virtual Machine

The following is displayed in the **Add an inbound NAT rule** creation page for an **Azure virtual machine**:

| Setting | Details |

| ---------- | ---------- |

| Name | The name of your inbound NAT rule |

| Type | Select **Azure virtual machine** or **Backend pool**. Inbound NAT rules can be configured by sending traffic to an individual VM or a set of machines in a backend pool.|

| Target virtual machine | Select the name of the Azure Virtual Machine this rule applies to from the available VMs in the dropdown list. |

| Frontend IP address | Select the frontend IP address. </br> The frontend IP address of your load balancer you want the inbound NAT rule associated to. |

| Frontend Port | This setting is the port associated with the frontend IP that you want traffic to be distributed based on this inbound NAT rule. |

| Service Tag | Enter a service tag to use for your rule. The frontend port value is populated based on Service Tag chosen. |

| Backend port | Enter a port for traffic sent to the backend virtual machine. |

| Protocol | Azure Load Balancer is a layer 4 network load balancer. </br> Your options are: TCP or UDP. |

| Enable TCP Reset | Load Balancer can send TCP resets to help create a more predictable application behavior on when the connection is idle. </br> Learn more about [TCP reset](load-balancer-tcp-reset.md) |

| Idle timeout (minutes) | Keep a TCP or HTTP connection open without relying on clients to send keep-alive messages. |

| Enable Floating IP | Some application scenarios prefer or require the same port to be used by multiple application instances on a single VM in the backend pool. If you want to reuse the backend port across multiple rules, you must enable [Floating IP](load-balancer-floating-ip.md) in the rule definition.|

##### Backend pool

The following is displayed in the **Add an inbound NAT rule** creation page for a **Backend pool**:

| Setting | Details |

| ---------- | ---------- |

| Name | The name of your inbound NAT rule |

| Type | Select **Azure virtual machine** or **Backend pool**. Inbound NAT rules can be configured by sending traffic to an individual VM or a set of machines in a backend pool.|

|Target backend pool | Select the backend pool this rule applies to from the dropdown menu. |

| Frontend IP address | Select the frontend IP address. </br> The frontend IP address of your load balancer you want the inbound NAT rule associated to. |

| Frontend port range start | Enter the starting port of a range of frontend ports pre-allocated for the specific backend pool. |

| Current number of machines in backend pool | The displayed value is the number of machines in the selected backend pool, and for information only; you can't modify this value. |

| Maximum number of machines in backend pool | Enter the maximum number of instances in the backend pool when scaling out. |

| Backend port | Enter a port for traffic sent to on backend pool. |

| Protocol | Azure Load Balancer is a layer 4 network load balancer. </br> Your options are: TCP or UDP. |

| Enable TCP Reset | Load Balancer can send TCP resets to help create a more predictable application behavior on when the connection is idle. </br> Learn more about [TCP reset](load-balancer-tcp-reset.md) |

| Idle timeout (minutes) | Keep a TCP or HTTP connection open without relying on clients to send keep-alive messages. |

| Enable Floating IP | Some application scenarios prefer or require the same port to be used by multiple application instances on a single VM in the backend pool. If you want to reuse the backend port across multiple rules, you must enable [Floating IP](load-balancer-floating-ip.md) in the rule definition.|

### Outbound rules

In the **Outbound rules** tab of the create load balancer portal page, select **+ Add an outbound rule** to open the creation page.

> [!NOTE]

> The outbound rules tab is only valid for a public standard load balancer. Outbound rules are not supported on an internal or basic load balancer. Azure Virtual Network NAT is the recommended way to provide outbound internet access for the backend pool. For more information on **Azure Virtual Network NAT** and the NAT gateway resource, see **[What is Azure Virtual Network NAT?](../virtual-network/nat-gateway/nat-overview.md)**.

#### **Add an outbound rule**

The following is displayed in the **Add outbound rule** creation page:

| Setting | Details |

| ------- | ------ |

| Name | The name of your outbound rule. |

| IP Version | Your options are **IPv4** or **IPv6**. |

| Frontend IP address | Select the frontend IP address. </br> The frontend IP address of your load balancer you want the outbound rule to be associated to. |

| Protocol | Azure Load Balancer is a layer 4 network load balancer. </br> Your options are: **All**, **TCP**, or **UDP**. |

| Idle timeout (minutes) | Keep a **TCP** or **HTTP** connection open without relying on clients to send keep-alive messages. |

| TCP Reset | Load balancer can send **TCP resets** to help create a more predictable application behavior on when the connection is idle. </br> Learn more about [TCP reset](load-balancer-tcp-reset.md) |

| Backend pool | The backend pool you would like this outbound rule to be applied on. |

| **Port allocation** |   |

| Port allocation | Your choices are: </br> **Manually choose number of outbound ports** </br> **Use the default number of outbound ports** </br> The recommended selection is the default of **Manually choose number of outbound ports** to prevent SNAT port exhaustion. If **Use the default number of outbound ports** is chosen, the **Outbound ports** selection is disabled. |

| Outbound ports | Your choices are: </br> **Ports per instance** </br> **Maximum number of backend instances**. </br> The recommended selections are select **Ports per instance** and enter **10,000**. |

## Portal settings

### Frontend IP configuration

The IP address of your Azure Load Balancer. It's the point of contact for clients.

You can have one or many frontend IP configurations. If you went through the create section in this article, you created a frontend for your load balancer.

If you want to add a frontend IP configuration to your load balancer, go to your load balancer in the Azure portal, select **Frontend IP configuration**, and then select **+Add**.

| Setting |  Details |

| ---------- | ---------- |

| Name | The name of your frontend IP configuration. |

| IP version | Your options are **IPv4** and **IPv6**. </br> Load balancer supports both IPv4 and IPv6 frontend IP configurations. |

| IP type | IP type determines if a single IP address is associated with your frontend or a range of IP addresses using an IP Prefix. </br> A [public IP prefix](../virtual-network/ip-services/public-ip-address-prefix.md) assists when you need to connect to the same endpoint repeatedly. The prefix ensures enough ports are given to assist with SNAT port issues. |

| Public IP address (or Prefix if you selected prefix above) | Select or create a new public IP (or prefix) for your load balancer frontend. |

### Backend pools

A backend address pool contains the IP addresses of the virtual network interfaces in the backend pool.

If you want to add a backend pool to your load balancer, go to your load balancer in the Azure portal, select **Backend pools**, and then select **+Add**.

| Setting | Details |

| ---------- |  ---------- |

| Name | The name of your backend pool. |

| Virtual network | The virtual network your backend instances are. |

| Backend Pool Configuration | Your options are: </br> **NIC** </br> **IP address** </br> NIC configures the backend pool to use the network interface card of the virtual machines. </br> IP address configures the backend pool to use the IP address of the virtual machines. </br> Learn more about [Backend pool management](backend-pool-management.md). |

| IP version | Your options are **IPv4** or **IPv6**. |

You can add virtual machines or Virtual Machine Scale Sets to the backend pool of your Azure Load Balancer. Create the virtual machines or Virtual Machine Scale Sets first. Next, add them to the load balancer in the portal.

### Health probes

A health probe is used to monitor the status of your backend VMs or instances. The health probe status determines when new connections are sent to an instance based on health checks.

If you want to add a health probe to your load balancer, go to your load balancer in the Azure portal, select **Health probes**, then select **+Add**.

| Setting | Details |

| ---------- | ---------- |

| Name | The name of your health probe. |

| Protocol | The protocol you select determines the type of check used to determine if the backend instance(s) are healthy. </br> Your options are: </br> **TCP** </br> **HTTPS** </br> **HTTP** </br> Ensure you're using the right protocol. This selection depends on the nature of your application. </br> The configuration of the health probe and probe responses determines which backend pool instances receive new flows. </br> You can use health probes to detect the failure of an application on a backend endpoint. </br> Learn more about [health probes](load-balancer-custom-probe-overview.md). |

| Port | The destination port for the health probe. </br> This setting is the port on the backend instance the health probe uses to determine the instance's health. |

| Interval | The number of seconds in between probe attempts. </br> The interval determines how frequently the health probe attempts to reach the backend instance. </br> If you select 5, the second probe attempt is made after 5 seconds and so on. |

| Unhealthy threshold | The number of consecutive probe failures that must occur before a VM is considered unhealthy.</br> If you select 2, no new flows are sent to this backend instance after two consecutive failures. |

### Load-balancing rules

Defines how incoming traffic is distributed to all the instances within the backend pool. A load-balancing rule maps a given frontend IP configuration and port to multiple backend IP addresses and ports.

If you want to add a load balancer rule to your load balancer, go to your load balancer in the Azure portal, select **Load-balancing rules**, and then select **+Add**.

| Setting | Details |

| ---------- | ---------- |

| Name | The name of the load balancer rule. |

| IP Version | Your options are **IPv4** or **IPv6**.  |

| Frontend IP address | Select the frontend IP address. </br> The frontend IP address of your load balancer you want the load balancer rule associated to.|

| Protocol | Azure Load Balancer is a layer 4 network load balancer. </br> Your options are: **TCP** or **UDP**. |

| Port | This setting is the port associated with the frontend IP that you want traffic to be distributed based on this load-balancing rule. |

| Backend port | This setting is the port on the instances in the backend pool you would like the load balancer to send traffic to. This setting can be the same as the frontend port or different if you need the flexibility for your application. |

| Backend pool | The backend pool you would like this load balancer rule to be applied on. |

| Health probe | The health probe you created to check the status of the instances in the backend pool. </br> Only healthy instances receive new traffic. |

| Session persistence |  Your options are: </br> **None** </br> **Client IP** </br> **Client IP and protocol**</br> </br> Maintain traffic from a client to the same virtual machine in the backend pool. This traffic is maintained during the session. </br> **None** specifies that successive requests from the same client can be handled by any virtual machine. </br> **Client IP** specifies that successive requests from the same client IP address are handled by the same virtual machine. </br> **Client IP and protocol** ensure that successive requests from the same client IP address and protocol are handled by the same virtual machine. </br> Learn more about [distribution modes](load-balancer-distribution-mode.md). |

| Idle timeout (minutes) | Keep a **TCP** or **HTTP** connection open without relying on clients to send keep-alive messages |

| TCP reset | Load balancer can send **TCP resets** to help create a more predictable application behavior on when the connection is idle. </br> Learn more about [TCP reset](load-balancer-tcp-reset.md)|

| Floating IP | Floating IP is Azure's terminology for a portion of what is known as **Direct Server Return (DSR)**. </br> DSR consists of two parts: <br> 1. Flow topology </br> 2. An IP address-mapping scheme at a platform level. </br></br> Azure Load Balancer always operates in a DSR flow topology whether floating IP is enabled or not. </br> This operation means that the outbound part of a flow is always correctly rewritten to flow directly back to the origin. </br> Without floating IP, Azure exposes a traditional load-balancing IP address-mapping scheme, the VM instances' IP. </br> Enabling floating IP changes the IP address mapping to the frontend IP of the load Balancer to allow for more flexibility. </br> For more information, see [Multiple frontends for Azure Load Balancer](load-balancer-multivip-overview.md).|

| Outbound source network address translation (SNAT) | Your options are: </br> **(Recommended) Use outbound rules to provide backend pool members access to the internet.** </br> **Use implicit outbound rule. This is not recommended because it can cause SNAT port exhaustion.** </br> Select the **Recommended** option to prevent SNAT port exhaustion. A **NAT gateway** or **Outbound rules** are required to provide SNAT for the backend pool members. For more information on **NAT gateway**, see [What is Virtual Network NAT?](../virtual-network/nat-gateway/nat-overview.md) </br> For more information on outbound connections in Azure, see [Using Source Network Address Translation (SNAT) for outbound connections](load-balancer-outbound-connections.md). |

### Inbound NAT rules

An inbound NAT rule forwards incoming traffic sent to frontend IP address and port combination.

The traffic is sent to a specific virtual machine or instance in the backend pool. Port forwarding is done by the same hash-based distribution as load balancing.

If your scenario requires Remote Desktop Protocol (RDP) or Secure Shell (SSH) sessions to separate VM instances in a backend pool. Multiple internal endpoints can be mapped to ports on the same frontend IP address.

The frontend IP addresses can be used to remotely administer your VMs without an extra jump box.

If you want to add an inbound nat rule to your load balancer, go to your load balancer in the Azure portal, select **Inbound NAT rules**, and then select **+Add**.

| Setting | Details |

| ---------- | ---------- |

| Name | The name of your inbound NAT rule |

| Frontend IP address | Select the frontend IP address. </br> The frontend IP address of your load balancer you want the inbound NAT rule associated to. |

| IP Version | Your options are **IPv4** and **IPv6**. |

| Service | The type of service you're running on Azure Load Balancer. </br> A selection here updates the port information appropriately. |

| Protocol | Azure Load Balancer is a layer 4 network load balancer. </br> Your options are: TCP or UDP. |

| Idle timeout (minutes) | Keep a TCP or HTTP connection open without relying on clients to send keep-alive messages. |

| TCP Reset | Load Balancer can send TCP resets to help create a more predictable application behavior on when the connection is idle. </br> Learn more about [TCP reset](load-balancer-tcp-reset.md) |

| Port | This setting is the port associated with the frontend IP that you want traffic to be distributed based on this inbound NAT rule. |

| Target virtual machine | The virtual machine part of the backend pool you would like this rule to be associated to. |

| Port mapping | This setting can be default or custom based on your application preference. |

### Outbound rules

Load balancer outbound rules configure outbound SNAT for VMs in the backend pool.

If you want to add an outbound rule to your load balancer, go to your load balancer in the Azure portal, select **Outbound rules**, and then select **+Add**.

| Setting | Details |

| ------- | ------ |

| Name | The name of your outbound rule. |

| Frontend IP address | Select the frontend IP address. </br> The frontend IP address of your load balancer you want the outbound rule to be associated to. |

| Protocol | Azure Load Balancer is a layer 4 network load balancer. </br> Your options are: **All**, **TCP**, or **UDP**. |

| Idle timeout (minutes) | Keep a **TCP** or **HTTP** connection open without relying on clients to send keep-alive messages. |

| TCP Reset | Load balancer can send **TCP resets** to create a more predictable application behavior when the connection is idle. </br> Learn more about [TCP reset](load-balancer-tcp-reset.md) |

| Backend pool | The backend pool you would like this outbound rule to be applied on. |

| Port allocation | Your options are **Manually choose number of outbound ports** or **Use the default number of outbound ports**. </br> When you use default port allocation, Azure can drop existing connections when you scale out. Manually allocate ports to avoid dropped connections. |

| **Outbound Ports** |   |

| Choose by | Your options are **Ports per instance** or **Maximum number of backend instances**. </br> When you use default port allocation, Azure can drop existing connections when you scale out. Manually allocate ports to avoid dropped connections. |

| Ports per instance | Enter number of ports to be used per instance. This entry is only available when choosing **Ports per instance** for outbound ports above. |

| Available Frontend ports | Displayed value of total available frontend ports based on selected port allocation. |

| Maximum number of backend instances | Enter the maximum number of back end instances. This entry is only available when choosing **Maximum number of backend instances** for outbound ports above. </br> You can't scale your backend pool above this number of instances. Increasing the number of instances decreases the number of ports per instance unless you also add more frontend IP addresses. |

## Next Steps

In this article, you learned about the different terms and settings in the Azure portal for Azure Load Balancer.

* [Learn](./load-balancer-overview.md) more about Azure Load Balancer.

* [FAQs](./load-balancer-faqs.yml) for Azure Load Balancer.


# Components

# Azure Load Balancer components

Azure Load Balancer includes a few key components. These components can be configured in your subscription through the Azure portal, Azure CLI, Azure PowerShell, an Azure Resource Manager Template or appropriate alternatives.

## Frontend IP configuration <a name = "frontend-ip-configurations"></a>

The IP address of your Azure Load Balancer. It's the point of contact for clients. These IP addresses can be either:

- **Public IP Address**

- **Private IP Address**

The nature of the IP address determines the **type** of load balancer created. Private IP address selection creates an internal load balancer. Public IP address selection creates a public load balancer.

| | **Public load balancer**  | **Internal load balancer** |

| ---------- | ---------- | ---------- |

| **Frontend IP configuration**| Public IP address | Private IP address|

| **Description** | A public load balancer maps the public IP and port of incoming traffic to the private IP and port of the VM. Load balancer maps traffic the other way around for the response traffic from the VM. You can distribute specific types of traffic across multiple VMs or services by applying load-balancing rules. For example, you can spread the load of web request traffic across multiple web servers.| An internal load balancer distributes traffic to resources that are inside a virtual network. Azure restricts access to the frontend IP addresses of a virtual network that are load balanced. Frontend IP addresses and virtual networks are never directly exposed to an internet endpoint, meaning an internal load balancer can't accept incoming traffic from the internet. Internal line-of-business applications run in Azure and are accessed from within Azure or from on-premises resources. |

| **SKUs supported** | Basic, Standard | Basic, Standard |

Load balancer can have multiple frontend IPs. Learn more about [multiple frontends](load-balancer-multivip-overview.md).

## Backend pool

The group of virtual machines or instances in a virtual machine scale set that's serving the incoming request. To scale cost-effectively to meet high volumes of incoming traffic, computing guidelines generally recommend adding more instances to the backend pool.

Load balancer instantly reconfigures itself via automatic reconfiguration when you scale instances up or down. Adding or removing VMs from the backend pool reconfigures the load balancer without other operations. The scope of the backend pool is any virtual machine in a single virtual network.

Backend pools support addition of instances via [network interface or IP addresses](backend-pool-management.md). VMs don't need a public IP address in order to be attached to backend pool of a public load balancer. VMs can be attached to the backend pool of a load balancer even if they are in a stopped state. You can also configure multiple backend pools with different groups of instances to a single load balancer. By creating multiple load balancing rules, each targeting a different backend pool, you can configure traffic to distribute to different sets of backend resources based on the load balancer frontend port and protocol.

## Health probes

A health probe is used to determine the health status of the instances in the backend pool. During load balancer creation, configure a health probe for the load balancer to use. This health probe determines if an instance is healthy and can receive traffic.

You can define the unhealthy threshold for your health probes. When a probe fails to respond, the load balancer stops sending new connections to the unhealthy instances. A probe failure doesn't affect existing connections. The connection continues until the application:

- Ends the flow

- Idle timeout occurs

- The VM shuts down

Load balancer provides different health probe types for endpoints: TCP, HTTP, and HTTPS. [Learn more about Load Balancer Health probes](load-balancer-custom-probe-overview.md).

Basic load balancer doesn't support HTTPS probes. Basic load balancer closes all TCP connections (including established connections).

## Load Balancer rules

A load balancer rule is used to define how incoming traffic is distributed to **all** the instances within the backend pool. A load-balancing rule maps a given frontend IP configuration and port to multiple backend IP addresses and ports. Load Balancer rules are for inbound traffic only.

For example, use a load balancer rule for port 80 to route traffic from your frontend IP to port 80 of your backend instances.

*Figure: Load-Balancing rules*

## High Availability Ports

A load balancer rule configured with **'protocol - all and port - 0'** is known as a High Availability (HA) port rule. This rule enables a single rule to load-balance all TCP and UDP flows that arrive on all ports of an internal Standard Load Balancer.

The load-balancing decision is made per flow. This action is based on the following five-tuple connection:

- source IP address

- source port

- destination IP address

- destination port

- protocol

The HA ports load-balancing rules help you with critical scenarios, such as high availability and scale for network virtual appliances (NVAs) inside virtual networks. The feature can help when a large number of ports must be load-balanced.

HA Ports are commonly used for Network Virtual Appliances (NVAs) such as firewalls, VPNs, or SD-WAN devices, where defining individual load-balancing rules per port is not practical. Traffic is distributed per connection flow (5-tuple), and health probes are used to ensure traffic is sent only to healthy instances.

Please note that HA Ports are not supported on Basic or Public Load Balancers and are not intended for typical web or application workloads that require port-specific rules.

*Figure: HA Ports rules*

Learn more about [HA ports](load-balancer-ha-ports-overview.md).

## Inbound NAT rules

An inbound NAT rule forwards incoming traffic sent to frontend IP address and port combination. The traffic is sent to a **specific** virtual machine or instance in the backend pool. Port forwarding is done by the same hash-based distribution as load balancing.

*Figure: Inbound NAT rules*

## Outbound rules

An outbound rule configures outbound Network Address Translation (NAT) for all virtual machines or instances identified by the backend pool. This rule enables instances in the backend to communicate (outbound) to the internet or other endpoints.

Learn more about [outbound connections and rules](load-balancer-outbound-connections.md).

Basic load balancer doesn't support outbound rules.

*Figure: Outbound rules*

## Limitations

- Learn about load balancer [limits](../azure-resource-manager/management/azure-subscription-service-limits.md)

- Load balancer provides load balancing and port forwarding for specific TCP or UDP protocols. Load-balancing rules and inbound NAT rules support TCP and UDP, but not other IP protocols including ICMP.

- Load Balancer backend pool can't consist of a [Private Endpoint](../private-link/private-endpoint-overview.md).

- Outbound flow from a backend VM to a frontend of an internal Load Balancer will fail.

- A load balancer rule can't span two virtual networks. All load balancer frontends and their backend instances must be in a single virtual network.

- Forwarding IP fragments isn't supported on load-balancing rules. IP fragmentation of UDP and TCP packets isn't supported on load-balancing rules.

- You can only have one Public Load Balancer (NIC based) and one internal Load Balancer (NIC based) per availability set. However, this constraint doesn't apply to IP-based load balancers.

## Next step

> [!div class="nextstepaction"]

> [Create a public Standard load balancer](quickstart-load-balancer-standard-public-portal.md)


# Concepts

# Azure Load Balancer algorithm

Azure Load Balancer is Azure's most performant Load Balancer all while keeping latency ultra-low. To learn more about Azure Load Balancer, visit [Azure Load Balancer overview](load-balancer-overview.md) or Azure Load balancer [components](components.md).

Azure Load Balancer uses a tuple-based hashing as the load-balancing algorithm.

## Load balancing algorithm

By creating a load balancer rule, you can distribute inbound traffic flows from a load balancer's frontend to its backend pools. Azure Load Balancer uses a five-tuple hashing algorithm for the distribution of inbound flows (not bytes). Load balancer rewrites the headers of TCP/UDP headers flows when directing traffic to the backend pool instances (load balancer doesn't rewrite HTTP/HTTPS headers). When the load balancer's health probe indicates a healthy backend endpoint, backend instances are available to receive new traffic flows.

By default, Azure Load Balancer uses a five-tuple hash.

The five-tuple includes:

- **Source IP address**

- **Source port**

- **Destination IP address**

- **Destination port**

- **IP protocol number to map flows to available servers**

You can also use session affinity [distribution mode](distribution-mode-concepts.md) which uses two-tuple or three-tuple based load balancing.

Azure Load Balancer supports any TCP/UDP application scenario and doesn't close or originate flows. Load balancer also doesn't interact with the payload of any flow. Application payloads are transparent to the load balancer. Any UDP or TCP application can be supported.

Load balancer operates on layer 4 and doesn't provide application layer gateway functionality. Protocol handshakes always occur directly between the client and the backend pool instance. Because the load balancer doesn't interact with the TCP payload nor does it provide TLS offload, you can build comprehensive encrypted scenarios. Using load balancer gains large scale-out for TLS applications by ending the TLS connection on the VM itself. For example, your TLS session keying capacity is only limited by the type and number of VMs you add to the backend pool.

A response to an inbound flow is always a response from a virtual machine. When the flow arrives on the virtual machine, the original source IP address is also preserved. Every endpoint is answered by a VM. For example, a TCP handshake occurs between the client and the selected backend VM. A response to a request to a front end is a response generated by a backend VM. When you successfully validate connectivity to a front end, you're validating the connectivity throughout to at least one backend virtual machine.

## Next steps

- Learn more about [Azure Load Balancer](load-balancer-overview.md).

- Learn about the [components](components.md) that make up Azure Load Balancer.

- Learn about [Health Probes](load-balancer-custom-probe-overview.md).

- Learn about Azure Load Balancer's traffic [distribution modes](distribution-mode-concepts.md)

- See [Create a public Standard Load Balancer](quickstart-load-balancer-standard-public-portal.md) to get started with using a Load Balancer: create one, create VMs with a custom IIS extension installed, and load balance the web app between the VMs.

- Learn about [Azure Load Balancer outbound connections](load-balancer-outbound-connections.md).


# Distribution Mode Concepts

# Azure Load Balancer distribution modes

Azure Load Balancer supports the following distribution modes for routing connections to instances in the backend pool:

| Distribution mode | Hash based | Session persistence: Client IP | Session persistence: Client IP and protocol |

| --- | --- | --- | --- |

| Overview | Traffic from the same client IP routed to any healthy instance in the backend pool | Traffic from the same client IP is routed to the same backend instance | Traffic from the same client IP and protocol is routed to the same backend instance |

| Tuples | five-tuple | two-tuple | three-tuple |

| Azure portal configuration | Session persistence: **None** | Session persistence: **Client IP** | Session persistence: **Client IP and protocol** |

| [REST API](/rest/api/load-balancer/load-balancers/create-or-update#loaddistribution) |  ```"loadDistribution":"Default"```| ```"loadDistribution":SourceIP```    | ```"loadDistribution":SourceIPProtocol```    |

There's no downtime when switching from one distribution mode to another on a load balancer.

## Hash based

Azure Load Balancer uses a five-tuple hash based distribution mode by default.

The five-tuple consists of:

- **Source IP**

- **Source port**

- **Destination IP**

- **Destination port**

- **Protocol type**

The hash is used to route traffic to healthy backend instances within the backend pool. The algorithm provides stickiness only within a transport session. When the client starts a new session from the same source IP, the source port changes and causes the traffic to go to a different backend instance.

In order to configure hash based distribution, you must select session persistence to be **None** in the Azure portal. This specifies that successive requests from the same client can be handled by any virtual machine.

> [!NOTE]

> When there is limited variation in source IP addresses and ports, the load balancer may not have enough distinct flow information to distribute traffic evenly across backends. In scenarios where intermediate devices (such as firewalls performing SNAT) reduce the number of visible source IP addresses and assign source ports in predictable patterns, the available variation in traffic flows can be significantly limited, especially when traffic originates from a small number of clients. This may result in highly skewed or no distribution across backend instances. If you experience uneven distribution, increase the number of clients sending traffic through the intermediate device, or try adjusting the number of intermediate device instances or load balancer backends to break the hashing symmetry.

## Session persistence

Session persistence is also known session affinity, source IP affinity, or client IP affinity. This distribution mode uses a two-tuple (source IP and destination IP) or three-tuple (source IP, destination IP, and protocol type) hash to route to backend instances. When using session persistence, connections from the same client go to the same backend instance within the backend pool.

Session persistence mode has two configuration types:

- **Client IP (2-tuple)** - Specifies that successive requests from the same client IP address are handled by the same backend instance.

- **Client IP and protocol (3-tuple)** - Specifies that successive requests from the same client IP address and protocol combination are handled by the same backend instance.

The following figure illustrates a two-tuple configuration. Notice how the two-tuple runs through the load balancer to virtual machine 1 (VM1). VM1 is backed up by VM2 and VM3.

## Use cases

Source IP affinity with client IP and protocol (source IP affinity three-tuple), solves an incompatibility between Azure Load Balancer and Remote Desktop Gateway (RD Gateway).

Another use case scenario is media upload. The data upload happens through UDP, but the control plane is achieved through TCP:

- A client starts a TCP session to the load-balanced public address and is directed to a specific DIP. The channel is left active to monitor the connection health.

- A new UDP session from the same client computer is started to the same load-balanced public endpoint. The connection is directed to the same DIP endpoint as the previous TCP connection. The media upload can be executed at high throughput while maintaining a control channel through TCP.

> [!NOTE]

> When Load Balancer backend pool members change either by removing or adding a virtual machine, the distribution of client requests is recomputed. You can't depend on new connections from existing clients to end up at the same server. Additionally, using source IP affinity distribution mode can cause an uneven distribution of traffic. Clients that run behind proxies might be seen as one unique client application.

## Next steps

For more information on how to configure the distribution mode of Azure Load Balancer, see [Configure the distribution mode for Azure Load Balancer](load-balancer-distribution-mode.md).


# Load Balancer Best Practices

# Azure Load Balancer Best Practices

This article discusses a collection of Azure best practices for your load balancer deployment. These best practices are derived from our experience with Azure networking and the experiences of customers like yourself.

For each best practice, this article explains:

- What the best practice is

- Why you want to enable that best practice

- What might happen if you fail to enable the best practice

- How you can learn to enable this best practice

These best practices are based on a consensus opinion, and Azure platform capability and features sets, as they exist at the time this article was written.

## Architectural best practices

The following architectural guidance helps ensure the reliability of your Azure Load Balancer deployment. It includes best practices for deploying with zone-redundancy, redundancy in your backend pool, and deploying a global load balancer. Along with reliability for Gateway Load Balancer, which is recommended when using NVAs instead of a dual load balancer set-up.

### Reliability best practices

The following best practices are recommended to ensure the reliability of your Azure Load Balancer deployment.

#### Deploy with zone-redundancy

Zone-redundancy provides the best resiliency by protecting the data path from zone failure. The load balancer's availability zone selection is synonymous with its frontend IP's zone selection. For public load balancers, if the public IP in the load balancer's frontend is zone redundant then the load balancer is also zone-redundant.

- Deploy load balancer in a region that supports availability zones and enable Zone-redundant when creating a new Public IP address used for the Frontend IP configuration.

- Public IP addresses can't be changed to zone redundant but we're updating all non-zonal Standard Public IPs to be zone redundant by default. For more information, visit the following Microsoft Azure Blog [Azure Public IPs are now zone-redundant by default | Microsoft Azure Blog](https://azure.microsoft.com/blog/azure-public-ips-are-now-zone-redundant-by-default/?msockid=028aa4446a5a601f37ecb0076b7761c7). To see the most updated list of regions that support zone redundant Standard Public IPs by default, see [Public IP addresses in Azure](../virtual-network/ip-services/public-ip-addresses.md)

- If you can't deploy as zone-redundant, the next option is to have a zonal load balancer deployment.

- A Zonal frontend is recommended when the backend is concentrated in a particular zone. Though we recommend deploying backend pool members across multiple zones to benefit from zone redundancy.

- Refer to the following the doc if you want to migrate existing deployments to zonal or zone-redundant [Migrate Load Balancer to availability zone support](/azure/reliability/migrate-load-balancer).

#### Redundancy in your backend pool

Ensure that the backend pool contains at least two instances. If your backend pool only has one instance and it's unhealthy, all traffic sent to the backend pool fails due to lack of redundancy. The Standard Load Balancer SLA is also only supported when there are at least two healthy backend pool instances per backend pool. Visit the [SLA documentation](https://www.microsoft.com/licensing/docs/view/Service-Level-Agreements-SLA-for-Online-Services?lang=1) for more information.

#### Deploy a global load balancer

Standard Load Balancer supports cross-region load balancing enabling regional redundancy through linking a global load balancer to your existing regional load balancers. With a global load balancer, if one region fails, the traffic is routed to the next closest healthy regional load balancer. For more details, visit the [Global Load Balancer documentation](cross-region-overview.md).

For more information, see [Azure Load Balancer Reliability documentation](/azure/reliability/reliability-load-balancer).

### Reliability with Gateway Load Balancer

The following best practices are recommended to ensure the reliability of your Gateway Load Balancer deployment.

#### Chain your Gateway Load Balancer to a Standard Public Load Balancer

Chaining your Gateway Load Balancer to a Standard Public Load Balancer is recommended. This configuration provides high availability and redundancy on both the NVA and application layer. For more information, see [Tutorial: Create a gateway load balancer](./tutorial-create-gateway-load-balancer.md)

#### Use a Gateway load balancer when using NVAs instead of a dual load balancer set-up.

We recommend using a Gateway load balancer in north-south traffic scenarios with partner Network Virtual Appliances (NVAs). It's easier to deploy because Gateway load balancers don’t require extra configuration such as user-defined routes (UDRs) because it maintains flow stickiness and flow symmetry. It's also easier to manage because NVAs can be easily added and removed. For more information, see the [Gateway Load Balancer documentation](gateway-overview.md).

## Configuration guidance

The following configuration guidance is best practices for configuring your Azure Load Balancer deployments.

### Create Network Security Groups (NSGs)

To explicitly permit allowed inbound traffic, you should create Network Security Groups (NSGs). NSGs must be created on the subnet or network interface card (NIC) of your VM, otherwise there will be no inbound connectivity to your Standard external load balancers. For more information, see [Create, change, or delete an Azure network security group](../virtual-network/manage-network-security-group.md).

### Unblock 168.63.129.16 IP address

Ensure 168.63.129.16 IP address isn't blocked by any Azure network security groups and local firewall policies. This IP address enables health probes from Azure Load Balancer to determine the health state of the VM. If it isn't allowed, the health probe fails as it is unable to reach your instance and it marks your instance as down. For more information, see [Azure Load Balancer health probe](load-balancer-custom-probe-overview.md) and [What is IP address 168.63.129.16?](../virtual-network/what-is-ip-address-168-63-129-16.md)s.

### Use outbound rules with manual port allocation

Use outbound rules with manual port allocation instead of default port allocation to prevent SNAT exhaustion or connection failures. Default port allocation automatically assigns a conservative number of ports which can cause a higher risk of SNAT port exhaustion. Manual port allocation can help maximize the number of SNAT ports made available for each of the instances in your backend pool which can help prevent your connections from being impacted due to port reallocation.

There are two options for manual port allocation, “ports per instance” or “maximum number of backend instances”. To understand the considerations of both, see [Source Network Address Translation (SNAT) for outbound connections](load-balancer-outbound-connections.md).

### Check your distribution mode

Azure Load Balancer uses a 5-tuple hash based distribution mode by default and also offers session persistence using a 2-tuple or 3-tuple hash. Consider whether your deployment could benefit from session persistence (also known as session affinity) where connections from the same client IP or same client IP and protocol go to the same backend instance within the backend pool. Also consider that enabling session affinity can cause uneven load distribution as most connections come from the same client IP or same client IP and protocol will be sent to the same backend VM.

For more information about Azure Load Balancers distribution modes, see [Azure Load Balancer distribution modes](distribution-mode-concepts.md).

### Enable TCP resets

Enabling TCP resets on your Load Balancer sends bidirectional TCP resets packets to both client and server endpoints on idle time-out to inform your application endpoints that the connection timed out and is no longer usable. Without enabling TCP reset, the Load Balancer silently drops flows when the idle time-out of a flow is reached. It can also be beneficial to increase idle time-out and/or use a TCP keep-alive if you’re seeing connections time out.

For more information on TCP resets, idle time-outs, and TCP keepalive, visit [Load Balancer TCP Reset and idle time-out in Azure](load-balancer-tcp-reset.md).

### Configure loop back interface when setting up floating IP

If you enable floating IP, ensure you have a loopback interface within guest OS that is configured with the frontend IP address of the load balancer. Floating IP needs to be enabled it you want to reuse the backend port across multiple rules. Some example use cases of port reuse include clustering for high availability and network virtual appliances. For more information, see [Azure Load Balancer Floating IP configuration](load-balancer-floating-ip.md#floating-ip-guest-os-configuration).

### Implement Gateway Load Balancer configuration best practices

Separate your trusted and untrusted traffic on two different tunnel interfaces; use the tunnel interface type external for untrusted/not yet inspected or managed traffic and use the tunnel interface type internal for trusted/inspected traffic. As a security best practice, this ensures isolation of trusted and untrusted traffic and can allow for more granular traffic control and troubleshooting.

Ensure your NVAs MTU limit is increased to at least 1550, or up to the recommended limit of 4000 for scenarios where jumbo frames are used. Without increasing the MTU limit, you can experience packet drops due to the larger packet size from other packets generated by the VXLAN headers.

## Retirement announcements

Along with new improvements and updates to Azure Load Balancer, there are also deprecations to functionalities. It's critical to stay updated and ensure you're making the necessary changes to avoid any potential service disruptions. For a complete list of retirement announcements, see the [Azure Updates page](https://azure.microsoft.com/updates?filters=%5B%22Load+Balancer%22%2C%22Retirements%22%5D) and filter for “Load Balancer” under “Products” and “Retirements” under “Update Type”.

### Use or upgrade to Standard Load Balancer

[Basic Load Balancer was retired September 30, 2025](https://azure.microsoft.com/updates?id=azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer) and customers should upgrade from Basic Load Balancer to Standard Load Balancer by then. Standard Load Balancer provides significant improvements including high performance, ultra-low latency, security by default, and SLA of 99.99% availability.

### Don't use default outbound access

Moving forward, don't use [default outbound access](../virtual-network/ip-services/default-outbound-access.md) and ensure all VMs have a defined explicit outbound method. This is recommended for better security and greater control over how your VMs connect to the internet. Default outbound access will [retire September 30, 2025](https://azure.microsoft.com/updates?id=default-outbound-access-for-vms-in-azure-will-be-retired-transition-to-a-new-method-of-internet-access) and VMs created after this date must use one of the following outbound solutions to communicate to the internet:

- Associate a NAT GW to the subnet

- Use one or more frontend IPs of a Load Balancer for outbound via outbound rules

- Assign an instance-level public IP address to the VM

## Next steps

> [!div class="nextstepaction"]

> [Azure Load Balancer overview](load-balancer-overview.md)


# Quickstart Load Balancer Standard Public Powershell

# Quickstart: Create a public load balancer to load balance VMs using Azure PowerShell

Get started with Azure Load Balancer by using Azure PowerShell to create a public load balancer and two virtual machines. Also, you deploy other resources including Azure Bastion, NAT Gateway, a virtual network, and the required subnets.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)

- Azure PowerShell installed locally or Azure Cloud Shell

If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 5.4.1 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell). If you're running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

## Create a resource group

An Azure resource group is a logical container into which Azure resources are deployed and managed.

Create a resource group with [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup):

```azurepowershell-interactive

$rg = @{

Name = 'CreatePubLBQS-rg'

Location = 'westus2'

}

New-AzResourceGroup @rg

```

## Create a public IP address

Use [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) to create a public IP address.

```azurepowershell-interactive

$publicip = @{

Name = 'myPublicIP'

ResourceGroupName = $rg.name

Location = 'westus2'

Sku = 'Standard'

AllocationMethod = 'static'

Zone = 1,2,3

}

New-AzPublicIpAddress @publicip

```

To create a zonal public IP address in zone 1, use the following command:

```azurepowershell-interactive

$publicip = @{

Name = 'myPublicIP'

ResourceGroupName = $rg.name

Location = 'westus2'

Sku = 'Standard'

AllocationMethod = 'static'

Zone = 1

}

New-AzPublicIpAddress @publicip

```

## Create a load balancer

This section details how you can create and configure the following components of the load balancer:

* Create a frontend IP with [New-AzLoadBalancerFrontendIpConfig](/powershell/module/az.network/new-azloadbalancerfrontendipconfig) for the frontend IP pool. This IP receives the incoming traffic on the load balancer

* Create a backend address pool with [New-AzLoadBalancerBackendAddressPoolConfig](/powershell/module/az.network/new-azloadbalancerbackendaddresspoolconfig) for traffic sent from the frontend of the load balancer. This pool is where your backend virtual machines are deployed

* Create a health probe with [Add-AzLoadBalancerProbeConfig](/powershell/module/az.network/add-azloadbalancerprobeconfig) that determines the health of the backend VM instances

* Create a load balancer rule with [Add-AzLoadBalancerRuleConfig](/powershell/module/az.network/add-azloadbalancerruleconfig) that defines how traffic is distributed to the VMs

* Create a public load balancer with [New-AzLoadBalancer](/powershell/module/az.network/new-azloadbalancer)

```azurepowershell-interactive

## Place public IP created in previous steps into variable. ##

$pip = @{

Name = 'myPublicIP'

ResourceGroupName = $rg.name

}

$publicIp = Get-AzPublicIpAddress @pip

## Create load balancer frontend configuration and place in variable. ##

$fip = @{

Name = 'myFrontEnd'

PublicIpAddress = $publicIp

}

$feip = New-AzLoadBalancerFrontendIpConfig @fip

## Create backend address pool configuration and place in variable. ##

$bepool = New-AzLoadBalancerBackendAddressPoolConfig -Name 'myBackEndPool'

## Create the health probe and place in variable. ##

$probe = @{

Name = 'myHealthProbe'

Protocol = 'tcp'

Port = '80'

IntervalInSeconds = '360'

ProbeCount = '5'

}

$healthprobe = New-AzLoadBalancerProbeConfig @probe

## Create the load balancer rule and place in variable. ##

$lbrule = @{

Name = 'myHTTPRule'

Protocol = 'tcp'

FrontendPort = '80'

BackendPort = '80'

IdleTimeoutInMinutes = '15'

FrontendIpConfiguration = $feip

BackendAddressPool = $bePool

}

$rule = New-AzLoadBalancerRuleConfig @lbrule -EnableTcpReset -DisableOutboundSNAT

## Create the load balancer resource. ##

$loadbalancer = @{

ResourceGroupName = $rg.name

Name = 'myLoadBalancer'

Location = 'westus2'

Sku = 'Standard'

FrontendIpConfiguration = $feip

BackendAddressPool = $bePool

LoadBalancingRule = $rule

Probe = $healthprobe

}

New-AzLoadBalancer @loadbalancer

```

## Configure virtual network

Before you deploy VMs and test your load balancer, create the supporting virtual network resources.

Create a virtual network for the backend virtual machines.

Create a network security group to define inbound connections to your virtual network.

Create an Azure Bastion host to securely manage the virtual machines in the backend pool.

Use a NAT gateway to provide outbound internet access to resources in the backend pool of your load balancer.

### Create virtual network, network security group, bastion host, and NAT gateway

* Create a virtual network with [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork)

* Create a network security group rule with [New-AzNetworkSecurityRuleConfig](/powershell/module/az.network/new-aznetworksecurityruleconfig)

* Create an Azure Bastion host with [New-AzBastion](/powershell/module/az.network/new-azbastion)

* Create a network security group with [New-AzNetworkSecurityGroup](/powershell/module/az.network/new-aznetworksecuritygroup)

* Create the NAT gateway resource with [New-AzNatGateway](/powershell/module/az.network/new-aznatgateway)

* Use [New-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/new-azvirtualnetworksubnetconfig) to associate the NAT gateway to the subnet of the virtual network

> [!IMPORTANT]

> [!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

```azurepowershell-interactive

## Create public IP address for NAT gateway ##

$ip = @{

Name = 'myNATgatewayIP'

ResourceGroupName = $rg.name

Location = 'westus2'

Sku = 'Standard'

AllocationMethod = 'Static'

}

$publicIP = New-AzPublicIpAddress @ip

## Create NAT gateway resource ##

$nat = @{

ResourceGroupName = $rg.name

Name = 'myNATgateway'

IdleTimeoutInMinutes = '10'

Sku = 'Standard'

Location = 'westus2'

PublicIpAddress = $publicIP

}

$natGateway = New-AzNatGateway @nat

## Create backend subnet config ##

$subnet = @{

Name = 'myBackendSubnet'

AddressPrefix = '10.1.0.0/24'

NatGateway = $natGateway

}

$subnetConfig = New-AzVirtualNetworkSubnetConfig @subnet

## Create Azure Bastion subnet. ##

$bastsubnet = @{

Name = 'AzureBastionSubnet'

AddressPrefix = '10.1.1.0/24'

}

$bastsubnetConfig = New-AzVirtualNetworkSubnetConfig @bastsubnet

## Create the virtual network ##

$net = @{

Name = 'myVNet'

ResourceGroupName = $rg.name

Location = 'westus2'

AddressPrefix = '10.1.0.0/16'

Subnet = $subnetConfig,$bastsubnetConfig

}

$vnet = New-AzVirtualNetwork @net

## Create public IP address for bastion host. ##

$ip = @{

Name = 'myBastionIP'

ResourceGroupName = $rg.name

Location = 'westus2'

Sku = 'Standard'

AllocationMethod = 'Static'

}

$publicip = New-AzPublicIpAddress @ip

## Create bastion host ##

$bastion = @{

ResourceGroupName = $rg.name

Name = 'myBastion'

PublicIpAddress = $publicip

VirtualNetwork = $vnet

}

New-AzBastion @bastion -AsJob

## Create rule for network security group and place in variable. ##

$nsgrule = @{

Name = 'myNSGRuleHTTP'

Description = 'Allow HTTP'

Protocol = '*'

SourcePortRange = '*'

DestinationPortRange = '80'

SourceAddressPrefix = 'Internet'

DestinationAddressPrefix = '*'

Access = 'Allow'

Priority = '2000'

Direction = 'Inbound'

}

$rule1 = New-AzNetworkSecurityRuleConfig @nsgrule

## Create network security group ##

$nsg = @{

Name = 'myNSG'

ResourceGroupName = $rg.name

Location = 'westus2'

SecurityRules = $rule1

}

New-AzNetworkSecurityGroup @nsg

```

## Create virtual machines

In this section, you create the two virtual machines for the backend pool of the load balancer.

* Create two network interfaces with [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface)

* Set an administrator username and password for the VMs with [Get-Credential](/powershell/module/microsoft.powershell.security/get-credential)

* Create the virtual machines with:

* [New-AzVM](/powershell/module/az.compute/new-azvm)

* [New-AzVMConfig](/powershell/module/az.compute/new-azvmconfig)

* [Set-AzVMOperatingSystem](/powershell/module/az.compute/set-azvmoperatingsystem)

* [Set-AzVMSourceImage](/powershell/module/az.compute/set-azvmsourceimage)

* [Add-AzVMNetworkInterface](/powershell/module/az.compute/add-azvmnetworkinterface)

```azurepowershell-interactive

# Set the administrator and password for the VMs. ##

$cred = Get-Credential

## Place the virtual network into a variable. ##

$net = @{

Name = 'myVNet'

ResourceGroupName = $rg.name

}

$vnet = Get-AzVirtualNetwork @net

## Place the load balancer into a variable. ##

$lb = @{

Name = 'myLoadBalancer'

ResourceGroupName = $rg.name

}

$bepool = Get-AzLoadBalancer @lb  | Get-AzLoadBalancerBackendAddressPoolConfig

## Place the network security group into a variable. ##

$ns = @{

Name = 'myNSG'

ResourceGroupName = $rg.name

}

$nsg = Get-AzNetworkSecurityGroup @ns

## For loop with variable to create virtual machines for load balancer backend pool. ##

for ($i=1; $i -le 2; $i++){

## Command to create network interface for VMs ##

$nic = @{

Name = "myNicVM$i"

ResourceGroupName = $rg.name

Location = 'westus2'

Subnet = $vnet.Subnets[0]

NetworkSecurityGroup = $nsg

LoadBalancerBackendAddressPool = $bepool

}

$nicVM = New-AzNetworkInterface @nic

## Create a virtual machine configuration for VMs ##

$vmsz = @{

VMName = "myVM$i"

VMSize = 'Standard_DS1_v2'

}

$vmos = @{

ComputerName = "myVM$i"

Credential = $cred

}

$vmimage = @{

PublisherName = 'MicrosoftWindowsServer'

Offer = 'WindowsServer'

Skus = '2019-Datacenter'

Version = 'latest'

}

$vmConfig = New-AzVMConfig @vmsz `

| Set-AzVMOperatingSystem @vmos -Windows `

| Set-AzVMSourceImage @vmimage `

| Add-AzVMNetworkInterface -Id $nicVM.Id

## Create the virtual machine for VMs ##

$vm = @{

ResourceGroupName = $rg.name

Location = 'westus2'

VM = $vmConfig

Zone = "$i"

}

New-AzVM @vm -AsJob

}

```

The deployments of the virtual machines and bastion host are submitted as PowerShell jobs. To view the status of the jobs, use [Get-Job](/powershell/module/microsoft.powershell.core/get-job):

```azurepowershell-interactive

Get-Job

Id     Name            PSJobTypeName   State         HasMoreData     Location             Command

--     ----            -------------   -----         -----------     --------             -------

1      Long Running O… AzureLongRunni… Completed     True            localhost            New-AzBastion

2      Long Running O… AzureLongRunni… Completed     True            localhost            New-AzVM

3      Long Running O… AzureLongRunni… Completed     True            localhost            New-AzVM

```

Ensure the **State** of the VM creation is **Completed** before moving on to the next steps.

[!INCLUDE [ephemeral-ip-note.md](~/reusable-content/ce-skilling/azure/includes/ephemeral-ip-note.md)]

## Install IIS

Use [Set-AzVMExtension](/powershell/module/az.compute/set-azvmextension) to install the Custom Script Extension.

The extension runs `PowerShell Add-WindowsFeature Web-Server` to install the IIS webserver and then updates the Default.htm page to show the hostname of the VM:

> [!IMPORTANT]

> Ensure the virtual machine deployments have completed from the previous steps before proceeding. Use `Get-Job` to check the status of the virtual machine deployment jobs.

```azurepowershell-interactive

## For loop with variable to install custom script extension on virtual machines. ##

for ($i=1; $i -le 2; $i++)

{

$ext = @{

Publisher = 'Microsoft.Compute'

ExtensionType = 'CustomScriptExtension'

ExtensionName = 'IIS'

ResourceGroupName = $rg.name

VMName = "myVM$i"

Location = 'westus2'

TypeHandlerVersion = '1.8'

SettingString = '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}'

}

Set-AzVMExtension @ext -AsJob

}

```

The extensions are deployed as PowerShell jobs. To view the status of the installation jobs, use [Get-Job](/powershell/module/microsoft.powershell.core/get-job):

```azurepowershell-interactive

Get-Job

Id     Name            PSJobTypeName   State         HasMoreData     Location             Command

--     ----            -------------   -----         -----------     --------             -------

8      Long Running O… AzureLongRunni… Running       True            localhost            Set-AzVMExtension

9      Long Running O… AzureLongRunni… Running       True            localhost            Set-AzVMExtension

```

Ensure the **State** of the jobs is **Completed** before moving on to the next steps.

## Test the load balancer

Use [Get-AzPublicIpAddress](/powershell/module/az.network/get-azpublicipaddress) to get the public IP address of the load balancer:

```azurepowershell-interactive

$ip = @{

ResourceGroupName = $rg.name

Name = 'myPublicIP'

}

Get-AzPublicIPAddress @ip | select IpAddress

```

Copy the public IP address, and then paste it into the address bar of your browser. The default page of IIS Web server is displayed on the browser.

## Clean up resources

When no longer needed, you can use the [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) command to remove the resource group, load balancer, and the remaining resources.

```azurepowershell-interactive

Remove-AzResourceGroup -Name $rg.name

```

## Next steps

In this quickstart, you:

* Created an Azure Load Balancer

* Attached two VMs to the load balancer

* Tested the load balancer

To learn more about Azure Load Balancer, continue to:

> [!div class="nextstepaction"]

> [What is Azure Load Balancer?](load-balancer-overview.md)


# Quickstart Load Balancer Standard Public Cli

# Quickstart: Create a public load balancer to load balance VMs using the Azure CLI

Get started with Azure Load Balancer by using the Azure CLI to create a public load balancer and two virtual machines. Along with these resources, you deploy Azure Bastion, NAT Gateway, a virtual network, and the required subnets.

[!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment.md)]

- This quickstart requires version 2.0.28 or later of the Azure CLI. If using Azure Cloud Shell, the latest version is already installed.

## Create a resource group

An Azure resource group is a logical container into which Azure resources are deployed and managed.

Create a resource group with [az group create](/cli/azure/group#az-group-create):

```azurecli

az group create \

--name CreatePubLBQS-rg \

--location eastus

```

## Create a virtual network

Before you deploy VMs and test your load balancer, create the supporting virtual network and subnet.

Create a virtual network using [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create). The virtual network and subnet contain the resources deployed later in this article.

```azurecli

az network vnet create \

--resource-group CreatePubLBQS-rg \

--location eastus \

--name myVNet \

--address-prefixes 10.1.0.0/16 \

--subnet-name myBackendSubnet \

--subnet-prefixes 10.1.0.0/24

```

## Create a public IP address

To access your web app on the Internet, you need a public IP address for the load balancer.

Use [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create) to create the public IP for the load balancer frontend.

```azurecli

az network public-ip create \

--resource-group CreatePubLBQS-rg \

--name myPublicIP \

--sku Standard \

--zone 1 2 3

```

To create a zonal public IP address in Zone 1 instead, use the following command:

```azurecli

az network public-ip create \

--resource-group CreatePubLBQS-rg \

--name myPublicIP \

--sku Standard \

--zone 1

```

## Create a load balancer

This section details how you can create and configure the following components of the load balancer:

* A frontend IP pool that receives the incoming network traffic on the load balancer

* A backend IP pool where the frontend pool sends the load balanced network traffic

* A health probe that determines health of the backend VM instances

* A load balancer rule that defines how traffic is distributed to the VMs

### Create the load balancer resource

Create a public load balancer with [az network lb create](/cli/azure/network/lb#az-network-lb-create):

```azurecli

az network lb create \

--resource-group CreatePubLBQS-rg \

--name myLoadBalancer \

--sku Standard \

--public-ip-address myPublicIP \

--frontend-ip-name myFrontEnd \

--backend-pool-name myBackEndPool

```

If the public IP created is zonal, the specified zone needs to be defined when creating the public load balancer.

```azurecli

az network lb create \

--resource-group CreatePubLBQS-rg \

--name myLoadBalancer \

--sku Standard \

--public-ip-address myPublicIP \

--frontend-ip-name myFrontEnd \

--public-ip-zone 1 \

--backend-pool-name myBackEndPool

```

### Create the health probe

A health probe checks all virtual machine instances to ensure they can send network traffic.

A virtual machine with a failed probe check is removed from the load balancer. The virtual machine is added back into the load balancer when the failure is resolved.

Create a health probe with [az network lb probe create](/cli/azure/network/lb/probe#az-network-lb-probe-create):

```azurecli

az network lb probe create \

--resource-group CreatePubLBQS-rg \

--lb-name myLoadBalancer \

--name myHealthProbe \

--protocol tcp \

--port 80

```

### Create the load balancer rule

A load balancer rule defines:

* Frontend IP configuration for the incoming traffic

* The backend IP pool to receive the traffic

* The required source and destination port

Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#az-network-lb-rule-create):

```azurecli

az network lb rule create \

--resource-group CreatePubLBQS-rg \

--lb-name myLoadBalancer \

--name myHTTPRule \

--protocol tcp \

--frontend-port 80 \

--backend-port 80 \

--frontend-ip-name myFrontEnd \

--backend-pool-name myBackEndPool \

--probe-name myHealthProbe \

--disable-outbound-snat true \

--idle-timeout 15 \

--enable-tcp-reset true

```

## Create a network security group

For a standard load balancer, the VMs in the backend pool are required to have network interfaces that belong to a network security group.

Use [az network nsg create](/cli/azure/network/nsg#az-network-nsg-create) to create the network security group:

```azurecli

az network nsg create \

--resource-group CreatePubLBQS-rg \

--name myNSG

```

### Create a network security group rule

Create a network security group rule using [az network nsg rule create](/cli/azure/network/nsg/rule#az-network-nsg-rule-create):

```azurecli

az network nsg rule create \

--resource-group CreatePubLBQS-rg \

--nsg-name myNSG \

--name myNSGRuleHTTP \

--protocol '*' \

--direction inbound \

--source-address-prefix '*' \

--source-port-range '*' \

--destination-address-prefix '*' \

--destination-port-range 80 \

--access allow \

--priority 200

```

## Create a bastion host

In this section, you create the resources for Azure Bastion. Azure Bastion is used to securely manage the virtual machines in the backend pool of the load balancer.

> [!IMPORTANT]

> [!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

### Create a public IP address

Use [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create) to create a public ip address for the bastion host. The public IP is used by the bastion host for secure access to the virtual machine resources.

```azurecli

az network public-ip create \

--resource-group CreatePubLBQS-rg \

--name myBastionIP \

--sku Standard \

--zone 1 2 3

```

### Create a bastion subnet

Use [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-create) to create a bastion subnet. The bastion subnet is used by the bastion host to access the virtual network.

```azurecli

az network vnet subnet create \

--resource-group CreatePubLBQS-rg \

--name AzureBastionSubnet \

--vnet-name myVNet \

--address-prefixes 10.1.1.0/27

```

### Create bastion host

Use [az network bastion create](/cli/azure/network/bastion#az-network-bastion-create) to create a bastion host. The bastion host is used to connect securely to the virtual machine resources created later in this article.

```azurecli

az network bastion create \

--resource-group CreatePubLBQS-rg \

--name myBastionHost \

--public-ip-address myBastionIP \

--vnet-name myVNet \

--sku Basic \

--location eastus

```

It can take a few minutes for the Azure Bastion host to deploy.

## Create backend servers

In this section, you create:

* Two network interfaces for the virtual machines

* Two virtual machines to be used as backend servers for the load balancer

### Create network interfaces for the virtual machines

Create two network interfaces with [az network nic create](/cli/azure/network/nic#az-network-nic-create):

```azurecli

array=(myNicVM1 myNicVM2)

for vmnic in "${array[@]}"

do

az network nic create \

--resource-group CreatePubLBQS-rg \

--name $vmnic \

--vnet-name myVNet \

--subnet myBackEndSubnet \

--network-security-group myNSG

done

```

### Create virtual machines

Create the virtual machines with [az vm create](/cli/azure/vm#az-vm-create):

```azurecli

az vm create \

--resource-group CreatePubLBQS-rg \

--name myVM1 \

--nics myNicVM1 \

--image win2019datacenter \

--admin-username azureuser \

--zone 1 \

--no-wait

```

```azurecli

az vm create \

--resource-group CreatePubLBQS-rg \

--name myVM2 \

--nics myNicVM2 \

--image win2019datacenter \

--admin-username azureuser \

--zone 2 \

--no-wait

```

It can take a few minutes for the VMs to deploy. You can continue to the next steps while the VMs are creating.

[!INCLUDE [ephemeral-ip-note.md](~/reusable-content/ce-skilling/azure/includes/ephemeral-ip-note.md)]

### Add virtual machines to load balancer backend pool

Add the virtual machines to the backend pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#az-network-nic-ip-config-address-pool-add):

```azurecli

array=(myNicVM1 myNicVM2)

for vmnic in "${array[@]}"

do

az network nic ip-config address-pool add \

--address-pool myBackendPool \

--ip-config-name ipconfig1 \

--nic-name $vmnic \

--resource-group CreatePubLBQS-rg \

--lb-name myLoadBalancer

done

```

## Create NAT gateway

To provide outbound internet access for resources in the backend pool, create a NAT gateway.

### Create public IP

Use [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create) to create a single IP for the outbound connectivity.

```azurecli

az network public-ip create \

--resource-group CreatePubLBQS-rg \

--name myNATgatewayIP \

--sku Standard \

--zone 1 2 3

```

To create a zonal public IP address in Zone 1 instead, use the following command:

```azurecli

az network public-ip create \

--resource-group CreatePubLBQS-rg \

--name myNATgatewayIP \

--sku Standard \

--zone 1

```

### Create NAT gateway resource

Use [az network nat gateway create](/cli/azure/network/nat#az-network-nat-gateway-create) to create the NAT gateway resource. The public IP created in the previous step is associated with the NAT gateway.

```azurecli

az network nat gateway create \

--resource-group CreatePubLBQS-rg \

--name myNATgateway \

--public-ip-addresses myNATgatewayIP \

--idle-timeout 10

```

### Associate NAT gateway with subnet

Configure the source subnet in virtual network to use a specific NAT gateway resource with [az network vnet subnet update](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-update).

```azurecli

az network vnet subnet update \

--resource-group CreatePubLBQS-rg \

--vnet-name myVNet \

--name myBackendSubnet \

--nat-gateway myNATgateway

```

## Install IIS

Use [az vm extension set](/cli/azure/vm/extension#az-vm-extension-set) to install IIS on the virtual machines and set the default website to the computer name.

```azurecli

array=(myVM1 myVM2)

for vm in "${array[@]}"

do

az vm extension set \

--publisher Microsoft.Compute \

--version 1.8 \

--name CustomScriptExtension \

--vm-name $vm \

--resource-group CreatePubLBQS-rg \

--settings '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}'

done

```

## Test the load balancer

To get the public IP address of the load balancer, use [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show).

Copy the public IP address, and then paste it into the address bar of your browser.

```azurecli

az network public-ip show \

--resource-group CreatePubLBQS-rg \

--name myPublicIP \

--query ipAddress \

--output tsv

```

## Clean up resources

When no longer needed, use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, load balancer, and all related resources.

```azurecli

az group delete \

--name CreatePubLBQS-rg

```

## Next steps

In this quickstart:

* You created a standard public load balancer

* Attached two virtual machines

* Configured the load balancer traffic rule and health probe

* Tested the load balancer

To learn more about Azure Load Balancer, continue to:

> [!div class="nextstepaction"]

> [What is Azure Load Balancer?](load-balancer-overview.md)


# Quickstart Load Balancer Standard Public Bicep

# Quickstart: Create a public load balancer to load balance VMs using a Bicep file

In this quickstart, you learn to use a BICEP file to create a public Azure load balancer. The public load balancer distributes traffic to virtual machines in a virtual network located in the load balancer's backend pool. Along with the public load balancer, this template creates a virtual network, network interfaces, a NAT Gateway, and an Azure Bastion instance.

Using a Bicep file takes fewer steps comparing to other deployment methods.

[!INCLUDE [About Bicep](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-bicep-introduction.md)]

## Prerequisites

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Review the Bicep file

The Bicep file used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/load-balancer-standard-create/).

Load balancer and public IP SKUs must match. When you create a standard load balancer, you must also create a new standard public IP address that is configured as the frontend for the standard load balancer. Microsoft recommends using standard SKU for production workloads.

Multiple Azure resources have been defined in the bicep file:

- [**Microsoft.Network/loadBalancers**](/azure/templates/microsoft.network/loadbalancers)

- [**Microsoft.Network/publicIPAddresses**](/azure/templates/microsoft.network/publicipaddresses): for the load balancer, bastion host, and the NAT gateway.

- [**Microsoft.Network/bastionHosts**](/azure/templates/microsoft.network/bastionhosts)

- [**Microsoft.Network/networkSecurityGroups**](/azure/templates/microsoft.network/networksecuritygroups)

- [**Microsoft.Network/virtualNetworks**](/azure/templates/microsoft.network/virtualnetworks)

- [**Microsoft.Compute/virtualMachines**](/azure/templates/microsoft.compute/virtualmachines) (3).

- [**Microsoft.Network/networkInterfaces**](/azure/templates/microsoft.network/networkinterfaces) (3).

- [**Microsoft.Compute/virtualMachine/extensions**](/azure/templates/microsoft.compute/virtualmachines/extensions) (3): use to configure the Internet Information Server (IIS), and the web pages.

- [**Microsoft.Network/natGateways**](/azure/templates/microsoft.network/natgateways): for the NAT gateway.

> [!IMPORTANT]

> [!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

To find more Bicep files or ARM templates that are related to Azure Load Balancer, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Network&pageNumber=1&sort=Popular).

## Deploy the Bicep file

1. Save the Bicep file as **main.bicep** to your local computer.

1. Deploy the Bicep file using either Azure CLI or Azure PowerShell.

# [CLI](#tab/CLI)

```azurecli

az group create --name exampleRG --location EastUS

az deployment group create --resource-group exampleRG --template-file main.bicep

```

# [PowerShell](#tab/PowerShell)

```azurepowershell

New-AzResourceGroup -Name exampleRG -Location EastUS

New-AzResourceGroupDeployment -ResourceGroupName exampleRG -TemplateFile ./main.bicep

```

---

> [!NOTE]

> The Bicep file deployment creates three availability zones. Availability zones are supported only in [certain regions](/azure/reliability/availability-zones-overview). Use one of the supported regions. If you aren't sure, enter **EastUS**.

You're prompted to enter the following values:

- **projectName**: used for generating resource names.

- **adminUsername**: virtual machine administrator username.

- **adminPassword**: virtual machine administrator password.

It takes about 10 minutes to deploy the Bicep file.

## Review deployed resources

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Select **Resource groups** from the left pane.

1. Select the resource group that you created in the previous section. The default resource group name is **exampleRG**.

1. Select the load balancer. Its default name is the project name with **-lb** appended.

1. Copy only the IP address part of the public IP address, and then paste it into the address bar of your browser.

The browser displays the default page of the Internet Information Services (IIS) web server.

To see the load balancer distribute traffic across all three VMs, you can force a refresh of your web browser from the client machine.

## Clean up resources

When you no longer need them, delete the:

- Resource group

- Load balancer

- Related resources

Go to the Azure portal, select the resource group that contains the load balancer, and then select **Delete resource group**.

## Next steps

In this quickstart, you:

- Created a virtual network for the load balancer and virtual machines.

- Created an Azure Bastion host for management.

- Created a standard load balancer and attached VMs to it.

- Configured the load-balancer traffic rule, and the health probe.

- Tested the load balancer.

To learn more, continue to the tutorials for Azure Load Balancer.

> [!div class="nextstepaction"]

> [Azure Load Balancer tutorials](./quickstart-load-balancer-standard-public-portal.md)


# Quickstart Load Balancer Standard Public Template

# Quickstart: Create a public load balancer to load balance VMs using an ARM template

This quickstart shows you how to deploy a standard load balancer to load balance virtual machines. The load balancer distributes traffic across multiple virtual machines in a backend pool. The template also creates a virtual network, network interfaces, a NAT Gateway, and an Azure Bastion instance.

Using an ARM template takes fewer steps comparing to other deployment methods.

[!INCLUDE [About Azure Resource Manager](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-introduction.md)]

If your environment meets the prerequisites and you're familiar with using ARM templates, select the **Deploy to Azure** button. The template will open in the Azure portal.

## Prerequisites

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Review the template

The template used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/load-balancer-standard-create/).

Load balancer and public IP SKUs must match. When you create a standard load balancer, you must also create a new standard public IP address that is configured as the frontend for the standard load balancer. Microsoft recommends using standard SKU for production workloads.

Multiple Azure resources have been defined in the template:

- [**Microsoft.Network/loadBalancers**](/azure/templates/microsoft.network/loadbalancers)

- [**Microsoft.Network/publicIPAddresses**](/azure/templates/microsoft.network/publicipaddresses): for the load balancer, bastion host, and the NAT gateway.

- [**Microsoft.Network/bastionHosts**](/azure/templates/microsoft.network/bastionhosts)

- [**Microsoft.Network/networkSecurityGroups**](/azure/templates/microsoft.network/networksecuritygroups)

- [**Microsoft.Network/virtualNetworks**](/azure/templates/microsoft.network/virtualnetworks)

- [**Microsoft.Compute/virtualMachines**](/azure/templates/microsoft.compute/virtualmachines) (3).

- [**Microsoft.Network/networkInterfaces**](/azure/templates/microsoft.network/networkinterfaces) (3).

- [**Microsoft.Compute/virtualMachine/extensions**](/azure/templates/microsoft.compute/virtualmachines/extensions) (3): use to configure the Internet Information Server (IIS), and the web pages.

- [**Microsoft.Network/natGateways**](/azure/templates/microsoft.network/natgateways): for the NAT gateway.

> [!IMPORTANT]

> [!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

To find more templates that are related to Azure Load Balancer, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Network&pageNumber=1&sort=Popular).

## Deploy the template

1. Select **Try it** from the following code block to open Azure Cloud Shell, and then follow the instructions to sign in to Azure.

```azurepowershell-interactive

$projectName = Read-Host -Prompt "Enter a project name with 12 or less letters or numbers that is used to generate Azure resource names"

$location = Read-Host -Prompt "Enter the location (i.e. EastUS)"

$adminUserName = Read-Host -Prompt "Enter the virtual machine administrator account name"

$adminPassword = Read-Host -Prompt "Enter the virtual machine administrator password" -AsSecureString

$resourceGroupName = "${projectName}rg"

$templateUri = "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.network/load-balancer-standard-create/azuredeploy.json"

New-AzResourceGroup -Name $resourceGroupName -Location $location

New-AzResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateUri $templateUri -Name $projectName -location $location -adminUsername $adminUsername -adminPassword $adminPassword

Write-Host "Press [ENTER] to continue."

```

Wait until you see the prompt from the console.

1. Select **Copy** from the previous code block to copy the PowerShell script.

1. Right-click the shell console pane and then select **Paste**.

1. Enter the values.

The template deployment creates three availability zones. Availability zones are supported only in [certain regions](/azure/reliability/availability-zones-overview). Use one of the supported regions. If you aren't sure, enter **EastUS**.

The resource group name is the project name with **`rg`** appended. You need the resource group name in the next section.

It takes about 10 minutes to deploy the template. When completed, the output is similar to:

![Azure Standard Load Balancer Resource Manager template PowerShell deployment output](./media/quickstart-load-balancer-standard-public-template/azure-standard-load-balancer-resource-manager-template-powershell-output.png)

Azure PowerShell is used to deploy the template. You can also use the Azure portal, Azure CLI, and REST API. To learn other deployment methods, see [Deploy templates](../azure-resource-manager/templates/deploy-portal.md).

## Review deployed resources

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Select **Resource groups** from the left pane.

1. Select the resource group that you created in the previous section. The default resource group name is the project name with **-rg** appended.

1. Select the load balancer. Its default name is the project name with **-lb** appended.

1. Copy only the IP address part of the public IP address, and then paste it into the address bar of your browser.

![Azure standard load balancer Resource Manager template public IP](./media/quickstart-load-balancer-standard-public-template/azure-standard-load-balancer-resource-manager-template-deployment-public-ip.png)

The browser displays the default page of the Internet Information Services (IIS) web server.

![IIS web server](./media/quickstart-load-balancer-standard-public-template/load-balancer-test-web-page.png)

To see the load balancer distribute traffic across all three VMs, you can force a refresh of your web browser from the client machine.

## Clean up resources

When you no longer need them, delete the:

* Resource group

* Load balancer

* Related resources

Go to the Azure portal, select the resource group that contains the load balancer, and then select **Delete resource group**.

## Next steps

In this quickstart, you:

* Created a virtual network for the load balancer and virtual machines.

* Created an Azure Bastion host for management.

* Created a standard load balancer and attached VMs to it.

* Configured the load-balancer traffic rule, and the health probe.

* Tested the load balancer.

To learn more, continue to the tutorials for Azure Load Balancer.

> [!div class="nextstepaction"]

> [Azure Load Balancer tutorials](./quickstart-load-balancer-standard-public-portal.md)


# Quickstart Load Balancer Standard Public Terraform

# Quickstart: Create a public load balancer to load balance VMs using Terraform

This quickstart shows you how to deploy a standard load balancer to load balance virtual machines using Terraform.

[!INCLUDE [About Terraform](~/azure-dev-docs-pr/articles/terraform/includes/abstract.md)]

> [!div class="checklist"]

> * Create an Azure resource group using [azurerm_resource_group](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group)

> * Create an Azure Virtual Network using [azurerm_virtual_network](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_network)

> * Create an Azure subnet using [azurerm_subnet](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/subnet)

> * Create an Azure public IP using [azurerm_public_ip](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/public_ip)

> * Create an Azure Load Balancer using [azurerm_lb](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/lb)

> * Create an Azure network interface using [azurerm_network_interface](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_interface)

> * Create an Azure network interface load balancer backend address pool association using [azurerm_network_interface_backend_address_pool_association](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_interface_backend_address_pool_association)

> * Create an Azure Linux Virtual Machine using [azurerm_linux_virtual_machine](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/linux_virtual_machine)

> * Create an Azure Virtual Machine Extension using [azurerm_virtual_machine_extension](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_machine_extension)

## Prerequisites

- Create an Azure account with an active subscription. You can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- [Install and configure Terraform](/azure/developer/terraform/quickstart-configure)

## Implement the Terraform code

The sample code for this article is located in the [Azure Terraform GitHub repo](https://github.com/Azure/terraform/tree/master/quickstart/101-azure-load-balancer-public). You can view the log file containing the [test results from current and previous versions of Terraform](https://github.com/Azure/terraform/tree/master/quickstart/101-azure-load-balancer-public/TestRecord.md). See more [articles and sample code showing how to use Terraform to manage Azure resources](/azure/terraform)

1. Create a directory in which to test and run the sample Terraform code, and make it the current directory.

1. Create a file named `providers.tf` and insert the following code.

1. Create a file named `main.tf` and insert the following code.

1. Create a file named `variables.tf` and insert the following code.

1. Create a file named `outputs.tf` and insert the following code.

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

1. Display the Azure resource group name.

```console

terraform output -raw resource_group_name

```

1. Optionally, display the VM (virtual machine) password.

```console

terraform output -raw vm_password

```

1. Display the public IP address.

```console

terraform output -raw public_ip_address

```

1. Paste the public IP address into the address bar of your web browser. The custom VM page of the Nginx web server is displayed in the browser.

## Clean up resources

[!INCLUDE [terraform-plan-destroy.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-plan-destroy.md)]

## Troubleshoot Terraform on Azure

[Troubleshoot common problems when using Terraform on Azure](/azure/developer/terraform/troubleshoot)

## Next steps

> [!div class="nextstepaction"]

> [What is Azure Load Balancer?](load-balancer-overview.md)


# Quickstart Load Balancer Standard Internal Powershell

# Quickstart: Create an internal load balancer to load balance virtual machines using Azure PowerShell

Get started with Azure Load Balancer creating an internal load balancer and two virtual machines with Azure PowerShell. Also, you deploy other resources including Azure Bastion, NAT Gateway, a virtual network, and the required subnets.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)

- Azure PowerShell installed locally or Azure Cloud Shell

If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 5.4.1 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell). If you're running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

## Create a resource group

An Azure resource group is a logical container into which Azure resources are deployed and managed.

Create a resource group with [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup).

```azurepowershell-interactive

$rg = @{

Name = 'CreateINTLBQS-rg'

Location = 'westus2'

}

New-AzResourceGroup @rg

```

## Configure virtual network

When you create an internal load balancer, a virtual network is configured as the network for the load balancer. Before you deploy VMs and test your load balancer, create the supporting virtual network resources.

- Create a public IP for the NAT gateway

- Create a virtual network for the backend virtual machines

- Create a network security group to define inbound connections to your virtual network

- Create an Azure Bastion host to securely manage the virtual machines in the backend pool

## Create a public IP address

Use [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) to create a public IP address for the NAT gateway.

```azurepowershell-interactive

## Create public IP address for NAT gateway and place IP in variable ##

$gwpublicip = @{

Name = 'myNATgatewayIP'

ResourceGroupName = $rg.name

Location = 'westus2'

Sku = 'Standard'

AllocationMethod = 'static'

Zone = 1,2,3

}

$gwpublicip = New-AzPublicIpAddress @gwpublicip

```

To create a zonal public IP address in zone 1, use the following command:

```azurepowershell-interactive

## Create a zonal public IP address for NAT gateway and place IP in variable ##

$gwpublicip = @{

Name = 'myNATgatewayIP'

ResourceGroupName = $rg.name

Location = 'westus2'

Sku = 'Standard'

AllocationMethod = 'static'

Zone = 1

}

$gwpublicip = New-AzPublicIpAddress @gwpublicip

```

> [!NOTE]

> The public IP address is used by the NAT gateway to provide outbound connectivity for the virtual machines in the backend pool. This is recommended when you create an internal load balancer and need the backend pool resources to have outbound connectivity. For more information, see [NAT gateway](load-balancer-outbound-connections.md).

### Create virtual network, network security group, bastion host, and NAT gateway

* Create a virtual network with [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork)

* Create a network security group rule with [New-AzNetworkSecurityRuleConfig](/powershell/module/az.network/new-aznetworksecurityruleconfig)

* Create an Azure Bastion host with [New-AzBastion](/powershell/module/az.network/new-azbastion)

* Create the NAT gateway resource with [New-AzNatGateway](/powershell/module/az.network/new-aznatgateway)

* Use [New-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/new-azvirtualnetworksubnetconfig) to associate the NAT gateway to the subnet of the virtual network

> [!IMPORTANT]

> [!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

```azurepowershell-interactive

## Create NAT gateway resource ##

$nat = @{

ResourceGroupName = $rg.name

Name = 'myNATgateway'

IdleTimeoutInMinutes = '10'

Sku = 'Standard'

Location = 'westus2'

PublicIpAddress = $gwpublicip

}

$natGateway = New-AzNatGateway @nat

## Create backend subnet config ##

$subnet = @{

Name = 'myBackendSubnet'

AddressPrefix = '10.1.0.0/24'

NatGateway = $natGateway

}

$subnetConfig = New-AzVirtualNetworkSubnetConfig @subnet

## Create Azure Bastion subnet. ##

$bastsubnet = @{

Name = 'AzureBastionSubnet'

AddressPrefix = '10.1.1.0/24'

}

$bastsubnetConfig = New-AzVirtualNetworkSubnetConfig @bastsubnet

## Create the virtual network ##

$net = @{

Name = 'myVNet'

ResourceGroupName = $rg.name

Location = 'westus2'

AddressPrefix = '10.1.0.0/16'

Subnet = $subnetConfig,$bastsubnetConfig

}

$vnet = New-AzVirtualNetwork @net

## Create public IP address for bastion host. ##

$bastionip = @{

Name = 'myBastionIP'

ResourceGroupName = $rg.name

Location = 'westus2'

Sku = 'Standard'

AllocationMethod = 'Static'

}

$bastionip = New-AzPublicIpAddress @bastionip

## Create bastion host ##

$bastion = @{

ResourceGroupName = $rg.name

Name = 'myBastion'

PublicIpAddress = $bastionip

VirtualNetwork = $vnet

}

New-AzBastion @bastion -AsJob

## Create rule for network security group and place in variable. ##

$nsgrule = @{

Name = 'myNSGRuleHTTP'

Description = 'Allow HTTP'

Protocol = '*'

SourcePortRange = '*'

DestinationPortRange = '80'

SourceAddressPrefix = 'Internet'

DestinationAddressPrefix = '*'

Access = 'Allow'

Priority = '2000'

Direction = 'Inbound'

}

$rule1 = New-AzNetworkSecurityRuleConfig @nsgrule

## Create network security group ##

$nsg = @{

Name = 'myNSG'

ResourceGroupName = $rg.name

Location = 'westus2'

SecurityRules = $rule1

}

New-AzNetworkSecurityGroup @nsg

```

## Create load balancer

This section details how you can create and configure the following components of the load balancer:

* Create a frontend IP with [New-AzLoadBalancerFrontendIpConfig](/powershell/module/az.network/new-azloadbalancerfrontendipconfig) for the frontend IP pool. This IP receives the incoming traffic on the load balancer

* Create a backend address pool with [New-AzLoadBalancerBackendAddressPoolConfig](/powershell/module/az.network/new-azloadbalancerbackendaddresspoolconfig) for traffic sent from the frontend of the load balancer

* Create a health probe with [Add-AzLoadBalancerProbeConfig](/powershell/module/az.network/add-azloadbalancerprobeconfig) that determines the health of the backend VM instances

* Create a load balancer rule with [Add-AzLoadBalancerRuleConfig](/powershell/module/az.network/add-azloadbalancerruleconfig) that defines how traffic is distributed to the VMs

* Create a public load balancer with [New-AzLoadBalancer](/powershell/module/az.network/new-azloadbalancer)

```azurepowershell-interactive

## Place virtual network created in previous step into a variable. ##

$net = @{

Name = 'myVNet'

ResourceGroupName = $rg.name

}

$vnet = Get-AzVirtualNetwork @net

## Create load balancer frontend configuration and place in variable. ##

$lbip = @{

Name = 'myFrontEnd'

PrivateIpAddress = '10.1.0.4'

SubnetId = $vnet.subnets[0].Id

}

$feip = New-AzLoadBalancerFrontendIpConfig @lbip

## Create backend address pool configuration and place in variable. ##

$bepool = New-AzLoadBalancerBackendAddressPoolConfig -Name 'myBackEndPool'

## Create the health probe and place in variable. ##

$probe = @{

Name = 'myHealthProbe'

Protocol = 'tcp'

Port = '80'

IntervalInSeconds = '360'

ProbeCount = '5'

}

$healthprobe = New-AzLoadBalancerProbeConfig @probe

## Create the load balancer rule and place in variable. ##

$lbrule = @{

Name = 'myHTTPRule'

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

ResourceGroupName = $rg.name

Name = 'myLoadBalancer'

Location = 'westus2'

Sku = 'Standard'

FrontendIpConfiguration = $feip

BackendAddressPool = $bePool

LoadBalancingRule = $rule

Probe = $healthprobe

}

New-AzLoadBalancer @loadbalancer

```

## Create virtual machines

In this section, you create the two virtual machines for the backend pool of the load balancer.

* Create three network interfaces with [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface)

* Set an administrator username and password for the VMs with [Get-Credential](/powershell/module/microsoft.powershell.security/get-credential)

* Create the virtual machines with:

* [New-AzVM](/powershell/module/az.compute/new-azvm)

* [New-AzVMConfig](/powershell/module/az.compute/new-azvmconfig)

* [Set-AzVMOperatingSystem](/powershell/module/az.compute/set-azvmoperatingsystem)

* [Set-AzVMSourceImage](/powershell/module/az.compute/set-azvmsourceimage)

* [Add-AzVMNetworkInterface](/powershell/module/az.compute/add-azvmnetworkinterface)

```azurepowershell-interactive

# Set the administrator and password for the VMs. ##

$cred = Get-Credential

## Place virtual network created in previous step into a variable. ##

$net = @{

Name = 'myVNet'

ResourceGroupName = $rg.name

}

$vnet = Get-AzVirtualNetwork @net

## Place the load balancer into a variable. ##

$lb = @{

Name = 'myLoadBalancer'

ResourceGroupName = $rg.name

}

$bepool = Get-AzLoadBalancer @lb  | Get-AzLoadBalancerBackendAddressPoolConfig

## Place the network security group into a variable. ##

$sg = @{

Name = 'myNSG'

ResourceGroupName = $rg.name

}

$nsg = Get-AzNetworkSecurityGroup @sg

## For loop with variable to create virtual machines for load balancer backend pool. ##

for ($i=1; $i -le 2; $i++)

{

## Command to create network interface for VMs ##

$nic = @{

Name = "myNicVM$i"

ResourceGroupName = $rg.name

Location = 'westus2'

Subnet = $vnet.Subnets[0]

NetworkSecurityGroup = $nsg

LoadBalancerBackendAddressPool = $bepool

}

$nicVM = New-AzNetworkInterface @nic

## Create a virtual machine configuration for VMs ##

$vmsz = @{

VMName = "myVM$i"

VMSize = 'Standard_DS1_v2'

}

$vmos = @{

ComputerName = "myVM$i"

Credential = $cred

}

$vmimage = @{

PublisherName = 'MicrosoftWindowsServer'

Offer = 'WindowsServer'

Skus = '2019-Datacenter'

Version = 'latest'

}

$vmConfig = New-AzVMConfig @vmsz `

| Set-AzVMOperatingSystem @vmos -Windows `

| Set-AzVMSourceImage @vmimage `

| Add-AzVMNetworkInterface -Id $nicVM.Id

## Create the virtual machine for VMs ##

$vm = @{

ResourceGroupName = $rg.name

Location = 'westus2'

VM = $vmConfig

Zone = "$i"

}

}

New-AzVM @vm -asjob

```

The deployments of the virtual machines and bastion host are submitted as PowerShell jobs. To view the status of the jobs, use [Get-Job](/powershell/module/microsoft.powershell.core/get-job):

```azurepowershell-interactive

Get-Job

Id     Name            PSJobTypeName   State         HasMoreData     Location             Command

--     ----            -------------   -----         -----------     --------             -------

1      Long Running O… AzureLongRunni… Completed     True            localhost            New-AzBastion

2      Long Running O… AzureLongRunni… Completed     True            localhost            New-AzVM

3      Long Running O… AzureLongRunni… Completed     True            localhost            New-AzVM

```

[!INCLUDE [ephemeral-ip-note.md](~/reusable-content/ce-skilling/azure/includes/ephemeral-ip-note.md)]

## Install IIS

Use [Set-AzVMExtension](/powershell/module/az.compute/set-azvmextension) to install the Custom Script Extension.

The extension runs `PowerShell Add-WindowsFeature Web-Server` to install the IIS webserver and then updates the Default.htm page to show the hostname of the VM:

> [!IMPORTANT]

> Ensure the virtual machine deployments have completed from the previous steps before proceeding. Use `Get-Job` to check the status of the virtual machine deployment jobs.

```azurepowershell-interactive

## For loop with variable to install custom script extension on virtual machines. ##

for ($i=1; $i -le 2; $i++)

{

$ext = @{

Publisher = 'Microsoft.Compute'

ExtensionType = 'CustomScriptExtension'

ExtensionName = 'IIS'

ResourceGroupName = $rg.name

VMName = "myVM$i"

Location = 'westus2'

TypeHandlerVersion = '1.8'

SettingString = '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}'

}

Set-AzVMExtension @ext -AsJob

}

```

The extensions are deployed as PowerShell jobs. To view the status of the installation jobs, use [Get-Job](/powershell/module/microsoft.powershell.core/get-job):

```azurepowershell-interactive

Get-Job

Id     Name            PSJobTypeName   State         HasMoreData     Location             Command

--     ----            -------------   -----         -----------     --------             -------

8      Long Running O… AzureLongRunni… Running       True            localhost            Set-AzVMExtension

9      Long Running O… AzureLongRunni… Running       True            localhost            Set-AzVMExtension

```

## Create the test virtual machine

Create the virtual machine with:

* [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface)

* [New-AzVM](/powershell/module/az.compute/new-azvm)

* [New-AzVMConfig](/powershell/module/az.compute/new-azvmconfig)

* [Set-AzVMOperatingSystem](/powershell/module/az.compute/set-azvmoperatingsystem)

* [Set-AzVMSourceImage](/powershell/module/az.compute/set-azvmsourceimage)

* [Add-AzVMNetworkInterface](/powershell/module/az.compute/add-azvmnetworkinterface)

```azurepowershell-interactive

# Set the administrator and password for the VM. ##

$cred = Get-Credential

## Place the virtual network into a variable. ##

$net = @{

Name = 'myVNet'

ResourceGroupName = $rg.name

}

$vnet = Get-AzVirtualNetwork @net

## Place the network security group into a variable. ##

$sg = @{

Name = 'myNSG'

ResourceGroupName = $rg.name

}

$nsg = Get-AzNetworkSecurityGroup @sg

## Command to create network interface for VM ##

$nic = @{

Name = "myNicTestVM"

ResourceGroupName = $rg.name

Location = 'westus2'

Subnet = $vnet.Subnets[0]

NetworkSecurityGroup = $nsg

}

$nicVM = New-AzNetworkInterface @nic

## Create a virtual machine configuration for VMs ##

$vmsz = @{

VMName = "myTestVM"

VMSize = 'Standard_DS1_v2'

}

$vmos = @{

ComputerName = "myTestVM"

Credential = $cred

}

$vmimage = @{

PublisherName = 'MicrosoftWindowsServer'

Offer = 'WindowsServer'

Skus = '2019-Datacenter'

Version = 'latest'

}

$vmConfig = New-AzVMConfig @vmsz `

| Set-AzVMOperatingSystem @vmos -Windows `

| Set-AzVMSourceImage @vmimage `

| Add-AzVMNetworkInterface -Id $nicVM.Id

## Create the virtual machine for VMs ##

$vm = @{

ResourceGroupName = $rg.name

Location = 'westus2'

VM = $vmConfig

}

New-AzVM @vm

```

## Test the load balancer

1. [Sign in](https://portal.azure.com) to the Azure portal.

1. Find the private IP address for the load balancer on the **Overview** screen. Select **All services** in the left-hand menu, select **All resources**, and then select **myLoadBalancer**.

1. Make note or copy the address next to **Private IP Address** in the **Overview** of **myLoadBalancer**.

1. Select **All services** in the left-hand menu, select **All resources**, and then from the resources list, select **myTestVM** that is located in the **CreateIntLBQS-rg** resource group.

1. On the **Overview** page, select **Connect**, then **Bastion**.

1. Enter the username and password entered during VM creation.

1. Open **Internet Explorer** on **myTestVM**.

1. Enter the IP address from the previous step into the address bar of the browser. The custom IIS Web server page is displayed.

To see the load balancer distribute traffic across all three VMs, you can force-refresh your web browser from the test machine.

## Clean up resources

When no longer needed, you can use the [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) command to remove the resource group, load balancer, and the remaining resources.

```azurepowershell-interactive

Remove-AzResourceGroup -Name $rg.name

```

## Next steps

In this quickstart:

* You created an internal load balancer

* Attached virtual machines

* Configured the load balancer traffic rule and health probe

* Tested the load balancer

To learn more about Azure Load Balancer, continue to:

> [!div class="nextstepaction"]

> [What is Azure Load Balancer?](load-balancer-overview.md)


# Quickstart Load Balancer Standard Internal Cli

# Quickstart: Create an internal load balancer to load balance VMs using the Azure CLI

Get started with Azure Load Balancer by using the Azure CLI to create an internal load balancer and two virtual machines. Other resources include Azure Bastion, NAT Gateway, a virtual network, and the required subnets.

[!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment.md)]

- This quickstart requires version 2.0.28 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed.

## Create a resource group

An Azure resource group is a logical container into which you deploy and manage your Azure resources.

Create a resource group with [az group create](/cli/azure/group#az-group-create).

```azurecli-interactive

az group create \

--name CreateIntLBQS-rg \

--location westus2

```

When you create an internal load balancer, a virtual network is configured as the network for the load balancer.

## Create the virtual network

Before you deploy VMs and test your load balancer, create the supporting virtual network and subnet. The virtual network and subnet contain the resources deployed later in this article.

Create a virtual network by using [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create).

```azurecli-interactive

az network vnet create \

--resource-group CreateIntLBQS-rg \

--location westus2 \

--name myVNet \

--address-prefixes 10.1.0.0/16 \

--subnet-name myBackendSubnet \

--subnet-prefixes 10.1.0.0/24

```

## Create an Azure Bastion host

In this example, you create an Azure Bastion host. The Azure Bastion host is used later in this article to securely manage the virtual machines and test the load balancer deployment.

> [!IMPORTANT]

> [!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

### Create a bastion public IP address

Use [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create) to create a public IP address for the Azure Bastion host.

```azurecli-interactive

az network public-ip create \

--resource-group CreateIntLBQS-rg  \

--name myBastionIP \

--sku Standard \

--zone 1 2 3

```

### Create a bastion subnet

Use [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-create) to create a subnet.

```azurecli-interactive

az network vnet subnet create \

--resource-group CreateIntLBQS-rg  \

--name AzureBastionSubnet \

--vnet-name myVNet \

--address-prefixes 10.1.1.0/27

```

### Create the bastion host

Use [az network bastion create](/cli/azure/network/bastion#az-network-bastion-create) to create a host.

```azurecli-interactive

az config set extension.use_dynamic_install=yes_without_prompt

az network bastion create \

--resource-group CreateIntLBQS-rg  \

--name myBastionHost \

--public-ip-address myBastionIP \

--vnet-name myVNet \

--location westus2 \

--sku Basic \

--only-show-errors \

--no-wait

```

It can take a few minutes for the Azure Bastion host to deploy.

## Create the load balancer

This section details how you can create and configure the following components of the load balancer:

* A frontend IP pool that receives the incoming network traffic on the load balancer

* A backend IP pool where the frontend pool sends the load balanced network traffic

* A health probe that determines health of the backend VM instances

* A load balancer rule that defines how traffic is distributed to the VMs

### Create the load balancer resource

Create an internal load balancer with [az network lb create](/cli/azure/network/lb#az-network-lb-create).

```azurecli-interactive

az network lb create \

--resource-group CreateIntLBQS-rg \

--name myLoadBalancer \

--sku Standard \

--vnet-name myVNet \

--subnet myBackendSubnet \

--backend-pool-name myBackEndPool \

--frontend-ip-name myFrontEnd

```

### Create the health probe

A health probe checks all virtual machine instances to ensure they can send network traffic.

A virtual machine with a failed probe check is removed from the load balancer. The virtual machine is added back into the load balancer when the failure is resolved.

Create a health probe with [az network lb probe create](/cli/azure/network/lb/probe#az-network-lb-probe-create).

```azurecli-interactive

az network lb probe create \

--resource-group CreateIntLBQS-rg \

--lb-name myLoadBalancer \

--name myHealthProbe \

--protocol tcp \

--port 80

```

### Create a load balancer rule

A load balancer rule defines:

* Frontend IP configuration for the incoming traffic

* The backend IP pool to receive the traffic

* The required source and destination port

Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#az-network-lb-rule-create).

```azurecli-interactive

az network lb rule create \

--resource-group CreateIntLBQS-rg \

--lb-name myLoadBalancer \

--name myHTTPRule \

--protocol tcp \

--frontend-port 80 \

--backend-port 80 \

--frontend-ip-name myFrontEnd \

--backend-pool-name myBackEndPool \

--probe-name myHealthProbe \

--idle-timeout 15 \

--enable-tcp-reset true

```

## Create a network security group

For a standard load balancer, the VMs in the backend pool are required to have network interfaces that belong to a network security group.

To create a network security group, use [az network nsg create](/cli/azure/network/nsg#az-network-nsg-create).

```azurecli-interactive

az network nsg create \

--resource-group CreateIntLBQS-rg \

--name myNSG

```

## Create a network security group rule

To create a network security group rule, use [az network nsg rule create](/cli/azure/network/nsg/rule#az-network-nsg-rule-create).

```azurecli-interactive

az network nsg rule create \

--resource-group CreateIntLBQS-rg \

--nsg-name myNSG \

--name myNSGRuleHTTP \

--protocol '*' \

--direction inbound \

--source-address-prefix '*' \

--source-port-range '*' \

--destination-address-prefix '*' \

--destination-port-range 80 \

--access allow \

--priority 200

```

## Create backend servers

In this section, you create:

* Two network interfaces for the virtual machines

* Two virtual machines to be used as servers for the load balancer

### Create network interfaces for the virtual machines

Create two network interfaces with [az network nic create](/cli/azure/network/nic#az-network-nic-create).

```azurecli-interactive

array=(myNicVM1 myNicVM2)

for vmnic in "${array[@]}"

do

az network nic create \

--resource-group CreateIntLBQS-rg \

--name $vmnic \

--vnet-name myVNet \

--subnet myBackEndSubnet \

--network-security-group myNSG

done

```

### Create the virtual machines

Create the virtual machines with [az vm create](/cli/azure/vm#az-vm-create).

```azurecli-interactive

array=(1 2)

for n in "${array[@]}"

do

az vm create \

--resource-group CreateIntLBQS-rg \

--name myVM$n \

--nics myNicVM$n \

--image win2022datacenter \

--admin-username azureuser \

--zone $n \

--no-wait

done

```

It can take a few minutes for the VMs to deploy.

[!INCLUDE [ephemeral-ip-note.md](~/reusable-content/ce-skilling/azure/includes/ephemeral-ip-note.md)]

## Add virtual machines to the backend pool

Add the virtual machines to the backend pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#az-network-nic-ip-config-address-pool-add).

```azurecli-interactive

array=(VM1 VM2)

for vm in "${array[@]}"

do

az network nic ip-config address-pool add \

--address-pool myBackendPool \

--ip-config-name ipconfig1 \

--nic-name myNic$vm \

--resource-group CreateIntLBQS-rg \

--lb-name myLoadBalancer

done

```

## Create NAT gateway

To provide outbound internet access for resources in the backend pool, create a NAT gateway.

### Create public IP

Use [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create) to create a single IP for the outbound connectivity.

```azurecli-interactive

az network public-ip create \

--resource-group CreateIntLBQS-rg \

--name myNATgatewayIP \

--sku Standard \

--zone 1 2 3

```

### Create NAT gateway resource

Use [az network nat gateway create](/cli/azure/network/nat#az-network-nat-gateway-create) to create the NAT gateway resource. The public IP created in the previous step is associated with the NAT gateway.

```azurecli-interactive

az network nat gateway create \

--resource-group CreateIntLBQS-rg \

--name myNATgateway \

--public-ip-addresses myNATgatewayIP \

--idle-timeout 10

```

### Associate NAT gateway with subnet

Configure the source subnet in virtual network to use a specific NAT gateway resource with [az network vnet subnet update](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-update).

```azurecli-interactive

az network vnet subnet update \

--resource-group CreateIntLBQS-rg \

--vnet-name myVNet \

--name myBackendSubnet \

--nat-gateway myNATgateway

```

## Create test virtual machine

Create the network interface with [az network nic create](/cli/azure/network/nic#az-network-nic-create).

```azurecli-interactive

az network nic create \

--resource-group CreateIntLBQS-rg \

--name myNicTestVM \

--vnet-name myVNet \

--subnet myBackEndSubnet \

--network-security-group myNSG

```

Create the virtual machine with [az vm create](/cli/azure/vm#az-vm-create).

```azurecli-interactive

az vm create \

--resource-group CreateIntLBQS-rg \

--name myTestVM \

--nics myNicTestVM \

--image Win2019Datacenter \

--admin-username azureuser \

--no-wait

```

You might need to wait a few minutes for the virtual machine to deploy.

## Install IIS

Use [az vm extension set](/cli/azure/vm/extension#az-vm-extension-set) to install IIS on the backend virtual machines and set the default website to the computer name.

```azurecli-interactive

array=(myVM1 myVM2)

for vm in "${array[@]}"

do

az vm extension set \

--publisher Microsoft.Compute \

--version 1.8 \

--name CustomScriptExtension \

--vm-name $vm \

--resource-group CreateIntLBQS-rg \

--settings '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}'

done

```

## Test the load balancer

1. [Sign in](https://portal.azure.com) to the Azure portal.

1. On the **Overview** page, find the private IP address for the load balancer. In the menu on the left, select **All services** > **All resources** > **myLoadBalancer**.

1. In the overview of **myLoadBalancer**, copy the address next to **Private IP Address**. If **Private IP address** isn't visible, select **See more**.

1. In the menu on the left, select **All services** > **All resources**. From the resources list, in the **CreateIntLBQS-rg** resource group, select **myTestVM**.

1. On the **Overview** page, select **Connect** > **Bastion**.

1. Enter the username and password that you entered when you created the VM.

1. On **myTestVM**, open **Internet Explorer**.

1. Enter the IP address from the previous step into the address bar of the browser. The default page of the IIS web server is shown on the browser.

## Clean up resources

When your resources are no longer needed, use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, load balancer, and all related resources.

```azurecli-interactive

az group delete \

--name CreateIntLBQS-rg

```

## Next steps

In this quickstart:

* You created an internal load balancer

* Attached two virtual machines

* Configured the load balancer traffic rule and health probe

* Tested the load balancer

To learn more about Azure Load Balancer, continue to:

> [!div class="nextstepaction"]

> [What is Azure Load Balancer?](load-balancer-overview.md)


# Quickstart Load Balancer Standard Internal Bicep

# Quickstart: Create an internal load balancer to load balance VMs using Bicep

In this quickstart, you learn to use a Bicep file to create an internal Azure load balancer. The internal load balancer distributes traffic to virtual machines in a virtual network located in the load balancer's backend pool. Along with the internal load balancer, this template creates a virtual network, network interfaces, a NAT Gateway, and an Azure Bastion instance.

[!INCLUDE [About Bicep](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-bicep-introduction.md)]

## Prerequisites

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Review the Bicep file

The Bicep file used in this quickstart is from the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates/blob/master/quickstarts/microsoft.network/internal-loadbalancer-create/main.bicep).

Multiple Azure resources have been defined in the Bicep file:

- [**Microsoft.Network/virtualNetworks**](/azure/templates/microsoft.network/virtualNetworks): Virtual network for load balancer and virtual machines.

- [**Microsoft.Network/networkInterfaces**](/azure/templates/microsoft.network/networkInterfaces): Network interfaces for virtual machines.

- [**Microsoft.Network/loadBalancers**](/azure/templates/microsoft.network/loadBalancers): Internal load balancer.

- [**Microsoft.Network/natGateways**](/azure/templates/microsoft.network/natGateways)

- [**Microsoft.Network/publicIPAddresses**](/azure/templates/microsoft.network/publicipaddresses): Public IP addresses for the NAT Gateway and Azure Bastion.

- [**Microsoft.Compute/virtualMachines**](/azure/templates/microsoft.compute/virtualmachines): Virtual machines in the backend pool.

- [**Microsoft.Network/bastionHosts**](/azure/templates/microsoft.network/bastionhosts): Azure Bastion instance.

- [**Microsoft.Network/virtualNetworks/subnets**](/azure/templates/microsoft.network/virtualnetworks/subnets): Subnets for the virtual network.

- [**Microsoft.Storage/storageAccounts**](/azure/templates/microsoft.storage/storageaccounts): Storage account for the virtual machines.

## Deploy the Bicep file

1. Save the Bicep file as **main.bicep** to your local computer.

1. Deploy the Bicep file using either Azure CLI or Azure PowerShell.

# [CLI](#tab/CLI)

```azurecli

az group create --name exampleRG --location eastus

az deployment group create --resource-group exampleRG --template-file main.bicep --parameters adminUsername=AzureAdmin

```

# [PowerShell](#tab/PowerShell)

```azurepowershell

New-AzResourceGroup -Name exampleRG -Location eastus

New-AzResourceGroupDeployment -ResourceGroupName exampleRG -TemplateFile ./main.bicep -adminUsername "<admin-user>"

```

---

> [!NOTE]

> Replace **\<admin-user\>** with the admin username. You'll also be prompted to enter **adminPassword**.

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

## Clean up resources

When no longer needed, use the Azure portal, Azure CLI, or Azure PowerShell to delete the resource group and its resources.

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

For a step-by-step tutorial that guides you through the process of creating a Bicep file, see:

> [!div class="nextstepaction"]

> [Quickstart: Create Bicep files with Visual Studio Code](../azure-resource-manager/bicep/quickstart-create-bicep-use-visual-studio-code.md)


# Quickstart Load Balancer Standard Internal Template

# Quickstart: Create an internal load balancer to load balance VMs using an ARM template

In this quickstart, you learn to use an Azure Resource Manager template (ARM template) to create an internal Azure load balancer. The internal load balancer distributes traffic to virtual machines in a virtual network located in the load balancer's backend pool. Along with the internal load balancer, this template creates a virtual network, network interfaces, a NAT Gateway, and an Azure Bastion instance.

Using an ARM template takes fewer steps comparing to other deployment methods.

[!INCLUDE [About Azure Resource Manager](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-introduction.md)]

If your environment meets the prerequisites and you're familiar with using ARM templates, select the **Deploy to Azure** button. The template opens in the Azure portal.

## Prerequisites

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Review the template

The template used in this quickstart is from the [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/internal-loadbalancer-create/).

Multiple Azure resources have been defined in the template:

- [**Microsoft.Network/virtualNetworks**](/azure/templates/microsoft.network/virtualNetworks): Virtual network for load balancer and virtual machines.

- [**Microsoft.Network/networkInterfaces**](/azure/templates/microsoft.network/networkInterfaces): Network interfaces for virtual machines.

- [**Microsoft.Network/loadBalancers**](/azure/templates/microsoft.network/loadBalancers): Internal load balancer.

- [**Microsoft.Network/natGateways**](/azure/templates/microsoft.network/natGateways)

- [**Microsoft.Network/publicIPAddresses**](/azure/templates/microsoft.network/publicipaddresses): Public IP addresses for the NAT Gateway and Azure Bastion.

- [**Microsoft.Compute/virtualMachines**](/azure/templates/microsoft.compute/virtualmachines): Virtual machines in the backend pool.

- [**Microsoft.Network/bastionHosts**](/azure/templates/microsoft.network/bastionhosts): Azure Bastion instance.

- [**Microsoft.Network/virtualNetworks/subnets**](/azure/templates/microsoft.network/virtualnetworks/subnets): Subnets for the virtual network.

- [**Microsoft.Storage/storageAccounts**](/azure/templates/microsoft.storage/storageaccounts): Storage account for the virtual machines.

To find more templates that are related to Azure Load Balancer, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Network&pageNumber=1&sort=Popular).

## Deploy the template

In this step, you deploy the template using Azure PowerShell with the [New-AzResourceGroupDeployment](/powershell/module/az.resources/new-azresourcegroupdeployment) command.

1. Select **Try it** from the following code block to open Azure Cloud Shell, and then follow the instructions to sign in to Azure.

1. Deploy the Bicep file using either Azure CLI or Azure PowerShell.

# [CLI](#tab/CLI)

```azurecli

echo "Enter a project name with 12 or less letters or numbers that is used to generate Azure resource names"

read projectName

echo "Enter the location (i.e. centralus)"

read location

resourceGroupName="${projectName}rg"

templateUri="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.network/internal-loadbalancer-create/azuredeploy.json"

az group create --name $resourceGroupName --location $location

az deployment group create --resource-group $resourceGroupName --template-uri $templateUri --name $projectName --parameters location=$location

read -p "Press [ENTER] to continue."

```

# [PowerShell](#tab/PowerShell)

```azurepowershell

$projectName = Read-Host -Prompt "Enter a project name with 12 or less letters or numbers that is used to generate Azure resource names"

$location = Read-Host -Prompt "Enter the location (i.e. centralus)"

$resourceGroupName = "${projectName}rg"

$templateUri = "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.network/internal-loadbalancer-create/azuredeploy.json"

New-AzResourceGroup -Name $resourceGroupName -Location $location

New-AzResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateUri $templateUri -Name $projectName -location $location

Write-Host "Press [ENTER] to continue."

```

---

You're prompted to enter the following values:

- **projectName**: used for generating resource names.

- **adminUsername**: virtual machine administrator username.

- **adminPassword**: virtual machine administrator password.

It takes about 10 minutes to deploy the template.

Azure PowerShell or Azure CLI is used to deploy the template. You can also use the Azure portal and REST API. To learn other deployment methods, see [Deploy templates](../azure-resource-manager/templates/deploy-portal.md).

## Review deployed resources

Use Azure CLI or Azure PowerShell to list the deployed resources in the resource group with the following commands:

# [CLI](#tab/CLI)

```azurecli-interactive

az resource list --resource-group $resourceGroupName

```

# [PowerShell](#tab/PowerShell)

```azurepowershell-interactive

Get-AzResource -ResourceGroupName $resourceGroupName

```

---

## Clean up resources

When no longer needed, use Azure CLI or Azure PowerShell to delete the resource group and its resources with the following commands:

# [CLI](#tab/CLI)

```azurecli-interactive

Remove-AzResourceGroup -Name "${projectName}rg"

```

# [PowerShell](#tab/PowerShell)

```azurepowershell-interactive

Remove-AzResourceGroup -Name CreateIntLBQS-rg

```

---

## Next steps

For a step-by-step tutorial that guides you through the process of creating a template, see:

> [!div class="nextstepaction"]

> [Tutorial: Create and deploy your first ARM template](../azure-resource-manager/templates/template-tutorial-create-first-template.md)


# Quickstart Load Balancer Standard Internal Terraform

# Quickstart: Create an internal load balancer to load balance internal traffic to VMs using Terraform

This quickstart shows you how to deploy a standard internal load balancer and two virtual machines using Terraform. Additional resources include Azure Bastion, NAT Gateway, a virtual network, and the required subnets.

[!INCLUDE [About Terraform](~/azure-dev-docs-pr/articles/terraform/includes/abstract.md)]

> [!div class="checklist"]

> * Create an Azure resource group using [azurerm_resource_group](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group)

> * Create an Azure Virtual Network using [azurerm_virtual_network](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_network)

> * Create an Azure subnet using [azurerm_subnet](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/subnet)

> * Create an Azure public IP using [azurerm_public_ip](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/public_ip)

> * Create an Azure Load Balancer using [azurerm_lb](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/lb)

> * Create an Azure network interface using [azurerm_network_interface](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_interface)

> * Create an Azure network interface load balancer backend address pool association using [azurerm_network_interface_backend_address_pool_association](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_interface_backend_address_pool_association)

> * Create an Azure Linux Virtual Machine using [azurerm_linux_virtual_machine](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/linux_virtual_machine)

> * Create an Azure Virtual Machine Extension using [azurerm_virtual_machine_extension](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_machine_extension)

> * Create an Azure NAT Gateway using [azurerm_nat_gateway](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/nat_gateway)

> * Create an Azure Bastion using [azurerm_bastion_host](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/bastion_host)

## Prerequisites

- Create an Azure account with an active subscription. You can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- [Install and configure Terraform](/azure/developer/terraform/quickstart-configure)

## Implement the Terraform code

The sample code for this article is located in the [Azure Terraform GitHub repo](https://github.com/Azure/terraform/tree/master/quickstart/101-azure-load-balancer-internal). You can view the log file containing the [test results from current and previous versions of Terraform](https://github.com/Azure/terraform/tree/master/quickstart/101-azure-load-balancer-internal/TestRecord.md). See more [articles and sample code showing how to use Terraform to manage Azure resources](/azure/terraform)

1. Create a directory in which to test and run the sample Terraform code, and make it the current directory.

1. Create a file named `providers.tf` and insert the following code.

1. Create a file named `main.tf` and insert the following code.

1. Create a file named `variables.tf` and insert the following code.

1. Create a file named `outputs.tf` and insert the following code.

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

1. Display the Azure resource group name.

```console

terraform output -raw resource_group_name

```

1. Optionally, display the VM (virtual machine) password.

```console

terraform output -raw vm_password

```

1. Display the frontend private IP address.

```console

terraform output -raw private_ip_address

```

1. Log in to the VM that isn't associated with the backend pool of the load balancer using Bastion.

1. Run the curl command to access the custom web page of the Nginx web server using the frontend private IP address of the load balancer.

```

curl http://<Frontend IP address>

```

## Clean up resources

[!INCLUDE [terraform-plan-destroy.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-plan-destroy.md)]

## Troubleshoot Terraform on Azure

[Troubleshoot common problems when using Terraform on Azure](/azure/developer/terraform/troubleshoot)

## Next steps

> [!div class="nextstepaction"]

> [What is Azure Load Balancer?](load-balancer-overview.md)


# Gateway Partners

# Azure Gateway Load Balancer partners

Azure has a growing ecosystem of partners offering their network appliances for use with Gateway Load Balancer.

## Partners

### A10 Networks

"Protecting enterprise workloads from DDoS attacks has become a must as organizations are migrating to the cloud alongside a rise in complexity, intensity, and frequency of attacks. With Azure Gateway Load Balancer, customers can now inject A10's Thunder Virtual Appliance, on top of Azure's DDoS Protection to offer improved L3-7 protection for latency sensitive workloads. Azure Gateway Load Balancer is setting a new precedent by simplifying the injection of L7 DDoS appliances in the path, providing transparent flow (bump in the wire) using an overlay network with low latency, preserving the health of the host and the network virtual appliances during the DDoS attacks."

**John Hofdahl - Area Vice President, Cloud Service Provider Team**

[Learn more](https://www.a10networks.com/blog/introducing-l3-7-ddos-protection-for-microsoft-azure-tenants/)

### Check Point

"Check Point CloudGuard Network Security now integrates with Azure Gateway Load Balancer, providing customers a simplified experience—enabling them to deploy, scale, and manage CloudGuard security gateways with ease. With this collaboration, CloudGuard users can deploy industry-leading advanced threat protection and traffic inspection, automated, everywhere and without any manual routing configuration."

**TJ Gonen - Head of Cloud Product Line at Check Point**

[Learn more](https://blog.checkpoint.com/2021/11/02/check-point-cloudguard-is-a-launch-partner-of-azure-gateway-load-balancer/)

### Cisco

"Enabling Cisco Secure Firewall with Azure Gateway Load Balancer is a great opportunity for customers looking for scalable firewalls in their public cloud workloads. It's another great step towards harmonizing security across public cloud and hybrid-cloud environments. Customers no longer have to worry about re-architecting with Azure Gateway Load Balancer – all you have to do is insert or remove Secure Firewall where you need it, for either incoming or outgoing traffic. We look forward to seeing customers benefit from reduced operational complexity, high availability, and rapid scalability."

**Justin Buchanan Sr. - Director, Product Management**

[Learn more](https://blogs.cisco.com/security/cisco-secure-firewall-to-support-microsoft-azure-gateway-load-balancer)

### Citrix

"The combination of the new Azure Gateway Load Balancer with Citrix ADCs provides unparalleled scalability, supporting services across multiple regions and making it simple to insert advanced Layer 7 features provided by the Citrix ADC platform including WAF, LB, CS, L7 DDoS, and bot protection. With Azure Gateway Load Balancer's integration with Citrix ADCs, customers gain the flexibility of easily adding or removing network appliances as their needs evolve."

**Gopinath Durairaj - Sr. Director, Product Management**

### cPacket Networks

"Together with Azure Gateway Load Balancer and the cPacket cCloud Visibility Suite, customers can quickly deploy scalable cloud observability for network-aware service assurance and security delivery. Customers now have the power to observe and troubleshoot application vs. network, connection, and security threat issues with load-balanced network traffic or even broker mirrored packet data to multiple destinations."

**Brendan O’Flaherty - CEO**

[Learn more](https://www.cpacket.com/)

### F5

"With Azure Gateway Load Balancer integration, organizations can easily consume application security and delivery solutions provided by F5. App teams can seamlessly enable sophisticated BIG-IP traffic protection with just one action or API call. Through a growing set of integrations, F5 and Microsoft customers can better secure and protect their infrastructure with F5 BIG-IP and Azure Gateway Load Balancer."

**Nicolas Ménant - Director, Product Management Automation & Ecosystems**

[Learn more](https://community.f5.com/t5/technical-articles/big-ip-integration-with-azure-gateway-load-balancer/ta-p/291102)

### Fortinet

"Securing your data and applications with Fortinet in Azure is easier than ever now that Azure Gateway Load Balancer supports transparent service chaining. With the combination of FortiGate-VM and Azure GWLB, all traffic destined to customer networks can be inspected before reaching their backend application, with high scalability and without introducing any management overhead in both existing and greenfield environments."

**Ali Bidabadi - Senior Director, Global Cloud Consulting & Architecture**

[Learn more](https://www.fortinet.com/content/dam/fortinet/assets/solutions/azure/QSG-FortiWeb-for-Microsoft-Azure-Quick-Start-Guide.pdf)

### Glasnostic

"Glasnostic is proud to be a partner for Azure Gateway Load Balancer. With Azure's new Gateway Load Balancer, using Glasnostic to make applications reliable and secure couldn't be any easier. Adding Glasnostic as an NVA to your Azure deployments provides you instantly with the holistic visibility and control you need to optimize performance, maximize reliability, and enforce security."

**Tobias Kunze - Co-founder & CEO**

### Palo Alto Networks

"As organizations move towards the cloud, networking security is an essential aspect of managing and scaling applications. We're excited to empower our customers with the ability to help protect their Azure deployments with our collaboration. Palo Alto Networks' integration of VM-Series virtual firewalls with Azure Gateway Load Balancer protects your workloads from network-based threats, all while maintaining the integrity of traffic packet headers and payload."

**Mukesh Gupta - VP, Product Management, Software Firewalls (VM-Series/CN-Series)**

[Learn more](https://www.paloaltonetworks.com/blog/network-security/vm-series-azure-gateway-load-balancer/)

### Trend Micro

"As a partner for Azure Gateway Load Balancer, we're excited to provide layered security that easily integrates with your existing architectures. Deep packet inspection, log files, and transparent integration are just a few of the features that chaining Trend Micro Cloud One – Network Security with Azure Gateway Load Balancer can provide for your applications."

**Blake Sutherland - Vice President**

[Learn more](https://www.trendmicro.com/en_us/research/21/k/azure-network-layer-security.html)

### Valtix

"Azure Gateway Load Balancer makes it easy for our customers to protect their outbound traffic by deploying Valtix Gateways in the traffic path, without any manual route configuration. With this collaboration, Valtix Gateways can be service chained to Azure Gateway Load Balancer to provide advanced network security with just one step. Customers can now actually focus on security with dynamic tag-based policies rather than spend lots of time on deployment."

**Jigar Shah - Vice President of Products**

[Learn more](https://valtix.com/blog/valtix-azure-gwlb-announcement/)

## Next steps

- [Create a Azure Gateway Load Balancer](tutorial-create-gateway-load-balancer.md)

- [What is Azure Gateway Load Balancer?](gateway-overview.md)


# Tutorial Create Gateway Load Balancer

# Tutorial: Create a gateway load balancer

Azure Load Balancer consists of Standard, Basic, and Gateway SKUs. Gateway Load Balancer is used for transparent insertion of Network Virtual Appliances (NVA). Use Gateway Load Balancer for scenarios that require high performance and high scalability of NVAs.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create virtual network.

> * Create network security group.

> * Create a gateway load balancer.

> * Chain a load balancer frontend to gateway load balancer.

You can choose to create a gateway load balancer using the Azure portal, Azure CLI, or Azure PowerShell.

## Prerequisites

# [Azure portal](#tab/azureportal)

- An Azure subscription. If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

- Two **standard** sku Azure Load Balancers with backend pools deployed in two different Azure regions.

- For information on creating a regional standard load balancer and virtual machines for backend pools, see [Quickstart: Create a public load balancer to load balance VMs using the Azure portal](quickstart-load-balancer-standard-public-portal.md).

# [Azure CLI](#tab/azurecli/)

[!INCLUDE [azure-cli-prepare-your-environment-no-header.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment-no-header.md)]

- This tutorial requires version 2.0.28 or later of the Azure CLI. If using Azure Cloud Shell, the latest version is already installed.

- An Azure account with an active subscription.[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An existing public standard SKU Azure Load Balancer. For more information on creating a load balancer, see **[Create a public load balancer using the Azure CLI](quickstart-load-balancer-standard-public-cli.md)**.

- For the purposes of this tutorial, the existing load balancer in the examples is named **myLoadBalancer**.

# [Azure PowerShell](#tab/azurepowershell/)

- An Azure account with an active subscription.[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An existing public standard SKU Azure Load Balancer. For more information on creating a load balancer, see **[Create a public load balancer using Azure PowerShell](quickstart-load-balancer-standard-public-powershell.md)**.

- For the purposes of this tutorial, the existing load balancer in the examples is named **myLoadBalancer**.

- Azure PowerShell installed locally or Azure Cloud Shell

If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 5.4.1 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell). If you're running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

---

## Create a virtual network and associated resources

# [Azure portal](#tab/azureportal)

[!INCLUDE [load-balancer-create-no-gateway](../../includes/load-balancer-create-no-gateway.md)]

# [Azure CLI](#tab/azurecli/)

The following sections describe how to create a virtual network and associated resources. The virtual network is needed for the resources that are in the backend pool of the gateway load balancer.

The resources include a bastion host, network security group, and network security group rules.

### Create a resource group

An Azure resource group is a logical container into which Azure resources are deployed and managed.

Create a resource group with [az group create](/cli/azure/group#az-group-create):

```azurecli-interactive

az group create \

--name TutorGwLB-rg \

--location eastus

```

## Create virtual network

A virtual network is needed for the resources that are in the backend pool of the gateway load balancer.

Use [az network virtual network create](/cli/azure/network/vnet#az-network-vnet-create) to create the virtual network.

```azurecli-interactive

az network vnet create \

--resource-group TutorGwLB-rg \

--location eastus \

--name myVNet \

--address-prefixes 10.1.0.0/16 \

--subnet-name myBackendSubnet \

--subnet-prefixes 10.1.0.0/24

```

## Create bastion public IP address

Use [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create) to create a public IP address for the Azure Bastion host

```azurecli-interactive

az network public-ip create \

--resource-group TutorGwLB-rg \

--name myBastionIP \

--sku Standard \

--zone 1 2 3

```

## Create bastion subnet

Use [az network vnet subnet create](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-create) to create the bastion subnet.

```azurecli-interactive

az network vnet subnet create \

--resource-group TutorGwLB-rg \

--name AzureBastionSubnet \

--vnet-name myVNet \

--address-prefixes 10.1.1.0/27

```

## Create bastion host

Use [az network bastion create](/cli/azure/network/bastion#az-network-bastion-create) to deploy a bastion host for secure management of resources in virtual network.

```azurecli-interactive

az network bastion create \

--resource-group TutorGwLB-rg \

--name myBastionHost \

--public-ip-address myBastionIP \

--vnet-name myVNet \

--location eastus

```

It can take a few minutes for the Azure Bastion host to deploy.

> [!IMPORTANT]

> [!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

## Create NSG

Use the following example to create a network security group. You configure the NSG rules needed for network traffic in the virtual network created previous

Use [az network nsg create](/cli/azure/network/nsg#az-network-nsg-create) to create the NSG.

```azurecli-interactive

az network nsg create \

--resource-group TutorGwLB-rg \

--name myNSG

```

## Create NSG Rules

Use [az network nsg rule create](/cli/azure/network/nsg/rule#az-network-nsg-rule-create) to create rules for the NSG.

```azurecli-interactive

az network nsg rule create \

--resource-group TutorGwLB-rg \

--nsg-name myNSG \

--name myNSGRule-AllowAll \

--protocol '*' \

--direction inbound \

--source-address-prefix '0.0.0.0/0' \

--source-port-range '*' \

--destination-address-prefix '0.0.0.0/0' \

--destination-port-range '*' \

--access allow \

--priority 100

az network nsg rule create \

--resource-group TutorGwLB-rg \

--nsg-name myNSG \

--name myNSGRule-AllowAll-TCP-Out \

--protocol 'TCP' \

--direction outbound \

--source-address-prefix '0.0.0.0/0' \

--source-port-range '*' \

--destination-address-prefix '0.0.0.0/0' \

--destination-port-range '*' \

--access allow \

--priority 100

```

# [Azure PowerShell](#tab/azurepowershell/)

The following sections describe how to create a virtual network and associated resources. The virtual network is needed for the resources that are in the backend pool of the gateway load balancer.

The resources include a bastion host, network security group, and network security group rules.

## Create a resource group

An Azure resource group is a logical container into which Azure resources are deployed and managed.

Create a resource group with [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup):

```azurepowershell-interactive

New-AzResourceGroup -Name 'TutorGwLB-rg' -Location 'eastus'

```

## Create virtual network

A virtual network is needed for the resources that are in the backend pool of the gateway load balancer. Use [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork) to create the virtual network. Use [New-AzBastion](/powershell/module/az.network/new-azbastion) to deploy a bastion host for secure management of resources in virtual network.

> [!IMPORTANT]

> [!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

>

```azurepowershell-interactive

## Create backend subnet config ##

$subnet = @{

Name = 'myBackendSubnet'

AddressPrefix = '10.1.0.0/24'

}

$subnetConfig = New-AzVirtualNetworkSubnetConfig @subnet

## Create Azure Bastion subnet. ##

$bastsubnet = @{

Name = 'AzureBastionSubnet'

AddressPrefix = '10.1.1.0/24'

}

$bastsubnetConfig = New-AzVirtualNetworkSubnetConfig @bastsubnet

## Create the virtual network ##

$net = @{

Name = 'myVNet'

ResourceGroupName = 'TutorGwLB-rg'

Location = 'eastus'

AddressPrefix = '10.1.0.0/16'

Subnet = $subnetConfig,$bastsubnetConfig

}

$vnet = New-AzVirtualNetwork @net

## Create public IP address for bastion host. ##

$ip = @{

Name = 'myBastionIP'

ResourceGroupName = 'TutorGwLB-rg'

Location = 'eastus'

Sku = 'Standard'

AllocationMethod = 'Static'

}

$publicip = New-AzPublicIpAddress @ip

## Create bastion host ##

$bastion = @{

ResourceGroupName = 'TutorGwLB-rg'

Name = 'myBastion'

PublicIpAddress = $publicip

VirtualNetwork = $vnet

}

New-AzBastion @bastion -AsJob

```

## Create NSG

Use the following example to create a network security group. You configure the NSG rules needed for network traffic in the virtual network created previously.

Use [New-AzNetworkSecurityRuleConfig](/powershell/module/az.network/new-aznetworksecurityruleconfig) to create rules for the NSG. Use [New-AzNetworkSecurityGroup](/powershell/module/az.network/new-aznetworksecuritygroup) to create the NSG.

```azurepowershell-interactive

## Create rule for network security group and place in variable. ##

$nsgrule1 = @{

Name = 'myNSGRule-AllowAll'

Description = 'Allow all'

Protocol = '*'

SourcePortRange = '*'

DestinationPortRange = '*'

SourceAddressPrefix = '0.0.0.0/0'

DestinationAddressPrefix = '0.0.0.0/0'

Access = 'Allow'

Priority = '100'

Direction = 'Inbound'

}

$rule1 = New-AzNetworkSecurityRuleConfig @nsgrule1

$nsgrule2 = @{

Name = 'myNSGRule-AllowAll-TCP-Out'

Description = 'Allow all TCP Out'

Protocol = 'TCP'

SourcePortRange = '*'

DestinationPortRange = '*'

SourceAddressPrefix = '0.0.0.0/0'

DestinationAddressPrefix = '0.0.0.0/0'

Access = 'Allow'

Priority = '100'

Direction = 'Outbound'

}

$rule2 = New-AzNetworkSecurityRuleConfig @nsgrule2

## Create network security group ##

$nsg = @{

Name = 'myNSG'

ResourceGroupName = 'TutorGwLB-rg'

Location = 'eastus'

SecurityRules = $rule1,$rule2

}

New-AzNetworkSecurityGroup @nsg

```

---

## Create and configure a gateway load balancer

# [Azure portal](#tab/azureportal)

In this section, you create the configuration and deploy the gateway load balancer.

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

1. In the **Load Balancer** page, select **Create**.

1. In the **Basics** tab of the **Create load balancer** page, enter, or select the following information:

| **Setting** | **Value** |

| ---                     | ---  |

| **Project details** |   |

| Subscription               | Select your subscription. |

| Resource group         | Select **load-balancer-rg**. |

| **Instance details** |   |

| Name                   | Enter **gateway-load-balancer** |

| Region         | Select **(US) East US**. |

| SKU           | Select **Gateway**. |

| Type          | Select **Internal**. |

1. Select **Next: Frontend IP configuration** at the bottom of the page.

1. In **Frontend IP configuration**, select **+ Add a frontend IP**.

1. In **Add frontend IP configuration**, enter or select the following information:

| **Setting** | **Value** |

| ------- | ----- |

| Name | Enter **lb-frontend-IP**. |

| Virtual network | Select **lb-vnet**. |

| Subnet | Select **backend-subnet**. |

| Assignment | Select **Dynamic** |

1. Select **Save**.

1.  Select **Next: Backend pools** at the bottom of the page.

1.  In the **Backend pools** tab, select **+ Add a backend pool**.

5.  In **Add backend pool**, enter or select the following information.

| **Setting** | **Value** |

| ------- | ----- |

| Name | Enter **lb-backend-pool**. |

| Backend Pool Configuration | Select **NIC**. |

| **Gateway load balancer configuration** |   |

| Type | Select **Internal and External**. |

| Internal port | Leave the default of **10800**. |

| Internal identifier | Leave the default of **800**. |

| External port | Leave the default of **10801**. |

| External identifier | Leave the default of **801**. |

6.  Select **Save**.

7.  Select the **Next: Inbound rules** button at the bottom of the page.

8.  In **Load balancing rule** in the **Inbound rules** tab, select **+ Add a load balancing rule**.

9.  In **Add load balancing rule**, enter or select the following information:

| **Setting** | **Value** |

| ------- | ----- |

| Name | Enter **lb-rule** |

| IP Version | Select **IPv4** or **IPv6** depending on your requirements. |

| Frontend IP address | Select **lb-frontend-IP**. |

| Backend pool | Select **lb-backend-pool**. |

| Health probe | Select **Create new**.</br> In **Name**, enter **lb-health-probe**.</br> Select **TCP** in **Protocol**.</br> Leave the rest of the defaults, and select **Save**. |

| Session persistence | Select **None**. |

| Enable TCP reset | Leave default of unchecked. |

| Enable floating IP | Leave default of unchecked. |

10. Select **Save**.

11. Select the blue **Review + create** button at the bottom of the page.

12. Select **Create**.

# [Azure CLI](#tab/azurecli/)

In this section, you create a gateway load balancer and configure it with a backend pool and frontend IP configuration. The backend pool is associated with the existing load balancer created in the prerequisites.

## Create Gateway Load Balancer

To create the load balancer, use [az network lb create](/cli/azure/network/lb#az-network-lb-create).

```azurecli-interactive

az network lb create \

--resource-group TutorGwLB-rg \

--name myLoadBalancer-gw \

--sku Gateway \

--vnet-name myVNet \

--subnet myBackendSubnet \

--backend-pool-name myBackendPool \

--frontend-ip-name myFrontEnd

```

## Create tunnel interface

An internal interface is automatically created with Azure CLI with the **`--identifier`** of **900** and **`--port`** of **10800**.

You use [az network lb address-pool tunnel-interface add](/cli/azure/network/lb/address-pool/tunnel-interface#az-network-lb-address-pool-tunnel-interface-add) to create external tunnel interface for the load balancer.

```azurecli-interactive

az network lb address-pool tunnel-interface add \

--address-pool myBackEndPool \

--identifier '901' \

--lb-name myLoadBalancer-gw \

--protocol VXLAN \

--resource-group TutorGwLB-rg \

--type External \

--port '10801'

```

## Create health probe

A health probe is required to monitor the health of the backend instances in the load balancer. Use [az network lb probe create](/cli/azure/network/lb/probe#az-network-lb-probe-create) to create the health probe.

```azurecli-interactive

az network lb probe create \

--resource-group TutorGwLB-rg \

--lb-name myLoadBalancer-gw \

--name myHealthProbe \

--protocol http \

--port 80 \

--path '/' \

--interval '5' \

--threshold '2'

```

## Create load-balancing rule

Traffic destined for the backend instances is routed with a load-balancing rule. Use [az network lb rule create](/cli/azure/network/lb/probe#az-network-lb-rule-create)  to create the load-balancing rule.

```azurecli-interactive

az network lb rule create \

--resource-group TutorGwLB-rg \

--lb-name myLoadBalancer-gw \

--name myLBRule \

--protocol All \

--frontend-port 0 \

--backend-port 0 \

--frontend-ip-name myFrontEnd \

--backend-pool-name myBackEndPool \

--probe-name myHealthProbe

```

# [Azure PowerShell](#tab/azurepowershell/)

In this section, you create the configuration and deploy the gateway load balancer. Use [New-AzLoadBalancerFrontendIpConfig](/powershell/module/az.network/new-azloadbalancerfrontendipconfig) to create the frontend IP configuration of the load balancer.

You use [New-AzLoadBalancerTunnelInterface](/powershell/module/az.network/new-azloadbalancerfrontendipconfig) to create two tunnel interfaces for the load balancer.

Create a backend pool with [New-AzLoadBalancerBackendAddressPoolConfig](/powershell/module/az.network/new-azloadbalancerbackendaddresspoolconfig) for the NVAs.

A health probe is required to monitor the health of the backend instances in the load balancer. Use [New-AzLoadBalancerProbeConfig](/powershell/module/az.network/new-azloadbalancerprobeconfig) to create the health probe.

Traffic destined for the backend instances is routed with a load-balancing rule. Use [New-AzLoadBalancerRuleConfig](/powershell/module/az.network/new-azloadbalancerruleconfig)  to create the load-balancing rule.

To create the deploy the load balancer, use [New-AzLoadBalancer](/powershell/module/az.network/new-azloadbalancer).

```azurepowershell-interactive

## Place virtual network configuration in a variable for later use. ##

$net = @{

Name = 'myVNet'

ResourceGroupName = 'TutorGwLB-rg'

}

$vnet = Get-AzVirtualNetwork @net

## Create load balancer frontend configuration and place in variable. ##

$fe = @{

Name = 'myFrontend'

SubnetId = $vnet.subnets[0].id

}

$feip = New-AzLoadBalancerFrontendIpConfig @fe

## Create backend address pool configuration and place in variable. ##

$int1 = @{

Type = 'Internal'

Protocol = 'Vxlan'

Identifier = '800'

Port = '10800'

}

$tunnelInterface1 = New-AzLoadBalancerBackendAddressPoolTunnelInterfaceConfig @int1

$int2 = @{

Type = 'External'

Protocol = 'Vxlan'

Identifier = '801'

Port = '10801'

}

$tunnelInterface2 = New-AzLoadBalancerBackendAddressPoolTunnelInterfaceConfig @int2

$pool = @{

Name = 'myBackendPool'

TunnelInterface = $tunnelInterface1,$tunnelInterface2

}

$bepool = New-AzLoadBalancerBackendAddressPoolConfig @pool

## Create the health probe and place in variable. ##

$probe = @{

Name = 'myHealthProbe'

Protocol = 'http'

Port = '80'

IntervalInSeconds = '360'

ProbeCount = '5'

RequestPath = '/'

}

$healthprobe = New-AzLoadBalancerProbeConfig @probe

## Create the load balancer rule and place in variable. ##

$para = @{

Name = 'myLBRule'

Protocol = 'All'

FrontendPort = '0'

BackendPort = '0'

FrontendIpConfiguration = $feip

BackendAddressPool = $bepool

Probe = $healthprobe

}

$rule = New-AzLoadBalancerRuleConfig @para

## Create the load balancer resource. ##

$lb = @{

ResourceGroupName = 'TutorGwLB-rg'

Name = 'myLoadBalancer-gw'

Location = 'eastus'

Sku = 'Gateway'

LoadBalancingRule = $rule

FrontendIpConfiguration = $feip

BackendAddressPool = $bepool

Probe = $healthprobe

}

New-AzLoadBalancer @lb

```

---

## Add network virtual appliances to the Gateway Load Balancer backend pool

> [!NOTE]

> If leveraging your own custom network virtual appliance in the backend pool of a Gateway Load Balancer, please ensure the MTU of all NVA virtual machines are raised to a minimum of 1550 bytes to accommodate for the VXLAN encapsulated headers. This will allow source packets up to the limit of 1500 byte packets in Azure, avoiding fragmentation.

# [Azure portal](#tab/azureportal)

Deploy NVAs through the Azure Marketplace. Once deployed, add the NVA virtual machines to the backend pool of the gateway load balancer. To add the virtual machines, go to the backend pools tab of your gateway load balancer.

# [Azure CLI](#tab/azurecli/)

Deploy NVAs through the Azure Marketplace. Once deployed, add the virtual machines to the backend pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#az-network-nic-ip-config-address-pool-add).

# [Azure PowerShell](#tab/azurepowershell/)

Deploy NVAs through the Azure Marketplace. Once deployed, add the virtual machines to the backend pool with [Set-AzNetworkInterfaceIpConfig -LoadBalancerBackendAddressPool](/powershell/module/az.network/set-aznetworkinterfaceipconfig).

---

## Chain load balancer frontend to Gateway Load Balancer

# [Azure portal](#tab/azureportal)

In this example, you'll chain the frontend of a standard load balancer to the gateway load balancer.

You add the frontend to the frontend IP of an existing load balancer in your subscription.

1. In the search box in the Azure portal, enter **Load balancer**. In the search results, select **Load balancers**.

2. In **Load balancers**, select **load-balancer** or your existing load balancer name.

3. In the load balancer page, select **Frontend IP configuration** in **Settings**.

4. Select the frontend IP of the load balancer. In this example, the name of the frontend is **lb-frontend-IP**.

5. Select **lb-frontend-IP (10.1.0.4)** in the pull-down box next to **Gateway load balancer**.

6. Select **Save**.

# [Azure CLI](#tab/azurecli/)

In this example, you'll chain the frontend of a standard load balancer to the gateway load balancer.

You add the frontend to the frontend IP of an existing load balancer in your subscription.

Use [az network lb frontend-ip show](/cli/azure/network/lb/frontend-ip#az-az-network-lb-frontend-ip-show) to place the resource ID of your gateway load balancer frontend into a variable.

Use [az network lb frontend-ip update](/cli/azure/network/lb/frontend-ip#az-network-lb-frontend-ip-update) to chain the gateway load balancer frontend to your existing load balancer.

```azurecli-interactive

feid=$(az network lb frontend-ip show \

--resource-group TutorGwLB-rg \

--lb-name myLoadBalancer-gw \

--name myFrontend \

--query id \

--output tsv)

az network lb frontend-ip update \

--resource-group CreatePubLBQS-rg \

--name myFrontendIP \

--lb-name myLoadBalancer \

--public-ip-address myPublicIP \

--gateway-lb $feid

```

# [Azure PowerShell](#tab/azurepowershell/)

In this example, you'll chain the frontend of a standard load balancer to the gateway load balancer.

You add the frontend to the frontend IP of an existing load balancer in your subscription.

Use [Set-AzLoadBalancerFrontendIpConfig](/powershell/module/az.network/set-azloadbalancerfrontendipconfig) to chain the gateway load balancer frontend to your existing load balancer.

```azurepowershell-interactive

## Place the gateway load balancer configuration into a variable. ##

$par1 = @{

ResourceGroupName = 'TutorGwLB-rg'

Name = 'myLoadBalancer-gw'

}

$gwlb = Get-AzLoadBalancer @par1

## Place the existing load balancer into a variable. ##

$par2 = @{

ResourceGroupName = 'CreatePubLBQS-rg'

Name = 'myLoadBalancer'

}

$lb = Get-AzLoadBalancer @par2

## Place the existing public IP for the existing load balancer into a variable.

$par3 = @{

ResourceGroupName = 'CreatePubLBQS-rg'

Name = 'myPublicIP'

}

$publicIP = Get-AzPublicIPAddress @par3

## Chain the gateway load balancer to your existing load balancer frontend. ##

$par4 = @{

Name = 'myFrontEndIP'

PublicIPAddress = $publicIP

LoadBalancer = $lb

GatewayLoadBalancerId = $gwlb.FrontendIpConfigurations.Id

}

$config = Set-AzLoadBalancerFrontendIpConfig @par4

$config | Set-AzLoadBalancer

```

---

## Chain virtual machine to Gateway Load Balancer

# [Azure portal](#tab/azureportal)

Alternatively, you can chain a VM's NIC IP configuration to the gateway load balancer.

You add the gateway load balancer's frontend to an existing VM's NIC IP configuration.

> [!IMPORTANT]

> A virtual machine must have a public IP address assigned before attempting to chain the NIC configuration to the frontend of the gateway load balancer.

1. In the search box in the Azure portal, enter **Virtual machine**. In the search results, select **Virtual machines**.

2. In **Virtual machines**, select the virtual machine that you want to add to the gateway load balancer. In this example, the virtual machine is named **myVM1**.

3. In the overview of the virtual machine, select **Networking** in **Settings**.

4. In **Networking**, select the name of the network interface attached to the virtual machine. In this example, it's **myvm1229**.

5. In the network interface page, select **IP configurations** in **Settings**.

6. Select **lb-frontend-IP** in **Gateway Load balancer**.

7. Select **Save**.

# [Azure CLI](#tab/azurecli/)

Alternatively, you can chain a VM's NIC IP configuration to the gateway load balancer.

You add the gateway load balancer's frontend to an existing VM's NIC IP configuration.

Use [az network lb frontend-ip show](/cli/azure/network/lb/frontend-ip#az-az-network-lb-frontend-ip-show) to place the resource ID of your gateway load balancer frontend into a variable.

Use [az network lb frontend-ip update](/cli/azure/network/nic/ip-config#az-network-nic-ip-config-update) to chain the gateway load balancer frontend to your existing VM's NIC IP configuration.

```azurecli-interactive

feid=$(az network lb frontend-ip show \

--resource-group TutorGwLB-rg \

--lb-name myLoadBalancer-gw \

--name myFrontend \

--query id \

--output tsv)

az network nic ip-config update \

--resource-group MyResourceGroup

--nic-name MyNIC

--name MyIPconfig

--gateway-lb $feid

```

# [Azure PowerShell](#tab/azurepowershell/)

Alternatively, you can chain a VM's NIC IP configuration to the gateway load balancer.

You add the gateway load balancer's frontend to an existing VM's NIC IP configuration.

Use [Set-AzNetworkInterfaceIpConfig](/powershell/module/az.network/set-aznetworkinterfaceipconfig) to chain the gateway load balancer frontend to your existing VM's NIC IP configuration.

```azurepowershell-interactive

## Place the gateway load balancer configuration into a variable. ##

$par1 = @{

ResourceGroupName = 'TutorGwLB-rg'

Name = 'myLoadBalancer-gw'

}

$gwlb = Get-AzLoadBalancer @par1

## Place the existing NIC into a variable. ##

$par2 = @{

ResourceGroupName = 'MyResourceGroup'

Name = 'myNic'

}

$nic = Get-AzNetworkInterface @par2

## Chain the gateway load balancer to your existing VM NIC. ##

$par3 = @{

Name = 'myIPconfig'

NetworkInterface = $nic

GatewayLoadBalancerId = $gwlb.FrontendIpConfigurations.Id

}

$config = Set-AzNetworkInterfaceIpConfig @par3

$config | Set-AzNetworkInterface

```

---

## Clean up resources

# [Azure portal](#tab/azureportal)

When no longer needed, delete the resource group, load balancer, and all related resources. To do so, select the resource group **load-balancer-rg** that contains the resources and then select **Delete**.

# [Azure CLI](#tab/azurecli/)

When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, load balancer, and the remaining resources.

```azurecli-interactive

az group delete \

--name TutorGwLB-rg

```

# [Azure PowerShell](#tab/azurepowershell/)

When no longer needed, you can use the [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) command to remove the resource group, load balancer, and the remaining resources.

```azurepowershell-interactive

Remove-AzResourceGroup -Name 'TutorGwLB-rg'

```

---

## Next steps

Create Network Virtual Appliances in Azure.

When creating the NVAs, choose the resources created in this tutorial:

* Virtual network

* Subnet

* Network security group

* Gateway load balancer

Advance to the next article to learn how to create a cross-region Azure Load Balancer.

> [!div class="nextstepaction"]

> [Global load balancer](tutorial-cross-region-portal.md)


# Gateway Deploy Dual Stack Load Balancer

# Deploy a dual-stack Azure Gateway Load Balancer

In this tutorial, you deploy IPv6 configurations to an existing IPv4-configured Azure Gateway Load Balancer.

You learn to:

> [!div class="checklist"]

> * Add IPv6 address ranges to an existing subnet.

> * Add an IPv6 frontend to Gateway Load Balancer.

> * Add an IPv6 backend pool to Gateway Load Balancer.

> * Add IPv6 configuration to network interfaces.

> * Add a load balancing rule for IPv6 traffic.

> * Chain the IPv6 load balancer frontend to Gateway Load Balancer.

Along with the Gateway Load Balancer, this scenario includes the following already-deployed resources:

- A dual stack virtual network and subnet.

- A standard Load Balancer with dual (IPv4 + IPv6) frontend configurations.

- A Gateway Load Balancer with IPv4 only.

- A network interface with a dual-stack IP configuration, a network security group attached, and public IPv4 & IPv6 addresses.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An existing dual-stack load balancer. For more information on creating a dual-stack load balancer, see [Deploy IPv6 dual stack application - Standard Load Balancer](virtual-network-ipv4-ipv6-dual-stack-standard-load-balancer-powershell.md).

- An existing IPv4 gateway balancer. For more information on creating a gateway load balancer, see [Create a gateway load balancer](./Tutorial-create-gateway-load-balancer.md).

## Add IPv6 address ranges to an existing subnet

This article assumes you already have a Gateway Load Balancer configured for IPv4 traffic, with a corresponding virtual network and subnet. In this step, you add IPv6 ranges to your Gateway Load Balancer's virtual network and subnet. This range is need when creating an IPv6 frontend configuration for your Gateway Load Balancer using a private IP address from this subnet/virtual network.

# [PowerShell](#tab/powershell)

```powershell-interactive

#Add IPv6 ranges to the virtual network and subnet

#Retrieve the virtual network object

$rg = Get-AzResourceGroup  -ResourceGroupName "myResourceGroup"

$vnet = Get-AzVirtualNetwork  -ResourceGroupName $rg.ResourceGroupName -Name "myVNet"

#Add IPv6 prefix to the virtual network

$vnet.addressspace.addressprefixes.add("fd00:db8:deca::/48")

#Update the running virtual network

$vnet |  Set-AzVirtualNetwork

#Retrieve the subnet object from the local copy of the virtual network

$subnet= $vnet.subnets[0]

#Add IPv6 prefix to the subnet

$subnet.addressprefix.add("fd00:db8:deca::/64")

#Update the running virtual network with the new subnet configuration

$vnet |  Set-AzVirtualNetwork

```

# [CLI](#tab/cli)

```azurecli-interactive

az network vnet subnet update

--vnet-name myVNet

--name myGWSubnet

--resource-group myResourceGroup

--address-prefixes  "10.1.0.0/24"  "fd00:db8:deca:deed::/64"

```

---

## Add an IPv6 frontend to gateway load balancer

Now that you've added IPv6 prefix ranges to your Gateway Load Balancer's subnet and virtual network, we can create a new IPv6 frontend configuration on the Gateway Load Balancer, with an IPv6 address from your subnet's range.

# [PowerShell](#tab/powershell)

```powershell-interactive

# Retrieve the load balancer configuration

$gwlb = Get-AzLoadBalancer -ResourceGroupName "myResourceGroup"-Name "myGatewayLoadBalancer"

# Add IPv6 frontend configuration to the local copy of the load balancer configuration

$gwlb | Add-AzLoadBalancerFrontendIpConfig `

-Name "myGatewayFrontEndv6" `

-PrivateIpAddressVersion "IPv6" `

-Subnet $subnet

#Update the running load balancer with the new frontend

$gwlb | Set-AzLoadBalancer

```

# [CLI](#tab/cli)

```azurecli-interactive

az network lb frontend-ip create --lb-name myGatewayLoadBalancer

--name myGatewayFrontEndv6

--resource-group myResourceGroup

--private-ip-address-version IPv6

--vnet-name myVNet

--subnet myGWSubnet

```

---

## Add an IPv6 backend pool to gateway load balancer

In order to distribute IPv6 traffic, you need a backend pool containing instances with IPv6 addresses. First, you create a backend pool on the Gateway Load Balancer. In the following step, you create IPv6 configurations to your existing backend NICs for IPv4 traffic, and attach them to this backend pool.

# [PowerShell](#tab/powershell)

```azurepowershell-interactive

## Create IPv6 tunnel interfaces

$int1 = @{

Type = 'Internal'

Protocol = 'Vxlan'

Identifier = '866'

Port = '2666'

}

$tunnelInterface1 = New-AzLoadBalancerBackendAddressPoolTunnelInterfaceConfig @int1

$int2 = @{

Type = 'External'

Protocol = 'Vxlan'

Identifier = '867'

Port = '2667'

}

$tunnelInterface2 = New-AzLoadBalancerBackendAddressPoolTunnelInterfaceConfig @int2

# Create the IPv6 backend pool

$pool = @{

Name = 'myGatewayBackendPoolv6'

TunnelInterface = $tunnelInterface1,$tunnelInterface2

}

# Add the backend pool to the load balancer

$gwlb | Add-AzLoadBalancerBackendAddressPoolConfig @pool

# Update the load balancer

$gwlb | Set-AzLoadBalancer

```

# [CLI](#tab/cli)

```azurecli-interactive

az network lb address-pool create --address-pool-name myGatewayBackendPool \

--lb-name myGatewayLoadBalancer \

--resource-group myResourceGroup \

--tunnel-interfaces "{[{"port": 2666,"identifier": 866,"protocol": "VXLAN","type": "Internal"},{"port": 2667,"identifier": 867,"protocol": "VXLAN","type": "External"}]}"

```

---

## Add IPv6 configuration to network interfaces

# [PowerShell](#tab/powershell)

```azurepowershell-interactive

#Retrieve the NIC object

$NIC_1 = Get-AzNetworkInterface -Name "myNic1" -ResourceGroupName $rg.ResourceGroupName

$backendPoolv6 = Get-AzLoadBalancerBackendAddressPoolConfig -Name "myGatewayBackendPoolv6" -LoadBalancer $gwlb

#Add an IPv6 IPconfig to NIC_1 and update the NIC on the running VM

$NIC_1 | Add-AzNetworkInterfaceIpConfig -Name myIPv6Config -Subnet $vnet.Subnets[0]  -PrivateIpAddressVersion IPv6 -LoadBalancerBackendAddressPool $backendPoolv6

$NIC_1 | Set-AzNetworkInterface

```

# [CLI](#tab/cli)

```azurecli-interactive

az network nic ip-config create \

--name myIPv6Config \

--nic-name myVM1 \

--resource-group MyResourceGroup \

--vnet-name myVnet \

--subnet mySubnet \

--private-ip-address-version IPv6 \

--lb-address-pools gwlb-v6pool \

--lb-name myGatewayLoadBalancer

```

---

## Add a load balancing rule for IPv6 traffic

Load balancing rules determine how traffic is routed to your backend instances. For Gateway Load Balancer, you create a load balancing rule with HA ports enabled, so that you can inspect traffic of all protocols, arriving on all ports.

# [PowerShell](#tab/powershell)

```azurepowershell-interactive

# Retrieve the updated (live) versions of the frontend and backend pool, and existing health probe

$frontendIPv6 = Get-AzLoadBalancerFrontendIpConfig -Name "myGatewayFrontEndv6" -LoadBalancer $gwlb

$backendPoolv6 = Get-AzLoadBalancerBackendAddressPoolConfig -Name "myGatewayBackendPoolv6" -LoadBalancer $gwlb

$healthProbe = Get-AzLoadBalancerProbeConfig -Name "myHealthProbe" -LoadBalancer $gwlb

# Create new LB rule with the frontend and backend

$gwlb | Add-AzLoadBalancerRuleConfig `

-Name "myRulev6" `

-FrontendIpConfiguration $frontendIPv6 `

-BackendAddressPool $backendPoolv6 `

-Protocol All `

-FrontendPort 0 `

-BackendPort 0 `

-Probe $healthProbe

#Finalize all the load balancer updates on the running load balancer

$gwlb | Set-AzLoadBalancer

```

# [CLI](#tab/cli)

```azurecli-interactive

az network lb rule create \

--resource-group myResourceGroup \

--lb-name myGatewayLoadBalancer \

--name myGatewayLoadBalancer-rule \

--protocol All \

--frontend-port 0 \

--backend-port 0 \

--frontend-ip-name gwlb-v6fe \

--backend-pool-name gwlb-v6pool \

--probe-name myGatewayLoadBalancer-hp

```

---

## Chain the IPv6 load balancer frontend to gateway load balancer

In this final step, you'll chain your existing Standard Load Balancer's IPv6 frontend to the Gateway Load Balancer's IPv6 frontend. Now, all IPv6 traffic headed to your Standard Load Balancer's frontend is forwarded to your Gateway Load Balancer for inspection by the configured NVAs before reaching your application.

# [PowerShell](#tab/powershell)

```azurepowershell-interactive

## Place the existing Standard load balancer into a variable. ##

$par1 = @{

ResourceGroupName = 'myResourceGroup'

Name = 'myLoadBalancer'

}

$lb = Get-AzLoadBalancer @par1

## Place the public frontend IP of the Standard load balancer into a variable.

$par3 = @{

ResourceGroupName = 'myResourceGroup'

Name = 'myIPv6PublicIP'

}

$publicIP = Get-AzPublicIPAddress @par3

## Chain the Gateway load balancer to your existing Standard load balancer frontend. ##

# $feip = Get-AzLoadBalancerFrontendIpConfig -Name "myGatewayFrontEndv6" -LoadBalancer $gwlb

$par4 = @{

Name = 'myIPv6FrontEnd'

PublicIPAddress = $publicIP

LoadBalancer = $lb

GatewayLoadBalancerId = $feip.id

}

$config = Set-AzLoadBalancerFrontendIpConfig @par4

$config | Set-AzLoadBalancer

```

# [CLI](#tab/cli)

```azurecli-interactive

feid=$(az network lb frontend-ip show \

--resource-group myResourceGroup \

--lb-name myLoadBalancer-gw \

--name myFrontend \

--query id \

--output tsv)

az network lb frontend-ip update \

--resource-group myResourceGroup \

--name myFrontendIP \

--lb-name myLoadBalancer \

--public-ip-address myIPv6PublicIP \

--gateway-lb $feid

```

---

## Limitations

- Gateway load balancer doesn't support NAT 64/46.

- When you implement chaining, the IP address version of Standard and Gateway Load Balancer front end configurations must match.

## Next steps

- Learn more about [Azure Gateway Load Balancer partners](./gateway-partners.md) for deploying network virtual appliances.


# Tutorial Gateway Outbound Connectivity

# Tutorial: Configure outbound connectivity with a gateway load balancer

Azure Load Balancer consists of Standard, Basic, and Gateway SKUs. Gateway Load Balancer (GWLB) is used for transparent insertion of Network Virtual Appliances (NVA). Use Gateway Load Balancer for scenarios that require high performance and high scalability of NVAs.

In this tutorial, you learn how to:

> [!div class="checklist"]

> - Chain a virtual machine’s IP or to a Gateway Load Balancer.

> - Create a new load balancer frontend IP configuration.

> - Create an outbound rule for virtual machine traffic.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An existing public standard SKU Azure Load Balancer. For more information on creating a load balancer, see [Create a public load balancer using the Azure portal](quickstart-load-balancer-standard-public-portal.md).

- For the purposes of this tutorial, the standard load balancer is named **myLoadBalancer** and is located in a resource group called **myResourceGroup**.

- An existing Gateway SKU Azure Load Balancer. For more information on creating a gateway load balancer, see [Create a gateway load balancer using the Azure portal](tutorial-create-gateway-load-balancer.md).

- For the purposes of this tutorial, the gateway load balancer in the examples is name **myGatewayLoadBalancer**.

- A virtual machine or network virtual appliance deployed in the same region and resource group as the load balancers. For more information on deploying a virtual machine, see [Create a Windows VM in the Azure portal](/azure/virtual-machines/windows/quick-create-portal).

- For the purposes of this tutorial, the virtual machine is named **myVM1**.

## Chain a virtual machine to a gateway load balancer

In this section, you chain an existing virtual machine’s public IP to a gateway load balancer. A gateway load balancer can be inserted in the path of outbound traffic by chaining to virtual machine instance level public IPs. This method secures both inbound and outbound traffic reaching or originating from this virtual machine’s public IP.

1. Navigate to your existing virtual machine. This example uses a virtual machine named **myVM1**.

1. To verify your virtual machine has a standard SKU public IP associated with it, select the listed public IP address in **Overview** of the virtual machine.

1. Under **Overview** of the public IP address, confirm that the SKU is **Standard**.

1. Return to your virtual machine.

1. In **Overview** of the virtual machine, select **Networking** > **Network settings**.

1. Select the network interface attached to the virtual machine.

1. In **Network interface**, select **IP configurations** under **Settings**.

1. Under **IP configurations**, select **myGWFrontend** from the **Gateway Load balancer** dropdown menu.

1. Select **Save**.

## Create a load balancer frontend

In this section, you create a new frontend IP configuration for outbound traffic in our existing standard public load balancer. Using separate public IPs for inbound and outbound traffic is a recommend best practice. Reusing the same public IP for inbound and outbound traffic can increase the risk of SNAT exhaustion, as load balancing and inbound NAT rules decrease the number of available SNAT ports.

1. Navigate to **myLoadBalancer** or your existing standard public load balancer and go to the **Frontend IP configuration** under **Settings**.

1. Select **+ Add** to create a new frontend IP configuration

1. In the **Add frontend IP configuration** page, enter or select the following information:

| Setting | Value |

| --- | --- |

| Name | Enter **myOutboundFrontend**. |

| IP version | Select **IPv4**. |

| IP type | Select **IP address**. |

| Public IP address | <br> Select **Create new**.</br> <br/> In **Add a public IP address**, enter **myOutboundPublicIP** for name, and select **Ok**.<br/>|

| Gateway Load balancer | Select **myGWFrontEnd**. |

1.	Select **Add**.

> [!NOTE]

> This step will *chain* your frontend to the gateway load balancer frontend specified.

> Any inbound or outbound traffic served by this frontend is redirected to the gateway load balancer for inspection by the configured NVAs before being distributed to this load balancer’s backend instances.

## Create outbound rule

1. In **Load balancer**, select **Outbound rules** under **Settings**.

1. Select **+ Add** in **Outbound rules** to add a rule.

1. In **Add outbound rule** window, Enter or select the following information in:

| Setting | Value |

| --- | --- |

| Name | Enter **myOutboundRule**. |

| IP version | Select **IPv4**. |

| Frontend IP address | Select the frontend IP address of the load balancer. This example uses **myOutboundFrontend**. |

| Protocol | Leave the default of **All**. |

| Idle timeout (minutes) | Enter **4** or your desired value. |

| TCP Reset | Leave the default of **Enabled**. |

| Backend pool | Select the backend pool of the load balancer. This example uses **myBackendPool**. |

| **Port allocation** | |

| Port allocation | Select **Manually choose number of outbound ports** |

| **Outbound ports** | |

| Choose by | Select **Maximum number of backend instances**. |

| Ports per instance | Enter the anticipated maximum number of backend instances. This example uses **2** backend instances.

1. Select **Add**.

> [!IMPORTANT]

>Gateway load balancer doesn't currently support chaining with NAT Gateway. Outbound traffic originating from Azure virtual machines, served through NAT Gateway, goes directly to the Internet. And that NAT Gateway takes precedence over any instance-level public IPs or load balancers for outbound traffic.

>

> NAT Gateway can be configured for outbound connectivity together with a Standard Public Load Balancer and Gateway Load Balancer architecture for inbound connectivity. In this scenario, all inbound traffic flows as expected through the gateway load balancer to the Standard load balancer, while outbound traffic goes to the Internet directly.

>

> If NVAs need to be inserted for outbound traffic, apply the methods described in this article. For example, chaining an instance-level public IP or outbound rules load balancer frontend to a gateway load balancer.

## Clean up resources

When no longer needed, delete the resource group, load balancer, and all related resources. To do so, select the resource group **myResourceGroup** that contains the resources and then select **Delete**.

## Next steps

In this tutorial, you learned how to:

- Chained a virtual machine’s IP address to a Gateway Load Balancer.

- Created a new load balancer frontend IP configuration.

- Created an outbound rule for virtual machine traffic.

> [!div class="nextstepaction"]

> Learn how to [deploy highly available NVAs](/azure/architecture/reference-architectures/dmz/nva-ha) with Azure Load Balancer.


# Tutorial Cross Region Portal

# Tutorial: Create an Azure Global Load Balancer

A global load balancer ensures a service is available globally across multiple Azure regions. If one region fails, the traffic is routed to the next closest healthy regional load balancer.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create global load balancer.

> * Create a backend pool containing two regional load balancers.

> * Create a load balancer rule.

> * Test the load balancer.

You can use the Azure portal, Azure CLI, or Azure PowerShell to complete this tutorial.

## Prerequisites

# [Azure portal](#tab/azureportal)

- An Azure subscription. If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

- Two **standard** sku Azure Load Balancers with backend pools deployed in two different Azure regions.

- For information on creating a regional standard load balancer and virtual machines for backend pools, see [Quickstart: Create a public load balancer to load balance VMs using the Azure portal](quickstart-load-balancer-standard-public-portal.md).

# [Azure CLI](#tab/azurecli/)

- An Azure subscription. If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

- Two **standard** sku Azure Load Balancers with backend pools deployed in two different Azure regions.

- For information on creating a regional standard load balancer and virtual machines for backend pools, see [Quickstart: Create a public load balancer to load balance VMs using Azure CLI](quickstart-load-balancer-standard-public-cli.md).

- Append the name of the load balancers and virtual machines in each region with a **-R1** and **-R2**.

- Azure CLI installed locally or Azure Cloud Shell.

If you choose to install and use the CLI locally, this quickstart requires Azure CLI version 2.0.28 or later. To find the version, run `az --version`. If you need to install or upgrade, see [Install the Azure CLI]( /cli/azure/install-azure-cli). When running Azure CLI locally, you'll need to sign in with `az login` to create a connection with Azure.

# [Azure PowerShell](#tab/azurepowershell/)

- An Azure subscription. If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

- Two **standard** sku Azure Load Balancers with backend pools deployed in two different Azure regions.

- For information on creating a regional standard load balancer and virtual machines for backend pools, see [Quickstart: Create a public load balancer to load balance VMs using Azure PowerShell](quickstart-load-balancer-standard-public-powershell.md).

- Azure PowerShell installed locally or Azure Cloud Shell.

If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 5.4.1 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell). If you're running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

---

## Create global load balancer

In this section, you create a global load balancer with a public IP address, a frontend IP configuration, a backend pool with region load balancers added, and a load balancer rule.

# [Azure portal](#tab/azureportal)

> [!IMPORTANT]

> To complete these steps, ensure that two regional load balancers with backend pools have been deployed in your subscription.  For more information, see, **[Quickstart: Create a public load balancer to load balance VMs using the Azure portal](quickstart-load-balancer-standard-public-portal.md)**.

### Create the load balancer resource and other resources

1. [Sign in](https://portal.azure.com) to the Azure portal.

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancer** in the search results.

3. In the **Load balancer** page, select **Create**.

4. In the **Basics** tab of the **Create load balancer** page, enter, or select the following information:

| Setting                 | Value                                              |

| ---                     | ---                                                |

| **Project details** |    |

| Subscription               | Select your subscription.    |

| Resource group         | Select **Create new** and enter **CreateCRLBTutorial-rg** in the text box. |

| **Instance details** |   |

| Name                   | Enter **myLoadBalancer-cr**                                   |

| Region         | Select **(US) East US**.                                        |

| Type          | Select **Public**.                                        |

| SKU           | Leave the default of **Standard**. |

| Tier           | Select **Global** |

5. Select **Next: Frontend IP configuration** at the bottom of the page.

6. In **Frontend IP configuration**, select **+ Add a frontend IP**.

7. Enter **LoadBalancerFrontend** in **Name** in **Add frontend IP address**.

8. Select **IPv4** or **IPv6** for **IP version**.

9.  In **Public IP address**, select **Create new**. Enter **myPublicIP-cr** in **Name**.  Select **Save** for the Add Public IP Address Dialog.

10. Select **Save**.

11. Select **Next: Backend pools** at the bottom of the page.

12. In **Backend pools**, select **+ Add a backend pool**.

13. Enter **myBackendPool-cr** in **Name** in **Add backend pool**.

14. In **Load balancers**, select **myLoadBalancer-r1** or your first regional load balancer in the **Load balancer** pull-down box. Verify the **Frontend IP configuration** and **IP address** correspond with **myLoadBalancer-r1**.

15. Select **myLoadBalancer-r2** or your second regional load balancer in the **Load balancer** pull-down box. Verify the **Frontend IP configuration** and **IP address** correspond with **myLoadBalancer-r2**.

16. Select **Add**.

18. Select **Next: Inbound rules** at the bottom of the page.

19. In **Inbound rules**, select **+ Add a load balancing rule**.

20. In **Add load balancing rule**, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| Name | Enter **myHTTPRule-cr**. |

| IP Version | Select **IPv4** or **IPv6** for **IP Version**. |

| Frontend IP address | Select **LoadBalancerFrontend**. |

| Protocol | Select **TCP**. |

| Port | Enter **80**. |

| Backend pool | Select **myBackendPool-cr**. |

| Session persistence | Select **None**. |

| Idle timeout (minutes) | Enter or move the slider to **15**. |

| TCP reset | Select **Enabled**. |

| Floating IP | Leave the default of **Disabled**. |

21. Select **Add**.

22. Select **Review + create** at the bottom of the page.

23. Select **Create** in the **Review + create** tab.

> [!NOTE]

> Cross region load-balancer deployment is listed to specific home Azure regions. For the current list, see [Home regions in Azure](cross-region-overview.md#home-regions-in-azure) for cross region load balancer.

# [Azure CLI](#tab/azurecli/)

### Create a resource group

An Azure resource group is a logical container into which Azure resources are deployed and managed.

Create a resource group with [az group create](/cli/azure/group#az-group-create):

* Named **myResourceGroupLB-CR**.

* In the **westus** location.

```azurecli-interactive

az group create \

--name myResourceGroupLB-CR \

--location westus

```

### Create the global load balancer resource

Create a global load balancer with [az network cross-region-lb create](/cli/azure/network/cross-region-lb#az-network-cross-region-lb-create):

* Named **myLoadBalancer-CR**.

* A frontend pool named **myFrontEnd-CR**.

* A backend pool named **myBackEndPool-CR**.

```azurecli-interactive

az network cross-region-lb create \

--name myLoadBalancer-CR \

--resource-group myResourceGroupLB-CR \

--frontend-ip-name myFrontEnd-CR \

--backend-pool-name myBackEndPool-CR

```

### Create the load balancer rule

A load balancer rule defines:

* Frontend IP configuration for the incoming traffic.

* The backend IP pool to receive the traffic.

* The required source and destination port.

Create a load balancer rule with [az network cross-region-lb rule create](/cli/azure/network/cross-region-lb/rule#az-network-cross-region-lb-rule-create):

* Named **myHTTPRule-CR**

* Listening on **Port 80** in the frontend pool **myFrontEnd-CR**.

* Sending load-balanced network traffic to the backend address pool **myBackEndPool-CR** using **Port 80**.

* Protocol **TCP**.

```azurecli-interactive

az network cross-region-lb rule create \

--backend-port 80 \

--frontend-port 80 \

--lb-name myLoadBalancer-CR \

--name myHTTPRule-CR \

--protocol tcp \

--resource-group myResourceGroupLB-CR \

--backend-pool-name myBackEndPool-CR \

--frontend-ip-name myFrontEnd-CR

```

## Create backend pool

In this section, you add two regional standard load balancers to the backend pool of the global load balancer.

> [!IMPORTANT]

> To complete these steps, ensure that two regional load balancers with backend pools have been deployed in your subscription.  For more information, see, **[Quickstart: Create a public load balancer to load balance VMs using Azure CLI](quickstart-load-balancer-standard-public-cli.md)**.

### Add the regional frontends to load balancer

In this section, you place the resource IDs of two regional load balancers frontends into variables, and then use the variables to add the frontends to the backend address pool of the global load balancer.

Retrieve the resource IDs with [az network lb frontend-ip show](/cli/azure/network/lb/frontend-ip#az-network-lb-frontend-ip-show).

Use [az network cross-region-lb address-pool address add](/cli/azure/network/cross-region-lb/address-pool/address#az-network-cross-region-lb-address-pool-address-add) to add the frontends you placed in variables in the backend pool of the global load balancer:

```azurecli-interactive

region1id=$(az network lb frontend-ip show \

--lb-name myLoadBalancer-R1 \

--name myFrontEnd-R1 \

--resource-group CreatePubLBQS-rg-r1 \

--query id \

--output tsv)

az network cross-region-lb address-pool address add \

--frontend-ip-address $region1id \

--lb-name myLoadBalancer-CR \

--name myFrontEnd-R1 \

--pool-name myBackEndPool-CR \

--resource-group myResourceGroupLB-CR

region2id=$(az network lb frontend-ip show \

--lb-name myLoadBalancer-R2 \

--name myFrontEnd-R2 \

--resource-group CreatePubLBQS-rg-r2 \

--query id \

--output tsv)

az network cross-region-lb address-pool address add \

--frontend-ip-address $region2id \

--lb-name myLoadBalancer-CR \

--name myFrontEnd-R2 \

--pool-name myBackEndPool-CR \

--resource-group myResourceGroupLB-CR

```

# [Azure PowerShell](#tab/azurepowershell/)

### Create a resource group

An Azure resource group is a logical container into which Azure resources are deployed and managed.

Create a resource group with [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup).

```azurepowershell-interactive

$rg = @{

Name = 'MyResourceGroupLB-CR'

Location = 'westus'

}

New-AzResourceGroup @rg

```

### Create global load balancer resources

In this section, you create the resources needed for the global load balancer.

A global standard sku public IP is used for the frontend of the global load balancer.

* Use [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) to create the public IP address.

* Create a frontend IP configuration with [New-AzLoadBalancerFrontendIpConfig](/powershell/module/az.network/new-azloadbalancerfrontendipconfig).

* Create a backend address pool with [New-AzLoadBalancerBackendAddressPoolConfig](/powershell/module/az.network/new-azloadbalancerbackendaddresspoolconfig).

* Create a load balancer rule with [Add-AzLoadBalancerRuleConfig](/powershell/module/az.network/add-azloadbalancerruleconfig).

* Create a global load Balancer with [New-AzLoadBalancer](/powershell/module/az.network/new-azloadbalancer).

```azurepowershell-interactive

`## Create global IP address for load balancer ##

$ip = @{

Name = 'myPublicIP-CR'

ResourceGroupName = 'MyResourceGroupLB-CR'

Location = 'westus'

Sku = 'Standard'

Tier = 'Global'

AllocationMethod = 'Static'

}

$publicIP = New-AzPublicIpAddress @ip

## Create frontend configuration ##

$fe = @{

Name = 'myFrontEnd-CR'

PublicIpAddress = $publicIP

}

$feip = New-AzLoadBalancerFrontendIpConfig @fe

## Create backend address pool ##

$be = @{

Name = 'myBackEndPool-CR'

}

$bepool = New-AzLoadBalancerBackendAddressPoolConfig @be

## Create the load balancer rule ##

$rul = @{

Name = 'myHTTPRule-CR'

Protocol = 'tcp'

FrontendPort = '80'

BackendPort = '80'

FrontendIpConfiguration = $feip

BackendAddressPool = $bepool

}

$rule = New-AzLoadBalancerRuleConfig @rul

## Create global load balancer resource ##

$lbp = @{

ResourceGroupName = 'myResourceGroupLB-CR'

Name = 'myLoadBalancer-CR'

Location = 'westus'

Sku = 'Standard'

Tier = 'Global'

FrontendIpConfiguration = $feip

BackendAddressPool = $bepool

LoadBalancingRule = $rule

}

$lb = New-AzLoadBalancer @lbp`

```

## Configure backend pool

In this section, you add two regional standard load balancers to the backend pool of the global load balancer.

> [!IMPORTANT]

> To complete these steps, ensure that two regional load balancers with backend pools have been deployed in your subscription.  For more information, see, **[Quickstart: Create a public load balancer to load balance VMs using Azure PowerShell](quickstart-load-balancer-standard-public-powershell.md)**.

* Use [Get-AzLoadBalancer](/powershell/module/az.network/get-azloadbalancer) and [Get-AzLoadBalancerFrontendIpConfig](/powershell/module/az.network/get-azloadbalancerfrontendipconfig) to store the regional load balancer information in variables.

* Use [New-AzLoadBalancerBackendAddressConfig](/powershell/module/az.network/new-azloadbalancerbackendaddressconfig) to create the backend address pool configuration for the load balancer.

* Use [Set-AzLoadBalancerBackendAddressPool](/powershell/module/az.network/new-azloadbalancerbackendaddresspool) to add the regional load balancer frontend to the global backend pool.

```azurepowershell-interactive

## Place the region one load balancer configuration in a variable ##

$region1 = @{

Name = 'myLoadBalancer-R1'

ResourceGroupName = 'CreatePubLBQS-rg-r1'

}

$R1 = Get-AzLoadBalancer @region1

## Place the region two load balancer configuration in a variable ##

$region2 = @{

Name = 'myLoadBalancer-R2'

ResourceGroupName = 'CreatePubLBQS-rg-r2'

}

$R2 = Get-AzLoadBalancer @region2

## Place the region one load balancer frontend configuration in a variable ##

$region1fe = @{

Name = 'MyFrontEnd-R1'

LoadBalancer = $R1

}

$R1FE = Get-AzLoadBalancerFrontendIpConfig @region1fe

## Place the region two load balancer frontend configuration in a variable ##

$region2fe = @{

Name = 'MyFrontEnd-R2'

LoadBalancer = $R2

}

$R2FE = Get-AzLoadBalancerFrontendIpConfig @region2fe

## Create the global backend address pool configuration for region 1 ##

$region1ap = @{

Name = 'MyBackendPoolConfig-R1'

LoadBalancerFrontendIPConfigurationId = $R1FE.Id

}

$beaddressconfigR1 = New-AzLoadBalancerBackendAddressConfig @region1ap

## Create the global backend address pool configuration for region 2 ##

$region2ap = @{

Name = 'MyBackendPoolConfig-R2'

LoadBalancerFrontendIPConfigurationId = $R2FE.Id

}

$beaddressconfigR2 = New-AzLoadBalancerBackendAddressConfig @region2ap

## Apply the backend address pool configuration for the global load balancer ##

$bepoolcr = @{

ResourceGroupName = 'myResourceGroupLB-CR'

LoadBalancerName = 'myLoadBalancer-CR'

Name = 'myBackEndPool-CR'

LoadBalancerBackendAddress = $beaddressconfigR1,$beaddressconfigR2

}

Set-AzLoadBalancerBackendAddressPool @bepoolcr

```

---

## Test the load balancer

# [Azure portal](#tab/azureportal)

In this section, you test the global load balancer. You connect to the public IP address in a web browser.  You stop the virtual machines in one of the regional load balancer backend pools and observe the failover.

1. Find the public IP address for the load balancer on the **Overview** screen. Select **All services** in the left-hand menu, select **All resources**, and then select **myPublicIP-cr**.

2. Copy the public IP address, and then paste it into the address bar of your browser. The default page of IIS Web server is displayed on the browser.

3. Stop the virtual machines in the backend pool of one of the regional load balancers.

4. Refresh the web browser and observe the failover of the connection to the other regional load balancer.

# [Azure CLI](#tab/azurecli/)

In this section, you test the global load balancer. You connect to the public IP address in a web browser.  You stop the virtual machines in one of the regional load balancer backend pools and observe the failover.

1. To get the public IP address of the load balancer, use [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show):

```azurecli-interactive

az network public-ip show \

--resource-group myResourceGroupLB-CR \

--name PublicIPmyLoadBalancer-CR \

--query ipAddress \

--output tsv

```

2. Copy the public IP address, and then paste it into the address bar of your browser. The default page of IIS Web server is displayed on the browser.

3. Stop the virtual machines in the backend pool of one of the regional load balancers.

4. Refresh the web browser and observe the failover of the connection to the other regional load balancer.

# [Azure PowerShell](#tab/azurepowershell/)

In this section, you test the global load balancer. You connect to the public IP address in a web browser.  You stop the virtual machines in one of the regional load balancer backend pools and observe the failover.

1. Use [Get-AzPublicIpAddress](/powershell/module/az.network/get-azpublicipaddress) to get the public IP address of the load balancer:

```azurepowershell-interactive

$ip = @{

Name = 'myPublicIP-CR'

ResourceGroupName = 'myResourceGroupLB-CR'

}

Get-AzPublicIPAddress @ip | select IpAddress

```

2. Copy the public IP address, and then paste it into the address bar of your browser. The default page of IIS Web server is displayed on the browser.

3. Stop the virtual machines in the backend pool of one of the regional load balancers.

4. Refresh the web browser and observe the failover of the connection to the other regional load balancer.

---

## Clean up resources

# [Azure portal](#tab/azureportal)

When no longer needed, delete the resource group, load balancer, and all related resources.

To do so, select the resource group **CreateCRLBTutorial-rg** that contains the resources and then select **Delete**.

# [Azure CLI](#tab/azurecli/)

When no longer needed, use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, load balancer, and all related resources.

```azurecli-interactive

az group delete \

--name myResourceGroupLB-CR

```

# [Azure PowerShell](#tab/azurepowershell/)

When no longer needed, you can use the [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) command to remove the resource group, load balancer, and the remaining resources.

```azurepowershell-interactive

Remove-AzResourceGroup -Name 'myResourceGroupLB-CR'

```

---

## Next steps

In this tutorial, you:

* Created a global load balancer.

* Added regional load balancers to the backend pool of the global load balancer.

* Created a load-balancing rule.

* Tested the load balancer.

For more information on global load balancer, see:

> [!div class="nextstepaction"]

> [Global load balancer](cross-region-overview.md)


# Tutorial Deploy Cross Region Load Balancer Template

# Tutorial: Deploy a global load balancer with Azure Resource Manager templates

A global load balancer ensures a service is available globally across multiple Azure regions. If one region fails, the traffic is routed to the next closest healthy regional load balancer.

Using an ARM template takes fewer steps comparing to other deployment methods.

[!INCLUDE [About Azure Resource Manager](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-introduction.md)]

If your environment meets the prerequisites and you're familiar with using ARM templates, select the **Deploy to Azure** button. The template opens in the Azure portal.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * All tutorials include a list summarizing the steps to completion

> * Each of these bullet points align to a key H2

> * Use these green checkboxes in a tutorial

## Prerequisites

-  An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) and access to the Azure portal.

## Review the template

In this section, you review the template and the parameters that are used to deploy the global load balancer.

The template used in this quickstart is from the Azure Quickstart Templates.

> [!NOTE]

> When you create a standard load balancer, you must also create a new standard public IP address that is configured as the frontend for the standard load balancer. Also, the Load balancers and public IP SKUs must match. In our case, we will create two standard public IP addresses, one for the regional level load balancer and another for the global load balancer.

Multiple Azure resources have been defined in the template:

- [**Microsoft.Network/loadBalancers**](/azure/templates/microsoft.network/loadBalancers):Regional and global load balancers.

- [**Microsoft.Network/publicIPAddresses**](/azure/templates/microsoft.network/publicipaddresses): for the load balancer, bastion host, and for each of the virtual machines.

- [**Microsoft.Network/bastionHosts**](/azure/templates/microsoft.network/bastionhosts)

- [**Microsoft.Network/networkSecurityGroups**](/azure/templates/microsoft.network/networksecuritygroups)

- [**Microsoft.Network/virtualNetworks**](/azure/templates/microsoft.network/virtualNetworks): Virtual network for load balancer and virtual machines.

- [**Microsoft.Compute/virtualMachines**](/azure/templates/microsoft.compute/virtualMachines) (2): Virtual machines.

- [**Microsoft.Network/networkInterfaces**](/azure/templates/microsoft.network/networkInterfaces) (2): Network interfaces for virtual machines.

- [**Microsoft.Compute/virtualMachine/extensions**](/azure/templates/microsoft.compute/virtualmachines/extensions) (2): use to configure the Internet Information Server (IIS), and the web pages.

> [!IMPORTANT]

> [!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

>

To find more templates that are related to Azure Load Balancer, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Network&pageNumber=1&sort=Popular).

## Deploy the template

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Enter and select **Deploy a custom template** in the search bar

1. In the **Custom deployment** page, enter **load-balancer-cross-region** in the **Quickstart template** textbox and select **quickstarts/microsoft.network/load-balancer-cross-region**.

1. Choose **Select template** and enter the following information:

| Name | Value |

| --- | --- |

| Subscription | Select your subscription |

| Resource group | Select your resource group or create a new resource group |

| Region | Select the deployment region for resources |

| Project Name | Enter a project name used to create unique resource names |

| LocationCR | Select the deployment region for the cross-region load balancer |

| Location-r1 | Select the deployment region for the regional load balancer and VMs |

| Location-r2 | Select the deployment region where the regional load balancer and VMs  |

| Admin Username | Enter a username for the virtual machines |

| Admin Password | Enter a password for the virtual machines |

1. Select **Review + create** to run template validation.

1. If no errors are present, Review the terms of the template and select **Create**.

## Verify the deployment

1. If necessary, sign in to the [Azure portal](https://portal.azure.com).

1. Select **Resource groups** from the left pane.

1. Select the resource group used in the deployment. The default resource group name is the **project name** with **-rg** appended. For example, **crlb-learn-arm-rg**.

1. Select the global load balancer. Its default name is the project name with **-cr** appended. For example, **crlb-learn-arm-cr**.

1. Copy only the IP address part of the public IP address, and then paste it into the address bar of your browser. The page resolves to a default IIS Windows Server web page.

## Clean up resources

When you no longer need them, delete the:

* Resource group

* Load balancer

* Related resources

1. Go to the Azure portal, select the resource group that contains the load balancer, and then select **Delete resource group**.

1. Select **apply force delete for selected Virtual machines and Virtual machine scale sets**, enter the name of the resource group, and then select **Delete > Delete **.

## Next steps

In this tutorial, you:

- Created a cross region load balancer\

- Created a regional load balancer

- Created three virtual machines and linked them to the regional load balancer

- Configured the global load balancer to work with the regional load balancer

- Tested the global load balancer.

Learn more about cross-region load balancer.

Advance to the next article to learn how to create...

> [!div class="nextstepaction"]

> [Tutorial: Create a load balancer with more than one availability set in the backend pool](tutorial-multi-availability-sets-portal.md)


# Cross Subscription How To Attach Backend

# Attach a cross-subscription backend to an Azure Load Balancer

In this article, you learn how to attach a cross-subscription backend to an Azure Load Balancer by creating a cross-subscription backend pool and attaching cross-subscription network interfaces to the backend pool of the load balancer.

A [cross-subscription load balancer](cross-subscription-overview.md) can reference a virtual network that resides in a different subscription other than the load balancers. This feature allows you to deploy a load balancer in one subscription and reference a virtual network in another subscription.

[!INCLUDE [load-balancer-cross-subscription-prerequisites](../../includes/load-balancer-cross-subscription-prerequisites.md)]

[!INCLUDE [load-balancer-cross-subscription-azure-sign-in](../../includes/load-balancer-cross-subscription-azure-sign-in.md)]

[!INCLUDE [load-balancer-cross-subscription-create-resource-group](../../includes/load-balancer-cross-subscription-create-resource-group.md)]

## Create a load balancer

In this section, you create a load balancer in **Azure Subscription B**. You create a load balancer with a frontend IP address.

# [Azure PowerShell](#tab/azurepowershell)

With Azure PowerShell, you'll:

- A load balancer with [`New-AzLoadBalancer`](/powershell/module/az.network/new-azloadbalancer)

- Create a public IP address with [`New-AzPublicIpAddress`](/powershell/module/az.network/new-azpublicipaddress)

- Add a frontend IP configuration with [`Add-AzLoadBalancerFrontendIpConfig`](/powershell/module/az.network/add-azloadbalancerfrontendipconfig)

- Create a backend address pool with [`New-AzLoadBalancerBackendAddressPool`](/powershell/module/az.network/new-azloadbalancerbackendaddresspool).

```azurepowershell

# Create a load balancer

$loadbalancer = @{

ResourceGroupName = 'resource group B'

Name = 'LB Name'

Location = 'eastus'

Sku = 'Standard'

}

$LB = New-AzLoadBalancer @loadbalancer

$LBinfo = @{

ResourceGroupName = 'resource group B'

Name = 'my-lb'

}

# Create a public IP address

$publicip = @{

Name = 'IP Address Name'

ResourceGroupName = 'resource group B'

Location = 'eastus'

Sku = 'Standard'

AllocationMethod = 'static'

Zone = 1,2,3

}

New-AzPublicIpAddress @publicip

# Place public IP created in previous steps into variable

$pip = @{

Name = 'IP Address Name'

ResourceGroupName = 'resource group B'

}

$publicIp = Get-AzPublicIpAddress @pip

## Create load balancer frontend configuration and place in variable

$fip = @{

Name = 'Frontend Name'

PublicIpAddress = $publicip

}

$LB = $LB | Add-AzLoadBalancerFrontendIpConfig @fip

$LB = $LB | Set-AzLoadBalancer

# Create backend address pool configuration and place in variable. ##

$be = @{

ResourceGroupName= "resource group B"

Name= "myBackEndPool"

LoadBalancerName= "LB Name"

VirtualNetwork=$vnet.id

SyncMode= "Automatic"

}

#Create the backend pool

$backend = New-AzLoadBalancerBackendAddressPool @be

$LB = Get-AzLoadBalancer @LBinfo

```

# [Azure CLI](#tab/azurecli)

With Azure CLI, you create a load balancer with [`az network lb create`](/cli/azure/network/lb#az_network_lb_create) and update the backend pool. This example configures the following resources:

- A frontend IP address that receives the incoming network traffic on the load balancer.

- A backend address pool where the frontend IP sends the load balanced network traffic.

```azurecli

# Create a load balancer

az network lb create --resource-group myResourceGroupLB --name myLoadBalancer --sku Standard --public-ip-address myPublicIP   --frontend-ip-name myFrontEnd --backend-pool-name BackendPool1 --tags 'IsRemoteFrontend=true'

```

In order to utilize the cross-subscription feature of Azure load balancer, backend pools need to have the syncMode property enabled and a virtual network reference. This section updates the backend pool created prior by attaching the cross-subscription virtual network and enabling the syncMode property.

```azurecli

## Configure the backend address pool and syncMode property

az network lb address-pool update --lb-name myLoadBalancer --resource-group myResourceGroupLB -n myResourceGroupLB --vnet ‘/subscriptions/<subscription A ID>/resourceGroups/{resource group name}/providers/Microsoft.Network/virtualNetwork/{VNet name}’ --sync-mode Automatic

```

---

[!INCLUDE [load-balancer-cross-subscription-health-probe-rules](../../includes/load-balancer-cross-subscription-health-probe-rules.md)]

[!INCLUDE [load-balancer-cross-subscription-add-nic](../../includes/load-balancer-cross-subscription-add-nic.md)]

[!INCLUDE [load-balancer-cross-subscription-clean-up](../../includes/load-balancer-cross-subscription-clean-up.md)]

## Next steps

> [!div class="nextstepaction"]

> [Create a cross-subscription internal load balancer](./cross-subscription-how-to-internal-load-balancer.md)


# Cross Subscription How To Attach Frontend

# Attach a cross-subscription frontend to an Azure Load Balancer

In this article, you learn how to create a load balancer in one Azure subscription and attach a frontend IP address from another subscription. You create a resource group for the load balancer and then create a load balancer with a frontend IP address. You also create a backend address pool, health probe, and load balancer rule.

A [cross-subscription load balancer](cross-subscription-overview.md) can reference a virtual network that resides in a different subscription other than the load balancers. This feature allows you to deploy a load balancer in one subscription and reference a virtual network in another subscription.

## Prerequisites

# [Azure PowerShell](#tab/azurepowershell)

- Two Azure subscriptions. One subscription for the virtual network and another subscription for the load balancer.

- An Azure account with active subscriptions. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)

- A public IP address deployed in one of the subscriptions. For this example, the public IP address is in **Azure Subscription A**.

- An existing [Virtual Network](../virtual-network/quick-create-powershell.md). deployed in one of the subscriptions. For this example, the virtual network is in **Azure Subscription B**.

If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 5.4.1 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see Install Azure PowerShell module. If you're running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

> [!IMPORTANT]

> All of the code samples will use example names and placeholders. Be sure to replace these with the values from your environment.

> The values needing replacement will be enclosed in angle brackets, like this: `<example value>`.

>

# [Azure CLI](#tab/azurecli/)

[!INCLUDE [azure-cli-prepare-your-environment.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment-no-header.md)]

- Two Azure subscriptions. One subscription for the virtual network (**Azure Subscription A**) and another subscription for the load balancer(**Azure Subscription B**).

- An Azure account with active subscriptions. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)

- A public IP address deployed in one of the subscriptions. For this example, the public IP address is in **Azure Subscription A**.

- An existing [Virtual Network](../virtual-network/quick-create-cli.md). deployed in one of the subscriptions. For this example, the virtual network is in **Azure Subscription B**.

If you choose to install and use the CLI locally, this quickstart requires Azure CLI version 2.60 or later. To find the version, run az --version. If you need to install or upgrade, see Install the Azure CLI.

> [!IMPORTANT]

> All of the code samples will use example names and placeholders. Be sure to replace these with the values from your environment.

> The values needing replacement will be enclosed in angle brackets, like this: `<example value>`.

---

## Sign in to Azure

# [Azure PowerShell](#tab/azurepowershell)

With Azure PowerShell, you sign into Azure with [`Connect-AzAccount`](/powershell/module/az.accounts/connect-azaccount), and change your subscription context with [`Set-AzContext`](/powershell/module/az.accounts/set-azcontext) to **Azure Subscription A**. Then get the public IP address information with [`Get-AzPublicIpAddress`](/powershell/module/az.network/get-azpublicipaddress). You need the Azure subscription ID, resource group name, and virtual network name from your environment.

```azurepowershell

# Sign in to Azure

Connect-AzAccount

# Set the subscription context to Azure Subscription A

Set-AzContext -Subscription '<Azure Subscription A>'

# Get the Public IP address information with Get-AzPublicIpAddress

$publicIp = Get-AzPublicIpAddress @pip

```

# [Azure CLI](#tab/azurecli/)

With Azure CLI, you'll sign into Azure with [az login](/cli/azure/reference-index#az-login), and change your subscription context with [`az account set`](/cli/azure/account#az_account_set) to **Azure Subscription A**.

```azurecli

# Sign in to Azure CLI and change subscription to Azure Subscription A

Az login

Az account set –subscription <Azure Subscription A>

```

---

## Create a resource group

In this section, you create a resource group in **Azure Subscription B**. This resource group is for all of your resources associate with your load balancer.

# [Azure PowerShell](#tab/azurepowershell)

With Azure PowerShell, you switch the subscription context with [`Set-AzContext`](/powershell/module/az.accounts/set-azcontext) and create a resource group with [`New-AzResourceGroup`](/powershell/module/az.resources/new-azresourcegroup).

```azurepowershell

# Set the subscription context to Azure Subscription B

Set-AzContext -Subscription '<Azure Subscription B>'

# Create a resource group

$rg = @{

Name = 'myResourceGroupLB'

Location = 'westus'

}

New-AzResourceGroup @rg

```

> [!NOTE]

> When create the resource group for your load balancer, use the same Azure region as the virtual network in **Azure Subscription A**.

# [Azure CLI](#tab/azurecli/)

With Azure CLI, you switch the subscription context with [`az account set`](/cli/azure/account#az_account_set) and create a resource group with [`az group create`](/cli/azure/group#az_group_create).

```azurecli

# Create a resource group in Azure Subscription B

az group create --name 'myResourceGroupLB' --location westus

```

> [!NOTE]

> When create the resource group for your load balancer, use the same Azure region as the virtual network in **Azure Subscription A**.

---

## Create a load balancer

In this section, you create a load balancer in **Azure Subscription B**. You create a load balancer with a frontend IP address.

# [Azure PowerShell](#tab/azurepowershell)

Create a load balancer with [`New-AzLoadBalancer`](/powershell/module/az.network/new-azloadbalancer), add a frontend IP configuration with [`Add-AzLoadBalancerFrontendIpConfig`](/powershell/module/az.network/add-azloadbalancerfrontendipconfig), and then create a backend address pool with [`New-AzLoadBalancerBackendAddressPool`](/powershell/module/az.network/new-azloadbalancerbackendaddresspool).

```azurepowershell

# Create a load balancer

$tags = @{

'IsRemoteFrontend'= 'true'

}

$loadbalancer = @{

ResourceGroupName = 'myResourceGroupLB'

Name = 'myLoadBalancer'

Location = 'westus'

Sku = 'Standard'

Tag = $tags

}

$LB = New-AzLoadBalancer @loadbalancer

$LBinfo = @{

ResourceGroupName = 'myResourceGroupLB'

Name = 'myLoadBalancer'

}

$fip = @{

Name = 'Frontend Name'

PublicIpAddress = $publicip

}

$LB = $LB | Add-AzLoadBalancerFrontendIpConfig @fip

$LB = $LB | Set-AzLoadBalancer

## Create backend address pool configuration and place in variable.

$net = @{

Name = 'vnet name'

ResourceGroupName = 'myResourceGroupLB'

}

$vnet = Get-AzVirtualNetwork @net

$be = @{

ResourceGroupName= "myResourceGroupLB"

Name= "myBackEndPool"

LoadBalancerName= "myLoadBalancer"

VirtualNetwork=$vnet.id

SyncMode= "Automatic"

}

#create the backend pool

$backend = New-AzLoadBalancerBackendAddressPool @be

$LB = Get-AzLoadBalancer @LBinfo

```

# [Azure CLI](#tab/azurecli/)

With Azure CLI, you create a load balancer with [`az network lb create`](/cli/azure/network/lb#az_network_lb_create) and update the backend pool. This example configures the following resources:

- A frontend IP address that receives the incoming network traffic on the load balancer.

- The public IP address is pulled from subscription A, and the load balancer is deployed in subscription B.

- The `IsRemoteFrontend:True` tag is added since the IP address is cross-subscription.

- A backend address pool where the frontend IP sends the load balanced network traffic.

```azurecli

# Create a load balancer

az network lb create --resource-group myResourceGroupLB --name myLoadBalancer --sku Standard --public-ip-address '/subscriptions/<subscription A ID>/resourceGroups/{resource group name} /providers/Microsoft.Network/publicIPAddresses/{public IP address name}’  --frontend-ip-name myFrontEnd --backend-pool-name MyBackendPool --tags 'IsRemoteFrontend=true'

```

In order to utilize the cross-subscription feature of Azure load balancer, backend pools need to have the syncMode property enabled and a virtual network reference. This section updates the backend pool created prior by attaching the cross-subscription virtual network and enabling the syncMode property.

```azurecli

## Configure the backend address pool and syncMode property

az network lb address-pool update --lb-name myLoadBalancer --resource-group myResourceGroupLB -n myResourceGroupLB --vnet ‘/subscriptions/<subscription A ID>/resourceGroups/{resource group name}/providers/Microsoft.Network/virtualNetwork/{VNet name}’ --sync-mode Automatic

```

---

[!INCLUDE [load-balancer-cross-subscription-health-probe-rules](../../includes/load-balancer-cross-subscription-health-probe-rules.md)]

[!INCLUDE [load-balancer-cross-subscription-clean-up](../../includes/load-balancer-cross-subscription-clean-up.md)]

## Next steps

> [!div class="nextstepaction"]

> [Create a cross-subscription internal load balancer](./cross-subscription-how-to-internal-load-balancer.md)


# Cross Subscription How To Global Backend

# Create a global load balancer with cross-subscription backends

In this article, you learn how to create a global load balancer with cross-subscription backends.

A [cross-subscription load balancer](cross-subscription-overview.md) can reference a virtual network that resides in a different subscription other than the load balancers. This feature allows you to deploy a load balancer in one subscription and reference a virtual network in another subscription.

## Prerequisites

# [Azure PowerShell](#tab/azurepowershell)

- Two Azure subscriptions.

- An Azure account with active subscriptions. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)

- A global public IP address deployed in **Azure Subscription A** located in a [Global load balancer home region](cross-subscription-how-to-global-backend.md).

- A regional load balancer deployed in **Azure Subscription A**.

- Azure PowerShell installed locally or Azure Cloud Shell.

If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 5.4.1 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see Install Azure PowerShell module. If you're running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

> [!IMPORTANT]

> All of the code samples will use example names and placeholders. Be sure to replace these with the values from your environment.

> The values needing replacement will be enclosed in angle brackets, like this: `<example value>`.

>

# [Azure CLI](#tab/azurecli/)

- Two Azure subscriptions. One subscription for the virtual network (**Azure Subscription A**) and another subscription for the load balancer(**Azure Subscription B**).

- An Azure account with active subscriptions. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)

- A global public IP address deployed in **Azure Subscription A** located in a [Global load balancer home region](cross-subscription-how-to-global-backend.md).

- A regional load balancer deployed in **Azure Subscription A**. For this example, the load balancer is called **load-balancer-regional** in a resource group called **resource-group-a**.

[!INCLUDE [azure-cli-prepare-your-environment.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment-no-header.md)]

If you choose to install and use the CLI locally, this quickstart requires Azure CLI version 2.60 or later. To find the version, run az --version. If you need to install or upgrade, see Install the Azure CLI.

> [!IMPORTANT]

> All of the code samples will use example names and placeholders. Be sure to replace these with the values from your environment.

> The values needing replacement will be enclosed in angle brackets, like this: `<example value>`.

---

## Sign in to Azure

# [Azure PowerShell](#tab/azurepowershell)

With Azure PowerShell, you sign into Azure with [`Connect-AzAccount`](/powershell/module/az.accounts/connect-azaccount), and change your subscription context with [`Set-AzContext`](/powershell/module/az.accounts/set-azcontext) to **Azure Subscription A**. Then get the regional load balancer information with [`Get-AzLoadBalancer`](/powershell/module/az.network/get-azloadbalancer) and [`Get-AzLoadBalancerFrontendIpConfig`](/powershell/module/az.network/get-azloadbalancerfrontendipconfig). You need the Azure subscription ID, resource group name, and virtual network name from your environment.

```azurepowershell

# Sign in to Azure

Connect-AzAccount

# Set the subscription context to Azure Subscription A

Set-AzContext -Subscription '<Subscription ID of Subscription A>'

# Get the Virtual Network information with Get-AzVirtualNetwork

$rlb= @{

Name = 'load-balancer-regional'

ResourceGroupName = 'resource-group-a'

}

$rlbinfo = Get-AzLoadBalancer @rlb

$rlbfe = Get-AzLoadBalancerFrontendIpConfig @rlbinfo

```

# [Azure CLI](#tab/azurecli/)

```azurecli

With Azure CLI, you'll sign into Azure with [az login](/cli/azure/reference-index#az-login), and change your subscription context with [`az account set`](/cli/azure/account#az_account_set) to **Azure Subscription A**.

```azurecli

# Sign in to Azure CLI and change subscription to Azure Subscription B

Az login

Az account set –subscription '<Subscription ID of Subscription B>'

```

---

## Create a resource group

In this section, you create a resource group in **Azure Subscription B**. This resource group is for all of your resources associate with your load balancer.

# [Azure PowerShell](#tab/azurepowershell)

With Azure PowerShell, you switch the subscription context with [`Set-AzContext`](/powershell/module/az.accounts/set-azcontext) and create a resource group with [`New-AzResourceGroup`](/powershell/module/az.resources/new-azresourcegroup).

```azurepowershell

# Set the subscription context to Azure Subscription B

Set-AzContext -Subscription '<Azure Subscription B>'

# Create a resource group

$rg = @{

Name = 'resource-group-b'

Location = 'eastus2'

}

New-AzResourceGroup @rg

```

> [!NOTE]

> When creating the resource group for your load balancer, use the same Azure region as the virtual network in **Azure Subscription A**.

# [Azure CLI](#tab/azurecli/)

With Azure CLI, you switch the subscription context with [`az account set`](/cli/azure/account#az_account_set) and create a resource group with [`az group create`](/cli/azure/group#az_group_create).

```azurecli

# Create a resource group in Azure Subscription B

az group create --name resource-group-b --location eastus2

```

> [!NOTE]

> When create the resource group for your load balancer, use the same Azure region as the virtual network in **Azure Subscription A**.

---

## Create a global load balancer

In this section, you create the resources needed for the global load balancer.

A global standard sku public IP is used for the frontend of the global load balancer.

# [Azure PowerShell](#tab/azurepowershell)

With Azure PowerShell, you:

- Use [`New-AzPublicIpAddress`](/powershell/module/az.network/new-azpublicipaddress) to create the public IP address.

- Create a frontend IP configuration with [`New-AzLoadBalancerFrontendIpConfig`](/powershell/module/az.network/new-azloadbalancerfrontendipconfig).

- Create a backend address pool with [`New-AzLoadBalancerBackendAddressPoolConfig`](/powershell/module/az.network/new-azloadbalancerbackendaddresspoolconfig).

- Create a load balancer rule with [`Add-AzLoadBalancerRuleConfig`](/powershell/module/az.network/add-azloadbalancerruleconfig).

- Create a global load Balancer with [`New-AzLoadBalancer`](/powershell/module/az.network/new-azloadbalancer).

```azurepowershell

# Create global IP address for load balancer

$ip = @{

Name = 'public-IP-global'

ResourceGroupName = 'resource-group-b'

Location = 'eastus2'

Sku = 'Standard'

Tier = 'Global'

AllocationMethod = 'Static'

}

$publicIP = New-AzPublicIpAddress @ip

# Create frontend configuration

$fe = @{

Name = 'front-end-config-global'

PublicIpAddress = $publicIP

}

$feip = New-AzLoadBalancerFrontendIpConfig @fe

# Create backend address pool

$be = @{

Name = 'backend-pool-global'

}

$bepool = New-AzLoadBalancerBackendAddressPoolConfig @be

# Create the load balancer rule

$rul = @{

Name = 'HTTP-rule-global'

Protocol = 'tcp'

FrontendPort = '80'

BackendPort = '80'

FrontendIpConfiguration = $feip

BackendAddressPool = $bepool

}

$rule = New-AzLoadBalancerRuleConfig @rul

# Create global load balancer resource

$lbp = @{

ResourceGroupName = 'resource-group-b'

Name = 'load-balancer-global'

Location = ‘eastus2’

Sku = 'Standard'

Tier = 'Global'

FrontendIpConfiguration = $feip

BackendAddressPool = $bepool

LoadBalancingRule = $rule

}

$lb = New-AzLoadBalancer @lbp

```

# [Azure CLI](#tab/azurecli/)

With Azure CLI, you:

- Create a global load balancer with [`az network cross-region-lb create`](/cli/azure/network/cross-region-lb#az-network-cross-region-lb-create).

- Create a load balancer rule with [`az network cross-region-lb rule create`](/cli/azure/network/cross-region-lb#az-network-cross-region-lb-rule-create).

```azurecli

# Create global load balancer

az network cross-region-lb create --name load-balancer-global --resource-group resource-group-b --frontend-ip-name front-end-config-global --backend-pool-name backend-pool-global

# create a load balancer rule

az network cross-region-lb rule create --backend-port 80 --frontend-port 80 --lb-name load-balancer-global --name HTTP-rule-global --protocol tcp --resource-group resource-group-b --backend-pool-name backend-pool-global --frontend-ip-name front-end-config-global

```

---

## Add load balancer frontends to global load balancer

In this section, you add a frontend IP configuration to the global load balancer.

# [Azure PowerShell](#tab/azurepowershell)

With Azure PowerShell, you:

- Use [`Set-AzLoadBalancerFrontendIpConfig`](/powershell/module/az.network/set-azloadbalancerfrontendipconfig) to add the regional load balancer frontend to the global backend pool.

- Use [`New-AzLoadBalancerBackendAddressConfig`](/powershell/module/az.network/new-azloadbalancerbackendaddressconfig) to create the backend address pool configuration for the load balancer.

```azurepowershell

## Create the global backend address pool configuration for region 2 ##

$rlbbaf = @{

Name = 'backend-pool-config-regional'

LoadBalancerFrontendIPConfigurationId = $rlbfe.Id

}

$beaddressconfigRLB = New-AzLoadBalancerBackendAddressConfig @region2ap

## Apply the backend address pool configuration for the global load balancer ##

$bepoolcr = @{

ResourceGroupName = 'resource-group-b'

LoadBalancerName = 'load-balancer-global'

Name = 'backend-pool-global'

LoadBalancerBackendAddress = $beaddressconfigRLB

}

Set-AzLoadBalancerBackendAddressPool @bepoolcr

```

# [Azure CLI](#tab/azurecli/)

With Azure CLI, you add the frontends you placed in variables in the backend pool of the global load balancer with use [`az network cross-region-lb address-pool`](/cli/azure/network/cross-region-lb#az-network-cross-region-lb-address-pool).

```azurecli

az network cross-region-lb address-pool address add \

--frontend-ip-address ‘/subscriptions/Subscription A/resourceGroups/rg-name/providers/Microsoft.Network/loadBalancers/rlb-name /frontendIPConfigurations/rlb-lb Frontend Name’

--lb-name load-balancer-global \

--name myFrontEnd-R2 \

--pool-name backend-pool-global \

--resource-group resource-group-b

```

## Next steps

> [!div class="nextstepaction"]

> [Create a cross-subscription internal load balancer](./cross-subscription-how-to-internal-load-balancer.md)


# Cross Subscription How To Internal Load Balancer

# Create a cross-subscription internal load balancer

In this how-to guide, you learn how to create a cross-subscription internal load balancer by connecting a virtual network in a subscription to a load balancer in a different subscription.

A [cross-subscription internal load balancer (ILB)](cross-subscription-overview.md) can reference a virtual network that resides in a different subscription other than the load balancers. This feature allows you to deploy a load balancer in one subscription and reference a virtual network in another subscription.

[!INCLUDE [load-balancer-cross-subscription-prerequisites](../../includes/load-balancer-cross-subscription-prerequisites.md)]

[!INCLUDE [load-balancer-cross-subscription-azure-sign-in](../../includes/load-balancer-cross-subscription-azure-sign-in.md)]

[!INCLUDE [load-balancer-cross-subscription-create-resource-group](../../includes/load-balancer-cross-subscription-create-resource-group.md)]

## Create a load balancer

In this section, you create a load balancer in **Azure Subscription B** that is connected to a virtual network in **Azure Subscription A**. You create a load balancer with a frontend IP address.

# [Azure PowerShell](#tab/azurepowershell)

With Azure PowerShell, you'll:

- A load balancer with [`New-AzLoadBalancer`](/powershell/module/az.network/new-azloadbalancer)

- Create a public IP address with [`New-AzPublicIpAddress`](/powershell/module/az.network/new-azpublicipaddress)

- Add a frontend IP configuration with [`Add-AzLoadBalancerFrontendIpConfig`](/powershell/module/az.network/add-azloadbalancerfrontendipconfig)

- Create a backend address pool with [`New-AzLoadBalancerBackendAddressPool`](/powershell/module/az.network/new-azloadbalancerbackendaddresspool).

```azurepowershell

# Create a load balancer

$tag = @{

'IsRemoteFrontend'= 'true'

}

$loadbalancer = @{

ResourceGroupName = 'myResourceGroupLB'

Name = 'myLoadBalancer'

Location = 'westus'

Sku = 'Standard'

Tag = $tag

}

$LB = New-AzLoadBalancer @loadbalancer

$LBinfo = @{

ResourceGroupName = 'myResourceGroupLB'

Name = 'myLoadBalancer'

}

## Add load balancer frontend configuration and apply to load balancer.

$fip = @{

Name = 'myFrontEnd'

SubnetId = $vnet.subnets[0].Id

}

$LB = $LB | Add-AzLoadBalancerFrontendIpConfig @fip

$LB = $LB | Set-AzLoadBalancer

## Create backend address pool configuration and place in variable.

$be = @{

ResourceGroupName= "myResourceGroupLB"

Name= "myBackEndPool"

LoadBalancerName= "myLoadBalancer"

VirtualNetwork=$vnet.id

SyncMode= "Automatic"

}

# Create  the backend pool

$backend = New-AzLoadBalancerBackendAddressPool @be

$LB = Get-AzLoadBalancer @LBinfo

```

# [Azure CLI](#tab/azurecli/)

With Azure CLI, you create a load balancer with [`az network lb create`](/cli/azure/network/lb#az_network_lb_create) and update the backend pool. This example configures the following:

- A frontend IP address that receives the incoming network traffic on the load balancer.

- The private IP address is pulled from the cross-subscription virtual network.

- The `IsRemoteFrontend:True` tag is added since the IP address is cross-subscription.

- A backend address pool where the frontend IP sends the load balanced network traffic.

```azurecli

# Create a load balancer with a frontend IP address and backend address pool

az network lb create --resource-group myResourceGroupLB --name myLoadBalancer --sku Standard --subnet '/subscriptions/subscription A ID/resourceGroups/{resource group name} /providers/Microsoft.Network/virtualNetwork/{VNet name}/subnets/{subnet name}’  --frontend-ip-name myFrontEnd --backend-pool-name MyBackendPool --tags 'IsRemoteFrontend=true'

```

In order to utilize the cross-subscription feature of Azure load balancer, backend pools need to have the syncMode property enabled and a virtual network reference. This section updates the backend pool created prior by attaching the cross-subscription virtual network and enabling the syncMode property.

```azurecli

## Configure the backend address pool and syncMode property

az network lb address-pool update --lb-name myLoadBalancer --resource-group myResourceGroupLB -n myResourceGroupLB --vnet ‘/subscriptions/subscription A ID/resourceGroups/{resource group name} /providers/Microsoft.Network/virtualNetwork/{VNet name}’ --sync-mode Automatic

```

---

[!INCLUDE [load-balancer-cross-subscription-health-probe-rules](../../includes/load-balancer-cross-subscription-health-probe-rules.md)]

[!INCLUDE [load-balancer-cross-subscription-add-nic](../../includes/load-balancer-cross-subscription-add-nic.md)]

[!INCLUDE [load-balancer-cross-subscription-clean-up](../../includes/load-balancer-cross-subscription-clean-up.md)]

## Next steps

> [!div class="nextstepaction"]

> [Attach a cross-subscription frontend to an Azure Load Balancer](./cross-subscription-how-to-attach-frontend.md)


# Load Balancer Basic Upgrade Guidance

# Upgrading from Basic Load Balancer - Guidance

> [!IMPORTANT]

> On September 30, 2025, Basic Load Balancer was retired. For more information, see the [official announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). If you are currently using Basic Load Balancer, make sure to upgrade to Standard Load Balancer as soon as possible. This article will help guide you through the upgrade process.

In this article, we discuss guidance for upgrading your Basic Load Balancer instances to Standard Load Balancer. Standard Load Balancer is recommended for all production instances and provides many [key differences](#basic-load-balancer-sku-vs-standard-load-balancer-sku) to your infrastructure.

## Steps to complete the upgrade

We recommend the following approach for upgrading to Standard Load Balancer:

1. Learn about some of the [key differences](#basic-load-balancer-sku-vs-standard-load-balancer-sku) between Basic Load Balancer and Standard Load Balancer.

1. Identify the Basic Load Balancer to upgrade.

1. Create a migration plan for planned downtime.

1. Perform migration with [automated PowerShell scripts](#upgrade-using-automated-scripts-recommended) for your scenario or create a new Standard Load Balancer with the Basic Load Balancer configurations.

1. Verify your application and workloads are receiving traffic through the Standard Load Balancer. Then delete your Basic Load Balancer resource.

## Basic Load Balancer SKU vs. Standard Load Balancer SKU

This section lists out some key differences between these two Load Balancer SKUs.

| Feature | Standard Load Balancer SKU | Basic Load Balancer SKU |

| ---- | ---- | ---- |

| **Backend type** | IP based, NIC based | NIC based |

| **Protocol** | TCP, UDP | TCP, UDP |

| **Backend pool endpoints** | Any virtual machines or virtual machine scale sets in a single virtual network | Virtual machines in a single availability set or virtual machine scale set |

| **[Health probe protocol](load-balancer-custom-probe-overview.md#probe-protocol)** | TCP, HTTP, HTTPS | TCP, HTTP |

| **[Health probe down behavior](load-balancer-custom-probe-overview.md#probe-down-behavior)** | TCP connections stay alive on an instance probe down and on all probes down | TCP connections stay alive on an instance probe down. All TCP connections end when all probes are down |

| **Availability zones** | Zone-redundant and zonal frontends for inbound and outbound traffic | Not available |

| **Diagnostics** | [Azure Monitor multi-dimensional metrics](load-balancer-standard-diagnostics.md) | Not supported |

| **HA Ports** | [Available for Internal Load Balancer](load-balancer-ha-ports-overview.md) | Not available |

| **Secure by default** | Closed to inbound flows unless allowed by a network security group. Internal traffic from the virtual network to the internal load balancer is allowed. | Open by default. Network security group optional. |

| **Outbound Rules** | [Declarative outbound NAT configuration](load-balancer-outbound-connections.md#outboundrules) | Not available |

| **TCP Reset on Idle** | Available on any rule | Not available |

| **[Multiple front ends](load-balancer-multivip-overview.md)** | Inbound and [outbound](load-balancer-outbound-connections.md) | Inbound only |

| **Management Operations** | Most operations < 30 seconds | Most operations 60-90+ seconds |

| **SLA** | [99.99%](https://azure.microsoft.com/support/legal/sla/load-balancer/v1_0/) | Not available |

| **Global Virtual Network Peering Support** | Standard ILB is supported via Global Virtual Network Peering | Not supported |

| **[NAT Gateway Support](../virtual-network/nat-gateway/nat-overview.md)** | Both Standard ILB and Standard Public Load Balancer are supported via Nat Gateway | Not supported |

| **[Private Link Support](../private-link/private-link-overview.md)** | Standard ILB is supported via Private Link | Not supported |

| **[Global tier (Preview)](cross-region-overview.md)** | Standard Load Balancer supports the Global tier for Public LBs enabling cross-region load balancing | Not supported |

For information on limits, see [Load Balancer limits](../azure-resource-manager/management/azure-subscription-service-limits.md#load-balancer).

## Upgrade using automated scripts (recommended)

Use these PowerShell scripts to help with upgrading from Basic to Standard SKU:

- [Upgrading a Basic to Standard public load balancer with PowerShell](./upgrade-basic-standard-with-powershell.md)

## Upgrade manually

> [!NOTE]

> Although manually upgrading your Basic Load Balancer to a Standard Load Balancer using the Portal is an option, we recommend using the [**automated script option**](./upgrade-basic-standard-with-powershell.md) above, due to the number of steps and complexity of the migration. The automation ensures a consistent migration and minimizes downtime to load balanced applications.

> [!WARNING]

> Before manually upgrading a Basic Load Balancer, make sure that all Public IPs associated with both the Load Balancer and its backend Virtual Machines are set to 'static'. If you disassociate a Public IP or remove all backend VMs before changing the IP allocation to static, the IP address may be lost.

When manually migrating from a Basic to Standard SKU Load Balancer, there are a couple key considerations to keep in mind:

- It isn't possible to mix Basic and Standard SKU IPs or Load Balancers. All Public IPs associated with a Load Balancer and its backend pool members must match.

- Public IP allocation method must be set to 'static' when a Public IP is disassociated from a Load Balancer or Virtual Machine, or the allocated IP will be lost.

- Standard SKU public IP addresses are secure by default, requiring that a Network Security Group explicitly allow traffic to any public IPs

- Standard SKU Load Balancers block outbound access by default. To enable outbound access, a public load balancer needs an outbound rule for backend members. For private load balancers, either configure a NAT Gateway on the backend pool members' subnet or add instance-level public IP addresses to each backend member.

Suggested order of operations for manually upgrading a Basic Load Balancer in common virtual machine and virtual machine scale set configurations using the Portal:

1. Change all Public IPs associated with the Basic Load Balancer and backend Virtual Machines to 'static' allocation

1. For private Load Balancers, record the private IP addresses allocated to the frontend IP configurations

1. Record the backend pool membership of the Basic Load Balancer

1. Record the load balancing rules, NAT rules, and health probe configuration of the Basic Load Balancer

1. Create a new Standard SKU Load Balancer, matching the public or private configuration of the Basic Load Balancer. Name the frontend IP configuration something temporary. For public load balancers, use a new Public IP address for the frontend configuration. For guidance, see [Create a Public Load Balancer in the Portal](./quickstart-load-balancer-standard-public-portal.md) or [Create an Internal Load Balancer in the Portal](./quickstart-load-balancer-standard-internal-portal.md)

1. Duplicate the Basic SKU Load Balancer configuration for the following:

1. Backend pool names

1. Backend pool membership (virtual machines and virtual machine scale sets)

1. Health probes

1. Load balancing rules - use the temporary frontend configuration

1. NAT rules - use the temporary frontend configuration

1. For public load balancers, if you don't have one already, [create a new Network Security Group](../virtual-network/tutorial-filter-network-traffic.md) with allow rules for the traffic coming through the Load Balancer rules

1. For Virtual Machine Scale Set backends, remove the Load Balancer association in the Networking settings and [update the instances](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-perform-manual-upgrades)

1. Delete the Basic Load Balancer

> [!NOTE]

> For Virtual Machine Scale Set backends, you'll need to remove the load balancer association in the Networking settings. Once removed, you'll also need to [**update the instances**](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-perform-manual-upgrades)

1. [Upgrade all Public IPs](../virtual-network/ip-services/public-ip-upgrade-portal.md) previously associated with the Basic Load Balancer and backend Virtual Machines to Standard SKU. For Virtual Machine Scale Sets, remove any instance-level public IP configuration, update the instances, then add a new one with Standard SKU and update the instances again.

1. Recreate the frontend configurations from the Basic Load Balancer on the newly created Standard Load Balancer, using the same public or private IP addresses as on the Basic Load Balancer

1. Update the load balancing and NAT rules to use the appropriate frontend configurations

1. For public Load Balancers, [create one or more outbound rules](./outbound-rules.md) to enable internet access for backend pools

1. Remove the temporary frontend configuration

1. Test that inbound and outbound traffic flow through the new Standard Load Balancer as expected

## FAQ

### Will the Basic Load Balancer retirement impact Cloud Services Extended Support (CSES) deployments?

No, this retirement won't impact your existing or new deployments on CSES. This means that you can still create and use Basic Load Balancers for CSES deployments. However, we advise using Standard SKU on Azure Resource Manager (ARM) native resources (those that don't depend on CSES) when possible, because Standard has more advantages than Basic.

### What will happen to my Basic Load Balancer resource post-retirement (September 30, 2025)?

Basic Load Balancers will remain operational after September 30, 2025, giving users more time to transition to Standard SKU. Customers who choose to continue using Basic Load Balancers after retirement date accept the risks and acknowledge that the service is unsupported and not covered by SLA guarantees.

## Next Steps

For guidance on upgrading Basic Public IP addresses to Standard SKUs, see:

> [!div class="nextstepaction"]

> [Upgrading a Basic Public IP to Standard Public IP - Guidance](../virtual-network/ip-services/public-ip-basic-upgrade-guidance.md)


# Upgrade Basic Standard With Powershell

# Upgrade a basic load balancer with PowerShell

>[!Important]

>On September 30, 2025, Basic Load Balancer was retired. For more information, see the [official announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). If you are currently using Basic Load Balancer, make sure to upgrade to Standard Load Balancer as soon as possible.

[Azure Standard Load Balancer](load-balancer-overview.md) offers a rich set of functionality and high availability through zone redundancy. To learn more about Load Balancer SKU, see [comparison table](./skus.md#skus).

This article introduces a PowerShell module that creates a Standard Load Balancer with the same configuration as the Basic Load Balancer, then associates the Virtual Machine Scale Set or Virtual Machine backend pool members with the new Load Balancer.

For an in-depth walk-through of the upgrade module and process, see the following video:

> [!VIDEO 8e203b99-41ff-4454-9cbd-58856708f1c6]

- 03:06 - <a href="https://learn-video.azurefd.net/vod/player?id=8e203b99-41ff-4454-9cbd-58856708f1c6?#time=0h3m06s" target="_blank">Step-by-step</a>

- 32:54 - <a href="https://learn-video.azurefd.net/vod/player?id=8e203b99-41ff-4454-9cbd-58856708f1c6#time=0h32m45s" target="_blank">Recovery</a>

- 40:55 - <a href="https://learn-video.azurefd.net/vod/player?id=8e203b99-41ff-4454-9cbd-58856708f1c6#time=0h40m55s" target="_blank">Advanced Scenarios</a>

- 57:54 - <a href="https://learn-video.azurefd.net/vod/player?id=8e203b99-41ff-4454-9cbd-58856708f1c6#time=0h57m54s" target="_blank">Resources</a>

## Upgrade Overview

The PowerShell module performs the following functions:

- Verifies that the provided Basic Load Balancer scenario is supported for upgrade.

- Backs up the Basic Load Balancer and Virtual Machine Scale Set configuration, enabling retry on failure or if errors are encountered.

- For public load balancers, updates the front end public IP addresses to Standard SKU and static assignment

- Upgrades the Basic Load Balancer configuration to a new Standard Load Balancer, ensuring configuration and feature parity.

- Migrates Virtual Machine Scale Set and Virtual Machine backend pool members from the Basic Load Balancer to the Standard Load Balancer.

- Creates and associates a network security group with the Virtual Machine Scale Set or Virtual Machine to ensure load balanced traffic reaches backend pool members. This follows Standard Load Balancer's move to a default-deny network policy.

- Upgrades instance-level Public IP addresses associated with Virtual Machine Scale Set or Virtual Machine instances

- Upgrades Inbound NAT Pools to Inbound NAT Rules for Virtual Machine Scale Set backends, creating a new backend pool for each migrated NAT Pool. Specify `-skipUpgradeNATPoolsToNATRules` to skip this upgrade and use the [standalone NAT Pool migration module](load-balancer-nat-pool-migration.md) later for more backend pool options.

- Logs the upgrade operation for easy audit and failure recovery.

>[!WARNING]

> Migrating _internal_ Basic Load Balancers where the backend VMs or VMSS instances do not have Public IP Addresses requires additional steps for backend connectivity to the internet. Review [How should I configure outbound traffic for my Load Balancer?](#how-should-i-configure-outbound-traffic-for-my-load-balancer)

>[!NOTE]

> If the Virtual Machine Scale Set in the Load Balancer backend pool has Public IP Addresses in its network configuration, the Public IP Addresses associated with each Virtual Machine Scale Set instance will change when they are upgraded to Standard SKU. This is because scale set instance-level Public IP addresses cannot be upgraded, only replaced with a new Standard SKU Public IP. All other Public IP addresses will be retained through the migration.

>[!NOTE]

> If the Virtual Machine Scale Set behind the Load Balancer is a **Service Fabric Cluster**, migration with this script will take more time, is higher risk to your application, and will cause downtime. Review [Service Fabric Cluster Load Balancer upgrade guidance](https://aka.ms/sfc-lb-upgrade) for migration options.

### Unsupported Scenarios

- Basic Load Balancers with IPv6 frontend IP configurations

- Basic Load Balancers for [Azure Kubernetes Services (AKS) clusters](/azure/aks/load-balancer-standard#moving-from-a-basic-sku-load-balancer-to-standard-sku)

- Basic Load Balancers with a Virtual Machine Scale Set backend pool member where one or more Virtual Machine Scale Set instances have ProtectFromScaleSetActions Instance Protection policies enabled

- Migrating a Basic Load Balancer to an existing Standard Load Balancer

- Basic Load Balancers with backend pool members that are part of an Availability Set but not all members of the Availability Set are behind the load balancer

- If your Basic Load Balancer has floating IP enabled on a secondary IP configuration of the network interface, update the floating IP to a primary IP before running the migration script to avoid any configuration issues

## Install the 'AzureBasicLoadBalancerUpgrade' module

### Prerequisites

- **PowerShell**: A supported version of PowerShell version 7 or higher is recommended for use with the AzureBasicLoadBalancerUpgrade module on all platforms including Windows, Linux, and macOS. However, PowerShell 5.1 on Windows is supported.

### Module Installation

Install the module from [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureBasicLoadBalancerUpgrade)

```powershell

Install-Module -Name AzureBasicLoadBalancerUpgrade -Scope CurrentUser -Repository PSGallery -Force

```

## Pre- and Post-migration Steps

### Pre-migration steps

- [Validate](#example-validate-a-scenario) support for your scenario

- Plan for [application downtime](#how-long-does-the-upgrade-take) during migration

- Develop inbound and outbound connectivity tests for your traffic

- Plan for instance-level Public IP changes on Virtual Machine Scale Set instances (see note)

- [Recommended] Create Network Security Groups or add security rules to an existing Network Security Group for your backend pool members. Allow the traffic through the Load Balancer along with any other traffic to be explicitly allowed on public Standard SKU resources

- [Recommended] Prepare your [outbound connectivity](../virtual-network/ip-services/default-outbound-access.md), taking one of the following approaches described in [How should I configure outbound traffic for my Load Balancer?](#how-should-i-configure-outbound-traffic-for-my-load-balancer)

- [Important] Remove all locks from the load balancer, its resource group, and any related resources before starting the migration

- [Important] Confirm you have the necessary permissions to delete and create load balancers, and to modify associated Virtual Machine Scale Sets (VMSS) and network interfaces

### Post-migration steps

- [Validate that your migration was successful](#example-validate-completed-migration)

- Test inbound application connectivity through the Load Balancer

- Test outbound connectivity from backend pool members to the Internet

- For Public Load Balancers with multiple backend pools, create [Outbound Rules](./outbound-rules.md) for each backend pool

## Use the module

1. Ensure you selected the Basic Load Balancer's subscription ID by running `Select-AzSubscription`.

```powershell

Select-AzSubscription -Subscription <SubscriptionId>

```

2. Find the Load Balancer you wish to upgrade. Record its name and resource group name.

3. Examine the basic module parameters:

- *BasicLoadBalancerName [string] Required* - This parameter is the name of the existing Basic Load Balancer you would like to upgrade

- *ResourceGroupName [string] Required* - This parameter is the name of the resource group containing the Basic Load Balancer

- *StandardLoadBalancerName [string] Optional* - Use this parameter to optionally configure a new name for the Standard Load Balancer. If not specified, the Basic Load Balancer name is reused.

- *RecoveryBackupPath [string] Optional* - This parameter allows you to specify an alternative path in which to store the Basic Load Balancer ARM template backup file (defaults to the current working directory)

>[!TIP]

>Additional parameters for advanced and recovery scenarios can be viewed by running `Get-Help Start-AzBasicLoadBalancerUpgrade -Detailed`

4. Run the `Start-AzBasicLoadBalancerUpgrade` command, using the following examples for guidance.

### Example: validate a scenario

Validate that a Basic Load Balancer is supported for upgrade

```powershell

Start-AzBasicLoadBalancerUpgrade -ResourceGroupName <loadBalancerRGName> -BasicLoadBalancerName <basicLBName> -validateScenarioOnly:$true

```

### Example: upgrade by name

Upgrade a Basic Load Balancer to a Standard Load Balancer with the same name, providing the Basic Load Balancer name and resource group name

```powershell

Start-AzBasicLoadBalancerUpgrade -ResourceGroupName <loadBalancerRGName> -BasicLoadBalancerName <basicLBName>

```

### Example: upgrade, change name, and show logs

Upgrade a Basic Load Balancer to a Standard Load Balancer with the specified name displayed in the logged output

```powershell

Start-AzBasicLoadBalancerUpgrade -ResourceGroupName <loadBalancerRGName> -BasicLoadBalancerName <basicLBName> -StandardLoadBalancerName <newStandardLBName> -FollowLog

```

### Example: upgrade with alternate backup path

Upgrade a Basic Load Balancer to a Standard Load Balancer with the specified name and store the Basic Load Balancer backup file at the specified path

```powershell

Start-AzBasicLoadBalancerUpgrade -ResourceGroupName <loadBalancerRGName> -BasicLoadBalancerName <basicLBName> -StandardLoadBalancerName <newStandardLBName> -RecoveryBackupPath C:\BasicLBRecovery

```

### Example: validate completed migration

Validate a completed migration by passing the Basic Load Balancer state file backup and the Standard Load Balancer name

```powershell

Start-AzBasicLoadBalancerUpgrade -validateCompletedMigration -StandardLoadBalancerName <newStandardLBName> -basicLoadBalancerStatePath C:\RecoveryBackups\State_mybasiclb_rg-basiclbrg_20220912T1740032148.json

```

### Example: migrate multiple, related Load Balancers

Migrate multiple Load Balancers with shared backend members at the same time, usually when an application has an internal and an external Load Balancer

```powershell

# build array of multiple basic load balancers

$multiLBConfig = @(

@{

'standardLoadBalancerName' = 'myStandardInternalLB01' # specifying the standard load balancer name is optional

'basicLoadBalancer' = (Get-AzLoadBalancer -ResourceGroupName myRG -Name myBasicInternalLB01)

},

@{

'standardLoadBalancerName' = 'myStandardExternalLB02'

'basicLoadBalancer' = (Get-AzLoadBalancer -ResourceGroupName myRG -Name myBasicExternalLB02)

}

)

# pass the array of load balancer configurations to the -MultiLBConfig parameter

Start-AzBasicLoadBalancerUpgrade -MultiLBConfig $multiLBConfig

```

### Example: retry failed virtual machine scale set migration

Retry a failed upgrade for a virtual machine scale set's load balancer (due to error or script termination) by providing the Basic Load Balancer and Virtual Machine Scale Set backup state file

```powershell

Start-AzBasicLoadBalancerUpgrade -FailedMigrationRetryFilePathLB C:\RecoveryBackups\State_mybasiclb_rg-basiclbrg_20220912T1740032148.json -FailedMigrationRetryFilePathVMSS C:\RecoveryBackups\VMSS_myVMSS_rg-basiclbrg_20220912T1740032148.json

```

### Example: retry failed virtual machine migration

Retry a failed upgrade for a VM load balancer (due to error or script termination) by providing the Basic Load Balancer backup state file

```powershell

Start-AzBasicLoadBalancerUpgrade -FailedMigrationRetryFilePathLB C:\RecoveryBackups\State_mybasiclb_rg-basiclbrg_20220912T1740032148.json

```

## Common Questions

### How can I list the Basic Load Balancers to be migrated in my environment?

One way to get a list of the Basic Load Balancers needing to be migrated in your environment is to use an Azure Resource Graph query. The following query lists all the Basic Load Balancers you have access to view:

```kusto

Resources

| where type == 'microsoft.network/loadbalancers' and sku.name == 'Basic'

```

''

We created a complex query which assesses the readiness of each Basic Load Balancer for migration on most of the criteria this module checks during [validation](#example-validate-a-scenario). The Resource Graph query can be found in our [GitHub project](https://github.com/Azure/AzLoadBalancerMigration/blob/main/AzureBasicLoadBalancerUpgrade/utilities/migration_graph_query.txt) or opened in the [Azure Resource Graph Explorer](https://portal.azure.com/?#blade/HubsExtension/ArgQueryBlade/query/resources%0A%7C%20where%20type%20%3D%3D%20%27microsoft.network%2Floadbalancers%27%20and%20sku.name%20%3D%3D%20%27Basic%27%0A%7C%20project%20fes%20%3D%20properties.frontendIPConfigurations%2C%20bes%20%3D%20properties.backendAddressPools%2C%5B%27id%27%5D%2C%5B%27tags%27%5D%2CsubscriptionId%2CresourceGroup%2Cname%0A%7C%20extend%20backendPoolCount%20%3D%20array_length%28bes%29%0A%7C%20extend%20internalOrExternal%20%3D%20iff%28isnotempty%28fes%29%2Ciff%28isnotempty%28fes%5B0%5D.properties.privateIPAddress%29%2C%27Internal%27%2C%27External%27%29%2C%27None%27%29%0A%20%20%20%20%7C%20join%20kind%3Dleftouter%20hint.strategy%3Dshuffle%20%28%0A%20%20%20%20%20%20%20%20resources%0A%20%20%20%20%20%20%20%20%7C%20where%20type%20%3D%3D%20%27microsoft.network%2Fpublicipaddresses%27%0A%20%20%20%20%20%20%20%20%7C%20where%20properties.publicIPAddressVersion%20%3D%3D%20%27IPv6%27%0A%20%20%20%20%20%20%20%20%7C%20extend%20publicIPv6LBId%20%3D%20tostring%28split%28properties.ipConfiguration.id%2C%27%2FfrontendIPConfigurations%2F%27%29%5B0%5D%29%0A%20%20%20%20%20%20%20%20%7C%20distinct%20publicIPv6LBId%0A%20%20%20%20%29%20on%20%24left.id%20%3D%3D%20%24right.publicIPv6LBId%0A%20%20%20%20%7C%20join%20kind%20%3D%20leftouter%20hint.strategy%3Dshuffle%20%28%0A%20%20%20%20%20%20%20%20resources%20%0A%20%20%20%20%20%20%20%20%7C%20where%20type%20%3D%3D%20%27microsoft.network%2Fnetworkinterfaces%27%20and%20isnotempty%28properties.virtualMachine.id%29%0A%20%20%20%20%20%20%20%20%7C%20extend%20vmNICHasNSG%20%3D%20isnotnull%28properties.networkSecurityGroup.id%29%0A%20%20%20%20%20%20%20%20%7C%20extend%20vmNICSubnetIds%20%3D%20tostring%28extract_all%28%27%28%2Fsubscriptions%2F%5Ba-f0-9-%5D%2B%3F%2FresourceGroups%2F%5Ba-zA-Z0-9-_%5D%2B%3F%2Fproviders%2FMicrosoft.Network%2FvirtualNetworks%2F%5Ba-zA-Z0-9-_%5D%2B%3F%2Fsubnets%2F%5Ba-zA-Z0-9-_%5D%2A%29%27%2Ctostring%28properties.ipConfigurations%29%29%29%0A%20%20%20%20%20%20%20%20%7C%20mv-expand%20ipConfigs%20%3D%20properties.ipConfigurations%0A%20%20%20%20%20%20%20%20%7C%20extend%20vmPublicIPId%20%3D%20extract%28%27%2Fsubscriptions%2F%5Ba-f0-9-%5D%2B%3F%2FresourceGroups%2F%5Ba-zA-Z0-9-_%5D%2B%3F%2Fproviders%2FMicrosoft.Network%2FpublicIPAddresses%2F%5Ba-zA-Z0-9-_%5D%2A%27%2C0%2Ctostring%28ipConfigs%29%29%0A%20%20%20%20%20%20%20%20%7C%20where%20isnotempty%28ipConfigs.properties.loadBalancerBackendAddressPools%29%20%0A%20%20%20%20%20%20%20%20%7C%20mv-expand%20bes%20%3D%20ipConfigs.properties.loadBalancerBackendAddressPools%0A%20%20%20%20%20%20%20%20%7C%20extend%20nicLoadBalancerId%20%3D%20tostring%28split%28bes.id%2C%27%2FbackendAddressPools%2F%27%29%5B0%5D%29%0A%20%20%20%20%20%20%20%20%7C%20summarize%20vmNICsNSGStatus%20%3D%20make_set%28vmNICHasNSG%29%20by%20nicLoadBalancerId%2CvmPublicIPId%2CvmNICSubnetIds%0A%20%20%20%20%20%20%20%20%7C%20extend%20allVMNicsHaveNSGs%20%3D%20set_has_element%28vmNICsNSGStatus%2CFalse%29%0A%20%20%20%20%20%20%20%20%7C%20summarize%20publicIpCount%20%3D%20dcount%28vmPublicIPId%29%20by%20nicLoadBalancerId%2C%20allVMNicsHaveNSGs%2C%20vmNICSubnetIds%0A%20%20%20%20%20%20%20%20%29%20on%20%24left.id%20%3D%3D%20%24right.nicLoadBalancerId%0A%20%20%20%20%20%20%20%20%7C%20join%20kind%20%3D%20leftouter%20%28%0A%20%20%20%20%20%20%20%20%20%20%20%20resources%0A%20%20%20%20%20%20%20%20%20%20%20%20%7C%20where%20type%20%3D%3D%20%27microsoft.compute%2Fvirtualmachinescalesets%27%0A%20%20%20%20%20%20%20%20%20%20%20%20%7C%20extend%20vmssSubnetIds%20%3D%20tostring%28extract_all%28%27%28%2Fsubscriptions%2F%5Ba-f0-9-%5D%2B%3F%2FresourceGroups%2F%5Ba-zA-Z0-9-_%5D%2B%3F%2Fproviders%2FMicrosoft.Network%2FvirtualNetworks%2F%5Ba-zA-Z0-9-_%5D%2B%3F%2Fsubnets%2F%5Ba-zA-Z0-9-_%5D%2A%29%27%2Ctostring%28properties.virtualMachineProfile.networkProfile.networkInterfaceConfigurations%29%29%29%0A%20%20%20%20%20%20%20%20%20%20%20%20%7C%20mv-expand%20nicConfigs%20%3D%20properties.virtualMachineProfile.networkProfile.networkInterfaceConfigurations%0A%20%20%20%20%20%20%20%20%20%20%20%20%7C%20extend%20vmssNicHasNSG%20%3D%20isnotnull%28properties.networkSecurityGroup.id%29%0A%20%20%20%20%20%20%20%20%20%20%20%20%7C%20mv-expand%20ipConfigs%20%3D%20nicConfigs.properties.ipConfigurations%0A%20%20%20%20%20%20%20%20%20%20%20%20%7C%20extend%20vmssHasPublicIPConfig%20%3D%20iff%28tostring%28ipConfigs%29%20matches%20regex%20%40%27publicIPAddressVersion%27%2Ctrue%2Cfalse%29%0A%20%20%20%20%20%20%20%20%20%20%20%20%7C%20where%20isnotempty%28ipConfigs.properties.loadBalancerBackendAddressPools%29%0A%20%20%20%20%20%20%20%20%20%20%20%20%7C%20mv-expand%20bes%20%3D%20ipConfigs.properties.loadBalancerBackendAddressPools%0A%20%20%20%20%20%20%20%20%20%20%20%20%7C%20extend%20vmssLoadBalancerId%20%3D%20tostring%28split%28bes.id%2C%27%2FbackendAddressPools%2F%27%29%5B0%5D%29%0A%20%20%20%20%20%20%20%20%20%20%20%20%7C%20summarize%20vmssNICsNSGStatus%20%3D%20make_set%28vmssNicHasNSG%29%20by%20vmssLoadBalancerId%2C%20vmssHasPublicIPConfig%2C%20vmssSubnetIds%0A%20%20%20%20%20%20%20%20%20%20%20%20%7C%20extend%20allVMSSNicsHaveNSGs%20%3D%20set_has_element%28vmssNICsNSGStatus%2CFalse%29%0A%20%20%20%20%20%20%20%20%20%20%20%20%7C%20distinct%20vmssLoadBalancerId%2C%20vmssHasPublicIPConfig%2C%20allVMSSNicsHaveNSGs%2C%20vmssSubnetIds%0A%20%20%20%20%20%20%20%20%29%20on%20%24left.id%20%3D%3D%20%24right.vmssLoadBalancerId%0A%7C%20extend%20subnetIds%20%3D%20set_difference%28todynamic%28coalesce%28vmNICSubnetIds%2CvmssSubnetIds%29%29%2Cdynamic%28%5B%5D%29%29%20%2F%2F%20return%20only%20unique%20subnet%20ids%0A%7C%20mv-expand%20subnetId%20%3D%20subnetIds%0A%7C%20extend%20subnetId%20%3D%20tostring%28subnetId%29%0A%7C%20project-away%20vmNICSubnetIds%2C%20vmssSubnetIds%2C%20subnetIds%0A%7C%20extend%20backendType%20%3D%20iff%28isnotempty%28bes%29%2Ciff%28isnotempty%28nicLoadBalancerId%29%2C%27VMs%27%2Ciff%28isnotempty%28vmssLoadBalancerId%29%2C%27VMSS%27%2C%27Empty%27%29%29%2C%27Empty%27%29%0A%7C%20extend%20lbHasIPv6PublicIP%20%3D%20iff%28isnotempty%28publicIPv6LBId%29%2Ctrue%2Cfalse%29%0A%7C%20project-away%20fes%2C%20bes%2C%20nicLoadBalancerId%2C%20vmssLoadBalancerId%2C%20publicIPv6LBId%2C%20subnetId%0A%7C%20extend%20vmsHavePublicIPs%20%3D%20iff%28publicIpCount%20%3E%200%2Ctrue%2Cfalse%29%0A%7C%20extend%20vmssHasPublicIPs%20%3D%20iff%28isnotempty%28vmssHasPublicIPConfig%29%2CvmssHasPublicIPConfig%2Cfalse%29%0A%7C%20extend%20warnings%20%3D%20dynamic%28%5B%5D%29%0A%7C%20extend%20errors%20%3D%20dynamic%28%5B%5D%29%0A%7C%20extend%20warnings%20%3D%20iff%28vmssHasPublicIPs%2Carray_concat%28warnings%2Cdynamic%28%5B%27VMSS%20instances%20have%20Public%20IPs%3A%20VMSS%20Public%20IPs%20will%20change%20during%20migration%27%2C%27VMSS%20instances%20have%20Public%20IPs%3A%20NSGs%20will%20be%20required%20for%20internet%20access%20through%20VMSS%20instance%20public%20IPs%20once%20upgraded%20to%20Standard%20SKU%27%5D%29%29%2Cwarnings%29%0A%7C%20extend%20warnings%20%3D%20iff%28vmsHavePublicIPs%2Carray_concat%28warnings%2Cdynamic%28%5B%27VMs%20have%20Public%20IPs%3A%20NSGs%20will%20be%20required%20for%20internet%20access%20through%20VM%20public%20IPs%20once%20upgraded%20to%20Standard%20SKU%27%5D%29%29%2Cwarnings%29%0A%7C%20extend%20warnings%20%3D%20iff%28%28backendType%20%3D%3D%20%27VMs%27%20and%20internalOrExternal%20%3D%3D%20%27Internal%27%20and%20not%28vmsHavePublicIPs%29%29%2Carray_concat%28warnings%2Cdynamic%28%5B%27Internal%20Load%20Balancer%3A%20LB%20is%20internal%20and%20VMs%20do%20not%20have%20Public%20IPs.%20Unless%20internet%20traffic%20is%20already%20%20being%20routed%20through%20an%20NVA%2C%20VMs%20will%20have%20no%20internet%20connectivity%20post-migration%20without%20additional%20action.%27%5D%29%29%2Cwarnings%29%0A%7C%20extend%20warnings%20%3D%20iff%28%28backendType%20%3D%3D%20%27VMSS%27%20and%20internalOrExternal%20%3D%3D%20%27Internal%27%20and%20not%28vmssHasPublicIPs%29%29%2Carray_concat%28warnings%2Cdynamic%28%5B%27Internal%20Load%20Balancer%3A%20LB%20is%20internal%20and%20VMSS%20instances%20do%20not%20have%20Public%20IPs.%20Unless%20internet%20traffic%20is%20already%20being%20routed%20through%20an%20NVA%2C%20VMSS%20instances%20will%20have%20no%20internet%20connectivity%20post-migration%20without%20additional%20action.%27%5D%29%29%2Cwarnings%29%0A%7C%20extend%20warnings%20%3D%20iff%28%28internalOrExternal%20%3D%3D%20%27External%27%20and%20backendPoolCount%20%3E%201%29%2Carray_concat%28warnings%2Cdynamic%28%5B%27External%20Load%20Balancer%3A%20LB%20is%20external%20and%20has%20multiple%20backend%20pools.%20Outbound%20rules%20will%20not%20be%20created%20automatically.%27%5D%29%29%2Cwarnings%29%0A%7C%20extend%20warnings%20%3D%20iff%28%28backendType%20%3D%3D%20%27VMs%27%20and%20%28vmsHavePublicIPs%20or%20internalOrExternal%20%3D%3D%20%27External%27%29%20and%20not%28allVMNicsHaveNSGs%29%29%2Carray_concat%28warnings%2Cdynamic%28%5B%27VMs%20Missing%20NSGs%3A%20Not%20all%20VM%20NICs%20or%20subnets%20have%20associated%20NSGs.%20An%20NSG%20will%20be%20created%20to%20allow%20load%20balanced%20traffic%2C%20but%20it%20is%20preferred%20that%20you%20create%20and%20associate%20an%20NSG%20before%20starting%20the%20migration.%27%5D%29%29%2Cwarnings%29%0A%7C%20extend%20warnings%20%3D%20iff%28%28backendType%20%3D%3D%20%27VMSS%27%20and%20%28vmssHasPublicIPs%20or%20internalOrExternal%20%3D%3D%20%27External%27%29%20and%20not%28allVMSSNicsHaveNSGs%29%29%2Carray_concat%28warnings%2Cdynamic%28%5B%27VMSS%20Missing%20NSGs%3A%20Not%20all%20VMSS%20NICs%20or%20subnets%20have%20associated%20NSGs.%20An%20NSG%20will%20be%20created%20to%20allow%20load%20balanced%20traffic%2C%20but%20it%20is%20preferred%20that%20you%20create%20and%20associate%20an%20NSG%20before%20starting%20the%20migration.%27%5D%29%29%2Cwarnings%29%0A%7C%20extend%20warnings%20%3D%20iff%28%28bag_keys%28tags%29%20contains%20%27resourceType%27%20and%20tags%5B%27resourceType%27%5D%20%3D%3D%20%27Service%20Fabric%27%29%2Carray_concat%28warnings%2Cdynamic%28%5B%27Service%20Fabric%20LB%3A%20LB%20appears%20to%20be%20in%20front%20of%20a%20Service%20Fabric%20Cluster.%20Unmanaged%20SF%20clusters%20may%20take%20an%20hour%20or%20more%20to%20migrate%3B%20managed%20are%20not%20supported%27%5D%29%29%2Cwarnings%29%0A%7C%20extend%20warningCount%20%3D%20array_length%28warnings%29%0A%7C%20extend%20errors%20%3D%20iff%28%28internalOrExternal%20%3D%3D%20%27External%27%20and%20lbHasIPv6PublicIP%29%2Carray_concat%28errors%2Cdynamic%28%5B%27External%20Load%20Balancer%20has%20IPv6%3A%20LB%20is%20external%20and%20has%20an%20IPv6%20Public%20IP.%20Basic%20SKU%20IPv6%20public%20IPs%20cannot%20be%20upgraded%20to%20Standard%20SKU%27%5D%29%29%2Cerrors%29%0A%7C%20extend%20errors%20%3D%20iff%28%28id%20matches%20regex%20%40%27%2F%28kubernetes%7Ckubernetes-internal%29%5E%27%20or%20%28bag_keys%28tags%29%20contains%20%27aks-managed-cluster-name%27%29%29%2Carray_concat%28errors%2Cdynamic%28%5B%27AKS%20Load%20Balancer%3A%20Load%20balancer%20appears%20to%20be%20in%20front%20of%20a%20Kubernetes%20cluster%2C%20which%20is%20not%20supported%20for%20migration%27%5D%29%29%2Cerrors%29%0A%7C%20extend%20errorCount%20%3D%20array_length%28errors%29%0A%7C%20project%20id%2CinternalOrExternal%2Cwarnings%2Cerrors%2CwarningCount%2CerrorCount%2CsubscriptionId%2CresourceGroup%2Cname%0A%7C%20sort%20by%20errorCount%2CwarningCount%0A%7C%20project-away%20errorCount%2CwarningCount).

### Will this migration cause downtime to my application?

Yes, because the Basic Load Balancer needs to be removed before the new Standard Load Balancer can be created, there's downtime to your application. See [How long does the Upgrade take?](#how-long-does-the-upgrade-take)

### Will the module migrate my frontend IP address to the new Standard Load Balancer?

Yes, for both public and internal load balancers, the module ensures that front end IP addresses are maintained. For public IPs, the IP is converted to a static IP before migration. For internal front ends, the module attempts to reassign the same IP address freed up when the Basic Load Balancer was deleted. If the private IP isn't available the script fails (see [What happens if my upgrade fails mid-migration?](#what-happens-if-my-upgrade-fails-mid-migration)).

### How long does the Upgrade take?

The upgrade normally takes a few minutes for the script to finish. The following factors may lead to longer upgrade times:

- Complexity of your load balancer configuration

- Number of backend pool members

- Instance count of associated Virtual Machine Scale Sets or Virtual Machines

- Service Fabric Cluster: Upgrades for Service Fabric Clusters take around an hour in testing

Keep the downtime in mind and plan for failover if necessary.

### Does the script migrate my backend pool members from my Basic Load Balancer to the newly created Standard Load Balancer?

Yes. The Azure PowerShell script migrates the Virtual Machine Scale Sets and Virtual Machines to the newly created Standard Load Balancer backend pools.

### Which load balancer components are migrated?

The script migrates the following from the Basic Load Balancer to the Standard Load Balancer:

**Public and Private Load Balancers:**

- Health Probes:

- All probes are migrated to the new Standard Load Balancer

- Load balancing rules:

- All load balancing rules are migrated to the new Standard Load Balancer

- Inbound NAT Rules:

- All user-created NAT rules are migrated to the new Standard Load Balancer

- Inbound NAT Pools:

- By default, NAT Pools are upgraded to NAT Rules

- To migrate NAT Pools instead, specify the `-skipUpgradeNATPoolsToNATRules` parameter when upgrading

- Backend pools:

- All backend pools are migrated to the new Standard Load Balancer

- All Virtual Machine Scale Set and Virtual Machine network interfaces and IP configurations are migrated to the new Standard Load Balancer

- If a Virtual Machine Scale Set is using Rolling Upgrade policy, the script will update the Virtual Machine Scale Set upgrade policy to "Manual" during the migration process and revert it back to "Rolling" after the migration is completed.

- Instance-level Public IP addresses

- For both Virtual Machines and Virtual Machine Scale Sets, converts attached Public IPs from Basic to Standard SKU. Note, Scale Set instance Public IPs change during the upgrade; virtual machine IPs don't.

- Tags from the Basic Load Balancer to Standard Load Balancer

**Public Load Balancer:**

- Public frontend IP configuration

- Converts the public IP to a static IP, if dynamic

- Updates the public IP SKU to Standard, if Basic

- Upgrade all associated public IPs to the new Standard Load Balancer

- Outbound Rules:

- Basic load balancers don't support configured outbound rules. The script creates an outbound rule in the Standard load balancer to preserve the outbound behavior of the Basic load balancer. For more information about outbound rules, see [Outbound rules](./outbound-rules.md).

- Network security group

- Basic Load Balancer doesn't require a network security group to allow outbound connectivity. In case there's no network security group associated with the Virtual Machine Scale Set, a new network security group is created to preserve the same functionality. This new network security group is associated to the Virtual Machine Scale Set backend pool member network interfaces. It allows the same load balancing rules, ports, and protocols along with preserving outbound connectivity.

**Internal Load Balancer:**

- Private frontend IP configuration

>[!NOTE]

> Network security groups are not configured as part of Internal Load Balancer upgrade. To learn more about NSGs, see [Network security groups](../virtual-network/network-security-groups-overview.md)

### How do I migrate when my backend pool members belong to multiple Load Balancers?

In a scenario where your backend pool members are also members of backend pools on another Load Balancer, such as when you have internal and external Load Balancers for the same application, the Basic Load Balancers need to be migrated at the same time. Trying to migrate the Load Balancers one at a time would attempt to mix Basic and Standard SKU resources, which isn't allowed. The migration script supports this by passing multiple Basic Load Balancers into the same [script execution using the `-MultiLBConfig` parameter](#example-migrate-multiple-related-load-balancers).

### How do I validate that a migration was successful?

At the end of its execution, the upgrade module performs the following validations, comparing the Basic Load Balancer to the new Standard Load Balancer. In a failed migration, this same operation can be called using the `-validateCompletedMigration` and `-basicLoadBalancerStatePath` parameters to determine the configuration state of the Standard Load Balancer (if one was created). The log file created during the migration also provides extensive detail on the migration operation and any errors.

- The Standard Load Balancer exists and its SKU is 'Standard'

- The count of front end IP configurations match and that the IP addresses are the same

- The count of backend pools and their memberships matches

- The count of load balancing rules matches

- The count of health probes matches

- The count of inbound NAT rules matches

- The count of inbound NAT pools matches

- External Standard Load Balancers have a configured outbound rule

- External Standard Load Balancer backend pool members have associated Network Security Groups

### How should I configure outbound traffic for my Load Balancer?

Standard SKU Load Balancers don't allow default outbound access for their backend pool members. Allowing outbound access to the internet requires more steps.

For external Load Balancers, you can use [Outbound Rules](./outbound-rules.md) to explicitly enable outbound traffic for your pool members. If you have a single backend pool, we automatically configure an Outbound Rule for you during migration; if you have more than one backend pool, you need to manually create your Outbound Rules to specify port allocations.

For internal Load Balancers, Outbound Rules aren't an option because there's no Public IP address to SNAT through. This leaves a couple options to consider:

- **NAT Gateway**: NAT Gateways are Azure's recommended approach for outbound traffic in most cases. However, NAT Gateways require that the attached subnet has no basic SKU network resources--meaning you need to have migrated all your Load Balancers and Public IP Addresses before you can use them. For this reason, we recommend using a two step approach where you first use one of the following approaches for outbound connectivity, then [switch to NAT Gateways](../virtual-network/nat-gateway/tutorial-nat-gateway-load-balancer-internal-portal.md) once your basic SKU migrations are complete.

- **Network Virtual Appliance**: Route your traffic through a Network Virtual Appliance, such as an Azure Firewall, to route your traffic to the internet. This option is ideal if you already have a Network Virtual Appliance configured.

- **Secondary External Load Balancer**: By adding a secondary external Load Balancer to your backend resources, you can use the external Load Balancer for outbound traffic by configuring outbound rules. If this external Load Balancer doesn't have any load balancing rules, NAT rules, or inbound NAT pools configured, your backend resources remain isolated to your internal network for inbound traffic--see [outbound-only load balancer configuration](./egress-only.md). With this option, the external Load Balancer can be configured before migrating from basic to standard SKU and migrated at the same time as the internal load balancer using [using the `-MultiLBConfig` parameter](#example-migrate-multiple-related-load-balancers)

- **Public IP Addresses**: Lastly, Public IP addresses can be added directly to your [Virtual Machines](../virtual-network/ip-services/associate-public-ip-address-vm.md) or [Virtual Machine Scale Set instances](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine). However, this option isn't recommended due to the extra security surface area and expense of adding Public IP Addresses.

### What happens if my upgrade fails mid-migration?

The module is designed to accommodate failures, either due to unhandled errors or unexpected script termination. The failure design is a 'fail forward' approach, where instead of attempting to move back to the Basic Load Balancer, you should correct the issue causing the failure (see the error output or log file), and retry the migration again, specifying the `-FailedMigrationRetryFilePathLB <BasicLoadBalancerBackupFilePath> -FailedMigrationRetryFilePathVMSS <VMSSBackupFile>` parameters. For public load balancers, because the Public IP Address SKU is updated to Standard, moving the same IP back to a Basic Load Balancer isn't possible.

Watch a video of the recovery process:

> [!VIDEO 8e203b99-41ff-4454-9cbd-58856708f1c6]

If your failed migration was targeting multiple load balancers at the same time, using the `-MultiLBConfig` parameter, recover each Load Balancer individually using the following process:

1. Address the cause of the migration failure. Check the log file `Start-AzBasicLoadBalancerUpgrade.log` for details

1. [Remove the new Standard Load Balancer](./update-load-balancer-with-vm-scale-set.md) (if created). Depending on which stage of the migration failed, you can have to remove the Standard Load Balancer reference from the Virtual Machine Scale Set, Virtual Machine network interfaces (IP configurations), and/or Health Probes to remove the Standard Load Balancer.

1. Locate the Basic Load Balancer state backup file. This file is in the directory where the script was executed, or at the path specified with the `-RecoveryBackupPath` parameter during the failed execution. The file is named: `State_<basicLBName>_<basicLBRGName>_<timestamp>.json`

1. Rerun the migration script, specifying the `-FailedMigrationRetryFilePathLB <BasicLoadBalancerbackupFilePath>` and `-FailedMigrationRetryFilePathVMSS <VMSSBackupFile>` (for Virtual Machine Scale set backends) parameters instead of -BasicLoadBalancerName or passing the Basic Load Balancer over the pipeline

## Next steps

- [If skipped, migrate from using NAT Pools to NAT Rules for Virtual Machine Scale Sets](load-balancer-nat-pool-migration.md)

- [Learn about Azure Load Balancer](load-balancer-overview.md)


# Load Balancer Standard Virtual Machine Scale Sets

# Guidance for Virtual Machine Scale Sets with Azure Load Balancer

When you work with Virtual Machine Scale Sets and Azure Load Balancer, consider the following guidelines.

## Port forwarding and inbound NAT rules

After the scale set has been created, the backend port can't be modified for a load-balancing rule used by a health probe of the load balancer. To change the port, remove the health probe by updating the virtual machine scale set and updating the port. Then configure the health probe again.

When you use the Virtual Machine Scale Set in the backend pool of the load balancer, the default inbound NAT rules are created automatically.

## Load-balancing rules

When you use the Virtual Machine Scale Set in the backend pool of the load balancer, the default load-balancing rule is created automatically.

## Virtual Machine Scale Set instance-level IPs

When Virtual Machine Scale Sets with [public IPs per instance](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking) are created with a load balancer in front,  the SKU of the Load Balancer (that is, Basic or Standard) determines the SKU of the instance IPs.

## Outbound rules

To create an outbound rule for a backend pool that's already referenced by a load-balancing rule, select **No** under **Create implicit outbound rules** in the Azure portal when the inbound load-balancing rule is created.

Use the following methods to deploy a Virtual Machine Scale Sets with an existing instance of Load Balancer:

* [Configure a Virtual Machine Scale Sets with an existing instance of Azure Load Balancer using the Azure portal](./configure-vm-scale-set-portal.md)

* [Configure a Virtual Machine Scale Sets with an existing instance of Azure Load Balancer using Azure PowerShell](./configure-vm-scale-set-powershell.md)

* [Configure a Virtual Machine Scale Sets with an existing instance of Azure Load Balancer using the Azure CLI](./configure-vm-scale-set-cli.md)


# Network Load Balancing Aws To Azure How To

# Migrate from AWS Network Load Balancer to Azure Load Balancer

If you're currently using AWS Network Load Balancer (NLB) and planning to migrate your workload to Azure, this guide helps you understand the migration process, feature mappings, and best practices. On Azure, [Azure Load Balancer](load-balancer-overview.md) provides low-latency Layer 4 load balancing capabilities that enable you to manage TCP and UDP traffic to your applications. You learn how to assess your current environment, plan and prepare the migration, and execute the transition while maintaining application availability and performance.

## What you accomplish

By following this guide, you'll:

- Map AWS Network Load Balancer features to Azure Load Balancer capabilities

- Prepare your environments for a successful migration

- Plan and execute a migration with minimal downtime

- Validate that your migrated workload meets performance and reliability requirements

- Understand how to iterate on the architecture for future enhancements

This article uses a gaming platform scenario to demonstrate common patterns like multi-protocol load balancing, zone redundancy, and client IP preservation that apply to many high-performance workloads.

## Example scenario: Gaming platform multi-protocol load balancing migration

In this example, a multi-player gaming platform uses AWS Network Load Balancer (NLB) to handle both TCP and UDP traffic simultaneously from game clients. The workload's architecture includes session management services running on EC2 instances handling player authentication and lobbies over TCP on port 7777, and real-time game data services deployed on EC2 instances processing low-latency gameplay packets over UDP on port 7778. The AWS NLB provides static IP addresses, cross-zone load balancing, and client IP preservation for game analytics and anti-cheat systems. This setup supports the workload's core gaming function of processing real-time multiplayer gaming with low-latency while maintaining reliability across multiple availability zones.

### Architectural overview

This architecture example showcases common network load balancing features in AWS and Azure, including multi-protocol support, static IP addresses, cross-zone distribution, and client IP preservation. The goal is to migrate this architecture from AWS Network Load Balancer to Azure Load Balancer while maintaining equivalent functionality and performance. In our architecture diagram, TCP traffic represents game session management services and UDP traffic represents real-time game data services.

Here's the architecture of the workload in AWS:

The diagram shows an AWS Network Load Balancer receiving gaming traffic through an Internet Gateway. Load balancers route requests based on protocol: TCP traffic on port 7777 is sent to session management services and UDP traffic on port 7778 is sent to real-time game data services. Both services are distributed across three availability zones, labeled 1a, 1b, and 1c. In each zone, session management services run on Amazon EC2 instances and real-time game data services run on Amazon EC2 instances. Each instance is placed in its own subnet and is protected by a security group and a network access control list (NACL). The load balancer uses static IP addresses and has cross-zone load balancing enabled. Client IP preservation is enabled for anti-cheat and analytics systems. Arrows from the services indicate connections to Amazon DynamoDB for player data and Amazon ElastiCache for session state. The diagram includes labels for VPC, subnets, security groups, NACLs, target groups, and shows the flow of traffic from the load balancer to the backend services and databases.

This is the architecture for the same gaming platform workload, migrated to Azure:

The diagram shows an Azure Load Balancer architecture in the East US region, spanning three availability zones. Gaming traffic enters through a static public IP address and is directed to an Azure Load Balancer configured with zone redundancy. The load balancer routes requests based on protocol: TCP traffic on port 7777 is sent to a backend pool containing Azure VMs labeled Session Management Service Instances, while UDP traffic on port 7778 is sent to a backend pool containing Azure VMs labeled Real-time Game Data Service Instances. Each backend pool is associated with a health probe monitoring service endpoints. The architecture includes separate subnets for each service tier, each protected by network security groups. Arrows from both services indicate connections to Azure Cosmos DB for player data and Azure Cache for Redis for session state. The diagram includes labels for virtual network, subnets, network security groups, backend pools, health probes, and shows the flow of traffic from the load balancer to the backend services and databases.

Both architectures provide equivalent capabilities:

- **High availability deployment**: Resources distributed across multiple availability zones for fault tolerance

- **Network isolation**: Virtual network with dedicated subnets for load balancer and application tiers

- **Multi-protocol support**: Simultaneous TCP and UDP traffic handling with protocol-specific backend pools

- **Static IP addresses**: Consistent external endpoint addresses for client connections

- **Cross-zone load balancing**: Hash-based traffic distribution across availability zones (distribution depends on client connection patterns and session persistence settings)

- **Client IP preservation**: Original client IP addresses maintained for analytics and anti-cheat systems

- **Low latency**: Optimized for low-latency scenarios with minimal processing overhead; actual latency depends on network topology, VM performance, datacenter design, and geographic proximity

- **High throughput**: Can support millions of flows for Standard Load Balancer with appropriate VM sizes and configuration; actual capacity depends on SKU, VM network limits, and tuning

- **Advanced health monitoring**: Comprehensive TCP and HTTP/HTTPS health probes (UDP services require TCP or HTTP health checks on alternate ports)

- **Network security controls**: Security groups/rules controlling traffic flow between network tiers

- **Auto-scaling integration**: Integrates with Virtual Machine Scale Sets and autoscale rules to scale backend instances based on traffic demand and resource utilization

- **Comprehensive monitoring**: Detailed metrics, diagnostics, and health monitoring for troubleshooting and optimization

### Production environment considerations

This migration is designed as a cutover migration. With this approach, you build out your Azure infrastructure in parallel with your existing AWS setup. This approach minimizes the complexity of migrating users in batches, and enables rapid rollback if any issues arise. As such, you experience a brief period of downtime during the DNS cutover, but the overall migration process is designed to minimize disruption to your services.

**Estimated downtime:**

- DNS propagation time: 5-15 minutes for 300-second TTL

- Session disruption: Existing sessions can be interrupted during cutover

- Service availability: During cutover, services are unavailable with DNS name resolution. The individual services are still available via IP address as long as the services aren't migrated at the same time.

**Recommended maintenance window:**

- Duration: 1-2 hours during low-traffic period

- Buffer time: Extra 30 minutes for unforeseen issues

- Rollback time: 15-30 minutes if needed

> [!NOTE]

> Resetting your DNS TTL values to 300 seconds (5 minutes) before the cutover helps reduce DNS caching delays for many resolvers; reducing the TTL to 60 seconds (1 minute) can further speed propagation for resolvers that respect short TTLs. Propagation depends on upstream and recursive resolvers and can't be guaranteed for all clients—prepare monitoring and rollback plans accordingly.

## Step 1: Assessment

Before migrating from AWS Network Load Balancer to Azure Load Balancer, it's crucial to assess the existing architecture and identify the capabilities that need to be mapped or replaced. This assessment helps ensure a smooth migration process and maintain the functionality of your gaming platform.

To plan to migrate your AWS workload to Azure, see [Migrate networking from Amazon Web Services to Azure](/azure/migration/migrate-networking-from-aws), which includes [example migration scenarios](/azure/migration/migrate-compute-from-aws#migration-guides) that might align to your use case.

### Direct capability mapping

The platform capabilities map from AWS NLB to Azure Load Balancer as follows:

| AWS NLB Capability | Azure Load Balancer Equivalent | Migration approach |

|---|---|---|

| **[AWS NLB Target Groups](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-target-groups.html)** | **[Load Balancer Backend Pools](backend-pool-management.md)** | Create backend pools for each protocol and service type. Backend pools can contain VMs, Virtual Machine Scale Sets, or IP addresses. Configure separate backend pools for TCP and UDP services to enable protocol-specific routing and health monitoring. |

| **[AWS NLB Protocol Support (TCP/UDP)](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-target-groups.html#target-group-routing-configuration)** | **[Load Balancer TCP/UDP Support](load-balancer-overview.md)** | Configure load balancing rules for both TCP and UDP protocols. Azure Load Balancer supports TCP and UDP protocols; internal load balancers also support "all ports" rules for port-agnostic load balancing. Public load balancers require specific port configurations. Create separate rules for different ports and protocols as needed for your services. Note: Health probes don't support UDP so custom health probes utilizing TCP or HTTP/HTTPS must be used. |

| **[AWS NLB Static IP Addresses](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/network-load-balancers.html#load-balancer-static-ip)** | **[Load Balancer Static Public IP](../virtual-network/ip-services/public-ip-addresses.md)** | Deploy Load Balancer with static Standard SKU public IP addresses. Azure provides persistent IP addresses that don't change during load balancer lifecycle. Configure frontend IP configurations with static public IPs to maintain consistent endpoints for clients. |

| **[AWS NLB Cross-zone Load Balancing](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/availability-zones.html#cross-zone-load-balancing)** | **[Load Balancer availability zone support](/azure/reliability/reliability-load-balancer)** | Enable zone redundancy on Load Balancer to automatically distribute traffic across all availability zones. Zone-redundant deployment provides automatic failover and hash-based traffic distribution (distribution evenness depends on traffic entropy and client connection patterns). Configure backend pools with VMs distributed across multiple zones for optimal fault tolerance. |

| **[AWS NLB Health Checks](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/target-group-health-checks.html)** | **[Load Balancer Health Probes](load-balancer-custom-probe-overview.md)** | Configure health probes for TCP services and alternate health check approaches for UDP services. Set probe interval, timeout, unhealthy threshold, and protocol to match AWS NLB configuration. Azure supports TCP, HTTP, and HTTPS health probes with configurable intervals and failure thresholds. For UDP services, use TCP or HTTP health probes on alternate ports since Azure Load Balancer doesn't support native UDP health probing. AWS NLB provides TCP, HTTP, and HTTPS options with slightly different timeout behaviors. |

| **[AWS NLB Flow Hash Algorithm](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html#load-balancer-algorithm)** | **[Load Balancer Distribution Mode](load-balancer-distribution-mode.md)** | Configure distribution mode to control traffic distribution. Azure Load Balancer uses 5-tuple hash (source IP, source port, destination IP, destination port, protocol) by default, while AWS NLB includes TCP sequence number in its flow hash. For applications requiring session affinity, configure Source IP affinity or Source IP and protocol distribution modes to ensure consistent routing. |

| **[AWS NLB Target Registration and Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-load-balancer.html)** | **[Azure Virtual Machine Scale Sets Auto Registration](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-portal)** | AWS Auto Scaling Groups automatically register/deregister EC2 instances with NLB target groups. Azure Virtual Machine Scale Sets provide equivalent functionality by automatically adding/removing VM instances to Load Balancer backend pools. Configure scale sets with automatic registration to backend pools during deployment. For individual VMs, use Azure Resource Manager templates or Azure CLI to programmatically add new VMs to backend pools by IP address or NIC configuration. |

| **[AWS NLB Scheme Configuration (Internet-facing/Internal)](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/network-load-balancers.html)** | **[Azure Load Balancer Public/Internal Configuration](load-balancer-overview.md)** | AWS NLB supports internet-facing (public) and internal schemes in a single load balancer configuration. Azure Load Balancer separates these as distinct resource types: create a Public Load Balancer for internet traffic with public IP frontend, or create an Internal (Private) Load Balancer for VNet-internal traffic with private IP frontend. You can't convert between types after creation - deploy separate load balancers for public and private traffic scenarios. Both types support identical backend pool and health probe configurations. |

| **[AWS NLB TLS Listener Support](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-listeners.html)** | **[Azure Application Gateway for TLS Termination](../application-gateway/ssl-overview.md)** | AWS NLB provides native TLS/SSL termination at Layer 4 with certificate management and TLS listeners (ports 443, custom TLS ports). Azure Load Balancer operates at Layer 4 and does NOT support TLS termination - it only supports TCP, UDP, and TCP_UDP protocols. For TLS termination in Azure, use Azure Application Gateway (Layer 7) which provides SSL/TLS offloading, certificate management, and end-to-end encryption. For Layer 4 TLS passthrough, configure Azure Load Balancer TCP listeners on port 443 and handle TLS termination on backend servers. |

| **[AWS NLB Idle Timeout Configuration](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/network-load-balancers.html#connection-idle-timeout)** | **[Azure Load Balancer TCP Idle Timeout](load-balancer-tcp-idle-timeout.md)** | AWS NLB supports a configurable idle timeout for TCP flows (60–6000 seconds; default 350 seconds). Public AWS documentation doesn't state that NLB injects TCP keepalive packets every 20 seconds for TLS listeners—for reliable session keepalives, use application-level keepalives or adjust the idle timeout. Azure Load Balancer provides a configurable TCP idle timeout (4–100 minutes; default 4 minutes) and TCP reset capabilities. Azure doesn't automatically generate keepalive packets; applications must implement their own keepalive mechanisms. Configure idle timeout settings to match application connection patterns and enable TCP reset to ensure clean connection termination when timeout is reached. |

| **[AWS NLB CloudWatch Metrics](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-cloudwatch-metrics.html)** | **[Load Balancer Azure Monitor Integration](load-balancer-standard-diagnostics.md)** | Configure diagnostic settings to send Load Balancer metrics to Azure Monitor. Enable detailed metrics for connections, throughput, and health probe status. Azure Monitor provides multi-dimensional metrics similar to CloudWatch, including *Byte Count*, *Packet Count*, and *SYN Count* metrics. Integrate with Azure Monitor workbooks for custom dashboards and alerting. |

### Capability mismatches and strategies

If your workload uses NLB capabilities that can't be directly addressed in Azure Load Balancer, consider the following strategies to still arrive at a comparable outcome.

- **Direct functional replacement using other Azure service**: Replace AWS NLB capabilities with Azure Load Balancer equivalents while maintaining core functionality. This approach prioritizes minimal disruption and uses native Azure integrations for security, monitoring, and performance optimization.

- **Architecture enhancement approach**: Use migration as an opportunity to modernize beyond AWS NLB capabilities by incorporating Azure Application Gateway for HTTP(S) APIs, Azure Traffic Manager for global distribution, and [Azure Front Door](../frontdoor/front-door-overview.md) for CDN and DDoS protection.

In the end, you need to decide whether an AWS NLB feature is necessary if there's no direct Azure Load Balancer equivalent and adjust your workload accordingly.

#### Proxy Protocol Support

**AWS NLB capability**: AWS NLB provides Proxy Protocol v2 support where:

- Client IP information is preserved and passed to backend targets via protocol headers

- Enables client IP visibility even when direct client IP preservation isn't available

- Useful for load balancer chaining scenarios and specific networking configurations

**Azure Load Balancer approach**: Azure Load Balancer doesn't have direct proxy protocol support, but provides equivalent functionality through:

- **Application-level solutions**: Implement custom headers or application logic to track client information when needed

- **Azure Application Gateway integration**: For HTTP-based APIs, use Application Gateway, which provides X-Forwarded-For headers

The preceding Proxy Protocol support illustrates an example of a critical mismatch in capability. There can be other features that don't have 1:1 equivalents in Azure Load Balancer. Before migrating, evaluate the features you currently use in AWS NLB and determine if they have direct equivalents or if alternative strategies are needed.

> [!NOTE]

> Evaluate all differences during your assessment phase and determine if your workload can accommodate these changes or if compensating architecture modifications are needed.

>

> Measuring performance and reliability is crucial to ensure that the migrated workload meets your application's latency requirements. This includes monitoring response times, connection establishment latency, jitter, and packet loss rates to validate that the Azure Load Balancer configuration performs optimally for your real-time scenarios. Standard Load Balancer provides an availability SLA, but workload-specific performance targets still require thorough testing.

>

> To ensure your migrated workload meets the performance and reliability criteria expected, establish baseline metrics from the AWS NLB before migration. This will allow you to compare the performance of the Azure Load Balancer after migration and ensure that it meets or exceeds the established benchmarks. Include all relevant metrics such as latency percentiles, concurrent connections, and packet loss rates in your baseline measurements.

## Step 2: Preparation

A detailed assessment can reveal opportunities to adjust resources at the source, easing both the migration process and post-migration operations. This step focuses on targeted adjustments to AWS NLB configurations and related services to ensure compatibility and performance on Azure for your workloads.

### Source service configuration

A successful migration requires detailed documentation of the existing AWS NLB configurations and dependent services to ensure a smooth transition to Azure Load Balancer.

#### Protocol-specific load balancing rule documentation

- Document existing AWS NLB listener configurations and target group settings to ensure equivalent Azure Load Balancer rules. Use [AWS CLI commands for load balancers](https://docs.aws.amazon.com/cli/latest/reference/elbv2/describe-load-balancers.html) to gather detailed configuration information for both TCP and UDP protocols.

- Export all routing configurations, health check settings, and client IP preservation configurations using the [AWS NLB target group documentation](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-target-groups.html).

- Document cross-zone load balancing settings and static IP configurations to ensure equivalent Azure zone redundancy and static public IP setup.

#### Health check configuration mapping

Map [AWS NLB health check configurations](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/target-group-health-checks.html) to Azure Load Balancer health probe equivalents using the [Azure Load Balancer health probe configuration guide](load-balancer-custom-probe-overview.md). This ensures TCP service health monitoring continues to function correctly after migration, and that appropriate alternate health check strategies are implemented for UDP services (using TCP or HTTP probes on alternate ports) with appropriate intervals for your workloads.

#### Performance baseline establishment

- Capture current performance metrics including latency percentiles (P50, P95, P99), concurrent connections, throughput, and packet loss rates

- Document current scaling patterns and peak load characteristics

- Record client IP preservation requirements for analytics and security systems

### Dependency changes

Prepare for migration by updating dependent services and configurations to ensure compatibility with Azure Load Balancer.

#### Application changes

- Configure health monitoring for your services over TCP/HTTP/HTTPS using [Azure Load Balancer health probes](manage-probes-how-to.md).

- Configure logging integration with Azure Monitor using the [Load Balancer metrics](load-balancer-monitor-alert-health-event-logs.md).

#### DNS configuration changes

- Reduce DNS TTL values on your domain records to 300 seconds (or 60 seconds for minimal downtime requirements) for faster cutover.

- If you plan to use Azure DNS, create A records pointing to Azure Load Balancer static public IP addresses using the [Azure DNS configuration guide](../dns/dns-operations-recordsets-cli.md#modify-an-existing-record-set). This change enables rapid DNS propagation during migration cutover with minimal impact on active sessions.

#### Backend pool updates

- Configure backend pool members across multiple availability zones for both TCP and UDP services

- Use [Azure Virtual Machine Scale Sets](load-balancer-standard-virtual-machine-scale-sets.md) for services with automatic scaling based on application metrics

- Implement zone distribution strategies that maintain performance during zone failures

### Environmental changes

Prepare your Azure environment by deploying the necessary infrastructure and configuring security and monitoring components to support the migrated workload. This preparation helps ensure a smooth transition and minimizes potential issues during the migration process.

#### Azure resource provisioning

- Deploy [Azure Load Balancer](load-balancer-overview.md), Virtual Machines, and Virtual Machine Scale Sets using [Infrastructure as Code](../azure-resource-manager/templates/overview.md) before cutover following the Load Balancer deployment guides.

- Configure static public IP addresses and zone redundancy before cutover to ensure platform stability.

- Enable thorough testing and validation in parallel environment before production cutover.

#### Network security setup

- Set up [Network Security Groups (NSGs)](../virtual-network/network-security-groups-overview.md) matching AWS security group rules for your traffic requirements.

- Configure DDoS protection for workloads using [Azure DDoS Protection](../ddos-protection/ddos-protection-overview.md).

- Maintain security posture before, during, and after migration.

#### Monitoring configuration

- Configure [Azure Load Balancer health event logs](load-balancer-health-event-logs.md) as part of your baseline monitoring. Depending on your migration plan, set up additional monitoring as needed.

- Set up dashboards and alerting rules including latency monitoring, concurrent connections, and health probe status using the [Azure Load Balancer standard diagnostics](load-balancer-standard-diagnostics.md).

### Change sequence and dependencies

The following list outlines a logical sequence of changes to implement during migration. This sequence ensures that all dependent services are available before configuration begins, preserving functionality throughout the migration. Think of it as your preflight checklist for migration day.

The general flow of changes is infrastructure deployment, service migration, and then configuration of load balancing rules, health probes, and monitoring. This sequence ensures that all dependent services are available before configuration begins, preserving user experience throughout the migration.

While the specific steps can vary based on your architecture, the general sequence is as follows:

1. **Azure infrastructure deployment** - Deploy Load Balancer with static IPs and VMs first as it's necessary for subsequent configuration steps.

1. **Health probe configuration** - Configure health probes for both protocol types matching AWS health check behavior using the [Load Balancer health probe guide](load-balancer-custom-probe-overview.md).

1. **Protocol-specific rule configuration** - Configure separate load balancing rules for TCP and UDP traffic with appropriate backend pools.

1. **DNS preparation** - Reduce TTL values and prepare DNS record updates for your domains. This step is crucial for ensuring minimal user disconnection when services are cut over.

1. **Application service migration** - Migrate services to Azure VMs and Scale Sets. This can be done in parallel with the Azure infrastructure deployment to save time.

1. **Monitoring setup** - Configure Azure Monitor dashboards and alerting for application-specific metrics including latency, connections, and health status.

In general, the migration process involves deploying and configuring new load balancer infrastructure, followed by migrating application services and then configuring monitoring.

## Step 3: Evaluation

After preparing your environment and making necessary changes, the next step is to evaluate the migration plan and define validation criteria. This step ensures that all capabilities are functioning as expected after the migration is complete.

### Validation criteria

As part of your migration planning, it's essential to define the validation criterion that measures the success of the migration. These criteria will help ensure that all capabilities function as expected after the migration is complete.

#### Success criteria definition

Establish validation criteria based on the original AWS NLB capabilities identified in the assessment section:

##### Functional criteria

- **Multi-protocol routing accuracy**: TCP and UDP traffic routes to correct backend pools based on protocol and port

- **Service health**: All services report healthy status across zones

- **Multi-zone distribution**: Traffic distributes correctly with automatic failover between availability zones

- **Connection handling**: Sessions maintain connectivity during infrastructure changes and scaling events

##### Performance criteria

- **Latency baseline**: Response time within 5% of AWS NLB baseline

- **Throughput capacity**: Handle equivalent concurrent connections and requests per second as AWS NLB

- **Connection establishment**: New session establishment latency meets requirements

- **Jitter minimization**: Consistent packet delivery timing for smooth experience

##### Reliability criteria

- **Session continuity**: Sessions maintain connectivity during zone failures and scaling events

- **High availability**: Desired uptime SLA is met, and automatic failover occurs within seconds

- **Platform-specific SLA**: Meet platform-specific requirements for user experience

- **Security functionality**: Client IP tracking functions correctly for fraud detection systems

### Workload validation methods

Define methods for validating the success criteria established for your workloads. This includes both automated and manual testing approaches to ensure comprehensive coverage of all capabilities.

#### Automated testing

- Create comprehensive automated tests covering all capabilities including:

- Multi-protocol load balancing validation for TCP and UDP traffic

- Performance and load testing against baseline metrics using appropriate tools

- Latency and jitter testing for real-time requirements

- Connection failover and scaling scenario testing under load conditions

#### Manual validation checklist

- Test client connections across both TCP and UDP services

- Validate session creation, operation, and termination flows

- Test security system functionality with client IP preservation

- Verify real-time performance under peak load conditions

- Test session persistence during zone failures and scaling events

- Validate analytics and monitoring data collection

## Step 4: Process

With your migration plan in place and preparatory changes completed, you're ready to move forward. Follow these detailed steps to execute the migration smoothly on migration day while minimizing impact on active sessions.

### Migration execution

Migration execution involves a series of steps to ensure a smooth transition from AWS NLB to Azure Load Balancer. The process includes final validation, parallel testing, DNS cutover, post-cutover validation, and AWS resource decommissioning.

#### Final validation and testing

Validate Azure Load Balancer configuration and service health before cutover:

- Test both TCP and UDP endpoints with appropriate clients

- Verify multi-protocol routing for different service types

- Confirm multi-zone backend pool distribution and service failover

- Validate service functionality across multiple zones with realistic scenarios

- Test high availability and zone failover scenarios under load

- Compare performance metrics against AWS NLB baseline including latency and jitter

- Verify Floating IP (DSR) guest OS configuration and network security prechecks (configure loopback interface, enable weak-host where required, and allow Load Balancer probe IP 168.63.129.16 in NSGs/firewalls)

#### DNS cutover execution

Execute DNS cutover from AWS NLB to Azure Load Balancer. Update domain DNS records to point to Azure Load Balancer static public IP addresses and monitor DNS propagation using DNS monitoring tools.

#### Post-cutover validation

During the post-cutover step, you validate the success of the migration by ensuring that all services are functioning correctly and that performance meets real-time requirements.

**Functional validation:**

- Verify all service routing functions correctly for both protocols

- Validate client IP preservation functionality for security systems

- Test session creation, operation, and termination flows

- Validate health probe behavior for TCP services and alternate health check approaches for UDP services

**Performance validation:**

- Monitor response times and latency against AWS NLB baseline

- Verify throughput capacity meets concurrent session requirements

- Test jitter and packet loss rates for real-time quality

#### AWS resource decommissioning

After successful validation, decommission AWS resources:

- Monitor Azure Load Balancer for 24-48 hours with production traffic

- Verify no traffic routing to AWS NLB

- Backup AWS NLB configuration for rollback capability

- Terminate AWS NLB and associated infrastructure resources

- Determine a monitoring window based on your DNS TTLs, traffic patterns, and rollback policy (commonly 24–72 hours, extended as needed for peak‑traffic coverage)

In general, consider the migration successful when all success criteria are met consistently over the monitoring period you defined and no performance degradation is observed compared to the AWS NLB baseline. Extend monitoring to cover peak hours and weekend traffic patterns as needed before final decommissioning.

## Iterative optimization

After migration, focus on optimizing the Azure Load Balancer configuration and validating performance, routing accuracy, and high availability. This iterative optimization process ensures that the migrated workload meets all success criteria established during the assessment step following the [Azure Well-Architected Framework service guide for Azure Load Balancer](/azure/well-architected/service-guides/azure-load-balancer).

### Iterative improvement process

The migration process is iterative and should be adjusted based on performance feedback and testing until success criteria are met:

#### Performance optimization cycle

1. **Baseline measurement**: Compare Azure Load Balancer metrics to AWS NLB baseline including latency, jitter, and connection metrics

1. **Bottleneck identification**: Identify performance gaps in routing, protocol handling, or backend communication

1. **Configuration tuning**: Adjust Load Balancer settings, backend probe intervals, connection limits, and application-specific parameters

1. **Validation testing**: Retest performance with simulated loads and measure improvements

1. **Monitoring adjustment**: Update monitoring thresholds and alerting rules for application-specific KPIs

#### Routing accuracy refinement

1. **Traffic pattern analysis**: Monitor actual request routing patterns versus expected patterns for both TCP and UDP

1. **Protocol rule optimization**: Refine TCP and UDP routing rules to handle edge cases and connection patterns

1. **Error rate analysis**: Identify and fix routing rules causing session errors or disconnections

1. **User experience validation**: Ensure sessions work seamlessly across both service types

#### High availability validation

1. **Traffic distribution verification**: Confirm traffic distributes correctly across availability zones for both protocols

1. **Failover process testing**: Validate automatic failover between zones during peak loads

1. **Recovery capability**: Test rapid recovery from zone failures while maintaining active sessions

1. **Health check accuracy**: Ensure health checks correctly identify service issues without false positives

## Key takeaways

Migrating a workload that uses AWS Network Load Balancer to Azure requires careful planning and systematic execution to obtain equivalent functionality and performance for real-time requirements. The key success factors include:

**Assessment and planning**: Map AWS NLB capabilities to Azure Load Balancer equivalents early in the process. Pay special attention to multi-protocol support, client IP preservation, and low-latency requirements for high-performance platforms.

**Use Azure integrations**: Take advantage of Azure static public IPs for consistent endpoints, Azure Monitor for observability, and Virtual Machine Scale Sets for service autoscaling to satisfy functional and nonfunctional requirements in your workload.

**Test thoroughly before cutover**: Use parallel testing with simulation tools to validate all functionality. Establish baseline metrics from your AWS environment and ensure Azure Load Balancer meets or exceeds performance expectations including latency, jitter, and connection handling.

**Plan for minimal downtime**: Reduce DNS TTL values beforehand and prepare all infrastructure in parallel. The actual cutover involves only DNS changes, minimizing session disruption and user impact.

**Monitor and optimize post-migration**: Use the iterative improvement process to fine-tune performance, routing accuracy, and high availability. Azure Load Balancer provides extensive monitoring capabilities to optimize your configuration over time with real traffic patterns.

**Platform-specific considerations**: Focus on latency-sensitive optimization, multi-protocol traffic handling, client IP preservation for security systems, and zone redundancy for high availability. Azure Load Balancer provides the enterprise-grade reliability and performance required for mission-critical platforms, though actual latency performance depends on datacenter design and network topology.

## Next steps

> [!div class="nextstepaction"]

> [Architecture best practices for Azure Load Balancer](/azure/well-architected/service-guides/azure-load-balancer)


# Tutorial Load Balancer Ip Backend Portal

# Tutorial: Create a public load balancer with an IP-based backend using the Azure portal

In this tutorial, you'll learn how to create a public load balancer with an IP based backend pool.

A traditional deployment of Azure Load Balancer uses the network interface of the virtual machines. With an IP-based backend, the virtual machines are added to the backend by IP address.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a virtual network

> * Create a NAT gateway for outbound connectivity

> * Create an Azure Load Balancer

> * Create an IP based backend pool

> * Create two virtual machines

> * Test the load balancer

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Create a virtual network

In this section, you'll create a virtual network for the load balancer, NAT gateway, and virtual machines.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. On the upper-left side of the screen, select **Create a resource** and search for **Virtual network** in the search box.

1. On the **Marketplace** page, select **Create > Virtual network** under **Virtual network**.

1. In **Create virtual network**, enter or select this information in the **Basics** tab:

| **Setting**          | **Value**                                                           |

|------------------|-----------------------------------------------------------------|

| **Project Details**  |                                                                 |

| Subscription     | Select your Azure subscription                                  |

| Resource Group   | Select **Create new**.<br/>Enter **Name** of **myResourceGroup** and select **Ok**.</br>|

| **Instance details** |                                                                 |

| Name             | Enter **myVNet**                                    |

| Region           | Select **(US) East US** |

1. Select the **IP Addresses** tab or select the **Next: IP Addresses** button at the bottom of the page.

1. In the **IP Addresses** tab, enter this information:

| Setting            | Value                      |

|--------------------|----------------------------|

| IPv4 address space | Enter **10.1.0.0/16** |

1. Select **+ Add subnet** enter this information:

| Setting            | Value                      |

|--------------------|----------------------------|

| Subnet name | Enter **myBackendSubnet** |

| Subnet address range | Enter **10.1.0.0/24** |

1. Select **Add**.

1. Select the **Security** tab.

1. Under **BastionHost**, select **Enable**. Enter this information:

| Setting            | Value                      |

|--------------------|----------------------------|

| Bastion name | Enter **myBastionHost** |

| AzureBastionSubnet address space | Enter **10.1.1.0/26** |

| Public IP Address | Select **Create new**. </br> For **Name**, enter **myBastionIP**. </br> Select **OK**. |

1. Select the **Review + create** tab or select the **Review + create** button.

1. Select **Create**.

> [!IMPORTANT]

>

> [!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

>

## Create NAT gateway

In this section, you'll create a NAT gateway and assign it to the subnet in the virtual network you created previously.

1. On the upper-left side of the screen, Search for **NAT gateway** in the search box.

1. On the **Marketplace** page,select **Create > NAT gateway** under **NAT gateway**.

1. In **Create network address translation (NAT) gateway**, enter or select this information in the **Basics** tab:

| **Setting**          | **Value**                                                           |

|------------------|-----------------------------------------------------------------|

| **Project Details**  |                                                                 |

| Subscription     | Select your Azure subscription.                                  |

| Resource Group   | Select **myResourceGroup** in the text box. |

| **Instance details** |                                                                 |

| Name             | Enter **myNATgateway**                                    |

| Region           | Select **(US) East US**  |

| Availability Zone | Select **None**. |

| Idle timeout (minutes) | Enter **10**. |

1. Select the **Outbound IP** tab, or select the **Next: Outbound IP** button at the bottom of the page.

1. In the **Outbound IP** tab, enter or select the following information:

| **Setting** | **Value** |

| ----------- | --------- |

| Public IP addresses | Select **Create a new public IP address**. </br> In **Name**, enter **myPublicIP-NAT**. </br> Select **OK**. |

1. Select the **Subnet** tab, or select the **Next: Subnet** button at the bottom of the page.

1. In the **Subnet** tab, select **myVNet** in the **Virtual network** pull-down.

1. Check the box next to **myBackendSubnet**.

1. Select the **Review + create** tab, or select the blue **Review + create** button at the bottom of the page.

1. Select **Create**.

## Create load balancer

In this section, you'll create a zone redundant load balancer that load balances virtual machines. With zone-redundancy, one or more availability zones can fail and the data path survives as long as one zone in the region remains healthy.

During the creation of the load balancer, you'll configure:

* Frontend IP address

* Backend pool

* Inbound load-balancing rules

1. In the search box at the top of the portal, enter **Load balancers**. Select **Load balancers** in the search results.

1. In the **Load balancer** page, select **+ Create**.

1. In the **Basics** tab of the **Create load balancer** page, enter, or select the following information:

| Setting                 | Value                                              |

| ---                     | ---                                                |

| **Project details** |   |

| Subscription               | Select your subscription.    |

| Resource group         | Select **myResourceGroup**. |

| **Instance details** |   |

| Name                   | Enter **myLoadBalancer**                                   |

| Region         | Select **(US) East US**.                                        |

| SKU           | Leave the default **Standard**. |

| Type          | Select **Public**.                                        |

| Tier          | Leave the default **Regional**. |

1. Select **Next: Frontend IP configuration** at the bottom of the page.

1. In **Frontend IP configuration**, select **+ Add a frontend IP configuration**.

1. Enter **myLoadBalancerFrontend** in **Name**.

1. Select **IPv4** or **IPv6** for the **IP version**.

> [!NOTE]

> IPv6 isn't currently supported with Routing Preference or Cross-region load-balancing (Global Tier).

1. Select **IP address** for the **IP type**.

> [!NOTE]

> For more information on IP prefixes, see [Azure Public IP address prefix](../virtual-network/ip-services/public-ip-address-prefix.md).

1. Select **Create new** in **Public IP address**.

1. In **Add a public IP address**, enter **myPublicIP-LB** for **Name**.

1. Select **Zone-redundant** in **Availability zone**.

> [!NOTE]

> In regions with [Availability Zones](/azure/reliability/availability-zones-overview?toc=%2fazure%2fvirtual-network%2ftoc.json), you can select zone-redundant (default option) or a specific zone. The choice depends on your specific domain failure requirements. In regions without Availability Zones, this field won't appear. </br> For more information on availability zones, see [Availability zones overview](/azure/reliability/availability-zones-overview).

1. Leave the default of **Microsoft Network** for **Routing preference**.

1. Select **OK**.

1. Select **Add**.

1. Select **Next: Backend pools** at the bottom of the page.

1. In the **Backend pools** tab, select **+ Add a backend pool**.

1. Enter **myBackendPool** for **Name** in **Add backend pool**.

1. Select **myVNet (myResourceGroup)** in **Virtual network**.

1. Select **IP Address** for **Backend Pool Configuration**.

1. Select **Save**.

1. Select the **Next: Inbound rules** button at the bottom of the page.

1. Under **Load balancing rule** in the **Inbound rules** tab, select **+ Add a load balancing rule**.

1. In **Add load balancing rule**, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| Name | Enter **myHTTPRule** |

| IP Version | Select **IPv4** or **IPv6** depending on your requirements. |

| Frontend IP address | Select **myLoadBalancerFrontend**. |

| Backend pool | Select **myBackendPool**. |

| Protocol | Select **TCP**. |

| Port | Enter **80**. |

| Backend port | Enter **80**. |

| Health probe | Select **Create new**. </br> In **Name**, enter **myHealthProbe**. </br> Select **HTTP** in **Protocol**. </br> Leave the rest of the defaults, and select **OK**. |

| Session persistence | Select **None**. |

| Idle timeout (minutes) | Enter or select **15**. |

| TCP reset | Select **Enabled**. |

| Floating IP | Select **Disabled**. |

| Outbound source network address translation (SNAT) | Leave the default of **(Recommended) Use outbound rules to provide backend pool members access to the internet.** |

25. Select **Add**.

26. Select the blue **Review + create** button at the bottom of the page.

27. Select **Create**.

> [!NOTE]

> In this example we created a NAT gateway to provide outbound Internet access. The outbound rules tab in the configuration is bypassed as it's optional and isn't needed with the NAT gateway. For more information on Azure NAT gateway, see [What is Azure Virtual Network NAT?](../virtual-network/nat-gateway/nat-overview.md)

> For more information about outbound connections in Azure, see [Source Network Address Translation (SNAT) for outbound connections](../load-balancer/load-balancer-outbound-connections.md)

## Create virtual machines

In this section, you'll create two VMs (**myVM1** and **myVM2**) in two different zones (**Zone 1** and **Zone 2**).

These VMs are added to the backend pool of the load balancer that was created earlier.

1. In the search box at the top of the portal, enter **Virtual machines**.

1. Select **+ Create > Azure virtual machine** in the search results.

1. In **Create a virtual machine**, enter or select the values in the **Basics** tab:

| Setting | Value                                          |

|-----------------------|----------------------------------|

| **Project Details** |  |

| Subscription | Select your Azure subscription |

| Resource Group | Select **myResourceGroup** |

| **Instance details** |  |

| Virtual machine name | Enter **myVM1** |

| Region | Select **(US) East US** |

| Availability Options | Select **Availability zones** |

| Availability zone | Select **Zone 1** |

| Image | Select **Windows Server 2022 Datacenter: Azure Edition - x64 Gen2** |

| Azure Spot instance | Leave the default |

| Size | Select **Standard_DS1_v2** or another image size. |

| **Administrator account** |  |

| Username | Enter a username |

| Password | Enter a password |

| Confirm password | Reenter password |

| **Inbound port rules** |  |

| Public inbound ports | Select **None** |

1. Select the **Networking** tab, or select **Next: Disks**, then **Next: Networking**.

1. In the Networking tab, select or enter:

| Setting | Value |

|-|-|

| **Network interface** |  |

| Virtual network | **myVNet** |

| Subnet | **myBackendSubnet** |

| Public IP | Select **None**. |

| NIC network security group | Select **Advanced**|

| Configure network security group | Select **Create new**. </br> In the **Create network security group**, enter **myNSG** in **Name**. </br> Within **Inbound rules**, select **+Add an inbound rule**. </br> Under **Service**, select **HTTP**. </br> In **Priority**, enter **100**. </br> Under **Name**, enter **myNSGRule** </br> Select **Add** </br> Select **OK** |

| **Load balancing**  |

| Place this virtual machine behind an existing load-balancing solution? | Select the check box.|

| **Load balancing settings** |

| Load balancing options | Select **Azure load balancer** |

| Select a load balancer | Select **myLoadBalancer**  |

| Select a backend pool | Select **myBackendPool** |

1. Select **Review + create**.

1. Review the settings, and then select **Create**.

1. Follow the steps 1 to 7 to create a VM with the following values and all the other settings the same as **myVM1**:

| Setting | Values for myVM2 |

| ------- | ----- |

| Name |  **myVM2** |

| Availability zone | **Zone 2** |

| Networking > Configure network security group | Select the existing **myNSG**|

## Install IIS

1. Select **All services** in the left-hand menu, select **All resources**, and then from the resources list, select **myVM1** that is located in the **myResourceGroup** resource group.

2. On the **Overview** page, select **Connect**, then **Bastion**.

3. Select the **Use Bastion** button.

4. Enter the username and password entered during VM creation.

5. Select **Connect**.

6. On the server desktop, navigate to **Windows Administrative Tools** > **Windows PowerShell**.

7. In the PowerShell Window, run the following commands to:

* Install the IIS server

* Remove the default iisstart.htm file

* Add a new iisstart.htm file that displays the name of the VM:

```powershell

# Install IIS server role

Install-WindowsFeature -name Web-Server -IncludeManagementTools

# Remove default htm file

Remove-Item C:\inetpub\wwwroot\iisstart.htm

# Add a new htm file that displays server name

Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)

```

8. Close the Bastion session with **myVM1**.

9. Repeat steps 1 to 7 to install IIS and the updated iisstart.htm file on **myVM2**.

## Test the load balancer

1. Find the public IP address for the load balancer on the **Overview** screen. Select **All services** in the left-hand menu, select **All resources**, and then select **myPublicIP-LB**.

2. Copy the public IP address, and then paste it into the address bar of your browser. The default page of IIS Web server is displayed on the browser.

![IIS Web server](./media/tutorial-load-balancer-standard-zonal-portal/load-balancer-test.png)

To see the load balancer distribute traffic to myVM2, force-refresh your web browser from the client machine.

## Clean up resources

If you're not going to continue to use this application, delete

the virtual network, virtual machine, and NAT gateway with the following steps:

1. From the left-hand menu, select **Resource groups**.

2. Select the **myResourceGroup** resource group.

3. Select **Delete resource group**.

4. Enter **myResourceGroup** and select **Delete**.

## Next steps

In this tutorial, you:

* Created a virtual network

* Created a NAT gateway

* Created a load balancer with an IP-based backend pool

* Tested the load balancer

Advance to the next article to learn how to create a cross-region load balancer:

> [!div class="nextstepaction"]

> [Create a cross-region Azure Load Balancer using the Azure portal](tutorial-cross-region-portal.md)


# Tutorial Load Balancer Standard Public Zonal Portal

# Tutorial: Load balance VMs within an availability zone by using the Azure portal

This tutorial creates a public [load balancer](https://aka.ms/azureloadbalancerstandard) with a zonal IP. In the tutorial, you specify a zone for your frontend and backend instances.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a virtual network with an Azure Bastion host for management.

> * Create a NAT gateway for outbound internet access of the resources in the virtual network.

> * Create a load balancer with a health probe and traffic rules.

> * Create zonal virtual machines (VMs) and attach them to a load balancer.

> * Create a basic Internet Information Services (IIS) site.

> * Test the load balancer.

For more information about availability zones and a standard load balancer, see [Standard load balancer and availability zones](load-balancer-standard-availability-zones.md).

## Prerequisites

* An Azure subscription

## Sign in to Azure

Sign in to the [Azure portal](https://portal.azure.com).

[!INCLUDE [load-balancer-create-bastion](../../includes/load-balancer-create-bastion.md)]

[!INCLUDE [load-balancer-nat-gateway-subnet-add](../../includes/load-balancer-nat-gateway-subnet-add.md)]

[!INCLUDE [load-balancer-public-create](../../includes/load-balancer-public-create.md)]

[!INCLUDE [load-balancer-create-virtual-machine-zonal](../../includes/load-balancer-create-virtual-machine-zonal.md)]

[!INCLUDE [ephemeral-ip-note.md](~/reusable-content/ce-skilling/azure/includes/ephemeral-ip-note.md)]

[!INCLUDE [load-balancer-install-iis](../../includes/load-balancer-install-iis.md)]

[!INCLUDE [load-balancer-cleanup-resources](../../includes/load-balancer-cleanup-resources.md)]

## Next steps

Advance to the next article to learn how to load balance VMs across availability zones:

> [!div class="nextstepaction"]

> [Load balance VMs across availability zones](./quickstart-load-balancer-standard-public-portal.md)


# Tutorial Multi Availability Sets Portal

# Tutorial: Create a load balancer with more than one availability set in the backend pool using the Azure portal

As part of a high availability deployment, virtual machines are often grouped into multiple availability sets.

Load Balancer supports more than one availability set with virtual machines in the backend pool.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a NAT gateway for outbound connectivity

> * Create a virtual network and a network security group

> * Create a standard SKU Azure Load Balancer

> * Create four virtual machines and two availability sets

> * Add virtual machines in availability sets to backend pool of load balancer

> * Test the load balancer

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

[!INCLUDE [load-balancer-nat-gateway](../../includes/load-balancer-nat-gateway.md)]

[!INCLUDE [load-balancer-create-no-bastion](../../includes/load-balancer-create-no-bastion.md)]

[!INCLUDE [load-balancer-nsg-http-rule](../../includes/load-balancer-nsg-http-rule.md)]

[!INCLUDE [load-balancer-public-create](../../includes/load-balancer-public-create.md)]

## Create virtual machines

In this section, you create two availability groups with two virtual machines per group. These machines are added to the backend pool of the load balancer during creation.

### Create first set of VMs

1. Select **+ Create a resource** in the upper left-hand section of the portal.

1. In **New**, select **Compute** > **Virtual machine**.

1. In the **Basics** tab of **Create a virtual machine**, enter, or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription |

| Resource group | Select **lb-resource-group**. |

| **Instance details** |   |

| Virtual machine name | Enter **lb-VM1**. |

| Region | Select **(US) East US**. |

| Availability options | Select **Availability set**. |

| Availability set | Select **Create new**. </br> Enter **lb-availability-set1** in **Name**. </br> Select **OK**. |

| Security type | Select **Trusted launch virtual machines**. |

| Image | Select **Windows Server 2022 Datacenter - x64 Gen2**. |

| Azure Spot instance | Leave the default of unchecked. |

| Size | Select a size for the virtual machine. |

| **Administrator account** |   |

| Username | Enter a username. |

| Password | Enter a password. |

1. Select the **Networking** tab, or select the **Next: Disks**, then **Next: Networking** button at the bottom of the page.

1. In the **Networking** tab, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Network interface** |   |

| Virtual network | Select **lb-VNet**. |

| Subnet | Select **backend-subnet**. |

| Public IP | Select **None**. |

| NIC network security group | Select **Advanced**. |

| Configure network security group | Skip this setting until the rest of the settings are completed. Complete after **Select a backend pool**.|

| **Load balancing** |   |

| Load-balancing options | Select **Azure load balancer**. |

| Select a load balancer | Select **load-balancer**. |

| Select a backend pool | Select **lb-backend-pool**. |

| Configure network security group | Select **Create new**. </br> In the **Create network security group**, enter **lb-NSG** in **Name**. </br> Under **Inbound rules**, select **+Add an inbound rule**. </br> Under  **Service**, select **HTTP**. </br> Under **Priority**, enter **100**. </br> In **Name**, enter **lb-NSG-rule** </br> Select **Add** </br> Select **OK** |

1. Select the **Review + create** tab, or select the blue **Review + create** button at the bottom of the page.

1. Select **Create**.

1. Repeat steps 1 through 7 to create the second virtual machine of the set. Replace the settings for the VM with the following information:

| Setting | Value |

| ------- | ----- |

| Name | Enter **lb-VM2**. |

| Availability set | Select **lb-availability-set1**. |

| Virtual Network | Select **lb-VNet**. |

| Subnet | Select **backend-subnet**. |

| Public IP | Select **None**. |

| NIC network security group | Select **Advanced**. |

| Configure network security group | Skip this setting until the rest of the settings are completed. Complete after **Select a backend pool**.|

| Load-balancing options | Select **Azure load balancer**. |

| Select a load balancer | Select **load-balancer**. |

| Select a backend pool | Select **lb-backend-pool**. |

| Configure network security group | Select **lb-NSG**. |

### Create second set of VMs

1. Select **+ Create a resource** in the upper left-hand section of the portal.

1. In **New**, select **Compute** > **Virtual machine**.

1. In the **Basics** tab of **Create a virtual machine**, enter, or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription |

| Resource group | Select **lb-resource-group**. |

| **Instance details** |   |

| Virtual machine name | Enter **lb-VM3**. |

| Region | Select **(US) East US**. |

| Availability options | Select **Availability set**. |

| Availability set | Select **Create new**. </br> Enter **lb-availability-set2** in **Name**. </br> Select **OK**. |

| Security type | Select **Trusted launch virtual machines**. |

| Image | Select **Windows Server 2022 Datacenter - x64 Gen2**. |

| Azure Spot instance | Leave the default of unchecked. |

| Size | Select a size for the virtual machine. |

| **Administrator account** |   |

| Username | Enter a username. |

| Password | Enter a password. |

1. Select the **Networking** tab, or select the **Next: Disks**, then **Next: Networking** button at the bottom of the page.

1. In the **Networking** tab, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Network interface** |   |

| Virtual network | Select **lb-VNet**. |

| Subnet | Select **backend-subnet**. |

| Public IP | Select **None**. |

| NIC network security group | Select **Advanced**. |

| Configure network security group | Skip this setting until the rest of the settings are completed. Complete after **Select a backend pool**.|

| **Load balancing** |   |

| Load-balancing options | Select **Azure load balancer**. |

| Select a load balancer | Select **load-balancer**. |

| Select a backend pool | Select **lb-backend-pool**. |

| Configure network security group | Select **lb-NSG**. |

6. Select the **Review + create** tab, or select the blue **Review + create** button at the bottom of the page.

7. Select **Create**.

8. Repeat steps 1 through 7 to create the second virtual machine of the set. Replace the settings for the VM with the following information:

| Setting | Value |

| ------- | ----- |

| Name | Enter **lb-VM4**. |

| Availability set | Select **lb-availability-set2**. |

| Virtual Network | Select **lb-VM3**. |

| NIC network security group | Select **Advanced**. |

| Configure network security group | Skip this setting until the rest of the settings are completed. Complete after **Select a backend pool**.|

| Load-balancing options | Select **Azure load balancer**. |

| Select a load balancer | Select **load-balancer**. |

| Select a backend pool | Select **lb-backend-pool**. |

| Configure network security group | Select **lb-NSG**. |

## Install IIS

In this section, you use the Azure Bastion host you created previously to connect to the virtual machines and install IIS.

1. In the search box at the top of the portal, enter **Virtual machine**.

1. Select **Virtual machines** in the search results.

1. Select **lb-VM1**.

1. Under **Payload** in the left-side menu, select **Run command > RunPowerShellScript**.

1. In the PowerShell Script window, add the following commands to:

* Install the IIS server

* Remove the default iisstart.htm file

* Add a new iisstart.htm file that displays the name of the VM:

```powershell

# Install IIS server role

Install-WindowsFeature -name Web-Server -IncludeManagementTools

# Remove default htm file

Remove-Item  C:\inetpub\wwwroot\iisstart.htm

# Add a new htm file that displays server name

Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)

```

1. Select **Run** and wait for the command to complete.

1. Repeat steps 1 through 8 for **lb-VM2**, **lb-VM3**, and **lb-VM4**.

## Test the load balancer

In this section, you discover the public IP address of the load balancer. You use the IP address to test the operation of the load balancer.

1. In the search box at the top of the portal, enter **Public IP**.

1. Select **Public IP addresses** in the search results.

1. Select **lb-Public-IP**.

1. Note the public IP address listed in **IP address** in the **Overview** page of **lb-Public-IP**:

1. Open a web browser and enter the public IP address in the address bar:

1. Select refresh in the browser to see the traffic balanced to the other virtual machines in the backend pool.

## Clean up resources

If you're not going to continue to use this application, delete

the load balancer and the supporting resources with the following steps:

1. In the search box at the top of the portal, enter **Resource group**.

1. Select **Resource groups** in the search results.

1. Select **lb-resource-group**.

1. In the overview page of **lb-resource-group**, select **Delete resource group**.

1. Select **Apply force delete for selected Virtual Machines and Virtual machine scale sets**.

1. Enter **lb-resource-group** in **Enter resource group name to confirm deletion**.

1. Select **Delete**.

## Next steps

In this tutorial, you:

* Created a virtual network and a network security group.

* Created an Azure Standard Load Balancer.

* Created two availability sets with two virtual machines per set.

* Installed IIS and tested the load balancer.

Advance to the next article to learn how to create a cross-region Azure Load Balancer:

> [!div class="nextstepaction"]

> [Create a cross-region load balancer](tutorial-cross-region-portal.md)


# Configure Inbound Nat Rules Vm Scale Set

# Configure inbound NAT Rules for Virtual Machine Scale Sets

In this article, you'll learn how to configure, update, and delete inbound NAT Rules for Virtual Machine Scale Set instances. Azure offers two options for inbound NAT rules. The first option is the ability to add a single inbound NAT rule to a single backend resource. The second option is the ability to create a group of inbound NAT rules for a backend pool. It's recommended to use the second option for inbound NAT rules when using Virtual Machine Scale Sets, since this option provides better flexibility and scalability. Learn more about the various options for [inbound NAT rules](inbound-nat-rules.md).

## Prerequisites

- A Standard SKU [Azure Load Balancer](quickstart-load-balancer-standard-public-portal.md) in the same subscription as the Virtual Machine Scale Set.

- A [Virtual Machine Scale Set instance](configure-vm-scale-set-portal.md) in the backend pool of the load balancer.

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Add inbound NAT rules

Individual inbound NAT rules can't be added to a Virtual Machine Scale Set. However, you can add a set of inbound NAT rules with a defined frontend port range and backend port for all instances in the Virtual Machine Scale Set.

To add a set of inbound NAT rules for the Virtual Machine Scale Sets, you create a set of inbound NAT rules in the load balancer that targets a backend pool using [az network lb inbound-nat-rule create](/cli/azure/network/lb/inbound-nat-rule#az-network-lb-inbound-nat-rule-create) as follows:

```azurecli

az network lb inbound-nat-rule create \

--resource-group MyResourceGroup \

--name MyNatRule \

--lb-name MyLb \

--protocol TCP \

--frontend-port-range-start 200 \

--frontend-port-range-end 250 \

--backend-port 22 \

--backend-pool-name mybackend \

--frontend-ip-name MyFrontendIp

```

The new inbound NAT rule can't have an overlapping frontend port range with existing inbound NAT rules. To view existing inbound NAT rules that are set up, use [az network lb inbound-nat-rule show](/cli/azure/network/lb/inbound-nat-rule#az-network-lb-inbound-nat-rule-show) as follows:

```azurecli

az network lb inbound-nat-rule show \

--lb-name <load-balancer-name> \

--name <nat-rule-name> \

--resource-group <resource-group-name>

```

## Add multiple inbound NAT rules behind a Virtual Machine Scale Set

Multiple sets of inbound NAT rules can be attached to a single Virtual Machine Scale Set, given that the rules frontend port ranges aren’t overlapping. This is accomplished by having multiple sets of inbound NAT rules that target the same backend pool as follows:

```azurecli

az network lb inbound-nat-rule create \

--resource-group MyResourceGroup \

--name MyNatRule \

--lb-name MyLb \

--protocol TCP \

--frontend-port-range-start 200 \

--frontend-port-range-end 250 \

--backend-port 22 \

--backend-pool-name mybackend \

--frontend-ip-name MyFrontendIp

az network lb inbound-nat-rule create \

--resource-group MyResourceGroup \

--name MyNatRule2 \

--lb-name MyLb \

--protocol TCP \

--frontend-port-range-start 150 \

--frontend-port-range-end 180 \

--backend-port 80 \

--backend-pool-name mybackend \

--frontend-ip-name MyFrontendIp

```

## Update inbound NAT rules

When using inbound NAT rules with Virtual Machine Scale Sets, Individual inbound NAT rules can't be updated. However, you can update a set of inbound NAT rules that target a backend pool using [az network lb inbound-nat-rule update](/cli/azure/network/lb/inbound-nat-rule#az-network-lb-inbound-nat-rule-update) as follows:

```azurecli

az network lb inbound-nat-rule update \

--resource-group MyResourceGroup \

--name MyNatRule \

--lb-name MyLb \

--frontend-port-range-start 150 \

--frontend-port-range-end 250

```

## Delete inbound NAT rules

When using inbound NAT rules with Virtual Machine Scale Sets, individual inbound NAT rules can't be deleted. However, you can delete the entire set of inbound NAT rules by deleting the inbound NAT rule that targets a specific backend pool. Use [az network lb inbound-nat-rule delete](/cli/azure/network/lb/inbound-nat-rule#az-network-lb-inbound-nat-rule-delete) to delete a set of rules:

```azurecli

az network lb inbound-nat-rule delete --resourcegroup MyResourceGroup --name MyNatRule --lb-name MyLb

```

## Next steps

To learn more about Azure Load Balancer and Virtual Machine Scale Sets, read more about the concepts.

Learn to use [Azure Load Balancer with Virtual Machine Scale Sets](load-balancer-standard-virtual-machine-scale-sets.md).


# Load Balancer Multiple Virtual Machine Scale Set

# Add multiple Virtual Machine Scale Set instances behind one Azure Load Balancer

In this article, you’ll learn how to configure multiple Virtual Machine Scale Set instances behind a single Azure Load Balancer.

## Prerequisites

# [Azure portal](#tab/azureportal)

- Access to the Azure portal

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)

- Two or more [Virtual Machine Scale Sets](/azure/virtual-machine-scale-sets/quick-create-portal)

- Ensure the upgrade policy is set to automatic.

- If manual upgrade policy is used, upgrade all virtual machine instances after attaching it to the load balancer.

- An existing [standard SKU load balancer](quickstart-load-balancer-standard-internal-portal.md) in the same subscription and virtual network as the Virtual Machine Scale Sets.

- The load balancer must also have a backend pool with health probes and load balancing rules attached.

# [Azure CLI](#tab/azurecli/)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)

- Two or more [Virtual Machine Scale Sets](/azure/virtual-machine-scale-sets/quick-create-portal)

- Ensure that the upgrade policy is set to automatic.

- If manual upgrade policy is used, upgrade all virtual machine instances after attaching it to the load balancer.

- An existing [standard SKU load balancer](quickstart-load-balancer-standard-internal-portal.md) in the same subscription and virtual network as the Virtual Machine Scale Sets.

- The load balancer must also have a backend pool with health probes and load balancing rules attached.

- Access to the Azure portal CLI

> [!NOTE]

> If you choose to use Azure CLI, you have can run AZ CLI in Azure Cloud Shell or as a local install. Review the following to ensure you are ready to use Azure CLI in the environment you choose.

- Use the Bash environment in [Azure Cloud Shell](../cloud-shell/quickstart.md)

- If you prefer to run CLI reference commands locally, [install](/cli/azure/install-azure-cli) the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see [How to run the Azure CLI in a Docker container](/cli/azure/run-azure-cli-docker).

- If you're using a local installation, sign in to the Azure CLI by using the [az sign-in](/cli/azure/reference-index#az-login) command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see [Sign in with the Azure CLI](/cli/azure/authenticate-azure-cli).

- When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see [Use extensions with the Azure CLI](/cli/azure/azure-cli-extensions-overview).

- Run [az version](/cli/azure/reference-index?#az-version) to find the version and dependent libraries that are installed. To upgrade to the latest version, run [az upgrade](/cli/azure/reference-index?#az-upgrade).

---

## Add Virtual Machine Scale Set to an Azure Load Balancer’s backend pool

In this section, you’ll learn how to attach your Virtual Machine Scale Sets behind a single Azure Load Balancer.

> [!NOTE]

> The following section assumes a virtual network named *myVnet* and an Azure Load Balancer named *myLoadBalancer* has been previously deployed. In addition, the following section assumes the backend pools are NIC based.

# [Azure portal](#tab/azureportal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

1. Select your balancer from the list.

1. In your load balancer's page, select **Backend pools** under **Settings**.

1. Select your backend pool.

1. In your backend pool's page, select **+ Add** under **IP configurations**

1. Select the two Virtual Machine Scale Sets that you want to add to the backend pool.

1. Select **Add** and **Save**.

# [Azure CLI](#tab/azurecli/)

1. Connect to your Azure subscription with Azure CLI.

1. Add the first Virtual Machine Scale Set to a load balancer with [az vmss update](/cli/azure/vmss#az-vmss-update), and replace the values in brackets with the names of the resources in your configuration.

```azurecli

az vmss update\

--resource-group <resource-group> \

--name <vmss-name> \

--add  virtualMachineProfile.networkProfile.networkInterfaceConfigurations[0].ipConfigurations[0].loadBalancerBackendAddressPools "{'id':'/subscriptions/<SubscriptionID>/resourceGroups/<Resource Group> /providers/Microsoft.Network/loadBalancers/<Load Balancer Name>/backendAddressPools/<Backend address pool name >'}"

```

This example deploys a Virtual Machine Scale Set with the following defined values:

- Virtual Machine Scale Set named *myVMSS*

- Azure Load Balancer named *MyLB*

- Load Balancer backend pool named *mybackend*

- Resource group named *myResourceGroup*

- Subscription ID named *SubscriptionID*

```azurecli

az vmss update \

--resource-group myResourceGroup \

--name myVMSS \

--add virtualMachineProfile.networkProfile.networkInterfaceConfigurations[0].ipConfigurations[0].loadBalancerBackendAddressPools "{'id':'/subscriptions/SubscriptionID/resourceGroups/myResourceGroup /providers/Microsoft.Network/loadBalancers/MyLb/backendAddressPools/mybackend'}"

```

3. Repeat the steps to attach your second Virtual Machine Scale Set to the backend pool of the Azure Load Balancer with `az vmss update`.

---

## Next steps

In this article, you attached multiple Virtual Machine Scale Sets behind a single Azure load balancer.

- [What is Azure Load Balancer?](load-balancer-overview.md)

- [What are Azure Virtual Machine Scale Sets?](/azure/virtual-machine-scale-sets/overview)


# Configure Vm Scale Set Portal

# Configure a Virtual Machine Scale Set with an existing Azure Standard Load Balancer

In this article, you'll learn how to configure a Virtual Machine Scale Set with an existing Azure Load Balancer. With an existing virtual network and standard sku load balancer, you can deploy a Virtual Machine Scale Set with a few clicks in the Azure portal, or with a few lines of code in the Azure CLI, or Azure PowerShell using the following tabs.

# [Azure portal](#tab/portal)

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- - An [Azure Virtual Network](../virtual-network/quick-create-portal.md) for the Virtual Machine Scale Set and the load balancer.

- An existing [standard sku load balancer](quickstart-load-balancer-standard-internal-portal.md) in the subscription where the Virtual Machine Scale Set will be deployed. Ensure the load balancer has a backend pool.

## Sign in to the Azure portal

Sign in to the [Azure portal](https://portal.azure.com).

## Deploy Virtual Machine Scale Set with existing load balancer

In this section, you'll create a Virtual Machine Scale Set in the Azure portal with an existing Azure load balancer.

> [!NOTE]

> The following steps assume a virtual network named **myVNet** and an Azure load balancer named **myLoadBalancer** has been previously deployed.

1. On the top left-hand side of the screen, select **Create a resource** and search for **Virtual Machine Scale Set** in the marketplace search.

1. Select **Virtual machine scale set** and Select **Create**.

1. In **Create a virtual machine scale set**, enter, or select this information in the **Basics** tab:

| Setting                        | Value                                                                                                 |

|--------------------------------|-------------------------------------------------------------------------------------------------------|

| **Project details**            |                                                                                                       |

| Subscription                   | Select your Azure subscription                                                                        |

| Resource Group                 | Select  Create new, enter **myResourceGroup**, then select OK, or select an existing  resource group. |

| **Scale set details**          |                                                                                                       |

| Virtual Machine Scale Set name | Enter **myVMSS**                                                                                      |

| Region                         | Select **East US 2**                                                                                  |

| Availability zone              | Select **None**                                                                                       |

| **Orchestration** |                    |

| Orchestration mode | Select **Uniform** |

| Security type | Select **Standard** |

| **Scaling** |  |

| Scaling mode | Select **Manual** |

| Instance count | Enter **2** |

| **Instance details**           |                                                                                                       |

| Image                          | Select **Ubuntu Server 22.04 LTS**                                                                    |

| Azure Spot instance            | Select **No**                                                                                         |

| Size                           | Leave at default                                                                                      |

| **Administrator account**      |                                                                                                       |

| Authentication type            | Select **SSH public key**                                                                                   |

| Username                       | Enter a username for the SSH public key. |

| SSH public key source | Select **Generate new key pair**. |

| SSH key type | Select **RSA SSH Format**. |

| Key pair name | Enter a name for the key pair. |

2. Select the **Networking** tab or select **Next: Spot > Next: Disks > Next: Networking**.

3. Enter or select this information in the **Networking** tab:

| Setting                           | Value                                                    |

|-----------------------------------|----------------------------------------------------------|

| **Virtual Network Configuration** |                                                          |

| Virtual network                   | Select **myVNet** or your existing virtual network.      |

| **Load balancing**       |                                                          |

| Load balancing options            | Select **Azure load balancer**                           |

| Select a load balancer            | Select **myLoadBalancer** or your existing load balancer |

| Select a backend pool             | Select **myBackendPool** or your existing backend pool. |

4. Select the **Management** tab.

5. In the **Management** tab, set **Boot diagnostics** to **Off**.

6. Select the blue **Review + create** button.

7. Review the settings and select the **Create** button.

# [Azure CLI](#tab/cli)

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- You need an existing [standard sku load balancer](quickstart-load-balancer-standard-internal-cli.md) in the subscription where the Virtual Machine Scale Set will be deployed. Ensure the load balancer has a backend pool.

- You need an [Azure Virtual Network](../virtual-network/quick-create-cli.md) for the Virtual Machine Scale Set.

[!INCLUDE [azure-cli-prepare-your-environment-no-header.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment-no-header.md)]

- This article requires version 2.0.28 or later of the Azure CLI. If using Azure Cloud Shell, the latest version is already installed.

## Deploy a Virtual Machine Scale Set with existing load balancer

Deploy a Virtual Machine Scale Set with [`az vmss create`](/cli/azure/vmss#az-vmss-create).

Replace the values in brackets with the names of the resources in your configuration.

```azurecli-interactive

az vmss create \

--resource-group <resource-group> \

--name <vmss-name>\

--image <your-image> \

--admin-username <admin-username> \

--generate-ssh-keys  \

--upgrade-policy-mode Automatic \

--instance-count 3 \

--vnet-name <virtual-network-name> \

--subnet <subnet-name> \

--lb <load-balancer-name> \

--backend-pool-name <backend-pool-name>

```

The below example deploys a Virtual Machine Scale Set with:

- Virtual Machine Scale Set named **myVMSS**

- Azure Load Balancer named **myLoadBalancer**

- Load balancer backend pool named **myBackendPool**

- Azure Virtual Network named **myVnet**

- Subnet named **mySubnet**

- Resource group named **myResourceGroup**

- Ubuntu Server image for the Virtual Machine Scale Set

```azurecli-interactive

az vmss create \

--resource-group myResourceGroup \

--name myVMSS \

--image Ubuntu2204 \

--admin-username adminuser \

--generate-ssh-keys \

--upgrade-policy-mode Automatic \

--instance-count 3 \

--vnet-name myVnet\

--subnet mySubnet \

--lb myLoadBalancer \

--backend-pool-name myBackendPool

```

> [!NOTE]

> After the scale set has been created, the backend port can't be modified for a load-balancing rule used by a health probe of the load balancer. To change the port, you can remove the health probe by updating the Azure virtual machine scale set, update the port and then configure the health probe again.

# [Azure PowerShell](#tab/powershell)

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- - An [Azure Virtual Network](../virtual-network/quick-create-powershell.md) for the Virtual Machine Scale Set and the load balancer.

- An existing [standard sku load balancer](quickstart-load-balancer-standard-internal-powershell.md) in the subscription where the Virtual Machine Scale Set will be deployed. Ensure the load balancer has a backend pool.

[!INCLUDE [cloud-shell-try-it.md](~/reusable-content/ce-skilling/azure/includes/cloud-shell-try-it.md)]

[!INCLUDE [updated-for-az](~/reusable-content/ce-skilling/azure/includes/updated-for-az.md)]

## Sign in to Azure CLI

Sign into Azure with [`Connect-AzAccount`](/powershell/module/az.accounts/connect-azaccount#example-1-connect-to-an-azure-account)

```azurepowershell-interactive

Connect-AzAccount

```

## Deploy a Virtual Machine Scale Set with existing load balancer

Deploy a Virtual Machine Scale Set with [`New-AzVMss`](/powershell/module/az.compute/new-azvmss). Replace the values in brackets with the names of the resources in your configuration.

```azurepowershell-interactive

$rsg = <resource-group>

$loc = <location>

$vms = <vm-scale-set-name>

$vnt = <virtual-network>

$sub = <subnet-name>

$lbn = <load-balancer-name>

$pol = <upgrade-policy-mode>

$img = <image-name>

$bep = <backend-pool-name>

$img = <image-name>

$lb = Get-AzLoadBalancer -ResourceGroupName $rsg -Name $lbn

New-AzVmss -ResourceGroupName $rsg -Location $loc -VMScaleSetName $vms -VirtualNetworkName $vnt -SubnetName $sub -LoadBalancerName $lb -UpgradePolicyMode $pol

```

The below example deploys a Virtual Machine Scale Set with the following values:

- Virtual Machine Scale Set named **myVMSS**

- Azure Load Balancer named **myLoadBalancer**

- Load balancer backend pool named **myBackendPool**

- Azure Virtual Network named **myVnet**

- Subnet named **mySubnet**

- Resource group named **myResourceGroup**

```azurepowershell-interactive

$rsg = "myResourceGroup"

$loc = "East US"

$vms = "myVMSS"

$vnt = "myVNet"

$sub = "default"

$pol = "Automatic"

$lbn = "myLoadBalancer"

$bep = "myBackendPool"

$img = "Ubuntu2204"

$lb = Get-AzLoadBalancer -ResourceGroupName $rsg -Name $lbn

New-AzVmss -ResourceGroupName $rsg -Location $loc -VMScaleSetName $vms -VirtualNetworkName $vnt -SubnetName $sub -LoadBalancerName $lb -UpgradePolicyMode $pol -BackendPoolName $bep -ImageName $img

```

> [!NOTE]

> After the scale set has been created, the backend port can't be modified for a load balancing rule used by a health probe of the load balancer. To change the port, you can remove the health probe by updating the Azure virtual machine scale set, update the port and then configure the health probe again.

## Next steps

In this article, you deployed a Virtual Machine Scale Set with an existing Azure Load Balancer.  To learn more about Virtual Machine Scale Sets and load balancer, see:

- [What is Azure Load Balancer?](load-balancer-overview.md)

- [What are Virtual Machine Scale Sets?](/azure/virtual-machine-scale-sets/overview)


# Load Balancer Multiple Ip

# Tutorial: Load balance multiple IP configurations

To host multiple websites, you can use another network interface associated with a virtual machine. Azure Load Balancer supports deployment of load-balancing to support the high availability of the websites.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create and configure a virtual network, subnet, and NAT gateway.

> * Create two Windows server virtual machines

> * Create a secondary NIC and network configurations for each virtual machine

> * Create two Internet Information Server (IIS) websites on each virtual machine

> * Bind the websites to the network configurations

> * Create and configure an Azure Load Balancer

> * Test the load balancer

[!INCLUDE [load-balancer-multi-ip-portal](../../includes/load-balancer-multi-ip-portal.md)]

[!INCLUDE [load-balancer-multi-ip-cli](../../includes/load-balancer-multi-ip-cli.md)]

[!INCLUDE [load-balancer-multi-ip-powershell](../../includes/load-balancer-multi-ip-powershell.md)]

## Next steps

Advance to the next article to learn how to create a cross-region load balancer:

> [!div class="nextstepaction"]

> [Create an Azure Global Load Balancer](/azure/load-balancer/tutorial-cross-region-portal?tabs=azureportal)


# Move Across Regions Azure Load Balancer

# Move an Azure Load Balancer to another Azure region

There are various scenarios in which you'd want to move an internal or external load balancer from one region to another. For example, you might want to create another load balancer with the same configuration for testing. You also might want to move a load balancer to another region as part of disaster recovery planning.

In a literal sense, you can't move an Azure load balancer from one region to another. But you can use an Azure Resource Manager template to export the existing configuration and public IP address of a load balancer. You can then stage the resource in another region by exporting the load balancer and public IP to a template, modifying the parameters to match the destination region, and then deploying the template to the new region. For more information on Resource Manager and templates, see [Export resource groups to templates](../azure-resource-manager/management/manage-resource-groups-powershell.md#export-resource-groups-to-templates).

In this article, you learn how to move an external or internal load balancer from one Azure region to another using the Azure portal or Azure PowerShell. Choose the tab that matches your preferred method and the type of load balancer you want to move.

# [External load balancer](#tab/external-load-balancer)

## Move an external load balancer to another region using the Azure portal

Use this procedure to move an external load balancer to another region using the Azure portal or Azure PowerShell.

# [Internal load balancer](#tab/internal-load-balancer)

## Move an Internal load balancer to another region using the Azure portal

Use this procedure to move an internal load balancer to another region using the Azure portal or Azure PowerShell.

---

# [Azure portal](#tab/azure-portal/external-load-balancer)

#### Prerequisites

- Make sure the Azure external load balancer is in the Azure region from which you want to move.

- Azure external load balancers can't be moved between regions. You have to associate the new load balancer to resources in the target region.

- To export an external load balancer configuration and deploy a template to create an external load balancer in another region, you need to be assigned the Network Contributor role or higher.

- Identify the source networking layout and all the resources that you're currently using. This layout includes but isn't limited to load balancers, network security groups,  public IPs, and virtual networks.

- Verify that your Azure subscription allows you to create external load balancers in the target region. Contact support to enable the required quota.

- Make sure your subscription has enough resources to support the addition of the load balancers. See [Azure subscription and service limits, quotas, and constraints](../azure-resource-manager/management/azure-subscription-service-limits.md#azure-networking-limits).

#### Prepare and move

The following procedures show how to prepare the external load balancer for the move by using a Resource Manager template and move the external load balancer configuration to the target region by using the Azure portal. You must first export the public IP configuration of external load balancer.

[!INCLUDE [updated-for-az](~/reusable-content/ce-skilling/azure/includes/updated-for-az.md)]

#### Export the public IP template and deploy the public IP from the portal

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Resource groups**.

2. Locate the resource group that contains the source public IP and select it.

3. Select **Settings** > **Export template**.

4. Select **Deploy** under **Export template**.

5. Select **TEMPLATE** > **Edit parameters** to open the parameters.json file in the online editor.

8. To edit the parameter of the public IP name, change the **value** property under **parameters** from the source public IP name to the name of your target public IP. Enclose the name in quotation marks.

```json

{

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"publicIPAddresses_myVM1pubIP_name": {

"value": "<target-publicip-name>"

}

}

}

```

Select **Save** in the editor.

9. Select **TEMPLATE** > **Edit template** to open the template.json file in the online editor.

10. To edit the target region to which the public IP will be moved, change the **location** property under **resources**:

```json

"resources": [

{

"type": "Microsoft.Network/publicIPAddresses",

"apiVersion": "2019-06-01",

"name": "[parameters('publicIPAddresses_myPubIP_name')]",

"location": "<target-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

"properties": {

"provisioningState": "Succeeded",

"resourceGuid": "7549a8f1-80c2-481a-a073-018f5b0b69be",

"ipAddress": "52.177.6.204",

"publicIPAddressVersion": "IPv4",

"publicIPAllocationMethod": "Static",

"idleTimeoutInMinutes": 4,

"ipTags": []

}

}

]

```

To get region location codes, see [Azure locations](https://azure.microsoft.com/global-infrastructure/locations/). The code for a region is the region name with no spaces. For example, the code for Central US is **centralus**.

12. You can also change other parameters in the template if you want to or need to, depending on your requirements:

* **SKU**. You can change the SKU of the public IP in the configuration from standard to basic or from basic to standard by changing the **name** property under **sku** in the template.json file:

```json

"resources": [

{

"type": "Microsoft.Network/publicIPAddresses",

"apiVersion": "2019-06-01",

"name": "[parameters('publicIPAddresses_myPubIP_name')]",

"location": "<target-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

```

* **Availability zone**. You can change the zone(s) of the public IP by changing the **zone** property. If the zone property isn't specified, the public IP is created as zone-redundant.

```json

"resources": [

{

"type": "Microsoft.Network/publicIPAddresses",

"apiVersion": "2019-06-01",

"name": "[parameters('publicIPAddresses_myPubIP_name')]",

"location": "<target-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

"zones": [

"1",

"2",

"3"

],

```

* **Public IP allocation method** and **Idle timeout**. You can change the public IP allocation method by changing the **publicIPAllocationMethod** property from **Static** to **Dynamic** or from **Dynamic** to **Static**. You can change the idle timeout by changing the **idleTimeoutInMinutes** property to the desired value. The default is **4**.

```json

"resources": [

{

"type": "Microsoft.Network/publicIPAddresses",

"apiVersion": "2019-06-01",

"name": "[parameters('publicIPAddresses_myPubIP_name')]",

"location": "<target-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

"zones": [

"1",

"2",

"3"

],

"properties": {

"provisioningState": "Succeeded",

"resourceGuid": "7549a8f1-80c2-481a-a073-018f5b0b69be",

"ipAddress": "52.177.6.204",

"publicIPAddressVersion": "IPv4",

"publicIPAllocationMethod": "Static",

"idleTimeoutInMinutes": 4,

"ipTags": []

```

For information on the allocation methods and idle timeout values, see [Create, change, or delete a public IP address](../virtual-network/ip-services/virtual-network-public-ip-address.md).

13. Select **Save** in the online editor.

14. Select **BASICS** > **Subscription** to choose the subscription where the target public IP will be deployed.

15. Select **BASICS** > **Resource group** to choose the resource group where the target public IP will be deployed. You can select **Create new** to create a new resource group for the target public IP. Make sure the name isn't the same as the source resource group of the existing source public IP.

16. Verify that **BASICS** > **Location** is set to the target location where you want the public IP to be deployed.

17. Under **SETTINGS**, verify that the name matches the name that you entered earlier in the parameters editor.

18. Select the **TERMS AND CONDITIONS** check box.

19. Select **Purchase** to deploy the target public IP.

20. If you have another public IP that's being used for outbound NAT for the load balancer being moved, repeat the previous steps to export and deploy the second outbound public IP to the target region.

#### Export the external load balancer template and deploy the load balancer from the Azure portal

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Resource groups**.

2. Locate the resource group that contains the source external load balancer and select it.

3. Select **Settings** > **Export template**.

4. Select **Deploy** under **Export template**.

5. Select **TEMPLATE** > **Edit parameters** to open the parameters.json file in the online editor.

5. To edit the parameter of the external load balancer name, change the **value** property of the source external load balancer name to the name of your target external load balancer. Enclose the name in quotation marks.

```json

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"loadBalancers_myLoadbalancer_ext_name": {

"value": "<target-external-lb-name>"

},

"publicIPAddresses_myPubIP_in_externalid": {

"value": "<target-publicIP-resource-ID>"

},

```

6. To edit value of the target public IP that you moved in the preceding steps, you must first obtain the resource ID, and then paste it into the parameters.json file. To obtain the ID:

1. In another browser tab or window, sign in to the [Azure portal](https://portal.azure.com) and select **Resource groups**.

2. Locate the target resource group that contains the public IP that you moved in the preceding steps. Select it.

3. Select **Settings** > **Properties**.

4. On the right-side, highlight the **Resource ID** and copy it to the clipboard. Alternatively, you can select **copy to clipboard** to the right of the **Resource ID** path.

5. Paste the resource ID into the **value** property in the **Edit Parameters** editor that's open in the other browser window or tab:

```json

```json

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"loadBalancers_myLoadbalancer_ext_name": {

"value": "<target-external-lb-name>"

},

"publicIPAddresses_myPubIP_in_externalid": {

"value": "<target-publicIP-resource-ID>"

},

```

6. Select **Save** in the online editor.

7. If you've configured outbound NAT and outbound rules for the load balancer, you see a third entry in this file for the external ID of the outbound public IP. Repeat the preceding steps in the **target region** to obtain the ID for the outbound public IP. Paste that ID into the parameters.json file:

```json

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"loadBalancers_myLoadbalancer_ext_name": {

"value": "<target-external-lb-name>",

},

"publicIPAddresses_myPubIP_in_externalid": {

"value": "<target-publicIP-resource-ID>",

},

"publicIPAddresses_myPubIP_out_externalid": {

"defaultValue": "<target-publicIP-outbound-resource-ID>",

}

},

```

8. Select **TEMPLATE** > **Edit template** to open the template.json file in the online editor.

9. To edit the target region to which the external load balancer configuration will be moved, change the **location** property under **resources** in the template.json file:

```json

"resources": [

{

"type": "Microsoft.Network/loadBalancers",

"apiVersion": "2019-06-01",

"name": "[parameters('loadBalancers_myLoadBalancer_name')]",

"location": "<target-external-lb-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

```

10. To get region location codes, see [Azure locations](https://azure.microsoft.com/global-infrastructure/locations/). The code for a region is the region name with no spaces. For example, the code for Central US is **centralus**.

11. You can also change other parameters in the template if you want to or need to, depending on your requirements:

* **SKU**. You can change the SKU of the external load balancer in the configuration from Standard to Basic or from Basic to Standard by changing the **name** property under **sku** in the template.json file:

```json

"resources": [

{

"type": "Microsoft.Network/loadBalancers",

"apiVersion": "2019-06-01",

"name": "[parameters('loadBalancers_myLoadBalancer_name')]",

"location": "<target-external-lb-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

```

For information on the differences between basic and standard SKU load balancers, see [Azure Standard Load Balancer overview](./load-balancer-overview.md).

* **Load balancing rules**. You can add or remove load balancing rules in the configuration by adding or removing entries in the **loadBalancingRules** section of the template.json file:

```json

"loadBalancingRules": [

{

"name": "myInboundRule",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"properties": {

"provisioningState": "Succeeded",

"frontendIPConfiguration": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPinbound')]"

},

"frontendPort": 80,

"backendPort": 80,

"enableFloatingIP": false,

"idleTimeoutInMinutes": 4,

"protocol": "Tcp",

"enableTcpReset": false,

"loadDistribution": "Default",

"disableOutboundSnat": true,

"backendAddressPool": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/backendAddressPools/myBEPoolInbound')]"

},

"probe": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/probes/myHTTPProbe')]"

}

}

}

]

```

For information on load balancing rules, see [What is Azure Load Balancer?](load-balancer-overview.md).

* **Probes**. You can add or remove a probe for the load balancer in the configuration by adding or removing entries in the **probes** section of the template.json file:

```json

"probes": [

{

"name": "myHTTPProbe",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"properties": {

"provisioningState": "Succeeded",

"protocol": "Http",

"port": 80,

"requestPath": "/",

"intervalInSeconds": 15,

"numberOfProbes": 2

}

}

],

```

For more information, see [Load Balancer health probes](load-balancer-custom-probe-overview.md).

* **Inbound NAT rules**. You can add or remove inbound NAT rules for the load balancer by adding or removing entries in the **inboundNatRules** section of the template.json file:

```json

"inboundNatRules": [

{

"name": "myInboundNATRule",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"properties": {

"provisioningState": "Succeeded",

"frontendIPConfiguration": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPinbound')]"

},

"frontendPort": 4422,

"backendPort": 3389,

"enableFloatingIP": false,

"idleTimeoutInMinutes": 4,

"protocol": "Tcp",

"enableTcpReset": false

}

}

]

```

To complete the addition or removal of an inbound NAT rule, the rule must be present or removed as a **type** property at the end of the template.json file:

```json

{

"type": "Microsoft.Network/loadBalancers/inboundNatRules",

"apiVersion": "2019-06-01",

"name": "[concat(parameters('loadBalancers_myLoadBalancer_name'), '/myInboundNATRule')]",

"dependsOn": [

"[resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name'))]"

],

"properties": {

"provisioningState": "Succeeded",

"frontendIPConfiguration": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPinbound')]"

},

"frontendPort": 4422,

"backendPort": 3389,

"enableFloatingIP": false,

"idleTimeoutInMinutes": 4,

"protocol": "Tcp",

"enableTcpReset": false

}

}

```

For information on inbound NAT rules, see [What is Azure Load Balancer?](load-balancer-overview.md).

* **Outbound rules**. You can add or remove outbound rules in the configuration by editing the **outboundRules** property in the template.json file:

```json

"outboundRules": [

{

"name": "myOutboundRule",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"properties": {

"provisioningState": "Succeeded",

"allocatedOutboundPorts": 10000,

"protocol": "All",

"enableTcpReset": false,

"idleTimeoutInMinutes": 15,

"backendAddressPool": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/backendAddressPools/myBEPoolOutbound')]"

},

"frontendIPConfigurations": [

{

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPoutbound')]"

}

]

}

}

]

```

For more information, see [Load Balancer outbound rules](./load-balancer-outbound-connections.md#outboundrules).

12. Select **Save** in the online editor.

13. Select **BASICS** > **Subscription** to choose the subscription where the target external load balancer will be deployed.

15. Select **BASICS** > **Resource group** to choose the resource group where the target load balancer will be deployed. You can select **Create new** to create a new resource group for the target external load balancer. Or you can choose the existing resource group that you created earlier for the public IP. Make sure the name isn't the same as the source resource group of the existing source external load balancer.

16. Verify that **BASICS** > **Location** is set to the target location where you want the external load balancer to be deployed.

17. Under **SETTINGS**, verify that the name matches the name you entered earlier in the parameters editor. Verify that the resource IDs are populated for any public IPs in the configuration.

18. Select the **TERMS AND CONDITIONS** check box.

19. Select **Purchase** to deploy the target public IP.

### Discard

If you want to discard the target public IP and external load balancer, delete the resource group that contains them. To do so, select the resource group from your dashboard in the portal and then select **Delete** at the top of the overview page.

### Clean up

To commit the changes and complete the move of the public IP and external load balancer, delete the source public IP and external load balancer or resource group. To do so, select that resource group from your dashboard in the portal and then select **Delete** at the top of each page.

### Next steps

In this tutorial, you moved an Azure external load balancer from one region to another and cleaned up the source resources. To learn more about moving resources between regions and disaster recovery in Azure, see:

- [Move resources to a new resource group or subscription](../azure-resource-manager/management/move-resource-group-and-subscription.md)

- [Move Azure VMs to another region](../site-recovery/azure-to-azure-tutorial-migrate.md)

# [Azure PowerShell](#tab/azure-powershell/external-load-balancer)

### Prerequisites

- Make sure that the Azure external load balancer is in the Azure region from which you want to move.

- Azure external load balancers can't be moved between regions. You have to associate the new load balancer to resources in the target region.

- To export an external load balancer configuration and deploy a template to create an external load balancer in another region, you need the Network Contributor role or higher.

- Identify the source networking layout and all the resources that you're currently using. This layout includes but isn't limited to load balancers, network security groups,  public IPs, and virtual networks.

- Verify that your Azure subscription allows you to create external load balancers in the target region that's used. Contact support to enable the required quota.

- Make sure that your subscription has enough resources to support the addition of load balancers for this process. See [Azure subscription and service limits, quotas, and constraints](../azure-resource-manager/management/azure-subscription-service-limits.md#azure-networking-limits)

### Prepare and move

The following steps show how to prepare the external load balancer for the move using a Resource Manager template, and move the external load balancer configuration to the target region using Azure PowerShell. As part of this process, the public IP configuration of the external load balancer must be included and must me done first before moving the external load balancer.

[!INCLUDE [updated-for-az](~/reusable-content/ce-skilling/azure/includes/updated-for-az.md)]

#### Export the public IP template and deploy from Azure PowerShell

1. Sign in to your Azure subscription with the [Connect-AzAccount](/powershell/module/az.accounts/connect-azaccount) command and follow the on-screen directions:

```azurepowershell-interactive

Connect-AzAccount

```

2. Obtain the resource ID of the public IP you want to move to the target region and place it in a variable using [Get-AzPublicIPAddress](/powershell/module/az.network/get-azpublicipaddress):

```azurepowershell-interactive

$sourcePubIPID = (Get-AzPublicIPaddress -Name <source-public-ip-name> -ResourceGroupName <source-resource-group-name>).Id

```

3. Export the source public IP to a .json file into the directory where you execute the command [Export-AzResourceGroup](/powershell/module/az.resources/export-azresourcegroup):

```azurepowershell-interactive

Export-AzResourceGroup -ResourceGroupName <source-resource-group-name> -Resource $sourceVNETID -IncludeParameterDefaultValue

```

4. The file downloaded will be named after the resource group the resource was exported from. Locate the file that was exported from the command named **\<resource-group-name>.json** and open it in an editor of your choice:

```azurepowershell

notepad.exe <source-resource-group-name>.json

```

5. To edit the parameter of the public IP name, change the property **defaultValue** of the source public IP name to the name of your target public IP, ensure the name is in quotes:

```json

{

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"publicIPAddresses_myVM1pubIP_name": {

"defaultValue": "<target-publicip-name>",

"type": "String"

}

}

```

6. To edit the target region where the public IP will be moved, change the **location** property under resources:

```json

"resources": [

{

"type": "Microsoft.Network/publicIPAddresses",

"apiVersion": "2019-06-01",

"name": "[parameters('publicIPAddresses_myPubIP_name')]",

"location": "<target-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

"properties": {

"provisioningState": "Succeeded",

"resourceGuid": "7549a8f1-80c2-481a-a073-018f5b0b69be",

"ipAddress": "52.177.6.204",

"publicIPAddressVersion": "IPv4",

"publicIPAllocationMethod": "Static",

"idleTimeoutInMinutes": 4,

"ipTags": []

}

}

]

```

7. To obtain region location codes, you can use the Azure PowerShell cmdlet [Get-AzLocation](/powershell/module/az.resources/get-azlocation) by running the following command:

```azurepowershell-interactive

Get-AzLocation | format-table

```

8. You can also change other parameters in the template if you choose, and are optional depending on your requirements:

* **Sku** - You can change the sku of the public IP in the configuration from Standard to Basic or Basic to Standard by altering the **sku** > **name** property in the **\<resource-group-name>.json** file:

```json

"resources": [

{

"type": "Microsoft.Network/publicIPAddresses",

"apiVersion": "2019-06-01",

"name": "[parameters('publicIPAddresses_myPubIP_name')]",

"location": "<target-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

```

For more information on the differences between basic and standard sku public ips, see [Create, change, or delete a public IP address](../virtual-network/ip-services/virtual-network-public-ip-address.md).

* **Availability zone**. You can change the zone(s) of the public IP by changing the **zone** property. If the zone property isn't specified, the public IP is created as zone-redundant.

```json

"resources": [

{

"type": "Microsoft.Network/publicIPAddresses",

"apiVersion": "2019-06-01",

"name": "[parameters('publicIPAddresses_myPubIP_name')]",

"location": "<target-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

"zones": [

"1",

"2",

"3"

],

```

* **Public IP allocation method** and **Idle timeout** - You can change both of these options in the template by altering the **publicIPAllocationMethod** property from **Static** to **Dynamic** or **Dynamic** to **Static**. The idle timeout can be changed by altering the **idleTimeoutInMinutes** property to your desired amount. The default is **4**:

```json

"resources": [

{

"type": "Microsoft.Network/publicIPAddresses",

"apiVersion": "2019-06-01",

"name": "[parameters('publicIPAddresses_myPubIP_name')]",

"location": "<target-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

"properties": {

"provisioningState": "Succeeded",

"resourceGuid": "7549a8f1-80c2-481a-a073-018f5b0b69be",

"ipAddress": "52.177.6.204",

"publicIPAddressVersion": "IPv4",

"publicIPAllocationMethod": "Static",

"idleTimeoutInMinutes": 4,

"ipTags": []

}

}

```

For more information on the allocation methods and the idle timeout values, see [Create, change, or delete a public IP address](../virtual-network/ip-services/virtual-network-public-ip-address.md).

9. Save the **\<resource-group-name>.json** file.

10. Create a resource group in the target region for the target public IP to be deployed using [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup).

```azurepowershell-interactive

New-AzResourceGroup -Name <target-resource-group-name> -location <target-region>

```

11. Deploy the edited **\<resource-group-name>.json** file to the resource group created in the previous step using [New-AzResourceGroupDeployment](/powershell/module/az.resources/new-azresourcegroupdeployment):

```azurepowershell-interactive

New-AzResourceGroupDeployment -ResourceGroupName <target-resource-group-name> -TemplateFile <source-resource-group-name>.json

```

12. To verify the resources were created in the target region, use [Get-AzResourceGroup](/powershell/module/az.resources/get-azresourcegroup) and [Get-AzPublicIPAddress](/powershell/module/az.network/get-azpublicipaddress):

```azurepowershell-interactive

Get-AzResourceGroup -Name <target-resource-group-name>

```

```azurepowershell-interactive

Get-AzPublicIPAddress -Name <target-publicip-name> -ResourceGroupName <target-resource-group-name>

```

#### Export the external load balancer template and deploy from Azure PowerShell

1. Sign in to your Azure subscription with the [Connect-AzAccount](/powershell/module/az.accounts/connect-azaccount) command and follow the on-screen directions:

```azurepowershell-interactive

Connect-AzAccount

```

2. Obtain the resource ID of the external load balancer you want to move to the target region and place it in a variable using [Get-AzLoadBalancer](/powershell/module/az.network/get-azloadbalancer):

```azurepowershell-interactive

$sourceExtLBID = (Get-AzLoadBalancer -Name <source-external-lb-name> -ResourceGroupName <source-resource-group-name>).Id

```

3. Export the source external load balancer configuration to a .json file into the directory where you execute the command [Export-AzResourceGroup](/powershell/module/az.resources/export-azresourcegroup):

```azurepowershell-interactive

Export-AzResourceGroup -ResourceGroupName <source-resource-group-name> -Resource $sourceExtLBID -IncludeParameterDefaultValue

```

4. The file downloaded will be named after the resource group the resource was exported from. Locate the file that was exported from the command named **\<resource-group-name>.json** and open it in an editor of your choice:

```azurepowershell

notepad.exe <source-resource-group-name>.json

```

5. To edit the parameter of the external load balancer name, change the property **defaultValue** of the source external load balancer name to the name of your target external load balancer, ensure the name is in quotes:

```json

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"loadBalancers_myLoadbalancer_ext_name": {

"defaultValue": "<target-external-lb-name>",

"type": "String"

},

"publicIPAddresses_myPubIP_in_externalid": {

"defaultValue": "<target-publicIP-resource-ID>",

"type": "String"

},

```

6. To edit value of the target public IP that was moved above, you must first obtain the resource ID and then copy and paste it into the **\<resource-group-name>.json** file. To obtain the ID, use [Get-AzPublicIPAddress](/powershell/module/az.network/get-azpublicipaddress):

```azurepowershell-interactive

$targetPubIPID = (Get-AzPublicIPaddress -Name <target-public-ip-name> -ResourceGroupName <target-resource-group-name>).Id

```

Type the variable and hit enter to display the resource ID. Highlight the ID path and copy it to the clipboard:

```powershell

PS C:\> $targetPubIPID

/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroupLB-Move/providers/Microsoft.Network/publicIPAddresses/myPubIP-in-move

```

7. In the **\<resource-group-name>.json** file, paste the **Resource ID** from the variable in place of the **defaultValue** in the second parameter for the public IP external ID, ensure you enclose the path in quotes:

```json

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"loadBalancers_myLoadbalancer_ext_name": {

"defaultValue": "<target-external-lb-name>",

"type": "String"

},

"publicIPAddresses_myPubIP_in_externalid": {

"defaultValue": "<target-publicIP-resource-ID>",

"type": "String"

},

```

8. If you configured outbound NAT and outbound rules for the load balancer, a third entry is present in this file for the external ID for the outbound public IP. Repeat the steps above in the **target region** to obtain the ID for the outbound public iP and paste that entry into the **\<resource-group-name>.json** file:

```json

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"loadBalancers_myLoadbalancer_ext_name": {

"defaultValue": "<target-external-lb-name>",

"type": "String"

},

"publicIPAddresses_myPubIP_in_externalid": {

"defaultValue": "<target-publicIP-resource-ID>",

"type": "String"

},

"publicIPAddresses_myPubIP_out_externalid": {

"defaultValue": "<target-publicIP-outbound-resource-ID>",

"type": "String"

}

},

```

10. To edit the target region where the external load balancer configuration will be moved, change the **location** property under **resources** in the **\<resource-group-name>.json** file:

```json

"resources": [

{

"type": "Microsoft.Network/loadBalancers",

"apiVersion": "2019-06-01",

"name": "[parameters('loadBalancers_myLoadBalancer_name')]",

"location": "<target-external-lb-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

```

11. To obtain region location codes, you can use the Azure PowerShell cmdlet [Get-AzLocation](/powershell/module/az.resources/get-azlocation) by running the following command:

```azurepowershell-interactive

Get-AzLocation | format-table

```

12. You can also change other parameters in the template if you choose, and are optional depending on your requirements:

* **Sku** - You can change the sku of the external load balancer in the configuration from standard to basic or basic to standard by altering the **sku** > **name** property in the **\<resource-group-name>.json** file:

```json

"resources": [

{

"type": "Microsoft.Network/loadBalancers",

"apiVersion": "2019-06-01",

"name": "[parameters('loadBalancers_myLoadBalancer_name')]",

"location": "<target-external-lb-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

```

For more information on the differences between basic and standard sku load balancers, see [Azure Standard Load Balancer overview](./load-balancer-overview.md)

* **Load balancing rules** - You can add or remove load balancing rules in the configuration by adding or removing entries to the **loadBalancingRules** section of the **\<resource-group-name>.json** file:

```json

"loadBalancingRules": [

{

"name": "myInboundRule",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"properties": {

"provisioningState": "Succeeded",

"frontendIPConfiguration": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPinbound')]"

},

"frontendPort": 80,

"backendPort": 80,

"enableFloatingIP": false,

"idleTimeoutInMinutes": 4,

"protocol": "Tcp",

"enableTcpReset": false,

"loadDistribution": "Default",

"disableOutboundSnat": true,

"backendAddressPool": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/backendAddressPools/myBEPoolInbound')]"

},

"probe": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/probes/myHTTPProbe')]"

}

}

}

]

```

For more information on load balancing rules, see [What is Azure Load Balancer?](./load-balancer-overview.md)

* **Probes** - You can add or remove a probe for the load balancer in the configuration by adding or removing entries to the **probes** section of the **\<resource-group-name>.json** file:

```json

"probes": [

{

"name": "myHTTPProbe",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"properties": {

"provisioningState": "Succeeded",

"protocol": "Http",

"port": 80,

"requestPath": "/",

"intervalInSeconds": 15,

"numberOfProbes": 2

}

}

],

```

For more information on Azure Load Balancer health probes, see [Load Balancer health probes](./load-balancer-custom-probe-overview.md)

* **Inbound NAT rules** - You can add or remove inbound NAT rules for the load balancer by adding or removing entries to the **inboundNatRules** section of the **\<resource-group-name>.json** file:

```json

"inboundNatRules": [

{

"name": "myInboundNATRule",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"properties": {

"provisioningState": "Succeeded",

"frontendIPConfiguration": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPinbound')]"

},

"frontendPort": 4422,

"backendPort": 3389,

"enableFloatingIP": false,

"idleTimeoutInMinutes": 4,

"protocol": "Tcp",

"enableTcpReset": false

}

}

]

```

To complete the addition or removal of an inbound NAT rule, the rule must be present or removed as a **type** property at the end of the **\<resource-group-name>.json** file:

```json

{

"type": "Microsoft.Network/loadBalancers/inboundNatRules",

"apiVersion": "2019-06-01",

"name": "[concat(parameters('loadBalancers_myLoadBalancer_name'), '/myInboundNATRule')]",

"dependsOn": [

"[resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name'))]"

],

"properties": {

"provisioningState": "Succeeded",

"frontendIPConfiguration": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPinbound')]"

},

"frontendPort": 4422,

"backendPort": 3389,

"enableFloatingIP": false,

"idleTimeoutInMinutes": 4,

"protocol": "Tcp",

"enableTcpReset": false

}

}

```

For more information on inbound NAT rules, see [What is Azure Load Balancer?](./load-balancer-overview.md)

* **Outbound rules** - You can add or remove outbound rules in the configuration by editing the **outboundRules** property in the **\<resource-group-name>.json** file:

```json

"outboundRules": [

{

"name": "myOutboundRule",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"properties": {

"provisioningState": "Succeeded",

"allocatedOutboundPorts": 10000,

"protocol": "All",

"enableTcpReset": false,

"idleTimeoutInMinutes": 15,

"backendAddressPool": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/backendAddressPools/myBEPoolOutbound')]"

},

"frontendIPConfigurations": [

{

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPoutbound')]"

}

]

}

}

]

```

For more information on outbound rules, see [Load Balancer outbound rules](./load-balancer-outbound-connections.md#outboundrules)

13. Save the **\<resource-group-name>.json** file.

10. Create or a resource group in the target region for the target external load balancer to be deployed using [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup). The existing resource group from above can also be reused as part of this process:

```azurepowershell-interactive

New-AzResourceGroup -Name <target-resource-group-name> -location <target-region>

```

11. Deploy the edited **\<resource-group-name>.json** file to the resource group created in the previous step using [New-AzResourceGroupDeployment](/powershell/module/az.resources/new-azresourcegroupdeployment):

```azurepowershell-interactive

New-AzResourceGroupDeployment -ResourceGroupName <target-resource-group-name> -TemplateFile <source-resource-group-name>.json

```

12. To verify the resources were created in the target region, use [Get-AzResourceGroup](/powershell/module/az.resources/get-azresourcegroup) and [Get-AzLoadBalancer](/powershell/module/az.network/get-azloadbalancer):

```azurepowershell-interactive

Get-AzResourceGroup -Name <target-resource-group-name>

```

```azurepowershell-interactive

Get-AzLoadBalancer -Name <target-publicip-name> -ResourceGroupName <target-resource-group-name>

```

### Discard

After the deployment, if you wish to start over or discard the public IP and load balancer in the target, delete the resource group that was created in the target and the moved public IP and load balancer will be deleted. To remove the resource group, use [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup):

```azurepowershell-interactive

Remove-AzResourceGroup -Name <resource-group-name>

```

### Clean up

To commit the changes and complete the move of the NSG, delete the source NSG or resource group, use [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) or [Remove-AzPublicIpAddress](/powershell/module/az.network/remove-azpublicipaddress) and [Remove-AzLoadBalancer](/powershell/module/az.network/remove-azloadbalancer)

```azurepowershell-interactive

Remove-AzResourceGroup -Name <resource-group-name>

```

``` azurepowershell-interactive

Remove-AzLoadBalancer -name <load-balancer> -ResourceGroupName <resource-group-name>

Remove-AzPublicIpAddress -Name <public-ip> -ResourceGroupName <resource-group-name>

```

### Next steps

In this tutorial, you moved an Azure network security group from one region to another and cleaned up the source resources. To learn more about moving resources between regions and disaster recovery in Azure, refer to:

- [Move resources to a new resource group or subscription](../azure-resource-manager/management/move-resource-group-and-subscription.md)

- [Move Azure VMs to another region](../site-recovery/azure-to-azure-tutorial-migrate.md)

# [Azure portal](#tab/azure-portal/internal-load-balancer)

### Prerequisites

- Make sure that the Azure internal load balancer is in the Azure region from which you want to move.

- Azure internal load balancers can't be moved between regions. You have to associate the new load balancer to resources in the target region.

- To export an internal load balancer configuration and deploy a template to create an internal load balancer in another region, you need the Network Contributor role or higher.

- Identify the source networking layout and all the resources that you're currently using. This layout includes but isn't limited to load balancers, network security groups, virtual machines, and virtual networks.

- Verify that your Azure subscription allows you to create internal load balancers in the target region that's used. Contact support to enable the required quota.

- Make sure that your subscription has enough resources to support the addition of load balancers for this process. See [Azure subscription and service limits, quotas, and constraints](../azure-resource-manager/management/azure-subscription-service-limits.md#azure-networking-limits)

### Prepare and move

The following steps show how to prepare the internal load balancer for the move using a Resource Manager template, and move the internal load balancer configuration to the target region using the Azure portal. As part of this process, the virtual network configuration of the internal load balancer must be included and must be done first before moving the internal load balancer.

[!INCLUDE [updated-for-az](~/reusable-content/ce-skilling/azure/includes/updated-for-az.md)]

#### Export the virtual network template and deploy from the Azure portal

1. Sign in to the [Azure portal](https://portal.azure.com) > **Resource Groups**.

2. Locate the Resource Group that contains the source virtual network and select it.

3. Select > **Settings** > **Export template**.

4. Choose **Deploy** under **Export template**.

5. Select **TEMPLATE** > **Edit parameters** to open the **parameters.json** file in the online editor.

6. To edit the parameter of the virtual network name, change the **value** property under **parameters**:

```json

{

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"virtualNetworks_myVNET1_name": {

"value": "<target-virtual-network-name>"

}

}

}

```

7. Change the source virtual network name value in the editor to a name of your choice for the target virtual network. Ensure you enclose the name in quotes.

8. Select **Save** in the editor.

9. Select **TEMPLATE** > **Edit template** to open the **template.json** file in the online editor.

10. To edit the target region where the virtual network will be moved, change the **location** property under resources:

```json

"resources": [

{

"type": "Microsoft.Network/virtualNetworks",

"apiVersion": "2019-06-01",

"name": "[parameters('virtualNetworks_myVNET1_name')]",

"location": "<target-region>",

"properties": {

"provisioningState": "Succeeded",

"resourceGuid": "6e2652be-35ac-4e68-8c70-621b9ec87dcb",

"addressSpace": {

"addressPrefixes": [

"10.0.0.0/16"

]

},

```

11. To obtain region location codes, see [Azure Locations](https://azure.microsoft.com/global-infrastructure/locations/). The code for a region is the region name with no spaces, **Central US** = **centralus**.

12. You can also change other parameters in the **template.json** file if you choose, and are optional depending on your requirements:

* **Address Space** - The address space of the virtual network can be altered before saving by modifying the **resources** > **addressSpace** section and changing the **addressPrefixes** property in the **template.json** file:

```json

"resources": [

{

"type": "Microsoft.Network/virtualNetworks",

"apiVersion": "2019-06-01",

"name": "[parameters('virtualNetworks_myVNET1_name')]",

"location": "<target-region",

"properties": {

"provisioningState": "Succeeded",

"resourceGuid": "6e2652be-35ac-4e68-8c70-621b9ec87dcb",

"addressSpace": {

"addressPrefixes": [

"10.0.0.0/16"

]

},

```

* **Subnet** - The subnet name and the subnet address space can be changed or added to by modifying the **subnets** section of the **template.json** file. The name of the subnet can be changed by altering the **name** property. The subnet address space can be changed by altering the **addressPrefix** property in the **template.json** file:

```json

"subnets": [

{

"name": "subnet-1",

"etag": "W/\"d9f6e6d6-2c15-4f7c-b01f-bed40f748dea\"",

"properties": {

"provisioningState": "Succeeded",

"addressPrefix": "10.0.0.0/24",

"delegations": [],

"privateEndpointNetworkPolicies": "Enabled",

"privateLinkServiceNetworkPolicies": "Enabled"

}

},

{

"name": "GatewaySubnet",

"etag": "W/\"d9f6e6d6-2c15-4f7c-b01f-bed40f748dea\"",

"properties": {

"provisioningState": "Succeeded",

"addressPrefix": "10.0.1.0/29",

"serviceEndpoints": [],

"delegations": [],

"privateEndpointNetworkPolicies": "Enabled",

"privateLinkServiceNetworkPolicies": "Enabled"

}

}

]

```

In the **template.json** file, to change the address prefix, it must be edited in two places, the section listed above and the **type** section listed below. Change the **addressPrefix** property to match the one above:

```json

"type": "Microsoft.Network/virtualNetworks/subnets",

"apiVersion": "2019-06-01",

"name": "[concat(parameters('virtualNetworks_myVNET1_name'), '/GatewaySubnet')]",

"dependsOn": [

"[resourceId('Microsoft.Network/virtualNetworks', parameters('virtualNetworks_myVNET1_name'))]"

],

"properties": {

"provisioningState": "Succeeded",

"addressPrefix": "10.0.1.0/29",

"serviceEndpoints": [],

"delegations": [],

"privateEndpointNetworkPolicies": "Enabled",

"privateLinkServiceNetworkPolicies": "Enabled"

}

},

{

"type": "Microsoft.Network/virtualNetworks/subnets",

"apiVersion": "2019-06-01",

"name": "[concat(parameters('virtualNetworks_myVNET1_name'), '/subnet-1')]",

"dependsOn": [

"[resourceId('Microsoft.Network/virtualNetworks', parameters('virtualNetworks_myVNET1_name'))]"

],

"properties": {

"provisioningState": "Succeeded",

"addressPrefix": "10.0.0.0/24",

"delegations": [],

"privateEndpointNetworkPolicies": "Enabled",

"privateLinkServiceNetworkPolicies": "Enabled"

}

}

]

```

13. Select **Save** in the online editor.

14. Select **BASICS** > **Subscription** to choose the subscription where the target virtual network will be deployed.

15. Select **BASICS** > **Resource group** to choose the resource group where the target virtual network will be deployed. You can select **Create new** to create a new resource group for the target virtual network. Ensure the name isn't the same as the source resource group of the existing virtual network.

16. Verify **BASICS** > **Location** is set to the target location where you wish for the virtual network to be deployed.

17. Verify under **SETTINGS** that the name matches the name that you entered in the parameters editor above.

18. Check the box under **TERMS AND CONDITIONS**.

19. Select the **Purchase** button to deploy the target virtual network.

### Export the internal load balancer template and deploy from Azure PowerShell

1. Select to the [Azure portal](https://portal.azure.com) > **Resource Groups**.

2. Locate the Resource Group that contains the source internal load balancer and select it.

3. Select > **Settings** > **Export template**.

4. Choose **Deploy** under **Export template**.

5. Select **TEMPLATE** > **Edit parameters** to open the **parameters.json** file in the online editor.

6. To edit the parameter of the internal load balancer name, change the property **defaultValue** of the source internal load balancer name to the name of your target internal load balancer, ensure the name is in quotes:

```json

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"loadBalancers_myLoadBalancer_name": {

"defaultValue": "<target-internal-lb-name>",

"type": "String"

},

"virtualNetworks_myVNET2_internalid": {

"defaultValue": "<target-vnet-resource-ID>",

"type": "String"

}

```

6. To edit value of the target virtual network that was moved above, you must first obtain the resource ID and then copy and paste it into the **parameters.json** file. To obtain the ID:

1. Select to the [Azure portal](https://portal.azure.com) > **Resource Groups** in another browser tab or window.

2. Locate the target resource group that contains the moved virtual network from the steps above, and select it.

3. Select > **Settings** > **Properties**.

4. On the right side of the portal, highlight the **Resource ID** and copy it to the clipboard. Alternatively, you can select the **copy to clipboard** button to the right of the **Resource ID** path.

5. Paste the resource ID into the **defaultValue** property into the **Edit Parameters** editor open in the other browser window or tab:

```json

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"loadBalancers_myLoadBalancer_name": {

"defaultValue": "<target-internal-lb-name>",

"type": "String"

},

"virtualNetworks_myVNET2_internalid": {

"defaultValue": "<target-vnet-resource-ID>",

"type": "String"

}

```

6. Select **Save** in the online editor.

7. Select **TEMPLATE** > **Edit template** to open the **template.json** file in the online editor.

8. To edit the target region where the internal load balancer configuration will be moved, change the **location** property under **resources** in the **template.json** file:

```json

"resources": [

{

"type": "Microsoft.Network/loadBalancers",

"apiVersion": "2019-06-01",

"name": "[parameters('loadBalancers_myLoadBalancer_name')]",

"location": "<target-internal-lb-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

```

9. To obtain region location codes, see [Azure Locations](https://azure.microsoft.com/global-infrastructure/locations/). The code for a region is the region name with no spaces, **Central US** = **centralus**.

10. You can also change other parameters in the template if you choose, and are optional depending on your requirements:

* **Sku** - You can change the sku of the internal load balancer in the configuration from standard to basic or basic to standard by altering the **sku** > **name** property in the **template.json** file:

```json

"resources": [

{

"type": "Microsoft.Network/loadBalancers",

"apiVersion": "2019-06-01",

"name": "[parameters('loadBalancers_myLoadBalancer_name')]",

"location": "<target-internal-lb-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

```

For more information on the differences between basic and standard sku load balancers, see [Azure Standard Load Balancer overview](./load-balancer-overview.md)

* **Availability zone** - You can change the zones of the load balancer's frontend by changing the **zone** property. If the zone property isn't specified, the frontend is created as zone-redundant.

```json

"frontendIPConfigurations": [

{

"name": "myfrontendIPinbound",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"type": "Microsoft.Network/loadBalancers/frontendIPConfigurations",

"properties": {

"provisioningState": "Succeeded",

"privateIPAddress": "10.0.0.6",

"privateIPAllocationMethod": "Dynamic",

"subnet": {

"id": "[concat(parameters('virtualNetworks_myVNET2_internalid'), '/subnet-1')]"

},

"loadBalancingRules": [

{

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/loadBalancingRules/myInboundRule')]"

}

],

"privateIPAddressVersion": "IPv4"

},

"zones": [

"1",

"2",

"3"

]

},

```

For more about availability zones, see [Regions and availability zones in Azure](/azure/reliability/availability-zones-overview).

* **Load balancing rules** - You can add or remove load balancing rules in the configuration by adding or removing entries to the **loadBalancingRules** section of the **template.json** file:

```json

"loadBalancingRules": [

{

"name": "myInboundRule",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"properties": {

"provisioningState": "Succeeded",

"frontendIPConfiguration": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPinbound')]"

},

"frontendPort": 80,

"backendPort": 80,

"enableFloatingIP": false,

"idleTimeoutInMinutes": 4,

"protocol": "Tcp",

"enableTcpReset": false,

"loadDistribution": "Default",

"disableOutboundSnat": true,

"backendAddressPool": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/backendAddressPools/myBEPoolInbound')]"

},

"probe": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/probes/myHTTPProbe')]"

}

}

}

]

```

For more information on load balancing rules, see [What is Azure Load Balancer?](./load-balancer-overview.md)

* **Probes** - You can add or remove a probe for the load balancer in the configuration by adding or removing entries to the **probes** section of the **template.json** file:

```json

"probes": [

{

"name": "myHTTPProbe",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"properties": {

"provisioningState": "Succeeded",

"protocol": "Http",

"port": 80,

"requestPath": "/",

"intervalInSeconds": 15,

"numberOfProbes": 2

}

}

],

```

For more information on Azure Load Balancer health probes, see [Load Balancer health probes](./load-balancer-custom-probe-overview.md)

* **Inbound NAT rules** - You can add or remove inbound NAT rules for the load balancer by adding or removing entries to the **inboundNatRules** section of the **template.json** file:

```json

"inboundNatRules": [

{

"name": "myInboundNATRule",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"properties": {

"provisioningState": "Succeeded",

"frontendIPConfiguration": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPinbound')]"

},

"frontendPort": 4422,

"backendPort": 3389,

"enableFloatingIP": false,

"idleTimeoutInMinutes": 4,

"protocol": "Tcp",

"enableTcpReset": false

}

}

]

```

To complete the addition or removal of an inbound NAT rule, the rule must be present or removed as a **type** property at the end of the **template.json** file:

```json

{

"type": "Microsoft.Network/loadBalancers/inboundNatRules",

"apiVersion": "2019-06-01",

"name": "[concat(parameters('loadBalancers_myLoadBalancer_name'), '/myInboundNATRule')]",

"dependsOn": [

"[resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name'))]"

],

"properties": {

"provisioningState": "Succeeded",

"frontendIPConfiguration": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPinbound')]"

},

"frontendPort": 4422,

"backendPort": 3389,

"enableFloatingIP": false,

"idleTimeoutInMinutes": 4,

"protocol": "Tcp",

"enableTcpReset": false

}

}

```

For more information on inbound NAT rules, see [What is Azure Load Balancer?](./load-balancer-overview.md)

12. Select **Save** in the online editor.

13. Select **BASICS** > **Subscription** to choose the subscription where the target internal load balancer will be deployed.

15. Select **BASICS** > **Resource group** to choose the resource group where the target load balancer will be deployed. You can select **Create new** to create a new resource group for the target internal load balancer or choose the existing resource group that was created previously for the virtual network. Ensure the name isn't the same as the source resource group of the existing source internal load balancer.

16. Verify **BASICS** > **Location** is set to the target location where you wish for the internal load balancer to be deployed.

17. Verify under **SETTINGS** that the name matches the name that you entered in the parameters editor previously. Verify the resource IDs are populated for any virtual networks in the configuration.

18. Check the box under **TERMS AND CONDITIONS**.

19. Select the **Purchase** button to deploy the target virtual network.

### Discard

If you wish to discard the target virtual network and internal load balancer, delete the resource group that contains the target virtual network and internal load balancer. To do so, select the resource group from your dashboard in the portal and select **Delete** at the top of the overview page.

### Clean up

To commit the changes and complete the move of the virtual network and internal load balancer, delete the source virtual network and internal load balancer or resource group. To do so, select the virtual network and internal load balancer or resource group from your dashboard in the portal and select **Delete** at the top of each page.

### Next steps

In this tutorial, you moved an Azure internal load balancer from one region to another and cleaned up the source resources. To learn more about moving resources between regions and disaster recovery in Azure, refer to:

- [Move resources to a new resource group or subscription](../azure-resource-manager/management/move-resource-group-and-subscription.md)

- [Move Azure VMs to another region](../site-recovery/azure-to-azure-tutorial-migrate.md)

# [Azure PowerShell](#tab/azure-powershell/internal-load-balancer)

### Prerequisites

- Make sure that the Azure internal load balancer is in the Azure region from which you want to move.

- Azure internal load balancers can't be moved between regions. You have to associate the new load balancer to resources in the target region.

- To export an internal load balancer configuration and deploy a template to create an internal load balancer in another region, you need the Network Contributor role or higher.

- Identify the source networking layout and all the resources that you're currently using. This layout includes but isn't limited to load balancers, network security groups, virtual machines, and virtual networks.

- Verify that your Azure subscription allows you to create internal load balancers in the target region that's used. Contact support to enable the required quota.

- Make sure that your subscription has enough resources to support the addition of load balancers for this process. See [Azure subscription and service limits, quotas, and constraints](../azure-resource-manager/management/azure-subscription-service-limits.md#azure-networking-limits)

### Prepare and move

The following steps show how to prepare the internal load balancer for the move using a Resource Manager template, and move the internal load balancer configuration to the target region using Azure PowerShell. As part of this process, the virtual network configuration of the internal load balancer must be included and must be done first before moving the internal load balancer.

[!INCLUDE [updated-for-az](~/reusable-content/ce-skilling/azure/includes/updated-for-az.md)]

#### Export the virtual network template and deploy from Azure PowerShell

1. Sign in to your Azure subscription with the [Connect-AzAccount](/powershell/module/az.accounts/connect-azaccount) command and follow the on-screen directions:

```azurepowershell-interactive

Connect-AzAccount

```

2. Obtain the resource ID of the virtual network you want to move to the target region and place it in a variable using [Get-AzVirtualNetwork](/powershell/module/az.network/get-azvirtualnetwork):

```azurepowershell-interactive

$sourceVNETID = (Get-AzVirtualNetwork -Name <source-virtual-network-name> -ResourceGroupName <source-resource-group-name>).Id

```

3. Export the source virtual network to a .json file into the directory where you execute the command [Export-AzResourceGroup](/powershell/module/az.resources/export-azresourcegroup):

```azurepowershell-interactive

Export-AzResourceGroup -ResourceGroupName <source-resource-group-name> -Resource $sourceVNETID -IncludeParameterDefaultValue

```

4. The file downloaded will be named after the resource group the resource was exported from. Locate the file that was exported from the command named **\<resource-group-name>.json** and open it in an editor of your choice:

```azurepowershell

notepad.exe <source-resource-group-name>.json

```

5. To edit the parameter of the virtual network name, change the property **defaultValue** of the source virtual network name to the name of your target virtual network, ensure the name is in quotes:

```json

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentmyResourceGroupVNET.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"virtualNetworks_myVNET1_name": {

"defaultValue": "<target-virtual-network-name>",

"type": "String"

}

```

6. To edit the target region for the virtual network, change the **location** property under resources:

```json

"resources": [

{

"type": "Microsoft.Network/virtualNetworks",

"apiVersion": "2019-06-01",

"name": "[parameters('virtualNetworks_myVNET1_name')]",

"location": "<target-region>",

"properties": {

"provisioningState": "Succeeded",

"resourceGuid": "6e2652be-35ac-4e68-8c70-621b9ec87dcb",

"addressSpace": {

"addressPrefixes": [

"10.0.0.0/16"

]

},

```

7. To obtain region location codes, you can use the Azure PowerShell cmdlet [Get-AzLocation](/powershell/module/az.resources/get-azlocation) by running the following command:

```azurepowershell-interactive

Get-AzLocation | format-table

```

8. You can also change other parameters in the **\<resource-group-name>.json** file if you choose, and are optional depending on your requirements:

* **Address Space** - The address space of the virtual network can be altered before saving by modifying the **resources** > **addressSpace** section and changing the **addressPrefixes** property in the **\<resource-group-name>.json** file:

```json

"resources": [

{

"type": "Microsoft.Network/virtualNetworks",

"apiVersion": "2019-06-01",

"name": "[parameters('virtualNetworks_myVNET1_name')]",

"location": "<target-region",

"properties": {

"provisioningState": "Succeeded",

"resourceGuid": "6e2652be-35ac-4e68-8c70-621b9ec87dcb",

"addressSpace": {

"addressPrefixes": [

"10.0.0.0/16"

]

},

```

* **Subnet** - The subnet name and the subnet address space can be changed or added to by modifying the **subnets** section of the **\<resource-group-name>.json** file. The name of the subnet can be changed by altering the **name** property. The subnet address space can be changed by altering the **addressPrefix** property in the **\<resource-group-name>.json** file:

```json

"subnets": [

{

"name": "subnet-1",

"etag": "W/\"d9f6e6d6-2c15-4f7c-b01f-bed40f748dea\"",

"properties": {

"provisioningState": "Succeeded",

"addressPrefix": "10.0.0.0/24",

"delegations": [],

"privateEndpointNetworkPolicies": "Enabled",

"privateLinkServiceNetworkPolicies": "Enabled"

}

},

{

"name": "GatewaySubnet",

"etag": "W/\"d9f6e6d6-2c15-4f7c-b01f-bed40f748dea\"",

"properties": {

"provisioningState": "Succeeded",

"addressPrefix": "10.0.1.0/29",

"serviceEndpoints": [],

"delegations": [],

"privateEndpointNetworkPolicies": "Enabled",

"privateLinkServiceNetworkPolicies": "Enabled"

}

}

]

```

In the **\<resource-group-name>.json** file, to change the address prefix, it must be edited in two places, the section listed above and the **type** section listed below. Change the **addressPrefix** property to match the one above:

```json

"type": "Microsoft.Network/virtualNetworks/subnets",

"apiVersion": "2019-06-01",

"name": "[concat(parameters('virtualNetworks_myVNET1_name'), '/GatewaySubnet')]",

"dependsOn": [

"[resourceId('Microsoft.Network/virtualNetworks', parameters('virtualNetworks_myVNET1_name'))]"

],

"properties": {

"provisioningState": "Succeeded",

"addressPrefix": "10.0.1.0/29",

"serviceEndpoints": [],

"delegations": [],

"privateEndpointNetworkPolicies": "Enabled",

"privateLinkServiceNetworkPolicies": "Enabled"

}

},

{

"type": "Microsoft.Network/virtualNetworks/subnets",

"apiVersion": "2019-06-01",

"name": "[concat(parameters('virtualNetworks_myVNET1_name'), '/subnet-1')]",

"dependsOn": [

"[resourceId('Microsoft.Network/virtualNetworks', parameters('virtualNetworks_myVNET1_name'))]"

],

"properties": {

"provisioningState": "Succeeded",

"addressPrefix": "10.0.0.0/24",

"delegations": [],

"privateEndpointNetworkPolicies": "Enabled",

"privateLinkServiceNetworkPolicies": "Enabled"

}

}

]

```

9. Save the **\<resource-group-name>.json** file.

10. Create a resource group in the target region for the target virtual network to be deployed using [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup)

```azurepowershell-interactive

New-AzResourceGroup -Name <target-resource-group-name> -location <target-region>

```

11. Deploy the edited **\<resource-group-name>.json** file to the resource group created in the previous step using [New-AzResourceGroupDeployment](/powershell/module/az.resources/new-azresourcegroupdeployment):

```azurepowershell-interactive

New-AzResourceGroupDeployment -ResourceGroupName <target-resource-group-name> -TemplateFile <source-resource-group-name>.json

```

12. To verify the resources were created in the target region, use [Get-AzResourceGroup](/powershell/module/az.resources/get-azresourcegroup) and [Get-AzVirtualNetwork](/powershell/module/az.network/get-azvirtualnetwork):

```azurepowershell-interactive

Get-AzResourceGroup -Name <target-resource-group-name>

```

```azurepowershell-interactive

Get-AzVirtualNetwork -Name <target-virtual-network-name> -ResourceGroupName <target-resource-group-name>

```

#### Export the internal load balancer template and deploy from Azure PowerShell

1. Sign in to your Azure subscription with the [Connect-AzAccount](/powershell/module/az.accounts/connect-azaccount) command and follow the on-screen directions:

```azurepowershell-interactive

Connect-AzAccount

```

2. Obtain the resource ID of the internal load balancer you want to move to the target region and place it in a variable using [Get-AzLoadBalancer](/powershell/module/az.network/get-azloadbalancer):

```azurepowershell-interactive

$sourceIntLBID = (Get-AzLoadBalancer -Name <source-internal-lb-name> -ResourceGroupName <source-resource-group-name>).Id

```

3. Export the source internal load balancer configuration to a .json file into the directory where you execute the command [Export-AzResourceGroup](/powershell/module/az.resources/export-azresourcegroup):

```azurepowershell-interactive

Export-AzResourceGroup -ResourceGroupName <source-resource-group-name> -Resource $sourceIntLBID -IncludeParameterDefaultValue

```

4. The file downloaded will be named after the resource group the resource was exported from. Locate the file that was exported from the command named **\<resource-group-name>.json** and open it in an editor of your choice:

```azurepowershell

notepad.exe <source-resource-group-name>.json

```

5. To edit the parameter of the internal load balancer name, change the property **defaultValue** of the source internal load balancer name to the name of your target internal load balancer, ensure the name is in quotes:

```json

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"loadBalancers_myLoadBalancer_name": {

"defaultValue": "<target-external-lb-name>",

"type": "String"

},

"virtualNetworks_myVNET2_externalid": {

"defaultValue": "<target-vnet-resource-ID>",

"type": "String"

}

```

6. To edit value of the target virtual network that was moved above, you must first obtain the resource ID and then copy and paste it into the **\<resource-group-name>.json** file. To obtain the ID, use [Get-AzVirtualNetwork](/powershell/module/az.network/get-azvirtualnetwork):

```azurepowershell-interactive

$targetVNETID = (Get-AzVirtualNetwork -Name <target-vnet-name> -ResourceGroupName <target-resource-group-name>).Id

```

Type the variable and hit enter to display the resource ID. Highlight the ID path and copy it to the clipboard:

```powershell

PS C:\> $targetVNETID

/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroupVNET-Move/providers/Microsoft.Network/virtualNetworks/myVNET2-Move

```

7. In the **\<resource-group-name>.json** file, paste the **Resource ID** from the variable in place of the **defaultValue** in the second parameter for the target virtual network ID, ensure you enclose the path in quotes:

```json

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"loadBalancers_myLoadBalancer_name": {

"defaultValue": "<target-external-lb-name>",

"type": "String"

},

"virtualNetworks_myVNET2_externalid": {

"defaultValue": "<target-vnet-resource-ID>",

"type": "String"

}

```

8. To edit the target region where the internal load balancer configuration will be moved, change the **location** property under **resources** in the **\<resource-group-name>.json** file:

```json

"resources": [

{

"type": "Microsoft.Network/loadBalancers",

"apiVersion": "2019-06-01",

"name": "[parameters('loadBalancers_myLoadBalancer_name')]",

"location": "<target-internal-lb-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

```

11. To obtain region location codes, you can use the Azure PowerShell cmdlet [Get-AzLocation](/powershell/module/az.resources/get-azlocation) by running the following command:

```azurepowershell-interactive

Get-AzLocation | format-table

```

12. You can also change other parameters in the template if you choose, and are optional depending on your requirements:

* **Sku** - You can change the sku of the internal load balancer in the configuration from standard to basic or basic to standard by altering the **sku** > **name** property in the **\<resource-group-name>.json** file:

```json

"resources": [

{

"type": "Microsoft.Network/loadBalancers",

"apiVersion": "2019-06-01",

"name": "[parameters('loadBalancers_myLoadBalancer_name')]",

"location": "<target-internal-lb-region>",

"sku": {

"name": "Standard",

"tier": "Regional"

},

```

For more information on the differences between basic and standard sku load balancers, see [Azure Standard Load Balancer overview](./load-balancer-overview.md)

* **Availability zone**. You can change the zone(s) of the load balancer's frontend by changing the zone property. If the zone property isn't specified, the frontend is created as zone-redundant.

```json

"frontendIPConfigurations": [

{

"name": "myfrontendIPinbound",

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPinbound')]"

"type": "Microsoft.Network/loadBalancers/frontendIPConfigurations",

"properties": {

"provisioningState": "Succeeded",

"privateIPAddress": "10.0.0.1",

"privateIPAllocationMethod": "Static",

"subnet": {

"id": "[concat(resourceId('Microsoft.Network/virtualNetworks', parameters('virtualNetworks_myVNET1_name')), '/subnet-1')]"

},

"privateIPAddressVersion": "IPv4"

},

"zones": [

"1",

"2",

"3"

]

}

],

```

* **Load balancing rules** - You can add or remove load balancing rules in the configuration by adding or removing entries to the **loadBalancingRules** section of the **\<resource-group-name>.json** file:

```json

"loadBalancingRules": [

{

"name": "myInboundRule",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"properties": {

"provisioningState": "Succeeded",

"frontendIPConfiguration": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPinbound')]"

},

"frontendPort": 80,

"backendPort": 80,

"enableFloatingIP": false,

"idleTimeoutInMinutes": 4,

"protocol": "Tcp",

"enableTcpReset": false,

"loadDistribution": "Default",

"disableOutboundSnat": true,

"backendAddressPool": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/backendAddressPools/myBEPoolInbound')]"

},

"probe": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/probes/myHTTPProbe')]"

}

}

}

]

```

For more information on load balancing rules, see [What is Azure Load Balancer?](./load-balancer-overview.md)

* **Probes** - You can add or remove a probe for the load balancer in the configuration by adding or removing entries to the **probes** section of the **\<resource-group-name>.json** file:

```json

"probes": [

{

"name": "myHTTPProbe",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"properties": {

"provisioningState": "Succeeded",

"protocol": "Http",

"port": 80,

"requestPath": "/",

"intervalInSeconds": 15,

"numberOfProbes": 2

}

}

],

```

For more information on Azure Load Balancer health probes, see [Load Balancer health probes](./load-balancer-custom-probe-overview.md)

* **Inbound NAT rules** - You can add or remove inbound NAT rules for the load balancer by adding or removing entries to the **inboundNatRules** section of the **\<resource-group-name>.json** file:

```json

"inboundNatRules": [

{

"name": "myInboundNATRule",

"etag": "W/\"39e5e9cd-2d6d-491f-83cf-b37a259d86b6\"",

"properties": {

"provisioningState": "Succeeded",

"frontendIPConfiguration": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPinbound')]"

},

"frontendPort": 4422,

"backendPort": 3389,

"enableFloatingIP": false,

"idleTimeoutInMinutes": 4,

"protocol": "Tcp",

"enableTcpReset": false

}

}

]

```

To complete the addition or removal of an inbound NAT rule, the rule must be present or removed as a **type** property at the end of the **\<resource-group-name>.json** file:

```json

{

"type": "Microsoft.Network/loadBalancers/inboundNatRules",

"apiVersion": "2019-06-01",

"name": "[concat(parameters('loadBalancers_myLoadBalancer_name'), '/myInboundNATRule')]",

"dependsOn": [

"[resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name'))]"

],

"properties": {

"provisioningState": "Succeeded",

"frontendIPConfiguration": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', parameters('loadBalancers_myLoadBalancer_name')), '/frontendIPConfigurations/myfrontendIPinbound')]"

},

"frontendPort": 4422,

"backendPort": 3389,

"enableFloatingIP": false,

"idleTimeoutInMinutes": 4,

"protocol": "Tcp",

"enableTcpReset": false

}

}

```

For more information on inbound NAT rules, see [What is Azure Load Balancer?](./load-balancer-overview.md)

13. Save the **\<resource-group-name>.json** file.

10. Create or a resource group in the target region for the target internal load balancer to be deployed using [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup). The existing resource group from above can also be reused as part of this process:

```azurepowershell-interactive

New-AzResourceGroup -Name <target-resource-group-name> -location <target-region>

```

11. Deploy the edited **\<resource-group-name>.json** file to the resource group created in the previous step using [New-AzResourceGroupDeployment](/powershell/module/az.resources/new-azresourcegroupdeployment):

```azurepowershell-interactive

New-AzResourceGroupDeployment -ResourceGroupName <target-resource-group-name> -TemplateFile <source-resource-group-name>.json

```

12. To verify the resources were created in the target region, use [Get-AzResourceGroup](/powershell/module/az.resources/get-azresourcegroup) and [Get-AzLoadBalancer](/powershell/module/az.network/get-azloadbalancer):

```azurepowershell-interactive

Get-AzResourceGroup -Name <target-resource-group-name>

```

```azurepowershell-interactive

Get-AzLoadBalancer -Name <target-publicip-name> -ResourceGroupName <target-resource-group-name>

```

### Discard

After the deployment, if you wish to start over or discard the virtual network and load balancer in the target, delete the resource group that was created in the target and the moved virtual network and load balancer will be deleted. To remove the resource group, use [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup):

```azurepowershell-interactive

Remove-AzResourceGroup -Name <resource-group-name>

```

### Clean up

To commit the changes and complete the move of the NSG, delete the source NSG or resource group, use [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) or [Remove-AzVirtualNetwork](/powershell/module/az.network/remove-azvirtualnetwork) and [Remove-AzLoadBalancer](/powershell/module/az.network/remove-azloadbalancer)

```azurepowershell-interactive

Remove-AzResourceGroup -Name <resource-group-name>

```

``` azurepowershell-interactive

Remove-AzLoadBalancer -name <load-balancer> -ResourceGroupName <resource-group-name>

Remove-AzVirtualNetwork -Name <virtual-network-name> -ResourceGroupName <resource-group-name>

```

### Next steps

In this tutorial, you moved an Azure internal load balancer from one region to another and cleaned up the source resources. To learn more about moving resources between regions and disaster recovery in Azure, refer to:

- [Move resources to a new resource group or subscription](../azure-resource-manager/management/move-resource-group-and-subscription.md)

- [Move Azure VMs to another region](../site-recovery/azure-to-azure-tutorial-migrate.md)

---


# Secure Load Balancer

# Secure your Azure Load Balancer deployment

Azure Load Balancer provides Layer 4 load balancing capabilities to distribute incoming and outbound traffic among healthy backend instances. Because Load Balancer operates at the transport layer, you must combine it with network controls, identity controls, monitoring, and workload-level encryption to secure the full deployment.

This article provides security recommendations for Azure Load Balancer. Implementing these recommendations helps you fulfill your security obligations and improves the overall security posture of your deployment. For an overview of Azure's network security services and how they work together, see [What is Azure network security?](../networking/security/network-security.md).

[!INCLUDE [Security horizontal Zero Trust statement](~/reusable-content/ce-skilling/azure/includes/security/zero-trust-security-horizontal.md)]

> [!IMPORTANT]

> Basic Load Balancer was retired on September 30, 2025. Existing Basic Load Balancers remain operational but are unsupported and not covered by SLA guarantees. Upgrade to Standard Load Balancer as soon as possible. For more information, see [Upgrading from Basic Load Balancer - Guidance](load-balancer-basic-upgrade-guidance.md).

## Network security

Network security for Azure Load Balancer focuses on limiting inbound exposure, controlling outbound connectivity, validating backend health, and integrating with other Azure network security services.

- **Use Standard Load Balancer SKU**: Deploy Standard Load Balancer for production workloads. Standard Load Balancer follows a secure-by-default model with closed inbound connections, supports availability zones, and provides a 99.99% SLA. Basic Load Balancer was retired on September 30, 2025, and shouldn't be used for new deployments. For more information, see [Azure Load Balancer overview](load-balancer-overview.md).

- **Implement network security groups on subnets and network interfaces**: Apply network security groups (NSGs) to backend subnets and network interfaces to explicitly permit only required ports, protocols, and source IP ranges. Standard Load Balancer doesn't allow inbound flows until an NSG explicitly permits the traffic. For more information, see [Azure Load Balancer security baseline](/security/benchmark/azure/baselines/azure-load-balancer-security-baseline#network-security).

- **Allow Azure Load Balancer health probe traffic**: Ensure that NSGs, user-defined routes, and local firewall policies allow health probe traffic from IP address 168.63.129.16. Blocked probes cause healthy backend instances to be removed from rotation and can create avoidable outages. For more information, see [Azure Load Balancer health probes](load-balancer-custom-probe-overview.md).

- **Use internal load balancer for private workloads**: Deploy an internal load balancer with private frontend IP addresses when the service doesn't need direct internet exposure. Use virtual network peering, VPN, ExpressRoute, Azure Firewall, or private access patterns to control who can reach the frontend. For more information, see [Azure Load Balancer components](components.md#frontend-ip-configurations).

- **Protect public load balancers with Azure DDoS Protection**: Enable Azure DDoS Network Protection on the virtual network that hosts public load balancers. DDoS Protection provides enhanced DDoS mitigation and detection capabilities that monitor endpoints for threats and signs of abuse. For more information, see [Protect your public load balancer with Azure DDoS Protection](tutorial-protect-load-balancer-ddos.md).

- **Use explicit outbound connectivity**: Don't rely on default outbound access. Default outbound access retired on September 30, 2025, so use Azure NAT Gateway for predictable outbound IP addresses, or configure explicit Standard Load Balancer outbound rules when NAT Gateway isn't appropriate. For more information, see [Outbound connections in Azure](load-balancer-outbound-connections.md) and [Azure NAT Gateway overview](../nat-gateway/nat-overview.md).

- **Configure appropriate distribution mode**: Select the distribution mode that fits your application and security requirements. Use the default 5-tuple hash for most workloads, and use session persistence only when the application requires it because persistence can create uneven distribution and reduce resiliency. For more information, see [Azure Load Balancer distribution modes](distribution-mode-concepts.md).

- **Enable TCP reset for clearer connection handling**: Configure TCP reset on load-balancing rules so clients and backend applications receive bidirectional TCP reset packets on idle timeout. Clear connection state helps applications recover faster and reduces ambiguous half-open connections. For more information, see [Azure Load Balancer best practices](load-balancer-best-practices.md#enable-tcp-resets).

- **Secure floating IP and Gateway Load Balancer designs**: When you use floating IP for high-availability scenarios, configure loopback interfaces correctly and apply host firewall controls. For Gateway Load Balancer and network virtual appliances, separate trusted and untrusted traffic on different tunnel interfaces and account for VXLAN header overhead. For more information, see [Azure Load Balancer best practices](load-balancer-best-practices.md).

- **Integrate inspection services when needed**: Azure Load Balancer is a Layer 4 service and doesn't inspect application payloads. Route traffic through Azure Firewall, network virtual appliances, Application Gateway, or Azure Front Door when you need firewalling, web application firewall, or Layer 7 inspection. For more information, see [Architecture best practices for Azure Load Balancer](/azure/well-architected/service-guides/azure-load-balancer#security).

## Identity and access management

Identity and access management for Azure Load Balancer controls who can create, update, delete, and review load balancer resources, rules, probes, frontend IPs, backend pools, and outbound connectivity.

- **Use Microsoft Entra ID for management-plane access**: Require administrators to authenticate with Microsoft Entra ID when using the Azure portal, Azure CLI, Azure PowerShell, or Azure Resource Manager APIs. Apply Conditional Access controls such as multifactor authentication, compliant device requirements, and sign-in risk policies for privileged networking roles. For more information, see [Microsoft Entra Conditional Access](/entra/identity/conditional-access/overview).

- **Implement Azure role-based access control**: Assign Azure RBAC roles to users, groups, managed identities, and automation accounts that manage load balancers. Use built-in roles such as Network Contributor only where the full network-management scope is required. For more information, see [What is Azure role-based access control?](../role-based-access-control/overview.md).

- **Use least privilege access**: Avoid broad Owner or Contributor assignments for routine load balancer operations. Create custom roles when operators need only specific permissions for load balancer read, write, rule, probe, or backend pool operations. For more information, see [Azure custom roles](../role-based-access-control/custom-roles.md).

- **Use Privileged Identity Management for elevated access**: Make high-impact roles eligible instead of permanently assigned by using Microsoft Entra Privileged Identity Management (PIM). Require approval, multifactor authentication, justification, and time-bound activation for roles that can change production load balancers. For more information, see [What is Microsoft Entra Privileged Identity Management?](/entra/id-governance/privileged-identity-management/pim-configure).

- **Separate duties for networking and workload teams**: Limit who can change load-balancing rules, inbound NAT rules, outbound rules, backend pool membership, and probe settings. Separation of duties reduces the risk that a single compromised identity can both expose a service and change the workload behind it. For more information, see [Azure RBAC best practices](../role-based-access-control/best-practices.md).

- **Audit management-plane changes**: Monitor Azure Activity Log events for load balancer configuration changes, role assignments, and diagnostic setting changes. Alert on unexpected updates to frontend IP configurations, rule mappings, outbound rules, or backend pool membership. For more information, see [Monitor Azure Load Balancer](monitor-load-balancer.md).

## Data protection

Data protection for Azure Load Balancer focuses on protecting traffic handled by backend workloads and protecting configuration and telemetry because Load Balancer doesn't store customer application data.

- **Encrypt application traffic end to end**: Azure Load Balancer operates at Layer 4 and doesn't terminate TLS or inspect payloads. Configure TLS on the backend application or on a Layer 7 service in front of the backend so traffic remains encrypted where required. For more information, see [Architecture best practices for Azure Load Balancer](/azure/well-architected/service-guides/azure-load-balancer#security).

- **Use the right service for TLS termination**: If your HTTP or HTTPS workload requires TLS termination, certificate management, URL routing, or web application firewall inspection, use Azure Application Gateway or Azure Front Door instead of relying on Load Balancer for those functions. For more information, see [Azure Load Balancer overview](load-balancer-overview.md).

- **Protect backend secrets and certificates**: Store TLS certificates, private keys, and application secrets used by backend instances in Azure Key Vault. Use managed identities for backend workloads instead of embedding secrets in scripts, templates, or VM extensions. For more information, see [Azure Key Vault overview](/azure/key-vault/general/overview).

- **Secure diagnostic data destinations**: Load balancer metrics, flow logs, and archived diagnostics can include IP addresses, ports, and topology details. Restrict access to Log Analytics workspaces, storage accounts, and Event Hubs that receive diagnostics, and use customer-managed keys for storage accounts when your compliance requirements call for them. For more information, see [Azure Storage encryption](../storage/common/storage-service-encryption.md).

- **Avoid exposing sensitive topology in names and tags**: Don't include secrets, internal project names, or sensitive network details in load balancer names, rule names, public IP DNS labels, or resource tags. These values can appear in logs, exports, alerts, and access reviews. For more information, see [Naming rules and restrictions for Azure resources](../azure-resource-manager/management/resource-name-rules.md).

## Logging and monitoring

Logging and monitoring for Azure Load Balancer provides visibility into availability, health probes, traffic patterns, and configuration changes so teams can detect security and reliability issues quickly.

- **Enable diagnostic settings**: Configure diagnostic settings to send load balancer metrics and supported logs to a Log Analytics workspace, storage account, or Event Hubs for analysis and retention. For more information, see [Monitor Azure Load Balancer](monitor-load-balancer.md#creating-a-diagnostic-setting).

- **Use Azure Monitor Insights**: Deploy Load Balancer Insights to view preconfigured dashboards, functional dependency diagrams, resource health, and metrics for proactive monitoring. For more information, see [Use Insights to monitor and configure Azure Load Balancer](load-balancer-insights.md).

- **Configure health probe monitoring**: Implement health probes that accurately represent application readiness, not just host availability. Monitor probe status so backend failures, firewall blocks, and application outages are detected before users are affected. For more information, see [Manage health probes for Azure Load Balancer](manage-probes-how-to.md).

- **Monitor connection and availability metrics**: Track metrics such as Data Path Availability, Health Probe Status, SYN Count, SNAT Connection Count, and Allocated SNAT Ports. Use alerts to identify failed backends, anomalous connection spikes, or outbound port exhaustion. For more information, see [Standard Load Balancer diagnostics with metrics, alerts, and resource health](load-balancer-standard-diagnostics.md#multi-dimensional-metrics).

- **Enable virtual network flow logs**: Configure virtual network flow logs to analyze traffic patterns around backend subnets and identify suspicious or unexpected flows. Forward logs to your security information and event management (SIEM) system for correlation with workload and identity events. For more information, see [Monitor Azure Load Balancer](monitor-load-balancer.md#analyzing-load-balancer-traffic-with-vnet-flow-logs).

- **Set up security and operations alerts**: Create Azure Monitor alerts for failed health probes, low data path availability, unusual traffic increases, SNAT exhaustion indicators, and unexpected Activity Log changes. Include runbook links and owner information in alert actions. For more information, see [Monitor Azure Load Balancer](monitor-load-balancer.md).

## Compliance and governance

Compliance and governance for Azure Load Balancer helps ensure consistent, supportable, and auditable configurations across subscriptions, regions, and environments.

- **Implement Azure Policy controls**: Use Azure Policy to audit and enforce load balancer requirements such as Standard SKU usage, diagnostic settings, tagging, and NSG associations on backend subnets. For more information, see [Azure Load Balancer security baseline](/security/benchmark/azure/baselines/azure-load-balancer-security-baseline#asset-management).

- **Standardize deployment with infrastructure as code**: Deploy load balancers, public IPs, rules, probes, backend pools, and outbound configurations with ARM templates, Bicep, or other approved infrastructure-as-code pipelines. Version-controlled templates reduce drift and provide evidence for compliance reviews. For more information, see [Create a public load balancer using Bicep](quickstart-load-balancer-standard-public-bicep.md) and [Create a public load balancer using an ARM template](quickstart-load-balancer-standard-public-template.md).

- **Use resource tagging**: Apply consistent tags for workload owner, data classification, environment, business criticality, and disaster recovery tier. Tags support cost management, compliance tracking, incident routing, and ownership reviews. For more information, see [Azure resource naming and tagging decision guide](/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming-and-tagging-decision-guide).

- **Review unsupported and legacy configurations**: Inventory Basic Load Balancers, implicit outbound dependencies, unmanaged public IPs, and missing diagnostics. Prioritize migration to Standard Load Balancer, NAT Gateway or explicit outbound rules, and monitored configurations. For more information, see [Upgrade from Basic to Standard Load Balancer](load-balancer-basic-upgrade-guidance.md).

- **Control changes through approved workflows**: Require change review for frontend IPs, inbound rules, NAT rules, outbound rules, backend pool membership, probe paths, and idle timeout settings. Use Azure Activity Log and deployment history to validate that changes came from approved identities and pipelines. For more information, see [Azure Resource Manager deployment history](../azure-resource-manager/templates/deployment-history.md).

## Backup and recovery

Backup and recovery for Azure Load Balancer focuses on preserving the configuration, documenting dependencies, and designing resilient topologies that keep traffic flowing during instance, zone, or regional failures.

- **Export and version the load balancer configuration**: Export the Standard Load Balancer configuration as an ARM template or Bicep file and store it in source control. Capture frontend IP configurations, public IP resources, backend pools, load-balancing rules, inbound NAT rules, outbound rules, health probes, and dependencies so you can restore or recreate the deployment quickly. For more information, see [Export templates in the Azure portal](../azure-resource-manager/templates/export-template-portal.md) and [Export templates with Azure CLI](../azure-resource-manager/templates/export-template-cli.md).

- **Document the topology before changes**: Record frontend IP addresses, DNS names, backend pool members, rule-to-probe mappings, NAT mappings, outbound connectivity design, NSG dependencies, route tables, and owning teams before planned changes. Current documentation reduces recovery time when a rollback or regional rebuild is needed. For more information, see [Azure Load Balancer components](components.md).

- **Use cross-region load balancer for multi-region failover**: Deploy Cross-region Load Balancer, also known as Global Load Balancer, when you need a single global frontend that distributes traffic across regional load balancers. Pair it with regional health monitoring and tested failover procedures. For more information, see [Cross-region load balancer](cross-region-overview.md) and [Deploy a cross-region load balancer using an ARM template](tutorial-deploy-cross-region-load-balancer-template.md).

- **Use zone-redundant frontends for availability zone resilience**: Use Standard Load Balancer with zone-redundant frontend IP configurations where availability zones are supported. Standard SKU includes built-in support for zone redundancy, and a zone-redundant frontend helps keep the data path available if a zone fails. For more information, see [Azure Load Balancer best practices](load-balancer-best-practices.md#architectural-best-practices).

- **Distribute backend pools across zones**: Place backend instances in multiple availability zones by using Virtual Machine Scale Sets or zonal virtual machines. Zone-redundant backend pools reduce the chance that a single zone failure removes all healthy instances from rotation. For more information, see [Migrate Load Balancer to availability zone support](/azure/reliability/migrate-load-balancer).

- **Configure health probes for automatic in-region failover**: Health probes determine which backend instances receive traffic. Configure probes against application-ready endpoints, choose appropriate intervals and thresholds, and test probe behavior during maintenance so traffic automatically fails over to healthy instances within the region. For more information, see [Manage health probes for Azure Load Balancer](manage-probes-how-to.md).

- **Test failover regularly**: Exercise instance, zone, and regional failover scenarios on a defined schedule. Validate that probes remove unhealthy instances, Cross-region Load Balancer or DNS routing sends traffic to the secondary region, outbound connectivity still works, and monitoring alerts reach the right responders. For more information, see [Azure Load Balancer best practices](load-balancer-best-practices.md).

## Next steps

- [Azure Load Balancer security baseline](/security/benchmark/azure/baselines/azure-load-balancer-security-baseline)

- [What is Azure network security?](../networking/security/network-security.md)


# Inbound Nat Rules

# Inbound NAT rules

An inbound NAT rule is used to forward traffic from a load balancer frontend to one or more instances in the backend pool.

## Why use an inbound NAT rule?

An inbound NAT rule is used for port forwarding. Port forwarding lets you connect to virtual machines by using the load balancer frontend IP address and port number. The load balancer receives the traffic on a port, and based on the inbound NAT rule, forwards the traffic to a designated virtual machine on a specific backend port. Note, unlike load balancing rules, inbound NAT rules don't need a health probe attached to it.

## Types of inbound NAT rules

There are two types of inbound NAT rule available for Azure Load Balancer, version 1 and version 2.

> [!NOTE]

> The recommendation is to use Inbound NAT rule V2 for Standard Load Balancer deployments targeting multiple virtual machines or virtual machine scale sets. For single virtual machine port, Inbound NAT rule V1 continues to be fully supported.

### Inbound NAT rule V2

An inbound NAT rule targeting multiple virtual machines references the entire backend pool. A range of frontend ports are preallocated based on the rule settings of **Frontend port range start** and **Maximum number of machines in the backend pool**.

During inbound port rule creation, port mappings are made to the backend pool from the preallocated range that's defined in the rule.

When the backend pool is scaled down, existing port mappings for the remaining virtual machines persist. When the backend pool is scaled up, new port mappings are created automatically for the new virtual machines added to the backend pool. An update to the inbound NAT rule settings isn't required.

> [!NOTE]

> If the predefined frontend port range doesn't have a sufficient number of frontend ports available, scaling up the backend pool is blocked. This blockage could result in a lack of network connectivity for the new instances.

### Inbound NAT rule V1 - single virtual machine

Inbound NAT rule V1 for a single virtual machine provides a 1:1 port mapping between a load balancer frontend IP/port and a specific backend virtual machine. This is used for scenarios such as SSH or RDP access to individual VMs through the load balancer.

### Inbound NAT Pools (Azure Virtual Machine Scale Sets) — Retiring September 30, 2027

Inbound NAT Pools are a feature of Inbound NAT rules V1 that automatically create Inbound NAT rules per Azure Virtual Machine Scale Set instance. The load balancer's frontend IP address and a range of frontend ports are used to map connections to individual Virtual Machine Scale Sets instances.

> [!IMPORTANT]

> On September 30, 2027, **Inbound NAT Pools** (the  Virtual Machine Scale Sets-specific feature of Inbound NAT rules V1) will be retired and starting November 15, 2026, you will not be able to create new Inbound NAT Pools. If you are currently using Inbound NAT Pools with Virtual Machine Scale Sets, upgrade to Inbound NAT rules V2 prior to the retirement date. **Single VM Inbound NAT rules V1 are not affected by this retirement.**

## Port mapping retrieval

You can use the portal to retrieve the port mappings for virtual machines in the backend pool. For more information, see [Manage inbound NAT rules](manage-inbound-nat-rules.md#view-port-mappings).

## Next steps

For more information about Azure Load Balancer inbound NAT rules, see:

- [Manage inbound NAT rules](manage-inbound-nat-rules.md)

- [Tutorial: Create a multiple virtual machines inbound NAT rule using the Azure portal](tutorial-nat-rule-multi-instance-portal.md)

- [Tutorial: Create a single virtual machine inbound NAT rule using the Azure portal](tutorial-load-balancer-port-forwarding-portal.md)

- [Tutorial: Migrate from Inbound NAT Pools to NAT Rules](load-balancer-nat-pool-migration.md)


# Tutorial Load Balancer Port Forwarding Portal

# Tutorial: Create a single virtual machine inbound NAT rule using the Azure portal

Inbound NAT rules allow you to connect to virtual machines (VMs) in an Azure virtual network by using an Azure Load Balancer public IP address and port number.

For more information about Azure Load Balancer rules, see [Manage rules for Azure Load Balancer using the Azure portal](manage-rules-how-to.md).

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a virtual network and virtual machines

> * Create a standard SKU public load balancer with frontend IP, health probe, backend configuration, load-balancing rule, and inbound NAT rules

> * Create a NAT gateway for outbound internet access for the backend pool

> * Install and configure a web server on the VMs to demonstrate the port forwarding and load-balancing rules

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Sign in to Azure

Sign in to the [Azure portal](https://portal.azure.com).

[!INCLUDE [load-balancer-create-vnet-vm](../../includes/load-balancer-create-vnet-vm.md)]

## Create a load balancer

You create a load balancer in this section. The frontend IP, backend pool, load-balancing, and inbound NAT rules are configured as part of the creation.

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

1. In the **Load balancer** page, select **Create**.

1. In the **Basics** tab of the **Create load balancer** page, enter, or select the following information:

| Setting                 | Value                                              |

| ---                     | ---                                                |

| **Project details** |   |

| Subscription               | Select your subscription.    |

| Resource group         | Select **load-balancer-rg**. |

| **Instance details** |   |

| Name                   | Enter *load-balancer*                                   |

| Region         | Select **East US**.                                        |

| SKU           | Leave the default **Standard**. |

| Type          | Select **Public**.                                        |

| Tier          | Leave the default **Regional**. |

1. Select **Next: Frontend IP configuration** at the bottom of the page.

1. In **Frontend IP configuration**, select **+ Add a frontend IP configuration**.

1. Enter *lb-frontend* in **Name**.

1. Select **IPv4** or **IPv6** for the **IP version**.

> [!NOTE]

> IPv6 isn't currently supported with Routing Preference or Cross-region load-balancing (Global Tier).

1. Select **IP address** for the **IP type**.

> [!NOTE]

> For more information on IP prefixes, see [Azure Public IP address prefix](../virtual-network/ip-services/public-ip-address-prefix.md).

1. Select **Create new** in **Public IP address**.

1. In **Add a public IP address**, enter *lb-frontend-ip* for **Name**.

1. Select **Zone-redundant** in **Availability zone**.

> [!NOTE]

> In regions with [Availability Zones](/azure/reliability/availability-zones-overview?toc=%2fazure%2fvirtual-network%2ftoc.json), you can select zone-redundant (default option) or a specific zone. The choice depends on your specific domain failure requirements. In regions without Availability Zones, this field won't appear. </br> For more information on availability zones, see [Availability zones overview](/azure/reliability/availability-zones-overview).

1. Leave the default of **Microsoft Network** for **Routing preference**.

1. Select **OK**.

1. Select **Add**.

1. Select **Next: Backend pools** at the bottom of the page.

1. In the **Backend pools** tab, select **+ Add a backend pool**.

1. Enter or select the following information in **Add backend pool**.

| Setting | Value |

| ------- | ----- |

| Name | Enter *lb-backend-pool*. |

| Virtual network | Select **lb-vnet (load-balancer-rg)**. |

| Backend Pool Configuration | Select **NIC**. |

1. Select **+ Add** in **Virtual machines**.

1. Select the checkboxes next to **lb-vm1** and **lb-vm2** in **Add virtual machines to backend pool**.

1. Select **Add** and then select **Save**.

1. Select the **Next: Inbound rules** button at the bottom of the page.

1. In **Load balancing rule** in the **Inbound rules** tab, select **+ Add a load balancing rule**.

1. In **Add load balancing rule**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| Name | Enter *lb-HTTP-rule* |

| IP Version | Select **IPv4** or **IPv6** depending on your requirements. |

| Frontend IP address | Select **lb-frontend (To be created)**. |

| Backend pool | Select **lb-backend-pool**. |

| Protocol | Select **TCP**. |

| Port | Enter *80*. |

| Backend port | Enter *80*. |

| Health probe | Select **Create new**. </br> In **Name**, enter *lb-health-probe*. </br> Select **TCP** in **Protocol**. </br> Leave the rest of the defaults, and select **Save**. |

| Session persistence | Select **None**. |

| Idle timeout (minutes) | Enter or select **15**. |

| Enable TCP reset | Select **checkbox** to enable. |

| Enable Floating IP | Leave the default of unchecked. |

| Outbound source network address translation (SNAT) | Leave the default of **(Recommended) Use outbound rules to provide backend pool members access to the internet.** |

For more information about load-balancing rules, see [Load-balancing rules](manage-rules-how-to.md#load-balancing-rules).

1. Select **Save**.

1. In **Inbound NAT rule** in the **Inbound rules** tab, select **+ Add an inbound nat rule**.

1. In **Add inbound NAT rule**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| Name | Enter *lb-NAT-rule-VM1-221*. |

| Target virtual machine | Select **lb-vm1**. |

| Network IP configuration | Select **ipconfig1 (10.0.0.4)**. |

| Frontend IP address | Select **lb-frontend (To be created)**. |

| Frontend Port | Enter *221*. |

| Service Tag | Select **Custom**. |

| Backend port | Enter *22*. |

| Protocol | Leave the default of **TCP**. |

| Enable TCP Reset | Leave the default of unchecked. |

| Idle timeout (minutes) | Leave the default **4**. |

| Enable Floating IP | Leave the default of unchecked. |

2. Select **Add**.

3. Select **+ Add an inbound nat rule**.

4. In **Add inbound NAT rule**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| Name | Enter *lb-NAT-rule-VM2-222*. |

| Target virtual machine | Select **lb-vm2**. |

| Network IP configuration | Select **ipconfig1 (10.0.0.5)**. |

| Frontend IP address | Select **lb-frontend**. |

| Frontend Port | Enter *222*. |

| Service Tag | Select **Custom**. |

| Backend port | Enter *22*. |

| Protocol | Leave the default of **TCP**. |

| Enable TCP Reset | Leave the default of unchecked. |

| Idle timeout (minutes) | Leave the default **4**. |

| Enable Floating IP | Leave the default of unchecked. |

5. Select **Add**.

6. Select the blue **Review + create** button at the bottom of the page.

7. Select **Create**.

## Create a NAT gateway

In this section, you create a NAT gateway for outbound internet access for resources in the virtual network.

For more information about outbound connections and Azure Virtual Network NAT, see [Using Source Network Address Translation (SNAT) for outbound connections](load-balancer-outbound-connections.md) and [What is Virtual Network NAT?](../virtual-network/nat-gateway/nat-overview.md)

1. In the search box at the top of the portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. In **NAT gateways**, select **+ Create**.

1. In **Create network address translation (NAT) gateway**, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **load-balancer-rg**. |

| **Instance details** |    |

| NAT gateway name | Enter *lb-nat-gateway*. |

| Region | Select **East US**. |

| Availability zone | Select **None**. |

| Idle timeout (minutes) | Enter *15*. |

1. Select the **Outbound IP** tab or select the **Next: Outbound IP** button at the bottom of the page.

1. In **Outbound IP**, select **Create a new public IP address** next to **Public IP addresses**.

1. Enter *nat-gw-public-ip* in **Name** in **Add a public IP address**.

1. Select **OK**.

1. Select the **Subnet** tab or select the **Next: Subnet** button at the bottom of the page.

1. In **Virtual network** in the **Subnet** tab, select **lb-vnet**.

1. Select **backend-subnet** under **Subnet name**.

1. Select the blue **Review + create** button at the bottom of the page, or select the **Review + create** tab.

1. Select **Create**.

## Install web server

In this section, you'll SSH to the virtual machines through the inbound NAT rules and install a web server.

1. In the search box at the top of the portal, enter *Load balancer*. Select **Load balancers** in the search results.

1. Select **load-balancer**.

1. Select **Fronted IP configuration** in **Settings**.

1. In the **Frontend IP configuration**, make note of the **IP address** for **lb-frontend**. In this example, it's **20.99.165.176**.

1. If you're using a Mac or Linux computer, open a Bash prompt. If you're using a Windows computer, open a PowerShell prompt.

1. At your prompt, open an SSH connection to **lb-vm1**. Replace the IP address with the address you retrieved in the previous step and port **221** you used for the lb-vm1 inbound NAT rule. Replace the path to the .pem with the path to where the key file was downloaded.

```console

ssh -i .\Downloads\lb-key-pair.pem azureuser@20.99.165.176 -p 221

```

> [!TIP]

> The SSH key you created can be used the next time your create a VM in Azure. Just select the **Use a key stored in Azure** for **SSH public key source** the next time you create a VM. You already have the private key on your computer, so you won't need to download anything.

1. From your SSH session, update your package sources and then install the latest NGINX package.

```bash

sudo apt-get -y update

sudo apt-get -y install nginx

```

1. Enter `Exit` to leave the SSH session

1. At your prompt, open an SSH connection to **lb-vm2**. Replace the IP address with the address you retrieved in the previous step and port **222** you used for the lb-vm2 inbound NAT rule. Replace the path to the .pem with the path to where the key file was downloaded.

```console

ssh -i .\Downloads\lb-key-pair.pem azureuser@20.99.165.176 -p 222

```

1. From your SSH session, update your package sources and then install the latest NGINX package.

```bash

sudo apt-get -y update

sudo apt-get -y install nginx

```

1. Enter `Exit` to leave the SSH session.

## Test the web server

In this section you test the web server by using the public IP address for the load balancer.

1. Open your web browser.

1. In the address bar, enter the IP address for the load balancer. In this example, it's **20.99.165.176**.

1. The default NGINX website is displayed.

## Clean up resources

If you're not going to continue to use this application, delete the virtual machines and load balancer with the following steps:

1. In the search box at the top of the portal, enter **Resource group**.  Select **Resource groups** in the search results.

1. Select **load-balancer-rg** in **Resource groups**.

1. Select **Delete resource group**.

1. Enter *load-balancer-rg* in **TYPE THE RESOURCE GROUP NAME:**. Select **Delete**.

## Next steps

Advance to the next article to learn how to create a cross-region load balancer:

> [!div class="nextstepaction"]

> [Create a multiple virtual machines inbound NAT rule using the Azure portal](tutorial-nat-rule-multi-instance-portal.md)


# Tutorial Nat Rule Multi Instance Portal

# Tutorial: Create inbound NAT rule V2 using the Azure portal

Inbound NAT rules allow you to connect to virtual machines (VMs) in an Azure virtual network by using an Azure Load Balancer public IP address and port number.

For more information about Azure Load Balancer rules, see [Manage rules for Azure Load Balancer using the Azure portal](manage-rules-how-to.md).

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a virtual network and virtual machines

> * Create a standard SKU public load balancer with frontend IP, health probe, backend configuration, and load-balancing rule

> * Create a multiple VMs inbound NAT rule

> * Create a NAT gateway for outbound internet access for the backend pool

> * Install and configure a web server on the VMs to demonstrate the port forwarding and load-balancing rules

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Create virtual network and virtual machines

A virtual network and subnet is required for the resources in the tutorial. In this section, you create a virtual network and virtual machines for the later steps.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

3. In **Virtual machines**, select **+ Create** > **+ Virtual machine**.

4. In **Create a virtual machine**, enter or select the following values in the **Basics** tab:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **Create new**. </br> Enter **TutorialLBPF-rg**. </br> Select **OK**. |

| **Instance details** |    |

| Virtual machine name | Enter **myVM1**. |

| Region | Enter **(US) West US 2**. |

| Availability options | Select **Availability zone**. |

| Availability zone | Enter **1**. |

| Security type | Select **Standard**. |

| Image | Select **Ubuntu Server 20.04 LTS - Gen2**. |

| Azure Spot instance | Leave the default of unchecked. |

| Size | Select a VM size. |

| **Administrator account** |    |

| Authentication type | Select **SSH public key**. |

| Username | Enter **azureuser**. |

| SSH public key source | Select **Generate new key pair**. |

| Key pair name | Enter **myKey**. |

| **Inbound port rules** |    |

| Public inbound ports | Select **None**. |

5. Select the **Networking** tab, or select **Next: Disks**, then **Next: Networking**.

6. In the **Networking** tab, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| **Network interface** |   |

| Virtual network | Select **Create new**. </br> Enter **myVNet** in **Name**. </br> In **Address space**, under **Address range**, enter **10.1.0.0/16**. </br> In **Subnets**, under **Subnet name**, enter **myBackendSubnet**. </br> In **Address range**, enter **10.1.0.0/24**. </br> Select **OK**. |

| Subnet | Select **myBackendSubnet**. |

| Public IP | Select **None**. |

| NIC network security group | Select **Advanced**. |

| Configure network security group | Select **Create new**. </br> Enter **myNSG** in **Name**. </br> Select **+ Add an inbound rule** under **Inbound rules**. </br> In **Service**, select **HTTP**. </br> Enter **100** in **Priority**. </br> Enter **myNSGRule** for **Name**. </br> Select **Add**. </br> Select **OK**. |

7. Select the **Review + create** tab, or select the **Review + create** button at the bottom of the page.

8. Select **Create**.

9. At the **Generate new key pair** prompt, select **Download private key and create resource**. Your key file is downloaded as myKey.pem. Ensure you know where the .pem file was downloaded, you need the path to the key file in later steps.

8. Follow the steps 1 through 8 to create another VM with the following values and all the other settings the same as **myVM1**:

| Setting | VM 2 |

| ------- | ----- |

| **Basics** |    |

| **Instance details** |   |

| Virtual machine name | **myVM2** |

| Availability zone | **2** |

| **Administrator account** |   |

| Authentication type | **SSH public key** |

| SSH public key source | Select **Use existing key stored in Azure**. |

| Stored Keys | Select **myKey**. |

| **Inbound port rules** |  |

| Public inbound ports | Select **None**. |

| **Networking** |   |

| **Network interface** |  |

| Public IP | Select **None**. |

| NIC network security group | Select **Advanced**. |

| Configure network security group | Select the existing **myNSG** |

## Create a load balancer

You create a load balancer in this section. The frontend IP, backend pool, load-balancing, and inbound NAT rules are configured as part of the creation.

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

2. In the **Load balancer** page, select **Create**.

3. In the **Basics** tab of the **Create load balancer** page, enter, or select the following information:

| Setting                 | Value                                              |

| ---                     | ---                                                |

| **Project details** |   |

| Subscription               | Select your subscription.    |

| Resource group         | Select **TutorialLBPF-rg**. |

| **Instance details** |   |

| Name                   | Enter **myLoadBalancer**                                   |

| Region         | Select **West US 2**.                                        |

| SKU           | Leave the default **Standard**. |

| Type          | Select **Public**.                                        |

| Tier          | Leave the default **Regional**. |

4. Select **Next: Frontend IP configuration** at the bottom of the page.

5. In **Frontend IP configuration**, select **+ Add a frontend IP**.

6. Enter **myFrontend** in **Name**.

7. Select **IPv4** or **IPv6** for the **IP version**.

> [!NOTE]

> IPv6 isn't currently supported with Routing Preference or Cross-region load-balancing (Global Tier).

8. Select **IP address** for the **IP type**.

> [!NOTE]

> For more information on IP prefixes, see [Azure Public IP address prefix](../virtual-network/ip-services/public-ip-address-prefix.md).

9. Select **Create new** in **Public IP address**.

10. In **Add a public IP address**, enter **myPublicIP** for **Name**.

11. Select **Zone-redundant** in **Availability zone**.

> [!NOTE]

> In regions with [Availability Zones](/azure/reliability/availability-zones-overview?toc=%2fazure%2fvirtual-network%2ftoc.json), you can select zone-redundant (default option) or a specific zone. The choice depends on your specific domain failure requirements. In regions without Availability Zones, this field won't appear. </br> For more information on availability zones, see [Availability zones overview](/azure/reliability/availability-zones-overview).

12. Leave the default of **Microsoft Network** for **Routing preference**.

13. Select **OK**.

14. Select **Add**.

15. Select **Next: Backend pools** at the bottom of the page.

16. In the **Backend pools** tab, select **+ Add a backend pool**.

17. Enter or select the following information in **Add backend pool**.

| Setting | Value |

| ------- | ----- |

| Name | Enter **myBackendPool**. |

| Virtual network | Select **myVNet (TutorialLBPF-rg)**. |

| Backend Pool Configuration | Select **NIC**. |

| IP version | Select **IPv4**. |

18. Select **+ Add** in **Virtual machines**.

19. Select the checkboxes next to **myVM1** and **myVM2** in **Add virtual machines to backend pool**.

20. Select **Add**.

21. Select **Add**.

22. Select the **Next: Inbound rules** button at the bottom of the page.

23. In **Load balancing rule** in the **Inbound rules** tab, select **+ Add a load balancing rule**.

24. In **Add load balancing rule**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| Name | Enter **myHTTPRule** |

| IP Version | Select **IPv4** or **IPv6** depending on your requirements. |

| Frontend IP address | Select **myFrontend**. |

| Backend pool | Select **myBackendPool**. |

| Protocol | Select **TCP**. |

| Port | Enter **80**. |

| Backend port | Enter **80**. |

| Health probe | Select **Create new**. </br> In **Name**, enter **myHealthProbe**. </br> Select **TCP** in **Protocol**. </br> Leave the rest of the defaults, and select **OK**. |

| Session persistence | Select **None**. |

| Idle timeout (minutes) | Enter or select **15**. |

| TCP reset | Select **Enabled**. |

| Floating IP | Select **Disabled**. |

| Outbound source network address translation (SNAT) | Leave the default of **(Recommended) Use outbound rules to provide backend pool members access to the internet.** |

For more information about load-balancing rules, see [Load-balancing rules](manage-rules-how-to.md#load-balancing-rules).

25. Select **Add**.

26. Select the blue **Review + create** button at the bottom of the page.

27. Select **Create**.

## Create a multiple VMs inbound NAT rule

In this section, you create a multiple instance inbound NAT rule to the backend pool of the load balancer.

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

2. Select **myLoadBalancer**.

3. In **myLoadBalancer**, select **Inbound NAT rules** in settings.

4. Select **+ Add** in **Inbound NAT rules**.

5. Enter or select the following information in **Add inbound NAT rule**.

| Setting | Value |

| ------- | ----- |

| Name | Enter **myNATRule-SSH**. |

| Type | Select **Backend pool**. |

| Target backend pool | Select **myBackendPool**. |

| Frontend IP address | Select **myFrontend**. |

| Frontend port range start | Enter **221**. |

| Maximum number of machines in backend pool | Enter **500**. |

| Backend port | Enter **22**. |

| Protocol | Select **TCP**. |

6. Leave the rest at the default and select **Add**.

> [!NOTE]

> To view the port mappings to the backend pool virtual machines, see [View port mappings](manage-inbound-nat-rules.md#view-port-mappings).

## Create a NAT gateway

In this section, you create a NAT gateway for outbound internet access for resources in the virtual network.

For more information about outbound connections and Azure Virtual Network NAT, see [Using Source Network Address Translation (SNAT) for outbound connections](load-balancer-outbound-connections.md) and [What is Virtual Network NAT?](../virtual-network/nat-gateway/nat-overview.md)

1. In the search box at the top of the portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

2. In **NAT gateways**, select **+ Create**.

3. In **Create network address translation (NAT) gateway**, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **TutorialLBPF-rg**. |

| **Instance details** |    |

| NAT gateway name | Enter **myNATgateway**. |

| Region | Select **West US 2**. |

| Availability zone | Select **None**. |

| Idle timeout (minutes) | Enter **15**. |

4. Select the **Outbound IP** tab or select the **Next: Outbound IP** button at the bottom of the page.

5. In **Outbound IP**, select **Create a new public IP address** next to **Public IP addresses**.

6. Enter **myNATGatewayIP** in **Name** in **Add a public IP address**.

7. Select **OK**.

8. Select the **Subnet** tab or select the **Next: Subnet** button at the bottom of the page.

9. In **Virtual network** in the **Subnet** tab, select **myVNet**.

10. Select **myBackendSubnet** under **Subnet name**.

11. Select the blue **Review + create** button at the bottom of the page, or select the **Review + create** tab.

12. Select **Create**.

## Install web server

In this section, you'll SSH to the virtual machines through the inbound NAT rules and install a web server.

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

2. Select **myLoadBalancer**.

3. Select **Fronted IP configuration** in **Settings**.

3. In the **Frontend IP configuration**, make note of the **IP address** for **myFrontend**. In this example, it's **20.99.165.176**.

4. If you're using a Mac or Linux computer, open a Bash prompt. If you're  using a Windows computer, open a PowerShell prompt.

5. At your prompt, open an SSH connection to **myVM1**. Replace the IP address with the address you retrieved in the previous step and port **221** you used for the myVM1 inbound NAT rule. Replace the path to the .pem with the path to where the key file was downloaded.

```console

ssh -i .\Downloads\myKey.pem azureuser@20.99.165.176 -p 221

```

> [!TIP]

> The SSH key you created can be used the next time your create a VM in Azure. Just select the **Use a key stored in Azure** for **SSH public key source** the next time you create a VM. You already have the private key on your computer, so you won't need to download anything.

6. From your SSH session, update your package sources and then install the latest NGINX package.

```bash

sudo apt-get -y update

sudo apt-get -y install nginx

```

7. Enter `Exit` to leave the SSH session

8. At your prompt, open an SSH connection to **myVM2**. Replace the IP address with the address you retrieved in the previous step and port **222** you used for the myVM2 inbound NAT rule. Replace the path to the .pem with the path to where the key file was downloaded.

```console

ssh -i .\Downloads\myKey.pem azureuser@20.99.165.176 -p 222

```

9. From your SSH session, update your package sources and then install the latest NGINX package.

```bash

sudo apt-get -y update

sudo apt-get -y install nginx

```

10. Enter `Exit` to leave the SSH session.

## Test the web server

You open your web browser in this section and enter the IP address for the load balancer you retrieved in the previous step.

1. Open your web browser.

2. In the address bar, enter the IP address for the load balancer. In this example, it's **20.99.165.176**.

3. The default NGINX website is displayed.

## Clean up resources

If you're not going to continue to use this application, delete

the virtual machines and load balancer with the following steps:

1. In the search box at the top of the portal, enter **Resource group**.  Select **Resource groups** in the search results.

2. Select **TutorialLBPF-rg** in **Resource groups**.

3. Select **Delete resource group**.

4. Enter **TutorialLBPF-rg** in **TYPE THE RESOURCE GROUP NAME:**. Select **Delete**.

## Next steps

Advance to the next article to learn how to create a cross-region load balancer:

> [!div class="nextstepaction"]

> [Create a cross-region load balancer using the Azure portal](tutorial-cross-region-portal.md)


# Manage Inbound Nat Rules

# Manage inbound NAT rules for Azure Load Balancer

An inbound NAT rule is used to forward traffic from a load balancer frontend to one or more instances in the backend pool.

There are two types of inbound NAT rule:

- **Inbound NAT rule V1 for virtual machines**: Targets a single machine in the backend pool of the load balancer.

- **Inbound NAT rule V2 for virtual machines and virtual machine scale sets**: Targets multiple virtual machines in the backend pool of the load balancer.

In this article, you learn how to add and remove an inbound NAT rule for both types. You learn how to change the frontend port allocation in a multiple instance inbound NAT rule. You can choose from the Azure portal, PowerShell, or CLI examples.

[!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

## Prerequisites

- A public load balancer in your subscription. For more information on creating an Azure Load Balancer, see [Quickstart: Create a public load balancer to load balance VMs using the Azure portal](quickstart-load-balancer-standard-public-portal.md). The load balancer name for the examples in this article is **myLoadBalancer**.

- If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 5.4.1 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell). If you're running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

[!INCLUDE [azure-cli-prepare-your-environment.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment-no-header.md)]

## Inbound NAT rule V1 for virtual machines

Choose this option to configure a rule for a single VM. Select Azure portal, PowerShell, or CLI for instructions.

# [**Portal**](#tab/inbound-nat-rule-portal)

In this example, you create an inbound NAT rule to forward port **500** to backend port **443**.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Inbound NAT rules** in **Settings**.

5. Select **+ Add** in **Inbound NAT rules** to add the rule.

6. Enter or select the following information in **Add inbound NAT rule**.

| Setting | Value |

| ------- | ----- |

| Name | Enter **myInboundNATrule**. |

| Type | Select **Azure Virtual Machine**. |

| Target virtual machine | Select the virtual machine that you wish to forward the port to. In this example, it's **myVM1**. |

| Network IP configuration | Select the IP configuration of the virtual machine. In this example, it's **ipconfig1(10.1.0.4)**. |

| Frontend IP address | Select **myFrontend**. |

| Frontend Port | Enter **500**. |

| Service Tag | Leave the default of **Custom**. |

| Backend port | Enter **443**. |

| Protocol | Select **TCP**. |

7. Leave the rest of the settings at the defaults and select **Add**.

# [**PowerShell**](#tab/inbound-nat-rule-powershell)

In this example, you create an inbound NAT rule to forward port **500** to backend port **443**.

- Use [Get-AzLoadBalancer](/powershell/module/az.network/get-azloadbalancer) to place the load balancer information into a variable.

- Use [Add-AzLoadBalancerInboundNatRuleConfig](/powershell/module/az.network/add-azloadbalancerinboundnatruleconfig) to create the inbound NAT rule.

- To save the configuration to the load balancer, use [Set-AzLoadBalancer](/powershell/module/az.network/set-azloadbalancer).

- Use [Get-AzLoadBalancerInboundNatRuleConfig](/powershell/module/az.network/get-azloadbalancerinboundnatruleconfig) to place the newly created inbound NAT rule information into a variable.

- Use [Get-AzNetworkInterface](/powershell/module/az.network/get-aznetworkinterface) to place the network interface information into a variable.

- Use [Set-AzNetworkInterfaceIpConfig](/powershell/module/az.network/set-aznetworkinterfaceipconfig) to add the newly created inbound NAT rule to the IP configuration of the network interface.

To save the configuration to the network interface, use [Set-AzNetworkInterface](/powershell/module/az.network/set-aznetworkinterface).

```azurepowershell

## Place the load balancer information into a variable for later use. ##

$slb = @{

ResourceGroupName = 'myResourceGroup'

Name = 'myLoadBalancer'

}

$lb = Get-AzLoadBalancer @slb

## Create the single virtual machine inbound NAT rule. ##

$rule = @{

Name = 'myInboundNATrule'

Protocol = 'Tcp'

FrontendIpConfiguration = $lb.FrontendIpConfigurations[0]

FrontendPort = '500'

BackendPort = '443'

}

$lb | Add-AzLoadBalancerInboundNatRuleConfig @rule

$lb | Set-AzLoadBalancer

## Add the inbound NAT rule to a virtual machine

$NatRule = @{

Name = 'MyInboundNATrule'

LoadBalancer = $lb

}

$NatRuleConfig = Get-AzLoadBalancerInboundNatRuleConfig @NatRule

$NetworkInterface = @{

ResourceGroupName = 'myResourceGroup'

Name = 'MyNIC'

}

$NIC = Get-AzNetworkInterface @NetworkInterface

$IPconfig = @{

Name = 'Ipconfig'

LoadBalancerInboundNatRule = $NatRuleConfig

}

$NIC | Set-AzNetworkInterfaceIpConfig @IPconfig

$NIC | Set-AzNetworkInterface

```

# [**CLI**](#tab/inbound-nat-rule-cli)

[!INCLUDE [azure-cli-prepare-your-environment.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment-no-header.md)]

In this example, you will create an inbound NAT rule to forward port **500** to backend port **443**. You will then attach the inbound NAT rule to a VM's NIC

- Use [az network lb inbound-nat-rule create](/cli/azure/network/lb/inbound-nat-rule#az-network-lb-inbound-nat-rule-create) to create the NAT rule.

- Use [az network nic ip-config inbound-nat-rule add](/cli/azure/network/nic/ip-config/inbound-nat-rule) to add the inbound NAT rule to a VM's NIC

```azurecli

az network lb inbound-nat-rule create \

--backend-port 443 \

--lb-name myLoadBalancer \

--name myInboundNATrule \

--protocol Tcp \

--resource-group myResourceGroup \

--frontend-ip-name myFrontend \

--frontend-port 500

az network nic ip-config inbound-nat-rule add \

--resource-group myResourceGroup \

--nic-name MyNic \

--ip-config-name MyIpConfig \

--inbound-nat-rule MyNatRule \

--lb-name myLoadBalancer

```

---

## Inbound NAT rule V2 for virtual machines and virtual machine scale sets

Choose this option to configure a rule with a range of ports to a backend pool of virtual machines. Select Azure portal, PowerShell, or CLI for instructions.

# [**Portal**](#tab/inbound-nat-rule-portal)

In this example, you create an inbound NAT rule to forward a range of ports starting at port 500 to backend port 443. The maximum number of machines in the backend pool is set by the parameter **Maximum number of machines in backend pool** with a value of **500**. This setting limits the backend pool to **500** virtual machines.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Inbound NAT rules** in **Settings**.

5. Select **+ Add** in **Inbound NAT rules** to add the rule.

6. Enter or select the following information in **Add inbound NAT rule**.

| Setting | Value |

| ------- | ----- |

| Name | Enter **myInboundNATrule**. |

| Type | Select **Backend pool**. |

| Target backend pool | Select your backend pool. In this example, it's **myBackendPool**. |

| Frontend IP address | Select your frontend IP address. In this example, it's **myFrontend**. |

| Frontend port range start | Enter **500**. |

| Maximum number of machines in backend pool | Enter **500**. |

| Backend port | Enter **443**. |

| Protocol | Select **TCP**. |

7. Leave the rest at the defaults and select **Add**.

# [**PowerShell**](#tab/inbound-nat-rule-powershell)

In this example, you create an inbound NAT rule to forward a range of ports starting at port 500 to backend port 443. The maximum number of machines in the backend pool is set by the parameter `-FrontendPortRangeEnd` with a value of **1000**. This setting limits the backend pool to **500** virtual machines.

- Use [Get-AzLoadBalancer](/powershell/module/az.network/get-azloadbalancer) to place the load balancer information into a variable.

- Use [Add-AzLoadBalancerInboundNatRuleConfig](/powershell/module/az.network/add-azloadbalancerinboundnatruleconfig) to create the inbound NAT rule.

- To save the configuration to the load balancer, use [Set-AzLoadBalancer](/powershell/module/az.network/set-azloadbalancer)

```azurepowershell

## Place the load balancer information into a variable for later use. ##

$slb = @{

ResourceGroupName = 'myResourceGroup'

Name = 'myLoadBalancer'

}

$lb = Get-AzLoadBalancer @slb

## Create the multiple virtual machines inbound NAT rule. ##

$rule = @{

Name = 'myInboundNATrule'

Protocol = 'Tcp'

BackendPort = '443'

FrontendIpConfiguration = $lb.FrontendIpConfigurations[0]

FrontendPortRangeStart = '500'

FrontendPortRangeEnd = '1000'

BackendAddressPool = $lb.BackendAddressPools[0]

}

$lb | Add-AzLoadBalancerInboundNatRuleConfig @rule

$lb | Set-AzLoadBalancer

```

# [**CLI**](#tab/inbound-nat-rule-cli)

In this example, you create an inbound NAT rule to forward a range of ports starting at port 500 to backend port 443. The maximum number of machines in the backend pool is set by the parameter `--frontend-port-range-end` with a value of **1000**. This setting limits the backend pool to **500** virtual machines.

- Use [az network lb inbound-nat-rule create](/cli/azure/network/lb/inbound-nat-rule#az-network-lb-inbound-nat-rule-create) to create the NAT rule.

```azurecli

az network lb inbound-nat-rule create \

--backend-port 443 \

--lb-name myLoadBalancer \

--name myInboundNATrule \

--protocol Tcp \

--resource-group myResourceGroup \

--backend-pool-name myBackendPool \

--frontend-ip-name myFrontend \

--frontend-port-range-end 1000 \

--frontend-port-range-start 500

```

---

## Change frontend port allocation for a multiple VM rule

# [**Portal**](#tab/inbound-nat-rule-portal)

To accommodate more virtual machines in the backend pool in a multiple instance rule, change the frontend port allocation in the inbound NAT rule. In this example, you change the **Maximum number of machines in backend pool** from **500** to **1000**. This setting increases the maximum number of machines in the backend pool to **1000**.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Inbound NAT rules** in **Settings**.

5. Select the inbound NAT rule you wish to change. In this example, it's **myInboundNATrule**.

6. In the properties of the inbound NAT rule, change the value in **Maximum number of machines in backend pool** to **1000**.

7. Select **Save**.

# [**PowerShell**](#tab/inbound-nat-rule-powershell)

To accommodate more virtual machines in the backend pool in a multiple instance rule, change the frontend port allocation in the inbound NAT rule. In this example, you change the parameter `-FrontendPortRangeEnd` to **1500**. This setting increases the maximum number of machines in the backend pool to **1000**.

- Use [Get-AzLoadBalancer](/powershell/module/az.network/get-azloadbalancer) to place the load balancer information into a variable.

- To change the port allocation, use [Set-AzLoadBalancerInboundNatRuleConfig](/powershell/module/az.network/set-azloadbalancerinboundnatruleconfig).

```azurepowershell

## Place the load balancer information into a variable for later use. ##

$slb = @{

ResourceGroupName = 'myResourceGroup'

Name = 'myLoadBalancer'

}

$lb = Get-AzLoadBalancer @slb

## Set the new port allocation

$rule = @{

Name = 'myInboundNATrule'

Protocol = 'Tcp'

BackendPort = '443'

FrontendIpConfiguration = $lb.FrontendIpConfigurations[0]

FrontendPortRangeStart = '500'

FrontendPortRangeEnd = '1500'

BackendAddressPool = $lb.BackendAddressPools[0]

}

$lb | Set-AzLoadBalancerInboundNatRuleConfig @rule

```

# [**CLI**](#tab/inbound-nat-rule-cli)

To accommodate more virtual machines in the backend pool, change the frontend port allocation in the inbound NAT rule. In this example, you change the parameter `--frontend-port-range-end` to **1500**. This setting increases the maximum number of machines in the backend pool to **1000**

- Use [az network lb inbound-nat-rule update](/cli/azure/network/lb/inbound-nat-rule#az-network-lb-inbound-nat-rule-update) to change the frontend port allocation.

```azurecli

az network lb inbound-nat-rule update \

--frontend-port-range-end 1500 \

--lb-name myLoadBalancer \

--name myInboundNATrule \

--resource-group myResourceGroup

```

---

## View port mappings

Port mappings for the virtual machines in the backend pool can be viewed by using the Azure portal.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page in, select **Inbound NAT rules** in **Settings**.

5. Select **myInboundNATrule** or your inbound NAT rule.

6. Scroll to the **Port mapping** section of the inbound NAT rule properties page.

## Remove an inbound NAT rule

# [**Portal**](#tab/inbound-nat-rule-portal)

In this example, you remove an inbound NAT rule.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page in, select **Inbound NAT rules** in **Settings**.

5. Select the three dots next to the rule you want to remove.

6. Select **Delete**.

# [**PowerShell**](#tab/inbound-nat-rule-powershell)

In this example, you remove an inbound NAT rule.

- Use [Get-AzLoadBalancer](/powershell/module/az.network/get-azloadbalancer) to place the load balancer information into a variable.

- To remove the inbound NAT rule, use [Remove-AzLoadBalancerInboundNatRuleConfig](/powershell/module/az.network/remove-azloadbalancerinboundnatruleconfig).

- To save the configuration to the load balancer, use [Set-AzLoadBalancer](/powershell/module/az.network/set-azloadbalancer).

```azurepowershell

## Place the load balancer information into a variable for later use. ##

$slb = @{

ResourceGroupName = 'myResourceGroup'

Name = 'myLoadBalancer'

}

$lb = Get-AzLoadBalancer @slb

## Remove the inbound NAT rule

$lb | Remove-AzLoadBalancerInboundNatRuleConfig -Name 'myInboundNATrule'

$lb | Set-AzLoadBalancer

```

# [**CLI**](#tab/inbound-nat-rule-cli)

In this example, you remove an inbound NAT rule.

- Use [az network lb inbound-nat-rule delete](/cli/azure/network/lb/inbound-nat-rule#az-network-lb-inbound-nat-rule-delete) to remove the rule.

```azurecli

az network lb inbound-nat-rule delete \

--lb-name myLoadBalancer \

--name myInboundNATrule \

--resource-group myResourceGroup

```

---

## Next steps

In this article, you learned how to manage inbound NAT rules for an Azure Load Balancer using the Azure portal, PowerShell and CLI.

For more information about Azure Load Balancer, see:

- [What is Azure Load Balancer?](load-balancer-overview.md)

- [Frequently asked questions - Azure Load Balancer](load-balancer-faqs.yml)


# Load Balancer Nat Pool Migration

# Migrate from Inbound NAT rules version 1 to version 2

An [inbound NAT rule](inbound-nat-rules.md) is used to forward traffic from a load balancer’s frontend to one or more instances in the backend pool. These rules provide a 1:1 mapping between the load balancer’s frontend IP address and backend instances. There are currently two versions of Inbound NAT rules, version 1 and version 2.

>[!Important]

> On September 30, 2027, **Inbound NAT Pools** (the Azure Virtual Machine Scale Sets-specific feature of Inbound NAT rules V1) will be retired. If you are currently using Inbound NAT Pools with Virtual Machine Scale Sets, migrate to Inbound NAT rules V2 prior to the retirement date. **Single VM Inbound NAT rules V1 are not affected by this retirement** and do not need to be migrated.

## NAT rule version 1

[Version 1](inbound-nat-rules.md) of Inbound NAT rules includes two distinct features:

- **Single VM Inbound NAT rules** — Provides 1:1 port mapping between a load balancer frontend IP/port and a specific virtual machine. Rules are applied directly to the VM's network interface card (NIC). **These are not being retired and do not need to be migrated.**

- **Inbound NAT Pools (Virtual Machine Scale Sets only)** — This is the legacy approach for assigning an Azure Load Balancer’s frontend port to each backend instance. Inbound NAT rules are automatically created and deleted per Virtual Machine Scale Set instance as the scale set scales up and down. NAT Pools are defined on the load balancer and referenced by the Virtual Machine Scale Sets NIC configuration via the `loadBalancerInboundNatPools` property. **These are being retired on September 30, 2027 and must be migrated to Inbound NAT rules V2.**

## NAT rule version 2

[Version 2](inbound-nat-rules.md) of Inbound NAT rules provide the same feature set as version 1, with extra benefits.

- Simplified deployment experience and optimized updates.

- Inbound NAT rules now target the backend pool of the load balancer and no longer require a reference on the virtual machine's NIC. Previously on version 1, both the load balancer and the virtual machine's NIC needed to be updated whenever the Inbound NAT rule was changed. Version 2 only requires a single call on the load balancer’s configuration, resulting in optimized updates.

- Easily retrieve port mapping between Inbound NAT rules and backend instances.

- With the legacy offering, to retrieve the port mapping between an Inbound NAT rule and a virtual machine instance, the rule would need to be correlated with the virtual machine's NIC. Version 2 injects the port mapping between the rule and backend instance directly into the load balancer’s configuration.

## How do I know if I’m using version 1 of Inbound NAT rules?

The easiest way to identify if your deployments are using version 1 of the feature is by inspecting the load balancer’s configuration. Version 1 nat rules will have a **Type** value of *Azure Virtual Machine* with a defined **Target virtual machine** value.

For version 2 NAT rules, the **Type** value will be *Backend pool* with a defined **Target backend pool** value.

To programmatically determine if a deployment is using version 1 of Inbound NAT rules, inspect the load balancer’s configuration using the Azure CLI or PowerShell. If either the `backendIPConfiguration` property within the `InboundNATRule` configuration is populated, then the deployment is version 1 of Inbound NAT rules. Version 2 rules will have the `backendAddressPool` property instead of the `backendIPConfiguration` property.

## How do I know if I’m using Inbound NAT Pools?

To check if your load balancer has Inbound NAT Pools configured:

# [Azure CLI](#tab/azure-cli)

```azurecli

az network lb inbound-nat-pool list -g MyResourceGroup --lb-name MyLoadBalancer

```

# [PowerShell](#tab/powershell)

```powershell

$slb = Get-AzLoadBalancer -Name "MyLoadBalancer" -ResourceGroupName "MyResourceGroup"

$slb.InboundNatPools

```

---

If the above commands return any results, your load balancer is using Inbound NAT Pools and should be migrated.

The key difference is the ARM property name: Inbound NAT Pools appear under the `inboundNatPools` property on the load balancer, while Inbound NAT rules appear under the `inboundNatRules` property. If your load balancer has a non-empty `inboundNatPools` array, it is using Inbound NAT Pools and must be migrated to V2 before September 30, 2027.

> [!NOTE]

> If your load balancer only has single VM Inbound NAT rules (Type = "Azure Virtual Machine") and no Inbound NAT Pools, **no migration is required**. Single VM V1 rules are not being retired.

## How to migrate from Inbound NAT Pools to version 2?

Prior to migrating it's important to review the following information:

- Migrating to version 2 of Inbound NAT rules causes downtime to active traffic that is flowing through the NAT rules. Traffic flowing through [load balancer rules](components.md) or [outbound rules](components.md) aren't impacted during the migration process.

- Plan out the max number of instances in a backend pool. Since version 2 targets the load balancer’s backend pool, a sufficient number of ports need to be allocated for the NAT rule’s frontend.

- Each backend instance is exposed on the port configured in the new NAT rule.

- Multiple NAT rules can’t exist if they have an overlapping port range or have the same backend port.

- NAT rules and load balancing rules can’t share the same backend port.

### Manual Migration

The following three steps need to be performed to migrate to version 2 of inbound NAT rules

1. Delete the version 1 of inbound NAT rules on the load balancer’s configuration.

2. Remove the reference to the NAT rule on the virtual machine or virtual machine scale set configuration.

1. All virtual machine scale set instances need to be updated.

3. Deploy version 2 of Inbound NAT rules.

### Virtual Machine Scale Set

> [!IMPORTANT]

> This is the required migration path for the Inbound NAT Pools retirement. All Virtual Machine Scale Set deployments using Inbound NAT Pools must complete this migration before September 30, 2027.

>

The following steps are used to migrate from version 1 to version 2 of Inbound NAT rules for a virtual machine scale set. It assumes the virtual machine scale set's upgrade mode is set to Manual. For more information, see [Orchestration modes for Virtual Machine Scale Sets in Azure](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-orchestration-modes)

# [Azure CLI](#tab/azure-cli)

```azurecli

az network lb inbound-nat-pool delete  -g MyResourceGroup --lb-name MyLoadBalancer -n MyNatPool

az vmss update -g MyResourceGroup -n MyVMScaleSet --remove virtualMachineProfile.networkProfile.networkInterfaceConfigurations[0].ipConfigurations[0].loadBalancerInboundNatPools

az vmss update-instances --instance-ids '*' --resource-group MyResourceGroup --name MyVMScaleSet

az network lb inbound-nat-rule create -g MyResourceGroup --lb-name MyLoadBalancer -n MyNatRule --protocol Tcp --frontend-port-range-start 201 --frontend-port-range-end 500 --backend-port 22 --backend-address-pool MybackendPool

```

# [PowerShell](#tab/powershell)

```powershell

# Remove the Inbound NAT rule

$slb = Get-AzLoadBalancer -Name "MyLoadBalancer" -ResourceGroupName "MyResourceGroup"

Remove-AzLoadBalancerInboundNatPoolConfig -Name myinboundnatpool -LoadBalancer $slb

Set-AzLoadBalancer -LoadBalancer $slb

# Remove the Inbound NAT pool association

$vmss = Get-AzVmss -ResourceGroupName "MyResourceGroup" -VMScaleSetName "MyVMScaleSet"

$vmss.VirtualMachineProfile.NetworkProfile.NetworkInterfaceConfigurations[0].IpConfigurations[0].loadBalancerInboundNatPools = $null

# Upgrade all instances in the VMSS

Update-AzVmssInstance -ResourceGroupName $resourceGroupName -VMScaleSetName $vmssName -InstanceId "*"

$slb | Add-AzLoadBalancerInboundNatRuleConfig -Name "NewNatRuleV2" -FrontendIPConfiguration $slb.FrontendIpConfigurations[0] -Protocol "Tcp" -FrontendPortRangeStart 201-FrontendPortRangeEnd 500 -BackendAddressPool $slb.BackendAddressPools[0] -BackendPort 22

$slb | Set-AzLoadBalancer

```

---

## Migration with automation script for Virtual Machine Scale Set

The migration process will reuse existing backend pools with membership matching the NAT Pools to be migrated; if no matching backend pool is found, the script will exit (without making changes). Alternatively, use the  `-backendPoolReuseStrategy` parameter to either always create new backend pools (`NoReuse`) or create a new backend pool if a matching one doesn't exist (`OptionalFirstMatch`). Backend pools and NAT Rule associations can be updated post migration to match your preference.

### Prerequisites

Before beginning the migration process, ensure the following prerequisites are met:

- The load balancer's SKU must be **Standard** to migrate a load balancer's NAT Pools to NAT Rules. To automate this upgrade process, see the steps provided in [Upgrade a Basic Load Balancer to Standard with PowerShell](upgrade-basic-standard-with-powershell.md).

- The Virtual Machine Scale Sets associated with the target Load Balancer must use either a 'Manual' or 'Automatic' upgrade policy--'Rolling' upgrade policy isn't supported. For more information, see [Virtual Machine Scale Sets Upgrade Policies](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-policy).

- Install the latest version of [PowerShell](/powershell/scripting/install/installing-powershell).

- Install the [Azure PowerShell modules](/powershell/azure/install-azure-powershell).

### Install the `AzureLoadBalancerNATPoolMigration` module

With the following command, install the `AzureLoadBalancerNATPoolMigration` module from the PowerShell Gallery:

```powershell

# Install the AzureLoadBalancerNATPoolMigration module

Install-Module -Name AzureLoadBalancerNATPoolMigration -Scope CurrentUser -Repository PSGallery -Force

```

### Upgrade NAT Pools to NAT Rules

With the `azureLoadBalancerNATPoolMigration` module installed, upgrade your NAT Pools to NAT Rules with the following steps:

1. Connect to Azure with `Connect-AzAccount`.

2. Collect the names of the **target load balancer** for the NAT Rules upgrade and its **Resource Group** name.

3. Run the migration command with your resource names replacing the placeholders of `<loadBalancerResourceGroupName>` and `<loadBalancerName>`:

```powershell

# Run the migration command

Start-AzNATPoolMigration -ResourceGroupName <loadBalancerResourceGroupName> -LoadBalancerName <loadBalancerName>

```

## Next steps

- Learn about [Managing Inbound NAT Rules](./manage-inbound-nat-rules.md)

- Learn about [Azure Load Balancer NAT Pools and NAT Rules](https://azure.microsoft.com/blog/manage-port-forwarding-for-backend-pool-with-azure-load-balancer/)


# Load Balancer Ha Ports Overview

# High availability ports overview

Azure Standard Load Balancer helps you load-balance **all** protocol flows on **all** ports simultaneously when you're using an internal load balancer via HA Ports.

High availability (HA) ports are a type of load balancing rule that provides an easy way to load-balance **all** flows that arrive on **all** ports of an internal standard load balancer. The load-balancing decision is made per flow. This action is based on the following five-tuple connection: source IP address, source port, destination IP address, destination port, and protocol

The HA ports load-balancing rules help you with critical scenarios, such as high availability and scale for network virtual appliances (NVAs) inside virtual networks. The feature can also help when a large number of ports must be load-balanced.

The HA ports load-balancing rules are configured when you set the frontend and backend ports to **0** and the protocol to **All**. The internal load balancer resource then balances all TCP and UDP flows, regardless of port number

## Why use HA ports?

### Network virtual appliances

You can use NVAs to help secure your Azure workload from multiple types of security threats. When you use NVAs in these scenarios, they must be reliable and highly available, and they must scale out for demand. Add NVA instances to the backend pool of your internal load balancer and configure an HA ports rule.

For NVA HA scenarios, HA ports offer the following advantages:

- Provide fast failover to healthy instances, with per-instance health probes

- Ensure higher performance with scale-out to **n**-active instances

- Provide **n**-active and active-passive scenarios

- Eliminate the need for complex solutions, such as Apache ZooKeeper nodes for monitoring appliances

The following diagram presents a hub-and-spoke virtual network deployment. The spokes force-tunnel their traffic to the hub virtual network and through the NVA, before leaving the trusted space. The NVAs are behind an internal Standard Load Balancer with an HA ports configuration. All traffic can be processed and forwarded accordingly. When configured as show in the following diagram, an HA Ports load-balancing rule additionally provides flow symmetry for ingress and egress traffic.

>[!NOTE]

> If you are using NVAs, confirm with their providers how to best use HA ports and to learn which scenarios are supported.

### Load balance a large number of ports

You can also use HA ports for applications that require load balancing of large numbers of ports. You can simplify these scenarios by using an internal [standard load balancer](./load-balancer-overview.md) with HA ports. A single load-balancing rule replaces multiple individual load-balancing rules, one for each port.

## Supported configurations

### A single, nonfloating IP (non-Direct Server Return) HA-ports configuration on an internal standard load balancer

This configuration is a basic HA ports configuration. Use the following steps to configure an HA ports load-balancing rule on a single frontend IP address:

1. When configuring a standard load balancer, select the **HA ports** check box in the load balancer rule configuration.

2. For **Floating IP**, select **Disabled**.

This configuration doesn't allow any other load-balancing rule configuration on the current load balancer resource. It also allows no other internal load balancer resource configuration for the given set of backend instances.

However, you can configure a public Standard Load Balancer for the backend instances in addition to this HA ports rule.

### A single, floating IP (Direct Server Return) HA-ports configuration on an internal standard load balancer

You can similarly configure your load balancer to use a load-balancing rule with **HA Port** with a single front end by setting the **Floating IP** to **Enabled**.

With this configuration, you can add more floating IP load-balancing rules and/or a public load balancer. However, you can't use a nonfloating IP, HA-ports load-balancing configuration on top of this configuration.

### Multiple HA-ports configurations on an internal standard load balancer

To configure more than one HA port frontend for the same backend pool, use the following steps:

- Configure more than one frontend private IP address for a single internal standard load balancer resource.

- Configure multiple load-balancing rules, where each rule has a single unique frontend IP address selected.

- Select the **HA ports** option, and then set **Floating IP** to **Enabled** for all the load-balancing rules.

### An internal load balancer with HA ports and a public load balancer on the same backend instance

You can configure **one** public standard load balancer resource for the backend resources with a single internal standard load balancer with HA ports.

## Flow symmetry

Flow symmetry is only supported in the architecture described in the above diagram, for the following configurations:

- When the load balancer backend pool contains instances that only have one NIC and one IP configuration each

- When the load balancer backend pool contains instances that have multiple NICs with only one IP configuration on each NIC

- Dual-stack scenarios, where each backend instance only has one NIC and only one IPv4 and IPv6 configuration on each NIC. Please note that flow symmetry is only guaranteed for IPv4 and IPv6 flows independently, as these IP configurations would be configured with two separate backend pools and frontend IP configurations, respectively.

Flow symmetry isn't guaranteed in any scenarios that involve two or more load balancer components, such as across two different load balancers, multiple backend pools, or multiple frontend IP configurations. Since traffic is distributed based on load balancing rules, which make independent decisions and aren't coordinated, flow symmetry cannot be guaranteed in such scenarios. As a result, flow symmetry isn't supported when placing NVAs between a public and internal load balancer. If you need flow symmetry in such scenarios, consider leveraging [Gateway Load Balancer](gateway-overview.md) instead.

## Design Consideration

- ICMP traffic is supported for internal standard load balancer when HA port is enabled.

## Limitations

- HA ports load-balancing rules are available only for an internal standard load balancer.

- The combining of an HA ports load-balancing rule and a non-HA ports load-balancing rule pointing to the same backend **ipconfiguration(s)** isn't supported on a single frontend IP configuration unless both have Floating IP enabled.

- TCP idle timeout isn't supported for Internal Load Balancer (ILB) HA ports when a User Defined Route (UDR) is used to forward traffic to the ILB.

- IP fragmenting isn't supported.

## Next steps

- [Learn about Standard Load Balancer](load-balancer-overview.md)


# Load Balancer Multivip Overview

# Multiple frontends for Azure Load Balancer

Azure Load Balancer supports multiple frontend IP configurations on a single resource. Each frontend provides an independent entry point for inbound traffic, so you can expose multiple services, domains, or protocols through one load balancer.

This article explains when multiple frontends are useful, how traffic flows from frontends through rules to backend pools, and what to consider when designing a multi-frontend topology.

> [!TIP]

> If you only need a single frontend, start with the [public load balancer quickstart](./quickstart-load-balancer-standard-public-portal.md) or [internal load balancer quickstart](./quickstart-load-balancer-standard-internal-portal.md). You can add frontends later without recreating the resource.

## When to use multiple frontends

Use multiple frontends when you need to:

- **Host multiple websites or services** — Assign a dedicated public IP to each service (for example, `app1.contoso.com` and `app2.contoso.com`) while sharing a single backend pool.

- **Separate protocols on different IPs** — Expose HTTP on one frontend IP and TCP/UDP on another to simplify network security group rules and monitoring.

- **Scale beyond single-IP inbound NAT port limits** — A single IP supports up to 65,535 ports per protocol. In large-scale deployments that use inbound NAT rules to map a unique port to each backend instance (for example, per-VM SSH or RDP access), a second frontend IP provides an additional full port range.

> [!NOTE]

> Each load balancer supports a maximum number of frontend configurations. See [Load Balancer service limits](../azure-resource-manager/management/azure-subscription-service-limits.md#load-balancer) for current limits. Each public frontend IP also incurs a charge. See [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for details.

## How multiple frontends work

A frontend IP configuration is the entry point for traffic into the load balancer. Each frontend is referenced by one or more rules that determine how traffic is handled:

| Rule type | Relationship to frontend |

|-----------|--------------------------|

| **Load balancing rule** | Distributes inbound traffic arriving on a frontend IP:port across all healthy instances in a backend pool. |

| **Inbound NAT rule** | Maps a specific frontend IP:port to a single backend instance:port, enabling direct access to individual VMs. |

| **Outbound rule** | Designates which frontend IP(s) provide SNAT ports for outbound connections initiated by backend instances. |

Multiple rules of any type can reference the same frontend, and multiple frontends can target the same backend pool. When multiple rules share a backend pool, those rules can share a single health probe as long as they target the same backend port and protocol.

### Same backend port versus different backend port

When multiple load balancing rules from different frontends target the same backend pool, you can route to:

- **Different backend ports** — Each rule specifies a unique backend port. No extra configuration is needed.

- **The same backend port** — You must enable Floating IP on each rule.

Without Floating IP, the load balancer translates the destination address to the backend VM's private IP. When two frontends both route to the same backend port, the VM receives traffic on the same IP:port regardless of which frontend it arrived on. The VM has no way to distinguish between the two flows or respond on the correct frontend IP.

Enabling Floating IP changes this behavior because the load balancer delivers packets with the original frontend IP preserved as the destination address. When you use Floating IP, you must configure the targeted backend VMs with a loopback interface or secondary IP that matches each frontend IP so the VMs can accept and respond to traffic correctly. For more information, see [Floating IP configuration](load-balancer-floating-ip.md).

## Next steps

- Learn how to [manage rules for Azure Load Balancer](manage-rules-how-to.md), including adding and removing frontend IP configurations.

- Learn about [Floating IP configuration](load-balancer-floating-ip.md) for same-port scenarios.

- Learn about [Azure Load Balancer outbound connections](load-balancer-outbound-connections.md).


# Load Balancer Tcp Reset

# Load Balancer TCP Reset and Idle Timeout

You can use [Standard Load Balancer](./load-balancer-overview.md) to create a more predictable application behavior for your scenarios by enabling TCP Reset on Idle for a given rule. Load Balancer's default behavior is to silently drop flows when the idle timeout of a flow is reached. Enabling TCP reset causes Load Balancer to send bidirectional TCP Resets (TCP reset packets) on idle timeout to inform your application endpoints that the connection timed out and is no longer usable. Endpoints can immediately establish a new connection if needed.

## TCP reset

You change this default behavior and enable sending TCP Resets on idle timeout on inbound NAT rules, load balancing rules, and [outbound rules](./load-balancer-outbound-connections.md#outboundrules). When enabled per rule, Load Balancer sends bidirectional TCP Resets (TCP RST packets) to both client and server endpoints at the time of idle timeout for all matching flows.

Endpoints receiving TCP RST packets close the corresponding socket immediately. This provides an immediate notification to the endpoint's connection release and any future communication on the same TCP connection will fail. Applications can purge connections when the socket closes and reestablish connections as needed without waiting for the TCP connection to eventually time out.

For many scenarios, a TCP reset can reduce the need to send TCP (or application layer) keepalives to refresh the idle timeout of a flow.

If your idle durations exceed configuration limits or your application shows an undesirable behavior with TCP Resets enabled, you can still need to use TCP keepalives, or application layer keepalives, to monitor the liveness of the TCP connections. Further, keepalives can also remain useful for when the connection is proxied somewhere in the path, particularly application layer keepalives.

By carefully examining the entire end to end scenario, you can determine the benefits from enabling TCP Resets and adjusting the idle timeout. Then you decide if more steps can be required to ensure the desired application behavior.

## Configurable TCP idle timeout

Azure Load Balancer Standard has a 4 minutes to 100-minutes timeout range for load balancer rules, outbound rules, and inbound NAT rules. The default is 4 minutes. If a period of inactivity is longer than the timeout value, there's no guarantee that the TCP or HTTP session is maintained between the client and your cloud service. Azure Load Balancer Basic has up to a 60 minute timeout range.

When the connection is closed, your client application can receive the following error message: "The underlying connection was closed: A connection that was expected to be kept alive was closed by the server."

If TCP resets are enabled, and it's missed for any reason, resets for any subsequent packets. If the TCP reset option isn't enabled, then packets are silently dropped.

A common practice is to use a TCP keep-alive. This practice keeps the connection active for a longer period. For more information, see these [.NET examples](/dotnet/api/system.net.servicepoint.settcpkeepalive). With keep-alive enabled, packets are sent during periods of inactivity on the connection. Keep-alive packets ensure the idle timeout value isn't reached and the connection is maintained for a long period.

The setting works for inbound connections only. To avoid losing the connection, configure the TCP keep-alive with an interval less than the idle timeout setting or increase the idle timeout value. To support these scenarios, support for a configurable idle timeout is available.

TCP keep-alive works for scenarios where battery life isn't a constraint. It isn't recommended for mobile applications. Using a TCP keep-alive in a mobile application can drain the device battery faster.

## Order of precedence

It's important to take into account how the idle timeout values set for different IPs could potentially interact.

### Inbound

- If there's an (inbound) load balancer rule with an idle timeout value set differently than the idle timeout of the frontend IP it references, the load balancer frontend IP idle timeout takes precedence.

- If there's an inbound NAT rule with an idle timeout value set differently than the idle timeout of the frontend IP it references, the load balancer frontend IP idle timeout takes precedence.

### Outbound

- If there's an outbound rule with an idle timeout value different than 4 minutes (which is what public IP outbound idle timeout is locked at), the outbound rule idle timeout takes precedence.

- Because a NAT gateway will always take precedence over load balancer outbound rules (and over public IP addresses assigned directly to VMs), the idle timeout value assigned to the NAT gateway will be used. (Along the same lines, the locked public IP outbound idle timeouts of 4 minutes of any IPs assigned to the NAT GW aren't considered.)

## Limitations

- TCP reset only sent during TCP connection in ESTABLISHED state.

- Idle timeout is not supported for UDP load balancing rules.

- TCP reset isn't supported for Internal Load Balancer HA ports when a network virtual appliance is in the path. A workaround could be to use outbound rule with TCP reset from Network Virtual Appliance.

- TCP idle timeout isn't supported for Internal Load Balancer (ILB) HA ports when a User Defined Route (UDR) is used to forward traffic to the ILB.

## Next steps

- Learn about [Standard Load Balancer](./load-balancer-overview.md).

- Learn about [outbound rules](./load-balancer-outbound-connections.md#outboundrules).

- [Configure TCP RST on Idle Timeout](load-balancer-tcp-idle-timeout.md)


# Load Balancer Floating Ip

# Azure Load Balancer Floating IP configuration

Load balancer provides several capabilities for both UDP and TCP applications.

## Floating IP

Some application scenarios prefer or require the use of the same port by multiple application instances on a single VM in the backend pool. Common examples of port reuse include clustering for high availability, network virtual appliances, and exposing multiple TLS endpoints without re-encryption. If you want to reuse the backend port across multiple rules, you must enable Floating IP in the rule definition. Enabling Floating IP allows for more flexibility.

| Floating IP status | Outcome |

| --- | --- |

| Floating IP enabled | Azure changes the IP address mapping to the Frontend IP address of the Load Balancer |

| Floating IP disabled |  Azure exposes the VM instances' IP address |

In the diagrams, you see how IP address mapping works before and after enabling Floating IP:

You configure Floating IP on a Load Balancer rule via the Azure portal, REST API, CLI, PowerShell, or other client. In addition to the rule configuration, you must also configure your virtual machine's Guest OS in order to use Floating IP.

The Floating IP rule type is the foundation of several load balancer configuration patterns. One example that is currently available is the [Configure one or more Always On availability group listeners](/azure/azure-sql/virtual-machines/windows/availability-group-listener-powershell-configure) configuration. Over time, we'll document more of these scenarios.

## Floating IP Guest OS configuration

In order to function, you configure the Guest OS for the virtual machine to receive all traffic bound for the frontend IP and port of the load balancer. Configuring the VM requires:

* adding a loopback network interface

* configuring the loopback with the frontend IP address of the load balancer

* ensuring the system can send/receive packets on interfaces that don't have the IP address assigned to that interface. Windows systems require setting interfaces to use the "weak host" model. For Linux systems, this model is normally used by default.

* configuring the host firewall to allow traffic on the frontend IP port.

> [!NOTE]

> The examples below all use IPv4; to use IPv6, substitute "ipv6" for "ipv4".

### Windows Server

<details>

<summary>Expand</summary>

For each VM in the backend pool, run the following commands at a Windows Command Prompt on the server.

1. To get the list of interface names you have on your VM, enter this command:

```console

netsh interface ipv4 show interface

```

2. For the VM NIC (Azure managed), enter the following command after replacing **interface-name** with the name of the interface you want to use:

```console

netsh interface ipv4 set interface <interface-name> weakhostreceive=enabled

```

3. For each loopback interface you added, enter these commands after replacing **loopback-interface-name** with the name of the loopback interface and **floating-IP** and **floating-IPnetmask** with the appropriate values that correspond to the load balancer frontend IP:

```console

netsh interface ipv4 add addr <loopback-interface-name> <floating-IP> <floating-IPnetmask>

netsh interface ipv4 set interface <loopback-interface-name> weakhostreceive=enabled  weakhostsend=enabled

```

4. Finally, if the guest host uses a firewall, ensure a rule set up so the traffic can reach the VM on the appropriate ports. This example configuration assumes a load balancer frontend IP configuration of 1.2.3.4 and a load balancing rule for port 80:

```console

netsh int ipv4 set int "Ethernet" weakhostreceive=enabled

netsh int ipv4 add addr "Loopback Pseudo-Interface 1" 1.2.3.4 255.255.255.0

netsh int ipv4 set int "Loopback Pseudo-Interface 1" weakhostreceive=enabled weakhostsend=enabled

netsh advfirewall firewall add rule name="http" protocol=TCP localport=80 dir=in action=allow enable=yes

```

</details>

### Ubuntu

<details>

<summary>Expand</summary>

For each VM in the backend pool, run the following commands via an SSH session.

1. To get the list of interface names you have on your VM, type this command:

```console

ip addr

```

2. For each loopback interface you added, enter these commands after replacing **loopback-interface-name** with the name of the loopback interface and **floating-IP** and **floating-IPnetmask** with the appropriate values that correspond to the load balancer frontend IP:

```console

sudo ip addr add <floating-IP>/<floating-IPnetmask> dev lo:0

```

3. Finally, if the guest host uses a firewall, ensure a rule set up so the traffic can reach the VM on the appropriate ports. This example configuration assumes a load balancer frontend IP configuration of 1.2.3.4, a load balancing rule for port 80, and the use of [UFW (Uncomplicated Firewall)](https://www.wikipedia.org/wiki/Uncomplicated_Firewall) in Ubuntu.

```console

sudo ip addr add 1.2.3.4/24 dev lo:0

sudo ufw allow 80/tcp

```

</details>

## <a name = "limitations"></a>Limitations

-  With Floating IP enabled on a load balancing rule, your application must use the primary IP configuration of the network interface for outbound.

-  If your application binds to the frontend IP address configured on the loopback interface in the guest OS, Azure's outbound connection doesn't rewrite the outbound flow, and the flow fails. Review [outbound scenarios](load-balancer-outbound-connections.md).

- You can't use Floating IP on secondary IP configurations for Load Balancing scenarios. This limitation doesn't apply to Public load balancers where the secondary IP configuration is IPv6 and part of a dual-stack configuration, or to architectures that utilize a NAT Gateway for outbound connectivity.

## Next steps

- Learn about [using multiple frontends](load-balancer-multivip-overview.md) with Azure Load Balancer.

- Learn about [Azure Load Balancer outbound connections](load-balancer-outbound-connections.md).


# Manage Rules How To

# Manage rules for Azure Load Balancer using the Azure portal

Azure Load Balancer supports rules to configure traffic to the backend pool.  In this article, you learn how to manage the rules for an Azure Load Balancer.

There are four types of rules:

- **Load-balancing rules** - A load balancer rule is used to define how incoming traffic is distributed to **all** the instances within the backend pool. A load-balancing rule maps a given frontend IP configuration and port to multiple backend IP addresses and ports. An example would be a rule created on port 80 to load balance web traffic.

- **High availability ports** - A load balancer rule configured with **protocol - all** and **port - 0**. These rules enable a single rule to load-balance all TCP and UDP traffic that arrive on all ports of an internal standard load balancer. The HA ports load-balancing rules help with scenarios, such as high availability and scale for network virtual appliances (NVAs) inside virtual networks. The feature can help when a large number of ports must be load-balanced.

- **Inbound NAT rule** - An inbound NAT rule forwards incoming traffic sent to frontend IP address and port combination. The traffic is sent to a **specific** virtual machine or instance in the backend pool. Port forwarding is done by the same hash-based distribution as load balancing.

- **Outbound rule** - An outbound rule configures outbound Network Address Translation (NAT) for **all** virtual machines or instances identified by the backend pool. This rule enables instances in the backend to communicate (outbound) to the internet or other endpoints.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- A standard public load balancer in your subscription. For more information on creating an Azure Load Balancer, see [Quickstart: Create a public load balancer to load balance VMs using the Azure portal](quickstart-load-balancer-standard-public-portal.md). The load balancer name for the examples in this article is **myLoadBalancer**.

- A standard internal load balancer in your subscription. For more information on creating an Azure Load Balancer, see [Quickstart: Create a internal load balancer to load balance VMs using the Azure portal](quickstart-load-balancer-standard-internal-portal.md). The load balancer name for the examples in this article is **myLoadBalancer**.

## Load-balancing rules

In this section, you learn how to add and remove a load-balancing rule. A public load balancer is used in the examples.

### Add a load-balancing rule

In this example, you create a rule to load balance port 80.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Load balancing rules** in **Settings**.

5. Select **+ Add** in **Load balancing rules** to add a rule.

6. Enter or select the following information in **Add load balancing rule**.

| Setting | Value |

| ------- | ----- |

| Name | **myHTTPRule** |

| IP Version | Select **IPv4** or **IPv6**. |

| Frontend IP address | Select the frontend IP address of the load balancer. <br> In this example, it's **myFrontendIP**. |

| Protocol | Leave the default of **TCP**. |

| Port | Enter **80**. |

| Backend port | Enter **80**. |

| Backend pool | Select the backend pool of the load balancer.</br> In this example, it's **myBackendPool**. |

| Health probe | Select **Create new**.</br> In **Name**, enter **myHealthProbe**.</br> Select **HTTP** in **Protocol**.</br> Leave the rest at the defaults or tailor to your requirements.</br> Select **OK**. |

| Session persistence | Select **None** or your required persistence.</br> For more information about distribution modes, see [Azure Load Balancer distribution modes](load-balancer-distribution-mode.md). |

| Idle timeout (minutes) | Leave the default of **4** or move the slider to your required idle timeout. |

| TCP reset | Select **Enabled**.</br> For more information on TCP reset, see [Load Balancer TCP Reset and Idle Timeout](load-balancer-tcp-reset.md). |

| Floating IP | Leave the default of **Disabled** or enable if your deployment requires floating IP.</br> For information on floating IP, see [Azure Load Balancer Floating IP configuration](load-balancer-floating-ip.md). |

| Outbound source network address translation (SNAT) | Leave the default of **(Recommended) Use outbound rules to provide backend pool members access to the internet.**</br> For more information on outbound rules and (SNAT), see [Outbound rules Azure Load Balancer](outbound-rules.md) and [Using Source Network Address Translation (SNAT) for outbound connections](load-balancer-outbound-connections.md).|

7. Select **Add**.

### Remove a load-balancing rule

In this example, you remove a load-balancing rule.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Load balancing rules** in **Settings**.

5. Select the three dots next to the rule you want to remove.

6. Select **Delete**.

## High availability ports

In this section, you learn how to add and remove a high availability ports rule. You use an internal load balancer in this example.

HA ports rules are supported on a standard internal load balancer.

### Add high availability ports rule

In this example, you create a high availability ports rule.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Load balancing rules** in **Settings**.

5. Select **+ Add** in **Load balancing rules** to add a rule.

6. Enter or select the following information in **Add load balancing rule**.

| Setting | Value |

| ------- | ----- |

| Name | Enter **myHARule**. |

| IP Version | Select **IPv4** or **IPv6**. |

| Frontend IP address | Select the frontend IP address of the load balancer. <br> In this example, it's **myFrontendIP**.</br> Select the box next to **HA Ports**. |

| Backend pool | Select the backend pool of the load balancer.</br> In this example, it's **myBackendPool**. |

| Health probe | Select **Create new**.</br> In **Name**, enter **myHealthProbe**.</br> Select **TCP** in **Protocol**.</br> Enter a TCP port in **Port**. In this example, it's port **80**. Enter a port that meets your requirements.</br> Leave the rest at the defaults or tailor to your requirements.</br> Select **OK**. |

| Session persistence | Select **None** or your required persistence.</br> For more information about distribution modes, see [Azure Load Balancer distribution modes](load-balancer-distribution-mode.md). |

| Idle timeout (minutes) | Leave the default of **4** or move the slider to your required idle timeout. |

| TCP reset | Select **Enabled**.</br> For more information on TCP reset, see [Load Balancer TCP Reset and Idle Timeout](load-balancer-tcp-reset.md). |

| Floating IP | Leave the default of **Disabled** or enable if your deployment requires floating IP.</br> For information on floating IP, see [Azure Load Balancer Floating IP configuration](load-balancer-floating-ip.md). |

For more information on HA ports rule configuration, see **[High availability ports overview](load-balancer-ha-ports-overview.md)**.

7. Select **Add**.

### Remove a high availability ports rule

In this example, you remove a load-balancing rule.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Load balancing rules** in **Settings**.

5. Select the three dots next to the rule you want to remove.

6. Select **Delete**.

## Inbound NAT rule

Inbound NAT rules are used to route connections to a specific VM in the backend pool. For more information and a detailed tutorial on configuring and testing inbound NAT rules, see [Tutorial: Configure port forwarding in Azure Load Balancer using the portal](tutorial-load-balancer-port-forwarding-portal.md).

## Outbound rule

You learn how to add and remove an outbound rule in this section. You use a public load balancer in this example.

Outbound rules are supported on standard public load balancers.

### Add outbound rule

In this example, you create an outbound rule.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Outbound rules** in **Settings**.

5. Select **+ Add** in **Outbound rules** to add a rule.

6. Enter or select the following information in **Add outbound rule**.

| Setting | Value |

| ------- | ----- |

| Name | Enter **myOutboundRule**. |

| IP Version | Select **IPv4** or **IPv6**. |

| Frontend IP address | Select the frontend IP address of the load balancer. <br> In this example, it's **myFrontendIP**. |

| Protocol | Leave the default of **All**. |

| Idle timeout (minutes) | Leave the default of **4** or move the slider to meet your requirements. |

| TCP Reset | Leave the default of **Enabled**. |

| Backend pool | Select the backend pool of the load balancer.</br> In this example, it's **myBackendPool**. |

| **Port allocation** |   |

| Port allocation | Select **Manually choose number of outbound ports**. |

| **Outbound ports** |  |

| Choose by | Select **Ports per instance**. |

| Ports per instance | Enter **10000**. |

7. Select **Add**.

### Remove an outbound rule

In this example, you remove an outbound rule.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Outbound rules** in **Settings**.

5. Select the three dots next to the rule you want to remove.

6. Select **Delete**.

## Next steps

In this article, you learned how to manage load-balancing rules for an Azure Load Balancer.

For more information about Azure Load Balancer, see:

- [What is Azure Load Balancer?](load-balancer-overview.md)

- [Frequently asked questions - Azure Load Balancer](load-balancer-faqs.yml)


# Load Balancer Tcp Idle Timeout

# Configure TCP reset and idle timeout for Azure Load Balancer

Azure Load Balancer rules have a default timeout range of 4 minutes to 100 minutes for Load Balancer rules, Outbound Rules, and Inbound NAT rules. The default setting is 4 minutes. If a period of inactivity is longer than the timeout value, there's no guarantee that the TCP or HTTP session is maintained between the client and your service.

The following sections describe how to change idle timeout and tcp reset settings for load balancer resources.

## Set tcp reset and idle timeout

---

# [**Portal**](#tab/tcp-reset-idle-portal)

To set the idle timeout and tcp reset for a load balancer, edit the load-balanced rule.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the left-hand menu, select **Resource groups**.

1. Select the resource group for your load balancer. In this example, the resource group is named **myResourceGroup**.

1. Select your load balancer. In this example, the load balancer is named **myLoadBalancer**.

1. In **Settings**, select **Load balancing rules**.

1. Select your load-balancing rule. In this example, the load-balancing rule is named **myLBrule**.

1. In the load-balancing rule, input your timeout value into **Idle timeout (minutes)**.

1. Under **TCP reset**, select **Enabled**.

1. Select **Save**.

# [**PowerShell**](#tab/tcp-reset-idle-powershell)

To set the idle timeout and tcp reset, set values in the following load-balancing rule parameters with [Set-AzLoadBalancer](/powershell/module/az.network/set-azloadbalancer):

* **IdleTimeoutInMinutes**

* **EnableTcpReset**

If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 5.4.1 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell). If you're running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

Replace the following examples with the values from your resources:

* **myResourceGroup**

* **myLoadBalancer**

```azurepowershell

$lb = Get-AzLoadBalancer -Name "myLoadBalancer" -ResourceGroup "myResourceGroup"

$lb.LoadBalancingRules[0].IdleTimeoutInMinutes = '15'

$lb.LoadBalancingRules[0].EnableTcpReset = 'true'

Set-AzLoadBalancer -LoadBalancer $lb

```

# [**Azure CLI**](#tab/tcp-reset-idle-cli)

To set the idle timeout and tcp reset, use the following parameters for [az network lb rule update](/cli/azure/network/lb/rule?az_network_lb_rule_update):

* **--idle-timeout**

* **--enable-tcp-reset**

Validate your environment before you begin:

* Sign in to the Azure portal and check that your subscription is active by running `az login`.

* Check your version of the Azure CLI in a terminal or command window by running `az --version`. For the latest version, see the [latest release notes](/cli/azure/release-notes-azure-cli?tabs=azure-cli).

* If you don't have the latest version, update your installation by following the [installation guide for your operating system or platform](/cli/azure/install-azure-cli).

Replace the following examples with the values from your resources:

* **myResourceGroup**

* **myLoadBalancer**

* **myLBrule**

```azurecli

az network lb rule update \

--resource-group myResourceGroup \

--name myLBrule \

--lb-name myLoadBalancer \

--idle-timeout 15 \

--enable-tcp-reset true

```

---

## Next steps

For more information on tcp idle timeout and reset, see [Load Balancer TCP Reset and Idle Timeout](load-balancer-tcp-reset.md)

For more information on configuring the load balancer distribution mode, see [Configure a load balancer distribution mode](load-balancer-distribution-mode.md).


# Load Balancer Distribution Mode

# Configure the distribution mode for Azure Load Balancer

Azure Load Balancer supports two distribution modes for distributing traffic to your applications:

* Hash-based

* Source IP affinity

To learn more about the different distribution modes supported by Azure Load Balancer, see [Azure Load Balancer distribution modes](distribution-mode-concepts.md).

In this article, you learn how to configure the distribution mode for your Azure Load Balancer.

## Configure distribution mode

---

# [**Azure portal**](#tab/azure-portal)

You can change the configuration of the distribution mode by modifying the load-balancing rule in the portal.

1. Sign in to the Azure portal and locate the resource group containing the load balancer you wish to change by clicking on **Resource Groups**.

1. In the load balancer overview screen, select **Load-balancing rules** under **Settings**.

1. In the load-balancing rules screen, select the load-balancing rule that you wish to change the distribution mode.

1. Under the rule, the distribution mode is changed by changing the **Session persistence** drop-down box.

The following options are available:

* **None (hash-based)** - Specifies that successive requests from the same client can be handled by any virtual machine.

* **Client IP (two-tuple: source IP and destination IP)** - Specifies that successive requests from the same client IP address are handled by the same virtual machine.

* **Client IP and protocol (three-tuple: source IP, destination IP, and protocol type)** - Specifies that successive requests from the same client IP address and protocol combination are handled by the same virtual machine.

1. Choose the distribution mode and then select **Save**.

# [**PowerShell**](#tab/azure-powershell)

[!INCLUDE [updated-for-az](~/reusable-content/ce-skilling/azure/includes/updated-for-az.md)]

Use PowerShell to change the load-balancer distribution settings on an existing load-balancing rule. The following command updates the distribution mode:

```azurepowershell-interactive

$lb = Get-AzLoadBalancer -Name MyLoadBalancer -ResourceGroupName MyResourceGroupLB

$lb.LoadBalancingRules[0].LoadDistribution = 'default'

Set-AzLoadBalancer -LoadBalancer $lb

```

Set the value of the `LoadDistribution` element for the type of load balancing required.

* Specify **SourceIP** for two-tuple (source IP and destination IP) load balancing.

* Specify **SourceIPProtocol** for three-tuple (source IP, destination IP, and protocol type) load balancing.

* Specify **Default** for the default behavior of five-tuple load balancing.

# [**CLI**](#tab/azure-cli)

[!INCLUDE [azure-cli-prepare-your-environment.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment.md)]

Use Azure CLI to change the load-balancer distribution settings on an existing load-balancing rule. The following command updates the distribution mode:

```azurecli-interactive

az network lb rule update \

--lb-name myLoadBalancer \

--load-distribution Default \

--name myHTTPRule \

--resource-group myResourceGroupLB

```

Set the value of `--load-distribution` for the type of load balancing required.

* Specify **SourceIP** for two-tuple (source IP and destination IP) load balancing.

* Specify **SourceIPProtocol** for three-tuple (source IP, destination IP, and protocol type) load balancing.

* Specify **Default** for the default behavior of five-tuple load balancing.

For more information on the command used in this article, see [az network lb rule update](/cli/azure/network/lb/rule#az-network-lb-rule-update)

---

## Next steps

* [Azure Load Balancer overview](load-balancer-overview.md)

* [Get started with configuring an internet-facing load balancer](quickstart-load-balancer-standard-public-powershell.md)

* [Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)


# Load Balancer Outbound Connections

# Use Source Network Address Translation (SNAT) for outbound connections

Certain scenarios require virtual machines or compute instances to have outbound connectivity to the internet. The frontend IPs of a public load balancer can be used to provide outbound connectivity to the internet for backend instances. This configuration uses **source network address translation (SNAT)** to translate virtual machine's private IP into the load balancer's public IP address. SNAT maps the IP address of the backend to the public IP address of your load balancer. SNAT prevents outside sources from having a direct address to the backend instances.

## <a name="scenarios"></a>Azure's outbound connectivity methods

The following methods are Azure's most commonly used methods to enable outbound connectivity, listed in order of priority when multiple methods are used:

| #  | Method                                                                                           | Type of port allocation | Production-grade?      | Rating |

| -- | ------------------------------------------------------------------------------------------------ | ----------------------- | ---------------------- | ------ |

| 1  | Associate a NAT gateway to the subnet                                                            | Dynamic, explicit       | Yes                    | Best   |

| 2  | Assign a public IP to the virtual machine                                                        | Static, explicit        | Yes                    | OK     |

| 3  | Use the frontend IP address(es) of a load balancer for outbound via outbound rules              | Static, explicit        | Yes, but not at scale  | OK     |

| 4  | Use the frontend IP address(es) of a load balancer for outbound without outbound rules          | Static, Implicit        | No                     | Worst  |

| 5  | [Default outbound access](../virtual-network/ip-services/default-outbound-access.md)            | Implicit                | No                     | Worst  |

## 1. Associate a NAT gateway to the subnet

Azure NAT Gateway simplifies outbound-only Internet connectivity for virtual networks. When configured on a subnet, all outbound connectivity uses your specified static public IP addresses. Outbound connectivity is possible without load balancer or public IP addresses directly attached to virtual machines. NAT Gateway is fully managed and highly resilient.

Using a NAT gateway is the best method for outbound connectivity. A NAT gateway is highly extensible, reliable, and doesn't have the same concerns of SNAT port exhaustion.

NAT gateway takes precedence over other outbound connectivity methods, including a load balancer, instance-level public IP addresses, and Azure Firewall.

For more information about Azure NAT Gateway, see [What is Azure NAT Gateway](../virtual-network/nat-gateway/nat-overview.md).

For details on how SNAT behavior works with NAT Gateway, see [SNAT with NAT Gateway](/azure/nat-gateway/nat-gateway-snat).

##  2. Assign a public IP to the virtual machine

| Associations                  | Method                                                                      | IP protocols                                                                                                                                         |

| ----------------------------- | --------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |

| Public IP on VM's NIC         | SNAT (Source Network Address Translation) </br> isn't used.                | TCP (Transmission Control Protocol) </br> UDP (User Datagram Protocol) </br> ICMP (Internet Control Message Protocol) </br> ESP (Encapsulating Security Payload) |

Traffic returns to the requesting client from the virtual machine's public IP address (Instance Level IP).

Azure uses the public IP assigned to the IP configuration of the instance's NIC for all outbound flows. The instance has all ephemeral ports available. It doesn't matter whether the VM is load balanced or not. This scenario takes precedence over the others, except for NAT Gateway.

A public IP assigned to a VM is a 1:1 relationship (rather than 1: many) and implemented as a stateless 1:1 NAT.

## <a name="outboundrules"></a>3. Use the frontend IP address(es) of a load balancer for outbound via outbound rules

Outbound rules enable you to explicitly define SNAT (source network address translation) for a standard SKU public load balancer. This configuration allows you to use the public IP or IPs of your load balancer for outbound connectivity of the backend instances.

This configuration enables:

- IP masquerading

- Simplifying your allowlists

- Reduces the number of public IP resources for deployment

With outbound rules, you have full declarative control over outbound internet connectivity. Outbound rules allow you to scale and tune this ability to your specific needs via manual port allocation. Manually allocating SNAT port based on the backend pool size and number of **frontendIPConfigurations** can help avoid SNAT exhaustion.

You can manually allocate SNAT ports either by "ports per instance" or "maximum number of backend instances". If you have virtual machines in the backend, it's recommended that you allocate ports by "ports per instance" to get maximum SNAT port usage.

Calculate ports per instance as follows:

**Number of frontend IPs * 64K / Number of backend instances**

If you have Virtual Machine Scale Sets in the backend, it's recommended to allocate ports by "maximum number of backend instances". If more VMs are added to the backend than remaining SNAT ports allowed, scale out of Virtual Machine Scale Sets could be blocked, or the new VMs won't receive sufficient SNAT ports.

> [!NOTE]

> When multiple frontend IPs are configured using outbound rules, outbound connections can come from any of the frontend IPs configured to the backend instance. We don't recommend building any dependencies on which frontend IP can be selected for connections.

For more information about outbound rules, see [Outbound rules](outbound-rules.md).

## 4. Use the frontend IP address(es) of a load balancer for outbound without outbound rules

This option is similar to the previous one, except when no outbound rules are created. In this case, the load balancer frontend(s) are still used for outbound, but this is done implicitly without rules that specify which frontend would be used. Not using outbound rules also decreases scalability of outbound, as implicit outbound connectivity has a fixed number of SNAT ports per frontend IP address, which could lead to port exhaustion in high-traffic scenarios.

## 5. Default outbound access

In Azure, virtual machines created in a virtual network without explicit outbound connectivity defined are assigned to a default outbound public IP address. This IP address enables outbound connectivity from the resources to the Internet. This access is referred to as [default outbound access](../virtual-network/ip-services/default-outbound-access.md). This method of access is **not recommended** as it's insecure and the IP addresses are subject to change.

> [!IMPORTANT]

> On March 31, 2026, new virtual networks will default to using private subnets. For more information, see the [official announcement](https://azure.microsoft.com/updates?id=default-outbound-access-for-vms-in-azure-will-be-retired-transition-to-a-new-method-of-internet-access). It is recommended to use one the explicit forms of connectivity as shown in options 1-3 above.

### What are SNAT ports?

Ports are used to generate unique identifiers used to maintain distinct flows. The internet uses a five-tuple to provide this distinction.

If a port is used for inbound connections, it has a **listener** for inbound connection requests on that port. That port can't be used for outbound connections. To establish an outbound connection, an **ephemeral port** is used to provide the destination with a port on which to communicate and maintain a distinct traffic flow. When these ephemeral ports are used for SNAT, they're called **SNAT ports**.

By definition, every IP address has 65,535 ports. Each port can either be used for inbound or outbound connections for TCP (Transmission Control Protocol) and UDP (User Datagram Protocol). When a public IP address is added as a frontend IP to a load balancer, 64,000 ports are eligible for SNAT.

Each port used in a load balancing or inbound NAT rule consumes a range of eight ports from the 64,000 available SNAT ports. This usage reduces the number of ports eligible for SNAT, if the same frontend IP is used for outbound connectivity. If load-balancing or inbound NAT rules consumed ports are in the same block of eight ports consumed by another rule, the rules don't require extra ports.

> [!NOTE]

> If you need to connect to any [supported Azure PaaS services](../private-link/availability.md) like Azure Storage, Azure SQL, or Azure Cosmos DB, you can use Azure Private Link to avoid SNAT entirely. Azure Private Link sends traffic from your virtual network to Azure services over the Azure backbone network instead of over the internet.

>

> Private Link is the recommended option over service endpoints for private access to Azure hosted services. For more information on the difference between Private Link and service endpoints, see [Compare Private Endpoints and Service Endpoints](../virtual-network/vnet-integration-for-azure-services.md#compare-private-endpoints-and-service-endpoints).

### How does default SNAT work?

When a VM creates an outbound flow, Azure translates the source IP address to an ephemeral IP address. This translation is done via SNAT.

If using SNAT without outbound rules via a public load balancer, SNAT ports are pre-allocated as described in the following default SNAT ports allocation table:

## <a name="preallocatedports"></a> Default port allocation table

When default port allocation is enabled, SNAT ports are allocated by default based on the backend pool size. Backends receive the number of ports defined by the table, per frontend IP, up to a maximum of 1024 ports. Default port allocation is NOT recommended for production workloads, as doing so allocates a minimal number of ports to each backend instance and increases the risk of SNAT port exhaustion. Instead, consider using NAT Gateway or manually allocating ports on your load balancer outbound rules.

There are multiple ways default port allocation can be enabled:

- Configuring a load balancing rule with disableOutboundSnat set to false, or by selecting the default port allocation option on a load balancer rule in the Azure portal

- Configuring an outbound rule but setting the allocatedOutboundPorts	property to 0, or by selecting "Enable default port allocation" in the Azure portal

As an example, with 100 VMs in a backend pool and only one frontend IP, each VM receives 512 ports. If a second frontend IP is added, each VM receives an extra 512 ports. This means each VM is allocated a total of 1,024 ports. As a result, adding a third frontend IP will NOT increase the number of allocated SNAT ports beyond 1024 ports.

As a rule of thumb, the number of SNAT ports provided when default port allocation is applied can be computed as: MIN(# of default SNAT ports provided based on pool size * number of frontend IPs associated with the pool, 1024)

The following <a name="snatporttable"></a>table shows the SNAT port preallocations for a single frontend IP, depending on the backend pool size:

| Pool size (VM instances) | Default SNAT ports |

| ------------------------ | ------------------ |

| 1-50                     | 1,024              |

| 51-100                   | 512                |

| 101-200                  | 256                |

| 201-400                  | 128                |

| 401-800                  | 64                 |

| 801-1,000                | 32                 |

## Port exhaustion

Every connection to the same destination IP and destination port uses a SNAT port. This connection maintains a distinct **traffic flow** from the backend instance or **client** to a **server**. This process gives the server a distinct port on which to address traffic. Without this process, the client machine is unaware of which flow a packet is part of.

Imagine having multiple browsers going to https://www.microsoft.com, which is:

* Destination IP = 23.53.254.142

* Destination Port = 443

* Protocol = TCP

Without SNAT ports for the return traffic, the client has no way to separate one query result from another.

Outbound connections can burst. A backend instance can be allocated insufficient ports. Use **connection reuse** functionality within your application. Without **connection reuse**, the risk of SNAT **port exhaustion** is increased.

For more information about connection pooling with Azure App Service, see [Troubleshooting intermittent outbound connection errors in Azure App Service](../app-service/troubleshoot-intermittent-outbound-connection-errors.md#avoiding-the-problem)

New outbound connections to a destination IP fail when port exhaustion occurs. Connections succeed when a port becomes available. This exhaustion occurs when the 64,000 ports from an IP address are spread thin across many backend instances. For guidance on mitigation of SNAT port exhaustion, see [Support and troubleshooting for Azure Load Balancer](./load-balancer-support-help.md).

## Port reuse

For TCP connections, the load balancer uses a single SNAT port for every destination IP and port. For connections to the same destination IP, a single SNAT port can be reused as long as the destination port differs. Reuse isn't possible when there already exists a connection to the same destination IP and port.

For UDP connections, the load balancer uses a **port-restricted cone NAT** algorithm, which consumes one SNAT port per destination IP, regardless of the destination port.

Individual ports can be reused for an unlimited number of connections where reuse is permitted (when the destination IP or port is different).

In the example in the following table, a backend instance with private IP 10.0.0.1 is making TCP connections to destination IPs 23.53.254.142 and 26.108.254.155, while the load balancer is configured with frontend IP address 192.0.2.0. Because the destination IPs are different, the same SNAT port can be reused for multiple connections.

| Flow | Source tuple | Source tuple after SNAT | Destination tuple    |

| ---- | ------------ | ----------------------- | -------------------- |

| 1    | 10.0.0.1:80  | 192.0.2.0:1             | 23.53.254.142:80     |

| 2    | 10.0.0.1:80  | 192.0.2.0:1             | 26.108.254.155:80    |

## Constraints

*	When a connection is idle with no new packets being sent, the ports will be released after 4 – 120 minutes.

*	This threshold can be configured via outbound rules.

*	Each IP address provides 64,000 ports that can be used for SNAT.

*	Each port can be used for both TCP and UDP connections to a destination IP address

*	A UDP SNAT port is needed whether the destination port is unique or not. For every UDP connection to a destination IP, one UDP SNAT port is used.

*	A TCP SNAT port can be used for multiple connections to the same destination IP provided the destination ports are different.

*	SNAT exhaustion occurs when a backend instance runs out of given SNAT Ports. A load balancer can still have unused SNAT ports. If a backend instance’s used SNAT ports exceed its given SNAT ports, it's unable to establish new outbound connections.

*	Fragmented packets are dropped unless outbound is through an instance level public IP on the VM's NIC.

*	Secondary IPv4 configurations of a network interface aren't supported with outbound rules. For outbound connectivity on secondary IPv4 configurations, attach instance level public IPs or use NAT Gateway instead.

## Next steps

*	[Support and troubleshooting for Azure Load Balancer](./load-balancer-support-help.md)

*	[Review SNAT metrics](./load-balancer-standard-diagnostics.md#how-do-i-check-my-snat-port-usage-and-allocation) and familiarize yourself with the correct way to filter, split, and view them.

*	Learn how to [migrate your existing outbound connectivity method to NAT gateway](../virtual-network/nat-gateway/tutorial-migrate-outbound-nat.md)


# Outbound Rules

# <a name="outboundrules"></a>Outbound rules Azure Load Balancer

Outbound rules allow you to explicitly define SNAT(source network address translation) for a public standard load balancer. This configuration allows you to use the public IPs of your load balancer to provide outbound internet connectivity for your backend instances.

This configuration enables:

* IP masquerading

* Simplifying your allow lists.

* Reduces the number of public IP resources for deployment.

With outbound rules, you have full declarative control over outbound internet connectivity. Outbound rules allow you to scale and tune this ability to your specific needs.

Outbound rules will only be followed if the backend VM doesn't have an instance-level public IP address (ILPIP).

With outbound rules, you can explicitly define outbound **SNAT** behavior.

Outbound rules allow you to control:

* **Which virtual machines are translated to which public IP addresses.**

* Two rules where backend pool 1 uses both blue IP addresses, and backend pool 2 uses the yellow IP prefix.

* **How outbound SNAT ports are allocated.**

* If backend pool 2 is the only pool making outbound connections, give all SNAT ports to backend pool 2 and none to backend pool 1.

* **Which protocols to provide outbound translation for.**

* If backend pool 2 needs UDP ports for outbound, and backend pool 1 needs TCP, give TCP ports to 1 and UDP ports to 2.

* **What duration to use for outbound connection idle timeout (4-120 minutes).**

* If there are long running connections with keepalives, reserve idle ports for long running connections for up to 120 minutes. Assume stale connections are abandoned and release ports in 4 minutes for fresh connections

* **Whether to send a TCP Reset on idle timeout.**

* When timing out idle connections, do we send a TCP RST to the client and server so they know the flow is abandoned?

> [!IMPORTANT]

> When a backend pool is configured by IP address, it will behave as a Basic Load Balancer with default outbound enabled. For secure by default configuration and applications with demanding outbound needs, configure the backend pool by NIC.

## Outbound rule definition

Outbound rules follow the same familiar syntax as load balancing and inbound NAT rules: **frontend** + **parameters** + **backend pool**.

An outbound rule configures outbound NAT for _all virtual machines identified by the backend pool_ to be translated to the _frontend_.

The _parameters_ provide fine grained control over the outbound NAT algorithm.

## <a name="scale"></a> Scale outbound NAT with multiple IP addresses

Each extra IP address provided by a frontend provides another 64,000 ephemeral ports for load balancer to use as SNAT ports. Load balancer uses IPs as needed based on the available ports. The Load balancer will use the next IP once the connections can no longer be made with the current IP in use.

Use multiple IP addresses to plan for large-scale scenarios. Use outbound rules to mitigate SNAT exhaustion as described in [Support and troubleshooting for Azure Load Balancer](load-balancer-support-help.md).

You can also use a [public IP prefix](./load-balancer-outbound-connections.md#outboundrules) directly with an outbound rule.

A public IP prefix increases scaling of your deployment. The prefix can be added to the allow list of flows originating from your Azure resources. You can configure a frontend IP configuration within the load balancer to reference a public IP address prefix.

The load balancer has control over the public IP prefix. The outbound rule will automatically use other public IP addresses contained within the public IP prefix after no more outbound connections can be made with the current IP in use from the prefix.

Each of the IP addresses within public IP prefix provides an extra 64,000 ephemeral ports per IP address for load balancer to use as SNAT ports.

## <a name="idletimeout"></a> Outbound flow idle timeout and TCP reset

Outbound rules provide a configuration parameter to control the outbound flow idle timeout and match it to the needs of your application. Outbound idle timeouts default to 4 minutes. For more information, see [configure idle timeouts](load-balancer-tcp-idle-timeout.md).

The default behavior of load balancer is to drop the flow silently when the outbound idle timeout has been reached. The `enableTCPReset` parameter enables a predictable application behavior and control. The parameter dictates whether to send bidirectional TCP Reset (TCP RST) at the timeout of the outbound idle timeout.

Review [TCP Reset on idle timeout](./load-balancer-tcp-reset.md) for details including region availability.

## <a name="preventoutbound"></a>Securing and controlling outbound connectivity explicitly

Load-balancing rules provide automatic programming of outbound NAT. Some scenarios benefit or require you to disable the automatic programming of outbound NAT by the load-balancing rule. Disabling via the rule allows you to control or refine the behavior.

You can use this parameter in two ways:

1. Prevention of the inbound IP address for outbound SNAT. Disable outbound SNAT in the load-balancing rule.

1. Tune the outbound **SNAT** parameters of an IP address used for inbound and outbound simultaneously. The automatic outbound NAT must be disabled to allow an outbound rule to take control. To change the SNAT port allocation of an address also used for inbound, the `disableOutboundSnat` parameter must be set to true.

The operation to configure an outbound rule fails if you attempt to redefine an IP address that is used for inbound.Disable the outbound NAT of the load-balancing rule first.

> [!IMPORTANT]

> Your virtual machine won't have outbound connectivity if you set this parameter to true and don't have an outbound rule to define outbound connectivity. Some operations of your VM or your application can depend on having outbound connectivity available. Make sure you understand the dependencies of your scenario and have considered impact of making this change.

Sometimes it's undesirable for a VM to create an outbound flow. There might be a requirement to manage which destinations receive outbound flows, or which destinations begin inbound flows. Use [network security groups](../virtual-network/network-security-groups-overview.md) to manage the destinations that the VM reaches. Use NSGs to manage which public destinations start inbound flows.

When you apply an NSG to a load-balanced VM, pay attention to the [service tags](../virtual-network/network-security-groups-overview.md#service-tags) and [default security rules](../virtual-network/network-security-groups-overview.md#default-security-rules).

Ensure that the VM can receive health probe requests from Azure Load Balancer.

If an NSG blocks health probe requests from the AZURE_LOADBALANCER default tag, your VM health probe fails and the VM is marked unavailable. The load balancer stops sending new flows to that VM.

## Outbound rules scenarios

* [Configure outbound connections to a specific set of public IPs or prefix](#scenario1out).

* [Modify SNAT port allocation](#scenario2out).

* [Enable outbound only](#scenario3out).

* [Outbound NAT for VMs only (no inbound)](#scenario4out).

* [Outbound NAT for internal standard load balancer](#scenario5out).

* [Enable both TCP & UDP protocols for outbound NAT with a public standard load balancer](#scenario6out).

### <a name="scenario1out"></a>Scenario 1: Configure outbound connections to a specific set of public IPs or prefix

#### Details

Use this scenario to tailor outbound connections to originate from a set of public IP addresses. Add public IPs or prefixes to an allow or block list based on origination.

This public IP or prefix can be the same as used by a load-balancing rule.

To use a different public IP or prefix than what is used by a load-balancing rule:

1. Create public IP prefix or public IP address.

1. Create a public standard load balancer

1. Create a frontend referencing the public IP prefix or public IP address you wish to use.

1. Reuse a backend pool or create a backend pool and place the VMs into a backend pool of the public load balancer

1. Configure an outbound rule on the public load balancer to enable outbound NAT for the VMs using the frontend. It isn't recommended to use a load-balancing rule for outbound. Disable outbound SNAT on the load-balancing rule.

### <a name="scenario2out"></a>Scenario 2: Modify [SNAT](load-balancer-outbound-connections.md) port allocation

#### Details

You can use outbound rules to tune the [automatic SNAT port allocation based on backend pool size](load-balancer-outbound-connections.md#preallocatedports).

If you experience SNAT exhaustion, increase the number of [SNAT](load-balancer-outbound-connections.md) ports given from the default of 1024.

Each public IP address contributes up to 64,000 ephemeral ports. The number of VMs in the backend pool determines the number of ports distributed to each VM. One VM in the backend pool has access to the maximum of 64,000 ports. For two VMs, a maximum of 32,000 [SNAT](load-balancer-outbound-connections.md) ports can be given with an outbound rule (2x 32,000 = 64,000).

You can use outbound rules to tune the SNAT ports given by default. You give more or less than the default [SNAT](load-balancer-outbound-connections.md) port allocation provides. Each public IP address from a frontend of an outbound rule contributes up to 64,000 ephemeral ports for use as [SNAT](load-balancer-outbound-connections.md) ports.

Load balancer gives [SNAT](load-balancer-outbound-connections.md) ports in multiples of 8. If you provide a value not divisible by 8, the configuration operation is rejected. Each load balancing rule and inbound NAT rule consume a range of eight ports. If a load balancing or inbound NAT rule shares the same range of 8 as another, no extra ports are consumed.

If you attempt to give out more [SNAT](load-balancer-outbound-connections.md) ports than are available (based on the number of public IP addresses), the configuration operation is rejected. For example, if you give 10,000 ports per VM and seven VMs in a backend pool share a single public IP, the configuration is rejected. Seven multiplied by 10,000 exceeds the 64,000 port limit. Add more public IP addresses to the frontend of the outbound rule to enable the scenario.

Revert to the [default port allocation](load-balancer-outbound-connections.md#preallocatedports) by specifying 0 for the number of ports. For more information on default SNAT port allocation, see [SNAT ports allocation table](./load-balancer-outbound-connections.md#preallocatedports).

### <a name="scenario3out"></a>Scenario 3: Enable outbound only

#### Details

Use a public standard load balancer to provide outbound NAT for a group of VMs. In this scenario, use an outbound rule by itself, without configuring extra rules.

> [!NOTE]

> **Azure NAT Gateway** can provide outbound connectivity for virtual machines without the need for a load balancer. See [What is Azure NAT Gateway?](../virtual-network/nat-gateway/nat-overview.md) for more information.

### <a name="scenario4out"></a>Scenario 4: Outbound NAT for VMs only (no inbound)

> [!NOTE]

> **Azure NAT Gateway** can provide outbound connectivity for virtual machines without the need for a load balancer. See [What is Azure NAT Gateway?](../virtual-network/nat-gateway/nat-overview.md) for more information.

#### Details

For this scenario:

Azure Load Balancer outbound rules and Virtual Network NAT are options available for egress from a virtual network.

1. Create a public IP or prefix.

1. Create a public standard load balancer.

1. Create a frontend associated with the public IP or prefix dedicated for outbound.

1. Create a backend pool for the VMs.

1. Place the VMs into the backend pool.

1. Configure an outbound rule to enable outbound NAT.

Use a prefix or public IP to scale [SNAT](load-balancer-outbound-connections.md) ports. Add the source of outbound connections to an allow or block list.

### <a name="scenario5out"></a>Scenario 5: Outbound NAT for internal standard load balancer

> [!NOTE]

> **Azure NAT Gateway** can provide outbound connectivity for virtual machines utilizing an internal standard load balancer. See [What is Azure NAT Gateway?](../virtual-network/nat-gateway/nat-overview.md) for more information.

#### Details

Outbound connectivity isn't available for an internal standard load balancer until it has been explicitly declared through instance-level public IPs or Virtual Network NAT, or by associating the backend pool members with an outbound-only load balancer configuration.

For more information, see [Outbound-only load balancer configuration](./egress-only.md).

### <a name="scenario6out"></a>Scenario 6: Enable both TCP & UDP protocols for outbound NAT with a public standard load balancer

#### Details

With a public standard load balancer, the automatic outbound NAT provided matches the transport protocol of the load-balancing rule.

1. Disable outbound [SNAT](load-balancer-outbound-connections.md) on the load-balancing rule.

1. Configure an outbound rule on the same load balancer.

1. Reuse the backend pool already used by your VMs.

1. Specify "protocol": "All" as part of the outbound rule.

When only inbound NAT rules are used, no outbound NAT is provided.

1. Place VMs in a backend pool.

1. Define one or more frontend IP configurations with public IP addresses or public IP prefix

1. Configure an outbound rule on the same load balancer.

1. Specify "protocol": "All" as part of the outbound rule

## Limitations

- The maximum number of usable ephemeral ports per frontend IP address is 64,000.

- The range of the configurable outbound idle timeout is 4 to 120 minutes (240 to 7200 seconds).

- Load balancer doesn't support ICMP for outbound NAT, the only supported protocols are TCP and UDP.

- Outbound rules can only be applied to primary IPv4 configuration of a NIC. You can't create an outbound rule for the secondary IPv4 configurations of a VM or NVA. Multiple NICs are supported.

- Outbound rules for the secondary IP configuration are only supported for IPv6.

- All virtual machines within an **availability set** must be added to the backend pool for outbound connectivity.

- All virtual machines within a **virtual machine scale set** must be added to the backend pool for outbound connectivity.

## Next steps

- Learn more about [Azure Standard Load Balancer](load-balancer-overview.md)

- See our [frequently asked questions about Azure Load Balancer](load-balancer-faqs.yml)


# Egress Only

# Outbound-only load balancer configuration

Use a combination of internal and external standard load balancers to create outbound connectivity for VMs behind an internal load balancer.

This configuration provides outbound NAT for an internal load balancer scenario, producing an "egress only" setup for your backend pool.

> [!NOTE]

> **Azure NAT Gateway** is the recommended configuration for outbound connectivity in production deployments. NAT Gateway is available in two SKUs: **Standard** (zonal) and **StandardV2** (zone-redundant, with IPv6 support, 100 Gbps throughput, and flow logs). For more information about **NAT Gateway**, see **[What is Azure NAT Gateway?](../nat-gateway/nat-overview.md)**

>

> To deploy an outbound only load balancer configuration with Azure NAT Gateway, see [Tutorial: Integrate NAT gateway with an internal load balancer - Azure portal](../nat-gateway/tutorial-nat-gateway-load-balancer-internal-portal.md).

>

> For more information about outbound connections in Azure and default outbound access, see [Source Network Address Translation (SNAT) for outbound connections](load-balancer-outbound-connections.md) and [Default outbound access](../virtual-network/ip-services/default-outbound-access.md).

*Figure: Egress only load balancer configuration*

> [!IMPORTANT]

> On March 31, 2026, new virtual networks default to using private subnets, and [default outbound access](../virtual-network/ip-services/default-outbound-access.md) is no longer provided. Use an explicit form of outbound connectivity, such as NAT Gateway. For more information, see the [official announcement](https://azure.microsoft.com/updates?id=default-outbound-access-for-vms-in-azure-will-be-retired-transition-to-a-new-method-of-internet-access).

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Create a virtual network and bastion host

[!INCLUDE [load-balancer-create-no-gateway](../../includes/load-balancer-create-no-gateway.md)]

## Create internal load balancer

In this section, you create the internal load balancer.

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

1. In the **Load balancer** page, select **Create**.

1. In the **Basics** tab of the **Create load balancer** page, enter, or select the following information:

| Setting                 | Value                                              |

| ---                     | ---                                                |

| **Project details** |   |

| Subscription               | Select your subscription.    |

| Resource group         | Select **load-balancer-rg**. |

| **Instance details** |   |

| Name                   | Enter **lb-internal**                                   |

| Region         | Select **(US) East US**.                                        |

| SKU           | Leave the default **Standard**. |

| Type          | Select **Internal**.                                        |

1. Select **Next: Frontend IP configuration** at the bottom of the page.

1. In **Frontend IP configuration**, select **+ Add a frontend IP configuration**.

1. Enter **lb-int-frontend** in **Name**.

1. Select **lb-vnet** in **Virtual Network**.

1. Select **backend-subnet** in **Subnet**.

1. Select **Dynamic** for **Assignment**.

1. Select **Zone-redundant** in **Availability zone**.

> [!NOTE]

> In regions with [Availability Zones](/azure/reliability/availability-zones-overview?toc=%2fazure%2fvirtual-network%2ftoc.json), you can select zone-redundant (default option) or a specific zone. The choice depends on your specific domain failure requirements. In regions without Availability Zones, this field doesn't appear. For more information on availability zones, see [Availability zones overview](/azure/reliability/availability-zones-overview).

1. Select **Add**.

1. Select **Next: Backend pools** at the bottom of the page.

1. In the **Backend pools** tab, select **+ Add a backend pool**.

1. Enter **lb-int-backend-pool** for **Name** in **Add backend pool**.

1. Select **NIC** or **IP Address** for **Backend Pool Configuration**.

1. Select **Save**.

1. Select the blue **Review + create** button at the bottom of the page.

1. Select **Create**.

## Create public load balancer

In this section, you create the public load balancer.

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

1. In the **Load balancer** page, select **Create**.

1. In the **Basics** tab of the **Create load balancer** page, enter, or select the following information:

| Setting                 | Value                                              |

| ---                     | ---                                                |

| **Project details** |   |

| Subscription               | Select your subscription.    |

| Resource group         | Select **load-balancer-rg**. |

| **Instance details** |   |

| Name                   | Enter **lb-public**                                   |

| Region         | Select **(US) East US**.                                        |

| SKU           | Leave the default **Standard**. |

| Type          | Select **Public**.                                        |

| Tier          | Leave the default **Regional**. |

1. Select **Next: Frontend IP configuration** at the bottom of the page.

1. In **Frontend IP configuration**, select **+ Add a frontend IP**.

1. Enter **lb-ext-frontend** in **Name**.

1. Select **IPv4** or **IPv6** for the **IP version**.

> [!NOTE]

> IPv6 isn't currently supported with Routing Preference or Cross-region load-balancing (Global Tier).

1. Select **IP address** for the **IP type**.

> [!NOTE]

> For more information on IP prefixes, see [Azure Public IP address prefix](../virtual-network/ip-services/public-ip-address-prefix.md).

1. Select **Create new** in **Public IP address**.

1. In **Add a public IP address**, enter **lb-public-ip** for **Name**.

1. Select **Zone-redundant** in **Availability zone**.

> [!NOTE]

> In regions with [Availability Zones](/azure/reliability/availability-zones-overview?toc=%2fazure%2fvirtual-network%2ftoc.json), you can select zone-redundant (default option) or a specific zone. The choice depends on your specific domain failure requirements. In regions without Availability Zones, this field doesn't appear. For more information on availability zones, see [Availability zones overview](/azure/reliability/availability-zones-overview).

1. Leave the default of **Microsoft Network** for **Routing preference**.

1. Select **OK**.

1. Select **Add**.

1. Select **Next: Backend pools** at the bottom of the page.

1. In the **Backend pools** tab, select **+ Add a backend pool**.

1. Enter **lb-pub-backend-pool** for **Name** in **Add backend pool**.

1. Select **lb-vnet** in **Virtual network**.

1. Select **NIC** or **IP Address** for **Backend Pool Configuration**.

1. Select **Save**.

1. Select the blue **Review + create** button at the bottom of the page.

1. Select **Create**.

## Create virtual machine

Create a virtual machine in this section. During creation, add it to the backend pool of the internal load balancer. After the virtual machine is created, add the virtual machine to the backend pool of the public load balancer.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. In **Virtual machines**, select **+ Create** > **Virtual machine**.

1. In **Create a virtual machine**, enter or select the values in the **Basics** tab:

| Setting | Value                                          |

|-----------------------|----------------------------------|

| **Project Details** |  |

| Subscription | Select your Azure subscription |

| Resource Group | Select **load-balancer-rg** |

| **Instance details** |  |

| Virtual machine name | Enter **lb-VM** |

| Region | Select **(US) East US** |

| Availability Options | Select **No infrastructure redundancy required** |

| Security type | Select **Standard**. |

| Image | Select **Windows Server 2022 Datacenter: Azure Edition - Gen2** |

| Azure Spot instance | Leave the default of unchecked. |

| Size | Choose VM size or take default setting |

| **Administrator account** |  |

| Username | Enter a username |

| Password | Enter a password |

| Confirm password | Reenter password |

| **Inbound port rules** |  |

| Public inbound ports | Select **None** |

1. Select the **Networking** tab, or select **Next: Disks**, and then **Next: Networking**.

1. In the Networking tab, select or enter:

| Setting | Value |

|-|-|

| **Network interface** |  |

| Virtual network | **lb-vnet** |

| Subnet | **backend-subnet** |

| Public IP | Select **None**. |

| NIC network security group | Select **Advanced**|

| Configure network security group | Leave the default of **vm-NSG**. This value might be different if you choose a different name for your VM. |

1. Under **Load balancing**, select the following values:

| Setting | Value |

|-|-|

| Load-balancing options | Select **Azure load balancing** |

| Select a load balancer | Select **lb-internal**  |

| Select a backend pool | Select **lb-int-backend-pool** |

1. Select **Review + create**.

1. Review the settings, and then select **Create**.

## Add VM to backend pool of public load balancer

In this section, you add the virtual machine you created previously to the backend pool of the public load balancer.

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

1. Select **lb-public**.

1. Select **Backend pools** in **Settings** in **lb-public**.

1. Select **lb-pub-backend-pool** under **Backend pool** in the **Backend pools** page.

1. In **lb-pub-backend-pool**, select **lb-vnet** in **Virtual network**.

1. In **Virtual machines**, select the blue **+ Add** button.

1. Select the box next to **lb-VM** in **Add virtual machines to backend pool**.

1. Select **Add**.

1. Select **Save**.

## Test connectivity before outbound rule

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **lb-VM**.

1. In the **Overview** page, select **Connect**, and then select **Bastion**.

1. Enter the username and password that you provided during VM creation.

1. Select **Connect**.

1. Open Microsoft Edge browser.

1.  Enter **https://ifconfig.me** in the address bar.

1.  The connection fails. By default, standard public load balancer [doesn't allow outbound traffic without a defined outbound rule](load-balancer-overview.md#securebydefault).

## Create a public load balancer outbound rule

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

1. Select **lb-public**.

1. Select **Outbound rules** in **Settings** in **lb-public**.

1. Select **+ Add** in **Outbound rules**.

1. Enter or select the following information to configure the outbound rule.

| Setting | Value |

| ------- | ----- |

| Name | Enter **myOutboundRule**. |

| Frontend IP address | Select **lb-ext-frontend**.|

| Protocol | Leave the default of **All**. |

| Idle timeout (minutes) | Move slider to **15 minutes**.|

| TCP Reset | Select **Enabled**.|

| Backend pool | Select **lb-pub-backend-pool**.|

| **Port allocation** |  |

| Port allocation | Select **Manually choose number of outbound ports**. |

| **Outbound ports** |  |

| Choose by | Select **Ports per instance**. |

| Ports per instance | Enter **10000**.

1. Select **Add**.

## Test connectivity after outbound rule

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **lb-VM**.

1. On the **Overview** page, select **Connect**, and then select **Bastion**.

1. Enter the username and password that you provided during VM creation.

1. Select **Connect**.

1. Open Microsoft Edge browser.

1. Enter **https://ifconfig.me** in the address bar.

1. The connection succeeds.

1. The IP address displayed is the frontend IP address of **lb-public**.

## Clean up resources

When you no longer need the resources, delete the resource group, load balancers, VM, and all related resources.

Select the resource group **load-balancer-rg** and then select **Delete**.

## Next steps

In this article, you created an "egress only" configuration by using a combination of public and internal load balancers.

This configuration balances incoming internal traffic to your backend pool while preventing any public inbound connections.

For more information about Azure Load Balancer and Azure Bastion, see [What is Azure Load Balancer?](load-balancer-overview.md) and [What is Azure Bastion?](../bastion/bastion-overview.md)


# Load Balancer Ipv6 For Linux

# Configure DHCPv6 for Linux VMs

Some of the Linux virtual-machine images in the Azure Marketplace don't have Dynamic Host Configuration Protocol version 6 (DHCPv6) configured by default. To support IPv6, DHCPv6 must be configured in the Linux OS distribution that you're using. The various Linux distributions configure DHCPv6 in various ways because they use different packages.

> [!NOTE]

> Recent SUSE Linux and CoreOS images in the Azure Marketplace have been pre-configured with DHCPv6. No additional changes are required when you use these images.

This document describes how to enable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.

> [!WARNING]

> By improperly editing network configuration files, you can lose network access to your VM. We recommended that you test your configuration changes on non-production systems. The instructions in this article have been tested on the latest versions of the Linux images in the Azure Marketplace. For more detailed instructions, consult the documentation for your own version of Linux.

# [RHEL/Oracle](#tab/redhat)

For RHEL and Oracle Linux versions 7.4 or higher, follow these steps:

1. Edit the */etc/sysconfig/network* file, and add the following parameter:

```config

NETWORKING_IPV6=yes

```

2. Edit the */etc/sysconfig/network-scripts/ifcfg-eth0* file, and add the following two parameters:

```config

IPV6INIT=yes

DHCPV6C=yes

```

3. Renew the IPv6 address:

```bash

sudo ifdown eth0 && sudo ifup eth0

```

# [openSUSE/SLES](#tab/suse)

Recent SUSE Linux Enterprise Server (SLES) and openSUSE images in Azure have been preconfigured with DHCPv6. No other changes are required when you use these images. If you have a VM that's based on an older or custom SUSE image, use one of the following procedures to configure DHCPv6.

## openSUSE 13 and SLES 11

1. Install the `dhcp-client` package, if needed:

```bash

sudo zypper install dhcp-client

```

2. Edit the */etc/sysconfig/network/ifcfg-eth0* file, and add the following parameter:

```config

DHCLIENT6_MODE='managed'

3. Renew the IPv6 address:

```bash

sudo ifdown eth0 && sudo ifup eth0

```

## openSUSE Leap and SLES 12

For openSUSE Leap and SLES 12, follow these steps:

1. Edit the */etc/sysconfig/network/ifcfg-eth0* file, and replace the `#BOOTPROTO='dhcp4'` parameter with the following value:

```config

BOOTPROTO='dhcp'

```

2. To the */etc/sysconfig/network/ifcfg-eth0* file, add the following parameter:

```config

DHCLIENT6_MODE='managed'

```

3. Renew the IPv6 address:

```bash

sudo ifdown eth0 && sudo ifup eth0

```

# [Ubuntu](#tab/ubuntu)

For Ubuntu versions 17.10 or higher, follow these steps:

1. Edit the **`/etc/dhcp/dhclient.conf`** file, and add the following line:

```config

timeout 10;

```

1. Create a new file in the cloud.cfg.d folder that retains your configuration through reboots. **The information in this file will override the default [NETPLAN]( https://netplan.io) config (in YAML configuration files at this location: /etc/netplan/*.yaml)**.

Create a */etc/cloud/cloud.config.d/91-azure-network.cfg* file.  Ensure that **`dhcp6: true`** is reflected under the required interface, as shown by the following sample:

```config

network:

version: 2

ethernets:

eth0:

dhcp4: true

dhcp6: true

match:

driver: hv_netvsc

set-name: eth0

```

1. Save the file and reboot.

1. Use **`ifconfig`** to verify virtual machine received IPv6 address.

If **`ifconfig`** isn't installed, run the following commands:

```bash

sudo apt update

sudo apt install net-tools

```

# [Debian](#tab/debian)

All supported Debian images in Azure have been preconfigured with DHCPv6. No other changes are required when you use these images. If you have a VM based on an older or custom Debian image, follow these steps:

1. Edit the */etc/dhcp/dhclient6.conf* file, and add the following line:

```config

timeout 10;

```

1. Edit the */etc/network/interfaces* file, and add the following configuration:

```config

iface eth0 inet6 auto

up sleep 5

up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

```

1. Renew the IPv6 address:

```bash

sudo ifdown eth0 && sudo ifup eth0

```

## [CoreOS](#tab/coreos)

Recent CoreOS images in Azure have been preconfigured with DHCPv6. No other changes are required when you use these images. If you have a VM based on an older or custom CoreOS image, follow these steps:

1. Edit the */etc/systemd/network/10_dhcp.network* file:

```config

[Match]

eth0

[Network]

DHCP=ipv6

```

2. Renew the IPv6 address:

```bash

sudo systemctl restart systemd-networkd

```

---


# Deploy Ipv4 Ipv6 Dual Stack Standard Load Balancer

# Deploy IPv6 dual stack application with Azure Load Balancer

This article shows you how to deploy a dual stack (IPv4 + IPv6) application using Standard Load Balancer in Azure. The scenario includes a dual stack virtual network with a dual stack subnet, a Standard Load Balancer with dual (IPv4 + IPv6) frontend configurations, VMs with NICs that have a dual IP configuration, dual network security group rules, and dual public IPs.

## Prerequisites

# [Azure CLI](#tab/azurecli/)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

[!INCLUDE [azure-cli-prepare-your-environment-no-header.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment-no-header.md)]

# [Azure PowerShell](#tab/azurepowershell/)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

# [ARM template](#tab/arm-template/)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

---

## Deploy a dual stack (IPv4 + IPv6) application

# [Azure PowerShell](#tab/azurepowershell/)

Follow these instructions in Azure PowerShell to deploy a dual stack (IPv4 + IPv6) application using Standard Load Balancer in Azure.

## Create a resource group

Before you can create your dual-stack virtual network, you must create a resource group with [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup). The following example creates a resource group named *myRGDualStack* in the *east us* location:

```azurepowershell-interactive

$rg = New-AzResourceGroup `

-ResourceGroupName "dsRG1"  `

-Location "east us"

```

## Create IPv4 and IPv6 public IP addresses

To access your virtual machines from the Internet, you need IPv4 and IPv6 public IP addresses for the load balancer. Create public IP addresses with [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress). The following example creates IPv4 and IPv6 public IP address named *dsPublicIP_v4* and *dsPublicIP_v6* in the *dsRG1* resource group:

```azurepowershell-interactive

$PublicIP_v4 = New-AzPublicIpAddress `

-Name "dsPublicIP_v4" `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-AllocationMethod Static `

-IpAddressVersion IPv4 `

-Sku Standard

$PublicIP_v6 = New-AzPublicIpAddress `

-Name "dsPublicIP_v6" `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-AllocationMethod Static `

-IpAddressVersion IPv6 `

-Sku Standard

```

To access your virtual machines using a RDP connection, create an IPV4 public IP addresses for the virtual machines with [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress).

```azurepowershell-interactive

$RdpPublicIP_1 = New-AzPublicIpAddress `

-Name "RdpPublicIP_1" `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-AllocationMethod Static `

-Sku Standard `

-IpAddressVersion IPv4

$RdpPublicIP_2 = New-AzPublicIpAddress `

-Name "RdpPublicIP_2" `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-AllocationMethod Static `

-Sku Standard `

-IpAddressVersion IPv4

```

## Create Standard Load Balancer

In this section, you configure dual frontend IP (IPv4 and IPv6) and the backend address pool for the load balancer and then create a Standard Load Balancer.

### Create frontend IP

Create a frontend IP with [New-AzLoadBalancerFrontendIpConfig](/powershell/module/az.network/new-azloadbalancerfrontendipconfig). The following example creates IPv4 and IPv6 frontend IP configurations named *dsLbFrontEnd_v4* and *dsLbFrontEnd_v6*:

```azurepowershell-interactive

$frontendIPv4 = New-AzLoadBalancerFrontendIpConfig `

-Name "dsLbFrontEnd_v4" `

-PublicIpAddress $PublicIP_v4

$frontendIPv6 = New-AzLoadBalancerFrontendIpConfig `

-Name "dsLbFrontEnd_v6" `

-PublicIpAddress $PublicIP_v6

```

### Configure backend address pool

Create a backend address pool with [New-AzLoadBalancerBackendAddressPoolConfig](/powershell/module/az.network/new-azloadbalancerbackendaddresspoolconfig) for the virtual machines deployed later. The following example creates backend address pools named *dsLbBackEndPool_v4* and *dsLbBackEndPool_v6* to include virtual machines with both IPV4 and IPv6 NIC configurations:

```azurepowershell-interactive

$backendPoolv4 = New-AzLoadBalancerBackendAddressPoolConfig `

-Name "dsLbBackEndPool_v4"

$backendPoolv6 = New-AzLoadBalancerBackendAddressPoolConfig `

-Name "dsLbBackEndPool_v6"

```

### Create a health probe

Use [Add-AzLoadBalancerProbeConfig](/powershell/module/az.network/add-azloadbalancerprobeconfig) to create a health probe to monitor the health of the VMs.

```azurepowershell

$probe = New-AzLoadBalancerProbeConfig -Name MyProbe -Protocol tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2

```

### Create a load balancer rule

A load balancer rule is used to define how traffic is distributed to the VMs. You define the frontend IP configuration for the incoming traffic and the backend IP pool to receive the traffic, along with the required source and destination port. To make sure only healthy VMs receive traffic, you can optionally define a health probe. Basic load balancer uses an IPv4 probe to assess health for both IPv4 and IPv6 endpoints on the VMs. Standard load balancer includes support for explicitly IPv6 health probes.

Create a load balancer rule with [Add-AzLoadBalancerRuleConfig](/powershell/module/az.network/add-azloadbalancerruleconfig). The following example creates load balancer rules named *dsLBrule_v4* and *dsLBrule_v6* and balances traffic on *TCP* port *80* to the IPv4 and IPv6 frontend IP configurations:

```azurepowershell-interactive

$lbrule_v4 = New-AzLoadBalancerRuleConfig `

-Name "dsLBrule_v4" `

-FrontendIpConfiguration $frontendIPv4 `

-BackendAddressPool $backendPoolv4 `

-Protocol Tcp `

-FrontendPort 80 `

-BackendPort 80 `

-probe $probe

$lbrule_v6 = New-AzLoadBalancerRuleConfig `

-Name "dsLBrule_v6" `

-FrontendIpConfiguration $frontendIPv6 `

-BackendAddressPool $backendPoolv6 `

-Protocol Tcp `

-FrontendPort 80 `

-BackendPort 80 `

-probe $probe

```

### Create load balancer

Create a Standard Load Balancer with [New-AzLoadBalancer](/powershell/module/az.network/new-azloadbalancer). The following example creates a public Standard Load Balancer named *myLoadBalancer* using the IPv4 and IPv6 frontend IP configurations, backend pools, and load-balancing rules that you created in the preceding steps:

```azurepowershell-interactive

$lb = New-AzLoadBalancer `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-Name "MyLoadBalancer" `

-Sku "Standard" `

-FrontendIpConfiguration $frontendIPv4,$frontendIPv6 `

-BackendAddressPool $backendPoolv4,$backendPoolv6 `

-LoadBalancingRule $lbrule_v4,$lbrule_v6 `

-Probe $probe

```

## Create network resources

Before you deploy some VMs and can test your balancer, you must create supporting network resources - availability set, network security group, virtual network, and virtual NICs.

### Create an availability set

To improve the high availability of your app, place your VMs in an availability set.

Create an availability set with [New-AzAvailabilitySet](/powershell/module/az.compute/new-azavailabilityset). The following example creates an availability set named *myAvailabilitySet*:

```azurepowershell-interactive

$avset = New-AzAvailabilitySet `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-Name "dsAVset" `

-PlatformFaultDomainCount 2 `

-PlatformUpdateDomainCount 2 `

-Sku aligned

```

### Create network security group

Create a network security group for the rules that govern inbound and outbound communication in your virtual network.

#### Create a network security group rule for port 3389

Create a network security group rule to allow RDP connections through port 3389 with [New-AzNetworkSecurityRuleConfig](/powershell/module/az.network/new-aznetworksecurityruleconfig).

```azurepowershell-interactive

$rule1 = New-AzNetworkSecurityRuleConfig `

-Name 'myNetworkSecurityGroupRuleRDP' `

-Description 'Allow RDP' `

-Access Allow `

-Protocol Tcp `

-Direction Inbound `

-Priority 100 `

-SourceAddressPrefix * `

-SourcePortRange * `

-DestinationAddressPrefix * `

-DestinationPortRange 3389

```

#### Create a network security group rule for port 80

Create a network security group rule to allow internet connections through port 80 with [New-AzNetworkSecurityRuleConfig](/powershell/module/az.network/new-aznetworksecurityruleconfig).

```azurepowershell-interactive

$rule2 = New-AzNetworkSecurityRuleConfig `

-Name 'myNetworkSecurityGroupRuleHTTP' `

-Description 'Allow HTTP' `

-Access Allow `

-Protocol Tcp `

-Direction Inbound `

-Priority 200 `

-SourceAddressPrefix * `

-SourcePortRange * `

-DestinationAddressPrefix * `

-DestinationPortRange 80

```

#### Create a network security group

Create a network security group with [New-AzNetworkSecurityGroup](/powershell/module/az.network/new-aznetworksecuritygroup).

```azurepowershell-interactive

$nsg = New-AzNetworkSecurityGroup `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-Name "dsNSG1"  `

-SecurityRules $rule1,$rule2

```

### Create a virtual network

Create a virtual network with [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork). The following example creates a virtual network named *dsVnet* with *mySubnet*:

```azurepowershell-interactive

# Create dual stack subnet

$subnet = New-AzVirtualNetworkSubnetConfig `

-Name "dsSubnet" `

-AddressPrefix "10.0.0.0/24","fd00:db8:deca:deed::/64"

# Create the virtual network

$vnet = New-AzVirtualNetwork `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-Name "dsVnet" `

-AddressPrefix "10.0.0.0/16","fd00:db8:deca::/48"  `

-Subnet $subnet

```

### Create NICs

Create virtual NICs with [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface). The following example creates two virtual NICs both with IPv4 and IPv6 configurations. (One virtual NIC for each VM you create for your app in the following steps).

```azurepowershell-interactive

$Ip4Config=New-AzNetworkInterfaceIpConfig `

-Name dsIp4Config `

-Subnet $vnet.subnets[0] `

-PrivateIpAddressVersion IPv4 `

-LoadBalancerBackendAddressPool $backendPoolv4 `

-PublicIpAddress  $RdpPublicIP_1

$Ip6Config=New-AzNetworkInterfaceIpConfig `

-Name dsIp6Config `

-Subnet $vnet.subnets[0] `

-PrivateIpAddressVersion IPv6 `

-LoadBalancerBackendAddressPool $backendPoolv6

$NIC_1 = New-AzNetworkInterface `

-Name "dsNIC1" `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-NetworkSecurityGroupId $nsg.Id `

-IpConfiguration $Ip4Config,$Ip6Config

$Ip4Config=New-AzNetworkInterfaceIpConfig `

-Name dsIp4Config `

-Subnet $vnet.subnets[0] `

-PrivateIpAddressVersion IPv4 `

-LoadBalancerBackendAddressPool $backendPoolv4 `

-PublicIpAddress  $RdpPublicIP_2

$NIC_2 = New-AzNetworkInterface `

-Name "dsNIC2" `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-NetworkSecurityGroupId $nsg.Id `

-IpConfiguration $Ip4Config,$Ip6Config

```

### Create virtual machines

Set an administrator username and password for the VMs with [Get-Credential](/powershell/module/microsoft.powershell.security/get-credential):

```azurepowershell-interactive

$cred = get-credential -Message "DUAL STACK VNET SAMPLE:  Please enter the Administrator credential to log into the VMs."

```

Now you can create the VMs with [New-AzVM](/powershell/module/az.compute/new-azvm). The following example creates two VMs and the required virtual network components if they don't already exist.

```azurepowershell-interactive

$vmsize = "Standard_A2"

$ImagePublisher = "MicrosoftWindowsServer"

$imageOffer = "WindowsServer"

$imageSKU = "2019-Datacenter"

$vmName= "dsVM1"

$VMconfig1 = New-AzVMConfig -VMName $vmName -VMSize $vmsize -AvailabilitySetId $avset.Id 3> $null | Set-AzVMOperatingSystem -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent 3> $null | Set-AzVMSourceImage -PublisherName $ImagePublisher -Offer $imageOffer -Skus $imageSKU -Version "latest" 3> $null | Set-AzVMOSDisk -Name "$vmName.vhd" -CreateOption fromImage  3> $null | Add-AzVMNetworkInterface -Id $NIC_1.Id  3> $null

$VM1 = New-AzVM -ResourceGroupName $rg.ResourceGroupName  -Location $rg.Location  -VM $VMconfig1

$vmName= "dsVM2"

$VMconfig2 = New-AzVMConfig -VMName $vmName -VMSize $vmsize -AvailabilitySetId $avset.Id 3> $null | Set-AzVMOperatingSystem -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent 3> $null | Set-AzVMSourceImage -PublisherName $ImagePublisher -Offer $imageOffer -Skus $imageSKU -Version "latest" 3> $null | Set-AzVMOSDisk -Name "$vmName.vhd" -CreateOption fromImage  3> $null | Add-AzVMNetworkInterface -Id $NIC_2.Id  3> $null

$VM2 = New-AzVM -ResourceGroupName $rg.ResourceGroupName  -Location $rg.Location  -VM $VMconfig2

```

## Determine IP addresses of the IPv4 and IPv6 endpoints

Get all Network Interface Objects in the resource group to summarize the IPs used in this deployment with `get-AzNetworkInterface`. Also, get the Load Balancer's frontend addresses of the IPv4 and IPv6 endpoints with `get-AzpublicIpAddress`.

```azurepowershell-interactive

$rgName= "dsRG1"

$NICsInRG= get-AzNetworkInterface -resourceGroupName $rgName

write-host `nSummary of IPs in this Deployment:

write-host ******************************************

foreach ($NIC in $NICsInRG) {

$VMid= $NIC.virtualmachine.id

$VMnamebits= $VMid.split("/")

$VMname= $VMnamebits[($VMnamebits.count-1)]

write-host `nPrivate IP addresses for $VMname

$IPconfigsInNIC= $NIC.IPconfigurations

foreach ($IPconfig in $IPconfigsInNIC) {

$IPaddress= $IPconfig.privateipaddress

write-host "    "$IPaddress

IF ($IPconfig.PublicIpAddress.ID) {

$IDbits= ($IPconfig.PublicIpAddress.ID).split("/")

$PipName= $IDbits[($IDbits.count-1)]

$PipObject= get-azPublicIpAddress -name $PipName -resourceGroup $rgName

write-host "    "RDP address:  $PipObject.IpAddress

}

}

}

write-host `nPublic IP addresses on Load Balancer:

(get-AzpublicIpAddress -resourcegroupname $rgName | where { $_.name -notlike "RdpPublicIP*" }).IpAddress

```

The following figure shows a sample output that lists the private IPv4 and IPv6 addresses of the two VMs, and the frontend IPv4 and IPv6 IP addresses of the Load Balancer.

![IP summary of dual stack (IPv4/IPv6) application deployment in Azure](./media/virtual-network-ipv4-ipv6-dual-stack-powershell/dual-stack-application-summary.png)

## View IPv6 dual stack virtual network in Azure portal

You can view the IPv6 dual stack virtual network in Azure portal as follows:

1. In the portal's search bar, enter *dsVnet*.

2. When **dsVnet** appears in the search results, select it. This launches the **Overview** page of the dual stack virtual network named *dsVnet*. The dual stack virtual network shows the two NICs with both IPv4 and IPv6 configurations located in the dual stack subnet named *dsSubnet*.

## Clean up resources

When no longer needed, you can use the [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) command to remove the resource group, VM, and all related resources.

```azurepowershell-interactive

Remove-AzResourceGroup -Name dsRG1

```

# [Azure CLI](#tab/azurecli/)

Follow these instructions in Azure CLI to deploy a dual stack (IPv4 + IPv6) application using Standard Load Balancer in Azure.

## Create a resource group

Before you can create your dual-stack virtual network, you must create a resource group with [az group create](/cli/azure/group). The following example creates a resource group named *DsResourceGroup01* in the *eastus* location:

```azurecli-interactive

az group create \

--name DsResourceGroup01 \

--location eastus

```

## Create IPv4 and IPv6 public IP addresses for load balancer

To access your IPv4 and IPv6 endpoints on the Internet, you need IPv4 and IPv6 public IP addresses for the load balancer. Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip). The following example creates IPv4 and IPv6 public IP address named *dsPublicIP_v4* and *dsPublicIP_v6* in the *DsResourceGroup01* resource group:

```azurecli-interactive

# Create an IPV4 IP address

az network public-ip create \

--name dsPublicIP_v4  \

--resource-group DsResourceGroup01  \

--location eastus  \

--sku STANDARD  \

--allocation-method static  \

--version IPv4

# Create an IPV6 IP address

az network public-ip create \

--name dsPublicIP_v6  \

--resource-group DsResourceGroup01  \

--location eastus \

--sku STANDARD  \

--allocation-method static  \

--version IPv6

```

## Create public IP addresses for VMs

To remotely access your VMs on the internet, you need IPv4 public IP addresses for the VMs. Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip).

```azurecli-interactive

az network public-ip create \

--name dsVM0_remote_access  \

--resource-group DsResourceGroup01 \

--location eastus  \

--sku Standard  \

--allocation-method static  \

--version IPv4

az network public-ip create \

--name dsVM1_remote_access  \

--resource-group DsResourceGroup01  \

--location eastus  \

--sku Standard  \

--allocation-method static  \

--version IPv4

```

## Create Standard Load Balancer

In this section, you configure dual frontend IP (IPv4 and IPv6) and the backend address pool for the load balancer and then create a Standard Load Balancer.

### Create load balancer

Create the Standard Load Balancer with [az network lb create](/cli/azure/network/lb) named **dsLB** that includes a frontend pool named **dsLbFrontEnd_v4**, a backend pool named **dsLbBackEndPool_v4** that is associated with the IPv4 public IP address **dsPublicIP_v4** that you created in the preceding step.

```azurecli-interactive

az network lb create \

--name dsLB  \

--resource-group DsResourceGroup01 \

--sku Standard \

--location eastus \

--frontend-ip-name dsLbFrontEnd_v4  \

--public-ip-address dsPublicIP_v4  \

--backend-pool-name dsLbBackEndPool_v4

```

### Create IPv6 frontend

Create an IPV6 frontend IP with [az network lb frontend-ip create](/cli/azure/network/lb/frontend-ip#az-network-lb-frontend-ip-create). The following example creates a frontend IP configuration named *dsLbFrontEnd_v6* and attaches the *dsPublicIP_v6* address:

```azurecli-interactive

az network lb frontend-ip create \

--lb-name dsLB  \

--name dsLbFrontEnd_v6  \

--resource-group DsResourceGroup01  \

--public-ip-address dsPublicIP_v6

```

### Configure IPv6 backend address pool

Create a IPv6 backend address pools with [az network lb address-pool create](/cli/azure/network/lb/address-pool#az-network-lb-address-pool-create). The following example creates backend address pool named *dsLbBackEndPool_v6*  to include VMs with IPv6 NIC configurations:

```azurecli-interactive

az network lb address-pool create \

--lb-name dsLB  \

--name dsLbBackEndPool_v6  \

--resource-group DsResourceGroup01

```

### Create a health probe

Create a health probe with [az network lb probe create](/cli/azure/network/lb/probe) to monitor the health of the virtual machines.

```azurecli-interactive

az network lb probe create -g DsResourceGroup01  --lb-name dsLB -n dsProbe --protocol tcp --port 3389

```

### Create a load balancer rule

A load balancer rule is used to define how traffic is distributed to the VMs. You define the frontend IP configuration for the incoming traffic and the backend IP pool to receive the traffic, along with the required source and destination port.

Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#az-network-lb-rule-create). The following example creates load balancer rules named *dsLBrule_v4* and *dsLBrule_v6* and balances traffic on *TCP* port *80* to the IPv4 and IPv6 frontend IP configurations:

```azurecli-interactive

az network lb rule create \

--lb-name dsLB  \

--name dsLBrule_v4  \

--resource-group DsResourceGroup01  \

--frontend-ip-name dsLbFrontEnd_v4  \

--protocol Tcp  \

--frontend-port 80  \

--backend-port 80  \

--probe-name dsProbe \

--backend-pool-name dsLbBackEndPool_v4

az network lb rule create \

--lb-name dsLB  \

--name dsLBrule_v6  \

--resource-group DsResourceGroup01 \

--frontend-ip-name dsLbFrontEnd_v6  \

--protocol Tcp  \

--frontend-port 80 \

--backend-port 80  \

--probe-name dsProbe \

--backend-pool-name dsLbBackEndPool_v6

```

## Create network resources

Before you deploy some VMs, you must create supporting network resources - availability set, network security group, virtual network, and virtual NICs.

### Create an availability set

To improve the availability of your app, place your VMs in an availability set.

Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set). The following example creates an availability set named *dsAVset*:

```azurecli-interactive

az vm availability-set create \

--name dsAVset  \

--resource-group DsResourceGroup01  \

--location eastus \

--platform-fault-domain-count 2  \

--platform-update-domain-count 2

```

### Create network security group

Create a network security group for the rules that govern inbound and outbound communication in your virtual network.

#### Create a network security group

Create a network security group with [az network nsg create](/cli/azure/network/nsg#az-network-nsg-create)

```azurecli-interactive

az network nsg create \

--name dsNSG1  \

--resource-group DsResourceGroup01  \

--location eastus

```

#### Create a network security group rule for inbound and outbound connections

Create a network security group rule to allow RDP connections through port 3389, internet connection through port 80, and for outbound connections with [az network nsg rule create](/cli/azure/network/nsg/rule#az-network-nsg-rule-create).

```azurecli-interactive

# Create inbound rule for port 3389

az network nsg rule create \

--name allowRdpIn  \

--nsg-name dsNSG1  \

--resource-group DsResourceGroup01  \

--priority 100  \

--description "Allow Remote Desktop In"  \

--access Allow  \

--protocol "*"  \

--direction Inbound  \

--source-address-prefixes "*"  \

--source-port-ranges "*"  \

--destination-address-prefixes "*"  \

--destination-port-ranges 3389

# Create inbound rule for port 80

az network nsg rule create \

--name allowHTTPIn  \

--nsg-name dsNSG1  \

--resource-group DsResourceGroup01  \

--priority 200  \

--description "Allow HTTP In"  \

--access Allow  \

--protocol "*"  \

--direction Inbound  \

--source-address-prefixes "*"  \

--source-port-ranges 80  \

--destination-address-prefixes "*"  \

--destination-port-ranges 80

# Create outbound rule

az network nsg rule create \

--name allowAllOut  \

--nsg-name dsNSG1  \

--resource-group DsResourceGroup01  \

--priority 300  \

--description "Allow All Out"  \

--access Allow  \

--protocol "*"  \

--direction Outbound  \

--source-address-prefixes "*"  \

--source-port-ranges "*"  \

--destination-address-prefixes "*"  \

--destination-port-ranges "*"

```

### Create a virtual network

Create a virtual network with [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create). The following example creates a virtual network named *dsVNET* with subnets *dsSubNET_v4* and *dsSubNET_v6*:

```azurecli-interactive

# Create the virtual network

az network vnet create \

--name dsVNET \

--resource-group DsResourceGroup01 \

--location eastus  \

--address-prefixes "10.0.0.0/16" "fd00:db8:deca::/48"

# Create a single dual stack subnet

az network vnet subnet create \

--name dsSubNET \

--resource-group DsResourceGroup01 \

--vnet-name dsVNET \

--address-prefixes "10.0.0.0/24" "fd00:db8:deca:deed::/64" \

--network-security-group dsNSG1

```

### Create NICs

Create virtual NICs for each VM with [az network nic create](/cli/azure/network/nic#az-network-nic-create). The following example creates a virtual NIC for each VM. Each NIC has two IP configurations (1 IPv4 config, 1 IPv6 config). You create the IPV6 configuration with [az network nic ip-config create](/cli/azure/network/nic/ip-config#az-network-nic-ip-config-create).

```azurecli-interactive

# Create NICs

az network nic create \

--name dsNIC0  \

--resource-group DsResourceGroup01 \

--network-security-group dsNSG1  \

--vnet-name dsVNET  \

--subnet dsSubNet  \

--private-ip-address-version IPv4 \

--lb-address-pools dsLbBackEndPool_v4  \

--lb-name dsLB  \

--public-ip-address dsVM0_remote_access

az network nic create \

--name dsNIC1 \

--resource-group DsResourceGroup01 \

--network-security-group dsNSG1 \

--vnet-name dsVNET \

--subnet dsSubNet \

--private-ip-address-version IPv4 \

--lb-address-pools dsLbBackEndPool_v4 \

--lb-name dsLB \

--public-ip-address dsVM1_remote_access

# Create IPV6 configurations for each NIC

az network nic ip-config create \

--name dsIp6Config_NIC0  \

--nic-name dsNIC0  \

--resource-group DsResourceGroup01 \

--vnet-name dsVNET \

--subnet dsSubNet \

--private-ip-address-version IPv6 \

--lb-address-pools dsLbBackEndPool_v6 \

--lb-name dsLB

az network nic ip-config create \

--name dsIp6Config_NIC1 \

--nic-name dsNIC1 \

--resource-group DsResourceGroup01 \

--vnet-name dsVNET \

--subnet dsSubNet \

--private-ip-address-version IPv6 \

--lb-address-pools dsLbBackEndPool_v6 \

--lb-name dsLB

```

### Create virtual machines

Create the VMs with [az vm create](/cli/azure/vm#az-vm-create). The following example creates two VMs and the required virtual network components if they don't already exist.

Create virtual machine *dsVM0* as follows:

```azurecli-interactive

az vm create \

--name dsVM0 \

--resource-group DsResourceGroup01 \

--nics dsNIC0 \

--size Standard_A2 \

--availability-set dsAVset \

--image MicrosoftWindowsServer:WindowsServer:2019-Datacenter:latest

```

Create virtual machine *dsVM1* as follows:

```azurecli-interactive

az vm create \

--name dsVM1 \

--resource-group DsResourceGroup01 \

--nics dsNIC1 \

--size Standard_A2 \

--availability-set dsAVset \

--image MicrosoftWindowsServer:WindowsServer:2019-Datacenter:latest

```

## View IPv6 dual stack virtual network in Azure portal

You can view the IPv6 dual stack virtual network in Azure portal as follows:

1. In the portal's search bar, enter *dsVnet*.

2. When **myVirtualNetwork** appears in the search results, select it. This launches the **Overview** page of the dual stack virtual network named *dsVnet*. The dual stack virtual network shows the two NICs with both IPv4 and IPv6 configurations located in the dual stack subnet named *dsSubnet*.

## Clean up resources

When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, VM, and all related resources.

```azurecli-interactive

az group delete --name DsResourceGroup01

```

# [ARM template](#tab/arm-template/)

Use the template described in this article to deploy a dual stack (IPv4 + IPv6) application using Standard Load Balancer in Azure.

## Required configurations

Search for the template sections in the template to see where they should occur.

### IPv6 addressSpace for the virtual network

Template section to add:

```JSON

"addressSpace": {

"addressPrefixes": [

"[variables('vnetv4AddressRange')]",

"[variables('vnetv6AddressRange')]"

```

### IPv6 subnet within the IPv6 virtual network addressSpace

Template section to add:

```JSON

{

"name": "V6Subnet",

"properties": {

"addressPrefix": "[variables('subnetv6AddressRange')]"

}

```

### IPv6 configuration for the NIC

Template section to add:

```JSON

{

"name": "ipconfig-v6",

"properties": {

"privateIPAllocationMethod": "Dynamic",

"privateIPAddressVersion":"IPv6",

"subnet": {

"id": "[variables('v6-subnet-id')]"

},

"loadBalancerBackendAddressPools": [

{

"id": "[concat(resourceId('Microsoft.Network/loadBalancers','loadBalancer'),'/backendAddressPools/LBBAP-v6')]"

}

```

### IPv6 network security group (NSG) rules

```JSON

{

"name": "default-allow-rdp",

"properties": {

"description": "Allow RDP",

"protocol": "Tcp",

"sourcePortRange": "33819-33829",

"destinationPortRange": "5000-6000",

"sourceAddressPrefix": "fd00:db8:deca:deed::/64",

"destinationAddressPrefix": "fd00:db8:deca:deed::/64",

"access": "Allow",

"priority": 1003,

"direction": "Inbound"

}

```

## Conditional configuration

If you're using a network virtual appliance, add IPv6 routes in the Route Table. Otherwise, this configuration is optional.

```JSON

{

"type": "Microsoft.Network/routeTables",

"name": "v6route",

"apiVersion": "[variables('ApiVersion')]",

"location": "[resourceGroup().location]",

"properties": {

"routes": [

{

"name": "v6route",

"properties": {

"addressPrefix": "fd00:db8:deca:deed::/64",

"nextHopType": "VirtualAppliance",

"nextHopIpAddress": "fd00:db8:ace:f00d::1"

}

```

## Optional configuration

### IPv6 Internet access for the virtual network

```JSON

{

"name": "LBFE-v6",

"properties": {

"publicIPAddress": {

"id": "[resourceId('Microsoft.Network/publicIPAddresses','lbpublicip-v6')]"

}

```

### IPv6 Public IP addresses

```JSON

{

"apiVersion": "[variables('ApiVersion')]",

"type": "Microsoft.Network/publicIPAddresses",

"name": "lbpublicip-v6",

"location": "[resourceGroup().location]",

"sku": {

"name": "Standard"

},

"properties": {

"publicIPAllocationMethod": "Static",

"publicIPAddressVersion": "IPv6"

}

```

### IPv6 Front end for Load Balancer

```JSON

{

"name": "LBFE-v6",

"properties": {

"publicIPAddress": {

"id": "[resourceId('Microsoft.Network/publicIPAddresses','lbpublicip-v6')]"

}

```

### IPv6 Backend address pool for Load Balancer

```JSON

"backendAddressPool": {

"id": "[concat(resourceId('Microsoft.Network/loadBalancers', 'loadBalancer'), '/backendAddressPools/LBBAP-v6')]"

},

"protocol": "Tcp",

"frontendPort": 8080,

"backendPort": 8080

},

"name": "lbrule-v6"

```

### IPv6 load balancer rules to associate incoming and outgoing ports

```JSON

{

"name": "ipconfig-v6",

"properties": {

"privateIPAllocationMethod": "Dynamic",

"privateIPAddressVersion":"IPv6",

"subnet": {

"id": "[variables('v6-subnet-id')]"

},

"loadBalancerBackendAddressPools": [

{

"id": "[concat(resourceId('Microsoft.Network/loadBalancers','loadBalancer'),'/backendAddressPools/LBBAP-v6')]"

}

```

## Sample VM template JSON

To deploy an IPv6 dual stack application in Azure virtual network using Azure Resource Manager template, view sample template [here](https://azure.microsoft.com/resources/templates/ipv6-in-vnet-stdlb/).

---

## Next steps

> [!div class="nextstepaction"]

> [What is IPv6 for Azure Virtual Network?](../virtual-network/ip-services/ipv6-overview.md)


# Ipv6 Dual Stack Standard Internal Load Balancer Powershell

# Deploy an IPv6 dual stack application using Standard Internal Load Balancer in Azure using PowerShell

This article shows you how to deploy a dual stack (IPv4 + IPv6) application in Azure that includes a dual stack virtual network and subnet, a Standard Internal Load Balancer with dual (IPv4 + IPv6) frontend configurations, VMs with NICs that have a dual IP configuration, network security group, and public IPs.

The procedure to create an IPv6-capable Internal Load Balancer is nearly identical to the process for creating an Internet-facing IPv6 Load Balancer described [here](virtual-network-ipv4-ipv6-dual-stack-standard-load-balancer-powershell.md). The only differences for creating an internal load balancer are in the frontend configuration as illustrated in the PowerShell example below:

```azurepowershell

$frontendIPv6 = New-AzLoadBalancerFrontendIpConfig `

-Name "dsLbFrontEnd_v6" `

-PrivateIpAddress "fd00:db8:deca:deed::100" `

-PrivateIpAddressVersion "IPv6" `

-Subnet $DsSubnet

```

The changes that make the above an internal load balancer frontend configuration are:

- The `PrivateIpAddressVersion` is specified as “IPv6”

- The `-PublicIpAddress` argument has been either omitted or replaced with `-PrivateIpAddress`. Note that the private address must be in the range of the Subnet IP space in which the internal load balancer will be deployed. If a static `-PrivateIpAddress` is omitted, the next free IPv6 address will be selected from the subnet in which the internal load Balancer is deployed.

- The dual stack subnet in which the internal load balancer will be deployed is specified with either a `-Subnet` or `-SubnetId` argument.

[!INCLUDE [cloud-shell-try-it.md](~/reusable-content/ce-skilling/azure/includes/cloud-shell-try-it.md)]

If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 6.9.0 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell). If you are running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

## Create a resource group

Before you can create your dual-stack virtual network, you must create a resource group with [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup). The following example creates a resource group named *dsStd_ILB_RG* in the *east us* location:

```azurepowershell

$rg = New-AzResourceGroup `

-ResourceGroupName "dsStd_ILB_RG"  `

-Location "east us"

```

## Create IPv4 and IPv6 public IP addresses

To access your virtual machines from the Internet, you need IPv4 and IPv6 public IP addresses for the VMs. Create public IP addresses with [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress). The following example creates IPv4 and IPv6 public IP address named *RdpPublicIP_1* and *RdpPublicIP_2* in the *dsStd_ILB_RG* resource group:

```azurepowershell

$RdpPublicIP_1 = New-AzPublicIpAddress `

-Name "RdpPublicIP_1" `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-AllocationMethod Static `

-IpAddressVersion IPv4  `

-sku Standard

$RdpPublicIP_2 = New-AzPublicIpAddress `

-Name "RdpPublicIP_2" `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-AllocationMethod Static `

-IpAddressVersion IPv6  `

-sku Standard

```

## Create the virtual network and the subnet

Create a virtual network using [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork) with dual stack a subnet configuration using [New-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/new-azvirtualnetworksubnetconfig). The following example creates a virtual network named *dsVnet* with *dsSubnet*.

```azurepowershell

# Create dual stack subnet config

$DsSubnet = New-AzVirtualNetworkSubnetConfig `

-Name "dsSubnet" `

-AddressPrefix "10.0.0.0/24","fd00:db8:deca:deed::/64"

# Create the virtual network

$vnet = New-AzVirtualNetwork `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-Name "dsVnet" `

-AddressPrefix "10.0.0.0/16","fd00:db8:deca::/48"  `

-Subnet $DsSubnet

#Refresh the fully populated subnet for use in load balancer frontend configuration

$DsSubnet = get-AzVirtualNetworkSubnetconfig -name dsSubnet -VirtualNetwork $vnet

```

## Create Standard Load Balancer

In this section, you configure dual frontend IP (IPv4 and IPv6) and the backend address pool for the load balancer and then create a Standard Load Balancer.

### Create frontend IP

Create a frontend IP with [New-AzLoadBalancerFrontendIpConfig](/powershell/module/az.network/new-azloadbalancerfrontendipconfig). The following example creates IPv4 and IPv6 frontend IP configurations named *dsLbFrontEnd_v4* and *dsLbFrontEnd_v6*:

```azurepowershell

$frontendIPv4 = New-AzLoadBalancerFrontendIpConfig `

-Name "dsLbFrontEnd_v4" `

-PrivateIpAddress "10.0.0.100"  `

-PrivateIpAddressVersion "IPv4"   `

-Subnet $DsSubnet

$frontendIPv6 = New-AzLoadBalancerFrontendIpConfig `

-Name "dsLbFrontEnd_v6" `

-PrivateIpAddress "fd00:db8:deca:deed::100"  `

-PrivateIpAddressVersion "IPv6"   `

-Subnet $DsSubnet

```

### Configure backend address pool

Create a backend address pool with [New-AzLoadBalancerBackendAddressPoolConfig](/powershell/module/az.network/new-azloadbalancerbackendaddresspoolconfig). The VMs attach to this backend pool in the remaining steps. The following example creates backend address pools named *dsLbBackEndPool_v4* and *dsLbBackEndPool_v6* to include VMs with both IPV4 and IPv6 NIC configurations:

```azurepowershell

$backendPoolv4 = New-AzLoadBalancerBackendAddressPoolConfig -Name "dsLbBackEndPool_v4"

$backendPoolv6 = New-AzLoadBalancerBackendAddressPoolConfig -Name "dsLbBackEndPool_v6"

```

### Create a load balancer rule

A load balancer rule is used to define how traffic is distributed to the VMs. You define the frontend IP configuration for the incoming traffic and the backend IP pool to receive the traffic, along with the required source and destination port. To make sure only healthy VMs receive traffic, you can optionally define a health probe. Basic load balancer uses an IPv4 probe to assess health for both IPv4 and IPv6 endpoints on the VMs. Standard load balancer includes support for explicitly IPv6 health probes.

Create a load balancer rule with [Add-AzLoadBalancerRuleConfig](/powershell/module/az.network/add-azloadbalancerruleconfig). The following example creates load balancer rules named *dsLBrule_v4* and *dsLBrule_v6* and balances traffic on *TCP* port *80* to the IPv4 and IPv6 frontend IP configurations:

```azurepowershell

$lbrule_v4 = New-AzLoadBalancerRuleConfig `

-Name "dsLBrule_v4" `

-FrontendIpConfiguration $frontendIPv4 `

-BackendAddressPool $backendPoolv4 `

-Protocol Tcp `

-FrontendPort 80 `

-BackendPort 80

$lbrule_v6 = New-AzLoadBalancerRuleConfig `

-Name "dsLBrule_v6" `

-FrontendIpConfiguration $frontendIPv6 `

-BackendAddressPool $backendPoolv6 `

-Protocol Tcp `

-FrontendPort 80 `

-BackendPort 80

```

### Create load balancer

Create a Standard Load Balancer with [New-AzLoadBalancer](/powershell/module/az.network/new-azloadbalancer). The following example creates a public Standard Load Balancer named *myInternalLoadBalancer* using the IPv4 and IPv6 frontend IP configurations, backend pools, and load-balancing rules that you created in the preceding steps:

```azurepowershell

$lb = New-AzLoadBalancer  `

-ResourceGroupName $rg.ResourceGroupName  `

-Location $rg.Location  `

-Name  "MyInternalLoadBalancer"  `

-Sku "Standard"  `

-FrontendIpConfiguration  $frontendIPv4,$frontendIPv6  `

-BackendAddressPool  $backendPoolv4,$backendPoolv6  `

-LoadBalancingRule  $lbrule_v4,$lbrule_v6

```

## Create network resources

Before you deploy some VMs and can test your balancer, you must create supporting network resources - availability set, network security group, and virtual NICs.

### Create an availability set

To improve the high availability of your application, place your VMs in an availability set.

Create an availability set with [New-AzAvailabilitySet](/powershell/module/az.compute/new-azavailabilityset). The following example creates an availability set named *dsAVset*:

```azurepowershell

$avset = New-AzAvailabilitySet `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-Name "dsAVset" `

-PlatformFaultDomainCount 2 `

-PlatformUpdateDomainCount 2 `

-Sku aligned

```

### Create network security group

Create a network security group for the rules that will govern inbound and outbound communication in your VNet.

#### Create a network security group rule for port 3389

Create a network security group rule to allow RDP connections through port 3389 with [New-AzNetworkSecurityRuleConfig](/powershell/module/az.network/new-aznetworksecurityruleconfig).

```azurepowershell

$rule1 = New-AzNetworkSecurityRuleConfig `

-Name 'myNetworkSecurityGroupRuleRDP' `

-Description 'Allow RDP' `

-Access Allow `

-Protocol Tcp `

-Direction Inbound `

-Priority 100 `

-SourceAddressPrefix * `

-SourcePortRange * `

-DestinationAddressPrefix * `

-DestinationPortRange 3389

```

#### Create a network security group rule for port 80

Create a network security group rule to allow internet connections through port 80 with [New-AzNetworkSecurityRuleConfig](/powershell/module/az.network/new-aznetworksecurityruleconfig).

```azurepowershell

$rule2 = New-AzNetworkSecurityRuleConfig `

-Name 'myNetworkSecurityGroupRuleHTTP' `

-Description 'Allow HTTP' `

-Access Allow `

-Protocol Tcp `

-Direction Inbound `

-Priority 200 `

-SourceAddressPrefix * `

-SourcePortRange 80 `

-DestinationAddressPrefix * `

-DestinationPortRange 80

```

#### Create a network security group

Create a network security group with [New-AzNetworkSecurityGroup](/powershell/module/az.network/new-aznetworksecuritygroup).

```azurepowershell

$nsg = New-AzNetworkSecurityGroup `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-Name "dsNSG1"  `

-SecurityRules $rule1,$rule2

```

### Create NICs

Create virtual NICs with [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface). The following example creates two virtual NICs both with IPv4 and IPv6 configurations. (One virtual NIC for each VM you create for your app in the following steps).

```azurepowershell

# Create the IPv4 configuration for NIC 1

$Ip4Config=New-AzNetworkInterfaceIpConfig `

-Name dsIp4Config `

-Subnet $vnet.subnets[0] `

-PrivateIpAddressVersion IPv4 `

-LoadBalancerBackendAddressPool $backendPoolv4 `

-PublicIpAddress  $RdpPublicIP_1

# Create the IPv6 configuration

$Ip6Config=New-AzNetworkInterfaceIpConfig `

-Name dsIp6Config `

-Subnet $vnet.subnets[0] `

-PrivateIpAddressVersion IPv6 `

-LoadBalancerBackendAddressPool $backendPoolv6

# Create NIC 1

$NIC_1 = New-AzNetworkInterface `

-Name "dsNIC1" `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-NetworkSecurityGroupId $nsg.Id `

-IpConfiguration $Ip4Config,$Ip6Config

# Create the IPv4 configuration for NIC 2

$Ip4Config=New-AzNetworkInterfaceIpConfig `

-Name dsIp4Config `

-Subnet $vnet.subnets[0] `

-PrivateIpAddressVersion IPv4 `

-LoadBalancerBackendAddressPool $backendPoolv4 `

-PublicIpAddress  $RdpPublicIP_2

# Create NIC 2 reusing the IPv6 configuration from NIC 1

$NIC_2 = New-AzNetworkInterface `

-Name "dsNIC2" `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-NetworkSecurityGroupId $nsg.Id `

-IpConfiguration $Ip4Config,$Ip6Config

```

### Create virtual machines

Set an administrator username and password for the VMs with [Get-Credential](/powershell/module/microsoft.powershell.security/get-credential):

```azurepowershell

$cred = get-credential -Message "DUAL STACK VNET SAMPLE:  Please enter the Administrator credential to log into the VM's"

```

Now you can create the VMs with [New-AzVM](/powershell/module/az.compute/new-azvm). The following example creates two VMs and the required virtual network components if they do not already exist.

```azurepowershell

$vmsize = "Standard_A2"

$ImagePublisher = "MicrosoftWindowsServer"

$imageOffer = "WindowsServer"

$imageSKU = "2019-Datacenter"

$vmName= "dsVM1"

$VMconfig1 = New-AzVMConfig -VMName $vmName -VMSize $vmsize -AvailabilitySetId $avset.Id 3> $null | Set-AzVMOperatingSystem -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent 3> $null | Set-AzVMSourceImage -PublisherName $ImagePublisher -Offer $imageOffer -Skus $imageSKU -Version "latest" 3> $null | Set-AzVMOSDisk -Name "$vmName.vhd" -CreateOption fromImage  3> $null | Add-AzVMNetworkInterface -Id $NIC_1.Id  3> $null

$VM1 = New-AzVM -ResourceGroupName $rg.ResourceGroupName  -Location $rg.Location  -VM $VMconfig1

$vmName= "dsVM2"

$VMconfig2 = New-AzVMConfig -VMName $vmName -VMSize $vmsize -AvailabilitySetId $avset.Id 3> $null | Set-AzVMOperatingSystem -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent 3> $null | Set-AzVMSourceImage -PublisherName $ImagePublisher -Offer $imageOffer -Skus $imageSKU -Version "latest" 3> $null | Set-AzVMOSDisk -Name "$vmName.vhd" -CreateOption fromImage  3> $null | Add-AzVMNetworkInterface -Id $NIC_2.Id  3> $null

$VM2 = New-AzVM -ResourceGroupName $rg.ResourceGroupName  -Location $rg.Location  -VM $VMconfig2

```

## View IPv6 dual stack virtual network in Azure portal

You can view the IPv6 dual stack virtual network in Azure portal as follows:

1. In the portal's search bar, enter *dsVnet*.

2. When **dsVnet** appears in the search results, select it. This launches the **Overview** page of the dual stack virtual network named *dsVnet*. The dual stack virtual network shows the two NICs with both IPv4 and IPv6 configurations located in the dual stack subnet named *dsSubnet*.

> [!NOTE]

> The IPv6 for Azure virtual network is available in the Azure portal in read-only for this preview release.

## Clean up resources

When no longer needed, you can use the [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) command to remove the resource group, VM, and all related resources.

```azurepowershell

Remove-AzResourceGroup -Name dsStd_ILB_RG

```

## Next steps

In this article, you created a Standard Load Balancer with a dual frontend IP configuration (IPv4 and IPv6). You also created a two virtual machines that included NICs with dual IP configurations (IPV4 + IPv6) that were added to the backend pool of the load balancer. To learn more about IPv6 support in Azure virtual networks, see [What is IPv6 for Azure Virtual Network?](../virtual-network/ip-services/ipv6-overview.md)


# Ipv6 Add To Existing Vnet Powershell

# Add an IPv4 application to IPv6 in Azure virtual network using PowerShell

This article shows you how to add IPv6 connectivity to an existing IPv4 application in an Azure virtual network with a Standard Load Balancer and Public IP. The in-place upgrade includes:

- IPv6 address space for the virtual network and subnet

- Standard Load Balancer with both IPv4 and IPV6 frontend configurations

- VMs with NICs that have both an IPv4 + IPv6 configuration

- IPv6 Public IP so the load balancer has Internet-facing IPv6 connectivity

[!INCLUDE [cloud-shell-try-it.md](~/reusable-content/ce-skilling/azure/includes/cloud-shell-try-it.md)]

If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 6.9.0 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell). If you're running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

## Prerequisites

This article assumes that you deployed a Standard Load Balancer as described in [Quickstart: Create a Standard Load Balancer - Azure PowerShell](../load-balancer/quickstart-load-balancer-standard-public-powershell.md).

## Retrieve the resource group

Before you can create your dual-stack virtual network, you must retrieve the resource group with [Get-AzResourceGroup](/powershell/module/az.resources/get-azresourcegroup).

```azurepowershell-interactive

$rg = Get-AzResourceGroup  -ResourceGroupName "myResourceGroupSLB"

```

## Create an IPv6 IP addresses

Create a public IPv6 address with [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) for your Standard Load Balancer. The following example creates an IPv6 public IP address named *PublicIP_v6* in the *myResourceGroupSLB* resource group:

```azurepowershell-interactive

$PublicIP_v6 = New-AzPublicIpAddress `

-Name "PublicIP_v6" `

-ResourceGroupName $rg.ResourceGroupName `

-Location $rg.Location  `

-Sku Standard  `

-AllocationMethod Static `

-IpAddressVersion IPv6

```

## Configure load balancer frontend

Retrieve the existing load balancer configuration and then add the new IPv6 IP address using [Add-AzLoadBalancerFrontendIpConfig](/powershell/module/az.network/Add-AzLoadBalancerFrontendIpConfig) as follows:

```azurepowershell-interactive

# Retrieve the load balancer configuration

$lb = Get-AzLoadBalancer -ResourceGroupName $rg.ResourceGroupName -Name "MyLoadBalancer"

# Add IPv6 components to the local copy of the load balancer configuration

$lb | Add-AzLoadBalancerFrontendIpConfig `

-Name "dsLbFrontEnd_v6" `

-PublicIpAddress $PublicIP_v6

#Update the running load balancer with the new frontend

$lb | Set-AzLoadBalancer

```

## Configure load balancer backend pool

Create the backend pool on the local copy of the load balancer configuration and update the running load balancer with the new backend pool configuration as follows:

```azurepowershell-interactive

$lb | Add-AzLoadBalancerBackendAddressPoolConfig -Name "LbBackEndPool_v6"

# Update the running load balancer with the new backend pool

$lb | Set-AzLoadBalancer

```

## Configure load balancer rules

Retrieve the existing load balancer frontend and backend pool configuration and then add new load-balancing rules using [Add-AzLoadBalancerRuleConfig](/powershell/module/az.network/Add-AzLoadBalancerRuleConfig).

```azurepowershell-interactive

# Retrieve the updated (live) versions of the frontend and backend pool

$frontendIPv6 = Get-AzLoadBalancerFrontendIpConfig -Name "dsLbFrontEnd_v6" -LoadBalancer $lb

$backendPoolv6 = Get-AzLoadBalancerBackendAddressPoolConfig -Name "LbBackEndPool_v6" -LoadBalancer $lb

# Create new LB rule with the frontend and backend

$lb | Add-AzLoadBalancerRuleConfig `

-Name "dsLBrule_v6" `

-FrontendIpConfiguration $frontendIPv6 `

-BackendAddressPool $backendPoolv6 `

-Protocol Tcp `

-FrontendPort 80 `

-BackendPort 80

#Finalize all the load balancer updates on the running load balancer

$lb | Set-AzLoadBalancer

```

## Add IPv6 address ranges

Add IPv6 address ranges to the virtual network and subnet hosting the VMs as follows:

```azurepowershell-interactive

#Add IPv6 ranges to the VNET and subnet

#Retrieve the VNET object

$vnet = Get-AzVirtualNetwork  -ResourceGroupName $rg.ResourceGroupName -Name "myVnet"

#Add IPv6 prefix to the VNET

$vnet.addressspace.addressprefixes.add("fd00:db8:deca::/48")

#Update the running VNET

$vnet |  Set-AzVirtualNetwork

#Retrieve the subnet object from the local copy of the VNET

$subnet= $vnet.subnets[0]

#Add IPv6 prefix to the Subnet (subnet of the VNET prefix, of course)

$subnet.addressprefix.add("fd00:db8:deca::/64")

#Update the running VNET with the new subnet configuration

$vnet |  Set-AzVirtualNetwork

```

## Add IPv6 configuration to NIC

Configure all of the VM NICs with an IPv6 address using [Add-AzNetworkInterfaceIpConfig](/powershell/module/az.network/Add-AzNetworkInterfaceIpConfig) as follows:

```azurepowershell-interactive

#Retrieve the NIC objects

$NIC_1 = Get-AzNetworkInterface -Name "myNic1" -ResourceGroupName $rg.ResourceGroupName

$NIC_2 = Get-AzNetworkInterface -Name "myNic2" -ResourceGroupName $rg.ResourceGroupName

$NIC_3 = Get-AzNetworkInterface -Name "myNic3" -ResourceGroupName $rg.ResourceGroupName

#Add an IPv6 IPconfig to NIC_1 and update the NIC on the running VM

$NIC_1 | Add-AzNetworkInterfaceIpConfig -Name MyIPv6Config -Subnet $vnet.Subnets[0]  -PrivateIpAddressVersion IPv6 -LoadBalancerBackendAddressPool $backendPoolv6

$NIC_1 | Set-AzNetworkInterface

#Add an IPv6 IPconfig to NIC_2 and update the NIC on the running VM

$NIC_2 | Add-AzNetworkInterfaceIpConfig -Name MyIPv6Config -Subnet $vnet.Subnets[0]  -PrivateIpAddressVersion IPv6 -LoadBalancerBackendAddressPool $backendPoolv6

$NIC_2 | Set-AzNetworkInterface

#Add an IPv6 IPconfig to NIC_3 and update the NIC on the running VM

$NIC_3 | Add-AzNetworkInterfaceIpConfig -Name MyIPv6Config -Subnet $vnet.Subnets[0]  -PrivateIpAddressVersion IPv6 -LoadBalancerBackendAddressPool $backendPoolv6

$NIC_3 | Set-AzNetworkInterface

```

## View IPv6 dual-stack virtual network in Azure portal

You can view the IPv6 dual-stack virtual network in Azure portal as follows:

1. In the portal's search bar, enter **virtual networks** and

1. In the **Virtual Networks** window, select **myVNet**.

1.  Select **Connected devices** under **Settings** to view the attached network interfaces. The dual stack virtual network shows the three NICs with both IPv4 and IPv6 configurations.

## Clean up resources

When no longer needed, you can use the [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) command to remove the resource group, VM, and all related resources.

```azurepowershell-interactive

Remove-AzResourceGroup -Name MyAzureResourceGroupSLB

```

## Next steps

In this article, you updated an existing Standard Load Balancer with a IPv4 frontend IP configuration to a dual stack (IPv4 and IPv6) configuration. You also added IPv6 configurations to the NICs of the VMs in the backend pool and to the Virtual Network that hosts them. To learn more about IPv6 support in Azure virtual networks, see [What is IPv6 for Azure Virtual Network?](../virtual-network/ip-services/ipv6-overview.md)


# Ipv6 Add To Existing Vnet Cli

# Add IPv6 to an IPv4 application in Azure virtual network using Azure CLI

This article shows you how to add IPv6 addresses to an application that is using IPv4 public IP address in an Azure virtual network for a Standard Load Balancer using Azure CLI. The in-place upgrade includes a virtual network and subnet, a Standard Load Balancer with IPv4 + IPV6 frontend configurations, VMs with NICs that have a IPv4 + IPv6 configurations, network security group, and public IPs.

## Prerequisites

- This article assumes that you deployed a Standard Load Balancer as described in [Quickstart: Create a Standard Load Balancer - Azure CLI](../load-balancer/quickstart-load-balancer-standard-public-cli.md).

[!INCLUDE [azure-cli-prepare-your-environment-no-header.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment-no-header.md)]

- This article requires version 2.0.28 or later of the Azure CLI. If using Azure Cloud Shell, the latest version is already installed.

## Create IPv6 addresses

Create public IPv6 address with [az network public-ip create](/cli/azure/network/public-ip) for your Standard Load Balancer. The following example creates an IPv6 public IP address named *PublicIP_v6* in the *myResourceGroupSLB* resource group:

```azurecli-interactive

az network public-ip create \

--name PublicIP_v6 \

--resource-group MyResourceGroupSLB \

--location EastUS \

--sku Standard \

--allocation-method static \

--version IPv6

```

## Configure IPv6 load balancer frontend

Configure the load balancer with the new IPv6 IP address using [az network lb frontend-ip create](/cli/azure/network/lb/frontend-ip#az-network-lb-frontend-ip-create) as follows:

```azurecli-interactive

az network lb frontend-ip create \

--lb-name myLoadBalancer \

--name dsLbFrontEnd_v6 \

--resource-group MyResourceGroupSLB \

--public-ip-address PublicIP_v6

```

## Configure IPv6 load balancer backend pool

Create the backend pool for NICs with IPv6 addresses using [az network lb address-pool create](/cli/azure/network/lb/address-pool#az-network-lb-address-pool-create) as follows:

```azurecli-interactive

az network lb address-pool create \

--lb-name myLoadBalancer \

--name dsLbBackEndPool_v6 \

--resource-group MyResourceGroupSLB

```

## Configure IPv6 load balancer rules

Create IPv6 load balancer rules with [az network lb rule create](/cli/azure/network/lb/rule#az-network-lb-rule-create).

```azurecli-interactive

az network lb rule create \

--lb-name myLoadBalancer \

--name dsLBrule_v6 \

--resource-group MyResourceGroupSLB \

--frontend-ip-name dsLbFrontEnd_v6 \

--protocol Tcp \

--frontend-port 80 \

--backend-port 80 \

--backend-pool-name dsLbBackEndPool_v6

```

## Add IPv6 address ranges

Add IPv6 address ranges to the virtual network and subnet hosting the load balancer as follows:

```azurecli-interactive

az network vnet update \

--name myVnet  \

--resource-group MyResourceGroupSLB \

--address-prefixes  "10.0.0.0/16"  "fd00:db8:deca::/48"

az network vnet subnet update \

--vnet-name myVnet \

--name mySubnet \

--resource-group MyResourceGroupSLB \

--address-prefixes  "10.0.0.0/24"  "fd00:db8:deca:deed::/64"

```

## Add IPv6 configuration to NICs

Configure the VM NICs with an IPv6 address using [az network nic ip-config create](/cli/azure/network/nic/ip-config#az-network-nic-ip-config-create) as follows:

```azurecli-interactive

az network nic ip-config create \

--name dsIp6Config_NIC1 \

--nic-name myNicVM1 \

--resource-group MyResourceGroupSLB \

--vnet-name myVnet \

--subnet mySubnet \

--private-ip-address-version IPv6 \

--lb-address-pools dsLbBackEndPool_v6 \

--lb-name dsLB

az network nic ip-config create \

--name dsIp6Config_NIC2 \

--nic-name myNicVM2 \

--resource-group MyResourceGroupSLB \

--vnet-name myVnet \

--subnet mySubnet \

--private-ip-address-version IPv6 \

--lb-address-pools dsLbBackEndPool_v6 \

--lb-name myLoadBalancer

az network nic ip-config create \

--name dsIp6Config_NIC3 \

--nic-name myNicVM3 \

--resource-group MyResourceGroupSLB \

--vnet-name myVnet \

--subnet mySubnet \

--private-ip-address-version IPv6 \

--lb-address-pools dsLbBackEndPool_v6 \

--lb-name myLoadBalancer

```

## View IPv6 dual-stack virtual network in Azure portal

You can view the IPv6 dual-stack virtual network in Azure portal as follows:

1. In the portal's search bar, enter **virtual networks** and

1. In the **Virtual Networks** window, select **myVNet**.

1.  Select **Connected devices** under **Settings** to view the attached network interfaces. The dual stack virtual network shows the three NICs with both IPv4 and IPv6 configurations.

## Clean up resources

When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, VM, and all related resources.

```azurecli-interactive

az group delete --name MyAzureResourceGroupSLB

```

## Next steps

In this article, you updated an existing Standard Load Balancer with a IPv4 frontend IP configuration to a dual stack (IPv4 and IPv6) configuration. You also added IPv6 configurations to the NICs of the VMs in the backend pool. To learn more about IPv6 support in Azure virtual networks, see [What is IPv6 for Azure Virtual Network?](../virtual-network/ip-services/ipv6-overview.md)


# Backend Pool Management

# Backend pool management

The backend pool is a critical component of the load balancer. The backend pool defines the group of resources that serve traffic for a given load-balancing rule.

There are two ways of configuring a backend pool:

1. Network Interface Card (NIC)

1. IP address

To preallocate a backend pool with an IP address range that will contain virtual machines and Virtual Machine Scale Sets, configure the pool by IP address and virtual network ID.

This article focuses on configuration of backend pools by IP addresses.

## Configure backend pool by IP address and virtual network

In scenarios with pre-populated backend pools, use IP and virtual network.

You configure backend pool management on the backend pool object as highlighted in the following examples.

### PowerShell

Create a new backend pool:

```azurepowershell-interactive

$be = @{

ResourceGroupName = 'myResourceGroup'

LoadBalancerName = 'myLoadBalancer'

Name = 'myBackendPool'

}

$backendPool = New-AzLoadBalancerBackendAddressPool @be

```

Update backend pool with a new IP from existing virtual network:

```azurepowershell-interactive

$vnet = @{

Name = 'myVnet'

ResourceGroupName = 'myResourceGroup'

}

$virtualNetwork = Get-AzVirtualNetwork @vnet

$add1 = @{

IpAddress = '10.0.0.5'

Name = 'TestVNetRef'

VirtualNetworkId = $virtualNetwork.Id

}

$ip1 = New-AzLoadBalancerBackendAddressConfig @add1

$backendPool.LoadBalancerBackendAddresses.Add($ip1)

Set-AzLoadBalancerBackendAddressPool -InputObject $backendPool

```

Retrieve the backend pool information for the load balancer to confirm that the backend addresses are added to the backend pool:

```azurepowershell-interactive

$pool = @{

ResourceGroupName = 'myResourceGroup'

LoadBalancerName = 'myLoadBalancer'

Name = 'myBackendPool'

}

Get-AzLoadBalancerBackendAddressPool @pool

```

Create a network interface and add it to the backend pool. Set the IP address to one of the backend addresses:

```azurepowershell-interactive

$net = @{

Name = 'myNic'

ResourceGroupName = 'myResourceGroup'

Location = 'eastus'

PrivateIpAddress = '10.0.0.5'

Subnet = $virtualNetwork.Subnets[0]

}

$nic = New-AzNetworkInterface @net

```

Create a VM and attach the NIC with an IP address in the backend pool:

```azurepowershell-interactive

# Create a username and password for the virtual machine

$cred = Get-Credential

# Create a virtual machine configuration

$net = @{

Name = 'myNic'

ResourceGroupName = 'myResourceGroup'

}

$nic = Get-AzNetworkInterface @net

$vmc = @{

VMName = 'myVM1'

VMSize = 'Standard_DS1_v2'

}

$vmos = @{

ComputerName = 'myVM1'

Credential = $cred

}

$vmi = @{

PublisherName = 'MicrosoftWindowsServer'

Offer = 'WindowsServer'

Skus = '2019-Datacenter'

Version = 'latest'

}

$vmConfig =

New-AzVMConfig @vmc | Set-AzVMOperatingSystem -Windows @vmos | Set-AzVMSourceImage @vmi | Add-AzVMNetworkInterface -Id $nic.Id

# Create a virtual machine using the configuration

$vm = @{

ResourceGroupName = 'myResourceGroup'

Zone = '1'

Location = 'eastus'

VM = $vmConfig

}

$vm1 = New-AzVM @vm

```

### CLI

Using CLI you can either populate the backend pool via command-line parameters or through a JSON configuration file.

Create and populate the backend pool via the command-line parameters:

```azurecli-interactive

az network lb address-pool create \

--resource-group myResourceGroup \

--lb-name myLB \

--name myBackendPool \

--vnet {VNET resource ID} \

--backend-address name=addr1 ip-address=10.0.0.4 \

--backend-address name=addr2 ip-address=10.0.0.5

```

Create and populate the Backend Pool via JSON configuration file:

```azurecli-interactive

az network lb address-pool create \

--resource-group myResourceGroup \

--lb-name myLB \

--name myBackendPool \

--vnet {VNET resource ID} \

--backend-address-config-file @config_file.json

```

JSON configuration file:

```JSON

[

{

"name": "address1",

"virtualNetwork": "/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/virtualNetworks/{vnet-name}",

"ipAddress": "10.0.0.4"

},

{

"name": "address2",

"virtualNetwork": "/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/virtualNetworks/{vnet-name}",

"ipAddress": "10.0.0.5"

}

]

```

Retrieve the backend pool information for the load balancer to confirm that the backend addresses are added to the backend pool:

```azurecli-interactive

az network lb address-pool show \

--resource-group myResourceGroup \

--lb-name MyLb \

--name MyBackendPool

```

Create a network interface and add it to the backend pool. Set the IP address to one of the backend addresses:

```azurecli-interactive

az network nic create \

--resource-group myResourceGroup \

--name myNic \

--vnet-name myVnet \

--subnet mySubnet \

--network-security-group myNetworkSecurityGroup \

--lb-name myLB \

--private-ip-address 10.0.0.4

```

Create a VM and attach the NIC with an IP address in the backend pool:

```azurecli-interactive

az vm create \

--resource-group myResourceGroup \

--name myVM \

--nics myNic \

--image Ubuntu2204 \

--admin-username azureuser \

--generate-ssh-keys

```

### Limitations

1. IP based backends can only be used for Standard Load Balancers

1. The backend resources must be in the same virtual network as the load balancer for IP based LBs

1. IP-based load balancers backend instances must still be virtual machines or virtual machine scale sets. Attaching other PaaS services to the backend pool of an IP based Load Balancer isn't supported.

1. A load balancer with IP based Backend Pool can't function as a Private Link service

1. [Private endpoint resources](../private-link/private-endpoint-overview.md) can't be placed in an IP based backend pool

1. IP-based load balancers don't support ACI containers

1. Load balancers or services such as Application Gateway can't be placed in the backend pool of the load balancer

1. Inbound NAT Rules can't be specified by IP address

1. You can configure IP based and NIC based backend pools for the same load balancer. You can't create a single backend pool that mixes backed addresses targeted by NIC and IP addresses within the same pool.

1. A virtual machine in the same virtual network as an internal load balancer can't access the frontend of the ILB and its backend VMs simultaneously.

1. Internet routing preference IPs are currently not supported with IP based backend pools. Any Internet routing preference IPs in IP based backend pools will be billed and routed via the default Microsoft global network.

1. Performing move-related operations on VNETs that are attached to IP-based backend pools isn't supported

1. If backend pools are constantly changing (due to the constant addition or removal of backend resources). This can cause reset signals sent back to the source from the backend resource. As a workaround, you can use retries.

> [!IMPORTANT]

> When a backend pool is configured by IP address, it will behave as a Basic Load Balancer with default outbound enabled. For secure by default configuration and applications with demanding outbound needs, configure the backend pool by NIC.

## Next steps

In this article, you learned about Azure Load Balancer backend pool management and how to configure a backend pool by IP address and virtual network.

Learn more about [Azure Load Balancer](load-balancer-overview.md).

Review the [REST API](/rest/api/load-balancer/loadbalancerbackendaddresspools/createorupdate) for IP based backend pool management.


# Howto Load Balancer Imds

# Retrieve load balancer metadata using Azure Instance Metadata Service (IMDS)

## Prerequisites

* Use the [latest API version](/azure/virtual-machines/windows/instance-metadata-service?tabs=windows#supported-api-versions) for your request.

## Sample request and response

> [!IMPORTANT]

> This example bypasses proxies. You **must** bypass proxies when querying IMDS. For more information, see [Proxies](/azure/virtual-machines/windows/instance-metadata-service?tabs=windows#proxies).

## Schema breakdown

| **Data** | **Description** | **Version introduced** |

|------|-------------|--------------------|

| `publicIpAddresses` | The instance level Public or Private IP of the specific Virtual Machine instance | 2020-10-01

| `inboundRules` | List of load balancing rules or inbound NAT rules using which the Load Balancer directs traffic to the specific Virtual Machine instance. Frontend IP addresses and the Private IP addresses listed here belong to the Load Balancer.  | 2020-10-01

| `outboundRules` | List of outbound rules by which the Virtual Machine behind Load Balancer sends outbound traffic. Frontend IP addresses and the Private IP addresses listed here belong to the Load Balancer. | 2020-10-01

### [Windows](#tab/windows/)

```powershell

Invoke-RestMethod -Headers @{"Metadata"="true"} -Method GET -NoProxy -Uri "http://169.254.169.254:80/metadata/loadbalancer?api-version=2020-10-01" | ConvertTo-Json

```

> [!NOTE]

> The -NoProxy parameter was introduced in PowerShell 6.0. If you are using an older version of PowerShell, remove -NoProxy in the request body and make sure you are not using a proxy while retrieving IMDS info. Learn more [here](/azure/virtual-machines/windows/instance-metadata-service?tabs=windows#proxies).

>

### [Linux](#tab/linux/)

```bash

curl -H "Metadata:true" --noproxy "*" "http://169.254.169.254:80/metadata/loadbalancer?api-version=2020-10-01"

```

---

### Sample response

```json

{

"loadbalancer": {

"publicIpAddresses":[

{

"frontendIpAddress":"51.0.0.1",

"privateIpAddress":"10.1.0.4"

}

],

"inboundRules":[

{

"frontendIpAddress":"50.0.0.1",

"protocol":"tcp",

"frontendPort":80,

"backendPort":443,

"privateIpAddress":"10.1.0.4"

},

{

"frontendIpAddress":"2603:10e1:100:2::1:1",

"protocol":"tcp",

"frontendPort":80,

"backendPort":443,

"privateIpAddress":"ace:cab:deca:deed::1"

}

],

"outboundRules":[

{

"frontendIpAddress":"50.0.0.1",

"privateIpAddress":"10.1.0.4"

},

{

"frontendIpAddress":"2603:10e1:100:2::1:1",

"privateIpAddress":"ace:cab:deca:deed::1"

}

]

}

}

```

## Next steps

[Support and troubleshooting for Azure Load Balancer](load-balancer-support-help.md)

Learn more about [Azure Instance Metadata Service](/azure/virtual-machines/windows/instance-metadata-service)

[Retrieve all metadata for an instance](/azure/virtual-machines/windows/instance-metadata-service?tabs=windows#access-azure-instance-metadata-service)

[Deploy a standard load balancer](quickstart-load-balancer-standard-public-portal.md)


# Manage Admin State How To

# Manage Administrative (Admin) State in Azure Load Balancer

Administrative State (Admin State) is a feature of Azure Load Balancer that allows you to override the Load Balancer’s health probe behavior on a per backend pool instance basis. There are three types of admin state values: **Up**, **Down**, **None**.

You can use the Azure portal, Azure PowerShell, or Azure CLI to manage the admin state for a backend pool instance. Each section provides instructions for each method with examples for setting, updating, or removing an admin state configuration.

## Prerequisites

# [Azure portal](#tab/azureportal)

- Access to the Azure portal.

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)

- An existing resource group for all resources.

- Two or more existing [Virtual Machines](/azure/virtual-machines/windows/quick-create-portal).

- An existing [standard load balancer](quickstart-load-balancer-standard-internal-portal.md) in the same subscription and virtual network as the virtual machines.

- The load balancer should have a backend pool with health probes and load balancing rules attached.

# [Azure PowerShell](#tab/azurepowershell)

- Access to the Azure portal.

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)

- An existing resource group for all resources.

- Existing [Virtual Machines](/azure/virtual-machines/windows/quick-create-powershell).

- An existing [standard load balancer](quickstart-load-balancer-standard-internal-powershell.md) in the same subscription and virtual network as the virtual machine.

- The load balancer should have a backend pool with health probes and load balancing rules attached.

# [Azure CLI](#tab/azurecli)

- Access to the Azure portal.

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)

- An existing resource group for all resources.

- Existing [Virtual Machines](/azure/virtual-machines/windows/quick-create-cli).

- An existing [standard load balancer](quickstart-load-balancer-standard-internal-cli.md) in the same subscription and virtual network as the virtual machine.

- The load balancer should have a backend pool with health probes and load balancing rules attached.

[!INCLUDE [azure-cli-prepare-your-environment-no-header.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment-no-header.md)]

---

## Set admin state on a new backend pool instance

In this section, you learn how to set an admin state to **Up** or **Down** as part of a new backend pool create.

# [Azure portal](#tab/azureportal)

1. Sign in to the Azure portal.

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select your load balancer from the list.

4. In your load balancer's page, select **Backend pools** under **Settings**.

5. Select **+ Add** in **Backend pools** to add a new backend pool.

6. In the **Add backend pool** window, enter or select the following information:

| **Setting** | **Value** |

|------------------------|----------------------------|

| **Name**                   | Enter `myBackendpool`.     |

| **Backend Pool Configuration** | Select **IP Address**. |

| **IP addresses**       | |

| **Backend Address Name** | Enter the name of your backend address. |

| **IP Address**         | Select the IP address to be added to the backend pool. |

7. Select **Save**.

8. In your **Backend pools** page, select the corresponding **Admin State** value of your recently added backend pool instance.

9.  In your **Admin state details** window, select **Down** from the dropdown menu.

10. Select **Save**.

# [Azure PowerShell](#tab/azurepowershell)

1. Connect to your Azure subscription with Azure PowerShell.

2. Create a new backend pool with a backend pool instance while setting the admin state value to UP or DOWN with [`New-AzLoadBalancerBackendAddressConfig`](/powershell/module/az.network/new-azloadbalancerbackendaddressconfig). Replace the values in brackets with the names of the resources in your configuration.

```azurepowershell

$rsg = <resource-group>

$vnt = <virtual-network-name>

$lbn = <load-balancer-name>

$bep = <backend-pool-name>

$ip = <ip-address>

$ben = <backend-address-name>

$vnet = Get-AzVirtualNetwork -Name $vnt -ResourceGroupName $rsg

$lb = Get-AzLoadBalancer -ResourceGroupName $rsg -Name $lbn

$ip1 = New-AzLoadBalancerBackendAddressConfig -IpAddress $ip -Name $ben -VirtualNetworkId $vnet.Id -AdminState “DOWN”

$lb | New-AzLoadBalancerBackendAddressPool -LoadBalancerBackendAddress $ip1 -Name $bep

```

This example sets a new backend pool instance admin state to DOWN with the following defined values:

[!INCLUDE [load-balancer-admin-state-example-values](../../includes/load-balancer-admin-state-example-values.md)]

```azurepowershell

$rsg = "MyResourceGroup"

$vnt = "MyVnet"

$lbn = "MyLB"

$bep = "MyAddressPool"

$ip = "10.0.2.4"

$ben = "MyBackend"

$vnet = Get-AzVirtualNetwork -Name $vnt -ResourceGroupName $rsg

$lb = Get-AzLoadBalancer -ResourceGroupName $rsg -Name $lbn

$ip1 = New-AzLoadBalancerBackendAddressConfig -IpAddress $ip -Name $ben -VirtualNetworkId $vnet.Id -AdminState “DOWN”

$lb | New-AzLoadBalancerBackendAddressPool -LoadBalancerBackendAddress $ip1 -Name $bep

```

# [Azure CLI](#tab/azurecli)

1. Connect to your Azure subscription with Azure CLI.

2. Create a new backend pool with a backend pool instance while setting admin state value to UP or DOWN with [az network lb address-pool create](/cli/azure/network/lb/address-pool#az-network-lb-pool-create). Replace the values in brackets with the names of the resources in your configuration.

```azurecli

az network lb address-pool create \

-g <resource-group> \

--lb-name <lb-name> \

-n <lb-backend-pool-name> \

--vnet <virtual-network-name> \

--backend-address “{name: <new-lb-backend-pool-address-name>,ip-address:<new-lb-backend-pool-address>}” \

--admin-state <admin-state-value>

```

1. This example updates a backend pool instance admin state to DOWN with the following defined values:

[!INCLUDE [load-balancer-admin-state-example-values](../../includes/load-balancer-admin-state-example-values.md)]

```azurecli

az network lb address-pool create \

-g MyResourceGroup \

--lb-name MyLb \

-n MyAddressPool \

--vnet MyVnet \

--backend-address “{name: MyBackend,ip-address:10.0.2.4}” \

--admin-state DOWN

```

---

## Set admin state as part of new backend pool instance after creation

In this section, you learn how to set an admin state to **Up** or **Down** as part of a new backend pool instance add.

# [Azure portal](#tab/azureportal)

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer** and select **Load balancers** in the search results.

3. On the load balancer's **Overview** page, select your load balancer from the list.

4. In your load balancer's page, select **Backend pools** under **Settings**.

5. Select your backend pool.

6. In your backend pool's page, select **+ Add** under **IP configurations**.

> [!NOTE]

> This step is assuming your backend pool is NIC-based.

7. Select the virtual machine you want to add to the backend pool.

8. Select **Add** and **Save**.

9. In your **Backend pools** page, select the corresponding **Admin State** value of your recently added backend pool instance.

10. In your **Admin state details** window, select **Up** from the dropdown menu.

11.	Select **Save**.

# [Azure PowerShell](#tab/azurepowershell)

1. Connect to your Azure subscription with Azure PowerShell.

1. Add a new backend pool instance with the admin state value configured to UP or DOWN with [New-AzLoadBalancerBackendAddressConfig](/powershell/module/az.network/new-azloadbalancerbackendaddressconfig). Replace the values in brackets with the names of the resources in your configuration.

```azurepowershell

$rsg = <resource-group>

$vnt = <virtual-network-name>

$lbn = <load-balancer-name>

$bep = <backend-pool-name>

$ip = <ip-address>

$ben = <backend-address-name>

$vnet = Get-AzVirtualNetwork -Name $vnt -ResourceGroupName $rsg

$lb = Get-AzLoadBalancer -ResourceGroupName $rsg -Name $lbn

$ip1 = New-AzLoadBalancerBackendAddressConfig -IpAddress $ip -Name $ben -VirtualNetworkId $vnet.Id -AdminState “UP”

$lb | Set-AzLoadBalancerBackendAddressPool -LoadBalancerBackendAddress $ip1 -Name $bep

```

1. This example sets a new backend pool instance admin state to UP with the following defined values:

[!INCLUDE [load-balancer-admin-state-example-values](../../includes/load-balancer-admin-state-example-values.md)]

```azurepowershell

# Set the values for the variables

$rsg = "MyResourceGroup"

$vnt = "MyVnet"

$lbn = "MyLB"

$bep = "MyAddressPool"

$ip = "10.0.2.4"

$ben = "MyBackend"

$vnet = Get-AzVirtualNetwork -Name $vnt -ResourceGroupName $rsg

$lb = Get-AzLoadBalancer -ResourceGroupName $rsg -Name $lbn

$ip1 = New-AzLoadBalancerBackendAddressConfig -IpAddress $ip -Name $ben -VirtualNetworkId $vnet.Id -AdminState “UP”

$lb | Set-AzLoadBalancerBackendAddressPool -LoadBalancerBackendAddress $ip1 -Name $bep

```

# [Azure CLI](#tab/azurecli)

1.	Connect to your Azure subscription with Azure CLI.

2.	Add a new backend pool instance with the admin state value is configured. The value can be set to UP or DOWN with [az network lb address-pool update](/cli/azure/network/lb/address-pool#az-network-lb-address-pool-update) . Replace the values in brackets with the names of the resources in your configuration.

```azurecli

az network lb address-pool update \

-g <resource-group> \

--lb-name <lb-name> \

-n <lb-backend-pool-name> \

--vnet <virtual-network-name> \

--backend-address “{name: <new-lb-backend-pool-address-name>,ip-address:<new-lb-backend-pool-address>}” |

--admin-state <admin-state-value>

```

1. This example sets a new backend pool instance admin state to UP with the following defined values:

[!INCLUDE [load-balancer-admin-state-example-values](../../includes/load-balancer-admin-state-example-values.md)]

```azurecli

az network lb address-pool update \

-g MyResourceGroup \

--lb-name MyLb \

-n MyAddressPool \

--vnet MyVnet \

--backend-address “{name: MyBackend,ip-address:10.0.2.4}” |

--admin-state UP

```

> [!NOTE]

> You can also use [`az network lb address-pool address add`](/cli/azure/network/lb/address-pool/address##az-network-lb-address-pool-add) to set admin state on as part of a new backend pool instance add.

---

## Update admin state on existing backend pool instance

In this section, you learn how to update an existing admin state from existing backend pool instance by setting the value to **Up** or **Down**.

# [Azure portal](#tab/azureportal)

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer** and select **Load balancers** in the search results.

3. Select your load balancer from the list.

4. In your load balancer's page, select **Backend pools** under **Settings**.

9. In your **Backend pools** page, select the corresponding **Admin State** value of your recently added backend pool instance.

10. In your **Admin state details** window, select **Up** from the dropdown menu.

11. Select **Save**.

# [Azure PowerShell](#tab/azurepowershell)

1. Connect to your Azure subscription with Azure PowerShell.

2. Update an existing backend pool instance with the admin state value configured to UP or DOWN with [New-AzLoadBalancerBackendAddressConfig](/powershell/module/az.network/new-azloadbalancerbackendaddressconfig). Replace the values in brackets with the names of the resources in your configuration.

```azurepowershell

# Set the values for the variables

$rsg = <resource-group>

$vnt = <virtual-network-name>

$lbn = <load-balancer-name>

$bep = <backend-pool-name>

$ip = <ip-address>

$ben = <backend-address-name>

$vnet = Get-AzVirtualNetwork -Name $vnt -ResourceGroupName $rsg

$lb = Get-AzLoadBalancer -ResourceGroupName $rsg -Name $lbn

$ip1 = New-AzLoadBalancerBackendAddressConfig -IpAddress $ip -Name $ben -VirtualNetworkId $vnet.Id -AdminState “DOWN”

$lb | Set-AzLoadBalancerBackendAddressPool -LoadBalancerBackendAddress $ip1 -Name $bep

```

1. This example sets an existing backend pool instance admin state to DOWN with the following defined values:

[!INCLUDE [load-balancer-admin-state-example-values](../../includes/load-balancer-admin-state-example-values.md)]

```azurepowershell

$rsg = "MyResourceGroup"

$vnt = "MyVnet"

$lbn = "MyLB"

$bep = "MyAddressPool"

$ip = "10.0.2.4"

$ben = "MyBackend"

$vnet = Get-AzVirtualNetwork -Name $vnt -ResourceGroupName $rsg

$lb = Get-AzLoadBalancer -ResourceGroupName $rsg -Name $lbn

$ip1 = New-AzLoadBalancerBackendAddressConfig -IpAddress $ip -Name $ben -VirtualNetworkId $vnet.Id -AdminState “DOWN”

$lb | Set-AzLoadBalancerBackendAddressPool -LoadBalancerBackendAddress $ip1 -Name $bep

```

# [Azure CLI](#tab/azurecli)

1. Connect to your Azure subscription with Azure CLI.

2. Update an existing backend pool instance, and configure the admin state value to UP or DOWN with [az network lb address-pool update](/cli/azure/network/lb/address-pool#az-network-lb-address-pool-update). Replace the values in brackets with the names of the resources in your configuration.

```azurecli

az network lb address-pool update \

-g <resource-group> \

--lb-name <lb-name> \

-n <lb-backend-pool-name> \

--backend-address “{name: <lb-backend-pool-address-name>,ip-address:<lb-backend-pool-address>}” |

--admin-state <admin-state-value>

```

1. This example updates an existing backend pool instance admin state to DOWN with the following defined values:

[!INCLUDE [load-balancer-admin-state-example-values](../../includes/load-balancer-admin-state-example-values.md)]

```azurecli

az network lb address-pool update \

-g MyResourceGroup \

--lb-name MyLb \

-n MyAddressPool \

--backend-address “{name: MyBackend,ip-address:10.0.2.4}” |

--admin-state DOWN

```

> [!NOTE]

> You can also use [`az network lb address-pool address update`](/cli/azure/network/lb/address-pool/address#az-network-lb-address-pool-update) to update admin state on an existing backend pool instance.

---

## Removing admin state from existing backend pool instance

In this section, you learn how to remove an existing admin state from an existing backend pool instance. This is done by setting the admin state value to **None**.

# [Azure portal](#tab/azureportal)

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer** and select **Load balancers** in the search results.

3. Select your load balancer from the list.

4. In your load balancer's page, select **Backend pools** under **Settings**.

5. Select the corresponding **Admin State** value of your backend pool instance that you would like to remove.

6. In your admin state’s window, select **None** from the dropdown menu.

7. Select **Save**.

# [Azure PowerShell](#tab/azurepowershell)

1. Connect to your Azure subscription with Azure PowerShell.

2. Remove an existing backend pool instance. This is done by setting the admin state value to **NONE** with [New-AzLoadBalancerBackendAddressConfig](/powershell/module/az.network/new-azloadbalancerbackendaddressconfig). Replace the values in brackets with the names of the resources in your configuration.

```azurepowershell

# Set the values for the variables

$rsg = <resource-group>

$vnt = <virtual-network-name>

$lbn = <load-balancer-name>

$bep = <backend-pool-name>

$ip = <ip-address>

$ben = <backend-address-name>

# Remove the admin state from the backend pool instance

$vnet = Get-AzVirtualNetwork -Name $vnt -ResourceGroupName $rsg

$lb = Get-AzLoadBalancer -ResourceGroupName $rsg -Name $lbn

$ip1 = New-AzLoadBalancerBackendAddressConfig -IpAddress $ip -Name $ben -VirtualNetworkId $vnet.Id -AdminState “NONE”

$lb | Set-AzLoadBalancerBackendAddressPool -LoadBalancerBackendAddress $ip1 -Name $bep

```

1. This example removes an existing backend pool instance admin state with the following defined values:

[!INCLUDE [load-balancer-admin-state-example-values](../../includes/load-balancer-admin-state-example-values.md)]

```azurepowershell

# Set the values for the variables

$rsg = "MyResourceGroup"

$vnt = "MyVnet"

$lbn = "MyLB"

$bep = "MyAddressPool"

$ip = "10.0.2.4"

# Remove the admin state from the backend pool instance

$vnet = Get-AzVirtualNetwork -Name $vnt -ResourceGroupName $rsg

$lb = Get-AzLoadBalancer -ResourceGroupName $rsg -Name $lbn

$ip1 = New-AzLoadBalancerBackendAddressConfig -IpAddress $ip -Name $ben -VirtualNetworkId $vnet.Id -AdminState “NONE”

$lb | Set-AzLoadBalancerBackendAddressPool -LoadBalancerBackendAddress $ip1 -Name $bep

```

# [Azure CLI](#tab/azurecli)

1. Connect to your Azure subscription with Azure CLI.

2. Remove an existing backend pool instance by setting the admin state value to **None** with [az network lb address-pool update](/cli/azure/network/lb/address-pool#az-network-lb-address-pool-update). Replace the values in brackets with the names of the resources in your configuration.

```azurecli

# Remove the admin state from the backend pool instance

az network lb address-pool update \

-g <resource-group> \

--lb-name <lb-name> \

-n <lb-backend-pool-name> \

--backend-address “{name: <lb-backend-pool-address-name>,ip-address:<lb-backend-pool-address>}” |

--admin-state <admin-state-value>

```

1. This example removes an existing backend pool instance admin state with the following defined values:

[!INCLUDE [load-balancer-admin-state-example-values](../../includes/load-balancer-admin-state-example-values.md)]

```azurecli

az network lb address-pool update \

-g MyResourceGroup \

--lb-name MyLb \

-n MyAddressPool \

--backend-address "{name: MyBackend,ip-address:10.0.2.4}" \

--admin-state NONE

```

> [!NOTE]

> You can also use [`az network lb address-pool address update`](/cli/azure/network/lb/address-pool/address#az-network-lb-address-pool-update) to remove admin state from an existing backend pool instance.

---

## Next Steps

> [!div class="nextstepaction"]

> [Administrative State (Admin State) in Azure Load Balancer](admin-state-overview.md)


# Instance Metadata Service Load Balancer

# Retrieve load balancer information by using Azure Instance Metadata Service

IMDS (Azure Instance Metadata Service) provides information about currently running virtual machine instances. The service is a REST API that's available at a well-known, nonroutable IP address (169.254.169.254).

When you place virtual machine or virtual machine set instances behind an Azure Standard Load Balancer, you can use IMDS to retrieve metadata related to the load balancer and the instances.

The metadata includes the following information for the virtual machines or virtual machine scale sets:

* The instance level Public or Private IP of the specific Virtual Machine instance

* Inbound rule configurations of the load balancer of each private IP of the network interface.

* Outbound rule configurations of the load balancer of each private IP of the network interface.

## Access the load balancer metadata using IMDS

For more information on how to access the load balancer metadata, see [Use Azure Instance Metadata Service to access load balancer information](howto-load-balancer-imds.md).

## Troubleshoot common error codes

For more information on support and troubleshooting resources, see [Support and troubleshooting for Azure Load Balancer](load-balancer-support-help.md).

## Support

If you're unable to retrieve a metadata response after multiple attempts, create a support issue in the Azure portal.

## Next steps

Learn more about [Azure Instance Metadata Service](/azure/virtual-machines/windows/instance-metadata-service)

[Deploy a standard load balancer](quickstart-load-balancer-standard-public-portal.md)


# Load Balancer Test Frontend Reachability

# Test reachability of Azure Public Load Balancer frontends with ping and traceroute

Standard Public Azure Load Balancer frontend IPv4 and IPv6 addresses support testing reachability using ping and traceroute. Testing reachability of a load balancer frontend is useful for troubleshooting inbound connectivity issues to Azure resources. In this article, you learn how to use ping and traceroute for testing a frontend of an existing Standard public load balancer. It can be completed from an Azure Virtual Machine or from a device outside of Azure.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) and access to the Azure portal.

- A standard public load balancer with an IPv4 and IPv6 frontend in your subscription. For more information on creating an Azure Load Balancer, see [Quickstart: Create a public load balancer](/azure/load-balancer/quickstart-load-balancer-standard-public-portal) to load balance VMs using the Azure portal.

- An Azure Virtual Machine with a public IP address assigned to its network interface. For more information on creating a virtual machine with a public IP, see [Quickstart: Create a Windows virtual machine in the Azure portal](/azure/virtual-machines/windows/quick-create-portal).

> [!NOTE]

> Testing inbound connectivity to Azure Load Balancer frontends is only supported for public load balancers. Testing inbound connectivity to internal load balancer frontends is not supported.

## Testing from a device outside of Azure

### [Windows](#tab/windows-outside)

This section describes testing reachability of a standard load balancer frontend from a Windows device outside of Azure.

### [Linux](#tab/linux-outside)

This section describes testing reachability of a standard load balancer frontend from a Linux device outside of Azure.

---

### Test the load balancer's frontend

Choose either ping or traceroute to test reachability of a standard load balancer frontend from a device outside of Azure.

### [Ping](#tab/ping/windows-outside)

Follow these steps to test reachability of a standard public load balancer frontend using `ping` from a Windows device outside of Azure:

1. From your Windows device, open the **Search taskbar** and enter `cmd`. Select **Command Prompt**.

2. In the command prompt, type the following command:

```cmd

ping <Input your load balancer public IP address>

```

3. Review ping's output.

### [Ping](#tab/ping/linux-outside)

Follow these steps to test reachability of a standard public load balancer frontend using `ping` from a Linux device outside of Azure:

1. Open Terminal.

2. Type the following command:

```bash

ping <Input your load balancer public IP address>

```

3. Review ping's output.

### [Traceroute](#tab/traceroute/windows-outside)

Follow these steps to test reachability of a standard public load balancer frontend using `tracert` from a Windows device outside of Azure:

1. From your Windows device, open the **Search taskbar** and enter `cmd`. Select **Command Prompt**.

2. In the command prompt, type the following command:

```cmd

tracert <Input your load balancer public IP address>

```

3. Review tracert's output.

### [Traceroute](#tab/traceroute/linux-outside)

Follow these steps to test reachability of a standard public load balancer frontend using `traceroute` from a Linux device outside of Azure:

1. Open Terminal.

2. Type the following command:

```bash

traceroute -I <Input your load balancer public IP address>

```

3. Review traceroute's output.

---

## Testing from an Azure Virtual Machine

This section describes how to test reachability of a standard public load balancer frontend from an Azure Virtual Machine. First, you create an inbound Network Security Group (NSG) rule on the virtual machine to allow ICMP traffic. Then, you test reachability of the frontend of the load balancer from the virtual machine with ping or traceroute.

### Configure inbound NSG rule

1. Sign in to the Azure portal.

1. In the Search bar at the top of the portal, enter **Virtual machines** and select Virtual machines.

1. In **Virtual machines**, select your virtual machine from the list.

1. In the virtual machine’s menu, select **Networking** and then select **Add inbound port rule**.

1. In **Add inbound security rule**, enter or select the following information:

| **Setting** | **Value** |

| --- | --- |

| **Source** | Enter **Any** |

| **Source port ranges** | Enter **\*** |

| **Destination** | Enter **Any** |

| **Service** | Enter **Custom** |

| **Destination port ranges** | Enter **\*** |

| **Protocol** | Select **ICMP** |

| **Action** | Select **Allow** |

| **Priority** | Enter **100** or a priority of your choosing. |

| **Name** | Enter **AllowICMP** or a name of your choosing |

| **Description** | Leave as Blank or enter a description |

1. Select **Add**.

### Connect to the virtual machine

### [Windows](#tab/windowsvm)

This section describes testing reachability of a standard load balancer frontend from a Windows Virtual Machine on Azure.

1. Return to **Overview** in the virtual machine’s menu and select **Connect**.

1. Sign in to your virtual machine using RDP, SSH, or Bastion.

### [Linux](#tab/linuxvm/)

This section describes testing reachability of a standard load balancer frontend from a Linux Virtual Machine on Azure.

1. Return to **Overview** in the virtual machine’s menu and select **Connect**.

1. Sign in to your virtual machine using SSH or Bastion.

---

### Test the load balancer's frontend

Choose either ping or traceroute to test reachability of a standard public load balancer frontend from an Azure Virtual Machine.

### [Ping](#tab/ping/windowsvm)

Follow these steps to test reachability of a standard public load balancer frontend using `ping` from a Windows virtual machine:

1. From your Windows device, open the **Search taskbar** and enter `cmd`. Select **Command Prompt**.

2. In the command prompt, type the following command:

```cmd

ping <Input your load balancer public IP address>

```

3. Review ping's output.

### [Ping](#tab/ping/linuxvm)

Follow these steps to test reachability of a standard public load balancer frontend using `ping` from a Linux virtual machine:

1. Open Terminal.

2. Type the following command:

```bash

ping <Input your load balancer public IP address>

```

3. Review ping's output.

### [Traceroute](#tab/traceroute/windowsvm)

Follow these steps to test reachability of a standard public load balancer frontend using `tracert` from a Windows virtual machine:

1. From your Windows device, open the **Search taskbar** and enter `cmd`. Select **Command Prompt**.

2. In the command prompt, type the following command:

```dos

tracert <Input your load balancer public IP address>

```

3. Review tracert's output.

### [Traceroute](#tab/traceroute/linuxvm)

Follow these steps to test reachability of a standard public load balancer frontend using `traceroute` from a Linux virtual machine:

1. Open Terminal.

2. Type the following command:

```bash

traceroute -I <Input your load balancer public IP address>

```

3. Review traceroute's output.

---

## Expected replies with ping

Based on the current health probe state of your backend instances, you receive different replies when testing the Load Balancer’s frontend with ping. Review the following scenarios for the expected reply:

| **Scenario** | **Expected reply** |

| --- | --- |

| **All backend instances are probed DOWN** | Destination host unreachable  |

| **All backend instances turned OFF** | Unresponsive: Request timed out |

| **At least 1 backend instance is probed UP** | Successful echo replies |

| **No backend instances behind Load Balancer/No load balancing rules associated** | Unresponsive: Request timed out |

## Usage considerations

- ICMP pings can't be disabled and are allowed by default on Standard Public Load Balancers.

- ICMP pings with packet sizes larger than 64 bytes will be dropped, leading to timeouts.

- Outbound ICMP pings are not supported on a Standard Load Balancer.

- ICMP pings are not supported on Global or Gateway Load Balancers.

- ICMP pings are not supported for regional load balancers (load balancers that are deployed behind a Global Load Balancer).

> [!NOTE]

> ICMP ping requests are not sent to the backend instances; they are handled by the Load Balancer.

## Next steps

- To troubleshoot load balancer issues, see [Support and troubleshooting for Azure Load Balancer](load-balancer-support-help.md).

- Learn how to [Manage rules for Azure Load Balancer using the Azure portal](manage-rules-how-to.md).


# Manage Probes How To

# Manage health probes for Azure Load Balancer using the Azure portal

Azure Load Balancer uses health probes to monitor the health of backend instances. In this article, you learn how to manage health probes for Azure Load Balancer.

There are three types of health probes:

| | Standard SKU | Basic SKU |

| --- | --- | --- |

| **Probe types** | TCP, HTTP, HTTPS | TCP, HTTP |

| **Probe down behavior** | All probes down, all TCP flows continue. | All probes down, all TCP flows expire. |

Health probes have the following properties:

| Health Probe configuration | Details |

| --- | --- |

| Name | Name of the health probe. This is a name you get to define for your health probe |

| Protocol | Protocol of health probe. This is the protocol type you would like the health probe to use. Available options are: TCP, HTTP, HTTPS |

| Port | Port of the health probe. The destination port you would like the health probe to use when it connects to the virtual machine to check the virtual machine's health status. You must ensure that the virtual machine is also listening on this port (that is, the port is open). |

| Interval (seconds) | Interval of health probe. The amount of time (in seconds) between consecutive health check attempts to the virtual machine |

| Used by | The list of load balancer rules using this specific health probe. You should have at least one rule using the health probe for it to be effective |

| Path | The URI used for requesting health status from the virtual machine instance by the health probe (only applicable for HTTPS probes).

>[!IMPORTANT]

>Load Balancer health probes originate from the IP address 168.63.129.16 and must not be blocked for probes to mark your instance as up. To see this probe traffic within your backend instance, review [the Azure Load Balancer FAQ](./load-balancer-faqs.yml).

>

>

>Regardless of configured time-out threshold, HTTP(S) load balancer health probes will automatically mark the instance as down if the server returns any status code that isn't HTTP 200 OK or if the connection is terminated via TCP reset.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- A standard public load balancer in your subscription. For more information on creating an Azure Load Balancer, see [Quickstart: Create a public load balancer to load balance VMs using the Azure portal](quickstart-load-balancer-standard-public-portal.md). The load balancer name for the examples in this article is **myLoadBalancer**.

## TCP health probe

In this section, you learn how to add and remove a TCP health probe. A public load balancer is used in the examples.

### Add a TCP health probe

In this example, you create a TCP health probe to monitor port 80.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Health probes** in **Settings**.

5. Select **+ Add** in **Health probes** to add a probe.

6. Enter or select the following information in **Add health probe**.

| Setting | Value |

| ------- | ----- |

| Name | Enter **myHealthProbe**. |

| Protocol | Select **TCP**. |

| Port | Enter the **TCP** port you wish to monitor. For this example, it's **port 80**. |

| Interval | Enter an interval between probe checks. For this example, it's the default of **5**. |

7. Select **Add**.

### Remove a TCP health probe

In this example, you remove a TCP health probe.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Health probes** in **Settings**.

5. Select the three dots next to the rule you want to remove.

6. Select **Delete**.

## HTTP health probe

In this section, you learn how to add and remove an HTTP health probe. A public load balancer is used in the examples.

### Add an HTTP health probe

In this example, you create an HTTP health probe.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Health probes** in **Settings**.

5. Select **+ Add** in **Health probes** to add a probe.

6. Enter or select the following information in **Add health probe**.

| Setting | Value |

| ------- | ----- |

| Name | Enter **myHealthProbe**. |

| Protocol | Select **HTTP**. |

| Port | Enter the **TCP** port you wish to monitor. For this example, it's **port 80**. |

| Path | Enter a URI used for requesting health status. For this example, it's **/**. |

| Interval | Enter an interval between probe checks. For this example, it's the default of **5**. |

7. Select **Add**.

### Remove an HTTP health probe

In this example, you remove an HTTP health probe.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Health probes** in **Settings**.

5. Select the three dots next to the rule you want to remove.

6. Select **Delete**.

## HTTPS health probe

In this section, you learn how to add and remove an HTTPS health probe. A public load balancer is used in the examples.

### Add an HTTPS health probe

In this example, you create an HTTPS health probe.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Health probes** in **Settings**.

5. Select **+ Add** in **Health probes** to add a probe.

6. Enter or select the following information in **Add health probe**.

| Setting | Value |

| ------- | ----- |

| Name | Enter **myHealthProbe**. |

| Protocol | Select **HTTPS**. |

| Port | Enter the **TCP** port you wish to monitor. For this example, it's **port 443**. |

| Path | Enter a URI used for requesting health status. For this example, it's **/**. |

| Interval | Enter an interval between probe checks. For this example, it's the default of **5**. |

7. Select **Add**.

### Remove an HTTPS health probe

In this example, you remove an HTTPS health probe.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

3. Select **myLoadBalancer** or your load balancer.

4. In the load balancer page, select **Health probes** in **Settings**.

5. Select the three dots next to the rule you want to remove.

6. Select **Delete**.

## Next steps

In this article, you learned how to manage health probes for an Azure Load Balancer.

For more information about Azure Load Balancer, see:

- [What is Azure Load Balancer?](load-balancer-overview.md)

- [Frequently asked questions - Azure Load Balancer](load-balancer-faqs.yml)

- [Azure Load Balancer health probes](load-balancer-custom-probe-overview.md)


# Create Custom Http Health Probe Howto

# Create a custom HTTP/HTTPS health probe for Azure Load Balancer

In this article, you learn to create a custom API for HTTP [health probes](load-balancer-custom-probe-overview.md) using Python, FLASK, and psutil. Health checks are performed on backend instances using HTTP GET and marked as healthy or unhealthy based on the response. The custom probe in this article marks instances as unhealthy if their CPU usage is over 75%. HTTP health probes can be used for many purposes, not just CPU utilization, when combine with your own logic and health checks.

## Prerequisites

-  An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) and access to the Azure portal.

- An existing standard SKU Azure Load Balancer. For more information on creating a load balancer, see [Create a public load balancer using the Azure portal](quickstart-load-balancer-standard-public-portal.md).

- An Azure Virtual Machine running linux in the backend pool of the Azure Load Balancer, see [Create a virtual machine using the Azure portal](/azure/virtual-machines/linux/quick-create-portal).

- Linux virtual machine has *python3*, *pip* and the following packages installed:

- *flask*

- *flask_restful*

- *psutil*

- Remote access to the virtual machine via SSH or Azure Bastion.

> [!IMPORTANT]

> [!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

>

## Configure API on virtual machine

In this section, you configure the virtual machine to run the custom API for the HTTP health probe.

1. Connect to the VM using SSH or Azure Bastion. This article uses SSH to connect to the VM.

1. Create a new folder to store the code for the health API, and enter the new folder:

```bash

mkdir health_API && cd health_API

```

1. Create a new python file and paste the following code into the file:

```bash

touch health.py && vim health.py

```

```python

# Import libraries

from flask import Flask

from flask_restful import Resource, Api

import psutil

# Define app and API

app = Flask(__name__)

api = Api(app)

# Define API GET method

class check_CPU_VM(Resource):

def get(self):

# If VM CPU utilization is over 75%, throw an error

if psutil.cpu_percent() >= 75.0:

return '',408

# Else keep the VM as healthy

else:

return '',200

# Add the GET method to the API at the path 'health_check'

api.add_resource(check_CPU_VM, '/health_check/')

# Expose the API on all available IP address on the VM

if __name__ == "__main__":

app.run(debug=True, host ="0.0.0.0")

```

1. Once you have copied the code into the file, install **python3** and the required packages (**flask, flask_restful, psutil**) if necessary. The following commands install python3 and the required packages on Ubuntu:

```bash

#Install Python

sudo apt-get update

sudo apt-get install python3

sudo apt-get install python3-pip

pip3 install flask flask_restful psutil

```

1. Run the API using the following command:

```bash

python3 health.py

```

1. Once the API starts running, you see two IP addresses that are exposed to the API on port **5000**.

- The first IP address is the local IP address that is only available to the VM.

- The second IP address is the private IP address of the VM, the Load Balancer’s health probe tests this IP address.

> [!NOTE]

> The API will need to be running on the VM for the health probe to work. When you close the SSH session, the API will stop running. Keep the window open while creating the health probe or run the API in the background.

## Create health probe

In this section, you create the health probe used to check the health of the backend instances running the custom API.

1. Navigate to the Azure portal and select the load balancer that you would like to add the health probe to.

1. Select **Health probes** under **Settings**.

1. Select **+ Add**.

1. In the **Add Health Probe** page, enter or select the following information:

| **Setting** | **Value** |

| --- | --- |

| **Name** | Enter **HTTP_Health** |

| **Protocol** | Select **HTTP** |

| **Port** | Enter **5000** |

| **Path** | Enter **/health_check/** |

| **Interval (seconds)** | Enter **5** |

1. Select **OK** to create the health probe.

## Create the load balancer rule

In this section, you create the load balancer rule that uses the HTTP health probe.

1. From the load balancer overview page, select **Load balancing rules** under **Settings**.

1. Select **+ Add**.

1. On the **Add load balancing rule** page, enter the following information:

| **Setting** | **Value** |

| --- | --- |

| **Name** | Enter **custom_HTTP_rule** |

| **Frontend IP address** | Select the frontend IP address of your load balancer. |

| **Backend pool** | Select the backend pool that you want to use. |

| **Protocol** | Select **TCP** |

| **Port** | Enter **5000** |

| **Backend port** | Enter **5000** |

| **Health probe** | Select **HTTP_Health (HTTP:5000/health_check/)** |

| **Session persistence** | Select **None** |

| **Idle timeout (minutes)** | Enter **5** |

1. Select **Save** to create the load balancing rule.

## Verify health probe

In this section, you verify that the health probe is working as expected by checking the running API and the load balancer metrics.

1. Navigate back to the SSH session to the VM running the API.

1. In the console window that is running the API, you should see a **GET** request every 5 seconds checking the health of the VM, and responding with a **200** status code if the VM is healthy.

1. Enter **ctrl+c** to stop the API.

1. Close the SSH session to the VM.

1. Navigate back to the load balancer overview page.

1. Select **Metrics** under **Monitoring**.

1. Select **+ Add metric** and enter/select the following information:

| **Setting** | **Value** |

| --- | --- |

| **Scope** | Select the load balancer to monitor. |

| **Metric Namespace** | Select **Load balancer standard** |

| **Metric** | Select **Health Probe status** |

| **Aggregation** | Select **Max** |

1. Select **checkmark** to add the metric.

## Clean up resources

When no longer needed, delete the resource group, load balancer, and all related resources.

## Next steps

> [!div class="nextstepaction"]

> [Manage health probes for Azure Load Balancer using the Azure portal](manage-probes-how-to.md)


# Load Balancer Monitor Metrics Cli

# Get Load Balancer metrics with Azure Monitor CLI

In this article, you learn some examples to list Load Balancer metrics using Azure Monitor CLI.

Complete reference documentation and other samples for retrieving metrics using Azure Monitor CLI are available in the [az monitor metrics reference](/cli/azure/monitor/metrics).

## Table of metric names via CLI

When you use CLI, Load Balancer metrics may use a different metric name for the CLI parameter value. When specifying the metric name via the `--metric dimension` parameter, use the CLI metric name instead. For example, the metric Data path availability would be used by specifying a parameter of `--metric VipAvailability`.

Here's a table of common Load Balancer metrics, the CLI metric name, and recommend aggregation values for queries:

|**Metric**|**CLI metric name**|**Recommended aggregation**|

|-----------------|-----------------|-----------------|

|Data path availability |VipAvailability |Average |

|Health probe status |DipAvailability |Average |

|SYN (synchronize) count |SYNCount |Average |

|SNAT connection count |SnatConnectionCount |Sum |

|Allocated SNAT ports |AllocatedSnatPorts |Average|

|Used SNAT ports |UsedSnatPorts |Average |

|Byte count |ByteCount |Sum |

|Packet count |PacketCount |Sum |

For metric definitions and further details, refer to [Monitoring load balancer data reference](./monitor-load-balancer-reference.md).

## CLI examples for Load Balancer metrics

The [az monitor metrics](/cli/azure/monitor/metrics/) command is used to view Azure resource metrics. To see the metric definitions available for a Standard Load Balancer, you run the [az monitor metrics list-definitions](/cli/azure/monitor/metrics#az-monitor-metrics-list-definitions) command.

```azurecli

# Display available metric definitions for a Standard Load Balancer resource

az monitor metrics list-definitions --resource <resource_id>

```

>[!NOTE]

>In the all the following examples, replace **<resource_id>** with the unique resource id of your Standard Load Balancer.

To retrieve Standard Load Balancer metrics for a resource, you can use the [az monitor metrics list](/cli/azure/monitor/metrics#az-monitor-metrics-list) command. For example, use the `--metric DipAvailability` option to collect the Health Probe Status metric from a Standard Load Balancer.

```azurecli

# List the Health Probe Status metric from a Standard Load Balancer

az monitor metrics list --resource <resource_id> --metric DipAvailability

```

When you run the above command, the output for Health Probe status will be like the following output:

```output

user@Azure:~$ az monitor metrics list --resource <resource_id> --metric DipAvailability

{

"cost": 59,

"interval": "0:01:00",

"namespace": "Microsoft.Network/loadBalancers",

"resourceregion": "eastus2",

"timespan": "2022-06-30T15:22:39Z/2022-06-30T16:22:39Z",

"value": [

{

"displayDescription": "Average Load Balancer health probe status per time duration",

"errorCode": "Success",

"errorMessage": null,

"id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/providers/Microsoft.Insights/metrics/DipAvailability",

"name": {

"localizedValue": "Health Probe Status",

"value": "DipAvailability"

},

"resourceGroup": "myResourceGroup",

"timeseries": [],

"type": "Microsoft.Insights/metrics",

"unit": "Count"

}

]

}

...

```

You can specify the aggregation type for a metric with the `–-aggregation` parameter. For recommended aggregations, see Monitoring load balancer data reference](./monitor-load-balancer-reference.md).

```azurecli

# List the average Health Probe Status metric from a Standard Load Balancer

az monitor metrics list --resource <resource_id> --metric DipAvailability --aggregation Average

```

To specify the interval to metrics, use the `--interval` parameter and specify a value in ##h##m format. The default interval is 1 m.

```azurecli

# List the average List the average Health Probe Status metric from a Standard Load Balancer in 5 minute intervals

az monitor metrics list --resource <resource_id> --metric DipAvailability --aggregation Average --interval 5m

```

By default, az monitor metrics list returns the resource’s aggregate metrics from the last hour. You can query metric data over a period of time using `--start-time` and `--end-time` with the format of date (yyyy-mm-dd) time (hh:mm:ss.xxxxx) timezone (+/-hh:mm). To list the average Health Probe Status aggregated per day from May 5, 2022 and May 10, 2022, use the following command:

```azurecli

# List average Health Probe Status metric aggregated per day from May 5, 2022 and May 10, 2022.

az monitor metrics list --resource <resource_id> --metric DipAvailability --start-time 2022-05-01T00:00:00Z --end-time 2022-05-10T00:00:00Z --interval PT24H --aggregation Average

```

>[!Note]

>Start and end times are represented using a format of yyyy-mm-dd format. For example, every day between May 5, 2022 and May 10, 2022 would be represented as `2022-05-01` and `2022-05-10`.

To split metrics on a dimension, such as “BackendIPAddress”, specify the dimension in the `--filter` flag. Dimensions of a metric are name/value pairs that include more data to describe the metric value. To learn more about which dimensions are supported for each metric, see [Monitoring load balancer data reference](./monitor-load-balancer-reference.md).

```azurecli

# List average Health Probe Status metric and filter for all BackendIPAddress dimensions

az monitor metrics list --resource $res --metric DipAvailability --filter "BackendIPAddress eq '*'" --aggregation Average

```

You can also specify a specific dimension value.

```azurecli

# List average Health Probe Status metric and filter for the 10.1.0.4 BackendIPAddress dimension

az monitor metrics list --resource <resource_id> --metric DipAvailability --filter "BackendIPAddress eq '10.1.0.4'" --aggregation Average

```

In cases where you need to filter on multiple dimension values, specify the `--filter` value using `and` between the values.

```azurecli

# List average Health Probe Status metric and filter for all BackendIPAddress and BackendPort dimensions

az monitor metrics list --resource <resource_id> --metric DipAvailability --filter "BackendIPAddress eq '*' and BackendPort eq '*'" --aggregation Average

```

## Next steps

* [Review the metric definitions to better understand how each is generated](./load-balancer-standard-diagnostics.md#multi-dimensional-metrics)

* [Create Connection Monitors for your Load Balancer](./load-balancer-standard-diagnostics.md)

* [Create your own workbooks](/azure/azure-monitor/visualize/workbooks-overview), you can take inspiration by clicking on the edit button in your detailed metrics dashboard


# Load Balancer Query Metrics Rest Api

# Get Load Balancer usage metrics using the Azure REST API

Collect the number of bytes processed by a [Standard Load Balancer](./load-balancer-overview.md) for an interval of time using the [Azure REST API](/rest/api/azure/).

Complete reference documentation and more samples for the REST API are available in the [Azure Monitor REST reference](/rest/api/monitor).

## Build the request

Use the following GET request to collect the [ByteCount metric](./load-balancer-standard-diagnostics.md#multi-dimensional-metrics) from a Standard Load Balancer.

```http

GET https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/loadBalancers/{loadBalancerName}/providers/microsoft.insights/metrics?api-version=2018-01-01&metricnames=ByteCount&timespan=2018-06-05T03:00:00Z/2018-06-07T03:00:00Z

```

### Request headers

The following headers are required:

|Request header|Description|

|--------------------|-----------------|

|*Content-Type:*|Required. Set to `application/json`.|

|*Authorization:*|Required. Set to a valid `Bearer` [access token](/rest/api/azure/#authorization-code-grant-interactive-clients). |

### URI parameters

| Name | Description |

| :--- | :---------- |

| subscriptionId | The subscription ID that identifies an Azure subscription. If you have multiple subscriptions, see [Working with multiple subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli). |

| resourceGroupName | The name of the resource group that contains the resource. You can obtain this value from the Azure Resource Manager API, CLI, or the portal. |

| loadBalancerName | The name of the Azure Load Balancer. |

| metric names | Comma-separated list of valid  [Load Balancer metrics](./load-balancer-standard-diagnostics.md). |

| api-version | The API version to use for the request.<br /><br /> This document covers api-version `2018-01-01`, included in the above URL.  |

| timespan | The timespan of the query. It's a string with the following format `startDateTime_ISO/endDateTime_ISO`. This optional parameter is set to return a day's worth of data in the example. |

| &nbsp; | &nbsp; |

### Request body

No request body is needed for this operation.

## Handle the response

Status code 200 is returned when the list of metric values is returned successfully. A full list of error codes is available in the [reference documentation](/rest/api/monitor/metrics/list#errorresponse).

## Example response

```json

{

"cost": 0,

"timespan": "2018-06-05T03:00:00Z/2018-06-07T03:00:00Z",

"interval": "PT1M",

"value": [

{

"id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/loadBalancers/{loadBalancerName}/providers/Microsoft.Insights/metrics/ByteCount",

"type": "Microsoft.Insights/metrics",

"name": {

"value": "ByteCount",

"localizedValue": "Byte Count"

},

"unit": "Count",

"timeseries": [

{

"metadatavalues": [],

"data": [

{

"timeStamp": "2018-06-06T17:24:00Z",

"total": 1067921034.0

},

{

"timeStamp": "2018-06-06T17:25:00Z",

"total": 0.0

},

{

"timeStamp": "2018-06-06T17:26:00Z",

"total": 3781344.0

},

]

}

]

}

],

"namespace": "Microsoft.Network/loadBalancers",

"resourceregion": "eastus"

}

```


# Load Balancer Monitor Alert Health Event Logs

# Monitor and alert with LoadBalancerHealthEvent logs

In this article, you learn how to monitor and alert with Azure Load Balancer health event logs. These logs can help you identify and troubleshoot ongoing issues affecting your load balancer resource’s health. The health event logs are provided through the Azure Monitor resource log category *LoadBalancerHealthEvent*.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An Azure Load Balancer resource. To learn how to create a Load Balancer resource, see [Quickstart: Create a public Standard Load Balancer](./quickstart-load-balancer-standard-public-portal.md).

- An Azure Monitor Log Analytics workspace. To learn how to create a Log Analytics workspace, see [Quickstart: Create a Log Analytics workspace](/azure/azure-monitor/logs/quick-create-workspace).

## Configuring diagnostic settings to collect LoadBalancerHealthEvent logs

In this section, you learn configure diagnostic settings to collect LoadBalancerHealthEvent logs and store the logs in a log analytics workspace.

> [!IMPORTANT]

> We recommend sending your logs to a Log Analytics workspace, which will enable you to control access, log data retention and archive settings, and more. To learn more about configuring Log Analytics workspaces, see [Log Analytics workspace overview - Azure Monitor](/azure/azure-monitor/logs/log-analytics-workspace-overview).

1. In the Azure portal, navigate to your load balancer resource.

1. From your load balancer resource's **Overview** page, choose  **Monitoring** > **Diagnostic settings**.

1. Select **+ Add diagnostic setting**.

1. In the **Diagnostic setting** window, select or enter the following settings:

| **Setting** | **Value** |

| --- | --- |

| **Diagnostic setting name** | Enter a name for the diagnostic setting. |

| **Logs** | |

| **Category Groups** | Select **LoadBalancerHealthEvent** or **Load Balancer Health Event**. |

| **Metrics** | Leave unchecked. |

| **Destination details** | Select **Send to Log Analytics workspace**.</br>Select your subscription and your Log Analytics workspace. |

> [!NOTE]

> Selecting **AllLogs** will result in all new log categories for load balancer resources to be automatically collected as they are supported. If you don't want this option, select only the log categories you want to collect. In this case, Load Balancer Health Event logs.

2. Select **Save** and close the **Diagnostic setting** window.

> [!NOTE]

> Once your diagnostic setting has been configured, it can take up to 90 minutes for logs to begin appearing. If there are no health events affecting your load balancer, you may not see any logs.

## Configure a log query

In this section, you learn how to query LoadBalancerHealthEvent logs in a Log Analytics workspace. In this example, you query for the latest *SnatPortExhaustion* health events from the last day, and summarize the events by the load balancer’s *resource IDs* and *frontend IP configurations*.

1. In the Azure portal, navigate to your load balancer resource.

1. From your load balancer resource’s **Overview** page, choose  **Monitoring** > **Logs**.

1. In the **Queries** window, enter **Latest SNAT Port** in the search bar.

1. From the results, select **Load to editor** under **Latest SNAT Port Exhaustion per LB Frontend**.

1. The following code is displayed in the query editor:

```kusto

// Latest Snat Port Exhaustion Per LB Frontend

// List the latest SNAT port exhaustion event per load balancer Frontend IP

ALBHealthEvent

| where TimeGenerated > ago(1d)

| where HealthEventType == "SnatPortExhaustion"

| summarize arg_max(TimeGenerated, *) by LoadBalancerResourceId, FrontendIP

```

1. Select **Run** to execute the query.

1. If you want to modify and save the query, make your query changes and select **Save**>**Save as query**.

1. In the **Save a query** window, enter a name for the query, other optional information, and select **Save**.

## Create alerts based on LoadBalancerHealthEvent logs

In this section, you learn how to create an alert that sends an email whenever a *SnatPortExhaustion* event is logged within the past 5 minutes. You can create alerts based on log queries to be notified immediately when health event logs are generated, indicating potential impact to your load balancer resource.

1.  In the Azure portal, navigate to your load balancer resource.

1.  From your load balancer resource’s **Overview** page, choose  **Monitoring** > **Alerts**.

3.  On the **Alerts** page, select **Create customer alert rule**.

4.  On the **Create an alert rule** page, choose **Custom log search** under **Signal name**.

5.  In the **Logs** window for Log Analytics, enter the following query and select **Run**:

```kusto

ALBHealthEvent

| where TimeGenerated > ago(5m)

| where HealthEventType == "SnatPortExhaustion"

| summarize arg_max(TimeGenerated, *) by LoadBalancerResourceId, FrontendIP

```

1. Select **Continue Editing Alert**

2. On the **Conditions** tab, set the **Threshold value** to 0 under **Alert logic**.

1. Select **Next: Actions>** or the **Actions** tab.

2. On the **Select an action group** page, select **+ Create action group**.

3. On the **Basics** tab, enter the following settings then select **Next: Notifications**:

| **Setting** | **Value** |

| --- | --- |

| **Project details** | |

| **Subscription** | Select your subscription. |

| **Resource group** | Select the resource group that contains your Log Analytics workspace. |

| **Region** | Select the region for the action group. |

| **Instance details** | |

| **Action group name** | Enter a name for the action group. |

| **Display name** | Enter a display name for the action group. |

4. On the **Notifications** tab, enter the following settings:

| **Setting** | **Value** |

| --- | --- |

| **Notification type** | Select **Email/SMS message/Push/Voice**.</br>Enter the email address to receive the alert.</br>Select **Ok**. |

| **Name** | Enter a name for the notification. |

5. Select **Review + create** then **Create** to create the action group.

6. On the **Create an alert rule** page, select **Next: Details** or the **Details** tab.

7. On the **Details** tab, enter the following settings:

8.

| **Setting** | **Value** |

| --- | --- |

| **Severity** | Select the severity level for the alert. |

| **Alert rule name** | Enter a name for the alert rule. |

| **Alert rule description** | Enter a description for the alert rule. |

| **Severity** | Select the severity level for the alert. |

| **Region** | Select the region for the alert rule. |

9.  Select **Review + create** then **Create** to create the alert rule.

## Next steps

In this article, you learned how to collect, analyze, and create alerts using these logs.

For more information about Azure Load Balancer health event logs and health event types, along with how to troubleshoot each health event type, see:

- [Azure Load Balancer health event logs](load-balancer-health-event-logs.md)

- [Support and troubleshooting for Azure Load Balancer](./load-balancer-support-help.md)


# Monitor Load Balancer

# Monitor Azure Load Balancer

[!INCLUDE [horz-monitor-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-intro.md)]

Load Balancer provides other monitoring data through:

- [Health Probes](./load-balancer-custom-probe-overview.md)

- [Resource health status](./load-balancer-standard-diagnostics.md#resource-health-status)

- [REST API](load-balancer-query-metrics-rest-api.md)

[!INCLUDE [horz-monitor-insights](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-insights.md)]

Load Balancer insights provide:

- Functional dependency view

- Metrics dashboard

- Overview tab

- Frontend and Backend Availability tab

- Data Throughput tab

- Flow Distribution

- Connection Monitors

- Metric Definitions

For more information on Load Balancer insights, see [Using Insights to monitor and configure your Azure Load Balancer](./load-balancer-insights.md).

[!INCLUDE [horz-monitor-resource-types](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-resource-types.md)]

For more information about the resource types for Load Balancer, see [Azure Load Balancer monitoring data reference](monitor-load-balancer-reference.md).

[!INCLUDE [horz-monitor-data-storage](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-data-storage.md)]

[!INCLUDE [horz-monitor-platform-metrics](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-platform-metrics.md)]

You can analyze metrics for Load Balancer with metrics from other Azure services using metrics explorer by opening **Metrics** from the **Azure Monitor** menu. See [Analyze metrics with Azure Monitor metrics explorer](/azure/azure-monitor/essentials/analyze-metrics) for details on using this tool.

For a list of available metrics for Load Balancer, see [Azure Load Balancer monitoring data reference](monitor-load-balancer-reference.md#metrics).

[!INCLUDE [horz-monitor-resource-logs](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-resource-logs.md)]

For the available resource log categories, their associated Log Analytics tables, and the log schemas for Load Balancer, see [Azure Load Balancer monitoring data reference](monitor-load-balancer-reference.md#resource-logs).

## Creating a diagnostic setting

Resource logs aren't collected and stored until you create a diagnostic setting and route them to one or more locations. You can create a diagnostic setting with the Azure portal, Azure PowerShell, or the Azure CLI.

To use the Azure portal and for general guidance, see [Create diagnostic setting to collect platform logs and metrics in Azure](/azure/azure-monitor/essentials/diagnostic-settings). To use PowerShell or the Azure CLI, see the following sections.

When you create a diagnostic setting, you specify which categories of logs to collect. The category for Load Balancer is **AllMetrics**.

### PowerShell

Sign in to Azure PowerShell:

```azurepowershell

Connect-AzAccount

```

#### Log analytics workspace

To send resource logs to a Log Analytics workspace, enter these commands. Replace the bracketed values with your values:

```azurepowershell

## Place the load balancer in a variable. ##

$lbpara = @{

ResourceGroupName = <your-resource-group-name>

Name = <your-load-balancer-name>

}

$lb = Get-AzLoadBalancer @lbpara

## Place the workspace in a variable. ##

$wspara = @{

ResourceGroupName = <your-resource-group-name>

Name = <your-log-analytics-workspace-name>

}

$ws = Get-AzOperationalInsightsWorkspace @wspara

## Enable the diagnostic setting. ##

Set-AzDiagnosticSetting `

-ResourceId $lb.id `

-Name <your-diagnostic-setting-name> `

-Enabled $true `

-MetricCategory 'AllMetrics' `

-WorkspaceId $ws.ResourceId

```

#### Storage account

To send resource logs to a storage account, enter these commands. Replace the bracketed values with your values:

```azurepowershell

## Place the load balancer in a variable. ##

$lbpara = @{

ResourceGroupName = <your-resource-group-name>

Name = <your-load-balancer-name>

}

$lb = Get-AzLoadBalancer @lbpara

## Place the storage account in a variable. ##

$storpara = @{

ResourceGroupName = <your-resource-group-name>

Name = <your-storage-account-name>

}

$storage = Get-AzStorageAccount @storpara

## Enable the diagnostic setting. ##

Set-AzDiagnosticSetting `

-ResourceId $lb.id `

-Name <your-diagnostic-setting-name> `

-StorageAccountId $storage.id `

-Enabled $true `

-MetricCategory 'AllMetrics'

```

#### Event hub

To send resource logs to an event hub namespace, enter these commands. Replace the bracketed values with your values:

```azurepowershell

## Place the load balancer in a variable. ##

$lbpara = @{

ResourceGroupName = <your-resource-group-name>

Name = <your-load-balancer-name>

}

$lb = Get-AzLoadBalancer @lbpara

## Place the event hub in a variable. ##

$hubpara = @{

ResourceGroupName = <your-resource-group-name>

Name = <your-event-hub-name>

}

$eventhub = Get-AzEventHubNamespace @hubpara

## Place the event hub authorization rule in a variable. ##

$hubrule = @{

ResourceGroupName = 'myResourceGroup'

Namespace = 'myeventhub8675'

}

$eventhubrule = Get-AzEventHubAuthorizationRule @hubrule

## Enable the diagnostic setting. ##

Set-AzDiagnosticSetting `

-ResourceId $lb.Id `

-Name 'myDiagSetting-event'`

-EventHubName $eventhub.Name `

-EventHubAuthorizationRuleId $eventhubrule.Id `

-Enabled $true `

-MetricCategory 'AllMetrics'

```

### Azure CLI

Sign in to Azure CLI:

```azurecli

az login

```

#### Log analytics workspace

To send resource logs to a Log Analytics workspace, enter these commands. Replace the bracketed values with your values:

```azurecli

lbid=$(az network lb show \

--name <your-load-balancer-name> \

--resource-group <your-resource-group> \

--query id \

--output tsv)

wsid=$(az monitor log-analytics workspace show \

--resource-group <your-resource-group> \

--workspace-name <your-log-analytics-workspace-name> \

--query id \

--output tsv)

az monitor diagnostic-settings create \

--name <your-diagnostic-setting-name> \

--resource $lbid \

--metrics '[{"category": "AllMetrics","enabled": true}]' \

--workspace $wsid

```

#### Storage account

To send resource logs to a storage account, enter these commands. Replace the bracketed values with your values:

```azurecli

lbid=$(az network lb show \

--name <your-load-balancer-name> \

--resource-group <your-resource-group> \

--query id \

--output tsv)

storid=$(az storage account show \

--name <your-storage-account-name> \

--resource-group <your-resource-group> \

--query id \

--output tsv)

az monitor diagnostic-settings create \

--name <your-diagnostic-setting-name> \

--resource $lbid \

--metrics '[{"category": "AllMetrics","enabled": true}]' \

--storage-account $storid

```

#### Event hub

To send resource logs to an event hub namespace, enter these commands. Replace the bracketed values with your values:

```azurecli

lbid=$(az network lb show \

--name <your-load-balancer-name> \

--resource-group <your-resource-group> \

--query id \

--output tsv)

az monitor diagnostic-settings create \

--name myDiagSetting-event \

--resource $lbid \

--metrics '[{"category": "AllMetrics","enabled": true}]' \

--event-hub-rule /subscriptions/<your-subscription-id>/resourceGroups/<your-resource-group>/providers/Microsoft.EventHub/namespaces/<your-event-hub-namespace>/authorizationrules/RootManageSharedAccessKey

```

[!INCLUDE [horz-monitor-activity-log](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-activity-log.md)]

> [!NOTE]

>  Load balancer activity logs will not include updates to NIC-based backend pools. To monitor and alert on updates to the load balancer backend pool for NIC-based backend pools, we recommend collecting logs on the NIC resource-level or at a resource group level instead.

[!INCLUDE [horz-monitor-analyze-data](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-analyze-data.md)]

[!INCLUDE [horz-monitor-external-tools](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-external-tools.md)]

## Analyzing Load Balancer Traffic with VNet flow logs

[Virtual network flow logs](../network-watcher/vnet-flow-logs-overview.md) are a feature of Azure Network Watcher that logs information about IP traffic flowing through a virtual network. Flow data from virtual network flow logs is sent to Azure Storage. From there, you can access the data and export it to any visualization tool, security information and event management (SIEM) solution, or intrusion detection system (IDS).

For general guidance on creating and managing virtual network flow logs, see [Manage virtual network flow logs](../network-watcher/vnet-flow-logs-portal.md). Once you have created your virtual network flow logs, you can access the data on [Log Analytics workspaces](/azure/azure-monitor/logs/log-analytics-overview) where you can also query and filter the data to identify traffic flowing through your Load Balancer. See [Traffic analytics schema and data aggregation](../network-watcher/traffic-analytics-schema.md) for more details on the virtual network flow logs schema.

You can also enable [Traffic Analytics](../network-watcher/traffic-analytics.md) when you are creating your virtual network flow logs which provides insights and visualizations on the flow log data such as traffic distribution, traffic pattern, application ports utilized, and top talkers in your virtual network.

## Log Analytics query for VNet flow logs

To view logs for inbound flows connected to a specific Load Balancer:

```Kusto

NTANetAnalytics

| where DestLoadBalancer == '<Subscription ID>/<Resource Group name>/<Load Balancer name>'

```

1. Use the query above in your Log Analytics workspace and update the string with the valid values for your Load Balancer. To learn more about using Log Analytics, see [Log Analytics tutorial](/azure/azure-monitor/logs/log-analytics-tutorial).

1. To view the source IP of the connection, either the `SrcIp` or `SrcPublicIps` column will be populated. All traffic originating from public non-malicious or Azure service-owned IP addresses will appear in `SrcPublicIps` and all other source IPs will appear in `SrcIP`. If you want more details on the type of traffic, you can use the `FlowType` column to filter for different types of IP addresses involved in the flow. See  [Traffic analytics schema and data aggregation notes](../network-watcher/traffic-analytics-schema.md#notes) for `FlowType` field definitions.

1. Identify the backend pool instances being used in the inbound connection through any of the following columns: `DestIP`, `MacAddress`, `DestVM`, `TargetResourceID`, `DestNic`.

1. Through these logs, you can gather further information about the connections going through your Load Balancer such as port information, protocol, and traffic size through packet and byte count sent from destination and source.

[!INCLUDE [horz-monitor-kusto-queries](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-kusto-queries.md)]

[!INCLUDE [horz-monitor-alerts](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-alerts.md)]

[!INCLUDE [horz-monitor-insights-alerts](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-insights-alerts.md)]

### Load Balancer alert rules

The following table lists some suggested alert rules for Load Balancer. These alerts are just examples. You can set alerts for any metric, log entry, or activity log entry listed in the [Azure Load Balancer monitoring data reference](monitor-load-balancer-reference.md).

| Alert type | Condition | Description |

|:---|:---|:---|

| Load balancing rule unavailable due to unavailable VMs | If data path availability split by Frontend IP address and Frontend Port (all known and future values) is equal to zero, or in a second independent alert, if health probe status is equal to zero, then fire alerts | These alerts help determine if the data path availability for any configured load balancing rules isn't servicing traffic due to all VMs in the associated backend pool being probed down by the configured health probe. Review [Support and troubleshooting for Azure Load Balancer](load-balancer-support-help.md) to investigate the potential root cause. |

| VM availability significantly low | If health probe status split by Backend IP and Backend Port is equal to user defined probed-up percentage of total pool size (that is, 25% are probed up), then fire alert | This alert determines if there are less than needed VMs available to serve traffic |

| Outbound connections to internet endpoint failing | If SNAT Connection Count filtered to Connection State = Failed is greater than zero, then fire alert | This alert fires when SNAT ports are exhausted and VMs are failing to initiate outbound connections. |

| Approaching SNAT exhaustion | If Used SNAT Ports is greater than user defined number, then fire alert | This alert requires a static outbound configuration where the same number of ports are always allocated. It then fires when a percentage of the allocated ports is used. |

[!INCLUDE [horz-monitor-advisor-recommendations](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-advisor-recommendations.md)]

## Related content

- See [Azure Load Balancer monitoring data reference](monitor-load-balancer-reference.md) for a reference of the metrics, logs, and other important values created for Load Balancer.

- See [Monitoring Azure resources with Azure Monitor](/azure/azure-monitor/essentials/monitor-azure-resource) for general details on monitoring Azure resources.


# Monitor Load Balancer Reference

# Azure Load Balancer monitoring data reference

[!INCLUDE [horz-monitor-ref-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-intro.md)]

See [Monitor Azure Load Balancer](monitor-load-balancer.md) for details on the data you can collect for Load Balancer and how to use it.

[!INCLUDE [horz-monitor-ref-metrics-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-intro.md)]

### Supported metrics for Microsoft.Network/loadBalancers

The following table lists the metrics available for the Microsoft.Network/loadBalancers resource type.

[!INCLUDE [horz-monitor-ref-metrics-tableheader](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-tableheader.md)]

|Metric|Name in REST API|Unit|Aggregation|Dimensions|Time Grains|DS Export|

|---|---|---|---|---|---|---|

|**Allocated SNAT Ports**<br><br>Total number of SNAT ports allocated within time period |`AllocatedSnatPorts` |Count |Average |`FrontendIPAddress`, `BackendIPAddress`, `ProtocolType` |PT1M |No|

|**Byte Count**<br><br>Total number of Bytes transmitted within time period |`ByteCount` |Bytes |Total |`FrontendIPAddress`, `FrontendPort`, `Direction`|PT1M |Yes|

|**Health Probe Status**<br><br>Average Load Balancer health probe status per time duration |`DipAvailability` |Count |Average |`ProtocolType`, `BackendPort`, `FrontendIPAddress`, `FrontendPort`, `BackendIPAddress`|PT1M |Yes|

|**Health Probe Status**<br><br>Azure Cross-region Load Balancer backend health and status per time duration |`GlobalBackendAvailability` |Count |Average |`FrontendIPAddress`, `FrontendPort`, `BackendIPAddress`, `ProtocolType` |PT1M |Yes|

|**Packet Count**<br><br>Total number of Packets transmitted within time period |`PacketCount` |Count |Total |`FrontendIPAddress`, `FrontendPort`, `Direction`|PT1M |Yes|

|**SNAT Connection Count**<br><br>Total number of new SNAT connections created within time period |`SnatConnectionCount` |Count |Total |`FrontendIPAddress`, `BackendIPAddress`, `ConnectionState`|PT1M |Yes|

|**SYN Count**<br><br>Total number of SYN Packets transmitted within time period |`SYNCount` |Count |Total |`FrontendIPAddress`, `FrontendPort`, `Direction`|PT1M |Yes|

|**Used SNAT Ports**<br><br>Total number of SNAT ports used within time period |`UsedSnatPorts` |Count |Average |`FrontendIPAddress`, `BackendIPAddress`, `ProtocolType` |PT1M |No|

|**Data Path Availability**<br><br>Average Load Balancer data path availability per time duration |`VipAvailability` |Count |Average |`FrontendIPAddress`, `FrontendPort`|PT1M |Yes|

### Load balancer metrics

This table includes additional information about metrics from the Microsoft.Network/loadBalancers table:

| Metric | Resource type | Description |

|:------ |:------------- |:----------- |

| Allocated SNAT ports | Public load balancer | Standard Load Balancer reports the number of SNAT ports allocated per backend instance. |

| Byte count | Public and internal load balancer | Standard Load Balancer reports the data processed per front end. You might notice that the bytes aren't distributed equally across the backend instances. This behavior is expected as Azure's Load Balancer algorithm is based on flows. |

| Health probe status | Public and internal load balancer | Standard Load Balancer uses a distributed health-probing service that monitors your application endpoint's health according to your configuration settings. This metric provides an aggregate or per-endpoint filtered view of each instance endpoint in the load balancer pool. You can see how Load Balancer views the health of your application, as indicated by your health probe configuration. |

| SNAT connection count | Public load balancer | Standard Load Balancer reports the number of outbound flows that are masqueraded to the Public IP address front end. Source network address translation (SNAT) ports are an exhaustible resource. This metric can give an indication of how heavily your application is relying on SNAT for outbound originated flows. Counters for successful and failed outbound SNAT flows are reported and can be used to troubleshoot and understand the health of your outbound flows. |

| SYN count (synchronize) | Public and internal load balancer | Standard Load Balancer doesn’t terminate Transmission Control Protocol (TCP) connections or interact with TCP or User Data-gram Packet (UDP) flows. Flows and their handshakes are always between the source and the virtual machine instance. To better troubleshoot your TCP protocol scenarios, you can make use of SYN packets counters to understand how many TCP connection attempts are made. The metric reports the number of TCP SYN packets that were received. |

| Used SNAT ports | Public load balancer | Standard Load Balancer reports the number of SNAT ports that are utilized per backend instance. |

| Data path availability | Public and internal load balancer |  Standard Load Balancer continuously exercises the data path from within a region to the load balancer front end, all the way to the SDN stack that supports your virtual machine. As long as healthy instances remain, the measurement follows the same path as your application's load-balanced traffic. The data path that your customer's use is also validated. The measurement is invisible to your application and doesn't interfere with other operations. |

>[!NOTE]

>Data Path Availability metric may take up to 10 minutes to appear in Azure Monitor metrics after a load balancer is created or updated.

### Global load balancer metrics

This table includes additional information about global metrics from the Microsoft.Network/loadBalancers table:

| Metric | Resource type | Description |

|:------ |:------------- |:----------- |

| Health probe status | Public global load balancer | Global load balancer uses a distributed health-probing service that monitors your application endpoint's health according to your configuration settings. This metric provides an aggregate or per-endpoint filtered view of each instance regional load balancer in the global load balancer's backend pool. You can see how global load balancer views the health of your application, as indicated by your health probe configuration. |

| Data path availability | Public global load balancer|  Global load balancer continuously exercises the data path from within a region to the load balancer front end, all the way to the SDN stack that supports your virtual machine. As long as healthy instances remain, the measurement follows the same path as your application's load-balanced traffic. The data path that your customer's use is also validated. The measurement is invisible to your application and doesn't interfere with other operations. |

> [!NOTE]

> Bandwidth-related metrics such as SYN packet, byte count, and packet count doesn't capture any traffic to an internal load balancer by using a UDR, such as from an NVA or firewall.

>

> Max and min aggregations are not available for the SYN count, packet count, SNAT connection count, and byte count metrics.

> Count aggregation is not recommended for Data path availability and health probe status. Use average instead for best represented health data.

[!INCLUDE [horz-monitor-ref-metrics-dimensions-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-dimensions-intro.md)]

[!INCLUDE [horz-monitor-ref-metrics-dimensions](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-dimensions.md)]

| Dimension | Name | Description |

|:----------|:-----|:------------|

| BackendIPAddress  | Backend IP       | The backend IP address of one or more relevant load balancing rules |

| BackendPort       | Backend Port     | The backend port of one or more relevant load balancing rules |

| ConnectionState   | Connection state | The state of SNAT connection. The state can be pending, successful, or failed |

| Direction         | Direction        | The direction traffic is flowing. This value can be inbound or outbound. |

| FrontendIPAddress | Frontend IP      | The frontend IP address of one or more relevant load balancing rules |

| FrontendPort      | Frontend Port    | The frontend port of one or more relevant load balancing rules |

| ProtocolType      | Protocol Type    | The protocol of the relevant load balancing rule. The protocol can be TCP or UDP |

[!INCLUDE [horz-monitor-ref-resource-logs](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-resource-logs.md)]

### Supported resource logs for Microsoft.Network/loadBalancers

[!INCLUDE [<ResourceType/namespace>](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/logs/microsoft-network-loadbalancers-logs-include.md)]

[!INCLUDE [horz-monitor-ref-logs-tables](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-logs-tables.md)]

### Load Balancer Microsoft.Network/LoadBalancers

- [ALBHealthEvent](/azure/azure-monitor/reference/tables/albhealthevent#columns)

- [AzureActivity](/azure/azure-monitor/reference/tables/azureactivity#columns)

[!INCLUDE [horz-monitor-ref-activity-log](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-activity-log.md)]

- [Microsoft.Network resource provider operations](/azure/role-based-access-control/resource-provider-operations#microsoftnetwork)

## Related content

- See [Monitor Azure Load Balancer](monitor-load-balancer.md) for a description of monitoring Load Balancer.

- See [Monitor Azure resources with Azure Monitor](/azure/azure-monitor/essentials/monitor-azure-resource) for details on monitoring Azure resources.


# Load Balancer Insights

# Using Insights to monitor and configure your Azure Load Balancer

Through Azure Monitor for networks, you're provided functional dependency visualizations and preconfigured metrics dashboard for your Load Balancers. These visuals help empower you to make informed design decisions and rapidly localize, diagnose, and resolve any faults.

>[!IMPORTANT]

>The Standard Load Balancer is required to see metrics from the Load Balancer namespace in the pre-configured metrics dashboard. You will still be able to see metrics from the VM, virtual machine scale set, and Connection Monitor namespaces however, we recommend [upgrading to Standard](./upgrade-basic-standard.md) for any production workloads to take advantage of the robust set of Load Balancer metrics.

## Functional dependency view

The functional dependency view enables you to picture even the most complex load balancer setups. With visual feedback on your latest Load Balancer configuration, you can make updates while keeping your configuration in mind.

You can access this view by visiting the Insights page of your Load Balancer resource in Azure.

For Standard Load Balancers, your backend pool resources are color-coded with Health Probe status indicating the current availability of your backend pool to serve traffic. Alongside the above topology you're presented with a time-wise graph of health status, giving a snapshot view of the health of your application.

> [!NOTE]

> If you intentionally probe down a backend pool instance (such as in active/passive scenarios), Insights will show that instance as down with a red status indicator. This is expected behavior and reflects the actual health probe status rather than indicating a fault.

[!INCLUDE [Resource Graph](~/reusable-content/ce-skilling/azure/includes/network-watcher-resource-graph-topology.md)]

## Metrics dashboard

From the Insights page of your Load Balancer, you can select More Detailed Metrics to view a preconfigured [Azure Monitor Workbook](/azure/azure-monitor/visualize/workbooks-overview) containing metrics visuals  relevant to specific aspects of your Load Balancer. This dashboard shows the Load Balancer status and links to relevant documentation at the top of the Overview tab.

You can navigate through the available tabs each of which contain visuals relevant to a specific aspect of your Load Balancer. Explicit guidance for each is available in the dashboard at the bottom of each tab.

The dashboard tabs currently available are:

* Overview

* Frontend and Backend Availability

* Data Throughput

* Flow Distribution

* Connection Monitors

* Metric Definitions

>[!NOTE]

>Displays on the Flow Distribution tab are not supported for load balancer backend pools configured by IP addresses. These are virtual machine-level metrics and can be seen by from the virtual machines / VMSS resources associated with the IP addresses attached instead.

### Overview tab

The Overview tab contains a searchable grid with the overall Data Path Availability and Health Probe Status for each of the Frontend IPs attached to your Load Balancer. These metrics indicate whether the Frontend IP is responsive and the compute instances in your Backend Pool are individually responsive to inbound connections.

You can also view the overall data throughput for each Frontend IP on this page to get a sense of whether you're producing and receive expected traffic levels. The guidance at the bottom of the page directs you to the appropriate tab should you see any irregular values.

### Frontend and Backend Availability tab

The Frontend and Backend Availability tabs show the Data Path Throughput and Health Probe Status metrics presented in a few useful views. The first graph shows the aggregate value so you can determine whether there's an issue. The rest of the graphs show these metrics split by various dimensions so that you can troubleshoot and identify the sources of any inbound availability issues.

A workflow for viewing these graphs is provided at the bottom of the page with common causes for various symptoms.

### Data Throughput tab

The Data Throughput tab allows you to review your inbound and outbound throughput to identify if your traffic patterns are as expected. It shows the inbound and outbound data throughput split by Frontend IP and Frontend Port so that you can identify if how the services you have running are performing individually.

### Flow Distribution

The Flow Distribution Tab helps you visualize and manage the number of flows your backend instances are receiving and producing. It shows the Flow Creation Rate and Flow Count for inbound and outbound traffic as well as the Network Traffic each VM and Virtual Machine Scale Set instance is receiving.

These views can give you feedback on whether your Load Balancer configuration or traffic patterns are leading to imbalanced traffic. For example, if you have session affinity configured and a single client is making a disproportionate number of requests. It will also let you know if you're approaching the [per VM flow limit](../virtual-network/virtual-machine-network-throughput.md#flow-limits-and-active-connections-recommendations) for your machine size.

### Connection Monitors

The Connection Monitors tab shows you the round-trip latency on a global map for all of the [Connection Monitors](../network-watcher/connection-monitor.md)  you've configured. These visuals provide useful information for services with strict latency requirements. To meet your requirements, you may need to add other regional deployments or  move to a [cross-regional load balancing](./cross-region-overview.md) model

### Metric Definitions

The Metric Definitions tab contains all the information shown in the [Multi-dimensional Metrics article](./load-balancer-standard-diagnostics.md#multi-dimensional-metrics).

## Next steps

* Review the dashboard and provide feedback using the below link if there's anything that can be improved

* [Review the metrics documentation to ensure you understand how each metric is calculated](./load-balancer-standard-diagnostics.md#multi-dimensional-metrics)

* [Create Connection Monitors for your Load Balancer](../network-watcher/connection-monitor.md)

* [Create your own workbooks](/azure/azure-monitor/visualize/workbooks-overview), you can take inspiration by clicking on the edit button in your detailed metrics dashboard


# Load Balancer Standard Diagnostics

# Standard load balancer diagnostics with metrics, alerts, and resource health

Azure Load Balancer exposes the following diagnostic capabilities:

* **Multi-dimensional metrics and alerts**: Provides multi-dimensional diagnostic capabilities through [Azure Monitor](/azure/azure-monitor/overview) for Azure Load Balancer configurations. You can monitor, manage, and troubleshoot your standard load balancer resources.

* **Resource health**: The Resource Health status of your load balancer is available in the **Resource health** page under **Monitor**. This automatic check informs you of the current availability of your load balancer resource.

This article provides a quick tour of these capabilities, and it offers ways to use them for a standard load balancer.

## <a name = "MultiDimensionalMetrics"></a>Multi-dimensional metrics

Azure Load Balancer provides multi-dimensional metrics via the Azure Metrics in the Azure portal, and it helps you get real-time diagnostic insights into your load balancer resources. Please note that multi-dimensional metrics are not supported for Basic Load Balancers

The various load balancer configurations provide the following metrics:

| Metric | Resource type | Description | Recommended aggregation |

| --- | --- | --- | --- |

| Data Path Availability | Public and internal load balancer | A load balancer continuously uses the data path from within a region to the load balancer frontend, to the network that supports your VM. As long as healthy instances remain, the measurement follows the same path as your application's load-balanced traffic. The data path in use is validated. The measurement is invisible to your application and doesn’t interfere with other operations. | Average |

| Health Probe Status | Public and internal load balancer | A load balancer uses a distributed health-probing service that monitors your application endpoint's health according to your configuration settings. This metric provides an aggregate or per-endpoint filtered view of each instance endpoint in the load balancer pool. You can see how load balancer views the health of your application, as indicated by your health probe configuration. |  Average |

| SYN Count | Public and internal load balancer |A load balancer doesn’t terminate Transmission Control Protocol (TCP) connections or interact with TCP or User Data-gram Packet (UDP) flows. Flows and their handshakes are always between the source and the VM instance. To better troubleshoot your TCP protocol scenarios, you can make use of SYN packets counters to understand how many TCP connection attempts are made. The metric reports the number of TCP SYN packets that were received.| Sum |

| Source Network Address Translation (SNAT) Connection Count | Public load balancer | A load balancer reports the number of outbound flows that are masqueraded to the Public IP address frontend.  SNAT ports are an exhaustible resource. This metric can give an indication of how heavily your application is relying on SNAT for outbound originated flows. Counters for successful and failed outbound SNAT flows are reported. The counters can be used to troubleshoot and understand the health of your outbound flows.| Sum |

| Allocated SNAT Ports | Public load balancer | A load balancer reports the number of SNAT ports allocated per backend instance | Average. |

| Used SNAT Ports | Public load balancer | A load balancer reports the number of SNAT ports that are utilized per backend instance. | Average |

| Byte Count |  Public and internal load balancer | A load balancer reports the data processed per front end. You may notice that the bytes aren’t distributed equally across the backend instances. This is expected as the Azure Load Balancer algorithm is based on flows | Sum |

| Packet Count |  Public and internal load balancer | A load balancer reports the packets processed per front end.| Sum |

>[!NOTE]

>Bandwidth-related metrics such as SYN packet, byte count, and packet count will not capture any traffic to an internal load balancer via a UDR (eg. from an NVA or firewall).

>

>Max and min aggregations are not available for the SYN count, packet count, SNAT connection count, and byte count metrics.

>Count aggregation is not recommended for Data path availability and health probe status. Use average instead for best represented health data.

>[!NOTE]

>Data Path Availability metric may take up to 10 minutes to appear in Azure Monitor metrics after a load balancer is created or updated.

### View your load balancer metrics in the Azure portal

The Azure portal exposes the load balancer metrics via the Metrics page. This page is available on both the load balancer's resource page for a particular resource and the Azure Monitor page.

>[!NOTE]

> Azure Load Balancer does not send health probes to deallocated virtual machines. When virtual machines are deallocated, the load balancer will stop reporting metrics for that instance. Metrics that are unavailable will appear as a dashed line in Portal, or display an error message indicating that metrics cannot be retrieved.

To view the metrics for your load balancer resources:

1. Go to the metrics page and do either of the following tasks:

* On the load balancer's resource page, select the metric type in the drop-down list.

* On the Azure Monitor page, select the load balancer resource.

2. Set the appropriate metric aggregation type.

3. Optionally, configure the required filtering and grouping.

4. Optionally, configure the time range and aggregation. By default time is displayed in UTC.

>[!NOTE]

>Time aggregation is important when interpreting certain metrics as data is sampled once per minute. If time aggregation is set to five minutes and metric aggregation type Sum is used for metrics such as SNAT allocation, your graph will display five times the total allocated SNAT ports.

>

>Recommendation: When analyzing metric aggregation type Sum and Count, we recommend using a time aggregation value that is greater than one minute.

### Retrieve multi-dimensional metrics programmatically via APIs

For API guidance for retrieving multi-dimensional metric definitions and values, see [Azure Monitoring REST API walkthrough](/azure/azure-monitor/essentials/rest-api-walkthrough#retrieve-metric-definitions). These metrics can be written to a storage account by adding a [diagnostic setting](/azure/azure-monitor/essentials/diagnostic-settings) for the 'All Metrics' category.

### <a name = "DiagnosticScenarios"></a>Common diagnostic scenarios and recommended views

#### Is the data path up and available for my load balancer frontend?

<details><summary>Expand</summary>

The Data Path Availability metric describes the health within the region of the data path to the compute host where your VMs are located. The metric is a reflection of the health of your load balancer, based on your configuration and the Azure infrastructure. You can use the metric to:

- Monitor the external availability of your service.

- Investigate the platform where your service is deployed and determine if it's healthy. Determine if your guest OS or application instance is healthy.

- Isolate whether an event is related to your service or the underlying data plane. Don’t confuse this metric with the Health Probe Status metric.

To get the Data Path Availability for your load balancer resources:

1. Make sure the correct load balancer resource is selected.

1. In the **Metric** drop-down list, select **Data Path Availability**.

1. In the **Aggregation** drop-down list, select **Avg**.

1. Additionally, add a filter on the frontend IP address or frontend port as the dimension with the required frontend IP address or frontend port. Then group them by the selected dimension.

The metric is generated by a probing service within the region that simulates traffic. The probing service periodically generates a packet that matches your deployment's frontend and load balancing rule. The packet then traverse the region from the source to the host of a VM in the backend pool. The load balancer infrastructure performs the same load balancing and translation operations as it does for all other traffic. After the probe arrives on the host, where a VM in the backend pool is located, the host generates a response to the probing service. Your VM doesn’t see this traffic.

Please note that the Data Path Availability metric will only be generated on frontend IP configurations with load balancing rules.

The Data Path Availability metric can be degraded for the following reasons:

- Your deployment has no healthy VMs remaining in the backend pool.

- An infrastructure outage has occurred.

For diagnostic purposes, you can use the [Metric for data path availability together with the health probe status](#vipavailabilityandhealthprobes).

Use **Average** as the aggregation for most scenarios.

</details>

#### Are the backend instances for my load balancer responding to probes?

<details>

<summary>Expand</summary>

The Health Probe Status metric describes the health of your application deployment as configured by you when you configure the health probe of your load balancer. The load balancer uses the status of the health probe to determine where to send new flows. Health probes originate from an Azure infrastructure address and are visible within the guest OS of the VM.

To get the Health Probe Status metric for your load balancer resources:

1. Select the **Health Probe Status** metric with **Avg** aggregation type.

2. Apply a filter on the required frontend IP address or port (or both).

Health probes fail for the following reasons:

- You configure a health probe to a port that isn’t listening or not responding or is using the wrong protocol. If your service is using direct server return or floating IP rules, verify the service is listening on the IP address of the NIC's IP configuration and the loopback that's configured with the frontend IP address.

- Your Network Security Group, the VM's guest OS firewall, or the application layer filters don't allow the health probe traffic.

Use **Average** as the aggregation for most scenarios.

</details>

#### How do I check my outbound connection statistics?

<details>

<summary>Expand</summary>

The SNAT connections metric describes the volume of successful and failed connections for [outbound flows](./load-balancer-outbound-connections.md).

A failed connections volume of greater than zero indicates SNAT port exhaustion. You must investigate further to determine what may be causing these failures. SNAT port exhaustion manifests as a failure to establish an [outbound flow](./load-balancer-outbound-connections.md). Review the article about outbound connections to understand the scenarios and mechanisms at work, and to learn how to mitigate and design to avoid SNAT port exhaustion.

To get SNAT connection statistics:

1. Select **SNAT Connections** metric type and **Sum** as aggregation.

2. Group by **Connection State** for successful and failed SNAT connection counts to be represented by different lines.

</details>

#### How do I check my SNAT port usage and allocation?

<details>

<summary>Expand</summary>

The used SNAT ports metric tracks how many SNAT ports are being consumed to maintain outbound flows. This metric indicates how many unique flows are established between an internet source and a backend VM or virtual machine scale set that is behind a load balancer and doesn’t have a public IP address. By comparing the number of SNAT ports you’re using with the Allocated SNAT Ports metric, you can determine if your service is experiencing or at risk of SNAT exhaustion and resulting outbound flow failure.

If your metrics indicate risk of [outbound flow](./load-balancer-outbound-connections.md) failure, reference the article and take steps to mitigate this to ensure service health.

To view SNAT port usage and allocation:

1. Set the time aggregation of the graph to 1 minute to ensure desired data is displayed.

2. Select **Used SNAT Ports** and/or **Allocated SNAT Ports** as the metric type and **Average** as the aggregation.

* By default, these metrics are the average number of SNAT ports allocated to or used by each backend VM or virtual machine scale set. They correspond to all frontend public IPs mapped to the load balancer, aggregated over TCP and UDP.

* To view total SNAT ports used by or allocated for the load balancer use metric aggregation **Sum**.

3. Filter to a specific **Protocol Type**, a set of **Backend IPs**, and/or **Frontend IPs**.

4. To monitor health per backend or frontend instance, apply splitting.

* Note splitting only allows for a single metric to be displayed at a time.

5. For example, to monitor SNAT usage for TCP flows per machine, aggregate by **Average**, split by **Backend IPs** and filter by **Protocol Type**.

</details>

#### How do I check inbound/outbound connection attempts for my service?

<details>

<summary>Expand</summary>

A SYN packets metric describes the volume of TCP SYN packets, which have arrived or were sent for outbound flows that are associated with a specific front end. You can use this metric to understand TCP connection attempts to your service.

For more information on outbound connections, see [Source Network Address Translation (SNAT) for outbound connections](load-balancer-outbound-connections.md)

Use **Sum** as the aggregation for most scenarios.

</details>

#### How do I check my network bandwidth consumption?

<details>

<summary>Expand</summary>

The bytes and packet counters metric describes the volume of bytes and packets that are sent or received by your service on a per-frontend basis.

Use **Sum** as the aggregation for most scenarios.

To get byte or packet count statistics:

1. Select the **Bytes Count** and/or **Packet Count** metric type, with **Sum** as the aggregation.

2. Do either of the following:

* Apply a filter on a specific frontend IP, frontend port, backend IP, or backend port.

* Get overall statistics for your load balancer resource without any filtering.

</details>

#### <a name = "vipavailabilityandhealthprobes"></a>How do I diagnose my load balancer deployment?

<details>

<summary>Expand</summary>

By using a combination of the data path availability and health probe status metrics on a single chart, you can identify where to look for the problem and resolve the problem. You can gain assurance that Azure is working correctly and use this knowledge to conclusively determine that the configuration or application is the root cause.

You can use health probe metrics to understand how Azure views the health of your deployment as per the configuration you’ve provided. Looking at health probes is always a great first step in monitoring or determining a cause.

You can take it a step further and use data path availability metric to gain insight into how Azure views the health of the underlying data plane that's responsible for your specific deployment. When you combine both metrics, you can isolate where the fault might be, as illustrated in this example:

*Figure: Combining data path availability and health probe status metrics*

The chart displays the following information:

- The infrastructure hosting your VMs was unavailable and at 0 percent at the beginning of the chart. Later, the infrastructure was healthy and the VMs were reachable, and more than one VM was placed in the back end. This information is indicated by the blue trace for data path availability, which was later at 100 percent.

- The health probe status, indicated by the purple trace, is at 0 percent at the beginning of the chart. The circled area in green highlights where the health probe status became healthy, and at which point the customer's deployment was able to accept new flows.

The chart allows customers to troubleshoot the deployment on their own without having to guess or ask support whether other issues are occurring. The service was unavailable because health probes were

failing due to either a misconfiguration or a failed application.

</details>

## Configure alerts for multi-dimensional metrics

Azure Load Balancer supports easily configurable alerts for multi-dimensional metrics. Configure custom thresholds for specific metrics to trigger alerts with varying levels of severity to empower a no touch resource monitoring experience.

To configure alerts:

1. Go to the alert page for the load balancer

2. Create new alert rule

1.  Configure alert condition (Note: to avoid noisy alerts, we recommend configuring alerts with the Aggregation type set to Average, looking back on a five-minute window of data, and with a threshold of 95%)

2.  (Optional) Add action group for automated repair

3.  Assign alert severity, name, and description that enables intuitive reaction

### Inbound availability alerting

>[!NOTE]

> If your load balancer's backend pools are empty, the load balancer will not have any valid data paths to test. As a result, the data path availability metric will not be available, and any configured Azure Alerts on the data path availability metric will not trigger.

To alert for inbound availability,  you can create two separate alerts using the data path availability and health probe status metrics. Customers may have different scenarios that require specific alerting logic, but the below examples are helpful for most configurations.

Using data path availability, you can fire alerts whenever a specific load-balancing rule becomes unavailable. You can configure this alert by setting an alert condition for the data path availability and splitting by all current values and future values for both frontend port and frontend IP address. Setting the alert logic to be less than or equal to 0 will cause this alert to be fired whenever any load-balancing rule becomes unresponsive. Set the aggregation granularity and frequency of evaluation according to your desired evaluation.

With health probe status, you can alert when a given backend instance fails to respond to the health probe for a significant amount of time. Set up your alert condition to use the health probe status metric and split by backend IP address and backend port, using the **Average** aggregation type. This ensures that you can alert separately for each individual backend instance’s ability to serve traffic on a specific port.

### Outbound availability alerting

For outbound availability, you can configure two separate alerts using the SNAT connection count and used SNAT port metrics.

To detect outbound connection failures, configure an alert using SNAT connection count and filtering to **Connection State = Failed**. Use the **Total** aggregation. Then, you can split this by backend IP address set to all current and future values to alert separately for each backend instance experiencing failed connections. Set the threshold to be greater than zero or a higher number if you expect to see some outbound connection failures.

With used SNAT ports, you can alert on a higher risk of SNAT exhaustion and outbound connection failure. Ensure you’re splitting by backend IP address and protocol when using this alert. Use the **Average** aggregation. Set the threshold to be greater than a percentage of the number of ports you’ve allocated per instance that you determine is unsafe. For example, configure a low severity alert when a backend instance uses 75% of its allocated ports. Configure a high severity alert when it uses 90% or 100% of its allocated ports.

## <a name = "ResourceHealth"></a>Resource health status

Health status for the standard load balancer resources is exposed via the existing **Resource health** under **Monitor > Service health**. It’s evaluated every **two minutes** by measuring data path availability that determines whether your frontend load-balancing endpoints are available.

| Resource health status | Description |

| --- | --- |

| Available | Your standard load balancer resource is healthy and available. |

| Degraded | Your standard load balancer has platform or user initiated events impacting performance. The metric for data path availability has reported less than 90% but greater than 25% health for at least two minutes. With this status, you experience moderate to severe performance effect. See [Support and troubleshooting for Azure Load Balancer](./load-balancer-support-help.md) to determine whether there are user initiated events impacting your availability.

| Unavailable | Your standard load balancer resource isn’t healthy. The metric for data path availability has reported less the 25% health for at least two minutes. With this status, you experience significant performance effect or lack of availability for inbound connectivity. There may be user or platform events causing unavailability. See [Support and troubleshooting for Azure Load Balancer](./load-balancer-support-help.md) to determine whether there are user initiated events impacting your availability. |

| Unknown | Health status for your load balancer resource hasn’t been updated or hasn’t received information for data path availability for the last 10 minutes. This state should be transient and will reflect correct status as soon as data is received. |

To view the health of your public standard load balancer resources:

1. Select  **Monitor** > **Service health**.

2. Select **Resource health**, and then make sure that **Subscription ID** and **Resource type = load balancer** are selected.

3. In the list, select the load balancer resource to view its historical health status.

A generic description of a resource health status is available in the [resource health documentation](/azure/service-health/resource-health-overview).

### Resource health alerts

Azure Resource Health alerts can notify you in near real-time when the health state of your Load balancer resource changes. It's recommended that you set resource health alerts to notify you when your Load balancer resource is in a **Degraded** or **Unavailable** state.

When you create Azure resource health alerts for Load balancer, Azure sends resource health notifications to your Azure subscription. You can create and customize alerts based on:

* The subscription affected

* The resource group affected

* The resource type affected (Load balancer)

* The specific resource (any Load balancer resource you choose to set up an alert for)

* The event status of the Load balancer resource affected

* The current status of the Load balancer resource affected

* The previous status of the Load balancer resource affected

* The reason type of the Load balancer resource affected

You can also configure who the alert should be sent to:

* A new action group (that can be used for future alerts)

* An existing action group

For more information on how to set up these resource health alerts, see:

* [Resource health alerts using Azure portal](/azure/service-health/resource-health-alert-monitor-guide#create-a-resource-health-alert-rule-in-the-azure-portal)

* [Resource health alerts using Resource Manager templates](/azure/service-health/resource-health-alert-arm-template-guide)

## Next steps

- Learn about [Network Analytics](/previous-versions/azure/azure-monitor/insights/azure-networking-analytics).

- Learn about using [Insights](./load-balancer-insights.md) to view these metrics preconfigured for your load balancer.

- Learn more about [Standard load balancer](./load-balancer-overview.md).


# Load Balancer Health Event Logs

# Azure Load Balancer health event logs

Azure Load Balancer supports health event logs to help you identify and troubleshoot ongoing issues affecting your load balancer resource’s health. These events are provided through the Azure Monitor resource log category LoadBalancerHealthEvent.

These logs are supported for Standard (regional and global tier) and Gateway Load Balancers.

## Severity definitions

Each health event type has an associated severity to indicate the level of expected impact. This property can help with filtering logs and creating more individualized alerts based on the urgency of the issue.

| **Severity** | **Description** |

| --- | --- |

| **Critical** | The load balancer resource needs immediate attention. The functionality of the load balancer is affected. This impact can cause issues such as failed connections, unsuccessful CRUD (create, read, update, delete) operations, or misconfigured load balancer components. |

| **Warning** | The load balancer resource needs to be monitored or reviewed. The functionality of the load balancer can be affected in certain scenarios or is operating in a partially degraded state. |

## Health event types and publishing frequency

Health events can be detected in various ways – some events are generated through actively checking the state of the load balancer, while others can be generated when an explicit condition being met. Each event has the possibility of being published every minute, if the event occurred during the detection window.

Once a health event is published, there's an extended window of time when the event isn't republished. This window of time prevents publication of excessive logs when there's a persistent issue. Following this redetection interval, the health event is republished if the issue still persists.

Each event log is published with a timestamp that indicates the time that Azure Load Balancer detects the event at the platform level. There can be a delay between the detection and the event publishing by Azure Monitor.

| **Status** | **LoadBalancerHealthEventType** | **Severity** | **Description** | **Detection window** | **Re-detection interval** | **Supported properties** |

| --- | --- | --- | --- | --- | --- | --- |

| **GA** | *DataPathAvailabilityWarning* | Warning | This event is published per affected Load Balancer frontend IP, when the Data Path Availability metric of the frontend IP is less than 90% due to platform issues | 1 minute | 5 minutes | Frontend IP address, List of frontend ports associated with affected load balancing rules |

| **GA** | *DataPathAvailabilityCritical* | Critical | This event is published per affected Load Balancer frontend IP, when the Data Path Availability metric of the frontend IP is less than 25% due to platform issues | 1 minute | 5 minutes | Frontend IP address, List of frontend ports associated with affected load balancing rules |

| **GA** | *NoHealthyBackends* | Critical | This event is published per Load Balancer frontend IP, when an associated backend pool has no backend instances responding to the configured health probes. As a result, the load balancer has no healthy backends to distribute traffic to. | On-demand | 60 minutes | Frontend IP address, Pairwise list of protocol and frontend ports associated with affected load balancing rules |

| **GA** | *HighSnatPortUsage* | Warning | This event is published on a per backend instance-level, when a backend instance utilizes more than 75% of its allocated ports from a single frontend IP. | On-demand | 5 minutes | Backend IP address, Frontend IP address |

| **GA** | *SnatPortExhaustion* | Critical | This event is published on a per backend instance-level. Publication occurs when a backend instance exhausts all allocated ports and fails any further outbound connections. This event continues until ports are released or more ports are allocated. | On-demand | 5 minutes | Backend IP address, Frontend IP address |

| **GA** | *ApproachingMaxRulesPerNicLimit* | Warning | This event is published per affected Load Balancer frontend IP, when one or more associated backend instances has more than 300 load balancing and inbound NAT rules configured in total. | 24 hours | 24 hours | Frontend IP address |

| **GA** | *GatewayLoadBalancerNoHealthyBackends* | Critical | This event is published per affected Load Balancer frontend IP, when there is a chained Gateway Load Balancer that is unreachable due to having no backend instances responding to its health probes. | On-demand | 60 minutes | Frontend IP address |

| **GA** | *NetworkPlatformThrottlingActive* | Critical | This event is published per Load Balancer frontend IP, when the platform bandwidth and/or throughput limits have been reached due to traffic destined to this frontend IP. | On-demand | 60 minutes | Frontend IP address |

For more information on the properties published with each health event log, refer to the Azure Log Analytics reference documentation for the log table [*ALBHealthEvent*](/azure/azure-monitor/reference/tables/albhealthevent).

## Next steps

In this article, you learned about Azure Load Balancer health event logs and health event types.

For more information about how to collect, analyze, and create alerts using these logs, along with troubleshooting each health event type, see:

- [Learn to monitor and alert with Azure Load Balancer health event logs](load-balancer-monitor-alert-health-event-logs.md).

- [Support and troubleshooting for Azure Load Balancer](load-balancer-support-help.md)


# Load Balancer Manage Health Status

# Manage Azure Load Balancer Health Status

Health status is an Azure Load Balancer feature that gives detailed health information about the backend instances in your Azure Load Balancer backend pool. Linked to your load balancing rule, this status provides insights into the health state and reasoning of these backend instances.

## State of backend instances

Health status exposes the state of your backend instances. There are two state values:

| **State** | **Description** |

|-----------|-----------------|

| Up | This state value represents a healthy backend instance. |

| Down | This state value represents an unhealthy backend instance. |

## Reason codes

Health status also exposes reason codes, categorized into User Triggered Reason Codes and Platform Triggered Reason Codes. These codes help you understand the precise reasons for the health probe state of your backend instances and why they're being probed Up or Down.

### User Triggered Reason Codes

User triggered reason codes are triggered based on how you configured your Load Balancer; these can be addressed by you, the user. The following tables describe the user-triggered reason codes along with the portal displayed reason for success and failed reason codes.

#### Success reason codes

The following table describes the success reason codes where the backend state is equal to **Up**:

| **Reason Code** | **Portal displayed reason** | **Description** |

|-------------|-------------------------|-------------|

| **Up_Probe_Success** | The backend instance is responding to health probe successfully. | Your backend instance is responding to the health probe successfully. |

| **Up_Probe_AllDownIsUp** | The backend instance is considered healthy due to enablement of *NoHealthyBackendsBehavior*. | Health probe state of the backend instance is ignored because *NoHealthyBackendsBehavior* is enabled. The backend instance is considered healthy and can receive traffic. |

| **Up_Probe_ApproachingUnhealthyThreshold** | Health probe is approaching an unhealthy threshold but backend instance remains healthy based on last response. | The most recent probe has failed to respond but the backend instance remains healthy enough based on earlier responses. |

| **Up_Admin**| The backend instance is healthy due to Admin State set to *Up*. | Health probe state of the backend instance is ignored because the Admin State is set to *UP*. The backend instance is considered healthy and can receive traffic. |

#### Failure reason codes

The following table describes the failure reason codes where the backend state is equal to **Down**:

| **Reason Code** | **Portal displayed reason** | **Description** |

|-------------|-------------------------|-------------|

| **Down_Probe_ApproachingHealthyThreshold** | Health probe is approaching a healthy threshold but backend instance remains unhealthy based on last response. | The most recent probe outcome is positive, but it doesn't meet the required number of responses in the healthy threshold, so the backend instance remains unhealthy. |

| **Down_Probe_HttpStatusCodeError** | A non-200 HTTP status code received; meaning there's an issue with the application listening on the port. | Your backend instance is returning a non-200 HTTP status code indicating an issue with the application listening on the port. |

| **Down_Probe_HttpEndpointUnreachable** | HTTP endpoint unreachable; meaning either an NSG rule blocking port or unhealthy app listening on port. | The health probe was able to establish a TCP handshake with your backend instance but the HTTP session was rejected which indicates two possibilities: An NSG rule blocking the port or no healthy application listening on the port. |

| **Down_Probe_TcpProbeTimeout** | TCP probe timeout; meaning either unhealthy backend instance, blocked health probe port, or unhealthy app listening on port. | Your backend instance has sent back no TCP response within the probe interval. This indicates three possibilities: An unhealthy Backend Instance, blocked health probe port, or unhealthy application listening on the port. |

| **Down_Probe_NoHealthyBackend** | No healthy backend instances behind the regional load balancer. | Your regional load balancer that is associated with a Global Load Balancer has no healthy backend instances behind it. |

| **Down_Admin** | The backend instance is unhealthy due to *Admin State* set to *Down*. | Health probe state of the backend instance is ignored because the *Admin State* is set to *Down*. The backend instance is considered unhealthy and can't receive new traffic. |

| **Down_Probe_HttpNoResponse** | Application isn't returning a response. | The health probe was able to establish an HTTP session but the application isn't returning a response. This indicates an unhealthy application listening on the port. |

> [!NOTE]

> In rare cases, **NA** will show as a reason code. This code is shown when the health probe has not probed your backend instance yet so there is no reason code to display.

### Platform Triggered reason codes

Platform triggered reason codes are triggered based on the Azure Load Balancer’s platform; these codes can't be addressed by you, the user. The following table below describes each reason code:

| **Reason Code** | **Portal displayed reason** | **Description** |

|-------------|-------------------------|-------------|

| **Up_Platform** | The backend instance is responding to the health probe successfully, but there may be an infrastructure related issue. The Azure service team is alerted and will resolve the issue.| The backend instance is responding to the health probe successfully, but there can be an infrastructure related issue. The Azure service team is alerted and will resolve the issue. |

| **Down_Platform** | The backend instance is unhealthy due to an infrastructure related issue. The Azure service team is alerted and will resolve the issue. | The backend instance is unhealthy due to an infrastructure related issue. The Azure service team is alerted and will resolve the issue. |

## How to retrieve health status

Health status can be retrieved on a per load balancing rule basis. This is supported via Azure port and REST API.

# [Azure portal](#tab/azure-portal)

1. Sign in to the Azure portal.

2. In the search bar, enter **Load Balancers** and select **Load Balancers** from the search results.

3. On the **Load Balancers** page, select your load balancer from the list.

4. In your load balancer's **Settings** section, select **Load balancing rules**.

5. In the **Load balancing rules** page, select **View details** under the **Health status** column for the rule you want to view.

6. Review the health status of your backend instances in the **Load balancing rule health status** window.

7. To retrieve the latest health status, select **Refresh**.

> [!IMPORTANT]

> The Load balancing rule health status window may take a few minutes to load the health status of your backend instances.

1. Select **Close** to exit the **Load balancing rule health status** window.

# [REST API](#tab/rest-api)

To retrieve the health status information via REST API, you need to do a two request process.

> [!NOTE]

> Using the REST API method requires that you have a **Bearer access token** for authorization. For assistance retrieving the access token, see [Get-AzAccessToken](/powershell/module/az.accounts/get-azaccesstoken) for details.

1. Use the following POST request to obtain the Location URI from the Response Headers.

```rest

POST https://management.azure.com/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/loadBalancers/<loadBalancerName>/loadBalancingRules/<loadBalancingRulesName>/health?api-version=2024-03-01&preserve-view=true

Authorization: Bearer <access token>

```

1. Copy the Location URI from the Response Headers. Location URI should follow this schema.

```rest

https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.Network/locations/<locationName>/operationResults/<operationResultsId>?api-version=2024-03-01&preserve-view=true

```

1. Use the copied Location URI to make a GET request.

```rest

GET https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.Network/locations/<locationName>/operationResults/<operationResultsId>?api-version=2024-03-01&preserve-view=true

Authorization: Bearer <access token>

```

1. A status code of 200 is returned and the health status information is displayed in the response body similar to this example response:

```JSON

{

"up": 2,

"down": 0,

"loadBalancerBackendAddresses": [

{

"ipAddress": "10.0.2.5",

"networkInterfaceIPConfigurationId": "/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/networkInterfaces/<networkInterfaceName>/ipConfigurations/<ipConfigurationName>",

"state": "Up",

"reason": "Up_Admin"

},

{

"ipAddress": "10.0.2.4",

"networkInterfaceIPConfigurationId": "/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/networkInterfaces/<networkInterfaceName>/ipConfigurations/<ipConfigurationName>",

"state": "Up",

"reason": "Up_Probe_Success"

}

]

}

```

## Design considerations

When using the health status feature, consider the following design considerations:

- If the virtual machine instance in the backend pool is turned off, health status returns empty values since the health status isn't retrievable.

- If you're using a global load balancer, health status displays the reason as *Down_Platform** when a regional load balancer’s backend pool is an IP-based backend address that isn't associated with a virtual machine instance.

- For retrieving health status, the Azure portal and REST API methods are the only supported methods.

## Limitations

When using the health status feature, consider the following limitations:

- Health status isn’t supported for nonprobed load balancing rules.

- Health status isn’t supported for Gateway Load Balancer.

## Next steps

> [!div class="nextstepaction"]

> [Create a public load balancer with an IP-based backend using the Azure portal](tutorial-load-balancer-ip-backend-portal.md)


# Load Balancer Support Help

# Support and troubleshooting for Azure Load Balancer

Here are suggestions for where you can get help when developing your Azure Load Balancer solutions.

## Self help troubleshooting

Various articles explain how to determine, diagnose, and fix issues that you might encounter when using Azure Load Balancer. Use these resources to troubleshoot deployment failures, connection issues, health probe problems, and performance issues.

For a full list of self help troubleshooting content, see [Azure Load Balancer troubleshooting documentation](/troubleshoot/azure/load-balancer/welcome-azure-load-balancer).

## Post a question on Microsoft Q&A

For quick and reliable answers on your technical product questions from Microsoft Engineers, Azure Most Valuable Professionals (MVPs), or our expert community, engage with us on [Microsoft Q&A](/answers/products/azure), Azure's preferred destination for community support.

If you can't find an answer to your problem using search, submit a new question to Microsoft Q&A. Use the following tag when asking your question:

| Area | Tag |

| --- | --- |

| [Azure Load Balancer](./load-balancer-overview.md) | [azure-load-balancer](/answers/tags/azure-load-balancer) |

## Create an Azure support request

Explore the range of [Azure support options and choose the plan](https://azure.microsoft.com/support/plans) that best fits, whether you're a developer just starting your cloud journey or a large organization deploying business-critical, strategic applications. Azure customers can create and manage support requests in the Azure portal.

- If you already have an Azure Support Plan, [open a support request here](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest).

- To sign up for a new Azure Support Plan, [compare support plans](https://azure.microsoft.com/support/plans/) and select the plan that works for you.

## Create a GitHub issue

If you need help with the language and tools used to develop and manage Azure Load Balancer, open an issue in its repository on GitHub.

| Library | GitHub issues URL|

| --- | --- |

| Azure PowerShell | https://github.com/Azure/azure-powershell/issues |

| Azure CLI | https://github.com/Azure/azure-cli/issues |

| Azure REST API | https://github.com/Azure/azure-rest-api-specs/issues |

| Azure SDK for Java | https://github.com/Azure/azure-sdk-for-java/issues |

| Azure SDK for Python | https://github.com/Azure/azure-sdk-for-python/issues |

| Azure SDK for .NET | https://github.com/Azure/azure-sdk-for-net/issues |

| Azure SDK for JavaScript | https://github.com/Azure/azure-sdk-for-js/issues |

| Terraform | https://github.com/hashicorp/terraform-provider-azurerm/issues |

| Bicep | https://github.com/Azure/bicep/issues |

## Stay informed of updates and new releases

Learn about important product updates, roadmap, and announcements in [Azure Updates](https://azure.microsoft.com/updates/?product=load-balancer).

News and information about Azure Load Balancer is shared at the [Azure Networking blog](https://techcommunity.microsoft.com/category/azure/blog/azurenetworkingblog).

## Next steps

Learn more about [Azure Load Balancer](./index.yml).


# Tutorial Protect Load Balancer Ddos

# Tutorial: Protect your public load balancer with Azure DDoS Protection

Azure DDoS Protection enables enhanced DDoS mitigation capabilities such as adaptive tuning, attack alert notifications, and monitoring to protect your public load balancers from large scale DDoS attacks.

> [!IMPORTANT]

> Azure DDoS Protection incurs a cost when you use the Network Protection SKU. Overages charges only apply if more than 100 public IPs are protected in the tenant. Ensure you delete the resources in this tutorial if you aren't using the resources in the future. For information about pricing, see [Azure DDoS Protection Pricing]( https://azure.microsoft.com/pricing/details/ddos-protection/). For more information about Azure DDoS protection, see [What is Azure DDoS Protection?](../ddos-protection/ddos-protection-overview.md)

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a DDoS Protection plan.

> * Create a virtual network with DDoS Protection and Bastion service enabled.

> * Create a standard SKU public load balancer with frontend IP, health probe, backend configuration, and load-balancing rule.

> * Create a NAT gateway for outbound internet access for the backend pool.

> * Create virtual machine, then install and configure IIS on the VMs to demonstrate the port forwarding and load-balancing rules.

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

- An Azure account with an active subscription.

## Create a DDoS protection plan

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal, enter **DDoS protection**. Select **DDoS protection plans** in the search results and then select **+ Create**.

1. In the **Basics** tab of **Create a DDoS protection plan** page, enter or select the following information:

| Setting | Value |

|--|--|

| **Project details** |   |

| Subscription | Select your Azure subscription. |

| Resource group | Select **Create new**.  </br> Enter **TutorLoadBalancer-rg**. </br> Select **OK**. |

| **Instance details** |   |

| Name | Enter **myDDoSProtectionPlan**. |

| Region | Select **(US) East US**. |

1. Select **Review + create** and then select **Create** to deploy the DDoS protection plan.

## Create the virtual network

In this section, you'll create a virtual network, subnet, Azure Bastion host, and associate the DDoS Protection plan. The virtual network and subnet contains the load balancer and virtual machines. The bastion host is used to securely manage the virtual machines and install IIS to test the load balancer. The DDoS Protection plan will protect all public IP resources in the virtual network.

> [!IMPORTANT]

> [!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

>

1. In the search box at the top of the portal, enter **Virtual network**. Select **Virtual Networks** in the search results.

2. In **Virtual networks**, select **+ Create**.

3. In **Create virtual network**, enter or select the following information in the **Basics** tab:

| **Setting** | **Value** |

|---|---|

| **Project Details** |  |

| Subscription | Select your Azure subscription. |

| Resource Group | Select **TutorLoadBalancer-rg** |

| **Instance details** |  |

| Name | Enter **myVNet** |

| Region | Select **East US** |

4. Select the **IP Addresses** tab or select **Next: IP Addresses** at the bottom of the page.

5. In the **IP Addresses** tab, enter this information:

| Setting            | Value                      |

|--------------------|----------------------------|

| IPv4 address space | Enter **10.1.0.0/16** |

6. Under **Subnet name**, select the word **default**. If a subnet isn't present, select **+ Add subnet**.

7. In **Edit subnet**, enter this information:

| Setting            | Value                      |

|--------------------|----------------------------|

| Subnet name | Enter **myBackendSubnet** |

| Subnet address range | Enter **10.1.0.0/24** |

8. Select **Save** or **Add**.

9. Select the **Security** tab.

10. Under **BastionHost**, select **Enable**. Enter this information:

| Setting            | Value                      |

|--------------------|----------------------------|

| Bastion name | Enter **myBastionHost** |

| AzureBastionSubnet address space | Enter **10.1.1.0/26** |

| Public IP Address | Select **Create new**. </br> For **Name**, enter **myBastionIP**. </br> Select **OK**. |

11. Under **DDoS Network Protection**, select **Enable**. Then from the drop-down menu, select **myDDoSProtectionPlan**.

12. Select the **Review + create** tab or select the **Review + create** button.

13. Select **Create**.

> [!NOTE]

> The virtual network and subnet are created immediately. The Bastion host creation is submitted as a job and will complete within 10 minutes. You can proceed to the next steps while the Bastion host is created.

## Create load balancer

In this section, you'll create a zone redundant load balancer that load balances virtual machines. With zone-redundancy, one or more availability zones can fail and the data path survives as long as one zone in the region remains healthy.

During the creation of the load balancer, you'll configure:

* Frontend IP address

* Backend pool

* Inbound load-balancing rules

* Health probe

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

2. In the **Load balancer** page, select **+ Create**.

3. In the **Basics** tab of the **Create load balancer** page, enter or select the following information:

| Setting                 | Value                                              |

| ---                     | ---                                                |

| **Project details** |   |

| Subscription               | Select your subscription.    |

| Resource group         | Select **TutorLoadBalancer-rg**. |

| **Instance details** |   |

| Name                   | Enter **myLoadBalancer**                                   |

| Region         | Select **East US**.                                        |

| SKU           | Leave the default **Standard**. |

| Type          | Select **Public**.                                        |

| Tier          | Leave the default **Regional**. |

4. Select **Next: Frontend IP configuration** at the bottom of the page.

5. In **Frontend IP configuration**, select **+ Add a frontend IP configuration**.

6. Enter **myFrontend** in **Name**.

7. Select **IPv4** for the **IP version**.

8. Select **IP address** for the **IP type**.

> [!NOTE]

> For more information on IP prefixes, see [Azure Public IP address prefix](../virtual-network/ip-services/public-ip-address-prefix.md).

9. Select **Create new** in **Public IP address**.

10. In **Add a public IP address**, enter **myPublicIP** for **Name**.

11. Select **Zone-redundant** in **Availability zone**.

> [!NOTE]

> In regions with [Availability Zones](/azure/reliability/availability-zones-overview?toc=%2fazure%2fvirtual-network%2ftoc.json), you can select zone-redundant (default option) or a specific zone. The choice depends on your specific domain failure requirements. In regions without Availability Zones, this field won't appear. </br> For more information on availability zones, see [Availability zones overview](/azure/reliability/availability-zones-overview).

12. Leave the default of **Microsoft Network** for **Routing preference**.

13. Select **OK**.

14. Select **Add**.

15. Select **Next: Backend pools** at the bottom of the page.

16. In the **Backend pools** tab, select **+ Add a backend pool**.

17. Enter **myBackendPool** for **Name** in **Add backend pool**.

18. Select **myVNet** in **Virtual network**.

19. Select **IP Address** for **Backend Pool Configuration**.

21. Select **Save**.

22. Select **Next: Inbound rules** at the bottom of the page.

23. Under **Load balancing rule** in the **Inbound rules** tab, select **+ Add a load balancing rule**.

24. In **Add load balancing rule**, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| Name | Enter **myHTTPRule** |

| IP Version | Select **IPv4** or **IPv6** depending on your requirements. |

| Frontend IP address | Select **myFrontend (To be created)**. |

| Backend pool | Select **myBackendPool**. |

| Protocol | Select **TCP**. |

| Port | Enter **80**. |

| Backend port | Enter **80**. |

| Health probe | Select **Create new**. </br> In **Name**, enter **myHealthProbe**. </br> Select **TCP** in **Protocol**. </br> Leave the rest of the defaults, and select **OK**. |

| Session persistence | Select **None**. |

| Idle timeout (minutes) | Enter or select **15**. |

| TCP reset | Select **Enabled**. |

| Floating IP | Select **Disabled**. |

| Outbound source network address translation (SNAT) | Leave the default of **(Recommended) Use outbound rules to provide backend pool members access to the internet.** |

25. Select **Add**.

26. Select the blue **Review + create** button at the bottom of the page.

27. Select **Create**.

> [!NOTE]

> In this example we'll create a NAT gateway to provide outbound Internet access. The outbound rules tab in the configuration is bypassed as it's optional and isn't needed with the NAT gateway. For more information on Azure NAT gateway, see [What is Azure Virtual Network NAT?](../virtual-network/nat-gateway/nat-overview.md)

> For more information about outbound connections in Azure, see [Source Network Address Translation (SNAT) for outbound connections](../load-balancer/load-balancer-outbound-connections.md)

## Create NAT gateway

In this section, you'll create a NAT gateway for outbound internet access for resources in the virtual network. For other options for outbound rules, check out [Network Address Translation (SNAT) for outbound connections](load-balancer-outbound-connections.md).

1. In the search box at the top of the portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

2. In **NAT gateways**, select **+ Create**.

3. In **Create network address translation (NAT) gateway**, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **TutorLoadBalancer-rg**. |

| **Instance details** |    |

| NAT gateway name | Enter **myNATgateway**. |

| Region | Select **East US**. |

| Availability zone | Select **None**. |

| Idle timeout (minutes) | Enter **15**. |

4. Select the **Outbound IP** tab or select **Next: Outbound IP** at the bottom of the page.

5. In **Outbound IP**, select **Create a new public IP address** next to **Public IP addresses**.

6. Enter **myNATgatewayIP** in **Name**.

7. Select **OK**.

8. Select the **Subnet** tab or select the **Next: Subnet** button at the bottom of the page.

9. In **Virtual network** in the **Subnet** tab, select **myVNet**.

10. Select **myBackendSubnet** under **Subnet name**.

11. Select the blue **Review + create** button at the bottom of the page, or select the **Review + create** tab.

12. Select **Create**.

## Create virtual machines

In this section, you'll create two VMs (**myVM1** and **myVM2**) in two different zones (**Zone 1**, and **Zone 2**).

These VMs are added to the backend pool of the load balancer that was created earlier.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

2. In **Virtual machines**, select **+ Create** > **Azure virtual machine**.

3. In **Create a virtual machine**, enter or select the following values in the **Basics** tab:

| Setting | Value                                          |

|-----------------------|----------------------------------|

| **Project Details** |  |

| Subscription | Select your Azure subscription |

| Resource Group | Select **TutorLoadBalancer-rg** |

| **Instance details** |  |

| Virtual machine name | Enter **myVM1** |

| Region | Select **((US) East US)** |

| Availability Options | Select **Availability zones** |

| Availability zone | Select **Zone 1** |

| Security type | Select **Standard**. |

| Image | Select **Windows Server 2022 Datacenter: Azure Edition - Gen2** |

| Azure Spot instance | Leave the default of unchecked. |

| Size | Choose VM size or take default setting |

| **Administrator account** |  |

| Username | Enter a username |

| Password | Enter a password |

| Confirm password | Reenter password |

| **Inbound port rules** |  |

| Public inbound ports | Select **None** |

4. Select the **Networking** tab, or select **Next: Disks**, then **Next: Networking**.

5. In the Networking tab, select or enter the following information:

| Setting | Value |

| ------- | ----- |

| **Network interface** |  |

| Virtual network | Select **myVNet** |

| Subnet | Select **myBackendSubnet** |

| Public IP | Select **None**. |

| NIC network security group | Select **Advanced** |

| Configure network security group | Skip this setting until the rest of the settings are completed. Complete after **Select a backend pool**.|

| Delete NIC when VM is deleted | Leave the default of **unselected**. |

| Accelerated networking | Leave the default of **selected**. |

| **Load balancing**  |

| **Load balancing options** |

| Load-balancing options | Select **Azure load balancer** |

| Select a load balancer | Select **myLoadBalancer**  |

| Select a backend pool | Select **myBackendPool** |

| Configure network security group | Select **Create new**. </br> In the **Create network security group**, enter **myNSG** in **Name**. </br> Under **Inbound rules**, select **+Add an inbound rule**. </br> Under  **Service**, select **HTTP**. </br> Under **Priority**, enter **100**. </br> In **Name**, enter **myNSGRule** </br> Select **Add** </br> Select **OK** |

6. Select **Review + create**.

7. Review the settings, and then select **Create**.

8. Follow the steps 1 through 7 to create another VM with the following values and all the other settings the same as **myVM1**:

| Setting | VM 2

| ------- | ----- |

| Name |  **myVM2** |

| Availability zone | **Zone 2** |

| Network security group | Select the existing **myNSG** |

[!INCLUDE [ephemeral-ip-note.md](~/reusable-content/ce-skilling/azure/includes/ephemeral-ip-note.md)]

## Install IIS

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

2. Select **myVM1**.

3. On the **Overview** page, select **Connect**, then **Bastion**.

4. Enter the username and password entered during VM creation.

5. Select **Connect**.

6. On the server desktop, navigate to **Start** > **Windows PowerShell** > **Windows PowerShell**.

7. In the PowerShell Window, run the following commands to:

* Install the IIS server

* Remove the default iisstart.htm file

* Add a new iisstart.htm file that displays the name of the VM:

```powershell

# Install IIS server role

Install-WindowsFeature -name Web-Server -IncludeManagementTools

# Remove default htm file

Remove-Item  C:\inetpub\wwwroot\iisstart.htm

# Add a new htm file that displays server name

Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)

```

8. Close the Bastion session with **myVM1**.

9. Repeat steps 1 to 8 to install IIS and the updated iisstart.htm file on **myVM2**.

## Test the load balancer

1. In the search box at the top of the page, enter **Public IP**. Select **Public IP addresses** in the search results.

2. In **Public IP addresses**, select **myPublicIP**.

3. Copy the item in **IP address**. Paste the public IP into the address bar of your browser. The custom VM page of the IIS Web server is displayed in the browser.

## Clean up resources

When no longer needed, delete the resource group, load balancer, and all related resources. To do so, select the resource group **TutorLoadBalancer-rg** that contains the resources and then select **Delete**.

## Next steps

Advance to the next article to learn how to:

> [!div class="nextstepaction"]

> [Create a public load balancer with an IP-based backend](tutorial-load-balancer-ip-backend-portal.md)
