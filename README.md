# QA Interview Bible

A professional documentation site for QA knowledge, interview preparation, testing strategy, and career growth.

## Overview

This repository is built with MkDocs Material and organized as a reusable knowledge base for software quality professionals. It is designed to grow into a structured reference covering hands-on QA topics, interview preparation, leadership notes, real bug case studies, and company research.

## Documentation Sections

- Career
- Resume
- Interview
- QA
- Mobile
- Automation
- Nook
- AI Testing
- API
- Leadership
- Real Bugs
- Company
- Writing Templates

## Local Preview

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

GitHub Actions automatically builds and deploys the documentation site to GitHub Pages on every push to `master`.

Expected site URL:

- `https://shihweihung.github.io/qa-interview-bible/`

## Writing Workflow

- Content is written in Markdown only.
- Keep one topic per page.
- Use lowercase filenames.
- Use descriptive headings.

Reusable page templates are available in [docs/writing-templates](/Users/swi/qa-interview-bible/docs/writing-templates).

## Contributing

See [CONTRIBUTING.md](/Users/swi/qa-interview-bible/CONTRIBUTING.md) for documentation rules, required article structure, and naming conventions.
