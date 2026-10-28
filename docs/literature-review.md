# Literature review

This file catalogs sources relevant to the design and evaluation of a **model-agnostic agentic research system**. Entries separate source claims from implementation ideas and questions requiring validation.

## 1. Alpha generation, part 1: Self-editing heartbeats with seeds

- **Author:** Soham Bafana
- **Source:** [Original Google document](https://docs.google.com/document/d/14qXSLPBZENOTmYJMJPQ7xFRtMzm00qCF9foTKqque70/mobilebasic)
- **Domain:** Agentic discovery; continuous autonomous research; technology and information scouting
- **Reviewed:** 2026-10-28

### Summary

The article describes a long-running information-discovery workflow rather than a one-shot deep-research report. An agent starts with carefully selected **seeds**—examples of the kinds of valuable, often obscure sources it should find—and runs short, repeated **heartbeats**. Each iteration follows a few promising leads, records discoveries, and **rewrites a compact scratchpad** containing its current understanding, priorities, and next steps. The next iteration resumes from that durable state, allowing discoveries to redirect the investigation.

The intended outcome is to uncover high-value, niche information (“rare tokens”) that conventional broad searches might overlook. The author reports substantial collections of sources and research artifacts across several domains; these are illustrative case studies, **not controlled quality evaluations**.

### Implications for our implementation

1. **Externalize research state:** Persist leads, hypotheses, completed actions, source provenance, and next-step priorities separately from any model's conversation history.
2. **Support exemplar seeding:** Accept user-curated links or documents as relevance examples, not just a natural-language research question.
3. **Use iterative replanning:** Let new evidence reprioritize and branch the search; balance exploiting strong leads against exploring unfamiliar areas.
4. **Decouple the agent from the model:** Expose research, retrieval, scheduling, storage, and checkpointing through provider-neutral interfaces usable by local and hosted models.
5. **Budget and validate:** Make cadence adaptive rather than necessarily one-minute; constrain spending, deduplicate findings, validate citations, and allow explicit stopping criteria.

### Evidence limitations / questions to test

The case studies report output volume, but do not establish novelty, accuracy, relevance, or cost-effectiveness relative to a conventional deep-research baseline. We should evaluate **useful novel findings per unit cost**, source quality, duplication, long-run drift, resilience when swapping models, and the value of adaptive versus fixed scheduling.

**Potential experiment:** Run identical seeded research topics with (a) conventional one-shot research, (b) fixed-query repeated search, and (c) self-editing heartbeat research, then blind-rate the evidence-backed useful discoveries at equal inference and tool budgets.
