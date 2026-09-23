# monday-morning-report — Current Work Plan

The current arc of work. Updated when the arc changes, not every
session. For session-by-session state, see HANDOFF.md.

---

## Goal

Validate the starter defaults with real specialty food founders and ship a
polished, distribution-ready v2 template.

## Why this arc, why now

The v1 template is built and working but the three-numbers-per-tier defaults
are working hypotheses, not validated. They need founder confirmation before
the template gets distributed. The sooner this happens, the less likely we
are to ship something that embarrasses the practice.

## Business question this arc answers

Do the starter defaults (cash position, confirmed POs, velocity pulse etc.)
match what specialty food founders at each tier actually need to track
Monday morning?

## Tasks

- [x] Fix `.gitignore` to exclude `~$*.xlsx` (Excel temp lock files)
- [x] Update CLAUDE.md stack/voice sections with actual values (Python, openpyxl, etc.)
- [ ] Share template with 3–5 specialty food founders — collect feedback on the three numbers per tier
- [ ] Update `data/metrics.py` with validated defaults based on founder input
- [ ] Regenerate `output/monday-morning-report.xlsx` with validated defaults
- [ ] Review Cinderhaven case study numbers for internal consistency with other Cinderhaven pieces
- [ ] Final polish pass on template copy and case study

## Out of scope for this arc

- Automated data connection (Shopify API, bank API, ERP) — separate productized engagement
- Google Sheets native version via gspread — only if import quality proves unacceptable
- Landing page or email capture — portfolio site, not this repo
- Article/LinkedIn content — handled separately

## Definition of done for this arc

- [ ] At least 3 founders have seen the template and confirmed (or corrected) the defaults
- [ ] `data/metrics.py` updated to reflect validated defaults
- [ ] `output/monday-morning-report.xlsx` regenerated with final defaults
- [ ] No placeholder or "Suggested default" labels on metrics that have been validated
- [ ] Case study numbers internally consistent with Cinderhaven profile

---

## Arc history

### 2026-05-26 — Build v1 template generator and case study
- Outcome: `output/monday-morning-report.xlsx` shipped with 4 tabs (Setup, This Week, History, Where to Find These), 9 starter metrics across 3 tiers, Cinderhaven 12-week case study, Google Sheets import guide. All built with Python/openpyxl. Working hypothesis defaults labeled clearly.
- Tag: v1.0 (suggested — not yet created)

---

## Improvement history

Track when this project was reviewed and improved via /improve.
Each entry records what was found, what was fixed, and when to
check again.

<!-- Entries are added by /improve — don't delete this section -->

### 2026-09-23 — Audit (health check only)
- **Findings:** 1 critical, 4 important, 3 nice-to-have
- **Top concerns:** Trend arrows can never move: This Week "Last Week (auto)" (C5/C8/C11) reads History!B3/D3/F3, which are formula mirrors of This Week itself, so Last Week always equals This Week and the arrow is always "→". Velocity Pulse guidance says "last 4 weeks ÷ store count" with no ÷4, which gives a 4x-inflated units/store/week. Workflow files (PLAN/HANDOFF/DECISIONS/CLAUDE.md) stop at 2026-05-27 and don't mention client mode, the golden lock, or CI.
- **Other findings:** client_mode `_load_kpis` stores blank KPI values, so a blank row counts as "populated" and suppresses the missing-metric warning; label-edit instructions contradict (This Week note says "change on the Setup tab", Setup A11 says "on the This Week tab", and Setup has no editable labels); README says the output xlsx is gitignored but it is tracked and golden-locked; client-mode.yml comment says v0.2.1 but installs v0.2.2, and its URLs still point at MsShawnP; Cash Position mixes 30-day AR with this-week-only AP (optimistic).
- **Checks run:** golden + client-mode tests 10/10 pass (pytest basetemp inside gitignored client-output/, then deleted); canonical drift gate clean; engagement guard clean. Manual security/code/data pass replaced /security-review, /ce:review, data-science-reviewer. No secrets found.
- **Action taken:** Audit only — no fixes this session
- **Next review:** 2026-12-22
