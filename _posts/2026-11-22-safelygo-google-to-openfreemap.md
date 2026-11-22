---
title: "SafelyGo: Why I switched from Google Maps to an open map (and the two tries that failed)"
date: 2026-11-22 23:55:00 -0600
project: safelygo
topic: Maps
---

**The surprise when I started building the Android app**
Until now I tested SafelyGo in Expo Go, a test app that already has everything built in, including a
Google Maps key. But my real submission will be an Android app file (an APK), and a real Android app
that shows Google Maps needs **its own Google Maps API key**. Without it, the map screen can crash.

**Why I didn't just get a Google key**
Getting a key turned out to be harder than I expected:
1. You need a **Google Cloud billing account with a credit card**, even though showing a map in a
   phone app costs $0. So a parent would have to sign up.
2. The free-trial sign-up asked me to confirm that I plan to use Google Cloud for a
   **commercial purpose**. SafelyGo is a school competition project, so checking that box felt like
   promising something that isn't true. I didn't check it.
3. The free trial ends after 90 days, which could be right when judges are trying the app.

Then I re-read the competition rules. They say the app must use **at least one API (e.g., maps or
SMS)**. They never say it has to be Google. So I looked for a map that needs no key at all.

**Try 1: plain OpenStreetMap**
OpenStreetMap is a free map that people around the world build together, like Wikipedia for maps.
It worked right away, but it looked busy: lots of bright roads and tiny labels everywhere. My honest
reaction was "this looks weird."

**Try 2: a cleaner style, which suddenly needed a key**
I switched to a cleaner style from a company called CARTO. The result:

<img src="/assets/images/safelygo/map-api-key-required.webp" style="border: 1px solid var(--line);" alt="A blank map with large gray text: API KEY REQUIRED, carto.com/basemaps/apikey, and a blue dot in the middle.">

CARTO now requires an API key, and the advice I followed was out of date. Lesson: **check that a
service really works the way you think before you switch to it.**

**Try 3: OpenFreeMap, checked first**
This time I checked first. OpenFreeMap uses the same OpenStreetMap data, has a clean style called
"Liberty", and needs **no key, no sign-up and no card**. I confirmed that all of its files loaded without
a key, and only then switched. It looked much better.

**Small fixes after trying it on my phone**
- The credit line at the bottom showed up **twice**, so I kept just one short line. Free maps require
  this credit, so it can't be removed completely.
- The **"my location"** button was slow. Getting a brand-new GPS reading can take over 10 seconds
  indoors, so now it uses the phone's location from the last minute if there is one, and otherwise waits
  at most 10 seconds. Reports still take a fresh reading, because campus safety needs to know exactly where to go.
- Place names are now shown **in English**.

**Where each map comes from now**

| Where | Map |
|---|---|
| Android app | OpenFreeMap (OpenStreetMap data) |
| Web version | OpenFreeMap, and now it shows **every** pin (the old web map could only show one) |
| iPhone | Apple Maps (built into the phone, no key needed) |

**Isn't a free map "cheap"?**
I worried about that too. But most people notice whether a map is clean and fast, not who made it.
OpenStreetMap data is real, and many apps build on it. For judges, I can explain it as a choice: no API keys
to leak, no payment account, and no extra tracking by a map company.

**What I learned:**
- Something that works in a test app isn't guaranteed to work in the real app.
- Don't agree to something that isn't true just to get past a sign-up screen.
- Check before switching. My second try failed because I didn't.
