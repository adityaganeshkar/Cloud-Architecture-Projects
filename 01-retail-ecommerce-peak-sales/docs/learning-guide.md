# Learning guide

Work through the architecture in this order. For each component, be able to explain its purpose, failure modes, scaling limit and security boundary.

## 1. Edge and traffic management

Study DNS, CDN caching, WAF rules, bot mitigation, API gateway rate limits and admission control. Separate cacheable browse traffic from checkout traffic. During a flash sale, protect the order path rather than allowing every request to overload it.

## 2. Domain boundaries

Catalog, cart, inventory, order, payment and notification have different data ownership and scaling patterns. Avoid splitting services only by technical layer. Keep inventory authority in one domain and do not let a cache decide whether stock exists.

## 3. Durable asynchronous processing

The Order API writes the order and outbox record in one transaction. A publisher relays the outbox event to a durable broker. Consumers use idempotency keys because delivery is at least once. Understand retries, visibility timeouts, ordering, dead-letter queues and replay safety.

## 4. Distributed transactions and compensation

A database transaction cannot atomically commit with an external payment provider. Model the order as a state machine. Use a saga-like workflow: reserve inventory, authorise payment, confirm order; compensate by releasing inventory when a definitive failure occurs. Reconcile ambiguous payment outcomes instead of blindly retrying.

## 5. Security and compliance

Use hosted payment fields or redirects and provider tokens so raw card data does not pass through application services. Apply least privilege, secret rotation, encryption, audit logging, input validation and secure webhook verification. Tokenisation reduces scope; it does not automatically remove PCI obligations.

## 6. Reliability and observability

Track request latency, error rate, saturation, queue depth and oldest-message age. Add business metrics such as checkout acceptance, payment outcomes, inventory reservation conflicts and order age by state. Practice dependency failure and recovery.

## 7. Capacity engineering

Estimate arrival rate, service time and concurrency. Load-test realistic mixes, not only a single endpoint. Increase load gradually, observe bottlenecks and validate autoscaling delay, database connection limits, cache hit rate and broker throughput.

## Exercises

1. Draw the checkout sequence and mark every durable write.
2. Explain what happens if the worker crashes after payment succeeds but before recording success.
3. Add an idempotency table and define key retention.
4. Design an inventory reservation with expiry and safe release.
5. Set an SLO for checkout acceptance and payment completion.
6. Compare the AWS, Azure and Google Cloud service choices for one deployment.
