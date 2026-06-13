# Tavi — waitlist landing page

The public marketing + waitlist page for Tavi (food-first dating, Brooklyn).
Live at <https://kadenlee1107.github.io/tavi/> via GitHub Pages (branch `main`, root).

## What it does

A single static page (`index.html`, no build step). The signup form writes each
entry to the `public.waitlist` table in the Tavi Supabase project using the
**publishable** (anon) key. That key is safe to ship in client code — the table's
security comes from row-level security, not key secrecy:

- anyone may INSERT a signup (the row's shape is validated by the RLS policy), and
- nobody may SELECT/read the list except the Supabase dashboard / service role.

So the email list stays private even though the page is public.

## Where the signups go / how to read them

Supabase dashboard → **Table Editor** → `waitlist` (columns: `email`,
`neighborhood`, `source`, `created_at`). Use **Export → CSV** to download the list.
The website itself cannot read the list back.

## Editing the page

Edit `index.html`, then:

```bash
git add -A && git commit -m "update landing page" && git push
```

GitHub Pages redeploys within ~1–2 minutes.

## Attaching a custom domain later

Buy a domain, add a `CNAME` file here containing the domain, then set the DNS
records GitHub shows under repo **Settings → Pages → Custom domain**. No changes to
the page are needed — the form keeps working.

## Schema

The `waitlist` table is defined in the main Tavi repo at
`supabase/migrations/20260613000001_waitlist.sql`.
