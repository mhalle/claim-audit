# Claim Audit

A Claude Code skill for auditing claims made by LLMs or humans, using information-theoretic grounding analysis.

**[Download latest skill](https://github.com/mhalle/claim-audit/releases/latest/download/claim-audit.skill)**

## What It Does

Evaluates whether claims are actually grounded in cited evidence or merely decorative, using the "scrub-and-probe" method from compression theory. A claim is **grounded** if removing the evidence would change the claim. A claim is **unsubstantiated** if the same assertion would be made regardless of the evidence.

Works for:
- AI-generated text (detecting hallucination)
- Human-authored text (detecting unsupported claims, citation padding)
- Self-audit of your own writing

## Installation

### Claude Code

```bash
curl -L https://github.com/mhalle/claim-audit/releases/latest/download/claim-audit.skill -o /tmp/claim-audit.skill
unzip /tmp/claim-audit.skill -d ~/.claude/skills/
```

### Claude on the Web

Download the [latest .skill file](https://github.com/mhalle/claim-audit/releases/latest/download/claim-audit.skill) and upload it to your conversation.

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

### Relationship to the Paper

This skill is a **qualitative interpretation** of the paper's quantitative framework. The paper defines precise mathematical constructs (KL divergence, information budgets, ISR thresholds); this skill translates them into heuristic judgments an LLM can apply through reasoning:

| Paper (quantitative) | Skill (qualitative) |
|---------------------|---------------------|
| Δ̄ = 𝔼_π[KL(P ∥ S_π)] | "high / medium / low / zero Δ" |
| ISR = Δ̄ / B2T | "high / medium / low confidence" |
| ISR < 1 → abstain | INSUFFICIENT verdict |
| log(p₁/p₀) nats | "would you know this without the source?" |

The skill cannot compute actual KL divergence between prior and posterior—it uses judgment to approximate what the math would show. For computational approaches, see the [Strawberry MCP implementation](https://github.com/leochlon/pythea/tree/main/strawberry).

### What This Skill Adds

Beyond the paper's framework, this skill introduces:

- Claim taxonomy (factual, interpretive, synthetic, editorial)
- Salience classification (load-bearing, supporting, illustrative)
- Rhetorical fairness evaluation
- Proportionate remediation strategies
- Human-specific failure modes (confirmation citation, authority padding, scope creep)
- Batch audit and document audit protocols
- Subagent strategies for unbiased self-audit

## Development

### Versioning

This project uses semantic versioning. To release a new version:

1. Update `metadata.version` in `SKILL.md`
2. Add entry to `CHANGELOG.md`
3. Commit, tag, and push:
   ```bash
   git add -A && git commit -m "Bump to vX.Y.Z"
   git tag vX.Y.Z
   git push && git push --tags
   ```

The GitHub Action will automatically build and attach `.skill` files to the release.

**Important:** Bump the version for documentation changes, not just code changes. The LLM reads the skill documentation and may change behavior based on it—documentation *is* the implementation for a skill.

## License

MIT
