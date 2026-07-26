# Connect ServiceNow to Your Own LLM — Custom Transformer Examples

Sample request/response transformer scripts for connecting ServiceNow's **Generative AI Controller (GAIC)** to external LLM providers via the **Generic LLM Connector** (`sys_generative_ai_custom_llm_transformer`).

## Companion video

These scripts are companion material for the video **"Connect ServiceNow to Your Own LLM"** on my YouTube channel.

📺 Video URL: https://youtu.be/R1HVirWwNUI

### Endpoints used in the video:
- https://api.anthropic.com/v1/messages
- https://generativelanguage.googleapis.com/v1beta/interactions
- https://router.huggingface.co/v1/chat/completions
- https://api.deepseek.com/chat/completions
- https://api.moonshot.ai/v1/chat/completions

## What's included

| File | Provider | Notes |
|---|---|---|
| `transformer-anthropic.js` | Anthropic (Claude) | Direct Messages API integration |
| `transformer-google.js` | Google Gemini | Targets the Gemini Interactions API (`steps` response schema) |
| `transformer-huggingface.js` | Hugging Face | OpenAI-compatible Inference Providers endpoint |
| `transformer-deepseek.js` | DeepSeek | OpenAI-compatible `/chat/completions` endpoint |
| `transformer-moonshot.js` | Moonshot AI (Kimi) | OpenAI-compatible `/chat/completions` endpoint variant |

Each file contains a **request transformer** (builds the outbound body/headers) and a **response transformer** (parses the provider's response back into text for GAIC).

## Disclaimer

These scripts are provided **for demonstration and educational purposes only**. They are simplified examples intended to illustrate the shape of a ServiceNow custom LLM transformer and are **not** production-ready code. They have not been hardened for error handling, retries, rate limiting, credential security, or data privacy requirements in a live instance.

Use them at your own risk. I take no responsibility or liability for any use of this code, including but not limited to any costs, data exposure, security issues, or damages that may result from deploying it in your own ServiceNow instance or against any third-party LLM API.

Always test work thoroughly in a non-production instance before considering deploying anything to production workflows.

## Before you build your own transformer

Every provider has its own request/response shape, auth header, and quirks — and those details change over time. Before creating your own scripts, read the current official documentation for the provider and model you're integrating:

**ServiceNow**
- Generative AI Controller: https://www.servicenow.com/docs/r/intelligent-experiences/generative-ai-controller/generative-ai-controller.html
- Create a model: https://www.servicenow.com/docs/r/intelligent-experiences/create-model.html
(Crucially, this page is missing details on API header configuration. Without this knowledge, you will not be able to connect to the endpoints. This is also a Zurich-release page, which currently does not exist for Australia, but is also valid for it.)
- Configure a Generic LLM Connector: https://www.servicenow.com/docs/r/intelligent-experiences/configure-a-generic-llm-connector.html (This is an Australia-release page, but its steps are largely unnecessary, superceded by the 'wizard' setup steps described in the Create a model page, and in my video. Does reference some useful tables, however.)
- A2A API Key credential behavior: https://www.servicenow.com/docs/r/intelligent-experiences/a2a-api-key-credential-behavior.html
(Oriented towards A2A credentials but content on API headers and prefixes also applicable to LLM API credentials.)

**Anthropic**
- Messages API reference: https://platform.claude.com/docs/en/api/messages
- Create a Message: https://platform.claude.com/docs/en/api/beta/messages/create

**Google Gemini**
- Interactions API reference: https://ai.google.dev/gemini-api/docs/interactions-overview
- Getting started: https://ai.google.dev/gemini-api/docs/get-started

**Hugging Face**
- Inference Providers — Chat Completion: https://huggingface.co/docs/inference-providers/en/tasks/chat-completion
- Your First API Call: https://huggingface.co/docs/inference-providers/en/guides/first-api-call

**DeepSeek**
- Create Chat Completion: https://api-docs.deepseek.com/api/create-chat-completion/
- Your First API Call: https://api-docs.deepseek.com/

**Moonshot AI (Kimi)**
- Create Chat Completion: https://platform.moonshot.ai/docs/api/chat
- QUickstart: https://platform.kimi.ai/docs/overview

APIs and schemas (model names, endpoint paths, response formats, etc.) evolve over time, so treat the docs above — not this repo — as the source of truth when you build your own transformer.

## License

No license is granted for production use. These files are shared as learning material to accompany the video above; adapt them for your own instance at your own discretion and risk.
