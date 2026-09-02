# bolt-prompt-builder

Workflow skill for the current Bolt platform.

The legacy edition reduced Bolt to WebContainers plus a fixed React/Supabase brief. The current version inspects the project first, distinguishes Bolt Database from Supabase, uses Plan Mode before implementation, covers GitHub and Version History, and supports web or Expo projects without forcing a backend.

## Core sequence

```text
inspect agent/backend/project -> plan -> atomic build -> verify -> review -> approved publish
```

## Verification

```bash
python3 scripts/validate_skill.py
```

Version `2026.09.02` is a breaking replacement of the June 2026 workflow.
