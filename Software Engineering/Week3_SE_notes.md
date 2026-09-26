# Week 3: Life Cycle Models II — Agile Model, XP, Scrum (+ start of Requirements Analysis & Specification)

**Most historically emphasized topics for this week (based on general NPTEL SE exam pattern):**
- Agile Manifesto's four value statements and the principles behind the Agile model — frequently tested as "which of the following is/are true about agile" MSQs.
- Agile vs Iterative Waterfall vs RAD vs Exploratory Programming — classic comparison/contrast MCQs.
- XP practices — especially pair programming, TDD, refactoring, continuous integration, and spike solutions (definition-matching and "which practice does X describe" questions).
- Scrum roles, ceremonies, and artifacts — Product Owner vs Scrum Master responsibilities, and the "no changes during a Sprint" rule is a favorite trap option.
- Purpose/uses of an SRS document and the exponentially-increasing cost-of-fixing-errors curve — a recurring "why do we need SRS" reasoning question.

---

## Agile Software Development: Motivation ⭐High

> **Agile**: Easily moved, light, nimble, active software processes.

- Agility is achieved by:
  - Fitting the process to the project (rather than forcing the project into a rigid process).
  - Avoidance of activities that waste time and effort.
- The Agile model was proposed to **overcome the shortcomings of the waterfall model** of development.
  - Proposed in the **mid-1990s**.
  - Primarily designed to help projects **adapt to change requests** quickly.
- In the Agile model, requirements are **decomposed into many small incremental parts** that can each be developed over **one to four weeks**.

---

## Ideology: The Agile Manifesto ⭐High

The Agile Manifesto expresses four value trade-offs (source: agilemanifesto.org):

| Value Favored | Over |
|---|---|
| Individuals and interactions | Process and tools |
| Working software | Comprehensive documentation |
| Customer collaboration | Contract negotiation |
| Responding to change | Following a plan |

> Note the "over" — the manifesto does not say the item on the right is worthless, only that the item on the left is valued **more**. This distinction is a common trick in MCQs.

---

## Agile Methodologies (Families) ⭐Medium

A number of concrete methodologies fall under the "Agile" umbrella:
- **XP** (Extreme Programming)
- **Scrum**
- Unified Process
- Crystal
- DSDM (Dynamic Systems Development Method)
- Lean

---

## Agile Model: Principal Techniques ⭐High

| Technique | Description |
|---|---|
| **User stories** | Simpler than use cases; short, informal descriptions of a feature from an end-user perspective. |
| **Metaphors** | Based on user stories; developers propose a common shared vision of what is required (a "simple shared story" of how the whole system works). |
| **Spike** | A simple/throwaway program written to explore potential solutions to a difficult design problem. |
| **Refactor** | Restructuring code **without changing its external behavior**, to improve efficiency, structure, readability, etc. |

---

## Agile Model: Nitty Gritty (Iteration Mechanics) ⭐Medium

- At any given time, **only one increment** is planned, developed, and deployed at the customer site.
  - **No long-term plans are made.**
- An iteration may not add significant functionality, but:
  - A **new release is invariably made at the end of every iteration**.
  - That release is delivered to the customer for regular use.

---

## Methodology: Communication ⭐Medium

- **Face-to-face communication is favoured over written documents.**
- To facilitate this:
  - The development team shares a **single office space**.
  - Team size is deliberately kept **small (5–9 people)**.
  - This is why the Agile model is best suited to **small projects**.

### Effectiveness of Communication Modes 🖼️
*(Diagram is a conceptual curve, not a strict data chart — described rather than redrawn.)*

The chart plots **Communication Effectiveness (y-axis)** against **Richness of the Communication Channel (x-axis, Cold → Hot)**. Ordered from least to most effective:

```
Cold  ─────────────────────────────────────────────►  Hot
Paper → Audiotape → Videotape → Email conversation →
Documentation Options → Phone conversation →
Video conversation → Modeling Options →
Face-to-face conversation → Face-to-face at whiteboard
```
*(Copyright 2002–2005 Scott W. Ambler; original diagram copyright 2002 Alistair Cockburn.)*

**Takeaway:** the richer/"hotter" the channel, the more effective the communication — this is the rationale behind Agile's preference for face-to-face conversation and whiteboard modeling over documentation.

---

## Agile Model: Principles ⭐High

> **Primary measure of progress: Incremental release of working software.**

Important principles behind the Agile model:
- **Frequent delivery** of versions — once every few weeks.
- Requirements **change requests are easily accommodated**.
- **Close cooperation** between customers and developers.
- **Face-to-face communication** among team members.

---

## Agile Documentation ⭐Medium

- **Travel light**: you need far less documentation than you think.
- Agile documents:
  - Are concise.
  - Describe information that is **less likely to change**.
  - Describe "good things to know."
  - Are **sufficiently** accurate, consistent, and detailed (not exhaustively so).
- Valid reasons to still produce documentation:
  - Project stakeholders require it.
  - To define a contract model.
  - To support communication with an external group.
  - To think something through.

### Agile Software Requirements Management (diagram)

Requirements are managed as a **prioritized stack**, not a fixed, frozen list:

```
High Priority
 ┌───────────────────────────────┐
 │ ████████████████████████████  │ ─┐
 │ ████████████████████████████  │  │  Each iteration implements the
 │ ████████████████████████████  │ ─┘  highest-priority requirements
 │ ████████████████████████████  │ ◄── New requirement: prioritized & added to stack
 │ ████████████████████████████  │ ◄── Requirements may be re-prioritized any time
 │ ████████████████████████████  │ ◄── Requirements may be removed any time
 └───────────────────────────────┘
Low Priority
        Requirements
```
*(Copyright 2004 Scott W. Ambler.)*

---

## Adoption Detractors (Risks/Criticisms of Agile) ⭐High

- **Sketchy/loose definitions** make inconsistent and diverse interpretations of "Agile" possible.
- **High-quality people skills required** — Agile relies heavily on skilled, self-disciplined individuals.
- **Short iterations inhibit long-term perspective.**
- **Higher risk of feature creep**:
  - Harder to manage feature creep and customer expectations.
  - Difficult to quantify cost, time, and quality up front.

---

## Agile Model: Shortcomings ⭐High

Agile derives agility by developing **tacit knowledge within the team**, rather than relying on formal documents. This causes problems:
- Tacit knowledge **can be misinterpreted**.
- **External review is difficult to get** (little documentation to review against).
- When the project is complete and the team disperses, **maintenance becomes difficult** (knowledge walks out the door with the team).

---

## Agile vs Iterative Waterfall Model ⭐High

| Aspect | Iterative Waterfall | Agile |
|---|---|---|
| Sequence | Planned sequence: requirements-capture → analysis → design → coding → testing | Delivery of working versions of the product in several increments |
| Progress measured by | Delivered **artefacts** — requirement specs, design docs, test plans, code reviews, etc. | Delivered **working software increments** |
| Documentation | Heavy | Minimal / "travel light" |

**Similarity:** We can say that **Agile teams use the waterfall model on a small scale** — i.e., within each short increment, a mini requirements → design → code → test sequence still happens.

---

## Agile vs RAD (Rapid Application Development) Model ⭐Medium

| Aspect | Agile | RAD |
|---|---|---|
| Prototyping | **Does NOT recommend developing prototypes** — systematic development of each incremental feature is emphasized | **Based on designing quick-and-dirty prototypes**, which are then refined into production-quality code |

---

## Agile vs Exploratory Programming ⭐Medium

**Similarities:**
- Frequent re-evaluation of plans.
- Emphasis on face-to-face communication.
- Relatively sparse use of documents.

**Key difference:** Agile teams **do follow defined and disciplined processes** and carry out **rigorous designs** — this is in sharp contrast to the **chaotic, ad-hoc coding** typical of exploratory programming.

---

## In-Slide Practice Questions (as posed by the instructor)

- What are the stages of the iterative waterfall model?
- What are the disadvantages of the iterative waterfall model?
- Why has the Agile model become so popular?
- What difficulties might be faced if no life cycle model is followed for a large project?
- Which types of risks can be better handled using the spiral model compared to the prototyping model?
- Which type of process model is suitable for: (a) a customization software, (b) a payroll add-on for contract employees to an existing payroll system?
- Which lifecycle model would you select for upgrading an existing mobile OS (needs 4G compatibility, power minimization, direct cloud backup upload)?
- **Suggest Suitable Life Cycle Model** — an academic institution automation software (course registration/grading, fee collection, staff salary, purchase/inventory) that will be built by tailoring a similar existing product: **70% reuse, 10% new code, 20% modification.** *(Hint: this points toward a reuse-oriented model.)*

---

# Extreme Programming (XP)

## XP: Origins and Naming Rationale ⭐Medium

> **Extreme Programming (XP)** was proposed by **Kent Beck in 1999**.

- The methodology got its name because it **recommends taking best practices to extreme levels**.
- Underlying philosophy: **"If something is good, why not do it all the time?"**

### Taking Good Practices to Extreme ⭐High

| If this practice is good... | ...then take it to the extreme: |
|---|---|
| Code review | Always review → **pair programming** |
| Testing | Continually write & execute test cases → **test-driven development (TDD)** |
| Incremental development | Come up with new increments **every few days** |
| Simplicity | Create the **simplest design** that supports only currently required functionality |
| Design | Everybody designs daily → **refactoring** |
| Architecture | Everybody works at defining/refining the architecture → **metaphor** |
| Integration testing | Build and integrate/test **several times a day** → **continuous integration** |

---

## XP: The 4 Values ⭐High

| Value | Meaning |
|---|---|
| **Communication** | Enhance communication among team members and with customers. |
| **Simplicity** | Build something simple that works today rather than something elaborate that takes time and may never be used; don't over-engineer for tomorrow. |
| **Feedback** | Keeping the system away from users is "trouble waiting to happen" — get feedback early and often. |
| **Courage** | Don't hesitate to discard code that isn't working out. |

---

## XP: Best Practices (Core Trio) ⭐Medium

- **Coding**: Without code, there's no working system — utmost attention must be placed on coding.
- **Testing**: The primary means for developing a fault-free product.
- **Listening**: Careful listening to customers is essential for a good-quality product.

---

## XP Development Activities ⭐High

### XP Planning an Increment
1. Begins by creating **"user stories."**
2. The Agile team assesses each story and **assigns a cost**.
3. A few stories are **grouped into a deliverable increment**.
4. A **delivery date is planned**.

### XP Design
- Follows the **KIS principle** (Keep It Simple).
- Encourages use of **CRC cards** (Class-Responsibility-Collaborator).
- For difficult design problems: suggests creating **"spike solutions"** — a throwaway design prototype.
- Encourages **"refactoring"** — refinement of the internal program design without changing external behavior.

### XP Coding
- Recommends constructing **unit test cases *before* coding commences** → this is **test-driven development (TDD)**.
- Encourages **"pair programming."**

### XP Testing
- **All unit tests are executed daily.**
- **"Acceptance tests"** are defined by the customer and executed to assess customer-visible functionality.

---

## Full List of XP Practices ⭐High

| # | Practice | Description |
|---|---|---|
| 1 | **Planning** | Determine scope of the next release by combining business priorities and technical estimates. |
| 2 | **Small releases** | Put a simple system into production, then release new versions in very short cycles. |
| 3 | **Metaphor** | All development is guided by a simple, shared story of how the whole system works. |
| 4 | **Simple design** | The system is designed to be as simple as possible. |
| 5 | **Testing** | Programmers continuously write and execute unit tests. |
| 6 | **Refactoring** | Programmers continuously restructure the system without changing its behavior, to remove duplication and simplify. |
| 7 | **Pair programming** | All production code is written by **two programmers at one machine.** |
| 8 | **Collective ownership** | Anyone can change any code, anywhere in the system, at any time. |
| 9 | **Continuous integration** | Integrate and build the system **many times a day** — every time a task is completed. |
| 10 | **40-hour week** | Work no more than 40 hours a week, as a rule. |
| 11 | **On-site customer** | A user is part of the team, available full-time to answer questions. |
| 12 | **Coding standards** | Programmers write all code per rules emphasizing communication through the code. |

**Mnemonic idea:** think of these as spanning *Plan → Build → Test → People-rules* — Planning/Small releases/Metaphor/Simple design (plan & design), Testing/Refactoring/Pair programming/Collective ownership/Continuous integration (build & verify), 40-hr week/On-site customer/Coding standards (people & process discipline).

---

## Emphasizes Test-Driven Development (TDD) — the XP Cycle ⭐High

1. Based on the user story, **develop test cases** first.
2. Implement a **quick-and-dirty feature** every couple of days.
3. **Get customer feedback.**
4. **Alter if necessary.**
5. **Refactor.**
6. **Take up the next feature.**

---

## Project Characteristics Suggesting Suitability of XP ⭐Medium

- **Projects involving new technology or research projects** — requirements change rapidly and unforeseen technical problems must be resolved.
- **Small projects** — easily developed using Extreme Programming.

---

# Scrum

## Scrum: Characteristics ⭐High

- One of the Agile processes.
- Relies on **self-organizing teams**.
- Product development progresses in a series of **month-long sprints**.
- Requirements are listed in a **product backlog**.

### Scrum Process Flow (diagram)

```
                     ┌───────────────┐
                     │  Daily Scrum  │
                     │   (loops)     │
                     └───────┬───────┘
                             │
 Product Backlog  --Sprint-->  [ Sprint Backlog ]  --Sprint-->  Product
 (all desired          Planning        │               Review    Increment
  work, prioritized                    ▼
  by Product Owner)              (Sprint executes;
                                  daily scrum loop
                                  runs throughout)
```
Flow: **Product Backlog → (Sprint Planning) → Sprint Backlog → [Daily Scrum loop during the Sprint] → (Sprint Review) → Product Increment.**

---

## Sprint ⭐High

> A **Sprint** is the fundamental process flow of Scrum: a month-long iteration during which an incremental product functionality is completed.

- Scrum projects progress in a series of **"sprints"** — analogous to XP iterations/time-boxes.
- **Target duration is one month.**
- A software increment is **designed, coded, and tested during a sprint**.
- **No changes are entertained during a sprint** — this is a very commonly tested fact.
- **No outside influence can interfere with the Scrum team during the Sprint.**
- Each day begins with the **Daily Scrum Meeting.**

---

## Scrum Framework: Roles, Ceremonies, Artifacts ⭐High

| Category | Items |
|---|---|
| **Roles** | Product Owner, Scrum Master, Team |
| **Ceremonies** | Sprint Planning, Sprint Review, Sprint Retrospective, Daily Scrum Meeting |
| **Artifacts** | Product Backlog, Sprint Backlog, Burndown Chart |

### Key Roles and Responsibilities

**Product Owner**
- Acts on behalf of customers to represent their interests.
- Defines the features of the product.
- Decides on release date and content.
- Prioritizes new features.
- Adjusts features and priority every iteration, as needed.
- Accepts or rejects work results.

**Development Team**
- Team of **five to nine people** with cross-functional skill sets.
- Typically **5–10 people** overall (QA, programmers, UI designers, etc.).
- Teams are **self-organizing**.
- **Membership can change only between sprints** (not mid-sprint).

**Scrum Master** (aka Project Manager)
- Represents management.
- Facilitates the Scrum process and **resolves impediments**.
- Ensures the team is **fully functional and productive**.
- Acts as a **buffer/shield between the team and outside interference**.

---

## Ceremonies (Detail) ⭐High

### Sprint Planning
- Goal: to **produce the Sprint Backlog.**
- **Product Owner** works with the **Team** to negotiate which Backlog Items the Team will work on to meet Release Goals.
- **Scrum Master** ensures the Team agrees to **realistic goals.**

### Daily Scrum ⭐High
- **Daily**, **15-minutes**, **stand-up meeting.**
- **NOT** for problem-solving.
- **NOT** a way to collect information about *who* is behind schedule.
- **IS** a meeting where team members make **informal commitments** to each other and the Scrum Master.
- **IS** a good way for the Scrum Master to track team progress.
- Three standard questions:
  1. What did you do yesterday?
  2. What will you do today?
  3. What obstacles are in your way?

### Sprint Review Meeting
- Team presents what it accomplished during the sprint — typically a **demo of new features**.
- **Informal** (2-hour prep-time rule — minimal preparation expected).
- Participants: Customers, Management, Product Owner, other teammates.

---

## Product Backlog ⭐High

> **Product Backlog**: A list of all desired work on the project, expressed as a prioritized list of Backlog Items.

- Usually a combination of:
  - **Story-based work** (e.g., "allow user to search and replace")
  - **Task-based work** (e.g., "improve exception handling")
- The list is **prioritized by the Product Owner.**
- **Managed and owned by the Product Owner.**
- Typically maintained as a **spreadsheet**, with items grouped by priority (e.g., Very High, High, Medium) and each item having an estimate and an owner.

---

## Sprint Backlog ⭐High

> **Sprint Backlog**: A subset of Product Backlog items that define the work for one Sprint.

- **Created by Team members** (not the Product Owner).
- **Each item has its own status.**
- **Updated daily.**

### Sprint Backlog During the Sprint
- Changes occur:
  - Team **adds new tasks** whenever needed to meet the Sprint Goal.
  - Team **can remove unnecessary tasks.**
  - **But: only the team updates the Sprint Backlog** (not the Product Owner or outsiders).
- **Estimates are updated** whenever there's new information.

---

## Burndown Charts ⭐High

> Burndown charts represent **"work done"** — remarkably simple but effective information disseminators.

Three types:

| Type | Measures |
|---|---|
| **Sprint Burndown Chart** | Progress **within** the current Sprint |
| **Release Burndown Chart** | Progress toward the next **release** |
| **Product Burndown Chart** | Progress of the **whole product** (all releases) |

### Sprint Burndown Chart
- Depicts **total Sprint Backlog hours remaining per day.**
- Shows the estimated amount of time to complete.
- **Ideally burns down to zero** by the end of the Sprint.
- **Usually is NOT a straight line** (work remaining can fluctuate day to day as new tasks are discovered).

```
Hours
remaining
  │╲
  │ ╲_╱╲
  │      ╲_
  │         ╲__
  │            ╲___
  └──────────────────► Days
```

### Release Burndown Chart
- Answers: **Will the next release be done on time? How many more sprints are needed?**
- **X-axis:** Sprints
- **Y-axis:** Amount of story points remaining
- Trend line generally slopes downward toward zero as sprints complete, though it may fluctuate if new stories are added.

### Product Burndown Chart
- A **"big picture"** view of the project's progress across **all releases**.
- Typically overlays **Estimated Burndown**, **Real Burndown**, and **Velocity** across all sprints of the product.

---

## Scalability of Scrum ⭐Low

- A typical Scrum team is **6–10 people.**
- **Jeff Sutherland** proposed and experimented with scaling Scrum to **over 800 people.**
- The scaling mechanism is called **"Scrum of Scrums"**, also known as **"Meta-Scrum."**

---

# Requirements Analysis and Specification (start of next topic — included in this file's slide range)

## What are Requirements? ⭐High

> **A Requirement is:** a capability or condition required from the system.

What's involved in requirements analysis and specification:
- **Gather and Analyze**: Determine what is expected by the client from the system.
- **Document**: Document these in a form that is clear to both the client and the development team members.

---

## Understanding and Specifying Requirements ⭐Medium

- **For toy problems:** understanding and specifying requirements is rather easy.
- **For industry-standard problems:** probably **the hardest, most problematic, and error-prone** among all development tasks.
- The task of requirements specification:
  - **Input**: User needs, hopefully fully understood by the users.
  - **Output**: A precise statement of what the software will do.

---

## Requirements for Generic Products ⭐Low

- When a company plans to develop a **generic product** (not for a specific client), who gives the requirements?
  - **The sales personnel!** — since there is no single client to consult, sales/marketing input drives the requirement set based on market needs.

---

## Activities in Requirements Analysis and Specification (diagram) ⭐High

```
Requirements Gathering
        ⇅
Requirements Analysis
        ⇅
Requirements Specification
        │
        ▼
   SRS Document
```

## Requirements Engineering Process (diagram) ⭐High

```
                    ┌───────────────────────────────────────┐
Feasibility Study ─►│ Requirements   Requirements  Requirements │
        │           │  Gathering  ⇄   Analysis   ⇄ Specification│
        ▼           └────────────────────────┬────────────────┘
Feasibility Report                            │
                                               ▼
                                        SRS Document
```

- **Feasibility Study** happens first, producing a **Feasibility Report**, before requirements gathering formally begins.
- Gathering, Analysis, and Specification are shown with **bidirectional arrows** — they iterate and feed back into each other.

## Requirements Analysis and Specification: Definitions Recap ⭐High

| Activity | Purpose |
|---|---|
| **Requirements Gathering** | Fully understand the user requirements. |
| **Requirements Analysis** | Remove inconsistencies, anomalies, etc. from the gathered requirements. |
| **Requirements Specification** | Document the requirements properly in an **SRS document**. |

---

## Need for SRS (Why a Good SRS Matters) ⭐High

- A **good SRS reduces development cost:**
  - Requirement errors are **expensive to fix later.**
  - Requirement changes cost a lot — **typically 40% of requirements change later** in a project.
  - A good SRS can **minimize changes and errors.**
  - **Substantial savings**: effort spent during the requirements phase saves **multiple times that effort** later.
- **Example — Cost of Fixing Errors Increases Exponentially:**
  - The cost to fix an error introduced during requirements rises steeply if not caught until design, then coding, then acceptance testing, then operation — **the cost curve is exponential**, not linear, across these phases.

```
Cost
  │                                      ╱
  │                                   ╱
  │                              ╱
  │                        ╱
  │              ╱
  │      ╱
  └───────────────────────────────────────► Phase
   Req   Design   Coding   Acc. Testing   Operation
```

---

## Uses of an SRS Document ⭐High

- Establishes the **basis for agreement** between customers and suppliers.
- Forms the **starting point for development.**
- Provides a basis for **estimating costs and schedules.**
- Provides a basis for **validation and verification.**
- Provides a basis for **user manual preparation.**
- Serves as a basis for **later enhancements.**

### SRS as the Basis for a User Manual
- The **User Manual** describes functionality from the **perspective of a user** — an important document for users.
- Typically also describes **how to carry out required tasks**, with examples.

---

## SRS Document: Stakeholders ⭐High

The SRS is intended for a **diverse audience**, each using it differently:

| Stakeholder | Use of the SRS |
|---|---|
| Customers and users | Validation, contract basis |
| Systems (requirements) analysts | Understanding and refining requirements |
| Developers/programmers | Implementing the system |
| Testers | Checking whether requirements have been met |
| Project Managers | Measuring and controlling the project |

- Different levels of **detail and formality** are needed for each audience.
- Companies use different **templates** for requirements specifications — often **variations of IEEE 830.**

## Requirement Process (overall loop, diagram) ⭐High

```
User needs
    │
    ▼
 Gathering ──► Analysis ──► Specification ──► Review ──► SRS Document
    ▲              ▲              ▲              │
    └──────────────┴──────────────┴──────────────┘
     (Specification and review may lead to further
        gathering and analysis — the process loops)
```

---

# Practice Exam (NPTEL Pattern) — 18 Questions

**Instructions:** Attempt all questions before checking the Answer Key. MCQ = single correct option; MSQ = multiple correct options (marked explicitly).

**Q1 (MCQ).** The Agile Manifesto values "Individuals and interactions" over which of the following?
a) Working software
b) Process and tools
c) Customer collaboration
d) Responding to change

**Q2 (MSQ).** Which of the following are principal techniques used in the Agile model?
a) User stories
b) Metaphors
c) Gantt charts
d) Spike solutions

**Q3 (MCQ).** In the Agile model, team size is deliberately kept small, typically in the range of:
a) 2–4 people
b) 5–9 people
c) 10–15 people
d) 20–25 people

**Q4 (MCQ).** According to the Agile model's principles, what is the primary measure of progress?
a) Number of design documents completed
b) Incremental release of working software
c) Number of test cases written
d) Lines of code produced

**Q5 (MSQ).** Which of the following are valid reasons to produce documentation under the Agile model?
a) Project stakeholders require it
b) To define a contract model
c) To fully specify every possible future requirement upfront
d) To support communication with an external group

**Q6 (MCQ).** Identify the correct statement regarding the Agile model versus the iterative Waterfall model:
a) Agile measures progress via delivered artefacts like design documents
b) Waterfall delivers working versions of the product in several increments
c) Agile teams essentially use the waterfall model on a small scale within each increment
d) Waterfall and Agile are identical in their documentation approach

**Q7 (MCQ).** Which of the following best distinguishes Agile from RAD (Rapid Application Development)?
a) Agile recommends quick-and-dirty prototypes; RAD does not
b) RAD is based on designing quick-and-dirty prototypes refined into production code, while Agile emphasizes systematic development of each incremental feature
c) Agile and RAD are the same methodology under different names
d) RAD does not involve any prototyping at all

**Q8 (MSQ).** Which of the following are shortcomings of the Agile model?
a) Sketchy definitions can lead to inconsistent interpretations
b) Requires high-quality people skills
c) Long iterations inhibit short-term perspective
d) Higher risk due to feature creep

**Q9 (MCQ).** Who proposed Extreme Programming (XP), and in what year?
a) Ken Schwaber, 1995
b) Kent Beck, 1999
c) Jeff Sutherland, 2001
d) Alistair Cockburn, 1998

**Q10 (MSQ).** Which of the following are among the "4 Values" of Extreme Programming?
a) Communication
b) Documentation
c) Simplicity
d) Courage

**Q11 (MCQ).** In XP, taking "testing" to the extreme results in which practice?
a) Pair programming
b) Continuous integration
c) Test-driven development (TDD)
d) 40-hour week

**Q12 (MCQ).** Which XP practice states that "all production code is written with two programmers at one machine"?
a) Collective ownership
b) Pair programming
c) On-site customer
d) Coding standards

**Q13 (MSQ).** Which of the following project characteristics suggest suitability of Extreme Programming?
a) Large, well-understood government projects with fixed requirements
b) Projects involving new technology or research
c) Small projects
d) Projects requiring extensive contractual documentation

**Q14 (MCQ).** In Scrum, what is the target duration of a single Sprint?
a) One week
b) Two weeks
c) One month
d) Three months

**Q15 (MSQ).** Which of the following statements about the Daily Scrum meeting are true?
a) It is a 15-minute stand-up meeting
b) It is meant for detailed problem solving
c) It involves answering three standard questions
d) It is a good way for the Scrum Master to track team progress

**Q16 (MCQ).** Who is primarily responsible for prioritizing the Product Backlog?
a) Scrum Master
b) Development Team
c) Product Owner
d) Customer's legal representative

**Q17 (MCQ).** Identify the correct sequence of the Scrum process flow:
a) Sprint Backlog → Product Backlog → Sprint Planning → Product Increment
b) Product Backlog → Sprint Planning → Sprint Backlog → (Daily Scrum during Sprint) → Sprint Review → Product Increment
c) Sprint Review → Sprint Planning → Product Backlog → Sprint Backlog
d) Product Increment → Sprint Backlog → Product Backlog → Sprint Review

**Q18 (MSQ).** Which of the following are valid uses of an SRS document?
a) Basis for agreement between customer and supplier
b) Basis for estimating costs and schedules
c) Replacement for all future communication with the customer
d) Basis for user manual preparation

---

## Answer Key

**Q1: b)** Process and tools. *The Manifesto explicitly favors "Individuals and interactions over process and tools."*

**Q2: a, b, d.** User stories, Metaphors, and Spike solutions are all principal Agile techniques; Gantt charts belong to traditional plan-driven project management, not Agile's lightweight technique set.

**Q3: b) 5–9 people.** The slides explicitly state team size is kept small (5–9) to enable face-to-face communication in a shared office space.

**Q4: b)** Incremental release of working software is explicitly stated as the primary measure of progress in Agile.

**Q5: a, b, d.** These are the stated valid reasons to document under Agile; "fully specifying every future requirement upfront" contradicts Agile's "travel light" philosophy.

**Q6: c)** Agile teams use the waterfall model on a small scale — within each short increment, a mini requirements→design→code→test cycle still occurs; this is the explicitly stated similarity.

**Q7: b)** This is the exact contrast given in the slides: RAD relies on quick-and-dirty prototypes refined into production quality code, whereas Agile emphasizes systematic development of each incremental feature without prototyping.

**Q8: a, b, d.** These are stated Adoption Detractors/Shortcomings. Option (c) is incorrect because it is **short** iterations (not long) that inhibit **long-term** (not short-term) perspective.

**Q9: b)** Kent Beck proposed XP in 1999.

**Q10: a, c, d.** Communication, Simplicity, Feedback, and Courage are the 4 Values. "Documentation" is not one of them — in fact Agile/XP explicitly de-emphasizes heavy documentation.

**Q11: c)** "If testing is good, continually write and execute test cases" is taken to the extreme as test-driven development.

**Q12: b)** Pair programming is defined exactly this way in the Full List of XP Practices.

**Q13: b, c.** New-technology/research projects (rapidly changing requirements, unforeseen technical problems) and small projects are explicitly stated as suited to XP; large fixed-requirement government projects and heavy contractual documentation needs are poor fits for XP's lightweight, adaptive style.

**Q14: c)** One month is the stated target duration for a Scrum Sprint.

**Q15: a, c, d.** The Daily Scrum is a 15-minute stand-up with three standard questions, useful for the Scrum Master to track progress. It is explicitly stated to be **NOT** a problem-solving session, so (b) is false.

**Q16: c)** The Product Owner defines features, decides release date/content, and prioritizes the Product Backlog.

**Q17: b)** This matches the process flow diagram: Product Backlog → Sprint Planning → Sprint Backlog → (Daily Scrum loop during the Sprint) → Sprint Review → Product Increment.

**Q18: a, b, d.** These are explicitly listed uses of an SRS. An SRS does not replace all future communication — requirements can still evolve and need discussion (option c is false).
