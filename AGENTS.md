# Copilot instructions for NetApp Workload Factory for EDA documentation

## Repository overview

Product: NetApp Workload Factory for EDA

NetApp Workload Factory for EDA manages Amazon FSx for NetApp ONTAP file systems used for electronic design automation (EDA) workloads. This documentation covers storage monitoring, volume latency analysis, and Perforce Helix Core integration for CI/CD.

## Repository structure

- `_whatsnew/` – Dated release-note entries included by whats-new.adoc
- `_include/` – Reusable content snippets (currently empty but reserved for future use)
- `store-redirects/` – Redirect pages for deprecated URLs (for example, when "Builders" was renamed to "EDA")
- `media/` – Images and screenshots for documentation

## Product-specific context

- **FSx for ONTAP terminology:** Use "FSx for ONTAP file system," not "FSx cluster" or "ONTAP cluster," for the managed service; in monitoring contexts, "cluster" may refer to the FSx file system itself.
- **EDA vs. Builders:** The product was formerly "Workload Factory for Builders" and was renamed to "Workload Factory for EDA" in January 2026; use "EDA" in all new content.
- **Latency analysis:** Basic analysis uses ONTAP QoS delay center metrics; AI-agent analysis requires Amazon Bedrock and provides deeper insight for data and cluster latency.
- **Tabbed analysis panel:** A latency event opens a panel with Overview (basic analysis) and Over time (interactive graph) tabs.
- **Notification behavior:** Latency notifications are sent per file system, group all affected volumes in one alert, and show at most 10 volumes in email.
- **Links requirement:** Latency, IOPS, and throughput graphs require AWS credentials; FSx for ONTAP links are required for component breakdown and AI analysis; events can be detected from SNS notifications without credentials or links.
- **Permission modes:** Latency monitoring requires read/write permissions; basic and read-only modes are not supported.
- **CloudWatch vs. ONTAP data:** Latency graphs use CloudWatch data and basic analysis uses ONTAP QoS data, so slight discrepancies are expected.

## Typical user workflows

- **Set up latency monitoring:** add AWS credentials → configure read/write thresholds → view events → analyze trends
- **Investigate a latency event:** select the event → review basic analysis → optionally run AI analysis → view the over-time graph → check historical breaches → remediate
- **Configure dashboards:** enable the Overview dashboard → configure the Project dashboard with AWS tag filters → monitor capacity, throughput, and IOPS
- **Perforce CI/CD:** create a project → associate an FSx volume → create snapshots → clone workspaces → integrate the P4V client → manage versions
