# Nat Overview

# What is Azure NAT Gateway?

Azure NAT Gateway is a fully managed and highly resilient network address translation (NAT) service. Use Azure NAT Gateway to let all instances in a subnet connect outbound to the internet while remaining fully private. A NAT gateway doesn't permit unsolicited inbound connections from the internet. Only packets that arrive as response packets to an outbound connection can pass through a NAT gateway.

Azure NAT Gateway dynamically allocates secure NAT (SNAT) ports to automatically scale outbound connectivity and minimize the risk of SNAT port exhaustion.

Azure NAT Gateway is available in two SKUs:

* *Standard* is zonal (deployed to a single availability zone) and provides scalable outbound connectivity for subnets in a single virtual network.

* *StandardV2* is zone redundant and provides higher throughput than the Standard SKU, IPv6 support, and flow log support.

## Standard SKU

You can associate a Standard NAT gateway with subnets in the same virtual network to provide outbound connectivity to the internet. A Standard NAT gateway operates out of a single availability zone.

## StandardV2 SKU

The StandardV2 SKU of Azure NAT Gateway provides all the same functionality of the Standard SKU, such as dynamic SNAT port allocation and secure outbound connectivity for subnets within a virtual network. Additionally, StandardV2 is zone redundant, meaning that it provides outbound connectivity from all zones in a region instead of a single zone.

### Key capabilities of StandardV2

* **Zone redundancy**: Operates across all availability zones in a region to maintain connectivity during a single zone failure.

* **IPv6 support**: Supports both IPv4 and IPv6 public IP addresses and prefixes for outbound connectivity.

* **Higher throughput**: Provides up to 100 Gbps of data throughput per NAT gateway, compared to 50 Gbps for Standard NAT gateways.

* **Flow log support**: Provides IP-based traffic information to help monitor and analyze outbound traffic flows.

To learn more about how to deploy a StandardV2 NAT gateway, see [Create a StandardV2 NAT gateway](./quickstart-create-nat-gateway-v2.md).

<a name = "key-limitations-of-standardv2-nat-gateway"></a>

### Key limitations of StandardV2

* The StandardV2 SKU requires StandardV2 public IP addresses or prefixes. Standard public IPs aren't supported with StandardV2.

* You can't upgrade the Standard SKU to the StandardV2 SKU. You must create a StandardV2 NAT gateway to replace the Standard NAT gateway on your subnet.

* The following regions don't support StandardV2 NAT gateways:

* Canada East

* Chile Central

* Indonesia Central

* Israel Northwest

* Malaysia West

* Qatar Central

* Sweden South

* West India

### Known issues of StandardV2

* IPv6 outbound traffic that uses load balancer outbound rules is disrupted when you associate a StandardV2 NAT gateway with a subnet. If you require both IPv4 and IPv6 outbound connectivity, use either:

* Load balancer outbound rules for both IPv4 and IPv6 traffic

* A Standard NAT gateway for IPv4 traffic and load balancer outbound rules for IPv6 traffic

* Outbound connections that use a load balancer, Azure Firewall, or VM instance-level public IPs might be interrupted when you add a StandardV2 NAT gateway to a subnet. All net new outbound connections use the StandardV2 NAT gateway.

For more information about known issues and limitations of the StandardV2 SKU of Azure NAT Gateway, see [Known limitations](./nat-sku.md#known-limitations).

## Azure NAT Gateway benefits

### Simple setup

Deployments with Azure NAT Gateway are intentionally simple. Attach a NAT gateway to a subnet and public IP address, and start connecting outbound to the internet right away. No maintenance or routing configurations are required. You can add more public IPs or subnets later without affecting your existing configuration.

The following steps show an example of how to set up a NAT gateway:

1. Create a non-zonal or zonal NAT gateway.

1. Assign a public IP address or public IP prefix.

1. Configure a subnet to use the NAT gateway.

If necessary, modify Transmission Control Protocol (TCP) idle timeout (optional). Review [timers](/azure/nat-gateway/nat-gateway-resource#idle-timeout-timers) before you change the default.

### Security

Azure NAT Gateway is built on the Zero Trust network security model. When you use Azure NAT Gateway, private instances within a subnet don't need public IP addresses to reach the internet. Private resources can reach external sources outside the virtual network by using SNAT for static public IP addresses or prefixes in Azure NAT Gateway.

You can provide a contiguous set of IPs for outbound connectivity by using a public IP prefix. You can configure destination firewall rules based on this predictable IP list.

### Resiliency

Azure NAT Gateway is a fully managed and distributed service. It doesn't depend on individual compute instances such as virtual machines or a single physical gateway device. A NAT gateway always has multiple fault domains and can sustain multiple failures without service outages. Software-defined networking makes a NAT gateway highly resilient.

### Scalability

A NAT gateway is scaled out from creation. No ramp-up or scale-out operation is required. Azure manages the operation of a NAT gateway for you.

Attach a NAT gateway to a subnet to provide outbound connectivity for all private resources in that subnet. All subnets in a virtual network can use the same NAT gateway resource. You can scale out outbound connectivity by assigning up to 16 public IP addresses to a NAT gateway. When you associate a NAT gateway with a public IP prefix, it automatically scales to the number of IP addresses needed for outbound.

### Performance

Azure NAT Gateway is a software-defined networking service. Each NAT gateway can process up to 50 Gbps of data for both outbound and return traffic.

A NAT gateway doesn't affect the network bandwidth of your compute resources. For more information, see [Performance](nat-gateway-resource.md#performance).

## Azure NAT Gateway basics

Azure NAT Gateway provides secure, scalable outbound connectivity for resources in a virtual network.

### Outbound connectivity

* Azure NAT Gateway is the method that we recommend for outbound connectivity.

To migrate outbound access to a NAT gateway from default outbound access or load balancer outbound rules, see [Migrate outbound access to Azure NAT Gateway](./tutorial-migrate-outbound-nat.md).

> [!NOTE]

> As of March 31, 2026, new virtual networks default to using private subnets. [Default outbound access](/azure/virtual-network/ip-services/default-outbound-access#when-is-default-outbound-access-provided) isn't provided by default. Use an explicit form of outbound connectivity instead, like Azure NAT Gateway.

* Azure NAT Gateway provides outbound connectivity at a subnet level. It replaces the default internet destination of a subnet to provide outbound connectivity.

* Azure NAT Gateway doesn't require any routing configurations on a subnet route table. After you attach a NAT gateway to a subnet, it provides outbound connectivity right away.

* Azure NAT Gateway allows flows to be created from the virtual network to the services outside your virtual network. Return traffic from the internet is allowed only in response to an active flow. Services outside your virtual network can't initiate an inbound connection through a NAT gateway.

* Azure NAT Gateway takes precedence over other outbound connectivity methods, including a load balancer, instance-level public IP addresses, and Azure Firewall.

* Azure NAT Gateway takes priority over other explicit outbound methods configured in a virtual network for all new connections. There are no drops in traffic flow for existing connections that use other explicit methods of outbound connectivity.

* Azure NAT Gateway doesn't have the same limitations of SNAT port exhaustion as [default outbound access](../virtual-network/ip-services/default-outbound-access.md) and [outbound rules of a load balancer](../load-balancer/outbound-rules.md).

* Azure NAT Gateway supports TCP, User Datagram Protocol (UDP) and Internet Control Message Protocol (ICMP) (Echo Request and Echo Reply).

> [!NOTE]

> Azure StandardV2 NAT Gateway supports outbound Internet Control Message Protocol (ICMP) Echo Request and Echo Reply (ping) for both IPv4 and IPv6. This capability is provided by default and requires no additional configuration. You can use the ping tool (ICMP Echo) to validate outbound connectivity and quickly diagnose reachability issues from your workloads. For steps to validate connectivity, see [Validate NAT gateway connectivity](/azure/nat-gateway/troubleshoot-nat#validate-nat-gateway-connectivity).

* Azure NAT Gateway supports [Azure App Service instances](/azure/app-service/networking/nat-gateway-integration) (web applications, REST APIs, and mobile back ends) through [virtual network integration](/azure/app-service/overview-vnet-integration).

* The subnet has a [system default route](/azure/virtual-network/virtual-networks-udr-overview#default) that routes traffic with destination 0.0.0.0/0 to the internet automatically. After you configure a NAT gateway to the subnet, virtual machines in the subnet communicate with the internet by using the public IP of the NAT gateway.

* When you create a user-defined route (UDR) in your subnet route table for 0.0.0.0/0 traffic, you override the default internet path for this traffic. A UDR that sends 0.0.0.0/0 traffic to a virtual appliance or a virtual network gateway (Azure VPN Gateway and Azure ExpressRoute) as the next hop type instead overrides NAT gateway connectivity to the internet.

Here's the flow:

UDR to next hop virtual appliance or virtual network gateway >> NAT gateway >> instance-level public IP address on a virtual machine >> load balancer outbound rules >> default system route to the internet.

### NAT gateway configurations

* Multiple subnets within the same virtual network can use different NAT gateways or the same NAT gateway.

* You can't attach multiple NAT gateways to a single subnet.

* A NAT gateway can't span multiple virtual networks. However, you can use a NAT gateway to provide outbound connectivity in a hub-and-spoke model. For more information, see the [Azure NAT Gateway hub-and-spoke tutorial](/azure/nat-gateway/tutorial-hub-spoke-route-nat).

* A Standard NAT gateway resource can use up to 16 IPv4 public IP addresses. A StandardV2 NAT gateway resource can use up to 16 IPv4 and 16 IPv6 public IP addresses.

* You can't deploy a NAT gateway in a [gateway subnet](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsub) or a subnet that contains [SQL managed instances](/azure/azure-sql/managed-instance/connectivity-architecture-overview#networking-constraints).

* Azure NAT Gateway works with any VM network interface or IP configuration. A NAT gateway can use SNAT for multiple IP configurations on a network interface.

* You can associate a NAT gateway with an Azure Firewall subnet in a hub virtual network and provide outbound connectivity from spoke virtual networks peered to the hub. To learn more, see the [article about Azure Firewall integration with Azure NAT Gateway](../firewall/integrate-with-nat-gateway.md).

### Availability zones

* You can create a Standard NAT gateway in a specific availability zone or place it in **No zone**.

* You can isolate a Standard NAT gateway in a specific zone when you create a [zonal NAT gateway](/azure/reliability/reliability-nat-gateway). After you deploy the NAT gateway, you can't change the zone selection.

* By default, a Standard NAT gateway is placed in **No zone**. Azure places a [nonzonal NAT gateway](/azure/reliability/reliability-nat-gateway) in a zone for you.

* A StandardV2 NAT gateway is zone redundant and operates across all availability zones in a region to maintain connectivity during a single zone failure.

### Default outbound access

* To provide secure outbound connectivity to the internet, [enable a private subnet](/azure/virtual-network/ip-services/default-outbound-access#how-can-i-transition-to-an-explicit-method-of-public-connectivity-and-disable-default-outbound-access). With this approach, you prevent the creation of default outbound IPs and instead use an explicit method of outbound connectivity, like a NAT gateway.

* Certain services don't function on a virtual machine in a private subnet without an explicit method of outbound connectivity, such as Windows Activation and Windows Updates. Activating or updating VM operating systems, such as Windows, requires an explicit method of outbound connectivity, like a NAT gateway.

* To migrate outbound access to a NAT gateway from default outbound access or load balancer outbound rules, see [Migrate outbound access to Azure NAT Gateway](./tutorial-migrate-outbound-nat.md).

> [!NOTE]

> As of March 31, 2026, new virtual networks default to using private subnets. [Default outbound access](/azure/virtual-network/ip-services/default-outbound-access#when-is-default-outbound-access-provided) is no longer provided by default. You must enable an explicit outbound method to reach public endpoints on the internet and within Microsoft. Use an explicit form of outbound connectivity instead, like a NAT gateway.

### Azure NAT Gateway and Basic resources

* A Standard NAT gateway works with Standard public IP addresses or public IP prefixes. A StandardV2 NAT gateway works only with StandardV2 public IP addresses or public IP prefixes.

* You can't use Azure NAT Gateway with subnets that have Basic resources. Resources for the Basic SKU, such as a Basic load balancer or Basic public IPs, don't work with Azure NAT Gateway. You can upgrade a Basic load balancer and Basic public IP to Standard to work with a NAT gateway.

* For more information about upgrading a load balancer from Basic to Standard, see [Upgrade a Basic load balancer](/azure/load-balancer/upgrade-basic-standard-with-powershell).

* For more information about upgrading a public IP from Basic to Standard, see [Upgrade a public IP address](../virtual-network/ip-services/public-ip-upgrade-portal.md).

* For more information about upgrading a public IP attached to a virtual machine from Basic to Standard, see [Upgrade a Basic public IP attached to a virtual machine](/azure/virtual-network/ip-services/public-ip-upgrade-vm).

### Connection timeouts and timers

* Azure NAT Gateway sends a TCP Reset (RST) packet for any connection flow that it doesn't recognize as an existing connection. The connection flow no longer exists if the Azure NAT Gateway idle timeout is reached or the connection was closed earlier.

* When the sender of traffic on the nonexistent connection flow receives the Azure NAT Gateway TCP RST packet, the connection is no longer usable.

* SNAT ports aren't readily available for reuse to the same destination endpoint after a connection closes. Azure NAT Gateway places SNAT ports in a cooldown state before they can be reused to connect to the same destination endpoint.

* SNAT port reuse (cooldown) timer durations vary for TCP traffic, depending on how the connection closes. To learn more, see [Port reuse timers](./nat-gateway-resource.md#port-reuse-timers).

* The Azure NAT Gateway TCP idle timeout timer defaults to 4 minutes but can be increased up to 120 minutes. Any activity on a flow can reset the idle timer, including TCP keepalives. To learn more, see [Idle timeout timers](./nat-gateway-resource.md#idle-timeout-timers).

* UDP traffic has an idle timeout timer of 4 minutes that you can't change.

* UDP traffic has a port reuse timer of 65 seconds. For this duration, a port is in hold-down before it's available for reuse to the same destination endpoint.

## Pricing and SLA

Standard and StandardV2 NAT gateways are the same price. For more information, see [Azure NAT Gateway pricing](https://azure.microsoft.com/pricing/details/azure-nat-gateway/).

For information on the service-level agreement (SLA), see the [Microsoft SLAs for online services](https://azure.microsoft.com/support/legal/sla/virtual-network-nat/v1_0/).

## Related content

* For more information about creating and validating a NAT gateway, see [Quickstart: Create a NAT gateway by using the Azure portal](quickstart-create-nat-gateway-portal.md).

* To view a video that provides more information about Azure NAT Gateway, see [How to get better outbound connectivity using Azure NAT Gateway](https://www.youtube.com/watch?v=2Ng_uM0ZaB4).

* For more information about the NAT gateway resource, see [NAT gateway resource](./nat-gateway-resource.md).


# Nat Gateway Resource

# NAT gateway resource

This article describes the key components of a network address translation (NAT) gateway resource that enable it to provide highly secure, scalable, and resilient outbound connectivity. NAT gateway resources are part of the Azure NAT Gateway service.

You can configure a NAT gateway in your subscription through supported clients. These clients include the Azure portal, the Azure CLI, Azure PowerShell, Azure Resource Manager templates, or appropriate alternatives.

## Azure NAT Gateway SKUs

Azure NAT Gateway is available in two SKUs: StandardV2 and Standard.

The StandardV2 SKU is zone redundant by default. It automatically spans multiple availability zones in a region to provide continued outbound connectivity even if one zone becomes unavailable.

The Standard SKU is a zonal resource. It's deployed into a specific availability zone and is resilient within that zone.

A StandardV2 NAT gateway supports IPv4 and IPv6 public IPs, whereas a Standard NAT gateway supports only IPv4 public IPs.

## Azure NAT Gateway architecture

Azure NAT Gateway uses software-defined networking to operate as a fully managed, distributed service. By design, a NAT gateway spans multiple fault domains, enabling it to withstand multiple failures without any effect to the service.

Azure NAT Gateway provides source network address translation (SNAT) for private instances within the associated subnets of your Azure virtual network. The private IPs of the virtual machines use SNAT for a NAT gateway's static public IP addresses to connect outbound to the internet. Azure NAT Gateway also provides destination network address translation (DNAT) for response packets to an outbound-originated connection only.

When a NAT gateway is configured to a subnet within a virtual network, it becomes the subnet's default next hop type for all outbound traffic directed to the internet. No extra routing configurations are required. A NAT gateway doesn't provide unsolicited inbound connections from the internet. DNAT is performed only for packets that arrive as a response to an outbound packet.

## Subnets

You can attach a StandardV2 or Standard NAT gateway to multiple subnets within a virtual network to provide outbound connectivity to the internet. When a NAT gateway is attached to a subnet, it assumes the default route to the internet. The NAT gateway serves as the next hop type for all outbound traffic destined for the internet.

NAT gateways have these limitations for subnet configurations:

* Each subnet can't have more than one NAT gateway attached.

* You can't attach a NAT gateway to subnets from different virtual networks.

* You can't use a NAT gateway with a [gateway subnet](/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsub). A gateway subnet is a designated subnet for a VPN gateway to send encrypted traffic between an Azure virtual network and on-premises location.

## Static public IP addresses

A NAT gateway can be associated with static public IP addresses or public IP prefixes. If you assign a public IP prefix, the entire public IP prefix is used. You can use a public IP prefix directly or [distribute the public IP addresses of the prefix](../virtual-network/ip-services/manage-public-ip-address-prefix.md) across multiple NAT gateway resources. The NAT gateway sends all traffic to the range of IP addresses of the prefix.

These conditions apply:

* A StandardV2 NAT gateway supports up to 16 IPv4 and 16 IPv6 public IP addresses.

* You can't use a Standard NAT gateway with IPv6 public IP addresses or prefixes. A Standard NAT gateway supports up to 16 IPv4 public IP addresses.

* You can't use a NAT gateway with public IP addresses for the Basic SKU.

| Azure NAT Gateway SKU | IPv4 | IPv6 |

| --- | --- | --- |

| StandardV2 | Yes, supports IPv4 public IP addresses and prefixes. | Yes, supports IPv6 public IP addresses and prefixes. |

| Standard | Yes, supports IPv4 public IP addresses and prefixes. | No, does not support IPv6 public IP addresses and prefixes. |

## SNAT ports

SNAT port inventory is provided by the public IP addresses, public IP prefixes, or both attached to a NAT gateway. SNAT port inventory is available on demand to all instances within a subnet attached to the NAT gateway. No preallocation of SNAT ports per instance is required.

For more information about SNAT ports and Azure NAT Gateway, see [Source Network Address Translation (SNAT) with Azure NAT Gateway](nat-gateway-snat.md).

When multiple subnets within a virtual network are attached to the same NAT gateway resource, the SNAT port inventory that the NAT gateway provides is shared across all subnets.

SNAT ports serve as unique identifiers to distinguish connection flows from one another. The *same SNAT port* can be used to connect to *different destination endpoints* at the same time.

*Different SNAT ports* are used to make connections to the *same destination endpoint* in order to distinguish connection flows from one another. SNAT ports being reused to connect to the same destination are placed on a [reuse cool-down timer](#port-reuse-timers) before they can be reused.

A single NAT gateway can scale by the number of public IP addresses associated with it. Each public IP address for a NAT gateway provides 64,512 SNAT ports to make outbound connections. A NAT gateway can scale up to more than 1 million SNAT ports. TCP and UDP are separate SNAT port inventories and are unrelated to NAT gateways.

## Availability zones

Azure NAT Gateway has two SKUs: Standard and StandardV2. To ensure that your architecture is resilient to zonal failures, deploy a StandardV2 NAT gateway, because it's a zone-redundant resource. When an [availability zone](/azure/reliability/availability-zones-overview) in a region goes down, new connections flow from the remaining healthy zones.

A Standard NAT gateway is a zonal resource, which means you can deploy and operate it out of individual availability zones. If the zone that's associated with a Standard NAT gateway goes down, the outage affects outbound connectivity for the subnets associated with the NAT gateway.

For more information about availability zones and Azure NAT Gateway, see [Reliability in Azure NAT Gateway](/azure/reliability/reliability-nat-gateway).

After you deploy a NAT gateway, you can't change the zone selection.

## Protocols

A NAT gateway interacts with IP and IP transport headers of UDP and TCP flows. A NAT gateway is agnostic to application-layer payloads. StandardV2 NAT Gateway also supports ICMP Echo Request and Echo Reply (ping). Other ICMP message types aren't supported.

> [!NOTE]

> Azure StandardV2 NAT Gateway supports outbound Internet Control Message Protocol (ICMP) Echo Request and Echo Reply (ping) for both IPv4 and IPv6. This capability is provided by default and requires no additional configuration. You can use the ping tool (ICMP Echo) to validate outbound connectivity and quickly diagnose reachability issues from your workloads. For steps to validate connectivity, see [Validate NAT gateway connectivity](/azure/nat-gateway/troubleshoot-nat#validate-nat-gateway-connectivity).

## TCP reset

A TCP reset packet is sent when a NAT gateway detects traffic on a connection flow that doesn't exist. The TCP reset packet indicates to the receiving endpoint that the connection flow was released and any future communication on this same TCP connection will fail. TCP reset is unidirectional for a NAT gateway.

The connection flow might not exist if:

* The connection reached the idle timeout after a period of inactivity on the connection flow, and the connection is silently dropped.

* The sender, either from the Azure network side or from the public internet side, sent traffic after the connection dropped.

The system sends a TCP reset packet only when it detects traffic on the dropped connection flow. This operation means a TCP reset packet might not be sent right away after a connection flow drops.

The system sends a TCP reset packet in response to detecting traffic on a nonexistent connection flow, regardless of whether the traffic originates from the Azure network side or the public internet side.

## TCP idle timeout

A NAT gateway provides a configurable idle timeout range of 4 minutes to 120 minutes for TCP protocols. UDP protocols have a nonconfigurable idle timeout of 4 minutes.

When a connection goes idle, the NAT gateway holds onto the SNAT port until the connection idle times out. Because long idle timeout timers can unnecessarily increase the likelihood of SNAT port exhaustion, we don't recommend that you increase the TCP idle timeout duration to longer than the default time of 4 minutes. The idle timer doesn't affect a flow that never goes idle.

You can use TCP keepalives to provide a pattern of refreshing long idle connections and endpoint liveness detection. For more information, see [these .NET examples](/dotnet/api/system.net.servicepoint.settcpkeepalive). TCP keepalives appear as duplicate acknowledgements (ACKs) to the endpoints, are low overhead, and are invisible to the application layer.

UDP idle timeout timers aren't configurable. You should use UDP keepalives to ensure that the connection doesn't reach the idle timeout value, and to maintain the connection. Unlike TCP connections, a UDP keepalive enabled on one side of the connection applies only to traffic flow in one direction. You must enable UDP keepalives on both sides of the traffic flow to keep the traffic flow alive.

## Timers

### Port reuse timers

Port reuse timers determine the amount of time after a connection closes that a source port is in hold-down before it can be reused for a new connection to go to the same destination endpoint by the NAT gateway.

The following table provides information about when a TCP port becomes available for reuse to the same destination endpoint by the NAT gateway.

| Timer | Description | Value |

| --- | --- | --- |

| TCP FIN | After a TCP FIN packet closes a connection, a 65-second timer holds down the SNAT port. The SNAT port is available for reuse after the timer ends. | 65 seconds |

| TCP RST | After a TCP RST packet (reset) closes a connection, a 16-second timer holds down the SNAT port. When the timer ends, the port is available for reuse. | 16 seconds |

| TCP half open | During connection establishment where one connection endpoint is waiting for acknowledgment from the other endpoint, a 30-second timer begins. If no traffic is detected, the connection closes. After the connection closes, the source port is available for reuse to the same destination endpoint. | 30 seconds |

For UDP traffic, after a connection closes, the port is in hold-down for 65 seconds before it's available for reuse.

### Idle timeout timers

| Timer | Description | Value |

| --- | --- | --- |

| TCP idle timeout | TCP connections can go idle when neither endpoint transmits any data for a prolonged period of time. You can configure a timer from 4 minutes (default) to 120 minutes (2 hours) to time out an idle connection. Traffic on the flow resets the idle timeout timer. | Configurable; 4 minutes (default) to 120 minutes |

| UDP idle timeout | UDP connections can go idle when endpoints don't transmit data for a prolonged period of time. UDP idle timeout timers are 4 minutes and are *not configurable*. Traffic on the flow resets the idle timeout timer. | Not configurable; 4 minutes |

> [!NOTE]

> These timer settings are subject to change. The provided values can help with troubleshooting. You shouldn't take a dependency on specific timers at this time.

## Bandwidth

Each SKU of Azure NAT Gateway has bandwidth limits:

* A StandardV2 NAT gateway supports up to 100 Gbps of data throughput per NAT gateway resource.

* A Standard NAT gateway provides 50 Gbps of throughput, which is split between outbound and inbound (response) data. Data throughput is rate limited at 25 Gbps for outbound and 25 Gbps for inbound (response) data per Standard NAT gateway resource.

## Performance

Standard and StandardV2 NAT gateways each support up to 50,000 concurrent connections per public IP address *to the same destination endpoint* over the internet for TCP and UDP traffic.

Each can support up to 2 million active connections simultaneously. The number of connections on a NAT gateway is counted based on the 5-tuple (source IP address, source port, destination IP address, destination port, and protocol). If a NAT gateway exceeds 2 million connections, the data path's availability declines and new connections fail.

A StandardV2 NAT gateway can process up to 10 million packets per second. A Standard NAT gateway can process up to 5 million packets per second.

## Limitations

* Standard and Basic public IPs aren't compatible with StandardV2 NAT gateways. Use StandardV2 public IPs instead.

To create a StandardV2 public IP, see [Create an Azure public IP](../virtual-network/ip-services/create-public-ip-portal.md).

* Basic load balancers aren't compatible with NAT gateways. Use Standard load balancers for both Standard and StandardV2 NAT gateways.

To upgrade a load balancer from Basic to Standard, see [Upgrade an Azure public load balancer](../load-balancer/upgrade-basic-standard.md).

* Basic public IPs aren't compatible with Standard NAT gateways. Use Standard public IPs instead.

To upgrade a public IP address from Basic to Standard, see [Upgrade a Basic public IP address to Standard](../virtual-network/ip-services/public-ip-basic-upgrade-guidance.md).

* Azure StandardV2 NAT Gateway supports outbound ICMP Echo Request and Echo Reply traffic (ping) for IPv4 and IPv6 scenarios. Other ICMP message types aren't supported.

* IP fragmentation isn't available for Azure NAT Gateway.

* Azure NAT Gateway doesn't support public IP addresses with a routing configuration type of **Internet**. To see a list of Azure services that do support the **Internet** routing configuration on public IPs, see [Supported services for routing over the public internet](/azure/virtual-network/ip-services/routing-preference-overview#supported-services).

* Azure NAT Gateway doesn't support public IPs with DDoS protection enabled. For more information, see [DDoS limitations](/azure/ddos-protection/ddos-protection-sku-comparison#limitations).

* Azure NAT Gateway isn't supported in a secured virtual hub network (vWAN) architecture.

* You can't upgrade a Standard NAT gateway to a StandardV2 NAT gateway. To achieve zone resiliency for architectures that use zonal NAT gateways, you must deploy a StandardV2 NAT gateway to replace the Standard SKU NAT gateway.

* You can't use Standard public IPs with a StandardV2 NAT gateway. You must re-IP to new StandardV2 public IPs to use a StandardV2 NAT gateway.

For more known limitations of StandardV2 NAT gateways, see [Azure NAT Gateway SKUs](nat-sku.md).

## Related content

* Review the [Azure NAT Gateway overview](nat-overview.md).

* Learn about [metrics and alerts for Azure NAT Gateway](nat-metrics.md).

* Learn how to [troubleshoot Azure NAT Gateway](troubleshoot-nat.md).


# Nat Metrics

# What is Azure NAT Gateway metrics and alerts?

This article provides an overview of all NAT gateway metrics and diagnostic capabilities. This article provides general guidance on how to use metrics and alerts to monitor, manage, and [troubleshoot](troubleshoot-nat.md) your NAT gateway resource.

All metrics are the same for Standard and StandardV2 NAT Gateway.

- Network Insights: Azure Monitor Insights provides you with visual tools to view, monitor, and assist you in diagnosing issues with your NAT gateway resource. Insights provide you with a topological map of your Azure setup and metrics dashboards.

*Figure: Azure NAT Gateway for outbound to Internet*

## Metrics overview

[!INCLUDE [horz-monitor-ref-metrics-tableheader](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-tableheader.md)]

[!INCLUDE [Microsoft.Network/natgateways](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/metrics/microsoft-network-natgateways-metrics-include.md)]

>[!NOTE]

> Count aggregation is not recommended for any of the NAT gateway metrics. Count aggregation adds up the number of metric values and not the metric values themselves. Use Sum aggregation instead to get the best representation of data values for connection count, bytes, and packets metrics.

>

> Use average for best represented health data for the datapath availability metric.

>

> For information about aggregation types, see [aggregation types](/azure/azure-monitor/essentials/metrics-aggregation-explained#aggregation-types).

## Where to find my NAT gateway metrics

NAT gateway metrics can be found in the following locations in the Azure portal.

- **Metrics** page under **Monitoring** from a NAT gateway's resource page.

- **Insights** page under **Monitoring** from a NAT gateway's resource page.

- Azure Monitor page under **Metrics**.

To view any one of your metrics for a given NAT gateway resource:

1. Select the NAT gateway resource you would like to monitor.

1. In the **Metric** drop-down menu, select one of the provided metrics.

1. In the **Aggregation** drop-down menu, select the recommended aggregation listed in the [metrics overview](#metrics-overview) table.

1. To adjust the time frame over which the chosen metric is presented on the metrics graph or to adjust how frequently the chosen metric is measured, select the **Time** window in the top right corner of the metrics page and make your adjustments.

## How to use NAT gateway metrics

The following sections detail how to use each NAT gateway metric to monitor, manage, and troubleshoot your NAT gateway resource.

### Bytes

The Bytes metric shows you the amount of data going outbound through NAT gateway and returning inbound in response to an outbound connection.

Use this metric to:

- View the amount of data being processed through NAT gateway to connect outbound or return inbound.

To view the amount of data passing through NAT gateway:

1. Select the NAT gateway resource you would like to monitor.

1. In the **Metric** drop-down menu, select the **Bytes** metric.

1. In the **Aggregation** drop-down menu, select **Sum**.

1. Select to **Add filter**.

1. In the **Property** drop-down menu, select **Direction (Out | In)**.

1. In the **Values** drop-down menu, select **Out**, **In**, or both.

1. To see data processed inbound or outbound as their own individual lines in the metric graph, select **Apply splitting**.

1. In the **Values** drop-down menu, select **Direction (Out | In)**.

### Packets

The Packets metric shows you the number of data packets passing through NAT gateway.

Use this metric to:

- Verify that traffic is passing outbound or returning inbound through NAT gateway.

- View the amount of traffic going outbound through NAT gateway or returning inbound.

To view the number of packets sent in one or both directions through NAT gateway, follow the same steps in the [Bytes](#bytes) section.

### Dropped Packets

The Dropped Packets metric shows you the number of data packets dropped by NAT gateway when traffic goes outbound or returns inbound in response to an outbound connection.

Use this metric to:

- Check if periods of dropped packets coincide with periods of failed SNAT connections with the [SNAT Connection Count](#snat-connection-count) metric.

- Help determine if you're experiencing a pattern of failed outbound connections or SNAT port exhaustion.

Possible reasons for dropped packets:

- Outbound connectivity failure can cause packets to drop. Connectivity failure can happen for various reasons. See the [NAT gateway connectivity troubleshooting guide](/azure/nat-gateway/troubleshoot-nat-connectivity) to help you further diagnose.

### SNAT Connection Count

The SNAT Connection Count metric shows you the number of new SNAT connections within a specified time frame. This metric can be filtered by **Attempted** and **Failed** connection states. A failed connection volume greater than zero can indicate SNAT port exhaustion.

Use this metric to:

- Evaluate the health of your outbound connections.

- Help diagnose if your NAT gateway is experiencing SNAT port exhaustion.

- Determine if you're experiencing a pattern of failed outbound connections.

To view the connection state of your connections:

1. Select the NAT gateway resource you would like to monitor.

1. In the **Metric** drop-down menu, select the **SNAT Connection Count** metric.

1. In the **Aggregation** drop-down menu, select **Sum**.

1. Select to **Add filter**.

1. In the **Property** drop-down menu, select **Connection State**.

1. In the **Values** drop-down menu, select **Attempted**, **Failed**, or both.

1. To see attempted and failed connections as their own individual lines in the metric graph, select **Apply splitting**.

1. In the **Values** drop-down menu, select **Connection State**.

### Total SNAT Connection Count

The Total SNAT Connection Count metric shows you the total number of active SNAT connections passing through NAT gateway.

You can use this metric to:

- Evaluate the volume of connections passing through NAT gateway.

- Determine if you're nearing the connection limit of NAT gateway.

- Help assess if you're experiencing a pattern of failed outbound connections.

Possible reasons for failed connections:

- A pattern of failed connections can happen for various reasons. See the [NAT gateway connectivity troubleshooting guide](/azure/nat-gateway/troubleshoot-nat-connectivity) to help you further diagnose.

>[!NOTE]

> When NAT gateway is attached to a subnet and public IP address, the Azure platform verifies NAT gateway is healthy by conducting health checks. These health checks appear in NAT gateway's SNAT Connection Count metrics. The amount of health check related connections may vary as the health check service is optimized, but is negligible and doesn’t impact NAT gateway’s ability to connect outbound.

### Datapath Availability

The datapath availability metric measures the health of the NAT gateway resource over time. This metric indicates if NAT gateway is available for directing outbound traffic to the internet. This metric is a reflection of the health of the Azure infrastructure.

You can use this metric to:

- Monitor the availability of NAT gateway.

- Investigate the platform where your NAT gateway is deployed and determine if it’s healthy.

- Isolate whether an event is related to your NAT gateway or to the underlying data plane.

Possible reasons for a drop in data path availability include:

- An infrastructure outage.

- There aren't healthy VMs available in your NAT gateway configured subnet. For more information, see the [NAT gateway connectivity troubleshooting guide](/azure/nat-gateway/troubleshoot-nat-connectivity).

## Alerts

Alerts can be configured in Azure Monitor for all NAT gateway metrics. These alerts proactively notify you when important conditions are found in your monitoring data. They allow you to identify and address potential issues with NAT gateway.

For more information about how metric alerts work, see [Azure Monitor Metric Alerts](/azure/azure-monitor/alerts/alerts-metric-overview). The following guidance describes how to configure some common and recommended types of alerts for your NAT gateway.

### Alerts for datapath availability degradation

Set up an alert on datapath availability to help you detect issues with the health of NAT gateway.

The recommended guidance is to alert on NAT gateway’s datapath availability when it drops below 90% over a 15-minute period. This configuration is indicative of a NAT gateway resource being in a degraded state.

To set up a datapath availability alert, follow these steps:

1. From the NAT gateway resource page, select **Alerts**.

1. Select **Create alert rule**.

1. From the signal list, select **Datapath Availability**.

1. From the **Operator** drop-down menu, select **Less than**.

1. From the **Aggregation type** drop-down menu, select **Average**.

1. In the **Threshold value** box, enter **90%**.

1. From the **Unit** drop-down menu, select **Count**.

1. From the **Aggregation granularity (Period)** drop-down menu, select **15 minutes**.

1. Create an **Action** for your alert by providing a name, notification type, and type of action that is performed when the alert is triggered.

1. Before deploying your action, **test the action group**.

1. Select **Create** to create the alert rule.

>[!NOTE]

>Aggregation granularity is the period of time over which the datapath availability is measured to determine if it has dropped below the threshold value.

Setting the aggregation granularity to less than 5 minutes may trigger false positive alerts that detect noise in the datapath.

### Alerts for SNAT port exhaustion

Set up an alert on the **SNAT Connection Count** metric to notify you of connection failures on your NAT gateway. A failed connection volume greater than zero can indicate that you reached the connection limit on your NAT gateway or that you hit SNAT port exhaustion. Investigate further to determine the root cause of these failures.

To create the alert, use the following steps:

1. From the NAT gateway resource page, select **Alerts**.

1. Select **Create alert rule**.

1. From the signal list, select **SNAT Connection Count**.

1. From the **Aggregation type** drop-down menu, select **Total**.

1. From the **Operator** drop-down menu, select **Greater than**.

1. From the **Unit** drop-down menu, select **Count**.

1. In the **Threshold value** box, enter 0.

1. In the Split by dimensions section, select **Connection State** under Dimension name.

1. Under Dimension values, select **Failed** connections.

1. From the When to evaluate section, select **1 minute** under the **Check every** drop-down menu.

1. For the lookback period, select **5 minutes** from the drop-down menu options.

1. Create an **Action** for your alert by providing a name, notification type, and type of action that is performed when the alert is triggered.

1. Before deploying your action, **test the action group**.

1. Select **Create** to create the alert rule.

>[!NOTE]

>SNAT port exhaustion on your NAT gateway resource is uncommon. If you see SNAT port exhaustion, check if NAT gateway's idle timeout timer is set higher than the default amount of 4 minutes. A long idle timeout timer setting can cause SNAT ports to be in hold down for longer, which results in exhausting SNAT port inventory sooner. You can also scale your NAT gateway with additional public IPs to increase NAT gateway's overall SNAT port inventory. To troubleshoot these kinds of issues, refer to the [NAT gateway connectivity troubleshooting guide](/azure/nat-gateway/troubleshoot-nat-connectivity#snat-exhaustion-due-to-nat-gateway-configuration).

### Alerts for nearing total SNAT connection count limit

Standard NAT gateway and StandardV2 NAT gateway each have a total active connection limit of 2 million connections.

The recommended guidance is to alert on NAT gateway’s Total SNAT Connection Count when it hits 80% of the total NAT gateway connection count limit, 1.6 million connections.

>[!Note]

> The 80% threshold is a recommended starting point. You can adjust the threshold value based on your NAT gateway usage patterns and connection volume. Depending on the number of public IPs associated to your NAT gateway, and the amount of destination endpoints being reached, you could hit the connection limit sooner than 2 million. NAT gateway supports up to 50,000 connections per public IP address per destination endpoint.

To set up a Total SNAT Connection count alert, follow these steps:

1. From the NAT gateway resource page, select **Alerts**.

2. Select **Create alert rule**.

3. From the signal list, select **Total SNAT Connection Count**.

4. In the Alert logic section, set **Threshold type** to **Static**.

5. From the Aggregation type drop-down menu, select **Total**.

6. From the **Value is** drop-down menu, select **Greater than**.

7. From the **Unit** drop-down menu, select **Count**.

8. In the **Threshold value** box, enter **1,600,000**.

9. In the **When to evaluate** section, set **Check every** to **1 minute**.

10. Set the **Lookback Period** to **5 minutes**.

>[!Note]

>The lookback period may need to be adjusted based on the connection patterns of your outbound traffic through NAT gateway. If you find that you’re alert is too noisy, set the look back period to a longer time duration.

11. Create an **Action** for your alert by providing a name, notification type, and type of action that is performed when the alert is triggered.

12. Before deploying your action, **test the action group**.

13. Select **Create** to create the alert rule.

### Alerts for NAT gateway resource health

[Azure Resource Health](/azure/service-health/overview) provides information on the health state of your NAT gateway resource. The resource health of your NAT gateway is evaluated by measuring the datapath availability of your NAT gateway endpoint. You can set up alerts to notify you when the health state of your NAT gateway resource changes. To learn more about NAT gateway resource health and setting up alerts, see:

* [Azure NAT Gateway Resource Health](/azure/nat-gateway/resource-health)

* [NAT Gateway Resource Health Alerts](/azure/nat-gateway/resource-health#resource-health-alerts)

* [How to create Resource Health Alerts in the Azure portal](/azure/service-health/resource-health-alert-monitor-guide)

## Network Insights

[Azure Monitor Network Insights](../network-watcher/network-insights-overview.md) allows you to visualize your Azure infrastructure setup and to review all metrics for your NAT gateway resource from a preconfigured metrics dashboard. These visual tools help you diagnose and troubleshoot any issues with your NAT gateway resource.

### View the topology of your Azure architectural setup

To view a topological map of your setup in Azure:

1. From your NAT gateway’s resource page, select **Insights** from the **Monitoring** section.

1. On the landing page for **Insights**, there's a topology map of your NAT gateway setup. This map shows the relationship between the different components of your network (subnets, virtual machines, public IP addresses).

1. Hover over any component in the topology map to view configuration information.

### View all NAT gateway metrics in a dashboard

The metrics dashboard can be used to better understand the performance and health of your NAT gateway resource. The metrics dashboard shows a view of all metrics for NAT gateway on a single page.

- All NAT gateway metrics can be viewed in a dashboard when selecting **Show Metrics Pane**.

- A full page view of all NAT gateway metrics can be viewed when selecting **View Detailed Metrics**.

For more information on what each metric is showing you and how to analyze these metrics, see [How to use NAT gateway metrics](#how-to-use-nat-gateway-metrics).

## Metrics FAQ

### What type of metrics are available for NAT gateway?

Standard and StandardV2 NAT gateway supports [multi-dimensional metrics](/azure/azure-monitor/essentials/data-platform-metrics#multi-dimensional-metrics). You can filter the multi-dimensional metrics by different dimensions to gain greater insight into the provided data. The [SNAT Connection Count](#snat-connection-count) metric allows you to filter the connections by Attempted and Failed connections, enabling you to distinguish between different types of connections made by the NAT gateway.

Refer to the dimensions column in the [metrics overview](#metrics-overview) table to see which dimensions are available for each NAT gateway metric.

### How do I store NAT gateway metrics long-term?

All [platform metrics are stored](/azure/azure-monitor/essentials/data-platform-metrics#retention-of-metrics) for 93 days. If you require long term access to your NAT gateway metrics data, NAT gateway metrics can be retrieved by using the [metrics REST API](/rest/api/monitor/metrics/list). For more information on how to use the API, see the [Azure monitoring REST API walkthrough](/azure/azure-monitor/essentials/rest-api-walkthrough).

>[!NOTE]

>Diagnostic Settings [doesn’t support the export of multi-dimensional metrics](/azure/azure-monitor/reference/supported-metrics/metrics-index#exporting-platform-metrics-to-other-locations) to another location, such as Azure Storage and Log Analytics.

>

>To retrieve NAT gateway metrics, use the metrics REST API.

### How do I interpret metrics charts?

Refer to [troubleshooting metrics charts](/azure/azure-monitor/essentials/metrics-troubleshoot) if you run into issues with creating, customizing or interpreting charts in Azure metrics explorer.

## Next steps

* Learn about [Azure NAT Gateway](nat-overview.md)

* Learn about [NAT gateway resource](nat-gateway-resource.md)

* Learn about [Azure Monitor](/azure/azure-monitor/overview)

* Learn about [troubleshooting NAT gateway resources](troubleshoot-nat.md).

* Learn about [troubleshooting NAT gateway connectivity](/azure/nat-gateway/troubleshoot-nat-connectivity)


# Quickstart Create Nat Gateway V2

# Quickstart: Create a StandardV2 NAT gateway

In this quickstart, learn how to create a network address translation (NAT) gateway for the StandardV2 SKU of Azure NAT Gateway by using the Azure portal, Azure PowerShell, or the Azure CLI. The Azure NAT Gateway service provides scalable outbound connectivity for virtual machines in Azure.

## Prerequisites

### [Portal](#tab/portal)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

### [PowerShell](#tab/powershell)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- Azure Cloud Shell or Azure PowerShell.

The steps in this quickstart run the Azure PowerShell cmdlets interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the commands in Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code, and then paste it into Cloud Shell to run it. You can also run Cloud Shell from within the Azure portal.

You can also [install Azure PowerShell locally](/powershell/azure/install-azure-powershell) to run the cmdlets. The steps in this article require Azure PowerShell module version 5.4.1 or later. To find your installed version, run `Get-Module -ListAvailable Az`. If you need to upgrade, see [`Update-AzModule`](/powershell/module/az.tools.installer/update-azmodule).

### [CLI](#tab/cli)

- [!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

- To run CLI reference commands locally, [install the Azure CLI](/cli/azure/install-azure-cli). If you're running on Windows or macOS, consider [running the Azure CLI in a Docker container](/cli/azure/run-azure-cli-docker).

- If you're using a local installation, sign in to the Azure CLI by using the [`az login`](/cli/azure/reference-index#az-login) command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see [Authenticate to Azure using Azure CLI](/cli/azure/authenticate-azure-cli).

- When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see [Use and manage extensions with the Azure CLI](/cli/azure/azure-cli-extensions-overview).

- To find the version and dependent libraries that are installed, run [`az version`](/cli/azure/reference-index?#az-version). To upgrade to the latest version, run [`az upgrade`](/cli/azure/reference-index?#az-upgrade).

---

## Create a resource group

Create a resource group to contain all resources for this quickstart.

### [Portal](#tab/portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal, enter **Resource group**. Select **Resource groups** in the search results.

1. Select **+ Create**.

1. On the **Basics** tab of **Create a resource group**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| **Subscription** | Select your subscription. |

| **Resource group** | Enter **test-rg**. |

| **Region** | Enter **East US**. |

1. Select **Review + create**.

1. Select **Create**.

### [PowerShell](#tab/powershell)

Create a resource group by using [`New-AzResourceGroup`](/powershell/module/az.resources/new-azresourcegroup). An Azure resource group is a logical container into which Azure resources are deployed and managed.

The following example creates a resource group named `test-rg` in the `eastus` location:

```azurepowershell-interactive

$rsg = @{

Name = 'test-rg'

Location = 'eastus'

}

New-AzResourceGroup @rsg

```

### [CLI](#tab/cli)

Create a resource group by using [`az group create`](/cli/azure/group#az-group-create). An Azure resource group is a logical container into which Azure resources are deployed and managed.

The following example creates a resource group named `test-rg` in the `eastus` location:

```azurecli-interactive

az group create \

--name test-rg \

--location eastus

```

---

## Create the NAT gateway

In this section, create the NAT gateway and supporting resources.

Azure NAT Gateway supports multiple deployment options for IP addresses and redundancy configurations to meet your connectivity and availability requirements.

### Zone-redundant IPv4 address

#### [Portal](#tab/portal)

1. Sign in to the [Azure preview portal](https://preview.portal.azure.com).

1. In the search box at the top of the portal, enter **Public IP address**. Select **Public IP addresses** in the search results.

1. Select **Create**.

1. In **Create public IP address**, enter the following information.

| Setting | Value |

| ------- | ----- |

| **Project details** | |

| **Subscription** | Select your subscription. |

| **Resource group** | Select your resource group. This example uses **test-rg**. |

| **Instance details** | |

| **Region** | Select a region. This example uses **East US**. |

| **Configuration details** | |

| **Name** | Enter **public-ip-nat**. |

| **IP version** | Select **IPv4**. |

| **SKU** | Select **Standard V2 (For use with Standard V2 NAT Gateway)**. |

| **Tier** | Select **Regional**. |

1. Select **Review + create**, and then select **Create**.

1. In the search box at the top of the Azure portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **Create**.

1. On the **Basics** tab of **Create network address translation (NAT) gateway**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| **Project details** | |

| **Subscription** | Select your subscription. |

| **Resource group** | Select **test-rg** or your resource group. |

| **Instance details** | |

| **NAT gateway name** | Enter **nat-gateway**. |

| **Region** | Select your region. This example uses **East US**. |

| **SKU** | Select **Standard V2**. |

| **TCP idle timeout (minutes)** | Leave the default of **4**. |

1. Select **Next**.

1. On the **Outbound IP** tab, select **+ Add public IP addresses or prefixes**.

1. In **Add public IP addresses or prefixes**, select **Public IP addresses**. Select the public IP address that you created earlier, **public-ip-nat**.

1. Select **Save**.

1. Select **Review + create**, and then select **Create**.

#### [PowerShell](#tab/powershell)

Create a zone-redundant IPv4 public IP address for the NAT gateway by using [`New-AzPublicIpAddress`](/powershell/module/az.network/new-azpublicipaddress).

```azurepowershell-interactive

## Create a public IP address for the NAT gateway ##

$ip = @{

Name = 'public-ip-nat'

ResourceGroupName = 'test-rg'

Location = 'eastus'

Sku = 'StandardV2'

AllocationMethod = 'Static'

IpAddressVersion = 'IPv4'

Zone = 1,2,3

}

$publicIPIPv4 = New-AzPublicIpAddress @ip

```

Create the NAT gateway resource by using [`New-AzNatGateway`](/powershell/module/az.network/new-aznatgateway).

```azurepowershell

## Create the NAT gateway resource ##

$nat = @{

ResourceGroupName = 'test-rg'

Name = 'nat-gateway'

IdleTimeoutInMinutes = '4'

Sku = 'StandardV2'

Location = 'eastus'

PublicIpAddress = $publicIPIPv4

Zone = 1,2,3

}

$natGateway = New-AzNatGateway @nat

```

#### [CLI](#tab/cli)

Create a zone-redundant IPv4 public IP address for the NAT gateway by using [`az network public-ip create`](/cli/azure/network/public-ip#az-network-public-ip-create).

```azurecli-interactive

az network public-ip create \

--resource-group test-rg \

--name public-ip-nat \

--location eastus \

--sku StandardV2 \

--allocation-method Static \

--version IPv4 \

--zone 1 2 3

```

Create the NAT gateway resource by using [`az network nat gateway create`](/cli/azure/network/nat/gateway#az-network-nat-gateway-create).

```azurecli-interactive

az network nat gateway create \

--resource-group test-rg \

--name nat-gateway \

--location eastus \

--public-ip-addresses public-ip-nat \

--idle-timeout 4 \

--sku StandardV2 \

--zone 1 2 3

```

---

### Zone-redundant IPv4 prefix

#### [Portal](#tab/portal)

1. Sign in to the [Azure preview portal](https://preview.portal.azure.com).

1. In the search box at the top of the portal, enter **Public IP prefix**. Select **Public IP Prefixes** in the search results.

1. Select **Create**.

1. On the **Basics** tab of **Create a public IP prefix**, enter the following information.

| Setting | Value |

| ------- | ----- |

| **Project details** | |

| **Subscription** | Select your subscription. |

| **Resource group** | Select your resource group. This example uses **test-rg**. |

| **Instance details** | |

| **Name** | Enter **public-ip-prefix-nat**. |

| **Region** | Select your region. This example uses **East US**. |

| **Sku** | Select **Standard V2**. |

| **IP version** | Select **IPv4**. |

| **Prefix ownership** | Select **Microsoft owned**. |

| **Prefix size** | Select a prefix size. This example uses **/28 (16 addresses)**. |

1. Select **Review + create**, and then select **Create**.

1. In the search box at the top of the Azure portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **Create**.

1. On the **Basics** tab of **Create network address translation (NAT) gateway**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| **Project details** | |

| **Subscription** | Select your subscription. |

| **Resource group** | Select **test-rg** or your resource group. |

| **Instance details** | |

| **NAT gateway name** | Enter **nat-gateway**. |

| **Region** | Select your region. This example uses **East US**. |

| **SKU** | Select **Standard V2**. |

| **TCP idle timeout (minutes)** | Leave the default of **4**. |

1. Select **Next**.

1. On the **Outbound IP** tab, select **+ Add public IP addresses or prefixes**.

1. In **Add public IP addresses or prefixes**, select **Public IP prefixes**. Select the public IP prefix that you created earlier, **public-ip-prefix-nat**.

1. Select **Review + create**, and then select **Create**.

#### [PowerShell](#tab/powershell)

Create a zone-redundant IPv4 public IP prefix for the NAT gateway by using [`New-AzPublicIpPrefix`](/powershell/module/az.network/new-azpublicipprefix).

```azurepowershell

## Create a public IP prefix for the NAT gateway ##

$ip = @{

Name = 'public-ip-prefix-nat'

ResourceGroupName = 'test-rg'

Location = 'eastus'

Sku = 'StandardV2'

PrefixLength = '31'

IpAddressVersion = 'IPv4'

Zone = 1,2,3

}

$publicIPIPv4prefix = New-AzPublicIpPrefix @ip

```

Create the NAT gateway resource by using [`New-AzNatGateway`](/powershell/module/az.network/new-aznatgateway).

```azurepowershell

## Create the NAT gateway resource ##

$nat = @{

ResourceGroupName = 'test-rg'

Name = 'nat-gateway'

IdleTimeoutInMinutes = '4'

Sku = 'StandardV2'

Location = 'eastus'

PublicIpPrefix = $publicIPIPv4prefix

Zone = 1,2,3

}

$natGateway = New-AzNatGateway @nat

```

#### [CLI](#tab/cli)

Create a zone-redundant IPv4 public IP prefix for the NAT gateway by using [`az network public-ip prefix create`](/cli/azure/network/public-ip/prefix#az-network-public-ip-prefix-create).

```azurecli-interactive

az network public-ip prefix create \

--resource-group test-rg \

--name public-ip-prefix-nat \

--location eastus \

--length 31 \

--sku StandardV2 \

--version IPv4 \

--zone 1 2 3

```

Create the NAT gateway resource by using [`az network nat gateway create`](/cli/azure/network/nat/gateway#az-network-nat-gateway-create).

```azurecli-interactive

az network nat gateway create \

--resource-group test-rg \

--name nat-gateway \

--location eastus \

--public-ip-prefixes public-ip-prefix-nat \

--idle-timeout 4 \

--sku StandardV2 \

--zone 1 2 3

```

---

## Create virtual network and subnet configurations

Create the virtual network and subnets that you need for this quickstart.

### [Portal](#tab/portal)

1. In the search box at the top of the Azure portal, enter **Virtual network**. Select **Virtual networks** in the search results.

1. Select **Create**.

1. On the **Basics** tab of **Create virtual network**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| **Project details** | |

| **Subscription** | Select your subscription. |

| **Resource group** | Select **test-rg** or your resource group. |

| **Instance details** | |

| **Name** | Enter **vnet-1**. |

| **Region** | Select your region. This example uses **East US**. |

1. Select the **IP Addresses** tab, or select **Next** > **Next**.

1. In **Subnets**, select the **default** subnet.

1. In **Edit subnet**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| **Subnet purpose** | Leave the default. |

| **Name** | Enter **subnet-1**. |

| **Private subnet** | |

| **Enable private subnet (no default outbound access)** | Select the checkbox. |

| **Security** | |

| **NAT gateway** | Select **nat-gateway**. |

1. Select **Save**.

1. Select **+ Add a subnet**.

1. In **Add a subnet**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| **Subnet purpose** | Select **Azure Bastion**. |

1. Leave the rest of the settings as default, and then select **Add**.

1. Select **Review + create**, and then select **Create**.

### [PowerShell](#tab/powershell)

Create the subnet configurations by using [`New-AzVirtualNetworkSubnetConfig`](/powershell/module/az.network/new-azvirtualnetworksubnetconfig). Create the virtual network by using [`New-AzVirtualNetwork`](/powershell/module/az.network/new-azvirtualnetwork).

```azurepowershell

## Create the subnet configuration and associate the NAT gateway with the subnet ##

$subnet = @{

Name = 'subnet-1'

AddressPrefix = '10.0.0.0/24'

NatGateway = $natGateway

DefaultOutboundAccess = $false

}

$subnetConfig = New-AzVirtualNetworkSubnetConfig @subnet

## Create the Azure Bastion subnet ##

$bastsubnet = @{

Name = 'AzureBastionSubnet'

AddressPrefix = '10.0.1.0/26'

}

$bastsubnetConfig = New-AzVirtualNetworkSubnetConfig @bastsubnet

## Create the virtual network ##

$net = @{

Name = 'vnet-1'

ResourceGroupName = 'test-rg'

Location = 'eastus'

AddressPrefix = '10.0.0.0/16'

Subnet = $subnetConfig,$bastsubnetConfig

}

$vnet = New-AzVirtualNetwork @net

```

### [CLI](#tab/cli)

Create the virtual network by using [`az network vnet create`](/cli/azure/network/vnet#az-network-vnet-create). Create and configure the subnet by using [`az network vnet subnet create`](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-create) and [`az network vnet subnet update`](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-update).

```azurecli-interactive

## Create the virtual network ##

az network vnet create \

--resource-group test-rg \

--name vnet-1 \

--location eastus \

--address-prefix 10.0.0.0/16 \

--subnet-name subnet-1 \

--subnet-prefix 10.0.0.0/24

## Associate the NAT gateway with the subnet and disable default outbound access ##

az network vnet subnet update \

--resource-group test-rg \

--vnet-name vnet-1 \

--name subnet-1 \

--nat-gateway nat-gateway \

--default-outbound false

## Create the Azure Bastion subnet ##

az network vnet subnet create \

--resource-group test-rg \

--vnet-name vnet-1 \

--name AzureBastionSubnet \

--address-prefix 10.0.1.0/26

```

---

## Create an Azure Bastion host

Create an Azure Bastion host to securely connect to the virtual machine.

### [Portal](#tab/portal)

1. In the search box at the top of the Azure portal, enter **Bastion**. Select **Bastions** in the search results.

1. Select **Create**.

1. On the **Basics** tab of **Create a Bastion**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| **Project details** | |

| **Subscription** | Select your subscription. |

| **Resource group** | Select **test-rg** or your resource group. |

| **Instance details** | |

| **Name** | Enter **bastion**. |

| **Region** | Select your region. This example uses **East US**. |

| **Tier** | Select **Developer**. |

| **Virtual network** | Select **vnet-1**. |

| **Subnet** | Select **AzureBastionSubnet**. |

1. Select **Review + create**, and then select **Create**.

### [PowerShell](#tab/powershell)

Create the Azure Bastion host by using [`New-AzBastion`](/powershell/module/az.network/new-azbastion).

```azurepowershell

## Create a public IP address for the Azure Bastion host ##

$ip = @{

Name = 'public-ip-bastion'

ResourceGroupName = 'test-rg'

Location = 'eastus'

Sku = 'Standard'

AllocationMethod = 'Static'

Zone = 1,2,3

}

$publicipbastion = New-AzPublicIpAddress @ip

## Create the Azure Bastion host ##

$bastion = @{

Name = 'bastion'

ResourceGroupName = 'test-rg'

PublicIpAddressRgName = 'test-rg'

PublicIpAddressName = 'public-ip-bastion'

VirtualNetworkRgName = 'test-rg'

VirtualNetworkName = 'vnet-1'

Sku = 'Basic'

}

New-AzBastion @bastion

```

### [CLI](#tab/cli)

Create a public IP address for the Azure Bastion host by using [`az network public-ip create`](/cli/azure/network/public-ip#az-network-public-ip-create). Create the Azure Bastion host by using [`az network bastion create`](/cli/azure/network/bastion#az-network-bastion-create).

```azurecli-interactive

## Create a public IP address for the Azure Bastion host ##

az network public-ip create \

--resource-group test-rg \

--name public-ip-bastion \

--location eastus \

--sku Standard \

--allocation-method Static \

--zone 1 2 3

## Create the Azure Bastion host ##

az network bastion create \

--resource-group test-rg \

--name bastion \

--location eastus \

--vnet-name vnet-1 \

--public-ip-address public-ip-bastion \

--sku Basic

```

---

The Azure Bastion host can take several minutes to deploy. Wait for the bastion host to deploy before you move on to the next section.

## Create a virtual machine

In this section, you create a virtual machine to test the NAT gateway and verify the public IP address of the outbound connection.

The following command creates Secure Shell (SSH) keys for authentication. You need the private key later to sign in to the virtual machine through Azure Bastion.

The username and password credentials are required for the command. You don't use the password to sign in to the virtual machine.

### [Portal](#tab/portal)

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **Create** > **Virtual machine**.

1. In **Create a virtual machine**, enter or select the following information on the **Basics** tab.

| Setting | Value |

| ------- | ----- |

| **Project details** | |

| **Subscription** | Select your subscription. |

| **Resource group** | Select **test-rg** or your resource group. |

| **Instance details** | |

| **Virtual machine name** | Enter **vm-1**. |

| **Region** | Select your region. This example uses **East US**. |

| **Availability options** | Leave the default of **No infrastructure redundancy required**. |

| **Security type** | Select **Standard**. |

| **Image** | Select **Ubuntu Server 24.04 LTS - Gen2**. |

| **Size** | Select a size. |

| **Authentication type** | Select **SSH public key**. |

| **Username** | Enter a username of your choice. You need this username to sign in to the virtual machine later. |

| **SSH public key source** | Select **Generate new key pair**. |

| **Key pair name** | Enter **ssh-key**. |

| **Public inbound ports** | Select **None**. |

1. Select **Next: Disks**, and then select **Next: Networking**.

1. On the **Networking** tab, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| **Network interface** | |

| **Virtual network** | Select **vnet-1**. |

| **Subnet** | Select **subnet-1**. |

| **Public IP** | Select **None**. |

| **NIC network security group** | Select **Basic**. |

| **Public inbound ports** | Leave the default of **None**. |

1. Select **Review + create**, and then select **Create**.

### [PowerShell](#tab/powershell)

Create a username and password for the virtual machine by using [`Get-Credential`](/powershell/module/microsoft.powershell.security/get-credential). Create a network interface for the virtual machine by using [`New-AzNetworkInterface`](/powershell/module/az.network/new-aznetworkinterface). Create the virtual machine configuration by using [`New-AzVMConfig`](/powershell/module/az.compute/new-azvmconfig). Create the virtual machine by using [`New-AzVM`](/powershell/module/az.compute/new-azvm).

```azurepowershell-interactive

## Get credentials for the virtual machine ##

$cred = Get-Credential

## Create the network interface for the virtual machine ##

$nic = @{

Name = "nic-1"

ResourceGroupName = 'test-rg'

Location = 'eastus'

Subnet = $vnet.Subnets[0]

}

$nicVM = New-AzNetworkInterface @nic

## Create the virtual machine configuration ##

$vmsz = @{

VMName = 'vm-1'

VMSize = 'Standard_DS1_v2'

}

$vmos = @{

ComputerName = 'vm-1'

Credential = $cred

DisablePasswordAuthentication = $true

}

$vmimage = @{

PublisherName = 'Canonical'

Offer = '0001-com-ubuntu-server-jammy'

Skus = '22_04-lts-gen2'

Version = 'latest'

}

$vmConfig = New-AzVMConfig @vmsz `

| Set-AzVMOperatingSystem @vmos -Linux `

| Set-AzVMSourceImage @vmimage `

| Add-AzVMNetworkInterface -Id $nicVM.Id

## Create the virtual machine ##

$vm = @{

ResourceGroupName = 'test-rg'

Location = 'eastus'

VM = $vmConfig

SshKeyName = 'ssh-key'

}

New-AzVM @vm -GenerateSshKey

```

### [CLI](#tab/cli)

Create a network interface for the virtual machine by using [`az network nic create`](/cli/azure/network/nic#az-network-nic-create). Create the virtual machine by using [`az vm create`](/cli/azure/vm#az-vm-create).

```azurecli-interactive

## Create a network interface for the virtual machine ##

az network nic create \

--resource-group test-rg \

--name nic-1 \

--vnet-name vnet-1 \

--subnet subnet-1

## Create the virtual machine ##

az vm create \

--resource-group test-rg \

--name vm-1 \

--location eastus \

--nics nic-1 \

--image Canonical:0001-com-ubuntu-server-jammy:22_04-lts-gen2:latest \

--size Standard_DS1_v2 \

--admin-username azureuser \

--generate-ssh-keys \

--public-ip-address ""

```

---

Wait for the virtual machine creation to finish before you move on to the next section.

> [!IMPORTANT]

> Ensure that you download the SSH private key to the virtual machine. You need the private key to sign in to the virtual machine through Azure Bastion.

## Test the NAT gateway

To test the NAT gateway, you first discover the public IP of the NAT gateway. You then connect to the test virtual machine and verify the outbound connection through the NAT gateway's public IP.

1. In the search box at the top of the portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **nat-gateway**.

1. Expand **Settings**, and then select **Outbound IP**.

1. Make note of the outbound IP address. Individual public IPs and public IP prefixes configured for the NAT gateway appear here.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **vm-1**.

1. On the **Overview** page, select **Connect**, and then select **Connect via Bastion**.

1. In the **Authentication** list, select **SSH Private Key From Local File**.

1. In **Username**, enter the username that you entered during virtual machine creation.

1. In **Local File**, select the SSH private key file that you downloaded earlier.

1. Select **Connect**.

1. In the Bash prompt, enter the following command:

```bash

curl ifconfig.me

```

1. Verify that the IP address returned by the command matches the public IP address of the NAT gateway that you noted earlier.

```output

azureuser@vm-1:~$ curl ifconfig.me

203.0.113.0.25

```

## Clean up resources

### [Portal](#tab/portal)

[!INCLUDE [portal-clean-up.md](~/reusable-content/ce-skilling/azure/includes/portal-clean-up.md)]

### [PowerShell](#tab/powershell)

If you no longer need this application, delete the virtual network, virtual machine, and NAT gateway by using the following command:

```azurepowershell-interactive

Remove-AzResourceGroup -Name 'test-rg' -Force

```

### [CLI](#tab/cli)

If you no longer need this application, delete the virtual network, virtual machine, and NAT gateway by using the following command:

```azurecli-interactive

az group delete \

--name test-rg \

--yes \

--no-wait

```

---

## Related content

- [Azure NAT Gateway overview](nat-overview.md)

- [NAT gateway resource](nat-gateway-resource.md)


# Nat Sku

# Azure NAT Gateway SKUs

Azure NAT Gateway has two stock-keeping units (SKUs): Standard and StandardV2. This article provides an overview of these SKUs and their differences.

## SKU comparison

| Category | Feature | Standard | StandardV2 |

| -------- | ------- | ---------- | -------- |

| Reliability | Availability zones | Not supported | Supported |

| Functionality | Source network address translation (SNAT) | Supported | Supported |

| | Dynamic port allocation | Supported | Supported |

| | Idle timeout timer | Supported | Supported |

| | Port reuse timer | Supported | Supported |

| | Protocols | TCP, UDP | TCP, UDP, ICMP Echo Request and Reply (ping) |

| | Public IP version | IPv4 | IPv4, IPv6 |

| | Attach point | Subnet | Subnet |

| Scalability | Public IP addresses | 16 IPv4 addresses | 16 IPv4 addresses, 16 IPv6 addresses |

| | Public IP prefixes | /28 IPv4 prefix | /28 IPv4 prefix, /124 IPv6 prefix |

| | Virtual networks | 1 | 1 |

| | Subnets | 800 | 800 |

| Monitoring | Metrics | Supported | Supported |

| Limits | Bandwidth | 50 Gbps per NAT gateway | 100 Gbps per NAT gateway, 1 Gbps per connection |

| | Packets per second | 5 million packets per second | 10 million packets per second, 100,000 packets per second per connection |

| | Connections per IP per destination | 50,000 | 50,000 |

| | Total connections | 2 million | 2 million |

## Pricing and SLA

Standard and StandardV2 NAT gateways are the same price. For more information, see [Azure NAT Gateway pricing](https://azure.microsoft.com/pricing/details/azure-nat-gateway/).

For information on the service-level agreement (SLA), see the [Microsoft SLAs for online services](https://azure.microsoft.com/support/legal/sla/virtual-network-nat/v1_0/).

## Standard SKU features

The Standard SKU is a zonal resource. It's deployed into a specific availability zone and is resilient within that zone.

You can attach a Standard NAT gateway to individual subnets within the same virtual network in order to provide scalable outbound connectivity to the internet.

## StandardV2 SKU features

### Zone redundancy

A StandardV2 NAT gateway is *zone redundant* by default. It automatically spans multiple availability zones in a region to provide continued outbound connectivity even if one zone becomes unavailable.

For more information, see [Reliability in Azure NAT Gateway](/azure/reliability/reliability-nat-gateway).

### Performance

A StandardV2 NAT gateway supports up to 100 Gbps of bandwidth and can process up to 10 million packets per second. On a per-connection basis, a StandardV2 NAT gateway supports 1 Gbps per connection and 100,000 packets per second.

### IPv6 support

You can attach a StandardV2 NAT gateway to 16 IPv6 public IPs and 16 IPv4 public IPs simultaneously in order to provide highly scalable dual-stack outbound connectivity to the internet.

### Flow logs

A StandardV2 NAT gateway supports flow logs through Azure Monitor. Flow logs provide visibility into the traffic that flows through the NAT gateway. For more information, see [Manage StandardV2 NAT gateway flow logs](./nat-gateway-flow-logs.md).

### Known limitations

* The StandardV2 SKU requires StandardV2 public IP addresses and prefixes. Standard public IPs aren't supported.

* You can't upgrade the Standard SKU to the StandardV2 SKU. You must deploy a StandardV2 NAT gateway to replace the Standard NAT gateway.

* Custom IP prefixes (bring-your-own-IP public IPs) aren't supported with the StandardV2 SKU. Only StandardV2 Azure public IPs are supported.

* The following regions don't support StandardV2 NAT gateways:

* Canada East

* Chile Central

* Indonesia Central

* Israel Northwest

* Malaysia West

* Qatar Central

* Sweden South

* West India

* Deployment of a StandardV2 NAT gateway as a managed NAT gateway for Azure Kubernetes Service (AKS) is now in preview. A StandardV2 NAT gateway can also be configured as a user-assigned NAT gateway for AKS workloads. For more information, see [Create a NAT gateway for your AKS cluster](/azure/aks/nat-gateway).

### Known issues

* A StandardV2 NAT gateway disrupts outbound connections made with load balancer outbound rules for IPv6 traffic only. If you see disruption to outbound connectivity for IPv6 outbound traffic with load balancer outbound rules, remove the StandardV2 NAT gateway from the subnet or virtual network. Then use either:

* Load balancer outbound rules to provide outbound connectivity for both IPv4 and IPv6 traffic

* A Standard NAT gateway to provide outbound connectivity for IPv4 traffic and load balancer outbound rules for IPv6 traffic

* Outbound connections that use a load balancer, Azure Firewall, or VM instance-level public IPs might be interrupted when you add a StandardV2 NAT gateway to a subnet. All net new outbound connections use the StandardV2 NAT gateway.

## Related content

* [Deploy a Standard NAT gateway](./quickstart-create-nat-gateway.md) for single-zone deployments.

* [Deploy a StandardV2 NAT gateway](./quickstart-create-nat-gateway-v2.md) to provide a zone-resilient network architecture.


# Tutorial Nat Gateway Load Balancer Public Portal

# Tutorial: Integrate a NAT gateway with a public load balancer using the Azure portal

In this tutorial, you learn how to integrate a NAT gateway with a public load balancer.

By default, an Azure Standard Load Balancer is secure. Outbound connectivity is explicitly defined by enabling outbound SNAT (Source Network Address Translation). SNAT is enabled in a load-balancing rule or outbound rules.

The NAT gateway integration replaces the need for outbound rules for backend pool outbound SNAT.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a NAT gateway

> * Create an Azure Load Balancer

> * Create two virtual machines for the backend pool of the Azure Load Balancer

> * Validate outbound connectivity of the virtual machines in the load balancer backend pool

## Prerequisites

An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Create a resource group

Create a resource group to contain all resources for this quickstart.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal enter **Resource group**. Select **Resource groups** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab of **Create a resource group**, enter, or select the following information.

| Setting | Value |

| ------- | ----- |

| Subscription | Select your subscription|

| Resource group | test-rg |

| Region | **East US 2** |

1. Select **Review + create**.

1. Select **Create**.

## Create the virtual network

1. In the search box at the top of the Azure portal, enter **Virtual network**. Select **Virtual networks** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create virtual network**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| Name | Enter **vnet-1**. |

| Region | Select your region. This example uses **East US 2**. |

1. Select the **IP Addresses** tab, or select **Next: Security**, then **Next: IP Addresses**.

1. In **Subnets** select the **default** subnet.

1. Enter or select the following information in **Edit subnet**.

| Setting | Value |

| ------- | ----- |

| Subnet purpose | Leave the default. |

| Name | Enter **subnet-1**. |

1. Leave the rest of the settings as default, then select **Save**.

1. Select **+ Add a subnet**.

1. In **Add a subnet** enter or select the following information.

| Setting | Value |

| ------- | ----- |

| Subnet purpose | Select **Azure Bastion**. |

1. Leave the rest of the settings as default, then select **Add**.

1. Select **Review + create**, then select **Create**.

## Create Azure Bastion host

Create an Azure Bastion host to securely connect to the virtual machine.

1. In the search box at the top of the Azure portal, enter **Bastion**. Select **Bastions** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create a Bastion**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| Name | Enter **bastion**. |

| Region | Select your region. This example uses **East US 2**. |

| Tier | Select **Developer**. |

| Virtual network | Select **vnet-1**. |

| Subnet | Select **AzureBastionSubnet**. |

1. Select **Review + create**, then select **Create**.

## Create a NAT gateway

1. In the search box at the top of the Azure portal, enter **Public IP address**. Select **Public IP addresses** in the search results.

1. Select **Create**.

1. Enter the following information in **Create public IP address**.

| Setting | Value |

| ------- | ----- |

| Subscription | Select your subscription. |

| Resource group | Select your resource group. The example uses **test-rg**. |

| Region | Select a region. This example uses **East US 2**. |

| Name | Enter **public-ip-nat**. |

| IP version | Select **IPv4**. |

| SKU | Select **Standard**. |

| Availability zone | Select **Zone-redundant**. |

| Tier | Select **Regional**. |

1. Select **Review + create** and then select **Create**.

1. In the search box at the top of the Azure portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create network address translation (NAT) gateway**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| NAT gateway name | Enter **nat-gateway**. |

| Region | Select your region. This example uses **East US 2**. |

| SKU | Select **Standard**. |

| TCP idle timeout (minutes) | Leave the default of **4**. |

1. Select **Next**.

1. In the **Outbound IP** tab, select **+ Add public IP addresses or prefixes**.

1. In **Add public IP addresses or prefixes**, select **Public IP addresses**. Select the public IP address you created earlier, **public-ip-nat**.

1. Select **Next**.

1. In the **Networking** tab, in **Virtual network**, select **vnet-1**.

1. Leave the checkbox for **Default to all subnets** unchecked.

1. In **Select specific subnets**, select **subnet-1**.

1. Select **Review + create**, then select **Create**.

[!INCLUDE [load-balancer-public-create-http.md](../../includes/load-balancer-public-create-http.md)]

[!INCLUDE [create-two-virtual-machines-linux-load-balancer.md](../../includes/create-two-virtual-machines-linux-load-balancer.md)]

## Test NAT gateway

In this section, you test the NAT gateway. You first discover the public IP of the NAT gateway. You then connect to the test virtual machine and verify the outbound connection through the NAT gateway.

1. In the search box at the top of the portal, enter **Public IP**. Select **Public IP addresses** in the search results.

1. Select **public-ip-nat**.

1. Make note of the public IP address:

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **vm-1**.

1. On the **Overview** page, select **Connect**, then select the **Bastion** tab.

1. Select **Use Bastion**.

1. Enter the username and password entered during VM creation. Select **Connect**.

1. In the bash prompt, enter the following command:

```bash

curl ifconfig.me

```

1. Verify the IP address returned by the command matches the public IP address of the NAT gateway.

```output

azureuser@vm-1:~$ curl ifconfig.me

203.0.113.25

```

1. Close the bastion connection to **vm-1**.

[!INCLUDE [portal-clean-up.md](~/reusable-content/ce-skilling/azure/includes/portal-clean-up.md)]

## Next steps

For more information on Azure NAT Gateway, see:

> [!div class="nextstepaction"]

> [Azure NAT Gateway overview](nat-overview.md)


# Tutorial Nat Gateway Load Balancer Internal Portal

# Tutorial: Integrate a NAT gateway with an internal load balancer using the Azure portal

In this tutorial, you learn how to integrate a NAT gateway with an internal load balancer.

By default, an Azure Standard Load Balancer is secure. Outbound connectivity is explicitly defined by enabling outbound SNAT (Source Network Address Translation).

SNAT is enabled for an internal backend pool via another public load balancer, network routing, or a public IP defined on a virtual machine.

The NAT gateway integration replaces the need for the deployment of a public load balancer, network routing, or a public IP defined on a virtual machine in the backend pool.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create an Azure Load Balancer

> * Create two virtual machines for the backend pool of the Azure Load Balancer

> * Create a NAT gateway

> * Validate outbound connectivity of the virtual machines in the load balancer backend pool

## Prerequisites

An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Create a resource group

Create a resource group to contain all resources for this quickstart.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal enter **Resource group**. Select **Resource groups** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab of **Create a resource group**, enter, or select the following information.

| Setting | Value |

| ------- | ----- |

| Subscription | Select your subscription|

| Resource group | test-rg |

| Region | **East US 2** |

1. Select **Review + create**.

1. Select **Create**.

## Create the virtual network

1. In the search box at the top of the Azure portal, enter **Virtual network**. Select **Virtual networks** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create virtual network**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| Name | Enter **vnet-1**. |

| Region | Select your region. This example uses **East US 2**. |

1. Select the **IP Addresses** tab, or select **Next: Security**, then **Next: IP Addresses**.

1. In **Subnets** select the **default** subnet.

1. Enter or select the following information in **Edit subnet**.

| Setting | Value |

| ------- | ----- |

| Subnet purpose | Leave the default. |

| Name | Enter **subnet-1**. |

1. Leave the rest of the settings as default, then select **Save**.

1. Select **+ Add a subnet**.

1. In **Add a subnet** enter or select the following information.

| Setting | Value |

| ------- | ----- |

| Subnet purpose | Select **Azure Bastion**. |

1. Leave the rest of the settings as default, then select **Add**.

1. Select **Review + create**, then select **Create**.

## Create Azure Bastion host

Create an Azure Bastion host to securely connect to the virtual machine.

1. In the search box at the top of the Azure portal, enter **Bastion**. Select **Bastions** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create a Bastion**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| Name | Enter **bastion**. |

| Region | Select your region. This example uses **East US 2**. |

| Tier | Select **Developer**. |

| Virtual network | Select **vnet-1**. |

| Subnet | Select **AzureBastionSubnet**. |

1. Select **Review + create**, then select **Create**.

## Create a NAT gateway

1. In the search box at the top of the Azure portal, enter **Public IP address**. Select **Public IP addresses** in the search results.

1. Select **Create**.

1. Enter the following information in **Create public IP address**.

| Setting | Value |

| ------- | ----- |

| Subscription | Select your subscription. |

| Resource group | Select your resource group. The example uses **test-rg**. |

| Region | Select a region. This example uses **East US 2**. |

| Name | Enter **public-ip-nat**. |

| IP version | Select **IPv4**. |

| SKU | Select **Standard**. |

| Availability zone | Select **Zone-redundant**. |

| Tier | Select **Regional**. |

1. Select **Review + create** and then select **Create**.

1. In the search box at the top of the Azure portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create network address translation (NAT) gateway**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| NAT gateway name | Enter **nat-gateway**. |

| Region | Select your region. This example uses **East US 2**. |

| SKU | Select **Standard**. |

| TCP idle timeout (minutes) | Leave the default of **4**. |

1. Select **Next**.

1. In the **Outbound IP** tab, select **+ Add public IP addresses or prefixes**.

1. In **Add public IP addresses or prefixes**, select **Public IP addresses**. Select the public IP address you created earlier, **public-ip-nat**.

1. Select **Next**.

1. In the **Networking** tab, in **Virtual network**, select **vnet-1**.

1. Leave the checkbox for **Default to all subnets** unchecked.

1. In **Select specific subnets**, select **subnet-1**.

1. Select **Review + create**, then select **Create**.

[!INCLUDE [load-balancer-internal-create-http.md](../../includes/load-balancer-internal-create-http.md)]

[!INCLUDE [create-two-virtual-machines-linux-load-balancer.md](../../includes/create-two-virtual-machines-linux-load-balancer.md)]

## Test NAT gateway

In this section, you test the NAT gateway. You first discover the public IP of the NAT gateway. You then connect to the test virtual machine and verify the outbound connection through the NAT gateway.

1. In the search box at the top of the portal, enter **Public IP**. Select **Public IP addresses** in the search results.

1. Select **public-ip-nat**.

1. Make note of the public IP address.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **vm-1**.

1. On the **Overview** page, select **Connect**, then select the **Bastion** tab.

1. Select **Use Bastion**.

1. Enter the username and password entered during virtual machine creation. Select **Connect**.

1. In the bash prompt, enter the following command.

```bash

curl ifconfig.me

```

1. Verify the IP address returned by the command matches the public IP address of the NAT gateway.

```output

azureuser@vm-1:~$ curl ifconfig.me

203.0.113.0.25

```

1. Close the bastion connection to **vm-1**.

[!INCLUDE [portal-clean-up.md](~/reusable-content/ce-skilling/azure/includes/portal-clean-up.md)]

## Next steps

For more information on Azure NAT Gateway, see:

> [!div class="nextstepaction"]

> [Azure NAT Gateway overview](nat-overview.md)


# Tutorial Migrate Outbound Nat

# Tutorial: Migrate outbound access to Azure NAT Gateway

In this tutorial, you learn how to migrate your outbound connectivity from [default outbound access](../virtual-network/ip-services/default-outbound-access.md) to a NAT gateway.

You learn how to change your outbound connectivity from load balancer outbound rules to a NAT gateway. You reuse the IP address from the outbound rule configuration for the NAT gateway.

Azure NAT Gateway is the recommended method for outbound connectivity. A NAT gateway is a fully managed and highly resilient Network Address Translation (NAT) service. A NAT gateway doesn't have the same limitations of Source Network Address Translation (SNAT) port exhaustion as default outbound access. A NAT gateway replaces the need for outbound rules in a load balancer for outbound connectivity.

> [!NOTE]

> For default outbound access replacement, StandardV2 NAT Gateway is deployed in the tutorial to ensure that you are using the zone-redundant version of NAT gateway (Standard SKU NAT Gateway is zonal). See [StandardV2 NAT Gateway](/azure/nat-gateway/nat-overview#standardv2-nat-gateway) for more details and see [known limitations](/azure/nat-gateway/nat-overview#key-limitations-of-standardv2-nat-gateway) for details on unsupported scenarios.

> [!NOTE]

> For the Load balancer outbound rule replacement, Standard SKU NAT Gateway is deployed in this tutorial and the frontend IP of the Load balancer is moved to the Standard NAT Gateway. StandardV2 NAT Gateway can be used to replace Load balancer outbound rules but can't be used with the Load balancer frontend IP. StandardV2 NAT Gateway requires new creation of a StandardV2 SKU public IP.

For more information about Azure NAT Gateway, see [What is Azure NAT Gateway?](nat-overview.md)

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Migrate default outbound access to a NAT gateway.

> * Migrate load balancer outbound connectivity and IP address to a NAT gateway.

## Prerequisites

* An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

* A standard public load balancer in your subscription. The load balancer must have a separate frontend IP address and outbound rules configured. For more information on creating an Azure Load Balancer, see [Quickstart: Create a public load balancer to load balance virtual machines using the Azure portal](../load-balancer/quickstart-load-balancer-standard-public-portal.md).

* The load balancer name used in the examples is **load-balancer**.

> [!NOTE]

> Azure NAT Gateway provides outbound connectivity for standard internal load balancers. For more information on integrating a NAT gateway with your internal load balancers, see [Tutorial: Integrate a NAT gateway with an internal load balancer using Azure portal](tutorial-nat-gateway-load-balancer-internal-portal.md).

## Create a resource group

Create a resource group to contain all resources for this tutorial.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal enter **Resource group**. Select **Resource groups** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab of **Create a resource group**, enter, or select the following information.

| Setting | Value |

| ------- | ----- |

| Subscription | Select your subscription|

| Resource group | test-rg |

| Region | **East US 2** |

1. Select **Review + create**.

1. Select **Create**.

## Migrate default outbound access

In this section, you learn how to change your outbound connectivity method from default outbound access to a NAT gateway.

1. In the search box at the top of the Azure portal, enter **Public IP address**. Select **Public IP addresses** in the search results.

1. Select **Create**.

1. Enter the following information in **Create public IP address**.

| Setting | Value |

| ------- | ----- |

| Subscription | Select your subscription. |

| Resource group | Select your resource group. The example uses **test-rg**. |

| Region | Select a region. This example uses **East US 2**. |

| Name | Enter **public-ip-nat**. |

| IP version | Select **IPv4**. |

| SKU | Select **StandardV2**. |

| Tier | Select **Regional**. |

1. Select **Review + create** and then select **Create**.

1. In the search box at the top of the Azure portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create network address translation (NAT) gateway**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| NAT gateway name | Enter **nat-gateway**. |

| Region | Select your region. This example uses **East US 2**. |

| SKU | Select **StandardV2**. |

| TCP idle timeout (minutes) | Leave the default of **4**. |

1. Select **Next**.

1. In the **Outbound IP** tab, select **+ Add public IP addresses or prefixes**.

1. In **Add public IP addresses or prefixes**, select **Public IP addresses**. Select the public IP address you created earlier, **public-ip-nat**.

1. Select **Next**.

1. In the **Networking** tab, in **Virtual network**, select your virtual network. In this example, it's **test-rg**.

1. Leave the checkbox for **Default to all subnets** unchecked.

1. In **Select specific subnets**, select your subnet. In this example, it's **subnet-1**.

1. Select **Review + create**, then select **Create**.

## Migrate load balancer outbound connectivity

In this section, you learn how to change your outbound connectivity method from outbound rules to a NAT gateway. You keep the same frontend IP address used for the outbound rules. You remove the outbound rule’s frontend IP configuration then create a NAT gateway with the same frontend IP address. A public load balancer is used throughout this section.

### Remove outbound rule frontend IP configuration

You remove the outbound rule and the associated frontend IP configuration from your load balancer. The load balancer name used in this example is **load-balancer**.

1. In the search box at the top of the portal, enter **Load balancer**. Select **Load balancers** in the search results.

1. Select **load-balancer** or your load balancer.

1. Expand **Settings**. Select **Frontend IP configuration**.

1. Note the **IP address** in **Frontend IP configuration** that you wish to migrate to a **NAT gateway**. You'll need this information in the next section. In this example, it's **frontend-ip-outbound**.

1. Select **Delete** next to the IP configuration you wish to remove. In this example, it's **frontend-ip-outbound**.

1. Select **Delete**.

1. In **Delete frontend-ip-outbound**, select the check box next to **I have read and understood that this frontend IP configuration as well as the associated resources listed above will be deleted**.

1. Select **Delete**. This procedure deletes the frontend IP configuration and the outbound rule associated with the frontend.

### Create NAT gateway

In this section, you create a NAT gateway with the IP address previously used for outbound rule and assign it to your precreated subnet within your virtual network. The subnet name for this example is **subnet-1**.

1. In the search box at the top of the Azure portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create network address translation (NAT) gateway**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| NAT gateway name | Enter **nat-gateway**. |

| Region | Select your region. This example uses **East US 2**. |

| SKU | Select **Standard**. |

| TCP idle timeout (minutes) | Leave the default of **4**. |

1. Select **Next**.

1. In the **Outbound IP** tab, select **+ Add public IP addresses or prefixes**.

1. In **Add public IP addresses or prefixes**, select **Public IP addresses**. Select the public IP address you removed from the load balancer in the previous steps. In this example, it's **public-ip-outbound**.

1. Select **Next**.

1. In the **Networking** tab, in **Virtual network**, select your virtual network. In this example, it's **test-rg**.

1. Leave the checkbox for **Default to all subnets** unchecked.

1. In **Select specific subnets**, select your subnet. In this example, it's **subnet-1**.

1. Select **Review + create**, then select **Create**.

## Next steps

In this article, you learned how to:

* Migrate default outbound access to a NAT gateway.

* Migrate load balancer outbound connectivity and IP address to a NAT gateway.

For more information about NAT gateway and the connectivity benefits it provides, see [Design virtual networks with NAT gateway](nat-gateway-resource.md).

Advance to the next article to learn how to integrate a NAT gateway with a public load balancer:

> [!div class="nextstepaction"]

> [Integrate a NAT gateway with a public load balancer using the Azure portal](tutorial-nat-gateway-load-balancer-public-portal.md)


# Tutorial Migrate Ilip Nat

# Tutorial: Migrate a virtual machine public IP address to Azure NAT Gateway

In this tutorial, you learn how to migrate your virtual machine's public IP address to a NAT gateway. You learn how to remove the IP address from the virtual machine. You reuse the IP address from the virtual machine for the NAT gateway.

Azure NAT Gateway is the recommended method for outbound connectivity. Azure NAT Gateway is a fully managed and highly resilient Network Address Translation (NAT) service. A NAT gateway doesn't have the same limitations of Source Network Address Translation (SNAT) port exhaustion as default outbound access. A NAT gateway replaces the need for a virtual machine to have a public IP address to have outbound connectivity.

For more information about Azure NAT Gateway, see [What is Azure NAT Gateway?](nat-overview.md)

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Remove the public IP address from the virtual machine.

> * Associate the public IP address from the virtual machine with a NAT gateway.

## Prerequisites

* An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

* An Azure Virtual Machine with a public IP address assigned to its network interface. For more information on creating a virtual machine with a public IP, see [Quickstart: Create a Windows virtual machine in the Azure portal](/azure/virtual-machines/windows/quick-create-portal).

* For the purposes of this article, the example virtual machine is named **vm-1**. The example public IP address is named **public-ip**.

> [!NOTE]

> Removal of the public IP address prevents direct connections to the virtual machine from the internet. RDP or SSH access won't function to the virtual machine after you complete this migration. To securely manage virtual machines in your subscription, use Azure Bastion. For more information on Azure Bastion, see [What is Azure Bastion?](../bastion/bastion-overview.md)

## Remove public IP from virtual machine

In this section, you learn how to remove the public IP address from the virtual machine.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines**.

1. In **Virtual machines**, select **vm-1** or your virtual machine.

1. In the **Overview** of **vm-1**, select **Public IP address**.

1. In **public-ip**, select the **Overview** page in the left-hand column.

1. In **Overview**, select **Dissociate**.

1. Select **Yes** in **Dissociate public IP address**.

### (Optional) Upgrade IP address

The NAT gateway resource requires a standard public IP address. In this section, you upgrade the IP you removed from the virtual machine in the previous section. If the IP address you removed is already a standard public IP, you can proceed to the next section.

1. In the search box at the top of the portal, enter **Public IP**. Select **Public IP addresses**.

1. In **Public IP addresses**, select **public-ip** or your basic IP address.

1. In the **Overview** of **public-ip**, select the IP address upgrade banner.

1. In **Upgrade to Standard SKU**, select the box next to **I acknowledge**. Select the **Upgrade** button.

1. When the upgrade is complete, proceed to the next section.

## Create NAT gateway

In this section, you create a NAT gateway with the IP address you previously removed from the virtual machine. You assign the NAT gateway to your precreated subnet within your virtual network. The subnet name for this example is **default**.

1. In the search box at the top of the Azure portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create network address translation (NAT) gateway**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| NAT gateway name | Enter **nat-gateway**. |

| Region | Select your region. This example uses **East US 2**. |

| SKU | Select **Standard**. |

| TCP idle timeout (minutes) | Leave the default of **4**. |

1. Select **Next**.

1. In the **Outbound IP** tab, select **+ Add public IP addresses or prefixes**.

1. In **Add public IP addresses or prefixes**, select **Public IP addresses**. Select the public IP address you removed from the virtual machine in the previous steps. In this example, it's **public-ip**.

1. Select **Next**.

1. In the **Networking** tab, in **Virtual network**, select your virtual network. In this example, it's **vnet-1**.

1. Leave the checkbox for **Default to all subnets** unchecked.

1. In **Select specific subnets**, select your subnet. In this example, it's **subnet-1**.

1. Select **Review + create**, then select **Create**.

## Next step

In this article, you learned how to:

* Remove a public IP address from a virtual machine.

* Create a NAT gateway and use the public IP address from the virtual machine for the NAT gateway resource.

NAT gateway provides connectivity benefits and allows any virtual machine created within this subnet to have outbound connectivity without requiring a public IP address. For more information about NAT gateway and its connectivity benefits, see the [Design virtual networks with NAT gateway](nat-gateway-resource.md) documentation.

Advance to the next article to learn how to migrate default outbound access to Azure NAT Gateway:

> [!div class="nextstepaction"]

> [Migrate outbound access to NAT gateway](tutorial-migrate-outbound-nat.md)


# Quickstart Create Nat Gateway

# Quickstart: Create a Standard NAT gateway

In this quickstart, learn how to create a network address translation (NAT) gateway for the Standard SKU of Azure NAT Gateway by using the Azure portal, Azure PowerShell, or the Azure CLI. The Azure NAT Gateway service provides scalable outbound connectivity for virtual machines in Azure.

The following diagram shows the resources that you'll create in this quickstart.

## Prerequisites

### [Portal](#tab/portal)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

### [PowerShell](#tab/powershell)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- Azure Cloud Shell or Azure PowerShell.

The steps in this quickstart run the Azure PowerShell cmdlets interactively in [Azure Cloud Shell](/azure/cloud-shell/overview). To run the commands in Cloud Shell, select **Open Cloud Shell** at the upper-right corner of a code block. Select **Copy** to copy the code, and then paste it into Cloud Shell to run it. You can also run Cloud Shell from within the Azure portal.

You can also [install Azure PowerShell locally](/powershell/azure/install-azure-powershell) to run the cmdlets. The steps in this article require Azure PowerShell module version 5.4.1 or later. To find your installed version, run `Get-Module -ListAvailable Az`. If you need to upgrade, see [`Update-AzModule`](/powershell/module/az.tools.installer/update-azmodule).

### [CLI](#tab/cli)

- [!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment-no-header.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment-no-header.md)]

---

## Create a resource group

### [Portal](#tab/portal)

1. In the search box at the top of the portal, enter **Resource groups**. Select **Resource groups** in the search results.

1. Select **+ Create**.

1. In **Create a resource group**, enter or select the following values:

| Setting | Value |

| --- | --- |

| **Project details** | |

| **Subscription** | Select your Azure subscription. |

| **Resource group** | Enter **test-rg**. |

| **Resource details** | |

| **Region** | Select **(US) East US 2**. |

1. Select **Review + create**.

1. Select **Create**.

### [PowerShell](#tab/powershell)

Create a resource group by using [`New-AzResourceGroup`](/powershell/module/az.resources/new-azresourcegroup). An Azure resource group is a logical container into which Azure resources are deployed and managed.

The following example creates a resource group named `test-rg` in the `eastus2` location:

```azurepowershell-interactive

$rsg = @{

Name = 'test-rg'

Location = 'eastus2'

}

New-AzResourceGroup @rsg

```

### [CLI](#tab/cli)

Create a resource group by using [`az group create`](/cli/azure/group#az-group-create). An Azure resource group is a logical container into which Azure resources are deployed and managed.

```azurecli-interactive

az group create \

--name test-rg \

--location eastus2

```

---

## Create a virtual network

### [Portal](#tab/portal)

The following procedure creates a virtual network with a resource subnet:

1. In the portal, search for and select **Virtual networks**.

1. On the **Virtual networks** page, select **+ Create**.

1. On the **Basics** tab of **Create virtual network**, enter or select the following information:

| Setting | Value |

| --- | --- |

| **Project details** | |

| **Subscription** | Select your subscription. |

| **Resource group** | Select **test-rg**. |

| **Instance details** | |

| **Name** | Enter **vnet-1**. |

| **Region** | Select **(US) East US 2**. |

1. Select **Next** to proceed to the **Security** tab.

1. Select **Next** to proceed to the **IP Addresses** tab.

1. In the address space box in **Subnets**, select the **default** subnet.

1. In **Edit subnet**, enter or select the following information:

| Setting | Value |

| --- | --- |

| **Subnet purpose** | Leave **Default**. |

| **Name** | Enter **subnet-1**. |

| **IPv4** | |

| **IPv4 address range** | Leave the default of **10.0.0.0/16**. |

| **Starting address** | Leave the default of **10.0.0.0**. |

| **Size** | Leave the default of **/24 (256 addresses)**. |

1. Select **Save**.

1. Select **Review + create** at the bottom of the pane. When the virtual network passes validation, select **Create**.

### [PowerShell](#tab/powershell)

Create a subnet configuration for the virtual machine subnet and an Azure Bastion host subnet by using [`New-AzVirtualNetworkSubnetConfig`](/powershell/module/az.network/new-azvirtualnetworksubnetconfig).

```azurepowershell-interactive

$subnet = @{

Name = 'subnet-1'

AddressPrefix = '10.0.0.0/24'

}

$subnetConfig = New-AzVirtualNetworkSubnetConfig @subnet

$bastsubnet = @{

Name = 'AzureBastionSubnet'

AddressPrefix = '10.0.1.0/26'

}

$bastsubnetConfig = New-AzVirtualNetworkSubnetConfig @bastsubnet

```

Create a virtual network by using [`New-AzVirtualNetwork`](/powershell/module/az.network/new-azvirtualnetwork).

```azurepowershell-interactive

$net = @{

Name = 'vnet-1'

ResourceGroupName = 'test-rg'

Location = 'eastus2'

AddressPrefix = '10.0.0.0/16'

Subnet = $subnetConfig, $bastsubnetConfig

}

$vnet = New-AzVirtualNetwork @net

```

### [CLI](#tab/cli)

Create a virtual network named `vnet-1` with a subnet named `subnet-1` by using [`az network vnet create`](/cli/azure/network/vnet#az-network-vnet-create).

```azurecli-interactive

az network vnet create \

--resource-group test-rg \

--name vnet-1 \

--address-prefix 10.0.0.0/16 \

--subnet-name subnet-1 \

--subnet-prefixes 10.0.0.0/24

```

Create an Azure Bastion subnet named `AzureBastionSubnet` by using [`az network vnet subnet create`](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-create).

```azurecli-interactive

az network vnet subnet create \

--name AzureBastionSubnet \

--resource-group test-rg \

--vnet-name vnet-1 \

--address-prefix 10.0.1.0/26

```

---

## Deploy Azure Bastion

### [Portal](#tab/portal)

Azure Bastion uses your browser to connect to virtual machines (VMs) in your virtual network over Secure Shell (SSH) or Remote Desktop Protocol (RDP) by using their private IP addresses. The VMs don't need public IP addresses, client software, or special configuration. For more information, see [What is Azure Bastion?](../bastion/bastion-overview.md).

> [!NOTE]

> [!INCLUDE [Pricing](~/reusable-content/ce-skilling/azure/includes/bastion-pricing.md)]

1. In the search box at the top of the portal, enter **Bastion**. Select **Bastions** in the search results.

1. Select **+ Create**.

1. On the **Basics** tab of **Create a Bastion**, enter or select the following information:

| Setting | Value |

| --- | --- |

| **Project details** | |

| **Subscription** | Select your subscription. |

| **Resource group** | Select **test-rg**. |

| **Instance details** | |

| **Name** | Enter **bastion**. |

| **Region** | Select **(US) East US 2**. |

| **Tier** | Select **Developer**. |

| **Configure virtual networks** | |

| **Virtual network** | Select **vnet-1**. |

> [!NOTE]

> The Developer SKU for Azure Bastion is free and doesn't require a dedicated Azure Bastion subnet. For more information, see [Quickstart: Deploy Azure Bastion - Developer SKU](../bastion/quickstart-developer-sku.md).

1. Select **Review + create**.

1. Select **Create**.

### [PowerShell](#tab/powershell)

Create a public IP address for the Azure Bastion host by using [`New-AzPublicIpAddress`](/powershell/module/az.network/new-azpublicipaddress).

```azurepowershell-interactive

$ip = @{

Name = 'public-ip'

ResourceGroupName = 'test-rg'

Location = 'eastus2'

Sku = 'Standard'

AllocationMethod = 'Static'

Zone = 1, 2, 3

}

$publicip = New-AzPublicIpAddress @ip

```

Create an Azure Bastion host by using [`New-AzBastion`](/powershell/module/az.network/new-azbastion).

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

New-AzBastion @bastion -AsJob

```

The Azure Bastion host can take several minutes to deploy.

### [CLI](#tab/cli)

Create a public IP address for the Azure Bastion host by using [`az network public-ip create`](/cli/azure/network/public-ip#az-network-public-ip-create).

```azurecli-interactive

az network public-ip create \

--resource-group test-rg \

--name public-ip \

--sku Standard \

--location eastus2 \

--zone 1 2 3

```

Create the Azure Bastion host by using [`az network bastion create`](/cli/azure/network/bastion#az-network-bastion-create).

```azurecli-interactive

az network bastion create \

--name bastion \

--public-ip-address public-ip \

--resource-group test-rg \

--vnet-name vnet-1 \

--location eastus2 \

--sku Basic \

--no-wait

```

The Azure Bastion host can take several minutes to deploy.

---

## Create a virtual machine

### [Portal](#tab/portal)

The following procedure creates a Linux virtual machine with SSH key authentication:

1. In the search box at the top of the portal, enter **Virtual machines**. Select **Virtual machines** in the search results.

1. Select **+ Create**, and then select **Azure virtual machine**.

1. On the **Basics** tab of **Create a virtual machine**, enter or select the following values:

| Setting | Value |

| --- | --- |

| **Project details** | |

| **Subscription** | Select your Azure subscription. |

| **Resource group** | Select **test-rg**. |

| **Instance details** | |

| **Virtual machine name** | Enter **vm-1**. |

| **Region** | Select **(US) East US 2**. |

| **Availability options** | Select **No infrastructure redundancy required**. |

| **Security type** | Select **Standard**. |

| **Image** | Select **Ubuntu Server 24.04 LTS - x64 Gen2**. |

| **Size** | Choose a size or leave the default setting. |

| **Administrator account** | |

| **Authentication type** | Select **SSH public key**. |

| **Username** | Enter **azureuser**. |

| **SSH public key source** | Select **Generate new key pair**. |

| **Key pair name** | Enter **vm-1_key**. |

1. Select the **Networking** tab, or select **Next: Disks** > **Next: Networking**.

1. Select the following values:

| Setting | Value |

| --- | --- |

| **Network interface** | |

| **Virtual network** | Select **vnet-1**. |

| **Subnet** | Select **subnet-1**. |

| **Public IP** | Select **None**. |

1. Select **Review + create**.

1. Review the settings, and then select **Create**.

1. When the **Generate new key pair** window opens, select **Download private key and create resource**. The key file is downloaded as **vm-1_key.pem**. Make sure you know where the .pem file is downloaded. You need the path to the key file to connect to the VM.

### [PowerShell](#tab/powershell)

In this section, you create a virtual machine to test the NAT gateway and verify the public IP address of the outbound connection.

Create a virtual machine by using [`New-AzVM`](/powershell/module/az.compute/new-azvm). An SSH key pair is generated during VM creation.

```azurepowershell-interactive

$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force

$cred = New-Object System.Management.Automation.PSCredential ('azureuser', $securePassword)

$vm = @{

ResourceGroupName = 'test-rg'

Location = 'eastus2'

Name = 'vm-1'

Image = 'Ubuntu2204'

Size = 'Standard_DS1_v2'

VirtualNetworkName = 'vnet-1'

SubnetName = 'subnet-1'

PublicIpAddressName = ''

GenerateSshKey = $true

SshKeyName = 'vm-1_key'

Credential = $cred

}

New-AzVM @vm

```

Wait for the virtual machine creation to finish before moving on to the next section.

### [CLI](#tab/cli)

Create a Linux virtual machine named `vm-1` with SSH key authentication by using [`az vm create`](/cli/azure/vm#az-vm-create).

```azurecli-interactive

az vm create \

--resource-group test-rg \

--name vm-1 \

--image Ubuntu2404 \

--admin-username azureuser \

--generate-ssh-keys \

--public-ip-address "" \

--subnet subnet-1 \

--vnet-name vnet-1

```

Wait for the virtual machine creation to finish before moving on to the next section.

---

## Create the NAT gateway

### [Portal](#tab/portal)

In this section, you create the NAT gateway resource and associate it with the subnet of the virtual network that you created.

1. In the search box at the top of the portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **+ Create**.

1. In **Create network address translation (NAT) gateway**, enter or select this information on the **Basics** tab:

| Setting | Value |

| --- | --- |

| **Project details** | |

| **Subscription** | Select your Azure subscription. |

| **Resource group** | Select **test-rg**. |

| **Instance details** | |

| **NAT gateway name** | Enter **nat-gateway**. |

| **Region** | Select **(US) East US 2**. |

| **SKU** | Select **Standard**. |

| **Availability zone** | Select **No Zone**. |

| **TCP idle timeout (minutes)** | Leave the default of **4**. |

For information about availability zones and NAT gateway, see [Reliability in Azure NAT Gateway](/azure/reliability/reliability-nat-gateway).

1. Select the **Outbound IP** tab, or select **Next: Outbound IP**.

1. Enter or select the following information:

| Setting | Value |

| --- | --- |

| **Public IP addresses** | Select **Create a new public IP address**. </br> In **Name**, enter **public-ip-nat**. </br> Select **OK**. |

1. Select the **Networking** tab, or select **Next: Networking**.

1. In **Virtual network**, select **vnet-1**.

1. In **Subnet name**, select the **subnet-1** checkbox.

1. Select the **Review + create** tab, or select the **Review + create** button at the bottom of the pane.

1. Select **Create**.

### [PowerShell](#tab/powershell)

In this section, you create the NAT gateway resource and associate it with the subnet of the virtual network.

Create a public IP address for the NAT gateway by using [`New-AzPublicIpAddress`](/powershell/module/az.network/new-azpublicipaddress).

```azurepowershell-interactive

$ip = @{

Name = 'public-ip-nat'

ResourceGroupName = 'test-rg'

Location = 'eastus2'

Sku = 'Standard'

AllocationMethod = 'Static'

Zone = 1, 2, 3

}

$publicIP = New-AzPublicIpAddress @ip

```

Create a NAT gateway resource by using [`New-AzNatGateway`](/powershell/module/az.network/new-aznatgateway).

```azurepowershell-interactive

$nat = @{

ResourceGroupName = 'test-rg'

Name = 'nat-gateway'

IdleTimeoutInMinutes = '10'

Sku = 'Standard'

Location = 'eastus2'

PublicIpAddress = $publicIP

}

$natGateway = New-AzNatGateway @nat

```

Associate the NAT gateway with `subnet-1` by using [`Set-AzVirtualNetworkSubnetConfig`](/powershell/module/az.network/set-azvirtualnetworksubnetconfig). Apply the configuration by using [`Set-AzVirtualNetwork`](/powershell/module/az.network/set-azvirtualnetwork).

```azurepowershell-interactive

$vnet = Get-AzVirtualNetwork -Name 'vnet-1' -ResourceGroupName 'test-rg'

$subnet = @{

VirtualNetwork = $vnet

Name = 'subnet-1'

AddressPrefix = '10.0.0.0/24'

NatGateway = $natGateway

}

Set-AzVirtualNetworkSubnetConfig @subnet

$vnet | Set-AzVirtualNetwork

```

### [CLI](#tab/cli)

In this section, you create the NAT gateway resource and associate it with the subnet of the virtual network.

Create a public IP address for the NAT gateway by using [`az network public-ip create`](/cli/azure/network/public-ip#az-network-public-ip-create).

```azurecli-interactive

az network public-ip create \

--resource-group test-rg \

--name public-ip-nat \

--sku Standard \

--allocation-method Static \

--location eastus2 \

--zone 1 2 3

```

Create a NAT gateway resource by using [`az network nat gateway create`](/cli/azure/network/nat#az-network-nat-gateway-create).

```azurecli-interactive

az network nat gateway create \

--resource-group test-rg \

--name nat-gateway \

--public-ip-addresses public-ip-nat \

--idle-timeout 10

```

Associate the NAT gateway with `subnet-1` by using [`az network vnet subnet update`](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-update).

```azurecli-interactive

az network vnet subnet update \

--resource-group test-rg \

--vnet-name vnet-1 \

--name subnet-1 \

--nat-gateway nat-gateway

```

---

## Test the NAT gateway

To test the NAT gateway, you first discover its public IP. You then connect to the test virtual machine and verify the outbound connection through that public IP.

1. In the search box at the top of the portal, enter **Public IP**. Select **Public IP addresses** in the search results.

1. Select **public-ip-nat**.

1. Make note of the public IP address.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **vm-1**.

1. On the **Overview** page, select **Connect**, and then select the **Bastion** tab.

1. Select **Use Bastion**.

1. Under **Authentication Type**, select **SSH Private Key from Local File**.

1. In **Username**, enter **azureuser**.

1. Select **Browse** and go to the **vm-1_key.pem** file downloaded during VM creation.

1. Select **Connect**.

1. In the Bash prompt, enter the following command:

```bash

curl ifconfig.me

```

1. Verify that the IP address returned by the command matches the public IP address of the NAT gateway.

```output

azureuser@vm-1:~$ curl ifconfig.me

203.0.113.0.25

```

## Clean up resources

### [Portal](#tab/portal)

[!INCLUDE [portal-clean-up.md](~/reusable-content/ce-skilling/azure/includes/portal-clean-up.md)]

### [PowerShell](#tab/powershell)

If you no longer need this application, delete the virtual network, virtual machine, and NAT gateway by using the following command:

```azurepowershell-interactive

Remove-AzResourceGroup -Name 'test-rg' -Force

```

### [CLI](#tab/cli)

If you no longer need this application, delete the virtual network, virtual machine, and NAT gateway by using the following command:

```azurecli-interactive

az group delete \

--name test-rg \

--yes

```

---

## Related content

- [Azure NAT Gateway overview](nat-overview.md)

- [NAT gateway resource](nat-gateway-resource.md)


# Nat Gateway V2 Migrate

# Migrate Azure NAT Gateway from Standard to StandardV2

The StandardV2 SKU of Azure NAT Gateway offers enhanced data-processing limits and high availability through zone redundancy. We recommend that you use the StandardV2 SKU for production workloads that require resiliency to zone outages.

This article discusses guidance for how to migrate your subnets from a Standard network address translation (NAT) gateway to a StandardV2 NAT gateway. In-place migration to a StandardV2 NAT gateway isn't available.

> [!IMPORTANT]

> Migration from a Standard NAT gateway to a StandardV2 NAT gateway involves *downtime and impact to existing connections*. Plan accordingly.

## Pre-migration steps

We recommend the following steps to prepare for the migration:

* A StandardV2 NAT gateway requires the use of StandardV2 public IPs. Existing Standard public IPs don't work with StandardV2 NAT gateways. Make sure that you can re-IP to StandardV2 public IPs before you create a StandardV2 NAT gateway.

* Check if you have requirements for allow lists at destination endpoints, because you have to re-IP to StandardV2 public IPs to use a StandardV2 NAT gateway.

* Plan for application downtime during the migration. Existing connections with a Standard NAT gateway are affected when you're migrating to a StandardV2 NAT gateway.

* Confirm which subnets in your virtual network need to be migrated to a StandardV2 NAT gateway.

## Unsupported scenarios

Before you migrate to a StandardV2 NAT gateway, make sure that your specific scenario is supported. Review the following unsupported scenarios and [known issues](#known-issues) with StandardV2 NAT gateways.

* You must use StandardV2 public IPs with StandardV2 NAT gateways. Standard public IPs aren't supported.

* StandardV2 NAT Gateway doesn't support Basic load balancers or Basic public IPs.

* StandardV2 NAT Gateway doesn't support the use of custom public IPs (bring your own IP).

* The following regions don't support StandardV2 NAT gateways and StandardV2 public IPs:

* Canada East

* Chile Central

* Indonesia Central

* Israel Northwest

* Malaysia West

* Qatar Central

* Sweden South

* West India

## Known issues

* A StandardV2 NAT gateway disrupts outbound connections made with load balancer outbound rules for IPv6 traffic only. If you see disruption to outbound connectivity for IPv6 outbound traffic with load balancer outbound rules, remove the StandardV2 NAT gateway from the subnet or virtual network. Then use either:

* Load balancer outbound rules to provide outbound connectivity for both IPv4 and IPv6 traffic

* A Standard NAT gateway to provide outbound connectivity for IPv4 traffic and load balancer outbound rules for IPv6 traffic

* Existing outbound connections that use a load balancer or instance-level public IPs on a VM instance might be interrupted when you attach a Standard or StandardV2 NAT gateway to the subnet. New connections use the NAT gateway.

## Guidance for manual migration

### Azure portal

To manually migrate from a Standard NAT gateway to a StandardV2 NAT gateway by using the Azure portal, use this suggested order of operations:

1. Select StandardV2 as the SKU.

2. Create a new StandardV2 public IP or a StandardV2 public IP prefix resource. Select the required IP version: IPv4 or IPv6.

3. Skip the **Networking** tab. You attach the StandardV2 NAT gateway to the subnet later.

4. Create the StandardV2 NAT gateway.

5. From your resource group, go to the subnet that you want to migrate from a Standard NAT gateway to a StandardV2 NAT gateway.

6. Update the subnet configuration to use the new StandardV2 NAT gateway. This step replaces your existing Standard NAT gateway with the StandardV2 NAT gateway.

7. Save the subnet configuration and validate connectivity.

8. Repeat steps 5 to 7 for each subnet that you want to migrate to a StandardV2 NAT gateway.

> [!NOTE]

> This migration doesn't delete your existing Standard NAT gateway or Standard public IP resources.

### Azure PowerShell

Before you migrate from a Standard NAT gateway to a StandardV2 NAT gateway by using Azure PowerShell, ensure that you meet the following criteria:

* You have Azure PowerShell installed locally, or you plan to use Azure Cloud Shell. If you choose to install and use PowerShell locally:

* This article requires Azure PowerShell module version 5.4.1 or later. To find the installed version, run `Get-Module -ListAvailable Az`. If you need to upgrade, see [Install Azure PowerShell](/powershell/azure/install-azure-powershell).

* Run `Connect-AzAccount` to create a connection with Azure.

* Ensure that your `Az.Network` module is 7.17.0 or later. To verify the installed module, use the command `Get-InstalledModule -Name "Az.Network"`. If the module requires an update, use the command `Update-Module -Name Az.Network`.

* Sign in to Azure PowerShell and select the subscription that you want to use. For more information, see [Sign in to Azure from Azure PowerShell](/powershell/azure/authenticate-azureps).

For the migration, use this suggested order of operations:

1. Create a new StandardV2 public IP or a StandardV2 public IP prefix resource by using the `New-AzPublicIpAddress` or `New-AzPublicIpPrefix` cmdlet. Select IPv4 or IPv6 for the IP version.

```powershell

$publicIp = New-AzPublicIpAddress -ResourceGroupName <your-resource-group> -Name <your-public-ip-name> -Location <your-location> -Sku StandardV2 -AllocationMethod Static -IpVersion IPv4 -Zone 1,2,3

```

Or

```powershell

$publicIpPrefix = New-AzPublicIpPrefix -ResourceGroupName <your-resource-group> -Name <your-public-ip-prefix-name> -Location <your-location> -Sku StandardV2 -PrefixLength 28 -Zone 1,2,3

```

2. Create a new StandardV2 NAT gateway by using the `New-AzNatGateway` cmdlet. Be sure to select StandardV2 as the SKU.

```powershell

$natGateway = New-AzNatGateway -ResourceGroupName <your-resource-group> -Name <your-nat-gateway-name> -Location <your-location> -Sku StandardV2, -PublicIpAddress $publicIp

```

Or

```powershell

$natGateway = New-AzNatGateway -ResourceGroupName <your-resource-group> -Name <your-nat-gateway-name> -Location <your-location> -Sku StandardV2 -PublicIpPrefix $publicIpPrefix

```

3. From your resource group, retrieve the subnet that you want to migrate from a Standard NAT gateway to a StandardV2 NAT gateway by using the `Get-AzVirtualNetwork` cmdlet.

```powershell

$subnet = Get-AzVirtualNetwork -ResourceGroupName <your-resource-group> -Name <your-vnet-name> | Get-AzVirtualNetworkSubnetConfig -Name <your-subnet-name>

```

4. Update the subnet configuration to use the new StandardV2 NAT gateway by using the `Set-AzVirtualNetworkSubnetConfig` cmdlet.

```powershell

Set-AzVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name <your-subnet-name> -NatGateway $natGateway

```

5. Save the subnet configuration by using the `Set-AzVirtualNetwork` cmdlet.

```powershell

Set-AzVirtualNetwork -VirtualNetwork $vnet

```

6. Repeat steps 3 to 5 for each subnet that you want to migrate to a StandardV2 NAT gateway.

> [!NOTE]

> This migration process doesn't delete your existing Standard NAT gateway or Standard public IP resources.

### Azure CLI

Before you migrate from a Standard NAT gateway to a StandardV2 NAT gateway by using the Azure CLI, ensure that you meet the following criteria:

* To run CLI reference commands locally, [install the Azure CLI](/cli/azure/install-azure-cli). If you're running on Windows or macOS, consider [running the Azure CLI in a Docker container](/cli/azure/run-azure-cli-docker).

* If you're using a local installation, sign in to the Azure CLI by using the [`az login`](/cli/azure/reference-index#az-login) command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see [Authenticate to Azure using the Azure CLI](/cli/azure/authenticate-azure-cli).

* When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see [Manage Azure CLI extensions](/cli/azure/azure-cli-extensions-overview).

* To find the version and dependent libraries that are installed, run [az version](/cli/azure/reference-index?#az-version). To upgrade to the latest version, run [az upgrade](/cli/azure/reference-index?#az-upgrade).

For the migration, use this suggested order of operations:

1. Create a new StandardV2 public IP or a StandardV2 public IP prefix resource by using the `az network public-ip create` or `az network public-ip prefix create` cmdlet. Select IPv4 or IPv6 for the IP version.

```azurecli-interactive

az network public-ip create \

--resource-group test-rg \

--name public-ip-nat \

--location eastus \

--sku StandardV2 \

--allocation-method Static \

--version IPv4 \

--zone 1 2 3

```

Or

```azurecli-interactive

az network public-ip prefix create \

--resource-group test-rg \

--name public-ip-prefix-nat \

--location eastus \

--sku StandardV2 \

--length 28 \

--version IPv4 \

--zone 1 2 3

```

2. Create a new StandardV2 NAT gateway by using the `az network nat gateway create` cmdlet. Be sure to select StandardV2 as the SKU.

```azurecli-interactive

az network nat gateway create \

--resource-group test-rg \

--name nat-gatewayv2 \

--location eastus \

--public-ip-addresses public-ip-nat \

--idle-timeout 4 \

--sku StandardV2 \

--zone 1 2 3

```

3. Replace the Standard NAT gateway on your subnet with your newly created StandardV2 NAT gateway by using the `az network vnet subnet update` cmdlet.

```azurecli-interactive

az network vnet subnet update \

--resource-group test-rg \

--vnet-name myVNet \

--name mySubnet \

--nat-gateway nat-gatewayv2

```

4. Repeat step 3 for each subnet that you want to migrate to a StandardV2 NAT gateway.

## Post-migration steps

After you migrate your subnets to a StandardV2 NAT gateway, we recommend the following steps:

1. Validate outbound connectivity to the internet from the virtual machines in the subnets that you migrated to the StandardV2 NAT gateway.

1. Monitor your applications for any issues related to connectivity or performance after the migration.

## Common questions

### Can I use my existing Standard public IPs with a StandardV2 NAT gateway?

No, a StandardV2 NAT gateway requires the use of StandardV2 public IPs. Existing Standard public IPs aren't compatible with a StandardV2 NAT gateway.

### Is there any downtime during the migration?

Yes, migrating from a Standard NAT gateway to a StandardV2 NAT gateway causes downtime and affects existing connections. Be sure to plan for application downtime during the migration and perform the migration during a maintenance window.

### How long is the expected downtime?

The duration of downtime depends on the number of subnets that you're migrating and the complexity of your network configuration. To minimize downtime, migrate one subnet at a time and validate connectivity before you proceed to the next subnet.

### Can I automate the migration process?

Yes, you can use Azure PowerShell or Azure CLI scripts to automate the migration process. The steps in this article can be adapted into scripts for automation.

### How do I revert back to a Standard NAT gateway if needed?

To revert back to a Standard NAT gateway, you need to reattach the subnets to the existing Standard NAT gateway and reassign the original Standard public IPs. This process also involves downtime and affects existing connections.

### Is my Standard NAT gateway deleted after migration?

No, migrating to a StandardV2 NAT gateway doesn't delete your existing Standard NAT gateway or your Standard public IP resources. You need to manually delete these resources if you no longer need them. Don't delete these resources until you fully validate that your workloads function as expected with the StandardV2 NAT gateway.

### How do I validate that the migration is successful?

After you migrate your subnets to a StandardV2 NAT gateway, you can validate the migration by checking outbound connectivity to the internet from your virtual machines in the migrated subnets. You can also monitor your applications for any connectivity or performance issues. For guidance on how to test connectivity for a NAT gateway, see [Create a StandardV2 NAT gateway](quickstart-create-nat-gateway-v2.md).


# Nat Gateway Design

# Design virtual networks with Azure NAT Gateway

Review this article to familiarize yourself with considerations for designing virtual networks with NAT gateway.

## Connect to the internet with a NAT gateway

NAT Gateway is recommended for all production workloads where you need to connect to a public endpoint over the internet. Outbound connectivity takes place right away upon deployment of a NAT gateway with a subnet and at least one public IP address. No routing configurations are required to start connecting outbound with the NAT gateway. The NAT gateway becomes the subnet’s default route to the internet.

In the presence of other outbound configurations within a virtual network, such as a load balancer or instance-level public IPs (IL PIPs), the NAT gateway takes precedence for outbound connectivity. New outbound initiated traffic and return traffic uses the NAT gateway. There's no down time on outbound connectivity after adding a NAT gateway to a subnet with existing outbound configurations.

## Use StandardV2 NAT gateway for zone-redundancy

[Availability zones](/azure/reliability/availability-zones-overview) are physically separate groups of datacenters within each Azure region. When one zone fails, services can fail over to one of the remaining healthy zones.

StandardV2 NAT Gateway supports availability zone scenarios.

When StandardV2 NAT gateway is deployed, outbound connections can flow out of any zone in the region. When a zone goes down, some in flight connections from the failed zone may be impacted, but all new connections flow out of the remaining healthy zones.

To learn more information, see [NAT gateway availability zones](/azure/nat-gateway/nat-availability-zones).

## Scale a NAT gateway to meet the demand of a dynamic workload

Scaling NAT Gateway is primarily a function of managing the shared, available SNAT port inventory.

When you scale your workload, assume that each flow requires a new SNAT port, and then scale the total number of available IP addresses for outbound traffic. Carefully consider the scale you're designing for, and then allocate IP addresses. NAT Gateway needs sufficient SNAT port inventory for expected peak outbound flows for all subnets that are attached to a NAT gateway.

As SNAT port exhaustion approaches, connection flows may not succeed.

### Scaling considerations

Each NAT gateway public IP address provides 64,512 SNAT ports to make outbound connections. A NAT gateway can scale up to over 1 million SNAT ports.

SNAT maps private addresses in your subnet to one or more public IP addresses attached to a NAT gateway, rewriting the source address and source port in the process. When multiple connections are made to the same destination endpoint, a new SNAT port is used. A new SNAT port must be used in order to distinguish different connection flows from one another going to the same destination.

Connection flows going to different destination endpoints can reuse the same SNAT port at the same time. SNAT port connections sent to different destinations are reused when possible. As SNAT port exhaustion approaches, flows may not succeed.

For a SNAT example, see [Example SNAT flows for NAT Gateway](nat-gateway-snat.md#example-snat-flows-for-nat-gateway).

## Connect to Azure services with Private Link

Connecting from your Azure virtual network to Azure PaaS services can be done directly over the Azure backbone and bypass the internet. When you bypass the internet to connect to other Azure PaaS services, you free up SNAT ports and reduce the risk of SNAT port exhaustion. Private Link should be used when possible to connect to Azure PaaS services in order to free up SNAT port inventory.

Private Link uses the private IP addresses of your virtual machines or other compute resources from your Azure network to directly connect privately and securely to Azure PaaS services over the Azure backbone. See a list of available Azure services that Private Link supports.

> [!NOTE]

> Microsoft recommends use of Azure Private Link for secure and private access to services hosted in Azure. [Service endpoints](/azure/virtual-network/virtual-network-service-endpoints-overview) can also be used to connect directly to Azure PaaS services over the Azure backbone.

## Provide outbound and inbound connectivity for your Azure virtual network

A NAT gateway, load balancer, and instance-level public IPs are flow direction aware and can coexist in the same virtual network to provide outbound and inbound connectivity seamlessly. Inbound traffic through a load balancer or instance-level public IPs is translated separately from outbound traffic through the NAT gateway.

Private instances use the NAT gateway for outbound traffic and any response traffic to the **outbound originated flow**. Private instances use instance-level public IPs or a load balancer for inbound traffic and any response traffic to the **inbound originated flow**.

The following examples demonstrate coexistence of a load balancer or instance-level public IPs with a NAT gateway. Inbound traffic traverses the load balancer or public IP. Outbound traffic traverses the NAT gateway.

### A NAT gateway and VM with an instance-level public IP

*Figure: A NAT gateway and VM with an instance-level public IP*

| Resource | Traffic flow direction | Connectivity method used |

| --- | --- | --- |

| VM (Subnet 1) | Inbound </br> Outbound | Instance-level public IP </br> NAT gateway |

| Virtual machine scale set (Subnet 1) | Inbound </br> Outbound | NA </br> NAT gateway |

| VMs (Subnet 2) | Inbound </br> Outbound |  NA </br> NAT gateway |

The virtual machine uses the NAT gateway for outbound and return traffic. Inbound originated traffic passes through the instance level public IP directly associated with the virtual machine in subnet 1. The virtual machine scale set from subnet 1 and VMs from subnet 2 can only egress and receive response traffic through the NAT gateway. No inbound originated traffic can be received.

### A NAT gateway and VM with a standard public load balancer

*Figure: A NAT gateway and VM with a standard public load balancer*

| Resource | Traffic flow direction | Connectivity method used |

| --- | --- | --- |

|VM and virtual machine scale set (Subnet 1) | Inbound </br> Outbound | Load balancer </br> NAT gateway |

|VMs (Subnet 2) | Inbound </br> Outbound | NA </br> NAT gateway |

NAT Gateway supersedes any outbound configuration from a load-balancing rule or outbound rules on the load balancer. VM instances in the backend pool use the NAT gateway to send outbound traffic and receive return traffic. Inbound originated traffic passes through the load balancer for all VM instances (Subnet 1) within the load balancer’s backend pool. VMs from subnet 2 can only egress and receive response traffic through the NAT gateway. No inbound originated traffic can be received.

### A NAT gateway and VM with an instance-level public IP and a standard public load balancer

*Figure: NAT Gateway and VM with an instance-level public IP and a standard public load balancer*

| Resource | Traffic flow direction | Connectivity method used |

| --- | --- | --- |

| VM (Subnet 1) | Inbound </br> Outbound | Instance-level public IP </br> NAT gateway |

| Virtual machine scale set (Subnet 1) | Inbound </br> Outbound | Load balancer </br> NAT gateway |

| VMs (Subnet 2) | Inbound </br> Outbound | NA </br> NAT gateway |

The NAT gateway supersedes any outbound configuration from a load-balancing rule or outbound rules on a load balancer and instance level public IPs on a virtual machine. All virtual machines in subnets 1 and 2 use the NAT gateway exclusively for outbound and return traffic. Instance-level public IPs take precedence over load balancer. The VM in subnet 1 uses the instance level public IP for inbound originating traffic. Virtual machine scale-sets don't have instance-level public IPs.

## How to use service tagged public IPs with NAT Gateway

[Service tags](/azure/virtual-network/service-tags-overview) represent a group of IP addresses from a given Azure service. Microsoft manages the address prefix encompassed by the service tag and automatically updates the service tag as addresses change, which reduces the complexity of managing network security rules.

Service tagged public IP addresses can be used with NAT gateway for providing outbound connectivity to the internet. To add a service tagged public IP to a NAT gateway, you can attach it using any of the available clients in Azure, such as the portal, CLI, or PowerShell. See [how to add and remove public IPs for NAT gateway](/azure/nat-gateway/manage-nat-gateway?tabs=manage-nat-portal#add-or-remove-a-public-ip-address) for detailed guidance.

> [!NOTE]

> NAT gateway doesn't support Public IP addresses with [routing preference "Internet"](/azure/virtual-network/ip-services/routing-preference-overview#routing-over-public-internet-isp-network). NAT gateway only supports public IPs that route over the Microsoft global network.

## Monitor outbound network traffic with StandardV2 NAT Gateway flow logs

StandardV2 NAT Gateway supports NAT gateway flow logs through Azure Monitor. NAT gateway flow logs provide IP level traffic information for traffic flowing through the StandardV2 NAT Gateway. For more information, see [Analyze NAT Gateway traffic with flow logs](./nat-gateway-flow-logs.md).

## NAT gateway and user defined routes

A NAT gateway relies on the subnet’s default route 0.0.0.0/0 to next hop internet to source NAT (SNAT) outbound traffic to the internet.

If you create a user-defined route (UDR) that sends 0.0.0.0/0 traffic to a virtual appliance as the next hop, the system’s default “Internet” route is overridden. As a result, all outbound traffic is sent to the virtual appliance instead of through the NAT gateway.

A common use of this pattern is forced tunneling: forwarding all 0.0.0.0/0 traffic to a virtual appliance such as a VPN gateway or ExpressRoute. The appliance can then redirect the traffic to an on-premises network, where it exits to the internet under on-premises security, monitoring, and compliance controls. In this scenario, the NAT gateway is bypassed and doesn't provide outbound internet connectivity.

If you instead configure a UDR with next hop = Internet, outbound traffic continues to flow through the NAT gateway. The NAT gateway performs SNAT for that traffic.

This approach is especially useful in scenarios where certain destinations, such as a Key Management Service (KMS) endpoint, must be reached over the internet. In this case, you can create a UDR with:

* Destination = KMS service address

* Next hop = Internet

With this configuration, the NAT gateway handles SNAT, and traffic to the KMS endpoint successfully flows over the internet.

## Use NAT gateway instead of default outbound access

When a virtual machine is deployed in a virtual network without an explicitly defined outbound connectivity method, it’s assigned a default outbound public IP address. This IP address enables outbound connectivity from the resources to the internet and to other public endpoints within Microsoft and is known as a default outbound IP. The default outbound access IP is owned by Microsoft and is subject to change without notice. The end user has no visibility of this default outbound access public IP address. This default outbound access public IP isn’t recommended for production workloads.

Secure outbound connectivity to the internet by [enabling private subnet](/azure/virtual-network/ip-services/default-outbound-access#how-can-i-transition-to-an-explicit-method-of-public-connectivity-and-disable-default-outbound-access). Private subnet prevents the creation of new default outbound IPs for virtual machines in your subnet. Instead use an explicit method of outbound connectivity like NAT gateway.

> [!IMPORTANT]

> On March 31, 2026, new virtual networks will default to using private subnets, meaning that default outbound access will no longer be provided by default, and that explicit outbound method must be enabled in order to reach public endpoints on the Internet and within Microsoft. It's recommended to use an explicit form of outbound connectivity instead, like NAT gateway.

Certain services don’t function on a virtual machine in a private subnet without an explicit method of outbound connectivity, such as Windows Activation and Windows Updates. To activate or update virtual machine operating systems, such as Windows, an explicit method of outbound connectivity is required, like NAT gateway.

## Limitations

* NAT Gateway isn't supported in a vWAN hub configuration.

* StandardV2 NAT Gateway requires StandardV2 SKU Public IP addresses and prefixes. Standard SKU public IPs aren’t supported.

* StandardV2 NAT Gateway doesn’t support custom IP prefixes (BYOIP)

* Managed NAT Gateway V2 for AKS workloads is now in preview. For more information, see [Create NAT Gateway for your AKS cluster](Create a managed or user-assigned NAT gateway for your Azure Kubernetes Service (AKS) cluster - Azure Kubernetes Service | Microsoft Learn

* StandardV2 NAT Gateway is available in select Azure regions. It’s not available in the following regions:

* Canada East

* Chile Central

* Indonesia Central

* Israel Northwest

* Malaysia West

* Qatar Central

* West India

* Sweden South

## Related content

- [Azure NAT Gateway resource](nat-gateway-resource.md).

- [SNAT and Azure NAT Gateway](nat-gateway-snat.md).

- [Azure NAT Gateway FAQ](faq.yml).


# Tutorial Hub Spoke Route Nat

# Tutorial: Use a NAT gateway with a hub and spoke network

A hub and spoke network is one of the building blocks of a highly available multiple location network infrastructure. The most common deployment of a hub and spoke network is done with the intention of routing all inter-spoke and outbound internet traffic through the central hub. The purpose is to inspect all of the traffic traversing the network with a Network Virtual Appliance (NVA) for security scanning and packet inspection.

For outbound traffic to the internet, the network virtual appliance would typically have one network interface with an assigned public IP address. The NVA after inspecting the outbound traffic forwards the traffic out the public interface and to the internet. Azure NAT Gateway eliminates the need for the public IP address assigned to the NVA. Associating a NAT gateway with the public subnet of the NVA changes the routing for the public interface to route all outbound internet traffic through the NAT gateway. The elimination of the public IP address increases security and allows for the scaling of outbound source network address translation (SNAT) with multiple public IP addresses and or public IP prefixes.

> [!IMPORTANT]

> The NVA used in this article is for demonstration purposes only and is simulated with an Ubuntu virtual machine. The solution doesn't include a load balancer for high availability of the NVA deployment. Replace the Ubuntu virtual machine in this article with an NVA of your choice. Consult the vendor of the chosen NVA for routing and configuration instructions. A load balancer and availability zones are recommended for a highly available NVA infrastructure.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a NAT gateway.

> * Create a hub and spoke virtual network.

> * Create a simulated Network Virtual Appliance (NVA).

> * Force all traffic from the spokes through the hub.

> * Force all internet traffic in the hub and the spokes out the NAT gateway.

> * Test the NAT gateway and inter-spoke routing.

## Prerequisites

# [**Portal**](#tab/portal)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

# [**Powershell**](#tab/powershell)

- An Azure account with an active subscription. You can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

[!INCLUDE [cloud-shell-try-it.md](~/reusable-content/ce-skilling/azure/includes/cloud-shell-try-it.md)]

If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 1.0.0 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell). If you're running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

---

## Create a resource group

Create a resource group to contain all resources for this quickstart.

# [**Portal**](#tab/portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal enter **Resource group**. Select **Resource groups** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab of **Create a resource group**, enter or select the following information.

| Setting | Value |

| ------- | ----- |

| Subscription | Select your subscription|

| Resource group | test-rg |

| Region | **West US** |

1. Select **Review + create**.

1. Select **Create**.

# [**Powershell**](#tab/powershell)

Create a resource group with [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup). An Azure resource group is a logical container into which Azure resources are deployed and managed.

The following example creates a resource group named **test-rg** in the **westus** location:

```azurepowershell-interactive

$rsg = @{

Name = 'test-rg'

Location = 'westus'

}

New-AzResourceGroup @rsg

```

---

## Create a NAT gateway

All outbound internet traffic traverses the NAT gateway to the internet. Use the following example to create a NAT gateway for the hub and spoke network.

# [**Portal**](#tab/portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the Azure portal, enter **Public IP address**. Select **Public IP addresses** in the search results.

1. Select **Create**.

1. Enter the following information in **Create public IP address**.

| Setting | Value |

| ------- | ----- |

| Subscription | Select your subscription. |

| Resource group | Select your resource group. The example uses **test-rg**. |

| Region | Select a region. This example uses **West US**. |

| Name | Enter **public-ip-nat**. |

| IP version | Select **IPv4**. |

| SKU | Select **Standard**. |

| Availability zone | Select **Zone-redundant**. |

| Tier | Select **Regional**. |

1. Select **Review + create** and then select **Create**.

1. In the search box at the top of the Azure portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create network address translation (NAT) gateway**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| NAT gateway name | Enter **nat-gateway**. |

| Region | Select your region. This example uses **West US**. |

| SKU | Select **Standard**. |

| TCP idle timeout (minutes) | Leave the default of **4**. |

1. Select **Next**.

1. In the **Outbound IP** tab, select **+ Add public IP addresses or prefixes**.

1. In **Add public IP addresses or prefixes**, select **Public IP addresses**. Select the public IP address you created earlier, **public-ip-nat**.

1. Select **Next**.

1. In the **Networking** tab, in **Virtual network**, select **vnet-1**.

1. Leave the checkbox for **Default to all subnets** unchecked.

1. In **Select specific subnets**, select **subnet-1**.

1. Select **Review + create**, then select **Create**.

# [**Powershell**](#tab/powershell)

Use [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) to create a zone redundant IPv4 public IP address for the NAT gateway.

```azurepowershell-interactive

## Create public IP address for NAT gateway ##

$ip = @{

Name = 'public-ip-nat'

ResourceGroupName = 'test-rg'

Location = 'westus'

Sku = 'Standard'

AllocationMethod = 'Static'

IpAddressVersion = 'IPv4'

Zone = 1,2,3

}

$publicIPIPv4 = New-AzPublicIpAddress @ip

```

Use [New-AzNatGateway](/powershell/module/az.network/new-aznatgateway) to create the NAT gateway resource.

```azurepowershell

## Create NAT gateway resource ##

$nat = @{

ResourceGroupName = 'test-rg'

Name = 'nat-gateway'

IdleTimeoutInMinutes = '4'

Sku = 'Standard'

Location = 'westus'

PublicIpAddress = $publicIPIPv4

Zone = 1

}

$natGateway = New-AzNatGateway @nat

```

---

## Create hub virtual network

The hub virtual network is the central network of the solution. The hub network contains the NVA appliance and a public and private subnet. The NAT gateway is assigned to the public subnet during the creation of the virtual network. An Azure Bastion host is configured as part of the following example. The bastion host is used to securely connect to the NVA virtual machine and the test virtual machines deployed in the spokes later in the article.

# [**Portal**](#tab/portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the Azure portal, enter **Virtual network**. Select **Virtual networks** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create virtual network**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| Name | Enter **vnet-1**. |

| Region | Select your region. This example uses **West US**. |

1. Select the **IP Addresses** tab, or select **Next: Security**, then **Next: IP Addresses**.

1. In **Subnets** select the **default** subnet.

1. Enter or select the following information in **Edit subnet**.

| Setting | Value |

| ------- | ----- |

| Subnet purpose | Leave the default. |

| Name | Enter **subnet-1**. |

1. Leave the rest of the settings as default, then select **Save**.

1. Select **+ Add a subnet**.

1. In **Add a subnet** enter or select the following information.

| Setting | Value |

| ------- | ----- |

| Subnet purpose | Select **Azure Bastion**. |

1. Leave the rest of the settings as default, then select **Add**.

1. Select **Review + create**, then select **Create**.

# [**Powershell**](#tab/powershell)

Use [New-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/add-azvirtualnetworksubnetconfig) to create the subnets.

```powershell

$subnetPrivateParams = @{

Name = "subnet-private"

AddressPrefix = "10.0.0.0/24"

}

$privateSubnetConfig = New-AzVirtualNetworkSubnetConfig @subnetPrivateParams

$subnetBastionParams = @{

Name = "AzureBastionSubnet"

AddressPrefix = "10.0.1.0/26"

}

$bastionSubnetConfig = New-AzVirtualNetworkSubnetConfig @subnetBastionParams

$subnetPublicParams = @{

Name = "subnet-public"

AddressPrefix = "10.0.253.0/28"

NatGateway = (Get-AzNatGateway -ResourceGroupName "test-rg" -Name "nat-gateway")

}

$publicSubnetConfig = New-AzVirtualNetworkSubnetConfig @subnetPublicParams

```

Use [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork) to create the virtual network.

```powershell

$vNetParams = @{

ResourceGroupName = "test-rg"

Name = "vnet-hub"

AddressPrefix = "10.0.0.0/16"

Location = "westus"

Subnet = $privateSubnetConfig, $bastionSubnetConfig, $publicSubnetConfig

}

$vNet = New-AzVirtualNetwork @vNetParams

```

---

## Create Azure Bastion host

Azure Bastion provides secure RDP and SSH connectivity to virtual machines over TLS without requiring public IP addresses on the VMs.

# [**Portal**](#tab/portal)

1. In the search box at the top of the Azure portal, enter **Bastion**. Select **Bastions** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create a Bastion**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| Name | Enter **bastion**. |

| Region | Select your region. This example uses **West US**. |

| Tier | Select **Developer**. |

| Virtual network | Select **vnet-1**. |

| Subnet | Select **AzureBastionSubnet**. |

1. Select **Review + create**, then select **Create**.

# [**Powershell**](#tab/powershell)

Use [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) to create a public IP address for the Azure Bastion host.

```powershell

$publicIpParams = @{

ResourceGroupName = "test-rg"

Name = "public-ip-bastion"

Sku = "Standard"

AllocationMethod = "Static"

Location = "westus"

Zone = 1,2,3

}

New-AzPublicIpAddress @publicIpParams

```

Use [New-AzBastion](/powershell/module/az.network/new-azbastion) to create the Azure Bastion host.

```powershell

$bastionParams = @{

ResourceGroupName = "test-rg"

Name = "bastion"

VirtualNetworkName = "vnet-hub"

PublicIpAddressName = "public-ip-bastion"

PublicIPAddressRgName = "test-rg"

VirtualNetworkRgName = "test-rg"

Sku = "Basic"

}

New-AzBastion @bastionParams

```

---

## Create simulated NVA virtual machine

The simulated NVA acts as a virtual appliance to route all traffic between the spokes and hub and traffic outbound to the internet. An Ubuntu virtual machine is used for the simulated NVA. Use the following example to create the simulated NVA and configure the network interfaces.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **+ Create** then **Azure virtual machine**.

1. In **Create a virtual machine** enter or select the following information in the **Basics** tab:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |   |

| Virtual machine name | Enter **vm-nva**. |

| Region | Select **(US) West US**. |

| Availability options | Select **No infrastructure redundancy required**. |

| Security type | Select **Standard**. |

| Image | Select **Ubuntu Server 24.04 LTS - x64 Gen2**. |

| VM architecture | Leave the default of **x64**. |

| Size | Select a size. |

| **Administrator account** |   |

| Authentication type | Select **SSH public key**. |

| Username | Enter a username. |

| SSH public key source | Select **Generate new key pair**. |

| SSH Key Type | Leave the default of **RSA SSH Format**. |

| Key pair name | Enter **ssh-key**. |

| **Inbound port rules** |  |

| Public inbound ports | Select **None**. |

1. Select **Next: Disks** then **Next: Networking**.

1. In the Networking tab, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Network interface** |   |

| Virtual network | Select **vnet-hub**. |

| Subnet | Select **subnet-public (10.0.253.0/28)**. |

| Public IP | Select **None**. |

| NIC network security group | Select **Advanced**. |

| Configure network security group | Select **Create new**. </br> In **Name** enter **nsg-nva**. </br> Select **OK**. |

1. Leave the rest of the options at the defaults and select **Review + create**.

1. Select **Create**.

1. The **Generate new key pair** dialog box appears. Select **Download private key and create resource**.

The private key will download to your local machine. The private key is needed in later steps for connecting to the virtual machine with Azure Bastion. The name of the private key file is the name you entered in the **Key pair name** field. In this example, the private key file is named **ssh-key**.

# [**Powershell**](#tab/powershell)

Use [New-AzNetworkSecurityGroup](/powershell/module/az.network/new-aznetworksecuritygroup) to create the network security group.

```powershell

$nsgParams = @{

ResourceGroupName = "test-rg"

Name = "nsg-nva"

Location = "westus"

}

New-AzNetworkSecurityGroup @nsgParams

```

Use [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface) to create the network interface.

```powershell

$nicParams = @{

ResourceGroupName = "test-rg"

Name = "nic-public"

SubnetId = (Get-AzVirtualNetwork -ResourceGroupName "test-rg" -Name "vnet-hub").Subnets[1].Id

NetworkSecurityGroupId = (Get-AzNetworkSecurityGroup -ResourceGroupName "test-rg" -Name "nsg-nva").Id

Location = "westus"

}

New-AzNetworkInterface @nicParams

```

Use [Get-Credential](/powershell/module/microsoft.powershell.security/get-credential) to set a user name and password for the VM and store them in the `$cred` variable.

```azurepowershell

$cred = Get-Credential

```

> [!NOTE]

> A username is required for the VM. The password is optional and won't be used if set. SSH key configuration is recommended for Linux VMs.

Use [New-AzVMConfig](/powershell/module/az.compute/new-azvmconfig) to define a VM.

```azurepowershell

$vmConfigParams = @{

VMName = "vm-nva"

VMSize = "Standard_DS4_v2"

}

$vmConfig = New-AzVMConfig @vmConfigParams

```

Use [Set-AzVMOperatingSystem](/powershell/module/az.compute/set-azvmoperatingsystem) and [Set-AzVMSourceImage](/powershell/module/az.compute/set-azvmsourceimage) to create the rest of the VM configuration. The following example creates an Ubuntu Server virtual machine:

```azurepowershell

$osParams = @{

VM = $vmConfig

ComputerName = "vm-nva"

Credential = $cred

}

$vmConfig = Set-AzVMOperatingSystem @osParams -Linux -DisablePasswordAuthentication

$imageParams = @{

VM = $vmConfig

PublisherName = "Canonical"

Offer = "ubuntu-24_04-lts"

Skus = "server"

Version = "latest"

}

$vmConfig = Set-AzVMSourceImage @imageParams

```

Use [Add-AzVMNetworkInterface](/powershell/module/az.compute/add-azvmnetworkinterface) to attach the NIC that you previously created to the VM.

```azurepowershell

# Get the network interface object

$nicParams = @{

ResourceGroupName = "test-rg"

Name = "nic-public"

}

$nic = Get-AzNetworkInterface @nicParams

$vmConfigParams = @{

VM = $vmConfig

Id = $nic.Id

}

$vmConfig = Add-AzVMNetworkInterface @vmConfigParams

```

Use [New-AzVM](/powershell/module/az.compute/new-azvm) to create the VM. The command will generate SSH keys for the virtual machine for login. Make note of the location of the private key. The private key is needed in later steps for connecting to the virtual machine with Azure Bastion.

```azurepowershell

$vmParams = @{

VM = $vmConfig

ResourceGroupName = "test-rg"

Location = "westus"

SshKeyName = "ssh-key"

}

New-AzVM @vmParams -GenerateSshKey

```

---

### Configure virtual machine network interfaces

The IP configuration of the primary network interface of the virtual machine is set to dynamic by default. Use the following example to change the primary network interface IP configuration to static and add a secondary network interface for the private interface of the NVA.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **vm-nva**.

1. In the **Overview** select **Stop** if the virtual machine is running.

1. Expand **Networking** then select **Network settings**.

1. In **Network settings** select the network interface name next to **Network Interface:**. The interface name is the virtual machine name and random numbers and letters. In this example, the interface name is **vm-nva271**.

1. In the network interface properties, select **IP configurations** in **Settings**.

1. Select the box next to **Enable IP forwarding**.

1. Select **Apply**.

1. When the apply action completes, select **ipconfig1**.

1. In **Private IP address settings** in **ipconfig1** select **Static**.

1. In **Private IP address** enter **10.0.253.10**.

1. Select **Save**.

1. When the save action completes, return to the networking configuration for **vm-nva**.

1. In **Network settings** of **vm-nva** select **Attach network interface**.

1. Select **Create and attach network interface**.

1. In **Create network interface** enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Resource group | Select **test-rg**. |

| **Network interface** |  |

| Name | Enter **nic-private**. |

| Subnet | Select **subnet-private (10.0.0.0/24)**. |

| NIC network security group | Select **Advanced**. |

| Configure network security group | Select **nsg-nva**. |

| Private IP address assignment | Select **Static**. |

| Private IP address | Enter **10.0.0.10**. |

1. Select **Create**.

1. Start the virtual machine.

# [**Powershell**](#tab/powershell)

Use [Set-AzNetworkInterface](/powershell/module/az.network/set-aznetworkinterface) to enable IP forwarding on the primary network interface.

```powershell

$nicParams = @{

ResourceGroupName = "test-rg"

Name = "nic-public"

}

$nic = Get-AzNetworkInterface @nicParams

$nic.EnableIPForwarding = $true

Set-AzNetworkInterface -NetworkInterface $nic

```

Use [Set-AzNetworkInterfaceIpConfig](/powershell/module/az.network/set-aznetworkinterfaceipconfig) to statically set the private IP address of the virtual machine for the public interface.

```powershell

$nicParams = @{

ResourceGroupName = "test-rg"

Name = "nic-public"

}

$nic = Get-AzNetworkInterface @nicParams

$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"

$nic.IpConfigurations[0].PrivateIpAddress = "10.0.253.10"

Set-AzNetworkInterface -NetworkInterface $nic

```

Use [Update-AzVM](/powershell/module/az.compute/update-azvm) to designate the **nic-public** interface as the primary interface.

```powershell

$vmParams = @{

ResourceGroupName = "test-rg"

Name = "vm-nva"

}

$vm = Get-AzVM @vmParams

$nicParams = @{

ResourceGroupName = "test-rg"

Name = "nic-public"

}

$nic = Get-AzNetworkInterface @nicParams

$vm.NetworkProfile.NetworkInterfaces | ForEach-Object {

$_.Primary = $false

}

$vm.NetworkProfile.NetworkInterfaces | Where-Object { $_.Id -eq $nic.Id } | ForEach-Object {

$_.Primary = $true

}

$updateParams = @{

ResourceGroupName = "test-rg"

VM = $vm

}

Update-AzVM @updateParams

```

Use [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface) to create the secondary network interface.

```powershell

$nicParams = @{

ResourceGroupName = "test-rg"

Name = "nic-private"

SubnetId = (Get-AzVirtualNetwork -ResourceGroupName "test-rg" -Name "vnet-hub").Subnets[0].Id

PrivateIpAddress = "10.0.0.10"

Location = "westus"

}

New-AzNetworkInterface @nicParams

```

Use [Stop-AzVM](/powershell/module/az.compute/stop-azvm) to shutdown and deallocate the virtual machine.

```powershell

$vmParams = @{

ResourceGroupName = "test-rg"

Name = "vm-nva"

Force = $true

}

Stop-AzVM @vmParams

```

Use [Add-AzVMNetworkInterface](/powershell/module/az.compute/add-azvmnetworkinterface) to attach the secondary network interface to the virtual machine.

```powershell

$vmParams = @{

ResourceGroupName = "test-rg"

Name = "vm-nva"

}

$vm = Get-AzVM @vmParams

$nicParams = @{

ResourceGroupName = "test-rg"

Name = "nic-private"

}

$nic = Get-AzNetworkInterface @nicParams

$vm = Add-AzVMNetworkInterface -VM $vm -Id $nic.Id

$updateParams = @{

ResourceGroupName = "test-rg"

VM = $vm

}

Update-AzVM @updateParams

```

Use [Start-AzVM](/powershell/module/az.compute/start-azvm) to start the virtual machine.

```powershell

$startVmParams = @{

ResourceGroupName = "test-rg"

Name = "vm-nva"

}

Start-AzVM @startVmParams

```

---

### Configure virtual machine software

The routing for the simulated NVA uses IP tables and internal NAT in the Ubuntu virtual machine. Connect to the NVA virtual machine with Azure Bastion to configure IP tables and the routing configuration.

1. In the [Azure portal](https://portal.azure.com), search for and select *virtual machines*.

1. On the **Virtual machines** page, select **vm-nva**.

1. On the VM's **Overview** page, select **Connect** then **Connect via Bastion**.

1. In the Bastion connection screen, change **Authentication Type** to **SSH Private Key from Local File**.

1. Enter the **Username** that you used when creating the virtual machine. In this example, the user is named **azureuser**, replace with the username you created.

1. In **Local File**, select the folder icon and browse to the private key file that was generated when you created the VM. The private key file is typically named `id_rsa` or `id_rsa.pem` or `ssh-key.pem`.

1. Select **Connect**.

1. Enter the following information at the prompt of the virtual machine to enable IP forwarding:

```bash

sudo nano /etc/sysctl.conf

```

1. In the Nano editor, remove the **`#`** from the line **`net.ipv4.ip_forward=1`**:

```bash

# Uncomment the next line to enable packet forwarding for IPv4

net.ipv4.ip_forward=1

```

Press **Ctrl + O** to save the file.

Press **Ctrl + X** to exit the editor.

1. Enter the following information to enable internal NAT in the virtual machine:

```bash

sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

sudo apt-get update

sudo apt install iptables-persistent

```

Select **Yes** twice.

```bash

sudo su

iptables-save > /etc/iptables/rules.v4

exit

```

1. Use Nano to edit the configuration with the following information:

```bash

sudo nano /etc/rc.local

```

Add the following line to the configuration file:

```bash

/sbin/iptables-restore < /etc/iptables/rules.v4

```

Press **Ctrl + O** to save the file.

Press **Ctrl + X** to exit the editor.

1. Reboot the virtual machine:

```bash

sudo reboot

```

## Create hub network route table

Route tables are used to overwrite Azure's default routing. Create a route table to force all traffic within the hub private subnet through the simulated NVA.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Route table**. Select **Route tables** in the search results.

1. Select **+ Create**.

1. In **Create Route table** enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |   |

| Region | Select **West US**. |

| Name | Enter **route-table-nat-hub**. |

| Propagate gateway routes | Leave the default of **Yes**. |

1. Select **Review + create**.

1. Select **Create**.

1. In the search box at the top of the portal, enter **Route table**. Select **Route tables** in the search results.

1. Select **route-table-nat-hub**.

1. Expand **Settings** then select **Routes**.

1. Select **+ Add** in **Routes**.

1. Enter or select the following information in **Add route**:

| Setting | Value |

| ------- | ----- |

| Route name | Enter **default-via-nat-hub**. |

| Destination type | Select **IP Addresses**. |

| Destination IP addresses/CIDR ranges | Enter **0.0.0.0/0**. |

| Next hop type | Select **Virtual appliance**. |

| Next hop address | Enter **10.0.0.10**. </br> **_This is the IP address you added to the private interface of the NVA in the previous steps._**. |

1. Select **Add**.

1. Select **Subnets** in **Settings**.

1. Select **+ Associate**.

1. Enter or select the following information in **Associate subnet**:

| Setting | Value |

| ------- | ----- |

| Virtual network | Select **vnet-hub (test-rg)**. |

| Subnet | Select **subnet-private**. |

1. Select **OK**.

# [**Powershell**](#tab/powershell)

Use [New-AzRouteTable](/powershell/module/az.network/new-azroutetable) to create the route table.

```powershell

$routeTableParams = @{

ResourceGroupName = "test-rg"

Name = "route-table-nat-hub"

Location = "westus"

}

New-AzRouteTable @routeTableParams

```

Use [Add-AzRouteConfig](/powershell/module/az.network/add-azrouteconfig) to create the route in the route table.

```powershell

$routeConfigParams = @{

Name = "default-via-nat-hub"

AddressPrefix = "0.0.0.0/0"

NextHopType = "VirtualAppliance"

NextHopIpAddress = "10.0.0.10"

}

$routeTableParams = @{

ResourceGroupName = "test-rg"

Name = "route-table-nat-hub"

}

$routeTable = Get-AzRouteTable @routeTableParams

$routeTable | Add-AzRouteConfig @routeConfigParams | Set-AzRouteTable

```

Use [Set-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/set-azvirtualnetworksubnetconfig) to associate the route table with the subnet.

```powershell

$vnetParams = @{

ResourceGroupName = "test-rg"

Name = "vnet-hub"

}

$vnet = Get-AzVirtualNetwork @vnetParams

$subnetParams = @{

VirtualNetwork = $vnet

Name = "subnet-private"

}

$subnet = Get-AzVirtualNetworkSubnetConfig @subnetParams

$subnet.RouteTable = $routeTable

Set-AzVirtualNetwork -VirtualNetwork $vnet

```

---

## Create spoke one virtual network

Create another virtual network in a different region for the first spoke of the hub and spoke network.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Virtual network**. Select **Virtual networks** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab of **Create virtual network**, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |   |

| Name | Enter **vnet-spoke-1**. |

| Region | Select **(US) South Central US**. |

1. Select **Next** to proceed to the **Security** tab.

1. Select **Next** to proceed to the **IP addresses** tab.

1. In the **IP Addresses** tab in **IPv4 address space**, select **Delete address space** to delete the address space that is auto populated.

1. Select **Add IPv4 address space**.

1. In **IPv4 address space** enter **10.1.0.0**. Leave the default of **/16 (65,536 addresses)** in the mask selection.

1. Select **+ Add a subnet**.

1. In **Add a subnet** enter or select the following information:

| Setting | Value |

| ------- | ----- |

| Subnet purpose | Leave the default **Default**. |

| Name | Enter **subnet-private**. |

| **IPv4** |   |

| IPv4 address range| Leave the default of **10.1.0.0/16**. |

| Starting address | Leave the default of **10.1.0.0**. |

| Size | Leave the default of **/24(256 addresses)**. |

1. Select **Add**.

1. Select **Review + create**.

1. Select **Create**.

# [**Powershell**](#tab/powershell)

Use [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork) to create the virtual network.

```powershell

$vnetParams = @{

ResourceGroupName = "test-rg"

Name = "vnet-spoke-1"

AddressPrefix = "10.1.0.0/16"

Location = "southcentralus"

}

New-AzVirtualNetwork @vnetParams

```

Use [Add-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/add-azvirtualnetworksubnetconfig) to create the subnet.

```powershell

$vnetParams = @{

ResourceGroupName = "test-rg"

Name = "vnet-spoke-1"

}

$vnet = Get-AzVirtualNetwork @vnetParams

$subnetParams = @{

VirtualNetwork = $vnet

Name = "subnet-private"

AddressPrefix = "10.1.0.0/24"

}

Add-AzVirtualNetworkSubnetConfig @subnetParams

Set-AzVirtualNetwork -VirtualNetwork $vnet

```

---

## Create peering between hub and spoke one

A virtual network peering is used to connect the hub to spoke one and spoke one to the hub. Use the following example to create a two-way network peering between the hub and spoke one.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Virtual network**. Select **Virtual networks** in the search results.

1. Select **vnet-hub**.

1. Expand **Settings**, then select **Peerings**.

1. Select **+ Add**.

1. Enter or select the following information in **Add peering**:

| Setting | Value |

| ------- | -----

| **Remote virtual network summary** |   |

| Peering link name | Enter **vnet-spoke-1-to-vnet-hub**. |

| Virtual network deployment model | Leave the default of **Resource manager**. |

| Subscription | Select your subscription. |

| Virtual network | Select **vnet-spoke-1 (test-rg)**. |

| **Remote virtual network peering settings** |   |

| Allow 'vnet-spoke-1' to access 'vnet-hub' | Leave the default of **Selected**. |

| Allow 'vnet-spoke-1' to receive forwarded traffic from 'vnet-hub' | Select the checkbox. |

| Allow gateway or route server in 'vnet-spoke-1' to forward traffic to 'vnet-hub' | Leave the default of **Unselected**. |

| Enable 'vnet-spoke-1' to use 'vnet-hub's' remote gateway or route server | Leave the default of **Unselected**. |

| **Local virtual network summary** |   |

| Peering link name | Enter **vnet-hub-to-vnet-spoke-1**. |

| **Local virtual network peering settings** |   |

| Allow 'vnet-hub' to access 'vnet-spoke-1' | Leave the default of **Selected**. |

| Allow 'vnet-hub' to receive forwarded traffic from 'vnet-spoke-1' | Select the checkbox. |

| Allow gateway or route server in 'vnet-hub' to forward traffic to 'vnet-spoke-1' | Leave the default of **Unselected**. |

| Enable 'vnet-hub' to use 'vnet-spoke-1's' remote gateway or route server | Leave the default of **Unselected**. |

1. Select **Add**.

1. Select **Refresh** and verify **Peering status** is **Connected**.

# [**Powershell**](#tab/powershell)

Use [Add-AzVirtualNetworkPeering](/powershell/module/az.network/add-azvirtualnetworkpeering) to create the peering from the hub to spoke one.

```powershell

# Create peering from hub to spoke one

$hubVnetParams = @{

ResourceGroupName = "test-rg"

Name = "vnet-hub"

}

$hubVnet = Get-AzVirtualNetwork @hubVnetParams

$spokeVnetParams = @{

ResourceGroupName = "test-rg"

Name = "vnet-spoke-1"

}

$spokeVnet = Get-AzVirtualNetwork @spokeVnetParams

$hubToSpokeParams = @{

Name = "vnet-hub-to-vnet-spoke-1"

VirtualNetwork = $hubVnet

RemoteVirtualNetworkId = $spokeVnet.Id

AllowForwardedTraffic = $true

}

Add-AzVirtualNetworkPeering @hubToSpokeParams

# Create peering from spoke one to hub

$spokeToHubParams = @{

Name = "vnet-spoke-1-to-vnet-hub"

VirtualNetwork = $spokeVnet

RemoteVirtualNetworkId = $hubVnet.Id

AllowForwardedTraffic = $true

}

Add-AzVirtualNetworkPeering @spokeToHubParams

```

---

## Create spoke one network route table

Create a route table to force all inter-spoke and internet egress traffic through the simulated NVA in the hub virtual network.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Route table**. Select **Route tables** in the search results.

1. Select **+ Create**.

1. In **Create Route table** enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |   |

| Region | Select **South Central US**. |

| Name | Enter **route-table-nat-spoke-1**. |

| Propagate gateway routes | Leave the default of **Yes**. |

1. Select **Review + create**.

1. Select **Create**.

1. In the search box at the top of the portal, enter **Route table**. Select **Route tables** in the search results.

1. Select **route-table-nat-spoke-1**.

1. Expand **Settings**, then select **Routes**.

1. Select **+ Add** in **Routes**.

1. Enter or select the following information in **Add route**:

| Setting | Value |

| ------- | ----- |

| Route name | Enter **default-via-nat-spoke-1**. |

| Destination type | Select **IP Addresses**. |

| Destination IP addresses/CIDR ranges | Enter **0.0.0.0/0**. |

| Next hop type | Select **Virtual appliance**. |

| Next hop address | Enter **10.0.0.10**. </br> **_This is the IP address you added to the private interface of the NVA in the previous steps._**. |

1. Select **Add**.

1. Select **Subnets** in **Settings**.

1. Select **+ Associate**.

1. Enter or select the following information in **Associate subnet**:

| Setting | Value |

| ------- | ----- |

| Virtual network | Select **vnet-spoke-1 (test-rg)**. |

| Subnet | Select **subnet-private**. |

1. Select **OK**.

# [**Powershell**](#tab/powershell)

Use [New-AzRouteTable](/powershell/module/az.network/new-azroutetable) to create the route table.

```powershell

$routeTableParams = @{

ResourceGroupName = "test-rg"

Name = "route-table-nat-spoke-1"

Location = "southcentralus"

}

New-AzRouteTable @routeTableParams

```

Use [Add-AzRouteConfig](/powershell/module/az.network/add-azrouteconfig) to create the route in the route table.

```powershell

$routeConfigParams = @{

Name = "default-via-nat-spoke-1"

AddressPrefix = "0.0.0.0/0"

NextHopType = "VirtualAppliance"

NextHopIpAddress = "10.0.0.10"

}

$routeTableParams = @{

ResourceGroupName = "test-rg"

Name = "route-table-nat-spoke-1"

}

$routeTable = Get-AzRouteTable @routeTableParams

$routeTable | Add-AzRouteConfig @routeConfigParams | Set-AzRouteTable

```

Use [Set-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/set-azvirtualnetworksubnetconfig) to associate the route table with the subnet.

```powershell

$vnetParams = @{

ResourceGroupName = "test-rg"

Name = "vnet-spoke-1"

}

$vnet = Get-AzVirtualNetwork @vnetParams

$subnetParams = @{

VirtualNetwork = $vnet

Name = "subnet-private"

}

$subnet = Get-AzVirtualNetworkSubnetConfig @subnetParams

$subnet.RouteTable = $routeTable

Set-AzVirtualNetwork -VirtualNetwork $vnet

```

---

## Create spoke one test virtual machine

A Windows Server 2022 virtual machine is used to test the outbound internet traffic through the NAT gateway and inter-spoke traffic in the hub and spoke network. Use the following example to create a Windows Server 2022 virtual machine.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **+ Create** then **Azure virtual machine**.

1. In **Create a virtual machine** enter or select the following information in the **Basics** tab:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |   |

| Virtual machine name | Enter **vm-spoke-1**. |

| Region | Select **(US) South Central US**. |

| Availability options | Select **No infrastructure redundancy required**. |

| Security type | Select **Standard**. |

| Image | Select **Windows Server 2022 Datacenter - x64 Gen2**. |

| VM architecture | Leave the default of **x64**. |

| Size | Select a size. |

| **Administrator account** |   |

| Authentication type | Select **Password**. |

| Username | Enter a username. |

| Password | Enter a password. |

| Confirm password | Reenter password. |

| **Inbound port rules** |  |

| Public inbound ports | Select **None**. |

1. Select **Next: Disks** then **Next: Networking**.

1. In the Networking tab, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Network interface** |   |

| Virtual network | Select **vnet-spoke-1**. |

| Subnet | Select **subnet-private (10.1.0.0/24)**. |

| Public IP | Select **None**. |

| NIC network security group | Select **Advanced**. |

| Configure network security group | Select **Create new**. </br> Enter **nsg-spoke-1**. |

| Inbound rules | Select **+ Add an inbound rule**. </br> Select **HTTP** in **Service**. </br> Select **Add**. </br> Select **OK**. |

1. Select **OK**.

1. Leave the rest of the options at the defaults and select **Review + create**.

1. Select **Create**.

# [**Powershell**](#tab/powershell)

Use [New-AzNetworkSecurityGroup](/powershell/module/az.network/new-aznetworksecuritygroup) to create the network security group.

```powershell

$nsgParams = @{

ResourceGroupName = "test-rg"

Name = "nsg-spoke-1"

Location = "southcentralus"

}

New-AzNetworkSecurityGroup @nsgParams

```

Use [New-AzNetworkSecurityRuleConfig](/powershell/module/az.network/new-aznetworksecurityruleconfig) to create an inbound NSG rule for HTTP.

```powershell

$nsgParams = @{

ResourceGroupName = "test-rg"

Name = "nsg-spoke-1"

}

$nsg = Get-AzNetworkSecurityGroup @nsgParams

$ruleParams = @{

Name = "allow-http"

Priority = 1000

Direction = "Inbound"

Access = "Allow"

Protocol = "Tcp"

SourceAddressPrefix = "*"

SourcePortRange = "*"

DestinationAddressPrefix = "*"

DestinationPortRange = "80"

}

$nsg | Add-AzNetworkSecurityRuleConfig @ruleParams

Set-AzNetworkSecurityGroup -NetworkSecurityGroup $nsg

```

Use [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface) to create the network interface.

```powershell

$nicParams = @{

ResourceGroupName = "test-rg"

Name = "nic-1"

SubnetId = (Get-AzVirtualNetwork -ResourceGroupName "test-rg" -Name "vnet-spoke-1").Subnets[0].Id

NetworkSecurityGroupId = (Get-AzNetworkSecurityGroup -ResourceGroupName "test-rg" -Name "nsg-spoke-1").Id

Location = "southcentralus"

}

New-AzNetworkInterface @nicParams

```

Use [Get-Credential](/powershell/module/microsoft.powershell.security/get-credential) to set a user name and password for the VM and store them in the `$cred` variable.

```azurepowershell

$cred = Get-Credential

```

Use [New-AzVMConfig](/powershell/module/az.compute/new-azvmconfig) to define a VM.

```azurepowershell

$vmConfigParams = @{

VMName = "vm-spoke-1"

VMSize = "Standard_DS4_v2"

}

$vmConfig = New-AzVMConfig @vmConfigParams

```

Use [Set-AzVMOperatingSystem](/powershell/module/az.compute/set-azvmoperatingsystem) and [Set-AzVMSourceImage](/powershell/module/az.compute/set-azvmsourceimage) to create the rest of the VM configuration. The following example creates a Windows Server virtual machine:

```azurepowershell

$osParams = @{

VM = $vmConfig

ComputerName = "vm-spoke-1"

Credential = $cred

}

$vmConfig = Set-AzVMOperatingSystem @osParams -Windows

$imageParams = @{

VM = $vmConfig

PublisherName = "MicrosoftWindowsServer"

Offer = "WindowsServer"

Skus = "2022-Datacenter"

Version = "latest"

}

$vmConfig = Set-AzVMSourceImage @imageParams

```

Use [Add-AzVMNetworkInterface](/powershell/module/az.compute/add-azvmnetworkinterface) to attach the NIC that you previously created to the VM.

```azurepowershell

# Get the network interface object

$nicParams = @{

ResourceGroupName = "test-rg"

Name = "nic-1"

}

$nic = Get-AzNetworkInterface @nicParams

$vmConfigParams = @{

VM = $vmConfig

Id = $nic.Id

}

$vmConfig = Add-AzVMNetworkInterface @vmConfigParams

```

Use [New-AzVM](/powershell/module/az.compute/new-azvm) to create the VM.

```azurepowershell

$vmParams = @{

VM = $vmConfig

ResourceGroupName = "test-rg"

Location = "southcentralus"

}

New-AzVM @vmParams

```

---

Wait for the virtual machine to finishing deploying before continuing to the next steps.

## Install IIS on spoke one test virtual machine

IIS is installed on the Windows Server 2022 virtual machine to test outbound internet traffic through the NAT gateway and inter-spoke traffic in the hub and spoke network.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **vm-spoke-1**.

1. Expand **Operations** then select **Run command**.

1. Select **RunPowerShellScript**.

1. Enter the following script in **Run Command Script**:

```powershell

# Install IIS server role

Install-WindowsFeature -name Web-Server -IncludeManagementTools

# Remove default htm file

Remove-Item  C:\inetpub\wwwroot\iisstart.htm

# Add a new htm file that displays server name

Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)

```

1. Select **Run**.

1. Wait for the script to complete before continuing to the next step. It can take a few minutes for the script to complete.

1. When the script completes, the **Output** displays the following:

```output

Success Restart Needed Exit Code      Feature Result

------- -------------- ---------      --------------

True    No             Success        {Common HTTP Features, Default Document, D...

```

# [**Powershell**](#tab/powershell)

Use [Set-AzVMExtension](/powershell/module/az.compute/set-azvmextension) to install IIS on the virtual machine.

```powershell

$vmExtensionParams = @{

ResourceGroupName = "test-rg"

VMName = "vm-spoke-1"

Name = "CustomScriptExtension"

Publisher = "Microsoft.Compute"

Type = "CustomScriptExtension"

TypeHandlerVersion = "1.10"

Settings = @{

"commandToExecute" = "powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path 'C:\inetpub\wwwroot\default.htm' -Value vm-spoke-1"

}

}

Set-AzVMExtension @vmExtensionParams

```

---

## Create the second spoke virtual network

Create the second virtual network for the second spoke of the hub and spoke network.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Virtual network**. Select **Virtual networks** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab of **Create virtual network**, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |   |

| Name | Enter **vnet-spoke-2**. |

| Region | Select **(US) West US 2**. |

1. Select **Next** to proceed to the **Security** tab.

1. Select **Next** to proceed to the **IP addresses** tab.

1. In the **IP Addresses** tab in **IPv4 address space**, select **Delete address space** to delete the address space that is auto populated.

1. Select **Add IPv4 address space**.

1. In **IPv4 address space** enter **10.2.0.0**. Leave the default of **/16 (65,536 addresses)** in the mask selection.

1. Select **+ Add a subnet**.

1. In **Add a subnet** enter or select the following information:

| Setting | Value |

| ------- | ----- |

| Subnet purpose | Leave the default **Default**. |

| Name | Enter **subnet-private**. |

| **IPv4** |   |

| IPv4 address range | Leave the default of **10.2.0.0/16**. |

| Starting address | Leave the default of **10.2.0.0**. |

| Size | Leave the default of **/24(256 addresses)**. |

1. Select **Add**.

1. Select **Review + create**.

1. Select **Create**.

# [**Powershell**](#tab/powershell)

Use [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork) to create the virtual network.

```powershell

$vnetParams = @{

ResourceGroupName = "test-rg"

Name = "vnet-spoke-2"

AddressPrefix = "10.2.0.0/16"

Location = "westus2"

}

New-AzVirtualNetwork @vnetParams

```

Use [Add-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/add-azvirtualnetworksubnetconfig) to create the subnet.

```powershell

$vnetParams = @{

ResourceGroupName = "test-rg"

Name = "vnet-spoke-2"

}

$vnet = Get-AzVirtualNetwork @vnetParams

$subnetParams = @{

VirtualNetwork = $vnet

Name = "subnet-private"

AddressPrefix = "10.2.0.0/24"

}

Add-AzVirtualNetworkSubnetConfig @subnetParams

Set-AzVirtualNetwork -VirtualNetwork $vnet

```

---

## Create peering between hub and spoke two

Create a two-way virtual network peer between the hub and spoke two.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Virtual network**. Select **Virtual networks** in the search results.

1. Select **vnet-hub**.

1. Select **Peerings** in **Settings**.

1. Select **+ Add**.

1. In the search box at the top of the portal, enter **Virtual network**. Select **Virtual networks** in the search results.

1. Select **vnet-hub**.

1. Select **Peerings** in **Settings**.

1. Select **+ Add**.

1. Enter or select the following information in **Add peering**:

| Setting | Value |

| ------- | -----

| **Remote virtual network summary** |   |

| Peering link name | Enter **vnet-spoke-2-to-vnet-hub**. |

| Virtual network deployment model | Leave the default of **Resource manager**. |

| Subscription | Select your subscription. |

| Virtual network | Select **vnet-spoke-2 (test-rg)**. |

| **Remote virtual network peering settings** |   |

| Allow 'vnet-spoke-2' to access 'vnet-hub' | Leave the default of **Selected**. |

| Allow 'vnet-spoke-2' to receive forwarded traffic from 'vnet-hub' | Select the checkbox. |

| Allow gateway or route server in 'vnet-spoke-2' to forward traffic to 'vnet-hub' | Leave the default of **Unselected**. |

| Enable 'vnet-spoke-2' to use 'vnet-hub's' remote gateway or route server | Leave the default of **Unselected**. |

| **Local virtual network summary** |   |

| Peering link name | Enter **vnet-hub-to-vnet-spoke-2**. |

| **Local virtual network peering settings** |   |

| Allow 'vnet-hub' to access 'vnet-spoke-2' | Leave the default of **Selected**. |

| Allow 'vnet-hub' to receive forwarded traffic from 'vnet-spoke-2' | Select the checkbox. |

| Allow gateway or route server in 'vnet-hub' to forward traffic to 'vnet-spoke-2' | Leave the default of **Unselected**. |

| Enable 'vnet-hub' to use 'vnet-spoke-2's' remote gateway or route server | Leave the default of **Unselected**. |

1. Select **Add**.

1. Select **Refresh** and verify **Peering status** is **Connected**.

# [**Powershell**](#tab/powershell)

Use [Add-AzVirtualNetworkPeering](/powershell/module/az.network/add-azvirtualnetworkpeering) to create the peering from the hub to spoke two.

```powershell

# Create peering from hub to spoke two

$hubVnetParams = @{

ResourceGroupName = "test-rg"

Name = "vnet-hub"

}

$hubVnet = Get-AzVirtualNetwork @hubVnetParams

$spokeVnetParams = @{

ResourceGroupName = "test-rg"

Name = "vnet-spoke-2"

}

$spokeVnet = Get-AzVirtualNetwork @spokeVnetParams

$hubToSpokeParams = @{

Name = "vnet-hub-to-vnet-spoke-2"

VirtualNetwork = $hubVnet

RemoteVirtualNetworkId = $spokeVnet.Id

AllowForwardedTraffic = $true

}

Add-AzVirtualNetworkPeering @hubToSpokeParams

# Create peering from spoke two to hub

$spokeToHubParams = @{

Name = "vnet-spoke-2-to-vnet-hub"

VirtualNetwork = $spokeVnet

RemoteVirtualNetworkId = $hubVnet.Id

AllowForwardedTraffic = $true

}

Add-AzVirtualNetworkPeering @spokeToHubParams

```

---

## Create spoke two network route table

Create a route table to force all outbound internet and inter-spoke traffic through the simulated NVA in the hub virtual network.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Route table**. Select **Route tables** in the search results.

1. Select **+ Create**.

1. In **Create Route table** enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |   |

| Region | Select **West US 2**. |

| Name | Enter **route-table-nat-spoke-2**. |

| Propagate gateway routes | Leave the default of **Yes**. |

1. Select **Review + create**.

1. Select **Create**.

1. In the search box at the top of the portal, enter **Route table**. Select **Route tables** in the search results.

1. Select **route-table-nat-spoke-2**.

1. In **Settings** select **Routes**.

1. Select **+ Add** in **Routes**.

1. Enter or select the following information in **Add route**:

| Setting | Value |

| ------- | ----- |

| Route name | Enter **default-via-nat-spoke-2**. |

| Destination type | Select **IP Addresses**. |

| Destination IP addresses/CIDR ranges | Enter **0.0.0.0/0**. |

| Next hop type | Select **Virtual appliance**. |

| Next hop address | Enter **10.0.0.10**. </br> **_This is the IP address you added to the private interface of the NVA in the previous steps._**. |

1. Select **Add**.

1. Select **Subnets** in **Settings**.

1. Select **+ Associate**.

1. Enter or select the following information in **Associate subnet**:

| Setting | Value |

| ------- | ----- |

| Virtual network | Select **vnet-spoke-2 (test-rg)**. |

| Subnet | Select **subnet-private**. |

1. Select **OK**.

# [**Powershell**](#tab/powershell)

Use [New-AzRouteTable](/powershell/module/az.network/new-azroutetable) to create the route table.

```powershell

$routeTableParams = @{

ResourceGroupName = "test-rg"

Name = "route-table-nat-spoke-2"

Location = "westus2"

}

New-AzRouteTable @routeTableParams

```

Use [Add-AzRouteConfig](/powershell/module/az.network/add-azrouteconfig) to create the route in the route table.

```powershell

$routeParams = @{

Name = "default-via-nat-spoke-2"

AddressPrefix = "0.0.0.0/0"

NextHopType = "VirtualAppliance"

NextHopIpAddress = "10.0.0.10"

}

$routeTableParams = @{

ResourceGroupName = "test-rg"

Name = "route-table-nat-spoke-2"

}

$routeTable = Get-AzRouteTable @routeTableParams

$routeTable | Add-AzRouteConfig @routeParams | Set-AzRouteTable

```

Use [Set-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/set-azvirtualnetworksubnetconfig) to associate the route table with the subnet.

```powershell

$vnetParams = @{

ResourceGroupName = "test-rg"

Name = "vnet-spoke-2"

}

$vnet = Get-AzVirtualNetwork @vnetParams

$subnetParams = @{

VirtualNetwork = $vnet

Name = "subnet-private"

}

$subnet = Get-AzVirtualNetworkSubnetConfig @subnetParams

$subnet.RouteTable = $routeTable

Set-AzVirtualNetwork -VirtualNetwork $vnet

```

---

## Create spoke two test virtual machine

Create a Windows Server 2022 virtual machine for the test virtual machine in spoke two.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **+ Create** then **Azure virtual machine**.

1. In **Create a virtual machine** enter or select the following information in the **Basics** tab:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |   |

| Virtual machine name | Enter **vm-spoke-2**. |

| Region | Select **(US) West US 2**. |

| Availability options | Select **No infrastructure redundancy required**. |

| Security type | Select **Standard**. |

| Image | Select **Windows Server 2022 Datacenter - x64 Gen2**. |

| VM architecture | Leave the default of **x64**. |

| Size | Select a size. |

| **Administrator account** |   |

| Authentication type | Select **Password**. |

| Username | Enter a username. |

| Password | Enter a password. |

| Confirm password | Reenter password. |

| **Inbound port rules** |  |

| Public inbound ports | Select **None**. |

1. Select **Next: Disks** then **Next: Networking**.

1. In the Networking tab, enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Network interface** |   |

| Virtual network | Select **vnet-spoke-2**. |

| Subnet | Select **subnet-private (10.2.0.0/24)**. |

| Public IP | Select **None**. |

| NIC network security group | Select **Advanced**. |

| Configure network security group | Select **Create new**. </br> Enter **nsg-spoke-2**. |

| Inbound rules | Select **+ Add an inbound rule**. </br> Select **HTTP** in **Service**. </br> Select **Add**. </br> Select **OK**. |

1. Leave the rest of the options at the defaults and select **Review + create**.

1. Select **Create**.

# [**Powershell**](#tab/powershell)

Use [New-AzNetworkSecurityGroup](/powershell/module/az.network/new-aznetworksecuritygroup) to create the network security group.

```powershell

$nsgParams = @{

ResourceGroupName = "test-rg"

Name = "nsg-spoke-2"

Location = "westus2"

}

New-AzNetworkSecurityGroup @nsgParams

```

Use [New-AzNetworkSecurityRuleConfig](/powershell/module/az.network/new-aznetworksecurityruleconfig) to create an inbound NSG rule for HTTP.

```powershell

$ruleParams = @{

Name = "allow-http"

Priority = 1000

Direction = "Inbound"

Access = "Allow"

Protocol = "Tcp"

SourceAddressPrefix = "*"

SourcePortRange = "*"

DestinationAddressPrefix = "*"

DestinationPortRange = "80"

}

$nsg = Get-AzNetworkSecurityGroup -ResourceGroupName "test-rg" -Name "nsg-spoke-2"

$nsg | Add-AzNetworkSecurityRuleConfig @ruleParams

Set-AzNetworkSecurityGroup -NetworkSecurityGroup $nsg

```

Use [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface) to create the network interface.

```powershell

$nicParams = @{

ResourceGroupName = "test-rg"

Name = "nic-2"

SubnetId = (Get-AzVirtualNetwork -ResourceGroupName "test-rg" -Name "vnet-spoke-2").Subnets[0].Id

NetworkSecurityGroupId = (Get-AzNetworkSecurityGroup -ResourceGroupName "test-rg" -Name "nsg-spoke-2").Id

Location = "westus2"

}

New-AzNetworkInterface @nicParams

```

Use [Get-Credential](/powershell/module/microsoft.powershell.security/get-credential) to set a user name and password for the VM and store them in the `$cred` variable.

```azurepowershell

$cred = Get-Credential

```

Use [New-AzVMConfig](/powershell/module/az.compute/new-azvmconfig) to define a VM.

```azurepowershell

$vmConfigParams = @{

VMName = "vm-spoke-2"

VMSize = "Standard_DS4_v2"

}

$vmConfig = New-AzVMConfig @vmConfigParams

```

Use [Set-AzVMOperatingSystem](/powershell/module/az.compute/set-azvmoperatingsystem) and [Set-AzVMSourceImage](/powershell/module/az.compute/set-azvmsourceimage) to create the rest of the VM configuration. The following example creates a Windows Server virtual machine:

```azurepowershell

$osParams = @{

VM = $vmConfig

ComputerName = "vm-spoke-2"

Credential = $cred

}

$vmConfig = Set-AzVMOperatingSystem @osParams -Windows

$imageParams = @{

VM = $vmConfig

PublisherName = "MicrosoftWindowsServer"

Offer = "WindowsServer"

Skus = "2022-Datacenter"

Version = "latest"

}

$vmConfig = Set-AzVMSourceImage @imageParams

```

Use [Add-AzVMNetworkInterface](/powershell/module/az.compute/add-azvmnetworkinterface) to attach the NIC that you previously created to the VM.

```azurepowershell

# Get the network interface object

$nicParams = @{

ResourceGroupName = "test-rg"

Name = "nic-2"

}

$nic = Get-AzNetworkInterface @nicParams

$vmConfigParams = @{

VM = $vmConfig

Id = $nic.Id

}

$vmConfig = Add-AzVMNetworkInterface @vmConfigParams

```

Use [New-AzVM](/powershell/module/az.compute/new-azvm) to create the VM.

```azurepowershell

$vmParams = @{

VM = $vmConfig

ResourceGroupName = "test-rg"

Location = "westus2"

}

New-AzVM @vmParams

```

---

Wait for the virtual machine to finish deploying before continuing to the next steps.

## Install IIS on spoke two test virtual machine

IIS is installed on the Windows Server 2022 virtual machine to test outbound internet traffic through the NAT gateway and inter-spoke traffic in the hub and spoke network.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **vm-spoke-2**.

1. In **Operations**, select **Run command**.

1. Select **RunPowerShellScript**.

1. Enter the following script in **Run Command Script**:

```powershell

# Install IIS server role

Install-WindowsFeature -name Web-Server -IncludeManagementTools

# Remove default htm file

Remove-Item  C:\inetpub\wwwroot\iisstart.htm

# Add a new htm file that displays server name

Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)

```

1. Select **Run**.

1. Wait for the script to complete before continuing to the next step. It can take a few minutes for the script to complete.

1. When the script completes, the **Output*** displays the following:

```output

Success Restart Needed Exit Code      Feature Result

------- -------------- ---------      --------------

True    No             Success        {Common HTTP Features, Default Document, D...

```

# [**Powershell**](#tab/powershell)

Use [Set-AzVMExtension](/powershell/module/az.compute/set-azvmextension) to install IIS on the virtual machine.

```powershell

$vmExtensionParams = @{

ResourceGroupName = "test-rg"

VMName = "vm-spoke-2"

Name = "CustomScriptExtension"

Publisher = "Microsoft.Compute"

Type = "CustomScriptExtension"

TypeHandlerVersion = "1.10"

Settings = @{

"commandToExecute" = "powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path 'C:\inetpub\wwwroot\default.htm' -Value vm-spoke-2"

}

}

Set-AzVMExtension @vmExtensionParams

```

---

## Test NAT gateway

To verify that the outbound internet traffic is leaving the NAT gateway, connect to the Windows Server 2022 virtual machines you created in the previous steps.

### Obtain NAT gateway public IP address

Obtain the NAT gateway public IP address for verification of the steps later in the article.

1. Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).

1. In the search box at the top of the portal, enter **Public IP**. Select **Public IP addresses** in the search results.

1. Select **public-ip-nat**.

1. Make note of value in **IP address**. The example used in this article is **203.0.113.25**.

### Test NAT gateway from spoke one

Use Microsoft Edge on the Windows Server 2022 virtual machine to connect to https://whatsmyip.com to verify the functionality of the NAT gateway.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **vm-spoke-1**.

1. In **Overview**, select **Connect** then **Connect via Bastion**.

1. Enter the username and password you entered when the virtual machine was created.

1. Select **Connect**.

1. Open **Microsoft Edge** when the desktop finishes loading.

1. In the address bar, enter **https://whatsmyip.com**.

1. Verify the outbound IP address displayed is the same as the IP of the NAT gateway you obtained previously.

1. Leave the bastion connection open to **vm-spoke-1**.

### Test NAT gateway from spoke two

Use Microsoft Edge on the Windows Server 2022 virtual machine to connect to https://whatsmyip.com to verify the functionality of the NAT gateway.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **vm-spoke-2**.

1. In **Overview**, select **Connect** then **Connect via Bastion**.

1. Enter the username and password you entered when the virtual machine was created.

1. Select **Connect**.

1. Open **Microsoft Edge** when the desktop finishes loading.

1. In the address bar, enter **https://whatsmyip.com**.

1. Verify the outbound IP address displayed is the same as the IP of the NAT gateway you obtained previously.

1. Leave the bastion connection open to **vm-spoke-2**.

## Test routing between the spokes

Traffic from spoke one to spoke two and spoke two to spoke one route through the simulated NVA in the hub virtual network. Use the following examples to verify the routing between spokes of the hub and spoke network.

### Test routing from spoke one to spoke two

Use Microsoft Edge to connect to the web server on **vm-spoke-2** you installed in the previous steps.

1. Return to the open bastion connection to **vm-spoke-1**.

1. Open **Microsoft Edge** if it's not open.

1. In the address bar, enter **10.2.0.4**.

1. Verify the IIS page is displayed from **vm-spoke-2**.

1. Close the bastion connection to **vm-spoke-1**.

### Test routing from spoke two to spoke one

Use Microsoft Edge to connect to the web server on **vm-spoke-1** you installed in the previous steps.

1. Return to the open bastion connection to **vm-spoke-2**.

1. Open **Microsoft Edge** if it's not open.

1. In the address bar, enter **10.1.0.4**.

1. Verify the IIS page is displayed from **vm-spoke-1**.

1. Close the bastion connection to **vm-spoke-1**.

# [**Portal**](#tab/portal)

[!INCLUDE [portal-clean-up.md](~/reusable-content/ce-skilling/azure/includes/portal-clean-up.md)]

# [**Powershell**](#tab/powershell)

Use [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) to delete the resource group.

```powershell

$rgParams = @{

Name = "test-rg"

Force = $true

}

Remove-AzResourceGroup @rgParams

```

---

## Next steps

Advance to the next article to learn how to use an Azure Gateway Load Balancer for highly available network virtual appliances:

> [!div class="nextstepaction"]

> [Gateway Load Balancer](../load-balancer/gateway-overview.md)


# Tutorial Hub Spoke Nat Firewall

# Integrate NAT gateway with Azure Firewall in a hub and spoke network for outbound connectivity

In this tutorial, you learn how to integrate a NAT gateway with Azure Firewall in a hub and spoke network for enhanced outbound connectivity and scalability.

Azure Firewall provides [2,496 SNAT ports per public IP address](../firewall/integrate-with-nat-gateway.md) configured per backend Virtual Machine Scale Set instance (minimum of two instances). You can associate up to 250 public IP addresses to Azure Firewall. Depending on your architecture requirements and traffic patterns, you might require more SNAT ports than what Azure Firewall can provide. You might also require the use of fewer public IPs while also requiring more SNAT ports. A better method for outbound connectivity is to use NAT gateway. NAT gateway provides 64,512 SNAT ports per public IP address and can be used with up to 16 public IP addresses.

NAT gateway can be integrated with Azure Firewall by configuring NAT gateway directly to the Azure Firewall subnet. This association provides a more scalable method of outbound connectivity. For production deployments, a hub and spoke network is recommended, where the firewall is in its own virtual network. The workload servers are peered virtual networks in the same region as the hub virtual network where the firewall resides. In this architectural setup, NAT gateway can provide outbound connectivity from the hub virtual network for all spoke virtual networks peered.

>[!NOTE]

> While you can deploy NAT Gateway in a hub and spoke virtual network architecture as described in this tutorial, NAT Gateway isn't supported in the hub virtual network of a vWAN architecture. To use in a vWAN architecture, NAT Gateway must be configured directly to the spoke virtual networks associated with the secured virtual hub (vWAN). For more information about Azure Firewall architecture options, see [What are the Azure Firewall Manager architecture options?](/azure/firewall-manager/vhubs-and-vnets)

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create a hub virtual network and deploy an Azure Firewall and Azure Bastion during deployment

> * Create a NAT gateway and associate it with the firewall subnet in the hub virtual network

> * Create a spoke virtual network

> * Create a virtual network peering

> * Create a route table for the spoke virtual network

> * Create a firewall policy for the hub virtual network

> * Create a virtual machine to test the outbound connectivity through the NAT gateway

## Prerequisites

# [Portal](#tab/portal)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

# [PowerShell](#tab/powershell)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

[!INCLUDE [cloud-shell-try-it.md](~/reusable-content/ce-skilling/azure/includes/cloud-shell-try-it.md)]

If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 1.0.0 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell). If you're running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

---

## Create a resource group

Create a resource group to contain all resources for this quickstart.

# [**Portal**](#tab/portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the portal enter **Resource group**. Select **Resource groups** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab of **Create a resource group**, enter, or select the following information.

| Setting | Value |

| ------- | ----- |

| Subscription | Select your subscription|

| Resource group | test-rg |

| Region | **West US** |

1. Select **Review + create**.

1. Select **Create**.

# [**Powershell**](#tab/powershell)

Create a resource group with [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup). An Azure resource group is a logical container into which Azure resources are deployed and managed.

The following example creates a resource group named **test-rg** in the **westus** location:

```azurepowershell-interactive

$rsg = @{

Name = 'test-rg'

Location = 'westus'

}

New-AzResourceGroup @rsg

```

---

## Create the hub virtual network

The hub virtual network contains the firewall subnet that is associated with the Azure Firewall and NAT gateway. Use the following example to create the hub virtual network.

# [**Portal**](#tab/portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the Azure portal, enter **Virtual network**. Select **Virtual networks** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create virtual network**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| Name | Enter **vnet-hub**. |

| Region | Select your region. This example uses **West US**. |

1. Select the **IP Addresses** tab, or select **Next: Security**, then **Next: IP Addresses**.

1. In **Subnets** select the **default** subnet.

1. Enter or select the following information in **Edit subnet**.

| Setting | Value |

| ------- | ----- |

| Subnet purpose | Leave the default. |

| Name | Enter **subnet-1**. |

1. Leave the rest of the settings as default, then select **Save**.

1. Select **+ Add a subnet**.

1. In **Add a subnet** enter or select the following information.

| Setting | Value |

| ------- | ----- |

| Subnet purpose | Select **Azure Bastion**. |

1. Leave the rest of the settings as default, then select **Add**.

1. Select **+ Add a subnet**.

1. In **Add a subnet** enter or select the following information.

| Setting | Value |

| ------- | ----- |

| Subnet purpose | Select **Azure Firewall**. |

1. Leave the rest of the settings as default, then select **Add**.

1. Select **Review + create**, then select **Create**.

# [**PowerShell**](#tab/powershell)

Use [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork) to create the hub virtual network.

```azurepowershell

# Create hub virtual network

$vnetParams = @{

ResourceGroupName = 'test-rg'

Location = 'westus'

Name = 'vnet-hub'

AddressPrefix = '10.0.0.0/16'

}

$hubVnet = New-AzVirtualNetwork @vnetParams

```

Use [Add-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/add-azvirtualnetworksubnetconfig) to create a subnet for Azure Firewall and Azure Bastion.

```azurepowershell

# Create default subnet

$subnetParams = @{

Name = 'subnet-1'

AddressPrefix = '10.0.0.0/24'

VirtualNetwork = $hubVnet

}

Add-AzVirtualNetworkSubnetConfig @subnetParams

# Create subnet for Azure Firewall

$subnetParams = @{

Name = 'AzureFirewallSubnet'

AddressPrefix  = '10.0.1.64/26'

VirtualNetwork = $hubVnet

}

Add-AzVirtualNetworkSubnetConfig @subnetParams

# Create subnet for Azure Bastion

$subnetParams = @{

Name = 'AzureBastionSubnet'

AddressPrefix  = '10.0.1.0/26'

VirtualNetwork = $hubVnet

}

Add-AzVirtualNetworkSubnetConfig @subnetParams

```

Use [Set-AzVirtualNetwork](/powershell/module/az.network/set-azvirtualnetwork) to update the virtual network.

```azurepowershell

# Create the virtual network

$hubVnet | Set-AzVirtualNetwork

```

---

## Create Azure Bastion host

Azure Bastion provides secure RDP and SSH connectivity to virtual machines over TLS without requiring public IP addresses on the VMs.

# [**Portal**](#tab/portal)

1. In the search box at the top of the Azure portal, enter **Bastion**. Select **Bastions** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create a Bastion**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| Name | Enter **bastion**. |

| Region | Select your region. This example uses **West US**. |

| Tier | Select **Developer**. |

| Virtual network | Select **vnet-1**. |

| Subnet | Select **AzureBastionSubnet**. |

1. Select **Review + create**, then select **Create**.

# [**Powershell**](#tab/powershell)

Use [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) to create a public IP for Azure Bastion.

```azurepowershell

# Create public IP for Azure Bastion

$publicIpBastionParams = @{

ResourceGroupName = 'test-rg'

Location = 'westus'

Name = 'public-ip-bastion'

Sku = 'Standard'

AllocationMethod = 'Static'

Zone = 1, 2, 3

}

$publicIpBastion = New-AzPublicIpAddress @publicIpBastionParams

```

Use [New-AzBastion](/powershell/module/az.network/new-azbastion) to create Azure Bastion.

```azurepowershell

# Create Azure Bastion

$bastionParams = @{

ResourceGroupName = "test-rg"

Name = "bastion"

VirtualNetworkName = "vnet-hub"

PublicIpAddressName = "public-ip-bastion"

PublicIPAddressRgName = "test-rg"

VirtualNetworkRgName = "test-rg"

Sku = "Basic"

}

New-AzBastion @bastionParams

```

---

## Create Azure Firewall

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Firewall**. Select **Firewalls** in the search results.

1. Select **+ Create**.

1. On the **Create a Firewall** page, use the following table to configure the firewall:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |   |

| Name | Enter **firewall**. |

| Region | Select **West US**. |

| Availability zone | Accept the default **None**. |

| Firewall SKU | Select **Standard**. |

| Firewall management | Select **Use a Firewall Policy to manage this firewall**. |

| Firewall policy | Select **Add new**.</br>Name: Enter **firewall-policy**.</br>Region: Select **West US**.</br>Policy tier: **Standard**.</br>Select **OK**. |

| **Choose a virtual network** |   |

| Virtual network | Select **Use existing**. |

| Virtual network | Select **vnet-hub**. |

| **Public IP address** |   |

| Public IP address | Select **Add new**.</br>Name: Enter **public-ip-firewall**.</br>SKU: **Standard**.</br>Assignment: **Static**.</br> Availability zone: **Zone-redundant**.</br>Select **OK**. |

1. Accept the other default values, then select **Review + create**.

1. Review the summary, and then select **Create** to create the firewall.

The firewall takes a few minutes to deploy.

1. After deployment completes, go to the **test-rg** resource group, and select the **firewall** resource.

1. Note the firewall private and public IP addresses. You use these addresses later.

# [**PowerShell**](#tab/powershell)

Use [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) to create a public IP for Azure Firewall.

```azurepowershell

# Create public IP for Azure Firewall

$publicIpFirewallParams = @{

ResourceGroupName = 'test-rg'

Location = 'westus'

Name = 'public-ip-firewall'

AllocationMethod  = 'Static'

Sku = 'Standard'

Zone = 1, 2, 3

}

$publicIpFirewall = New-AzPublicIpAddress @publicIpFirewallParams

```

Use [New-AzFirewallPolicy](/powershell/module/az.network/new-azfirewallpolicy) to create a firewall policy.

```azurepowershell

# Create firewall policy

$firewallPolicyParams = @{

ResourceGroupName = 'test-rg'

Location = 'westus'

Name = 'firewall-policy'

}

$firewallPolicy = New-AzFirewallPolicy @firewallPolicyParams

```

Use [New-AzFirewall](/powershell/module/az.network/new-azfirewall) to create Azure Firewall.

```azurepowershell

# Create Azure Firewall

$firewallParams = @{

ResourceGroupName = 'test-rg'

Location = 'westus'

Name = 'firewall'

VirtualNetworkName = 'vnet-hub'

PublicIpName = 'public-ip-firewall'

FirewallPolicyId = $firewallPolicy.Id

}

$firewall = New-AzFirewall @firewallParams

```

---

## Create the NAT gateway

All outbound internet traffic traverses the NAT gateway to the internet. Use the following example to create a NAT gateway for the hub and spoke network and associate it with the **AzureFirewallSubnet**.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Public IP address**. Select **Public IP addresses** in the search results.

1. Select **+ Create**.

1. Enter the following information in **Create public IP address**.

| Setting | Value |

| ------- | ----- |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| Region | Select **West US**. |

| Name | Enter **public-ip-nat**. |

| IP version | Select **IPv4**. |

| SKU | Select **Standard**. |

| Availability zone | Select **Zone-redundant**. |

| Tier | Select **Regional**. |

1. Select **Review + create** and then select **Create**.

> [!NOTE]

> A Standard V2 Public IP address can only be associated with a Standard V2 NAT Gateway and not any other services.

1. In the search box at the top of the portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **+ Create**.

1. Enter or select the following information in the **Basics** tab of **Create network address translation (NAT) gateway**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |  |

| NAT gateway name | Enter **nat-gateway**. |

| Region | Select **West US**. |

| SKU | Select **Standard**. |

| TCP idle timeout (minutes) | Leave the default of **4**. |

1. Select **Next**.

1. In the **Outbound IP** tab, select **+ Add public IP addresses or prefixes**.

10. In **Add public IP addresses or prefixes**, select **Public IP addresses**. Select the public IP address you created earlier, **public-ip-nat**.

11. Select **Next**.

12. In the **Networking** tab, in **Virtual network**, select **vnet-hub**.

13. Leave the checkbox for **Default to all subnets** unchecked.

14. In **Select specific subnets**, select **AzureFirewallSubnet**.

15. Select **Review + create**, then select **Create**.

# [**PowerShell**](#tab/powershell)

Use [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) to create a zone redundant IPv4 public IP address for the NAT gateway.

```azurepowershell

## Create public IP address for NAT gateway ##

$ip = @{

Name = 'public-ip-nat'

ResourceGroupName = 'test-rg'

Location = 'westus'

Sku = 'Standard'

AllocationMethod = 'Static'

IpAddressVersion = 'IPv4'

Zone = 1,2,3

}

$publicIPIPv4 = New-AzPublicIpAddress @ip

```

> [!NOTE]

> A Standard V2 Public IP address can only be associated with a Standard V2 NAT Gateway and not any other services.

Use [New-AzNatGateway](/powershell/module/az.network/new-aznatgateway) to create the NAT gateway resource.

```azurepowershell

## Create NAT gateway resource ##

$nat = @{

ResourceGroupName = 'test-rg'

Name = 'nat-gateway'

IdleTimeoutInMinutes = '4'

Sku = 'Standard'

Location = 'westus'

PublicIpAddress = $publicIPIPv4

Zone = 1

}

$natGateway = New-AzNatGateway @nat

```

Use [Set-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/set-azvirtualnetworksubnetconfig) to associate NAT gateway with AzureFirewallSubnet.

```azurepowershell

# Get the hub virtual network

$vnetHub = Get-AzVirtualNetwork -ResourceGroupName 'test-rg' -Name 'vnet-hub'

# Associate NAT gateway with AzureFirewallSubnet

$subnetParams = @{

VirtualNetwork = $vnetHub

Name = 'AzureFirewallSubnet'

AddressPrefix = '10.0.1.64/26'

NatGateway = $natGateway

}

Set-AzVirtualNetworkSubnetConfig @subnetParams

# Update the virtual network

$vnetHub | Set-AzVirtualNetwork

```

---

## Create spoke virtual network

The spoke virtual network contains the test virtual machine used to test the routing of the internet traffic to the NAT gateway. Use the following example to create the spoke network.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Virtual network**. Select **Virtual networks** in the search results.

1. Select **+ Create**.

1. In the **Basics** tab of **Create virtual network**, enter, or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |   |

| Name | Enter **vnet-spoke**. |

| Region | Select **West US**. |

1. Select **Next** to proceed to the **Security** tab.

1. Select **Next** to proceed to the **IP addresses** tab.

1. In the **IP Addresses** tab in **IPv4 address space**, select **Delete address space** to delete the address space that is auto populated.

1. Select **+ Add IPv4 address space**.

1. In **IPv4 address space** enter **10.1.0.0**. Leave the default of **/16 (65,536 addresses)** in the mask selection.

1. Select **+ Add a subnet**.

1. In **Add a subnet** enter or select the following information:

| Setting | Value |

| ------- | ----- |

| Subnet purpose | Leave the default **Default**. |

| Name | Enter **subnet-private**. |

| **IPv4** |   |

| IPv4 address range| Leave the default of **10.1.0.0/16**. |

| Starting address | Leave the default of **10.1.0.0**. |

| Size | Leave the default of **/24(256 addresses)**. |

1. Select **Add**.

1. Select **Review + create**.

1. Select **Create**.

# [**PowerShell**](#tab/powershell)

Use [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork) to create the spoke virtual network.

```azurepowershell

# Create spoke virtual network

$vnetParams = @{

ResourceGroupName = 'test-rg'

Location = 'westus'

Name = 'vnet-spoke'

AddressPrefix = '10.1.0.0/16'

}

$spokeVnet = New-AzVirtualNetwork @vnetParams

```

Use [Add-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/add-azvirtualnetworksubnetconfig) to create a subnet for the spoke virtual network.

```azurepowershell

# Create subnet in spoke virtual network

$subnetParams = @{

Name = 'subnet-private'

AddressPrefix = '10.1.0.0/24'

VirtualNetwork = $spokeVnet

}

Add-AzVirtualNetworkSubnetConfig @subnetParams

```

Use [Set-AzVirtualNetwork](/powershell/module/az.network/set-azvirtualnetwork) to update the spoke virtual network.

```azurepowershell

# Create the virtual network

$spokeVnet | Set-AzVirtualNetwork

```

---

## Create peering between the hub and spoke

A virtual network peering is used to connect the hub to the spoke and the spoke to the hub. Use the following example to create a two-way network peering between the hub and spoke.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Virtual network**. Select **Virtual networks** in the search results.

1. Select **vnet-hub**.

1. Select **Peerings** in **Settings**.

1. Select **+ Add**.

1. Enter or select the following information in **Add peering**:

| Setting | Value |

| ------- | -----

| **Remote virtual network summary** |   |

| Peering link name | Enter **vnet-spoke-to-vnet-hub**. |

| Virtual network deployment model | Leave the default of **Resource manager**. |

| Subscription | Select your subscription. |

| Virtual network | Select **vnet-spoke (test-rg)**. |

| **Remote virtual network peering settings** |   |

| Allow 'vnet-spoke' to access 'vnet-hub' | Leave the default of **Selected**. |

| Allow 'vnet-spoke' to receive forwarded traffic from 'vnet-hub' | Select the checkbox. |

| Allow gateway or route server in 'vnet-spoke' to forward traffic to 'vnet-hub' | Leave the default of **Unselected**. |

| Enable 'vnet-spoke' to use 'vnet-hub's' remote gateway or route server | Leave the default of **Unselected**. |

| **Local virtual network summary** |   |

| Peering link name | Enter **vnet-hub-to-vnet-spoke**. |

| **Local virtual network peering settings** |   |

| Allow 'vnet-hub' to access 'vnet-spoke' | Leave the default of **Selected**. |

| Allow 'vnet-hub' to receive forwarded traffic from 'vnet-spoke' | Select the checkbox. |

| Allow gateway or route server in 'vnet-hub' to forward traffic to 'vnet-spoke' | Leave the default of **Unselected**. |

| Enable 'vnet-hub' to use 'vnet-spoke's' remote gateway or route server | Leave the default of **Unselected**. |

1. Select **Add**.

1. Select **Refresh** and verify **Peering status** is **Connected**.

# [**PowerShell**](#tab/powershell)

Use [Add-AzVirtualNetworkPeering](/powershell/module/az.network/add-azvirtualnetworkpeering) to create a peering from the hub to the spoke.

```azurepowershell

# Create peering from hub to spoke

$peeringParams = @{

Name = 'vnet-hub-to-vnet-spoke'

VirtualNetwork = $hubVnet

RemoteVirtualNetworkId = $spokeVnet.Id

AllowForwardedTraffic = $true

}

Add-AzVirtualNetworkPeering @peeringParams

```

Use [Add-AzVirtualNetworkPeering](/powershell/module/az.network/add-azvirtualnetworkpeering) to create a peering from the spoke to the hub.

```azurepowershell

# Create peering from spoke to hub

$peeringParams = @{

Name = 'vnet-spoke-to-vnet-hub'

VirtualNetwork = $spokeVnet

RemoteVirtualNetworkId = $hubVnet.Id

AllowForwardedTraffic = $true

}

Add-AzVirtualNetworkPeering @peeringParams

```

---

## Create spoke network route table

A route table forces all traffic leaving the spoke virtual network to the hub virtual network. The route table is configured with the private IP address of the Azure Firewall as the virtual appliance.

### Obtain private IP address of firewall

The private IP address of the firewall is needed for the route table created later in this article. Use the following example to obtain the firewall private IP address.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Firewall**. Select **Firewalls** in the search results.

1. Select **firewall**.

1. In the **Overview** of **firewall**, note the IP address in the field **Firewall private IP**. The IP address in this example is **10.0.1.68**.

# [**PowerShell**](#tab/powershell)

Use [Get-AzFirewall](/powershell/module/az.network/get-azfirewall) to obtain the private IP address of the firewall.

```azurepowershell

# Get the private IP address of the firewall

$firewallParams = @{

ResourceGroupName = 'test-rg'

Name = 'firewall'

}

$firewall = Get-AzFirewall @firewallParams

$firewall.IpConfigurations[0].PrivateIpAddress

```

---

### Create route table

Create a route table to force all inter-spoke and internet egress traffic through the firewall in the hub virtual network.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Route table**. Select **Route tables** in the search results.

1. Select **+ Create**.

1. In **Create Route table** enter or select the following information:

| Setting | Value |

| ------- | ----- |

| **Project details** |   |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |   |

| Region | Select **West US**. |

| Name | Enter **route-table-spoke**. |

| Propagate gateway routes | Select **No**. |

1. Select **Review + create**.

1. Select **Create**.

1. In the search box at the top of the portal, enter **Route table**. Select **Route tables** in the search results.

1. Select **route-table-spoke**.

1. In **Settings** select **Routes**.

1. Select **+ Add** in **Routes**.

1. Enter or select the following information in **Add route**:

| Setting | Value |

| ------- | ----- |

| Route name | Enter **route-to-hub**. |

| Destination type | Select **IP Addresses**. |

| Destination IP addresses/CIDR ranges | Enter **0.0.0.0/0**. |

| Next hop type | Select **Virtual appliance**. |

| Next hop address | Enter **10.0.1.68**. |

1. Select **Add**.

1. Select **Subnets** in **Settings**.

1. Select **+ Associate**.

1. Enter or select the following information in **Associate subnet**:

| Setting | Value |

| ------- | ----- |

| Virtual network | Select **vnet-spoke (test-rg)**. |

| Subnet | Select **subnet-private**. |

1. Select **OK**.

# [**PowerShell**](#tab/powershell)

Use [New-AzRouteTable](/powershell/module/az.network/new-azroutetable) to create the route table.

```azurepowershell

# Create route table

$routeTableParams = @{

ResourceGroupName = 'test-rg'

Location = 'westus'

Name = 'route-table-spoke'

}

$routeTable = New-AzRouteTable @routeTableParams

```

Use [Add-AzRouteConfig](/powershell/module/az.network/add-azrouteconfig) to create a route in the route table.

```azurepowershell

# Create route

$routeConfigParams = @{

Name = 'route-to-hub'

AddressPrefix = '0.0.0.0/0'

NextHopType = 'VirtualAppliance'

NextHopIpAddress = $firewall.IpConfigurations[0].PrivateIpAddress

RouteTable = $routeTable

}

Add-AzRouteConfig @routeConfigParams

```

Use [Set-AzRouteTable](/powershell/module/az.network/set-azroutetable) to update the route table.

```azurepowershell

# Update the route table

$routeTable | Set-AzRouteTable

```

Use [Set-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/set-azvirtualnetworksubnetconfig) to associate the route table with the spoke subnet.

```azurepowershell

# Associate route table with subnet

$subnetConfigParams = @{

VirtualNetwork = $spokeVnet

Name = 'subnet-private'

AddressPrefix = '10.1.0.0/24'

RouteTable = $routeTable

}

Set-AzVirtualNetworkSubnetConfig @subnetConfigParams

```

Use [Set-AzVirtualNetwork](/powershell/module/az.network/set-azvirtualnetwork) to update the spoke virtual network.

```azurepowershell

# Update the virtual network

$spokeVnet | Set-AzVirtualNetwork

```

---

## Configure firewall

Traffic from the spoke through the hub must be allowed through and firewall policy and a network rule. Use the following example to create the firewall policy and network rule.

### Configure network rule

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Firewall**. Select **Firewall Policies** in the search results.

1. Select **firewall-policy**.

1. Expand **Settings** then select **Network rules**.

1. Select **+ Add a rule collection**.

1. In **Add a rule collection** enter or select the following information:

| Setting | Value |

| ------- | ----- |

| Name | Enter **spoke-to-internet**. |

| Rule collection type | Select **Network**. |

| Priority | Enter **100**. |

| Rule collection action | Select **Allow**. |

| Rule collection group | Select **DefaultNetworkRuleCollectionGroup**. |

| Rules |    |

| Name | Enter **allow-web**. |

| Source type | **IP Address**. |

| Source | Enter **10.1.0.0/24**. |

| Protocol | Select **TCP**. |

| Destination Ports | Enter **80**,**443**. |

| Destination Type | Select **IP Address**. |

| Destination | Enter * |

1. Select **Add**.

# [**PowerShell**](#tab/powershell)

Use [Get-AzFirewallPolicy](/powershell/module/az.network/get-azfirewallpolicy) to get the existing firewall policy.

```powershell

# Get the existing firewall policy

$firewallPolicyParams = @{

Name = 'firewall-policy'

ResourceGroupName = 'test-rg'

}

$firewallPolicy = Get-AzFirewallPolicy @firewallPolicyParams

```

Use [New-AzFirewallPolicyNetworkRule](/powershell/module/az.network/new-azfirewallpolicynetworkrule) to create a network rule.

```powershell

# Create a network rule for web traffic

$networkRuleParams = @{

Name = 'allow-internet'

SourceAddress = '10.1.0.0/24'

Protocol = 'TCP'

DestinationAddress = '*'

DestinationPort = '*'

}

$networkRule = New-AzFirewallPolicyNetworkRule @networkRuleParams

```

Use [New-AzFirewallPolicyFilterRuleCollection](/powershell/module/az.network/new-azfirewallpolicyfilterrulecollection) to create a rule collection for the network rule.

```powershell

# Create a rule collection for the network rule

$ruleCollectionParams = @{

Name = 'spoke-to-internet'

Priority = 100

Rule = $networkRule

ActionType = 'Allow'

}

$ruleCollection = New-AzFirewallPolicyFilterRuleCollection @ruleCollectionParams

```

Use [New-AzFirewallPolicyRuleCollectionGroup](/powershell/module/az.network/new-azfirewallpolicyrulecollectiongroup) to create a rule collection group.

```powershell

$newRuleCollectionGroupParams = @{

Name = 'DefaultNetworkRuleCollectionGroup'

Priority = 200

FirewallPolicyObject = $firewallPolicy

RuleCollection = $ruleCollection

}

New-AzFirewallPolicyRuleCollectionGroup @newRuleCollectionGroupParams

```

---

## Create test virtual machine

An Ubuntu virtual machine is used to test the outbound internet traffic through the NAT gateway. Use the following example to create an Ubuntu virtual machine.

# [**Portal**](#tab/portal)

1. In the portal, search for and select **Virtual machines**.

1. In **Virtual machines**, select **+ Create**, then **Azure virtual machine**.

1. On the **Basics** tab of **Create a virtual machine**, enter, or select the following information:

| Setting | Value |

|---|---|

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg**. |

| **Instance details** |  |

| Virtual machine name | Enter **vm-spoke**. |

| Region | Select **West US**. |

| Availability options | Select **No infrastructure redundancy required**. |

| Security type | Leave the default of **Standard**. |

| Image | Select **Ubuntu Server 24.04 LTS - x64 Gen2**. |

| VM architecture | Leave the default of **x64**. |

| Size | Select a size. |

| **Administrator account** |  |

| Authentication type | Select **SSH public key**. |

| Username | Enter **azureuser**. |

| SSH public key source | Select **Generate new key pair**. |

| Key pair name | Enter **vm-spoke-key**. |

| **Inbound port rules** |  |

| Public inbound ports | Select **None**. |

1. Select the **Networking** tab at the top of the page or select **Next:Disks**, then **Next:Networking**.

1. Enter or select the following information in the **Networking** tab:

| Setting | Value |

|---|---|

| **Network interface** |  |

| Virtual network | Select **vnet-spoke**. |

| Subnet | Select **subnet-private (10.1.0.0/24)**. |

| Public IP | Select **None**. |

| NIC network security group | Select **Advanced**. |

| Configure network security group | Select **Create new**.</br> Enter **nsg-1** for the name.</br> Leave the rest at the defaults and select **OK**. |

1. Leave the rest of the settings at the defaults and select **Review + create**.

1. Review the settings and select **Create**.

1. The **Generate new key pair** dialog box appears. Select **Download private key and create resource**.

The private key downloads to your local machine. The private key is needed in later steps for connecting to the virtual machine with Azure Bastion. The name of the private key file is the name you entered in the **Key pair name** field. In this example, the private key file is named **ssh-key**.

Wait for the virtual machine to finishing deploying before proceeding to the next steps.

>[!NOTE]

>Virtual machines in a virtual network with a bastion host don't need public IP addresses. Bastion provides the public IP, and the VMs use private IPs to communicate within the network. You can remove the public IPs from any VMs in bastion hosted virtual networks. For more information, see [Dissociate a public IP address from an Azure VM](../virtual-network/ip-services/remove-public-ip-address-vm.md).

# [**PowerShell**](#tab/powershell)

Use [New-AzNetworkSecurityGroup](/powershell/module/az.network/new-aznetworksecuritygroup) to create the network security group.

```azurepowershell

$nsgParams = @{

ResourceGroupName = "test-rg"

Name = "nsg-1"

Location = "westus"

}

New-AzNetworkSecurityGroup @nsgParams

```

Use [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface) to create the network interface.

```azurepowershell

$nicParams = @{

ResourceGroupName = "test-rg"

Name = "nic-1"

SubnetId = (Get-AzVirtualNetwork -ResourceGroupName "test-rg" -Name "vnet-spoke").Subnets[0].Id

NetworkSecurityGroupId = (Get-AzNetworkSecurityGroup -ResourceGroupName "test-rg" -Name "nsg-1").Id

Location = "westus"

}

New-AzNetworkInterface @nicParams

```

Use [Get-Credential](/powershell/module/microsoft.powershell.security/get-credential) to set a user name and password for the VM and store them in the `$cred` variable.

```azurepowershell

$cred = Get-Credential

```

> [!NOTE]

> A username is required for the VM. The password is optional and won't be used if set. SSH key configuration is recommended for Linux VMs.

Use [New-AzVMConfig](/powershell/module/az.compute/new-azvmconfig) to define a VM.

```azurepowershell

$vmConfigParams = @{

VMName = "vm-spoke"

VMSize = "Standard_DS4_v2"

}

$vmConfig = New-AzVMConfig @vmConfigParams

```

Use [Set-AzVMOperatingSystem](/powershell/module/az.compute/set-azvmoperatingsystem) and [Set-AzVMSourceImage](/powershell/module/az.compute/set-azvmsourceimage) to create the rest of the VM configuration. The following example creates an Ubuntu Server virtual machine:

```azurepowershell

$osParams = @{

VM = $vmConfig

ComputerName = "vm-spoke"

Credential = $cred

}

$vmConfig = Set-AzVMOperatingSystem @osParams -Linux -DisablePasswordAuthentication

$imageParams = @{

VM = $vmConfig

PublisherName = "Canonical"

Offer = "ubuntu-24_04-lts"

Skus = "server"

Version = "latest"

}

$vmConfig = Set-AzVMSourceImage @imageParams

```

Use [Add-AzVMNetworkInterface](/powershell/module/az.compute/add-azvmnetworkinterface) to attach the NIC that you previously created to the VM.

```azurepowershell

# Get the network interface object

$nicParams = @{

ResourceGroupName = "test-rg"

Name = "nic-1"

}

$nic = Get-AzNetworkInterface @nicParams

$vmConfigParams = @{

VM = $vmConfig

Id = $nic.Id

}

$vmConfig = Add-AzVMNetworkInterface @vmConfigParams

```

Use [New-AzVM](/powershell/module/az.compute/new-azvm) to create the VM. The command generates SSH keys for the virtual machine for sign-in. Make note of the location of the private key. The private key is needed in later steps for connecting to the virtual machine with Azure Bastion.

```azurepowershell

$vmParams = @{

VM = $vmConfig

ResourceGroupName = "test-rg"

Location = "westus"

SshKeyName = "vm-spoke-key"

}

New-AzVM @vmParams -GenerateSshKey

```

---

## Test NAT gateway

You connect to the Ubuntu virtual machines you created in the previous steps to verify that the outbound internet traffic is leaving the NAT gateway.

### Obtain NAT gateway public IP address

Obtain the NAT gateway public IP address for verification of the steps later in the article.

# [**Portal**](#tab/portal)

1. In the search box at the top of the portal, enter **Public IP**. Select **Public IP addresses** in the search results.

1. Select **public-ip-nat**.

1. Make note of value in **IP address**. The example used in this article is **203.0.113.0.25**.

# [**PowerShell**](#tab/powershell)

Use [Get-AzPublicIpAddress](/powershell/module/az.network/get-azpublicipaddress) to obtain the public IP address of the NAT gateway.

```azurepowershell

# Get the public IP address of the NAT gateway

$publicIpNatParams = @{

ResourceGroupName = 'test-rg'

Name = 'public-ip-nat'

}

$publicIpNat = Get-AzPublicIpAddress @publicIpNatParams

$publicIpNat.IpAddress

```

---

### Test NAT gateway from spoke

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **vm-spoke**.

1. In **Overview**, select **Connect** then **Connect via Bastion**.

1. Select **SSH** as the connection type. Upload your SSH private key file. Select **Connect**.

1. In the bash prompt, enter the following command:

```bash

curl ifconfig.me

```

1. Verify the IP address returned by the command matches the public IP address of the NAT gateway.

```output

azureuser@vm-1:~$ curl ifconfig.me

203.0.113.0.25

```

1. Close the Bastion connection to **vm-spoke**.

# [**Portal**](#tab/portal)

[!INCLUDE [portal-clean-up.md](~/reusable-content/ce-skilling/azure/includes/portal-clean-up.md)]

# [**PowerShell**](#tab/powershell)

Use [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) to remove the resource group.

```azurepowershell

# Remove resource group

$rgParams = @{

Name = 'test-rg'

}

Remove-AzResourceGroup @rgParams

```

---

## Next steps

Advance to the next article to learn how to integrate a NAT gateway with an Azure Load Balancer:

> [!div class="nextstepaction"]

> [Integrate NAT gateway with an internal load balancer](tutorial-nat-gateway-load-balancer-internal-portal.md)


# Quickstart Create Nat Gateway V2 Templates

# Quickstart: Create a Standard V2 Azure NAT Gateway - Deployment templates

Get started with NAT Gateway V2 by using an Azure Resource Manager template (ARM template), Bicep template, or Terraform. The templates deploy a NAT gateway, virtual network, subnet, and Ubuntu virtual machine for testing NAT gateway functionality. The NAT gateway is assigned to a subnet of the virtual network.

[!INCLUDE [About Azure Resource Manager](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-introduction.md)]

If your environment meets the prerequisites and you're familiar with using ARM templates, select the **Deploy to Azure** button. The template opens in the Azure portal.

[![Deploy to Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fquickstarts%2Fmicrosoft.network%2Fnat-gateway-1-vm%2Fazuredeploy.json)

## Prerequisites

# [ARM template](#tab/ARM)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

# [Bicep](#tab/Bicep)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

# [Terraform](#tab/Terraform)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- [Install and configure Terraform](/azure/developer/terraform/quickstart-configure)

---

## Review the template

The template used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/nat-gateway-1-vm/).

# [ARM template](#tab/ARM)

Multiple Azure resources are defined in the template:

- [**Microsoft.Network/networkSecurityGroups**](/azure/templates/microsoft.network/networksecuritygroups): Creates a network security group.

- [**Microsoft.Network/networkSecurityGroups/securityRules**](/azure/templates/microsoft.network/networksecuritygroups/securityrules): Creates a security rule.

- [**Microsoft.Network/publicIPAddresses**](/azure/templates/microsoft.network/publicipaddresses): Creates a public IP address.

- [**Microsoft.Network/publicIPPrefixes**](/azure/templates/microsoft.network/publicipprefixes): Creates a public IP prefix.

- [**Microsoft.Network/natGateways**](/azure/templates/microsoft.network/natgateways): Creates a NAT gateway resource.

- [**Microsoft.Network/virtualNetworks**](/azure/templates/microsoft.network/virtualnetworks): Creates a virtual network.

- [**Microsoft.Network/virtualNetworks/subnets**](/azure/templates/microsoft.network/virtualnetworks/subnets): Creates a virtual network subnet.

- [**Microsoft.Network/networkInterfaces**](/azure/templates/microsoft.network/networkinterfaces): Creates a network interface.

- [**Microsoft.Compute/virtualMachines**](/azure/templates/microsoft.compute/virtualmachines): Creates a virtual machine.

# [Bicep](#tab/Bicep)

Multiple Azure resources are defined in the template:

- [**Microsoft.Network/networkSecurityGroups**](/azure/templates/microsoft.network/networksecuritygroups): Creates a network security group.

- [**Microsoft.Network/networkSecurityGroups/securityRules**](/azure/templates/microsoft.network/networksecuritygroups/securityrules): Creates a security rule.

- [**Microsoft.Network/publicIPAddresses**](/azure/templates/microsoft.network/publicipaddresses): Creates a public IP address.

- [**Microsoft.Network/publicIPPrefixes**](/azure/templates/microsoft.network/publicipprefixes): Creates a public IP prefix.

- [**Microsoft.Network/natGateways**](/azure/templates/microsoft.network/natgateways): Creates a NAT gateway resource.

- [**Microsoft.Network/virtualNetworks**](/azure/templates/microsoft.network/virtualnetworks): Creates a virtual network.

- [**Microsoft.Network/virtualNetworks/subnets**](/azure/templates/microsoft.network/virtualnetworks/subnets): Creates a virtual network subnet.

- [**Microsoft.Network/networkInterfaces**](/azure/templates/microsoft.network/networkinterfaces): Creates a network interface.

- [**Microsoft.Compute/virtualMachines**](/azure/templates/microsoft.compute/virtualmachines): Creates a virtual machine.

# [Terraform](#tab/Terraform)

The sample code for this article is located in the [Azure Terraform GitHub repo](https://github.com/Azure/terraform/tree/master/quickstart/101-nat-gateway-v2-create). You can view the log file containing the [test results from current and previous versions of Terraform](https://github.com/Azure/terraform/tree/master/quickstart/101-nat-gateway-v2-create/TestRecord.md). See more [articles and sample code showing how to use Terraform to manage Azure resources](/azure/terraform).

The following Azure resources are defined in the Terraform configuration:

- [azurerm_resource_group](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group): Creates a resource group.

- [azurerm_public_ip](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/public_ip): Creates a public IP address.

- [azurerm_nat_gateway](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/nat_gateway): Creates a NAT gateway resource.

- [azurerm_nat_gateway_public_ip_association](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/nat_gateway_public_ip_association): Associates a public IP with the NAT gateway.

- [azurerm_virtual_network](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_network): Creates a virtual network.

- [azurerm_subnet](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/subnet): Creates a virtual network subnet.

- [azurerm_subnet_nat_gateway_association](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/subnet_nat_gateway_association): Associates the NAT gateway with the subnet.

- [azurerm_network_security_group](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_security_group): Creates a network security group.

- [azurerm_network_interface](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_interface): Creates a network interface.

- [azurerm_linux_virtual_machine](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/linux_virtual_machine): Creates a virtual machine.

---

## Deploy the template

# [ARM template](#tab/ARM)

1. Select **Try it** from the following code block to open Azure Cloud Shell, and then follow the instructions to sign in to Azure.

```azurepowershell-interactive

$resourceGroupName = Read-Host -Prompt "Enter the Resource Group name"

$location = Read-Host -Prompt "Enter the location (i.e. centralus)"

$adminUsername = Read-Host -Prompt "Enter the administrator username"

$adminPasswordOrKey = Read-Host -Prompt "Enter the SSH public key" -AsSecureString

$deploymentParams = @{

ResourceGroupName = $resourceGroupName

TemplateUri = "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.network/nat-gateway-1-vm/azuredeploy.json"

adminUsername = $adminUsername

adminPasswordOrKey = $adminPasswordOrKey

}

New-AzResourceGroup -Name $resourceGroupName -Location $location

New-AzResourceGroupDeployment @deploymentParams

Write-Host "Press [ENTER] to continue ..."

```

2. Select **Copy** from the previous code block to copy the PowerShell script.

3. Right-click the shell console pane and then select **Paste**.

4. Enter the values.

The template deployment creates:

- Resource group

- NAT gateway

- Virtual network and subnet

- Virtual machine (Ubuntu)

> [!NOTE]

> The template uses SSH public key authentication. When prompted, provide your SSH public key, such as the contents of **~/.ssh/id_rsa.pub**. If you need to create an SSH key pair, see [Create and use an SSH key pair for Linux VMs in Azure](/azure/virtual-machines/linux/mac-create-ssh-keys).

It takes a few minutes to deploy the template. When completed, the output is similar to:

```azurepowershell-interactive

ResourceGroupName : myResourceGroup

Location          : centralus

ProvisioningState : Succeeded

Timestamp         : 12/9/2019 1:46:56 AM

Mode              : Incremental

TemplateLink      : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.network/nat-gateway-1-vm/azuredeploy.json

Parameters        :

Name                   Type                       Value

=====================  =========================  ==========

adminUsername          String                     azureuser

adminPasswordOrKey     SecureString

Outputs           :

DeploymentDebugLogLevel :

```

# [Bicep](#tab/Bicep)

1. Save the Bicep file as **main.bicep** to your local computer.

1. Deploy the Bicep file using either Azure CLI or Azure PowerShell.

# [CLI](#tab/CLI)

```azurecli

resourceGroupName="myResourceGroup"

location="centralus"

adminUsername="azureuser"

az group create \

--name $resourceGroupName \

--location $location

az deployment group create \

--resource-group $resourceGroupName \

--template-file main.bicep \

--parameters adminUsername=$adminUsername adminPasswordOrKey='<your-ssh-public-key>'

```

# [PowerShell](#tab/PowerShell)

```azurepowershell-interactive

$resourceGroupName = "myResourceGroup"

$location = "centralus"

$adminUsername = "azureuser"

$adminPasswordOrKey = "<your-ssh-public-key>"

$deploymentParams = @{

ResourceGroupName = $resourceGroupName

TemplateFile = "main.bicep"

adminUsername = $adminUsername

adminPasswordOrKey = $adminPasswordOrKey

}

New-AzResourceGroup -Name $resourceGroupName -Location $location

New-AzResourceGroupDeployment @deploymentParams

```

---

> [!NOTE]

> Replace **\<your-ssh-public-key\>** with your SSH public key, such as the contents of **~/.ssh/id_rsa.pub**. If you need to create an SSH key pair, see [Create and use an SSH key pair for Linux VMs in Azure](/azure/virtual-machines/linux/mac-create-ssh-keys).

It takes a few minutes to deploy the template. When completed, the output is similar to:

```output

DeploymentName          : main

ResourceGroupName       : myResourceGroup

ProvisioningState       : Succeeded

Timestamp               : 12/9/2019 1:46:56 AM

Mode                    : Incremental

TemplateLink            :

Parameters              :

Name                   Type                       Value

=====================  =========================  ==========

adminUsername          String                     azureuser

adminPasswordOrKey     SecureString

Outputs                 :

DeploymentDebugLogLevel :

```

# [Terraform](#tab/Terraform)

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

### Initialize Terraform

[!INCLUDE [terraform-init.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-init.md)]

### Create a Terraform execution plan

[!INCLUDE [terraform-plan.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-plan.md)]

### Apply a Terraform execution plan

[!INCLUDE [terraform-apply-plan.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-apply-plan.md)]

---

## Validate the deployment

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Select **Resource groups** from the left pane.

1. Select the resource group that you created in the previous section. The default resource group name is **myResourceGroup**.

1. Verify that the following resources are in the resource group:

- **nat-gateway**: NAT gateway

- **vnet-1**: Virtual network

- **vm-1**: Virtual machine

- **public-ip-nat**: Public IP for NAT gateway

- **nsg-1**: Network security group

## Test NAT gateway

In this section, you test the NAT gateway. You first discover the public IP of the NAT gateway. You then connect to the test virtual machine and verify the outbound connection through the NAT gateway public IP.

1. In the search box at the top of the portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **nat-gateway**.

1. Expand **Settings**, then select **Outbound IP**.

1. Make note of the IP address deployed for the outbound IP address.

1. In the search box at the top of the portal, enter **Virtual machine**. Select **Virtual machines** in the search results.

1. Select **vm-1**.

1. On the **Overview** page, select **Connect**, then select **Connect via Bastion**.

1. In the **Authentication** pull-down, select **SSH Private Key From Local File**.

1. In **Username**, enter the username you entered during template deployment.

1. In **Local File**, select the SSH private key file that corresponds to your public key.

1. Select **Connect**.

1. In the bash prompt, enter the following command:

```bash

curl ifconfig.me

```

1. Verify the IP address returned by the command matches the public IP address of the NAT gateway you noted earlier.

```output

azureuser@vm-1:~$ curl ifconfig.me

203.0.113.25

```

## Clean up resources

When you no longer need the resources that you created with the NAT gateway, delete the resource group. This removes the NAT gateway and all the related resources.

# [ARM template](#tab/ARM)

To delete the resource group, call the `Remove-AzResourceGroup` cmdlet:

```azurepowershell-interactive

Remove-AzResourceGroup -Name myResourceGroup

```

# [Bicep](#tab/Bicep)

```azurecli-interactive

az group delete --name myResourceGroup

```

# [Terraform](#tab/Terraform)

[!INCLUDE [terraform-plan-destroy.md](~/azure-dev-docs-pr/articles/terraform/includes/terraform-plan-destroy.md)]

---

## Next steps

For more information on Azure NAT Gateway, see:

> [!div class="nextstepaction"]

> [Azure NAT Gateway overview](nat-overview.md)

>

> [Azure NAT Gateway resource](nat-gateway-resource.md)

For more information on Terraform with Azure, see:

> [!div class="nextstepaction"]

> [Terraform on Azure documentation](/azure/developer/terraform)


# Secure Nat Gateway

# Secure your Azure NAT Gateway deployment

Azure NAT Gateway is a fully managed Network Address Translation (NAT) service that enables outbound internet connectivity for resources in private subnets. NAT Gateway blocks all unsolicited inbound connections and masks private IP addresses behind static public IPs, providing a secure-by-default outbound connectivity model.

This article provides security recommendations for Azure NAT Gateway. For an overview of Azure's network security services and how they work together, see [What is Azure network security?](../networking/security/network-security.md).

[!INCLUDE [Security horizontal Zero Trust statement](~/reusable-content/ce-skilling/azure/includes/security/zero-trust-security-horizontal.md)]

## Network security

Azure NAT Gateway follows a Zero Trust network security model, blocking unsolicited inbound traffic by design. Only return traffic from active outbound connections passes through the gateway.

- **Associate NAT Gateway with private subnets**: Enable [private subnets](../virtual-network/ip-services/default-outbound-access.md) to remove default outbound access and require explicit outbound connectivity through NAT Gateway. This prevents resources from using unpredictable default outbound IP addresses. For more information, see [Design virtual networks with Azure NAT Gateway](nat-gateway-design.md).

- **Scale public IP addresses for SNAT port availability**: Assign multiple public IP addresses or a public IP prefix to your NAT Gateway to increase the available SNAT port inventory and reduce the risk of SNAT port exhaustion. Each public IP address provides 64,512 SNAT ports. For more information, see [Azure NAT Gateway resource](nat-gateway-resource.md).

- **Use predictable outbound IPs for firewall allowlisting**: Assign a public IP prefix to NAT Gateway to provide a contiguous, predictable set of outbound IP addresses. Configure destination firewall rules based on this known IP range. For more information, see [What is Azure NAT Gateway?](nat-overview.md).

- **Integrate with Azure Firewall for traffic inspection**: Deploy NAT Gateway on the Azure Firewall subnet in a hub-and-spoke topology to combine outbound SNAT scalability with centralized traffic inspection and threat protection. For firewall-specific hardening guidance, see [Secure your Azure Firewall deployment](../firewall/secure-firewall.md). For more information, see [Tutorial: Integrate NAT gateway with Azure Firewall in a hub-and-spoke network](tutorial-hub-spoke-nat-firewall.md).

- **Use Private Link to reduce internet exposure**: Connect to Azure PaaS services through [Azure Private Link](../private-link/private-link-overview.md) instead of routing through NAT Gateway. This reduces outbound internet traffic, frees SNAT ports, and eliminates public internet exposure for Azure service communication. For more information, see [Design virtual networks with Azure NAT Gateway](nat-gateway-design.md).

- **Restrict NAT Gateway subnet scope**: Associate NAT Gateway only with subnets that require outbound internet access. Subnets hosting internal-only workloads should not have a NAT Gateway association. For more information, see [Azure NAT Gateway resource](nat-gateway-resource.md).

For related network-layer security guidance, see [Secure your Virtual Network deployment](../virtual-network/secure-virtual-network.md) and [Secure your Azure Load Balancer deployment](../load-balancer/secure-load-balancer.md).

## Identity and access management

Control who can create, modify, and delete NAT Gateway resources using Azure role-based access control.

- **Assign least-privilege roles for NAT Gateway management**: Use the Network Contributor built-in role for users who need to manage NAT Gateway resources, rather than granting broader roles like Contributor. For more information, see [Azure built-in roles for Networking](../role-based-access-control/built-in-roles/networking.md#network-contributor).

- **Apply resource locks to prevent accidental deletion**: Set a Delete lock on production NAT Gateway resources to prevent accidental removal, which would immediately disrupt outbound connectivity for all associated subnets. For more information, see [Lock your Azure resources to protect your infrastructure](../azure-resource-manager/management/lock-resources.md).

## Data protection

Azure NAT Gateway operates at the network layer and does not inspect, store, or process customer data content.

- **Use NAT Gateway for outbound IP masking**: NAT Gateway replaces private source IP addresses and ports with its public IP and translated SNAT ports, hiding internal network topology from external destinations. For more information, see [Azure NAT Gateway SNAT](nat-gateway-snat.md).

- **Implement end-to-end encryption for sensitive traffic**: Because NAT Gateway operates at Layer 4, configure TLS encryption at the application layer for all sensitive outbound communication passing through the gateway. For more information, see [Azure data security and encryption best practices](../security/fundamentals/data-encryption-best-practices.md).

## Logging and monitoring

Monitor NAT Gateway health and traffic patterns to detect SNAT exhaustion, connectivity failures, and unusual outbound activity.

- **Enable flow logs for outbound traffic auditing (StandardV2)**: Configure NAT Gateway flow logs through diagnostic settings to capture source and destination IPs, translated NAT IPs, packet counts, and dropped packet data. Use flow logs for compliance auditing, forensic analysis, and anomaly detection. For more information, see [Monitor NAT gateway with flow logs](monitor-nat-gateway-flow-logs.md).

- **Configure SNAT exhaustion alerts**: Create Azure Monitor alerts when the SNAT Connection Count metric shows failed connections greater than zero. Failed SNAT connections indicate port exhaustion, which causes outbound connectivity failures. For more information, see [NAT Gateway metrics and alerts](nat-metrics.md).

- **Monitor datapath availability**: Set up alerts when Datapath Availability drops below 90% over a 15-minute window, which indicates NAT Gateway infrastructure degradation. For more information, see [NAT Gateway metrics and alerts](nat-metrics.md).

- **Alert on connection count limits**: Configure alerts when Total SNAT Connection Count approaches 1.6 million (80% of the 2-million maximum) to proactively prevent connectivity degradation. For more information, see [NAT Gateway metrics and alerts](nat-metrics.md).

- **Use Network Insights dashboards**: Deploy the pre-configured NAT Gateway Network Insights dashboard in Azure Monitor for a visual overview of metrics, traffic patterns, and health status. For more information, see [Monitor NAT gateway](monitor-nat-gateway.md).

- **Configure resource health alerts**: Set up Azure Resource Health alerts to receive notifications when NAT Gateway enters a degraded or unavailable state. For more information, see [Resource health for NAT gateway](resource-health.md).

## Compliance and governance

Enforce consistent security configurations across NAT Gateway deployments using policy and governance controls.

- **Audit availability zone configuration with Azure Policy**: Use the built-in policy definition "[Preview]: NAT gateway should be Zone Aligned" to audit or deny NAT Gateway deployments that don't have exactly one entry in their zones array. Relevant NAT Gateway resilience policies are typically Preview; review the policy version and effects before enforcing them in production. For zone-redundant outbound connectivity, deploy the StandardV2 SKU (zone-redundant by default) rather than relying only on policy. For more information, see [Azure Policy built-in definitions for Azure networking services](../networking/policy-reference.md).

- **Monitor resource health history**: Review the 30-day resource health history for NAT Gateway resources to identify patterns of degradation or availability issues that may indicate underlying infrastructure problems. For more information, see [Resource health for NAT gateway](resource-health.md).

## Backup and recovery

Azure NAT Gateway is a fully managed service with built-in resilience, but design choices affect availability during zone or region failures.

- **Deploy StandardV2 for zone redundancy**: Use the StandardV2 SKU, which is zone-redundant by default. When an availability zone failure occurs, new connections automatically flow from the remaining healthy zones with no manual intervention. For more information, see [Design virtual networks with Azure NAT Gateway](nat-gateway-design.md).

- **Plan for regional resiliency**: NAT Gateway is a regional resource and doesn't provide native multi-region capabilities or automatic failover between regions. For multi-region architectures, deploy independent NAT Gateway instances in each region and use zone-redundant or multi-region application architecture for workload resilience. For more information, see [Reliability in Azure NAT Gateway](/azure/reliability/reliability-nat-gateway).

## Next steps

- [What is Azure NAT Gateway?](nat-overview.md)

- [Design virtual networks with Azure NAT Gateway](nat-gateway-design.md)

- [Azure NAT Gateway SNAT](nat-gateway-snat.md)

- [NAT Gateway metrics and alerts](nat-metrics.md)

- [Overview of Microsoft cloud security benchmark v2](/security/benchmark/azure/overview)


# Nat Gateway Snat

# Source Network Address Translation (SNAT) with Azure NAT Gateway

Source Network Address Translation (SNAT) allows traffic from a private virtual network to connect to the internet while remaining fully private. SNAT rewrites the source IP and port of the originating packet to a public IP and port combination. Ports are used as unique identifiers to distinguish different connections from one another. The internet uses a five-tuple hash (protocol, source IP/port, destination IP/port) to provide this distinction.

SNAT also allows multiple private instances within a virtual network to use the same single public IP address or set of IP addresses (prefix) to connect to the internet.

NAT gateway enables a many-to-one SNAT capability. Many private instances in a subnet can SNAT to a public IP address attached to NAT gateway in order to connect to the internet. When NAT gateway makes multiple connections to the same destination endpoint, each new connection uses a different SNAT port so that connections can be distinguished from one another.

SNAT port exhaustion occurs when a source endpoint has run out of available SNAT ports to differentiate between new connections. When SNAT port exhaustion occurs, connections fail.

## Scale SNAT for NAT gateway

Scaling NAT gateway is primarily a function of managing the shared, available SNAT port inventory.

SNAT port inventory is provided by the public IP addresses, public IP prefixes or both attached to NAT gateway. SNAT port inventory is made available on-demand to all instances within a subnet attached to NAT gateway. As the workload of a subnet’s private instances scale, NAT gateway allocates SNAT ports as needed.

When multiple subnets within a virtual network are attached to the same NAT gateway resource, the SNAT port inventory provided by NAT gateway is shared across all subnets.

A single NAT gateway can scale up to 16 IP addresses. Each NAT gateway public IP address provides 64,512 SNAT ports to make outbound connections. NAT gateway can scale up to over 1 million SNAT ports. TCP and UDP are separate SNAT port inventories and are unrelated to NAT gateway.

## NAT gateway dynamically allocates SNAT ports

NAT gateway dynamically allocates SNAT ports across a subnet's private resources, such as virtual machines. All available SNAT ports are used on-demand by any virtual machine in subnets configured with NAT gateway.

*Figure: SNAT port allocation*

Preallocation of SNAT ports to each virtual machine is required for other SNAT methods. This preallocation of SNAT ports can cause SNAT port exhaustion on some virtual machines while others still have available SNAT ports for connecting outbound.

With NAT gateway, preallocation of SNAT ports isn't required, which means SNAT ports aren't left unused by virtual machines not actively needing them.

After a SNAT port is released, it's available for use by any virtual machine within subnets configured with NAT gateway. On-demand allocation allows dynamic and divergent workloads on subnets to use SNAT ports as needed. As long as SNAT ports are available, SNAT flows succeed.

*Figure: SNAT port exhaustion*

## NAT gateway SNAT port selection and reuse

NAT gateway selects a SNAT port at random out of the available inventory of ports to make new outbound connections. If NAT gateway doesn't find any available SNAT ports, then it reuses a SNAT port. The same SNAT port can be used to connect to multiple different destinations at the same time.

A SNAT port can be reused to connect to the same destination endpoint. Before the port is reused, NAT gateway places a SNAT port reuse timer for cool down on the port after the connection closes.

The SNAT port reuse timer helps prevent ports from being selected too quickly for connecting to the same destination. This process is helpful when destination endpoints have firewalls or other services configured that place a cool down timer on source ports. SNAT port reuse timers vary based on how a connection flow was closed. To learn more, see [Port Reuse Timers](/azure/nat-gateway/nat-gateway-resource#timers).

*Figure: SNAT port reuse*

## Example SNAT flows for NAT gateway

### Many to one SNAT with NAT gateway

NAT gateway provides a many to one configuration in which multiple private instances within a NAT gateway configured subnet can use the same public IP address to connect outbound.

In the following table, two different virtual machines (10.0.0.1 and 10.2.0.1) make connections to https://microsoft.com destination IP 23.53.254.142. When NAT gateway is configured with public IP address 65.52.1.1, each virtual machine's source IPs are translated into NAT gateway's public IP address and a SNAT port:

| Flow | Source tuple | Source tuple after SNAT | Destination tuple |

| --- | --- | --- | --- |

| 1 | 10.0.0.1:4283 | 65.52.1.1:1234 | 23.53.254.142:80 |

| 2 | 10.0.0.1:4284 | 65.52.1.1:1235 | 23.53.254.142:80 |

| 3 | 10.2.0.1:5768 | 65.52.1.1:1236 | 23.53.254.142:80 |

**IP masquerading** or **port masquerading** is the act of replacing the private IP and port with the public IP and port before connecting to the internet. Multiple private resources can be masqueraded behind the same public IP of NAT gateway.

### NAT gateway reuses a SNAT port to connect to a new destination

As mentioned previously, NAT gateway can reuse the same SNAT port to connect simultaneously to a new destination endpoint. In the following table, NAT gateway translates flow 4 to a SNAT port that is already in use for other destinations (see flow 1 from previous table).

| Flow | Source tuple | Source tuple after SNAT | Destination tuple |

| --- | --- | --- | --- |

| 4 | 10.0.0.1:4285 | 65.52.1.1:1234 | 26.108.254.155:80 |

### NAT gateway SNAT port cool down for reuse to the same destination

In a scenario where NAT gateway reuses a SNAT port to make new connections to the same destination endpoint, the SNAT port is first placed in a SNAT port reuse phase for cool down. The SNAT port reuse period helps ensure that SNAT ports aren't reused too quickly when connecting to the same destination. This SNAT port reuse for cool down on NAT gateway is beneficial in scenarios where the destination endpoint has a firewall with its own source port timer for cool down in place.

To demonstrate this SNAT port reuse cool down behavior, let's take a closer look at flow 4 from the previous table. Flow 4 was connecting to a destination endpoint fronted by a firewall with a 20-second source port cool down timer.

| Flow | Source tuple | Source tuple after SNAT | Destination tuple | Packet type connection is closed with | Destination firewall timer for cool down for source port |

| --- | --- | --- | --- | --- | --- |

| 4 | 10.0.0.1:4285 | 65.52.1.1:1234 | 26.108.254.155:80 | TCP FIN | 20 seconds |

Connection flow 4 closes with a TCP FIN packet. Since the connection is closed with a TCP FIN packet, NAT gateway places SNAT port 1234 in cool down for 65 seconds before it can be reused. Because port 1234 is in cool down for longer than the firewall source port cool down timer duration of 20 seconds, connection flow 5 proceeds with reusing SNAT port 1234 without issue.

| Flow | Source tuple | Source tuple after SNAT | Destination tuple |

| --- | --- | --- | --- |

| 5 | 10.2.0.1:5769 | 65.52.1.1:1234 | 26.108.254.155:80 |

Keep in mind that NAT gateway places SNAT ports under different SNAT port reuse cool down timers depending on how the previous connection closed. For more information about SNAT port reuse timers, see [Port Reuse Timers](/azure/nat-gateway/nat-gateway-resource#port-reuse-timers).

Don't take a dependency on the specific way source ports are assigned in the above examples. The preceding are illustrations of the fundamental concepts only.

## Related content

- [What is Azure NAT Gateway?](/azure/nat-gateway/nat-overview)

- [Design virtual network with NAT gateway](/azure/nat-gateway/nat-gateway-resource)

- [Azure NAT Gateway metrics and alerts](/azure/nat-gateway/nat-metrics)


# Manage Nat Gateway

# Manage NAT gateway

Learn how to create and remove a NAT gateway resource from a virtual network subnet. A NAT gateway enables outbound connectivity for resources in an Azure Virtual Network. You can change the public IP addresses and public IP address prefixes associated with the NAT gateway changed after deployment.

This article explains how to manage the following aspects of NAT gateway:

- Create a NAT gateway and associate it with an existing subnet.

- Remove a NAT gateway from an existing subnet and delete the NAT gateway.

- Add or remove a public IP address or public IP prefix.

> [!NOTE]

> Associating a NAT Gateway with a subnet makes it the preferred outbound connectivity method for all new connections. NAT Gateway takes precedence over other explicit outbound configurations, including load balancer outbound rules, firewalls, and instance‑level public IP addresses.

> Existing connections are not interrupted and continue to use their original outbound path until they are re‑established.

## Prerequisites

# [**Azure portal**](#tab/manage-nat-portal)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An existing Azure Virtual Network and subnet. For more information, see [Quickstart: Create a virtual network using the Azure portal](../virtual-network/quick-create-portal.md).

- The example virtual network that is used in this article is named *vnet-1*.

- The example subnet is named *subnet-1*.

- The example NAT gateway is named *nat-gateway*.

# [**Azure PowerShell**](#tab/manage-nat-powershell)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An existing Azure Virtual Network and subnet. For more information, see [Quickstart: Create a virtual network using the Azure portal](../virtual-network/quick-create-portal.md).

- The example virtual network that is used in this article is named *vnet-1*.

- The example subnet is named *subnet-1*.

- The example NAT gateway is named *nat-gateway*.

To use Azure PowerShell for this article, you need:

- Azure PowerShell installed locally or Azure Cloud Shell.

If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 5.4.1 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell).

If you run PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

- Ensure that your `Az.Network` module is 4.3.0 or later. To verify the installed module, use the command `Get-InstalledModule -Name "Az.Network"`. If the module requires an update, use the command `Update-Module -Name Az.Network`.

- Sign in to Azure PowerShell and select the subscription that you want to use. For more information, see [Sign in with Azure PowerShell](/powershell/azure/authenticate-azureps).

# [**Azure CLI**](#tab/manage-nat-cli)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An existing Azure Virtual Network and subnet. For more information, see [Quickstart: Create a virtual network using the Azure portal](../virtual-network/quick-create-portal.md).

- The example virtual network that is used in this article is named *vnet-1*.

- The example subnet is named *subnet-1*.

- The example NAT gateway is named *nat-gateway*.

To use Azure CLI for this article, you need:

- Azure CLI version 2.31.0 or later. Azure Cloud Shell uses the latest version.

[!INCLUDE [azure-cli-prepare-your-environment-no-header.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment-no-header.md)]

# [**Bicep**](#tab/manage-nat-bicep)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An existing Azure Virtual Network a subnet. For more information, see [Quickstart: Create a virtual network using the Azure portal](../virtual-network/quick-create-portal.md).

- The example virtual network that is used in this article is named *vnet-1*.

- The example subnet is named *subnet-1*.

- The example NAT gateway is named *nat-gateway*.

---

## Create a NAT gateway and associate it with an existing subnet

You can create a NAT gateway resource and add it to an existing subnet by using the Azure portal, Azure PowerShell, Azure CLI, or Bicep.

# [**Azure portal**](#tab/manage-nat-portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the Azure portal, enter *NAT gateway*. Select **NAT gateways** in the search results.

1. Select **+ Create**.

1. Enter or select the following information in the **Basics** tab of **Create network address translation (NAT) gateway**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select your resource group or select **Create new** to create a new resource group. |

| **Instance details** |  |

| NAT gateway name | Enter *nat-gateway*. |

| Region | Select your region. This example uses **East US 2**. |

| Availability zone | Select **No Zone**. For more information about NAT gateway and availability zones, see [Reliability in Azure NAT Gateway](/azure/reliability/reliability-nat-gateway). |

| TCP idle timeout (minutes) | Select the default of **4**. |

1. Select the **Outbound IP** tab, or select **Next: Outbound IP**.

1. You can select an existing public IP address or prefix or both to associate with the NAT gateway and enable outbound connectivity.

- To create a new public IP for the NAT gateway, select **Create a new public IP address**. Enter *public-ip-nat* in **Name**. Select **OK**.

- To create a new public IP prefix for the NAT gateway, select **Create a new public IP prefix**. Enter *public-ip-prefix-nat* in **Name**. Select a **Prefix size**. Select **OK**.

1. Select the **Subnet** tab, or select **Next: Subnet**.

1. Select your virtual network. In this example, select **vnet-1** in the dropdown list.

1. Select the checkbox next to **subnet-1**.

1. Select **Review + create**.

1. Select **Create**.

# [**Azure PowerShell**](#tab/manage-nat-powershell)

### Public IP address

To create a NAT gateway with a public IP address, run the following PowerShell commands.

Use the [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) cmdlet to create a public IP address for the NAT gateway.

```azurepowershell

## Create public IP address for NAT gateway ##

$ip = @{

Name = 'public-ip-nat'

ResourceGroupName = 'test-rg'

Location = 'eastus2'

Sku = 'Standard'

AllocationMethod = 'Static'

}

New-AzPublicIpAddress @ip

```

Use the [New-AzNatGateway](/powershell/module/az.network/new-aznatgateway) cmdlet to create a NAT gateway resource and associate the public IP address that you created. Use the [Set-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/set-azvirtualnetworksubnetconfig) cmdlet to configure the NAT gateway for your virtual network subnet.

```azurepowershell

## Place the virtual network into a variable. ##

$net = @{

Name = 'vnet-1'

ResourceGroupName = 'test-rg'

}

$vnet = Get-AzVirtualNetwork @net

## Place the public IP address you created previously into a variable. ##

$pip = @{

Name = 'public-ip-nat'

ResourceGroupName = 'test-rg'

}

$publicIP = Get-AzPublicIPAddress @pip

## Create NAT gateway resource ##

$nat = @{

ResourceGroupName = 'test-rg'

Name = 'nat-gateway'

IdleTimeoutInMinutes = '4'

Sku = 'Standard'

Location = 'eastus2'

PublicIpAddress = $publicIP

}

$natGateway = New-AzNatGateway @nat

## Create the subnet configuration. ##

$sub = @{

Name = 'subnet-1'

VirtualNetwork = $vnet

NatGateway = $natGateway

AddressPrefix = '10.0.0.0/24'

}

Set-AzVirtualNetworkSubnetConfig @sub

## Save the configuration to the virtual network. ##

$vnet | Set-AzVirtualNetwork

```

### Public IP prefix

To create a NAT gateway with a public IP prefix, use these commands.

Use the [New-AzPublicIpPrefix](/powershell/module/az.network/new-azpublicipprefix) cmdlet to create a public IP prefix for the NAT gateway.

```azurepowershell

## Create public IP prefix for NAT gateway ##

$ip = @{

Name = 'public-ip-prefix-nat'

ResourceGroupName = 'test-rg'

Location = 'eastus2'

Sku = 'Standard'

PrefixLength ='29'

}

New-AzPublicIpPrefix @ip

```

Use the [New-AzNatGateway](/powershell/module/az.network/new-aznatgateway) cmdlet to create a NAT gateway resource and associate the public IP prefix you created. Use the [Set-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/set-azvirtualnetworksubnetconfig) cmdlet to configure the NAT gateway for your virtual network subnet.

```azurepowershell

## Place the virtual network into a variable. ##

$net = @{

Name = 'vnet-1'

ResourceGroupName = 'test-rg'

}

$vnet = Get-AzVirtualNetwork @net

## Place the public IP prefix you created previously into a variable. ##

$pip = @{

Name = 'public-ip-prefix-nat'

ResourceGroupName = 'test-rg'

}

$publicIPprefix = Get-AzPublicIPPrefix @pip

## Create NAT gateway resource ##

$nat = @{

ResourceGroupName = 'test-rgNAT'

Name = 'nat-gateway'

IdleTimeoutInMinutes = '4'

Sku = 'Standard'

Location = 'eastus2'

PublicIpPrefix = $publicIPprefix

}

$natGateway = New-AzNatGateway @nat

## Create the subnet configuration. ##

$sub = @{

Name = 'subnet-1'

VirtualNetwork = $vnet

NatGateway = $natGateway

AddressPrefix = '10.0.0.0/24'

}

Set-AzVirtualNetworkSubnetConfig @sub

## Save the configuration to the virtual network. ##

$vnet | Set-AzVirtualNetwork

```

# [**Azure CLI**](#tab/manage-nat-cli)

### Public IP address

To create a NAT gateway with a public IP address, use the following commands.

Use [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create) to create a public IP address for the NAT gateway.

```azurecli

az network public-ip create \

--resource-group test-rg \

--location eastus2 \

--name public-ip-nat \

--sku standard

```

Use [az network nat gateway create](/cli/azure/network/nat/gateway#az-network-nat-gateway-create) to create a NAT gateway resource and associate the public IP address that you created.

```azurecli

az network nat gateway create \

--resource-group test-rg \

--name nat-gateway \

--public-ip-addresses public-ip-nat \

--idle-timeout 4

```

Use [az network vnet subnet update](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-update) to associate the NAT gateway with your virtual network subnet.

```azurecli

az network vnet subnet update \

--resource-group test-rg \

--vnet-name vnet-1 \

--name subnet-1 \

--nat-gateway nat-gateway

```

### Public IP prefix

To create a NAT gateway with a public IP prefix, use the following commands.

Use [az network public-ip prefix create](/cli/azure/network/public-ip/prefix#az-network-public-ip-prefix-create) to create a public IP prefix for the NAT gateway.

```azurecli

az network public-ip prefix create \

--length 29 \

--resource-group test-rg \

--location eastus2 \

--name public-ip-prefix-nat

```

Use [az network nat gateway create](/cli/azure/network/nat/gateway#az-network-nat-gateway-create) to create a NAT gateway resource and associate the public IP prefix that you created.

```azurecli

az network nat gateway create \

--resource-group test-rg \

--name nat-gateway \

--public-ip-prefixes public-ip-prefix-nat \

--idle-timeout 10

```

Use [az network vnet subnet update](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-update) to associate the NAT gateway with your virtual network subnet.

```azurecli

az network vnet subnet update \

--resource-group test-rg \

--vnet-name vnet-1 \

--name subnet-1 \

--nat-gateway nat-gateway

```

# [**Bicep**](#tab/manage-nat-bicep)

```bicep

@description('Name of the NAT gateway')

param natgatewayname string = 'nat-gateway'

@description('Name of the NAT gateway public IP')

param publicipname string = 'public-ip-nat'

@description('Name of resource group')

param location string = resourceGroup().location

var existingVNetName = 'vnet-1'

var existingSubnetName = 'subnet-1'

resource vnet 'Microsoft.Network/virtualNetworks@2023-05-01' existing = {

name: existingVNetName

}

output vnetid string = vnet.id

resource publicip 'Microsoft.Network/publicIPAddresses@2023-06-01' = {

name: publicipname

location: location

sku: {

name: 'Standard'

}

properties: {

publicIPAddressVersion: 'IPv4'

publicIPAllocationMethod: 'Static'

idleTimeoutInMinutes: 4

}

}

resource natgateway 'Microsoft.Network/natGateways@2023-06-01' = {

name: natgatewayname

location: location

sku: {

name: 'Standard'

}

properties: {

idleTimeoutInMinutes: 4

publicIpAddresses: [

{

id: publicip.id

}

]

}

}

output natgatewayid string = natgateway.id

resource updatedsubnet01 'Microsoft.Network/virtualNetworks/subnets@2023-06-01' = {

parent: vnet

name: existingSubnetName

properties: {

addressPrefix: vnet.properties.subnets[0].properties.addressPrefix

natGateway: {

id: natgateway.id

}

}

}

```

---

## Remove a NAT gateway from an existing subnet and delete the resource

To remove a NAT gateway from an existing subnet, complete the following steps.

# [**Azure portal**](#tab/manage-nat-portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the Azure portal, enter *NAT gateway*. Select **NAT gateways** in the search results.

1. Select **nat-gateway**.

1. Under **Settings**, select **Subnets**.

1. To remove NAT gateway from **all** subnets, select **Disassociate**.

2. To remove NAT gateway from only one of multiple subnets, unselect the checkbox next to the subnet and select **Save**.

You can now associate the NAT gateway with a different subnet or virtual network in your subscription. To delete the NAT gateway resource, complete the following steps.

1. In the search box at the top of the Azure portal, enter *NAT gateway*. Select **NAT gateways** in the search results.

1. Select **nat-gateway**.

1. Select **Delete**.

1. Select **Yes**.

# [**Azure PowerShell**](#tab/manage-nat-powershell)

Use [Set-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/set-azvirtualnetworksubnetconfig) to remove the NAT gateway association from the subnet by setting the value to $null. Use [Set-AzVirtualNetwork](/powershell/module/az.network/set-azvirtualnetwork) to update the virtual network configuration.

```azurepowershell

# Specify the resource group and NAT gateway name

$resourceGroupName = "test-rg"

# Specify the virtual network name and subnet name

$virtualNetworkName = "vnet-1"

$subnetName = "subnet-1"

# Get the virtual network

$vnet = @{

Name = $virtualNetworkName

ResourceGroupName = $resourceGroupName

}

$virtualNetwork = Get-AzVirtualNetwork @vnet

# Get the subnet

$subnet = $virtualNetwork.Subnets | Where-Object {$_.Name -eq $subnetName}

# Remove the NAT gateway association from the subnet

$subnet.NatGateway = $null

# Update the subnet configuration

$subConfig = @{

Name = $subnetName

VirtualNetwork = $virtualNetwork

AddressPrefix = $subnet.AddressPrefix

}

Set-AzVirtualNetworkSubnetConfig @subConfig

# Update the virtual network

Set-AzVirtualNetwork -VirtualNetwork $virtualNetwork

```

Use [Remove-AzNatGateway](/powershell/module/az.network/remove-aznatgateway) to delete the NAT gateway resource.

```azurepowershell

# Specify the resource group and NAT gateway name

$resourceGroupName = "test-rg"

$natGatewayName = "nat-gateway"

$nat = @{

Name = $natGatewayName

ResourceGroupName = $resourceGroupName

}

Remove-AzNatGateway @nat

```

# [**Azure CLI**](#tab/manage-nat-cli)

Use [az network vnet subnet update](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-update) to remove the NAT gateway from the subnet.

```azurecli

az network vnet subnet update \

--resource-group test-rg \

--vnet-name vnet-1 \

--name subnet-1 \

--remove natGateway

```

Use [az network nat gateway delete](/cli/azure/network/nat/gateway#az-network-nat-gateway-delete) to delete the NAT gateway resource.

```azurecli

az network nat gateway delete \

--name nat-gateway \

--resource-group test-rg

```

# [**Bicep**](#tab/manage-nat-bicep)

```bicep

@description('Name of resource group')

param location string = resourceGroup().location

var existingVNetName = 'vnet-1'

var existingSubnetName = 'subnet-1'

resource vnet 'Microsoft.Network/virtualNetworks@2023-05-01' existing = {

name: existingVNetName

}

output vnetid string = vnet.id

resource updatedsubnet01 'Microsoft.Network/virtualNetworks/subnets@2023-06-01' = {

parent: vnet

name: existingSubnetName

properties: {

addressPrefix: vnet.properties.subnets[0].properties.addressPrefix

}

}

```

---

> [!NOTE]

> When you delete a NAT gateway, the public IP address or prefix associated with it isn't deleted.

## Add or remove a public IP address

Complete the following steps to add or remove a public IP address from a NAT gateway.

# [**Azure portal**](#tab/manage-nat-portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the Azure portal, enter *Public IP address*. Select **Public IP addresses** in the search results.

1. Select **Create**.

1. Enter the following information in **Create public IP address**.

| Setting | Value |

| ------- | ----- |

| Subscription | Select your subscription. |

| Resource group | Select your resource group. The example uses **test-rg**. |

| Region | Select a region. This example uses **East US 2**. |

| Name | Enter *public-ip-nat2*. |

| IP version | Select **IPv4**. |

| SKU | Select **Standard**. |

| Availability zone | Select the default of **Zone-redundant**. |

| Tier | Select **Regional**. |

1. Select **Review + create** and then select **Create**.

1. In the search box at the top of the Azure portal, enter *NAT gateway*. Select **NAT gateways** in the search results.

1. Select **nat-gateway**.

1. Under **Settings**, select **Outbound IP**.

1. The IP addresses and prefixes associated with the NAT gateway are displayed. Next to **Public IP addresses**, select **Change**.

1. Next to **Public IP addresses**, select the dropdown for IP addresses. Select the IP address that you created to add to the NAT gateway. To remove an address, unselect it.

1. Select **OK**.

1. Select **Save**.

# [**PowerShell**](#tab/manage-nat-powershell)

### Add public IP address

To add a public IP address to the NAT gateway, add it to an array object along with the current IP addresses. The PowerShell cmdlets replace all the addresses.

In this example, the existing IP address associated with the NAT gateway is named *public-ip-nat*. Replace this value with an array that contains both public-ip-nat and a new IP address. If you have multiple IP addresses already configured, you must also add them to the array.

Use [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) to create a new IP address for the NAT gateway.

```azurepowershell

## Create public IP address for NAT gateway ##

$ip = @{

Name = 'public-ip-nat2'

ResourceGroupName = 'test-rg'

Location = 'eastus2'

Sku = 'Standard'

AllocationMethod = 'Static'

}

New-AzPublicIpAddress @ip

```

Use [Set-AzNatGateway](/powershell/module/az.network/set-aznatgateway) to add the public IP address to the NAT gateway.

```azurepowershell

## Place NAT gateway into a variable. ##

$ng = @{

Name = 'nat-gateway'

ResourceGroupName = 'test-rg'

}

$nat = Get-AzNatGateway @ng

## Place the existing public IP address associated with the NAT gateway into a variable. ##

$ip = @{

Name = 'public-ip-nat'

ResourceGroupName = 'test-rg'

}

$publicIP1 = Get-AzPublicIPaddress @ip

## Place the public IP address you created previously into a variable. ##

$ip = @{

Name = 'public-ip-nat2'

ResourceGroupName = 'test-rg'

}

$publicIP2 = Get-AzPublicIPaddress @ip

## Place the public IP address variables into an array. ##

$pipArray = $publicIP1,$publicIP2

## Add the IP address to the NAT gateway. ##

$nt = @{

NatGateway = $nat

PublicIpAddress = $pipArray

}

Set-AzNatGateway @nt

```

### Remove public IP address

To remove a public IP from a NAT gateway, create an array object that *doesn't* contain the IP address you want to remove. For example, you have a NAT gateway configured with two public IP addresses. You want to remove one of the IP addresses. The IP addresses associated with the NAT gateway are named public-ip-nat and public-ip-nat2. To remove public-ip-nat2, create an array object for the PowerShell command that contains *only* public-ip-nat. When you apply the command, the array is reapplied to the NAT gateway, and public-ip-nat is the only associated public IP address.

Use [Set-AzNatGateway](/powershell/module/az.network/set-aznatgateway) to remove a public IP address from the NAT gateway.

```azurepowershell

## Place NAT gateway into a variable. ##

$ng = @{

Name = 'nat-gateway'

ResourceGroupName = 'test-rg'

}

$nat = Get-AzNatGateway @ng

## Place the existing public IP address associated with the NAT gateway into a variable. ##

$ip = @{

Name = 'public-ip-nat'

ResourceGroupName = 'test-rg'

}

$publicIP1 = Get-AzPublicIPaddress @ip

## Place the second public IP address into a variable. ##

$ip = @{

Name = 'public-ip-nat2'

ResourceGroupName = 'test-rg'

}

$publicIP2 = Get-AzPublicIPAddress @ip

## Place ONLY the public IP you wish to keep in the array. ##

$pipArray = $publicIP1

## Add the public IP address to the NAT gateway. ##

$nt = @{

NatGateway = $nat

PublicIpAddress = $pipArray

}

Set-AzNatGateway @nt

```

# [**Azure CLI**](#tab/manage-nat-cli)

### Add public IP address

In this example, the existing public IP address associated with the NAT gateway is named *public-ip-nat*.

Use [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create) to create a new IP address for the NAT gateway.

```azurecli

az network public-ip create \

--resource-group test-rg \

--location eastus2 \

--name public-ip-nat2 \

--sku standard

```

Use [az network nat gateway update](/cli/azure/network/nat/gateway#az-network-nat-gateway-update) to add the public IP address that you created to the NAT gateway. The Azure CLI command replaces the values. It doesn't add a new value. To add the new IP address to the NAT gateway, you must also include any other IP addresses associated to the NAT gateway.

```azurecli

az network nat gateway update \

--name nat-gateway \

--resource-group test-rg \

--public-ip-addresses public-ip-nat public-ip-nat2

```

### Remove public IP address

Use [az network nat gateway update](/cli/azure/network/nat/gateway#az-network-nat-gateway-update) to remove a public IP address from the NAT gateway. The Azure CLI command replaces the values. It doesn't remove a value. To remove a public IP address, include any IP address in the command that you want to keep. Omit the value that you want to remove. For example, you have a NAT gateway configured with two public IP addresses. You want to remove one of the IP addresses. The IP addresses associated with the NAT gateway are named public-ip-nat and public-ip-nat2. To remove public-ip-nat2, omit the name of the IP address from the command. The command reapplies the IP addresses listed in the command to the NAT gateway. It removes any IP address not listed.

```azurecli

az network nat gateway update \

--name nat-gateway \

--resource-group test-rg \

--public-ip-addresses public-ip-nat

```

# [**Bicep**](#tab/manage-nat-bicep)

Use the Azure portal, Azure PowerShell, or Azure CLI to add or remove a public IP address from a NAT gateway.

---

## Add or remove a public IP prefix

Complete the following steps to add or remove a public IP prefix from a NAT gateway.

# [**Azure portal**](#tab/manage-nat-portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the Azure portal, enter *Public IP prefix*. Select **Public IP Prefixes** in the search results.

1. Select **Create**.

1. Enter the following information in the **Basics** tab of **Create a public IP prefix**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select your resource group. This example uses **test-rg**. |

| **Instance details** |   |

| Name | Enter *public-ip-prefix-nat*. |

| Region | Select your region. This example uses **East US 2**. |

| IP version | Select **IPv4**. |

| Prefix ownership | Select **Microsoft owned**. |

| Prefix size | Select a prefix size. This example uses **/28 (16 addresses)**. |

1. Select **Review + create**, then select **Create**.

1. In the search box at the top of the Azure portal, enter *NAT gateway*. Select **NAT gateways** in the search results.

1. Select **nat-gateway**.

1. Under **Settings**, select **Outbound IP**.

1. The page displays the IP addresses and prefixes associated with the NAT gateway. Next to **Public IP prefixes**, select **Change**.

1. Next to **Public IP Prefixes**, select the dropdown box. Select the IP address prefix that you created to add the prefix to the NAT gateway. To remove a prefix, unselect it.

1. Select **OK**.

1. Select **Save**.

# [**Azure PowerShell**](#tab/manage-nat-powershell)

### Add public IP prefix

To add a public IP prefix to the NAT gateway, add it to an array object along with the current IP prefixes. The PowerShell cmdlets replace all the IP prefixes.

In this example, the existing public IP prefix associated with the NAT gateway is named *public-ip-prefix-nat*. Replace this value with an array that contains both public-ip-prefix-nat and a new IP address prefix. If you have multiple IP prefixes already configured, you must also add them to the array.

Use [New-AzPublicIpPrefix](/powershell/module/az.network/new-azpublicipprefix) to create a new public IP prefix for the NAT gateway.

```azurepowershell

## Create public IP prefix for NAT gateway ##

$ip = @{

Name = 'public-ip-prefix-nat2'

ResourceGroupName = 'test-rg'

Location = 'eastus2'

Sku = 'Standard'

PrefixLength = '29'

}

New-AzPublicIpPrefix @ip

```

Use [Set-AzNatGateway](/powershell/module/az.network/set-aznatgateway) to add the public IP prefix to the NAT gateway.

```azurepowershell

## Place NAT gateway into a variable. ##

$ng = @{

Name = 'nat-gateway'

ResourceGroupName = 'test-rg'

}

$nat = Get-AzNatGateway @ng

## Place the existing public IP prefix associated with the NAT gateway into a variable. ##

$ip = @{

Name = 'public-ip-prefix-nat'

ResourceGroupName = 'test-rg'

}

$prefixIP1 = Get-AzPublicIPPrefix @ip

## Place the public IP prefix you created previously into a variable. ##

$ip = @{

Name = 'public-ip-prefix-nat2'

ResourceGroupName = 'test-rg'

}

$prefixIP2 = Get-AzPublicIPprefix @ip

## Place the public IP address variables into an array. ##

$preArray = $prefixIP1,$prefixIP2

## Add the IP address prefix to the NAT gateway. ##

$nt = @{

NatGateway = $nat

PublicIpPrefix = $preArray

}

Set-AzNatGateway @nt

```

### Remove public IP prefix

To remove a public IP prefix from a NAT gateway, create an array object that *doesn't* contain the IP address prefix that you want to remove. For example, you have a NAT gateway configured with two public IP prefixes. You want to remove one of the IP prefixes. The IP prefixes associated with the NAT gateway are named public-ip-prefix-nat and public-ip-prefix-nat2. To remove public-ip-prefix-nat2, create an array object for the PowerShell command that contains *only* public-ip-prefix-nat. When you apply the command, the array is reapplied to the NAT gateway, and public-ip-prefix-nat is the only prefix associated.

Use the [Set-AzNatGateway](/powershell/module/az.network/set-aznatgateway) cmdlet to remove a public IP prefix from the NAT gateway.

```azurepowershell

## Place NAT gateway into a variable. ##

$ng = @{

Name = 'nat-gateway'

ResourceGroupName = 'test-rg'

}

$nat = Get-AzNatGateway @ng

## Place the existing public IP prefix associated with the NAT gateway into a variable. ##

$ip = @{

Name = 'public-ip-prefix-nat'

ResourceGroupName = 'test-rg'

}

$prefixIP1 = Get-AzPublicIPPrefix @ip

## Place the secondary public IP prefix into a variable. ##

$ip = @{

Name = 'public-ip-prefix-nat2'

ResourceGroupName = 'test-rg'

}

$prefixIP2 = Get-AzPublicIPprefix @ip

## Place ONLY the prefix you wish to keep in the array. DO NOT ADD THE SECONDARY VARIABLE ##

$preArray = $prefixIP1

## Add the IP address prefix to the NAT gateway. ##

$nt = @{

NatGateway = $nat

PublicIpPrefix = $preArray

}

Set-AzNatGateway @nt

```

# [**Azure CLI**](#tab/manage-nat-cli)

### Add public IP prefix

In this example, the existing public IP prefix associated with the NAT gateway is named *public-ip-prefix-nat*.

Use [az network public-ip prefix create](/cli/azure/network/public-ip/prefix#az-network-public-ip-prefix-create) to create a public IP prefix for the NAT gateway.

```azurecli

az network public-ip prefix create \

--length 29 \

--resource-group test-rg \

--location eastus2 \

--name public-ip-prefix-nat2

```

Use [az network nat gateway update](/cli/azure/network/nat/gateway#az-network-nat-gateway-update) to add the public IP prefix that you created to the NAT gateway. The Azure CLI command replaces values. It doesn't add a value. To add the new IP address prefix to the NAT gateway, you must also include any other IP prefixes associated to the NAT gateway.

```azurecli

az network nat gateway update \

--name nat-gateway \

--resource-group test-rg \

--public-ip-prefixes public-ip-prefix-nat public-ip-prefix-nat2

```

### Remove public IP prefix

Use [az network nat gateway update](/cli/azure/network/nat/gateway#az-network-nat-gateway-update) to remove a public IP prefix from the NAT gateway. The Azure CLI command replaces the values. It doesn't remove a value. To remove a public IP prefix, include any prefix in the command that you wish to keep. Omit the one you want to remove. For example, you have a NAT gateway configured with two public IP prefixes. You want to remove one of the prefixes. The IP prefixes associated with the NAT gateway are named public-ip-prefix-nat and public-ip-prefix-nat2. To remove public-ip-prefix-nat2, omit the name of the IP prefix from the command. The command reapplies the IP prefixes listed in the command to the NAT gateway. It removes any IP address not listed.

```azurecli

az network nat gateway update \

--name nat-gateway \

--resource-group test-rg \

--public-ip-prefixes public-ip-prefix-nat

```

# [**Bicep**](#tab/manage-nat-bicep)

Use the Azure portal, Azure PowerShell, or Azure CLI to add or remove a public IP prefix from a NAT gateway.

---

## Next steps

To learn more about Azure Virtual Network NAT and its capabilities, see the following articles:

- [What is Azure NAT Gateway?](nat-overview.md)

- [Reliability in Azure NAT Gateway](/azure/reliability/reliability-nat-gateway)

- [Design virtual networks with NAT gateway](nat-gateway-resource.md)


# Manage Nat Gateway V2

# Manage a Standard V2 NAT gateway

Learn how to create and remove a NAT gateway resource from a virtual network subnet. A NAT gateway enables outbound connectivity for resources in an Azure Virtual Network. You can change the public IP addresses and public IP address prefixes associated with the NAT gateway changed after deployment.

This article explains how to manage the following aspects of NAT gateway:

- Create a NAT gateway and associate it with an existing subnet.

- Remove a NAT gateway from an existing subnet and delete the NAT gateway.

- Add or remove a public IP address or public IP prefix.

> [!NOTE]

> Associating a NAT Gateway with a subnet makes it the preferred outbound connectivity method for all new connections. NAT Gateway takes precedence over other explicit outbound configurations, including load balancer outbound rules, firewalls, and instance‑level public IP addresses.

> Existing connections are not interrupted and continue to use their original outbound path until they are re‑established.

## Prerequisites

# [**Azure portal**](#tab/manage-nat-portal)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An existing Azure Virtual Network and subnet. For more information, see [Quickstart: Create a virtual network using the Azure portal](../virtual-network/quick-create-portal.md).

- The example virtual network that is used in this article is named **vnet-1**.

- The example subnet is named **subnet-1**.

- The example NAT gateway is named **nat-gateway**.

# [**Azure PowerShell**](#tab/manage-nat-powershell)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An existing Azure Virtual Network and subnet. For more information, see [Quickstart: Create a virtual network using the Azure portal](../virtual-network/quick-create-portal.md).

- The example virtual network that is used in this article is named **vnet-1**.

- The example subnet is named **subnet-1**.

- The example NAT gateway is named **nat-gateway**.

To use Azure PowerShell for this article, you need:

- Azure PowerShell installed locally or Azure Cloud Shell.

If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 5.4.1 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azure-powershell).

If you run PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

- Ensure that your `Az.Network` module is 4.3.0 or later. To verify the installed module, use the command `Get-InstalledModule -Name "Az.Network"`. If the module requires an update, use the command `Update-Module -Name Az.Network`.

- Sign in to Azure PowerShell and select the subscription that you want to use. For more information, see [Sign in with Azure PowerShell](/powershell/azure/authenticate-azureps).

# [**Azure CLI**](#tab/manage-nat-cli)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An existing Azure Virtual Network and subnet. For more information, see [Quickstart: Create a virtual network using the Azure portal](../virtual-network/quick-create-portal.md).

- The example virtual network that is used in this article is named **vnet-1**.

- The example subnet is named **subnet-1**.

- The example NAT gateway is named **nat-gateway**.

To use Azure CLI for this article, you need:

- Azure CLI version 2.31.0 or later. Azure Cloud Shell uses the latest version.

[!INCLUDE [azure-cli-prepare-your-environment-no-header.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment-no-header.md)]

# [**Bicep**](#tab/manage-nat-bicep)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An existing Azure Virtual Network and subnet. For more information, see [Quickstart: Create a virtual network using the Azure portal](../virtual-network/quick-create-portal.md).

- The example virtual network that is used in this article is named **vnet-1**.

- The example subnet is named **subnet-1**.

- The example NAT gateway is named **nat-gateway**.

# [**Terraform**](#tab/manage-nat-terraform)

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An existing Azure Virtual Network and subnet. For more information, see [Quickstart: Create a virtual network using the Azure portal](../virtual-network/quick-create-portal.md).

- The example virtual network that is used in this article is named **vnet-1**.

- The example subnet is named **subnet-1**.

- The example NAT gateway is named **nat-gateway**.

- [Installation and configuration of Terraform](/azure/developer/terraform/quickstart-configure).

---

## Create a NAT gateway and associate it with an existing subnet

You can create a NAT gateway resource and add it to an existing subnet by using the Azure portal, Azure PowerShell, Azure CLI, Bicep, or Terraform.

# [**Azure portal**](#tab/manage-nat-portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the Azure portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create network address translation (NAT) gateway**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group. |

| **Instance details** |  |

| NAT gateway name | Enter **nat-gateway**. |

| Region | Select your region. This example uses **West US**. |

| SKU | Select **Standard V2**. |

| TCP idle timeout (minutes) | Leave the default of **4**. |

1. Select **Next**.

1. In the **Outbound IP** tab, select **+ Add public IP addresses or prefixes**.

1. In **Add public IP addresses or prefixes**, select **Public IP addresses**. You can select an existing public IP address or create a new one.

- To create a new public IP for the NAT gateway, select **Create a new public IP address**. Enter **public-ip-nat** in **Name**. Select **OK**.

- To create a new public IP prefix for the NAT gateway, select **Create a new public IP prefix**. Enter **public-ip-prefix-nat** in **Name**. Select a **Prefix size**. Select **OK**.

1. Select **Save**.

1. Select the **Networking** tab, or select **Next**.

1. Select your virtual network. In this example, select **vnet-1** in the dropdown list.

1. Leave the **Default to all subnets** unselected.

1. Select **subnet-1** from the dropdown list.

1. Select **Review + create**.

1. Select **Create**.

# [**Azure PowerShell**](#tab/manage-nat-powershell)

### Public IP address

To create a NAT gateway with a public IP address, run the following PowerShell commands.

Use the [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) cmdlet to create a public IP address for the NAT gateway.

```azurepowershell

## Create public IP address for NAT gateway ##

$ip = @{

Name = 'public-ip-nat'

ResourceGroupName = 'test-rg'

Location = 'eastus'

Sku = 'StandardV2'

AllocationMethod = 'Static'

IpAddressVersion = 'IPv4'

Zone = 1,2,3

}

New-AzPublicIpAddress @ip

```

Use the [New-AzNatGateway](/powershell/module/az.network/new-aznatgateway) cmdlet to create a NAT gateway resource and associate the public IP address that you created. Use the [Set-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/set-azvirtualnetworksubnetconfig) cmdlet to configure the NAT gateway for your virtual network subnet.

```azurepowershell

## Place the virtual network into a variable. ##

$net = @{

Name = 'vnet-1'

ResourceGroupName = 'test-rg'

}

$vnet = Get-AzVirtualNetwork @net

## Place the public IP address you created previously into a variable. ##

$pip = @{

Name = 'public-ip-nat'

ResourceGroupName = 'test-rg'

}

$publicIPIPv4 = Get-AzPublicIPAddress @pip

## Create NAT gateway resource ##

$nat = @{

ResourceGroupName = 'test-rg'

Name = 'nat-gateway'

IdleTimeoutInMinutes = '4'

Sku = 'StandardV2'

Location = 'eastus'

PublicIpAddress = $publicIPIPv4

Zone = 1,2,3

}

$natGateway = New-AzNatGateway @nat

## Create the subnet configuration. ##

$sub = @{

Name = 'subnet-1'

VirtualNetwork = $vnet

NatGateway = $natGateway

AddressPrefix = '10.0.0.0/24'

}

Set-AzVirtualNetworkSubnetConfig @sub

## Save the configuration to the virtual network. ##

$vnet | Set-AzVirtualNetwork

```

### Public IP prefix

To create a NAT gateway with a public IP prefix, use these commands.

Use the [New-AzPublicIpPrefix](/powershell/module/az.network/new-azpublicipprefix) cmdlet to create a public IP prefix for the NAT gateway.

```azurepowershell

## Create public IP prefix for NAT gateway ##

$ip = @{

Name = 'public-ip-prefix-nat'

ResourceGroupName = 'test-rg'

Location = 'eastus'

Sku = 'StandardV2'

PrefixLength = '31'

IpAddressVersion = 'IPv4'

Zone = 1,2,3

}

New-AzPublicIpPrefix @ip

```

Use the [New-AzNatGateway](/powershell/module/az.network/new-aznatgateway) cmdlet to create a NAT gateway resource and associate the public IP prefix you created. Use the [Set-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/set-azvirtualnetworksubnetconfig) cmdlet to configure the NAT gateway for your virtual network subnet.

```azurepowershell

## Place the virtual network into a variable. ##

$net = @{

Name = 'vnet-1'

ResourceGroupName = 'test-rg'

}

$vnet = Get-AzVirtualNetwork @net

## Place the public IP prefix you created previously into a variable. ##

$pip = @{

Name = 'public-ip-prefix-nat'

ResourceGroupName = 'test-rg'

}

$publicIPIPv4prefix = Get-AzPublicIPPrefix @pip

## Create NAT gateway resource ##

$nat = @{

ResourceGroupName = 'test-rg'

Name = 'nat-gateway'

IdleTimeoutInMinutes = '4'

Sku = 'StandardV2'

Location = 'eastus'

PublicIpPrefix = $publicIPIPv4prefix

Zone = 1,2,3

}

$natGateway = New-AzNatGateway @nat

## Create the subnet configuration. ##

$sub = @{

Name = 'subnet-1'

VirtualNetwork = $vnet

NatGateway = $natGateway

AddressPrefix = '10.0.0.0/24'

}

Set-AzVirtualNetworkSubnetConfig @sub

## Save the configuration to the virtual network. ##

$vnet | Set-AzVirtualNetwork

```

# [**Azure CLI**](#tab/manage-nat-cli)

### Public IP address

To create a NAT gateway with a public IP address, use the following commands.

Use [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create) to create a StandardV2 public IP address for the NAT gateway.

```azurecli

az network public-ip create \

--resource-group test-rg \

--name public-ip-nat \

--location eastus \

--sku StandardV2 \

--allocation-method Static \

--version IPv4 \

--zone 1 2 3

```

Use [az network nat gateway create](/cli/azure/network/nat/gateway#az-network-nat-gateway-create) to create a NAT gateway resource and associate the public IP address that you created.

```azurecli

az network nat gateway create \

--resource-group test-rg \

--name nat-gateway \

--location eastus \

--public-ip-addresses public-ip-nat \

--idle-timeout 4 \

--sku StandardV2 \

--zone 1 2 3

```

Use [az network vnet subnet update](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-update) to associate the NAT gateway with your virtual network subnet.

```azurecli

az network vnet subnet update \

--resource-group test-rg \

--vnet-name vnet-1 \

--name subnet-1 \

--nat-gateway nat-gateway

```

### Public IP prefix

To create a NAT gateway with a public IP prefix, use the following commands.

Use [az network public-ip prefix create](/cli/azure/network/public-ip/prefix#az-network-public-ip-prefix-create) to create a StandardV2 public IP prefix for the NAT gateway.

```azurecli

az network public-ip prefix create \

--resource-group test-rg \

--name public-ip-prefix-nat \

--location eastus \

--length 31 \

--sku StandardV2 \

--version IPv4 \

--zone 1 2 3

```

Use [az network nat gateway create](/cli/azure/network/nat/gateway#az-network-nat-gateway-create) to create a NAT gateway resource and associate the public IP prefix that you created.

```azurecli

az network nat gateway create \

--resource-group test-rg \

--name nat-gateway \

--location eastus \

--public-ip-prefixes public-ip-prefix-nat \

--idle-timeout 4 \

--sku StandardV2 \

--zone 1 2 3

```

Use [az network vnet subnet update](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-update) to associate the NAT gateway with your virtual network subnet.

```azurecli

az network vnet subnet update \

--resource-group test-rg \

--vnet-name vnet-1 \

--name subnet-1 \

--nat-gateway nat-gateway

```

# [**Bicep**](#tab/manage-nat-bicep)

```bicep

@description('Name of the NAT gateway')

param natGatewayName string = 'nat-gateway'

@description('Name of the NAT gateway public IP')

param publicIpName string = 'public-ip-nat'

@description('Name of resource group')

param location string = resourceGroup().location

var existingVNetName = 'vnet-1'

var existingSubnetName = 'subnet-1'

resource vnet 'Microsoft.Network/virtualNetworks@2024-05-01' existing = {

name: existingVNetName

}

resource publicIp 'Microsoft.Network/publicIPAddresses@2024-05-01' = {

name: publicIpName

location: location

sku: {

name: 'StandardV2'

tier: 'Regional'

}

zones: [

'1'

'2'

'3'

]

properties: {

publicIPAddressVersion: 'IPv4'

publicIPAllocationMethod: 'Static'

idleTimeoutInMinutes: 4

}

}

resource natGateway 'Microsoft.Network/natGateways@2024-05-01' = {

name: natGatewayName

location: location

sku: {

name: 'StandardV2'

}

zones: [

'1'

'2'

'3'

]

properties: {

idleTimeoutInMinutes: 4

publicIpAddresses: [

{

id: publicIp.id

}

]

}

}

resource updatedSubnet 'Microsoft.Network/virtualNetworks/subnets@2024-05-01' = {

parent: vnet

name: existingSubnetName

properties: {

addressPrefix: vnet.properties.subnets[0].properties.addressPrefix

natGateway: {

id: natGateway.id

}

}

}

```

# [**Terraform**](#tab/manage-nat-terraform)

### Public IP address

To create a NAT gateway with a public IP address, create a file named *main.tf* with the following Terraform configuration. The configuration creates a StandardV2 public IP address, a StandardV2 NAT gateway, and associates the NAT gateway with an existing subnet.

> [!NOTE]

> The `zones` argument must be omitted when `sku_name` is set to `StandardV2`. StandardV2 NAT gateways are zone-redundant by default.

```hcl

resource "azurerm_public_ip" "nat" {

name                = "public-ip-nat"

location            = "eastus2"

resource_group_name = "test-rg"

allocation_method   = "Static"

sku                 = "StandardV2"

sku_tier            = "Regional"

ip_version          = "IPv4"

zones               = ["1", "2", "3"]

}

resource "azurerm_nat_gateway" "nat" {

name                    = "nat-gateway"

location                = "eastus2"

resource_group_name     = "test-rg"

sku_name                = "StandardV2"

idle_timeout_in_minutes = 4

}

resource "azurerm_nat_gateway_public_ip_association" "nat" {

nat_gateway_id       = azurerm_nat_gateway.nat.id

public_ip_address_id = azurerm_public_ip.nat.id

}

data "azurerm_subnet" "subnet" {

name                 = "subnet-1"

virtual_network_name = "vnet-1"

resource_group_name  = "test-rg"

}

resource "azurerm_subnet_nat_gateway_association" "subnet" {

subnet_id      = data.azurerm_subnet.subnet.id

nat_gateway_id = azurerm_nat_gateway.nat.id

}

```

### Public IP prefix

To create a NAT gateway with a public IP prefix, create a file named *main.tf* with the following Terraform configuration.

```hcl

resource "azurerm_public_ip_prefix" "nat" {

name                = "public-ip-prefix-nat"

location            = "eastus2"

resource_group_name = "test-rg"

prefix_length       = 31

sku                 = "StandardV2"

ip_version          = "IPv4"

zones               = ["1", "2", "3"]

}

resource "azurerm_nat_gateway" "nat" {

name                    = "nat-gateway"

location                = "eastus2"

resource_group_name     = "test-rg"

sku_name                = "StandardV2"

idle_timeout_in_minutes = 4

}

resource "azurerm_nat_gateway_public_ip_prefix_association" "nat" {

nat_gateway_id      = azurerm_nat_gateway.nat.id

public_ip_prefix_id = azurerm_public_ip_prefix.nat.id

}

data "azurerm_subnet" "subnet" {

name                 = "subnet-1"

virtual_network_name = "vnet-1"

resource_group_name  = "test-rg"

}

resource "azurerm_subnet_nat_gateway_association" "subnet" {

subnet_id      = data.azurerm_subnet.subnet.id

nat_gateway_id = azurerm_nat_gateway.nat.id

}

```

Run the following commands to deploy the configuration:

```terraform

terraform init

terraform plan

terraform apply

```

---

## Remove a NAT gateway from an existing subnet and delete the resource

To remove a NAT gateway from an existing subnet, complete the following steps.

# [**Azure portal**](#tab/manage-nat-portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the Azure portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **nat-gateway**.

1. Select **Networking**.

1. To remove NAT gateway from **all** subnets, select **Disassociate**.

1. To remove NAT gateway from only one of multiple subnets, unselect the checkbox next to the subnet in the dropdown and select **Save**.

You can now associate the NAT gateway with a different subnet or virtual network in your subscription. To delete the NAT gateway resource, complete the following steps.

1. In the search box at the top of the Azure portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **nat-gateway**.

1. Select **Delete**.

1. Select **Yes**.

# [**Azure PowerShell**](#tab/manage-nat-powershell)

Use [Set-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/set-azvirtualnetworksubnetconfig) to remove the NAT gateway association from the subnet by setting the value to $null. Use [Set-AzVirtualNetwork](/powershell/module/az.network/set-azvirtualnetwork) to update the virtual network configuration.

```azurepowershell

# Specify the resource group and NAT gateway name

$resourceGroupName = "test-rg"

# Specify the virtual network name and subnet name

$virtualNetworkName = "vnet-1"

$subnetName = "subnet-1"

# Get the virtual network

$vnet = @{

Name = $virtualNetworkName

ResourceGroupName = $resourceGroupName

}

$virtualNetwork = Get-AzVirtualNetwork @vnet

# Get the subnet

$subnet = $virtualNetwork.Subnets | Where-Object {$_.Name -eq $subnetName}

# Remove the NAT gateway association from the subnet

$subnet.NatGateway = $null

# Update the subnet configuration

$subConfig = @{

Name = $subnetName

VirtualNetwork = $virtualNetwork

AddressPrefix = $subnet.AddressPrefix

}

Set-AzVirtualNetworkSubnetConfig @subConfig

# Update the virtual network

Set-AzVirtualNetwork -VirtualNetwork $virtualNetwork

```

Use [Remove-AzNatGateway](/powershell/module/az.network/remove-aznatgateway) to delete the NAT gateway resource.

```azurepowershell

# Specify the resource group and NAT gateway name

$resourceGroupName = "test-rg"

$natGatewayName = "nat-gateway"

$nat = @{

Name = $natGatewayName

ResourceGroupName = $resourceGroupName

}

Remove-AzNatGateway @nat

```

# [**Azure CLI**](#tab/manage-nat-cli)

Use [az network vnet subnet update](/cli/azure/network/vnet/subnet#az-network-vnet-subnet-update) to remove the NAT gateway from the subnet.

```azurecli

az network vnet subnet update \

--resource-group test-rg \

--vnet-name vnet-1 \

--name subnet-1 \

--remove natGateway

```

Use [az network nat gateway delete](/cli/azure/network/nat/gateway#az-network-nat-gateway-delete) to delete the NAT gateway resource.

```azurecli

az network nat gateway delete \

--name nat-gateway \

--resource-group test-rg

```

# [**Bicep**](#tab/manage-nat-bicep)

Deploy the subnet without the `natGateway` property to remove the NAT gateway association.

```bicep

@description('Name of resource group')

param location string = resourceGroup().location

var existingVNetName = 'vnet-1'

var existingSubnetName = 'subnet-1'

resource vnet 'Microsoft.Network/virtualNetworks@2024-05-01' existing = {

name: existingVNetName

}

resource updatedSubnet 'Microsoft.Network/virtualNetworks/subnets@2024-05-01' = {

parent: vnet

name: existingSubnetName

properties: {

addressPrefix: vnet.properties.subnets[0].properties.addressPrefix

}

}

```

# [**Terraform**](#tab/manage-nat-terraform)

To remove a NAT gateway from a subnet and delete the resource, remove the `azurerm_subnet_nat_gateway_association`, `azurerm_nat_gateway`, and any associated public IP resources from your Terraform configuration, then apply the changes.

If you only want to remove the NAT gateway association from the subnet, remove the `azurerm_subnet_nat_gateway_association` resource from your configuration:

```hcl

# Remove this resource block from your configuration to disassociate the NAT gateway from the subnet

# resource "azurerm_subnet_nat_gateway_association" "subnet" {

#   subnet_id      = data.azurerm_subnet.subnet.id

#   nat_gateway_id = azurerm_nat_gateway.nat.id

# }

```

To delete the NAT gateway and all its associations, remove the NAT gateway and all association resource blocks from your configuration. Run the following commands to apply the changes:

```terraform

terraform plan

terraform apply

```

---

> [!NOTE]

> When you delete a NAT gateway, the public IP address or prefix associated with it isn't deleted.

## Add or remove a public IP address

Complete the following steps to add or remove a public IP address from a NAT gateway.

# [**Azure portal**](#tab/manage-nat-portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the Azure portal, enter **Public IP address**. Select **Public IP addresses** in the search results.

1. Select **Create**.

1. Enter the following information in **Create public IP address**.

| Setting | Value |

| ------- | ----- |

| Subscription | Select your subscription. |

| Resource group | Select your resource group. The example uses **test-rg**. |

| Region | Select a region. This example uses **East US 2**. |

| Name | Enter **public-ip-nat2**. |

| IP version | Select **IPv4**. |

| SKU | Select **Standard V2**. |

| Availability zone | Select the default of **Zone-redundant**. |

| Tier | Select **Regional**. |

1. Select **Review + create** and then select **Create**.

1. In the search box at the top of the Azure portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **nat-gateway**.

1. Under **Settings**, select **Outbound IP**.

1. The IP addresses and prefixes associated with the NAT gateway are displayed. Select the IP address you want to remove and select **Remove**.

1. To add a public IP address, select **Edit**.

1. Select the public IP address that you created to add it to the NAT gateway.

1. Select **OK**.

1. Select **Save**.

# [**PowerShell**](#tab/manage-nat-powershell)

### Add public IP address

To add a public IP address to the NAT gateway, add it to an array object along with the current IP addresses. The PowerShell cmdlets replace all the addresses.

In this example, the existing IP address associated with the NAT gateway is named **public-ip-nat**. Replace this value with an array that contains both **public-ip-nat** and a new IP address. If you have multiple IP addresses already configured, you must also add them to the array.

Use [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) to create a new IP address for the NAT gateway.

```azurepowershell

## Create public IP address for NAT gateway ##

$ip = @{

Name = 'public-ip-nat2'

ResourceGroupName = 'test-rg'

Location = 'eastus'

Sku = 'StandardV2'

AllocationMethod = 'Static'

IpAddressVersion = 'IPv4'

Zone = 1,2,3

}

New-AzPublicIpAddress @ip

```

Use [Set-AzNatGateway](/powershell/module/az.network/set-aznatgateway) to add the public IP address to the NAT gateway.

```azurepowershell

## Place NAT gateway into a variable. ##

$ng = @{

Name = 'nat-gateway'

ResourceGroupName = 'test-rg'

}

$nat = Get-AzNatGateway @ng

## Place the existing public IP address associated with the NAT gateway into a variable. ##

$ip = @{

Name = 'public-ip-nat'

ResourceGroupName = 'test-rg'

}

$publicIPIPv4-1 = Get-AzPublicIPaddress @ip

## Place the public IP address you created previously into a variable. ##

$ip = @{

Name = 'public-ip-nat2'

ResourceGroupName = 'test-rg'

}

$publicIPIPv4-2 = Get-AzPublicIPaddress @ip

## Place the public IP address variables into an array. ##

$pipArray = $publicIIPv4-1,$publicIIPv4-2

## Add the IP address to the NAT gateway. ##

$nt = @{

NatGateway = $nat

PublicIpAddress = $pipArray

}

Set-AzNatGateway @nt

```

### Remove public IP address

To remove a public IP from a NAT gateway, create an array object that **doesn't** contain the IP address you want to remove. For example, you have a NAT gateway configured with two public IP addresses. You want to remove one of the IP addresses. The IP addresses associated with the NAT gateway are named public-ip-nat and public-ip-nat2. To remove public-ip-nat2, create an array object for the PowerShell command that contains **only** public-ip-nat. When you apply the command, the array is reapplied to the NAT gateway, and public-ip-nat is the only associated public IP address.

Use [Set-AzNatGateway](/powershell/module/az.network/set-aznatgateway) to remove a public IP address from the NAT gateway.

```azurepowershell

## Place NAT gateway into a variable. ##

$ng = @{

Name = 'nat-gateway'

ResourceGroupName = 'test-rg'

}

$nat = Get-AzNatGateway @ng

## Place the existing public IP address associated with the NAT gateway into a variable. ##

$ip = @{

Name = 'public-ip-nat'

ResourceGroupName = 'test-rg'

}

$publicIPIPv4-1 = Get-AzPublicIPaddress @ip

## Place the second public IP address into a variable. ##

$ip = @{

Name = 'public-ip-nat2'

ResourceGroupName = 'test-rg'

}

$publicIPIPv4-2 = Get-AzPublicIPAddress @ip

## Place ONLY the public IP you wish to keep in the array. ##

$pipArray = $publicIPIPv4-1

## Add the public IP address to the NAT gateway. ##

$nt = @{

NatGateway = $nat

PublicIpAddress = $pipArray

}

Set-AzNatGateway @nt

```

# [**Azure CLI**](#tab/manage-nat-cli)

### Add public IP address

In this example, the existing public IP address associated with the NAT gateway is named **public-ip-nat**.

Use [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create) to create a new IP address for the NAT gateway.

```azurecli

az network public-ip create \

--resource-group test-rg \

--name public-ip-nat2 \

--location eastus \

--sku StandardV2 \

--allocation-method Static \

--version IPv4 \

--zone 1 2 3

```

Use [az network nat gateway update](/cli/azure/network/nat/gateway#az-network-nat-gateway-update) to add the public IP address that you created to the NAT gateway. The Azure CLI command replaces the values. It doesn't add a new value. To add the new IP address to the NAT gateway, you must also include any other IP addresses associated to the NAT gateway.

```azurecli

az network nat gateway update \

--name nat-gateway \

--resource-group test-rg \

--public-ip-addresses public-ip-nat public-ip-nat2

```

### Remove public IP address

Use [az network nat gateway update](/cli/azure/network/nat/gateway#az-network-nat-gateway-update) to remove a public IP address from the NAT gateway. The Azure CLI command replaces the values. It doesn't remove a value. To remove a public IP address, include any IP address in the command that you want to keep. Omit the value that you want to remove. For example, you have a NAT gateway configured with two public IP addresses. You want to remove one of the IP addresses. The IP addresses associated with the NAT gateway are named public-ip-nat and public-ip-nat2. To remove public-ip-nat2, omit the name of the IP address from the command. The command reapplies the IP addresses listed in the command to the NAT gateway. It removes any IP address not listed.

```azurecli

az network nat gateway update \

--name nat-gateway \

--resource-group test-rg \

--public-ip-addresses public-ip-nat

```

# [**Bicep**](#tab/manage-nat-bicep)

Use the Azure portal, Azure PowerShell, or Azure CLI to add or remove a public IP address from a NAT gateway.

# [**Terraform**](#tab/manage-nat-terraform)

### Add public IP address

To add a public IP address to the NAT gateway, add a new `azurerm_public_ip` resource and a new `azurerm_nat_gateway_public_ip_association` resource to your Terraform configuration.

In this example, the existing public IP address associated with the NAT gateway is named **public-ip-nat**.

```hcl

resource "azurerm_public_ip" "nat2" {

name                = "public-ip-nat2"

location            = "eastus2"

resource_group_name = "test-rg"

allocation_method   = "Static"

sku                 = "StandardV2"

sku_tier            = "Regional"

ip_version          = "IPv4"

zones               = ["1", "2", "3"]

}

resource "azurerm_nat_gateway_public_ip_association" "nat2" {

nat_gateway_id       = azurerm_nat_gateway.nat.id

public_ip_address_id = azurerm_public_ip.nat2.id

}

```

### Remove public IP address

To remove a public IP address from the NAT gateway, remove the corresponding `azurerm_nat_gateway_public_ip_association` resource block from your configuration. You can also remove the `azurerm_public_ip` resource if it's no longer needed.

Run the following commands to apply the changes:

```terraform

terraform plan

terraform apply

```

---

## Add or remove a public IP prefix

Complete the following steps to add or remove a public IP prefix from a NAT gateway.

# [**Azure portal**](#tab/manage-nat-portal)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the search box at the top of the Azure portal, enter **Public IP prefix**. Select **Public IP Prefixes** in the search results.

1. Select **Create**.

1. Enter the following information in the **Basics** tab of **Create a public IP prefix**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select your resource group. This example uses **test-rg**. |

| **Instance details** |   |

| Name | Enter **public-ip-prefix-nat**. |

| Region | Select your region. This example uses **East US 2**. |

| Sku | Select **Standard V2**. |

| IP version | Select **IPv4**. |

| Prefix ownership | Select **Microsoft owned**. |

| Prefix size | Select a prefix size. This example uses **/28 (16 addresses)**. |

1. Select **Review + create**, then select **Create**.

1. In the search box at the top of the Azure portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **nat-gateway**.

1. Under **Settings**, select **Outbound IP**.

1. The page displays the IP addresses and prefixes associated with the NAT gateway. Select the prefix you want to remove and select **Remove**.

1. To add a public IP prefix, select **Edit**. Select the public IP prefix that you created to add it to the NAT gateway.

1. Select **OK**.

1. Select **Save**.

# [**Azure PowerShell**](#tab/manage-nat-powershell)

### Add public IP prefix

To add a public IP prefix to the NAT gateway, add it to an array object along with the current IP prefixes. The PowerShell cmdlets replace all the IP prefixes.

In this example, the existing public IP prefix associated with the NAT gateway is named **public-ip-prefix-nat**. Replace this value with an array that contains both **public-ip-prefix-nat** and a new IP address prefix. If you have multiple IP prefixes already configured, you must also add them to the array.

Use [New-AzPublicIpPrefix](/powershell/module/az.network/new-azpublicipprefix) to create a new public IP prefix for the NAT gateway.

```azurepowershell

## Create public IP prefix for NAT gateway ##

$ip = @{

Name = 'public-ip-prefix-nat2'

ResourceGroupName = 'test-rg'

Location = 'eastus2'

Sku = 'StandardV2'

PrefixLength = '29'

Zone = 1,2,3

IpAddressVersion = 'IPv4'

}

New-AzPublicIpPrefix @ip

```

Use [Set-AzNatGateway](/powershell/module/az.network/set-aznatgateway) to add the public IP prefix to the NAT gateway.

```azurepowershell

## Place NAT gateway into a variable. ##

$ng = @{

Name = 'nat-gateway'

ResourceGroupName = 'test-rg'

}

$nat = Get-AzNatGateway @ng

## Place the existing public IP prefix associated with the NAT gateway into a variable. ##

$ip = @{

Name = 'public-ip-prefix-nat'

ResourceGroupName = 'test-rg'

}

$publicIPIPv4prefix-1 = Get-AzPublicIPPrefix @ip

## Place the public IP prefix you created previously into a variable. ##

$ip = @{

Name = 'public-ip-prefix-nat2'

ResourceGroupName = 'test-rg'

}

$publicIPIPv4prefix-2 = Get-AzPublicIPprefix @ip

## Place the public IP address variables into an array. ##

$preArray = $publicIPIPv4prefix-1,$publicIPIPv4prefix-2

## Add the IP address prefix to the NAT gateway. ##

$nt = @{

NatGateway = $nat

PublicIpPrefix = $preArray

}

Set-AzNatGateway @nt

```

### Remove public IP prefix

To remove a public IP prefix from a NAT gateway, create an array object that **doesn't** contain the IP address prefix that you want to remove. For example, you have a NAT gateway configured with two public IP prefixes. You want to remove one of the IP prefixes. The IP prefixes associated with the NAT gateway are named public-ip-prefix-nat and public-ip-prefix-nat2. To remove public-ip-prefix-nat2, create an array object for the PowerShell command that contains **only** public-ip-prefix-nat. When you apply the command, the array is reapplied to the NAT gateway, and public-ip-prefix-nat is the only prefix associated.

Use the [Set-AzNatGateway](/powershell/module/az.network/set-aznatgateway) cmdlet to remove a public IP prefix from the NAT gateway.

```azurepowershell

## Place NAT gateway into a variable. ##

$ng = @{

Name = 'nat-gateway'

ResourceGroupName = 'test-rg'

}

$nat = Get-AzNatGateway @ng

## Place the existing public IP prefix associated with the NAT gateway into a variable. ##

$ip = @{

Name = 'public-ip-prefix-nat'

ResourceGroupName = 'test-rg'

}

$publicIPIPv4prefix-1 = Get-AzPublicIPPrefix @ip

## Place the secondary public IP prefix into a variable. ##

$ip = @{

Name = 'public-ip-prefix-nat2'

ResourceGroupName = 'test-rg'

}

$publicIPIPv4prefix-2 = Get-AzPublicIPrefix @ip

## Place ONLY the prefix you wish to keep in the array. DO NOT ADD THE SECONDARY VARIABLE ##

$preArray = $publicIPIPv4prefix-1

## Add the IP address prefix to the NAT gateway. ##

$nt = @{

NatGateway = $nat

PublicIpPrefix = $preArray

}

Set-AzNatGateway @nt

```

# [**Azure CLI**](#tab/manage-nat-cli)

### Add public IP prefix

In this example, the existing public IP prefix associated with the NAT gateway is named **public-ip-prefix-nat**.

Use [az network public-ip prefix create](/cli/azure/network/public-ip/prefix#az-network-public-ip-prefix-create) to create a public IP prefix for the NAT gateway.

```azurecli

az network public-ip prefix create \

--resource-group test-rg \

--name public-ip-prefix-nat2 \

--location eastus \

--length 31 \

--sku StandardV2 \

--version IPv4 \

--zone 1 2 3

```

Use [az network nat gateway update](/cli/azure/network/nat/gateway#az-network-nat-gateway-update) to add the public IP prefix that you created to the NAT gateway. The Azure CLI command replaces values. It doesn't add a value. To add the new IP address prefix to the NAT gateway, you must also include any other IP prefixes associated to the NAT gateway.

```azurecli

az network nat gateway update \

--name nat-gateway \

--resource-group test-rg \

--public-ip-prefixes public-ip-prefix-nat public-ip-prefix-nat2

```

### Remove public IP prefix

Use [az network nat gateway update](/cli/azure/network/nat/gateway#az-network-nat-gateway-update) to remove a public IP prefix from the NAT gateway. The Azure CLI command replaces the values. It doesn't remove a value. To remove a public IP prefix, include any prefix in the command that you wish to keep. Omit the one you want to remove. For example, you have a NAT gateway configured with two public IP prefixes. You want to remove one of the prefixes. The IP prefixes associated with the NAT gateway are named public-ip-prefix-nat and public-ip-prefix-nat2. To remove public-ip-prefix-nat2, omit the name of the IP prefix from the command. The command reapplies the IP prefixes listed in the command to the NAT gateway. It removes any IP address not listed.

```azurecli

az network nat gateway update \

--name nat-gateway \

--resource-group test-rg \

--public-ip-prefixes public-ip-prefix-nat

```

# [**Bicep**](#tab/manage-nat-bicep)

Use the Azure portal, Azure PowerShell, or Azure CLI to add or remove a public IP prefix from a NAT gateway.

# [**Terraform**](#tab/manage-nat-terraform)

### Add public IP prefix

To add a public IP prefix to the NAT gateway, add a new `azurerm_public_ip_prefix` resource and a new `azurerm_nat_gateway_public_ip_prefix_association` resource to your Terraform configuration.

In this example, the existing public IP prefix associated with the NAT gateway is named **public-ip-prefix-nat**.

```hcl

resource "azurerm_public_ip_prefix" "nat2" {

name                = "public-ip-prefix-nat2"

location            = "eastus2"

resource_group_name = "test-rg"

prefix_length       = 31

sku                 = "StandardV2"

ip_version          = "IPv4"

zones               = ["1", "2", "3"]

}

resource "azurerm_nat_gateway_public_ip_prefix_association" "nat2" {

nat_gateway_id      = azurerm_nat_gateway.nat.id

public_ip_prefix_id = azurerm_public_ip_prefix.nat2.id

}

```

### Remove public IP prefix

To remove a public IP prefix from the NAT gateway, remove the corresponding `azurerm_nat_gateway_public_ip_prefix_association` resource block from your configuration. You can also remove the `azurerm_public_ip_prefix` resource if it's no longer needed.

Run the following commands to apply the changes:

```terraform

terraform plan

terraform apply

```

---

## Next steps

To learn more about Azure NAT Gateway and its capabilities, see the following articles:

- [What is Azure NAT Gateway?](nat-overview.md)

- [Reliability in Azure NAT Gateway](/azure/reliability/reliability-nat-gateway)

- [Design virtual networks with NAT gateway](nat-gateway-resource.md)


# Region Move Nat Gateway

# Create and configure NAT gateway after moving resources to another region

In this article, you'll learn how to set up a NAT gateway after moving resources to a different region. You might want to move resources to a new Azure region that better suits your customers' location or meets your organization's needs and policies.

> [!NOTE]

> NAT gateway instances can't directly be moved from one region to another. A workaround is to use Azure Resource Mover to move all the resources associated with the existing NAT gateway to the new region. You then create a new instance of NAT gateway in the new region and then associate the moved resources with the new instance. After the new NAT gateway is functional in the new region, you delete the old instance in the previous region.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- **Owner** access in the subscription in which resources you want to move are located.

- Resources from previous region moved to new region. For more information on moving resources to another region, see [Move resources to another region with Azure Resource Mover](../resource-mover/move-region-within-resource-group.md). Follow the steps in that article to move the resources in your previous region that are associated with the NAT gateway. After successful move of the resources, continue with the steps in this article.

## Create a new NAT gateway

After you move all the resources associated with the original NAT gateway instance to the new region and verify them, you can create a new NAT gateway instance. Then, you can associate the moved resources with the new NAT gateway.

1. In the search box at the top of the Azure portal, enter **NAT gateway**. Select **NAT gateways** in the search results.

1. Select **Create**.

1. Enter or select the following information in the **Basics** tab of **Create network address translation (NAT) gateway**.

| Setting | Value |

| ------- | ----- |

| **Project details** |  |

| Subscription | Select your subscription. |

| Resource group | Select **test-rg** or your resource group or the existing resource group with the moved resources. |

| **Instance details** |  |

| NAT gateway name | Enter **nat-gateway**. |

| Region | Select your region. This example uses **East US 2**. |

| SKU | Select **Standard V2**. |

| TCP idle timeout (minutes) | Leave the default of **4**. |

1. Select **Next**.

1. In the **Outbound IP** tab, select **+ Add public IP addresses or prefixes**.

1. In **Add public IP addresses or prefixes**, select **Public IP addresses**. Select an existing public IP address in your subscription or create a new public IP. In this example, it's **public-ip**.

1. Select **Next**.

1. In the **Networking** tab, in **Virtual network**, select your virtual network. In this example, it's **vnet-1**.

1. Leave the checkbox for **Default to all subnets** unchecked.

1. In **Select specific subnets**, select your subnet. In this example, it's **subnet-1**.

1. Select **Review + create**, then select **Create**.

## Test NAT gateway in new region

For steps on how to test the NAT gateway, see [Quickstart: Create a NAT gateway - Azure portal](quickstart-create-nat-gateway-portal.md#test-nat-gateway).

## Delete old instance of NAT gateway

After you create the new NAT gateway and test the deployment, you can delete the source resources from the old region including the old NAT gateway instance.

## Next steps

For more information on moving resources in Azure, see:

- [Move NSGs to another region](../virtual-network/move-across-regions-nsg-portal.md).

- [Move public IP addresses to another region](../virtual-network/move-across-regions-publicip-portal.md).

- [Move a storage account to another region](../storage/common/storage-account-move.md?tabs=azure-portal)


# Nat Gateway Flow Logs

# Manage StandardV2 NAT Gateway Flow Logs

NAT Gateway Flow Logs provide IP information on the traffic flowing through your StandardV2 NAT gateway. Logs are captured through Azure Monitor resource log category `NatGatewayFlowLogsV1`, which you enable through Diagnostic Settings on your StandardV2 NAT gateway resource.

## Why use flow logs?

Flow logs provide visibility to the traffic flowing through your NAT gateway, which is critical to:

- **Monitor outbound traffic:** Detect unexpected outbound connections or potential security risks.

- **Ensure traceability:** Maintain a record of traffic flows for auditing and forensic analysis.

- **Analyze traffic patterns:** Understand bandwidth consumption and identify top talkers (for example, which virtual machines initiate the most outbound connections).

- **Troubleshoot connectivity issues:** Pinpoint failures or misconfigurations in outbound traffic paths.

- **Verify compliance:** Confirm that outbound traffic aligns with organizational policies and regulatory requirements.

## About the logs

Logs are captured in a 1-minute time window and can take up to 3 minutes for the data to become available in Azure Monitor.

The following table describes the fields and their definitions for *NatGatewayFlowlogsV1* log category.

| **Field** | **Type** | **Description** |

|----|----|----|

| TimeGenerated | Time in \[UTC\] | Time the data was generated from the data source. |

| SourceIp | string | Source IP address of originating traffic (Azure virtual machine's private IP). |

| DestinationIp | string | Destination IP address of originating traffic (Internet IP address). |

| NatGatewayIp | string | NAT Gateway IP address. |

| packetsSent | int / null | Count of packets sent from source IP and allowed by the NAT Gateway. |

| PacketsReceived | int / null | Count of packets received from destination IP and allowed by the NAT Gateway.  |

| PacketsSentDropped | int / null | Count of packets sent from source IP and dropped by the NAT Gateway. |

| PacketsReceivedDropped | int / null | Count of packets received from destination IP and dropped by the NAT Gateway. |

| BytesSent | int / null | Count of bytes sent from source IP and allowed by the NAT Gateway. |

| BytesReceived | int / null | Count of bytes received from destination IP and allowed by the NAT Gateway.  |

| \_resourceId | string | Resource ID of the NAT Gateway connected to the traffic |

## FAQs

**How is the pricing calculated?**

When your NAT gateway resource has *NatGatewayFlowlogsV1* log category enabled, it incurs a \$4 monthly fee. The charge is prorated hourly based on how long the Diagnostic setting remains active. For example, if the setting is enabled for 71.5 hours, you will be billed for 72 hours and total cost for that month would be \[72 ÷ 730 (total number of hours in a month) × \$4\] = \$0.40.

**What do dropped packets mean?**

The packetsSentDropped and packetsReceivedDropped fields indicate packets that were dropped after a NAT gateway connection was successfully established. These dropped fields don't include failures to establish a connection, such as failures caused by SNAT port exhaustion.

**Does Standard NAT Gateway have Flow Logs?**

Flow Logs are only available for [StandardV2 NAT Gateway](/azure/nat-gateway/nat-overview).

## Next step

To learn how to set up flow logs, see [enabling and analyzing StandardV2 NAT Gateway flow logs](/azure/nat-gateway/monitor-nat-gateway-flow-logs).


# Monitor Nat Gateway Flow Logs

# Monitor with StandardV2 NAT Gateway Flow Logs

In this article, you learn how to set up, monitor, and troubleshoot with Azure StandardV2 NAT Gateway flow logs. These logs can help you monitor and analyze the traffic flows going through your NAT gateway resource. The health event logs are provided through the Azure Monitor resource log category NatGatwayFlowlogsV1, which is enabled through Diagnostic Settings.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An Azure StandardV2 NAT Gateway resource. To learn how to create a StandardV2 NAT Gateway resource, see [Quickstart: Create a StandardV2 NAT Gateway](./quickstart-create-nat-gateway-v2.md).

- An Azure Monitor Log Analytics workspace. To learn how to create a Log Analytics workspace, see [Quickstart: Create a Log Analytics workspace](/azure/azure-monitor/logs/quick-create-workspace).

> [!NOTE]

> If you're sending logs to Azure Storage or Event Hubs, ensure the region of your storage account and Event Hubs namespace are in the same region as your StandardV2 NAT gateway resource.

1. In the Azure portal, navigate to your StandardV2 NAT gateway resource.

1. From your NAT gateway resource's **Overview** page, choose **Monitoring** > **Diagnostic settings**.

1. Select **+ Add diagnostic setting**.

1. In the **Diagnostic setting** window, select or enter the following settings:

| **Setting** | **Value** |

| --- | --- |

| **Diagnostic setting name** | Enter a name for the diagnostic setting. |

| **Logs** | |

| **Category Groups** | Select **NatGatewayFlowlogsV1**. |

| **Metrics** | Leave unchecked. |

| **Destination details** | Select **Send to Log Analytics workspace**.</br>Select your subscription and your Log Analytics workspace. |

1. Select Save and close the Diagnostic setting window.

> [!NOTE]

> Once your diagnostic setting is configured, it can take up to 90 minutes for logs to appear.

## Configure a log query

In this section, you learn how to query StandardV2 NAT Gateway flow logs to identify virtual machines generating the most outbound traffic sent – commonly referred to as top talkers. This insight is useful for diagnosing unexpected spikes in traffic and understanding bandwidth consumption patterns. The sample query provided sorts the virtual machines by the total number of packets sent in descending order. The query allows you to quickly pinpoint which virtual machines are sending the most outbound traffic from your NAT gateway.

1. In the Azure portal, navigate to your Log Analytics workspace resource associated to your StandardV2 NAT gateway resource.

1. From your Log Analytics workspace's **Overview** page, choose **Logs**.

1. Enter the following code in the query editor:

1. The following code is displayed in the query editor:

```kusto

NatGatewayFlowlogsV1

| where TimeGenerated > ago(1d)

| summarize TotalPacketsSent = sum(PacketsSent) by SourceIP

| sort by TotalPacketsSent desc

```

1. Select **Run** to execute the query.

1. If you want to modify and save the query, make your query changes and select **Save**>**Save as query**.

1. In the **Save a query** window, enter a name for the query, other optional information, and select **Save**.

## Next step

For more information about StandardV2 NAT Gateway flow logs, see [StandardV2 NAT Gateway Flow Logs](./nat-gateway-flow-logs.md).


# Nat Gateway Support Help

# Support and troubleshooting for Azure NAT Gateway

Here are suggestions for where you can get help when developing your Azure NAT Gateway solutions.

## Self help troubleshooting

Various articles explain how to determine, diagnose, and fix issues that you might encounter when using Azure NAT Gateway. Use these articles to troubleshoot connectivity failures, SNAT port exhaustion, configuration issues, and more.

For a full list of self help troubleshooting content, see [Azure NAT Gateway troubleshooting documentation](/troubleshoot/azure/nat-gateway/welcome-azure-nat-gateway).

## Post a question on Microsoft Q&A

For quick and reliable answers on your technical product questions from Microsoft Engineers, Azure Most Valuable Professionals (MVPs), or our expert community, engage with us on [Microsoft Q&A](/answers/products/azure), Azure's preferred destination for community support.

If you can't find an answer to your problem using search, submit a new question to Microsoft Q&A. Use the following tag when asking your question:

| Area | Tag |

| --- | --- |

| [Azure NAT Gateway](./nat-overview.md) | [azure-nat-gateway](/answers/tags/429/azure-nat-gateway) |

## Create an Azure support request

Explore the range of [Azure support options and choose the plan](https://azure.microsoft.com/support/plans) that best fits, whether you're a developer just starting your cloud journey or a large organization deploying business-critical, strategic applications. Azure customers can create and manage support requests in the Azure portal.

- If you already have an Azure Support Plan, [open a support request here](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest).

- To sign up for a new Azure Support Plan, [compare support plans](https://azure.microsoft.com/support/plans/) and select the plan that works for you.

## Create a GitHub issue

If you need help with the language and tools used to develop and manage Azure NAT Gateway, open an issue in its repository on GitHub.

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

News and information about Azure NAT Gateway is shared at the [Azure Networking blog](https://techcommunity.microsoft.com/category/azure/blog/azurenetworkingblog).

## Next steps

Learn more about [Azure NAT Gateway](./nat-overview.md)


# Monitor Nat Gateway Reference

# Azure NAT Gateway monitoring data reference

[!INCLUDE [horz-monitor-ref-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-intro.md)]

See [Monitor Azure NAT Gateway](monitor-nat-gateway.md) for details on the data you can collect for Azure NAT Gateway and how to use it.

[!INCLUDE [horz-monitor-ref-metrics-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-intro.md)]

NAT gateway metrics can be found in the following locations in the Azure portal.

- **Metrics** page under **Monitoring** from a NAT gateway's resource page.

- **Insights** page under **Monitoring** from a NAT gateway's resource page.

- Azure Monitor page under **Metrics**.

### Supported metrics for Microsoft.Network/natgateways

The following table lists the metrics available for the Microsoft.Network/natgateways resource type.

[!INCLUDE [horz-monitor-ref-metrics-tableheader](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-tableheader.md)]

[!INCLUDE [Microsoft.Network/natgateways](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/metrics/microsoft-network-natgateways-metrics-include.md)]

> [!NOTE]

> Count aggregation is not recommended for any of the NAT gateway metrics. Count aggregation adds up the number of metric values and not the metric values themselves. Use Total aggregation instead to get the best representation of data values for connection count, bytes, and packets metrics.

>

> Use Average for best represented health data for the datapath availability metric.

>

> For information about aggregation types, see [aggregation types](/azure/azure-monitor/essentials/metrics-aggregation-explained#aggregation-types).

For more information, see [How to use NAT gateway metrics](nat-metrics.md#how-to-use-nat-gateway-metrics).

[!INCLUDE [horz-monitor-ref-metrics-dimensions-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-dimensions-intro.md)]

[!INCLUDE [horz-monitor-ref-metrics-dimensions](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-dimensions.md)]

- ConnectionState: Attempted, Failed

- Direction: In, Out

- Protocol: 6 TCP, 17 UDP

[!INCLUDE [horz-monitor-ref-activity-log](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-activity-log.md)]

- [Microsoft.Network resource provider operations](/azure/role-based-access-control/resource-provider-operations#microsoftnetwork)

## Related content

- See [Monitor Azure NAT Gateway](monitor-nat-gateway.md) for a description of monitoring Azure NAT Gateway.

- See [Monitor Azure resources with Azure Monitor](/azure/azure-monitor/essentials/monitor-azure-resource) for details on monitoring Azure resources.


# Monitor Nat Gateway

# Monitor Azure NAT Gateway

[!INCLUDE [azmon-horz-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-intro.md)]

## Collect data with Azure Monitor

This table describes how you can collect data to monitor your service, and what you can do with the data once collected:

|Data to collect|Description|How to collect and route the data|Where to view the data|Supported data|

|---------|---------|---------|---------|---------|

|Metric data|Metrics are numerical values that describe an aspect of a system at a particular point in time. Metrics can be aggregated using algorithms, compared to other metrics, and analyzed for trends over time.| You can export metric data using the [Azure Monitor REST API](/azure/azure-monitor/essentials/rest-api-walkthrough). Metrics can be obtained by [data collection rules](/azure/azure-monitor/data-collection/data-collection-rule-overview). This feature is currently in preview.|[Metrics explorer](/azure/azure-monitor/essentials/metrics-getting-started)| [Azure NAT Gateway metrics supported by Azure Monitor](/azure/nat-gateway/monitor-nat-gateway-reference#metrics)|

|Activity log data|The Azure Monitor activity log provides insight into subscription-level events. The activity log includes information like when a resource is modified or a virtual machine is started.| You can export activity log data using the [Azure Monitor REST API](/azure/azure-monitor/essentials/rest-api-walkthrough). Activity logs can be obtained by [data collection rules](/azure/azure-monitor/data-collection/data-collection-rule-overview). This feature is currently in preview.|[Activity log](/azure/azure-monitor/essentials/activity-log)|  |

[!INCLUDE [azmon-horz-supported-data](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-supported-data.md)]

## Built in monitoring for Azure NAT Gateway

[Azure Monitor Network Insights](../network-watcher/network-insights-overview.md) allows you to visualize your Azure infrastructure setup and to review all metrics for your NAT gateway resource from a preconfigured metrics dashboard. These visual tools help you diagnose and troubleshoot any issues with your NAT gateway resource.

For more information on NAT Gateway Insights, see [Network Insights](nat-metrics.md#network-insights).

[!INCLUDE [azmon-horz-tools](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-tools.md)]

[!INCLUDE [azmon-horz-export-data](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-export-data.md)]

[!INCLUDE [azmon-horz-kusto](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-kusto.md)]

[!INCLUDE [azmon-horz-alerts-part-one](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-alerts-part-one.md)]

[!INCLUDE [azmon-horz-alerts-part-two](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-alerts-part-two.md)]

[!INCLUDE [azmon-horz-advisor](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/azmon-horz-advisor.md)]

## Related content

- See [Azure NAT Gateway monitoring data reference](monitor-nat-gateway-reference.md) for a reference of the metrics, logs, and other important values created for Azure NAT Gateway.

- See [Monitoring Azure resources with Azure Monitor](/azure/azure-monitor/essentials/monitor-azure-resource) for general details on monitoring Azure resources.


# Resource Health

# Azure NAT Gateway Resource Health

This article provides guidance on how to use Azure Resource Health to monitor and troubleshoot connectivity issues with your NAT gateway resource. Resource health provides an automatic check to keep you informed on the current availability of your NAT gateway.

## Resource health status

[Azure Resource Health](/azure/service-health/overview) provides information about the health of your NAT gateway resource. You can use resource health and Azure monitor notifications to keep you informed on the availability and health status of your NAT gateway resource. Resource health can help you quickly assess whether an issue is due to a problem in your Azure infrastructure or because of an Azure platform event. The resource health of your NAT gateway is evaluated by measuring the data-path availability of your NAT gateway endpoint.

You can view the status of your NAT gateway’s health status on the **Resource Health** page, found under **Support + troubleshooting** for your NAT gateway resource.

The health of your NAT gateway resource is displayed as one of the following statuses:

| Resource health status | Description |

|---|---|

| Available | Your NAT gateway resource is healthy and available. |

| Degraded | Your NAT gateway resource has platform or user initiated events affect the health of your NAT gateway. The metric for the data-path availability reports less than 80% but greater than 25% health for the last 15 minutes. You experience moderate to severe performance effect. |

| Unavailable | Your NAT gateway resource isn't healthy. The metric for the data-path availability reports less than 25% for the past 15 minutes. You experience significant performance effect or unavailability of your NAT gateway resource for outbound connectivity. There might be user or platform events causing unavailability. |

| Unknown | Health status for your NAT gateway resource isn't updated or received information for data-path availability for more than 5 minutes. This state should be transient and reflects the correct status as soon as data is received. |

For more information about Azure Resource Health, see [Resource Health overview](/azure/service-health/resource-health-overview).

To view the health of your NAT gateway resource:

1. From the NAT gateway resource page, under **Support + troubleshooting**, select **Resource health**.

1. In the health history section, select the drop-down arrows next to dates to get more information on health history events of your NAT gateway resource. You can view up to 30 days of history in the health history section.

1. Select the **+ Add resource health alert** at the top of the page to set up an alert for a specific health status of your NAT gateway resource.

## Resource health alerts

Azure Resource Health alerts can notify you in near real-time when the health state of your NAT gateway resource changes. Set resource health alerts to notify you when your NAT gateway resource changes to a **Degraded** or **Unavailable** health state.

After you create Azure resource health alerts for NAT gateway, Azure sends resource health notifications to your Azure subscription when the health state of NAT gateway changes. You can create and customize alerts based on:

* The subscription affected

* The resource group affected

* The resource type affected (Microsoft.Network/NATGateways)

* The specific resource (any NAT gateway resource you choose to set up an alert for)

* The event status of the NAT gateway resource affected

* The current status of the NAT gateway resource affected

* The previous status of the NAT gateway resource affected

* The reason type of the NAT gateway resource affected

You can also configure who the alert should be sent to:

* A new action group (that can be used for future alerts)

* An existing action group

For more information on how to set up these resource health alerts, see:

* [Resource health alerts using Azure portal](/azure/service-health/resource-health-alert-monitor-guide#create-a-resource-health-alert-rule-in-the-azure-portal)

* [Resource health alerts using Resource Manager templates](/azure/service-health/resource-health-alert-arm-template-guide)

## Next steps

- Learn about [Azure NAT Gateway](./nat-overview.md)

- Learn about [metrics and alerts for NAT gateway](./nat-metrics.md)

- Learn about [troubleshooting NAT gateway resources](./troubleshoot-nat.md)

- Learn about [Azure resource health](/azure/service-health/resource-health-overview)
