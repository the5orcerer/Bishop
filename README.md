# Bishop - Secret Detection Patterns

**Bishop** is a comprehensive collection of carefully crafted Regular Expressions (regex) used to detect sensitive information leaks in codebases. Whether it's exposed API keys, secrets, passwords, database credentials, or configuration files — Bishop helps identify and alert developers and security researchers to these critical issues fast and effectively.

> **Repo:** [https://github.com/the5orcerer/Bishop](https://github.com/the5orcerer/Bishop)

---

## Features

* High-confidence regex patterns for detecting:
  * API keys (OpenAI, Stripe, AWS, GCP, Azure, and 50+ services)
  * Authentication tokens (JWT, OAuth, Bearer tokens)
  * Cloud provider credentials (AWS, GCP, Azure, DigitalOcean)
  * Database connection strings (MongoDB, PostgreSQL, MySQL, Redis)
  * Payment processor keys (Stripe, PayPal, Square, Braintree)
  * Communication service tokens (Slack, Discord, Twilio, SendGrid)
  * Private keys and certificates (RSA, SSH, PGP)
  * Personal identifiable information (PII)
* Ready-to-use YAML structure for integration with tools
* Simple integration into scanners, linters, CI/CD pipelines
* Open-source and customizable

---

## Directory Structure

Patterns are organized into categories for easy navigation:

```
patterns/
├── api-keys/              # Third-party API keys (OpenAI, Twilio, GitHub, etc.)
├── authentication/        # Cryptographic keys, tokens, JWT, OAuth patterns
├── cloud-providers/       # AWS, GCP, Azure, DigitalOcean credentials
├── communication/         # Slack, Discord, email service tokens
├── custom/                # User-defined custom patterns
├── databases/             # Database connection strings and credentials
├── devops/                # CI/CD, Docker, Kubernetes, Terraform secrets
├── frameworks/            # React, Vue, Angular, Node.js specific patterns
├── generic/               # Generic credential and secret patterns
├── mobile/                # Mobile app specific patterns (React Native, Ionic)
├── payment/               # Stripe, PayPal, Square payment processor keys
├── personal-data/         # PII patterns (SSN, credit cards, phone numbers)
└── third-party-rules/     # External rule sets (Nuclei, TruffleHog)
```

---

## Pattern Format

All patterns follow this YAML structure:

```yaml
patterns:
  - pattern:
      name: "Pattern Name"
      regex: "regex-pattern"
      confidence: "High|Medium|Low"
```

### Confidence Levels

| Level | Description |
|-------|-------------|
| **High/Critical** | Highly specific patterns with minimal false positives |
| **Medium** | Reasonably specific, may require some review |
| **Low/Info** | Generic patterns, higher false positive rate |

---

## Example Patterns

### AWS Access Key

```yaml
- pattern:
    name: "AWS Access Key ID"
    regex: "AKIA[0-9A-Z]{16}"
    confidence: "High"
```

### Stripe Secret Key

```yaml
- pattern:
    name: "Stripe Secret Key"
    regex: "sk_live_[0-9a-zA-Z]{24}"
    confidence: "High"
```

### JWT Token

```yaml
- pattern:
    name: "JWT Token"
    regex: "eyJ[A-Za-z0-9-_=]+\\.eyJ[A-Za-z0-9-_=]+\\.?[A-Za-z0-9-_.+/=]*"
    confidence: "Medium"
```

### Database Connection String

```yaml
- pattern:
    name: "MongoDB Connection String"
    regex: "mongodb(?:\\+srv)?://[a-zA-Z0-9_-]+:[a-zA-Z0-9_-]+@[a-zA-Z0-9.-]+"
    confidence: "High"
```

---

## Usage

### With grep/ripgrep

```bash
# Search for AWS keys
rg "AKIA[0-9A-Z]{16}" ./src

# Search for Stripe keys
grep -rE "sk_live_[0-9a-zA-Z]{24}" ./
```

### With Python

```python
import re
import yaml

# Load patterns
with open('patterns/api-keys/api-keys.yaml', 'r') as f:
    data = yaml.safe_load(f)

# Search in code
code = open('app.js').read()
for item in data['patterns']:
    pattern = item['pattern']
    matches = re.findall(pattern['regex'], code)
    if matches:
        print(f"Found {pattern['name']}: {matches}")
```

### Integration Examples

* **CI/CD Pipelines**: GitHub Actions, GitLab CI, Jenkins
* **Pre-commit Hooks**: Prevent secrets from being committed
* **Static Analysis**: Integrate with custom scanners
* **IDE Plugins**: VS Code, JetBrains extensions

---

## Quick Start

1. Clone the repository:
   ```bash
   git clone https://github.com/the5orcerer/Bishop.git
   ```

2. Browse patterns by category:
   ```bash
   ls patterns/
   ```

3. Use patterns in your scanner or tool of choice

---

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on:

* Adding new patterns
* Improving existing patterns
* Reporting false positives/negatives
* Documentation improvements

---

## Roadmap

- [x] Organize patterns into categories
- [x] Add contribution guidelines
- [ ] Add automated testing for patterns
- [ ] Create VS Code extension
- [ ] Add example scanner scripts
- [ ] Integrate with TruffleHog/Gitleaks formats

---

## License

This project is licensed under the **MIT License**. See `LICENSE` for more information.

---

## Stay Connected

Made with care by [the5orcerer](https://github.com/the5orcerer)

Join the mission to eliminate secret leaks — one pattern at a time.
