---
name: hermes-build-guide
description: Use when a user wants an A-to-Z implementation guide for a project that will be built with Nous Research Hermes Agent, especially when they want a deep requirements interview, Hermes capability verification, copyable step prompts, or a resumable standalone HTML guide with Run/Tested/Complete progress.
---

# Hermes Build Guide

Create **Hermes Agent-only** project build guides. The result is not a generic coding plan and not a guide for Claude Code, Codex, OpenCode, or another agent. It is a documentation-grounded sequence of prompts a user can run in Hermes Agent one step at a time.

## Core principle

**Verify Hermes first. Interview deeply second. Architect third. Generate prompts last.**

Never invent a Hermes capability, command, setting, integration, tool, path, flag, runtime behavior, or deployment method. A plausible-sounding prompt that Hermes cannot actually execute is a failed guide.

## 1. Mandatory Hermes documentation gate

Before asking architecture-specific questions or drafting any Hermes prompt, verify the current official documentation for Hermes Agent during the current run.

Start with these official sources:

1. `https://hermes-agent.nousresearch.com/docs/llms.txt` — current machine-readable documentation index. Read this first.
2. `https://hermes-agent.nousresearch.com/docs/llms-full.txt` — full current documentation when broad coverage is needed.
3. Relevant pages under `https://hermes-agent.nousresearch.com/docs/` identified from the index.
4. `https://github.com/NousResearch/hermes-agent` when the docs are ambiguous or source-level verification is useful.
5. If the user has Hermes installed and command execution is available, prefer `hermes --help`, `hermes <command> --help`, `hermes doctor`, or other documented inspection commands for environment-specific confirmation.

### Documentation rules

- Treat official docs and official repository/source as authoritative.
- Do not use memory as evidence that Hermes supports something.
- Do not treat absence from one page as proof of non-support; search the official index/repository first.
- If a required capability cannot be verified, mark it **UNVERIFIED** and redesign the workflow around verified capabilities or ask the user to change the requirement.
- Never hide an unverified dependency inside a prompt.
- Re-check documentation if the project changes materially during the interview.

Create a **Hermes capability ledger** before final guide generation. Each relevant capability must record:

- capability/feature;
- verified status: `VERIFIED`, `UNVERIFIED`, or `NOT NEEDED`;
- official source URL or CLI/source reference;
- short evidence/constraint;
- how the guide will use it;
- verification date.

No Hermes-specific instruction may appear in the final prompts unless its required Hermes capability is `VERIFIED` in this ledger.

## 2. Deep adaptive project interview: 30–100 decisions

Conduct a structured interview before producing the guide. The interview must resolve **at least 30 and at most 100 meaningful project decisions**, scaled to project complexity.

Use `references/interview-question-bank.md` as the coverage checklist and branching source. Do not mechanically ask every question.

### Complexity bands

- **Focused project:** 30–40 resolved decisions.
- **Medium multi-component project:** 41–60 resolved decisions.
- **Complex autonomous/integrated system:** 61–80 resolved decisions.
- **High-risk or many-integration system:** 81–100 resolved decisions.

A decision already clearly supplied by the user counts as resolved. Do **not** force the user to repeat known information merely to hit a number. When useful, show prefilled decisions and ask the user only to correct them.

Ask questions in coherent batches, normally 5–10 at a time, so the interview is practical. Use branching: skip irrelevant sections and go deeper where architecture depends on the answer.

The interview must resolve, where relevant:

- purpose and definition of success;
- users/operators and permissions;
- input channels and outputs;
- autonomy boundaries and required approvals;
- data sources and systems of record;
- integrations/APIs/MCP servers;
- credentials and secret handling;
- storage/database needs;
- memory/state/session behavior;
- schedules/background execution;
- files and attachments;
- external actions and write permissions;
- failure/retry/idempotency behavior;
- security/privacy constraints;
- UI/dashboard/reporting needs;
- observability/logging;
- deployment/runtime environment;
- expected volume/performance;
- test fixtures and acceptance tests;
- recovery/rollback;
- production handoff and operating procedure.

### Interview completion gate

Do not generate the final guide until:

1. the target complexity band has enough resolved decisions;
2. no architecture-changing unknown remains;
3. all required external services are identified;
4. Hermes capability verification covers every planned Hermes-dependent behavior;
5. success criteria and end-to-end acceptance tests are explicit.

If critical information remains missing, continue the interview instead of guessing.

## 3. Build the project architecture

Translate the resolved interview into a dependency-ordered architecture.

Prefer small independently testable components. A typical sequence may resemble:

`foundation → environment/config → credentials → data/storage → integrations → core logic → Hermes reasoning/orchestration → safety/approval gates → UI/reporting → autonomous execution → error handling → end-to-end testing → production run`

This is only a pattern; derive the real order from dependencies.

For every proposed component, map the required Hermes capabilities back to the capability ledger. Remove or redesign any component that depends on an unverified capability.

## 4. Decompose into Hermes build steps

Create enough steps that each one is bounded, testable, and safe to run independently. Do not optimize for an arbitrary step count.

Every step must have:

- step number and title;
- objective;
- why it occurs at this point;
- prerequisites/dependencies;
- one Hermes prompt;
- expected outcome;
- concrete test/verification instructions;
- stop condition before the next step.

### Prompt contract

Every Hermes prompt must:

1. identify the current project and current step;
2. tell Hermes to inspect existing project files/state before modifying anything;
3. explicitly preserve already-working behavior;
4. implement **only this step** and not race ahead into later steps;
5. use only documentation-verified Hermes behaviors/tools and project dependencies;
6. avoid embedding secrets; use environment/config/secret mechanisms established for the project;
7. include concrete validation/tests for the work performed;
8. handle errors rather than silently declaring success;
9. tell Hermes to stop after this step and report: files/actions changed, tests run, results, and any blocker;
10. require the user to verify the step before continuing when manual validation is necessary.

Do not make copy-paste prompts vague. Name the relevant project files, interfaces, data shapes, commands, integrations, and acceptance criteria when the interview established them.

## 5. Generate a standalone HTML guide

The final deliverable is **one self-contained `.html` file**, not a PDF. Use `assets/guide-template.html` as the base UI and replace its clearly marked sample content with the actual project guide.

Do not require external CSS, fonts, JavaScript, CDNs, or a build step. The guide must remain useful when opened locally/offline after generation.

### Required guide sections

1. Project title and one-paragraph outcome.
2. How to use the guide.
3. Project overview and success criteria.
4. Hermes capability ledger with official references and verification date.
5. Interview-derived requirements summary.
6. Architecture/data-flow summary.
7. Prerequisites and credential checklist.
8. Ordered build sequence.
9. Step cards with Hermes prompts.
10. End-to-end acceptance tests.
11. Production/run procedure.
12. Troubleshooting/recovery guidance.
13. Final completion checklist.

### Required step card UI

Each prompt card must contain:

- number + title;
- objective;
- prerequisites;
- actual Hermes prompt in a readable code/prompt panel;
- **Copy Prompt** button;
- expected result;
- how to test;
- three persistent status controls: **Run**, **Tested**, **Complete**;
- persistent notes field.

Copying a prompt must **not** mark it as Run. The user marks Run only after actually executing it in Hermes.

### Progress state semantics

Persist progress with `localStorage` using a stable project-specific guide ID.

- Checking `Complete` automatically checks `Run` and `Tested`.
- Unchecking `Run` clears `Tested` and `Complete`.
- Unchecking `Tested` clears `Complete`.
- Notes autosave.
- Store a last-touched timestamp/step.
- Show overall completed-step progress.
- Show the last touched step.
- Compute the next recommended incomplete step and provide a **Continue** action that scrolls to it.
- Include **Export Progress** and **Import Progress** so progress can be backed up or moved if browser/file-origin storage is cleared or isolated.

The HTML must visibly explain that browser-local progress is stored on that device/browser and that export is the recovery mechanism.

## 6. Final guide validation

Before delivering the HTML, run a guide audit:

### Hermes-grounding audit
- Every Hermes-specific action maps to a `VERIFIED` ledger item.
- No made-up command, flag, tool, or integration.
- Official URLs/references are present for verification-sensitive capabilities.

### Dependency audit
- No step depends on a later step.
- Every prerequisite is introduced earlier or explicitly external.
- The first step can actually be run from the user's stated starting state.

### Prompt audit
- Each prompt is bounded to one step.
- Each prompt contains a test and stop/report condition.
- Existing work is preserved.
- Secrets are not embedded.

### HTML audit
- File opens without external dependencies.
- Copy Prompt works.
- Run/Tested/Complete state behavior is correct.
- Notes persist.
- Progress/Continue updates correctly.
- Export/import progress works.
- No sample placeholders remain.

Only after these audits should the guide be presented as ready for the user to test in Hermes.

## Quick reference

| Phase | Required output | Hard gate |
|---|---|---|
| Hermes research | capability ledger | no prompt without VERIFIED capability |
| Interview | 30–100 resolved decisions | no architecture-changing unknowns |
| Architecture | dependency-ordered components | no unverified Hermes dependency |
| Prompt design | bounded Hermes prompts | test + stop/report in every step |
| HTML generation | standalone resumable guide | Run/Tested/Complete + notes persist |
| Audit | grounding/dependency/prompt/HTML checks | all pass before delivery |

## Common mistakes

- Designing first and checking Hermes docs later.
- Assuming Hermes is just a coding CLI and ignoring its actual documented execution surfaces.
- Asking 30 generic questions even when half are irrelevant.
- Counting repeated questions as interview depth.
- Generating one giant prompt for the entire project.
- Letting a step implement future steps.
- Treating copied as equivalent to Run.
- Marking Complete without Tested.
- Using localStorage without an export/import fallback.
- Including API keys or passwords in the generated guide.
- Using a polished UI to hide unsupported Hermes assumptions.

## Red flags — stop and verify

Stop guide generation and return to official Hermes documentation if you catch yourself thinking:

- “Hermes probably supports this.”
- “This command looks right.”
- “Most agents can do this, so Hermes can too.”
- “We can fix the unsupported part later.”
- “The user will figure out the missing integration.”

Verification comes before convenience.
