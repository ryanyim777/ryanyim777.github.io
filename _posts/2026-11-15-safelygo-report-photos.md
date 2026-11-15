---
title: "SafelyGo: adding photos to reports without making them public"
date: 2026-11-15 19:00:00 -0600
project: safelygo
topic: Security
---

**What I did:**
Students can now add a photo to a safety report. On the report form there are two buttons, Take photo and Choose photo.
You see a preview (and can remove it), and when you send the report, the photo goes with it.
Under "My reports" you can see a small version of the photo.

**Where the photo goes:**
Pictures don't go in the database table. They go in Supabase Storage, which is like a cloud folder (called a bucket).
The table only saves where the photo is, in a column called `photo_path`.

I made the bucket **private**. A private bucket has no public link at all.
When the app wants to show a photo, it asks for a temporary link that works for one hour,
and the storage rules check who is asking.

```sql
insert into storage.buckets (id, name, public, file_size_limit, allowed_mime_types)
values ('report-photos', 'report-photos', false, 5242880, array['image/jpeg']);
```

That also limits files to 5 MB and JPEG only.

**Storage rules (RLS for files):**
Every student uploads into a folder named after their own user ID.
`storage.foldername(name)[1]` is the first folder in the file path, so the rule just compares it to the logged-in user:

```sql
-- Upload: only into your own folder
with check (
  bucket_id = 'report-photos'
  and (storage.foldername(name))[1] = (select auth.uid())::text
)

-- View: your own photos, or everything if you're an admin
using (
  bucket_id = 'report-photos'
  and ((storage.foldername(name))[1] = (select auth.uid())::text or (select public.is_admin()))
)
```

There are no update or delete rules, so a photo can't be replaced or removed from the app. It's evidence.
I also changed the report rule so a report can only point to a photo inside the sender's own folder.
That way nobody can attach someone else's photo to their report.

**Making photos smaller (and more private):**
Phone photos are big. Before uploading, the app shrinks the photo to 1280 pixels wide and saves it again as a new JPEG.
It uploads faster on school Wi-Fi, and I don't ask the picker for the hidden photo data (like where it was taken).

**What I learned:**
- Files and table rows are stored in different places, but both need permission rules.
- "Private by default, temporary links to view" is a simple way to protect sensitive pictures.
- Test with boring photos. No faces, no addresses, nothing personal.

**Next step:**
The admin screen, where campus safety staff can see all reports (and photos) and update their status.
