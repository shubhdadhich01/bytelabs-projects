# 10 Production-Style Cloud Projects (AWS, Azure, Multi-Cloud)

A portfolio of paid, hands-on projects covering Cloud, DevOps, DevSecOps, FinOps, Security and Networking. Each one is built around a realistic business scenario with problems seeded into it, so the buyer investigates, fixes and proves the result instead of following a tutorial.

**Design constraints (from the brief)**

- Each project costs a buyer **under $20** to run end to end
- Even split between **AWS and Azure**, with multi-cloud projects counting toward both
- Audience: job seekers, beginners and advanced learners
- Infrastructure as Code is **Terraform**; CI/CD is a mix of **GitHub Actions, Azure DevOps and Jenkins**
- Mostly **combined, end-to-end** projects
- Every project is unique (original scenarios and architectures, not copied from any course or site)

---

## 1. Market Demand Signals

What current hiring data says, which drove the project selection:

- Most senior and cloud DevOps roles in the US now list **Kubernetes** as a baseline skill.
- **Terraform** is arguably the most job-creating tool in the DevOps ecosystem because of its multi-cloud support.
- **DevSecOps** carries a salary premium of roughly 10 to 20 percent.
- Observability, Kubernetes, cloud security, high availability, incident response and automation are among the skills linked to higher pay in cloud engineer postings.
- DevSecOps employers want proof that you built and operated pipelines, using named tools: SAST/DAST/SCA scanners, secrets management and runtime security. SBOM generation and dependency verification are emerging gaps most candidates lack.
- FinOps postings ask for automation of cost forecasting and anomaly detection, plus familiarity with the **FOCUS** billing taxonomy.
- **Platform Engineer** is the hot job title, and cost optimization is a skill that gets people hired even when it is not in the job description.
- Employers reward portfolios that show business value, not just a list of tools.

---

## 2. Portfolio Overview

| # | Project | Cloud | Level | CI/CD | Est. cost |
|---|---|---|---|---|---|
| 1 | Audit-Ready Web Platform | AWS | Beginner | GitHub Actions | $4-8 |
| 2 | Secure Supply Chain for a Fintech API | AWS | Intermediate | Jenkins | $6-12 |
| 3 | Cloud Bill Shock Rescue | AWS | Intermediate | Jenkins | $3-6 |
| 4 | Self-Service Kubernetes Platform | AWS | Advanced | GitHub Actions | $8-15 |
| 5 | Governance-First Landing Zone Lite | Azure | Beginner | Azure DevOps | $3-6 |
| 6 | Signed-and-Admitted AKS Pipeline | Azure | Intermediate | Azure DevOps | $5-10 |
| 7 | Private-by-Default Hub-and-Spoke | Azure | Advanced | Azure DevOps | $8-15 |
| 8 | SRE Incident Response Lab | Azure | Intermediate/Advanced | Azure DevOps | $5-10 |
| 9 | AWS to Azure Private Connectivity | Multi-cloud | Advanced | GitHub Actions | $8-15 |
| 10 | One Pipeline, Two Clouds Capstone | Multi-cloud | Advanced | GitHub Actions | $10-18 |

**Cost note:** these are estimates assuming 6 to 10 hours of runtime and a one-command `terraform destroy` at the end. Current cloud pricing has not been verified. Check every figure in the AWS Pricing Calculator and Azure Pricing Calculator before advertising it.

**Domain coverage**

| Domain | Projects |
|---|---|
| Cloud / IaC | 1, 4, 5, 9, 10 |
| DevOps / GitOps | 1, 4, 5, 10 |
| DevSecOps | 2, 6, 10 |
| FinOps | 3, 4, 10 |
| Security | 1, 2, 5, 6, 7 |
| Networking | 4, 7, 9 |
| SRE / Observability | 4, 8 |

---

## 3. Project Briefs

### Project 1: Audit-Ready Web Platform

- **Cloud:** AWS | **Level:** Beginner | **CI/CD:** GitHub Actions | **Est. cost:** $4-8
- **Domains:** DevOps, Security, FinOps basics, Cloud
- **Business problem:** A startup failed a customer security questionnaire. Its app runs from a single public subnet and uses static access keys.
- **Architecture:** VPC with public and private subnets, ALB in front, ECS Fargate running the app, RDS in private subnets. Terraform state is stored in S3 with locking. GitHub Actions authenticates to AWS through OIDC, so no keys are stored.
- **Tools:** Terraform, Checkov, AWS Budgets, CloudTrail, GitHub Actions
- **Seeded problems:** 10 findings the buyer must discover and remediate (for example public exposure, static credentials, missing encryption, missing logging)
- **Outcome:** A hardened environment and a questionnaire-ready evidence pack.
- **Skills proven:** secure VPC design, OIDC-based CI/CD, IaC scanning, basic cost guardrails

### Project 2: Secure Supply Chain for a Fintech API

- **Cloud:** AWS | **Level:** Intermediate | **CI/CD:** Jenkins | **Est. cost:** $6-12
- **Domains:** DevSecOps, Security, DevOps
- **Business problem:** The security team will not approve releases that have no scan evidence or provenance.
- **Architecture:** Jenkins on a Spot EC2 instance runs these stages in order: secrets scan, SAST, dependency scan, image build, SBOM generation, image signing, then an OPA policy gate. The image is pushed to ECR and deployed to ECS. GuardDuty and Security Hub findings feed back into the pipeline.
- **Tools:** Jenkins, SonarQube, Trivy, Syft, cosign, Conftest/OPA, ECR, ECS, GuardDuty, Security Hub
- **Seeded problems:** 5 bad commits (hardcoded secret, vulnerable dependency, risky base image, misconfigured container, unsigned artifact) that the pipeline must block
- **Outcome:** A working shift-left pipeline with a security report generated per build.
- **Skills proven:** pipeline-native security, SBOM and signing, policy-as-code, cloud security services

### Project 3: Cloud Bill Shock Rescue

- **Cloud:** AWS | **Level:** Intermediate | **CI/CD:** Jenkins | **Est. cost:** $3-6
- **Domains:** FinOps, Cloud, Automation
- **Business problem:** The bill doubled and nobody can say why.
- **Architecture:** A pre-seeded "wasteful" environment (idle EC2, orphaned EBS volumes, oversized RDS, resources with no tags). Cost data lands in S3 and is queried with Athena. Tag enforcement uses AWS Config and an SCP. Anomaly alerts go to Slack, and a Lambda function stops non-prod resources outside working hours.
- **Tools:** Terraform, Cost Explorer and Data Exports, Athena, Lambda, Python, AWS Config, Jenkins
- **Seeded problems:** idle, orphaned, oversized and untagged resources, plus a simulated cost spike
- **Outcome:** A before/after savings report in dollars and percentages, a strong portfolio piece.
- **Note:** Cost data can take up to a day to appear, so plan the lab as a two-day timeline.
- **Skills proven:** cost allocation, tagging governance, anomaly detection, automated optimization

### Project 4: Self-Service Kubernetes Platform

- **Cloud:** AWS | **Level:** Advanced | **CI/CD:** GitHub Actions | **Est. cost:** $8-15
- **Domains:** Platform Engineering, DevOps/GitOps, FinOps, Observability
- **Business problem:** Ten dev teams want to deploy on their own, but the platform team cannot afford cluster sprawl or runaway cost.
- **Architecture:** EKS with Karpenter on Spot nodes, Argo CD for GitOps, Kyverno guardrails, Prometheus and Grafana for monitoring, and OpenCost to show cost per namespace.
- **Tools:** Terraform, EKS, Karpenter, Argo CD, Kyverno, Helm, Prometheus, Grafana, OpenCost, GitHub Actions
- **Outcome:** A new team onboards through a pull request, and the buyer can show cost per team.
- **Skills proven:** Kubernetes at platform level, GitOps, admission policy, autoscaling, cost visibility

### Project 5: Governance-First Landing Zone Lite

- **Cloud:** Azure | **Level:** Beginner | **CI/CD:** Azure DevOps | **Est. cost:** $3-6
- **Domains:** Cloud governance, Security, Networking basics
- **Business problem:** A new company needs guardrails in place before any workload arrives.
- **Architecture:** Management groups and Azure Policy (allowed regions, required tags, no public storage), a basic hub-spoke VNet with NSGs, Key Vault, and managed identities. A small web app is deployed on top.
- **Tools:** Terraform, Azure Policy, Azure DevOps, Key Vault, Defender for Cloud (free tier)
- **Outcome:** The buyer sees policy block a bad deployment and can explain why.
- **Skills proven:** Azure governance, policy as code, secure network baseline, identity-first secrets

### Project 6: Signed-and-Admitted AKS Pipeline

- **Cloud:** Azure | **Level:** Intermediate | **CI/CD:** Azure DevOps | **Est. cost:** $5-10
- **Domains:** DevSecOps, Kubernetes, Security
- **Business problem:** Unsigned and vulnerable images keep reaching the cluster.
- **Architecture:** Azure DevOps runs Gitleaks, Checkov and Trivy, generates an SBOM, then signs the image into ACR. AKS admission policy accepts only signed images. Secrets come from Key Vault through the CSI driver, with Workload Identity.
- **Tools:** Terraform, Azure DevOps, ACR, AKS (free control plane tier), Azure Policy for Kubernetes, Key Vault, Trivy, Gitleaks, Checkov
- **Outcome:** An unsigned image is rejected live in the cluster.
- **Skills proven:** supply chain security, admission control, workload identity, secrets management

### Project 7: Private-by-Default Hub-and-Spoke

- **Cloud:** Azure | **Level:** Advanced | **CI/CD:** Azure DevOps | **Est. cost:** $8-15
- **Domains:** Networking, Security
- **Business problem:** Compliance says no PaaS service may be reachable from the internet.
- **Architecture:** A hub VNet with Azure Firewall (Basic tier) and a spoke for the app. Private Endpoints for SQL and Storage, Private DNS zones, and Application Gateway with WAF as the only public entry point. Flow logs go to Log Analytics.
- **Tools:** Terraform, Azure Firewall, Private Endpoints, Private DNS, Application Gateway WAF, Log Analytics, KQL, Azure DevOps
- **Outcome:** A traffic-path proof pack and a debugging exercise on private DNS, a common real-world headache.
- **Skills proven:** zero-trust network design, private connectivity, DNS troubleshooting, log analysis

### Project 8: SRE Incident Response Lab

- **Cloud:** Azure | **Level:** Intermediate/Advanced | **CI/CD:** Azure DevOps | **Est. cost:** $5-10
- **Domains:** SRE, Observability, Incident response
- **Business problem:** The app has no SLOs and the team learns about outages from customer tweets.
- **Architecture:** An AKS or App Service app with Azure Monitor and Application Insights, SLO-based alerts, and auto-remediation through Automation runbooks. Failure injection scripts trigger 6 incident scenarios.
- **Tools:** Terraform, Azure Monitor, Application Insights, KQL, Azure Automation, Grafana, Azure DevOps
- **Seeded problems:** 6 incident scenarios (for example resource exhaustion, bad deployment, dependency failure)
- **Outcome:** The buyer resolves each incident and writes a postmortem, which is the evidence interviewers ask for.
- **Skills proven:** SLO design, alerting, incident handling, automated remediation, postmortem writing

### Project 9: AWS to Azure Private Connectivity

- **Cloud:** Multi-cloud | **Level:** Advanced | **CI/CD:** GitHub Actions | **Est. cost:** $8-15
- **Domains:** Networking, Multi-cloud, Security
- **Business problem:** After an acquisition, an AWS app must call an Azure database privately.
- **Architecture:** A site-to-site IPsec VPN between an AWS Transit Gateway or VGW and an Azure VPN Gateway, with BGP routing. Cross-cloud DNS forwarding, centralized logs, and a failover test.
- **Tools:** Terraform (AWS and Azure providers), GitHub Actions, BGP, Route 53 Resolver, Azure Private DNS
- **Seeded problems:** 5 injected faults, including overlapping CIDRs, MTU issues and missing routes
- **Outcome:** A working cross-cloud private path and a troubleshooting guide.
- **Skills proven:** hybrid and multi-cloud networking, routing, DNS, fault isolation

### Project 10: One Pipeline, Two Clouds Capstone

- **Cloud:** Multi-cloud | **Level:** Advanced | **CI/CD:** GitHub Actions | **Est. cost:** $10-18
- **Domains:** DevSecOps, FinOps, Platform, Multi-cloud
- **Business problem:** A company wants vendor flexibility, one security standard and one cost view across both clouds.
- **Architecture:** One GitHub Actions pipeline with scan, SBOM, signing and an OPA gate deploys the same app to ECS Fargate and Azure Container Apps. Scheduled drift detection runs, and a Python and DuckDB job normalizes both clouds' billing data into a FOCUS-style report.
- **Tools:** Terraform, GitHub Actions, Trivy, cosign, OPA, ECS Fargate, Azure Container Apps, DuckDB, Python
- **Outcome:** One dashboard of cost per environment per cloud, and a security gate that behaves identically on both.
- **Skills proven:** multi-cloud delivery, unified policy, drift detection, FOCUS-style cost normalization

---

## 4. Standard Package Contents (Same Pattern for Every Project)

1. Business story and problem statement
2. Seeded problems for the buyer to find and fix
3. Architecture diagram with decisions explained
4. Terraform code and pipeline definition
5. Teardown script (one-command destroy)
6. Budget alarm and tagging so the cost promise holds
7. Validation checklist and expected results
8. Portfolio write-up template (what to show in interviews)

## 5. Suggested Learning Path and Bundling

- **Start here:** Project 1 (AWS) or Project 5 (Azure)
- **Build skills:** Projects 2, 3, 6, 7 and 8
- **Finish with:** Projects 4, 9 and 10
- This progression makes bundle pricing natural, for example Beginner Pack, DevSecOps Pack, FinOps Pack, Networking Pack and Capstone Pack.

## 6. Next Steps

- Pick which projects to expand into **full blueprints**: architecture diagram, repo structure, pipeline, runbook and validation steps.
- Verify all cost estimates against current AWS and Azure pricing before publishing.

---

## Sources Consulted for Demand Research

- Edstellar, 10 Key Skills Every DevOps Engineer Should Have in 2026: https://edstellar.com/blog/devops-engineers-skills
- Hirebase, The Most In-Demand Technical Skills for 2026: https://www.hirebase.org/blogs/in-demand-technical-skills-2026
- DEV Community, Cloud Engineer Skills in 2026: https://dev.to/gnana_6392e836fd500a957dc/cloud-engineer-skills-in-2026-breadth-gets-hired-depth-gets-paid-2bok
- KORE1, How to Hire DevOps Engineers in 2026: https://kore1.com/hire-devops-engineers-2026-guide
- Artech, DevOps roles in 2026: https://www.artech.com/blog/devops-roles-2026-skills-resume-portfolio/
- Harvey Nash, The DevOps skills employers are looking for in 2026: https://harveynash.co.uk/latest-news/the-devops-skills-employers-are-looking-for-in-2026
- RemoteStack, Most In-Demand DevOps Skills for Remote Jobs in 2026: https://remotestack.in/blog/most-in-demand-devops-skills-remote-2026
- FinOps Foundation job board: https://jobs.finops.org/?p=8371 and https://jobs.finops.org/?p=7974
- ResumeGeni, DevSecOps Engineer job description and skills guides: https://resumegeni.com/blog/devsecops-engineer-skills-guide
