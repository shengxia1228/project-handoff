# Project Handoff

A portable Agent Skill for preserving project state across AI sessions.

## What is Project Handoff?

When working with AI agents on a long-running project, a single conversation can eventually become too long.

The AI may start forgetting earlier decisions, repeating work, confusing planned work with completed work, or losing important context.

Project Handoff solves this by creating a:

`PROJECT_HANDOFF.md`

inside your project.

This file records the current project state so a fresh AI session can quickly understand where the previous session stopped and continue working.

## What does it save?

Project Handoff can record:

- Project goal
- Current project state
- Current stopping point
- Completed work
- Work in progress
- Planned and unverified work
- Important files
- Technical decisions
- Failed approaches
- Known bugs and blockers
- Verification and test status
- Recommended next steps

The goal is not to summarize the conversation.

The goal is to preserve the **actual project state**.

## Why not just use AI Memory?

AI Memory and Project Handoff solve different problems.

**Memory** helps an AI remember previous conversations and user preferences.

**Project Handoff** creates an explicit project-level handoff file that another AI agent can read.

This makes the project state portable between different conversations and compatible AI agents.

## How it works

```text
Long AI session
      ↓
Project Handoff
      ↓
PROJECT_HANDOFF.md
      ↓
Fresh AI session
      ↓
Verify project state
      ↓
Continue working
