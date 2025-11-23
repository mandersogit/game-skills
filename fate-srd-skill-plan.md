# Plan: Converting Fate SRDs into Agent Skills

## 1. Audience, definitions, and objectives

### 1.1 Who this plan is for

This plan is for **skill authors** (humans or agent sub‑agents) who will transform Fate SRD texts into **Claude agent skills**.

It assumes you:

- Understand Fate at a basic level (what SRDs are, how aspects/skills/stunts work).
- Are comfortable editing markdown.
- Have read at least one of the Fate SRDs you intend to work on.

### 1.2 What “skills” means here

In this document, **“skills” always means Claude agent skills**, not in‑universe Fate character skills.

- **Agent skill**: a folder with a `SKILL.md` that teaches Claude a **procedure or capability** (e.g., “facilitate Fate character creation,” “run a conflict,” “explain compels to a new player”). 【F:reference/anthropic-skills/agent_skills_spec.md†L1-L55】
- **Fate character skills/approaches**: in‑game stats like Fight, Athletics, Flashy, etc. These are SRD content that the agent may reference inside a SKILL, but they are **not** Claude skills by themselves.

Every SKILL produced from this plan is:

- **Agent‑facing** first, written to help the model:
  - run or co‑run a Fate game,
  - assist a human GM or player,
  - teach Fate rules,
  - or generate Fate‑compatible content.
- **Human‑readable** second, so a GM or designer can inspect and refine it.

### 1.3 Objectives

Across all Fate SRDs under `reference/fate-srd/markdown/`, this plan aims to:

- Build a complete library of Claude agent skills that captures **100% of the rules, procedures, and table guidance** across Fate SRDs (core, toolkits, and setting‑specific SRDs).
- Ensure skills are organized around **play responsibilities and workflows**, not just rule sections:
  - Table setup & safety
  - Teaching and rules tutoring
  - Character and party creation
  - Scene/challenge/conflict procedures
  - GM operations (prep, pacing, spotlight, campaign structure)
  - Content generation (NPCs, scenarios, settings)
- Provide a **repeatable template** for per‑SRD plans (e.g., Fate Condensed, Fate Core, Fate Accelerated, System Toolkit, setting SRDs), so new SRD→skill collections can be added without reinventing the process.

---

## 2. Goal and guiding sources

### 2.1 Agent Skills docs and patterns

All contributors **must** familiarize themselves with:

- **Claude Agent Skills overview** – describes progressive disclosure, loading levels (metadata, SKILL.md, deeper resources), and how skills are invoked. 【F:reference/claude-docs/agent-skills/overview.md†L1-L107】
- **Agent Skills quickstart** – shows how `skill_id`s are used in API calls, and what good names/descriptions look like. 【F:reference/claude-docs/agent-skills/quickstart.md†L13-L110】
- **Agent Skills Spec** – defines required SKILL.md frontmatter (`name`, `description`, etc.) and file layout rules. 【F:reference/anthropic-skills/agent_skills_spec.md†L1-L55】
- **Skill Creator skill** – codifies metadata, progressive disclosure, and the core do/don’t list for SKILL contents. 【F:reference/anthropic-skills/skill-creator/SKILL.md†L2-L113】
- **Template skill** – minimal example to mirror in structure and naming conventions. 【F:reference/anthropic-skills/template-skill/SKILL.md†L1-L6】
- **Best practices** – guidance on concision, specificity, and when to push content into references. 【F:reference/claude-docs/agent-skills/best-practices.md†L13-L133】

We also reuse patterns from the **Superpowers** collection (short, purpose‑driven skills grouped by workflow). 【F:reference/obra-superpowers/README.md†L1-L130】

### 2.2 Fate SRD sources

For Fate, the primary SRDs live under:

- `reference/fate-srd/markdown/`

This includes, at minimum (names may vary slightly):

- Fate Core SRD
- Fate Accelerated SRD
- Fate Condensed SRD
- Fate System Toolkit
- Fate Worlds / setting SRDs

Each of these will eventually have **its own per‑SRD plan** (see §7).

---

## 3. What the skills must enable (play responsibilities)

Every Fate‑related agent skill should explicitly support one or more **play responsibilities**. This is how we avoid “pure extraction” skills that don’t help at the table.

Define the following responsibility tags and use them consistently:

- `table-setup` – materials, expectations, safety tools, session zero.
- `rules-tutoring` – explaining rules and options to new or existing players.
- `character-creation` – building or advancing PCs, extras, or similar entities.
- `scene-procedures` – challenges, contests, conflicts, scene framing and transitions.
- `gm-operations` – prep, pacing, spotlight management, difficulty setting, etc.
- `content-generation` – NPCs, locations, issues, obstacles, fronts, etc.
- `meta-system` – licensing, system comparisons, migration from earlier Fate editions.

**Every SKILL.md must declare at least one responsibility tag** in its frontmatter (see §6.2).

When we say “100% coverage,” we mean:

- Every **SRD rule section** is covered,
- And every **play responsibility** above has robust, cross‑SRD support.

---

## 4. Non‑goals and guardrails

To avoid regressions and confusion:

- Do **not** create one Claude skill per Fate **character skill/approach** (e.g., no `fate-core-skill-fight`). Character skills live **in characters**, not as Claude skills.
- Do **not** dump stunt or spell catalogs into SKILL.md bodies. Long lists belong in `references/` or external tools; SKILL.md should show patterns and procedures for using or writing stunts.
- Do **not** introduce house rules or personal hacks unless:
  - they are explicitly framed as optional,
  - clearly separated from SRD‑derived content,
  - and tagged accordingly.
- Do **not** write SKILLs that only mirror SRD prose. Each SKILL must encode **procedures, decision rules, and examples** that help the agent act at the table.

If you cannot articulate how a proposed SKILL helps a GM, player, tutor, or content‑author in a Fate game, it likely doesn’t belong in this library.

---

## 5. Overall process

This section governs **all** Fate SRDs. Individual SRDs will refine this via their own `*-skills-plan.md` (see §7).

### 0. Orient on the Claude Agent Skills model

Before touching Fate content:

- Read the Agent Skills overview for progressive disclosure, loading levels, and the execution environment for SKILLs and references. 【F:reference/claude-docs/agent-skills/overview.md†L34-L128】
- Skim the quickstart to see `skill_id` usage and how names/descriptions impact discovery. 【F:reference/claude-docs/agent-skills/quickstart.md†L13-L110】
- Review Skill Creator and best practices to internalize how to:
  - keep SKILL.md bodies lean,
  - push long examples and catalogs into `references/`,
  - and structure procedures as actionable lists. 【F:reference/anthropic-skills/skill-creator/SKILL.md†L65-L118】【F:reference/claude-docs/agent-skills/best-practices.md†L13-L133】

### 1. Inventory and scope the SRDs

For Fate specifically:

1. List all SRD markdown files under `reference/fate-srd/markdown/`.
2. For each SRD, record:
   - **System**: `fate-core`, `fate-accelerated`, `fate-condensed`, `toolkit`, `worlds/<name>`, etc.
   - **Type**: core rules, variant rules, toolkit, setting, adventure.
   - **Intended audience**: players, GMs, both.
   - **Overlap**: which rules duplicate or specialize other SRDs (e.g., FAE reuses Fate Core actions & aspects).

This inventory will drive:

- which **per‑SRD plan** files we need,
- where **shared core skills** vs **system overlays** live.

### 2. Segment each SRD into atomic units

For each SRD:

1. Parse its structure (headings, subheadings, callouts).
2. Identify **atomic “teachable units”** – chunks that correspond to:
   - a single user task (e.g., “create a high concept aspect”),
   - a discrete procedure (e.g., “run a challenge in Fate Core”),
   - or a compact concept with clear edges (e.g., “GM Fate point budget”).
3. For each unit, record:
   - SRD section and line range,
   - **Play responsibilities** (see §3),
   - **Primary roles** (GM, player, tutor, content‑author),
   - **Phase** (session zero, character creation, main play loop, advancement, campaign structure),
   - **System level**:
     - `core` (applies broadly across Fate),
     - `system-specific` (e.g., only Fate Condensed),
     - `setting-specific`.

Capture this in a working spreadsheet or YAML index; it will become the **coverage matrix** (§6.1).

### 3. Define skill taxonomy and folder layout

Using the atomic units and tags:

1. Group units into **domains** aligned both with rules and workflows, for example:
   - `table-foundations` (setup, materials, safety, session zero),
   - `character-creation`,
   - `actions-and-outcomes`,
   - `aspects-and-economy`,
   - `challenges-contests-conflicts`,
   - `extras-and-advanced-rules`,
   - `gm-operations`,
   - `setting-tools`,
   - `meta`.
2. For Fate, place skills under:
   - `skills/fate-core/...`
   - `skills/fate-accelerated/...`
   - `skills/fate-condensed/...`
   - `skills/fate-toolkit/...`
   - `skills/fate-worlds/<setting>/...`
3. Use hyphen‑case names that mirror SKILL frontmatter `name`:
   - e.g., `skills/fate-core/character-creation/high-concept-aspects/`
     with `name: fate-core-character-creation-high-concept-aspects`. 【F:reference/anthropic-skills/template-skill/SKILL.md†L1-L6】
4. For setting‑specific SRDs, add **overlays** in sibling folders:
   - e.g., `skills/fate-worlds/frontier-spirit/character-creation/...`
   that extend or override core Fate guidance rather than duplicating it.
5. Reserve lightweight `references/` subfolders **inside** a skill folder when:
   - you need long rule examples,
   - you want catalogs (e.g., sample stunts),
   - you store generators or play aids that are too long for SKILL.md. 【F:reference/anthropic-skills/skill-creator/SKILL.md†L93-L149】

### 4. Design per‑SRD skill plans

For each major SRD, create a **plan document** at repo root, e.g.:

- `fate-core-skills-plan.md`
- `fate-accelerated-skills-plan.md`
- `fate-condensed-skills-plan.md`
- `fate-system-toolkit-skills-plan.md`
- `fate-worlds-<setting>-skills-plan.md`

Each per‑SRD plan should:

- Declare **scope**: which SRD file(s) and systems it covers.
- Declare **goals**: what kinds of play it must support (one‑shots, campaigns, online play, etc.).
- Enumerate **modules** (like “Character Creation,” “Actions & Outcomes,” “GM Ops”), each with:
  - a list of concrete SKILLs (names + suggested folder paths),
  - roles/modes (GM/player/tutor/content‑author; copilot/autopilot/reference),
  - SRD line anchors for each SKILL (or tight ranges).
- Explicitly declare **non‑goals** for that SRD (e.g., “no setting fiction summaries”).

You can use the `fate-condensed-skills-plan.md` as a pattern: it shows how to map one SRD to a full skill inventory with anchors and paths.

### 5. Author SKILL.md per atomic unit (via the per‑SRD plan)

For each skill listed in a per‑SRD plan:

1. Re‑read the relevant SRD section(s) in full.
2. Review **Skill Creator** and **best practices**; make notes on:
   - when the skill should trigger,
   - what inputs it expects (user intent, current game state),
   - what it should produce (rulings, prompts, checklists, content). 【F:reference/anthropic-skills/skill-creator/SKILL.md†L65-L118】【F:reference/claude-docs/agent-skills/best-practices.md†L13-L133】
3. Start from a template SKILL.md that contains:
   - YAML frontmatter:
     - `name` (hyphen‑case, unique),
     - `description` (one‑sentence, discovery‑friendly),
     - optional metadata (see §6.2).
   - Sections:
     - **When to use this skill**
     - **Key concepts**
     - **Step‑by‑step procedure**
     - **Examples**
     - **Pitfalls & edge cases**
     - **Related skills**
4. Keep SKILL.md **concise**:
   - Prefer < ~500 lines where possible.
   - Move heavy content (large tables, long example series, stunt lists) into `references/`, linking explicitly from SKILL.md. 【F:reference/anthropic-skills/skill-creator/SKILL.md†L119-L190】
5. Enforce spec compliance early:
   - SKILL.md must open with valid YAML frontmatter declaring `name` and `description`.
   - Avoid adding separate READMEs; SKILL.md is the single entrypoint. 【F:reference/anthropic-skills/agent_skills_spec.md†L1-L55】

### 6. Validate completeness and responsibility coverage

At the **SRD level** (per‑SRD plan):

- Confirm every heading/subheading in the SRD maps to **at least one SKILL**.
- Confirm every play responsibility in §3 is covered for that SRD where applicable.
- Use a coverage index (see §6.1) to mark:
  - SRD section → SKILL path(s),
  - SKILL path → responsibility tags and roles.

At the **library level** (across all Fate SRDs):

- Confirm there are no major gaps in:
  - table setup & safety,
  - character creation,
  - conflict/scene tools,
  - GM operations,
  - content generation.
- Check for unhealthy duplication:
  - Shared procedures (e.g., the four actions, compels) should live in core/system‑neutral skills where possible, with thin overlays in Condensed/Accelerated/etc.

Add a “spec compliance” column to the coverage index to track that each skill folder:

- Has correct frontmatter,
- Stays reasonably sized,
- Uses references appropriately. 【F:reference/anthropic-skills/skill-creator/SKILL.md†L119-L190】

### 7. Review and iterate

- Peer review SKILLs for:
  - fidelity to SRD rules and intent,
  - clarity and stepwise usability,
  - appropriate tone (collaborative, safety‑aware).
- Test SKILLs using:
  - **Sub‑agents** and the testing patterns from Superpowers (`testing-skills-with-subagents`, etc.) to simulate play situations. 【F:reference/obra-superpowers/skills/testing-skills-with-subagents/SKILL.md†L1-L120】
  - Real or hypothetical play transcripts.
- Ensure license and attribution requirements for Fate SRDs are respected in any generated content skills (you may centralize this in a `fate-srd-licensing` SKILL).

---

## 6. Coverage index and metadata

### 6.1 Coverage index design

Maintain a machine‑readable coverage index (YAML or CSV), with entries like:

```yaml
- srd_file: reference/fate-srd/markdown/fate-core-SRD.md
  section_id: actions-and-outcomes
  section_range: L800-L1025
  skills:
    - path: skills/fate-core/actions-and-outcomes/core-loop/
      name: fate-core-actions-core-loop
  responsibilities: [scene-procedures, rules-tutoring]
  roles: [gm, player, tutor]
  spec_compliant: true
