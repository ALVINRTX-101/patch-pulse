# Security Policy

## Reporting vulnerabilities

Do not disclose vulnerabilities in public issues. Report security issues privately to the repository maintainers.

## Operational controls

1. Store secrets in environment variables or an approved secret manager.
2. Use least-privilege Jira/API/Ansible credentials.
3. Keep Tier 1 inventories limited to approved Dev/Staging assets.
4. Keep production execution disabled unless explicitly governed.
5. Preserve audit logs and protect them from unauthorized modification.
6. Review generated changes before enabling non-dry-run operation.
