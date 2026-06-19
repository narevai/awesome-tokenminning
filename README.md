<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/logo-dark.png">
    <img src="assets/logo.png" width="220" alt="Token mining elephant">
  </picture>
</p>

<h1 align="center">Awesome Token Mining</h1>

<p align="center">
  <em>The same work. Fewer tokens. Lower bill.</em>
</p>

<p align="center">
  <a href="https://awesome.re"><img src="https://awesome.re/badge.svg" alt="Awesome"></a>
  <img src="https://img.shields.io/github/stars/narevai/awesome-tokenminning?style=flat-square&color=111111&label=stars" alt="Stars">
  <img src="https://img.shields.io/badge/categories-10-111111?style=flat-square" alt="10 categories">
  <img src="https://img.shields.io/badge/tools-50%2B-111111?style=flat-square" alt="50+ tools">
  <img src="https://img.shields.io/badge/license-CC0-111111?style=flat-square" alt="CC0 license">
</p>

<p align="center">
  <strong>60–90% self-host savings &middot; 20&times; prompt compression &middot; 10&times; cache hits &middot; 85% smarter routing</strong><br>
  <sub>Curated open-source projects for cutting LLM bills without cutting capability — self-hosting, quantization, KV cache tricks, token compression, semantic caching, model routing, and cost observability. Every entry earns its place by concretely reducing token spend, inference cost, or API bills. <a href="#contributing">Contribute</a> &middot; <a href="CONTRIBUTING.md">guidelines</a>.</sub>
</p>

---

You know the bill. Tokens in, dollars out. You spin up another agent, another RAG pipeline, another 200K context window — and somewhere a GPU farm charges you rent.

The fix is not one trick. It is a stack: host your own weights, quantize them, compress the prompts, cache what repeats, route easy work to cheap models, and measure every cent before it compounds.

This list is the map.

## Self-Hosting

Run models on your own hardware or rented GPUs. At scale, self-hosting often beats per-token API pricing by 60–90%.

- [Exo](https://github.com/exo-explore/exo) - Clusters laptops and desktops into a distributed inference mesh. Splits models across devices so you can run 70B+ locally instead of paying per-token APIs.
- [llama.cpp](https://github.com/ggerganov/llama.cpp) - Efficient C/C++ inference for LLaMA-family models. The foundation many local runners build on; excellent for CPU and quantized models.
- [llamafile](https://github.com/mozilla-ai/llamafile) - Single-file executable models built on llama.cpp. Ship weights + runtime together with zero install — ideal for offline, zero-API-cost deployments.
- [LocalAI](https://github.com/mudler/LocalAI) - OpenAI-compatible API server that runs on CPU, GPU, or Apple Silicon. Broad model and backend support without cloud lock-in.
- [Ollama](https://github.com/ollama/ollama) - One-command local model runner. Best for prototyping, single-user workflows, and edge deployments on consumer hardware.
- [Tabby](https://github.com/TabbyML/tabby) - Self-hosted AI coding assistant. Replace Copilot-style subscriptions with a model you control.

## vLLM & High-Throughput Inference

Production-grade serving stacks that squeeze more tokens per GPU dollar through PagedAttention, continuous batching, and OpenAI-compatible APIs.

- [vLLM](https://github.com/vllm-project/vllm) - Industry-standard high-throughput inference engine. Up to 10–20× better concurrency than naive serving on the same hardware.
- [SGLang](https://github.com/sgl-project/sglang) - Fast structured generation and serving runtime with RadixAttention for prefix caching across requests.
- [TensorRT-LLM](https://github.com/NVIDIA/TensorRT-LLM) - NVIDIA's optimized inference library. Maximum throughput on datacenter GPUs when you need every FLOP.
- [TGI (Text Generation Inference)](https://github.com/huggingface/text-generation-inference) - Hugging Face's production server with continuous batching, quantization, and tensor parallelism.
- [LMDeploy](https://github.com/InternLM/lmdeploy) - Efficient deployment toolkit from OpenMMLab with TurboMind backend for high-throughput serving.
- [Aphrodite Engine](https://github.com/aphrodite-engine/aphrodite-engine) - vLLM-compatible inference engine with additional optimizations for open models.

## Quantization

Shrink model weights so the same GPU serves more tokens per dollar. Match the format to your runtime: GGUF for llama.cpp/Ollama, AWQ/GPTQ for vLLM/TGI.

- [AutoGPTQ](https://github.com/AutoGPTQ/AutoGPTQ) - Post-training 4-bit quantization with GPTQ. Cuts VRAM ~4× on NVIDIA GPUs while keeping perplexity within ~2% of FP16.
- [AWQ (llm-awq)](https://github.com/mit-han-lab/llm-awq) - Activation-aware INT3/4 quantization (MLSys 2024 best paper). Preserves salient weight channels for better accuracy at 4-bit on datacenter GPUs.
- [bitsandbytes](https://github.com/bitsandbytes-foundation/bitsandbytes) - 4-bit/8-bit loading in PyTorch for research and QLoRA fine-tuning. Lets you fit larger models on consumer GPUs without cloud APIs.

## KV Cache & Speculative Decoding

Attack the two biggest inference bottlenecks: KV cache memory on long contexts, and serial token generation. These squeeze more throughput from hardware you already own.

- [EAGLE](https://github.com/SafeAILab/EAGLE) - Speculative decoding via feature extrapolation. A small draft head proposes multiple tokens; the main model verifies in parallel for ~2–3× faster generation with provably identical output distribution.
- [kvpress](https://github.com/NVIDIA/kvpress) - NVIDIA's unified library of KV cache compression methods (SnapKV, H2O, Finch, and more). Drop-in Hugging Face pipeline for long-context workloads where cache size dominates memory.
- [Medusa](https://github.com/FasterDecoding/Medusa) - Adds lightweight prediction heads to a frozen base model to speculate multiple tokens per step. No separate draft model required.
- [SnapKV](https://github.com/FasterDecoding/SnapKV) - Fine-tuning-free KV cache compression. Observes attention patterns in a prompt window, keeps only clustered important positions per head — up to 8× memory savings on 16K+ contexts.

## Token Compression

Shrink prompts and outputs before they hit the bill. These tools target the tokens you never needed in the first place.

- [Claw Compactor](https://github.com/open-compress/claw-compactor) - 14-stage content-aware compression pipeline with AST-aware code folding, JSON sampling, and reversible storage. Zero LLM inference cost; 15–82% savings depending on content type.
- [Caveman](https://github.com/JuliusBrussee/caveman) - Agent skill that cuts ~65% of output tokens by dropping filler while preserving technical accuracy. Also compresses CLAUDE.md and memory files for compound input savings.
- [caveman-code](https://getcaveman.dev/) - Standalone CLI that stacks input, tool-call, dedup, and output compression layers for agent workloads.
- [LLMLingua](https://github.com/microsoft/LLMLingua) - Microsoft Research prompt compressor. Up to 20× compression on long contexts with ~1.5% accuracy loss on benchmarks.
- [LongLLMLingua](https://github.com/microsoft/LLMLingua) - Long-context variant that mitigates "lost in the middle" while compressing RAG prompts to a fraction of their size.
- [LLMLingua-2](https://github.com/microsoft/LLMLingua) - Faster, task-agnostic prompt compression using a distilled model for near-real-time use.
- [Ponytail](https://github.com/DietrichGebert/ponytail) - Agent skill that stops over-engineering via a YAGNI ladder: stdlib, native platform, and one-liners before custom code. Agentic benchmark: ~54% less code, ~22% fewer tokens, ~20% lower cost on real Claude Code sessions.
- [TokenForge](https://github.com/Manavarya09/tokenforge) - Full-stack Rust optimizer for code, CLI output, conversation history, JSON, and MCP schemas. AST-aware folding with lossless SQLite-backed reversibility.
- [Tokenless](https://github.com/TokenFleet-AI/tokenless) - Rust toolkit for schema compression, differential responses, TOON encoding, and command-output rewriting. Targets 60–90% savings on agent tool-call loops.

## Semantic & Response Caching

Skip the LLM entirely when a similar question was already answered, or reuse provider-side prefix caches.

- [GPTCache](https://github.com/zilliztech/GPTCache) - Semantic cache for LLM apps. Vector similarity matching returns cached responses for equivalent queries — up to 10× cost reduction on hit.
- [LiteLLM](https://github.com/BerriAI/litellm) - Universal LLM gateway with in-memory, Redis, S3, and semantic caching backends. One integration for caching across providers.
- [RedisVL](https://github.com/redis/redis-vl) - Redis vector library for building semantic caches with sub-millisecond lookups at scale.
- [ModelCache](https://github.com/shibing624/ModelCache) - Multi-level semantic cache with embedding similarity and TTL management for production LLM apps.
- [OpenAI Prompt Caching Cookbook](https://github.com/openai/openai-cookbook/blob/main/examples/Prompt_Caching_201.ipynb) - Practical guide to structuring prompts for up to 90% off cached input tokens on OpenAI models.

## Gateways & Model Routing

Route easy tasks to cheap models and hard tasks to capable ones. Enforce budgets before spend happens.

- [Conduit](https://github.com/ashita-ai/conduit) - ML-powered router using Thompson Sampling bandits. Learns which model handles each query type best, balancing cost, quality, and latency from live traffic.
- [LiteLLM Proxy](https://github.com/BerriAI/litellm) - Production proxy with budget limits, rate limiting, load balancing, and fallback chains across 100+ models.
- [LLMRouter](https://github.com/ulab-uiuc/llmrouter) - Research-grade routing library with 16+ strategies (KNN, MLP, Elo, graph-based, BERT routers). Unified CLI for training cost-aware routers on benchmark data.
- [Martian](https://github.com/withmartian/martian) - Model router that picks the cheapest model that can handle each request.
- [OpenRouter](https://openrouter.ai/) - Unified API across providers with automatic routing to cheapest available model for a given capability tier.
- [ParetoBandit](https://github.com/ParetoBandit/ParetoBandit) - Cost-aware contextual bandit router with online budget pacing. Adapts when model prices or quality shift — routing decisions in microseconds on CPU.
- [Portkey](https://github.com/Portkey-AI/gateway) - AI gateway with caching, retries, load balancing, and observability hooks for multi-provider setups.
- [RouteLLM](https://github.com/lm-sys/RouteLLM) - ML-based router that sends queries to strong or weak models based on difficulty. Up to 85% cost reduction with minimal quality loss.

## Observability & Cost Tracking

You can't optimize what you can't measure. These tools attribute token spend to users, features, and prompts.

- [CostPilot](https://github.com/aryanjp1/costpilot) - Self-hosted LLM cost dashboard with a 3-line Python SDK. Tracks spend, tokens, and latency per model/feature with forecasting and savings recommendations.
- [Helicone](https://github.com/Helicone/helicone) - LLM observability proxy that logs every request with latency, cost, and cache hit metrics.
- [llmwatch](https://github.com/DanMeon/llmwatch) - Lightweight SDK instrumentation for OpenAI, Anthropic, Google, and more. Tags costs by feature/user with bundled pricing for 1000+ models — no proxy required.
- [Narev](https://github.com/narev-ai/narev) - AI billing and cost attribution SDK. Pin live pricing, calculate per-request COGS, and wire usage-based billing.
- [Shekel](https://github.com/arieradle/shekel) - Budget enforcement and cost tracking for agentic systems. One-line Python integration with OpenTelemetry metrics, circuit breakers, and per-tool spend limits.

## Context & Prompt Optimization

Engineering patterns and libraries that reduce context bloat without adding new infrastructure.

- [Anthropic Prompt Caching Docs](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching) - Official guide to `cache_control` breakpoints for up to 90% off repeated input prefixes.
- [DSPy](https://github.com/stanfordnlp/dspy) - Declarative prompt optimization from Stanford NLP. Optimizers like MIPROv2 and BootstrapFewShot prune redundant instructions and pick efficient few-shot examples from your data.
- [Mem0](https://github.com/mem0ai/mem0) - Long-term memory layer for agents. Stores and retrieves only relevant facts instead of replaying full chat history — cuts recurring context tokens on every turn.
- [tiktoken](https://github.com/openai/tiktoken) - Fast BPE tokenizer. Count tokens before you send them and catch bloated prompts at build time.

## Related Lists

- [awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps) - Curated collection of LLM applications and use cases.
- [awesome-local-llm](https://github.com/rafska/awesome-local-llm) - Resources for running LLMs locally.
- [awesome-ai-tools](https://github.com/mahseema/awesome-ai-tools) - Broader AI tooling landscape.

## Contributing

Contributions welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a PR.

**Quick rules:**

- Add projects that concretely reduce token spend, inference cost, or API bills.
- Prefer open-source or freely usable tools with active maintenance.
- One line per entry: what it does and why it saves money.
- No paid-only products without a meaningful free tier unless they're industry-standard references (e.g. cloud GPU providers).

## License

[CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/). To the extent possible under law, contributors waive all copyright and related rights to this list.
