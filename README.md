# Local Coding LLMs on a 32 GB Mac

Field report from testing local coding models, inference backends and coding agents on an Apple Silicon Mac with 32 GB unified memory (October 2026).

**Read it here:** https://nikay99.github.io/local-coding-llm-mac/

## Short version

- **Model:** Qwen3.6-35B-A3B (4-bit) was the best model that runs stably on 32 GB. Dense models and models with classic attention ran out of memory or were too slow for agent work.
- **Backend:** LM Studio's Splash runtime generated 170 tok/s instead of 68 tok/s with MLX, with the same weights and quality.
- **Agent:** OpenCode and pi tied on targeted tasks (10/12); on real open-source bug fixes OpenCode was clearly more reliable.
- **Workflow:** With only the issue text, the local model fixed about half of 8 real bug fixes from popular libraries. With a short brief plus an acceptance test written by a stronger model, OpenCode fixed all 8.
- **Prompting:** A short working-rules prompt ("read first, never invent missing things, verify at the end") stopped the model from inventing missing files.

## What was tested

1. 7 models on 12 coding tasks with hidden tests, plus prompt, sampling and max-token variants.
2. 9 coding agents (OpenCode, pi, Qwen Code, Claude Code, Codex CLI, Crush, mini-swe-agent, Goose, Aider) on the same model, with tasks built to expose agent differences.
3. 8 real bug fixes and features from yargs-parser, qs, humanize, python-tabulate and python-dotenv, graded with the maintainers' own tests, run inside a macOS sandbox.

Single runs are noisy; see the Limits section on the page.
