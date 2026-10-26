# QALBU Modest Wear — Setup (Android-friendly)

## 1. Supabase connection
Open `index.html` in a text editor and replace these two values near the bottom:
- `PASTE_SUPABASE_PROJECT_URL_HERE` with `https://YOUR-PROJECT.supabase.co` (not the `/rest/v1/` address)
- `PASTE_SUPABASE_ANON_OR_PUBLISHABLE_KEY_HERE` with the **publishable** key from Supabase API settings.
Never use a `service_role` or secret key in this public file.

## 2. Database
In Supabase → SQL Editor → New query, run the contents of `supabase_setup.sql`. This version matches the `staff_profiles(user_id, role)` table used in the current setup and allows `staff` or `admin` roles.

## 3. Admin account
In Supabase → Authentication → Users, find the account and copy its User UID. In SQL Editor run (replace the example UUID):
`insert into public.staff_profiles (user_id, role) values ('YOUR-USER-UUID', 'admin') on conflict (user_id) do update set role='admin';`
Only trusted accounts should be added here. Do not create public staff sign-up.

## 4. Publish on GitHub Pages
Upload `index.html` to the root of the `qalbu-store` repository and commit. Repository → Settings → Pages → deploy from branch `main`, folder `/(root)`.

## 5. Manage products
Open the published website, go to Staff Login and sign in. Add/edit products, descriptions, prices and image URLs. For image URLs, use a direct public image URL. The current version uses image URLs rather than a built-in phone-gallery upload.

This is a product catalog with staff management, not a full checkout yet. Payment, orders, delivery and stock tracking are not included.
