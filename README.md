# 🕵️‍♂️ Bishop - JavaScript Leak Detector

**Bishop** is a collection of carefully crafted Regular Expressions (regex) used to detect sensitive information leaks in JavaScript codebases. Whether it's exposed API keys, secrets, passwords, or configuration files — Bishop helps identify and alert developers and security researchers to these critical issues fast and effectively.

> 🔗 **Repo:** [https://github.com/the5orcerer/Bishop](https://github.com/the5orcerer/Bishop)

---

## 🚀 Features

* 🧠 High-confidence regex patterns for detecting:

  * API keys
  * Secrets & tokens
  * User credentials
  * Commented-out sensitive data
  * Cloud provider credentials (AWS, GCP, Azure, etc.)
* 🔍 Ready-to-use YAML structure for integration with tools
* 🔧 Simple integration into scanners, linters, CI/CD pipelines
* 💡 Open-source and customizable

---

## 📦 Pattern Categories

All patterns follow this structure:

```yaml
patterns:
  - pattern:
      name: <Pattern Name>
      regex: <Regex>
      confidence: <low|medium|high>
```

---

### 🔐 Password and Credential Patterns

```yaml
- pattern:
    name: Generic Password
    regex: "(?i)\\b(pass|password|passwd|pwd|passcode|passphrase|pin)\\b\\s*[:=]\\s*['\"]?([a-zA-Z0-9@#$_%&*!+-]{8,})['\"]?"
    confidence: high
```

---

### 👤 Username and Identity Patterns

```yaml
- pattern:
    name: Generic Username
    regex: "(?i)\\b(user|username|login|usr|uid|userid|uname|admin_user|root_user|db_user|email)\\b\\s*[:=]\\s*['\"]?([a-zA-Z0-9-_@.]{5,})['\"]?"
    confidence: medium
```

---

### 🔑 Secret, Token, and Key Patterns

```yaml
- pattern:
    name: Generic Secret
    regex: "(?i)\\b(secret|token|auth_token|api_key|apiKey|access_token|session_token|jwt_token|encryption_key|ssh_key|crypt_key|access_key)\\b\\s*[:=]\\s*['\"]?([a-zA-Z0-9-_]{8,})['\"]?"
    confidence: high
```

---

### 💬 Sensitive Information in Comments

```yaml
- pattern:
    name: Sensitive Comment
    regex: "(?i)(?:#|\\/\\/|\\/\\*|<!--)\\s*(pass|password|passwd|pwd|user|username|secret|token|auth_token|api_key|apiKey|access_key)\\s*[:=]\\s*['\"]?([a-zA-Z0-9@#$_%&*!+-]{5,})['\"]?"
    confidence: low
```

---

## 🛠 Usage

You can integrate Bishop regex patterns with:

* Static code analysis tools
* CI/CD pipeline scanners (like GitHub Actions, GitLab CI, etc.)
* Custom Python or Node.js scripts for repo audits
* Git hooks or pre-commit scanners

**Example Python parser coming soon in `/scripts` folder.**

---

## 📂 Roadmap

* [ ] Add patterns for third-party service keys (Stripe, Firebase, Twilio)
* [ ] Integrate auto-scanner script
* [ ] VS Code plugin support
* [ ] Add example usage with `grep`, `ripgrep`, or custom scanner

---

## 🙌 Contributing

We welcome PRs for:

* New regex patterns
* Improvements to pattern accuracy
* Usage scripts
* Documentation

Please follow the contribution guidelines in `CONTRIBUTING.md`.

---

## 📜 License

This project is licensed under the **MIT License**. See `LICENSE` for more information.

---

## 🔗 Stay Connected

Made with ❤️ by [the5orcerer](https://github.com/the5orcerer)

Join the mission to eliminate JavaScript leaks — one pattern at a time.
