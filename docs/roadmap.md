# Faultstack Roadmap

This document tracks the current product direction for `faultstack` at a
gameplay level. It sits above the crate split in
[docs/architecture.md](architecture.md) and the content/teaching note in
[docs/teaching.md](teaching.md).

The short version:

- the player is building and scaling the classical control stack around a
  fault-tolerant quantum computer
- the main gameplay surface is component placement, cable routing, controller
  configuration, and runtime observation
- the main long-term constraints are bandwidth, latency, and feedback
  deadlines

## Product Direction

`faultstack` should feel like a systems architecture game, not a quantum state
simulator and not a generic factory clone.

The strongest player fantasy is:

- bring a fragile quantum control stack online
- route the right information through the right hardware
- diagnose bottlenecks
- unlock better infrastructure
- scale to more demanding fault-tolerant workloads

That means the most important mechanics are:

- routing clarity
- cable throughput
- packet latency
- feedback deadlines
- meaningful hardware unlocks

The game should also teach something real while doing that. The intended
learning spine is documented in [docs/teaching.md](teaching.md).

## Product Direction And Validation Layer

This section is a constraint system for future roadmap decisions. New features
should not only be technically coherent. They should improve player decision
clarity, visible system dynamics, and replay value.

### Core Positioning

Definition:

- `faultstack` is a systems-engineering puzzle game about stabilizing a fragile
  quantum machine under timing, routing, and feedback constraints

Design shift:

- from architecture-driven simulation
- to player-driven problem solving

Question every feature must answer:

- does this improve player decision clarity and satisfaction per minute

### Player Experience Pillars

Immediate fantasy:

- the player is an operator/architect rescuing unstable quantum systems
- the first 5-10 minutes must communicate instability, limited tools, and
  visible improvement from player action

Visible system dynamics:

- hidden complexity should become observable signals:
  packet flow, congestion buildup, missed deadlines, unstable regions, and
  overload propagation
- failure must be localizable, interpretable, and attributable to a player
  decision
- the main board should communicate failure before the player needs to read a
  long debrief
- the player should be able to answer "what failed?" quickly, not only after
  panel-diving

Decision density:

- each mission should force meaningful tradeoffs:
  latency vs cost, routing simplicity vs robustness, centralization vs
  distribution
- avoid passive simulation; maintain regular decision pressure
- early missions can still use short observe-understand-adjust loops instead of
  constant crisis

Replay value:

- missions should support optimization goals such as throughput, latency
  margin, cost, board cleanliness, or solution complexity
- success should encourage "one more run to improve it", not only
  "I have seen this once"

### Scope Control

Preserve the abstraction boundary:

- keep packets, routing, timing, queueing, syndrome/decoder/correction loops
- avoid full quantum state simulation and amplitude-level realism

Challenge structure:

- prefer tight authored challenges over broad open-ended sandbox scope
- delay blank-board sandbox and procedural generation until authored mission
  quality is already strong
- keep seeded lab templates as the safe experimentation layer for now

### Vertical Slice Gate

Before committing to a larger release push, `faultstack` should prove one
minimal but complete player-facing slice.

Must include:

1. clear visual board language
2. one onboarding mission with guided teaching
3. one intermediate mission with congestion and feedback pressure
4. a debrief that explains outcome and next improvement angle
5. at least one real replay incentive

Validation criteria:

- the player understands the goal without outside explanation
- the player can identify why failure occurred
- the player voluntarily retries to improve the result

### UX Priorities

- make bottlenecks, deadline violations, and overload propagation obvious
- reduce terminology friction in the early game
- introduce concepts through interaction before heavy prose
- keep gameplay readable from short clips; the system should be watchable
- preserve domain identity while simplifying presentation

### Product Risks

Primary risk:

- over-indexing on technical authenticity while under-serving accessibility,
  readability, and fun

Mitigation:

- prioritize clarity over completeness
- prioritize interaction over explanation
- prioritize feedback over realism where the player-facing result is stronger

### Steam Go / No-Go Criteria

Do not commit to a bigger release scope unless these are true:

- the 10-minute hook works and reaches meaningful success/failure quickly
- at least one mission is intrinsically fun, not only interesting
- gameplay is visually interpretable to an external observer
- players naturally seek optimization and replay

### External Framing

Pitch direction:

- "stabilize a failing quantum system under real engineering constraints"

Avoid leading with:

- "learn quantum error correction"
- "simulate quantum computers"

### Content Authoring Rule

Each authored mission should explicitly declare:

- what pressure it introduces
- what signal exposes failure
- what decision space remains open to the player
- what optimization axis makes replay worthwhile

Guiding principle:

- build a game where understanding emerges from interaction, not instruction

## Teaching Goals

`faultstack` should teach three things at the same time:

- system-level reasoning
- quantum hardware and architecture depth
- performance and scaling intuition

Those are product goals, not optional flavor.

The target feeling is:

- "I understand why this architecture works."
- "I understand why this architecture fails."
- "I understand what changed when the system scaled up."

## Core Loop

The intended core loop is:

1. Enter the campus map and check the recommended next action.
2. Use `Workbench`, `Supply Depot`, `Research Center`, `Mission Control`, or
   `Systems Lab` depending on what the career state is asking for.
3. Launch a mission or seeded lab template.
4. Place the required control-stack components.
5. Route cables between compatible ports.
6. Configure roles and supporting hardware.
7. Bring the QPU online.
8. Observe packet flow, bottlenecks, and failures.
9. Rebuild or upgrade the stack.
10. Complete the run, earn credits/research when applicable, and unlock new
    capability.

## Progression Principles

Every unlock should solve a problem the player already felt.

Good examples:

- the player hits cable congestion, then unlocks a wider cable
- the player misses correction deadlines, then unlocks a faster cable
- the player struggles with syndrome feedback, then unlocks a decoder or
  better controller

Avoid unlocks that are only cosmetic or redundant.

## Current State

The current mission rack is split into optional `Training` and main-path
`Contracts`.

Training:

- `workbench-place-component`
- `workbench-route-cable`
- `workbench-configure-component`
- `workbench-commission-syndrome-fpga`
- `qpu1q-bringup`

Contracts:

- `qpu1q-readout`
- `qpu-rep3x-syndrome`
- `qpu-rep3x-congestion`

Current reality:

- all three first-wave contracts can be completed
- the Macroquad UI now starts in a `Campus Map` instead of a mission pop-up
- the player-facing shell now has six buildings:
  `Mission Control`, `Research Center`, `Supply Depot`, `Systems Lab`,
  `QPU Lab`, and `Workbench`
- `Mission Control` is now the single mission browser for lessons, tutorials,
  and contracts
- `Systems Lab` is now the persistent shared floor workspace used to complete
  accepted missions
- `QPU Lab` is now the persistent shared package-design workspace used to edit
  saved QPU layouts
- `Workbench` is no longer the main lesson surface; it is now a placeholder
  building for later calibration/build workflows
- `CareerState` now owns long-lived credits, research, split system/QPU/package
  inventory, accepted/tracked mission state, persistent workspace state,
  building access, recommended-next action, autosave persistence, and
  persistent stretch-goal progress
- accepted missions now grant temporary system/QPU/package inventory through a
  derived availability layer, and the player can accept many missions while
  tracking one at a time through the shared lab workspaces
- saved QPU package designs are now cloned onto placed floor QPUs instead of
  being edited only on already-placed instances
- `Research Center` now unlocks after the first clear of `qpu1q-readout`
  and gates the rep3 and congestion ladder through explicit projects
- mission acceptance no longer rewrites the persistent `Systems Lab` or saved
  QPU design workspace
- authored Systems/QPU scaffolds can now be loaded explicitly and are filtered
  by the player's current available inventory instead of being silently seeded
  onto the workspace
- mission completion now routes through explicit `play -> debrief -> back to
  campus` flow
- visible stretch goals and mastery tracking now exist, without extra economy
  rewards yet
- first-clear contract rewards now include research, replay rewards now exist,
  and owned hardware is persistent and reusable across runs because the shared
  lab is now the main campaign surface
- contract missions now support layered hints instead of relying only on fully
  guided steps
- `Basic Cable` and `Wide Cable` now diverge mechanically in
  `qpu-rep3x-congestion`
- repetition-code QPUs now expose a dedicated `QPU View` with ancilla round
  history, decoder state, correction state, accepted/missed counters, and a
  selected-round detail pane with trace timing
- `QPU_Rep3_X` now emits real round-by-round ancilla parity metadata for the
  current hybrid repetition-code loop
- rep3 runtime traces now carry stable round ids plus emitted/deadline/
  resolved timing, and the ops/UI layers derive latency benchmarks from that
  single trace path
- `qpu-rep3x-syndrome` and `qpu-rep3x-congestion` now use worst accepted
  correction latency as the primary optional optimization metric instead of
  board-edit counts
- authored repetition-code QPUs now carry a bounded interior draft with fixed
  wall ports, semantic rep3 markers, editable macro-components, and editable
  local cables
- `QPU_Rep3_X` now supports a real inner macro-board: fixed boundary ports
  owned by the shell profile, plus player-authored local architecture inside
  the shell
- the rep3 interior editor now reuses the same placement/routing engine as the
  main board instead of acting like a detached mini-game
- `QPU Macro-Architecture I` now exists as a research beat after congestion
  and unlocks editable rep3 interiors, rep3 macro-block missions, and the
  first rep3 interior lab template
- the mission catalog now includes `Workbench: Rep3 Interior Bring-Up`,
  `QPU Rep3 X Interior Retrofit`, and `QPU Rep3 X Interior Pressure`
- the first syndrome-FPGA commissioning lesson now exists as optional training
  with a dedicated constrained decoder panel instead of narrow inspector
  row-cyclers
- syndrome-FPGA rep3 mappings now propagate into runtime packet metadata and
  change live correction outcomes in the rep3 loop
- authored cable waypoints now persist in `BoardDraft` instead of existing only
  in the UI route tool
- a first `EditorBoard` ECS projection now exists over `BoardDraft` for future
  editor work
- direct mission selection still exists through debug and CLI paths for
  testing
- the palette now uses expandable sections with cable routing surfaced near the
  top
- wheel zoom, middle-mouse pan, drag ghost previews, and drag-move are
  available in the board view
- moving a component now attempts to reroute attached cables from stored
  waypoint intent instead of always dropping them
- persistent lab sessions now fail closed when the live board exceeds derived
  inventory availability after loaned mission equipment is removed

The main remaining design gap is not basic content coverage. It is that the
game still teaches by explicit instruction more than it challenges by systems
pressure.

The main product priority should now shift toward content and gameplay. Editor
and UX work should continue only when they directly unlock better missions,
clearer failure signals, or faster content iteration.

## Current Priorities

### 1. Turn the teaching pillars into content

The next missions should explicitly reinforce the three core teaching goals:

- system-level reasoning through diagnosis, bottlenecks, and tradeoffs
- quantum architecture depth through believable control-stack roles and data
  paths
- scaling intuition through distance, traffic, contention, and deadlines

That means content should be authored around "what the player should
understand after this mission", not just "what the player should build".

### 2. Turn tutorials into problem-solving missions

The next step is to stop telling the player exactly what to do.

The game gets more interesting when missions shift from:

- "place this part, then connect this cable"

to:

- "make this control stack work under these constraints"

That means:

- fewer exact build instructions after the first mission
- more outcome-based objectives
- more room for multiple valid layouts
- more diagnosis and iteration after first contact with failure

### 3. Make cable and timing pressure visibly real

Bandwidth and latency are now mechanically present enough to support a first
real congestion mission. The next job is to make that pressure more legible and
more common across authored problems.

The cable system is now split into:

- cable content/spec under `crates/faultstack-ops/src/components/cables`
- routing and compilation under `crates/faultstack-ops/src/routing`

That should now be turned into gameplay:

- `Basic Cable`
- `Wide Cable`
- later `Fast Cable`, `Cryo Cable`, or other specialized lines

Immediate follow-up:

- surface blocked outputs, queue depth, and missed-deadline causes more clearly
  in inspection/UI
- create more boards where transport choice changes runtime behavior in an
  obvious way
- add challenge from congestion, route length, and deadline pressure without
  relying on exact instructions

### 4. Start building toward deeper QEC teaching

The error-correction side is the most promising place to add real educational
depth without turning the game into an expensive physics simulator.

The intended approach is:

- do not simulate full quantum amplitudes or device physics
- do simulate error processes, syndrome generation, decoding, timing, and
  architectural constraints
- treat error correction as an operational system the player can diagnose and
  design around

Immediate follow-up:

- make the syndrome -> decoder -> correction loop more explicit in content and
  UI language
- build on the dedicated `QPU View` until ancilla parity, round history, and
  inner-architecture state are visually legible in repetition-code missions
- keep the classical decoder behavior fixed-function and the syndrome-FPGA
  surface constrained so the live loop stays legible while the teaching layer
  settles
- build on the new commissioning training lesson until the parity-to-decision
  mapping feels legible and worth using in later live contracts
- move next toward player-arranged processing logic through a constrained
  decoder panel, not a detached abstract mini-game
- teach logical-vs-physical reasoning through missions, not just prose
- add code-distance, decoder-quality, and repeated-cycle ideas incrementally
- add controller-side frame tracking only after ancilla and decoder behavior
  are already visually legible
- keep the abstraction cheap enough that gameplay stays fast and legible

### 5. Build a stronger visual language for hardware

The board should communicate what parts do before the player reads labels or
opens the inspector.

Direction:

- components should get semantic micro-diagrams on their bodies, not just text
- QPUs and logical blocks should advertise their internal structure at a glance
- cables and ports should visually reinforce role and capacity differences
- detail should scale by layer:
  - board view: semantic thumbnail
  - selection/hover: clearer expanded legend
  - QPU/interior view: fuller schematic

Near-term examples:

- a `Rep3 Logical Block` should read as a protected object, not a generic box
- a syndrome FPGA should visually read as `parity bits in -> decision out`
- wide cables should be visibly distinct from basic cables without relying on
  labels
- the `QPU View` should inherit the same visual language as the board

### 6. Add challenge through authored constraints, not content sprawl

The game does not need many more components yet. It needs better authored
problems.

The next mission constraints should come from:

- tighter board footprints
- route detours and corridor contention
- component budgets
- cable-type restrictions
- deadline-sensitive correction paths
- optional efficiency targets

### 7. Improve board editing ergonomics and UI layout

The first UX pass landed. The next one should make editing more reliable
instead of just more convenient.

Already landed:

- zoom the board camera with the mouse wheel
- pan the board with middle-mouse drag
- drag placed components with the mouse instead of forcing remove-and-replace
- show a ghost preview for drag placement and move validity
- reroute attached cables on move using stored waypoint intent
- move mission selection into a separate interface window so the palette has
  more room
- make the palette use expandable categories instead of one long flat list
- pin cable kinds near the top of the palette so route-building tools are easy
  to reach

Immediate follow-up:

- route more live editor interaction through `EditorBoard`
- make partial reroute loss clearer when a moved component forces cable removal
- expand board-editing feedback around invalid drops and reroute failures
- keep editor work tightly tied to better mission authoring and lower UI
  friction

Design goal:

- faster iteration while testing missions
- less UI friction during routing-heavy boards
- more board space and palette clarity as the component list grows

### 7. Introduce a separate editor ECS world

The first step is now in place: `faultstack-ops` has an `EditorBoard`
projection backed by a separate ECS world that roundtrips to `BoardDraft`.
Editor interaction still mostly runs through `TutorialSession`, so the next
work is integration rather than invention.

The intended direction is:

- keep `BoardDraft` as the canonical authored and serialized board format
- use a separate editor ECS world for live editing state
- keep the sim runtime in its own ECS world

That editor ECS world should own:

- selection, hover, and drag state
- placed component instances during editing
- cable instances during editing
- change propagation such as "component moved" and "cable dirty"
- auto-reroute, overlap validation, and preview rebuild triggers

It should not replace:

- mission definitions and catalog data
- progression state
- the persistent/authored board format
- the packet sim runtime

Design goal:

- get ECS benefits for editor interactions and change propagation
- avoid polluting sim runtime with editor concerns
- preserve a stable authored format for missions, save/load, and diffs

### 8. Reshape the player-facing UI into clear screens

The game should feel like a polished game client, not a development shell with
all information shown at once.

The intended screen structure is:

- `Main Menu`
  - `Continue`
  - `New Campaign`
  - `Training`
  - `Settings`
  - later `Profile` / save-slot work if it ever matters
- `Campus Map`
  - six buildings visible from day one
  - one recommended-next banner
  - building lock/open state shown clearly
- `Mission Control`
  - lessons, tutorials, and contracts in one mission browser
- `Supply Depot`
  - store cards with price, owned count, blockers, and recommendation flags
- `Research Center`
  - linear research ladder with costs, blockers, and unlock bundles
- `Systems Lab`
  - persistent shared floor workspace using owned system inventory plus saved
    QPU packages
- `QPU Lab`
  - persistent QPU package editor using owned QPU macro-components
- `Workbench`
  - future calibration/build shell, not the primary lesson browser
- `In Mission`
  - slim top HUD
  - left build/palette rail
  - center board view
  - right inspector tabs
  - bottom strip for runtime events and later `QEC tracking`
- `Debrief`
  - success/fail
  - reward/unlock delta
  - stretch progress
  - `Replay` / `Back to Hub`

Design rules:

- each screen should have one clear primary action
- mission cards should summarize, not explain
- detailed text belongs in a selected detail pane or briefing view
- the board should remain the dominant surface during play
- runtime/QEC history should have a stable home instead of being squeezed into
  whichever panel currently has space

UI slice status:

- `Campus Map v1`
  - landed: six-building campus shell, typed building access, Mission Control
    mission browser, persistent Systems/QPU labs, and autosave-backed career
    state
- `Mission HUD v2`
  - next: slimmer top bar, stronger runtime signal, and a reserved bottom strip
    for runtime and QEC history

## Challenge Principles

To make missions more challenging and interesting, prefer these patterns:

- ask for an outcome, not a checklist
- leave at least one meaningful routing or placement decision to the player
- let the player fail for a readable reason
- make the bottleneck visible in the board and inspector
- reward cleaner or cheaper solutions with optional stretch goals

Good examples:

- "deliver eight readout packets using at most one `Wide Cable`"
- "keep correction misses at zero with a long return path"
- "fit the full readout chain inside this narrow board region"
- "stabilize the QPU while two hot lanes share one corridor"

Avoid:

- exact placement chores after the player already learned the mechanic
- adding new parts before current parts create interesting tradeoffs
- fake challenge from hidden rules or arbitrary restrictions

## Content Principles

Every main-path mission should answer five questions:

- what concept is this mission teaching
- what system pressure makes that concept matter
- what visible failure tells the player they are wrong
- what degrees of freedom the player still has
- what short debrief the player should leave with

Good debriefs are conceptual:

- "Readout is its own data path."
- "The decoder return path is part of a live loop."
- "At larger scale, traffic layout matters more than just having the right
  parts."

Avoid:

- missions that only introduce a new component without a new systems lesson
- missions that teach by hidden author intent instead of readable failure
- missions that scale up size without changing what the player is forced to
  reason about

## Future Hardware Track

The first versions should stay architecture-first and hardware-agnostic enough
to keep the core lessons clean.

Later, `faultstack` can expand into hardware-family-specific add-ons:

- cryogenic superconducting systems
- trapped-ion systems
- neutral-atom systems
- photonic systems

Those tracks can introduce more concrete hardware nouns and routing artifacts:

- amplifier lines, attenuators, splitters, circulators
- lasers, tweezers, avalanche photodiodes, detectors
- optical routing and loss-oriented components

The rule for that future expansion is:

- only add hardware-family-specific details when they create new systems
  reasoning
- do not add them just because the nouns are interesting
- keep the main path understandable before branching into specialized stacks

## Roadmap

### Now

Move from guided onboarding into first real puzzle missions.

Focus:

- keep all current missions manually selectable during testing
- preserve the current tutorial spine as teachable entry content
- reduce instruction density in later missions
- author future missions around explicit learning outcomes from
  `docs/teaching.md`
- add outcome-driven objectives and smaller authored constraints
- make the QEC loop teachable as a system, not just as mission flavor
- make failure causes understandable from runtime signals and inspection
- improve inspection around congestion and blocked outputs
- only take editor/runtime work that directly unlocks better content or clearer
  teaching

Target player feeling:

- "I see why this board is failing."
- "I have at least two ways to fix it."
- "The better cable or layout actually matters."

### Next

Deepen the main systems axis: bandwidth and latency.

Focus:

- build more than one mission around the now-real `Basic Cable` vs `Wide Cable`
  runtime distinction
- create more deadline-driven correction and contention missions
- build missions that teach architecture and scaling, not just new mechanics
- add richer QEC ideas at the Pauli/syndrome/decoder level without jumping to
  full quantum-state simulation
- make congestion sources obvious enough that the player can diagnose them
  without tutorial hints
- add supporting components only when they sharpen those constraints

Likely additions:

- `Fast Cable`
- a simple prioritization or buffering component
- optional mission medals or secondary objectives

### Selected Next Slice

Turn the new rep3 macro-board into a longer campaign-quality architecture arc.

Focus:

- keep `qpu1q-readout` as the first contract the player is expected to solve
- keep the hybrid `QEC tracking` layer and dedicated `QPU View` as the visible
  foundation
- treat the editable rep3 interior as a second constrained board, not a blank
  sandbox or microscopic qubit editor
- build authored missions where the outer board can be correct while the run
  still fails because the inner QPU architecture is incomplete or poorly laid
  out
- keep the shell boundary and wall ports fixed by QPU type so the player learns
  system decomposition instead of editing raw physics primitives
- use only complete macro-components inside the QPU:
  `Rep3Register`, `SyndromeTap`, `CorrectionInjector`, `ReadoutInterface`, and
  `ControlGateway`
- make the right-side `QPU View` explain local readiness, missing paths, and
  selected macro-block role clearly enough that the player can debug the inner
  board without prose-heavy tutorials
- expand the rep3 mission chain through authored constraints:
  limited interior space, partial authored shells, edit budgets, and stronger
  interaction between inner-path quality and outer routing pressure
- keep other QPU families authored-only until rep3 proves fun as a buildable
  macro-board

Success criteria:

- the player can understand the rep3 shell boundary, fixed ports, and editable
  macro-blocks at a glance
- a run can fail for a clearly visible local-architecture reason, not only for
  outer transport failure
- the inner board feels like real hardware architecture work rather than a
  detached puzzle layer
- the rep3 content arc becomes longer and more replayable without adding
  microscopic physics editing

### Later

Scale from one-QPU bring-up into larger fault-tolerance architecture.

Focus:

- less scaffolded repetition-code mission chains
- denser boards
- competing readout, syndrome, and correction traffic
- mixed objective boards with throughput and timing pressure at once
- larger patches

Target player feeling:

- “I’m designing a real control stack now.”

### Not Yet

Do not prioritize these until the main progression loop feels strong:

- blank-board sandbox
- branching tech tree complexity
- many tiny cable variants
- too many new components at once
- save-slot or profile-management UI beyond practical dev needs

## Early Progression Arc

### Campus Onboarding

Missions:

- `workbench-place-component`
- `workbench-route-cable`
- `workbench-configure-component`
- `workbench-commission-syndrome-fpga`
- `qpu1q-bringup`

Teaches:

- component placement
- port-to-port routing
- FPGA role configuration
- one-QPU bring-up and readiness

Rule:

- the first three `Workbench` lessons now gate the early campus loop on
  purpose so owned hardware and building access stay legible
- later `Workbench` lessons should remain optional or recommended rather than
  becoming a second mandatory track

Campus beats:

- `Supply Depot` first teaches owned hardware through `Basic Cable Kit` and
  `FPGA Chassis`
- `Systems Lab` unlocks after `workbench-configure-component`
- `Mission Control` then points at `qpu1q-readout`
- `Research Center` unlocks after the first clear of `qpu1q-readout`
- `Rep3 Foundation` then unlocks the rep3 lesson/contract/lab slice

### Contract Tier 1: Readout

Mission:

- `qpu1q-readout`

Teaches:

- ADC/readout chain
- downstream draining
- longer cable planning

Unlock direction:

- improved transport, starting with `Wide Cable`

### Contract Tier 2: Feedback

Mission:

- `qpu-rep3x-syndrome`

Teaches:

- syndrome extraction
- ancilla parity checks as live signals
- decode loop closure
- correction return path
- first latency benchmark on a live correction loop

Unlock direction:

- larger correction-driven systems

### Contract Tier 3: Congestion

Current dev mission:

- `qpu-rep3x-congestion`

Teaches:

- a long correction return can fail under `Basic Cable` and stabilize under
  `Wide Cable`
- worst-case accepted correction latency is the optimization target, not just
  binary mission completion

Follow-up target:

- build more contracts where throughput and latency pressure decide the outcome
  without relying on explicit cable instructions

### Research Beat: QPU Macro-Architecture I

Unlocks:

- editable rep3 QPU interiors with fixed shell wall ports
- rep3 macro-component palette
- `Workbench: Rep3 Interior Bring-Up`
- `QPU Rep3 X Interior Retrofit`
- `QPU Rep3 X Interior Pressure`
- `Rep3 Interior Bench`

Teaching goal:

- the player learns that the outer control stack and the inner logical-machine
  architecture are separate but connected design problems

### Contract Tier 4: QPU Interior Architecture

Missions:

- `workbench-rep3-interior-bringup`
- `qpu-rep3x-interior-retrofit`
- `qpu-rep3x-interior-pressure`

Teaches:

- fixed shell boundaries versus editable local architecture
- local readiness through required inner paths
- macro-block role placement and routing inside a constrained QPU
- failure attribution when the outer board is healthy but the inner QPU is not

### Contract Tier 5: Timing

Target mission type:

- a board where corrections fail because routes are too slow or too indirect

Teaches:

- latency as a hard design constraint
- later, why frame tracking can sometimes beat a slow physical correction path

## Architectural Rule

Keep the current split:

- `faultstack-sim` executes packets generically
- `faultstack-ops` owns domain logic, content, board state, and progression
- `faultstack-ui` renders and dispatches interaction

For editor architecture specifically:

- `BoardDraft` remains the canonical authored representation
- a separate editor ECS world should become the live mutable editing model
- editor ECS should mirror or project board data during editing, not replace
  the durable format
- preview/runtime builds should compile from editor state back into the normal
  ops/sim pipeline
- stable authored ids should remain distinct from ECS entity ids

For progression work specifically:

- mission unlocks and credits belong in `faultstack-ops`
- UI should only render the current progression state
- cable types should stay split between `components/cables` and `routing`

## Immediate Next Steps

1. Expand the rep3 macro-board content arc so `QPU Macro-Architecture I` feels
   like a real ladder, not a single unlock beat.
2. Add stronger debrief attribution for local-QPU failures so the player sees
   `invalid inner architecture` as distinct from `bad outer routing`.
3. Author more contracts where the outer board is mostly solved and the main
   challenge is repairing or optimizing the inner rep3 architecture.
4. Add replay incentives to the new interior missions:
   footprint, edit count, cable budget, and zero-missed variants.
5. Add another live contract where inner-board quality and outer return-path
   congestion interact in the same run.
6. Keep other QPU families read-only until the rep3 macro-board loop proves
   fun, legible, and worth optimizing.
7. Later, revisit richer constrained decoder logic once the macro-board and
   current commissioning chain feel strong together.
