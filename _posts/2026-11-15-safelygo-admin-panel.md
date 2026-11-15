---
title: "SafelyGo: an admin panel, and why hiding a button is not security"
date: 2026-11-15 21:00:00 -0600
project: safelygo
topic: Security
---

**What I did:**
I built the admin panel for campus safety staff. An admin can see every report from every student,
filter them by status (Sent, In review, Resolved), open one to see the note, photo and location,
change its status, fix the type if the student picked the wrong one, and leave a staff note.
The student then sees the new status and the note under "My reports."

The list also updates by itself. When a student sends a new report, it shows up on the admin screen
without pulling down to refresh.

**Two accounts, two roles:**
To test it, I used two app accounts: a student account and an admin account named "Administrator."
Something I didn't understand at first: my Supabase dashboard login and an account inside my app are
different things, even with the same email. The dashboard account owns the database.
The app account is just a user of the app, so I had to sign up in the app separately.

An account only becomes an admin when I run this in the dashboard:

```sql
update public.profiles
set role = 'admin'
where id = (select id from auth.users where email = '<the account email>');
```

The app itself can never change anyone's role. Students can only edit their own name.

**The SQL behind the admin panel:**

Admins can read everyone's name (students still see only their own):

```sql
create policy "Admins read all profiles"
  on public.profiles for select
  to authenticated
  using ((select public.is_admin()));
```

I linked reports to profiles with a foreign key, so one query returns the report and the sender's name:

```sql
alter table public.reports
  add constraint reports_reporter_profile_fkey
  foreign key (reporter_id) references public.profiles (id) on delete cascade;
```

And I turned on Realtime for the reports table, so the app gets told when a report is added or changed:

```sql
alter publication supabase_realtime add table public.reports;
```

In the app, the admin screen subscribes to those changes and reloads the list (that's the Observer pattern),
and it unsubscribes when the screen closes. Realtime follows the same RLS rules,
so a student only hears about their own reports.

**Hiding a button is not security:**
Students don't see the Admin button, and the admin screens are blocked for them in the app's navigation.
But that's only for convenience. Someone could change the app's code and show the button anyway.
The real protection is in the database: every request goes through Row Level Security and `is_admin()`,
so even a modified app can't read or change other students' reports.

**What went wrong / what surprised me:**
- After I made my account an admin, the Admin button didn't appear. The app reads your role when you log in,
  so I had to log out and back in.
- "Hi Administrator" was too long and got cut off in the header. Now long titles shrink a little to fit.

**What I learned:**
- Decide permissions in the database, not just in the screens.
- Make important things (like who is an admin) impossible to change from the app at all.
- Realtime plus the Observer pattern makes the app feel alive without constant refreshing.

**Next step:**
The real map (my third-party API), then Guardian Mode with live location sharing.
