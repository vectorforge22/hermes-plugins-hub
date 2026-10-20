# Hermes Agent Desktop Plugins

An index of in-house plugins for [Hermes Agent Desktop](https://hermesagent.com/) created by the [VectorForge22](https://github.com/vectorforge22) Team. 

Use this page to discover available plugins and find their documentation or source.

## Plugin Index

| Plugin | Description | Version | Status |
| --- | --- | --- | --- |
| *[Prompt Queue](https://github.com/vectorforge22/prompt-queue)* | *Kanban-style prompt queue for the Hermes desktop app. Each card is a prompt with its own target mode (new session, existing session, project, or a profile's Bot Chat). Press ▶ Play and the queue drains strictly top-down — gated on the global model slot, background self-improvement review completion, and context compaction. Also includes markdown-folder ingest and a trust-aware `::enqueue` directive (ask-first by default).* | *1.4.4* | *Available & in active development* |
| *[Background Review & Completion Watch](https://github.com/vectorforge22/background-review-watch)* | *Makes the background self-improvement review and batch context compaction visible: status-bar chips for review running/done/stale with live elapsed time, a turn-countdown fill bar to the next nudge, an always-visible compaction chip (compacting/done/failed/stale with committed reduction or failure class), reply-guard / review-overlap diagnostics, and a settings page that tunes the orphan-detection ceilings.* | *0.5.0* | *Catalog entry in review ([PR #141983](https://github.com/NousResearch/hermes-agent/pull/141983))* |
| *[Tool Activity](https://github.com/vectorforge22/tool-activity)* | *Live, expandable "what is the model doing right now" chip in the desktop status bar for the focused session: current tool + target with a parallel-call count, and a panel showing in-flight elapsed timers plus the last 12 completed calls with durations and error marks.* | *0.1.0* | *Available (local install; not yet submitted to the catalog)* |

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
