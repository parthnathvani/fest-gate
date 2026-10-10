# Fest Gate

Campus event registration, digital QR passes and organizer check-in.

## Start

1. Install Node.js 20 or later.
2. Open a terminal in this folder and run `npm install` once.
3. Run `npm start`.
4. Open `http://localhost:3000`.

Sign in with Google using the Google button, or create a Student account with email and password. Google sign-in uses Firebase Authentication for project festgate-a1f30; add localhost to the Firebase Authentication authorized domains and enable Google as a provider in Firebase Console. The app exchanges Google credentials on the local server and issues an opaque app session. Organizer account creation is disabled unless the administrator sets `ORGANIZER_SIGNUP_CODE` in the private `.env` file. Existing Organizer accounts continue to sign in with their password. Organizer and student pages have different tools.

To authorize a new organizer, copy `.env.example` to `.env`, set a long private `ORGANIZER_SIGNUP_CODE`, restart the server, then share that code only with the intended organizer. Do not commit or share `.env`.

Organizers can download the application database as `fest-gate-database.csv`. It includes account names/roles, events, registrations, check-ins, activity, duplicate attempts and email statuses. Account passwords and password hashes are never exported.

## Email

The app generates sign-in alerts, student-login alerts to organizers, registration confirmations, organizer registration alerts, check-in receipts, 24-hour and 1-hour reminders, post-event thank-yous and duplicate-scan alerts. Each automation can be enabled or paused in Organizer → Automations. With no SMTP configuration, these are recorded as **Demo outbox · not sent** in the email log. To send real mail, copy `.env.example` to `.env`, add SMTP host, username, password and sender, then restart `npm start`. For Gmail, use an App Password. Keep `.env` private; do not share it.

Reminder automations check events in the background while the server is running. Email status is shown in the outbox. Generated codes and event data persist in `fest-gate-data.json` on this computer. The CSV export is built from that application database. Firestore cloud data storage is not yet connected: this project currently has only the Firebase web configuration, and a secure server-side Firestore connection still needs a private service-account credential configured locally. Do not paste or commit that private JSON/key.
