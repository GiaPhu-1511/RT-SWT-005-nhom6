# Gap Statement — LLM-based REST API Test Generation and Testing

Evidence table: N = 14 papers

---

## Identified Gaps

### GAP-T (Technology)
* **The Stateful & Interdependent Endpoint Problem:** Most existing tools test REST API endpoints in isolation (stateless testing). Real-world applications require ordered transaction sequences (e.g., `POST /login` -> `POST /cart` -> `GET /checkout`). Current LLM techniques lack robust long-context state tracking to navigate multi-endpoint dependency graphs smoothly.
* **High Financial Cost and Pipeline Latency:** The highest testing accuracies are heavily dependent on proprietary commercial models (GPT-4o, Claude 3). Running autonomous Multi-Agent refinement loops inside continuous integration (CI/CD) pipelines generates unsustainable token costs and introduces severe execution latency bottlenecks.

**Evidence:**
* Current LLM frameworks focus primarily on stateless generation, showing low success rates when dealing with business logic requiring complex parameter sequencing and dynamic state dependencies.
* Multi-agent execution setups show significant delays and high API token billing when scaling to large OpenAPI specifications within continuous integration setups.

---

### GAP-M (Metric)
* **Lack of Cost-Latency-Performance Trade-off Metrics:** Existing validation frameworks focus almost exclusively on standard software testing metrics (e.g., code coverage, bug detection rates) without evaluating the operational viability of the underlying LLMs. There is a lack of unified metrics to benchmark test accuracy against token expenditure and pipeline execution time.

**Evidence:**
* The synthesized primary studies evaluate LLM performance through traditional coverage lenses, leaving a structural gap in evaluating the economic and temporal cost-efficiency of these AI agents.

---

### GAP-D (Dataset)
* **Data Privacy vs. Cloud Leakage:** Enterprise systems contain private, sensitive OpenAPI specifications and staging payloads. There is a strict shortage of research optimizing localized, on-premise Small Language Models (SLMs, 7B/14B) specifically fine-tuned to process software test data without cloud communication.

**Evidence:**
* The majority of benchmarked datasets rely on open-source public APIs, with minimal representation of highly secured, enterprise-grade, on-premise setups optimized for low-parameter SLMs.

---

## Synthesized Gap Statement

While LLM-driven approaches have made significant progress in automating REST API testing, a deep divide remains between theoretical framework capabilities and practical enterprise integration. Current methodologies fail to adequately address the **Stateful & Interdependent Endpoint Problem (GAP-T)**, which severely limits automated testing of real-world, complex business logic. Furthermore, this technical bottleneck is compounded by operational and economic constraints: top-tier performance remains gated behind expensive, high-latency commercial LLMs, creating a clear **Cost-Latency trade-off (GAP-M)**. Meanwhile, attempts to migrate these pipelines to local environments to avoid **Cloud Data Leakage (GAP-D)** are stalled by a distinct lack of open benchmarks and fine-tuning datasets tailored for specialized, enterprise-grade Small Language Models (SLMs). 

Consequently, future research must bridge these gaps by shifting focus toward resource-efficient, state-aware Multi-Agent architectures and on-premise SLM fine-tuning that guarantee data privacy without sacrificing test coverage or exploding operational CI/CD pipeline costs.