---
name: Job Agent
description: Find job positions that match the user's needs.
---

## Overview
This Skill focuses only on identifying job positions that fit the user's needs.

**Quality over quantity:** Only return verified, currently active job postings. Better to return 2-3 confirmed active jobs than 5+ jobs with uncertain availability.

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
- Provide a short list of matching roles with rationale
- For each job, include:
  - Company and Job title
  - Direct job posting link (if accessible)
  - Company careers page as backup link
  - Source job search site where (which Job Search Sites) the posting was found
  - Posting date (when the job was posted/updated)
- CRITICAL: Only show job positions posted or updated within the last 2 weeks (verify posting date)
- Verify that job listings are currently active and accepting applications by checking:
  - Job posting page loads successfully (not showing "no longer available" or "position closed")
  - Posting has an "Apply" or "Apply Now" button visible
  - No messages indicating "This position has been filled" or similar
- Test each job link to ensure it's accessible (returns HTTP 200 status) before including in results
- If a direct link is broken or shows "no longer available", EXCLUDE it from results entirely
- If unsure about job availability, do NOT include it - only show verified active positions
- Check job_history.md to avoid showing saved jobs again
- Check blacklist.md for two types of exclusions:
  - Blacklisted Companies: Exclude ALL jobs from these companies (entire company blocked)
  - Blacklisted Jobs: Exclude ONLY specific job titles at specific companies (other jobs from same company are still allowed)
- Do NOT automatically save results - user will manually add jobs to job_history.md if interested
- For testing, return only the top 5 most recent results

## Job Search Sites
- https://www.linkedin.com/

## Future Job Search Sites (to be added later)
- https://nl.indeed.com/
- https://www.werkzoeken.nl/vacatures/
- https://www.nationalevacaturebank.nl/ 

## Resources
- job_history.md: Manually save jobs you're interested in (user-maintained)
- blacklist.md: Two-level blacklist (user-maintained):
  - Blacklisted Companies: Block all jobs from specific companies
  - Blacklisted Jobs: Block specific job postings

## When to Apply
Apply when the user asks for job positions based on their needs.
