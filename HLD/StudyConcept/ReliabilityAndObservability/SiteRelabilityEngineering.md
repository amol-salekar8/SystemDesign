# Site Reliability Engineering (SRE)
 - SLO, SLI, and SLA are core concepts in Site Reliability Engineering (SRE) and service management.

|Term	| Type	        | Audience          | 	Example           |
|-------|--------------|-------------------|--------------------|
|SLI	| Measurement	 | Engineers         | 	99.92%  uptime             |
|SLO	| Target	      | Internal team     | 	99.9% uptime goal |
|SLA	| Contract	    | Customers | 	99.5% guaranteed |

📊 Measure → 🎯 Target → 📜 Contract

## 1️⃣ SLI – Service Level Indicator

**Q. What it is:**
- A metric that measures how well a service is performing.

It answers:
👉 “How are we doing right now?”

**Examples:**
 - **Availability:** % of successful requests (e.g., 99.95%)
- **Latency:** 95th percentile response time < 200ms
- **Error rate:** < 0.1% failed requests
- **Throughput:** Requests per second

Think of SLI as the actual measured value.

**📌 Example:**
 - 99.92% of requests succeeded in the last 30 days → That’s your SLI.

## 2️⃣ SLO – Service Level Objective
**Q.What it is ?**
- A target for an SLI.

**It answers:**
👉 “What performance level do we aim to achieve?”

It’s an internal goal set by the engineering team.

**Example:**
1) **SLI:** Availability
2) **SLO:** 99.9% availability per month

If you hit ≥ 99.9%, you're good.
If not, you've violated your objective.

**📌 Example:**
- We promise internally that availability will be ≥ 99.9% monthly.
- SLOs are used for:
  - Reliability planning
  - Error budgets
  - Release decisions

## 3️⃣ SLA – Service Level Agreement
**Q.What it is ?**
- A formal contract between provider and customer.

**It answers:** 👉 “What happens if we don’t meet the agreed performance?”

**SLAs include:**
- Guaranteed performance levels
- Measurement method
- Reporting process
- Penalties or compensation

**Example:**
- SLA: 99.5% uptime guaranteed per month. 
- If below 99.5%, customer receives service credits.

**SLAs are usually:**
- Slightly lower than SLOs (to provide buffer)
- Legally binding



Core Process

# SRE & Platform Processes Overview

| Area of Focus | Process to be Established | Tools (In House) | Tools (Our Expertise) |
|---------------|--------------------------|-----------------|----------------------|
| **Reliability Management** | SLO/SLI framework | Splunk Observability Cloud | Datadog |
|  | Define, measure, and enforce service reliability | AWS CloudWatch | Azure Monitor |
|  | Error budget tracking and ownership |  |  |
| **Incident Management** | Blameless postmortems | Splunk On-Call | PagerDuty |
|  | Establish/Improve RCA process | ServiceNow | Mattermost |
|  | Incident Workflow | MS Teams | Slack |
|  | Corrective Actions | XWiki | Confluence |
|  | RCA Documentation | ADO |  |
|  | Reduce MTTR, improve response consistency |  |  |
|  | Unified incident culture |  |  |
| **Observability & Alerting** | Centralized Observability | Splunk Cloud, Splunk Observability Cloud | Datadog, Grafana |
|  | Instrument for observability |  |  |
|  | Develop standards for metrics, logs, traces | Azure Log Analytics | Prometheus |
|  | Develop templates for dashboards and alerts | AWS CloudWatch Logs |  |
|  | Early anomaly detection |  |  |
|  | Visibility across systems |  |  |
| **Change Management** | Tooling for controlled rollouts | ADO, Spinnaker, Istio Ingress, Route53 | ArgoCD, GitLab Pipeline, GitHub Actions |
|  | Canary deployments |  |  |
|  | Blue-green deployments |  |  |
|  | GitOps |  |  |
| **Capacity Planning** | Demand forecasting and autoscaling | Kubernetes HPA | AWS Autoscaling |
|  | Service Level Load testing | Azure VM ScaleSet | KEDA |
|  | Prevent resource exhaustion | Kubernetes HPA |  |
|  | Proactive scaling decisions |  |  |
|  | Cloud Cost Optimization |  |  |
| **Toil Management** | Track toil hours, automate repetitive tasks | Tool Development: Java | Java |
|  | Increase engineering velocity |  | Python |
|  | Toil budget and automation focus |  | Golang, Typescript |
| **Release Reliability** | Chaos Engineering | Chaos Mesh | Datadog Chaos Controller |
|  | Validate reliability under stress | Spinnaker |  |
|  | Verified resilience |  |  |
| **Platform Modernization** | Standardized, reusable Infrastructure-as-Code (IaC) frameworks | Hybrid Cloud | Amazon Web Services / Microsoft Azure |
|  | Configuration management repositories | Azure | Terraform / ARM Templates / AWS CloudFormation / CDKs |
|  | Pre-approved deployment templates & pipelines |  |  |
|  | Automated environment provisioning and teardowns | Kubernetes | Chef / Ansible |
|  | Offload tasks from Platform & DevOps teams | Istio | Kubernetes & CNCF Tool Integrations (Istio, KEDA, Crossplane) |