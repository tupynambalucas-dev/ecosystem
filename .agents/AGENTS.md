<context-hierarchy>
  <parent src="../AGENTS.md" type="global-rules" />
  <system-instruction>
    AGENT: You are operating in the .agents bounded context of tupynambalucas-dev/org-ecosystem. If you have not read ../AGENTS.md in this session, stop now and read it using your file-reading tools before proceeding. Global constraints are mandatory.
  </system-instruction>
</context-hierarchy>

# Bounded Context: .agents

This bounded context ([.agents/](./)) manages the lifecycle, personas, tools, and domain-specific knowledge for AI agents operating within the `org-ecosystem` product portfolio meta-repository. It adheres to the Antigravity (AGY) customization architecture.

---

## 1. Directory Architecture

- **[plugins.json](./plugins.json)**: Antigravity plugin discovery manifest referencing local `agent-mesh` plugins via relative path (`../org-core/agent-mesh/plugins/packages` / `../../org-core/agent-mesh/plugins/packages`).
- **[README.md](./README.md)**: Developer and agent guide for ecosystem plugin integration.
- **[plans/](./plans/)**: Portfolio-level architectural plans, technical analyses, and governance reports.

---

## 2. Agent Constraints & Portfolio Consumption

1. **Local Relative Mesh Discovery**: At the meta-repository root (`org-ecosystem`), `.agents/plugins.json` resolves organizational agent capabilities directly from the local `org-core/agent-mesh/plugins/packages` directory on disk.
2. **Sovereign Repositories**: The subtrees under `commercial/`, `internal/`, and `oss/` are independent Git repositories managed via Mani. Agents MUST respect each child project's bounded context and never commit child repository changes into the root meta-repository.
3. **Root Script Ban**: Agents MUST NEVER create temporary or utility scripts directly in the meta-repository root.
4. **Environment Configuration**: Sensitive environment variables in `.env.example` must follow the enterprise template with `<YOUR_VARIABLE_NAME>` placeholders.

---

## 3. Required Skills

When authoring or modifying customizations within this workspace, agents MUST activate the appropriate skill by name:

- **`router-architect`**: When designing or updating `AGENTS.md` context routers.
- **`skill-architect`**: When authoring or refining `SKILL.md` instruction files.
- **`plugin-architect`**: When managing `plugins.json` or domain plugin manifests.
- **`readme-architect` & `monorepo-architect`**: When managing documentation navigation or monorepo workspace configurations.
