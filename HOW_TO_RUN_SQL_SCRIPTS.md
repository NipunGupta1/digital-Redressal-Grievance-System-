# 📝 How to Run SQL Scripts in Supabase - Detailed Guide

This guide will walk you through running the SQL scripts in Supabase SQL Editor step by step.

---

## 🎯 Prerequisites

- You have a Supabase account
- You have created a Supabase project
- Your project is fully initialized (usually takes 2-3 minutes)

---

## 📋 Step-by-Step Instructions

### **Step 1: Open Your Supabase Project**

1. Go to [https://app.supabase.com](https://app.supabase.com)
2. Log in to your account
3. Click on your project (the one you created for this application)

   **What you'll see:** The Supabase dashboard with a sidebar on the left

---

### **Step 2: Navigate to SQL Editor**

1. Look at the **left sidebar** in the Supabase dashboard
2. Find and click on **"SQL Editor"** (it has a `</>` icon)
   - It's usually in the middle section of the sidebar
   - You might need to scroll down if you don't see it immediately

   **What you'll see:** A new page with a SQL query editor interface

---

### **Step 3: Create a New Query**

1. In the SQL Editor page, look for a button that says:
   - **"New query"** (usually at the top)
   - OR a **"+"** button
   - OR a button with **"New"** text

2. Click on it to create a new blank query

   **What you'll see:** A blank SQL editor/text area where you can type SQL code

---

### **Step 4: Run the First Script (schema.sql)**

#### **4a. Open the schema.sql file**

1. In your code editor (VS Code, Cursor, etc.), open the file:
   ```
   supabase/schema.sql
   ```

2. **Select ALL the content** in the file:
   - **Windows/Linux:** Press `Ctrl + A` (or `Cmd + A` on Mac)
   - **Mac:** Press `Cmd + A`
   - OR manually select all text from the beginning to the end

3. **Copy the content:**
   - **Windows/Linux:** Press `Ctrl + C` (or `Cmd + C` on Mac)
   - **Mac:** Press `Cmd + C`
   - OR right-click → Copy

#### **4b. Paste into Supabase SQL Editor**

1. Go back to your Supabase browser tab
2. Click inside the SQL Editor text area (the blank space)
3. **Paste the content:**
   - **Windows/Linux:** Press `Ctrl + V` (or `Cmd + V` on Mac)
   - **Mac:** Press `Cmd + V`
   - OR right-click → Paste

   **What you'll see:** The entire SQL script pasted into the editor

#### **4c. Run the Script**

You have **TWO ways** to run the script:

**Method 1: Using the Run Button**
1. Look for a button that says:
   - **"Run"** (usually green or blue)
   - OR **"Execute"**
   - Usually located at the bottom-right or top-right of the editor
2. Click the **"Run"** button

**Method 2: Using Keyboard Shortcut**
1. **Windows/Linux:** Press `Ctrl + Enter`
2. **Mac:** Press `Cmd + Enter`

#### **4d. Verify Success**

After running, you should see:

✅ **Success Message:**
- A message saying: **"Success. No rows returned"**
- OR **"Success"** with a green checkmark
- OR something like: **"Query executed successfully"**

⚠️ **If you see an error:**
- Don't worry! Read the error message
- Common issues:
  - Tables already exist → This is OK, the script uses `IF NOT EXISTS`
  - Syntax error → Check if you copied the entire file correctly
  - Permission error → Make sure you're in the right project

---

### **Step 5: Run the Second Script (functions.sql)**

#### **5a. Clear the Editor (Optional but Recommended)**

1. In the SQL Editor, clear the previous query:
   - Select all (`Ctrl + A` or `Cmd + A`)
   - Press `Delete` or `Backspace`
   - OR click "New query" again to create a fresh one

#### **5b. Open and Copy functions.sql**

1. In your code editor, open the file:
   ```
   supabase/functions.sql
   ```

2. **Select ALL the content** (`Ctrl + A` or `Cmd + A`)

3. **Copy the content** (`Ctrl + C` or `Cmd + C`)

#### **5c. Paste and Run**

1. Go back to Supabase SQL Editor
2. **Paste** the content (`Ctrl + V` or `Cmd + V`)
3. **Run** the script:
   - Click **"Run"** button
   - OR press `Ctrl + Enter` (Windows/Linux) / `Cmd + Enter` (Mac)

#### **5d. Verify Success**

You should see:
- ✅ **"Success. No rows returned"** or similar success message

---

### **Step 6: Verify Tables Were Created**

1. In the Supabase sidebar, click on **"Table Editor"** (it has a table icon)
2. You should see **three tables**:
   - ✅ **users**
   - ✅ **grievances**
   - ✅ **badges**

3. Click on each table to see its structure:
   - You should see columns matching the schema we created

---

## 🎨 Visual Guide (What You'll See)

### **Supabase Dashboard Sidebar:**
```
📊 Dashboard
🔍 Table Editor     ← Click here to verify tables
📝 SQL Editor       ← Click here to run scripts
🔐 Authentication
📤 Storage
... (other options)
```

### **SQL Editor Interface:**
```
┌─────────────────────────────────────────┐
│  New query              [Run] [Save]     │
├─────────────────────────────────────────┤
│                                         │
│  [SQL Code Goes Here]                  │
│                                         │
│                                         │
└─────────────────────────────────────────┘
```

---

## 🔍 Troubleshooting

### **Problem: "relation already exists"**
**Solution:** This is normal! The script uses `IF NOT EXISTS`, so it won't create duplicates. Your tables are already there.

### **Problem: "permission denied"**
**Solution:** 
- Make sure you're logged into the correct Supabase account
- Verify you're in the right project
- Check that your project is fully initialized

### **Problem: Tables not showing**
**Solution:**
- Refresh the Table Editor page
- Go back to SQL Editor and run `schema.sql` again
- Check if there were any error messages

### **Problem: "syntax error"**
**Solution:**
- Make sure you copied the ENTIRE file (including all lines)
- Check for any extra characters or missing quotes
- Try copying the file content again

### **Problem: Script runs but nothing happens**
**Solution:**
- This is actually GOOD! "No rows returned" means success
- Check Table Editor to verify tables exist
- The script created tables, indexes, triggers, and policies

---

## ✅ Success Checklist

After completing all steps, verify:

- [ ] ✅ `schema.sql` ran successfully (showed "Success" message)
- [ ] ✅ `functions.sql` ran successfully (showed "Success" message)
- [ ] ✅ Can see `users` table in Table Editor
- [ ] ✅ Can see `grievances` table in Table Editor
- [ ] ✅ Can see `badges` table in Table Editor
- [ ] ✅ No error messages in SQL Editor

---

## 🚀 Next Steps

Once the SQL scripts are run successfully:

1. **Set up environment variables** (`.env.local` file)
2. **Run the application:** `npm run dev`
3. **Test the application:** Visit `http://localhost:3000`

---

## 💡 Pro Tips

1. **Save Your Queries:** After running, you can click "Save" to save the query for future reference
2. **Use Templates:** Supabase SQL Editor has templates - you can save these scripts as templates
3. **Check Logs:** If something goes wrong, check "Logs" in the sidebar to see detailed error messages
4. **Test Queries:** You can test individual queries by selecting just a portion and running it

---

## 📞 Need Help?

If you're stuck:
1. Check the error message carefully
2. Verify you copied the entire SQL file
3. Make sure your Supabase project is active (not paused)
4. Try refreshing the page and running again

---

**That's it! Your database is now set up! 🎉**

