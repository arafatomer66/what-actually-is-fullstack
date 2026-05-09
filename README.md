# What Actually Is Fullstack?

> A reference menu of the real software engineering stack — 28 categories, ~400 items, picked from the messy reality of modern systems.

This isn't a tutorial. It's a **menu** you can browse when:

- You're starting a project and need to know what layers exist
- You're auditing a system and want to find what you're missing
- You're learning the field and tired of "frontend + backend" oversimplifications
- You're picking a stack and want to see your options before committing

---

## Table of Contents

- [The Problem with "Full Stack"](#the-problem-with-full-stack)
- [A Better Mental Model](#a-better-mental-model)
- [The Complete Stack](#the-complete-stack)
  - [1. Client Layer](#1-client-layer)
  - [2. Edge Layer](#2-edge-layer)
  - [3. Frontend](#3-frontend)
  - [4. API Gateway / BFF](#4-api-gateway--bff)
  - [5. Application Layer](#5-application-layer)
  - [6. Integration / Messaging](#6-integration--messaging)
  - [7. Data Layer](#7-data-layer)
  - [8. Data Engineering](#8-data-engineering)
  - [9. ML / AI Layer](#9-ml--ai-layer)
  - [10. Analytics & BI](#10-analytics--bi)
  - [11. Platform Layer](#11-platform-layer)
  - [12. Infrastructure Layer](#12-infrastructure-layer)
  - [13. CI/CD & Build](#13-cicd--build)
  - [14. Infrastructure as Code & Config](#14-infrastructure-as-code--config)
  - [15. Identity & Access](#15-identity--access)
  - [16. Security](#16-security)
  - [17. Observability](#17-observability)
  - [18. Reliability & Operations](#18-reliability--operations)
  - [19. Testing](#19-testing)
  - [20. Communication & Collaboration](#20-communication--collaboration)
  - [21. Payments & Commerce](#21-payments--commerce)
  - [22. Compliance & Governance](#22-compliance--governance)
  - [23. FinOps & Cost](#23-finops--cost)
  - [24. Content & CMS](#24-content--cms)
  - [25. Search & Discovery](#25-search--discovery)
  - [26. Developer Experience](#26-developer-experience)
  - [27. Domain-Specific Layers](#27-domain-specific-layers)
  - [28. Organizational Layer](#28-organizational-layer)
- [How to Use This List](#how-to-use-this-list)
- [Senior Engineer's Filter — Know Now vs Explore Later](#senior-engineers-filter--know-now-vs-explore-later)
- [What This List Is NOT](#what-this-list-is-not)
- [Contributing](#contributing)
- [License](#license)

---

## The Problem with "Full Stack"

You've seen the meme:

> **What we call Full Stack:** Frontend + Backend
>
> **The ACTUAL Full Stack:** Frontend, Database, Server, Networking, Cloud, CI/CD, Security, Containers, CDN, Backup...

The meme is directionally right — "frontend + backend" is a marketing simplification — but as a literal stack diagram it's muddled:

- **Security appears twice** without clarifying AppSec vs InfraSec
- **Ordering is wrong** — CDN sits at the edge (top of request path), not buried near "Backup"
- **Categories overlap** — Containers run on Cloud Infra, Networking spans both
- **It's missing major layers** — observability, message queues, caching, DNS, secrets, IaC, identity

A real production system has more than ten layers, and they don't stack as a single tower.

---

## A Better Mental Model

Real systems are **planes** (the request path) crossed with **cross-cutting concerns** (apply everywhere).

### The request path (top → bottom)

```
┌─────────────────────────────────────────────┐
│  CLIENT         Browser / Mobile / Desktop  │
├─────────────────────────────────────────────┤
│  EDGE           DNS → CDN → WAF → LB        │
├─────────────────────────────────────────────┤
│  FRONTEND       SPA / SSR / Static          │
├─────────────────────────────────────────────┤
│  API GATEWAY    Auth, rate-limit, routing   │
├─────────────────────────────────────────────┤
│  APPLICATION    Services / Workers / Jobs   │
├─────────────────────────────────────────────┤
│  INTEGRATION    Queues, Streams, Pub/Sub    │
├─────────────────────────────────────────────┤
│  DATA           OLTP DB · Cache · Search ·  │
│                 Object store · Warehouse    │
├─────────────────────────────────────────────┤
│  PLATFORM       Containers / Orchestration  │
│                 (K8s, ECS, serverless)      │
├─────────────────────────────────────────────┤
│  INFRASTRUCTURE Compute · Network · Storage │
│                 (VPC, subnets, IAM, cloud)  │
└─────────────────────────────────────────────┘
```

### Cross-cutting (touches every layer)

| Concern | Examples |
|---|---|
| **Identity & Auth** | OAuth/OIDC, IdP, SSO, mTLS |
| **Security** | AppSec (OWASP), InfraSec, secrets mgmt, SAST/DAST |
| **Observability** | Logs, metrics, traces, alerts, SLOs |
| **CI/CD** | Build, test, artifact, deploy, rollback |
| **IaC & Config** | Terraform, Helm, feature flags |
| **Reliability** | Backups, DR, runbooks, chaos testing |
| **Data governance** | PII handling, retention, audit, compliance |
| **Cost & FinOps** | Tagging, budgets, rightsizing |

---

## The Complete Stack

### 1. Client Layer

- Web browser (desktop, mobile)
- Native mobile (iOS, Android)
- Native desktop (macOS, Windows, Linux)
- Wearables, TV, console, embedded/IoT
- CLI tools, SDKs
- PWA / Service Workers / offline cache
- Browser storage (cookies, localStorage, IndexedDB)

### 2. Edge Layer

- DNS (Route53, Cloudflare DNS)
- CDN (Cloudflare, Fastly, CloudFront)
- WAF (web application firewall)
- DDoS protection
- TLS termination / certificate management (Let's Encrypt, ACM)
- Load balancer (L4/L7, ALB/NLB)
- Edge compute (Workers, Lambda@Edge)
- Reverse proxy (Nginx, Envoy)
- Bot mitigation

### 3. Frontend

- Framework (React, Vue, Angular, Svelte, Flutter Web)
- Rendering strategy (SPA, SSR, SSG, ISR, RSC)
- Build tooling (Vite, Webpack, Turbopack, esbuild)
- State management (Redux, Zustand, GetX, Signals)
- Styling (CSS, Tailwind, CSS-in-JS)
- Design system / component library
- Routing
- Forms & validation
- i18n / localization
- Accessibility (a11y)
- Performance (Core Web Vitals, bundle budgets)
- Analytics SDK
- Feature flags client

### 4. API Gateway / BFF

- API gateway (Kong, AWS API Gateway, Apigee)
- BFF (backend-for-frontend)
- Rate limiting, throttling, quotas
- Request authentication / authorization
- API routing, versioning
- GraphQL gateway / federation

### 5. Application Layer

- Web servers / app servers (Node, Spring, Django, Rails, .NET, Go)
- Microservices / monolith / modular monolith
- Background workers / job runners
- Cron / scheduled jobs
- Serverless functions (Lambda, Cloud Functions)
- Real-time (WebSockets, SSE, WebRTC, MQTT)
- API styles (REST, GraphQL, gRPC, tRPC, SOAP)
- Schema registries (Protobuf, Avro, OpenAPI)
- Service mesh (Istio, Linkerd, Consul)

### 6. Integration / Messaging

- Message queues (SQS, RabbitMQ, ActiveMQ)
- Event streaming (Kafka, Kinesis, Pulsar)
- Pub/sub (Redis Pub/Sub, Google Pub/Sub)
- Workflow engines (Temporal, Airflow, Step Functions)
- Webhooks
- iPaaS / integration platforms (Zapier, MuleSoft)
- Change data capture (Debezium)

### 7. Data Layer

- OLTP databases (Postgres, MySQL, SQL Server, Oracle)
- NoSQL (MongoDB, DynamoDB, Cassandra, Couchbase)
- Key-value (Redis, Memcached, etcd)
- Graph DB (Neo4j, Neptune)
- Time-series (InfluxDB, TimescaleDB, Prometheus TSDB)
- Search (Elasticsearch, OpenSearch, Algolia, Meilisearch)
- Vector DB (Pinecone, Chroma, pgvector, Weaviate)
- Object/blob storage (S3, GCS, R2, Azure Blob)
- File systems (EFS, FSx)
- Block storage (EBS)
- Data warehouse (Snowflake, BigQuery, Redshift, Databricks)
- Data lake / lakehouse (Iceberg, Delta, Hudi)
- Cache layers (Redis, Memcached, application cache)
- Database migrations (Flyway, Liquibase, Prisma Migrate)
- Connection pooling (PgBouncer, RDS Proxy)

### 8. Data Engineering

- ETL/ELT (Fivetran, Airbyte, Stitch)
- Transformation (dbt, Dataform)
- Orchestration (Airflow, Dagster, Prefect)
- Stream processing (Flink, Spark Streaming, ksqlDB)
- Batch processing (Spark, Hadoop)
- Reverse ETL (Hightouch, Census)
- Data catalog (DataHub, Amundsen, Collibra)
- Data quality (Great Expectations, Soda, Monte Carlo)

### 9. ML / AI Layer

- Model training (PyTorch, TensorFlow, JAX)
- Model serving (TorchServe, Triton, Vertex, SageMaker, Bedrock)
- Feature stores (Feast, Tecton)
- Experiment tracking (MLflow, W&B)
- LLM orchestration (LangChain, LlamaIndex)
- RAG pipelines (embedding, vector search, retrieval)
- Prompt management & evals (Braintrust, Langsmith, Promptfoo)
- AI gateway / proxy (LiteLLM, Portkey)
- Guardrails / safety filters
- GPU/accelerator infrastructure

### 10. Analytics & BI

- Product analytics (Amplitude, Mixpanel, PostHog)
- Web analytics (GA4, Plausible)
- Event tracking (Segment, Snowplow, Rudderstack)
- BI tools (Looker, Tableau, Metabase, Power BI)
- A/B testing & experimentation (Optimizely, GrowthBook, Statsig)
- Funnels, cohorts, dashboards

### 11. Platform Layer

- Containers (Docker, containerd, Podman)
- Orchestration (Kubernetes, ECS, Nomad)
- Serverless platforms (Lambda, Cloud Run, Fargate, Vercel)
- Service mesh (Istio, Linkerd)
- Helm / Kustomize / Operators
- Internal Developer Platform (Backstage, golden paths)
- PaaS (Heroku, Render, Fly.io, Railway)

### 12. Infrastructure Layer

- Compute (VMs, bare metal, GPUs, Spot/Reserved)
- Networking (VPC, subnets, route tables, NAT, peering, Transit Gateway)
- VPN / Zero Trust (Tailscale, Cloudflare Access, AWS VPN)
- Storage (EBS, EFS, S3-class)
- Cloud providers (AWS, GCP, Azure, OCI, multi-cloud)
- On-prem / hybrid / colocation
- Hardware (servers, switches, racks)

### 13. CI/CD & Build

- Source control (Git, GitHub, GitLab, Bitbucket)
- Code review tooling
- CI (GitHub Actions, GitLab CI, Jenkins, CircleCI, Buildkite)
- CD (Argo CD, Flux, Spinnaker)
- Artifact registries (npm, Maven, Docker Hub, ECR, Artifactory)
- Release strategies (blue/green, canary, rolling, feature flags)
- Build caching (Nx, Turborepo, Bazel, Gradle cache)

### 14. Infrastructure as Code & Config

- Terraform / OpenTofu / Pulumi / CloudFormation / CDK
- Ansible / Chef / Puppet / Salt
- Helm / Kustomize
- Config management (Consul, etcd, AWS AppConfig)
- Feature flags (LaunchDarkly, GrowthBook, Unleash)
- Secrets management (Vault, AWS Secrets Manager, Doppler, 1Password)

### 15. Identity & Access

- IdP (Okta, Auth0, Entra ID, Cognito, Clerk, WorkOS)
- Protocols (OAuth 2.0, OIDC, SAML, SCIM)
- MFA / passkeys / WebAuthn
- SSO
- IAM (cloud-level, role-based, ABAC)
- Service-to-service auth (mTLS, SPIFFE/SPIRE)
- API keys / tokens / JWT

### 16. Security

- AppSec (OWASP Top 10, input validation, output encoding)
- SAST / DAST / IAST
- SCA (Snyk, Dependabot, Renovate)
- Container scanning (Trivy, Grype)
- Secret scanning (GitGuardian, TruffleHog)
- IDS/IPS, EDR
- SIEM (Splunk, Datadog SIEM, Sentinel)
- SOAR (incident automation)
- Pentesting / red team / bug bounty
- Threat modeling
- Encryption at rest & in transit (KMS, HSM)
- Certificate management (PKI)
- Zero Trust architecture
- DLP (data loss prevention)

### 17. Observability

- Logs (Loki, ELK, Datadog Logs, CloudWatch)
- Metrics (Prometheus, Datadog, New Relic, CloudWatch)
- Traces (OpenTelemetry, Jaeger, Tempo, Honeycomb)
- APM (Datadog APM, New Relic, Dynatrace)
- Real user monitoring (RUM)
- Synthetic monitoring
- Profiling (continuous, flame graphs)
- Error tracking (Sentry, Bugsnag, Rollbar)
- Status pages (Statuspage, Incident.io)
- SLO/SLI tooling (Nobl9, Sloth)
- Alerting (PagerDuty, Opsgenie, Grafana Alerts)
- Dashboards (Grafana, Datadog)

### 18. Reliability & Operations

- On-call rotation
- Incident management (PagerDuty, Incident.io, FireHydrant)
- Runbooks
- Postmortems / blameless culture
- Chaos engineering (Gremlin, Chaos Mesh)
- Load testing (k6, Locust, JMeter, Gatling)
- Capacity planning
- Backup & restore (Velero, native cloud snapshots)
- Disaster recovery (RTO/RPO, multi-region)
- Game days

### 19. Testing

- Unit tests
- Integration tests
- E2E (Playwright, Cypress, Selenium)
- Contract tests (Pact)
- Visual regression (Chromatic, Percy)
- Performance tests
- Security tests
- Accessibility tests (axe-core)
- Mutation testing
- Test data management
- Mocking / stubs (WireMock, MSW)

### 20. Communication & Collaboration

- Email (SES, SendGrid, Postmark, Resend)
- SMS (Twilio, MessageBird)
- Push notifications (FCM, APNs, OneSignal)
- In-app messaging
- Notification orchestration (Knock, Courier)
- Customer support (Zendesk, Intercom, HelpScout)

### 21. Payments & Commerce

- Payment processors (Stripe, Adyen, Braintree, local processors)
- Billing & subscriptions (Stripe Billing, Chargebee, Recurly)
- Tax (Stripe Tax, Avalara, TaxJar)
- Fraud (Sift, Stripe Radar)
- Ledger / accounting
- PCI scope management

### 22. Compliance & Governance

- SOC 2, ISO 27001, HIPAA, GDPR, CCPA, PCI-DSS, FedRAMP
- Audit logging
- Data retention & deletion
- Consent management (OneTrust, Cookiebot)
- Data residency
- DPAs, sub-processor lists
- Risk register
- Vendor management

### 23. FinOps & Cost

- Cloud cost monitoring (Vantage, CloudHealth, native cost explorers)
- Tagging strategy
- Budgets & alerts
- Rightsizing, reserved capacity, savings plans
- Showback / chargeback

### 24. Content & CMS

- Headless CMS (Contentful, Sanity, Strapi, Payload)
- Traditional CMS (WordPress, Drupal)
- DAM (digital asset management)
- Media processing (Cloudinary, imgix, ffmpeg pipelines)
- Video streaming (Mux, Cloudflare Stream)
- Static site generators (Next.js, Astro, Hugo)

### 25. Search & Discovery

- Full-text search (Elasticsearch, OpenSearch, Meilisearch, Typesense)
- Hosted search (Algolia)
- Recommendation systems
- Personalization engines
- SEO infrastructure (sitemaps, structured data)

### 26. Developer Experience

- Local dev environments (Docker Compose, devcontainers, Tilt, Skaffold)
- Cloud dev environments (Codespaces, Gitpod)
- Documentation (Docusaurus, MkDocs, Mintlify)
- API docs (Swagger UI, Redoc, Bump)
- ADRs (architecture decision records)
- Code generators / scaffolding
- Linters & formatters (ESLint, Prettier, Biome, Ruff)
- Pre-commit hooks (Husky, lefthook)
- Monorepo tooling (Nx, Turborepo, Bazel, Lerna)

### 27. Domain-Specific Layers

Only relevant when you're building in these spaces:

- **IoT:** device fleet management, OTA updates, MQTT brokers
- **Gaming:** netcode, matchmaking, anti-cheat, game servers
- **Fintech:** ledger, KYC/AML, core banking integration
- **Healthcare:** HL7/FHIR, EHR integration
- **Geo:** PostGIS, mapping (Mapbox, Google Maps), routing engines
- **Blockchain:** nodes, indexers, wallets, smart contracts
- **AR/VR:** rendering pipelines, spatial computing

### 28. Organizational Layer

Not technical, but real:

- Team topologies (Stream-aligned, Platform, Enabling, Complicated-subsystem)
- Ownership / RACI / CODEOWNERS
- Engineering ladders, hiring
- Documentation culture, RFC process
- On-call comp, fairness
- Vendor procurement, legal review

---

## How to Use This List

**The list tells you what exists. It does not tell you what to pick.**

### Realistic project sizing

Nobody builds with all of it. A typical project uses 10–30% of this list:

| Project type | Realistic subset |
|---|---|
| Weekend MVP / side project | ~15–25 items (frontend, one DB, hosting, basic auth, Git) |
| Funded startup, year 1 | ~50–80 items (add observability, CI/CD, payments, basic security) |
| Series B+ / production SaaS | ~150–200 items (add SRE, compliance, data platform, IDP) |
| Enterprise / regulated | ~250–350 items (add governance, audit, multi-region, full security stack) |

### Three questions per category

When walking through the list for your project, ask:

1. **Do I need this layer at all?** (Most side projects don't need a service mesh.)
2. **What's the cheapest thing that works?** (SQLite > Postgres > distributed DB — pick the leftmost option that fits.)
3. **What's the upgrade path?** (Don't lock yourself out of the next step.)

### Pick by what you're optimizing for

| If you care most about... | Skip these | Don't skip these |
|---|---|---|
| Shipping fast | service mesh, IDP, multi-region, formal IaC | hosting, basic auth, error tracking |
| Reliability | exotic databases, ML | observability, runbooks, backups, on-call |
| Compliance | unmanaged services, hand-rolled auth | audit logs, IdP, encryption, vendor review |
| Cost | premium SaaS, multi-cloud | FinOps tagging, rightsizing, reserved capacity |
| Scale | monolith-only patterns | caching, queues, async, capacity planning |

---

## Senior Engineer's Filter — Know Now vs Explore Later

You don't need fluency in all 400 items. As a senior, you need **deep working knowledge of the request path and cross-cutting basics**, and the ability to **pick up specialized layers on demand** when a project actually needs them.

The mistake juniors make is trying to pre-learn everything. The mistake mid-levels make is going deep on the wrong things. The senior move is knowing **which 15% to be fluent in and which 85% to look up while building.**

### Need to know NOW (fluency — should be able to architect, debug, and reason about without looking up)

1. **HTTP & API design** — methods, status codes, idempotency, versioning, REST/GraphQL/gRPC tradeoffs
2. **One frontend framework deeply** — rendering, state, routing, lifecycle (React, Vue, or Angular)
3. **Relational databases** — schema design, indexes, transactions, isolation levels, N+1, query plans
4. **Auth fundamentals** — sessions vs tokens, OAuth/OIDC flow, password hashing, CSRF/XSS, JWT pitfalls
5. **Git** — branching, rebase, merge, resolving conflicts, recovering from mistakes
6. **One cloud provider's core** — compute, VPC/subnets, IAM, object storage, managed DBs
7. **Containers** — images, layers, volumes, networking, multi-stage builds
8. **Caching** — when to cache, invalidation strategies, Redis primitives, cache stampedes
9. **Async patterns** — queues vs streams, at-least-once vs exactly-once, idempotency, retries, DLQs
10. **Security baseline** — OWASP Top 10, TLS, secrets management (and why never to commit them)
11. **Observability essentials** — structured logging, the four golden signals, reading a trace
12. **Testing** — unit vs integration vs E2E, when to mock vs when not to, test pyramid
13. **CI/CD** — pipeline anatomy, artifacts, deployment strategies (blue/green, canary)
14. **Performance fundamentals** — Big-O, latency budgets, bottleneck identification, profiling
15. **System design tradeoffs** — CAP, consistency models, sharding, replication, eventual consistency
16. **Linux & networking basics** — processes, file descriptors, DNS, TCP, ports, `curl`/`dig`/`tcpdump`

### Explore WHILE BUILDING (look it up when the project demands it — pre-learning is mostly wasted)

- **Service mesh** (Istio, Linkerd) — only when service count justifies it
- **Stream processing** (Flink, Kafka Streams, ksqlDB) — only with real streaming workloads
- **ML/AI ops** — vector DBs, model serving, RAG, evals — only when shipping AI features
- **Specific BI tools** (Looker, Tableau, Metabase) — only when in a data-heavy role
- **Internal Developer Platforms** (Backstage, golden paths) — only at platform-team scale
- **Chaos engineering** (Gremlin, Chaos Mesh) — only when reliability budget supports it
- **SIEM/SOAR specifics** — only in a security-focused role
- **Compliance frameworks** (SOC 2, HIPAA, PCI-DSS) — only when an audit is on the calendar
- **Payment processors** (Stripe, Adyen) — only when actually building payments
- **Niche databases** (graph, time-series, vector) — only when the data shape demands it
- **Specific cloud services beyond core** — read the docs the day you need them
- **Domain-specific layers** (gaming netcode, EHR/FHIR, blockchain, IoT MQTT) — only in that domain
- **Multi-region / DR** — only past serious scale (Series B+, regulated)
- **Edge compute** (Workers, Lambda@Edge) — only when latency budget demands it
- **Advanced IaC** (custom Terraform modules, operators, CRDs) — fluency comes from doing, not reading
- **Service mesh, mTLS, SPIFFE** — only at zero-trust-mature orgs
- **Reverse ETL, data catalogs** (Hightouch, DataHub) — only in data-platform roles
- **Specialized observability** (continuous profiling, eBPF tooling) — only when the basic stack is exhausted

### The principle

**Fluency in the request path + cross-cutting basics; on-demand for specialized planes.**

If you can confidently design a request from browser to database and back — covering auth, caching, queue, observability, deployment — you have the senior baseline. Everything else is research-on-arrival, and that's fine. The list is here exactly so you know what to research when the moment comes.

---

## What This List Is NOT

- **Not a recipe.** It's a menu. You pick a subset.
- **Not prescriptive.** Postgres or MongoDB? K8s or Lambda? Depends on your data shape, team size, workload — choices need a real architecture conversation.
- **Not exhaustive for every domain.** IoT, gaming, fintech, healthcare each have specialized stacks barely sketched here.
- **Not future-proof.** Tools listed will get replaced. The categories are stable; the names rotate every 5 years.
- **Not a hiring rubric.** "Full stack engineer" realistically means client + edge + app + primary datastore. The other layers are platform/SRE/security/data territory. Nobody owns all of this.

---

## Contributing

Spotted a missing tool, layer, or category? Open a PR. Useful additions:

- New categories with clear scope (not overlapping existing ones)
- Tools that are genuinely production-popular (not "I tried it once")
- Better examples for sparse categories
- Corrections to wrong placements

---

## License

MIT — see [LICENSE](LICENSE).
