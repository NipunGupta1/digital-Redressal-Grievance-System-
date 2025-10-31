# 📋 Step-by-Step Setup Guide

## Digital Grievance Redressal System with Geo Map & Badge System

Follow these steps to set up and run the application:

---

## ✅ Step 1: Verify Node.js Installation

Check if Node.js is installed:
```bash
node --version
npm --version
```

**Required**: Node.js 18+ and npm 9+

If not installed, download from: https://nodejs.org/

---

## ✅ Step 2: Install All Packages

The packages are already installed! But if you need to reinstall:

```bash
npm install
```

**Packages being installed:**
- ✅ Next.js 14 (React framework)
- ✅ React 18 & React DOM
- ✅ TypeScript
- ✅ Supabase Client (PostgreSQL database)
- ✅ Leaflet & React-Leaflet (maps)
- ✅ Tailwind CSS (styling)
- ✅ Axios (HTTP client)
- ✅ Lucide React (icons)
- ✅ And all other dependencies

---

## ✅ Step 3: Set Up Supabase Database

### Create Supabase Account & Project

1. **Sign Up:**
   - Go to https://supabase.com
   - Click "Start your project"
   - Sign up with GitHub, Google, or email (free account)

2. **Create New Project:**
   - Click "New Project"
   - Choose an organization (or create one)
   - Fill in project details:
     - **Name**: grievance-redressal-system (or any name)
     - **Database Password**: Create a strong password (save it!)
     - **Region**: Choose closest to you
   - Click "Create new project"
   - Wait 2-3 minutes for project to initialize

3. **Get Your API Keys:**
   - Once project is ready, go to **Settings** → **API**
   - Copy these values:
     - **Project URL** (looks like: `https://xxxxx.supabase.co`)
     - **anon public** key (long string starting with `eyJ...`)

---

## ✅ Step 4: Set Up Database Schema

1. **Open SQL Editor:**
   - In Supabase dashboard, click **SQL Editor** in the left sidebar
   - Click **New query**

2. **Create Tables:**
   - Copy the entire contents of `supabase/schema.sql`
   - Paste into SQL Editor
   - Click **Run** (or press Ctrl+Enter)
   - You should see "Success. No rows returned"

3. **Create Helper Functions:**
   - Copy the entire contents of `supabase/functions.sql`
   - Paste into SQL Editor
   - Click **Run**
   - You should see "Success. No rows returned"

4. **Verify Tables Created:**
   - Go to **Table Editor** in left sidebar
   - You should see three tables: `users`, `grievances`, `badges`

---

## ✅ Step 5: Configure Environment Variables

1. Create a file named `.env.local` in the root directory (same level as `package.json`)

2. Add your Supabase credentials:

```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project-id.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key-here
```

**Important Notes:**
- Replace `your-project-id` with your actual Supabase project ID
- Replace `your-anon-key-here` with your actual anon/public key
- The `NEXT_PUBLIC_` prefix is required for Next.js to expose these to the browser
- Never commit `.env.local` to git (it's already in `.gitignore`)

**Optional (for admin operations):**
```env
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
```
Get this from Settings → API → service_role key (keep this secret!)

---

## ✅ Step 6: Initialize Badges (Optional)

The badge system will auto-initialize when you first access it, but you can manually initialize:

1. Start the application (Step 7)
2. Navigate to the "Badges" tab
3. Click "Initialize Default Badges" button

Or initialize via API:
```bash
curl -X POST http://localhost:3000/api/badges
```

---

## ✅ Step 7: Run the Development Server

```bash
npm run dev
```

The application will start at: **http://localhost:3000**

Open your browser and navigate to `http://localhost:3000`

---

## ✅ Step 8: Test the Application

1. **Submit a Grievance:**
   - Click "Submit Grievance" tab
   - Fill in the form
   - Click on the map to select location
   - Submit

2. **View on Map:**
   - Click "Map View" tab
   - See your grievance marked on the map

3. **View All Grievances:**
   - Click "All Grievances" tab
   - Filter by status

4. **Check Badges:**
   - Click "Badges" tab
   - Earn badges by submitting grievances

---

## 🛠️ Technology Stack Used

| Technology | Purpose | Version |
|------------|---------|---------|
| **Next.js** | React framework (frontend + backend) | 14.0.4 |
| **React** | UI library | 18.2.0 |
| **TypeScript** | Type-safe JavaScript | 5.3.3 |
| **Supabase** | PostgreSQL database & backend | Latest |
| **@supabase/supabase-js** | Supabase client library | 2.38.5 |
| **Leaflet** | Interactive maps | 1.9.4 |
| **React-Leaflet** | React wrapper for Leaflet | 4.2.1 |
| **Tailwind CSS** | Utility-first CSS | 3.3.6 |
| **Axios** | HTTP client | 1.6.2 |
| **Lucide React** | Icon library | 0.294.0 |

---

## 📁 Project Structure

```
hackthon/
├── app/                    # Next.js app directory
│   ├── api/               # API routes (backend)
│   │   ├── auth/         # Authentication
│   │   ├── grievances/   # Grievance CRUD
│   │   └── badges/        # Badge management
│   ├── layout.tsx         # Root layout
│   ├── page.tsx           # Home page
│   └── globals.css        # Global styles
├── components/            # React components
│   ├── GrievanceMap.tsx   # Map visualization
│   ├── GrievanceForm.tsx  # Submit form
│   ├── GrievanceList.tsx  # List view
│   ├── BadgeDisplay.tsx   # Badge showcase
│   └── LocationPicker.tsx # Map location picker
├── types/                 # TypeScript types
│   └── database.ts        # Database type definitions
├── lib/                   # Utility functions
│   ├── supabase.ts       # Supabase client
│   └── badgeSystem.ts    # Badge logic
├── supabase/              # Database scripts
│   ├── schema.sql        # Database schema
│   └── functions.sql     # Helper functions
├── package.json          # Dependencies
├── tsconfig.json         # TypeScript config
├── tailwind.config.js    # Tailwind config
└── .env.local            # Environment variables (create this)
```

---

## 🐛 Troubleshooting

### Issue: "Cannot find module '@supabase/supabase-js'"
**Solution:** Run `npm install` again

### Issue: Supabase connection error
**Solution:** 
- Check `.env.local` file exists and has correct values
- Verify `NEXT_PUBLIC_SUPABASE_URL` starts with `https://`
- Verify `NEXT_PUBLIC_SUPABASE_ANON_KEY` is not empty
- Check Supabase project is not paused
- Restart the dev server after changing `.env.local`

### Issue: "relation does not exist" or table errors
**Solution:**
- Make sure you ran `supabase/schema.sql` in SQL Editor
- Verify tables exist in Table Editor
- Check table names match exactly (users, grievances, badges)

### Issue: Map not loading
**Solution:**
- Check browser console for errors
- Ensure internet connection (maps load from OpenStreetMap)
- Verify Leaflet CSS is loaded

### Issue: Port 3000 already in use
**Solution:**
```bash
# Kill process on port 3000
# Windows:
netstat -ano | findstr :3000
taskkill /PID <PID> /F

# macOS/Linux:
lsof -ti:3000 | xargs kill -9

# Or use a different port:
npm run dev -- -p 3001
```

### Issue: RPC function errors
**Solution:**
- Make sure you ran `supabase/functions.sql` in SQL Editor
- Verify functions exist: Go to Database → Functions in Supabase dashboard

---

## 🚀 Production Build

To build for production:

```bash
# Build the application
npm run build

# Start production server
npm start
```

**For Production Deployment:**
- Set environment variables in your hosting platform (Vercel, Netlify, etc.)
- Supabase free tier includes:
  - 500 MB database
  - 2 GB bandwidth
  - Unlimited API requests
  - Perfect for small to medium applications

---

## 📝 Next Steps (Future Enhancements)

- [ ] Add user authentication (Supabase Auth)
- [ ] Add file upload for attachments (Supabase Storage)
- [ ] Add email notifications (Supabase Edge Functions)
- [ ] Add admin dashboard
- [ ] Add real-time updates (Supabase Realtime)
- [ ] Add mobile app support

---

## 🔒 Security Notes

- Never commit `.env.local` to version control
- Keep `SUPABASE_SERVICE_ROLE_KEY` secret (only use server-side)
- Use Row Level Security (RLS) policies in Supabase for production
- Current setup allows all operations for development - tighten policies for production

---

## 📞 Support

If you encounter any issues:
1. Check the troubleshooting section
2. Verify all prerequisites are installed
3. Check Supabase project is active
4. Review browser console for errors
5. Check Supabase dashboard logs (Logs → API)

---

## 🎓 Supabase Resources

- [Supabase Documentation](https://supabase.com/docs)
- [Supabase Dashboard](https://app.supabase.com)
- [Supabase Discord Community](https://discord.supabase.com)

---

**Happy Coding! 🎉**
