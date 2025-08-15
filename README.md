# CST8917-Assignment2

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
| **Monitoring & Observability** | Azure Monitor, Application Insights, Log Analytics. | CloudWatch Logs, X-Ray. | Cloud Logging, Cloud Monitoring, Error Reporting. |
| **Pricing Model** | 400,000 GB-sec & 1M requests free/month; $0.20 per extra 1M requests; $0.000016 per GB-sec; 1 ms billing. | Same as Azure. | 400,000 GB-sec & 2M requests free/month; $0.40 per extra 1M requests; $0.0000125 per GB-sec; 100 ms billing. |
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
| **Monitoring & Observability** | Azure Monitor, Application Insights. | AWS Management Console visualization, CloudWatch, CloudTrail. | Cloud Logging, Cloud Monitoring. |
| **Pricing Model** | Pay-per-action + function execution. | Pay-per-state transition + execution time. | Pay-per-step execution. |
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
| **Monitoring & Observability** | Azure Monitor, run history. | CloudWatch, Step Functions console. | Cloud Logging, Execution Logs. |
| **Pricing Model** | Pay-per-action/trigger. | Pay per step/event. | Pay per execution. |
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

| Criteria | Azure Service Bus | AWS SQS + SNS | GCP Pub/Sub |
| --- | --- | --- | --- |
| **Core Features** | Queues, topics, sessions, dead-lettering, filters. | SQS (queues), SNS (pub/sub). | Real-time pub/sub, global delivery. |
| **Integration** | Works with Azure Functions, Logic Apps, Event Grid, IoT Hub. | Integrates with Lambda, EventBridge, SNS, SQS. | Integrates with Cloud Functions, Dataflow, BigQuery. |
| **Monitoring & Observability** | Azure Monitor, Service Bus Explorer, DLQ metrics. | CloudWatch, DLQ metrics. | Cloud Logging, Pub/Sub metrics. |
| **Pricing Model** | Tiered: Basic/Standard/Premium by operations & data volume. | Pay-per-request (SQS) and per-notification (SNS). | Pay-as-you-go by message count and data volume. |
| **Strengths** | Rich enterprise features: filtering, sessions, dead-lettering. | Simple, durable, highly available. | Global scale, simple pub/sub model, strong GCP integration. |
| **Weaknesses** | More complex setup; costlier feature-rich tiers. | Lacks advanced features like sessions, filtering. | No FIFO by default; fewer enterprise messaging features. |

**Narrative Analysis:**  
Azure Service Bus stands out for advanced enterprise messaging features—including sessions, filtering, and dead-letter capabilities—making it ideal for complex, resilient architectures. AWS achieves similar functionality through separate services (SQS for queues, SNS for pub/sub), offering simplicity and robustness but with fewer advanced features. GCP Pub/Sub excels in real-time, globally scaled messaging, though it trades off some enterprise-grade capabilities found in Azure Service Bus.

---
## 5. Azure Event Grid

| Cloud Provider | Equivalent Service | Description |
| -------------- | ------------------ | ----------- |
| **Azure**      | Azure Event Grid   | Fully managed Pub/Sub event routing service supporting HTTP and MQTT ingestion, CNCF CloudEvents format, and native integration with Azure services. |
| **AWS**        | Amazon EventBridge | Event bus for routing/filtering AWS and custom events with optional transformations. |
| **GCP**        | Google Eventarc    | Event routing service for GCP resources and HTTP endpoints using CloudEvents. |

**Comparison Table**

| Criteria | Azure Event Grid | AWS EventBridge | Google Eventarc |
| --- | --- | --- | --- |
| **Core Features** | Pub/Sub topics, HTTP & MQTT ingestion, CloudEvents format, filtering by content/metadata. | Rules-based routing, optional transformations, AWS product integrations. | Point-to-point delivery, CloudEvents format, GCP integrations. |
| **Integration** | Azure Functions, Logic Apps, Service Bus, Event Hubs; CI/CD via Azure DevOps & GitHub Actions. | Deep AWS integration, custom API ingestion; works with AWS CI/CD pipelines. | GCP service integration; REST API for external; works with Cloud Build. |
| **Monitoring & Observability** | Azure Monitor, Log Analytics, dead-letter destinations. | CloudWatch, DLQ support, Event Replay. | Cloud Logging, DLQ via Pub/Sub. |
| **Pricing Model** | Pay-per-event (ingress, matches, delivery). | Pay-per-event + state transitions. | Pay-per-event; cost per trigger execution. |
| **Strengths** | Easy Azure integration, HTTP/MQTT ingestion, CloudEvents support. | Deep AWS integration, optional event archival. | Tight GCP integration, CloudEvents support. |
| **Weaknesses** | No event archival, no in-flight processing. | Requires custom development for many external sources. | Limited external delivery options, no processing. |

**Narrative Analysis:**  
Azure Event Grid is best suited for teams operating in the Azure ecosystem who need a lightweight, scalable event routing service. Its Pub/Sub model simplifies scaling and decoupling between event producers and consumers, and its support for the CNCF CloudEvents standard reduces integration effort with compliant sources. While it lacks built-in complex processing, pairing it with Azure Functions or Logic Apps enables flexible workflows. Compared to AWS EventBridge, it offers simpler external event ingestion via HTTP and MQTT, and compared to Google Eventarc, it has stronger support for external destinations.

---

## 6. Azure Event Hubs

| Cloud Provider | Equivalent Service | Description |
| -------------- | ------------------ | ----------- |
| **Azure**      | Azure Event Hubs   | Fully managed real-time data ingestion and streaming platform capable of handling millions of events per second. |
| **AWS**        | Amazon Kinesis     | Real-time data streaming service for high-throughput event processing. |
| **GCP**        | Google Cloud Pub/Sub | Global messaging and event ingestion service for building real-time apps. |

**Comparison Table**

| Criteria | Azure Event Hubs | Amazon Kinesis | Google Cloud Pub/Sub |
| --- | --- | --- | --- |
| **Core Features** | High-throughput ingestion, multiple consumer groups, partitioned streams, Kafka protocol support. | Real-time streaming, shard-based scaling, replay. | Pub/Sub messaging, push/pull delivery, filtering. |
| **Integration** | Azure Functions, Stream Analytics, Synapse, ML; CI/CD via DevOps & GitHub Actions. | AWS Lambda, S3, EMR, SageMaker; pipelines via CodePipeline. | Dataflow, BigQuery, Cloud Functions; integrates with Cloud Build. |
| **Monitoring & Observability** | Azure Monitor, Log Analytics, Event Hubs Capture. | CloudWatch, enhanced monitoring APIs. | Cloud Monitoring, Cloud Logging. |
| **Pricing Model** | Pay-per-event or throughput units; standard/dedicated tiers. | Pay-as-you-go by data volume & shard-hours. | Pay-as-you-go per message; first 10 GB free/month. |
| **Strengths** | High throughput, native Azure integration, Kafka compatibility. | Easy AWS integration, flexible scaling. | Global, scalable, simple setup. |
| **Weaknesses** | Limited retention, complex advanced setup. | Requires shard management, can be costly. | No query language, high volume costs. |

**Narrative Analysis:**  
Azure Event Hubs excels at high-throughput, low-latency event ingestion in Azure ecosystems, making it a strong choice for IoT, analytics, and telemetry pipelines. Its Kafka protocol support improves interoperability, and native Azure service integration enables end-to-end data processing with minimal glue code. While retention limits and advanced configuration complexity can be drawbacks, pairing Event Hubs with Azure Stream Analytics or Functions delivers robust streaming solutions.

---

## Conclusion

Across the evaluated categories—compute, orchestration, integration, messaging, and event streaming—Azure consistently offers tightly integrated services with rich feature sets, making it ideal for building complex, enterprise-grade serverless solutions with minimal glue code. AWS alternatives often provide more granular control and robust scalability but tend to split functionality across multiple services, increasing setup complexity. GCP services prioritize ease of use, fast onboarding, and global reach but can lack certain enterprise-focused capabilities found in Azure or AWS.

From a serverless architecture perspective:  
- **Best for deep service integration & enterprise workflows** → Azure  
- **Best for scalability & fine-grained control** → AWS  
- **Best for simplicity & global reach** → GCP

---

## Reference

- [Serverless showdown: AWS Lambda vs Azure Functions vs Google Cloud Functions](https://www.pluralsight.com/resources/blog/cloud/serverless-showdown-aws-lambda-vs-azure-functions-vs-google-cloud-functions)
- [Google Cloud Dataflow vs AWS Step Functions](https://www.projectpro.io/compare/google-cloud-dataflow-vs-aws-step-functions)
- [Azure Service Bus vs Google Cloud Pub/Sub](https://ably.com/compare/azure-service-bus-vs-google-pub-sub)
- [Amazon SQS vs Google Cloud Pub/Sub](https://ably.com/compare/amazon-sqs-vs-google-pub-sub)
- [Amazon EventBridge Alternatives: Comparing Hookdeck, Azure Event Grid, Google Eventarc, and Confluent Kafka](https://hookdeck.com/blog/amazon-eventbridge-alternatives)
- [Amazon Kinesis vs Azure Event Hubs](https://www.projectpro.io/compare/amazon-kinesis-vs-azure-event-hubs)
- [Azure Event Hubs vs Google Cloud Pub/Sub](https://www.projectpro.io/compare/azure-event-hubs-vs-google-cloud-pub-sub)
