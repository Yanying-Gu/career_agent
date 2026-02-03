# DS/ML/AI taxonomy — 9 layers of abstraction

This taxonomy separates DS/ML/AI into layers from **business goals → problem → modeling → production-ready systems**, including MLE and GenAI/LLM layers. It helps reason from business objectives down to technical decisions and clarifies responsibilities across roles (DS, MLE, Data Engineer, DevOps).

## The 9 layers

### 1) Business / Use Cases / Applications (Why are we doing it?)

This is the **business context/business problem**. What real-world problem are we solving?

**Examples**
- Fraud detection
- A/B testing
- Recommendation systems

### 2) Problem Type (What are we trying to solve?)

It is the **prediction problem**. These are **problem formulations**, not tools.

**Examples**
- Classification
- Anomaly detection
- Causal inference
- Reinforcement learning

### 3) Models / Methods (How do we solve it?)

These are **algorithms or modeling approaches**.

Statistical tests like Chi-squared are not predictive models, but they belong to the broader **statistical methods** toolbox. So we could rename this category: **Models & statistical methods**.

**Examples**
- Random forest
- Bayesian models
- Statistical tests (Chi-squared, KS, etc.)

### 4) Libraries / Frameworks (What tools implement it?)

This is **engineering tooling**. These are implementation layers, not concepts.

**Examples**
- pandas
- PyTorch

### 5) Feature & Data Platform Layer

Turn raw data into **reliable, reproducible features** for training and serving, backed by the **storage + compute backbone** that makes those features possible.

Words used here: layer, system, platform, pipeline, infrastructure

**Feature (ML-facing)**
- Feature engineering (domain transformations, encodings, aggregations)
- Feature pipelines (batch + streaming)
- Training-serving consistency
- Feature validation (quality checks, schema / contract expectations)
- Feature stores (offline/online, registry)

**Data platform (backbone)**
- Warehouses / lakehouses
- Batch + stream processing engines
- Ingestion foundations (ELT/ETL reliability, schema enforcement, data contracts)
- Storage + compute governance primitives (access controls, lineage/metadata)

**Responsibility**
- Data Scientist owns: feature design + domain transformations. They answer: “What should the model learn from?” They usually prototype in pandas.
- MLE owns: production feature pipelines, training-serving consistency, feature store integration, reproducibility. They answer: “Can these features run reliably at scale?”
- Data Engineer owns: ingestion + core data pipelines, ETL reliability, schema enforcement, data contracts, warehouse/lake ingestion. They answer: “Can we trust the raw data and its guarantees?”

**Tools**
- Prototype: pandas
- Platform / processing: Spark, dbt, Snowflake, Databricks

### 6) MLOps & Lifecycle Layer

This is about **keeping ML alive after deployment.** DS decides *what* to retrain. MLE builds *how* to retrain.

**Examples**
- Experiment tracking
- Monitoring
- Drift detection
- Retraining pipelines
- Airflow orchestration
- Observability (CloudWatch)
- Versioning
- Rollbacks

### 7) Platform & Infrastructure Layer

This layer solves deployment, scaling, reliability. This is software engineering + cloud engineering.

**Responsibility split**
- MLE primary owner: model containerization, serving architecture, API design, deployment pipelines, autoscaling, performance tuning
- DevOps shared owner: cluster management, networking, security, infrastructure reliability, cloud governance

DevOps ensures the platform exists. MLE ensures ML runs on it.

**Examples**
- Docker
- Kubernetes
- Serverless (Lambda, Functions)
- APIs (API Gateway)
- CI/CD (GitLab)
- IaC (Terraform/CDK)
- Cloud compute (AWS/Azure/GCP)

### 8) GenAI / LLM System Layer

A new stack on top of ML:
- RAG pipelines
- Vector DBs
- Prompt engineering
- Agents & tools
- Memory systems
- LangChain / orchestration

### 9) Roles & Ownership Layer (Who owns what?)

This layer clarifies how responsibilities typically split across roles so you can communicate scope clearly in a CV, interview, or design doc.

**Mental model**
- Use case → Problem formulation → Model / method → Library / framework (DS)
- → Feature & data platform → Platform & infra → MLOps & lifecycle (MLE/DE/DevOps, depending on org)
- → GenAI/LLM system layer (new)

**Rule of thumb**
- Data Scientist: defines what to learn + why it matters
- MLE: makes it run reliably in production
- Data Engineer: makes the data trustworthy and available at scale
- DevOps/Platform: keeps the infrastructure secure and reliable

