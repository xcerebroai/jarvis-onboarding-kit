# JARVIS Agent Install — Client Onboarding Kit

**Version 1.0 — July 2026 — Just Jarvis LLC / Xcerebro AI**

This kit contains everything needed to take a client from "I bought the install" to "I use my JARVIS Agent every day." Follow the documents in order.

## Branding Rules (READ FIRST)

- **Client-facing documents and calls:** Say **JARVIS** only. Never say "Hermes," "GoHighLevel," or "GHL" to a client, on camera, or in anything the client keeps. The CRM is "Jarvis CRM." The agent is "JARVIS Agent."
- **Internal documents (this SOP, tracker, team chat):** Hermes / GHL terminology is fine.
- Files 01, 02, 04, 06, 07 are **client-facing** — JARVIS branding only.
- Files 03 and 05 are **internal** — never send to a client.

## The Documents

| # | File | Audience | When |
|---|------|----------|------|
| 01 | Client Intake Form | Client | Sent immediately after purchase, before scheduling |
| 02 | Pre-Install Access Checklist | Client | Sent with the install call confirmation, 48h before call |
| 03 | Team Install SOP | Internal | Used live during the install call |
| 04 | Client Handoff Playbook | Client | Delivered at the end of the install call |
| 05 | Install Tracker & QA Checklist | Internal | Filled out during and after every install |
| 06 | Follow-Up & Support Guide | Both | Day 7 and Day 30 check-ins |
| 07 | Email Templates | Internal (sent to client) | The full onboarding email sequence |

## The Onboarding Flow at a Glance

```
Purchase
  → Email #1 (Welcome + Intake Form)         [same day]
  → Intake reviewed by team                   [within 24h — Marc/Alexia]
  → Email #2 (Booking link + Access Checklist)[after intake received]
  → Install call scheduled                    [client picks slot]
  → Email #3 (48h reminder + checklist nudge)
  → INSTALL CALL (60–90 min, Team SOP doc 03)
  → Email #4 (Handoff Playbook + recap)       [same day as call]
  → Day 7 follow-up call/message              [doc 06]
  → Email #5 (Day 7 recap + tuning changes)
  → Day 30 check-in                           [doc 06]
  → Client moved to "active" status
```

## Hard Rules Learned From Past Installs (do not skip)

1. **Claude connections default to the API-key path**, not subscription sign-in. Console API key, model pinned to the cheaper tier, spend limit set. Subscription/OAuth sign-in has caused silent billing against the wrong pool before. ChatGPT installs may use sign-in as default.
2. **CRM tags are added additively** (`POST /contacts/{id}/tags`). Never write tags through an upsert body — it replaces the tag array and re-fires automations (this caused ~231 duplicate texts on a prior project).
3. **CRM API calls may need a browser-style User-Agent** to pass the Cloudflare WAF.
4. **White-label overlay is applied at deploy time**, never by editing Hermes files in place. In-place edits break on every Hermes update.
5. **No testing on real contacts.** Ever. Use the standard test contact (doc 03, section on testing).
6. **Install is not complete** until the client personally sends a prompt and gets a business-specific answer, and the QA checklist (doc 05) is fully green.
