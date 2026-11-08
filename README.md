# Awesome-Workflow-Execution-Analytics-Metrics

# Awesome Workflow Execution Analytics & Metrics

> A curated list of top Workflow Execution Analytics and Metrics platforms — both SaaS/Hosted commercial solutions and open-source alternatives for monitoring, observability, and performance analysis of automated workflows and business processes.  
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [Postman Flows Analytics](#postman-flows-analytics)
  - [Datadog APM](#datadog-apm)
  - [New Relic Workflow Automation](#new-relic-workflow-automation)
  - [Dynatrace Workflows](#dynatrace-workflows)
  - [Grafana Cloud Workflows](#grafana-cloud-workflows)
  - [Mixpanel Flows](#mixpanel-flows)
  - [Segment](#segment)
  - [Honeycomb](#honeycomb)
  - [Coralogix](#coralogix)
- [Open-Source Software](#-open-source-software)
  - [Prometheus](#prometheus)
  - [Apache Airflow](#apache-airflow)
  - [SigNoz](#signoz)
  - [Temporal](#temporal)
  - [Prefect](#prefect)
  - [Jaeger](#jaeger)
  - [Argo Workflows](#argo-workflows)
  - [Dagster](#dagster)
  - [Flyte](#flyte)
  - [OpenTelemetry](#opentelemetry)
  - [OpenLineage](#openlineage)
  - [Domino](#domino)
  - [n8nTrace](#n8ntrace)
  - [Grafana n8n Dashboards](#grafana-n8n-dashboards)
- [Comparison at a Glance](#-comparison-at-a-glance)
- [Contributing](#-contributing)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted Workflow Execution Analytics and Metrics platforms. These are not open-source but are included as reference points for feature comparison.

### Postman Flows Analytics
**Type:** API workflow execution analytics  
Postman Flows provides an Analytics tab for monitoring deployed flows running in Postman Cloud. You can track when, how often, and how long actions run, with success/failure status for each block. Run logs allow drilling into individual blocks to view input, output, and detailed execution data. Time ranges are selectable (maximum three days), and runs can be filtered by run ID, flow name, status, and trigger type. The run ID is available from the response's `x-session-id` header [citation:1][citation:12].  
**Best for:** Teams building API-centric workflows in Postman wanting execution visibility without additional tooling.

### Datadog APM
**Type:** Application performance monitoring with trace pipeline  
Datadog APM collects traces from instrumented applications to provide end-to-end visibility into request flows across microservices. The Trace Pipeline allows customizable ingestion and retention of traces, with Processing Pipelines for transforming and enriching span attributes after ingestion. Custom metrics can be generated from spans for queries and comparisons. The Ingestion Control page provides volume overviews and configuration settings across services [citation:13]. Datadog also offers Synthetics for simulated user requests and Real User Monitoring for frontend performance analysis [citation:2].  
**Best for:** Organizations wanting comprehensive APM with customizable trace retention and metric generation from spans.

### New Relic Workflow Automation
**Type:** Workflow execution monitoring with events and logs  
New Relic Workflow Automation provides detailed execution metrics including total steps executed, failed run counts, and which steps failed. Run history lists all workflow executions with status and timestamps. Workflow runs emit `WorkflowAutomationEvent` data in NRDB with attributes including status (STARTED, COMPLETED, FAILED, TIMED_OUT, STOPPED), definition name, runId, duration, and step details. Logs are attributed with workflow name, version, runId, and entityGuid, with DEBUG and TRACE log levels capturing action inputs and outputs [citation:14]. Schedules support cron expressions with a minimum interval of 10 minutes [citation:3].  
**Best for:** Teams already using New Relic observability wanting workflow execution data in the same platform.

### Dynatrace Workflows
**Type:** Workflow execution tracking with detailed state  
Dynatrace Workflows tracks each execution as an individual entry with state (SUCCESS, RUNNING, ERROR, WAITING), trigger type (Manual, Schedule, Event), and runtime. The `IExecution` type provides properties including startedAt, endedAt, runtime, state, triggerType, and workflowType (STANDARD or SIMPLE). The Automation Utils SDK provides functions like `actionExecution()`, `execution()`, and `getExecutionLink()` for programmatic access to execution details, plus constants like `executionId` and `taskName` [citation:4]. Executions can be filtered by keyword, workflow name, state, trigger type, and timeframe [citation:15].  
**Best for:** Enterprises in the Dynatrace ecosystem needing programmatic access to workflow execution state.

### Grafana Cloud Workflows
**Type:** Workflow run observability (public preview)  
Grafana Cloud Workflows includes a Latest runs panel showing the 10 most recent runs of a workflow being edited. Each run displays status (Running, Success, Failed), start time, and step-level details including duration and inline inputs/outputs. Full step inputs and outputs can be viewed in a details dialog, with instance ID and execution ID available for API or support reference. The panel updates automatically as steps start and finish [citation:5].  
**Best for:** Teams using Grafana Cloud for observability wanting integrated workflow run visibility.

### Mixpanel Flows
**Type:** User journey and conversion flow analytics  
Mixpanel Flows analyzes user paths through product events, tracing forward and backward from anchor events. The query API supports configurable direction (forward/reverse steps, 0–5 range), per-step filters with AND/OR combinators, conversion windows (day, week, month, session), and count types (unique users, total events, unique sessions). Visualization modes include Sankey diagrams, ranked paths, and tree views. Results include a node DataFrame with step index, event name, and user counts [citation:6].  
**Best for:** Product teams analyzing user behavior flows and conversion paths rather than automated workflow execution.

### Segment
**Type:** Customer data pipeline with event tracking  
Segment's Analytics libraries (Identify, Track, Screen, Group, Alias) capture user actions as events with associated properties. The Track method records actions with human-readable event names and property dictionaries. The Flush utility forces queue flushing regardless of configured thresholds. While not a workflow analytics platform per se, Segment's event pipeline feeds downstream analytics tools that can analyze workflow-related user actions [citation:7].  
**Best for:** Teams wanting to pipe workflow-related user events into downstream analytics platforms.

### Honeycomb
**Type:** Observability with AI-assisted investigation  
Honeycomb provides distributed tracing and observability with features including BubbleUp Insights (automatically surfacing notable differences and potential root causes in query results) and Canvas (collaborative investigation workspace with AI agent assistance). The Canvas Slack App allows asking questions of Honeycomb data without leaving Slack. GitHub integration grounds investigations in actual code paths and recent commits [citation:8].  
**Best for:** Teams wanting AI-assisted root cause analysis of performance issues in distributed systems.

### Coralogix
**Type:** Observability with CI/CD workflow integration  
Coralogix provides a GitHub Action that exports telemetry from completed GitHub Actions workflows. Logs include task name, status, and severity. Traces represent each workflow as a separate trace with jobs as spans, enabling bottleneck identification via execution time visualization. Metrics include `github_workflow_failed_job_count_total`, `github_workflow_overall_job_count_total`, and `github_workflow_successful_job_count_total`, all with a service name label (repository name) for per-repository alerting [citation:9].  
**Best for:** Teams wanting CI/CD pipeline observability integrated with broader application monitoring.

---

## 🟩 Open-Source Software

Self-hosted, community-driven Workflow Execution Analytics, monitoring, and orchestration platforms. Sorted descending by GitHub Star count.

### [Prometheus](https://github.com/prometheus/prometheus) [![Stars](https://img.shields.io/github/stars/prometheus/prometheus?style=social&color=white)](https://github.com/prometheus/prometheus/stargazers)
**Stack:** Go | **License:** Apache 2.0  
The de facto standard for metrics collection and alerting in cloud-native environments. Prometheus can monitor workflow execution through custom metrics exported by workflow engines. Example alert rules from a Go workflow library demonstrate patterns for detecting high error rates (`rate(workflow_process_error_count[5m]) > 0.1`), consumer lag (`workflow_process_lag_alert == 1`), process down states (`workflow_process_states == 0`), high skip rates, slow processing (95th percentile latency), and low completion rates [citation:10]. Workflow engines like Argo Workflows expose Prometheus metrics on port 9090 by default [citation:20].  
**Best for:** Teams wanting a standard, battle-tested metrics foundation for workflow alerting and dashboards.

### [Apache Airflow](https://github.com/apache/airflow) [![Stars](https://img.shields.io/github/stars/apache/airflow?style=social&color=white)](https://github.com/apache/airflow/stargazers)
**Stack:** Python | **License:** Apache 2.0  
Industry-leading open-source workflow orchestration platform with rich built-in execution analytics and observability. Airflow provides comprehensive run history, task duration charts, landing times, Gantt views, execution status breakdowns, and native OpenTelemetry/StatsD metrics export for pipeline monitoring and alerting across large-scale data engineering workflows.  
**Best for:** Teams requiring complex, programmatic DAG scheduling with built-in execution history, task latency graphs, and SLA monitoring.

### [SigNoz](https://github.com/signoz/signoz) [![Stars](https://img.shields.io/github/stars/signoz/signoz?style=social&color=white)](https://github.com/signoz/signoz/stargazers)
**Stack:** Go / TypeScript / ClickHouse | **License:** Open Source  
An open-source, OpenTelemetry-native APM and observability platform that acts as an alternative to Datadog. SigNoz provides unified monitoring for traces, metrics, and logs with ClickHouse-powered analytics, making it ideal for deep execution tracing, step duration breakdown, and bottleneck identification across distributed workflows.  
**Best for:** Teams seeking a self-hosted, Datadog-like observability suite built natively on OpenTelemetry to trace workflow steps and job durations.

### [Temporal](https://github.com/temporalio/temporal) [![Stars](https://img.shields.io/github/stars/temporalio/temporal?style=social&color=white)](https://github.com/temporalio/temporal/stargazers)
**Stack:** Go | **License:** MIT  
A resilient workflow execution platform for building durable microservices and distributed orchestrations. Temporal tracks complete workflow history, state transitions, retry attempts, timeout events, and activity execution latencies, exposing detailed SDK and server metrics via Prometheus for end-to-end execution reliability analytics.  
**Best for:** Developers building mission-critical code-as-workflow systems requiring event history replay, failure analytics, and execution state guarantees.

### [Prefect](https://github.com/prefecthq/prefect) [![Stars](https://img.shields.io/github/stars/prefecthq/prefect?style=social&color=white)](https://github.com/prefecthq/prefect/stargazers)
**Stack:** Python | **License:** Apache 2.0  
Modern open-source orchestration and workflow intelligence engine designed for Python developers. Features an interactive dashboard for flow run history, real-time state tracking, task concurrency metrics, failure root-cause analysis, and automated event-driven alerts for modern data and ML pipelines.  
**Best for:** Python-first teams wanting modern workflow execution observability, task-level telemetry, and automated notifications.

### [Jaeger](https://github.com/jaegertracing/jaeger) [![Stars](https://img.shields.io/github/stars/jaegertracing/jaeger?style=social&color=white)](https://github.com/jaegertracing/jaeger/stargazers)
**Stack:** Go | **License:** Apache 2.0  
CNCF graduated open-source distributed tracing platform. Jaeger enables end-to-end distributed tracing across complex workflow pipelines and microservices, allowing teams to visualize workflow DAG dependencies as trace timelines, isolate bottleneck tasks, and analyze latency distributions.  
**Best for:** Visualizing individual workflow execution timelines, span latencies, and service dependencies in distributed setups.

### [Argo Workflows](https://github.com/argoproj/argo-workflows) [![Stars](https://img.shields.io/github/stars/argoproj/argo-workflows?style=social&color=white)](https://github.com/argoproj/argo-workflows/stargazers)
**Stack:** Go / Kubernetes | **License:** Apache 2.0  
Kubernetes-native container workflow engine for parallel jobs, CI/CD, and machine learning pipelines. Provides real-time DAG and step visualization, pod-level execution logs, historical duration metrics, and native Prometheus metrics export on port 9090 for cluster-wide workflow monitoring [citation:20].  
**Best for:** Kubernetes-native teams running containerized compute pipelines requiring real-time DAG execution tracking and Prometheus metrics.

### [Dagster](https://github.com/dagster-io/dagster) [![Stars](https://img.shields.io/github/stars/dagster-io/dagster?style=social&color=white)](https://github.com/dagster-io/dagster/stargazers)
**Stack:** Python / TypeScript | **License:** Apache 2.0  
Cloud-native data orchestrator and asset management platform centered on data assets. Dagster UI provides rich execution analytics including run timelines, asset materialization history, compute duration comparisons, data lineage tracking, and automated error diagnostics.  
**Best for:** Data platform teams managing asset-centric pipelines needing deep execution telemetry and data lineage analytics.

### [Flyte](https://github.com/flyteorg/flyte) [![Stars](https://img.shields.io/github/stars/flyteorg/flyte?style=social&color=white)](https://github.com/flyteorg/flyte/stargazers)
**Stack:** Python / Go / Kubernetes | **License:** Apache 2.0  
Production-grade, type-safe workflow orchestrator for machine learning, data engineering, and AI pipelines. Offers detailed execution tracking, node-level runtime profiling, artifact caching analytics, reproducible execution logs, and Prometheus metrics out of the box.  
**Best for:** Machine learning and AI workflows requiring typed task inputs/outputs, step-level duration profiling, and execution lineage.

### [OpenTelemetry](https://github.com/open-telemetry/opentelemetry-collector) [![Stars](https://img.shields.io/github/stars/open-telemetry/opentelemetry-collector?style=social&color=white)](https://github.com/open-telemetry/opentelemetry-collector/stargazers)
**Stack:** Multiple (language SDKs) / Go | **License:** Apache 2.0  
A vendor-neutral observability framework for generating, collecting, and exporting telemetry data (traces, metrics, logs). Workflow engines and applications can instrument with OpenTelemetry SDKs and use the OpenTelemetry Collector to emit standardized telemetry that integrates with any compatible backend (Prometheus, Jaeger, SigNoz, Grafana Tempo, Datadog, etc.) [citation:9].  
**Best for:** Teams wanting vendor-neutral instrumentation that can feed any observability backend.

### [OpenLineage](https://github.com/OpenLineage/OpenLineage) [![Stars](https://img.shields.io/github/stars/OpenLineage/OpenLineage?style=social&color=white)](https://github.com/OpenLineage/OpenLineage/stargazers)
**Stack:** Java / Python | **License:** Apache 2.0  
An open standard and framework for lineage and operational metadata collection from workflow orchestrators (Airflow, Spark, Dagster, Flink). OpenLineage captures runtime execution events (START, COMPLETE, FAIL), task run durations, input/output dataset states, and job dependencies for end-to-end data pipeline governance and analytics.  
**Best for:** Organizations tracking cross-system workflow execution lineage, dataset changes, and pipeline health metadata.

### [Domino](https://github.com/Tauffer-Consulting/domino) [![Stars](https://img.shields.io/github/stars/Tauffer-Consulting/domino?style=social&color=white)](https://github.com/Tauffer-Consulting/domino/stargazers)
**Stack:** Python / React / Apache Airflow | **License:** Apache 2.0  
An open-source workflow creation and monitoring platform providing a visual drag-and-drop GUI on top of Apache Airflow. Modular components (called Pieces) execute in isolated Docker containers, mapping directly to Airflow tasks. The monitoring view offers real-time execution tracking, status updates, run logs, and task outputs [citation:21].  
**Best for:** Teams wanting a visual workflow builder with real-time execution monitoring powered by Airflow.

### [n8nTrace](https://github.com/Mohammedaljer/n8nTrace) [![Stars](https://img.shields.io/github/stars/Mohammedaljer/n8nTrace?style=social&color=white)](https://github.com/Mohammedaljer/n8nTrace/stargazers)
**Stack:** Docker / PostgreSQL | **License:** MIT  
A self-hosted observability dashboard for n8n workflows designed to provide visibility without exposing sensitive workflow data. A lightweight collector gathers execution metadata (status, duration, workflow ID, instance ID) and stores it in PostgreSQL. Features include execution analytics (success/failure rates, duration trends), instance health monitoring, Prometheus-style metrics explorer, RBAC, and audit logging [citation:22].  
**Best for:** n8n users needing workflow performance visibility for business teams without exposing sensitive data.

### [Grafana n8n Dashboards](https://github.com/nluecke/grafana-n8n-dashboards) [![Stars](https://img.shields.io/github/stars/nluecke/grafana-n8n-dashboards?style=social&color=white)](https://github.com/nluecke/grafana-n8n-dashboards/stargazers)
**Stack:** Grafana / PostgreSQL | **License:** Open Source  
A collection of Grafana dashboards (including Dashboard ID: 24475) for analyzing n8n workflow and execution performance using the PostgreSQL database backend. Provides executive summary metrics (total workflows, active workflows, executions in range, success rate, failed executions), execution performance trends (executions over time by status, P50/P95/P99 duration), workflow quality insights, and queue metrics [citation:16].  
**Best for:** Teams already using Grafana wanting a ready-made n8n workflow analytics dashboard.

---

## 📊 Comparison at a Glance

| Software | License | Focus | Workflow Engine Support | Self-Hosted | Best For |
|----------|---------|-------|------------------------|-------------|----------|
| **Postman Flows** | Proprietary | API workflow analytics | Postman Flows | ❌ | API-centric workflows |
| **Datadog APM** | Proprietary | Trace pipeline | Any (instrumented) | ❌ | Full APM + custom metrics |
| **New Relic** | Proprietary | Workflow events | New Relic Workflows | ❌ | New Relic ecosystem |
| **Dynatrace** | Proprietary | Execution state | Dynatrace Workflows | ❌ | Programmatic state access |
| **Grafana Cloud** | Proprietary | Run panel | Grafana Workflows | ❌ | Grafana Cloud users |
| **Mixpanel Flows** | Proprietary | User journey | (Product events) | ❌ | Conversion path analysis |
| **Segment** | Proprietary | Event pipeline | Any (downstream analytics) | ❌ | Workflow-related user event routing |
| **Honeycomb** | Proprietary | AI observability | Any (distributed tracing) | ❌ | AI root cause analysis of system latencies |
| **Coralogix** | Proprietary | CI/CD telemetry | GitHub Actions | ❌ | CI/CD pipeline observability |
| **Prometheus** | Apache 2.0 | Metrics + alerting | Any (exporters) | ✅ | Standard metrics foundation |
| **Apache Airflow** | Apache 2.0 | Workflow orchestration + analytics | Apache Airflow | ✅ | Programmatic DAGs + execution charts |
| **SigNoz** | Open Source | OpenTelemetry APM | Any (OTel instrumented) | ✅ | Self-hosted APM & trace analytics |
| **Temporal** | MIT | Durable execution + metrics | Temporal Workflows | ✅ | Microservice state & execution history |
| **Prefect** | Apache 2.0 | Workflow orchestration + observability | Prefect Flows | ✅ | Python-first workflow execution UI |
| **Jaeger** | Apache 2.0 | Distributed tracing | Any (OpenTelemetry / Jaeger) | ✅ | Distributed workflow step tracing |
| **Argo Workflows** | Apache 2.0 | Kubernetes container workflows | Kubernetes / Argo | ✅ | Container DAG execution tracking |
| **Dagster** | Apache 2.0 | Asset orchestration + analytics | Dagster Pipelines | ✅ | Asset-centric pipeline telemetry |
| **Flyte** | Apache 2.0 | AI/ML pipeline orchestration | Kubernetes / Flyte | ✅ | Typed task profiling & execution lineage |
| **OpenTelemetry** | Apache 2.0 | Vendor-neutral telemetry | Any (instrumented) | ✅ (SDK / Collector) | Standardized instrumentation |
| **OpenLineage** | Apache 2.0 | Data pipeline lineage & metadata | Airflow, Spark, Dagster, Flink | ✅ | Cross-engine lineage & execution metadata |
| **Domino** | Apache 2.0 | Visual workflow + monitoring | Apache Airflow | ✅ | Visual builder + real-time status |
| **n8nTrace** | MIT | n8n observability dashboard | n8n | ✅ | n8n metadata-only visibility |
| **Grafana n8n Dashboards** | Open Source | PostgreSQL analytics dashboard | n8n (PostgreSQL) | ✅ | Ready-made n8n dashboard |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source Workflow Execution Analytics or Metrics tool that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source. Note that dedicated open-source workflow analytics platforms are still emerging; many available tools are extensions for specific workflow engines (Airflow, n8n) or general-purpose observability infrastructure (Prometheus, OpenTelemetry).

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐
