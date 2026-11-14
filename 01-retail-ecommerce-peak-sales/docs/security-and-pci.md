# Security and PCI considerations

This is a design checklist, not a compliance assessment.

- Use a PCI-compliant payment service provider with hosted fields or redirect-based checkout.
- Keep primary account numbers and card verification values out of application logs, databases, traces and analytics.
- Store provider tokens and references only where required; protect them as sensitive data.
- Verify payment webhooks cryptographically, validate timestamps and prevent replay.
- Use TLS in transit and managed encryption at rest.
- Store secrets in a managed secret store; rotate credentials and avoid committing secrets.
- Apply least-privilege service identities and separate production environments.
- Validate and encode untrusted input; protect administrative interfaces with strong authentication.
- Maintain audit trails for order, refund, inventory and privileged operations.
- Confirm actual PCI scope with the acquiring bank or qualified assessor; tokenisation does not by itself eliminate compliance obligations.
