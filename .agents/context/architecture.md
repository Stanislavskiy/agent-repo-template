# Architecture
> Scope: system topology, service boundaries, data flow, infrastructure.
> For code style/patterns → `conventions.md`. For domain rules → `domain.md`.

## System Topology
```
[Draw ASCII or describe layers]

Client → [API Gateway] → [Service A] ──┬── [DB A]
                      ↘ [Service B] ──┴── [Cache]
                                      ↘── [Queue] → [Worker]
```

## Services / Modules
| Name | Responsibility | Owns | Consumes |
|------|---------------|------|----------|
| `[service-a]` | [one line] | `[db/table]` | `[service-b API]` |
| `[service-b]` | [one line] | `[db/table]` | `[queue topic]` |

## Data Flow
```
[Describe the critical happy path, e.g.:]
Request → Auth middleware → Rate limiter → Handler → Repository → DB
                                        ↘ Event bus → Async worker
```

## Infrastructure
| Concern | Technology | Notes |
|---------|-----------|-------|
| Hosting | `[provider/service]` | [region, tier] |
| Container | `[Docker / K8s / ECS]` | [cluster details] |
| Database | `[engine@version]` | [primary + replica?] |
| Cache | `[Redis / Memcached]` | [TTL strategy] |
| Queue | `[SQS / RabbitMQ / Kafka]` | [topics/queues] |
| CDN | `[CloudFront / Cloudflare]` | [assets, edge rules] |
| Secrets | `[Vault / SSM / Doppler]` | [rotation policy] |
| CI/CD | `[GitHub Actions / GitLab]` | [pipeline file path] |
| Observability | `[Datadog / Grafana]` | [key dashboards] |

## Deployment Environments
| Env | Branch | Auto-deploy | Notes |
|-----|--------|-------------|-------|
| `dev` | `develop` | ✅ on push | |
| `staging` | `main` | ✅ on push | mirrors prod data shape |
| `prod` | tags `v*` | manual approval | [rollback procedure] |

## Scalability Touchpoints
- **Horizontal scale:** `[which services scale out, HPA rules if K8s]`
- **Bottlenecks:** `[known hotspots, e.g. DB connection pool, specific queue]`
- **Rate limits:** `[external APIs with quotas the agent must not spam]`

## Security Boundaries
- Trust boundary: `[e.g. all inbound traffic terminates at API gateway]`
- Service-to-service auth: `[JWT / mTLS / IAM roles]`
- Never do: `[e.g. direct DB access from frontend, plain-text secrets in env]`
