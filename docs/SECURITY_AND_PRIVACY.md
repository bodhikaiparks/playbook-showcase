# Security and privacy

This page summarizes how PLAYBOOK approaches security and privacy, at a level suitable for a public
audience.

## The public demo

The interactive demo at [playbook-casino-demo.pages.dev](https://playbook-casino-demo.pages.dev) is a
separate static build with fictional data.

- **No connection to real systems.** It has no backend, database, API routes, sign-in or Salesforce
  connection, and it offers no way to connect one.
- **Nothing collected.** It sets no cookies, includes no analytics, and its pages make no requests
  to other sites. Visitor progress stays in the browser tab and disappears when the tab closes or the
  demo is restarted.
- **Visitors are isolated.** Separate tabs, windows and browsers never share a fictional day.
- **Security headers.** It is served over HTTPS with a restrictive Content Security Policy and
  protections against framing and content sniffing.
- **Checked before publication.** The demo's build is scanned for credentials, Salesforce endpoints,
  database connection strings, server routes and unexpected outside hosts, and browser-tested, in
  continuous integration and before each release.
- **Fictional by design.** Every account, deal and task is invented. Changes between fictional days
  are labelled as scenario data, never as Salesforce observations.

## The connected application

- **Read-only Salesforce access** with minimal permissions. PLAYBOOK never writes to Salesforce.
- **Authentication on every request.** Each protected page and API route re-checks the session on the
  server.
- **Tenant isolation.** Each user's workspace is identified only from their session. Another
  workspace's records are never returned.
- **Protected credentials.** Salesforce credentials stay on the server and are encrypted at rest.
- **Validated configuration.** Settings are validated at startup, and unsafe configurations are
  refused in production-like environments.
- **Minimal personal data.** Contact phone numbers and email addresses from Salesforce are not
  stored.
- **Tested.** Automated tests cover tenant isolation, request forgery and the read-only boundary,
  among other security properties.

## Certifications and audits

No third-party security audit or certification (such as SOC 2, ISO 27001 or HIPAA) has been
performed. Organizations considering a private integration receive a security review as part of
onboarding.

## Reporting a concern

To report a suspected security issue, please get in touch privately through
[Contact](https://www.linkedin.com/in/bodhiparks/) rather than in a public channel.
