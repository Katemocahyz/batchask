# batchask

Feed a thousand prompts, get a thousand answers

## Usage

```bash
python batch.py prompts.jsonl -o answers.jsonl --workers 4 --rpm 300
```

## Features

- Idempotent: ids already in the output are skipped on a rerun
- Real rate limiting: sliding windows on requests/min and tokens/min
- Failures go to a sidecar file with error type, message and status
- JSONL in, JSONL out: the input is streamed line by line
- A bad input line is logged and skipped, never fatal
- Progress, token counts and a cost estimate on stderr
- Per-row overrides for model, system, temperature and max_tokens
- 4xx fails fast; 429 and 5xx retry with jittered backoff

## Installation

```bash
pip install -r requirements.txt
export OPENAI_API_KEY=sk-...
```

## Project structure

```text
├── .github/
│   └── workflows/
│       └── ci.yml
├── docs/
│   ├── configuration.md
│   ├── development.md
│   ├── faq.md
│   ├── roadmap.md
│   ├── tradeoffs.md
│   └── usage.md
├── tests/
│   └── test_smoke.py
├── .gitignore
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── Makefile
├── SECURITY.md
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

## License

MIT. Do whatever you want.
