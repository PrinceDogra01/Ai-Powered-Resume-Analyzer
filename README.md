# ResumeIQ

**AI Powered Resume Analyzer & ATS Scoring System**

ResumeIQ helps you analyze resumes with AI-driven ATS scoring, targeted improvements, skill gap insights, and role-matched recommendations.

## Prerequisites

- Node.js 18+
- Firebase project: `aceresume-5d09b`
- Gemini API key (Google AI Studio)

## Run locally

1. Install dependencies:
   ```bash
   npm install
   ```
2. Environment (already configured if `.env` exists):
   ```bash
   cp .env.example .env
   ```
   Set `GEMINI_API_KEY` in `.env`.
3. **Start the dev server** (required — otherwise you get `ERR_CONNECTION_REFUSED`):
   ```bash
   npm start
   ```
   Or: `npm run dev`

   Keep this terminal open while using the app.

4. Open [http://localhost:3000](http://localhost:3000) (browser may open automatically)

### `ERR_CONNECTION_REFUSED`?

This means nothing is listening on that port. Fix:

1. Open a terminal in the project folder.
2. Run `npm start` and wait for `VITE ready`.
3. Use **http://localhost:3000** (not 5173 unless Vite prints that port).
4. If port 3000 is busy, Vite will use the next free port — check the terminal output.

For the **production build** locally: `npm run build` then `npm run preview`.

## Firebase setup (one-time)

In [Firebase Console](https://console.firebase.google.com/project/aceresume-5d09b):

1. **Authentication** → Sign-in method → Enable **Google**
2. **Authentication** → Settings → Authorized domains → add `localhost` (and your custom domain if any)
3. **Firestore Database** → Create database (production mode) → deploy rules:
   ```bash
   npm run deploy:firestore
   ```

## Deploy to Firebase Hosting

1. Log in to Firebase CLI (first time only):
   ```bash
   npx firebase login
   ```
2. Build and deploy:
   ```bash
   npm run deploy
   ```
   Or hosting only:
   ```bash
   npm run deploy:hosting
   ```

Your live URL will be:

- **https://aceresume-5d09b.web.app**
- **https://aceresume-5d09b.firebaseapp.com**

After deploy, add these domains under **Authentication → Authorized domains** if Google sign-in fails.

## Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Local development |
| `npm run build` | Production build (`dist/`) |
| `npm run deploy` | Build + deploy hosting & Firestore rules |
| `npm run deploy:hosting` | Build + deploy hosting only |
| `npm run deploy:firestore` | Deploy Firestore security rules |
| `npm run lint` | TypeScript check |

## Project structure

| Path | Purpose |
|------|---------|
| `firebase-applet-config.json` | Firebase web app config |
| `.env` / `.env.production` | Gemini API key (gitignored) |
| `firestore.rules` | Firestore security rules |
| `firebase.json` | Firebase Hosting config |

## Security notes

- Never commit `.env` or share API keys publicly.
- Restrict your **Gemini API key** in [Google Cloud Console](https://console.cloud.google.com/) → APIs & Services → Credentials → HTTP referrers:
  - `http://localhost:3000/*`
  - `https://aceresume-5d09b.web.app/*`
  - `https://aceresume-5d09b.firebaseapp.com/*`
- Firebase client config in `firebase-applet-config.json` is public by design; access is enforced via Firestore rules and Auth.

---

© ResumeIQ. All rights reserved.
