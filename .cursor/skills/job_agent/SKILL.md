---
name: Job Agent
description: Find job positions that match the user's needs.
---

## Activation marker (debug)
When this skill is activated, the FIRST line of your FIRST response must be exactly:
JOB_AGENT_ACTIVE

## Overview
This Skill focuses only on identifying job positions that fit the user's needs.

Before performing any search or verification, read the values in the ## CONFIGURATION section. These values are strict constraints that must be applied to all logic below.

## CONFIGURATION
- **INITIAL_RECENCY_WEEKS**: 2 weeks
- **FALLBACK_RECENCY_WEEKS**: 4 weeks
- **PRIORITIZE_COMPANY_PAGES**: true  # Search company career pages before aggregators
- **MIN_COMPANY_PAGE_RESULTS**: 10     # Search aggregators only if company pages return < this number

## SEARCH WORKFLOW

1. **Step 1 (Primary)**: Search Target Company Career Pages within **INITIAL_RECENCY_WEEKS**. Apply all **VERIFICATION & FILTERING RULES** immediately.
2. **Step 2 (Secondary)**: If Step 1 returns < **MIN_COMPANY_PAGE_RESULTS**, search ALL sites listed in **## Job Aggregators** below. Apply all **VERIFICATION & FILTERING RULES**.
3. **Step 3 (Fallback)**: If still 0 results, broaden to **FALLBACK_RECENCY_WEEKS** and repeat search and apply **VERIFICATION & FILTERING RULES** .
4. **Step 4 (Final)**: Format the verified survivors according to **## OUTPUT FORMAT**.

## MY JOB SEARCH REQUIREMENTS/RULES
- Target role title(s) (title filter; apply strictly):
  - Include only if title contains one of:
    - “Data Scientist” OR “Data Science” OR token/word "DS"
    - “Machine Learning” OR token/word “ML”
    - "AI engineer" OR token/word “AI”
  - Exclude if title contains:
    - “Analyst” (Data Analyst/BI Analyst/etc.)
    - “Data Engineer”
  - If unsure → ask me
- Company size: Medium to enterprise-sized companies (exclude startups and consulting firms)
- Location and work mode: Alkmaar (within 50 km radius) STRICT (onsite, hybrid, remote)
  - Include if city is within 50 km of Alkmaar (Amsterdam/Haarlem OK, etc.)
  - OR include if explicitly Remote and Netherlands-based (even if no city)
  - Amsterdam: ~40 km ✓
  - Haarlem: ~20 km ✓
  - Eindhoven: ~120 km ✗ (too far)
- Experience level: Mid or Senior
- Required skills or keywords: Optional (to be specified later)

## VERIFICATION & FILTERING RULES
- **Blacklist Check**: Consult `career_agent/.cursor/skills/job_agent/references/blacklist.md`. Exclude blacklisted companies, titles, or specific URLs.
- **History Check**: Consult `career_agent/.cursor/skills/job_agent/references/job_history.md`. Do NOT suggest jobs already saved, applied, or archived.
- **Recency & Posting Date**:
  - Prefer postings with a visible posting/updated date within the current recency window (**INITIAL_RECENCY_WEEKS**, or **FALLBACK_RECENCY_WEEKS** if in fallback).
  - If the posting date is not visible, do NOT exclude the job for that reason alone.
  - If a visible posting/updated date is present and it is outside the current recency window, exclude it.
- **Live Check**: 
  - **HTTP check**: Verify the **job posting page URL** returns HTTP 200 (no 404/410/3xx loops).
  - **Closed/expired text check**: Exclude if the page shows any “closed/expired” messaging, including (non-exhaustive):
    - "no longer available", "position closed", "sorry, this job is no longer available", "filled"
    - "This job has expired", "We couldn't find this job", "Sorry, ..."
    - "vacature is verlopen", "niet meer beschikbaar", "deze vacature is gesloten"
  - **Apply flow check (required)**:
    - The posting must have a visible "Apply" / "Apply Now" button **AND**
    - The **apply target URL** (if separate, e.g. `/apply` on Lever/Workday/Greenhouse) must also return HTTP 200 and show an actual application form (e.g. "Submit your application"), not an error page.
- **Cookie/JS gated pages (special case)**:
  - If the posting/apply flow cannot be verified due to cookie banners, JS-rendering, bot protection, or other gating, do NOT exclude automatically.
  - Mark the result as **Unverified (cookie/JS gated)** in the output and include a short note on what could not be verified.
- **Availability**: If unsure, exclude it. Only show verified active positions. (**Exceptions**: "posting date not shown" is allowed if the job passes **Live Check**; cookie/JS gated pages may be listed as **Unverified (cookie/JS gated)**.)

## OUTPUT FORMAT
- Provide a short list of matching roles with rationale.
- For each job, include:
  - Company and Job title
  - Direct job posting link
  - **Source type and URL:**
    - **[Company Career Page]** (e.g., "ING Careers: https://...")
    - **[Job Aggregator]** (e.g., "LinkedIn: https://...")
  - Posting date (or **"not shown"**)
  - Verification status: **Verified** OR **Unverified (cookie/JS gated)** (with a one-line reason)
  - **Priority indicator:** Mark jobs from Target Company Career Pages with ⭐.
- Do NOT automatically save results - user adds them manually.
- For testing, return only the top **MIN_COMPANY_PAGE_RESULTS** most recent results.

## Target Company Career Pages (Primary Sources - Search First)

- ING: https://careers.ing.com/en
- Schiphol: https://www.schiphol.nl/en/careers
- Albert Heijn: https://werk.ah.nl/vacatures

## Job Aggregators (Secondary Sources)

When Step 2 triggers, search ALL of the following sites. Additional reputable sources are permitted.

- LinkedIn: https://www.linkedin.com/jobs/
- Indeed NL: https://nl.indeed.com/
- Werkzoeken: https://www.werkzoeken.nl/vacatures/
- Nationale Vacaturebank: https://www.nationalevacaturebank.nl/

## Resources
- career_agent/.cursor/skills/job_agent/references/job_history.md: Manually save jobs you're interested in (user-maintained)
- career_agent/.cursor/skills/job_agent/references/blacklist.md: Three-level blacklist (user-maintained):
  - Blacklisted Companies: Block all jobs from specific companies
  - Blacklisted Job Titles: Block specific job title at specific company (all URLs)
  - Blacklisted Job Postings (URLs): Block specific posting URLs only (e.g., expired links)

## When to Apply
Apply when the user asks for job positions based on their needs.
