# claude-memento-prompt

**A system prompt for Claude that applies the core insight of [Microsoft's Memento](https://github.com/microsoft/memento) — split long reasoning into discrete blocks, compress each block into a *memento* (a compact summary), and continue from there. No model fine-tuning required.**

🌐 **Live page:** [jaquatech.github.io/claude-memento-prompt](https://jaquatech.github.io/claude-memento-prompt/)

---

## What is this?

Memento is a Microsoft Research technique for extending the effective reasoning length of LLMs. Instead of one unbounded chain-of-thought, reasoning is split into blocks. After each block the model writes a short summary — the *memento* — and the block detail is evicted. The next block continues from the summary alone.

The original paper implements this with special tokens and KV-cache masking in vLLM. This repo adapts the same **conceptual structure** into a plain system prompt any Claude user can use today.

```
<block id="1" topic="...">
  Reason fully about the sub-problem here.
</block>

<memento id="1">
  Dense summary — only this carries forward.
</memento>

<block id="2" topic="...">
  Reason from memento(s), not from prior block content.
</block>
...
Final answer written from mementos only.
```

---

## How to use

Claude Desktop no longer has a plain "Custom Instructions" field. Use one of:

**A — Install the `.skill` file (Claude Desktop / Claude Code)**
Download [`memento.skill`](memento.skill) from this repo, then in Claude Desktop:
`Customize → Install plugin` → select the file.
The skill is immediately active in all conversations.

**B — Claude Desktop — Create plugin manually**
`Customize → Create plugin → Create with Claude`.
Paste the prompt text as the plugin instruction content.

**C — Claude.ai Project instructions**
Create a Project → open its instructions → paste the prompt. All conversations in that project inherit it.

**D — API**
Pass the prompt text as the `system` parameter in any Anthropic API call.

The full prompt text is on the [live page](https://jaquatech.github.io/claude-memento-prompt/) with a one-click copy button.

---

## Good use cases

- Multi-field integration/schema mapping (each block = a field family)
- Long debugging sessions (isolate hypotheses per block)
- Architecture decisions (compare options independently, synthesize from mementos)
- Document drafting (outline, logic, tone in separate blocks before writing)
- Code review (logic / correctness / performance / style each get a block)

---

## Credits

- Research paper: [microsoft/memento](https://github.com/microsoft/memento) (MIT License)
- Prompt adaptation: [Jaquatech / Jan Romppanen](https://github.com/Jaquatech) — public domain (CC0)

Not affiliated with Microsoft.
