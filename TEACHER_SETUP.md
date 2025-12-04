# Quick Setup Guide for Teachers

## 🚀 5-Minute Setup

### Step 1: Firebase Setup (2 minutes)

1. Go to https://console.firebase.google.com/
2. Click "Add Project" → Name it "SOL-Tracker" → Create
3. Click "Realtime Database" in sidebar → "Create Database"
4. Choose "europe-west1" → Start in "test mode" → Enable
5. Click ⚙️ (gear icon) → "Project settings"
6. Scroll to "Your apps" → Click `</>` icon
7. Name it "SOL Tracker" → Register app
8. **COPY the firebaseConfig code block**

### Step 2: Configure HTML File (1 minute)

1. Open `sol-tracker.html`
2. Find line ~641 (search for "firebaseConfig")
3. Replace the placeholder config with your copied config
4. **IMPORTANT:** Make sure `databaseURL` is included (looks like `https://your-project.firebaseio.com`)
5. Save the file

### Step 3: Deploy to GitHub (2 minutes)

1. Go to https://github.com/new
2. Name repository (e.g., "sol-tracker")
3. Make it Public or Private
4. Upload `sol-tracker.html`
5. Rename it to `index.html` (GitHub Pages requirement)
6. Go to Settings → Pages
7. Source: "Deploy from a branch" → Branch: "main" → Save
8. Your URL: `https://yourusername.github.io/sol-tracker/`

**Done!** Share the URL with students.

---

## 🔑 Student Login Info

Print this and give to students (or send via email):

```
=== SOL Progress Tracker Login ===
URL: [YOUR GITHUB PAGES URL]

User 001 (Finn):
  Username: user001
  Password: finn2025

User 002 (Ayca):
  Username: user002
  Password: ayca2025

User 003 (Raffaele):
  Username: user003
  Password: raffaele2025

User 004 (Max):
  Username: user004
  Password: max2025

User 005 (Moritz):
  Username: user005
  Password: moritz2025

User 006 (Emilia):
  Username: user006
  Password: emilia2025

Teacher View:
  Username: teacher
  Password: teacher2025
```

---

## 👀 Monitoring Students

### View Student Data in Firebase

1. Go to Firebase Console → Realtime Database
2. You'll see all student data updating in real-time:
   - `users/user001/stats/totalMinutes` - How long they've studied
   - `users/user001/journal/` - Their journal entries
   - `users/user001/tasks/` - What tasks they've completed
   - `users/user001/sessions/` - Individual study sessions

### Export All Data

You can export the entire database:
1. In Firebase Realtime Database
2. Click the three dots ⋮ next to your database URL
3. "Export JSON"
4. This gives you everything

### Teacher Dashboard

Login with:
- Username: `teacher`
- Password: `teacher2025`

Currently shows placeholder. To see real student data, you can:
1. Check Firebase Console directly (easiest)
2. Modify the teacher view in the HTML (more advanced)

---

## 🎯 What Students Can Do

1. **Track Study Time** - Start/stop timer, saves to database
2. **Complete Tasks** - Check off daily, weekly, specimen tasks
3. **Write Journal** - Document progress, tag entries (success/problem/help)
4. **Earn Badges** - 10 achievements unlock automatically
5. **See Progress** - Charts show weekly time, task completion
6. **Track Streak** - Daily study streak counter
7. **Export Data** - Download their own progress as JSON

---

## 🔧 Common Issues & Fixes

### Students can't login
- Check they're using correct username/password (case-sensitive)
- Verify Firebase is running (check Console)
- Check browser console (F12) for errors

### Data not saving
- Firebase rules might be blocking writes
- Go to Database → Rules tab
- For testing, use:
  ```json
  {
    "rules": {
      ".read": true,
      ".write": true
    }
  }
  ```
- ⚠️ This is open access - fine for testing, but set proper rules later

### Want to change passwords?
- Open `sol-tracker.html`
- Find `const USERS = {` (around line 670)
- Change the password values
- Save and re-upload to GitHub

### Want to customize tasks?
- Find `const TASK_TEMPLATES = {` (around line 855)
- Modify tasks for each student type
- Save and re-upload

---

## 📊 Advanced: Custom Teacher Dashboard

If you want to see student data in the teacher view, you can modify the HTML:

```javascript
// In loadTeacherView() function (around line 1437)
// Replace the placeholder with:

database.ref('users').on('value', (snapshot) => {
    const allUsers = snapshot.val() || {};
    
    // Display student stats
    Object.keys(allUsers).forEach(userId => {
        if (userId !== 'teacher') {
            const user = allUsers[userId];
            const stats = user.stats || {};
            
            // Show stats, journals, etc.
            console.log(`${userId}: ${stats.totalMinutes || 0} minutes studied`);
        }
    });
});
```

---

## 🎨 Customization Ideas

### Change Colors
Search for color codes in the HTML:
- `#667eea` - Primary purple
- `#764ba2` - Secondary purple
- `#27ae60` - Success green
- `#e74c3c` - Error red

### Add More Badges
In the `BADGES` array (around line 730), add:
```javascript
{
    id: 'custom-badge',
    icon: '🌟',
    name: 'Your Badge',
    description: 'Your requirement',
    requirement: (stats) => stats.yourCondition >= value
}
```

### Change Target Hours
In `calculateProgress()` function (around line 771):
```javascript
const targetHours = 40; // Change this number
```

---

## 📱 Mobile Access

Students can use this on phones/tablets:
- Same URL works everywhere
- Responsive design adapts to screen size
- Data syncs across all devices

---

## 🔐 Security for Production

When ready for real use:

### 1. Change All Passwords
Edit the HTML, change passwords to something students can't guess.

### 2. Set Firebase Rules
```json
{
  "rules": {
    "users": {
      "$userId": {
        ".read": "$userId === auth.uid || root.child('users/' + auth.uid + '/isTeacher').val() === true",
        ".write": "$userId === auth.uid"
      }
    }
  }
}
```

### 3. Enable Firebase Authentication (Optional)
For proper security, set up Firebase Auth:
- Email/password authentication
- Prevents direct database access
- More secure for production

---

## 📞 Need Help?

1. Check browser console (F12) for errors
2. Check Firebase Console for database issues
3. Review this guide
4. Check the detailed README.md

---

**Quick Reference:**
- Firebase Console: https://console.firebase.google.com/
- GitHub: https://github.com/
- Chart.js Docs: https://www.chartjs.org/

**Student Tracking at a Glance:**
- Total study time
- Task completion rates
- Journal entries (with tags for "need help")
- Streak tracking
- Badge achievements
- Weekly progress charts
