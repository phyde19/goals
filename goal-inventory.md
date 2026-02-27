# 2026 Goal Inventory

- **Make deployments real**
  - CI/CD for batch jobs (DABs)
  - CI/CD for web apps (ArgoCD + OpenShift)
  - Stop manually cloning workflows and running shell scripts to deploy

- **Automate the repetitive MLOps work**
  - Repo creation, cluster provisioning, prod promotion — all currently manual and ad-hoc
  - Figure out how much of my day is automatable and start chipping away at it
  - Self-service docs and tooling so data scientists aren't blocked on me for common tasks

- **Compass as a platform, not an app**
  - Plugin architecture so AI devs build a service and get UI/auth/CRUD for free
  - Reduce time-to-production for new AI use cases
  - CLARITY proves the model

- **Fix secrets and auth**
  - Standardize credential patterns across production jobs
  - Automated rotation so I'm not triaging auth failures every morning
  - Move toward WIF and secret scopes, away from copying JSON files around

- **Better developer infrastructure**
  - Two new dev servers, clean setup, repeatable config
  - A real development environment for genai app work

- **Respond to what the teams actually asked for**
  - Brainstorm action items: model guidance, GCP enablement, compute help, integration testing, feature monitoring
  - LLM fine-tuning / open source SLMs as an exploratory track

- **Keep production running**
  - This is the baseline — batch job monitoring, incident response, platform admin, data scientist support
  - New projects (CLARITY, Reconsiderations) entering the portfolio
  - Service level metrics to formalize what "running well" means

---

## Detailed Inventory (Ranked Within Groups)

---

## Production Operations
- Production ML batch job monitoring, triage, and incident response (SRI, Readmission, HCC, STROKE, PRISE)
- Credential and secrets management (CyberArk, Azure Key Vault, GCP SA keys) — rotation, triage, reducing auth failures
- Staging → prod workflow promotion (manual cloning, validation runs, Airflow registration)
- Airflow DAG management, scheduling, variables, connections
- Productionize CLARITY and Reconsiderations (new projects entering the pipeline)
- CMS Validation tool support

## Databricks & Data Platform Administration
- Databricks workspace governance (repos, workflows, clusters, compute, service principals)
- Unity Catalog environment management (dev_dsa → test_dsa → dsa, citizen DS catalogs)
- MLflow model registry (registered models, versioning, aliases)
- BigQuery project management (prod + nonprod, DSA/INSIGHTS datasets)
- Identity and access management across Azure Entra, Databricks, GCP IAM, Saviynt
- Databricks sandbox environment setup

## Data Scientist Enablement
- Day-to-day support through the development lifecycle (notebooks, clusters, promotion process)
- ADO repo access and permissions management
- Cookie-cutter repo provisioning for new projects
- db_gcp_auto_script_template support (DS workflow for DDL/DML changes to GCP prod — branch, update, PR, Azure Pipeline → Databricks → BigQuery prod)
- DataScope library support (PySpark feature engineering)
- BigQuery auth and connectivity troubleshooting (adc.json, secret scopes, WIF)

## CI/CD
- Databricks Asset Bundles (DABs) for batch job deployment automation
- ArgoCD for GitOps-based web app deployment to OpenShift
- Azure DevOps pipeline improvements (currently underutilized)

## Operational Automation & Self-Service
- Audit recurring MLOps tasks and estimate time allocation
- Automate repo creation (from manual cookiecutter to scripted/intake-driven)
- Automate or templatize Databricks cluster provisioning
- Reduce manual steps in prod workflow promotion
- Self-service documentation for common developer questions (BigQuery setup, secret scopes, cluster config)

## Compass
- Complete distributed plugin architecture (Hub + Plugin Registry + Plugin Services)
- Compass as a developer platform — AI devs get UI, auth, CRUD, deployment for free
- Plugin contract standardization and starter template for new plugin services
- CLARITY as first external plugin validating the model
- Frontend cleanup and technical debt reduction
- Deployment automation for Compass itself (OpenShift CI/CD)

## Secrets & Credential Modernization
- Standardize credential mechanisms per production job
- Adopt Workload Identity Federation and Databricks secret scopes where possible
- Automated rotation to reduce manual triage
- Document credential standards so this isn't tribal knowledge

## Developer Infrastructure
- Provision and configure rn021117 and rn021118 (greenfield dev servers)
- Standardized dev environment for genai app development
- Sudo access management and user provisioning
- Repeatable server setup for fast onboarding

## DSCoE Brainstorm Requests
- LLM model availability guidance (what's available, PHI, cost)
- GCP nonprod enablement (service accounts for AI/NLP team)
- Databricks compute optimization guidance (memory profiling, cluster sizing)
- Databricks model serving and experimentation evaluation
- Integration testing for prod migration (catch config errors earlier)
- Feature monitoring improvements via DataScope
- Notifications for new Databricks service activations

## LLM / Model Exploration
- GPU compute cost assessment for fine-tuning in Databricks
- Open source SLM feasibility for PHI-sensitive, domain-specific use cases
- Databricks model serving and training infrastructure evaluation

## Service Level Metrics
- Identify service level metrics for ML pipelines (Q1)
- Develop tracking and reporting plan (Q2)
- Implement metric framework (Q3)
- Review results with leadership and adjust (Q4)

## AIVA (Cross-Team)
- Technical consultation on AI evaluation system design
- Testing methodology, offline evals, monitoring infrastructure
- Bring patterns from Compass and batch ML work
