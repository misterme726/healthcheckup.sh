# HealthCheckup

A small, maintainable application to run health checks against services and report results. Designed to be easy to configure, run locally, and integrate into CI/CD pipelines.

## Features
- Periodic health probes (HTTP, TCP, command-based)
- Configurable checks and thresholds
- JSON and plain-text output
- Exit codes for CI integration
- Simple logging

## Repository layout
- `src/` — application source code  
- `config/` — example configs (YAML/JSON)  
- `tests/` — unit and integration tests  
- `Dockerfile` — container image build  
- `README.md` — this file

## Prerequisites
- Git
- Node.js >= 14 / Python >= 3.8 / Go 1.16 (adjust for your stack) — check project language
- Optional: Docker

## Installation
Clone the repo and install dependencies (adjust commands for project language):

git clone <repo-url>
cd healthcheckup

# Node.js example
npm install

# Python example (if applicable)
pip install -r requirements.txt

## Configuration
Create or edit a config file in `config/` (YAML or JSON). Typical fields:
- name: service name
- type: http | tcp | cmd
- target: URL / host:port / shell command
- interval: probe interval in seconds
- timeout: probe timeout
- retries: number of retries before failing
- alert: optional alerting configuration

Example (YAML):
```yaml
checks:
    - name: api
        type: http
        target: https://api.example.com/health
        interval: 30
        timeout: 5
        retries: 2
```

## Usage
Run with a config file:
```bash
# Node.js example
node src/index.js --config config/default.yaml

# Docker example
docker build -t healthcheckup:latest .
docker run --rm -v $(pwd)/config:/app/config healthcheckup:latest --config /app/config/default.yaml
```

Output formats:
- `--output json` for machine-readable results
- `--output text` (default)

Exit codes:
- `0` — all checks passed
- non-zero — at least one check failed

## Testing
Run tests:
```bash
# Node.js
npm test

# Python (pytest)
pytest
```

## Logging & Monitoring
- Logs to stdout by default; set `LOG_LEVEL` environment variable to adjust verbosity.
- Integrate output with monitoring systems via JSON output or custom hooks.

## Contributing
- Fork the repository and open a pull request.
- Follow existing code style and include tests for new behavior.
- Run linters and tests before submitting.

## License
Specify a license (e.g., MIT). Add a `LICENSE` file at the repo root.

## Contact
For issues, use the repository issue tracker.
