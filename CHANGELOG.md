# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2025-01-12

### Added
- Initial release
- Core audit protocol with three dimensions: source fidelity, information delta, rhetorical fairness
- Claim taxonomy: factual, interpretive, synthetic, editorial
- Salience classification: load-bearing, supporting, illustrative
- Nine verdict types including INSUFFICIENT and UNVERIFIABLE
- Confidence calibration based on ISR thresholds
- Guidance for inaccessible sources
- Resource files:
  - `theory.md` - Information-theoretic framework with EDFL, ISR, and empirical findings
  - `failure-modes.md` - 12 common failure patterns
  - `remediation.md` - Strategies and decision tree
  - `document-audit.md` - Protocol for complete documents

### Credits
- Based on [Predictable Compression Failures](https://arxiv.org/abs/2509.11208) by Chlon, Karim, & Chlon (Hassana Labs)
- Adapted from [Strawberry MCP](https://github.com/leochlon/pythea/tree/main/strawberry)
