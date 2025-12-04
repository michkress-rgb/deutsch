# 🔧 SOL Tracker - Troubleshooting Guide

## Common Issues & Solutions

### 🔴 Firebase Connection Issues

#### Issue: "Error connecting to database"
**Causes:**
- Firebase config not properly set up
- Database URL incorrect
- Firebase project not initialized

**Solutions:**
1. Open Firebase Console: https://console.firebase.google.com/
2. Check your project exists
3. Go to Realtime Database section
4. Copy the database URL (looks like: `https://your-project.firebaseio.com`)
5. In `sol-tracker.html`, find the `firebaseConfig` object
6. Make sure `databaseURL` is set correctly
7. Refresh the page

**Check in browser console (F12):**
```javascript
// You should see this message:
✅ Firebase initialized successfully
```

---

#### Issue: Data not saving to Firebase
**Causes:**
- Database rules blocking writes
- Network connection lost
- Firebase quota exceeded

**Solutions:**

1. **Check Database Rules:**
   - Firebase Console → Realtime Database → Rules tab
   - For testing, use:
   ```json
   {
     "rules": {
       ".read": true,
       ".write": true
     }
   }
   ```
   - Click "Publish"

2. **Check Network:**
   - Open browser console (F12) → Network tab
   - Look for failed requests to Firebase
   - Make sure you're online

3. **Check Quota:**
   - Firebase Console → Usage tab
   - Free tier: 10GB downloads/month, 1GB stored
   - If exceeded, upgrade plan

---

### 🔴 Login Issues

#### Issue: "Incorrect password" even with correct password
**Causes:**
- Case sensitivity (passwords are case-sensitive)
- Extra spaces in password
- Wrong user selected

**Solutions:**
1. Check you selected correct User ID from dropdown
2. Passwords are case-sensitive: `finn2025` ≠ `Finn2025`
3. Don't add spaces before/after password
4. If still failing, ask teacher to verify password in HTML file

**Teacher: Change password in HTML:**
```javascript
// Find this section in sol-tracker.html (around line 670)
const USERS = {
    'user001': {
        password: 'finn2025',  // Change this
        // ...
    }
}
```

---

### 🔴 Timer Issues

#### Issue: Timer not starting
**Causes:**
- JavaScript error
- Page not fully loaded
- Browser blocking scripts

**Solutions:**
1. Refresh the page (Ctrl+R or Cmd+R)
2. Check browser console (F12) for errors
3. Make sure JavaScript is enabled in browser settings
4. Try a different browser (Chrome/Edge recommended)

---

#### Issue: Timer stops unexpectedly
**Causes:**
- Internet connection lost
- Browser went to sleep
- Tab backgrounded on mobile

**Solutions:**
1. Keep the tab active while timing
2. Don't let device go to sleep during session
3. If stopped, restart timer
4. Session saves when you click "Save Session"

---

#### Issue: "Session too short" error
**Cause:**
- Trying to save session under 1 minute

**Solution:**
- Study for at least 1 minute before saving
- This prevents accidental logging

---

### 🔴 Task Issues

#### Issue: Tasks won't check off
**Causes:**
- Firebase write rules
- Network delay
- Page needs refresh

**Solutions:**
1. Wait 2-3 seconds and try again
2. Refresh the page
3. Check Firebase connection (see Firebase issues above)
4. Check browser console for errors

---

#### Issue: Tasks reset unexpectedly
**Causes:**
- Browser cache cleared
- Different device
- Database reset by teacher

**Solutions:**
1. Tasks are stored in Firebase, not locally
2. Same user can access from any device
3. If reset, check with teacher (might be intentional)
4. Check Firebase Console → Realtime Database to see current data

---

### 🔴 Journal Issues

#### Issue: Journal entries not saving
**Causes:**
- Empty text field
- Firebase connection lost
- Database rules

**Solutions:**
1. Make sure you've written something (can't save empty entry)
2. Check Firebase connection
3. Try saving again after a few seconds
4. Check browser console for errors

---

#### Issue: Can't see past journal entries
**Causes:**
- No entries created yet
- Firebase not loading data
- Display limit (shows last 10)

**Solutions:**
1. Scroll down in journal section
2. If completely empty, you haven't created entries yet
3. Refresh the page
4. Check Firebase Console to see if entries exist

---

### 🔴 Badge Issues

#### Issue: Badges not unlocking
**Causes:**
- Requirements not met
- Stats not updating
- Badge check not running

**Solutions:**
1. Check badge requirements (see STUDENT_GUIDE.md)
2. Verify your stats meet requirements
3. Refresh the page to trigger badge check
4. Badges update after completing activities

**Badge Requirements:**
- 🎯 Getting Started: 1 study session
- ⏰ Time Master: 5 hours (300 minutes)
- 🔥 Week Warrior: 7-day streak
- ✅ Task Master: 20 tasks
- 📅 Daily Disciplin: 10 daily completions
- 📝 Exam Ready: 3 specimen papers
- 📔 Reflective Learner: 15 journal entries
- 🏃 Marathon Runner: 20 hours (1200 minutes)
- 💯 Perfectionist: 3 perfect weeks
- 🎓 A-Grade Ready: 80% progress

---

### 🔴 Chart Issues

#### Issue: Charts not displaying
**Causes:**
- Chart.js CDN not loading
- No data to display
- JavaScript error

**Solutions:**
1. Check internet connection
2. If no data, complete some activities first
3. Refresh the page
4. Check browser console for errors
5. Try different browser

---

#### Issue: Charts show incorrect data
**Causes:**
- Data still syncing
- Time zone differences
- Browser cache

**Solutions:**
1. Wait a few seconds for Firebase to sync
2. Refresh the page
3. Clear browser cache and reload
4. Check Firebase Console for actual data

---

### 🔴 Progress Bar Issues

#### Issue: Progress bar stuck at 0%
**Causes:**
- No activities completed yet
- Stats not calculating
- Firebase not updating

**Solutions:**
1. Complete some activities (study session, tasks, etc.)
2. Refresh the page
3. Check that stats are updating in Firebase

**Progress Calculation:**
- 50% from study time (target: 40 hours)
- 30% from tasks (target: 50 tasks)
- 20% from streak (target: 30 days)

---

### 🔴 Streak Issues

#### Issue: Streak not incrementing
**Causes:**
- Studied same day (doesn't increment twice)
- Didn't save study session
- Time zone issues

**Solutions:**
1. Streak updates once per day
2. Must complete a study session (start timer + save)
3. Check `lastStudyDate` in Firebase Console
4. Streak resets if you miss a day

---

#### Issue: Streak reset unexpectedly
**Causes:**
- Missed a day
- Time zone midnight passed
- Database reset

**Solutions:**
1. Streaks reset if you don't study for a day
2. Study every day to maintain streak
3. Even 10 minutes counts!

---

### 🔴 Export Issues

#### Issue: Export button not working
**Causes:**
- Browser blocking download
- No data to export
- JavaScript error

**Solutions:**
1. Allow downloads in browser settings
2. Check pop-up blocker settings
3. Try different browser
4. Check console for errors

**Manual Export:**
1. Go to Firebase Console
2. Realtime Database → Your data
3. Click three dots ⋮ → "Export JSON"

---

### 🔴 Mobile Issues

#### Issue: Layout broken on mobile
**Causes:**
- Old browser
- Zoom level
- Screen too small

**Solutions:**
1. Update mobile browser
2. Reset zoom to 100%
3. Use portrait orientation
4. Try desktop site if needed

---

#### Issue: Timer stops when screen locks
**Causes:**
- Mobile OS suspends background tabs
- Battery saver mode

**Solutions:**
1. Keep screen on during study session
2. Disable battery saver temporarily
3. Use desktop for long sessions
4. Timer state should save when you return

---

### 🔴 Browser-Specific Issues

#### Chrome/Edge
- Usually works best
- Clear cache: Ctrl+Shift+Delete

#### Firefox
- May need to allow Firebase in settings
- Clear cache: Ctrl+Shift+Delete

#### Safari
- May block third-party cookies
- Settings → Privacy → Uncheck "Block all cookies"
- Clear cache: Cmd+Option+E

#### Mobile Browsers
- Use Chrome or Safari on mobile
- Enable JavaScript
- Allow cookies

---

### 🔴 Network Issues

#### Issue: "Network error" or slow loading
**Causes:**
- Slow internet
- Firebase server issues
- Firewall blocking Firebase

**Solutions:**
1. Check internet speed
2. Try different network
3. Check Firebase status: https://status.firebase.google.com/
4. If behind school firewall, ask IT to whitelist:
   - `*.firebaseio.com`
   - `*.firebase.com`

---

### 🔴 For Teachers: Admin Issues

#### Issue: Can't see all student data
**Causes:**
- Teacher view not fully implemented
- Database rules blocking access

**Solutions:**
1. Use Firebase Console for now:
   - Go to Realtime Database
   - Browse user data directly
2. To implement full teacher view:
   - Modify `loadTeacherView()` function
   - Add code to loop through all users
   - Display aggregated stats

**Quick Teacher Dashboard:**
```javascript
// Add to loadTeacherView() function
database.ref('users').on('value', (snapshot) => {
    const users = snapshot.val() || {};
    console.log('All student data:', users);
    // Display as needed
});
```

---

#### Issue: Need to reset student data
**Causes:**
- Testing
- Student made errors

**Solutions:**

1. **Reset Individual Student:**
   ```javascript
   // In Firebase Console → Realtime Database
   // Navigate to users/user001
   // Click three dots → Delete
   // Then import fresh data from firebase-init.json
   ```

2. **Reset All Data:**
   ```javascript
   // In Firebase Console → Realtime Database
   // Click three dots on root
   // Import firebase-init.json
   ```

---

#### Issue: Need to change passwords
**Location in code:** Line ~670 in `sol-tracker.html`

**Steps:**
1. Open `sol-tracker.html` in editor
2. Find `const USERS = {`
3. Change password values
4. Save file
5. Re-upload to GitHub/hosting

---

### 🔴 Performance Issues

#### Issue: Page loading slowly
**Causes:**
- Too much data in database
- Slow internet
- Images/charts loading

**Solutions:**
1. Clear browser cache
2. Close other tabs
3. Check internet speed
4. Firebase free tier is fast enough for 6 students

---

#### Issue: Charts updating slowly
**Causes:**
- Chart.js recalculating
- Large dataset

**Solutions:**
1. Wait a few seconds
2. Refresh page
3. Normal behavior for real-time updates

---

## 🔍 Debugging Tools

### Browser Console (F12)
**How to use:**
1. Press F12 (or right-click → Inspect)
2. Go to "Console" tab
3. Look for errors (red text)
4. Copy error message

**Common messages:**
- ✅ `Firebase initialized successfully` - Good!
- ❌ `Firebase initialization error` - Check config
- ❌ `Permission denied` - Check database rules

### Firebase Console
**What to check:**
1. **Realtime Database:**
   - See live data
   - Check if updates happening
   - Verify structure

2. **Usage:**
   - Check if quota exceeded
   - Monitor active connections

3. **Rules:**
   - Verify read/write permissions

### Network Tab
**How to use:**
1. F12 → Network tab
2. Reload page
3. Look for:
   - Red items (failed requests)
   - Firebase requests
   - Loading times

---

## 🆘 Still Having Issues?

### For Students:
1. Try different browser
2. Clear cache and cookies
3. Check with classmate if they have same issue
4. Write in journal with 🆘 tag
5. Email teacher

### For Teachers:
1. Check Firebase Console first
2. Check browser console (F12)
3. Verify config is correct
4. Test with different user account
5. Check GitHub repository for updates

### Emergency Solutions:
1. **Complete reset:**
   - Delete Firebase project
   - Create new one
   - Start fresh setup

2. **Backup plan:**
   - Use spreadsheet tracking temporarily
   - Student manual logs
   - Import to Firebase later

---

## 📋 Pre-Launch Checklist

Before giving to students:

- [ ] Firebase project created
- [ ] Realtime Database enabled
- [ ] Config in HTML file updated
- [ ] Test rules set (can change later)
- [ ] Deployed to GitHub Pages
- [ ] Tested login with each user ID
- [ ] Timer works and saves
- [ ] Tasks can be checked off
- [ ] Journal entries save
- [ ] Charts display
- [ ] Mobile version works
- [ ] Printed reference cards ready

---

## 📞 Getting More Help

**Resources:**
- Firebase Docs: https://firebase.google.com/docs/database
- Chart.js Docs: https://www.chartjs.org/docs
- GitHub Pages: https://pages.github.com/
- MDN Web Docs: https://developer.mozilla.org/

**Check the HTML comments:**
The code has extensive comments explaining each function.

**Community:**
- Stack Overflow for Firebase questions
- GitHub Issues for this project

---

**Version:** 1.0  
**Last Updated:** December 2024

*Most issues can be solved by refreshing the page, checking internet connection, or verifying Firebase configuration. When in doubt, check the browser console!*
