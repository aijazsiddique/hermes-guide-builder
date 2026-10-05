# Octop Capability Baseline

Audited against `TencentCloud/Octop` current `main` during skill authoring on 2026-10-06. Source URLs observed at commit `eb28011249c02cafd389b2d424294c6c1b9cf422` (release line `1.0.2b6`). Re-verify before every generated guide.

This file is a baseline, not permanent truth.

| Capability | Baseline status | Evidence | Design consequence |
|---|---|---|---|
| Persistent expert agents | VERIFIED | `src/octop/api/routers/agents.py`, `src/octop/cli/commands/agent.py` | Create/reuse specialist experts as independent persistent workers. |
| Agent personas / MBTI | VERIFIED | `docs/personas.md`, agent API/CLI | Use for interaction style, not as sole storage for hard operating policy. |
| Native Expert Teams | VERIFIED / Beta | `docs/expert-teams.md`, `src/octop/api/routers/teams.py` | One host agent coordinates a roster of experts. |
| Native team minimum 2 members | VERIFIED | `TEAM_MIN_MEMBERS = 2` in `src/octop/infra/agents/teams/service.py` | Never create a filler member; choose another topology if only one real specialist is needed. |
| Team nesting | UNSUPPORTED | team member validation rejects `kind=team` | A team cannot be a member of another native team. |
| Team host is coordinator-only | VERIFIED | team `AGENTS.md`, `SOUL.md`, host tool allowlist | Do not make native host browse/code/edit/use MCP/Skills. |
| Team host tool allowlist | VERIFIED | `HOST_TOOLS_ALLOWED` in team service | Baseline: `agent_list`, `ask_agent`, `memory_search`, `memory_get`, `current_time`. Recheck current code. |
| Team members have separate workspaces | VERIFIED | `docs/expert-teams.md`, team templates | Assignment messages must carry needed context; no implicit shared workspace. |
| Team host async dispatch | VERIFIED | `docs/expert-teams.md`, team manager | Good for parallel work; host closes out after member callbacks. |
| Member-to-member peer calls | VERIFIED | `docs/agent-call-agent.md`, `docs/agent-delegation.md` | Use for targeted collaboration; verify sync/background behavior in current release. |
| Stopped member auto-start | UNSUPPORTED baseline | `docs/expert-teams.md`, team template | Preflight/start members before team acceptance tests. |
| In-flight job persistence across process restart | UNSUPPORTED baseline | `docs/expert-teams.md`, delegation docs | Critical workflows need restart/recovery expectations. |
| Team creation HTTP API | VERIFIED | `POST /api/teams` in `src/octop/api/routers/teams.py` | Public control-plane route exists for authenticated callers. |
| Team create/edit fields | VERIFIED | `TeamCreateBody`, `TeamPatchBody` | Name, description, default model, UI metadata, welcome, member IDs; current source does not expose regular host Skills/MCP/persona fields. |
| Dedicated `octop team create` CLI | NOT FOUND in audited source | CLI command search + `src/octop/cli/commands/` | Never invent it. Use current supported API/Dashboard/control-plane route, or stop for manual control-plane action. |
| Agent create CLI | VERIFIED | `octop agent create`, `octop agent from-expert` | Good supported route for specialist creation when current version matches. |
| Agent lifecycle CLI | VERIFIED | `agent start/stop/reload/delete/list/use` | Validate member state before team use. |
| Agent PATCH API | VERIFIED | `src/octop/api/routers/agents.py` | Supports persona, model, system prompt, config, Skill packages, knowledge-base IDs, MCP server IDs, etc. |
| Per-agent built-in tool policy | VERIFIED | `src/octop/infra/agents/settings/tool_catalog.py` | Apply least privilege to member experts. Critical tools may be non-disableable. |
| Agent Skills | VERIFIED | Skills CLI and Skill Manager | Put reusable hard workflow instructions into Skills when appropriate. |
| Skill package root `SKILL.md` | VERIFIED | Skill Manager / skill package code | This guide-builder ZIP is intentionally structured with root `SKILL.md`. |
| Skill Manager | VERIFIED | `src/octop/infra/agents/builtin_skills/skill-manager/SKILL.md` | Can inspect/install/import/update current agent Skills from Git/ZIP/etc; respect current-agent boundary. |
| MCP / Connectors on experts | VERIFIED | agent API + connectors source/docs | Assign to workers that need them; native team host baseline strips MCP. |
| Knowledge bases on experts | VERIFIED | agent API and dashboard/runtime | Attach domain knowledge to the worker that needs it. |
| ACP outbound coding delegation | VERIFIED | `docs/acp.md`, `acp_runner` tool catalog | Useful for code-heavy member roles if enabled and runner exists. |
| Cron | VERIFIED | cron CLI/API/tools | Schedule the agent whose tools/policy match the recurring task; verify current team-host behavior before attaching jobs to a host. |
| Channels | VERIFIED | user guide/API/CLI | For native team UX, team host is the natural group entry; verify exact channel support/version. |
| Octop↔Octop Bridge | VERIFIED in audited release | current source/release history | Consider only when remote-instance experts are a real requirement. |

## Known version-drift conflict discovered during audit

The repository contains stale guidance around CLI login:

- Current `AGENTS.md` in the audited tree says: **no `octop user login`**; CLI trusts local filesystem access, with acting user pinned via `octop config set-user` or root `--user`.
- Current `src/octop/cli/commands/user.py` contains user administration commands but no `login` subcommand.
- Current `src/octop/cli/support/state.py` `CLIState` stores only `default_user` and `default_agent`.
- Some docs and the bundled `octop-assistant` Skill still mention `octop user login` and a CLI token.

Therefore generated guides MUST NOT blindly repeat old login instructions. Re-read the current command source and `octop --help` on the target instance. Runtime/source wins when documentation conflicts.

## High-value source paths

- https://github.com/TencentCloud/Octop/blob/main/docs/expert-teams.md
- https://github.com/TencentCloud/Octop/blob/main/docs/agent-call-agent.md
- https://github.com/TencentCloud/Octop/blob/main/docs/agent-delegation.md
- https://github.com/TencentCloud/Octop/blob/main/docs/personas.md
- https://github.com/TencentCloud/Octop/blob/main/src/octop/api/routers/teams.py
- https://github.com/TencentCloud/Octop/blob/main/src/octop/infra/agents/teams/service.py
- https://github.com/TencentCloud/Octop/blob/main/src/octop/infra/agents/teams/template/AGENTS.md
- https://github.com/TencentCloud/Octop/blob/main/src/octop/infra/agents/teams/template/SOUL.md
- https://github.com/TencentCloud/Octop/blob/main/src/octop/api/routers/agents.py
- https://github.com/TencentCloud/Octop/blob/main/src/octop/cli/commands/agent.py
- https://github.com/TencentCloud/Octop/blob/main/src/octop/infra/agents/settings/tool_catalog.py
- https://github.com/TencentCloud/Octop/blob/main/src/octop/infra/agents/builtin_skills/skill-manager/SKILL.md
- https://github.com/TencentCloud/Octop/blob/main/AGENTS.md