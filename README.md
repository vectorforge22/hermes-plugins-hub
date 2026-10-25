# Hermes Agent Desktop Plugins

An index of in-house plugins for [Hermes Agent Desktop](https://hermesagent.com/) created by the [ARDR Systems](https://github.com/vectorforge22) Team. 

Use this page to discover available plugins and find their documentation or source.

## Plugin Index

| Plugin | What it does | Current | First catalog merge | Latest catalog merge |
| --- | --- | --- | --- | --- |
| [Prompt Queue](https://github.com/vectorforge22/prompt-queue) | Kanban-style prompt queue: per-card target modes (new/existing session, project, profile Bot Chat), strictly top-down drain gated on model slot / review / compaction, `::enqueue`. | 1.4.4 | v1.1.1 · 2026-10-05 | v1.4.4 · 2026-10-18 ([#140536](https://github.com/NousResearch/hermes-agent/pull/140536)) |
| [Background Review & Completion Watch](https://github.com/vectorforge22/background-review-watch) | Status-bar chips for the background self-improvement review and batch context compaction, nudge-countdown fill bar, reply-guard diagnostics, settings page. | 0.5.0 | v0.5.0 · 2026-10-20 | v0.5.0 · 2026-10-20 ([#141983](https://github.com/NousResearch/hermes-agent/pull/141983)) |
| [Tool Activity](https://github.com/vectorforge22/tool-activity) | Live "what is the model doing right now" chip for the focused session: in-flight tool calls with timers plus the last 12 completed. | 0.1.0 | — | — (not yet submitted) |

## Catalog history

One row per merge into the [Nous plugin catalog](https://github.com/NousResearch/hermes-agent/tree/main/plugin-catalog), recording the as-merged version and exact-SHA pin. Maintenance rule: add a row only when a catalog entry merges — local releases live in each plugin's CHANGELOG, not here.

### Prompt Queue

| Merged | Version | Pin | PR | Notes |
| --- | --- | --- | --- | --- |
| 2026-10-05 | 1.1.1 | da41ee7 | [#131983](https://github.com/NousResearch/hermes-agent/pull/131983) | First entry — submitted as v1.1.0 @ 4851cd1, bumped to 1.1.1 at merge with disclosure cleanup (`e1a2e08`). |
| 2026-10-18 | 1.4.4 | 04314c0 | [#140536](https://github.com/NousResearch/hermes-agent/pull/140536) | Per-card target modes, compaction gate, markdown ingest; maintainer disclosure follow-up `f733c91` same day. |

### Background Review & Completion Watch

| Merged | Version | Pin | PR | Notes |
| --- | --- | --- | --- | --- |
| 2026-10-20 | 0.5.0 | 75c6f45 | [#141983](https://github.com/NousResearch/hermes-agent/pull/141983) | First entry, merged unchanged (commit `78f4dfe`). Renamed from `bg-review-watch` pre-publication; v0.6.0 (per-session chips) is next. |

### Tool Activity

Not yet submitted to the catalog (local install only).

## Disclaimer

These plugins are independently developed in-house projects. They are not official Hermes Agent Desktop plugins and are not affiliated with, endorsed by, or supported by Nous Research. They are provided as-is, without guarantees of availability, compatibility, or fitness for a particular purpose. Review each plugin's source and permissions before installing it, and keep backups of important data. You are responsible for any model-provider charges, subscription usage, and data you send through Hermes Agent Desktop or its plugins. Always follow the terms and policies of your chosen model provider.

## Effects on Hermes Agent Performance

Plugins do not inherently make a model generate tokens faster. Their effect depends on what they do, how often they run, and the workload. UI-only plugins generally add small desktop-side work; plugins that poll, process large amounts of data, make network requests, or add instructions and history can add overhead or increase response time and context usage.

| Model setup | What mainly affects perceived performance | Plugin considerations |
| --- | --- | --- |
| **Local model** | Your computer's CPU/GPU, available memory, model size, and local runtime determine generation speed. | Plugin processing competes for the same desktop resources. Local queues and background tasks can also keep the machine busy. |
| **Frontier lab API** | Provider-side model speed, service load, network latency, and API limits influence response time and throughput. | Desktop UI work still uses local resources. Plugins that add context or make extra requests can increase latency, token usage, and possibly API costs. |
| **Nous Research API subscription** | Performance depends on the selected model, service load, network path, and the subscription's current usage limits and policies. | The same plugin overhead applies: added context or requests may affect latency and usage. Subscription terms and limits are set by the provider and may change. |

For example, **Prompt Queue** runs queued prompts sequentially and waits for the turn and background review to finish before starting the next item. This reduces unattended throughput by design; it does not make an individual model response slower. **Background Review & Completion Watch** and **Tool Activity** primarily surface status in the desktop UI, though their actual resource use depends on their implementation and workload. These are general expectations, not benchmark results; measure with your own models, providers, and sessions for a reliable comparison.
