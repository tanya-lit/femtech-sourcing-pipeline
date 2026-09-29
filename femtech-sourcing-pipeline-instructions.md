# Femtech Pre-Seed/Seed Sourcing Pipeline — Scheduled Task Instructions

This is the full instruction set that runs automatically every Monday morning. It's saved here so you have a readable, standalone record of exactly what the automation does, separate from the tracker's own README tab. If you ever want to change what it does, this is the file to hand back to Claude to update.

**Owner:** Tanya (Tatsiana Litvinova), Venture Institute Fellow
**Runs:** Every Monday, ~8:00 AM Pacific, on your computer (via the scheduled task's local-device link)
**Primary output file:** `Venture Institute/Sourcing/femtech-sourcing-tracker.xlsx` on your computer (updated in place, never overwritten wholesale — this is the single source of truth, and what the dedup check reads each week)
**Mirror copy:** the same tracker is also duplicated to Google Drive, in `Venture Institute/FemTech Sourcing/femtech-sourcing-tracker` (see Step 5) — this is a read-friendly backup copy, not where new data is written from
**Key file:** `Venture Institute/Sourcing/.apify_key` (Apify API key, used for LinkedIn sourcing)

---

## Thesis being screened against

- **Stage:** Pre-seed/seed only
- **Geography:** US only (hard gate — non-US companies are logged and excluded, not scored)
- **Sector:** Femtech, specifically one of three equally-weighted sub-areas:
  - AI-powered diagnostics
  - Integrated women's health platforms
  - Hormonal health solutions
- **#1 dealbreaker:** weak team/founder-market fit — weighted most heavily in scoring and always called out explicitly when weak, even if other factors look strong.

## Step 1 — Check for duplicates first

Before sourcing anything new, read the **Screening Log (Dedup)** tab in the local tracker on your computer. It lists every company this pipeline has ever screened, with outcome and date. Any company already in that log is skipped entirely — never re-added or re-scored.

## Step 2 — Source new candidates

Pulled weekly from the sources with genuine week-to-week refresh (per your sourcing directory's own suggested cadence — the rest of your ~30-source directory, like accelerator cohorts, syndicates, and conferences, stays on your manual/periodic radar rather than being forced into a weekly cycle):

1. **LinkedIn (via Apify)** — using the stored API key. Searches founder titles ("Founder," "Co-Founder," "Founding Engineer") plus sub-thesis keywords; watches for company pages created in the last 6–24 months with 1–15 employees.
2. **FemTech Insider** (femtechinsider.com) — news and investment posts.
3. **FutureFemHealth** (futurefemhealth.com) — latest newsletter issue.
4. **TechCrunch / Axios Pro Rata / Fierce Biotech / MobiHealthNews** — femtech/women's health seed announcements from the past week.
5. **ClinicalTrials.gov** — new trial registrations naming small, unfamiliar sponsor companies.
6. **NIH SBIR/STTR award database** — new awards to companies in the three sub-areas.
7. **SEC EDGAR full-text search** — new Form D filings (Rule 506(b)/(c)) from the past week.

The detailed "what a good signal looks like" reference for each of these lives in `Venture Institute/outputs/femtech-sourcing-signals.md` and `femtech-deal-sourcing-directory.md` — the pipeline reads those each run rather than guessing.

## Step 3 — Screen and score

For every new candidate not already in the Screening Log:

1. **Hard gates first:** confirm US-incorporated/operating and pre-seed/seed stage. Fails either → logged as excluded, never scored.
2. **Score 1–5 on each of six criteria** (mirroring your deal-screener rubric), using only public signals — press, LinkedIn, grant/registry records. There's no deck or founder interview at this stage, so every score is labeled a first-pass triage, not a full diligence call:
   - Team & Founder-Market Fit — **30%** (the dealbreaker; a solo founder with no clinical/technical background matching the specific claim scores ≤2.5 regardless of other strengths, and this is always spelled out in the Notes column)
   - Thesis Fit (stage/geo/sector) — 15%
   - Market Opportunity & Timing — 15%
   - Product/Technology Differentiation — 15%
   - Traction & Validation — 15%
   - Business Model & Path to Fundability — 10%
3. **Total Weighted Score (%)** = weighted average of the six scores, scaled to a percentage (formula in the sheet, not a hardcoded number).
4. **≥65%** → added to the **Sourcing List** tab (the list you asked for, with all the columns: name, stage, region, founders, LinkedIns, website, total raised, product description, thesis sub-category, per-criterion scores, total score, sources, date, notes).
5. **<65% but still on-thesis** → added to **Below Threshold - Watch** instead, so nothing close is silently dropped.
6. **Either way** → logged in **Screening Log (Dedup)** with outcome, score, and date, so it's never re-screened.

## Step 4 — Save locally

- The workbook is updated in place at its existing path on your computer — new rows are appended, nothing existing is overwritten.
- If your computer isn't reachable when Monday's run fires, the run still happens: results are held and committed to the real file the next time your computer is connected, rather than being lost or skipped. In that case the Drive mirror step below is skipped for that run too, since there's nothing new to copy over yet.

## Step 5 — Mirror the output to Google Drive

After the local file is saved, the pipeline also duplicates just the finished tracker to Google Drive, in `Venture Institute/FemTech Sourcing/`, so you have a copy that opens straight from Drive/Sheets on any device without needing your computer connected.

- Google Drive has no "edit in place" for files, so each week this is done by uploading a fresh copy and trashing the previous week's copy — you should only ever see one `femtech-sourcing-tracker` file in that Drive folder at a time, never a pile of old versions.
- The upload is built without running it through a LibreOffice recalculation pass — an earlier version of this pipeline did use that step, and it turned out to inject invisible drawing objects into the file that made Google Drive unable to open or convert it. Skipping that step is what makes the Drive copy open reliably as a real Google Sheet.
- This Drive file is a mirror for reading/sharing only — the pipeline never reads it back for dedup or scoring, so it's safe to view or share without affecting future runs.
- If the Drive upload fails for any reason (permissions, connectivity), the run doesn't stop — the local file is still saved correctly, and the failure is called out in your summary message so you know the Drive copy is stale until the next successful run.

## Step 6 — Notify

After each run, you get a short chat message: how many new companies were screened, how many made the Sourcing List (with names/scores), how many went to Watch, whether the Drive mirror refreshed successfully, and any access or parsing problems (e.g., an invalid Apify key, an unreachable source, or a Drive upload failure).

## Tone and judgment calls

Notes are written balanced and direct — weaknesses (especially founder-market fit) are called out plainly, not smoothed over. The US/pre-seed/seed hard gates here are sourcing-stage filters you set for this list specifically; they're separate from your "don't redirect me on off-thesis deals" instruction, which applies when you personally bring a deal to discuss.

---

*Last updated: 2026-09-14. To change sources, scoring, thresholds, cadence, or the Drive-mirroring behavior, just tell Claude — this file and the live scheduled task should be updated together.*
