# Contributing to Bishop

Thank you for your interest in contributing to Bishop! This document provides guidelines and instructions for contributing.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How to Contribute](#how-to-contribute)
- [Pattern Guidelines](#pattern-guidelines)
- [Directory Structure](#directory-structure)
- [Submitting Changes](#submitting-changes)
- [Testing Patterns](#testing-patterns)

---

## Code of Conduct

- Be respectful and inclusive
- Focus on constructive feedback
- Help maintain a welcoming environment for all contributors

---

## How to Contribute

### Reporting Issues

1. Check if the issue already exists
2. Create a new issue with:
   - Clear description of the problem
   - Steps to reproduce (if applicable)
   - Expected vs actual behavior
   - Sample data that triggers false positives/negatives

### Adding New Patterns

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/new-pattern-name`
3. Add your pattern(s) to the appropriate category file
4. Test your patterns thoroughly
5. Submit a pull request

---

## Pattern Guidelines

### Pattern Structure

All patterns must follow this YAML structure:

```yaml
patterns:
  - pattern:
      name: "Pattern Name"
      regex: "your-regex-pattern"
      confidence: "High|Medium|Low"
```

### Confidence Levels

- **High/Critical**: Pattern is highly specific with minimal false positives (e.g., `sk_live_[0-9a-zA-Z]{24}` for Stripe)
- **Medium**: Pattern is reasonably specific but may have some false positives
- **Low/Info**: Pattern is generic and may require manual review

### Regex Best Practices

1. **Be Specific**: Use specific prefixes/suffixes when available
   ```yaml
   # Good - specific prefix
   regex: "ghp_[0-9a-zA-Z]{36}"
   
   # Avoid - too generic
   regex: "[a-zA-Z0-9]{40}"
   ```

2. **Use Word Boundaries**: Prevent partial matches
   ```yaml
   regex: "\\b[A-Z0-9]{20}\\b"
   ```

3. **Escape Special Characters**: Properly escape regex metacharacters
   ```yaml
   regex: "https://hooks\\.slack\\.com/services/T[0-9A-Z]{8,10}/B[0-9A-Z]{8,10}/[0-9a-zA-Z]{24}"
   ```

4. **Use Non-Capturing Groups**: When grouping without capture
   ```yaml
   regex: "(?:sk|pk)_live_[0-9a-zA-Z]{24}"
   ```

5. **Test Edge Cases**: Consider various contexts where secrets appear
   - In JSON: `"apiKey": "value"`
   - In env files: `API_KEY=value`
   - In code: `const apiKey = 'value'`

### Naming Conventions

- Use descriptive, clear names
- Include the service name: "Stripe Secret Key", "AWS Access Key"
- Be consistent with existing patterns

---

## Directory Structure

Place your patterns in the appropriate category:

```
patterns/
├── api-keys/              # Third-party API keys (OpenAI, Twilio, etc.)
├── authentication/        # Cryptographic keys, tokens, OAuth patterns
├── cloud-providers/       # AWS, GCP, Azure credentials
├── communication/         # Slack, Discord, email service tokens
├── custom/                # User-defined custom patterns
├── databases/             # Database connection strings
├── devops/                # CI/CD, infrastructure secrets
├── frameworks/            # React, Vue, Angular, Node.js patterns
├── generic/               # Generic credential patterns
├── mobile/                # Mobile app specific patterns
├── payment/               # Stripe, PayPal, payment processor keys
├── personal-data/         # PII patterns (SSN, credit cards, etc.)
└── third-party-rules/     # External rule sets (Nuclei, TruffleHog)
```

### Choosing the Right Category

| Pattern Type | Directory |
|-------------|-----------|
| Stripe, PayPal, Square keys | `payment/` |
| AWS, GCP, Azure credentials | `cloud-providers/` |
| Slack, Discord, Twilio tokens | `communication/` |
| MongoDB, PostgreSQL connection strings | `databases/` |
| JWT, RSA keys, OAuth tokens | `authentication/` |
| React env vars, Express secrets | `frameworks/` |

---

## Submitting Changes

### Pull Request Process

1. **Update Documentation**: If adding new categories or significant patterns
2. **Follow Formatting**: Match existing YAML style and indentation
3. **Write Clear Commit Messages**:
   ```
   feat: Add Anthropic API key pattern
   fix: Update OpenAI key regex for new format
   docs: Update README with new category
   ```
4. **Reference Issues**: Link related issues in your PR description

### PR Checklist

- [ ] Pattern follows the required YAML structure
- [ ] Confidence level is appropriate
- [ ] Pattern is placed in the correct category
- [ ] No duplicate patterns exist
- [ ] Regex has been tested against sample data
- [ ] No sensitive data included in examples

---

## Testing Patterns

### Manual Testing

Test your regex patterns using:

```bash
# Using grep
echo "sk_live_abcd1234567890abcdef1234" | grep -E "sk_live_[0-9a-zA-Z]{24}"

# Using Python
import re
pattern = r"sk_live_[0-9a-zA-Z]{24}"
test_string = "sk_live_abcd1234567890abcdef1234"
print(re.search(pattern, test_string))
```

### Online Tools

- [regex101.com](https://regex101.com/) - Test and debug regex
- [regexr.com](https://regexr.com/) - Visual regex testing

### Test Cases to Consider

1. **True Positives**: Valid secrets that should match
2. **True Negatives**: Non-secrets that should NOT match
3. **Edge Cases**: Secrets in various contexts (JSON, env files, code)

---

## Questions?

Feel free to open an issue for any questions about contributing!

---

Thank you for helping make Bishop better!
