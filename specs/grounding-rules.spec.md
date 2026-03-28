---
spec: grounding-rules
version: "1.0.0"
description: Source priority hierarchy, contradiction detection, and citation format for knowledge-base repositories
extracted_from: paulwu/agent365-management
requires: []
variables:
  - name: PRIMARY_SOURCE_URL
    description: "The authoritative documentation URL (highest-priority source)"
    required: true
    example: "https://learn.microsoft.com/en-us/entra/agent-id/"
  - name: PRIMARY_SOURCE_NAME
    description: "Human-readable name for the primary source"
    required: true
    example: "Microsoft Learn"
  - name: CACHED_BASELINE_FILE
    description: "Path to the cached baseline note file"
    required: true
    example: "notes/Microsoft-Learn-Entra-AgentID.md"
  - name: SECONDARY_NOTE_FILES
    description: "Comma-separated list of secondary research note filenames"
    required: false
    default: ""
    example: "ChatGPT.md, Gemini.md, Researcher.md"
  - name: NOTES_FOLDER
    description: "Folder containing research notes"
    required: false
    default: "notes"
  - name: DOCS_FOLDER
    description: "Folder containing generated documentation"
    required: false
    default: "docs"
---

# Grounding Rules Spec

## Pattern

### Source Hierarchy

All factual answers must follow this priority order:

1. **Live content** from `{{PRIMARY_SOURCE_URL}}` — always the highest-authority source
2. **Cached baseline** in `{{CACHED_BASELINE_FILE}}` — use when live fetches are unavailable
3. **Secondary research notes** in `{{NOTES_FOLDER}}/` ({{SECONDARY_NOTE_FILES}}) — supporting context only
4. **Generated docs** in `{{DOCS_FOLDER}}/` — treat as output, NOT as a factual source of truth

### Contradiction Detection

When information from a note in `{{NOTES_FOLDER}}/` conflicts with live or cached {{PRIMARY_SOURCE_NAME}} content:

1. **Flag the contradiction explicitly** with a ⚠️ warning
2. **List every conflicting source** — include the note's file path, Author (from frontmatter), and Priority alongside the {{PRIMARY_SOURCE_NAME}} page URL
3. **Prefer the {{PRIMARY_SOURCE_NAME}} version** as authoritative
4. Still show the disagreeing note's content so the user can decide whether to update it
5. Remind the user they can correct the note using `@notes-author`

### Contradiction Output Template

```
⚠️ **Contradiction detected:**

| Source | Says | Author | Priority |
|---|---|---|---|
| {{PRIMARY_SOURCE_NAME}} ([Page Title](url)) | <what the primary source says> | — | — |
| `{{NOTES_FOLDER}}/<file>.md` | <what the note says> | <Author from frontmatter> | <Priority> |

**The {{PRIMARY_SOURCE_NAME}} version is authoritative.** If the note is outdated, you can update it with `@notes-author`.
```

### Priority-Based Conflict Resolution

When two notes disagree with each other (not with the primary source):

- **Lower Priority number = higher importance** — prefer the note with the lower number
- **Always present both sides** — list every conflicting note with file path, Author, and Priority
- When citing a note, include its `Author` (from the YAML frontmatter)

### copilot-instructions.md Template

Add this to `.github/copilot-instructions.md` under "Canonical sources and grounding":

```markdown
## Canonical sources and grounding

- Treat live content under `{{PRIMARY_SOURCE_URL}}` as the highest-authority source.
- Use `{{CACHED_BASELINE_FILE}}` as the cached baseline when live fetches are unavailable.
- Use other files in `{{NOTES_FOLDER}}/` ({{SECONDARY_NOTE_FILES}}) as secondary research only.
- Treat `{{DOCS_FOLDER}}/` as generated output, not as the factual source of truth.
- If a source disagrees with {{PRIMARY_SOURCE_NAME}}, call out the contradiction explicitly, prefer {{PRIMARY_SOURCE_NAME}}, and include the URL for manual verification.
```
