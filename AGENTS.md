# tupynambalucas-dev Product Ecosystem Sub-Meta-Repository Agent Context

This document serves as the context router (Layer 2 when nested inside `tupynambalucas-dev/org`, or Layer 1 in standalone checkouts) for AI agents operating in the `tupynambalucas-dev/ecosystem` product portfolio meta-repository (`projects/org/ecosystem/`).

## Workspace Navigation

- [Parent Master Orchestrator (`../AGENTS.md`)](../AGENTS.md): Root `tupynambalucas-dev/org` agent context router when mounted inside `projects/org/`.
- [README.md](./README.md): Primary developer documentation and Mani portfolio orchestration runbook.
- [mani.yaml](./mani.yaml): Declarative multi-repository sub-manifest managing product repositories, remotes, and batch tasks.
- [tupynambalucas-dev-ecosystem.code-workspace](./tupynambalucas-dev-ecosystem.code-workspace): Canonical multi-root IDE workspace binding portfolio solutions.
- [LICENSE](./LICENSE): Apache License 2.0 governing meta-repository orchestration assets.
- [commercial/omnichannel](./commercial/omnichannel/README.md): Commercial omnichannel messaging engine and client platform (Turborepo Monorepo).
- [commercial/elo-organico](./commercial/elo-organico/README.md): Commercial organic product sharing and community management platform (Turborepo Monorepo).
- [internal/tessel](./internal/tessel/README.md): Proprietary enterprise core platform and internal software asset (Turborepo Monorepo).
- [oss/](./oss/): Directory for open-source community repositories and SDKs.
- [clients/](./clients/): Directory for corporate B2B client project deliveries under `tupynambalucas-dev`.

## Governance Standards

- **Branching Model**: Single-Branch GitHub Flow on `main`. Short-lived branches MUST use Conventional Commit prefixes (`feat/`, `fix/`, `docs/`, `chore/`, `refactor/`, `ci/`, `perf/`, `test/`, `build/`, `style/`, `revert/`, `hotfix/`).
- **Cryptographic Signature**: All Git commits and annotated tags MUST be signed with SSH (`git commit -S -m "..."`).
- **Conventional Commits**: All commit messages must follow `<type>[optional (<scope>)][!]: <description>` (`<= 72` chars target, `<= 100` chars maximum).
- **Zero-Emoji Policy**: Emojis are strictly forbidden across all code, PRs, comments, and agent interactions.
- **Secret Hygiene**: Never commit plaintext tokens. Sourced via Infisical (`infisical run -- ...`) or local/parent `.env` files.
- **License**: `Apache-2.0` (`Copyright (c) 2026 tupynambalucas.dev`) across public portfolio assets.
- **Workspace Orchestration**: Repositories are managed as sovereign Git repositories coordinated via `mani`. Git submodules and `160000` commit gitlinks are deprecated and removed.

## Multi-Repository Operations with Mani

Cross-repository commands and queries are executed using `mani` (either from the root `org/` workspace or directly inside `ecosystem/`):

```bash
# Check status across all portfolio projects
mani run status

# Comprehensive portfolio audit table
mani run overview

# Fetch remote changes for all projects
mani run fetch

# Pull latest main across all projects
mani run pull

# Display current branches
mani run branch

# Selective synchronization by category tags
mani sync --tags commercial
mani sync --tags internal
mani sync --tags oss
mani sync --tags clients
```

## AI Agent Plugin Consumption

`ecosystem` and its portfolio applications consume domain plugins and sovereign MCP servers from `agent-mesh` without NTFS directory junctions:
- **Nested Meta-Repository Mode (`org/ecosystem`)**: Root [`.agents/plugins.json`](./.agents/plugins.json) resolves local plugins directly via `../agent-mesh/plugins/packages` with fallback to `node_modules/@tupynambalucas-dev/agent-mesh/plugins/packages`.
- **Child Product Monorepo Mode (`omnichannel`, `elo-organico`, `tessel`)**: Resolved via `../../../agent-mesh/plugins/packages` inside `org/ecosystem/<category>/<repo>` with fallback to `node_modules/@tupynambalucas-dev/agent-mesh/plugins/packages` (`catalogs.plugins-stack`: `github:tupynambalucas-dev/agent-mesh`).
- **Sovereign Execution**: MCP servers run via self-contained launchers (`scripts/launcher.cjs`) and committed bundles (`dist/bin.cjs`).

## Architectural Plans & Artifact Dual-Storage Standard

Architectural blueprints, technical plans, and master plans follow strict enterprise storage standards:
- **Storage Location**: Blueprints, analyses, and reports reside in `<target-repo>/.agents/plans/<artifact-slug>/` (or `<target-repo>/.agents/plans/<artifact-slug>.md`) within the respective repository for which the artifact is created. Creating a `plans/` directory at the root of any repository is strictly prohibited.
- **Topologies**: Topology 1 (Single-File Plan) for atomic refactors/features; Topology 2 (Multi-Artifact Plan Suite) for multi-domain frameworks with master `README.md` and numbered domain documents.
- **Dual-Storage Invariant**: Whenever an agent creates a plan artifact in the Antigravity conversation directory (`<appDataDir>/brain/<conversation-id>/`), an identical synchronized copy MUST ALWAYS be mirrored in `<target-repo>/.agents/plans/<artifact-slug>/` (or `<target-repo>/.agents/plans/<artifact-slug>.md`).
- **Ignore & Index Triad**: All repositories ignore `.agents/plans/` in `.gitignore`, while explicitly un-ignoring it in `.ignore` and `.rgignore` (`!.agents/plans/`, `!.agents/plans/**`) and setting `"search.useIgnoreFiles": false` in `.vscode/settings.json` so files can always be attached with `@`.

## Required Skills

Agents operating at the `ecosystem` meta-repository layer MUST autonomously engage the domain skills:

- **Atelier Plugin (`@tupynambalucas-dev/plugin-atelier`)**: `router-architect`, `skill-architect`, `rule-architect`, `hook-architect`, `plugin-architect`, `plan-architect`.
- **GitHub Domain Plugins (`@tupynambalucas-dev/plugin-github-*`)**: `github-repo-architect`, `readme-architect`, `readme-auditor`, `monorepo-architect`, `community-health-architect`, `license-architect`, `github-standards-architect`, `mani-operator`, `github-flow-operator`, `github-actions-operator`, `github-releases-operator`.
- **Secrets Plugin (`@tupynambalucas-dev/plugin-secrets`)**: `infisical-vault-operator`, `secret-rotation-operator`.
