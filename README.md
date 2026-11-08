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
  - [Granyt](#granyt)
  - [n8n-trace](#n8n-trace)
  - [Grafana n8n Dashboard](#grafana-n8n-dashboard)
  - [OpenTelemetry](#opentelemetry)
  - [Starflow](#starflow)
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

Self-hosted, community-driven Workflow Execution Analytics tools. The open-source ecosystem for dedicated workflow analytics is emerging; many tools are extensions for specific workflow engines.

### Prometheus
**Stack:** Go | **License:** Apache 2.0  
The de facto standard for metrics collection and alerting in cloud-native environments. Prometheus can monitor workflow execution through custom metrics exported by workflow engines. Example alert rules from a Go workflow library demonstrate patterns for detecting high error rates (`rate(workflow_process_error_count[5m]) > 0.1`), consumer lag (`workflow_process_lag_alert == 1`), process down states (`workflow_process_states == 0`), high skip rates, slow processing (95th percentile latency), and low completion rates [citation:10]. Workflow engines like Argo Workflows expose Prometheus metrics on port 9090 by default [citation:20].  
**Best for:** Teams wanting a standard, battle-tested metrics foundation for workflow alerting and dashboards.

### Granyt
**Stack:** Python / Next.js / PostgreSQL | **License:** MIT  
An open-source observability platform built specifically for Apache Airflow. The `granyt-sdk` installs as a lightweight listener that automatically captures DAG and task execution events without code changes. Features include automatic lineage tracking via OpenLineage, Sentry-like error capture with full stack traces and DAG context, operator adapters for Snowflake, BigQuery, dbt, S3, and others that extract rich metrics (row counts, bytes processed, query IDs), and custom DataFrame metrics from Pandas/Polars. Self-hosted via Docker Compose with PostgreSQL. No credit card or sales call required [citation:18][citation:23].  
**Best for:** Airflow teams wanting purpose-built, self-hosted observability without enterprise observability platform costs.

### n8n-trace
**Stack:** Docker / PostgreSQL | **License:** Open Source (per community post)  
A self-hosted observability dashboard for n8n workflows designed to provide visibility without exposing sensitive workflow data. A lightweight n8n workflow collects execution metadata (status, duration, workflow ID, instance ID) and writes it to a dedicated PostgreSQL database. Only operational metadata is stored — no payloads or secrets. Features include workflow execution analytics (success/failure rates, duration trends), instance health monitoring, Prometheus-style metrics explorer, multi-instance support, role-based access control scoped by instance/workflow ID/tag, and audit logging. Runs as a single Docker container alongside PostgreSQL [citation:22].  
**Best for:** n8n users needing workflow performance visibility for business teams without exposing sensitive data.

### Grafana n8n Dashboard
**Stack:** Grafana / PostgreSQL | **License:** Open Source (per Grafana dashboard)  
A Grafana dashboard (ID: 24475) for analyzing n8n workflow and execution performance using the PostgreSQL database backend. Provides executive summary metrics (total workflows, active workflows, executions in range, success rate, failed executions, running executions), execution performance trends (executions over time by status, P50/P95/P99 duration), workflow quality insights (most executed, daily success rate trend, most failures, slowest workflows), and resource/queue management (queue depth, long-running executions, recent errors). Requires Grafana ≥9, n8n with PostgreSQL, and PostgreSQL ≥12 [citation:16].  
**Best for:** Teams already using Grafana wanting a ready-made n8n workflow analytics dashboard.

### OpenTelemetry
**Stack:** Multiple (language SDKs) | **License:** Apache 2.0  
A vendor-neutral observability framework for generating, collecting, and exporting telemetry data (traces, metrics, logs). Workflow engines and applications can instrument with OpenTelemetry SDKs to emit standardized telemetry that integrates with any compatible backend (Prometheus, Jaeger, Grafana Tempo, Datadog, etc.). Coralogix's GitHub Action uses the OpenTelemetry endpoint for exporting workflow telemetry [citation:9].  
**Best for:** Teams wanting vendor-neutral instrumentation that can feed any observability backend.

### Starflow
**Stack:** Python / React / Apache Airflow | **License:** Open Source (per PyPI)  
An open-source workflow management platform with a GUI for creating, editing, and monitoring workflows. Every Starflow workflow corresponds to an Apache Airflow DAG, and each Piece corresponds to an Airflow task. The monitoring page shows real-time status of each workflow Piece, including logs and results of each run. Workflows can be scheduled periodically, at specific times, or triggered manually. Pieces run in isolated Docker containers and are versioned, tested, and documented. Scalable and Kubernetes-native [citation:21].  
**Best for:** Teams wanting a visual workflow builder with real-time execution monitoring powered by Airflow.

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
| **Coralogix** | Proprietary | CI/CD telemetry | GitHub Actions | ❌ | CI/CD pipeline observability |
| **Prometheus** | Apache 2.0 | Metrics + alerting | Any (exporters) | ✅ | Standard metrics foundation |
| **Granyt** | MIT | Airflow observability | Apache Airflow | ✅ | Airflow-specific OSS |
| **n8n-trace** | Open Source | n8n observability | n8n | ✅ | n8n metadata-only visibility |
| **Grafana n8n** | Open Source | Dashboard | n8n (PostgreSQL) | ✅ | Ready-made n8n dashboard |
| **OpenTelemetry** | Apache 2.0 | Vendor-neutral telemetry | Any (instrumented) | ✅ (SDK) | Standardized instrumentation |
| **Starflow** | Open Source | Visual workflow + monitoring | Apache Airflow | ✅ | Visual builder + real-time status |

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
