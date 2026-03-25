# mybudget — by Danai

Personal finance tracker with multi-user authentication, built as a single HTML file powered by Firebase.

## Features

- **Monthly tracker** — log expenses, income, and transfers between accounts. Compare actuals vs budget targets per category with visual progress indicators.
- **Yearly overview** — month-by-month breakdown by category, YTD totals, and income vs expenses chart.
- **Quarterly review** — Q1 summary with spending breakdown, monthly trend, and category performance vs annual targets.
- **Investment portfolio** — track ETF holdings, cost basis, current value, P&L, and allocation chart.
- **Multi-user** — each account has isolated data stored in Firebase Firestore. Sign up with email/password.
- **Persistent storage** — data syncs to Firebase and is accessible from any device.

## Tech stack

- Vanilla HTML / CSS / JavaScript — no build step, no framework
- [Firebase](https://firebase.google.com/) (Auth + Firestore) for authentication and data storage
- [Chart.js](https://www.chartjs.org/) for charts
- [Cormorant Garamond](https://fonts.google.com/specimen/Cormorant+Garamond) + [DM Sans](https://fonts.google.com/specimen/DM+Sans) via Google Fonts

## Setup

### 1. Firebase project

1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Create a new project (e.g. `mybudget-d`)
3. **Authentication** → Get started → Sign-in method → **Email/Password** → Enable → Save
4. **Firestore Database** → Create database → Production mode → `europe-west3` → Done

### 2. Firestore security rules

In Firestore → Rules tab, replace the default rules with:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null
        && request.auth.uid == userId;
    }
  }
}
```

### 3. Firebase credentials

The `firebaseConfig` object in `index.html` is already populated for this project. If you fork this for a different Firebase project, replace it with your own config from:

> Project settings (⚙️) → Your apps → Web app → SDK setup and configuration

### 4. Deploy to GitHub Pages

1. Create a new GitHub repository
2. Upload `index.html` (rename from `mybudget.html` if needed)
3. Go to **Settings → Pages → Branch: main → Save**
4. Your app will be live at `https://<username>.github.io/<repo-name>`

### 5. Authorize your domain

In Firebase Console → Authentication → Settings → **Authorized domains** → Add domain:

```
<username>.github.io
```

Without this step, Firebase will block login requests from GitHub Pages.

## Usage

- Open the app URL and click **Create account** to register with your email and password
- Each user's data is completely separate
- Account balances, transactions, income, targets, and investments are all saved automatically after each change

## Accounts tracked

`ΕΒ1` · `ΕΒ2` · `Alpha Bank` · `Freedom` · `Piraeus` · `Cash` · `Προθεσμιακή` · `Pre Paid`

## Expense categories

**Needs:** Rent · Utilities · Supermarket · Transportation · Healthcare · Kids · Kindergarten · Loucy

**Wants:** Delivery · Shopping · Hobbies · Subscriptions · Gifts · Entertainment · Education · Unbudgeted

**Savings & investments:** ETF · Emergency Fund · EB2 savings · Children Fund

## Local development

No build step needed. Open `index.html` directly in a browser — note that Firebase Auth blocks `localhost` by default in projects created after April 2025. Add `localhost` to your authorized domains in Firebase Console if you want to test locally.

---
