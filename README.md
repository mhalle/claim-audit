# Claim Audit

A Claude Code skill for auditing claims made by LLMs or humans, using information-theoretic grounding analysis.

## What It Does

Evaluates whether claims are actually grounded in cited evidence or merely decorative, using the "scrub-and-probe" method from compression theory. A claim is **grounded** if removing the evidence would change the claim. A claim is **unsubstantiated** if the same assertion would be made regardless of the evidence.

Works for:
- AI-generated text (detecting hallucination)
- Human-authored text (detecting unsupported claims, citation padding)
- Self-audit of your own writing

## Installation

Download the release zip and install as a Claude Code skill, or clone directly:

```bash
# Clone to your skills directory
git clone https://github.com/mhalle/claim-audit ~/.claude/skills/claim-audit
```

## Usage

Trigger phrases:
- "verify this claim"
- "audit for hallucination"
- "is this supported by the evidence"
- "fact-check this"
- "check if grounded"
- "check my sources"
- "audit my reasoning"
- "does this hold up"

## Credits

### Theoretical Foundation

This skill operationalizes concepts from:

**Paper:** [Predictable Compression Failures: Why Language Models Actually Hallucinate](https://arxiv.org/abs/2509.11208)
**Authors:** Leon Chlon, Ahmed Karim, Maggie Chlon (Hassana Labs)

Key concepts adapted:
- Information Delta (Δ) — posterior/prior probability ratio
- Information Source Reliability (ISR) — bits of evidence per bits of claim
- Compression-theoretic model of hallucination/confabulation

### MCP Implementation

Based on the Strawberry MCP server from the Pythea project:
https://github.com/leochlon/pythea/tree/main/strawberry

### What This Skill Adds

- Claim taxonomy (factual, interpretive, synthetic, editorial)
- Salience classification (load-bearing, supporting, illustrative)
- Proportionate remediation strategies
- Human-specific failure modes (confirmation citation, authority padding, scope creep)
- Batch audit and document audit protocols

## License

MIT
