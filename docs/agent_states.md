Agent States: Semi-Autonomous Share Market Analyst (Week 1)
Objective

Design a single-agent workflow that generates risk-aware, explainable trade ideas by:

ingesting market + user context

detecting valid technical setups

evaluating risk constraints

generating structured trade proposals

requiring Human-in-the-Loop (HITL) approval before any execution-level action

The agent must NEVER execute real trades.

State Machine (High Level)
1. intake

Parse user request (symbol, timeframe, capital, risk preference).

Identify user type (trader / analyst / portfolio manager).

Initialize TradeCase object.

Determine required data (price, volume, indicators).

2. missing_info_check

Ensure required inputs exist:

symbol

timeframe

capital

risk %

If missing → ask targeted questions and stop.

3. data_ingestion

Accept OHLCV price data (historical candles).

Normalize into structured format.

Validate data integrity (no nulls, proper sequence).

4. signal_detection

Call detect_signal tool.

Identify breakout / pullback / support bounce.

Attach confidence score.

5. risk_evaluation

Call evaluate_risk tool.

Compute:

position size

max risk amount

risk–reward ratio

Validate against user-defined constraints.

6. proposal_generation

Generate structured trade plan:

Entry

Stop loss

Target

Position size

Thesis

Confidence

Assess HITL requirement.

7. human_approval (HITL)

Must trigger if:

User requests real execution

Allocation > configured % threshold

Confidence < 0.7

High volatility detected

Risk > user allowed %

Ask explicitly:

"Approve paper trade simulation? (yes/no)"
OR
"Approve generating broker-ready order instructions? (yes/no)"

8. finalize

Produce:

Structured trade summary

Risk breakdown

Scenario analysis

Audit log of tool calls

Never place real trade.

Stop Conditions (Must Ask Human)

User says “execute now”

Allocation > 5% capital

Risk exceeds allowed %

Confidence < 0.6

Conflicting signals

Extreme volatility spike

Output Guarantee

Every final answer must include:

Trade Decision (propose_trade | request_more_info | no_trade | escalate_risk_review)

Entry / Stop / Target

Position Size

Risk–Reward Ratio

Confidence Score

Evidence Used (signal type + volume confirmation)

HITL Question (if applicable)