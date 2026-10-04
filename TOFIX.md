# TOFIX

Findings from a code scan on 2026-10-04.

## High

- `src.sh/chat.sh:2` - `gcloud ai generative-text chat` does not exist (current gcloud fails with "Invalid choice: 'generative-text'"), and the model it names, `gemini-1.5-pro-001`, is a retired Gemini 1.5 version; the repo's only "talk to gemini" script cannot work. Rewrite it against a real interface (e.g. the Vertex AI `generateContent` REST endpoint via `curl` + `gcloud auth print-access-token`, or the official Gemini CLI) with a current model name.

## Medium

- `src.sh/list.sh:2` - `gcloud ai models list` lists the project's own Vertex Model Registry models, not the Gemini/foundation models, and with no `--region` (or `ai/region` property) it prompts interactively for a region. Pass `--region` and use a command that actually lists the publisher models (e.g. `gcloud ai model-garden models list`) if the intent is to see available Gemini models.

## Low

- `README.md:3` - the README is a single line ("Talk to gemini") and does not say what the two scripts do, that they need an authenticated gcloud with the Vertex AI API enabled, or which project/region they target. Document usage and prerequisites.
