# Event Hubs About

# What is Azure Event Hubs?

Azure Event Hubs is a fully managed, real-time data streaming platform that can ingest millions of events per second with low latency. As a native Azure service with built-in Apache Kafka compatibility, Event Hubs enables you to run existing Kafka workloads without code changes or cluster management overhead.

Organizations use Event Hubs to build data pipelines for IoT telemetry, application logging, clickstream analytics, financial transaction processing, and other scenarios that require high-throughput, reliable event ingestion. Event Hubs integrates with Azure analytics services to enable real-time insights and long-term data retention.

## At a glance

| Attribute | Details |

|-----------|----------|

| **Service type** | Fully managed event streaming platform (PaaS) |

| **Protocols supported** | Apache Kafka, AMQP 1.0, HTTPS |

| **Data retention** | Up to 7 days (Standard), 90 days (Premium/Dedicated) |

| **Pricing tiers** | [Standard, Premium, Dedicated](event-hubs-quotas.md) |

| **SLA** | [Up to 99.99%](https://azure.microsoft.com/support/legal/sla/event-hubs/) |

## Why choose Azure Event Hubs?

- **Zero infrastructure management**: Fully managed service with automatic patching, scaling, and monitoring. No clusters to provision or maintain.

- **Enterprise-grade reliability**: Up to 99.99% SLA with availability zone support and [geo-replication](use-geo-replication.md) for business continuity.

- **Kafka without the complexity**: Run Kafka workloads with better cost efficiency and no operational overhead. No separate Kafka clusters required.

- **Seamless Azure integration**: Native integration with [Stream Analytics](../stream-analytics/stream-analytics-introduction.md), [Azure Functions](../azure-functions/functions-overview.md), [Data Explorer](/azure/data-explorer/data-explorer-overview), and many other Azure services.

- **Flexible pricing**: Choose from consumption-based or dedicated capacity models. Scale from megabytes to terabytes based on demand.

## When to use Event Hubs

Event Hubs is designed for high-throughput, low-latency event streaming scenarios. Consider Event Hubs when you need to:

| Scenario | Description |

|----------|-------------|

| **Real-time analytics** | Process streaming data to generate immediate insights, dashboards, and alerts |

| **IoT telemetry ingestion** | Collect device data from millions of IoT sensors, vehicles, or industrial equipment |

| **Application logging** | Centralize logs from distributed applications for monitoring and troubleshooting |

| **Clickstream analytics** | Analyze user behavior patterns across web and mobile applications |

| **Financial transactions** | Process high-volume trading data, fraud detection signals, and payment events |

| **Event sourcing** | Implement event-driven architectures with durable, ordered event storage |

### Choosing between Azure messaging services

Azure offers multiple messaging services. Use this guidance to select the right service:

| Service | Best for | Message pattern |

|---------|----------|-----------------|

| **Event Hubs** | High-throughput event streaming, telemetry, log aggregation | Many producers, multiple consumers, time-ordered events |

| **Service Bus** | Enterprise messaging with transactions, sessions, dead-lettering | Point-to-point or pub/sub with delivery guarantees |

| **Event Grid** | Reactive event-driven architectures, serverless triggers | Push-based event routing with filtering |

For detailed guidance, see [Choose between Azure messaging services](../service-bus-messaging/compare-messaging-services.md).

## How it works

Event Hubs provides a unified streaming platform with time-based retention, decoupling event producers from consumers. Both can perform large-scale data ingestion and processing through multiple protocols.

### Core components

| Component | Description |

|-----------|-------------|

| **Producer applications** | Applications that send events to Event Hubs using [Event Hubs SDKs](sdks.md), Kafka producer clients, or HTTPS |

| **Namespace** | Management container for one or more event hubs. Handles [streaming capacity](event-hubs-scalability.md), [network security](network-security.md), and [geo-disaster recovery](event-hubs-geo-dr.md) at the namespace level |

| **Event hub / Kafka topic** | An append-only distributed log that organizes events. Contains one or more [partitions](event-hubs-features.md#partitions) for parallel processing |

| **Partitions** | Ordered sequences of events used to scale throughput. Think of partitions as lanes on a freeway—more partitions enable higher throughput |

| **Consumer applications** | Applications that read events by tracking their position (offset) in each partition. Can use [Event Hubs SDKs](sdks.md) or Kafka consumer clients |

| **Consumer group** | A logical view of the event hub that enables multiple consumer applications to read the same stream independently, each maintaining its own position |

### Event flow

1. **Ingest**: Producer applications send events to an event hub. Events are assigned to partitions based on partition key or round-robin distribution.

2. **Store**: Events are durably stored with configurable retention (1-90 days depending on tier). The [Capture](event-hubs-capture-overview.md) feature can also write events to long-term storage.

3. **Process**: Consumer applications read events from partitions using consumer groups. Each consumer tracks its offset using [checkpointing](event-hubs-features.md#checkpointing) for reliable processing.

For a detailed explanation, see [Event Hubs features](event-hubs-features.md).

## Key capabilities

### Core platform features

#### Apache Kafka compatibility

Event Hubs is a multi-protocol event streaming engine that natively supports Apache Kafka, AMQP 1.0, and HTTPS. You can bring Kafka workloads to Event Hubs without code changes, cluster management, or third-party Kafka services.

Event Hubs is built as a cloud-native broker engine, delivering better performance and cost efficiency than self-managed Kafka clusters. For more information, see [Azure Event Hubs for Apache Kafka](azure-event-hubs-apache-kafka-overview.md).

#### Flexible scaling

Start with data streams in megabytes and grow to gigabytes or terabytes. The [auto-inflate](event-hubs-auto-inflate.md) feature automatically scales throughput units to meet demand. For predictable high-volume workloads, [dedicated clusters](event-hubs-dedicated-overview.md) provide reserved capacity.

#### Large message support (preview)

While most streaming scenarios involve lightweight messages under 1 MB, Event Hubs accommodates events up to 20 MB with [dedicated clusters](event-hubs-dedicated-overview.md). For more information, see [Send and receive large messages](event-hubs-quickstart-stream-large-messages.md).

### Data management

#### Schema Registry

[Azure Schema Registry](schema-registry-overview.md) provides a centralized repository for managing schemas of event streaming applications. It ensures data compatibility and consistency across producers and consumers, supports schema evolution, and integrates with Kafka applications using Avro and JSON schemas.

#### Capture

[Capture](event-hubs-capture-overview.md) your streaming data in near real time to Azure Blob Storage or Azure Data Lake Storage for long-term retention or batch analytics. Capture runs automatically on the same stream used for real-time processing.

### Azure integrations

#### Stream Analytics integration

Event Hubs integrates with [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) for real-time stream processing. Use the built-in no-code editor with drag-and-drop functionality, or write SQL-based queries for complex transformations.

For more information, see [Process Event Hubs data using Stream Analytics](../stream-analytics/no-code-build-power-bi-dashboard.md).

#### Azure Data Explorer integration

[Azure Data Explorer](/azure/data-explorer/data-explorer-overview) delivers high-performance analytics on large volumes of streaming data. Integrate Event Hubs with Data Explorer for near real-time analytics and exploration.

For more information, see [Ingest data from Event Hubs into Azure Data Explorer](/azure/data-explorer/ingest-data-event-hub-overview).

#### Azure Functions and serverless

Event Hubs integrates with [Azure Functions](../azure-functions/functions-bindings-event-hubs.md) for serverless event processing. The ecosystem also supports [Azure Spring Apps](/azure/developer/java/spring-framework/configure-spring-cloud-stream-binder-java-app-azure-event-hub), Kafka Connectors, Apache Spark, and Apache Flink.

### Local development

The [Event Hubs emulator](overview-emulator.md) provides a local development experience for developing and testing code against the service in isolation, free from cloud dependencies.

### Client libraries

Event Hubs provides [client libraries](sdks.md) for .NET, Java, Python, JavaScript, and Go. These SDKs support both AMQP and Kafka protocols, enabling you to choose the best fit for your application.

### Monitoring

[Monitor Event Hubs](monitor-event-hubs.md) using Azure Monitor metrics, diagnostic logs, and alerts. Track throughput, latency, errors, and consumer lag to ensure optimal performance.

## Security and compliance

Event Hubs provides enterprise-grade security features:

| Feature | Description |

|---------|-------------|

| **Authentication** | [Microsoft Entra ID](authenticate-application.md) with role-based access control (RBAC), [Shared Access Signatures](authenticate-shared-access-signature.md), or [Managed Identities](authenticate-managed-identity.md) |

| **Network security** | [Private Link](private-link-service.md) for private connectivity, [VNet service endpoints](event-hubs-service-endpoints.md), and [IP firewall rules](event-hubs-ip-filtering.md) |

| **Encryption** | Data encrypted at rest with Microsoft-managed or [customer-managed keys](configure-customer-managed-key.md), TLS 1.2 for data in transit |

For more information, see [Event Hubs security baseline](/security/benchmark/azure/baselines/event-hubs-security-baseline).

## High availability and disaster recovery

Event Hubs provides multiple layers of reliability:

- **Availability zones**: [Zone-redundant](event-hubs-availability-and-consistency.md) deployments distribute replicas across zones within a region (Premium and Dedicated tiers)

- **Geo-disaster recovery**: [Geo-DR](event-hubs-geo-dr.md) enables failover to a secondary region with metadata synchronization

- **SLA guarantees**: Up to [99.99% availability](https://azure.microsoft.com/support/legal/sla/event-hubs/) depending on tier and configuration

## Pricing tiers

For current pricing and detailed feature comparison, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/) and [quotas and limits](event-hubs-quotas.md).

## Related content

- [Event Hubs features and terminology](event-hubs-features.md)

- [Apache Kafka developer guide](apache-kafka-developer-guide.md)

- [Migrate from Apache Kafka to Event Hubs](apache-kafka-migration-guide.md)


# Azure Event Hubs Apache Kafka Overview

# What is Azure Event Hubs for Apache Kafka?

This article explains how you can use Azure Event Hubs to stream data from [Apache Kafka](https://kafka.apache.org) applications without setting up a Kafka cluster on your own.

## Overview

Azure Event Hubs provides an Apache Kafka endpoint on an event hub, which enables users to connect to the event hub using the Kafka protocol. You can often use an event hub's Kafka endpoint from your applications without any code changes. You modify only the configuration, that is, update the connection string in configurations to point to the Kafka endpoint exposed by your event hub instead of pointing to a Kafka cluster. Then, you can start streaming events from your applications that use the Kafka protocol into event hubs, which are equivalent to Kafka topics.

To learn more about how to migrate your Apache Kafka applications to Azure Event Hubs, see the [migration guide](apache-kafka-migration-guide.md).

> [!NOTE]

> - This feature is supported only in the **standard, premium, and **dedicated** tiers.

> - Event Hubs for Apache Kafka Ecosystems support [Apache Kafka version 1.0](https://kafka.apache.org/10/documentation.html) and later.

## Apache Kafka and Azure Event Hubs conceptual mapping

Conceptually, Apache Kafka and Event Hubs are very similar. They're both partitioned logs built for streaming data, whereby the client controls which part of the retained log it wants to read. The following table maps concepts between Apache Kafka and Event Hubs.

| Apache Kafka Concept | Event Hubs Concept|

| --- | --- |

| Cluster | Namespace |

| Topic | An event hub |

| Partition | Partition|

| Consumer Group | Consumer Group |

| Offset | Offset|

## Apache Kafka features supported on Azure Event Hubs

### Kafka Streams

Kafka Streams is a client library for stream analytics that is part of the Apache Kafka open-source project, but is separate from the Apache Kafka event broker.

> [!NOTE]

> Kafka Streams is currently in public preview in Premium and Dedicated tier.

Azure Event Hubs supports the Kafka Streams client library, with details and concepts available [here](apache-kafka-streams.md).

The most common reason Azure Event Hubs customers ask for Kafka Streams support is because they're interested in Confluent's "ksqlDB" product. "ksqlDB" is a proprietary shared source project that is [licensed such](https://github.com/confluentinc/ksql/blob/master/LICENSE) that no vendor "offering software-as-a-service, platform-as-a-service, infrastructure-as-a-service, or other similar online services that compete with Confluent products or services" is permitted to use or offer "ksqlDB" support. Practically, if you use ksqlDB, you must either operate Kafka yourself or you must use Confluent’s cloud offerings. The licensing terms might also affect Azure customers who offer services for a purpose excluded by the license.

Standalone and without ksqlDB, Kafka Streams has fewer capabilities than many alternative frameworks and services, most of which have built-in streaming SQL interfaces, and all of which integrate with Azure Event Hubs today:

- [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md)

- [Azure Synapse Analytics (via Event Hubs Capture)](../event-grid/event-hubs-integration.md)

- [Azure Databricks](/azure/databricks/scenarios/databricks-stream-from-eventhubs)

- [Apache Samza](https://samza.apache.org/learn/documentation/latest/connectors/eventhubs)

- [Apache Storm](event-hubs-storm-getstarted-receive.md)

- [Apache Spark](event-hubs-kafka-spark-tutorial.md)

- [Apache Flink](event-hubs-kafka-flink-tutorial.md)

- [Apache Flink on HDInsight on Azure Kubernetes Service](../hdinsight-aks/flink/flink-overview.md)

- [Akka Streams](event-hubs-kafka-akka-streams-tutorial.md)

### Kafka Transactions

> [!NOTE]

> Kafka Transactions is currently in public preview in Premium and Dedicated tier.

>

Azure Event Hubs supports Kafka transactions. For more details about the support and concepts, see [Apache Kafka transactions](apache-kafka-transactions.md).

### Compression

> [!NOTE]

> Kafka compression for Event Hubs is currently supported only in Premium and Dedicated tiers.

>

The client-side [compression](https://cwiki.apache.org/confluence/display/KAFKA/Compression) feature in Apache Kafka clients conserves compute resources and bandwidth by compressing a batch of multiple messages into a single message on the producer side and decompressing the batch on the consumer side. The Apache Kafka broker treats the batch as a special message.

Kafka producer application developers can enable message compression by setting the `compression.type` property. Azure Event Hubs currently supports `gzip` compression.

```properties

Compression.type = none | gzip

```

While the feature is only supported for Apache Kafka producer traffic and consumer traffic, AMQP consumer can consume compressed Kafka traffic as decompressed messages.

## Key differences between Apache Kafka and Azure Event Hubs

While [Apache Kafka](https://kafka.apache.org/) is software you typically need to install and operate, Event Hubs is a fully managed, cloud-native service. There are no servers, disks, or networks to manage and monitor and no brokers to consider or configure, ever. You create a namespace, which is an endpoint with a fully qualified domain name, and then you create Event Hubs (topics) within that namespace.

For more information about Event Hubs and namespaces, see [Event Hubs features](event-hubs-features.md#namespace). As a cloud service, Event Hubs uses a single stable virtual IP address as the endpoint, so clients don't need to know about the brokers or machines within a cluster. Even though Event Hubs implements the same protocol, this difference means that all Kafka traffic for all partitions is predictably routed through this one endpoint rather than requiring firewall access for all brokers of a cluster.

Scale in Event Hubs is controlled by how many [throughput units (TUs)](event-hubs-scalability.md#throughput-units) or [processing units](event-hubs-scalability.md#processing-units) you purchase. If you enable the [Auto-Inflate](event-hubs-auto-inflate.md) feature for a standard tier namespace, Event Hubs automatically scales up TUs when you reach the throughput limit. This feature also works with the Apache Kafka protocol support. For a premium tier namespace, you can increase the number of processing units assigned to the namespace.

## Is Apache Kafka the right solution for your workload?

If you come from a background of building applications that use Apache Kafka, it's also useful to understand that Azure Event Hubs is part of a fleet of services that also includes [Azure Service Bus](../service-bus-messaging/service-bus-messaging-overview.md) and [Azure Event Grid](../event-grid/overview.md).

While some providers of commercial distributions of Apache Kafka might suggest that Apache Kafka is a one-stop shop for all your messaging platform needs, the reality is that Apache Kafka doesn't implement, for instance, the [competing-consumer](/azure/architecture/patterns/competing-consumers) queue pattern. It doesn't support [publish-subscribe](/azure/architecture/patterns/publisher-subscriber) at a level that allows subscribers access to the incoming messages based on server-evaluated rules other than plain offsets. It has no facilities to track the lifecycle of a job initiated by a message or sidelining faulty messages into a dead-letter queue. All of these features are foundational for many enterprise messaging scenarios.

To understand the differences between patterns and which pattern is best covered by which service, see the [Asynchronous messaging options in Azure](/azure/architecture/guide/technology-choices/messaging) guidance. As an Apache Kafka user, you can find that communication paths you realized with Kafka can be realized with far less basic complexity and yet more powerful capabilities by using either Event Grid or Service Bus.

If you need specific features of Apache Kafka that aren't available through the Event Hubs for Apache Kafka interface or if your implementation pattern exceeds the [Event Hubs quotas](event-hubs-quotas.md), you can also run a [native Apache Kafka cluster in Azure HDInsight](../hdinsight/kafka/apache-kafka-introduction.md).

## Security and authentication

Every time you publish or consume events from an Event Hubs for Kafka, your client tries to access the Event Hubs resources. You want to ensure that the resources are accessed using an authorized entity. When using Apache Kafka protocol with your clients, set your configuration for authentication and encryption using the SASL mechanisms. When using Event Hubs for Kafka, TLS-encryption is required (as all data in transit with Event Hubs is TLS encrypted). You can specify the SASL_SSL option in your configuration file.

Azure Event Hubs provides multiple options to authorize access to your secure resources:

- OAuth 2.0

- Shared access signature (SAS)

### OAuth 2.0

Event Hubs integrates with Microsoft Entra ID, which provides an **OAuth 2.0** compliant centralized authorization server. By using Microsoft Entra ID, you can use Azure role-based access control (Azure RBAC) to grant fine grained permissions to your client identities. Use this feature with your Kafka clients by specifying **SASL_SSL** for the protocol and  **OAUTHBEARER** for the mechanism. For details about Azure roles and levels for scoping access, see [Authorize access with Microsoft Entra ID](authorize-access-azure-active-directory.md).

```properties

bootstrap.servers=NAMESPACENAME.servicebus.windows.net:9093

security.protocol=SASL_SSL

sasl.mechanism=OAUTHBEARER

sasl.jaas.config=org.apache.kafka.common.security.oauthbearer.OAuthBearerLoginModule required;

sasl.login.callback.handler.class=CustomAuthenticateCallbackHandler

```

> [!NOTE]

> These configuration properties are for the Java programming language. For **samples** that show how to use OAuth with Event Hubs for Kafka using different programming languages, see [samples on GitHub](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/oauth).

### Shared Access Signature (SAS)

Event Hubs also provides **Shared Access Signatures (SAS)** for delegated access to Event Hubs for Kafka resources. Authorizing access using the OAuth 2.0 token-based mechanism provides superior security and ease of use over SAS. The built-in roles can also eliminate the need for ACL-based authorization, which you have to maintain and manage. You can use this feature with your Kafka clients by specifying **SASL_SSL** for the protocol and **PLAIN** for the mechanism.

```properties

bootstrap.servers=NAMESPACENAME.servicebus.windows.net:9093

security.protocol=SASL_SSL

sasl.mechanism=PLAIN

sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";

```

> [!IMPORTANT]

> Replace `{YOUR.EVENTHUBS.CONNECTION.STRING}` with the connection string for your Event Hubs namespace. For instructions on getting the connection string, see [Get an Event Hubs connection string](event-hubs-get-connection-string.md). Here's an example configuration: `sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="Endpoint=sb://mynamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=XXXXXXXXXXXXXXXX";`

> [!NOTE]

> When using SAS authentication with Kafka clients, established connections aren't disconnected when the SAS key is regenerated.

> [!NOTE]

> [Generated shared access signature tokens](authenticate-shared-access-signature.md#generate-a-shared-access-signature-token) aren't supported when using the Event Hubs for Apache Kafka endpoint.

## Samples

For a **tutorial** with step-by-step instructions to create an event hub and access it using SAS or OAuth, see [Quickstart: Data streaming with Event Hubs using the Kafka protocol](event-hubs-quickstart-kafka-enabled-event-hubs.md).

## Other Azure Event Hubs features

The Event Hubs for Apache Kafka feature is one of three protocols concurrently available on Azure Event Hubs along with HTTP and AMQP. You can write with any of these protocols and read with any another, so that your current Apache Kafka producers can continue publishing via Apache Kafka, but your reader can benefit from the native integration with Event Hubs' AMQP interface, such as Azure Stream Analytics or Azure Functions. Conversely, you can readily integrate Azure Event Hubs into AMQP routing networks as a target endpoint, and yet read data through Apache Kafka integrations.

Additionally, Event Hubs features such as [Capture](event-hubs-capture-overview.md), which enables extremely cost efficient long-term archival via Azure Blob Storage and Azure Data Lake Storage, and [Geo Disaster-Recovery](event-hubs-geo-dr.md) also work with the Event Hubs for Kafka feature.

## Idempotency

Azure Event Hubs for Apache Kafka supports both idempotent producers and idempotent consumers.

One of the core tenets of Azure Event Hubs is the concept of **at-least once** delivery. This approach ensures that events are always delivered. It also means that consumers can receive events more than once, even repeatedly. For this reason, it's important that the consumer supports the [idempotent consumer](https://microservices.io/patterns/communication-style/idempotent-consumer.html) pattern.

## Related content

This article introduces Event Hubs for Kafka. To learn more, see [Apache Kafka developer guide for Azure Event Hubs](apache-kafka-developer-guide.md).

For a **tutorial** with step-by-step instructions to create an event hub and access it using SAS or OAuth, see [Quickstart: Data streaming with Event Hubs using the Kafka protocol](event-hubs-quickstart-kafka-enabled-event-hubs.md).

Also, see the [OAuth samples on GitHub](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/oauth).


# Schema Registry Overview

# Azure Schema Registry in Event Hubs

Event streaming and messaging scenarios often deal with structured data in the event or message payload. However, the structured data is of little value to the event broker, which only deals with bytes. Schema-driven formats such as [Apache Avro](https://avro.apache.org/), [JSONSchema](https://json-schema.org/), or [Protobuf](https://protobuf.dev/) are often used to serialize or deserialize such structured data to/from binary.

An event producer uses a schema definition to serialize the event payload and publish it to an event broker such as Event Hubs. Event consumers read the event payload from the broker and deserialize it by using the same schema definition.

Both producers and consumers can validate the integrity of the data by using the same schema.

## What is Azure Schema Registry?

**Azure Schema Registry** is a feature of Event Hubs that provides a central repository for schemas for event-driven and messaging-centric applications. It provides the flexibility for your producer and consumer applications to **exchange data without having to manage and share the schema**. It also provides a simple governance framework for reusable schemas and defines relationship between schemas through a logical grouping construct (schema groups).

With schema-driven serialization frameworks like Apache Avro, JSONSchema, and Protobuf, moving serialization metadata into shared schemas can also help **reduce the per-message overhead**. Each message doesn't need to include the metadata (type information and field names) as it does with tagged formats such as JSON.

> [!NOTE]

> The feature is available in the **Standard**, **Premium**, and **Dedicated** tiers.

>

Storing schemas alongside the events and inside the eventing infrastructure ensures that the metadata required for serialization or deserialization is always available and schemas can't be misplaced.

## Related content

- To learn more about Azure Schema registry, see [Azure Schema Registry Concepts](schema-registry-concepts.md).

- To learn how to create a schema registry using the Azure portal, see [Create an Event Hubs schema registry using the Azure portal](create-schema-registry.md).

- See the following **Schema Registry Avro client library** samples.

- [.NET](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/schemaregistry/Microsoft.Azure.Data.SchemaRegistry.ApacheAvro/tests/Samples)

- [Java](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/schemaregistry/azure-data-schemaregistry-apacheavro/src/samples)

- [JavaScript](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/schemaregistry/schema-registry-avro/samples)

- [Python](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/schemaregistry/azure-schemaregistry-avroencoder/samples)

- [Kafka Avro Integration for Azure Schema Registry](https://github.com/Azure/azure-schema-registry-for-kafka/tree/master/csharp/avro/samples)


# Event Hubs Features

﻿---

title: Event Hubs features and terminology

description: Learn about the core concepts, features, and terminology of Azure Event Hubs including namespaces, partitions, consumers, and protocols.

ms.topic: concept-article

ms.date: 01/12/2026

---

# Event Hubs features and terminology

This article explains the core concepts and terminology of Azure Event Hubs. For a high-level overview, see [What is Event Hubs?](./event-hubs-about.md)

## Concepts at a glance

| Concept | Description |

|---------|-------------|

| **Namespace** | Management container for one or more event hubs. Controls network access and scaling. |

| **Event hub** | An append-only log that stores events. Equivalent to a Kafka topic. |

| **Partition** | Ordered sequence of events within an event hub. Enables parallel processing. |

| **Producer/Publisher** | Application that sends events to an event hub. |

| **Consumer** | Application that reads events from an event hub. |

| **Consumer group** | Independent view of the event stream. Multiple groups can read the same data separately. |

| **Offset** | Position of an event within a partition. Used to track reading progress. |

| **Checkpointing** | Saving the current offset so consumers can resume from where they left off. |

---

## Architecture

### Namespace

An Event Hubs **namespace** is a management container for event hubs (or topics, in Kafka parlance). It provides network endpoints and controls access through features like [IP filtering](event-hubs-ip-filtering.md), [virtual network service endpoints](event-hubs-service-endpoints.md), and [Private Link](private-link-service.md).

### Partitions

[!INCLUDE [event-hubs-partitions](./includes/event-hubs-partitions.md)]

---

## Event producers

A **producer** (or publisher) is any application that sends events to an event hub.

### Publishing options

| Method | Description |

|--------|-------------|

| **Azure SDKs** | [.NET](event-hubs-dotnet-standard-getstarted-send.md), [Java](event-hubs-java-get-started-send.md), [Python](event-hubs-python-get-started-send.md), [JavaScript](event-hubs-node-get-started-send.md), [Go](event-hubs-go-get-started-send.md) |

| **REST API** | [HTTP POST requests](/rest/api/eventhub/) for lightweight clients |

| **Kafka clients** | Use existing Kafka producers without code changes |

| **AMQP 1.0** | Any AMQP client such as [Apache Qpid](https://qpid.apache.org/) |

### Key behaviors

- **Batch or individual**: Publish events one at a time or in batches. Maximum 1 MB per publish operation.

- **Partition keys**: Specify a partition key to group related events in the same partition, ensuring ordered delivery.

- **Authorization**: Use Microsoft Entra ID (OAuth2) or Shared Access Signatures (SAS) for access control.

<a name="publisher-policy"></a>

### Publisher policies

Publisher policies enable granular control when you have many independent publishers. Each publisher uses a unique identifier:

```http

//<my namespace>.servicebus.windows.net/<event hub name>/publishers/<my publisher name>

```

The publisher name must match the SAS token used for authentication. When using publisher policies, the **PartitionKey** must match the publisher name.

---

<a name="event-consumers"></a>

## Event consumers

A **consumer** is any application that reads events from an event hub. Event Hubs uses a **pull model**—consumers request events rather than having events pushed to them.

### Consumer groups

A **consumer group** is an independent view of the event stream. Multiple consumer groups can read the same event hub simultaneously, each tracking their own position.

| Guideline | Recommendation |

|-----------|----------------|

| Readers per partition | One active reader per partition within a consumer group (up to five in special scenarios) |

| Default group | Every event hub has a default consumer group (`$Default`) |

| Multiple applications | Create separate consumer groups for each application (analytics, archival, alerting) |

```http

//<my namespace>.servicebus.windows.net/<event hub name>/<Consumer Group #1>

//<my namespace>.servicebus.windows.net/<event hub name>/<Consumer Group #2>

```

### Offsets

An **offset** is the position of an event within a partition—think of it as a cursor. Consumers use offsets to specify where to start reading. You can start from:

- A specific offset value

- A timestamp

- The beginning or end of the stream

### Checkpointing

**Checkpointing** is when a consumer saves its current offset. This enables:

- **Resumption**: If a consumer disconnects, it resumes from the last checkpoint

- **Failover**: A new consumer instance can take over from where another left off

- **Replay**: Process historical events by specifying an earlier offset

> [!IMPORTANT]

> In AMQP, checkpointing is the consumer's responsibility. The Event Hubs service provides offsets, but consumers must store checkpoints.

[!INCLUDE [storage-checkpoint-store-recommendations](./includes/storage-checkpoint-store-recommendations.md)]

### Event processor clients

The Azure SDKs provide intelligent consumer clients that handle partition management, load balancing, and checkpointing automatically:

| Language | Client |

|----------|--------|

| .NET | [EventProcessorClient](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient) |

| Java | [EventProcessorClient](https://github.com/Azure/azure-sdk-for-java/blob/master/sdk/eventhubs/azure-messaging-eventhubs/src/main/java/com/azure/messaging/eventhubs/EventProcessorClient.java) |

| Python | [EventHubConsumerClient](/python/api/azure-eventhub/azure.eventhub.aio.eventhubconsumerclient) |

| JavaScript | [EventHubConsumerClient](/javascript/api/@azure/event-hubs/eventhubconsumerclient) |

### Event data structure

Each event contains:

- **Body**: The event payload

- **Offset**: Position in the partition

- **Sequence number**: Order within the partition

- **User properties**: Custom metadata

- **System properties**: Service-assigned metadata (enqueue time, etc.)

---

## Data management

### Event retention

Events are automatically removed based on a time-based retention policy.

| Tier | Default | Maximum |

|------|---------|---------|

| Standard | 1 hour | 7 days |

| Premium | 1 hour | 90 days |

| Dedicated | 1 hour | 90 days |

Key points:

- Events can't be explicitly deleted

- Retention changes apply to existing events

- Events become unavailable exactly when the retention period expires

> [!NOTE]

> Event Hubs is a real-time streaming engine, not a database. For long-term storage, use [Event Hubs Capture](event-hubs-capture-overview.md) to archive events to [Azure Storage](../storage/blobs/storage-blobs-overview.md), [Data Lake Storage](../data-lake-store/data-lake-store-overview.md), or [Azure Synapse](store-captured-data-data-warehouse.md).

### Event Hubs Capture

[Capture](event-hubs-capture-overview.md) automatically saves streaming data to Azure Blob Storage or Azure Data Lake Storage. Configure a minimum size and time window to control capture frequency.

| Format | Description |

|--------|-------------|

| **Avro** | Default format for captured data |

| **Parquet** | Available through the no-code editor in Azure portal ([learn more](../stream-analytics/capture-event-hub-data-parquet.md?toc=%2Fazure%2Fevent-hubs%2Ftoc.json)) |

### Log compaction

[Log compaction](log-compaction.md) retains only the latest event for each unique key, rather than using time-based retention. Useful for maintaining current state without storing full history.

---

## Protocols

Event Hubs supports multiple protocols for flexibility across different client types.

| Protocol | Send | Receive | Best for |

|----------|------|---------|----------|

| **AMQP 1.0** | Yes | Yes | High throughput, low latency, persistent connections |

| **Apache Kafka** | Yes | Yes | Existing Kafka applications (version 1.0+) |

| **HTTPS** | Yes | No | Lightweight clients, firewall-restricted environments |

### Protocol comparison

- **AMQP**: Requires persistent bidirectional socket. Higher initial cost, but better performance for frequent operations. Used by Azure SDKs.

- **Kafka**: Native support means existing Kafka applications work without code changes. Just reconfigure the bootstrap server to point to your Event Hubs namespace.

- **HTTPS**: Simple HTTP POST for sending. No receiving support. Good for occasional, low-volume publishing.

For Kafka integration details, see [Event Hubs for Apache Kafka](azure-event-hubs-apache-kafka-overview.md).

---

## Access control

### Microsoft Entra ID

Microsoft Entra ID provides OAuth 2.0 authentication with role-based access control (RBAC). Assign built-in roles to control access:

| Role | Permissions |

|------|-------------|

| **Azure Event Hubs Data Owner** | Full access to send and receive events |

| **Azure Event Hubs Data Sender** | Send events only |

| **Azure Event Hubs Data Receiver** | Receive events only |

For details, see [Authorize access with Microsoft Entra ID](authorize-access-azure-active-directory.md).

### Shared Access Signatures (SAS)

SAS tokens provide scoped access at the namespace or event hub level. A SAS token is generated from a SAS key and typically grants only **send** or **listen** permissions.

For details, see [Shared Access Signature authentication](../service-bus-messaging/service-bus-sas.md).

### Application groups

[Application groups](resource-governance-overview.md) let you define resource access policies (like throttling) for collections of client applications that share a security context (SAS policy or Microsoft Entra application ID).

---

## Related content

### Get started

- [.NET quickstart](event-hubs-dotnet-standard-getstarted-send.md)

- [Java quickstart](event-hubs-java-get-started-send.md)

- [Python quickstart](event-hubs-python-get-started-send.md)

- [JavaScript quickstart](event-hubs-node-get-started-send.md)

### Learn more

- [Scalability and throughput units](event-hubs-scalability.md)

- [Availability and consistency](event-hubs-availability-and-consistency.md)

- [Event Hubs Capture overview](event-hubs-capture-overview.md)

- [Event Hubs for Apache Kafka](azure-event-hubs-apache-kafka-overview.md)

### Reference

- [Quotas and limits](event-hubs-quotas.md)

- [Event Hubs FAQ](event-hubs-faq.yml)

- [Event Hubs samples](event-hubs-samples.md)


# Event Hubs Quotas

# Azure Event Hubs quotas and limits

The following tables provide quotas and limits specific to [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/). For information about Event Hubs pricing, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).

## Common limits for all tiers

[!INCLUDE [event-hubs-common-limits](./includes/event-hubs-common-limits.md)]

## Basic vs. standard vs. premium vs. dedicated tiers

[!INCLUDE [event-hubs-tier-limits](./includes/event-hubs-tier-limits.md)]

[!INCLUDE [event-hubs-tier-features](./includes/event-hubs-tier-features.md)]

## Next steps

You can learn more about Event Hubs by visiting the following links:

* [Event Hubs overview](./event-hubs-about.md)

* [Auto-inflate](event-hubs-auto-inflate.md)

* [Event Hubs FAQ](event-hubs-faq.yml)


# Event Hubs Create

# Quickstart: Create an event hub using Azure portal

In this quickstart, you create an Azure Event Hubs namespace and an event hub in the namespace by using the [Azure portal](https://portal.azure.com).

## Prerequisites

- An Azure subscription. If you don't have one, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

- If you're new to Azure Event Hubs, read through [Event Hubs overview](event-hubs-about.md) and [Event Hubs features](event-hubs-features.md).

## Create a resource group

A resource group is a logical collection of Azure resources. All resources are deployed and managed in a resource group. To create a resource group:

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the left navigation, select **Resource groups**, and then select **Create**.

1. For **Subscription**, select the name of the Azure subscription in which you want to create the resource group.

1. Type a unique **name for the resource group**. The system immediately checks to see if the name is available in the currently selected Azure subscription.

1. Select a **region** for the resource group.

1. Select **Review + Create**.

1. On the **Review + Create** page, select **Create**.

## Create an Event Hubs namespace

An Event Hubs namespace provides a unique scoping container, in which you create one or more event hubs. To create a namespace in your resource group using the portal, do the following actions:

1. In the Azure portal, select **All services** in the left menu, and select **Event Hubs** in the **Analytics** category.

1. On the **Event Hubs** page, select **Create** on the toolbar.

1. On the **Create namespace** page, take the following steps:

1. Select the **subscription** in which you want to create the namespace.

1. Select the **resource group** you created in the previous step.

1. Enter a **name** for the namespace. The system immediately checks to see if the name is available.

1. Select a **location** for the namespace.

1. Choose **Basic** for the **pricing tier**. If you plan to use the namespace from **Apache Kafka** apps, use the **Standard** tier. The basic tier doesn't support Apache Kafka workloads. To learn about differences between tiers, see [Quotas and limits](event-hubs-quotas.md), [Event Hubs Premium](event-hubs-premium-overview.md), and [Event Hubs Dedicated](event-hubs-dedicated-overview.md) articles.

1. Leave the **throughput units** (for standard tier) or **processing units** (for premium tier) settings as it is. To learn about throughput units or processing units: [Event Hubs scalability](event-hubs-scalability.md).

1. Enable the **Auto-inflate** feature if you want Event Hubs to automatically increase the number of throughput units (TUs) to meet usage needs. Increasing TUs prevents throttling scenarios where data ingress or data egress rates exceed the rates allowed by the TUs assigned to the namespace. The Event Hubs service increases the throughput when load increases beyond the minimum threshold, without any requests failing with ServerBusy errors.

1. Select **Review + Create** at the bottom of the page.

1. On the **Review + Create** page, review the settings, and select **Create**. Wait for the deployment to complete.

1. On the **Deployment** page, select **Go to resource** to navigate to the page for your namespace.

1. Confirm that you see the **Event Hubs namespace** page similar to the following example:

> [!NOTE]

> Azure Event Hubs provides you with a Kafka endpoint. This endpoint enables your Event Hubs namespace to natively understand [Apache Kafka](https://kafka.apache.org/intro) message protocol and APIs. With this capability, you can communicate with your event hubs as you would with Kafka topics without changing your protocol clients or running your own clusters. Event Hubs supports [Apache Kafka versions 1.0](https://kafka.apache.org/10/documentation.html) and later. For more information, see [Use Event Hubs from Apache Kafka applications](azure-event-hubs-apache-kafka-overview.md).

## Create an event hub

To create an event hub within the namespace, do the following actions:

1. On the **Overview** page, select **+ Event hub** on the command bar.

1. Type a name for your event hub, then select **Review + create**.

The **partition count** setting allows you to parallelize consumption across many consumers. For more information, see [Partitions](event-hubs-scalability.md#partitions).

The **message retention** setting specifies how long the Event Hubs service keeps data. For more information, see [Event retention](event-hubs-features.md#event-retention).

1. On the **Review + create** page, select **Create**.

1. You can check the status of the event hub creation in alerts. After the event hub is created, you see it in the list of event hubs.

## Related content

In this article, you created a resource group, an Event Hubs namespace, and an event hub. For step-by-step instructions to send events to (or) receive events from an event hub, see these tutorials:

- [.NET Core](event-hubs-dotnet-standard-getstarted-send.md)

- [Java](event-hubs-java-get-started-send.md)

- [Python](event-hubs-python-get-started-send.md)

- [JavaScript](event-hubs-node-get-started-send.md)

- [Go](event-hubs-go-get-started-send.md)

- [C (send only)](event-hubs-c-getstarted-send.md)

- [Apache Storm (receive only)](event-hubs-storm-getstarted-receive.md)

[3]: ./media/event-hubs-quickstart-portal/sender1.png

[4]: ./media/event-hubs-quickstart-portal/receiver1.png


# Event Hubs Quickstart Cli

# Quickstart: Create an event hub using Azure CLI

In this quickstart, you will create an event hub using Azure CLI.

[!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment.md](~/reusable-content/azure-cli/azure-cli-prepare-your-environment.md)]

- This article requires version 2.0.4 or later of the Azure CLI. If using Azure Cloud Shell, the latest version is already installed.

## Create a resource group

Run the following command to create a resource group. A resource group is a logical collection of Azure resources. All resources are deployed and managed in a resource group.

Select **Copy** to copy the command and paste it into the Cloud Shell or CLI window, and run it. Update the resource group name and the region if you like.

```azurecli-interactive

rgName="contosorg$RANDOM"

region="eastus"

az group create --name $rgName --location $region

```

You see the output similar to the following one. You see the resource group name in the `name` field with a random number replacing `$RANDOM`.

```json

{

"id": "/subscriptions/0000000000-0000-0000-0000-000000000000000/resourceGroups/contosorg32744",

"location": "eastus",

"managedBy": null,

"name": "contosorg32744",

"properties": {

"provisioningState": "Succeeded"

},

"tags": null,

"type": "Microsoft.Resources/resourceGroups"

}

```

## Create an Event Hubs namespace

Run the following command to create an Event Hubs namespace. An Event Hubs namespace provides a unique scoping container, referenced by its fully qualified domain name, in which you create one or more event hubs. Update the name of the namespace if you like.

```azurecli-interactive

# Create an Event Hubs namespace. Specify a name for the Event Hubs namespace.

namespaceName="contosoehubns$RANDOM"

az eventhubs namespace create --name $namespaceName --resource-group $rgName -l $region

```

You see the output similar to the following one. You see the name of the namespace in the `name` field.

```json

{

"createdAt": "2023-03-13T20:28:53.037Z",

"disableLocalAuth": false,

"id": "/subscriptions/0000000000-0000-0000-0000-0000000000000000/resourceGroups/contosorg32744/providers/Microsoft.EventHub/namespaces/contosoehubns17861",

"isAutoInflateEnabled": false,

"kafkaEnabled": true,

"location": "East US",

"maximumThroughputUnits": 0,

"metricId": "0000000000-0000-0000-0000-0000000000000000:contosoehubns17861",

"minimumTlsVersion": "1.2",

"name": "contosoehubns17861",

"provisioningState": "Succeeded",

"publicNetworkAccess": "Enabled",

"resourceGroup": "contosorg32744",

"serviceBusEndpoint": "https://contosoehubns17861.servicebus.windows.net:443/",

"sku": {

"capacity": 1,

"name": "Standard",

"tier": "Standard"

},

"status": "Active",

"tags": {},

"type": "Microsoft.EventHub/Namespaces",

"updatedAt": "2023-03-13T20:29:45.637Z",

"zoneRedundant": false

}

```

## Create an event hub

Run the following command to create an event hub. Update the name of the event hub if you like.

```azurecli-interactive

# Create an event hub. Specify a name for the event hub.

eventhubName="contosoehub$RANDOM"

az eventhubs eventhub create --name $eventhubName --resource-group $rgName --namespace-name $namespaceName

```

You see the output similar to the following one. You see the name of the event hub in the `name` field.

```json

{

"captureDescription": null,

"createdAt": "2023-03-13T20:32:04.457000+00:00",

"id": "/subscriptions/000000000-0000-0000-0000-00000000000000/resourceGroups/contosorg32744/providers/Microsoft.EventHub/namespaces/contosoehubns17861/eventhubs/contosoehub23255",

"location": "eastus",

"messageRetentionInDays": 7,

"name": "contosoehub23255",

"partitionCount": 4,

"partitionIds": [

"0",

"1",

"2",

"3"

],

"resourceGroup": "contosorg32744",

"status": "Active",

"systemData": null,

"type": "Microsoft.EventHub/namespaces/eventhubs",

"updatedAt": "2023-03-13T20:32:04.727000+00:00"

}

```

Congratulations! You have used Azure CLI to create an Event Hubs namespace, and an event hub within that namespace.

## Clean up resources

If you want to keep this event hub so that you can test sending and receiving events, ignore this section. Otherwise, run the following command to delete the resource group. This command deletes all the resources in the resource group and the resource group itself.

```azurecli-interactive

az group delete --name $rgName

```

## Next steps

In this article, you created a resource group, an Event Hubs namespace, and an event hub. For step-by-step instructions to send events to (or) receive events from an event hub, see the **Send and receive events** tutorials:

- [.NET Core](event-hubs-dotnet-standard-getstarted-send.md)

- [Java](event-hubs-java-get-started-send.md)

- [Python](event-hubs-python-get-started-send.md)

- [JavaScript](event-hubs-node-get-started-send.md)

- [Go](event-hubs-go-get-started-send.md)

- [C (send only)](event-hubs-c-getstarted-send.md)

- [Apache Storm (receive only)](event-hubs-storm-getstarted-receive.md)


# Event Hubs Quickstart Powershell

# Quickstart: Create an event hub using Azure PowerShell

In this quickstart, you create an event hub using Azure PowerShell.

## Prerequisites

An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

[!INCLUDE [cloud-shell-try-it.md](~/reusable-content/ce-skilling/azure/includes/cloud-shell-try-it.md)]

If you're using PowerShell locally, you must run the latest version of PowerShell to complete this quickstart. If you need to install or upgrade, see [Install and Configure Azure PowerShell](/powershell/azure/install-azure-powershell).

## Create a resource group

Run the following command to create a resource group. A resource group is a logical collection of Azure resources. All resources are deployed and managed in a resource group.

If you're using Azure Cloud Shell, switch to **PowerShell** from **Bash** in the upper left corner. Select **Copy** to copy the command and paste it into the Cloud Shell, and run it.

The following example creates a resource group in the East US region. Replace `myResourceGroup` with the name of the resource group you want to use.

```azurepowershell-interactive

$rgName="myResourceGroup$(Get-Random)"

$region="eastus"

New-AzResourceGroup –Name $rgName –Location $region

```

You see the output similar to the following one. You see the name of the resource with the random number suffix.

```bash

ResourceGroupName : myResourceGroup1625872532

Location          : eastus

ProvisioningState : Succeeded

Tags              :

ResourceId        : /subscriptions/0000000000-0000-0000-0000-0000000000000/resourceGroups/myResourceGroup1625872532

```

## Create an Event Hubs namespace

Run the following command to create an Event Hubs namespace in the resource group. An Event Hubs namespace provides a unique fully qualified domain name in which you can create one or more event hubs. Update the value of the namespace if you like.

```azurepowershell-interactive

$namespaceName="myNamespace$(Get-Random)"

New-AzEventHubNamespace -ResourceGroupName $rgName -Name $namespaceName -Location $region

```

You see the output similar to the following one. You see the name of the namespace in the `Name` field.

```bash

Name                   : myNamespace143349827

Id                     : /subscriptions/0000000000-0000-0000-0000-00000000000000/resourceGroups/myResourceGroup162587253

2/providers/Microsoft.EventHub/namespaces/myNamespace143349827

ResourceGroupName      : myResourceGroup1625872532

Location               : East US

Sku                    : Name : Standard , Capacity : 1 , Tier : Standard

Tags                   :

ProvisioningState      : Succeeded

Status                 : Active

CreatedAt              : 3/13/2023 10:22:54 PM

UpdatedAt              : 3/13/2023 10:23:41 PM

ServiceBusEndpoint     : https://myNamespace143349827.servicebus.windows.net:443/

Enabled                : True

KafkaEnabled           : True

IsAutoInflateEnabled   : False

MaximumThroughputUnits : 0

ZoneRedundant          : False

ClusterArmId           :

DisableLocalAuth       : False

MinimumTlsVersion      : 1.2

KeySource              :

Identity               :

IdentityType           :

IdentityId             :

EncryptionConfig       :

```

## Create an event hub

Now that you have an Event Hubs namespace, create an event hub within that namespace by running the following command.

```azurepowershell-interactive

$ehubName="myEventHub"

New-AzEventHub -ResourceGroupName $rgName -NamespaceName $namespaceName -EventHubName $ehubName

```

You see output similar to the following one.

```bash

ArchiveNameFormat            :

BlobContainer                :

CaptureEnabled               :

CreatedAt                    : 3/13/2023 10:26:07 PM

DataLakeAccountName          :

DataLakeFolderPath           :

DataLakeSubscriptionId       :

DestinationName              :

Encoding                     :

Id                           : /subscriptions/00000000000-0000-0000-0000-00000000000000/resourceGroups/myResourceGroup162

5872532/providers/Microsoft.EventHub/namespaces/myNamespace143349827/eventhubs/myEven

tHub

IntervalInSeconds            :

Location                     : eastus

MessageRetentionInDays       : 7

Name                         : myEventHub

PartitionCount               : 4

PartitionId                  : {0, 1, 2, 3}

ResourceGroupName            : myResourceGroup1625872532

SizeLimitInBytes             :

SkipEmptyArchive             :

Status                       : Active

StorageAccountResourceId     :

SystemDataCreatedAt          :

SystemDataCreatedBy          :

SystemDataCreatedByType      :

SystemDataLastModifiedAt     :

SystemDataLastModifiedBy     :

SystemDataLastModifiedByType :

Type                         : Microsoft.EventHub/namespaces/eventhubs

UpdatedAt                    : 3/13/2023 10:26:07 PM

```

Congratulations! You have used Azure PowerShell to create an Event Hubs namespace, and an event hub within that namespace.

## Clean up resources

If you want to keep this event hub so that you can test sending and receiving events, ignore this section. Otherwise, run the following command to delete the resource group. This command deletes all the resources in the resource group and the resource group itself.

```azurepowershell-interactive

Remove-AzResourceGroup $rgName

```

## Next steps

In this article, you created the Event Hubs namespace, and used sample applications to send and receive events from your event hub. For step-by-step instructions to send events to (or) receive events from an event hub, see the **Send and receive events** tutorials:

- [.NET Core](event-hubs-dotnet-standard-getstarted-send.md)

- [Java](event-hubs-java-get-started-send.md)

- [Python](event-hubs-python-get-started-send.md)

- [JavaScript](event-hubs-node-get-started-send.md)

- [Go](event-hubs-go-get-started-send.md)

- [C (send only)](event-hubs-c-getstarted-send.md)

- [Apache Storm (receive only)](event-hubs-storm-getstarted-receive.md)

[create a free account]: https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn

[Install and Configure Azure PowerShell]: /powershell/azure/install-az-ps

[New-AzResourceGroup]: /powershell/module/az.resources/new-azresourcegroup

[fully qualified domain name]: https://wikipedia.org/wiki/Fully_qualified_domain_name

[3]: ./media/event-hubs-quickstart-powershell/sender1.png

[4]: ./media/event-hubs-quickstart-powershell/receiver1.png

[5]: ./media/event-hubs-quickstart-powershell/metrics.png


# Event Hubs Bicep Namespace Event Hub

# Quickstart: Create an event hub by using Bicep

Azure Event Hubs is a Big Data streaming platform and event ingestion service, capable of receiving and processing millions of events per second. Event Hubs can process and store events, data, or telemetry produced by distributed software and devices. Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters. For detailed overview of Event Hubs, see [Event Hubs overview](event-hubs-about.md) and [Event Hubs features](event-hubs-features.md). In this quickstart, you create an event hub by using [Bicep](../azure-resource-manager/bicep/overview.md). You deploy a Bicep file to create a namespace of type [Event Hubs](./event-hubs-about.md), with one event hub.

[!INCLUDE [About Bicep](~/reusable-content/ce-skilling/azure/includes/resource-manager-quickstart-bicep-introduction.md)]

## Prerequisites

If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Review the Bicep file

The Bicep file used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/eventhubs-create-namespace-and-eventhub/).

The resources defined in the Bicep file include:

- [**Microsoft.EventHub/namespaces**](/azure/templates/microsoft.eventhub/namespaces)

- [**Microsoft.EventHub/namespaces/eventhubs**](/azure/templates/microsoft.eventhub/namespaces/eventhubs)

## Deploy the Bicep file

1. Save the Bicep file as **main.bicep** to your local computer.

1. Deploy the Bicep file using either Azure CLI or Azure PowerShell.

# [CLI](#tab/CLI)

```azurecli

az group create --name exampleRG --location eastus

az deployment group create --resource-group exampleRG --template-file main.bicep --parameters projectName=<project-name>

```

# [PowerShell](#tab/PowerShell)

```azurepowershell

New-AzResourceGroup -Name exampleRG -Location eastus

New-AzResourceGroupDeployment -ResourceGroupName exampleRG -TemplateFile ./main.bicep -projectName "<project-name>"

```

---

> [!NOTE]

> Replace **\<project-name\>** with a project name. It will be used to generate the Event Hubs name and the Namespace name.

When the deployment finishes, you should see a message indicating the deployment succeeded.

## Validate the deployment

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

When no longer needed, use the Azure portal, Azure CLI, or Azure PowerShell to delete the VM and all of the resources in the resource group.

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

In this article, you created an Event Hubs namespace and an event hub in the namespace using Bicep. For step-by-step instructions to send events to (or) receive events from an event hub, see the **Send and receive events** tutorials:

- [.NET Core](event-hubs-dotnet-standard-getstarted-send.md)

- [Java](event-hubs-java-get-started-send.md)

- [Python](event-hubs-python-get-started-send.md)

- [JavaScript](event-hubs-node-get-started-send.md)

- [Go](event-hubs-go-get-started-send.md)

- [C (send only)](event-hubs-c-getstarted-send.md)

- [Apache Storm (receive only)](event-hubs-storm-getstarted-receive.md)

[3]: ./media/event-hubs-quickstart-powershell/sender1.png

[4]: ./media/event-hubs-quickstart-powershell/receiver1.png

[5]: ./media/event-hubs-quickstart-powershell/metrics.png

[Understand the structure and syntax of Bicep files]: ../azure-resource-manager/bicep/file.md

[Deploy resources with Bicep and Azure PowerShell]: ../azure-resource-manager/bicep/deploy-powershell.md

[Deploy resource with Bicep and Azure CLI]: ../azure-resource-manager/bicep/deploy-cli.md


# Event Hubs Resource Manager Namespace Event Hub

# Quickstart: Create an event hub by using an ARM template

In this quickstart, you create an event hub by using an [Azure Resource Manager template (ARM template)](../azure-resource-manager/management/overview.md). You deploy an ARM template to create a namespace of type [Event Hubs](./event-hubs-about.md), with one event hub.

## Prerequisites

- If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

- If you're new to Azure Event Hubs, see [Event Hubs overview](event-hubs-about.md) and [Event Hubs features](event-hubs-features.md).

## Review the template

The template used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/eventhubs-create-namespace-and-eventhub/).

The resources defined in the template include:

- [**Microsoft.EventHub/namespaces**](/azure/templates/microsoft.eventhub/namespaces)

- [**Microsoft.EventHub/namespaces/eventhubs**](/azure/templates/microsoft.eventhub/namespaces/eventhubs)

To find more template samples, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=eventhub&pageNumber=1&sort=Popular).

## Deploy the template

### Using Azure portal user interface

1. If your environment meets the prerequisites and you're familiar with using ARM templates, select the **Deploy to Azure** button. The template opens in the Azure portal.

2. Select an existing **resource group** or create a resource group and select it.

1. Select the **region**.

1. Enter a unique **name** for the **project**. This name is used to generate names for an Event Hubs namespace and an event hub in the namespace.

1. Select **Review + create**.

1. On the **Review + create** page, select **Create**.

### Using Azure Cloud Shell

To deploy the template using Azure Cloud Shell:

1. Select **Open Cloud Shell** from the following code block, and then follow the instructions to sign in to the Azure Cloud Shell.

```azurepowershell-interactive

$projectName = Read-Host -Prompt "Enter a project name that is used for generating resource names"

$location = Read-Host -Prompt "Enter the location (i.e. centralus)"

$resourceGroupName = "${projectName}rg"

$templateUri = "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.eventhub/eventhubs-create-namespace-and-eventhub/azuredeploy.json"

New-AzResourceGroup -Name $resourceGroupName -Location $location

New-AzResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateUri $templateUri -projectName $projectName

Write-Host "Press [ENTER] to continue ..."

```

It takes a few moments to create an event hub.

1. Select **Copy** to copy the PowerShell script.

1. Right-click the shell console, and then select **Paste**.

1. Press **ENTER** to run the commands.

## Validate the deployment

To verify the deployment, you can either open the resource group from the [Azure portal](https://portal.azure.com), or use the following Azure PowerShell script. If the Cloud Shell is still open, you don't need to copy/run the first line (Read-Host).

```azurepowershell-interactive

$projectName = Read-Host -Prompt "Enter the same project name that you used in the last procedure"

$resourceGroupName = "${projectName}rg"

$namespaceName = "${projectName}ns"

Get-AzEventHub -ResourceGroupName $resourceGroupName -Namespace $namespaceName

Write-Host "Press [ENTER] to continue ..."

```

## Clean up resources

When the Azure resources are no longer needed, clean up the resources you deployed by deleting the resource group. If the Cloud Shell is still open, you don't need to copy/run the first line (Read-Host).

```azurepowershell-interactive

$projectName = Read-Host -Prompt "Enter the same project name that you used in the last procedure"

$resourceGroupName = "${projectName}rg"

Remove-AzResourceGroup -ResourceGroupName $resourceGroupName

Write-Host "Press [ENTER] to continue ..."

```

## Next steps

In this article, you created an Event Hubs namespace, and an event hub in the namespace. For step-by-step instructions to send events to (or) receive events from an event hub, see the **Send and receive events** tutorials:

- [.NET Core](event-hubs-dotnet-standard-getstarted-send.md)

- [Java](event-hubs-java-get-started-send.md)

- [Python](event-hubs-python-get-started-send.md)

- [JavaScript](event-hubs-node-get-started-send.md)

- [Go](event-hubs-go-get-started-send.md)

- [C (send only)](event-hubs-c-getstarted-send.md)

- [Apache Storm (receive only)](event-hubs-storm-getstarted-receive.md)

[3]: ./media/event-hubs-quickstart-powershell/sender1.png

[4]: ./media/event-hubs-quickstart-powershell/receiver1.png

[5]: ./media/event-hubs-quickstart-powershell/metrics.png

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/templates/syntax.md

[Azure Quickstart Templates]:  https://azure.microsoft.com/resources/templates/?term=event+hubs

[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/management/manage-resources-powershell.md

[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/management/manage-resources-cli.md

[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/quickstarts/microsoft.eventhub/event-hubs-create-event-hub-and-consumer-group/


# Event Hubs Dotnet Standard Getstarted Send

# Quickstart: Send events to and receive events from Azure Event Hubs using .NET

Azure Event Hubs is a real-time data streaming platform that can receive and process millions of events per second. If you're building .NET applications that need to ingest or react to high-volume event streams, Event Hubs provides the scalable infrastructure to do it.

In this quickstart, you create a .NET console application that sends events to an event hub and receives them using the **Azure.Messaging.EventHubs** library. By the end, you'll have working code you can adapt for your own event-driven scenarios.

## Prerequisites

If you're new to Azure Event Hubs, see [Event Hubs overview](event-hubs-about.md) before you complete this quickstart.

> [!NOTE]

> If you're already familiar with the service, you can see .NET samples for Event Hubs in our .NET SDK repository on GitHub: [Event Hubs samples on GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/eventhub/Azure.Messaging.EventHubs/samples), [Event processor samples on GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/eventhub/Azure.Messaging.EventHubs.Processor/samples).

To complete this quickstart, you need:

- **Microsoft Azure subscription**. To use Azure services, including Event Hubs, you need a subscription. If you don't have an existing Azure account, you can sign up for a [free trial](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- **Microsoft Visual Studio 2022**. The Azure Event Hubs client library uses new features that were introduced in C# 8.0. You can still use the library with previous C# language versions, but the new syntax isn't available. To use the full syntax, we recommend that you compile with the [.NET Core SDK](https://dotnet.microsoft.com/download) 3.0 or higher and [language version](/dotnet/csharp/language-reference/configure-language-version#override-a-default) set to `latest`. If you're using Visual Studio, versions before Visual Studio 2022 aren't compatible with the tools needed to build C# 8.0 projects. Visual Studio 2022, including the free Community edition, can be downloaded [here](https://visualstudio.microsoft.com/vs/).

- **Create an Event Hubs namespace and an event hub**. Use the Azure portal to create an Event Hubs namespace and an event hub in the namespace. Then, get the management credentials that your application needs to communicate with the event hub. To create a namespace and an event hub, see [Quickstart: Create an event hub using Azure portal](event-hubs-create.md).

### Authenticate the app to Azure

[!INCLUDE [event-hub-passwordless-template-tabbed](../../includes/passwordless/event-hub/event-hub-passwordless-template-tabbed.md)]

## Send events to the event hub

This section shows you how to create a .NET Core console application to send events to the event hub you created.

### Create a console application

1. If Visual Studio 2022 is already open, select **File** on the menu, select **New**, and then select **Project**. Otherwise, launch Visual Studio 2022 and select **Create a new project** if you see a popup window.

1. In the **Create a new project** dialog box, complete the following steps: If you don't see this dialog box, select **File** on the menu, select **New**, and then select **Project**.

1. Select **C#** for the programming language.

1. Select **Console** for the type of the application.

1. Select **Console Application** from the results list.

1. Select **Next**.

1. Enter **EventHubsSender** for the project name, **EventHubsQuickStart** for the solution name, and then select **Next**.

1. On the **Additional information** page, select **Create**.

### Add the NuGet packages to the project

### [Passwordless (Recommended)](#tab/passwordless)

1. Select **Tools** > **NuGet Package Manager** > **Package Manager Console** from the menu.

1. Run the following commands to install the **Azure.Messaging.EventHubs** and **Azure.Identity** NuGet packages. Press **ENTER** to run the second command.

```powershell

Install-Package Azure.Messaging.EventHubs

Install-Package Azure.Identity

```

### [Connection String](#tab/connection-string)

1. Select **Tools** > **NuGet Package Manager** > **Package Manager Console** from the menu.

1. Run the following command to install the **Azure.Messaging.EventHubs** NuGet package:

```powershell

Install-Package Azure.Messaging.EventHubs

```

---

### Write code to send events to the event hub

## [Passwordless (Recommended)](#tab/passwordless)

1. Replace the existing code in the `Program.cs` file with the following sample code. Then, replace `<EVENT_HUB_NAMESPACE>` and `<HUB_NAME>` placeholder values for the `EventHubProducerClient` parameters with the names of your Event Hubs namespace and the event hub. For example: `"spehubns0309.servicebus.windows.net"` and `"spehub"`.

Here are the important steps from the code:

1. Creates an [EventHubProducerClient](/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient) object using the namespace and the event hub name.

1. Invokes the [CreateBatchAsync](/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient.createbatchasync) method on the [EventHubProducerClient](/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient) object to create an [EventDataBatch](/dotnet/api/azure.messaging.eventhubs.producer.eventdatabatch) object.

1. Adds events to the batch using the [EventDataBatch.TryAdd](/dotnet/api/azure.messaging.eventhubs.producer.eventdatabatch.tryadd) method.

1. Sends the batch of events to the event hub using the [EventHubProducerClient.SendAsync](/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient.sendasync) method.

```csharp

using Azure.Identity;

using Azure.Messaging.EventHubs;

using Azure.Messaging.EventHubs.Producer;

using System.Text;

// number of events to be sent to the event hub

int numOfEvents = 3;

// The Event Hubs client types are safe to cache and use as a singleton for the lifetime

// of the application, which is best practice when events are being published or read regularly.

// TODO: Replace the <EVENT_HUB_NAMESPACE> and <HUB_NAME> placeholder values

EventHubProducerClient producerClient = new EventHubProducerClient(

"<EVENT_HUB_NAMESPACE>.servicebus.windows.net",

"<HUB_NAME>",

new DefaultAzureCredential());

// Create a batch of events

using EventDataBatch eventBatch = await producerClient.CreateBatchAsync();

for (int i = 1; i <= numOfEvents; i++)

{

if (!eventBatch.TryAdd(new EventData(Encoding.UTF8.GetBytes($"Event {i}"))))

{

// if it is too large for the batch

throw new Exception($"Event {i} is too large for the batch and cannot be sent.");

}

}

try

{

// Use the producer client to send the batch of events to the event hub

await producerClient.SendAsync(eventBatch);

Console.WriteLine($"A batch of {numOfEvents} events has been published.");

Console.ReadLine();

}

finally

{

await producerClient.DisposeAsync();

}

```

## [Connection String](#tab/connection-string)

1. Replace the existing code in the `Program.cs` file with the following sample code. Then, replace the `<CONNECTION_STRING>` and `<HUB_NAME>` placeholder values for the `EventHubProducerClient` parameters.

Here are the important steps from the code:

1. Creates an [EventHubProducerClient](/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient) object using the primary connection string to the namespace and the event hub name.

1. Invokes the [CreateBatchAsync](/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient.createbatchasync) method on the [EventHubProducerClient](/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient) object to create an [EventDataBatch](/dotnet/api/azure.messaging.eventhubs.producer.eventdatabatch) object.

1. Adds events to the batch using the [EventDataBatch.TryAdd](/dotnet/api/azure.messaging.eventhubs.producer.eventdatabatch.tryadd) method.

1. Sends the batch of events to the event hub using the [EventHubProducerClient.SendAsync](/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient.sendasync) method.

```csharp

using Azure.Messaging.EventHubs;

using Azure.Messaging.EventHubs.Producer;

using System.Text;

// number of events to be sent to the event hub

int numOfEvents = 3;

// The Event Hubs client types are safe to cache and use as a singleton for the lifetime

// of the application, which is best practice when events are being published or read regularly.

// TODO: Replace the <CONNECTION_STRING> and <HUB_NAME> placeholder values

EventHubProducerClient producerClient = new EventHubProducerClient(

"<CONNECTION_STRING>",

"<HUB_NAME>");

// Create a batch of events

using EventDataBatch eventBatch = await producerClient.CreateBatchAsync();

for (int i = 1; i <= numOfEvents; i++)

{

if (!eventBatch.TryAdd(new EventData(Encoding.UTF8.GetBytes($"Event {i}"))))

{

// if it is too large for the batch

throw new Exception($"Event {i} is too large for the batch and cannot be sent.");

}

}

try

{

// Use the producer client to send the batch of events to the event hub

await producerClient.SendAsync(eventBatch);

Console.WriteLine($"A batch of {numOfEvents} events has been published.");

Console.ReadLine();

}

finally

{

await producerClient.DisposeAsync();

}

```

---

2. Build the project, and ensure that there are no errors.

3. Run the program and wait for the confirmation message.

```csharp

A batch of 3 events has been published.

```

> [!NOTE]

> If you get an error "InvalidIssuer: Token issuer is invalid" when using Microsoft Entra authentication, it might be because the wrong Microsoft Entra Tenant ID is being used. In your code, replace 'new DefaultAzureCredential()' with 'new DefaultAzureCredential(new DefaultAzureCredentialOptions {TenantId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"})' to explicitly specify Microsoft Entra Tenant ID.

> [!IMPORTANT]

> If you're using the Passwordless (Microsoft Entra role-based access control) authentication, select **Tools**, then select **Options**. In the **Options** window, expand **Azure Service Authentication**, and select **Account Selection**. Confirm that you're using the account that was added to the **Azure Event Hubs Data Owner** role on the Event Hubs namespace.

4. On the **Event Hubs namespace** page in the Azure portal, you see three incoming messages in the **Messages** chart. Refresh the page to update the chart if needed. It might take a few seconds for it to show that the messages are received.

> [!NOTE]

> For the complete source code with more informational comments, see [this file on GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/eventhub/Azure.Messaging.EventHubs/samples/Sample04_PublishingEvents.md)

## Receive events from the event hub

This section shows how to write a .NET Core console application that receives events from an event hub using an event processor. The event processor simplifies receiving events from event hubs.

### Create an Azure Storage account and a blob container

In this quickstart, you use Azure Storage as the checkpoint store. Use the following steps to create an Azure Storage account:

1. [Create an Azure Storage account](../storage/common/storage-account-create.md?tabs=azure-portal)

1. [Create a blob container](../storage/blobs/storage-quickstart-blobs-portal.md#create-a-container)

1. Authenticate to the blob container by using either Microsoft Entra ID (passwordless) authentication or a connection string to the namespace.

[!INCLUDE [storage-checkpoint-store-recommendations](./includes/storage-checkpoint-store-recommendations.md)]

## [Passwordless (Recommended)](#tab/passwordless)

[!INCLUDE [event-hub-storage-assign-roles](../../includes/passwordless/event-hub/event-hub-storage-assign-roles.md)]

## [Connection String](#tab/connection-string)

[Get the connection string for the storage account](../storage/common/storage-account-get-info.md#get-a-connection-string-for-the-storage-account)

Record the connection string and the container name. Use them in the code to receive events from the event hub.

---

### Create a project for the receiver

1. In the Solution Explorer window, right-click the **EventHubQuickStart** solution, point to **Add**, and select **New Project**.

1. Select **Console application**, and select **Next**.

1. Enter **EventHubsReceiver** for the **Project name**, and select **Create**.

1. In the **Solution Explorer** window, right-click **EventHubsReceiver**, and select **Set as a Startup Project**.

### Add the NuGet packages to the project

### [Passwordless (Recommended)](#tab/passwordless)

1. Select **Tools** > **NuGet Package Manager** > **Package Manager Console** from the menu.

1. In the **Package Manager Console** window, confirm that **EventHubsReceiver** is selected for the **Default project**. If not, use the drop-down list to select **EventHubsReceiver**.

1. Run the following command to install the **Azure.Messaging.EventHubs** and **Azure.Identity** NuGet packages. Press **ENTER** to run the last command.

```powershell

Install-Package Azure.Messaging.EventHubs

Install-Package Azure.Messaging.EventHubs.Processor

Install-Package Azure.Identity

```

### [Connection String](#tab/connection-string)

1. Select **Tools** > **NuGet Package Manager** > **Package Manager Console** from the menu.

1. In the **Package Manager Console** window, confirm that **EventHubsReceiver** is selected for the **Default project**. If not, use the drop-down list to select **EventHubsReceiver**.

1. Run the following command to install the **Azure.Messaging.EventHubs** NuGet package:

```powershell

Install-Package Azure.Messaging.EventHubs

Install-Package Azure.Messaging.EventHubs.Processor

```

---

### Update the code

Replace the contents of **Program.cs** with the following code:

## [Passwordless (Recommended)](#tab/passwordless)

1. Replace the existing code in the `Program.cs` file with the following sample code. Then, replace the `<STORAGE_ACCOUNT_NAME>` and `<BLOB_CONTAINER_NAME>` placeholder values for the `BlobContainerClient` URI. Replace the `<EVENT_HUB_NAMESPACE>` and `<HUB_NAME>` placeholder values for the `EventProcessorClient` as well.

Here are the important steps from the code:

1. Creates an [EventProcessorClient](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient) object using the Event Hubs namespace and the event hub name. You need to build [BlobContainerClient](/dotnet/api/azure.storage.blobs.blobcontainerclient) object for the container in the Azure storage you created earlier.

1. Specifies handlers for the [ProcessEventAsync](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient.processeventasync) and [ProcessErrorAsync](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient.processerrorasync) events of the [EventProcessorClient](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient) object.

1. Starts processing events by invoking the [StartProcessingAsync](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient.startprocessingasync) on the [EventProcessorClient](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient) object.

1. Stops processing events after 30 seconds by invoking [StopProcessingAsync](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient.stopprocessingasync) on the [EventProcessorClient](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient) object.

```csharp

using Azure.Identity;

using Azure.Messaging.EventHubs;

using Azure.Messaging.EventHubs.Consumer;

using Azure.Messaging.EventHubs.Processor;

using Azure.Storage.Blobs;

using System.Text;

// Create a blob container client that the event processor will use

// TODO: Replace <STORAGE_ACCOUNT_NAME> and <BLOB_CONTAINER_NAME> with actual names

BlobContainerClient storageClient = new BlobContainerClient(

new Uri("https://<STORAGE_ACCOUNT_NAME>.blob.core.windows.net/<BLOB_CONTAINER_NAME>"),

new DefaultAzureCredential());

// Create an event processor client to process events in the event hub

// TODO: Replace the <EVENT_HUBS_NAMESPACE> and <HUB_NAME> placeholder values

var processor = new EventProcessorClient(

storageClient,

EventHubConsumerClient.DefaultConsumerGroupName,

"<EVENT_HUB_NAMESPACE>.servicebus.windows.net",

"<HUB_NAME>",

new DefaultAzureCredential());

// Register handlers for processing events and handling errors

processor.ProcessEventAsync += ProcessEventHandler;

processor.ProcessErrorAsync += ProcessErrorHandler;

// Start the processing

await processor.StartProcessingAsync();

// Wait for 30 seconds for the events to be processed

await Task.Delay(TimeSpan.FromSeconds(30));

// Stop the processing

await processor.StopProcessingAsync();

Task ProcessEventHandler(ProcessEventArgs eventArgs)

{

// Write the body of the event to the console window

Console.WriteLine("\tReceived event: {0}", Encoding.UTF8.GetString(eventArgs.Data.Body.ToArray()));

Console.ReadLine();

return Task.CompletedTask;

}

Task ProcessErrorHandler(ProcessErrorEventArgs eventArgs)

{

// Write details about the error to the console window

Console.WriteLine($"\tPartition '{eventArgs.PartitionId}': an unhandled exception was encountered. This was not expected to happen.");

Console.WriteLine(eventArgs.Exception.Message);

Console.ReadLine();

return Task.CompletedTask;

}

```

## [Connection String](#tab/connection-string)

1. Replace the existing code in the `Program.cs` file with the following sample code. Then, replace the `<AZURE_STORAGE_CONNECTION_STRING>` and `<BLOB_CONTAINER_NAME>` placeholder values for the `BlobContainerClient` URI. Replace the `<EVENT_HUB_NAMESPACE_CONNECTION_STRING>` and `<HUB_NAME>` placeholder values for the `EventProcessorClient` as well.

Here are the important steps from the code:

1. Creates an [EventProcessorClient](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient) object using the primary connection string to the namespace and the event hub. You need to build [BlobContainerClient](/dotnet/api/azure.storage.blobs.blobcontainerclient) object for the container in the Azure storage you created earlier.

1. Specifies handlers for the [ProcessEventAsync](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient.processeventasync) and [ProcessErrorAsync](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient.processerrorasync) events of the [EventProcessorClient](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient) object.

1. Starts processing events by invoking the [StartProcessingAsync](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient.startprocessingasync) on the [EventProcessorClient](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient) object.

1. Stops processing events after 30 seconds by invoking [StopProcessingAsync](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient.stopprocessingasync) on the [EventProcessorClient](/dotnet/api/azure.messaging.eventhubs.eventprocessorclient) object.

```csharp

using Azure.Messaging.EventHubs;

using Azure.Messaging.EventHubs.Consumer;

using Azure.Messaging.EventHubs.Processor;

using Azure.Storage.Blobs;

using System.Text;

// Create a blob container client that the event processor will use

BlobContainerClient storageClient = new BlobContainerClient(

"<AZURE_STORAGE_CONNECTION_STRING>", "<BLOB_CONTAINER_NAME>");

// Create an event processor client to process events in the event hub

var processor = new EventProcessorClient(

storageClient,

EventHubConsumerClient.DefaultConsumerGroupName,

"<EVENT_HUBS_NAMESPACE_CONNECTION_STRING>",

"<HUB_NAME>");

// Register handlers for processing events and handling errors

processor.ProcessEventAsync += ProcessEventHandler;

processor.ProcessErrorAsync += ProcessErrorHandler;

// Start the processing

await processor.StartProcessingAsync();

// Wait for 30 seconds for the events to be processed

await Task.Delay(TimeSpan.FromSeconds(30));

// Stop the processing

await processor.StopProcessingAsync();

Task ProcessEventHandler(ProcessEventArgs eventArgs)

{

// Write the body of the event to the console window

Console.WriteLine("\tReceived event: {0}", Encoding.UTF8.GetString(eventArgs.Data.Body.ToArray()));

return Task.CompletedTask;

}

Task ProcessErrorHandler(ProcessErrorEventArgs eventArgs)

{

// Write details about the error to the console window

Console.WriteLine($"\tPartition '{eventArgs.PartitionId}': an unhandled exception was encountered. This was not expected to happen.");

Console.WriteLine(eventArgs.Exception.Message);

return Task.CompletedTask;

}

```

---

2. Build the project, and ensure that there are no errors.

> [!NOTE]

> For the complete source code with more informational comments, see [this file on GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/eventhub/Azure.Messaging.EventHubs.Processor/samples/Sample01_HelloWorld.md).

3. Run the receiver application.

4. You see a message that the events are received. Press ENTER after you see a received event message.

```bash

Received event: Event 1

Received event: Event 2

Received event: Event 3

```

These events are the three events you sent to the event hub earlier by running the sender program.

5. In the Azure portal, you can verify that there are three outgoing messages, which Event Hubs sent to the receiving application. Refresh the page to update the chart. It might take a few seconds for it to show that the messages are received.

## Schema validation for Event Hubs SDK-based applications

You can use Azure Schema Registry to perform schema validation when you stream data with your Event Hubs SDK-based applications.

Azure Schema Registry of Event Hubs provides a centralized repository for managing schemas, and you can seamlessly connect your new or existing applications with Schema Registry.

To learn more, see [Validate schemas with Event Hubs SDK](schema-registry-dotnet-send-receive-quickstart.md).

## Samples and reference

This quickstart provides step-by-step instructions to implement a scenario of sending a batch of events to an event hub and then receiving them. For more samples, select the following links.

- [Event Hubs samples on GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/eventhub/Azure.Messaging.EventHubs/samples)

- [Event processor samples on GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/eventhub/Azure.Messaging.EventHubs.Processor/samples)

- [Azure role-based access control (Azure RBAC) sample](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Azure.Messaging.EventHubs/ManagedIdentityWebApp)

For complete .NET library reference, see our [SDK documentation](/dotnet/api/overview/azure/event-hubs).

## Clean up resources

Delete the resource group that has the Event Hubs namespace or delete only the namespace if you want to keep the resource group.

## Related content

See the following tutorial:

> [!div class="nextstepaction"]

> [Tutorial: Visualize data anomalies in real-time events sent to Azure Event Hubs](../stream-analytics/stream-analytics-real-time-fraud-detection.md?toc=%2Fazure%2Fevent-hubs%2FTOC.json)


# Event Hubs Java Get Started Send

# Quickstart: Send events to or receive events from Azure Event Hubs

In this Quickstart, you learn how to send events to and receive events from an Azure event hub using the **azure-messaging-eventhubs** Java package.

> [!TIP]

> If you're working with Azure Event Hubs resources in a Spring application, we recommend that you consider [Spring Cloud Azure](/azure/developer/java/spring-framework/) as an alternative. Spring Cloud Azure is an open-source project that provides seamless Spring integration with Azure services. To learn more about Spring Cloud Azure, and to see an example using Event Hubs, see [Spring Cloud Stream with Azure Event Hubs](/azure/developer/java/spring-framework/configure-spring-cloud-stream-binder-java-app-azure-event-hub).

## Prerequisites

If you're new to Azure Event Hubs, see [Event Hubs overview](event-hubs-about.md) before you do this quickstart.

To complete this quickstart, you need the following prerequisites:

- **Microsoft Azure subscription**. To use Azure services, including Azure Event Hubs, you need a subscription. If you don't have an existing Azure account, you can sign up for a [free trial](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) or use your MSDN subscriber benefits when you [create an account](https://azure.microsoft.com).

- A Java development environment. This quickstart uses [Eclipse](https://www.eclipse.org/). Java Development Kit (JDK) with version 8 or above is required.

- **Create an Event Hubs namespace and an event hub**. The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub. To create a namespace and an event hub, follow the procedure in [this article](event-hubs-create.md). Then, get the **connection string for the Event Hubs namespace** by following instructions from the article: [Get connection string](event-hubs-get-connection-string.md#azure-portal). You use the connection string later in this quickstart.

## Send events

This section shows you how to create a Java application to send events an event hub.

### Add reference to Azure Event Hubs library

First, create a new **Maven** project for a console/shell application in your favorite Java development environment. Update the `pom.xml` file as follows. The Java client library for Event Hubs is available in the [Maven Central Repository](https://central.sonatype.com/artifact/com.azure/azure-messaging-eventhubs).

### [Passwordless (Recommended)](#tab/passwordless)

```xml

<dependency>

<groupId>com.azure</groupId>

<artifactId>azure-messaging-eventhubs</artifactId>

<version>5.20.2</version>

</dependency>

<dependency>

<groupId>com.azure</groupId>

<artifactId>azure-identity</artifactId>

<version>1.16.1</version>

<scope>compile</scope>

</dependency>

```

### [Connection String](#tab/connection-string)

```xml

<dependency>

<groupId>com.azure</groupId>

<artifactId>azure-messaging-eventhubs</artifactId>

<version>5.20.2</version>

</dependency>

```

---

> [!NOTE]

> Update the version to the latest version published to the Maven repository.

### Authenticate the app to Azure

[!INCLUDE [event-hub-passwordless-template-tabbed-basic](../../includes/passwordless/event-hub/event-hub-passwordless-template-tabbed-basic.md)]

### Write code to send messages to the event hub

## [Passwordless (Recommended)](#tab/passwordless)

Add a class named `Sender`, and add the following code to the class:

> [!IMPORTANT]

> - Update `<NAMESPACE NAME>` with the name of your Event Hubs namespace.

> - Update `<EVENT HUB NAME>` with the name of your event hub.

```java

package ehubquickstart;

import com.azure.messaging.eventhubs.*;

import java.util.Arrays;

import java.util.List;

import com.azure.identity.*;

public class SenderAAD {

// replace <NAMESPACE NAME> with the name of your Event Hubs namespace.

// Example: private static final String namespaceName = "contosons.servicebus.windows.net";

private static final String namespaceName = "<NAMESPACE NAME>.servicebus.windows.net";

// Replace <EVENT HUB NAME> with the name of your event hub.

// Example: private static final String eventHubName = "ordersehub";

private static final String eventHubName = "<EVENT HUB NAME>";

public static void main(String[] args) {

publishEvents();

}

/**

* Code sample for publishing events.

* @throws IllegalArgumentException if the EventData is bigger than the max batch size.

*/

public static void publishEvents() {

// create a token using the default Azure credential

DefaultAzureCredential credential = new DefaultAzureCredentialBuilder()

.authorityHost(AzureAuthorityHosts.AZURE_PUBLIC_CLOUD)

.build();

// create a producer client

EventHubProducerClient producer = new EventHubClientBuilder()

.fullyQualifiedNamespace(namespaceName)

.eventHubName(eventHubName)

.credential(credential)

.buildProducerClient();

// sample events in an array

List<EventData> allEvents = Arrays.asList(new EventData("Foo"), new EventData("Bar"));

// create a batch

EventDataBatch eventDataBatch = producer.createBatch();

for (EventData eventData : allEvents) {

// try to add the event from the array to the batch

if (!eventDataBatch.tryAdd(eventData)) {

// if the batch is full, send it and then create a new batch

producer.send(eventDataBatch);

eventDataBatch = producer.createBatch();

// Try to add that event that couldn't fit before.

if (!eventDataBatch.tryAdd(eventData)) {

throw new IllegalArgumentException("Event is too large for an empty batch. Max size: "

+ eventDataBatch.getMaxSizeInBytes());

}

}

}

// send the last batch of remaining events

if (eventDataBatch.getCount() > 0) {

producer.send(eventDataBatch);

}

producer.close();

}

}

```

## [Connection String](#tab/connection-string)

Add a class named `Sender`, and add the following code to the class:

> [!IMPORTANT]

> Update `<Event Hubs namespace connection string>` with the connection string to your Event Hubs namespace. Update `<Event hub name>` with the name of your event hub in the namespace.

```java

import com.azure.messaging.eventhubs.*;

import java.util.Arrays;

import java.util.List;

public class Sender {

private static final String connectionString = "<Event Hubs namespace connection string>";

private static final String eventHubName = "<Event hub name>";

public static void main(String[] args) {

publishEvents();

}

}

```

### Add code to publish events to the event hub

Add a method named `publishEvents` to the `Sender` class:

```java

/**

* Code sample for publishing events.

* @throws IllegalArgumentException if the EventData is bigger than the max batch size.

*/

public static void publishEvents() {

// create a producer client

EventHubProducerClient producer = new EventHubClientBuilder()

.connectionString(connectionString, eventHubName)

.buildProducerClient();

// sample events in an array

List<EventData> allEvents = Arrays.asList(new EventData("Foo"), new EventData("Bar"));

// create a batch

EventDataBatch eventDataBatch = producer.createBatch();

for (EventData eventData : allEvents) {

// try to add the event from the array to the batch

if (!eventDataBatch.tryAdd(eventData)) {

// if the batch is full, send it and then create a new batch

producer.send(eventDataBatch);

eventDataBatch = producer.createBatch();

// Try to add that event that couldn't fit before.

if (!eventDataBatch.tryAdd(eventData)) {

throw new IllegalArgumentException("Event is too large for an empty batch. Max size: "

+ eventDataBatch.getMaxSizeInBytes());

}

}

}

// send the last batch of remaining events

if (eventDataBatch.getCount() > 0) {

producer.send(eventDataBatch);

}

producer.close();

}

```

---

Build the program, and ensure that there are no errors. You'll run this program after you run the receiver program.

## Receive events

The code in this tutorial is based on the [EventProcessorClient sample on GitHub](https://github.com/Azure/azure-sdk-for-java/blob/master/sdk/eventhubs/azure-messaging-eventhubs-checkpointstore-blob/src/samples/java/com/azure/messaging/eventhubs/checkpointstore/blob/EventProcessorBlobCheckpointStoreSample.java), which you can examine to see the full working application.

[!INCLUDE [storage-checkpoint-store-recommendations](./includes/storage-checkpoint-store-recommendations.md)]

### Create an Azure Storage and a blob container

In this quickstart, you use Azure Storage (specifically, Blob Storage) as the checkpoint store. Checkpointing is a process by which an event processor marks or commits the position of the last successfully processed event within a partition. Marking a checkpoint is typically done within the function that processes the events. To learn more about checkpointing, see [Event processor](event-processor-balance-partition-load.md).

Follow these steps to create an Azure Storage account.

1. [Create an Azure Storage account](../storage/common/storage-account-create.md?tabs=azure-portal)

2. [Create a blob container](../storage/blobs/storage-quickstart-blobs-portal.md#create-a-container)

3. Authenticate to the blob container

## [Passwordless (Recommended)](#tab/passwordless)

[!INCLUDE [event-hub-storage-assign-roles](../../includes/passwordless/event-hub/event-hub-storage-assign-roles.md)]

## [Connection String](#tab/connection-string)

[Get the connection string to the storage account](../storage/common/storage-configure-connection-string.md).

Note down the **connection string** and the **container name**. You use them in the receive code.

---

### Add Event Hubs libraries to your Java project

## [Passwordless (Recommended)](#tab/passwordless)

Add the following dependencies in the pom.xml file.

- [azure-messaging-eventhubs](https://central.sonatype.com/artifact/com.azure/azure-messaging-eventhubs)

- [azure-messaging-eventhubs-checkpointstore-blob](https://central.sonatype.com/artifact/com.azure/azure-messaging-eventhubs-checkpointstore-blob)

- [azure-identity](https://central.sonatype.com/artifact/com.azure/azure-identity)

```xml

<dependencies>

<dependency>

<groupId>com.azure</groupId>

<artifactId>azure-messaging-eventhubs</artifactId>

<version>5.20.2</version>

</dependency>

<dependency>

<groupId>com.azure</groupId>

<artifactId>azure-messaging-eventhubs-checkpointstore-blob</artifactId>

<version>1.20.6</version>

</dependency>

<dependency>

<groupId>com.azure</groupId>

<artifactId>azure-identity</artifactId>

<version>1.16.1</version>

<scope>compile</scope>

</dependency>

</dependencies>

```

### [Connection String](#tab/connection-string)

Add the following dependencies in the pom.xml file.

- [azure-messaging-eventhubs](https://central.sonatype.com/artifact/com.azure/azure-messaging-eventhubs)

- [azure-messaging-eventhubs-checkpointstore-blob](https://central.sonatype.com/artifact/com.azure/azure-messaging-eventhubs-checkpointstore-blob)

```xml

<dependencies>

<dependency>

<groupId>com.azure</groupId>

<artifactId>azure-messaging-eventhubs</artifactId>

<version>5.20.2</version>

</dependency>

<dependency>

<groupId>com.azure</groupId>

<artifactId>azure-messaging-eventhubs-checkpointstore-blob</artifactId>

<version>1.20.6</version>

</dependency>

</dependencies>

```

---

## [Passwordless (Recommended)](#tab/passwordless)

1. Add the following `import` statements at the top of the Java file.

```java

import com.azure.messaging.eventhubs.*;

import com.azure.messaging.eventhubs.checkpointstore.blob.BlobCheckpointStore;

import com.azure.messaging.eventhubs.models.*;

import com.azure.storage.blob.*;

import java.util.function.Consumer;

import com.azure.identity.*;

```

2. Create a class named `Receiver`, and add the following string variables to the class. Replace the placeholders with the correct values.

> [!IMPORTANT]

> Replace the placeholders with the correct values.

> - `<NAMESPACE NAME>` with the name of your Event Hubs namespace.

> - `<EVENT HUB NAME>` with the name of your event hub in the namespace.

```java

private static final String namespaceName = "<NAMESPACE NAME>.servicebus.windows.net";

private static final String eventHubName = "<EVENT HUB NAME>";

```

3. Add the following `main` method to the class.

> [!IMPORTANT]

> Replace the placeholders with the correct values.

> - `<STORAGE ACCOUNT NAME>` with the name of your Azure Storage account.

> - `<CONTAINER NAME>` with the name of the blob container in the storage account

```java

// create a token using the default Azure credential

DefaultAzureCredential credential = new DefaultAzureCredentialBuilder()

.authorityHost(AzureAuthorityHosts.AZURE_PUBLIC_CLOUD)

.build();

// Create a blob container client that you use later to build an event processor client to receive and process events

BlobContainerAsyncClient blobContainerAsyncClient = new BlobContainerClientBuilder()

.credential(credential)

.endpoint("https://<STORAGE ACCOUNT NAME>.blob.core.windows.net")

.containerName("<CONTAINER NAME>")

.buildAsyncClient();

// Create an event processor client to receive and process events and errors.

EventProcessorClient eventProcessorClient = new EventProcessorClientBuilder()

.fullyQualifiedNamespace(namespaceName)

.eventHubName(eventHubName)

.consumerGroup(EventHubClientBuilder.DEFAULT_CONSUMER_GROUP_NAME)

.processEvent(PARTITION_PROCESSOR)

.processError(ERROR_HANDLER)

.checkpointStore(new BlobCheckpointStore(blobContainerAsyncClient))

.credential(credential)

.buildEventProcessorClient();

System.out.println("Starting event processor");

eventProcessorClient.start();

System.out.println("Press enter to stop.");

System.in.read();

System.out.println("Stopping event processor");

eventProcessorClient.stop();

System.out.println("Event processor stopped.");

System.out.println("Exiting process");

```

## [Connection String](#tab/connection-string)

1. Add the following **import** statements at the top of the Java file.

```java

import com.azure.messaging.eventhubs.*;

import com.azure.messaging.eventhubs.checkpointstore.blob.BlobCheckpointStore;

import com.azure.messaging.eventhubs.models.*;

import com.azure.storage.blob.*;

import java.util.function.Consumer;

```

2. Create a class named `Receiver`, and add the following string variables to the class. Replace the placeholders with the correct values.

> [!IMPORTANT]

> Replace the placeholders with the correct values.

> - `<Event Hubs namespace connection string>` with the connection string to your Event Hubs namespace. Update

> - `<Event hub name>` with the name of your event hub in the namespace.

> - `<Storage connection string>` with the connection string to your Azure storage account.

> - `<Storage container name>` with the name of your container in your Azure Blob storage.

```java

private static final String connectionString = "<Event Hubs namespace connection string>";

private static final String eventHubName = "<Event hub name>";

private static final String storageConnectionString = "<Storage connection string>";

private static final String storageContainerName = "<Storage container name>";

```

3. Add the following `main` method to the class.

```java

public static void main(String[] args) throws Exception {

// Create a blob container client that you use later to build an event processor client to receive and process events

BlobContainerAsyncClient blobContainerAsyncClient = new BlobContainerClientBuilder()

.connectionString(storageConnectionString)

.containerName(storageContainerName)

.buildAsyncClient();

// Create a builder object that you will use later to build an event processor client to receive and process events and errors.

EventProcessorClientBuilder eventProcessorClientBuilder = new EventProcessorClientBuilder()

.connectionString(connectionString, eventHubName)

.consumerGroup(EventHubClientBuilder.DEFAULT_CONSUMER_GROUP_NAME)

.processEvent(PARTITION_PROCESSOR)

.processError(ERROR_HANDLER)

.checkpointStore(new BlobCheckpointStore(blobContainerAsyncClient));

// Use the builder object to create an event processor client

EventProcessorClient eventProcessorClient = eventProcessorClientBuilder.buildEventProcessorClient();

System.out.println("Starting event processor");

eventProcessorClient.start();

System.out.println("Press enter to stop.");

System.in.read();

System.out.println("Stopping event processor");

eventProcessorClient.stop();

System.out.println("Event processor stopped.");

System.out.println("Exiting process");

}

```

---

4. Add the two helper methods (`PARTITION_PROCESSOR` and `ERROR_HANDLER`) that process events and errors to the `Receiver` class.

```java

public static final Consumer<EventContext> PARTITION_PROCESSOR = eventContext -> {

PartitionContext partitionContext = eventContext.getPartitionContext();

EventData eventData = eventContext.getEventData();

System.out.printf("Processing event from partition %s with sequence number %d with body: %s%n",

partitionContext.getPartitionId(), eventData.getSequenceNumber(), eventData.getBodyAsString());

// Every 10 events received, it will update the checkpoint stored in Azure Blob Storage.

if (eventData.getSequenceNumber() % 10 == 0) {

eventContext.updateCheckpoint();

}

};

public static final Consumer<ErrorContext> ERROR_HANDLER = errorContext -> {

System.out.printf("Error occurred in partition processor for partition %s, %s.%n",

errorContext.getPartitionContext().getPartitionId(),

errorContext.getThrowable());

};

```

5. Build the program, and ensure that there are no errors.

## Run the applications

1. Run the **Receiver** application first.

1. Then, run the **Sender** application.

1. In the **Receiver** application window, confirm that you see the events that were published by the Sender application.

```cmd

Starting event processor

Press enter to stop.

Processing event from partition 0 with sequence number 331 with body: Foo

Processing event from partition 0 with sequence number 332 with body: Bar

```

1. Press **ENTER** in the receiver application window to stop the application.

```cmd

Starting event processor

Press enter to stop.

Processing event from partition 0 with sequence number 331 with body: Foo

Processing event from partition 0 with sequence number 332 with body: Bar

Stopping event processor

Event processor stopped.

Exiting process

```

## Related content

See the following samples on GitHub:

- [azure-messaging-eventhubs samples](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/eventhubs/azure-messaging-eventhubs/src/samples/java/com/azure/messaging/eventhubs)

- [azure-messaging-eventhubs-checkpointstore-blob samples](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/eventhubs/azure-messaging-eventhubs-checkpointstore-blob/src/samples/java/com/azure/messaging/eventhubs/checkpointstore/blob).


# Event Hubs Python Get Started Send

# Quickstart: Send events to or receive events from event hubs by using Python

In this Quickstart, you learn how to send events to and receive events from an event hub using the **azure-eventhub** Python package.

## Prerequisites

If you're new to Azure Event Hubs, see [Event Hubs overview](event-hubs-about.md) before you do this quickstart.

To complete this quickstart, ensure you have the following prerequisites:

- **Microsoft Azure subscription**: Sign up for a [free trial](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) if you don't have one.

- **Python 3.8 or later**: Ensure pip is installed and updated.

- **Visual Studio Code (recommended)**: Or use any other IDE of your choice.

- **Event Hubs namespace and event hub**: Follow [this guide](event-hubs-create.md) to create them in the [Azure portal](https://portal.azure.com).

### Install the packages to send events

To install the Python packages for Event Hubs, open a command prompt that has Python in its path. Change the directory to the folder where you want to keep your samples.

## [Passwordless (Recommended)](#tab/passwordless)

```shell

pip install azure-eventhub

pip install azure-identity

pip install aiohttp

```

## [Connection String](#tab/connection-string)

```shell

pip install azure-eventhub

```

---

### Authenticate the app to Azure

[!INCLUDE [event-hub-passwordless-template-tabbed](../../includes/passwordless/event-hub/event-hub-passwordless-template-tabbed-basic.md)]

## Send events

In this section, create a Python script to send events to the event hub that you created earlier.

1. Open your favorite Python editor, such as [Visual Studio Code](https://code.visualstudio.com/).

1. Create a script called *send.py*. This script sends a batch of events to the event hub that you created earlier.

1. Paste the following code into *send.py*:

## [Passwordless (Recommended)](#tab/passwordless)

In the code, use real values to replace the following placeholders:

* `EVENT_HUB_FULLY_QUALIFIED_NAMESPACE` - You see the fully qualified name on the **Overview** page of the namespace. It should be in the format: `<NAMESPACENAME>>.servicebus.windows.net`.

* `EVENT_HUB_NAME` - Name of the event hub.

```python

import asyncio

from azure.eventhub import EventData

from azure.eventhub.aio import EventHubProducerClient

from azure.identity.aio import DefaultAzureCredential

EVENT_HUB_FULLY_QUALIFIED_NAMESPACE = "EVENT_HUB_FULLY_QUALIFIED_NAMESPACE"

EVENT_HUB_NAME = "EVENT_HUB_NAME"

credential = DefaultAzureCredential()

async def run():

# Create a producer client to send messages to the event hub.

# Specify a credential that has correct role assigned to access

# event hubs namespace and the event hub name.

producer = EventHubProducerClient(

fully_qualified_namespace=EVENT_HUB_FULLY_QUALIFIED_NAMESPACE,

eventhub_name=EVENT_HUB_NAME,

credential=credential,

)

print("Producer client created successfully.")

async with producer:

# Create a batch.

event_data_batch = await producer.create_batch()

# Add events to the batch.

event_data_batch.add(EventData("First event "))

event_data_batch.add(EventData("Second event"))

event_data_batch.add(EventData("Third event"))

# Send the batch of events to the event hub.

await producer.send_batch(event_data_batch)

# Close credential when no longer needed.

await credential.close()

asyncio.run(run())

```

## [Connection String](#tab/connection-string)

In the code, use real values to replace the following placeholders:

* `EVENT_HUB_CONNECTION_STR`

* `EVENT_HUB_NAME`

> [!NOTE]

> Make sure that **EVENT_HUB_NAME** is the name of the event hub and not the Event Hubs namespace. If this value is incorrect, you receive the error code: `CBS Token authentication failed.`.

```python

import asyncio

from azure.eventhub import EventData

from azure.eventhub.aio import EventHubProducerClient

EVENT_HUB_CONNECTION_STR = "EVENT_HUB_CONNECTION_STR"

EVENT_HUB_NAME = "EVENT_HUB_NAME"

async def run():

# Create a producer client to send messages to the event hub.

# Specify a connection string to your event hubs namespace and

# the event hub name.

producer = EventHubProducerClient.from_connection_string(

conn_str=EVENT_HUB_CONNECTION_STR, eventhub_name=EVENT_HUB_NAME

)

async with producer:

# Create a batch.

event_data_batch = await producer.create_batch()

# Add events to the batch.

event_data_batch.add(EventData("First event "))

event_data_batch.add(EventData("Second event"))

event_data_batch.add(EventData("Third event"))

# Send the batch of events to the event hub.

await producer.send_batch(event_data_batch)

asyncio.run(run())

```

---

> [!NOTE]

> For examples of other options for sending events to an event hub asynchronously using a connection string, see the [GitHub send_async.py page](https://github.com/Azure/azure-sdk-for-python/blob/master/sdk/eventhub/azure-eventhub/samples/async_samples/send_async.py). The patterns shown there are also applicable to sending events passwordless.

## Receive events

This quickstart uses Azure Blob storage as a checkpoint store. The checkpoint store is used to persist checkpoints (that is, the last read positions).

[!INCLUDE [storage-checkpoint-store-recommendations](./includes/storage-checkpoint-store-recommendations.md)]

### Create an Azure storage account and a blob container

Create an Azure storage account and a blob container in it by doing the following steps:

1. [Create an Azure Storage account](../storage/common/storage-account-create.md?tabs=azure-portal)

2. [Create a blob container](../storage/blobs/storage-quickstart-blobs-portal.md#create-a-container).

3. Authenticate to the blob container.

Be sure to record the connection string and container name for later use in the receive code.

## [Passwordless (Recommended)](#tab/passwordless)

[!INCLUDE [event-hub-storage-assign-roles](../../includes/passwordless/event-hub/event-hub-storage-assign-roles.md)]

## [Connection String](#tab/connection-string)

Follow instructions from [Get the connection string to the storage account](../storage/common/storage-configure-connection-string.md) to get the connection string to the storage account, which you use in the script (`BLOB_STORAGE_CONNECTION_STRING`). You need the connection string and the name of the blob container you created.

---

### Install the packages to receive events

For the receiving side, you need to install one or more packages. In this quickstart, you use Azure Blob storage to persist checkpoints so that the program doesn't read the events that it already read. It performs metadata checkpoints on received messages at regular intervals in a blob. This approach makes it easy to continue receiving messages later from where you left off.

## [Passwordless (Recommended)](#tab/passwordless)

```shell

pip install azure-eventhub-checkpointstoreblob-aio

pip install azure-identity

```

## [Connection String](#tab/connection-string)

```shell

pip install azure-eventhub-checkpointstoreblob-aio

```

---

### Create a Python script to receive events

In this section, you create a Python script to receive events from your event hub:

1. Open your favorite Python editor, such as [Visual Studio Code](https://code.visualstudio.com/).

1. Create a script called *recv.py*.

1. Paste the following code into *recv.py*:

## [Passwordless (Recommended)](#tab/passwordless)

In the code, use real values to replace the following placeholders:

* `BLOB_STORAGE_ACCOUNT_URL` - This value should be in the format: `https://<YOURSTORAGEACCOUNTNAME>.blob.core.windows.net/`

* `BLOB_CONTAINER_NAME` - Name of the blob container in the Azure storage account.

* `EVENT_HUB_FULLY_QUALIFIED_NAMESPACE`  - You see the fully qualified name on the **Overview** page of the namespace. It should be in the format: `<NAMESPACENAME>>.servicebus.windows.net`.

* `EVENT_HUB_NAME` - Name of the event hub.

```python

import asyncio

from azure.eventhub.aio import EventHubConsumerClient

from azure.eventhub.extensions.checkpointstoreblobaio import (

BlobCheckpointStore,

)

from azure.identity.aio import DefaultAzureCredential

BLOB_STORAGE_ACCOUNT_URL = "BLOB_STORAGE_ACCOUNT_URL"

BLOB_CONTAINER_NAME = "BLOB_CONTAINER_NAME"

EVENT_HUB_FULLY_QUALIFIED_NAMESPACE = "EVENT_HUB_FULLY_QUALIFIED_NAMESPACE"

EVENT_HUB_NAME = "EVENT_HUB_NAME"

credential = DefaultAzureCredential()

async def on_event(partition_context, event):

# Print the event data.

print(

'Received the event: "{}" from the partition with ID: "{}"'.format(

event.body_as_str(encoding="UTF-8"), partition_context.partition_id

)

)

# Update the checkpoint so that the program doesn't read the events

# that it has already read when you run it next time.

await partition_context.update_checkpoint(event)

async def main():

# Create an Azure blob checkpoint store to store the checkpoints.

checkpoint_store = BlobCheckpointStore(

blob_account_url=BLOB_STORAGE_ACCOUNT_URL,

container_name=BLOB_CONTAINER_NAME,

credential=credential,

)

# Create a consumer client for the event hub.

client = EventHubConsumerClient(

fully_qualified_namespace=EVENT_HUB_FULLY_QUALIFIED_NAMESPACE,

eventhub_name=EVENT_HUB_NAME,

consumer_group="$Default",

checkpoint_store=checkpoint_store,

credential=credential,

)

async with client:

# Call the receive method. Read from the beginning of the partition

# (starting_position: "-1")

await client.receive(on_event=on_event, starting_position="-1")

# Close credential when no longer needed.

await credential.close()

if __name__ == "__main__":

# Run the main method.

asyncio.run(main())

```

## [Connection String](#tab/connection-string)

In the code, use real values to replace the following placeholders:

* `BLOB_STORAGE_CONNECTION_STRING` - Connection string to the Blob Storage account that you noted earlier.

* `BLOB_CONTAINER_NAME` - Name of the blob container you created in the blob storage.

* `EVENT_HUB_CONNECTION_STR` - Connection string to the Event Hubs namespace you noted earlier.

* `EVENT_HUB_NAME` - Name of the event hub.

```python

import asyncio

from azure.eventhub.aio import EventHubConsumerClient

from azure.eventhub.extensions.checkpointstoreblobaio import (

BlobCheckpointStore,

)

BLOB_STORAGE_CONNECTION_STRING = "BLOB_STORAGE_CONNECTION_STRING"

BLOB_CONTAINER_NAME = "BLOB_CONTAINER_NAME"

EVENT_HUB_CONNECTION_STR = "EVENT_HUB_CONNECTION_STR"

EVENT_HUB_NAME = "EVENT_HUB_NAME"

async def on_event(partition_context, event):

# Print the event data.

print(

'Received the event: "{}" from the partition with ID: "{}"'.format(

event.body_as_str(encoding="UTF-8"), partition_context.partition_id

)

)

# Update the checkpoint so that the program doesn't read the events

# that it has already read when you run it next time.

await partition_context.update_checkpoint(event)

async def main():

# Create an Azure blob checkpoint store to store the checkpoints.

checkpoint_store = BlobCheckpointStore.from_connection_string(

BLOB_STORAGE_CONNECTION_STRING, BLOB_CONTAINER_NAME

)

# Create a consumer client for the event hub.

client = EventHubConsumerClient.from_connection_string(

EVENT_HUB_CONNECTION_STR,

consumer_group="$Default",

eventhub_name=EVENT_HUB_NAME,

checkpoint_store=checkpoint_store,

)

async with client:

# Call the receive method. Read from the beginning of the

# partition (starting_position: "-1")

await client.receive(on_event=on_event, starting_position="-1")

if __name__ == "__main__":

asyncio.run(main())

```

---

> [!NOTE]

> For examples of other options for receiving events from an event hub asynchronously using a connection string, see the [GitHub recv_with_checkpoint_store_async.py

page](https://github.com/Azure/azure-sdk-for-python/blob/master/sdk/eventhub/azure-eventhub/samples/async_samples/recv_with_checkpoint_store_async.py). The patterns shown there are also applicable to receiving events passwordless.

### Run the receiver app

1. Launch a command prompt.

1. Run the following command and sign in using account that was added to the **Azure Event Hubs Data Owner** role on the Event Hubs namespace and **Storage Blob Data Contributor** role on the Azure storage account.

```azurecli

az login

```

1. Switch to the folder that has the receive.py file, and run the following command:

```bash

python recv.py

```

### Run the sender app

1. Launch a command prompt.

1. Run the following command and sign in using account that was added to the **Azure Event Hubs Data Owner** role on the Event Hubs namespace and **Storage Blob Data Contributor** role on the Azure storage account.

```azurecli

az login

```

1. Switch to the folder that has the send.py, and then run this command:

```bash

python send.py

```

The receiver window should display the messages that were sent to the event hub.

### Troubleshooting

If you don't see events in the receiver window or the code reports an error, try the following troubleshooting tips:

* If you don't see results from *recy.py*, run *send.py* several times.

* If you see errors about "coroutine" when using the passwordless code (with credentials), make sure you're using importing from `azure.identity.aio`.

* If you see "Unclosed client session" with passwordless code (with credentials), make sure you close the credential when finished. For more information, see [Async credentials](/python/api/overview/azure/identity-readme?view=azure-python&preserve-view=true#async-credentials).

* If you see authorization errors with *recv.py* when accessing storage, make sure you followed the steps in [Create an Azure storage account and a blob container](#create-an-azure-storage-account-and-a-blob-container) and assigned the **Storage Blob Data Contributor** role to the service principal.

* If you receive events with different partition IDs, this result is expected. Partitions are a data organization mechanism that relates to the downstream parallelism required in consuming applications. The number of partitions in an event hub directly relates to the number of concurrent readers you expect to have. For more information, see [Learn more about partitions](./event-hubs-features.md#partitions).

## Next steps

In this quickstart, you sent and received events asynchronously. To learn how to send and receive events synchronously, go to the [GitHub sync_samples page](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/eventhub/azure-eventhub/samples/sync_samples).

Explore more examples and advanced scenarios in the [Azure Event Hubs client library for Python samples](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/eventhub/azure-eventhub/samples).


# Event Hubs Node Get Started Send

# Quickstart: Send events to or receive events from event hubs by using JavaScript

In this Quickstart, you learn how to send events to and receive events from an event hub using the **@azure/event-hubs** npm package.

If you're new to Azure Event Hubs, see [Event Hubs overview](event-hubs-about.md) before you begin.

## Prerequisites

- Microsoft Azure subscription. To use Azure services, including Azure Event Hubs, you need a subscription. If you don't have an Azure account, sign up for a [free trial](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- Node.js LTS. Download the latest [long-term support (LTS) version](https://nodejs.org).

- Visual Studio Code (recommended) or any other integrated development environment (IDE).

- Create an Event Hubs namespace and an event hub. Use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs Get the management credentials that your application needs to communicate with the event hub. For more information, see [Create an event hub using Azure portal](event-hubs-create.md).

### Install npm packages to send events

To install the [Node Package Manager (npm) package for Event Hubs](https://www.npmjs.com/package/@azure/event-hubs), open a Command Prompt window that has `npm` in its path. Change the directory to the folder where you want to keep your samples.

### [Passwordless (Recommended)](#tab/passwordless)

Run these commands:

```shell

npm install @azure/event-hubs

npm install @azure/identity

```

### [Connection String](#tab/connection-string)

Run this command:

```shell

npm install @azure/event-hubs

```

---

### Authenticate the app to Azure

[!INCLUDE [event-hub-passwordless-template-tabbed](../../includes/passwordless/event-hub/event-hub-passwordless-template-tabbed-basic.md)]

## Send events

In this section, you create a JavaScript application that sends events to an event hub.

1. Open a text editor, such as [Visual Studio Code](https://code.visualstudio.com).

1. Create a file called *send.js*. Paste the following code into it:

## [Passwordless (Recommended)](#tab/passwordless)

In the code, use real values to replace the following placeholders:

- `EVENT HUBS NAMESPACE NAME`

- `EVENT HUB NAME`

```javascript

const { EventHubProducerClient } = require("@azure/event-hubs");

const { DefaultAzureCredential } = require("@azure/identity");

// Event hubs

const eventHubsResourceName = "EVENT HUBS NAMESPACE NAME";

const fullyQualifiedNamespace = `${eventHubsResourceName}.servicebus.windows.net`;

const eventHubName = "EVENT HUB NAME";

// Azure Identity - passwordless authentication

const credential = new DefaultAzureCredential();

async function main() {

// Create a producer client to send messages to the event hub.

const producer = new EventHubProducerClient(fullyQualifiedNamespace, eventHubName, credential);

// Prepare a batch of three events.

const batch = await producer.createBatch();

const events = [

{ body: "passwordless First event" },

{ body: "passwordless Second event" },

{ body: "passwordless Third event" },

];

for (const event of events) {

if (!batch.tryAdd(event)) {

throw new Error("Event is too large for the batch.");

}

}

// Send the batch to the event hub.

await producer.sendBatch(batch);

// Close the producer client.

await producer.close();

console.log("A batch of three events have been sent to the event hub");

}

main().catch((err) => {

console.log("Error occurred: ", err);

});

```

## [Connection String](#tab/connection-string)

In the code, use real values to replace the following placeholders:

- `EVENT HUB NAME`

- `EVENT HUBS NAMESPACE CONNECTION STRING`

```javascript

const { EventHubProducerClient } = require("@azure/event-hubs");

const connectionString = "EVENT HUBS NAMESPACE CONNECTION STRING";

const eventHubName = "EVENT HUB NAME";

async function main() {

// Create a producer client to send messages to the event hub.

const producer = new EventHubProducerClient(connectionString, eventHubName);

// Prepare a batch of three events.

const batch = await producer.createBatch();

const events = [

{ body: "First event" },

{ body: "Second event" },

{ body: "Third event" },

];

for (const event of events) {

if (!batch.tryAdd(event)) {

throw new Error("Event is too large for the batch.");

}

}

// Send the batch to the event hub.

await producer.sendBatch(batch);

// Close the producer client.

await producer.close();

console.log("A batch of three events have been sent to the event hub");

}

main().catch((err) => {

console.log("Error occurred: ", err);

});

```

---

1. To run the application, use this command:

```bash

node send.js

```

The command sends a batch of three events to your event hub.

If you're using the passwordless (Microsoft Entra ID Role-based access control (RBAC)) authentication, you might need sign into Azure using the account that you added to the Azure Event Hubs Data Owner role. Use the `az login` command.

1. In the Azure portal, verify that the event hub received the messages. To update the chart, refresh the page. It might take a few seconds for it to show that the messages are received.

> [!NOTE]

> For more information and the complete source code, see [GitHub sendEvents.js page](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/eventhub/event-hubs/samples/v5/javascript/sendEvents.js).

## Receive events

In this section, you receive events from an event hub by using an Azure Blob storage checkpoint store in a JavaScript application. It performs metadata checkpoints on received messages at regular intervals in an Azure Storage blob. This approach makes it easy to continue receiving messages later from where you left off.

[!INCLUDE [storage-checkpoint-store-recommendations](./includes/storage-checkpoint-store-recommendations.md)]

### Create an Azure storage account and a blob container

To create an Azure storage account with a blob container:

1. [Create an Azure storage account](../storage/common/storage-account-create.md?tabs=azure-portal)

1. [Create a blob container in the storage account](../storage/blobs/storage-quickstart-blobs-portal.md#create-a-container)

1. Authenticate to the blob container

## [Passwordless (Recommended)](#tab/passwordless)

[!INCLUDE [event-hub-storage-assign-roles](../../includes/passwordless/event-hub/event-hub-storage-assign-roles.md)]

## [Connection String](#tab/connection-string)

Get the connection string to the storage account. See [Configure Azure Storage connection strings](../storage/common/storage-configure-connection-string.md).

Note the connection string and the container name. You use them in the code to receive events.

---

### Install the npm packages to receive events

For the receiving side, you need to install two more packages. In this quickstart, you use Azure Blob storage to persist checkpoints so that the program doesn't read the events that it already read. It performs metadata checkpoints on received messages at regular intervals in a blob. This approach makes it easy to continue receiving messages later from where you left off.

### [Passwordless (Recommended)](#tab/passwordless)

Run these commands:

```shell

npm install @azure/storage-blob

npm install @azure/eventhubs-checkpointstore-blob

npm install @azure/identity

```

### [Connection String](#tab/connection-string)

Run these commands:

```shell

npm install @azure/storage-blob

npm install @azure/eventhubs-checkpointstore-blob

```

---

### Write code to receive events

1. Open a text editor, such as [Visual Studio Code](https://code.visualstudio.com).

1. Create a file called *receive.js*. Paste the following code into it:

### [Passwordless (Recommended)](#tab/passwordless)

In the code, use real values to replace the following placeholders:

- `EVENT HUBS NAMESPACE NAME`

- `EVENT HUB NAME`

- `STORAGE ACCOUNT NAME`

- `STORAGE CONTAINER NAME`

```javascript

const { DefaultAzureCredential } = require("@azure/identity");

const { EventHubConsumerClient, earliestEventPosition  } = require("@azure/event-hubs");

const { ContainerClient } = require("@azure/storage-blob");

const { BlobCheckpointStore } = require("@azure/eventhubs-checkpointstore-blob");

// Event hubs

const eventHubsResourceName = "EVENT HUBS NAMESPACE NAME";

const fullyQualifiedNamespace = `${eventHubsResourceName}.servicebus.windows.net`;

const eventHubName = "EVENT HUB NAME";

const consumerGroup = "$Default"; // name of the default consumer group

// Azure Storage

const storageAccountName = "STORAGE ACCOUNT NAME";

const storageContainerName = "STORAGE CONTAINER NAME";

const baseUrl = `https://${storageAccountName}.blob.core.windows.net`;

// Azure Identity - passwordless authentication

const credential = new DefaultAzureCredential();

async function main() {

// Create a blob container client and a blob checkpoint store using the client.

const containerClient = new ContainerClient(

`${baseUrl}/${storageContainerName}`,

credential

);

const checkpointStore = new BlobCheckpointStore(containerClient);

// Create a consumer client for the event hub by specifying the checkpoint store.

const consumerClient = new EventHubConsumerClient(consumerGroup, fullyQualifiedNamespace, eventHubName, credential, checkpointStore);

// Subscribe to the events, and specify handlers for processing the events and errors.

const subscription = consumerClient.subscribe({

processEvents: async (events, context) => {

if (events.length === 0) {

console.log(`No events received within wait time. Waiting for next interval`);

return;

}

for (const event of events) {

console.log(`Received event: '${event.body}' from partition: '${context.partitionId}' and consumer group: '${context.consumerGroup}'`);

}

// Update the checkpoint.

await context.updateCheckpoint(events[events.length - 1]);

},

processError: async (err, context) => {

console.log(`Error : ${err}`);

}

},

{ startPosition: earliestEventPosition }

);

// After 30 seconds, stop processing.

await new Promise((resolve) => {

setTimeout(async () => {

await subscription.close();

await consumerClient.close();

resolve();

}, 30000);

});

}

main().catch((err) => {

console.log("Error occurred: ", err);

});

```

### [Connection String](#tab/connection-string)

In the code, use real values to replace the following placeholders:

- `EVENT HUBS NAMESPACE CONNECTION STRING`

- `EVENT HUB NAME`

- `STORAGE CONNECTION STRING`

- `STORAGE CONTAINER NAME`

```javascript

const { EventHubConsumerClient, earliestEventPosition  } = require("@azure/event-hubs");

const { ContainerClient } = require("@azure/storage-blob");

const { BlobCheckpointStore } = require("@azure/eventhubs-checkpointstore-blob");

const connectionString = "EVENT HUBS NAMESPACE CONNECTION STRING";

const eventHubName = "EVENT HUB NAME";

const consumerGroup = "$Default"; // name of the default consumer group

const storageConnectionString = "STORAGE CONNECTION STRING";

const containerName = "STORAGE CONTAINER NAME";

async function main() {

// Create a blob container client and a blob checkpoint store using the client.

const containerClient = new ContainerClient(storageConnectionString, containerName);

const checkpointStore = new BlobCheckpointStore(containerClient);

// Create a consumer client for the event hub by specifying the checkpoint store.

const consumerClient = new EventHubConsumerClient(consumerGroup, connectionString, eventHubName, checkpointStore);

// Subscribe to the events, and specify handlers for processing the events and errors.

const subscription = consumerClient.subscribe({

processEvents: async (events, context) => {

if (events.length === 0) {

console.log(`No events received within wait time. Waiting for next interval`);

return;

}

for (const event of events) {

console.log(`Received event: '${event.body}' from partition: '${context.partitionId}' and consumer group: '${context.consumerGroup}'`);

}

// Update the checkpoint.

await context.updateCheckpoint(events[events.length - 1]);

},

processError: async (err, context) => {

console.log(`Error : ${err}`);

}

},

{ startPosition: earliestEventPosition }

);

// After 30 seconds, stop processing.

await new Promise((resolve) => {

setTimeout(async () => {

await subscription.close();

await consumerClient.close();

resolve();

}, 30000);

});

}

main().catch((err) => {

console.log("Error occurred: ", err);

});

```

---

1. To run this code, use the command `node receive.js`. The window display messages about received events.

```bash

C:\Self Study\Event Hubs\JavaScript>node receive.js

Received event: 'First event' from partition: '0' and consumer group: '$Default'

Received event: 'Second event' from partition: '0' and consumer group: '$Default'

Received event: 'Third event' from partition: '0' and consumer group: '$Default'

```

> [!NOTE]

> For the complete source code, including informational comments, see [receiveEventsUsingCheckpointStore.js](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/eventhub/eventhubs-checkpointstore-blob/samples/v1/javascript/receiveEventsUsingCheckpointStore.js).

The receiver program receives events from all the partitions of the default consumer group in the event hub.

## Clean up resources

Delete the resource group that has the Event Hubs namespace or delete only the namespace if you want to keep the resource group.

## Related content

- [JavaScript samples](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/eventhub/event-hubs/samples/v5/javascript)

- [TypeScript samples](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/eventhub/event-hubs/samples/v5/typescript)


# Event Hubs Go Get Started Send

# Quickstart: Send events to or receive events from Event Hubs using Go

Azure Event Hubs is a Big Data streaming platform and event ingestion service, capable of receiving and processing millions of events per second. Event Hubs can process and store events, data, or telemetry produced by distributed software and devices. Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters. For detailed overview of Event Hubs, see [Event Hubs overview](event-hubs-about.md) and [Event Hubs features](event-hubs-features.md).

This quickstart describes how to write Go applications to send events to or receive events from an event hub.

> [!NOTE]

> This quickstart is based on samples on GitHub at [https://github.com/Azure/azure-sdk-for-go/tree/main/sdk/messaging/azeventhubs](https://github.com/Azure/azure-sdk-for-go/tree/main/sdk/messaging/azeventhubs). The send events section is based on the **example_producing_events_test.go** sample and the receive one is based on the **example_processor_test.go** sample. The code is simplified for the quickstart and all the detailed comments are removed, so look at the samples for more details and explanations.

## Prerequisites

To complete this quickstart, you need the following prerequisites:

- Go installed locally. Follow [these instructions](https://go.dev/doc/install) if necessary.

- An active Azure account. If you don't have an Azure subscription, create a [free account][] before you begin.

- **Create an Event Hubs namespace and an event hub**. Use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub. To create a namespace and an event hub, follow the procedure in [this article](event-hubs-create.md).

## Send events

This section shows you how to create a Go application to send events to an event hub.

### Install Go package

Get the Go package for Event Hubs as shown in the following example.

```bash

go get github.com/Azure/azure-sdk-for-go/sdk/messaging/azeventhubs

```

### Code to send events to an event hub

Here's the code to send events to an event hub. The main steps in the code are:

1. Create an Event Hubs producer client using a connection string to the Event Hubs namespace and the event hub name.

1. Create a batch object and add sample events to the batch.

1. Send the batch of events to th events.

> [!IMPORTANT]

> Replace `NAMESPACE CONNECTION STRING` with the connection string to your Event Hubs namespace and `EVENT HUB NAME` with the event hub name in the sample code.

```go

package main

import (

"context"

"github.com/Azure/azure-sdk-for-go/sdk/messaging/azeventhubs"

)

func main() {

// create an Event Hubs producer client using a connection string to the namespace and the event hub

producerClient, err := azeventhubs.NewProducerClientFromConnectionString("NAMESPACE CONNECTION STRING", "EVENT HUB NAME", nil)

if err != nil {

panic(err)

}

defer producerClient.Close(context.TODO())

// create sample events

events := createEventsForSample()

// create a batch object and add sample events to the batch

newBatchOptions := &azeventhubs.EventDataBatchOptions{}

batch, err := producerClient.NewEventDataBatch(context.TODO(), newBatchOptions)

if err != nil {

panic(err)

}

for i := 0; i < len(events); i++ {

err = batch.AddEventData(events[i], nil)

if err != nil {

panic(err)

}

}

// send the batch of events to the event hub

err = producerClient.SendEventDataBatch(context.TODO(), batch, nil)

if err != nil {

panic(err)

}

}

func createEventsForSample() []*azeventhubs.EventData {

return []*azeventhubs.EventData{

{

Body: []byte("hello"),

},

{

Body: []byte("world"),

},

}

}

```

Don't run the application yet. You first need to run the receiver app and then the sender app.

## Receive events

### Create a Storage account and container

State such as leases on partitions and checkpoints in the events are shared between receivers using an Azure Storage container. You can create a storage account and container with the Go SDK, but you can also create one by following the instructions in [About Azure storage accounts](../storage/common/storage-account-create.md).

[!INCLUDE [storage-checkpoint-store-recommendations](./includes/storage-checkpoint-store-recommendations.md)]

### Go packages

To receive the messages, get the Go packages for Event Hubs as shown in the following example.

```bash

go get github.com/Azure/azure-sdk-for-go/sdk/messaging/azeventhubs

go get github.com/Azure/azure-sdk-for-go/sdk/storage/azblob

```

### Code to receive events from an event hub

Here's the code to receive events from an event hub. The main steps in the code are:

1. Check a checkpoint store object that represents the Azure Blob Storage used by the event hub for checkpointing.

1. Create an Event Hubs consumer client using a connection string to the Event Hubs namespace and the event hub name.

1. Create an event processor using the client object and the checkpoint store object. The processor receives and processes events.

1. For each partition in the event hub, create a partition client with processEvents as the function to process events.

1. Run all partition clients to receive and process events.

> [!IMPORTANT]

> Replace the following placeholder values with actual values:

> - `AZURE STORAGE CONNECTION STRING` with the connection string for your Azure storage account

> - `BLOB CONTAINER NAME` with the name of the blob container you created in the storage account

> - `NAMESPACE CONNECTION STRING` with the connection string for your Event Hubs namespace

> - `EVENT HUB NAME` with the event hub name in the sample code.

```go

package main

import (

"context"

"errors"

"fmt"

"time"

"github.com/Azure/azure-sdk-for-go/sdk/messaging/azeventhubs"

"github.com/Azure/azure-sdk-for-go/sdk/messaging/azeventhubs/checkpoints"

"github.com/Azure/azure-sdk-for-go/sdk/storage/azblob/container"

)

func main() {

// create a container client using a connection string and container name

checkClient, err := container.NewClientFromConnectionString("AZURE STORAGE CONNECTION STRING", "CONTAINER NAME", nil)

if err != nil {

panic(err)

}

// create a checkpoint store that will be used by the event hub

checkpointStore, err := checkpoints.NewBlobStore(checkClient, nil)

if err != nil {

panic(err)

}

// create a consumer client using a connection string to the namespace and the event hub

consumerClient, err := azeventhubs.NewConsumerClientFromConnectionString("NAMESPACE CONNECTION STRING", "EVENT HUB NAME", azeventhubs.DefaultConsumerGroup, nil)

if err != nil {

panic(err)

}

defer consumerClient.Close(context.TODO())

// create a processor to receive and process events

processor, err := azeventhubs.NewProcessor(consumerClient, checkpointStore, nil)

if err != nil {

panic(err)

}

//  for each partition in the event hub, create a partition client with processEvents as the function to process events

dispatchPartitionClients := func() {

for {

partitionClient := processor.NextPartitionClient(context.TODO())

if partitionClient == nil {

break

}

go func() {

if err := processEvents(partitionClient); err != nil {

panic(err)

}

}()

}

}

// run all partition clients

go dispatchPartitionClients()

processorCtx, processorCancel := context.WithCancel(context.TODO())

defer processorCancel()

if err := processor.Run(processorCtx); err != nil {

panic(err)

}

}

func processEvents(partitionClient *azeventhubs.ProcessorPartitionClient) error {

defer closePartitionResources(partitionClient)

for {

receiveCtx, receiveCtxCancel := context.WithTimeout(context.TODO(), time.Minute)

events, err := partitionClient.ReceiveEvents(receiveCtx, 100, nil)

receiveCtxCancel()

if err != nil && !errors.Is(err, context.DeadlineExceeded) {

return err

}

fmt.Printf("Processing %d event(s)\n", len(events))

for _, event := range events {

fmt.Printf("Event received with body %v\n", string(event.Body))

}

if len(events) != 0 {

if err := partitionClient.UpdateCheckpoint(context.TODO(), events[len(events)-1], nil); err != nil {

return err

}

}

}

}

func closePartitionResources(partitionClient *azeventhubs.ProcessorPartitionClient) {

defer partitionClient.Close(context.TODO())

}

```

## Run receiver and sender apps

1. Run the receiver app first.

1. Run the sender app.

1. Wait for a minute to see the following output in the receiver window.

```bash

Processing 2 event(s)

Event received with body hello

Event received with body world

```

## Next steps

See samples on GitHub at [https://github.com/Azure/azure-sdk-for-go/tree/main/sdk/messaging/azeventhubs](https://github.com/Azure/azure-sdk-for-go/tree/main/sdk/messaging/azeventhubs).

[Event Hubs overview]: event-hubs-about.md

[free account]: https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn


# Event Hubs C Getstarted Send

# Quickstart: Send events to Azure Event Hubs using C

## Introduction

Azure Event Hubs is a Big Data streaming platform and event ingestion service, capable of receiving and processing millions of events per second. Event Hubs can process and store events, data, or telemetry produced by distributed software and devices. Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters. For detailed overview of Event Hubs, see [Event Hubs overview](event-hubs-about.md) and [Event Hubs features](event-hubs-features.md).

This tutorial describes how to send events to an event hub using a console application in C.

## Prerequisites

To complete this tutorial, you need the following:

* A C development environment. This tutorial assumes the gcc stack on an Azure Linux VM with Ubuntu 14.04.

* [Microsoft Visual Studio](https://www.visualstudio.com/).

* **Create an Event Hubs namespace and an event hub**. Use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub. To create a namespace and an event hub, follow the procedure in [this article](event-hubs-create.md). Get the value of access key for the event hub by following instructions from the article: [Get connection string](event-hubs-get-connection-string.md#azure-portal). You use the access key in the code you write later in this tutorial. The default key name is: **RootManageSharedAccessKey**.

## Write code to send messages to Event Hubs

In this section shows how to write a C app to send events to your event hub. The code uses the Proton AMQP library from the [Apache Qpid project](https://qpid.apache.org/). This is analogous to using Service Bus queues and topics with AMQP from C as shown [in this sample](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504). For more information, see the [Qpid Proton documentation](https://qpid.apache.org/proton/index.html).

1. From the [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow the instructions to install Qpid Proton, depending on your environment.

2. To compile the Proton library, install the following packages:

```shell

sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev

```

3. Download the [Qpid Proton library](https://qpid.apache.org/proton/index.html), and extract it, e.g.:

```shell

wget https://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz

tar xvfz qpid-proton-0.7.tar.gz

```

4. Create a build directory, compile and install:

```shell

cd qpid-proton-0.7

mkdir build

cd build

cmake -DCMAKE_INSTALL_PREFIX=/usr ..

sudo make install

```

5. In your work directory, create a new file called **sender.c** with the following code. Remember to replace the values for your SAS key/name, event hub name, and namespace. You must also substitute a URL-encoded version of the key for the **SendRule** created earlier. You can URL-encode it [here](https://www.w3schools.com/tags/ref_urlencode.asp).

```c

#include "proton/message.h"

#include "proton/messenger.h"

#include <getopt.h>

#include <proton/util.h>

#include <sys/time.h>

#include <stddef.h>

#include <stdio.h>

#include <string.h>

#include <unistd.h>

#include <stdlib.h>

#include <signal.h>

volatile sig_atomic_t stop = 0;

#define check(messenger)                                                     \

{                                                                          \

if(pn_messenger_errno(messenger))                                        \

{                                                                        \

printf("check\n");                                                     \

die(__FILE__, __LINE__, pn_error_text(pn_messenger_error(messenger))); \

}                                                                        \

}

void interrupt_handler(int signum){

if(signum == SIGINT){

stop = 1;

}

}

pn_timestamp_t time_now(void)

{

struct timeval now;

if (gettimeofday(&now, NULL)) pn_fatal("gettimeofday failed\n");

return ((pn_timestamp_t)now.tv_sec) * 1000 + (now.tv_usec / 1000);

}

void die(const char *file, int line, const char *message)

{

printf("Dead\n");

fprintf(stderr, "%s:%i: %s\n", file, line, message);

exit(1);

}

int sendMessage(pn_messenger_t * messenger) {

char * address = (char *) "amqps://{SAS Key Name}:{SAS key}@{namespace name}.servicebus.windows.net/{event hub name}";

char * msgtext = (char *) "Hello from C!";

pn_message_t * message;

pn_data_t * body;

message = pn_message();

pn_message_set_address(message, address);

pn_message_set_content_type(message, (char*) "application/octect-stream");

pn_message_set_inferred(message, true);

body = pn_message_body(message);

pn_data_put_binary(body, pn_bytes(strlen(msgtext), msgtext));

pn_messenger_put(messenger, message);

check(messenger);

pn_messenger_send(messenger, 1);

check(messenger);

pn_message_free(message);

}

int main(int argc, char** argv) {

printf("Press Ctrl-C to stop the sender process\n");

signal(SIGINT, interrupt_handler);

pn_messenger_t *messenger = pn_messenger(NULL);

pn_messenger_set_outgoing_window(messenger, 1);

pn_messenger_start(messenger);

while(!stop) {

sendMessage(messenger);

printf("Sent message\n");

sleep(1);

}

// release messenger resources

pn_messenger_stop(messenger);

pn_messenger_free(messenger);

return 0;

}

```

6. Compile the file, assuming **gcc**:

```

gcc sender.c -o sender -lqpid-proton

```

> [!NOTE]

> This code uses an outgoing window of 1 to force the messages out as soon as possible. It is recommended that your application try to batch messages to increase throughput. See the [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how to use the Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).

Run the application to send messages to the event hub.

Congratulations! You have now sent messages to an event hub.

## Next steps

Read the following articles:

- [Event processor](event-processor-balance-partition-load.md)

- [Features and terminology in Azure Event Hubs](event-hubs-features.md).

[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png

[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png


# Event Hubs Storm Getstarted Receive

# Quickstart: Receive events from Event Hubs using Apache Storm

[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data. This section shows how to use an Azure Event Hubs Storm spout to receive events from Event Hubs. Using Apache Storm, you can split events across multiple processes hosted in different nodes. The Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.

For more information about Event Hubs receive patterns, see the [Event Hubs overview][Event Hubs overview].

## Prerequisites

Before you start with the quickstart, **create an Event Hubs namespace and an event hub**. Use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub. To create a namespace and an event hub, follow the procedure in [this article](event-hubs-create.md).

## Create project and add code

1. Use the following command to install the package into the local Maven store. This enables you to add it as a reference in the Storm project in a later step.

```shell

mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar

```

1. In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).

![File -> New -> Project][12]

1. Select **Use default Workspace location**, then click **Next**

1. Select the **maven-archetype-quickstart** archetype, then click **Next**

1. Insert a **GroupId** and **ArtifactId**, then click **Finish**

1. In **pom.xml**, add the following dependencies in the `<dependency>` node.

```xml

<dependency>

<groupId>org.apache.storm</groupId>

<artifactId>storm-core</artifactId>

<version>0.9.2-incubating</version>

<scope>provided</scope>

</dependency>

<dependency>

<groupId>com.microsoft.eventhubs</groupId>

<artifactId>eventhubs-storm-spout</artifactId>

<version>0.9</version>

</dependency>

<dependency>

<groupId>com.netflix.curator</groupId>

<artifactId>curator-framework</artifactId>

<version>1.3.3</version>

<exclusions>

<exclusion>

<groupId>log4j</groupId>

<artifactId>log4j</artifactId>

</exclusion>

<exclusion>

<groupId>org.slf4j</groupId>

<artifactId>slf4j-log4j12</artifactId>

</exclusion>

</exclusions>

<scope>provided</scope>

</dependency>

```

1. In the **src** folder, create a file called **Config.properties** and copy the following content, substituting the `receive rule key` and `event hub name` values:

```java

eventhubspout.username = ReceiveRule

eventhubspout.password = {receive rule key}

eventhubspout.namespace = ioteventhub-ns

eventhubspout.entitypath = {event hub name}

eventhubspout.partitions.count = 16

# if not provided, will use storm's zookeeper settings

# zookeeper.connectionstring=localhost:2181

eventhubspout.checkpoint.interval = 10

eventhub.receiver.credits = 10

```

The value for **eventhub.receiver.credits** determines how many events are batched before releasing them to the Storm pipeline. For the sake of simplicity, this example sets this value to 10. In production, it should usually be set to higher values; for example, 1024.

1 . Create a new class called **LoggerBolt** with the following code:

```java

import java.util.Map;

import org.slf4j.Logger;

import org.slf4j.LoggerFactory;

import backtype.storm.task.OutputCollector;

import backtype.storm.task.TopologyContext;

import backtype.storm.topology.OutputFieldsDeclarer;

import backtype.storm.topology.base.BaseRichBolt;

import backtype.storm.tuple.Tuple;

public class LoggerBolt extends BaseRichBolt {

private OutputCollector collector;

private static final Logger logger = LoggerFactory

.getLogger(LoggerBolt.class);

@Override

public void execute(Tuple tuple) {

String value = tuple.getString(0);

logger.info("Tuple value: " + value);

collector.ack(tuple);

}

@Override

public void prepare(Map map, TopologyContext context, OutputCollector collector) {

this.collector = collector;

this.count = 0;

}

@Override

public void declareOutputFields(OutputFieldsDeclarer declarer) {

// no output fields

}

}

```

This Storm bolt logs the content of the received events. This can easily be extended to store tuples in a storage service. The [HDInsight Storm with Event Hub example] uses this same approach to store data into Azure Storage and Power BI.

11. Create a class called **LogTopology** with the following code:

```java

import java.io.FileReader;

import java.util.Properties;

import backtype.storm.Config;

import backtype.storm.LocalCluster;

import backtype.storm.StormSubmitter;

import backtype.storm.generated.StormTopology;

import backtype.storm.topology.TopologyBuilder;

import com.microsoft.eventhubs.samples.EventCount;

import com.microsoft.eventhubs.spout.EventHubSpout;

import com.microsoft.eventhubs.spout.EventHubSpoutConfig;

public class LogTopology {

protected EventHubSpoutConfig spoutConfig;

protected int numWorkers;

protected void readEHConfig(String[] args) throws Exception {

Properties properties = new Properties();

if (args.length > 1) {

properties.load(new FileReader(args[1]));

} else {

properties.load(EventCount.class.getClassLoader()

.getResourceAsStream("Config.properties"));

}

String username = properties.getProperty("eventhubspout.username");

String password = properties.getProperty("eventhubspout.password");

String namespaceName = properties

.getProperty("eventhubspout.namespace");

String entityPath = properties.getProperty("eventhubspout.entitypath");

String zkEndpointAddress = properties

.getProperty("zookeeper.connectionstring"); // opt

int partitionCount = Integer.parseInt(properties

.getProperty("eventhubspout.partitions.count"));

int checkpointIntervalInSeconds = Integer.parseInt(properties

.getProperty("eventhubspout.checkpoint.interval"));

int receiverCredits = Integer.parseInt(properties

.getProperty("eventhub.receiver.credits")); // prefetch count

// (opt)

System.out.println("Eventhub spout config: ");

System.out.println("  partition count: " + partitionCount);

System.out.println("  checkpoint interval: "

+ checkpointIntervalInSeconds);

System.out.println("  receiver credits: " + receiverCredits);

spoutConfig = new EventHubSpoutConfig(username, password,

namespaceName, entityPath, partitionCount, zkEndpointAddress,

checkpointIntervalInSeconds, receiverCredits);

// set the number of workers to be the same as partition number.

// the idea is to have a spout and a logger bolt co-exist in one

// worker to avoid shuffling messages across workers in storm cluster.

numWorkers = spoutConfig.getPartitionCount();

if (args.length > 0) {

// set topology name so that sample Trident topology can use it as

// stream name.

spoutConfig.setTopologyName(args[0]);

}

}

protected StormTopology buildTopology() {

TopologyBuilder topologyBuilder = new TopologyBuilder();

EventHubSpout eventHubSpout = new EventHubSpout(spoutConfig);

topologyBuilder.setSpout("EventHubsSpout", eventHubSpout,

spoutConfig.getPartitionCount()).setNumTasks(

spoutConfig.getPartitionCount());

topologyBuilder

.setBolt("LoggerBolt", new LoggerBolt(),

spoutConfig.getPartitionCount())

.localOrShuffleGrouping("EventHubsSpout")

.setNumTasks(spoutConfig.getPartitionCount());

return topologyBuilder.createTopology();

}

protected void runScenario(String[] args) throws Exception {

boolean runLocal = true;

readEHConfig(args);

StormTopology topology = buildTopology();

Config config = new Config();

config.setDebug(false);

if (runLocal) {

config.setMaxTaskParallelism(2);

LocalCluster localCluster = new LocalCluster();

localCluster.submitTopology("test", config, topology);

Thread.sleep(5000000);

localCluster.shutdown();

} else {

config.setNumWorkers(numWorkers);

StormSubmitter.submitTopology(args[0], config, topology);

}

}

public static void main(String[] args) throws Exception {

LogTopology topology = new LogTopology();

topology.runScenario(args);

}

}

```

This class creates a new Event Hubs spout, using the properties in the configuration file to instantiate it. It is important to note that this example creates as many spouts tasks as the number of partitions in the event hub, in order to use the maximum parallelism allowed by that event hub.

## Next steps

You can learn more about Event Hubs by visiting the following links:

* [Event Hubs overview][Event Hubs overview]

* [Create an event hub](event-hubs-create.md)

* [Event Hubs FAQ](event-hubs-faq.yml)

[Event Hubs overview]: ./event-hubs-about.md

[HDInsight Storm]: ../hdinsight/storm/apache-storm-overview.md

[HDInsight Storm with Event Hub example]: https://github.com/Azure-Samples/hdinsight-java-storm-eventhub

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png


# Event Hubs Quickstart Kafka Enabled Event Hubs

# Quickstart: Stream data with Azure Event Hubs and Apache Kafka

Azure Event Hubs provides a Kafka endpoint that you can use to connect Apache Kafka applications to a managed streaming service without running your own cluster. If you already have Kafka producer or consumer applications, you can point them to Event Hubs with minimal configuration changes.

In this quickstart, you configure sample Kafka producer and consumer apps to stream data through an Event Hubs namespace using the Apache Kafka protocol.

> [!NOTE]

> This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/quickstart/java).

## Prerequisites

To complete this quickstart, make sure you have the following prerequisites:

* Read through the [Event Hubs for Apache Kafka](azure-event-hubs-apache-kafka-overview.md) article.

* An Azure subscription. If you don't have one, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

* Create a Windows virtual machine and install the following components:

* [Java Development Kit (JDK) 1.7+](/azure/developer/java/fundamentals/java-support-on-azure).

* [Download](https://maven.apache.org/download.cgi) and [install](https://maven.apache.org/install.html) a Maven binary archive.

* [Git](https://www.git-scm.com/).

## Create an Azure Event Hubs namespace

When you create an Event Hubs namespace, the Kafka endpoint for the namespace is automatically enabled. You can stream events from your applications that use the Kafka protocol into event hubs. Follow step-by-step instructions in the [Create an event hub using Azure portal](event-hubs-create.md) to create an Event Hubs namespace. If you're using a dedicated cluster, see [Create a namespace and event hub in a dedicated cluster](event-hubs-dedicated-cluster-create-portal.md#create-a-namespace-and-event-hub-within-a-cluster).

> [!NOTE]

> Event Hubs for Kafka isn't supported in the **basic** tier.

## Send and receive messages with Kafka in Event Hubs

### [Passwordless (Recommended)](#tab/passwordless)

This section shows you how to enable a managed identity for a virtual machine and use that identity to authenticate with Event Hubs for Kafka. This authentication mechanism is recommended when connecting to Event Hubs for Kafka from Azure compute services because it eliminates the need for credentials in your code.

1. Enable a system-assigned managed identity for the virtual machine. For more information about configuring managed identity on a virtual machine (VM), see [Configure managed identities for Azure resources on a VM using the Azure portal](../active-directory/managed-identities-azure-resources/qs-configure-portal-windows-vm.md#system-assigned-managed-identity). Managed identities for Azure resources provide Azure services with an automatically managed identity in Microsoft Entra ID. You can use this identity to authenticate to any service that supports Microsoft Entra authentication, without having credentials in your code.

1. Using the **Access control** page of the Event Hubs namespace you created, assign the **Azure Event Hubs Data Owner** role to the VM's managed identity.

Azure Event Hubs supports using Microsoft Entra ID to authorize requests to Event Hubs resources. With Microsoft Entra ID, you can use Azure role-based access control (Azure RBAC) to grant permissions to a security principal, which can be a user or an application service principal.

1. In the Azure portal, navigate to your Event Hubs namespace. Go to **Access Control (IAM)** in the left navigation.

1. Select **+ Add** and select **Add role assignment**.

1. On the **Role** tab, select **Azure Event Hubs Data Owner**, and select **Next**.

1. In the **Members** tab, select the **Managed Identity** in the **Assign access to** section.

1. Select the **+Select members** link.

1. On the **Select managed identities** page, follow these steps:

1. Select the **Azure subscription** that has the VM.

1. For **Managed identity**, select **Virtual machine**.

1. Select your virtual machine's managed identity.

1. Select **Select** at the bottom of the page.

1. Select **Review + Assign**.

1. Restart the VM and sign back in to the VM for which you configured the managed identity.

1. Clone the [Azure Event Hubs for Kafka repository](https://github.com/Azure/azure-event-hubs-for-kafka).

1. Navigate to `azure-event-hubs-for-kafka/tutorials/oauth/java/managedidentity/consumer`.

1. Switch to the `src/main/resources/` folder, and open `consumer.config`. Replace `namespacename` with the name of your Event Hubs namespace.

```xml

bootstrap.servers=NAMESPACENAME.servicebus.windows.net:9093

security.protocol=SASL_SSL

sasl.mechanism=OAUTHBEARER

sasl.jaas.config=org.apache.kafka.common.security.oauthbearer.OAuthBearerLoginModule required;

sasl.login.callback.handler.class=CustomAuthenticateCallbackHandler;

```

> [!NOTE]

> You can find all the OAuth samples for Event Hubs for Kafka [here](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/oauth).

1. Switch back to the **Consumer** folder where the `pom.xml` file is, and run the consumer code to process events from the event hub using your Kafka clients:

```java

mvn clean package

mvn exec:java -Dexec.mainClass="TestConsumer"

```

1. Launch another command prompt window, and navigate to `azure-event-hubs-for-kafka/tutorials/oauth/java/managedidentity/producer`.

1. Switch to the `src/main/resources/` folder, and open `producer.config`. Replace `mynamespace` with the name of your Event Hubs namespace.

1. Switch back to the **Producer** folder where the `pom.xml` file is, and run the producer code to stream events into Event Hubs:

```shell

mvn clean package

mvn exec:java -Dexec.mainClass="TestProducer"

```

You see messages about events sent in the producer window. Now, check the consumer app window to see the messages that it receives from the event hub.

### [Connection string](#tab/connection-string)

1. Clone the [Azure Event Hubs for Kafka repository](https://github.com/Azure/azure-event-hubs-for-kafka).

1. Go to *azure-event-hubs-for-kafka/quickstart/java/consumer*.

1. Update the configuration details for the consumer in *src/main/resources/consumer.config* as follows:

```xml

bootstrap.servers=NAMESPACENAME.servicebus.windows.net:9093

security.protocol=SASL_SSL

sasl.mechanism=PLAIN

sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";

```

> [!IMPORTANT]

> Replace `{YOUR.EVENTHUBS.CONNECTION.STRING}` with the connection string for your Event Hubs namespace. For instructions on getting the connection string, see [Get an Event Hubs connection string](event-hubs-get-connection-string.md). Here's an example configuration: `sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="Endpoint=sb://mynamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=XXXXXXXXXXXXXXXX";`

1. Run the consumer code and process events from the event hub by using your Kafka clients:

```java

mvn clean package

mvn exec:java -Dexec.mainClass="TestConsumer"

```

1. Go to *azure-event-hubs-for-kafka/quickstart/java/producer*.

1. Update the configuration details for the producer in *src/main/resources/producer.config* as follows:

```xml

bootstrap.servers=NAMESPACENAME.servicebus.windows.net:9093

security.protocol=SASL_SSL

sasl.mechanism=PLAIN

sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";

```

> [!IMPORTANT]

> Replace `{YOUR.EVENTHUBS.CONNECTION.STRING}` with the connection string for your Event Hubs namespace. For instructions on getting the connection string, see [Get an Event Hubs connection string](event-hubs-get-connection-string.md). Here's an example configuration: `sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="Endpoint=sb://mynamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=XXXXXXXXXXXXXXXX";`

1. Run the producer code and stream events into Event Hubs:

```shell

mvn clean package

mvn exec:java -Dexec.mainClass="TestProducer"

```

If your Event Hubs Kafka cluster has events, you now start receiving them from the consumer.

---

## Schema validation for Kafka with Schema Registry

You can use Azure Schema Registry to perform schema validation when you stream data with your Kafka applications using Event Hubs.

Azure Schema Registry of Event Hubs provides a centralized repository for managing schemas, and you can seamlessly connect your new or existing Kafka applications with Schema Registry.

To learn more, see [Validate schemas for Apache Kafka applications using Avro](schema-registry-kafka-java-send-receive-quickstart.md).

## Clean up resources

If you no longer need the resources, delete the resource group and all related resources. In the Azure portal, select the resource group for your Event Hubs namespace and select **Delete**.

## Next steps

In this article, you learned how to stream into Event Hubs without changing your protocol clients or running your own clusters. To learn more, see [Apache Kafka developer guide for Azure Event Hubs](apache-kafka-developer-guide.md).


# Event Hubs Quickstart Stream Large Messages

# Quickstart: Send and receive large messages with Azure Event Hubs

In this quickstart, you learn how to send and receive large messages (up to 20 MB) by using Azure Event Hubs. If you're new to Event Hubs, see [Event Hubs overview](event-hubs-about.md) before you begin.

## Prerequisites

- An Azure subscription. To use Azure services, including Event Hubs, you need a subscription. If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) or activate your [Monthly Azure credits for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/?WT.mc_id=A85619ABF).

- A [self-serve scalable dedicated cluster](event-hubs-dedicated-cluster-create-portal.md), an Event Hubs namespace, and an event hub. Use the Azure portal to create a dedicated cluster and namespace inside a cluster. To create an event hub, see [Quickstart: Create an event hub by using the Azure portal](event-hubs-create.md). You can skip this step if you already have a self-serve scalable dedicated cluster.

## Configure an Event Hubs dedicated cluster

To stream large messages, you must configure your self-serve scalable dedicated cluster.

In the Azure portal, go to the **Settings** section for the dedicated cluster. Under **Settings**, select the **Quota** tab.

- Validate that the value for the read-only key `supportslargemessages` is set to `True`.

- You can update the key `eventhubmaxmessagesizeinbytes` to a suitable value in bytes. An acceptable range for this value is between 1,048,576 and 20,971,520 bytes.

After you save the configuration, you're ready to stream large messages with Event Hubs.

> [!IMPORTANT]

> Large message streaming is only supported with self-serve scalable dedicated clusters built out of the latest infrastructure. The `Supportslargemessages` key reflects this capability.

>

> If a cluster value is false, it doesn't support streaming large messages. To enable this feature, you must re-create the cluster. Streaming large messages doesn't incur any extra charges.

## Stream large messages with Event Hubs

Eligible self serve Event hubs dedicated clusters allow streaming of large messages up to 20 MB, both in batches and as individual publications. You can use any existing Event Hubs SDK or Kafka API to stream large messages to Event Hubs. For existing connections, restart clients or re-establish connection to stream large messages.

For more information, see [Send events to and receive events from Event Hubs by using .NET](event-hubs-dotnet-standard-getstarted-send.md).

> [!TIP]

> Make sure to review any Event Hubs Advanced Message Queuing Protocol (AMQP) client or Kafka client configuration that might limit the maximum message size that you stream into Event Hubs. You must update client timeout to a higher value (> 60s) to stream large message , and refine it based on your testing results to meet your workload needs.

>

> By default, the AMQP client prefetch count is 300. Lower this value to avoid client-side memory issues when you deal with large messages.

For the complete SDK reference, see [Azure Event Hubs libraries for .NET](/dotnet/api/overview/azure/event-hubs).


# Event Hubs Capture Enable Through Portal

# Quickstart: Enable capturing of events streaming through Azure Event Hubs

In this quickstart, you use the Azure portal to enable capturing of events to Azure Storage or Azure Data Lake Storage Gen 2. Event Hubs Capture automatically delivers streaming data in Event Hubs to a storage account of your choice.

You can configure capture settings when creating an event hub or for an existing event hub. For conceptual information on this feature, see [Event Hubs Capture overview][capture-overview].

## Prerequisites

- An Azure subscription. If you don't have one, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

- An Event Hubs namespace (Standard tier or higher). If you need to create one, see [Create an Event Hubs namespace](event-hubs-create.md#create-an-event-hubs-namespace). The Basic tier doesn't support the Capture feature.

- An Azure Storage account (Premium tier with Block Blob support), or an Azure Data Lake Storage Gen 2 account.

## Enable Capture when you create an event hub

If you don't have an Event Hubs namespace to work with, create a namespace by following steps from the article: [Create an Event Hubs namespace](event-hubs-create.md#create-an-event-hubs-namespace). Make sure that you select **Standard** or higher **pricing tier**. The basic tier doesn't support the Capture feature.

To create an event hub within the namespace, follow these steps:

1. On the **Overview** page for your namespace, select **+ Event hub** on the command bar.

1. On the **Create event hub** page, type a name for your event hub, and then select **Next: Capture** at the bottom of the page.

1. On the **Capture** tab, select **On** for **Capture**.

1. Drag the slider to set the **Time window** in minutes. The default time window is 5 minutes. The minimum value is 1 and the maximum is 15.

1. Drag the slider to set the **Size window (MB)**. The default value is 300 MB. The minimum value is 10 MB and the maximum value is 500 MB.

1. Specify whether you want Event Hubs to **emit empty files when no events occur during the Capture time window**.

To store captured files, see one of the following sections based on the type of storage you want to use.

> [!IMPORTANT]

> Azure Data Lake Storage Gen1 is retired, so don't use it for capturing event data. For more information, see the [official announcement](https://azure.microsoft.com/updates/action-required-switch-to-azure-data-lake-storage-gen2-by-29-february-2024/). If you're using Azure Data Lake Storage Gen1, migrate to Azure Data Lake Storage Gen2. For more information, see [Azure Data Lake Storage migration guidelines and patterns](../storage/blobs/data-lake-storage-migrate-gen1-to-gen2.md).

## Capture data to Azure Storage

1. For **Capture Provider**, select **Azure Storage Account** (default).

1. For **Azure Storage Container**, choose the **Select the container** link.

1. On the **Storage accounts** page, select the storage account that you want to use to capture data.

1. On the **Containers** page, select the container where you want to store captured files, and then choose **Select**.

Because Event Hubs Capture uses service-to-service authentication with storage, you don't need to specify a storage connection string. The resource picker selects the resource URI for your storage account automatically. If you use Azure Resource Manager, you must supply this URI explicitly as a string.

1. On the **Create event hub** page, confirm that the selected container shows up.

1. For **Capture file name format**, specify format for the captured file names.

1. Select **Review + create** at the bottom of the page.

1. On the **Review + create** page, review settings, and select **Create** to create the event hub.

> [!NOTE]

> If public access is disabled on the storage account, allow **trusted services**, which include Azure Event Hubs, to access the storage account. For details and step-by-step instructions, see [this article](../storage/common/storage-network-security.md#grant-access-to-trusted-azure-services).

## Capture data to Azure Data Lake Storage Gen 2

Follow the [Create a storage account](../storage/common/storage-account-create.md?tabs=azure-portal#create-a-storage-account) article to create an Azure Storage account. Set **Hierarchical namespace** to **Enabled** on the **Advanced** tab to make it an Azure Data Lake Storage Gen 2 account. The Azure Storage account must be in the same subscription as the event hub.

1. Select **Azure Storage** as the capture provider. To use Azure Data Lake Storage Gen2, select **Azure Storage**.

1. For **Azure Storage Container**, choose the **Select the container** link.

1. Select the **Azure Data Lake Storage Gen 2** account from the list.

1. Select the **container** (file system in Data Lake Storage Gen 2), and then choose **Select** at the bottom of the page.

1. For **Capture file name format**, specify format for the captured file names.

1. Select **Review + create** at the bottom of the page.

1. On the **Review + create** page, review settings, and select **Create** to create the event hub.

> [!NOTE]

> The container you create in an Azure Data Lake Storage Gen 2 using this user interface (UI) appears under **File systems** in **Storage Explorer**. Similarly, the file system you create in a Data Lake Storage Gen 2 account shows up as a container in this UI.

## Configure Capture for an existing event hub

You can configure Capture on existing event hubs that are in Event Hubs namespaces. To enable Capture on an existing event hub, or to change your Capture settings, follow these steps:

1. On the home page for your namespace, select **Event Hubs** under **Entities** in the left menu.

1. Select the event hub for which you want to configure the Capture feature.

1. On the **Event Hubs Instance** page, select **Capture** in the left menu.

1. On the **Capture** page, select **Avro** for **Output event serialization format**. The **Parquet** format is supported only via Azure Stream Analytics integration. For more information, see [Capture Event Hubs data in parquet format and analyze with Azure Synapse Analytics](../stream-analytics/event-hubs-parquet-capture-tutorial.md).

1. Select **On** for **Capture**.

1. To configure other settings, see the sections:

- [Capture data to Azure Storage](#capture-data-to-azure-storage)

- [Capture data to Azure Data Lake Storage Gen 2](#capture-data-to-azure-data-lake-storage-gen-2)

## Clean up resources

If you no longer need the resources you created, delete them to avoid incurring charges:

1. Go to your Event Hubs namespace in the Azure portal.

1. Select the event hub you created.

1. Select **Delete** to remove the event hub.

To delete all resources at once, delete the resource group that contains the namespace.

## Related content

You can use a system-assigned or a user-assigned managed identity when capturing event data. First, you enable a managed identity for a namespace, grant the identity an appropriate role on the target storage for capturing events, and then configure the event hub to capture events using the managed identity. For more information, see the following articles:

- [Enable managed identity for a namespace](enable-managed-identity.md).

- [Use a managed identity to capture events](event-hubs-capture-managed-identity.md)

[capture-overview]: event-hubs-capture-overview.md


# Event Hubs Resource Manager Namespace Event Hub Enable Capture

# Create a namespace with event hub and enable Capture using a template

This article shows how to use an Azure Resource Manager template that creates an [Event Hubs](./event-hubs-about.md) namespace, with one event hub instance, and also enables the [Capture feature](event-hubs-capture-overview.md) on the event hub. The article describes how to define which resources are deployed, and how to define parameters that are specified when the deployment is executed. You can use this template for your own deployments, or customize it to meet your requirements.

This article also shows how to specify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on the destination you choose.

For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates]. For the JSON syntax and properties to use in a template, see [Microsoft.EventHub resource types](/azure/templates/microsoft.eventhub/allversions).

For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].

For the complete templates, select the following GitHub links:

- [Create an event hub and enable Capture to Storage template][Event Hub and enable Capture to Storage template]

- [Create an event hub and enable Capture to Azure Data Lake Store template][Event Hub and enable Capture to Azure Data Lake Store template]

> [!NOTE]

> To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.

> [!IMPORTANT]

> Azure Data Lake Storage Gen1 is retired, so don't use it for capturing event data. For more information, see the [official announcement](https://azure.microsoft.com/updates/action-required-switch-to-azure-data-lake-storage-gen2-by-29-february-2024/). If you are using Azure Data Lake Storage Gen1, migrate to Azure Data Lake Storage Gen2. For more information, see [Azure Data Lake Storage migration guidelines and patterns](../storage/blobs/data-lake-storage-migrate-gen1-to-gen2.md).

## What will you deploy?

With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md). Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to Azure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing. Select the following button to enable Event Hubs Capture into Azure Storage:

[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fquickstarts%2Fmicrosoft.eventhub%2Feventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)

Select the following button to enable Event Hubs Capture into Azure Data Lake Store:

[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fquickstarts%2Fmicrosoft.eventhub%2Feventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)

## Parameters

With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed. The template includes a section called `Parameters` that contains all the parameter values. You should define a parameter for those values that vary based on the project you're deploying or based on the environment you're deploying to. Don't define parameters for values that always stay the same. Each parameter value is used in the template to define the resources that are deployed.

The template defines the following parameters.

### eventHubNamespaceName

The name of the Event Hubs namespace to create.

```json

"eventHubNamespaceName":{

"type":"string",

"metadata":{

"description":"Name of the EventHub namespace"

}

}

```

### eventHubName

The name of the event hub created in the Event Hubs namespace.

```json

"eventHubName":{

"type":"string",

"metadata":{

"description":"Name of the event hub"

}

}

```

### messageRetentionInDays

The number of days to retain the messages in the event hub.

```json

"messageRetentionInDays":{

"type":"int",

"defaultValue": 1,

"minValue":"1",

"maxValue":"7",

"metadata":{

"description":"How long to retain the data in event hub"

}

}

```

### partitionCount

The number of partitions to create in the event hub.

```json

"partitionCount":{

"type":"int",

"defaultValue":2,

"minValue":2,

"maxValue":32,

"metadata":{

"description":"Number of partitions chosen"

}

}

```

### captureEnabled

Enable Capture on the event hub.

```json

"captureEnabled":{

"type":"string",

"defaultValue":"true",

"allowedValues": [

"false",

"true"],

"metadata":{

"description":"Enable or disable the Capture for your event hub"

}

}

```

### captureEncodingFormat

The encoding format you specify to serialize the event data.

```json

"captureEncodingFormat":{

"type":"string",

"defaultValue":"Avro",

"allowedValues":[

"Avro"],

"metadata":{

"description":"The encoding format in which Capture serializes the EventData"

}

}

```

### captureTime

The time interval in which Event Hubs Capture starts capturing the data.

```json

"captureTime":{

"type":"int",

"defaultValue":300,

"minValue":60,

"maxValue":900,

"metadata":{

"description":"The time window in seconds for the capture"

}

}

```

### captureSize

The size interval at which Capture starts capturing the data.

```json

"captureSize":{

"type":"int",

"defaultValue":314572800,

"minValue":10485760,

"maxValue":524288000,

"metadata":{

"description":"The size window in bytes for capture"

}

}

```

### captureNameFormat

The name format used by Event Hubs Capture to write the Avro files. The capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields. These fields can be arranged in any order, with or without delimiters.

```json

"captureNameFormat": {

"type": "string",

"defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",

"metadata": {

"description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimiters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"

}

}

```

### apiVersion

The API version of the template.

```json

"apiVersion":{

"type":"string",

"defaultValue":"2017-04-01",

"metadata":{

"description":"ApiVersion used by the template"

}

}

```

Use the following parameters if you choose Azure Storage as your destination.

### destinationStorageAccountResourceId

Capture requires an Azure Storage account resource ID to enable capturing to your desired Storage account.

```json

"destinationStorageAccountResourceId":{

"type":"string",

"metadata":{

"description":"Your existing Storage account resource ID where you want the blobs be captured"

}

}

```

### blobContainerName

The blob container in which to capture your event data.

```json

"blobContainerName":{

"type":"string",

"metadata":{

"description":"Your existing storage container in which you want the blobs captured"

}

}

```

### subscriptionId

Subscription ID for the Event Hubs namespace and Azure Data Lake Store. Both these resources must be under the same subscription ID.

```json

"subscriptionId": {

"type": "string",

"metadata": {

"description": "Subscription ID of both Azure Data Lake Store and Event Hubs namespace"

}

}

```

### dataLakeAccountName

The Azure Data Lake Store name for the captured events.

```json

"dataLakeAccountName": {

"type": "string",

"metadata": {

"description": "Azure Data Lake Store name"

}

}

```

### dataLakeFolderPath

The destination folder path for the captured events. This path is the folder in your Data Lake Store to which the events are pushed during the capture operation. To set permissions on this folder, see [Use Azure Data Lake Store to capture data from Event Hubs](../data-lake-store/data-lake-store-archive-eventhub-capture.md).

```json

"dataLakeFolderPath": {

"type": "string",

"metadata": {

"description": "Destination capture folder path"

}

}

```

## Azure Storage or Azure Data Lake Storage Gen 2 as destination

Creates a namespace of type `Microsoft.EventHub/Namespaces`, with one event hub, and also enables Capture to Azure Blob Storage or Azure Data Lake Storage Gen2.

```json

"resources":[

{

"apiVersion":"[variables('ehVersion')]",

"name":"[parameters('eventHubNamespaceName')]",

"type":"Microsoft.EventHub/Namespaces",

"location":"[variables('location')]",

"sku":{

"name":"Standard",

"tier":"Standard"

},

"resources": [

{

"apiVersion": "2017-04-01",

"name": "[parameters('eventHubNamespaceName')]",

"type": "Microsoft.EventHub/Namespaces",

"location": "[resourceGroup().location]",

"sku": {

"name": "Standard"

},

"properties": {

"isAutoInflateEnabled": "true",

"maximumThroughputUnits": "7"

},

"resources": [

{

"apiVersion": "2017-04-01",

"name": "[parameters('eventHubName')]",

"type": "EventHubs",

"dependsOn": [

"[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"

],

"properties": {

"messageRetentionInDays": "[parameters('messageRetentionInDays')]",

"partitionCount": "[parameters('partitionCount')]",

"captureDescription": {

"enabled": "true",

"skipEmptyArchives": false,

"encoding": "[parameters('captureEncodingFormat')]",

"intervalInSeconds": "[parameters('captureTime')]",

"sizeLimitInBytes": "[parameters('captureSize')]",

"destination": {

"name": "EventHubArchive.AzureBlockBlob",

"properties": {

"storageAccountResourceId": "[parameters('destinationStorageAccountResourceId')]",

"blobContainer": "[parameters('blobContainerName')]",

"archiveNameFormat": "[parameters('captureNameFormat')]"

}

}

}

}

}

]

}

]

```

## Commands to run deployment

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## PowerShell

[!INCLUDE [updated-for-az](~/reusable-content/ce-skilling/azure/includes/updated-for-az.md)]

Deploy your template to enable Event Hubs Capture into Azure Storage:

```powershell

New-AzResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.eventhub/eventhubs-create-namespace-and-enable-capture/azuredeploy.json

```

Deploy your template to enable Event Hubs Capture into Azure Data Lake Store:

```powershell

New-AzResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/quickstarts/microsoft.eventhub/eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json

```

## Azure CLI

Azure Blob Storage as destination:

```azurecli

az deployment group create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.eventhub/eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]

```

Azure Data Lake Store as destination:

```azurecli

az deployment group create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/quickstarts/microsoft.eventhub/eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]

```

## Next steps

You can also configure Event Hubs Capture via the [Azure portal](https://portal.azure.com). For more information, see [Enable Event Hubs Capture using the Azure portal](event-hubs-capture-enable-through-portal.md).

You can learn more about Event Hubs by visiting the following links:

* [Event Hubs overview](./event-hubs-about.md)

* [Create an event hub](event-hubs-create.md)

* [Event Hubs FAQ](event-hubs-faq.yml)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/templates/syntax.md

[Azure Quickstart Templates]:  https://azure.microsoft.com/resources/templates/?term=event+hubs

[Azure Resources naming conventions]: /azure/cloud-adoption-framework/ready/azure-best-practices/naming-and-tagging

[Event hub and enable Capture to Storage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.eventhub/eventhubs-create-namespace-and-enable-capture

[Event hub and enable Capture to Azure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.eventhub/eventhubs-create-namespace-and-enable-capture-for-adls


# Event Hubs Capture Python

# Quickstart: Capture Event Hubs data in Azure Storage and read it by using Python (azure-eventhub)

You can configure an event hub so that the data that's sent to an event hub is captured in an Azure storage account or Azure Data Lake Storage Gen 1 or Gen 2. This article shows you how to write Python code to send events to an event hub and read the captured data from **Azure Blob storage**. For more information about this feature, see [Event Hubs Capture feature overview](event-hubs-capture-overview.md).

This quickstart uses the [Azure Python SDK](https://azure.microsoft.com/develop/python/) to demonstrate the Capture feature. The **sender.py** app sends simulated environmental telemetry to event hubs in JSON format. The event hub is configured to use the Capture feature to write this data to Blob storage in batches. The **capturereader.py** app reads these blobs and creates an append file for each device. The app then writes the data into CSV files.

In this quickstart, you:

> [!div class="checklist"]

> * Create an Azure Blob storage account and container in the Azure portal.

> * Create an Event Hubs namespace by using the Azure portal.

> * Create an event hub with the Capture feature enabled and connect it to your storage account.

> * Send data to your event hub by using a Python script.

> * Read and process files from Event Hubs Capture by using another Python script.

## Prerequisites

- Python 3.8 or later, with pip installed and updated.

- An Azure subscription. If you don't have one, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

- An active Event Hubs namespace and event hub.

[Create an Event Hubs namespace and an event hub in the namespace](event-hubs-create.md). Record the name of the Event Hubs namespace, the name of the event hub, and the primary access key for the namespace. To get the access key, see [Get an Event Hubs connection string](event-hubs-get-connection-string.md#azure-portal). The default key name is *RootManageSharedAccessKey*. For this quickstart, you need only the primary key. You don't need the connection string.

- An Azure storage account, a blob container in the storage account, and a connection string to the storage account. If you don't have these items, do the following steps:

1. [Create an Azure storage account](../storage/common/storage-account-create.md?tabs=azure-portal)

1. [Create a blob container in the storage account](../storage/blobs/storage-quickstart-blobs-portal.md#create-a-container)

1. [Get the connection string to the storage account](../storage/common/storage-account-get-info.md#get-a-connection-string-for-the-storage-account)

Be sure to record the connection string and container name for later use in this quickstart.

## Enable Capture feature for the event hub

Enable the Capture feature for the event hub. To do so, follow the instructions in [Enable Event Hubs Capture using the Azure portal](event-hubs-capture-enable-through-portal.md). Select the storage account and the blob container you created in the preceding step. Select **Avro** for **Output event serialization format**.

## Create a Python script to send events to your event hub

In this section, you create a Python script that sends 200 events (10 devices * 20 events) to an event hub. These events are a sample environmental reading that's sent in JSON format.

1. Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].

2. Create a script called *sender.py*.

3. Paste the following code into *sender.py*.

```python

import time

import os

import uuid

import datetime

import random

import json

from azure.eventhub import EventHubProducerClient, EventData

# This script simulates the production of events for 10 devices.

devices = []

for x in range(0, 10):

devices.append(str(uuid.uuid4()))

# Create a producer client to produce and publish events to the event hub.

producer = EventHubProducerClient.from_connection_string(conn_str="EVENT HUBS NAMESPACE CONNECTION STRING", eventhub_name="EVENT HUB NAME")

for y in range(0,20):    # For each device, produce 20 events.

event_data_batch = producer.create_batch() # Create a batch. You will add events to the batch later.

for dev in devices:

# Create a dummy reading.

reading = {

'id': dev,

'timestamp': str(datetime.datetime.utcnow()),

'uv': random.random(),

'temperature': random.randint(70, 100),

'humidity': random.randint(70, 100)

}

s = json.dumps(reading) # Convert the reading into a JSON string.

event_data_batch.add(EventData(s)) # Add event data to the batch.

producer.send_batch(event_data_batch) # Send the batch of events to the event hub.

# Close the producer.

producer.close()

```

4. Replace the following values in the scripts:

* Replace `EVENT HUBS NAMESPACE CONNECTION STRING` with the connection string for your Event Hubs namespace.

* Replace `EVENT HUB NAME` with the name of your event hub.

5. Run the script to send events to the event hub.

6. In the Azure portal, you can verify that the event hub has received the messages. Switch to **Messages** view in the **Metrics** section. Refresh the page to update the chart. It might take a few seconds for the page to display that the messages have been received.

[![Verify that the event hub received the messages](./media/get-started-capture-python-v2/messages-portal.png)](./media/get-started-capture-python-v2/messages-portal.png#lightbox)

## Create a Python script to read your Capture files

In this example, the captured data is stored in Azure Blob storage. The script in this section reads the captured data files from your Azure storage account and generates CSV files for you to easily open and view. You see 10 files in the current working directory of the application. These files contain the environmental readings for the 10 devices.

1. In your Python editor, create a script called *capturereader.py*. This script reads the captured files and creates a file for each device to write the data only for that device.

2. Paste the following code into *capturereader.py*.

```python

import os

import string

import json

import uuid

import avro.schema

from azure.storage.blob import ContainerClient, BlobClient

from avro.datafile import DataFileReader, DataFileWriter

from avro.io import DatumReader, DatumWriter

def processBlob2(filename):

reader = DataFileReader(open(filename, 'rb'), DatumReader())

dict = {}

for reading in reader:

parsed_json = json.loads(reading["Body"])

if not 'id' in parsed_json:

return

if not parsed_json['id'] in dict:

list = []

dict[parsed_json['id']] = list

else:

list = dict[parsed_json['id']]

list.append(parsed_json)

reader.close()

for device in dict.keys():

filename = os.getcwd() + '\\' + str(device) + '.csv'

deviceFile = open(filename, "a")

for r in dict[device]:

deviceFile.write(", ".join([str(r[x]) for x in r.keys()])+'\n')

def startProcessing():

print('Processor started using path: ' + os.getcwd())

# Create a blob container client.

container = ContainerClient.from_connection_string("AZURE STORAGE CONNECTION STRING", container_name="BLOB CONTAINER NAME")

blob_list = container.list_blobs() # List all the blobs in the container.

for blob in blob_list:

# Content_length == 508 is an empty file, so process only content_length > 508 (skip empty files).

if blob.size > 508:

print('Downloaded a non empty blob: ' + blob.name)

# Create a blob client for the blob.

blob_client = ContainerClient.get_blob_client(container, blob=blob.name)

# Construct a file name based on the blob name.

cleanName = str.replace(blob.name, '/', '_')

cleanName = os.getcwd() + '\\' + cleanName

with open(cleanName, "wb+") as my_file: # Open the file to write. Create it if it doesn't exist.

my_file.write(blob_client.download_blob().readall()) # Write blob contents into the file.

processBlob2(cleanName) # Convert the file into a CSV file.

os.remove(cleanName) # Remove the original downloaded file.

# Delete the blob from the container after it's read.

container.delete_blob(blob.name)

startProcessing()

```

3. Replace `AZURE STORAGE CONNECTION STRING` with the connection string for your Azure storage account. The name of the container you created in this quickstart is *capture*. If you used a different name for the container, replace *capture* with the name of the container in the storage account.

## Run the scripts

1. Open a command prompt that has Python in its path, and then run these commands to install Python prerequisite packages:

```

pip install azure-storage-blob

pip install azure-eventhub

pip install avro-python3

```

2. Change your directory to the directory where you saved *sender.py* and *capturereader.py*, and run this command:

```

python sender.py

```

This command starts a new Python process to run the sender.

3. Wait a few minutes for the capture to run, and then enter the following command in your original command window:

```

python capturereader.py

```

This capture processor uses the local directory to download all the blobs from the storage account and container. It processes files that aren't empty, and it writes the results as CSV files into the local directory.

## Next steps

Check out [Python samples on GitHub](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/eventhub/azure-eventhub/samples).

[Overview of Event Hubs Capture]: event-hubs-capture-overview.md

[1]: ./media/event-hubs-archive-python/event-hubs-python1.png

[About Azure storage accounts]:../storage/common/storage-create-storage-account.md

[Visual Studio Code]: https://code.visualstudio.com/

[Event Hubs overview]: ./event-hubs-about.md


# Create Schema Registry

# Quickstart: Create an Azure Event Hubs schema registry using Azure portal

In this quickstart, you create a schema group with schemas in a schema registry hosted by Azure Event Hubs.

*Azure Schema Registry* is a feature of Event Hubs. It provides a central repository for schemas for event-driven and messaging-centric applications. It provides the flexibility for your producer and consumer applications to *exchange data without having to manage and share the schema*. It also provides a simple governance framework for reusable schemas and defines relationship between schemas through a grouping construct (schema groups). For more information, see [Azure Schema Registry in Event Hubs](schema-registry-overview.md).

> [!NOTE]

> - The feature isn't available in the **Basic** tier.

> - Make sure that you're a member of one of these roles: **Owner**, **Contributor**, or **Schema Registry Contributor**. For more information, see [Azure role-based access control](schema-registry-concepts.md#azure-role-based-access-control).

> - If the event hub is in a *virtual network*, you can't create schemas in the Azure portal unless you access the portal from a virtual machine in the same virtual network.

## Prerequisites

[Create an Event Hubs namespace](event-hubs-create.md#create-an-event-hubs-namespace). You can instead use an existing namespace.

## Create a schema group

1. Navigate to the **Event Hubs Namespace** page.

1. In the left menu, expand **Entities** and select **Schema Registry**.

1. To create a schema group, select **+ Schema Group**.

1. On the **Create Schema Group** page, do these steps:

1. Enter a **name** for the schema group.

1. For **Serialization type**, select **Avro** serialization format. This format applies to all schemas in the schema group. **JSON** serialization format is also supported (preview).

1. Select a **compatibility mode** for all schemas in the group. For **Avro**, forward and backward compatibility modes are supported.

1. Select **Create** to create the schema group.

1. Select the name of the schema group in the list of schema groups.

1. You see the **Schema Group** page for the group.

## Add a schema to the schema group

In this section, you add a schema to the schema group using the Azure portal.

1. On the **Schema Group** page, select **+ Schema** on the toolbar.

1. On the **Create Schema** page, do these steps:

1. For **Name**, enter `orderschema`.

1. Enter the following **schema** into the text box. You can instead select a file with the schema.

```json

{

"namespace": "com.azure.schemaregistry.samples",

"type": "record",

"name": "Order",

"fields": [

{

"name": "id",

"type": "string"

},

{

"name": "amount",

"type": "double"

}

]

}

```

1. Select **Create**.

1. Select the **schema** from the list of schemas.

1. You see the **Schema Overview** page for the schema.

1. If there are multiple versions of a schema, you see them in the **Versions**. Select a version to switch to that version schema.

## Create a new version of schema

1. Update the schema in the text box, and select **Validate**. In the following example, you add a new field called `description` to the schema.

1. Review validation status and changes, and select **Save**.

You see that `2` is selected for the **version** on the **Schema Overview** page.

1. Select `1` to see the version 1 of the schema.

## Clean up resources

> [!NOTE]

> Don't clean up resources if you want to continue to the next quickstart linked from **Next step**.

1. Navigate to the **Event Hubs Namespace** page.

1. Select **Schema Registry** on the left menu.

1. Select the **schema group** you created in this quickstart.

1. On the **Schema Group** page, select **Delete** on the toolbar.

1. On the **Delete Schema Group** page, type the name of the schema group, and select **Delete**.

## Next step

> [!div class="nextstepaction"]

> [Validate schema when sending and receiving events - AMQP and .NET](schema-registry-dotnet-send-receive-quickstart.md).


# Schema Registry Kafka Java Send Receive Quickstart

# Validate schemas for Apache Kafka applications using Avro (Java)

In this quickstart guide, we explore how to validate event from Apache Kafka applications using Azure Schema Registry for Event Hubs.

In this use case a Kafka producer application uses Avro schema stored in Azure Schema Registry to, serialize the event and publish them to a Kafka topic/event hub in Azure Event Hubs. The Kafka consumer deserializes the events that it consumes from Event Hubs. For that it uses schema ID of the event and the Avro schema, which is stored in Azure Schema Registry.

## Prerequisites

If you're new to Azure Event Hubs, see [Event Hubs overview](event-hubs-about.md) before you do this quickstart.

To complete this quickstart, you need the following prerequisites:

- If you don't have an **Azure subscription**, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

- In your development environment, install the following components:

* [Java Development Kit (JDK) 1.7+](/azure/developer/java/fundamentals/java-support-on-azure).

* [Download](https://maven.apache.org/download.cgi) and [install](https://maven.apache.org/install.html) a Maven binary archive.

* [Git](https://www.git-scm.com/)

- Clone the [Azure Schema Registry for Kafka](https://github.com/Azure/azure-schema-registry-for-kafka.git) repository.

## Create an event hub

Follow instructions from the quickstart: [Create an Event Hubs namespace and an event hub](event-hubs-create.md) to create an Event Hubs namespace and an event hub. Then, follow instructions from [Get the connection string](event-hubs-get-connection-string.md) to get a connection string to your Event Hubs namespace.

Note down the following settings that you use in the current quickstart:

- Connection string for the Event Hubs namespace

- Name of the event hub

## Create a schema

Follow instructions from [Create schemas using Schema Registry](create-schema-registry.md) to create a schema group and a schema.

1. Create a schema group named **contoso-sg** using the Schema Registry portal. Use Avro as the serialization type and **None** for the compatibility mode.

1. In that schema group, create a new Avro schema with schema name: ``Microsoft.Azure.Data.SchemaRegistry.example.Order`` using the following schema content.

```json

{

"namespace": "Microsoft.Azure.Data.SchemaRegistry.example",

"type": "record",

"name": "Order",

"fields": [

{

"name": "id",

"type": "string"

},

{

"name": "amount",

"type": "double"

},

{

"name": "description",

"type": "string"

}

]

}

```

## Register an application to access schema registry

You can use Microsoft Entra ID to authorize your Kafka producer and consumer application to access Azure Schema Registry resources by registering your client application with a Microsoft Entra tenant from the Azure portal.

To register a Microsoft Entra application named  `example-app` see [Register your application with a Microsoft Entra tenant](authenticate-application.md).

- tenant.id - sets the tenant ID of the application

- client.id - sets the client ID of the application

- client.secret - sets the client secret for authentication

And if you're using managed identity, you would need:

- use.managed.identity.credential - indicates that MSI credentials should be used, should be used for MSI-enabled VM

- managed.identity.clientId - if specified, it builds MSI credential with given client ID

- managed.identity.resourceId - if specified, it builds MSI credential with given resource ID

## Add user to Schema Registry Reader role

Add your user account to the **Schema Registry Reader** role at the namespace level. You can also use the **Schema Registry Contributor** role, but that's not necessary for this quickstart.

1. On the **Event Hubs namespace** page, select **Access control (IAM)** on the left menu.

2. On the **Access control (IAM)** page, select **+ Add** -> **Add role assignment** on the menu.

3. On the **Assignment type** page, select **Next**.

4. On the **Roles** page, select **Schema Registry Reader (Preview)**, and then select **Next** at the bottom of the page.

5. Use the **+ Select members** link to add the `example-app` application that you created in the previous step to the role, and then select **Next**.

6. On the **Review + assign** page, select **Review + assign**.

## Update client application configuration of Kafka applications

You need to update the client configuration of the Kafka producer and consumer applications with the configuration related to Microsoft Entra application that we created and the schema registry information.

To update the Kafka Producer configuration, navigate to *azure-schema-registry-for-kafka/tree/master/java/avro/samples/kafka-producer*.

1. Update the configuration of the Kafka application in *src/main/resources/app.properties* by following [Kafka Quickstart guide for Event Hubs](event-hubs-quickstart-kafka-enabled-event-hubs.md).

1. Update the configuration details for the producer in *src/main/resources/app.properties* using schema registry related configuration and Microsoft Entra application that you created above as follows:

```xml

schema.group=contoso-sg

schema.registry.url=https://<NAMESPACENAME>.servicebus.windows.net

tenant.id=<>

client.id=<>

client.secret=<>

1. Follow the same instructions and update the *azure-schema-registry-for-kafka/tree/master/java/avro/samples/kafka-consumer* configuration as well.

1. For both Kafka producer and consumer applications, following Avro schema is used:

```avro

{

"namespace": "com.azure.schemaregistry.samples",

"type": "record",

"name": "Order",

"fields": [

{

"name": "id",

"type": "string"

},

{

"name": "amount",

"type": "double"

},

{

"name": "description",

"type": "string"

}

]

}

```

## Using Kafka producer with Avro schema validation

To run the Kafka producer application, navigate to *azure-schema-registry-for-kafka/tree/master/java/avro/samples/kafka-producer*.

1. You can run the producer application so that it can produce Avro specific records or generic records. For specific records mode you need to first generate the classes against either the producer schema using the following maven command:

```shell

mvn generate-sources

```

1. Then you can run the producer application using the following commands.

```shell

mvn clean package

mvn -e clean compile exec:java -Dexec.mainClass="com.azure.schemaregistry.samples.producer.App"

```

1. Upon successful execution of the producer application, it prompts you to choose the producer scenario. For this quickstart, you can choose option *1 - produce Avro SpecificRecords*.

```shell

Enter case number:

1 - produce Avro SpecificRecords

2 - produce Avro GenericRecords

```

1. Upon successful data serialization and publishing, you should see the following console logs in your producer application:

```shell

INFO com.azure.schemaregistry.samples.producer.KafkaAvroSpecificRecord - Sent Order {"id": "ID-0", "amount": 10.0, "description": "Sample order 0"}

INFO com.azure.schemaregistry.samples.producer.KafkaAvroSpecificRecord - Sent Order {"id": "ID-1", "amount": 11.0, "description": "Sample order 1"}

INFO com.azure.schemaregistry.samples.producer.KafkaAvroSpecificRecord - Sent Order {"id": "ID-2", "amount": 12.0, "description": "Sample order 2"}

```

## Using Kafka consumer with Avro schema validation

To run the Kafka consumer application, navigate to *azure-schema-registry-for-kafka/tree/master/java/avro/samples/kafka-consumer*.

1. You can run the consumer application so that it can consume Avro specific records or generic records. For specific records mode you need to first generate the classes against either the producer schema using the following maven command:

```shell

mvn generate-sources

```

1. Then you can run the consumer application using the following command.

```shell

mvn clean package

mvn -e clean compile exec:java -Dexec.mainClass="com.azure.schemaregistry.samples.consumer.App"

```

1. Upon successful execution of the consumer application, it prompts you to choose the producer scenario. For this quickstart, you can choose option *1 - consume Avro SpecificRecords*.

```shell

Enter case number:

1 - consume Avro SpecificRecords

2 - consume Avro GenericRecords

```

1. Upon successful data consumption and deserialization, you should see the following console logs in your producer application:

```shell

INFO com.azure.schemaregistry.samples.consumer.KafkaAvroSpecificRecord - Order received: {"id": "ID-0", "amount": 10.0, "description": "Sample order 0"}

INFO com.azure.schemaregistry.samples.consumer.KafkaAvroSpecificRecord - Order received: {"id": "ID-1", "amount": 11.0, "description": "Sample order 1"}

INFO com.azure.schemaregistry.samples.consumer.KafkaAvroSpecificRecord - Order received: {"id": "ID-2", "amount": 12.0, "description": "Sample order 2"}

```

## Clean up resources

Delete the Event Hubs namespace or delete the resource group that contains the namespace.


# Schema Registry Dotnet Send Receive Quickstart

# Quickstart: Validate using an Avro schema when streaming events using Event Hubs .NET SDKs (AMQP)

In this quickstart, you learn how to send events to and receive events from an event hub with schema validation using the **Azure.Messaging.EventHubs** .NET library.

*Azure Schema Registry* is a feature of Event Hubs. The registry provides a central repository for schemas for event-driven and messaging-centric applications. It provides the flexibility for your producer and consumer applications to *exchange data without having to manage and share the schema*. It also provides a simple governance framework for reusable schemas and defines relationship between schemas through a grouping construct (schema groups). For more information, see [Azure Schema Registry in Event Hubs](schema-registry-overview.md).

## Prerequisites

If you're new to Azure Event Hubs, see [Event Hubs overview](event-hubs-about.md) before you do this quickstart.

To complete this quickstart, you need the following prerequisites:

- If you don't have an **Azure subscription**, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

- Microsoft Visual Studio 2022.

The Azure Event Hubs client library uses features that were introduced in C# 8.0. You can still use the library with previous C# language versions, but the new syntax isn't available. To make use of the full syntax, we recommended that you compile with the [.NET Core SDK](https://dotnet.microsoft.com/download) 3.0 or higher and [language version](/dotnet/csharp/language-reference/configure-language-version) set to `latest`.

If you're using Visual Studio, versions before Visual Studio 2019 aren't compatible with the tools needed to build C# 8.0 projects. To download Visual Studio 2019 or Visual Studio 2022, including the free Community edition, see [Visual Studio](https://visualstudio.microsoft.com/vs/).

## Create an event hub

To create an Event Hubs namespace and an event hub, follow instructions from [Create an Event Hubs namespace and an event hub](event-hubs-create.md).

To get a connection string to your Event Hubs namespace, follow instructions from [Get the connection string](event-hubs-get-connection-string.md).

Note down the following settings to use in the current quickstart:

- Connection string for the Event Hubs namespace

- Name of the event hub

## Create a schema

To create a schema group and a schema, follow instructions from [Create schemas using Schema Registry](create-schema-registry.md).

1. Create a schema group named *contoso-sg* using the Schema Registry portal. Use **Avro** as the serialization type and **None** for the compatibility mode.

1. In that schema group, create a new Avro schema with schema name: `Microsoft.Azure.Data.SchemaRegistry.example.Order`. Use the following schema content.

```json

{

"namespace": "Microsoft.Azure.Data.SchemaRegistry.example",

"type": "record",

"name": "Order",

"fields": [

{

"name": "id",

"type": "string"

},

{

"name": "amount",

"type": "double"

},

{

"name": "description",

"type": "string"

}

]

}

```

## Add user to Schema Registry Reader role

Add your user account to the **Schema Registry Reader** role at the namespace level. You can also use the **Schema Registry Contributor** role, but that's not necessary for this quickstart.

1. On the **Event Hubs Namespace** page, on the left menu, select **Access control (IAM)**.

1. On the **Access control (IAM)** page, select **+ Add** > **Add role assignment**.

1. On the **Roles** page, select **Schema Registry Reader**, and then select **Next**.

1. Use the **+ Select members** link to add your user account to the role, and then select **Next**.

1. On the **Review + assign** page, select **Review + assign**.

## Produce events to event hubs with schema validation

### Create console application for event producer

1. Start Visual Studio.

1. Select **Create a new project**.

1. On the **Create a new project** dialog, do the following steps. If you don't see this dialog, select **File** on the menu, select **New**, and then select **Project**.

1. Select **C#** for the programming language.

1. Select **Console** for the type of the application.

1. Select **Console Application** from the results list.

1. Then, select **Next**.

1. Enter **OrderProducer** for the project name, **SRQuickStart** for the solution name, and then select **OK** to create the project.

### Add the Event Hubs NuGet package

1. Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.

1. Run the following commands to install **Azure.Messaging.EventHubs** and other NuGet packages. Press **ENTER** to run the last command.

```cmd

Install-Package Azure.Messaging.EventHubs

Install-Package Azure.Identity

Install-Package Microsoft.Azure.Data.SchemaRegistry.ApacheAvro

Install-Package Azure.ResourceManager.Compute

```

1. Authenticate producer applications to connect to Azure by using Visual Studio. For more information, see [Azure Identity client library for .NET](/dotnet/api/overview/azure/identity-readme#authenticate-via-visual-studio).

1. Sign in to Azure using the user account that's a member of the `Schema Registry Reader` role at the namespace level. For information about schema registry roles, see [Azure role-based access control](schema-registry-concepts.md#azure-role-based-access-control).

### Code generation using the Avro schema

1. Use the same content you used to create the schema to create a file named `Order.avsc`. Save the file in the project or solution folder.

1. Use this schema file to generate code for .NET. You can use any external code generation tool such as [avrogen](https://www.nuget.org/packages/Apache.Avro.Tools/) for code generation. For example, run ` avrogen -s .\Order.avsc .` to generate code.

1. After you generate code, you see the file named `Order.cs` in the `\Microsoft\Azure\Data\SchemaRegistry\example` folder. For the Avro schema here, it generates the C# types in `Microsoft.Azure.Data.SchemaRegistry.example` namespace.

1. Add the `Order.cs` file to the `OrderProducer` project.

### Write code to serialize and send events to the event hub

1. Add the following code to the `Program.cs` file. See the code comments for details. High-level steps in the code are:

1. Create a producer client that you can use to send events to an event hub.

1. Create a schema registry client that you can use to serialize and validate data in an `Order` object.

1. Create a new `Order` object using the generated `Order` type.

1. Use the schema registry client to serialize the `Order` object to `EventData`.

1. Create a batch of events.

1. Add the event data to the event batch.

1. Use the producer client to send the batch of events to the event hub.

```csharp

using Azure.Data.SchemaRegistry;

using Azure.Identity;

using Microsoft.Azure.Data.SchemaRegistry.ApacheAvro;

using Azure.Messaging.EventHubs;

using Azure.Messaging.EventHubs.Producer;

using Microsoft.Azure.Data.SchemaRegistry.example;

// connection string to the Event Hubs namespace

const string connectionString = "EVENTHUBSNAMESPACECONNECTIONSTRING";

// name of the event hub

const string eventHubName = "EVENTHUBNAME";

// Schema Registry endpoint

const string schemaRegistryEndpoint = "EVENTHUBSNAMESPACENAME.servicebus.windows.net";

// name of the consumer group

const string schemaGroup = "SCHEMAGROUPNAME";

// The Event Hubs client types are safe to cache and use as a singleton for the lifetime

// of the application, which is best practice when events are being published or read regularly.

EventHubProducerClient producerClient;

// Create a producer client that you can use to send events to an event hub

producerClient = new EventHubProducerClient(connectionString, eventHubName);

// Create a schema registry client that you can use to serialize and validate data.

var schemaRegistryClient = new SchemaRegistryClient(schemaRegistryEndpoint, new DefaultAzureCredential());

// Create an Avro object serializer using the Schema Registry client object.

var serializer = new SchemaRegistryAvroSerializer(schemaRegistryClient, schemaGroup, new SchemaRegistryAvroSerializerOptions { AutoRegisterSchemas = true });

// Create a new order object using the generated type/class 'Order'.

var sampleOrder = new Order { id = "1234", amount = 45.29, description = "First sample order." };

EventData eventData = (EventData)await serializer.SerializeAsync(sampleOrder, messageType: typeof(EventData));

// Create a batch of events

using EventDataBatch eventBatch = await producerClient.CreateBatchAsync();

// Add the event data to the event batch.

eventBatch.TryAdd(eventData);

// Send the batch of events to the event hub.

await producerClient.SendAsync(eventBatch);

Console.WriteLine("A batch of 1 order has been published.");

```

1. Replace the following placeholder values with the real values.

- `EVENTHUBSNAMESPACECONNECTIONSTRING` - connection string for the Event Hubs namespace

- `EVENTHUBNAME` - name of the event hub

- `EVENTHUBSNAMESPACENAME` - name of the Event Hubs namespace

- `SCHEMAGROUPNAME` - name of the schema group

```csharp

// connection string to the Event Hubs namespace

const string connectionString = "EVENTHUBSNAMESPACECONNECTIONSTRING";

// name of the event hub

const string eventHubName = "EVENTHUBNAME";

// Schema Registry endpoint

const string schemaRegistryEndpoint = "EVENTHUBSNAMESPACENAME.servicebus.windows.net";

// name of the consumer group

const string schemaGroup = "SCHEMAGROUPNAME";

```

1. Build the project, and ensure that there are no errors.

1. Run the program and wait for the confirmation message.

```csharp

A batch of 1 order has been published.

```

1. In the Azure portal, you can verify that the event hub received the events. Switch to **Messages** view in the **Metrics** section. Refresh the page to update the chart. It might take a few seconds for it to show that it received the messages.

## Consume events from event hubs with schema validation

This section shows how to write a .NET Core console application that receives events from an event hub and use schema registry to deserialize event data.

### Additional prerequisites

- Create the storage account to be used the event processor.

### Create consumer application

1. In the Solution Explorer window, right-click the **SRQuickStart** solution, select **Add**, and select **New Project**.

1. Select **Console application**, and select **Next**.

1. Enter **OrderConsumer** for the **Project name**, and select **Create**.

1. In the **Solution Explorer** window, right-click **OrderConsumer**, and select **Set as a Startup Project**.

### Add the Event Hubs NuGet package

1. Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.

1. In the **Package Manager Console** window, confirm that **OrderConsumer** is selected for the **Default project**. If not, use the dropdown list to select **OrderConsumer**.

1. Run the following command to install the required NuGet packages. Press **ENTER** to run the last command.

```cmd

Install-Package Azure.Messaging.EventHubs

Install-Package Azure.Messaging.EventHubs.Processor

Install-Package Azure.Identity

Install-Package Microsoft.Azure.Data.SchemaRegistry.ApacheAvro

Install-Package Azure.ResourceManager.Compute

```

1. Authenticate producer applications to connect to Azure by using Visual Studio, as shown in [Azure Identity client library for .NET](/dotnet/api/overview/azure/identity-readme#authenticate-via-visual-studio).

1. Sign-in to Azure using the user account that's a member of the `Schema Registry Reader` role at the namespace level. For information about schema registry roles, see [Azure role-based access control](schema-registry-concepts.md#azure-role-based-access-control).

1. Add the `Order.cs` file you generated as part of creating the producer app to the **OrderConsumer** project.

1. Right-click **OrderConsumer** project, and select **Set as Startup project**.

### Write code to receive events and deserialize them using Schema Registry

1. Add the following code to the `Program.cs` file. See the code comments for details. High-level steps in the code are:

1. Create a consumer client that you can use to send events to an event hub.

1. Create a blob container client for the blob container in the  Azure blob storage.

1. Create an event processor client and register event and error handlers.

1. In the event handler, create a schema registry client that you can use to deserialize event data into an `Order` object.

1. Deserialize the event data into an `Order` object using the serializer.

1. Print the information about the received order.

```csharp

using Azure.Data.SchemaRegistry;

using Azure.Identity;

using Microsoft.Azure.Data.SchemaRegistry.ApacheAvro;

using Azure.Storage.Blobs;

using Azure.Messaging.EventHubs;

using Azure.Messaging.EventHubs.Consumer;

using Azure.Messaging.EventHubs.Processor;

using Microsoft.Azure.Data.SchemaRegistry.example;

// connection string to the Event Hubs namespace

const string connectionString = "EVENTHUBSNAMESPACECONNECTIONSTRING";

// name of the event hub

const string eventHubName = "EVENTHUBNAME";

// Schema Registry endpoint

const string schemaRegistryEndpoint = "EVENTHUBSNAMESPACENAME.servicebus.windows.net";

// name of the consumer group

const string schemaGroup = "SCHEMAGROUPNAME";

// connection string for the Azure Storage account

const string blobStorageConnectionString = "AZURESTORAGECONNECTIONSTRING";

// name of the blob container that will be used as a checkpoint store

const string blobContainerName = "BLOBCONTAINERNAME";

// Create a blob container client that the event processor will use

BlobContainerClient storageClient = new BlobContainerClient(blobStorageConnectionString, blobContainerName);

// Create an event processor client to process events in the event hub

EventProcessorClient processor = new EventProcessorClient(storageClient, EventHubConsumerClient.DefaultConsumerGroupName, connectionString, eventHubName);

// Register handlers for processing events and handling errors

processor.ProcessEventAsync += ProcessEventHandler;

processor.ProcessErrorAsync += ProcessErrorHandler;

// Start the processing

await processor.StartProcessingAsync();

// Wait for 30 seconds for the events to be processed

await Task.Delay(TimeSpan.FromSeconds(30));

// Stop the processing

await processor.StopProcessingAsync();

static async Task ProcessEventHandler(ProcessEventArgs eventArgs)

{

// Create a schema registry client that you can use to serialize and validate data.

var schemaRegistryClient = new SchemaRegistryClient(schemaRegistryEndpoint, new DefaultAzureCredential());

// Create an Avro object serializer using the Schema Registry client object.

var serializer = new SchemaRegistryAvroSerializer(schemaRegistryClient, schemaGroup, new SchemaRegistryAvroSerializerOptions { AutoRegisterSchemas = true });

// Deserialized data in the received event using the schema

Order sampleOrder = (Order)await serializer.DeserializeAsync(eventArgs.Data, typeof(Order));

// Print the received event

Console.WriteLine($"Received order with ID: {sampleOrder.id}, amount: {sampleOrder.amount}, description: {sampleOrder.description}");

await eventArgs.UpdateCheckpointAsync(eventArgs.CancellationToken);

}

static Task ProcessErrorHandler(ProcessErrorEventArgs eventArgs)

{

// Write details about the error to the console window

Console.WriteLine($"\tPartition '{eventArgs.PartitionId}': an unhandled exception was encountered. This was not expected to happen.");

Console.WriteLine(eventArgs.Exception.Message);

return Task.CompletedTask;

}

```

1. Replace the following placeholder values with the real values.

- `EVENTHUBSNAMESPACE-CONNECTIONSTRING` - connection string for the Event Hubs namespace

- `EVENTHUBNAME` - name of the event hub

- `EVENTHUBSNAMESPACENAME` - name of the Event Hubs namespace

- `SCHEMAGROUPNAME` - name of the schema group

- `AZURESTORAGECONNECTIONSTRING` - connection string for the Azure storage account

- `BLOBCONTAINERNAME` - Name of the blob container

```csharp

// connection string to the Event Hubs namespace

const string connectionString = "EVENTHUBSNAMESPACE-CONNECTIONSTRING";

// name of the event hub

const string eventHubName = "EVENTHUBNAME";

// Schema Registry endpoint

const string schemaRegistryEndpoint = "EVENTHUBSNAMESPACENAME.servicebus.windows.net";

// name of the consumer group

const string schemaGroup = "SCHEMAGROUPNAME";

// Azure storage connection string

const string blobStorageConnectionString = "AZURESTORAGECONNECTIONSTRING";

// Azure blob container name

const string blobContainerName = "BLOBCONTAINERNAME";

```

1. Build the project, and ensure that there are no errors.

1. Run the receiver application.

1. You should see a message that the event hub received the events.

```bash

Received order with ID: 1234, amount: 45.29, description: First sample order.

```

These events are the three events you sent to the event hub earlier by running the sender program.

## Samples

See [Azure Schema Registry Apache Avro client library for .NET](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/schemaregistry/Microsoft.Azure.Data.SchemaRegistry.ApacheAvro).

## Clean up resources

Delete the Event Hubs namespace or delete the resource group that contains the namespace.

## Next step

> [!div class="nextstepaction"]

> [Azure Schema Registry client library for .NET](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/schemaregistry/Azure.Data.SchemaRegistry)


# Event Hubs Dedicated Cluster Create Portal

# Quickstart: Create a Dedicated Azure Event Hubs cluster using Azure portal

Event Hubs clusters offer **single-tenant deployments** for customers with the most demanding streaming needs. This offering has a guaranteed **99.99%** service level agreement (SLA), which is available only in our Dedicated pricing tier. An [Event Hubs cluster](event-hubs-dedicated-overview.md) can ingress millions of events per second with guaranteed capacity and subsecond latency. Namespaces and event hubs created within a cluster include all features of the premium offering and more, but without any ingress limits. The Dedicated offering also includes the popular [Event Hubs Capture](event-hubs-capture-overview.md) feature at no extra cost, allowing you to automatically batch and log data streams to [Azure Blob Storage](../storage/blobs/storage-blobs-introduction.md) or [Azure Data Lake Storage Gen 1](../data-lake-store/data-lake-store-overview.md).

Dedicated clusters are provisioned and billed by **capacity units (CUs)**, a pre-allocated amount of CPU and memory resources. You can purchase up to 10 CUs for a cluster in the Azure portal. If you need a cluster larger than 10 CU, you can submit an Azure support request to scale up your cluster after its creation. In this quickstart, we walk you through creating a 1 CU Event Hubs cluster through the Azure portal.

> [!NOTE]

> - The Dedicated tier isn't available in all regions. Try to create a Dedicated cluster in the Azure portal and see supported regions in the **Location** drop-down list on the **Create Event Hubs Cluster** page.

> - This [Azure portal](https://portal.azure.com) self-serve experience is currently in **preview**. If you have any questions about the Dedicated offering, reach out to the [Event Hubs team](mailto:askeventhubs@microsoft.com).

## Prerequisites

To complete this quickstart, make sure that you have:

- An Azure account. If you don't have one, [purchase an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin. This feature isn't supported with a free Azure account.

- [Visual Studio](https://visualstudio.microsoft.com/vs/) 2017 Update 3 (version 15.3, 26730.01) or later.

- [.NET Standard SDK](https://dotnet.microsoft.com/download), version 2.0 or later.

- [Created a resource group](../event-hubs/event-hubs-create.md#create-a-resource-group).

## Create an Event Hubs Dedicated Cluster

An Event Hubs cluster provides a unique scoping container in which you can create one or more namespaces.

> [!WARNING]

> You won't be able to delete the cluster for at least 4 hours after you create it. Therefore, you're charged for a minimum 4 hours of usage of the cluster. For more information on pricing, see [Event Hubs - Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).

To create a cluster in your resource group using the Azure portal, complete the following steps:

1. Follow [this link](https://portal.azure.com) to create a cluster on Azure portal. Conversely, select **All services** from the left navigation pane, then type in **Event Hubs Clusters** in the search bar and select **Event Hubs Clusters** from the list of results.

1. On the **Event Hubs Clusters** page, select **+ Create** on the toolbar.

1. On the **Create Cluster** page, configure the following settings:

1. Enter a **name for the cluster**. The system immediately checks to see if the name is available.

2. Select the **subscription** in which you want to create the cluster.

3. Select the **resource group** in which you want to create the cluster.

1. Notice that the **Support Scaling** option is set to **Enabled**.

1. Select a **location** for the cluster. If your preferred region is grayed out or it's temporarily out of capacity. Submit a [support request](#submit-a-support-request) to the Event Hubs team for further assistance.

1. For **Capacity units**, move the slider to set the number or CUs. The minimum value is 1 and the maximum value is 10.

1. Select the **Next: Tags** button at the bottom of the page. You might have to wait a few minutes for the system to fully provision the resources.

3. On the **Tags** page, configure the following:

1. Enter a **name** and a **value** for the tag you want to add. This step is **optional**.

2. Select the **Review + Create** button.

> [!IMPORTANT]

> You won't be able to delete the cluster for at least 4 hours after you create it. Therefore, you're charged for a minimum 4 hours of usage of the cluster. For more information on pricing, see [Event Hubs - Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).

1. On the **Review + Create** page, review the details, and select **Create**.

5. After the creation is successful, select **Go to resource** to navigate to the home page for your Event Hubs cluster.

## Create a namespace and event hub within a cluster

1. To create a namespace within a cluster, on the **Event Hubs Cluster** page for your cluster, select **+Namespace** from the top menu.

2. On the **Create a namespace** page, do the following steps:

1. Enter a **name for the namespace**.  The system checks to see if the name is available.

2. The namespace inherits the following properties:

1. Subscription ID

2. Resource Group

3. Location

4. Cluster Name

3. Select **Create** to create the namespace. Now you can manage your cluster.

3. Once your namespace is created, you can [create an event hub](event-hubs-create.md#create-an-event-hub) as you would normally create one within a namespace.

## Scale a Dedicated cluster

For clusters created with the **Support Scaling** option set, use the following steps to scale out or scale in your cluster.

1. On the **Event Hubs Cluster** page for your Dedicated cluster, select **Scale** on the left menu.

1. Use the slider to increase (scale out) or decrease (scale in) capacity units assigned to the cluster.

1. Then, select **Save** on the command bar.

The **Scale** tab is available only for the Event Hubs clusters created with the **Support scaling** option checked. You don't see the **Scale** tab for clusters that were created before this feature was released or for the clusters you created without selecting the **Support scaling** option. If you wish to change the size of a cluster that you can't scale yourself, or if your preferred region isn't available, submit a support request by using the following steps.

### Submit a support request

1. In [Azure portal](https://portal.azure.com), select **Help + support** from the left menu.

2. Select **Create a support request** on the toolbar.

3. On the support page, follow these steps:

1. For **Issue Type**, select **Technical** from the drop-down list.

2. For **Subscription**, select your subscription.

3. For **Service**, select **My services**, and then select **Event Hubs**.

4. For **Resource**, select your cluster if it exists already, otherwise select **General Question/Resource Not Available**.

5. For **Problem type**, select **Quota or Configuration changes**.

6. For **Problem subtype**, select one of the following values from the drop-down list:

1. Select **Dedicated Cluster SKU requests** to request for the feature to be supported in your region.

2. Select **Scale up or down a Dedicated Cluster** if you want to scale up or scale down your Dedicated cluster.

7. For **Subject**, describe the issue.

![Support ticket page](./media/event-hubs-dedicated-cluster-create-portal/support-ticket.png)

## Delete a Dedicated cluster

1. To delete the cluster, select **Delete** from the toolbar on the **Event Hubs Cluster** page for your cluster.

> [!IMPORTANT]

> You won't be able to delete the cluster for at least 4 hours after you create it. Therefore, you're charged for a minimum 4 hours of usage of the cluster. For more information on pricing, see [Event Hubs - Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).

1. A message appears confirming your wish to delete the cluster.

1. Type the **name of the cluster** and select **Delete** to delete the cluster.

![Delete cluster page](./media/event-hubs-dedicated-cluster-create-portal/delete-cluster-page.png)

## Next steps

In this article, you created an Event Hubs cluster. For step-by-step instructions to send and receive events from an event hub, and capture events to an Azure storage or Azure Data Lake Store, see the following tutorials:

- Send and receive events

- [.NET Core](event-hubs-dotnet-standard-getstarted-send.md)

- [Java](event-hubs-java-get-started-send.md)

- [Python](event-hubs-python-get-started-send.md)

- [JavaScript](event-hubs-node-get-started-send.md)

- [Use Azure portal to enable Event Hubs Capture](event-hubs-capture-enable-through-portal.md)

- [Use Azure Event Hubs for Apache Kafka](azure-event-hubs-apache-kafka-overview.md)


# Event Hubs Kafka Stream Analytics

# Tutorial: Process Apache Kafka for Event Hubs events using Stream analytics

This article shows how to stream data into Event Hubs and process it with Azure Stream Analytics. It walks you through the following steps:

1. Create an Event Hubs namespace.

2. Create a Kafka client that sends messages to the event hub.

3. Create a Stream Analytics job that copies data from the event hub into an Azure blob storage.

You don't need to change your protocol clients or run your own clusters when you use the Kafka endpoint exposed by an event hub. Azure Event Hubs supports [Apache Kafka version 1.0.](https://kafka.apache.org/10/documentation.html) and above.

## Prerequisites

To complete this quickstart, make sure you have the following prerequisites:

* An Azure subscription. If you don't have one, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

* [Java Development Kit (JDK) 1.7+](/azure/developer/java/fundamentals/java-support-on-azure).

* [Download](https://maven.apache.org/download.cgi) and [install](https://maven.apache.org/install.html) a Maven binary archive.

* [Git](https://www.git-scm.com/)

* An **Azure Storage account**. If you don't have one, [create one](../storage/common/storage-account-create.md) before proceeding further. The Stream Analytics job in this walkthrough stores the output data in an Azure blob storage.

## Create an Event Hubs namespace

When you create an Event Hubs namespace, the Kafka endpoint for the namespace is automatically enabled. You can stream events from your applications that use the Kafka protocol into event hubs. Follow step-by-step instructions in the [Create an event hub using Azure portal](event-hubs-create.md) to create an Event Hubs namespace. If you're using a dedicated cluster, see [Create a namespace and event hub in a dedicated cluster](event-hubs-dedicated-cluster-create-portal.md#create-a-namespace-and-event-hub-within-a-cluster).

> [!NOTE]

> Event Hubs for Kafka isn't supported in the **basic** tier.

## Send messages with Kafka in Event Hubs

1. Clone the [Azure Event Hubs for Kafka repository](https://github.com/Azure/azure-event-hubs-for-kafka) to your machine.

2. Navigate to the folder: `azure-event-hubs-for-kafka/quickstart/java/producer`.

4. Update the configuration details for the producer in `src/main/resources/producer.config`. Specify the **name** and **connection string** for the **event hub namespace**.

```xml

bootstrap.servers={EVENT HUB NAMESPACE}.servicebus.windows.net:9093

security.protocol=SASL_SSL

sasl.mechanism=PLAIN

sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{CONNECTION STRING for EVENT HUB NAMESPACE}";

```

5. Navigate to `azure-event-hubs-for-kafka/quickstart/java/producer/src/main/java/`, and open **TestDataReporter.java** file in an editor of your choice.

6. Comment out the following line of code:

```java

//final ProducerRecord<Long, String> record = new ProducerRecord<Long, String>(TOPIC, time, "Test Data " + i);

```

3. Add the following line of code in place of the commented code:

```java

final ProducerRecord<Long, String> record = new ProducerRecord<Long, String>(TOPIC, time, "{ \"eventData\": \"Test Data " + i + "\" }");

```

This code sends the event data in **JSON** format. When you configure input for a Stream Analytics job, you specify JSON as the format for the input data.

7. **Run the producer** and stream into Event Hubs. On a Windows machine, when using a **Node.js command prompt**, switch to the `azure-event-hubs-for-kafka/quickstart/java/producer` folder before running these commands.

```shell

mvn clean package

mvn exec:java -Dexec.mainClass="TestProducer"

```

## Verify that event hub receives the data

1. Select **Event Hubs** under **ENTITIES**. Confirm that you see an event hub named **test**.

![Event hub - test](./media/event-hubs-kafka-stream-analytics/test-event-hub.png)

2. Confirm that you see messages coming in to the event hub.

![Event hub - messages](./media/event-hubs-kafka-stream-analytics/confirm-event-hub-messages.png)

## Process event data using a Stream Analytics job

In this section, you create an Azure Stream Analytics job. The Kafka client sends events to the event hub. You create a Stream Analytics job that takes event data as input and outputs it to an Azure blob storage. If you don't have  an **Azure Storage account**, [create one](../storage/common/storage-account-create.md).

The query in the Stream Analytics job passes through the data without performing any analytics. You can create a query that transforms the input data to produce output data in a different format or with gained insights.

### Create a Stream Analytics job

1. Select **+ Create a resource** in the [Azure portal](https://portal.azure.com).

2. Select **Analytics** in the **Azure Marketplace** menu, and select **Stream Analytics job**.

3. On the **New Stream Analytics** page, do the following actions:

1. Enter a **name** for the job.

2. Select your **subscription**.

3. Select **Create new** for the **resource group** and enter the name. You can also **use an existing** resource group.

4. Select a **location** for the job.

5. Select **Create** to create the job.

![New Stream Analytics job](./media/event-hubs-kafka-stream-analytics/new-stream-analytics-job.png)

### Configure job input

1. In the notification message, select **Go to resource** to see the **Stream Analytics job** page.

2. Select **Inputs** in the **JOB TOPOLOGY** section on the left menu.

3. Select **Add stream input**, and then select **Event Hub**.

![Add event hub as an input](./media/event-hubs-kafka-stream-analytics/select-event-hub-input.png)

4. On the **Event Hub input** configuration page, do the following actions:

1. Specify an **alias** for the input.

2. Select your **Azure subscription**.

3. Select the **event hub namespace** your created earlier.

4. Select **test** for the **event hub**.

5. Select **Save**.

![Event hub input configuration](./media/event-hubs-kafka-stream-analytics/event-hub-input-configuration.png)

### Configure job output

1. Select **Outputs** in the **JOB TOPOLOGY** section on the menu.

2. Select **+ Add** on the toolbar, and select **Blob storage**

3. On the Blob storage output settings page, do the following actions:

1. Specify an **alias** for the output.

2. Select your Azure **subscription**.

3. Select your **Azure Storage account**.

4. Enter a **name for the container** that stores the output data from the Stream Analytics query.

5. Select **Save**.

![Blob Storage output configuration](./media/event-hubs-kafka-stream-analytics/output-blob-settings.png)

### Define a query

After you have a Stream Analytics job setup to read an incoming data stream, the next step is to create a transformation that analyzes data in real time. You define the transformation query by using [Stream Analytics Query Language](/stream-analytics-query/stream-analytics-query-language-reference). In this walkthrough, you define a query that passes through the data without performing any transformation.

1. Select **Query**.

2. In the query window, replace `[YourOutputAlias]` with the output alias you created earlier.

3. Replace `[YourInputAlias]` with the input alias you created earlier.

4. Select **Save** on the toolbar.

![Screen capture shows the query window with values for input and output variables.](./media/event-hubs-kafka-stream-analytics/query.png)

### Run the Stream Analytics job

1. Select **Overview** on the left menu.

2. Select **Start**.

![Start menu](./media/event-hubs-kafka-stream-analytics/start-menu.png)

1. On the **Start job** page, select **Start**.

![Start job page](./media/event-hubs-kafka-stream-analytics/start-job-page.png)

1. Wait until the status of the job changes from **Starting** to **running**.

![Job status - running](./media/event-hubs-kafka-stream-analytics/running.png)

## Test the scenario

1. Run the **Kafka producer** again to send events to the event hub.

```shell

mvn exec:java -Dexec.mainClass="TestProducer"

```

1. Confirm that you see **output data** is generated in the **Azure blob storage**. You see a JSON file in the container with 100 rows that look like the following sample rows:

```

{"eventData":"Test Data 0","EventProcessedUtcTime":"2018-08-30T03:27:23.1592910Z","PartitionId":0,"EventEnqueuedUtcTime":"2018-08-30T03:27:22.9220000Z"}

{"eventData":"Test Data 1","EventProcessedUtcTime":"2018-08-30T03:27:23.3936511Z","PartitionId":0,"EventEnqueuedUtcTime":"2018-08-30T03:27:22.9220000Z"}

{"eventData":"Test Data 2","EventProcessedUtcTime":"2018-08-30T03:27:23.3936511Z","PartitionId":0,"EventEnqueuedUtcTime":"2018-08-30T03:27:22.9220000Z"}

```

The Azure Stream Analytics job received input data from the event hub and stored it in the Azure blob storage in this scenario.

## Next steps

In this article, you learned how to stream into Event Hubs without changing your protocol clients or running your own clusters. To learn more about Event Hubs for Apache Kafka, see [Apache Kafka developer guide for Azure Event Hubs](apache-kafka-developer-guide.md).


# Event Hubs Data Explorer

# Send and view events with Event Hubs Data Explorer

Event Hubs Data Explorer is a portal-based tool for sending test events to and viewing events from an Azure event hub. Developers and operators can use it to test end-to-end flows or inspect events at specific offsets for debugging - without writing custom client applications.

This article shows you how to use Data Explorer to send events (custom payloads or precanned datasets) and view events from your event hub.

You can perform two kinds of operations on an Azure Event Hubs namespace:

- **Management operations**: Create, update, and delete Event Hubs namespaces and event hubs.

- **Data operations**: Send and view events from an event hub.

> [!IMPORTANT]

> - If your Event Hubs namespace is accessible only through a private endpoint, access Event Hubs Data Explorer from a virtual machine in the same virtual network as the private endpoint. This configuration ensures that the web browser has required access to the private endpoint.

> - Event Hubs Data Explorer doesn't support management operations. You must create the event hub before you can use the data explorer to send or view events.

> - The data explorer shows event payloads (known as *values* in Kafka) sent by using the Kafka protocol, but it doesn't show the *key* for the specific event.

> - Don't use Event Hubs Data Explorer for larger messages, because it can result in timeouts depending on the message size and network latency between client and Event Hubs service. Instead, use your own client to work with larger messages so you can specify your own timeout values.

> - The [role-based access control (RBAC)](authorize-access-azure-active-directory.md#azure-built-in-roles-for-azure-event-hubs) role assigned to a user determines the operations that the user can perform by using Event Hubs Data Explorer.

## Prerequisites

To use Event Hubs Data Explorer, [create an Azure Event Hubs namespace and an event hub](event-hubs-create.md).

## Launch Event Hubs Data Explorer

Launch Event Hubs Data Explorer from the Azure portal using one of the following methods:

- On the Azure portal, go to your Event Hubs namespace, select **Data Explorer** from the left menu, and then select the **event hub**.

- Alternatively, go to your Event Hubs namespace, and follow these steps:

- Select **Event Hubs** under **Entities**, and then select the event hub you want to explore.

- On the **Event Hubs instance** page, select **Data Explorer** from the left menu.

## Send events

You can send either custom payloads or precanned datasets to the selected event hub by using the **Send events** experience.

To do so, select **Send events**, which opens the right pane.

### Send a custom payload

To send a custom payload:

1. For **Select Dataset**, select **Custom payload**. You can also select precanned datasets such as Yellow Taxi data or Weather data, as shown in the next section.

1. For **Content-Type**, select **Text/Plain**, **XML**, **JSON**, **AVRO**, or **Raw**.

1. Either upload a file or enter the payload in the **Enter payload** box.

1. (Optional) Specify system properties.

1. (Optional) Specify custom properties, which are available as key-value pairs.

1. (Optional) If you want to send multiple payloads, select the **Repeat send** checkbox and specify the **Repeat send count** (the number of payloads to send) and **Interval between repeat send in ms**.

After you define the payload details, select **Send** to send the event payload.

### Send a precanned dataset

To send event payloads from a precanned dataset:

1. For **Select Dataset**, select an option from the **Precanned datasets**, such as Yellow taxi or Weather data.

1. (Optional) Specify system properties.

1. (Optional) Specify custom properties, which are available as key-value pairs.

1. (Optional) If you want to send multiple payloads, select the **Repeat send** checkbox and specify the **Repeat send count** (the number of payloads to send) and **Interval between repeat send in ms**.

1. After you define the payload details, select **Send** to send the event payload.

## View events

Event Hubs Data Explorer enables you to view events so you can inspect data that matches your criteria.

To view events, define the following properties or rely on the default settings:

1. **PartitionID**: Select either a specific partition or **All partition IDs**.

1. **Consumer Group**: Select **$Default** or another consumer group, or create one.

1. **Event position**: Select **Oldest position** (the start of the event hub), **Newest position** (the latest event), or **Custom position** (for a specific offset, sequence number, or timestamp).

1. **Oldest position**: Begin receiving events from the first event in the partition that isn't expired due to the retention policy.

1. **Custom position**: Add a filter to specify the position in the partition to begin receiving events from.

1. **Newest position**: Begin receiving events from the event that's enqueued right after the view call. Only events sent after the last viewing of events are received.

1. **Advanced properties**: Specify the **Maximum batch size** and **Maximum wait time in seconds**.

After you set the options, select **View events** to pull the events and display them in the data explorer.

After the events load, you can select **View next events** to pull events by using the same query again, or select **Clear all** to refresh the grid.

### Download event payload

When you view events on a given event hub, you can download the event payload for further review.

To download the event payload, select the specific event, and then select the **Download** button that appears above the event payload body.

## Related content

- [What is Azure Event Hubs?](event-hubs-about.md)

- [Event Hubs features and terminology](event-hubs-features.md)


# Event Hubs Samples

# Git repositories with samples for Azure Event Hubs

You can find Event Hubs samples on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples). These samples demonstrate key features in [Azure Event Hubs](./index.yml). This article categorizes and describes the samples available, with links to each.

## .NET samples

| Version | Samples location |

| ------- | ---------------- |

| Azure.Messaging.EventHubs version 5 (latest) | [Event Hubs samples on GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/eventhub/Azure.Messaging.EventHubs/samples)<br/>[Event Hubs Processor samples on GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/eventhub/Azure.Messaging.EventHubs.Processor/samples) |

| Azure.ResourceManager.EventHubs | [Management samples on GitHub](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/eventhub/Azure.ResourceManager.EventHubs/samples) |

## Java samples

| Version | Samples location |

| ------- | ---------------- |

| azure-messaging-eventhubs version 5 (latest) | [GitHub location](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/eventhubs/azure-messaging-eventhubs/src/samples/java/com/azure/messaging/eventhubs) |

## Spring samples

| Version                                        | Samples location |

| ------- | ---------------- |

| spring-cloud-azure-starter-eventhubs version 4 | [GitHub location](https://github.com/Azure-Samples/azure-spring-boot-samples/tree/main/eventhubs/spring-cloud-azure-starter-eventhubs/eventhubs-client) |

| spring-cloud-azure-starter-integration-eventhubs version 4 | [GitHub location](https://github.com/Azure-Samples/azure-spring-boot-samples/tree/main/eventhubs/spring-cloud-azure-starter-integration-eventhubs/eventhubs-integration) |

| spring-cloud-azure-stream-binder-eventhubs version 4 | [GitHub location](https://github.com/Azure-Samples/azure-spring-boot-samples/tree/main/eventhubs/spring-cloud-azure-stream-binder-eventhubs) |

## Python samples

| Version | Samples location |

| ------- | ---------------- |

| azure-eventhub version 5 (latest) | [GitHub location](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/eventhub/azure-eventhub/samples) |

## JavaScript samples

| Version | Samples location |

| ------- | ---------------- |

| azure/event-hubs version 5 (latest) | [GitHub location](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/eventhub/event-hubs/samples) |

## Go samples

You can find Go samples for Azure Event Hubs in the [azeventhubs](https://github.com/Azure/azure-sdk-for-go/tree/main/sdk/messaging/azeventhubs) folder in the [azure-sdk-for-go](https://github.com/Azure/azure-sdk-for-go/) GitHub repository.

## Azure CLI samples

You can find Azure CLI samples for Azure Event Hubs in the [azure-event-hubs](https://github.com/Azure/azure-event-hubs/tree/master/samples/Management/CLI) GitHub repository.

## Azure PowerShell samples

You can find Azure PowerShell samples for Azure Event Hubs in the [azure-event-hubs](https://github.com/Azure/azure-event-hubs/tree/master/samples/Management/PowerShell) GitHub repository.

## Apache Kafka samples

You can find samples for the Event Hubs for Apache Kafka feature in the [azure-event-hubs-for-kafka](https://github.com/Azure/azure-event-hubs-for-kafka) GitHub repository.

## Next steps

You can learn more about Event Hubs in the following articles:

- [Event Hubs overview](./event-hubs-about.md)

- [Event Hubs features](event-hubs-features.md)

- [Event Hubs FAQ](event-hubs-faq.yml)


# Event Hubs Capture Overview

# Capture events through Azure Event Hubs in Azure Blob Storage or Azure Data Lake Storage

The Azure Event Hubs Capture feature automatically captures streaming data that flows through Event Hubs to an [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Storage](https://azure.microsoft.com/services/data-lake-store/) account. To control when Event Hubs stores the data, you can specify a time or a size interval. You can quickly enable or set up the Event Hubs Capture feature. It doesn't require administrative costs to run, and it scales automatically with Event Hubs capacity.

The Standard tier uses [throughput units](event-hubs-scalability.md#throughput-units), and the Premium tier uses [processing units](event-hubs-scalability.md#processing-units). Event Hubs Capture simplifies the process of loading streaming data into Azure and enables you to focus on data processing rather than data capture.

Use Event Hubs Capture to process real-time and batch-based pipelines on the same stream. This approach helps you build solutions that grow with your needs over time. If you use batch-based systems and plan to add real-time processing later, or if you want to add an efficient cold path to an existing real-time solution, Event Hubs Capture simplifies working with streaming data.

## Important points to consider

- The destination storage account, either Blob Storage or Data Lake Storage, must reside in the same subscription as the event hub when you don't use managed identity for authentication.

- Event Hubs doesn't support capturing events in premium Azure Storage accounts.

- Event Hubs Capture supports nonpremium Storage accounts that allow block blobs.

## How Event Hubs Capture works

Event Hubs serves as a time-retention durable buffer for telemetry ingress, similar to a distributed log. The [partitioned consumer model](event-hubs-scalability.md#partitions) enables scalability. Each partition is an independent segment of data and is consumed independently. This data is deleted after the configurable retention period, so the event hub never gets *too full*.

Event Hubs Capture enables you to specify a Blob Storage account and container, or a Data Lake Storage account, to store captured data. These accounts can reside in the same region as your event hub or in another region, which adds flexibility.

Event Hubs Capture writes captured data in [Apache Avro](https://avro.apache.org/) format, which is a compact, fast, binary format that provides rich data structures with inline schema. The Hadoop ecosystem, Azure Stream Analytics, and Azure Data Factory use this format. Later sections in this article provide more information about working with Avro.

> [!NOTE]

> - When you use the no-code editor in the Azure portal, you can capture streaming data in Event Hubs to a Data Lake Storage account in the Parquet format. For more information, see [Capture data from Event Hubs in Parquet format](../stream-analytics/capture-event-hub-data-parquet.md) and [Capture Event Hubs data in Parquet format and analyze it by using Azure Synapse Analytics](../stream-analytics/event-hubs-parquet-capture-tutorial.md).

>

> - To configure Event Hubs Capture with Data Lake Storage, follow the same steps as configuring it with Blob Storage. For more information, see [Configure Event Hubs Capture](event-hubs-capture-enable-through-portal.md).

>

> - Data Lake Storage Gen1 is retired and no longer supported for Event Hubs Capture. If you use Gen1, migrate to Gen2 to ensure compatibility and continued support.

### Capture windowing

To control capturing, use Event Hubs Capture to set up a window that uses a minimum size and time configuration. The system applies a *first wins* policy, which means that the first condition met—either size or time—triggers the capture. For example, if you have a fifteen-minute, 100-megabyte (MB) capture window and send 1 MB per second, the size window triggers before the time window.

Each partition captures data independently and writes a completed block blob at the time of capture. The blob name reflects the time when the capture interval was encountered.

The storage naming convention follows this structure:

```

{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}

```

The date values are padded with zeroes. The following filename shows an example:

```

https://mystorageaccount.blob.core.windows.net/mycontainer/mynamespace/myeventhub/0/2017/12/08/03/03/17.avro

```

If your Storage blob becomes temporarily unavailable, Event Hubs Capture retains your data for the data retention period that you configure on your event hub. After your Storage account becomes available again, Event Hubs Capture backfills the data.

### Scale throughput units or processing units

In the Standard tier of Event Hubs, [throughput units](event-hubs-scalability.md#throughput-units) control traffic. In the Premium tier, [processing units](event-hubs-scalability.md#processing-units) control traffic. Event Hubs Capture copies data directly from the internal Event Hubs storage, which bypasses throughput unit or processing unit egress quotas and saves your egress for other processing readers such as Stream Analytics or Apache Spark.

After you configure Event Hubs Capture, it starts automatically when you send your first event and continues running. To help downstream systems confirm that the process works, Event Hubs writes empty files when no data is available. This process provides a predictable cadence and marker that can feed your batch processors.

## Set up Event Hubs Capture

To configure Capture when you create an event hub, use the [Azure portal](https://portal.azure.com) or an Azure Resource Manager template (ARM template). For more information, see the following articles:

- [Enable Event Hubs Capture by using the Azure portal](event-hubs-capture-enable-through-portal.md)

- [Create an Event Hubs namespace that includes an event hub and enable Capture by using an ARM template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

> [!NOTE]

> If you enable the Capture feature for an existing event hub, the feature captures only the events that arrive *after* you turn it on. It doesn't capture events that exist before activation.

## Event Hubs Capture billing

The Event Hubs Premium tier includes the Capture feature. For the Standard tier, Azure charges for Capture monthly based on the number of throughput units for the namespace. As you scale throughput units up or down, Event Hubs Capture adjusts its metering to match performance. These meters scale in tandem.

Capture doesn't consume egress quota because Azure bills it separately.

For more information, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).

## Integrate with Azure Event Grid

You can create an Azure Event Grid subscription with an Event Hubs namespace as its source. For more information about how to create an Event Grid subscription with an event hub as a source and an Azure Functions app as the sink, see [Migrate captured Event Hubs data to Azure Synapse Analytics](../event-grid/event-hubs-integration.md).

## Explore captured files

To learn how to explore captured Avro files, see [Explore captured Avro files](explore-captured-avro-files.md).

## Azure Storage account as a destination

To enable Capture on an event hub that uses Storage as the capture destination, or to update properties on an event hub that uses Storage as the capture destination, the user or service principal must have a role-based access control (RBAC) role that includes the following permissions assigned at the storage account scope:

```

Microsoft.Storage/storageAccounts/blobServices/containers/write

Microsoft.Storage/storageAccounts/blobServices/containers/blobs/write

```

Without this permission, the following error appears:

```

Generic: Linked access check failed for capture storage destination <StorageAccount Arm Id>.

User or the application with object id <Object Id> making the request doesn't have the required data plane write permissions.

Please enable Microsoft.Storage/storageAccounts/blobServices/containers/write, Microsoft.Storage/storageAccounts/blobServices/containers/blobs/write permission(s) on above resource for the user or the application and retry.

TrackingId:<ID>, SystemTracker:mynamespace.servicebus.windows.net:myhub, Timestamp:<TimeStamp>

```

To resolve this problem, add the user account or the service principal to the [Storage Blob Data Owner](../role-based-access-control/built-in-roles.md#storage-blob-data-owner) built-in role, which includes the required permissions.

## Related content

Event Hubs Capture provides a straightforward way to ingest data into Azure. With Data Lake Storage, Azure Data Factory, and Azure HDInsight, you can perform batch processing and analytics by using familiar tools and platforms at any scale.

To enable this feature, use the Azure portal or an ARM template:

- [Use the Azure portal to enable Event Hubs Capture](event-hubs-capture-enable-through-portal.md)

- [Use an ARM template to enable Event Hubs Capture](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

For more information about data redundancy options for your Capture destination storage account, see [Reliability in Blob Storage](/azure/reliability/reliability-storage-blob).


# Event Hubs Capture Managed Identity

# Authenticate modes for capturing events to destinations in Azure Event Hubs

Azure Event Hubs allows you to select different authentication modes when capturing events to a destination such as [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Storage Gen 1 or Gen 2](https://azure.microsoft.com/services/data-lake-store/) account of your choice. The authentication mode determines how the capture agent running in Event Hubs authenticate with the capture destination.

## Prerequisites

1. Enable system-assigned or user-assigned managed identity by following instructions from the article: [Enable a managed identity for an Event Hubs namespace](enable-managed-identity.md). After you enable an identity for a namespace, you can use the identity when configuring the Capture feature for an event hub in the namespace.

1. On the target Azure Storage or Data Lake Store account, use the **Access control** page, and add this managed identity to the **Storage Blob Data Contributor** role.

## Use managed identity to capture events

[Managed identity](../active-directory/managed-identities-azure-resources/overview.md) is the preferred way to seamlessly access the capture destination from your event hub, using Microsoft Entra ID based authentication and authorization.

You can use system-assigned or user-assigned managed identities with Event Hubs Capture destinations.

## Use a system-assigned managed identity

System-assigned Managed Identity is automatically created and associated with an Azure resource, which is an Event Hubs namespace in this case.

To use system assigned identity, the capture destination must have the required role assignment enabled for the corresponding system assigned identity.

Then you can select `System Assigned` managed identity option when enabling the capture feature in an event hub.

Then capture agent would use the identity of the namespace for authentication and authorization with the capture destination.

### Use a user-assigned managed identity

You can create a user-assigned managed identity and use it for authenticate and authorize with the capture destination of Event hubs. Once the managed identity is created, you can assign it to the Event Hubs namespace and make sure that the capture destination has the required role assignment enabled for the corresponding user assigned identity.

Then you can select `User Assigned` managed identity option when enabling the capture feature in an event hub and assign the required user assigned identity when enabling the capture feature.

Then capture agent would use the configured user assigned identity for authentication and authorization with the capture destination.

#### Capturing events to a capture destination in a different subscription

The Event Hubs Capture feature also support capturing data to a capture destination in a different subscription with the use of managed identity.

> [!IMPORTANT]

> To enable capture with a storage account in a different subscription, the **Microsoft.EventHub Resource Provider must be registered for the subscription** which owns the storage account.

>

> To learn more about registering a Resource Provider with a specific Azure Subscription, refer to the [documentation](../azure-resource-manager/management/resource-providers-and-types.md#register-resource-provider).

>

You may use the portal or use the ARM templates in [guide](./event-hubs-resource-manager-namespace-event-hub-enable-capture.md) with corresponding managed identity.

## Related content

Learn more about the feature and how to enable it using the Azure portal and Azure Resource Manager template:

- [Capture events through Azure Event Hubs in Azure Blob Storage or Azure Data Lake Storage](event-hubs-capture-overview.md)

- [Use the Azure portal to enable Event Hubs Capture](event-hubs-capture-enable-through-portal.md)

- [Use an Azure Resource Manager template to enable Event Hubs Capture](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)


# Explore Captured Avro Files

# Exploring captured Avro files in Azure Event Hubs

This article provides the schema for Avro files captured by Azure Event Hubs and a few tools to explore the files.

## Schema

The Avro files produced by Event Hubs Capture have the following Avro schema:

## Azure Storage Explorer

You can verify that captured files were created in the Azure Storage account using tools such as [Azure Storage Explorer][Azure Storage Explorer]. You can download files locally to work on them.

An easy way to explore Avro files is by using the [Avro Tools][Avro Tools] jar from Apache. You can also use [Apache Spark][Apache Spark] to perform complex distributed processing on the ingested data.

## Use Apache Spark

[Apache Spark][Apache Spark] is a "unified analytics engine for large-scale data processing." It supports different languages, including SQL, and can easily access Azure Blob storage. There are a few options to run Apache Spark in Azure, and each provides easy access to Azure Blob storage:

- [HDInsight: Address files in Azure storage][HDInsight: Address files in Azure storage]

- [Azure Databricks: Azure Blob storage][Azure Databricks: Azure Blob Storage]. See the following sample: [Streaming at Scale with Event Hubs Capture](https://github.com/Azure-Samples/streaming-at-scale/tree/main/eventhubs-capture-databricks-delta).

- [Azure Kubernetes Service](/azure/aks/spark-job)

## Use Avro Tools

[Avro Tools][Avro Tools] are available as a jar package. After you download the jar file, you can see the schema of a specific Avro file by running the following command:

```shell

java -jar avro-tools-1.9.1.jar getschema <name of capture file>

```

This command returns

```json

{

"type":"record",

"name":"EventData",

"namespace":"Microsoft.ServiceBus.Messaging",

"fields":[

{"name":"SequenceNumber","type":"long"},

{"name":"Offset","type":"string"},

{"name":"EnqueuedTimeUtc","type":"string"},

{"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},

{"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},

{"name":"Body","type":["null","bytes"]}

]

}

```

You can also use Avro Tools to convert the file to JSON format and perform other processing.

To perform more advanced processing, download and install Avro for your choice of platform. At the time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.

Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python]. You can also read the [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.

## Next steps

Event Hubs Capture is the easiest way to get data into Azure. Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need. See the following articles to learn more about this feature.

- [Event Hubs Capture overview](event-hubs-capture-overview.md)

- [Use the Azure portal to enable Event Hubs Capture](event-hubs-capture-enable-through-portal.md)

- [Use an Azure Resource Manager template to enable Event Hubs Capture](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

[Apache Avro]: https://avro.apache.org/

[Apache Spark]: https://spark.apache.org/

[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade

[Azure Storage Explorer]: https://github.com/microsoft/AzureStorageExplorer/releases

[Avro Tools]: https://downloads.apache.org/avro/stable/java/

[Java]: https://avro.apache.org/docs/1.11.1/getting-started-java/

[Python]: https://avro.apache.org/docs/1.11.1/getting-started-python/

[Event Hubs overview]: ./event-hubs-about.md

[HDInsight: Address files in Azure storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md

[Azure Databricks: Azure Blob Storage]:/azure/databricks/archive/storage/azure-storage

[Streaming at Scale: Event Hubs Capture]:https://github.com/yorek/streaming-at-scale/tree/master/event-hubs-capture


# Log Compaction

# Log compaction in Azure Event Hubs

Log compaction is a way of retaining data in Event Hubs using event key based retention. By default, each event hub/Kafka topic is created with time-based retention or the *delete* cleanup policy, where events are purged upon the expiration of the retention time. Rather using coarser-grained time based retention, you can use event key-based retention mechanism where Event Hubs retains the last known value for each event key of an event hub or a Kafka topic.

> [!NOTE]

> Log compaction feature isn't supported in the **basic** tier.

As shown in the following image, an event log (of an event hub partition) may have multiple events with the same key. If you're using a compacted event hub, then Event Hubs service takes care of purging old events and only keeping the latest events of a given event key.

### Compaction key

The partition key that you set with each event is used as the compaction key.

### Tombstones

Client application can mark existing events of an event hub to be deleted during compaction job. These markers are known as *Tombstones*. Client applications set tombstones by sending a new event with an existing key and a `null` event payload.

## How log compaction works

You can enable log compaction at each event hub/Kafka topic level. You can ingest events to a compacted entity from any supported protocol. Azure Event Hubs service runs a compaction job for each compacted event hub. Compaction job cleans each event hub partition log by only retaining the latest event of a given event key.

At any given time, the event log of a compacted event hub can have a *cleaned* portion and *dirty* portion. The clean portion contains the events that are compacted by the compaction job while the dirty portion comprises the events that are yet to be compacted.

The Event Hubs service manages the execution of the compaction job and user can't control it. Therefore, Event Hubs service determines when to start compaction and how fast it compact a given compacted event hub.

> [!NOTE]

> Event Hubs performs compaction to eliminate event payloads with the same key, but this process is triggered non-deterministically, which can result in multiple event payloads with the same key between compaction job runs.

>

## Compaction guarantees

Log compaction feature of Event Hubs provides the following guarantee:

- Ordering of the messages is always maintained at the key and partition level. Compaction job doesn't alter ordering of messages but it just discards the old events of the same key.

- The sequence number and offset of a message never changes.

- Any consumer progressing from the start of the event log sees at least the final state of all events in the order they were written.

- Consumers can still see events that are marked to be deleted for the time defined by *Tombstone Retention Time(hours)*.

## Log compaction use cases

Log compaction can be useful in scenarios where you stream the same set of updatable events. As compacted event hubs only keep the latest events, users don't need to worry about the growth of the event storage. Therefore log compaction is commonly used in scenarios such as Change Data Capture(CDC), maintaining event in tables for stream processing applications and event caching.

## Quotas and limits

| Limit | Basic | Standard | Premium |  Dedicated |

| ----- | ----- | -------- | -------- | --------- |

| Size of compacted event hub  | N/A | 1 GB per partition | 250 GB per partition | 250 GB per partition |

For other quotas and limits, see [Event Hubs quotas and limits](event-hubs-quotas.md).

## Next steps

For instructions on how to use log compaction in Event Hubs, see [Use log compaction](./use-log-compaction.md)


# Resource Governance Overview

# Resource governance with application groups

Azure Event Hubs enables you to govern event streaming workloads of client applications that connect to Event Hubs. You can create logical groups known as *application groups* where each group is a collection of client applications, and then apply quota and access management policies for an application group (group of client applications).

> [!NOTE]

> Application groups are available only in **premium** and **dedicated** tiers.

## Application groups

An application group is a collection of one or more client applications that interact with the Event Hubs data plane. Each application group can be scoped to a single Event Hubs namespace or event hubs (entity) within a namespace and should use a uniquely identifying condition such as the security context - shared access signatures (SAS) or Microsoft Entra application ID - of the client application.

Event Hubs currently supports using security contexts for creating application groups. Therefore, each application group must have a unique SAS policy or Microsoft Entra application ID associated with them. If preferred, you can use security context at event hub level to use an application group with a specific event hub within a namespace.

Application groups are logical entities that are created at the namespace level. Therefore, client applications interacting with event hubs don't need to be aware of the existence of an application group. Event Hubs can associate any client application to an application group by using the identifying condition.

As illustrated below, you can create application groups based on the security context that each client application uses. Therefore, application groups can span across multiple client applications using the same security context.

Application groups have no direct association with a consumer group. Depending on the application group identifier such as security context, one consumer group can have one or more application groups associated with it or one application group can span across multiple consumer groups.

These are the key attributes of an application group:

| Parameter | Description |

| ---- | ----------- |

| name | Unique name of an application group. |

| clientAppGroupIdentifier | Associate an application group with a uniquely identifying condition (i.e security context such as SAS policy or Microsoft Entra application ID). |

| policies | List of policies, such as throttling policies that control event streaming between client applications and the Event Hubs namespace|

| isEnabled | Determine whether the client applications of an application group can access Event Hubs namespaces or not. |

## Application group policies

Each application group can contain zero or more policies that control the data plane access of the client applications that are part of the application group. Application groups currently support throttling policies.

### Throttling policies

You can have throttling policies specified using different ingress and egress metrics. Application groups support using the following metrics to throttle ingress or egress workloads of client applications.

| Parameter | Description |

| ---- | ----------- |

| IncomingBytes | Publisher throughput in bytes per second. |

| OutgoingBytes | Consumer throughput in bytes per second. |

| IncomingMessages | Number of events published per second. |

| OutgoingMessages | Number of events consumed per second. |

When policies for application groups are applied, the client application workload may slow down or encounter server busy exceptions.

### Throttling policy - threshold Limits

The following table shows minimum threshold limits that you can set for different metric ID in throttling policy:

| Metric ID | Minimum limit |

| --------- | ------------- |

| IncomingByte | 1 KB |

| OutgoingByte | 1 KB |

| IncomingMessage | 1  |

| Outgoing message | 1 |

> [!NOTE]

> Limits set on the throttling policy's threshold value would take precedence over any value set for Kafka topic properties. For example, `IncomingBytes` would have higher priority over `message.max.bytes`.

> Application group throttling is expected to throttle consistent higher than permitted traffic scenarios (spanning across few minutes).Quick bursts in traffic for few seconds might not experience throttling via Application Groups. Looking at permitted throughput over the time horizon of few minutes is recommended approach to validate throttling.

### Protocol support and error codes

Application group supports throttling operations happening via following protocols – AMQP, Kafka and HTTP. The following table provides you the expected error codes returned by application groups:

| Protocol | Operation | Error code  | Error message |

| -------- | --------- | ---------- | ------------- |

| AMQP | Send | 50004 |SubCode:50013, Application group is throttled with application group ID & policy name |

| HTTP | Send | 503 | Subcode: 50013. Application group is throttled with application group ID and policy name  |

| Kafka | Send | PolicyViolation | Broker: policy violation |

Due to restrictions at protocol level, error messages aren't supported during receive operation. When application groups are throttling on receive operations, you would experience sluggish consumption of messages at consumer side.

### Disabling application groups

Application group is enabled by default and that means all the client applications can access Event Hubs namespace for publishing and consuming events by adhering to the application group policies.

When an application group is disabled, the client will still be able to connect to the event hub, but the authorization will fail and then the client connection gets closed. Therefore, you'll see lots of successful open and close connections, with same number of authorization failures in diagnostic logs.

## Next steps

For instructions on how to create and manage application groups, see [Resource governance for client applications using Azure portal](resource-governance-with-app-groups.md)


# Overview Emulator

# Azure Event Hubs emulator overview

The **Azure Event Hubs emulator** is a local development tool designed to help developers test and prototype Event Hubs applications in an offline, cost-effective, and isolated environment. The emulator simulates the Event Hubs service locally, which enables faster development cycles, eliminates cloud-related costs, and provides a controlled testing environment. This article provides an overview of the emulator's benefits, features, limitations, and usage guidelines to help you get started.

## Benefits

The primary advantages of using the emulator are:

- **Local development**: The emulator provides a local development experience, so you can work offline and avoid network latency.

- **Cost efficiency**: With the emulator, you can test your applications without incurring any cloud usage costs.

- **Isolated testing environment**: You can test your code in isolation, to help ensure that other activities in the cloud don't affect the tests.

- **Optimized inner development loop**: You can use the emulator to quickly prototype and test your applications before deploying them to the cloud.

## Features

The emulator provides these features:

- **Containerized deployment**: It runs as a Docker container (Linux based).

- **Cross-platform compatibility**: You can use it on any platform, including Windows, macOS, and Linux.

- **Configurability**: You can manage the number of event hubs, partitions, and other entities by using the JSON supplied configuration.

- **Streaming support**: It supports streaming events using Kafka and Advanced Message Queuing Protocol (AMQP).

- **Observability**: It provides observability features, including console and file logging.

## Known limitations

The current version of the emulator has the following limitations:

- When you use Kafka, only producer and consumer APIs are compatible with Event Hubs emulator.

- Under Kafka configuration, `securityProtocol` and `saslmechanism` can only have the following values:

```

SecurityProtocol = SecurityProtocol.SaslPlaintext,

SaslMechanism = SaslMechanism.Plain

```

- It doesn't support on-the-fly management operations through a client-side SDK.

> [!NOTE]

> After a container restart, data and entities don't persist in the emulator.

## Differences between the emulator and cloud service

Because the Event Hubs emulator is meant only for development and test purposes, there are functional differences between the emulator and the cloud service.

The emulator doesn't support these high-level features:

- Azure features like virtual network integration, Microsoft Entra ID integration, activity logs, and a UI portal

- Event Hubs Capture

- Resource governance features like application groups

- Autoscale capabilities

- Geo-disaster recovery capabilities

- Schema registry integration

- Visual metrics and alerts

> [!NOTE]

> The emulator is intended solely for development and test scenarios. We discourage any kind of production use. We don't provide any official support for the emulator.

>

> Report any problems or suggestions in the emulator's [GitHub installer repository](https://github.com/Azure/azure-event-hubs-emulator-installer/issues).

## Usage quotas

Like Event Hubs on Azure, the emulator provides the following quotas for usage:

| Property| Value| User configurable within limits

| ----|----|----

| Number of supported namespaces| 1 |No

| Maximum number of event hubs in a namespace| 10| Yes

| Maximum number of consumer groups in an event hub| 20 |Yes

| Maximum number of partitions in an event hub |32 |Yes

| Maximum size of an event being published to an event hub (batch/nonbatch) |1 MB |No

| Minimum event retention time | 1 hr | No

Emulator enforces these limits. While some values are configurable using config.json, you can't exceed the listed maximums. Any configuration changes must be made before starting the emulator.

## Quota configuration changes

By default, the emulator runs with the [config.json](https://github.com/Azure/azure-event-hubs-emulator-installer/blob/main/EventHub-Emulator/Config/Config.json) configuration file. You can configure the quotas associated with Event Hubs by editing this file in the following ways, based on your needs:

- **Entities**: You can add more entities (event hubs), with a customized number of partitions and consumer groups, in accordance with supported quotas.

- **Logging**: The emulator supports logging on a console, in a file, or both. You can choose according to your personal preference.

> [!IMPORTANT]

> You must supply any changes in JSON configuration before you run the emulator. Changes aren't honored on the fly. For changes to take effect, you must restart the container.

>

> You can't rename the preset namespace (`name`) in the configuration file.

## Logs for debugging

During testing, console or file logs help you debug unexpected failures. To review the logs:

- **Console logs**: On the Docker desktop UI, select the container name.

- **File logs**: In the container, go to */home/app/EmulatorLogs*.

## Related content

[Test locally by using the Azure Event Hubs emulator](test-locally-with-event-hub-emulator.md)


# Event Hubs Emulator Whats New

# What's new with Event Hubs emulator

This article provides a detailed overview of the enhancements introduced in the latest version of the Azure Event Hubs emulator, along with information about previous versions.

> [!NOTE]

> The emulator is intended solely for development and test purpose. Any kind of production use is strictly discouraged. We don't provide any official support for the emulator.

>

> Kindly report any problems or suggestions in the emulator's [GitHub installer repository](https://github.com/Azure/azure-event-hubs-emulator-installer/issues).

## Latest version ``2.1.0``

> *Released March 11th, 2025*

This release introduces health check API in Event Hubs emulator.

- Health check API can be accessed at *http://localhost:5300/health*

## Previous releases

### ``2.0.1`` (November 19th,2024)

This release introduces Apache Kafka support in Event Hubs emulator.

- The producer and consumer APIs are now compatible with the Event Hubs emulator.

### ``1.2.4`` (July 1st,2024)

This release provides enhanced connectivity fixes for Emulator.

- When the emulator container and interacting application are running natively on local machine, use following connection string:

`"Endpoint=sb://localhost;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=SAS_KEY_VALUE;UseDevelopmentEmulator=true;"`

- Applications (Containerized/Non-containerized) on the different machine and same local network can interact with Emulator using the IPv4 address of the machine. Use following connection string:

`"Endpoint=sb://192.168.y.z;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=SAS_KEY_VALUE;UseDevelopmentEmulator=true;"`

- Application containers on the same bridge network can interact with Emulator using its alias or IP. Following connection string assumes the name of Emulator container is "eventhubs-emulator":

`Endpoint=sb://eventhubs-emulator;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=SAS_KEY_VALUE;UseDevelopmentEmulator=true;"`

- Application containers on the different bridge network can interact with Emulator using the "host.docker.internal" as host. Use following connection string:

`"Endpoint=sb://host.docker.internal;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=SAS_KEY_VALUE;UseDevelopmentEmulator=true;"`

- Fixes emulator not accepting connections for initial few seconds after launch.

- Namespace name and type are now optional parameters in user supplied JSON configuration.

### ``1.2.3`` (21st May,2024)

- Initial Launch

## Next steps

- [Learn more about the Azure Event Hubs emulator](overview-emulator.md)

- [Get started using the Azure Event Hubs emulator for development](test-locally-with-event-hub-emulator.md)


# Event Hubs Premium Overview

# Azure Event Hubs Premium overview

Azure Event Hubs Premium (Premium tier) is designed for high-end streaming scenarios that require elastic, superior performance with predictable latency. The Premium tier provides reserved compute, memory, and storage resources, which minimize cross-tenant interference in a managed multitenant platform-as-a-service (PaaS) environment.

Event Hubs Premium replicates events to three replicas, which are distributed across Azure availability zones where available. All replicas are synchronously flushed to the underlying fast storage before the send operation is reported as completed. Events that aren't read immediately or that need to be reread later can be retained for up to 90 days. They're transparently held in an availability-zone-redundant storage tier.

In addition to these storage-related features and all capabilities and protocol support of the Standard tier, the isolation model of the Premium tier enables features like [dynamic partition scale-up](dynamically-add-partitions.md). You also get far more generous [quota allocations](event-hubs-quotas.md). Event Hubs Capture is included at no extra cost.

> [!NOTE]

> - Event Hubs Premium supports Transport Layer Security (TLS) 1.2 or greater.

> - The Premium tier isn't available in all regions. Try to create a namespace in the Azure portal. See the supported regions in the **Location** dropdown list on the **Create Namespace** page.

You can purchase 1, 2, 4, 6, 8, 10, 12, and 16 processing units (PUs) for each namespace. Because the Premium tier is a capacity-based offering, the achievable throughput isn't set by a throttle like it is in the Standard tier. The throughput depends on the work you ask Event Hubs to do, which is similar to the Dedicated tier. The effective ingest and stream throughput per PU depends on various factors, such as the:

* Number of producers and consumers.

* Payload size.

* Partition count.

* Egress request rate.

* Use of Event Hubs Capture, Schema Registry, and other advanced features.

For more information, see [Comparison between Event Hubs SKUs](event-hubs-quotas.md).

## Why choose Event Hubs Premium?

The Premium tier offers three compelling benefits for customers who require better isolation in a multitenant environment with low latency and high-throughput data ingestion needs.

### Superior performance with a two-tier storage engine

The Premium tier uses a new two-tier log storage engine that drastically improves the data ingress performance with substantially reduced overall latency without compromising the durability guarantees.

### Better isolation and predictability

The Premium tier offers an isolated compute and memory capacity to achieve more predictable latency and far reduced *noisy neighbor* impact risk in a multitenant deployment.

It implements a *cluster in cluster* model in its multitenant clusters to provide predictability and performance while retaining all the benefits of a managed multitenant PaaS environment.

### Cost savings and scalability

The Premium tier is a multitenant offering, so it can dynamically scale flexibly and quickly. Capacity is allocated in PUs that allocate isolated pods of CPU and memory inside the cluster. The number of those pods can be scaled up or down per namespace. For this reason, the Premium tier is a low-cost option for messaging scenarios with the overall throughput range that's less than 120 MB/sec but higher than what you can achieve with the Standard tier.

## Encryption of events

Event Hubs provides encryption of data at rest with Azure Storage Service Encryption. The Event Hubs service uses Azure Storage to store the data. All the data that's stored with Azure Storage is encrypted by using Microsoft-managed keys. If you use your own key (also referred to as Bring Your Own Key [BYOK] or customer-managed key), the data is still encrypted by using the Microsoft-managed key.

In addition, the Microsoft-managed key is encrypted by using the customer-managed key. This feature enables you to create, rotate, disable, and revoke access to customer-managed keys that are used for encrypting Microsoft-managed keys. Enabling the BYOK feature is a one-time setup process on your namespace. For more information, see [Configure customer-managed keys for encrypting Azure Event Hubs data at rest](configure-customer-managed-key.md).

> [!NOTE]

> All Event Hubs namespaces enabled for the Apache Kafka RPC protocol by default can be used by your existing Kafka-based applications. Having Kafka enabled on your cluster doesn't affect your non-Kafka use cases. There's no option or need to disable Kafka on a cluster.

## Quotas and limits

The Premium tier offers all the features of the Standard plan but with better performance, isolation, and more generous quotas. For more information on quotas and limits, see [Event Hubs quotas and limits](event-hubs-quotas.md).

## High availability with availability zones

Event Hubs Standard, Premium, and Dedicated tiers offer [availability zones](/azure/reliability/availability-zones-service-support) support with no extra cost. By using availability zones, you can run event streaming workloads in physically separate locations within each Azure region that are tolerant to local failures.

> [!IMPORTANT]

> - Availability zone support is only available in [Azure regions with availability zones](/azure/reliability/availability-zones-region-support).

>

## Premium vs. Dedicated tiers

In comparison to the Dedicated offering, the Premium tier provides the following benefits:

- Isolation inside a large multitenant environment can shift resources quickly.

- Scaling is far more elastic and quick.

- PUs can be dynamically adjusted.

When compared to the Dedicated tier, the Premium tier is often a more cost-effective option for event streaming workloads up to 160 MB/sec (per namespace), especially with changing loads throughout the day or week.

> [!NOTE]

> For the extra robustness gained by availability zone support, the minimal deployment scale for the Dedicated tier is eight capacity units (CUs). You have availability zone support in the Premium tier from the first PU in all availability zone regions.

## Pricing

The Premium offering is billed by [PUs](event-hubs-scalability.md#processing-units), which correspond to a share of isolated resources (CPU, memory, and storage) in the underlying infrastructure.

## FAQs

[!INCLUDE [event-hubs-dedicated-clusters-faq](./includes/event-hubs-premium-faq.md)]

## Related content

See the following articles:

- [Create an event hub](event-hubs-create.md). Select **Premium** for **Pricing tier**.

- [Event Hubs Premium pricing](https://azure.microsoft.com/pricing/details/event-hubs/) for more details on pricing.

- [Event Hubs FAQ](event-hubs-faq.yml) to find answers to some frequently asked questions about Event Hubs.


# Event Hubs Dedicated Overview

# Azure Event Hubs Dedicated tier overview

Azure Event Hubs Dedicated tier is a single-tenant solution designed to meet the needs of enterprise-scale, mission-critical event streaming workloads. This article provides an overview of the Dedicated tier, highlighting its key features, benefits, and use cases, showing how it supports high-performance, low-latency applications using Event Hubs SDK or Apache Kafka APIs.

## Benefits of dedicated clusters

The Dedicated tier of Event Hubs offers several benefits to customers who need to run mission-critical workloads at enterprise-level capacity.

### Low-latency event streaming

These clusters are optimized for low end-to-end latency and high performance. These clusters enable businesses to handle high-velocity and high-volume data streaming.

### Stream large volumes of data

Dedicated clusters can stream events at the scale of gigabytes per second or millions of events per second for most of the use cases. You can also scale these clusters to accommodate changes in event streaming volume.

### Guaranteed consistent performance

Event Hubs dedicated clusters minimize the latency jitter and ensure consistent performance with guaranteed capacity.

### Zero interference

Event Hubs dedicated clusters operate on a single-tenant architecture. This architecture ensures that the allocated resources aren't being shared with any other tenants. Unlike with other tiers, you don't see any cross-tenant interference in a dedicated cluster.

### Self-serve scaling

The dedicated cluster offers self-serve scaling capabilities that allow you to adjust the capacity of the cluster according to dynamic loads and to facilitate business operations. You can scale out during spikes in usage and scale in when the usage is low.

### High-end features and generous quotas

Dedicated clusters include all features of the Premium tier and more. The service also manages load balancing, operating system updates, security patches, and partitioning. You can spend less time on infrastructure maintenance and more time on building your event streaming applications.

### Supports streaming large messages

In most streaming scenarios, data is lightweight, typically less than 1 MB, and requires high throughput. There are instances where messages can't be divided into smaller segments. Self-serve dedicated clusters can accommodate events up to 20 MB of size at no extra cost. This capability allows Event Hubs to handle a wide range of message sizes to ensure uninterrupted business operations. For more information, see [Send and receive large messages with Azure Event Hubs](event-hubs-quickstart-stream-large-messages.md).

## Capacity units

Dedicated clusters are provisioned and billed by capacity units (CUs), which is a preallocated amount of CPU and memory resources.

How much you can ingest and stream per CU depends on factors such as the:

- Number of producers and consumers.

- Number of partitions.

- Producer and consumer configuration.

- Payload size.

- Egress rate.

To determine the necessary number of CUs, you should carry out your anticipated event streaming workload on an Event Hubs dedicated cluster while you observe the cluster's resource utilization. For more information, see [When should I scale my dedicated cluster](#when-should-i-scale-my-dedicated-cluster).

## Cluster types

Event Hubs dedicated clusters come in two distinct types: self-serve scalable clusters and legacy clusters. These two types differ in their support for the number of CUs, the amount of throughput each CU provides, and the regional and zone availability.

As a dedicated cluster user, you can determine the type of cluster by examining the availability of the capacity scaling feature in the portal. If this capability is present, you're using a self-serve scalable cluster. Conversely, if it isn't available, you're using a legacy dedicated cluster. Alternatively, you can look for the [Azure Resource Manager properties](/azure/templates/microsoft.eventhub/clusters?pivots=deployment-language-arm-template) related to dedicated clusters.

### Self-serve scalable clusters

Event Hubs self-serve scalable clusters are based on new infrastructure and allow users to scale the number of CUs allocated to each cluster. By creating a dedicated cluster through the Event Hubs portal or Azure Resource Manager templates (ARM templates), you gain access to a self-service scalable cluster. To learn how to scale your dedicated cluster, see [Scale Event Hubs dedicated clusters](event-hubs-dedicated-cluster-create-portal.md).

Approximately one CU in a self-serve scalable cluster provides *ingress capacity ranging from 100 MB/sec to 200 MB/sec*, although actual throughput might fluctuate depending on various factors.

With self-serve scalable clusters, you can purchase up to 10 CUs for a cluster in the Azure portal. In contrast to traditional clusters, these clusters can be scaled incrementally with CUs ranging from 1 to 10. If you need a cluster larger than 10 CUs, you can [submit a support request](event-hubs-dedicated-cluster-create-portal.md#submit-a-support-request) to scale up your cluster after its creation.

> [!IMPORTANT]

> To enable Availability zones on a Event Hubs dedicated cluster, it must be provisioned with three or more CUs.

>

### Legacy clusters

Event Hubs dedicated clusters created before the availability of self-serve scalable clusters are referred to as legacy clusters.

To use these legacy clusters, direct creation through the Azure portal or ARM templates isn't possible. Instead, you must [submit a support request](event-hubs-Dedicated-cluster-create-portal.md#submit-a-support-request) to create one.

Approximately one CU in a legacy cluster provides *ingress capacity ranging from 50 MB/sec to 100 MB/sec*, although actual throughput might fluctuate depending on various factors.

With a legacy cluster, you can purchase up to 20 CUs.

Legacy Event Hubs dedicated clusters require at least eight CUs to enable availability zones. Availability zone support is only available in [Azure regions with availability zones](/azure/reliability/availability-zones-region-support).

> [!IMPORTANT]

> Migrating an existing legacy cluster to a self-serve cluster isn't currently supported. For more information, see [Migrating a legacy cluster to a self-serve scalable cluster](#can-i-migrate-my-standard-or-premium-namespaces-to-a-dedicated-tier-cluster).

## Determine the cluster type

You can determine the cluster type that you're using with the following methods.

| Method | Action | Self-serve scalable clusters | Legacy clusters | Notes |

| -------------| ------------- | --------- | --------- | --------- |

| Use the portal | Check for the presence of the **Scale** tab under the cluster. | The **Scale** page is available in the cluster UI.| No **Scale** page is available in the cluster UI. |  |

| Use Azure Resource Manager| Check for the `supportsScaling` Azure Resource Manager property on the cluster.  | Check for the presence of the **Scale** page under the cluster.   | No **Scale** page is available in the cluster UI. | Check this property in the portal, the Azure CLI, or PowerShell. Needs API version *2022-01-01-preview* or newer. |

| Use `nslookup`| Run the `nslookup` command on a namespace in a cluster.   | CNAME maps to `*.cloudapp.azure.com`.   | CNAME maps to `*.cloudapp.net`. | Example: `nslookup ns.servicebus.windows.net`. |

## Quotas and limits

The Event Hubs Dedicated offering is billed at a fixed monthly price with a *minimum of four hours of usage*. The Dedicated tier offers all the features of the Premium plan, but with enterprise-scale capacity and limits for customers with demanding workloads.

For more information about quotas and limits, see [Event Hubs quotas and limits](event-hubs-quotas.md).

## FAQs

[!INCLUDE [event-hubs-dedicated-clusters-faq](./includes/event-hubs-dedicated-clusters-faq.md)]

## Related content

Explore more about Event Hubs Dedicated:

- [Create an Event Hubs cluster through the Azure portal](https://portal.azure.com).

- [Event Hubs Dedicated pricing](https://azure.microsoft.com/pricing/details/event-hubs/): Learn about pricing tiers and capacity options.

- [Event Hubs FAQ](event-hubs-faq.yml): Find answers to frequently asked questions about Event Hubs.


# Compare Tiers

# Compare Azure Event Hubs tiers

This article compares tiers of Azure Event Hubs.

> [!NOTE]

> This article compares only features and quotas of tiers. For pricing information, see [Azure Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).

## Features

[!INCLUDE [event-hubs-tier-features](./includes/event-hubs-tier-features.md)]

## Quotas

[!INCLUDE [event-hubs-tier-limits](./includes/event-hubs-tier-limits.md)]

## Related content

For pricing information for each tier, see [Azure Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).


# Schema Registry Concepts

# Schema Registry in Azure Event Hubs

Schema Registry in Azure Event Hubs has many benefits. Schema Registry helps maintain data consistency, simplify schema evolution, enhance interoperability, and reduce development effort in loosely coupled and event-streaming workflows. Large distributed organizations that employ a centralized repository for schemas can use Schema Registry to achieve highly reliable data processing and governance with little operational overhead.

Schema registries in Azure Event Hubs fulfill many roles in schema-driven event-streaming scenarios:

* Provide a repository where multiple schemas can be registered, managed, and evolved

* Manage schema evolution with multiple compatibility rules

* Perform data validation for all schematized data

* Provide client-side libraries (serializers and deserializers) for producers and consumers

* Improve network throughput efficiency by passing the schema ID instead of the schema definition for every payload

Schema registries in Azure Event Hubs are supported on Standard, Premium, and Dedicated tiers.

## Schema registry components

The schema registry is part of the Event Hubs namespace but can also be used with other message or event brokers, including Azure messaging services. It comprises multiple schema groups, which act as a logical grouping of schemas and can be managed independently of other schema groups.

### Schemas

In any loosely coupled system, multiple applications communicate, primarily through data. Schemas define the structure of the data in a declarative way. As a result, the contract between producer and consumer applications is well defined, ensuring reliable processing at scale.

A schema definition includes:

* Fields: Individual data elements like name, book title, or address.

* Data types: The type of data that can be stored, like string, date-time, or array.

* Structure: How the fields are organized, like nested structures or arrays.

Schemas define the contract between producers and consumers. A schema defined in an Event Hubs schema registry helps manage the contract outside event data, which removes the payload overhead.

#### Schema formats

Schema formats are used to determine the manner in which a schema is structured and defined. Each format outlines specific guidelines and syntax for defining the structure of the events that are used for event streaming.

##### Avro schema

[Apache Avro](https://avro.apache.org/) is a popular data serialization system that uses a compact binary format and provides schema evolution capabilities.

To learn more about using Avro schema format with an Event Hubs schema registry, see:

* [How to use Schema Registry with Kafka and Avro](schema-registry-kafka-java-send-receive-quickstart.md)

* [How to use Schema Registry with Event Hubs, .NET, an SDK (AMQP), and Avro](schema-registry-dotnet-send-receive-quickstart.md)

##### JSON schema

A [JSON (JavaScript Object Notation) schema](https://json-schema.org/) is a standardized way of defining the structure and data types of the events. A JSON schema enables the confident and reliable use of the JSON data format in event streaming.

To learn more about using the JSON schema format with an Event Hubs schema registry, see [How to use a schema registry with Kafka and JSON schema](schema-registry-json-schema-kafka.md).

##### Protocol Buffers

[Protocol Buffers (Protobuf)](https://protobuf.dev/) is a language-neutral, platform-neutral, extensible mechanism for serializing structured data. It's used for efficiently defining data structures and serializing them into a compact binary format.

### Schema groups

Schema groups are logical groups of similar schemas that are organized according to your business criteria. A schema group holds:

* Multiple schema definitions.

* Multiple versions of a specific schema.

* Metadata regarding the schema type and compatibility for all schemas in the group.

You can think of a schema group as a subset of the schema registry that aligns with a particular application or organizational unit, with a separate authorization model. This extra security boundary helps ensure that metadata and trade secrets aren't leaked in the shared services model. It also allows application owners to manage schemas independently of other applications that share the same namespace.

## Schema evolution

Schemas need to evolve with the business requirement of producers and consumers. Schema Registry supports schema evolution by introducing compatibility modes at the schema group level. When you create a schema group, you can specify the compatibility mode of the schemas that you include in that schema group. When you update a schema, the change needs to comply with the assigned compatibility mode so that it can create a new version of the schema.

Schema evolution is supported for Avro schema format only.

Schema Registry is supported in the following compatibility modes.

### Backward compatibility

Backward compatibility mode allows the consumer code to use a new version of a schema and process messages with an old version of the schema. Backward compatibility mode allows the following changes to be made on a schema:

* Delete fields

* Add optional fields

### Forward compatibility

Forward compatibility allows the consumer code to use an old schema version and read messages with the new schema. Forward compatibility mode allows the following changes to be made on a schema:

* Add fields

* Delete optional fields

### No compatibility

When the ``None`` compatibility mode is used, Schema Registry doesn't do any compatibility checks when you update schemas.

## Client SDKs

You can use one of the following libraries to include an Avro serializer. You can use Avro serializers to serialize and deserialize payloads that contain schema identifiers for the schema registry and Avro-encoded data:

| Programming language | SDK | Samples |

| ------ | -----| ----|

| **.NET** | [Microsoft.Azure.Data.SchemaRegistry.ApacheAvro](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/schemaregistry/Microsoft.Azure.Data.SchemaRegistry.ApacheAvro) | [.NET Samples](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/schemaregistry/Microsoft.Azure.Data.SchemaRegistry.ApacheAvro/tests/Samples) |

| **Java** | [azure-data-schemaregistry-avro](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/schemaregistry/azure-data-schemaregistry-apacheavro) | [Java samples](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/schemaregistry/azure-data-schemaregistry-apacheavro/src/samples)|

|**Python** | [azure-schemaregistry-avroserializer](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/schemaregistry/azure-schemaregistry-avroencoder/) | [Python samples](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/schemaregistry/azure-schemaregistry-avroencoder/samples)|

|**JavaScript** | [@azure/schema-registry-avro](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/schemaregistry/schema-registry-avro) | [Node.js samples](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/schemaregistry/schema-registry-avro/samples) |

Additionally, the below libraries are also available based on your workloads.

* **Apache Kafka**: Run [Kafka-integrated Avro](https://github.com/Azure/azure-schema-registry-for-kafka/) serializers and deserializers backed by Schema Registry. The Java client's Apache Kafka client serializer for Schema Registry can be used in any Apache Kafka scenario and with any Apache Kafka-based deployment or cloud service.

* **Azure CLI**: For an example of adding a schema to a schema group by using the Azure CLI, see [Adding a schema to a schema group by using the Azure CLI](https://github.com/Azure/azure-event-hubs/tree/master/samples/Management/CLI/AddschematoSchemaGroups).

* **PowerShell**: For an example of adding a schema to a schema group by using PowerShell, see [Adding a schema to a schema group by using PowerShell](https://github.com/Azure/azure-event-hubs/tree/master/samples/Management/PowerShell/AddingSchematoSchemagroups).

## Limits

For limits (like the number of schemas you can use in a namespace) of Event Hubs, see [Event Hubs quotas and limits](event-hubs-quotas.md).

## Azure role-based access control

To access a schema registry programmatically, follow these steps:

1. [Register your application in Microsoft Entra ID](../active-directory/develop/quickstart-register-app.md).

1. Add the security principal of the application to one of the following Azure role-based access control (RBAC) roles at the namespace level.

| Role | Description |

| ---- | ----------- |

| Owner | Read, write, and delete schema registry groups and schemas |

| Contributor | Read, write, and delete schema registry groups and schemas |

| [Schema Registry Reader](../role-based-access-control/built-in-roles/analytics.md#schema-registry-reader) | Read and list schema registry groups and schemas |

| [Schema Registry Contributor](../role-based-access-control/built-in-roles/analytics.md#schema-registry-contributor) | Read, write, and delete schema registry groups and schemas |

To learn how to create and register an application by using the Azure portal, see [Register an application with Microsoft Entra ID](../active-directory/develop/quickstart-register-app.md). You need the client ID (application ID), the tenant ID, and the secret to use in the code.

## Related content

* To learn how to create a schema registry by using the Azure portal, see [Create an Event Hubs schema registry by using the Azure portal](create-schema-registry.md).

* See the following samples from the Schema Registry Avro client library:

* [.NET](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/schemaregistry/Microsoft.Azure.Data.SchemaRegistry.ApacheAvro/tests/Samples)

* [Java](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/schemaregistry/azure-data-schemaregistry-apacheavro/src/samples)

* [JavaScript](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/schemaregistry/schema-registry-avro/samples)

* [Python](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/schemaregistry/azure-schemaregistry-avroencoder/samples)

* [Kafka Avro Integration for Schema Registry](https://github.com/Azure/azure-schema-registry-for-kafka/tree/master/csharp/avro/samples)


# Schema Registry Client Side Enforcement

# Client-side schema enforcement

Client-side schema enforcement ensures that data is validated against schemas defined in the schema registry on the client side rather than the broker/server side. The producer application can use schemas to validate and serialize data before sending the data to an event hub. Similarly, a consumer application can deserialize and validate data after it receives events from an event hub.

Client-side schema enforcement ensures that data is validated on the client side. The producer application sends the data, and the consumer application receives it. That data is validated against schemas defined in the schema registry on the client side rather than the broker/server side.

This diagram illustrates the flow:

> [!NOTE]

> The diagram showcases the information flow when event producers and consumers use a schema registry with the Kafka protocol and Avro schema. Other protocols and schema formats work in a similar way.

>

### Producer

1. The Kafka producer application uses `KafkaAvroSerializer` to serialize event data by using the specified schema. The producer application provides details of the schema registry endpoint and other optional parameters that are required for schema validation.

1. The serializer looks for the schema in the schema registry to serialize event data. If it finds the schema, then the corresponding schema ID is returned. You can configure the producer application to automatically register the schema with the schema registry if it doesn't exist.

1. The serializer prepends the schema ID to the serialized data that's published to the event hub.

### Consumer

1. The Kafka consumer application uses `KafkaAvroDeserializer` to deserialize data that it receives from the event hub.

1. The deserializer uses the schema ID (prepended by the producer) to retrieve the schema from the schema registry.

1. The deserializer uses the schema to deserialize event data that it receives from the event hub.

1. The schema registry client uses caching to prevent redundant schema registry lookups in the future.


# Event Processor Balance Partition Load

# Partition load balancing for event processing

Partition load balancing is a technique in Azure Event Hubs that distributes event processing workloads across multiple instances of your application. The event processor client automatically manages partition ownership and coordinates work distribution among all active consumer instances.

In the newer SDK versions (5.0 onwards), **EventProcessorClient** (.NET and Java) or **EventHubConsumerClient** (Python and JavaScript) handles load balancing automatically. You subscribe to the events you're interested in by registering an event handler.

This article describes a sample scenario for using multiple instances of client applications to read events from an event hub. It also explains key concepts like partition ownership, checkpointing, and load balancing.

> [!TIP]

> If you're using an older version of the client library, see the migration guides: [.NET](https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/eventhub/Azure.Messaging.EventHubs/MigrationGuide.md), [Java](https://github.com/Azure/azure-sdk-for-java/blob/master/sdk/servicebus/azure-messaging-servicebus/migration-guide.md), [Python](https://github.com/Azure/azure-sdk-for-python/blob/master/sdk/servicebus/azure-servicebus/migration_guide.md), and [JavaScript](https://github.com/Azure/azure-sdk-for-js/blob/master/sdk/servicebus/service-bus/migrationguide.md).

> [!NOTE]

> The key to scale for Event Hubs is the idea of partitioned consumers. In contrast to the [competing consumers](/previous-versions/msp-n-p/dn568101(v=pandp.10)) pattern, the partitioned consumer pattern enables high scale by removing the contention bottleneck and facilitating end-to-end parallelism.

## Example scenario

As an example scenario, consider a home security company that monitors 100,000 homes. Every minute, it gets data from various sensors such as a motion detector, door/window open sensor, glass break detector, and so on, installed in each home. The company provides a web site for residents to monitor the activity of their home in near real time.

Each sensor pushes data to an event hub. The event hub is configured with 16 partitions. On the consuming end, you need a mechanism that can read these events, consolidate them (filter, aggregate, and so on) and dump the aggregate to a storage blob, which is then projected to a user-friendly web page.

## Consumer application

When you design a consumer in a distributed environment, the scenario must handle the following requirements:

- **Scale:** Create multiple consumers, with each consumer taking ownership of reading from a few Event Hubs partitions.

- **Load balance:** Increase or reduce the consumers dynamically. For example, when a new sensor type (for example, a carbon monoxide detector) is added to each home, the number of events increases. In that case, the operator (a human) increases the number of consumer instances. Then, the pool of consumers can rebalance the number of partitions they own, to share the load with the newly added consumers.

- **Seamless resume on failures:** If a consumer (**consumer A**) fails (for example, the virtual machine hosting the consumer suddenly crashes), then other consumers can pick up the partitions owned by **consumer A** and continue. Also, the continuation point, called a *checkpoint* or *offset*, should be at the exact point at which **consumer A** failed, or slightly before that.

- **Consume events:** While the previous three points deal with the management of the consumer, there must be code to consume events and do something useful with it. For example, aggregate it and upload it to blob storage.

## Event processor or consumer client

You don't need to build your own solution to meet these requirements. The Azure Event Hubs SDKs provide this functionality. In .NET or Java SDKs, use an event processor client (`EventProcessorClient`). In Python and JavaScript SDKs, use `EventHubConsumerClient`. In the old version of SDK, the event processor host (`EventProcessorHost`) supported these features.

For most production scenarios, use the event processor client for reading and processing events. The processor client provides a robust experience for processing events across all partitions of an event hub in a performant and fault-tolerant manner while providing a means to checkpoint its progress. Event processor clients can work cooperatively within the context of a consumer group for a given event hub. Clients automatically manage distribution and balancing of work as instances become available or unavailable for the group.

## Partition ownership

An event processor instance typically owns and processes events from one or more partitions. The system evenly distributes ownership of partitions among all the active event processor instances associated with an event hub and consumer group combination.

Each event processor has a unique identifier and claims ownership of partitions by adding or updating an entry in a checkpoint store. All event processor instances communicate with this store periodically to update their own processing state and to learn about other active instances. The system uses this data to balance the load among the active processors. New instances can join the processing pool to scale up. When instances go down, either because of failures or to scale down, the system gracefully transfers partition ownership to other active processors.

Partition ownership records in the checkpoint store keep track of Event Hubs namespace,  event hub name, consumer group, event processor identifier (also known as owner), partition ID, and the last modified time.

| Event Hubs namespace               | Event hub name | **Consumer group** | Owner                                | Partition ID | Last modified time  |

| ---------------------------------- | -------------- | :----------------- | :----------------------------------- | :----------- | :------------------ |

| mynamespace.servicebus.windows.net | myeventhub     | myconsumergroup    | 3be3f9d3-9d9e-4c50-9491-85ece8334ff6 | 0            | 2020-01-15T01:22:15 |

| mynamespace.servicebus.windows.net | myeventhub     | myconsumergroup    | f5cc5176-ce96-4bb4-bbaa-a0e3a9054ecf | 1            | 2020-01-15T01:22:17 |

| mynamespace.servicebus.windows.net | myeventhub     | myconsumergroup    | 72b980e9-2efc-4ca7-ab1b-ffd7bece8472 | 2            | 2020-01-15T01:22:10 |

|                                    |                | :                  |                                      |              |                     |

|                                    |                | :                  |                                      |              |                     |

| mynamespace.servicebus.windows.net | myeventhub     | myconsumergroup    | 844bd8fb-1f3a-4580-984d-6324f9e208af | 15           | 2020-01-15T01:22:00 |

Each event processor instance acquires ownership of a partition and starts processing the partition from last known [checkpoint](#checkpoint). If a processor fails (VM shuts down), other instances detect the failure by looking at the last modified time. Other instances try to get ownership of the partitions previously owned by the inactive instance. The checkpoint store guarantees that only one of the instances succeeds in claiming ownership of a partition. So, at any given point in time, there's at most one processor that receives events from a partition.

## Receive messages

When you create an event processor, specify functions that process events and errors. Each call to the function that processes events delivers a single event from a specific partition. You must handle this event. If you want to make sure the consumer processes every message at least once, write your own code with retry logic. But be cautious about poisoned messages.

Process events relatively fast. That is, do as little processing as possible. If you need to write to storage and do some routing, it's better to use two consumer groups and have two event processors.

## Checkpoint

*Checkpointing* is a process by which an event processor marks or commits the position of the last successfully processed event within a partition. Marking a checkpoint typically happens within the function that processes the events and occurs on a per-partition basis within a consumer group.

If an event processor disconnects from a partition, another instance can resume processing the partition at the checkpoint that the last processor of that partition in that consumer group previously committed. When the processor connects, it passes the offset to the event hub to specify the location at which to start reading. In this way, you can use checkpointing to both mark events as "complete" by downstream applications and to provide resiliency when an event processor goes down. You can return to older data by specifying a lower offset from this checkpointing process.

When the checkpoint marks an event as processed, it adds or updates an entry in the checkpoint store with the event's offset and sequence number. Decide the frequency of updating the checkpoint. Updating after each successfully processed event can have performance and cost implications  as it triggers a write operation to the underlying checkpoint store. Also, checkpointing every single event is indicative of a queued messaging pattern for which a Service Bus queue might be a better option than an event hub. The idea behind Event Hubs is that you get "at least once" delivery at great scale. By making your downstream systems idempotent, it's easy to recover from failures or restarts that result in the same events being received multiple times.

[!INCLUDE [storage-checkpoint-store-recommendations](./includes/storage-checkpoint-store-recommendations.md)]

## Thread safety and processor instances

By default, the function that processes events is called sequentially for a given partition. Subsequent events and calls to this function from the same partition queue up behind the scenes as the event pump continues to run in the background on other threads. Events from different partitions can be processed concurrently. You must synchronize any shared state that's accessed across partitions.

## Related content

See the following quickstarts:

- [.NET Core](event-hubs-dotnet-standard-getstarted-send.md)

- [Java](event-hubs-java-get-started-send.md)

- [Python](event-hubs-python-get-started-send.md)

- [JavaScript](event-hubs-node-get-started-send.md)


# Event Hubs Federation Overview

# Multi-site and multi-region federation

Many sophisticated solutions require the same event streams to be made available for consumption in multiple locations, or they require event streams to be collected in multiple locations and then consolidated into a specific location for consumption. There's also often the need to enrich or reduce event streams or do event format conversions, also for within a single region and solution.

Practically, that means your solution will maintain multiple Event Hubs, often in different regions and Event Hubs namespaces, and then replicate events between them. You might also exchange events with sources and targets like [Azure Service Bus](../service-bus-messaging/service-bus-messaging-overview.md), [Azure IoT Hub](../iot/iot-introduction.md), or [Apache Kafka](https://kafka.apache.org).

Maintaining multiple active Event Hubs in different regions also allows clients to choose and switch between them if their contents are being merged, which makes the overall system more resilient against regional availability issues.

This "Federation" chapter explains federation patterns and how to realize these patterns using the serverless [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) or the [Azure Functions][1] runtimes, with the option of having your own transformation or enrichment code right in the event flow path.

## Federation Patterns

There are many potential motivations for why you may want to move events between different Event Hubs or other sources and targets, and we enumerate the most important patterns in this section and also link to more detailed guidance for the respective pattern.

- [Resiliency against regional availability events](#resiliency-against-regional-availability-events)

- [Latency optimization](#latency-optimization)

- [Validation, reduction, and enrichment](#validation-reduction-and-enrichment)

- [Integration with analytics services](#integration-with-analytics-services)

- [Consolidation and normalization of event streams](#consolidation-and-normalization-of-event-streams)

- [Splitting and routing of event streams](#splitting-and-routing-of-event-streams)

- [Log projections](#log-projections)

### Resiliency against regional availability events

![Regional Availability](media/event-hubs-federation-overview/regional-availability.png)

While maximum availability and reliability are the top operational priorities for Event Hubs, there are nevertheless many ways in which a producer or consumer might be prevented from talking to its assigned "primary" Event Hubs because of networking or name resolution issues, or where an Event Hubs might indeed be temporarily unresponsive or returning errors.

Such conditions aren't "disastrous" such that you'll want to abandon the regional deployment altogether as you might do in a [disaster recovery](event-hubs-geo-dr.md) situation, but the business scenario of some applications might already be impacted by availability events that last not more than a few minutes or even seconds.

There are two foundational patterns to address such scenarios:

- The [replication][4] pattern is about replicating the contents of a primary Event Hubs to a secondary Event Hubs, whereby the primary Event Hubs is generally used by the application for both producing and consuming events and the secondary serves as a fallback option in case the primary Event Hubs is becoming unavailable. Since replication is unidirectional, from the primary to the secondary, a switchover of both producers and consumers from an unavailable primary to the secondary will cause the old primary to no longer receive new events and it will therefore be no longer current.

Pure replication is therefore only suitable for one-way failover scenarios. Once the failover has been performed, the old primary is abandoned and a new secondary Event Hubs needs to be created in a different target region.

- The [merge][5] pattern extends the replication pattern by performing a continuous merge of the contents of two or more Event Hubs. Each event originally produced into one of the Event Hubs included in the scheme is replicated to the other Event Hubs. As events are replicated, they are annotated such that they are subsequently ignored by the replication process of the replication target. The results of using the merge pattern are two or more Event Hubs that will contain the same set of events in an eventually consistent fashion.

In either case, the contents of the Event Hubs will not be identical. Events from any one producer and grouped by the same partition key will appear in the same relative order as originally submitted, but the absolute order of events may differ. This is especially true for scenarios where the partition count of source and target Event Hubs differ, which is desirable for several of the extended patterns described here. A [splitter or router](#splitting-and-routing-of-event-streams) may obtain a slice of a much larger Event Hubs with hundreds of partitions and funnel into a smaller Event Hubs with just a handful of partitions, more suitable for handling the subset with limited processing resources. Conversely, a [consolidation](#consolidation-and-normalization-of-event-streams) may funnel data from several smaller Event Hubs into a single, larger Event Hubs with more partitions to cope with the consolidated throughput and processing needs.

The criterion for keeping events together is the partition key and not the original partition ID. Further considerations about relative order and how to perform a failover from one Event Hubs to the next without relying on the same scope of stream offsets is discussed in [replication][4] pattern description.

Guidance:

- [Replication pattern][4]

- [Merge pattern][5]

### Latency optimization

![Latency Optimization](media/event-hubs-federation-overview/latency-optimization.png)

Event streams are written once by producers, but may be read any number of times by event consumers. For scenarios where an event stream in a region is shared by multiple consumers, and needs to be accessed repeatedly during analytics processing residing in a different region, or with throughout demands that would starve out concurrent consumers, it may be beneficial to place a copy of the event stream near the analytics processor to reduce the roundtrip latency.

Good examples for when replication should be preferred over consuming events remotely from across regions are especially those where the regions are extremely far apart, for instance Europe and Australia being nearly antipodes, geographically and network latencies can easily exceed 250 ms for any round trip. You can't accelerate the speed of light, but you can reduce the number of high-latency round trips to interact with data.

Guidance:

- [Replication pattern][4]

### Validation, reduction, and enrichment

![Validation, reduction, enrichment](media/event-hubs-federation-overview/validation-enrichment.png)

Event streams may be submitted into an Event Hubs by clients external to your own solution. Such event streams may require for externally submitted events to be checked for compliance with a given schema, and for non-compliant events to be dropped.

In scenarios where clients are extremely bandwidth constrained as it is the case in many "Internet of Things" scenarios with metered bandwidth, or where events are originally sent over non-IP networks with constrained packet sizes, the events may have to be enriched with reference data to add further context for being usable by downstream event processors.

In other cases, especially when streams are being consolidated, the event data may have to be reduced in complexity or sheer size by omitting some detail.

Any of these operations may occur as part of replication, consolidation, or merge flows.

Guidance:

- [Editor pattern][6]

### Integration with analytics services

![Integration with analytics services](media/event-hubs-federation-overview/integration.png)

Several of Azure's cloud-native analytics services like Azure Stream Analytics or Azure Synapse work best with streamed or pre-batched data served up from Azure Event Hubs, and Azure Event Hubs also enables integration with several open-source analytics packages such as Apache Samza, Apache Flink, Apache Spark, and Apache Storm.

If your solution primarily uses Service Bus or Event Grid, you can make these events easily accessible to such analytics systems and also for archival with Event Hubs Capture if you funnel them into Event Hubs. Event Grid can do so natively with its [Event Hubs integration](../event-grid/handler-event-hubs.md), for Service Bus you follow the [Service Bus replication guidance](https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/functions/config/ServiceBusCopyToEventHub).

Azure Stream Analytics [integrates with Event Hubs directly](../stream-analytics/stream-analytics-define-inputs.md#stream-data-from-event-hubs).

Guidance:

- [Replication pattern][4]

### Consolidation and normalization of event streams

![Consolidation and normalization of event streams](media/event-hubs-federation-overview/consolidation.png)

Global solutions are often composed of regional footprints that are largely independent including having their own analytics capabilities, but supra-regional and global analytics perspectives will require an integrated perspective and that's why a central consolidation of the same event streams that are evaluated in the respective regional footprints for the local perspective.

Normalization is a flavor of the consolidation scenario, whereby two or more incoming event streams carry the same kind of events, but with different structures or different encodings, and the events most be transcoded or transformed before they can be consumed.

Normalization may also include cryptographic work such as decrypting end-to-end encrypted payloads and re-encrypting it with different keys and algorithms for the downstream consumer audience.

Guidance:

- [Merge pattern][5]

- [Editor pattern][6]

### Splitting and routing of event streams

![Splitting and routing of event streams](media/event-hubs-federation-overview/splitting.png)

Azure Event Hubs is occasionally used in "publish-subscribe" style scenarios where an incoming torrent of ingested events far exceeds the capacity of Azure Service Bus or Azure Event Grid, both of which have native publish-subscribe filtering and distribution capabilities and are preferred for this pattern.

While a true "publish-subscribe" capability leaves it to subscribers to pick the events they want, the splitting pattern has the producer map events to partitions by a predetermined distribution model and designated consumers then exclusively pull from "their" partition. With the Event Hubs buffering the overall traffic, the content of a particular partition, representing a fraction of the original throughput volume, may then be replicated into a queue for reliable, transactional, competing consumer consumption.

Many scenarios where Event Hubs is primarily used for moving events within an application within a region have some cases where select events, maybe just from a single partition, also have to be made available elsewhere. This scenario is similar to the splitting scenario, but might use a scalable router that considers all the messages arriving in an Event Hubs and cherry-picks just a few for onward routing and might differentiate routing targets by event metadata or content.

Guidance:

- [Routing pattern][7]

### Log projections

![Log projection](media/event-hubs-federation-overview/log-projection.png)

In some scenarios, you will want to have access to the latest value sent for any substream of an event, and commonly distinguished by the partition key. In Apache Kafka, this is often achieved by enabling "log compaction" on a topic, which discards all but the latest event labeled with any unique key. The log compaction approach has three compounding disadvantages:

- The compaction requires a continuous reorganization of the log, which is an excessively expensive operation for a broker that is optimized for append-only workloads.

- Compaction is destructive and does not allow for a compacted and non-compacted perspective of the same stream.

- A compacted stream still has a sequential access model, meaning that finding the desired value in the log requires reading the entire log in the worst case, which typically leads to optimizations that implement the exact pattern presented here: projecting the log contents into a database or cache.

Ultimately, a compacted log is a key-value store and as such, it is the worst possible implementation option for such a store. It is far more efficient for lookups and for queries to create and use a permanent projection of the log onto a proper key-value store or some other database.

Since events are immutable and the order is always preserved in a log, any projection of a log into a key-value store will always be identical for the same range of events, meaning that a projection you keep updated always provides an authoritative view and there is never any good reason to rebuild it from the log contents once built.

Guidance:

- [Log projection][8]

## Replication application technologies

Implementing the patterns above requires a scalable and reliable execution environment for the replication tasks that you want to configure and run. On Azure, the runtime environments that are best suited for such tasks are stateless tasks are [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) for stateful stream replication tasks and [Azure Functions](../azure-functions/functions-overview.md) for stateless replication tasks.

### Stateful replication applications in Azure Stream Analytics

For stateful replication applications that need to consider relationships between events, create composite events, enrich events or reduce events, create data aggregations, and transform event payloads, [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) is the best implementation option.

In Azure Stream Analytics, you [create jobs](../stream-analytics/stream-analytics-quick-create-portal.md) that integrate [inputs](../stream-analytics/stream-analytics-add-inputs.md) and

[outputs](../stream-analytics/stream-analytics-define-outputs.md) and integrate the data from the inputs through

[queries](/stream-analytics-query/stream-analytics-query-language-reference)

that yield a result that is then made available on the outputs.

Queries are based on the [SQL query language](/stream-analytics-query/stream-analytics-query-language-reference)

and can be used to easily filter, sort, aggregate, and join streaming data over a period of time. You can also extend this SQL language with

[JavaScript](../stream-analytics/stream-analytics-javascript-user-defined-functions.md) and [C# user-defined functions (UDFs)](../stream-analytics/stream-analytics-edge-csharp-udf-methods.md). You can easily adjust the event ordering options and duration of time windows when performing aggregation operations through simple language constructs and/or configurations.

Each job has one or several outputs for the transformed data, and you can control what happens in response to the information you've analyzed. For example, you can:

- Send data to services such as Azure Functions, Service Bus Topics or Queues to trigger communications or custom workflows downstream.

- Send data to a Power BI dashboard for real-time dashboarding.

- Store data in other Azure storage services (for example, Azure Data Lake, Azure Synapse Analytics, etc.) to perform batch analytics or train machine learning models based on very large, indexed pools of historical data.

- Store projections (also called "materialized views") in databases ([SQL Database](../stream-analytics/sql-database-output.md), [Azure Cosmos DB](../stream-analytics/azure-cosmos-db-output.md)).

### Stateless replication applications in Azure Functions

For stateless replication tasks where you want to forward events without considering their payloads or processes them singly without having to consider the relationships of events (except their relative order), you can use Azure Functions, which provides enormous flexibility.

Azure Functions has prebuilt, scalable triggers and output bindings for [Azure Event Hubs](../azure-functions/functions-bindings-event-hubs.md), [Azure IoT Hub](../azure-functions/functions-bindings-event-iot.md), [Azure Service Bus](../azure-functions/functions-bindings-service-bus.md), [Azure Event Grid](../azure-functions/functions-bindings-event-grid.md), and [Azure Queue Storage](../azure-functions/functions-bindings-storage-queue.md), as well as custom extensions for [RabbitMQ](https://github.com/azure/azure-functions-rabbitmq-extension), and [Apache Kafka](https://github.com/azure/azure-functions-kafka-extension). Most triggers will dynamically adapt to the throughput needs by scaling the number of concurrently executing instances up and down based on documented metrics.

For building log projections, Azure Functions supports output bindings for

[Azure Cosmos DB](../azure-functions/functions-bindings-cosmosdb-v2-output.md) and [Azure Table Storage](../azure-functions/functions-bindings-storage-table-output.md).

Azure Functions can run under a [Azure managed identity](../active-directory/managed-identities-azure-resources/overview.md) and with that, it can hold the configuration values for credentials in tightly access-controlled storage inside of [Azure Key Vault](/azure/key-vault/general/overview).

Azure Functions furthermore allows the replication tasks to directly integrate with Azure virtual networks and [service endpoints](../virtual-network/virtual-network-service-endpoints-overview.md) for all Azure messaging services, and it is readily integrated with [Azure Monitor](/azure/azure-monitor/overview).

With the Azure Functions consumption plan, the prebuilt triggers can even scale down to zero while no messages are available for replication, which means you incur no costs for keeping the configuration ready to scale back up; the key downside of using the consumption plan is that the latency for replication tasks "waking up" from this state is significantly higher than with the hosting plans where the infrastructure is kept running.

In contrast to all of this, most common replication engines for messaging and eventing, such as Apache Kafka's [MirrorMaker](http://kafka.apache.org/documentation/#basic_ops_mirror_maker)

require you to provide a hosting environment and scale the replication engine yourself. That includes configuring and integrating the security and networking features and facilitating the flow of monitoring data, and then you still don't have an opportunity to inject custom replication tasks into the flow.

### Choosing between Azure Functions and Azure Stream Analytics

Azure Stream Analytics (ASA) is the best option whenever you need to process the payload of your events while replicating them. ASA can copy events one by one or it can create aggregates that condense the information of event streams before forwarding it. It can [readily lean on complementing reference data](../stream-analytics/stream-analytics-use-reference-data.md) held in Azure Blob Storage or Azure SQL Database without having to import such data into a stream.

With ASA, you can easily create persistent, materialized views of streams in hyper-scale databases. It's a far superior approach to the clunky "log compaction" model of Apache Kafka and the volatile, client-side table projections of Kafka Streams.

ASA can readily process events having payloads encoded in the [CSV, JSON, and Apache Avro formats](../stream-analytics/stream-analytics-parsing-json.md) and you can plug in [custom deserializers](../stream-analytics/custom-deserializer.md) for any other format.

For all replication tasks where you want to copy event streams "as-is" and without touching the payloads, or if you need to implement a router, perform cryptographic work, change the encoding of payloads, or if otherwise need full control over the data stream contents, Azure Functions is the best option.

## Next Steps

In this article, we explored a range of federation patterns and explained the role of Azure Functions as the event and messaging replication runtime in Azure.

Next, you might want to read up how to set up a replicator application with Azure Stream Analytics or Azure Functions and then how to replicate event flows between Event Hubs and various other eventing and messaging systems:

- [Event replication task patterns][10]

- [Process data with Azure Stream Analytics][9]

- [Event replicator applications in Azure Functions][1]

- [Replicating events between Event Hubs][2]

- [Replicating events to Azure Service Bus][3]

- [Use Apache Kafka MirrorMaker with Event Hubs][11]

[1]: event-hubs-federation-replicator-functions.md

[2]: https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/functions/config/EventHubCopy

[3]: https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/functions/config/EventHubCopyToServiceBus

[4]: event-hubs-federation-patterns.md#replication

[5]: event-hubs-federation-patterns.md#merge

[6]: event-hubs-federation-patterns.md#editor

[7]: event-hubs-federation-patterns.md#routing

[8]: event-hubs-federation-patterns.md#log-projection

[9]: process-data-azure-stream-analytics.md

[10]: event-hubs-federation-patterns.md#replication

[11]: event-hubs-kafka-mirror-maker-tutorial.md


# Event Hubs Federation Replicator Functions

# Event replication tasks and applications with Azure Functions

> [!TIP]

> For all stateful replication tasks where you need to consider the payloads of your events and

> transform, aggregate, enrich, or reduce them, use [Azure Stream

Analytics](../stream-analytics/stream-analytics-introduction.md) instead of Azure Functions.

As explained in the [event replication and cross-region federation](event-hubs-federation-overview.md) article, stateless replication of event streams between pairs of Event Hubs and between Event Hubs and other event stream sources and targets leans on Azure Functions.

[Azure Functions](../azure-functions/functions-overview.md) is a scalable and reliable execution environment for configuring and running serverless applications, including event replication and federation tasks.

In this overview, you will learn about Azure Functions' built-in capabilities for such applications, about  code blocks that you can adapt and modify for transformation tasks, and about how to configure an Azure Functions application such that it integrates ideally with Event Hubs and other Azure Messaging services. For many details, this article will point to the Azure Functions documentation.

[!INCLUDE [messaging-replicator-functions](../../includes/messaging-replicator-functions.md)]


# Event Hubs Federation Patterns

# Event replication tasks patterns

The [federation overview](event-hubs-federation-overview.md) and the

[replicator functions overview](event-hubs-federation-replicator-functions.md) explain the rationale for and the basic elements of replication tasks, and we recommend that you familiarize yourself with them before you continue with this article.

In this article, we detail implementation guidance for several of the patterns highlighted in the overview section.

## Replication

The Replication pattern copies events from one Event Hub to the next, or from an Event Hub to some other destination like a Service Bus queue. The events are forwarded without making any modifications to the event payload.

The implementation of this pattern is covered by the

[Event replication between Event Hubs](https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/functions/config/EventHubCopy) and

[Event replication between Event Hubs and Service Bus](https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/functions/config/EventHubCopyToServiceBus)

samples and the [Use Apache Kafka MirrorMaker with Event Hubs](event-hubs-kafka-mirror-maker-tutorial.md) tutorial for the specific case of replicating data from an Apache Kafka broker into Event Hubs.

### Streams and order preservation

Replication, either through Azure Functions or Azure Stream Analytics, doesn't aim to assure the creation of exact 1:1 clones of a source Event Hub into a target Event Hub. Instead, it focuses on preserving the relative order of events where the application requires it. The application communicates this by grouping related events with the same partition key and [Event Hubs arranges messages with the same partition key sequentially in the same partition](event-hubs-features.md#partitions).

> [!IMPORTANT]

> The "offset" information is unique for each Event Hub and offsets

> for the same events will differ across Event Hub instances. To locate a

> position in a copied eventstream, use time-based offsets and refer to the

> [propagated service-assigned metadata](#service-assigned-metadata).

>

> Time-based offsets start your receiver at a specific point in time:

> - *EventPosition.FromStart()* - Read all retained data again.

> - *EventPosition.FromEnd()* - Read all new data from the time of connection.

> - *EventPosition.FromEnqueuedTime(dateTime)* - All data starting from a given date and time.

>

> In the EventProcessor, you set the position through the InitialOffsetProvider

> on the EventProcessorOptions. With the other receiver APIs, the position is

> passed through the constructor.

The prebuilt replication function helpers [provided as samples](https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/src/Azure.Messaging.Replication)

that are used in the Azure Functions based guidance ensure that eventstreams with the same partition key retrieved from a source partition are submitted into the target Event Hub as a batch in the original stream and with the same partition key.

If the partition count of the source and target Event Hub is identical, all streams in the target map to the same partitions as they did in the source. If the partition count is different, which matters in some of the further patterns described in the following, the mapping will differ, but streams are always kept together and in order.

The relative order of events belonging to different streams or of independent events without a partition key in a target partition might always differ from the source partition.

### Service-assigned metadata

The service-assigned metadata of an event obtained from the source Event Hub, the original enqueue time, sequence number, and offset, are replaced by new service-assigned values in the target Event Hub. However, with the [helper functions](https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/src/Azure.Messaging.Replication), replication tasks that are provided in our samples, the original values are preserved in user properties: `repl-enqueue-time` (ISO8601 string),

`repl-sequence`, `repl-offset`.

Those properties are of type string and contain the stringified value of the respective original properties. If the event is forwarded multiple times, the service-assigned metadata of the immediate source is appended to the already existing properties, with values separated by semicolons.

### Failover

If you're using replication for disaster recovery purposes, to protect against regional availability events in the Event Hubs service, or against network interruptions, any such failure scenario requires performing a failover from one Event Hub to the next, telling producers and/or consumers to use the secondary endpoint.

For all failover scenarios, it's assumed that the required elements of the namespaces are structurally identical, meaning that Event Hubs and Consumer Groups are identically named and that shared access signature rules and/or role-based access control rules are set up in the same way. You can create (and update) a secondary namespace by following the

[guidance for moving namespaces](move-across-regions.md) and omitting the cleanup step.

To force producers and consumers to switch, you need to make the information about which namespace to use available for lookup in a location that's easy to reach and update. If producers or consumers encounter frequent or persistent errors, they should consult that location and adjust their configuration. There are numerous ways to share that configuration, but we point out two in the following: DNS and file shares.

#### DNS-based failover configuration

One candidate approach is to hold the information in DNS SRV records in a DNS you control and point to the respective Event Hub endpoints.

> [!IMPORTANT]

> Mind that Event Hubs doesn't allow for its endpoints to be

> directly aliased with CNAME records, which means you use DNS as a

> resilient lookup mechanism for endpoint addresses and not to directly resolve

> IP address information.

Assume you own the domain `example.com` and, for your application, a zone

`test.example.com`. For two alternate Event Hubs, you now create two

further nested zones, and an SRV record in each.

The SRV records are, following common convention, prefixed with

`_azure_eventhubs._amqp` and hold two endpoint records: One for AMQP-over-TLS on

port 5671 and one for AMQP-over-WebSockets on port 443, both pointing to the Event Hubs endpoint of the namespace corresponding to the zone.

| Zone                   | SRV record                                                                                                                                                            |

| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| `eh1.test.example.com` | **`_azure_servicebus._amqp.eh1.test.example.com`**<br>`1 1 5671 eh1-test-example-com.servicebus.windows.net`<br>`2 2 443 eh1-test-example-com.servicebus.windows.net` |

| `eh2.test.example.com` | **`_azure_servicebus._amqp.eh2.test.example.com`**<br>`1 1 5671 eh2-test-example-com.servicebus.windows.net`<br>`2 2 443 eh2-test-example-com.servicebus.windows.net` |

In your application's zone, you then create a CNAME entry that points to the subordinate zone corresponding to your primary Event Hub:

| CNAME record                | Alias                    |

| --------------------------- | ------------------------ |

| `eventhub.test.example.com` | `eh1.test.example.com`   |

Using a DNS client that allows for querying CNAME and SRV records explicitly (the built-in clients of Java and .NET only allow for simple resolution of names to IP addresses), you can then resolve the desired endpoint. With

[DnsClient.NET](https://dnsclient.michaco.net/), for instance, the lookup function is:

```C#

static string GetEventHubName(string aliasName)

{

const string SrvRecordPrefix = "_azure_eventhub._amqp.";

LookupClient lookup = new LookupClient();

return (from CNameRecord alias in (lookup.Query(aliasName, QueryType.CNAME).Answers)

from SrvRecord srv in lookup.Query(SrvRecordPrefix + alias.CanonicalName, QueryType.SRV).Answers

where srv.Port == 5671

select srv.Target).FirstOrDefault()?.Value.TrimEnd('.');

}

```

The function returns the target host name registered for port 5671 of the zone currently aliased with the CNAME as shown previously.

Performing a failover requires editing the CNAME record and pointing it to the alternate zone.

The advantage of using DNS, and specifically

[Azure DNS](../dns/dns-overview.md), is that Azure DNS information is globally replicated and therefore resilient against single-region outages.

This procedure is similar to how the [Event Hubs Geo-DR](event-hubs-geo-dr.md) works, but fully under your own control and also works with active/active scenarios.

#### File-share based failover configuration

The simplest alternative to using DNS for sharing endpoint information is to put the name of the primary endpoint into a plain-text file and serve the file from an infrastructure that's robust against outages and still allows updates.

If you already run a highly available web site infrastructure with global availability and content replication, adding such a file there and republish the file if a switch is needed.

> [!CAUTION]

> You should only publish the endpoint name in this way, not a full connection string including secrets.

#### Extra considerations for failing over consumers

For Event Hub consumers, further considerations for the failover strategy depend on the needs of the event processor.

If there's a disaster that requires rebuilding a system, including databases, from backup data, and the databases are fed directly or via intermediate processing from the events held in the Event Hub, you'll restore the backup and then want to start replaying events into the system from the moment at which the database backup was created and not from the moment the original system was destroyed.

If a failure only affects a slice of a system or indeed only a single Event Hub, which has become unreachable, you'll likely want to continue processing events from about the same position where processing was interrupted.

To realize either scenario and using the event processor of your respective Azure SDK,

[you'll create a new checkpoint store](event-processor-balance-partition-load.md#checkpoint)

and provide an initial partition position, based on the _timestamp_ that you want to resume processing from.

If you still have access to the checkpoint store of the Event Hub you're switching away from, the [propagated metadata](#service-assigned-metadata)

discussed previously will help you to skip events that were already handled and resume precisely from where you last left off.

## Merge

The merge pattern has one or more replication tasks pointing to one target, possibly concurrently with regular producers also sending events to the same target.

Variations of these patterns are:

- Two or more replication functions concurrently acquiring events from separate sources and sending them to the same target.

- One more replication function acquiring events from a source while the target is also used directly by producers.

- The prior pattern, but mirrored between two or more Event Hubs, resulting in those Event Hubs containing the same streams, no matter where events are produced.

The first two pattern variations are trivial and don't differ from plain replication tasks.

The last scenario requires excluding already replicated events from being replicated again. The technique is demonstrated and explained in the [EventHubToEventHubMerge](https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/functions/code/EventHubMerge)

sample.

## Editor

The editor pattern builds on the [replication](#replication) pattern, but messages are modified before they're forwarded.

Examples for such modifications are:

- **_Transcoding_** - If the event content (also referred to as "body" or

"payload") arrives from the source encoded using the _Apache Avro_ format or some proprietary serialization format, but the expectation of the system owning the target is for the content to be _JSON_ encoded, a transcoding replication task will first deserialize the payload from _Apache Avro_ into an in-memory object graph and then serialize that graph into the _JSON_ format for the event that's being forwarded. Transcoding also includes **content compression** and decompression tasks.

- **_Transformation_** - Events that contain structured data might require reshaping of that data for easier consumption by downstream consumers. This might involve work like flattening nested structures, pruning extraneous data elements, or reshaping the payload to exactly fit a given schema.

- **_Batching_** - Events might be received in batches (multiple events in a single transfer) from a source, but have to be forwarded singly to a target, or vice versa. A task might therefore forward multiple events based on a single input event transfer or aggregate a set of events that are then transferred together.

- **_Validation_** - Event data from external sources often need to be checked for whether they're in compliance with a set of rules before they might be forwarded. The rules might be expressed using schemas or code. Events that are found not to be in compliance might be dropped, with the issue noted in logs, or might be forwarded to a special target destination to handle them further.

- **_Enrichment_** - Event data coming from some sources might require enrichment with further context for it to be usable in target systems. This might involve looking up reference data and embedding that data with the event, or adding information about the source that's known to the replication task, but not contained in the events.

- **_Filtering_** - Some events arriving from a source might have to be withheld from the target based on some rule. A filter tests the event against a rule and drops the event if the event doesn't match the rule. Filtering out duplicate events by observing certain criteria and dropping subsequent events with the same values is a form of filtering.

- **_Cryptography_** - A replication task might have to decrypt content arriving from the source and/or encrypt content forwarded onwards to a target, and/or it might have to verify the integrity of content and metadata relative to a signature carried in the event, or attach such a signature.

- **_Attestation_** - A replication task might attach metadata, potentially protected by a digital signature, to an event that attests that the event has been received through a specific channel or at a specific time.

- **_Chaining_** - A replication task might apply signatures to streams of events such that the integrity of the stream is protected and missing events can be detected.

The transformation, batching, and enrichment patterns are generally best implemented with [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) jobs.

All those patterns can be implemented using Azure Functions, using the [Event Hubs Trigger](../azure-functions/functions-bindings-event-hubs-trigger.md) for acquiring events and the

[Event Hub output binding](../azure-functions/functions-bindings-event-hubs-output.md) for delivering them.

## Routing

The routing pattern builds on the [replication](#replication) pattern, but instead of having one source and one target, the replication task has multiple targets, illustrated here in C#:

```csharp

[FunctionName("EH2EH")]

public static async Task Run(

[EventHubTrigger("source", Connection = "EventHubConnectionAppSetting")] EventData[] events,

[EventHub("dest1", Connection = "EventHubConnectionAppSetting")] EventHubClient output1,

[EventHub("dest2", Connection = "EventHubConnectionAppSetting")] EventHubClient output2,

ILogger log)

{

foreach (EventData eventData in events)

{

// send to output1 and/or output2 based on criteria

EventHubReplicationTasks.ConditionalForwardToEventHub(input, output1, log, (eventData) => {

return ( inputEvent.SystemProperties.SequenceNumber%2==0 ) ? inputEvent : null;

});

EventHubReplicationTasks.ConditionalForwardToEventHub(input, output2, log, (eventData) => {

return ( inputEvent.SystemProperties.SequenceNumber%2!=0 ) ? inputEvent : null;

});

}

}

```

The routing function will consider the message metadata and/or the message payload and then pick one of the available destinations to send to.

In Azure Stream Analytics, you can achieve the same with defining multiple outputs and then executing a query per output.

```sql

select * into dest1Output from inputSource where Info = 1

select * into dest2Output from inputSource where Info = 2

```

## Log projection

The log projection pattern flattens the eventstream onto an indexed database, with events becoming records in the database. Typically, events are added to the same collection or table, and the Event Hub partition key becomes part of the primary key looking for making the record unique.

Log projection can produce a time-series historian of your event data or a compacted view, whereby only the latest event is retained for each partition key. The shape of the target database is ultimately up to you and your application's needs. This pattern is also referred to as "event sourcing".

> [!TIP]

> You can easily create log projections into [Azure SQL Database](../stream-analytics/sql-database-output.md) and [Azure Cosmos DB](../stream-analytics/azure-cosmos-db-output.md) in Azure Stream Analytics, and you should prefer that option.

The following Azure Function projects the contents of an Event Hub compacted into an Azure Cosmos DB collection.

```C#

[FunctionName("Eh1ToCosmosDb1Json")]

[ExponentialBackoffRetry(-1, "00:00:05", "00:05:00")]

public static async Task Eh1ToCosmosDb1Json(

[EventHubTrigger("eh1", ConsumerGroup = "Eh1ToCosmosDb1", Connection = "Eh1ToCosmosDb1-source-connection")] EventData[] input,

[CosmosDB(databaseName: "SampleDb", collectionName: "foo", ConnectionStringSetting = "CosmosDBConnection")] IAsyncCollector<object> output,

ILogger log)

{

foreach (var ev in input)

{

if (!string.IsNullOrEmpty(ev.SystemProperties.PartitionKey))

{

var record = new

{

id = ev.SystemProperties.PartitionKey,

data = JsonDocument.Parse(ev.Body),

properties = ev.Properties

};

await output.AddAsync(record);

}

}

}

```

## Next steps

- [Event replicator applications in Azure Functions][1]

- [Replicating events between Event Hubs][2]

- [Replicating events to Azure Service Bus][3]

[1]: event-hubs-federation-replicator-functions.md

[2]: https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/functions/config/EventHubCopy

[3]: https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/functions/config/EventHubCopyToServiceBus


# Event Hubs Federation Configuration

# Configured replication tasks - Azure Event Hubs

[!INCLUDE [messaging-configured-functions](../../includes/messaging-configured-functions.md)]

## Next Steps

* [Replicating event data between Event Hubs](https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/functions/config/EventHubCopy)

* [Replicating event data to Service Bus](https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/functions/config/EventHubCopyToServiceBus)

* [Replicating event data from Service Bus](https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/functions/config/ServiceBusCopyToEventHub)


# Geo Replication

# Geo-replication in Azure Event Hubs

Azure Event Hubs geo-replication keeps copies of your namespace's metadata (entities, configuration, and properties) and event data in multiple Azure regions. If your primary region experiences an outage, you can promote a secondary region to keep your streaming applications running with minimal data loss.

The following sections explain how geo-replication works, compare synchronous and asynchronous replication modes, and describe how to manage secondary regions.

> [!NOTE]

> The Event Hubs geo-replication feature is available on the Premium and Dedicated tiers only.

Geo-replication ensures that metadata and data of a namespace is continuously replicated from a primary region to the secondary region. The namespace can be thought of as being extended to more than one region, with one region being the primary and the other being the secondary.

At any time, the secondary region can be promoted to become a primary region. Promoting a secondary repoints the namespace FQDN (fully qualified domain name) to the selected secondary region, and the previous primary region is demoted to a secondary region.

## Scenarios

Event Hubs geo-replication can be used in multiple scenarios.

### Business continuity and disaster recovery

Geo-replication ensures disaster recovery and business continuity for all streaming data on your namespace. By replicating data across regions, organizations can safeguard against data loss and ensure that their applications remain operational even in the event of a regional outage. This feature is crucial for mission-critical applications that require high availability and minimal downtime.

### Global data distribution

Geo-replication can be used to distribute data globally, allowing applications to access data from the nearest region. This reduces latency and improves performance for workloads located in different parts of the world.

### Data sovereignty and compliance

Organizations operating in multiple countries or regions often need to comply with data sovereignty laws that require data to be stored within specific geographic boundaries. Geo-replication allows these organizations to replicate data to regions that comply with local regulations, ensuring that they meet legal requirements while still maintaining a unified data platform.

### Migration and upgrades

Geo-replication can also be used to facilitate data migration, maintenance, and system upgrades. Organizations can migrate their namespace proactively from a primary to a secondary region to allow for any maintenance and upgrades on the primary region.

## Basic concepts

The geo-replication feature uses a primary-secondary replication model to replicate metadata and data. At any given time, there's a single primary region that serves both producers and consumers. The secondary region acts as a hot standby region, so you can't interact with the secondary region. However, it runs in the same configuration as the primary region, which means it can quickly step in after promotion.

Some of the key aspects of the geo-replication feature are:

-	Primary-secondary replication model – Geo-replication is built on a primary-secondary replication model, where at a given time there's only one primary namespace that serves event producers and event consumers.

-	Event Hubs performs fully managed byte-to-byte replication of metadata, event data, and consumer offset across secondaries with the configured consistency levels.

-	Single namespace hostname - After you successfully configure a geo-replication-enabled namespace, use the namespace hostname in your client application. The hostname behaves agnostic of the configured primary and secondary regions, and always points to the primary region.

- When you initiate a promotion, the hostname points to the region selected to be the new primary region. The old primary becomes a secondary region.

- You can't read or write on the secondary regions.

- Customer-managed promotion from primary to secondary region, providing full ownership and visibility for outage resolution. Metrics are available, which can help to automate the promotion from customer side.

- You can add or remove secondary regions.

-	Replication consistency - Two replication consistency settings are available: synchronous and asynchronous.

| State | Diagram |

| --- | ---|

| Before failover (promotion of secondary) | :::image type="content" source="./media/geo-replication/a-as-primary.png" alt-text="Diagram showing when region A is primary, B is secondary."::: |

| After failover (promotion of secondary) | :::image type="content" source="./media/geo-replication/b-as-primary.png" alt-text="Diagram showing when B is made the primary, that A becomes the new secondary."::: |

## Replication modes

Two replication consistency configurations are available: synchronous and asynchronous. Understand the differences between these two configurations because they affect your applications and your data consistency.

### Asynchronous replication

When you use asynchronous replication, the primary commits all requests and then sends an acknowledgment to the client. Replication to the secondary regions happens asynchronously. You can configure the maximum acceptable amount of lag time - the service side offset between the latest action on the primary and the secondary regions. The service continuously replicates the data and metadata, ensuring the lag remains as small as possible. If the lag for an active secondary grows beyond the user configured maximum replication lag, the primary starts throttling incoming requests.

### Synchronous replication

When you use synchronous replication, the system sends all requests to the secondary location. The secondary location commits and confirms the operation before the primary location commits. As a result, your application publishes at the rate it takes to publish, replicate, acknowledge, and commit. This process means your application depends on the availability of both regions. If the secondary region lags or is unavailable, the primary location doesn't acknowledge or commit messages and throttles incoming requests.

### Replication consistency comparison

With **synchronous** replication:

* Latency is longer due to the distributed commit operations.

* Availability depends on the availability of two regions. If one region goes down, your namespace is unavailable.

On the other hand, synchronous replication provides the greatest assurance that your data is safe. With synchronous replication, data commits in all of the regions you configured for geo-replication, providing the best data assurance.

With **asynchronous** replication:

* Latency is minimally affected.

* The loss of a secondary region doesn't immediately affect availability. However, availability is affected once the configured maximum replication lag is reached.

As such, it doesn't have the absolute guarantee that all regions have the data before the commit like synchronous replication does, and data loss or duplication might occur. However, as you're no longer immediately affected when a single region lags or is unavailable, application availability improves, in addition to having a lower latency.

| Capability                     | Synchronous replication                                      | Asynchronous replication                                           |

|--------------------------------|--------------------------------------------------------------|--------------------------------------------------------------------|

| Latency                        | Longer due to distributed commit operations                  | Minimally affected                                                 |

| Availability                   | Tied to availability of secondary regions                    | Loss of a secondary region doesn't immediately affect availability |

| Data consistency               | Data always committed in both regions before acknowledgment  | Data committed in primary only before acknowledgment               |

| RPO (Recovery Point Objective) | RPO 0, no data loss on promotion                             | RPO > 0, possible data loss on promotion                           |

You can change the replication mode after configuring geo-replication. You can switch from synchronous to asynchronous or from asynchronous to synchronous. If you switch from asynchronous to synchronous, the secondary region is configured as synchronous after lag reaches zero. If you're running with a continual lag for whatever reason, you might need to pause your publishers for lag to reach zero and your mode to be able to switch to synchronous. The reasons to enable synchronous replication, instead of asynchronous replication, are tied to the importance of the data, specific business needs, or compliance reasons, rather than availability of your application.

> [!NOTE]

> If a secondary region lags or becomes unavailable, the application can't replicate to this region and starts throttling once the replication lag is reached. To continue using the namespace in the primary location, remove the afflicted secondary region. If you remove all secondary regions, the namespace continues without geo-replication enabled. You can add other secondary regions at any time. Top-level entities, which are event hubs, are replicated synchronously, regardless of the replication mode configured.

>

## Secondary region selection

To enable the geo-replication feature, use primary and secondary regions where the feature is enabled. The geo-replication feature depends on being able to replicate published messages from the primary to the secondary regions. If the secondary region is on another continent, this choice has a major impact on replication lag from the primary to the secondary region. If you're using geo-replication for availability reasons, choose secondary regions on the same continent where possible. To get a better understanding of the latency induced by geographic distance, see [Azure network round-trip latency statistics](/azure/networking/azure-network-latency).

> [!NOTE]

> Geo-replication requires that primary and secondary copies of the Event Hubs be on the same tier. You can't configure geo-replication across tiers.

>

## Geo-replication management

The geo-replication feature enables you to configure a secondary region towards which to replicate metadata and data. As such, you can perform the following management tasks:

-	**Configure geo-replication** - You can configure secondary regions on any new or existing namespace in a region by enabling the geo-replication feature.

-	**Configure the replication consistency** - Set synchronous and asynchronous replication when you configure geo-replication. You can also switch this setting later.

-	**Trigger promotion/failover** - All promotions are customer initiated.

-	**Remove a secondary** - If you want to remove a secondary region, you can do so. The data in the secondary region is deleted.

### Criteria to trigger promotion

Here are some cases where a promotion of a secondary to primary might be triggered.

* Regional outage: If there's a regional outage affecting the primary region, promote the secondary region to ensure business continuity and minimize downtime.

* Maintenance activities: During planned maintenance activities in the primary region, promoting the secondary region can help maintain high availability for mission-critical applications.

* Disaster recovery: In the event of a disaster affecting the primary region, promoting the secondary region ensures that your data remains accessible and your applications continue to function.

* Performance issues: If the primary region is experiencing performance issues that affect the availability or reliability of your Event Hubs, promoting the secondary region can help mitigate these issues.

Occasionally test failover mechanisms to ensure the business continuity plan is effective and your applications can seamlessly switch to the secondary region when needed.

## Monitoring data replication

You can monitor the progress of the replication job by checking the replication lag metric in Application Metrics logs.

-	Enable Application Metrics logs in your Event Hubs namespace by following [Monitoring Azure Event Hubs - Azure Event Hubs | Microsoft Learn](./monitor-event-hubs.md).

-	After enabling Application Metrics logs, produce and consume data from the namespace for a few minutes before you start to see the logs.

-	To view Application Metrics logs, go to the **Monitoring** section of the Event Hubs page, and select **Logs** on the left menu. Use the following query to find the replication lag (in seconds) between the primary and secondary namespaces.

```kusto

AzureDiagnostics

| where TimeGenerated > ago(1h)

| where Category == "ApplicationMetricsLogs"

| where ActivityName_s == "ReplicationLag"

```

-	The column `count_d` shows the replication lag in seconds between the primary and secondary region.

## Publishing data

Publishing applications can send data to geo-replicated namespaces through the namespace hostname of the geo-replication-enabled namespace. The publishing approach is the same as the non-geo-replication case. You don't need to make any changes to data plane SDKs or client applications.

Event publishing might not be available during the following circumstances:

-	After requesting promotion of a secondary region, the existing primary region rejects any new events that are published to the event hub.

-	When replication lag between primary and secondary regions reaches the max replication lag duration, the publisher ingress workload might get throttled.

Publisher applications can't directly access any namespaces in the secondary regions.

## Consuming data

Consuming applications can consume data by using the namespace hostname of a namespace with the geo-replication feature enabled. Consumer operations aren't supported from the moment that promotion starts until promotion finishes.

### Checkpointing and offset management

Event-consuming applications can maintain offset management the same way they do with a non-geo-replicated namespace. Geo-replication-enabled namespaces don't need special consideration for offset management.

> [!WARNING]

> In the event of forced failover (that is, non-graceful failover), some data might be lost because it's not yet copied over. This data loss might cause the offsets of that specific data to be different across the primary and secondary regions for the namespace. However, the offsets stay within the bounds of the maximum replication lag configured for the namespace.

> In such cases, start consuming from the last committed offset. Some data might have duplicate processing and you must handle it on the client side.

>

#### Kafka

Consumers commit offsets directly to Event Hubs, and the system replicates offsets across regions. Therefore, consumers can start consuming from where they left off in the primary region.

Here's a list of supported Apache Kafka clients:

| Client name | Version |

| ----------- | ------- |

| Apache Kafka | 2.1.0 or later |

| Librdkafka and derived libraries | 2.1.0 or later |

For other libraries, support depends on the API version:

| API name | Version supported |

| -------------- | ----------------- |

| Metadata API | 7 or later |

| Fetch API | 9 or later|

| ListOffset API| 4 or later |

| OffsetFetch API | 5 or later |

| OffsetForLeaderEpoch API | 0 or later |

#### Event Hubs SDK and AMQP

For AMQP, users manage the checkpoint by using a checkpoint store such as Azure Blob storage or a custom storage solution. If there's a failover, the secondary region must have the checkpoint store so that clients can retrieve checkpoint data and avoid loss of messages.

The latest version of the Event Hubs SDK includes changes to checkpoint representation to support failovers. Use the [latest versions of the SDKs](sdks.md), but prior versions of the following SDKs are supported as well.

| Language | Package name|

| -------- | ----------- |

| C# | [Azure.Messaging.EventHubs](https://www.nuget.org/packages/Azure.Messaging.EventHubs/) |

| C# | [Microsoft.Azure.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) |

> [!WARNING]

> As part of the implementation, the checkpoint format is adapted when you enable geo-replication on a namespace. Subsequent checkpoints after the geo-replication pairing are written with a new format. If you force promote a secondary region to primary right after the geo-replication pairing is done but before a new checkpoint is stored (this situation might happen in the case of forced promotion or failover), new data published after promotion might be lost.

>

> In such cases, start consuming from the last committed offset. Some data might have duplicate processing and you must handle it on the client side.

>

> Upgrade to the [latest versions of the SDKs](sdks.md).

>

## Considerations

Keep in mind the following considerations:

- In your promotion planning, consider the time factor. For example, if you lose connectivity for longer than 15 to 20 minutes, you might decide to initiate the promotion.

- You should [rehearse](/azure/architecture/reliability/disaster-recovery#disaster-recovery-plan) promoting a complex distributed infrastructure at least once.

## Pricing

Pricing varies based on the tier you pick, but generally has two parameters:

* The compute charge for the cluster or namespace.

* The bandwidth charge for the data being replicated between the primary and secondary regions.

> [!NOTE]

> To determine the charges, see the pricing details listed at [Azure Event Hubs](https://azure.microsoft.com/products/event-hubs/). The geo-replication charge depends on the location of the primary region.

>

### Dedicated clusters

When you use geo-replication with Event Hubs dedicated clusters, you need at least two dedicated clusters in separate regions. You can use these clusters to host namespaces other than the one being geo-replicated. You pay for these dedicated clusters separately based on the number of Capacity Units (CUs) allocated to each.

When you enable geo-replication, the only extra charge is the bandwidth charge for the data replicated from primary to secondary. This charge depends on the location of the primary region.

### Premium namespaces

For Premium namespaces, when you enable geo-replication, you get the same number of processing units (PUs) in the secondary region. You pay for the **number of PUs** you use and the **bandwidth for the data transferred between the primary and secondary region**.

For example, if you enable geo-replication on a Premium namespace that you provisioned with **4 PUs**, you pay for

* 4 PUs in the primary region,

* 4 PUs in the secondary region,

* Geo-replication charge per GB of data replicated.

You pay bandwidth charges based on the data transferred between the primary and secondary regions.

### Pricing meters

The pricing meters for the geo-replication data transfer bandwidth charge appear with the following details:

| Product Name | Meter Description |

| --- | ---|

| Service Bus | Service Bus - Geo Replication Zone 1 GB Data Transfer - REGION NAME |

| Service Bus | Service Bus - Geo Replication Zone 2 GB Data Transfer - REGION NAME |

| Service Bus | Service Bus - Geo Replication Zone 3 GB Data Transfer - REGION NAME |

## Private endpoints

This section provides additional considerations when using geo-replication with namespaces that use private endpoints. For general information about using private endpoints with Event Hubs, see [Integrate Azure Event Hubs with Azure Private Link](private-link-service.md).

When you implement geo-replication for an Event Hubs namespace that uses private endpoints, create private endpoints for both the primary and secondary regions. Configure these endpoints against virtual networks that host both primary and secondary instances of your application. For example, if you have two virtual networks, VNET-1 and VNET-2, you need to create two private endpoints on the Event Hubs namespace, using subnets from VNET-1 and VNET-2 respectively. Set up the virtual networks with [cross-region peering](/azure/virtual-network/virtual-network-peering-overview), so that clients can communicate with either of the private endpoints. Finally, manage the [DNS](/azure/private-link/private-endpoint-dns) so all clients get the DNS information that points the namespace endpoint (namespacename.servicebus.windows.net) to the IP address of the private endpoint in the current primary region.

> [!IMPORTANT]

> When you promote a secondary region for Event Hubs, update the DNS entry to point to the corresponding endpoint.

This approach provides the benefit that failover can occur independently at the application layer or on the Event Hubs namespace:

- **Application-only failover:** In this scenario, the application moves from VNET-1 to VNET-2. Since private endpoints are configured on both VNET-1 and VNET-2 for both primary and secondary namespaces, the application continues to function seamlessly.

- **Event Hubs namespace-only failover:** If the failover occurs only at the Event Hubs namespace level, the application remains operational because private endpoints are configured on both virtual networks.

By following these guidelines, you can ensure robust and reliable failover mechanisms for your Event Hubs namespaces that use private endpoints.

## Related content

To learn how to use the Geo-replication feature, see [Use Geo-replication](use-geo-replication.md).


# Event Hubs Geo Dr

# Azure Event Hubs geo-disaster recovery

Geo-disaster recovery is a disaster recovery feature in Azure Event Hubs that continuously replicates your namespace configuration (event hubs, consumer groups, and settings) from a primary namespace to a secondary namespace. This feature enables you to initiate a failover from the primary to the secondary namespace during regional outages.

> [!NOTE]

> This article describes the geo-disaster recovery feature that replicates metadata only. For information about the geo-replication feature, which replicates both data and metadata, see [Geo-replication](./geo-replication.md).

The all-active Azure Event Hubs cluster model with [availability zone support](/azure/reliability/reliability-event-hubs) provides resiliency against hardware and datacenter outages. However, if a disaster occurs where an entire region and all zones are unavailable, you can use geo-disaster recovery to recover your workload and application configuration.

The concepts and workflow described in this article apply to disaster scenarios, not temporary outages. For a detailed discussion of disaster recovery in Microsoft Azure, see [Disaster recovery for Azure applications](/azure/architecture/resiliency/disaster-recovery-azure-applications). With geo-disaster recovery, you can initiate a once-only failover move from the primary to the secondary at any time. The failover move points the chosen alias name for the namespace to the secondary namespace. After the move, the pairing is removed. The failover is nearly instantaneous once initiated.

> [!IMPORTANT]

> - The feature enables instantaneous continuity of operations with the same configuration, but **does not replicate the event data**. Unless the disaster caused the loss of all zones, the event data that is preserved in the primary event hub after failover is recoverable and the historic events can be obtained from there once access is restored. For replicating event data and operating corresponding namespaces in active/active configurations to cope with outages and disasters, don't lean on this geo-disaster recovery feature set, but follow the [replication guidance](event-hubs-federation-overview.md).

> - Microsoft Entra role-based access control (RBAC) assignments to entities in the primary namespace aren't replicated to the secondary namespace. Create role assignments manually in the secondary namespace to secure access to them.

To set up geo-disaster recovery pairing and initiate failover, see [Configure geo-disaster recovery](configure-geo-disaster-recovery.md).

## Basic concepts and terms

The disaster recovery feature implements metadata disaster recovery and relies on primary and secondary disaster recovery namespaces. The geo-disaster recovery feature is available for the [standard, premium, and dedicated tiers](https://azure.microsoft.com/pricing/details/event-hubs/) only. You don't need to make any connection string changes, as the connection is made via an alias.

The following terms are used in this article:

- **Alias**: The name for a disaster recovery configuration that you set up. The alias provides a single stable Fully Qualified Domain Name (FQDN) connection string. Applications use this alias connection string to connect to a namespace.

- **Primary/secondary namespace**: The namespaces that correspond to the alias. The primary namespace is active and it receives messages (can be an existing or a new namespace). The secondary namespace is passive and doesn't receive messages. The metadata between both is in sync, so both can seamlessly accept messages without any application code or connection string changes. To ensure that only the active namespace receives messages, you must use the alias.

- **Metadata**: Entities such as event hubs and consumer groups, and their properties of the service that are associated with the namespace. Only entities and their settings are replicated automatically. Messages and events aren't replicated.

- **Failover**: The process of activating the secondary namespace.

## Supported namespace pairs

The following combinations of primary and secondary namespaces are supported:

| Primary namespace tier | Allowed secondary namespace tier |

| ----------------- | -------------------- |

| Standard | Standard, Dedicated |

| Premium | Premium |

| Dedicated | Dedicated |

> [!IMPORTANT]

> You can't pair namespaces that are in the same dedicated cluster. You can pair namespaces that are in separate clusters.

## Failover considerations

When planning for failover, consider the following points:

- By design, Event Hubs geo-disaster recovery doesn't replicate data. Therefore, you can't reuse the old offset value of your primary event hub on your secondary event hub. Restart your event receiver by using one of the following methods:

- *EventPosition.FromStart()* - If you want to read all data on your secondary event hub.

- *EventPosition.FromEnd()* - If you want to read all new data from the time of connection to your secondary event hub.

- *EventPosition.FromEnqueuedTime(dateTime)* - If you want to read all data received in your secondary event hub starting from a given date and time.

- Consider the time factor in your failover planning. For example, if you lose connectivity for longer than 15 to 20 minutes, you might decide to initiate the failover.

- Because no data is replicated, current active sessions aren't replicated. Additionally, duplicate detection and scheduled messages might not work. New sessions, scheduled messages, and new duplicates work.

- You should [rehearse](/azure/architecture/reliability/disaster-recovery#disaster-recovery-plan) failing over a complex distributed infrastructure at least once.

- Synchronizing entities can take some time, approximately 50-100 entities per minute.

- Some aspects of the management plane for the secondary namespace become read-only while geo-recovery pairing is active.

- The data plane of the secondary namespace is read-only while geo-recovery pairing is active. The data plane of the secondary namespace accepts GET requests to enable validation of client connectivity and access controls.

## Private endpoints

This section provides considerations when using geo-disaster recovery with namespaces that use private endpoints. To learn about using private endpoints with Event Hubs in general, see [Configure private endpoints](private-link-service.md).

### New pairings

If you try to create a pairing between a primary namespace with a private endpoint and a secondary namespace without a private endpoint, the pairing fails. The pairing succeeds only if both primary and secondary namespaces have private endpoints. Use the same configurations on the primary and secondary namespaces and on virtual networks where you create private endpoints.

> [!NOTE]

> When you try to pair the primary namespace with a private endpoint and a secondary namespace, the validation process only checks whether a private endpoint exists on the secondary namespace. It doesn't check whether the endpoint works or will work after failover. It's your responsibility to ensure that the secondary namespace with private endpoint works as expected after failover.

>

> To test that the private endpoint configurations are the same on primary and secondary namespaces, send a read request (for example: [`Get Event Hub`](/rest/api/eventhub/get-event-hub)) to the secondary namespace from outside the virtual network, and verify that you receive an error message from the service.

### Existing pairings

If a pairing between primary and secondary namespace already exists, private endpoint creation on the primary namespace fails. To resolve the error, create a private endpoint on the secondary namespace first and then create one for the primary namespace.

> [!NOTE]

> While you can access the secondary namespace as read-only, you can update the private endpoint configurations.

### Recommended configuration

When you create a disaster recovery configuration for your application and Event Hubs namespaces, create private endpoints for both primary and secondary Event Hubs namespaces. These private endpoints connect to virtual networks that host both primary and secondary instances of your application.

Suppose you have two virtual networks, `VNET-1` and `VNET-2`, and these primary and secondary namespaces: `EventHubs-Namespace1-Primary` and `EventHubs-Namespace2-Secondary`. Complete the following steps:

- On `EventHubs-Namespace1-Primary`, create two private endpoints that use subnets from `VNET-1` and `VNET-2`

- On `EventHubs-Namespace2-Secondary`, create two private endpoints that use the same subnets from `VNET-1` and `VNET-2`

![Private endpoints and virtual networks](./media/event-hubs-geo-dr/private-endpoints-virtual-networks.png)

The advantage of this approach is that failover can happen at the application layer independent of Event Hubs namespace. Consider the following scenarios:

**Application-only failover:** In this scenario, the application doesn't exist in `VNET-1` but moves to `VNET-2`. As both private endpoints are configured on both `VNET-1` and `VNET-2` for both primary and secondary namespaces, the application just works.

**Event Hubs namespace-only failover**: In this scenario, since both private endpoints are configured on both virtual networks for both primary and secondary namespaces, the application just works.

> [!NOTE]

> For guidance on geo-disaster recovery of a virtual network, see [Virtual Network - Business Continuity](../virtual-network/virtual-network-disaster-recovery-guidance.md).

## Role-based access control (RBAC)

Microsoft Entra role-based access control (RBAC) assignments to entities in the primary namespace aren't replicated to the secondary namespace. Create role assignments manually in the secondary namespace to secure access to them.

## Related content

- [Configure geo-disaster recovery](configure-geo-disaster-recovery.md)

- [Geo-replication](geo-replication.md)

- [.NET GeoDR sample](https://github.com/Azure/azure-event-hubs/tree/master/samples/Management/DotNet/GeoDRClient)

- [Java GeoDR sample](https://github.com/Azure-Samples/eventhub-java-manage-event-hub-geo-disaster-recovery)


# Configure Geo Disaster Recovery

# Configure geo-disaster recovery for Azure Event Hubs

This article shows you how to set up geo-disaster recovery pairing between Event Hubs namespaces and initiate failover. For conceptual information about this feature, see [Geo-disaster recovery overview](event-hubs-geo-dr.md).

## Prerequisites

- An Azure subscription. If you don't have one, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

- An Event Hubs namespace (Standard, Premium, or Dedicated tier). The Basic tier doesn't support geo-disaster recovery.

## Set up geo-disaster recovery pairing

To set up geo-disaster recovery, you create or use an existing primary namespace, create a secondary namespace in a different region, and then pair the two. This pairing gives you an alias that you can use to connect. Because you use an alias, you don't have to change connection strings.

> [!NOTE]

> Only new namespaces can be added to your failover pairing.

1. Create the primary namespace.

1. Create the secondary namespace in a different region. This step is optional. You can create the secondary namespace while creating the pairing in the next step.

1. In the Azure portal, navigate to your primary namespace.

1. Select **Geo-recovery** on the left menu, and select **Initiate pairing** on the toolbar.

1. On the **Initiate pairing** page, follow these steps:

1. Select an existing secondary namespace or create one in a different region.

1. For **Alias**, enter an alias for the geo-dr pairing.

1. Select **Create**.

1. On the **Geo-DR Alias** page, select **Shared access policies** on the left menu to access the primary connection string for the alias. Use this connection string instead of using the connection string to the primary or secondary namespace directly.

Finally, add monitoring to detect if a failover is necessary. In most cases, the service is one part of a large ecosystem, and automatic failovers are rarely possible because failovers must often be performed in sync with the remaining subsystem or infrastructure.

## Initiate failover

When you initiate the failover, two steps are required:

1. Set up another passive namespace and update the pairing so you can fail over again if another outage occurs.

1. Pull messages from the former primary namespace once it's available again. After that, use that namespace for regular messaging outside of your geo-recovery setup, or delete the old primary namespace.

> [!NOTE]

> Only *fail-forward* semantics are supported. When you initiate a failover with geo-disaster recovery, you can optionally re-pair with a new namespace after failover completes. Failing back to the previous primary replica isn't supported.

# [Azure portal](#tab/portal)

1. In the Azure portal, navigate to your primary namespace.

1. Select **Geo-recovery** on the left menu.

1. Select **Failover** on the toolbar.

> [!WARNING]

> Failing over activates the secondary namespace and removes the primary namespace from the geo-disaster recovery pairing. Create another namespace to have a new geo-disaster recovery pair.

# [Azure CLI](#tab/cli)

Use the [`az eventhubs georecovery-alias fail-over`](/cli/azure/eventhubs/georecovery-alias#az-eventhubs-georecovery-alias-fail-over) command.

# [Azure PowerShell](#tab/powershell)

Use the [`Set-AzEventHubGeoDRConfigurationFailOver`](/powershell/module/az.eventhub/set-azeventhubgeodrconfigurationfailover) cmdlet.

# [C#](#tab/csharp)

Use the [`DisasterRecoveryConfigsOperationsExtensions.FailOverAsync`](/dotnet/api/microsoft.azure.management.eventhub.disasterrecoveryconfigsoperationsextensions.failoverasync) method.

For sample code that uses this method, see the [`GeoDRClient`](https://github.com/Azure/azure-event-hubs/blob/3cb13d5d87385b97121144b0615bec5109415c5a/samples/Management/DotNet/GeoDRClient/GeoDRClient/GeoDisasterRecoveryClient.cs#L137) sample in GitHub.

---

## Break pairing

If you made a mistake (for example, you paired the wrong regions during the initial setup), you can break the pairing of the two namespaces at any time.

1. In the Azure portal, navigate to your primary namespace.

1. Select **Geo-recovery** on the left menu.

1. Select **Break pairing** on the toolbar.

If you want to use the paired namespaces as regular namespaces, delete the alias.

## Related content

- [Geo-disaster recovery overview](event-hubs-geo-dr.md)

- [Geo-replication](geo-replication.md)

- [.NET GeoDR sample](https://github.com/Azure/azure-event-hubs/tree/master/samples/Management/DotNet/GeoDRClient)

- [Java GeoDR sample](https://github.com/Azure-Samples/eventhub-java-manage-event-hub-geo-disaster-recovery)


# Authorize Access Event Hubs

# Authorize access to Azure Event Hubs

Every time you publish or consume events from an event hub, your client accesses Event Hubs resources. Each request to a secure resource must be authorized to ensure the client has the required permissions to publish or consume data.

Azure Event Hubs provides these options for authorizing access to secure resources:

- Microsoft Entra ID

- Shared access signature

> [!NOTE]

> This article applies to Event Hubs and [Apache Kafka](azure-event-hubs-apache-kafka-overview.md) scenarios.

## Microsoft Entra ID

Microsoft Entra integration with Event Hubs resources lets you use Azure role-based access control (RBAC) for fine-grained control over a client's access to resources. Use Azure RBAC to grant permissions to a security principal, which might be a user, a group, or an application service principal. Microsoft Entra authenticates the security principal, then returns an OAuth 2.0 token. The token can be used to authorize a request to access an Event Hubs resource.

For more information about authenticating with Microsoft Entra ID, see the following articles:

- [Authenticate requests to Azure Event Hubs using Microsoft Entra ID](authenticate-application.md)

- [Authorize access to Event Hubs resources using Microsoft Entra ID](authorize-access-azure-active-directory.md)

## Shared access signatures

Shared access signatures (SAS) for Event Hubs resources let you delegate limited access to Event Hubs resources. Adding constraints on the time interval when the signature is valid or on the permissions it grants gives flexibility in managing resources. For more information, see [Authenticate using shared access signatures (SAS)](authenticate-shared-access-signature.md).

Authorizing users or applications with an OAuth 2.0 token from Microsoft Entra ID offers better security and ease of use than shared access signatures (SAS). With Microsoft Entra ID, you don't need to store access tokens with your code, reducing potential security risks. While you can continue to use shared access signatures (SAS) to grant fine-grained access to Event Hubs resources, Microsoft Entra ID offers similar capabilities without the need to manage SAS tokens or worry about revoking a compromised SAS.

By default, all Event Hubs resources are secured and available only to the account owner. Although you can use any of the authorization strategies outlined above to grant clients access to Event Hubs resources, Microsoft recommends using Microsoft Entra ID when possible for maximum security and ease of use.

For more information about authorization using SAS, see [Authorizing access to Event Hubs resources using Shared Access Signatures](authorize-access-shared-access-signature.md).

## Next steps

- Review [Azure RBAC samples](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/Rbac) in our GitHub repository.

- See these articles:

- [Authenticate requests to Azure Event Hubs from an application using Microsoft Entra ID](authenticate-application.md).

- [Authenticate a managed identity with Microsoft Entra ID to access Event Hubs resources](authenticate-managed-identity.md).

- [Authenticate requests to Azure Event Hubs using shared access signatures](authenticate-shared-access-signature.md).

- [Authorize access to Event Hubs resources using Microsoft Entra ID](authorize-access-azure-active-directory.md).

- [Authorize access to Event Hubs resources using shared access signatures](authorize-access-shared-access-signature.md).


# Authenticate Shared Access Signature

# Authenticate access to Event Hubs resources using shared access signatures (SAS)

Shared access signature (SAS) gives you granular control over the type of access you grant to the clients. Here are some of the controls you can set in a SAS:

- The interval over which the SAS is valid, which includes the start time and expiry time.

- The permissions granted by the SAS. For example, a SAS for an Event Hubs namespace might grant the permission to listen for event, but not the permission to send events.

- Only clients that present valid credentials can send data to an event hub.

- A client can't impersonate another client.

- A rogue client can be blocked from sending data to an event hub.

This article covers authenticating the access to Event Hubs resources using SAS. To learn about **authorizing** access to Event Hubs resources using SAS, see [this article](authorize-access-shared-access-signature.md).

> [!NOTE]

> We recommend that you use Microsoft Entra credentials when possible as a security best practice, rather than using the shared access signatures, which can be more easily compromised. While you can continue to use shared access signatures (SAS) to grant fine-grained access to your Event Hubs resources, Microsoft Entra ID offers similar capabilities without the need to manage SAS tokens or worry about revoking a compromised SAS.

>

> For more information about Microsoft Entra integration in Azure Event Hubs, see [Authorize access to Event Hubs using Microsoft Entra ID](authorize-access-azure-active-directory.md).

## Configuring for SAS authentication

You can configure a SAS rule on an Event Hubs namespace, or an entity (event hub or Kafka topic). Configuring a SAS rule on a consumer group is currently not supported, but you can use rules configured on a namespace or entity to secure access to consumer group. The following image shows how the authorization rules apply on sample entities.

![Diagram that shows event hubs with listen, send, and manage rules.](./media/authenticate-shared-access-signature/configure-sas-authorization-rule.png)

In this example, the sample Event Hubs namespace (ExampleNamespace) has two entities: eh1 and Kafka topic1. The authorization rules are defined both at the entity level and also at the namespace level.

The manageRuleNS, sendRuleNS, and listenRuleNS authorization rules apply to both eh1 and topic1. The listenRule-eh and sendRule-eh authorization rules apply only to eh1 and sendRuleT authorization rule applies only to topic1.

When you use sendRuleNS authorization rule, client applications can send to both eh1 and topic1. When sendRuleT authorization rule is used, it enforces granular access to topic1 only and hence client applications using this rule for access now can't send to eh1, but only to topic1.

## Generate a Shared Access Signature token

Any client that has access to name of an authorization rule name and one of its signing keys can generate a SAS token. The token is generated by crafting a string in the following format:

- `se`  – Token expiry instant. Integer reflecting seconds since epoch 00:00:00 UTC on 1 January 1970 (UNIX epoch) when the token expires

- `skn` – Name of the authorization rule, which is the SAS key name.

- `sr` – URI of the resource being accessed.

- `sig` – Signature.

The signature-string is the SHA-256 hash computed over the resource URI (scope as described in the previous section) and the string representation of the token expiry instant, separated by line feed (LF). The hash computation looks similar to the following pseudo code and returns a 256-bit/32-byte hash value.

```

SHA-256('https://<yournamespace>.servicebus.windows.net/'+'\n'+ 1438205742)

```

The token contains the nonhashed values so that the recipient can recompute the hash with the same parameters, verifying that the issuer is in possession of a valid signing key.

The resource URI is the full URI of the Service Bus resource to which access is claimed. For example, `http://<namespace>.servicebus.windows.net/<entityPath>` or `sb://<namespace>.servicebus.windows.net/<entityPath>` that is, `http://contoso.servicebus.windows.net/eh1`.

The URI must be percent-encoded.

The SAS rule used for signing must be configured on the entity specified by this URI, or by one of its hierarchical parents. For example, `http://contoso.servicebus.windows.net/eh1` or `http://contoso.servicebus.windows.net` in the previous example.

A SAS token is valid for all resources prefixed with the `<resourceURI>` used in the signature-string.

> [!NOTE]

> You generate an access token for Event Hubs using shared access policy. For more information, see [Shared access authorization policy](authorize-access-shared-access-signature.md#shared-access-authorization-policies).

### Generating a signature(token) from a policy

Following section shows generating a SAS token using shared access signature policies,

#### NodeJS

```javascript

function createSharedAccessToken(uri, saName, saKey) {

if (!uri || !saName || !saKey) {

throw "Missing required parameter";

}

var encoded = encodeURIComponent(uri);

var now = new Date();

var week = 60*60*24*7;

var ttl = Math.round(now.getTime() / 1000) + week;

var signature = encoded + '\n' + ttl;

var hash = crypto.createHmac('sha256', saKey).update(signature, 'utf8').digest('base64');

return 'SharedAccessSignature sr=' + encoded + '&sig=' +

encodeURIComponent(hash) + '&se=' + ttl + '&skn=' + saName;

}

```

To use a policy name and a key value to connect to an event hub, use the `EventHubProducerClient` constructor that takes the `AzureNamedKeyCredential` parameter.

```javascript

const producer = new EventHubProducerClient("NAMESPACE NAME.servicebus.windows.net", eventHubName, new AzureNamedKeyCredential("POLICYNAME", "KEYVALUE"));

```

You need to add a reference to `AzureNamedKeyCredential`.

```javascript

const { AzureNamedKeyCredential } = require("@azure/core-auth");

```

To use a SAS token that you generated using the code, use the `EventHubProducerClient` constructor that takes the `AzureSASCredential` parameter.

```javascript

var token = createSharedAccessToken("https://NAMESPACENAME.servicebus.windows.net", "POLICYNAME", "KEYVALUE");

const producer = new EventHubProducerClient("NAMESPACENAME.servicebus.windows.net", eventHubName, new AzureSASCredential(token));

```

You need to add a reference to `AzureSASCredential`.

```javascript

const { AzureSASCredential } = require("@azure/core-auth");

```

#### JAVA

```java

private static String GetSASToken(String resourceUri, String keyName, String key)

{

long epoch = System.currentTimeMillis()/1000L;

int week = 60*60*24*7;

String expiry = Long.toString(epoch + week);

String sasToken = null;

try {

String stringToSign = URLEncoder.encode(resourceUri, "UTF-8") + "\n" + expiry;

String signature = getHMAC256(key, stringToSign);

sasToken = "SharedAccessSignature sr=" + URLEncoder.encode(resourceUri, "UTF-8") +"&sig=" +

URLEncoder.encode(signature, "UTF-8") + "&se=" + expiry + "&skn=" + keyName;

} catch (UnsupportedEncodingException e) {

e.printStackTrace();

}

return sasToken;

}

public static String getHMAC256(String key, String input) {

Mac sha256_HMAC = null;

String hash = null;

try {

sha256_HMAC = Mac.getInstance("HmacSHA256");

SecretKeySpec secret_key = new SecretKeySpec(key.getBytes(), "HmacSHA256");

sha256_HMAC.init(secret_key);

Encoder encoder = Base64.getEncoder();

hash = new String(encoder.encode(sha256_HMAC.doFinal(input.getBytes("UTF-8"))));

} catch (InvalidKeyException e) {

e.printStackTrace();

} catch (NoSuchAlgorithmException e) {

e.printStackTrace();

} catch (IllegalStateException e) {

e.printStackTrace();

} catch (UnsupportedEncodingException e) {

e.printStackTrace();

}

return hash;

}

```

#### PHP

```php

function generateSasToken($uri, $sasKeyName, $sasKeyValue)

{

$targetUri = strtolower(rawurlencode(strtolower($uri)));

$expires = time();

$expiresInMins = 60;

$week = 60*60*24*7;

$expires = $expires + $week;

$toSign = $targetUri . "\n" . $expires;

$signature = rawurlencode(base64_encode(hash_hmac('sha256',

$toSign, $sasKeyValue, TRUE)));

$token = "SharedAccessSignature sr=" . $targetUri . "&sig=" . $signature . "&se=" . $expires . 		"&skn=" . $sasKeyName;

return $token;

}

```

#### C#

```csharp

private static string createToken(string resourceUri, string keyName, string key)

{

TimeSpan sinceEpoch = DateTime.UtcNow - new DateTime(1970, 1, 1);

var week = 60 * 60 * 24 * 7;

var expiry = Convert.ToString((int)sinceEpoch.TotalSeconds + week);

string stringToSign = HttpUtility.UrlEncode(resourceUri) + "\n" + expiry;

using (var hmac = new HMACSHA256(Encoding.UTF8.GetBytes(key)))

{

var signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(stringToSign)));

var sasToken = String.Format(CultureInfo.InvariantCulture, "SharedAccessSignature sr={0}&sig={1}&se={2}&skn={3}", HttpUtility.UrlEncode(resourceUri), HttpUtility.UrlEncode(signature), expiry, keyName);

return sasToken;

}

}

```

#### PowerShell

```azurepowershell-interactive

[Reflection.Assembly]::LoadWithPartialName("System.Web")| out-null

$URI="myNamespace.servicebus.windows.net/myEventHub/"

$Access_Policy_Name="RootManageSharedAccessKey"

$Access_Policy_Key="myPrimaryKey"

#Token expires now+300

$Expires=([DateTimeOffset]::Now.ToUnixTimeSeconds())+300

$SignatureString=[System.Web.HttpUtility]::UrlEncode($URI)+ "`n" + [string]$Expires

$HMAC = New-Object System.Security.Cryptography.HMACSHA256

$HMAC.key = [Text.Encoding]::ASCII.GetBytes($Access_Policy_Key)

$Signature = $HMAC.ComputeHash([Text.Encoding]::ASCII.GetBytes($SignatureString))

$Signature = [Convert]::ToBase64String($Signature)

$SASToken = "SharedAccessSignature sr=" + [System.Web.HttpUtility]::UrlEncode($URI) + "&sig=" + [System.Web.HttpUtility]::UrlEncode($Signature) + "&se=" + $Expires + "&skn=" + $Access_Policy_Name

$SASToken

```

#### BASH

```bash

get_sas_token() {

local EVENTHUB_URI='EVENTHUBURI'

local SHARED_ACCESS_KEY_NAME='SHAREDACCESSKEYNAME'

local SHARED_ACCESS_KEY='SHAREDACCESSKEYVALUE'

local EXPIRY=${EXPIRY:=$((60 * 60 * 24))} # Default token expiry is 1 day

local ENCODED_URI=$(echo -n $EVENTHUB_URI | jq -s -R -r @uri)

local TTL=$(($(date +%s) + $EXPIRY))

local UTF8_SIGNATURE=$(printf "%s\n%s" $ENCODED_URI $TTL | iconv -t utf8)

local HASH=$(echo -n "$UTF8_SIGNATURE" | openssl sha256 -hmac $SHARED_ACCESS_KEY -binary | base64)

local ENCODED_HASH=$(echo -n $HASH | jq -s -R -r @uri)

echo -n "SharedAccessSignature sr=$ENCODED_URI&sig=$ENCODED_HASH&se=$TTL&skn=$SHARED_ACCESS_KEY_NAME"

}

```

## Authenticating Event Hubs publishers with SAS

An event publisher defines a virtual endpoint for an event hub. The publisher can only be used to send messages to an event hub and not receive messages.

Typically, an event hub employs one publisher per client. All messages that are sent to any of the publishers of an event hub are enqueued within that event hub. Publishers enable fine-grained access control.

A unique token is assigned to each Event Hubs client, which is uploaded to the client. The tokens are produced such that each unique token grants access to different unique publisher. A client that holds a token can only send to one publisher, and no other publisher. If multiple clients share the same token, then each of them shares the publisher.

All tokens are assigned with SAS keys. Typically, all tokens are signed with the same key. Clients aren't aware of the key, which prevents clients from manufacturing tokens. Clients operate on the same tokens until they expire.

For example, to define authorization rules scoped down to only sending/publishing to Event Hubs, you need to define a send authorization rule. It can be done at a namespace level or give more granular scope to a particular entity (event hubs instance or a topic). A client or an application that is scoped with such granular access is called, Event Hubs publisher. To do so, follow these steps:

1. Create a SAS key on the entity you want to publish to assign the **send** scope on it. For more information, see [Shared access authorization policies](authorize-access-shared-access-signature.md#shared-access-authorization-policies).

2. Generate a SAS token with an expiry time for a specific publisher by using the key generated in step1. For the sample code, see [Generating a signature(token) from a policy](#generating-a-signaturetoken-from-a-policy).

3. Provide the token to the publisher client, which can only send to the entity and the publisher that token grants access to.

Once the token expires, the client loses its access to send/publish to the entity.

> [!NOTE]

> Although we don't recommend it, it's possible to equip devices with tokens that grant access to an event hub or a namespace. Any device that holds this token can send messages directly to that event hub. Furthermore, the device can't be blocklisted from sending to that event hub.

>

> We recommend that you give specific and granular scopes.

> [!IMPORTANT]

> Once the tokens are created, each client is provisioned with its own unique token.

>

> When the client sends data into an event hub, it tags its request with the token. To prevent an attacker from eavesdropping and stealing the token, the communication between the client and the event hub must occur over an encrypted channel.

>

> If an attacker steals a token, the attacker can impersonate the client whose token has been stolen. Disallowing a publisher, renders that client unusable until it receives a new token that uses a different publisher.

## Authenticating Event Hubs consumers with SAS

To authenticate back-end applications that consume data generated by Event Hubs producers, Event Hubs token authentication requires its clients to have either the **manage** rights or the **listen** privileges assigned to its Event Hubs namespace or event hub instance or topic. Data is consumed from Event Hubs using consumer groups. While SAS policy gives you granular scope, this scope is defined only at the entity level and not at the consumer level. It means that the privileges defined at the namespace level or the event hub or topic level are applied to the consumer groups of that entity.

## Disable local/SAS Key authentication

For certain organizational security requirements, you want to disable local/SAS key authentication completely and rely on the Microsoft Entra ID based authentication, which is the recommended way to connect with Azure Event Hubs. You can disable local/SAS key authentication at the Event Hubs namespace level using Azure portal or Azure Resource Manager template.

### Disable local/SAS Key authentication via the portal

You can disable local/SAS key authentication for a given Event Hubs namespace using the Azure portal.

1. Navigate to your Event Hubs namespace in the Azure portal.

1. On the **Overview** page, select **Enabled** for **Local Authentication** as shown in the following image.

1. On the **Local Authentication** popup, select **Disabled**, and select **OK**.

![Screenshot that shows the Local Authentication popup with the Disabled option selected.](./media/authenticate-shared-access-signature/disabling-local-auth.png)

### Disable local/SAS Key authentication using a template

You can disable local authentication for a given Event Hubs namespace by setting `disableLocalAuth` property to `true` as shown in the following Azure Resource Manager template (ARM Template).

```json

"resources":[

{

"apiVersion":"[variables('ehVersion')]",

"name":"[parameters('eventHubNamespaceName')]",

"type":"Microsoft.EventHub/Namespaces",

"location":"[variables('location')]",

"sku":{

"name":"Standard",

"tier":"Standard"

},

"resources": [

{

"apiVersion": "2017-04-01",

"name": "[parameters('eventHubNamespaceName')]",

"type": "Microsoft.EventHub/Namespaces",

"location": "[resourceGroup().location]",

"sku": {

"name": "Standard"

},

"properties": {

"isAutoInflateEnabled": "true",

"maximumThroughputUnits": "7",

"disableLocalAuth": true

},

"resources": [

{

"apiVersion": "2017-04-01",

"name": "[parameters('eventHubName')]",

"type": "EventHubs",

"dependsOn": [

"[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"

],

"properties": {

"messageRetentionInDays": "[parameters('messageRetentionInDays')]",

"partitionCount": "[parameters('partitionCount')]"

}

}

]

}

]

```

## Samples

- See the .NET sample #6 in [this GitHub location](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/eventhub/Azure.Messaging.EventHubs/samples) to learn how to publish events to an event hub using shared access credentials or the default Azure credential identity.

- See the .NET sample #5 in [this GitHub location](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/eventhub/Azure.Messaging.EventHubs.Processor/samples) to learn how to consume or process events using shared access credentials or the default Azure credential identity.

## Next steps

Now that you understand SAS authentication, explore these related topics:

**Secure your Event Hubs further:**

- [Authorize access using Shared Access Signatures](authenticate-shared-access-signature.md) - Learn authorization concepts

- [Use Azure role-based access control (RBAC)](authorize-access-azure-active-directory.md) - Implement enterprise-grade security


# Authorize Access Shared Access Signature

# Shared access signature authorization for Event Hubs

A shared access signature (SAS) provides a way to grant limited access to resources in your Event Hubs namespace. SAS guards access to Event Hubs resources based on authorization rules. You configure these rules on either a namespace or an event hub. This article provides an overview of the SAS model and reviews SAS best practices.

> [!NOTE]

> This article covers authorizing access to Event Hubs resources using SAS. To learn about **authenticating** access to Event Hubs resources using SAS, see [Authenticate with SAS](authenticate-shared-access-signature.md).

## What are shared access signatures?

A shared access signature (SAS) provides delegated access to Event Hubs resources based on authorization rules. An authorization rule has a name, is associated with specific rights, and carries a pair of cryptographic keys. Use the rule’s name and key through the Event Hubs clients or in your own code to generate SAS tokens. A client can then pass the token to Event Hubs to prove authorization for the requested operation.

SAS is a claim-based authorization mechanism that uses simple tokens. When you use SAS, you never pass keys on the wire. Instead, you use keys to cryptographically sign information that the service can later verify. You can use SAS similar to a username and password scheme where the client is in immediate possession of an authorization rule name and a matching key. You can also use SAS similar to a federated security model, where the client receives a time-limited and signed access token from a security token service without ever coming into possession of the signing key.

> [!NOTE]

> Azure Event Hubs also supports authorizing to Event Hubs resources by using Microsoft Entra ID. Authorizing users or applications by using OAuth 2.0 token returned by Microsoft Entra ID provides superior security and ease of use over shared access signatures (SAS). By using Microsoft Entra ID, there's no need to store the tokens in your code and risk potential security vulnerabilities.

>

> Microsoft recommends using Microsoft Entra ID with your Azure Event Hubs applications when possible. For more information, see [Authorize access to Azure Event Hubs resource using Microsoft Entra ID](authorize-access-azure-active-directory.md).

> [!IMPORTANT]

> SAS tokens are critical to protecting your resources. While providing granularity, SAS grants clients access to your Event Hubs resources. Don't share them publicly. When sharing, if required for troubleshooting reasons, consider using a reduced version of any log files or deleting the SAS tokens (if present) from the log files. Make sure the screenshots don't contain the SAS information either.

## Shared access authorization policies

Each Event Hubs namespace and each Event Hubs entity (an event hub or a Kafka topic) has a shared access authorization policy made up of rules. The policy at the namespace level applies to all entities inside the namespace, irrespective of their individual policy configuration.

For each authorization policy rule, you decide on three pieces of information: name, scope, and rights. The name is a unique name in that scope. The scope is the URI of the resource in question. For an Event Hubs namespace, the scope is the fully qualified domain name (FQDN), such as `https://<yournamespace>.servicebus.windows.net/`.

The rights provided by the policy rule can be a combination of:

- **Send** – Gives the right to send messages to the entity

- **Listen** – Gives the right to listen or receive messages from the entity

- **Manage** – Gives the right to manage the topology of the namespace, including creation and deletion of entities. The **Manage** right includes the **Send** and **Listen** rights.

A namespace or entity policy can hold up to 12 shared access authorization rules, providing room for the three sets of rules, each covering the basic rights, and the combination of Send and Listen. This limit underlines that the SAS policy store isn't intended to be a user or service account store. If your application needs to grant access to Event Hubs resources based on user or service identities, it should implement a security token service that issues SAS tokens after an authentication and access check.

An authorization rule is assigned a **primary key** and a **secondary key**. These keys are cryptographically strong keys. Don’t lose them or leak them. They’re always available in the Azure portal. You can use either of the generated keys, and you can regenerate them at any time. If you regenerate or change a key in the policy, all previously issued tokens based on that key become instantly invalid. However, ongoing connections created based on such tokens continue to work until the token expires.

When you create an Event Hubs namespace, a policy rule named **RootManageSharedAccessKey** is automatically created for the namespace. This policy has **manage** permissions for the entire namespace. Treat this rule like an administrative root account and don't use it in your application. You can create more policy rules in the **Configure** tab for the namespace in the portal, via PowerShell, or Azure CLI.

## Best practices when using SAS

When you use shared access signatures in your applications, be aware of two potential risks:

- If a SAS leaks, anyone who obtains it can use it, which can potentially compromise your Event Hubs resources.

- If a SAS provided to a client application expires and the application can't retrieve a new SAS from your service, the application's functionality might be hindered.

The following recommendations for using shared access signatures can help mitigate these risks:

- **Have clients automatically renew the SAS if necessary**: Clients should renew the SAS well before expiration to allow time for retries if the service providing the SAS is unavailable. If your SAS is meant for a small number of immediate, short-lived operations that are expected to complete within the expiration period, then renewal might be unnecessary. However, if you have a client that routinely makes requests via SAS, then the possibility of expiration comes into play. The key consideration is to balance the need for the SAS to be short-lived (as previously stated) with the need to ensure that the client requests renewal early enough (to avoid disruption due to the SAS expiring before a successful renewal).

- **Be careful with the SAS start time**: If you set the start time for SAS to **now**, then due to clock skew (differences in current time according to different machines), failures might occur intermittently for the first few minutes. In general, set the start time to be at least 15 minutes in the past. Or, don't set it at all, which makes it valid immediately in all cases. The same generally applies to the expiry time as well. Remember that you might observe up to 15 minutes of clock skew in either direction on any request.

- **Be specific with the resource to be accessed**: A security best practice is to provide users with the minimum required privileges. If a user only needs read access to a single entity, grant them read access to that single entity, and not read, write, or delete access to all entities. This approach also helps lessen the damage if a SAS is compromised because the SAS has less power in the hands of an attacker.

- **Don't always use SAS**: Sometimes the risks associated with a particular operation against your Event Hubs outweigh the benefits of SAS. For such operations, create a middle-tier service that writes to your event hubs after business rule validation, authentication, and auditing.

- **Always use HTTPS**: Always use HTTPS to create or distribute a SAS. If a SAS is passed over HTTP and intercepted, an attacker performing a man-in-the-middle attack can read the SAS and then use it just as the intended user could, potentially compromising sensitive data or allowing for data corruption by the malicious user.

## Conclusion

Shared access signatures are useful for providing limited permissions to Event Hubs resources to your clients. They're a vital part of the security model for any application using Azure Event Hubs. If you follow the best practices listed in this article, you can use SAS to provide greater flexibility of access to your resources, without compromising the security of your application.

## Related content

See the following related articles:

- [Authenticate requests to Azure Event Hubs using Shared Access Signatures](authenticate-shared-access-signature.md)

- [Authenticate requests to Azure Event Hubs from an application using Microsoft Entra ID](authenticate-application.md)

- [Authenticate a managed identity with Microsoft Entra ID to access Event Hubs Resources](authenticate-managed-identity.md)


# Authenticate Managed Identity

# Authenticate a managed identity with Microsoft Entra ID to access Event Hubs Resources

Azure Event Hubs supports Microsoft Entra authentication with [managed identities for Azure resources](../active-directory/managed-identities-azure-resources/overview.md). Managed identities for Azure resources can authorize access to Event Hubs resources using Microsoft Entra credentials from applications running in Azure Virtual Machines (VMs), Function apps, Virtual Machine Scale Sets, and other services. By using managed identities for Azure resources together with Microsoft Entra authentication, you can avoid storing credentials with your applications that run in the cloud. This article shows how to authorize access to an event hub by using a managed identity from an Azure VM.

## Enable managed identities on a VM

Before you use managed identities for Azure resources to access Event Hubs resources from your VM, you must first enable managed identities for Azure Resources on the VM. To learn how to enable managed identities for Azure resources, see [Configure managed identities on Azure VMs](../active-directory/managed-identities-azure-resources/qs-configure-portal-windows-vm.md).

## Grant permissions to a managed identity in Microsoft Entra ID

To authorize a request to Event Hubs service from a managed identity in your application, first configure Azure role-based access control (RBAC) settings for that managed identity. Azure Event Hubs defines Azure roles that encompass permissions for sending events to and receiving events from Event Hubs. When an Azure role is assigned to a managed identity, the managed identity is granted access to Event Hubs data at the appropriate scope. For more information about assigning Azure roles, see [Authenticate with Microsoft Entra ID for access to Event Hubs resources](authorize-access-azure-active-directory.md).

## Sample application

The procedure in this section uses a simple application that runs under a managed identity and accesses Event Hubs resources.

Here we're using a sample web application hosted in [Azure App Service](https://azure.microsoft.com/services/app-service/). For step-by-step instructions for creating a web application, see [Create an ASP.NET Core web app in Azure](../app-service/quickstart-dotnetcore.md)

Once the application is created, follow these steps:

1. Go to **Settings** and select **Identity**.

1. Select the **Status** to be **On**.

1. Select **Save** to save the setting.

4. Select **Yes** on the information message.

Once you've enabled this setting, a new service identity is created in your Microsoft Entra ID and configured into the App Service host.

Now, assign this service identity to a role in the required scope in your Event Hubs resources.

### To Assign Azure roles using the Azure portal

Assign one of the [Event Hubs roles](authorize-access-azure-active-directory.md#azure-built-in-roles-for-azure-event-hubs) to the managed identity at the desired scope (Event Hubs namespace, resource group, subscription). For detailed steps, see [Assign Azure roles using the Azure portal](/azure/role-based-access-control/role-assignments-portal).

> [!NOTE]

> For a list of services that support managed identities, see [Services that support managed identities for Azure resources](../active-directory/managed-identities-azure-resources/services-support-managed-identities.md).

### Test the web application

1. Create an Event Hubs namespace and an event hub.

2. Deploy the web app to Azure. See the following tabbed section for links to the sample web application on GitHub.

3. Ensure that the SendReceive.aspx is set as the default document for the web app.

3. Enable **identity** for the web app.

4. Assign this identity to the **Event Hubs Data Owner** role at the namespace level or event hub level.

5. Run the web application, enter the namespace name and event hub name, a message, and select **Send**. To receive the event, select **Receive**.

You can find the sample web application that sends and receives data from Event Hubs resources in the [GitHub repo](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Azure.Messaging.EventHubs/ManagedIdentityWebApp).

Install the latest package from [NuGet](https://www.nuget.org/packages/Azure.Messaging.EventHubs/), and start sending events to Event Hubs using **EventHubProducerClient** and receiving events using **EventHubConsumerClient**.

> [!NOTE]

> For a Java sample that uses a managed identity to publish events to an event hub, see [Publish events with Azure identity sample on GitHub](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/eventhubs/azure-messaging-eventhubs/src/samples/java/com/azure/messaging/eventhubs).

```csharp

protected async void btnSend_Click(object sender, EventArgs e)

{

await using (EventHubProducerClient producerClient = new EventHubProducerClient(txtNamespace.Text, txtEventHub.Text, new DefaultAzureCredential()))

{

// create a batch

using (EventDataBatch eventBatch = await producerClient.CreateBatchAsync())

{

// add events to the batch. only one in this case.

eventBatch.TryAdd(new EventData(Encoding.UTF8.GetBytes(txtData.Text)));

// send the batch to the event hub

await producerClient.SendAsync(eventBatch);

}

txtOutput.Text = $"{DateTime.Now} - SENT{Environment.NewLine}{txtOutput.Text}";

}

}

protected async void btnReceive_Click(object sender, EventArgs e)

{

await using (var consumerClient = new EventHubConsumerClient(EventHubConsumerClient.DefaultConsumerGroupName, $"{txtNamespace.Text}.servicebus.windows.net", txtEventHub.Text, new DefaultAzureCredential()))

{

int eventsRead = 0;

try

{

using CancellationTokenSource cancellationSource = new CancellationTokenSource();

cancellationSource.CancelAfter(TimeSpan.FromSeconds(5));

await foreach (PartitionEvent partitionEvent in consumerClient.ReadEventsAsync(cancellationSource.Token))

{

txtOutput.Text = $"Event Read: { Encoding.UTF8.GetString(partitionEvent.Data.Body.ToArray()) }{ Environment.NewLine}" + txtOutput.Text;

eventsRead++;

}

}

catch (TaskCanceledException ex)

{

txtOutput.Text = $"Number of events read: {eventsRead}{ Environment.NewLine}" + txtOutput.Text;

}

}

}

```

> [!NOTE]

> If the source service or app doesn't restart after the access to the event hub is disabled by removing the source's managed identity from the Event Hubs RBAC role, the source app may continue to publish events to or receiev events from the event hub until the token expires (default token validity is 24 hours). This behavior is by design.

>

> Therefore, after you remove the source's managed identity from the RBAC role, restart the source app or service to immediately expire the token and prevent it from sending events to or receiving events from the event hub.

## Event Hubs for Kafka

You can use Apache Kafka applications to send messages to and receive messages from Azure Event Hubs using managed identity OAuth. See the following sample on GitHub: [Event Hubs for Kafka - send and receive messages using managed identity OAuth](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/oauth/java/managedidentity).

## Samples

- .NET.

- For a sample that uses the latest **Azure.Messaging.EventHubs** package, see [Publish events with a managed identity](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Azure.Messaging.EventHubs/ManagedIdentityWebApp)

- For a sample that uses the legacy **Microsoft.Azure.EventHubs** package, see [this .NET sample on GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/Rbac/ManagedIdentityWebApp)

- Java - see the following samples.

- **Publish events with Azure identity** sample on [GitHub](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/eventhubs/azure-messaging-eventhubs/src/samples/java/com/azure/messaging/eventhubs).

- To learn how to use the Apache Kafka protocol to send events to and receive events from an event hub using a managed identity, see [Event Hubs for Kafka sample to send and receive messages using a managed identity](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/oauth/java/managedidentity).

## Related content

- See the following article to learn about managed identities for Azure resources: [What is managed identities for Azure resources?](../active-directory/managed-identities-azure-resources/overview.md)

- See the following related articles:

- [Authenticate requests to Azure Event Hubs from an application using Microsoft Entra ID](authenticate-application.md)

- [Authenticate requests to Azure Event Hubs using Shared Access Signatures](authenticate-shared-access-signature.md)

- [Authorize access to Event Hubs resources using Microsoft Entra ID](authorize-access-azure-active-directory.md)

- [Authorize access to Event Hubs resources using Shared Access Signatures](authorize-access-shared-access-signature.md)


# Authenticate Application

# Authenticate an application with Microsoft Entra ID to access Event Hubs

Microsoft Azure provides integrated access control management for resources and applications based on Microsoft Entra ID. A key advantage of using Microsoft Entra ID with Azure Event Hubs is that you don't need to store credentials in code. Instead, request an OAuth 2.0 access token from the Microsoft identity platform. The resource name to request a token is `https://eventhubs.azure.net/`, and it's the same for all clouds/tenants (For Kafka clients, the resource to request a token is `https://<namespace>.servicebus.windows.net`). Microsoft Entra authenticates the security principal, such as a user, group, service principal, or managed identity, running the application. If authentication succeeds, Microsoft Entra ID returns an access token to the application, which can then use the token to authorize requests to Azure Event Hubs resources.

When a role is assigned to a Microsoft Entra security principal, Azure grants access to those resources for that security principal. Access can be scoped to the subscription, resource group, Event Hubs namespace, or any resource under it. A Microsoft Entra security principal can assign roles to a user, group, application service principal, or a [managed identity for Azure resources](../active-directory/managed-identities-azure-resources/overview.md).

> [!NOTE]

> A role definition is a collection of permissions. Azure role-based access control (Azure RBAC) enforces these permissions through role assignment. A role assignment includes three elements: security principal, role definition, and scope. For more information, see [Understanding the different roles](../role-based-access-control/overview.md).

## Built-in roles for Azure Event Hubs

Azure provides these built-in roles to authorize access to Event Hubs data using Microsoft Entra ID and OAuth:

- [Azure Event Hubs Data Owner](../role-based-access-control/built-in-roles.md#azure-event-hubs-data-owner): Use this role to give complete access to Event Hubs resources.

- [Azure Event Hubs Data Sender](../role-based-access-control/built-in-roles.md#azure-event-hubs-data-sender): A security principal assigned to this role can send events to a specific event hub or all event hubs in a namespace.

- [Azure Event Hubs Data Receiver](../role-based-access-control/built-in-roles.md#azure-event-hubs-data-receiver): A security principal assigned to this role can receive events from a specific event hub or all event hubs in a namespace.

For Schema Registry built-in roles, see [Schema Registry roles](schema-registry-concepts.md#azure-role-based-access-control).

> [!IMPORTANT]

> The preview release supported adding Event Hubs data access privileges to the Owner or Contributor role. However, these privileges are no longer honored. If you're using the Owner or Contributor role, switch to the Azure Event Hubs Data Owner role.

## Authenticate from an application

A key advantage of using Microsoft Entra ID with Event Hubs is that you don't need to store your credentials in your code. Instead, request an OAuth 2.0 access token from Microsoft identity platform. Microsoft Entra authenticates the security principal (a user, a group, or service principal) running the application. If authentication succeeds, Microsoft Entra ID returns the access token to the application, and the application can then use the access token to authorize requests to Azure Event Hubs.

The following sections explain how to configure a native application or web application for authentication with Microsoft identity platform 2.0. For more information about Microsoft identity platform 2.0, see [Microsoft identity platform (v2.0) overview](../active-directory/develop/v2-overview.md).

For an overview of the OAuth 2.0 code grant flow, see [Authorize access to Microsoft Entra web applications using the OAuth 2.0 code grant flow](../active-directory/develop/v2-oauth2-auth-code-flow.md).

### Register your application with Microsoft Entra ID

The first step to use Microsoft Entra ID to authorize Event Hubs resources is to register a client application with a Microsoft Entra tenant in the [Azure portal](https://portal.azure.com/). Follow steps in the [Quickstart: Register an application with the Microsoft identity platform](../active-directory/develop/quickstart-register-app.md) to register an application in Microsoft Entra ID that represents your application trying to access Event Hubs resources.

When you register your client application, you supply information about the application. Microsoft Entra ID provides a client ID, also called an application ID, to associate the application with Microsoft Entra runtime. To learn more about the client ID, see [Application and service principal objects in Microsoft Entra ID](../active-directory/develop/app-objects-and-service-principals.md).

> [!NOTE]

> If you register the application as a native application, specify any valid URI for the Redirect URI. For native applications, this value doesn't need to be a real URL. For web applications, the redirect URI must be a valid URI because it specifies the URL where tokens are provided.

After you register your application, you see the **Application (client) ID** under **Settings**:

### Create a client secret for authentication

The application requires a client secret to prove its identity when requesting a token. Follow steps from [Add a client secret](../active-directory/develop/quickstart-register-app.md#add-a-client-secret) to create a client secret for your app in Microsoft Entra ID.

## Assign Azure roles using the Azure portal

Assign one of the [Event Hubs roles](#built-in-roles-for-azure-event-hubs) to the application's service principal at the desired scope, such as the Event Hubs namespace, resource group, or subscription. For detailed steps, see [Assign Azure roles using the Azure portal](/azure/role-based-access-control/role-assignments-portal).

After defining the role and its scope, test this behavior with samples available [in this GitHub location](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/Rbac). To learn more about managing access to Azure resources using Azure role-based access control (RBAC) and the Azure portal, see [this article](/azure/role-based-access-control/role-assignments-portal).

### Use client libraries to acquire tokens

After registering your application and granting it permissions to send or receive data in Azure Event Hubs, add code to your application to authenticate a security principal and acquire an OAuth 2.0 token. To authenticate and acquire the token, use one of the [Microsoft identity platform authentication libraries](../active-directory/develop/reference-v2-libraries.md) or another open-source library that supports OpenID Connect 1.0. Your application can then use the access token to authorize a request against Azure Event Hubs.

For scenarios where acquiring tokens is supported, see the [Scenarios](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet/wiki/scenarios) section of the [Microsoft Authentication Library (MSAL) for .NET](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) GitHub repository.

## Samples

- [RBAC samples using the legacy .NET Microsoft.Azure.EventHubs package](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/Rbac). We're working on creating a new version of this sample using the latest Azure.Messaging.EventHubs package. See the already converted [Managed Identity](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Azure.Messaging.EventHubs/ManagedIdentityWebApp).

- [RBAC sample using the legacy Java com.microsoft.azure.eventhubs package](https://github.com/Azure/azure-event-hubs/tree/master/samples/Java/Rbac). Use the [migration guide](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/eventhubs/azure-messaging-eventhubs/migration-guide.md) to migrate this sample to use the new package (`com.azure.messaging.eventhubs`). To learn more about using the new package, see samples [here](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/eventhubs/azure-messaging-eventhubs/src/samples/java/com/azure/messaging/eventhubs).

## Related content

- To learn more about Azure RBAC, see [What is Azure role-based access control (Azure RBAC)](../role-based-access-control/overview.md).

- To learn how to assign and manage Azure role assignments with Azure PowerShell, Azure CLI, or the REST API, see these articles.

- [Add or remove Azure role assignments using Azure PowerShell](../role-based-access-control/role-assignments-powershell.md)

- [Add or remove Azure role assignments using Azure CLI](../role-based-access-control/role-assignments-cli.md)

- [Add or remove Azure role assignments using the REST API](../role-based-access-control/role-assignments-rest.md)

- [Add Azure role assignments using Azure Resource Manager templates](../role-based-access-control/role-assignments-template.md)

See the following related articles:

- [Authenticate a managed identity with Microsoft Entra ID to access Event Hubs resources](authenticate-managed-identity.md)

- [Authenticate requests to Azure Event Hubs using Shared Access Signatures](authenticate-shared-access-signature.md)

- [Authorize access to Event Hubs resources using Microsoft Entra ID](authorize-access-azure-active-directory.md)

- [Authorize access to Event Hubs resources using shared access signatures](authorize-access-shared-access-signature.md)


# Authorize Access Azure Active Directory

# Authorize access to Azure Event Hubs resources using Microsoft Entra ID

Azure Event Hubs supports using Microsoft Entra ID to authorize requests to Event Hubs resources, providing secure authentication and granular access control. With Microsoft Entra ID, you can use Azure role-based access control (RBAC) to grant permissions to security principals, including users and application service principals. This approach eliminates the need for shared access keys and provides better security for your Event Hubs implementations. To learn more about roles and role assignments, see [Understanding the different roles](../role-based-access-control/overview.md).

## Overview

When a security principal (a user, or an application) attempts to access an Event Hubs resource, the request must be authorized. With Microsoft Entra ID, access to a resource is a two-step process.

1. First, the security principal’s identity is authenticated, and an OAuth 2.0 token is returned. The resource name to request a token is `https://eventhubs.azure.net/`, and it's the same for all clouds/tenants. For Kafka clients, the resource to request a token is `https://<namespace>.servicebus.windows.net`.

1. Next, the token is passed as part of a request to the Event Hubs service to authorize access to the specified resource.

The authentication step requires that an application request contains an OAuth 2.0 access token at runtime. If an application is running within an Azure entity such as an Azure VM,  a virtual machine scale set, or an Azure Function app, it can use a managed identity to access the resources. To learn how to authenticate requests made by a managed identity to Event Hubs service, see [Authenticate access to Azure Event Hubs resources with Microsoft Entra ID and managed identities for Azure Resources](authenticate-managed-identity.md).

The authorization step requires that one or more Azure roles be assigned to the security principal. Azure Event Hubs provides Azure roles that encompass sets of permissions for Event Hubs resources. The roles that are assigned to a security principal determine the permissions that the principal has. For more information about Azure roles, see [Azure built-in roles for Azure Event Hubs](#azure-built-in-roles-for-azure-event-hubs).

Native applications and web applications that make requests to Event Hubs can also authorize with Microsoft Entra ID. To learn how to request an access token and use it to authorize requests for Event Hubs resources, see [Authenticate access to Azure Event Hubs with Microsoft Entra ID from an application](authenticate-application.md).

## Assign Azure roles for access rights

Microsoft Entra authorizes access rights to secured resources through [Azure role-based access control (Azure RBAC)](../role-based-access-control/overview.md). Azure Event Hubs defines a set of Azure built-in roles that encompass common sets of permissions used to access event hub data and you can also define custom roles for accessing the data.

When an Azure role is assigned to a Microsoft Entra security principal, Azure grants access to those resources for that security principal. Access can be scoped to the level of subscription, the resource group, the Event Hubs namespace, or any resource under it. A Microsoft Entra security principal can be a user, or an application service principal, or a [managed identity for Azure resources](../active-directory/managed-identities-azure-resources/overview.md).

## Azure built-in roles for Azure Event Hubs

Azure provides the following Azure built-in roles for authorizing access to Event Hubs data using Microsoft Entra ID and OAuth:

| Role | Description |

| ---- | ----------- |

| [Azure Event Hubs Data owner](../role-based-access-control/built-in-roles.md#azure-event-hubs-data-owner) | Use this role to give complete access to Event Hubs resources. |

| [Azure Event Hubs Data sender](../role-based-access-control/built-in-roles.md#azure-event-hubs-data-sender) | Use this role to allow the security principal to send events to Event Hubs resources. |

| [Azure Event Hubs Data receiver](../role-based-access-control/built-in-roles.md#azure-event-hubs-data-receiver) | Use this role to allow the security principal to receive events from Event Hubs resources. |

For Schema Registry built-in roles, see [Schema Registry roles](schema-registry-concepts.md#azure-role-based-access-control).

## Resource scope

Before you assign an Azure role to a security principal, determine the scope of access that the security principal should have. Best practices dictate that it's always best to grant only the narrowest possible scope.

The following list describes the levels at which you can scope access to Event Hubs resources, starting with the narrowest scope:

- **Consumer group**: At this scope, role assignment applies only to this entity. Currently, the Azure portal doesn't support assigning an Azure role to a security principal at this level.

- **Event hub**: Role assignment applies to event hubs and their consumer groups.

- **Namespace**: Role assignment spans the entire topology of Event Hubs under the namespace and to the consumer group associated with it.

- **Resource group**: Role assignment applies to all the Event Hubs resources under the resource group.

- **Subscription**: Role assignment applies to all the Event Hubs resources in all of the resource groups in the subscription.

> [!NOTE]

> - Keep in mind that Azure role assignments might take up to five minutes to propagate.

> - This content applies to both Event Hubs and Event Hubs for Apache Kafka. For more information on Event Hubs for Kafka support, see [Event Hubs for Kafka - security and authentication](azure-event-hubs-apache-kafka-overview.md#security-and-authentication).

For more information about how built-in roles are defined, see [Understand role definitions](../role-based-access-control/role-definitions.md#control-and-data-actions). For information about creating Azure custom roles, see [Azure custom roles](../role-based-access-control/custom-roles.md).

## Samples

- [Microsoft.Azure.EventHubs samples](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/Rbac).

These samples use the legacy **Microsoft.Azure.EventHubs** library, but you can easily update it to using the latest **Azure.Messaging.EventHubs** library. To move the sample from using the legacy library to new one, see the [Guide to migrate from Microsoft.Azure.EventHubs to Azure.Messaging.EventHubs](https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/eventhub/Azure.Messaging.EventHubs/MigrationGuide.md).

- [Azure.Messaging.EventHubs samples](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Azure.Messaging.EventHubs/ManagedIdentityWebApp)

This sample has been updated to use the latest **Azure.Messaging.EventHubs** library.

- [Event Hubs for Kafka - OAuth samples](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/oauth).

## Related content

- Learn how to assign an Azure built-in role to a security principal, see [Authenticate access to Event Hubs resources using Microsoft Entra ID](authenticate-application.md).

- Learn [how to create custom roles with Azure RBAC](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/Rbac/CustomRole).

- Learn [how to use Microsoft Entra ID with EH](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/Rbac/AzureEventHubsSDK)

See the following related articles:

- [Authenticate requests to Azure Event Hubs from an application using Microsoft Entra ID](authenticate-application.md)

- [Authenticate a managed identity with Microsoft Entra ID to access Event Hubs Resources](authenticate-managed-identity.md)

- [Authenticate requests to Azure Event Hubs using Shared Access Signatures](authenticate-shared-access-signature.md)

- [Authorize access to Event Hubs resources using Shared Access Signatures](authorize-access-shared-access-signature.md)


# Network Security

# Network security for Azure Event Hubs

This article describes how to use the following security features with Azure Event Hubs:

- Service tags

- IP Firewall rules

- Network service endpoints

- Private endpoints

## Service tags

A service tag represents a group of IP address prefixes from a given Azure service. Microsoft manages the address prefixes encompassed by the service tag and automatically updates the service tag as addresses change, minimizing the complexity of frequent updates to network security rules. For more information about service tags, see [Service tags overview](../virtual-network/service-tags-overview.md).

You can use service tags to define network access controls on [network security groups](../virtual-network/network-security-groups-overview.md#security-rules) or [Azure Firewall](../firewall/service-tags.md). Use service tags in place of specific IP addresses when you create security rules. By specifying the service tag name (for example, `EventHub`) in the appropriate *source* or *destination* field of a rule, you can allow or deny the traffic for the corresponding service.

| Service tag | Purpose | Can use inbound or outbound? | Can be regional? | Can use with Azure Firewall? |

| --- | -------- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|

| `EventHub` | Azure Event Hubs. | Outbound | Yes | Yes |

## IP firewall

By default, Event Hubs namespaces are accessible from internet as long as the request comes with valid authentication and authorization. With IP firewall, you can restrict it further to only a set of IPv4 or IPv6 addresses or address ranges in [CIDR (Classless Inter-Domain Routing)](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) notation.

This feature is helpful in scenarios in which Azure Event Hubs should be only accessible from certain well-known sites. Firewall rules enable you to configure rules to accept traffic originating from specific IPv4 or IPv6 addresses. For example, if you use Event Hubs with [Azure Express Route](../expressroute/expressroute-faqs.md#supported-services), you can create a **firewall rule** to allow traffic from only your on-premises infrastructure IP addresses.

The IP firewall rules are applied at the Event Hubs namespace level. Therefore, the rules apply to all connections from clients using any supported protocol. Any connection attempt from an IP address that doesn't match an allowed IP rule on the Event Hubs namespace is rejected as unauthorized. The response doesn't mention the IP rule. IP filter rules are applied in order, and the first rule that matches the IP address determines the accept or reject action.

For more information, see [How to configure IP firewall for an event hub](event-hubs-ip-filtering.md).

## Network service endpoints

The integration of Event Hubs with [Virtual Network (virtual network) Service Endpoints](../virtual-network/virtual-network-service-endpoints-overview.md) enables secure access to messaging capabilities from workloads such as virtual machines that are bound to virtual networks, with the network traffic path being secured on both ends.

Once configured to bound to at least one virtual network subnet service endpoint, the respective Event Hubs namespace no longer accepts traffic from anywhere but authorized subnets in virtual networks. From the virtual network perspective, binding an Event Hubs namespace to a service endpoint configures an isolated networking tunnel from the virtual network subnet to the messaging service.

The result is a private and isolated relationship between the workloads bound to the subnet and the respective Event Hubs namespace, in spite of the observable network address of the messaging service endpoint being in a public IP range. There's an exception to this behavior. When you enable a service endpoint, by default, the service enables the `denyall` rule in the [IP firewall](event-hubs-ip-filtering.md) associated with the virtual network. You can add specific IP addresses in the IP firewall to enable access to the Event Hubs public endpoint.

> [!IMPORTANT]

> This feature isn't supported in the **basic** tier.

### Advanced security scenarios enabled by virtual network integration

Solutions that require tight and compartmentalized security, and where virtual network subnets provide the segmentation between the compartmentalized services, still need communication paths between services residing in those compartments.

Any immediate IP route between the compartments, including those carrying HTTPS over TCP/IP, carries the risk of exploitation of vulnerabilities from the network layer on up. Messaging services provide insulated communication paths, where messages are even written to disk as they transition between parties. Workloads in two distinct virtual networks that are both bound to the same Event Hubs instance can communicate efficiently and reliably via messages, while the respective network isolation boundary integrity is preserved.

That means your security sensitive cloud solutions not only gain access to Azure industry-leading reliable and scalable asynchronous messaging capabilities, but they can now use messaging to create communication paths between secure solution compartments that are inherently more secure than what is achievable with any peer-to-peer communication mode, including HTTPS and other TLS-secured socket protocols.

### Bind event hubs to virtual networks

**Virtual network rules** are the firewall security feature that controls whether your Azure Event Hubs namespace accepts connections from a particular virtual network subnet.

Binding an Event Hubs namespace to a virtual network is a two-step process. You first need to create a **virtual Network service endpoint** on a virtual network's subnet and enable it for **Microsoft.EventHub** as explained in the [service endpoint overview](../virtual-network/virtual-network-service-endpoints-overview.md) article. Once you have added the service endpoint, you bind the Event Hubs namespace to it with a **virtual network rule**.

The virtual network rule is an association of the Event Hubs namespace with a virtual network subnet. While the rule exists, all workloads bound to the subnet are granted access to the Event Hubs namespace. Event Hubs itself never establishes outbound connections, doesn't need to gain access, and is therefore never granted access to your subnet by enabling this rule.

For more information, see [How to configure virtual network service endpoints for an event hub](event-hubs-service-endpoints.md).

## Private endpoints

[Azure Private Link service](../private-link/private-link-overview.md) enables you to access Azure Services (for example, Azure Event Hubs, Azure Storage, and Azure Cosmos DB) and Azure hosted customer/partner services over a **private endpoint** in your virtual network.

A private endpoint is a network interface that connects you privately and securely to a service powered by Azure Private Link. The private endpoint uses a private IP address from your virtual network, effectively bringing the service into your virtual network. All traffic to the service can be routed through the private endpoint, so no gateways, NAT devices, ExpressRoute or VPN connections, or public IP addresses are needed. Traffic between your virtual network and the service traverses over the Microsoft backbone network, eliminating exposure from the public Internet. You can connect to an instance of an Azure resource, giving you the highest level of granularity in access control.

> [!IMPORTANT]

> This feature isn't supported in the **basic** tier.

For more information, see [How to configure private endpoints for an event hub](private-link-service.md).

## Next steps

See the following articles:

- [How to configure IP firewall for an event hub](event-hubs-ip-filtering.md)

- [How to configure virtual network service endpoints for an event hub](event-hubs-service-endpoints.md)

- [How to configure private endpoints for an event hub](private-link-service.md)


# Confidential Computing

# Azure Event Hubs confidential computing overview

Azure Event Hubs Dedicated supports [confidential computing](../confidential-computing/overview.md) to protect your event data in use. Confidential computing uses hardware-based trusted execution environments (TEEs) to provide enhanced data protection, preventing unauthorized access to your events while they're being processed.

When you enable confidential computing on an Event Hubs Dedicated namespace, your data benefits from hardware-level isolation in addition to existing encryption at rest and in transit. This capability helps organizations that handle sensitive or regulated data meet strict security and compliance requirements.

## Benefits

Confidential computing for Azure Event Hubs provides the following advantages:

- **No code changes required**: Enable confidential computing at the namespace level without modifying your applications or event processing patterns.

- **Defense in depth**: Combines with existing Event Hubs security features like [customer-managed keys](configure-customer-managed-key.md), [private endpoints](private-link-service.md), and [managed identities](authenticate-managed-identity.md).

- **Event streaming protection**: Your event hubs benefit from hardware-level isolation during event processing.

## Regional availability

Confidential computing for Azure Event Hubs is available in select regions.

| Region |

|--------|

| Korea Central |

| UAE North |

## Limitations

The following limitations apply to confidential computing for Azure Event Hubs:

- Confidential computing is available only on the **[Dedicated tier](event-hubs-dedicated-overview.md)**.

- You must enable confidential computing during namespace creation. You can't enable it on existing namespaces.

## Enable confidential computing by using the Azure portal

1. Go to the [Azure portal](https://portal.azure.com) and open the Event Hubs namespace creation page.

1. Select **Dedicated** for the pricing tier.

1. Select a [supported region](#regional-availability) as the location.

1. For **Confidential compute**, select **Enabled**.

1. Fill in the remaining required fields for your namespace configuration.

1. Select **Review + create**, and then select **Create** to deploy the namespace with confidential computing enabled.

## Enable confidential computing by using a template

You can enable confidential computing programmatically by including the `platformCapabilities` property in your deployment template.

### Step 1: Create a Dedicated cluster with confidential computing

# [Bicep](#tab/bicep)

The following Bicep file creates an Event Hubs Dedicated cluster with confidential computing enabled:

```bicep

@description('Name of the Event Hubs Dedicated cluster')

param clusterName string

@description('Location for the cluster. Must be a region that supports confidential computing.')

@allowed([

'koreacentral'

'uaenorth'

])

param location string = 'uaenorth'

@description('Capacity units for the Dedicated cluster')

@minValue(1)

param capacity int = 1

resource eventHubCluster 'Microsoft.EventHub/clusters@2025-05-01-preview' = {

name: clusterName

location: location

sku: {

name: 'Dedicated'

capacity: capacity

}

properties: {

supportsScaling: true

platformCapabilities: {

confidentialCompute: {

mode: 'Enabled'

}

}

}

}

output clusterArmId string = eventHubCluster.id

```

# [ARM template](#tab/arm)

The following ARM template creates an Event Hubs Dedicated cluster with confidential computing enabled:

```json

{

"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"clusterName": {

"type": "string",

"metadata": {

"description": "Name of the Event Hubs Dedicated cluster"

}

},

"location": {

"type": "string",

"defaultValue": "uaenorth",

"allowedValues": [

"koreacentral",

"uaenorth"

],

"metadata": {

"description": "Location for the cluster. Must be a region that supports confidential computing."

}

},

"capacity": {

"type": "int",

"defaultValue": 1,

"minValue": 1,

"metadata": {

"description": "Capacity units for the Dedicated cluster"

}

}

},

"resources": [

{

"type": "Microsoft.EventHub/clusters",

"apiVersion": "2025-05-01-preview",

"name": "[parameters('clusterName')]",

"location": "[parameters('location')]",

"sku": {

"name": "Dedicated",

"capacity": "[parameters('capacity')]"

},

"properties": {

"supportsScaling": true,

"platformCapabilities": {

"confidentialCompute": {

"mode": "Enabled"

}

}

}

}

],

"outputs": {

"clusterArmId": {

"type": "string",

"value": "[resourceId('Microsoft.EventHub/clusters', parameters('clusterName'))]"

}

}

}

```

---

### Step 2: Create a namespace in the Dedicated cluster

After the cluster is created, create an Event Hubs namespace inside it by referencing the cluster's resource ID.

# [Bicep](#tab/bicep)

```bicep

@description('Name of the Event Hubs namespace')

param namespaceName string

@description('Location for the namespace. Must match the cluster location.')

param location string

@description('Resource ID of the Dedicated cluster')

param clusterArmId string

resource eventHubNamespace 'Microsoft.EventHub/namespaces@2025-05-01-preview' = {

name: namespaceName

location: location

sku: {

name: 'Standard'

tier: 'Standard'

capacity: 1

}

properties: {

clusterArmId: clusterArmId

}

}

```

# [ARM template](#tab/arm)

```json

{

"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"namespaceName": {

"type": "string",

"metadata": {

"description": "Name of the Event Hubs namespace"

}

},

"location": {

"type": "string",

"metadata": {

"description": "Location for the namespace. Must match the cluster location."

}

},

"clusterArmId": {

"type": "string",

"metadata": {

"description": "Resource ID of the Dedicated cluster"

}

}

},

"resources": [

{

"type": "Microsoft.EventHub/namespaces",

"apiVersion": "2025-05-01-preview",

"name": "[parameters('namespaceName')]",

"location": "[parameters('location')]",

"sku": {

"name": "Standard",

"tier": "Standard",

"capacity": 1

},

"properties": {

"clusterArmId": "[parameters('clusterArmId')]"

}

}

]

}

```

---

## Combine confidential computing with customer-managed keys

For maximum data protection, combine confidential computing with [customer-managed keys](configure-customer-managed-key.md) backed by [Azure Key Vault Managed HSM](/azure/key-vault/managed-hsm/overview). This combination ensures that:

- Your data is protected in use by confidential computing.

- Your encryption keys are stored in validated hardware security modules.

- You maintain full control over your encryption keys.

## Use Azure Policy to enforce confidential computing

Create an Azure Policy definition to enforce that all Event Hubs Dedicated clusters in your organization have confidential computing enabled. This approach ensures consistent security configuration across your Azure environment.

The following policy definition denies or audits the creation of Dedicated clusters that don't have confidential computing enabled:

```json

{

"mode": "All",

"parameters": {

"effect": {

"type": "String",

"metadata": {

"displayName": "Effect",

"description": "Deny or Audit"

},

"allowedValues": [

"Deny",

"Audit"

],

"defaultValue": "Deny"

}

},

"policyRule": {

"if": {

"allOf": [

{

"field": "type",

"equals": "Microsoft.EventHub/clusters"

},

{

"not": {

"field": "Microsoft.EventHub/clusters/platformCapabilities.confidentialCompute.mode",

"equals": "Enabled"

}

}

]

},

"then": {

"effect": "[parameters('effect')]"

}

}

}

```

To use this policy, create a custom policy definition in Azure Policy and assign it to the appropriate scope, such as a management group, subscription, or resource group.

> [!NOTE]

> When combining confidential computing with customer-managed keys, use a user-assigned managed identity. This requirement exists because the identity must be granted access to the Managed HSM before creating the namespace. A system-assigned identity only exists after the namespace is created.

## Related content

- [What is confidential computing?](../confidential-computing/overview.md)

- [Azure confidential computing products](../confidential-computing/overview-azure-products.md)

- [Confidential computing use cases](../confidential-computing/use-cases-scenarios.md)

- [Configure customer-managed keys for Azure Event Hubs](configure-customer-managed-key.md)

- [Azure Event Hubs Dedicated](event-hubs-dedicated-overview.md)

- [Azure Key Vault Managed HSM](/azure/key-vault/managed-hsm/overview)


# Network Security Perimeter

# Network Security Perimeter for Azure Event Hubs

Network Security Perimeter (NSP) is a network isolation feature that enables you to define a logical network boundary for Platform as a Service (PaaS) resources, including Azure Event Hubs. It restricts public network access to resources within the perimeter while allowing secure communication between associated PaaS services.

## Overview

Network Security Perimeter provides an extra layer of security for your Azure Event Hubs namespace by:

- **Restricting public access**: By default, resources within the perimeter are protected from unauthorized external access.

- **Enabling secure PaaS-to-PaaS communication**: Event Hubs can securely communicate with other Azure services like Azure Storage and Azure Key Vault within the same perimeter.

- **Simplifying network security management**: Instead of managing individual service firewalls, you can define access rules at the perimeter level.

- **Supporting compliance requirements**: NSP helps meet regulatory requirements by providing clear network boundaries for your data.

Operating as a service under Azure Private Link, Network Security Perimeter facilitates secure communication for PaaS services deployed outside the virtual network. It supports:

- Seamless interaction among PaaS services within the perimeter

- Communication with external resources through carefully configured access rules

- Outbound access to services such as Azure Key Vault for Bring Your Own Key (BYOK) encryption and Azure Storage for Event Hubs Capture

## Key capabilities

When you associate an Event Hubs namespace with a Network Security Perimeter, you gain the following capabilities:

| Capability | Description |

| --- | --- |

| **Inbound access rules** | Control which external resources, IP addresses, or subscriptions can send data to your Event Hubs namespace. |

| **Outbound access rules** | Define which external resources your Event Hubs namespace can communicate with (for example, storage accounts for Capture). |

| **Profile-based management** | Apply different access rule sets to different resources using NSP profiles. |

| **Diagnostic logging** | Monitor network access attempts and audit security events through NSP diagnostic logs. |

## Supported scenarios

Network Security Perimeter for Event Hubs supports the following scenarios:

- **Event ingestion from Azure services**: Allow other Azure services within the same perimeter to send events to your Event Hubs namespace.

- **Kafka workloads**: Integrating Event Hubs with Kafka within the NSP framework enhances data streaming capabilities while maintaining robust security.

- **Data capture**: Configure outbound rules to allow Event Hubs to write captured data to Azure Storage or Azure Data Lake Storage.

- **Customer-managed keys**: Enable outbound access to Azure Key Vault for encryption with customer-managed keys (BYOK).

## Limitations

Be aware of the following limitations when using Network Security Perimeter with Event Hubs:

- Network Security Perimeter doesn't support [Azure Event Hubs - Geo-disaster recovery](./event-hubs-geo-dr.md).

- Certain Network Security Perimeter features, such as same perimeter access, cross perimeter access, and subscription access rules, don't work with Shared Access Signature (SAS) authentication. Use Microsoft Entra ID authentication for full NSP functionality.

## Associate Event Hubs with a Network Security Perimeter

To learn how to associate a Network Security Perimeter with your Event Hubs namespace, see [Associate Network Security Perimeter with Event Hubs](associate-network-security-perimeter.md).

## Related content

- [Network security perimeter concepts](/azure/private-link/network-security-perimeter-concepts)

- [Create a network security perimeter](/azure/private-link/create-network-security-perimeter-portal)

- [Diagnostic logs in network security perimeter](/azure/private-link/network-security-perimeter-diagnostic-logs)

- [Network security for Azure Event Hubs](./network-security.md)

- [Use private endpoints with Event Hubs](./private-link-service.md)

- [Configure IP firewall rules](./event-hubs-ip-filtering.md)


# Security Controls Policy

# Azure Policy Regulatory Compliance controls for Azure Event Hubs

[Regulatory Compliance in Azure Policy](../governance/policy/concepts/regulatory-compliance.md)

provides Microsoft created and managed initiative definitions, known as _built-ins_, for the

**compliance domains** and **security controls** related to different compliance standards. This

page lists the **compliance domains** and **security controls** for Azure Event Hubs. You can assign

the built-ins for a **security control** individually to help make your Azure resources compliant

with the specific standard.

[!INCLUDE [azure-policy-compliancecontrols-introwarning](../../includes/policy/standards/intro-warning.md)]

[!INCLUDE [azure-policy-compliancecontrols-eventhubs](~/azure-policy-autogen-docs/includes/policy/standards/byrp/microsoft.eventhub.md)]

## Next steps

- Learn more about [Azure Policy Regulatory Compliance](../governance/policy/concepts/regulatory-compliance.md).

- See the built-ins on the [Azure Policy GitHub repo](https://github.com/Azure/azure-policy).


# Transport Layer Security Enforce Minimum Version

# Enforce a minimum required version of Transport Layer Security (TLS) for requests to an Event Hubs namespace

Communication between a client application and an Azure Event Hubs namespace is encrypted using Transport Layer Security (TLS). TLS is a standard cryptographic protocol that ensures privacy and data integrity between clients and services over the Internet. For more information about TLS, see [Transport Layer Security](https://datatracker.ietf.org/wg/tls/about/).

Azure Event Hubs supports choosing a specific TLS version for namespaces. Currently Azure Event Hubs uses TLS 1.2 on public endpoints by default, but TLS 1.0 and TLS 1.1 are still supported for backward compatibility.

Azure Event Hubs namespaces permit clients to send and receive data with TLS 1.0 and above. To enforce stricter security measures, you can configure your Event Hubs namespace to require that clients send and receive data with a newer version of TLS. If an Event Hubs namespace requires a minimum version of TLS, then any requests made with an older version will fail.

> [!WARNING]

> As of 20 October 2025, TLS 1.0 and TLS 1.1 will no longer be supported on Azure Event Hubs. The minimum TLS version will be 1.2 for all Event Hubs deployments.

> [!IMPORTANT]

> On 31 October 2024, TLS 1.3 will be enabled for AMQP traffic. TLS 1.3 is already enabled for Kafka and HTTPS traffic. Java clients may have a problem with TLS 1.3 due to a dependency on an older version of Proton-J. For more details, read [Java client changes to support TLS 1.3 with Azure Service Bus and Azure Event Hubs](https://techcommunity.microsoft.com/t5/messaging-on-azure-blog/java-client-changes-to-support-tls-1-3-with-azure-service-bus/ba-p/4089355)

> [!IMPORTANT]

> If you are using a service that connects to Azure Event Hubs, make sure that service is using the appropriate version of TLS to send requests to Azure Event Hubs before you set the required minimum version for an Event Hubs namespace.

## Permissions necessary to require a minimum version of TLS

To set the  `MinimumTlsVersion`  property for the Event Hubs namespace, a user must have permissions to create and manage Event Hubs namespaces. Azure role-based access control (Azure RBAC) roles that provide these permissions include the  **Microsoft.EventHub/namespaces/write**  or  **Microsoft.EventHub/namespaces/\***  action. Built-in roles with this action include:

- The Azure Resource Manager [Owner](../role-based-access-control/built-in-roles.md#owner) role

- The Azure Resource Manager [Contributor](../role-based-access-control/built-in-roles.md#contributor) role

- The [Azure Event Hubs Data Owner](../role-based-access-control/built-in-roles.md#azure-event-hubs-data-owner) role

Role assignments must be scoped to the level of the Event Hubs namespace or higher to permit a user to require a minimum version of TLS for the Event Hubs namespace. For more information about role scope, see [Understand scope for Azure RBAC](../role-based-access-control/scope-overview.md).

Be careful to restrict assignment of these roles only to those who require the ability to create an Event Hubs namespace or update its properties. Use the principle of least privilege to ensure that users have the fewest permissions that they need to accomplish their tasks. For more information about managing access with Azure RBAC, see [Best practices for Azure RBAC](../role-based-access-control/best-practices.md).

> [!NOTE]

> The classic subscription administrator roles Service Administrator and Co-Administrator include the equivalent of the Azure Resource Manager [**Owner**](../role-based-access-control/built-in-roles.md#owner) role. The  **Owner**  role includes all actions, so a user with one of these administrative roles can also create and manage Event Hubs namespaces. For more information, see [**Azure roles, Microsoft Entra roles, and classic subscription administrator roles**](../role-based-access-control/rbac-and-directory-admin-roles.md#classic-subscription-administrator-roles).

## Network considerations

When a client sends a request to an Event Hubs namespace, the client establishes a connection with the Event Hubs namespace endpoint first, before processing any requests. The minimum TLS version setting is checked after the TLS connection is established. If the request uses an earlier version of TLS than that specified by the setting, the connection will continue to succeed, but the request will eventually fail.

> [!NOTE]

> Due to limitations in the confluent library, errors coming from an invalid TLS version will not surface when connecting through the Kafka protocol. Instead a general exception will be shown.

Here're a few important points to consider:

- A network trace would show the successful establishment of a TCP connection and successful TLS negotiation, before a 401 is returned if the TLS version used is less than the minimum TLS version configured.

- Penetration or endpoint scanning on `yournamespace.servicebus.windows.net` will indicate the support for TLS 1.0, TLS 1.1, and TLS 1.2, as the service continues to support all these protocols. The minimum TLS version, enforced at the namespace level, indicates what the lowest TLS version the namespace will support.

## Next steps

See the following documentation for more information.

- [Configure the minimum TLS version for an Event Hubs namespace](transport-layer-security-configure-minimum-version.md)

- [Configure Transport Layer Security (TLS) for an Event Hubs client application](transport-layer-security-configure-client-version.md)

- [Use Azure Policy to audit for compliance of minimum TLS version for an Event Hubs namespace](transport-layer-security-audit-minimum-version.md)


# Event Hubs Availability And Consistency

# Availability and consistency in Event Hubs

This article provides information about availability and consistency supported by Azure Event Hubs.

## Availability

Azure Event Hubs spreads the risk of catastrophic failures of individual machines or even complete racks across clusters that span multiple failure domains within a datacenter. It implements transparent failure detection and failover mechanisms such that the service will continue to operate within the assured service-levels and typically without noticeable interruptions when such failures occur.

If an Event Hubs namespace is created in a region with [availability zones](/azure/reliability/availability-zones-overview), the outage risk is further spread across three physically separated facilities, and the service has enough capacity reserves to instantly cope up with the complete, catastrophic loss of the entire facility. For more information, see [Azure Event Hubs - Geo-disaster recovery](event-hubs-geo-dr.md).

When a client application sends events to an event hub without specifying a partition, events are automatically distributed among partitions in your event hub. If a partition isn't available for some reason, events are distributed among the remaining partitions. This behavior allows for the greatest amount of up time. For use cases that require the maximum up time, this model is preferred instead of sending events to a specific partition.

## Consistency

In some scenarios, the ordering of events can be important. For example, you may want your back-end system to process an update command before a delete command. In this scenario, a client application sends events to a specific partition so that the ordering is preserved. When a consumer application consumes these events from the partition, they are read in order.

With this configuration, keep in mind that if the particular partition to which you are sending is unavailable, you will receive an error response. As a point of comparison, if you don't have an affinity to a single partition, the Event Hubs service sends your event to the next available partition.

Therefore, if high availability is most important, don't target a specific partition (using partition ID/key). Using partition ID/key downgrades the availability of an event hub to partition-level. In this scenario, you are making an explicit choice between availability (no partition ID/key) and consistency (pinning events to a specific partition). For detailed information about partitions in Event Hubs, see [Partitions](event-hubs-features.md#partitions).

## Appendix

### Send events without specifying a partition

We recommend sending events to an event hub without setting partition information to allow the Event Hubs service to balance the load across partitions. See the following quick starts to learn how to do so in different programming languages.

- [Send events using .NET](event-hubs-dotnet-standard-getstarted-send.md)

- [Send events using Java](event-hubs-java-get-started-send.md)

- [Send events using JavaScript](event-hubs-node-get-started-send.md)

- [Send events using Python](event-hubs-python-get-started-send.md)

### Send events to a specific partition

In this section, you learn how to send events to a specific partition using different programming languages.

### [.NET](#tab/dotnet)

To send events to a specific partition, create the batch using the [EventHubProducerClient.CreateBatchAsync](/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient.createbatchasync#Azure_Messaging_EventHubs_Producer_EventHubProducerClient_CreateBatchAsync_Azure_Messaging_EventHubs_Producer_CreateBatchOptions_System_Threading_CancellationToken_) method by specifying either the `PartitionId` or the `PartitionKey` in [CreateBatchOptions](/dotnet/api/azure.messaging.eventhubs.producer.createbatchoptions). The following code sends a batch of events to a specific partition by specifying a partition key. Event Hubs ensures that all events sharing a partition key value are stored together and delivered in order of arrival.

```csharp

var batchOptions = new CreateBatchOptions { PartitionKey = "cities" };

using var eventBatch = await producer.CreateBatchAsync(batchOptions);

```

You can also use the [EventHubProducerClient.SendAsync](/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient.sendasync#Azure_Messaging_EventHubs_Producer_EventHubProducerClient_SendAsync_System_Collections_Generic_IEnumerable_Azure_Messaging_EventHubs_EventData__Azure_Messaging_EventHubs_Producer_SendEventOptions_System_Threading_CancellationToken_) method by specifying either **PartitionId** or **PartitionKey** in [SendEventOptions](/dotnet/api/azure.messaging.eventhubs.producer.sendeventoptions).

```csharp

var sendEventOptions  = new SendEventOptions { PartitionKey = "cities" };

// create the events array

producer.SendAsync(events, sendEventOptions)

```

### [Java](#tab/java)

To send events to a specific partition, create the batch using the [createBatch](https://github.com/Azure/azure-sdk-for-java/blob/master/sdk/eventhubs/azure-messaging-eventhubs/src/main/java/com/azure/messaging/eventhubs/EventHubProducerClient.java) method by specifying either **partition ID** or **partition key** in [createBatchOptions](https://github.com/Azure/azure-sdk-for-java/blob/master/sdk/eventhubs/azure-messaging-eventhubs/src/main/java/com/azure/messaging/eventhubs/models/CreateBatchOptions.java). The following code sends a batch of events to a specific partition by specifying a partition key.

```java

CreateBatchOptions batchOptions = new CreateBatchOptions();

batchOptions.setPartitionKey("cities");

```

You can also use the [EventHubProducerClient.send](https://github.com/Azure/azure-sdk-for-java/blob/master/sdk/eventhubs/azure-messaging-eventhubs/src/main/java/com/azure/messaging/eventhubs/EventHubProducerClient.java) method by specifying either **partition ID** or **partition key** in [SendOptions](https://github.com/Azure/azure-sdk-for-java/blob/master/sdk/eventhubs/azure-messaging-eventhubs/src/main/java/com/azure/messaging/eventhubs/models/SendOptions.java).

```java

List<EventData> events = Arrays.asList(new EventData("Melbourne"), new EventData("London"), new EventData("New York"));

SendOptions sendOptions = new SendOptions();

sendOptions.setPartitionKey("cities");

producer.send(events, sendOptions);

```

### [Python](#tab/python)

To send events to a specific partition, when creating a batch using the [`EventHubProducerClient.create_batch`](/python/api/azure-eventhub/azure.eventhub.eventhubproducerclient#create-batch---kwargs-) method, specify the `partition_id` or the `partition_key`. Then, use the [`EventHubProducerClient.send_batch`](/python/api/azure-eventhub/azure.eventhub.aio.eventhubproducerclient#send-batch-event-data-batch--typing-union-azure-eventhub--common-eventdatabatch--typing-list-azure-eventhub-) method to send the batch to the event hub's partition.

```python

event_data_batch = await producer.create_batch(partition_key='cities')

```

You can also use the [EventHubProducerClient.send_batch](/python/api/azure-eventhub/azure.eventhub.eventhubproducerclient#send-batch-event-data-batch----kwargs-) method by specifying values for `partition_id` or `partition_key` parameters.

```python

producer.send_batch(event_data_batch, partition_key="cities")

```

### [JavaScript](#tab/javascript)

To send events to a specific partition, [Create a batch](/javascript/api/@azure/event-hubs/eventhubproducerclient#createBatch_CreateBatchOptions_) using the [EventHubProducerClient.CreateBatchOptions](/javascript/api/@azure/event-hubs/eventhubproducerclient#createBatch_CreateBatchOptions_) object by specifying the `partitionId` or the `partitionKey`. Then, send the batch to the event hub using the [EventHubProducerClient.SendBatch](/javascript/api/@azure/event-hubs/eventhubproducerclient#sendBatch_EventDataBatch__OperationOptions_) method.

See the following example.

```javascript

const batchOptions = { partitionKey = "cities"; };

const batch = await producer.createBatch(batchOptions);

```

You can also use the [EventHubProducerClient.sendBatch](/javascript/api/@azure/event-hubs/eventhubproducerclient#sendBatch_EventData____SendBatchOptions_) method by specifying either **partition ID** or **partition key** in [SendBatchOptions](/javascript/api/@azure/event-hubs/sendbatchoptions).

```javascript

const sendBatchOptions = { partitionKey = "cities"; };

// prepare events

producer.sendBatch(events, sendBatchOptions);

```

---

## Next steps

You can learn more about Event Hubs by visiting the following links:

- [Event Hubs service overview](./event-hubs-about.md)

- [Event Hubs terminology](event-hubs-features.md)


# Event Hubs Scalability

# Scaling with Event Hubs

There are two factors that influence scaling with Event Hubs.

- Throughput units (standard tier) or processing units (premium tier)

- Partitions

## Throughput units

Throughput units control the throughput capacity of event hubs. Throughput units are prepurchased units of capacity. A single throughput unit provides the following capabilities:

* Ingress: Up to 1 MB per second or 1,000 events per second (whichever comes first).

* Egress: Up to 2 MB per second or 4,096 events per second.

If you exceed the capacity of the throughput units you purchased, ingress is throttled and Event Hubs throws a [EventHubsException](/dotnet/api/azure.messaging.eventhubs.eventhubsexception) with a Reason value of ServiceBusy. Egress doesn't produce throttling exceptions, but it still can't go beyond the capacity of the throughput units you purchased. If you receive publishing rate exceptions or expect to see higher egress, check how many throughput units you purchased for the namespace. You can manage throughput units on the **Scale** page of the namespaces in the [Azure portal](https://portal.azure.com). You can also manage throughput units programmatically by using the [Event Hubs APIs](./event-hubs-samples.md).

You prepurchase throughput units and pay for them by the hour. Once you purchase throughput units, you pay for a minimum of one hour. You can purchase up to 40 throughput units for an Event Hubs namespace, and all event hubs in that namespace share these throughput units. All partitions and consumers within each event hub share the total ingress and egress capacity of these throughput units, so multiple consumers reading from the same partition share the available bandwidth.

The **Auto-inflate** feature of Event Hubs automatically scales up by increasing the number of throughput units to meet usage needs. Increasing throughput units prevents throttling scenarios, in which:

- Data ingress rates exceed set throughput units.

- Data egress request rates exceed set throughput units.

The Event Hubs service increases the throughput when load increases beyond the minimum threshold, without any requests failing with ServerBusy errors.

For more information about the autoinflate feature, see [Automatically scale throughput units](event-hubs-auto-inflate.md).

## Processing units

[Event Hubs Premium](./event-hubs-premium-overview.md) provides superior performance and better isolation within a managed multitenant PaaS environment. The resources in a Premium tier are isolated at the CPU and memory level so that each tenant workload runs in isolation. This resource container is called a **Processing Unit** (PU). You can purchase 1, 2, 4, 6, 8, 10, 12, or 16 processing Units for each Event Hubs Premium namespace.

How much you can ingest and stream with a processing unit depends on various factors such as your producers, consumers, the rate at which you're ingesting and processing, and much more.

For example, Event Hubs Premium namespace with one PU and one event hub (100 partitions) can approximately offer core capacity of ~5-10 MB/s ingress and 10-20 MB/s egress for both AMQP or Kafka workloads.

For more information about configuring PUs for a premium tier namespace, see [Configure processing units](configure-processing-units-premium-namespace.md).

> [!NOTE]

> For more information about quotas and limits, see [Azure Event Hubs - quotas and limits](event-hubs-quotas.md).

## Partitions

[!INCLUDE [event-hubs-partitions](./includes/event-hubs-partitions.md)]

## Related content

To learn more about Event Hubs, see the following articles:

- [Automatically scale throughput units for a standard tier namespace](event-hubs-auto-inflate.md)

- [Configure processing units for a premium tier namespace](configure-processing-units-premium-namespace.md)


# Event Hubs Amqp Troubleshoot

# AMQP errors in Azure Event Hubs

This article provides some of the errors you receive when using AMQP with Azure Event Hubs. They are all standard behaviors of the service. You can avoid them by making send/receive calls on the connection/link, which automatically recreates the connection/link.

## Link is closed

You see the following error when the AMQP connection and link are active but no calls (for example, send or receive) are made using the link for 30 minutes. So, the link is closed. The connection is still open.

"

AMQP:link: detach-forced: The link 'G2:7223832:user.tenant0.cud_00000000000-0000-0000-0000-00000000000000' is force detached by the broker because of errors occurred in publisher(link164614). Detach origin: AmqpMessagePublisher.IdleTimerExpired: Idle timeout: 00:30:00. TrackingId:00000000000000000000000000000000000000_G2_B3, SystemTracker:mynamespace:Topic:MyTopic, Timestamp: 2/16/2018 11:10:40 PM

"

## Connection is closed

You see the following error on the AMQP connection when all links in the connection have been closed because there was no activity (idle) and a new link hasn't been created in 5 minutes.

"

Error{condition=amqp:connection:forced, description='The connection was inactive for more than the allowed 300000 milliseconds and is closed by container 'LinkTracker'. TrackingId:00000000000000000000000000000000000_G21, SystemTracker:gateway5, Timestamp:2019-03-06T17:32:00', info=null}

"

## Link isn't created

You see this error when a new AMQP connection is created but a link isn't created within 1 minute of the creation of the AMQP Connection.

"

Error{condition=amqp:connection:forced, description='The connection was inactive for more than the allowed 60000 milliseconds and is closed by container 'LinkTracker'. TrackingId:0000000000000000000000000000000000000_G21, SystemTracker:gateway5, Timestamp:2019-03-06T18:41:51', info=null}

"

## Next steps

To learn more about AMQP, see [AMQP 1.0 protocol guide](../service-bus-messaging/service-bus-amqp-protocol-guide.md).


# Event Hubs Get Connection String

# Get an Azure Event Hubs connection string

To communicate with an event hub in a namespace, you need a connection string for the namespace or the event hub. If you use a connection string to the namespace from your application, the application will have the provided access (manage, read, or write) to all event hubs in the namespace. If you use a connection string to the event hub, you'll have the provided access to that specific event hub.

The connection string for a namespace has the following components embedded within it,

* Fully qualified domain name of the Event Hubs namespace you created (it includes the Event Hubs namespace name followed by `servicebus.windows.net`)

* Name of the shared access key

* Value of the shared access key

The connection string for a namespace looks like:

```bash

Endpoint=sb://<NamespaceName>.servicebus.windows.net/;SharedAccessKeyName=<KeyName>;SharedAccessKey=<KeyValue>

```

The connection string for an event hub has an extra component in it, i.e., `EntityPath=<EventHubName>`.

```bash

Endpoint=sb://<NamespaceName>.servicebus.windows.net/;SharedAccessKeyName=<KeyName>;SharedAccessKey=<KeyValue>;EntityPath=<EventHubName>

```

This article shows you how to get a connection string to a namespace or a specific event hub by using the Azure portal, PowerShell, or CLI.

## Azure portal

### Connection string for a namespace

1. Sign in to [Azure portal](https://portal.azure.com).

2. Select **All services** in the left navigational menu.

3. Select **Event Hubs** in the **Analytics** section.

4. In the list of event hubs, select your event hub.

6. On the **Event Hubs namespace** page, select **Shared Access Policies** on the left menu under **Settings**.

7. Select a **shared access policy** in the list of policies. The default one is named: **RootManageSharedAccessPolicy**. You can add a policy with appropriate permissions (send, listen), and use that policy.

8. Select the **copy** button next to the **Connection string-primary key** field.

### Connection string for a specific event hub in a namespace

This section gives you steps for getting a connection string to a specific event hub in a namespace.

1. On the **Event Hubs namespace** page, select the event hub in the bottom pane.

1. On the **Event Hubs instance** page, select **Shared access policies** on the left menu under **Settings**.

1. There's no default policy created for an event hub. Create a policy with **Manage**, **Send**, or **Listen** access.

1. Select the policy from the list.

1. Select the **copy** button next to the **Connection string-primary key** field.

## Azure PowerShell

You can use the [Get-AzEventHubKey](/powershell/module/az.eventhub/get-azeventhubkey) to get the connection string for the specific policy/rule.

Here's a sample command to get the connection string for a namespace. `MyAuthRuleName` is the name of the shared access policy. For a namespace, there's a default one: `RootManageSharedAccessKey`.

```azurepowershell-interactive

Get-AzEventHubKey -ResourceGroupName MyResourceGroupName -NamespaceName MyNamespaceName -AuthorizationRuleName MyAuthRuleName

```

Here's a sample command to get the connection string for a specific event hub within a namespace:

```azurepowershell-interactive

Get-AzEventHubKey -ResourceGroupName MyResourceGroupName -NamespaceName MyNamespaceName -EventHubName MyEventHubName -AuthorizationRuleName MyAuthRuleName

```

Here's a sample command to get the connection string for an event hub in a Geo-DR cluster, which has an alias.

```azurepowershell-interactive

Get-AzEventHubKey -ResourceGroupName MyResourceGroupName -NamespaceName MyNamespaceName -EventHubName MyEventHubName -AliasName MyAliasName -Name MyAuthRuleName

```

## Azure CLI

Here's a sample command to get the connection string for a namespace. `MyAuthRuleName` is the name of the shared access policy. For a namespace, there's a default one: `RootManageSharedAccessKey`

```azurecli-interactive

az eventhubs namespace authorization-rule keys list --resource-group MyResourceGroupName --namespace-name MyNamespaceName --name RootManageSharedAccessKey

```

Here's a sample command to get the connection string for a specific event hub within a namespace:

```azurecli-interactive

az eventhubs eventhub authorization-rule keys list --resource-group MyResourceGroupName --namespace-name MyNamespaceName --eventhub-name MyEventHubName --name MyAuthRuleName

```

Here's a sample command to get the connection string for an event hub in a Geo-DR cluster, which has an alias.

```azurecli-interactive

az eventhubs georecovery-alias authorization-rule keys list --resource-group MyResourceGroupName --namespace-name MyNamespaceName --eventhub-name MyEventHubName --alias-name MyAliasName --name MyAuthRuleName

```

For more information about Azure CLI commands for Event Hubs, see [Azure CLI for Event Hubs](/cli/azure/eventhubs).

## Related content

You can learn more about Event Hubs by visiting the following links:

* [Event Hubs overview](./event-hubs-about.md)

* [Create an event hub](event-hubs-create.md)


# Connect Event Hub

# Connect to an event hub (.NET)

This article shows how to connect to an event hub in different ways by using the .NET SDK. The examples use [EventHubProducerClient](/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient), which is used to send messages to an event hub. You can use similar variations of constructors for [EventHubConsumerClient](/dotnet/api/azure.messaging.eventhubs.consumer.eventhubconsumerclient) to consume events from an event hub.

## Connect using a connection string

This section shows how to connect to an event hub using a connection string to a namespace or an event hub.

If you have connection string to the namespace and the event hub name, use the [EventHubProducerClient](/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient) constructor that has the connection string and the event hub name parameter.

```csharp

// Use the constructor that takes the connection string to the namespace and event hub name

producerClient = new EventHubProducerClient(NAMESPACE-CONNECTIONSTRING, EVENTHUBNAME);

```

Alternatively, you can append `;EntityPath=<EVENTHUBNAME>` the namespace's connection string and use the constructor that takes only the connection string.

```csharp

// Use the constructor that takes the connection string to the namespace and event hub name

producerClient = new EventHubProducerClient(connectionString);

```

You can also use this constructor if you have a connection string to the event hub (not the namespace).

## Connect using a policy name and its key value

The following example shows you how to connect to an event hub using a name and value of the SAS policy you created for an event hub.

```csharp

//use the constructor that takes AzureNamedKeyCredential parameter

producerClient = new EventHubProducerClient("<NAMESPACENAME>.servicebus.windows.net", "EVENTHUBNAME", new AzureNamedKeyCredential("SASPOLICYNAME", "KEYVALUE"));

```

## Connect using a SAS token

The following example shows you how to connect to an event hub using a SAS token that's generated using a SAS policy.

```csharp

var token = createToken("NAMESPACENAME.servicebus.windows.net", "SASPOLICYNAME", "KEYVALUE");

producerClient = new EventHubProducerClient("NAMESPACENAME.servicebus.windows.net", "EVENTHUBNAME", new AzureSasCredential(token));

```

Here's the sample code for generating a token using a SAS policy and key value:

```csharp

private static string createToken(string resourceUri, string keyName, string key)

{

TimeSpan sinceEpoch = DateTime.UtcNow - new DateTime(1970, 1, 1);

var week = 60 * 60 * 24 * 7;

var expiry = Convert.ToString((int)sinceEpoch.TotalSeconds + week);

string stringToSign = HttpUtility.UrlEncode(resourceUri) + "\n" + expiry;

HMACSHA256 hmac = new HMACSHA256(Encoding.UTF8.GetBytes(key));

var signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(stringToSign)));

var sasToken = String.Format(CultureInfo.InvariantCulture, "SharedAccessSignature sr={0}&sig={1}&se={2}&skn={3}", HttpUtility.UrlEncode(resourceUri), HttpUtility.UrlEncode(signature), expiry, keyName);

return sasToken;

}

```

<a name='connect-using-azure-ad-application'></a>

## Connect using Microsoft Entra application

1. Create a Microsoft Entra application.

1. Assign application's service principal to the appropriate [role-based access control (RBAC) role](authorize-access-azure-active-directory.md#azure-built-in-roles-for-azure-event-hubs) (owner, sender, or receiver). For more information, see [Authorize access with Microsoft Entra ID](authorize-access-azure-active-directory.md).

```csharp

var clientSecretCredential = new ClientSecretCredential("TENANTID", "CLIENTID", "CLIENTSECRET");

producerClient = new EventHubProducerClient("NAMESPACENAME.servicebus.windows.net", "EVENTHUBNAME", clientSecretCredential);

```

## Next steps

Review samples on GitHub:

* [Azure.Messaging.EventHubs samples](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/eventhub/Azure.Messaging.EventHubs/samples)

* [Azure.Messaging.EventHubs.Processor](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/eventhub/Azure.Messaging.EventHubs.Processor)


# Configure Processing Units Premium Namespace

# Configure processing units for a premium tier Azure Event Hubs namespace

This article provides instructions for configuring processing units (PUs) for a premium tier Azure Event Hubs namespace. To learn more about the **premium** tier, see [Event Hubs Premium](event-hubs-premium-overview.md).

## Configure processing units when creating a namespace

You can configure the number of processing units (PUs) for your namespace (1, 2, 4, 6, 8, 10, 12, or 16) at the time of creating a premium namespace. You see the setting on **Basics** page of the creation wizard as shown in the following image:

## Configure processing units for an existing namespace

To update the number of PUs for an existing premium namespace, follow these steps:

1. On the **Event Hubs namespace** page for your namespace, select **Scale** under **Settings** on the left menu.

1. Update the value for **processing units**, and select **Save**.

## Related content

To learn more about processing units and Event Hubs premium tier, see the following articles.

- [Event Hubs Premium](event-hubs-premium-overview.md)

- [Event Hubs scalability](event-hubs-scalability.md)


# Add Custom Data Event

# Add custom data to events in Azure Event Hubs

Because an event consists mainly of an opaque set of bytes, it may be difficult for consumers of those events to make informed decisions about how to process them. To allow event publishers to offer better context for consumers, events may also contain custom metadata, in the form of a set of key-value pairs. One common scenario for the inclusion of metadata is to provide a hint about the type of data contained by an event, so that consumers understand its format and can deserialize it appropriately.

> [!NOTE]

> This metadata is not used by, or in any way meaningful to, the Event Hubs service; it exists only for coordination between event publishers and consumers.

The following sections show you how to add custom data to events in different programming languages.

## .NET

```csharp

var eventBody = new BinaryData("Hello, Event Hubs!");

var eventData = new EventData(eventBody);

eventData.Properties.Add("EventType", "com.microsoft.samples.hello-event");

eventData.Properties.Add("priority", 1);

eventData.Properties.Add("score", 9.0);

```

For the full code sample, see [Publishing events with custom metadata](https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/eventhub/Azure.Messaging.EventHubs/samples/Sample04_PublishingEvents.md#publishing-events-with-custom-metadata).

## Java

```java

EventData firstEvent = new EventData("EventData Sample 1".getBytes(UTF_8));

firstEvent.getProperties().put("EventType", "com.microsoft.samples.hello-event");

firstEvent.getProperties().put("priority", 1);

firstEvent.getProperties().put("score", 9.0);

```

For the full code sample, see [Publish events with custom metadata](https://github.com/Azure/azure-sdk-for-java/blob/master/sdk/eventhubs/azure-messaging-eventhubs/src/samples/java/com/azure/messaging/eventhubs/PublishEventsWithCustomMetadata.java).

## Python

```python

event_data = EventData('Message with properties')

event_data.properties = {'event-type': 'com.microsoft.samples.hello-event', 'priority': 1, "score": 9.0}

```

For the full code sample, see [Send Event Data batch with properties](https://github.com/Azure/azure-sdk-for-python/blob/azure-eventhub_5.3.1/sdk/eventhub/azure-eventhub/samples/async_samples/send_async.py).

## JavaScript

```javascript

let eventData = { body: "First event", properties: { "event-type": "com.microsoft.samples.hello-event", "priority": 1, "score": 9.0  } };

```

## Next steps

See the following quickstarts and samples.

- Quickstarts: [.NET](event-hubs-dotnet-standard-getstarted-send.md), [Java](event-hubs-java-get-started-send.md), [Python](event-hubs-python-get-started-send.md), [JavaScript](event-hubs-node-get-started-send.md)

- Samples on GitHub: [.NET](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/eventhub/Azure.Messaging.EventHubs/samples), [Java](https://github.com/Azure/azure-sdk-for-java/blob/master/sdk/eventhubs/azure-messaging-eventhubs/src/samples), [Python](https://github.com/Azure/azure-sdk-for-python/blob/azure-eventhub_5.3.1/sdk/eventhub/azure-eventhub/samples), [JavaScript](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/eventhub/event-hubs/samples/v5/javascript), [TypeScript](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/eventhub/event-hubs/samples/v5/typescript)


# Dynamically Add Partitions

# Dynamically add partitions to an event hub (Apache Kafka topic)

Event Hubs provides message streaming through a partitioned consumer pattern in which each consumer only reads a specific subset, or partition, of the message stream. This pattern enables horizontal scale for event processing and provides other stream-focused features that are unavailable in queues and topics. A partition is an ordered sequence of events that is held in an event hub. As newer events arrive, they're added to the end of this sequence. For more information about partitions in general, see [Partitions](event-hubs-scalability.md#partitions)

You can specify the number of partitions at the time of creating an event hub. In some scenarios, you may need to add partitions after the event hub has been created. This article describes how to dynamically add partitions to an existing event hub.

> [!IMPORTANT]

> Dynamic additions of partitions is available only in **premium** and **dedicated** tiers of Event Hubs.

> [!NOTE]

> For Apache Kafka clients, an **event hub** maps to a **Kafka topic**. For more mappings between Azure Event Hubs and Apache Kafka, see [Kafka and Event Hubs conceptual mapping](azure-event-hubs-apache-kafka-overview.md#apache-kafka-and-azure-event-hubs-conceptual-mapping)

## Update the partition count

This section shows you how to update partition count of an event hub in different ways (PowerShell, CLI, and so on.).

### PowerShell

Use the [Set-AzEventHub](/powershell/module/az.eventhub/set-azeventhub) PowerShell command to update partitions in an event hub.

```azurepowershell-interactive

Set-AzEventHub -ResourceGroupName MyResourceGroupName -Namespace MyNamespaceName -Name MyEventHubName -partitionCount 12

```

### CLI

Use the [`az eventhubs eventhub update`](/cli/azure/eventhubs/eventhub#az-eventhubs-eventhub-update) CLI command to update partitions in an event hub.

```azurecli-interactive

az eventhubs eventhub update --resource-group MyResourceGroupName --namespace-name MyNamespaceName --name MyEventHubName --partition-count 12

```

### Resource Manager template

Update value of the `partitionCount` property in the Resource Manager template and redeploy the template to update the resource.

```json

{

"apiVersion": "2017-04-01",

"type": "Microsoft.EventHub/namespaces/eventhubs",

"name": "[concat(parameters('namespaceName'), '/', parameters('eventHubName'))]",

"location": "[parameters('location')]",

"dependsOn": [

"[resourceId('Microsoft.EventHub/namespaces', parameters('namespaceName'))]"

],

"properties": {

"messageRetentionInDays": 7,

"partitionCount": 12

}

}

```

### Apache Kafka

Use the `AlterTopics` API (for example, via **kafka-topics** CLI tool) to increase the partition count. For details, see [Modifying Kafka topics](http://kafka.apache.org/documentation/#basic_ops_modify_topic).

## Event Hubs clients

Let's look at how Event Hubs clients behave when the partition count is updated on an event hub.

When you add a partition to an existing even hub, the event hub client receives a `MessagingException` from the service informing the clients that entity metadata (entity is your event hub and metadata is the partition information) has been altered. The clients will automatically reopen the AMQP links, which would then pick up the changed metadata information. The clients then operate normally.

### Sender/producer clients

Event Hubs provides three sender options:

- **Partition sender** – In this scenario, clients send events directly to a partition. Although partitions are identifiable and events can be sent directly to them, we don't recommend this pattern. Adding partitions doesn't impact this scenario. We recommend that you restart applications so that they can detect newly added partitions.

- **Partition key sender** – in this scenario, clients sends the events with a key so that all events belonging to that key end up in the same partition. In this case, service hashes the key and routes to the corresponding partition. The partition count update can cause out-of-order issues because of hashing change. So, if you care about ordering, ensure that your application consumes all events from existing partitions before you increase the partition count.

- **Round-robin sender (default)** – In this scenario, the Event Hubs service round robins the events across partitions, and also uses a load-balancing algorithm. Event Hubs service is aware of partition count changes and will send to new partitions within seconds of altering partition count.

### Receiver/consumer clients

Event Hubs provides direct receivers and an easy consumer library called the [Event Processor](event-processor-balance-partition-load.md).

- **Direct receivers** – The direct receivers listen to specific partitions. Their runtime behavior isn't affected when partitions are scaled out for an event hub. The application that uses direct receivers needs to take care of picking up the new partitions and assigning the receivers accordingly.

- **Event processor host** – This client doesn't automatically refresh the entity metadata. So, it wouldn't pick up on partition count increase. Recreating an event processor instance will cause an entity metadata fetch, which in turn will create new blobs for the newly added partitions. Pre-existing blobs won't be affected. Restarting all event processor instances is recommended to ensure that all instances are aware of the newly added partitions, and load-balancing is handled correctly among consumers.

If you're using the old version of .NET SDK ([WindowsAzure.ServiceBus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/)), the event processor host removes an existing checkpoint upon restart if partition count in the checkpoint doesn't match the partition count fetched from the service. This behavior may have an impact on your application.

[!INCLUDE [service-bus-track-0-and-1-sdk-support-retirement](../../includes/service-bus-track-0-and-1-sdk-support-retirement.md)]

## Apache Kafka clients

This section describes how Apache Kafka clients that use the Kafka endpoint of Azure Event Hubs behave when the partition count is updated for an event hub.

Kafka clients that use Event Hubs with the Apache Kafka protocol behave differently from event hub clients that use AMQP protocol. Kafka clients update their metadata once every `metadata.max.age.ms` milliseconds. You specify this value in the client configurations. The `librdkafka` libraries also use the same configuration. Metadata updates inform the clients of service changes including the partition count increases. For a list of configurations, see [Apache Kafka configurations for Event Hubs](apache-kafka-configurations.md).

### Sender/producer clients

Producers always dictate that send requests contain the partition destination for each set of produced records. So, all produce partitioning is done on client-side with producer’s view of broker's metadata. Once the new partitions are added to the producer’s metadata view, they'll be available for producer requests.

### Consumer/receiver clients

When a consumer group member performs a metadata refresh and picks up the newly created partitions, that member initiates a group rebalance. Consumer metadata then will be refreshed for all group members, and the new partitions will be assigned by the allotted rebalance leader.

## Recommendations

- If you use partition key with your producer applications and depend on key hashing to ensure ordering in a partition, dynamically adding partitions isn't recommended.

> [!IMPORTANT]

> While the existing data preserves ordering, partition hashing will be broken for messages hashed after the partition count changes due to addition of partitions.

- Adding partition to an existing topic or event hub instance is recommended in the following cases:

- When you use the default method of sending events

- Kafka default partitioning strategies, example – Sticky Assignor strategy

## Next steps

For more information about partitions, see [Partitions](event-hubs-scalability.md#partitions).


# Event Hubs Exchange Events Different Protocols

# Exchange events between consumers and producers that use different protocols: AMQP, Kafka, and HTTPS

Azure Event Hubs supports three protocols for consumers and producers: AMQP, Kafka, and HTTPS. Each one of these protocols has its own way of representing a message, so naturally the following question arises: if an application sends events to an Event Hub with one protocol and consumes them with a different protocol, what do the various parts and values of the event look like when they arrive at the consumer? This article discusses best practices for both producer and consumer to ensure that the values within an event are correctly interpreted by the consuming application.

The advice in this article specifically covers these clients, with the listed versions used in developing the code snippets:

* Kafka Java client (version 1.1.1 from https://www.mvnrepository.com/artifact/org.apache.kafka/kafka-clients)

* Microsoft Azure Event Hubs Client for Java (version 1.1.0 from https://github.com/Azure/azure-event-hubs-java)

* Microsoft Azure Event Hubs Client for .NET (version 2.1.0 from https://github.com/Azure/azure-event-hubs-dotnet)

* HTTPS (supports producers only)

Other AMQP clients may behave slightly differently. AMQP has a well-defined type system, but the specifics of serializing language-specific types to and from that type system depends on the client, as does how the client provides access to the parts of an AMQP message.

## Event Body

All of the Microsoft AMQP clients represent the event body as an uninterpreted bag of bytes. A producing application passes a sequence of bytes to the client, and a consuming application receives that same sequence from the client. The interpretation of byte sequence happens within the application code.

When sending an event via HTTPS, the event body is the POSTed content, which is also treated as uninterpreted bytes. It is easy to achieve the same state in a Kafka producer or consumer by using the provided ByteArraySerializer and ByteArrayDeserializer as shown in the following code:

### Kafka byte[] producer

```java

final Properties properties = new Properties();

// add other properties

properties.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, ByteArraySerializer.class.getName());

final KafkaProducer<byte[], byte[]> producer = new KafkaProducer<byte[], byte[]>(properties);

final byte[] eventBody = new byte[] { 0x01, 0x02, 0x03, 0x04 };

ProducerRecord<byte[], byte[]> pr =

new ProducerRecord<byte[], byte[]>(myTopic, myPartitionId, myTimeStamp, eventBody);

```

### Kafka byte[] consumer

```java

final Properties properties = new Properties();

// add other properties

properties.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, ByteArrayDeserializer.class.getName());

final KafkaConsumer<byte[], byte[]> consumer = new KafkaConsumer<byte[], byte[]>(properties);

ConsumerRecord<byte[], byte[]> cr = /* receive event */

// cr.value() is a byte[] with values { 0x01, 0x02, 0x03, 0x04 }

```

This code creates a transparent byte pipeline between the two halves of the application and allows the application developer to manually serialize and deserialize in any way desired, including making deserialization decisions at runtime, for example based on type or sender information in user-set properties on the event.

Applications that have a single, fixed event body type may be able to use other Kafka serializers, and deserializers to transparently convert data. For example, consider an application, which uses JSON. The construction and interpretation of the JSON string happens at the application level. At the Event Hubs level, the event body is always a string, a sequence of bytes representing characters in the UTF-8 encoding. In this case, the Kafka producer or consumer can take advantage of the provided

StringSerializer or StringDeserializer as shown in the following code:

### Kafka UTF-8 string producer

```java

final Properties properties = new Properties();

// add other properties

properties.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());

final KafkaProducer<Long, String> producer = new KafkaProducer<Long, String>(properties);

final String exampleJson = "{\"name\":\"John\", \"number\":9001}";

ProducerRecord<Long, String> pr =

new ProducerRecord<Long, String>(myTopic, myPartitionId, myTimeStamp, exampleJson);

```

### Kafka UTF-8 string consumer

```java

final Properties properties = new Properties();

// add other properties

properties.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());

final KafkaConsumer<Long, String> consumer = new KafkaConsumer<Long, String>(properties);

ConsumerRecord<Long, Bytes> cr = /* receive event */

final String receivedJson = cr.value();

```

For the AMQP side, both Java and .NET provide built-in ways to convert strings to and from UTF-8 byte sequences. The Microsoft AMQP clients represent events as a class named EventData. The following examples show you how to serialize a UTF-8 string into an EventData event body in an AMQP producer, and how to deserialize an EventData event body into a UTF-8 string in an AMQP consumer.

### Java AMQP UTF-8 string producer

```java

final String exampleJson = "{\"name\":\"John\", \"number\":9001}";

final EventData ed = EventData.create(exampleJson.getBytes(StandardCharsets.UTF_8));

```

### Java AMQP UTF-8 string consumer

```java

EventData ed = /* receive event */

String receivedJson = new String(ed.getBytes(), StandardCharsets.UTF_8);

```

### C# .NET UTF-8 string producer

```csharp

string exampleJson = "{\"name\":\"John\", \"number\":9001}";

EventData working = new EventData(Encoding.UTF8.GetBytes(exampleJson));

```

### C# .NET UTF-8 string consumer

```csharp

EventData ed = /* receive event */

// getting the event body bytes depends on which .NET client is used

byte[] bodyBytes = ed.Body.Array;  // Microsoft Azure Event Hubs Client for .NET

// byte[] bodyBytes = ed.GetBytes(); // Microsoft Azure Service Bus

string receivedJson = Encoding.UTF8.GetString(bodyBytes);

```

Because Kafka is open-source, the application developer can inspect the implementation of any serializer or deserializer and implement code, which produces or consumes a compatible sequence of bytes on the AMQP side.

## Event User Properties

User-set properties can be set and retrieved from both AMQP clients (in the Microsoft AMQP clients they are called properties) and Kafka (where they are called headers). HTTPS senders can set user properties on an event by supplying them as HTTP headers in the POST operation. However, Kafka treats both event bodies and event header values as byte sequences. Whereas in AMQP clients, property values have types, which are communicated by encoding the property values according to the AMQP type system.

HTTPS is a special case. At the point of sending, all property values are UTF-8 text. The Event Hubs service does a limited amount of interpretation to convert appropriate property values to AMQP-encoded 32-bit and 64-bit signed integers, 64-bit floating point numbers, and booleans. Any property value, which does not fit one of those types is treated as a string.

Mixing these approaches to property typing means that a Kafka consumer sees the raw AMQP-encoded byte sequence, including the AMQP type information. Whereas an AMQP consumer sees the untyped byte sequence sent by the Kafka producer, which the application must interpret.

For Kafka consumers that receive properties from AMQP or HTTPS producers, use the AmqpDeserializer class, which is modeled after the other deserializers in the Kafka ecosystem. It interprets the type information in the AMQP-encoded byte sequences to deserialize the data bytes into a Java type.

As a best practice, we recommend that you include a property in messages sent via AMQP or HTTPS. The Kafka consumer can use it to determine whether header values need AMQP deserialization. The value of the property is not important. It just needs a well-known name that the Kafka consumer can find in the list of headers and

adjust its behavior accordingly.

> [!NOTE]

> The Event Hubs service natively converts some of the EventHubs specific [AmqpMessage properties](http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-messaging-v1.0-os.html#type-properties) to [Kafka’s record headers](https://kafka.apache.org/32/javadoc/org/apache/kafka/common/header/Headers.html) as **strings**. Kafka message header is a list of &lt;key, value&gt; pairs where key is string and value is always a byte array. For these supported properties, the byte array will have an UTF8encoded string.

>

> Here is the list of immutable properties that Event Hubs support in this conversion today. If you set values for user properties with the names in this list, you don’t need to deserialize at the Kafka consumer side.

>

> - message-id

> - user-id

> - to

> - reply-to

> - content-type

> - content-encoding

> - creation-time

### AMQP to Kafka part 1: create and send an event in C# (.NET) with properties

```csharp

// Create an event with properties "MyStringProperty" and "MyIntegerProperty"

EventData working = new EventData(Encoding.UTF8.GetBytes("an event body"));

working.Properties.Add("MyStringProperty", "hello");

working.Properties.Add("MyIntegerProperty", 1234);

// BEST PRACTICE: include a property which indicates that properties will need AMQP deserialization

working.Properties.Add("AMQPheaders", 0);

```

### AMQP to Kafka part 2: use AmqpDeserializer to deserialize those properties in a Kafka consumer

```java

final AmqpDeserializer amqpDeser = new AmqpDeserializer();

ConsumerRecord<Long, Bytes> cr = /* receive event */

final Header[] headers = cr.headers().toArray();

final Header headerNamedMyStringProperty = /* find header with key "MyStringProperty" */

final Header headerNamedMyIntegerProperty = /* find header with key "MyIntegerProperty" */

final Header headerNamedAMQPheaders = /* find header with key "AMQPheaders", or null if not found */

// BEST PRACTICE: detect whether AMQP deserialization is needed

if (headerNamedAMQPheaders != null) {

// The deserialize() method requires no prior knowledge of a property's type.

// It returns Object and the application can check the type and perform a cast later.

Object propertyOfUnknownType = amqpDeser.deserialize("topicname", headerNamedMyStringProperty.value());

if (propertyOfUnknownType instanceof String) {

final String propertyString = (String)propertyOfUnknownType;

// do work here

}

propertyOfUnknownType = amqpDeser.deserialize("topicname", headerNamedMyIntegerProperty.value());

if (propertyOfUnknownType instanceof Integer) {

final Integer propertyInt = (Integer)propertyOfUnknownType;

// do work here

}

} else {

/* event sent via Kafka, interpret header values the Kafka way */

}

```

If the application knows the expected type for a property, there are deserialization methods that do not require a cast afterwards, but they throw an error if the property is not of the expected type.

### AMQP to Kafka part 3: a different way of using AmqpDeserializer in a Kafka consumer

```java

// BEST PRACTICE: detect whether AMQP deserialization is needed

if (headerNamedAMQPheaders != null) {

// Property "MyStringProperty" is expected to be of type string.

try {

final String propertyString = amqpDeser.deserializeString(headerNamedMyStringProperty.value());

// do work here

}

catch (IllegalArgumentException e) {

// property was not a string

}

// Property "MyIntegerProperty" is expected to be a signed integer type.

// The method returns long because long can represent the value range of all AMQP signed integer types.

try {

final long propertyLong = amqpDeser.deserializeSignedInteger(headerNamedMyIntegerProperty.value());

// do work here

}

catch (IllegalArgumentException e) {

// property was not a signed integer

}

} else {

/* event sent via Kafka, interpret header values the Kafka way */

}

```

Going the other direction is more involved, because headers set by a Kafka producer are always seen by an AMQP consumer as raw bytes (type org.apache.qpid.proton.amqp.Binary for the Microsoft Azure Event Hubs Client for Java, or `System.Byte[]` for Microsoft's .NET AMQP clients). The easiest path is to use one of the Kafka-supplied serializers to generate the bytes for the header values on the Kafka producer side, and then write a compatible deserialization code on the AMQP consumer side.

As with AMQP-to-Kafka, the best practice that we recommend is to include a property in messages sent via Kafka. The AMQP consumer can use the property to determine whether header values need deserialization. The value of the property is not important. It just needs a well-known name that the AMQP consumer can find in the list of headers and adjust its behavior accordingly. If the Kafka producer cannot be changed, it is also possible for the consuming application to check whether the property value is of a binary or byte type and attempt deserialization based on the type.

### Kafka to AMQP part 1: create and send an event from Kafka with properties

```java

final String topicName = /* topic name */

final ProducerRecord<Long, String> pr = new ProducerRecord<Long, String>(topicName, /* other arguments */);

final Headers h = pr.headers();

// Set headers using Kafka serializers

IntegerSerializer intSer = new IntegerSerializer();

h.add("MyIntegerProperty", intSer.serialize(topicName, 1234));

LongSerializer longSer = new LongSerializer();

h.add("MyLongProperty", longSer.serialize(topicName, 5555555555L));

ShortSerializer shortSer = new ShortSerializer();

h.add("MyShortProperty", shortSer.serialize(topicName, (short)22222));

FloatSerializer floatSer = new FloatSerializer();

h.add("MyFloatProperty", floatSer.serialize(topicName, 1.125F));

DoubleSerializer doubleSer = new DoubleSerializer();

h.add("MyDoubleProperty", doubleSer.serialize(topicName, Double.MAX_VALUE));

StringSerializer stringSer = new StringSerializer();

h.add("MyStringProperty", stringSer.serialize(topicName, "hello world"));

// BEST PRACTICE: include a property which indicates that properties will need deserialization

h.add("RawHeaders", intSer.serialize(0));

```

### Kafka to AMQP part 2: manually deserialize those properties in C# (.NET)

```csharp

EventData ed = /* receive event */

// BEST PRACTICE: detect whether manual deserialization is needed

if (ed.Properties.ContainsKey("RawHeaders"))

{

// Kafka serializers send bytes in big-endian order, whereas .NET on x86/x64 is little-endian.

// Therefore it is frequently necessary to reverse the bytes before further deserialization.

byte[] rawbytes = ed.Properties["MyIntegerProperty"] as System.Byte[];

if (BitConverter.IsLittleEndian)

{

Array.Reverse(rawbytes);

}

int myIntegerProperty = BitConverter.ToInt32(rawbytes, 0);

rawbytes = ed.Properties["MyLongProperty"] as System.Byte[];

if (BitConverter.IsLittleEndian)

{

Array.Reverse(rawbytes);

}

long myLongProperty = BitConverter.ToInt64(rawbytes, 0);

rawbytes = ed.Properties["MyShortProperty"] as System.Byte[];

if (BitConverter.IsLittleEndian)

{

Array.Reverse(rawbytes);

}

short myShortProperty = BitConverter.ToInt16(rawbytes, 0);

rawbytes = ed.Properties["MyFloatProperty"] as System.Byte[];

if (BitConverter.IsLittleEndian)

{

Array.Reverse(rawbytes);

}

float myFloatProperty = BitConverter.ToSingle(rawbytes, 0);

rawbytes = ed.Properties["MyDoubleProperty"] as System.Byte[];

if (BitConverter.IsLittleEndian)

{

Array.Reverse(rawbytes);

}

double myDoubleProperty = BitConverter.ToDouble(rawbytes, 0);

rawbytes = ed.Properties["MyStringProperty"] as System.Byte[];

string myStringProperty = Encoding.UTF8.GetString(rawbytes);

}

```

### Kafka to AMQP part 3: manually deserialize those properties in Java

```java

final EventData ed = /* receive event */

// BEST PRACTICE: detect whether manual deserialization is needed

if (ed.getProperties().containsKey("RawHeaders")) {

byte[] rawbytes =

((org.apache.qpid.proton.amqp.Binary)ed.getProperties().get("MyIntegerProperty")).getArray();

int myIntegerProperty = 0;

for (byte b : rawbytes) {

myIntegerProperty <<= 8;

myIntegerProperty |= ((int)b & 0x00FF);

}

rawbytes = ((org.apache.qpid.proton.amqp.Binary)ed.getProperties().get("MyLongProperty")).getArray();

long myLongProperty = 0;

for (byte b : rawbytes) {

myLongProperty <<= 8;

myLongProperty |= ((long)b & 0x00FF);

}

rawbytes = ((org.apache.qpid.proton.amqp.Binary)ed.getProperties().get("MyShortProperty")).getArray();

short myShortProperty = (short)rawbytes[0];

myShortProperty <<= 8;

myShortProperty |= ((short)rawbytes[1] & 0x00FF);

rawbytes = ((org.apache.qpid.proton.amqp.Binary)ed.getProperties().get("MyFloatProperty")).getArray();

int intbits = 0;

for (byte b : rawbytes) {

intbits <<= 8;

intbits |= ((int)b & 0x00FF);

}

float myFloatProperty = Float.intBitsToFloat(intbits);

rawbytes = ((org.apache.qpid.proton.amqp.Binary)ed.getProperties().get("MyDoubleProperty")).getArray();

long longbits = 0;

for (byte b : rawbytes) {

longbits <<= 8;

longbits |= ((long)b & 0x00FF);

}

double myDoubleProperty = Double.longBitsToDouble(longbits);

rawbytes = ((org.apache.qpid.proton.amqp.Binary)ed.getProperties().get("MyStringProperty")).getArray();

String myStringProperty = new String(rawbytes, StandardCharsets.UTF_8);

}

```

## Next steps

In this article, you learned how to stream into Event Hubs without changing your protocol clients or running your own clusters. To learn more about Event Hubs and Event Hubs for Kafka, see the following articles:

* [Learn about Event Hubs](./event-hubs-about.md)

* [Learn about Event Hubs for Kafka](azure-event-hubs-apache-kafka-overview.md)

* [Explore more samples on the Event Hubs for Kafka GitHub](https://github.com/Azure/azure-event-hubs-for-kafka)

* Use [MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) to [stream events from Kafka on premises to Event Hubs on cloud.](event-hubs-kafka-mirror-maker-tutorial.md)

* Learn how to stream into Event Hubs using [native Kafka applications](event-hubs-quickstart-kafka-enabled-event-hubs.md), [Apache Flink](event-hubs-kafka-flink-tutorial.md), or [Akka Streams](event-hubs-kafka-akka-streams-tutorial.md)


# Test Locally With Event Hub Emulator

# Test locally by using the Azure Event Hubs emulator

The Azure Event Hubs emulator enables developers to test and validate their applications locally without connecting to the cloud. This guide provides step-by-step instructions for setting up, running, and interacting with the emulator using Docker or automated scripts.

## Prerequisites

- [Docker desktop](https://docs.docker.com/desktop/install/windows-install/#:~:text=Install%20Docker%20Desktop%20on%20Windows%201%20Download%20the,on%20your%20choice%20of%20backend.%20...%20More%20items)

- Minimum hardware requirements:

- 2 GB of RAM

- 5 GB of disk space

- Windows Subsystem for Linux (WSL) configuration (only for Windows):

- [Install WSL](/windows/wsl/install)

- [Configure Docker to use WSL](https://docs.docker.com/desktop/wsl/#:~:text=Turn%20on%20Docker%20Desktop%20WSL%202%201%20Download,engine%20..%20...%206%20Select%20Apply%20%26%20Restart)

> [!NOTE]

> Before you continue with the steps in this article, make sure Docker Desktop is operational in the background.

## Run the Azure Event Hubs emulator

Run the Azure Event Hubs emulator using either an automated script or a Linux container. Choose the method that best fits your development environment.

### [Automated script](#tab/automated-script)

Before you run an automated script, clone the emulator's [GitHub installer repository](https://github.com/Azure/azure-event-hubs-emulator-installer) locally.

### Windows

Use the following steps to run the Event Hubs emulator locally on Windows.

1. **Open PowerShell** and navigate to the directory where the [common](https://github.com/Azure/azure-event-hubs-emulator-installer/tree/main/EventHub-Emulator/Scripts/Common) scripts folder is cloned using `cd`:

```powershell

cd <path to your common scripts folder> # Update this path

2. Issue wsl command to open WSL at this directory.

```powershell

wsl

3. **Run the setup script** *./LaunchEmulator.sh* Running the script brings up two containers: the Event Hubs emulator and Azurite (a dependency for the emulator).

```bash

./Launchemulator.sh

### Linux and macOS

To run the Event Hubs emulator locally on Linux or macOS:

- Run the setup script *LaunchEmulator.sh*. Running the script brings up two containers: the Event Hubs emulator and Azurite (a dependency for the emulator).

### [Docker (Linux container)](#tab/docker-linux-container)

1. To start the emulator, supply a configuration for the entities that you want to use. Save the following JSON file locally as *config.json*:

```JSON

{

"UserConfig": {

"NamespaceConfig": [

{

"Type": "EventHub",

"Name": "emulatorNs1",

"Entities": [

{

"Name": "eh1",

"PartitionCount": "2",

"ConsumerGroups": [

{

"Name": "cg1"

}

]

}

]

}

],

"LoggingConfig": {

"Type": "File"

}

}

}

```

2. To spin up containers for Event Hubs emulator, Save the following .yaml file as *docker-compose.yaml*.

```yaml

name: microsoft-azure-eventhubs

services:

emulator:

container_name: "eventhubs-emulator"

image: "mcr.microsoft.com/azure-messaging/eventhubs-emulator:latest"

pull_policy: always

volumes:

- "${CONFIG_PATH}:/Eventhubs_Emulator/ConfigFiles/Config.json"

ports:

- "5672:5672"

- "9092:9092"

- "5300:5300"

environment:

BLOB_SERVER: azurite

METADATA_SERVER: azurite

ACCEPT_EULA: ${ACCEPT_EULA}

depends_on:

- azurite

networks:

eh-emulator:

aliases:

- "eventhubs-emulator"

azurite:

container_name: "azurite"

image: "mcr.microsoft.com/azure-storage/azurite:latest"

pull_policy: always

ports:

- "10000:10000"

- "10001:10001"

- "10002:10002"

networks:

eh-emulator:

aliases:

- "azurite"

networks:

eh-emulator:

```

3. Create an .env file to declare the environment variables for the Event Hubs emulator:

```

# Centralized environment variables store for docker-compose

# 1. CONFIG_PATH: Path to config.json file

CONFIG_PATH="<Replace with path to config.json file>"

# 2. ACCEPT_EULA: Pass 'Y' to accept license terms.

ACCEPT_EULA="N"

```

The argument `ACCEPT_EULA` confirms the [Microsoft Software License Terms](https://github.com/Azure/azure-event-hubs-emulator-installer/blob/main/EMULATOR_EULA.md). Be sure to place the .env file in the same directory as the *docker-compose.yaml* file.

> [!IMPORTANT]

> When you're specifying file paths in Windows, use double backslashes (`\\`) instead of single backslashes (`\`) to avoid confusion with escape characters.

4. To run the emulator, execute the following command:

```

docker compose -f <PathToDockerComposeFile> up -d

```

---

After the steps are successful, you can find the containers running in Docker.

## Interact with the emulator

By default, emulator uses [config.json](https://github.com/Azure/azure-event-hubs-emulator-installer/blob/main/EventHub-Emulator/Config/Config.json) configuration file. You can configure entities (Event Hubs/ Kafka topics) by making changes to configuration file. To know more, visit [make configuration changes](overview-emulator.md#quota-configuration-changes)

You can use the following connection string to connect to the Event Hubs emulator:

- When the emulator container and interacting application are running natively on local machine, use following connection string:

```

"Endpoint=sb://localhost;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=SAS_KEY_VALUE;UseDevelopmentEmulator=true;"

```

- Applications (Containerized/Non-containerized) on the different machine and same local network can interact with Emulator using the IPv4 address of the machine. Use following connection string:

```

"Endpoint=sb://192.168.y.z;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=SAS_KEY_VALUE;UseDevelopmentEmulator=true;"

```

- Application containers on the same bridge network can interact with Emulator using its alias or IP. Following connection string assumes the name of Emulator has default value that is"eventhubs-emulator":

```

"Endpoint=sb://eventhubs-emulator;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=SAS_KEY_VALUE;UseDevelopmentEmulator=true;"

```

- Application containers on the different bridge network can interact with Emulator using the "host.docker.internal" as host. Use following connection string:

```

"Endpoint=sb://host.docker.internal;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=SAS_KEY_VALUE;UseDevelopmentEmulator=true;"

```

### [Using Kafka](#tab/using-kafka)

While interacting with Kafka, ensure to set the Producer and consumer config as following:

```

{

BootstrapServers =  //Value of bootstrap servers would depend on kind of connection string being used

SecurityProtocol = SecurityProtocol.SaslPlaintext,

SaslMechanism = SaslMechanism.Plain,

SaslUsername = "$ConnectionString",

SaslPassword = //Value of connection string would depend on topology

};

```

Value of BootstrapServers and SaslPassword would depend on your setup topology. Refer to [Interact with Emulator](#interact-with-the-emulator) section for details.

> [!IMPORTANT]

> When using Kafka, only Producer and consumer APIs are compatible with Event Hubs emulator.

### [Using AMQP](#tab/using-amqp)

With the latest client SDK releases, you can interact with the emulator in various programming languages. For details, see

[Client SDKs](./sdks.md).

---

To get started, refer to the [Event Hubs emulator samples on GitHub](https://github.com/Azure/azure-event-hubs-emulator-installer/tree/main/Sample-Code-Snippets/dotnet/EventHubs-Emulator-Demo/EventHubs-Emulator-Demo).

## Related content

[Overview of the Azure Event Hubs emulator](overview-emulator.md)

[Event Hubs emulator samples on GitHub](https://github.com/Azure/azure-event-hubs-emulator-installer/tree/main/Sample-Code-Snippets/dotnet/EventHubs-Emulator-Demo/EventHubs-Emulator-Demo)


# Apache Kafka Developer Guide

# Apache Kafka developer guide for Azure Event Hubs

This guide helps Kafka developers build and migrate applications to Azure Event Hubs. Whether you're connecting an existing Kafka application or building a new streaming solution, you'll find quickstarts, tutorials, and integration patterns organized by your development journey.

## Prerequisites

Before you start developing, ensure you have:

- An Azure Event Hubs namespace with Kafka enabled (Standard tier or higher)

- Your preferred Kafka client library installed

- Connection string or Microsoft Entra credentials for authentication

For an overview of how Event Hubs works with Kafka, see [Event Hubs for Apache Kafka](azure-event-hubs-apache-kafka-overview.md).

## Get started in 5 minutes

The fastest way to connect to Event Hubs is to modify your existing Kafka client configuration. No code changes required—just update your connection settings.

**Quick start**: [Data streaming with Event Hubs using the Kafka protocol](event-hubs-quickstart-kafka-enabled-event-hubs.md) walks you through connecting producers and consumers with just a configuration change.

### Language-specific quickstarts

Choose your language to get a working producer and consumer sample:

| Language | Sample | Client library |

|----------|--------|----------------|

| **Java** | [Quickstart](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/quickstart/java) | Apache Kafka client |

| **C# / .NET** | [Quickstart](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/quickstart/dotnet) | Confluent .NET client |

| **Python** | [Quickstart](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/quickstart/python) | Confluent Python client |

| **Node.js** | [Quickstart](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/quickstart/node) | node-rdkafka |

| **Go** | [Quickstart](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/quickstart/go) | Confluent Go client |

| **Go (Sarama)** | [Quickstart](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/quickstart/go-sarama-client) | Sarama client |

### Command-line tools

For testing and debugging, use these CLI tools:

| Tool | Sample | Use case |

|------|--------|----------|

| **Kafka CLI** | [Quickstart](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/quickstart/kafka-cli) | Bundled with Apache Kafka distribution |

| **kcat** | [Quickstart](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/quickstart/kafkacat) | Lightweight, fast CLI based on librdkafka |

## Build streaming pipelines

Once you've connected your application, you can build more sophisticated streaming pipelines. This section covers integrations with popular stream processing frameworks and data integration tools.

### Stream processing frameworks

Connect your stream processing applications to Event Hubs:

| Framework | Tutorial | Description |

|-----------|----------|-------------|

| **Apache Spark** | [Tutorial](event-hubs-kafka-spark-tutorial.md) | Real-time streaming with Spark Structured Streaming |

| **Apache Flink** | [Tutorial](event-hubs-kafka-flink-tutorial.md) | Stateful stream processing with exactly-once semantics |

| **Akka Streams** | [Tutorial](event-hubs-kafka-akka-streams-tutorial.md) | Reactive stream processing for Scala and Java |

| **Azure Stream Analytics** | [Tutorial](event-hubs-kafka-stream-analytics.md) | No-code stream processing with SQL-like queries |

| **Spring Cloud Stream** | [Tutorial](/azure/developer/java/spring-framework/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub) | Spring Boot integration using Kafka binder |

### Data integration with Kafka Connect

Kafka Connect enables you to stream data between Event Hubs and external systems using pre-built connectors:

| Resource | Description |

|----------|-------------|

| [Kafka Connect integration](event-hubs-kafka-connect-tutorial.md) | Deploy and configure Kafka Connect with Event Hubs |

| [Kafka Connect tutorial (GitHub)](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/connect) | End-to-end example with FileStreamSource and FileStreamSink |

### Log aggregation and observability

Centralize logs from your infrastructure into Event Hubs:

| Tool | Tutorial | Description |

|------|----------|-------------|

| **Logstash** | [Tutorial](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/logstash) | Elastic Stack log pipeline |

| **Filebeat** | [Tutorial](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/filebeat) | Lightweight log shipper |

| **FluentD** | [Tutorial](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/fluentd) | Unified logging layer |

| **Apache NiFi** | [Tutorial](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/nifi) | Visual dataflow management |

## Migrate existing Kafka workloads

If you're migrating from an existing Kafka cluster, Event Hubs supports replication and hybrid scenarios.

### Replicate data with MirrorMaker

Use Kafka MirrorMaker to replicate data from an existing Kafka cluster to Event Hubs:

| Resource | Description |

|----------|-------------|

| [Mirror a Kafka broker to Event Hubs](event-hubs-kafka-mirror-maker-tutorial.md) | Step-by-step guide for MirrorMaker setup |

| [MirrorMaker tutorial (GitHub)](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/mirror-maker) | Sample configurations and scripts |

### Migration planning

For a complete migration guide, including configuration mapping and feature differences, see [Apache Kafka migration guide for Event Hubs](apache-kafka-migration-guide.md).

## Advanced scenarios

### Schema management

Manage schemas for your Kafka applications:

| Resource | Description |

|----------|-------------|

| [Azure Schema Registry](schema-registry-overview.md) | Native schema registry built into Event Hubs |

| [Confluent Schema Registry integration](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/schema-registry) | Use Confluent Schema Registry with Event Hubs |

### Authentication with OAuth / Microsoft Entra ID

For production workloads, use Microsoft Entra ID instead of connection strings:

| Resource | Description |

|----------|-------------|

| [OAuth tutorial (GitHub)](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/oauth) | Java and Go samples for OAuth authentication |

### Protocol interoperability

Event Hubs supports multiple protocols. Learn how to exchange events between Kafka and AMQP clients:

| Resource | Description |

|----------|-------------|

| [Interop tutorial (GitHub)](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/interop) | Exchange events between different protocols |

## Configuration reference

For recommended Kafka client configurations when using Event Hubs, see [Apache Kafka client configurations](apache-kafka-configurations.md). This guide covers:

- Required connection settings

- Configurations that differ from Kafka defaults

- Event Hubs-specific constraints

- Troubleshooting common configuration issues

## Get help

- [Apache Kafka troubleshooting guide for Event Hubs](apache-kafka-troubleshooting-guide.md)

- [Frequently asked questions - Event Hubs for Apache Kafka](apache-kafka-frequently-asked-questions.yml)

- [GitHub samples repository](https://github.com/Azure/azure-event-hubs-for-kafka)


# Apache Kafka Migration Guide

# Migrate to Azure Event Hubs for Apache Kafka

This guide provides a clear path for migrating your Apache Kafka applications to Azure Event Hubs. Event Hubs exposes a Kafka-compatible endpoint, allowing you to connect existing Kafka clients with configuration changes only—no code modifications required.

## Before you migrate

### Verify feature compatibility

Event Hubs supports most Kafka client operations, but some features aren't available. Review this table to ensure your workload is compatible:

| Feature | Supported | Notes |

|---------|-----------|-------|

| Produce messages | ✅ Yes | Standard producer API |

| Consume messages | ✅ Yes | Standard consumer API |

| Consumer groups | ✅ Yes | Offset management supported |

| Compression (gzip) | ✅ Yes | Only gzip is supported |

| Schema Registry | ✅ Yes | Use [Azure Schema Registry](schema-registry-overview.md) |

| Kafka Connect | ✅ Yes | See [Kafka Connect integration](event-hubs-kafka-connect-tutorial.md) |

| Compression (snappy, lz4, zstd) | ✅ Yes | Use gzip or none |

| Kafka Transactions | ✅ Yes | Currently in Preview. |

For the complete list of supported operations, see [Event Hubs for Apache Kafka](azure-event-hubs-apache-kafka-overview.md).

### Assess your current Kafka setup

Before migrating, document your existing configuration:

| Item | What to note | Event Hubs equivalent |

|------|--------------|----------------------|

| **Number of topics** | Total topics in use | Event hubs (1:1 mapping) |

| **Partitions per topic** | Partition count | Partitions per event hub (can be increased after creation on Premium/Dedicated tiers, but can't be decreased) |

| **Retention period** | Current retention settings | 1-7 days (Standard), 1-90 days (Premium/Dedicated) |

| **Throughput** | Peak MB/sec | [Throughput units or processing units](event-hubs-scalability.md) |

| **Message size** | Maximum message size | 1 MB (Standard/Premium), 20 MB (Dedicated) |

| **Compression type** | snappy, lz4, gzip, etc. | Change to gzip or none if using other types |

### Choose your Event Hubs tier

Select a tier based on your requirements:

| Requirement | Recommended tier |

|-------------|------------------|

| Development/testing, low throughput | Standard |

| **Production Kafka workloads**, zone redundancy, full Kafka protocol support | **Premium** |

| High throughput, large messages (>1 MB), dedicated resources | Dedicated |

> [!IMPORTANT]

> For full Kafka protocol compatibility, use **Premium** or **Dedicated** tier. The Standard tier has limitations that may affect some Kafka workloads.

For detailed tier comparison, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/) and [quotas](event-hubs-quotas.md).

## Migration steps

### Step 1: Create Event Hubs resources

1. **Create a namespace**: Follow [Create an Event Hubs namespace](event-hubs-create.md)

2. **Create event hubs**: Create one event hub for each Kafka topic you're migrating

3. **Get connection string**: Follow [Get connection string](event-hubs-get-connection-string.md)

Note your namespace FQDN from the connection string:

```

Endpoint=sb://NAMESPACE.servicebus.windows.net/;SharedAccessKeyName=...

```

The FQDN is: `NAMESPACE.servicebus.windows.net`

### Step 2: Update client configuration

Update your Kafka client configuration to connect to Event Hubs. Locate where `bootstrap.servers` is defined in your application and apply these settings:

```properties

bootstrap.servers=NAMESPACE.servicebus.windows.net:9093

security.protocol=SASL_SSL

sasl.mechanism=PLAIN

sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="YOUR_CONNECTION_STRING";

```

Replace:

- `NAMESPACE` with your Event Hubs namespace name

- `YOUR_CONNECTION_STRING` with your full connection string

For framework-specific configuration and recommended settings, see [Apache Kafka client configurations](apache-kafka-configurations.md).

### Step 3: Migrate existing data (optional)

If you need to migrate historical data from your existing Kafka cluster to Event Hubs, use Kafka MirrorMaker:

- [Mirror a Kafka broker to Event Hubs](event-hubs-kafka-mirror-maker-tutorial.md)

For ongoing replication or hybrid scenarios, MirrorMaker can run continuously to keep both systems synchronized during a phased migration.

### Step 4: Update consumer offsets

When consumers connect to Event Hubs for the first time, they won't have existing offsets. Configure `auto.offset.reset` based on your needs:

| Setting | Behavior |

|---------|----------|

| `earliest` | Start reading from the beginning of available data |

| `latest` | Start reading only new messages |

## Validate the migration

### Verify producer connectivity

1. Start your producer application with the updated configuration

2. Send test messages to Event Hubs

3. Confirm messages arrive in the Azure portal:

- Navigate to your Event Hubs namespace

- Select **Overview** > **Metrics** > **Messages**

### Verify consumer connectivity

1. Start your consumer application with the updated configuration

2. Confirm messages are being received

3. Monitor consumer lag using Azure Monitor or your application metrics

### Performance validation

Compare performance against your baseline:

| Metric | How to verify |

|--------|---------------|

| Throughput (MB/sec) | Monitor incoming/outgoing bytes in Azure portal |

| Latency | Measure end-to-end message delivery time in your application |

| Consumer lag | Check consumer group lag in Azure portal or via Kafka consumer metrics |

For performance optimization, see [Apache Kafka client configurations](apache-kafka-configurations.md).

## Decommission Kafka cluster

After successful validation:

1. **Monitor in parallel**: Run both systems for a stabilization period

2. **Redirect all traffic**: Update all producers and consumers to use Event Hubs

3. **Verify no traffic**: Confirm the Kafka cluster has no active connections

4. **Decommission**: Shut down and remove Kafka infrastructure

## Troubleshooting

If you encounter issues during migration:

| Issue | Resource |

|-------|----------|

| Connection or authentication errors | [Apache Kafka troubleshooting guide](apache-kafka-troubleshooting-guide.md) |

| Configuration problems | [Apache Kafka client configurations](apache-kafka-configurations.md) |

| General questions | [Frequently asked questions](apache-kafka-frequently-asked-questions.yml) |

## Related content

- [Event Hubs for Apache Kafka overview](azure-event-hubs-apache-kafka-overview.md)

- [Apache Kafka developer guide](apache-kafka-developer-guide.md)

- [Quickstart: Stream data using Kafka protocol](event-hubs-quickstart-kafka-enabled-event-hubs.md)

- [Event Hubs quotas and limits](event-hubs-quotas.md)


# Apache Kafka Troubleshooting Guide

# Apache Kafka troubleshooting guide for Event Hubs

This article provides troubleshooting tips for issues that you might run into when using Event Hubs for Apache Kafka.

## Server Busy exception

You might see ThrottledRequests metrics because of Kafka throttling. With AMQP clients, Event Hubs immediately returns a **server busy** exception upon service throttling. It's equivalent to a "try again later" message. In Kafka, incoming messages are delay before being acknowledged while outgoing message will see delayed delivery. The delay length is returned in milliseconds as `throttle_time_ms` in the produce/fetch response. In most cases, these delayed requests aren't logged as ThrottledRequests metrics on Event Hubs dashboards. Instead, the response's `throttle_time_ms` value should be used as an indicator that throughput has exceeded the provisioned quota.

If the traffic is excessive, the service has the following behavior:

- If produce request's delay exceeds request time-out(*request.timeout.ms*), Event Hubs returns **Policy Violation** error code.

- If fetch request's delay exceeds request time out, Event Hubs logs the request as throttled and responds with empty set of records and no error code.

## No records received

You might see consumers not getting any records and constantly rebalancing. In this scenario, consumers don't get any records and constantly rebalance. There's no exception or error when it happens, but the Kafka logs will show that the consumers are stuck trying to rejoin the group and assign partitions. There are a few possible causes:

- Make sure that your `request.timeout.ms` is at least the recommended value of 60000 and your `session.timeout.ms` is at least the recommended value of 30000. Having these settings too low could cause consumer time-outs, which then cause rebalances (which then cause more time-outs, which cause more rebalancing, and so on)

- If your configuration matches those recommended values, and you're still seeing constant rebalancing, feel free to open up an issue (make sure to include your entire configuration in the issue so that we can help debug).

## Compression/Message format version issue

Event Hubs for Kafka currently support only `gzip` compression algorithm. If any other algorithm is used, client applications see a message-format version  error (for example, `The message format version on the broker does not support the request.`).

If an unsupported compression algorithm needs to be used, compressing your data with that specific algorithm before sending it to the brokers and decompressing after receiving is a valid workaround. The message body is just a byte array to the service, so client-side compression/decompression won't cause any issues.

## UnknownServerException

You might receive an UnknownServerException from Kafka client libraries similar to the following example:

```

org.apache.kafka.common.errors.UnknownServerException: The server experienced an unexpected error when processing the request

```

Open a ticket with Microsoft support. Debug-level logging and exception timestamps in UTC are helpful in debugging the issue.

## Other issues

Check the following items if you see issues when using Kafka on Event Hubs.

- **Firewall blocking traffic** - Make sure that port **9093** isn't blocked by your firewall.

- **TopicAuthorizationException** - The most common causes of this exception are:

- A typo in the connection string in your configuration file, or

- Trying to use Event Hubs for Kafka on a Basic tier namespace. The Event Hubs for Kafka feature isn't supported in the basic tier.

- **Kafka version mismatch** - Event Hubs for Kafka Ecosystems supports Kafka versions 1.0 and later. Some applications using Kafka version 0.10 and later could occasionally work because of the Kafka protocol's backwards compatibility, but we strongly recommend against using old API versions. Kafka versions 0.9 and earlier don't support the required SASL protocols and can't connect to Event Hubs.

- **Strange encodings on AMQP headers when consuming with Kafka** - when sending events to an event hub over AMQP, any AMQP payload headers are serialized in AMQP encoding. Kafka consumers don't deserialize the headers from AMQP. To read header values, manually decode the AMQP headers. Alternatively, you can avoid using AMQP headers if you know that you are consuming via Kafka protocol. For more information, see [this GitHub issue](https://github.com/Azure/azure-event-hubs-for-kafka/issues/56).

- **SASL authentication** - Getting your framework to cooperate with the SASL authentication protocol required by Event Hubs can be more difficult than meets the eye. See if you can troubleshoot the configuration using your framework's resources on SASL authentication.

## Limits

Apache Kafka vs. Event Hubs Kafka. For the most part, Azure Event Hubs' Kafka interface has the same defaults, properties, error codes, and general behavior that Apache Kafka does. The instances that these two explicitly differ (or where Event Hubs imposes a limit that Kafka doesn't) are listed here:

- The max length of the `group.id` property is 256 characters

- The max size of `offset.metadata.max.bytes` is 1,024 bytes

- Offset commits are throttled to 2 calls/second per partition with a maximum internal log size of 1 MB

## Next steps

To learn more about Event Hubs and Event Hubs for Kafka, see the following articles:

- [Apache Kafka developer guide for Event Hubs](apache-kafka-developer-guide.md)

- [Apache Kafka migration guide for Event Hubs](apache-kafka-migration-guide.md)

- [Frequently asked questions - Event Hubs for Apache Kafka](apache-kafka-frequently-asked-questions.yml)

- [Recommended configurations](apache-kafka-configurations.md)


# Apache Kafka Transactions

# Transactions in Apache Kafka for Azure Event Hubs

This article provides detail on how to use the [Apache Kafka](https://kafka.apache.org/) transactional API with Azure Event Hubs.

## Overview

Event Hubs provides a Kafka endpoint that can be used by your existing Kafka client applications as an alternative to running your own Kafka cluster. Event Hubs works with many of your existing Kafka applications. For more information, see [Event Hubs for Apache Kafka](azure-event-hubs-apache-kafka-overview.md).

This document focuses on how to use Kafka’s transactional API with Azure Event Hubs seamlessly.

> [!NOTE]

> Kafka Transactions is currently in Public preview in Premium, and Dedicated tier.

>

## Transactions in Apache Kafka

In cloud native environments, applications must be made resilient to network disruptions and namespace restarts and upgrades. Applications requiring strict processing guarantees must utilize a transactional framework or API to ensure that either all of the operations are executed, or none are so that the application and data state is reliably managed. If the set of operations fail, they can be reliably tried again atomically to ensure the right processing guarantees.

> [!NOTE]

> Transactional guarantees are typically required when there are multiple operations that need to be processed in an "all or nothing" fashion.

>

> For all other operations, client applications are **resilient by default** to retry the operation with an exponential backoff, if the specific operation failed.

Apache Kafka provides a transactional API to ensure this level of processing guarantees across the same or different set of topic/partitions.

Transactions apply to the following cases:

* Transactional producers.

* Exactly once processing semantics.

### Transactional Producers

Transactional producers ensure that data is written atomically to multiple partitions across different topics. Producers can initiate a transaction, write to multiple partitions on the same topic or across different topics, and then commit or abort the transaction.

To ensure that a producer is transactional, `enable.idempotence` should be set to true to ensure that the data is written exactly once, thus avoiding duplicates on the *send* side. Additionally, `transaction.id` should be set to uniquely identify the producer.

```java

producerProps.put("enable.idempotence", "true");

producerProps.put("transactional.id", "transactional-producer-1");

KafkaProducer<String, String> producer = new KafkaProducer(producerProps);

```

Once the producer is initialized, the following call ensures that the producer registers with the broker as a transactional producer -

```java

producer.initTransactions();

```

The producer must then begin a transaction explicitly, perform send operations across different topics and partitions as normal, and then commit the transaction with the following call –

```java

producer.beginTransaction();

/*

Send to multiple topic partitions.

*/

producer.commitTransaction();

```

If the transaction needs to be aborted due to a fault or a time out, then the producer can call the `abortTransaction()` method.

```java

producer.abortTransaction();

```

### Exactly once semantics

Exactly once semantics builds on the transactional producers by adding consumers in the transactional scope of the producers, so that each record is guaranteed to be read, processed, and written **exactly once**.

First the transactional producer is instantiated -

```java

producerProps.put("enable.idempotence", "true");

producerProps.put("transactional.id", "transactional-producer-1");

KafkaProducer<K, V> producer = new KafkaProducer(producerProps);

producer.initTransactions();

```

Then, the consumer must be configured to read only nontransactional messages, or committed transactional messages by setting the following property –

```java

consumerProps.put("isolation.level", "read_committed");

KafkaConsumer <K,V> consumer = new KafkaConsumer<>(consumerProps);

```

Once the consumer is instantiated, it can subscribe to the topic from where the records must be read –

```java

consumer.subscribe(singleton("inputTopic"));

```

After the consumer polls the records from the input topic, the producer begins the transactional scope within which the record is processed and written to the output topic. Once the records are written, the updated map of offsets for all partitions is created. The producer then sends this updated offset map to the transaction before committing the transaction.

In any exception, the transaction is aborted and the producer retries the processing once again atomically.

```java

while (true) {

ConsumerRecords records = consumer.poll(Long.Max_VALUE);

producer.beginTransaction();

try {

for (ConsumerRecord record : records) {

/*

Process record as appropriate

*/

// Write to output topic

producer.send(producerRecord(“outputTopic”, record));

}

/*

Generate the offset map to be committed.

*/

Map <TopicPartition, OffsetAndMetadata> offsetsToCommit = new Hashap<>();

for (TopicPartition partition : records.partitions()) {

// Calculate the offset to commit and populate the map.

offsetsToCommit.put(partition, new OffsetAndMetadata(calculated_offset))

}

// send offsets to transaction and then commit the transaction.

producer.sendOffsetsToTransaction(offsetsToCommit, group);

producer.commitTransaction();

} catch (Exception e)

{

producer.abortTransaction();

}

}

```

> [!WARNING]

>If the transaction is not committed or aborted before the `max.transaction.timeout.ms`, the transaction is aborted by Event Hubs automatically. The default `max.transaction.timeout.ms` is set to **15 minutes** by Event Hubs, but the producer can override it to a lower value by setting the `transaction.timeout.ms` property in the producer configuration properties.

## Migration Guide

If you have existing Kafka applications that you’d like to use with Azure Event Hubs, see the [Kafka migration guide for Azure Event Hubs](apache-kafka-migration-guide.md) to hit the ground running quickly.

## Next steps

To learn more about Event Hubs and Event Hubs for Kafka, see the following articles:

- [Apache Kafka troubleshooting guide for Event Hubs](apache-kafka-troubleshooting-guide.md)

- [Frequently asked questions - Event Hubs for Apache Kafka](apache-kafka-frequently-asked-questions.yml)

- [Apache Kafka developer guide for Azure Event Hubs](apache-kafka-developer-guide.md)

- [Recommended configurations](apache-kafka-configurations.md)


# Apache Kafka Streams

# Kafka Streams for Azure Event Hubs

This article provides details on how to use the [Kafka Streams](https://kafka.apache.org/documentation/streams/) client library with Azure Event Hubs.

> [!NOTE]

> Kafka Streams functionality is available in **Public Preview** for Event Hubs Premium and Dedicated tiers only.

>

## Overview

Apache Kafka Streams is a Java only client library that provides a framework for processing of streaming data and building real-time applications against the data stored in Kafka topics. All the processing is scoped to the client, while Kafka topics act as the data store for intermediate data, before the output is written to the destination topic.

Event Hubs provides a Kafka endpoint to be used with your existing Kafka client applications as an alternative to running your own Kafka cluster. Event Hubs works with many of your existing Kafka applications. For more information, see [Event Hubs for Apache Kafka](azure-event-hubs-apache-kafka-overview.md).

## Using Kafka Streams with Azure Event Hubs

Azure Event Hubs natively supports both the AMQP and Kafka protocol. However, to ensure compatible Kafka Streams behavior, some of the default configuration parameters have to be updated for Kafka clients.

| Property | Default behavior for Event Hubs | Modified behavior for Kafka streams | Explanation |

| ----- | ---- | ----| ---- |

| `messageTimestampType` | set to `AppendTime` | should be set to `CreateTime` | Kafka Streams relies on creation timestamp rather than append timestamp |

| `message.timestamp.difference.max.ms` | max allowed value is 90 days | Property is used to govern past timestamps only. Future time is set to 1 hour and can't be changed. | It is in line with the Kafka protocol specification |

| `min.compaction.lag.ms` | | max allowed value is two days ||

| Infinite retention topics | | size based truncation of 250 GB for each topic-partition||

| Delete record API for infinite retention topics| | Not implemented. As a workaround, the topic can be updated and a finite retention time can be set.| This functionality will be supported in GA |

### Other considerations

Here are some of the other considerations to keep in mind.

* Kafka streams client applications must be granted management, read, and write permissions for the entire namespaces to be able to create temporary topics for stream processing.

* Temporary topics and partitions count towards the quota for the given namespace. They should be kept under consideration when provisioning the namespace or cluster.

* Infinite retention time for "Offset" Store is limited by max message retention time of the Stock Keeping Unit (SKU). Check [Event Hubs Quotas](event-hubs-quotas.md) for these tier specific values.

They include, updating the topic configuration in the `messageTimestampType` to use the `CreateTime` (that is, Event creation time) instead of the `AppendTime` (that is, log append time).

To override the default behavior (required), the below setting must be set in Azure Resource Manager (ARM).

> [!NOTE]

> Only the specific parts of the ARM template are shown to highlight the configuration that needs to be updated.

>

```json

{

"parameters": {

"namespaceName": "contoso-test-namespace",

"resourceGroupName": "contoso-resource-group",

"eventHubName": "contoso-event-hub-kafka-streams-test",

...

"parameters": {

"properties": {

...

"messageTimestampType": "CreateTime",

"retentionDescription": {

"cleanupPolicy": "Delete",

"retentionTimeInHours": -1,

"tombstoneRetentionTimeInHours": 1

}

}

}

}

}

```

## Kafka Streams concepts

Kafka streams provide a simple abstraction layer over the Kafka producer and consumer APIs to help developers get started with real time streaming scenarios faster. The light-weight library depends on an **Apache Kafka compatible broker** (like Azure Event Hubs) for the internal messaging layer, and manages a **fault tolerant local state store**. With the transactional API, the Kafka streams library supports rich processing features such as **exactly once processing** and **one record at a time processing**.

Records arriving out of order benefit from **event-time based windowing operations**.

> [!NOTE]

> We recommend familiarizing yourself with [Kafka Streams documentation](https://kafka.apache.org/37/documentation/streams/) and [Kafka Streams core concepts](https://kafka.apache.org/37/documentation/streams/core-concepts).

>

### Streams

A stream is the abstracted representation of a Kafka topic. It consists of an unbounded, continuously updating data set of immutable data records, where each data record is a key-value pair.

### Stream processing topology

A Kafka streams application defines the computational logic through a [DAG (directed acyclic graph)](https://en.wikipedia.org/wiki/Directed_acyclic_graph) represented by a processor [topology](https://javadoc.io/doc/org.apache.kafka/kafka-streams/latest/org/apache/kafka/streams/Topology.html). The processor topology comprises stream processors(nodes in the topology) which represent a processing step, connected by streams(edges in the topology).

Stream processors can be chained to upstream processors or downstream processors, except for certain special cases:

* Source processors - These processors don't have any upstream processors and read from one or more streams directly. They can then be chained to downstream processors.

* Sink processors - These processors don't have any downstream processors and must write directly to a stream.

Stream processing topology can be defined either with the [Kafka Streams DSL](https://kafka.apache.org/37/streams/developer-guide/dsl-api/) or with the lower-level [Processor API](https://kafka.apache.org/37/streams/developer-guide/processor-api/).

### Stream and Table duality

Streams and tables are 2 different but useful abstractions provided by the [Kafka Streams DSL](https://kafka.apache.org/37/streams/developer-guide/dsl-api/), modeling both time series and relational data formats that must coexist for stream processing use-cases.

Kafka extends it further and introduces a duality between streams and tables, where a

* A **stream** can be considered as a changelog of a **table**, and

* A **table** can be considered as a snapshot of the latest value of each key in a **stream**.

This duality allows tables and streams to be used interchangeably as required by the use-case.

For example

* Joining static customer data (modeled as a table) with dynamic transactions (modeled as a stream), and

* Joining changing portfolio positions in a day traders portfolio (modeled as a stream) with the latest market data feed(modeled as a stream).

### Time

Kafka Streams allows windowing and grace functions to allow for out of order data records to be ingested and still be included in the processing. To ensure that this behavior is deterministic, there are more notions of time in Kafka streams. They include:

* Creation time (also known as 'Event time') - It's the time when the event occurred and the data record was created.

* Processing time - It's the time when the data record is processed by the stream processing application (or when it's consumed).

* Append time (also known as 'Creation time') - It's the time when the data is stored and committed to the storage of the Kafka broker. It differs from the creation time because of the time difference between the creation of the event and the actual ingestion by the broker.

### Stateful operations

State management enables sophisticated stream processing applications like joining and aggregating data from different streams. This is achieved with state stores provided by Kafka Streams and accessed using [stateful operators in the Kafka Streams DSL](https://kafka.apache.org/37/streams/developer-guide/dsl-api/#stateful-transformations).

Stateful transformations in the DSL include:

* [Aggregating](https://kafka.apache.org/37/streams/developer-guide/dsl-api/#aggregating)

* [Joining](https://kafka.apache.org/37/streams/developer-guide/dsl-api/#joining)

* [Windowing (as part of aggregations and joins)](https://kafka.apache.org/37/streams/developer-guide/dsl-api/#windowing)

* [Applying custom processors and transformers](https://kafka.apache.org/37/streams/developer-guide/dsl-api/#applying-processors-and-transformers-processor-api-integration), which can be stateful, for Processor API integration

### Window and grace

Windowing operations in the  [Kafka Streams DSL](https://kafka.apache.org/37/streams/developer-guide/dsl-api/) allow developers to control how records are grouped for a given key for [stateful operations like aggregations and joins](#stateful-operations).

Windowing operations also permit the specification of a **grace period** to provide some flexibility for out-of-order records for a given window. A record that is meant for a given window and arrives after the given window but within the grace period is accepted. Records arriving after the grace period is over are discarded.

Applications must utilize the windowing and grace period controls to improve fault tolerance for out-of-order records. The appropriate values vary based on the workload and must be identified empirically.

### Processing guarantees

Business and technical users seek to extract key business insights from the output of stream processing workloads, which translate to high transactional guarantee requirements. Kafka streams work together with Kafka transactions to ensure transactional processing guarantees by integrating with the Kafka compatible brokers' (such as Azure Event Hubs) underlying storage system to ensure that offset commits and state store updates are written atomically.

To ensure transactional processing guarantees, the `processing.guarantee` setting in the Kafka Streams configs must be updated from the default value of `at_least_once` to `exactly_once_v2` (for client versions at or after Apache Kafka 2.5) or `exactly_once` (for client versions before Apache Kafka 2.5.x).

## Next steps

This article provided an introduction to Event Hubs for Kafka. To learn more, see [Apache Kafka developer guide for Azure Event Hubs](apache-kafka-developer-guide.md).

For a **tutorial** with step-by-step instructions to create an event hub and access it using SAS or OAuth, see [Quickstart: Data streaming with Event Hubs using the Kafka protocol](event-hubs-quickstart-kafka-enabled-event-hubs.md).

Also, see the [OAuth samples on GitHub](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/oauth).


# Event Hubs Kafka Mirrormaker 2 Tutorial

# Replicate data from a Kafka cluster to Event Hubs using Apache Kafka Mirror Maker 2

This tutorial shows how to replicate data from an existing Kafka cluster to Azure Event Hubs using Mirror Maker 2.

![Image showing the flow of events from Kafka MirrorMaker to Event Hubs.](./media/event-hubs-kafka-mirror-maker-tutorial/mirrormaker-2-kafka-to-event-hubs.png)

> [!NOTE]

> This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/mirror-maker-2)

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create an Event Hubs namespace

> * Set up or use an existing Kafka cluster

> * Configure Kafka Mirror Maker 2

> * Run Kafka Mirror Maker 2

## Introduction

Apache Kafka MirrorMaker 2.0 (MM2) is designed to make it easier to mirror or replicate topics from one Kafka cluster to another. Mirror Maker uses the Kafka Connect framework to simplify configuration and scaling. For more detailed information on Kafka MirrorMaker, see the [Kafka Mirroring/MirrorMaker guide](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330).

As Azure Event Hubs is compatible with Apache Kafka protocol, you can use Mirror Maker 2 to replicate data between an existing Kafka cluster and an Event Hubs namespace.

Mirror Maker 2 dynamically detects changes to topics and ensures source and target topic properties are synchronized, including offsets and partitions. It can be used to replicated data bi-directionally between Kafka cluster and Event Hubs namespace.

## Prerequisites

To complete this tutorial, make sure you have:

* Read through the [Event Hubs for Apache Kafka](azure-event-hubs-apache-kafka-overview.md) article.

* An Azure subscription. If you don't have one, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

* [Java Development Kit (JDK) 1.7+](/azure/developer/java/fundamentals/java-support-on-azure)

* On Ubuntu, run `apt-get install default-jdk` to install the JDK.

* Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.

* [Download](https://maven.apache.org/download.cgi) and [install](https://maven.apache.org/install.html) a Maven binary archive

* On Ubuntu, you can run `apt-get install maven` to install Maven.

* [Git](https://www.git-scm.com/downloads)

* On Ubuntu, you can run `sudo apt-get install git` to install Git.

* [Apache Kafka distribution](https://kafka.apache.org/downloads)

* Download the preferred Apache Kafka distribution (which should contain the Mirror Maker 2 distribution.)

## Create an Event Hubs namespace

An Event Hubs namespace is required to send and receive from any Event Hubs service. See [Creating an event hub](event-hubs-create.md) for instructions to create a namespace and an event hub. Make sure to copy the Event Hubs connection string for later use.

## Clone the example project

Now that you have an Event Hubs connection string, clone the Azure Event Hubs for Kafka repository and navigate to the `mirror-maker-2` subfolder:

```shell

git clone https://github.com/Azure/azure-event-hubs-for-kafka.git

cd azure-event-hubs-for-kafka/tutorials/mirror-maker-2

```

## Set up or use an existing Kafka cluster

If you don't have an existing Kafka cluster, use the [Kafka quickstart guide](https://kafka.apache.org/quickstart) to set up a Kafka cluster with the desired settings (or use an existing Kafka cluster). For testing purposes, you can also create a couple of topics in the newly created Kafka cluster and publish data to them.

If you already have an existing Kafka cluster on-premises or in a managed Kafka cloud service, then you can use it to replicate existing data to Event Hubs.

## Configure Kafka Mirror Maker 2

Apache Kafka distribution comes with `connect-mirror-maker.sh` script that is bundled with the Kafka library that implements a distributed Mirror Maker 2 cluster. It manages the Connect workers internally based on a configuration file. Internally MirrorMaker driver creates and handles pairs of each connector – *MirrorSource Connector*, *MirrorSink Connector*, *MirrorCheckpoint Connector*, and *MirrorHeartbeat Connector*.

1. To configure Mirror Maker 2 to replicate data, you need to update Mirror Maker 2 configuration file `kafka-to-eh-connect-mirror-maker.properties` to define the replication topology.

1. In the `kafka-to-eh-connect-mirror-maker.properties` config file, define cluster aliases that you plan to use for your Kafka cluster(source) and Event Hubs (destination).

```config

# cluster aliases

clusters = source, destination

```

1. Then specify the connection information for your source, which is your Kafka cluster.

```config

source.bootstrap.servers = your-kafka-cluster-hostname:9092

#source.security.protocol=SASL_SSL

#source.sasl.mechanism=PLAIN

#source.sasl.jaas.config=<replace sasl jaas config of your Kafka cluster>;

```

1. Specify connection information for destination, which is the Event Hubs namespace that you created.

```config

destination.bootstrap.servers = <your-enventhubs-namespace>.servicebus.windows.net:9093

destination.security.protocol=SASL_SSL

destination.sasl.mechanism=PLAIN

destination.sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username='$ConnectionString' password='<Your Event Hubs namespace connection string.>';

```

1. Enable replication flow from source Kafka cluster to destination Event Hubs namespace.

```config

source->destination.enabled = true

source->destination.topics = .*

```

1. Update the replication factor of the remote topics and internal topics that Mirror Maker creates at the destination.

```config

replication.factor=3

checkpoints.topic.replication.factor=3

heartbeats.topic.replication.factor=3

offset-syncs.topic.replication.factor=3

offset.storage.replication.factor=3

status.storage.replication.factor=3

config.storage.replication.factor=3

```

1. Then you copy `kafka-to-eh-connect-mirror-maker.properties` configuration file to the Kafka distribution's config directory and can run the Mirror Maker 2 script using the following command.

```bash

./bin/connect-mirror-maker.sh ./config/kafka-to-eh-connect-mirror-maker.properties

```

1. Upon the successful execution of the script, you should see the Kafka topics and events getting replicated to your Event Hubs namespace.

1. To verify that events are making it to the Kafka-enabled Event Hubs, check out the ingress statistics in the [Azure portal](https://azure.microsoft.com/features/azure-portal/), or run a consumer against the Event Hubs.

## Samples

See the following samples on GitHub:

- [Sample code for this tutorial on GitHub](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/mirror-maker-2)

- If you're hosting Apache Kafka on Kubernetes using the CNCF Strimzi operator, you can use [Strimzi Mirror Maker 2 sample for Event Hubs](https://strimzi.io/blog/2020/06/09/mirror-maker-2-eventhub).

## Next steps

To learn more about Event Hubs for Kafka, see the following articles:

- [Explore samples on our GitHub](https://github.com/Azure/azure-event-hubs-for-kafka)


# Event Hubs Kafka Mirror Maker Tutorial

# Replicate data from a Kafka cluster to Event Hubs using Apache Kafka Mirror Maker 1

This tutorial shows how to mirror a Kafka broker into an Azure Event Hubs using Kafka Mirror Maker 1.

![Kafka MirrorMaker with Event Hubs](./media/event-hubs-kafka-mirror-maker-tutorial/evnent-hubs-mirror-maker1.png)

> [!NOTE]

> This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/mirror-maker)

> [!NOTE]

> This article contains references to a term that Microsoft no longer uses. When the term is removed from the software, we'll remove it from this article.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create an Event Hubs namespace

> * Clone the example project

> * Set up a Kafka cluster

> * Configure Kafka MirrorMaker

> * Run Kafka MirrorMaker

## Introduction

This tutorial shows how an event hub and Kafka MirrorMaker can integrate an existing Kafka pipeline into Azure by "mirroring" the Kafka input stream in the Event Hubs service, which allows for

integration of Apache Kafka streams using several [federation patterns](event-hubs-federation-overview.md).

An Azure Event Hubs Kafka endpoint enables you to connect to Azure Event Hubs using the Kafka protocol (that is, Kafka clients). By making minimal changes to a Kafka application, you can connect to Azure Event Hubs and enjoy the benefits of the Azure ecosystem. Event Hubs currently supports the protocol of Apache Kafka versions 1.0 and later.

You can use Apache Kafka's MirrorMaker 1 unidirectionally from Apache Kafka to Event Hubs. MirrorMaker 2 can be used in both directions, but the [`MirrorCheckpointConnector` and `MirrorHeartbeatConnector` that are configurable in MirrorMaker 2](https://cwiki.apache.org/confluence/display/KAFKA/KIP-382%3A+MirrorMaker+2.0) must both be configured to point to the Apache Kafka broker and not to Event Hubs. This tutorial shows configuring MirrorMaker 1.

## Prerequisites

To complete this tutorial, make sure you have:

* Read through the [Event Hubs for Apache Kafka](azure-event-hubs-apache-kafka-overview.md) article.

* An Azure subscription. If you don't have one, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

* [Java Development Kit (JDK) 1.7+](/azure/developer/java/fundamentals/java-support-on-azure)

* On Ubuntu, run `apt-get install default-jdk` to install the JDK.

* Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.

* [Download](https://maven.apache.org/download.cgi) and [install](https://maven.apache.org/install.html) a Maven binary archive

* On Ubuntu, you can run `apt-get install maven` to install Maven.

* [Git](https://www.git-scm.com/downloads)

* On Ubuntu, you can run `sudo apt-get install git` to install Git.

## Create an Event Hubs namespace

An Event Hubs namespace is required to send and receive from any Event Hubs service. See [Creating an event hub](event-hubs-create.md) for instructions to create a namespace and an event hub. Make sure to copy the Event Hubs connection string for later use.

## Clone the example project

Now that you have an Event Hubs connection string, clone the Azure Event Hubs for Kafka repository and navigate to the `mirror-maker` subfolder:

```shell

git clone https://github.com/Azure/azure-event-hubs-for-kafka.git

cd azure-event-hubs-for-kafka/tutorials/mirror-maker

```

## Set up a Kafka cluster

Use the [Kafka quickstart guide](https://kafka.apache.org/quickstart) to set up a cluster with the desired settings (or use an existing Kafka cluster).

## Configure Kafka MirrorMaker

Kafka MirrorMaker enables the "mirroring" of a stream. Given source and destination Kafka clusters, MirrorMaker ensures any messages sent to the source cluster are received by both the source and destination clusters. This example shows how to mirror a source Kafka cluster with a destination event hub. This scenario can be used to send data from an existing Kafka pipeline to Event Hubs without interrupting the flow of data.

For more detailed information on Kafka MirrorMaker, see the [Kafka Mirroring/MirrorMaker guide](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330).

To configure Kafka MirrorMaker, give it a Kafka cluster as its consumer/source and an event hub as its producer/destination.

#### Consumer configuration

Update the consumer configuration file `source-kafka.config`, which tells MirrorMaker the properties of the source Kafka cluster.

##### source-kafka.config

```

bootstrap.servers={SOURCE.KAFKA.IP.ADDRESS1}:{SOURCE.KAFKA.PORT1},{SOURCE.KAFKA.IP.ADDRESS2}:{SOURCE.KAFKA.PORT2},etc

group.id=example-mirrormaker-group

exclude.internal.topics=true

client.id=mirror_maker_consumer

```

#### Producer configuration

Now update the producer configuration file `mirror-eventhub.config`, which tells MirrorMaker to send the duplicated (or "mirrored") data to the Event Hubs service. Specifically, change `bootstrap.servers` and `sasl.jaas.config` to point to your Event Hubs Kafka endpoint. The Event Hubs service requires secure (SASL) communication, which is achieved by setting the last three properties in the following configuration:

##### mirror-eventhub.config

```

bootstrap.servers={YOUR.EVENTHUBS.FQDN}:9093

client.id=mirror_maker_producer

#Required for Event Hubs

sasl.mechanism=PLAIN

security.protocol=SASL_SSL

sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";

```

> [!IMPORTANT]

> Replace `{YOUR.EVENTHUBS.CONNECTION.STRING}` with the connection string for your Event Hubs namespace. For instructions on getting the connection string, see [Get an Event Hubs connection string](event-hubs-get-connection-string.md). Here's an example configuration: `sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="Endpoint=sb://mynamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=XXXXXXXXXXXXXXXX";`

## Run Kafka MirrorMaker

Run the Kafka MirrorMaker script from the root Kafka directory using the newly updated configuration files. Make sure to either copy the config files to the root Kafka directory, or update their paths in the following command.

```shell

bin/kafka-mirror-maker.sh --consumer.config source-kafka.config --num.streams 1 --producer.config mirror-eventhub.config --whitelist=".*"

```

To verify that events are reaching the event hub, see the ingress statistics in the [Azure portal](https://azure.microsoft.com/features/azure-portal/), or run a consumer against the event hub.

With MirrorMaker running, any events sent to the source Kafka cluster are received by both the Kafka cluster and the mirrored event hub. By using MirrorMaker and an Event Hubs Kafka endpoint, you can migrate an existing Kafka pipeline to the managed Azure Event Hubs service without changing the existing cluster or interrupting any ongoing data flow.

## Samples

See the following samples on GitHub:

- [Sample code for this tutorial on GitHub](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/mirror-maker)

- [Azure Event Hubs Kafka MirrorMaker running on an Azure Container Instance](https://github.com/djrosanova/EventHubsMirrorMaker)

## Next steps

To learn more about Event Hubs for Kafka, see the following articles:

- [Connect Apache Spark to an event hub](event-hubs-kafka-spark-tutorial.md)

- [Connect Apache Flink to an event hub](event-hubs-kafka-flink-tutorial.md)

- [Integrate Kafka Connect with an event hub](event-hubs-kafka-connect-tutorial.md)

- [Explore samples on our GitHub](https://github.com/Azure/azure-event-hubs-for-kafka)

- [Connect Akka Streams to an event hub](event-hubs-kafka-akka-streams-tutorial.md)

- [Apache Kafka developer guide for Azure Event Hubs](apache-kafka-developer-guide.md)


# Event Hubs Kafka Connect Tutorial

# Integrate Apache Kafka Connect support on Azure Event Hubs

[Apache Kafka Connect](https://kafka.apache.org/documentation/#connect) is a framework to connect and import/export data from/to any external system such as MySQL, HDFS, and file system through a Kafka cluster. This article walks you through using Kafka Connect framework with Event Hubs.

This article walks you through integrating Kafka Connect with an event hub and deploying basic `FileStreamSource` and `FileStreamSink` connectors. While these connectors aren't meant for production use, they demonstrate an end-to-end Kafka Connect scenario where Azure Event Hubs acts as a Kafka broker.

> [!NOTE]

> This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/connect).

## Prerequisites

To complete this walkthrough, make sure you have the following prerequisites:

- Azure subscription. If you don't have one, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- [Git](https://www.git-scm.com/downloads)

- Linux/macOS

- Latest Kafka release available from [kafka.apache.org](https://kafka.apache.org/downloads)

- Read through the [Event Hubs for Apache Kafka](./azure-event-hubs-apache-kafka-overview.md) introduction article

## Create an Event Hubs namespace

An Event Hubs namespace is required to send and receive from any Event Hubs service. See [Creating an event hub](event-hubs-create.md) for instructions to create a namespace and an event hub. Get the Event Hubs connection string and fully qualified domain name (FQDN) for later use. For instructions, see [Get an Event Hubs connection string](event-hubs-get-connection-string.md).

## Clone the example project

Clone the Azure Event Hubs repository and navigate to the tutorials/connect subfolder:

```bash

git clone https://github.com/Azure/azure-event-hubs-for-kafka.git

cd azure-event-hubs-for-kafka/tutorials/connect

```

## Configure Kafka Connect for Event Hubs

Minimal reconfiguration is necessary when redirecting Kafka Connect throughput from Kafka to Event Hubs. The following `connect-distributed.properties` sample illustrates how to configure Connect to authenticate and communicate with the Kafka endpoint on Event Hubs:

```properties

# e.g. namespace.servicebus.windows.net:9093

bootstrap.servers={YOUR.EVENTHUBS.FQDN}:9093

group.id=connect-cluster-group

# connect internal topic names, auto-created if not exists

config.storage.topic=connect-cluster-configs

offset.storage.topic=connect-cluster-offsets

status.storage.topic=connect-cluster-status

# internal topic replication factors - auto 3x replication in Azure Storage

config.storage.replication.factor=1

offset.storage.replication.factor=1

status.storage.replication.factor=1

rest.advertised.host.name=connect

offset.flush.interval.ms=10000

key.converter=org.apache.kafka.connect.json.JsonConverter

value.converter=org.apache.kafka.connect.json.JsonConverter

internal.key.converter=org.apache.kafka.connect.json.JsonConverter

internal.value.converter=org.apache.kafka.connect.json.JsonConverter

internal.key.converter.schemas.enable=false

internal.value.converter.schemas.enable=false

# required EH Kafka security settings

security.protocol=SASL_SSL

sasl.mechanism=PLAIN

sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";

producer.security.protocol=SASL_SSL

producer.sasl.mechanism=PLAIN

producer.sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";

consumer.security.protocol=SASL_SSL

consumer.sasl.mechanism=PLAIN

consumer.sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";

# path to the libs directory within the Kafka release

plugin.path={KAFKA.DIRECTORY}/libs

```

> [!IMPORTANT]

> Replace `{YOUR.EVENTHUBS.CONNECTION.STRING}` with the connection string for your Event Hubs namespace. For instructions on getting the connection string, see [Get an Event Hubs connection string](event-hubs-get-connection-string.md). Here's an example configuration: `sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="Endpoint=sb://mynamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=XXXXXXXXXXXXXXXX";`

## Run Kafka Connect

In this step, a Kafka Connect worker is started locally in distributed mode, using Event Hubs to maintain cluster state.

1. Save the `connect-distributed.properties` file locally. Be sure to replace all values in braces.

2. Navigate to the location of the Kafka release on your machine.

4. Run `./bin/connect-distributed.sh /PATH/TO/connect-distributed.properties`. The Connect worker REST API is ready for interaction when you see `'INFO Finished starting connectors and tasks'`.

> [!NOTE]

> Kafka Connect uses the Kafka AdminClient API to automatically create topics with recommended configurations, including compaction. A quick check of the namespace in the Azure portal reveals that the Connect worker's internal topics have been created automatically.

>

>Kafka Connect internal topics **must use compaction**. The Event Hubs team isn't responsible for fixing improper configurations if internal Connect topics are incorrectly configured.

### Create connectors

This section walks you through spinning up `FileStreamSource` and `FileStreamSink` connectors.

1. Create a directory for input and output data files.

```bash

mkdir ~/connect-quickstart

```

2. Create two files: one file with seed data from which the `FileStreamSource` connector reads, and another to which our `FileStreamSink` connector writes.

```bash

seq 1000 > ~/connect-quickstart/input.txt

touch ~/connect-quickstart/output.txt

```

3. Create a `FileStreamSource` connector. Be sure to replace the curly braces with your home directory path.

```bash

curl -s -X POST -H "Content-Type: application/json" --data '{"name": "file-source","config": {"connector.class":"org.apache.kafka.connect.file.FileStreamSourceConnector","tasks.max":"1","topic":"connect-quickstart","file": "{YOUR/HOME/PATH}/connect-quickstart/input.txt"}}' http://localhost:8083/connectors

```

You should see the event hub `connect-quickstart` on your Event Hubs instance after running the command.

4. Check status of source connector.

```bash

curl -s http://localhost:8083/connectors/file-source/status

```

Optionally, you can use [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer/releases) to verify that events arrived in the `connect-quickstart` topic.

5. Create a FileStreamSink Connector. Again, make sure you replace the curly braces with your home directory path.

```bash

curl -X POST -H "Content-Type: application/json" --data '{"name": "file-sink", "config": {"connector.class":"org.apache.kafka.connect.file.FileStreamSinkConnector", "tasks.max":"1", "topics":"connect-quickstart", "file": "{YOUR/HOME/PATH}/connect-quickstart/output.txt"}}' http://localhost:8083/connectors

```

6. Check the status of sink connector.

```bash

curl -s http://localhost:8083/connectors/file-sink/status

```

7. Verify that data has been replicated between files and that the data is identical across both files.

```bash

# read the file

cat ~/connect-quickstart/output.txt

# diff the input and output files

diff ~/connect-quickstart/input.txt ~/connect-quickstart/output.txt

```

### Cleanup

Kafka Connect creates Event Hubs topics to store configurations, offsets, and status that persist even after the Connect cluster has been taken down. Unless this persistence is desired, we recommend that you delete these topics. You might also want to delete the `connect-quickstart` Event Hubs that were created during this walkthrough.

## Related content

To learn more about Event Hubs for Kafka, see the following articles:

- [Apache Kafka developer guide for Azure Event Hubs](apache-kafka-developer-guide.md)

- [Explore samples on our GitHub](https://github.com/Azure/azure-event-hubs-for-kafka)


# Event Hubs Kafka Spark Tutorial

# Connect your Apache Spark application with Azure Event Hubs

This tutorial walks you through connecting your Spark application to Event Hubs for real-time streaming. This integration enables streaming without having to change your protocol clients, or run your own Kafka or Zookeeper clusters. This tutorial requires Apache Spark v2.4+ and Apache Kafka v2.0+.

> [!NOTE]

> This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/spark/)

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create an Event Hubs namespace

> * Clone the example project

> * Run Spark

> * Read from Event Hubs for Kafka

> * Write to Event Hubs for Kafka

## Prerequisites

Before you start this tutorial, make sure that you have:

-	Azure subscription. If you don't have one, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

-	[Apache Spark v2.4](https://spark.apache.org/downloads.html)

-	[Apache Kafka v2.0](https://kafka.apache.org/20/documentation.html)

-	[Git](https://www.git-scm.com/downloads)

> [!NOTE]

> The Spark-Kafka adapter was updated to support Kafka v2.0 as of Spark v2.4. In previous releases of Spark, the adapter supported Kafka v0.10 and later but relied specifically on Kafka v0.10 APIs. As Event Hubs for Kafka doesn't support Kafka v0.10, the Spark-Kafka adapters from versions of Spark prior to v2.4 aren't supported by Event Hubs for Kafka Ecosystems.

## Create an Event Hubs namespace

An Event Hubs namespace is required to send and receive from any Event Hubs service. See [Creating an event hub](event-hubs-create.md) for instructions to create a namespace and an event hub. Get the Event Hubs connection string and fully qualified domain name (FQDN) for later use. For instructions, see [Get an Event Hubs connection string](event-hubs-get-connection-string.md).

## Clone the example project

Clone the Azure Event Hubs repository and navigate to the `tutorials/spark` subfolder:

```bash

git clone https://github.com/Azure/azure-event-hubs-for-kafka.git

cd azure-event-hubs-for-kafka/tutorials/spark

```

## Read from Event Hubs for Kafka

With a few configuration changes, you can start reading from Event Hubs for Kafka. Update **BOOTSTRAP_SERVERS** and **EH_SASL** with details from your namespace and you can start streaming with Event Hubs as you would with Kafka. For the full sample code, see sparkConsumer.scala file on the GitHub.

```scala

//Read from your Event Hub!

val df = spark.readStream

.format("kafka")

.option("subscribe", TOPIC)

.option("kafka.bootstrap.servers", BOOTSTRAP_SERVERS)

.option("kafka.sasl.mechanism", "PLAIN")

.option("kafka.security.protocol", "SASL_SSL")

.option("kafka.sasl.jaas.config", EH_SASL)

.option("kafka.request.timeout.ms", "60000")

.option("kafka.session.timeout.ms", "30000")

.option("kafka.group.id", GROUP_ID)

.option("failOnDataLoss", "true")

.load()

//Use dataframe like normal (in this example, write to console)

val df_write = df.writeStream

.outputMode("append")

.format("console")

.start()

```

If you receive an error similar to the following error, add `.option("spark.streaming.kafka.allowNonConsecutiveOffsets", "true")` to the `spark.readStream` call and try again.

```bash

IllegalArgumentException: requirement failed: Got wrong record for <spark job name> even after seeking to offset 4216 got offset 4217 instead. If this is a compacted topic, consider enabling spark.streaming.kafka.allowNonConsecutiveOffsets

```

## Write to Event Hubs for Kafka

You can also write to Event Hubs the same way you write to Kafka. Don't forget to update your configuration to change **BOOTSTRAP_SERVERS** and **EH_SASL** with information from your Event Hubs namespace. For the full sample code, see sparkProducer.scala file on the GitHub.

```scala

df = /**Dataframe**/

//Write to your Event Hub!

df.writeStream

.format("kafka")

.option("topic", TOPIC)

.option("kafka.bootstrap.servers", BOOTSTRAP_SERVERS)

.option("kafka.sasl.mechanism", "PLAIN")

.option("kafka.security.protocol", "SASL_SSL")

.option("kafka.sasl.jaas.config", EH_SASL)

.option("checkpointLocation", "./checkpoint")

.start()

```

## Next steps

To learn more about Event Hubs and Event Hubs for Kafka, see the following articles:

- [Mirror a Kafka broker in an event hub](event-hubs-kafka-mirror-maker-tutorial.md)

- [Connect Apache Flink to an event hub](event-hubs-kafka-flink-tutorial.md)

- [Integrate Kafka Connect with an event hub](event-hubs-kafka-connect-tutorial.md)

- [Explore samples on our GitHub](https://github.com/Azure/azure-event-hubs-for-kafka)

- [Connect Akka Streams to an event hub](event-hubs-kafka-akka-streams-tutorial.md)

- [Apache Kafka developer guide for Azure Event Hubs](apache-kafka-developer-guide.md)


# Event Hubs Kafka Flink Tutorial

# Use Apache Flink with Azure Event Hubs for Apache Kafka

This tutorial shows you how to connect Apache Flink to an event hub without changing your protocol clients or running your own clusters. For more information on Event Hubs' support for the Apache Kafka consumer protocol, see [Event Hubs for Apache Kafka](azure-event-hubs-apache-kafka-overview.md).

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create an Event Hubs namespace

> * Clone the example project

> * Run Flink producer

> * Run Flink consumer

> [!NOTE]

> This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/flink)

## Prerequisites

To complete this tutorial, make sure you have the following prerequisites:

* Read through the [Event Hubs for Apache Kafka](azure-event-hubs-apache-kafka-overview.md) article.

* An Azure subscription. If you don't have one, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

* [Java Development Kit (JDK) 1.7+](/azure/developer/java/fundamentals/java-support-on-azure)

* On Ubuntu, run `apt-get install default-jdk` to install the JDK.

* Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.

* [Download](https://maven.apache.org/download.cgi) and [install](https://maven.apache.org/install.html) a Maven binary archive

* On Ubuntu, you can run `apt-get install maven` to install Maven.

* [Git](https://www.git-scm.com/downloads)

* On Ubuntu, you can run `sudo apt-get install git` to install Git.

## Create an Event Hubs namespace

An Event Hubs namespace is required to send or receive from any Event Hubs service. See [Creating an event hub](event-hubs-create.md) for instructions to create a namespace and an event hub. Make sure to copy the Event Hubs connection string for later use.

## Clone the example project

Now that you have the Event Hubs connection string, clone the Azure Event Hubs for Kafka repository and navigate to the `flink` subfolder:

```shell

git clone https://github.com/Azure/azure-event-hubs-for-kafka.git

cd azure-event-hubs-for-kafka/tutorials/flink

```

## Run Flink producer

Using the provided Flink producer example, send messages to the Event Hubs service.

### Provide an Event Hubs Kafka endpoint

#### producer.config

Update the `bootstrap.servers` and `sasl.jaas.config` values in `producer/src/main/resources/producer.config` to direct the producer to the Event Hubs Kafka endpoint with the correct authentication.

```xml

bootstrap.servers={YOUR.EVENTHUBS.FQDN}:9093

client.id=FlinkExampleProducer

sasl.mechanism=PLAIN

security.protocol=SASL_SSL

sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \

username="$ConnectionString" \

password="{YOUR.EVENTHUBS.CONNECTION.STRING}";

```

> [!IMPORTANT]

> Replace `{YOUR.EVENTHUBS.CONNECTION.STRING}` with the connection string for your Event Hubs namespace. For instructions on getting the connection string, see [Get an Event Hubs connection string](event-hubs-get-connection-string.md). Here's an example configuration: `sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="Endpoint=sb://mynamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=XXXXXXXXXXXXXXXX";`

### Run producer from the command line

To run the producer from the command line, generate the JAR and then run from within Maven (or generate the JAR using Maven, then run in Java by adding one or more necessary Kafka JARs to the classpath):

```shell

mvn clean package

mvn exec:java -Dexec.mainClass="FlinkTestProducer"

```

The producer will now begin sending events to the event hub at topic `test` and printing the events to stdout.

## Run Flink consumer

Using the provided consumer example, receive messages from the event hub.

### Provide an Event Hubs Kafka endpoint

#### consumer.config

Update the `bootstrap.servers` and `sasl.jaas.config` values in `consumer/src/main/resources/consumer.config` to direct the consumer to the Event Hubs Kafka endpoint with the correct authentication.

```xml

bootstrap.servers={YOUR.EVENTHUBS.FQDN}:9093

group.id=FlinkExampleConsumer

sasl.mechanism=PLAIN

security.protocol=SASL_SSL

sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \

username="$ConnectionString" \

password="{YOUR.EVENTHUBS.CONNECTION.STRING}";

```

> [!IMPORTANT]

> Replace `{YOUR.EVENTHUBS.CONNECTION.STRING}` with the connection string for your Event Hubs namespace. For instructions on getting the connection string, see [Get an Event Hubs connection string](event-hubs-get-connection-string.md). Here's an example configuration: `sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="Endpoint=sb://mynamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=XXXXXXXXXXXXXXXX";`

### Run consumer from the command line

To run the consumer from the command line, generate the JAR and then run from within Maven (or generate the JAR using Maven, then run in Java by adding one or more necessary Kafka JARs to the classpath):

```shell

mvn clean package

mvn exec:java -Dexec.mainClass="FlinkTestConsumer"

```

If the event hub has events (for example, if your producer is also running), then the consumer now begins receiving events from the topic `test`.

Check out [Flink's Kafka Connector Guide](https://nightlies.apache.org/flink/flink-docs-stable/docs/connectors/datastream/kafka) for more detailed information about connecting Flink to Kafka.

## Next steps

To learn more about Event Hubs for Kafka, see the following articles:

- [Mirror a Kafka broker in an event hub](event-hubs-kafka-mirror-maker-tutorial.md)

- [Connect Apache Spark to an event hub](event-hubs-kafka-spark-tutorial.md)

- [Integrate Kafka Connect with an event hub](event-hubs-kafka-connect-tutorial.md)

- [Explore samples on our GitHub](https://github.com/Azure/azure-event-hubs-for-kafka)

- [Connect Akka Streams to an event hub](event-hubs-kafka-akka-streams-tutorial.md)

- [Apache Kafka developer guide for Azure Event Hubs](apache-kafka-developer-guide.md)


# Event Hubs Kafka Connect Debezium

# Integrate Apache Kafka Connect support on Azure Event Hubs with Debezium for Change Data Capture

**Change Data Capture (CDC)** is a technique used to track row-level changes in database tables in response to create, update, and delete operations. [Debezium](https://debezium.io/) is a distributed platform that builds on top of Change Data Capture features available in different databases (for example, [logical decoding in PostgreSQL](https://www.postgresql.org/docs/current/static/logicaldecoding-explanation.html)). It provides a set of [Kafka Connect connectors](https://debezium.io/documentation/reference/stable/connectors/index.html) that tap into row-level changes in database tables and convert them into event streams that are then sent to [Apache Kafka](https://kafka.apache.org/).

This tutorial walks you through how to set up a change data capture based system on Azure using [Event Hubs](./event-hubs-about.md?WT.mc_id=devto-blog-abhishgu) (for Kafka), [Azure Database for PostgreSQL](/azure/postgresql/overview) and Debezium. It uses the [Debezium PostgreSQL connector](https://debezium.io/documentation/reference/stable/connectors/postgresql.html) to stream database modifications from PostgreSQL to Kafka topics in Event Hubs.

> [!NOTE]

> This article contains references to a term that Microsoft no longer uses. When the term is removed from the software, we'll remove it from this article.

In this tutorial, you take the following steps:

> [!div class="checklist"]

> * Create an Event Hubs namespace

> * Setup and configure Azure Database for PostgreSQL

> * Configure and run Kafka Connect with Debezium PostgreSQL connector

> * Test change data capture

> * (Optional) Consume change data events with a `FileStreamSink` connector

## Prerequisites

To complete this walk through, you require:

- Azure subscription. If you don't have one, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- Linux/macOS

- Kafka release (version 1.1.1, Scala version 2.11), available from [kafka.apache.org](https://kafka.apache.org/downloads#1.1.1)

- Read through the [Event Hubs for Apache Kafka](./azure-event-hubs-apache-kafka-overview.md) introduction article

## Create an Event Hubs namespace

An Event Hubs namespace is required to send and receive from any Event Hubs service. See [Creating an event hub](event-hubs-create.md) for instructions to create a namespace and an event hub. Get the Event Hubs connection string and fully qualified domain name (FQDN) for later use. For instructions, see [Get an Event Hubs connection string](event-hubs-get-connection-string.md).

## Set up and configure Azure Database for PostgreSQL

[Azure Database for PostgreSQL](/azure/postgresql/overview) is a relational database service based on the community version of open-source PostgreSQL database engine, and is available in three deployment options: Single Server, Flexible Server, and Cosmos DB for PostgreSQL. [Follow these instructions](/azure/postgresql/quickstart-create-server-database-portal) to create an Azure Database for PostgreSQL server using the Azure portal.

## Setup and run Kafka Connect

This section covers the following topics:

- Debezium connector installation

- Configuring Kafka Connect for Event Hubs

- Start Kafka Connect cluster with Debezium connector

### Download and setup Debezium connector

Follow the latest instructions in the [Debezium documentation](https://debezium.io/documentation/reference/stable/connectors/postgresql.html#postgresql-deployment) to download and set up the connector.

- Download the connector’s plug-in archive. For example, to download version `1.2.0` of the connector, use this link - https://repo1.maven.org/maven2/io/debezium/debezium-connector-postgres/1.2.0.Final/debezium-connector-postgres-1.2.0.Final-plugin.tar.gz

- Extract the JAR files and copy them to the [Kafka Connect plugin.path](https://kafka.apache.org/documentation/#connectconfigs).

### Configure Kafka Connect for Event Hubs

Minimal reconfiguration is necessary when redirecting Kafka Connect throughput from Kafka to Event Hubs. The following `connect-distributed.properties` sample illustrates how to configure Connect to authenticate and communicate with the Kafka endpoint on Event Hubs:

> [!IMPORTANT]

> - Debezium auto-creates a topic per table and a bunch of metadata topics. Kafka **topic** corresponds to an Event Hubs instance (event hub). For Apache Kafka to Azure Event Hubs mappings, see [Kafka and Event Hubs conceptual mapping](azure-event-hubs-apache-kafka-overview.md#apache-kafka-and-azure-event-hubs-conceptual-mapping).

> - There are different **limits** on number of event hubs in an Event Hubs namespace depending on the tier (Basic, Standard, Premium, or Dedicated). For these limits, See [Quotas](compare-tiers.md#quotas).

```properties

bootstrap.servers={YOUR.EVENTHUBS.FQDN}:9093 # e.g. namespace.servicebus.windows.net:9093

group.id=connect-cluster-group

# connect internal topic names, auto-created if not exists

config.storage.topic=connect-cluster-configs

offset.storage.topic=connect-cluster-offsets

status.storage.topic=connect-cluster-status

# internal topic replication factors - auto 3x replication in Azure Storage

config.storage.replication.factor=1

offset.storage.replication.factor=1

status.storage.replication.factor=1

rest.advertised.host.name=connect

offset.flush.interval.ms=10000

key.converter=org.apache.kafka.connect.json.JsonConverter

value.converter=org.apache.kafka.connect.json.JsonConverter

internal.key.converter=org.apache.kafka.connect.json.JsonConverter

internal.value.converter=org.apache.kafka.connect.json.JsonConverter

internal.key.converter.schemas.enable=false

internal.value.converter.schemas.enable=false

# required EH Kafka security settings

security.protocol=SASL_SSL

sasl.mechanism=PLAIN

sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";

producer.security.protocol=SASL_SSL

producer.sasl.mechanism=PLAIN

producer.sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";

consumer.security.protocol=SASL_SSL

consumer.sasl.mechanism=PLAIN

consumer.sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{YOUR.EVENTHUBS.CONNECTION.STRING}";

plugin.path={KAFKA.DIRECTORY}/libs # path to the libs directory within the Kafka release

```

> [!IMPORTANT]

> Replace `{YOUR.EVENTHUBS.CONNECTION.STRING}` with the connection string for your Event Hubs namespace. For instructions on getting the connection string, see [Get an Event Hubs connection string](event-hubs-get-connection-string.md). Here's an example configuration: `sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="Endpoint=sb://mynamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=XXXXXXXXXXXXXXXX";`

### Run Kafka Connect

In this step, a Kafka Connect worker is started locally in distributed mode, using Event Hubs to maintain cluster state.

1. Save the `connect-distributed.properties` file locally. Be sure to replace all values in braces.

2. Navigate to the location of the Kafka release on your machine.

3. Run `./bin/connect-distributed.sh /PATH/TO/connect-distributed.properties` and wait for the cluster to start.

> [!NOTE]

> Kafka Connect uses the Kafka AdminClient API to automatically create topics with recommended configurations, including compaction. A quick check of the namespace in the Azure portal reveals that the Connect worker's internal topics have been created automatically.

>

> Kafka Connect internal topics **must use compaction**. The Event Hubs team isn't responsible for fixing improper configurations if internal Connect topics are incorrectly configured.

### Configure and start the Debezium PostgreSQL source connector

Create a configuration file (`pg-source-connector.json`) for the PostgreSQL source connector - replace the values as per your Azure PostgreSQL instance.

```json

{

"name": "todo-connector",

"config": {

"connector.class": "io.debezium.connector.postgresql.PostgresConnector",

"database.hostname": "<replace with Azure PostgreSQL instance name>.postgres.database.azure.com",

"database.port": "5432",

"database.user": "<replace with database user name>",

"database.password": "<replace with database password>",

"database.dbname": "postgres",

"database.server.name": "my-server",

"plugin.name": "wal2json",

"table.whitelist": "public.todos"

}

}

```

> [!TIP]

> `database.server.name` attribute is a logical name that identifies and provides a namespace for the particular PostgreSQL database server/cluster being monitored.

To create an instance of the connector, use the Kafka Connect REST API endpoint:

```bash

curl -X POST -H "Content-Type: application/json" --data @pg-source-connector.json http://localhost:8083/connectors

```

To check the status of the connector:

```bash

curl -s http://localhost:8083/connectors/todo-connector/status

```

## Test change data capture

To see change data capture in action, you need to create/update/delete records in the Azure PostgreSQL database.

Start by connecting to your Azure PostgreSQL database (the following example uses [psql](https://www.postgresql.org/docs/12/app-psql.html)).

```bash

psql -h <POSTGRES_INSTANCE_NAME>.postgres.database.azure.com -p 5432 -U <POSTGRES_USER_NAME> -W -d <POSTGRES_DB_NAME> --set=sslmode=require

e.g.

psql -h my-postgres.postgres.database.azure.com -p 5432 -U testuser@my-postgres -W -d postgres --set=sslmode=require

```

**Create a table and insert records**

```sql

CREATE TABLE todos (id SERIAL, description VARCHAR(50), todo_status VARCHAR(12), PRIMARY KEY(id));

INSERT INTO todos (description, todo_status) VALUES ('setup postgresql on azure', 'complete');

INSERT INTO todos (description, todo_status) VALUES ('setup kafka connect', 'complete');

INSERT INTO todos (description, todo_status) VALUES ('configure and install connector', 'in-progress');

INSERT INTO todos (description, todo_status) VALUES ('start connector', 'pending');

```

The connector should now spring into action and send change data events to an Event Hubs topic with the following name `my-server.public.todos`, assuming you have `my-server` as the value for `database.server.name` and `public.todos` is the table whose changes you're tracking (as per `table.whitelist` configuration).

**Check Event Hubs topic**

Let's introspect the contents of the topic to make sure everything is working as expected. The following example uses [`kafkacat`](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/quickstart/kafkacat), but you can also [create a consumer using any of the options listed here](apache-kafka-developer-guide.md).

Create a file named `kafkacat.conf` with the following contents:

```

metadata.broker.list=<enter event hubs namespace>.servicebus.windows.net:9093

security.protocol=SASL_SSL

sasl.mechanisms=PLAIN

sasl.username=$ConnectionString

sasl.password=<enter event hubs connection string>

```

> [!NOTE]

> Update `metadata.broker.list` and `sasl.password` attributes in `kafkacat.conf` as per Event Hubs information.

In a different terminal, start a consumer:

```bash

export KAFKACAT_CONFIG=kafkacat.conf

export BROKER=<enter event hubs namespace>.servicebus.windows.net:9093

export TOPIC=my-server.public.todos

kafkacat -b $BROKER -t $TOPIC -o beginning

```

You should see the JSON payloads representing the change data events generated in PostgreSQL in response to the rows you had added to the `todos` table. Here's a snippet of the payload:

```json

{

"schema": {...},

"payload": {

"before": null,

"after": {

"id": 1,

"description": "setup postgresql on azure",

"todo_status": "complete"

},

"source": {

"version": "1.2.0.Final",

"connector": "postgresql",

"name": "fulfillment",

"ts_ms": 1593018069944,

"snapshot": "last",

"db": "postgres",

"schema": "public",

"table": "todos",

"txId": 602,

"lsn": 184579736,

"xmin": null

},

"op": "c",

"ts_ms": 1593018069947,

"transaction": null

}

```

The event consists of the `payload` along with its `schema` (omitted for brevity). In `payload` section, notice how the create operation (`"op": "c"`) is represented - `"before": null` means that it was a newly `INSERT`ed row, `after` provides values for the columns in the row, `source` provides the PostgreSQL instance metadata from where this event was picked up and so on.

You can try the same with update or delete operations as well and introspect the change data events. For example, to update the task status for `configure and install connector` (assuming its `id` is `3`):

```sql

UPDATE todos SET todo_status = 'complete' WHERE id = 3;

```

## (Optional) Install FileStreamSink connector

Now that all the `todos` table changes are being captured in Event Hubs topic, you use the FileStreamSink connector (that is available by default in Kafka Connect) to consume these events.

Create a configuration file (`file-sink-connector.json`) for the connector - replace the `file` attribute as per your file system.

```json

{

"name": "cdc-file-sink",

"config": {

"connector.class": "org.apache.kafka.connect.file.FileStreamSinkConnector",

"tasks.max": "1",

"topics": "my-server.public.todos",

"file": "<enter full path to file e.g. /Users/foo/todos-cdc.txt>"

}

}

```

To create the connector and check its status:

```bash

curl -X POST -H "Content-Type: application/json" --data @file-sink-connector.json http://localhost:8083/connectors

curl http://localhost:8083/connectors/cdc-file-sink/status

```

Insert/update/delete database records and monitor the records in the configured output sink file:

```bash

tail -f /Users/foo/todos-cdc.txt

```

## Cleanup

Kafka Connect creates Event Hubs topics to store configurations, offsets, and status that persist even after the Kafka Connect cluster has been taken down. Unless this persistence is desired, we recommend that you delete these topics. You might also want to delete the `my-server.public.todos` event hub that were created during this walk through.

## Next steps

To learn more about Event Hubs for Kafka, see the following articles:

- [Mirror a Kafka broker in an event hub](event-hubs-kafka-mirror-maker-tutorial.md)

- [Connect Apache Spark to an event hub](event-hubs-kafka-spark-tutorial.md)

- [Connect Apache Flink to an event hub](event-hubs-kafka-flink-tutorial.md)

- [Explore samples on our GitHub](https://github.com/Azure/azure-event-hubs-for-kafka)

- [Connect Akka Streams to an event hub](event-hubs-kafka-akka-streams-tutorial.md)

- [Apache Kafka developer guide for Azure Event Hubs](apache-kafka-developer-guide.md)


# Event Hubs Kafka Akka Streams Tutorial

# Using Akka Streams with Event Hubs for Apache Kafka

This tutorial shows you how to connect Akka Streams through the Event Hubs support for Apache Kafka without changing your protocol clients or running your own clusters.

In this tutorial, you learn how to:

> [!div class="checklist"]

> * Create an Event Hubs namespace

> * Clone the example project

> * Run Akka Streams producer

> * Run Akka Streams consumer

> [!NOTE]

> This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs-for-kafka/tree/master/tutorials/akka/java)

## Prerequisites

To complete this tutorial, make sure you have the following prerequisites:

* Read through the [Event Hubs for Apache Kafka](azure-event-hubs-apache-kafka-overview.md) article.

* An Azure subscription. If you don't have one, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

* [Java Development Kit (JDK) 1.8+](/azure/developer/java/fundamentals/java-support-on-azure)

* On Ubuntu, run `apt-get install default-jdk` to install the JDK.

* Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.

* [Download](https://maven.apache.org/download.cgi) and [install](https://maven.apache.org/install.html) a Maven binary archive

* On Ubuntu, you can run `apt-get install maven` to install Maven.

* [Git](https://www.git-scm.com/downloads)

* On Ubuntu, you can run `sudo apt-get install git` to install Git.

## Create an Event Hubs namespace

An Event Hubs namespace is required to send or receive from any Event Hubs service. See [Create an event hub](event-hubs-create.md) for detailed information. Make sure to copy the Event Hubs connection string for later use.

## Clone the example project

Now that you have an Event Hubs connection string, clone the Azure Event Hubs for Kafka repository and navigate to the `akka` subfolder:

```shell

git clone https://github.com/Azure/azure-event-hubs-for-kafka.git

cd azure-event-hubs-for-kafka/tutorials/akka/java

```

## Run Akka Streams producer

Using the provided Akka Streams producer example, send messages to the Event Hubs service.

### Provide an Event Hubs Kafka endpoint

#### Producer application.conf

Update the `bootstrap.servers` and `sasl.jaas.config` values in `producer/src/main/resources/application.conf` to direct the producer to the Event Hubs Kafka endpoint with the correct authentication.

```xml

akka.kafka.producer {

#Akka Kafka producer properties can be defined here

# Properties defined by org.apache.kafka.clients.producer.ProducerConfig

# can be defined in this configuration section.

kafka-clients {

bootstrap.servers="{YOUR.EVENTHUBS.FQDN}:9093"

sasl.mechanism=PLAIN

security.protocol=SASL_SSL

sasl.jaas.config="org.apache.kafka.common.security.plain.PlainLoginModule required username=\"$ConnectionString\" password=\"{YOUR.EVENTHUBS.CONNECTION.STRING}\";"

}

}

```

> [!IMPORTANT]

> Replace `{YOUR.EVENTHUBS.CONNECTION.STRING}` with the connection string for your Event Hubs namespace. For instructions on getting the connection string, see [Get an Event Hubs connection string](event-hubs-get-connection-string.md). Here's an example configuration: `sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="Endpoint=sb://mynamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=XXXXXXXXXXXXXXXX";`

### Run producer from the command line

To run the producer from the command line, generate the JAR and then run from within Maven (or generate the JAR using Maven, then run in Java by adding the necessary Kafka Java Archive files (JARs) to the classpath):

```shell

mvn clean package

mvn exec:java -Dexec.mainClass="AkkaTestProducer"

```

The producer begins sending events to the event hub at topic `test`, and prints the events to stdout.

## Run Akka Streams consumer

Using the provided consumer example, receive messages from the event hub.

### Provide an Event Hubs Kafka endpoint

#### Consumer application.conf

Update the `bootstrap.servers` and `sasl.jaas.config` values in `consumer/src/main/resources/application.conf` to direct the consumer to the Event Hubs Kafka endpoint with the correct authentication.

```xml

akka.kafka.consumer {

#Akka Kafka consumer properties defined here

wakeup-timeout=60s

# Properties defined by org.apache.kafka.clients.consumer.ConsumerConfig

# defined in this configuration section.

kafka-clients {

request.timeout.ms=60000

group.id=akka-example-consumer

bootstrap.servers="{YOUR.EVENTHUBS.FQDN}:9093"

sasl.mechanism=PLAIN

security.protocol=SASL_SSL

sasl.jaas.config="org.apache.kafka.common.security.plain.PlainLoginModule required username=\"$ConnectionString\" password=\"{YOUR.EVENTHUBS.CONNECTION.STRING}\";"

}

}

```

> [!IMPORTANT]

> Replace `{YOUR.EVENTHUBS.CONNECTION.STRING}` with the connection string for your Event Hubs namespace. For instructions on getting the connection string, see [Get an Event Hubs connection string](event-hubs-get-connection-string.md). Here's an example configuration: `sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="Endpoint=sb://mynamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=XXXXXXXXXXXXXXXX";`

### Run consumer from the command line

To run the consumer from the command line, generate the JAR and then run from within Maven (or generate the JAR using Maven, then run in Java by adding the necessary Kafka JARs to the classpath):

```shell

mvn clean package

mvn exec:java -Dexec.mainClass="AkkaTestConsumer"

```

If the event hub has events (for instance, if your producer is also running), then the consumer begins receiving events from topic `test`.

Check out the [Akka Streams Kafka Guide](https://doc.akka.io/docs/akka-stream-kafka/current/home.html) for more detailed information about Akka Streams.

## Next steps

To learn more about Event Hubs for Kafka, see the following articles:

- [Mirror a Kafka broker in an event hub](event-hubs-kafka-mirror-maker-tutorial.md)

- [Connect Apache Spark to an event hub](event-hubs-kafka-spark-tutorial.md)

- [Connect Apache Flink to an event hub](event-hubs-kafka-flink-tutorial.md)

- [Integrate Kafka Connect with an event hub](event-hubs-kafka-connect-tutorial.md)

- [Explore samples on our GitHub](https://github.com/Azure/azure-event-hubs-for-kafka)

- [Apache Kafka developer guide for Azure Event Hubs](apache-kafka-developer-guide.md)


# Use Log Compaction

# Use log compaction

This article shows you how to use log compaction feature in Event Hubs. To understand the details of log compaction, see [Log Compaction](log-compaction.md).

In this article you'll, follow these key steps:

- Create a compacted event hub/Kafka topic.

- Publish events to a compacted event hub.

- Consume events from a compacted event hub.

> [!NOTE]

> Log compaction feature isn't supported in the **Basic** tier.

## Create a compacted event hub/Kafka topic

This section shows you how to create a compacted event hub using Azure portal and an Azure Resource Manager (ARM) template.

### [Azure portal](#tab/portal)

You can create a compacted event hub using the Azure portal by following these steps.

1. Navigate to your Event Hubs namespace.

1. On the Event Hubs Namespace page, select Event Hubs in the left menu.

1. At the top of the window, select + Event Hubs.

1. Type a *name* for your event hub, and specify the *partition count*. Since we're creating a compacted event hub, select *compaction policy* as *compaction* and provide the desired value for *tombstone retention time*.

1. Select *create* and create the compacted event hub.

### [ARM template](#tab/arm)

The following example shows how to create a compacted event hub/Kafka topic using an ARM template.

```json

"resources": [

{

"apiVersion": "2017-04-01",

"name": "[parameters('eventHubName')]",

"type": "eventhubs",

"dependsOn": [

"[resourceId('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"

],

"properties": {

"partitionCount": "[parameters('partitionCount')]",

"retentionDescription": {

"cleanupPolicy": "compact",

"tombstoneRetentionTimeInHours": "24"

}

}

}

]

```

---

## Triggering compaction

Event Hubs service determines when the compaction job of a given compacted event hub should be executed. Compacted event hub reaches the compaction threshold when there are considerable number of events or the total size of a given event log grows significantly.

## Publish event to a compacted topic

Publishing events to a compacted event hub is the same as publishing events to a regular event hub. As the client application you only need to determine the compaction key, which you set using partition key.

### Using Event Hubs SDK(AMQP)

With Event Hubs SDK, you can set partition key and publish events as shown below:

```csharp

var enqueueOptions = new EnqueueEventOptions

{

PartitionKey = "Key-1"

};

await producer.EnqueueEventAsync(eventData, enqueueOptions);

```

### Using Kafka

With Kafka you can set the partition key when you create the `ProducerRecord` as shown below:

```java

ProducerRecord<String, String> record = new ProducerRecord<String, String>(TOPIC, "Key-1" , "Value-1");

```

## Quotas and limits

| Limit | Basic | Standard | Premium |  Dedicated |

| ----- | ----- | -------- | -------- | --------- |

| Size of compacted event hub  | N/A | 1 GB per partition | 250 GB per partition | 250 GB per partition |

For other quotas and limits, see [Event Hubs quotas and limits](event-hubs-quotas.md).

## Consuming events from a compacted topic

There are no changes required at the consumer side to consume events from a compacted event hub. So, you can use any of the existing consumer applications to consume data from a compacted event hub.

## Next steps

- For conceptual information on how log compaction work, see [Log compaction](log-compaction.md).


# Schema Registry Json Schema Kafka

# Use JSON Schema with Apache Kafka applications

This tutorial walks you through a scenario where you use JSON Schemas to serialize and deserialize event using Azure Schema Registry in Event Hubs.

In this use case a Kafka producer application uses JSON schema stored in Azure Schema Registry to, serialize the event and publish them to a Kafka topic/event hub in Azure Event Hubs. The Kafka consumer deserializes the events that it consumes from Event Hubs. For that it uses schema ID of the event and JSON schema, which is stored in Azure Schema Registry.

## Prerequisites

If you're new to Azure Event Hubs, see [Event Hubs overview](event-hubs-about.md) before you do this quickstart.

To complete this quickstart, you need the following prerequisites:

- If you don't have an **Azure subscription**, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

- In your development environment, install the following components:

* [Java Development Kit (JDK) 1.7+](/azure/developer/java/fundamentals/java-support-on-azure).

* [Download](https://maven.apache.org/download.cgi) and [install](https://maven.apache.org/install.html) a Maven binary archive.

* [Git](https://www.git-scm.com/)

- Clone the [Azure Schema Registry for Kafka](https://github.com/Azure/azure-schema-registry-for-kafka.git) repository.

## Create an event hub

Follow instructions from the quickstart: [Create an Event Hubs namespace and an event hub](event-hubs-create.md) to create an Event Hubs namespace and an event hub. Then, follow instructions from [Get the connection string](event-hubs-get-connection-string.md) to get a connection string to your Event Hubs namespace.

Note down the following settings that you use in the current quickstart:

- Connection string for the Event Hubs namespace

- Name of the event hub

## Create a schema

Follow instructions from [Create schemas using Schema Registry](create-schema-registry.md) to create a schema group and a schema.

1. Create a schema group named **contoso-sg** using the Schema Registry portal. Use *JSON Schema* as the serialization type.

1. In that schema group, create a new JSON schema with schema name: ``Microsoft.Azure.Data.SchemaRegistry.example.CustomerInvoice`` using the following schema content.

```json

{

"$id": "https://example.com/person.schema.json",

"$schema": "https://json-schema.org/draft/2020-12/schema",

"title": "CustomerInvoice",

"type": "object",

"properties": {

"invoiceId": {

"type": "string"

},

"merchantId": {

"type": "string"

},

"transactionValueUsd": {

"type": "integer"

},

"userId": {

"type": "string"

}

}

}

```

## Register an application to access schema registry

You can use Microsoft Entra ID to authorize your Kafka producer and consumer application to access Azure Schema Registry resources. To enable it, you need to register your client application with a Microsoft Entra tenant from the Azure portal.

To register a Microsoft Entra application named  `example-app` see [Register your application with a Microsoft Entra tenant](authenticate-application.md).

- tenant.id - sets the tenant ID of the application

- client.id - sets the client ID of the application

- client.secret - sets the client secret for authentication

And if you're using managed identity, you would need:

- use.managed.identity.credential - indicates that MSI credentials should be used, should be used for MSI-enabled VM

- managed.identity.clientId - if specified, it builds MSI credential with given client ID managed.identity.resourceId - if specified, it builds MSI credential with given resource ID

## Add user to Schema Registry Reader role

Add your user account to the **Schema Registry Reader** role at the namespace level. You can also use the **Schema Registry Contributor** role, but that's not necessary for this quickstart.

1. On the **Event Hubs namespace** page, select **Access control (IAM)** on the left menu.

2. On the **Access control (IAM)** page, select **+ Add** -> **Add role assignment** on the menu.

3. On the **Assignment type** page, select **Next**.

4. On the **Roles** page, select **Schema Registry Reader**, and then select **Next** at the bottom of the page.

5. Use the **+ Select members** link to add the `example-app` application that you created in the previous step to the role, and then select **Next**.

6. On the **Review + assign** page, select **Review + assign**.

## Update client application configuration of Kafka applications

You need to update the client configuration of the Kafka producer and consumer applications with the Microsoft Entra application details and with the schema registry information.

To update the Kafka Producer configuration, navigate to *azure-schema-registry-for-kafka/tree/master/java/json/samples/kafka-producer*.

1. Update the configuration of the Kafka application in *src/main/resources/app.properties* by following [Kafka Quickstart guide for Event Hubs](event-hubs-quickstart-kafka-enabled-event-hubs.md).

1. Update the configuration details for the producer in *src/main/resources/app.properties* using schema registry related configuration and Microsoft Entra application that you created in the previous step as follows:

```xml

schema.group=contoso-sg

schema.registry.url=https://<NAMESPACENAME>.servicebus.windows.net

tenant.id=<>

client.id=<>

client.secret=<>

1. Follow the same instructions and update the *azure-schema-registry-for-kafka/tree/master/java/json/samples/kafka-consumer* configuration as well.

1. For both Kafka producer and consumer applications, following JSON schema is used:

```json

{

"$id": "https://example.com/person.schema.json",

"$schema": "https://json-schema.org/draft/2020-12/schema",

"title": "CustomerInvoice",

"type": "object",

"properties": {

"invoiceId": {

"type": "string"

},

"merchantId": {

"type": "string"

},

"transactionValueUsd": {

"type": "integer"

},

"userId": {

"type": "string"

}

}

}

```

## Using Kafka producer with JSON schema validation

To run the Kafka producer application, navigate to *azure-schema-registry-for-kafka/tree/master/java/json/samples/kafka-producer*.

1. You can run the producer application so that it can produce JSON Schema specific records or generic records. For specific records mode you need to first generate the classes against either the producer schema using the following maven command:

```shell

mvn generate-sources

```

1. Then you can run the producer application using the following commands.

```shell

mvn clean package

mvn -e clean compile exec:java -Dexec.mainClass="com.azure.schemaregistry.samples.producer.App"

```

1. Upon successful execution of the producer application, it prompts you to choose the producer scenario. For this quickstart, you can choose option *1 - produce SpecificRecords*.

```shell

Enter case number:

1 - produce SpecificRecords

```

1. Upon successful data serialization and publishing, you should see the following console logs in your producer application:

```shell

INFO com.azure.schemaregistry.samples.producer.KafkaJsonSpecificRecord - Sent Order Invoice 0

INFO com.azure.schemaregistry.samples.producer.KafkaJsonSpecificRecord - Sent Order Invoice 1

INFO com.azure.schemaregistry.samples.producer.KafkaJsonSpecificRecord - Sent Order Invoice 2

```

## Using Kafka consumer with JSON schema validation

To run the Kafka consumer application, navigate to *azure-schema-registry-for-kafka/tree/master/java/json/samples/kafka-consumer*.

1. You can run the consumer application so that it can consume JSON Schema specific records or generic records. For specific records mode you need to first generate the classes against either the producer schema using the following maven command:

```shell

mvn generate-sources

```

1. Then you can run the consumer application using the following command.

```shell

mvn clean package

mvn -e clean compile exec:java -Dexec.mainClass="com.azure.schemaregistry.samples.consumer.App"

```

1. Upon successful execution of the consumer application, it prompts you to choose the producer scenario. For this quickstart, you can choose option *1 - consume SpecificRecords*.

```shell

Enter case number:

1 - consume SpecificRecords

```

1. Upon successful data consumption and deserialization, you should see the following console logs in your producer application:

```shell

INFO com.azure.schemaregistry.samples.consumer.KafkaJsonSpecificRecord - Invoice received: {invoiceId=Invoice 0, merchantId=Merchant Id 0, transactionValueUsd=0, userId=User Id 0}

INFO com.azure.schemaregistry.samples.consumer.KafkaJsonSpecificRecord - Invoice received: {invoiceId=Invoice 1, merchantId=Merchant Id 1, transactionValueUsd=1, userId=User Id 1}

INFO com.azure.schemaregistry.samples.consumer.KafkaJsonSpecificRecord - Invoice received: {invoiceId=Invoice 2, merchantId=Merchant Id 2, transactionValueUsd=2, userId=User Id 2}

```

## Clean up resources

Delete the Event Hubs namespace or delete the resource group that contains the namespace.


# Process Data Azure Stream Analytics

# Process data from your event hub using Azure Stream Analytics

The Azure Stream Analytics service makes it easy to ingest, process, and analyze streaming data from Azure Event Hubs, enabling powerful insights to drive real-time actions. You can use the Azure portal to visualize incoming data and write a Stream Analytics query. Once your query is ready, you can move it into production in only a few clicks.

## Key benefits

Here are the key benefits of Azure Event Hubs and Azure Stream Analytics integration:

- **Preview data** – You can preview incoming data from an event hub in the Azure portal.

- **Test your query** – Prepare a transformation query and test it directly in the Azure portal. For the query language syntax, see [Stream Analytics Query Language](/stream-analytics-query/built-in-functions-azure-stream-analytics) documentation.

- **Deploy your query to production** – You can deploy the query into production by creating and starting an Azure Stream Analytics job.

## End-to-end flow

> [!IMPORTANT]

> - If you aren't a member of [owner](../role-based-access-control/built-in-roles.md#owner) or [contributor](../role-based-access-control/built-in-roles.md#contributor) roles at the Azure subscription level, you must be a member of the [Stream Analytics Query Tester](../role-based-access-control/built-in-roles.md#stream-analytics-query-tester) role at the Azure subscription level to successfully complete steps in this section. This role allows you to perform testing queries without creating a stream analytics job first. For instructions on assigning a role to a user, see [Assign AD roles to users](../active-directory/roles/manage-roles-portal.md).

> - If your event hub allows only the private access via private endpoints, you must have the Stream Analytics job joined to the same network so that the job can access events in the event hub.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Navigate to your **Event Hubs namespace** and then navigate to the **event hub**, which has the incoming data.

1. On the left navigation menu, expand **Features**, and select **Process data**, and then select **Start** on the **Enable real time insights from events** tile.

1. You see a query page with values already set for the following fields. If you see a popup window about a consumer group and a policy being created for you, select **OK**. You immediately see a snapshot of the latest incoming data in this tab.

1. Your **event hub** as an input for the query.

1. Sample **SQL query** with SELECT statement.

1. An **output** alias to refer to your query test results.

- The serialization type in your data is automatically detected (JSON/CSV). You can manually change it as well to JSON/CSV/AVRO.

- You can preview incoming data in the table format or raw format.

- If your data shown isn't current, select **Refresh** to see the latest events.

- In the preceding image, the results are shown in the table format. To see the raw data, select **Raw**

1. Select **Test query** to see the snapshot of test results of your query in the **Test results** tab. You can also download the results.

Write your own query to transform the data. See [Stream Analytics Query Language reference](/stream-analytics-query/stream-analytics-query-language-reference).

1. Once you tested the query and you want to move it in to production, select **Create Stream Analytics job**.

1. On the **New Stream Analytics job** page, follow these steps:

1. Specify a **name** for the job.

1. Select your **Azure subscription** where you want the job to be created.

1. Select the **resource group** for the Stream Analytics job resource.

1. Select the **location** for the job.

1. For the **Event Hubs policy name**, create a new policy or select an existing one.

1. For the **Event Hubs consumer group**, create a new consumer group or select an existing consumer group.

1. Select **Create** to create the Stream Analytics job.

> [!NOTE]

>  We recommend that you create a consumer group and a policy for each new Azure Stream Analytics job that you create from the Event Hubs page. Consumer groups allow only five concurrent readers, so providing a dedicated consumer group for each job will avoid any errors that might arise from exceeding that limit. A dedicated policy allows you to rotate your key or revoke permissions without impacting other resources.

1. Your Stream Analytics job is now created where your query is the same that you tested, and input is your event hub.

9.	Add an [output](../stream-analytics/stream-analytics-define-outputs.md) of your choice.

1. Navigate back to Stream Analytics job page by clicking the name of the job in breadcrumb link.

1. Select **Edit query** above the **Query** window.

1. Update `[OutputAlias]` with your output name, and select **Save query** link above the query. Close the Query page by selecting X in the top-right corner.

1. Now, on the Stream Analytics job page, select **Start** on the toolbar to start the job.

## Access

**Issue** : User can't access preview data because they don’t have right permissions on the Subscription.

Option 1: The user who wants to preview incoming data needs to be added as a Contributor on Subscription.

Option 2: The user needs to be added as Stream Analytics Query tester role on Subscription. Navigate to Access control for the subscription. Add a new role assignment for the user as "Stream Analytics Query Tester" role.

Option 3: The user can create Azure Stream Analytics job. Set input as this event hub and navigate to "Query" to preview incoming data from this event hub.

Option 4: The admin can create a custom role on the subscription. Add the following permissions to the custom role and then add user to the new custom role.

## Streaming units

Your Azure Stream Analytics job defaults to three streaming units (SUs). To adjust this setting, select **Scale** on the left menu in the **Stream Analytics job** page in the Azure portal. To learn more about streaming units, see [Understand and adjust Streaming Units](../stream-analytics/stream-analytics-streaming-unit-consumption.md).

[!INCLUDE [geo-replication-stream-analytics-job](../stream-analytics/includes/geo-replication-stream-analytics-job.md)]

## Related content

To learn more about Stream Analytics queries, see [Stream Analytics Query Language](/stream-analytics-query/built-in-functions-azure-stream-analytics)


# Resource Governance With App Groups

# Govern resources for client applications with application groups

Azure Event Hubs enables you to govern event streaming workloads for client applications that connect to Event Hubs by using **application groups**. For more information, see [Resource governance with application groups](resource-governance-overview.md).

This article shows you how to perform the following tasks:

- Create an application group.

- Enable or disable an application group

- Define threshold limits and apply throttling policies to an application group

- Validate throttling with Diagnostic Logs

> [!NOTE]

> Application groups are available only in **premium** and **dedicated** tiers.

## Create an application group

This section shows you how to create an application group using Azure portal, CLI, PowerShell, and an Azure Resource Manager (ARM) template.

### [Azure portal](#tab/portal)

You can create an application group using the Azure portal by following these steps.

1. Navigate to your Event Hubs namespace.

1. On the left menu, select **Application Groups** under **Settings**.

1. On the **Application Groups** page, select **+ Application Group** on the command bar.

1. On the **Add application group** page, follow these steps:

1. Specify a **name** for the application group.

1. Confirm that **Enabled** is selected. To have the application group in the disabled state first, clear the **Enabled** option. This flag determines whether the clients of an application group can access Event Hubs or not.

1. For **Security context type**, select **Namespace Shared access policy**, **event hub Shared Access Policy** or **Microsoft Entra application**.Application group supports the selection of SAS key at either namespace or at entity (event hub) level. When you create the application group, you should associate with either a shared access signatures (SAS) or Microsoft Entra application ID, which is used by client applications.

1. If you selected **Namespace Shared access policy**:

1. For **SAS key name**, select the SAS policy that can be used as a security context for this application group. You can select **Add SAS Policy** to add a new policy and then associate with the application group.

1. If you selected **Event Hubs Shared access policy**:

1. For **SAS key name**, copy the SAS policy name from Event Hubs "Shared Access Policies" Page and paste into textbox

1. If you selected **Microsoft Entra application**:

1. For **Microsoft Entra Application (client) ID**, specify the Microsoft Entra application or client ID.

### [Supported Security Context type](#supported-security-context-type)

Review the auto-generated **Client group ID**, which is the unique ID associated with the application group. The scope of application governance (namespace or entity level) would depend on the access level for the used Microsoft Entra application ID. The following table  shows auto generated Client Group ID for different security Context type:

| Security Context type | Auto-generated client group ID|

| ---| ---		|

| Namespace shared access key	| `NamespaceSASKeyName=<NamespaceLevelKeyName>` |

| Microsoft Entra Application		| `AADAppID=<AppID>`				|

| Event Hubs shared access key 	| `EntitySASKeyName=<EntityLevelKeyName>` 	|

> [!NOTE]

> All existing application groups created with namespace shared access key would continue to work with client group ID starting with `SASKeyName`. However all new application groups would have updated client group ID as shown above.

1. To add a policy, follow these steps:

1. Enter a **name** for the policy.

1. For **Type**, select **Throttling policy**.

1. For **Metric ID**, select one of the following options: **Incoming messages**, **Outgoing messages**, **Incoming bytes**, **Outgoing bytes**. In the following example, **Incoming messages** is selected.

1. For **Rate limit threshold**, enter the threshold value. In the following example, **10000** is specified as the threshold for the number of incoming messages.

Here's a screenshot of the page with another policy added.

1. Now, on the **Add application group** page, select **Add**.

1. Confirm that you see the application group in the list of application groups.

You can delete the application group in the list by selecting the trash icon button next to it in the list.

### [Azure CLI](#tab/cli)

Use the CLI command: [`az eventhubs namespace application-group create`](/cli/azure/eventhubs/namespace/application-group#az-eventhubs-namespace-application-group-create) to create an application group at Event Hubs namespace or event hub level. You must set --client-app-group-identifier based on the security

context type you are choosing. Please review the [table](#supported-security-context-type) above to know supported Security context type

The following example creates an application group named `myAppGroup` in the namespace `mynamespace` in the Azure resource group `MyResourceGroup`. It uses the following configurations.

- Shared access policy is used as the security context

- Client app group ID is set to `NamespaceSASKeyName=<NameOfTheSASkey>`.

- First throttling policy for the `Incoming messages` metric with `10000` as the threshold.

- Second throttling policy for the `Incoming bytes` metric with `20000` as the threshold.

```azurecli-interactive

az eventhubs namespace application-group create --namespace-name mynamespace \

-g MyResourceGroup \

--name myAppGroup \

--client-app-group-identifier NamespaceSASKeyName=keyname \

--throttling-policy-config name=policy1 metric-id=IncomingMessages rate-limit-threshold=10000 \

--throttling-policy-config name=policy2 metric-id=IncomingBytes rate-limit-threshold=20000

```

To learn more about the CLI command, see [`az eventhubs namespace application-group create`](/cli/azure/eventhubs/namespace/application-group#az-eventhubs-namespace-application-group-create).

### [Azure PowerShell](#tab/powershell)

Use the PowerShell command: [`New-AzEventHubApplicationGroup`](/powershell/module/az.eventhub/new-azeventhubapplicationgroup) to create an application group  at Event Hubs namespace or event hub level. You must set -ClientAppGroupIdentifier based on the security

context type you are choosing. Please review the [table](#supported-security-context-type) above to know supported Security context type

The following example uses the [`New-AzEventHubThrottlingPolicyConfig`](/powershell/module/az.eventhub/new-azeventhubthrottlingpolicyconfig) to create two policies that will be associated with the application.

- First throttling policy for the `Incoming bytes` metric with `12345` as the threshold.

- Second throttling policy for the `Incoming messages` metric with `23416` as the threshold.

Then, it creates an application group named `myappgroup` in the namespace `mynamespace` in the Azure resource group `myresourcegroup` by specifying the throttling policies and shared access policy as the security context.

```azurepowershell-interactive

$policy1 = New-AzEventHubThrottlingPolicyConfig -Name policy1 -MetricId IncomingBytes -RateLimitThreshold 12345

$policy2 = New-AzEventHubThrottlingPolicyConfig -Name policy2 -MetricId IncomingMessages -RateLimitThreshold 23416

New-AzEventHubApplicationGroup -ResourceGroupName myresourcegroup -NamespaceName mynamespace -Name myappgroup

-ClientAppGroupIdentifier NamespaceSASKeyName=myauthkey -ThrottlingPolicyConfig $policy1, $policy2

```

To learn more about the PowerShell command, see [`New-AzEventHubApplicationGroup`](/powershell/module/az.eventhub/new-azeventhubapplicationgroup).

### [ARM template](#tab/arm)

The following example shows how to create an application group using an ARM template. In this example, the application group is associated with an existing SAS policy name `contososaspolicy` by setting the client `AppGroupIdentifier` as `NamespaceSASKeyName=contososaspolicy`. The application group policies are also defined in the ARM template. You must set ClientAppGroupIdentifier based on the security context type you are choosing. Please review the [table](#supported-security-context-type) above to know supported Security context type

```json

{

"type": "ApplicationGroups",

"apiVersion": "2022-01-01-preview",

"name": "[parameters('applicationGroupName')]",

"dependsOn": [

"[resourceId('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]",

"[resourceId('Microsoft.EventHub/namespaces/authorizationRules', parameters('eventHubNamespaceName'),parameters('namespaceAuthorizationRuleName'))]"

],

"properties": {

"ClientAppGroupIdentifier": "NamespaceSASKeyName=contososaspolicy",

"policies": [{

"Type": "ThrottlingPolicy",

"Name": "ThrottlingPolicy1",

"metricId": "IncomingMessages",

"rateLimitThreshold": 10

},

{

"Type": "ThrottlingPolicy",

"Name": "ThrottlingPolicy2",

"metricId": "IncomingBytes",

"rateLimitThreshold": 3951729

}

],

"isEnabled": true

}

}

```

---

## Enable or disable an application group

You can prevent client applications accessing your Event Hubs namespace by disabling the application group that contains those applications. When the application group is disabled, client applications won't be able to publish or consume data. Any established connections from client applications of that application group will also be terminated.

This section shows you how to enable or disable an application group using Azure portal, PowerShell, CLI, and ARM template.

### [Azure portal](#tab/portal)

1. On the **Event Hubs Namespace** page, select **Application Groups** on the left menu.

1. Select the application group that you want to enable or disable.

1. On the **Edit application group** page, clear checkbox next to **Enabled** to disable an application group, and then select **Update** at the bottom of the page. Similarly, select the checkbox to enable an application group.

### [Azure CLI](#tab/cli)

Use the [`az eventhubs namespace application-group update`](/cli/azure/eventhubs/namespace/application-group#az-eventhubs-namespace-application-group-update) command with `--is-enabled` set to `false` to disable an application group. Similarly, to enable an application group, set this property to `true` and run the command.

The following sample command disables the application group named `myappgroup` in the Event Hubs namespace `mynamespace` that's in the resource group `myresourcegroup`.

```azurecli-interactive

az eventhubs namespace application-group update --namespace-name mynamespace -g myresourcegroup --name myappgroup --is-enabled false

```

### [Azure PowerShell](#tab/powershell)

Use the [Set-AzEventHubApplicationGroup](/powershell/module/az.eventhub/set-azeventhubapplicationgroup) command with `-IsEnabled` set to `false` to disable an application group. Similarly, to enable an application group, set this property to `true` and run the command.

The following sample command disables the application group named `myappgroup` in the Event Hubs namespace `mynamespace` that's in the resource group `myresourcegroup`.

```azurepowershell-interactive

Set-AzEventHubApplicationGroup -ResourceGroupName myresourcegroup -NamespaceName mynamespace -Name myappgroup -IsEnabled false

```

### [ARM template](#tab/arm)

The following ARM template shows how to update an existing namespace (`contosonamespace`) to disable an application group by setting the `isEnabled` property to `false`. The identifier for the app group is `SASKeyName=RootManageSharedAccessKey`.

> [!NOTE]

> The following sample also adds two throttling policies

```json

{

"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"namespace_name": {

"defaultValue": "contosonamespace",

"type": "String"

},

"client-app-group-identifier": {

"defaultValue": "SASKeyName=RootManageSharedAccessKey",

"type": "String"

}

},

"resources": [

{

"type": "Microsoft.EventHub/namespaces/applicationGroups",

"apiVersion": "2022-01-01-preview",

"name": "[concat(parameters('namespace_name'), '/contosoappgroup')]",

"properties": {

"clientAppGroupIdentifier": "[parameters('client-app-group-identifier')]",

"isEnabled": false,

"policies": [

{

"type": "ThrottlingPolicy",

"name": "incomingmsgspolicy",

"metricId": "IncomingMessages",

"rateLimitThreshold": 10000

},

{

"type": "ThrottlingPolicy",

"name": "incomingbytespolicy",

"metricId": "IncomingBytes",

"rateLimitThreshold": 20000

}

]

}

}

]

}

```

---

## Apply throttling policies

You can add zero or more policies when you create an application group or to an existing application group. For example, you can add throttling policies related to `IncomingMessages`, `IncomingBytes` or `OutgoingBytes` to the `contosoAppGroup`. These policies will get applied to event streaming workloads of client applications that use the SAS policy `contososaspolicy`.

To learn how to add policies while creating an application group, see the [Create an application group](#create-an-application-group) section.

You can also add policies after an application group is created.

### [Azure portal](#tab/portal)

1. On the **Event Hubs Namespace** page, select **Application Groups** on the left menu.

1. Select the application group that you want to add, update, or delete a policy.

1. On the **Edit application group** page, you can do the following steps:

1. Update settings (including threshold values) for existing policies

1. Add a new policy

### [Azure CLI](#tab/cli)

Use the [`az eventhubs namespace application-group policy add`](/cli/azure/eventhubs/namespace/application-group/policy#az-eventhubs-namespace-application-group-policy-add) to add a policy to an existing application group.

**Example:**

```azurecli-interactive

az eventhubs namespace application-group policy add --namespace-name mynamespace -g MyResourceGroup --name myAppGroup --throttling-policy-config name=policy1 metric-id=OutgoingMessages rate-limit-threshold=10500 --throttling-policy-config name=policy2 metric-id=IncomingBytes rate-limit-threshold=20000

```

### [Azure PowerShell](#tab/powershell)

Use the [Set-AzEventHubApplicationGroup](/powershell/module/az.eventhub/set-azeventhubapplicationgroup) command with `-ThrottlingPolicyConfig` set to appropriate values.

**Example:**

```azurepowershell-interactive

$policyToBeAppended = New-AzEventHubThrottlingPolicyConfig -Name policy1 -MetricId IncomingBytes -RateLimitThreshold 12345

$appGroup = Get-AzEventHubApplicationGroup -ResourceGroupName myresourcegroup -NamespaceName mynamespace -Name myappgroup

$appGroup.ThrottlingPolicyConfig += $policyToBeAppended

Set-AzEventHubApplicationGroup -ResourceGroupName myresourcegroup -NamespaceName mynamespace -Name myappgroup -ThrottlingPolicyConfig $appGroup.ThrottlingPolicyConfig

```

### [ARM template](#tab/arm)

The following ARM template shows how to update an existing namespace (`contosonamespace`) to add throttling policies. The identifier for the app group is `NamespaceSASKeyName=RootManageSharedAccessKey`.

```json

{

"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"namespace_name": {

"defaultValue": "contosonamespace",

"type": "String"

},

"client-app-group-identifier": {

"defaultValue": "NamespaceSASKeyName=RootManageSharedAccessKey",

"type": "String"

}

},

"resources": [

{

"type": "Microsoft.EventHub/namespaces/applicationGroups",

"apiVersion": "2022-01-01-preview",

"name": "[concat(parameters('namespace_name'), '/contosoappgroup')]",

"properties": {

"clientAppGroupIdentifier": "[parameters('client-app-group-identifier')]",

"isEnabled": true,

"policies": [

{

"type": "ThrottlingPolicy",

"name": "incomingmsgspolicy",

"metricId": "IncomingMessages",

"rateLimitThreshold": 10000

},

{

"type": "ThrottlingPolicy",

"name": "incomingbytespolicy",

"metricId": "IncomingBytes",

"rateLimitThreshold": 20000

}

]

}

}

]

}

```

---

### Decide threshold value for throttling policies

Azure Event Hubs supports [Application Metric Logs](monitor-event-hubs-reference.md#application-metrics-logs) functionality to observe usual throughput within your system and accordingly decide on the threshold value for application group. You can follow these steps to decide on a threshold value:

1. Turn on [diagnostic settings](/azure/azure-monitor/essentials/diagnostic-settings) in Event Hubs with **Application Metric logs** as selected category and choose **Log Analytics** as destination.

2. Create an empty application group without any throttling policy.

3. Continue sending messages/events to event hub at usual throughput.

4. Go to **Log Analytics workspace** and query for the right activity name (based on the (resource-governance-overview.md#throttling-policy---threshold-limits)) in **AzureDiagnostics** table. The following sample query is set to track threshold value for incoming messages:

```kusto

AzureDiagnostics

| where ActivityName_s =="IncomingMessages"

| where Outcome_s =="Success"

```

5. Select the **Chart** section on Log Analytics workspace and plot a chart between time generated on Y axis and count of messages sent on x axis.

In this example, you can see that the usual throughput never crossed more than 550 messages (expected current throughput). This observation helps you define the actual threshold value.

6. Once you decide the threshold value, add a new throttling policy inside the application group.

## Publish or consume events

Once you successfully add throttling policies to the application group, you can test the throttling behavior by either publishing or consuming events using client applications that are part of the `contosoAppGroup` application group. To test, you can use either an [AMQP client](event-hubs-dotnet-standard-getstarted-send.md) or a [Kafka client](event-hubs-quickstart-kafka-enabled-event-hubs.md) application and same SAS policy name or Microsoft Entra application ID that's used to create the application group.

> [!NOTE]

> When your client applications are throttled, you should experience a slowness in publishing or consuming data.

### Validate Throttling with Application Groups

Similar to [Deciding Threshold limits for Throttling Policies](resource-governance-with-app-groups.md#decide-threshold-value-for-throttling-policies), you can use Application Metric logs to validate throttling and find more details.

You can use the below example query to find out all the throttled requests in certain timeframe. You must update the ActivityName to match the operation that you expect to be throttled.

```kusto

AzureDiagnostics

|  where Category =="ApplicationMetricsLogs"

| where ActivityName_s =="IncomingMessages"

| where Outcome_s =="Throttled"

```

Due to restrictions at protocol level, throttled request logs are not generated for consumer operations within event hub ( `OutgoingMessages` or `OutgoingBytes`). When requests are throttled at consumer side, you would observe sluggish egress throughput.

## Next steps

- For conceptual information on application groups, see [Resource governance with application groups](resource-governance-overview.md).

- See [Azure PowerShell reference for Event Hubs](/powershell/module/az.eventhub#event-hub)

- See [Azure CLI reference for Event Hubs](/cli/azure/eventhubs)


# Configure Event Hub Properties

# Configure properties for an event hub

This article shows you how to configure properties such as status, partition count, retention time, etc. for an event hub.

## Configure status

You can update the status of an event hub to one of these values on the **Properties** page after the event hub is created.

- Select **Active** (default) if you want to send events to and receive events from an event hub.

- Select **Disabled** if you want to disable both sending and receiving events from an event hub.

- Select **SendDisabled** if you want to disable sending events to an event hub.

## Configure partition count

The **Properties** page allows you to see the number of partitions in an event hub for event hubs in all tiers. It allows you to update the partition count for event hubs in a premium or dedicated tier. For other tiers, you can only specify the partition count at the time of creating an event hub. To learn about partitions in Event Hubs, see [Scalability](event-hubs-scalability.md#partitions)

### Configure cleanup policy

You see the cleanup policy for an event hub on the **Properties** page. You can't update it. By default, an event hub is created with the **delete** cleanup policy, where events are purged upon the expiration of the retention time. While creating an event hub, you can set the cleanup policy to **Compact**. For more information, see [Log compaction](log-compaction.md) and [Configure log compaction](use-log-compaction.md).

## Configure retention time

If the cleanup policy is set to **Delete**, the **retention time** is the maximum time that Event Hubs retains an event before discarding the event. The **Properties** page allows you to specify retention time in hours.

If the cleanup policy is set to **Compact** at the time of creating an event hub, the **infinite retention time** is automatically enabled. You can set the **Tombstone retention time in hours** though. Client applications can mark existing events of an event hub to be deleted during a compaction job by sending a new event with an existing key and a `null` event payload. These markers are known as **Tombstones**. The **Tombstone retention time in hours** is the time to retain tombstone markers in a compacted event hub.

## Azure CLI

Use the [`az eventhubs eventhub update`](/cli/azure/eventhubs/eventhub#az-eventhubs-eventhub-update) command to configure partition count and retention settings for an event hub.

- Use the `--status` parameter to set the status of an existing event hub to `Active`, `Disabled`, or `SendDisabled` or `ReceiveDisabled`.

- Use `--partition-count` parameter to specify the number of partitions. You can specify the partition count for an existing event hub only if it's in the premium or dedicated tier namespace.

- Use the `--retention-time` to specify the number of hours to retain events for an event hub, if the `cleanupPolicy` is `Delete`.

- Use the `--tombstone-retention-time-in-hours` to specify the number of hours to retain the tombstone markers, if the `cleanupPolicy` is `Compact`.

## Azure PowerShell

Use the [`Set-AzEventHub`](/powershell/module/az.eventhub/set-azeventhub) by using the `-Status`, `-RetentionTimeInHour` or `TomstoneRetentionTimeInHour` parameters. Currently, the PowerShell command doesn't support updating the partition count for an event hub.

## Azure Resource Manager template

If you're using an Azure Resource Manager template, use the `partitionCount` and `retentionTimeinHours` as shown in the following example. `MYNAMESPACE` is the name of the Event Hubs namespace and `MYEVENTHUB` is the name of the event hub in this example.

```json

{

"type": "Microsoft.EventHub/namespaces/eventhubs",

"apiVersion": "2022-10-01-preview",

"name": "MYNAMESPACE/MYEVENTHUB ",

"properties": {

"partitionIds": [],

"partitionCount": 1,

"captureDescription": null,

"retentionDescription": {

"cleanupPolicy": "Delete",

"retentionTimeInHours": 1

}

}

}

```

## Next steps

See the following articles:

- [Scalability](event-hubs-scalability.md#partitions)

- [Log compaction](log-compaction.md) and [Configure log compaction](use-log-compaction.md)-


# Event Hubs Auto Inflate

# Auto inflate in Azure Event Hubs (standard tier)

The Auto inflate feature of Azure Event Hubs automatically scales up throughput units (TUs) based on your workload, so you don't have to manually adjust capacity as traffic increases. If your workload has variable traffic patterns, Auto inflate eliminates the need to monitor and manually adjust throughput capacity.

> [!NOTE]

> The Auto inflate feature is currently supported only in the standard tier.

## How Auto inflate works

Event Hubs traffic is controlled by TUs (standard tier). For the limits such as ingress and egress rates per TU, see [Event Hubs quotas and limits](event-hubs-quotas.md). Auto inflate enables you to start small with the minimum required TUs you choose. The feature then scales automatically to the maximum limit of TUs you need, depending on the increase in your traffic. Auto inflate provides the following benefits:

- An efficient scaling mechanism to start small and scale up as you grow.

- Automatically scale to the specified upper limit without throttling issues.

- More control over scaling, because you control when and how much to scale.

> [!NOTE]

> Auto inflate doesn't **automatically scale down** the number of TUs when ingress or egress rates drop below the limits.

## Pricing considerations

With Auto inflate enabled, you can start small with your TUs and scale up as your usage needs increase. The upper limit for inflation doesn't immediately affect pricing, which depends on the number of TUs used per hour.

## Related content

- [Enable Auto inflate for an Event Hubs namespace](enable-auto-inflate.md)

- [Event Hubs quotas and limits](event-hubs-quotas.md)

- [Event Hubs overview](event-hubs-about.md)


# Enable Auto Inflate

# Enable Auto inflate for an Event Hubs namespace

The Auto inflate feature automatically scales throughput units (TUs) for your Event Hubs namespace based on traffic demand. This article shows you how to enable Auto inflate using the Azure portal or an Azure Resource Manager (ARM) template.

For information about how Auto inflate works, see [Auto inflate in Azure Event Hubs](event-hubs-auto-inflate.md).

## Prerequisites

- An Azure subscription. If you don't have one, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- A standard tier Event Hubs namespace (Auto inflate isn't supported in the basic tier).

## Enable Auto inflate using the Azure portal

You can enable Auto inflate when you create a namespace or on an existing namespace.

### Enable Auto inflate during namespace creation

1. In the [Azure portal](https://portal.azure.com), select **Create a resource** > **Integration** > **Event Hubs**.

1. On the **Create Namespace** page, enter the namespace details and select **Standard** for the pricing tier.

1. Under **Throughput units**, select the **Enable** checkbox for Auto inflate.

1. Set the initial number of throughput units and the maximum limit.

1. Select **Review + create**, and then select **Create**.

### Enable Auto inflate on an existing namespace

1. In the [Azure portal](https://portal.azure.com), go to your Event Hubs namespace.

1. Under **Settings** in the left menu, select **Scale**.

1. In the **Scale Settings** page, select the **Enable** checkbox (if Auto inflate isn't already enabled).

1. Enter the **maximum** number of throughput units or use the scrollbar to set the value.

1. (Optional) Update the **minimum** number of throughput units at the top of this page.

1. Select **Save**.

> [!NOTE]

> When you apply the Auto inflate configuration, the Event Hubs service emits diagnostic logs that provide information about why and when the throughput increased. To enable diagnostic logging, select **Diagnostic settings** in the left menu of the Event Hub page. For more information, see [Set up diagnostic logs for an Azure event hub](monitor-event-hubs-reference.md#resource-logs).

## Enable Auto inflate using an ARM template

You can enable Auto inflate during an ARM template deployment by setting the `isAutoInflateEnabled` property to `true` and specifying the `maximumThroughputUnits` value.

The following example template creates a standard tier namespace with Auto inflate enabled and a maximum of 10 throughput units:

```json

{

"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"namespaceName": {

"defaultValue": "fabrikamehubns",

"type": "String"

}

},

"variables": {},

"resources": [

{

"type": "Microsoft.EventHub/namespaces",

"apiVersion": "2022-10-01-preview",

"name": "[parameters('namespaceName')]",

"location": "East US",

"sku": {

"name": "Standard",

"tier": "Standard",

"capacity": 1

},

"properties": {

"minimumTlsVersion": "1.2",

"publicNetworkAccess": "Enabled",

"disableLocalAuth": false,

"zoneRedundant": true,

"isAutoInflateEnabled": true,

"maximumThroughputUnits": 10,

"kafkaEnabled": true

}

}

]

}

```

For the complete template, see the [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.eventhub/eventhubs-create-namespace-and-enable-inflate) template on GitHub.

## Related content

- [Auto inflate in Azure Event Hubs](event-hubs-auto-inflate.md)

- [Event Hubs quotas and limits](event-hubs-quotas.md)

- [Event Hubs overview](event-hubs-about.md)


# Event Hubs Management Libraries

# Event Hubs management libraries

You can use the Azure Event Hubs management libraries to dynamically provision Event Hubs namespaces and entities. This dynamic nature enables complex deployments and messaging scenarios, so that you can programmatically determine what entities to provision. These libraries are currently available for .NET.

## Supported functionality

* Namespace creation, update, deletion

* Event Hubs creation, update, deletion

* Consumer Group creation, update, deletion

## Prerequisites

To get started using the Event Hubs management libraries, you must authenticate with Microsoft Entra ID. Microsoft Entra ID requires that you authenticate as a service principal, which provides access to your Azure resources. For information about creating a service principal, see one of these articles:

* [Use the Azure portal to create Active Directory application and service principal that can access resources](../active-directory/develop/howto-create-service-principal-portal.md)

* [Use Azure PowerShell to create a service principal to access resources](../active-directory/develop/howto-authenticate-service-principal-powershell.md)

* [Use Azure CLI to create a service principal to access resources](/cli/azure/create-an-azure-service-principal-azure-cli)

These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries. The Microsoft Entra application must be added to the **Azure Event Hubs Data Owner** role at the resource group level.

## Sample code

The pattern to manipulate any Event Hubs resource follows a common protocol:

1. Obtain a token from Microsoft Entra ID using the `Microsoft.Identity.Client` library.

1. Create the `EventHubManagementClient` object.

1. Then, use the client object to create an Event Hubs namespace and an event hub.

Here's the sample code to create an Event Hubs namespace and an event hub.

```csharp

namespace event_hub_dotnet_management

{

using System;

using System.Threading.Tasks;

using Microsoft.Azure.ResourceManager.EventHubs;

using Microsoft.Azure.ResourceManager.EventHubs.Models;

using Microsoft.Identity.Client;

using Microsoft.Rest;

public static class EventHubManagementSample

{

private static string resourceGroupName = "<YOUR EXISTING RESOURCE GROUP NAME>";

private static string namespaceName = "<EVENT HUBS NAMESPACE TO BE CREATED>";

private const string eventHubName = "<EVENT HUB TO BE CREATED>";

private const string location = "<REGION>"; //for example: "eastus"

public static async Task Main()

{

// get a token from Microsoft Entra ID

var token = await GetToken();

// create an EventHubManagementClient

var creds = new TokenCredentials(token);

var ehClient = new EventHubManagementClient(creds)

{

SubscriptionId = "<AZURE SUBSCRIPTION ID>"

};

// create an Event Hubs namespace using the EventHubManagementClient

await CreateNamespace(ehClient);

// create an event hub using the EventHubManagementClient

await CreateEventHub(ehClient);

Console.WriteLine("Press a key to exit.");

Console.ReadLine();

}

// Get an authentication token from Azure AD first

private static async Task<string> GetToken()

{

try

{

Console.WriteLine("Acquiring token...");

var tenantId = "<AZURE TENANT ID>";

// use the Azure AD app that's a member of Azure Event Hubs Data Owner role at the resource group level

var clientId = "<AZURE APPLICATION'S CLIENT ID>";

var clientSecret = "<CLIENT SECRET>";

IConfidentialClientApplication app;

app = ConfidentialClientApplicationBuilder.Create(clientId)

.WithClientSecret(clientSecret)

.WithAuthority($"https://login.microsoftonline.com/{tenantId}")

.Build();

var result = await app.AcquireTokenForClient(new[] { $"https://management.core.windows.net/.default" })

.ExecuteAsync()

.ConfigureAwait(false);

// If the token isn't a valid string, throw an error.

if (string.IsNullOrEmpty(result.AccessToken))

{

throw new Exception("Token result is empty!");

}

return result.AccessToken;

}

catch (Exception e)

{

Console.WriteLine("Could not get a new token...");

Console.WriteLine(e.Message);

throw e;

}

}

// Create an Event Hubs namespace

private static async Task CreateNamespace(EventHubManagementClient ehClient)

{

try

{

Console.WriteLine("Creating namespace...");

await ehClient.Namespaces.CreateOrUpdateAsync(resourceGroupName, namespaceName, new EHNamespace { Location = location });

Console.WriteLine("Created namespace successfully.");

}

catch (Exception e)

{

Console.WriteLine("Could not create a namespace...");

Console.WriteLine(e.Message);

}

}

// Create an event hub

private static async Task CreateEventHub(EventHubManagementClient ehClient)

{

try

{

Console.WriteLine("Creating Event Hub...");

await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, eventHubName, new Eventhub());

Console.WriteLine("Created Event Hub successfully.");

}

catch (Exception e)

{

Console.WriteLine("Could not create an Event Hub...");

Console.WriteLine(e.Message);

}

}

}

}

```

## Next steps

* [.NET Management sample](https://github.com/Azure-Samples/event-hubs-dotnet-management/)

* [Microsoft.Azure.Management.EventHub Reference](/dotnet/api/Microsoft.Azure.Management.EventHub)


# Use Geo Replication

# How to use Geo-replication

This tutorial shows you how to use the Geo-replication with Event Hubs. To learn more about this feature, see [Geo-replication](./geo-replication.md). In this article you learn how to:

-	Enable Geo-replication on a new namespace.

-	Enable Geo-replication on an existing namespace.

-	Perform a planned promotion or failover.

-	Remove the secondary from your namespace.

## Enable Geo-replication on a new namespace

### [Dedicated](#tab/Dedicated)

> [!NOTE]

> To use geo-replication feature, at least one Dedicated Event Hubs cluster is needed in each region where Geo-replication feature is available.

>

1. Navigate to the **Event Hubs Cluster** page for your Event Hubs cluster. Expand **Entities**, and select **Cluster Namespaces**.

2. To create an Event Hubs namespace in an Event Hubs cluster in a region with Geo-replication enabled, on the **Cluster Namespaces** page, on the toolbar, select **+ Namespace**. Provide a name for the namespace, and select **Enable Geo-replication**.

### [Premium](#tab/Premium)

1. Follow the steps to create an Event Hubs namespace as listed [here](event-hubs-create.md) and pick the `Premium` tier.

2. Provide a name for the namespace, and select **Enable Geo-replication**.

---

3. Select **Add secondary region**, and select a secondary region and a corresponding Event Hubs dedicated cluster running in that region.

4. Select asynchronous or synchronous **replication mode** as the replication consistency mode. If you select asynchronous consistency, enter the allowable amount of time the secondary region can lag behind the primary region in minutes.

5. Then, select **Create** to create the Geo-replicated Event Hubs namespace. The deployment takes a couple of minutes to complete.

6. Once the namespace is created, you can navigate to it and select **Geo-replication** on the left menu to see your Geo-replication configuration.

## Enable Geo-replication on an existing namespace

1. Navigate to your Event Hubs namespace in the Azure portal, and select **Geo-replication** on the left menu.

2. Select **Add secondary region**, and select a secondary region and the corresponding Event Hubs Dedicated clusters running in that region.

3. Select asynchronous or synchronous replication mode as the replication consistency mode. If selecting asynchronous consistency, enter the allowable amount of time the secondary region can lag behind the primary region in minutes.

After a secondary region is added, all of the data held in the primary namespace is replicated to the secondary. Complete replication can take a while depending on various factors with the main one being how much data is in your primary namespace. Users can observe replication progress by monitoring the lag to the secondary region.

## Promote secondary

You can promote your configured secondary region to being the primary region. When you promote a secondary region to primary, the current primary region becomes the secondary region. A promotion can be planned or forced. Planned promotions ensure both regions are caught up before accepting new traffic. Forced promotions take effect as quickly as possible and doesn't wait for things to be caught up.

To initiate a promotion of your secondary region to primary, select failover icon.

When in the promotion flow, you can select planned or forced. You can also choose to select forced after starting a planned promotion. Enter the word **promote** in the prompt to be able to start the promotion.

If doing a planned promotion, then once the promotion process is initiated, the new primary rejects any new events until failover is completed. The promotion process repoints the fully qualified domain name(FQDN) for your namespace to the selected region, complete data replication between the two regions and configure the new primary region to be active. Promotion doesn't require any changes to clients, and that they continue to work after the promotion event.

In the case where your primary region goes down completely, you can still perform a forced promotion.

## Switch replication mode

To switch between replication modes, or update the maximum replication lag, click on the link under **Replication consistency**, and click the checkbox to enable / disable synchronous replication, or update the value in the textbox to change the asynchronous maximum replication lag.

## Remove a secondary

To remove a Geo-replication pairing with a secondary, select **Geo-replication** on the left menu, select the secondary region, and then select **Remove**. At the prompt, enter the word **delete**, and then you can delete the secondary.

When a secondary region is removed, all of the data that it held is also removed. If you wish to re-enable Geo-replication with that region and cluster, it has to replicate the primary region data all over again.

## Related content

For conceptual information about the Geo-replication feature, see [Azure Event Hubs geo-replication](geo-replication.md).


# Monitor Event Hubs

# Monitor Azure Event Hubs

[!INCLUDE [horz-monitor-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-intro.md)]

Azure Monitor documentation describes the following concepts:

- What is Azure Monitor?

- Costs associated with monitoring

- Monitoring data collected in Azure

- Configuring data collection

- Standard tools in Azure for analyzing and alerting on monitoring data

The following sections describe the specific data gathered for Azure Event Hubs. These sections also provide examples for configuring data collection and analyzing this data with Azure tools.

> [!TIP]

> To understand costs associated with Azure Monitor, see [Azure Monitor cost and usage](/azure/azure-monitor/cost-usage). To understand the time it takes for your data to appear in Azure Monitor, see [Log data ingestion time](/azure/azure-monitor/logs/data-ingestion-time).

[!INCLUDE [horz-monitor-resource-types](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-resource-types.md)]

For more information about the resource types for Event Hubs, see [Azure Event Hubs monitoring data reference](monitor-event-hubs-reference.md).

[!INCLUDE [horz-monitor-data-storage](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-data-storage.md)]

- Azure Storage

If you use Azure Storage to store the diagnostic logging information, the information is stored in containers named *insights-logs-operationlogs* and *insights-metrics-pt1m*. Sample URL for an operation log: `https://<Azure Storage account>.blob.core.windows.net/insights-logs-operationallogs/resourceId=/SUBSCRIPTIONS/<Azure subscription ID>/RESOURCEGROUPS/<Resource group name>/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/<Namespace name>/y=<YEAR>/m=<MONTH-NUMBER>/d=<DAY-NUMBER>/h=<HOUR>/m=<MINUTE>/PT1H.json`. The URL for a metric log is similar.

- Azure Event Hubs

If you use Azure Event Hubs to store the diagnostic logging information, the information is stored in Event Hubs instances named *insights-logs-operationlogs* and *insights-metrics-pt1m*. You can also select an existing event hub except for the event hub for which you're configuring diagnostic settings.

- Log Analytics

If you use Log Analytics to store the diagnostic logging information, the information is stored in tables named *AzureDiagnostics / AzureMetrics* or resource specific tables.

> [!IMPORTANT]

> Enabling these settings requires additional Azure services: storage account, event hub, or Log Analytics. These services might increase your cost. To calculate an estimated cost, visit the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator).

> [!NOTE]

> When you enable metrics in a diagnostic setting, dimension information isn't currently included as part of the information sent to a storage account, event hub, or log analytics.

[!INCLUDE [horz-monitor-platform-metrics](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-platform-metrics.md)]

Resource Logs aren't collected and stored until you create a diagnostic setting and route them to one or more locations. When you create a diagnostic setting, you specify which categories of logs to collect. The categories for Azure Event Hubs are listed in [Azure Event Hubs monitoring data reference](monitor-event-hubs-reference.md#resource-logs).

> [!NOTE]

> Azure Monitor doesn't include dimensions in the exported metrics data that's sent to a destination like Azure Storage, Azure Event Hubs, and Log Analytics.

For a list of available metrics for Event Hubs, see [Azure Event Hubs monitoring data reference](monitor-event-hubs-reference.md#metrics).

### Analyze metrics

You can analyze metrics for Azure Event Hubs, along with metrics from other Azure services, by selecting **Metrics** from the **Azure Monitor** section on the home page for your Event Hubs namespace. See [Analyze metrics with Azure Monitor metrics explorer](/azure/azure-monitor/essentials/analyze-metrics) for details on using this tool. For a list of the platform metrics collected, see [Monitoring Azure Event Hubs data reference metrics](monitor-event-hubs-reference.md#metrics).

For reference, you can see a list of [all resource metrics supported in Azure Monitor](/azure/azure-monitor/essentials/metrics-supported).

> [!TIP]

> Azure Monitor metrics data is available for 90 days. However, when creating charts only 30 days can be visualized. For example, if you want to visualize a 90 day period, you must break it into three charts of 30 days within the 90 day period.

### Filter and split

For metrics that support dimensions, you can apply filters using a dimension value. For example, add a filter with `EntityName` set to the name of an event hub. You can also split a metric by dimension to visualize how different segments of the metric compare with each other. For more information of filtering and splitting, see [Advanced features of Azure Monitor](/azure/azure-monitor/essentials/metrics-charts).

[!INCLUDE [horz-monitor-resource-logs](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-resource-logs.md)]

For the available resource log categories, their associated Log Analytics tables, and the log schemas for Event Hubs, see [Azure Event Hubs monitoring data reference](monitor-event-hubs-reference.md#resource-logs).

### Analyze logs

Using Azure Monitor Log Analytics requires you to create a diagnostic configuration and enable **Send information to Log Analytics**. For more information, see the [Metrics](#azure-monitor-platform-metrics) section. Data in Azure Monitor Logs is stored in tables, with each table having its own set of unique properties. Azure Event Hubs has the capability to dispatch logs to either of two destination tables: Azure Diagnostic or Resource specific tables in Log Analytics. For a detailed reference of the logs and metrics, see [Azure Event Hubs monitoring data reference](monitor-event-hubs-reference.md).

> [!IMPORTANT]

> When you select **Logs** from the Azure Event Hubs menu, Log Analytics is opened with the query scope set to the current workspace. It means that log queries include only data from that resource. If you want to run a query that includes data from other databases or data from other Azure services, select **Logs** from the **Azure Monitor** menu. See [Log query scope and time range in Azure Monitor Log Analytics](/azure/azure-monitor/logs/scope) for details.

### Use runtime logs

Azure Event Hubs allows you to monitor and audit data plane interactions of your client applications using runtime audit logs and application metrics logs.

Using *Runtime audit logs* you can capture aggregated diagnostic information for all data plane access operations such as publishing or consuming events. *Application metrics logs* capture the aggregated data on certain runtime metrics (such as consumer lag and active connections) related to client applications are connected to Event Hubs.

> [!NOTE]

> Runtime audit logs are available only in **premium** and **dedicated** tiers.

### Enable runtime logs

You can enable either runtime audit or application metrics logging by selecting *Diagnostic settings* from the *Monitoring* section on the Event Hubs namespace page in Azure portal. Select **Add diagnostic setting** as shown in the following image.

Then you can enable log categories *RuntimeAuditLogs* or *ApplicationMetricsLogs* as needed.

Once runtime logs are enabled, Event Hubs start collecting and storing them according to the diagnostic setting configuration.

### Publish and consume sample data

To collect sample runtime audit logs in your Event Hubs namespace, you can publish and consume sample data using client applications that are based on the [Event Hubs SDK](../event-hubs/event-hubs-dotnet-standard-getstarted-send.md). That SDK uses Advanced Message Queuing Protocol (AMQP). Or you can use any [Apache Kafka client application](../event-hubs/event-hubs-quickstart-kafka-enabled-event-hubs.md).

Application metrics include the following runtime metrics.

Therefore you can use application metrics to monitor runtime metrics such as consumer lag or active connection from a given client application. Fields associated with runtime audit logs are defined in [application metrics logs reference](../event-hubs/monitor-event-hubs-reference.md#runtime-audit-logs).

[!INCLUDE [horz-monitor-activity-log](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-activity-log.md)]

[!INCLUDE [horz-monitor-analyze-data](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-analyze-data.md)]

[!INCLUDE [horz-monitor-external-tools](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-external-tools.md)]

[!INCLUDE [horz-monitor-kusto-queries](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-kusto-queries.md)]

### Sample Kusto queries

Following are sample queries that you can use to help you monitor your Azure Event Hubs resources:

### [AzureDiagnostics](#tab/AzureDiagnostics)

- Get errors from the past seven days.

```Kusto

AzureDiagnostics

| where TimeGenerated > ago(7d)

| where ResourceProvider =="MICROSOFT.EVENTHUB"

| where Category == "OperationalLogs"

| summarize count() by "EventName"

- Get runtime audit logs generated in the last one hour.

```Kusto

AzureDiagnostics

| where TimeGenerated > ago(1h)

| where ResourceProvider =="MICROSOFT.EVENTHUB"

| where Category == "RuntimeAuditLogs"

```

- Get access attempts to a key vault that resulted in "key not found" error.

```Kusto

AzureDiagnostics

| where ResourceProvider == "MICROSOFT.EVENTHUB"

| where Category == "Error" and OperationName == "wrapkey"

| project Message

```

- Get operations performed with a key vault to disable or restore the key.

```Kusto

AzureDiagnostics

| where ResourceProvider == "MICROSOFT.EVENTHUB"

| where Category == "info" and OperationName == "disable" or OperationName == "restore"

| project Message

```

- Get capture failures and their duration in seconds.

```kusto

AzureDiagnostics

| where ResourceProvider == "MICROSOFT.EVENTHUB"

| where Category == "ArchiveLogs"

| summarize count() by "failures", "durationInSeconds"

```

### [Resource Specific Table](#tab/Resourcespecifictable)

- Get Operational Logs for event hub resource for last seven days.

```Kusto

AZMSOperationalLogs

| where Timegenerated > ago(7d)

| where Provider == "EVENTHUB"

| where resourceId == "<Resource Id>" // Replace your resource Id

```

- Get capture logs for event hub for last seven days.

```Kusto

AZMSArchiveLogs

| where EventhubName == "<Event Hub Name>" //Enter event hub entity name

| where TimeGenerated > ago(7d)

```

---

### Analyze runtime audit logs

You can analyze the collected runtime audit logs using the following sample query.

### [AzureDiagnostics](#tab/AzureDiagnosticsforRuntimeAudit)

```kusto

AzureDiagnostics

| where TimeGenerated > ago(1h)

| where ResourceProvider == "MICROSOFT.EVENTHUB"

| where Category == "RuntimeAuditLogs"

```

### [Resource Specific Table](#tab/ResourcespecifictableforRuntimeAudit)

```kusto

AZMSRuntimeAuditLogs

| where TimeGenerated > ago(1h)

| where Provider == "EVENTHUB"

```

---

Up on the execution of the query you should be able to obtain corresponding audit logs in the following format.

By analyzing these logs, you should be able to audit how each client application interacts with Event Hubs. Each field associated with runtime audit logs is defined in [runtime audit logs reference](../event-hubs/monitor-event-hubs-reference.md#runtime-audit-logs).

### Analyze application metrics

You can analyze the collected application metrics logs using the following sample query.

### [AzureDiagnostics](#tab/AzureDiagnosticsforAppMetrics)

```kusto

AzureDiagnostics

| where TimeGenerated > ago(1h)

| where Category == "ApplicationMetricsLogs"

```

### [Resource Specific Table](#tab/ResourcespecifictableforAppMetrics)

```kusto

AZMSApplicationMetricLogs

| where TimeGenerated > ago(1h)

| where Provider == "EVENTHUB"

```

---

[!INCLUDE [horz-monitor-alerts](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-alerts.md)]

You can access alerts for Azure Event Hubs by selecting **Alerts** from the **Azure Monitor** section on the home page for your Event Hubs namespace. See [Create, view, and manage metric alerts using Azure Monitor](/azure/azure-monitor/alerts/alerts-metric) for details on creating alerts.

### Event Hubs alert rules

The following table lists some suggested alert rules for Event Hubs. These alerts are just examples. You can set alerts for any metric, log entry, or activity log entry listed in the [Azure Event Hubs monitoring data reference](monitor-event-hubs-reference.md).

| Alert type | Condition | Description  |

|:---|:---|:---|

| Metric | CPU              | When CPU utilization exceeds a set value       |

| Metric | Available Memory | When Available Memory drops below a set value |

| Metric | Capture Backlog  | When Capture Backlog is above a certain value |

[!INCLUDE [horz-monitor-advisor-recommendations](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-advisor-recommendations.md)]

## Related content

- See [Azure Event Hubs monitoring data reference](monitor-event-hubs-reference.md) for a reference of the metrics, logs, and other important values created for Event Hubs.

- See [Monitoring Azure resources with Azure Monitor](/azure/azure-monitor/essentials/monitor-azure-resource) for general details on monitoring Azure resources.


# Enable Managed Identity

# Enable managed identity for an Azure Event Hubs namespace

This article shows you how to enable a managed identity for an Azure Event Hubs namespace. The identity can be either a system-assigned managed identity or a user-assigned managed identity.

## Enable system-assigned managed identity for a namespace

Here are the steps to enable a system-assigned managed identity for an Event Hubs namespace by using the Azure portal.

1. Sign-in to the [Azure portal](https://portal.azure.com).

1. Navigate to your Event Hubs namespace.

1. On the **Event Hubs namespace** page, select **Identity** on the left menu.

1. On the **Identity** page, confirm that you are on the **System assigned** tab.

1. For the **Status** field, select **On**.

1. Select **Save** the command bar.

1. In the Pop-up window, select **Yes**.

## Enable user-assigned managed identity for a namespace

Here are the steps to enable a user-assigned managed identity for an Event Hubs namespace by using the Azure portal.

1. Sign-in to the [Azure portal](https://portal.azure.com).

1. If you didn't create a user-assigned identity already, create one by following instructions from: [Manage user-assigned managed identities](/entra/identity/managed-identities-azure-resources/how-manage-user-assigned-managed-identities).

1. In the Azure portal, navigate to your Event Hubs namespace.

1. On the **Event Hubs namespace** page, select **Identity** on the left menu.

1. Switch to the **User assigned** tab, and select **+ Add** on the command bar.

1. In the **Add user assigned identity** pane, search for and select a user-assigned identity, and then select **Add**.

## Related content

After you enable managed identity for your Event Hubs namespace, grant the identity appropriate role on a target resource. For example, if you want to enable capturing of event data on an event hub using a managed identity, the managed identity should be added to the **Storage Blob Data Contributor** role on the Azure storage or Data Lake Store account. For more information on using identities for capturing event data, see [Authenticate modes for capturing events to destinations in Azure Event Hubs](event-hubs-capture-managed-identity.md).


# Event Hubs Ip Filtering

# Allow access to Azure Event Hubs namespaces from specific IP addresses or ranges

By default, users can access Event Hubs namespaces from the internet as long as the request comes with valid authentication and authorization. By using the IP firewall, you can restrict access to only a set of IPv4 and IPv6 addresses or address ranges in [CIDR (Classless Inter-Domain Routing)](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) notation.

This feature is helpful in scenarios where Azure Event Hubs should be accessible only from certain well-known sites. Firewall rules enable you to configure rules to accept traffic originating from specific IPv4 and IPv6 addresses. For example, if you use Event Hubs with [Azure Express Route][express-route], you can create a **firewall rule** to allow traffic from only your on-premises infrastructure IP addresses.

## IP firewall rules

You specify IP firewall rules at the Event Hubs namespace level. The rules apply to all connections from clients using any supported protocol. The Event Hubs namespace rejects any connection attempt from an IP address that doesn't match an allowed IP rule as unauthorized. The response doesn't mention the IP rule. IP firewall rules are applied in order, and the first rule that matches the IP address determines the accept or reject action.

## Important points

- This feature isn't supported in the **basic** tier.

- When you turn on firewall rules for your Event Hubs namespace, the firewall blocks incoming requests by default, unless requests originate from a service operating from allowed public IP addresses. Blocked requests include the requests from other Azure services, from the Azure portal, from logging and metrics services, and so on. As an exception, you can allow access to Event Hubs resources from certain **trusted services** even when the IP filtering is enabled. For a list of trusted services, see [Trusted Microsoft services](#trusted-microsoft-services).

- Specify **at least one IP firewall rule or virtual network rule** for the namespace to allow traffic only from the specified IP addresses or subnet of a virtual network. If there are no IP and virtual network rules, users can access the namespace over the public internet (by using the access key).

## Configure firewall rules using the Azure portal

When creating a namespace, you can either allow public only (from all networks) or private only (only via private endpoints) access to the namespace. Once you create the namespace, you can allow access from specific IP addresses or from specific virtual networks (by using network service endpoints).

### Configure public access when creating a namespace

To enable public access, select **Public access** on the **Networking** page of the namespace creation wizard.

After you create the namespace, select **Networking** in the left menu of the **Event Hubs Namespace** page.

By default, **Public network access** is enabled for the namespace for **all networks**.

This option enables public access from all networks by using an **access key**. The namespace accepts connections from any IP address (using the access key).

The next section provides you details on configuring IP firewall rules to specify the IP addresses from which the access is allowed.

### Configure IP firewall for an existing namespace

This section shows you how to use the Azure portal to create IP firewall rules for an Event Hubs namespace.

1. Navigate to your **Event Hubs namespace** in the [Azure portal](https://portal.azure.com).

1. Select **Networking** under **Settings** on the left menu.

1. On the **Networking** page, select **Manage** under **Public network access**.

1. On the **Public network access** page, in the **Default action** section, select **Enable from selected networks** to allow access from only specified IP addresses.

> [!IMPORTANT]

> If you choose **Selected networks**, add at least one IP firewall rule or a virtual network that has access to the namespace. Choose **Disabled** if you want to restrict all traffic to this namespace over [private endpoints](private-link-service.md) only.

1. In the **IP Addresses** section, select **Add your client IP address** option to give your current client IP the access to the namespace.

1. For **address range**, enter specific IPv4 or IPv6 addresses or address ranges in CIDR notation.

> [!IMPORTANT]

> We recommend that you add IPv6 addresses to the list of allowed IP addresses now so that your clients don't break when the service eventually switches to supporting only IPv6.

1. In the **Exception** section, specify whether you want to **allow trusted Microsoft services to access this resource**. See [Trusted Microsoft services](#trusted-microsoft-services) for details.

1. Select **Save** on the toolbar to save the settings. Wait for a few minutes for the confirmation to show up on the portal notifications.

> [!NOTE]

> To restrict access to specific virtual networks, see [Allow access from specific networks](event-hubs-service-endpoints.md).

[!INCLUDE [event-hubs-trusted-services](./includes/event-hubs-trusted-services.md)]

## Configure firewall rules by using Resource Manager templates

> [!IMPORTANT]

> The Firewall feature isn't supported in the basic tier.

The following Resource Manager template enables adding an IP filter rule to an existing Event Hubs namespace.

The **ipMask** in the template is a single IPv4 address or a block of IP addresses in CIDR notation. For example, in CIDR notation 70.37.104.0/24 represents the 256 IPv4 addresses from 70.37.104.0 to 70.37.104.255, with 24 indicating the number of significant prefix bits for the range.

> [!NOTE]

> The default value of the `defaultAction` is `Allow`. When adding virtual network or firewalls rules, make sure you set the `defaultAction` to `Deny`.

```json

{

"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"namespace_name": {

"defaultValue": "contosoehub1333",

"type": "String"

}

},

"variables": {},

"resources": [

{

"type": "Microsoft.EventHub/namespaces",

"apiVersion": "2022-01-01-preview",

"name": "[parameters('namespace_name')]",

"location": "East US",

"sku": {

"name": "Standard",

"tier": "Standard",

"capacity": 1

},

"properties": {

"minimumTlsVersion": "1.2",

"publicNetworkAccess": "Enabled",

"disableLocalAuth": false,

"zoneRedundant": true,

"isAutoInflateEnabled": false,

"maximumThroughputUnits": 0,

"kafkaEnabled": true

}

},

{

"type": "Microsoft.EventHub/namespaces/authorizationrules",

"apiVersion": "2022-01-01-preview",

"name": "[concat(parameters('namespace_name'), '/RootManageSharedAccessKey')]",

"location": "eastus",

"dependsOn": [

"[resourceId('Microsoft.EventHub/namespaces', parameters('namespace_name'))]"

],

"properties": {

"rights": [

"Listen",

"Manage",

"Send"

]

}

},

{

"type": "Microsoft.EventHub/namespaces/networkRuleSets",

"apiVersion": "2022-01-01-preview",

"name": "[concat(parameters('namespace_name'), '/default')]",

"location": "East US",

"dependsOn": [

"[resourceId('Microsoft.EventHub/namespaces', parameters('namespace_name'))]"

],

"properties": {

"publicNetworkAccess": "Enabled",

"defaultAction": "Deny",

"virtualNetworkRules": [],

"ipRules": [

{

"ipMask": "10.1.1.1",

"action": "Allow"

},

{

"ipMask": "11.0.0.0/24",

"action": "Allow"

},

{

"ipMask": "172.72.157.204",

"action": "Allow"

}

]

}

}

]

}

```

To deploy the template, follow the instructions for [Azure Resource Manager][lnk-deploy].

> [!IMPORTANT]

> If you don't add any IP or virtual network rules, all traffic flows into the namespace even if you set the `defaultAction` to `deny`. Users can access the namespace over the public internet (by using the access key). To allow traffic only from the specified IP addresses or subnet of a virtual network, specify at least one IP rule or virtual network rule for the namespace.

## Configure firewall rules by using Azure CLI

Use [`az eventhubs namespace network-rule-set`](/cli/azure/eventhubs/namespace/network-rule-set) add, list, update, and remove commands to manage IP firewall rules for an Event Hubs namespace.

## Configure firewall rules by using Azure PowerShell

Use the [`Set-AzEventHubNetworkRuleSet`](/powershell/module/az.eventhub/set-azeventhubnetworkruleset) cmdlet to add one or more IP firewall rules. An example from the article:

```azurepowershell-interactive

$ipRule1 = New-AzEventHubIPRuleConfig -IPMask 2.2.2.2 -Action Allow

$ipRule2 = New-AzEventHubIPRuleConfig -IPMask 3.3.3.3 -Action Allow

$virtualNetworkRule1 = New-AzEventHubVirtualNetworkRuleConfig -SubnetId '/subscriptions/subscriptionId/resourcegroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVirtualNetwork/subnets/default'

$networkRuleSet = Get-AzEventHubNetworkRuleSet -ResourceGroupName myResourceGroup -NamespaceName myNamespace

$networkRuleSet.IPRule += $ipRule1

$networkRuleSet.IPRule += $ipRule2

$networkRuleSet.VirtualNetworkRule += $virtualNetworkRule1

Set-AzEventHubNetworkRuleSet -ResourceGroupName myResourceGroup -NamespaceName myNamespace -IPRule $ipRule1,$ipRule2 -VirtualNetworkRule $virtualNetworkRule1,$virtualNetworkRule2,$virtualNetworkRule3

```

## Default action and public network access

### REST API

For API versions **2021-01-01-preview and earlier**, the default value of the `defaultAction` property is `Deny`. However, the service doesn't enforce the deny rule unless you set IP filters or virtual network rules. If you don't set any IP filters or virtual network rules, the service treats the default action as `Allow`.

From API version **2021-06-01-preview onwards**, the default value of the `defaultAction` property is `Allow`, which accurately reflects the service-side enforcement. If you set the default action to `Deny`, the service enforces IP filters and virtual network rules. If you set the default action to `Allow`, the service doesn't enforce IP filters and virtual network rules. The service remembers the rules when you turn them off and then back on again.

API version **2021-06-01-preview onwards** also introduces a new property named `publicNetworkAccess`. If you set this property to `Disabled`, operations are restricted to private links only. If you set it to `Enabled`, operations are allowed over the public internet.

For more information about these properties, see [Create or Update Network Rule Set](/rest/api/eventhub/namespaces/create-or-update-network-rule-set) and [Create or Update Private Endpoint Connections](/rest/api/eventhub/private-endpoint-connections/create-or-update).

> [!NOTE]

> None of the preceding settings bypass validation of claims through SAS or Microsoft Entra authentication. The authentication check always runs after the service validates the network checks that the `defaultAction`, `publicNetworkAccess`, and `privateEndpointConnections` settings configure.

### Azure portal

Azure portal always uses the latest API version to get and set properties. If you configured your namespace by using **2021-01-01-preview and earlier** versions with the `defaultAction` set to `Deny`, and you specified zero IP filters and virtual network rules, the portal previously checked **Selected Networks** on the **Networking** page of your namespace. Now, it checks the **All networks** option.

## Next steps

To constrain access to Event Hubs to Azure virtual networks, see the following article:

- [Virtual Network Service Endpoints for Event Hubs][lnk-vnet]

[express-route]:  ../expressroute/expressroute-faqs.md#supported-services

[lnk-deploy]: ../azure-resource-manager/templates/deploy-powershell.md

[lnk-vnet]: event-hubs-service-endpoints.md


# Event Hubs Service Endpoints

# Allow access to Azure Event Hubs namespaces from specific virtual networks

Integrate Event Hubs with Azure Virtual Network service endpoints to restrict access to your Event Hubs namespace from specific virtual network subnets. This article explains how virtual network integration works and provides step-by-step instructions to configure it.

## Overview

By using [Virtual Network service endpoints][vnet-sep], workloads running in a virtual network, such as virtual machines, can securely access your Event Hubs namespace. The network traffic path is secured on both ends.

When you configure an Event Hubs namespace with at least one virtual network service endpoint, the namespace only accepts traffic from authorized subnets. From the virtual network perspective, the service endpoint creates an isolated networking tunnel from the subnet to the Event Hubs namespace.

This configuration establishes a private and isolated connection between workloads in the subnet and your Event Hubs namespace, even though the Event Hubs service endpoint uses a public IP address.

## Important points

- This feature isn't supported in the **basic** tier.

- When you enable virtual networks for your Event Hubs namespace, incoming requests are blocked by default unless they originate from a service operating from allowed virtual networks. Blocked requests include the requests from other Azure services, the Azure portal, logging and metrics services, and so on. As an exception, you can allow access to Event Hubs resources from certain **trusted services** even when virtual networks are enabled. For a list of trusted services, see [Trusted services](#trusted-microsoft-services).

- Specify **at least one IP rule or virtual network rule** for the namespace to allow traffic only from the specified IP addresses or subnet of a virtual network. If you don't specify any IP and virtual network rules, the namespace is accessible over the public internet (using the access key).

## Advanced security scenarios enabled by virtual network integration

Virtual network integration supports scenarios that require strict security isolation while still allowing communication between compartmentalized services.

Direct IP routes between network compartments, even those using HTTPS over TCP/IP, are vulnerable to network-layer exploits. Event Hubs provides a more secure alternative by acting as an intermediary. Workloads in separate virtual networks that connect to the same Event Hubs instance can exchange messages reliably while maintaining network isolation.

This approach gives security-sensitive solutions access to Azure's scalable messaging capabilities while creating communication paths that are more secure than direct peer-to-peer connections.

## Bind Event Hubs to virtual networks

**Virtual network rules** control whether your Event Hubs namespace accepts connections from a specific virtual network subnet.

To bind an Event Hubs namespace to a virtual network:

1. Create a **service endpoint** on a virtual network subnet and enable it for **Microsoft.EventHub**. For more information, see [Virtual network service endpoints][vnet-sep].

1. Add a **virtual network rule** to bind the Event Hubs namespace to the service endpoint.

The virtual network rule creates an association between the Event Hubs namespace and the virtual network subnet. All workloads in the subnet can access the Event Hubs namespace while the rule exists.

> [!NOTE]

> Event Hubs doesn't establish outbound connections to your subnet. The rule only grants inbound access from the subnet to Event Hubs.

## Use Azure portal

When creating a namespace, you can choose between:

- **Public access**: Allows access from all networks.

- **Private access**: Restricts access to private endpoints only.

After creating the namespace, you can further refine access by specifying IP addresses or virtual networks or network security perimeters.

### Configure public access when creating a namespace

To enable public access, select **Public access** on the **Networking** page of the namespace creation wizard.

After you create the namespace, select **Networking** in the left menu of the **Event Hubs Namespace** page.

By default, **Public network access** is enabled for the namespace for **all networks**.

This option enables public access from all networks by using an **access key**. The namespace accepts connections from any IP address (using the access key).

The next section provides you details on configuring virtual network service endpoints to specify the virtual networks from which the access is allowed.

### Configure selected networks for an existing namespace

This section shows you how to use Azure portal to add a virtual network service endpoint. To limit access, integrate the virtual network service endpoint for this Event Hubs namespace.

1. Go to your **Event Hubs namespace** in the [Azure portal](https://portal.azure.com).

1. Select **Networking** under **Settings** in the left menu.

1. On the **Networking** page, select **Manage** under **Public network access**.

1. On the **Public network access** page, in the **Default action** section, select **Enable from selected networks** to allow access from only specified IP addresses.

> [!IMPORTANT]

> If you choose **Selected networks**, add at least one IP firewall rule or a virtual network that has access to the namespace. Choose **Disabled** if you want to restrict all traffic to this namespace over [private endpoints](private-link-service.md) only.

1. In the **Virtual networks** section of the page, select **+Add a virtual network** -> **Add existing virtual network***. Select **Add new virtual network** if you want to create a new virtual network.

> [!IMPORTANT]

> If you choose **Selected networks**, add at least one IP firewall rule or a virtual network that can access your namespace. Choose **Disabled** if you want to restrict all traffic to this namespace over [private endpoints](private-link-service.md) only.

1. Select the **virtual network** from the list of virtual networks, select the **subnet**, and then select **Enable**. You must enable the service endpoint before adding the virtual network to the list. If the service endpoint isn't enabled, the portal prompts you to enable it.

1. You see a success message after enabling the service endpoint for the subnet for **Microsoft.EventHub**. Select **Add** at the bottom of the page to add the network.

> [!NOTE]

> If you're unable to enable the service endpoint, you can ignore the missing virtual network service endpoint by using the Resource Manager template. This functionality isn't available on the portal.

1. In the **Exception** section, specify whether you want to **allow trusted Microsoft services to access this resource**. See [Trusted Microsoft services](#trusted-microsoft-services) for details.

1. Select **Save** on the toolbar to save the settings. Wait a few minutes for the confirmation to appear in the portal notifications.

> [!NOTE]

> To restrict access to specific IP addresses or ranges, see [Allow access from specific IP addresses or ranges](event-hubs-ip-filtering.md).

> [!NOTE]

> To delete a Virtual Network rule, first remove any Azure Resource Manager delete lock on the Virtual Network.

[!INCLUDE [event-hubs-trusted-services](./includes/event-hubs-trusted-services.md)]

## Use Resource Manager template

This sample Resource Manager template adds a virtual network rule to an existing Event Hubs namespace. It specifies the ID of a subnet in a virtual network for the network rule.

The ID is a fully qualified Resource Manager path for the virtual network subnet. For example: `/subscriptions/{id}/resourceGroups/{rg}/providers/Microsoft.Network/virtualNetworks/{vnet}/subnets/default`.

When adding virtual network or firewall rules, set the value of `defaultAction` to `Deny`.

```json

{

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"eventhubNamespaceName": {

"type": "string",

"metadata": {

"description": "Name of the Event Hubs namespace"

}

},

"virtualNetworkName": {

"type": "string",

"metadata": {

"description": "Name of the Virtual Network Rule"

}

},

"subnetName": {

"type": "string",

"metadata": {

"description": "Name of the Virtual Network Sub Net"

}

},

"location": {

"type": "string",

"metadata": {

"description": "Location for Namespace"

}

}

},

"variables": {

"namespaceNetworkRuleSetName": "[concat(parameters('eventhubNamespaceName'), concat('/', 'default'))]",

"subNetId": "[resourceId('Microsoft.Network/virtualNetworks/subnets/', parameters('virtualNetworkName'), parameters('subnetName'))]"

},

"resources": [

{

"apiVersion": "2018-01-01-preview",

"name": "[parameters('eventhubNamespaceName')]",

"type": "Microsoft.EventHub/namespaces",

"location": "[parameters('location')]",

"sku": {

"name": "Standard",

"tier": "Standard"

},

"properties": { }

},

{

"apiVersion": "2017-09-01",

"name": "[parameters('virtualNetworkName')]",

"location": "[parameters('location')]",

"type": "Microsoft.Network/virtualNetworks",

"properties": {

"addressSpace": {

"addressPrefixes": [

"10.0.0.0/23"

]

},

"subnets": [

{

"name": "[parameters('subnetName')]",

"properties": {

"addressPrefix": "10.0.0.0/23",

"serviceEndpoints": [

{

"service": "Microsoft.EventHub"

}

]

}

}

]

}

},

{

"apiVersion": "2018-01-01-preview",

"name": "[variables('namespaceNetworkRuleSetName')]",

"type": "Microsoft.EventHub/namespaces/networkruleset",

"dependsOn": [

"[concat('Microsoft.EventHub/namespaces/', parameters('eventhubNamespaceName'))]"

],

"properties": {

"publicNetworkAccess": "Enabled",

"defaultAction": "Deny",

"virtualNetworkRules":

[

{

"subnet": {

"id": "[variables('subNetId')]"

},

"ignoreMissingVnetServiceEndpoint": false

}

],

"ipRules":[],

"trustedServiceAccessEnabled": false

}

}

],

"outputs": { }

}

```

To deploy the template, follow the instructions for [Azure Resource Manager][lnk-deploy].

> [!IMPORTANT]

> If you don't specify any IP or virtual network rules, all traffic flows into the namespace even if you set the `defaultAction` to `Deny`. The namespace is accessible over the public internet (using the access key). To allow traffic only from the specified IP addresses or subnet of a virtual network, specify at least one IP rule or virtual network rule for the namespace.

## Use Azure CLI

Use the [`az eventhubs namespace network-rule-set`](/cli/azure/eventhubs/namespace/network-rule-set) commands to manage virtual network rules for an Event Hubs namespace:

- `add` - Add a virtual network rule

- `list` - List all network rules

- `update` - Update network rules

- `remove` - Remove a virtual network rule

## Use Azure PowerShell

Use the following Azure PowerShell commands to manage virtual network rules for an Event Hubs namespace:

| Command | Description |

|---------|-------------|

| [`Add-AzEventHubVirtualNetworkRule`](/powershell/module/az.eventhub/add-azeventhubvirtualnetworkrule) | Add a virtual network rule |

| [`New-AzEventHubVirtualNetworkRuleConfig`](/powershell/module/az.eventhub/new-azeventhubipruleconfig) | Create a virtual network rule configuration (use with `Set-AzEventHubNetworkRuleSet`) |

| [`Set-AzEventHubNetworkRuleSet`](/powershell/module/az.eventhub/set-azeventhubnetworkruleset) | Apply network rule configuration to a namespace |

| [`Remove-AzEventHubVirtualNetworkRule`](/powershell/module/az.eventhub/remove-azeventhubvirtualnetworkrule) | Remove a virtual network rule |

## Default action and public network access

### REST API

The behavior of the `defaultAction` property varies by API version:

| API version | Default value | Behavior |

|-------------|---------------|----------|

| **2021-01-01-preview and earlier** | `Deny` | The deny rule isn't enforced unless you configure IP filters or virtual network rules. Without rules, traffic is allowed. |

| **2021-06-01-preview and later** | `Allow` | The service enforces the configured action. Set to `Deny` to block traffic not matching your rules. |

API version **2021-06-01-preview** also introduces the `publicNetworkAccess` property:

- `Enabled` - Allow operations over the public internet

- `Disabled` - Restrict operations to private links only

The service remembers your rules when you disable and re-enable them.

For more information, see [Create or Update Network Rule Set](/rest/api/eventhub/namespaces/create-or-update-network-rule-set) and [Create or Update Private Endpoint Connections](/rest/api/eventhub/private-endpoint-connections/create-or-update).

> [!NOTE]

> Network settings don't bypass authentication. The service always validates SAS or Microsoft Entra authentication claims after checking the network rules configured by `defaultAction`, `publicNetworkAccess`, and `privateEndpointConnections`.

### Azure portal

The Azure portal always uses the latest API version to get and set properties. If you previously configured your namespace by using **2021-01-01-preview and earlier** versions with `defaultAction` set to `Deny`, and you specified zero IP filters and virtual network rules, the portal previously checked **Selected Networks** on the **Networking** page of your namespace. Now, it checks the **All networks** option.

## Related content

- [Azure virtual network service endpoints][vnet-sep]

- [Allow access from specific IP addresses or ranges][ip-filtering]

- [Use private endpoints for Azure Event Hubs](private-link-service.md)

[vnet-sep]: ../virtual-network/virtual-network-service-endpoints-overview.md

[lnk-deploy]: ../azure-resource-manager/templates/deploy-powershell.md

[ip-filtering]: event-hubs-ip-filtering.md


# Private Link Service

# Allow access to Azure Event Hubs namespaces via private endpoints

Azure Private Link Service enables you to access Azure Services (for example, Azure Event Hubs, Azure Storage, and Azure Cosmos DB) and Azure hosted customer/partner services over a **private endpoint** in your virtual network.

A private endpoint is a network interface that connects you privately and securely to a service powered by Azure Private Link. The private endpoint uses a private IP address from your virtual network, effectively bringing the service into your virtual network. All traffic to the service is routed through the private endpoint, so no gateways, NAT devices, ExpressRoute or VPN connections, or public IP addresses are needed. Traffic between your virtual network and the service traverses over the Microsoft backbone network, eliminating exposure from the public Internet. You can connect to an instance of an Azure resource, giving you the highest level of granularity in access control.

For more information, see [What is Azure Private Link?](../private-link/private-link-overview.md)

## Important points

- This feature isn't supported in the **basic** tier.

- Enabling private endpoints can prevent other Azure services from interacting with Event Hubs. Requests that are blocked include those from other Azure services, from the Azure portal, from logging and metrics services, and so on. As an exception, you can allow access to Event Hubs resources from certain **trusted services** even when private endpoints are enabled. For a list of trusted services, see [Trusted services](#trusted-microsoft-services).

## Add a private endpoint using Azure portal

### Prerequisites

To integrate an Event Hubs namespace with Azure Private Link, you need the following entities or permissions:

- An Event Hubs namespace.

- An Azure virtual network.

- A subnet in the virtual network. You can use the **default** subnet.

- Owner or contributor permissions for both the namespace and the virtual network.

Your private endpoint and virtual network must be in the same region. When you select a region for the private endpoint using the portal, it automatically filters virtual networks that are in that region. Your namespace can be in a different region.

Your private endpoint uses a private IP address in your virtual network.

### Configure private access when creating a namespace

When creating a namespace, you can either allow public only (from all networks) or private only (only via private endpoints) access to the namespace.

If you select the **Private access** option on the **Networking** page of the namespace creation wizard, you can add a private endpoint on the page by selecting **+ Private endpoint** button. See the next section for the detailed steps for adding a private endpoint.

### Configure private access for an existing namespace

If you already have an Event Hubs namespace, you can create a private link connection by following these steps:

#### Disable public access

Disable public access to your Event Hubs namespace to allow access only via private endpoints.

1. Navigate to your **Event Hubs namespace** in the [Azure portal](https://portal.azure.com).

1. Select **Networking** under **Settings** on the left menu.

1. On the **Networking** page, select **Manage** under **Public network access**.

1. On the **Public network access** page, select **Disable** to restrict inbound access while allowing outbound access. In the pop-up, select **Proceed** to confirm.

1. On the **Public network access** page, select **Save** at the bottom of the page.

1. In the **Exception** section, specify whether you want to **allow trusted Microsoft services to access this resource**. See [Trusted Microsoft services](#trusted-microsoft-services) for details.

#### Add a private endpoint

Now, add a private endpoint to your Event Hubs namespace by following these steps:

1. On the **Networking** page, switch to the **Private access** tab.

1. Select the **Create private Endpoint** button at the top of the page.

7. On the **Basics** page, follow these steps:

1. Select the **Azure subscription** in which you want to create the private endpoint.

2. Select the **resource group** for the private endpoint resource.

3. Enter a **name** for the private endpoint.

1. Enter a **name for the network interface**.

1. Select a **region** for the private endpoint. Your private endpoint must be in the same region as your virtual network, but can be in a different region from the private link resource that you're connecting to.

1. Select **Next: Resource >** button at the bottom of the page.

8. On the **Resource** page, review settings, and select **Next: Virtual Network**.

9. On the **Virtual Network** page, you select the subnet in a virtual network to where you want to deploy the private endpoint.

1. Select a **virtual network**. Only virtual networks in the currently selected subscription and location are listed in the drop-down list.

2. Select a **subnet** in the virtual network you selected.

1. Notice that the **network policy for private endpoints** is disabled. If you want to enable it, select **edit**, update the setting, and select **Save**.

1. For **Private IP configuration**, by default, **Dynamically allocate IP address** option is selected. If you want to assign a static IP address, select **Statically allocate IP address***.

1. For **Application security group**, select an existing application security group or create one that's to be associated with the private endpoint.

1. Select **Next: DNS >** button at the bottom of the page.

10. On the **DNS** page, select whether you want the private endpoint to be integrated with a private DNS zone, and then select **Next: Tags**.

1. On the **Tags** page, create any tags (names and values) that you want to associate with the private endpoint resource. Then, select **Review + create** button at the bottom of the page.

1. On the **Review + create**, review all the settings, and select **Create** to create the private endpoint.

12. Confirm that you see the private endpoint connection you created shows up in the list of endpoints. Refresh the page and switch to the **Private endpoint connections** tab. In this example, the private endpoint is auto-approved because you connected to an Azure resource in your directory and you have sufficient permissions.

[!INCLUDE [event-hubs-trusted-services](./includes/event-hubs-trusted-services.md)]

To allow trusted services to access your namespace, switch to the **Public Access** tab on the **Networking** page, and select **Yes** for **Allow trusted Microsoft services to bypass this firewall?**.

## Add a private endpoint using PowerShell

The following example shows how to use Azure PowerShell to create a private endpoint connection. It doesn't create a dedicated cluster for you. Follow steps in [this article](event-hubs-dedicated-cluster-create-portal.md) to create a dedicated Event Hubs cluster.

```azurepowershell-interactive

$rgName = "<RESOURCE GROUP NAME>"

$vnetlocation = "<VIRTUAL NETWORK LOCATION>"

$vnetName = "<VIRTUAL NETWORK NAME>"

$subnetName = "<SUBNET NAME>"

$namespaceLocation = "<NAMESPACE LOCATION>"

$namespaceName = "<NAMESPACE NAME>"

$peConnectionName = "<PRIVATE ENDPOINT CONNECTION NAME>"

# create resource group

New-AzResourceGroup -Name $rgName -Location $vnetLocation

# create virtual network

$virtualNetwork = New-AzVirtualNetwork `

-ResourceGroupName $rgName `

-Location $vnetlocation `

-Name $vnetName `

-AddressPrefix 10.0.0.0/16

# create subnet with endpoint network policy disabled

$subnetConfig = Add-AzVirtualNetworkSubnetConfig `

-Name $subnetName `

-AddressPrefix 10.0.0.0/24 `

-PrivateEndpointNetworkPoliciesFlag "Disabled" `

-VirtualNetwork $virtualNetwork

# update virtual network

$virtualNetwork | Set-AzVirtualNetwork

# create an event hubs namespace in a dedicated cluster

$namespaceResource = New-AzResource -Location $namespaceLocation `

-ResourceName $namespaceName `

-ResourceGroupName $rgName `

-Sku @{name = "Standard"; capacity = 1} `

-Properties @{clusterArmId = "/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP NAME>/providers/Microsoft.EventHub/clusters/<EVENT HUBS CLUSTER NAME>"} `

-ResourceType "Microsoft.EventHub/namespaces" -ApiVersion "2018-01-01-preview"

# create private endpoint connection

$privateEndpointConnection = New-AzPrivateLinkServiceConnection `

-Name $peConnectionName `

-PrivateLinkServiceId $namespaceResource.ResourceId `

-GroupId "namespace"

# get subnet object that you'll use later

$virtualNetwork = Get-AzVirtualNetwork -ResourceGroupName  $rgName -Name $vnetName

$subnet = $virtualNetwork | Select -ExpandProperty subnets `

| Where-Object  {$_.Name -eq $subnetName}

# create a private endpoint

$privateEndpoint = New-AzPrivateEndpoint -ResourceGroupName $rgName  `

-Name $vnetName   `

-Location $vnetlocation `

-Subnet  $subnet   `

-PrivateLinkServiceConnection $privateEndpointConnection

(Get-AzResource -ResourceId $namespaceResource.ResourceId -ExpandProperties).Properties

```

### Configure the private DNS Zone

Create a private DNS zone for Event Hubs domain and create an association link with the virtual network:

```azurepowershell-interactive

$zone = New-AzPrivateDnsZone -ResourceGroupName $rgName `

-Name "privatelink.servicebus.windows.net"

$link  = New-AzPrivateDnsVirtualNetworkLink -ResourceGroupName $rgName `

-ZoneName "privatelink.servicebus.windows.net" `

-Name "mylink" `

-VirtualNetworkId $virtualNetwork.Id

$networkInterface = Get-AzResource -ResourceId $privateEndpoint.NetworkInterfaces[0].Id -ApiVersion "2019-04-01"

foreach ($ipconfig in $networkInterface.properties.ipConfigurations) {

foreach ($fqdn in $ipconfig.properties.privateLinkConnectionProperties.fqdns) {

Write-Host "$($ipconfig.properties.privateIPAddress) $($fqdn)"

$recordName = $fqdn.split('.',2)[0]

$dnsZone = $fqdn.split('.',2)[1]

New-AzPrivateDnsRecordSet -Name $recordName -RecordType A -ZoneName "privatelink.servicebus.windows.net"  `

-ResourceGroupName $rgName -Ttl 600 `

-PrivateDnsRecords (New-AzPrivateDnsRecordConfig -IPv4Address $ipconfig.properties.privateIPAddress)

}

}

```

## Manage private endpoints using Azure portal

When you create a private endpoint, the connection must be approved. If the resource for which you're creating a private endpoint is in your directory, you can approve the connection request provided you have sufficient permissions. If you're connecting to an Azure resource in another directory, you must wait for the owner of that resource to approve your connection request.

There are four provisioning states:

| Service action | Service consumer private endpoint state | Description |

|--|--|--|

| None | Pending | Connection is created manually and is pending approval from the Private Link resource owner. |

| Approve | Approved | Connection was automatically or manually approved and is ready to be used. |

| Reject | Rejected | Connection was rejected by the private link resource owner. |

| Remove | Disconnected | Connection was removed by the private link resource owner. The private endpoint becomes informative and should be deleted for cleanup. |

###  Approve, reject, or remove a private endpoint connection

1. Sign in to the Azure portal.

2. In the search bar, type in **event hubs**.

3. Select the **namespace** that you want to manage.

4. Select the **Networking** tab.

5. Go to the appropriate following section based on the operation you want to: approve, reject, or remove.

### Approve a private endpoint connection

1. If there are any connections that are pending, you see a connection listed with **Pending** in the provisioning state.

2. Select the **private endpoint** you wish to approve

3. Select the **Approve** button.

4. On the **Approve connection** page, add a comment (optional), and select **Yes**. If you select **No**, nothing happens.

5. You should see the status of the private endpoint connection in the list changed to **Approved**.

### Reject a private endpoint connection

1. If there are any private endpoint connections you want to reject, whether it's a pending request or existing connection, select the connection and select the **Reject** button.

2. On the **Reject connection** page, enter a comment (optional), and select **Yes**. If you select **No**, nothing happens.

3. You should see the status of the private endpoint connection in the list changed to **Rejected**.

### Delete a private endpoint connection

1. To delete a private endpoint connection, select it in the list, and select **Delete** on the toolbar.

2. On the **Delete connection** page, select **Yes** to confirm the deletion of the private endpoint. If you select **No**, nothing happens.

3. You should see the status changed to **Disconnected**. Then, the endpoint disappears from the list.

## Validate that the private link connection works

You should validate that resources within the virtual network of the private endpoint are connecting to your Event Hubs namespace over a private IP address, and that they have the correct private DNS zone integration.

First, create a virtual machine by following the steps in [Create a Windows virtual machine in the Azure portal](/azure/virtual-machines/windows/quick-create-portal)

In the **Networking** tab:

1. Specify **Virtual network** and **Subnet**. You must select the Virtual Network on which you deployed the private endpoint.

2. Specify a **public IP** resource.

3. For **NIC network security group**, select **None**.

4. For **Load balancing**, select **No**.

Connect to the VM, open the command line, and run the following command:

```console

nslookup <event-hubs-namespace-name>.servicebus.windows.net

```

You should see a result that looks like the following.

```console

Non-authoritative answer:

Name:    <event-hubs-namespace-name>.privatelink.servicebus.windows.net

Address:  10.0.0.4 (private IP address associated with the private endpoint)

Aliases:  <event-hubs-namespace-name>.servicebus.windows.net

```

## Limitations and design considerations

- For pricing information, see [Azure Private Link pricing](https://azure.microsoft.com/pricing/details/private-link/).

- This feature is available in all Azure public regions.

- Maximum number of private endpoints per Event Hubs namespace: 120.

- The traffic is blocked at the application layer, not at the TCP layer. Therefore, you see TCP connections or `nslookup` operations succeeding against the public endpoint even though the public access is disabled.

For more, see [Azure Private Link service: Limitations](../private-link/private-link-service-overview.md#limitations)

## Related content

- Learn more about [Azure Private Link](../private-link/private-link-service-overview.md)

- Learn more about [Azure Event Hubs](event-hubs-about.md)


# Associate Network Security Perimeter

# Associate network security perimeter (NSP) with an Azure Event Hubs namespace

You can associate a network security perimeter (NSP) with an Azure Event Hubs namespace to enhance the security of your event streaming infrastructure. This association restricts access to the Event Hubs namespace based on the defined security perimeter, allowing you to:

- Control which Azure resources can communicate with your Event Hubs namespace.

- Define inbound and outbound access rules for your event streaming workloads.

- Monitor and audit network access to your Event Hubs resources.

> [!NOTE]

> For conceptual information, see [Network security perimeter for Azure Event Hubs](network-security-perimeter.md).

## Prerequisites

Before you begin, ensure you have the following prerequisites in place:

- An existing Azure Event Hubs namespace.

- An existing network security perimeter (NSP) in your Azure subscription. If you don't have one, [create a network security perimeter](/azure/private-link/create-network-security-perimeter-portal) first.

- A profile configured within the NSP to associate with your Event Hubs namespace.

- The **Contributor** role or higher on the Event Hubs namespace.

- The **Network Security Perimeter Contributor** role or higher on the NSP.

## Associate NSP with an Azure Event Hubs namespace

Follow these steps to associate an NSP with your Event Hubs namespace using the Azure portal:

1. Sign in to the [Azure portal](https://portal.azure.com/).

1. In the search box, enter **Event Hubs**, and then select **Event Hubs** from the search results.

1. Select your Event Hubs namespace from the list.

1. In the left-hand menu under **Settings**, select **Networking**.

1. Select the **Public access** tab.

1. Under the **Network security perimeter** section, select **Associate NSP**.

1. In the **Associate network security perimeter** page, complete the following configuration:

| Setting | Description |

| --- | --- |

| **Network security perimeter** | Select the NSP you want to associate from the dropdown list. Only NSPs in the same region as your Event Hubs namespace are available. |

| **Profile** | Select the profile within the NSP to associate with the Event Hubs namespace. Profiles contain the access rules that apply to associated resources. |

1. Select **Associate** to complete the association.

1. Wait for the association to complete. The process typically takes a few minutes.

1. Once the association is complete, verify that the NSP appears under the **Network security perimeter** section of your Event Hubs namespace.

## Manage NSP settings

After associating the NSP with your Event Hubs namespace, you can manage and configure the security settings.

### View and modify NSP configuration

1. On the **Networking** page of your Event Hubs namespace, select **Manage** in the **Network security perimeter** section.

1. Review the inbound and outbound access rules configured for the NSP. These rules determine what traffic is allowed to and from your Event Hubs namespace.

1. To add or modify inbound and outbound rules:

1. Navigate to the NSP configuration page by selecting the **NSP name** at the top of the page.

1. In the NSP configuration, you can:

- Add **inbound access rules** to allow specific external resources or IP addresses to access your Event Hubs namespace.

- Add **outbound access rules** to allow your Event Hubs namespace to communicate with external resources.

- Modify or delete existing rules as needed.

> [!TIP]

> When configuring access rules, follow the principle of least privilege by only allowing the minimum required access for your workloads.

### Assign a managed identity

To use managed identity with your NSP-associated Event Hubs namespace:

1. In the **Associate resource** section, select **Manage** for **Identity**.

1. Follow the steps in [Enable managed identity for Event Hubs](enable-managed-identity.md) to assign a system-assigned or user-assigned managed identity to your namespace.

## Verify the association

After completing the association, perform these verification steps:

1. **Test connectivity**: Verify that the Event Hubs namespace is accessible only from resources within the defined network security perimeter.

- Attempt to connect from a resource inside the perimeter (should succeed).

- Attempt to connect from a resource outside the perimeter (should be blocked unless allowed by access rules).

1. **Review diagnostic logs**: Enable diagnostic logging for your Event Hubs namespace to monitor connection attempts and identify any access issues.

1. **Validate application functionality**: Ensure that your applications can still send and receive events as expected.

## Best practices

Follow these best practices when using NSP with Event Hubs:

- **Plan your perimeter**: Before you associate an NSP, map out all the resources that need to communicate with your Event Hubs namespace.

- **Use profiles effectively**: Create separate profiles for different environments (development, staging, production) to apply appropriate access rules.

- **Monitor regularly**: Set up alerts and regularly review access logs to detect unauthorized access attempts.

- **Keep rules updated**: As your infrastructure changes, update your NSP rules to reflect new requirements while maintaining security.

- **Test changes**: Before applying NSP changes in production, test them in a nonproduction environment.

## Troubleshooting

If you encounter issues after associating an NSP with your Event Hubs namespace:

| Issue | Possible cause | Solution |

| --- | --- | --- |

| Applications can't connect to Event Hubs | NSP is blocking the traffic | Add an inbound access rule to allow traffic from your application's network. |

| Event Hubs can't send data to downstream services | Outbound rules are too restrictive | Add an outbound access rule to allow traffic to the required destination. |

| NSP doesn't appear in the dropdown list | NSP is in a different region | Create an NSP in the same region as your Event Hubs namespace. |

| Association fails | Insufficient permissions | Verify you have the required roles on both the Event Hubs namespace and the NSP. |

## Related content

- [Network security perimeter for Azure Event Hubs](network-security-perimeter.md)

- [Azure network security perimeter concepts](/azure/private-link/network-security-perimeter-concepts)

- [Create a network security perimeter](/azure/private-link/create-network-security-perimeter-portal)


# Configure Customer Managed Key

# Configure customer-managed keys for encrypting Azure Event Hubs data at rest

Azure Event Hubs provides encryption of data at rest with Azure Storage Service Encryption (Azure SSE). The Event Hubs service uses Azure Storage to store the data. All the data that's stored in Azure Storage is encrypted using Microsoft-managed keys. If you use your own key (also referred to as Bring Your Own Key (BYOK) or customer-managed key), the data is still encrypted using the Microsoft-managed key, but in addition the Microsoft-managed key will be encrypted using the customer-managed key. This feature enables you to create, rotate, disable, and revoke access to customer-managed keys that are used for encrypting Microsoft-managed keys. Enabling the BYOK feature is a one time setup process on your namespace.

> [!IMPORTANT]

> - The BYOK capability is supported by **premium** and **dedicated** tiers of Event Hubs.

> - The encryption can be enabled only for new or empty namespaces. If the namespace contains event hubs, the encryption operation fails.

You can use Azure Key Vault (including Azure Key Vault Managed Hardware Security Module) to manage your keys and audit your key usage. You can either create your own keys and store them in a key vault, or you can use the Azure Key Vault APIs to generate keys. For more information about Azure Key Vault, see [What is Azure Key Vault?](/azure/key-vault/general/overview)

This article shows how to configure a key vault with customer-managed keys by using the Azure portal. To learn how to create a key vault using the Azure portal, see [Quickstart: Create an Azure Key Vault using the Azure portal](/azure/key-vault/general/quick-create-portal).

## Enable customer-managed keys (Azure portal)

To enable customer-managed keys in the Azure portal, follow these steps. If you're using the dedicated tier, navigate to your Event Hubs Dedicated cluster first.

1. Select the namespace on which you want to enable BYOK.

1. On the **Settings** page of your Event Hubs namespace, select **Encryption**.

1. Select the **Customer-managed key encryption at rest** as shown in the following image.

![Enable customer managed key](./media/configure-customer-managed-key/enable-customer-managed-key.png)

> [!NOTE]

> Currently you can't configure Azure Key Vault Managed HSM through the portal.

## Set up a key vault with keys

After you enable customer-managed keys, you need to associate the customer managed key with your Azure Event Hubs namespace. Event Hubs supports only Azure Key Vault. If you enable the **Encryption with customer-managed key** option in the previous section, you need to have the key imported into Azure Key Vault. Also, the keys must have **Soft Delete** and **Do Not Purge** configured for the key. These settings can be configured using [PowerShell](/azure/key-vault/general/key-vault-recovery) or [CLI](/azure/key-vault/general/key-vault-recovery).

### Create key vault or key vault managed HSM

> [!IMPORTANT]

> Using customer-managed keys with Azure Event Hubs requires that the key vault have two required properties configured. They are:  **Soft Delete** and **Do Not Purge**. These properties are enabled by default when you create a new key vault in the Azure portal. However, if you need to enable these properties on an existing key vault, you must use either PowerShell or Azure CLI.

# [Key Vault](#tab/Key-Vault)

1. To create a new key vault, follow the Azure Key Vault [Quickstart](/azure/key-vault/general/overview). For more information about importing existing keys, see [About keys, secrets, and certificates](/azure/key-vault/general/about-keys-secrets-certificates).

2. To turn on both soft delete and purge protection when creating a vault, use the [az keyvault create](/cli/azure/keyvault#az-keyvault-create) command.

```azurecli-interactive

az keyvault create --name ContosoVault --resource-group ContosoRG --location westus --enable-soft-delete true --enable-purge-protection true

```

3. To add purge protection to an existing vault (that already has soft delete enabled), use the [az keyvault update](/cli/azure/keyvault#az-keyvault-update) command.

```azurecli-interactive

az keyvault update --name ContosoVault --resource-group ContosoRG --enable-purge-protection true

```

# [Key Vault Managed HSM](#tab/Key-Vault-Managed-HSM)

1. To create a new Managed HSM, follow the Managed HSM [Quickstart](/azure/key-vault/managed-hsm/quick-create-cli). For information about Azure KeyVault, see [About Azure KeyVault](/azure/key-vault/general/overview).

2. To turn on both soft delete and purge protection when creating a vault, use the [az keyvault create](/cli/azure/keyvault#az-keyvault-create) command.

```azurecli-interactive

az keyvault create --hsm-name ContosoVault --resource-group ContosoRG --location westus --enable-soft-delete true --enable-purge-protection true

```

After creation, you need to [activate the Managed HSM](/azure/key-vault/managed-hsm/quick-create-cli#activate-your-managed-hsm) and ensure that you have the correct permissions to generate keys by [assigning an RBAC role and local RBAC role](/azure/key-vault/managed-hsm/secure-your-managed-hsm) with the correct permissions.

3. To add purge protection to an existing vault (that already has soft delete enabled), use the [az keyvault update](/cli/azure/keyvault#az-keyvault-update) command.

```azurecli-interactive

az keyvault update --hsm-name ContosoVault --resource-group ContosoRG --enable-purge-protection true

```

---

## Create Keys

Create keys by following these steps:

1. To create a new key, select **Generate/Import** from the **Keys** menu under **Settings**.

![Select Generate/Import button](./media/configure-customer-managed-key/select-generate-import.png)

2. Set **Options** to **Generate** and give the key a name.

![Create a key](./media/configure-customer-managed-key/create-key.png)

3. You can now select this key to associate with the Event Hubs namespace for encrypting from the drop-down list.

![Select key from key vault](./media/configure-customer-managed-key/select-key-from-key-vault.png)

> [!NOTE]

> For redundancy, you can add up to three keys. If one of the keys has expired, or isn't accessible, the other keys are used for encryption.

4. Fill in the details for the key and click **Select**. This enables the encryption of the Microsoft-managed key with your key (customer-managed key).

## Managed identities

There are two types of managed identities that you can assign to an Event Hubs namespace.

- **System-assigned**: You can enable a managed identity directly on an Event Hubs namespace. When you enable a system-assigned managed identity, an identity is created in Microsoft Entra that's tied to the lifecycle of that Event Hubs namespace. So when the namespace is deleted, Azure automatically deletes the identity for you. By design, only that Azure resource (namespace) can use this identity to request tokens from Microsoft Entra ID.

- **User-assigned**: You can also create a managed identity as a standalone Azure resource, which is called user-assigned identity. You can create a user-assigned managed identity and assign it to one or more Event Hubs namespaces. In the case of user-assigned managed identities, the identity is managed separately from the resources that use it. They aren't tied to the lifecycle of the namespace. You can explicitly delete a user-assigned identity when you no longer need it.

For more information, see [What are managed identities for Azure resources?](../active-directory/managed-identities-azure-resources/overview.md).

## Encrypt using system-assigned identities (template)

This section shows how to do the following tasks using **Azure Resource Manager templates**.

1. Create an **Event Hubs namespace** with a managed service identity.

2. Create a **key vault** and grant the service identity access to the key vault.

3. Update the Event Hubs namespace with the key vault information (key/value).

### Create an Event Hubs cluster and namespace with managed service identity

This section shows you how to create an Azure Event Hubs namespace with managed service identity by using an Azure Resource Manager template and PowerShell.

1. Create an Azure Resource Manager template to create an Event Hubs namespace with a managed service identity. Name the file: **CreateEventHubClusterAndNamespace.json**:

```json

{

"$schema":"https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",

"contentVersion":"1.0.0.0",

"parameters":{

"clusterName":{

"type":"string",

"metadata":{

"description":"Name for the Event Hub cluster."

}

},

"namespaceName":{

"type":"string",

"metadata":{

"description":"Name for the Namespace to be created in cluster."

}

},

"location":{

"type":"string",

"defaultValue":"[resourceGroup().location]",

"metadata":{

"description":"Specifies the Azure location for all resources."

}

}

},

"resources":[

{

"type":"Microsoft.EventHub/clusters",

"apiVersion":"2018-01-01-preview",

"name":"[parameters('clusterName')]",

"location":"[parameters('location')]",

"sku":{

"name":"Dedicated",

"capacity":1

}

},

{

"type":"Microsoft.EventHub/namespaces",

"apiVersion":"2018-01-01-preview",

"name":"[parameters('namespaceName')]",

"location":"[parameters('location')]",

"identity":{

"type":"SystemAssigned"

},

"sku":{

"name":"Standard",

"tier":"Standard",

"capacity":1

},

"properties":{

"isAutoInflateEnabled":false,

"maximumThroughputUnits":0,

"clusterArmId":"[resourceId('Microsoft.EventHub/clusters', parameters('clusterName'))]"

},

"dependsOn":[

"[resourceId('Microsoft.EventHub/clusters', parameters('clusterName'))]"

]

}

],

"outputs":{

"EventHubNamespaceId":{

"type":"string",

"value":"[resourceId('Microsoft.EventHub/namespaces',parameters('namespaceName'))]"

}

}

}

```

2. Create a template parameter file named: **CreateEventHubClusterAndNamespaceParams.json**.

> [!NOTE]

> Replace the following values:

> - `<EventHubsClusterName>` - Name of your Event Hubs cluster

> - `<EventHubsNamespaceName>` - Name of your Event Hubs namespace

> - `<Location>` - Location of your Event Hubs namespace

```json

{

"$schema":"https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",

"contentVersion":"1.0.0.0",

"parameters":{

"clusterName":{

"value":"<EventHubsClusterName>"

},

"namespaceName":{

"value":"<EventHubsNamespaceName>"

},

"location":{

"value":"<Location>"

}

}

}

```

3. Run the following PowerShell command to deploy the template to create an Event Hubs namespace. Then, retrieve the ID of the Event Hubs namespace to use it later. Replace `{MyRG}` with the name of the resource group before running the command.

```powershell

$outputs = New-AzResourceGroupDeployment -Name CreateEventHubClusterAndNamespace -ResourceGroupName {MyRG} -TemplateFile ./CreateEventHubClusterAndNamespace.json -TemplateParameterFile ./CreateEventHubClusterAndNamespaceParams.json

$EventHubNamespaceId = $outputs.Outputs["eventHubNamespaceId"].value

```

### Grant Event Hubs namespace identity access to key vault

Set the key vault access policy so that the managed identity of the Event Hubs namespace can access key value in the key vault. Use the ID of the Event Hubs namespace from the previous section.

```powershell

$identity = (Get-AzureRmResource -ResourceId $EventHubNamespaceId -ExpandProperties).Identity

Set-AzureRmKeyVaultAccessPolicy -VaultName {keyVaultName} -ResourceGroupName {RGName} -ObjectId $identity.PrincipalId -PermissionsToKeys get,wrapKey,unwrapKey,list

```

### Encrypt data in Event Hubs namespace with customer-managed key from key vault

You have done the following steps so far:

1. Created a premium namespace with a managed identity.

2. Create a key vault and granted the managed identity access to the key vault.

In this step, you'll update the Event Hubs namespace with key vault information.

1. Create a JSON file named **CreateEventHubClusterAndNamespace.json** with the following content:

```json

{

"$schema":"https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",

"contentVersion":"1.0.0.0",

"parameters":{

"clusterName":{

"type":"string",

"metadata":{

"description":"Name for the Event Hub cluster."

}

},

"namespaceName":{

"type":"string",

"metadata":{

"description":"Name for the Namespace to be created in cluster."

}

},

"location":{

"type":"string",

"defaultValue":"[resourceGroup().location]",

"metadata":{

"description":"Specifies the Azure location for all resources."

}

},

"keyVaultUri":{

"type":"string",

"metadata":{

"description":"URI of the KeyVault."

}

},

"keyName":{

"type":"string",

"metadata":{

"description":"KeyName."

}

}

},

"resources":[

{

"type":"Microsoft.EventHub/namespaces",

"apiVersion":"2018-01-01-preview",

"name":"[parameters('namespaceName')]",

"location":"[parameters('location')]",

"identity":{

"type":"SystemAssigned"

},

"sku":{

"name":"Standard",

"tier":"Standard",

"capacity":1

},

"properties":{

"isAutoInflateEnabled":false,

"maximumThroughputUnits":0,

"clusterArmId":"[resourceId('Microsoft.EventHub/clusters', parameters('clusterName'))]",

"encryption":{

"keySource":"Microsoft.KeyVault",

"keyVaultProperties":[

{

"keyName":"[parameters('keyName')]",

"keyVaultUri":"[parameters('keyVaultUri')]"

}

]

}

}

}

]

}

```

2. Create a template parameter file: **UpdateEventHubClusterAndNamespaceParams.json**.

> [!NOTE]

> Replace the following values:

> - `<EventHubsClusterName>` - Name of your Event Hubs cluster.

> - `<EventHubsNamespaceName>` - Name of your Event Hubs namespace

> - `<Location>` - Location of your Event Hubs namespace

> - `<KeyVaultName>` - Name of your key vault

> - `<KeyName>` - Name of the key in the key vault

# [Key Vault](#tab/Key-Vault)

```json

{

"$schema":"https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",

"contentVersion":"1.0.0.0",

"parameters":{

"clusterName":{

"value":"<EventHubsClusterName>"

},

"namespaceName":{

"value":"<EventHubsNamespaceName>"

},

"location":{

"value":"<Location>"

},

"keyName":{

"value":"<KeyName>"

},

"keyVaultUri":{

"value":"https://<KeyVaultName>.vault.azure.net"

}

}

}

```

# [Key Vault Managed HSM](#tab/Key-Vault-Managed-HSM)

```json

{

"$schema":"https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",

"contentVersion":"1.0.0.0",

"parameters":{

"namespaceName":{

"value":"<ServiceBusNamespaceName>"

},

"location":{

"value":"<Location>"

},

"keyName":{

"value":"<KeyName>"

},

"keyVaultUri":{

"value":"https://<KeyVaultName>.managedhsm.azure.net"

}

}

}

```

---

3. Run the following PowerShell command to deploy the Resource Manager template. Replace `{MyRG}` with the name of your resource group before running the command.

```powershell

New-AzResourceGroupDeployment -Name UpdateEventHubNamespaceWithEncryption -ResourceGroupName {MyRG} -TemplateFile ./UpdateEventHubClusterAndNamespace.json -TemplateParameterFile ./UpdateEventHubClusterAndNamespaceParams.json

```

## Encrypt using user-assigned identities (template)

1. Create a **user-assigned identity**.

1. Create a **key vault** and grant access to the user-assigned identity via access policies.

1. Create an **Event Hubs namespace** with the managed user-identity and the key vault information.

### Create a user-assigned identity

Follow instructions from the [Create a user-assigned managed identity](../active-directory/managed-identities-azure-resources/how-to-manage-ua-identity-portal.md#create-a-user-assigned-managed-identity) article to create a user-assigned identity. You can also create a user-assigned identity using [CLI](../active-directory/managed-identities-azure-resources/how-to-manage-ua-identity-cli.md), [PowerShell](../active-directory/managed-identities-azure-resources/how-to-manage-ua-identity-powershell.md), [Azure Resource Manager template](../active-directory/managed-identities-azure-resources/how-to-manage-ua-identity-arm.md), and [REST](../active-directory/managed-identities-azure-resources/how-to-manage-ua-identity-rest.md).

> [!NOTE]

> You can assign up to **4** user identities to a namespace. These associations are deleted when the namespace is deleted or when you pass the `identity -> type` in the template to `None`.

### Grant access to user-assigned identity

1. Get the **Service principal ID** for the user identity using the following PowerShell command. In the example, `ud1` is the user-assigned identity to be used for encryption.

```azurepowershell-interactive

$servicePrincipal=Get-AzADServicePrincipal -SearchString "ud1"

```

1. Grant the user-assigned identity access to the key vault by assigning an access policy.

```azurepowershell-interactive

Set-AzureRmKeyVaultAccessPolicy -VaultName {keyVaultName} -ResourceGroupName {RGName} -ObjectId $servicePrincipal.Id -PermissionsToKeys get,wrapKey,unwrapKey,list

```

> [!NOTE]

> You can add up to **3** keys but the user identity used for encryption should be the same for all keys. Currently, only single encryption identity is supported.

### Create an Event Hubs namespace with user identity and key vault information

This section gives you an example that shows you how to do the following tasks using an Azure Resource Manager template.

1. Assign a user-managed identity to an Event Hubs namespace.

```json

"identity": {

"type": "UserAssigned",

"userAssignedIdentities": {

"[parameters('identity').userAssignedIdentity]": {}

}

},

```

1. Enable encryption on the namespace by specifying a key from your key vault and the user-managed identity to access the key.

```json

"encryption":{

"keySource":"Microsoft.KeyVault",

"keyVaultProperties":[

{

"keyName": "[parameters('keyName')]",

"keyVaultUri": "[parameters('keyVaultUri')]",

"identity": {

"userAssignedIdentity": "[parameters('identity').userAssignedIdentity]"

}

}

]

}

```

1. Create a JSON file named **CreateEventHubsNamespaceWithUserIdentityAndEncryption.json** with the following content:

```json

{

"$schema":"https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",

"contentVersion":"1.0.0.0",

"parameters":{

"clusterName":{

"type":"string",

"metadata":{

"description":"Name for the Event Hub cluster."

}

},

"namespaceName":{

"type":"string",

"metadata":{

"description":"Name for the Namespace to be created in cluster."

}

},

"location":{

"type":"string",

"defaultValue":"[resourceGroup().location]",

"metadata":{

"description":"Specifies the Azure location for all resources."

}

},

"keyVaultUri":{

"type":"string",

"metadata":{

"description":"URI of the KeyVault."

}

},

"keyName":{

"type":"string",

"metadata":{

"description":"KeyName."

},

"identity": {

"type": "Object",

"defaultValue": {

"userAssignedIdentity": ""

},

"metadata": {

"description": "user-assigned identity."

}

}

},

"resources":[

{

"type":"Microsoft.EventHub/clusters",

"apiVersion":"2018-01-01-preview",

"name":"[parameters('clusterName')]",

"location":"[parameters('location')]",

"sku":{

"name":"Dedicated",

"capacity":1

}

},

{

"type":"Microsoft.EventHub/namespaces",

"apiVersion":"2021-01-01-preview",

"name":"[parameters('namespaceName')]",

"location":"[parameters('location')]",

"sku":{

"name":"Standard",

"tier":"Standard",

"capacity":1

},

"identity": {

"type": "UserAssigned",

"userAssignedIdentities": {

"[parameters('identity').userAssignedIdentity]": {}

}

},

"properties":{

"encryption":{

"keySource":"Microsoft.KeyVault",

"keyVaultProperties":[

{

"keyName": "[parameters('keyName')]",

"keyVaultUri": "[parameters('keyVaultUri')]",

"identity": {

"userAssignedIdentity": "[parameters('identity').userAssignedIdentity]"

}

}

]

}

}

}

]

}

```

1. Create a template parameter file: **CreateEventHubsNamespaceWithUserIdentityAndEncryptionParams.json**.

# [Key Vault](#tab/Key-Vault)

```json

{

"$schema":"https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",

"contentVersion":"1.0.0.0",

"parameters":{

"namespaceName":{

"value":"<EventHubsNamespaceName>"

},

"location":{

"value":"<Location>"

},

"keyVaultUri":{

"value":"https://<KeyVaultName>.vault.azure.net"

},

"keyName":{

"value":"<KeyName>"

},

"identity": {

"value": {

"userAssignedIdentity": "/subscriptions/<AZURE SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP NAME>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER MANAGED IDENTITY NAME>"

}

}

}

}

```

# [Key Vault Managed HSM](#tab/Key-Vault-Managed-HSM)

```json

{

"$schema":"https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",

"contentVersion":"1.0.0.0",

"parameters":{

"namespaceName":{

"value":"<ServiceBusNamespaceName>"

},

"location":{

"value":"<Location>"

},

"keyVaultUri":{

"value":"https://<KeyVaultName>.managedhsm.azure.net"

},

"keyName":{

"value":"<KeyName>"

},

"identity": {

"value": {

"userAssignedIdentity": "/subscriptions/<AZURE SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP NAME>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER MANAGED IDENTITY NAME>"

}

}

}

}

```

---

In the parameter file, replace placeholders with appropriate values.

| Placeholder | value |

| ----------- | ----- |

| `<EventHubsNamespaceName>` | Name of the Event Hubs namespace. |

| `<Location>` | Location where you want the namespace to be created. |

| `<KeyVaultName>` | Name of the key vault. |

| `<KeyName>` | Name of the key in the key vault. |

| `<AZURE SUBSCRIPTION ID>` | Your Azure subscription ID. |

| `<RESOURCE GROUP NAME>` | Resource group of the user-managed identity. |

| `<USER MANAGED IDENTITY NAME>` | Name of the user-managed identity. |

1. Run the following PowerShell command to deploy the Resource Manager template. Replace `{MyRG}` with the name of your resource group before running the command.

```azurepowershell-interactive

New-AzResourceGroupDeployment -Name CreateEventHubsNamespaceWithEncryption -ResourceGroupName {MyRG} -TemplateFile ./ CreateEventHubsNamespaceWithUserIdentityAndEncryption.json -TemplateParameterFile ./ CreateEventHubsNamespaceWithUserIdentityAndEncryptionParams.json

```

## Use both user-assigned and system-assigned identities

A namespace can have both system-assigned and user-assigned identities at the same time. In this case, the `type` property would be `SystemAssigned`, `UserAssigned` as shown in the following example.

```json

"identity": {

"type": "SystemAssigned, UserAssigned",

"userAssignedIdentities": {

"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<userIdentity1>" : {}

}

}

```

In this scenario, you can choose either the system-assigned identity or the user-assigned identity for encrypting the data at rest.

In the Resource Manager template, if you don't specify an `identity` attribute, the system-managed identity is used. Here's an example snippet.

```json

"properties":{

"encryption":{

"keySource":"Microsoft.KeyVault",

"keyVaultProperties":[

{

"keyName":"[parameters('keyName')]",

"keyVaultUri":"[parameters('keyVaultUri')]"

}

]

}

}

```

See the following example for using the user-managed identity for the encryption. Notice the `identity` attribute is set to the user-managed identity.

```json

"properties":{

"encryption":{

"keySource":"Microsoft.KeyVault",

"keyVaultProperties":[

{

"keyName":"[parameters('keyName')]",

"keyVaultUri":"[parameters('keyVaultUri')]",

"identity": {

"userAssignedIdentity": "[parameters('identity').userAssignedIdentity]"

}

}

]

}

}

```

## Enable infrastructure (or double) encryption of data

If you require a higher level of assurance that your data is secure, you can enable infrastructure level encryption which is also known as Double Encryption.

When infrastructure encryption is enabled, data in the Event Hubs namespace account is encrypted twice, once at the service level and once at the infrastructure level, using two different encryption algorithms and two different keys. Hence, infrastructure encryption of Event Hubs data protects against a scenario where one of the encryption algorithms or keys can be compromised.

You can enable infrastructure encryption by updating the Azure Resource Manager template with `requireInfrastructureEncryption` property in the above **CreateEventHubClusterAndNamespace.json** as shown in the following example.

```json

"properties":{

"isAutoInflateEnabled":false,

"maximumThroughputUnits":0,

"clusterArmId":"[resourceId('Microsoft.EventHub/clusters', parameters('clusterName'))]",

"encryption":{

"keySource":"Microsoft.KeyVault",

"requireInfrastructureEncryption":true,

"keyVaultProperties":[

{

"keyName":"[parameters('keyName')]",

"keyVaultUri":"[parameters('keyVaultUri')]"

}

]

}

}

```

## Rotate, revoke, and cache encryption keys

### Rotate your encryption keys

You can rotate your key in the key vault by using the Azure Key Vaults rotation mechanism. Activation and expiration dates can also be set to automate key rotation. The Event Hubs service detects new key versions and start using them automatically.

### Revoke access to keys

Revoking access to the encryption keys won't purge the data from Event Hubs. However, the data can't be accessed from the Event Hubs namespace. You can revoke the encryption key through access policy or by deleting the key. Learn more about access policies and securing your key vault from [Secure access to a key vault](/azure/key-vault/general/security-features).

Once the encryption key is revoked, the Event Hubs service on the encrypted namespace becomes inoperable. If the access to the key is enabled or the delete key is restored, Event Hubs service picks the key so you can access the data from the encrypted Event Hubs namespace.

### Caching of keys

The Event Hubs instance (event hub) polls its listed encryption keys every 5 minutes. It caches and uses them until the next poll, which is after 5 minutes. As long as at least one key is available, the event hub is accessible. If all listed keys are inaccessible when it polls, all event hubs become unavailable.

Here are more details:

- Every 5 minutes, the Event Hubs service polls all customer-managed keys listed in the namespace’s record:

- If a key has been rotated, the record is updated with the new key.

- If a key has been revoked, the key is removed from the record.

- If all keys have been revoked, the namespace’s encryption status is set to **Revoked**. The data can't be accessed from the Event Hubs namespace.'

## Considerations when using geo-disaster recovery

> [!IMPORTANT]

> To enable Geo-DR on a namespace that's using the BYOK encryption, the secondary namespace for pairing must have a system-assigned or user-assigned managed identity enabled on it.

### Geo-disaster recovery - encryption with system-assigned identities

To enable encryption of Microsoft-managed key with a customer managed key, an [access policy](/azure/key-vault/general/secure-your-key-vault) is set up for a system-assigned managed identity on the specified Azure KeyVault. This ensures controlled access to the Azure KeyVault from the Azure Event Hubs namespace.

Due to this:

- If [Geo disaster recovery](event-hubs-geo-dr.md) is already enabled for the Event Hubs namespace and you're looking to enable customer managed key, then

- Break the pairing.

- [Set up the access policy](/azure/key-vault/general/assign-access-policy-portal) for the system-assigned managed identity for both the primary and secondary namespaces to the key vault.

- Set up encryption on the primary namespace.

- Re-pair the primary and secondary namespaces.

- If you're looking to enable Geo-DR on an Event Hubs namespace where customer-managed key is already set up, then follow these steps:

- [Set up the access policy](/azure/key-vault/general/assign-access-policy-portal) for the managed identity for the secondary namespace to the key vault.

- Pair the primary and secondary namespaces.

### Geo-disaster recovery - encryption with user-assigned identities

Here are a few recommendations:

1.	Create managed identity and assign Key Vault permissions to your managed identity.

2.	Add the identity as a user assigned identity, and enable encryption with the identity on both namespaces.

3.	Pair namespaces together

Conditions for enabling Geo-DR and Encryption with User-Assigned Identities:

1.	Secondary namespace must already have Encryption enabled with a User-Assigned identity if it's to be paired with a primary namespace that has Encryption enabled.

2.	It isn't possible to enable Encryption on an already paired primary, even if the secondary has a User-Assigned identity associated with the namespace.

## Set up diagnostic logs

Setting diagnostic logs for BYOK enabled namespaces gives you the required information about the operations. These logs can be enabled and later stream to an event hub or analyzed through log analytics or streamed to storage to perform customized analytics. To learn more about diagnostic logs, see [Overview of Azure Diagnostic logs](/azure/azure-monitor/essentials/platform-logs-overview). For the schema, see [Monitor data reference](monitor-event-hubs-reference.md#customer-managed-key-user-logs-schema).

## Customer Lockbox for Microsoft Azure

[Customer Lockbox for Microsoft Azure](/azure/security/fundamentals/customer-lockbox-overview) doesn't apply to Azure Event Hubs. Microsoft personnel don't access customer event data during support operations. Microsoft personnel only have access to the following metadata:

- Names of Event Hubs entities (event hubs)

- Configuration settings for the namespace and its entities

Event data headers and event body content aren't accessible to Microsoft personnel. Additionally, event data is serialized to binary format on the client side before being sent to the Event Hubs service, so it isn't stored or viewable in a human-readable form on the server. As a result, Customer Lockbox approval isn't required for Azure Event Hubs support scenarios.

## Next steps

See the following articles:

- [Event Hubs overview](event-hubs-about.md)

- [Key Vault overview](/azure/key-vault/general/overview)


# Transport Layer Security Configure Minimum Version

# Configure the minimum TLS version for an Event Hubs namespace

Azure Event Hubs namespaces permit clients to send and receive data with TLS 1.0 and above. To enforce stricter security measures, you can configure your Event Hubs namespace to require that clients send and receive data with a newer version of TLS. If an Event Hubs namespace requires a minimum version of TLS, then any requests made with an older version will fail. For conceptual information about this feature, see [Enforce a minimum required version of Transport Layer Security (TLS) for requests to an Event Hubs namespace](transport-layer-security-enforce-minimum-version.md).

You can configure the minimum TLS version using the Azure portal or Azure Resource Manager (ARM) template.

## Specify the minimum TLS version in the Azure portal

You can specify the minimum TLS version when creating an Event Hubs namespace in the Azure portal on the **Advanced** tab.

You can also specify the minimum TLS version for an existing namespace on the **Configuration** page.

## Create a template to configure the minimum TLS version

To configure the minimum TLS version for an Event Hubs namespace with a template, create a template with the  `MinimumTlsVersion`  property set to 1.0, 1.1, or 1.2. When you create an Event Hubs namespace with an Azure Resource Manager template, the `MinimumTlsVersion` property is set to 1.2 by default, unless explicitly set to another version.

> [!NOTE]

> Namespaces created using an api-version prior to 2022-01-01-preview will have 1.0 as the value for `MinimumTlsVersion`. This behavior was the prior default, and is still there for backwards compatibility.

The following steps describe how to create a template in the Azure portal.

1. In the Azure portal, choose  **Create a resource**.

2. In  **Search the Marketplace** , type  **custom deployment** , and then press  **ENTER**.

3. Choose **Custom deployment (deploy using custom templates) (preview)**, choose  **Create** , and then choose  **Build your own template in the editor**.

4. In the template editor, paste in the following JSON to create a new namespace and set the minimum TLS version to TLS 1.2. Remember to replace the placeholders in angle brackets with your own values.

```json

{

"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {},

"variables": {

"eventHubNamespaceName": "[concat(uniqueString(subscription().subscriptionId), 'tls')]"

},

"resources": [

{

"name": "[variables('eventHubNamespaceName')]",

"type": "Microsoft.EventHub/namespaces",

"apiVersion": "2022-01-01-preview",

"location": "westeurope",

"properties": {

"minimumTlsVersion": "1.2"

},

"dependsOn": [],

"tags": {}

}

]

}

```

5. Save the template.

6. Specify resource group parameter, then choose the  **Review + create**  button to deploy the template and create a namespace with the  `MinimumTlsVersion`  property configured.

> [!NOTE]

> After you update the minimum TLS version for the Event Hubs namespace, it may take up to 30 seconds before the change is fully propagated.

Configuring the minimum TLS version requires api-version 2022-01-01-preview or later of the Azure Event Hubs resource provider.

## Check the minimum required TLS version for a namespace

To check the minimum required TLS version for your Event Hubs namespace, you can query the Azure Resource Manager API. You'll need a Bearer token to query against the API, which you can retrieve using the [ARMClient](https://github.com/projectkudu/ARMClient) app by executing the following commands.

```powershell

.\ARMClient.exe login

.\ARMClient.exe token <your-subscription-id>

```

Once you have your bearer token, you can use the script below in combination with something like [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) to query the API.

```http

@token = Bearer <Token received from ARMClient>

@subscription = <your-subscription-id>

@resourceGroup = <your-resource-group-name>

@namespaceName = <your-namespace-name>

###

GET https://management.azure.com/subscriptions/{{subscription}}/resourceGroups/{{resourceGroup}}/providers/Microsoft.EventHub/namespaces/{{namespaceName}}?api-version=2022-01-01-preview

content-type: application/json

Authorization: {{token}}

```

The response should look something like the below, with the minimumTlsVersion set under the properties.

```json

{

"sku": {

"name": "Premium",

"tier": "Premium",

"capacity": 1

},

"id": "/subscriptions/<your-subscription-id>/resourceGroups/<your-resource-group-name>/providers/Microsoft.EventHub/namespaces/<your-namespace-name>",

"name": "<your-namespace-name>",

"type": "Microsoft.EventHub/Namespaces",

"location": "West Europe",

"properties": {

"minimumTlsVersion": "1.2",

"publicNetworkAccess": "Enabled",

"disableLocalAuth": false,

"zoneRedundant": true,

"isAutoInflateEnabled": false,

"maximumThroughputUnits": 0,

"kafkaEnabled": true,

"provisioningState": "Succeeded",

"status": "Active"

}

}

```

## Test the minimum TLS version from a client

To test that the minimum required TLS version for an Event Hubs namespace forbids calls made with an older version, you can configure a client to use an older version of TLS. For more information about configuring a client to use a specific version of TLS, see [Configure Transport Layer Security (TLS) for a client application](transport-layer-security-configure-client-version.md).

When a client accesses an Event Hubs namespace using a TLS version that doesn't meet the minimum TLS version configured for the namespace, Azure Event Hubs returns error code 401 (Unauthorized) and a message indicating that the TLS version that was used isn't permitted for making requests against this Event Hubs namespace.

> [!NOTE]

> Due to limitations in the confluent library, errors coming from an invalid TLS version will not surface when connecting through the Kafka protocol. Instead a general exception will be shown.

> [!NOTE]

> When you configure a minimum TLS version for an Event Hubs namespace, that minimum version is enforced at the application layer. Tools that attempt to determine TLS support at the protocol layer may return TLS versions in addition to the minimum required version when run directly against the Event Hubs namespace endpoint.

## Next steps

For more information, see the following articles.

- [Enforce a minimum required version of Transport Layer Security (TLS) for requests to an Event Hubs namespace](transport-layer-security-enforce-minimum-version.md)

- [Configure Transport Layer Security (TLS) for an Event Hubs client application](transport-layer-security-configure-client-version.md)

- [Use Azure Policy to audit for compliance of minimum TLS version for an Event Hubs namespace](transport-layer-security-audit-minimum-version.md)


# Transport Layer Security Audit Minimum Version

# Use Azure Policy to audit for compliance of minimum TLS version for an Azure Event Hubs namespace

If you have a large number of Microsoft Azure Event Hubs namespaces, you may want to perform an audit to make sure that all namespaces are configured for the minimum version of TLS that your organization requires. To audit a set of Event Hubs namespaces for their compliance, use Azure Policy. Azure Policy is a service that you can use to create, assign, and manage policies that apply rules to Azure resources. Azure Policy helps you to keep those resources compliant with your corporate standards and service level agreements. For more information, see [Overview of Azure Policy](../governance/policy/overview.md).

## Create a policy with an audit effect

Azure Policy supports effects that determine what happens when a policy rule is evaluated against a resource. The audit effect creates a warning when a resource is not in compliance, but does not stop the request. For more information about effects, see [Understand Azure Policy effects](../governance/policy/concepts/effects.md).

To create a policy with an audit effect for the minimum TLS version with the Azure portal, follow these steps:

1. In the Azure portal, navigate to the Azure Policy service.

2. Under the  **Authoring**  section, select  **Definitions**.

3. Select  **Add policy definition**  to create a new policy definition.

4. For the  **Definition location**  field, select the  **More**  button to specify where the audit policy resource is located.

5. Specify a name for the policy. You can optionally specify a description and category.

6. Under  **Policy rule** , add the following policy definition to the  **policyRule**  section.

```json

{

"policyRule": {

"if": {

"allOf": [

{

"field": "type",

"equals": "Microsoft.EventHub/namespaces"

},

{

"not": {

"field": "Microsoft.EventHub/namespaces/minimumTlsVersion",

"equals": "1.2"

}

}

]

},

"then": {

"effect": "audit"

}

}

}

```

7. Save the policy.

### Assign the policy

Next, assign the policy to a resource. The scope of the policy corresponds to that resource and any resources beneath it. For more information on policy assignment, see [Azure Policy assignment structure](../governance/policy/concepts/assignment-structure.md).

To assign the policy with the Azure portal, follow these steps:

1. In the Azure portal, navigate to the Azure Policy service.

2. Under the  **Authoring**  section, select  **Assignments**.

3. Select  **Assign policy**  to create a new policy assignment.

4. For the  **Scope**  field, select the scope of the policy assignment.

5. For the  **Policy definition**  field, select the  **More**  button, then select the policy you defined in the previous section from the list.

6. Provide a name for the policy assignment. The description is optional.

7. Leave  **Policy enforcement**  set to _Enabled_. This setting has no effect on the audit policy.

8. Select  **Review + create**  to create the assignment.

### View compliance report

After you have assigned the policy, you can view the compliance report. The compliance report for an audit policy provides information on which Event Hubs namespaces are not in compliance with the policy. For more information, see [Get policy compliance data](../governance/policy/how-to/get-compliance-data.md).

It may take several minutes for the compliance report to become available after the policy assignment is created.

To view the compliance report in the Azure portal, follow these steps:

1. In the Azure portal, navigate to the Azure Policy service.

2. Select  **Compliance**.

3. Filter the results for the name of the policy assignment that you created in the previous step. The report shows how many resources are not in compliance with the policy.

4. You can drill down into the report for additional details, including a list of Event Hubs namespaces that are not in compliance.

## Use Azure Policy to enforce the minimum TLS version

Azure Policy supports cloud governance by ensuring that Azure resources adhere to requirements and standards. To enforce a minimum TLS version requirement for the Event Hubs namespaces in your organization, you can create a policy that prevents the creation of a new Event Hubs namespace that sets the minimum TLS requirement to an older version of TLS than that which is dictated by the policy. This policy will also prevent all configuration changes to an existing namespace if the minimum TLS version setting for that namespace is not compliant with the policy.

The enforcement policy uses the deny effect to prevent a request that would create or modify an Event Hubs namespace so that the minimum TLS version no longer adheres to your organization's standards. For more information about effects, see [Understand Azure Policy effects](../governance/policy/concepts/effects.md).

To create a policy with a deny effect for a minimum TLS version that is less than TLS 1.2, provide the following JSON in the  **policyRule**  section of the policy definition:

```json

{

"policyRule": {

"if": {

"allOf": [

{

"field": "type",

"equals": " Microsoft.EventHub/namespaces"

},

{

"not": {

"field": " Microsoft.EventHub/namespaces/minimumTlsVersion",

"equals": "1.2"

}

}

]

},

"then": {

"effect": "deny"

}

}

}

```

After you create the policy with the deny effect and assign it to a scope, a user cannot create an Event Hubs namespace with a minimum TLS version that is older than 1.2. Nor can a user make any configuration changes to an existing Event Hubs namespace that currently requires a minimum TLS version that is older than 1.2. Attempting to do so results in an error. The required minimum TLS version for the Event Hubs namespace must be set to 1.2 to proceed with namespace creation or configuration.

An error will be shown if you try to create an Event Hubs namespace with the minimum TLS version set to TLS 1.0 when a policy with a deny effect requires that the minimum TLS version be set to TLS 1.2.

## Next steps

See the following documentation for more information.

- [Enforce a minimum required version of Transport Layer Security (TLS) for requests to an Event Hubs namespace](transport-layer-security-enforce-minimum-version.md)

- [Configure the minimum TLS version for an Event Hubs namespace](transport-layer-security-configure-minimum-version.md)

- [Configure Transport Layer Security (TLS) for an Event Hubs client application](transport-layer-security-configure-client-version.md)


# Transport Layer Security Configure Client Version

# Configure Transport Layer Security (TLS) for an Event Hubs client application

For security purposes, an Azure Event Hubs namespace may require that clients use a minimum version of Transport Layer Security (TLS) to send requests. Calls to Azure Event Hubs will fail if the client is using a version of TLS that is lower than the minimum required version. For example, if a namespace requires TLS 1.2, then a request sent by a client who is using TLS 1.1 will fail.

This article describes how to configure a client application to use a particular version of TLS. For information about how to configure a minimum required version of TLS for an Azure Event Hubs namespace, see [Enforce a minimum required version of Transport Layer Security (TLS) for requests to an Event Hubs namespace](transport-layer-security-configure-minimum-version.md).

## Configure the client TLS version

In order for a client to send a request with a particular version of TLS, the operating system must support that version.

The following example shows how to set the client's TLS version to 1.2 from .NET. The .NET Framework used by the client must support TLS 1.2. For more information, see [Support for TLS 1.2](/dotnet/framework/network-programming/tls#support-for-tls-12).

# [.NET](#tab/dotnet)

The following sample shows how to enable TLS 1.2 in a .NET client using the Azure.Messaging.ServiceBus client library of Event Hubs:

```csharp

{

// Enable TLS 1.2 before connecting to Event Hubs

System.Net.ServicePointManager.SecurityProtocol = System.Net.SecurityProtocolType.Tls12;

// Connection string to your Event Hubs namespace

string connectionString = "<NAMESPACE CONNECTION STRING>";

// Name of your Event Hub

string eventHubName = "<EVENT HUB NAME>";

// The sender used to publish messages to the queue

var producer = new EventHubProducerClient(connectionString, eventHubName);

// Use the producer client to send a message to the Event Hubs queue

using EventDataBatch eventBatch = await producer.CreateBatchAsync();

var eventData = new EventData("This is an event body");

if (!eventBatch.TryAdd(eventData))

{

throw new Exception($"The event could not be added.");

}

}

```

---

## Verify the TLS version used by a client

To verify that the specified version of TLS was used by the client to send a request, you can use [Fiddler](https://www.telerik.com/fiddler) or a similar tool. Open Fiddler to start capturing client network traffic, then execute one of the examples in the previous section. Look at the Fiddler trace to confirm that the correct version of TLS was used to send the request.

## Next steps

See the following documentation for more information.

- [Enforce a minimum required version of Transport Layer Security (TLS) for requests to an Event Hubs namespace](transport-layer-security-enforce-minimum-version.md)

- [Configure the minimum TLS version for an Event Hubs namespace](transport-layer-security-configure-minimum-version.md)

- [Use Azure Policy to audit for compliance of minimum TLS version for an Event Hubs namespace](transport-layer-security-audit-minimum-version.md)


# Passwordless Migration Event Hubs

# Migrate an application to use passwordless connections with Azure Event Hubs

[!INCLUDE [passwordless-intro](../../includes/passwordless/migration-guide/passwordless-intro.md)]

## Configure your local development environment

Passwordless connections can be configured to work for both local and Azure-hosted environments. In this section, you apply configurations to allow individual users to authenticate to Azure Event Hubs for local development.

### Assign user roles

[!INCLUDE [assign-roles-event-hubs](../../includes/assign-roles-event-hubs.md)]

### Sign-in to Azure locally

[!INCLUDE [default-azure-credential-sign-in](~/reusable-content/ce-skilling/azure/includes/passwordless/default-azure-credential-sign-in.md)]

### Update the application code to use passwordless connections

The Azure Identity client library, for each of the following ecosystems, provides a `DefaultAzureCredential` class that handles passwordless authentication to Azure:

- [.NET](/dotnet/api/overview/azure/Identity-readme?view=azure-dotnet&preserve-view=true#defaultazurecredential)

- [C++](https://github.com/Azure/azure-sdk-for-cpp/blob/main/sdk/identity/azure-identity/README.md#defaultazurecredential)

- [Go](https://pkg.go.dev/github.com/Azure/azure-sdk-for-go/sdk/azidentity#readme-defaultazurecredential)

- [Java](/java/api/overview/azure/identity-readme?view=azure-java-stable&preserve-view=true#defaultazurecredential)

- [Node.js](/javascript/api/overview/azure/identity-readme?view=azure-node-latest&preserve-view=true#defaultazurecredential)

- [Python](/python/api/overview/azure/identity-readme?view=azure-python&preserve-view=true#defaultazurecredential)

`DefaultAzureCredential` supports multiple authentication methods. The method to use is determined at runtime. This approach enables your app to use different authentication methods in different environments (local vs. production) without implementing environment-specific code. See the preceding links for the order and locations in which `DefaultAzureCredential` looks for credentials.

## [.NET](#tab/dotnet)

1. To use `DefaultAzureCredential` in a .NET application, install the `Azure.Identity` package:

```dotnetcli

dotnet add package Azure.Identity

```

1. At the top of your file, add the following code:

```csharp

using Azure.Identity;

```

1. Identify the locations in your code that create an `EventHubProducerClient` or `EventProcessorClient` object to connect to Azure Event Hubs. Update your code to match the following example:

```csharp

DefaultAzureCredential credential = new();

var eventHubNamespace = $"https://{namespace}.servicebus.windows.net";

// Event Hubs producer

EventHubProducerClient producerClient = new(

eventHubNamespace,

eventHubName,

credential);

// Event Hubs processor

EventProcessorClient processorClient = new(

storageClient,

EventHubConsumerClient.DefaultConsumerGroupName,

eventHubNamespace,

eventHubName,

credential);

```

## [Go](#tab/go)

1. To use `DefaultAzureCredential` in a Go application, install the `azidentity` module:

```bash

go get -u github.com/Azure/azure-sdk-for-go/sdk/azidentity

```

1. At the top of your file, add the following code:

```go

import (

"github.com/Azure/azure-sdk-for-go/sdk/azidentity"

)

```

1. Identify the locations in your code that create a `ProducerClient` or `ConsumerClient` instance to connect to Azure Event Hubs. Update your code to match the following example:

```go

credential, err := azidentity.NewDefaultAzureCredential(nil)

eventHubNamespace := fmt.Sprintf(

"https://%s.servicebus.windows.net",

namespace)

if err != nil {

// handle error

}

// Event Hubs producer

producerClient, err = azeventhubs.NewProducerClient(

eventHubNamespace,

eventHubName,

credential,

nil)

if err != nil {

// handle error

}

// Event Hubs processor

processorClient, err = azeventhubs.NewConsumerClient(

eventHubNamespace,

eventHubName,

azeventhubs.DefaultConsumerGroup,

credential,

nil)

if err != nil {

// handle error

}

```

## [Java](#tab/java)

1. To use `DefaultAzureCredential` in a Java application, install the `azure-identity` package via one of the following approaches:

1. [Include the BOM file](/java/api/overview/azure/identity-readme?view=azure-java-stable&preserve-view=true#include-the-bom-file).

1. [Include a direct dependency](/java/api/overview/azure/identity-readme?view=azure-java-stable&preserve-view=true#include-direct-dependency).

1. At the top of your file, add the following code:

```java

import com.azure.identity.DefaultAzureCredentialBuilder;

```

1. Identify the locations in your code that create an `EventHubProducerClient` or `EventProcessorClient` object to connect to Azure Event Hubs. Update your code to match the following example:

```java

DefaultAzureCredential credential = new DefaultAzureCredentialBuilder()

.build();

String eventHubNamespace = "https://" + namespace + ".servicebus.windows.net";

// Event Hubs producer

EventHubProducerClient producerClient = new EventHubClientBuilder()

.credential(eventHubNamespace, eventHubName, credential)

.buildProducerClient();

// Event Hubs processor

EventProcessorClient processorClient = new EventProcessorClientBuilder()

.consumerGroup(consumerGroupName)

.credential(eventHubNamespace, eventHubName, credential)

.checkpointStore(new SampleCheckpointStore())

.processEvent(eventContext -> {

System.out.println(

"Partition ID = " +

eventContext.getPartitionContext().getPartitionId() +

" and sequence number of event = " +

eventContext.getEventData().getSequenceNumber());

})

.processError(errorContext -> {

System.out.println(

"Error occurred while processing events " +

errorContext.getThrowable().getMessage());

})

.buildEventProcessorClient();

```

## [Node.js](#tab/nodejs)

1. To use `DefaultAzureCredential` in a Node.js application, install the `@azure/identity` package:

```bash

npm install --save @azure/identity

```

1. At the top of your file, add the following code:

```nodejs

import { DefaultAzureCredential } from "@azure/identity";

```

1. Identify the locations in your code that create an `EventHubProducerClient` or `EventHubConsumerClient` object to connect to Azure Event Hubs. Update your code to match the following example:

```nodejs

const credential = new DefaultAzureCredential();

const eventHubNamespace = `https://${namespace}.servicebus.windows.net`;

// Event Hubs producer

const producerClient = new EventHubProducerClient(

eventHubNamespace,

eventHubName,

credential);

// Event Hubs processor

const processorClient = new EventHubConsumerClient(

consumerGroupName,

eventHubNamespace,

eventHubName,

credential

);

```

## [Python](#tab/python)

1. To use `DefaultAzureCredential` in a Python application, install the `azure-identity` package:

```bash

pip install azure-identity

```

1. At the top of your file, add the following code:

```python

from azure.identity import DefaultAzureCredential

```

1. Identify the locations in your code that create an `EventHubProducerClient` or `EventHubConsumerClient` object to connect to Azure Event Hubs. Update your code to match the following example:

```python

credential = DefaultAzureCredential()

event_hub_namespace = "https://%s.servicebus.windows.net" % namespace

# Event Hubs producer

producer_client = EventHubProducerClient(

fully_qualified_namespace = event_hub_namespace,

eventhub_name = event_hub_name,

credential = credential

)

# Event Hubs processor

processor_client = EventHubConsumerClient(

fully_qualified_namespace = event_hub_namespace,

eventhub_name = event_hub_name,

consumer_group = "$Default",

checkpoint_store = checkpoint_store,

credential = credential

)

```

---

4. Make sure to update the event hubs namespace in the URI of your `EventHubProducerClient` or `EventProcessorClient` objects. You can find the namespace name on the overview page of the Azure portal.

### Run the app locally

After making these code changes, run your application locally. The new configuration should pick up your local credentials, such as the Azure CLI, Visual Studio, or IntelliJ. The roles you assigned to your user in Azure allows your app to connect to the Azure service locally.

## Configure the Azure hosting environment

Once your application is configured to use passwordless connections and runs locally, the same code can authenticate to Azure services after it's deployed to Azure. The sections that follow explain how to configure a deployed application to connect to Azure Event Hubs using a [managed identity](/azure/active-directory/managed-identities-azure-resources/overview). Managed identities provide an automatically managed identity in Microsoft Entra ID for applications to use when connecting to resources that support Microsoft Entra authentication. Learn more about managed identities:

* [Passwordless Overview](/azure/developer/intro/passwordless-overview)

* [Managed identity best practices](/azure/active-directory/managed-identities-azure-resources/managed-identity-best-practice-recommendations)

### Create the managed identity

[!INCLUDE [create-user-assigned-managed-identity](~/reusable-content/ce-skilling/azure/includes/passwordless/migration-guide/create-user-assigned-managed-identity.md)]

#### Associate the managed identity with your web app

You need to configure your web app to use the managed identity you created. Assign the identity to your app using either the Azure portal or the Azure CLI.

# [Azure portal](#tab/azure-portal-associate)

Complete the following steps in the Azure portal to associate an identity with your app. These same steps apply to the following Azure services:

* Azure Spring Apps

* Azure Container Apps

* Azure virtual machines

* Azure Kubernetes Service

1. Navigate to the overview page of your web app.

1. Select **Identity** from the left navigation.

1. On the **Identity** page, switch to the **User assigned** tab.

1. Select **+ Add** to open the **Add user assigned managed identity** flyout.

1. Select the subscription you used previously to create the identity.

1. Search for the **MigrationIdentity** by name and select it from the search results.

1. Select **Add** to associate the identity with your app.

# [Azure CLI](#tab/azure-cli-associate)

[!INCLUDE [associate-managed-identity-cli](~/reusable-content/ce-skilling/azure/includes/passwordless/migration-guide/associate-managed-identity-cli.md)]

# [Service Connector](#tab/service-connector-associate)

[!INCLUDE [service-connector-commands-event-hubs](../../includes/passwordless/migration-guide/service-connector-commands-event-hubs.md)]

---

### Assign roles to the managed identity

Next, you need to grant permissions to the managed identity you created to access your event hub. Grant permissions by assigning a role to the managed identity, just like you did with your local development user.

### [Azure portal](#tab/assign-role-azure-portal)

1. Navigate to your event hub overview page and select **Access Control (IAM)** from the left navigation.

1. Choose **Add role assignment**

1. In the **Role** search box, search for *Azure Event Hubs Data Sender*, which is a common role used to manage data operations for queues. You can assign whatever role is appropriate for your use case. Select the *Azure Event Hubs Data Sender* from the list and choose **Next**.

1. On the **Add role assignment** screen, for the **Assign access to** option, select **Managed identity**. Then choose **+Select members**.

1. In the flyout, search for the managed identity you created by name and select it from the results. Choose **Select** to close the flyout menu.

1. Select **Next** a couple times until you're able to select **Review + assign** to finish the role assignment.

1. Repeat these steps for the **Azure Event Hub Data Receiver** role.

### [Azure CLI](#tab/assign-role-azure-cli)

To assign a role at the resource level using the Azure CLI, you first must retrieve the resource ID using the [`az eventhubs eventhub show`](/cli/azure/eventhubs/eventhub) show command. You can filter the output properties using the `--query` parameter.

```azurecli

az eventhubs eventhub show \

--resource-group '<your-resource-group-name>' \

--namespace-name '<your-event-hubs-namespace>' \

--name '<your-event-hub-name>' \

--query id

```

Copy the output ID from the preceding command. You can then assign roles using the [az role assignment](/cli/azure/role/assignment) command of the Azure CLI.

```azurecli

az role assignment create --assignee "<user@domain>" \

--role "Azure Event Hubs Data Receiver" \

--scope "<your-resource-id>"

az role assignment create --assignee "<user@domain>" \

--role "Azure Event Hubs Data Sender" \

--scope "<your-resource-id>"

```

### [Service Connector](#tab/assign-role-service-connector)

If you connected your services using Service Connector you don't need to complete this step. The necessary role configurations were handled for you when you ran the Service Connector CLI commands.

---

[!INCLUDE [Code changes to use user-assigned managed identity](~/reusable-content/ce-skilling/azure/includes/passwordless/migration-guide/passwordless-user-assigned-managed-identity.md)]

### Test the app

After deploying the updated code, browse to your hosted application in the browser. Your app should be able to connect to the event hub successfully. Keep in mind that it can take several minutes for the role assignments to propagate through your Azure environment. Your application is now configured to run both locally and in a production environment without the developers having to manage secrets in the application itself.

## Next steps

In this tutorial, you learned how to migrate an application to passwordless connections.

You can read the following resources to explore the concepts discussed in this article in more depth:

* [Passwordless connections for Azure services](/azure/developer/intro/passwordless-overview)

* To learn more about .NET, see [Get started with .NET in 10 minutes](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro).


# Troubleshooting Guide

# Troubleshoot connectivity issues - Azure Event Hubs

If your client application can't connect to an event hub, use this article to diagnose and resolve the issue. Connectivity problems fall into two categories: permanent issues (the connection never succeeds) and transient issues (intermittent failures).

For **permanent issues**, check these settings and other options mentioned in the [Troubleshoot permanent connectivity issues](#troubleshoot-permanent-connectivity-issues) section:

- Connection string

- Your organization's firewall settings

- IP firewall settings

- Network security settings (service endpoints, private endpoints, and more)

For **transient issues**, try the following options that can help with troubleshooting the issues. For more information, see [Troubleshoot transient connectivity problems](#troubleshoot-transient-connectivity-problems).

- Upgrade to latest version of the SDK

- Run commands to check dropped packets

- Obtain network traces.

## Troubleshoot permanent connectivity issues

If the application can't connect to the event hub at all, follow the steps in this section to troubleshoot the issue.

### Check if there's a service outage

Check for the Azure Event Hubs service outage on the [Azure service status site](https://azure.microsoft.com/status/).

### Verify the connection string

Verify that the connection string you're using is correct. See [Get connection string](event-hubs-get-connection-string.md) to get the connection string by using the Azure portal, CLI, or PowerShell.

For Kafka clients, verify that `producer.config` or `consumer.config` files are configured properly. For more information, see [Send and receive messages with Kafka in Event Hubs](event-hubs-quickstart-kafka-enabled-event-hubs.md#send-and-receive-messages-with-kafka-in-event-hubs).

[!INCLUDE [event-hubs-connectivity](./includes/event-hubs-connectivity.md)]

### Verify that Event Hubs service tag is allowed in your network security groups

If your application runs inside a subnet and there's an associated network security group, confirm whether the internet outbound traffic is allowed or Event Hubs service tag (`EventHub`) is allowed. See [Virtual network service tags](../virtual-network/service-tags-overview.md) and search for `EventHub`.

### Check if the application needs to be running in a specific subnet of a virtual network

Confirm that your application runs in a virtual network subnet that has access to the namespace. If it doesn't, run the application in the subnet that has access to the namespace or add the IP address of the machine on which application is running to the [IP firewall](event-hubs-ip-filtering.md).

When you create a virtual network service endpoint for an event hub namespace, the namespace accepts traffic only from the subnet that's bound to the service endpoint. There's an exception to this behavior. You can add specific IP addresses in the IP firewall to enable access to the event hub's public endpoint. For more information, see [Network service endpoints](event-hubs-service-endpoints.md).

### Check the IP firewall settings for your namespace

Check that the public IP address of the machine on which the application is running isn't blocked by the IP firewall.

By default, Event Hubs namespaces are accessible from internet as long as the request comes with valid authentication and authorization. With IP firewall, you can restrict it further to only a set of IPv4 or IPv6 addresses or address ranges in [CIDR (Classless Inter-Domain Routing)](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) notation.

The IP firewall rules are applied at the Event Hubs namespace level. Therefore, the rules apply to all connections from clients using any supported protocol. Any connection attempt from an IP address that doesn't match an allowed IP rule on the Event Hubs namespace is rejected as unauthorized. The response doesn't mention the IP rule. IP filter rules are applied in order, and the first rule that matches the IP address determines the accept or reject action.

For more information, see [Configure IP firewall rules for an Azure Event Hubs namespace](event-hubs-ip-filtering.md). To check whether you have IP filtering, virtual network, or certificate chain issues, see [Troubleshoot network-related problems](#troubleshoot-network-related-problems).

### Check if the namespace can be accessed using only a private endpoint

If the Event Hubs namespace is configured to be accessible only via private endpoint, confirm that the client application is accessing the namespace over the private endpoint.

[Azure Private Link service](../private-link/private-link-overview.md) enables you to access Azure Event Hubs over a **private endpoint** in your virtual network. A private endpoint is a network interface that connects you privately and securely to a service powered by Azure Private Link. The private endpoint uses a private IP address from your virtual network, effectively bringing the service into your virtual network. All traffic to the service can be routed through the private endpoint, so no gateways, NAT devices, ExpressRoute or VPN connections, or public IP addresses are needed. Traffic between your virtual network and the service traverses over the Microsoft backbone network, eliminating exposure from the public Internet. You can connect to an instance of an Azure resource, giving you the highest level of granularity in access control.

For more information, see [Configure private endpoints](private-link-service.md). See the **Validate that the private endpoint connection works** section to confirm that a private endpoint is used.

### Troubleshoot network-related problems

To troubleshoot network-related problems with Event Hubs, follow these steps:

Browse to or use [wget](https://www.gnu.org/software/wget/) to access `https://<yournamespacename>.servicebus.windows.net/`. This step helps you check whether you have IP filtering, virtual network, or certificate chain problems (most common when using Java SDK).

An example of **successful message**:

```xml

<feed xmlns="http://www.w3.org/2005/Atom"><title type="text">Publicly Listed Services</title><subtitle type="text">This is the list of publicly-listed services currently available.</subtitle><id>uuid:27fcd1e2-3a99-44b1-8f1e-3e92b52f0171;id=30</id><updated>2019-12-27T13:11:47Z</updated><generator>Service Bus 1.1</generator></feed>

```

An example of **failure error message**:

```json

<Error>

<Code>400</Code>

<Detail>

Bad Request. To know more visit https://aka.ms/sbResourceMgrExceptions. . TrackingId:b786d4d1-cbaf-47a8-a3d1-be689cda2a98_G22, SystemTracker:NoSystemTracker, Timestamp:2019-12-27T13:12:40

</Detail>

</Error>

```

## Troubleshoot transient connectivity problems

If you're experiencing intermittent connectivity problems, go through the following sections for troubleshooting tips.

### Use the latest version of the client SDK

Later versions of the SDK might fix some transient connectivity problems. Make sure you're using the latest version of client SDKs in your applications. SDKs are continuously improved with new or updated features and bug fixes, so always test with the latest package. Check the release notes for fixed problems and added or updated features.

For information about client SDKs, see the [Azure Event Hubs - Client SDKs](sdks.md) article.

### Run the command to check dropped packets

When there are intermittent connectivity problems, run the following command to check if there are any dropped packets. This command tries to establish 25 different TCP connections every 1 second with the service. Then, you can check how many of them succeeded or failed and also see TCP connection latency. You can download the `psping` tool from [here](/sysinternals/downloads/psping).

```shell

.\psping.exe -n 25 -i 1 -q <yournamespacename>.servicebus.windows.net:5671 -nobanner

```

You can use equivalent commands if you're using other tools such as `tnc`, `ping`, and so on.

Obtain a network trace if the previous steps don't help and analyze it using tools such as [Wireshark](https://www.wireshark.org/). Contact [Microsoft Support](https://support.microsoft.com/) if needed.

### Service upgrades and restarts

Transient connectivity problems can happen because of backend service upgrades and restarts. When these problems happen, you might see the following symptoms:

- Incoming messages or requests drop.

- The log file shows error messages.

- The applications disconnect from the service for a few seconds.

- Requests are momentarily throttled.

If your application code uses the SDK, it already has an active retry policy. The application reconnects without significant impact to the application or workflow. By catching these transient errors, backing off, and then retrying the call, you make sure your code can handle these transient problems.

## Next steps

See the following articles:

* [Troubleshoot authentication and authorization issues](troubleshoot-authentication-authorization.md)


# Troubleshoot Authentication Authorization

# Troubleshoot authentication and authorization issues - Azure Event Hubs

The [Troubleshoot connectivity issues](troubleshooting-guide.md) article provides tips for troubleshooting connectivity issues with Azure Event Hubs. This article provides tips and recommendations for troubleshooting authentication and authorization issues with Azure Event Hubs.

<a name='if-you-are-using-azure-active-directory'></a>

## If you are using Microsoft Entra ID

If you are using Microsoft Entra ID to authenticate and authorize with Azure Event Hubs, confirm that the identity accessing the event hub is a member of the right **Azure role** at the right **resource scope** (consumer group, event hub, namespace, resource group, or subscription).

### Azure roles

- [Azure Event Hubs Data owner](../role-based-access-control/built-in-roles.md#azure-event-hubs-data-owner) for complete access to Event Hubs resources.

- [Azure Event Hubs Data sender](../role-based-access-control/built-in-roles.md#azure-event-hubs-data-receiver) for the send access.

- [Azure Event Hubs Data receiver](../role-based-access-control/built-in-roles.md#azure-event-hubs-data-sender) for the receive access.

For Schema Registry built-in roles, see [Schema Registry roles](schema-registry-concepts.md#azure-role-based-access-control).

### Resource scopes

- **Consumer group**: At this scope, role assignment applies only to this entity. Currently, the Azure portal doesn't support assigning an Azure role to a security principal at this level.

- **Event hub**: Role assignment applies to the Event Hub entity and the consumer group under it.

- **Namespace**: Role assignment spans the entire topology of Event Hubs under the namespace and to the consumer group associated with it.

- **Resource group**: Role assignment applies to all the Event Hubs resources under the resource group.

- **Subscription**: Role assignment applies to all the Event Hubs resources in all of the resource groups in the subscription.

For more information, see the following articles:

- [Authenticate an application with Microsoft Entra ID to access Event Hubs resources](authenticate-application.md)

- [Authorize access to Event Hubs resources using Microsoft Entra ID](authorize-access-azure-active-directory.md)

## If you are using Shared access signatures (SAS)

If you are using [SAS](authenticate-shared-access-signature.md), follow these steps:

- Ensure that the SAS key you are using is correct. If not, use the right SAS key.

- Verify that the key has the right permissions (send, receive, or manage). If not, use a key that has the permission you need.

- Check if the key has expired. We recommend that you renew the SAS well before expiration. If there is clock skew between client and the Event Hubs service nodes, the authentication token might expire before client realizes it. Current implementation accounts clock skew up to 5 minutes, that is, client renews the token 5 minutes before it expires. Therefore, if the clock skew is bigger than 5 minutes the client can observe intermittent authentication failures.

- If **SAS start time** is set to **now**, you may see intermittent failures for the first few minutes due to clock skew (differences in current time on different machines). Set the start time to be at least 15 minutes in the past or don't set it at all. The same generally applies to the expiry time as well.

For more information, see the following articles:

- [Authenticate using shared access signatures (SAS)](authenticate-shared-access-signature.md).

- [Authorizing access to Event Hubs resources using Shared Access Signatures](authorize-access-shared-access-signature.md)

## Next steps

See the following articles:

* [Troubleshoot connectivity issues](troubleshooting-guide.md)


# Troubleshoot Checkpoint Store Issues

# Troubleshoot checkpoint store issues

This article discusses issues with using Blob Storage as a checkpoint store.

## Issues with using Blob Storage as a checkpoint store

You may see issues when using a blob storage account as a checkpoint store that are related to delays in processing, or failures to create checkpoints when using the SDK, etc.

[!INCLUDE [storage-checkpoint-store-recommendations](./includes/storage-checkpoint-store-recommendations.md)]

## Using Blob Storage checkpoint store on Azure Stack Hub

If you're using Azure Blob Storage as the checkpoint store in an environment that supports a different version of Storage Blob SDK than the ones that are typically available on Azure, you need to use code to change the Storage service API version to the specific version supported by that environment. For example, if you're running [Event Hubs on an Azure Stack Hub version 2002](/azure-stack/user/event-hubs-overview), the highest available version for the Storage service is version 2017-11-09. In this case, you need to use code to target the Storage service API version to 2017-11-09. For an example of how to target a specific Storage API version, see these samples on GitHub:

- [.NET](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/eventhub/Azure.Messaging.EventHubs.Processor/samples/)

- [Java](https://github.com/Azure/azure-sdk-for-java/blob/master/sdk/eventhubs/azure-messaging-eventhubs-checkpointstore-blob/src/samples/java/com/azure/messaging/eventhubs/checkpointstore/blob/EventProcessorWithCustomStorageVersion.java).

- [JavaScript](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/eventhub/eventhubs-checkpointstore-blob/samples/v1/javascript/receiveEventsWithApiSpecificStorage.js) or  [TypeScript](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/eventhub/eventhubs-checkpointstore-blob/samples/v1/typescript/src/receiveEventsWithApiSpecificStorage.ts)

- Python - [Synchronous](https://github.com/Azure/azure-sdk-for-python/blob/master/sdk/eventhub/azure-eventhub-checkpointstoreblob/samples/receive_events_using_checkpoint_store_storage_api_version.py), [Asynchronous](https://github.com/Azure/azure-sdk-for-python/blob/master/sdk/eventhub/azure-eventhub-checkpointstoreblob-aio/samples/receive_events_using_checkpoint_store_storage_api_version_async.py)

If you run Event Hubs receiver that uses Blob Storage as the checkpoint store without targeting the version that Azure Stack Hub supports, you receive the following error message:

```

The value for one of the HTTP headers is not in the correct format

```

### Sample error message in Python

For Python, an error of `azure.core.exceptions.HttpResponseError` is passed to the error handler `on_error(partition_context, error)` of `EventHubConsumerClient.receive()`. But, the method `receive()` doesn't raise an exception. `print(error)` prints the following exception information:

```bash

The value for one of the HTTP headers is not in the correct format.

RequestId:f048aee8-a90c-08ba-4ce1-e69dba759297

Time:2020-03-17T22:04:13.3559296Z

ErrorCode:InvalidHeaderValue

Error:None

HeaderName:x-ms-version

HeaderValue:2019-07-07

```

The logger logs two warnings like the following ones:

```bash

WARNING:azure.eventhub.extensions.checkpointstoreblobaio._blobstoragecsaio:

An exception occurred during list_ownership for namespace '<namespace-name>.eventhub.<region>.azurestack.corp.microsoft.com' eventhub 'python-eh-test' consumer group '$Default'.

Exception is HttpResponseError('The value for one of the HTTP headers is not in the correct format.\nRequestId:f048aee8-a90c-08ba-4ce1-e69dba759297\nTime:2020-03-17T22:04:13.3559296Z\nErrorCode:InvalidHeaderValue\nError:None\nHeaderName:x-ms-version\nHeaderValue:2019-07-07')

WARNING:azure.eventhub.aio._eventprocessor.event_processor:EventProcessor instance '26d84102-45b2-48a9-b7f4-da8916f68214' of eventhub 'python-eh-test' consumer group '$Default'. An error occurred while load-balancing and claiming ownership.

The exception is HttpResponseError('The value for one of the HTTP headers is not in the correct format.\nRequestId:f048aee8-a90c-08ba-4ce1-e69dba759297\nTime:2020-03-17T22:04:13.3559296Z\nErrorCode:InvalidHeaderValue\nError:None\nHeaderName:x-ms-version\nHeaderValue:2019-07-07'). Retrying after 71.45254944090853 seconds

```

## Next steps

See the following article learn about partitioning and checkpointing: [Balance partition load across multiple instances of your application](event-processor-balance-partition-load.md)


# Exceptions Dotnet

# EventHubsException - .NET

An **EventHubsException** is triggered when an operation specific to Event Hubs has caused an issue, including both errors within the service and specific to the client.

## Exception information

The exception includes the following contextual information to assist in understanding the context of the error and its relative severity.

- **IsTransient**: Identifies whether the exception is considered recoverable or not. In the case where it was considered transient, the appropriate retry policy has already been applied and retries were unsuccessful.

- **Reason**: Provides a set of well-known reasons for the failure that help to categorize and clarify the root cause. These reasons are intended to allow for applying exception filtering and other logic when inspecting the text of an exception message wouldn't be ideal. Some key failure reasons are:

- **Client Closed**: Occurs when an Event Hub client that has already been closed or disposed. We recommend that you check the application code to ensure objects from the Event Hubs client library are created and closed in the intended scope.

- **Service Timeout**: Indicates that the Event Hubs service didn't respond to an operation within the expected amount of time. This issue may have been caused by a transient network issue or service problem. The Event Hubs service may or may not have successfully completed the request; the status isn't known. It's recommended to attempt to verify the current state and retry if necessary.

- **Quota Exceeded**: Indicates that there are too many active read operations for a single consumer group. This limit depends on the tier of the Event Hubs namespace, and moving to a higher tier may be needed. An alternative would be to create additional consumer groups and ensure that the number of consumer client reads for any group is within the limit. For more information, see [Azure Event Hubs quotas and limits](event-hubs-quotas.md).

- **Message Size Exceeded**: Event data as a maximum size allowed for both an individual event and a batch of events. It includes the data of the event, and any associated metadata and system overhead. To resolve this error, reduce the number of events sent in a batch or reduce the size of data included in the message. Because size limits are subject to change, see to [Azure Event Hubs quotas and limits](event-hubs-quotas.md) for specifics.

- **Consumer Disconnected**: A consumer client was disconnected by the Event Hub service from the Event Hub instance. It typically occurs when a consumer with a higher owner level asserts ownership over a partition and consumer group pairing.

- **Resource Not Found**: The Event Hubs service couldn't find a resource such as an event hub, consumer group, or partition. It may have been deleted or that there's an issue with the Event Hubs service itself.

## Handling exceptions

You can react to a specific failure reason for the **EventHubException**  in several ways. One way is to apply an exception filter clause as part of the catch block.

```csharp

try

{

// Read events using the consumer client

}

catch (EventHubsException ex) when

(ex.Reason == EventHubsException.FailureReason.ConsumerDisconnected)

{

// Take action based on a consumer being disconnected

}

```

## Next steps

There are other exceptions that are documented in the [legacy article](event-hubs-messaging-exceptions.md). Some of them apply only to the legacy Event Hubs .NET client library.


# Event Hubs Messaging Exceptions

# Event Hubs messaging exceptions - .NET (legacy)

This section lists the .NET exceptions generated by .NET Framework APIs.

> [!IMPORTANT]

> Some of the exceptions listed in the article apply only to legacy Event Hubs .NET library. For example: Microsoft.ServiceBus.* exceptions.

>

> For information about the EventHubsException raised by the new .NET library, see [EventHubsException - .NET](exceptions-dotnet.md)

[!INCLUDE [service-bus-track-0-and-1-sdk-support-retirement](../../includes/service-bus-track-0-and-1-sdk-support-retirement.md)]

## Exception categories

The Event Hubs .NET APIs generate exceptions that can fall into the following categories, along with the associated action you can take to try to fix them:

- User coding error:

- [System.ArgumentException](/dotnet/api/system.argumentexception?view=netcore-3.1&preserve-view=true)

- [System.InvalidOperationException](/dotnet/api/system.invalidoperationexception?view=netcore-3.1&preserve-view=true)

- [System.OperationCanceledException](/dotnet/api/system.operationcanceledexception?view=netcore-3.1&preserve-view=true)

- [System.Runtime.Serialization.SerializationException](/dotnet/api/system.runtime.serialization.serializationexception?view=netcore-3.1&preserve-view=true)

General action: Try to fix the code before proceeding.

- Setup/configuration error:

- [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception)

- [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception)

- [System.UnauthorizedAccessException](/dotnet/api/system.unauthorizedaccessexception?view=netcore-3.1&preserve-view=true)

General action: Review your configuration and change if necessary.

- Transient exceptions:

- [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception)

- [Microsoft.ServiceBus.Messaging.ServerBusyException](#serverbusyexception)

- [Microsoft.Azure.EventHubs.ServerBusyException](#serverbusyexception)

- [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception)

General action: Retry the operation or notify users.

- Other exceptions:

- [System.Transactions.TransactionException](/dotnet/api/system.transactions.transactionexception?view=netcore-3.1&preserve-view=true)

- [System.TimeoutException](#timeoutexception)

- [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception)

- [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception)

General action: Specific to the exception type; refer to the table in the following section.

## Exception types

The following table lists messaging exception types, and their causes, and notes suggested action you can take.

| Exception Type | Description/Cause/Examples | Suggested Action | Note on automatic/immediate retry |

| -------------- | -------------------------- | ---------------- | --------------------------------- |

| [TimeoutException](/dotnet/api/system.timeoutexception?view=netcore-3.1&preserve-view=true) |The server didn't respond to the requested operation within the specified time, which is controlled by [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings). The server may have completed the requested operation. This exception can happen because of network or other infrastructure delays. |Check the system state for consistency and retry if necessary.<br /> See [TimeoutException](#timeoutexception). | Retry might help in some cases; add retry logic to code. |

| [InvalidOperationException](/dotnet/api/system.invalidoperationexception?view=netcore-3.1&preserve-view=true) |The requested user operation isn't allowed within the server or service. See the exception message for details. For example, [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) generates this exception if the message was received in [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode. | Check the code and the documentation. Make sure the requested operation is valid. | Retry won't help. |

| [OperationCanceledException](/dotnet/api/system.operationcanceledexception?view=netcore-3.1&preserve-view=true) | An attempt is made to invoke an operation on an object that has already been closed, aborted, or disposed. In rare cases, the ambient transaction is already disposed. | Check the code and make sure it doesn't invoke operations on a disposed object. | Retry won't help. |

| [UnauthorizedAccessException](/dotnet/api/system.unauthorizedaccessexception?view=netcore-3.1&preserve-view=true) | The [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) object couldn't acquire a token, the token is invalid, or the token doesn't contain the claims required to do the operation. | Make sure the token provider is created with the correct values. Check the configuration of the Access Control Service. | Retry might help in some cases; add retry logic to code. |

| [ArgumentException](/dotnet/api/system.argumentexception?view=netcore-3.1&preserve-view=true)<br /> [ArgumentNullException](/dotnet/api/system.argumentnullexception?view=netcore-3.1&preserve-view=true)<br />[ArgumentOutOfRangeException](/dotnet/api/system.argumentoutofrangeexception?view=netcore-3.1&preserve-view=true) | One or more arguments supplied to the method are invalid. The URI supplied to [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) or [Create](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) contains path segment(s). The URI scheme supplied to [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) or [Create](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) is invalid. The property value is larger than 32 KB. | Check the calling code and make sure the arguments are correct. | Retry will not help. |

| [Microsoft.ServiceBus.Messaging MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) <br /><br/> [Microsoft.Azure.EventHubs MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception) | Entity associated with the operation does not exist or it has been deleted. | Make sure the entity exists. | Retry will not help. |

| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) | Client is not able to establish a connection to Event Hubs. |Make sure the supplied host name is correct and the host is reachable. | Retry might help if there are intermittent connectivity issues. |

| [Microsoft.ServiceBus.Messaging ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) <br /> <br/>[Microsoft.Azure.EventHubs ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) | Service is not able to process the request at this time. | Client can wait for a period of time, then retry the operation. <br /> See [ServerBusyException](#serverbusyexception). | Client may retry after certain interval. If a retry results in a different exception, check retry behavior of that exception. |

| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) | Generic messaging exception that may be thrown in the following cases: An attempt is made to create a [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) using a name or path that belongs to a different entity type (for example, a topic). An attempt is made to send a message larger than 1 MB. The server or service encountered an error during processing of the request. See the exception message for details. This exception is usually a transient exception. | Check the code and ensure that only serializable objects are used for the message body (or use a custom serializer). Check the documentation for the supported value types of the properties and only use supported types. Check the [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception) property. If it is **true**, you can retry the operation. | Retry behavior is undefined and might not help. |

| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) | Attempt to create an entity with a name that is already used by another entity in that service namespace. | Delete the existing entity or choose a different name for the entity to be created. | Retry will not help. |

| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) | The messaging entity has reached its maximum allowable size. This exception can happen if the maximum number of receivers (which is 5) has already been opened on a per-consumer group level. | Create space in the entity by receiving messages from the entity or its subqueues. <br /> See [QuotaExceededException](#quotaexceededexception) | Retry might help if messages have been removed in the meantime. |

| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) | Request for a runtime operation on a disabled entity. |Activate the entity. | Retry might help if the entity has been activated in the interim. |

| [Microsoft.ServiceBus.Messaging MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) <br /><br/> [Microsoft.Azure.EventHubs MessageSizeExceededException](/dotnet/api/microsoft.azure.eventhubs.messagesizeexceededexception) | A message payload exceeds the 1-MB limit. This 1-MB limit is for the total message, which can include system properties and any .NET overhead. | Reduce the size of the message payload, then retry the operation. |Retry will not help. |

## QuotaExceededException

[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) indicates that a quota for a specific entity has been exceeded.

This exception can happen if the maximum number of receivers (5) has already been opened on a per-consumer group level.

### Event Hubs

Event Hubs has a limit of 20 consumer groups per Event Hubs. When you attempt to create more, you receive a [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception).

## TimeoutException

A [TimeoutException](/dotnet/api/system.timeoutexception?view=netcore-3.1&preserve-view=true) indicates that a user-initiated operation is taking longer than the operation timeout.

For Event Hubs, the timeout is specified either as part of the connection string, or through [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). The error message itself might vary, but it always contains the timeout value specified for the current operation.

Timeouts are expected to happen during or in-between maintenance operations such as Event Hubs service updates (or) OS updates on resources that run the service. During OS updates, entities are moved around and nodes are updated or rebooted, which can cause timeouts. For service level agreement (SLA) details for the Azure Event Hubs service, see [SLA for Event Hubs](https://azure.microsoft.com/support/legal/sla/event-hubs/).

### Common causes

There are two common causes for this error: incorrect configuration, or a transient service error.

- **Incorrect configuration**

The operation timeout might be too small for the operational condition. The default value for the operation timeout in the client SDK is 60 seconds. Check to see if your code has the value set to something too small. The condition of the network and CPU usage can affect the time it takes for a particular operation to complete, so the operation timeout should not be set to a small value.

- **Transient service error**

Sometimes the Event Hubs service can experience delays in processing requests; for example, during periods of high traffic. In such cases, you can retry your operation after a delay, until the operation is successful. If the same operation still fails after multiple attempts, visit the [Azure service status site](https://azure.microsoft.com/status/) to see if there are any known service outages.

## ServerBusyException

A [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) or [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) indicates that a server is overloaded. There are two relevant error codes for this exception.

### Error code 50002

This error can occur for one of two reasons:

- The load isn't evenly distributed across all partitions on the event hub, and one partition hits the local throughput unit limitation.

**Resolution**: Revising the partition distribution strategy or trying [EventHubClient.Send(eventDataWithOutPartitionKey)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient) might help.

- The Event Hubs namespace doesn't have sufficient throughput units (you can check the **Metrics** screen in the Event Hubs namespace window in the [Azure portal](https://portal.azure.com) to confirm). The portal shows aggregated (1 minute) information, but we measure the throughput in real time – so it's only an estimate.

**Resolution**: Increasing the throughput units on the namespace can help.

You can configure throughput units on the **Scale** page or **Overview** page of your **Event Hubs namespace** page in the Azure portal. Or, you can use [Auto-inflate](event-hubs-auto-inflate.md), which automatically scales up by increasing the number of throughput units, to meet usage needs.

Throughput units (TUs) apply to all event hubs in an Event Hubs namespace. It means that you purchase TUs at the namespace level and are shared among the event hubs under that namespace. Each TU entitles the namespace to the following capabilities:

- Up to 1 MB per second of ingress events (events sent into an event hub), but no more than 1000 ingress events, management operations, or control API calls per second.

- Up to 2 MB per second of egress events (events consumed from an event hub), but no more than 4096 egress events.

- Up to 84 GB of event storage (enough for the default 1 hour retention period).

On the **Overview** page, in the **Show metrics** section, switch to the **Throughput** tab. Select the chart to open it in a larger window with 1-minute intervals on the x-axis. Look at the peak values and divide them by 60 to get incoming bytes/second or outgoing bytes/second. Use similar approach to calculate number of requests per second at peak times on the **Requests** tab.

If you see values higher than number of TUs * limits (1 MB per second for ingress or 1000 requests for ingress/second, 2 MB per second for egress), increase the number of TUs by using the **Scale** (on the left menu) page of an Event Hubs namespace to manually scale higher or to use the [Auto-inflate](event-hubs-auto-inflate.md) feature of Event Hubs. You can scale up to 40 TUs when you are manually scaling or automatically scaling the namespace.

### Error code 50008

This error should rarely occur. It happens when the container running code for your namespace is low on CPU – not more than a few seconds before the Event Hubs load balancer begins.

**Resolution**: Limit calls to the GetRuntimeInformation method. Azure Event Hubs supports up to 50 calls per second per consumer group to the GetRuntimeInfo per second. You may receive an exception similar to the following one once the limit is reached:

```

ExceptionId: 00000000000-00000-0000-a48a-9c908fbe84f6-ServerBusyException: The request was terminated because the namespace 75248:aaa-default-eventhub-ns-prodb2b is being throttled. Error code : 50008. Please wait 10 seconds and try again.

```

## Next steps

You can learn more about Event Hubs by visiting the following links:

* [Event Hubs overview](./event-hubs-about.md)

* [Create an Event Hub](event-hubs-create.md)

* [Event Hubs FAQ](event-hubs-faq.yml)


# Resource Manager Exceptions

# Azure Event Hubs - Resource Manager exceptions

This article lists exceptions generated when interacting with Azure Event Hubs using Azure Resource Manager - via templates or direct calls.

> [!IMPORTANT]

> This document is frequently updated. Please check back for updates.

The following sections provide various exceptions/errors that are surfaced through Azure Resource Manager.

## Error code: Conflict

| Error code | Error subcode | Error message | Description | Recommendation |

| ---------- | ------------- | ------------- | ----------- | -------------- |

| Conflict | 40300 | The maximum number of resources of type EventHub has been reached or exceeded. Actual: #, Max allowed: # | The namespace has reached its [quota](event-hubs-quotas.md) for the number of Event Hubs it can contain. | Delete any unused or extraneous event hubs from the namespace or consider upgrading to a [dedicated cluster](event-hubs-dedicated-overview.md). |

| Conflict | none | Disaster recovery (DR) config can't be deleted because replication is in progress. Fail over or break pairing before attempting to delete the DR Config. | [GeoDR replication](event-hubs-geo-dr.md) is in progress, so the config can't be deleted at this time. | To unblock deletion of the config, either wait until replication has completed, trigger a failover, or break the GeoDR pairing. |

| Conflict | none | Namespace update failed with conflict in backend. | Another operation is currently being done on this namespace. | Wait until the current operation completes, and then retry. |

## Error code: 429

| Error code | Error subcode | Error message | Description | Recommendation |

| ---------- | ------------- | ------------- | ----------- | -------------- |

| 429 | none | Namespace provisioning in transition | Another operation is currently being done on this namespace. | Wait until the current operation completes, and then retry. |

| 429 | none | Disaster recovery operation in progress. | A [GeoDR](event-hubs-geo-dr.md) operation is currently being done on this namespace or pairing. | Wait until the current GeoDR operation completes, and then retry. |

## Error code: BadRequest

| Error code | Error subcode | Error message | Description | Recommendation |

| ---------- | ------------- | ------------- | ----------- | -------------- |

| BadRequest | 40000 | PartitionCount can't be changed for an event hub. | Basic, standard, or premium tier of Azure Event Hubs doesn't support changing partitions. | Create a new event hub with the wanted number of partitions in your basic, standard, or premium tier namespace. Partition scale-out is supported for [dedicated clusters](event-hubs-dedicated-overview.md). |

| BadRequest | 40000 | The value '#' for MessageRetentionInDays isn't valid for the Basic tier. the value can't exceed '1' day(s). | Basic tier Event Hubs namespaces only support message retention of up to 1 day. | If more than one day of message retention is wanted, [create a standard Event Hubs namespace](event-hubs-create.md). |

| BadRequest | 40000 | The event hub can't be disabled. | The Capture feature is enabled for continuous flow of messages. | Disable the Capture feature and then try disabling the event hub. |

| BadRequest | none | The specified name isn't available. | Namespace names must be unique, and the specified name is already taken. | If you're the owner of the existing namespace with the specified name, you can delete it, which will cause data loss. Then, try again with the same name. If the namespace isn't safe to delete (or you aren't the owner), choose another namespace name. |

| BadRequest | none | The specified subscription has reached its quota of namespaces. | Your subscription has reached the [quota](event-hubs-quotas.md) for the number of namespaces it can hold. | Consider deleting unused namespaces in this subscription, creating another subscription, or upgrading to a [dedicated cluster](event-hubs-dedicated-overview.md). |

| BadRequest | none | Can't update a namespace that is secondary | The namespace can't be updated because it's the secondary namespace in a [GeoDR pairing](event-hubs-geo-dr.md). | If appropriate, make the change to the primary namespace in this pairing instead. Otherwise break the GeoDR pairing to make the change. |

| BadRequest | none | Can't set Auto-Inflate in basic SKU | Auto-Inflate can't be enabled on basic tier Event Hubs namespaces. | To [enable Auto Inflate](event-hubs-auto-inflate.md) on a namespace, make sure it's of standard or premium tier. |

| BadRequest | none | There isn't enough capacity to create the namespace. Contact your Event Hubs administrator. | The selected region is at capacity and more namespaces can't be created. | Select another region to house your namespace. |

| BadRequest | none | The operation can't be done on entity type 'ConsumerGroup' because the namespace 'namespace name' is using 'Basic' tier.  | Basic tier Event Hubs namespaces have a quota(event-hubs-quotas.md) of one consumer group (the default). Creating more consumer groups isn't supported. | Continue using the default consumer group ($Default), or if more are needed, consider using a standard or premium tier Event Hubs namespace instead. |

| BadRequest | none | The namespace 'namespace name' doesn't exist. | The namespace provided couldn't be found. | Double check that the namespace name is correct and can be found in your subscription. If it isn't, [create an Event Hubs namespace](event-hubs-create.md). |

| BadRequest | none | The location property of the resource doesn't match its containing Namespace. | Creating an event hub in a specific region failed because it didn't match the region of the namespace. | Try creating the event hub in the same region as the namespace. |

## Error code: Internal server error

| Error code | Error subcode | Error message | Description | Recommendation |

| ---------- | ------------- | ------------- | ----------- | -------------- |

| Internal Server Error | none | Internal Server Error. | The Event Hubs service had an internal error. | Retry the failing operation. If the operation continues to fail, contact support. |


# Monitor Event Hubs Reference

# Azure Event Hubs monitoring data reference

[!INCLUDE [horz-monitor-ref-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-intro.md)]

See [Monitor Azure Event Hubs](monitor-event-hubs.md) for details on the data you can collect for Event Hubs and how to use it.

Azure Event Hubs creates monitoring data using [Azure Monitor](/azure/azure-monitor/overview), which is a full stack monitoring service in Azure. Azure Monitor provides a complete set of features to monitor your Azure resources. It can also monitor resources in other clouds and on-premises.

Azure Event Hubs collects the same kinds of monitoring data as other Azure resources that are described in [Monitoring data from Azure resources](/azure/azure-monitor/essentials/monitor-azure-resource#monitoring-data).

[!INCLUDE [horz-monitor-ref-metrics-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-intro.md)]

### Supported metrics for Microsoft.EventHub/clusters

The following table lists the metrics available for the Microsoft.EventHub/clusters resource type.

[!INCLUDE [horz-monitor-ref-metrics-tableheader](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-tableheader.md)]

[!INCLUDE [Microsoft.EventHub/clusters](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/metrics/microsoft-eventhub-clusters-metrics-include.md)]

### Supported metrics for Microsoft.EventHub/Namespaces

The following table lists the metrics available for the Microsoft.EventHub/Namespaces resource type.

[!INCLUDE [horz-monitor-ref-metrics-tableheader](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-tableheader.md)]

[!INCLUDE [<ResourceType/namespace>](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/metrics/microsoft-eventhub-namespaces-metrics-include.md)]

The following tables list all the automatically collected platform metrics collected for Azure Event Hubs. The resource provider for these metrics is `Microsoft.EventHub/clusters` or `Microsoft.EventHub/namespaces`.

*Request metrics* count the number of data and management operations requests. This table provides more information about values from the preceding tables.

| Metric name         | Description |

|:--------------------|:------------|

| Incoming Requests   | The number of requests made to the Event Hubs service over a specified period. This metric includes all the data and management plane operations. |

| Successful Requests | The number of successful requests made to the Event Hubs service over a specified period. |

| Throttled Requests  | The number of requests that were throttled because the usage was exceeded. |

This table provides more information for message metrics from the preceding tables.

| Metric name | Description |

|:------------|:------------|

| Incoming Messages | The number of events or messages sent to Event Hubs over a specified period. |

| Outgoing Messages | The number of events or messages received from Event Hubs over a specified period. |

| Captured Messages | The number of captured messages. |

| Incoming Bytes    | Incoming bytes for an event hub over a specified period. |

| Outgoing Bytes    | Outgoing bytes for an event hub over a specified period. |

| Size              | Size of an event hub in bytes. |

> [!NOTE]

> - These values are point-in-time values. Incoming messages that are consumed immediately after that point-in-time might not be reflected in these metrics.

> - The Incoming Requests metric includes all the data and management plane operations. The Incoming Messages metric gives you the total number of events that are sent to the event hub. For example, if you send a batch of 100 events to an event hub, it counts as 1 incoming request and 100 incoming messages.

This table provides more information for capture metrics from the preceding tables.

| Metric name | Description |

|:------------|:------------|

| Captured Messages | The number of captured messages.  |

| Captured Bytes    | Captured bytes for an event hub.  |

| Capture Backlog   | Capture backlog for an event hub. |

This table provides more information for connection metrics from the preceding tables.

| Metric name | Description |

|:------------|:------------|

| Active Connections | The number of active connections on a namespace and on an entity (event hub) in the namespace. Value for this metric is a point-in-time value. Connections that were active immediately after that point-in-time might not be reflected in the metric. |

| Connections Opened | The number of open connections. |

| Connections Closed | The number of closed connections. |

This table provides more information for error metrics from the preceding tables.

| Metric name | Description |

|:------------|:------------|

| Server Errors         | The number of requests not processed because of an error in the Event Hubs service over a specified period. |

| User Errors           | The number of requests not processed because of user errors over a specified period. |

| Quota Exceeded Errors | The number of errors caused by exceeding quotas over a specified period. |

The following two types of errors are classified as *user errors*:

1. Client-side errors (In HTTP that would be 400 errors).

2. Errors that occur while processing messages.

> [!NOTE]

> Logic Apps creates epoch receivers. Receivers can be moved from one node to another depending on the service load. During those moves, `ReceiverDisconnection` exceptions might occur. They are counted as user errors on the Event Hubs service side. Logic Apps can collect failures from Event Hubs clients so that you can view them in user logs.

[!INCLUDE [horz-monitor-ref-metrics-dimensions-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-dimensions-intro.md)]

[!INCLUDE [horz-monitor-ref-metrics-dimensions](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-dimensions.md)]

| Dimension name  | Description |

|:----------------|:------------|

| EntityName      | Name of the event hub. With the 'Incoming Requests' metric, the Entity Name dimension has a value of `-NamespaceOnlyMetric-` in addition to all your event hubs. It represents the requests that were made at the namespace level. Examples include a  request to list all event hubs in the namespace or requests to entities that failed authentication or authorization. |

| OperationResult | Either indicates `success` or the appropriate error state, such as `serverbusy`, `clienterror` or `quotaexceeded`. |

Adding dimensions to your metrics is optional. If you don't add dimensions, metrics are specified at the namespace level.

> [!NOTE]

> When you enable metrics in a diagnostic setting, dimension information isn't currently included as part of the information sent to a storage account, event hub, or log analytics.

[!INCLUDE [horz-monitor-ref-resource-logs](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-resource-logs.md)]

### Supported resource logs for Microsoft.EventHub/Namespaces

[!INCLUDE [Microsoft.EventHub/Namespaces](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/logs/microsoft-eventhub-namespaces-logs-include.md)]

[!INCLUDE [horz-monitor-ref-logs-tables](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-logs-tables.md)]

### Event Hubs Microsoft.EventHub/namespaces

- [AzureActivity](/azure/azure-monitor/reference/tables/azureactivity#columns)

- [AzureMetrics](/azure/azure-monitor/reference/tables/azuremetrics#columns)

- [AzureDiagnostics](/azure/azure-monitor/reference/tables/azurediagnostics#columns)

- [AZMSApplicationMetricLogs](/azure/azure-monitor/reference/tables/azmsapplicationmetriclogs#columns)

- [AZMSOperationalLogs](/azure/azure-monitor/reference/tables/azmsoperationallogs#columns)

- [AZMSRunTimeAuditLogs](/azure/azure-monitor/reference/tables/azmsruntimeauditlogs#columns)

- [AZMSDiagnosticErrorLogs](/azure/azure-monitor/reference/tables/azmsdiagnosticerrorlogs#columns)

- [AZMSVnetConnectionEvents](/azure/azure-monitor/reference/tables/azmsvnetconnectionevents#columns)

- [AZMSArchiveLogs](/azure/azure-monitor/reference/tables/azmsarchivelogs#columns)

- [AZMSAutoscaleLogs](/azure/azure-monitor/reference/tables/azmsautoscalelogs#columns)

- [AZMSKafkaCoordinatorLogs](/azure/azure-monitor/reference/tables/azmskafkacoordinatorlogs#columns)

- [AZMSKafkaUserErrorLogs](/azure/azure-monitor/reference/tables/azmskafkausererrorlogs#columns)

- [AZMSCustomerManagedKeyUserLogs](/azure/azure-monitor/reference/tables/azmscustomermanagedkeyuserlogs#columns)

### Event Hubs resource logs

Azure Event Hubs now has the capability to dispatch logs to either of two destination tables: Azure Diagnostic or [Resource specific tables](/azure/azure-monitor/essentials/resource-logs) in Log Analytics. You could use the toggle available on Azure portal to choose destination tables.

Azure Event Hubs uses Kusto tables from Azure Monitor Logs. You can query these tables with Log Analytics.

You can view our sample queries to get started with different log categories.

> [!IMPORTANT]

> Dimensions aren't exported to a Log Analytics workspace.

[!INCLUDE [event-hubs-diagnostic-log-schema](./includes/event-hubs-diagnostic-log-schema.md)]

### Runtime audit logs

Runtime audit logs capture aggregated diagnostic information for all data plane access operations (such as send or receive events) in Event Hubs.

> [!NOTE]

> Runtime audit logs are available only in **premium** and **dedicated** tiers.

Runtime audit logs include the elements listed in the following table:

| Name | Description | Supported in Azure Diagnostics | Supported in Resource Specific table |

|:------- |:-------|:-----|:-----|

| `ActivityId` | A randomly generated UUID that ensures uniqueness for the audit activity. | Yes | Yes  |

| `ActivityName` | Runtime operation name.| Yes | Yes  |

| `ResourceId` | Resource associated with the activity. | Yes | Yes |

| `Timestamp` | Aggregation time. | Yes | No |

| `TimeGenerated [UTC]`|Time of executed operation (in UTC) | No | Yes |

| `Status` | Status of the activity (success or failure). | Yes | Yes  |

| `Protocol` | Type of the protocol associated with the operation. | Yes | Yes  |

| `AuthType` | Type of authentication (Microsoft Entra ID or SAS Policy). | Yes | Yes  |

| `AuthKey` | Microsoft Entra ID application ID or SAS policy name that's used to authenticate to a resource. | Yes | Yes  |

| `NetworkType` | Type of the network access: `Public` or `Private`. | Yes | Yes |

| `ClientIP` | IP address of the client application. | Yes | Yes  |

| `Count` | Total number of operations performed during the aggregated period of 1 minute. | Yes | Yes  |

| `Properties` | Metadata that are specific to the data plane operation. | Yes | Yes  |

| `Category` | Log category | Yes | No |

| `Provider`|Name of Service emitting the logs, such as EventHubs | No | Yes  |

| `Type`  | Type of logs emitted | No | Yes |

Here's an example of a runtime audit log entry:

AzureDiagnostics:

```json

{

"ActivityId": "<activity id>",

"ActivityName": "ConnectionOpen | Authorization | SendMessage | ReceiveMessage",

"ResourceId": "/SUBSCRIPTIONS/xxx/RESOURCEGROUPS/<Resource Group Name>/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/<Event Hubs namespace>/eventhubs/<event hub name>",

"Time": "1/1/2021 8:40:06 PM +00:00",

"Status": "Success | Failure",

"Protocol": "AMQP | KAFKA | HTTP | Web Sockets",

"AuthType": "SAS | Azure Active Directory",

"AuthId": "<AAD application name | SAS policy name>",

"NetworkType": "Public | Private",

"ClientIp": "x.x.x.x",

"Count": 1,

"Category": "RuntimeAuditLogs"

}

```

Resource specific table entry:

```json

{

"ActivityId": "<activity id>",

"ActivityName": "ConnectionOpen | Authorization | SendMessage | ReceiveMessage",

"ResourceId": "/SUBSCRIPTIONS/xxx/RESOURCEGROUPS/<Resource Group Name>/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/<Event Hubs namespace>/eventhubs/<event hub name>",

"TimeGenerated (UTC)": "1/1/2021 8:40:06 PM +00:00",

"Status": "Success | Failure",

"Protocol": "AMQP | KAFKA | HTTP | Web Sockets",

"AuthType": "SAS | Azure Active Directory",

"AuthId": "<AAD application name | SAS policy name>",

"NetworkType": "Public | Private",

"ClientIp": "x.x.x.x",

"Count": 1,

"Type": "AZMSRuntimeAUditLogs",

"Provider":"EVENTHUB"

}

```

### Application metrics logs

Application metrics logs capture the aggregated information on certain metrics related to data plane operations. The captured information includes the following runtime metrics.

> [!NOTE]

> Application metrics logs are available only in **premium** and **dedicated** tiers.

| Name | Description |

|:-------|:------- |

| `ConsumerLag` |Indicate the lag between consumers and producers.  For more details, see [Consumer lag](#consumer-lag) section.|

| `NamespaceActiveConnections` | Details of active connections established from a client to the event hub.  |

| `GetRuntimeInfo` | Obtain run time information from Event Hubs.  |

| `GetPartitionRuntimeInfo` | Obtain the approximate runtime information for a logical partition of an event hub.  |

| `IncomingMessages` | Details of number of messages published to Event Hubs using AMQP protocol. |

| `IncomingBytes` | Details of Publisher throughput sent to Event Hubs |

| `OutgoingMessages` | Details of number of messages consumed from Event Hubs using AMQP protocol.|

| `OutgoingBytes` | Details of Consumer throughput from Event Hubs. |

| `OffsetCommit` | Number of offset commit calls made to the event hub  |

| `OffsetFetch` | Number of offset fetch calls made to the event hub. |

#### Consumer lag

- The following points govern the emission of consumer lag for Kafka consumers.

- A namespace is idle from Kafka offset commit point of view if there are no offset commits for any Kafka consumer group under the namespace.

- If namespace is idle for an hour, then emission of lag metrics stops.

- As long as the namespace is not idle for offset commit, metrics are emitted for all Kafka consumer groups under that namespace.

- If a namespace is non-idle and the last offset commit for a consumer group predates the hub or topic's retention period, consumer lag will no longer be emitted.

- For AMQP consumers, consumer lag is emitted only as long as there are active receivers on the consumer group.

### Diagnostic Error Logs

Diagnostic error logs capture error messages for any client side, throttling, and Quota exceeded errors. They provide detailed diagnostics for error identification.

Diagnostic Error Logs include elements listed in following table:

| Name | Description | Supported in Azure Diagnostics | Supported in AZMSDiagnosticErrorLogs (Resource specific table) |

|:---|:---|:---|:---|

| `ActivityId` | A randomly generated UUID that ensures uniqueness for the audit activity. | Yes | Yes |

| `ActivityName` | Operation name  | Yes | Yes |

| `NamespaceName` | Name of Namespace | Yes | yes |

| `EntityType` | Type of Entity | Yes | Yes  |

| `EntityName` | Name of Entity | Yes | Yes   |

| `OperationResult` | Type of error in Operation (`clienterror` or `serverbusy` or `quotaexceeded`) | Yes | Yes |

| `ErrorCount` | Count of identical errors during the aggregation period of 1 minute. | Yes | Yes  |

| `ErrorMessage` | Detailed Error Message | Yes | Yes  |

| `ResourceProvider` | Name of Service emitting the logs. Possible values: `Microsoft.EventHub` and `Microsoft.ServiceBus` | Yes | Yes  |

| `Time Generated (UTC)` | Operation time | No | Yes |

| `EventTimestamp` | Operation Time | Yes | No |

| `Category` | Log category | Yes | No |

| `Type`  | Type of Logs emitted | No | Yes |

Here's an example of Diagnostic error log entry:

```json

{

"ActivityId": "0000000000-0000-0000-0000-00000000000000",

"SubscriptionId": "<Azure Subscription Id",

"NamespaceName": "Name of Event Hubs Namespace",

"EntityType": "EventHub",

"EntityName": "Name of Event Hub",

"ActivityName": "SendMessage",

"ResourceId": "/SUBSCRIPTIONS/xxx/RESOURCEGROUPS/<Resource Group Name>/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/<Event hub namespace name>",,

"OperationResult": "ServerBusy",

"ErrorCount": 1,

"EventTimestamp": "3/27/2024 1:02:29.126 PM +00:00",

"ErrorMessage": "the request was terminated because the entity is being throttled by the application group with application group name <application group name> and policy name <throttling policy name>.error code: 50013.",

"category": "DiagnosticErrorLogs"

}

```

Resource specific table entry:

```json

{

"ActivityId": "0000000000-0000-0000-0000-00000000000000",

"NamespaceName": "Name of Event Hubs Namespace",

"EntityType": "Event Hub",

"EntityName": "Name of Event Hub",

"ActivityName": "SendMessage",

"ResourceId": "/SUBSCRIPTIONS/xxx/RESOURCEGROUPS/<Resource Group Name>/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/<Event hub namespace name>",,

"OperationResult": "ServerBusy",

"ErrorCount": 1,

"TimeGenerated [UTC]": "1/27/2024 4:02:29.126 PM +00:00",

"ErrorMessage": "The request was terminated because the entity is being throttled by the application group with application group name <application group name> and policy name <throttling policy name>.error code: 50013.",

"Type": "AZMSDiagnosticErrorLogs"

}

```

[!INCLUDE [horz-monitor-ref-activity-log](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-activity-log.md)]

- [Microsoft.EventHub resource provider operations](/azure/role-based-access-control/permissions/integration#microsofteventhub)

## Related content

- See [Monitor Azure Event Hubs](monitor-event-hubs.md) for a description of monitoring Event Hubs.

- See [Monitor Azure resources with Azure Monitor](/azure/azure-monitor/essentials/monitor-azure-resource) for details on monitoring Azure resources.


# Sdks

# Azure Event Hubs - Client SDKs

This article provides following information for the SDKs supported by Azure Event Hubs:

- Location of package that you can use in your applications

- GitHub location where you can find source code, samples, readme, change log, reported issues, and also raise new issues

- Links to quickstart tutorials

## Client SDKs

The following table describes all the latest available Azure Event Hubs runtime clients. The core focus of these libraries is to **send and receive messages** from an event hub.

| Language | Package | Reference |

| -------- | ------- | --------------- |

| . NET Standard | [Azure.Messaging.EventHubs](https://www.nuget.org/packages/Azure.Messaging.EventHubs/) |<ul><li>[GitHub location](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/eventhub/Azure.Messaging.EventHubs)</li><li>[Tutorial](event-hubs-dotnet-standard-getstarted-send.md)</li></ul> |

|       | [Azure.Messaging.EventHubs.Processor](https://www.nuget.org/packages/Azure.Messaging.EventHubs.Processor/) | <ul><li>[GitHub location](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/eventhub/Azure.Messaging.EventHubs.Processor)</li><li>[Tutorial](event-hubs-dotnet-standard-getstarted-send.md)</li></ul> |

| Java | [azure-messaging-eventhubs](https://central.sonatype.com/artifact/com.azure/azure-messaging-eventhubs) | <ul><li>[GitHub location](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/eventhubs/azure-messaging-eventhubs)</li><li>[Tutorial](event-hubs-java-get-started-send.md)</li></ul> |

|      | [azure-messaging-eventhubs-checkpointstore-blob](https://central.sonatype.com/artifact/com.azure/azure-messaging-eventhubs-checkpointstore-blob) | <ul><li>[GitHub location](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/eventhubs/azure-messaging-eventhubs-checkpointstore-blob)</li><li>[Tutorial](event-hubs-java-get-started-send.md)</li></ul> |

| Python |  [azure-eventhub](https://pypi.org/project/azure-eventhub/) | <ul><li>[GitHub location](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/eventhub/azure-eventhub)</li><li>[Tutorial](event-hubs-python-get-started-send.md)</li></ul> |

|        | [azure-eventhub-checkpointstoreblob-aio](https://pypi.org/project/azure-eventhub-checkpointstoreblob-aio/) | <ul><li>[GitHub location](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/eventhub/azure-eventhub-checkpointstoreblob-aio)</li><li>[Tutorial](event-hubs-python-get-started-send.md)</li></ul> |

| JavaScript | [Azure/event-hubs](https://www.npmjs.com/package/@azure/event-hubs) | <ul><li>[GitHub location](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/eventhub/event-hubs)</li><li>[Tutorial](event-hubs-node-get-started-send.md)</li></ul> |

|            | [azure/eventhubs-checkpointstore-blob](https://www.npmjs.com/package/@azure/eventhubs-checkpointstore-blob) | <ul><li>[GitHub location](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/eventhub/eventhubs-checkpointstore-blob)</li><li>[Tutorial](event-hubs-node-get-started-send.md)</li></ul> |

| Go | [Azure-event-hubs-go](https://github.com/Azure/azure-event-hubs-go) | <ul><li>[GitHub location](https://github.com/Azure/azure-event-hubs-go)</li><li>[Tutorial](event-hubs-go-get-started-send.md)</li></ul> |

| C | [Azure-event-hubs-c](https://github.com/Azure/azure-event-hubs-c) | <ul><li>[GitHub location](https://github.com/Azure/azure-event-hubs-c)</li><li>[Tutorial](event-hubs-c-getstarted-send.md)</li></ul> |

The following table lists older Azure Event Hubs runtime clients. While these packages might receive critical bug fixes, they aren't in active development. We recommend using the latest SDKs listed in the table instead.

[!INCLUDE [service-bus-track-0-and-1-sdk-support-retirement](../../includes/service-bus-track-0-and-1-sdk-support-retirement.md)]

| Language | Package | Reference |

| -------- | ------- | --------------- |

| . NET Standard  | [Microsoft.Azure.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) (**legacy**) | <ul><li>[GitHub location](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/eventhub/Azure.Messaging.EventHubs)</li><li>[Tutorial](event-hubs-dotnet-standard-getstarted-send.md)</li></ul> |

|       | [Microsoft.Azure.EventHubs.Processor](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor) (**legacy**) | <ul><li>[GitHub location](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/eventhub/Azure.Messaging.EventHubs.Processor)</li><li>[Tutorial](event-hubs-dotnet-standard-getstarted-send.md)</li></ul> |

| . NET Framework | [WindowsAzure.Messaging](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) (**legacy**) | |

|   Java   | [azure-eventhubs](https://central.sonatype.com/artifact/com.microsoft.azure/azure-eventhubs) **(legacy)** | <ul><li>[GitHub location](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/eventhubs/microsoft-azure-eventhubs)</li><li>[Tutorial](event-hubs-java-get-started-send.md)</li></ul> |

## Management SDKs

Here's a list of currently available management-specific libraries. None of these libraries contain runtime operations, and are for the sole purpose of **managing Event Hubs entities**.

- [.NET Standard](/dotnet/api/microsoft.azure.management.eventhub)

- [Java](/java/api/com.microsoft.azure.management.eventhub)

- [Python](/python/api/azure-mgmt-eventhub)

- [JavaScript](/javascript/api/@azure/arm-eventhub/)

## .NET packages

### Client libraries

- **Azure.Messaging.EventHubs**: It's the current version of the library, conforming to the unified Azure SDK design guidelines and under active development for new features. It supports the .NET Standard platform, allowing it to be used by both the full .NET Framework and .NET Core. There's feature parity at a high level with Microsoft.Azure.EventHubs, with details and the client hierarchy taking a different form. This library is the one that we recommend you to use.

- **Microsoft.Azure.EventHubs**: It was the initial library to break out Event Hubs into a dedicated client that isn’t bundled with Service Bus. It supports the .NET Standard 2.0 platform, allowing it to be used by both the full .NET Framework and .NET Core. It's still the dominant version of the library with respect to usage and third-party blog entries, extensions, and such. The baseline functionality is the same as the current library, though there are some minor bits that one offers and the other doesn’t. It's currently receiving bug fixes and critical updates but is no longer receiving new features.

- **Windows.Azure.ServiceBus**: It was the original library, back when Event Hubs was still more entangled with Service Bus. It supports only the full .NET Framework, because it predates .NET Core. This library offers some corollary functionality that isn’t supported by the newer libraries.

### Management libraries

- **Microsoft.Azure.Management.EventHub**:  It's the current GA version of the management library for Event Hubs. It supports the .NET Standard 2.0 platform, allowing it to be used by both the full .NET Framework and .NET Core.

## Next steps

You can learn more about Event Hubs by visiting the following links:

* [Event Hubs overview](./event-hubs-about.md)

* [Create an event hub](event-hubs-create.md)

* [Event Hubs FAQ](event-hubs-faq.yml)


# Apache Kafka Configurations

# Apache Kafka client configurations for Azure Event Hubs

This guide helps Kafka developers configure their client applications when migrating from Apache Kafka to Azure Event Hubs. Event Hubs provides a Kafka-compatible endpoint, allowing you to use existing Kafka client libraries with minimal configuration changes.

## Before you begin

### What you can and can't configure

Azure Event Hubs is a fully managed service. Unlike self-managed Kafka clusters, you don't have access to broker-side configurations. This means:

| Configuration type | Configurable? | Notes |

|--------------------|---------------|-------|

| **Client-side configurations** | ✅ Yes | Producer and consumer settings in your application code |

| **Broker/server configurations** | ❌ No | Managed by Event Hubs (replication, retention policies, etc.) |

| **Topic-level configurations** | ⚠️ Limited | Partition count and retention set via Azure portal or APIs, not Kafka AdminClient |

### Use defaults unless you have a specific need

> [!IMPORTANT]

> **For most workloads, the default Kafka client configurations work well with Event Hubs.** Only modify settings when you have a specific performance requirement or encounter issues. Incorrect configuration changes can negatively impact throughput, latency, and reliability.

The tables in this article list configurations that **differ from standard Kafka defaults** or have **Event Hubs-specific constraints**. If a configuration isn't listed here, use the Kafka client default value.

### Required connection settings

All Kafka clients connecting to Event Hubs require these authentication settings:

```properties

bootstrap.servers=<your-namespace>.servicebus.windows.net:9093

security.protocol=SASL_SSL

sasl.mechanism=PLAIN

sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="<your-connection-string>";

```

For more connection options, see [Connect to Event Hubs using Kafka protocol](event-hubs-quickstart-kafka-enabled-event-hubs.md).

## Java client configuration properties

This section covers configurations for the official Apache Kafka Java client. For the full list of Kafka producer and consumer configurations, see the [Apache Kafka documentation](https://kafka.apache.org/documentation/).

### Configurations that differ from Kafka defaults

The following settings have Event Hubs-specific constraints or recommended values that differ from standard Kafka defaults:

#### Producer and consumer

| Property | Default | Recommended for Event Hubs | Constraint | Notes |

|----------|---------|---------------------------|------------|-------|

| `metadata.max.age.ms` | 300000 | 180000 | Must be < 240000 | Azure closes idle connections after 240 seconds |

| `connections.max.idle.ms` | 540000 | 180000 | Must be < 240000 | Prevents sending on closed connections (appears as expired batches) |

#### Producer only

| Property | Default | Recommended for Event Hubs | Constraint | Notes |

|----------|---------|---------------------------|------------|-------|

| `max.request.size` | 1048576 | 1000000 | Must be < 1046528 | **Critical**: Connections close if exceeded. Reduce from default. |

| `request.timeout.ms` | 30000 | 60000 | Must be > 20000 | Event Hubs enforces 20 second minimum internally |

| `compression.type` | none | `none` or `gzip` | Only `gzip` supported | Other compression types (snappy, lz4, zstd) aren't supported |

#### Consumer only

| Property | Default | Recommended for Event Hubs | Constraint | Notes |

|----------|---------|---------------------------|------------|-------|

| `heartbeat.interval.ms` | 3000 | 3000 (keep default) | — | Don't change this value |

| `session.timeout.ms` | 45000 | 30000 | 6000–300000 | Increase if you see frequent rebalancing |

| `max.poll.interval.ms` | 300000 | 300000 (keep default) | Must be > `session.timeout.ms` | Increase only if processing takes longer than 5 minutes |

### Configurations to keep at defaults

These settings work well with Event Hubs at their default values. Only change them if you have specific requirements:

| Property | Default | When to consider changing |

|----------|---------|---------------------------|

| `retries` | 2147483647 | Rarely needs changing |

| `delivery.timeout.ms` | 120000 | Adjust if using custom retry strategy |

| `linger.ms` | 0 | Increase for high-throughput scenarios (trades latency for throughput) |

| `batch.size` | 16384 | Increase for high-throughput scenarios |

| `acks` | all | Use `1` for higher throughput with slightly less durability |

| `enable.idempotence` | true | Keep enabled for exactly-once producer semantics. Requires `request.timeout.ms` ≥ 60000, high `retries` (default is sufficient), and `acks=all` |

## librdkafka configuration properties

This section covers configurations for librdkafka-based clients (Confluent Python, Confluent .NET, Confluent Go, and others). For the complete configuration reference, see the [librdkafka documentation](https://github.com/edenhill/librdkafka/blob/master/CONFIGURATION.md).

### Configurations that differ from librdkafka defaults

#### Producer and consumer

| Property | Default | Recommended for Event Hubs | Constraint | Notes |

|----------|---------|---------------------------|------------|-------|

| `socket.keepalive.enable` | false | true | — | Required to prevent idle connection closure |

| `metadata.max.age.ms` | 900000 | 180000 | Must be < 240000 | Azure closes idle connections after 240 seconds |

#### Producer only

| Property | Default | Recommended for Event Hubs | Constraint | Notes |

|----------|---------|---------------------------|------------|-------|

| `request.timeout.ms` | 5000 | 60000 | Must be > 20000 | **Critical**: librdkafka default is too low for Event Hubs |

| `compression.codec` | none | `none` or `gzip` | Only `gzip` supported | Other compression types aren't supported |

#### Consumer only

| Property | Default | Recommended for Event Hubs | Constraint | Notes |

|----------|---------|---------------------------|------------|-------|

| `heartbeat.interval.ms` | 3000 | 3000 (keep default) | — | Don't change this value |

| `session.timeout.ms` | 45000 | 30000 | 6000–300000 | Increase if you see frequent rebalancing |

| `max.poll.interval.ms` | 300000 | 300000 (keep default) | Must be > `session.timeout.ms` | Increase only if processing takes longer than 5 minutes |

### Configurations to keep at defaults

| Property | Default | When to consider changing |

|----------|---------|---------------------------|

| `retries` | 2147483647 | Rarely needs changing |

| `partitioner` | consistent_random | Handles null keys well; change only for specific key distribution needs |

## Troubleshooting common issues

If you encounter problems after migrating from Kafka to Event Hubs, check these common configuration-related issues:

| Symptom | Likely cause | Solution |

|---------|--------------|----------|

| Connection closed unexpectedly | `max.request.size` exceeds 1,046,528 bytes | Set `max.request.size=1000000` |

| Expired batches or send timeouts | Idle connections closed by Azure | Set `connections.max.idle.ms=180000` and `metadata.max.age.ms=180000` |

| Request timeouts (librdkafka) | Default `request.timeout.ms` too low | Set `request.timeout.ms=60000` |

| Frequent consumer rebalancing | `session.timeout.ms` too low or processing too slow | Increase `session.timeout.ms` or `max.poll.interval.ms`. Consider setting unique `group.instance.id` per consumer instance to reduce rebalances from transient disconnections |

| Offset commit failures | Processing takes too long between polls | Increase `max.poll.interval.ms`, reduce batch size, or parallelize processing |

| Compression errors | Unsupported compression type | Use `compression.type=gzip` or `compression.type=none` |

| Authentication failures | Incorrect connection string format | Verify `sasl.jaas.config` format and connection string value |

| High latency spikes | `linger.ms` set too high, causing batch accumulation delays | Reduce `linger.ms` value (use `0` for lowest latency) |

| Data disappearing earlier than expected | Event Hubs retention period shorter than original Kafka retention | Adjust retention in Azure portal; check [quotas and limits](event-hubs-quotas.md) for max retention per tier |

| Unexpected offset reset | Consumer offsets expired beyond Event Hubs retention period | Ensure `auto.offset.reset` is configured appropriately; increase retention or process data before offsets expire |

| Not receiving all data from all partitions | Zombie consumer application running in your environment with the same `group.id` | Isolate and kill the zombie application |

## Configuration not supported

The following Kafka features and configurations aren't available with Event Hubs:

| Feature | Reason |

|---------|--------|

| Kafka AdminClient for topic management | Use Azure portal, CLI, or ARM templates instead |

| Broker configurations | Event Hubs is fully managed |

| Transactions | Not currently supported |

| Exactly-once semantics (EOS) | Not currently supported |

| Compression types other than gzip | Only gzip compression is supported |

| Custom partitioner on server side | Partition assignment is client-side only |

## Related content

- [Azure Event Hubs for Apache Kafka overview](azure-event-hubs-apache-kafka-overview.md)

- [Quickstart: Stream data with Event Hubs using Kafka protocol](event-hubs-quickstart-kafka-enabled-event-hubs.md)

- [Migrate from Apache Kafka to Event Hubs](apache-kafka-migration-guide.md)

- [Event Hubs quotas and limits](event-hubs-quotas.md)

- [Apache Kafka documentation: Producer configs](https://kafka.apache.org/documentation/#producerconfigs)

- [Apache Kafka documentation: Consumer configs](https://kafka.apache.org/documentation/#consumerconfigs)


# Policy Reference

# Azure Policy built-in definitions for Azure Event Hubs

This page is an index of [Azure Policy](../governance/policy/overview.md) built-in policy

definitions for Azure Event Hubs. For additional Azure Policy built-ins for other services, see

[Azure Policy built-in definitions](/azure/governance/policy/samples/built-in-policies).

The name of each built-in policy definition links to the policy definition in the Azure portal. Use

the link in the **Version** column to view the source on the

[Azure Policy GitHub repo](https://github.com/Azure/azure-policy).

## Azure Event Hubs

[!INCLUDE [azure-policy-reference-rp-eventhubs](~/azure-policy-autogen-docs/includes/policy/reference/byrp/microsoft.eventhub.md)]

## Next steps

- See the built-ins on the [Azure Policy GitHub repo](https://github.com/Azure/azure-policy).

- Review the [Azure Policy definition structure](../governance/policy/concepts/definition-structure.md).

- Review [Understanding policy effects](../governance/policy/concepts/effects.md).


# Event Hubs Partitions

Event Hubs organizes sequences of events sent to an event hub into one or more partitions. As newer events arrive, they're added to the end of this sequence.

A partition can be thought of as a commit log. Partitions hold event data that contains the following information:

- Body of the event

- User-defined property bag describing the event

- Metadata such as its offset in the partition, its number in the stream sequence

- Service-side timestamp at which it was accepted

### Advantages of using partitions

Event Hubs is designed to help with processing of large volumes of events, and partitioning helps with that in two ways:

- Even though Event Hubs is a PaaS service, there's a physical reality underneath. Maintaining a log that preserves the order of events requires that these events are being kept together in the underlying storage and its replicas and that results in a throughput ceiling for such a log. Partitioning allows for multiple parallel logs to be used for the same event hub and therefore multiplying the available raw input-output (IO) throughput capacity.

- Your own applications must be able to keep up with processing the volume of events that are being sent into an event hub. It might be complex and requires substantial, scaled-out, parallel processing capacity. The capacity of a single process to handle events is limited, so you need several processes. Partitions are how your solution feeds those processes and yet ensures that each event has a clear processing owner.

### Number of partitions

The number of partitions is specified at the time of creating an event hub. It must be between one and the maximum partition count allowed for each pricing tier. For the partition count limit for each tier, see [this article](../event-hubs-quotas.md#basic-vs-standard-vs-premium-vs-dedicated-tiers).

We recommend that you choose at least as many partitions as you expect that are required during the peak load of your application for that particular event hub.

For tiers other than the premium and dedicated tiers, you can't change the partition count for an event hub after its creation. For an event hub in a premium or dedicated tier, you can [increase the partition count](../dynamically-add-partitions.md) after its creation, but you can't decrease them. The distribution of streams across partitions will change when it's done as the mapping of partition keys to partitions changes, so you should try hard to avoid such changes if the relative order of events matters in your application.

Setting the number of partitions to the maximum permitted value is tempting, but always keep in mind that your event streams need to be structured such that you can indeed take advantage of multiple partitions. If you need absolute order preservation across all events or only a handful of substreams, you might not be able to take advantage of many partitions. Also, many partitions make the processing side more complex.

It doesn't matter how many partitions are in an event hub when it comes to pricing. It depends on the number of pricing units ([throughput units

(TUs)](../event-hubs-scalability.md#throughput-units) for the standard tier, [processing units (PUs)](../event-hubs-scalability.md#processing-units) for the premium tier, and [capacity units (CUs)](../event-hubs-dedicated-overview.md#capacity-units) for the dedicated tier) for the namespace or the dedicated cluster. For example, an event hub of the standard tier with 32 partitions or with one partition incur the exact same cost when the namespace is set to one TU capacity. Also, you can scale TUs or PUs on your namespace or CUs of your dedicated cluster independent of the partition count.

[!INCLUDE [event-hubs-partition-count](event-hubs-partition-count.md)]

### Mapping of events to partitions

You can use a partition key to map incoming event data into specific partitions for the purpose of data organization. The partition key is a sender-supplied value passed into an event hub. It's processed through a static hashing function, which creates the partition assignment. If you don't specify a partition key when publishing an event, a round-robin assignment is used.

The event publisher is only aware of its partition key, not the partition to which the events are published. This decoupling of key and partition insulates the sender from needing to know too much about the downstream processing. A per-device or user unique identity makes a good partition key, but other attributes such as geography can also be used to group related events into a single partition.

Specifying a partition key enables keeping related events together in the same partition and in the exact order in which they arrived. The partition key is some string that is derived from your application context and identifies the interrelationship of the events. A sequence of events identified by a partition key is a *stream*. A partition is a multiplexed log store for many such streams.

> [!NOTE]

> While you can send events directly to partitions, we don't recommend it, especially when high availability is important to you. It downgrades the availability of an event hub to partition-level. For more information, see [Availability and Consistency](../event-hubs-availability-and-consistency.md).


# Storage Checkpoint Store Recommendations

Follow these recommendations when you use Azure Blob Storage as a checkpoint store:

- Use a separate container for each consumer group. You can use the same storage account, but use one container per each group.

- Don't use the storage account for anything else.

- Don't use the container for anything else.

- Create the storage account in the same region as the deployed application. If the application is on-premises, try to choose the closest region possible.

On the **Storage account** page in the Azure portal, in the **Blob service** section, ensure that the following settings are disabled.

- Hierarchical namespace

- Blob soft delete

- Versioning


# Event Hubs Common Limits

The following limits are common across all tiers.

| Limit |  Notes | Value |

| --- |  --- | --- |

| Size of an event hub name |- | 256 characters |

| Size of a consumer group name | Kafka protocol doesn't require the creation of a consumer group. | <p>Kafka: 256 characters</p><p>Advanced Message Queuing Protocol (AMQP): 50 characters |

| Number of non-epoch receivers per consumer group |- |5 |

| Number of authorization rules per namespace | Subsequent requests for authorization rule creation are rejected.|12 |

| Number of calls to the GetRuntimeInformation method |  - | 50 per second per consumer group |

| Number of virtual networks | - | 128 |

| Number of IP Config rules | - | 128 |

| Maximum length of a schema group name | | 50 |

| Maximum length of a schema name | | 100 |

| Size in bytes per schema | | 1 MB |

| Number of properties per schema group | | 1024 |

| Size in bytes per schema group property key | | 256 |

| Size in bytes per schema group property value | | 1024 |

| Number of concurrent receive requests on a hub/topic | Subsequent receive requests are throttled. This quota applies to the combined number of concurrent receive operations across all consumers/consumer groups | 5000 |


# Event Hubs Tier Limits

The following table shows limits that are different for Basic, Standard, Premium, and Dedicated tiers.

> [!NOTE]

> - In the table, CU is [capacity unit](../event-hubs-dedicated-overview.md), PU is [processing unit](../event-hubs-scalability.md#processing-units), and TU is [throughput unit](../event-hubs-scalability.md#throughput-units).

> - You can configure [TUs](../enable-auto-inflate.md) for a Basic or Standard tier namespace or [PUs](../configure-processing-units-premium-namespace.md) for a Premium tier namespace.

> - When you [create a dedicated cluster](../event-hubs-dedicated-cluster-create-portal.md#create-an-event-hubs-dedicated-cluster), Azure Event Hubs assigns one CU to the cluster. If you enable the **Support scaling** option while creating the cluster, you can scale out by increasing CUs or scale in by decreasing CUs for the cluster. For step-by-step instructions, see [Scale dedicated cluster](../event-hubs-dedicated-cluster-create-portal.md#scale-a-dedicated-cluster). For clusters that don't support the **Support scaling** feature, [submit a ticket](../event-hubs-dedicated-cluster-create-portal.md#submit-a-support-request) to adjust CUs for the cluster.

| Limit | Basic | Standard | Premium | Dedicated |

| ----- | ----- | -------- | -------- | --------- |

| Maximum size of Event Hubs publication | 256 KB | 1 MB | 1 MB | 20 MB |

| Number of consumer groups per event hub | 1 | 20 | 100 | 1,000<br/>No limit per CU |

| Number of Kafka consumer groups per namespace | N/A | 1,000 | 1,000 | 1,000 |

| Number of brokered connections per namespace | 100 | 5,000 | 10,000 per PU<br/><br/>For example, if the namespace is assigned 4 PUs, the limit is 40,000. | 100,000 per CU |

| Maximum retention period of event data | 1 day | 7 days | 90 days | 90 days |

| Event storage for retention | 84 GB per TU | 84 GB per TU | 1 TB per PU | 10 TB per CU |

| Maximum TUs or PUs or CUs | 40 TUs | 40 TUs | 16 PUs | 20 CUs |

| Number of partitions per event hub | 32 | 32 | 100 per event hub, but there's a limit of 200 per PU at the namespace level.<br/><br/> For example, if a namespace is assigned 2 PUs, the limit for total number of partitions in all event hubs in the namespace is 2 * 200 = 400. | 1,024 per event hub<br/> 2,000 per CU |

| Number of namespaces per subscription per region | 1,000 (all tiers) | 1,000 (all tiers) | 1,000 (all tiers) | 1,000 (50 per CU) |

| Number of event hubs per namespace | 10 | 10 | 100 per PU | 1,000 |

| Capture | N/A | Pay per hour | Included | Included |

| Size of compacted event hub | N/A | 1 GB per partition | 250 GB per partition | 250 GB per partition |

| Size of the schema registry (namespace) in megabytes | N/A | 25 | 100 | 1,024 |

| Number of schema groups in a schema registry or namespace | N/A | 1: excluding the default group | 100 <br/>1 MB per schema | 1,000<br/>1 MB per schema |

| Number of schema versions across all schema groups | N/A | 25 | 1,000 | 10,000 |

| Throughput per unit | Ingress: 1 MB/sec or 1,000 events per second<br/>Egress: 2 MB/sec or 4,096 events per second | Ingress: 1 MB/sec or 1,000 events per second<br/>Egress: 2 MB/sec or 4,096 events per second | No limits per PU * | No limits per CU * |

\* Depends on factors such as resource allocation, number of partitions, and storage.

> [!NOTE]

> You can publish events individually or batched. The publication limit (according to tier) applies regardless of whether it's a single event or a batch. Publishing events larger than the maximum threshold is rejected.


# Event Hubs Tier Features

The following table shows the list of features that are available (or not available) in a specific tier of Azure Event Hubs.

| Feature | Basic | Standard | Premium | Dedicated |

| ------- | ------| -------- | ------- | --------- |

| Tenancy | Multitenant | Multitenant | Multitenant with resource isolation | Exclusive single tenant |

| Private link | N/A | Yes | Yes | Yes |

| Customer-managed key <br/>(bring your own key) | N/A | N/A | Yes | Yes |

| Capture | N/A | Priced separately | Included | Included |

| Dynamic partitions scale-out | N/A | N/A | Yes | Yes |

| Ingress events | Pay per million events | Pay per million events | Included | Included |

| Runtime audit logs | N/A | N/A | Yes | Yes |

| Availability zone | Yes | Yes | Yes | Yes |

| Geo-disaster recovery | N/A | Yes | Yes | Yes |

| Geo-replication | N/A | N/A | Yes | Yes |

| IP firewall | N/A | Yes | Yes | Yes |

> [!NOTE]

> *Included* in the table means the feature is available and there's no separate charge for using it.


# Event Hubs Premium Faq

### What can I achieve with a processing unit?

How much you can ingest and stream with a processing unit depends on factors such as your producers, consumers, and the rate at which you're ingesting and processing. For details on processing units, see [Scaling with Event Hubs](../event-hubs-scalability.md).

### Can I migrate my Standard namespaces to Premium namespaces?

We currently don't support migrating from Standard namespaces to Premium namespaces.


# Event Hubs Dedicated Clusters Faq

### What can I achieve with a cluster?

For an Event Hubs cluster, how much you can ingest and stream depends on factors such as your producers, consumers, and the rate at which you're ingesting and processing.

The following table shows the benchmark results that we achieved during our testing with a legacy dedicated cluster.

| Payload shape | Receivers | Ingress bandwidth| Ingress messages | Egress bandwidth | Egress messages | Total TUs | TUs per CU |

| ------------- | --------- | ---------------- | ------------------ | ----------------- | ------------------- | --------- | ---------- |

| Batches of 100x1KB | 2 | 400 MB/sec | 400k messages/sec | 800 MB/sec | 800k messages/sec | 400 TUs | 100 TUs |

| Batches of 10x10KB | 2 | 666 MB/sec | 66.6k messages/sec | 1.33 GB/sec | 133k messages/sec | 666 TUs | 166 TUs |

| Batches of 6x32KB | 1 | 1.05 GB/sec | 34k messages/sec | 1.05 GB/sec | 34k messages/sec | 1,000 TUs | 250 TUs |

In the testing, the following criteria were used:

- A Dedicated-tier Event Hubs cluster with four CUs was used.

- The event hub used for ingestion had 200 partitions.

- The data that was ingested was received by two receiver applications receiving from all partitions.

### Can I scale up or scale down my cluster?

If you create the cluster with the **Support scaling** option set, you can use the [self-serve experience](../event-hubs-dedicated-cluster-create-portal.md#scale-a-dedicated-cluster) to scale out and scale in, as needed. You can scale up to 10 CUs with self-serve scalable clusters. Self-serve scalable dedicated clusters are based on new infrastructure, so they perform better than dedicated clusters that don't support self-serve scaling. The performance of dedicated clusters depends on factors such as resource allocation, number of partitions, and storage. We recommend that you determine the required number of CUs after you test with a real workload.

[Submit a support request](../event-hubs-dedicated-cluster-create-portal.md#submit-a-support-request) to scale out or scale in your dedicated cluster in the following scenarios:

- You need more than 10 CUs for a self-serve scalable dedicated cluster (a cluster that was created with the **Support scaling** option set).

- You need to scale out or scale in a cluster that was created without selecting the **Support scaling** option.

- You need to scale out or scale in a dedicated cluster that was created before the self-serve experience was released.

> [!WARNING]

> You won't be able to delete the cluster for at least four hours after you create it. You're charged for a minimum of four hours of usage of the cluster. For more information on pricing, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).

### Can I migrate from a legacy cluster to a self-serve scalable cluster?

Because of the difference in the underlying hardware and software infrastructure, we don't currently support migration of clusters that don't support self-serve scaling to self-serve scalable dedicated clusters. If you want to use self-serve scaling, you must re-create the cluster. To learn how to create a scalable cluster, see [Create an Event Hubs dedicated cluster](../event-hubs-dedicated-cluster-create-portal.md).

### When should I scale my dedicated cluster?

CPU consumption is the key indicator of the resource consumption of your dedicated cluster. When the overall CPU consumption begins to reach 70% (without observing any abnormal conditions, such as a high number of server errors or a low number of successful requests), that means your cluster is moving toward its maximum capacity. You can use this information as an indicator to consider whether you need to scale up your dedicated cluster or not.

To monitor the CPU usage of the dedicated cluster, follow these steps:

1. On the **Metrics** page of your Event Hubs dedicated cluster, select **Add metric**.

1. Select **CPU** as the metric and use **Max** as the aggregation.

1. Select **Add filter** and add a filter for the **Property** type **Role**. Use the equal operator and select all the values (**Backend** and **Gateway**) from the dropdown list.

Then you can monitor this metric to determine when you should scale your dedicated cluster. You can also set up [alerts](/azure/azure-monitor/alerts/alerts-overview) against this metric to get notified when CPU usage reaches the thresholds you set.

### How does geo-disaster recovery work with my cluster?

You can geo-pair a namespace under a Dedicated-tier cluster with another namespace under a Dedicated-tier cluster. We don't encourage pairing a Dedicated-tier namespace with a namespace in the Standard offering because the throughput limit is incompatible and results in errors.

### Can I migrate my Standard or Premium namespaces to a Dedicated-tier cluster?

We don't currently support an automated migration process for migrating your Event Hubs data from a Standard or Premium namespace to a dedicated one.

### Why does a legacy zone-redundant dedicated cluster have a minimum of eight CUs?

To provide zone redundancy for the Dedicated offering, all compute resources must have three replicas across three datacenters in the same region. This minimum requirement supports zone redundancy (so that the service can still function when two zones or datacenters are down) and results in a compute capacity equivalent to eight CUs.

We can't change this quota. It's a restriction of the current architecture with a Dedicated tier.


# Event Hubs Trusted Services

## Trusted Microsoft services

When you enable the **Allow trusted Microsoft services to bypass this firewall** setting, the following services within the same tenant are granted access to your Event Hubs resources.

| Trusted service | Supported usage scenarios |

| --------------- | ------------------------- |

| Azure Event Grid | Allows Azure Event Grid to send events to event hubs in your Event Hubs namespace. You also need to do the following steps: <ul><li>Enable system-assigned identity for a topic or a domain</li><li>Add the identity to the Azure Event Hubs Data Sender role on the Event Hubs namespace</li><li>Then, configure the event subscription that uses an event hub as an endpoint to use the system-assigned identity.</li></ul> <p>For more information, see [Event delivery with a managed identity](../../event-grid/managed-service-identity.md)</p>|

| Azure Stream Analytics | Allows an Azure Stream Analytics job to read data from ([input](../../stream-analytics/stream-analytics-add-inputs.md)) or write data to ([output](../../stream-analytics/event-hubs-output.md)) event hubs in your Event Hubs namespace. <p>**Important**: The Stream Analytics job should be configured to use a **managed identity** to access the event hub. For more information, see [Use managed identities to access the event hub from an Azure Stream Analytics job (Preview)](../../stream-analytics/event-hubs-managed-identity.md). </p>|

| Azure IoT Hub | Allows IoT Hub to send messages to event hubs in your Event Hubs namespace. You also need to do the following steps: <ul><li>Enable system-assigned identity for your IoT hub</li><li>Add the identity to the Azure Event Hubs Data Sender role on the Event Hubs namespace.</li><li>Then, configure the IoT Hub that uses an event hub as a custom endpoint to use the identity-based authentication.</li></ul>

| Azure API Management | <p>The API Management service allows you to send events to an event hub in your Event Hubs namespace.</p> <ul><li>You can trigger custom workflows by sending events to your event hub when an API is invoked by using the [send-request policy](../../api-management/api-management-sample-send-request.md).</li><li>You can also treat an event hub as your backend in an API. For a sample policy, see [Authenticate using a managed identity to access an event hub](https://github.com/Azure/api-management-policy-snippets/blob/master/examples/Authenticate%20using%20Managed%20Identity%20to%20access%20Event%20Hub.xml). You also need to do the following steps:<ol><li>Enable system-assigned identity on the API Management instance. For instructions, see [Use managed identities in Azure API Management](../../api-management/api-management-howto-use-managed-service-identity.md).</li><li>Add the identity to the **Azure Event Hubs Data Sender** role on the Event Hubs namespace</li></ol></li></ul> |

| Azure Monitor (Diagnostic Settings and Action Groups) | Allows Azure Monitor to send diagnostic information and alert notifications to event hubs in your Event Hubs namespace. Azure Monitor can read from the event hub and also write data to the event hub. |

| Azure Synapse | Allows Azure Synapse to connect to the event hub using the Synapse Workspace Managed Identity. Add the Azure Event Hubs Data Sender, Receiver or Owner role to the identity on the Event Hubs namespace. |

| Azure Data Explorer | Allows Azure Data Explorer to receive events from the event hub using the Managed Identity of the cluster. You need to do the following steps: <ul><li>[Configure](/azure/data-explorer/configure-managed-identities-cluster) the Managed Identity on Azure Data Explorer</li><li>Grant the **Azure Event Hubs Data Receiver** role to the identity, on the event hub.</li></ul>  |

| Azure IoT Central | <p>Allows IoT Central to export data to event hubs in your Event Hubs namespace. You also need to do the following steps:</p><ul><li>Enable system-assigned identity for your IoT Central application.</li><li>Add the identity to the **Azure Event Hubs Data Sender** role on the Event Hubs namespace.</li><li>Then, configure the Event Hubs [export destination on your IoT Central application](../../iot-central/core/howto-export-to-event-hubs.md) to use identity-based authentication.</li></ul>

| Azure Health Data Services | Allows Healthcare APIs IoT connector to ingest medical device data from your Event Hubs namespace and persist data in your configured [Fast Healthcare Interoperability Resources (FHIR®) service](../../healthcare-apis/fhir/overview.md). The IoT connector should be configured to use a managed identity to access the event hub. For more information, see [Get started with the IoT connector - Azure Healthcare APIs](../../healthcare-apis/iot/get-started.md). |

| Azure Digital Twins | Allows Azure Digital Twins to egress data to event hubs in your Event Hubs namespace. You also need to do the following steps: <p><ul><li>Enable system-assigned identity for your Azure Digital Twins instance.</li><li>Add the identity to the **Azure Event Hubs Data Sender** role on the Event Hubs namespace.</li><li>Then, configure an Azure Digital Twins endpoint or Azure Digital Twins data history connection that uses the system-assigned identity to authenticate. For more information about configuring endpoints and event routes to Event Hubs resources from Azure Digital Twins, see [Route Azure Digital Twins events](../../digital-twins/concepts-route-events.md) and [Create endpoints in Azure Digital Twins](../../digital-twins/how-to-create-endpoints.md). </li></ul> |

The other trusted services for Azure Event Hubs can be found below:

- Azure Arc

- Azure Kubernetes

- Azure Machine Learning

- Microsoft Purview


# Event Hubs Connectivity

### What protocols I can use to send and receive events?

Producers or senders can use Advanced Messaging Queuing Protocol (AMQP), Kafka, or HTTPS protocols to send events to an event hub.

Consumers or receivers use AMQP or Kafka to receive events from an event hub. Event Hubs supports only the pull model for consumers to receive events from it. Even when you use event handlers to handle events from an event hub, the event processor internally uses the pull model to receive events from the event hub.

#### AMQP

You can use the **AMQP 1.0** protocol to send events to and receive events from Azure Event Hubs. AMQP provides reliable, performant, and secure communication for both sending and receiving events. You can use it for high-performance and real-time streaming and is supported by most Azure Event Hubs SDKs.

#### HTTPS/REST API

You can only send events to Event Hubs using HTTP POST requests. Event Hubs doesn't support receiving events over HTTPS. It's suitable for lightweight clients where a direct TCP connection isn't feasible.

#### Apache Kafka

Azure Event Hubs has a built-in Kafka endpoint that supports Kafka producers and consumers. Applications that are built using Kafka can use Kafka protocol (version 1.0 or later) to send and receive events from Event Hubs without any code changes.

Azure SDKs abstract the underlying communication protocols and provide a simplified way to send and receive events from Event Hubs using languages like C#, Java, Python, JavaScript, etc.

### What ports do I need to open on the firewall?

You can use the following protocols with Azure Event Hubs to send and receive events:

- Advanced Message Queuing Protocol 1.0 (AMQP)

- Hypertext Transfer Protocol 1.1 with Transport Layer Security (HTTPS)

- Apache Kafka

See the following table for the outbound ports you need to open to use these protocols to communicate with Azure Event Hubs.

| Protocol | Ports | Details |

| -------- | ----- | ------- |

| AMQP | 5671 and 5672 | See [AMQP protocol guide](../../service-bus-messaging/service-bus-amqp-protocol-guide.md) |

| HTTPS | 443 | This port is used for the HTTP/REST API and for AMQP-over-WebSockets. |

| Kafka | 9093 | See [Use Event Hubs from Kafka applications](../azure-event-hubs-apache-kafka-overview.md)

The HTTPS port is required for outbound communication also when AMQP is used over port 5671, because several management operations performed by the client SDKs and the acquisition of tokens from Microsoft Entra ID (when used) run over HTTPS.

The official Azure SDKs generally use the AMQP protocol for sending and receiving events from Event Hubs. The AMQP-over-WebSockets protocol option runs over port TCP 443 just like the HTTP API, but is otherwise functionally identical with plain AMQP. This option has higher initial connection latency because of extra handshake round trips and slightly more overhead as tradeoff for sharing the HTTPS port. If this mode is selected, TCP port 443 is sufficient for communication. The following options allow selecting the plain AMQP or AMQP WebSockets mode:

| Language | Option   |

| -------- | ----- |

| .NET     | [EventHubConnectionOptions.TransportType](/dotnet/api/azure.messaging.eventhubs.eventhubconnectionoptions.transporttype) property with [EventHubsTransportType.AmqpTcp](/dotnet/api/azure.messaging.eventhubs.eventhubstransporttype) or [EventHubsTransportType.AmqpWebSockets](/dotnet/api/azure.messaging.eventhubs.eventhubstransporttype) |

| Java     | [com.microsoft.azure.eventhubs.EventProcessorClientBuilder.transporttype](https://github.com/Azure/azure-sdk-for-java/blob/master/sdk/eventhubs/azure-messaging-eventhubs/src/main/java/com/azure/messaging/eventhubs/EventProcessorClientBuilder.java) with [AmqpTransportType.AMQP](/java/api/com.azure.core.amqp.amqptransporttype) or [AmqpTransportType.AMQP_WEB_SOCKETS](/java/api/com.azure.core.amqp.amqptransporttype) |

| Node  | [EventHubConsumerClientOptions](/javascript/api/@azure/event-hubs/eventhubconsumerclientoptions) has a `webSocketOptions` property. |

| Python | [EventHubConsumerClient.transport_type](/python/api/azure-eventhub/azure.eventhub.eventhubconsumerclient) with [TransportType.Amqp](/python/api/azure-eventhub/azure.eventhub.transporttype) or [TransportType.AmqpOverWebSocket](/python/api/azure-eventhub/azure.eventhub.transporttype) |

### What IP addresses do I need to allow?

When you're working with Azure, sometimes you have to allow specific IP address ranges or URLs in your corporate firewall or proxy to access all Azure services you're using or trying to use. Verify that the traffic is allowed on IP addresses used by Event Hubs. For IP addresses used by Azure Event Hubs: see [Azure IP Ranges and Service Tags - Public Cloud](https://www.microsoft.com/download/details.aspx?id=56519).

Also, verify that the IP address for your namespace is allowed. To find the right IP addresses to allow for your connections, follow these steps:

1. Run the following command from a command prompt:

```

nslookup <YourNamespaceName>.servicebus.windows.net

```

2. Note down the IP address returned in `Non-authoritative answer`.

If you use a namespace hosted in an older cluster (based on Cloud Services - CNAME ending in *.cloudapp.net) and the namespace is **zone redundant**, you need to follow few extra steps. If your namespace is on a newer cluster (based on Virtual Machine Scale Set - CNAME ending in *.cloudapp.azure.com) and zone redundant you can skip below steps.

1. First, you run nslookup on the namespace.

```

nslookup <yournamespace>.servicebus.windows.net

```

2. Note down the name in the **non-authoritative answer** section, which is in one of the following formats:

```

<name>-s1.cloudapp.net

<name>-s2.cloudapp.net

<name>-s3.cloudapp.net

```

3. Run nslookup for each one with suffixes s1, s2, and s3 to get the IP addresses of all three instances running in three availability zones,

> [!NOTE]

> The IP address returned by the `nslookup` command isn't a static IP address. However, it remains constant until the underlying deployment is deleted or moved to a different cluster.

### What client IPs are sending events to or receiving events from my namespace?

First, enable [IP filtering](../event-hubs-ip-filtering.md) on the namespace.

Then, Enable diagnostic logs for [Event Hubs virtual network connection events](../monitor-event-hubs-reference.md#event-hubs-virtual-network-connection-event-schema) by following instructions in the [Enable diagnostic logs](/azure/azure-monitor/essentials/diagnostic-settings). You see the IP address for which connection is denied.

```json

{

"SubscriptionId": "0000000-0000-0000-0000-000000000000",

"NamespaceName": "namespace-name",

"IPAddress": "1.2.3.4",

"Action": "Deny Connection",

"Reason": "IPAddress doesn't belong to a subnet with Service Endpoint enabled.",

"Count": "65",

"ResourceId": "/subscriptions/0000000-0000-0000-0000-000000000000/resourcegroups/testrg/providers/microsoft.eventhub/namespaces/namespace-name",

"Category": "EventHubVNetConnectionEvent"

}

```

> [!IMPORTANT]

> Virtual network logs are generated only if the namespace allows access from **specific IP addresses** (IP filter rules). If you don't want to restrict access to your namespace using these features and still want to get virtual network logs to track IP addresses of clients connecting to the Event Hubs namespace, you could use the following workaround: [Enable IP filtering](../event-hubs-ip-filtering.md), and add the total addressable IPv4 range (`0.0.0.0/1` - `128.0.0.0/1`) and IPv6 range (`::/1` - `8000::/1`).

> [!NOTE]

> Currently, it's not possible to determine the source IP of an individual message or event.


# Event Hubs Diagnostic Log Schema

Event Hubs captures diagnostic logs for the following categories:

| Category | Description |

| -------- | ----------- |

| Archive Logs | Captures information about [Event Hubs Capture](../event-hubs-capture-overview.md) operations, specifically, logs related to capture errors. |

| Operational Logs | Capture all management operations that are performed on the Azure Event Hubs namespace. Data operations aren't captured, because of the high volume of data operations that are conducted on Azure Event Hubs. |

| Auto scale logs | Captures autoinflate operations done on an Event Hubs namespace. |

| Kafka coordinator logs | Captures Kafka coordinator operations related to Event Hubs. |

| Kafka user error logs | Captures information about Kafka APIs called on Event Hubs. |

| Event Hubs virtual network connection event | Captures information about IP addresses and virtual networks sending traffic to Event Hubs. |

| Customer-managed key user logs | Captures operations related to customer-managed key. |

| Runtime Audit Logs | Capture aggregated diagnostic information for all data plane access operations (such as send or receive events) in Event Hubs. |

| Application Metric Logs | Capture the aggregated information on certain metrics related to data plane operations. |

All logs are stored in JavaScript Object Notation (JSON) format. Each entry has string fields that use the format described in the following sections.

### Archive logs schema

Archive log JSON strings include elements listed in the following table:

Name | Description | Supported in Azure Diagnostics | Supported in AZMSArchiveLogs (Resource specific table)

------- | ------- | ------| ------

`TaskName` | Description of the task that failed | Yes | Yes

`ActivityId` | Internal ID, used for tracking | Yes | Yes

`trackingId` | Internal ID, used for tracking | Yes | Yes

`resourceId` | Azure Resource Manager resource ID | yes | Yes

`eventHub` | Event hub full name (includes namespace name)| Yes | No

`EventhubName`| Name of event hub entity | No | Yes

`partitionId` | Event hub's partition being written to | Yes | Yes

`archiveStep` | possible values: ArchiveFlushWriter, DestinationInit | Yes | Yes

`startTime` | Failure start time | Yes | No

`Time Generated (UTC)` | Timestamp of operation | No | Yes

`failures` | Number of times the failure occurred | Yes | Yes

`durationInSeconds` | Duration of failure | Yes | Yes

`message` | Error message | Yes | Yes

`category` | Log Category | Yes | No

`Provider`|Name of the service emitting the logs, for example, Event Hubs | No | Yes

`Type`  | Type of log emitted| No | Yes

The following code is an example of an archive log JSON string:

AzureDiagnostics:

```json

{

"TaskName": "EventHubArchiveUserError",

"ActivityId": "000000000-0000-0000-0000-0000000000000",

"trackingId": "0000000-0000-0000-0000-00000000000000000",

"resourceId": "/SUBSCRIPTIONS/000000000-0000-0000-0000-0000000000000/RESOURCEGROUPS/<Resource Group Name>/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/<Event Hubs Namespace Name>",

"eventHub": "<Event Hub full name>",

"partitionId": "1",

"archiveStep": "ArchiveFlushWriter",

"startTime": "9/22/2016 5:11:21 AM",

"failures": 3,

"durationInSeconds": 360,

"message": "Microsoft.WindowsAzure.Storage.StorageException: The remote server returned an error: (404) Not Found. ---> System.Net.WebException: The remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",

"category": "ArchiveLogs"

}

```

Resource specific table entry:

```json

{

"TaskName": "EventHubArchiveUserError",

"ActivityId": "000000000-0000-0000-0000-0000000000000",

"trackingId": "0000000-0000-0000-0000-00000000000000000",

"resourceId": "/SUBSCRIPTIONS/000000000-0000-0000-0000-0000000000000/RESOURCEGROUPS/<Resource Group Name>/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/<Event Hubs Namespace Name>",

"EventHubName": "<Event Hub full name>",

"partitionId": "1",

"archiveStep": "ArchiveFlushWriter",

"TimeGenerated(UTC)": "9/22/2016 5:11:21 AM",

"failures": 3,

"durationInSeconds": 360,

"message": "Microsoft.WindowsAzure.Storage.StorageException: The remote server returned an error: (404) Not Found. ---> System.Net.WebException: The remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",

"Provider":"EVENTHUB",

"Type":"AZMSArchiveLogs"

}

```

### Operational logs schema

Operational log JSON strings include elements listed in the following table:

Name | Description | Supported in AzureDiagnostics | Supported in AZMSOperationalLogs (Resource specific table)

------- | -------| ----| -----|

`ActivityId` | Internal ID, used for tracking purposes | Yes | Yes

`EventName` | Operation name. For a list of values for this element, see the [Event names](#event-names) | Yes | Yes

`resourceId` | Azure Resource Manager resource ID | Yes | Yes

`SubscriptionId` | Subscription ID | Yes | Yes

`EventTimeString` | Operation time | Yes | No

`Time Generated (UTC)` | Timestamp of operation | No | Yes

`EventProperties` |Properties for the operation. This element provides more information about the event as shown in the following example. | Yes | Yes

`Status` | Operation status. The value can be either **Succeeded** or **Failed**.  | Yes | Yes

`Caller` | Caller of operation (Azure portal or management client) | Yes | Yes

`Category` | Log Category | Yes | No

`Provider`|Name of the service emitting the logs, for example, Event Hubs | No | Yes

`Type`  | Type of logs emitted | No | Yes

The following code is an example of an operational log JSON string:

AzureDiagnostics:

```json

Example:

{

"ActivityId": "00000000-0000-0000-0000-00000000000000",

"EventName": "Create EventHub",

"resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-0000000000000/RESOURCEGROUPS/<Resource Group Name>/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/<Event Hubs namespace name>",

"SubscriptionId": "000000000-0000-0000-0000-000000000000",

"EventTimeString": "9/28/2016 8:40:06 PM +00:00",

"EventProperties": "{\"SubscriptionId\":\"0000000000-0000-0000-0000-000000000000\",\"Namespace\":\"<Namespace Name>\",\"Via\":\"https://<Namespace Name>.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",

"Status": "Succeeded",

"Caller": "ServiceBus Client",

"category": "OperationalLogs"

}

```

Resource specific table entry:

```json

Example:

{

"ActivityId": "00000000-0000-0000-0000-00000000000000",

"EventName": "Create EventHub",

"resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-0000000000000/RESOURCEGROUPS/<Resource Group Name>/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/<Event Hubs namespace name>",

"SubscriptionId": "000000000-0000-0000-0000-000000000000",

"TimeGenerated (UTC)": "9/28/2016 8:40:06 PM +00:00",

"EventProperties": "{\"SubscriptionId\":\"0000000000-0000-0000-0000-000000000000\",\"Namespace\":\"<Namespace Name>\",\"Via\":\"https://<Namespace Name>.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",

"Status": "Succeeded",

"Caller": "ServiceBus Client",

"Provider": "EVENTHUB",

"Type":"AZMSOperationalLogs"

}

```

#### Event names

Event name is populated as operation type + resource type from the following enumerations. For example, `Create Queue`, `Retrieve Event Hub`, or `Delete Rule`.

| Operation type | Resource type |

| -------------- | ------------- |

|- Create<br>- Update<br>- Delete<br>- Retrieve<br>- Unknown | - Namespace<br>- Queue<br>- Topic<br>- Subscription<br>- Event Hubs<br>- SharedAccessPolicy<br>- UsageCredit<br>- Rule<br>- ConsumerGroup |

### Autoscale logs schema

Autoscale log JSON includes elements listed in the following table:

| Name | Description | Supported in Azure Diagnostics | Supported in AZMSAutoscaleLogs (Resource specific table)

| ---- | ----------- |----| ----|

| `TrackingId` | Internal ID, which is used for tracing purposes | Yes | Yes

| `ResourceId` | Azure Resource Manager resource ID. | Yes | Yes

| `Message` | Informational message, which provides details about autoinflate action. The message contains previous and current value of throughput unit for a given namespace and what triggered the inflate of the TU. | Yes | Yes

|`Time Generated (UTC)` | Timestamp of operation | No | Yes

|`Provider`|Name of Service emitting the logs, for example, Event Hubs | No | Yes

|`Type`  | Type of logs emitted | No | Yes

Here's an example autoscale event:

AzureDiagnostics:

```json

{

"TrackingId": "fb1b3676-bb2d-4b17-85b7-be1c7aa1967e",

"Message": "Scaled-up EventHub TUs (UpdateStartTimeUTC: 5/13/2021 7:48:36 AM, PreviousValue: 1, UpdatedThroughputUnitValue: 2, AutoScaleReason: 'IncomingMessagesPerSecond reached 2170')",

"ResourceId": "/subscriptions/0000000-0000-0000-0000-000000000000/resourcegroups/testrg/providers/microsoft.eventhub/namespaces/namespace-name"

}

```

Resource specific table entry:

```json

{

"TrackingId": "fb1b3676-bb2d-4b17-85b7-be1c7aa1967e",

"Message": "Scaled-up EventHub TUs (UpdateStartTimeUTC: 5/13/2021 7:48:36 AM, PreviousValue: 1, UpdatedThroughputUnitValue: 2, AutoScaleReason: 'IncomingMessagesPerSecond reached 2170')",

"ResourceId": "/subscriptions/0000000-0000-0000-0000-000000000000/resourcegroups/testrg/providers/microsoft.eventhub/namespaces/namespace-name",

"timeGenerated (UTC)" : "9/28/2022 8:40:06 PM +00:00",

"Provider" : "EVENTHUB",

"Type" : "AZMSAutoscaleLogs"

}

```

### Kafka coordinator logs schema

Kafka coordinator log JSON includes elements listed in the following table:

| Name | Description | Supported in Azure Diagnostics | Supported in AZMSKafkaCoordinatorLogs (Resource specific table)

| ---- | ----------- |----|----|

| `RequestId` | Request ID, which is used for tracing purposes | Yes | Yes

| `ResourceId` | Azure Resource Manager resource ID | Yes | Yes

| `Operation` | Name of the operation done during the group coordination | Yes | Yes

| `ClientId` | Client ID | Yes | Yes

| `NamespaceName` | Namespace name | Yes | Yes

| `SubscriptionId` | Azure subscription ID | Yes | Yes

| `Message` | Informational or warning message, which provides details about actions done during the group coordination. | Yes | Yes

|`Time Generated (UTC)` | Timestamp of operation | No | Yes

|`Provider`|Name of Service emitting the logs, for example, ServiceBus | No | Yes

|`Type`  | Type of log emitted | No | Yes

#### Example

AzureDiagnostics:

```json

{

"RequestId": "FE01001A89E30B020000000304620E2A_KafkaExampleConsumer#0",

"Operation": "Join.Start",

"ClientId": "KafkaExampleConsumer#0",

"Message": "Start join group for new member namespace-name:c:$default:I:KafkaExampleConsumer#0-cc40856f7f3c4607915a571efe994e82, current group size: 0, API version: 2, session timeout: 10000ms, rebalance timeout: 300000ms.",

"SubscriptionId": "0000000-0000-0000-0000-000000000000",

"NamespaceName": "namespace-name",

"ResourceId": "/subscriptions/0000000-0000-0000-0000-000000000000/resourcegroups/testrg/providers/microsoft.eventhub/namespaces/namespace-name",

"Category": "KafkaCoordinatorLogs"

}

```

Resource Specific table entry:

```json

{

"RequestId": "FE01001A89E30B020000000304620E2A_KafkaExampleConsumer#0",

"Operation": "Join.Start",

"ClientId": "KafkaExampleConsumer#0",

"Message": "Start join group for new member namespace-name:c:$default:I:KafkaExampleConsumer#0-cc40856f7f3c4607915a571efe994e82, current group size: 0, API version: 2, session timeout: 10000ms, rebalance timeout: 300000ms.",

"SubscriptionId": "0000000-0000-0000-0000-000000000000",

"NamespaceName": "namespace-name",

"ResourceId": "/subscriptions/0000000-0000-0000-0000-000000000000/resourcegroups/testrg/providers/microsoft.eventhub/namespaces/namespace-name",

"Time Generated (UTC) ": "9/28/2022 8:40:06 PM +00:00",

"Provider" : "EVENTHUB",

"Type" : "AZMSKafkaCoordinatorLogs"

}

```

### Kafka user error logs schema

Kafka user error log JSON includes elements listed in the following table:

| Name | Description | Supported in Azure Diagnostics | Supported in AZMSKafkaUserErrorLogs (Resource specific table)

| ---- | ----------- |----| ----|

| `TrackingId` | Tracking ID, which is used for tracing purposes. | Yes | Yes

| `NamespaceName` | Namespace name | Yes | Yes

| `Eventhub` | Event hub name | Yes | Yes

| `PartitionId` | Partition ID | Yes | Yes

| `GroupId` | Group ID | Yes | Yes

| `ClientId` | Client ID | Yes | Yes

| `ResourceId` | Azure Resource Manager resource ID. | Yes | Yes

| `Message` | Informational message, which provides details about an error | Yes | Yes

|`TimeGenerated (UTC)` | Timestamp for executed operation | No | Yes

|`Provider` | Name of service emitting the logs, for example, Event Hubs | No | Yes

| `Type` | Type of log emitted | NO | Yes

### Event Hubs virtual network connection event schema

Event Hubs virtual network (virtual network) connection event JSON includes elements listed in the following table:

| Name | Description | Supported in Azure Diagnostics | Supported in AZMSVNetConnectionevents (Resource specific table) |

| ---  | ----------- |-----| -----|

| `SubscriptionId` | Azure subscription ID | Yes | Yes

| `NamespaceName` | Namespace name | Yes | Yes

| `IPAddress` | IP address of a client connecting to the Event Hubs service | Yes | Yes

| `Action` | Action done by the Event Hubs service when evaluating connection requests. Supported actions are **Accept Connection** and **Deny Connection**. | Yes | Yes

| `Reason` | Provides a reason why the action was done | Yes | No

| `Message` | Provides a reason why the action was done | No | Yes

| `Count` | Number of occurrences for the given action | Yes | Yes

| `ResourceId` | Azure Resource Manager resource ID. | Yes | Yes

|`Time Generated (UTC)` | Timestamp of operation | No | Yes

|`Provider`|Name of Service emitting the logs, for example, ServiceBus | No | Yes

|`Type`  | AZMSVNetConnectionevents | No | Yes

Virtual network logs are generated only if the namespace allows access from **selected networks** or from **specific IP addresses** (IP filter rules). If you don't want to restrict the access to your namespace using these features and still want to get virtual network logs to track IP addresses of clients connecting to the Event Hubs namespace, you could use the following workaround. [Enable IP filtering](../event-hubs-ip-filtering.md), and add the total addressable IPv4 range  (`0.0.0.0/1` - `128.0.0.0/1`) and IPv6 range (`::/1` - `8000::/1`). Event Hubs IP filtering doesn't support IPv6 ranges. You might see private endpoint addresses in the IPv6 format in the log.

#### Example

AzureDiagnostics:

```json

{

"SubscriptionId": "0000000-0000-0000-0000-000000000000",

"NamespaceName": "namespace-name",

"IPAddress": "1.2.3.4",

"Action": "Deny Connection",

"Reason": "IPAddress doesn't belong to a subnet with Service Endpoint enabled.",

"Count": "65",

"ResourceId": "/subscriptions/0000000-0000-0000-0000-000000000000/resourcegroups/testrg/providers/microsoft.eventhub/namespaces/namespace-name",

"Category": "EventHubVNetConnectionEvent"

}

```

Resource specific table entry:

```json

{

"SubscriptionId": "0000000-0000-0000-0000-000000000000",

"NamespaceName": "namespace-name",

"IPAddress": "1.2.3.4",

"Action": "Deny Connection",

"Message": "IPAddress doesn't belong to a subnet with Service Endpoint enabled.",

"Count": "65",

"ResourceId": "/subscriptions/0000000-0000-0000-0000-000000000000/resourcegroups/testrg/providers/microsoft.eventhub/namespaces/namespace-name",

"Provider": "EVENTHUB",

"Time Generated (UTC) ": "9/28/2022 8:40:06 PM +00:00",

"Type" : "AZMSKafkauserErrorlogs"

}

```

### Customer-managed key user logs schema

Customer-managed key user log JSON includes elements listed in the following table:

| Name | Description | Supported in Azure Diagnostics | Supported in AZMSCustomerManagedKeyUserLogs (Resource specific table)

| ---- | ----------- |-----|-----|

| `Category` | Type of category for a message. It's one of the following values: **error** and **info**. For example, if the key from your key vault is being disabled, then it would be an information category or if a key can't be unwrapped, it could fall under error.| Yes | Yes

| `ResourceId` | Internal resource ID, which includes Azure subscription ID and namespace name | Yes | Yes

| `KeyVault` | Name of the Key Vault resource | Yes | Yes

| `Key` | Name of the Key Vault key that's used to encrypt the Event Hubs namespace. | Yes | Yes

| `Version` | Version of the Key Vault key.| Yes | Yes

| `Operation` | The operation that's performed on the key in your key vault. For example, disable/enable the key, wrap, or unwrap. | Yes | Yes

| `Code` | The code associated with the operation. Example: Error code, 404 means that key wasn't found. | Yes | Yes

| `Message` | Message, which provides details about an error or informational message | Yes | Yes

|`Time Generated (UTC)` | Timestamp of operation | No | Yes

|`Provider`|Name of Service emitting the logs, for example, ServiceBus | No | Yes

|`Type`  | Type of log emitted | No | Yes

Here's an example of the  log for a customer managed key:

AzureDiagnostics:

```json

{

"TaskName": "CustomerManagedKeyUserLog",

"ActivityId": "11111111-1111-1111-1111-111111111111",

"category": "error"

"resourceId": "/SUBSCRIPTIONS/11111111-1111-1111-1111-11111111111/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",

"keyVault": "https://mykeyvault.vault-int.azure-int.net",

"key": "mykey",

"version": "1111111111111111111111111111111",

"operation": "wrapKey",

"code": "404",

"message": "Key not found: ehbyok0/111111111111111111111111111111"

}

{

"TaskName": "CustomerManagedKeyUserLog",

"ActivityId": "11111111111111-1111-1111-1111111111111",

"category": "info"

"resourceId": "/SUBSCRIPTIONS/111111111-1111-1111-1111-11111111111/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",

"keyVault": "https://mykeyvault.vault-int.azure-int.net",

"key": "mykey",

"version": "111111111111111111111111111111",

"operation": "disable | restore",

"code": "",

"message": ""

}

```

Resource specific table entry:

```json

{

"TaskName": "CustomerManagedKeyUserLog",

"ActivityId": "11111111-1111-1111-1111-111111111111",

"category": "error"

"resourceId": "/SUBSCRIPTIONS/11111111-1111-1111-1111-11111111111/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",

"keyVault": "https://mykeyvault.vault-int.azure-int.net",

"key": "mykey",

"version": "1111111111111111111111111111111",

"operation": "wrapKey",

"code": "404",

"message": "Key not found: ehbyok0/111111111111111111111111111111",

"Provider": "EVENTHUB",

"Time Generated (UTC) ": "9/28/2022 8:40:06 PM +00:00",

"Type" : "AZMSCustomerManagedKeyUserLogs"

}

{

"TaskName": "CustomerManagedKeyUserLog",

"ActivityId": "11111111111111-1111-1111-1111111111111",

"category": "info"

"resourceId": "/SUBSCRIPTIONS/111111111-1111-1111-1111-11111111111/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",

"keyVault": "https://mykeyvault.vault-int.azure-int.net",

"key": "mykey",

"version": "111111111111111111111111111111",

"operation": "disable | restore",

"code": "",

"message": "",

"Provider": "EVENTHUB",

"Time Generated (UTC) ": "9/28/2022 8:40:06 PM +00:00",

"Type" : "AZMSCustomerManagedKeyUserLogs"

}

```

Following are the common errors codes to look for when BYOK encryption is enabled.

| Action | Error code |	Resulting state of data |

| ------ | ---------- | ----------------------- |

| Remove wrap/unwrap permission from a key vault | 403 |	Inaccessible |

| Remove Microsoft Entra ID role membership from a Microsoft Entra principal that granted the wrap/unwrap permission | 403 |	Inaccessible |

| Delete an encryption key from the key vault | 404 | Inaccessible |

| Delete the key vault | 404 | Inaccessible (assumes soft-delete is enabled, which is a required setting.) |

| Changing the expiration period on the encryption key such that it's already expired | 403 |	Inaccessible  |

| Changing the NBF (not before) such that key encryption key isn't active | 403 | Inaccessible  |

| Selecting the **Allow MSFT Services** option for the key vault firewall or otherwise blocking network access to the key vault that has the encryption key | 403 | Inaccessible |

| Moving the key vault to a different tenant | 404 | Inaccessible |

| Intermittent network issue or DNS/AAD/MSI outage |  | Accessible using cached data encryption key |


# Event Hubs Partition Count

A [partition](../event-hubs-features.md#partitions) is a data organization mechanism that enables parallel publishing and consumption. While it supports parallel processing and scaling, total capacity remains limited by the namespace's scaling allocation. Balance scaling units (throughput units for the standard tier, processing units for the premium tier, or capacity units for the dedicated tier) and partitions to achieve optimal scale.

Start with your workload profile: average payload size, events per second, and sensitivity to throughput drops or latency spikes. Use the per-partition throughput below as a starting point, then validate with load tests:

- **Standard tier**: ~1 MB/s ingress and ~2 MB/s egress per partition.

- **Premium and Dedicated tiers**: ~1-2 MB/s ingress and ~2-5 MB/s egress per partition.

Estimate partitions by dividing your expected ingress and egress by the applicable per-partition rates and taking the larger result. If observed throughput or latency doesn't meet expectations, increase partitions (Premium and Dedicated tiers only) and retest.

Partitions also set the ceiling for consumer parallelism. How that ceiling works depends on the consumer type:

- **Epoch (exclusive) consumers** — Used by `EventProcessorClient` (.NET, Java) and `EventHubConsumerClient` (Python, JavaScript), which is the recommended pattern for production AMQP workloads. Only one epoch consumer can own a given partition in a consumer group at a time. If you deploy more processor instances than partitions, the extra instances aren't assigned any partitions and sit idle until an existing owner releases one. If a new epoch consumer connects with a higher owner level, the service disconnects the current owner with a `ConsumerDisconnected` error, and the new consumer takes over.

- **Non-epoch consumers** — Up to 5 non-epoch receivers can read the same partition concurrently within a consumer group. Each receiver sees the same events (fan-out), so this mode doesn't increase processing throughput per partition. Connecting an epoch consumer to a partition disconnects all non-epoch consumers on that partition.

- **Kafka consumers** — Kafka consumers use the group coordination protocol (`group.id`) instead of AMQP epochs, but the partition-ownership model is equivalent: each partition is assigned to exactly one consumer member within a consumer group at a time. When a new member joins or an existing member leaves, the group rebalances and redistributes partition assignments. If there are more consumer members than partitions, the excess members receive no assignments and remain idle until a future rebalance frees up a partition. To reduce unnecessary rebalancing from transient disconnections, set a unique `group.instance.id` per consumer instance (static membership).

In practice, **the number of partitions equals the maximum number of parallel consumers per consumer group** regardless of whether you use AMQP epoch consumers or Kafka consumers. Factor this into your partition count when you plan for scale-out.

If your application has an affinity to a particular partition, increasing the number of partitions isn't beneficial. For more information, see [availability and consistency](../event-hubs-availability-and-consistency.md).
