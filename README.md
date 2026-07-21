# deep-interview-skills

Standalone Claude Code skills for Socratic requirements-gathering before implementation. Ask one question at a time, score ambiguity after every answer, stop asking once clear enough, then write a spec.

- [`deep-interview/`](deep-interview/SKILL.md) -- full version: Round 0 topology gate for multi-component scope, per-component clarity tracking, ontology extraction/convergence tracking, challenge-agent perspective shifts (Contrarian/Simplifier/Ontologist).
- [`deep-interview-lite/`](deep-interview-lite/SKILL.md) -- lightweight version: same core loop (one question at a time, ambiguity scoring, spec output), no topology/ontology tracking, no challenge agents. Use for small/single-deliverable tasks.

Both are self-contained -- no external skill or plugin dependencies. State and specs are written under a local `.deep-interview/` (or `.deep-interview-lite/`) directory in the project you're working in.

## Install

Drop a folder into your Claude Code skills directory, e.g.:

```
cp -r deep-interview ~/.claude/skills/deep-interview
cp -r deep-interview-lite ~/.claude/skills/deep-interview-lite
```
