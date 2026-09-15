# Loom walkthrough script (about 4 minutes)

## 0:00–0:25 — The problem

"Hi, I'm Habeeb. I build voice and workflow automations for businesses that lose leads when calls are missed or information is incomplete. This demo is a home-services intake agent. It answers the call, collects the details a dispatcher needs, and sends a structured service request to a webhook."

## 0:25–0:55 — The map

Show the README architecture. Explain: "The caller is the starting point. Retell handles the conversation. The custom function is the bridge. n8n receives the JSON, validates it, and can write the request to a CRM or sheet. The important design choice is that the agent does not announce success until the backend confirms success."

## 0:55–1:45 — The live call

Run the golden-path call. Use the AC-not-cooling scenario. Let the agent ask the questions. Point out the one-question-at-a-time behavior and the read-back confirmation.

## 1:45–2:30 — The prompt

Show the prompt. Explain role, style, safety rules, intake sequence, tool rule, and failure rule. Say: "These are separate sections because each one controls a different failure. The role controls identity. The safety rules prevent risky advice. The intake sequence makes the data complete. The tool rule controls timing."

## 2:30–3:15 — The API handoff

Show the function schema and n8n execution. Point to the exact JSON body, HTTP status, and returned status. Do not show secret headers or private customer data.

## 3:15–3:45 — Reliability test

Show one missing-field or tool-failure test. Say: "The agent is allowed to say it needs a human. That is better than a confident lie."

## 3:45–4:05 — Close

"This prototype shows how I approach automation: start with a business failure, turn it into a conversation contract, pass structured data through an API, and test the failure path instead of only showing the happy path."

## Recording checklist

- Use a clean browser profile if possible.
- Hide API keys, phone numbers, email addresses, and webhook secrets.
- Zoom the browser so the prompt and JSON are readable.
- Keep the recording under five minutes.
- Export as MP4 and name it `Habeeb_Olajide_Retell_n8n_Walkthrough.mp4`.
