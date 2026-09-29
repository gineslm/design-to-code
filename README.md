# Design to Code

> **Note:** this repository's documentation and code are written in Spanish. This README is an English summary for readers who don't read Spanish. → [Leer en español](README.es.md)

> Applied research on how to structure AI-agent-assisted processes so they are traceable, reproducible, and sufficiently well-defined before reaching implementation.

This repository started from a concrete question:

> **How much of the work of turning design into code can be delegated to AI agents, and with what guarantees?**

The research began within the flow **documentation → design/prototyping → frontend implementation**, but more general findings emerged during testing: the process's performance depended less on "asking the agent for more" and more on **how the work was defined, chained, and validated**.

That led to two distinct outcomes:

1. a **staged-process methodology**, first formulated from the design-to-code case and later abstracted into a reusable core;
2. a second-order problem — coordinating multiple contexts that don't share memory — which opened its own architectural line of work and later gave rise to **Warp**.

This repository holds the research, the derived methodology, and its application to the design → code process.

---

## 1. The starting question

The initial goal had two fronts:

- assess how much of the design-to-code conversion could be automated;
- study an AI-assisted design and prototyping flow with enough control and fidelity.

The process under study was organized into three layers:

```text
definition
   ↓
design
   ↓
implementation
```

The working hypothesis was that each layer could rely on a different agent, as long as the transitions between them were sufficiently specified.

The research was carried out on a real Angular frontend case, comparing different transfer modes from design tools and running several conversions of the same project.

---

## 2. What was tested

The tests weren't only about checking whether an agent could generate code. They aimed to isolate **which conditions made the process reliable and reproducible**.

### Test A — raw conversion

Direct import of a view to observe what the system produced without a developed methodology around it.

It served as an initial diagnostic.

### Test B — full conversion with accumulated context

The full flow was executed:

```text
styles
→ shared components
→ application shell
→ pages
→ navigation
```

The run reached the intended functional goal and helped consolidate the procedure.

### Test C — replicability without conversation history

The same conversion was run through an agent that only had access to:

- documentation;
- the repository;
- process artifacts.

It did not have access to the conversation history from the previous tests.

This test made it possible to study whether the method could hold up on **persistent artifacts**, rather than depending on conversational memory.

### Test D — blind conversion with the corrected method

After detecting losses of visual fidelity in C, a visual check was added to the procedure and the run was repeated.

The result was especially useful because fidelity **did not improve substantially**.

That ruled out the problem being solely in the final conversion step, and shifted the analysis upstream.

---

## 3. Main finding: definition determines the outcome

The tests pointed to an operational conclusion:

> **improving the conversion alone isn't enough if the specifications reaching implementation are still incomplete.**

The fidelity of the result depended directly on the quality of the upstream artifacts:

- documentation;
- functional definition;
- design specifications;
- contracts between stages;
- component specs.

The bottleneck identified was, therefore, the **specification contract between design and implementation**.

The consequence was significant: the problem stopped being simply "how to generate better code" and became "how to prepare a process so an agent has to interpret as little as possible at each transition."

---

## 4. From tests to a methodology

A set of principles that could be formulated independently of the specific case was extracted from the research.

The core lives in:

[`core/metodologia-global.md`](core/metodologia-global.md)

That document is defined as an **agnostic core for staged transformation processes**. Its degree of universality is explicitly bounded: it stems from a single process and distinguishes between confirmed rules, supported rules, and hypotheses.

The main principles are:

### Traceability

Every result must be traceable back to the decision or source that produced it, and every decision must be traceable forward to where it lands.

### Versioning and lineage

Derived artifacts must make it possible to detect when they've fallen out of sync with their sources.

### Ambiguity reduction

Each phase must make explicit what was implicit, so the downstream actor **interprets less and executes more**.

### Reuse and consistency

Repeated patterns must be defined once and reused, instead of being duplicated and diverging.

### Waterfall with iteration

A phase is validated before building on it, but it can be iterated internally and revisited if new knowledge emerges.

### Retroactivity

Returning to a closed phase is not considered a failure. If a later phase uncovers an upstream problem, it's fixed at the source, logged, and its forward impact is assessed.

### Cumulative enrichment

Each phase adds information without losing what was already established.

### Constant method, variable source

The method must be able to stay stable while the project it's applied to changes.

---

## 5. Gates and human validation

The methodology introduces explicit stopping points.

They don't all have the same scope:

```text
task
  ↓
content stop

phase
  ↓
consolidation gate

layer change
  ↓
reinforced gate
```

The purpose of the gate isn't to add bureaucracy, but to prevent an error or contradiction from silently propagating further.

Human validation is part of the model: closing a phase isn't reduced to a mechanical check, because the content requires judgment.

---

## 6. The methodology applied to the Design to Code flow

The concrete application of the core lives in:

[`core/metodologia-aplicada.md`](core/metodologia-aplicada.md)

The applied methodology organizes the process into three layers with distinct responsibilities.

### Definition

Reasons, documents, and orchestrates.

It's the source of scope and requirement decisions.

### Design

Turns the definition into visual form.

It shouldn't silently introduce new requirements: gaps must be surfaced upward or logged.

### Implementation

Turns design and specifications into code.

Its responsibility is to implement faithfully, not to redefine requirements or design by default.

The governing principle is:

> **decisions must be made where the context to make them exists.**

A lower layer may discover something that forces a higher one to be revisited, but that change must be logged and propagated.

---

## 7. Contracts between layers

Transitions aren't treated as simple file handoffs.

They work as **contracts** that must let the receiver operate without needing the sender's conversation history.

In the current model:

```text
Definition ──briefing──→ Design

Definition ──technical profile──→ Implementation

Design ──handoff──→ Implementation
```

The strong test of sufficiency is:

> **can a receiver with no access to the history execute correctly using only what crosses the boundary?**

That criterion is precisely what motivated the tests with "blind" agents.

---

## 8. Design and specification artifacts

The repository also contains a specific design layer and a family of specs that materialize the design → implementation contract.

Among them:

- `spec-app.md`
- `spec-componente.md`
- `spec-ds.md`
- `spec-entidades.md`
- `spec-navegacion.md`
- `spec-vision-general.md`
- `spec-vista.md`

These specs aren't a decorative catalog: they try to reduce the number of implicit decisions that would otherwise be left to implementation.

The current research points precisely to this boundary as the main area that still needs to mature.

---

## 9. Logging, drift, and failure modes

The methodology identifies three relevant failure modes:

### Smuggling

A decision appears that no stage had authorized.

It may be a legitimate finding, but it must be logged.

### Drift

Something already validated upstream is lost or contradicted.

### Incoherence

Two pieces produced in parallel stop fitting together.

In all three cases, logging is what separates an auditable change from invisible debt.

That's why decisions that emerge during the process shouldn't remain only in a conversation.

---

## 10. Maturity: what we know and what we don't

This repository deliberately distinguishes between:

- **confirmed** — demonstrated by sufficient evidence within the research;
- **supported** — backed by available evidence, but not yet closed;
- **hypothesis** — plausible, pending testing.

Among the current results:

- the agent-assisted flow is viable end to end;
- the tests support that documentation and specification quality directly determines fidelity;
- improving the conversion alone did not resolve the deviations;
- the design → code contract remains the main pending area;
- extrapolating the methodological core to other processes is still a hypothesis, because it has only been tested on a single domain so far.

This repository should be read as **evolving research**, not as a finished standard.

---

## 11. The problem the methodology didn't solve

While the research was developing, a different problem appeared.

The work started to be spread across multiple conversations and tools:

- some researched;
- some ran tests;
- some consolidated methodology;
- some worked on design or implementation.

Those contexts didn't share memory.

The consequence was that project knowledge became scattered and could fall out of sync.

The first attempt to model this problem lives in:

[`core/arquitectura-de-contextos.md`](core/arquitectura-de-contextos.md)

That document is explicitly marked as **exploratory**. It describes an initial mechanism based on:

- bridge documents;
- editing responsibilities;
- states;
- information feedback;
- human synchronization.

It's not part of the mature methodological core.

It was the signal that a problem of a different order had appeared.

---

## 12. This is where Warp was born

The methodology mainly answers:

> **how should an agent-assisted process move forward and be validated?**

The new question was:

> **how do you keep knowledge and responsibility coherent when several instances work on that process without sharing memory?**

That second question was later split off from this repository and evolved into its own architectural research:

**Warp — a knowledge architecture for human–AI collaboration**

Warp develops that problem around ideas such as:

- persistent responsibilities;
- THREADs;
- MANIFESTs;
- HANDOFFs;
- document authority;
- shared corpus;
- interchangeable agents;
- Git as the history of knowledge;
- progressive context loading;
- structural validation.

Design to Code and Warp are therefore related projects, but not equivalent:

```text
Design to Code
→ investigates a process
→ extracts a methodology
→ discovers a coordination problem

Warp
→ takes that problem
→ abstracts it
→ develops a knowledge architecture
```

**Warp repository:** [github.com/gineslm/warp](https://github.com/gineslm/warp)

---

## 13. Repository structure

```text
.
├── core/
│   ├── metodologia-global.md
│   ├── metodologia-aplicada.md
│   ├── arquitectura-de-contextos.md
│   └── convenciones-repo.md
│
├── domain/
│   └── capa-diseno/
│       ├── metodologia-capa-diseno.md
│       ├── fases-proceso-diseno.md
│       └── spec/
│           ├── spec-app.md
│           ├── spec-componente.md
│           ├── spec-ds.md
│           ├── spec-entidades.md
│           ├── spec-navegacion.md
│           ├── spec-vision-general.md
│           └── spec-vista.md
│
├── metodologia-sintesis.md
├── decisiones-consolidacion.md
├── entrada-decisiones-2026-08-06.md
└── CONTEXT_GIT.md
```

The structure reflects three distinct levels:

```text
methodological core
        ↓
process application
        ↓
layer-specific artifacts
```

---

## 14. Status

The research is still ongoing.

The main open lines of work are:

1. improving the specification contract between design and implementation;
2. bringing the definition and design/prototyping layers up to the same level of completeness;
3. continuing to validate which core principles are actually transferable to other processes;
4. progressively separating the context-related architectural problems that already belong to Warp out of this repository;
5. measuring impact on time, cost, consistency, and rework in a real pilot.

---

## Author

**Ginés López Montalbán**

Frontend / UX-UI · Design Systems · AI-assisted processes

---

## Note on scope

This repository documents a research effort and an evolving methodology.

It does not claim to present as universal conclusions that, so far, have only been obtained from a single process, nor does it claim that the current flow removes the need for human judgment.

The goal is to make explicit the decisions, the tests, the limits, and the maturity level of each finding.
