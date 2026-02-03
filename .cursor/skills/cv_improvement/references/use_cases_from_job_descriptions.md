# Use cases / applications from job descriptions

This is a reference list of **Layer-1 use cases** derived from `job_descriptions.md`, with (1) a short description, (2) evidence from the postings, and (3) the key “extra info to clarify” when turning the use case into a practice project.

## Combined: Use cases (with description, evidence, and “extra info to clarify”)

### 1) Conversational AI / chat automation (LLM features at scale)
- **Description**: Build LLM-powered features that operate inside high-volume conversations (assistants, workflows, automations) with product metrics, evaluation, and production rollout.
- **Evidence (jobs)**:
  - Manychat — Machine Learning Engineer (AI Core Team): “ML/LLM solutions end-to-end”, “AI workflows”, “agents”.
  - Manychat — Senior ML Scientist: GenAI/LLM + prompt engineering + RAG preferred.
- **Extra info you’ll need** (use **H: GenAI agents / RAG assistants**):
  - Task type: Q&A, drafting, summarization, tool execution.
  - Knowledge sources: corpus size, freshness, permissions.
  - Safety constraints: disallowed content, prompt injection handling.
  - Evaluation: gold set + rubric, hallucination measurement, cost/latency budget.

### 2) AI agents (tool-using workflows)
- **Description**: Systems that plan/decide steps and call tools (APIs/functions) to complete tasks; requires evaluation, monitoring, and reliable service boundaries.
- **Evidence (jobs)**:
  - Manychat — MLE (AI Core Team): “AI agents (RAG, vector search, memory, tools)”.
  - WeAreBrain — AI Engineer: “design robust AI agents and context-based workflows.”
- **Extra info you’ll need** (use **H**):
  - Task type; tools available; permissions.
  - Safety constraints (prompt injection); fallback behavior.
  - Evaluation method + latency/cost budgets.

### 3) RAG / enterprise knowledge assistant (retrieval + generation)
- **Description**: Retrieve relevant documents/chunks and generate grounded answers; includes indexing, retrieval quality, hallucination control, and prompt-injection considerations.
- **Evidence (jobs)**:
  - Manychat — MLE (AI Core Team): “RAG, vector search”.
  - WeAreBrain — AI Engineer: “Experience with Retrieval Augmented Generation”.
- **Extra info you’ll need** (use **H**):
  - Task type (Q&A vs summarization), corpus size/freshness, permissions.
  - Safety constraints (prompt injection).
  - Evaluation: gold set + rubric, hallucination, cost/latency.

### 4) Search & retrieval components (semantic retrieval / “vector search”)
- **Description**: Improve information retrieval relevance and latency, often via embeddings + vector search + ranking; used inside agents and RAG.
- **Evidence (jobs)**:
  - Manychat — MLE (AI Core Team): “vector search”.
- **Extra info you’ll need** (map to **A: Recommender/ranking** + **H** depending on stack):
  - If retrieval is “ranking a candidate set”: objective + candidate set + feedback + constraints (A).
  - If retrieval is for RAG: knowledge sources + safety + evaluation (H).

### 5) Recommendations
- **Description**: Personalize what a user sees next (items/content) to optimize engagement, conversion, or retention; includes cold-start and exploration/exploitation tradeoffs.
- **Evidence (jobs)**:
  - Bloom & Wild — MLE: “recommendation algorithms”.
  - Catawiki — DS (ML): “Recommender systems” listed as a plus.
- **Extra info you’ll need** (**A: Recommender/ranking**):
  - Objective: CTR, conversion, margin, retention, diversity/novelty.
  - Candidate set: what items can be recommended and why.
  - Feedback type: implicit (click/view) vs explicit (rating).
  - Constraints: cold start, stock/availability, fairness/diversity, exploration policy.

### 6) Ranking (low-latency ML services)
- **Description**: Real-time ordering of candidates (items/results) under strict latency + reliability constraints (often “production-grade, low-latency ML services”).
- **Evidence (jobs)**:
  - Bloom & Wild — MLE: “low-latency ML services for ranking models”.
- **Extra info you’ll need** (**A**):
  - Objective; candidate set; feedback type.
  - Constraints: cold start, fairness/diversity, exploration; (often also latency/SLA).

### 7) Forecasting
- **Description**: Predict future demand/behavior over time (daily/weekly horizons, seasonality, promotions) to drive operations, supply, or marketing.
- **Evidence (jobs)**:
  - Bloom & Wild — MLE: “forecasting engines / forecasting methods”.
  - Nationale Postcode Loterij — DS: “forecasting” listed among techniques used.
- **Extra info you’ll need** (**B: Forecasting**):
  - Forecast target: demand, revenue, staffing, deliveries; per SKU/store/day?
  - Horizon & granularity: next 7 days daily vs next 4 hours 15-min.
  - Drivers: seasonality, holidays, marketing, price, weather.
  - Loss function: MAPE vs quantiles (under/over cost asymmetry).

### 8) Product experimentation (A/B testing)
- **Description**: Measure impact of product changes via controlled experiments; includes experiment design, analysis, guardrails, and decision-making.
- **Evidence (jobs)**:
  - Uber — Data Scientist (Payments): “Design and run experiments… impact of product changes.”
  - Uber — Sr Data Scientist, Payments: “Design experiments… conclusions… impact of product changes.”
  - Bloom & Wild — MLE: supports “design of A/B tests”.
  - Nationale Postcode Loterij — DS: explicitly mentions A/B testing.
- **Extra info you’ll need** (**D: Experimentation/causal impact**):
  - Unit of randomization: user/session/merchant; interference risks.
  - Primary metric + guardrails; minimal detectable effect.
  - Eligibility & ramp: who gets treatment; gradual rollout plan.
  - Bias risks: selection, novelty effects, logging gaps.

### 9) Causal impact measurement (causal inference)
- **Description**: Estimate “what caused what” (uplift/impact) when experimentation isn’t enough or to strengthen conclusions; often paired with A/B testing.
- **Evidence (jobs)**:
  - Nationale Postcode Loterij — DS: explicitly lists “causal inference”.
- **Extra info you’ll need** (**D**):
  - Unit of randomization + assumptions; interference risks.
  - Primary metric + guardrails; minimal detectable effect.
  - Eligibility & ramp; bias risks (selection, logging gaps, novelty effects).

### 10) Payments funnel analytics / payments UX optimization (FinTech product analytics)
- **Description**: Analyze payment success/failure, friction, and drop-offs; define strategic metrics; run experiments; propose product improvements.
- **Evidence (jobs)**:
  - Uber — Data Scientist II, Payments: “understand our payment experiences”, “metrics”, “experiments”.
  - Uber — Sr Data Scientist, Payments: “streamline and optimize Uber’s global payment experiences”, “experiments”, “metrics”.
- **Extra info you’ll need** (**E: Payments/product analytics**):
  - Funnel definition: steps, drop-off, success/fail states.
  - Instrumented events: what you can observe; missing instrumentation.
  - Experiment constraints: risk, regulatory, partner dependencies.

### 11) Retail banking analytics: lending / pricing / personalization
- **Description**: Use analytics/ML to improve bank decisions in lending and pricing and personalization, typically in risk/pricing contexts.
- **Evidence (jobs)**:
  - ING — Senior Data Scientist: “lending, pricing, and personalization analytics”.
- **Extra info you’ll need** (closest fit: **D** for impact + constraints; sometimes **C** for risk-style monitoring):
  - Decision to support: approval/pricing/personalization action and when it is taken.
  - Primary metric + guardrails (risk, fairness, profit, churn).
  - Experimentation constraints (where A/B tests are or aren’t feasible).

### 12) Credit risk / credit decisioning
- **Description**: Predict default/credit outcomes and support decisioning policies; emphasizes end-to-end ML implementation and domain knowledge.
- **Evidence (jobs)**:
  - ING — Senior Data Scientist: advantage: “lending, credit risk, and credit decision domains”.
- **Extra info you’ll need** (closest fit: **C: Fraud/anomaly/AML-style monitoring**, adapted to credit):
  - Definition of “bad” (default, delinquency, write-off) + label delay.
  - Cost of errors (false positives vs false negatives) + operational decision thresholds.
  - Drift sources (macro changes, product changes) + policy/rules hybrid.

### 13) RegTech / regulatory reporting analytics
- **Description**: Build analytics/DS solutions that support regulatory reporting; requires auditability, governance, and aligning with regulatory standards.
- **Evidence (jobs)**:
  - ABN AMRO — Senior Data Scientist (Global Finance / Clearing): “data science solutions for regulatory reporting”, mentions EMIR/MIFID/SFTR.
- **Extra info you’ll need** (**F: RegTech / regulatory reporting**):
  - Regulation scope: what report, what fields, what deadlines.
  - Auditability: lineage, reproducibility, explanation requirements.
  - Data contracts: schema stability, reconciliation checks.

### 14) ML governance, monitoring, drift/bias controls (compliance-aware ML)
- **Description**: Ensure deployed models remain compliant and reliable: monitoring, drift/bias detection, documentation, risk controls, audit trails.
- **Evidence (jobs)**:
  - ABN AMRO — Senior DS (RegTech): “monitoring frameworks to detect bias, drift, and data corruption”.
  - Garanti BBVA — RPA Developer – Data Scientist: “AI governance framework”, “risk controls”, “audit trails”, “DORA/GDPR”.
- **Extra info you’ll need** (closest fit: **F** + monitoring specifics):
  - What must be auditable; what artifacts are required (model cards, approvals).
  - Monitoring targets (latency, drift, bias, data quality) + thresholds + rollback rules.
  - Ownership/workflow for incidents and model changes.

### 15) Intelligent automation (RPA) for business operations
- **Description**: Automate repetitive workflows using RPA/low-code tools, often integrating ML/GenAI for decisioning and content handling.
- **Evidence (jobs)**:
  - Garanti BBVA — RPA Developer – Data Scientist: “Power Automate cloud flows, desktop flows (RPA)”, automating Operations/Finance/Risk workflows.
- **Extra info you’ll need** (**G: RPA / IDP / document AI**):
  - Workflow steps + exceptions; what requires human review.
  - Acceptance criteria (time saved, error rate), audit/logging requirements.
  - If GenAI is integrated: safety constraints + evaluation rubric (H).

### 16) Intelligent Document Processing (IDP)
- **Description**: Extract, classify, and route documents (forms/invoices/contracts) using OCR + document AI; often requires human-in-the-loop.
- **Evidence (jobs)**:
  - Garanti BBVA — RPA Developer – Data Scientist: “IDP solutions using AI Builder or Azure Form Recognizer”.
- **Extra info you’ll need** (**G**):
  - Document types: invoices, KYC forms, emails; variability.
  - Ground truth: human-labeled fields, acceptance criteria.
  - Error tolerance: which fields must be perfect vs “good enough”.
  - Human-in-the-loop: review UI, escalation rules.

### 17) Document generation & summarization (GenAI content tasks)
- **Description**: Use GenAI to draft/summarize documents with governance, monitoring, and safe usage patterns.
- **Evidence (jobs)**:
  - Garanti BBVA — RPA Developer – Data Scientist: “document generation, and summarization use cases”.
- **Extra info you’ll need** (**H**):
  - Task type: drafting vs summarization; audience and correctness requirements.
  - Knowledge sources + permissions (what the model may see).
  - Safety constraints + evaluation (rubric, hallucinations), cost/latency budgets.

### 18) People analytics / employee feedback insights (incl. text + LLM themes)
- **Description**: Turn survey/feedback data into insights and product features; often blends quantitative modeling with text/LLM evaluation.
- **Evidence (jobs)**:
  - Effectory — Senior Data Scientist (Indeed mirror + Effectory site): employee feedback analytics; mentions LLMs/prompt engineering/generative AI evaluation and multi-step flow development.
- **Extra info you’ll need** (**I: People analytics / text insights**):
  - Outcome: sentiment themes, drivers of engagement, churn risk.
  - Text languages: multilingual handling.
  - Privacy: anonymity thresholds, aggregation rules.
  - Human trust: explanation of themes, stability over time.

## Optional: Fraud / anomaly / AML-style monitoring
- **Description**: Detect suspicious behavior and prioritize investigations; adversarial behavior and operational workflows are central.
- **Evidence shown in previous chat**: This theme came up repeatedly in your earlier discussion (e.g., “Anomaly detection vs Fraud detection”, “AML”) even though it is not strongly present in the successfully-fetched text blocks inside `job_descriptions.md`.
- **Extra info you’ll need** (**C: Fraud / anomaly / AML-style monitoring**):
  - Definition of “bad”: confirmed fraud vs suspicious; label delay.
  - Cost of errors: false negatives vs false positives (ops workload).
  - Investigation workflow: queueing, prioritization, thresholds.
  - Adversarial behavior: concept drift by attackers, rule/model hybrid.

