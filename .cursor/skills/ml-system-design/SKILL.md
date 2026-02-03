---
name: ml-system-design
description: "Framework for architecting and reasoning about end-to-end Machine Learning systems. Triggers when the user is in PLAN mode or expresses intent to: (1) design a new ML system/feature, (2) draft an ML design document, (3) scale an existing ML service, or (4) reason about architectural trade-offs (e.g., latency vs. accuracy). Follows the Ali Aminian & Alex Xu 'Machine Learning System Design Interview' framework."
---

# ML System Design Orchestrator

This skill guides you through architecting production-grade ML systems using the industry-standard interview framework and the 9-layer DS/ML/AI taxonomy.

## Operating Protocol

When triggered, especially in **PLAN mode**, guide the user through these five phases sequentially. Do not skip to modeling until the objective and scale are clarified.

### Phase 1: Clarification & Objective Setting
- **Primary Goal**: Define the business problem and KPIs.
- **Action**: Help the user fill out the `assets/system_design_template.md`.
- **Key Questions**:
    - What is the primary KPI (e.g., CTR, Conversion, Revenue)?
    - What are the guardrail metrics (e.g., latency, diversity)?
    - What is the scale (number of users, items, requests per second)?

### Phase 2: High-Level Architecture
- **Framework**: Propose a "Candidate Generation → Ranking → Re-ranking" flow for retrieval systems, or an appropriate DAG for other tasks.
- **Mapping**: Align each component to the 9-layer taxonomy (`career_agent/.cursor/skills/cv_improvement/references/ds_ml_ai_taxonomy.md`).
- **Storage/Compute**: Define Batch vs. Streaming vs. Online requirements.

### Phase 3: Data Engineering & Feature Layer
- **Signals**: Identify positive/negative feedback loops.
- **Labels**: Define the label window and potential leakage/bias (position bias, exposure bias).
- **Features**: Group features into User, Item, and Contextual categories.

### Phase 4: Modeling & Deep Dive
- **Baselines**: Always start with a simple, transparent baseline (e.g., Logistic Regression, Popularity).
- **Deep Learning**: Propose PyTorch-based architectures (e.g., Two-tower, DNN rankers) if scale/complexity justifies it.
- **Exploration**: Propose Bandit policies (e.g., Thompson Sampling, E-greedy) to close the RL gap.
- **OPE**: Define how policies will be evaluated offline (e.g., IPS, SNIPS).

### Phase 5: Evaluation & Monitoring
- **Offline Metrics**: Ranking metrics (NDCG, Recall) vs. Classification metrics (AUC, LogLoss).
- **Online Monitoring**: Drift detection, latency tracking, and A/B testing strategy.

## Design Principles

1. **Imperative Guidance**: Always give clear, actionable steps for the next phase.
2. **Progressive Disclosure**: Refer to `references/` for complex formulas (e.g., OPE) or specific PyTorch snippets if the design doc gets too long.
3. **Plan Mode Synergy**: When the user is in PLAN mode, use this framework to structure the `cursor_plan.md` or design doc.
