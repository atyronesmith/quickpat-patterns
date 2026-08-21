# quickpat-f5wx3hvs

Multi-chart quickstart (3 charts)

- **Version:** 0.1.0
- **Source:** `/tmp/quickpat-f5wx3hvs/helm`

## Architecture

This quickstart provides the following capabilities:

- **Vector Database** - Stores document embeddings for similarity search
- **Object Storage** - S3-compatible storage for raw documents and artifacts

## Helm Dependencies

| Chart | Version | Repository |
|-------|---------|------------|
| pgvector | 0.1.0 | https://rh-ai-quickstart.github.io/ai-architecture-charts |

## Required OpenShift Operators

The following operators are automatically installed by the Validated Pattern:

| Operator | Subscription | Channel | Source |
|----------|-------------|---------|--------|
| AMQ Streams (Kafka) | amq-streams | stable | redhat-operators |
| OpenShift Pipelines | openshift-pipelines-operator-rh | latest | redhat-operators |

## Secrets Configuration

The following secrets were detected and should be configured before deployment:

| Secret | Values Path | Action |
|--------|-------------|--------|
| `password` | `minio.minio.password` | Set via Vault or values |
| `imagePullSecrets` | `product-recommender-system.imagePullSecrets` | Set via Vault or values |
| `LLM_API_KEY` | `product-recommender-system.llm.secret.data.LLM_API_KEY` | Set via Vault or values |
| `SUMMARY_LLM_API_KEY` | `product-recommender-system.llm.secret.data.SUMMARY_LLM_API_KEY` | Set via Vault or values |
| `secret` | `product-recommender-system.feast.secret` | Set via Vault or values |

## Framework Architecture

This pattern uses the **multisource configuration** approach. Infrastructure Helm charts (clustergroup, vault, external-secrets) are pulled dynamically from the upstream Validated Patterns registry rather than stored locally. This means:

- No fork of multicloud-gitops required
- Upstream bug fixes are received by bumping `clusterGroupChartVersion`
- No `common/` git subtree needed (modern patterns use Ansible collections in the utility container)

The `pattern.sh` script runs all make targets inside a podman-based utility container (`quay.io/validatedpatterns/utility-container`) which includes the `rhvp.cluster_utils` Ansible collection and all required tooling.

> **Note:** The multisource feature is not yet documented on validatedpatterns.io but is used by all current production patterns (multicloud-gitops, rag-llm-gitops) and documented in the [common repo README](https://github.com/validatedpatterns/common).

## Pattern Configuration

- **Pattern name:** quickpat-f5wx3hvs
- **Application name:** quickpat-f5wx3hvs
- **Namespace:** quickpat-f5wx3hvs
- **Chart strategy:** remote
- **Vault enabled:** True

## Deployment

```bash
git init && git add -A && git commit -m "Initial pattern"
oc login <cluster>
./pattern.sh make install
```
