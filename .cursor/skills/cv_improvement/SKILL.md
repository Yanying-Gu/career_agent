---
name: cv-improvement
description: Improve and tailor a CV/resume to specific job descriptions. Use for CV edits, rewriting bullets, matching keywords, and maintaining CV-tailoring inputs in `references/` (notably `job_links.md` and monthly-sharded `job_descriptions_YYYY-MM.md`), including warning and sharding when job description archives get large.
---

# CV improvement workflow

## Inputs (CV tailoring)

- **Job links**: `references/job_links.md`
- **Job description raw text (monthly shards)**:
  - Shards: `references/job_descriptions_YYYY-MM.md` (example: `job_descriptions_2026-02.md`)
  - Use `job_links.md` as the index of what you care about tailoring for.

## Add / update a job description

- Add the job link to `job_links.md` using the `[YYYY-MM-DD]` date as “added/updated”.
- Fetch the job posting text (or note `FETCH FAILED`).
- Append a new section to the **current month** shard file:
  - `## Company — Job Title`
  - `- URL: ...`
  - `### Raw job text`
  - fenced ` ```text ` block (or `FETCH FAILED: ...`)

## Size guardrails (inform + shard)

Before appending, check the current month shard size/lines.

- **Warn** if approaching “too big”:
  - \(\ge 0.8\) MB **or** \(\ge 1500\) lines
- **Consider it too big** if:
  - \(\ge 1.0\) MB **or** \(\ge 2000\) lines

If “too big”, inform the user and start the next shard:
- Monthly: create/use `job_descriptions_YYYY-MM.md` for the next month.
- If the month file becomes too big mid-month, fall back to weekly sharding for the remainder (e.g. `job_descriptions_2026-02_wk2.md`) and link it from `job_descriptions.md`.
