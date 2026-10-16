# Safarni — Travel Discovery & Booking Frontend

A collaborative travel-booking web application built during the **Huma-volve Front-End Internship**. Safarni brings together tour discovery, hotel browsing, car rentals, interactive maps, user accounts, and booking/checkout interfaces in a React application connected to a Laravel API.

> **Project status:** This repository contains the React frontend from a team internship project. The original API service may be unavailable, so dynamic features might not work on the current hosted URL. A fully interactive **MSW portfolio demo** is proposed, but **has not yet been implemented**. No booking or payment made through an eventual demo should be treated as real.

## Application overview

- **Tour discovery:** Browse recommended/popular tours, inspect details and availability, search/filter by category, location, price and rating, and compare tours.
- **Car rental:** Browse vehicles, open details, select dates, and enter booking/checkout flows.
- **Hotels and rooms:** Responsive hotel and room browsing screens, with booking-related pages.
- **Authentication and profiles:** Login, registration, form validation, password recovery/OTP screens, account/profile workflows, and integration points for Google sign-in.
- **Maps:** Leaflet-based map views and location-related interfaces.
- **Checkout:** Booking and payment UI, with Stripe client integration in the original implementation. Payment completion depends on the external backend and Stripe setup; no production-payment claims are made here.

Availability of these features depends on whether the corresponding backend services and integrations are running. Some hotel content is currently frontend/static.

## Technology stack

| Area | Technologies |
| --- | --- |
| Application | React 19, TypeScript, Vite 6 |
| UI | Tailwind CSS, Radix UI, Lucide React, Swiper, Lottie |
| Data / forms | TanStack Query, Axios, React Hook Form, Formik, Yup, Zod |
| Maps | Leaflet, React-Leaflet |
| Navigation | React Router |
| Integration | Google OAuth client, Stripe client libraries, Laravel REST APIs |

## My contributions — Mohamed Nasr

This is a **team project**, not a solo implementation. My documented Git contributions primarily cover:

- Developed and integrated **login, registration, forgot-password, verification and password-reset frontend workflows** with existing REST APIs.
- Integrated **Google OAuth UI** and refined API error handling and unauthorized-session behavior.
- Improved **form validation feedback**, sign-up and password-reset styling, authentication navigation and responsive layouts.
- Added **Lottie animations** and other onboarding/authentication UI enhancements.
- Contributed to dependency/type-safety maintenance and resolving cross-team integration issues.

Selected evidence from the team's repository:

- [Authentication PR #3](https://github.com/Huma-volve/round-5-front-Safarni/pull/3)
- [Authentication PR #5](https://github.com/Huma-volve/round-5-front-Safarni/pull/5)
- [Authentication PR #6](https://github.com/Huma-volve/round-5-front-Safarni/pull/6)

Other travel/booking features were developed collaboratively by the internship team; this README does not attribute all those features to one developer.

## Architecture and repositories

```text
src/
  api/         API integrations for auth, tours, cars, locations, checkout
  hooks/       TanStack Query hooks and feature logic
  components/  Feature UI and reusable components
  pages/       Authentication, tour, booking, hotel, car, payment screens
  routes/      React Router configuration
  context/     Checkout state context
  lib/         HTTP client and shared types
```

- [My frontend fork](https://github.com/MohammedNasr51/round-5-front-Safarni)
- [Original team frontend](https://github.com/Huma-volve/round-5-front-Safarni)
- [Related Huma-volve Laravel backend](https://github.com/Huma-volve/round5-safarnia)

## Running locally

Use a maintained Node.js LTS installation (Node 20 or 22 is a sensible choice for this Vite 6 project).

```bash
git clone https://github.com/MohammedNasr51/round-5-front-Safarni.git
cd round-5-front-Safarni
npm ci
cp .env.example .env
npm run dev
```

On Windows, create `.env` by copying `.env.example` manually or with `copy .env.example .env` in Command Prompt.

The repository currently reads `VITE_GOOGLE_CLIENT_ID` for Google OAuth. **Important:** API base URLs are hardcoded in two different Axios modules (`src/lib/axios-instance.ts` and `src/api/car.ts`). Running the app locally does *not* restore the unavailable API; update/configure those URLs to point to a working backend if you want live integration. Do not commit real API credentials or secrets.

```bash
npm run lint
npm run build
npm run preview
```

## Planned no-backend portfolio demonstration

An optional Mock Service Worker (MSW) mode can intercept requests to a same-origin `/api` endpoint and simulate search, login, bookings, profiles and payment acknowledgments in the browser. In this future demo:

- Data will be **fictional and browser-local**, resettable and persistable across refreshes.
- All **payments and bookings will be simulated**, never charged or reserved.
- Google OAuth and Stripe services must be disabled/replaced with clearly labeled demo equivalents.
- Real Laravel integration will remain available when demo mode is disabled.

The detailed implementation specification is maintained separately as `CODEX_SAFARNI_MSW.md` (add it to the repo if desired).

## Technical limitations / maintenance notes

- `src/lib/axios-instance.ts` still points to a hardcoded HTTP API URL, which can cause HTTPS mixed-content failures. `src/api/car.ts` uses a separate backend base URL. Normalize both clients before public demo deployment.
- The authentication verification hook currently navigates on settled mutation, including errors; error-path navigation should be corrected.
- Some routes are declared twice; these should be cleaned up.
- This frontend has not yet been validated here as an end-to-end functioning deployment.
- Do not publicly deploy the related Laravel backend without a separate security review, including the unauthenticated deployment webhook visible in its `routes/api.php`.

## Credit

Built collaboratively as part of the Huma-volve internship. See the [original repository](https://github.com/Huma-volve/round-5-front-Safarni) for project history and team contributions.
