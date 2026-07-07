# TECHNICAL SETUP — HERMES · CLAUDE · TELEGRAM (Doc 10)
**Start to finish, no business prep. Every command and code. ~45–60 min on a clean machine. v1.0**

FLOW: Prereqs → Install Hermes → Claude key → Telegram bot → Wire it → Test → Auto-start

## STEP 1 — Prerequisites
Shell: Mac Cmd+Space → `terminal` · Windows Start → `powershell`
```
node --version
python3 --version     # Mac
python --version      # Windows
```
Need Node v18+, Python 3.10+. Node → nodejs.org LTS. Python (Win) → python.org, tick "Add Python to PATH". Mac dev-tools popup → Install (`xcode-select --install` if no popup). Windows: don't pre-install Git.

**Network check (do not skip):**
```
curl -I https://api.telegram.org
```
HTTP response = clear · hangs/redirect = blocked → do everything on a phone hotspot, fix network after.

## STEP 2 — Install Hermes
Run the installer → let the "11 steps" finish untouched. Then FRESH shell:
```
hermes --version
hermes gateway
```
✅ Healthy first run prints "Hermes Gateway Starting… Messaging platforms + cron scheduler". Missing-provider messages = to-do list, not errors.

## STEP 3 — Get the Claude API key (browser — nothing installs)
1. console.anthropic.com → sign up (separate from claude.ai chat; a chat subscription does NOT include API)
2. Billing → card → starter credits ($5–25)
3. **Settings → Limits → set monthly spend limit** — BEFORE creating any key
4. API Keys → Create Key → copy with the **Copy button** (drag-select = stray spaces)
Key format: `sk-ant-api03-xxxxxxxx...` — shown ONCE, save immediately.

## STEP 4 — Connect Claude in Hermes
1. Provider screen → **"I have an API key"** → paste
2. ⛔ TWO TRAPS: never click "Sign in with Anthropic OAuth" / never run `claude setup-token` (wrong billing path) · VERIFY THE SLOT — key in the **Anthropic** row, **OpenRouter row EMPTY**
3. Pin model to **Sonnet** (Opus ≈ 5× cost)
4. Gateway reads **ready**

Error decoder: "authentication failed" = wrong slot/bad paste · "no usable credit" = unfunded account or key from a different account (key+money+account must match) · mentions "OpenRouter" = trash the OpenRouter entry, select Anthropic, restart.

## STEP 5 — Create the Telegram bot (phone)
1. Search **@BotFather** (verified) → `/newbot`
2. Display name = anything · username must end in `bot`
3. Token returned, format `1234567890:AAExxxxxxxx...` → save securely
4. **Tap START on the new bot** (bots can't speak first)

**Numeric user ID** (number, not @username):
- @userinfobot (exact handle, verified) → Start → copy `Id:`
- Fallback: message your own bot, then browser:
```
https://api.telegram.org/bot<TOKEN>/getUpdates
```
→ find `"from":{"id":` → that number
- Lost the bot? BotFather → `/mybots` → tap bot → tap its @username

## STEP 6 — Wire Telegram in Hermes
Messaging → Telegram: bot token → paste · **Allowed Telegram user IDs** → numeric ID(s), comma-separated · **Allow all users = false/empty, always** · Home channel ID = same user ID (enables agent-initiated messages) · Save → full restart if UI looks stale.

## STEP 7 — Test everything
From the phone:
> confirm you're connected
> What AI model are you using?
- Replies + names Sonnet = both pipes work
- Billing proof: console.anthropic.com → **Usage** — test traffic must appear there (= billing on YOUR key + limit)
- Silent bot + "Connected" status = allowlist miss, or you're messaging from the account the agent is linked to

## STEP 8 — Survive reboots
- Windows: PowerShell **as Administrator** → `hermes gateway install`
- Mac: `hermes gateway --help` → service option
- Final proof: reboot → bot answers, no manual launch
Anytime: `hermes gateway status` · `hermes gateway restart`

## DONE-STATE CHECKLIST
| # | Check | Pass looks like |
|---|---|---|
| 1 | `hermes --version` | Banner in a fresh shell |
| 2 | Gateway | "ready" + startup box |
| 3 | Provider | Anthropic row · OpenRouter empty · OAuth never |
| 4 | Model | Sonnet pinned |
| 5 | Spend limit | Set on Console |
| 6 | Telegram | Token · numeric ID allowlisted · allow-all false |
| 7 | Round-trip | Bot replies from allowed phone |
| 8 | Billing | Traffic on Console Usage page |
| 9 | Reboot | Answers after restart, no manual launch |
