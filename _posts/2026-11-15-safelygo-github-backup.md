---
title: "SafelyGo: Backing up my code to a private GitHub repo, and cleaning up personal info"
date: 2026-11-15 18:30:00 -0600
project: safelygo
topic: Security
---

**Why I did this:**
Until now, my app's code only lived on my computer. If the computer broke, I would lose everything.
So I put the code in a **private GitHub repository**: a copy in the cloud that only I can see.

**Two words I finally understood:**
- **Commit** = a save point. Small and often, like saving a game before a hard level.
- **Push** = sending those save points to GitHub, which is the cloud backup.

Now I push right after every commit. If my computer stopped working tomorrow,
I could download everything from GitHub and keep going.

**Checking before uploading:**
Before the first push, I checked **every commit**, not just the latest one, for things that must never go online:
- the `.env` file (it holds my app's keys)
- my `private/` folder (competition documents, personal information)
- secret keys, and real locations

None of them were in the history. The `.env` file and the `private/` folder are listed in `.gitignore`,
which tells Git never to include them.

**Cleaning up personal info on my blog:**
While checking, I noticed my personal email address in a few places on this blog
(the settings, the footer, and the About page). I removed it, and now people can reach me through my GitHub profile instead.
I also turned on two GitHub settings:
- **Keep my email addresses private**
- **Block command line pushes that expose my email**

**What I learned the hard way:**
Fixing old commits ("rewriting history") changes the ID of *every* commit after it. My notes listed commit IDs,
so I had to update them too. Before rewriting anything, I always made a full backup copy first, just in case.

**What I learned:**
- Commit small and often, and push right away. A backup you forget to make doesn't help.
- Check the whole history, not just the latest version. Something deleted later can still be in an old commit.
- Personal information can hide in unexpected places, like a website footer.
