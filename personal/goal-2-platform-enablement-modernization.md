# Goal 2: AI Platform Enablement, Standardization, and Modernization
Weight: 22–35%

This goal covers the work that makes our platforms better — CI/CD, developer experience, 
Compass as a reusable AI platform, infrastructure improvements, and responding to what 
our data science teams have actually asked for.

---

## 1. CI/CD

This is probably the single biggest improvement area. Right now deployment for both 
batch jobs and web apps is largely manual.

**Batch jobs — Databricks Asset Bundles (DABs):**
- Evaluate and adopt DABs as the deployment mechanism for Databricks workflows
- This was directly requested by the PA team in the Feb brainstorm
- Would replace the manual workflow cloning process (nonprod → prod) with 
  code-defined job configuration that moves through environments via pipeline
- Goal: a data scientist defines their workflow as a bundle, PRs it, and 
  promotion to prod is automated (or at minimum semi-automated)

**Web apps — ArgoCD:**
- Implement ArgoCD for GitOps-based deployment of AI web applications to OpenShift
- Also raised in the brainstorm (item 23) — the PA team specifically mentioned 
  ArgoCD and Azure Pipelines as options for CI/CD to OpenShift
- Currently Compass and other apps deploy via manual shell scripts 
  (podman build → push to Nexus → oc apply → oc rollout restart)
- ArgoCD watches a git repo for manifest changes and syncs to the cluster. 
  YAML-driven, auditable, repeatable

## 2. MLOps Operational Automation and Self-Service

A lot of what I do day-to-day is repetitive operational work that arrives informally 
(Teams messages, emails) and gets executed manually. The question worth asking formally: 
how much of the daily MLOps workload is automatable, how much of that automation could 
be officially approved, and what's the realistic time savings?

Examples of work that's currently manual and ad-hoc:

- **Repo creation**: data scientists send project name, lead, description over Teams. 
  I SSH into the dev server, find the cookie-cutter repo, run `cookiecutter .` and 
  fill in the prompts manually. A quick win is a polished shell script. The real win 
  is some kind of intake form or queue where a requester enters info, I approve, 
  and it runs.

- **Databricks cluster creation**: requests come in informally, I go create clusters 
  through the workspace UI or API. Could be templated and requested through a 
  standard process.

- **Prod workflow promotion**: after a staging → main PR is approved, I manually clone 
  the nonprod workflow to prod, update git source, verify tasks, do a validation run, 
  register in Airflow. Every step is documented but none of it is automated.

- **Recurring support questions**: things like "how do I set up my adc.json for BigQuery," 
  "how do secret scopes work," "how do I configure my cluster." Some of this is a 
  documentation problem. Some of it is a tooling/self-service problem.

This isn't about introducing a specific tool or building a portal. It's about:

1. **Audit**: catalog the recurring operational tasks and estimate time spent
2. **Classify**: which ones are documentation fixes, which are scriptable, 
   which need a lightweight request/approval workflow
3. **Incrementally automate**: start with the highest-frequency, lowest-risk items 
   (repo creation, cluster templates, documented procedures)
4. **Measure**: track time saved and use that to justify further investment

The goal is to shift MLOps time from manual execution toward platform work — 
without overbuilding tooling that's harder to maintain than the manual process.

## 3. Compass as a Developer Platform

Compass is the team's AI chat platform. The refactor goal is to make it a thin API 
gateway + UI shell so that AI developers can build plugin services and get the 
frontend, auth, conversation CRUD, and deployment infrastructure for free.

What this means practically:
- Complete the distributed plugin architecture (Hub + Plugin Registry + Plugin Services)
- External AI devs build a FastAPI service that implements the plugin contract, 
  register it, and Compass handles everything else (UI, auth via Azure Entra, 
  conversation persistence, streaming proxy)
- Plugin registry backed by Postgres (replacing Databricks-as-CRUD-DB)
- Standardized plugin request/response contract (PluginRequest → streaming frames)
- Template/starter repo for new plugin services
- CLARITY is the first external plugin proving out this model

This directly addresses brainstorm item 24 — the PA team asked about template repos 
for creating chat/AI apps and whether Compass could serve this purpose.

## 4. On-Prem Server Maintenance and Developer Platform

- Provision and configure rn021117 and rn021118 (new dev servers, greenfield setup)
- Sudo access management and user provisioning
- Standardized development environment for genai app development 
  (podman, python, node, proper tooling)
- Better than what we have on rn000224 which is shared with external 
  devs and stakeholders and has accumulated years of config drift
- Goal: a clean, repeatable server setup that new team members can onboard to quickly

## 5. Secrets Rotation and Management

This is a quality of life improvement that directly reduces production incidents.

- Better secrets rotation practices across CyberArk, Azure Key Vault, and GCP SA keys
- Reduce or eliminate morning auth triage on production batch jobs
- Investigate automated rotation where possible
- Cleaner credential patterns for BigQuery access 
  (e.g. Databricks secret scopes instead of copying JSON files around, 
  WIF instead of long-lived SA keys)
- Document and standardize which credential mechanism each production 
  job should use

## 6. DSCoE Brainstorm Action Items

Concrete asks from the Feb 2, 2026 brainstorm meeting with AI/NLP and PA teams:

**AI/NLP team requests:**
- GCP nonprod enablement: set up GCP_IDDSCOECTZN_TU + GCP_IDDSCOECTZN_TR 
  with service accounts (item 2)
- Model availability guidance: document what LLMs are available (Vertex AI, 
  Azure OpenAI, Databricks foundation models), when to use which, PHI 
  considerations, cost (items 4-9)
- Databricks compute guidance: help with cluster memory issues, profiling, 
  GPU cluster cost assessment (items 11-13)
- Model hosting/experimentation: evaluate Databricks model serving, register 
  external models, set up endpoints (items 14-15)
- Notifications when new Databricks services are activated (item 19)

**PA team requests:**
- Integration testing: today the only evidence for prod migration is "the job ran." 
  Explore lightweight integration tests that catch errors earlier — bad connection 
  strings, schema drift, etc. (item 25)
- Feature monitoring: currently tacked on at end of jobs. Better approach would be 
  adding as a module in DataScope for better developer ergonomics (item 26)

## 7. LLM Fine-Tuning and Open Source SLMs (Nice to Have)

The AI/NLP team expressed interest in GPU clusters for fine-tuning and training 
smaller language models (brainstorm item 12). This is exploratory but worth scoping:

- Cost assessment: GPU vs CPU clusters in Databricks
- Evaluate feasibility of fine-tuning open source models (e.g. for PHI-safe, 
  domain-specific use cases where external API calls are a concern)
- Understand what Databricks offers here (model serving, foundation model APIs, 
  training infrastructure)

## 8. AIVA (Tangential)

AIVA is the enterprise's flagship member-facing AI chatbot. This sits outside 
our team but I'm involved in a technical capacity — specifically around AI 
evaluation system design (testing, offline evals, monitoring, session logging). 

My role here is consultative: inform good system design for the evaluation 
infrastructure, not own the AIVA application itself. Bring patterns from 
Compass and batch ML work where applicable.

---

## How This Maps to Division Goals

| Division Goal | How This Satisfies It |
|---|---|
| Code and Data Modernization (20%) | CI/CD adoption (DABs, ArgoCD), credential modernization, operational automation |
| Implement AI Automation (25%) | Compass platform, LLM exploration, AIVA eval support, self-service tooling |
| Support Core Business Functions — AI efforts (35%) | Compass plugins, model availability guidance, developer enablement |
