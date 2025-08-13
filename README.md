# CST8917-Assignment2

# CST8917 – Serverless Service Alternatives Report

**Author:** *Nidhi Desai*  
**Date:** August 15, 2025  

---

## 1. Azure Functions (Triggers & Bindings)

| Cloud Provider | Equivalent Service | Description |
| --- | --- | --- |
| **Azure** | Azure Functions | Event-driven serverless compute service with extensive trigger and binding support. |
| **AWS** | AWS Lambda | Event-driven compute triggered by AWS events, HTTP requests, or schedules. |
| **GCP** | Cloud Functions | Lightweight event-driven compute triggered by HTTP, events, or Pub/Sub. |

**Comparison Table**

| Criteria | Azure Functions | AWS Lambda | GCP Cloud Functions |
| --- | --- | --- | --- |
| **Core Features** | Multiple triggers & bindings (Blob, Queue, HTTP, Cosmos DB, Event Hub, Service Bus). | Event sources like S3, DynamoDB Streams, API Gateway, EventBridge. | HTTP triggers, Pub/Sub, Cloud Storage events, Firestore. |
| **Integration** | Azure-native services, CI/CD via Azure DevOps & GitHub Actions. | AWS-native ecosystem, integrates with SAM, CDK, CodePipeline. | Works with GCP services, Cloud Build, Cloud Deploy. |
| **Monitoring** | Azure Monitor, App Insights, Log Analytics. | CloudWatch Logs, X-Ray. | Cloud Logging, Monitoring, Error Reporting. |
| **Pricing** | Pay-per-execution, first 1M free/month. | Pay-per-execution, first 1M free/month. | Pay-per-execution, first 2M free/month. |
| **Strengths** | Rich bindings, strong integration. | Large ecosystem, mature runtime. | Simple setup, Firebase integration. |
| **Weaknesses** | Azure-focused. | No native bindings. | Limited triggers. |

**Narrative Analysis:**  
Azure Functions shine for integration-heavy workloads with its bindings model. AWS Lambda offers the broadest ecosystem reach but requires manual wiring. GCP Cloud Functions is the most beginner-friendly.

---

## 2. Durable Functions (Chaining, Orchestration, Fan-out/Fan-in)

| Cloud Provider | Equivalent Service | Description |
| --- | --- | --- |
| **Azure** | Durable Functions | Extension of Azure Functions for orchestrated, stateful workflows. |
| **AWS** | AWS Step Functions | Orchestration service for AWS Lambdas & services. |
| **GCP** | Workflows | Service to orchestrate GCP APIs and HTTP endpoints. |

**Comparison Table**

| Criteria | Azure Durable Functions | AWS Step Functions | GCP Workflows |
| --- | --- | --- | --- |
| **Core Features** | Function chaining, fan-out/fan-in, human interaction patterns. | Sequential, parallel, branching workflows. | Sequential, parallel, API orchestration. |
| **Integration** | Works with Azure Functions & bindings. | Integrates with Lambda, ECS, SQS, API Gateway. | Integrates with Cloud Run, Pub/Sub. |
| **Monitoring** | App Insights, Azure Monitor. | CloudWatch, Step Functions Console. | Cloud Logging, Workflow Execution Logs. |
| **Pricing** | Pay-per-action + function execution. | Pay-per-state transition. | Pay-per-step execution. |
| **Strengths** | Code-first orchestration. | Visual workflow design. | Simple YAML orchestration. |
| **Weaknesses** | Azure-only. | Higher cost at scale. | Fewer built-in integrations. |

**Narrative Analysis:**  
Durable Functions are developer-friendly for code-based orchestration. AWS Step Functions excel with visual design. GCP Workflows is light and straightforward but less feature-rich.

---

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
| --- | --- | --- |
| **Azure** | Service Bus | Fully managed enterprise messaging (queues & pub/sub). |
| **AWS** | Amazon SQS (queues) + SNS (topics) | SQS for FIFO/standard queues; SNS for pub/sub. |
| **GCP** | Pub/Sub | Global pub/sub messaging. |

**Comparison Table**

| Criteria | Azure Service Bus | AWS SQS + SNS | GCP Pub/Sub |
| --- | --- | --- | --- |
| **Core Features** | FIFO queues, topics, dead-letter queues, sessions. | SQS queues, SNS pub/sub, dead-letter queues. | Pub/sub, push & pull delivery, DLQs. |
| **Integration** | Azure Functions, Logic Apps. | Lambda, Step Functions. | Cloud Functions, Dataflow. |
| **Monitoring** | Azure Monitor, Metrics. | CloudWatch. | Cloud Monitoring. |
| **Pricing** | Per operation, message size, connection. | Pay-per-request. | Pay per message volume. |
| **Strengths** | Enterprise features (sessions, transactions). | High durability, simple scaling. | Global low-latency delivery. |
| **Weaknesses** | Azure-only. | SNS/SQS split model. | No FIFO support. |

---

## 5. Azure Event Grid

| Cloud Provider | Equivalent Service | Description |
| --- | --- | --- |
| **Azure** | Event Grid | Event routing for reactive architectures. |
| **AWS** | EventBridge | Event bus for routing events. |
| **GCP** | Eventarc | Event routing to GCP services. |

**Comparison Table**

| Criteria | Azure Event Grid | AWS EventBridge | GCP Eventarc |
| --- | --- | --- | --- |
| **Core Features** | Event filtering, fan-out, retries. | Event filtering, schema registry. | Event routing, filters. |
| **Integration** | Azure Functions, Logic Apps. | Lambda, Step Functions. | Cloud Run, Functions. |
| **Monitoring** | Azure Monitor. | CloudWatch. | Cloud Logging. |
| **Pricing** | Per million operations. | Per event published/ingested. | Per event delivered. |
| **Strengths** | Tight Azure integration. | SaaS/event source variety. | Strong GCP-native routing. |
| **Weaknesses** | Azure-focused. | Slightly more complex config. | Smaller event source list. |

---

## 6. Azure Event Hubs

| Cloud Provider | Equivalent Service | Description |
| --- | --- | --- |
| **Azure** | Event Hubs | Big data streaming ingestion. |
| **AWS** | Kinesis Data Streams | Scalable real-time streaming. |
| **GCP** | Pub/Sub | Large-scale event ingestion. |

**Comparison Table**

| Criteria | Azure Event Hubs | AWS Kinesis | GCP Pub/Sub |
| --- | --- | --- | --- |
| **Core Features** | High-throughput streaming, partitioned consumers. | Real-time data streams, shards. | Pub/sub messaging, global. |
| **Integration** | Stream Analytics, Functions. | Lambda, Firehose. | Dataflow, Functions. |
| **Monitoring** | Azure Monitor. | CloudWatch. | Cloud Monitoring. |
| **Pricing** | Throughput units/hour. | Per shard-hour + data transfer. | Per message volume. |
| **Strengths** | Deep Azure analytics integration. | Fine-grained scaling. | Global low-latency delivery. |
| **Weaknesses** | TU model can be costly. | Requires shard mgmt. | No ordering guarantee. |

---

## Conclusion

Azure provides strong service integration, making it easier to build fully managed serverless apps. AWS equivalents often split functionality across multiple services, offering more customization but more setup. GCP prioritizes simplicity and global reach but sometimes lacks niche features.

From a serverless perspective:  
- **Best integration & productivity** → Azure  
- **Best scalability & ecosystem** → AWS  
- **Best simplicity & global delivery** → GCP  

---
