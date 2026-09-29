# Femtech Pre-Seed/Seed Sourcing Pipeline

An automated weekly pipeline that sources, screens, and scores pre-seed/seed femtech startups against a fixed investment thesis, so new candidates are surfaced without manual searching each week.

Full run-by-run logic (sources, scoring rubric, thresholds, notification behavior) lives in [femtech-sourcing-pipeline-instructions.md](femtech-sourcing-pipeline-instructions.md) — that file is the source of truth and is what gets updated whenever the pipeline's behavior changes.

> **Note:** This repo documents the pipeline's logic only. The actual sourcing output (the tracker spreadsheet with screened companies, scores, and notes) and the API key used for LinkedIn sourcing are kept private and are not included here.

## Thesis

- **Stage:** Pre-seed/seed only
- **Geography:** US only (hard gate)
- **Sector:** Femtech, across three equally-weighted sub-areas:
  - AI-powered diagnostics
  - Integrated women's health platforms
  - Hormonal health solutions
- **Top dealbreaker:** weak team/founder-market fit — weighted most heavily and always called out explicitly when weak.

## How it works

1. **Dedup check** — skips any company already logged in a prior run.
2. **Source new candidates** — pulled weekly from LinkedIn (via Apify), FemTech Insider, FutureFemHealth, TechCrunch/Axios Pro Rata/Fierce Biotech/MobiHealthNews, ClinicalTrials.gov, the NIH SBIR/STTR database, and SEC EDGAR Form D filings.
3. **Screen and score** — hard gates (US, pre-seed/seed) first, then a 1–5 score on six weighted criteria (Team & Founder-Market Fit 30%, Thesis Fit 15%, Market Opportunity & Timing 15%, Product/Technology Differentiation 15%, Traction & Validation 15%, Business Model & Path to Fundability 10%).
4. **Route by score** — ≥65% total weighted score → Sourcing List; below threshold but on-thesis → Watch list; every outcome logged for dedup.
5. **Save & notify** — tracker updated in place locally, mirrored to Google Drive as a read-only copy, and a summary message is sent after each run.

## Cadence

Runs automatically every Monday ~8:00 AM Pacific.

---

*Owner: Tanya (Tatsiana Litvinova), Venture Institute Fellow*
