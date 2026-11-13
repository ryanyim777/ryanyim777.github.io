# My engineering portfolio & build journal

A Jekyll site hosted free on GitHub Pages. It's two things at once:

- a **portfolio**: what I've designed and built, including what went wrong, and
- a **journal**: an honest record of what I learned and how I felt along the way, kept for years.

**Rule #1: everything in this folder is public.** Drafts and private thoughts live in my
private notes folder, not here. Only finished, checked writing gets copied in.

## Where things live

| Place | Language | What | Public? |
|---|---|---|---|
| `C:\dev\ryanyim777.github.io\` (this repo) | English | Finished posts and project pages | ✅ Yes |
| `C:\dev\portfolio-notes\` | Korean (+ English drafts) | Daily study notes, drafts, private thoughts | ❌ No |
| `C:\dev\<project>\` | — | Each project's own code (e.g. `C:\dev\safelygo\`) | Depends |

The old unzipped copy in Documents is only a backup from Oct 31. Don't edit it; this clone is the real one.

## Folder map

| Folder / file | What it is |
|---|---|
| `_config.yml` | Site title, tagline, links |
| `_projects/` | One file per project (the polished summary page) |
| `_posts/` | Journal / build log entries (newest shows first) |
| `about.md` | About page |
| `assets/images/<project>/` | Photos, one folder per project (`assets/images/journal/` for non-project posts) |
| `templates/` | Starters: `new-log-entry.md`, `new-reflection.md`, `new-project.md` |

## The writing flow

```
Every work day (10 min, Korean, private)
  → C:\dev\portfolio-notes\<project>\notes\YYYY-MM-DD-....md
      what I did, what broke, what I learned, how I felt

About once a week (English, public)
  → Claude drafts the post(s) from that week's notes: structure + text + <!-- comments -->
  → I edit it myself in VS Code (wording, photos)
  → I ask Claude to review (privacy, broken links, image paths)
  → commit → push (me in VS Code, or Claude when I ask)

At each milestone
  → update _projects/<project>.md (status, goals table, what went wrong, results)
```

"Once a week, 5–10 lines" is the **minimum**, not a limit. Long posts are fine when I have a lot to say.

## One project, many posts

The project page (`_projects/<project>.md`) is the **short summary / cover page**. The details live in posts.
Any post with `project: <slug>` is listed automatically under "Build log for this project",
grouped by its `topic:` (oldest first inside each group; posts without a topic go under "Other").

```yaml
---
title: "How I protected the admin role"
project: safelygo
topic: Security        # Weekly log / Design / Security / Debugging / Testing / Results ...
---
```

Split however it reads best: by date ("Week 2") or one idea per post ("The localhost bug").
Reuse the same topic names so the groups stay tidy.

## Editing posts myself (VS Code)

1. VS Code → **File → Open Folder** → `C:\dev\ryanyim777.github.io`
   (install the recommended spell checker when VS Code asks).
2. Posts are in `_posts/`, project pages in `_projects/`. Edit them like any document.
3. `Ctrl + Shift + V` opens a preview (plain style, not the site design, but shows text, tables, and images).
4. `<!-- ... -->` is a hidden comment. It never shows on the site. Claude uses these for notes like "screenshot here".
5. **Photos:** put the file in `assets/images/<project>/` (under ~500 KB), then add one line where it should appear:
   ```markdown
   ![SOS button on the home screen](/assets/images/safelygo/sos-home.png)
   ```
   The path **must start with `/assets/`**. Relative paths break because post URLs are deep (`/log/2026/11/11/...`).
6. **Publish:** Source Control (left sidebar) → write a message → **Commit** → **Sync Changes**. The site updates in 1–2 minutes.
   If the site still looks old, press `Ctrl + F5` (the browser cached the old page).

Quick fixes on github.com (pencil ✏️ icon) are fine too, but then **Pull / Sync in VS Code first** next time,
so my PC copy isn't behind.

## Posting step by step

1. Copy a template:
   - project progress → `templates/new-log-entry.md`
   - anything else (competition recap, year in review, a book, a thought) → `templates/new-reflection.md`
2. Save it as `_posts/YYYY-MM-DD-short-title.md` (lowercase English + hyphens; future dates won't show).
   Use the date the work **started** (a late-night session that crosses midnight keeps the first date).
3. Add photos to `assets/images/<project>/` (shrink to under ~500 KB first).
   In the post: `![What the photo shows](/assets/images/safelygo/sos-button.png)`
4. Run the privacy check below.
5. Commit and push:
   ```bash
   git add .
   git commit -m "Add post: short title"
   git push
   ```
   The site updates about a minute later.

## Privacy check (every post, every photo)

Ask: **"Would I be fine with a stranger reading this ten years from now?"** Then check:

- [ ] No home address, phone number, email, or detailed schedule
- [ ] No real school name or city (my apps use a fictional school, "Sunnyvale High")
- [ ] No other people's names or photos without their OK
- [ ] No keys, passwords, project IDs, or member IDs (blur them in screenshots)
- [ ] Map screenshots use fake test locations only

Public journal vs. private notes:

| Goes here (public) | Stays in private notes |
|---|---|
| What I built, learned, broke, fixed | Unsorted thoughts and worries |
| How it felt ("I was frustrated", "this was so cool") | Stories about friends, family, teachers |
| Rough timing ("this fall") | Exact places, dates, contacts |

## Writing tips

- **Make it sound like me.** Claude drafts posts from my notes; I read every draft out loud and change anything
  that doesn't sound like me before posting. Only real facts and my real feelings go in.
- **Be honest about tools.** If I used AI (e.g. Claude Code as a pair programmer), say so and say what *I* decided.
- **Failures are the best content.** Say what broke, why, and what I changed.
- Use numbers whenever I can: "load time dropped from 4 s to 1 s."
- If I followed a tutorial, link it and explain what I did differently.

## Preview on my computer (optional)

```bash
gem install jekyll
jekyll serve
```

Then open http://localhost:4000
