---
spec: doc-architecture
version: "1.0.0"
description: Three-layer notes → docs → scripts architecture for documentation knowledge bases
extracted_from: paulwu/agent365-management
requires: []
variables:
  - name: RAW_RESEARCH_FOLDER
    description: "Folder for raw research and cached documentation"
    required: false
    default: "notes"
  - name: SYNTHESIZED_DOCS_FOLDER
    description: "Folder for synthesized topic guides"
    required: false
    default: "docs"
  - name: AUTOMATION_FOLDER
    description: "Folder for automation scripts"
    required: false
    default: "scripts"
  - name: PROJECT_NAME
    description: "Name of the project"
    required: true
    example: "Agent 365 Management"
  - name: PROJECT_DESCRIPTION
    description: "One-line description of the project"
    required: true
    example: "Knowledge base for Microsoft Agent 365 management"
---

# Documentation Architecture Spec

## Pattern

### Three-Layer Architecture

The repository has three working layers:

1. **`{{RAW_RESEARCH_FOLDER}}/`** — Raw research and cached documentation (primary knowledge notes)
2. **`{{SYNTHESIZED_DOCS_FOLDER}}/`** — Synthesized topic guides (generated from the research)
3. **`{{AUTOMATION_FOLDER}}/`** — Automation scripts and tooling that operationalize the documentation

### Information Flow

```
{{RAW_RESEARCH_FOLDER}}/     →    {{SYNTHESIZED_DOCS_FOLDER}}/     →    {{AUTOMATION_FOLDER}}/
(raw research)                (synthesized guides)              (operational scripts)
```

- **New information** → add to `{{RAW_RESEARCH_FOLDER}}/` first
- **End-user guides** → generate or update in `{{SYNTHESIZED_DOCS_FOLDER}}/`
- **Operational automation** → implement in `{{AUTOMATION_FOLDER}}/`

### Rules

- Keep factual answers grounded in the primary source first, then `{{RAW_RESEARCH_FOLDER}}/`
- Do not answer from `{{SYNTHESIZED_DOCS_FOLDER}}/` alone — it's generated output, not the source of truth
- If you add or remove any file in `{{SYNTHESIZED_DOCS_FOLDER}}/`, update `README.md` in both the structure listing and the topic-guide table
- Add new research to `{{RAW_RESEARCH_FOLDER}}/`; add or update end-user guides in `{{SYNTHESIZED_DOCS_FOLDER}}/`

### copilot-instructions.md Template

```markdown
## Repository architecture

The repository has three working layers:

1. `{{RAW_RESEARCH_FOLDER}}/` stores raw research and cached documentation.
2. `{{SYNTHESIZED_DOCS_FOLDER}}/` stores synthesized topic guides generated from those sources.
3. `{{AUTOMATION_FOLDER}}/` stores automation scripts and tooling.
```

### Documentation Conventions

- Use `###` step-oriented headings in `{{SYNTHESIZED_DOCS_FOLDER}}/`
- Use Markdown tables for role/license/permission mappings
- Include `References` sections with primary source links
- Use Mermaid diagrams for multi-step relationships
