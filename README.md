# Hermes Guide Builder

A documentation-grounded skill/plugin for creating **A-to-Z Hermes Agent project build guides** as standalone, resumable HTML files.

Instead of guessing what Hermes can do, the workflow verifies the current official Hermes documentation first, interviews the user deeply, builds a dependency-ordered architecture, and only then generates step-by-step prompts for Hermes.

## What it does

1. **Verify Hermes capabilities first**
   - Reads the current official Hermes documentation.
   - Builds a capability ledger with `VERIFIED`, `UNVERIFIED`, and `NOT NEEDED` states.
   - Prevents unsupported Hermes commands, tools, or behaviors from being silently invented.

2. **Run a deep adaptive project interview**
   - Resolves roughly **30–100 meaningful project decisions**, depending on complexity.
   - Reuses facts already supplied by the user instead of forcing duplicate questions.
   - Covers architecture, integrations, data, credentials, autonomy, safety, reliability, deployment, and acceptance testing.

3. **Create a dependency-ordered Hermes build plan**
   - Breaks the project into bounded, independently testable steps.
   - Each step contains one copyable Hermes prompt, expected result, concrete test instructions, and a stop condition.

4. **Generate a standalone HTML guide**
   - No external CSS, JavaScript, fonts, CDN, or build step.
   - One-click **Copy Prompt** controls.
   - Persistent **Run / Tested / Complete** state per step.
   - Persistent notes, progress bar, last-touched step, and **Continue** action.
   - Progress export/import for backup or moving between browsers/devices.

## Progress semantics

Each build step has three states:

- **Run** — the prompt was actually executed in Hermes.
- **Tested** — the result was verified.
- **Complete** — the step was accepted and is ready to move on.

Rules:

- Marking **Complete** automatically marks **Run** and **Tested**.
- Clearing **Run** also clears **Tested** and **Complete**.
- Clearing **Tested** clears **Complete**.
- Copying a prompt does **not** mark the step as Run.

## Repository structure

```text
hermes-guide-builder/
├── README.md
├── plugin.json
├── .codex-plugin/
│   └── plugin.json
└── skills/
    └── hermes-build-guide/
        ├── SKILL.md
        ├── assets/
        │   └── guide-template.html
        └── references/
            └── interview-question-bank.md
```

## Core workflow

```text
Project idea
   ↓
Current Hermes documentation verification
   ↓
Hermes capability ledger
   ↓
30–100 adaptive project decisions
   ↓
Dependency-ordered architecture
   ↓
Bounded Hermes build prompts
   ↓
Standalone resumable HTML guide
   ↓
Run → Tested → Complete
```

## Guide quality gates

Before a generated guide is considered ready, the skill requires four audits:

- **Hermes grounding audit** — every Hermes-specific action maps to a verified capability.
- **Dependency audit** — no step depends on a later step.
- **Prompt audit** — every prompt is bounded, testable, preserves existing work, and has a stop/report condition.
- **HTML audit** — copy controls, persistence, notes, progress, continue, and export/import must work.

## Main files

### `skills/hermes-build-guide/SKILL.md`

The reusable workflow: documentation gate, adaptive interview, architecture rules, prompt contract, HTML requirements, and validation.

### `skills/hermes-build-guide/references/interview-question-bank.md`

A 100-question branching bank covering outcome, triggers, actions, data, integrations, Hermes execution, AI behavior, safety, reliability, UI/observability, deployment, and acceptance.

### `skills/hermes-build-guide/assets/guide-template.html`

The self-contained HTML shell for generated guides, including persistent Run/Tested/Complete state, notes, progress, Continue, and progress import/export.

## Version

Current plugin version: **0.1.0**

This is the first testable version. The intended next phase is to generate real project guides, execute them step-by-step in Hermes, and refine the skill from real failures and friction.

## Hermes references

The skill instructs the agent to verify current official Hermes sources during each guide-generation run, starting with:

- https://hermes-agent.nousresearch.com/docs/llms.txt
- https://hermes-agent.nousresearch.com/docs/llms-full.txt
- https://hermes-agent.nousresearch.com/docs/
- https://github.com/NousResearch/hermes-agent

## Author

**Aijaz Siddique**

## Note

This is an independent project and is not an official Nous Research or Hermes Agent project.
