# 🚀 Quick Supabase Setup Guide

## Step 1: Create Supabase Project

1. Go to https://supabase.com
2. Sign up / Login
3. Click "New Project"
4. Fill in:
   - Project name: `grievance-redressal`
   - Database password: (save this!)
   - Region: Choose closest
5. Wait 2-3 minutes for setup

## Step 2: Get API Keys

1. In Supabase dashboard → **Settings** → **API**
2. Copy:
   - **Project URL**: `https://xxxxx.supabase.co`
   - **anon public key**: `eyJhbGc...` (long string)

## Step 3: Set Up Database

1. Go to **SQL Editor** (left sidebar)
2. Click **New query**
3. Copy and paste contents of `supabase/schema.sql`
4. Click **Run** (or Ctrl+Enter)
5. Copy and paste contents of `supabase/functions.sql`
6. Click **Run**

## Step 4: Configure Environment

Create `.env.local` in project root:

```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project-id.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key-here
```

## Step 5: Verify Setup

1. Go to **Table Editor** → Should see: `users`, `grievances`, `badges`
2. Run `npm run dev`
3. Visit http://localhost:3000
4. Try submitting a grievance!

## Troubleshooting

**"relation does not exist"**
→ Run `supabase/schema.sql` again

**Connection error**
→ Check `.env.local` has correct values

**Tables not showing**
→ Refresh Supabase dashboard

---

That's it! Your database is ready! 🎉

