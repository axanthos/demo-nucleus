+++
schema = "rf-episode-manifest/v0-draft"
project = "demo-nucleus"
lane = "chat"
client = "chatgpt"
model = "gpt-6"
date = "2026-11-20"
episode = "Correct WebUI project-instructions rendering path"
patches = ["rf_patch_demo-nucleus_20261120_133359.zip"]
+++

## Intention

Correct the WebUI project-instructions rendering path from `ai/context/renderings/chatgpt_project_instructions.md` to the canonical `ai/context/renderings/webui_project_instructions.md`, preserving the latest previously delivered rendering byte for byte. This is a file-path maintenance episode, not a research episode.

## Decisions

- Treat the researcher-provided path correction as authoritative: the canonical WebUI rendering path is `ai/context/renderings/webui_project_instructions.md`.
- Reuse the exact bytes of `ai/context/renderings/chatgpt_project_instructions.md` as delivered in `rf_patch_demo-nucleus_20261120_132104.zip`, rather than the older rendering in the supplied snapshot. No wording, version stamp, ratification interpretation, or substantive content is changed.
- The source RF method protocol and ratified research charter remain unchanged, as do the Claude rendering and all research decisions.
- The repository-relative ZIP patch contains the destination file and this manifest only. The supplied RF protocol documents ZIP file addition/overwrite, but no deletion operation. To complete the **move**, the obsolete `ai/context/renderings/chatgpt_project_instructions.md` must be removed in the repository after import; do not retain it as a competing WebUI rendering.

## Artifacts

- `ai/context/renderings/webui_project_instructions.md`: byte-identical relocation of the latest delivered ChatGPT/WebUI rendering; SHA-256 `0e471b962fca5dd8b2fe25894bb1228d3924389ad4bff96d3aad000d2b21782a` (6634 bytes, 6626 Unicode characters).
- `ai/sessions/manifests/20261120_webui_rendering_path_correction.md`: retrospective provenance and relocation instructions for this patch.
- `ai/context/renderings/chatgpt_project_instructions.md`: obsolete source path; **remove from repository after importing this ZIP**. Not included or overwritten by the ZIP.
- `ai/context/project_charter.md` and `ai/context/rf_method_protocol.md`: source documents, neither modified nor included in this patch.

## Sources

- Supplied `demo-nucleus-snapshot-20261120-141854-full.zip`, the latest supplied repository snapshot; used to verify project identity and RF method, and to identify the obsolete rendering path. The snapshot predates the successful updated rendering patch.
- Previously delivered `rf_patch_demo-nucleus_20261120_132104.zip`, specifically `ai/context/renderings/chatgpt_project_instructions.md` with SHA-256 `0e471b962fca5dd8b2fe25894bb1228d3924389ad4bff96d3aad000d2b21782a`: authoritative **content source** for the copied rendering.
- `ai/sessions/manifests/20261120_render_chatgpt_after_ratification.md` from that previous patch: provenance for the ratification-aware rendering.
- `ai/context/rf_method_protocol.md` v2.1 (2026-07-25), from the snapshot: patch packaging, UTC filenames, manifest schema, relation paths, and context governance.
- `ai/context/project_charter.md` in the snapshot (SHA-256 `e2ff098946c605fed7d23d2bcaf6c2686e4719343f3d9d79b1d63292d1d9cbe6`): unmodified source for the existing rendered project identity.
- Researcher's current instruction specifying the canonical WebUI path and requiring a minimal correction only. No external references or empirical analysis used.

## Relations

- `ai/sessions/manifests/20261120_webui_rendering_path_correction.md -> produces -> ai/context/renderings/webui_project_instructions.md`
- `ai/context/renderings/webui_project_instructions.md -> supersedes -> ai/context/renderings/chatgpt_project_instructions.md`
- `ai/context/renderings/webui_project_instructions.md -> derived_from -> ai/context/renderings/chatgpt_project_instructions.md`
- `ai/context/renderings/webui_project_instructions.md -> derived_from -> ai/context/project_charter.md`
- `ai/context/renderings/webui_project_instructions.md -> derived_from -> ai/context/rf_method_protocol.md`

## Open points

- **Required import cleanup:** the file-overlay ZIP format does not express removal. After importing, remove `ai/context/renderings/chatgpt_project_instructions.md` from the repository (for example, `git rm ai/context/renderings/chatgpt_project_instructions.md`) and confirm only `ai/context/renderings/webui_project_instructions.md` is active. If this obsolete path has already been removed, no deletion is needed.
- The charter's Markdown status header remains at odds with its RF ratification record, as documented in the preceding episode; out of scope and untouched here.
- No literature review, corpus inspection, analytical specification, or research advancement was performed.
