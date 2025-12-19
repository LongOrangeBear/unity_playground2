# Claude Code — Unity Workflow

> **Core Rules**: See [AGENTS.md](file:///home/meow/work/unity/test1/AGENTS.md) — this is the authoritative ruleset.

---

## ⚠️ MANDATORY: Before Any Unity Operation

**READ AGENTS.md FIRST** — specifically these sections:
1. `## ⛔ Non-Negotiables` — rules that MUST be followed
2. `### MCP Tool Limitations` — known gotchas with MCP tools
3. `### Scene Creation Checklist` — required steps for new scenes

**Do NOT rely on memory** — always check the current rules before:
- Creating/loading scenes
- Creating GameObjects or Prefabs
- Modifying components via MCP
- Any operation that touches Unity assets

---

## MCP Quick Reference (Common Gotchas)

| Operation | Correct | Wrong |
|-----------|---------|-------|
| Scene create path | `path="Assets/Scenes"` | `path="Assets/Scenes/MyScene.unity"` |
| Position/Rotation | `[x, y, z]` array | `{x:, y:, z:}` dict |
| Scene load | Use `build_index` or both `name`+`path` | Just `path` alone |
| New scene | Add Camera + AudioListener | Empty scene (no camera!) |

---

## When Given a Task

1. **Identify Unity surface area**: Scenes / Prefabs / UI Toolkit / UGUI / Addressables / ScriptableObjects
2. **Produce a minimal plan** (max 8 bullets)
3. **Implement** via file edits (C#, UXML, USS, asmdef, etc.)
4. **Verify**:
   - Build/compile succeeds
   - No unintended Prefab Overrides (Inspector → Overrides)
   - No UI Toolkit inline overrides (unless explicitly approved)
   - Play Mode safety respected for Addressables + ScriptableObjects
   - Active Scene set correctly
5. **Report**:
   - Changed files (paths)
   - Editor verification steps
   - Rollback plan (git revert points)

---

## Escalation to Tooling

If any step requires Editor interaction not possible via file edits:
- **Propose a Unity Editor script** (`MenuItem` or Companion API) to make it automatable
- Examples: Baking lighting, NavMesh, Asset import settings

---

## Deliverables (Every Task)

1. **List of changed files** (paths)
2. **How to wire in Unity** (components, Inspector settings, layers/tags)
3. **Verification steps** (what to check in Editor)
4. **Risk notes**:
   - Any created overrides (explain why if intentional)
   - Any inline styles (explain exception if allowed)
   - Play Mode persistence concerns
5. **Rollback plan** (git commit/revert reference)

---

## Project Context

- **Unity**: 6.x
- **Render Pipeline**: URP
- **Input**: New Input System
- **Force Text Serialization**: Enabled (required for AI to read .prefab/.unity)
- **Target Platforms**: PC (expandable)
- **Folder conventions**: `Assets/{Scripts,Prefabs,Materials,Scenes,Data,Plans}`

---

## References

- [AGENTS.md](file:///home/meow/work/unity/test1/AGENTS.md) — Operating rules (non-negotiables, checklists)
- [GEMINI.md](file:///home/meow/work/unity/test1/GEMINI.md) — Gemini-specific workflow
