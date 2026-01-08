# Documentation Standards (LLM Guide)

## Purpose
This file defines a concise, consistent format for language/tool docs in this repo. The goal is a quick reference for advanced topics, with a small refresher section when helpful.

## General Rules
- Keep it short and scannable; prefer bullets over paragraphs.
- Favor advanced/real-world usage over basic syntax.
- Include authoritative external links near the top.
- Use clear headings; avoid deep nesting.
- Only add sections that add value; skip empty sections.
- Use fenced code blocks with a language tag.
- Prefer ASCII; use Unicode only when the source material requires it.

## Suggested Format (Template)
Use this as a starting point and remove sections that do not apply.

```markdown
# <Title>
Short intro explaining the concept, language, tool, or project.
1-3 sentences max.

## External Documentation
- [Authoritative Source](https://example.com)
- [Authoritative Source](https://example.com)

## Table of Contents
- [<Section>](#section)
- [<Section>](#section)

## Key Concepts
1-2 sentences of context.
- Syntax: <short note>
- Unique rule: <short note>
- Why it exists: <short note>
- When it is useful: <short note>

\`\`\`<lang>
// quick demo
\`\`\`

## Advanced Patterns
- Pattern: <what it is>
- When to use: <brief>
- Tradeoffs: <brief>

## Pitfalls
- Common mistake and the fix.
- Edge case to remember.

## Tooling / Ecosystem (Optional)
- <tool> for <purpose>
- <tool> for <purpose>

## Refresher (Optional)
One short section for basics if needed.

## Related Topics
- [Doc Name](DocName.md)
```

## Notes for LLMs
- Keep sections under ~8 bullets when possible.
- If a topic is huge, split into multiple docs and cross-link.
- Prefer a single, minimal example over multiple long examples.
- If you must add a table, keep it small and useful.
