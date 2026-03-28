---
spec: readme-structure
version: "1.0.0"
description: README structure with table of contents, collapsible folder tree, agent table, and prerequisite warnings
extracted_from: paulwu/agent365-management
requires: []
variables:
  - name: PROJECT_NAME
    description: "Name of the project"
    required: true
    example: "Agent 365 Management"
  - name: PROJECT_DESCRIPTION
    description: "One-line description"
    required: true
    example: "Knowledge base for Microsoft Agent 365 management"
  - name: COPILOT_PRIMER_PATH
    description: "Path to the Copilot primer documentation"
    required: false
    default: "docs/github-copilot-primer/README.md"
---

# README Structure Spec

## Pattern

### Section Order

The README should follow this structure:

```
1. Title (# Project Name — Repository Guide)
2. Purpose (what the project does, agent table)
3. Table of Contents (links to all major sections)
4. How to Use This Repository
   - Topic guides table
   - Source material reference
   - Updating documentation
5. Using the Copilot Agents
   - Prerequisites for wizard agents
   - Agent examples (one section per agent)
   - Priority scale reference (if using notes conventions)
6. Folder Structure (collapsible, at the end)
```

### Agent Table

Near the top, after the Purpose description:

```markdown
The repository includes N custom [Copilot agents]({{COPILOT_PRIMER_PATH}}):

| Agent | Invoke with | Purpose |
|---|---|---|
| **Agent Name** | `@agent-name` | Description. **Requires interactive mode.** (if wizard) |
```

### Table of Contents

After the agent table, add a TOC with links to all major sections:

```markdown
## Table of Contents

- [How to Use This Repository](#how-to-use-this-repository)
- [Using the Copilot Agents](#using-the-copilot-agents)
- [Folder Structure](#folder-structure)
```

### Prerequisite Warning for Wizard Agents

Before the agent usage examples:

```markdown
#### ⚠️ Before Using the Wizard Agents

The wizard agents require interactive input and Azure access. Before invoking them:

1. **Switch to interactive mode** — Press **Shift+Tab** to exit autopilot mode.
2. **Log in to Azure CLI** — Run `az login` first.
3. **Ensure PowerShell 7 is installed** — Run `pwsh --version`.
```

### Collapsible Folder Structure

At the END of the README, use HTML `<details>` for the folder tree:

```html
## Folder Structure

<details>
<summary>Click to expand the full directory tree</summary>

\```
Project/
├── folder/     ← description
│   └── file    description
\```

</details>
```

This keeps the folder structure available but doesn't clutter the main content.

### Topic Guide Tables

Use two tables — one for primary/pillar documents, one for additional guides:

```markdown
### Looking for guidance on a specific topic?

| Document | Covers |
|---|---|
| [doc-name.md](path) | **Topic** — brief description |

Additional topic guides:

| Document | Covers |
|---|---|
| [doc-name.md](path) | Brief description |
```
