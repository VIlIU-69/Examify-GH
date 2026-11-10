# Examify GH – free stack, Stage 1 (sign-in, saved papers, admin overview)
Cost: $0. Works on phone and PC. You need only a browser. No coding.

## Part 1 – Supabase (login + database)
1. Go to supabase.com, sign up, click **New project**. Name it `examify-gh`, set a database password (save it), pick the region closest to Ghana that is offered, create it, and wait until it finishes. On the Security options: keep **Enable Data API** ticked, leave **Automatically expose new tables** unticked, and tick **Enable automatic RLS**.
2. Open **SQL Editor** > **New query**. Paste everything from `schema.sql` > **Run**. It should say "Success".
3. Open **Project Settings > API** (or the "Connect" button). Copy two things: the **Project URL** and the **anon / publishable key**. (This key is meant to be public. Never copy the `service_role` / secret key anywhere.)
4. Open **Authentication > Sign In / Providers > Email**. For the pilot, switch **Confirm email OFF** so teachers can sign in straight away (Supabase's default email sending may be limited). Turn it back on before a public launch.

## Part 2 – Put your two keys in the app
5. Open `index.html` in any text editor. Near the bottom, replace `PASTE_YOUR_SUPABASE_URL` and `PASTE_YOUR_SUPABASE_ANON_KEY` with the two values (keep the quote marks). Save.

## Part 3 – GitHub, then Cloudflare Pages (hosting)
6. At github.com create a free account > **New repository** > name `examify-gh` > Create.
7. Click **uploading an existing file** and upload `index.html` (the one with your keys) > **Commit changes**.
8. At dash.cloudflare.com create a free account > **Workers & Pages** > **Create** > **Pages** > **Connect to Git** > pick `examify-gh`.
9. Framework preset: **None**. Leave Build command empty. Build output directory: `/` (or leave blank if it allows). **Save and Deploy**. (Cloudflare's menu wording can change slightly.)
10. In about a minute you get a link ending in `.pages.dev`. That is your live app. Open it on your phone and PC.

## Part 4 – Make yourself the admin
11. Open your live app > **Create an account** with your email.
12. In Supabase > **SQL Editor**, run (use your email):
    `update profiles set role='admin' where email='YOU@example.com';`
13. Sign out and sign in again. An **Admin** item now appears.

## Test checklist (5 minutes)
- Create a second account in a private window: it must NOT see Admin and must NOT see your papers.
- Add a paper, open it, delete it.
- Admin overview shows teacher count, active, saved papers.

## Later
Custom domain: buy one, add it in Cloudflare Pages > Custom domains. Stage 2: AI exam generation (Gemini key kept in a Cloudflare function, never in index.html).
