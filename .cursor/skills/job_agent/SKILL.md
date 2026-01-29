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

1. **Step 1 (Primary)**: Search Target Company Career Pages within **INITIAL_RECENCY_WEEKS**
2. **Step 2 (Secondary)**: If Step 1 returns < **MIN_COMPANY_PAGE_RESULTS**, also search Example Job Search Sites within **INITIAL_RECENCY_WEEKS**
3. **Step 3 (Fallback)**: If Steps 1+2 return < **MIN_COMPANY_PAGE_RESULTS** results, broaden to **FALLBACK_RECENCY_WEEKS** for both source types
4. **Step 4 (Final)**: Apply all quality checks and "Output Standards" to results


## Inputs I Need
- Target role title(s): Data Scientist, Machine Learning Engineer, AI Engineer
- Company size: Medium to enterprise-sized companies (exclude startups and consulting firms)
- Location and work mode: Alkmaar, within 50 km radius STRICT (onsite, hybrid, remote)
  - Amsterdam: ~40 km ✓
  - Haarlem: ~20 km ✓
  - Eindhoven: ~120 km ✗ (too far)
- Experience level: Mid or Senior
- Required skills or keywords: Optional (to be specified later)

## Output Standards
- ONLY include verified, currently active positions
- Provide a short list of matching roles with rationale
- For each job, include:
  - Company and Job title
  - Direct job posting link (if accessible)
  - **Source type and URL:**
    - **[Company Career Page]** if found via Target Company Career Pages (e.g., "ING Careers: https://careers.ing.com/...")
    - **[Job Aggregator]** if found via Example Job Search Sites (e.g., "LinkedIn: https://linkedin.com/...")
  - Posting date (when the job was posted/updated)
  - **Priority indicator:** Mark jobs from Target Company Career Pages with ⭐ (more reliable)
- CRITICAL: Use the recency window currently active in the **SEARCH WORKFLOW**. (verify posting date)
- Verify that job listings are currently active and accepting applications by checking:
  - Job posting page loads successfully (not showing "no longer available" or "position closed")
  - Posting has an "Apply" or "Apply Now" button visible
  - No messages indicating "This position has been filled" or similar
- Test each job link to ensure it's accessible (returns HTTP 200 status) before including in results
- If a direct link is broken or shows "no longer available", EXCLUDE it from results entirely
- If unsure about job availability, do NOT include it - only show verified active positions
- Check job_history.md to avoid showing saved jobs again
- Check blacklist.md for three types of exclusions:
  - Blacklisted Companies: Exclude ALL jobs from these companies (entire company blocked)
  - Blacklisted Job Titles: Exclude all postings with this specific job title at this company (e.g., "Uber - Staff ML Engineer" blocks ALL Staff ML Engineer roles at Uber)
  - Blacklisted Job Postings (URLs): Exclude only specific posting URLs (e.g., expired links). Same job title with new URL is allowed
- Do NOT automatically save results - user will manually add jobs to job_history.md if interested
- For testing, return only the top **MIN_COMPANY_PAGE_RESULTS** most recent results

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
