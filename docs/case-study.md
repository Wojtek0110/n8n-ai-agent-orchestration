# Case study: coordinating a staged game-feature implementation

## Context

**Project:** Deckdrive (card-driven roguelite game developed in Godot)

**Automation milestone:** `DD-GAME-13-003` — starter card system

**Historical timeframe:** October 2026 (as documented in the supplied project handoff)

The goal was not to let an AI agent freely decide game mechanics. The human first defined the gameplay and approved the target behavior. The automation then coordinated a technical implementation process under explicit guardrails.

## Challenge

A multi-stage coding objective involves repeated code edits, dependencies between stages, regression testing, and occasional interruptions. A simple “call an AI model” workflow is not enough because it cannot reliably answer: Which iteration is authorized? Did tests pass? Is the worktree the expected one? Can the task resume safely? Should automation pause for human input?

## Solution

Three n8n workflows were built around a separate Worker service:

- **Orchestrator + quota guard:** the main workflow reads Worker state, selects the next approved stage/iteration, guards agent invocations, validates HTTP results, and reports terminal statuses.
- **Live monitor:** polls Worker progress every 15 seconds, computes readable iteration/stage labels, and stops on terminal conditions.
- **SMTP error alert:** reports n8n technical failures, with sensitive execution details omitted from emails.

The task's **10 stages** covered: card data/identity, per-player deck lifecycle, effect execution and costs, drive/navigation, intent change, lane switching, honking, combining five starting-card types, gameplay/HUD API boundary, and an end-to-end single-player loop.

## Important controls

- Human-approved TASK and STAGE requirements are authoritative; the agent cannot invent gameplay decisions.
- Worker verifies the Git baseline, branch, approved paths, and the four-file-per-iteration limit.
- Focused tests run within iterations; full-suite tests run at stage checkpoints.
- An unknown quota reading is a **stop**, not permission to proceed.
- Interrupted or inconsistent Task State is a **recovery condition**, not an automatic retry.
- Final review, `COMPLETE`, commits, and merges remain human-controlled.

## Outcome and evidence

The supplied Deckdrive development-status document (dated **24 October 2026**) records `DD-GAME-13-003` as `COMPLETE` after human review, all `CARD13.1`–`CARD13.10` stages passed, and subsequent card gameplay/HUD integration into the `dev` branch via [PR #31](https://github.com/Wojtek0110/deckdrive/pull/31). It reports manual 1P/2P checks and a full test-suite pass after integration.

**Evidence boundary:** These outcomes are based on the project handoff documentation. This portfolio repository contains sanitized workflow exports and documentation, **not** the Worker's runtime logs, independently measured run durations, or new test results. No throughput, success-rate, time-saved, or cost-savings metric is claimed.

## Lessons / tradeoffs

- **Safety vs. speed:** strict checkpoints slow down fully autonomous execution, but make decisions auditable and easier to recover.
- **Orchestration vs. authority:** n8n coordinates actions; it does not become the owner of mutable Worker or gameplay state.
- **Fail-closed dependencies:** a quota probe is useful, but its failure must not silently start the agent.
- **Operational transparency:** a monitor and status emails are helpful, but Worker Task State remains the source of truth.

## What I would add next

A mock Worker implementation, synthetic fixtures covering state transitions, contract tests for n8n branches, and a metrics dashboard for duration and stop reasons would make this case study fully reproducible without sharing the private production environment.
