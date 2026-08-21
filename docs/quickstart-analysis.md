# lemonade-stand-assistant

A Helm chart for Lemonade Stand Assistant Application

- **Version:** 1.0.0
- **Source:** `/tmp/quickpat-1vtr16sx/chart`

## Architecture

This quickstart provides the following capabilities:

- **LLM Serving** - Model inference endpoint (e.g. vLLM, llama-stack)
- **Object Storage** - S3-compatible storage for raw documents and artifacts

> **Note:** This quickstart requires GPU resources.

## Required OpenShift Operators

The following operators are automatically installed by the Validated Pattern:

| Operator | Subscription | Channel | Source |
|----------|-------------|---------|--------|
| Node Feature Discovery | nfd | stable | redhat-operators |
| NVIDIA GPU Operator | gpu-operator-certified | v24.9 | certified-operators |
| Red Hat OpenShift AI | rhods-operator | fast | redhat-operators |
| OpenShift Serverless | serverless-operator | stable | redhat-operators |
| OpenShift Service Mesh | servicemeshoperator | stable | redhat-operators |

## Framework Architecture

This pattern uses the **multisource configuration** approach. Infrastructure Helm charts (clustergroup, vault, external-secrets) are pulled dynamically from the upstream Validated Patterns registry rather than stored locally. This means:

- No fork of multicloud-gitops required
- Upstream bug fixes are received by bumping `clusterGroupChartVersion`
- No `common/` git subtree needed (modern patterns use Ansible collections in the utility container)

The `pattern.sh` script runs all make targets inside a podman-based utility container (`quay.io/validatedpatterns/utility-container`) which includes the `rhvp.cluster_utils` Ansible collection and all required tooling.

> **Note:** The multisource feature is not yet documented on validatedpatterns.io but is used by all current production patterns (multicloud-gitops, rag-llm-gitops) and documented in the [common repo README](https://github.com/validatedpatterns/common).

## Pattern Configuration

- **Pattern name:** lemonade-stand-assistant
- **Application name:** lemonade-stand-assistant
- **Namespace:** lemonade-stand-assistant
- **Chart strategy:** remote
- **Vault enabled:** True

## Deployment

```bash
git init && git add -A && git commit -m "Initial pattern"
oc login <cluster>
./pattern.sh make install
```
