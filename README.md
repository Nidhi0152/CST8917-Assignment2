# CST8917-Assignment2

# CST8917 – Serverless Service Alternatives Report

**Author:** *Nidhi Desai*  

---

## 1. Azure Functions (Triggers & Bindings)

| Cloud Provider | Equivalent Service | Description |
| --- | --- | --- |
| **Azure** | Azure Functions | Microsoft’s FaaS (launched 2016) for event-driven, stateless code with rich triggers and bindings. |
| **AWS** | AWS Lambda | Amazon’s FaaS (launched 2014) running code on AWS events, HTTP, or schedules. |
| **GCP** | Cloud Functions | Google’s FaaS (launched 2016) for lightweight event-driven workloads via HTTP, Pub/Sub, or storage. |

**Comparison Table**

| Criteria | Azure Functions | AWS Lambda | GCP Cloud Functions |
| --- | --- | --- | --- |
| **Core Features** | Multiple triggers & bindings (HTTP, Blob, Queue, Cosmos DB, Event Hub, Service Bus, Timers). | Event sources like S3, DynamoDB Streams, API Gateway, EventBridge. | HTTP triggers, Pub/Sub, Cloud Storage events, Firestore. |
| **Integration** | Deep Azure ecosystem integration; CI/CD with Azure DevOps, GitHub Actions; native HTTP support out of the box. | AWS-native integration; requires API Gateway for HTTP; integrates with SAM, CDK, CodePipeline. | Tight GCP integration; native HTTP support; works with Cloud Build, Cloud Deploy. |
| **Monitoring** | Azure Monitor, Application Insights, Log Analytics. | CloudWatch Logs, X-Ray. | Cloud Logging, Cloud Monitoring, Error Reporting. |
| **Pricing** | 400,000 GB-sec & 1M requests free/month; $0.20 per extra 1M requests; $0.000016 per GB-sec; 1 ms billing. | Same as Azure. | 400,000 GB-sec & 2M requests free/month; $0.40 per extra 1M requests; $0.0000125 per GB-sec; 100 ms billing. |
| **Strengths** | Rich bindings model; streamlined HTTP integration; flexible hosting plans (Consumption, Premium, Dedicated). | Mature ecosystem; custom concurrency controls; provisioned concurrency to reduce cold starts. | Extra free tier requests; simpler setup; Firebase-friendly. |
| **Weaknesses** | Higher cold start times (>5s) than AWS and GCP; no native Go runtime. | Requires separate API Gateway for HTTP; no native bindings. | Rounds duration to nearest 100 ms; no PowerShell runtime. |


**Narrative Analysis:**  
Azure Functions delivers extensive trigger and binding options, making it well-suited for integration-heavy and event-driven workloads. Its multiple hosting plans allow developers to choose between cost efficiency and performance. AWS Lambda is more mature, offers better cold start mitigation, and provides granular concurrency control, but lacks native bindings. GCP Cloud Functions stands out with its larger free request quota and ease of setup, though its 100 ms billing increments can increase costs at scale.

---

## 2. Durable Functions (Chaining, Orchestration, Fan-out/Fan-in)

| Cloud Provider | Equivalent Service | Description |
| --- | --- | --- |
| **Azure** | Durable Functions | Extension of Azure Functions for orchestrated, stateful workflows. |
| **AWS** | AWS Step Functions | Visual workflow orchestration for distributed and serverless applications. |
| **GCP** | Workflows | Orchestrates Google Cloud services and APIs in a serverless workflow. |

**Comparison Table**

| Criteria | Azure Durable Functions | AWS Step Functions | GCP Workflows |
| --- | --- | --- | --- |
| **Core Features** | Function chaining, fan-out/fan-in, human interaction patterns. | Sequential, parallel, branching workflows for order processing, ETL, microservices orchestration. | Sequential, parallel orchestration of APIs and services. |
| **Integration** | Works with Azure Functions & bindings. | Integrates with Lambda, S3, Kinesis, SNS, SQS, DynamoDB, ECS. | Integrates with Cloud Functions, Cloud Run, Pub/Sub, BigQuery. |
| **Monitoring** | Azure Monitor, Application Insights. | AWS Management Console visualization, CloudWatch, CloudTrail. | Cloud Logging, Cloud Monitoring. |
| **Pricing** | Pay-per-action + function execution. | Pay-per-state transition + execution time. | Pay-per-step execution. |
| **Strengths** | Code-first orchestration; deep Azure integration. | Visual design; robust AWS integration; high availability. | Simple YAML/JSON orchestration; easy API automation. |
| **Weaknesses** | Azure-only; less visual. | Costly at scale with many state transitions. | Fewer advanced features than AWS or Azure. |

**Narrative Analysis:**  
Durable Functions target developers preferring code-based orchestration, offering strong integration with Azure services. AWS Step Functions is ideal for visual, large-scale workflows with mature AWS service integration. GCP Workflows offers lightweight orchestration for API-based automation within Google Cloud.

----

## 3. Azure Logic Apps

| Cloud Provider | Equivalent Service | Description |
| --- | --- | --- |
| **Azure** | Logic Apps | Low-code/no-code workflow automation. |
| **AWS** | Step Functions + EventBridge + AppFlow | Combined orchestration & integration. |
| **GCP** | Workflows + AppSheet Automation | API orchestration with low-code automation. |

**Comparison Table**

| Criteria | Azure Logic Apps | AWS Step Functions + EventBridge + AppFlow | GCP Workflows + AppSheet |
| --- | --- | --- | --- |
| **Core Features** | Drag-and-drop connectors, triggers, actions. | Orchestration, event routing, SaaS integration. | Workflow automation, API orchestration. |
| **Integration** | 400+ connectors. | Integrates AWS & SaaS services. | GCP-native & API connectors. |
| **Monitoring** | Azure Monitor, run history. | CloudWatch, Step Functions console. | Cloud Logging, Execution Logs. |
| **Pricing** | Pay-per-action/trigger. | Pay per step/event. | Pay per execution. |
| **Strengths** | Fast prototyping, huge connector library. | Powerful event routing. | Tight GCP integration. |
| **Weaknesses** | Costly at scale. | Multi-service setup needed. | Smaller connector library. |

**Narrative Analysis:**  
Logic Apps are best for quick, connector-heavy automation. AWS splits features across multiple services. GCP offers basic automation with smaller scope.

---

## 4. Azure Service Bus (Queues & Topics)

| Cloud Provider | Equivalent Service | Description |
| -------------- | ------------------ | ----------- |
| **Azure**      | Azure Service Bus  | Enterprise-grade messaging with queues, topics, sessions, filtering, and dead-letter support. |
| **AWS**        | Amazon SQS + SNS   | SQS for queueing messages; SNS for pub/sub notifications. |
| **GCP**        | Google Pub/Sub     | Global pub/sub messaging for real-time event delivery. |

**Comparison Table**

| Criteria              | Azure Service Bus                             | AWS SQS + SNS                                  | GCP Pub/Sub                                              |
|-----------------------|-----------------------------------------------|------------------------------------------------|----------------------------------------------------------|
| **Core Features**     | Queues, topics, sessions, dead-lettering, filters. | SQS (queues), SNS (pub/sub).                   | Real-time pub/sub, global delivery.                      |
| **Integration**       | Works with Azure Functions, Logic Apps, Event Grid, IoT Hub. | Integrates with Lambda, EventBridge, SNS, SQS. | Integrates with Cloud Functions, Dataflow, BigQuery.     |
| **Security**          | RBAC via Azure AD, encryption, AAD integration. | IAM-based, data encryption at rest & transit.  | IAM, VPC controls, encryption at rest & transit.         |
| **Pricing**           | Tiered: Basic/Standard/Premium by operations & data volume. | Pay-per-request (SQS) and per-notification (SNS). | Pay-as-you-go by message count and data volume.          |
| **Scalability & Performance** | High availability, geo-replication, sub-millisecond latency, high throughput. | Auto-scaling queues, high durability.          | Low-latency, high-throughput, SLA-backed performance.    |
| **Strengths**         | Rich enterprise features: filtering, sessions, dead-lettering. | Simple, durable, highly available.             | Global scale, simple pub/sub model, strong GCP integration. |
| **Weaknesses**        | More complex setup; costlier feature-rich tiers. | Lacks advanced features like sessions, filtering. | No FIFO by default; fewer enterprise messaging features. |

**Narrative Analysis:**  
Azure Service Bus stands out for advanced enterprise messaging features—including sessions, filtering, and dead-letter capabilities—making it ideal for complex, resilient architectures. AWS achieves similar functionality through separate services (SQS for queues, SNS for pub/sub), offering simplicity and robustness but with fewer advanced features. GCP Pub/Sub excels in real-time, globally scaled messaging, though it trades off some enterprise-grade capabilities found in Azure Service Bus.

---
## 5. Azure Event Grid

| Cloud Provider | Equivalent Service | Description |
| -------------- | ------------------ | ----------- |
| **Azure**      | Azure Event Grid   | Fully managed Pub/Sub event routing service supporting HTTP and MQTT ingestion, CNCF CloudEvents format, and native integration with Azure services. Ideal for building reactive, event-driven applications with minimal infrastructure management. |
| **AWS**        | Amazon EventBridge | Point-to-point event bus for ingesting, filtering, and routing events with optional simple transformations. Best suited for AWS-centric event-driven architectures. |
| **GCP**        | Google Eventarc    | Point-to-point event delivery service, primarily focused on Google Cloud integrations, supporting the CNCF CloudEvents format but lacking in-flight transformations. |

**Comparison Table**

| Criteria | Azure Event Grid | AWS EventBridge | Google Eventarc |
|----------|------------------|-----------------|-----------------|
| **Core Features** | Pub/Sub topics, HTTP & MQTT ingestion, CloudEvents format, filtering by content/metadata. | Rules-based event routing, optional transformations, AWS product integrations. | Point-to-point delivery, CloudEvents format, GCP product integrations. |
| **Integration** | Native Azure services (Functions, Logic Apps, Service Bus) + HTTP/MQTT for external systems; works with Azure DevOps & GitHub Actions. | Deep AWS integration, custom API ingestion for external systems, works with AWS CI/CD pipelines. | Strong GCP service integration, external via REST API; integrates with Cloud Build. |
| **Monitoring & Observability** | Azure Monitor, Log Analytics, Azure Dashboard, dead-letter destinations. | Amazon CloudWatch, DLQ support, Event Replay. | GCP Cloud Logging, DLQ via Pub/Sub. |
| **Pricing Model** | Pay-per-event (ingress, matches, delivery). Serverless, no infra costs. | Pay-per-event + state transitions (Pipes/Scheduler). | Pay-per-event; cost per trigger execution. |
| **Strengths** | Easy integration with Azure, HTTP/MQTT ingestion, CloudEvents support | Deep AWS integration, optional event archival | Tight GCP integration, CloudEvents support | 
| **Weaknesses** | No event archival, no in-flight processing | Requires custom development for many external sources, complex

**Narrative Analysis:**  
Azure Event Grid is best suited for teams operating in the Azure ecosystem who need a lightweight, scalable event routing service. Its Pub/Sub model simplifies scaling and decoupling between event producers and consumers, and its support for the CNCF CloudEvents standard reduces integration effort with compliant sources. While it lacks built-in complex processing, pairing it with Azure Functions or Logic Apps enables flexible workflows. Compared to AWS EventBridge, it offers simpler external event ingestion via HTTP and MQTT, and compared to Google Eventarc, it has stronger support for external destinations.

---

## 6. Azure Event Hubs

| Cloud Provider | Equivalent Service | Description |
| -------------- | ------------------ | ----------- |
| **Azure**      | Azure Event Hubs   | Fully managed real-time data ingestion and streaming platform capable of handling millions of events per second. Ideal for IoT telemetry, log/event processing, and large-scale analytics pipelines. |
| **AWS**        | Amazon Kinesis     | Fully managed platform for collecting, processing, and analyzing streaming data in real time, with deep AWS service integration. |
| **GCP**        | Google Cloud Pub/Sub | Global messaging and event ingestion service for building real-time, event-driven applications with high throughput and low latency. |

**Comparison Table**

| Criteria | Azure Event Hubs | Amazon Kinesis | Google Cloud Pub/Sub |
|----------|------------------|---------------|----------------------|
| **Core Features** | Real-time event ingestion, multiple consumer groups, partitioned data streams, integration with Azure Functions/Stream Analytics for processing. | Real-time streaming, shard-based scaling, replay capabilities, integration with Lambda/Analytics tools. | Pub/Sub messaging, push & pull delivery, message filtering, fan-out to multiple subscribers. |
| **Integration Options** | Tight Azure integration (Functions, Stream Analytics, Synapse, Machine Learning); supports Kafka protocol; CI/CD via Azure DevOps/GitHub Actions. | Native AWS service integration (S3, Lambda, EMR, SageMaker); pipelines via CodePipeline. | Works with GCP services (Dataflow, BigQuery, Cloud Functions) and integrates with Cloud Build pipelines. |
| **Monitoring & Observability** | Azure Monitor, Log Analytics, Event Hubs Capture for long-term storage. | Amazon CloudWatch, enhanced monitoring APIs. | Google Cloud Monitoring, Cloud Logging. |
| **Pricing Model** | Pay-per-event or throughput units; tiers for standard and dedicated clusters. | Pay-as-you-go based on data volume and shard-hours. | Pay-as-you-go per message volume; first 10 GB free per month. |
| **Strengths** | High throughput, Azure-native integrations, Kafka compatibility. | Easy AWS integration, flexible scaling. | Global, scalable, simple to start. |
| **Weaknesses** | Limited event retention, setup complexity for advanced scenarios. | Requires shard management, can be costly at scale. | No query language, costs can grow with high message volume. |

**Narrative Analysis:**  
Azure Event Hubs excels at high-throughput, low-latency event ingestion in Azure ecosystems, making it a strong choice for IoT, analytics, and telemetry pipelines. Its Kafka protocol support improves interoperability, and native Azure service integration enables end-to-end data processing with minimal glue code. While retention limits and advanced configuration complexity can be drawbacks, pairing Event Hubs with Azure Stream Analytics or Functions delivers robust streaming solutions.

---

## Conclusion

Azure provides strong service integration, making it easier to build fully managed serverless apps. AWS equivalents often split functionality across multiple services, offering more customization but more setup. GCP prioritizes simplicity and global reach but sometimes lacks niche features.

From a serverless perspective:  
- **Best integration & productivity** → Azure  
- **Best scalability & ecosystem** → AWS  
- **Best simplicity & global delivery** → GCP  

---

## Reference

- [Serverless showdown: AWS Lambda vs Azure Functions vs Google Cloud Functions](https://www.pluralsight.com/resources/blog/cloud/serverless-showdown-aws-lambda-vs-azure-functions-vs-google-cloud-functions)
- [Google Cloud Dataflow vs AWS Step Functions](https://www.projectpro.io/compare/google-cloud-dataflow-vs-aws-step-functions)
- [Azure Service Bus vs Google Cloud Pub/Sub](https://ably.com/compare/azure-service-bus-vs-google-pub-sub)
- [Amazon SQS vs Google Cloud Pub/Sub](https://ably.com/compare/amazon-sqs-vs-google-pub-sub)
- [Amazon EventBridge Alternatives: Comparing Hookdeck, Azure Event Grid, Google Eventarc, and Confluent Kafka](https://hookdeck.com/blog/amazon-eventbridge-alternatives)
- [Amazon Kinesis vs Azure Event Hubs](https://www.projectpro.io/compare/amazon-kinesis-vs-azure-event-hubs)
- [Azure Event Hubs vs Google Cloud Pub/Sub](https://www.projectpro.io/compare/azure-event-hubs-vs-google-cloud-pub-sub)
