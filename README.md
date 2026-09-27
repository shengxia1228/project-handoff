# Project Handoff

A portable Agent Skill for preserving and transferring project state across AI sessions.

## What is Project Handoff?

When you use an AI agent to work on a long-running project, a single conversation can eventually become too large.

As context grows, the agent may begin to:

- forget previously settled decisions
- repeat work that has already been completed
- confuse planned work with completed work
- lose important project details
- fail to continue accurately after moving to a fresh conversation

Project Handoff is designed to solve this problem.

When invoked, the Skill creates or updates:

`PROJECT_HANDOFF.md`

inside the current project.

This file records the **current project state**, rather than merely summarizing the previous conversation.

A fresh AI session can read the handoff, verify the actual project state, and continue from where the previous session stopped.

## What does it preserve?

Project Handoff can record information such as:

- project goal
- current project state
- current stopping point
- completed work
- work in progress
- planned work
- unverified work
- important files and directories
- settled technical decisions
- abandoned approaches
- known bugs and blockers
- testing and verification status
- recommended next steps

The goal is not to preserve chat history.

The goal is to preserve the **actual working state of the project**.

## Why not just use AI Memory?

AI Memory and Project Handoff solve different problems.

**Memory** is mainly useful for remembering things such as:

- previous conversations
- user preferences
- historical context
- long-term information

**Project Handoff** creates an explicit project-level handoff file.

Because the handoff lives inside the project itself, it can move together with the project.

As long as another AI agent can read the project files, it can also read `PROJECT_HANDOFF.md`.

This makes it useful when:

- switching to a fresh conversation
- switching models
- switching AI agents
- switching clients
- continuing long-running work across multiple days

## Workflow

```text
Long-running AI project
        ↓
Invoke Project Handoff
        ↓
Create / update PROJECT_HANDOFF.md
        ↓
Open a fresh AI session
        ↓
Read and verify the project state
        ↓
Continue from the previous stopping point
```

## When should I use it?

Use Project Handoff when:

- the current AI conversation has become too long
- you want to start a fresh conversation
- you are stopping work for the day
- you want to switch to another AI agent
- you are worried that important project context may be lost
- you want to create a reliable project checkpoint

When `project-handoff` is invoked, it creates or updates:

```text
PROJECT_HANDOFF.md
```

In the new AI session, you can tell the agent:

> Read `PROJECT_HANDOFF.md`, verify the current project state, and continue from the documented stopping point.

## One project, one handoff

Each project maintains its own independent:

`PROJECT_HANDOFF.md`

For example:

```text
Projects/
├── Project-A/
│   └── PROJECT_HANDOFF.md
│
└── Project-B/
    └── PROJECT_HANDOFF.md
```

Invoking Project Handoff again inside **Project-A**:

> updates Project-A's existing `PROJECT_HANDOFF.md`

Invoking it inside **Project-B**:

> creates or updates Project-B's own `PROJECT_HANDOFF.md`

Handoffs from unrelated projects should never be reused or overwritten.

## Facts and plans are kept separate

Project Handoff attempts to distinguish between states such as:

- completed
- in progress
- not started
- blocked
- planned
- unverified
- abandoned

For example, if a previous conversation only said:

> We plan to implement authentication.

the handoff should not claim:

> Authentication has been implemented.

If something cannot be confirmed, it should be marked as:

`Unverified`

or:

`Unknown`

Actual project files, repository state, Git status, tests, and runtime results should take priority over model memory.

## Skill structure

```text
project-handoff/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    └── handoff-format.md
```

### `SKILL.md`

Contains the core Project Handoff instructions and behavior.

### `references/handoff-format.md`

Defines the structure and expected contents of `PROJECT_HANDOFF.md`.

### `agents/openai.yaml`

Contains OpenAI-specific Skill metadata.

## Compatibility

The core logic lives in `SKILL.md`, which makes the Skill relatively portable across compatible Agent Skill environments.

Platform-specific differences may exist in:

- installation
- Skill discovery
- invocation
- available tools
- filesystem access

## Project status

This is a personal project maintained on a best-effort basis.

Compatibility with every AI agent, model, client, or Skill implementation is not guaranteed.

Issues and compatibility requests may not always receive support.

## License

MIT License
