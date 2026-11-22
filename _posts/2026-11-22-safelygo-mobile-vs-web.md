---
title: "SafelyGo: One app, three ways to run it (Expo Go, the web, and an Android file)"
date: 2026-11-22 20:00:00 -0600
project: safelygo
topic: Planning
---

**The question:**
Before testing today, I asked myself something simple: is the app on my phone the "real" mobile app?
Not exactly. SafelyGo is **one codebase**, but right now there are three different ways to run it,
and each one has a different job.

**The three versions:**

| | Expo Go (on my phones) | Web app | Android app file (APK) |
|---|---|---|---|
| **What it is** | Expo's test app loads my code **from my computer** | A copy of the app on a website | A real app you install, with the code **inside** it |
| **Who it's for** | Me, while building and testing | Anyone with a link, on any device | People with an Android phone |
| **Needs my computer on?** | Yes, on the same Wi-Fi | No | No |
| **After I change the code** | Shows up right away (Reload) | I have to deploy again (`npm run deploy:web`) | I have to build a new file |
| **Status** | Using it every day | Online | Not built yet |

All three talk to the **same database** (Supabase). A report sent from my phone shows up on the web,
and the other way around. The only thing that changes is how the app gets onto the screen.

**Why Expo Go isn't enough:**
Expo Go is perfect for building. I save a file, and both phones update in seconds.
But it only works while my computer is running the project, and on an iPhone, Expo Go only opens
projects from your own account. A judge can't just open it.

**Why I still need the web app:**
- **It opens anywhere.** iPhone, Android, or a computer, with nothing to install.
- **It's a quick preview.** Someone can try the app in a minute.
- **It fixed password reset on phones.** The reset email needs a normal web address to send you back to,
  and Expo Go's address doesn't work for that. Now the link opens the website's reset page.

But the web isn't a phone app. The bottom tabs and the map look a little different,
and location sharing can stop when the browser is in the background.

**Why not just put it in the app stores?**

| | Google Play (Android) | Apple App Store (iPhone) |
|---|---|---|
| **Developer account** | One-time fee | **$99 every year** |
| **Age** | Adult account (a parent would have to sign up) | Adult account (a parent would have to sign up) |
| **Before going public** | New personal accounts must test with a group of testers for a couple of weeks first | Apple reviews every app, even for testing with other people |
| **Without a store** | Yes, you can share an **APK** file directly | No. Apple doesn't allow installing a file you send someone |

So for a school project, the stores take too long and need a parent's account.
Android has a way around them: the APK file. iPhone doesn't.

**What changed in my plan:**
In my [iPhone vs web post](/log/2026/11/17/safelygo-iphone-vs-web/), I said the web link would be my main submission.
When I read the competition rules carefully, I saw that the app has to run on **Android or iOS**.
A website isn't either one, so I changed the order:

1. **Android APK: the main submission.** It's a real mobile app, and judges can install it without a store.
2. **Web link: a quick preview** for anyone who wants to try it right away.
3. **A demo video recorded on my iPhone,** so judges can see the iPhone version too.

The code doesn't change at all. It's still one codebase for all three.

**What I learned:**
- "One codebase" doesn't mean "one way to run it." Each way has its own job.
- Check the rules *before* deciding how to submit, not after. I almost picked the wrong main link.
- The hard part of sharing an app isn't the code. It's the stores, the accounts, and the rules around them.

**Next step:**
Test everything I built last week on both phones, then build the live campus safety map.
After that, the Android APK.
