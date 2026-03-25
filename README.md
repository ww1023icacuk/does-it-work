# Does It Work? 🏫♿

A real-time accessibility status tracker for Imperial College London's South Kensington campus. Students and staff can report whether accessibility features (lifts, ramps, accessible toilets, hearing loops, etc.) are currently working, helping everyone navigate campus with confidence.

**Live site:** https://does-it-work-52f1d.web.app

---

## Features

- **Real-time sync** — reports from any user are instantly visible to everyone via Firebase Firestore
- **100+ accessibility features** across 22 buildings, sourced from AccessAble
- **QR codes** — generate and print a QR code for any feature; scanning leads to a quick yes/no reporting page
- **Search** — find any feature by name, building, or type
- **Crowdsourced confidence scoring** — time-decay weighted trust engine determines status from multiple reports
- **Comments** — users can leave notes with their reports; visibility configurable by admins
- **14-day report counts** — shows how recently and frequently each feature has been reported
- **Three themes** — Dark (default), Light, High Contrast; saved per browser
- **Campus dropdown** — ready for expansion to White City and Silwood Park campuses
- **Admin panel** — protected by Firebase Authentication (no password in source code)

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Single-file HTML/CSS/JS (no build step) |
| Database | Firebase Firestore (real-time) |
| Auth | Firebase Authentication (email/password) |
| Hosting | Firebase Hosting |
| QR codes | qrcodejs |

---

## Project Structure

```
Hackathon/
├── index.html           # Main application (all code in one file)
├── backup.html          # Backup copy of index.html
├── logo_does_it_work.png # App logo (shown in header)
├── firebase.json        # Firebase Hosting config
├── .firebaserc          # Firebase project binding
└── README.md            # This file
```

---

## Getting Started (Local Development)

No build step required. Open `index.html` directly in a browser, or serve it locally:

```bash
npx serve .
# or
python3 -m http.server 8080
```

Firebase features (real-time sync, auth) require a live internet connection.

---

## Deployment

```bash
firebase deploy --only hosting
```

Requires [Firebase CLI](https://firebase.google.com/docs/cli) and being logged in:

```bash
npm install -g firebase-tools
firebase login
```

---

## Admin Access

The admin panel is at `#/admin` (⚙️ button, visible only when logged in).

To set up admin credentials:
1. Go to [Firebase Console → Authentication](https://console.firebase.google.com/project/does-it-work-52f1d/authentication)
2. Enable the **Email/Password** provider
3. Add a user under the **Users** tab

Admin capabilities:
- Reset reports for individual features or all features
- Verify/override a feature's status
- Control comment visibility (public or admin-only)
- Upload a custom logo
- Import additional features via CSV/TSV

---

## Importing Feature Data

From the admin panel, drag and drop a TSV or CSV file with the following columns:

| # | Column |
|---|---|
| 1 | Fixture ID |
| 2 | Building |
| 3 | Building Area/Zone |
| 4 | Fixture Type |
| 5 | Fixture Subtype |
| 6 | Location Detail |
| 7 | Floor/Level |
| 8 | Access Type |
| 9 | Key Dimensions |
| 10 | Operational Notes |
| 11 | Condition/Status (`Operational` / `Out of Service` / `Not Available`) |
| 12 | Source URL |

---

## Firebase Collections

| Collection | Purpose |
|---|---|
| `reports` | Crowdsourced status reports per feature |
| `overrides` | Staff-verified status overrides |
| `app/shared` | Imported buildings, logo, comments visibility setting |

---

## Accessibility

- ARIA labels and roles throughout
- Keyboard navigable
- High Contrast theme available
- Designed for use on mobile (responsive, touch-friendly)
- Screen-reader friendly status badges

---

## Built at Imperial College London Hackathon
