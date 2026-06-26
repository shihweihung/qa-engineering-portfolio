# QA Interview Bible

QA Interview Bible is a long-term public knowledge base for software quality, testing, and engineering communication. It is designed to be professional, reusable, and safe to share with future employers.

## Repository purpose

This repository exists to document durable software engineering knowledge, especially in areas such as:

- quality engineering fundamentals
- test strategy and planning
- automation design
- API and mobile testing
- debugging and defect analysis
- interview preparation
- technical leadership and communication

The goal is not to preserve company-specific implementation details. The goal is to publish educational material that remains useful across teams, products, and industries.

## Public portfolio standards

This repository is public and should always remain suitable for external readers.

- Never include confidential, proprietary, regulated, or internal-only information.
- Generalize all examples, incidents, workflows, architectures, and datasets.
- Focus on transferable engineering reasoning instead of employer-specific process.
- Write every page so it can teach someone outside the original context.

## Governance documents

Repository governance is defined by the following documents:

- [CONTRIBUTING.md](/Users/swi/qa-interview-bible/CONTRIBUTING.md)
- [STYLE_GUIDE.md](/Users/swi/qa-interview-bible/STYLE_GUIDE.md)
- [SECURITY.md](/Users/swi/qa-interview-bible/SECURITY.md)
- [AI_RULES.md](/Users/swi/qa-interview-bible/AI_RULES.md)
- [DISCLAIMER.md](/Users/swi/qa-interview-bible/DISCLAIMER.md)
- [CODE_OF_CONDUCT.md](/Users/swi/qa-interview-bible/CODE_OF_CONDUCT.md)

All contributors should read these files before adding or revising content.

## Documentation sections

- Career
- Resume
- Interview
- QA
- Mobile
- Automation
- eReader
- AI Testing
- API
- Leadership
- Real Bugs
- Company
- Writing Templates

## Writing model

Each article should be:

- educational
- reusable
- technically accurate
- professionally written
- suitable for a public engineering documentation site

Reusable page templates are available in [docs/writing-templates](/Users/swi/qa-interview-bible/docs/writing-templates).

## Local preview

Create a virtual environment and install dependencies:

```bash
python3 -m venv .venv
.venv/bin/pip install --upgrade pip setuptools wheel
.venv/bin/pip install -r requirements.txt
```

Build the site:

```bash
.venv/bin/mkdocs build
```

Serve the site locally:

```bash
.venv/bin/mkdocs serve
```

## Deployment

GitHub Actions builds and deploys the documentation site to GitHub Pages on pushes to `master`.

Published site:

- `https://shihweihung.github.io/qa-interview-bible/`
