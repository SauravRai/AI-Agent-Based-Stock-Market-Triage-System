Agent I/O Contract (Week 1)
Input (User → Agent)

User message + optional market data (OHLCV array).

Minimal Required Fields (by end of intake)

symbol

timeframe

capital

risk_percent

Optional:

preferred_strategy

volatility_filter

max_allocation %

Internal Object (Canonical)

Agent maintains a TradeCase object:

case_id

user_type

symbol

timeframe

capital

risk_percent

signal_type

entry

stop_loss

target

position_size

risk_reward_ratio

confidence

volatility_score

hitl_required

audit_log (tool calls + timestamps)

Output (Agent → User)
Required Output Format

Trade Decision

propose_trade

request_more_info

no_trade

escalate_risk_review

Trade Plan

Entry

Stop Loss

Target

Position Size

Risk Summary

Max capital at risk

Risk–Reward ratio

Allocation %

Signal Evidence

Pattern detected

Volume confirmation

Confidence level

Policy Flags

within_risk_limit: true/false

high_volatility: true/false

hitl_required: true/false

Next Steps

HITL approval question (if needed)

HITL Language

If approval required:

"Approve paper trade simulation? (yes/no)"
"Approve generating broker-ready order instructions? (yes/no)"

Agent must NOT proceed without explicit confirmation.