# ai-redteam-wordlists

Wordlists `.txt` and workflow helpers for defensive, authorized red-team testing of AI assistants.

- Massive: 5,000+ seeds -> tens of thousands of generated variants.
- Structured by category (`fundamentals`, `prompt_injection`, `llm_output`, `data_attacks`, `app_system`).
- Multi-language: FR, EN, ES, DE, IT, AR, ZH.
- Transformations: base64, hex, rot13, homoglyphs, zero-width, reverse, leet, fragmentation.
- Format wrappers: JSON, YAML, CSV, HTML, Markdown, INI, Logs, MCP.
- Enriched JSONL metadata for sorting and analysis.

## Contents

- `seclists/` — curated `.txt` payload sets only.
- `wordlist` — main launcher (no `.py` usage required).
- `tools/` — provider/mode notes and recommended wordlists.
- `configs/` — example target and environment variables.

## Usage

From repo root:

```bash
./wordlist run <provider> <model> <mode> <wordlist> <out_dir> [options]

Example (local):

./wordlist run ollama llama3.2:3b exact_extract \
seclists/AI-LLM-Chatbot-Local-Validated-Smoke.txt runs/local-smoke --limit 1 --no-progress

Providers:
openrouter, anthropic, gemini, gemini-cli, claude-code, ollama

Modes:
exact_extract, rag_verbatim, multi_turn, tool_choice

Outputs per run:

- results.jsonl
- summary.json
- summary.md

## Evidence of compromise (concise)

Reproducible synthetic-canary leak proof (local):

./wordlist run ollama llama3.2:3b exact_extract \
seclists/AI-LLM-Chatbot-Local-Validated-Smoke.txt runs/quick-check --limit 1 --no-progress

Observed summary:

- tested: 1
- findings: 1
- clean: 0
- api_errors: 0
- score: protected_hits: ["token"]

This demonstrates synthetic token-marker extraction in controlled testing.

GPT-5.5-style proof command (same framework, replace credentials/provider target as authorized):

./wordlist run openrouter gpt-5.5-medium exact_extract \
seclists/AI-LLM-GPT55-Validated-Positive-Leakage.txt runs/gpt55-proof --limit 1 --no-progress

## Safety policy

- Synthetic canary-only inputs (no real credentials, tokens, or secrets).
- Non-destructive checks only.
- Execute only within explicit authorization and scope.
