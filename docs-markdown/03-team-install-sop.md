# Hermes Agent Install SOP — INTERNAL ONLY

**Never send this document to a client.** Client-facing language: the agent is "JARVIS," the CRM is "Jarvis CRM." Internally we say Hermes and GHL.

**Roles:** Installer runs the call. Marc/Alexia handle intake review, scheduling, and 7-day follow-up. Escalate blockers to Quentin.

---

## Phase 0 — Before the Call (Installer prep, ~30 min, day before)

1. Read the client's intake form top to bottom.
2. Create the client folder from the template:
   ```
   Clients/<Client Name>/Hermes Install/
     01-Company-Info/
     02-Buy-Box/
     03-Scripts/
     04-SOPs/
     05-Jarvis-GHL/
     06-Skills/
     07-Final-Handoff/
   ```
3. Pre-draft the knowledge-base markdown files from the intake (company overview, buy box, scripts, offer rules, guardrails). Use the standard KB structure — 9 files + index. Naming convention: `##-topic-name.md` (e.g., `02-buy-box.md`). You should walk into the call with 80% of the KB written.
4. Confirm which AI path applies (see Phase 3 decision table) based on intake Q38–40.
5. Open the Install Tracker (doc 05) and fill in the header.
6. Log into the client's GHL sub-account (with their prior permission) and screenshot current pipelines, tags, and automations into `05-Jarvis-GHL/`.

## Phase 1 — Call Open (5 min)

1. Confirm the client is at their computer with Telegram on both devices.
2. Set expectations: "60–90 minutes; by the end JARVIS is live, trained, connected to your CRM, and you'll test it yourself."
3. Share screen or have client share theirs. **Client types their own passwords. We never receive, store, or screenshot credentials.** If a token appears on screen, don't save the recording frame; paste tokens directly where they belong and into the client's own secure notes.

## Phase 2 — Telegram Setup (10 min)

1. Client opens Telegram, searches **@BotFather**, sends `/newbot`.
2. Bot display name: client's brand (e.g., "Anchor Home Offers AI"). Username must end in `bot`.
3. BotFather returns the **bot token** → client pastes it straight into Hermes config (next phase) and into their own password manager. We record only "token saved: yes" in the tracker.
4. Get the **Telegram User ID / Chat ID**:
   - Use the Hermes-recommended ID bot first.
   - Fallbacks: @userinfobot or @RawDataBot.
   - Backup: have the client message their new bot, then pull the chat ID via the Bot API `getUpdates`.
5. Record in tracker: bot username, user ID captured (yes/no).

## Phase 3 — Hermes Install & AI Connection (15–20 min)

1. Client downloads and installs **Hermes Agent Desktop** and **Hermes Dashboard Desktop**.
2. Launch both; if terminal launch is required, walk them through it. Confirm agent shows **online** and dashboard sees the agent before proceeding.
3. Client signs into their Hermes account. Confirm correct workspace.

### AI model connection — decision table

| Client situation | Path |
|---|---|
| Wants Claude | **API key path (default for Claude — see below)** |
| Wants ChatGPT, has active subscription | Subscription sign-in path |
| Wants ChatGPT, needs direct billing or sign-in fails | OpenAI API key path |
| Needs a model not offered via sign-in | API key path |

### ⚠️ Claude = API key path, always (unless Quentin approves an exception)

**Why:** subscription/OAuth sign-in has previously routed Hermes usage through the Claude Code OAuth credentials pool — silent, wrong-bucket billing that took real effort to diagnose. Do not repeat it.

Steps:
1. Client creates an Anthropic **Console** account (console.anthropic.com) — this is separate from a claude.ai chat subscription; a chat plan does not include API access.
2. Client adds a payment method and **sets a monthly spend limit** matching their intake budget (Q40).
3. Client creates an API key, pastes it directly into Hermes config, and saves it in their own password manager. The full key is shown once — save immediately.
4. **Pin the model in Hermes config to the designated cheaper tier for all calls.** Do not leave model selection on default/auto.
5. Verify in the Console usage page that the test calls (next step) show up there — this proves billing is on the key, not an OAuth pool.

### Verification (all paths)
Ask via the Hermes interface:
- "What AI model are you currently using?" → must name the pinned model.
- "Respond with one sentence confirming you are ready to help with real estate wholesaling."

## Phase 4 — White-Label Overlay (10 min) — DO NOT SKIP

The client must never see "Hermes" in the product.

1. Apply the **deploy-time overlay** (standard overlay package) — never edit Hermes source files in place; in-place edits break on every upstream update.
2. Overlay rebrands the ~8–10 customer-visible strings to **JARVIS**.
3. Restart the agent, then verify: agent name in Telegram replies, dashboard title, any greeting/system strings. Ask the agent "what is your name?" → must answer JARVIS (branded), not Hermes.
4. Record overlay version in the tracker.

## Phase 5 — Connect Telegram to Hermes (5 min)

1. In Hermes Telegram settings, enter bot token + user ID.
2. Test from the client's phone: "Hello JARVIS, confirm you are connected."
3. If no reply: token correct? client pressed Start on the bot? user ID correct? agent running? → restart agent, retest.

## Phase 6 — Train the Agent (15 min)

Upload the pre-drafted KB files from Phase 0, then fill gaps live with the client. Required set:

1. `01-company-overview.md` — business, market, team, brand voice, do-not-say list
2. `02-buy-box.md` — cities, zips, property types, equity, repairs, min spread, deal-killers
3. `03-lead-intake.md` — intake questions: motivation, condition, timeline, price, occupancy, mortgage/liens/probate
4. `04-scripts.md` — cold call, inbound, follow-up, objections, appointment confirm, offer explanation, dead-lead revival
5. `05-offer-comping.md` — ARV method, conservative comping, repair estimating, MAO formula, fee calc
6. `06-crm-sops.md` — pipeline stages, tags, custom fields, follow-up cadence, SMS rules
7. `07-disposition.md` — buyer list process, marketing, assignment vs double close
8. `08-guardrails.md` — see below, non-negotiable
9. `09-escalation.md` — hot-lead triggers, see below
10. `00-index.md` — file map

### Guardrails (paste into every install's `08-guardrails.md`)
Agent must NOT: promise an offer or closing date; state a definitive property value; give legal or tax advice; tell a seller to stop paying a mortgage or ignore foreclosure notices; claim to be a licensed agent unless the client is; misrepresent identity; send mass SMS outside the client's compliance process; send offers/contracts/final approvals without client sign-off.

Agent SHOULD: gather info, identify motivation, ask condition/timeline/price/occupancy/lien questions as intake only, summarize leads, recommend next steps, escalate hot leads.

### Hot-lead escalation triggers (paste into `09-escalation.md`)
Sell now · vacant · behind on payments · non-paying tenant · inherited/probate · foreclosure · flexible on price · wants offer today · requests callback · gives access · has a competing offer.
On any trigger: summarize → mark hot → tag in CRM → correct pipeline stage → notify client → recommend action.

### Agent role prompt (base for every wholesaling client)
> You are the client's real estate wholesaling operations assistant. You help manage seller leads, buyer leads, follow-up, CRM updates, appointment prep, offer prep, and daily execution. Think like an acquisitions and operations assistant. You are not a lawyer, tax advisor, or licensed agent unless the client says otherwise. Keep answers clear, direct, action-focused. Gather info, summarize motivation, identify urgency, recommend next steps. Escalate urgent or valuable leads immediately.

## Phase 7 — Connect GHL ("Jarvis CRM") (15 min)

1. In the client's GHL sub-account: create a **Private Integration token** with minimum required scopes (contacts read/write, opportunities, tags, notes; add calendars only if booking is in scope). Avoid the legacy location API key when the private integration is available.
2. Paste token into Hermes integrations → select correct location/sub-account → save.

### ⚠️ Hard technical rules (from prior production incidents)
- **Tags:** add via the additive endpoint `POST /contacts/{id}/tags`. **Never** send tags inside a contact upsert body — upsert replaces the whole tag array and re-fires tag-trigger automations (caused ~231 duplicate texts on a prior project).
- **WAF:** if API calls return Cloudflare blocks, set a browser-style User-Agent header on Hermes's GHL requests.

3. **Field mapping — complete BEFORE any write test.** Verify these exist (create or document as missing): first/last name, phone, email, property address/city/state/zip, lead source, motivation, timeline, asking price, est. repairs, occupancy, mortgage balance, arrears, liens, probate status, foreclosure status, appointment date, notes, pipeline stage, tags.
4. Pipeline mapping (create if missing): New Lead → Contacted → Qualified → Appointment Set → Offer Made → Follow Up → Contract Sent → Under Contract → Closed / Dead Lead.
5. Standard tags: Hermes Lead (display: "JARVIS Lead"), Hot Seller, Follow Up, Needs Offer, Appointment Set, Dead Lead, Buyer Lead, Agent Lead, Probate, Foreclosure, Absentee Owner, Tired Landlord.

### Agent permissions — default posture
ALLOW: read contacts, create/update contacts, notes, additive tags, move stages, create tasks, draft (not send) SMS/email, prepare lead summaries.
REQUIRE CLIENT APPROVAL: sending SMS/email, booking appointments, triggering automations, offers, contracts, anything legal-adjacent.
Adjust only with the client's explicit sign-off; record final permission set in the tracker.

## Phase 8 — Automation Safety Review (10 min)

Before ANY live write, review with the client: tag triggers, stage triggers, form triggers, appointment triggers, active SMS/email campaigns, missed-call text back, nurture sequences, internal notifications.

Identify which tags/stages fire messages. If a standard tag collides with an existing trigger, rename ours or pause theirs during testing.

## Phase 9 — Testing (15 min) — all 7 must pass

**Standard test contact (every install, same convention):**
First: Hermes · Last: Test · Phone: client-approved test number · Email: hermestest@example.com · Address: 123 Test Property St · Source: Hermes Install Test · Tag: Hermes Test

| # | Test | Prompt | Pass condition |
|---|------|--------|----------------|
| 1 | Telegram | "Are you connected?" | Replies in Telegram as JARVIS |
| 2 | Model | "What model are you using and are you ready to help with wholesaling?" | Names pinned model, confirms |
| 3 | Knowledge | "What is my buy box?" | Answers from uploaded files, matches intake |
| 4 | Business benefit | "How can you benefit my wholesaling business?" | Specific: intake, follow-up, comping, CRM, dispo, daily tasks |
| 5 | Fake seller lead | "Seller lead: John Smith, 123 Main St, San Antonio TX. House needs work, tenant not paying, wants to sell fast. What next?" | Identifies motivated seller, asks missing info, recommends steps, clean summary |
| 6 | GHL write | Have agent create/update the test contact | Contact + notes + additive tags + correct stage in GHL; **no unwanted automation fired**; billing shows on the API key (Claude installs: check Console usage) |
| 7 | Escalation | "This seller wants to sign today. What should you do?" | Escalates to client, no promises |

After test 6: delete the test contact or leave it clearly tagged Hermes Test.

## Phase 10 — Handoff (10 min)

1. Deliver the **Client Handoff Playbook** (doc 04) — JARVIS-branded version only.
2. Walk through the daily workflow live: client sends "What should I focus on today in my wholesaling business?" **from their own phone.**
3. The install is not complete until the client personally sends a prompt and gets a business-specific answer.
4. Final acceptance prompt (client sends it): *"How can you benefit my real estate wholesaling business, and what should I ask you every day to make more money?"* Answer must reference their market, buy box, lead process, and CRM.
5. Schedule the Day-7 follow-up before ending the call.
6. Complete the Install Tracker (doc 05) and file it in `07-Final-Handoff/`.

## What NOT To Do

- Don't start without a reviewed intake. Don't skip the white-label overlay. Don't use subscription sign-in for Claude. Don't leave model selection on auto. Don't put tags in upsert bodies. Don't test on real contacts. Don't let Hermes fire live automations unreviewed. Don't store client passwords anywhere. Don't end the call before the client drives a test themselves.

## Troubleshooting Quick Reference

**Telegram bot silent:** token correct → client pressed Start → user ID correct → agent running → signed in → integration enabled → restart agent.
**AI not responding (Claude/API):** key valid → spend limit not hit → model pinned correctly → Console shows the traffic (if traffic is missing from Console but the agent works, STOP — it's billing through the wrong path; fix before continuing) → restart agent.
**AI not responding (ChatGPT sign-in):** signed in → subscription active → correct model → usage cap → restart.
**GHL failing:** right sub-account → token valid + scoped → Cloudflare block? add browser UA → fields exist → pipeline exists → tags exist → token not expired.
**Weak KB answers:** sharpen buy box, add examples, more specific SOPs, clear do/don't rules, market detail → retest tests 3–5.
