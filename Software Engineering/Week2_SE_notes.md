# Week 2: Life Cycle Models

**Most historically emphasized topics for this week (NPTEL SE exam pattern):**
- Classical Waterfall Model phases + the Iterative Waterfall Model's "phase containment of errors" concept — recurring MCQ/MSQ staple.
- V-Model: its relationship to Waterfall, when to use it, its weaknesses — frequently contrasted against Waterfall/Spiral.
- Spiral Model's four quadrants and its identity as a "meta model" that subsumes other models.
- Agile Manifesto's four value statements, XP's 4 values + practice list, and Scrum roles/ceremonies/artifacts — heavily tested via "which of the following is/are true" MSQs.
- Model-selection ("which life cycle model would you choose for scenario X") and model-vs-model comparison questions (Prototyping vs RAD, Agile vs Waterfall, Incremental vs Evolutionary) — a recurring NPTEL SE question type across years.

---

## Life Cycle Model: Basic Concepts ⭐High

> **Software life cycle model** (also called a *process model* or *SDLC*): a descriptive and diagrammatic model of the software life cycle that identifies all activities undertaken during product development, establishes a precedence ordering among these activities, and divides the life cycle into phases.

- Each life cycle phase consists of several activities — e.g., the design stage might consist of structured analysis, structured design, and design review.
- **Why model the life cycle?** A graphical and written description helps common understanding among developers, helps identify inconsistencies/redundancies/omissions in the development process, and helps tailor a process model to specific projects.
- A development team must identify a suitable life cycle model and **adhere to it** — the primary advantage is that it helps develop software in a systematic and disciplined manner.
- **Single programmer vs team:** A lone programmer working on a problem within their grasp can use an informal *exploratory* approach (code → test → design → fix, repeated in any order) and still succeed. A team, however, needs a precise shared understanding of who does what and when — otherwise the project descends into chaos. A project fails if one engineer starts coding, another writes the test document first, another defines the file structure, and another defines I/O independently.

### Phase entry/exit criteria and milestones
- A life cycle model defines **entry and exit criteria** for every phase. A phase is complete only when all its exit criteria are satisfied, and a phase can start only when its entry criteria are satisfied.
  - Example: exit criteria for the SRS phase = the SRS document is complete, reviewed, and approved by the customer.
- **Milestones** help project managers track progress; phase entry and exit points are important milestones.
- **With a life cycle model**, the project manager can accurately state at any time which stage (design/code/test/etc.) the project is in.
- **Without one**, tracking becomes very difficult — the manager must depend on team members' guesses, commonly leading to the **"99% complete syndrome"** (the project always seems 99% done but never finishes).

### Deliverables: myth vs. reality
| | Statement |
|---|---|
| **Myth** | The only deliverable of a successful project is the working program. |
| **Reality** | Documentation of all aspects of software development is needed to support operation and maintenance. |

### Common life cycle models covered in this course
Waterfall · V-model · Evolutionary (traditional models) · Prototyping · Spiral · Agile models

```
                 Conceptualize
                       │
     Retire ◄──────────┼──────────► Specify
        ▲                            │
        │        Software            ▼
     Deliver      Life Cycle       Design
        ▲                            │
        │                            ▼
      Test ◄───────── Code ◄────── Maintain
```
*(The generic software life cycle: Conceptualize → Specify → Design → Code → Test → Deliver → Maintain → Retire.)*

---

## Classical Waterfall Model ⭐High

The classical waterfall model divides the life cycle into a strict linear sequence of phases:

```
Feasibility Study
       │
       ▼
Requirements Analysis
   & Specification
       │
       ▼
     Design
       │
       ▼
Coding & Unit Testing
       │
       ▼
Integration & System
     Testing
       │
       ▼
   Maintenance
```
*"Simplest and most intuitive" of the life cycle models — each phase must finish before the next begins.*

### Relative effort across phases
- The phases between feasibility study and testing are called the **development phases**.
- Among all phases, **maintenance consumes the maximum effort** (development effort : maintenance effort ≈ **40:60**).
- Among the *development* phases specifically, **testing consumes the maximum effort**.
- Most organizations define standards for phase deliverables and phase entry/exit criteria, and prescribe methodologies for specification, design, testing, and project management — together these form the organization's **software development methodology**, which fresh engineers are expected to master.
- **Metaphor:** like a mathematician presenting a proof as a single clean chain of deductions — even though the actual proof process involved a convoluted set of partial attempts, blind alleys, and backtracks — project documents should, irrespective of the life cycle model actually followed, reflect a classical-waterfall-style structure to aid comprehension.

### Phase 1 — Feasibility Study
> **Main aim:** determine whether developing the software is financially worthwhile (economic feasibility) and technically feasible, while roughly understanding what the customer wants (input data, processing needed, output data, and constraints).

**Three feasibility dimensions:**
```
        Economic feasibility
       (cost/benefit feasibility)
                │
Technical ──────┼────── Schedule
feasibility     │       feasibility
          Feasibility
          Dimensions
```

**Activities during feasibility study:**
1. Work out an overall understanding of the problem.
2. Formulate different solution strategies.
3. Examine alternative strategies in terms of resources required, cost of development, and development time.
4. Perform a **cost/benefit analysis (CBA)** to determine the best solution — a solution may even turn out to be infeasible due to high cost, resource constraints, or technical reasons.

**Cost/Benefit Analysis (CBA):**
- Identify all costs: development costs, set-up costs, operational costs.
- Identify the value of the benefits.
- Check that benefits exceed costs.

**The business case:**
- Feasibility studies should produce a "business case" justifying the project start, showing benefits will exceed costs, and accounting for business risks.
- Costs include development + operation; benefits may be quantifiable or non-quantifiable.

**Writing an effective business case (6 parts):**
| # | Section | Key content |
|---|---|---|
| 1 | Executive summary | High-level overview |
| 2 | Project background | What exactly the project undertakes (not the "bigger picture") |
| 3 | Business opportunity | What difference it makes; what if we don't do it |
| 4 | Costs | Development, implementation, training, change management, operations |
| 5 | Benefits | Usually revenue generation and cost reduction |
| 6 | Risks | Identify risks and explain how they'll be managed |

🖼️ *A worked case study (SPF scheme for a coal mining company, "CFL") illustrates feasibility study in practice — a manager visits the site, identifies functionality and data needs, proposes alternatives, and presents a Go/No-Go decision. This is a real-world example, not something to memorize structurally.*

### Phase 2 — Requirements Analysis and Specification
> **Aim:** understand the exact requirements of the customer and document them properly. Consists of two distinct activities: **requirements gathering & analysis** and **requirements specification**.

- **Requirements gathering:** data is usually collected from end-users through interviews and discussions (e.g., interviewing all accountants of an organization for an accounting software).
- **Requirements analysis:** the data initially collected typically contains contradictions and ambiguities, because each user has only a partial and incomplete view of the system. These ambiguities/contradictions must be identified and resolved through discussion with customers.
- **Requirements specification:** the resolved requirements are organized into a **Software Requirements Specification (SRS)** document, after removing inconsistencies, anomalies, and incompleteness.

### Phase 3 — Design
> During design, the requirements specification is transformed into a form suitable for implementation in a programming language.

Two commonly used design approaches:

| Approach | Consists of | Notes |
|---|---|---|
| **Traditional (structured) design** | Structured analysis (via DFDs) + structured design | High-level design decomposes the system into modules and represents invocation relationships among them; detailed design designs data structures & algorithms per module. |
| **Object-oriented design (OOD)** | Identify real-world objects & their relationships (e.g., employees, managers, payroll register, departments) → refine object structure into detailed design | Advantages: lower development effort, lower development time, better maintainability. |

```
Structured design example (payroll-like system):
                    root
                     │
      ┌──────────────┼──────────────┐
    order          indent          query
      │
 ┌────┴────┐
Handle-   Handle-       Handle-query
order     indent
  │
Get-order → Accept-order → Process-order
```

### Phase 4 — Coding and Unit Testing
- Each module of the design is coded.
- Each module is **unit tested** — tested independently as a standalone unit — and debugged.
- Each module is documented.

### Phase 5 — Integration and System Testing
- Different modules are integrated in a planned manner, usually through a number of steps; at each integration step, the partially integrated system is tested.
```
        M1    M2    M5    M7
          \   |    /    /
           \  |   /    /
    M3 ──── integrated system ──── M4, M6, M8
```
- After all modules are successfully integrated and tested, **system testing** is carried out — its goal is to ensure the developed system functions according to the requirements specified in the SRS document.

### Phase 6 — Maintenance
- Maintenance of any software requires **much more effort** than the effort to develop the product itself (development : maintenance ≈ 40:60).

| Type | Description |
|---|---|
| **Corrective maintenance** | Correcting errors not discovered during development phases. |
| **Perfective maintenance** | Improving implementation and enhancing functionalities. |
| **Adaptive maintenance** | Porting software to a new environment (e.g., new computer/OS). |

---

## Iterative Waterfall Model ⭐High

- The classical waterfall model is **idealistic** — it assumes no defect is ever introduced during any development activity. In practice, defects get introduced in almost every phase.
- Defects usually get **detected much later** in the life cycle (e.g., a design defect might go unnoticed until coding or testing). The later a defect is detected, the more expensive its removal.
- Once a defect is detected, the phase in which it occurred must be **reworked**, along with all subsequent phases — hence the need for **feedback paths** in the classical waterfall model.

```
Feasibility Study
   │▲
   ▼│
Requirements Analysis
   │▲
   ▼│
  Design
   │▲
   ▼│
  Coding
   │▲
   ▼│
  Testing
   │▲
   ▼│
Maintenance
```
*(Feedback arrows allow going back to a prior phase when a defect traceable to that phase is found — this is what turns the "classical" waterfall into the "iterative" waterfall.)*

> **Phase containment of errors:** the principle of detecting an error as close as possible to its point of introduction — ideally in the same phase in which it was introduced. A defect found in the design phase itself is far cheaper to fix than one found only at the end of integration/system testing, because rework then must be carried out on design *and* code *and* test phases.

- The iterative waterfall model is **by far the most widely used model** — almost every other model discussed in this course is derived from it.

### Waterfall — strengths, deficiencies, and when to use

| Strengths | Deficiencies |
|---|---|
| Easy to understand and use, especially by inexperienced staff | All requirements must be known upfront — but in most real projects, requirements change after project start |
| Milestones are well understood by the team | Can give a false impression of progress |
| Provides requirements stability during development | Integration is one "big bang" at the end |
| Facilitates strong management control (plan, staff, track) | Little opportunity for the customer to preview the system |

**When to use the Waterfall Model:** requirements are well known and stable, technology is understood, and the development team has experience with similar projects.

---

## V Model ⭐High

- A variant of the waterfall model that **emphasizes verification and validation (V&V)**, with V&V activities spread across the entire life cycle.
- In every development phase, testing activities are planned **in parallel** with development.

```
Project Planning                                      Production, Operation
                                                          & Maintenance
     │                                                        ▲
     ▼                                                        │
Requirements Specification ─────────────────────────── System Testing
     │                                                        ▲
     ▼                                                        │
High Level Design ───────────────────────────────── Integration Testing
     │                                                        ▲
     ▼                                                        │
Detailed Design ───────────────────────────────────────  Unit Testing
     │                                                        ▲
     └──────────────────────► Coding ──────────────────────────┘
```
*Left arm = development/decomposition; right arm = corresponding V&V/testing activity, planned in parallel with its counterpart on the left.*

**V-Model steps (paired):**
| Development side | Corresponding V&V/testing side |
|---|---|
| Planning | — |
| Requirements Analysis & Specification | System test design |
| High-level Design | Integration test design |
| Detailed Design | Unit test design |

| Strengths | Weaknesses |
|---|---|
| Emphasizes V&V planning from early stages of development | Does not support overlapping of phases |
| Each deliverable is made testable | Does not handle iterations or phases well |
| Easy to use | Does not easily accommodate later changes to requirements |
| | Does not provide support for effective risk handling |

**When to use the V-Model:** natural choice for systems requiring high reliability (e.g., embedded control applications, safety-critical software); all requirements known up-front; solution and technology are known.

---

## Prototyping Model ⭐High

- A **derivative of the waterfall model**. Before actual development starts, a working **prototype** of the system is built.
- A prototype is a **toy implementation**: limited functional capabilities, low reliability, inefficient performance.

**Reasons for prototyping / developing a prototype:**
- Learning by doing — useful where requirements are only partially known.
- Improved communication and improved user involvement.
- Reduced need for documentation and reduced maintenance costs.
- Illustrate to the customer input data formats, messages, reports, or interactive dialogs.
- Examine technical issues tied to major design decisions (e.g., response time of a hardware controller, efficiency of a sorting algorithm).
- It is impossible to "get it right" the first time — so the team plans to **throw away** the first version to develop good software.

**Building the prototype:**
- Start with approximate requirements, carry out a quick design.
- The prototype is built using short-cuts: inefficient/inaccurate/dummy functions, table look-ups instead of real computation, etc.

```
Requirements    Quick      Customer         Customer
 Gathering  →  Design  →  Evaluation of  →  satisfied? ──No──► Refine
                          Prototype                Requirements
                                │                       │
                               Yes                      └───(loop back to
                                │                            Quick Design)
                                ▼
                      Design → Implement → Test → Maintain
                     (actual system, built using Waterfall Model)
```
- The developed prototype is submitted to the customer for evaluation; based on feedback it is refined, and this cycle continues until the customer approves it. **The actual system is then developed using the waterfall model.**
- Requirements analysis & specification effectively becomes redundant — the final working prototype (incorporating all user feedback) serves as an **animated requirements specification**.
- The design and code of the prototype are usually **thrown away**, though the experience gained helps a great deal while developing the actual software.
- Even though building a working prototype involves additional cost, overall development cost is usually **lower** for systems with unclear requirements or unresolved technical issues, because issues that would otherwise surface later as expensive change requests get resolved early.

| Advantages | Disadvantages |
|---|---|
| Resulting software is usually more usable | Expensive for some projects |
| User needs are better accommodated | Susceptible to over-engineering — designers may add sophistication not present in the prototype |
| Higher quality design | |
| Resulting software is easier to maintain | |
| Overall lower development cost | |

---

## Major Difficulties of Waterfall-Based Models ⭐Medium

1. **Difficulty accommodating change requests** during development — ~40% of requirements typically change during development.
2. **High cost** incurred in developing custom applications.
3. Waterfall-based approaches are **"heavy-weight processes."**
4. Requirements are determined at the very start and assumed fixed from that point on, with long-term planning based on this fixed assumption.

> "...the assumption that one can specify a satisfactory system in advance, get bids for its construction, have it built, and install it... this assumption is fundamentally wrong, and many software acquisition problems spring from this..." — **Frederick Brooks**

---

## Incremental Model ⭐High

- **Key idea (Victor Basili):** take advantage of what is learned during development of earlier, incremental, deliverable versions of the system. Start with a simple implementation of a subset of requirements and iteratively enhance the evolving sequence of versions; at each version, design modifications are made along with new functional capabilities.
- **Waterfall = single release; Incremental (iterative) = many releases (increments).**
  - First increment: core functionality.
  - Successive increments: add/fix functionality.
  - Final increment: the complete product.
- Each iteration is a **short mini-project** with its own separate life cycle (e.g., a mini-waterfall).
- Key characteristics: builds the system incrementally; consists of a planned number of iterations; each iteration produces a working program.
- **Benefit:** facilitates and manages change.
- Forms the foundation of agile techniques, and the basis for RUP (Rational Unified Process) and XP (Extreme Programming).

```
Requirements   Split into   Design
   Outline  →   Features  →   │
                               ▼
                Develop Increment → Validate Increment →
                Integrate Increment → Validate System → Final System
```

**Incremental delivery (per increment):**
```
increment 1: design → build → install → Customer feedback
increment 2:            design → build → install → Customer feedback
increment 3:                       design → build → install → Customer feedback
```
*(Each successive increment's design/build/install cycle starts once the prior increment is delivered, so increments overlap in time and each folds in customer feedback from the previous one.)*

### Which step (increment) first? — Value/Cost ratio
- Some steps are pre-requisites due to physical dependencies; others can be in any order.
- **V/C ratio** is used to prioritize: **V** = value to customer (score 1–10), **C** = cost to developers (score 0–10).

**Worked example:**
| Step | Value | Cost | V/C ratio | Priority order |
|---|---|---|---|---|
| Profit-based pay for managers | 9 | 1 | 9 | 1st |
| Profit reports | 9 | 2 | 4.5 | 2nd |
| Purchasing plans | 9 | 4 | 2.25 | 3rd |
| Ad hoc enquiry | 5 | 5 | 1 | 4th |
| Online database | 1 | 9 | 0.11 | 5th |

---

## Evolutionary Model (with Iterations) ⭐High

- **Recognizes the reality of changing requirements** — Capers Jones's research on 8000 projects found ~40% of final requirements arrived *after* development had already begun.
- **Promotes early risk mitigation** by breaking the system into mini-projects and focusing on riskier issues first — *"plan a little, design a little, and code a little."*
- Encourages all development participants (end users, testers, integrators, technical writers) to be involved **earlier**.

> **"A complex system will be most successful if implemented in small steps... 'retreat' to a previous successful step on failure... opportunity to receive feedback from the real world before throwing in all resources... and you can correct possible errors..."** — Tom Gilb, *Software Metrics*

> **Craig Larman:** Evolutionary iterative development implies that requirements, plan, estimates, and solution evolve/are refined over the course of iterations, rather than being fully defined and "frozen" in a major up-front specification effort.

- First the **core modules** are developed; the initial skeletal software is then refined into increasing levels of capability (iterations) by adding new functionality in successive versions.
- Development happens over several **"mini waterfalls."** Each iteration ends with delivery of tangible, tested, integrated, executable code — an incremental improvement.
- **Iteration length is short and fixed**, usually **2–6 weeks**; development typically takes many iterations (e.g., 10–15).
- Requirements/design are **not frozen** upfront — there's an ongoing opportunity to modify them.

```
Initial Rough    Specification →  Development  → Validation
Requirements          │                                │
                       ▼                                ▼
                 Initial version → Intermediate versions → Final version
```

| Advantages | Problems |
|---|---|
| Users can experiment with a partially developed system well before the full version releases | The process is intangible — no regular, well-defined deliverables |
| Helps find exact user requirements | The process is unpredictable — hard to manage scheduling, workforce allocation, etc. |
| Core modules get tested thoroughly, reducing final errors | Systems are rather poorly structured — continual unpredictable changes degrade structure |
| Better management of complexity (one increment at a time) | Systems may not even converge to a final version |
| Better management of changing requirements | |
| Faster/better incorporation of customer feedback than waiting until after full development | |
| Training can start on an earlier release; frequent releases let developers fix unanticipated problems quicker | |

---

## RAD (Rapid Application Development) Model ⭐High

- Sometimes called the **rapid prototyping model**.
- **Major aims:** decrease time and cost of software development; facilitate accommodating change requests as early as possible, before large investments have been made in development/testing.
- **Underlying principle:** make only short-term plans and make heavy reuse of existing code, to reduce time/cost while retaining flexibility.

**Methodology:**
- Plans are made **one increment at a time**; the time planned for each iteration is called a **time box**.
- Each iteration enhances the implemented functionality a little.
- During each iteration: a quick-and-dirty prototype-style implementation of selected functionality is built → customer evaluates and gives feedback → prototype is refined based on that feedback.

**How RAD achieves faster development:** through specialized tools supporting a visual style of development, use of reusable components, and use of standard APIs.

| Suitable for RAD | Unsuitable for RAD |
|---|---|
| Customized product for one or two customers only | Few plug-in components available |
| Performance and reliability not critical | High performance or reliability required |
| System can be split into several independent modules | No precedent for similar products exists |
| | System cannot be modularized |

### Prototyping vs. RAD
| Prototyping Model | RAD Model |
|---|---|
| Prototype is used to gain insight into the solution, choose between alternatives, and elicit feedback | Prototype **evolves into** deliverable software |
| Prototype is usually **thrown away** | Prototype is **kept and refined** into the final product |
| Better quality/reliability | Faster development, but possibly poorer quality/reliability |

### RAD vs. Iterative Waterfall
- Iterative waterfall: all product functionalities are developed together.
- RAD: functionalities are developed incrementally through heavy code/design reuse, with customer feedback after each iteration used to refine the prototype.
- Iterative waterfall does **not** easily accommodate change requests, but produces good documentation and generally better quality/reliability than RAD.

### RAD vs. Evolutionary Model
- Incremental development occurs in **both**.
- In RAD, each increment is a **quick-and-dirty prototype**; in the evolutionary model, each increment is **systematically developed using the iterative waterfall model**.
- RAD develops software in **shorter** increments; evolutionary-model increments are comparatively **larger**.

---

## Unified Process (RUP) ⭐Medium

- Developed by Ivar Jacobson, Grady Booch, and James Rumbaugh — **incremental and iterative**.
- **Rational Unified Process (RUP)** is the version tailored by Rational Software (acquired by IBM in Feb 2003).

**Four phases** (iterative development happens *within* every phase; each iteration may span two weeks or less):
```
Iterations   Iterations   Iterations   Iterations
    │            │            │            │
Inception → Elaboration → Construction → Transition
```

**Two-dimensional structure of RUP:**
- **Horizontal axis:** time — the lifecycle aspect of the process (phases above).
- **Vertical axis:** core process workflows (e.g., communication, planning, modeling, construction, deployment) recurring across phases.

**Work products by phase:**
| Inception | Elaboration | Construction | Transition |
|---|---|---|---|
| Vision document | Use-case model | Design model | SW increment |
| Initial use-case model | Requirements | SW components | Beta test reports |
| Initial business case | Analysis model | Test plan | User feedback |
| Initial risk list | Preliminary model | Test procedure & cases | ... |
| Project plan | Revised risk list | User manual | |
| Prototype(s) | Preliminary manual | Installation manual | |

**Inception-phase activities / outcomes:** formulate project scope; risk management, staffing, project plan; initial requirements capture; cost/benefit analysis; initial risk analysis; project scope definition; define a candidate architecture; develop a disposable prototype; initial use-case model (10–20% complete); first-pass domain model.

---

## Spiral Model ⭐High

- Proposed by **Boehm in 1988**.
- Each **loop of the spiral** represents a phase of the software process — e.g., innermost loop = system feasibility, next loop = requirements definition, next = system design, and so on. **There are no fixed phases** — the phases are just illustrative examples for a given project.
- The team decides how to structure the project into phases: start with a generic model and add extra phases for specific projects or as problems are identified.
- Each loop is split into **four sectors (quadrants):**

```
              Determine Objectives
                        │
     Identify &         │         Develop Next
     Resolve Risks ◄────┼────►   Level of Product
                        │
              Customer Evaluation
                 of Prototype
```

| Quadrant | Name | Activities |
|---|---|---|
| 1st | **Objective Setting** | Identify phase objectives; examine associated risks (risk = any adverse circumstance that might hamper successful project completion); find alternate solutions. |
| 2nd | **Risk Assessment & Reduction** | For each identified risk, carry out detailed analysis and take steps to reduce it (e.g., build a prototype if requirements risk is high). |
| 3rd | **Development & Validation** | Develop and validate the next level of the product. |
| 4th | **Review & Planning** | Review results so far with the customer; plan the next iteration around the spiral. |

- With each iteration around the spiral, a **progressively more complete** version of the software is built.

**Spiral Model as a "meta model":**
- Subsumes all other discussed models — a **single-loop spiral represents the waterfall model**.
- Uses an evolutionary approach — iterations over the spiral are evolutionary levels.
- Enables understanding and reacting to risk during each iteration.
- Uses **prototyping** as a risk-reduction mechanism while retaining the **step-wise approach** of the waterfall model.

---

## Agile Models ⭐High

- **Agile:** easily moved, light, nimble, active software processes. Achieved by fitting the process to the project and avoiding time-wasting activities.
- Proposed in the **mid-1990s** to overcome shortcomings of the waterfall model; primarily designed to help projects adapt to **change requests**.
- Requirements are decomposed into many small incremental parts, each developed over **one to four weeks**.

> **Agile Manifesto** (agilemanifesto.org) — four value statements, each favoring the left over the right:
> - **Individuals and interactions** over processes and tools
> - **Working software** over comprehensive documentation
> - **Customer collaboration** over contract negotiation
> - **Responding to change** over following a plan

**Agile methodologies include:** XP, Scrum, Unified Process, Crystal, DSDM, Lean.

**Principal techniques:**
| Technique | Meaning |
|---|---|
| User stories | Simpler than use cases |
| Metaphors | Common vision of what's required, based on user stories |
| Spike | A simple program to explore potential solutions |
| Refactor | Restructure code without changing behavior, to improve efficiency/structure |

**Nitty-gritty of agile execution:**
- At a time, only **one increment** is planned, developed, and deployed at the customer site — no long-term plans.
- Even if an iteration doesn't add significant functionality, a **new release is still made at the end of each iteration** and delivered to the customer.
- **Face-to-face communication** is favored over written documents; the team shares a single office space and is deliberately kept **small (5–9 people)** — this makes agile best suited to **small projects**.

🖼️ *"Effectiveness of Communication Modes" diagram — plots communication channels (paper/documentation at the "cold" end, through email/phone/video, to face-to-face conversation at the "hot" end) against communication effectiveness; illustrates why agile favors face-to-face. Purely illustrative, not something to redraw for the exam.*

**Agile Model — Principles:**
- Primary measure of progress: **incremental release of working software**.
- Frequent delivery (every few weeks); requirement change requests easily accommodated; close cooperation between customers and developers; face-to-face communication among team members.

**Agile documentation:**
- "Travel light" — far less documentation than you'd think is needed.
- Agile documents are concise, describe information less likely to change, describe "good things to know," and are sufficiently accurate/consistent/detailed.
- Valid reasons to document: stakeholders require it; to define a contract model; to support communication with an external group; to think something through.

**Agile requirements management:** each iteration implements the **highest-priority** requirements from a prioritized stack; new requirements are prioritized and added to the stack at any time; requirements may be **reprioritized** or **removed** at any time.

**Adoption detractors:**
- Sketchy definitions → inconsistent/diverse interpretations.
- Requires high-quality people/skills.
- Short iterations inhibit long-term perspective.
- Higher risk from **feature creep** — harder to manage customer expectations; difficult to quantify cost, time, quality.

**Shortcomings:**
- Agility comes from **tacit knowledge** within the team rather than formal documents — can be misinterpreted, external review is difficult, and maintenance becomes difficult once the project is complete and the team disperses.

### Agile vs. Iterative Waterfall
| Iterative Waterfall | Agile |
|---|---|
| Steps through a planned sequence: requirements-capture → analysis → design → coding → testing | Sequences delivery of **working versions** of the product across several increments |
| Progress measured via delivered artefacts (spec, design docs, test plans, code reviews) | Progress measured via working software |
| — | *Similarity:* Agile teams essentially use the waterfall model **on a small scale**, within each increment |

### Agile vs. RAD
- Agile does **not** recommend prototypes — it emphasizes systematic development of each incremental feature.
- RAD is based on quick-and-dirty prototypes that are refined into production-quality code.

### Agile vs. Exploratory Programming
- **Similarities:** frequent re-evaluation of plans, emphasis on face-to-face communication, sparse use of documents.
- **Difference:** agile teams follow **defined, disciplined processes** and rigorous design — unlike the chaotic coding of exploratory programming.

---

## Extreme Programming (XP) ⭐High

- Proposed by **Kent Beck in 1999**. Named "extreme" because it recommends taking good practices to extreme levels — *"if something is good, why not do it all the time."*

**Taking good practices to the extreme:**
| If this is good... | ...then XP says do it "extremely": |
|---|---|
| Code review | Always review → **pair programming** |
| Testing | Continually write & execute tests → **test-driven development** |
| Incremental development | New increments every few days |
| Simplicity | Simplest design supporting only currently required functionality |
| Design | Everybody designs daily → **refactoring** |
| Architecture | Everybody works on defining/refining it → **metaphor** |
| Integration testing | Build & integrate several times a day → **continuous integration** |

**4 Values of XP:**
| Value | Meaning |
|---|---|
| Communication | Enhance communication among team members and with customers |
| Simplicity | Build something simple that works today, rather than something elaborate that's never used |
| Feedback | Keeping systems away from users is "trouble waiting to happen" |
| Courage | Don't hesitate to discard code |

**Best practices:** Coding (utmost attention — no working system without it), Testing (primary means of a fault-free product), Listening (careful listening to customers essential for quality), Designing (without it, dependencies become too complex to comprehend), Feedback (essential for learning customer requirements).

**XP Activities:**
| Activity | Key points |
|---|---|
| **XP Planning** | Begins with "user stories"; team assesses & costs each story; stories grouped into a deliverable increment; commitment made on delivery date |
| **XP Design** | Follows the **KIS** principle; encourages CRC cards; suggests "spike solutions" (design prototypes) for hard problems; encourages **refactoring** |
| **XP Coding** | Recommends writing unit test cases **before** coding (test-driven development); encourages **pair programming** |
| **XP Testing** | All unit tests executed daily; customer-defined **acceptance tests** assess customer-visible functionality |

**Full list of XP practices (13):**
1. Planning — scope of next release from business priorities + technical estimates
2. Small releases — simple system into production, then frequent short-cycle releases
3. Metaphor — a shared story guiding all development
4. Simple design — as simple as possible
5. Testing — continuous unit test writing/execution
6. *(design is covered via refactoring — see #7)*
7. Refactoring — continuously restructure without changing behavior
8. Pair programming — all production code written by two programmers at one machine
9. Collective ownership — anyone can change any code anywhere, anytime
10. Continuous integration — integrate/build many times a day
11. 40-hour week — no more than 40 hours/week as a rule
12. On-site customer — a user is part of the team, available full-time
13. Coding standards — code follows rules that emphasize communication

**Test-Driven Development (TDD) emphasis:** based on a user story, develop test cases first → implement a quick-and-dirty feature every couple of days → get customer feedback → alter if necessary → refactor → take up the next feature.

**When is XP suitable?**
- Projects involving new technology or research (requirements change rapidly, unforeseen technical problems arise).
- **Small projects.**

---

## Scrum ⭐High

**Characteristics:** self-organizing teams; product progresses through a series of month-long **sprints**; requirements captured as items in a **product backlog**; one of the agile processes.

```
Product Backlog → Sprint Planning → Sprint Backlog → [ Sprint
                                                          (Daily Scrum each day) ]
                                                              │
                                                              ▼
                                                     Sprint Review → Product Increment
```

**Sprint:**
- Target duration: **one month**; analogous to XP iterations/time boxes.
- The increment is designed, coded, and tested **during** the sprint.
- **No changes** are entertained during a sprint.

**Scrum Framework:**
| Category | Items |
|---|---|
| Roles | Product Owner, Scrum Master, (Development) Team |
| Ceremonies | Sprint Planning, Sprint Review, Sprint Retrospective, Daily Scrum Meeting |
| Artifacts | Product Backlog, Sprint Backlog, Burndown Chart |

**Key roles:**
| Role | Responsibilities |
|---|---|
| **Product Owner** | Represents customer interests; defines product features; decides release date/content; prioritizes features by market value; adjusts features/priority each iteration; accepts/rejects work results |
| **Development Team** | 5–9 people, cross-functional skill sets (QA, programmers, UI designers, etc.); self-organizing; membership changes only between sprints |
| **Scrum Master** (aka Project Manager) | Represents management to the project; facilitates the scrum process; removes impediments; ensures team is fully functional/productive; shields team from external interference |

**Ceremonies in detail:**
- **Sprint Planning Meeting:** goal is to produce the Sprint Backlog — Product Owner negotiates with the Team on which backlog items to work on to meet release goals; Scrum Master ensures realistic goals.
- **Sprint:** fundamental process flow — a month-long iteration completing incremental functionality; NO outside influence may interfere during the sprint; each day starts with the Daily Scrum Meeting.
- **Daily Scrum:** daily, 15-minute stand-up; **not** for problem solving; **not** about tracking who's behind schedule. Three questions: (1) What did you do yesterday? (2) What will you do today? (3) What obstacles are in your way? It is a meeting where team members make commitments to each other and the Scrum Master, and a good way for the Scrum Master to track team progress.
- **Sprint Review Meeting:** team presents what it accomplished during the sprint — typically a demo of new features; informal (2-hour prep-time rule); participants include customers, management, product owner, other engineers.

**Product Backlog:** a prioritized list of all desired work — story-based ("let user search and replace") and task-based ("improve exception handling") items; owned/managed by the Product Owner; typically a spreadsheet.

**Sprint Backlog:** a subset of Product Backlog items defining the work for one sprint; created by team members; each item has its own status, updated daily. During the sprint, the team may add/remove tasks as needed to meet the sprint goal, but **only the team** can update the Sprint Backlog; estimates are updated as new information arrives.

**Burndown Charts** — used to represent "work done"; simple but effective information disseminators. Three types:
| Type | Shows |
|---|---|
| **Sprint Burndown Chart** | Total Sprint Backlog hours remaining per day; ideally burns to zero by sprint end (in practice, not a straight line) |
| **Release Burndown Chart** | X-axis = sprints, Y-axis = story points remaining; answers "will the release finish on time? how many more sprints?" |
| **Product Burndown Chart** | "Big picture" view of progress across all releases |

**Scalability of Scrum:** a typical Scrum team is 6–10 people; Jeff Sutherland scaled it to over 800 people using a **"Scrum of Scrums"** (aka Meta-Scrum); meeting frequency depends on the degree of coupling between work packets.

### Agile vs. Plan-Driven Processes
| Agile | Plan-Driven |
|---|---|
| Small products and teams; scalability limited | Large products and teams; hard to scale down |
| Largely untested on safety-critical products | Proven for highly critical products |
| Good for dynamic environments, but expensive for stable ones | Good for stable environments, but expensive for dynamic ones |
| Requires experienced personnel throughout | Requires only a few experienced personnel |
| Personnel thrive on freedom and chaos | Personnel thrive on structure and order |

---

## Quick-Reference: Model Selection Cheat Sheet ⭐High

| Scenario characteristic | Best-fit model(s) |
|---|---|
| Requirements well known, stable; technology understood | Waterfall |
| High reliability / safety-critical, requirements known up-front | V-Model |
| Requirements partially known / unclear; need to explore UI or technical feasibility | Prototyping |
| Need to reuse a lot of existing code, tight time/cost, modest reliability needs | RAD |
| Core functionality needed fast, then incremental enhancement; large project split into independent modules | Incremental Model |
| Requirements expected to evolve substantially during development | Evolutionary Model |
| High/uncertain risk that needs active, iterative management | Spiral Model |
| Small team (5–9), requirements likely to change often, need fast customer feedback | Agile / XP / Scrum |

---

## Practice Exam (NPTEL Pattern)

**1.** A software life cycle model primarily does NOT do which of the following?
a) Identify activities undertaken during product development
b) Establish a precedence ordering among activities
c) Guarantee zero defects in the delivered software
d) Divide the life cycle into phases

**2. (MSQ)** Which of the following are true regarding phase entry/exit criteria?
a) A phase is complete only when all its exit criteria are satisfied
b) A phase can start only if its entry criteria are satisfied
c) Entry and exit criteria are optional and rarely defined in practice
d) Phase entry and exit points are considered important milestones

**3.** The "99% complete syndrome" is most closely associated with:
a) Following a life cycle model rigorously
b) Absence of a life cycle model, making progress tracking difficult
c) The maintenance phase of the waterfall model
d) The daily scrum meeting

**4.** In the classical waterfall model, which phase typically consumes the maximum effort among ALL life cycle phases (including post-delivery)?
a) Design
b) Coding and unit testing
c) Testing
d) Maintenance

**5.** Among the *development* phases alone (feasibility study through testing) of the classical waterfall model, which phase consumes the maximum effort?
a) Requirements analysis
b) Design
c) Testing
d) Coding

**6. (MSQ)** Which of the following are dimensions of feasibility examined during the feasibility study phase?
a) Economic feasibility
b) Technical feasibility
c) Schedule feasibility
d) Structural feasibility

**7.** What is "phase containment of errors"?
a) Ensuring no errors ever occur in any phase
b) Detecting an error as close as possible to its phase of introduction
c) Containing all testing activity to a single phase
d) Preventing feedback loops between phases

**8.** Which of the following is NOT a deficiency of the classical/iterative waterfall model?
a) Requires all requirements to be known upfront
b) Can give a false impression of progress
c) Integration happens as one big bang at the end
d) Provides strong management control through well-understood milestones

**9.** The V-Model is best described as:
a) A model with no relationship to the Waterfall model
b) A variant of Waterfall emphasizing verification and validation spread across the life cycle
c) A purely iterative, risk-driven model with four quadrants
d) An agile methodology emphasizing pair programming

**10. (MSQ)** Which are weaknesses of the V-Model?
a) Does not support overlapping of phases
b) Does not handle iterations or phase changes well
c) Provides no support for effective risk handling
d) Cannot be used for safety-critical software

**11.** In the Prototyping Model, once the customer approves the prototype, the actual system is developed using:
a) The Spiral model
b) The Waterfall model
c) Extreme Programming
d) RAD

**12.** Which of the following is generally true when comparing the Prototyping Model to RAD?
a) In RAD, the prototype is usually thrown away
b) In Prototyping, the prototype evolves directly into the deliverable software
c) In RAD, the prototype evolves into deliverable software, while in Prototyping it is usually discarded
d) Both models never produce a working prototype

**13.** According to Frederick Brooks (as quoted in the material), the fundamentally wrong assumption behind many waterfall-based software acquisition problems is:
a) That software should always be tested before delivery
b) That one can specify a satisfactory system in advance, have it built, and install it
c) That documentation is unnecessary
d) That prototypes should always be discarded

**14.** In the Incremental Model, the Value/Cost (V/C) ratio is used to:
a) Estimate total project cost
b) Decide the order in which steps/increments should be implemented
c) Measure customer satisfaction after delivery
d) Calculate testing effort per module

**15.** Using V=9, C=1 for one candidate step and V=1, C=9 for another, which step should be prioritized first, and why?
a) The second step, because higher cost implies higher value
b) The first step, because its V/C ratio (9) is far higher than the second's (0.11)
c) Both are equal priority since V+C is the same
d) Neither — priority is unrelated to V/C ratio

**16.** In the Evolutionary Model, iteration length is typically:
a) 6–12 months
b) 2–6 weeks
c) A single day
d) Exactly one calendar year

**17. (MSQ)** Which of the following are listed as problems of the Evolutionary Model?
a) The process is intangible, with no regular well-defined deliverables
b) The process is unpredictable and hard to manage
c) Systems are always perfectly structured regardless of changes
d) Systems may never converge to a final version

**18.** The Spiral Model was proposed by:
a) Kent Beck
b) Victor Basili
c) Barry Boehm
d) Frederick Brooks

**19.** In the Spiral Model, risk assessment and reduction occurs in which quadrant?
a) First quadrant
b) Second quadrant
c) Third quadrant
d) Fourth quadrant

**20. (MSQ)** Why is the Spiral Model called a "meta model"?
a) A single-loop spiral represents the Waterfall model
b) It uses an evolutionary approach across iterations
c) It uses prototyping as a risk-reduction mechanism
d) It eliminates the need for any risk analysis

**21. (MSQ)** Which of the following are among the four value statements of the Agile Manifesto?
a) Individuals and interactions over processes and tools
b) Comprehensive documentation over working software
c) Customer collaboration over contract negotiation
d) Responding to change over following a plan

**22.** In Extreme Programming, writing unit test cases before writing the code itself is known as:
a) Pair programming
b) Test-driven development
c) Continuous integration
d) Refactoring

**23. (MSQ)** Which of the following are among the 4 values of XP?
a) Communication
b) Simplicity
c) Feedback
d) Documentation

**24.** In Scrum, the Daily Scrum meeting is best described as:
a) A 15-minute stand-up meeting for problem solving
b) A 15-minute stand-up meeting where members answer three set questions, not for problem solving
c) A 2-hour formal review meeting with customers
d) A meeting held only at the start of a sprint

**25. (MSQ)** Which are recognized types of Burndown Charts in Scrum?
a) Sprint Burndown Chart
b) Release Burndown Chart
c) Product Burndown Chart
d) Feature Burndown Chart

---

## Answer Key

1. **c** — A life cycle model structures and disciplines development; it cannot guarantee zero defects (the iterative model exists precisely because defects still occur).
2. **a, b, d** — Entry/exit criteria are standard practice and function as milestones; (c) is false — they are, in fact, typically well-defined.
3. **b** — Without a life cycle model, managers rely on guesses, commonly producing a project that seems perpetually "99% done."
4. **d** — Maintenance consumes the most effort overall (~60% vs. 40% for development), per the stated 40:60 ratio.
5. **c** — Among the development phases specifically (feasibility through testing), testing consumes the most effort.
6. **a, b, c** — The three feasibility dimensions given are economic, technical, and schedule feasibility; "structural feasibility" isn't one of them.
7. **b** — Phase containment of errors means catching a defect in the same phase it was introduced, minimizing costly rework in later phases.
8. **d** — Strong management control is a *strength*, not a deficiency, of the waterfall model.
9. **b** — The V-Model is explicitly described as a variant of Waterfall that spreads verification & validation activities across the whole life cycle.
10. **a, b, c** — These three are explicitly listed weaknesses; the V-Model is actually well-suited to (not incapable of) safety-critical software.
11. **b** — Once the prototype is approved, the actual system is built using the waterfall model.
12. **c** — This is the core distinction: RAD's prototype becomes the product; the classic prototyping model's prototype is thrown away.
13. **b** — Brooks specifically calls out the assumption of specifying, building, and installing a system exactly as planned in advance as fundamentally wrong.
14. **b** — V/C ratio prioritizes which increment/step to implement first.
15. **b** — 9/1 = 9 vs. 1/9 ≈ 0.11 — the first step has a far higher value-to-cost ratio and should be prioritized.
16. **b** — Evolutionary Model iterations are short and fixed, typically 2–6 weeks.
17. **a, b, d** — These are the stated problems; systems are explicitly said to be "rather poorly structured," not perfectly structured.
18. **c** — Barry Boehm proposed the Spiral Model in 1988.
19. **b** — Risk assessment and reduction is the second quadrant's activity.
20. **a, b, c** — All three reasons are given for calling it a meta model; it does not eliminate risk analysis — risk analysis is central to it.
21. **a, c, d** — The Manifesto favors *working software* over comprehensive documentation, not the reverse, so (b) is false as stated.
22. **b** — This describes test-driven development (TDD), one of XP's core coding practices.
23. **a, b, c** — XP's 4 values are Communication, Simplicity, Feedback, and Courage — "Documentation" is not one of them.
24. **b** — The Daily Scrum is a strict 15-minute stand-up structured around three questions, explicitly not a problem-solving session.
25. **a, b, c** — Sprint, Release, and Product burndown charts are the three types named; "Feature Burndown Chart" is not mentioned.
