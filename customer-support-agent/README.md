# Customer Support Agent (Website Encyclopedia Builder)

An n8n workflow that turns any business website into an AI customer support agent's knowledge base — automatically.

## What it does

1. **Form Trigger** — submit a business website URL
2. **Sitemap discovery** — fetches `sitemap.xml` (or `sitemap_index.xml` / `wp-sitemap.xml`), following nested sitemap indexes when present
3. **Scraping** — fetches each page's HTML and extracts clean text content (title, meta description, body text)
4. **Encyclopedia builder** — feeds all scraped content to an LLM, which synthesizes it into a structured Markdown "Support Encyclopedia" (policies, amenities, FAQs, contact info, etc., deduplicated and organized by category)
5. **AI Support Agent** — uses that encyclopedia as its system knowledge to answer customer questions

## Why it's useful

Instead of manually writing FAQ scripts for a support bot, this workflow reads a business's own website and generates a comprehensive, structured knowledge base automatically — then powers a live AI agent with it.

## Channel

The included workflow tests the agent via n8n's built-in **Chat Trigger**, so it can be tried out immediately without any messaging platform setup.

The same `AI Agent` node can be connected to a messaging channel instead (or in addition) — for example:
- **WhatsApp** — via the WhatsApp Business Cloud API trigger/reply nodes (built into n8n)
- **Telegram** — via n8n's Telegram Trigger/Send Message nodes
- **Slack, Instagram, Messenger**, etc. — any n8n-supported chat trigger + reply pair

Swapping channels is just a matter of replacing the trigger and reply nodes at the edges — the scraping and encyclopedia-building core stays the same.

## Key tools/integrations

- Form Trigger
- HTTP Request + XML + Code nodes (sitemap crawling & scraping — no paid scraping API required)
- LLM Chain via [OpenRouter](https://openrouter.ai) (model-agnostic — works with Gemini, Claude, GPT, etc.)
- n8n Chat Trigger (included, ready to test out of the box)

## Setup

1. Import `customer_support_agent.json` into n8n
2. Add your OpenRouter credential to the `openrouter-model` node (any OpenRouter-supported model works — set the model ID in the node)
3. Run the `form_trigger` → `build_encyclopedia` chain once per business to generate its knowledge base
4. Paste the generated encyclopedia into the `AI Agent`'s System Message field
5. Test via the built-in Chat Trigger, or connect a messaging channel (WhatsApp, Telegram, etc.) for production use

## Notes / limitations

- Sitemap discovery assumes a fairly standard structure; highly custom sites may need the URL-fetching logic adjusted
- The encyclopedia is currently a manual copy-paste step from the builder chain into the Agent's System Message — a future version could automate this with an n8n Data Table for multi-business support
- No credentials are included in the exported JSON (n8n never exports these) — you'll need to connect your own
