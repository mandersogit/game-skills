# Fate Condensed → Agent Skills Coverage Plan

## Purpose

Convert the **Fate Condensed SRD** into a cohesive bundle of Claude Agent Skills that:

- Let an agent:
  - GM a Fate Condensed game end‑to‑end.
  - Play a Fate Condensed PC.
  - Assist a human GM and/or players with rules, adjudication, and pacing.
  - Assist with content creation (characters, NPCs, situations, threats).
- Are structured as **folders containing `SKILL.md` files** that follow Anthropic’s Agent Skills spec and best practices.

> In this document, **“skill”** always means a **Claude agent skill** (a directory with `SKILL.md`), not an in‑universe Fate character skill like Athletics, Fight, or Rapport.

---

## Audience and tone

- **Learner:** Claude (the agent), who loads these skills dynamically during play or preparation.
- **Human readers:** Fate‑capable GMs/players and contributors authoring or reviewing the skills.

**Tone guidelines:**

- Neutral, supportive facilitator voice.
- Prioritize **procedures, checklists, and decision trees** over lore.
- Assume the human table remains the final authority; the agent offers rules help and suggestions, not mandates.
- Always surface **safety & calibration** hooks when play touches risk, trauma, or boundaries (even if the detailed tools come from other SRDs/toolkits).

---

## Outputs for Fate Condensed

This plan should result in:

1. A set of **skill folders** under `skills/fate-condensed/`, each with a `SKILL.md`.
2. A **coverage index** file (e.g. `skills/fate-condensed/coverage.yaml`) mapping:
   - SRD section(s) → skill folder(s)
   - Skill folder → roles (GM / player / both / author) and phase (prep / in‑play / between sessions / advanced).
3. **Consistent metadata**:
   - `name`: machine‑friendly name (e.g. `fate-condensed-actions-overcome`).
   - `description`: 1–2 line “when to use this skill.”
   - Optional tags in `x-meta` (roles, phase of play, system = `fate-condensed`).
4. Optional helper artifacts:
   - Short reference handouts in `references/` (e.g. four actions cheat sheet, outcome ladder).
   - Example prompts or dialogues that demonstrate intended usage.

---

## Role & phase coverage expectations

Every Fate Condensed rule or procedure should be covered from the perspective of **who is using it and when**:

**Roles:**

- `gm`: Running the world, framing scenes, setting difficulty, running NPCs.
- `player`: Playing a PC, making decisions, invoking/compelling aspects.
- `both`: Shared procedures (dice, outcomes, teamwork) that affect everyone.
- `author`: Content creation and meta‑design (NPCs, situations, threats).

**Phases of play:**

- `prep`: Before a session (session zero, setting, character creation, scenario prep).
- `in-play`: During active scenes and conflicts.
- `between-sessions`: Milestones, advancement, campaign pacing.
- `advanced`: Optional/variant rules, scale, weapons/armor, boss mechanics.

Each skill in the taxonomy below should be tagged with **role(s)** and **phase(s)** in a consistent way (either in the coverage index or in `x-meta` in the frontmatter).

---

## Source anchors in the Fate Condensed SRD

At minimum, skills should draw from:

- **Introduction / What Do I Need to Play? / For Veterans: Changes From Fate Core**
- **Getting Started**
  - Define Your Setting
  - Create Your Characters (Who Are You? Aspects, Skills, Stunts, Stress & Consequences setup)
- **Taking Action, Rolling the Dice**
  - Difficulty and Opposition
  - Modifying the Dice (Invoking Aspects, Using Stunts)
  - Outcomes (Failure, Tie, Success, Success with Style)
- **Aspects and Fate Points** (including guidance referenced from “Aspects and Fate Points” where applicable)
- **Challenges, Conflicts, and Contests**
  - Setting Up Scenes (Zones, Situation Aspects, Turn Order)
  - Teamwork
  - Challenges, Contests (and Creating Advantages in a Contest)
  - Conflicts (Taking Harm, Stress, Consequences, Getting Taken Out, Conceding, Ending a Conflict, Recovering)
- **Advancement**
  - Minor / Major Milestones
  - Sessions and Arcs
- **Being the Game Master**
  - Setting Difficulty and Opposition
  - NPCs (major/minor NPCs, monsters, threats)
  - Your Fate Points (GM fate point economy)
- **Optional / Advanced Sections** (toward the end of the SRD)
  - Full defense and other action variants (if present)
  - Aspects and Scale
  - Time Shifts
  - Ways to Break the Rules for Big Bads
  - Ways to Handle Multiple Targets
  - Weapon and Armor Ratings
  - Any other Fate Condensed‑specific hacks or options.

Exact headings and subheadings should be captured per your local SRD copy; the coverage index is responsible for recording precise sections.

---

## Skill taxonomy for Fate Condensed (proposed)

This taxonomy is designed to achieve near‑100% procedural coverage of Fate Condensed with a manageable number of skills an agent can load and combine.

For each skill below:

- **Folder**: Proposed path under `skills/fate-condensed/`.
- **Role(s)**: `gm`, `player`, `both`, `author`.
- **Phase(s)**: `prep`, `in-play`, `between-sessions`, `advanced`.
- **Purpose**: What the skill enables the agent to do.
- **Key SRD anchors**: Sections/headings to pull from.

---

### A. Foundations & table setup

1. **System overview & materials**

   - **Folder:** `skills/fate-condensed/foundations/system-overview`
   - **Roles:** both
   - **Phases:** prep
   - **Purpose:** Explain what Fate Condensed is, what materials are needed, and what makes it different from Fate Core, at a level an agent can reuse when orienting new players.
   - **Anchors:** Introduction; “What Do I Need to Play?”; “For Veterans: Changes From Fate Core.”

2. **Table calibration & safety**

   - **Folder:** `skills/fate-condensed/foundations/calibration-and-safety`
   - **Roles:** both
   - **Phases:** prep, in-play
   - **Purpose:** Provide scripts and checklists for setting tone, negotiating content boundaries, using the SRD’s “bogus rule” or similar calibration advice, and pausing/rewinding scenes when needed.
   - **Anchors:** Any Fate Condensed text that discusses table expectations, tone, consent, or “bogus rule”–style guidance. (For more detailed safety techniques, this skill can cross‑link to skills built from the Accessibility or Horror Toolkits.)

3. **Session zero & setting definition**

   - **Folder:** `skills/fate-condensed/prep/define-setting`
   - **Roles:** gm, author (players may also use, but GM‑led)
   - **Phases:** prep
   - **Purpose:** Walk a group through collaboratively defining their setting, its core issues, themes, and constraints, turning the SRD’s “Define Your Setting” section into a structured facilitation script.
   - **Anchors:** Getting Started → Define Your Setting.

---

### B. Character creation

4. **Character creation overview**

   - **Folder:** `skills/fate-condensed/character/creation-overview`
   - **Roles:** both
   - **Phases:** prep
   - **Purpose:** Step‑by‑step guide for creating a PC according to Fate Condensed: choose concept, write aspects, pick skills, select stunts, set stress/consequences, etc.
   - **Anchors:** Getting Started → Create Your Characters → Who Are You? (summary of character elements).

5. **Aspects: high concept, trouble, relationships, free aspects**

   - **Folder:** `skills/fate-condensed/character/aspects`
   - **Roles:** both
   - **Phases:** prep, in-play
   - **Purpose:** Help players and GMs write strong aspects for high concept, trouble, relationship, and free slots, including examples, common pitfalls, and how these aspects will be invoked/compelled later.
   - **Anchors:** Create Your Characters → Aspects (High Concept, Trouble, Relationship, Free Aspects); any references to good/bad aspect examples; any cross‑references to Aspects and Fate Points.

6. **Skills and the skill pyramid**

   - **Folder:** `skills/fate-condensed/character/skills-and-pyramid`
   - **Roles:** both
   - **Phases:** prep, between-sessions
   - **Purpose:** Explain the skill list used in Fate Condensed, the adjective ladder, starting skill ratings, skill cap, and pyramid requirements; help players build legal and effective skill spreads.
   - **Anchors:** Create Your Characters → Skills (including Adjective Ladder, Starting Skills, Skill Cap and Pyramid).

7. **Stunts and refresh**

   - **Folder:** `skills/fate-condensed/character/stunts-and-refresh`
   - **Roles:** both
   - **Phases:** prep, in-play, between-sessions
   - **Purpose:** Turn the SRD’s stunt rules into templates and examples, including how to write new stunts, how many stunts PCs start with, refresh tradeoffs, and when stunts apply during play.
   - **Anchors:** Create Your Characters → Stunts; any optional stunt templates or examples referenced earlier in the SRD.

8. **Stress tracks & consequences setup**

   - **Folder:** `skills/fate-condensed/character/stress-and-consequences-setup`
   - **Roles:** both
   - **Phases:** prep
   - **Purpose:** Set initial stress boxes and consequence slots for PCs; explain what they mean, how they’ll be used in conflicts, and how they appear on character sheets.
   - **Anchors:** Create Your Characters → Stress & Consequences (or equivalent); any later recap in conflict sections that describes starting tracks.

---

### C. Aspects & fate point economy in play

9. **Aspect principles & invocation**

   - **Folder:** `skills/fate-condensed/aspects/principles-and-invokes`
   - **Roles:** both
   - **Phases:** in-play
   - **Purpose:** Teach and enforce the core truths about aspects (always true, double‑edged, permission, etc.), how to invoke them, free invokes vs paid invokes, boosts, and how aspects shape the fiction.
   - **Anchors:** Any “Aspects and Fate Points”–style section; Taking Action → Modifying the Dice → Invoking Aspects; examples that show aspects in use.

10. **Compels, self‑compels, and fate point flow**

   - **Folder:** `skills/fate-condensed/aspects/compels-and-economy`
   - **Roles:** both (with GM emphasis)
   - **Phases:** in-play, between-sessions
   - **Purpose:** Provide procedures for offering and negotiating compels, self‑compels, consequences of accepting/refusing, and how fate points circulate to and from the GM; include “bogus rule” or calibration hooks where appropriate.
   - **Anchors:** Fate Point economy sections; any rules text about compels, self‑compels, refusing compels, GM fate points.

---

### D. Dice, actions, and outcomes

11. **Dice, ladder, and outcomes**

   - **Folder:** `skills/fate-condensed/actions/dice-and-outcomes`
   - **Roles:** both
   - **Phases:** in-play
   - **Purpose:** Provide a single, reusable “roll engine” skill: roll 4dF + skill, compare to difficulty/opposition using the ladder, and interpret the four outcomes (Failure, Tie, Success, Success with Style), including “success at cost” variants.
   - **Anchors:** Taking Action, Rolling the Dice; Difficulty and Opposition; Outcomes and all subcases (simple failure, major/minor cost, partial success, etc.).

12. **Overcome**

   - **Folder:** `skills/fate-condensed/actions/overcome`
   - **Roles:** both
   - **Phases:** in-play
   - **Purpose:** Turn the Overcome action into a specific checklist: when to choose Overcome, how to set difficulty, how each outcome maps to fictional results and costs, and how aspects/stunts modify it.
   - **Anchors:** Taking Action → Overcome (if separate) or the general Actions section where Overcome is defined.

13. **Create an Advantage**

   - **Folder:** `skills/fate-condensed/actions/create-advantage`
   - **Roles:** both
   - **Phases:** in-play
   - **Purpose:** Teach the nuances of Create Advantage, including discovering existing aspects vs creating new ones, assigning free invokes, and how success, success with style, and failure all produce different fictional and mechanical results.
   - **Anchors:** Taking Action → Create an Advantage; any notes about discovering unknown aspects; contest‑specific “creating advantages in a contest” section.

14. **Attack**

   - **Folder:** `skills/fate-condensed/actions/attack`
   - **Roles:** both
   - **Phases:** in-play
   - **Purpose:** Advisor for applying the Attack action: what counts as an attack, how to interpret hit/miss, how to convert shifts to stress and consequences, how stunts and aspects modify attacks.
   - **Anchors:** Taking Action → Attack; conflict rules where Attack interacts with stress/consequences.

15. **Defend**

   - **Folder:** `skills/fate-condensed/actions/defend`
   - **Roles:** both
   - **Phases:** in-play
   - **Purpose:** Detail the Defend action: when it applies, how it differs from Overcome or full defense, how outcomes translate into narrative, and how aspects/stunts affect defense.
   - **Anchors:** Taking Action → Defend; any conflict text that describes defending against attacks or advantages.

---

### E. Scenes, zones, and structured situations

16. **Scene framing, zones, and situation aspects**

   - **Folder:** `skills/fate-condensed/scenes/framing-zones-and-situations`
   - **Roles:** gm, author
   - **Phases:** prep, in-play
   - **Purpose:** Convert “Setting Up Scenes” guidance into actionable GM procedures: define zones, place situation aspects, track who is where, decide when movement merits a roll, and render the environment as a set of usable aspects.
   - **Anchors:** Challenges, Conflicts, and Contests → Setting Up Scenes; Zones; Situation Aspects; Turn Order (for initiative).

17. **Teamwork and table tempo**

   - **Folder:** `skills/fate-condensed/scenes/teamwork-and-tempo`
   - **Roles:** both
   - **Phases:** in-play
   - **Purpose:** Formalize teamwork rules (helping, combining skills, sharing free invokes) and provide advice on keeping spotlight and pacing balanced across players.
   - **Anchors:** Teamwork section under Challenges/Conflicts/Contests; any sidebars about turn order and spotlight.

---

### F. Challenges, contests, and conflicts

18. **Challenges and contests**

   - **Folder:** `skills/fate-condensed/structures/challenges-and-contests`
   - **Roles:** gm, both
   - **Phases:** prep, in-play
   - **Purpose:** Provide clear, distinct procedures for running challenges and contests: how to break a situation into steps, how to set up victory conditions, how to handle Create Advantage within contests, and how to convert outcomes to narrative progress.
   - **Anchors:** Challenges section; Contests section; “Creating Advantages in a Contest.”

19. **Conflicts: structure and flow**

   - **Folder:** `skills/fate-condensed/structures/conflicts`
   - **Roles:** gm, both
   - **Phases:** in-play
   - **Purpose:** End‑to‑end conflict loop: set up sides, establish zones and aspects, handle turn order, conduct actions, apply harm, handle concessions and “taken out,” and end the conflict cleanly.
   - **Anchors:** Conflicts section; Turn Order; Taking Harm; Ending a Conflict.

---

### G. Harm, concessions, and recovery

20. **Stress and consequences in play**

   - **Folder:** `skills/fate-condensed/harm/stress-and-consequences-in-play`
   - **Roles:** both
   - **Phases:** in-play
   - **Purpose:** Explain how to mark stress boxes and assign consequences in response to attacks or other harm, how to factor in existing consequences, and how to describe them fictionally.
   - **Anchors:** Taking Harm; Stress; Consequences; any worked examples involving applying harm.

21. **Conceding, being taken out, and recovery**

   - **Folder:** `skills/fate-condensed/harm/conceding-and-recovery`
   - **Roles:** both
   - **Phases:** in-play, between-sessions
   - **Purpose:** Provide rules and scripts for offering/accepting concessions, determining what “taken out” means, and how recovery works between scenes and sessions (including clearing stress and healing consequences).
   - **Anchors:** Getting Taken Out; Conceding; Ending a Conflict; Recovering From Conflicts.

---

### H. Advancement and campaign pacing

22. **Milestones and advancement**

   - **Folder:** `skills/fate-condensed/progression/milestones-and-advancement`
   - **Roles:** both
   - **Phases:** between-sessions
   - **Purpose:** Detail minor vs major milestones, what can change at each (skills, stunts, aspects, stress, etc.), and how to guide players in updating their characters.
   - **Anchors:** Advancement → Minor Milestones; Major Milestones; Improving Skill Ratings.

23. **Sessions and arcs**

   - **Folder:** `skills/fate-condensed/progression/sessions-and-arcs`
   - **Roles:** gm, author
   - **Phases:** prep, between-sessions
   - **Purpose:** Help GMs structure sessions and arcs, tie milestones to story beats, and manage campaign pacing (short arcs vs long campaigns).
   - **Anchors:** Advancement → Sessions and Arcs; any references to arc structure or campaign guidance in GM sections.

---

### I. GM operations and adversaries

24. **Difficulty, opposition, and GM fate points**

   - **Folder:** `skills/fate-condensed/gm/difficulty-and-gm-fate-points`
   - **Roles:** gm
   - **Phases:** prep, in-play
   - **Purpose:** Provide concrete methods for setting difficulty, choosing between static vs active opposition, pricing partial success and success at cost, and managing the GM’s own fate point economy.
   - **Anchors:** Being the Game Master → Setting Difficulty and Opposition; Your Fate Points; any Fate Condensed‑specific notes on opposition building.

25. **NPCs, monsters, and threats**

   - **Folder:** `skills/fate-condensed/gm/npcs-and-threats`
   - **Roles:** gm, author
   - **Phases:** prep, in-play
   - **Purpose:** Turn the NPC creation rules into patterns (major vs minor NPCs, monsters, big bads, other threats), including aspect selection, skill ratings, stunts, and how to represent threats using the Fate “fractal.”
   - **Anchors:** Being the Game Master → NPCs (Major NPCs, Minor NPCs, Monsters/Big Bads/Threats); any references to the Fate fractal.

---

### J. Optional and advanced rules

26. **Full defense and other action variants**

   - **Folder:** `skills/fate-condensed/options/action-variants`
   - **Roles:** both
   - **Phases:** advanced, in-play
   - **Purpose:** Document optional action variants (e.g. full defense) and how they alter the standard action/outcome loop; provide guidance on when and why to use them.
   - **Anchors:** “For Veterans: Changes From Fate Core” (if it describes full defense changes); any dedicated optional rule section on full defense or action variants.

27. **Scale, time shifts, and boss rule‑bending**

   - **Folder:** `skills/fate-condensed/options/scale-time-and-big-bads`
   - **Roles:** gm, author
   - **Phases:** advanced, prep, in-play
   - **Purpose:** Explain and operationalize:
     - Aspects and Scale (how scale modifies actions and advantages).
     - Time Shifts (using shifts to adjust time taken).
     - Ways to Break the Rules for Big Bads (challenge/contest immunity, expendable minion armor, reveal true form, scaling things up, solo bonus, “threat is a map/hive”).
   - **Anchors:** Aspects and Scale; Time Shifts; Ways to Break the Rules for Big Bads and its subheadings.

28. **Weapons and armor ratings, multi‑target rules**

   - **Folder:** `skills/fate-condensed/options/weapons-armor-and-multi-targets`
   - **Roles:** gm, both
   - **Phases:** advanced, in-play
   - **Purpose:** Capture the optional weapon/armor rating rules and “ways to handle multiple targets”, including concrete examples and advice about when to use or skip these options.
   - **Anchors:** Ways to Handle Multiple Targets; Weapon and Armor Ratings.

---

## Process for implementing this plan

When an agent or contributor is tasked with turning Fate Condensed into skills, they should:

1. **Read Fate Condensed SRD in full**
   - Do at least one pass focused on understanding play flow (from “What Do I Need to Play?” through GM sections and optional rules).

2. **Create or update the coverage index**
   - Initialize `skills/fate-condensed/coverage.yaml` (or similar).
   - For each SRD section, record:
     - Section heading.
     - Page/line reference (if helpful).
     - Proposed skill(s) from the taxonomy above.

3. **Confirm role & phase tags for each skill**
   - For every entry in the taxonomy, decide:
     - `roles`: subset of {gm, player, both, author}.
     - `phases`: subset of {prep, in-play, between-sessions, advanced}.

4. **Author `SKILL.md` for each skill**
   - Use the Agent Skills Spec and internal skill‑creator guidance for structure.
   - Each `SKILL.md` should include:
     - YAML frontmatter with `name`, `description`, and optional `x-meta` (roles, phases, system, source = `fate-condensed-srd`).
     - Body sections such as:
       - **When to use this skill**
       - **Inputs** (what the agent needs to know from the conversation)
       - **Procedure / checklist**
       - **Examples** (short dialogues)
       - **Common pitfalls / edge cases**
       - **Related skills** (links to sibling skills in this bundle or to other Fate SRD bundles, such as Fate Core or toolkits).

5. **Test skills in realistic scenarios**
   - Run table‑style prompts:
     - “Help me build a Fate Condensed character.”
     - “GM a short Fate Condensed conflict between X and Y.”
     - “Explain how to handle this attack roll and its consequences.”
   - Verify that Claude:
     - Loads the correct subset of skills.
     - Produces rulings that match the SRD’s intent.
     - Offers calibration and safety hooks when appropriate.

6. **Iterate and refine**
   - Update the coverage index when refactoring or splitting/merging skills.
   - Adjust cross‑links and descriptions so skills compose well and don’t duplicate large blocks of SRD text.

---

## Non‑goals (to avoid regression)

- **Not** building a catalog of Fate character skills (e.g., Athletics, Fight, Rapport) as separate Claude skills. Those are in‑fiction abilities; here we are encoding **procedures and facilitation workflows**.
- **Not** rewriting the Fate Condensed SRD wholesale inside the skills. Skills should reference and summarize, not reproduce long passages verbatim.
- **Not** inventing house rules or unofficial hacks unless they are clearly marked as:
  - Optional, and
  - Traceable to a specific toolkit or non‑Condensed SRD.
- **Not** designing setting‑specific content in this plan. Setting overlays (e.g., Frontier Spirit, Venture City) should live in **separate skills** that extend these Fate Condensed fundamentals.
