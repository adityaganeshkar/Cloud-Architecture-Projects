# Order lifecycle

A suggested order state machine:

```mermaid
stateDiagram-v2
  [*] --> PENDING_PAYMENT
  PENDING_PAYMENT --> CONFIRMED: payment approved
  PENDING_PAYMENT --> PAYMENT_FAILED: definitive decline
  PENDING_PAYMENT --> RECONCILIATION_REQUIRED: ambiguous outcome
  RECONCILIATION_REQUIRED --> CONFIRMED: provider confirms approval
  RECONCILIATION_REQUIRED --> PAYMENT_FAILED: provider confirms decline
  CONFIRMED --> FULFILMENT_PENDING
  FULFILMENT_PENDING --> SHIPPED
  SHIPPED --> DELIVERED
  PAYMENT_FAILED --> [*]
  DELIVERED --> [*]
```

The order and outbox event are committed in one database transaction. Inventory reservation is an explicit operation with an expiry. Payment authorization uses a stable idempotency key derived from the order/payment attempt. Unknown provider outcomes enter reconciliation rather than an unsafe blind retry.
