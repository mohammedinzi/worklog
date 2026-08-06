# Engineering Worklog

Daily work log for EasyCloud, kept by Inzi. Every task done during the day — infra work, CRM
features, bug fixes, client rollouts — gets logged here the same day. When someone asks "what
did you do on [date]" or "what did you do this month," this page is the answer: open it, search
or click a day on the calendar, done.

**Live site:** `https://<github-username>.github.io/worklog/` (once GitHub Pages is enabled —
see below).

## What's here

- `index.html` — the page itself: search, status/workstream filters, a mini calendar to jump to
  any day, and a month → day → item timeline. Light/dark theme, works on phone and desktop.
- `data/entries.js` — the actual log data, as a plain JS array. This is the only file you need
  to touch to add new entries.

## Logging a new day

Open `data/entries.js` and add one object per work item to the `window.WORKLOG_ENTRIES` array:

```js
{
  date: "2026-08-07",          // required, YYYY-MM-DD
  time: "14:30",               // optional, "HH:MM" 24h, or null
  status: "good",              // "good" (completed) | "warn" (in progress/blocked-but-resolved) | "bad" (blocked)
  statusLabel: "Completed",    // shown on the pill — can be any short phrase, e.g. "Blocked · resolved next day"
  title: "Short, specific title of the work item",
  tag: "Module / Area",        // e.g. "Lead / Integrations"
  purpose: "One or two sentences: why this mattered, in plain language.",
  detail: "<p>Optional deeper technical detail. Raw HTML — use <strong> and multiple <p> tags freely.</p>",
  detailText: "Plain-text version of the same detail, used for search matching only.",
  phase: "Workstream name",    // groups items in the Workstream filter dropdown
  phaseId: "phase-13"          // any unique slug for that workstream; reuse an existing phaseId to add to an existing workstream
}
```

Leave `detail`/`detailText` as empty strings (`""`) if there's no extra technical detail to add —
the "Technical detail" toggle just won't show for that entry.

Save the file, refresh `index.html` — no build step, nothing else to run.

## Previewing locally

```bash
python3 -m http.server 8000
# open http://localhost:8000/index.html
```

## Publishing (GitHub Pages)

1. Push this repo to GitHub (already the case if you're reading this on GitHub).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to "Deploy from a branch," pick the `main`
   branch and `/ (root)` folder, then save.
4. GitHub publishes the page at `https://<username>.github.io/<repo>/` within a minute or two.

After that, any push to `main` updates the live page automatically.
