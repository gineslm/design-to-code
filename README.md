# Design to Code

A methodology for working with AI agents in staged processes, developed from hands-on research into how to take a digital product from its definition all the way to code.

> This README is also available in Spanish → [Leer en español](README.es.md)

---

## 1. What this repository is

This repository contains a **methodology**: a set of principles, rules and templates for organizing a process in which AI agents take part, so that the result is faithful to what was asked for, reproducible and traceable.

The methodology grew out of a specific case, the **definition → design → implementation** path of a web application, and it is written at two levels:

- a **universal core** (tier 1), valid for any AI-assisted process, regardless of the tool or the project;
- its **application to this process** (tier 2): the three layers, how work is handed over between them and, in more detail, the design layer and its specification system.

What the repository does **not** contain is data from a specific project (what the methodology calls tier 3), application code or tools. It is the method a project adopts, not a project.

**Where to start.** If you're after the general idea, this README is enough. If you want the method, read [`core/metodologia-global.md`](core/metodologia-global.md) first and then [`core/metodologia-aplicada.md`](core/metodologia-aplicada.md). If you're going to apply it to the design layer, continue with [`domain/capa-diseno/`](domain/capa-diseno/). The methodology documents are written in Spanish.

---

## 2. What we set out to find

The research started from a practical question: **how much of the work of turning a design into code can be delegated to AI agents, and with what guarantees?**

To answer it, we studied a complete process in three layers:

- **Definition**: what gets built and under what constraints (requirements, entities, user stories, technical profile).
- **Design**: the visual form (design system, wireframes, components, views and a navigable prototype).
- **Implementation**: the code.

The working hypothesis was that each layer could rely on a different agent, as long as the step from one layer to the next was well specified. The case study was a real frontend application in Angular, built with AI-assisted design and coding tools.

---

## 3. How it was evaluated

The tests weren't meant to check whether an agent can generate code, but to isolate **which conditions make the process reliable**. Each one changed one variable compared with the previous one.

- **Test A: raw conversion.** A view was imported directly from the design tool, with no method around it, to see what the system produced on its own. It served as an initial diagnosis.
- **Test B: full conversion with accumulated context.** The whole flow (styles, shared components, application structure, pages and navigation) was run with an agent that had the entire history of previous work in front of it. It reached the functional goal and helped consolidate the procedure.
- **Test C: blind conversion.** The same conversion, but with an agent **without access to the history**: it only had the method documentation, the repository and the package delivered by the design layer. This is what the methodology calls working in a **clean context**, and it is the decisive test: if the method works, it has to work with what is written down, not with what the agent remembers from earlier conversations.
- **Test D: blind conversion with the corrected method.** After the results of C, a visual check was added to the conversion procedure and the exercise was repeated.

---

## 4. What we found

**The method works when it forces the agent not to improvise.** In the blind conversion, the agent didn't fill the gaps on its own: it logged each one and asked about it. Whatever was written explicitly in the design (copy, accessibility attributes, formats, behavior) reached the code with high fidelity.

**Green tests don't guarantee fidelity.** In C, all verification consisted of building and passing tests; the agent never opened a browser. The tests checked text and behavior, not appearance, and gave a false sense of correctness. Of twelve visual deviations, ten were things that **were in the design and weren't carried over**. The methodology captures this lesson as the difference between **verifying** (checking mechanically) and **validating** (judging whether the result is the right one).

**What doesn't travel in the package doesn't exist for the agent.** There was a rule to check interface changes in the browser, but it lived in the user's general configuration, not in the documents the agent received. An agent in a clean context only applies what is written in what it's given.

**Failures originate upstream and show up downstream.** The white background that came out of the conversion wasn't an implementation error: the specification declared a surface color different from the one the prototype used. Likewise, the selector that the agent built with the wrong component wasn't typed in the specification, which left it as "pending". Comparing B, C and the prototype confirmed it: **neither conversion reproduced the prototype**, and each gained and lost fidelity in different places. The problem lay in the process, not in the blind mode.

**AI-generated design covers the happy path well and leaves edge states incomplete**: loading, empty, error and validation states were only half defined, even though the briefing required them.

**Improving the conversion isn't enough.** Test D added a visual check to implementation and fidelity didn't improve substantially. That ruled out the last stretch as the source of the problem and moved the analysis to what reaches that stretch.

All the tests point to the same conclusion: **the implementing agent can only be faithful to what it receives in writing**. Whatever the hand-over leaves open, the agent resolves silently and its own way. The weak point of the process was the **specification contract between design and implementation**.

---

## 5. The solution: specs as the contract between design and implementation

The answer the research arrived at is to **move all the knowledge implementation needs into specification templates (specs)**, instead of leaving it scattered across the definition, the research, the prototype and the design conversations.

Specs are filled in during the design layer. They gather what comes from the definition (the data model, the requirements, the technical constraints) and what is decided while designing (components, states, tokens, navigation), and they leave it **settled and written down**. The package delivered to implementation (the *handoff*) carries them in full. That way, the implementing agent receives everything it needs to **implement without interpreting**: decisions are made upstream, where there is context to make them well, and not by default during conversion.

The system has seven documents, in [`domain/capa-diseno/spec/`](domain/capa-diseno/spec/):

| Spec | What it captures |
|---|---|
| [`spec-app`](domain/capa-diseno/spec/spec-app.md) | Global application requirements: list of components, file structure, decisions shared between design and engineering (e.g. breakpoints), global rules. |
| [`spec-ds`](domain/capa-diseno/spec/spec-ds.md) | What the design system must expose: tokens in two layers (raw primitive values and semantic usage names) and their minimum scope. |
| [`spec-navegacion`](domain/capa-diseno/spec/spec-navegacion.md) | Screens and transitions (origin → action → destination). It is the basis for routing. |
| [`spec-entidades`](domain/capa-diseno/spec/spec-entidades.md) | The data model. It originates in the definition layer and is recorded here so views and components can reference it. |
| [`spec-vista`](domain/capa-diseno/spec/spec-vista.md) | Each screen: which components make it up, layout and responsiveness, states, navigation, behavior and data. |
| [`spec-componente`](domain/capa-diseno/spec/spec-componente.md) | Each reusable piece: the native component it maps to, properties, drawn states, tokens, behavior and accessibility. |
| [`spec-vision-general`](domain/capa-diseno/spec/spec-vision-general.md) | The index that connects the others and sets the acceptance criterion for the whole set. |

Specs **nest** from global to atomic (application → views → components → design system), and each level references the one below without repeating it. Some are **molds** filled in once per item (each component, each view); others are **requirement sheets** that set a rule for the whole application.

Three rules make them effective:

- **They're filled in after high fidelity.** A component's sheet is completed once its states are already drawn, so it records real values and nothing is left "pending".
- **No view uses components without a sheet.** That way no unspecified piece reaches implementation.
- **Components consume only semantic tokens.** Never raw values, which makes it possible to change the theme or brand without touching the components.

The selector case shows the effect. While the specification left it open, the conversion had to choose a component and chose wrong. As soon as the sheet declared the native component read from the prototype, the decision disappeared from implementation: there was nothing left to interpret. Because the sheet describes each component by its function, its states and its tokens, and declares which native component it maps to, it can be carried over to different frameworks without implementation having to reinvent it.

**Acceptance criterion:** with all seven specs complete, someone who has seen none of the design work has everything they need to translate it into code.

---

## 6. The methodology behind it

Specs work because they're part of a method that decides when they're filled in, who validates, and what happens when something doesn't fit. That method lives in [`core/`](core/).

**The starting point.** An agent works only with the information it receives, and **it resolves on its own, without warning, any ambiguity that information leaves open**. So the strategy isn't to cut stages to go faster, but to complete and validate them one by one, so that the information needed is captured in the process before an agent has to fill it in.

**Four principles** ([`metodologia-global`](core/metodologia-global.md) §1):

- **Ambiguity reduction**: every hand-over makes explicit what was implicit, so the receiver interprets less and executes more.
- **Cumulative enrichment**: each stage adds detail without losing or re-deciding what was already settled.
- **Validation**: an agent can verify, but the close of each stage is validated by a person.
- **Traceability**: every result can be traced back to the decision that produced it, and every decision forward to where it landed.

**A structure** that organizes the process into nested units: **process → layer → phase → task**. Each **layer** works with its own context and shares no memory with the others, so the step between layers is governed by **contracts** that set what must cross. Within each phase, the agent analyzes, proposes a plan, executes and verifies, and a person validates. Closures get stronger as you move up a level: a task is validated, a phase is closed with a **gate** that logs what was decided, and a layer is closed with a reinforced gate that checks versions and consistency.

**A dynamic** for when things don't go in order: returning to a phase that's already closed is normal, as long as it's fixed at the source, leaves a trail, and its effect on later work is assessed.

**Its application to this process** ([`metodologia-aplicada`](core/metodologia-aplicada.md)) defines the role of each layer and its three contracts: the *briefing* (definition → design), the *technical profile* (definition → implementation) and the *handoff* (design → implementation), which is the one that carries the specs. The design layer, the most developed, has its method in [`metodologia-capa-diseno`](domain/capa-diseno/metodologia-capa-diseno.md) and its six phases in [`fases-proceso-diseno`](domain/capa-diseno/fases-proceso-diseno.md): design system, navigation, wireframes, components, views, and prototype with handoff.

---

## 7. Scope

**Developed:**

- the universal core of the methodology;
- the overview of the three layers and their contracts;
- the full design layer: method, phases and spec system.

**Not developed yet:**

- the definition and implementation layers don't have their own document; they're described in the overview;
- the reverse direction, from code to design, is identified but not developed;
- manual editing inside the tools is still a blind spot for logging: whatever is changed by hand without going through the agent isn't recorded.

**Split off into another project:** coordination between conversations and agents that don't share memory. See section 10.

**A general limit:** the core was extracted from a single process. The methodology distinguishes what has external backing from what has been observed here, and it doesn't present as universal what isn't yet.

---

## 8. Current status

The methodology is a **draft** and still evolving:

- the universal core is in a new version (v0.5) that restructures the principles and still has sections being written;
- the layer overview coexists with an earlier synthesis document that needs to be merged into it;
- pending work is in [`evolucion/TAREAS.md`](evolucion/TAREAS.md).

The open lines of work are bringing the definition and implementation layers up to the level of the design layer, continuing to check which core principles hold up in other processes, and developing the code-to-design direction.

---

## 9. How the repository is organized

```text
.
├── core/                        current method: core and overview
│   ├── metodologia-global.md
│   ├── metodologia-aplicada.md
│   ├── metodologia-aplicada-sintesis.md
│   └── convenciones-repo.md
├── domain/                      method per layer
│   └── capa-diseno/
│       ├── metodologia-capa-diseno.md
│       ├── fases-proceso-diseno.md
│       └── spec/                specification system
├── evolucion/                   how the method came to be
│   ├── TAREAS.md
│   ├── decisiones-consolidacion.md
│   └── entrada-decisiones-2026-08-06.md
└── CONTEXT_GIT.md               Git versioning rules
```

- **`core/`** holds the current method: the universal core, the process overview and the conventions used to maintain the documents.
- **`domain/`** holds the method for each layer. Today, only design.
- **`evolucion/`** isn't method: it gathers pending work and the historical record of the decisions and tests that shaped the methodology. It's useful for understanding why the method is the way it is. In case of any discrepancy, what's in `core/` and `domain/` prevails.

Each document has a header with its version, its status and the documents it derives from. The change history is kept in Git, with one commit per decision.

---

## 10. Relationship with Warp

During the research, the work was spread across many conversations and tools that didn't share memory, and the project's state started to drift out of sync. That problem is different from the one this methodology studies: it isn't about how a process moves forward and gets validated, but about how to keep knowledge coherent when several agents work on it over time.

It was explored here first and then split off into its own project, **Warp**: a Git-based knowledge architecture for coordinating people and agents, organized into persistent lines of responsibility, with explicit authority over each document.

→ [github.com/gineslm/warp](https://github.com/gineslm/warp)

---

## 11. License and author

Dual license: code under **MIT**, and documentation and methodology under **CC BY-SA 4.0**. See [`LICENSE`](LICENSE), [`LICENSE-CODE`](LICENSE-CODE) and [`LICENSE-DOCS`](LICENSE-DOCS).

**Ginés López Montalbán**
Design Engineer · Frontend / UX-UI · Design Systems · AI-assisted processes
[Online profile](https://www.dsigncloud.es/dosier/en/)
