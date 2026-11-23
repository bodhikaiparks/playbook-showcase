# Salesforce integration

**Built to integrate with Salesforce.**

This page describes how the connected PLAYBOOK application works with Salesforce. It is written for
sales leaders, Salesforce administrators and revenue operations teams. The public demo does not
connect to Salesforce; it uses fictional data only.

## Purpose

PLAYBOOK reads a rep's own Salesforce work and turns it into a prioritized day of plays. Salesforce
remains the system of record. Outcomes recorded in PLAYBOOK stay in PLAYBOOK, marked "reported by
you", and a task counts as verified closed only when Salesforce's own record shows it closed.

## How it connects

- **OAuth 2.0 with PKCE.** Each user connects their own Salesforce login, and PLAYBOOK never sees a
  Salesforce password.
- **Minimal permissions.** PLAYBOOK requests API access and a refresh token only, and refuses
  broader grants.
- **Server-side only.** The browser never receives a Salesforce token, and all Salesforce calls are
  made by the server.
- **Credentials protected.** Tokens are encrypted at rest. Disconnecting revokes PLAYBOOK's access
  at Salesforce and deletes the stored credentials and data.
- **Controlled access.** A deployment can be limited to approved Salesforce organizations, and the
  integration can be switched off entirely.

## Read-only by design

- PLAYBOOK **never writes** to Salesforce: no inserts, updates or deletes.
- It reads only the connected user's own records: **Accounts, Contacts, Opportunities, Tasks and
  Events**, limited to open work and recent activity.
- It does not read Leads or Cases.
- Contact phone numbers and email addresses are not stored. PLAYBOOK only needs to know that a
  channel exists and may be used, and it respects do-not-call and email opt-out flags.

## How Salesforce data becomes plays

| Salesforce data                                    | In PLAYBOOK                                      |
| -------------------------------------------------- | ------------------------------------------------ |
| A task due today or overdue                        | A **commitment**, always shown, oldest due first |
| A meeting today                                    | A meeting commitment at its set time             |
| An opportunity with a next step or a slipping date | An optional deal play                            |
| An opportunity or account with no recent activity  | An optional review or reactivation play          |
| A contact                                          | How a play can be reached, respecting opt-outs   |

Each play records its reason, so the interface can always say why a hand comes first. "No recent
activity" means no activity recorded in Salesforce, not proof of real-world silence.

## Validation scope

- The integration has been validated against a **Salesforce Developer Edition organization**
  containing fictional and sample data.
- PLAYBOOK is **not** Salesforce-certified, **not** listed on AppExchange and **not** endorsed by
  Salesforce. It is not yet deployed with production customers.
- Compatibility with any particular organization is not assumed.

## Private onboarding

Public visitors cannot connect a Salesforce organization. Connecting a real organization is a
controlled, private process:

1. An introductory conversation.
2. Compatibility testing against the organization's edition, API access, field-level security and
   how the team uses tasks and events.
3. A security review with the organization's administrator.
4. Approved onboarding of specific users.

---

Interested in connecting PLAYBOOK to your Salesforce organization? Let's discuss private
onboarding: [Contact](https://www.linkedin.com/in/bodhiparks/).
