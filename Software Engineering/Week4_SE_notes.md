# Week 4: Requirements Analysis and Specification

**Most likely to be tested (based on general NPTEL SE exam patterns):**
- The **properties of a good SRS document** (concise, unambiguous, consistent, complete, traceable, verifiable) — very frequently turned into "which of the following is/is not a property" MCQs/MSQs.
- **Types of requirement problems** — ambiguity vs. inconsistency vs. incompleteness — tested through short scenario one-liners.
- The **IEEE 830 standard's section numbering** (what goes in 1.x, 2.x, 3.x) — tested as "which section describes X?"
- **Functional vs. non-functional requirements vs. constraints vs. external interfaces** — classifying a given requirement statement into the correct bucket.
- **Decision tables / decision trees** — constructing or reading a table from a word problem (the flight-meal exercise pattern).
- What an **SRS should NOT contain** (design, development plans, product assurance plans) and the **8 categories of "bad" requirements writing** (noise, silence, overspecification, etc.).

---

## 1. Where Requirements Analysis & Specification Fits ⭐ High

> **Definition:** Requirements engineering is the discipline of discovering, understanding, documenting, and validating what a software system is required to do, before design begins.

The process, as this course frames it, is a **cycle**, not a one-shot activity:

```
        needs
          │
          ▼
   ┌─────────────┐
   │  Gathering  │◄──────┐
   └──────┬──────┘       │
          │              │
          ▼              │
   ┌─────────────┐       │
   │  Analysis   │◄──────┤
   └──────┬──────┘       │
          │              │
          ▼              │
   ┌────────────────┐    │
   │ Specification  │◄───┤
   └───────┬────────┘    │
          │              │
          ▼              │
   ┌─────────────┐       │
   │   Review    │───────┘
   └──────┬──────┘
          │
          ▼
   ┌────────────────┐
   │  SRS Document  │
   └────────────────┘
```

- **Gathering → Analysis → Specification → Review** loop back on each other: if review finds a problem, you may have to re-gather, re-analyze, or re-specify.
- The output of the whole cycle is the **SRS (Software Requirements Specification) document.**
- Exam angle: this diagram is often the basis of "which stage comes right after X" or "which stage feeds back into Y" questions.

---

## 2. Requirements Gathering ⭐ High

> **Definition:** Requirements gathering is the activity of collecting information about what the customer/user needs from the system, from existing systems, documents, and stakeholders.

**Techniques used to gather requirements (5 core activities):**
1. Study existing documentation
2. Interview (stakeholders, users)
3. Task analysis
4. Scenario analysis
5. Form analysis (studying forms currently used)

**General approach also includes:**
- Observing existing (manual) systems
- Studying existing procedures
- Discussing with customers and end-users
- Input and output analysis
- Analyzing what needs to be done

**Special difficulty — no existing system to observe:**
- If there is **no working system** to observe, gathering requires a **lot of imagination and creativity**.
- Interacting directly with the customer to gather data **requires a lot of experience**.

**Desirable attributes of a good requirements analyst:**
- Good interaction (interpersonal) skills
- Imagination and creativity
- Experience

**Worked Example — Case Study: Automation of Office Work at the CSE Department**
This case study is the textbook's running example of how gathering actually plays out:
- The department's academic, inventory, and financial information was handled manually by two office clerks, a store keeper, and two attendants.
- Because of a low budget, the HoD assigned the work to a team of **student volunteers** instead of hiring analysts.
- The team was first **briefed by the HoD** on which activities to automate.
- The analysts **interviewed** the two office clerks about their specific tasks to be automated, and also interviewed student/faculty representatives who would use the software.
- For each task, they performed **task and scenario analysis** — asking what steps the task involves and what scenarios might arise.
- They also collected the different types of **forms** being used (**form analysis**).
- They then performed **requirements analysis**: understanding requirements from each user group and identifying inconsistencies, ambiguities, and incompleteness — resolving what they could with users and escalating unresolved issues to the HoD.
- Finally, they documented everything as an **SRS document** (**requirements specification**).

| Case-study action | Gathering technique it demonstrates |
|---|---|
| Briefing by HoD, talking to clerks/students/faculty | Interview |
| Asking steps + possible scenarios per task | Task & Scenario analysis |
| Collecting existing forms | Form analysis |
| Removing inconsistencies/ambiguities, escalating to HoD | Requirements analysis |
| Writing the final document | Requirements specification |

---

## 3. Requirements Analysis: Purpose & Challenges ⭐ High

> **Definition:** Requirements analysis is the process of clearly and thoroughly understanding the user's requirements, and removing all incompleteness, ambiguity, and inconsistency from the initial (raw) statement of the problem.

**Main purposes:**
- Clearly understand user requirements.
- Detect **inconsistencies, ambiguities, and incompleteness**.

**Why it's hard:**
- It is very difficult to get a clear, in-depth understanding of the problem — **especially when there is no working model** of the system to refer to.
- Experienced analysts deliberately take considerable time to clearly understand the exact requirements the customer has in mind — as the slides quote: *"Without a clear understanding of the problem, it is impossible to develop a satisfactory system."*

**Three questions every analyst must be able to answer before moving forward:**
1. What is the problem?
2. What are the possible solutions to the problem?
3. What complexities might arise while solving the problem?

**Detecting subtle problems:**
- Some anomalies/inconsistencies are so subtle that they **escape even experienced eyes**.
- If a **formal specification** of the system is constructed, many of these subtle anomalies and inconsistencies get detected — this is a strong argument for formal/structured specification over plain narrative.

**End result:** inconsistencies and anomalies are removed, and requirements are systematically organized into the **SRS document**.

---

## 4. Types of Requirement Problems: Ambiguity, Inconsistency, Incompleteness ⭐ High

These three terms are commonly tested against short scenario statements, so know the *distinguishing feature* of each.

| Problem | Definition | Worked example from slides |
|---|---|---|
| **Ambiguity** | The requirement statement allows **multiple valid interpretations**. | *"All customers must have the same control field."* → Could mean (1) all control fields follow the same *format*, OR (2) one single control field value is issued for *all* customers. |
| **Inconsistent requirement** | Some part of a requirement **contradicts** another part/requirement. | Customer A: "turn off heater and open water shower when temperature > 100°C." Customer B: "turn off heater and turn ON cooler when temperature > 100°C." — both can't be satisfied together. |
| **Incomplete requirement** | Some requirements are **not included at all**, usually due to oversight. | The analyst never recorded what should happen when temperature falls **below 90°C** (heater should turn ON, water shower should turn OFF) — this case was simply missing from the spec. |

- Exam trap: a question may describe a scenario and ask you to *classify* it as ambiguous vs. inconsistent vs. incomplete — read carefully for whether it's a *missing* case (incomplete), a *contradiction* between two stated rules (inconsistent), or *one statement with two readings* (ambiguous).

---

## 5. The SRS Document: Purpose & Nature ⭐ High

> **Definition:** The Software Requirements Specification (SRS) document is the systematically organized documentation of the requirements arrived at during requirements analysis.

**Main aim of the SRS:**
- Systematically organize the requirements arrived at during requirements analysis.
- Document requirements properly.

**The SRS document is useful in (multiple) contexts:**
- Statement of user needs
- Contract document (between developer and customer)
- Reference document
- Definition for implementation

**SRS as a "black-box" specification:**
- The system is treated as a **black box** whose internal details are not known/documented.
- Only the visible **external (input/output) behaviour** is documented.

```
 Input Data ───►  [ S ]  ───► Output Data
```

**What SRS concentrates on:**
- **What** needs to be done, in terms of input–output behaviour.
- It carefully **avoids the solution ("how to do it")** aspects — that belongs to design, not requirements.

**Language/level:**
- Requirements at this stage are written using **end-user terminology** (not technical/implementation jargon).
- If necessary, a more **formal requirement specification** may be developed from the SRS later (e.g., for design purposes).

---

## 6. Properties of a Good SRS Document ⭐ High

These properties are prime MCQ/MSQ material — expect "which of the following is/is NOT a property of a good SRS" style questions.

| Property | What it means |
|---|---|
| **Concise** | Should not be unnecessarily long-winded, but must not sacrifice clarity — should not be ambiguous either. |
| **Specifies *what*, not *how*** | States what the system must do, without dictating the solution/implementation approach. |
| **Easy to change** | Should be well-structured, so individual requirements can be modified without disturbing unrelated parts. |
| **Consistent** | No two parts of the SRS should contradict each other. |
| **Complete** | All requirements needed to build the system should be present — nothing left to oversight. |
| **Traceable** | You should be able to trace which part of the specification corresponds to which part of the design, code, etc., and vice versa. |
| **Verifiable** | Every requirement should be objectively checkable. Example of a **non-verifiable** requirement: *"system should be user friendly"* — there's no objective test for this. |

- Exam trap: **"user friendly," "fast," "good," "efficient"** without a measurable criterion are classic examples of *unverifiable* / *ambiguous* requirements used as distractor options.

---

## 7. What an SRS Should NOT Include ⭐ High

| Excluded item | Why it's excluded |
|---|---|
| **Project development plans** (cost, staffing, schedules, methods, tools, etc.) | The **lifetime of an SRS lasts until the software is made obsolete**, while development plans have a **much shorter lifetime** — mixing them would make the SRS go stale fast. |
| **Product assurance plans** (Configuration Management, Verification & Validation, test plans, Quality Assurance, etc.) | These have **different audiences** and **different lifetimes** compared to the SRS. |
| **Designs** | Requirements and designs have **different audiences**; requirements analysis and design are **different areas of expertise**. |

- Exam angle: given a list of document contents, identify which ones do **not** belong in an SRS.

---

## 8. The Four Parts of an SRS Document ⭐ High

| Part | What it covers |
|---|---|
| **Functional Requirements** | What the system should do — heart & bulk of the SRS. |
| **External Interfaces** | User, hardware, software, and communication interfaces; file export formats. |
| **Non-Functional Requirements** | Qualities the system must have that can't be expressed as functions (maintainability, portability, usability, security, safety, reliability, performance). |
| **Constraints** | Restrictions on hardware, OS/DBMS, I/O device capabilities, standards compliance, data representation by interfaced systems. |

---

## 9. Functional Requirements (Deep Dive) ⭐ High

> **Definition:** Functional requirements specify all the functionality that the system must support — they form the **heart** of the SRS document and its **bulk**.

**Key rule:** Functional requirements must specify system outputs for given inputs **and** the relationship between them — including **behaviour for invalid inputs**, not just valid ones.

**Functional Requirement Documentation — 3 components:**
1. **Overview** — purpose of the function, approach/techniques used.
2. **Inputs and Outputs** — sources of inputs, destination of outputs, quantities/units of measure, valid ranges, timing.
3. **Processing** — validation of input data, exact sequence of operations, responses to abnormal situations, methods (equations/algorithms) used to transform inputs to outputs.

**Model: system as a set of functions**
- It's desirable to think of every system as performing a set of functions {f₁, f₂, ... fᵢ}.
- Each function fᵢ transforms a set of input data into a corresponding set of output data:

```
 Input Data ───► ( fᵢ ) ───► Output Data
```

**Worked example — F1: Search Book**
```
 Author Name ───► ( F1: Search Book ) ───► Book Details
```
- Input: an author's name.
- Output: details of the author's books and their locations in the library.

**What a high-level functional requirement is:**
- A set of high-level requirements, where each:
  - Takes in some data from the user.
  - Outputs some data to the user.
  - Might consist of a set of identifiable **sub-functions**.
- For each high-level requirement, describe: **input data set, output data set,** and the **processing** required to obtain the output set from the input set.

**"Is it a functional requirement?" — the test:**
- A high-level function is one **using which the user can get some useful piece of work done.**
- Example posed in the slides: *can receipt printing (during an ATM withdrawal) be called a functional requirement on its own?* — A genuine high-level requirement typically involves: accepting data from the user → transforming it into the required response → outputting the response to the user. (Receipt printing alone is a sub-step, not a complete high-level requirement by itself.)

**Use Cases:**
> **Definition:** A use case is a UML term representing a high-level functional requirement.
- Use-case representation is **more well-defined and has agreed documentation standards** compared to a plain high-level functional requirement description.
- Because of this, **many organizations document functional requirements as use cases.**

**Worked examples — Library system functional requirements:**
- **Req. 1 (Search):** Once the user selects "search," they are asked to enter keywords. The system outputs details of all books whose title or author name matches any keyword — details include Title, Author Name, Publisher, Year of Publication, ISBN Number, Catalog Number, Location in the Library.
- **Req. 2 (Renew):** Once "renew" is selected, the user enters membership number and password. After password validation, the list of books borrowed by the user is displayed. The user can renew any book by clicking its corresponding renew box.

**High-level function — a closer view:**
- A high-level function usually involves a **series of interactions** between the system and one or more users.
- Even for the *same* high-level function, there can be **different interaction sequences (scenarios)**, because users may select different options or enter different data.

---

## 10. Non-Functional Requirements ⭐ High

> **Definition:** Non-functional requirements are characteristics of the system that **cannot be expressed as functions** — they describe qualities of the system rather than specific behaviours.

**Categories mentioned:**
- Maintainability
- Portability
- Usability
- Security
- Safety
- Reliability issues
- Performance issues

**Worked example — performance requirement (response time):**
- "How fast can the system produce results?" → At a rate that does not overload another system it supplies data to, etc.
- Example concrete requirement: *"Response time should be less than 1 second, 90% of the time."*
- Crucially — a non-functional requirement **needs to be measurable** (this is the **verifiability** property from Section 6 applied specifically to NFRs).

---

## 11. Constraints & External Interface Requirements ⭐ Medium

**Constraints** (restrictions imposed on the solution):
- Hardware to be used
- Operating system or DBMS to be used
- Capabilities of I/O devices
- Standards compliance
- Data representations by the interfaced system

**External Interface Requirements** (how the system talks to the outside world):
- User interfaces
- Hardware interfaces
- Software interfaces
- Communication interfaces with other systems
- File export formats

---

## 12. Goals of Implementation ⭐ Low

> **Definition:** Goals describe things that are **desirable** of the system but **would not be checked for compliance** (unlike requirements, which are mandatory and verifiable).

- Examples: reusability issues, functionalities to be developed in the future.
- Exam trap: a question may list a "goal" as if it were a requirement — remember goals are **not verified/enforced**, which is what distinguishes them from actual requirements.

---

## 13. The IEEE 830-1998 Standard for SRS ⭐ High

This is one of the most exam-relevant topics of the week — know **what each numbered section contains.**

> **Definition:** IEEE 830-1998 is a standard template/structure for organizing an SRS document.

**Overall document skeleton:**

| Section | Contains |
|---|---|
| Title | — |
| Table of Contents | — |
| **1. Introduction** | Describes purpose of the system, intended audience |
| — 1.1 Purpose | What the system will and will not do |
| — 1.2 Scope | What the system will and will not do |
| — 1.3 Definitions, Acronyms, Abbreviations | Defines the vocabulary of the SRS (may also be in appendix) |
| — 1.4 References | Lists all referenced documents and their sources |
| — 1.5 Overview | Describes how the SRS is organized |
| **2. Overall Description** | Presents the business case & operational concept of the system |
| — 2.1 Product Perspective | External interfaces: system, user, hardware, software, communication; constraints: memory, operational, site adaptation |
| — 2.2 Product Functions | Summarizes the major functional capabilities |
| — 2.3 User Characteristics | Describes technical skills of each user class |
| — 2.4 Constraints | Other constraints limiting developer's options — e.g., regulatory policies, target platform, database, network, development standards |
| — 2.5 Assumptions and Dependencies | — |
| **3. Specific Requirements** | Specifies software requirements in sufficient detail so designers can design the system and testers can verify whether requirements are met; states requirements externally perceivable by users/operators/connected systems; must include, at minimum, every input (stimulus), every output (response), and all functions performed |
| — 3.1 External Interfaces | Detail all inputs and outputs (complements, doesn't duplicate, Section 2 info); examples: GUI screens, file formats |
| — 3.2 Functions | Detailed specifications of each use case, including collaboration and other useful diagrams |
| — 3.3 Performance Requirements | — |
| — 3.4 Logical Database Requirements | Types of data entities and their relationships |
| — 3.5 Design Constraints | Standards compliance and specific software/hardware to be used |
| — 3.6 Software System Quality Attributes | — |
| — 3.7 Object Oriented Models | Class Diagram, State and Collaboration Diagram, Activity Diagrams, etc. |
| **4. Appendices** | — |
| **5. Index** | — |

**Section 3 — alternative organization templates:**
Section 3 (Specific Requirements) doesn't have to be organized only by the 3.1–3.7 scheme above — it can instead be organized based on:
- **Modes**
- **User classes**
- **Concepts (object/class)**
- **Features**
- **Stimuli**

**Worked example — SRS excerpts for "Academic Administration Software" (AAS):**

*3.1 Functional Requirements → 3.1.1 Subject Registration* (concerned with students selecting, adding, dropping, changing a subject):
- **F-001:** The system shall allow a student to register a subject.
- **F-002:** It shall allow a student to drop a course.
- **F-003:** It shall support checking how many students have already registered for a course.

*3.2 Design Constraints:*
- **C-001:** AAS shall provide user interface through standard web browsers.
- **C-002:** AAS shall use an open source RDBMS such as PostgreSQL.
- **C-003:** AAS shall be developed using the JAVA programming language.

*3.3 Non-Functional Requirements:*
- **N-001:** AAS shall respond to a query in less than 5 seconds.
- **N-002:** AAS shall operate with zero downtime.
- **N-003:** AAS shall allow up to 100 users to remotely connect to the system.
- **N-004:** The system will be accompanied by a well-written user manual.

- Exam angle: given a requirement statement like the ones above (F-xxx / C-xxx / N-xxx), be ready to classify it as functional, design constraint, or non-functional.

---

## 14. Examples of Bad SRS Documents ⭐ High

Another classic "identify the flaw type" topic.

| Flaw | Definition | Notes / Example |
|---|---|---|
| **Unstructured Specification** | Writing the SRS as a **narrative essay** — one of the worst formats. | Difficult to change, difficult to be precise, difficult to be unambiguous, leaves scope for contradictions. |
| **Noise** | Presence of text containing information **irrelevant** to the problem. | — |
| **Silence** | Aspects **important to the proper solution are omitted.** | (Same underlying issue as "incompleteness" from Section 4.) |
| **Overspecification** | Addressing **"how to"** aspects instead of "what." | e.g., *"Library member names should be stored in sorted descending order"* — this restricts the designer's solution space unnecessarily. |
| **Contradictions** | The same thing is **described in different, conflicting ways** at several places. | (Related to "inconsistency" from Section 4.) |
| **Ambiguity** | **Literary expressions** or **unquantifiable aspects.** | e.g., "good user interface." |
| **Forward References** | References to aspects of the problem that are **defined only later** in the text. | — |
| **Wishful Thinking** | Descriptions of aspects for which **realistic solutions will be hard to find.** | — |

- Exam trap: distinguish **Overspecification** (dictating *how*, e.g. "sorted descending order") from a normal functional requirement (dictating *what*).

---

## 15. Suggestions for Writing Good Quality Requirements ⭐ Medium

- Keep sentences and paragraphs **short**.
- Use **active voice**.
- Use proper **grammar, spelling, and punctuation**.
- Use **terms consistently** and define them in a **glossary**.
- To check if a requirement is sufficiently well-defined: **read it from the developer's perspective.**
- **Split a requirement into multiple sub-requirements**, because:
  - Each sub-requirement will require **separate test cases** and should be **separately traceable**.
  - If several requirements are strung together in one paragraph, it's easy to **overlook one** during construction or testing.

---

## 16. SRS Review ⭐ Medium

> **Definition:** SRS review is the process of checking a completed SRS document (typically by developers along with user representatives) to confirm it correctly reflects actual user requirements.

- **Who does it:** Developers, along with user representatives.
- **Purpose:**
  - Verify that the SRS conforms to the **actual user requirements**.
  - Detect defects **early** and correct them (cheaper to fix at this stage than later).
- **How it's typically done:** Using a **standard inspection process**, often supported by **checklists**.
- This maps back onto the "Review" stage in the overall cycle diagram from Section 1 — and if review finds a defect, the cycle loops back to gathering/analysis/specification.

---

## 17. Representing Complex Processing Logic: Decision Trees & Decision Tables ⭐ High

Both are ways to represent complex conditional/processing logic in an SRS, especially useful for functional requirements that branch based on user choices.

### Decision Trees

> **Definition:** A decision tree is a diagram where the **edges** represent conditions and the **leaf nodes** represent actions to be performed — it gives a graphic view of the logic involved in decision-making and the corresponding actions taken.

**Worked Example — Library Membership automation Software (LMS):**
LMS should support three options: **New member, Renewal, Cancel membership.**

```
                        ┌──► New member ──► Get details, Create record, Print bill
                        │
 User input ────────────┼──► Renewal    ──► Get details, Update record, Print bill
                        │
                        ├──► Cancel     ──► Get details, Print cheque, Delete record
                        │
                        └──► Invalid option ──► Print error message
```

Detailed walkthrough of each branch:
- **New member:** software asks for name, address, phone number, etc. If proper information is entered: a membership record is created, and a bill is printed for the annual membership charge plus the security deposit payable.
- **Renewal:** LMS asks for the member's name and membership number, and checks validity. If valid: the membership expiry date is updated and the annual membership bill is printed. If not valid: an error message is displayed.
- **Cancel membership:** if a valid member's name is entered: the membership is cancelled, a cheque for the balance amount due is printed, and the membership record is deleted.

### Decision Tables

> **Definition:** A decision table specifies, in tabular form: (1) which variables/conditions are to be tested, (2) what actions are to be taken if the conditions are true, and (3) the order in which decision-making is performed.

- **Upper rows** of the table specify the **variables/conditions** to be evaluated.
- **Lower rows** specify the **actions** to be taken when the corresponding conditions are satisfied.
- **Terminology:** each **column** is called a **rule** — a rule means *"if this condition is true, execute the corresponding action."*

**Worked Example — Decision table for LMS:**

| | Rule 1 | Rule 2 | Rule 3 | Rule 4 |
|---|---|---|---|---|
| **Conditions** | | | | |
| Valid selection | NO | YES | YES | YES |
| New member | -- | YES | NO | NO |
| Renewal | -- | NO | YES | NO |
| Cancellation | -- | NO | NO | YES |
| **Actions** | | | | |
| Display error message | ✓ | | | |
| Ask member's name etc. | | ✓ | ✓ | ✓ |
| Build customer record | | ✓ | | |
| Generate bill | | ✓ | ✓ | |
| Ask membership details | | ✓ | | |
| Update expiry date | | | ✓ | |
| Print cheque | | | | ✓ |
| Delete record | | | | ✓ |

### Decision Tree vs. Decision Table

| | Decision Tree | Decision Table |
|---|---|---|
| Representation | Graphical (branching diagram) | Tabular (rows × columns) |
| Best suited for | Fewer conditions, easy visual tracing of a path | Many conditions/combinations, compact representation |
| Building blocks | Edges = conditions; leaves = actions | Rows = conditions & actions; columns = rules |

### Practice Exercise (from the slides — try it yourself)
> "If the flight is more than half-full and ticket cost is more than Rs. 3000, free meals are served unless it is a domestic flight. The meals are charged on all domestic flights." — Develop a decision table for this.

*Suggested conditions:* Flight > half full? (Y/N); Ticket cost > Rs. 3000? (Y/N); Domestic flight? (Y/N). *Suggested actions:* Serve free meals / Charge for meals. Work through the combinations: free meals only when (flight > half full) AND (cost > 3000) AND (NOT domestic); every domestic flight is charged regardless of the other two conditions.

---

## Practice Exam (NPTEL Pattern)

*Answer each question yourself first, then check the Answer Key at the end.*

**Q1.** Which of the following is NOT one of the standard requirements-gathering activities mentioned in this course?
(a) Interview
(b) Task analysis
(c) Code review
(d) Form analysis

**Q2 (MSQ).** Which of the following are desirable attributes of a good requirements analyst?
(a) Good interaction skills
(b) Imagination and creativity
(c) Experience
(d) Expertise in low-level device driver programming

**Q3.** A requirement states: "All customers must have the same control field." This statement is best classified as:
(a) Incomplete requirement
(b) Inconsistent requirement
(c) Ambiguous requirement
(d) Overspecified requirement

**Q4.** Two customers give contradictory instructions for the same condition (e.g., one says turn ON the cooler, another says open the water shower, both when temperature > 100°C). This is an example of:
(a) Ambiguity
(b) Incompleteness
(c) Inconsistency
(d) Wishful thinking

**Q5.** An analyst fails to record what the system should do when temperature falls below 90°C. This is an example of:
(a) Ambiguity
(b) Incompleteness
(c) Inconsistency
(d) Noise

**Q6.** Why is it particularly difficult to obtain a clear, in-depth understanding of a problem during requirements analysis?
(a) The customer is always uncooperative
(b) There is often no working model of the problem to refer to
(c) Analysts are rarely allowed to meet users
(d) Formal specifications are mandatory by law

**Q7.** In the SRS document, the system is treated as a "black box." This means:
(a) The system's source code must be hidden from the customer
(b) Only external, input-output behaviour is documented; internal details are not
(c) The SRS must not mention any interfaces
(d) The system cannot be tested until it is built

**Q8 (MSQ).** Which of the following are properties of a good SRS document?
(a) Concise
(b) Traceable
(c) Specifies exactly how the system must be implemented internally
(d) Verifiable

**Q9.** Which of the following requirement statements is NOT verifiable?
(a) "Response time should be less than 1 second, 90% of the time."
(b) "The system shall allow a student to register a subject."
(c) "The system should have a user-friendly interface."
(d) "AAS shall respond to a query in less than 5 seconds."

**Q10 (MSQ).** Which of the following should NOT be included in an SRS document?
(a) Project development plans (cost, staffing, schedules)
(b) Functional requirements
(c) Product assurance plans (QA, V&V, test plans)
(d) Design details

**Q11.** According to the course, functional requirements form:
(a) A minor, optional part of the SRS
(b) The heart and bulk of the SRS document
(c) Part of the appendices only
(d) The same thing as non-functional requirements

**Q12.** A functional requirement must specify:
(a) Only the expected output for valid inputs
(b) System behaviour for valid inputs only, leaving invalid inputs undefined
(c) Outputs for given inputs, the relationship between them, and behaviour for invalid inputs too
(d) Only the algorithm to be used internally

**Q13 (MSQ).** Which of the following are examples of non-functional requirements?
(a) Maintainability
(b) "The system shall allow a student to register a subject"
(c) Portability
(d) Security

**Q14.** In the IEEE 830-1998 SRS standard, which section is primarily responsible for describing external interfaces, functions, performance requirements, logical database requirements, design constraints, and object-oriented models in detail?
(a) Section 1 — Introduction
(b) Section 2 — Overall Description
(c) Section 3 — Specific Requirements
(d) Appendices

**Q15.** In the IEEE 830-1998 standard, "1.2 Scope" and "1.1 Purpose" together are meant to describe:
(a) The database schema
(b) What the system will and will not do
(c) The project's budget and staffing plan
(d) UML class diagrams

**Q16 (MSQ).** According to the IEEE 830 standard, Section 3 (Specific Requirements) can alternatively be organized based on:
(a) Modes
(b) User classes
(c) Stimuli
(d) Project budget

**Q17.** A requirement is written as: "Library member names should be stored in a sorted descending order." This is an example of:
(a) Ambiguity
(b) Overspecification
(c) Silence
(d) Forward reference

**Q18.** Writing an entire SRS as a narrative essay is considered a poor practice mainly because:
(a) It takes too long to write
(b) It is difficult to change, difficult to be precise, difficult to be unambiguous, and leaves scope for contradictions
(c) Customers cannot read essays
(d) It violates copyright law

**Q19.** In a decision tree used to represent processing logic, the leaf nodes represent:
(a) Conditions
(b) Actions to be performed
(c) Data types
(d) User inputs

**Q20 (MSQ).** In a decision table, which of the following statements are correct?
(a) A column of the table is called a rule.
(b) Upper rows specify the variables/conditions to be evaluated.
(c) Lower rows specify the actions taken when the corresponding conditions are satisfied.
(d) Decision tables cannot represent more than two conditions.

---

## Answer Key

**Q1: (c)** — Code review is a testing/quality activity, not a requirements-gathering technique; the course lists studying documentation, interview, task analysis, scenario analysis, and form analysis.

**Q2: (a), (b), (c)** — The slides explicitly list good interaction skills, imagination/creativity, and experience as desirable attributes; low-level device driver expertise is unrelated.

**Q3: (c)** — The statement allows multiple interpretations (same format vs. same value for all customers), which is the defining feature of ambiguity.

**Q4: (c)** — Two stated requirements directly contradict each other for the same condition, which is the definition of an inconsistent requirement.

**Q5: (b)** — A case (temperature < 90°C) was simply never recorded — an omission, which defines incompleteness.

**Q6: (b)** — The slides state this difficulty is especially pronounced "if there is no working model of the problem."

**Q7: (b)** — "Black-box specification" means documenting only the visible input/output behaviour, not the internal implementation.

**Q8: (a), (b), (d)** — Concise, traceable, and verifiable are all listed properties; specifying exact internal implementation ("how") is the opposite of what a good SRS should do.

**Q9: (c)** — "User-friendly" is explicitly given as the textbook example of an unquantifiable, unverifiable requirement; the other three have measurable/checkable criteria.

**Q10: (a), (c), (d)** — Development plans, product assurance plans, and designs are all explicitly excluded from the SRS; functional requirements are one of the SRS's four core parts.

**Q11: (b)** — The slides state functional requirements are the "heart" of the SRS and "form the bulk of the document."

**Q12: (c)** — Functional requirements must cover outputs for given inputs, the input-output relationship, and behaviour for invalid inputs as well.

**Q13: (a), (c), (d)** — Maintainability, portability, and security are non-functional qualities; "allow a student to register a subject" is a functional requirement (a specific action the system performs).

**Q14: (c)** — Section 3 (Specific Requirements) contains subsections 3.1–3.7 covering exactly these topics in detail.

**Q15: (b)** — Both 1.1 Purpose and 1.2 Scope are described in the slides as covering "what the system will and will not do."

**Q16: (a), (b), (c)** — The standard explicitly lists modes, user classes, concepts (object/class), features, and stimuli as alternative Section 3 organizations; project budget is never part of an SRS.

**Q17: (b)** — Dictating storage order ("how") rather than required behaviour ("what") is the textbook example of overspecification, which restricts the designer's solution space.

**Q18: (b)** — The slides list exactly these four problems (hard to change, hard to be precise, hard to be unambiguous, scope for contradictions) as the reasons narrative-essay SRS documents are bad.

**Q19: (b)** — In a decision tree, edges represent conditions and leaf nodes represent the actions to be performed.

**Q20: (a), (b), (c)** — All three are explicitly stated definitions/terminology for decision tables; there's no such limit on the number of conditions a decision table can represent.
