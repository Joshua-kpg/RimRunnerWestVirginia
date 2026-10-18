# RimRunnerWestVirginia

Unofficial West Virginia HS boys basketball ratings. Not affiliated with the WVSSAC or MaxPreps.
Status: **HELD (waiting on hosting)**. Preview: https://joshua-kpg.github.io/RimRunnerWestVirginia/ (GitHub Pages). No Firebase project yet
(the Google accounts are at their project quota) and Cloudflare Pages is at its project limit, so accounts, picks and follows save only in the
visitor's browser until the site's own Firebase project exists.

## Files
- `index.html` — the whole app (data embedded). `logos/` — small WebP school logos (from MaxPreps school profiles), served with the site.
- `data/results.json` — 2026-27 finals ledger written by the nightly updater.
- `firebase/` — Firestore rules and auth config for the site's future Firebase project (accounts, picks, follows).

## Teams
127 teams: the 121 WVSSAC boys basketball schools on MaxPreps from the WVSSAC 2025-2027 classifications / Regional Alignment (revised 8-14-26):
AAAA 20, AAA 28, AA 34, A 39 (Pickens, WVSSAC Class A Region II, has no MaxPreps boys basketball page), plus 6 Other West Virginia schools
outside the WVSSAC that played 8+ WVSSAC teams in 2025-26. Conferences = each school's MaxPreps 2026-27 conference (17 with 2+ listed teams);
WVSSAC regions are postseason only and are not used as conferences.

## Season rule
WVSSAC boys basketball "1st Contest May Be Held" = Tue Dec 8, 2026 (WVSSAC HS Standardized Calendar 2024-2030). Games involving a WVSSAC school
before that date are left out (schedule build and nightly updater); games between two non-WVSSAC schools are kept.

## Nightly scores
`.github/workflows/nightly-scores.yml` runs `scripts/update_scores.py` at 06:30 and 14:00 UTC (1:30 am / 9:00 am Eastern standard time) and on
manual dispatch. Before `SEASON_START` in index.html (the first game on the MaxPreps schedules) the script makes no requests. From then on it reads
boys basketball finals for the last 3 days from the MaxPreps West Virginia scores-by-date page (team-page fallback), matches them to the schedule by
MaxPreps team id + date, records them in `data/results.json` and bakes scores and W-L records into `index.html`. The page recomputes Elo from those
finals. It commits only when data changed; GitHub Pages updates from the commit.
