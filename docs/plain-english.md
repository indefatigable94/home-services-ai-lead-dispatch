# Plain English walkthrough

**What this is for:** a home-services owner (or a hiring manager who thinks like one) who wants to know what the system *does* before they care how it is wired.

## The feeling, not the tool list

When the phone rings at 6pm and nobody picks up, that job usually goes to whoever answers first. Incomplete intake is almost as bad: the tech shows up without the ZIP, the urgency, or a callback number, and the office spends the morning playing phone tag.

This build is a voice intake agent for a fictional company, **Princeton Heating & Air**. It answers the call, gathers the facts a dispatcher actually needs, and only claims success when the backend confirms the request landed.

## How a call feels end to end

1. Homeowner calls about an AC that runs but does not cool.
2. The agent (Maya) asks one clear question at a time: name, phone, address or ZIP, what is wrong, urgency, new vs existing customer, preferred window.
3. She reads it back. If something is wrong, she fixes it before doing anything permanent.
4. She sends a structured service request to an automation workflow (n8n).
5. That workflow checks that required fields are present. If they are, it can create or update a contact and opportunity in GoHighLevel and return a confirmation reference. If they are not, it returns `needs_human` instead of pretending.
6. Maya tells the caller only what the system confirmed. No invented prices. No fake arrival times.

## What "good" looks like here

| Owner cares about | How this build handles it |
|---|---|
| Missed or messy calls | Structured intake every time |
| Bad data in the CRM | Required-field gate before write |
| Lying AI | Agent speaks only confirmed backend status |
| Emergencies | Safety rules first; escalate, do not troubleshoot gas/smoke/flooding near power |
| Trust | Human callback path when tools fail |

## Honest status

This repository is a **reproducible setup and wiring guide**. The prompt, tool schema, sample payloads, n8n import, and GHL handoff notes are here so you can rebuild the chain. Treat it as a live production system only after you have verified: real call → real webhook payload → confirmed response → spoken result, plus at least one failure path.

## Where to go next

- Step-by-step setup: [setup-checklist.md](setup-checklist.md)
- How Retell, n8n, and the JSON contract fit: [technical-breakdown.md](technical-breakdown.md)
- How the lead would land in GoHighLevel: [ghl-wiring-summary.md](ghl-wiring-summary.md)
