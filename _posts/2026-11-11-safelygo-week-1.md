---
title: "SafelyGo, Week 1: an SOS button, a database, and a bug I had to prove"
project: safelygo
---

**What I did:**
I started my first mobile app, SafelyGo, a campus safety app for my BPA competition.
Before writing any code, I wrote a one-page plan of the app's features and rules.
Then I built the home screen with a big red SOS button. Tapping it opens an "Are you sure?" step,
and a demo mode makes sure it never calls 911 while I'm testing.
After that I connected a real database (Supabase) and added sign up, log in, log out, and password reset.

**What went wrong / what surprised me:**
- I created my database server in Mumbai by accident because I left the region on "Auto."
  You can't move it later, so I had to delete it and start over in the US.
- The password reset link kept opening "localhost" on my phone. My settings looked correct,
  so I tested the server with different links and found out it rejects links that use an IP address,
  which is exactly what my testing app uses. It wasn't my code. It works on the web version now.
- After signing out, the app showed an "Unmatched Route" error because it tried to open a screen that was locked.
  I fixed it by telling the app to send logged-out users to the sign-in screen.

**What I learned:**
- A git commit is like a save point in a game. I can always go back.
- Never put secret keys in your code. Mine live in a `.env` file that never gets uploaded.
- When something "should work" but doesn't, change one thing at a time and test until you find the cause.

**How it felt:**
Seeing my own app open on my phone for the first time was really cool.

**Next step:**
A contacts screen where you can tap a number to call, then safety reports and a real map.
