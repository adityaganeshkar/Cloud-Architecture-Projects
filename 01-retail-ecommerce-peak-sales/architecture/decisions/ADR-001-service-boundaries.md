# ADR-001: Domain-oriented service boundaries

- **Status:** Accepted
- **Decision:** Separate catalog, cart, inventory, order, payment adapter and notification responsibilities by business capability.
- **Context:** These domains have different consistency, scaling and security needs.
- **Consequences:** Clear ownership and independent scaling improve change isolation, but introduce network failure, observability and distributed-data complexity. Start with a modular monolith if team size and operational maturity do not justify independently deployed services.
