# Architecture overview

PLAYBOOK runs in two environments that share the same casino interface and the same planning and
accounting rules. The connected application is private; the public demo is a separate static build
on fictional data.

```text
Connected application (private)               Public demo
───────────────────────────────               ───────────
Browser                                       Browser
  │                                             │  static HTML, JavaScript and CSS
  ▼                                             ▼
Next.js application                           Cloudflare Pages (static hosting)
  ├─ sign-in (Clerk)                            └─ the same casino interface,
  ├─ casino game services                          fictional scenarios built in,
  │    over pure domain rules                      state kept in the browser tab
  ├─ PostgreSQL through Prisma                     (no backend, database or sign-in)
  └─ server-side Salesforce client
       └─ OAuth, read-only ──▶ Salesforce
```

## Connected PLAYBOOK application

- **Stack:** Next.js (App Router), React and TypeScript, with Tailwind CSS and Motion for the casino
  interface.
- **Authentication:** Clerk. Every protected page and API route re-checks the session on the
  server.
- **Data:** PostgreSQL through Prisma. Each user works in their own workspace, and the server scopes
  every request to it.
- **Salesforce:** OAuth 2.0 with PKCE and a read-only integration. Salesforce communication happens
  only on the server. See [Salesforce integration](SALESFORCE_INTEGRATION.md).
- **Planning:** pure, deterministic domain rules turn the CRM read and the Buy-In answers into a
  ranked plan. Due commitments come first, oldest first, and are never dropped. Optional plays fill
  the remaining time.
- **Honest Commitment Accounting (v2):** Worked, Handled, Verified closed, Still open and Follow-up
  planned are computed by pure functions from the day's recorded outcomes and from Salesforce's own
  task records. Verified closed comes only from real Salesforce observations.
- **Persistence first:** every answer, outcome and decision is saved before anything is celebrated
  on screen. Workdays are stored, and a private record book compares a user's own finished days.

The connected application's source code is private.

## Public static casino demo

- **Build:** a Next.js static export of the same casino interface. The output is plain HTML,
  JavaScript, CSS and fonts.
- **Data:** six fictional Salesforce scenarios, built into the demo when it's built.
- **Interactions:** everything runs in the browser. Outcomes live in the page's state.
- **Isolation:** the Buy-In answers and display settings are kept per browser tab only. A new tab,
  window or browser always starts a fresh day, and **Restart demo** clears the tab.
- **No connection to anything private:** no Salesforce connection, no backend, no API routes, no
  database, no sign-in and no cookies.
- **Accounting:** the demo uses the same accounting rules as the connected application. With no
  Salesforce records to observe, Verified closed is never shown, and the interface explains why.
- **Hosting:** Cloudflare Pages, serving the static files with a restrictive Content Security Policy
  and other security headers.

## Shared by both

- The casino interface: Buy-In, Casino Floor, Cards, Roulette, Slots, Record Outcome, The Deck and
  Cash Out.
- The planning, ranking and commitment-accounting rules.
- Accessibility: keyboard operation, visible focus, screen-reader announcements and respect for
  reduced-motion settings.
