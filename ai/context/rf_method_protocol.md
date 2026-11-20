# RF method protocol

Version: 2.1 (2026-07-25). Generic, project-independent instructions for
AI collaborators on any RF-governed project. Slow-moving by design;
destined to ship with RF (`rf init`). Project specifics live in
`project_charter.md`, never here.

## Context governance

- The repo copies of this file and the project charter are the source of
  truth. UI project fields (Claude, ChatGPT) and agent context files
  (`CLAUDE.md`, `AGENTS.md`) are renderings: generated from source,
  stamped with source version and date, never edited in place.
- Any patch that changes a source file also regenerates the paste-ready
  rendering under `ai/context/renderings/`. Renderings are curated operational
  projections, not concatenations, but should preserve the protocol's actionable
  requirements substantially intact. Compress wording before dropping whole
  requirements; if project-state detail causes overflow, move it to the correct
  continuity layer rather than hollowing out the general method. Validate each
  rendering against the target surface's configured character limit.
- Continuity never relies solely on the transient working memory of one
  human or model mediator. The governed record preserves history,
  project context consolidates durable state, and episode handoffs carry
  the active frontier.

## Workflow

- Spec-first: no code without a spec in `specs/`; design discussion
  precedes specs; tests are written against the spec before
  implementation.
- Test assertions are never changed without case-by-case approval.
  Expected values that depend on environment (timezone, locale, paths)
  are computed through the same public helpers production uses.
- Root cause before fix when debugging; explain the mechanism.
- Every file shipped is built by diffing against the latest snapshot,
  never from a stale working copy.
- Long-running work proceeds in coherent episodes rather than relying on
  indefinitely growing chats. Episode boundaries follow the work's
  semantic structure, not an arbitrary message count.

## Continuity of inquiry

- Keep universal RF method in this protocol. Distinguish durable project 
  continuity, active programme continuity, and episode continuity
  Put durable project-specific commitments in the charter and in specifications;
  a programme document carries the active multi-episode arc; a handoff states 
  what is still in motion and where the next episode should resume. Avoid 
  duplicating actionable rules across layers.
- At episode close, preserve the minimum state needed for a fresh
  mediator to resume productive work without avoidable rediscovery or
  qualitative discontinuity. The exact fields may vary by work type;
  theoretical derivation, debugging, and implementation need not share
  one rigid template.
- Preserve active objectives, current frontier, unresolved tensions,
  relevant assumptions, and a recommended re-entry point when they are
  needed for continuation. Mark conclusions as derived, hypotheses, or
  open questions when that distinction matters.
- Episode handoffs complement manifests. Manifests are retrospective
  governed accounts of what an episode contributed; handoffs are
  prospective orientation for continuation.
- Treat continuity as a functional requirement. Evaluate the practice 
  empirically: if a fresh mediator must reopen old chats or reconstruct settled
  reasoning, record what was missing and revise the continuity practice.
- Preserve operational context as well as informational state when
  continuity depends on it. Operational context may include the active
  division of labour, mode of work, decision strategy, review discipline,
  validation criteria, or other conventions whose loss would materially
  change how work proceeds after a mediator change.
- Resume continuity-first. Begin with the designated episode handoff and
  the consolidated documents it explicitly references; presume that this
  governed continuity state is sufficient for normal continuation.
- Expand retrieval only when continuation reveals a concrete missing
  dependency. Do not search older conversations, episode records, or
  external personal context merely as a precaution. When the designated
  continuity state proves insufficient, record the gap and improve the
  continuity representation rather than making exhaustive recovery the
  normal resumption procedure.

## Patch protocol

- Patches are zip files with repo-relative paths, applied with
  `uv run tools\apply_patch_zip.py --repo . --zip <path> --overwrite`.
- Naming: `rf_patch_<project>_YYYYMMDD_HHMMSS.zip`, where `<project>`
  is the project slug from `project.toml` and the timestamp is taken at
  build time, in UTC. The slug disambiguates across projects (one Downloads
  folder serves many repos); the timestamp disambiguates across
  parallel clients. Uniqueness is the invariant: names are never
  reissued, even for corrected or superseded patches; a client without
  a reliable clock must ensure uniqueness by other means.
- Each patch is sent with a commit message: title line only, imperative
  mood, max 72 chars, no trailing period.

## Parallel clients

- Several AI clients (e.g. Claude and ChatGPT) may serve the chat lane
  of one project in parallel. Timestamp naming makes their patches
  collision-free without coordination; the manifest front matter
  (`client`, `model`) carries attribution.
- Every client builds against the latest snapshot, never a stale
  working copy; the patch register and the manifests are the surface
  through which each track sees the other's work.
- Each client surface gets its own rendering of the context files,
  regenerated on source version bump (see Context governance).

## Episode manifest protocol

- Every patch includes an episode manifest at
  `ai/sessions/manifests/<YYYYMMDD>_<slug>.md`.
- Schema `rf-episode-manifest/v0-draft`: TOML front matter (schema,
  project, lane, client, model, date, episode, patches) over sections
  `## Intention`, `## Decisions`, `## Artifacts`, `## Sources`,
  `## Relations`, `## Open points`.
- Every relation MUST use one of the admissible relation families defined by 
  the project record model. Current families are: refines, produces, 
  derived_from, implements, tests, supports, cites, supersedes, depends_on, 
  provides_context_for, related_to, executes, imports, applies, and appends.
- Relations proposals are written as code spans (backticked) to
  survive markdown emphasis/math processing of snake_case paths:
  ``- `<source_path> -> <family> -> <target_path>` ``. Both paths are
  full repo-relative paths from the project root, exactly as they
  appear in the repo tree — e.g. `writeup/theory_notes/foo.md`, never
  a bare filename like `foo.md`. Ingestion resolves a relation by
  matching this literal path against the artifact store; an
  incomplete path does not error, it silently links a placeholder
  record instead of the real file.
- Manifests are written at episode close, never reconstructed for past
  episodes; missing manifests stay missing.
- Manifests may end with an optional `## Researcher note` section:
  two or three sentences in the researcher's own words, added at
  review or acceptance time. It is the one manifest section never
  written by a model — voice, not summary. Models leave it out;
  boundary tooling may prompt for it.

## Code style

- Python 3.11+, type hints throughout, frozen dataclasses for config.
- Lines grouped into ~5–7 LOC paragraphs, each preceded by one comment
  line; module and function docstrings required.
- Explicit over clever; no magic. `tomllib` for TOML reads, `tomli-w`
  for writes. Credentials via `keyring` only. Typed exceptions with
  human-readable, field-specific messages.

## Architecture principles

- File-first: all state is plain text in the project directory.
- Local-first: no cloud dependency for core functionality.
- Delegate to best-of-breed: no Git commit UI, no code editor, no chat
  UI. RF mirrors and logs; it does not host.
- Machine settings in `machine.toml` (outside repo); project settings in
  `project.toml` (in repo). Path fields stored raw; tilde expansion at
  point of use only. Pure components; side effects in thin wrappers.
- Agent rule: the record kernel contains no agent loops and never
  invokes models. Agentic execution happens at adapter boundaries under
  per-lane gate policy (default: review-before-inscription with
  consolidated changesets).

## What to avoid

- Over-engineering for scale while prototyping.
- Jumping to code without design discussion.
