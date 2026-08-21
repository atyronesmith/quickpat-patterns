# quickpat-3b99g3f3

Multi-chart quickstart (4 charts)

- **Version:** 0.1.0
- **Source:** `/tmp/quickpat-3b99g3f3/charts`

## Architecture

This quickstart provides the following capabilities:

- **LLM Serving** - Model inference endpoint (e.g. vLLM, llama-stack)

> **Note:** This quickstart requires GPU resources.

## Helm Dependencies

| Chart | Version | Repository |
|-------|---------|------------|
| install-operators | * | local |
| keycloak | * | local |

## Required OpenShift Operators

The following operators are automatically installed by the Validated Pattern:

| Operator | Subscription | Channel | Source |
|----------|-------------|---------|--------|
| cert-manager Operator for Red Hat OpenShift | openshift-cert-manager-operator | stable | redhat-operators |
| Node Feature Discovery | nfd | stable | redhat-operators |
| NVIDIA GPU Operator | gpu-operator-certified | v24.9 | certified-operators |
| Red Hat OpenShift AI | rhods-operator | fast | redhat-operators |
| Red Hat Build of Keycloak | rhbk-operator | stable-v26 | redhat-operators |
| OpenShift Serverless | serverless-operator | stable | redhat-operators |
| OpenShift Service Mesh | servicemeshoperator | stable | redhat-operators |

## Secrets Configuration

The following secrets were detected and should be configured before deployment:

| Secret | Values Path | Action |
|--------|-------------|--------|
| `keycloak` | `maas-code-assistant.keycloak` | Set via Vault or values |
| `openshiftClientSecret` | `keycloak.realm.openshiftClientSecret` | Set via Vault or values |
| `password` | `keycloak.realm.admin.password` | Set via Vault or values |
| `password` | `keycloak.realm.user.password` | Set via Vault or values |
| `credentialsSecret` | `keycloak.postgresCluster.credentialsSecret` | Set via Vault or values |

## Framework Architecture

This pattern uses the **multisource configuration** approach. Infrastructure Helm charts (clustergroup, vault, external-secrets) are pulled dynamically from the upstream Validated Patterns registry rather than stored locally. This means:

- No fork of multicloud-gitops required
- Upstream bug fixes are received by bumping `clusterGroupChartVersion`
- No `common/` git subtree needed (modern patterns use Ansible collections in the utility container)

The `pattern.sh` script runs all make targets inside a podman-based utility container (`quay.io/validatedpatterns/utility-container`) which includes the `rhvp.cluster_utils` Ansible collection and all required tooling.

> **Note:** The multisource feature is not yet documented on validatedpatterns.io but is used by all current production patterns (multicloud-gitops, rag-llm-gitops) and documented in the [common repo README](https://github.com/validatedpatterns/common).

## Pattern Configuration

- **Pattern name:** quickpat-3b99g3f3
- **Application name:** quickpat-3b99g3f3
- **Namespace:** quickpat-3b99g3f3
- **Chart strategy:** remote
- **Vault enabled:** True

## Deployment

```bash
git init && git add -A && git commit -m "Initial pattern"
oc login <cluster>
./pattern.sh make install
```
