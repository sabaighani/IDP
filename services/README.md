# services/

The workloads that run on the platform. Each service has its own folder.

**Expected layout of one service**
```
services/<name>/
├── src/                 application code
├── Dockerfile
├── chart/               Helm chart (uses the shared platform labels)
├── docs/ + mkdocs.yml   service documentation (TechDocs-ready)
├── service.yaml         the platform contract (step 09)
└── catalog-info.yaml    Backstage catalog entry
```

**Why it matters**
`service.yaml` is the only file a developer writes to get a service onto the platform. `catalog-info.yaml` lets a developer portal such as Backstage discover the service later without rework.

**Filled in at:** step 01
