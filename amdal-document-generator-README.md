# AMDAL Document Generator

An n8n workflow that automates the drafting of AMDAL (Analisis Mengenai Dampak Lingkungan / Environmental Impact Assessment) documents — a formal document required in Indonesia for certain business and construction projects.

## Problem

Drafting an AMDAL document requires writing multiple formal narrative sections (background, geophysical conditions, biological conditions, social conditions, impact identification, environmental management/monitoring plans, and conclusions) based on project-specific data. Writing these manually is repetitive and time-consuming, especially across many projects.

## Solution

This workflow takes basic project data through a simple form, uses an LLM to draft each required narrative section in formal Indonesian, and automatically inserts the generated text into a Google Docs template — producing a ready-to-review draft document with no manual writing or copy-pasting.

## How it works

1. **Form Trigger** — Collects project details: company name, business type, project location, land area, preparation date, and optional environmental data (PM10 air quality, noise levels, BOD water quality).
2. **Edit Fields** — Normalizes the submitted form data into clean variable names for use downstream.
3. **Basic LLM Chain (OpenRouter → Claude)** — Generates all required narrative sections (background, geophysical, biological, social conditions, impact identification and explanation, management plan, monitoring plan, conclusion) strictly from the provided data, in formal Indonesian, returned as structured JSON.
4. **Code** — Parses the LLM's JSON output and merges it with the original data for use in the next step.
5. **Copy File (Google Drive)** — Duplicates a pre-made AMDAL Google Docs template, named after the company.
6. **Update Document (Google Docs)** — Finds and replaces all placeholder tags (e.g. `{{narasi_kesimpulan}}`) in the copied template with the generated narrative text and project data.

## Tools/Integrations

- n8n Form Trigger
- LangChain Basic LLM Chain (n8n)
- OpenRouter (Claude Sonnet 4.5)
- Google Drive API
- Google Docs API
- JavaScript (Code node) for JSON parsing

## Notes

- The workflow enforces that the LLM only uses supplied data — no fabricated statistics or claims — via explicit prompt instructions.
- `workflow.json` in this folder has all credentials and identifiers scrubbed/replaced with placeholders. To use it yourself: import into n8n, reconnect your own Google Drive/Docs and OpenRouter credentials, and set up your own Google Docs template with matching `{{placeholder}}` tags.
