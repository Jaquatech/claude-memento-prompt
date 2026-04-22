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

### Claude Desktop

**Simple path (works everywhere):**

1. Open [jaquatech.github.io/claude-memento-prompt](https://jaquatech.github.io/claude-memento-prompt/) and click **Copy prompt**
2. In Claude Desktop: **Customize → Create plugin → Create with Claude**
3. Paste the prompt as the plugin instruction content and save

The skill will be active for every new conversation. To use it in an existing conversation, start a fresh chat.

Alternatively, use **Project instructions** for a specific project: open the project → instructions → paste the prompt.

**Native skill file (Claude Desktop agent mode / Cowork):**

If you have Claude Desktop's agent mode (Cowork) enabled, a pre-packaged `memento.skill` file is available at [`dist/memento.skill`](dist/memento.skill). This is the native skill archive format — import it through Claude Desktop's skill import UI (if available) or drop it into your local skills directory. Once installed, invoke it with `/memento` or let it auto-trigger on non-trivial tasks.

---

### Claude Code CLI

Install from the marketplace in one command:

```shell
/plugin marketplace add Jaquatech/claude-memento-prompt
/plugin install memento@jaquatech-memento
/reload-plugins
```

Invoke explicitly:

```shell
/memento:memento What are the tradeoffs between PostgreSQL and MongoDB?
```

The skill also triggers automatically on any non-trivial task and whenever you say things like "think this through" or "reason carefully".

To test locally without installing: `claude --plugin-dir ./skill`

---

### Claude.ai Projects

Create a Project → open its instructions → paste the prompt. All conversations in that project inherit it.

---

### API

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
