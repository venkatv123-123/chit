# Chit Fund Manager

A mobile-first chit fund management app built from the provided mockups. It runs entirely in the browser with **no database server required** — all data is stored in the browser's `localStorage` and seeded from the mockup content.

## Screens
1. Login
2. Dashboard (stats, payment status donut, collection table)
3. Chits List (+ Add Chit)
4. Chit Details (Members / Payments / Messages / Reports tabs)
5. Member Profile (participation, financial summary, history)
6. Payment Details (verify payment, WhatsApp reminder, status timeline)
7. WhatsApp Messages (templates + history)
8. Reports (with CSV/Excel export)
9. Settings (business info, automation toggles, logout, reset data)

## Tech
- React 18 + Vite
- React Router
- Tailwind CSS
- localStorage as the data store (no backend / DB needed)

## Run locally
```bash
npm install
npm run dev
```
Then open the URL Vite prints (default http://localhost:5173).

## Demo login
- Email: `admin@chitfund.com`
- Password: `admin123`

## Data
- Data persists in your browser via `localStorage`.
- Use **Settings → Reset demo data** to restore the original seed.

## Where the data lives
- Seed data: `src/data/seed.js`
- Store / actions: `src/data/store.jsx`

## Swapping in a real backend later
All reads go through `useStore()` and all writes through its action methods
(`addChit`, `addMember`, `markPaid`, etc.). To move to a real DB/API later,
replace the bodies of those methods with network calls — the screens stay the same.
