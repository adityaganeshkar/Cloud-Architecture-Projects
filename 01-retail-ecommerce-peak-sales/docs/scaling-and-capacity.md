# Scaling and capacity

## Workload model

Model traffic by endpoint and user journey: browse, search, cart updates, checkout submission, order status and payment callbacks. A 10× peak multiplier is a planning assumption, not a capacity guarantee.

## Key relationships

- Approximate concurrency = arrival rate × average response time (Little's Law).
- Required worker throughput must exceed the sustained event arrival rate or the queue will grow.
- Queue depth alone is insufficient; monitor oldest-message age and time-to-drain.
- Cache hit rate reduces read pressure but does not protect authoritative writes.
- Database connections, locks, hot keys and transaction duration often become limits before application CPU.

## Test plan

1. Establish a baseline with representative data and request mix.
2. Ramp to 2×, 5× and 10× expected peak traffic.
3. Test sudden bursts as well as sustained plateaus.
4. Inject dependency latency and failures.
5. Verify order integrity, idempotency and inventory correctness after every run.
6. Record p50/p95/p99 latency, errors, saturation, queue age, DB connections and business outcomes.
7. Tune one bottleneck at a time and repeat.

Do not claim a capacity number until it has been measured in the target environment.
