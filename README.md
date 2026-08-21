# AZPARMADA Currency Exchange — PRD

## Original Problem Statement
Build a modern, professional, mobile-first, RTL Persian currency exchange rate management website for "AZPARMADA" currency exchange office. Two parts: (1) Public rate display (USD/EUR/TRY buy & sell in Toman, 6 direct conversion pairs, last-update timestamp, exchange calculator) and (2) Admin dashboard (secure JWT login, edit all rates, save, logout). Real backend + database + protected routes.

## Architecture
- **Frontend**: React 19 + React Router 7 + Tailwind + Shadcn UI + Sonner toasts, dir=rtl, Vazirmatn + JetBrains Mono fonts.
- **Backend**: FastAPI on port 8001, all routes prefixed `/api`.
- **DB**: MongoDB (motor async). Collections: `admins`, `exchange_rates` (single doc `_id="current"`).
- **Auth**: JWT (HS256, 12 h) with bcrypt password hashing. Bearer token in `Authorization` header; frontend stores in `localStorage[azparmada_token]`.
- **Seeding**: Startup seeds admin from `.env` (Safarzadeh / azparmada1355.) and default rates (USD 620k/625k, EUR 670k/675k, TRY 20500/21000, plus 6 conversions).

## User Personas
- **Public visitor**: Views live rates on mobile/desktop, uses calculator.
- **Admin (صرافی manager)**: Logs in and updates rates.

## Endpoints
- `GET /api/rates` — public
- `PUT /api/rates` — admin only
- `POST /api/auth/login` → `{token, admin}`
- `GET /api/auth/me` — verify token

## Implemented (2026-02)
- Public page with hero, live rates dashboard summary, 3 currency rate cards (Buy green #0B6E4F / Sell terracotta #D95C14), 6-pair conversion table, exchange calculator with swap.
- Admin login (split-screen with side art) with error toast for wrong creds.
- Admin dashboard: 3 stat cards, 6 toman inputs, 6 conversion inputs, sticky save bar with Persian success toast, refresh button, logout.
- RTL layout with Persian digit formatting, Persian datetime, tabular monospace numbers.
- JWT auth, bcrypt, protected `/admin` route, seed idempotent.

## Backlog (P1/P2)
- P1: Rate-change history log (audit trail)
- P1: Optional public marquee/ticker for headline pairs
- P2: Multi-admin management + role separation
- P2: Rate change % delta indicators (day over day)
