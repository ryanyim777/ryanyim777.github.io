# My engineering portfolio

A Jekyll site hosted free on GitHub Pages. No installs are needed to update it:
you can edit everything right on github.com.

## Folder map

| Folder / file | What it is |
|---|---|
| `_config.yml` | Your name, email, school. **Edit this first.** |
| `_projects/` | One file per project (the polished summary pages) |
| `_posts/` | Build log entries (short notes, newest shows first) |
| `about.md` | About page |
| `assets/images/` | Photos (make one folder per project) |
| `templates/` | Copy-and-paste starters for new posts and projects |

## Everyday workflow

**New build log entry (aim for once a week):**
1. Copy `templates/new-log-entry.md`.
2. Create `_posts/YYYY-MM-DD-short-title.md` (example: `2026-11-08-first-jam.md`).
   Posts dated in the future won't show up.
3. Fill in 5–10 lines and add a photo.

**Adding a photo:**
1. Upload it to `assets/images/<project>/` (shrink it first; under 500 KB is ideal).
2. In your post: `![What the photo shows](/assets/images/feeder/photo-name.jpg)`

**Finished a milestone?** Update the matching page in `_projects/`.

## Writing tips

- Write like you're explaining to a smart friend, in your own voice.
- **Failures are the best content.** Say what broke, why, and what you changed.
- Use numbers whenever you can: "jams dropped from 7/10 to 2/10."
- If you followed a tutorial, link it and explain what *you* did differently.
- Never post your home address, phone number, or detailed schedule.

## Publish (one-time setup)

1. Create a repo named **`<your-github-id>.github.io`** and upload these files.
2. Go to **Settings → Pages** → Source: *Deploy from a branch* → `main` / `(root)`.
3. Wait about a minute, then visit `https://<your-github-id>.github.io`.

## Preview on your computer (optional)

```bash
gem install jekyll
jekyll serve
```

Then open http://localhost:4000
