# quickpat-zpoz2owp

Multi-chart quickstart (9 charts)

- **Version:** 0.1.0
- **Source:** `/tmp/quickpat-zpoz2owp/helm`

## Architecture

This quickstart provides the following capabilities:

- **LLM Serving** - Model inference endpoint (e.g. vLLM, llama-stack)
- **Vector Database** - Stores document embeddings for similarity search
- **Object Storage** - S3-compatible storage for raw documents and artifacts

> **Note:** This quickstart requires GPU resources.

## Required OpenShift Operators

The following operators are automatically installed by the Validated Pattern:

| Operator | Subscription | Channel | Source |
|----------|-------------|---------|--------|
| Node Feature Discovery | nfd | stable | redhat-operators |
| NVIDIA GPU Operator | gpu-operator-certified | v24.9 | certified-operators |
| Red Hat OpenShift AI | rhods-operator | fast | redhat-operators |
| OpenShift Pipelines | openshift-pipelines-operator-rh | latest | redhat-operators |
| OpenShift Serverless | serverless-operator | stable | redhat-operators |
| OpenShift Service Mesh | servicemeshoperator | stable | redhat-operators |

## Secrets Configuration

The following secrets were detected and should be configured before deployment:

| Secret | Values Path | Action |
|--------|-------------|--------|
| `apiKey` | `copilot-backend.llm.apiKey` | Set via Vault or values |
| `apiKey` | `copilot-llama-stack.model.apiKey` | Set via Vault or values |
| `password` | `minio.minio.password` | Set via Vault or values |
| `password` | `pg-airman-mcp.postgres.password` | Set via Vault or values |
| `password` | `pgadmin.pgadmin.password` | Set via Vault or values |
| `password` | `pgadmin.postgres.password` | Set via Vault or values |
| `password` | `pgvector.postgres.password` | Set via Vault or values |
| `readonlyPassword` | `pgvector.postgres.readonlyPassword` | Set via Vault or values |

## Framework Architecture

This pattern uses the **multisource configuration** approach. Infrastructure Helm charts (clustergroup, vault, external-secrets) are pulled dynamically from the upstream Validated Patterns registry rather than stored locally. This means:

- No fork of multicloud-gitops required
- Upstream bug fixes are received by bumping `clusterGroupChartVersion`
- No `common/` git subtree needed (modern patterns use Ansible collections in the utility container)

The `pattern.sh` script runs all make targets inside a podman-based utility container (`quay.io/validatedpatterns/utility-container`) which includes the `rhvp.cluster_utils` Ansible collection and all required tooling.

> **Note:** The multisource feature is not yet documented on validatedpatterns.io but is used by all current production patterns (multicloud-gitops, rag-llm-gitops) and documented in the [common repo README](https://github.com/validatedpatterns/common).

## Pattern Configuration

- **Pattern name:** quickpat-zpoz2owp
- **Application name:** quickpat-zpoz2owp
- **Namespace:** quickpat-zpoz2owp
- **Chart strategy:** remote
- **Vault enabled:** True

## Deployment

```bash
git init && git add -A && git commit -m "Initial pattern"
oc login <cluster>
./pattern.sh make install
```
