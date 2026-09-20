# patch-pulse

Production-oriented vulnerability remediation orchestration platform with a 3-Tier Governance Policy.

## Governance

| Tier | Environment / Asset | Workflow |
|---|---|---|
| Tier 1 | Dev/Staging | Auto-remediate with Ansible/API |
| Tier 2 | Standard infrastructure | Jira Standard Change request, then remediation |
| Tier 3 | Critical infrastructure | Manual CAB approval required before execution |

The application defaults to **dry-run** mode. Remediation requires explicit configuration.

## Features

- Vulnerability ingestion from JSON
- Governance classification
- Tier 1 Ansible execution
- Tier 2 Jira Standard Change creation
- Tier 3 CAB approval gate
- Verification hooks
- Structured audit logging
- Retries with exponential backoff
- Environment-variable secrets
- Scope/production safety controls
- CLI workflow
- Unit tests
- Docker support
- GitHub Actions CI

## Quick start

```bash
cp .env.example .env
python -m venv .venv
# Linux/macOS
source .venv/bin/activate
# Windows
# .venv\Scripts\activate

pip install -r requirements.txt
python -m app.main --help
```

Run the sample in dry-run mode:

```bash
python -m app.main remediate --input examples/vulnerabilities.json
```

Enable a real Tier 1 Ansible run only after validating inventory and controls:

```bash
export PATCH_PULSE_DRY_RUN=false
export PATCH_PULSE_ALLOWED_ENVIRONMENTS=dev,staging
python -m app.main remediate --input examples/vulnerabilities.json
```

## Security model

- Never commit `.env`, API tokens, SSH keys, or credentials.
- Jira and other credentials are read from environment variables.
- Tier 1 is restricted to explicitly allowed environments.
- Tier 2 never executes remediation until the configured Jira gate is satisfied.
- Tier 3 never auto-executes; CAB approval is an external/manual control.
- Production remediation is disabled by default.
- Every workflow produces an audit event.

## Example input

See `examples/vulnerabilities.json`.

## License

MIT
