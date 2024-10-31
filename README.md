# Prometheus-and-Grafana-Learning Repo

This repo is maintained by [Devops with Mike](https://www.youtube.com/@DevOpsWithMike0/videos/)

For Cloud and DevOps interview preparation, use this platform [Wandaprep](http://www.wandaprep.com/)

# Monitoring and Observability in DevOps
Monitoring and observability are key concepts in DevOps, enabling teams to track the health, performance, and behavior of applications, infrastructure, and services. They help with early detection of issues, performance bottlenecks, and support proactive system maintenance.

- **Monitoring**: Focuses on collecting and analyzing metrics, logs, and traces from various systems to understand the system’s current state.
- **Observability**: Encompasses monitoring but also dives deeper into understanding why the system behaves a certain way, based on insights gathered from telemetry data like logs, traces, and metrics.

## What is Prometheus?
Prometheus is an open-source monitoring and alerting toolkit designed to record and process real-time metrics in a time-series format. It’s widely used for monitoring services and applications in cloud-native and microservices-based environments.

### Key Features of Prometheus:

* Built-in `time-series database` (TSDB).
* A pull-based metric collection mechanism.
* Alerting with rules and integrations.
* Querying language (`PromQL`) for querying metrics data.
* Highly scalable and can scrape thousands of metrics per second.

### Prometheus Pull Mechanism
Prometheus uses a pull-based model to gather metrics data. Instead of receiving data pushed from applications, Prometheus pulls metrics by sending requests to designated endpoints (known as exporters or targets). Each application or service exposes its metrics on a URL endpoint (usually /metrics), and Prometheus scrapes this endpoint at specified intervals.

**Advantages of the Pull Model**:
* Allows fine-grained control over which metrics are collected.
* Can handle auto-discovery in dynamic environments (e.g., Kubernetes).
* Simplifies alerting and fault detection, as Prometheus can detect if a target becomes unavailable.

## Prometheus Architecture

![Prometheus Architecture](https://samirbehara.com/wp-content/uploads/2019/05/prometheus-architecture.png)

The architecture of Prometheus is modular and includes several key components:

1.  **Prometheus Server**:
- Core component that scrapes and stores metrics from configured targets.
- Runs the time-series database to store data locally.

2. **Time-Series Database (TSDB)**:
- Specialized database optimized for handling time-stamped data.
- Stores data with high compression to save space and increase efficiency.

3. **Prometheus Query Language (PromQL)**:
- Language used for querying metrics data from Prometheus.
- Allows for complex aggregations, filters, and transformations on collected data.

4. **Alertmanager**:
- Receives alerts from Prometheus, processes them based on user-defined rules, and sends notifications to external services (e.g., Slack, email).
- Supports `alert deduplication`, `grouping`, and `inhibition`.

5. **Exporters**:
- Components that expose metrics in a format Prometheus understands (e.g., Node Exporter for system metrics, MySQL Exporter for MySQL metrics).
- Custom exporters can be created to monitor application-specific metrics.

6. **Pushgateway (Optional)**:
- Used for short-lived jobs or batch processes that can’t be scraped by Prometheus.
- Allows metrics to be temporarily stored and later retrieved by Prometheus.

## Main Components in Prometheus Setup

![Detailed Prometheus Setup](https://chronosphere.io/wp-content/uploads/2023/11/Prometheus-Architecture-1.png)

1. **Data Collection (Scraping Targets)**: Prometheus scrapes data from targets at regular intervals.
2. **Storage**: Time-series data is stored in the Prometheus TSDB.
3. **Querying and Alerts**:
    - PromQL is used to query stored metrics.
    - Alertmanager processes and routes alerts based on configured rules.
4. **Exporters and Instrumentation**:
    - Exporters expose metrics for applications.
    - Applications can also be instrumented to expose custom metrics.

## What is Visualization?
**Visualization** is the practice of representing metrics data in a graphical form, such as charts, dashboards, and graphs. Visualization tools like Grafana help transform raw data into easily understandable insights, assisting teams in monitoring trends, spotting anomalies, and troubleshooting effectively.

## What is Grafana?
Grafana is an open-source platform for data visualization, monitoring, and alerting. It provides customizable dashboards that allow DevOps and SRE teams to visualize metrics data from a variety of sources, including Prometheus. Grafana supports multiple data sources and allows complex querying, data transformations, and rich visualizations.

### Key Features of Grafana
1. **Custom Dashboards**: Allows users to create highly customized dashboards using panels and visualizations.

![Dashboard for Node-exporter](https://grafana.com/grafana/dashboards/11074-node-exporter-for-prometheus-dashboard-en-v20201010/)

2. **Alerting**: Integrated alerting with notifications.
Multi-source Compatibility: Connects to various data sources such as Prometheus, Elasticsearch, Graphite, and many more.

3. **Plugins**: Extensible with plugins for different visualizations, data sources, and integrations.

## Data Sources in Grafana
Data Sources in Grafana are services that provide data to Grafana for visualization. Each data source has unique query capabilities, but Grafana abstracts the details, enabling seamless use within dashboards.
- **Prometheus**: Most popular for time-series data from monitoring systems.
- **Elasticsearch**: Commonly used for log aggregation and analysis.
- **Graphite**: An older but popular time-series data source.
- **MySQL/PostgreSQL**: Used for relational database metrics.
- **Cloud Monitoring**: AWS CloudWatch, Google Cloud Monitoring, and Azure Monitor support.

## Prometheus and Grafana in an End-to-End DevOps Pipeline
Prometheus and Grafana, when integrated, provide powerful monitoring and observability capabilities for a DevOps pipeline, allowing teams to achieve better system reliability and faster issue resolution. Here’s an overview of how these tools fit into an end-to-end DevOps pipeline:

1. **Instrumentation**: Applications and infrastructure components are instrumented to expose metrics, which are either collected directly by Prometheus or exposed via exporters.

2. **Data Collection with Prometheus**:
    - Prometheus collects metrics data by scraping configured targets at regular intervals.
    - Metrics are stored in Prometheus’s time-series database and queried using PromQL for insights.

3. **Alerting**:    
    - Prometheus evaluates alerting rules, and alerts are routed to the Alertmanager.
    - Alertmanager handles deduplication, grouping, and notification routing.

4. **Data Visualization with Grafana**:
    - Grafana connects to Prometheus as a data source to query and visualize metrics data.
    - Custom dashboards in Grafana help DevOps teams view critical metrics, monitor SLIs (Service Level Indicators), and track the health of services.
    - Grafana also supports alerting based on data queries.
5. **Automated Incident Response**:
    - Alerts can trigger automated responses, like running scripts or adjusting resources, for self-healing.
    - Teams receive alerts through integrations with tools like Slack, PagerDuty, or email.
6. **Continuous Improvement**:
    - Collected metrics and insights help teams identify areas for improvement.
    - Trends and patterns in Grafana dashboards aid in retrospective analysis, identifying potential bottlenecks or failures in the pipeline.