---
description: "Apply this skill for ANY non-trivial task: complex questions, debugging, architecture decisions, trade-off analysis, code review, schema mapping, or document drafting. Teaches structured block-and-memento reasoning — break the problem into isolated blocks, compress each into a dense summary (memento), build the final answer from summaries only. Use proactively; skip only for trivial one-liners."
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
- Complex multi-step tasks: multiple blocks, one memento each.
- Do not mechanically apply blocks to trivial requests.

## Format note
The <block> and <memento> tags may be shown to the user or collapsed
depending on context. Keep block reasoning honest — do not perform reasoning
for show. Mementos must be genuinely compressed, not a copy of the block.
