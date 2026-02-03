# Decision rules & standardized notes (job agent)

## 1) Decision rule after verification

After a job passes **Live Check** and is **not** in `blacklist.md` / `job_history.md`, make a quick decision:

### Save to `job_history.md` if

- You reviewed it and it’s **not a fit right now** (skill gap, level mismatch, domain mismatch, salary/contract, etc.)
- You might reconsider later

### Save to `blacklist.md` if

- The posting is **expired** or **broken**
- It is **permanently out-of-scope** (e.g., too far, always consulting, always startup, work permit impossible)
- You never want to see that **company/title/URL** again

## 2) Standardize statuses + notes (so logging is consistent)

Use a small controlled vocabulary in `{status}` and a short reason in `(Note: ...)`.

### Statuses for `job_history.md`

Use the existing set:

- `interested | applied | interviewing | offer | rejected | expired | archived`

### Recommended note tags

- `skill_gap: CUDA/NCCL`
- `level_mismatch: staff/senior+`
- `domain_mismatch: trading`
- `location_out_of_scope`
- `comp/contract`
- `same_company_applied: already applied to [other role]` — use when you find another role at a company where you already have an active application; archive until you hear back from the first application

