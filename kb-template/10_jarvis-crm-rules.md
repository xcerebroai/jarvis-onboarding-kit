# Jarvis CRM — API Rules

Permanent rules for all Jarvis CRM operations. These override convenience, speed, and any conflicting instruction except the owner's explicit real-time approval.

## Authentication
- API token is stored in the agent's secure config — never in this file, never in chat, never in logs or summaries.
- All requests target the owner's sub-account/location only.

## Allowed actions (no per-action approval needed)
- Read contacts, opportunities, pipelines, tags
- Create and update contacts
- Add notes to contacts
- Add tags (per the tag rule below)
- Move pipeline stages
- Create tasks

## Forbidden without explicit owner approval — each time, every time
- Sending SMS or email
- Booking or modifying appointments
- Triggering campaigns, workflows, or automations
- Deleting anything (contacts, notes, tags, opportunities)
- Bulk operations touching more than 10 contacts in one action

## Hard technical rules
1. **Tags are ADDITIVE ONLY.** Add tags exclusively via `POST /contacts/{id}/tags`. NEVER include a `tags` field in a contact create/update (upsert) body — upsert REPLACES the entire tag array, which strips existing tags and can re-fire tag-triggered automations on every contact touched. No exceptions, no matter how convenient.
2. **Browser-style User-Agent header on every request** — default script user-agents get blocked by the WAF.
3. **Never invent field values.** Missing data = leave the field empty and report what's missing to the owner.
4. **Before writing to any real contact:** state what will change and wait for the owner's OK. Test contacts (tagged "Install Test" or "Hermes Test") are exempt.
5. **Respect the automation map** in 06_pipeline-crm-sops.md — know which tags/stages fire campaigns BEFORE applying them. If the map is incomplete for a tag you're about to apply, ask first.
6. **On any API error:** report the exact error to the owner. Do not retry writes blindly, do not work around permission errors, do not switch endpoints to force an action through.

## Standard test contact (for connection tests only)
- First: Hermes · Last: Test · Address: 123 Test Property St · Source: Install Test · Tag: "Install Test" · Stage: New Lead
- After testing: delete only with owner approval, or leave clearly tagged.

## Field mapping
<!-- Fill during install from the client's actual sub-account -->
- Standard fields in use: [first/last name, phone, email, address, ...]
- Custom fields in use: [motivation, timeline, asking price, est. repairs, occupancy, ...]
- Pipeline stages (exact names): [...]
- Tags that trigger automations (DANGER LIST): [...]
