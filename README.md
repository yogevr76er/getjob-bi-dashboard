# getjob BI Dashboard

Live at **https://getjob-bi.vercel.app**.

## Architecture

- `index.html` — static dashboard. On load, fetches `/workers.json` and renders.
- `workers.json` — current snapshot of active workers from Ubeya. Auto-updated
  daily by a workflow in [`-ubeya-scraper`](https://github.com/yogevr76er/-ubeya-scraper)
  (job: `ubeya-workers-snapshot`), which scrapes Ubeya, regenerates this file,
  and pushes here. Vercel auto-deploys on push.
- `vercel.json` — disables caching for `workers.json` so the dashboard always
  serves the latest data.

## Manual refresh

```
# In ../getjob_BI:
python scripts/generate_workers_json.py
cp data/workers.json ../getjob-bi-dashboard/workers.json
git -C ../getjob-bi-dashboard add workers.json
git -C ../getjob-bi-dashboard commit -m "data: manual refresh"
git -C ../getjob-bi-dashboard push
```
