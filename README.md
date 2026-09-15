# Habib Olajide — Automation Engineer & Prompt Engineer

**Featured build: Princeton Heating & Air — 24/7 AI Lead & Dispatch System**

Home-service companies lose jobs when calls are missed, details are incomplete, or follow-up is slow. This portfolio shows a Retell voice agent wired to an n8n webhook, with a clear path into GoHighLevel, so intake becomes structured data a dispatcher can trust.

> **Honest status:** reproducible setup + wiring guide. Call it production-proven only after you verify live call → webhook payload → response → spoken result (and one failure path). No API keys or real customer data live in this repo.

## Skim this first

- **Problem:** missed / messy inbound calls → lost revenue and bad CRM data
- **Approach:** prompt-engineered voice intake + HTTP tool call + workflow validation + CRM handoff
- **Proof artifacts:** agent prompt, tool schema, importable n8n workflow, sample JSON, test plan, Loom script
- **Pages site:** https://indefatigable94.github.io/home-services-ai-lead-dispatch/

## Architecture

```text
Caller
  -> Retell voice agent
  -> create_service_request (POST JSON)
  -> n8n webhook
  -> validate required fields
  -> [optional] GoHighLevel contact + opportunity
  -> confirmation or needs_human
  -> agent speaks only what the backend confirmed
```

## Two ways to read it

| If you want… | Start here |
|---|---|
| Owner-friendly story | [docs/plain-english.md](docs/plain-english.md) |
| Contracts, nodes, payloads | [docs/technical-breakdown.md](docs/technical-breakdown.md) |
| CRM handoff | [docs/ghl-wiring-summary.md](docs/ghl-wiring-summary.md) |
| Rebuild steps | [docs/setup-checklist.md](docs/setup-checklist.md) |

## Prompt architecture (short)

The agent prompt is split on purpose:

1. **Role** — intake coordinator, not technician
2. **Style** — one question at a time
3. **Safety** — emergencies escalate; no invented prices or ETAs
4. **Intake** — required dispatcher fields
5. **Tool rule** — call only after confirmed read-back
6. **Response** — speak backend status only

Full prompt: [agent-prompt.md](agent-prompt.md)

## API / webhook flow

1. Retell custom function POSTs flat JSON ([tool-schema.json](tool-schema.json)).
2. n8n receives at `retell/create-service-request` ([n8n-retell-service-request-workflow.json](n8n-retell-service-request-workflow.json)).
3. Code node validates required keys.
4. Response is either `status: received` + `confirmation_reference`, or `status: needs_human` + `missing_fields`.

Samples:

- [samples/sample-request.json](samples/sample-request.json)
- [samples/sample-response-received.json](samples/sample-response-received.json)
- [samples/sample-response-needs-human.json](samples/sample-response-needs-human.json)

## Failure handling

| Case | Expected behavior |
|---|---|
| Missing required field | No premature tool success; ask again or return `needs_human` |
| Gas / smoke / live electrical flood risk | Safety first; escalate; do not troubleshoot |
| Price or availability unknown | Refuse to invent; human review |
| Tool timeout / CRM error | Apologize; route to human; never claim the request was created |

Full matrix: [test-plan.md](test-plan.md)

## Stack

Retell AI · n8n · HTTP webhooks · JSON schemas · GoHighLevel (documented hop) · structured prompt design

## Demo assets

- Walkthrough script: [loom-walkthrough.md](loom-walkthrough.md)
- Setup checklist: [docs/setup-checklist.md](docs/setup-checklist.md)
- Portfolio site: `docs/index.html (also docs/site/index.html)` (GitHub Pages)

## Repo map

```text
.
├── README.md
├── agent-prompt.md
├── tool-schema.json
├── n8n-retell-service-request-workflow.json
├── test-plan.md
├── loom-walkthrough.md
├── samples/
└── docs/
    ├── plain-english.md
    ├── technical-breakdown.md
    ├── ghl-wiring-summary.md
    ├── setup-checklist.md
    └── site/index.html
```

## About

Habib Olajide — automation and prompt engineering for conversational agents, workflow orchestration, and API/webhook handoffs. Background in healthcare/operations shapes how this system thinks about triage, escalation, and clean handoffs.

Contact: holajide@gmail.com
