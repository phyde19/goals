# Goal 1: Enable and Deliver Core Business ML Platforms and Pipelines

**Weight:** 30–40%

Deliver and sustain the MLOps platforms, pipelines, and integrations that power 
business-critical analytics and AI use cases. Own delivery from development support 
through production operations.

---

## Production ML Pipeline Operations

Ensure continuity and reliability of production ML batch jobs across the active portfolio:

- **Active models:** SRI, Inpatient Readmission, High Cost Claimant (HCC), STROKE, PRISE
- Monitor and triage production job health (Airflow + Databricks)
- Manage the full staging-to-production promotion lifecycle for each model
- Coordinate with data scientists on prod migration readiness and validation
- Respond to and resolve production incidents (compute failures, data access issues, credential expiration)

## New Project Onboarding

Productionize new ML and AI initiatives entering the pipeline:

- **CLARITY** — deploy and support as a production Compass plugin with full lifecycle management
- **Reconsiderations** — coordinate cross-team dependencies (UiPath integration, ADO access) and stand up production workflows
- Establish operational contracts (monitoring, escalation, SLAs) for each new project at onboarding

## Data Scientist Enablement

Serve as the primary operational partner for the data science team throughout the development lifecycle:

- Support development workflows in Databricks (notebooks, clusters, Unity Catalog, MLflow)
- Guide teams through staging → production promotion
- Provision new project repos from standardized templates
- Maintain and support shared tooling (DataScope feature engineering library, db_gcp_auto_script_template)
- Manage ADO repository access and permissions

## Platform Administration

### Databricks
- Workspace governance: repos, workflows, compute, Unity Catalog
- Environment management across dev, test, and production catalogs
- MLflow model registry: versioning, staging/production aliases, artifact management
- Service principal administration
- Databricks sandbox environment setup

### Airflow
- DAG management, scheduling, and variable/connection maintenance
- Concurrency management and pool configuration
- Databricks integration support (RunNow operator)

### Data Platform
- BigQuery project management (idd-dscoe-prod-1 / idd-dscoe-nonprod-1)
- DSA and INSIGHTS dataset governance
- Identity and access management across Azure Entra, Databricks, and GCP IAM
- Provisioning coordination through Saviynt

## Credential and Key Management

- Manage credentials across CyberArk, Azure Key Vault, and GCP service accounts
- Support production service account lifecycle (rotation, access reviews, troubleshooting)
- Proactively address auth-related production failures through improved rotation practices

## Additional Production Support

- **CMS Validation Tool** — ongoing support for the Medicare Advantage bid validation application
- **Incident response** — triage and resolution of production issues as they arise across all supported platforms

---

## Alignment to Division Goals

| Division Goal | Alignment |
|---|---|
| **Support Core Business Functions (35%)** | Direct — production operations, data scientist enablement, and new project onboarding |
| **Service Level Metrics (20%)** | Define and implement service level metrics for ML pipelines: identify (Q1), plan (Q2), implement tracking (Q3), review and adjust (Q4) |
