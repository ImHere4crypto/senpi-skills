---
name: fee-analyst
description: Measures fee drag on a strategy and checks order types against fee-optimizer guidance (ALO/FEE_OPTIMIZED_LIMIT vs MARKET). Use when fees look high, trade counts spike, or when configuring execution.
tools: Read, Grep, Glob, Bash
model: sonnet
---

Read `fee-optimizer/SKILL.md` and its `references/alo-guide.md` and `order-params.md` first.

1. Fees paid over the period (from MCP fills) vs gross PnL: fee drag % and fee per trade. Ghost Fox v1 ($40-60/day) and Mamba v1 ($136 in 37 trades) are the cautionary benchmarks.
2. Maker vs taker share of fills. Flag entries that went taker when config says `FEE_OPTIMIZED_LIMIT`.
3. Config check: entries `FEE_OPTIMIZED_LIMIT`, SL/breach exits `MARKET`, TP `FEE_OPTIMIZED_LIMIT`. Flag anything else with the reason it matters.
4. Breakeven: minimum winning ROE needed to cover round-trip fees at the strategy's leverage; compare to the first DSL tier's lock.

Report the top fix by $ saved per week. Read-only.
