# ADR-003: Hosted payment capture and tokenisation

- **Status:** Accepted
- **Decision:** Use a PCI-compliant payment provider's hosted fields or redirect flow and store provider tokens/references rather than raw card data.
- **Context:** Handling cardholder data directly increases security and compliance scope.
- **Consequences:** The application depends on provider availability and token semantics. Tokenisation reduces scope but does not remove the need to validate PCI obligations, secure webhooks and protect tokens.
