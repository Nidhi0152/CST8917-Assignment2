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

## Reference

- [Serverless showdown: AWS Lambda vs Azure Functions vs Google Cloud Functions](https://www.pluralsight.com/resources/blog/cloud/serverless-showdown-aws-lambda-vs-azure-functions-vs-google-cloud-functions)
- 
