# Hosting Chit Fund Manager in the cloud (no laptop needed)

You need two free cloud services:

1. **Supabase** – hosts your PostgreSQL database **and** the API (no server to run).
2. **Vercel** (or Netlify) – hosts the app and gives you a public URL.

Once deployed, open the Vercel URL on your laptop and phone. Data is shared
across both devices because it lives in PostgreSQL, not the browser.

---

## Step 1 — Create the PostgreSQL database (Supabase)

1. Go to https://supabase.com and sign up (free).
2. Click **New Project**. Pick a name, a strong DB password, and a region near you.
3. Wait ~2 minutes for it to provision.
4. Open **SQL Editor** → **New query**.
5. Paste the contents of `supabase/schema.sql` and click **Run**.
6. New query again, paste `supabase/seed.sql`, click **Run**. (Optional demo data.)
7. Open **Project Settings → API** and copy:
   - **Project URL**  → this is `VITE_SUPABASE_URL`
   - **anon public key** → this is `VITE_SUPABASE_ANON_KEY`

## Step 2 — Put the code on GitHub

1. Create a free GitHub account if you don't have one.
2. Create a new empty repository.
3. Push this project to it:
   ```bash
   git init
   git add .
   git commit -m "Chit Fund Manager"
   git branch -M main
   git remote add origin https://github.com/<you>/<repo>.git
   git push -u origin main
   ```
   (The `.env` file is git-ignored, so your keys stay private.)

## Step 3 — Deploy the app (Vercel)

1. Go to https://vercel.com and sign in with GitHub (free).
2. **Add New → Project** and import your repo.
3. Framework preset: **Vite** (auto-detected). Build command `npm run build`,
   output dir `dist`.
4. Under **Environment Variables**, add:
   - `VITE_SUPABASE_URL` = your Project URL
   - `VITE_SUPABASE_ANON_KEY` = your anon public key
5. Click **Deploy**. In ~1 minute you get a URL like
   `https://chit-fund-manager.vercel.app`.

Open that URL on your laptop and phone. Done — always online, no laptop required.

---

## Running locally against PostgreSQL (optional)

1. Copy `.env.example` to `.env`.
2. Fill in `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`.
3. `npm run dev`.

If those env vars are missing, the app automatically runs in **offline
localStorage mode** (per-device data, no database) — handy for quick demos.

## How the app knows which backend to use

`src/data/supabaseClient.js` checks for the two env vars.
- Both present → PostgreSQL via Supabase (`src/data/supabaseStore.jsx`).
- Missing → localStorage (`src/data/store.jsx` LocalStoreProvider).

The screens are identical in both modes.

## Login
- Email: `admin@chitfund.com`
- Password: `admin123`

(This is a simple client-side check. For real multi-user security, switch to
Supabase Auth later.)
