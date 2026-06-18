# placement-tracker

A single-page progress tracker for two prep tracks — **GenAI & Agentic AI** (16-week roadmap) and **SQL — LeetCode Top 50** (10–14 day sprint) — built for NIT Rourkela placement prep.

No backend, no build step, no dependencies. Everything runs in one `index.html` file and saves to your browser's `localStorage`, so your progress stays on whichever device you open it on.

## Features

- Day-by-day checklist across both tracks, grouped by phase and week
- Every resource link included inline (CodeWithHarry, CampusX, Krish Naik, official docs, LeetCode study plan)
- Per-day notes field and a separate "doubt" field for things to revisit
- A dedicated **Doubts & notes** view that collects every flagged doubt across both tracks in one place — useful right before an interview, or to paste into Claude for a deeper explanation
- An **All resources** view that deduplicates every link from both tracks for quick lookup
- A live progress ledger (days complete, % complete, daily streak) in the left rail
- Fully responsive — works on mobile if you want to tick things off between classes

## Run it locally

No installation needed. Just open `index.html` in any browser:

```bash
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

Or serve it locally if you prefer:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy to GitHub Pages

1. Create a new repository on GitHub (e.g. `placement-tracker`) and push this folder:

   ```bash
   git init
   git add .
   git commit -m "Initial commit: placement tracker"
   git branch -M main
   git remote add origin https://github.com/<your-username>/placement-tracker.git
   git push -u origin main
   ```

2. On GitHub, go to **Settings → Pages**.
3. Under **Source**, select **Deploy from a branch**.
4. Choose the **main** branch and the **/ (root)** folder, then click **Save**.
5. Wait 1–2 minutes. Your tracker will be live at:

   ```
   https://<your-username>.github.io/placement-tracker/
   ```

That's it — no build step, no `gh-pages` branch needed, since this is a static HTML file at the repo root.

## Editing the curriculum

All content lives in the `CURRICULUM` object near the top of the `<script>` block in `index.html`. Each track has `phases` → `weeks` → `days`. To add, remove, or edit a resource, edit that object directly — the UI rebuilds itself from it automatically. Each `day` entry supports:

```js
{
  title: "What to do",
  tag: "time estimate or label",
  desc: "One or two sentences of context",
  link: "https://...",      // optional
  linkText: "Display name for the link"  // optional
}
```

## Notes on data persistence

Progress is stored in `localStorage` under the key `placement_tracker_v1`. This means:

- Your progress is tied to **one browser on one device**. It won't sync across your phone and laptop automatically.
- Clearing browser site data, or using a different browser/incognito window, will reset your progress.
- If you want to back up your progress, open the browser console on the page and run:

  ```js
  console.log(localStorage.getItem('placement_tracker_v1'))
  ```

  Copy the output somewhere safe. To restore it later, run:

  ```js
  localStorage.setItem('placement_tracker_v1', '<paste your saved JSON here>')
  ```

  then refresh the page.

## License

Use freely for your own prep — no attribution required.
