# HERMES AGENT INSTALLATION — INSTRUCTIONS & CHECKLIST (Doc 09)
**Mac (Terminal) & Windows (PowerShell) · Generalized for all installs · v1.1**

---

# PART 1 — STEP-BY-STEP INSTRUCTIONS

## STEP 1 — Open the shell
- **Mac:** Cmd+Space → type `terminal` → Enter
- **Windows:** Start → type `powershell` → Enter

## STEP 2 — Check prerequisites
```
node --version
python3 --version      (Mac)
python --version       (Windows)
```
Need: **Node v18+**, **Python 3.10+**.
- Node missing → nodejs.org → LTS installer, defaults (Mac chip: Apple menu → About This Mac)
- Python missing (Windows) → python.org → tick **"Add Python to PATH"** on the FIRST screen
- Mac: "command line developer tools" popup → **Install** (includes Git, 5–15 min). No popup? `xcode-select --install`
- Windows: do NOT pre-install Git — the Hermes installer handles it

## STEP 3 — Network pre-flight
```
curl -I https://api.telegram.org
```
- HTTP response → clear, continue
- Hangs/redirects → network blocks Telegram → phone hotspot for the install; permanent fix afterward

## STEP 4 — Run the Hermes installer
1. Download from the standard source and launch
2. "System prerequisites — X of 11 steps" runs → let it finish untouched
3. Mac: stuck at 0 of 11 = hidden developer-tools dialog → find it, Install, wait; relaunch installer if it doesn't resume in 2 min
4. Let ALL steps finish including "Download Hermes Agent" — never cancel mid-way

Install locations: Mac `~/.hermes/hermes-agent` · Windows `C:\Users\<username>\AppData\Local\hermes\hermes-agent`

## STEP 5 — Verify
⚠️ **Close the shell entirely. Open a FRESH one.**
```
hermes --version
```
Expected: version banner (0.18+, Python version, project path).
Still "command not found"? Run the full path — Mac: `~/.hermes/hermes-agent/venv/bin/hermes --version` · Windows: `...\hermes-agent\venv\Scripts\hermes --version`. If that works, it's a PATH issue only.

## STEP 6 — First run
```
hermes gateway
```
Healthy = the "Hermes Gateway Starting… Messaging platforms + cron scheduler" box. Missing provider/channel messages = the to-do list, not errors.

## STEP 7 — Continue setup in the Hermes app
1. **AI provider:** API-key path ONLY — "I have an API key" → key in the **Anthropic** row → OpenRouter row EMPTY → never the OAuth sign-in → pin **Sonnet**
2. **Messaging:** bot token + numeric user ID → allowlist filled → allow-all = false → Save
3. Knowledge base, CRM, acceptance per the Install Cheat Sheet (Doc 08)

## STEP 8 — Make it survive reboots
- Windows: PowerShell **as Administrator** → `hermes gateway install`
- Mac: `hermes gateway --help` → service/install option
- Reboot test: restart → agent answers with no app opened manually

---

# PART 2 — PER-INSTALL CHECKLIST

**Machine:** ________ **OS:** ☐ Mac ☐ Windows **Date:** ________ **Installed by:** ________

## A. Prerequisites
- [ ] Shell opened (Terminal / PowerShell)
- [ ] `node --version` → v18+
- [ ] Python 3.10+ (Windows: "Add Python to PATH" ticked)
- [ ] Mac only: developer tools installed
- [ ] Windows only: Git NOT pre-installed
- [ ] Network pre-flight → Telegram reachable ☐ YES ☐ NO → hotspot used ☐

## B. Installation
- [ ] Installer downloaded from standard source
- [ ] All 11 prerequisite steps completed, no cancel mid-way
- [ ] Mac only: dev-tools dialog accepted if stalled
- [ ] Completed through "Download Hermes Agent"

## C. Verification
- [ ] FRESH shell after install
- [ ] `hermes --version` banner — version recorded: ________
- [ ] Version 0.18+ ☐ (0.17 Windows: flashing-window patch may be needed)
- [ ] `hermes gateway` prints startup box

## D. App-side setup
- [ ] API key in **Anthropic** row ☐ · OpenRouter row EMPTY ☐
- [ ] OAuth NEVER used ☐
- [ ] Model = **Sonnet** ☐
- [ ] Gateway reads **ready** ☐
- [ ] Telegram: token ☐ · numeric ID allowlisted ☐ · allow-all false ☐ · saved ☐
- [ ] Round-trip: bot replies from an allowed phone ☐

## E. Durability
- [ ] Auto-start installed (Win: Admin PowerShell → `hermes gateway install` / Mac: service option)
- [ ] Reboot test passed ☐ (or scheduled: ________)

## F. Sign-off
- [ ] ALL boxes checked — install COMPLETE
- Notes: ______________________________________

## Quick fixes
| Symptom | Fix |
|---|---|
| "command not found" after install | Fresh shell → full venv path |
| Installer stuck at 0 of 11 (Mac) | Accept the hidden dev-tools dialog |
| Telegram "attempt 1/8" + DNS-over-HTTPS | Hotspot → DNS 1.1.1.1/8.8.8.8 → router whitelist → dedicated data line |
| Gateway weird after repeated launches (Win) | End ALL hermes/python/node processes → launch once → wait 30s |
| Stale UI status | Full quit (tray too) → reopen; terminal log is truth |
