# Open Stacks — Deployment Guide

## Stack
- **Frontend**: Static HTML (Vercel)
- **Database**: Supabase (books table)
- **Storage**: Supabase Storage (covers + PDFs)
- **Realtime**: Supabase Realtime (live sync across all readers)

---

## Step 1 — Supabase Setup

1. Go to [supabase.com](https://supabase.com) → your project
2. Open **SQL Editor** → paste the entire contents of `supabase_schema.sql` → **Run**
3. Go to **Project Settings → API**
4. Copy:
   - `Project URL` → you'll need this
   - `anon / public` key → you'll need this

---

## Step 2 — Add Your Keys

Open `public/index.html` and replace lines 2–3:

```js
const SUPABASE_URL = 'YOUR_SUPABASE_URL';       // e.g. https://xyzabc.supabase.co
const SUPABASE_ANON_KEY = 'YOUR_SUPABASE_ANON_KEY'; // eyJhbGci...
```

---

## Step 3 — Deploy to Vercel

### Option A — Vercel CLI (fastest)
```bash
npm i -g vercel
cd openstacks
vercel
# Follow prompts — framework: Other, root: ./
```

### Option B — GitHub + Vercel Dashboard
1. Push this folder to a GitHub repo
2. Go to [vercel.com](https://vercel.com) → **Add New Project**
3. Import the repo
4. Set **Root Directory** to `/` (or the folder name)
5. **Framework Preset**: Other
6. Deploy

---

## Step 4 — Add Environment Variables (optional but recommended)

Instead of hardcoding keys in the HTML, set them as Vercel env vars and use a build step. For a pure static site the inline approach works fine — Supabase anon keys are designed to be public.

---

## Adding Books After Deployment

- Hit **+** on the live site
- Fill in title, author, genre, year, pages, description
- Drop in a cover image (JPG/PNG) and PDF
- Click **Add Book**
- The book appears on **every open browser tab in real time** via Supabase Realtime

---

## File Structure

```
openstacks/
├── public/
│   └── index.html        ← entire app
├── supabase_schema.sql   ← run once in Supabase SQL Editor
├── vercel.json           ← routing config
└── README.md
```
