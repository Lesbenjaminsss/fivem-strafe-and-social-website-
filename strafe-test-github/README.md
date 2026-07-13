# STRAFE - Movement Speed Test

Chrome-based strafe test where you hold **SHIFT** and press **W-A-S-D** in order to earn points.

## Features

- Hold SHIFT + press W-A-S-D in sequence (+1 point per completion)
- Timer options: 15s, 30s, 1m, 2m, 3m
- Per-duration leaderboards (top 10)
- User registration with email verification
- IP tracking on scores and registrations
- Cyberpunk/neon UI with Aurora background, glassmorphism
- Custom mouse cursor effects (glow, trail, ripple, burst sparks, grid overlay)
- Firebase Firestore backend for persistent data

## Setup

### 1. Firebase

1. Create a project at [Firebase Console](https://console.firebase.google.com/)
2. Enable **Firestore Database** (start in test mode)
3. Go to **Project Settings** > Add Web App > Copy the config
4. Replace the placeholder values in `index.html`:

```js
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

5. Set Firestore rules (for testing only):

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

### 2. EmailJS (for email verification)

1. Create an account at [EmailJS](https://www.emailjs.com/)
2. Add an email service and create a template with variables: `{{code}}`, `{{to_email}}`, `{{user}}`
3. Replace the placeholder values in `index.html`:

```js
emailjs.init('YOUR_EMAILJS_PUBLIC_KEY');

// In sendVerificationCode():
emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', { ... });
```

### 3. Run

Open `index.html` with a local server (fetch API won't work with `file://`):

```bash
npx http-server . -p 3000
```

Then open http://localhost:3000

## Tech Stack

- Vanilla HTML/CSS/JS
- Firebase Firestore
- EmailJS
- Google Fonts (Exo 2 + Rajdhani)
