# Technical Overview

## Production responsibilities

The production EA was responsible for:

- reading MT4 indicator state across H4 and M30;
- evaluating only completed candles for confirmation;
- maintaining H4 regime validity until M30 confirmation;
- tracking asynchronous H4 MACD zero-line confirmation across configured symbol groups;
- enforcing a 12-hour maximum pair-confirmation window;
- preventing duplicate notification delivery;
- allowing later genuine confirmation sequences;
- sending email and MetaTrader mobile push notifications;
- avoiding all trade placement and order-management operations.

## State-machine model

Each pair group maintains enough state to distinguish:

1. no active confirmation window;
2. first symbol confirmed;
3. second symbol confirmed in matching direction within window;
4. expired window;
5. wrong-direction rejection;
6. already-processed event;
7. new valid sequence.

This reduces ambiguous behavior that commonly appears when trading rules are implemented as stateless indicator checks.
