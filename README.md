# Product Portfolio & Ecosystem Meta-Repository (`tupynambalucas-dev/ecosystem`)

Central orchestrator and unified multi-repository workspace for customer-facing SaaS products (`commercial/`), proprietary internal assets (`internal/`), open-source community solutions (`oss/`), and B2B client deliveries (`clients/`) across the `tupynambalucas-dev` organization. Nested directly inside the master [`tupynambalucas-dev/org`](https://github.com/tupynambalucas-dev/org) meta-repository at `projects/org/ecosystem/` (or cloned standalone), it coordinates autonomous product monorepos via [Mani](https://manicli.com) and multi-root IDE workspaces while preserving independent Git histories, branches, release lifecycles, and CI/CD pipelines.

---

## 1. Architecture Overview

The organization operates under a hierarchical meta-repository topology where foundational enterprise governance (`org`) hosts the commercial and proprietary product portfolio (`org/ecosystem/`):

```mermaid
flowchart TD
    subgraph EnterpriseTier["Layer 0: Master Enterprise Foundation (tupynambalucas-dev/org)"]
        Org["org (Master Organization Host)"]
        DotGithub[".github & .github-private (Org Governance)"]
        AgentMesh["agent-mesh (Universal Agent Mesh)"]
        Platform["platform (Core Monorepo)"]
        Docs["docs (Documentation Hub)"]
        Foundation["foundation (WSL2 DaC, Identities & CLI Suite)"]
        Org --> DotGithub
        Org --> AgentMesh
        Org --> Platform
        Org --> Docs
        Org --> Foundation
    end

    subgraph PortfolioTier["Layer 1: Product Portfolio (tupynambalucas-dev/ecosystem -> org/ecosystem/)"]
        Eco["ecosystem (Ecosystem Orchestrator)"]
        Commercial["commercial/ (SaaS / Paid Services)"]
        Internal["internal/ (Proprietary Company Assets)"]
        OSS["oss/ (Open Source Community Tools)"]
        Clients["clients/ (Corporate B2B Deliveries)"]

        Omnichannel["omnichannel (Turborepo Monorepo)"]
        EloOrganico["elo-organico (Turborepo Monorepo)"]
        Tessel["tessel (Turborepo Monorepo)"]

        Eco --> Commercial
        Eco --> Internal
        Eco --> OSS
        Eco --> Clients

        Commercial --> Omnichannel
        Commercial --> EloOrganico
        Internal --> Tessel
    end

    Org -->|"Hosts at org/ecosystem/"| Eco
    AgentMesh -.->|"Relative Plugin Resolution (../agent-mesh/plugins/packages)"| Eco
```

---

## 2. Managed Repositories & Navigation

| Repository | Path / Namespace | Branch | Documentation | Agent Context | Purpose |
| :--- | :--- | :--- | :--- | :--- | :--- |
| [`omnichannel`](./commercial/omnichannel/README.md) | `commercial/omnichannel` | `main` | [`README.md`](./commercial/omnichannel/README.md) | [`AGENTS.md`](./commercial/omnichannel/AGENTS.md) | Commercial multi-tenant omnichannel messaging gateway and FSM workflow engine for WhatsApp and Instagram. |
| [`elo-organico`](./commercial/elo-organico/README.md) | `commercial/elo-organico` | `main` | [`README.md`](./commercial/elo-organico/README.md) | [`AGENTS.md`](./commercial/elo-organico/AGENTS.md) | Commercial organic product sharing and community management platform (Turborepo Monorepo). |
| [`tessel`](./internal/tessel/README.md) | `internal/tessel` | `main` | [`README.md`](./internal/tessel/README.md) | [`AGENTS.md`](./internal/tessel/AGENTS.md) | Proprietary hybrid spatial social ecosystem, WebGPU/Three.js 3D simulation engine, and distributed API core. |
| `oss/*` | `oss/` | `main` | *(per project)* | *(per project)* | Open-source developer tools, public SDKs, and community extensions. |
| `clients/*` | `clients/` | `main` | *(per project)* | *(per project)* | Corporate B2B client solutions delivered under `tupynambalucas-dev`. |

### Multi-Root IDE Workspace

Open [`tupynambalucas-dev-ecosystem.code-workspace`](./tupynambalucas-dev-ecosystem.code-workspace) in VS Code or Antigravity IDE for a portfolio-focused workspace (`ecosystem`, `omnichannel`, `elo-organico`, `tessel`), or open [`../tupynambalucas-dev.code-workspace`](../tupynambalucas-dev.code-workspace) from the parent `org/` directory to mount the entire organization.

---

## 3. Environment, Secret & Plugin Governance

1. **Secret Resolution via Infisical & `.env` Templates**:
   Each managed product monorepo defines its own project-scoped Infisical environment and `.env.example` template. Secrets are injected at runtime via `infisical run --projectId <PROJECT_ID> --env dev -- <command>` or local/ancestor `.env` files excluded from Git.
2. **AI Agent Mesh Consumption (`agent-mesh`)**:
   At the `ecosystem` meta-repository level, [`.agents/plugins.json`](./.agents/plugins.json) imports the 11 domain plugins and 9 sovereign MCP servers directly via relative path `../agent-mesh/plugins/packages` (when nested inside `org/`) with fallback to `node_modules/@tupynambalucas-dev/agent-mesh/plugins/packages`. Child product monorepos (`commercial/*`, `internal/*`) resolve plugins via `../../../agent-mesh/plugins/packages` or `node_modules/@tupynambalucas-dev/agent-mesh/plugins/packages` (`catalogs.plugins-stack`: `'github:tupynambalucas-dev/agent-mesh'`).
3. **Mani Ignore & Search Indexing Invariant**:
   [`mani.yaml`](./mani.yaml) enforces `sync_gitignore: false` and `ignore_non_existing: true`. Managed repository directories (`commercial/`, `internal/`, `oss/`, `clients/`) are ignored in [`.gitignore`](./.gitignore) while explicitly un-ignored in [`.ignore`](./.ignore) and [`.rgignore`](./.rgignore) so `@` file mentions and workspace search index all portfolio code seamlessly.

---

## 4. Getting Started

### Prerequisites

- **Git**: `>= 2.40` (configured with Ed25519 SSH commit signing)
- **Mani CLI**: `>= 0.30`
- **Node.js**: `>= 22.x` & **pnpm**: `>= 10.x`

Install `mani` on Windows via Scoop (or use the pre-configured `tupynambalucas-dev` WSL2 distribution):

```powershell
scoop bucket add poldi https://github.com/aliesbelik/poldi
scoop install mani
```

### Workspace Initialization

Synchronize `ecosystem` directly from the parent `tupynambalucas-dev/org` orchestrator (recommended) or clone standalone:

```bash
# Option A: From parent tupynambalucas-dev/org root
mani sync --tags ecosystem

# Option B: Standalone or scoped inside org/ecosystem
git clone git@github.com:tupynambalucas-dev/ecosystem.git
cd ecosystem
mani sync

# Or synchronize selectively by portfolio tier tag
mani sync --tags commercial
mani sync --tags internal
mani sync --tags oss
mani sync --tags clients
```

---

## 5. Multi-Repository Operations

| Command | Target Scope | Description |
| :--- | :--- | :--- |
| `mani sync` | All repositories | Clones and synchronizes all portfolio repositories declared in [`mani.yaml`](./mani.yaml). |
| `mani sync --tags <tag>` | Tagged subset | Synchronizes only repositories matching `commercial`, `internal`, `oss`, or `clients`. |
| `mani run status` | All synced repos | Executes `git status -s` in parallel across all portfolio repositories. |
| `mani run dirty` | Dirty repos only | Displays a formatted table of only repositories containing uncommitted changes. |
| `mani run overview` | All synced repos | Displays a consolidated audit table with active branch, dirty status, and latest commit. |
| `mani run fetch` | All synced repos | Fetches remote updates and prunes stale references across all projects. |
| `mani run pull` | All synced repos | Pulls latest `main` branch updates across all portfolio projects. |
| `mani run branch` | All synced repos | Displays the active Git branch for each portfolio repository in a table. |

```bash
# Execute daily multi-repository status and synchronization checks
mani run status
mani run overview
mani run fetch
mani run pull
```

---

## 6. Governance & Contributing Standards

All development across `ecosystem` and its portfolio repositories must comply with organizational governance:

1. **Cryptographic Commit Signing**: All Git commits and annotated tags MUST be signed using SSH (`git commit -S -m "..."`). Unsigned commits are rejected by repository rulesets.
2. **Conventional Commits**: Commit messages must follow the Conventional Commits v1.0.0 specification (`<type>(<scope>): <description>`).
3. **Single-Branch GitHub Flow**: Each product repository operates independently on `main`. Developers create feature branches (`feat/<slug>`, `fix/<slug>`, `docs/<slug>`, `chore/<slug>`), push them, and open Pull Requests against `main`.
4. **Zero-Emoji Invariant**: Emojis are strictly prohibited in commit messages, documentation, code comments, and agent interactions.
5. **Secret Hygiene**: Never commit `.env` files or plaintext credentials.
6. **AI Agent Context**: Autonomous agents operating in this workspace MUST read [AGENTS.md](./AGENTS.md) prior to executing tasks.

---

## 7. License

Licensed under the [Apache License 2.0](./LICENSE). Copyright (c) 2026 tupynambalucas.dev.
