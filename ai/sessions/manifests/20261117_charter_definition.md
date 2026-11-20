+++
schema = "rf-episode-manifest/v0-draft"
project = "demo-nucleus"
lane = "chat"
client = "chatgpt"
model = "gpt-6"
date = "2026-11-17"
episode = "Define initial research identity and charter"
patches = ["rf_patch_demo-nucleus_20261117_112148.zip"]
+++

## Intention

Define a research identity and appropriately bounded goals for a genuine ResearchFlow demonstration, and submit a proposed project charter for researcher review and ratification.

## Decisions

- Proposed research subject: the relationship between textual and emoji-based laughter markers in the *What's New, Switzerland?* French-speaking WhatsApp corpus.
- Primary focus for this controlled demonstration: distribution, co-occurrence/alternation, and speaker-level usage profiles.
- Within-speaker temporal variation remains of research interest but is conditional and secondary at this stage.
- Preserve the charter at the proposal's level of specificity; a literature review and corpus assessment must precede substantive operational choices.
- The charter is **not ratified** by this patch; researcher approval remains outstanding. No research analysis or literature review has been performed.

## Artifacts

- `ai/context/project_charter.md`: the frozen discussion draft for review; no method or result fixed in advance.
- `ai/context/renderings/chatgpt_project_instructions.md`: generated, version/date-stamped operational instructions for ChatGPT.
- `ai/context/renderings/claude_project_instructions.md`: generated, version/date-stamped operational instructions for Claude.
- `ai/sessions/manifests/20261117_charter_definition.md`: retrospective episode account (this manifest).

## Sources

- `ai/context/rf_method_protocol.md` (v2.1, 2026-07-25), read from the snapshot supplied for this episode; governs workflow and patch form.
- User's in-episode research formulation, including candidate marker types, analytical scales, and questions intentionally left open.
- User's ratification workflow instruction and decision to prioritize the first aspect while retaining longitudinal analysis as a possible extension.
- No external literature, corpus data, or empirical findings were consulted or introduced.

## Relations

- `ai/sessions/manifests/20261117_charter_definition.md -> produces -> ai/context/project_charter.md`
- `ai/context/renderings/chatgpt_project_instructions.md -> derived_from -> ai/context/project_charter.md`
- `ai/context/renderings/chatgpt_project_instructions.md -> derived_from -> ai/context/rf_method_protocol.md`
- `ai/context/renderings/claude_project_instructions.md -> derived_from -> ai/context/project_charter.md`
- `ai/context/renderings/claude_project_instructions.md -> derived_from -> ai/context/rf_method_protocol.md`

## Open points

- Researcher review and explicit ratification or revision of `ai/context/project_charter.md`.
- Subsequent literature review and corpus access/coverage assessment before methods or coding decisions.
- Open marker inventory, segmentation/unit of analysis, ambiguity handling, comparison strategy, and temporal feasibility.
- Rendering character limits are not specified in the supplied project snapshot; generated renderings were conservatively kept under 8,000 characters each pending confirmation of configured limits.
