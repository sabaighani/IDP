# gitops/

The desired state of the cluster. ArgoCD watches this folder and makes the cluster match it.

**What lives here**
- ArgoCD `Application` and `ApplicationSet` definitions
- One overlay per environment: `dev`, `staging`, `prod`

**Rule**
Git is the single source of truth. Nobody changes the cluster by hand; every change is a pull request to this folder.

**Filled in at:** step 05
