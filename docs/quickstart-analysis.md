# vllm-cpu

A quickstart for TinyLlama and AnythingLLM

- **Version:** 1.0.0
- **Source:** `/tmp/quickpat-xs3w1nae/helm`

## Architecture

This quickstart provides the following capabilities:

- **LLM Serving** - Model inference endpoint (e.g. vLLM, llama-stack)
- **Vector Database** - Stores document embeddings for similarity search

## Required OpenShift Operators

The following operators are automatically installed by the Validated Pattern:

| Operator | Subscription | Channel | Source |
|----------|-------------|---------|--------|
| cert-manager Operator for Red Hat OpenShift | openshift-cert-manager-operator | stable | redhat-operators |
| Red Hat OpenShift AI | rhods-operator | fast | redhat-operators |
| OpenShift Pipelines | openshift-pipelines-operator-rh | latest | redhat-operators |
| OpenShift Serverless | serverless-operator | stable | redhat-operators |
| OpenShift Service Mesh | servicemeshoperator | stable | redhat-operators |

## Secrets Configuration

The following secrets were detected and should be configured before deployment:

| Secret | Values Path | Action |
|--------|-------------|--------|
| `maxOutputTokens` | `vllm-cpu.model.maxOutputTokens` | Set via Vault or values |

## Framework Architecture

This pattern uses the **multisource configuration** approach. Infrastructure Helm charts (clustergroup, vault, external-secrets) are pulled dynamically from the upstream Validated Patterns registry rather than stored locally. This means:

- No fork of multicloud-gitops required
- Upstream bug fixes are received by bumping `clusterGroupChartVersion`
- No `common/` git subtree needed (modern patterns use Ansible collections in the utility container)

The `pattern.sh` script runs all make targets inside a podman-based utility container (`quay.io/validatedpatterns/utility-container`) which includes the `rhvp.cluster_utils` Ansible collection and all required tooling.

> **Note:** The multisource feature is not yet documented on validatedpatterns.io but is used by all current production patterns (multicloud-gitops, rag-llm-gitops) and documented in the [common repo README](https://github.com/validatedpatterns/common).

## Pattern Configuration

- **Pattern name:** vllm-cpu
- **Application name:** vllm-cpu
- **Namespace:** vllm-cpu
- **Chart strategy:** remote
- **Vault enabled:** True

## Deployment

```bash
git init && git add -A && git commit -m "Initial pattern"
oc login <cluster>
./pattern.sh make install
```
