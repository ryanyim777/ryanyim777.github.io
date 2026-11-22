---
title: "SafelyGo: Where does a password reset link go? (Site URL and redirect URLs)"
date: 2026-11-22 23:00:00 -0600
project: safelygo
topic: Security
---

**The question:**
To make password reset work from a phone, I changed two settings in Supabase: the **Site URL**
and the list of **Redirect URLs**. It worked, but I didn't really understand what I had changed.
Did I break testing on my phones over Wi-Fi? Why are there four addresses in the list?
And how does a list of addresses stop an attack? So I asked until it made sense.

**Site URL: the default place a link goes back to**
A password reset email has a link in it. After you click it, Supabase needs to send you somewhere:
- If the app said "send them back here" **and** that address is on the allowed list, you go there.
- Otherwise, you go to the **Site URL**.

My Site URL used to be `localhost`. `localhost` means "this same device". On my computer, that's fine.
But on a phone, it means "look for SafelyGo inside this phone's browser", and there's nothing there.
That's why reset links never worked from a phone. Now the Site URL is my website, which opens anywhere.

**Did this change how I test on my phones?**
No. I was worried about this, but the Site URL is only used for links in emails:

| Connection | What it connects | Uses the Site URL? |
|---|---|---|
| Expo Go on the same Wi-Fi | My phone ↔ my computer (to get the code) | No |
| The app ↔ the database | My phone ↔ Supabase (address + public key) | No |
| A link in an email | The email ↔ the screen it opens | **Yes, only this** |

**The four redirect URLs**
This is the list of addresses a link is *allowed* to go back to. `**` means "any page under this address".

| Address | What it is | Used now? |
|---|---|---|
| `exp://**` | Expo Go's address | Not really. Supabase refuses addresses that are just number IPs, which Expo Go uses. That's exactly why I needed a website. |
| `safelygo://**` | The SafelyGo app itself | Later: when I build the Android app, a link can open the app directly |
| `http://localhost:8081/**` | The web version running on my computer | When I test in my computer's browser |
| My website's `/reset-password` page | The reset page on the live website | Yes, this is what phones use now |

**How a list of addresses stops an attack**
The reset link carries a **secret one-time key**. When you click it, Supabase checks the key and then
sends you back to the redirect address *already signed in*.

Imagine there was no allowed list:
1. An attacker asks for a password reset **with my email**, and sets the "send them back to"
   address to **their own website**.
2. I get a **real** email from Supabase. Nothing looks suspicious, because it isn't fake.
3. I click it, and my signed-in key gets delivered to **the attacker's website**.
4. The attacker uses that key to get into my account.

With the allowed list, step 3 fails: the attacker's website isn't on the list, so Supabase ignores it
and sends me to my own Site URL instead. It's like a delivery company that only delivers to
addresses the homeowner registered. If someone writes a different address on the label, it still goes home.

There's one more small safety detail on the reset screen. It always says "If an account exists for
that email, we sent a reset link." It never says whether an email is signed up, so nobody can use
the form to check who has an account.

**Cleanup before I submit:**
- `exp://**` doesn't do anything, so I can remove it.
- `localhost` can go once I'm done developing.
- `safelygo://` stays for the Android app.

**What I learned:**
- A setting can work and I can still not understand it. Asking "what did I just change?" is worth it.
- The Site URL is about email links, not about how the app connects to the database.
- Security isn't only about passwords. It's also about **where secret things are allowed to go**.
