# Operations runbook

## Flash-sale readiness

- Confirm quotas, autoscaling limits, database capacity and broker throughput.
- Verify dashboards and paging routes.
- Validate CDN cache rules and WAF/rate-limit policies.
- Confirm payment provider status and webhook delivery.
- Check DLQ is empty or has an understood baseline.
- Run a controlled load test and verify rollback procedures.

## Queue backlog

1. Check oldest-message age, arrival rate and consumer throughput.
2. Check downstream payment/database saturation before increasing worker count.
3. Scale consumers gradually within dependency limits.
4. Inspect DLQ and repeated error classes.
5. Replay only after the cause is fixed and idempotency is verified.

## Payment ambiguity

1. Stop blind retries for the affected payment operation.
2. Query the provider using its idempotency/reference key.
3. Reconcile provider state with the order state.
4. Confirm or fail the order based on authoritative provider result.
5. Release inventory only after a definitive failure/compensation decision.
6. Record the incident and improve the runbook.
