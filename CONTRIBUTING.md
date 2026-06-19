# Contributing to Awesome Token Mining

Thanks for helping curate the best resources for saving on AI tokens!

## What belongs here

Add projects that help people:

- **Spend fewer tokens** — compression, context pruning, concise output tooling
- **Pay less per token** — self-hosting, quantization, efficient inference engines
- **Skip tokens entirely** — semantic caching, prompt caching, response reuse
- **Route smarter** — sending easy work to cheap models, hard work to capable ones
- **See the bill** — observability, attribution, and cost tracking

## What does not belong here

- General AI news or hype with no clear cost-saving angle
- Chat UIs, local runners, or agent apps whose only hook is "self-hosted" — if Ollama, llama.cpp, or LocalAI already cover the cost story, skip the wrapper
- Broad LLM platforms (tracing, evals, prompt management) where cost tracking is a side feature, not the product
- Generic RAG, agent, or evaluation frameworks without a direct token-reduction or cost-measurement story
- Abandoned projects with no commits in 12+ months (unless historically significant)
- Pure model repos with no inference or cost story (link to model hubs instead)
- Affiliate links or paid placement

## How to add an entry

1. Pick the right category. Create a new `##` section only if nothing fits.
2. Add your entry in **alphabetical order** within that category.
3. Use this format:

   ```markdown
   - [Project Name](https://github.com/org/repo) - One sentence: what it does and how it saves tokens or money.
   ```

4. Keep descriptions factual. Cite measurable claims when you can (e.g. "up to 20× compression" from the project's own benchmarks).
5. Open a PR with a clear title like `Add LiteLLM to Gateways section`.

## Pull request checklist

- [ ] Link works and points to the canonical source (usually GitHub or official docs)
- [ ] Entry is in alphabetical order within its section
- [ ] Description is one line and explains the cost-saving value
- [ ] No duplicate entries (search the README first)

## Suggesting a new category

Open an issue first if you want to add a major new section (e.g. "Quantization Tools" or "GPU Cloud Marketplaces"). Describe why existing categories don't fit and list at least 3 candidate projects.
