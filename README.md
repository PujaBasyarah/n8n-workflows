# n8n Workflows Portfolio

A collection of automation workflows I've built with [n8n](https://n8n.io) — real use cases, exported as JSON with explanations and screenshots so you can see how each one works.

## Projects

| Project | Description | Key Tools/Integrations |
| --- | --- | --- |
| [AMDAL Document Generator](https://github.com/PujaBasyarah/n8n-workflows/blob/main/amdal-document-generator) | Auto-generates environmental impact assessment (AMDAL) document narratives from a form submission, using an LLM to write formal sections, then fills a Google Docs template automatically. | Form Trigger, LLM Chain (OpenRouter/Claude), Google Drive, Google Docs |
| [Customer Support Agent](https://github.com/PujaBasyarah/n8n-workflows/blob/main/customer-support-agent) | Scrapes a business website's sitemap, builds a structured knowledge-base "encyclopedia" using an LLM, and powers an AI support agent that answers customer questions from it. Tested via n8n's Chat Trigger; ready to connect to WhatsApp, Telegram, or other channels. | Form Trigger, HTTP Request/XML/Code (scraping), LLM Chain (OpenRouter), Chat Trigger |

*(More projects coming soon.)*

## About

I build practical automations that connect forms, AI models, and document/data tools to remove manual work. Each project folder contains:

- The exported workflow JSON (credentials scrubbed — see note below)
- A screenshot of the workflow canvas
- A written explanation of the problem it solves and how it works

## A note on credentials

Every exported workflow here has had all API keys, tokens, and webhook IDs removed or replaced with placeholders. Only credential *references* (names, not actual secrets) remain, matching how n8n exports work by default. These files are for demonstration only — they are not directly runnable without reconnecting your own credentials in n8n.

## Contact

Feel free to reach out if you'd like to collaborate or discuss automation work.
