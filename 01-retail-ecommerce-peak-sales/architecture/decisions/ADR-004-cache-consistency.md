# ADR-004: Cache read-heavy catalog data, not inventory authority

- **Status:** Accepted
- **Decision:** Cache catalog/product reads where safe; keep stock reservation in an authoritative transactional store.
- **Context:** Flash-sale browse traffic is read-heavy, while inventory correctness is a business invariant.
- **Consequences:** Caching improves latency and reduces database load, but requires invalidation/TTL strategy. Checkout must never trust a potentially stale cache as the final stock authority.
