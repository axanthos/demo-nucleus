# ResearchFlow project instructions — ChatGPT

> Generated: 2026-11-20 UTC. Sources: `ai/context/rf_method_protocol.md` v2.1 (2026-07-25); `ai/context/project_charter.md` (2026-11-17 text, ratified in RF record 2026-11-17). Target: ChatGPT project instructions. Generated operational projection; do not edit directly.

## Authority and context

The repository's `ai/context/rf_method_protocol.md` is authoritative for RF method; `ai/context/project_charter.md` is authoritative for project-specific commitments. The RF artifact record (`.researchflow/artifacts.toml`, `.researchflow/events.tsv`) confirms the charter was **ratified on 2026-11-17**. Its source Markdown nevertheless retains the header **"Discussion draft — not ratified"**; this is an unresolved source/status inconsistency, not a withdrawal of ratification. Do not silently rewrite the charter. Chat/UI instructions and agent files are generated operational projections, never primary sources or independently edited. When either source changes, regenerate each relevant rendering, date/version-stamp it, and check it against the target's configured character cap. Keep operational requirements; compress rather than omit important rules.

## Research identity and frontier

Project `demo-nucleus`: a small but genuine, controlled empirical investigation of textual versus emoji-based expressions of laughter in the *What's New, Switzerland?* French-speaking WhatsApp corpus. It also demonstrates ResearchFlow; the demonstration cannot predetermine scholarly questions, methods, or findings.

Central question: how are textual and emoji laughter resources distributed and combined, including co-occurrence, alternation, and distinct speaker profiles? Do not presume pragmatic complementarity or substitution from message-level patterns. Primary emphasis: distribution/combination and speaker variation. Intra-speaker change over time is an interesting but conditional extension, not a required focus of this limited demonstration.

Initial objectives: identify a justified resource inventory; examine within-message distribution and joint/separate occurrence; examine speaker variation; consider temporal change only where supportable. Literature review precedes design fixation, assessing previous work, conceptual framing, and originality. Open choices include candidate forms (including ambiguous abbreviations), emoji variants, analytical units and denominators, contextual ambiguity, comparisons, speaker and temporal coverage, privacy/access constraints, and interpretation. The ratified charter commits to no particular test, method, effect, or fixed inventory. Work reproducibly, document choices and limits, accept negative/inconclusive findings. Generalization beyond the corpus needs justification. Consult the charter for its full wording.

## RF working method

- Discuss design before writing specifications. **No code without a spec in `specs/`**; write tests against that spec before implementation. Never change a test assertion without individual approval. Compute environmental expected values (timezone, locale, paths) via the same public helpers as production.
- On bugs, establish and explain the root-cause mechanism before fixing. Keep the prototype proportionate; avoid premature scale-driven engineering.
- Construct each shipped file by diffing against the **latest** supplied repository snapshot, not a stale workspace. Coordinate concurrent clients via repository manifests and the patch register, not assumed chat synchrony.
- Use coherent, semantically bounded work episodes. Persist important history in the governed record, durable project commitments in charter/specs, multi-episode work in a programme document when needed, and the current frontier in an episode handoff. Do not duplicate actionable rules across layers.
- At close preserve active objectives, unresolved issues, assumptions, results (mark derived vs hypothetical vs open), operating/review conventions where necessary, and a useful re-entry point. A manifest retrospectively records contributions; a handoff prospectively orients the next mediator. Test the adequacy of continuity: if a new mediator has to reconstruct prior work, record and repair the missing handoff state.
- Resume by reading the designated handoff and consolidated documents it references. Retrieve older chats, records, or external context only for a **specific** missing dependency; do not exhaustively rediscover settled reasoning.

## RF patch and manifest requirements

- Deliver repo-relative files in a ZIP applied by `uv run tools\apply_patch_zip.py --repo . --zip <path> --overwrite` (Windows command spelling from RF protocol).
- Name each newly built patch `rf_patch_<project-slug>_YYYYMMDD_HHMMSS.zip` with timestamp at build time in **UTC**; never reuse names. Include an imperative, one-line commit message no longer than 72 characters, without a period.
- Every patch includes an episode manifest `ai/sessions/manifests/<YYYYMMDD>_<slug>.md`. Use TOML front matter with `schema`, `project`, `lane`, `client`, `model`, `date`, `episode`, `patches`, followed by `## Intention`, `## Decisions`, `## Artifacts`, `## Sources`, `## Relations`, `## Open points`.
- Relations must have full literal repo-relative paths, backticked as ``- `<source_path> -> <family> -> <target_path>` ``. Allowed families: `refines`, `produces`, `derived_from`, `implements`, `tests`, `supports`, `cites`, `supersedes`, `depends_on`, `provides_context_for`, `related_to`, `executes`, `imports`, `applies`, `appends`. Incomplete paths create misleading placeholders.
- Write manifests only at episode close; never reconstruct old missing manifests. Optional `## Researcher note` is exclusively the researcher's own words, added during review or acceptance—never drafted by the model.

## Implementation and architecture, if later relevant

Python 3.11+, typed APIs, frozen config dataclasses, module/function docstrings, and clear ~5–7-line code paragraphs each preceded by a comment line. Use `tomllib` to read and `tomli-w` to write TOML; credentials only through `keyring`; typed, human-readable, field-specific errors. Keep RF file-first and local-first; separate pure components from thin side-effect wrappers. Machine-local settings belong in untracked `machine.toml`, project settings in `project.toml`; keep raw stored paths and expand `~` only when used. RF mirrors/logs rather than replacing Git, editors, or chat UIs. Keep agent loops out of the record kernel; agent action happens at adapter boundaries under lane gates (default: review-before-inscription via consolidated changesets).
