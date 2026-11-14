# ADR-002: Durable asynchronous order processing

- **Status:** Accepted
- **Decision:** Persist order state and an outbox event atomically, then publish to a durable broker for asynchronous processing.
- **Context:** Checkout should not wait for notifications, fulfilment or other slow downstream work, and accepted orders must not disappear after a process crash.
- **Consequences:** The system gains resilience and burst absorption, but must handle at-least-once delivery, duplicate events, eventual consistency, retries, DLQs and reconciliation.
