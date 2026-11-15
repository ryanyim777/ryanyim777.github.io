---
title: "SafelyGo: a tap-to-call contact list, and SQL that decides who can change it"
project: safelygo
topic: Security
---


**What I did:**
I built the Contacts tab for SafelyGo. It lists emergency numbers, school offices, and help lines.
You tap a contact, and your phone opens the dialer with the number already filled in.

I didn't write the phone numbers inside the app's code.
I put them in my database instead, so a school admin can change a number without updating the app.
Then I wrote SQL rules so that every logged-in student can read the list, but only an admin can change it.

<!-- ![The Contacts tab with Emergency, School, and Support sections](/assets/images/safelygo/contacts-tab.png) -->

**The SQL, step by step:**

*1. The table.* Each contact has a name, a phone number, a short description, and a category.
`check` rules stop bad data. For example, the category can only be one of three words.

```sql
create table if not exists public.emergency_contacts (
  id          uuid primary key default gen_random_uuid(),
  name        text not null check (char_length(name) between 1 and 60),
  phone       text not null,
  category    text not null check (category in ('emergency', 'school', 'support')),
  sort_order  integer not null default 100,
  is_active   boolean not null default true
);
```

*2. "Is this person an admin?"* I wrote a small function that looks up the user's role.
Students can only read their own profile, so the function needs special permission
(`security definer`) to check the role for them.

```sql
create or replace function public.is_admin()
returns boolean
language sql stable security definer set search_path = ''
as $$
  select exists (
    select 1 from public.profiles
    where id = (select auth.uid()) and role = 'admin'
  );
$$;
```

*3. Row Level Security (RLS).* These rules run on every request.
Reading is open to logged-in users. Adding, editing, and deleting need `is_admin()` to be true.

```sql
create policy "Signed-in users can read contacts"
  on public.emergency_contacts for select
  to authenticated
  using (is_active or (select public.is_admin()));

create policy "Admins can insert contacts"
  on public.emergency_contacts for insert
  to authenticated
  with check ((select public.is_admin()));
```

*4. GRANT and RLS work together.* GRANT says *what* actions are possible (read, write, delete).
RLS says *who* can do them, row by row. I think of GRANT as the building pass and RLS as the lock on each room.
A request has to get past both.

*5. Starter data that is safe to run twice.* `where not exists` only adds the contacts if the table is empty,
so running the file again doesn't create copies.

I checked that it works: when I asked for the contacts while logged out, the database said "permission denied."

**What went wrong / what surprised me:**
- I wanted to use my real local area code to make the school numbers look real.
  Then I realized it would show where I live, and it could even be someone's real number.
  So I kept the fake 555-01xx numbers. They are saved for movies and TV, so nobody gets called by mistake.
- I moved the "make a phone call" code into its own class (`PhoneService`).
  Now the SOS button and the Contacts tab share it, so I only have to fix it in one place.
  It also blocks 911 while the app is in demo mode, so I can't call 911 by accident while testing.
- The linter caught a pattern in my screen code that can cause extra re-renders.
  I changed it so the screen only updates after the data arrives.

**What I learned:**
- Don't hardcode data that might change. Keep it in the database and let the right people edit it.
- Security has two layers here: what is allowed (GRANT) and who is allowed (RLS).
- Fake data is a privacy tool too.

**Next step:**
Safety reports with three categories, then an admin screen that reuses `is_admin()`.
