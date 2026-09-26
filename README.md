# golden-path

A small internal developer platform, built step by step on Kubernetes, and documented as a video series.

A developer adds one YAML file to Git. The platform builds, scans, signs, deploys and monitors the service automatically.

> **Status:** work in progress. Step 00 (repository scaffold) is done. See the [roadmap](#roadmap).

## Why this project

<!-- TODO(human): 3-4 sentences in your own words. Who is this for, what problem does it solve, and what will a reader be able to do after following along? -->

## How it works

```
Developer pushes a change
        │
        ▼
CI (GitHub Actions)     lint · test · build image · scan · SBOM · sign
        │
        ▼
Git (gitops/)           desired state of the cluster, single source of truth
        │
        ▼
ArgoCD                  syncs the cluster to match Git
        │
        ▼
Kubernetes (kind)       Kyverno enforces policy · Prometheus + Grafana observe
        ▲
        │
Terraform (platform/)   creates the cluster and its foundations
```

## Repository layout

| Path | Purpose |
|---|---|
| [`platform/`](platform/) | Terraform: cluster and infrastructure |
| [`gitops/`](gitops/) | Desired cluster state, watched by ArgoCD |
| [`services/`](services/) | Workloads that run on the platform |
| [`policies/`](policies/) | Kyverno policies (policy as code) |
| [`portal/`](portal/) | Backstage developer portal (optional, last step) |
| [`scripts/`](scripts/) | Helper scripts used by the Taskfile |
| [`docs/`](docs/) | Architecture decision records and per-step notes |
| [`.github/workflows/`](.github/workflows/) | CI pipelines |

## Roadmap

Each step ends with a working repository, marked with a git tag (`step-00`, `step-01`, ...).

| Step | What we build | Visible result | AI companion |
|---|---|---|---|
| 00 | Repository scaffold, Taskfile | `task doctor` checks your tools | |
| 01 | Sample service in Docker | Runs with one command | |
| 02 | CI with GitHub Actions | Green check on every push | AI pull request review |
| 03 | Local cluster with Terraform and kind | `task up` creates a cluster | Terraform MCP server |
| 04 | Deploy with Helm | App opens in the browser | Kubernetes MCP troubleshooting |
| 05 | GitOps with ArgoCD | Push to Git, app updates itself | ArgoCD MCP server |
| 06 | Supply chain security | Unsigned image is rejected | |
| 07 | Policy as code with Kyverno | Deploy without limits is blocked | |
| 08 | Observability | Dashboard and a real alert | Grafana MCP: "why did it fire?" |
| 09 | The golden path | One YAML file, everything automated | |
| 10 | Failure scenarios and demo | Break it, watch it recover | Agent-assisted diagnosis |
| 11 | Developer portal (optional) | "Create service" form opens a PR | |

## Prerequisites

| Tool | Used for |
|---|---|
| [Git](https://git-scm.com/) | Source control |
| [Docker](https://www.docker.com/) | Containers and the kind cluster |
| [Task](https://taskfile.dev/) | Runs the project's commands |
| [Terraform](https://www.terraform.io/) | Infrastructure as code |
| [kind](https://kind.sigs.k8s.io/) | Local Kubernetes cluster |
| [kubectl](https://kubernetes.io/docs/tasks/tools/) | Talk to the cluster |
| [Helm](https://helm.sh/) | Package and deploy apps |

Check that everything is installed:

```
task doctor
```

## Quick start

```
task --list      # see all available tasks
task doctor      # verify your tools
task up          # create the platform (available from step 03)
task down        # tear it down
```

## Following along

Every step is a git tag. To see the repository exactly as it was at a given step:

```
git checkout step-03
```

Run `task down` before switching to another step, because the cluster and Terraform state live outside Git.

## Design principles

- **Git is the source of truth.** Nobody changes the cluster by hand.
- **AI proposes, humans approve.** AI tools work with read-only access by default, and every change goes through a pull request, CI and policy checks.
- **API-first.** The platform runs without a portal. The portal is only an interface on top of pull requests.
- **Every decision is written down.** See [`docs/adr/`](docs/adr/).

## License

To be decided.
