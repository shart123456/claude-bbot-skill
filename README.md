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
bbot/
├── SKILL.md                                  - Skill definition, triggers, workflow routing
├── configs/                                  - API key templates, custom preset YAMLs
├── data/                                     - Wordlists, target scope files
├── documentation/
│   ├── bbot_technical_reference.md           - Full BBOT config and architecture reference
│   ├── modules_cloud_enumeration.md          - Cloud and storage modules
│   ├── modules_code_repository.md            - GitHub, GitLab, Postman, Docker modules
│   ├── modules_dns_subdomain_enum.md         - DNS and subdomain enumeration modules
│   ├── modules_email_credentials.md          - Email and credential discovery modules
│   ├── modules_ip_intelligence.md            - IP intelligence and tech detection modules
│   ├── modules_output_modules.md             - Output and reporting modules
│   ├── modules_port_scanning.md              - Port scanning and service detection modules
│   ├── modules_vulnerability_scanning.md     - Vulnerability scanning modules
│   └── modules_web_scanning.md               - Web scanning and fuzzing modules
├── examples/                                 - Sample execution flows
├── playbooks/                                - Multi-workflow orchestration guides
├── cauldron/                                 - Runtime scan artifacts and output
├── resources/                                - Helper scripts and API integration docs
├── templates/                                - Scan report output templates
└── workflows/
    ├── passive_recon.md                      - Zero-contact recon, API sources only
    ├── safe_active_recon.md                  - Light active scanning, safe for most programs
    ├── full_engagement.md                    - Comprehensive 8-phase engagement
    ├── subdomain_takeover.md                 - Dangling DNS and zone takeover detection
    ├── vuln_scan.md                          - Nuclei + badsecrets + baddns
    ├── cloud_hunt.md                         - S3, GCS, Azure blob enumeration
    ├── web_app_audit.md                      - Parameter mining, fuzzing, secret detection
    └── code_leak_hunt.md                     - GitHub, GitLab, Postman, Trufflehog
```

## Workflows

| Workflow | Description |
|---|---|
| `passive_recon` | No direct target interaction, API sources only |
| `safe_active_recon` | Light active scanning, safe for most programs |
| `full_engagement` | Comprehensive 8-phase scan for permissive scopes |
| `subdomain_takeover` | Detect dangling DNS and takeover candidates |
| `vuln_scan` | Nuclei + badsecrets + baddns on live hosts |
| `cloud_hunt` | S3, GCS, Azure blob enumeration |
| `web_app_audit` | Parameter mining, secret detection, web fuzzing |
| `code_leak_hunt` | GitHub, GitLab, Postman, Trufflehog |

## Requirements

- BBOT v2.8.2+ installed at `/opt/bbot/`
- Claude Code with skills support

## Setup After Cloning

**1. Clone the repo**

```bash
git clone git@github.com:shart123456/claude-bbot-skill.git
```

**2. Place it in your Claude Code skills directory**

```bash
mv claude-bbot-skill ~/.claude/skills/bbot
```

**3. Verify Claude Code picks it up**

```bash
ls ~/.claude/skills/bbot/SKILL.md
```

Claude Code automatically loads skills from `~/.claude/skills/`. No additional configuration required.

**4. Set up API keys (optional but recommended)**

The passive recon workflow benefits from several API keys. Add these to your shell profile (`~/.bashrc` or `~/.zshrc`):

```bash
export GITHUB_TOKEN="ghp_..."
export SHODAN_KEY="..."
export VT_KEY="..."                # VirusTotal
export ST_KEY="..."                # SecurityTrails
export CHAOS_KEY="..."             # ProjectDiscovery Chaos
export HUNTER_KEY="..."            # Hunter.io
export CENSYS_ID="..."
export CENSYS_SECRET="..."
export POSTMAN_KEY="..."
export WPSCAN_KEY="..."
```

Free API keys available at: GitHub, VirusTotal, Hunter.io, Chaos (chaos.projectdiscovery.io), WPScan.

**5. Verify BBOT is installed**

```bash
bbot --version
# Should output: bbot 2.8.x
```

If not installed:

```bash
pip install bbot
# or
pipx install bbot
```

## Usage

Once installed, activate by saying things like:

- "Run BBOT scan for [company]"
- "Enumerate subdomains for [target]"
- "Check for subdomain takeover on [target]"
- "Scan for S3 buckets for [company]"
- "Run nuclei on [target]"
- "Passive recon on [target]"
- "Full engagement on [target]"
