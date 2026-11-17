# AI Agents Configuration Hub (`.agents`)

The `.agents/` directory is the Bounded Context for AI behavior customization, tool integration, and knowledge routing within the `org-ecosystem` product portfolio meta-repository.

---

## Architecture & Integration

Our AI agent configuration at the `org-ecosystem` meta-repository root consumes the local `agent-mesh` domain plugins directly via relative filesystem path:

### 1. Plugin Discovery Manifest (`plugins.json`)

```json
{
  "entries": [
    {
      "path": "../org-core/agent-mesh/plugins/packages"
    },
    {
      "path": "../../org-core/agent-mesh/plugins/packages"
    }
  ]
}
```

All 10 domain plugins (`appsheet`, `atelier`, `docusaurus`, `github-flow`, `github-org`, `gwork`, `repo`, `research`, `secrets`, `web`) and 8 sovereign MCP servers are loaded directly from the local `org-core/agent-mesh` repository on the workstation.

### 2. Sovereign MCP Launchers

MCP servers bundled in `@tupynambalucas-dev/agent-mesh` execute via self-contained launchers (`scripts/launcher.cjs`) without requiring external path resolutions.

---

## Directory Layout

- [plugins.json](./plugins.json): Runtime plugin discovery manifest.
- [AGENTS.md](./AGENTS.md): Bounded context router for `.agents/`.
- [plans/](./plans/): Portfolio-level architectural plans, technical analyses, and governance reports.

---

## Navigation

- Parent Workspace: [Org-Ecosystem Meta-Repository Root](../README.md)
