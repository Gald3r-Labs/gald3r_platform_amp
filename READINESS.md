# gald3r Readiness Report — Amp (Amp Code)

> An honest accounting of how much of the gald3r framework installs natively on this
> platform, what degrades to an approximation, and what has no native home yet.
> Generated from a live documentation crawl on 2026-06-02.

**Overall readiness: ✅ Full.** Amp (Sourcegraph) is highly extensible. gald3r's commands,
rules, skills, hooks, and MCP all land on native mechanisms; only declarative sub-agents fall
short, since Amp auto-spawns subagents and custom agents require an experimental plugin API.

## C.R.A.S.H. capability grid

| | Capability | Native? | What gald3r gets here | The gap |
|---|---|:---:|---|---|
| **C** | Commands | ✅ | `.agents/commands/<name>.md` → native `/slash` commands (shebang scripts work too); plugins add palette commands via `amp.registerCommand()` | None functionally — but Amp is folding file commands into Skills (deprecation announced 2026-01-29), so `@g-*` may need to ship as Skills |
| **R** | Rules | ✅ | `AGENTS.md` (also `AGENT.md` / legacy `CLAUDE.md`), hierarchical lookup with YAML `globs` for file-scoped guidance | None — gald3r rules load here as first-class, always-on convention files |
| **A** | Agents | ⚠️ | Auto-spawned subagents + built-in `deep`/`smart`/`rush` modes; plugins can mint custom agents/modes via `amp.experimental.createAgent()` | No declarative subagent file — gald3r's `g-agnt-*` roles can't install standalone; custom agents require writing a plugin |
| **S** | Skills | ✅ | Native Agent Skills — `SKILL.md` dirs in `.agents/skills/` (also reads `.claude/skills/`); may bundle `mcp.json` + `scripts/` | None — gald3r's `g-skl-*` install natively; this is now Amp's recommended extensibility path |
| **H** | Hooks | ✅ | Two surfaces: settings `amp.hooks` array (event+action, e.g. `tool:pre-execute`) and Plugin API `amp.on(session.start\|agent.start\|tool.call\|tool.result\|agent.end)` | None functionally — but the contract is split across two places and the settings-array form is still Preview, so `g-hk-*` session-start / pre-commit wiring is less uniform |

_Legend: ✅ native · ⚠️ partial / approximated · ❌ no native mechanism · ❓ unverified_

**Beyond C.R.A.S.H. — MCP: ✅** Native MCP servers via the `amp.mcpServers` config object and
`amp mcp add` CLI — local (`command`/`args`/`env`) and remote (`url`/`headers`), with OAuth
(`amp mcp oauth login`) and per-skill bundling through `mcp.json`. gald3r's MCP backend connects directly.

## Adoptable extras (non-C.R.A.S.H.)

Platform-native strengths gald3r can lean on, and which need wiring:

| Feature | Status | gald3r fit |
|---|:---:|---|
| Plugin API (`registerTool` / `registerCommand` / `on` / experimental `createAgent`) | ✅ present | The primary, growing extensibility surface — hosts custom tools, hooks, and agent/mode shims |
| Code-review Checks (`.agents/checks/*.md` with YAML frontmatter, codebase-scoped) | ⚙️ needs customization | Could codify gald3r review constraints / security invariants as native checks |
| Streaming output (`--stream-json` / `-thinking` / `-input`), headless CLI | ✅ present | A real automation/CI entry point for gald3r tooling and agent-to-agent piping |
| Sourcegraph code-intelligence (cross-repo search, dependency-chain analysis) | ✅ present | Augments gald3r skills/agents — trace API consumers across an org's repos |
| Curated community extensions (`ampcode/amp-contrib`, `sourcegraph/amp-examples-and-guides`) | ➖ n.a. | Reference patterns for skills/tools/MCPs; no gald3r work required |

## The ceiling, and what's beyond it

gald3r runs at full strength on this platform — commands, rules, agents, skills, and hooks all map onto native mechanisms, so the framework installs without compromise. As third-party adaptation goes, this is the high end: nothing here has to be approximated.

But adaptation, however clean, is still gald3r living as a guest inside someone else's tool. The native build goes further — **gald3r_agent**, running on the **gald3r throne** over the **gald3r_world_tree** — where these primitives aren't mapped onto a host, they *are* the substrate. Same framework, no host in between.

> ### gald3r_agent — coming soon. 🌳

---

<sub>Capabilities verified against the platform's official documentation on 2026-06-02, and
re-verified each release via the gald3r platform-docs crawl. This report describes gald3r's
third-party adaptation surface; it is not an endorsement or critique of the platform itself.</sub>
