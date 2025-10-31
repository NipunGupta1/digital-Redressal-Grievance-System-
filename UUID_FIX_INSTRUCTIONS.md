# 🔧 UUID Error Fix Instructions

## Problem
You're getting this error:
```
invalid input syntax for type uuid: "demo-user-1761894486689"
```

## Cause
The application was generating demo user IDs like `demo-user-1761894486689`, but Supabase requires proper UUID format (like `550e8400-e29b-41d4-a716-446655440000`).

## Solution Applied
I've fixed the code to:
1. ✅ Generate proper UUIDs using `crypto.randomUUID()`
2. ✅ Create demo users in the database with valid UUIDs
3. ✅ Validate UUID format before database operations
4. ✅ Clear old invalid user IDs from localStorage

## What You Need to Do

### Step 1: Clear Browser Storage
The old invalid user ID is stored in your browser's localStorage. Clear it:

**Option A: Clear via Browser Console**
1. Open your browser's Developer Tools (F12)
2. Go to **Console** tab
3. Type and press Enter:
   ```javascript
   localStorage.removeItem('userId')
   ```
4. Refresh the page (F5)

**Option B: Clear via Application Tab**
1. Open Developer Tools (F12)
2. Go to **Application** tab (Chrome) or **Storage** tab (Firefox)
3. Expand **Local Storage**
4. Click on your domain
5. Find `userId` key and delete it
6. Refresh the page

**Option C: Clear All Site Data**
1. Open Developer Tools (F12)
2. Go to **Application** tab
3. Click **Clear site data** button
4. Refresh the page

### Step 2: Restart Development Server
```bash
# Stop the server (Ctrl+C)
# Then restart:
npm run dev
```

### Step 3: Test the Application
1. Open http://localhost:3000
2. The app will automatically create a new demo user with a valid UUID
3. Try submitting a grievance - it should work now!

## What Changed in the Code

### ✅ New Files Created:
- `lib/utils.ts` - UUID generation utility
- `app/api/auth/demo-user/route.ts` - Demo user creation endpoint

### ✅ Updated Files:
- `app/page.tsx` - Now creates real users in database with valid UUIDs
- `app/api/grievances/route.ts` - Added UUID validation
- `app/api/badges/route.ts` - Added UUID validation
- `lib/badgeSystem.ts` - Added UUID validation

## Verification

After clearing localStorage and restarting, check:

1. **Browser Console** - Should see no UUID errors
2. **Network Tab** - Check `/api/auth/demo-user` request returns a valid UUID
3. **Supabase Dashboard** - Go to Table Editor → `users` table → Should see new user with UUID format

## UUID Format Example

✅ **Valid UUID:**
```
550e8400-e29b-41d4-a716-446655440000
```

❌ **Invalid (old format):**
```
demo-user-1761894486689
```

## Still Having Issues?

If you still see the error:

1. **Clear localStorage again** (see Step 1 above)
2. **Check Supabase connection** - Verify `.env.local` has correct values
3. **Check browser console** - Look for any other error messages
4. **Verify database** - Make sure tables are created (run schema.sql)

---

**The fix is complete! Just clear localStorage and refresh! 🎉**

