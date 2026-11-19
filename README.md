# 50 Secure Code Review Projects

A practical, portfolio-focused collection of 50 secure code review and application security projects. The collection progresses from foundational source review to advanced application, architecture, and pipeline assessments.

> **Training-lab notice:** Code snippets and findings in this repository are intentionally designed for authorized education. Screenshots are simulated illustrations using fictional code, tools, and results; they are not evidence from a real assessment. Run exercises only against code and systems you own or are explicitly authorized to assess.

## Learning path

| Level | Projects | Focus |
|---|---:|---|
| Beginner | 01–15 | Review fundamentals, common languages, input handling, authentication, and secure coding standards |
| Intermediate | 16–35 | Authorization, APIs, injection classes, cryptography, dependencies, containers, and IaC |
| Advanced | 36–50 | Frameworks, architecture, CI/CD, SAST customization, CodeQL, and end-to-end assessments |

## Beginner projects

| # | Project | Main focus |
|---:|---|---|
| 01 | [Secure Code Review Lab Setup](projects/beginner/01-secure-code-review-lab-setup/README.md) | Build a safe local review environment |
| 02 | [Source Code Security Review Fundamentals](projects/beginner/02-source-code-review-fundamentals/README.md) | Establish a repeatable manual review method |
| 03 | [Python Code Security Review](projects/beginner/03-python-code-security-review/README.md) | Identify and remediate common Python weaknesses |
| 04 | [JavaScript Code Security Review](projects/beginner/04-javascript-code-security-review/README.md) | Review browser and server-side JavaScript patterns |
| 05 | [PHP Code Security Review](projects/beginner/05-php-code-security-review/README.md) | Review PHP input, output, and database handling |
| 06–15 | Planned | SQL injection, XSS, secrets, authentication, password storage, validation, uploads, and standards |

## Intermediate projects

Projects 16–35 will cover access control, IDOR, JWT, OAuth 2.0, sessions, REST and GraphQL APIs, SSRF, command injection, path traversal, deserialization, cryptography, business logic, race conditions, XXE, CORS, dependencies, logging, Docker, and infrastructure as code.

## Advanced projects

Projects 36–50 will cover advanced language/framework reviews, multi-tenant systems, microservices, CI/CD, secrets and security architecture, SAST, custom Semgrep rules, CodeQL, OWASP Top 10 reviews, and a complete enterprise code review.

## Standard project deliverables

Each walkthrough aims to include:
- Scope, objectives, prerequisites, and lab safety notes
- A small, intentionally vulnerable training example
- Manual review steps and relevant tool commands
- Simulated editor, scan, and findings screenshots (clearly labeled)
- Finding explanation, CWE/OWASP mapping, and severity rationale
- Secure remediation and validation steps
- Evidence notes and a concise report template

## Suggested tools

- Code editors: Visual Studio Code or another editor of choice
- SAST: Semgrep, CodeQL, and language-native analyzers
- Dependency review: OSV-Scanner and package-manager audit tools
- Manual review: source search, data-flow tracing, and framework documentation

## Repository structure

```text
projects/
  beginner/
    01-secure-code-review-lab-setup/
    02-source-code-review-fundamentals/
    03-python-code-security-review/
    04-javascript-code-security-review/
    05-php-code-security-review/
  intermediate/
  advanced/
_assets/
  screenshots/
```

## Disclaimer

This repository is for defensive education and authorized secure development. Examples are intentionally simplified and may omit production concerns. Do not use the exercises to test third-party systems without written permission.
