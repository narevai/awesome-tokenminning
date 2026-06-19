# Awesome Token Mining [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Curated projects, tools, and techniques for **mining more value from every AI token** — self-hosting, compression, caching, routing, and observability.

The goal is simple: do the same work with fewer tokens, cheaper models, or your own hardware. This list collects the best open-source and practical resources for cutting LLM bills without cutting capability.

## Contents

- [Self-Hosting](#self-hosting)
- [vLLM & High-Throughput Inference](#vllm--high-throughput-inference)
- [Token Compression](#token-compression)
- [Semantic & Response Caching](#semantic--response-caching)
- [Gateways & Model Routing](#gateways--model-routing)
- [Observability & Cost Tracking](#observability--cost-tracking)
- [Context & Prompt Optimization](#context--prompt-optimization)
- [Related Lists](#related-lists)
- [Contributing](#contributing)

---

## Self-Hosting

Run models on your own hardware or rented GPUs. At scale, self-hosting often beats per-token API pricing by 60–90%.

- [Ollama](https://github.com/ollama/ollama) - One-command local model runner. Best for prototyping, single-user workflows, and edge deployments on consumer hardware.
- [LocalAI](https://github.com/mudler/LocalAI) - OpenAI-compatible API server that runs on CPU, GPU, or Apple Silicon. Broad model and backend support without cloud lock-in.
- [llama.cpp](https://github.com/ggerganov/llama.cpp) - Efficient C/C++ inference for LLaMA-family models. The foundation many local runners build on; excellent for CPU and quantized models.
- [text-generation-webui](https://github.com/oobabooga/text-generation-webui) - Gradio UI for running and experimenting with local models. Great for evaluating models before committing to production serving.
- [Open WebUI](https://github.com/open-webui/open-webui) - Self-hosted ChatGPT-style interface that talks to Ollama, OpenAI, and other backends from a single UI.
- [Tabby](https://github.com/TabbyML/tabby) - Self-hosted AI coding assistant. Replace Copilot-style subscriptions with a model you control.
- [Jan](https://github.com/janhq/jan) - Desktop app for running models locally with an offline-first workflow.

## vLLM & High-Throughput Inference

Production-grade serving stacks that squeeze more tokens per GPU dollar through PagedAttention, continuous batching, and OpenAI-compatible APIs.

- [vLLM](https://github.com/vllm-project/vllm) - Industry-standard high-throughput inference engine. Up to 10–20× better concurrency than naive serving on the same hardware.
- [SGLang](https://github.com/sgl-project/sglang) - Fast structured generation and serving runtime with RadixAttention for prefix caching across requests.
- [TensorRT-LLM](https://github.com/NVIDIA/TensorRT-LLM) - NVIDIA's optimized inference library. Maximum throughput on datacenter GPUs when you need every FLOP.
- [TGI (Text Generation Inference)](https://github.com/huggingface/text-generation-inference) - Hugging Face's production server with continuous batching, quantization, and tensor parallelism.
- [LMDeploy](https://github.com/InternLM/lmdeploy) - Efficient deployment toolkit from OpenMMLab with TurboMind backend for high-throughput serving.
- [Aphrodite Engine](https://github.com/aphrodite-engine/aphrodite-engine) - vLLM-compatible inference engine with additional optimizations for open models.

## Token Compression

Shrink prompts and outputs before they hit the bill. These tools target the tokens you never needed in the first place.

- [Caveman](https://github.com/JuliusBrussee/caveman) - Agent skill that cuts ~65% of output tokens by dropping filler while preserving technical accuracy. Also compresses CLAUDE.md and memory files for compound input savings.
- [caveman-code](https://getcaveman.dev/) - Standalone CLI that stacks input, tool-call, dedup, and output compression layers for agent workloads.
- [LLMLingua](https://github.com/microsoft/LLMLingua) - Microsoft Research prompt compressor. Up to 20× compression on long contexts with ~1.5% accuracy loss on benchmarks.
- [LongLLMLingua](https://github.com/microsoft/LLMLingua) - Long-context variant that mitigates "lost in the middle" while compressing RAG prompts to a fraction of their size.
- [LLMLingua-2](https://github.com/microsoft/LLMLingua) - Faster, task-agnostic prompt compression using a distilled model for near-real-time use.

## Semantic & Response Caching

Skip the LLM entirely when a similar question was already answered, or reuse provider-side prefix caches.

- [GPTCache](https://github.com/zilliztech/GPTCache) - Semantic cache for LLM apps. Vector similarity matching returns cached responses for equivalent queries — up to 10× cost reduction on hit.
- [LiteLLM](https://github.com/BerriAI/litellm) - Universal LLM gateway with in-memory, Redis, S3, and semantic caching backends. One integration for caching across providers.
- [RedisVL](https://github.com/redis/redis-vl) - Redis vector library for building semantic caches with sub-millisecond lookups at scale.
- [ModelCache](https://github.com/shibing624/ModelCache) - Multi-level semantic cache with embedding similarity and TTL management for production LLM apps.
- [OpenAI Prompt Caching Cookbook](https://github.com/openai/openai-cookbook/blob/main/examples/Prompt_Caching_201.ipynb) - Practical guide to structuring prompts for up to 90% off cached input tokens on OpenAI models.

## Gateways & Model Routing

Route easy tasks to cheap models and hard tasks to capable ones. Enforce budgets before spend happens.

- [LiteLLM Proxy](https://github.com/BerriAI/litellm) - Production proxy with budget limits, rate limiting, load balancing, and fallback chains across 100+ models.
- [RouteLLM](https://github.com/lm-sys/RouteLLM) - ML-based router that sends queries to strong or weak models based on difficulty. Up to 85% cost reduction with minimal quality loss.
- [OpenRouter](https://openrouter.ai/) - Unified API across providers with automatic routing to cheapest available model for a given capability tier.
- [Portkey](https://github.com/Portkey-AI/gateway) - AI gateway with caching, retries, load balancing, and observability hooks for multi-provider setups.
- [Martian](https://github.com/withmartian/martian) - Model router that picks the cheapest model that can handle each request.

## Observability & Cost Tracking

You can't optimize what you can't measure. These tools attribute token spend to users, features, and prompts.

- [Langfuse](https://github.com/langfuse/langfuse) - Open-source LLM engineering platform with tracing, prompt management, and cost analytics per request.
- [Helicone](https://github.com/Helicone/helicone) - LLM observability proxy that logs every request with latency, cost, and cache hit metrics.
- [OpenLIT](https://github.com/openlit/openlit) - OpenTelemetry-native observability for LLM apps with token and cost dashboards.
- [Lunary](https://github.com/lunary-ai/lunary) - LLM product analytics with cost tracking, prompt versioning, and user-level attribution.
- [Narev](https://github.com/narev-ai/narev) - AI billing and cost attribution SDK. Pin live pricing, calculate per-request COGS, and wire usage-based billing.

## Context & Prompt Optimization

Engineering patterns and libraries that reduce context bloat without adding new infrastructure.

- [tiktoken](https://github.com/openai/tiktoken) - Fast BPE tokenizer. Count tokens before you send them and catch bloated prompts at build time.
- [Anthropic Prompt Caching Docs](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching) - Official guide to `cache_control` breakpoints for up to 90% off repeated input prefixes.
- [RAGAS](https://github.com/explodinggradients/ragas) - Evaluate RAG pipelines to find when you're over-retrieving context and paying for irrelevant chunks.
- [LlamaIndex Response Synthesizers](https://docs.llamaindex.ai/en/stable/module_guides/querying/response_synthesizers/) - Configurable summarization and refinement modes that trade context size for answer quality.
- [Cursor Rules / AGENTS.md patterns](https://github.com/PatrickJS/awesome-cursorrules) - Keep agent context files lean. Smaller system prompts mean smaller bills on every turn.

## Related Lists

- [awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps) - Curated collection of LLM applications and use cases.
- [awesome-local-llm](https://github.com/rafska/awesome-local-llm) - Resources for running LLMs locally.
- [awesome-ai-tools](https://github.com/mahseema/awesome-ai-tools) - Broader AI tooling landscape.

## Contributing

Contributions welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a PR.

**Quick rules:**

- Add projects that concretely reduce token spend, inference cost, or API bills.
- Prefer open-source or freely usable tools with active maintenance.
- One line per entry: what it does and why it saves money.
- No paid-only products without a meaningful free tier unless they're industry-standard references (e.g. cloud GPU providers).

## License

[![CC0](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, contributors waive all copyright and related rights to this list.
