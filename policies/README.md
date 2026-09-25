# policies/

Policy as code. Rules the cluster enforces, written as Kyverno policies.

**Examples planned**
- Every container must set CPU and memory limits
- Only signed images are allowed to run
- Required labels (`team`, `app.kubernetes.io/name`) must be present

**Why it matters**
Policies are reviewed and versioned like any other code, so security and quality rules are not tribal knowledge.

**Filled in at:** step 07
