# claude-bbot-skill

A Claude Code skill for running BBOT (Bighuge BLS OSINT Tool) scans during bug bounty reconnaissance.

## What it does

Provides Claude with full context to execute intelligent BBOT scans that stay within program scope, respect rate limits, and select appropriate modules based on the engagement type (passive, safe-active, or thorough).

Covers all 117+ BBOT modules organized by category:

- DNS enumeration
- Port scanning
- Web scanning and fuzzing
- Vulnerability scanning
- Cloud storage enumeration
- Code repository discovery
- Email and credential discovery
- Output modules

## Structure

```
SKILL.md                  - Skill definition and activation triggers
CLAUDE.md                 - Full BBOT technical reference
modules/                  - Module documentation by category
workflows/                - Pre-built scan workflows for common scenarios
```

## Workflows

| Workflow | Description |
|---|---|
| `passive-recon` | No direct target interaction, API sources only |
| `safe-active-recon` | Light active scanning, safe for most programs |
| `full-engagement` | Comprehensive scan for permissive scopes |
| `subdomain-takeover` | Detect dangling DNS and takeover candidates |
| `vuln-scan` | Nuclei + badsecrets + baddns on live hosts |
| `cloud-hunt` | S3, GCS, Azure blob enumeration |
| `web-app-audit` | Parameter mining, secret detection, web fuzzing |
| `code-leak-hunt` | GitHub, GitLab, Postman, Trufflehog |

## Requirements

- BBOT v2.8.2+ installed at `/opt/bbot/`
- Claude Code with skills support

## Usage

Activate by saying things like:

- "Run BBOT scan for [company]"
- "Enumerate subdomains for [target]"
- "Check for subdomain takeover on [target]"
- "Scan for S3 buckets for [company]"
- "Run nuclei on [target]"
