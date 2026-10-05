# Octop Team Guide Builder

A prompt-generation Skill for designing and building verified multi-agent systems in TencentCloud Octop.

## What it does

1. Re-checks the current Octop repository/docs and records a capability ledger.
2. Runs an adaptive requirements interview.
3. Chooses the correct Octop topology (native Expert Team, regular orchestrator + peers, single expert, or justified hybrid).
4. Produces a dependency-ordered standalone HTML guide.
5. Every guide step contains one copyable prompt for the Octop main/builder agent, an expected result, a test, notes, and Run/Tested/Complete state.

## What it deliberately does not do

The Skill itself does not provision or modify the target Octop agents/team. The generated prompts are executed by a separate Octop main/builder agent.

## Install into an Octop agent

Use Octop's built-in Skill Manager to inspect the ZIP first, then install it. The package has a root `SKILL.md`, matching Octop's Skill package expectations.

After installation, start a new conversation so the Skill is fully available.