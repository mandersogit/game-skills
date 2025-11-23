# Plan: Converting Fate SRDs into Agent Skills

## Goal and guiding sources
- Build a complete library of Claude agent skills that captures 100% of the rules and guidance across all Fate SRD documents (core, toolkits, and setting-specific SRDs).
- Ensure every contributor starts by reading the Claude Agent Skills overview to align on what a skill is, how progressive disclosure works, and the three loading levels (metadata, SKILL.md instructions, deeper resources). 【F:reference/claude-docs/agent-skills/overview.md†L1-L107】
- Ensure every contributor reads and follows the Skill Creator skill before drafting or updating a skill, since it codifies the required metadata, structure, and concision principles. 【F:reference/anthropic-skills/skill-creator/SKILL.md†L2-L70】
- Conform to the Anthropic Agent Skills Spec: every skill is a folder with a `SKILL.md` entrypoint that begins with YAML frontmatter declaring the `name` and `description`, plus optional metadata fields. 【F:reference/anthropic-skills/agent_skills_spec.md†L1-L55】
- Reuse patterns from the Superpowers collection: concise, purpose-focused skills grouped by workflow domains and surfaced through predictable activation conventions. 【F:reference/obra-superpowers/README.md†L1-L130】

## Overall process
0. **Orient on the Claude Agent Skills model**
   - Read `reference/claude-docs/agent-skills/overview.md` for a grounding in progressive disclosure, the three loading levels, and the code-execution context that underpins SKILL.md, auxiliary references, and scripts. 【F:reference/claude-docs/agent-skills/overview.md†L34-L128】
   - Skim the Agent Skills quickstart to see how skills are invoked and versioned via `skill_id` in API calls; keep these triggers in mind when writing discovery-friendly descriptions. 【F:reference/claude-docs/agent-skills/quickstart.md†L13-L110】

1. **Inventory and scope the SRDs**
   - List all SRD markdown files under `reference/fate-srd/markdown/` and log their intended audiences (players, GMs, setting material, toolkits).
   - Note duplicated rule explanations across SRDs (e.g., Fate Accelerated vs Fate Core) to plan for shared “core rules” skills plus setting overlays.

2. **Segment each SRD into atomic topics**
   - Parse the document outline (headings, subheadings, callouts) and normalize terminology.
   - Break content into atomic “teachable units” that map to a single user task, rule concept, or procedure (e.g., “Create high concept”, “Apply aspects”, “Run contests”).
   - Capture cross-references between units (e.g., “Aspects” underpin “Invoking for effect”).

3. **Define skill taxonomy and folder layout**
   - Organize skills by role (player-facing, GM-facing), phase (character creation, play loop, advancement), and system component (aspects, approaches/skills, stress/consequences, actions & outcomes, extras, setting tools).
   - Mirror Superpowers’ clarity by grouping skills under domain folders (e.g., `skills/character-creation/`, `skills/actions-and-outcomes/`, `skills/setting-tools/`). Pull navigation copy and naming conventions directly from the template frontmatter to keep folder names aligned with SKILL names. 【F:reference/anthropic-skills/template-skill/SKILL.md†L1-L6】
   - For setting-specific SRDs, add overlays in sibling folders (e.g., `skills/settings/frontier-spirit/`) that extend or override core guidance.
   - Reserve lightweight `references/` subfolders for long rule examples, stunt catalogs, and setting generators so SKILL.md bodies stay lean while still discoverable through explicit links. 【F:reference/anthropic-skills/skill-creator/SKILL.md†L93-L149】

4. **Author SKILL.md templates per unit**
   - First, review the Skill Creator skill to apply its guidance on metadata, progressive disclosure, and what to include or exclude from a skill folder. 【F:reference/anthropic-skills/skill-creator/SKILL.md†L2-L113】
   - Start from a template that includes: YAML frontmatter (name, description, optional license/metadata), a short “When to use” blurb, step-by-step guidance, examples, pitfalls, and cross-links to related skills.
   - Keep instructions concise and actionable like the Superpowers skills, with explicit triggers and outputs. Lean on the best-practices guidance to trim unnecessary context and right-size the specificity for each workflow. 【F:reference/claude-docs/agent-skills/best-practices.md†L13-L133】
   - Enforce the Agent Skills Spec requirements early: SKILL.md must open with YAML containing hyphen-case `name` and an explicit `description`, and should avoid auxiliary markdown files like README to prevent clutter. 【F:reference/anthropic-skills/agent_skills_spec.md†L1-L55】【F:reference/anthropic-skills/skill-creator/SKILL.md†L65-L118】
   - Provide a short “progressive disclosure” checklist in each template to decide what moves into `references/` (long examples, variant stunts, optional subsystems) versus what remains in the SKILL.md core workflow. 【F:reference/anthropic-skills/skill-creator/SKILL.md†L119-L190】

5. **Validate completeness**
   - Map each SRD heading to at least one skill; maintain a coverage spreadsheet or YAML index that records the SKILL path(s) covering each section.
   - For overlapping rules, ensure the shared core skill is referenced by all relevant overlays to prevent divergence.
   - Add a “Spec compliance” column that confirms each skill folder hits the mandatory frontmatter fields and keeps SKILL.md under ~500 lines, with heavy content shifted into linked references. 【F:reference/anthropic-skills/agent_skills_spec.md†L1-L55】【F:reference/anthropic-skills/skill-creator/SKILL.md†L119-L190】

6. **Review and iterate**
   - Peer review for clarity and fidelity to the SRD text; test-drive skills in sample scenarios.
   - Version and license compliance: include SRD attribution and CC licensing where required in metadata or accompanying LICENSE files.

## Example transformation: Fate Accelerated (character creation)
Using the Fate Accelerated SRD as a worked example, here is how to translate a section into skills.

1) **Source segment**
   - The “Who Do You Want To Be?” section explains the character creation building blocks and highlights that every player shares responsibility for telling the story. 【F:reference/fate-srd/markdown/fate-accelerated-SRD.md†L81-L171】

2) **Atomic units extracted**
   - Collaboratively tell the story and make choices that improve the table’s experience.
   - Define character concept elements: high concept, trouble, additional aspects, name/appearance.

3) **Resulting skills**
   - `skills/fate-core/story-collaboration/` – Guidance for players and GMs on making narrative-forward choices that help everyone have fun. Pulls the two key behaviors from lines 84-93 (stay in character, choose story-interesting actions). 【F:reference/fate-srd/markdown/fate-accelerated-SRD.md†L84-L93】
   - `skills/fate-core/character-aspects/high-concept/` – How to craft a high concept that both helps and complicates the character, with examples for inspiration. 【F:reference/fate-srd/markdown/fate-accelerated-SRD.md†L123-L131】
   - `skills/fate-core/character-aspects/trouble/` – How to define the recurring problem or obligation that complicates the character’s life, plus sample troubles. 【F:reference/fate-srd/markdown/fate-accelerated-SRD.md†L133-L141】
   - `skills/fate-core/character-aspects/additional-aspects/` – Guidance for choosing extra aspects now or during play and tying them to relationships or signature traits. 【F:reference/fate-srd/markdown/fate-accelerated-SRD.md†L143-L155】
   - `skills/fate-core/character-fundamentals/name-and-appearance/` – Quick checklist for naming the character and writing a visual description. 【F:reference/fate-srd/markdown/fate-accelerated-SRD.md†L156-L159】

4) **SKILL.md outline for one unit (high concept)**
   - Frontmatter: `name: fate-high-concept`, `description: Craft a high concept aspect that defines who your character is and creates both advantages and complications`.
   - Body: When to use (during character creation or refresh), step-by-step prompts to draft phrasing, dual-purpose test (helps & hinders), 3-5 example high concepts from the SRD, and a short checklist for invoking/compelling uses.

5) **Coverage mapping**
   - Add an entry to the coverage index noting that `fate-accelerated-SRD.md` lines 123-131 map to `character-aspects/high-concept` and that the same skill also serves Fate Core’s equivalent guidance.

## Deliverables to reach 100% coverage
- A root `skills/` tree containing modular skills for every Fate SRD rule, example, and procedure.
- A coverage index (YAML/CSV) linking SRD sections to skill paths, updated as new SRDs are parsed.
- Authoring guidelines + template to ensure consistency across contributors.
- Validation checklist aligned with the Agent Skills Spec to confirm every skill has correct frontmatter and clear activation/use instructions.
