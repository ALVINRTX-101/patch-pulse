# Automated Vulnerability Management Platform

A policy-driven orchestration framework that ingests vulnerability scanner findings, applies context-aware SLA deadlines, creates tickets in Jira, and triggers Ansible playbooks for automated remediation.

## Architecture

1. **Scanner Trigger**: Tenable / Qualys detects vulnerabilities.
2. **Policy Evaluation**: `orchestration/jira_bridge.py` matches findings against `config/policy.json`.
3. **Jira Lifecycle**: Tickets created automatically with dynamic due dates based on asset tiers.
4. **Remediation**: Low-risk tiers auto-remediated via `playbooks/patch_system.yml`.

## Setup Instructions

1. Clone the repository:
   ```bash
   git clone [https://github.com/YOUR_USERNAME/auto-vuln-remediation.git](https://github.com/YOUR_USERNAME/auto-vuln-remediation.git)
   cd auto-vuln-remediation
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Configure environment variables in `.env`:
   ```env
   JIRA_BASE_URL=[https://your-domain.atlassian.net](https://your-domain.atlassian.net)
   JIRA_EMAIL=your-email@domain.com
   JIRA_API_TOKEN=your-jira-api-token
   JIRA_PROJECT_KEY=SEC
   ```

4. Run the orchestration script:
   ```bash
   python orchestration/jira_bridge.py
   ```
