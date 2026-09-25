# Validation Methodology

## Why controlled testing was needed

The strategy uses H4 conditions and can produce infrequent qualifying setups. Waiting for several natural events would make functional verification slow and non-deterministic.

## Validation layers

- **Compile validation:** production MQL4 source compiled with 0 errors and 0 warnings.
- **Controlled logic validation:** 12 deterministic scenarios executed with 12/12 PASS.
- **Safety review:** the alert-only boundary was checked to ensure no order-placement or order-management path was part of the production behavior.
- **Channel validation:** MetaTrader email and mobile push paths were exercised separately from strategy timing.
- **Persistence checks:** duplicate-event state handling was tested independently from normal signal generation.

## Important limitation

These tests validate software behavior against specified rules. They do not validate trading profitability or predict future market performance.
