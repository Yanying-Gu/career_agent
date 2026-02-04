---
name: save-job-descriptions
description: Save and maintain job descriptions for CV tailoring. Syncs jobs from job_history.md to job_links.md, fetches job posting content, and maintains monthly-sharded job_descriptions_YYYY-MM.md files. Use when the user asks to: (1) sync job descriptions, (2) update job links, (3) save job descriptions from job history, or (4) maintain the job_links.md or job_descriptions files.
---

# Save Job Descriptions

## Workflow

### Step 1: Sync job_history.md → job_links.md

1. Read `.cursor/skills/job_agent/references/job_history.md`
2. Read `references/job_links.md`
3. Compare the two files
4. Identify jobs in job_history.md that are NOT in job_links.md
5. Add missing jobs to `job_links.md` with today's date `[YYYY-MM-DD]`
   - Format: `- **Company** - Job Title [YYYY-MM-DD] (URL)`
   - Preserve any status notes (e.g., "rejected", "applied", "archived")

### Step 2: Fetch and save job descriptions

For each newly added job link:
1. Follow the **"Add / update a job description"** rules below
2. Fetch the job posting content
3. Append to the current month's job_descriptions file

### Step 3: Report results

After completing the workflow, provide a summary:
- ✅ **Successfully added**: List jobs with descriptions fetched successfully
- ❌ **Fetch failed (marked in file)**: List jobs where fetching failed (privacy gate, timeout, 404, etc.)
  - Include the reason for failure (e.g., "privacy gate", "timeout", "URL not found")

## Inputs (CV tailoring)

- **Job links index**: `references/job_links.md`
- **Job history source**: `.cursor/skills/job_agent/references/job_history.md`
- **Job description raw text (monthly shards)**:
  - Shards: `references/job_descriptions_YYYY-MM.md` (example: `job_descriptions_2026-02.md`)
  - Use `job_links.md` as the index of what you care about tailoring for.

## Add / update a job description

1. Add the job link to `job_links.md` with `[YYYY-MM-DD]` date
2. Fetch the job posting text (or note `FETCH FAILED`)
3. Append a new section to the **current month** shard file:
   - `## Company — Job Title`
   - `- URL: ...`
   - `### Raw job text`
   - fenced ` ```text ` block (or `FETCH FAILED: ...`)

## Size guardrails (inform + shard)

Before appending, check the current month shard size/lines.

- **Warn** if approaching "too big":
  - \(\ge 0.8\) MB **or** \(\ge 1500\) lines
- **Consider it too big** if:
  - \(\ge 1.0\) MB **or** \(\ge 2000\) lines

If "too big", inform the user and start the next shard:
- Monthly: create/use `job_descriptions_YYYY-MM.md` for the next month.
- If the month file becomes too big mid-month, fall back to weekly sharding for the remainder (e.g. `job_descriptions_2026-02_wk2.md`) and link it from `job_descriptions.md`.
