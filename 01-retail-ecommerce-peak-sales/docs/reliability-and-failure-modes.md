# Reliability and failure modes

| Failure | User/business impact | Design response |
|---|---|---|
| Traffic surge | Latency and overload | CDN, rate limits, admission control, independent autoscaling |
| Cache outage | Higher database load | Bypass cache with protection, circuit breaker, controlled degradation |
| Database saturation | Checkout failures | Connection pooling, bounded concurrency, query tuning, capacity alarms |
| Broker backlog | Delayed order processing | Monitor oldest-message age, scale consumers within downstream limits |
| Duplicate delivery | Repeated processing | Idempotent consumers and unique business-operation keys |
| Payment timeout | Unknown payment state | Reconcile with provider before retrying |
| Poison message | Repeated worker failure | Bounded retries, DLQ, alert and controlled replay |
| Inventory race | Overselling | Atomic conditional reservation in authoritative inventory store |

## Operational principles

- Set explicit timeouts on every network call.
- Use bounded retries with exponential backoff and jitter.
- Do not retry non-idempotent side effects without a stable idempotency key.
- Apply circuit breakers and bulkheads to isolate dependencies.
- Alert on symptoms and business impact, not just CPU.
- Test restoration and replay procedures before a real incident.
