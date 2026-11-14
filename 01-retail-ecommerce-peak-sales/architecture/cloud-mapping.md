# Multi-cloud service mapping

| Capability | AWS | Azure | Google Cloud |
|---|---|---|---|
| CDN / edge | CloudFront | Azure Front Door | Cloud CDN |
| WAF | AWS WAF | Azure Web Application Firewall | Cloud Armor |
| API management | API Gateway | API Management | API Gateway / Apigee |
| Containers | ECS / EKS | AKS / Container Apps | GKE / Cloud Run |
| Cache | ElastiCache | Azure Managed Redis | Memorystore |
| Queue / events | SQS / SNS / EventBridge | Service Bus / Event Grid | Pub/Sub |
| Relational database | Aurora / RDS | Azure Database for PostgreSQL | Cloud SQL / AlloyDB |
| Object storage | S3 | Blob Storage | Cloud Storage |
| Secrets and keys | Secrets Manager / KMS | Key Vault | Secret Manager / Cloud KMS |
| Observability | CloudWatch / X-Ray | Azure Monitor / Application Insights | Cloud Monitoring / Cloud Trace |

## Selection principles

- Prefer managed services for commodity capabilities unless portability or control requirements justify operating them.
- Select one cloud as the primary deployment target; equivalent services are not identical in semantics, limits or pricing.
- Validate regional availability, quotas, durability, failover behavior, networking costs and operational maturity.
- Keep domain interfaces stable so service implementations can change without leaking provider-specific concepts throughout the application.
