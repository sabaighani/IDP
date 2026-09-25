# platform/

Infrastructure as code for the platform itself, written in Terraform.

**What lives here**
- The local Kubernetes cluster definition (kind)
- Reusable Terraform modules and their tests
- Later: an optional AWS environment built from the same modules

**Why it is separate**
Infrastructure changes slowly and carries more risk than application changes. Keeping it in its own folder makes it easy to review, test and version independently.

**Filled in at:** step 03
