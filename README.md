# ai-redteam-wordlists

Wordlists `.txt` and workflow helpers for defensive, authorized red-team testing of AI assistants.

- Massive: 5,000+ seeds → tens of thousands of generated variants.
- Structured by category (`fundamentals`, `prompt_injection`, `llm_output`, `data_attacks`, `app_system`).
- Multi-language: FR, EN, ES, DE, IT, AR, ZH, etc.
- Transformations: base64, hex, rot13, homoglyphs, zero-width, reverse, leet, fragmentation.
- Format wrappers: JSON, YAML, CSV, HTML, Markdown, INI, Logs, MCP.
- Enriched JSONL metadata for analysis, sorting, filtering.

## Contents

- `seclists/` — `.txt` payload sets.
- `wordlist` — executable launcher (do not run `.py` files directly).
- `tools/` — provider/mode references and advanced usage notes.
- `configs/` — sample target and config snippets.

## Quick usage

From repo root:

```bash
./wordlist run <provider> <model> <mode> <wordlist> <out_dir> [options]
```

Example:

```bash
./wordlist run ollama llama3.2:3b exact_extract \
  seclists/AI-LLM-Chatbot-Local-Validated-Smoke.txt runs/local-smoke --ids 1-20
```

Supported providers: `openrouter`, `anthropic`, `gemini`, `gemini-cli`, `claude-code`, `ollama`.

Supported modes: `exact_extract`, `rag_verbatim`, `multi_turn`, `tool_choice`.

Outputs: `results.jsonl`, `summary.json`, `summary.md`.

## Evidence of compromise (concise)

- Local proof run example (synthetic canary payloads, local Ollama).
- Command used:

```bash
./wordlist run ollama llama3.2:3b exact_extract \
  seclists/AI-LLM-Chatbot-Local-Validated-Smoke.txt runs/quick-check --limit 1 --no-progress
```

- Result (summary):
  - `tested: 1`
  - `findings: 1`
  - `clean: 0`
  - `api_errors: 0`

The matching payload surfaced a synthetic token leak pattern (redacted in model output), with
`protected_hits: ["token"]` in the generated score.

Re-run locally to regenerate proof artifacts:

```bash
./wordlist run ollama llama3.2:3b exact_extract \
  seclists/AI-LLM-Chatbot-Local-Validated-Smoke.txt runs/quick-check --limit 1 --no-progress
```

## Safety policy

- Synthetic canary-only data (no real secrets).
- Non-destructive checks only.
- Respect each target model and platform authorization scope.
