# Case Study: MT4 Multi-Timeframe Forex Signal EA

## Context

OSYSTIC engineered an alert-only MetaTrader 4 Expert Advisor for a rule-based swing-trading workflow. The challenge was less about order execution and more about making nuanced indicator timing rules deterministic, auditable, and resistant to false or duplicate alerts.

## Rule translation

The main signal path combined an H4 regime with an M30 closed-candle confirmation. The delivered baseline used H4 MACD 6,13,5, H4 OsMA 12,26,9, and M30 MACD 6,13,5.

For a BUY regime, H4 MACD had to remain above zero while H4 OsMA was below zero until the first qualifying closed M30 MACD bar confirmed above zero. SELL behavior mirrored the rule set in the opposite direction.

A separate pair-confirmation module tracked two symbol groups. Either symbol could lead, but the second confirmation had to arrive in the same direction within a maximum of 12 hours. Exact 12-hour confirmation remained valid; later confirmation was rejected.

## State and duplicate control

The EA maintained event state so the same qualifying event would not generate repeated notifications. The design still allowed a genuinely new confirmation sequence to alert later without requiring an artificial global reset unrelated to the trading rules.

## Alert-only safety boundary

The system intentionally did not place, modify, or close trades. Its responsibility ended at qualifying a signal and delivering the notification. This made the automation suitable for workflows where the trader performs an independent review before acting.

## Validation strategy

Naturally occurring H4 conditions can be rare, making live-only validation inefficient. OSYSTIC therefore separated production logic from a controlled test-only evidence harness.

The production source compiled with 0 errors and 0 warnings. Controlled scenarios completed 12/12 PASS and covered positive, negative, invalid, expired, duplicate, and new-sequence cases.

## Outcome

The Phase 1 engineering and controlled-validation baseline was completed and delivered. The project was later closed before the subsequent client-environment deployment stage was executed.

The result is a clean example of converting discretionary indicator rules into deterministic event-driven automation while preserving an explicit safety boundary between signal generation and trading execution.
