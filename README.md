# Awesome-Systems-Monitoring-Alerting

# Top Systems Monitoring & Alerting Tools Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Metrics Collection, Alert Routing & Long-Term Storage*  
**Last updated: March 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Systems Monitoring & Alerting**. These tools collect metrics from infrastructure and applications, evaluate alert rules, route notifications, and store time-series data for long-term analysis and capacity planning.

**Examples** include Datadog, New Relic, Dynatrace, AppDynamics, Splunk, Elastic Observability, LogicMonitor, Sumo Logic, SolarWinds, and Grafana Cloud (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, long-term storage, and transparent alerting — ideal for SREs prioritizing data sovereignty, developers building observability pipelines, and organizations avoiding per-host SaaS pricing.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[Datadog](https://www.datadoghq.com/)**  
  Unified monitoring and analytics platform with infrastructure monitoring, APM, logs, and synthetics. Pricing is **per-host with annual commitments** — the UX and ecosystem lead the managed SaaS category, but the bill grows linearly with fleet size .

- **[New Relic](https://newrelic.com/)**  
  Full-stack observability with **ingest-based pricing** rather than per-host. High host count with manageable data volumes tends to favor New Relic's pricing structure over Datadog's per-host model .

- **[Dynatrace](https://www.dynatrace.com/)**  
  AI-powered observability with automatic discovery, distributed tracing, and Davis AI for root-cause analysis. Enterprise-focused with premium pricing.

- **[Splunk Observability Cloud](https://www.splunk.com/)**  
  Metrics, traces, and logs with real-time alerting and AI-driven anomaly detection within the Splunk ecosystem.

- **[Elastic Observability](https://www.elastic.co/observability)**  
  Logs, metrics, and APM built on the Elastic Stack. **Elasticsearch 9.5** (August 2026) added **Prometheus remote write v1 and native PromQL**, with ~80% of real-world queries running unmodified — a significant step for teams already using Elasticsearch .

- **[LogicMonitor](https://www.logicmonitor.com/)**  
  Automated infrastructure monitoring with AIOps capabilities for hybrid cloud environments.

- **[Sumo Logic](https://www.sumologic.com/)**  
  Cloud-native log analytics and observability with security analytics integration.

- **[SolarWinds](https://www.solarwinds.com/)**  
  Infrastructure monitoring and network management for on-premises and hybrid environments.

- **[Grafana Cloud](https://grafana.com/)**  
  Managed observability platform running **Grafana Mimir** under the hood. The choice for teams committed to the open-source ecosystem who want a managed option keeping data in a familiar format .

## Open-Source GitHub Projects

- **[Prometheus](https://github.com/prometheus/prometheus)**  
  **The de facto standard for metrics collection and alerting.** Pull-based scraping, PromQL query language, and Alertmanager for routing. A single-node Prometheus handles most small-to-medium deployments. **The ecosystem's real strength is its exporters** — standard integrations for Linux (`node_exporter`, port 9100), MySQL (`mysqld_exporter`, port 9104), PostgreSQL (`postgres_exporter`, port 9187), Redis (`redis_exporter`, port 9121), Nginx (port 9113), Kafka (port 9308), and 30+ more components .

- **[Thanos](https://github.com/thanos-io/thanos)**  
  **The safest choice for existing Prometheus fleets needing long-term storage.** Uses a **sidecar pattern** — no change to Prometheus's scrape or write path. Uploads TSDB blocks to S3-compatible object storage, provides global query view across multiple Prometheus instances, and deduplicates HA pairs . **Trade-off**: more components to operate (Sidecar, Store, Compactor, Query, Query Frontend) .

- **[Grafana Mimir](https://github.com/grafana/mimir)**  
  **Built for multi-tenant scale** — thousands of active series per tenant, SaaS-scale deployments. Successor to Cortex, which is effectively **superseded** — new development activity is minimal and core maintainers migrated to Mimir . **Mimir v3.0** (November 2025) is a meaningful improvement . Requires a dedicated platform engineering team .

- **[VictoriaMetrics](https://github.com/VictoriaMetrics/VictoriaMetrics)**  
  **The simplicity and storage-efficiency champion.** Single small executable with no external dependencies. Uses **10x less RAM than InfluxDB** for millions of unique series, with up to **70x better compression than TimescaleDB** . **MetricsQL** is a PromQL superset. Single-node VictoriaMetrics can substitute for moderately sized Thanos/Mimir clusters . **Best for teams prioritizing operational simplicity and not requiring SQL analytics on metrics** .

- **[Alertmanager](https://github.com/prometheus/alertmanager)**  
  **The standard alert routing layer for Prometheus.** Deduplicates, groups, and routes alerts to receivers including Slack, PagerDuty, email, and webhooks. Silences, inhibition rules, and high-availability clustering.

- **[Grafana](https://github.com/grafana/grafana)**  
  **The visualization layer that ties everything together.** Connects to Prometheus, Thanos, Mimir, VictoriaMetrics, and 100+ other data sources. Dashboard templating, alerting, and annotation.

- **[OpenTelemetry Collector](https://github.com/open-telemetry/opentelemetry-collector)**  
  **Vendor-agnostic telemetry pipeline** for receiving, processing, and exporting metrics, traces, and logs . **Removes the need for multiple agents** — one collector can scrape Prometheus endpoints, receive OTLP, and export to any backend . The standard way to **decouple instrumentation from backends** and support migration without re-instrumenting .

- **[Upright](https://github.com/basecamp/upright)**  
  **37signals' open-source synthetic monitoring system** built on the open-source observability stack. **Playwright probes** run real browser flows with video recording on failure. **Multi-site architecture** distinguishes regional blips from real outages — if one site in Amsterdam fails but four others succeed, it's regional . Runs across **5 global sites for ~$110/month** using cheap VPS nodes .

- **[SigNoz](https://github.com/SigNoz/signoz)**  
  **OpenTelemetry-native observability platform** with logs, traces, and metrics in one application. Built on ClickHouse. The open-source alternative to Datadog and New Relic for teams going **all-in on OpenTelemetry from a greenfield start** .

- **[Coroot](https://github.com/coroot/coroot)**  
  **eBPF-powered APM** — DataDog and New Relic alternative with rapid insights into system performance. No code changes required for instrumentation .

- **[Statuz](https://github.com/statuzlabs/statuz)**  
  **Self-hosted status and incident management** for everything that matters. Lightweight Go backend, HTTP/TCP checks, persistent incident tracking, and planned maintenance. Single static binary with SQLite or Postgres .

- **[OpenStatus](https://github.com/openstatusHQ/openstatus)**  
  **Open-source synthetic monitoring and status page platform** with global monitoring, **monitoring-as-code via YAML**, and CI/CD integration. Customizable public/private status pages .

### Additional Strong Open-Source Options

- **Blackbox Exporter** — Probing HTTP/HTTPS, DNS, TCP, and ICMP endpoints. Port 9115 .
- **Node Exporter** — Hardware and OS metrics for Linux/Unix. Port 9100 .
- **Cortex** — Still Apache 2.0 and functional (v1.21 shipped April 2026 with Parquet mode), but new development is minimal. **Mimir is the successor** .
- **ClickHouse TimeSeries** — New table engine with Prometheus remote write/read and **PromQL dialect covering 85%+ of the language** (private preview as of ClickHouse 26.9) .
- **Arc** — SQL-native time-series database storing Parquet on S3. **Not a Prometheus replacement** — no remote write, no PromQL. For teams whose metrics need to join with application data via SQL .

**Frameworks for building custom systems**: Combine **Prometheus** for scraping and alert evaluation, **Thanos** or **VictoriaMetrics** for long-term storage depending on whether you prioritize migration safety or operational simplicity, **Alertmanager** for routing, **Grafana** for visualization, and **OpenTelemetry Collector** for vendor-neutral ingestion — to build a complete self-hosted monitoring stack that scales from a single node to multi-region fleets .

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Systems monitoring tools differ significantly in scale ceiling, operational complexity, and storage philosophy. **Thanos, Mimir, and VictoriaMetrics solve different problems** — Thanos for existing Prometheus fleets, Mimir for multi-tenant scale, VictoriaMetrics for simplicity . **Cortex is superseded by Mimir** — new development is minimal . **Alert fatigue is a real operational risk** — thresholds require empirical tuning against actual baseline behavior, and multi-site probing reduces false positives from regional network blips .
- Self-hosted open-source solutions require proper storage planning (object storage for Thanos/Mimir, disk for VictoriaMetrics), backup strategies, and ongoing maintenance of exporters and collector configurations.

---

**Made for SREs, platform engineers, DevOps teams, and developers building reliable infrastructure.**  
Let's make systems monitoring more open, scalable, and alert-fatigue resistant.
