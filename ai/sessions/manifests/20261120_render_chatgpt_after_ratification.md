+++
schema = "rf-episode-manifest/v0-draft"
project = "demo-nucleus"
lane = "chat"
client = "chatgpt"
model = "gpt-6"
date = "2026-11-20"
episode = "Render ChatGPT project instructions after charter ratification"
patches = ["rf_patch_demo-nucleus_20261120_132104.zip"]
+++

## Intention

Update the ChatGPT paste-ready project-instructions rendering against the latest supplied `demo-nucleus` snapshot to reflect the ResearchFlow-recorded ratification of the existing charter, without changing the charter itself.

## Decisions

- The charter is ratified in the governed record (ratification event dated 2026-11-17 and artifact `decision_state = "ratified"`). This is a governance-state update, not new research content or a fresh approval by the model.
- The charter Markdown still begins `**Status:** Discussion draft — not ratified`; preserve that source file verbatim and surface the discrepancy explicitly in the rendering rather than silently modifying the ratified text.
- Refresh only the ChatGPT rendering requested by the researcher. Keep the charter's limited, genuine research scope and retain the RF method requirements and existing methodological open questions.
- The Claude rendering is not changed by this patch. No literature review, corpus analysis, analytical design, or implementation was carried out.

## Artifacts

- `ai/context/renderings/chatgpt_project_instructions.md`: regenerated ChatGPT project instructions with a new generation stamp, corrected governed ratification status, and unchanged substantive working protocol.
- `ai/sessions/manifests/20261120_render_chatgpt_after_ratification.md`: retrospective manifest for this rendering patch.
- `ai/context/project_charter.md`: ratified source, **not included or modified** in the patch.

## Sources

- Supplied `demo-nucleus-snapshot-20261120-141854-full.zip` (most recent snapshot for this episode).
- `ai/context/project_charter.md` (snapshot content hash SHA-256 `e2ff098946c605fed7d23d2bcaf6c2686e4719343f3d9d79b1d63292d1d9cbe6`); its text still bears the outdated discussion-draft status header.
- `ai/context/rf_method_protocol.md` v2.1 (2026-07-25), especially context governance, patch protocol, and manifest schema.
- `.researchflow/artifacts.toml` and `.researchflow/events.tsv` from the snapshot: charter decision state `ratified`, event on 2026-11-17.
- Previous `ai/context/renderings/chatgpt_project_instructions.md` as basis for preserving the existing curated operational projection.

## Relations

- `ai/sessions/manifests/20261120_render_chatgpt_after_ratification.md -> produces -> ai/context/renderings/chatgpt_project_instructions.md`
- `ai/context/renderings/chatgpt_project_instructions.md -> derived_from -> ai/context/project_charter.md`
- `ai/context/renderings/chatgpt_project_instructions.md -> derived_from -> ai/context/rf_method_protocol.md`

## Open points

- The charter's first-line status disagrees with the RF ratification record; any correction of the source text should be separately authorized and tracked.
- The older Claude rendering still describes the charter as unratified and is outside the scope of this ChatGPT-only patch.
- No configured maximum length for the ChatGPT target surface is present in the supplied snapshot; this projection has 6626 characters, under a conservative 8,000-character working ceiling.
- Literature review, corpus assessment, and analytical operationalization remain future research work.
