# Curated Advisor Specs

Reusable, parameterized [Copilot agent](https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-custom-agents) patterns for documentation knowledge bases — extracted from real projects and designed to be imported into any repository.

## Documentation

👉 **[Full documentation →](docs/spec-driven-development/README.md)**

- [Spec File Format Reference](docs/spec-driven-development/spec-format.md) — YAML frontmatter, `{{VARIABLE}}` syntax, manifest and project config schemas
- [FAQ](docs/spec-driven-development/faq.md) — How export/import works, applying to other projects, drift detection, overrides

## Available Specs

| Spec | What It Captures |
|---|---|
| [`grounding-rules`](specs/grounding-rules.spec.md) | Source priority hierarchy, contradiction detection, citation format |
| [`notes-conventions`](specs/notes-conventions.spec.md) | YAML frontmatter (`Author`, `Priority`), priority scale (1-5+) |
| [`wizard-agent`](specs/wizard-agent.spec.md) | Prerequisite checks, `az account show` detection, autopilot warning, command generation |
| [`research-agent`](specs/research-agent.spec.md) | Fetch live docs, cross-reference cached notes, flag contradictions, save response |
| [`doc-architecture`](specs/doc-architecture.spec.md) | `notes/` → `docs/` → `scripts/` three-layer architecture |
| [`readme-structure`](specs/readme-structure.spec.md) | README with TOC, collapsible folder tree, agent table, prerequisite warnings |

## Quick Start

### 1. Copy the meta-agents into your project

```bash
mkdir -p your-project/.github/agents
cp .github/agents/Spec-Importer.agent.md your-project/.github/agents/
cp .github/agents/Spec-Exporter.agent.md your-project/.github/agents/
cp .github/agents/Spec-Drift.agent.md    your-project/.github/agents/
```

### 2. Import specs (interactive mode — press Shift+Tab first)

```
@spec-importer Import grounding-rules and research-agent specs from ~/curated-advisor-specs/specs/
```

The importer collects your project-specific values (URLs, folder names, agent names) and generates the corresponding files.

### 3. Check for drift later

```
@spec-drift Compare this project against its imported specs
```

## Projects Using These Specs

| Project | Specs Imported |
|---|---|
| [agent365-management](https://github.com/paulwu/agent365-management) | All 6 specs (reference implementation) |

## How It Was Built

These specs were extracted from the [agent365-management](https://github.com/paulwu/agent365-management) project, which is a documentation knowledge base for Microsoft Agent 365 / Entra Agent ID. The patterns evolved over iterative development and were generalized into parameterized specs so they can be reused across repositories.

## License

This project is licensed under the [GNU General Public License v2.0](LICENSE).
