# 🔐 Authentication Setup Guide

This guide will help you set up authentication with Supabase Auth for the Grievance Redressal System.

## ✅ What's Been Added

1. **Login Page** (`/login`) - User and admin login
2. **Signup Page** (`/signup`) - User registration
3. **Admin Dashboard** (`/admin`) - Admin-only grievance management
4. **Protected Routes** - Automatic redirect to login if not authenticated
5. **Auth Context** - Global authentication state management
6. **Logout Functionality** - Secure session termination

## 🚀 Setup Steps

### Step 1: Enable Supabase Auth

1. Go to your Supabase project dashboard
2. Navigate to **Authentication** → **Providers** (left sidebar)
3. Enable **Email** provider (should be enabled by default)
4. Optionally configure:
   - **Email templates** - Customize welcome/reset emails
   - **Redirect URLs** - Add `http://localhost:3000` for development

### Step 2: Update Database Schema

Run the auth integration SQL script:

1. Go to **SQL Editor** in Supabase
2. Run `supabase/auth-integration.sql`:
   ```sql
   -- This makes password optional in users table
   -- And creates a trigger to sync auth.users with public.users
   ```

Or manually run:
```sql
ALTER TABLE users ALTER COLUMN password DROP NOT NULL;
```

### Step 3: Create Test Users

#### Option A: Via Signup Page (Recommended)
1. Visit `http://localhost:3000/signup`
2. Create accounts with different roles:
   - **Citizen**: `citizen@demo.com` / `demo123`
   - **Admin**: `admin@demo.com` / `demo123` (select Admin role)
   - **Officer**: `officer@demo.com` / `demo123` (select Officer role)

#### Option B: Via Supabase Dashboard
1. Go to **Authentication** → **Users**
2. Click **Add user** → **Create new user**
3. Enter email and password
4. After creating, go to **Table Editor** → `users` table
5. Find the user and set `role` to `admin` or `citizen`

### Step 4: Verify Email (Development)

For development, you can disable email confirmation:

1. Go to **Authentication** → **Settings**
2. Under **Email Auth**, toggle **Enable email confirmations** OFF
3. This allows immediate login without email verification

**For Production:** Keep email confirmations ON for security.

## 📝 Usage

### For Users (Citizens)
1. **Sign Up**: Visit `/signup` and create an account
2. **Login**: Visit `/login` and sign in
3. **Submit Grievances**: After login, you can submit grievances
4. **View Badges**: Check your earned badges
5. **Logout**: Click logout button in header

### For Admins
1. **Login**: Visit `/login` with admin credentials
2. **Admin Dashboard**: Click "Admin" tab or visit `/admin`
3. **Manage Grievances**:
   - View all grievances
   - Update status (pending → in-progress → resolved)
   - Add resolutions
   - Reject grievances
4. **View Statistics**: See dashboard stats

## 🔒 Security Features

- ✅ **Password Hashing**: Handled by Supabase Auth
- ✅ **Session Management**: Automatic token refresh
- ✅ **Protected Routes**: Unauthorized users redirected to login
- ✅ **Role-Based Access**: Admin-only pages protected
- ✅ **Secure Logout**: Clears session and tokens

## 🎨 User Roles

- **Citizen**: Can submit grievances, view badges
- **Officer**: Can view and manage assigned grievances
- **Admin**: Full access to all grievances and admin dashboard

## 🐛 Troubleshooting

### Issue: "User already registered"
**Solution**: User exists in Supabase Auth but not in `users` table. Run the auth-integration.sql trigger or manually create the user profile.

### Issue: Can't login after signup
**Solution**: 
- Check if email confirmation is required
- Verify user was created in `users` table
- Check browser console for errors

### Issue: Admin role not working
**Solution**: 
- Verify user's `role` field in `users` table is set to `admin`
- Clear browser cache and login again
- Check ProtectedRoute component logs

### Issue: "Invalid login credentials"
**Solution**:
- Verify email/password are correct
- Check if user exists in Supabase Auth (Authentication → Users)
- Try resetting password

## 📚 API Endpoints

### Authentication (Handled by Supabase Auth)
- `POST /api/auth/signup` - Not needed (using Supabase Auth directly)
- `POST /api/auth/login` - Not needed (using Supabase Auth directly)
- Sign in/up handled by `supabase.auth.signInWithPassword()` and `supabase.auth.signUp()`

### User Profile
- User profile fetched from `users` table automatically on login

## 🔄 Migration from Demo Users

If you were using demo users before:

1. **Clear localStorage**:
   ```javascript
   localStorage.removeItem('userId')
   ```

2. **Create account**: Use signup page
3. **Login**: Use login page
4. **Old demo users**: Can be cleaned up from database

## ✨ Features

- ✅ Email/Password authentication
- ✅ User registration with role selection
- ✅ Session persistence
- ✅ Automatic logout on token expiry
- ✅ Protected routes
- ✅ Role-based access control
- ✅ Admin dashboard
- ✅ User profile display

---

**Authentication is now fully integrated! 🎉**

