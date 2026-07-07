# Install Tracker & QA Checklist — INTERNAL

One copy per client. File the completed version in `Clients/<Name>/Hermes Install/07-Final-Handoff/`. An install is DONE only when every QA box is checked.

---

## Header

- Client name:
- Business name:
- Market:
- Date installed:
- Installed by:
- Intake form received (date):
- Intake reviewed by:
- Install call scheduled (date/time):
- Day-7 follow-up scheduled (date/time):

## Pre-Call Prep

- [ ] Intake reviewed top to bottom
- [ ] Client folder created from template
- [ ] KB files pre-drafted (9 + index)
- [ ] AI path decided: ☐ Claude API key ☐ ChatGPT sign-in ☐ OpenAI API key ☐ Other: ______
- [ ] GHL sub-account reviewed; pipelines/tags/automations screenshotted

## Telegram

- [ ] Telegram on phone + computer
- [ ] Bot created via BotFather — bot username: ______
- [ ] Bot token saved by client (we do NOT store it)
- [ ] User ID / Chat ID captured — method used: ______

## Hermes / AI

- [ ] Hermes Agent Desktop installed, online
- [ ] Hermes Dashboard installed, sees agent
- [ ] Client signed into Hermes — correct workspace
- [ ] AI connected — provider: ______ · connection type: ☐ API key ☐ Subscription
- [ ] **Claude installs only:** Console account created · spend limit set ($____/mo) · model pinned to cheap tier · test traffic visible in Console usage page
- [ ] White-label overlay applied — version: ______ · agent identifies as JARVIS everywhere

## Training

- [ ] All 9 KB files + index uploaded
- [ ] Guardrails file uploaded (standard block)
- [ ] Escalation triggers file uploaded (standard block)
- [ ] Base role prompt set
- [ ] Skills uploaded — list: ______

## GHL Connection

- [ ] Private Integration token created (min scopes) — scopes: ______
- [ ] Correct location/sub-account selected
- [ ] Field mapping verified — missing fields documented: ______
- [ ] Pipeline stages verified/created
- [ ] Standard tags created (client-facing display "JARVIS Lead")
- [ ] **Tag writes confirmed additive endpoint (never upsert body)**
- [ ] WAF/User-Agent workaround needed? ☐ No ☐ Yes (applied)
- [ ] Agent permissions set — final posture: ______
- [ ] Automation review completed — collisions found/handled: ______

## Testing (all 7 required)

- [ ] T1 Telegram connection
- [ ] T2 Model confirmation (names pinned model)
- [ ] T3 Buy box answered from KB
- [ ] T4 Business benefit — specific to client
- [ ] T5 Fake seller lead — summary + next steps
- [ ] T6 GHL write via test contact — no unwanted automation fired · billing confirmed on key
- [ ] T7 Escalation behavior
- [ ] Test contact deleted or clearly tagged

## Handoff

- [ ] Playbook (doc 04) delivered
- [ ] Client sent a prompt from their own phone and got a business-specific answer
- [ ] Final acceptance prompt passed
- [ ] Day-7 call booked
- [ ] Recap email (template #4) sent same day

## Notes / Open Items

-

## Day-7 Follow-Up (fill after check-in)

- Client used agent ___ days out of 7
- Telegram working: Y/N · AI connected: Y/N · GHL connected: Y/N
- **Claude installs: Console usage matches expected traffic (no OAuth leak): Y/N**
- Leads created correctly: Y/N · Notes formatted well: Y/N · Automations behaving: Y/N
- KB gaps found: ______
- Tuning changes made: ______
- Recap email (template #5) sent: Y/N

## Day-30 Check-In

- Still active daily/weekly/rarely
- Top use cases:
- Upsell/expansion opportunity:
- Testimonial asked: Y/N
