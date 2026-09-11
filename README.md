# batchask-kit

Run a JSONL of prompts through an LLM, results to JSONL

Small but I use it weekly.

## Highlights

- Failures go to a sidecar file with error type, message and status
- JSONL in, JSONL out: the input is streamed line by line
- Idempotent: ids already in the output are skipped on a rerun
- Progress, token counts and a cost estimate on stderr
- Real rate limiting: sliding windows on requests/min and tokens/min
- 4xx fails fast; 429 and 5xx retry with jittered backoff
- Per-row overrides for model, system, temperature and max_tokens
- A bad input line is logged and skipped, never fatal

## Installation

```bash
pip install -r requirements.txt
export OPENAI_API_KEY=sk-...
```

## Usage

```bash
python batch.py prompts.jsonl -o answers.jsonl --workers 4 --rpm 300
```

## Project structure

```text
├── .github/
│   └── workflows/
│       └── ci.yml
├── docs/
│   ├── configuration.md
│   ├── development.md
│   ├── roadmap.md
│   └── tradeoffs.md
├── tests/
│   └── test_smoke.py
├── .editorconfig
├── .gitignore
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── batch.py
├── prompts.sample.jsonl
└── requirements.txt
```

## Development

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m pytest -q
```

## Notes

- mostly stable, edge cases remain

## License

MIT. Do whatever you want.
