# Digital Grievance Redressal System

A comprehensive digital grievance redressal system with geo-location mapping and badge/achievement system built with Next.js, TypeScript, Supabase (PostgreSQL), and Leaflet maps.

## Features

- 🗺️ **Geo Map Integration**: Interactive map using Leaflet to visualize grievance locations
- 🏆 **Badge System**: Achievement system that rewards users for their engagement
- 📝 **Grievance Management**: Submit, track, and manage grievances with status updates
- 🔍 **Location-based Tracking**: Select location on map for accurate grievance positioning
- 📊 **Status Filtering**: Filter grievances by status (pending, in-progress, resolved, rejected)
- 🎨 **Modern UI**: Beautiful, responsive interface built with Tailwind CSS

## Technology Stack

- **Frontend**: Next.js 14, React 18, TypeScript
- **Backend**: Next.js API Routes
- **Database**: Supabase (PostgreSQL)
- **Maps**: Leaflet & React-Leaflet
- **Styling**: Tailwind CSS
- **Icons**: Lucide React

## Step-by-Step Setup Guide

### Prerequisites

- Node.js 18+ installed
- Supabase account (free tier available)
- npm or yarn package manager

### Installation Steps

#### 1. Install Dependencies

```bash
npm install
```

This will install all required packages including:
- Next.js 14
- React 18
- TypeScript
- Supabase Client
- Leaflet & React-Leaflet
- Tailwind CSS
- And all other dependencies

#### 2. Set Up Supabase

1. **Create a Supabase Account:**
   - Go to [https://supabase.com](https://supabase.com)
   - Sign up for a free account
   - Create a new project

2. **Get Your API Keys:**
   - Go to Project Settings → API
   - Copy your `Project URL` and `anon/public` key

3. **Set Up Database Schema:**
   - Go to SQL Editor in Supabase dashboard
   - Run the SQL script from `supabase/schema.sql` to create tables
   - Run the SQL script from `supabase/functions.sql` to create helper functions

#### 3. Set Up Environment Variables

Create a `.env.local` file in the root directory:

```env
NEXT_PUBLIC_SUPABASE_URL=your-project-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
# Optional: For admin operations
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
```

Replace `your-project-url` and `your-anon-key` with your actual Supabase credentials.

If you prefer not to type these values manually, an example file and a helper script are included:

- `.env.local.example` — shows placeholder keys you can copy from.
- `scripts\create-env.ps1` — interactive PowerShell script that creates `.env.local` from your input (Windows PowerShell). Run it from the project root:

```powershell
cd E:\Buildingnewprojecteveryweek\hackthon
.\scripts\create-env.ps1
```

After creating `.env.local`, restart the dev server.

#### 4. Initialize Badges (Optional)

The badge system will auto-initialize when you first access the badges API endpoint, or you can manually initialize by clicking the "Initialize Default Badges" button in the Badges tab.

#### 5. Run the Development Server

```bash
npm run dev
```

The application will be available at `http://localhost:3000`

### Project Structure

```
├── app/
│   ├── api/              # API routes
│   │   ├── auth/        # Authentication endpoints
│   │   ├── grievances/  # Grievance CRUD operations
│   │   └── badges/       # Badge management
│   ├── layout.tsx        # Root layout
│   ├── page.tsx          # Main page
│   └── globals.css       # Global styles
├── components/
│   ├── GrievanceMap.tsx      # Map visualization
│   ├── GrievanceForm.tsx     # Submit grievance form
│   ├── GrievanceList.tsx     # List all grievances
│   ├── BadgeDisplay.tsx      # Badge showcase
│   └── LocationPicker.tsx    # Map location selector
├── models/
│   ├── User.ts          # User schema
│   ├── Grievance.ts     # Grievance schema
│   └── Badge.ts         # Badge schema
├── lib/
│   ├── db.ts            # Database connection
│   └── badgeSystem.ts   # Badge logic
└── package.json         # Dependencies
```

## Usage

### Submitting a Grievance

1. Click on "Submit Grievance" tab
2. Fill in the form:
   - Title (required)
   - Description (required)
   - Category (infrastructure, water-supply, etc.)
   - Priority (low, medium, high, urgent)
   - Location (click on map to select)
3. Click "Submit Grievance"

### Viewing Grievances

- **Map View**: See all grievances plotted on an interactive map
- **List View**: Browse all grievances with filtering options
- Click on map markers to see grievance details

### Badge System

Badges are automatically awarded when you:
- Submit your first grievance ("First Step")
- Submit 10 grievances ("Active Citizen")
- Submit 50 grievances ("Community Hero")
- Resolve 5 grievances ("Problem Solver")
- Submit 10 infrastructure-related grievances ("Infrastructure Expert")

## API Endpoints

### Grievances
- `GET /api/grievances` - Get all grievances (with optional query params: status, category, userId)
- `POST /api/grievances` - Create a new grievance
- `GET /api/grievances/[id]` - Get a specific grievance
- `PATCH /api/grievances/[id]` - Update a grievance

### Badges
- `GET /api/badges` - Get all badges (with optional userId query param)
- `POST /api/badges` - Initialize default badges

### Auth
- `POST /api/auth/register` - Register a new user

## Development Commands

```bash
# Development server
npm run dev

# Build for production
npm run build

# Start production server
npm start

# Lint code
npm run lint
```

## Troubleshooting

### Map not loading
- Ensure Leaflet CSS is loaded (check `app/layout.tsx`)
- Check browser console for errors
- Verify internet connection (maps load from OpenStreetMap)

### Supabase connection errors
- Verify `.env.local` file has correct `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY`
- Check Supabase project is active and not paused
- Verify database tables are created (run schema.sql in SQL Editor)

### Packages not installing
- Clear cache: `npm cache clean --force`
- Delete `node_modules` and `package-lock.json`, then run `npm install` again

## Next Steps

- Add user authentication (JWT)
- Add file upload for grievance attachments
- Add email notifications
- Add admin dashboard
- Add grievance assignment to officers
- Add real-time updates

## License

MIT

