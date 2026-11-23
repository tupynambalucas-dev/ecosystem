# AI Agents Configuration Hub (`.agents`)

The `.agents/` directory is the Bounded Context for AI behavior customization, tool integration, and knowledge routing within the `ecosystem` product portfolio meta-repository.

---

## Architecture & Integration

Our AI agent configuration at the `ecosystem` meta-repository root consumes the `agent-mesh` domain plugins directly via relative filesystem path when nested inside `org/` (or via `node_modules` fallback in standalone mode):

### 1. Plugin Discovery Manifest (`plugins.json`)

```json
{
  "entries": [
    {
      "path": "../agent-mesh/plugins/packages"
    },
    {
      "path": "node_modules/@tupynambalucas-dev/agent-mesh/plugins/packages"
    }
  ]
}
```

All 11 domain plugins (`appsheet`, `atelier`, `docusaurus`, `github-actions`, `github-flow`, `github-org`, `github-releases`, `github-repo`, `gwork`, `profile`, `research`, `secrets`, `web`) and 9 sovereign MCP servers are loaded directly from `../agent-mesh/plugins/packages` on the workstation without requiring NTFS directory junctions.

### 2. Sovereign MCP Launchers

MCP servers bundled in `@tupynambalucas-dev/agent-mesh` execute via self-contained launchers (`scripts/launcher.cjs`) without requiring external path resolutions.

---

## Directory Layout

- [plugins.json](./plugins.json): Runtime plugin discovery manifest.
- [AGENTS.md](./AGENTS.md): Bounded context router for `.agents/`.
- [plans/](./plans/): Portfolio-level architectural plans, technical analyses, and governance reports.

---

## Navigation

- Parent Workspace: [Ecosystem Meta-Repository Root](../README.md)
