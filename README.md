# Community CPR Dispatch — R&D Wiki

A static wiki recording an AI-assisted software delivery experiment: what happened,
and what we learned about process, models, and tooling. The application is a testbed;
the product is the process.

The site is **plain static HTML** — no build step, no Jekyll, no GitHub Actions, no
Ruby. GitHub Pages serves the files exactly as they are (a `.nojekyll` file guarantees
this).

## Structure

```
index.html        Overview — what this is, timeline, the reset, the numbers
technical.html    Technical track — the harness, sensors, CI review, determinism
business.html     Business & organization track — team, output, cost, risks
experiment.html   Experiment reference — the register of controlled experiments
qa.html           QA automation — the UI/API test lanes, the skill chain, the regression gate
assets/style.css  Shared stylesheet
.nojekyll         Tells GitHub Pages to serve the files as-is
```

Two tracks (technical, business) stand alone and share the overview. The experiment
reference is a register: one entry per controlled experiment, appended as runs finish,
with the full deep-dive documents living outside this repo.

## Publish on GitHub Pages

1. Create a new repository and push these files to it:
   ```bash
   git init
   git add .
   git commit -m "Community CPR Dispatch R&D wiki"
   git branch -M main
   git remote add origin git@github.com:<org>/<repo>.git
   git push -u origin main
   ```
2. In the repository: **Settings → Pages**.
3. Under **Build and deployment**, set **Source: Deploy from a branch**, then
   **Branch: `main` / `(root)`**, and **Save**.
4. Wait ~1 minute. The site publishes at `https://<org>.github.io/<repo>/`.

To serve it from a subfolder instead, move these files under `/docs` and pick
**Branch: `main` / `/docs`** in step 3.

## Preview locally

Open `index.html` directly in a browser, or serve the folder:

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

## Editing

- Content is in the five `.html` files; styling is all in `assets/style.css`.
- The navigation block is repeated in each page's `<aside class="sidebar">` — five
  links, kept in sync by hand. If the wiki grows enough that this duplication starts
  to hurt, that is the signal to move to a templated setup (e.g. Jekyll, which
  GitHub Pages builds natively) — not before. Zero premature complexity.

## Notes on content

- Neutral, descriptive tone: a record and its findings, not a pitch.
- Cost and output figures are the curated numbers from the weekly reviews; where a
  figure is an estimate, the page says so.
- Experiment entries deliberately omit derivations and caveats that live in the full
  documents (`model-and-harness-comparison.md`, its presentation script). An entry for a
  run still in flight says so and carries no result.
