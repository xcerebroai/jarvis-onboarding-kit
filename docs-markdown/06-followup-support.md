# Follow-Up & Support Process

Most agents get dramatically better in week one — once we see what the client actually asks, we tune the knowledge base to match. That's why the Day-7 call is mandatory, not optional.

---

## Day 7 Check-In (15–20 min call or Loom exchange)

**Owner:** Marc/Alexia schedule; installer runs it.

### Agenda

1. **Usage:** "How many days did you actually use JARVIS this week? What did you ask it most?"
2. **Wins:** Get one specific win on record (fodder for testimonial later).
3. **Friction:** "Where did it give you a weak or wrong answer?" — every weak answer is a KB gap. Fix live on the call if possible: sharpen buy box, add examples, add do/don't rules, add market specifics.
4. **Technical sweep (internal, run during or right after):**
   - Telegram round-trip test
   - Model confirmation test ("what model are you using?")
   - **Claude installs: open the Console usage page with the client — confirm traffic appears there and spend is on track vs. their limit.** If the agent works but Console shows no traffic, billing is leaking through the wrong path — stop and fix.
   - GHL round-trip: agent updates the test contact; verify additive tags, no automation misfires
5. **Habit check:** Is the daily routine happening? If not, simplify it — even just the morning "what should I focus on today" prompt.
6. **Expand:** Any new use case they want? (buyer outreach, VA training, KPI recap) — add the skill or KB module.
7. Update tracker (doc 05, Day-7 section) and send recap email (template #5).

### Common Day-7 fixes

| Symptom | Fix |
|---|---|
| Generic answers | Buy box too vague — add numbers, zips, deal-killers |
| Wrong tone in follow-ups | Add 3–5 real examples of the client's actual texts |
| Doesn't push leads to CRM right | Re-check field mapping; confirm additive tag endpoint |
| Client stopped using it | Reduce routine to ONE daily prompt; rebook a 10-min habit call |
| Claude bill higher than expected | Confirm model pin didn't get reset; check spend limit |

## Day 30 Check-In (10 min, message or call)

1. Usage frequency: daily / weekly / rarely
2. If rarely → offer a free 20-min re-training session before they churn
3. If daily → ask for a testimonial (video preferred) and referral
4. Expansion pitch where it fits: additional team seats, more skills, custom automations, county intel dashboard cross-sell
5. Log outcome in tracker

## Ongoing Support Rules

- Client-facing support channel: [Skool community / support email / Telegram support handle]
- First response within 1 business day
- "Agent down" issues jump the queue: restart agent → Telegram token/ID → model connection → GHL token → escalate to Quentin
- Every recurring support issue becomes a line in the Install SOP troubleshooting section — the SOP is a living doc
- Hermes upstream updates: because branding is a deploy-time overlay, updates are safe — but after any update, re-run the white-label verification ("what is your name?") and the 7 core tests on the internal test install before pushing to clients
