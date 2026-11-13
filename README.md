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
  → pick the best parts of that week's notes
  → write the English post myself (draft in portfolio-notes\<project>\drafts\)
  → privacy check → copy into _posts/ → commit → push

At each milestone
  → update _projects/<project>.md (status, goals table, what went wrong, results)
```

"Once a week, 5–10 lines" is the **minimum**, not a limit. Long posts are fine when I have a lot to say.

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

- **Write it myself, in my own voice.** Grammar mistakes are fine; my English growing over the years is part of the story.
  If I ask AI for help, ask it to *point out* awkward parts, not rewrite them.
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
