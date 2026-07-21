---
name: deep-interview-lite
description: Lightweight Socratic interview that clarifies a vague idea before implementation. Asks one question at a time, scores ambiguity after each answer, writes a short spec once clear enough. Use for small-to-medium tasks where the full deep-interview's topology/ontology tracking is overkill.
argument-hint: "<idea or vague description>"
---

<Purpose>
Turns a vague idea into a short written spec by asking one targeted question at a time and scoring ambiguity after every answer. Stops asking once ambiguity drops below a threshold, writes the spec, then asks the user how to proceed. No topology gate, no ontology tracking, no challenge-agent personas -- just the core loop.
</Purpose>

<Use_When>
- User has a vague idea and a few rounds of Q&A would prevent building the wrong thing
- Task is small/medium -- one clear deliverable, not a multi-component system
- User wants some clarification but not a long structured interview
</Use_When>

<Do_Not_Use_When>
- Request already has file paths, function names, or acceptance criteria -- just do it
- Idea has multiple independent components/workstreams that could each go wrong in different ways -- use the full deep-interview instead (it tracks each component separately)
- User explicitly wants the full deep-interview
</Do_Not_Use_When>

<Steps>

## 1. Resolve threshold
Default ambiguity threshold: `0.2` (20%). Check `.claude/settings.json` for a `deepInterview.ambiguityThreshold` override if present; otherwise use the default. State it once: "Clarity target: ambiguity <= {threshold*100}%."

## 2. Detect greenfield vs brownfield
Quick check: does the repo already have relevant source code for this idea?
- Brownfield: skim the relevant files yourself first (grep/read, or a search subagent). Never ask the user something the code already answers.
- Greenfield: skip this step.

## 3. Interview loop
Repeat until ambiguity <= threshold or the user says "enough" / "just build it" (allowed from round 2 on):

1. **Ask exactly one question**, targeting whichever of these three is least clear so far:
   - **Goal** -- what exactly should happen, stated as one unambiguous sentence
   - **Constraints** -- boundaries, non-goals, what's explicitly out of scope
   - **Success criteria** -- how you'd verify it's done (a test you could write)
   - (brownfield adds a 4th: **Context** -- how this fits the existing code)
   Say in one line which dimension you're targeting and why, then ask.
2. **Score ambiguity** after the answer:
   - Greenfield: `ambiguity = 1 - (goal*0.4 + constraints*0.3 + criteria*0.3)`
   - Brownfield: `ambiguity = 1 - (goal*0.35 + constraints*0.25 + criteria*0.25 + context*0.15)`
   - Show the score and which dimension is still weakest.
3. **Hard cap at round 8**: proceed with whatever clarity exists, note the risk.

## 4. Write the spec
Once ambiguity <= threshold (or early exit / hard cap), write a short spec to `.deep-interview-lite/{slug}.md`:

```markdown
# Spec: {title}
- Ambiguity: {score}% (threshold {threshold}%) | Status: {PASSED|EARLY_EXIT|CAPPED}

## Goal
{one clear sentence}

## Constraints / Non-Goals
- {...}

## Acceptance Criteria
- [ ] {testable criterion}

## Open Questions
- {anything still unresolved, if early exit or capped}
```

## 5. Ask how to proceed
Don't touch code yet. Ask: "Spec's ready (ambiguity {score}%). Implement now, write a plan first, keep refining, or stop here?" Proceed only after the user picks.

</Steps>

<Example>
```
Clarity target: ambiguity <= 20%.

Round 1 | Targeting: Goal | "Add a search feature" -- what should the user actually be able to search: this app's own content, or an external source?
> user's own saved notes

Ambiguity: 62% (Goal 0.6, Constraints 0.0, Criteria 0.0)

Round 2 | Targeting: Constraints | Should search match full text, or just titles/tags?
> full text, case-insensitive

Ambiguity: 38% (Goal 0.8, Constraints 0.6, Criteria 0.0)

Round 3 | Targeting: Success criteria | What result would tell you it's working -- exact match only, or should typos/partial words also surface results?
> exact substring match is fine for v1

Ambiguity: 15% (Goal 0.9, Constraints 0.8, Criteria 0.8) -- threshold met.
```
</Example>
