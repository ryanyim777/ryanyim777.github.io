---
title: "SafelyGo: Turning the web app off (without losing the address)"
date: 2026-11-17 22:30:00 -0600
project: safelygo
topic: Security
---

**Why:**
After I [put the web version online](/log/2026/11/17/safelygo-web-online/), I realized anyone with the link
could open it. The database rules protect everyone's data, but I still wanted the app closed
until I share it with the judges. I also really liked the address, so I didn't want to lose it.

**Is the address mine?**
Yes. The address was made from my project's name and is tied to my Expo project.
As long as I don't delete that project, nobody else can take it. (Note to self: **never delete the Expo project.**)

**How I turned it off:**
I can't just "pause" the website, but I can replace the app with a one-page **"Coming soon"** site.
It has a small "don't list me in search engines" tag. Now the address shows this:

<img src="/assets/images/safelygo/web-coming-soon.webp" style="border: 1px solid var(--line);" alt="A simple page with a shield icon, SafelyGo, and the text Coming soon. This app is not open right now.">

Now it's one command each way, run inside the project folder:
- turn off: `npm run web:off`
- turn on: `npm run deploy:web`

**Mistakes and surprises:**
1. **My first try failed with an "ENOENT" error.** I ran the command from my user folder instead of the project folder,
   and I ran it before the command even existed. npm commands only work in the folder that has `package.json`.
2. **The old app still showed up for a while.** The hosting service keeps a copy of each page for up to
   **1 hour** (a cache). So after switching, the old version can stay visible for up to an hour.
   That works the other way too: I need to turn the app back on **at least an hour before judging**.
3. **Every deployment has its own extra address.** Each time I deploy, the service also creates a second address
   just for that version, and those kept showing the app. I deleted the old ones. Turning the app back on simply makes a new one.

**What it doesn't change:**
The database is still running, so my phone tests in Expo Go work the same. Turning off the website
only hides the web version.

**What I learned:**
- "Off" can mean "replace it with a placeholder," which keeps the address safe.
- Caches make changes slow to appear, so plan ahead before important moments.
- Run commands in the right folder!
