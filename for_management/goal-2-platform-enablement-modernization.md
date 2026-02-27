# Goal 2: AI Platform Enablement, Standardization, and Modernization

**Weight:** 22–35%

Enable teams to build, deploy, and operate AI and ML workloads more efficiently through 
standardized platforms, automated pipelines, and improved developer experience. Modernize 
manual processes into repeatable, enterprise-ready workflows.

---

## CI/CD and Deployment Automation

Establish automated, auditable deployment pipelines for both ML batch jobs and AI web applications.

**ML batch jobs:**
- Adopt Databricks Asset Bundles (DABs) for code-defined job configuration and environment promotion
- Replace manual workflow cloning with pipeline-driven staging → production deployment
- Directly addresses feedback from the Predictive Analytics team

**AI web applications:**
- Implement GitOps-based deployment to OpenShift using ArgoCD
- Move from manual container build/deploy scripts to declarative, version-controlled deployments
- Improve deployment auditability, rollback capability, and consistency across environments

## Operational Efficiency and Self-Service

Assess and incrementally automate recurring MLOps operational tasks to increase team capacity 
for platform and enablement work.

**Approach:**
- Audit recurring operational requests and estimate time allocation
- Classify each task: documentation improvement, scriptable automation, or structured request/approval workflow
- Prioritize high-frequency, low-risk items for automation first
- Measure time recovered and use results to inform further investment

**Target areas:**
- Project repository provisioning (standardize intake and execution)
- Compute resource provisioning (templated cluster configurations)
- Production workflow promotion (reduce manual steps in staging → prod handoff)
- Developer onboarding documentation (self-service guides for common platform tasks)

## Compass AI Platform

Mature Compass from an internal chat application into a reusable AI developer platform 
that accelerates delivery of new AI use cases.

- Refactor to a plugin-based architecture: Compass provides the UI shell, authentication, 
  conversation management, and deployment infrastructure
- AI developers build and register independent plugin services — reducing time-to-production 
  for new AI capabilities
- Standardize the plugin contract and provide starter templates for new plugin development
- CLARITY is the first initiative validating this model in production

## Developer Infrastructure

Improve the on-premises development environment for the data science and AI engineering teams.

- Provision and configure two new dedicated development servers
- Establish a standardized, repeatable environment setup for AI/ML application development
- Improve access management and onboarding processes for new team members

## Credential Management Modernization

Reduce production incidents related to credential expiration and improve security posture.

- Standardize credential mechanisms across production workloads (CyberArk, Azure Key Vault, GCP)
- Adopt improved patterns for cross-cloud authentication (e.g., Workload Identity Federation, 
  Databricks secret scopes)
- Document per-project credential standards to reduce ad-hoc troubleshooting

## Data Science Team Enablement (Brainstorm Action Items)

Respond to concrete requests surfaced in the February 2026 DSCoE brainstorm meeting.

**AI/NLP team:**
- Enable GCP nonprod environments with appropriate service accounts
- Publish guidance on available LLM models, PHI considerations, and cost implications
- Support Databricks compute optimization (cluster sizing, memory profiling, GPU cost assessment)
- Evaluate Databricks model serving and experimentation capabilities

**Predictive Analytics team:**
- Explore lightweight integration testing for production migration (catch configuration errors before deployment)
- Improve feature monitoring through integration with the DataScope library

## LLM Fine-Tuning and Open Source Models (Exploratory)

Scope the feasibility and cost of fine-tuning smaller, open-source language models for 
domain-specific use cases — particularly where PHI sensitivity limits the use of 
external API-based models.

- Assess GPU compute costs in Databricks
- Evaluate Databricks model serving and training infrastructure
- Determine organizational readiness and potential use cases

## AIVA Support (Cross-Team)

Provide technical consultation for the enterprise AI Virtual Assistant initiative — 
specifically around AI evaluation system design, testing methodology, and monitoring infrastructure. 
Contribute MLOps patterns and lessons learned from Compass and batch ML operations.

---

## Alignment to Division Goals

| Division Goal | Alignment |
|---|---|
| **Code and Data Modernization (20%)** | CI/CD adoption, credential modernization, operational automation |
| **Implement AI Automation (25%)** | Compass platform, self-service tooling, LLM exploration, AIVA evaluation support |
| **Support Core Business Functions (35%)** | Developer enablement, brainstorm action items, Compass plugin delivery |
