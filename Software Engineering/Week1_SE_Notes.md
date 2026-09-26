# Week 1: Introduction to Software Engineering

**Most historically emphasized topics for this week (NPTEL SE pattern):**
- Exploratory style — why it fails, and the exponential effort-vs-size curve
- Abstraction and Decomposition (definitions + examples)
- The GOTO controversy and Structured Programming
- Classical Waterfall Model phases and relative effort (maintenance/testing)
- Feasibility study — the three feasibility dimensions and CBA

---

## 1. What is Software Engineering? ⭐High

> **IEEE Definition:** "Software engineering is the application of a systematic, disciplined, quantifiable approach to the development, operation, and maintenance of software; that is, the application of engineering to software."

- SE is an **engineering approach** to developing software — analogous to building construction, where established methods replace ad hoc effort.
- It represents the **systematic collection of past experience**, organized into:
  - Techniques
  - Methodologies
  - Guidelines
- The core idea: software development should not depend purely on individual talent or intuition — it should follow repeatable, disciplined processes.

## 2. The Software Crisis ⭐High

Historically, software products commonly:
- Fail to meet user requirements
- Are expensive to build and maintain
- Are difficult to alter, debug, and enhance
- Are often delivered late
- Use resources (time, memory, manpower) non-optimally

**Relative Cost of Hardware vs Software (1960 → 2018):**
- In 1960, hardware dominated total project cost; software was a minor line item.
- By 2018, this inverted sharply — software costs (e.g., licensing suites) far exceed hardware costs (laptop/desktop). The slides give a concrete example: a laptop (~₹45,000) vs. a node-locked Rational Suite license (~₹3,14,600) vs. a floating license (~₹6,03,200).
- **Exam takeaway:** the crossover shows software, not hardware, became the dominant cost driver over time — a key reason SE as a discipline became necessary.

**Standish Group Report (classic exam statistic):**
- 28% of projects: Successful
- 49% of projects: Delayed or cost overrun
- 23% of projects: Cancelled

**Factors contributing to the software crisis:**
1. Larger, more complex problems being attempted
2. Poor project management
3. Lack of adequate training in software engineering
4. Increasing skill shortage
5. Low productivity improvements relative to demand

## 3. Programming: An Art or Engineering? ⭐Medium

The slides frame this as an evolution along two axes — "esoteric past experience" (craft/art) moving toward "engineering" via systematic technology development over time.

| Aspect | Art (craft) | Engineering |
|---|---|---|
| Use of past experience | Unorganized | Systematically arranged |
| Basis | Intuition, thumb rules | Theoretical basis + quantitative techniques |
| Decision-making | Ad hoc | Tradeoffs between alternatives, cost-effectiveness driven |
| Applicability | Works for small/toy problems | Scales to large, complex problems |

- Programming still retains "art" elements (many rules are thumb rules, tradeoffs are judgment calls), but SE tries to give it an **engineering discipline** on top.

## 4. Exploratory (Build-and-Fix) Style ⭐High

- Early programmers used the **exploratory style** (also called **build-and-fix**):
  - A "dirty" program is quickly developed.
  - Bugs are fixed as and when noticed.
  - Analogous to how a beginner/junior student writes code — no upfront planning.

```
        ┌────────┐
        │ Initial│
        │ Coding │
        └───┬────┘
            │
            ▼
        ┌────────┐
        │  Test  │◄────┐
        └───┬────┘     │
            │           │
            ▼           │
        ┌────────┐     │
        │  Fix   │─────┘
        └────────┘
     (Do Until Done)
```

**Why the exploratory style fails for non-trivial projects:**
- Effort, time, and cost grow **exponentially** with program size under the exploratory approach — vs. an ideal linear growth if a machine were generating the program.
- Two curves are contrasted in the slides: "Exploratory" (steep, exponential) vs. "Machine" (linear) — Software Engineering aims to pull the real curve as close to linear as possible.

```
Effort
  │                          ,•  Exploratory (exponential)
  │                       ,•'
  │                    ,•'
  │                ,•'          .··  Software Engineering (flatter)
  │            ,•'          .··'
  │        ,•'         .··'
  │    ,•'        .··'  _____________ Machine (near-linear)
  │_.•'___.··'____________________________
  └───────────────────────────────► Program Size
```

- Besides exponential cost growth, exploratory style causes:
  - Unmaintainable code
  - Serious difficulty in **team development** environments (no shared structure/understanding)

## 5. Human Cognition & Why Exploratory Style Breaks Down ⭐High

This is the *conceptual justification* for why SE techniques exist — a favorite source of "why" questions.

- Human memory is modeled as two parts (Miller, 1956):
  - **Short-term memory (STM)**
  - **Long-term memory (LTM)**

```
   ┌───────────────────┐
   │ Short Term Memory │
   └─────────┬─────────┘
             │
             ▼
   ┌───────────────────┐
   │  Processing Center │
   └─────────┬─────────┘
             ▲
             │
   ┌───────────────────┐
   │  Long Term Memory  │
   └───────────────────┘
          (Brain)
```

- **Example given:** "It's 10:10 AM, how many hours remain today?" → "10 AM" is held in STM, "a day is 24 hours" is fetched from LTM into STM, and the processing center computes 24−10.

**Properties of short-term memory:**
- An item stored in STM can be lost via:
  - **Decay** with time, or
  - **Displacement** by newer information
- Items are typically retained only a **few tens of seconds** in STM unless actively recycled/rehearsed.

**What counts as an "item"?**
- Any set of related information: a character, a digit, a word, a sentence, a story, even a picture.
- Each item normally occupies **one slot** in memory.
- **Chunking:** when several related items are grouped together, they can be treated as occupying just *one* memory slot instead of several — e.g., remembering the binary number `110010101001` is hard, but its octal grouping `(110)(010)(101)(001)` → `6251` is much easier: three-item groups become single chunks.

**Evidence of STM in daily life:**
- Looking up a phone number, dialing it, getting a busy tone, and redialing shortly after **without** re-checking the directory — but forgetting it entirely after a few days.

**The Magical Number 7:**
- A person can comfortably handle **≤ 7 items** in short-term memory.
- Beyond 7 items, comprehension becomes **exceedingly difficult**.

**Implication for program development:**
- A small program with few variables is within an individual's easy grasp.
- As independent variables increase, comprehension quickly exceeds an individual's grasping power, requiring disproportionately large effort to master.
- If a *machine* were generating the program instead of a human, the effort-vs-size curve would be **linear** — the exponential blowup is a specifically *human* cognitive limitation.
- **Conclusion:** SE principles exist specifically to counteract these human cognitive limitations and keep the effort-size curve closer to linear.

## 6. Abstraction & Decomposition — The Two Fundamental Techniques ⭐High

The two principles SE relies on most heavily to overcome human cognitive limits:

### Abstraction
- **Definition:** Simplifying a problem by omitting unnecessary details — focusing attention on only one aspect while ignoring others. Also called **model building**.
- **Example:** To understand a country, you wouldn't meet every citizen or examine every tree — you'd study a **map**, an abstract representation capturing only the relevant aspect (geography, roads, etc.).
- **Multiple abstractions possible:** the same problem can have several valid abstractions, each focusing on a different aspect (e.g., political map vs. terrain map vs. climate map).
- **Hierarchy of abstractions:** for complex problems, a single level of abstraction is inadequate — a **hierarchy** may be needed, where a model at one layer is an abstraction of the layer below it, and an implementation of the layer above it.
  - **Example (biological taxonomy):**
  ```
                    Living Organisms
                          │
        ┌─────────┬───────┴───────┬─────────┐
     Animalia   Plantae         Fungae     (Kingdom)
        │           │              │
    Mollusca    Chordata    Ascomycota  Zygomycota  (Phylum)
                    │
                Homo Sapien   Solanum Tuberosum   Coprinus Comatus  (Species)
  ```

### Decomposition
- **Definition:** Decompose a problem into many small, largely independent parts; solve each part separately; the full problem is solved once all parts are solved.
- **Analogy:** it's far easier to break individual sticks than a bundle tied together.
- **Caveat:** arbitrary decomposition doesn't help — the decomposed parts must be reasonably **independent** of one another for the technique to work.
- **Example:** a book is easier to understand when organized into independent chapters, vs. everything mixed together.

## 7. Why Study Software Engineering? ⭐Medium

Three reasons given across the slides:
1. **Handle exponential complexity growth with size** — via systematic techniques based on abstraction (modelling) and decomposition.
2. **Learn systematic techniques** across the lifecycle: specification, design, user interface development, testing, project management, maintenance — and appreciate issues in team development.
3. **Become a better programmer** — higher productivity, better-quality programs.

## 8. Jobs vs Projects vs Exploration ⭐Medium

| Type | Uncertainty of Outcome | Description |
|---|---|---|
| **Jobs** | Very low | Repetition of well-defined, well-understood, routine tasks |
| **Projects** | Moderate | In the middle — mix of challenge and routine |
| **Exploration** | Very high | Outcome highly uncertain, e.g., finding a cure for cancer |

- Software development is classified as a **project** — it has routine elements but also genuine uncertainty/challenge.

## 9. Types of Software Projects ⭐Medium

Two broad categories:
- **Products (Generic software):**
  - **Horizontal market software** — meets needs common across many companies (e.g., office software).
  - **Vertical market software** — designed for a particular industry.
  - Sold as **packaged software** — prewritten, available for purchase.
- **Services (Custom software):**
  - Software developed at a specific user's request; developer typically tailors an existing generic solution rather than building from scratch.
  - Umbrella term covering: **software customization, software maintenance, software testing**, and **contract programmers (CP)** performing coding or other assigned tasks.

**Market context (India-specific, exam-relevant fact):**
- Global software business is worth several trillions of US$, roughly split half products / half services.
- The **services segment is growing faster**.
- **India's IT sector contribution to GDP** rose from ~1.2% (1998) to ~**9.5% (2015)**.
- Indian software companies have historically focused mainly on the **services** segment.

**Factors accelerating growth of services:**
- Large amounts of existing code available in companies → new software built by modifying the closest existing match rather than starting fresh.
- Increased speed of doing business → requires shortening project durations.

**Traditional vs Modern software projects:**
| Traditional (~40 years ago) | Modern |
|---|---|
| Every project started from scratch | Significant reuse; tailoring existing software/libraries |
| Projects were multi-year long | Shorter, incremental delivery |
| Languages (FORTRAN, PASCAL, COBOL, BASIC) offered little reuse scope | Facilitates client feedback and customer participation |
| No GUI — command selection from text menus | Incremental software delivery with evolving functionality |

## 10. Computer Systems Engineering ⭐Low

- Many products require **both software and specific hardware** to run (e.g., a coffee vending machine, a robotic toy, a health-band product).
- **Computer systems engineering** encompasses software engineering — the high-level problem is deciding which tasks are solved by **software** vs. **hardware**.
- Hardware and software are typically developed **together** — a hardware simulator is often used during software development, followed by integration and final system testing.

```
Feasibility Study
        │
        ▼
Requirements Analysis
   & Specification
        │
        ▼
Hardware/Software
   Partitioning
     ┌──┴──┐
     ▼     ▼
 Hardware  Software
   Dev.      Dev.
     └──┬──┘
        ▼
 Integration & Testing

 (Project Management spans all stages)
```

## 11. Emergence & Evolution of Software Engineering Techniques ⭐High

This is a **chronological progression** — a favorite source of sequencing/ordering MCQs.

| Era | Technique | Key Characteristics |
|---|---|---|
| **1950s** | Exploratory / assembly-language programming | No structure; programs limited to a few hundred lines of assembly; every programmer had their own intuitive style (exploratory/build-and-fix). |
| **Early 1960s** | High-level languages (FORTRAN, ALGOL, COBOL) | Greatly reduced development effort; but style was **still exploratory**; program sizes limited to a few thousand lines. |
| **Late 1960s** | **Control flow-based design** | Programs grew larger/more complex; exploratory style proved insufficient; hard to write correct, cost-effective programs and to understand others' code. Advice: "pay attention to control structure design." **Flowcharting** technique developed to represent/design control structure. |
| **Early 1970s** | **Data structure-oriented design** | Realization that data structure design matters more than control structure alone. Program structure is *derived from* the data structure. Example: **Jackson's Structured Programming (JSP)**, developed by Michael Jackson (1970s); also **Warnier-Orr Methodology**. |
| **Late 1970s** | **Data flow-oriented design** | Identify data items input to a system and the processing required to produce outputs. Identifies **processing stations (functions)** and the **data flowing between them**. Generic — can model any system, not just software. Major advantage: **simplicity**. |
| **1980s** | **Object-oriented design** | Natural objects (e.g., employee, payroll-register) in a problem are identified first; relationships among objects — composition, reference, inheritance — are determined. Each object acts as a **data hiding / data abstraction** entity. |

**Evolution diagram (conceptual, from source):**
```
Ad hoc → Control flow-based → Data structure-based → Data flow-based → Object-Oriented
                                                                          │
                                                          ┌───────────────┼───────────────┐
                                                     Component-based  Service-oriented  Aspect-oriented
```

**Object-Oriented advantages (why it gained wide acceptance):**
- Simplicity
- Increased reuse possibilities
- Lower development time and cost
- More robust code
- Easy maintenance

### The GOTO Controversy (High-yield sub-topic)

- Many programmers used assembly languages extensively, where **JUMP instructions** were common for branching — so GOTO-style control was considered "inevitable."
- **Dijkstra** published the article **"Goto Statement Considered Harmful"** (Communications of the ACM) — sparked major controversy; many programmers were initially unhappy and published counter-articles defending GOTO.
- It was eventually **conclusively proven** that only **three programming constructs** are sufficient to express *any* programming logic:
  1. **Sequence** (e.g., `a = 0; b = 5;`)
  2. **Selection** (e.g., `if (c == true) k = 5; else m = 5;`)
  3. **Iteration** (e.g., `while (k > 0) k = j - k;`)
- This became the basis of **Structured Programming**.

### Structured Programming ⭐High

> A program is called **structured** if it uses only sequence, selection, and iteration constructs, and consists of modules.

- Practical exceptions are sometimes permitted: e.g., a premature loop exit (`break`) or exception handling.
- **Advantages of structured programming:**
  - Easier to read and understand
  - Easier to maintain
  - Requires less effort and time for development
  - Less buggy
- **Research finding:** programmers commit fewer errors using structured `if-then-else` and `do-while` constructs compared to test-and-branch (GOTO) constructs.

## 12. Exploratory Style vs Modern Software Development Practices ⭐High

A detailed contrast — very commonly tested as a comparison table:

| Dimension | Exploratory Style (old) | Modern Practices |
|---|---|---|
| Error handling philosophy | Error **correction** after the fact | Emphasis shifted to error **prevention** |
| When errors are detected | Only during testing | As close to the point of introduction as possible, in every phase |
| Role of coding | Coding = program development (synonymous) | Coding is only a **small part** of overall development effort |
| Requirements | Minimal attention | Significant effort on requirements specification |
| Design phase | No distinct design phase | Distinct design phase using standard design techniques |
| Reviews | Absent | Periodic reviews carried out during all stages |
| Testing | Ad hoc | Systematic, standard testing techniques |
| Documentation / Visibility | Poor, inconsistent | Good, consistent — "visibility" makes project management easier |
| Fault diagnosis & maintenance | Difficult (poor docs) | Smoother, due to good documentation |
| Metrics | Not used | Used to support project management and quality assurance |
| Project planning | Minimal/none | Proper estimation, scheduling, monitoring mechanisms; use of **CASE tools** |

**Review Question posed directly in the slides (verbatim-style, likely exam-relevant):**
- *What is structured programming?*
- *What problems may appear if a large program is developed without using structured programming techniques?*

## 13. Life Cycle Models ⭐High

> **Definition:** A software life cycle model (also called a **process model** or **SDLC**) is a descriptive and diagrammatic model of the software life cycle that identifies all activities undertaken during product development, establishes a precedence ordering among activities, and divides the life cycle into phases.

```
        Conceptualize
             │
    Retire ──┼── Specify
             │
   Deliver ──┼── Design
             │
             Code
             │
            Test
   (Cyclic life-cycle wheel)
```

- Each life cycle **phase** consists of several **activities** — e.g., the design stage might include structured analysis, structured design, and design review.

**Why model the life cycle?**
- Helps build **common understanding** of activities among developers.
- Helps identify **inconsistencies, redundancies, and omissions** in the development process.
- Helps in **tailoring** a process model to specific projects.
- Adhering to a chosen model helps develop software in a **systematic and disciplined manner**.

**Single-programmer vs team development:**
- A lone programmer working on a small, graspable problem has freedom to sequence steps flexibly (this is essentially the **exploratory model**, usable in many orders — e.g., Code→Test→Design, or Design→Test→Change Code, or Specify→Code→Design→Test).
- In **team development**, there must be a precise, shared understanding of *when* to do *what* — otherwise it leads to **chaos and project failure** (e.g., one engineer starts coding, another writes the test document first, another defines file structure — with no coordination, the project fails).

**Phase entry and exit criteria:**
- A life cycle model defines entry and exit criteria for every phase.
- A phase is considered complete **only when all its exit criteria are satisfied**.
- Example: exit criteria for the Software Requirements Specification (SRS) phase = the SRS document is complete, reviewed, and **approved by the customer**.
- A phase can start only if its **phase-entry criteria** are satisfied.

**Milestones:**
- Help project managers **track progress**.
- Phase entry and phase exit points are important milestones.

**Life cycle model and project management:**
- With a life cycle model, a manager can fairly accurately state at any time which stage (design/code/test/etc.) the project is in.
- **Without** a life cycle model, tracking is very difficult — the manager depends on team members' guesses, commonly leading to the **"99% complete syndrome"** (a project perpetually reported as "almost done" without a reliable way to verify actual progress).

**Project deliverables — Myth vs Reality:**
| Myth | Reality |
|---|---|
| The only deliverable for a successful project is the working program | Documentation of **all aspects** of software development is needed to support operation and maintenance |

**Commonly used life cycle models (previewed here, detailed in Weeks 2–3):**
- Waterfall model
- V model
- Evolutionary model
- Prototyping model
- Spiral model
- Agile models

**Software life cycle (software process) — series of identifiable stages:**
1. Feasibility study
2. Requirements analysis and specification
3. Design
4. Coding
5. Testing
6. Maintenance

## 14. Classical Waterfall Model ⭐High

Divides the life cycle into the following phases, in strict sequence:
1. Feasibility study
2. Requirements analysis and specification
3. Design
4. Coding and unit testing
5. Integration and system testing
6. Maintenance

```
Feasibility Study
        │
        ▼
Requirements Analysis
        │
        ▼
     Design
        │
        ▼
     Coding
        │
        ▼
     Testing
        │
        ▼
   Maintenance
```

- Described as the **simplest and most intuitive** life cycle model.

**Relative effort across phases (High-yield fact — often asked directly):**
- **Development phases** = feasibility study through testing (excludes maintenance).
- Among **all** life cycle phases, **Maintenance** consumes the **maximum** effort overall.
- Among **development phases specifically**, **Testing** consumes the maximum effort.

**Process Model (organizational context):**
- Most organizations define standards for:
  - Outputs (deliverables) at the end of every phase
  - Entry and exit criteria for every phase
  - Methodologies for specification, design, testing, and project management
- These guidelines collectively form the organization's **software development methodology**, which fresh engineers are expected to master.

## 15. Feasibility Study ⭐High

The **first step** of the life cycle. Main aim: determine whether developing the software is **financially worthwhile** and **technically feasible**.

**Three dimensions of feasibility:**
```
              Economic Feasibility
             (cost/benefit feasibility)
                      │
   Technical ─────────┼───────── Schedule
   Feasibility     Feasibility    Feasibility
   Dimensions      Dimensions     Dimensions
```
1. **Technical feasibility** — can it be built with available technology/skills?
2. **Economic feasibility (cost/benefit)** — is it financially worthwhile?
3. **Schedule feasibility** — can it be completed in the required timeframe?

**What feasibility study roughly determines about customer needs:**
- Data to be input to the system
- Processing needed on that data
- Output data to be produced
- Constraints on system behavior

**Case Study referenced in slides — SPF Scheme for CFL:**
- CFL has 50,000+ employees, mostly casual labourers.
- Mining is a risky profession → casualties are high.
- An existing PF (Provident Fund) scheme has high settlement time.
- Need: a Special Provident Fund (SPF) scheme for **faster disbursement of benefits**.
- Feasibility process illustrated: manager visits main office to find main functionalities required → visits mine site to find data to be input → suggests alternate solutions → determines the best solution → presents to CFL officials → **Go/No-Go decision**.

**Activities during feasibility study:**
1. Work out an overall understanding of the problem.
2. Formulate different solution strategies.
3. Examine alternative strategies in terms of resources required, cost of development, and development time.
4. Perform a **cost/benefit analysis (CBA)** to determine the best solution — or conclude that **none** of the solutions is feasible, due to high cost, resource constraints, or technical reasons.

**Cost-Benefit Analysis (CBA):**
- Identify all **costs**: development costs, set-up costs, operational costs.
- Identify the value of **benefits**.
- Check that benefits are **greater than** costs.

**The Business Case:**
- Benefits of the delivered project must outweigh costs.
- **Costs** include: development, operation.
- **Benefits** can be: quantifiable or non-quantifiable.

---

## Practice Exam — NPTEL Pattern (Self-Test First)

*Attempt all questions before checking the Answer Key. MSQ = more than one option may be correct.*

**Q1 (MCQ).** As per the IEEE definition discussed, software engineering is best described as:
a) A purely creative, unstructured activity
b) The application of a systematic, disciplined, quantifiable approach to development, operation, and maintenance of software
c) Only the coding phase of a project
d) A management-only discipline with no technical content

**Q2 (MCQ).** As per the Standish Group report cited in the lecture, approximately what percentage of software projects were reported as cancelled?
a) 49%
b) 28%
c) 23%
d) 12%

**Q3 (MSQ).** Which of the following are commonly cited problems with software products, per the "software crisis" discussion?
a) Fail to meet user requirements
b) Delivered late
c) Always under budget
d) Difficult to alter, debug, and enhance

**Q4 (MCQ).** In the exploratory (build-and-fix) style, the general sequence of activity is:
a) Design → Specify → Test
b) Initial coding → Test → Fix → repeat until done
c) Requirements → Design → Code → Test → Maintain
d) Test → Design → Code

**Q5 (MCQ).** Why does the exploratory programming style break down for large/non-trivial programs?
a) Because compilers cannot process large programs
b) Because effort, time, and cost grow exponentially with program size under this style
c) Because large programs cannot be tested at all
d) Because hardware costs increase with program size

**Q6 (MCQ).** Per Miller (1956), human memory is conventionally modeled as consisting of which two parts?
a) Working memory and cache memory
b) Short-term memory and long-term memory
c) Sensory memory and procedural memory
d) Episodic memory and semantic memory

**Q7 (MCQ).** "Chunking," as discussed in the context of human cognition, refers to:
a) Deleting unimportant information permanently
b) Grouping several related items together so they occupy a single memory slot instead of several
c) Increasing the total capacity of long-term memory
d) A technique used only in data structure design

**Q8 (MCQ).** According to the "Magical Number 7" concept, comprehension becomes exceedingly difficult when the number of items a person must deal with exceeds approximately:
a) 3
b) 5
c) 7
d) 12

**Q9 (MSQ).** Which of the following are true regarding Abstraction, as discussed in the lecture?
a) It simplifies a problem by omitting unnecessary details
b) It is also called model building
c) A complex problem always has exactly one valid abstraction
d) For complex problems, a hierarchy of abstractions may be needed

**Q10 (MCQ).** The principle illustrated by "it is easier to break individual sticks than a bundle tied together" refers to:
a) Abstraction
b) Decomposition
c) Structured programming
d) Feasibility study

**Q11 (MCQ).** For decomposition to be effective, the decomposed parts of a problem must be:
a) Tightly coupled and interdependent
b) Reasonably independent of each other
c) Of exactly equal size
d) Written in the same programming language

**Q12 (MSQ).** Which of the following are classified as reasons to study Software Engineering, per the lecture?
a) To acquire skills to develop large programs by handling exponential complexity growth
b) To learn systematic techniques of specification, design, testing, and project management
c) To avoid ever having to write documentation
d) To acquire skills to become a better, more productive programmer

**Q13 (MCQ).** In the "Jobs vs Projects vs Exploration" classification, software development is best categorized as:
a) A Job — fully routine and well understood
b) A Project — moderate uncertainty, mix of challenge and routine
c) Pure Exploration — outcome is completely uncertain
d) None of these — it doesn't fit this classification

**Q14 (MCQ).** India's IT sector contribution to GDP, as cited in the lecture, rose to approximately what percentage in 2015 (from ~1.2% in 1998)?
a) 5.5%
b) 9.5%
c) 15%
d) 20%

**Q15 (MCQ).** Which article by Dijkstra is credited with triggering the shift away from GOTO statements toward structured programming?
a) "Structured Programming Considered Essential"
b) "Goto Statement Considered Harmful"
c) "On the Cruelty of Really Teaching Computer Science"
d) "A Discipline of Programming"

**Q16 (MSQ).** Which of the following are among the three constructs proven sufficient to express any programming logic (forming the basis of structured programming)?
a) Sequence
b) Recursion
c) Selection
d) Iteration

**Q17 (MCQ).** In the Classical Waterfall Model, which single life-cycle phase consumes the maximum effort overall (across all phases, including maintenance)?
a) Design
b) Coding
c) Testing
d) Maintenance

**Q18 (MCQ).** Among the *development* phases specifically (feasibility study through testing, excluding maintenance) in the Waterfall Model, which phase consumes the maximum effort?
a) Requirements analysis
b) Design
c) Testing
d) Coding

**Q19 (MCQ).** Without a defined life cycle model, project managers commonly face a tracking problem known as:
a) The critical path problem
b) The 99% complete syndrome
c) The waterfall paradox
d) The feasibility gap

**Q20 (MSQ).** Which of the following are among the three dimensions of feasibility assessed during a feasibility study?
a) Technical feasibility
b) Economic (cost/benefit) feasibility
c) Legal feasibility
d) Schedule feasibility

---

## Answer Key

| Q | Answer | Justification |
|---|---|---|
| 1 | (b) | Matches the IEEE definition given verbatim in the lecture. |
| 2 | (c) 23% | Standish Group figures: 28% successful, 49% delayed/cost overrun, 23% cancelled. |
| 3 | (a), (b), (d) | These are explicitly listed crisis symptoms; "always under budget" contradicts the lecture (projects are typically expensive/over-budget). |
| 4 | (b) | Exploratory style = Initial Coding → Test → Fix → repeat ("Do Until Done"). |
| 5 | (b) | The core reason given is exponential growth of effort/time/cost with size under exploratory style, vs. linear for a machine. |
| 6 | (b) | Miller's 1956 model: short-term memory + long-term memory. |
| 7 | (b) | Chunking groups related items so they occupy one memory slot instead of several — e.g., binary→octal grouping example. |
| 8 | (c) 7 | "The Magical Number 7" — comprehension becomes hard beyond ~7 items. |
| 9 | (a), (b), (d) | Abstraction omits detail and is called model building; complex problems often need a *hierarchy* of abstractions, not a single one — so (c) is false. |
| 10 | (b) | The sticks-bundle analogy specifically illustrates decomposition (breaking a problem into independent parts). |
| 11 | (b) | Decomposition only helps if the resulting parts are reasonably independent; arbitrary splitting doesn't help. |
| 12 | (a), (b), (d) | These three are explicitly listed reasons; documentation is emphasized as necessary, not avoided — so (c) is false. |
| 13 | (b) | Software development sits in the "Projects" category — moderate uncertainty, mix of routine and challenge. |
| 14 | (b) 9.5% | Explicitly cited figure: ~9.5% in 2015, up from ~1.2% in 1998. |
| 15 | (b) | Dijkstra's "Goto Statement Considered Harmful," published in Communications of the ACM. |
| 16 | (a), (c), (d) | Sequence, Selection, and Iteration are the three constructs; recursion is not one of the three named. |
| 17 | (d) | Maintenance consumes the maximum effort among *all* life-cycle phases. |
| 18 | (c) | Among development phases specifically (excluding maintenance), Testing consumes the maximum effort. |
| 19 | (b) | Lack of a life cycle model leads to the "99% complete syndrome" — inability to accurately track real progress. |
| 20 | (a), (b), (d) | The three feasibility dimensions given are Technical, Economic (cost/benefit), and Schedule — "Legal feasibility" is not one of the three named in this lecture. |
