# Disneyland Public Permit Feed

Live curated feed of City of Anaheim building permits related to the Disneyland Resort.

**Repo:** https://github.com/scoopdisney/dlr-permit-watch

Deploy to Vercel as e.g. `dlpermitwatch.vercel.app` or `disneylandpermits.vercel.app`.

Primary source: City of Anaheim Accela ePermit portal  
Discovery aid: ThemeParkIQ Disneyland Construction Tracker

## Automatic permit scan (permit-scan.yml)

Every three hours GitHub Actions runs `scan.mjs`, which checks public government sources directly and records what it finds in `data/scan/`. It never edits `data/permits.json`, which stays hand-curated.

| File | What it holds |
|------|---------------|
| `data/scan/records.csv` | Every Disney record the scanner has seen, latest state |
| `data/scan/log.csv` | Every change ever detected: NEW, STATUS, DETAIL |
| `data/scan/health.json` | Whether each source worked on the last run |
| `data/scan/events.txt` | This run's changes (empty on a quiet run) |

The first run is a baseline and reports nothing. After that, a run that finds a change comments on the `permit-log` issue and mentions @scoopdisney. A quiet run stays quiet. If a source fails, its old rows are kept and the run posts SOURCE DOWN (and SOURCE BACK when it recovers).

Run it by hand: Actions, Permit scan, Run workflow.
