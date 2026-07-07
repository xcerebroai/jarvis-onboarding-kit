# AI AGENT INSTALL — START-TO-FINISH CHEAT SHEET
**Mac (Terminal) & Windows (PowerShell) · Just Jarvis / Xcerebro AI · v1.1**
*Internal use. Client-facing language: the agent is JARVIS, the CRM is Jarvis CRM.*

---

## PHASE 0 — BEFORE YOU TOUCH THE MACHINE

- [ ] Intake form reviewed; buy box in writing
- [ ] Decide whose Anthropic Console account/card (default: client's)
- [ ] KB template files ready with placeholders filled (02_buy-box.md MUST have real numbers)
- [ ] Know which channel(s): Telegram (default) / WhatsApp (dedicated number ONLY)
- [ ] Client at the machine — THEY type all passwords; we never receive credentials

---

## PHASE 1 — PREREQUISITES

**Open the shell:**
- Mac: Cmd+Space → "terminal" → Enter
- Windows: Start → "powershell" → Enter

**Check what exists:**
```
node --version        # need v18+
```
```
# Mac:
python3 --version     # need 3.10+
# Windows:
python --version
```

**If Node missing:** nodejs.org → LTS installer → defaults. (Apple Silicon vs Intel: Apple menu → About This Mac.)
**If Python missing (Windows):** python.org → installer → ✅ TICK "Add Python to PATH" on the first screen.
**Mac only:** if any command triggers the "command line developer tools" popup → click Install (brings Git too, 5–15 min). If no popup: `xcode-select --install`
**Windows only:** don't hand-install Git — the Hermes installer pulls it.

**Network pre-flight (60 seconds, saves an hour):**
```
curl -I https://api.telegram.org
```
- HTTP response → clear, proceed
- Hangs / weird redirect → network blocks Telegram. Plan hotspot NOW for the install; permanent fix later (see Troubleshooting).

⚠️ **RULE: after ANY install, close the shell completely and open a FRESH one.** New commands aren't visible to old sessions. This causes half the fake "it didn't install" panics.

---

## PHASE 2 — INSTALL HERMES

1. Run the standard Hermes installer
2. Let it finish untouched — the "11 steps" prerequisite phase may stall waiting for the Mac developer-tools popup (click Install on it)
3. Fresh shell, then:
```
hermes --version
```
- [ ] Note the version in the tracker (0.18+ = flashing-window bug fixed upstream; 0.17 on Windows may need the local patch later)
4. First run:
```
hermes gateway
```
Its complaints = your to-do list. "Provider not configured" etc. is normal on a virgin install.

---

## PHASE 3 — CONNECT CLAUDE (THE LANDMINE FIELD)

**Nothing installs for Claude — it's a key, not a program.**

**Browser (client drives):**
1. console.anthropic.com → sign up with CLIENT's email (separate from claude.ai chat — a chat subscription does NOT include API)
2. Billing → add card → buy starter credits ($5–25)
3. - [ ] **SET MONTHLY SPEND LIMIT NOW** (Settings → Limits) — before the first key exists
4. API Keys → Create Key → name it → **copy with the Copy button** (drag-select = stray spaces)

**Hermes app:**
5. Click **"I have an API key"** (bottom of provider screen)
6. ⛔ **NEVER click "Sign in with Anthropic OAuth"** or run `claude setup-token` — that bills the wrong bucket silently. Cancel any popup mentioning OAuth.
7. - [ ] **VERIFY THE SLOT:** key must land in the **Anthropic** row. OpenRouter row = EMPTY. Blue/active dot on Anthropic. (The "I have an API key" dialog has dropped keys into OpenRouter before — check every time.)
8. - [ ] **PIN THE MODEL: Sonnet** (highest Sonnet number). Opus = ~5x cost on routine traffic.
9. Gateway status should now read **ready**.

**Error decoder:**
| Bot/gateway says | Meaning | Fix |
|---|---|---|
| Provider authentication failed | Key in wrong slot or bad paste | Check OpenRouter row empty; re-paste with Copy button |
| No usable credit | Account unfunded OR key from a different account | Key + money + account must be the same house; buy credits |
| Error mentions "OpenRouter" | OpenRouter still active provider | TRASH the OpenRouter entry (not just clear text), select Anthropic, restart |

---

## PHASE 4 — TELEGRAM

**Create the bot (client's phone):**
1. Search **@BotFather** (verified check) → `/newbot`
2. Display name = client's brand · username must end in `bot`
3. Copy the **bot token** → client saves it in their password manager. Never in screenshots/group chats.
4. Client taps **START on the new bot** (bot can't speak first)

**Get the numeric user ID (not the @username):**
- @userinfobot (EXACT handle, verified — search results are full of scam clones) → Start → copy the Id number
- Bulletproof fallback: client messages their own bot, then open `https://api.telegram.org/bot<TOKEN>/getUpdates` → find `"from":{"id":` → that number
- Lost the bot later? BotFather → `/mybots` → tap bot → tap its @username

**Wire it (Hermes → Messaging → Telegram):**
- [ ] Bot token pasted
- [ ] Numeric user ID in **Allowed Telegram user IDs** (comma-separate multiple people)
- [ ] **Allow all users = false/empty. Always.** Open bot = anyone burning the client's API money.
- [ ] Home channel ID = same user ID (lets the agent initiate: crons, alerts)
- [ ] Save changes

**Round-trip test:** client's phone → bot → "confirm you're connected"
⚠️ The sender must NOT be the account the agent is linked to (WhatsApp lesson: you can't message yourself). For Telegram bots this is fine — just make sure the sender's ID is on the allowlist. Silent bot + "Connected" status = allowlist miss.

---

## PHASE 5 — KNOWLEDGE BASE

1. Create the folder:
   - Mac: `~/Documents/JARVIS-Knowledge`
   - Windows: `Documents\JARVIS-Knowledge`
2. Drop in the filled template set: `_INDEX.md`, `00`–`09`, plus `10_jarvis-crm-rules.md`
3. Load + persist (send to the agent):
> Read every file in [folder path], starting with _INDEX.md. These are your permanent knowledge base — your source of truth. Add a permanent instruction to your memory: at the start of every session, on any channel, read this folder before business tasks. Then prove it: summarize the operating doctrine in 3 bullets and state my buy box.
4. - [ ] Buy box comes back with the CLIENT's real numbers (generic answer = files not found or placeholders never filled)
5. Convention: business doctrine in the root; machine/technical notes in an `ops\` subfolder — keep them separate.

---

## PHASE 6 — JARVIS CRM CONNECTION

1. Client's sub-account → Settings → **Private Integrations** → create token
   Scopes: contacts R/W, opportunities, tags, notes, tasks. Nothing more.
2. Store the token the agent's secure-config way — ask the agent itself: *"What's the secure way to store credentials in your config, without putting them in a plain knowledge file?"* Never paste tokens into KB files.
3. - [ ] **AUTOMATION REVIEW FIRST:** list which tags/stages/forms fire campaigns in his sub-account → fill the DANGER LIST in 06 + 10 files. (This is the 231-duplicate-texts insurance.)
4. Deploy `10_jarvis-crm-rules.md` and have the agent confirm. Core rules it enforces:
   - Tags via additive `POST /contacts/{id}/tags` ONLY — never in an upsert body
   - Browser-style User-Agent on all requests
   - No invented values; approval before real-contact writes; no blind retries on errors
5. Connection test — agent creates the standard test contact (Hermes Test / 123 Test Property St / tag "Install Test" / stage New Lead) and reads it back with ID, tags, stage
6. - [ ] Human check in the CRM: contact right, tags right, **nothing fired**

---

## PHASE 7 — MAKE IT SURVIVE REBOOTS

- Windows: `hermes gateway install` — **run PowerShell as Administrator** (without admin it silently falls back to a flimsy Startup-folder VBS)
- Mac: check `hermes gateway --help` for the service/install option
- [ ] Reboot test if time allows: restart machine → bot answers without anyone opening the app

---

## PHASE 8 — ACCEPTANCE (ALL MUST PASS)

- [ ] Bot answers on Telegram from client's phone
- [ ] "What AI model are you using?" → names **Sonnet**
- [ ] "What is my buy box?" → client's real numbers
- [ ] Console **Usage page shows today's traffic** (proves billing is on the key + spend limit — the check that catches wrong-path billing on day one)
- [ ] Test contact verified in CRM, zero automations fired
- [ ] **Client sends a prompt with their own hands**
- [ ] Handoff playbook delivered · Day-7 follow-up booked · tracker filed

---

## STANDING RULES (EVERY INSTALL, NO EXCEPTIONS)

1. OAuth for Claude: never. API key path only.
2. Key slot: Anthropic row, verified visually, every time.
3. Spend limit before first key.
4. Sonnet pinned, not Opus.
5. Allowlists locked; allow-all false.
6. WhatsApp = dedicated number only. Never a personal line (ban risk lands on the human).
7. No testing on real contacts. Ever.
8. Agent ground rules in doctrine: no fabricated numbers · report-before-fix · if a safety guard blocks an action, surface it — never restructure around it.
9. Client types their own passwords. We store none.
10. Client-facing = JARVIS. Hermes/GHL are internal words.

---

## TROUBLESHOOTING QUICK-DRAW

**"command not found" right after installing** → fresh shell. (Windows delete syntax: `Remove-Item path -Force`, not `rm -f`.)

**Telegram stuck at "attempt 1/8" + DNS-over-HTTPS hunting** → network blocks Telegram. Ladder: hotspot test (2 min, confirms it) → DNS swap to 1.1.1.1/8.8.8.8 (Mac: System Settings → Wi-Fi → Details → DNS) → router parental-controls/filtering whitelist for api.telegram.org → dedicated data SIM or paid auto-connect VPN (last resort — VPNs fail silently). US home ISPs almost never block; check for a VPN on the machine or a missed macOS "allow incoming connections?" popup first.

**Bot connected but silent** → allowlist: numeric ID (not @username), saved, sender isn't the linked account itself.

**Gateway weirdness after repeated launches (Windows)** → Task Manager → Details → end ALL hermes/python/node processes → launch ONCE → wait 30s. Multiple stacked instances = event-loop stalls, ghost states.

**UI shows stale status (says "not paired"/"needs setup" after you fixed it)** → full quit (system tray too) → reopen. The terminal log is the truth; the UI lags.

**Flashing node.exe windows (Windows, WhatsApp bridge)** → v0.17 bug: bridge respawns with a visible console; closing the window kills it and loops. 0.18+ fixed upstream. On 0.17: hidden-window patch + crash-loop alert (see Dark Phoenix ops notes).

**Every fix on a live agent:** report-only diagnosis → backups + rollback command in hand → then change. Never let the agent kill the gateway it's running through.
