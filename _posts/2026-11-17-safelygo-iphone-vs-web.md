---
title: "SafelyGo: Why there's no iPhone app file, and how the web link compares"
date: 2026-11-17 18:00:00 -0600
project: safelygo
topic: Planning
---

**The question:**
I test SafelyGo on my iPhone every day, so I wondered: why can't I just hand out an iPhone app?
The answer is that I *can* run it on an iPhone, but I can't easily *share* it as an iPhone app.

**Why there's no iPhone app file:**

| | Android | iPhone |
|---|---|---|
| Sharing as a file | One **APK** file, anyone can install it | Apple doesn't allow this |
| Installing on other people's phones | Free | Needs the **Apple Developer Program** ($99 a year), then TestFlight or the App Store |
| Age | No limit | You have to be an adult to join, so a parent would have to sign up |
| Review | None | Even TestFlight testing for other people goes through Apple's review |
| Expo Go | — | On iPhone, Expo Go only opens projects from your own account, so judges couldn't open mine |

So from the start, my plan has been: **a web link and an Android APK**, with no iPhone distribution.
The competition only needs a link where judges can run the app, so that's enough.

**What I'll submit:**
1. **A web link.** It opens on an iPhone, an Android phone, or a computer. This is the easiest for judges.
2. **An Android APK** for anyone who wants to install a real app.
3. **A demo video recorded on my iPhone**, since it looks the cleanest there.

The app is one codebase for iPhone, Android, and web. If I ever want to publish a real iPhone app
after the competition, I won't have to rebuild anything. I'd only need the developer account.

**Will the web link look the same as the iPhone app?**
Mostly, yes, because it's the same code. The screens, colors, buttons, the Check on me conversation,
"I need help", reports, and live updates are all the same. But a few things are different on the web:

| | iPhone app (Expo Go) | Web link (Safari on iPhone) |
|---|---|---|
| **Bottom tabs** | iPhone's own tab bar, with icons and words | My own tab buttons, **words only, no icons** (for now) |
| **Map** | Apple Maps | **OpenStreetMap** (looks a little different) |
| **Top of the screen** | Full screen | Safari's **address bar** is at the top |
| **Sharing location** | While the app is open | While the **browser tab** is open, and it may stop when the screen turns off |
| **Calling** | Opens the phone app | Also opens the phone app on an iPhone (a computer can't make calls) |
| **On a computer** | — | The content stays in the middle, about 800 pixels wide |

**How I plan to make them closer:**
1. **Add icons to the web tabs**, so the bottom bar looks like the app's.
2. **Support "Add to Home Screen".** On an iPhone, Safari can save a website to the home screen.
   With the right settings it opens **without the address bar**, like an app. Then I can tell judges:
   "To try it like an app, tap Share → Add to Home Screen."

After I put the web version online, I'll open it in Safari on my iPhone and compare the two side by side.
I'll fix whatever feels most different first.

**What I learned:**
- "Works on iPhone" and "can be shared as an iPhone app" are two different things.
- Planning how people will actually *get* the app matters as much as building it.
- One codebase for three platforms saves a lot of work, but each platform still has small differences to check.
