# 📘 Software Engineering — NPTEL Exam Notes
**Course:** Software Engineering by Prof. Rajib Mall, IIT Kharagpur
**Week:** 1 | **Topics:** Introduction, Software Crisis, Complexity, Design Evolution, Life Cycle Models

---

## Topic 1: What is Software Engineering? 📅 Week 1

### 1. 🔑 Key Definitions Box

> **Software Engineering (IEEE):** "The application of a systematic, disciplined, quantifiable approach to the development, operation, and maintenance of software; that is, the application of engineering to software."

> **Exploratory (Build-and-Fix) Style:** A style of software development where a "dirty" program is quickly written and bugs are fixed as and when noticed — no planning or systematic process.

> **Software Crisis:** The recurring situation where software products fail to meet requirements, are expensive, hard to maintain, delivered late, and use resources non-optimally.

---

### 2. Concept Explanation

Software engineering applies the same disciplined, systematic approach that civil/mechanical engineers use — but for building software. Just as an architect doesn't "build and fix" a skyscraper, a software engineer doesn't just start typing code and hope it works.

The field arose because of the **Software Crisis** — programs were growing in size and complexity, but development methods hadn't kept up. Projects were cancelled, delayed, or failed to satisfy users. The Standish Group Report showed only **28% of software projects are successful**, 49% are delayed or over budget, and 23% are cancelled.

Software engineering systematically collects **past experience** (in the form of techniques, methodologies, and guidelines) to avoid reinventing the wheel and repeating old mistakes.

---

### 3. Comparison Table

| Feature | Exploratory Style | Software Engineering Approach |
|---|---|---|
| Planning | None — start coding immediately | Systematic phases (requirements, design, code, test) |
| Error Detection | Only during testing | At each phase (error prevention focus) |
| Team Suitability | Only solo/very small projects | Essential for team development |
| Code Maintainability | Unmaintainable | Maintainable by design |
| Documentation | Minimal or none | Full documentation at each phase |
| Effort vs. Size | Exponential growth | Near-linear growth |
| Basis | Intuition | Scientific techniques + past experience |

---

### 4. 🧠 Mnemonic

**"SE Fixes the CRUDE mess"**
**C**risis → **R**equirements missed → **U**nder budget fails → **D**ue dates missed → **E**xpensive

*(Software Engineering addresses all these CRUDE problems of the software crisis)*

---

### 5. MCQ Trap Patterns

- ❌ Software is easier to develop than hardware, so it's always cheaper → ✅ Software costs have grown dramatically; today software can cost far more than hardware (e.g., Rational Suite: ₹6 lakh vs Laptop: ₹45K).
- ❌ Exploratory style works fine for medium-sized projects → ✅ Exploratory style only works for very small (toy) programs; effort grows exponentially with size.
- ❌ The IEEE definition says SE is about only development → ✅ IEEE definition covers development, **operation, and maintenance**.
- ❌ Software crisis is caused mainly by bad programmers → ✅ Causes include larger problems, poor project management, lack of SE training, skill shortage, low productivity improvement.
- ❌ 23% of projects are successful per the Standish Group → ✅ **28%** are successful; **23%** are cancelled; **49%** are delayed or over budget.

---

### 6. Quick Recall

- SE = Engineering approach + systematic collection of past experience (techniques, methodologies, guidelines)
- Software crisis symptoms: fails requirements, expensive, difficult to alter/debug, delivered late, resources wasted
- Standish Group: 28% success / 49% delayed / 23% cancelled
- Exploratory style = build-and-fix = suitable for toy programs only
- Effort grows **exponentially** with program size under exploratory style, **nearly linearly** with SE techniques

---

## Topic 2: Human Cognition & Complexity 📅 Week 1

### 1. 🔑 Key Definitions Box

> **Short-Term Memory (STM):** The active, working part of human memory that holds items for a few tens of seconds. Susceptible to decay over time or displacement by new information.

> **Long-Term Memory (LTM):** The permanent storage part of human memory from which items are fetched into STM for processing.

> **Item (in memory):** Any set of related information that occupies one place in short-term memory (e.g., a character, a word, a sentence, or even a picture).

> **Chunking:** The cognitive technique of grouping related items together so that multiple pieces of information occupy only one slot in short-term memory.

> **The Magical Number 7 (Miller's Law):** Humans can hold approximately 7 (±2) items in short-term memory at one time; beyond this, comprehension becomes exceedingly difficult.

---

### 2. Concept Explanation

George Miller (1956) identified that human short-term memory can hold roughly **7 items** simultaneously. This is why large programs become difficult — a program with many independent variables quickly exceeds what a human brain can grasp.

Under exploratory style, as program size grows, the programmer must mentally juggle more variables, interactions, and states than the STM can handle — causing **exponential growth in effort**. A machine writing programs wouldn't face this limitation, so its effort would grow linearly.

Software engineering solves this through **abstraction** and **decomposition** — techniques specifically designed to respect human cognitive limits.

---

### 3. Comparison Table

| Memory Type | Duration | Capacity | Function |
|---|---|---|---|
| Short-Term Memory | Seconds to minutes | ~7 items | Active processing/computation |
| Long-Term Memory | Permanent | Very large | Storage of known facts/patterns |

| Technique | What It Does | SE Application |
|---|---|---|
| Chunking | Groups related items into one slot | Modules, classes, packages |
| Abstraction | Hides irrelevant details | UML models, diagrams |
| Decomposition | Breaks problem into independent parts | Modules, functions, layers |

---

### 4. 🧠 Mnemonic

**"7 Items, 2 Tools"**
STM holds ~**7** items → solved by **2** key tools: **A**bstraction + **D**ecomposition

---

### 5. MCQ Trap Patterns

- ❌ Chunking increases the number of items in short-term memory → ✅ Chunking **reduces** the number of slots used by grouping related items.
- ❌ Long-term memory is the bottleneck in software development → ✅ **Short-term memory** is the bottleneck — its capacity of ~7 items limits how much of a program a developer can understand at once.
- ❌ Miller's law says humans can hold exactly 7 items in memory → ✅ Miller's number is 7 **± 2** (i.e., 5 to 9 items).
- ❌ Increasing team size linearly reduces the cognitive load per member → ✅ Team development introduces coordination and communication overhead; it isn't a simple linear gain.
- ❌ Abstraction and decomposition are just coding techniques → ✅ They are **cognitive techniques** deployed by SE to overcome human memory limitations; applicable at design, requirements, and architecture stages.

---

### 6. Quick Recall

- STM: ~7 items, lasts seconds, displaced by new info
- Chunking: grouping items so they occupy fewer STM slots
- Magical number 7 → beyond 7 items, understanding breaks down
- SE principles (abstraction + decomposition) keep effort-size curve near-linear
- Without SE, effort grows exponentially with size due to STM limits

---

## Topic 3: Abstraction & Decomposition 📅 Week 1

### 1. 🔑 Key Definitions Box

> **Abstraction:** Simplifying a problem by omitting unnecessary details and focusing on one relevant aspect at a time. Also called **model building**.

> **Decomposition:** Breaking a complex problem into many small, more-or-less **independent** parts that can be solved separately.

> **Hierarchy of Abstractions:** For complex problems, a single abstraction level is insufficient — multiple layers of models are built, where each layer is an abstraction of the layer below it.

> **Model:** An abstract representation of a system focusing on specific aspects while ignoring irrelevant details.

---

### 2. Concept Explanation

**Abstraction** is like studying a country via different types of maps (political map, physical map, road map) rather than visiting every house. Each map is an abstract model that highlights specific features. Multiple abstractions of the same problem are possible — different models reveal different aspects.

**Decomposition** is like breaking a bundle of sticks one-by-one instead of all together. A book is also a good example — chapters are decomposed, independent units that together form the whole. The critical rule is that decomposed parts must be **more or less independent** of each other; arbitrary decomposition doesn't help.

Both techniques directly address the 7-item STM limit — abstraction reduces the number of details visible at once, and decomposition ensures each part is small enough to fit in STM.

---

### 3. Comparison Table

| Aspect | Abstraction | Decomposition |
|---|---|---|
| What it does | Hides irrelevant details; focuses on one aspect | Breaks whole into small, independent parts |
| Goal | Simplify understanding | Divide and conquer |
| Analogy | Different types of maps of a country | Breaking a bundle of sticks one by one |
| Multiple versions? | Yes — different abstractions for different aspects | Yes — different ways to decompose |
| SE example | UML diagrams, DFDs, ER diagrams | Modules, functions, subsystems |
| Works alone? | Yes | Yes — but decomposed parts must be independent |

---

### 4. 🧠 Mnemonic

**"A MAP is an Abstraction; A BOOK is Decomposition"**
- **Map** → focuses on one aspect (political/road/physical) = **Abstraction**
- **Book chapters** → independent units that form the whole = **Decomposition**

---

### 5. MCQ Trap Patterns

- ❌ Abstraction means ignoring all details of a problem → ✅ Abstraction means ignoring **irrelevant** details while focusing on **one specific aspect**.
- ❌ Decomposition works even when parts are interdependent → ✅ Decomposed parts must be **more or less independent**; arbitrary decomposition doesn't help.
- ❌ A single abstraction is sufficient for any complex problem → ✅ Complex problems require a **hierarchy of abstractions** — multiple layers.
- ❌ Decomposition and abstraction are alternatives — you use one or the other → ✅ Both are used together and complement each other in SE.
- ❌ Abstraction is a programming technique only → ✅ Abstraction is a **cognitive technique** used at every stage — requirements, design, architecture.

---

### 6. Quick Recall

- Abstraction = model building = focus on one aspect, ignore irrelevant details
- Multiple abstractions of same problem = possible and useful
- Complex problems need a **hierarchy** of abstractions
- Decomposition = divide into independent parts, solve separately
- Parts must be independent — arbitrary decomposition is useless
- Both overcome the 7-item STM limit

---

## Topic 4: Evolution of Software Design Techniques 📅 Week 1

### 1. 🔑 Key Definitions Box

> **Structured Programming:** A programming methodology using only three constructs — **sequence**, **selection (if-then-else)**, and **iteration (loops)** — and avoiding GOTO statements. Programs are organized into modules.

> **Control Flow-Based Design:** Design technique (late 1960s) focusing on a program's control structure — the sequence in which instructions are executed. Used flow charts.

> **Spaghetti Code:** Unstructured, messy code resulting from excessive use of GOTO statements, resembling tangled spaghetti in its control flow.

> **Data Structure-Oriented Design:** Design technique (early 1970s) that derives program structure from data structure design. Example: Jackson's Structured Programming (JSP).

> **Data Flow-Oriented Design:** Design technique (late 1970s) that first identifies data flowing through a system and the processing stations (functions) that transform that data.

> **Object-Oriented Design (OOD):** Design technique (1980s) that identifies natural objects in a problem, their attributes, relationships (composition, reference, inheritance), and behavior. Objects act as data-hiding entities.

> **JSP (Jackson's Structured Programming):** A data structure-oriented design methodology developed by Michael Jackson in the 1970s; program code structure should correspond to the data structure.

---

### 2. Concept Explanation

Software design techniques evolved in response to increasing program sizes:

- **1950s (Ad hoc/Exploratory):** Assembly language, few hundred lines, pure build-and-fix.
- **Early 1960s (High-Level Languages):** FORTRAN, ALGOL, COBOL — reduced effort but style still exploratory. Program sizes ~few thousand lines.
- **Late 1960s (Control Flow):** Programs grew larger; experienced programmers focused on "pay attention to control structure." Flow charts emerged. Dijkstra's "GOTO Considered Harmful" (1969) sparked the Structured Programming revolution. Proved: any logic expressible with just sequence + selection + iteration.
- **Early 1970s (Data Structure):** Programs grew larger still; attention shifted to designing data structures first, then deriving program structure. JSP by Michael Jackson.
- **Late 1970s (Data Flow):** DFD-based approach — identify inputs, processing stations (functions), outputs, and data flowing between them. Generic and simple.
- **1980s (Object-Oriented):** OOD gained wide acceptance for simplicity, reuse, lower cost, robustness, and easy maintenance.
- **Beyond OO:** Component-based, Aspect-oriented, Service-oriented design.

---

### 3. Comparison Table

| Era | Technique | Key Focus | Example Tool/Method |
|---|---|---|---|
| 1950s | Ad hoc (Exploratory) | Write & fix | Assembly language |
| Early 1960s | High-Level Language | Reduce coding effort | FORTRAN, COBOL |
| Late 1960s | Control Flow-Based | Program control structure | Flow charts, Structured Prog. |
| Early 1970s | Data Structure-Oriented | Data structure drives code | JSP (Michael Jackson), Warnier-Orr |
| Late 1970s | Data Flow-Oriented | Data + processing stations | DFD (Data Flow Diagrams) |
| 1980s | Object-Oriented | Real-world objects + relationships | UML, OOP languages |
| 1990s+ | Component / Aspect / Service | Reuse, modularity, services | CBD, SOA |

---

### 4. 🧠 Mnemonic

**"Ex-HiC-DSO-DO-OO"** → (Evolution order)

**Ex**ploratory → **Hi**gh-Level Language → **C**ontrol Flow → **D**ata **S**tructure → **D**ata Fl**o**w → **O**bject-**O**riented

Or tell a story: *"Even High schoolers Can Do Some Outstanding Object-Oriented code"*

---

### 5. MCQ Trap Patterns

- ❌ Dijkstra proved GOTO statements are always wrong → ✅ Dijkstra showed GOTO is **harmful** and unnecessary; only sequence, selection, iteration are sufficient. Violations are occasionally **permitted** (e.g., break, exception handling).
- ❌ JSP was developed by James Jackson → ✅ JSP (Jackson's Structured Programming) was developed by **Michael** Jackson in the **1970s**.
- ❌ Data flow-oriented design can only be used for software systems → ✅ Data flow is a **generic technique** applicable to any system (not just software), e.g., a car assembly unit.
- ❌ Object-Oriented design came before Data Flow-Oriented design → ✅ Data Flow (late 70s) → OOD (1980s). OO came **after**.
- ❌ Structured programming eliminates all GOTO use absolutely → ✅ Structured programming **discourages** GOTO but permits violations for practical reasons (break, exception handling).
- ❌ Control flow design focuses on data items in a system → ✅ Control flow focuses on the **sequence of instruction execution**; data-flow design focuses on data items.

---

### 6. Quick Recall

- Structured programming: sequence + selection + iteration only — NO GOTO
- Dijkstra's paper: "GOTO Statement Considered Harmful" — ACM 1969
- Spaghetti code = result of excessive GOTO usage
- JSP = data structure-oriented; Michael Jackson; 1970s
- Data flow = identifies processing stations and data flowing between them
- OOD = objects + inheritance + composition + data hiding; 1980s
- Advantages of OOD: simplicity, reuse, lower cost, robustness, easy maintenance
- Evolution order: Exploratory → HLL → Control Flow → Data Structure → Data Flow → OO → Component/Aspect/Service

---

## Topic 5: Life Cycle Models 📅 Week 1

### 1. 🔑 Key Definitions Box

> **Software Life Cycle (Software Process):** A series of identifiable stages a software product undergoes during its lifetime: Feasibility Study → Requirements Analysis & Specification → Design → Coding → Testing → Maintenance.

> **Life Cycle Model (Process Model / SDLC):** A descriptive and diagrammatic model of the software life cycle that identifies all activities, establishes precedence ordering among activities, and divides the life cycle into phases.

> **Phase Entry Criteria:** Conditions that must be satisfied before a phase can begin.

> **Phase Exit Criteria:** Conditions that must be satisfied before a phase is considered complete and the next phase can begin.

> **Milestone:** A significant event in a project — phase entry and exit are important milestones that help managers track project progress.

> **99% Complete Syndrome:** A project management problem where, without a life cycle model, the project appears perpetually "almost done" because progress is based on team members' guesses.

> **Software Development Methodology:** The guidelines and methodologies (for specification, design, testing, project management, etc.) defined by an organization for its software development process.

> **Visibility:** Production of good quality, consistent, and standard documents at each phase — makes project management easier and enables fault diagnosis and maintenance.

> **Classical Waterfall Model:** The simplest and most intuitive life cycle model — phases flow strictly downward: Feasibility Study → Requirements Analysis → Design → Coding & Unit Testing → Integration & System Testing → Maintenance.

---

### 2. Concept Explanation

A **life cycle model** gives the entire development team a shared understanding of **"when to do what"**. Without it, engineers work independently and chaotically — one starts coding, another writes test plans, another defines file structures — leading to project failure.

The life cycle model enforces **discipline**: a phase only starts when entry criteria are met, and only ends when exit criteria are satisfied. For example, the Requirements phase exits only when the **SRS (Software Requirements Specification)** document is complete, reviewed, and customer-approved.

Milestones (especially phase entry/exit points) allow project managers to track progress accurately. Without a model, the only way to know project status is to ask team members — which produces the dangerous **99% complete syndrome**.

**Visibility** is a key modern improvement — producing standard, consistent documents at every phase so that fault diagnosis and maintenance become manageable, not mysteries.

---

### 3. Comparison Table — With vs. Without Life Cycle Model

| Aspect | With Life Cycle Model | Without Life Cycle Model |
|---|---|---|
| Progress Tracking | Manager can tell exact phase | Depends on team guesses |
| Discipline | Structured, phase-by-phase | Chaotic, ad hoc |
| Team Coordination | Clear entry/exit criteria | Engineers work out of sync |
| 99% Syndrome | Avoided | Very likely to occur |
| Deliverables | Standard docs at each phase | Only the final working program (myth) |

---

### 3b. Classical Waterfall Model — Phases & Relative Effort

| Phase | Description | Relative Effort |
|---|---|---|
| Feasibility Study | Is it worth building? Technical + financial assessment | Low |
| Requirements Analysis & Specification | What does the customer need? → SRS document | Medium |
| Design | How to build it? System + detailed design | Medium-High |
| Coding & Unit Testing | Write and unit-test each module | Medium |
| Integration & System Testing | Assemble and test the whole system | **Highest among development phases** |
| Maintenance | Enhance, fix, adapt post-delivery | **Highest overall** |

> **Key fact:** Among all phases, **Maintenance** consumes the most effort. Among **development** phases, **Testing** consumes the most effort.

---

### 3c. Life Cycle Models Overview

| Model | Type | Characteristics |
|---|---|---|
| Classical Waterfall | Traditional | Phases flow strictly top-down; simple; no iteration |
| V Model | Traditional | Test planning done in parallel with each development phase |
| Evolutionary | Traditional | Iterative refinement of requirements + design |
| Prototyping | Traditional | Build a prototype first; refine requirements |
| Spiral | Traditional | Risk-driven; iterates through four quadrants |
| Agile | Modern | Incremental delivery; customer collaboration; adaptive |

---

### 4. 🧠 Mnemonic

**Waterfall phases → "Frank Really Designed Codes That Must"**
**F**easibility → **R**equirements → **D**esign → **C**oding → **T**esting → **M**aintenance

And for effort: **"Maintenance Matters Most; Testing is Toughest in Development"**

---

### 5. MCQ Trap Patterns

- ❌ The only deliverable in a software project is the final working program → ✅ **Myth!** Documentation of all aspects (at every phase) is needed for operation and maintenance.
- ❌ A phase can start whenever the team decides → ✅ A phase can start **only if its entry criteria have been satisfied**.
- ❌ Testing consumes the maximum effort among all phases → ✅ Testing is maximum among **development phases** only; **Maintenance** consumes the most effort overall.
- ❌ Life cycle models are only needed for large teams → ✅ They are needed whenever **a team** develops software; a single programmer has the freedom of exploratory model.
- ❌ The 99% complete syndrome means a project is almost done → ✅ It means progress reporting is unreliable — the project appears perpetually near-complete because it's based on guesses.
- ❌ Visibility means UI/UX of the software → ✅ In SE, visibility means **good quality, consistent, standard documentation** produced at each phase.
- ❌ The Classical Waterfall Model allows phases to overlap → ✅ In the classical waterfall, phases flow **strictly sequentially** — one must complete before the next begins.

---

### 6. Quick Recall

- Life cycle model = SDLC = process model = descriptive + diagrammatic
- 3 purposes of life cycle model: common understanding / identify inconsistencies / tailoring for specific projects
- Phase entry/exit criteria = mandatory gates
- Milestones = phase entry/exit points (key for tracking)
- 99% complete syndrome = problem without life cycle model
- Visibility = standard, consistent documents at every phase
- Waterfall phases: Feasibility → Req → Design → Code → Test → Maintenance
- Max effort overall: **Maintenance**; max among development: **Testing**
- SRS complete + reviewed + customer-approved = exit criteria for Requirements phase
- Software development methodology = org's guidelines for spec/design/testing/PM

---

## Topic 6: Feasibility Study 📅 Week 1

### 1. 🔑 Key Definitions Box

> **Feasibility Study:** The first phase of the software life cycle. Its main aim is to determine whether developing the software is **financially worthwhile** and **technically feasible**.

> **Economic Feasibility (Cost/Benefit Feasibility):** Determination of whether the benefits of the system outweigh its costs (development + set-up + operational costs).

> **Technical Feasibility:** Assessment of whether the required technology, tools, and expertise exist to build the system.

> **Schedule Feasibility:** Assessment of whether the project can be completed within the required time frame.

> **Cost-Benefit Analysis (CBA):** Identifying all costs (development, set-up, operational) and all benefits (quantifiable and non-quantifiable) to determine if benefits outweigh costs.

> **Go/No-Go Decision:** The output of the feasibility study — proceed with the project or abandon it.

---

### 2. Concept Explanation

The feasibility study happens **before** committing major resources. A manager roughly understands what the customer wants (inputs, processing, outputs, constraints) and formulates **different solution strategies** — not just one. Each alternative is examined for resources required, cost, and development time.

A **cost/benefit analysis** is then performed to pick the best solution. It may also conclude that **none** of the solutions is feasible (high cost, resource constraints, or technical impossibility).

The three dimensions of feasibility are **Economic + Technical + Schedule**. Organizations present the findings to the client for the **Go/No-Go decision** before proceeding to requirements analysis.

---

### 3. Comparison Table

| Feasibility Dimension | Question Asked | Example |
|---|---|---|
| Economic (Cost/Benefit) | Are benefits > costs? | Will the payroll system save more than it costs to build? |
| Technical | Can we build it with current tech? | Is the required hardware/software available? |
| Schedule | Can we finish on time? | Can we deliver by the client's deadline? |

| Cost Types | Benefit Types |
|---|---|
| Development costs | Quantifiable (time saved, error reduction) |
| Set-up costs | Non-quantifiable (better decisions, reputation) |
| Operational costs | — |

---

### 4. 🧠 Mnemonic

**"ETS = Every Team Should (do feasibility)"**
**E**conomic + **T**echnical + **S**chedule = 3 feasibility dimensions

---

### 5. MCQ Trap Patterns

- ❌ Feasibility study determines the exact requirements of the system → ✅ Feasibility study only **roughly** understands requirements — exact requirements come in the **Requirements Analysis** phase.
- ❌ A feasibility study always recommends proceeding with development → ✅ Feasibility study may conclude **none** of the solutions is feasible.
- ❌ The output of the feasibility study is the SRS document → ✅ The SRS is the output of the **Requirements Analysis** phase; feasibility study produces a **feasibility report / Go-No-Go decision**.
- ❌ Only financial aspects are considered in feasibility → ✅ Three dimensions: **Economic, Technical, and Schedule** feasibility.
- ❌ During feasibility study, only one solution strategy is considered → ✅ **Multiple** alternate solution strategies are formulated and compared.

---

### 6. Quick Recall

- Feasibility study = first phase = determines if software is worth building
- 3 dimensions: Economic + Technical + Schedule
- CBA: identify all costs (dev + set-up + operational) vs. benefits (quantifiable + non-quantifiable)
- Alternate solutions are formulated and compared — best one chosen
- May conclude no feasible solution exists
- Output: Go/No-Go decision (presented to client)
- Feasibility study ≠ Requirements Analysis (it only roughly understands the problem)

---

## 🎯 Practice MCQ / MSQ (NPTEL Style)

---

**Q1.** According to the IEEE definition, software engineering is the application of systematic, disciplined, quantifiable approach to which of the following?

- (A) Development of software only
- (B) Development and testing of software
- (C) Development, operation, and maintenance of software
- (D) Design and coding of software

> ✅ **Answer: (C)** — The IEEE definition explicitly covers **development, operation, and maintenance**. "Only development" is a common wrong option.

---

**Q2.** According to the Standish Group report, approximately what percentage of software projects are cancelled?

- (A) 28%
- (B) 49%
- (C) 23%
- (D) 35%

> ✅ **Answer: (C)** — 23% cancelled, 28% successful, 49% delayed or over budget. These exact numbers are frequently tested.

---

**Q3.** Which of the following is/are characteristics of the Exploratory (build-and-fix) style? *(MSQ — select all that apply)*

- (A) A dirty program is quickly developed and bugs fixed as noticed
- (B) Suitable for very small (toy) programs only
- (C) Results in maintainable, well-structured code
- (D) Leads to exponential growth of effort with program size
- (E) Suitable for team development environments

> ✅ **Answer: (A), (B), (D)** — Exploratory style produces unmaintainable code (not C) and is unsuitable for team environments (not E).

---

**Q4.** The "Magical Number 7" in the context of software engineering refers to:

- (A) The maximum number of developers in an agile team
- (B) The number of phases in the waterfall model
- (C) The approximate capacity of human short-term memory in items
- (D) The number of structured programming constructs

> ✅ **Answer: (C)** — Miller (1956) established that STM holds approximately 7 (±2) items. This directly explains why large programs are cognitively difficult.

---

**Q5.** Which of the following are the two fundamental techniques used by software engineering to overcome human cognitive limitations?

- (A) Debugging and Testing
- (B) Abstraction and Decomposition
- (C) Modularization and Compilation
- (D) Verification and Validation

> ✅ **Answer: (B)** — Abstraction (model building) and Decomposition are the two key principles explicitly identified by Prof. Mall as addressing STM limits.

---

**Q6.** Jackson's Structured Programming (JSP) belongs to which category of design techniques?

- (A) Control flow-based design
- (B) Object-oriented design
- (C) Data flow-oriented design
- (D) Data structure-oriented design

> ✅ **Answer: (D)** — JSP was developed by Michael Jackson in the 1970s and is a data **structure**-oriented technique where program code structure corresponds to data structure.

---

**Q7.** Dijkstra's landmark paper "GOTO Statement Considered Harmful" was published in:

- (A) 1960
- (B) 1965
- (C) 1969
- (D) 1975

> ✅ **Answer: (C)** — Dijkstra's paper was published in **Communications of ACM, 1969**, and formed the basis of structured programming.

---

**Q8.** Which of the following statements about the Classical Waterfall Model are TRUE? *(MSQ)*

- (A) Maintenance phase consumes the maximum effort among all phases
- (B) Testing phase consumes the maximum effort among development phases
- (C) Phases can be executed in any order
- (D) Phase entry and exit criteria are defined for each phase
- (E) Only the working program is the project deliverable

> ✅ **Answer: (A), (B), (D)** — (C) is wrong: phases flow strictly sequentially in classical waterfall. (E) is a myth — documentation is equally important.

---

**Q9.** The "99% complete syndrome" in software project management refers to:

- (A) Projects that are nearly complete and require only minor work
- (B) Projects that appear perpetually near-complete due to unreliable progress estimates when no life cycle model is followed
- (C) A metric that measures project completion percentage
- (D) Projects that deliver 99% of required features but skip maintenance

> ✅ **Answer: (B)** — Without a life cycle model, progress reporting relies on team members' guesses, creating the illusion of being "almost done" indefinitely.

---

**Q10.** Which of the following are dimensions assessed during the Feasibility Study? *(MSQ)*

- (A) Economic (Cost/Benefit) feasibility
- (B) User interface feasibility
- (C) Technical feasibility
- (D) Schedule feasibility
- (E) Code quality feasibility

> ✅ **Answer: (A), (C), (D)** — The three standard dimensions of feasibility are Economic, Technical, and Schedule. UI and code quality assessments are not feasibility dimensions.

---

*Notes compiled from: NPTEL Software Engineering — Week 1 slides by Prof. Rajib Mall, IIT Kharagpur*
*Prepared for: MCQ/MSQ exam preparation — Saurabh, MCA 2025–27, BCIT/GGSIP*
