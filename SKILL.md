---
name: bolt-prompt-builder
description: >
  Guides planning, building, repairing, testing and releasing web or Expo projects with the current Bolt platform. Use when the user mentions Bolt, bolt.new, Bolt Database, Supabase in Bolt, Claude Agent, Plan Mode, Bolt GitHub workflows or Bolt mobile projects. Inspect project age, agent, backend and repository state before generating prompts.
license: MIT
---

# Bolt Prompt Builder

This skill reflects current Bolt workflows: Claude Agent, Plan Mode, Bolt Database or Supabase, GitHub/version history, web and Expo projects, and proportional release safety.

## Origin version check

Canonical source:

```text
https://github.com/AndreAlmeidaDC/bolt-prompt-builder
```

At meaningful use, follow `references/version-check.md`. Never self-update silently.

## Load order

1. Read `references/vibecode-core.md`.
2. Read `references/platform-bolt.md`.
3. Use `references/archetypes.md` only if platform choice is open.
4. Apply the smallest supported project mode.

## Non-negotiable boundaries

- Inspect existing agent, framework, database, Git and deployment state before architecture advice.
- Do not force Supabase or Bolt Database into projects that need no persistence.
- Never promise an unsupported migration between database modes.
- Mobile intent must be declared at project start and verified on devices/builds.
- Separate Plan Mode from implementation.
- Do not publish, connect production data, migrate databases, spend money or perform external writes without explicit approval.

## Output

Return only the needed artifact: project knowledge, planning prompt, backend decision, atomic implementation prompt, diagnostic/reanchoring prompt, verification prompt or release checklist.

## Change history

| Date | Version | Change |
|---|---|---|
| 2026-09-02 | 2026.09.02 | Rebuilt around Claude Agent, Plan Mode, Bolt Database/Supabase decisions, GitHub, version history, Expo, current verification and release gates. |
