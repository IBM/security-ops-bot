# security-ops-bot

Public documentation and request portal for the IBM GitHub org security operations bot.

## What this repo is for

The security-ops bot automatically scans every active IBM GitHub org repository for open security
alerts (Dependabot, code scanning, secret scanning), tracks SLA deadlines, and enforces
remediation. This repo serves two purposes:

1. **Documentation** — guides for repo admins who receive a security tracking issue.
2. **Request portal** — a place to submit self-service requests to the bot (see below).

## Requesting a security enforcement exemption

If your repository cannot remediate its security alerts and archiving is not appropriate
(e.g. a legacy repo awaiting decommission, alerts blocked on an upstream fix), you can request
that it be added to the exemption list.

**Exempt repos are still scanned** and their alerts appear in org-wide security reports, but no
tracking issue is created and the Enforcer will never archive them.

> **Exemption is a last resort.** Before requesting, check whether the alert can be
> [dismissed](https://docs.github.com/en/code-security/dependabot/dependabot-alerts/dismissing-dependabot-alerts)
> in the GitHub Security tab as a false positive or not applicable.

### How to request

1. [Open an issue](https://github.com/IBM/security-ops-bot/issues/new/choose) using the **"Request security enforcement exemption"** template.
2. Set the issue title to `[EXEMPT REQUEST] <repo-name>` (the template pre-fills this).
3. Fill in the justification in the issue body.
4. Submit — within 10 minutes you will receive an **"Awaiting approval"** comment confirming
   the request was received and notifying the review team.
5. A security team member will review your request. Once approved (by adding the `approved`
   label), the automation runs within 10 minutes and will:
   - Add your repository to the exemption list.
   - Close the open security tracking issue in your repository with a comment linking back here.
   - Post a confirmation comment on this issue and close it.

> **Note:** only IBM GitHub org members with Write access to this repo can add the `approved`
> label. If your request has been waiting more than a few business days, contact the IBM GitHub
> org administrators.

## Documentation

| Page | Description |
|---|---|
| [Security Issue Guide](https://ibm.github.io/security-ops-bot/security-issue-guide.html) | Explains the security tracking issue opened by the bot and what repo admins need to do |

## How the bot works

The bot runs as a GitHub App installed on the IBM GitHub org. Four components run on a daily
schedule from the private `opentech-security-ops` repo:

| Component | Schedule (UTC) | What it does |
|---|---|---|
| Dependabot Scanner | 06:00 daily | Scans all org repos for open Dependabot vulnerability alerts |
| Code & Secret Scanner | 07:00 daily | Scans all org repos for open code scanning and secret scanning alerts |
| Enforcer | 08:00 daily | Evaluates SLA deadlines, posts warnings, archives repos that breach their deadline |
| Exempt Request Processor | Every 10 minutes | Processes approved exemption requests submitted via issues in this repo |
