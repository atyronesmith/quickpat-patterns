# QuickPat Generated Patterns

Validated Patterns generated from Red Hat AI Quickstarts by [QuickPat](https://github.com/atyronesmith/quickpat).

Each branch contains a complete [Validated Pattern](https://validatedpatterns.io/) ready for deployment with the VP framework.

## Branches

| Branch | Quickstart |
|--------|------------|
| [RAG](../../tree/RAG) | Retrieval-Augmented Generation |
| [maas-code-assistant](../../tree/maas-code-assistant) | Model-as-a-Service Code Assistant |
| [product-recommender](../../tree/product-recommender) | Product Recommender |
| [lemonade-stand](../../tree/lemonade-stand) | Lemonade Stand |
| [llm-cpu-serving](../../tree/llm-cpu-serving) | LLM CPU Serving |
| [data-governance](../../tree/data-governance) | Data Governance |

## Usage

Clone a specific pattern branch:

```bash
git clone -b RAG https://github.com/atyronesmith/quickpat-patterns.git rag-pattern
```

Then follow the standard [Validated Patterns deployment](https://validatedpatterns.io/learn/quickstart/) process.

## How It Works

These patterns are automatically generated and published by CI whenever the QuickPat source is updated. Each push to `main` on the QuickPat repo triggers a workflow that:

1. Generates a Validated Pattern from each AI Quickstart
2. Validates the output (schema checks, helm lint, kubeconform)
3. Publishes each pattern to its branch in this repo

## License

Apache License 2.0. See [LICENSE](LICENSE) for details.
