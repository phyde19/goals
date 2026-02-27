# Goal 1: Enable and Deliver Core Business ML Platforms and Pipelines
Weight: 30–40%

This goal covers the day-to-day work that keeps our ML and data science platforms running. 
Production support, data scientist enablement, platform administration, and getting new 
projects into production.

---

## 1. Production Support for ML Batch Jobs

Continue owning the production lifecycle for our Databricks batch jobs triggered from Airflow.
This includes monitoring, triaging failures, coordinating fixes with data scientists, and 
managing the staging-to-prod promotion process.

Active projects:
- SRI
- Inpatient Readmission
- High Cost Claimant (HCC)
- STROKE (clinical model)
- PRISE (Provider Risk & Insights Scoring Engine)

What this looks like practically:
- Morning monitoring of Airflow DAG runs and Databricks workflow status
- Triaging compute failures, executor timeouts, OOM errors, GCP connection issues
- Managing Airflow variables (job name + job ID key-value pairs, cron schedules)
- Coordinating prod migration tickets in ADO with data scientists
- Manual workflow cloning (nonprod_gcp_* → prod_gcp_*) and validation runs
- Pulling branches to Databricks repo folders (staging → repos/Staging, main → repos/Production)

## 2. Getting CLARITY and Reconsiderations Off the Ground

These are newer initiatives that need to be productionized. CLARITY is already integrated 
as a Compass plugin and Reconsiderations has cross-team dependencies (UiPath dev team 
collaboration, ADO repo access coordination). Both need the standard deployment pipeline 
work: nonprod workflow validation, prod workflow setup, Airflow registration, and 
ongoing monitoring once live.

## 3. Data Scientist Support

Day-to-day enablement for our data science team through the full development lifecycle.

- Supporting development workflows in Databricks (notebooks, clusters, Unity Catalog)
- Walking through the staging → prod promotion process
- Cookie-cutter repo setup for new projects (currently manual — SSH into server, 
  run cookiecutter with project info received over Teams/email)
- db_gcp_auto_script_template support (branch, update, PR, pipeline → Databricks → GBQ prod)
- Troubleshooting data access issues (BigQuery auth, Unity Catalog permissions, etc.)
- ADO repo access and permissions management (Saviynt roles, project security groups)
- DataScope library support (reusable PySpark feature engineering)

## 4. Databricks Administration

- Workspace management: repos, workflows, clusters, Unity Catalog
- Unity Catalog governance across environments (dev_dsa → test_dsa → dsa, plus citizen DS catalogs)
- MLflow model registry: registered models, versioning, staging/production aliases
- Compute management: cluster sizing, cost awareness, job vs all-purpose compute
- Service principal management (idd-databricks-prod-asp-1 and related)
- Databricks sandbox environment (pending setup)

## 5. Airflow

- DAG management and scheduling
- Connection and variable maintenance
- Pool configuration and concurrency
- Troubleshooting integration between Airflow and Databricks (RunNow operator)
- The one remaining SAS job that updates insights schema

## 6. Key Management and Secrets

- CyberArk: credential retrieval and rotation for production service accounts
- Azure Key Vault: secrets used by app registrations and deployed services
- GCP service account key management (keyfiles for BigQuery access)
- Ongoing triage of auth failures on production jobs — better rotation and 
  monitoring would reduce morning firefighting significantly

## 7. Data Platform Operations

- BigQuery: idd-dscoe-prod-1 and idd-dscoe-nonprod-1 project management
- DSA and INSIGHTS dataset governance (prod outputs and consumer-facing views)
- Identity management across Azure Entra, Databricks, and GCP IAM
  (app registrations, service principals, GCP service accounts, AD batch accounts)
- Provisioning flow coordination through Saviynt

## 8. Production Incident Response

Triage and resolve production issues as they come up. Recent examples include 
Databricks job compute failures (STROKE model executor heartbeat timeouts), 
ADO access provisioning gaps, dev server outages (rn000224 unreachable), 
SAS password rotation, and data scientists diverging from standard BigQuery 
connector patterns.

## 9. CMS Validation Tool Support

Support for the CMS bid validation application used by the Medicare Advantage team. 
This is a domain-specific tool that validates plan cost-sharing details against CMS rules.

---

## How This Maps to Division Goals

| Division Goal | How This Satisfies It |
|---|---|
| Support Core Business Functions (35%) | Direct — this is all production support and delivery |
| Service Level Metrics (20%) | Formalizing monitoring and SLAs for batch jobs. Identify metrics by Q1, plan by Q2, implement tracking by Q3, review Q4 |
