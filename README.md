# SOL Progress Tracker - A-Level German

A comprehensive student tracking and gamification system for self-organized learning (Selbstorganisiertes Lernen).

## 🎯 Features

### For Students:
- **Individual Login System** - Each student has a unique user ID and password
- **Real-time Progress Tracking** - Live updates across all devices
- **Study Timer** - Clock study sessions with automatic logging
- **Task Management** - Daily, weekly, and specimen paper tasks personalized per student
- **Learning Journal** - Document progress, challenges, and successes
- **Gamification & Badges** - 10 achievement badges to unlock
- **Visual Progress** - Charts showing weekly study time and task completion
- **Streak Tracking** - Daily study streak counter
- **Data Export** - Download all progress data as JSON

### For Teachers:
- **Teacher Dashboard** - Monitor all students at once
- **Real-time Updates** - See student activity as it happens
- **Journal Access** - Read student reflections and support requests

## 👤 Student Login Credentials

| User ID | Password | Student | Plan Type |
|---------|----------|---------|-----------|
| user001 | finn2025 | Finn | Structured |
| user002 | ayca2025 | Ayca | Turkish-German |
| user003 | raffaele2025 | Raffaele | Law & Economics |
| user004 | max2025 | Max | Accountability |
| user005 | moritz2025 | Moritz | Native Speaker |
| user006 | emilia2025 | Emilia | Philosophical |
| teacher | teacher2025 | Teacher | Teacher View |

## 🔧 Firebase Setup Instructions

### Step 1: Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add Project"
3. Enter project name (e.g., "SOL-Tracker")
4. Disable Google Analytics (optional)
5. Click "Create Project"

### Step 2: Create Realtime Database

1. In Firebase Console, click "Realtime Database" in left menu
2. Click "Create Database"
3. Select location (e.g., "europe-west1")
4. Start in **"Test mode"** for development (⚠️ Change to production rules later!)
5. Click "Enable"

### Step 3: Get Firebase Configuration

1. In Firebase Console, click the gear icon ⚙️ → "Project settings"
2. Scroll down to "Your apps"
3. Click the web icon `</>`
4. Register your app (enter nickname, e.g., "SOL Tracker")
5. Copy the `firebaseConfig` object

### Step 4: Configure the HTML File

Open `sol-tracker.html` and replace the Firebase configuration (around line 641):

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    databaseURL: "YOUR_DATABASE_URL",  // ⚠️ IMPORTANT - from Realtime Database
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

**Important:** Make sure the `databaseURL` matches your Realtime Database URL (found in the Realtime Database section).

### Step 5: Set Database Rules (Security)

1. In Firebase Console → Realtime Database → Rules tab
2. Replace with these rules:

```json
{
  "rules": {
    "users": {
      "$userId": {
        ".read": "auth == null || $userId === auth.uid || root.child('users').child(auth.uid).child('isTeacher').val() === true",
        ".write": "auth == null || $userId === auth.uid"
      }
    }
  }
}
```

**For development/testing**, you can use these open rules (⚠️ NOT for production):

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

### Step 6: Deploy

#### Option A: GitHub Pages
1. Create a new GitHub repository
2. Upload `sol-tracker.html` 
3. Rename to `index.html`
4. Enable GitHub Pages in repository settings
5. Access via: `https://yourusername.github.io/repository-name/`

#### Option B: Firebase Hosting
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
```

#### Option C: Local Testing
Simply open `sol-tracker.html` in any modern web browser.

## 📊 Data Structure

The Firebase Realtime Database uses this structure:

```
sol-tracker/
└── users/
    ├── user001/
    │   ├── stats/
    │   │   ├── totalMinutes: 0
    │   │   ├── completedTasks: 0
    │   │   ├── currentStreak: 0
    │   │   ├── earnedBadges: []
    │   │   ├── journalEntries: 0
    │   │   └── ...
    │   ├── sessions/
    │   │   └── [sessionId]/
    │   │       ├── date: "2025-01-15T10:30:00"
    │   │       └── minutes: 45
    │   ├── tasks/
    │   │   ├── daily/
    │   │   ├── weekly/
    │   │   └── specimen/
    │   ├── journal/
    │   │   └── [entryId]/
    │   │       ├── text: "Today I..."
    │   │       ├── tags: ["success"]
    │   │       └── date: "2025-01-15"
    │   └── lastStudyDate: "2025-01-15"
    └── user002/
        └── ...
```

## 🎖️ Achievement Badges

1. **🎯 Getting Started** - Complete your first study session
2. **⏰ Time Master** - Study for 5 hours total
3. **🔥 Week Warrior** - Study for 7 days in a row
4. **✅ Task Master** - Complete 20 tasks
5. **📅 Daily Disciplin** - Complete daily routine 10 times
6. **📝 Exam Ready** - Complete 3 specimen papers
7. **📔 Reflective Learner** - Write 15 journal entries
8. **🏃 Marathon Runner** - Study for 20 hours total
9. **💯 Perfectionist** - Complete all weekly tasks 3 weeks in a row
10. **🎓 A-Grade Ready** - Reach 80% overall progress

## 📝 Student-Specific Task Templates

Each student receives personalized tasks based on their learning plan:

### User 001 (Finn) - Structured Plan
- **Daily:** Vocabulary (15min) + Grammar (10min)
- **Weekly:** Essay, Reading, Listening practice
- **Specimen:** Papers every 2 weeks

### User 002 (Ayca) - Turkish-German
- **Daily:** Turkish-German Vocabulary (10min) + Grammar (15min)
- **Weekly:** Vocabulary trainer, Essay, Reading
- **Specimen:** Mock exams weeks 3, 5, 7

### User 003 (Raffaele) - Law & Economics
- **Daily:** Specialized vocabulary (20min) + Essay planning (15min)
- **Weekly:** Thematic essay, Vocabulary mastery, Literature analysis
- **Specimen:** Full paper sets weeks 4, 8

### User 004 (Max) - Accountability
- **Daily:** Grammar (15min) + Vocabulary (10min)
- **Weekly:** Intellectual essay, Text analysis, Debate prep
- **Specimen:** Strict Monday deadlines

### User 005 (Moritz) - Native Speaker
- **Daily:** Essay structure practice (15min)
- **Weekly:** Formal essay, Literature analysis, Writing workshop
- **Specimen:** Focus on formal writing

### User 006 (Emilia) - Philosophical
- **Daily:** Philosophical vocabulary (15min) + Critical reading (20min)
- **Weekly:** Philosophical essay, Literature study, Mind mapping
- **Specimen:** Mock exams weeks 4, 8

## 🎨 Design Features

- **Gradient Background** - Purple/blue gradient for visual appeal
- **Responsive Design** - Works on desktop, tablet, and mobile
- **Real-time Updates** - Firebase synchronization across devices
- **Clean UI** - Modern card-based layout
- **Color Coding** - Visual indicators for task status
- **Chart.js Integration** - Beautiful data visualizations

## 🔐 Security Notes

- Passwords are stored in client-side JavaScript (simple authentication)
- For production, implement proper Firebase Authentication
- Set appropriate database rules to restrict access
- Change default passwords immediately
- Consider HTTPS for production deployment

## 📱 Browser Compatibility

- ✅ Chrome/Edge (Recommended)
- ✅ Firefox
- ✅ Safari
- ✅ Mobile browsers

## 🆘 Troubleshooting

### "Error connecting to database"
- Check Firebase configuration is correct
- Verify databaseURL matches your Realtime Database
- Check browser console for error messages

### Data not saving
- Check Firebase Database rules allow write access
- Verify you're connected to the internet
- Check browser console for errors

### Charts not displaying
- Ensure Chart.js CDN is accessible
- Check browser console for JavaScript errors

### Timer not working
- Check browser permissions for JavaScript
- Refresh the page and try again

## 📧 Support

For issues or questions, contact your teacher or check:
- Firebase Console for database issues
- Browser Developer Tools (F12) for JavaScript errors
- GitHub repository for updates

## 📄 License

Educational use for ISN students.

---

**Version:** 1.0  
**Last Updated:** December 2024  
**Created by:** Michael for ISN A-Level German Students
