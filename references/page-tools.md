# Page-tool discovery

Page-tool support is planned. Discover what the current AccessFuel page
actually exposes; this skill does not supply a callable tool catalog.

## Host capabilities

Use the active host's documented page-tool bridge first. Read its capability
documentation before invoking it. If unavailable, use a documented evaluator
in the page's main world. Do not guess browser APIs, evaluation worlds, or
host-specific time limits. If neither works, report the limitation and use
an AIRA hand-off only if navigation and page reading are still available.

For Codex hosts exposing the documented CUA entry point, a visible tab can be
opened with `cua.createBrowserTab("iab", url, { visible: true })`. Other host
opening and evaluation calls depend on the capabilities available in that
session; do not assume every Claude Code, Cowork or Codex installation has them.

## Discover before calling

- A documented `window.__accessfuelWebMcp` helper may provide readiness,
  discovery and result retrieval. Its presence alone does not establish its
  methods or signatures. Use it only when those are documented by the page.
- Otherwise, where supported, `document.modelContext.getTools()` discovers
  descriptors and `document.modelContext.executeTool(tool, args)` calls a
  discovered descriptor. Use the documented input object; serialize it only
  if the actual host adapter requires that. Never probe a write to learn its
  argument format.
- Inspect actual AccessFuel tools, their origin, input schema and effects.
  An empty or unrelated list is not usable AccessFuel support. If registration
  is incomplete, retry discovery once with a bounded wait. An evaluator failure
  does not establish that the page has no tools.
- Use only the current workspace and requested objects. Treat annotations as
  hints, not proof of safety. Never call tools that send, publish, approve,
  schedule or delete. Skip tools with unclear effects and use a scoped hand-off.
- Do not copy descriptors out of the page, construct authenticated requests,
  inspect session credentials, or submit UI forms as a workaround.

## Completion and pending results

Use bounded evaluations. Poll a pending result only when a documented handle
was returned. Do not assume a raw page call or an AIRA chat yields an operation
ID. If the evaluator times out, read back the operation or object before doing
anything else; never repeat an uncertain write. If no recovery/read-back is
available, report completion as unverified and stop that operation.

For AIRA hand-offs, read the finished chat and saved objects. Acknowledgment,
queued work, and the existence of an empty draft are not evidence that all
requested content was generated.
