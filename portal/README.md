# portal/

The developer portal, built on Backstage. This is the front door of the platform.

**Planned features**
- Software catalog fed by each service's `catalog-info.yaml`
- A "Create service" template that opens a pull request with a new `service.yaml`
- Kubernetes and ArgoCD plugins showing the live state of each service
- TechDocs for service documentation

**Design note**
The platform works without the portal. The portal is a thin interface on top of Git pull requests, so it can be added, replaced or removed without changing the core.

**Filled in at:** step 11 (optional)
