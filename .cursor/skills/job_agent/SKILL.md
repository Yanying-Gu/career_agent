---
name: Job Agent
description: Find job positions that match the user's needs.
---

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
2. **Step 2 (Secondary)**: If Step 1 returns < **MIN_COMPANY_PAGE_RESULTS**, search Job Aggregators. Apply all **VERIFICATION & FILTERING RULES**.
3. **Step 3 (Fallback)**: If still 0 results, broaden to **FALLBACK_RECENCY_WEEKS** and repeat search and apply **VERIFICATION & FILTERING RULES**.
4. **Step 4 (Final)**: Format the verified survivors according to **## OUTPUT FORMAT**.

## MY JOB SEARCH REQUIREMENTS
- Target role title(s): Data Scientist, Machine Learning Engineer, AI Engineer
- Company size: Medium to enterprise-sized companies (exclude startups and consulting firms)
- Location and work mode: Alkmaar, within 50 km radius STRICT (onsite, hybrid, remote)
  - Amsterdam: ~40 km ✓
  - Haarlem: ~20 km ✓
  - Eindhoven: ~120 km ✗ (too far)
- Experience level: Mid or Senior
- Required skills or keywords: Optional (to be specified later)

## VERIFICATION & FILTERING RULES
- **Blacklist Check**: Consult `blacklist.md`. Exclude blacklisted companies, titles, or specific URLs.
- **History Check**: Consult `job_history.md`. Do NOT suggest jobs already saved, applied, or archived.
- **Live Check**: 
  - Link must return HTTP 200.
  - Page must NOT show "no longer available", "position closed", "sorry, this job is no longer available", or "filled".
  - Posting must have a visible "Apply" or "Apply Now" button.
- **Availability**: If unsure, exclude it. Only show verified active positions.

## OUTPUT FORMAT
- Provide a short list of matching roles with rationale.
- For each job, include:
  - Company and Job title
  - Direct job posting link
  - **Source type and URL:**
    - **[Company Career Page]** (e.g., "ING Careers: https://...")
    - **[Job Aggregator]** (e.g., "LinkedIn: https://...")
  - Posting date
  - **Priority indicator:** Mark jobs from Target Company Career Pages with ⭐.
- Do NOT automatically save results - user adds them manually.
- For testing, return only the top **MIN_COMPANY_PAGE_RESULTS** most recent results.

## Target Company Career Pages (Primary Sources - Search First)

- ING: https://careers.ing.com/en
- Schiphol: https://www.schiphol.nl/en/careers

## Example Job Search Sites (Secondary Sources - Non-exhaustive; Use If Needed)

This list is illustrative; you may use other reputable sources.

- https://www.linkedin.com/
- https://nl.indeed.com/
- https://www.werkzoeken.nl/vacatures/
- https://www.nationalevacaturebank.nl/

## Resources
- job_history.md: Manually save jobs you're interested in (user-maintained)
- blacklist.md: Three-level blacklist (user-maintained):
  - Blacklisted Companies: Block all jobs from specific companies
  - Blacklisted Job Titles: Block specific job title at specific company (all URLs)
  - Blacklisted Job Postings (URLs): Block specific posting URLs only (e.g., expired links)

## When to Apply
Apply when the user asks for job positions based on their needs.
