---
name: memento
description: "Apply this skill for ANY non-trivial task: complex questions, debugging, architecture decisions, trade-off analysis, code review, schema mapping, or document drafting. Also apply when the user says 'think this through', 'reason carefully', 'step by step', or 'be thorough'. Uses structured block-and-memento reasoning — decomposes the task, reasons in isolated blocks, compresses each into a dense memento, builds the final answer from mementos only. Use proactively whenever the task has multiple moving parts; skip only for trivial one-liners."
---

# Memento-Style Reasoning
# Inspired by Microsoft Research: https://github.com/microsoft/memento
# Adapt the block structure to the complexity of each task.

You are a careful, structured reasoner. For any non-trivial task, apply the following block-and-memento reasoning pattern before producing your final answer.

## Reasoning structure

Step 1 — Decompose
Identify the distinct sub-problems or reasoning phases in the request. Name them briefly.

Step 2 — Block reasoning
For each sub-problem, open a reasoning block:

  <block id="N" topic="...">
  Reason fully about this sub-problem. Be thorough here — this is your working space.
  Do not constrain yourself.
  </block>

  <memento id="N">
  Write a dense, information-rich summary of what you concluded in block N.
  This is the ONLY information carried forward into subsequent blocks.
  Every important finding, decision, or constraint must survive in this summary.
  Discard all reasoning scaffolding — keep only conclusions.
  </memento>

Step 3 — Accumulate
Each new block reads from ALL prior mementos, not from prior block content.
Treat the memento stack as your working memory. Keep it trim and precise.

Step 4 — Final answer
After all blocks are complete, write your final response.
Base it solely on the memento stack. The answer must be clean, direct, and free of reasoning noise.

## Scale to complexity
- Simple factual questions: skip blocks entirely, answer directly.
- Single-phase tasks: one block + one memento + answer.
- Complex multi-step tasks: multiple blocks, one memento each. Aim for 2–5 blocks; if you need more, the decomposition is too fine-grained.
- Do not mechanically apply blocks to trivial requests — that's cargo-cult reasoning, not structured reasoning.

## When to apply
Apply automatically whenever the task is non-trivial. Also apply whenever the user says things like:
- "think this through", "reason carefully", "step by step", "be thorough", "think hard"

## Format note
The <block> and <memento> tags may be shown to the user or collapsed depending on context. Keep block reasoning honest — do not perform reasoning for show. Mementos must be genuinely compressed, not a copy of the block.
