---
title: "SafelyGo"
summary: "A campus safety app for students: send an SOS, report safety concerns, call emergency contacts, and share your live location with people you trust."
status: "In progress"
timeline: "Nov 2026 – present"
order: 4
skills: [React Native, Expo, TypeScript, Supabase, OOP]
# cover: /assets/images/safelygo/cover.png
---

## Problem

When something goes wrong at school, like someone getting hurt, a stranger acting strange, or a broken stair,
students often don't know who to tell or how to tell them fast. And when students walk home alone,
their family or friends usually have no easy way to know they got there safely.

I wanted to build one simple app that helps with both: getting help fast in an emergency,
and letting the people you trust watch out for you.

I'm building SafelyGo for the BPA Virtual Mobile Applications event (2026–27). It's my first mobile app.

## Goals

| Requirement | Target | Actual |
|---|---|---|
| SOS | One button + one confirm → call 911, alert Guardians and the school | SOS button + confirm step working (demo mode, no real call) |
| Backend database | Supabase, with Row Level Security on every table | Connected |
| Accounts | Sign up, log in, log out, password reset | Done (phone reset waits for the web build) |
| Safety reports | 3 categories, optional photo/note, automatic location | Not started |
| Guardian Mode | Share location only during a "Watch Me" trip | Not started |
| Admin panel | Campus safety staff can review and manage reports | Not started |

## Design

**SOS is a big button, not a menu.** In an emergency there's no time to pick from a list.
One red button on the home screen, then one "Are you sure?" step so it can't go off by accident in a pocket.

**Only 3 report types.** Someone hurt, suspicious person, or unsafe place. Fewer choices means faster reports.
If a student picks the wrong one, school staff can change it later.

**Location is shared only during a trip.** In Guardian Mode, you start a "Watch Me" trip with a destination and an arrival time.
Your Guardians see your location only until you arrive. I think a safety app shouldn't track you all the time.

**Accessible by default.** Every message uses an icon, text, and color together, never color alone,
so people with color blindness can still understand it. Buttons are large and have screen-reader labels.

**Clean code structure.** Screens never talk to the database directly. They call a Service
(like `AuthService`), which uses a Repository (like `ProfileRepository`), which talks to Supabase.
This makes the code easier to change and to explain.

The app uses a made-up school, "Sunnyvale High," and the school name can be changed in one settings file.

## Build

- **Week 1 (Nov 11–13):** Planned the app, set up the project, built the SOS home screen,
  connected the Supabase database, and added sign up, log in, and password reset.

## What went wrong (and how I fixed it)

1. **Database server in the wrong country** → I left the region on "Auto" and it picked Mumbai, very far from my users
   → the region can't be changed, so I deleted the project and made a new one in the US East region
   → no harm done because there was no data yet. Lesson: never trust "Auto" for settings you can't change later.
2. **Password reset link opened "localhost" on my phone** → my settings looked right, so I tested the server
   with different links and found it rejects links that use an IP address, which is what Expo Go uses for testing
   → password reset works on the web version now, and it will work on phones after the web build is published.
3. **"Unmatched Route" after signing out** → the app tried to go to the home screen, which is locked when you're logged out
   → I told the locked screens where to send people instead (the sign-in screen).

## Results

Coming after mock judging (Dec 5) and final submission.

## What I'd do next

- Contacts tab (tap a number to call)
- Safety reports and a real map
- Admin panel for school staff
- Guardian Mode (the hardest part, so I'm doing it last)
