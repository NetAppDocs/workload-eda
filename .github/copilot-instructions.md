# Copilot instructions for NetApp Workload Factory for EDA documentation

## Repository overview

Product: NetApp Workload Factory for EDA

NetApp Workload Factory for EDA helps customers optimize Amazon FSx for NetApp ONTAP file systems for electronic design automation (EDA) workloads. It provides dashboards for monitoring storage health and performance, latency analysis with AI-powered insights, and integration with Perforce Helix Core for CI/CD workflows.

## Repository structure

- `_whatsnew/` – Individual release note files included by whats-new.adoc
- `_include/` – Reusable content snippets (currently empty but reserved for future use)
- `store-redirects/` – Redirect pages for deprecated URLs (e.g., when "Builders" was renamed to "EDA")
- `media/` – Images and screenshots for documentation

## Product-specific context

- **FSx for ONTAP terminology:** Use "FSx for ONTAP file system" not "FSx cluster" or "ONTAP cluster" when referring to the managed service. In monitoring contexts, "cluster" may refer to the FSx file system itself.
- **EDA vs. Builders:** The product was formerly called "Workload Factory for Builders" and was renamed to "Workload Factory for EDA" in January 2026. Use "EDA" in all new content.
- **Latency analysis components:** Basic analysis uses ONTAP QoS delay center metrics; AI-agent analysis requires Amazon Bedrock configuration and provides deeper insights for data/cluster latency scenarios.
- **Tabbed analysis panel:** Latency events open a panel with Overview (basic analysis) and Over time (interactive graph) tabs.
- **Notification behavior:** Latency notifications are sent per-file-system (not per-volume) and group all affected volumes in a single alert. Max 10 volumes shown in email.
- **Links requirement:** Latency graphs (latency, IOPS, throughput) are available with AWS credentials only. FSx for ONTAP links are required for component breakdown in basic analysis and for AI analysis. Events can be detected without credentials or links (from SNS notifications).
- **Permission modes:** EDA requires read/write permissions. Basic and read-only modes are not supported for latency monitoring.
- **CloudWatch vs. ONTAP data:** Latency graphs show CloudWatch data; basic analysis uses ONTAP QoS data. Slight discrepancies are expected and documented.

## Typical user workflows

- **Setup latency monitoring:** Add AWS credentials → Configure thresholds (warning/critical for read/write) → View events table → Analyze trends with graphs
- **Investigate latency event:** Select event from table → Review Overview tab (basic analysis) → Optionally run AI-agent analysis → View Over time graph → Check Historical breaches → Implement remediation
- **Configure dashboards:** Enable Overview dashboard (CloudWatch metrics) → Configure Project dashboard with AWS tags as custom filters → Monitor capacity, throughput, IOPS
- **Perforce CI/CD integration:** Create project → Associate FSx volume → Create snapshots → Clone workspaces → Integrate P4V client → Manage versions
